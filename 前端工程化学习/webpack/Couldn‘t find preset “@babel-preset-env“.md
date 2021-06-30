### `TypeError: Cannot read property 'tap' of undefined`

问题描述，`npm install babel-preset-env --save-dev`后，进行webpack打包报错

```js
Error: Couldn‘t find preset “@babel/preset-env“ relative to directory....
```

解决方法：使用babel-preset-es2015来转化

1. `npm install babel-preset-es2015`

```js
// 处理babel，es7
{
        test: /\.js$/,
        use: {
            loader: 'babel-loader',
                options: {
                    // presets: ['@babel/preset-env']
                    presets: ['es2015']
                }
        },
         exclude: /node_modules/
}
```

