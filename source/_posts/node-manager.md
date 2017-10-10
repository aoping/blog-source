---
title: node版本管理
date: 2017-10-10 14:22:47
tags: node
categories: node
---

Node版本管理器有nvm n nvmw nvm-windows等，但这些对操作系统都有要求，下面根据不同操作系统简单介绍一下

<!--more-->

# windows

## nvmw
https://github.com/hakobera/nvmw


## nvm-windows(推荐)

github地址：https://github.com/coreybutler/nvm-windows

### 安装nvm-windows


- 如果之前安装过node, 需要删除相应的安装目录，避免有影响
主要检查以下两个目录

```
C:\Program Files\nodejs
C:\Users<user>\AppData\Roaming\npm
```

- 下载发布包https://github.com/coreybutler/nvm-windows/releases，下载nvm-setup.zip，解压后点击exe文件，进行安装即可

### 安装node

如 
``` 
nvm install 6.11.4 
```


### 使用相应版本的node

```
nvm use 6.11.4
```


### 其他命令

```
nvm list  查看安装的node版本
nvm uninstall <version> 卸载
nvm version 查看nvm的版本
```

### 配置npm
- 执行命令，执行成功在
``` 
C:\Users\<你的用户名> 
```
下会生成.npmrc文件

```
npm config set prefix "G:\software\npm-global"
```

- 再次是配置环境变量,
```
设置——系统——关于——系统信息——高级程序设置——环境变量——xxx用户的变量
```
如果你之前安装过npm, 则将
``` 
C:\Users\你的用户名\AppData\Roaming\npm
```
 改为 
 ``` 
 G:\software\npm-global 
 ```
反之直接添加PATH
``` 
G:\software\npm-global 
```

### 安装nrm
nrm（npm registry manager ）npm的镜像源管理工具   https://github.com/Pana/nrm
- 安装
```
npm install -g nrm
```
- 其他命令
```
nrm ls    展示所有可切换的镜像地址
nrm use cnpm    切换到cnpm
```


### 安装cnpm

如果你安装了nrm，可以忽略
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
npm install -g cnpm --registry=http://r.cnpmjs.org
```

### 全局安装模块

```
npm install hexo-cli -g
```

### 其他

任何全局npm模块在您已安装的各种版本的node.js之间不共享



# linux(ubuntu)

## nvm

install using curl

```
curl https://raw.githubusercontent.com/creationix/nvm/v0.20.0/install.sh | bash
```

install using wget

```
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.20.0/install.sh | bash
```

## n




