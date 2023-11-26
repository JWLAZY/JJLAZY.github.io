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
npm全程node package manger, 是管理第三方nodejs库的工具。

npm包管理工具和其他包管理工具不太一样的地方是下载的包在当前项目的node_modules文件夹中。所以如果你有很多前端项目就会导致你的电脑硬盘紧张，因为每个前端项目都会自己保留一份需要的第三方库，不会集中管理。

### NPM使用
每一个nodejs项目都会有一个package.json文件。可以理解这个文件是这个nodejs项目的使用说明书，其中包含了项目的说和项目的各种启动脚本和依赖的第三方包。

#### 创建node项目

创建node项目也就是创建一个package.json文件，然后再丰富启动脚本和依赖的第三方库。

**创建命令**
```
  npm init
```
实例：
![s](https://r2.lizhitech.work/images/npm_init.png)

...
执行完成后就会在项目文件中创建一个package.json的文件，这时项目就初始化了。接下来就配置启动命令和第三方库就可以了。

**下载第三方库**
```
npm install react
```
**启动脚本**
```
npm run command(start,build,test,etc...)
```
# NRM
...
