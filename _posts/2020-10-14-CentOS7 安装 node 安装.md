---
layout: post
title: CentOS 7 安装 Node.js
date: 2020-10-14
Author: 小萌 
tags: [技术分享]
comments: true
toc: true


---



> 简单记录一下，在CentOS 7 环境下安装Node.js

### 开始

##### 一、环境介绍

系统版本：CentOS Linux 7 (Core)

内核版本：Linux version 4.16.13-1.el7.elrepo.x86_64

##### 二、安装node.js

###### 1、确认依赖环境

确认服务器有nodejs编译及依赖相关软件，如果没有可通过运行以下命令安装。

```
#yum -y install gcc gcc-c++ openssl-devel
```

###### 2、下载Node.JS源码包并解压

进入要存放下载资源的目录，本文存放在/usr/local/src/目录下。然后执行命令下载源码包：

```
#cd /usr/local/src/
#wget https://npm.taobao.org/mirrors/node/v14.13.1/node-v14.13.1-linux-x64.tar.xz
```

解压

```
#tar -xvf node-v14.13.1-linux-x64.tar.xz
```

解压完成后重命名文件夹，将文件夹重命名为node（非必须）：

```html
#mv node-v14.13.1-linux-x64 node
```

###### 3、测试是否安装成功

进入 node 目录下的bin目录，执行 ls命令：

```
cd node/bin && ls 
```

会看到node和npm，使用如下命令：

```
./node -v
```

![image-20201014175355598](https://i.loli.net/2020/10/14/whkKztcOFsq9PSQ.png)

图：这里本人下载的两个中 ，node1 为使用的源码。

如果看到v14.13.1，则说明安装成功。

###### 4、设置全局

现在node和npm还不能全局使用，我们要添加环境变量，首先在 root 目录下找到 .bash_profile 文件，编辑：

```
vim ~/.bash_profile
```

找到PATH=$PATH:$HOME/bin，在后面添加路径：/usr/local/src/node/bin，添加后的结果如下（注意冒号）：

![image-20201014175653261](https://i.loli.net/2020/10/14/LKHE3i1NRsWZUrA.png)

保存修改，然后使用如下命令使配置生效：

```
source ~/.bash_profile
```

5、验证全局

在任意位置执行node -v命令，查看是否输出node版本号，如果是，则全局设置生效。现在可以在任何目录下执行node和npm命令了！

这里，就可以在任何文件目录下，使用node/bin的node、npm、npx 操作。

### 结束