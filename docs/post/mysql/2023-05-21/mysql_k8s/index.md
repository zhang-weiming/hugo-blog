# K8S部署MySQL 5.7


- 使用`ConfigMap`自定义mysql相关配置
- 持久化目录挂载
- NodePort方式暴露端口

<!--more-->

### ConfigMap

```yaml
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

```yaml
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

这里是用`hostPath`方式挂载了主机目录，不推荐在生产环境中使用这种目录挂载方式，因为一旦Pod重启，可能会由于重新调度而发生漂移，新Pod被起在其他机器节点上，导致数据丢失。

建议使用`nfs`，以`PVC`的形式挂载持久化数据目录。

```yaml
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


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/mysql/2023-05-21/mysql_k8s/  

