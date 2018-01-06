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

- loader
css-loader style-loader babel-loader

- 提取css
ExtractTextPlugins
```js
const ExtractTextPlugin = require("extract-text-webpack-plugin");

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


