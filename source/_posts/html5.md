---
title: html5
date: 2017-10-03 08:54:20
tags: html html5
categories: html
---
# 本节主要记录html5的相关知识

<!--more-->


## 推出的理由
- web浏览器之间兼容性很低
- 文档结构不够明确
- web应用程序功能收到限制


## 语法的改变
- 内容类型
- doctype声明
- 指定字符编码
- 可以省略标记的yuans
- 省略引号
- boolean值可以省略

## 元素
### 新增的结构元素
section article aside header hgroup footer nav figure

#### 主题结构元素

- article
    有header p footer
    可以嵌套
    特殊的section
- section    
    需要设置样式时用div
    有标题内容h1才使用section
    可以嵌套
- nav
    应用场景：
```
<nav>
    <h2>xxx</h2>
    <ul>
        <li><a></a></li>
    </ul>
</nav>
```

- aside
    表示当前页面或文章的附属信息部分，相关引用、侧边栏、广告、导航条等

- time与微格式

    ```
        <time datetime="2015-10-10" pubdate>2015-10-10</time>
        
    ```


#### 非主体结构元素
- header footer hgroup
    hgroup包裹h1-h6,表示子标题
- address


#### 表单新增元素



#### 


### 网页编排规则
- 显示编排内容区域块
- 显示编排内容区域块
- 标题分级
- 不同区块可以使用相同标题




### 新增的其他元素
video audio embed mark progress meter time canvas

### 新增的input类型
email url number range DatePickers

### 废除的元素
- 能使用css代替的元素 basefont big center font s tt u等
- 不再使用frame框架
- 只有部分浏览器支持的元素
- 其他被废除的元素


## 属性
### 新增的属性

#### 表单内元素的form属性


### 废除的属性

### 全局属性
contentEditable 可以继承
designMode只能在js里编辑
hidden
spellcheck 对input textarea检查
tabindex 设置为-1（可以通过js获取到）



# 新增api









