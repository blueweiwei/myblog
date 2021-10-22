---
layout: post
title: 邮件 API Power Automate
date: 2021-10-08
Author: 小萌 
tags: [ 技术分享 ]
comments: true
toc: true

---


> 利用 Power Automate 自动流，实现邮局api


## Power Automate(简称 PA)

官方文档介绍：

```JavaScript
- 自动化业务流程

- 发送过期任务的自动提醒

- 在计划中系统之间移动业务数据

- 连接到接近 300 个数据源或任何公开发布的 API

- 甚至可以在本地计算机中自动执行任务，如在 Excel 中计算数据。
```


因为PA好多模板是基于微软的邮件进行通知，所以PA 在使用outlook发邮件的时候，可以连续发信。因此，萌生了，用PA 联合 outlook，实现简单的发信api。

普通程序使用 smtp进行发信，经常会出现发现间隔过短会造成发信失败。然鹅使用PA ，自家 outlook 可以一秒内发信多次，大大提高发信的成功率。

## 原理

使用微软官方的 Power Automate （flow 流）服务，构建发信api。

## 演示笔记

#### 登录 Power Automate 平台

官网传送门 : [Power Automate | Microsoft Power Platform](https://flow.microsoft.com/zh-cn/)

![image.png](https://i.loli.net/2021/10/08/dyZYOmGszWRhHIg.png)

### 创建流

![image_1.png](https://i.loli.net/2021/10/08/K6zt2finMedbo9u.png)

控制台 → 创建 → 即时云端流 → 触发方式 （当收到 HTTP 请求时）→ 创建

![image_2.png](https://i.loli.net/2021/10/08/z713wavnUNsWjCJ.png)

## 构建流

### 构建请求头

![image_3.png](https://i.loli.net/2021/10/08/Ok7MxgnXZc8Sb41.png)

点击 使用示例有效负载生成 架构，填入你想要请求的参数。

当前只演示比较简单的邮件，具体请按照自己意愿处理。


![image_4.png](https://i.loli.net/2021/10/08/KNPHRgBTaock9nm.png)

![image_5.png](https://i.loli.net/2021/10/08/vWChdM7aQBKIYJk.png)

点击 新步骤

### 绑定邮件信息

![image_6.png](https://i.loli.net/2021/10/08/E1fKIydQPOZDaVz.png)


选择 发送电子邮件 操作

![image_7.png](https://i.loli.net/2021/10/08/sSg3y9dWalpGBfC.png)


填入相关动态内容

### 返回响应（可有可无）

完成邮件后，我们api需要返回一个状态码

![image_8.png](https://i.loli.net/2021/10/08/CUmIprF1gqyjE5c.png)


![image_9.png](https://i.loli.net/2021/10/08/9lHViFOuGnyaZpE.png)

也就是，只要流状态卫200，即返回 json数据 

### 保存即可

保存。

返回 构建请求头处，获取HTTP POST URL

![image_10.png](https://i.loli.net/2021/10/08/uwE2ItNLC4fsKbP.png)

### 测试

![image_11.png](https://i.loli.net/2021/10/08/mbJhYEPro9TuV8Z.png)

![image_12.png](https://i.loli.net/2021/10/08/i74djfeqlaXHLx8.png)

连续多点几下请求，邮箱收到很多。具体还得自行测试。

## 简单聊一下

相比之下，更愿意使用SMTP进行发信，但是自己服务器容易出现发信失败。

PA 在绑定自己邮箱的时候，尽量使用office365的账号，使用普通账号，可能outlook发信有限制。发信可能会出现到垃圾箱，如果是自己使用，可以添加收件人白名单。为什莫会进垃圾箱，不做探讨。

有相关不完善的地方，还请指正。

ps: 文章只是提供了一种比较稳定的发信方案，有资金还是使用邮局方便。

