# Docker服务启动时，容器自动被拉起


每次启动虚拟机，docker 服务会自动启动，同时发现是总是有几个不需要的容器会被自动拉起...

期望是，docker服务自启动或重启后，正在运行中的容器中只有我们想要的。

<!--more-->

## 原因解析

出现这个现象是因为在之前使用`docker run`命令拉起容器时，使用了`--restart=always`参数设置导致的。

`--restart`的参数值有以下4个：

- no：容器退出时，不重启容器。
- on-failure：只有在非0状态退出时才从新启动容器。
- always：无论退出状态是如何，都重启容器。
- unless-stopped：在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器。

## 解决

更新容器的`--restart`参数：
```shell
docker update --restart=on-failure <容器ID|容器名称>
```

在之后拉起容器的时候，不要随意使用`--restart=always`参数项。

## 参考

- [Docker 容器开机启动设置](https://www.xiexianbin.cn/docker/client/2017-05-21-docker-restart-policies/index.html)


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/docker/2022-09-29/docker%E6%9C%8D%E5%8A%A1%E5%90%AF%E5%8A%A8%E6%97%B6%E5%AE%B9%E5%99%A8%E8%87%AA%E5%8A%A8%E8%A2%AB%E6%8B%89%E8%B5%B7/  

