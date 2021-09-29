---
title: github搭建hexo博客和绑定域名的详细过程
date: 2019-09-09 19:21:48

comments: true
toc: true
categories:
  - hexo
tags:
  - hexo
  - 博客
abbrlink: 2
slug: 2
---




## []()1、https://github.com/ 先注册账号 比如我的是 waimao8


## []()2、New repository waimao8.github.io


## []()3、下载git https://git-scm.com/downloads 默认安装 安装好后，用git --version 来查看一下版本


## []()4、下载 https://nodejs.org/en/download/ 选LTS 默认安装 ，安装完后，打开命令行
<!-- more -->

```
node -v

```

```
npm -v

```

## []()5、安装hexo

 先创建一个文件夹blog，然后cd到这个文件夹下（或者在这个文件夹下直接右键git bash打开）  
 输入命令  `npm install -g hexo-cli`   
 用 hexo -v 查看一下版本  
 初始化一下hexo  
 hexo init myblog 或者hexo init  
 cd /D/hexo/blog/myblog (每个人的安装目录都不一样，可参考我的


```
npm install

```

```
hexo g

```

```
hexo server

```
 在浏览器输入localhost:4000就可以看到你生成的博客了


## []()6、生成SSH添加到GitHub


```
git config --global user.name "yourname"

```

```
git config --global user.email "youremail"

```
 这里的yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱  
 检查一下你有没有输对


```
git config user.name
git config user.email

```
 然后创建SSH,一路回车  
 ssh-keygen -t rsa -C “youremail”  
 这个时候它会告诉你已经生成了.ssh的文件夹。在你的电脑中找到这个文件夹  
 一般在这个位置c/Users/Administrator/.ssh/  
 GitHub的最右上角setting中，找到SSH keys的设置选项，点击New SSH key  
 把你的id_rsa.pub里面的信息复制进去  
 在gitbash中，查看是否成功


```
ssh -T git@github.com

```
 如果提示Are you sure you want to continue connecting (yes/no)?，输入yes，然后会看到：


```
Hi liuxianan! You've successfully authenticated, but GitHub does not provide shell access.

```
 看到这个信息说明SSH已配置成功！

 此时你还需要配置：


```
git config --global user.name "liuxianan"// 你的github用户名，非昵称

```

```
git config --global user.email  "xxx@qq.com"// 填写你的github注册邮箱

```

## []()7、将hexo部署到GitHub

 打开站点配置文件 _config.yml，翻到最后，修改为  
 YourgithubName就是你的GitHub账户


```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  或者 
  repo:git@github.com:waimao8/waimao8.github.io.git
  branch: master

```
 安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub


```
npm install hexo-deployer-git --save

```
 然后


```
hexo clean
hexo generate
hexo deploy

```
 hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写  
 hexo deploy 部署文章，可以用hexo d缩写

 注意deploy时可能要你输入username和password。

 得到下图就说明部署成功了，过一会儿就可以在 [http://waimao8.github.io ](http://waimao8.github.io)这个网站看到你的博客了！！


## []()8、设置个人域名

 打开cmd  
 ping waimao8.github.io  
 得到ip：185.199.110.153  
 添加域名解析，A到185.199.110.153  
 ping下哪个ip的访问速度快，就A到哪里ip  
 点击添加解析，记录类型选A或CNAME，A记录的记录值就是ip地址，github(官方文档)提供了两个IP地址，192.30.252.153和192.30.252.154，这两个IP地址为github的服务器地址，两个都要填上，解析记录设置两个www和@，线路就默认就行了，CNAME记录值填你的github博客网址 比如我的 waimao8.github.io  
 Settings）设置，然后在 GitHub Pages的 Custom domain设置里填上购买的域名  
 新域名配置完成，可以访问了

   
