## 1、核⼼概念之 Entry

### Entry ⽤来指定 webpack 的打包⼊⼝

### 原理依赖图

<img src="https://raw.githubusercontent.com/YuanWenLai/Note.IO/main/%E5%89%8D%E7%AB%AF%E5%B7%A5%E7%A8%8B%E5%8C%96%E5%AD%A6%E4%B9%A0/webpack/imgaes/entry.png"  />

### 理解：

- 依赖图的入口是entry
- 对于非代码比如图片、字体依赖也会不断加入到依赖图中

### Entry的基本用法：

1. 单入口：entry是一个字符串

   ```js
   module.export = {
   	entry: './path/my/test/index.js'
   }
   ```

2. 多入口：entry是一个对象

   ```js
   module.export = {
   	entry: {
           app: './src/index.js',
           adminApp: './src/adminApp.js'
       }
   }
   ```



## 2、核⼼概念之 Output

### Output ⽤来告诉 webpack 如何将编译后的⽂件输出到磁盘

### Output 的基本用法：

1. 单入口：

   ```js
   module.export = {
   	entry: './path/my/test/index.js',
       output: {
           filename: 'bundle.js',
         },
   }
   ```

2. 多入口：通过占位符确保⽂件名称的唯⼀

   ```js
   module.export = {
   	entry: {
           app: './src/index.js',
           adminApp: './src/adminApp.js'
       },
       output: {
           filename: '[name].js',
           path: __dirname + '/dist',
       },
   }
   ```



## 3、核⼼概念之 Loaders

- webpack 开箱即用只支持 JS 和 JSON 两种文件类型，通过 Loaders 去支持其它文件类型并且把它们转化成有效的模块，并且可以添加到依赖图中。
- loader本身是一个函数，接受源文件作为参数，返回转换的结果。

### 常用的Loaders有哪些？

| 名称          | 描述                       |
| :------------ | -------------------------- |
| babel-loader  | 转换es6、es7等js新特性     |
| css-loader    | 支撑.css文件的加载和解析   |
| less-loader   | 支持less转化为css          |
| ts-loader     | 将TS转化为js               |
| file-loader   | 进行图片、字体等文件的打包 |
| raw-loader    | 将文件以字符串的形式导入   |
| thread-loader | 多进程打包js和css          |



### Loaders 的基本用法：

1. 单入口：

   ```js
   module.exports = {
     module: {
       rules: [
         { test: /\.css$/, use: 'css-loader' },
         { test: /\.ts$/, use: 'ts-loader' },
       ],
     },
   };
   ```



## 4、核⼼概念之 Plugins

- 插件主要用于loaders实现不了的场景。
- 插件用于bundle文件的优化，资源管理和环境变量注入。
- 作用于整个构建过程。

### 常用的Plugins有哪些？

| 名称                     | 描述                                           |
| :----------------------- | ---------------------------------------------- |
| ComonsChunkPlugin        | 将chunks相同的模块代码提取成公共js             |
| CleanWebpackPlugin       | 清理构建目录                                   |
| ExtractTextWebpackPlugin | 将css文件从bundle文件里提取成一个独立的css文件 |
| CopyWebpackPlugin        | 将文件或者文件夹拷贝到构建的输出目录           |
| HtmlWebpackPlugin        | 创建html文件去承载输出的bundle                 |
| UglifyjsWebpackPlugin    | 压缩js                                         |
| ZipWebpackPlugin         | 将一个打包的资源生成一个zip文件                |



### Loaders 的基本用法：

```js
const path = require('path');
module.exports = {
    output: {
        filename: 'bundle.js'
    },
plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
    ]
}
```





## 4、核⼼概念之 Mode

- Mode ⽤来指定当前的构建环境是：production、development 还是 none。
- 设置 mode 可以使⽤ webpack 内置的函数，默认值为 production。

### Mode的内置函数功能

| 选项        | 描述                                                         |
| :---------- | ------------------------------------------------------------ |
| development | 设置`process.env.NODE_ENV`的值为`development`，开启`NameChunkPlugin`和`NameModulesPlugin` |
| production  | 设置`process.env.NODE_ENV`的值为`production`，开启`FlagDependenceUsagePlugin`，<br />`FlagIncludeChunksPlugin`,`ModuleConcatenationPlugin`,`NoEmitOnErrorPlugin`，<br />`OccurrenceOrderPlugin`，`SideEffectsFlagPlugin`和`TerserPlugin` |
| node        | 不开启任何                                                   |









