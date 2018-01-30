---
title: ubuntu常用软件安装
date: 2017-10-06 18:02:45
tags: ubuntu 软件安装
categories: ubuntu
---



http://blog.csdn.net/shidaping/article/details/52218278
http://blog.csdn.net/tao_627/article/details/52635691



安装微信
http://blog.csdn.net/ch593030323/article/details/53571807

<!--more-->

安装qq(2017版)
http://blog.csdn.net/xs18952904/article/details/74931089?locationNum=2&fps=1
http://blog.csdn.net/ysy950803/article/details/52958538


安装迅雷
http://blog.csdn.net/zhuyucheng123/article/details/51147550

登录激活就可以使用了

安装mongodb
http://blog.csdn.net/flyfish111222/article/details/51886787
http://www.cnblogs.com/weschen/p/7395667.html（选择此方法）
```
sudo apt-get install mongodb // 安装mongodb
service mongodb start
service mongodb stop
```
```
sudo systemctl enable mongod    //设置开机启动mongodb服务
sudo service mongod start   //启动服务
systemctl status mongod

```

- MongoError: Authentication failed.
http://cnodejs.org/topic/5617d80941ceb58c4f8e6e37



安装robomongo
http://blog.csdn.net/cristal_tina/article/details/53634209


安装gitbook
http://blog.csdn.net/qq_26437925/article/details/52959733?locationNum=8&fps=1

安装webstorm
http://www.linuxidc.com/Linux/2017-08/146059.htm


安装wps
**下载地址**   
 http://wps-community.org/download.html
**字体缺失下载地址**

启动WPS for Linux后，出现提示"系统缺失字体" 。

出现提示的原因是因为WPS for Linux没有自带windows的字体，只要在Linux系统中加载字体即可。

具体操作步骤如下：

1. 下载缺失的字体文件，然后复制到Linux系统中的/usr/share/fonts文件夹中。

国外下载地址：https://www.dropbox.com/s/lfy4hvq95ilwyw5/wps_symbol_fonts.zip

国内下载地址：https://pan.baidu.com/s/1eS6xIzo

（上述数据来源网络，侵删）

下载完成后，解压并进入目录中，继续执行：

sudo cp * /usr/share/fonts

2. 执行以下命令,生成字体的索引信息：

sudo mkfontscale

sudo mkfontdir

3. 运行fc-cache命令更新字体缓存。

sudo fc-cache

4. 重启wps即可，字体缺失的提示不再出现。


## 安装zsh

```
0.查看shells
cat /etc/shells
1.
sudo yum install zsh
或者
sudo apt-get install zsh
2.
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
3.切换成zsh
chsh -s /bin/zsh
```


## 服务器软件
```
sudo apt-get install vim openssl build-essential libssl-dev wget curl git 
```