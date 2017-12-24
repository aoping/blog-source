---
title: web构建——webpack详解
date: 2017-12-23 10:09:10
tags:
categories:
---
# 构建目的
压缩
优化
缓存
分离js css

<!--more-->

# webpack

## 原理
- 一切皆模块
- 
Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。


## 安装
局部安装执行命令要写完整路径
```js
npm install webpack webpack-dev-server -g // 全局安装
npm install webpack webpack-dev-server --save-dev // 局部安装

npm install webpack@1.2.x --save-dev // 局部安装webpack1
```

## 命令行
webpack配置文件默认名为webpack.config.js
在命令行输入webpack/webpack-dev-server，会在命令执行目录下找webpack.config.js
如果webpack配置文件名字不为webpack.config.js，或不在命令执行目录下，可以输入``` webpack --config ./build/webpack.dev.js ```
```
webpack index.js bundle.js --colors // 把index.js打包成bundle.js
```

### 参数

--progress 打印打包日志

--colors 带颜色的日志

--watch 监控自动打包

-d 生成map映射文件

-p 压缩混淆脚本


## 配置文件
### context
context说明:
1. 它是一个绝对路径，所以要用到path.resolve函数
2. 不设表示起点目录是当前目录
3. 入口文件是在context指定的目录为基础，再往下找

```js
context: path.resolve(__dirname,'src')
```

### entry
- 可为string object array
```js
// 多入口
entry: {
    index: './src/index.js',
    main: './src/main.js'
}
entry: ['./src/index.js','./src/main.js']
// 或单入口
entry: './src/index.js'
```
### output
- filename必须
- filename可以用[name] | [id] | [hash] | [chunkhash]来命名
    [name] 与entry中的key相同
    [id] 与entry中顺序相同，从0开始
    [hash] 每次都不同
    [chunkhash] 文件变化才会改变
- path需是绝对路径，不指定时表示当前目录
```javascript
output: {
    filename: '[name].js',
    path: path.resolve('./build')
}
```

### watch
开启监听模式


### resolve
定义了解析模块路径时的配置，常用的就是extensions，可以用来指定模块的后缀，这样在引入模块时就不需要写后缀了，会自动补全
```js
resolve: {
    extensions: ['', '.js', '.jsx']
}
```

### devtool

devtool选项   配置结果

source-map  在一个单独的文件中产生一个完整且功能完全的文件。这个文件具有最好的source map，但是它会减慢打包速度；

cheap-module-source-map	在一个单独的文件中生成一个不带列映射的map，不带列映射提高了打包速度，但是也使得浏览器开发者工具只能对应到具体的行，不能对应到具体的列（符号），会对调试造成不便；

eval-source-map	使用eval打包源文件模块，在同一个文件中生成干净的完整的source map。这个选项可以在不影响构建速度的前提下生成完整的sourcemap，但是对打包后输出的JS文件的执行具有性能和安全的隐患。在** 开发阶段 **这是一个非常好的选项，在生产阶段则一定不要启用这个选项；

cheap-module-eval-source-map	这是在打包文件时最快的生成source map的方法，生成的Source Map 会和打包后的JavaScript文件同行显示，没有列映射，和eval-source-map选项具有相似的缺点；


### loaders
#### 语法
```js
module: {
    rules: [
        {
            test: /\.css$/,
            use: [
                {loader: 'style-loader'},
                {loader: 'css-loader'},
                {loader: 'less-loader'}
            ],
            exclude: /node_modules/
        },
        {
            test: /\.css$/,
            loader: 'style!css!sass',
            exclude: /node_modules/
        },
        {
            test: /\.css$/,
            use: [
                {
                    loader: "style-loader"
                }, {
                    loader: "css-loader",
                    options: {
                        modules: true, // 指定启用css modules
                        localIdentName: '[name]__[local]--[hash:base64:5]' // 指定css的类名格式
                    }
                }
            ]
        },
        {
            test: /\.vue$/,
            loader: 'vue-loader'
        },
        {
            test: /(\.jsx|\.js)$/,
            use: {
                loader: "babel-loader",
                options: {
                    presets: [
                        "env", "react"
                    ]
                }
            },
            exclude: /node_modules/
        }
    ]
}

```
- loader从右到左加载
- webpack3.*/webpack2.*已经内置可处理JSON文件


