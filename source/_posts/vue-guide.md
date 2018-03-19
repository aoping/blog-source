---
title: vue入门
date: 2018-03-17 11:23:19
tags: vue
categories: vue
---

# 什么是 Vue

vue 优点： 轻量级 高效率 上手快 简单易学 文档全面简洁

vue 包括 模板渲染 模块化 扩展功能（路由 ajax)

## 前置知识

node
html js css
es6/7

# 知识

## 安装

```
npm i vue
```

## vue 实例

## 生命周期

beforeCreated creaed mounted destroyed

## 组件

### 注册

#### 全局组件

```vue
Vue.component('my-header',{
  template:'<p>{{a}}</p>',
  data: function(){
    return {
      a: 1
    }
  }
})
```

#### 局部组件

```
var myHeader = {
  template:'<p>{{a}}</p>',
  components: {
    'my-header-child': myHeaderChild
  }
}

components: {
  'my-header': myHeader
}
```

# 基础

v-text

v-html

* 对象循环

```
v-for="(value,key) in object"
```

数组循环

```
v-for="(item,index) in array"
```

## 触发更新

## $set

## 标签属性绑定

```

```

## 事件绑定

### 事件修改器

@keydown.13

### 自定义事件

### 组件事件传递

# 组件

通过 is 动态引入组件

keep-alive

# 动画

# 指令

# 插件

vue-router

vue-resource

安装 -> 引入 -> 注册插件 -> 实例化 -> 挂载

```js
npm i vue-router --save
import VueRouter from 'vue-router'
Vue.use(VueRouter)
const router = new VueRouter({
  // mode: 'history',
  saveScrollPosition: true,
  scrollBehavior: () => ({
    y: 0
  }),
  routes: map
})
new Vue({
  router,
  data() {
    return {

    }
  }
})
```

# vue 脚手架
