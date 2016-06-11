http://redux.js.org/docs/advanced/Middleware.html

# Middleware

你已经在 [Async Action](。) 的例子对 middleware 有了一些了解。如果你使用过服务端的库如 [Express](。) 和 [Koa](。)，你应该已经对 middleware 非常熟悉。在这些框架中，middleware 是一些代码使你可以在框架接受到请求之前和生成响应请求这段时间做一些事情。例如，Express 或 Koa middleware 可以添加 CORS headers，logging，compression，和更多。middleware 最有用的功能是多个 middleware 能以队列的方式组合。你可以使用多个独立的第三方 middleware 在单独的项目中。

Redux middleware 解决与 Express 或 Koa 不同的问题，但概念是相似的。他提供第三方拓展 dispatch 的 action 到达 reducer 之间的处理。人们使用 Redux middleware 可以输出日至，异常捕获，编写异步 API，路由功能和其他更多。

这篇文章首先带你深入理解 middleware 的概念，然后在结尾给出一些非常实用的例子展示 middleware 的强大功能。你可以来回切换这两部分内容，当你感到困惑时。

## 认识 Middleware

middleware 可以用来做各种各样的事情，包括异步 API 调用，弄清楚他时如何演变而来是非常重要的事情。我会指引你走过 middleware 重构路程，以日至输出和异常捕获 middleware 为例子。

### 日志问题

Redux 的一个好处是 state 的更改是可预测的和透明的。每当 action 被 dispatch，新的 state 会被计算出来并保存。state 不能被自己更改，只能被特定的 action 经过 reducer 更改。

一个不友好的地方如果我想为每个 action 输出日志，同时输出 state 计算之后的值？和有时出现异常，我想在这之前输出日志，并察看是哪一个 action 引发的。

![](/images/2016/06/1-1.png)

在 redux 要用什么途径实现？

### 尝试 #1：手动输出日志

最原始的解决方案是在每个 dispatch 的调用位置前后手动输出日志，这不是真实的解决方案，但这是处理问题的第一步。

> 注意
> 如果你使用 react-redux 或类似的绑定方式，你可能不会直接在组件访问 store 实例。在下一个小章节，请假设已经向下传递 store。

例如，你使用这段代码创建 todo 项：

`store.dispatch(addTodo('Use Redux'))`

输出 action 和 state，你可以用这种方式：

```javascript
let action = addTodo('Use Redux')

console.log('dispatching', action)
store.dispatch(action)
console.log('next state', store.getState())
```

他达到了期望的效果，但你不会想每次需要都写一遍重复的代码的。

### 尝试 #2：包装 Dispatch

你可以用一个函数包装这段代码：

```javascript
function dispatchAndLog(store, action) {
  console.log('dispatching', action)
  store.dispatch(action)
  console.log('next state', store.getState())
}
```

你可以代替每个调用 `store.dispatch()` 的地方：

```javascript
dispatchAndLog(store, addTodo('Use Redux'))
```

我们本可在这里停下来，但每次导入新的特定 function 时不是非常便利。

### 尝试 #3：Monkeypatching Dispatch

如果我们替换 store 实例内的 dispatch function 会怎么样？Redux store 是原生的 object 带有[少量方法](。)，而我们写的是 JavaScript，因此我们可以 monkeypatch `dispatch` 的实现：

```javascript
let next = store.dispatch
store.dispatch = function dispatchAndLog(action) {
  console.log('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  return result
}
```

这里已经非常接近我们想要的！当我们 dispatch action 时，他可以保证日志正确的输出。Monkeypatching 的方式感觉上不是很正确，但我们现在可以享受一会。

### 问题：异常捕获

如果我们想在 dispatch 应用不仅一种处理怎么办？

一种不同但有用的处理是在生产环境捕获 JavaScript 抛出的异常。全局的 `window.onerror` 事件不是可靠的因为他不提供旧浏览器的堆栈信息，这无法让人知道错误为什么发生。

如果他用处不大，任何时候 dispatch action 导致的错误，我们可以发送堆栈追踪到异常捕获服务例如 [Sentry](。) ，导致错误的 action，和当前 state？这种方式更容器报告错误给开发者。

无论如何，保存日志输出和异常报告分离是很重要的。理想情况下我们想他们分别位于不同模块，甚至在不同的 packages。除此之外我们无法拥有一个健壮的生态系统。(暗示：我们将慢慢知道什么是 middleware！)

 如果日志输出和异常报告彼此分离，他们可能像这样的：

 ```javascript
function patchStoreToAddLogging(store) {
  let next = store.dispatch
  store.dispatch = function dispatchAndLog(action) {
    console.log('dispatching', action)
    let result = next(action)
    console.log('next state', store.getState())
    return result
  }
}

function patchStoreToAddCrashReporting(store) {
  let next = store.dispatch
  store.dispatch = function dispatchAndReportErrors(action) {
    try {
      return next(action)
    } catch (err) {
      console.error('Caught an exception!', err)
      Raven.captureException(err, {
        extra: {
          action,
          state: store.getState()
        }
      })
      throw err
    }
  }
}
```

