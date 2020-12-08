## vue2.x 自定义事件 .sync

#### 1.父子组件通信错误警告

```javascript
Avoid mutating a prop directly since the value will be overwritten whenever the parent component re-renders. Instead, use a data or computed property based on the prop's value. 
```

报错原因：

```
所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。
```



##### 解决方法：

父组件调用子组件弹窗：

```javascript
// 子组件弹窗
<check-num-dialog 
:visible.sync="dialogVisible"
:num-list="numData"
/>
```



子组件获取父组件下发的数据：

```javascript
// 子组件通过props获得的数据用监听属性监听，发生改变赋值给子组件本身的data.visibleFlag
export default {
    props:{
        visible:{
            type: Boolean,
            default: false
        }
    }，
    data() {
        return {
            visibleFlag: this.visible
        }
    },
    watch: {
        visible:function (newVal, oldval) {
            this.visibleFlag = newVal
        }
    },
    // 若子组件需要关闭弹窗，则会触发数据状态改变，子组件数据改变，父组件没有同步改变，或出现上述警告。
    // 因此需要.sync 修饰符对prop进行双向绑定
    close() {
        this.visibleFlag = false
        this.$emit('update:visible',false)
     },
}
```



---

### 总结：

1. 父组件下发数据给子组件时，子组件最好别直接使用`props`传来的数据，为了更好的维护，需要监听属性辅助，数据变化时，将父组件变化的数据赋值给子组件本身的`data`数据，在子组件进行引用。
2. 子组件更新了公共数据时，需要向父组件发出更新，不然数据不一致。.sync 修饰符能很好的帮助我们对这两个组件进行“双向数据绑定”，避免`vue`发出警告。

