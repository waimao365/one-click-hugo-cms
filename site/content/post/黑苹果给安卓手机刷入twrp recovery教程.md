---
title: 黑苹果给安卓手机刷入twrp recovery教程
date: 2019-12-18 01:00:32
comments: true
toc: true
categories:
  - 安卓手机
  - twrp
  - recovery
  - 黑苹果

tags:
  - 安卓手机
  - twrp
  - recovery
  - 黑苹果


abbrlink: 16
slug: 16
---

# 手机设置
点击设置，系统，关机手机，版本号联系点击三下，进入开发者模式，找到开发者选项，打开OME解锁，打开Android调试，打开网络ADB调试。
<!-- more -->
# 下载twrp
 下面以lgnexus5x为例
 https://twrp.me/lg/lgnexus5x.html


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191218000645.png)

下载最新的
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191218000719.png)

# 安装 ADB 和 Fastboot 工具
点击下载platform-tools
https://dl.google.com/android/repository/platform-tools-latest-darwin.zip
解压后放在一个方便使用的位置，英文名字的文件夹
打开终端，用 cd 命令进入 SDK 目录的 platform-tools 文件夹。即 输入 cd 和一个空格，后面输入文件夹路径，也可以直接拖拽文件夹进终端。下面是我的路径存放地址示例：
cd ~/desktop/az/platform-tools


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191218001247.png)

文件夹路径可以直接使用快捷键win+ alt + C来复制，粘贴当然还是`win + V

把 ADB 拷贝到系统，回车后继续输入你的密码。密码是隐藏的，输入完毕，回车就行
sudo cp adb /usr/bin/adb
把 Fastboot 也复制进来
sudo cp fastboot /usr/bin/fastboot

# 刷入第三方 Recovery （以 TWRP 为例）

手机关机，按住音量减号键+开机键 进入bootloader刷机模式，（或者在终端输入adb reboot bootloader）
手机用USB线连接电脑（尽量用原装线，台式机尽量插机箱后面的USB接口）
cd ~/desktop/az/platform-tools    （这个是我的platform-tools存放的路径，你可以自己设置的哈）
有两个方法可以刷入的

## 方法一 
输入 fastboot flash recovery
把recovery文件img结尾的拖入命令后，留意空格哈
如果无法刷入recovery，建议使用这个命令sudo fastboot flash recovery
这个刷好recovery无法自动重启，可以长按关机键关机，再安装音量加+开机键十秒左右，一般就会进入recovery
实在没有进入，可以手机开机，输入命令 adb reboot recovery


把下载好的文件twrp文件放到platform-tools 并重新命名为twrp.img

## 方法二
把下载好的文件twrp文件放到platform-tools 并重新命名为twrp.img
输入 fastboot flash recovery twrp.img
再输入命令
fastboot boot twrp.img
正常手机就会重启到recovery 模式了，就可以进入里面刷机了。

# 终端相关的命令解释
adb reboot bootloader   
进入手机刷机模式bootloader

adb reboot recovery      
进入手机恢复模式recovery

adb reboot system       
进入手机系统




