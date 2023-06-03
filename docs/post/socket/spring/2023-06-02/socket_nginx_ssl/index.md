# websocket服务在nginx中代理后无法正常连接


nginx配置中，在443端口配了ssl证书，基于nginx代理地址访问websocket服务异常。

<!--more-->

后端项目，使用SpringBoot框架，并基于spring自带的websocket功能开启了websocket服务。

在连接socket地址的时候发现，直连服务地址没问题，但是通过nginx代理地址连接异常，有如下报错：

```text
websocket Error: write EPROTO 66931976:error:100000f7:SSL routines:OPENSSL_internal:WRONG_VERSION_NUMBER:../../../../src/third_party/boringssl/src/ssl/tls_record.cc:242:
...
```

经过对比排查后发现，nginx代理的 location 块配置有问题。

## 解决

原来的 location 配置：
```editorconfig
location /api/ {
    proxy_pass http://x.x.x.x:8080;
    proxy_read_timeout 1200;#设置等待后台响应时间
    proxy_next_upstream error timeout invalid_header http_500 http_503 http_404;
    proxy_cookie_path / /;
    client_max_body_size    1000m;
    proxy_set_header Host $proxy_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $remote_addr;
}
```

修改后的 location 配置：
```editorconfig
location /api/ {
    proxy_pass http://x.x.x.x:8080;
    proxy_read_timeout 1200;#设置等待后台响应时间
    proxy_next_upstream error timeout invalid_header http_500 http_503 http_404;
    proxy_cookie_path / /;
    client_max_body_size    1000m;
    proxy_set_header Host $proxy_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $remote_addr;
    
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection \"upgrade\";
}
```


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/socket/spring/2023-06-02/socket_nginx_ssl/  

