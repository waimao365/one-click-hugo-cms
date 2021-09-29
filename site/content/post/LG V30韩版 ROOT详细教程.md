
---
title: LG V30韩版 ROOT详细教程
date: '2019/12/23 20:10:32'
comments: true
toc: true
categories:
  - 安卓手机
  - LG V30
  - 刷机
  - root

tags:
  - 安卓手机
  - LG V30
  - 刷机
  - root

abbrlink: 18
slug: 18
---


#前言
2019年最火的洋垃圾LG V30，骁龙835cpu（从此告别发烧），4G内存，64G储存，能满足日用生活，能玩游戏，2k屏幕，hifi，极高的性价比。
<!-- more -->
# LG V30韩版 ROOT详细教程
一个非常详细的视频教程，建议大家仔细观看，全部看懂了再来操作
https://www.bilibili.com/video/av47071667
看视频刷机比较麻烦，我把视频整理成图文版的，包括命令这些，方便机友们刷机
需要的工具视频下面的评论里面都有的，大家可以先去下载

# 准备工作
## 安装LG官方驱动
## 安装LGUP刷机工具

把下载的modle和LGUP覆盖到安卓目录

## 安装谷歌驱动


首先下载并打开此ADB工具箱http://pan.baidu.com/s/1nuHwTcP
在弹出的窗口中输入y并按回车，依次重复操作3 次


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223193123.png)

# 混刷 h930的kdz
手机拔掉sim卡，断开wifi，退出google账户，设置，常规，关于手机，软件信息，连续点击内部版本号开启开发人员选项。
进入开发人员选项，点击启用OEM解锁，和USB调试，手机关机。关机后，按住音量+，插入已经连接电脑的USB线，手机会进入download 刷机模式
右键点击LGUP软件，选择以管理员身份运行，

 ![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223132526.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223132704.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223132846.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223132942.png)

刷完之后会卡LOGO

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223133059.png)

按住音量减和电源键 8秒以上，会闪屏一下，当LOGO出现后，立刻松开，再重新按住关机键，直到出现data peset界面，才松开。用音量键选择YES，按电源键 进入恢复出厂设置

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223133708.png)

开始硬格手机，格式完毕后，就可以进入系统，手机开机没有基带的，不能使用SIM卡，

# 解锁BootLoader
按照前面的教程打开设置进入开发者模式，启用OEM解锁，和USB调试，usb调成照片传输模式

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223134217.png)


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223134343.png)

LG V30工具包里有命令的，我还是把命令贴这里，方便一些
输入命令
adb devices
勾选手机始终运行在此计算机上进行操作，点确定
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223160120.png)

adb reboot bootloader
-----进入了fastboot-----
fastboot flash unlock unlock.bin



![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223160511.png)

fastboot reboot
-----解锁了BL并重启了手机-----
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223160704.png)

手机开机后，按照前面的教程打开设置进入开发者模式，启用OEM解锁，和USB调试，usb调成照片传输模式

输入
adb devices
adb reboot bootloader
fastboot getvar unlocked
出现 yes  就是解锁成功了。
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223161325.png)

----进入fastboot以查看是否解锁-----
# root，备份欧版recovery
fastboot boot TWRP.img
临时进入twrp，可以手机操作切换到中文
格式化分区
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223161714.png)
会出现红字 不用理

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223161820.png)

再清除 cache

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223162004.png)
也会出现红字，点击返回，点击重启bootloader

fastboot boot TWRP.img
再次进入twrp，电脑上可以显示手机存储了。把拷贝内存文件夹里面的三个文件复制粘贴到手机里面
依次刷入这三个文件，顺序不能乱，这次刷入没有出现红字。
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223162654.png)

接着备份欧版官方的recocery

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223162928.png)

备份好后，复制到电脑，重启手机到bootloader
输入
fastboot flash recovery TWRP.img
再次输入
fastboot boot TWRP.img
电脑上就可以看到手机储存了

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223163401.png)
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223163523.png)

