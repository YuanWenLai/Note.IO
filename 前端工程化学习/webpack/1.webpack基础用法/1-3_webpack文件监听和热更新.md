## 1、`webpack`中的文件监听 -- Watch

### 文件监听是在发现源码发剩变化时，自动重新构建输出新的文件。

`webpack` 开启的监听模式有两种方式：

- 启动`webpack`命令时，带上 `--watch`参数
- 在配置`webpack.config.js`中设置`watch:true`

### `webpack`中的文件监听使用。

1. 在`package.json`配置

   ```json
   {
       "name": "hello-webpack",
       "version": "1.0.0",
       "description": "Hello webpack",
       "main": "index.js",
       "scripts": {
           "build": "webpack ",
           "watch": "webpack --watch"
       },
       "keywords": [],
       "author": "",
       "license": "ISC"
   }
   ```

   唯⼀缺陷：每次需要⼿动刷新浏览器。

   

2. 文件监听原理分析

   轮询判断文件的最后编辑时间是否发生变化

   某个文件发生了变化，并不会立即告诉监听者，而是缓存起来，等待`aggregateTimeout`

   ```js
   module.export = {
       // 默认为false，不开启
       watch: true,
       watchOption: {
           // 默认为空，不监听的文件或文件夹，支持正则匹配
           igonred: '/node_modules/',
           // 监听到变化发生后，会等300ms再去执行，默认300ms
           aggregateTimeout：300，
           // 判断文件是否发生变化是通过不停轮询，监听指定文件的编辑时间是否变化，默认每秒：1000次/s
           poll:1000
       }
   }
   ```





## 2、`webpack-dev-server`热更新

模块热替换（HMR hot module replacement）功能会在应用运行中替换、添加和删除模块，而无需重新加载整个页面。

主要通过以下几种方式，来显著加快开发速度：

- `WDS`不刷新浏览器，不输出文件，而是放到内存中
- 保留在完全重新加载页面时对视的应用程序状态
- 只更新变更内容，以节省宝贵的开发时间
- 调整样式更快加速，几乎相当于在浏览器调试器中更改样式

1. 在`package.json`配置

   ```json
   {
       "name": "hello-webpack",
       "version": "1.0.0",
       "description": "Hello webpack",
       "main": "index.js",
       "scripts": {
           "build": "webpack ",
           "dev": "webpack-dev-server --open"
       },
       "keywords": [],
       "author": "",
       "license": "ISC"
   }
   ```

   

   

   ### 简单理解热更新原理

   1. webpack Compile将Js编译成Bundle
   2. HMR Server:将热更新的文件输出给HMR Rumtime
   3. Bundle server：提供文件在浏览器访问
   4. HMR server会被注入到浏览器，更新文件的变化
   5. bundle.js 构建输出的文件

