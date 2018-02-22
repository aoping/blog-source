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
require.include // 

### import.then()

### 代码分割场景
- 分离业务代码和第三方依赖
- 分离业务代码、业务公共代码和第三方依赖
- 分离首次加载和访问后加载代码

### 

