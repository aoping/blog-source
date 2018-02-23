---
title: webpack-learn
date: 2018-02-22 21:40:12
tags:
categories:
---



# 3.2 webpack 支持es6 commonjs amd(异步加载方式)

# 3.3 编译es6
babel-loader  babel-core babel-preset-env

### preset
babel-preset-env
```js
targets: {
  browser: ['> 1%', 'last 2 versions']
}

```

### plugins
babel-polyfill(全局垫片，为开发应用准备的)
babel-runtime-transform　（局部垫片，为框架准备的）
```
npm install babel-polyfill babel-runtime --save
npm install babel-plugin-runtime-transform --save-dev
```

# 3.5 提取公用模块
CommonsChunkPlugin
## 应用场景
- 单页应用
- 单页应用　＋　第三方依赖
- 多页应用　＋　第三方依赖　＋　webpack生成代码

注意：CommonsChunkPlugin对单页应用并没有用，要用懒加载


## 打包第三方依赖
```js
entry: {
  'vendor': ['jquery', 'lodash]
}
new webpack.optimize.CommonsChunkPlugin({
        name: 'vendor',
        minChunks: Infinity
      })
```


## 代码分割和懒加载

### require.ensure
注意不会执行
```js
require.ensure(['lodash'], function() {
  var _ = require('lodash')

},'vendor')
```
require.include // 

### import.then()

### 代码分割场景
- 分离业务代码和第三方依赖
- 分离业务代码、业务公共代码和第三方依赖
- 分离首次加载和访问后加载代码

## 处理css
引入
css modules
配置less / sass
提取css代码

### style-loader 插入style标签
  options: 
    insertInto 
    singleton 
    transform // 在插入浏览器之前执行，根据浏览器而变化
- style-loader/url 插入style标签链接
```
style-loader/url!file-loader
```
- style-loader/useable 样式的引用与否
```
import base from './base.css'
base.use()
base.unuse()
```


### css-loader import css文件
options
  alias
  modules

#### css modules
:local
:global
composes 
composes: ... from  // 注意引入顺序，应该写在第一行

### postcss
```
npm install postcss postcss-loader autoprefixer cssnano postcss-cssnext --save-dev 
```


## tree shaking
### js: uglifyjs

本地tree shaking
第三方库tree shaking

lodash不能通过常规来tree shaking
可以用babel-plugin-lodash

### css: purifycss
```
npm install purifycss-webpack glob-all --save-dev
```


## 文件处理
file-loader url-loader img-loader postcss-sprites
### 图片处理
#### css引入的图片

自动合成雪碧图
postcss-sprites
spritePath
retina: true
压缩图片
Base64编码

### 字体处理
### 第三方库处理

webpack.providePlugin
imports-loader
window

##### jquery
1.引入CDN地址，可以直接使用
2. webpack.providePlugin
```
new webpack.providePlugin({
  $: 'jquery'
})
```
3. 来自自己的一个目录中
配合resolve使用

4. imports-loader
```

  test: path.resolve(__dirname,'app.js'),
  use: [{
    loader: 'imports-loader',
    options: {
      $: 'jquery'
    }
  }]

``

### html-webpack-plugin
处理html中的图片
1.用html-loader来
```js
{
  test: /\.html$/,
  use: [
    {
      loader: 'html-loader',
      options: {
        attrs: ['img:src','img:data-src']
      }
    }
  ]
}
```

2.在HTML中用require引入图片
```
<img :src="$require('')">
```

## html配合优化
html-webpack-inline-chunk-plugin 把js直接插入HTML
inline-mainfest-webpack-plugin 把js直接插入HTML,有bug



