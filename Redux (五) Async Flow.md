http://redux.js.org/docs/advanced/AsyncFlow.html

# Async Flow

如果不使用 [middleware](。)，Redux 只提供了[同步数据流](。)。这是 [createStore()](。)的默认值。

你可以使用 [applyMiddleware()](。) 增强 [createStore()](。)。这不是唯一的方式，但他能让你[便捷快速的使用异步 action](。)。

Asynchronous middleware 如 redux-thunk 或 redux-promise 都是包裹 store 的 [dispatch](。) 方法使你可以在 action creator 内 dispatch 一些其他的 action，例如 function 和 Promises。你可以将任意 middleware 的任意功能整合到 dispatch，你 dispatch 的 action 会以此被队列中的 middleware 捕获并传递到下一个 middleware。例如，Promise middleware 可以截取 Promises 并 dispatch 一对 begin/end action 异步的响应每一个 Promise。

当队列的最后一个 middleware dispatch 了一个 action，他将会是一个原生 object，这部分的内容属于 [synchronous Redux data flow](。) 。

[完整的异步例子源代码](。)。

## 下一步

现在你已经知道在 Redux 中 middleware 可以做什么事情，是时候学习他是如何工作的了，和如何创建属于你自己的 middleware。下一章节将详细讨论关于 [Middleware](。) 的实现问题。
