## Tree shaking

### 1、什么是Tree shaking

Tree shaking 是一个通常用于描述移除Javascript上下文的未引用代码（dead-code）的行为术语。

它依赖于Es6的import和export语句，用来检测代码模块是否被导出、导入且被Javascript文件使用。

see more: https://developer.mozilla.org/zh-CN/docs/Glossary/Tree_shaking 



### 2、webpack使用Tree shaking

:fallen_leaf:概念：

​		1个模块可能有多个方法，只要其中某个方法用到了，整个文件都会被打包到bundle里面。

​		Tree shaking就是在打包的时候，检测没用用到的代码或模块文件，将它们擦除

使用：

​		webpack是默认使用的，在mode:production时，默认开启Tree shaking。

​		也可以在.babelrc中设置modules: ​f​al​s​e。



### 3、Tree shaking识别的DCE(dead code elimination)

1. 代码不会被执行，不可到达
2. 代码执行的结果不会被用到
3. 代码只会影响死变量（只读不写）

例如：

```js
// 死代码	
var demo = 'test'

if(false) {
    console.log('永远不会执行的死代码')
}
```



### 4、Tree shaking的原理

利用ES6模块的特点：

- 只能作为模块顶层的语句出现
- import的模块名只能是字符串常量
- import binding是 immutable的

利用代码擦除插件：

- uglify阶段，删除无用的代码