# Redux 与 React

要分离表现层和容器层。

表现层不是 Redux 的工作，由自己定义。

容器层用来连接 redux 与 表现层。

表现层任何与 state 关联的操作都分离出来，交由容器层处理。

# 最新理解

单一 Object Tree 的更容易将服务器的状态注入到客户端。并且开发是可以将 Object 保存在本地，加快开发速度。

reducers 是纯函数，你可以随意控制执行顺序，或传入额外的数据区分动作。

随着 APP 的增长，可以分割多个 reducer，管理 APP 不同部分。


# redux 的作用是帮助你管理状态？

https://github.com/calesce/redux-slider-monitor

这个 demo 中，拖动下方进度条 (表示状态变更)，app 的 UI 也变化了。

不明白的是跟 Reactjs 自带的 state 有什么区别？

如果只是这样的 demo，Reactjs 自身也能实现，但是需要在 render 函数中写很多判断。

那么 redux 就是为了解决这个问题的？同时还提升开发体验？

继续了解。

Redux 可以与 Reactjs 一起使用，也可以与其他库一起使用。

是一个 state 管理库？

整个 app 的状态保存在单个 store 中的 object tree 中。

唯一更改 state tree 状态的方式是触发一个 action。

object 记录发生的事情。

要指定哪些 action 转换到 state tree，你需要写纯 reducers 。

reducer 是一个纯函数 (`(state, action) => state`)，描述了 action 如何将 state 转换到下一个 state。

```javascript

/**
 * This is a reducer, a pure function with (state, action) => state signature.
 * It describes how an action transforms the state into the next state.
 *
 * The shape of the state is up to you: it can be a primitive, an array, an object,
 * or even an Immutable.js data structure. The only important part is that you should
 * not mutate the state object, but return a new object if the state changes.
 *
 * 重要的部分是你不应该更改 state object，如果 state 更改了应该返回一个新的 object
 *
 * In this example, we use a `switch` statement and strings, but you can use a helper that
 * follows a different convention (such as function maps) if it makes sense for your project.
 */

function counter(state = 0, action) {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1
  case 'DECREMENT':
    return state - 1
  default:
    return state
  }
}
// Create a Redux store holding the state of your app.
// Its API is { subscribe, dispatch, getState }.
let store = createStore(counter)

// You can subscribe to the updates manually, or use bindings to your view layer.
store.subscribe(() =>
  console.log(store.getState())
)

// The only way to mutate the internal state is to dispatch an action.
// The actions can be serialized, logged or stored and later replayed.
store.dispatch({ type: 'INCREMENT' })
// 1
store.dispatch({ type: 'INCREMENT' })
// 2
store.dispatch({ type: 'DECREMENT' })


```

作为直接修改 state 的替代，通过分配一个叫做 action 对象表示发生的事情，然后写一个特定的函数 (reducer) 决定 action 如何转换整个 app 的状态。

如果你来自 flux，你需要知道 redux 没有 Dispatcher 或多个 store。

redux 只有单个 store 和单个 root reducing function。

redux 尝试提供可预见的 state  (所有 state 可能变化的操作写在一个 function 中，并把变化保存在 state tree 中，使得错误可以重现，并且测试变得简单)。

到这里对 redux 有一个概念上的了解了。

可以使用 `combineReducers` 将多个 function 合并成一个 reducer。

reducer 会返回变化后的 state，不是直接在 reducer 中更改 state。


## February 19, 2016 14:41 继续阅读 redux 文档

### basic 部分

http://redux.js.org/docs/basics/index.html

#### Action



Action 的定义：Action 是 App 发送到 stroe 的信息的载体。他们是 store 唯一可以获取信息的来源。通过使用 `store.dispatch()` 发送信息到 store。

Action 是原生 Object 对象，内部必须包含一个 type 属性，表明这个 action 执行什么操作。

type 通常定义为 const string 类型。

如果你的 app 足够大，把他们移动到一个单独的模块

`import { ADD_TODO, REMOVE_TODO } from '../actionTypes'`。

Object 内部除了 type，其它结构取决于你.

#### reducer

We’ll explore how to perform side effects in the [advanced walkthrough](http://redux.js.org/docs/advanced/index.html).
