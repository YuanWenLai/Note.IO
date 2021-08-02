### webpack配置webpack-dev-server 报错问题

问题描述，每次修改代码，需要自动编译和运行，需要用到webpack-dev-server，自动打包运行

```js
// 安装loader
npm install -D webpack-dev-server

// webpack配置文件
devServer: {
    port: 3000,
    hot: true, // 热更新
    contentBase: '../dist'
}

// package.jsom中，配置scripts启动命令
"scripts": {
    "dev": "webpack-dev-server --config build/webpack.config.js --open",
 }
    
 // 执行开发环境的启动
 npm run dev
```

报错问题：Error: Cannot find module 'webpack-cli/bin/config-yargs'

问题分析：`webpack-cli`的新版本对`webpack-dev-server`版本的不兼容

解决方法：

1. `set package.json  "webpack-cli": "3.3.12"`
2. `npm install`