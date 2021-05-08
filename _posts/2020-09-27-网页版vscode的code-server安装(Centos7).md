---
layout: post
title: 网页版vscode的code-server安装(Centos7)
date: 2020-09-27
Author: 小萌 
tags: [实用教程,在线编程]
comments: true
toc: true

---



> 使用docker 安装code-server，也就是vscode的在线版
>
> 渐渐的docker技术被西方抛弃了，然而docker的魅力以及便利性无处不在

## 安装docker

安装docker

```html
yum -y install docker 
systemctl start docker
systemctl enable docker
```

## 配置docker镜像加速地址

1. 修改daemon.json这个文件

   ```html
   vi /etc/docker/daemon.json
   ```

2. 配置仓库的镜像地址(建议阿里云首个)

   ```html
   "registry-mirrors": [
           "https://1nj0zren.mirror.aliyuncs.com",
           "https://docker.mirrors.ustc.edu.cn",
           "http://f1361db2.m.daocloud.io",
           "https://registry.docker-cn.com"
       ]
   ```

3. 重新加载下这个配置文件，并重启docker

   ```htmkl
   systemctl daemon-reload
   systemctl restart docker
   ```

## 拉取code-server镜像

```html
docker pull codercom/code-server
```

这个过程比较漫长，因为要下载大约800MB+

![image-20200927162816985](https://i.loli.net/2020/09/27/cxOumVQt1LdCqva.png)

输入命令,查看拉去的镜像

```html
docker images
```

![image-20200927162918303](https://i.loli.net/2020/09/27/RKq6vsUXI4HFfnZ.png)

## 启动镜像

```html
docker run -p 8081:8081 -v "/app:/home/coder/project" --privileged=true -e PASSWORD='123456' -d $IMAGE ID --allow-http
```

其中，需要简单配置一下端口以及images id 、密码口令

```html
启动命令的一些解释tips:
-p 是映射宿主机和docker容器的端口号
privileged=true 是忽略掉挂在目录权限问题，不然后面vscod无法创建文件
-v 挂载容器卷，是映射宿主机的目录和容器的目录，app目录是我自己建的文件夹
-e 设置密码
-d 后台启动容器
d07f57675529是要启动的镜像id,你的可能跟我不一样。可以用docker images命令查看
–allow-http 运行http方式访问
```

## 用浏览器访问vscode

ok

##### 