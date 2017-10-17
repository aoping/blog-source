---
title: php安装
date: 2017-10-17 14:26:19
tags: software php
categories: 学习笔记
---

windows下PHP环境的搭建:
https://segmentfault.com/a/1190000003409708

在windows下的CLI模式下如何运行php文件
https://jingyan.baidu.com/article/da1091fb096c97027849d68e.html

执行httpd -k install 发生 could not bind to address 0.0.0.0:80
这是因为iis占用了80端口
可以在管理员权限下cmd执行
```
Windows 7/Vista
net stop was /y
or XP:
net stop iisadmin /y
```
https://www.sitepoint.com/unblock-port-80-on-windows-run-apache/