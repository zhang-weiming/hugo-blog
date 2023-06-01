# Docker网络设置


虚拟机里，docker 容器部署的 nacos-ruoyi 无法访问到 docker 容器部署的 mysql 数据库

<!--more-->

## 原因解析

这个问题是由 docker 本身的网络设置导致的。

安装docker时，docker会默认创建一个内部的桥接网络docker0，见下方样例。每创建一个容器分配一个虚拟网卡，容器之间可以根据ip互相访问。
```shell
[root@33fcf82ab4dd /]# [root@CentOS ~]# ifconfig
......
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 0.0.0.0
        inet6 fe80::42:41ff:fe93:7102  prefixlen 64  scopeid 0x20<link>
        ether 02:42:41:93:71:02  txqueuelen 0  (Ethernet)
        RX packets 9374  bytes 737420 (720.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 10553  bytes 171557354 (163.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
......

```

## 解决

1. 输入`docker inspect`命令，查询容器的虚拟网卡IP：
    ```shell
    [root@localhost conf]# docker inspect mysql-ruoyi | grep IPAddress
                ...
                "SecondaryIPAddresses": null,
                "IPAddress": "172.17.0.2",
                        "IPAddress": "172.17.0.2",
                ...
    ```
2. 修改 nacos 启动配置文件中的 mysql IP
3. 重启容器
4. 浏览器输入页面地址，验证访问正常

## 参考

- [Docker容器互访三种方式](https://www.cnblogs.com/shenh/p/9714547.html)


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/docker/2022-09-29/docker%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE/  

