---
title: n1终极玩法Armbian-5.77安装docker宝塔openwrt和HomeAssistant
date: 2020-06-02 15:55:32
comments: true
toc: true
categories:
  - N1
  - docker
  - 宝塔
  - openwrt
  - Home Assistant
tags:
  - N1
  - docker
  - 宝塔
  - openwrt
  - Home Assistant
abbrlink: 23
slug: 23
---

#  安装Armbian-5.77

https://www.right.com.cn/forum/thread-510423-1-1.html  
##  下载Armbian-5.77写入U盘
##  替换低负载的dtb  
meson-gxl-s905d-phicomm-n1-xiangsm.dtb  
##  开启bbr  
在/etc/sysctl.conf末尾添加下面两行:  
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr  
然后执行  
sudo sysctl -p  
##  写入emmc  
./install.sh  
##  更换国内源  
如果有外国IP就不用更换源了  
sudo nano /etc/apt/sources.list

修改源为国内源
deb http://mirrors.tuna.tsinghua.edu.cndebian stretch main contrib non-free  
deb http://mirrors.tuna.tsinghua.edu.cn/debian stretch-updates main contrib non-free  
deb http://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free  
deb http://mirrors.tuna.tsinghua.edu.cn/debian stretch-backports main  

保存后，更新源  
执行 apt-get update 命令即可更新源  
执行 apt-get upgrade 更新软件  
##  安装docker  
输入 armbian-config  
选择Software，回车确认 接着选择Softy，回车确认 最后选择docker，空格勾选，回车确认开始安装  
然后，按tab键，选择OK，回车确认 最后等docker程序自动安装完成  
##  docker安装portainer  
docker pull portainer/portainer  
docker run -d -p 9888:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always --name prtainer portainer/portainer  
如果遇到安装失败一般都是源的问题，换IP可以解决  

##  挂载docker数据到数据盘  
考虑到N1只有6G可用储存，我们可以将dockers安装到数据盘，接入U盘或者硬盘，输入  
df -i，比如查询硬盘为  /dev/sda1  
将硬盘挂载到mnt （其他目录也可以） 
输入mount /dev/sda1 /mnt  
输入 blkid /dev/sda1 查询 得到数据  
UUID="a78e3c99-2754-034e-abd1-36后面省略  
输入命令开机自动挂载  
echo 'UUID=a78e3c99-2754-034e-abd1-36后面省略 /mnt ext4 defaults 0 0' >> /etc/fstab  
输入 mount -a  
检查是否挂载好  df -h  
备份docker数据  
cp -r /var/lib/docker_data /var/lib/docker  
移动docker数据到硬盘  
mv /var/lib/docker /mnt/docker  
把硬盘的目录发送到N1  
ln -s /mnt/docker /var/lib/docker

##  docker安装openwrt  
docker pull unifreq/openwrt-aarch64:r20.04.08  
ip link set eth0 promisc on  
modprobe pppoe  
docker network create -d macvlan --subnet=192.168.123.0/24 --gateway=192.168.123.1 -o parent=eth0 macnet  
docker run --restart always -d --network macnet --privileged --ip=192.168.123.2 unifreq/openwrt-aarch64:r20.04.08 /sbin/init  
大家根据自己的实际IP改下代码  
再登录portainer管理页面，点container  
vi /etc/config/network  
按i改网关信息，op的ip要改成跟主路由同网关，比如192.168.123.2或者192.168.123.3，改好后依次按返回键，:wq保存退出。再点disconnect，在containers那勾选op 点restart重启op。 (部分op需手动复制粘贴以下两条  
192.168.2.1改成你主路由ip。不复制进去就登陆不了op  
option gateway '192.168.123.1'  
option dns '114.114.114.114 223.5.5.5'  
另外再教大家安装下载好的openwrt  
导入本地编译好的rootfs.tar.gz并部署  
随便导入一个文件夹  cd /到这个文件夹  
docker import openwrt-armvirt-64-default-rootfs.tar.gz openwrt:R9.9.15  
再输入   
docker run --restart always -d --network macnet --privileged --ip=192.168.123.5 openwrt:R9.9.15 /sbin/init  
vi /etc/config/network  
设置网关为192.168.123.5  
重启openwrt 输入192.168.123.5 就可以登陆了  
默认的账号root 密码password  

#  安装Home Assistant  
docker run -d --restart=always --name="home-assistant" -e TZ=Asia/Shanghai -v /var/lib/docker/homeassistant:/config -p 8123:8123 -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/aarch64-homeassistant:0.88.1
  
  具体参考另一篇文章  
  https://163168.xyz/posts/6.html

# 安装宝塔搭建网站  
安装过程直接看这里  
https://hub.docker.com/r/startwish/n1-bt-lnmp

默认的信息
宝塔面板登录页面是

你的IP:8888/startwish
账号startwish

密码startwish

系统root账户的密码是startwish  
可以通过宝塔搭建自己的网站了！！！