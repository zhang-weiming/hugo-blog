---
type: posts
reward: true
title: "K8S部署MySQL-5.7"
date: 2023-05-21
draft: false
tags: ["k8s", "mysql"]
author: "张大锅"
categories:
  - MySQL
---

## k8s部署MySQL 5.7

### ConfigMap

``` yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: mysql
  labels:
    app: mysql
data:
  my.cnf: |-
    [client]
    default-character-set=utf8mb4
    [mysql]
    default-character-set=utf8mb4
    [mysqld]
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci
    init_connect='SET NAMES utf8mb4'
    skip-character-set-client-handshake = true
    max_connections=2000
    secure_file_priv=/var/lib/mysql
    bind-address=0.0.0.0
    symbolic-links=0
    sql_mode='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'
```

### Service

``` yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: mysql
  name: mysql-svc
  namespace: mysql
spec:
  type: NodePort
  ports:
    - name: http
      port: 3306
      protocol: TCP
      targetPort: 3306
  selector:
    app: mysql
```

### Deployment

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  namespace: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - args:
            - --datadir
            - /var/lib/mysql/datadir
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: root
            - name: MYSQL_USER
              value: user
            - name: MYSQL_PASSWORD
              value: user
          image: mysql:5.7
          name: mysql-container
          ports:
            - containerPort: 3306
              name: dbapi
          volumeMounts:
            - mountPath: /var/lib/mysql
              name: mysql-storage
            - name: config
              mountPath: /etc/mysql/conf.d/my.cnf
              subPath: my.cnf
      volumes:
        - name: mysql-storage
          hostPath:
            path: /data/k8s/volumes/mysql
            type: Directory
        - name: config
          configMap:
            name: mysql-config
        - name: localtime
          hostPath:
            type: File
            path: /etc/localtime
```
