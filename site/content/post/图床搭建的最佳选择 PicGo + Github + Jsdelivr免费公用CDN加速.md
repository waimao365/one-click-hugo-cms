---
title: 图床搭建的最佳选择 PicGo + Github + Jsdelivr免费公用CDN加速.
date: 2019-12-13 12:33:32
comments: true
toc: true
categories:
  - Github
  - hexo
  - PicGo
  - Jsdelivr
tags:
  - Github
  - hexo
  - PicGo
  - Jsdelivr
abbrlink: 12
slug: 12
---




**图床搭建的最佳选择 PicGo + Github + Jsdelivr免费公用CDN加速**

# Github创建仓库


## 点击 New repository

<!-- more -->

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/0.png)
## 创建好后，获取Token


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/2.png)


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/3.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/4.png)

## 这个Token只出现一次的，一定要记得复制好，pico设置要用到的

# 下载picgo

https://github.com/Molunerfinn/PicGo/releases

我使用的是黑苹果，下载PicGo-2.1.2.dmg
安装好后，在屏幕右上角会有一个标志，右键打开详细窗口

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/5.png)





设定仓库名：waimao8/image   （你设置成你自己的哈）
分支名一般是master   （默认建议这个）
存储的路径：img         （可以不填我没有填）
设定自定义域名：可以不填使用默认的，但是Github服务器在外国，访问速度不太理想，我们可以通过Jsdelivr免费公用CDN加速来加速图片是访问速度
所以我设置成
https://cdn.jsdelivr.net/gh/waimao8/image@master


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191213175919.png)

记得点设为默认图床哦！

# 顺便介绍下这篇文件的制作过程
打开 http://marxi.co/
登陆微信
默认截图的快捷键ctrl+win+A，选择截图后，
点击shift+win+p
截图会自动通过Picgo上传到Github上面了，直接粘贴到文章就可以了，真的是非常方便！

笔记本屏幕太小，我外接了显示器，发现点击shift+win+p后，上次图片失败，
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191213175553.png)百度了一下相关的教程
打开mac的系统偏好设置，点击显示器，点击颜色，选择普通RGB描述文件，就可以了。
