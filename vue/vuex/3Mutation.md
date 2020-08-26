# Mutation

> 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 **事件类型 (type)** 和 一个 **回调函数 (handler)**。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数

> vuex 中store数据改变的唯一方法是使用mutation

```javascript
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    //这个选项更像是事件注册
    //注册事件类型（type）为 increment，回调函数（handler）为第一个参数为state
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
```

> 不能直接调用一个 mutation handler
>
> 当触发一个类型为 `increment` 的 mutation 时，调用此函数

```javascript
//以相应的 type 调用 store.commit 方法，并出发 回调函数（handle）
store.commit('increment')
```

### 提交载荷（Payload）

> 你可以向 `store.commit` 传入额外的参数，即 mutation 的 **载荷（payload）**

```javascript
// ...
mutations: {
  increment (state, n) {
    state.count += n
  }
}
```

```javascript
store.commit('increment', 10)
```

> 在大多数情况下，载荷应该是一个对象，这样可以包含多个字段并且记录的 mutation 会更易读

```javascript
// ...
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

```javascript
store.commit('increment', {
  amount: 10
})
```

> 对象风格的提交方式                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

```javascript
store.commit({
  type: 'increment',
  amount: 10
})
```

> 当使用对象风格的提交方式，整个对象都作为载荷传给 mutation 函数，因此 handler 保持不变

```javascript
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

### 使用常量替代 Mutation 事件类型

```javascript
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'
```

```javascript
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

### 在组件中提交 Mutation

> 你可以在组件中使用 `this.$store.commit('xxx')` 提交 mutation，或者使用 `mapMutations` 辅助函数将组件中的 methods 映射为 `store.commit` 调用（需要在根节点注入 `store`）

```javascript
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```



























