---
layout:     post
title:      亲测本地电脑同时配置gitlab和github账号
subtitle:   同时配置gitlab和github账号
date:       2019-03-22
author:     SYP
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Git
---

## 简介

我自己的git账号属于GitHub, 公司使用的是GitLab，电脑已经配置了公司的GitLab账号了。虽然家里也有电脑，但是平时工作的一些总结什么的，想发到自己的GitHub上，所以，我就想在自己电脑上**既能使用GitLab又能使用GitHub**。
## 思路
ssh 方式链接到 Github／GitLab，需要唯一的公钥，如果想同一台电脑绑定两个Github/GitLab 帐号，需要两个条件:
***1.  能够生成两对 私钥/公钥***
***2.  push 时，可以区分两个账户，推送到相应的仓库***
### 解决方案
***1.  生成 私钥/公钥 时，密钥文件命名避免重复***
***2.  设置不同 Host 对应同一 HostName 但密钥不同***
***3.  取消 git 全局用户名/邮箱设置，为每个仓库独立设置 用户名/邮箱***
## 操作步骤
*本操作步骤是在windows环境下操作的*
### 1.  查看已生成的秘钥
git bash下输入命令 ls ~/.ssh/，看到 id_rsa 与 id_rsa_pub 则说明已经有一对密钥
`$  ls ~/.ssh`
![image.png](https://upload-images.jianshu.io/upload_images/16384352-cde87cdb4bdd06e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 生成新公钥
生成新的公钥，并命名为 **id_rsa_gitlab** (保证与之前密钥文件名称不同即可,文件名最好有意义，否则写后面的配置的时候写错文件名，我的文件名是id_rsa_gitlab）
>***我计划id_rsa用于github,id_rsa_gitlab用于gitlab***

`ssh-keygen -t rsa -f ~/.ssh/id_rsa_gitlab -C "yourmail@xxx.com"`

如下图：
![image.png](https://upload-images.jianshu.io/upload_images/16384352-e4ff91bbfe072ca7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
上面命令执行完，～／.ssh下就出现了"_gitlab"结尾的文件
![image.png](https://upload-images.jianshu.io/upload_images/16384352-cd7168f0e1215472.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 配置config文件
在 **.ssh 文件夹**下新建 **config **文件并编辑，令不同 **Host 实际映射到同一HostName**，但密钥文件不同。Host 前缀可自定义：
```
# default                                                                       
Host github.com
HostName github.com
User songyp
IdentityFile ~/.ssh/id_rsa
# two                                                                           
Host gitlab.com
HostName gitlab.com
User git
IdentityFile ~/.ssh/id_rsa_gitlab
```
>      *#Host myhost（这里是自定义的host简称，以后连接远程服务器就可以用命令ssh myhost）[注意下面有缩进]*
>      *#User 登录用户名(如：git)*
>      *#HostName 主机名可用ip也可以是域名(如:github.com或者bitbucket.org)*
>      *#Port 服务器open-ssh端口（默认：22,默认时一般不写此行*
>      *#IdentityFile 证书文件路径（如~/.ssh/id_rsa_\*)*

我的配置如下：
![image.png](https://upload-images.jianshu.io/upload_images/16384352-a053c631a7573e8a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 使用SSH密钥连接Github
使用SSH密钥连接Github网上教程很多，这里不再赘述

### 测试 ssh 链接
```
ssh -T git@gitlab.com
ssh -T git@github.com
# Hi XXX! You've successfully authenticated, but GitHub does not provide shell access.
# 出现上边这句，表示链接成功
```
### 取消全局 用户名/邮箱设置，并进入项目文件夹单独设置
```
# 取消全局 用户名/邮箱 配置
git config –global –unset user.name
git config –global –unset user.email
# 单独设置每个repo 用户名/邮箱
git config user.email “xxxx@xx.com”
git config user.name “xxxx”
```
> PS：
> （1）git config命令要到工程目录下（反正就是git目录）执行，否则是出错的，下面就是不在git目录下执行的结果：后来我恍然大悟，然后切换到工程目录下执行就OK了。
> （2）“单独设置每个repo 用户名/邮箱”这个步骤，我就是跑到工程下，执行git config user.email “xxxx@xx.com”和git config user.name “xxxx”命令。看来以后每次我GitHub／GitLab clone一个新的工程下来，都要在clone完成后，在这个工程目录下执行这两条语句来配置。【解决办法】：工作电脑平时使用公司的gitlab比较多，可以把公司的账户设置为全局，然后在单独的需要用别的账号的工程下配置对应的账号。这样就不用频繁地做这个配置。（这个全局设置与单独工程下设置地顺序不做要求)

### 最后
后边你就可以进行git操作了，如clone、push等