如果这些 function 被发布为单独的 module，我们可以使用他们给 store 打补丁：

```javascript
patchStoreToAddLogging(store)
patchStoreToAddCrashReporting(store)
```

现在，还是不很优雅。

### 尝试 #4:隐藏 Monkeypatching

Monkeypatching 是 hack 的行为。“替换任何你喜欢的方法”，这是什么类型的 API？让我们来看看他的本质。前面我们的 function 替换了 `store.dispatch`。如果我们返回一个新的 dispatch function 会怎么样？

```javascript
function logger(store) {
  let next = store.dispatch

  // Previously:
  // store.dispatch = function dispatchAndLog(action) {

  return function dispatchAndLog(action) {
    console.log('dispatching', action)
    let result = next(action)
    console.log('next state', store.getState())
    return result
  }
}
```

我们可以在 Redux 内部提供一个辅助方法使我们可以应用 monkeypatching，实现细节如下：

```javascript
function applyMiddlewareByMonkeypatching(store, middlewares) {
  middlewares = middlewares.slice()
  middlewares.reverse()

  // Transform dispatch function with each middleware.
  middlewares.forEach(middleware =>
    store.dispatch = middleware(store)
  )
}
```

我们可以使用他应用多个 middleware 如：

```javascript
applyMiddlewareByMonkeypatching(store, [ logger, crashReporter ])
```

但这样还是 monkeypatching。

事实上我们将他隐藏到了库中并不能改变这个事实。

### 尝试 #5:移除 Monkeypatching。

为什么我们还要覆盖 `dispatch`？当然，可以在稍后调用他，但也有另一个原因：每个 middleware 可以访问 (和调用) 前一个包裹的 `store.dispatch`:

```javascript
function logger(store) {
  // Must point to the function returned by the previous middleware:
  let next = store.dispatch

  return function dispatchAndLog(action) {
    console.log('dispatching', action)
    let result = next(action)
    console.log('next state', store.getState())
    return result
  }
}
```

这是最简单的 middleware 队列！

如果 `applyMiddlewareByMonkeypatching` 处理了第一个 middleware 后不直接绑定 `store.dispatch`，`store.dispatch` 将会保持对原始 `dispatch` function 的指向。然后第二个 middleware 也会绑定原始的 dispatch function。

但这里有不同的方式启用队列。middleware 可以接收 `next()` 做为 dispatch function 替代从 store 实例读取。

```javascript
function logger(store) {
  return function wrapDispatchToAddLogging(next) {
    return function dispatchAndLog(action) {
      console.log('dispatching', action)
      let result = next(action)
      console.log('next state', store.getState())
      return result
    }
  }
}
```

现在是 “我们要好好学习” 的时间，因此可能需要一段时间才能理解。function 的级连有些吓人。ES 6 的箭头 function 可以使他更直观：

```javascript
const logger = store => next => action => {
  console.log('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  return result
}

const crashReporter = store => next => action => {
  try {
    return next(action)
  } catch (err) {
    console.error('Caught an exception!', err)
    Raven.captureException(err, {
      extra: {
        action,
        state: store.getState()
      }
    })
    throw err
  }
}
```

**Redux middleware 就是这样实现的。**

现在 middleware 使用 `next()` dispatch function，并返回一个 dispatch function，反过来又充当下一个 middleware 的 `next()`，等等执行下去。这对访问一些 store 方法很有用例如 `getState()`,因此 `store` 做为顶层参数始终可用。


### 尝试 #6：原生方式应用 Middleware

我们可以使用 `applyMiddleware()` 替代 `applyMiddlewareByMonkeypatching()`，他完全包裹了 `dispatch()` function，并返回所使用的 store 的副本：

```javascript
// Warning: Naïve implementation!
// That's *not* Redux API.

function applyMiddleware(store, middlewares) {
  middlewares = middlewares.slice()
  middlewares.reverse()

  let dispatch = store.dispatch
  middlewares.forEach(middleware =>
    dispatch = middleware(store)(dispatch)
  )

  return Object.assign({}, store, { dispatch })
}
```
`applyMiddleware ()` 的实现与 Redux 的非常相似，但有三处重要的方面不一样：

    - 他只暴露 [store API](。) 的子集给 middleware ：`dispatch(action)` 和 `getState()`。
    - 他有点言行不一例如你在 middleware 使用了 `store.dispatch(action)` 替代了 `next(action)`，action 将会再次遍历整个 middleware 队列,包括当前 middleware。这对 asynchronous middleware 非常有用，例如我们[之前的文章所讨论](。)。
    - 要确保你只应用 middleware 一次，他会运行在 `createStore()` 而不是在 store 自身。用 `(...middlewares) => (createStore) => createStore` 替代 `(store, middlewares) => store`

