---
title: Vuex
date: 2018-07-19 19:38:03
tags: vue
categories: 笔记 
---

## 基本概念

`Vuex`是`Vue.js`的应用中的状态管理方案。

有四个核心概念：

  - State：状态数据，可以全局引入后调用。
  - Getter：对`state`进行过滤、处理或计算，而派生出新的状态数据。
  - Mutation： 更改`store`中的`state`唯一方法是提交`mutation`。
  - Action：类似与`mutation`，但不直接更改`state`，提交`mutation`，由它去更改`state`。原因是`mutation`不能异步更改`state`，但可通过`action`操作。

### 多文件结构

```js
// state.js
export default {
    title: 'index page',
    name: 'hello world',
    num: 0
}
```

```js
// actions.js
export default {
    increateNumAction(context, count){
        context.commit('increate',count);
    }
}
```

```js
// getters.js
export default {
    getNumGetter: (state) => {
        return "this num is: " + state.num;
    }
}
```

```js
// mutations.js
export default {
    increate(state, count=1) {
        state.num+=count;
    }
}
```

### 使用

获取`state`:

```js
// 直接获取
this.$store.state.xxx;

// 计算属性获取
export default {
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

触发`action`：

```js
// 全局调用
this.$store.dispatch('XXX');

// 定义方法
export default {
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

获取getter：

```js
// 全局调用
this.$store.getters.XXX;

// 引入调用
mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```