---
title: 'SSH连线时出现「WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!」'
date: 2016-12-29 14:24:03
tags:
---
## SSH连线时出现「WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!」解决方法

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
这里依每台电脑而不同
Please contact your system administrator.
Add correct host key in /home/conbar/.ssh/known_hosts to get rid of this message.
Offending key in /home/conbar/.ssh/known_hosts:10
RSA host key for 这里是服务器的IP或网址 has changed and you have requested strict checking.
Host key verification failed.
```
* 会出现这信息是因为，第一次SSH连现时，会生成一个认证，储存在客户端中的known_hosts，但是如果服务器端重装过，认证信息也会更改，服务器端与客户端不同时，就会跳出错误。因此，只要把电脑中的认证信息删除，联机时重新生成，就能解决。要删除很简单，只要在客户端输入以下命令

```
ssh-keygen -R 服务器端的IP或网址
```
