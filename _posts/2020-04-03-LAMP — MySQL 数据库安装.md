---
layout: post
title: LAMP — MySQL 数据库安装
date: 2020-04-03
Author: 小萌 
tags: [网站搭建]
comments: true
toc: true
---

**介绍一下在 CentOS 7 上安装 mysql 数据库。由于 MySQL 项目被 甲骨文公司收购，CentOS 作为开源项目，需要避免闭源的潜在危险。CentOS 7 开始，采取 MySQL 开源分支--MariaDB数据库来代替 MySQL 数据库。当然，MariaDB 与 MySQL 使用方式大同小异，MariaDB 完全可以代替 MySQL 。**

因此，后面可能在书面上出现 MySQL 与 MariaDB 的交集出现，两者本质上一致。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/images/50.jpg)

开始 。

1. 执行如下命令，下载并安装 MariaDB 数据库：
   `yum -y install mariadb mariadb-server`

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image7.png)安装 MariaDB 服务

  2.启动数据库、设置为开机自启：
`systemctl start mariadb.service //启动服务`
`systemctl status mariadb.service //服务状态`
`systemctl enable mariadb.service //服务开机自启`

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/mairadb.png)

3. 执行如下命令，修改 MariaDB 数据库 **root** 用户的密码，并提高 MariaDB 数据库的安全性。
   `mysql_secure_installation //初始化数据库信息`

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image9.png)配置 数据库

- 默认密码为空，所以提示 Enter current password for root (enter for none) 时，输入 回车（enter） 就可以。

- 提示 Set root password? [Y/n] ，输入 y。输入新的密码，例如: 123123。后面还有一系列的配置确认，一路输入 y回车即可。

**注意：**
（1）输入的密码不会显示出来。为了便于演示，我们设置的密码很简单，在真实的生产环境中一定要设置复杂度高的密码，以免被暴力破解。
（2）设置 MariaDB 根密码仅是保护数据库的最基本措施。在构建或安装数据库驱动的应用程序时，用户通常可以为该应用程序创建数据库服务用户，并避免使用根账户执行除数据库管理以外的操作。

4.输入如下命令，进入 MariaDB 数据库；然后，查看root账号下的数据库信息。
`mysql -uroot -p //进入MariaDB数据库`
输入设置的密码。
`show databases;`

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/033001/image10.png)进入 数据库

至此，CentOS 7上安装数据库完成。

![img](https://blaclacloud.coding.net/p/tcshare/d/tcsharea/git/raw/master/image/images/46.jpg)

新的一周，应该有新的气象，向前，向前 !!!