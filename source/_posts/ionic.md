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
- 发布订阅模式 events  类似vue $emit
```js
this.event.publish('chat.received', messageSend, Date.now())

this.event.subscribe('chat.received', (msg, time) => {
      this.messageList.push(msg);
      this.scrollToBottom();
    })
```

- 向组件传递参数 @input
- 组件没有生命周期 
- 扫描二维码要 animate:false