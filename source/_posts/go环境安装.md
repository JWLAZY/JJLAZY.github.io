---
title: go环境搭建
tags: go
date: 2020-05-07
---
# 下载安装包
1. 因为本人使用的是mac使用可以直接下载安装包，地址：https://golang.org/doc/install?download=go1.14.2.darwin-amd64.pkg
2. 下载后双击安装即可
3. 安装包没有修改环境变量，所以终端无法执行go命令，所以安装完后修改 ~/.bash_profile 增加 /usr/local/go/bin到环境变量中
4. source ~/.bash_profile
5. go version 可以看见终端输出版本，安装成功
