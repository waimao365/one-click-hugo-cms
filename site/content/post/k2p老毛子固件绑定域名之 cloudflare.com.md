---
title: k2p老毛子固件绑定域名之 cloudflare.com
date: 2020-01-03 13:10:32
comments: true
toc: true
categories:
  - k2p
  - 域名
  - cloudflare
  - 路由
  - 网站
tags:
  - k2p
  - 域名
  - cloudflare
  - 路由
  - 网站

abbrlink: 20
slug: 20

---


k2p老毛子固件绑定域名之 cloudflare.com


使用 Cloudflare 实现顶级个人域名的 ddns 服务。 https://www.cloudflare.com


使用前需要安装 curl 程序，可以安装opt后输入 opkg install curl 敲回车键安装启用opt
 <!-- more -->

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200103134738.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200103134543.png)


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200103132446.png)




点击获取
https://dash.cloudflare.com/profile/api-tokens

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200103132545.png)

输入密码和验证码，就可以获得

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200103132918.png)

复制到  用户 Global API Key