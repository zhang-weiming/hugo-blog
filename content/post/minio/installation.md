---
type: posts
reward: false
keywords:
- Docker
- minio
title: "Docker部署minio"
date: 2023-09-30
draft: false
tags: ["Docker", "minio"]
author: "张大锅"
categories:
  - minio
---

docker部署minio过程记录

<!--more-->

## 1. 准备工作

1.1 拉取镜像：

```shell
docker pull minio/minio
```

1.2 创建目录

```shell
mkdir /data/minio
```

## 2. 部署

2.1 启动minio容器

```shell
docker run -p 19000:9000 -p 19090:9090 --name minio -d --restart=unless-stopped \
    -e "MINIO_ROOT_USER=minio" \
    -e "MINIO_ROOT_PASSWORD=123456" \
    -v /data/minio/data:/data \
    -v /data/minio/config:/root/.minio \
    minio/minio server /data \
    --console-address ":9000" --address ":9090"
```

## 3. 访问minio操作台

浏览器访问`http://localhost:19000`，看到如下页面，部署完成。

![minio操作台登录页面](/img/minio/minio-console-page.png)
