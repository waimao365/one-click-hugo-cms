---
title: N1安装omv后安装docker+transmission+lnmp搭建网站
date: 2019-12-08 18:31:42
comments: true
toc: true
categories:
  - 斐讯N1
tags:
  - 斐讯N1
  - omv
  - docker
  - lnmp
abbrlink: 8
slug: 8
---
N1安装好omv后，
进入系统，常规设置，修改web管理员密码，需要安装的lnmp搭建网站的话，还需要修改端口，自动登出时间可以设置为1天。
进入磁盘，文件管理，挂着ext4格式的U盘或者硬盘（其他格式的不能修改权限比如777 755等）
<!-- more -->
进入共享文件夹，设置共享，设置ftp nfs smb 等
进入omv-extars，打开docker ce
进入插件安装transmissionbt ，webdav docker
启动容器，设置路径数据盘，避免8G内存不够用

安装transmission-web 看官方的教程

https://github.com/ronggang/transmission-web-control/wiki/Linux-Installation-CN

安装最新发布版本
<!-- more -->

docker安装portainer

> docker run -d -p 9888:9000 \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
--name prtainer-test \
docker.io/portainer/portainer


docker run -d -p 9888:9000 --restart=always --name portainer -v /var/run/docker.sock:/var/run/docker.sock -v /Users/lee/dev/docker_file/portainer/data:/data docker.io/portainer/portainer
安装lnmp（我试过通过docker安装deibian后安装lnmp和宝塔，omv是改过端口的，安装后omv还是打不开，所以我选择直接安装）
宝塔会占内存，经常安装出错，所以我选择安装lnmp无人值守安装
https://lnmp.org/auto.html 选择版本
无人值守安装命令：
wget http://soft.vpser.net/lnmp/lnmp1.6.tar.gz -cO lnmp1.6.tar.gz && tar zxf lnmp1.6.tar.gz && cd lnmp1.6 && LNMP_Auto="y" DBSelect="3" DB_Root_Password="lnmp.org" InstallInnodb="y" PHPSelect="8" SelectMalloc="1" ./install.sh lnmp
默认数据库密码是lnmp.org 大家可以先修改
一切都是自动的，大概要2个小时，安装好后，打开NI的ip
在首页可以看到 查看本地环境: 探针 phpinfo phpMyAdmin
再参考
LNMP添加、删除虚拟主机及伪静态使用教程
https://lnmp.org/faq/lnmp-vhost-add-howto.html
安装好后，先停止 nginx
lnmp nginx stop
移动wwwroot文件夹到数据盘比如我的数据盘目录是/sharedfolders/2t/www
mv /home/wwwroot /sharedfolders/2t/www
将数据盘的wwwroot印射回/home/wwwroot
ln -s /sharedfolders/2t/www/wwwroot /home/wwwroot
这样网站的数据就不占N1的空间了，都是在外接的数据盘上面了（必须ext4格式）
添加域名后/home/wwwroot/目录回有一个域名的目录，在里面上传php程序安装，（比如我的这个博客typecho）

下面是lnmp相关的命令
添加主机

lnmp vhost add
修改添加的主机的端口
/usr/local/nginx/conf/vhost

重启lnmp start|stop|restart 启动停止重新启动

lnmp restart
lnmp nginx restart

列出网站(虚拟主机)
执行：lnmp vhost list

删除网站(虚拟主机)
执行：lnmp vhost del
