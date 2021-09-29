---
title: hugo搭建和使用教程
date: 2020-06-01 15:55:32
abbrlink: 22
slug: 22
comments: true
toc: true
categories:
  - hugo
  - 网站
  - github

tags:
  - hugo
  - 网站
  - github

---

#  前言  
  做博客就图个稳定，一次性买了10年的域名，搭配免费的github，适合做长期博客。  
  之前安装的hexo，可玩性非常强，前面文章有写一些关于hexo的安装使用教程，用了一年多，也发现了一些问题，hexo版本更新各种不兼容，访问速度慢，，很影响心情，自己都懒得搭理博客了，国内cdn加速需要备案，只是做个小站，不想太麻烦。  
  所幸，无意中发现荒野无灯大神把站转移到hugo，访问速度非常快，于是自己马上搭建了一个，打开文章页面基本上是秒开，之前hexo打开文章大约要5-6秒，用不同设备，不同网络测试很多次，hugo博客的访问速度要快4倍以上。并且文章越多，hugo的优势就越明显，为避免以后迁移麻烦，所以赶紧把博客迁到了hugo。主题也是我喜欢的，非常简洁。  
  下面开始教程吧！！！
#  安装hugo
下载hugo https://gohugo.io
解压到任意目录，比如D:\hugo\bin
将Hugo添加到Windows的环境变量 PATH中  
系统变量和用户变量都添加D:\hugo\bin  
下载Git https://git-scm.com  并安装  
下载Go语言开发环境 https://golang.org/dl  并安装
打开Git Bash 输入 hugo version 出现hugo static site generator相关信息表示安装完成  
打开D盘 右键点击 git bash here  
输入hugo new site blog
 
# 安装主题
去官网下载主题  https://themes.gohugo.io  
我下载的是even  https://themes.gohugo.io/hugo-theme-even  
cd /blog  
git clone https://github.com/olOwOlo/hugo-theme-even themes/even  
安装好后 打开D:\blog\themes\even\exampleSite  
找到config.toml和content 复制到D:\blog目录下  
输入  
hugo --theme=even --baseUrl="ch0769.github.io" --buildDrafts  
 #even改成你的主题 ch0769.github.io也改成你的网址  
 出现 public 文件夹  cd /public  
 依次输入  
 git init  
 git add .  
 git commit -m "yyyy/mm/dd-hh:mm"  
 git remote add origin https://github.com/ch0769/ch0769.github.io.git   
 git push -u origin master

cd /blog  
hugo  
hugo server  
可以本地预览了 http://localhost:1313
# 新建文章
hugo new post\hugo搭建和使用教程.md  
会在D:\blog\content\post  hugo搭建和使用教程.md  
可以下载Visual Studio Code编辑和修改文章，记得换行前要先打两个空格，再按回车键。 
#  hugo使用教程
##  添加固定链接  
 
这篇教程的加法参考如下  
title: hugo搭建和使用教程  
date: 2020-06-01 15:55:32  
url: /hugodajian.html  
（hugodajian 可以改成数字或者任意字母）
##  写文章后部署  
在blog目录输入hugo  
在blog/public目录依次输入  
git add .  
git commit -m "yyyy/mm/dd-hh:mm"  
git push -u origin master  
##  Netlify 自动编译部署生成 Web 网站  
官方首页：https://www.netlify.com  
##  快速在Netlify建立Jekyll、Hexo、Hugo静态博客
网站首页：https://www.staticgen.com/  
教程可以看这里 https://kuleyu.github.io/hexolog/post/31808.html   
## 写文章日期格式  
date: 2020-06-01 15:55:32  

##  从hexo导入文章到hugo的固定链接设置  

hexo设置 permalink: posts/:abbrlink.html  
文章页面设置 abbrlink: 1   （每篇文章加一个数）  
hugo固定链接设置   
文章里面的  
abbrlink: 1  
改成  
url: /posts/1.html  
域名从hexo解析到hugo后，固定链接是不变的  
也可以不用阿拉伯数字，随便输入其他字母也是可以的，这个看个人喜欢了。  
## 绑定域名
绑域名非常简单，大家可以翻我前面的教程。  
这里发现一个问题  
绑定域名后  
输入  git push -u origin master  出现错误如下  
git上传文件出错[rejected] master -> master (fetch first) error: failed to push some refs to  
这个是因为github中的README.md文件不在本地代码目录中，可以通过如下命令进行代码合并  
git pull --rebase origin master  
再输入  
git push origin master  
就可以了。



