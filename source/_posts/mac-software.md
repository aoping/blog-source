---
title: mac常用软件
date: 2017-11-28 09:32:37
tags: software
categories: software
---

# 装机软件

## 常用
1. 谷歌浏览器 √
2. 360浏览器 √
3. foxmail √
4. qq 微信 √
5. 网易云音乐 √
6. teamviewer √
7. 番茄土豆 √
8. MPlayerX √
9. 迅雷 √
10. ps 
11. wps √
12. TightVNC
13. 搜狗输入法 √
14. gitbook
15. iThoughtsX
- BetterZip
- AppZapper
- shotcat  键盘操作


## 开发

### 开发环境 
1. homebrew http://brew.sh/ √
2. git √
1. nvm √ 一定要比node先安装
1. nrm √
2. node npm yarn √
3. arc
4. java √
5. python 2.7.13 √
6. ruby √
7. php -> vs studio 2017 要修改php.ini 参考 http://blog.csdn.net/rilyu/article/details/37379873 √ 

#### 脚手架
1. hexo-cli √
2. weex-toolkit √
3. 





### 开发软件

1. gitkraken √
2. sourcetree √
3. vscode √
4. cmder √
5. git bash √
6. mongodb √
7. Robomongo 0.9.0-RC9 √
8. virtual box
9. webstorm
10. RedisDesktopManager
11. android studio
12. Charles
13. Genymotion
14. mysql-workbench
15. sublimeText √
16. notepad++ √
17. TortoiseSVN
18. atom
19. mysql
20. IntelliJ IDEA 2017.1.2
21. 

### mac使用
文本编辑快捷键 http://www.cnblogs.com/wangfenjin/archive/2012/09/06/2672871.html

键盘快捷键
Mission Control          Ctrl ＋ 上
应用程序窗口              Ctrl ＋ 下
切换工作空间             Ctrl ＋ 左/右
显示桌面                     F11
显示DashBoard          F12
切换窗口    command ＋ tab
最小化窗口有快捷键（Cmd+M）



### 安装教程
#### arcanist
https://secure.phabricator.com/book/phabricator/article/arcanist/#installing-arcanist

#### 安装ssh
https://help.github.com/articles/connecting-to-github-with-ssh/


### 问题

#### CocoaPods not working in macOS High Sierra
- sudo gem update --system
sudo gem install -n /usr/local/bin cocoapods

pod install


#### pod install 安装失败
xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance

https://www.jianshu.com/p/07a281ff57d3

#### 把PHP设为全局path
php: command not found 命令找不到
export PATH=$PATH:/usr/local/PHP/bin