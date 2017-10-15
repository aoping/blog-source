---
title: express知识点
date: 2017-10-15 08:50:13
tags: node express 学习笔记
categories: node
---


## 安装express
```
npm i express -g
```

## express生成器
### 安装
```
npm i express-generator -g
```
### 使用
```
express -h // 帮助
express myapp //生成app

```
### 安装依赖
```
cd myapp
npm i
```

### 启动
```
DEBUG=myapp npm start  // mac or linux
set DEBUG=myapp & npm start // windows
```

## express架构

```
var express = require('express')
var app = express()

// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');
```