#### 参数
test：一个用以匹配loaders所处理文件的拓展名的正则表达式（必须）
use: 
    loader：loader的名称（必须）
    options
include/exclude:手动添加必须处理的文件（文件夹）或屏蔽不需要处理的文件（文件夹）（可选）；
query：为loaders提供额外的设置选项（可选）

#### 常用loader
- babel-loader： 让下一代的js文件转换成现代浏览器能够支持的JS文件。
    ##### 安装
        安装列表：
        babel-core
        babel-cli(如果在命令行使用)
        babel-loader
        babel预置（babel-preset-<es2015,es2016,es2017,env,stage-0,stage-1,stage-2,stage-3>）
        babel插件(babel-plugin-<transform-object-rest-spread>)

    ##### 配置
    babel有些复杂，所以大多数都会新建一个.babelrc进行配置

    方法一：在.babelrc或.babelrc.js中
    ```json
        {
            "presets": [ "env", "stage-0"],
            "plugins": [ "transform-object-rest-spread"]
        }
    ```
    方法二：在package.json中
    ```json
    {
        "name": "",
        "version": "1.0.0",
        "description": "",
        "main": "index.js",
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1"
        },
        "author": "",
        "license": "ISC",
        "devDependencies": {
            "babel-loader": "^7.1.2",
            "babel-plugin-transform-object-rest-spread": "^6.26.0",
            "webpack": "^3.10.0"
        },
        "babel" :{
            "presets": [ "env", "stage-0"],
            "plugins": [ "transform-object-rest-spread"]
        }
    }
    ```


- css-loader,style-loader:两个建议配合使用，用来解析css文件，能够解释@import,url()如果需要解析less就在后面加一个less-loader
    css-loader: css-loader使你能够使用类似@import 和 url(...)的方法实现 require()的功能
    style-loader: 将所有的计算后的样式加入页面中
    postcss-loader: 
- autoprefixer-loader
- file-loader: 生成的文件名就是文件内容的MD5哈希值并会保留所引用资源的原始扩展名
- url-loader: 功能类似 file-loader,但是文件大小低于指定的限制时，可以返回一个DataURL事实上
```js
// webpack.config.js
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
```
- vue-loader


### plugins


#### 常用plugin

- CommonsChunkPlugin: 在打包多个入口文件时会提取出公用的部分，生成common.js
```js
var commonsPlugin = new webpack.optimize.CommonsChunkPlugin('common.js');

```

- ExtractTextWebpackPlugin: 它会将入口中引用css文件，都打包都独立的css文件中，而不是内嵌在js打包文件中
从bundle中提取文本，单独存一个文件，最常用的是将css单独放在一个文件中，当style样式比较大时，这个办法比较好，会加快很多，因为样式和js可以同时请求
```js

var ExtractTextPlugin = require('extract-text-webpack-plugin')
var lessRules = {
    use: [
        {loader: 'css-loader'},
        {loader: 'less-loader'}
    ]
}

var baseConfig = {
    // ... 
    module: {
        rules: [
            // ...
            {test: /\.less$/, use: ExtractTextPlugin.extract(lessRules)}
        ]
    },
    plugins: [BannerPlugin
        new ExtractTextPlugin('main.css') // 参数如果是字符串表示css文件名
    ]
}
```
- HtmlWebpackPlugin: 依据一个简单的index.html模版，生成一个自动引用你打包后的js文件的新index.html
自动生成入口文件dist/index.html，这个文件不会实际生成，只是放在内存中，即使有实际的文件 dist/index.html，也不会读取，还是读取自动生成在内存中的文件
```js
var HTMLWebpackPlugin = require('html-webpack-plugin')
var baseConfig = {
    // ...
    plugins: [
        new HTMLWebpackPlugin()
    ]
}
或
new HtmlWebpackPlugin({
    filename: 'index.html',
    template: './template/index.html',
    inject: true
})
```
- HotModuleReplacementPlugin: 它允许你在修改组件代码时，自动刷新实时预览修改后的结果注意永远不要在生产环境中使用HMR。
```js
new webpack.HotModuleReplacementPlugin()
```
- OccurenceOrderPlugin: 为组件分配ID,通过这个插件webpack可以分析和优先考虑使用最多 的模块，然后为他们分配最小的ID
```js
new webpack.optimize.OccurenceOrderPlugin()
```
- UglifyJsPlugin: 压缩代码
```js
new webpack.optimize.UglifyJsPlugin()
或
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
new UglifyJsPlugin()
```

