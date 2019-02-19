---
layout:     post
title:      Centos7安装Nginx
subtitle:   快速实现Centos7安装Nginx
date:       2019-02-19
author:     SYP
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Centos
    - Linux
    - Nginx
    - Yum


---

> 正所谓前人栽树，后人乘凉。
>
> 感谢[BY](http://qiubaiying.top)提供的博客模板
>
> [我的的博客](http://songyp.github.io)

## 安装Nginx

```
yum install -y nginx
```

## Nginx默认目录

输入命令：

```
whereis nginx
```

即可看到类似于如下的内容：

```
nginx: /usr/sbin/nginx /usr/lib64/nginx /etc/nginx /usr/share/nginx
```

以下是Nginx的默认路径：

(1) Nginx配置路径：/etc/nginx/
(2) PID目录：/var/run/nginx.pid
(3) 错误日志：/var/log/nginx/[error](https://www.centos.bz/tag/error/).log
(4) 访问日志：/var/log/nginx/access.log
(5) 默认站点目录：/usr/share/nginx/html

事实上，只需知道Nginx配置路径，其他路径均可在/etc/nginx/nginx.conf 以及/etc/nginx/conf.d/default.conf 中查询到。

## 常用命令

(1) 启动：

```
nginx
```

(2) 测试Nginx配置是否正确：

```
nginx -t
```

(3) 优雅重启：

```
nginx -s reload
```

(4) 查看nginx的进程号：

```
ps -ef |grep nginx
```

(5)nginx服务停止

```
nginx -s stop
kill -9 pid
```

当然，Nginx也可以编译源码安装，步骤相对要繁琐一些，总的来说，还是比较简单的，本文不作赘述

## 参考文章

<https://www.shangxuejun.com/article/14>

