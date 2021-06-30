### `Syntax Error: TypeError: this.getOptions is not a function`

问题描述，安装完`less-loader`后，进行webpack打包报错

```js
Syntax Error: TypeError: this.getOptions is not a function
```

原因分析，是less-loader安装的版本太高，卸载重新安装7.0版本即可

解决方法：

1. `set package.json  "less-loader": "5.0.0"`
2. `npm install`