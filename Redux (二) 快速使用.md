layout: [post]
title: Redux (二) 快速使用
date: 2016-04-17 01:02:08
tags:
- 标签
categories:
- 分类
- 子分类
---

介绍如何快速上手 Redux。

<!-- more -->


---

# Redux 快速使用

上一篇文章用简单的文字介绍了 Action,Reducer，Store。

现在配合代码详细介绍。

## Action

Action 是原生的 JavaScript Object 类型，内部必须包含一个 type 属性，表明这个 Action 执行什么操作。

```javascript

// action.js
export const ADD_MSG = 'ADD_MSG';

// action creators
export function addMsg(text,index){
    return {
        type:ADD_MSG,
        text,
        index,
    }
}

```

这里使用函数 `addMsg` 生成一个 Action，这样做的好处是可以动态修改 Action 的值。

这个 Action 中有一个固定的属性 `type`，表明需要添加消息。

剩下的属性可以自由定义，Reducer 会根据这些信息执行操作。

 `text,index` 是 ES 6 的写法，等同于` {text:text,index:index}`。

## Reducer

Reducer 是纯函数，如  `(state, Action) => state`，通过  Action 将当前 State 转为下一个 State。

一个应用程序只有一个根 Reducer。

Reducer 执行完成后返回下一个 State，绝不允许直接改变当前 State。

大型程序的不同模块想让不同函数 (Reducer) 处理，只能通过属性分隔。

使用 'createStore' 创建一个与 reducer 绑定的 Store，每次调用 Dispatch(Action)  都传递参数给 Reducer 并执行。

Reducer 第一个参数是当前应用程序的 State，第二个参数是 Action 对象。

下面的 State 由内容模块和历史纪录模块组成，分别由 'content' 和 'history' 函数生成。

```javascript

// reducer/index.js
import content from './content';
import history from './history';

export default function todoApp(state = 'INIT', action) {
    return {
        content: content(state.content, action),
        history:history(state,action)
    }
}

// reducer/content.js
import {
    ADD_MSG,MOVE_TO_HISTORY
} from '../action';

export default function content(state = [], action) {
    switch (action.type) {
        case ADD_MSG:
            return [
              ...state,
              {
                  index: action.index + 1,
                  text: action.text
              }
            ]
            case MOVE_TO_HISTORY:

            return [{text:''}];
        default:
            return state;
    }
}


// store/index
import rootReducer from '../reducer';
const store = createStore(rootReducer,initialState);



```

Reducer 如果不执行必须返回当前 State。

```javascript
import {
    ADD_MSG
} from './action';

export default function inputBoard(state = [], action) {
    switch (action.type) {
        case ADD_MSG:
        return [
          ...state,
          {
              index: action.index + 1,
              text: action.text
          }
        ]
        default:
            return state;
    }
}

```

### combineReducers

Redux 提供了一个快速合并 Reducer 的函数 'combineReducers'

```javascript
export default function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
// 等价于
export default const todoApp = combineReducers({
  visibilityFilter,
  todos
})

// 也可以指定不同的 Key

const reducer = combineReducers({
  a: doSomethingWithA,
  b: processB,
  c: c
})

// 等价于

function reducer(state = {}, action) {
  return {
    a: doSomethingWithA(state.a, action),
    b: processB(state.b, action),
    c: c(state.c, action)
  }
}

```

### ES 6 语法

使用 ES 6 可以更近一步简化程序，因为 combineReducers 需要的是一个对象，可以使用 ES 6 的 ' * ' 导入所有内容到一个对象中。

```javascript
import { combineReducers } from 'redux'
import * as reducers from './reducers'

const todoApp = combineReducers(reducers)
```

## Store

Store 是连接 Action 和 Reducer 的桥梁。

他的职责有：

- 保存应用程序状态
- 允许通过 getState() 获取状态
- 运行通过 dispatch(action) 更新状态
- 通过 subscribe(listener) 主持监听方法
- 通过 subscribe(listener) 方法返回的监听器，清除监听方法。

