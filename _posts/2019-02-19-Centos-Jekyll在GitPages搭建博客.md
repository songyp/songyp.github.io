---
layout:     post
title:      Centos7-使用Jekyll在GitPages搭建博客
subtitle:   快速实现Centos7-使用Jekyll在GitPages搭建博客
date:       2019-02-19
author:     SYP
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Centos
    - Linux
    - Nginx
    - Git
    - Jekyll



---

> 正所谓前人栽树，后人乘凉。
>
> 感谢[BY](http://qiubaiying.top)提供的博客模板
>
> [我的的博客](http://songyp.github.io)

## 前言

> 安装Git并拉取分支，部署Jekyll

## 安装Git 

这一步的教程略过 安装过程可以百度 关键词 git安装 git教程

## 拉取代码

在项目页，找到原谅色按钮”clone or download”复制链接，通常为”https://github.com/用户名/项目名.git”。 
调出命令行： 

`git clone https://github.com/用户名/项目名.git`

## 安装Ruby 

`yum install ruby `

如果出现ruby版本过低错误，请参考我另外一篇文章 [Centos升级Ruby](https://songyp.github.io/2019/02/19/Centos%E5%8D%87%E7%BA%A7Ruby/)

## 安装Jekyll

`gem install jekyll`

## 配置Jekyll

`cd jekyll path // 移动到你的jekyll项目下，也就是你从git里clone下来的项目`

`jekyll serve // 启动服务，默认链接地址\"http:localhost:4000\`

期间遇到的一个问题：

```
Configuration file: /Users/czre/git/blog/_config.yml
       Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
  Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/! 
```

这个原因是因为没有jekyll-paginate，使用gem install jekyll-paginate安装一下就好了。 
另外也有可能出现没有jekyll-gist错误，解决方法同上，这些错误取决模板所采用的一些服务。 

 `jekyll server -H 127.0.0.1 --incremental`

将此脚本命令设置为后台执行，SSH客户端断开继续执行

`ctrl + z`

`bg 1`

## 安装&配置Nginx

安装nginx略过

对nginx.conf进行修改，可通过whereis nginx查看具体的nginx.conf的位置

把nginx.conf添加 一个虚拟域名解析（根据不同的端口或者域名来配置），把监听root目录为clone下来的文件夹里面_site即可

## 完成

ngin绑定_site之后，即可通过域名或者ip+端口的形式进行访问了