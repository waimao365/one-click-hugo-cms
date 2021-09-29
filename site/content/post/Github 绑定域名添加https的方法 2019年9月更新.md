---
title: Github 绑定域名添加https的方法2019年9月更新
date: 2019-09-14 15:40:43

comments: true
toc: true
categories:
  - Github
  - hexo
  - 域名
  
tags:
  - Github
  - hexo
  - 域名
abbrlink: 5
slug: 5
---
  
  官方教程  
 https://help.github.com/en/articles/using-a-custom-domain-with-github-pages  
 打开 [https://github.com/](https://github.com/)  
 打开 [https://github.com/waimao8/waimao8.github.io/settings](https://github.com/waimao8/waimao8.github.io/settings)  
 绑定域名：163168.xyz
<!-- more -->
 ![1.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMTkvMDkvMTQvT3djYURRVWxMdGQxN0Z2LnBuZw?x-oss-process=image/format,png)

 打开你要绑定域名的项目，进入设置页面。并在 Github Pages - Custom domain 这一栏填上你的网址  
 163168.xyz

 在source 目录添加一个新文件CNAME，不带任何后缀，这就是全称，里面写的是你的域名 163168.xyz  
 ![2.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMTkvMDkvMTQveVc1YWRzSE4zUVVEeHdxLnBuZw?x-oss-process=image/format,png)

 
 免费https域名解析  
 [https://dash.cloudflare.com/](https://dash.cloudflare.com/)  
 从域名服务商ns到下面两个地址  
 candy.ns.cloudflare.com  
 earl.ns.cloudflare.com  
 电脑运行cmd ping waimao8.github.io  
 ![4.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMTkvMDkvMTQvdzFJOHVseG9HZmprc0RpLnBuZw?x-oss-process=image/format,png)  
 查询ip位  
 185.199.108.153  
 之前ping的是185.199.110.153

 从cloudflare解析域名 163168.xyz  
 185.199.110.153  
 185.199.111.153  
 ![6.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMTkvMDkvMTQvalpQblh1NGhrSm1NVHkxLnBuZw?x-oss-process=image/format,png)  
 等30分钟左右生效  
 点击 https://163168.xyz/ 生效就可以访问了

   