把里面的twrp文件夹复制到电脑，然后手机关机


# 刷回韩版系统

关机状态下，按住音量加 插入USB，就会进入刷机模式
右键点击LGUP，以管理员身份运行。

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223163954.png)

刷韩版的kdz系统
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223164216.png)

选分区的时候排除recovery，recoverybak两个分区，也就是不刷入官方recovery，因为韩版系统即使解锁bootloader也无法进入fastboot，也就无法刷入TWRP

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223164329.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223164450.png)

刷完，一般会进入TWRP，如果没有进去，就要从 混刷 h930的kdz 开始重新刷

刷完韩版系统，进入TWRP后
格式化data，再清除 cache，依次刷入
1_Magisk-v16.0
2_no-verity-opt-encrypt-6.0
3_lg-rctd-disabler-1.0(1)adb shell
刷完后把之前备份复制到电脑的欧版recocery，（带备份日期和时间的这个文件夹）复制到手机，从TWRP恢复。

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223174444.png)

恢复之后关机再开机，一般可以正常进系统，如果等10分钟还不能开机，就要重新执行工厂格式化开机

按住音量减和电源键 8秒以上，会闪屏一下，当LOGO出现后，立刻松开，再重新按住关机键，直到出现data peset界面，才松开。用音量键选择YES，按电源键 进入恢复出厂设置
按照前面的教程，并引用了之前的图片
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223133708.png)

开始硬格手机，格式完毕后，就可以进入系统
现在的系统状态是已解锁BL锁，有root权限
把TWEP.img文件复制到手机储存
打开开发者模式，开启adb调试
输入下面的命令
adb shell
su

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223175719.png)

手机点允许

dd if=/sdcard/TWRP.img of=/dev/block/bootdevice/by-name/recovery

# 教程补充

刷机前可以先备份基带再刷机

手机进入刷机模式（完全关机按住音量+插入数据线连接电脑）

右键管理员打开桌面“LG UP”。

先备份基带（备份xbl xbl2 modem分区） （机锋论坛浪大教程）

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223185115.png)

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20191223185236.png)


以后要升级系统，可以从刷回韩版教程开始刷

在ADB和Fastboot工具的文件夹中，按住shift并右击空白处，选择“在此处打开Powershell窗口”（旧版Windows为命令提示符）
界面不同，但命令无区别）,进入命令行窗口。



#  机锋精品教程

 LG V30韩版解锁Bootloader+TWRP+韩版系统+root详细教程&资源  （非常详细的刷机教程）
 http://bbs.gfan.com/android-9493762-1-4.html


LG V30官方KDZ混刷教程
http://bbs.gfan.com/android-9313407-1-1.html

 LG V30解BL 安装TWRP及root详细教程
 ttp://bbs.gfan.com/android-9313266-1-1.html

韩版刷机说明..防砖.刷第三方
http://bbs.gfan.com/android-9561523-1-1.html

 韩版v300l，解锁+root+原生系统教程之五大步（补充）
 http://bbs.gfan.com/android-9506755-1-1.html

LG V30目前可以通刷的版本说明
http://bbs.gfan.com/android-9310017-1-3.html

【PIE+Volte】韩版移动电信成功开启Volte更新详细教程
http://bbs.gfan.com/android-9618911-1-3.html

韩版用户折腾经验分享
http://bbs.gfan.com/android-9492238-1-6.html


俄罗斯论坛LG V30刷机固件下载
http://4pda.ru/forum/index.php?showtopic=902834

看下载量 Dot OS 这个不错 也是官方的，比较稳定，其他rom应该也不错的。
8.1
https://forum.xda-developers.com/lg-v30/development/rom-dotos-v2-2-t37984419.0

9.0
https://forum.xda-developers.com/lg-v30/development/rom-pie-dot-os-3-0-t3908490


LG-US998 20D ROM 常用底包 里面有解锁的相关链接
https://forum.xda-developers.com/lg-v30/development/rom-lg-us998-20d-rom-t3830318