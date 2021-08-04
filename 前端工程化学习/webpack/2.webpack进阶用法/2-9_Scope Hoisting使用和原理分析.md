## scope  hoisting

### 1、什么是scope hoisting

​		Scope Hoisting 是 webpack3 的新功能，直译为 "**「作用域提升」**"，它可以让 webpack 打包出来的**「代码文件更小」**，**「运行更快」**。

​		在 JavaScript 中，还有“变量提升”和“函数提升”，JavaScript 会将变量和函数的声明提升到当前作用域顶部，而“作用域提升”也类似，webpack 将引入到 JS 文件“提升到”它的引入者的顶部。

对比使用scope hoisting和不使用的效果：

```js
// 源代码
// main.js
export default "hello！！";

// index.js
import str from "./main.js";
console.log(str);
```

```js
// 不使用 scope hoisting的打包
[  (function (module, __webpack_exports__, __webpack_require__) {    
  var __WEBPACK_IMPORTED_MODULE_0__main_js__ = __webpack_require__(1);    
  console.log(__WEBPACK_IMPORTED_MODULE_0__main_js__["a"]);
}),  (function (module, __webpack_exports__, __webpack_require__) {    __webpack_exports__["a"] = ('hello！！');  })]
```

```js
// 使用 scope hoisting
[
  (function (module, __webpack_exports__, __webpack_require__) {
    var main = ('hello！！');
    console.log(main);
  })
]
```



### 2、scope hoisting 原理

​		scope hoisting原理：分析出模块之间的依赖关系，尽可能将打散的模块合并到一个函数，然后适当的重命名一些变量防止变量名冲突，以达到减少函数声明的代码和内存开销。

​		scope hoisting分析模块之间的依赖，**必须采用ES6模块语句化**，否则scope hoisting无法生效。



### 3、scope hoisting 的使用方式

1. **自动启用**

   ​	webpack的mode为production模式时，scope hoisting默认开启

2. **手动启用**

   ​	非默认启用的mode下，手动启用webpack内置的scope hoisting

   ```js
   // 配置ModuleConcatenationPlugin插件
   // webpack.config.js
   const webpack = require('webpack')
   
   module.exports = {
       // ....
       plugins:[
           new webpack.optimize.ModuleConcatenationPlugin()
       ]
   }
   ```

   

   ​	由于scope hoisting只能检测ES6的语法模块，CommonJs的语法无法检测，但大多数包可能还用CommonJs，因此为了充分发挥scope hoisting的作用，可以在webpack增加一下配置：

   ```js
   // webpack.config.js
   const webpack = require('webpack')
   
   module.exports = {
       // ....
       resolve: {
         	// 针对npm中的第三方模块，优先采用jsnext:main指向es6模块语法的文件
           mianFields: ['jsnext:main','browser','main']
       },
       plugins:[
           new webpack.optimize.ModuleConcatenationPlugin()
       ]
   }
   ```

   ​	针对非es6模块化语法的代码，wenpack会降级处理不使用scope hoisting的优化，可以在package.json命令上增加参数`--display-optimization-bailout`

   ```json
   {
       "scripts": {
           "build": "webpack --display-optimization-bailout"
       }
   }
   ```

   