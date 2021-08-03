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
                    'sass-loader',
                    {
                        loader: 'postcss-loader',
                        options: {
                            plugins: () => {
                                require('autoprefixer')({
                                    browers:['last 2 version','>1%','iOS 7']
                                })
                            }
                        }
                    }
                ]
            }
        ]
    }
};
```

