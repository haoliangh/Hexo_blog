---
title: 共享Mac上的Shadowsocks代理
date: 2016-12-22 23:01:17
tags:
---

## 共享Mac上的Shadowsocks代理，需要借助Privoxy。

1. 在 [http://www.privoxy.org/#DOWNLOAD](http://www.privoxy.org/#DOWNLOAD) 下载安装

2. 修改 /usr/local/etc/privoxy/config

    * 搜索到“forward-socks5t   /”（不含双引号）那一行，去掉注释的符号，把端口改为1080（系Shadowsocks的SOCKS5端口）

        > forward-socks5t   /               127.0.0.1:1080 .

        ``` bash
        $ hexo new "My New Post"
        ```
    
    * 搜索到“listen-address  127.0.0.1:8118”（不含双引号）那一行，去掉注释的符号，把127.0.0.1改为0.0.0.0（否则只能作用于本机），端口号默认或选择一个未占用的端口

        > listen-address  0.0.0.0:1992

3. 在终端中运行

    ``` bash
    cd /usr/local/sbin/
    ```
    ``` bash
    ./privoxy --no-daemon /usr/local/etc/privoxy/config
    ```

完成上诉步骤，通过访问电脑IP的1992端口即能共享Mac的Shadowsocks。