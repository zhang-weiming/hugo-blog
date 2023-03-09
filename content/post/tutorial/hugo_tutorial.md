---
title: "hugo开发博客"
date: 2023-02-25
draft: false
tags: ["hugo", "博客"]
author: "张大锅"
---

- 总结日常百度的技术知识
- 记录工作中遇到的技术难题及解决方法
- ...

- [ ] 关键目录说明
- [ ] demo案例

## 博客创建工具

hugo

## 新建博客仓库

``` sh
hugo new site <仓库名>
```

## 关键目录说明

待补充...

## demo案例

待补充...

### 本地起服务

1. 先使用下面的查看本机IP

    ``` shell
    ip a
    ```

2. 找到下图中红色箭头指向的IP地址：
    
    ![查看本机IP](/img/tutorial/ip_a.png)

3. 使用本机IP起服务
    
    ``` shell
    hugo server -D --bind <本机IP> --baseURL=http://<本机IP>
    ```

## 参考

- [Hugo中文文档](https://www.gohugo.org/doc/)
- [Hugo框架中文文档 内容管理 静态文件](https://www.andbible.com/post/hugo-content-management-static-files/)
