---
title: 慕课网电商学习笔记
date: 2018-01-06 10:08:31
tags:
categories:
---

### 模块化方案
JavaScript模块化 --- Commonjs、AMD、CMD、ES6 modules https://zhuanlan.zhihu.com/p/32324311?utm_medium=social&utm_source=wechat_session
AMD
CMD
CommonJS
ES6
### 架构设计
![架构设计](http://ozpjnt6fg.bkt.clouddn.com/1.png)
### 技术选型
![技术选型](http://ozpjnt6fg.bkt.clouddn.com/1.png)
软件过程
前后端分离
模块化方案
框架选择
打包方案
版本控制
发布过程
### 软件要求
nodejs&npm
git
sublime/vscode

### 代理服务器
charles fiddle

### 项目初始化

#### .gitingore
```
.DS_Store
/node_modules/
/dist/
```
#### webpack
webpack2.x有bug，不兼容ie8, 因为default是保留字
webpack支持commonjs和es6模块引入
- 公共模块
CommonsChunkPlugins

  明确第三方库（jquery lodash等，这些应该利用长期缓存）
  ```js
    entry: {
      vendor: ["jquery", "other-lib"],
      app: "./entry"
    },
    plugins: [
      new webpack.optimize.CommonsChunkPlugin({
        name: "vendor",
        // filename: "vendor.js"
        // (给 chunk 一个不同的名字)

        minChunks: Infinity,
        // (随着 entry chunk 越来越多，
        // 这个配置保证没其它的模块会打包进 vendor chunk)
      })
    ]
  ```
疑问：
  抽取css模块？？？



- loader
css css-loader style-loader postcss-loader autoprefixer-loader
js babel-loader
模板引擎 html-loader ejs-loader
图片 url-loader file-loader image-webpack-loader(压缩)

** import进来的css不会经过后面的loader？ **

用less的时候可以不用importLoaders

import进来的css会被单独成一个style标签
```js
module: {
  rules: [
    {
      test: /\.css$/,
      loader: 'style-loader!css-loader?importLoaders=1!postcss-loader'
    }
  ]
},
postcss: [
  require('autoprefixer')({
    browsers: ['last 5 versions']
  })
]
```
- 提取css
ExtractTextPlugins
```js
const ExtractTextPlugin = require("extract-text-webpack-plugin");
// webpack1
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "css-loader"
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin("styles.css"),
  ]
}

// webpack2
module: {
  rules: [
    {
      test: /\.css$/,
      use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "css-loader",
          publicPath: "/dist"
      })
    }
  ]
},

new ExtractTextPlugin("[name].css"), // name是entry名
```


- copy-webpack-plugin
```js
var Copy = require('copy-webpack-plugin')
//  文件拷贝插件,将图片和字体拷贝到dist目录
var copyPlugin = new Copy([
  { from: './src/assets/images', to: './images' },
  { from: './src/assets/font', to: './font' }
])
```


- BannerPlugin
```js
var bannerPlugin = new webpack.BannerPlugin({
  banner: '// { "framework": "Vue" }\n',
  raw: true
})
```


- HtmlWebpackPlugin
如果HTML中要用ejs模板引擎，需要``` html-loader```
```js
var HtmlWebpackPlugin = require('html-webpack-plugin');
var path = require('path');

var webpackConfig = {
  entry: 'index.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js'
  },
  plugins: [new HtmlWebpackPlugin()]
};
```
把js以inline的形式引入
```html
  <!-- index.html -->
  <% compilation.assets[htmlWebpackPlugin.files.]%>

  <script></script>
```


- 图片 字体
url-loader   file-loader
```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
}
```
#### webpack-dev-server
方法一二都是自动刷新（不推荐）

方法一： 访问http://localhost:8080/webpack-dev-server
  原理：用iframe包裹
  好处：不用修改配置文件
  坏处：URL路径不会改变

方法二：
  在entry后面加下面的代码
  ```js
  'webpack-dev-server/client?http://localhost:8088/'
  ```
  然后命令行输入
  ```
  webpack-dev-server --inline --port 8088
  ```
#### package.json
```json
  "dev": "WEBPACK_ENV=dev webpack-dev-server --inline --port 8088",
  "dev_win": "set WEBPACK_ENV=dev && webpack-dev-server --inline --port 8088",
```
```js
$ webpack --config XXX.js   //使用另一份配置文件（比如webpack.config2.js）来打包

$ webpack --watch   //监听变动并自动打包

$ webpack -p    //压缩混淆脚本，这个非常非常重要！

$ webpack -d    //生成map映射文件，告知哪些模块被最终打包到哪里了
```

#### 几点疑问
##### html-webpack-plugin
参考 https://segmentfault.com/a/1190000007294861
https://www.cnblogs.com/wonyun/p/6030090.html
- html-webpack-plugin引入js css的顺序有什么规则？

- html-webpack-plugin怎么只引入相关的js
  有个chunks字段，在里面引入相关chunk即可
  ```js
  var HtmlWebpackPlugin = require('html-webpack-plugin')
   new HtmlWebpackPlugin({
      title       : '首页',
      inject: true,
      hash: true,
      chunks      : ['common', 'index']
    })
  ```
- hash为true改一个文件就所有的hash都会改变？
  该 hash 值是该次 webpack 编译的 hash 值
- 

#### webpack进阶教程（二）——webpack引入jquery多种方法探究
https://segmentfault.com/a/1190000007249293

- html模板引擎中引入图片最好用cdn图片，也可以用require
```ejs
${require('../asserts/img/a.png')}
```


### git
#### 命令及简写

```

```

### 通用页面
头部
侧边栏
通用提示页



### 常见技巧
- 开发中遇到跨域问题
  可以用charles重定向


### 疑问
- 怎么利用缓存以及缓存带来的危害？
  利用hash，是文件的hash还是``` ?hash ```
  有三种hash (hash chunkhash ?hash)
  chunkhash


# 开发和生产

## 开发


## 生产



### 常用配置
```js
// webpack.config.js
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
var ExtractTextPlugin   = require('extract-text-webpack-plugin')
var ignorePlugin = new webpack.IgnorePlugin(/jquery.min.js/);

// 获取html-webpack-plugin参数的方法 
var getHtmlConfig = function(name, title){
  return {
      template    : './view/' + name + '.html',
      filename    : 'view/' + name + '.html',
      title       : title,
      inject      : true,
      hash        : true,
      chunks      : ['common', name]
  };
};

module.exports = {
  entry: {
    'list': path.resolve(__dirname, './app/list.js'),
    'index': path.resolve(__dirname, './app/index.js'),
  },
  output: {
    filename: '[name].[chunkhash].js',
    path: path.resolve(__dirname, './dist')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
            fallback: "style-loader",
            use: "css-loader",
            publicPath: "/dist"
        })
      }
    ]
  },
  // externals : {
  //   'jquery' : 'window.jQuery'
  // },
  plugins: [
    // 独立通用模块到js/base.js
    new webpack.optimize.CommonsChunkPlugin({
        name : 'common',
        filename : 'js/base.js'
    }),
    // 把css单独打包到文件里
    new ExtractTextPlugin("[name].[chunkhash].css"),
    // new ExtractTextPlugin("common.css"),
    
    new HtmlWebpackPlugin(getHtmlConfig('index', '首页')),
    new HtmlWebpackPlugin(getHtmlConfig('list', '商品列表页')),
    ignorePlugin
  ]
}
```