---
title: video-learn
date: 2018-04-11 13:02:15
tags:
categories:
---

# vue 饿了么

## vue1 与 Vue2 的变化

### 子组件派发事件

```
// vue1
// 子组件派发
this.$dispatch('click',data)
// 父组件接收
events: {
    click(data){

    }
}

// vue2
// 子组件派发
this.$emit('click',data)
// 父组件接收
需绑定在组件上
```

### ref 绑定

```
// vue1
v-ref:'comp'

// vue2
ref=""
```

### 获取 dom

```
// vue1
v-el:food
this.$els.food

// vue2
ref=""
```

### 子组件不能修改 props 属性

### 过渡变化

### vue-router api 改变

v-link -> route-view
router api

## 技巧

### 正方形图片

```css
img {
  width: 100%;
  height: 0;
  padding-top: 100%;
}
```

## vue 获取 dom

```
v-el:food
this.$els.food
```

## vue 获取组件

```
ref="comp"
this.$refs.comp
```

## 延迟执行

```
this.$nextTick(()=>{

})
```

## props 传入对象

组件的值变化，外面也会变化

## 1px

```

```

## 2x3x 图

```

```

## better-srcoll

需要在获取数据后创建或刷新

## better-scroll 获取不到元素时，可以利用过渡效果

```

```

## 移动端点击解决方案

fastclick

## chrome 显示不了小于 12px 的大小

## 上下居中对齐

```css
.middle {
  display: inline-block;
  vertilcal-align: top;
}
```

## switch on 属性绑定在最外层，以便点击全部位置可以改变样式

### 是否显示元素

```
v-show="show()"
filter
```

### 自适应

flex 布局
@media

### 时间戳格式化

### 获取 query 对象

### 给 data 初始化赋值

自执行函数

```
data(){
    return {
        xxx:(()=>{
            return 1
        })()
    }
}
```

### 设备像素比

# 音乐播放器

## 技巧

### 导入组件首字母要大写

### jsonp

https://github.com/webmodules/jsonp

#### 原理

通过 script 标签的跨域获取回调

### window resize 事件

```
window.addEventListen("resize",()=>{})
```

### 后端代理请求

修改 refer 等

### 延时执行

20 是因为 17ms 是 dom 刷新时间

```
setTimeout(（）=>{

},20)
```

### 标识变量不需要放在 data 里

### 图片加载好有一个事件 onload

这时可以监听做些操作，如 better-scroll 的刷新

### 图片懒加载

vue-lazyload

### fastclick 与 better-scroll 冲突

在需要点击的元素上添加 class="needclick"

### 格式化数据

\_\_normalizeSinger

### req 可以用 class 来定义

```
export class x {
    constructor({id, name}) {
    this.id = id
    this.name = name
    this.avatar = `https://y.gtimg.cn/music/photo_new/T001R300x300M000${id}.jpg?max_age=2592000`
  }

}
```

### 数组拼接

concat

### 获取元素高度

clientHeight

### 尽量用硬件加速

transation3d

### vuex

开启浏览器调试工具

```
const debug = process.env.NODE_ENV !== 'production'
```

### 通用

构造数据对象

### transform-origin

从哪里开始变化 top

### ios 高斯模糊

```css
backdrop: blur(20px);
```

### 居中显示

```css
.loading-container
        position: absolute
        width: 100%
        top: 50%
        transform: translatey;
```

### 动画

#### css 动画

#### js 钩子

create-keyframe-animation

### audio 播放

#### api

```
play
```

## 工具

#### url 拼接

#### 获取 URL parms

#### addClass hasClass

#### 获取 data-index

```

```

#### 为 js 添加浏览器前缀

```js
let elementStyle = document.createElement("div").style;

let vendor = (() => {
  let transformNames = {
    webkit: "webkitTransform",
    Moz: "MozTransform",
    O: "OTransform",
    ms: "msTransform",
    standard: "transform"
  };

  for (let key in transformNames) {
    if (elementStyle[transformNames[key]] !== undefined) {
      return key;
    }
  }

  return false;
})();

export function prefixStyle(style) {
  if (vendor === false) {
    return false;
  }

  if (vendor === "standard") {
    return style;
  }

  return vendor + style.charAt(0).toUpperCase() + style.substr(1);
}
```
