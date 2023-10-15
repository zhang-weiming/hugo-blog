---
type: posts
reward: false
keywords:
- DST
- server
title: "搭建饥荒联机版Linux服务器"
date: 2023-10-14
draft: false
tags: ["DST", "server"]
author: "张大锅"
categories:
  - Games
  - DST
---

在 Ubuntu 系统中搭建饥荒联机版服务器。

<!--more-->

## 搭建步骤

### 1. 安装steamcmd

  64位机器：
  ```shell
  sudo dpkg --add-architecture i386 # If running a 64bit OS
  sudo apt-get update
  sudo apt-get install libstdc++6:i386 libgcc1:i386 libcurl4-gnutls-dev:i386
  ```
  32位机器：
  ```shell
  sudo apt-get update
  sudo apt-get install libstdc++6 libgcc1 libcurl4-gnutls-dev
  ```

  更多信息请参考：https://developer.valvesoftware.com/wiki/SteamCMD

### 2. 配置服务器令牌

1) 访问[Klei Accounts 网站](https://accounts.klei.com/)并登录您的帐户。（请注意，该游戏的 Xbox 和 PlayStation 版本不支持专用服务器。）。

![klei account log in](/img/games/dst/klei-account-log-in.png)

以steam为例，点击steam图标，跳转到steam登录页面，登录成功后，点击下方绿色按钮：

![link steam account to klei](/img/games/dst/steam-link-klei.png)

之后会跳转回[Klei Accounts 网站](https://accounts.klei.com/account/info)。

2) 登录成功后，在帐户页面上，访问“**GAMES**”选项卡，然后向下滚动到“饥荒联机版”并单击“**Game Servers**”按钮。

![klei games](/img/games/dst/klei-games.png)

3) 如果没有任何服务器，单击“**Add New Server**”按钮进行注册。如果有，单击绿色的“**Configure Server**”按钮。

![server list](/img/games/dst/dst-server-list.png)

4) 在“Configure Server”页面中，您将找到一个包含一些选项的表单，您可以编辑这些选项来自定义您的服务器。准备好后，单击“**Download Settings**”按钮。下载 Zip 存档，解压内容，并将文件夹“MyDediServer”放入**~/.klei/DoNotStarveTogether/**中。

![configure server form](/img/games/dst/configure-server-form.png)

### 3. 创建将运行服务器的脚本

[下载此 shell 脚本](https://accounts.klei.com/assets/gamesetup/linux/run_dedicated_servers.sh)并将其移至~/run_dedicated_servers.sh

### 4. 赋予脚本可执行权限

  在终端中，运行：chmod u+x ~/run_dedicated_servers.sh

### 5. 运行脚本来启动专用服务器

  在终端中，运行：~/run_dedicated_servers.sh

## 参考

- [Forums - Klei](https://forums.kleientertainment.com/forums/topic/64441-dedicated-server-quick-setup-guide-linux/)
