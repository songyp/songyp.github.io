---
layout:     post
title:      亲测申请Let's encrypt免费证书
subtitle:   快速申请Let's encrypt免费证书
date:       2019-02-28
author:     SYP
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - SSL

---
> 注意：请在一台能访问公网的Linux机器上操作 参考文档：[Let’s Encrypt 泛域名证书免费申请 - 云+社区 - 腾讯云](https://cloud.tencent.com/developer/article/1157919)

## 安装[acme.sh](https://github.com/Neilpang/acme.sh)及申请证书

**登录可连接外网的Linux服务器**，本教程以192.168.50.221为例

```
[michael_yuanding@yuanding-2014 ~]$ su - root
密码：
[root@yuanding-2014 ~]# 
```

*注：我这台服务器不能以root用户登录，然后我切换到root用户进行操作（普通用户请自己进行尝试）*

**下载acme.sh**

`wget -O - https://get.acme.sh | sh`

```bash
[root@yuanding-2014 ~]# wget -O - https://get.acme.sh | sh
--2019-02-28 10:18:14--  https://get.acme.sh/
正在解析主机 get.acme.sh... 144.217.161.63, 2607:5300:201:3100::5663
正在连接 get.acme.sh|144.217.161.63|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：705 [text/plain]
正在保存至: “STDOUT”

100%[====================================================================================================>] 705         --.-K/s   in 0s      

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     02019-02-28 10:18:23 (203 MB/s) - 已写入标准输出 [705/705]

100  170k  100  170k    0     0  25752      0  0:00:06  0:00:06 --:--:-- 46265
[2019年 02月 28日 星期四 10:18:30 CST] Installing from online archive.
[2019年 02月 28日 星期四 10:18:30 CST] Downloading https://github.com/Neilpang/acme.sh/archive/master.tar.gz
[2019年 02月 28日 星期四 10:18:43 CST] Extracting master.tar.gz
[2019年 02月 28日 星期四 10:18:43 CST] It is recommended to install socat first.
[2019年 02月 28日 星期四 10:18:43 CST] We use socat for standalone server if you use standalone mode.
[2019年 02月 28日 星期四 10:18:43 CST] If you don't use standalone mode, just ignore this warning.
[2019年 02月 28日 星期四 10:18:43 CST] Installing to /root/.acme.sh
[2019年 02月 28日 星期四 10:18:43 CST] Installed to /root/.acme.sh/acme.sh
[2019年 02月 28日 星期四 10:18:43 CST] Installing alias to '/root/.bashrc'
[2019年 02月 28日 星期四 10:18:43 CST] OK, Close and reopen your terminal to start using acme.sh
[2019年 02月 28日 星期四 10:18:43 CST] Installing alias to '/root/.cshrc'
[2019年 02月 28日 星期四 10:18:43 CST] Installing alias to '/root/.tcshrc'
[2019年 02月 28日 星期四 10:18:43 CST] Installing cron job
[2019年 02月 28日 星期四 10:18:43 CST] Good, bash is found, so change the shebang to use bash as preferred.
[2019年 02月 28日 星期四 10:18:43 CST] OK
[2019年 02月 28日 星期四 10:18:43 CST] Install success!
```

**DNSPOD token申请**

![11.png](https://upload-images.jianshu.io/upload_images/16384352-07f4357a890613e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ID及Token赋值给相关变量**，DNSPOD的ID,Token

`export DP_Id="<ID>"`
`export DP_Key="<Token>"`

![image.png](https://upload-images.jianshu.io/upload_images/16384352-a54945f367599614.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**申请HTTPS证书**

*注意：需要申请ssl证书的该域名必须是在DNSPOD上解析的，如果是第三方的域名运营商只需要把域名解析的DNS改成DNSPOD的DNS服务器即可，不然的话会提示***invalid domain的错误信息*

证书默认放置位置为 ~/.acme.sh/<Your_Domain>/

`/root/.acme.sh/acme.sh --issue --dns dns_dp -d aioper.cn -d *.aioper.cn`

 fullchain.cer <Your_Domain>.key 下载两个文件进行使用

```bash
-----END CERTIFICATE-----
[2019年 02月 28日 星期四 11:06:55 CST] Your cert is in  /root/.acme.sh/aioper.cn/aioper.cn.cer 
[2019年 02月 28日 星期四 11:06:55 CST] Your cert key is in  /root/.acme.sh/aioper.cn/aioper.cn.key 
[2019年 02月 28日 星期四 11:06:55 CST] The intermediate CA cert is in  /root/.acme.sh/aioper.cn/ca.cer 
[2019年 02月 28日 星期四 11:06:55 CST] And the full chain certs is there:  /root/.acme.sh/aioper.cn/fullchain.cer 
```

找到证书，证书位于/root/.acme.sh/aioper.cn

将fullchain.cer 、aioper.cn.key放到WEB目录。fullchain.cer名字改为aioper.cn.crt。即可开启ssl。