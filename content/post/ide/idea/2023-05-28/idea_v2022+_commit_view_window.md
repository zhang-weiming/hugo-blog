---
type: posts
reward: true
title: "IDEA 2022版本没有commit对话框"
date: 2023-05-28T04:18:06+08:00
draft: false
tags: ["idea", "commit"]
author: "张大锅"
categories:
  - ide
---

## 需求

![img.png](/img/ide/idea/2023-05-28/img.png)

老版本的IDEA在project下面都有一个commit的对话框，但是在2022版本默认没有这个。

## 解决

打开方式：Settings -> Version Contrl -> Commit，勾选上`Use non-modal commit interface`，则还原为老版本。

![img_1.png](/img/ide/idea/2023-05-28/img_1.png)


## 参考

- [IDEA 2022版本没有commit 对话框](https://blog.csdn.net/ISaiSai/article/details/124907435)