- BannerPlugin: 在打包的文件中添加注释
```js
var bannerPlugin = new webpack.BannerPlugin({
  banner: '// { "framework": "Vue" }\n',
  raw: true
})
 
```
- NamedModulesPlugin: 显示模块名
```
new webpack.NamedModulesPlugin()
```

- autoprefixer

```js
require('autoprefixer')
```

- OccurenceOrderPlugin:为组件分配ID，通过这个插件webpack可以分析和优先考虑使用最多的模块，并为它们分配最小的ID

```js
new webpack.optimize.OccurrenceOrderPlugin()
```

- clean-webpack-plugin

```js
cnpm install clean-webpack-plugin --save-dev

const CleanWebpackPlugin = require("clean-webpack-plugin");
  plugins: [
    ...// 这里是之前配置的其它各种插件
    new CleanWebpackPlugin('build/*.*', {
      root: __dirname,
      verbose: true,
      dry: false
  })
  ]

```

## 区分环境
```js
// package.json
"scripts": {
    "start": "NODE_ENV=development webpack-dev-server",
    "build": "NODE_ENV=production webpack"
}
```

```js
var ENV = process.env.NODE_ENV
var baseConfig = {
    // ... 
    plugins: [
        new webpack.DefinePlugin({
            'process.env.NODE_ENV': JSON.stringify(ENV)
        })
    ]
}

```

## webpack-dev-server

### 使用方法
方法一：在webpack.config.js里配置
```js
devServer: {
    contentBase: path.join(__dirname, "../public"), //　根目录为 ./public下
    port: 9000, // 端口
    hot:true, // 当有文件变动时，网页重新刷新
    // 这里得装一个插件webpack.HotModuleReplacementPlugin，但当webpack 或 webpack-dev-server启动时，有参考 --hot，那么就不用装这个插件
    inline: true, // 默认是true ?????
    open: true // 自动打开默认浏览器
}
```
方法二：命令行
这种方式会自动刷新页面
```
webpack-dev-server --hot --inline --hotOnly
```
--hot: adds the HotModuleReplacementPlugin and switch the server to hot mode.
--inline: embed the webpack-dev-server runtime into the bundle.
--hot --inline: also adds the webpack/hot/dev-server entry.
--open: 自动打开默认浏览器


方法三：插件
```js
var webpackDevServer = require('webpack-dev-server')
var webpack =require('webpack')
var config = require('./webpack.config.js')

new webpackDevServer(webpack(config),{
    hot: true,
    historyApiFallback: true
}).listen(3000, 'localhost', function (err, result) {
    if (err) console.log(err);
    console.log('Listening at localhost:3000');
  })
```
### options
devserver的配置选项	功能描述
contentBase	默认webpack-dev-server会为根文件夹提供本地服务器，如果想为另外一个目录下的文件提供本地服务器，应该在这里设置其所在目录（本例设置到“public"目录）
port	设置默认监听端口，如果省略，默认为”8080“
inline	设置为true，当源文件改变时会自动刷新页面
historyApiFallback	在开发单页应用时非常有用，它依赖于HTML5 history API，如果设置为true，所有的跳转将指向index.html


## 打包方式
- 命令行
｀｀｀
webpack
webpack-dev-server
｀｀｀

