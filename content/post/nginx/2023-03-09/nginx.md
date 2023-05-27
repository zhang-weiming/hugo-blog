---
type: posts
reward: true
title: "Nginx代理后，端口丢失和https变为http的问题"
date: 2023-03-09T23:57:22+08:00
tags: ["nginx", "反向代理", "重定向"]
draft: false
author: "张大锅"
categories:
  - Nginx
---

## 问题现象

`project`服务默认使用端口80，我们通过修改配置，将其端口修改为`A`，并增加路由前缀`/project/`。

现在，`project`服务访问地址为：http://x.x.x.x:A/project/。

我们在Nginx里做了一层代理，Nginx配置如下：

``` nginx
   server {
      listen B ssl;
      server_name  y.y.y.y;
      ...
      
      location /project/ {
          proxy_pass http://x.x.x.x:A/project/;
      }
   }
```

代理之后，当`project`服务返回**302重定向**时，端口就会消失，流程如下：

1. 访问`project`主页地址：http://x.x.x.x:A/project/；
2. 查看请求信息，可以看到如下信息，说明**URL重定向到了登录页面，但是丢失了端口**：
    ``` yaml
    General:
      Status Code: 302 Found
    Response Headers：
      Location: https://x.x.x.x/project/signin # 这里给出的地址就是重定向后的目标地址
    ```
3. 手动添加端口后访问页面正常：https://x.x.x.x:A/project/signin

## 初步尝试

最开始的解决方案是修改响应头里的Location字段。
- 参考资料
  - [Apache和Nginx自定义修改Response Header中的Location值](https://www.cnblogs.com/lwx19960428/p/apache-nginx-location-header.html)
  - [Nginx里Header修改](https://www.cnblogs.com/52fhy/p/10166352.html)

但由于**改动过大**，放弃了该方案。

经过进一步查找资料，进行了如下配置。配完以后，发现端口不再丢失，但是协议从https变成了http。

``` nginx
location /project/ {
    proxy_set_header Host $http_host; # 添加了这一行
    proxy_pass http://x.x.x.x:A/project/;
}
```

## 不完美解决方案

其实算是个不完整的Nginx配置，配置步骤如下：

1. 将请求代理到http协议的80端口；
   ``` nginx
   server {
      listen B ssl;
      server_name  y.y.y.y;
      ...
         
      location /project/ {
       # 1、现将请求代理到http协议的B端口（内部映射到80）
       proxy_set_header Host $host:80;
       proxy_pass  http://x.x.x.x:A/project/;
      }
   }
   ```
2. 再将80端口的请求全部重定向到https协议的A端口。
   ``` nginx
   server {
       listen 80;
       server_name  y.y.y.y;
       ...
   
       # 2、将http-80端口的全部请求重定向到https-B端口
       location / {
           return 301 https://x.x.x.x:B$request_uri;
       }
   }
   ```

## 最终解决方案

``` nginx
   server {
      listen B ssl;
      server_name  y.y.y.y;
      ...
         
      location /project/ {
          proxy_pass        http://x.x.x.x:A/project/;
          proxy_redirect    http://           https://;
          proxy_set_header  Host              $host:B;
          proxy_set_header  X-Real-IP         $remote_addr;
          proxy_set_header  X-Forwarded-For   $proxy_add_x_forwarded_for;
      }
   }
```

## 参考

- [**nginx 配置https 并解决重定向后https协议变成了http的问题**](https://blog.csdn.net/ptonlix/article/details/84533088)
- [nginx处理redirect location端口丢失的问题](https://blog.csdn.net/weixin_34186128/article/details/91742483)
- [nginx配置https，重定向后https变成了http](https://www.cnblogs.com/52py/p/12374067.html)
- [Nginx配置http访问自动跳转到https](https://blog.csdn.net/qq_26003101/article/details/112787473)
- [Nginix反向代理---https重定向后变http问题解决](https://blog.csdn.net/qq_29974229/article/details/122250743)
- [深度硬核文:Nginx的301重定向处理过程分析](https://zhuanlan.zhihu.com/p/84539204)
