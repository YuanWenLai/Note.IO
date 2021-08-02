## webpack打包的文件指纹.

### 1、什么是文件指纹

webpack 打包文件的前缀或后缀



### 2、文件指纹如何生成

- `Hash`：和整个项目的构建相关，只要项目文件有修改，整个项目构建的hash值就会更改
- `Chunkhash`：和webpack打包的chunk相关，不同的entry会生成不同的chunkhash值
- `Contenthash`： 根据文件内容来定义hash，文件内容不变，则contenthash不变



### 3、JS的文件指纹设置

设置output的filename，使用[chunkhash]

```js
module.exports = {
    entry: {
        app: './src/app.js',
        search: './src/search.js'
    },
    output: {
        filename: '[name][chunkhash:8].js',
        path: __dirname + '/dist'
    }
};
```



### 4、CSS的文件指纹设置

设置 MiniCssExtractPlugin 的 filename，使⽤ [contenthash]

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
    plugins: [
        new MiniCssExtractPlugin({ 
        	filename: `[name][contenthash:8].css`
        })
    ]
};
```





### 5、图片的文件指纹设置

设置 file-loader 的 name，使⽤ [hash]

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
    module: {
        rules: [
            {
            test: /\.(png|svg|jpg|gif)$/,
            use: [{
            	loader: 'file-loader’,
                 options: {
                    name: 'img/[name][hash:8].[ext] '
                 } 
             	}
             ] 
            }
        ]
    }
};
```

