---
title: Nexus 5X手机在支付宝的蚂蚁森林自动收能量的过程.
date: 2019-12-10 00:21:32
comments: true
toc: true
categories:
  - 安卓手机
tags:
  - 安卓手机
  - magisk
  - edxposed
  - XQuickEnergy
abbrlink: 11
slug: 11
---

# 下载刷机包

https://downloads.aospextended.com/bullhead

个人觉得aospextended的rom比较省电，其他刷机包或者不刷机也是可以的，只要是手机不能杀支付宝的后台就行，如果需要用都省电模式，要在省电模式里面排除支付宝。
<!-- more -->
# 下载twrp
https://twrp.me/lg/lgnexus5x.html

# 下载magisk
[下载MagiskManager-v7.4.0.apk](https://t00y.com/file/22940096-413054846)

[下载Magisk-v20.1.zip](https://t00y.com/file/22940096-413054839)
https://t00y.com/file/22940096-413054839
刷入twrp
在twrp中四清，刷入aospextended的刷机包
在twrp中刷入Magisk-v20.1.zip

手机开机
安装Magisk Manager v7.4
在magisk中安装好riru-core，再安装riru edxposed
在酷安下载安装edxposed installer 
<!-- more -->

# 下载插件
下载插件[小鸡炖蘑菇](https://t00y.com/file/22940096-413054804) 
或者[XQuickEnergy](https://t00y.com/file/22940096-413054745)
安装后，在edxposed软件中勾选插件，重启手机，打开支付宝，就可以通过上面两个插件设置自动收取能量了，记得，支付宝不可以退出哦！
# 下载tasker软件设定自动打开支付宝
点击任务，新建任务，命名打开支付宝，点+号。点程序，点启动应用，点支付宝。点配置文件，点+号，点时间，点从上午6点到凌晨1点，点每30分钟。点击打开支付宝，就完成了设置，这样即使支付宝后天即使被关闭了，每30分钟也会自动打开一次，时间都是可以自己设置的。十分钟打开一次也可以，一个小时打开一次也行，主要是看支付宝多久会被杀后台。

