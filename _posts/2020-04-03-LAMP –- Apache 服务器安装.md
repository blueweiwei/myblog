---
layout: post
title: LAMP –Apache 服务器安装
date: 2020-04-03
Author: 小萌 
tags: [网站搭建]
comments: true
toc: true

---

**今天介绍一下 在 Linux CentOS 7 服务器上安装 Apache 服务器。**

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/images/83.jpg)

开始。

1.使用 SSH 工具连接到服务器端。

```
yum -y install httpd
```

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image1.png)SSH 成功连接

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image2.png)安装 Apache

2. 执行如下命令，安装 Apache 的扩展文件。

```
yum -y install httpd-manual mod_ssl mod_perl mod_auth_mysql
```

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image3.png)安装 Apache 扩展文件

同样看到这个“ 完毕! ”，表示安装完成。

3. 执行如下命令，启动 apache http 服务。

```
systemctl start httpd.service //启动服务`
`systemctl status httpd.service //服务状态`
`systemctl enable httpd.service //服务开机自启
```

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/httpdstatus.png)httpd 服务启动

4. 打开本地浏览器，并访问 **服务器公网地址**，可以查看到 Apache 的测试页面。证明 Apache HTTP 服务部署启动成功。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image6.png)本地浏览器 测试页

5. 这里，如果无法正常访问，需要查看一下 firewalld 是否开放 80 端口 ，如果作为初学者，可以采用临时关闭防火墙的方法。
   部分命令：
   `systemctl status firewalld //服务器 firewalld 开启状态`
   `systemctl stop firewalld //关闭服务器 firewalld`
   `systemctl start firewalld //开启服务器 firewalld`

在 firewalld开启的情况下开放固定端口：
`firewall-cmd --zone=publsic --list-ports //查看已开放端口`
`firewall-cmd --zone=public --**add**-port=**5672**/**tcp** --permanent //开放5672的tcp端口`
`firewall-cmd --zone=public --**remove**-port=**5672**/**udp** --permanent //关闭5672的udp端口`

至此，能够 正常访问**服务器公网地址**并看到页面 ，CentOS 7的 apache 服务器安装成功。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/images/75.jpg)

Apache 服务器安装成功后，就可以在服务器上放置静态html网页，能够进行基本的访问。后续将给大家介绍 动态交互网页 PHP以及 数据库 MaraDB 的安装以及注意事项。

Thank for look forwod to my Blog ! My friends ！！！