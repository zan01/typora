# getter 

> 从 store 中的 state 中派生出一些状态
>
> 共享的过滤数据，类似计算函数，对 `state` 中的数据进行过滤
>
> **getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算**
>
> Getter 接受 state 作为其第一个参数

```javascript
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```



1. **通过属性访问**

    > Getter 会暴露为 `store.getters` 对象，你可以以属性的形式访问这些值
    >
    > 注意，getter 在通过属性访问时是作为 Vue 的响应式系统的一部分缓存其中的

    ```javascript
    store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]
    ```

2. **Getter 也可以接受其他 getter 作为第二个参数**

    ```javascript
    getters: {
      // ...
      doneTodosCount: (state, getters) => {
        return getters.doneTodos.length
      }
    }
    ```

3. **通过方法访问**

    > 注意，getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果

    > 你也可以通过让 getter 返回一个函数，来实现给 getter 传参。在你对 store 里的数组进行查询时非常有用

    ```javascript
    getters: {
      // ...
      getTodoById: (state) => (id) => {
        return state.todos.find(todo => todo.id === id)
      }
    }
    ```

    ```javascript
    store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
    ```

4. **mapGetters 辅助函数**

    > `mapGetters` 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：

    ```javascript
    import { mapGetters } from 'vuex'
    
    export default {
      // ...
      computed: {
      // 使用对象展开运算符将 getter 混入 computed 对象中
        ...mapGetters([
          'doneTodosCount',
          'anotherGetter',
          // ...
        ])
      }
    }
    ```

    如果你想将一个 getter 属性另取一个名字，使用对象形式

    ```javascript
    ...mapGetters({
      // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
      doneCount: 'doneTodosCount'
    })
    ```

    

    