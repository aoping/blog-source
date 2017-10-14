---
title: es6-async
date: 2017-10-14 09:55:55
tags: es6 异步
categories: es6
---

## 回调地狱
在es5时代，js只能用callback来进行异步操作，这不仅不宜阅读，而且极难调试。
```
var fs = require('fs');
fs.readFile('a.json', function(error, data){
  if (error) console.log(error);
  else {
    fs.readFile('b.json', function(error, data){
      if (error) console.log(error);
      else {
        console.log(data);
      }
    });
  }
});
```
<!--more-->

Promise的出现解决了这个问题

## Promise
es6给我们带来了Promise,这极有效的避免了回调地狱
```
var fs = require('fs');

var readFile = function (fileName){
  return new Promise(function (resolve, reject){
    fs.readFile(fileName, function(error, data){
      if (error) reject(error);
      resolve(data);
    });
  });
};

readFile(a.json).then(es => {
  readFile(b.json).then(es => {
    console.log(a,b)
  })
})
```
大家可以试一下如果用callback,这段代码如何写
但是，也许大家发现了如果要再读取多个问题，也是非常繁琐，这就是generator要解决的问题

## generator/yeild/co
Generator 函数是协程在 ES6 的实现，最大特点就是可以交出函数的执行权（即暂停执行）
```
var fs = require('fs');

var readFile = function (fileName){
  return new Promise(function (resolve, reject){
    fs.readFile(fileName, function(error, data){
      if (error) reject(error);
      resolve(data);
    });
  });
};

var gen = function* (){
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```
也许大家发现了也不好阅读，下面就是今天的主角async

## async/await

async/await是generator的语法糖,是es7提案
async返回一个Promise对象，使用then获取返回值，可以用try...catch获取异常
await正如字面意思等待的意思，后面可以是任意的表达式(不用关心它是不是异步)
await只能在asnyc内
希望多个请求并发执行时，用Promise.all

async的优点
内置执行器、更好的语义、更广的适用性

```
function sleep(second) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('request done! ' + Math.random());
        }, second);
    })
}
async function correctDemo() {
    let p1 = sleep(1000);
    let p2 = sleep(1000);
    let p3 = sleep(1000);
    await Promise.all([p1, p2, p3]);
    console.log('clear the loading~');
}
correctDemo();// clear the loading~
```

## 参考链接
http://www.ruanyifeng.com/blog/2015/05/async.html
https://juejin.im/entry/59df22c16fb9a0452340df42
