### `TypeError: webpackMerge is not a function`

问题描述

```js
// webpack.dev.js中用CommonJs导入一个安装好的webpack-merge的时候报了这个错
const WebpackMerge = require('webpack-merge') // 用于合并webpack的配置文件
module.exports = WebpackMerge(webpackConfig, {
    // todo...
})

```

原因分析

```js
// 查看webpack-merge源码
// webpack-merge抛出的是一个对象
// const WebpackMerge = require('webpack-merge') 引用的是一个对象
// 我们需要用的是对象中merge函数

// ...
declare function merge<Configuration extends object>(firstConfiguration: Configuration | Configuration[], ...configurations: Configuration[]): Configuration;
// ....
export { customizeArray, customizeObject, CustomizeRule, merge, merge as default, mergeWithCustomize, mergeWithRules, unique, };

```

解决方法：

```js
// 修复引用方式
const WebpackMerge = require('webpack-merge') // 用于合并webpack的配置文件
module.exports = WebpackMerge.merge(webpackConfig, {
    // todo...
})
```

反思总结：多看官网文档和引用的源码