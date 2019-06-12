---
title: 给Centos系统设置静态IP
date: 2013-05-20 16:29:29
tags: centos
categories: linux
---

如果我们想更改主机地址为静态地址或者更改主机名，需要修改的几个文件包括：   
/etc/sysconfig/network   Centos设置主机名和网络配置    
/etc/sysconfig/network-scripts/ifcfg-eth0  针对特定的网卡进行设置    
/etc/resolv.conf  设置DNS    
/etc/hosts  设置指定的域名解析地址

一般我们只需要修改网卡的Centos配置文件就可以了, 例子如下:
```
DEVICE=eth0BOOTPROTO=staticTYPE=EthernetNAME="taovps etho0"BROADCAST=192.168.56.255HWADDR=08:00:27:21:F8:80IPADDR=192.168.1.101IPV6INIT=yesIPV6_AUTOCONF=yesNETMASK=255.255.255.0NETWORK=192.168.1.1ONBOOT=yes
```
Centos设置IP完成后，重启一下网卡就可以了：  
```
service network restart
```
设置后查看是否已经生效
```
ifconfig eth0
```
这样就完成了