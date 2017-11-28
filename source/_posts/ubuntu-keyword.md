---
title: ubuntu使用技巧
date: 2017-10-15 09:25:37
tags: ubuntu 使用技巧
categories: ubuntu
---

**分屏显示**

- ctrl+Windowskey(Super key)+上下左右

**多窗口分屏式终端--Terminatgongzuoquor**

- 可在同一屏打开多个窗口，安装如下
```
sudo apt-get install terminator
```

![1.png](1.png)
**显示桌面/开启工作区**
- 依次打开系统设置，外观，行为，在中间有开启工作区和添加“显示桌面”图标到启动器，勾选即可
- alt+ctrl+方向箭头 切换工作区
<!--more-->

**显示隐藏文件**
- ctrl+h



## 命令
**创建用户**
```
useradd zoro -m -s /bin/bash
passwd zoro
su zoro
gpasswd -a zoro sudo //sudo分组

```


