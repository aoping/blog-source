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
用定义的参数
```
<%=htmlWebpackPlugin.options.title%>
```

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



## 搭建开发环境
### webpack watch mode



### webpack-dev-serve
live reloading
打包文件？No
搭建本地服务
路径重定向
支持https
浏览器中显示编译错误
接口代理
模块热更新（HRM）
devServer
  inline
  contentBase
  port
  historyApiFallback API重定向
  https
  proxy 远程代理
  hot 模块热更新
  openpage 
  lazy 启动时不打包编译，只初始化打开的页面
  overlay 遮罩编译错误提示

#### HRM
webpack.HotModuleReplacePlugin()
webpack.NamedModulesPlugin()
module.hot // 
module.hot.accept // 接口
module.hot.decline // 接口
style-loader， vue-loader等会自己处理HRM，原生js需要自己写HRM




### express + webpack


## devtool
开发环境 devtool: 'cheap-module-eval-source-map'
生产环境 devtool: '#source-map'

css-loader的signalnon为true时sourceMap没用


## eslint


## 开发与生产环境
### 开发环境
模块热更新
sourceMap
接口代理
代码规范检查


### 生产环境
提取公用代码
压缩混淆
文件压缩或Base64编码
去除无用代码

### 共同点
同样的入口
同样的代码处理
同样的解析配置

webpack-merge拼接不同环境


## webpack分析
1.官网
http://webpack.github.io/analyse/
```js
 webpack --profile -- json > stats.json
```
2.插件
```
npm i webpack-bundle-analyzer --save-dev
var BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin
new BundleAnalyzerPlugin(), // webpack分析

```


##　打包速度
文件多？
页面多？
依赖多？

办法一　分开vendor和app
DllPlugin DllReferencePlugin

办法二　UglifyJsPlugin并行处理　parallel cache

办法三　HappyPack并行，给loader用的

办法四　babel-loader  cacheDirected include exclude

其他　减少resolve  去除sourcemap cache-loader


## 长缓存
要抽出manifest(webpack runtime)

改变业务代码,不能改变vendor--用chunkhash

模块顺序变化，引入新模块，vendor变化--用NamedChunksPlugin NamedModulesPlugin

动态引入模块，vendor变化--定义chunkname

## 多页面应用
### 特点
多入口entry

多页面html

每个页面不同的chunk

每个页面不同的参数

### 实现
两种方式
#### 多配置
webpack
parallel-webpack

优点：可以使用parallel-webpack提高打包速度，配置灵活
缺点：不能多页面间共享代码


####　单配置
优点：多页面间共享代码
缺点：打包慢，　输出内容比较复杂



```
// webpack.web.dll.js

var path = require('path') 
var webpack = require('webpack') 
 
module.exports = { 
  entry: { 
    'vue': ['vue', 'vue-router', 'vuex'] 
  }, 
  output: { 
    path: path.join(__dirname, './src/dll/'), 
    filename: '[name].dll.js', 
    library: '[name]' 
  }, 
  plugins: [ 
    new webpack.DllPlugin({ 
      path: path.join(__dirname, './src/dll/', '[name]-manifest.json'), 
      name: '[name]' 
    }), 
    new webpack.optimize.UglifyJsPlugin() 
  ] 
} 

// 
// new webpack.DllReferencePlugin({ 
    //   manifest: require('./src/dll/vue-manifest.json') 
    // }), 
```

## webpack打包图片
image src和background里的图片可以直接打包
js中的图片要通过require引入
HTML中的图片要html-withimg-loader
```
module: {
　　loaders: [
　　　　{
　　　　　　test: /\.html$/,
　　　　　　loader: 'html-withimg-loader'
　　　　}
　　]
}
```
