---
type: posts
reward: true
title: "TheiaIDE安装部署时，可能出现的几个问题"
date: 2023-05-10
draft: false
tags: ["theia", "ide", "webide", "error"]
author: "张大锅"
categories:
  - ide
---

在安装TheiaIDE过程中，遇到诸多报错问题，在此记录一下问题解决过程。

官方给出的安装过程相关命令，简洁的让人觉得不简单...

<!--more-->

``` shell
git clone https://kgithub.com/eclipse-theia/theia \
    && cd theia \
    && yarn \
    && yarn download:plugins \
    && yarn browser build \
    && yarn browser start
```

## [Theia](https://theia-ide.org/) 源码和官方文档

- 源码：https://github.com/eclipse-theia/theia
- 文档：https://github.com/eclipse-theia/theia/tree/master/doc#quick-start
  - theia/doc/Developing.md

## 可能遇到的问题以及解决方法

### 问题1：安装依赖报错，前置依赖版本不匹配

根据提示，安装各个依赖的对应版本即可。

CentOS安装软件包命令模板：
```shell
yum install -y <package name>-<version>
```

### 问题2：g++报错，无法识别命令参数 `-std=gnu++14`

报错如下：

```shell
...
make: Entering directory `/root/theiaide/theia/node_modules/nsfw/build'
  CXX(target) Release/obj.target/nsfw/src/NSFW.o
g++: error: unrecognized command line option ‘-std=gnu++14’
make: *** [Release/obj.target/nsfw/src/NSFW.o] Error 1
make: Leaving directory `/root/theiaide/theia/node_modules/nsfw/build'
```

解决：

1. 安装前置依赖 scl
    ```shell
    yum install -y centos-release-scl
    ```
2. 安装 gcc 8 版本
    ```shell
     yum install -y devtoolset-8-gcc devtoolset-8-gcc-c++
    ```
    devtoolset-8中的gcc版本为gcc 8，除此之外还有如下版本：
    ```text
     devtoolset-3: gcc 4.9
     devtoolset-4: gcc 5
     devtoolset-6: gcc 6
     devtoolset-7: gcc 7
     devtoolset-8: gcc 8
    ```
3. 备份已有 gcc/g++ 命令，更新成 gcc/g++8
    ```shell
     mv /usr/bin/gcc /usr/bin/gcc-bak4.8.5
     mv /usr/bin/g++ /usr/bin/g++-bak4.8.5
     ln -s /opt/rh/devtoolset-8/root/bin/gcc /usr/bin/gcc
     ln -s /opt/rh/devtoolset-8/root/bin/g++ /usr/bin/g++
    ```
4. 查看版本
    ```shell
    [root@localhost ~]# gcc --version
    gcc (GCC) 8.3.1 20190311 (Red Hat 8.3.1-3)
    Copyright (C) 2018 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
    
    [root@localhost ~]# g++ --version
    g++ (GCC) 8.3.1 20190311 (Red Hat 8.3.1-3)
    Copyright (C) 2018 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
    
    ```

### 问题3：yarn安装依赖过程中，gyp报错：exit status 2

报错原因：

缺少`bzip2`命令，安装依赖过程中，无法解压 .bz2 压缩包进而报错。

解决：

- 安装`bzip2`命令
  ``` shell
  yum install -y bzip2
  ```
- 删除 node_modules 目录
- 再次执行 yarn

### 问题4：yarn安装electron报错

报错如下：
```shell
error /root/theiaide/theia/node_modules/electron: Command failed.
Exit code: 1
Command: node install.js
Arguments:
Directory: /root/theiaide/theia/node_modules/electron
Output:
RequestError: connect ETIMEDOUT 20.205.243.166:443
    at ClientRequest.<anonymous> (/root/theiaide/theia/node_modules/electron/node_modules/got/source/request-as-event-emitter.js:178:14)
    at Object.onceWrapper (node:events:628:26)
    at ClientRequest.emit (node:events:525:35)
    at ClientRequest.origin.emit (/root/theiaide/theia/node_modules/electron/node_modules/@szmarczak/http-timer/source/index.js:37:11)
    at TLSSocket.socketErrorListener (node:_http_client:481:9)
at TLSSocket.emit (node:events:513:28)
```

解决：

设置环境变量：
```shell
export NODE_TLS_REJECT_UNAUTHORIZED=0
```

## 参考

- [TheiaIDE 文档 - Github](https://github.com/eclipse-theia/theia/tree/master/doc#quick-start) 部署相关文档在`theia/doc/Developing.md`文件中
- [centos安装python3详细教程](https://zhuanlan.zhihu.com/p/469429564)
- [centos下升级g++版本](https://blog.csdn.net/qq_53332653/article/details/110817130)
