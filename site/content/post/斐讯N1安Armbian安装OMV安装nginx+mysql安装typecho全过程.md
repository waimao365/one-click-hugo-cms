---
title: 斐讯N1安Armbian安装OMV安装nginx+mysql安装typecho全过程
date: 2019-12-08 18:28:42
comments: true
toc: true
categories:
 
  - 斐讯N1
  - omv
  - typecho
  - lnmp
  - mysql
  - nginx

tags:
  - 斐讯N1
  - omv
  - typecho
  - lnmp
  - mysql
  - nginx

abbrlink: 7
slug: 7
---
#  安装armbian

测试了很多版本的Armbian+omv，OMV经常会报错，改用了XQ7的N1首个支持FullCone Nat的Armbian系统，非常好用
下面是链接
https://www.right.com.cn/forum/thread-788004-1-1.html
<!-- more -->
ROM下载地址：链接：https://share.weiyun.com/5IsYMcO 密码：fop0i5
需要说明的是img制作成U盘后，不需要替换dtb，不需要更换内核，直接使用就可以，一步到位。

先把镜像写入U盘，从U盘启动后，从路由器找到N1的ip地址
通过Xshell登陆 输入N1的ip 账号root 密码1234
第一次进入需要修改密码
再写入N1的内置存储，用下面的命令就可以了
/boot/create-mbr-linux.sh
/root/install.sh
写入完成后，断电，拔U盘，插电重启

切换中国时间
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

运行
nano /etc/apt/sources.list
修改源为国内源
deb http://mirrors.tuna.tsinghua.edu.cn/debian stretch main contrib non-free
deb http://mirrors.tuna.tsinghua.edu.cn/debian stretch-updates main contrib non-free
deb http://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free
deb http://mirrors.tuna.tsinghua.edu.cn/debian stretch-backports main

或者

deb http://mirrors.ustc.edu.cn/debian stretch main contrib non-free
deb http://mirrors.ustc.edu.cn/debian stretch-updates main contrib non-free
deb http://mirrors.ustc.edu.cn/debian stretch-backports main contrib non-free
deb http://mirrors.ustc.edu.cn/debian-security/ stretch/updates main contrib non-free

保存后，更新源
执行 apt-get update 命令即可更新源
执行 apt-get upgrade 更新软件

##  做一个补充，切换国内源后安装omv和插件有一定概率会出问题，官方的也是一样，最稳的做法是，外国ip，官方源，稳定，速度又快。

#  安装omv

armbian-config

选择Software，回车确认 接着选择Softy，回车确认 最后选择OMV，空格勾选，回车确认开始安装

然后，按tab键，选择OK，回车确认 最后等OMV程序自动安装完成

依次选择Exit、Cancel，返回命令行
至此OMV安装完毕，正常的话，浏览器输入N1 ip或http://aml/ ,会看到OpenMediaVault登陆界面

此时使用默认用户名：admin 默认密码：openmediavault ，登陆即可


OMV安装OMVEXTRAS
官方教程  https://www.openmediavault.cn/read-omvextrasorg.html
安装好后，按下图设置

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112165303.png)

#  安装Typecho

##  在文件管理，找到自己的usb设备，我的是移动2T的移动硬盘，选择挂载。

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112170829.png)


用winscp软件，到2t下面建www文件夹，在www下面建typecho文件夹，在typecho下面建public_html 文件夹  都设置777权限，如下图

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112170108.png)
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112170222.png)


##  安装nginx和mysql
在插件找插件，点安装就可以的，先安装nginx，再安装mysql，安装好后入下图


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112171153.png)

###  设置nginx 点击pools，添加typecho

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112171656.png)
点击服务器，添加后保存
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112171847.png)
应用更改后再设置，选择typecho目录，选择公共目录，选择public_html，启用php，php-fpm-pool选择刚刚建立的typecho

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112172404.png)

Index下面的三个选项都打开

这里先打乱一些顺序，我发现安装好typecho后，只能打开前台，文件页面和管理后台都出现404，下面就是解决方法
下面有个扩展选项，填入下面代码


if (-f $request_filename/index.html){
    rewrite (.*) $1/index.html break;
}
if (-f $request_filename/index.php){
    rewrite (.*) $1/index.php;
}
if (!-f $request_filename){
    rewrite (.*) /index.php;
}


![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112173220.png)

也可以直接在配置 /etc/nginx/sites-available/zzz-omv-nginx 最后面加上面的代码
就可以了

最后在General点击启用，nginx 就配置好了
下面配置数据库

###  omv安装数据库
https://www.openmediavault.cn/read-omv-install-mysql.html

打开mysql，重设密码。绑定ip改成n1的ip

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112174209.png)

点击show
用户ID：omvadmin
密码：刚修改过的
登陆后，创建数据库
![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112174527.png)
官方下载 http://typecho.org/   
解压后，将文件上传到前面建立都public_html文件夹，就可以安装了。

### mysql自动启动
安装配置完nginx和mysql后默认mysql是不能自启动的。所以还要配置数据库自启动。用winscp连接OMV系统【默认用户名root密码openmediavault】。连接后打开etc-找到rc.loal,右键点编辑，在exit 0上一行添加service mysqld start保存退出。就可以了

###  备份数据库和还原数据库

![](https://cdn.jsdelivr.net/gh/waimao8/image@master/20200112182628.png)


#  顺便推荐一个非常漂亮的主题
https://zhebk.cn/Web/Akina.html


#  下面是相关命令和教程


omv-firstaid
First aid 界面翻译

configure network interface 配置网络界面

configure web control panel 配置Web控制面板

change control panel administrator password 更改控制面板管理员密码

restore failed login attempt counter 恢复失败登录尝试计数器

restore configuration backup 恢复配置备份

check configuration status file 检查配置状态文件

check RRD database 检查RRD数据库

clear local upload package repository 清除本地上传包存储库

clean apt 清除apt

clear web control panel cache 清除Web控制面板缓存

submit diagnostic report to administrator 向管理员提交诊断
卸载相关
apt-get remove 会删除软件包而保留软件的配置文件
apt-get purge 会同时清除软件包和软件的配置文件
卸载openmediavault命令
apt-get purge openmediavault

armbian-config可视化操作里面有许多快捷的系统设置，
比如说基本的时间设置、网络设置，Wi-Fi设置，设置热点、安装桌面和远程、安装热门的第三方软件（诸如nginx Nextcloud、Plex、OpenMediaVault、Pi-hole、Transmission、Docker等热门软件）
下面收集了一些omv的相关教程，可以参考
omv使用

OMV安装NextCloud
https://www.openmediavault.cn/read-omv-an-zhuang-nextcloud.html

phicomm N1 armbian环境下安装功能丰富的开源NAS系统 OpenMediaVault
https://www.right.com.cn/forum/thread-342164-1-1.html

N1 OpenMediaVault 使用DLNA+VLC多媒体应用的小白教程
https://www.right.com.cn/forum/thread-342841-1-1.html

OpenMediaVault(OMV)配置Docker
https://www.jianshu.com/p/5b0eacc61527

OMV安装可道云(kodexplorer)
https://www.jianshu.com/p/4731a1ef01d1

OMV安装web服务器详细教程
https://jingyan.baidu.com/article/0aa223757304e688cd0d6464.html


