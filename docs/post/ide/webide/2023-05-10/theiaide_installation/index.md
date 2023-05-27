# Theiaide主机部署


## 简介

theiaide安装过程中诸多报错问题解决记录文档。

- 代码：https://github.com/eclipse-theia/theia
- 文档：https://github.com/eclipse-theia/theia/tree/master/doc#quick-start，theia/doc/Developing.md文件

``` shell
git clone https://kgithub.com/eclipse-theia/theia \
    && cd theia \
    && yarn \
    && yarn download:plugins \
    && yarn browser build \
    && yarn browser start
```

## 问题1：安装依赖报错，前置依赖版本不匹配

- 根据提示，安装相应版本的依赖
```shell
# CentOS安装软件包命令模板
yum install -y <package name>-<version>
```

## 问题2：yarn安装依赖过程中，gyp报错：exit status 2

**报错原因：**

缺少bzip2命令，安装依赖过程中，无法解压压缩包导致报错。

**解决方法：**

安装bzip2命令
``` shell
yum install -y bzip2
```

## theiaide配置文件模块分析

待补充...

## 参考

- [theiaide doc - Github](https://github.com/eclipse-theia/theia/tree/master/doc#quick-start)
  - 部署相关说明部分在`theia/doc/Developing.md`文件中


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/ide/webide/2023-05-10/theiaide_installation/  

