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

先使用下面的查看本机IP

``` sh
ip a
```

找到下图中红色箭头指向的IP地址：

![查看本机IP](/img/tutorial/ip_a.png)

使用本机IP起服务

``` sh
hugo server -D --bind 172.28.101.145 --baseURL=http://172.28.101.145
```

## 参考

- [Hugo中文文档](https://www.gohugo.org/doc/)
- [Hugo框架中文文档 内容管理 静态文件](https://www.andbible.com/post/hugo-content-management-static-files/)