注意整个应用程序只有一个 Store，如果不同的数据相分别处理，请使用 [Reducer 组合](http://redux.js.org/docs/basics/Reducers.html#splitting-reducers) 的方式代替创建多个 Store。

### 创建 Store

上面的章节中我们已经使用 `combineReducers()` 将多个 Reducer 合并成一个并且导出，现在我们使用这个 Reducer 创建 Store。
createStore 第二个参数可以传入 State 初始值。

```javascript
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp)
```

创建完成 Store 之后，我们就可以在任意位置使用 `getState`，`subscribe` 和 `dispatch` 了

```javascript
import { addTodo, completeTodo, setVisibilityFilter, VisibilityFilters } from './actions'

// Log the initial state
console.log(store.getState())

// Every time the state changes, log it
// Note that subscribe() returns a function for unregistering the listener
let unsubscribe = store.subscribe(() =>
  console.log(store.getState())
)

// Dispatch some actions
store.dispatch(addTodo('Learn about actions'))
store.dispatch(addTodo('Learn about reducers'))
store.dispatch(addTodo('Learn about store'))
store.dispatch(completeTodo(0))
store.dispatch(completeTodo(1))
store.dispatch(setVisibilityFilter(VisibilityFilters.SHOW_COMPLETED))

// Stop listening to state updates
unsubscribe()
```

## 数据流

Redux 程序遵循严格的单向数据流。

这意味着应用程序内所有数据都拥有相同的生命周期模式，这样你的应用程序更加易懂和可预测，也确保了数据的标准化，你不再需要拷贝多个相同的数据彼此单独处理了。

如果你仍不放心，阅读 [Motivation](http://redux.js.org/docs/introduction/Motivation.html) 和 [The Case for Flux](https://medium.com/@dan_abramov/the-case-for-flux-379b7d1982c6) 了解关于单向数据流完整的讨论。尽管 Redux 不完全于 Flux 一样，但他有相同的好处。

Redux 中数据的生命周期有四步:

1. 调用 `store.dispatch(action)`。

你可以在应用程序的任意位置调用 `dispatch`，包括组件内和 XHR 回调方法，甚至在定时器内。

2. Redux Store 调用你传入 Reducer 方法。

Store 会传递两个参数给 Reducer:当前 State 和 Action。

注意 Reducer 是纯函数，他只用来计算下一个 State，他应该是完全可预测的，输入过的内容要在任意时候都能确保相同。他不应该执行任何有副作用的 API 例如 Router 转换，这些应该发生于 Action 被 Dispatch 之前。

3. 根 Reducer 可以合并多个 Reducer 的输出到单个 State 树。

你的根 Reducer 的结构完全取决于你，Redux 提供了 [combineReducers()](http://redux.js.org/docs/api/combineReducers.html) 辅助函数将多个处理 State 树分支的 Reducer 组合成一个 Reducer。

当你触发 Action 时，由 `combineReducers()` 返回的 Reducer 将会调用所有已组合的 Reducer，这些 Reducer 返回的结果会组合成一个单独的 State 树。

4. Redux Store 更新由根 Reducer 返回的新的 State。

现在新的树是应用程序的下一个 State！每个 `store.subscribe(listener)` 返回的监听器都会被调用；在监听器内能调用 store.getState() 获取当前 State。

然后 UI 会根据新的 state 而被更新。如果你使用 React Redux，这等同于 React 中的 `component.setState(newState)` 被调用。


## 下一步

现在你已经了解 Redux 的基础用法了，接下来我们准备配合 React 使用。

> 更高级的使用者：如果你已经熟悉基础概念并完成了这个指南，不要忘记去[高级指南](http://redux.js.org/docs/advanced/index.html) 的 [async flow](http://redux.js.org/docs/advanced/AsyncFlow.html) 学习当中间件在 [async action](http://redux.js.org/docs/advanced/AsyncActions.html) 到达 reducer 之前是如何转换的。
