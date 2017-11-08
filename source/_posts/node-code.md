---
title: node代码片段
date: 2017-11-08 20:49:47
tags: node
categories: 学习笔记
---

- 下载网络资源

```js
var request = require('request');
var fs = require('fs');

/*
* url 网络文件地址
* filename 文件名
* callback 回调函数
*/
function downloadFile(uri,filename,callback){
    var stream = fs.createWriteStream(filename);
    request(uri).pipe(stream).on('close', callback); 
}

var fileUrl  = 'http://p4.so.qhimgs1.com/t01cab6339ead2b1894.jpg';
var filename = '1.jpg';
downloadFile(fileUrl,filename,function(){
    console.log('close');
});
```