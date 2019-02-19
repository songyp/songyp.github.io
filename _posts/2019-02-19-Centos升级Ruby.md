---
layout:     post
title:      Centos升级Ruby
subtitle:   快速实现Centos升级Ruby
date:       2019-02-19
author:     SYP
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Centos
    - Linux
    - Ruby

---

> 正所谓前人栽树，后人乘凉。
>
> 感谢[BY](http://qiubaiying.top)提供的博客模板
>
> [我的的博客](http://songyp.github.io)

## 前言

在安装jekyll时，所需要的使用ruby工具进行操作，发现在线安装的Ruby版本过低，jekyll支持的版本最少为2.1。

```
[root@VM_16_3_centos ~]# gem install jekyll
Fetching: public_suffix-3.0.3.gem (100%)
ERROR:  Error installing jekyll:
        public_suffix requires Ruby version >= 2.1.
```

## 在线安装ruby 

使用[yum](https://www.baidu.com/s?wd=yum&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)在线安装ruby，安装的版本为2.0.0。

`yum install ruby`

`ruby -v`

```
[root@VM_16_3_centos ~]# ruby -v
ruby 2.0.0p648 (2015-12-16) [x86_64-linux]
[root@VM_16_3_centos ~]# 
```

## 添加ruby仓库

### 添加aliyun镜像并检测Ruby版本

`gem sources -a http://mirrors.aliyun.com/rubygems/` 

## 安装RAM

> RAM（[Ruby Version Manager](https://rvm.io/) ）是一款RAM的命令行工具，可以使用RAM[轻松安装](https://www.baidu.com/s?wd=%E8%BD%BB%E6%9D%BE%E5%AE%89%E8%A3%85&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)，管理Ruby版本。RVM包含了Ruby的版本管理和Gem库管理(gemset)

可以使用如下命令进行安装RAM：

`gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`

`curl -sSL https://get.rvm.io | bash -s stable`

更新配置文件，使其立马生效：

`source /etc/profile.d/rvm.sh`

查看RVM版本信息，如果可以代表安装成功。

`rvm -v`

```
[root@VM_16_3_centos ~]# rvm -v
rvm 1.29.7 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
[root@VM_16_3_centos ~]# 
```

接下来查看Ruby版本：

`rvm list know`

```
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.10]
[ruby-]2.2[.10]
[ruby-]2.3[.7]
[ruby-]2.4[.4]
[ruby-]2.5[.1]
[ruby-]2.6[.0-preview2]
ruby-head
 
# for forks use: rvm install ruby-head-<name> --url https://github.com/github/ruby.git --branch 2.2
 
# JRuby
jruby-1.6[.8]
jruby-1.7[.27]
jruby-9.1[.17.0]
jruby[-9.2.0.0]
jruby-head
 
# Rubinius
rbx-1[.4.3]
rbx-2.3[.0]
rbx-2.4[.1]
rbx-2[.5.8]
rbx-3[.100]
rbx-head
 
# TruffleRuby
truffleruby[-1.0.0-rc2]
 
# Opal
opal
 
# Minimalistic ruby implementation - ISO 30170:2012
mruby-1.0.0
mruby-1.1.0
mruby-1.2.0
mruby-1.3.0
mruby-1[.4.0]
mruby[-head]
 
# Ruby Enterprise Edition
ree-1.8.6
ree[-1.8.7][-2012.02]
 
# Topaz
topaz
 
# MagLev
maglev-1.0.0
maglev-1.1[RC1]
maglev[-1.2Alpha4]
maglev-head
 
# Mac OS X Snow Leopard Or Newer
macruby-0.10
macruby-0.11
macruby[-0.12]
macruby-nightly
macruby-head
 
# IronRuby
ironruby[-1.1.3]
--------------------- 
```

安装Ruby，从上面查到的信息随便找一个比2.2.2版本要高的就行：

`rvm install 2.5`

验证版本：

`ruby -v`

```
[root@VM_16_3_centos ~]# ruby -v
ruby 2.5.3p105 (2018-10-18 revision 65156) [x86_64-linux]
[root@VM_16_3_centos ~]# 
```

成功升级。

## 注意：

> 如果使用rvm安装发现下载缓慢，可以考虑删除原来的仓库地址，只保留[阿里云](https://www.baidu.com/s?wd=%E9%98%BF%E9%87%8C%E4%BA%91&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)镜像。

`gem sources --remove https://rubygems.org/`

## 参考文章

https://blog.csdn.net/qq_26440803/article/details/82717244

