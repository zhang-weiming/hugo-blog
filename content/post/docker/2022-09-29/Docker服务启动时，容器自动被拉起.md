---
type: posts
reward: true
title: "Docker服务启动时，容器自动被拉起"
date: 2022-09-29
draft: false
tags: ["Docker", "container", "restart"]
author: "张大锅"
categories:
  - Docker
---

## 问题描述

每次启动虚拟机，docker 服务会自动启动，同时发现总是有几个容器会自动被启动。

而我们期望的是，docker服务自启动后，运行中的容器列表为空。

## 问题原因解析

这个问题是由 docker run 命令中的 \-\-restart=always 参数设置导致的。

\-\-restart 具体参数值有以下4个：

- no : 容器退出时，不重启容器
- on-failure : 只有在非0状态退出时才从新启动容器
- always : 无论退出状态是如何，都重启容器
- unless-stopped : 在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器

## 解决

- docker update --restart=on-failure <容器ID|容器名称>

## 参考

- [Docker 容器开机启动设置](https://www.xiexianbin.cn/docker/client/2017-05-21-docker-restart-policies/index.html)
