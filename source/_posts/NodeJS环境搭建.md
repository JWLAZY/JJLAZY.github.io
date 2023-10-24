---
title: NodeJS环境搭建
date: 2023-10-24 11:17:48
tags: [NodeJS, JavaScript]
categories: [NodeJS]
---

# 前言
本文章主要讲解如何搭建NodeJS项目常用配置，适合没有接触过NodeJS的同学，如果已经接触过NodeJS可以忽略。

# NVM
nodejs有很多版本，而有些开源库对nodejs的版本有要求，所以我们需要在电脑上安装各种各样的nodejs版本并且需要可以随时切换，如果我们自己配置文件夹配置切换脚本就太复杂了，所以采用了NVM(node version manager)。这个工具可以帮我们下载各个版本的Nodejs，并且可以随时切换。

NVM的官方地址：[点击](https://github.com/nvm-sh/nvm)

## 安装步骤

只需要按照文档中执行安装命令即可。
安装命令
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```
在终端中执行。

**注意**

如果下载进度不走的话，应该是被墙了。需要给终端设置代理。如何配置代理需要自己研究下。
```
export http_proxy=127.0.0.1:7890;
export https_proxy=$http_proxy；
```
## 安装成功如下图

![Alt text](https://s2.loli.net/2023/10/24/X2PcEQOF7NGqCdv.png)

## NVM常用命令
![Alt text](https://s2.loli.net/2023/10/24/C4OpLoSwlYbHtiU.png)


**nvm ls** :展示nodejs版本列表

**nvm ls-remote**:展示服务器上所有的nodejs版本

**nvm install version**:安装制定版本的nodejs

**nvm alias default 18.16.0**:设置默认nodejs版本，每次打开终端都是这个版本

**nvm use version**:临时切换到指定版本

# NPM
...
# NRM
...
