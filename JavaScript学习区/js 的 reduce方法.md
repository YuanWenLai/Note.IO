## js 的 reduce方法

### 1. reduce介绍

ruduce语法：

```javascript
reduce() 语法：arr.reduce(callback,[initialValue])

callback:函数中包含四个参数
- previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
- currentValue （数组中当前被处理的元素）
- index （当前元素在数组中的索引)
- array （调用的数组）
 
initialValue （作为第一次调用 callback 的第一个参数。）
```



例子：

```javascript
const arr = [1, 2, 3, 4, 5]
const sum = arr.reduce((pre, item) => {
    return pre + item
}, 0)
console.log(sum) // 15
```



应用：利用reduce来计算一个字符串中每个字母出现次数

```javascript
const str = 'jshdjsihh';
     const obj = str.split('').reduce((pre,item) => {
         pre[item] ? pre[item] ++ : pre[item] = 1
         return pre
     },{})
console.log(obj) // {j: 2, s: 2, h: 3, d: 1, i: 1}
```

