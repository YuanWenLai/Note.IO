# es6 模块export与export default的区别

###  1.export命令用于规定模块的对外接口

一个模块就是一个独立文件。该文件内部的变量、方法和类对象，外部无法获取。若想获取，必须使用`export`

```javascript
// example.js
export var myName = 'cavin'
export var nbaStart = 'LBJ'
export function run(){ return 'go'}
```

es6将example.js文件视为一个模块，`export`对外部输出了能访问的变量。

`export`的另外一种写法：

```javascript
// example.js
var myName = 'cavin'
var nbaStart = 'LBJ'
function run(){ return 'go'}
export {
	myName,
    nbaStart,
    run
}
```

通常情况下，`export`导出的变量也可以更名，使用`as`关键字重命名。

```javascript
// example.js
var myName = 'cavin'
var nbaStart = 'LBJ'
function run(){ return 'go'}
export {
	myName as myFullName,
    nbaStart as superStart,
    run as toRun
}
```

导入的时候，使用`import`加载这个模块。

```javascript
import {myFullName, superStart, toRun} from 'example.js'
```



***

###  2.export default命令，为模块指定默认输出

使用`import`命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。但是，用户肯定希望快速上手，未必愿意阅读文档，去了解模块有哪些属性和方法。

为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到`export default`命令，为模块指定默认输出。

```javascript
// example2.js
export default function () {
    ....
}
```



---

### 3.export与export default的使用区别

1. 使用expoet，import命令接受一对大括号，里面需要指定导入模块的变量名，导入时也可以用关键字as更改变量名。

```javascript
import { myFullName as useName } from 'example.js'
```

2. 与export命令区别，导入export default的模块，不需要大括号，import命令可以指定任意名字。

```javascript
import useExample from 'example2.js'
```



---



## 总结：

1. export命令对外接口是有名称且import导入接口的名字需要一致，还需要大括号，而export default导出的，不需要一致名字和大括号。
2. export default命令指定模块输出，因此一个模块只有一个输出，唯一对应，所以不需要大括号。

---

