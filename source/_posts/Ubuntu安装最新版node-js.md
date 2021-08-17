---
title: Ubuntu安装最新版node.js
date: 2021-08-17 20:13:07
tags:
- 编程
- nodejs
- npm
- ubuntu
- linux
- vps
- 服务器
- 乌班图
---

这篇文章教大家在Ubuntu下安装nodejs最新版本

命令如下

```shell
cd ~
apt-get update
wget -O nodejs_latest.sh https://raw.githubusercontent.com/nodesource/distributions/master/deb/setup_current.x
bash nodejs_latest.sh
apt install nodejs
```

安装完成使用 `nodejs -V` 和 `npm -V` 检测`nodejs`和`npm`版本