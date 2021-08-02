### `TypeError: Cannot read property 'tap' of undefined`

问题描述，安装完`html-webpack-plugin`后，进行webpack打包报错

```js
TypeError: Cannot read property 'tap' of undefined
at ScriptExtHtmlWebpackPlugin.compilationCallback (E:\vue-project\vue-element-admin-master\node_modules\script-ext-html-webpack-plugin\lib\plugin.js:50:57)
```

#### 解决方法

1. `set "html-webpack-plugin": "^4.0.0-alpha" => "4.0.0-alpha"`
2. `remove node_modules`
3. `remove package-lock.json`
4. `npm install`