## webpack打包之代码压缩

### 1、JS压缩

- webpack4.0+，内置了uglifyjs-webpack-plugin
- mode=production时，默认压缩js

### 2、CSS压缩

- 使用optimize-css-assets-webpack-plugin压缩
- 使用cssnano压缩

```js
module.exports = {
    entry: {
        app: './src/app.js',
        search: './src/search.js'
    },
    output: {
        filename: '[name][chunkhash:8].js',
        path: __dirname + '/dist'
    },
    plugins:[
        new OptimizeCSSAssetsPlugin({
            assetNameRegExp: /\.css$/g,
            cssProcessor: require('cssnano')
        })
    ]
};
```

### 3、HTML压缩

- 修改html-webpack-plugin，设置压缩参数

```js
module.exports = {
    entry: {
        app: './src/app.js',
        search: './src/search.js'
    },
    output: {
        filename: '[name][chunkhash:8].js',
        path: __dirname + '/dist'
    },
    plugins:[
        new HtmlWebpackPlugin({
            template: path.join(__dirname, 'src/search.html’),
            filename: 'search.html’, + chunks: ['search’],
            inject: true,
            minify: {
            html5: true,
            collapseWhitespace: true,
            preserveLineBreaks: false,
            minifyCSS: true,
            minifyJS: true,
            removeComments: false
            } 
        })
    ]
};
```

