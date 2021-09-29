---
title: 斐讯N1 docker安装homeassistant  配置斐讯dc1智能插座
date: 2019-09-16 12:52:42
comments: true
toc: true
categories:
  - 斐讯N1
tags:
  - 斐讯N1
  - homeassistant
  - docker
  - 斐讯DC1
abbrlink: 6
slug: 6
---

斐讯N1 docker安装homeassistant  配置斐讯dc1智能插座
 
 默认代码

 
```
docker run -d --restart=always --name="home-assistant" -e TZ=Asia/Shanghai -v /var/lib/docker/homeassistant:/config -p 8123:8123 -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/aarch64-homeassistant:latest

```
<!-- more -->
homeassistant:latest表示最新版的 用0.88.1顺手了，配置文件也有了，就不想安装最新版本的了。新版也试用过，不太好用  
 刚开始用的代码是
 
```
docker run -d --restart=always --name="home-assistant" -e TZ=Asia/Shanghai -v /var/lib/docker/homeassistant:/config -p 8123:8123 -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/aarch64-homeassistant:0.88.1

```
 没几天发现N1omv不能登陆，查询到内存储存已满，查找到var/lib/docker/homeassistant/config 里面有一个home-assistant_v2.db文件占了2G多，而且会不断的变大，更改 /docker/homeassistant的安装目录到移动硬盘  
 这个是我的docker的安装目录，/sharedfolders/2t/docker  
 所以修改后的代码就是把/var/lib/docker更换成/sharedfolders/2t/docker

 
```
docker run -d --restart=always --name="home-assistant" -e TZ=Asia/Shanghai -v /sharedfolders/2t/docker/homeassistant:/config -p 8123:8123 -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/aarch64-homeassistant:0.88.1

```
 下载DCI配网工具
 给DC1配置好网络，要在路由里面找到DC1的ip就算完成了
 
 下载 20190628 HA Docker - DC1 M1.rar 里面有配置说明的  
 蓝奏云网盘下载 https://www.lanzous.com/b987569  
 下载的文件里面有配置说明的，我也简单说下，把custom_components、M1（悟空净化器）、packages上传到/homeassistant根目录，下面内容复制进configuration.yaml底部  
 homeassistant:  
 packages: !include_dir_named packages  
 斐讯K2老毛子固件路由。高级设置，内部网络，DHCP服务器，自定义配置文件 “hosts”  
 增加以下两句  
 192.168.123.24 Smartplugconnect.phicomm.com  
 192.168.123.24 aircat.phicomm.com  
 备注：192.168.123.24是我的斐讯N1的ip  
 修改packages/phicomm_dc1m.yaml  
 ip修改成你在路由器里面看到DC1的ip

 配置根目录的automations.yaml  
 我设置了饮水机06.30开 00.30关 打印机18.00开 00.00关，下面是代码

 
```
- alias: switch_on 06.30
  initial_state: true
  trigger:
  - platform: time
    at: '06:30:00'
  action:
  - service: switch.turn_on 
    entity_id: switch.dc1_s1_template
- alias: switch_off 00.30
  initial_state: true
  trigger:
  - platform: time
    at: '00:30:00'
  action:
  - service: switch.turn_off
    entity_id: switch.dc1_s1_template


- alias: switch_on 18.00
  initial_state: true
  trigger:
  - platform: time
    at: '18:00:00'
  action:
  - service: switch.turn_on
    entity_id: switch.dc1_3_s3_template
- alias: switch_off 00.00
  initial_state: true
  trigger:
  - platform: time
    at: '00:00:00'
  action:
  - service: switch.turn_off
    entity_id: switch.dc1_3_s3_template


```
 配置过程发现问题解决的的3个方法  
 1、斐讯DCI拔插头断电，再接电  
 2、重启homeassistant  
 3、退出homeassistant账户，重新登陆

 可以在docker重启homeassistant ，也可以在网页重启，配置好文件后可以按下图更改，0.88.1配置是这样的，新版貌似没有配置检查。  
 ![dc1配置.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMTkvMDkvMTYvNzFxSWZnT2N0WFFFckI1LnBuZw?x-oss-process=image/format,png)

   
  