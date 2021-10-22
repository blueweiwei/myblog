---
layout: post
title: sharelist 安装教程之阿里云盘
date: 2021-10-22
Author: 小萌 
tags: [ 技术分享 ]
comments: true
toc: true
---

> 简单的一个sharelist 安装教程

## 用途

sharelist 是一个比较优秀的开源网盘挂载服务。

官方仓库：`https://github.com/reruin/sharelist`

当前可用仓库: `https://github.com/blueweiwei/sharelist_new`

官方仓库现在已经更新，推荐用docker安装。我的仓库，还是保留着当前可用的源文件版本。

```
ShareList 是一个易用的网盘工具，支持快速挂载 GoogleDrive、OneDrive 、天翼云、蓝奏云等，可通过插件扩展功能。

主要功能：多种网盘系统快速挂载、支持虚拟目录和虚拟文件、支持目录加密、插件机制、国际化支持，WebDAV导出。

```

## 下载与安装

**linux下** :

```linux
#Debian/Ubuntu系统
apt-get -y install git

#CentOS/RHEL系统
yum -y install git

# 需要安装好node 以及pm2

#下载源码安装
git clone https://github.com/blueweiwei/sharelist_new.git
cd sharelist && bash install.sh
```

如果没有安装node.js 以及 PM2，需要提前安装好

具体可用查看  [Node.js 安装配置 | 菜鸟教程 (runoob.com)](https://www.runoob.com/nodejs/nodejs-install-setup.html)

```
# 安装 pm2 
npm install pm2 -g
```

在此，访问`http://ip:33001`

## 挂载阿里云盘

访问`http://ip:33001` 后，初始化后台口令。

登陆 `http://ip:33001/manage` 进入后台后，

![image-20211022224552292](https://i.loli.net/2021/10/22/XZpE5uxoelSAJfd.png)

保存之后,进入首页进行输入refreshToken

手机安装好 阿里云盘 客户端

进行登陆

文件管理路径找到 `Android/data/com.alicloud.databox/files/logs/trace/`

在找到的bin文件,里面有RefreshToken的值.

填入即可.



