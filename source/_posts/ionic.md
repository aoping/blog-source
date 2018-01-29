---
title: ionic
date: 2018-01-26 14:37:59
tags: ionic
categories: 学习笔记
---


## angular 4语法

- 单向绑定 {{}}
- 双向绑定 [(ngModel)]="editorMessage"
- 后台获取dom viewChild 
```js
  // ts
  @ViewChild(Content) content: Content; //全局的 content
  @ViewChild('chatInput') messageInput: TextInput; //获取前台的输入框

  // html
  <ion-textarea
        #chatInput
        [(ngModel)]="editorMessage"
        (keyup.enter)="sendMessage()"
        (focus)="focus()"
        placeholder="输入内容"></ion-textarea>
```