- 使用webpack依赖包
```js
// build.js
const webpack = require('webpack')
const webpackConfig = require('./webpack.config.js');
webpack(webpackConfig, (err, stats) => {
  if (err) throw err
  console.log('已打包好了，我们做点别的事')
})
```
```js
// 执行
node build.js
```
- 使用webpack编译器
```js
// 编译器运行比上面要快些，没有监视，只是编译
const webpack = require('webpack')
const webpackConfig = require('./webpack.config.js');
const compiler = webpack(webpackConfig)
compiler.run( (err, stats) => {
  if (err) throw err
  console.log('已打包好了，我们做点别的事...')
})
```

```js
// 监视&编译
const webpack = require('webpack')
const webpackConfig = require('./webpackfile.js');
const compiler = webpack(webpackConfig)
const watching = compiler.watch({
  /* watchOptions */
}, (err, stats) => {
  // Print watch/build result here...
  console.log('我一直在监视着呢');
});
```

## 示例
### vue


## 常见问题

## 专题
### HMR

HMR意思是不需要刷新页面，改动就可以直接展示在页面上，依赖于webpack-dev-server
首先需要安装这两个库，npm install --save-dev webpack-dev-server react-hot-loader
安装完成后，就要开始配置了，首先需要修改entry配置：
```
entry: {
  helloworld: [
    'webpack-dev-server/client?http://localhost:3000',
    'webpack/hot/only-dev-server',
    './helloworld'
  ]
},
```
通过这种方式指定资源热启动对应的服务器，然后需要配置react-hot-loader到loaders的配置当中，比如我的所有组件代码全部放在scripts文件夹下：
```
{
  test: /\.js?$/,
  loaders: ['react-hot', 'babel'],
  include: [path.join(__dirname, 'scripts')]
}
```
再配置一下plugins，加上热替换的插件和防止报错的插件：
```
plugins: [
  new webpack.HotModuleReplacementPlugin(),
  new webpack.NoErrorsPlugin()
]
```
最后在index.js里加上
```
//HMR 接口
if(module.hot){
    module.hot.accept('./component',()=>{
        const nextComponent=component();
        document.body.replaceChild(nextComponent,demoComponent);
        demoComponent=nextComponent;
    })
}
```
这样配置就完成了，但是现在要调试需要启动一个服务器，而且之前配置里映射到http://localhost:3000，所以就在本地3000端口起个服务器吧，在项目根目录下面建个server.js：
```
var webpack = require('webpack');
var WebpackDevServer = require('webpack-dev-server');
var config = require('./webpack.config');

new WebpackDevServer(webpack(config), {
  publicPath: config.output.publicPath,
  hot: true,
  historyApiFallback: true
}).listen(3000, 'localhost', function (err, result) {
  if (err) console.log(err);
  console.log('Listening at localhost:3000');
});
```

### vue HMR
// TODOS


### react HMR
// TODOS

### express HMR
// TODOS




## 实战
- 命令行把index.js打包成bundle.js
```js
webpack ./index.js bundle.js --colors
```
- js引入js/css
```js
require('2.js')
require('style!css!./main.css')
```
- 打包css
    方法一：引入css时解析
    ```
    require('style!css!./main.css')
    ```
    方法二：命令行
    ```
    webpack ./entry.js bundle.js --module-bind 'css=style!css'
    ```
    方法三：配置文件
    ```js
    module: {
        rules: [
            {
                test: /\.css$/,
                loader: "style!css"
            }
        ]
    }
    ```



# babel https://babeljs.io/
## babel stage
stage-0 = stage-1 + transform-do-expressions + transform-function-bind
stage-1 = stage-2 + transform-class-constructor-call (Deprecated) + transform-class-properties + transform-decorators + 
 transform-export-extensions
stage-2 = stage-3 + syntax-trailing-function-commas + transform-object-reset-spread
stage-3 = transform-async-to-generator + transform-exponentiation-operator

## 命令行
```
babel script.js --presets stage-0

```
