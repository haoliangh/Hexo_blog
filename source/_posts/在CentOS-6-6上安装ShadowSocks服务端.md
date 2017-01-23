---
title: 在CentOS 6.6上安装ShadowSocks服务端
date: 2017-01-23 15:02:20
tags:
---
## 在CentOS 6.6上安装ShadowSocks服务端

1. 查看系统
	
	```
		[root@localhost ~]# cat /etc/issue
		CentOS release 6.6 (Final)	
	```
	```
		[root@localhost ~]# uname -a
		Linux localhost.localdomain 2.6.32-042stab106.6 #1 SMP Mon Apr 20 14:48:47 MSK 2015 x86_64 x86_64 x86_64 GNU/Linux
	```
	
2. 安装ShadowSocks

	```
		# yum install python-setuptools && easy_install pip 
		# pip install shadowsocks
	```
	
3. 创建配置文件/etc/shadowsocks.json

	```
		[root@localhost /]# touch /etc/shadowsocks.json 
		[root@localhost /]# vi /etc/shadowsocks.json 
	```
	```
		{ 
		"server":"138.128.208.158", 
		"server_port":443, 
		"local_address": "127.0.0.1", 
		"local_port":1080, 
		"password":"MyPass", 
		"timeout":600, 
		"method":"rc4-md5"
		}
	```
	> 备注：加密方式官方默认使用aes-256-cfb，推荐使用rc4-md5，因为 RC4比AES速度快好几倍。
各字段说明：

    * server:服务器IP
    * server_port:服务器端口
    * local_port:本地端端口
    * password:用来加密的密码
    * timeout:超时时间（秒）
    * method:加密方法，可选择 “bf-cfb”, “aes-256-cfb”, “des-cfb”, “rc4″等
    
4. 使用配置文件在后台运行shadowsocks服务
	
	```
		[root@localhost /]# ssserver -c /etc/shadowsocks.json -d start
	```
	
5. 若要停止服务

	```
		[root@localhost /]# ssserver -c /etc/shadowsocks.json -d stop
	```
	
6. 把程序添加到开机自启动
	> 把启动程序的命令添加到/etc/rc.d/rc.local文件中
	
	```
		vi /etc/rc.d/rc.local
	```
	```
		#!/bin/sh
		#
		# This script will be executed *after* all the other init scripts.
		# You can put your own initialization stuff in here if you don't
		# want to do the full Sys V style init stuff.
		
		[root@localhost /]# ssserver -c /etc/shadowsocks.json -d start
	```