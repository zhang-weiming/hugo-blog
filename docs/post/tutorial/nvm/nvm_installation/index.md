# nvm安装教程


[nvm](https://github.com/nvm-sh/nvm)安装教程，以`v0.39.3`版本为例。

<!--more-->

## 基于git安装（👈推荐）

### 💡前置依赖
- git v1.7.10+

### 🔨安装步骤

1. 克隆nvm仓库到你的用户目录下
   - `cd ~/`，然后`git clone https://github.com/nvm-sh/nvm.git .nvm`
2. `cd ~/.nvm`，然后切换到你想要的版本号（tag），比如v0.39.3 `git checkout v0.39.3`
3. 在你的 shell 环境中激活 nvm：`. ./nvm.sh`

然后在你的环境变量配置文件中，加入以下几行，这样当你下次进入到命令行时会自动激活 nvm：

```shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

此时，你已成功安装`nvm`工具！👏👏👏

### 🚀更新版本

进入用户目录下的.nvm，然后切换到你想要的版本号（tag）即可。

```shell
cd ~/.nvm
git checkout <tag>
```

## 参考

- [nvm安装指导文档](https://github.com/nvm-sh/nvm#git-install)


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/tutorial/nvm/nvm_installation/  

