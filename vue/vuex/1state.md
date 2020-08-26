# state

1. **vuex state 在计算函数中的使用方式**

    ```javascript
    export default {
      // ...
      computed: mapState({
        // 箭头函数可使代码更简练
        count: state => state.count,
    
        // 传字符串参数 'count' 等同于 `state => state.count`
        countAlias: 'count',
    
        // 为了能够使用 `this` 获取局部状态，必须使用常规函数
        countPlusLocalState (state) {
          return state.count + this.localCount
        }
      })
    }
    ```

    

2. **mapState 工具辅助函数的使用**

    > //当映射的计算属性的名称与 state 的子节点名称相同时，我们也可以给 mapState 传一个字符串数组。
    >
    > // 映射 this.count 为 store.state.count
    >
    > //mapState 函数返回一个对象

    ```javascript
    // computed: mapState(['count']),
    computed: {
        count() {
            return this.$store.state.count;
        },
    }
    ```

    

3. **展开运算符**

    > 计算函数中使用展开运算符展开mapState 函数返回的对象进入计算函数中进行对象合并

    ```javascript
    computed: {
        localComputed() { /* ... */ },
        // 使用对象展开运算符将此对象混入到外部对象中
        ...mapState({
            // ...
        })
    }
    ```

    