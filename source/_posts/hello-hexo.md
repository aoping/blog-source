---
title: hello-hexo
date: 2017-09-30 13:06:10
tags: hexo
categories: hexo
---

# 命令
```
npm install -g hexo-cli
hexo init [folder]
hexo new [layout] <title>
hexo generate hexo g
hexo publish [layout] <filename>
hexo server
hexo s --debug 
hexo deploy hexo d
```

# 技巧
## 折叠

```
<!-- more -->
```
## 引用自己的文章
```
{% post_link markdown-learning-by-maxiang 点击这里查看这篇文章 %}
```
- markdown-learning-by-maxiang是你的文章名称