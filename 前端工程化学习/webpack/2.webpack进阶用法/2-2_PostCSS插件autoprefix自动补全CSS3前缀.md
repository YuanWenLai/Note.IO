## `webpack`自动补全`CSS3`前缀

​		浏览器最核心的部分--`rendering engine`,渲染引擎。不同的浏览器内核，对网页的编写语法的解析也不同，导致前端工程师需要为不同浏览器增加`css3`前缀，减少不同浏览器渲染的差异性。

### 1、`css3`的属性为什么需要前缀

​		浏览器最核心的部分--`rendering engine`,渲染引擎。不同的浏览器内核，对网页的编写语法的解析也不同，导致前端工程师需要为不同浏览器增加`css3`前缀，减少不同浏览器渲染的差异性。

```css
.box {
    -moz-border-radius: 10px;
    -webkit-border-radius: 10px;
    -o-border-radius: 10px;
    border-radius: 10px;
}
```



### 2、浏览器的内核简介

| 浏览器内核 | `css3`前缀 | 主流的浏览器      |
| ---------- | ---------- | ----------------- |
| `Trident`  | `-ms`      | `IE`              |
| `Geko`     | `-moz`     | `FireFox`         |
| `Webkit`   | `-webkit`  | `chrome`,`safari` |
| `Presto`   | `-o`       | `Opera`           |



### 3、`PostCss`插件`autoprefixer`自动补齐`CSS3`前缀

- 依据`can i user`规则

```js
// webpack.config.js

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
                test: /\.scss$/,
                use: [
                    'style-loader',
                    'css-loader',
                    'postcss-loader'，
                    'sass-loader',
                ]
            }
        ]
    }
};

// 在根目录下建postcss.config.js
module.exports = {
    plugins: [
        // postcss插件
        require('autoprefixer')
    ]
}
```



- 在根目录的`package.json`下添加`postcss`的配置项`browserslist`

```json
{
  "name": "halo-webpack4.0",
  "main": "index.js",
  "scripts": {
    "dev": "webpack-dev-server --config build/webpack.config.js --open",
    "build-pro": "webpack --config ./build/webpack.prod.js --mode=production",
    "build-dev": "webpack --config ./build/webpack.dev.js --mode=development"
  },
  "author": "yuanwenlai",
  "browserslist": [
    "> 1%",
    "last 100 versions",
    "not ie <= 8"
  ]
}

```



### 4、`PostCss`插件`autoprefixer`构建测试验证

1. 建测试文件`index.css`，打包后查看打包的`css`文件是否增加前缀

```css
// index.css
.container {
    height: 100vh;
    border-radius: 30px;
    box-sizing:border-box;
    background: rgb(158, 235, 224);
    font-size: 56px;
}
```

```css
// index3ec78ca401afbe76f09b.css
.container{
    background:#9eebe0;
    -webkit-border-radius:.4rem;
    -moz-border-radius:.4rem;
    border-radius:.4rem;
    -webkit-box-sizing:border-box;
    -moz-box-sizing:border-box;
    box-sizing:border-box;
    font-size:.74666667rem;
    height:100vh
}
```

构建测试结果：`postcss`构建`css`前缀成功！