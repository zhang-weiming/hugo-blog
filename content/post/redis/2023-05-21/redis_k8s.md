---
type: posts
reward: true
title: "K8S部署Redis 3.0.7"
date: 2023-05-21
draft: false
tags: ["k8s", "mysql"]
author: "张大锅"
categories:
  - Redis
---

- 使用`ConfigMap`自定义redis相关配置
- NodePort方式暴露端口

<!--more-->

### ConfigMap

```yaml
kind: ConfigMap
apiVersion: v1
metadata:
  name: redis-config
  namespace: redis
  labels:
    app: redis
data:
  redis.conf: |-
    dir /srv
    port 6379
    bind 0.0.0.0
    appendonly yes
    daemonize no
    #protected-mode no
    requirepass abc@12345678
    pidfile /srv/redis-6379.pid

```

### Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: redis
  namespace: redis
  labels:
    app: redis
spec:
  type: NodePort
  ports:
    - name: tcp
      port: 6379
      nodePort: 30379
  selector:
    app: redis

```

### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis
  namespace: redis
  labels:
    app: redis
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis
        image: redis:3.0.7
        command:
          - "sh"
          - "-c"
          - "redis-server /usr/local/redis/redis.conf"
        ports:
        - containerPort: 6379
        resources:
          limits:
            cpu: 1000m
            memory: 1024Mi
          requests:
            cpu: 1000m
            memory: 1024Mi
        livenessProbe:
          tcpSocket:
            port: 6379
          initialDelaySeconds: 300
          timeoutSeconds: 1
          periodSeconds: 10
          successThreshold: 1
          failureThreshold: 3
        readinessProbe:
          tcpSocket:
            port: 6379
          initialDelaySeconds: 5
          timeoutSeconds: 1
          periodSeconds: 10
          successThreshold: 1
          failureThreshold: 3
        volumeMounts:
        - name: config
          mountPath:  /usr/local/redis/redis.conf
          subPath: redis.conf
      volumes:
      - name: config
        configMap:
          name: redis-config
```