因此在 `createStore()` 之前使用他太笨重，createStore 接收最后一个参数接收他的值。

### 最终实现

我们写好的 middleware：

```javascript
const logger = store => next => action => {
  console.log('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  return result
}

const crashReporter = store => next => action => {
  try {
    return next(action)
  } catch (err) {
    console.error('Caught an exception!', err)
    Raven.captureException(err, {
      extra: {
        action,
        state: store.getState()
      }
    })
    throw err
  }
}
```

如何应用他们到 Redux store：

```javascript
import { createStore, combineReducers, applyMiddleware } from 'redux'

let todoApp = combineReducers(reducers)
let store = createStore(
  todoApp,
  // applyMiddleware() tells createStore() how to handle middleware
  applyMiddleware(logger, crashReporter)
)
```

就是这样！现在任何 dispatch 的 action 到 store 实例都会经过 `logger` 和 `crashReporter`:

```javascript
// Will flow through both logger and crashReporter middleware!
store.dispatch(addTodo('Use Redux'))
```


## 七个例子

如果你对上面的章节感到混乱，想知道还有哪些类似的写法。这个章节为你和我解决这个问题，帮助你快速解开困惑。

下面每一个都是有效的 Redux middleware。他们不是都很有用，但至少它们读起来很愉快。

```javascript
/**
 * Logs all actions and states after they are dispatched.
 */
const logger = store => next => action => {
  console.group(action.type)
  console.info('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  console.groupEnd(action.type)
  return result
}

/**
 * Sends crash reports as state is updated and listeners are notified.
 */
const crashReporter = store => next => action => {
  try {
    return next(action)
  } catch (err) {
    console.error('Caught an exception!', err)
    Raven.captureException(err, {
      extra: {
        action,
        state: store.getState()
      }
    })
    throw err
  }
}

/**
 * Schedules actions with { meta: { delay: N } } to be delayed by N milliseconds.
 * Makes `dispatch` return a function to cancel the timeout in this case.
 */
const timeoutScheduler = store => next => action => {
  if (!action.meta || !action.meta.delay) {
    return next(action)
  }

  let timeoutId = setTimeout(
    () => next(action),
    action.meta.delay
  )

  return function cancel() {
    clearTimeout(timeoutId)
  }
}

/**
 * Schedules actions with { meta: { raf: true } } to be dispatched inside a rAF loop
 * frame.  Makes `dispatch` return a function to remove the action from the queue in
 * this case.
 */
const rafScheduler = store => next => {
  let queuedActions = []
  let frame = null

  function loop() {
    frame = null
    try {
      if (queuedActions.length) {
        next(queuedActions.shift())
      }
    } finally {
      maybeRaf()
    }
  }

  function maybeRaf() {
    if (queuedActions.length && !frame) {
      frame = requestAnimationFrame(loop)
    }
  }

  return action => {
    if (!action.meta || !action.meta.raf) {
      return next(action)
    }

    queuedActions.push(action)
    maybeRaf()

    return function cancel() {
      queuedActions = queuedActions.filter(a => a !== action)
    }
  }
}

/**
 * Lets you dispatch promises in addition to actions.
 * If the promise is resolved, its result will be dispatched as an action.
 * The promise is returned from `dispatch` so the caller may handle rejection.
 */
const vanillaPromise = store => next => action => {
  if (typeof action.then !== 'function') {
    return next(action)
  }

  return Promise.resolve(action).then(store.dispatch)
}

/**
 * Lets you dispatch special actions with a { promise } field.
 *
 * This middleware will turn them into a single action at the beginning,
 * and a single success (or failure) action when the `promise` resolves.
 *
 * For convenience, `dispatch` will return the promise so the caller can wait.
 */
const readyStatePromise = store => next => action => {
  if (!action.promise) {
    return next(action)
  }

  function makeAction(ready, data) {
    let newAction = Object.assign({}, action, { ready }, data)
    delete newAction.promise
    return newAction
  }

  next(makeAction(false))
  return action.promise.then(
    result => next(makeAction(true, { result })),
    error => next(makeAction(true, { error }))
  )
}

/**
 * Lets you dispatch a function instead of an action.
 * This function will receive `dispatch` and `getState` as arguments.
 *
 * Useful for early exits (conditions over `getState()`), as well
 * as for async control flow (it can `dispatch()` something else).
 *
 * `dispatch` will return the return value of the dispatched function.
 */
const thunk = store => next => action =>
  typeof action === 'function' ?
    action(store.dispatch, store.getState) :
    next(action)


// You can use all of them! (It doesn’t mean you should.)
let todoApp = combineReducers(reducers)
let store = createStore(
  todoApp,
  applyMiddleware(
    rafScheduler,
    timeoutScheduler,
    thunk,
    vanillaPromise,
    readyStatePromise,
    logger,
    crashReporter
  )
)
```
