---
layout: post
title: VSCode–快速配置PHP调试，浏览器快速调试
date: 2020-05-31
Author: 小萌 
tags: [技术分享]
comments: true
toc: true
---

**使用Adobe Dreamweaver一大段时间了，渐渐发现，DW的软件打开速度太慢。而且，DW也是众收费软件之一。于是，我的代码编辑平台转向了VSCode。**



Visual Studio Code是微软公司发布的免费代码编辑平台，对众多语言均有所支持。再者，考虑到GitHub的托管平台的快速连接，选择VSCode是不二之选。当然，完美的将工作环境以及工作习惯迁移到VSCode，是我选择VSCode的原因。

接下来，为大家讲述一下，在vscode软件下，快速预览PHP代码的方法。

开始。

准备环境：
1.计算机以及网络等正常要求
2.安装 phpstudy 服务器集成开发环境(以小P集成开发为例)
3.正常运行服务器集成开发环境。PHP + apache/nginx
3.Visual Studio Code安装完成

打开vscode界面后，进入PHP页面（新建、输入相关代码）。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_214906.jpg)

在PHP页面的右键下，相关选项如图。

在扩展插件里，搜索 “open php” ，找到相关插件--“open php/html/js in browser”。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_215103.jpg)

安装插件。

在安装完成后，快捷键 “Ctrl + ,” 打开设置界面。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_215255.jpg)

在设置页面，打开 “扩展”-->"open php/html/js in browser"，找到相关配置文件。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_215358.jpg)

在这里，我们需要配置相关服务器来运行PHP文件。

”Custom Url To Open“ --> 将默认localhost改成服务器的网站地址+端口号。
"Document Root Folder" --> 将文件的目录修改为当前服务器目录。
”Selected Browser“--> 修改默认打开浏览器。

接下来，我们返回到PHP文件页面。右键可以发现多出一条选项。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_215434.jpg)

右键点击“在浏览器打开”，便可以将PHP文件在浏览器打开。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/0523/2020-05-23_215604.jpg)效果图

接下来，你就可以更加灵活的编写代码。