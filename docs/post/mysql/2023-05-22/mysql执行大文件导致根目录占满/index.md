# MySQL执行较大sql脚本导致服务器跟目录占满


年轻人，要善用临时表...

<!--more-->

## 问题描述

删除一个较大体量的数据库后，发现mysql无法正常执行sql脚本，并给出以下报错：
``` shell
[error]/tmp/ib1tJjCi file has no space left
```
同时，发现服务器磁盘根目录满了！
``` shell
[root@template ~]# df -h
Filesystem                Size  Used Avail Use% Mounted on
/dev/vda3                  16G   15G  20K  100% /
devtmpfs                   32G     0   32G   0% /dev
tmpfs                      32G     0   32G   0% /dev/shm
tmpfs                      32G  3.3G   29G  11% /run
tmpfs                      32G     0   32G   0% /sys/fs/cgroup
/dev/mapper/data-data_lv  600G   21G  579G   4% /data
/dev/vda1                 497M  123M  375M  25% /boot
tmpfs                     6.3G     0  6.3G   0% /run/user/1002
```

## 问题定位

执行命令：
```shell
[root@template ~]# lsof |egrep 'tmp|deleted'
...
mysqld    19544 20112          mysql   13u      REG              253,3          0    8412343 /tmp/ibX4BLkY (deleted)
mysqld    19544 20112          mysql  281u      REG              253,3          0    8414596 /tmp/MLhfq6Il (deleted)
mysqld    19544 20137          mysql    6u      REG              253,3          0    8388677 /tmp/ib70QbfZ (deleted)
mysqld    19544 20137          mysql    7u      REG              253,3          0    8412302 /tmp/ibrctchx (deleted)
mysqld    19544 20137          mysql    8u      REG              253,3          0    8412305 /tmp/ibhPedj5 (deleted)
mysqld    19544 20137          mysql    9u      REG              253,3          0    8412317 /tmp/ib1tJjCi (deleted)
mysqld    19544 20137          mysql   12uW     REG              252,0   12582912  537507500 /data/mysql/ibtmp1
mysqld    19544 20137          mysql   13u      REG              253,3          0    8412343 /tmp/ibX4BLkY (deleted)
mysqld    19544 20137          mysql  281u      REG              253,3          0    8414596 /tmp/MLhfq6Il (deleted)
mysqld    19544 20138          mysql    6u      REG              253,3          0    8388677 /tmp/ib70QbfZ (deleted)
mysqld    19544 20138          mysql    7u      REG              253,3          0    8412302 /tmp/ibrctchx (deleted)
mysqld    19544 20138          mysql    8u      REG              253,3          0    8412305 /tmp/ibhPedj5 (deleted)
mysqld    19544 20138          mysql    9u      REG              253,3          0    8412317 /tmp/ib1tJjCi (deleted)
...
```
发现`mysqld`进程有大量临时文件没有释放磁盘空间。

## 进一步定位

进入mysql安装目录，发现ibtmp1文件非常大
```shell
-rw-r----- 1 mysql mysql  41K May 22 12:33 ib_buffer_pool
-rw-r----- 1 mysql mysql 268M May 23 00:13 ibdata1
-rw-r----- 1 mysql mysql 3.0G May 23 00:13 ib_logfile0
-rw-r----- 1 mysql mysql 3.0G May 23 00:13 ib_logfile1
-rw-r----- 1 mysql mysql 142G May 22 23:57 ibtmp1
```

## 解决

1. 修改 my.cnf 配置文件

在 [mysqld] 下添加如下配置：
```editorconfig
[mysqld]
...
innodb_temp_data_file_path = ibtmp1:12M:autoextend:max:5G
```

2. 进入mysql命令行，设置 innodb_fast_shutdown 参数
```mysql-sql
SET GLOBAL innodb_fast_shutdown = 0;
```

3. 关闭 mysql 服务
```shell
systemctl stop mysqld
```

4. 删除 ibtmp1 文件（重启过程中会自动删除）

5. 启动 mysql 服务
```shell
systemctl start mysqld
```

## 知识链接

`innodb_fast_shutdown`参数有3个值：
- 0
- 1 (默认值)
- 2

支持全动态局设置。

使用场景：在做数据库关闭升级的时候`set global innodb_fast_shutdown=0`，这样能最大保障数据的完整性。

- 设置为1：关闭MySQL的时候不会做清除脏页和插入缓冲区的合并操作，也不会将脏页刷新到磁盘
- 设置为0：会做清除脏页和插入缓冲区的合并操作，也会将脏页全部刷新到磁盘上面去，但是这个时候关闭的速度也是最慢的
- 设置为2：不会做清除脏页和插入缓冲区的合并操作，也不会将脏页刷新到磁盘，但是会刷新到redo log里面，再下次启动mysql的时候恢复


## 参考
- [mysql导致根目录爆满_MYSQL临时表导致根分区爆满问题分析](https://blog.csdn.net/weixin_30332165/article/details/113221115)
- [MySQL · 故障处理 · ibtmp1 文件过大](https://huiraoo.github.io/blog/2020/08/05/mysql-ibtmp1/)
- [Mysql innodb_fast_shutdown](https://www.cnblogs.com/Presley-lpc/p/9177081.html)


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/mysql/2023-05-22/mysql%E6%89%A7%E8%A1%8C%E5%A4%A7%E6%96%87%E4%BB%B6%E5%AF%BC%E8%87%B4%E6%A0%B9%E7%9B%AE%E5%BD%95%E5%8D%A0%E6%BB%A1/  

