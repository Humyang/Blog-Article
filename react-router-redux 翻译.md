layout: [post]
title: react-router-redux 翻译
date: 2016-07-23 12:22:54
tags:
- 前端
categories:
- 前端
- redux
- router
- react
---

文章简介

<!-- more -->


---

[原文地址](https://github.com/reactjs/react-router-redux)

# react-router-redux

You're a smart person. You use [Redux](https://github.com/rackt/redux) to manage your application state. You use [React Router](https://github.com/reactjs/react-router) to do routing. All is good.

你很智慧。你使用 Redux 管理你的应用程序状态。你也使用 React Router 处理路由操作。都值得称赞。

But the two libraries don't coordinate. You want to do time travel with your application state, but React Router doesn't navigate between pages when you replay actions. It controls an important part of application state: the URL.

但这两个库并不协调，比如你想应用程序的 state 实现时间旅行，但当你重放 action 时 React Router 不会切换两个页面。他控制着应用程序状态重要的一部分：URL。

This library helps you keep that bit of state in sync with your Redux store. We keep a copy of the current location hidden in state. When you rewind your application state with a tool like [Redux DevTools](https://github.com/gaearon/redux-devtools), that state change is propagated to React Router so it can adjust the component tree accordingly. You can jump around in state, rewinding, replaying, and resetting as much as you'd like, and this library will ensure the two stay in sync at all times.

这个库帮助你使这部分的状态保持与 Redux store 同步。我们会将当前位置信息的一份副本隐藏在 Redux 状态树。当你使用如 Redux DevTools 之类的工具重现应用程序状态时，状态的变更会发送给 React Router 因此可以相应的调整组件树。你可以跳转，重置，重放，这个库会确保任何时候他们两个库都能同步。


**This library is not necessary for using Redux together with React Router. You can use the two together just fine without any additional libraries. It is useful if you care about recording, persisting, and replaying user actions, using time travel. If you don't care about these features, just** [use Redux and React Router directly](。).

同时使用 Redux 和 React Router 时这个库不是必须的。你可以直接使用他们不需要其他额外的库。他只是协助你记录，保存，和重现 action，和时间旅行。如果你不需要这些功能，那么直接使用 Redux 和 React Router 吧。

## 安装

```javascript
npm install --save react-router-redux
```

If you want to install the next major version, use react-router-redux@next. Run npm dist-tag ls react-router-redux to see what next is aliased to.

如果你想安装下一代版本，使用 `react-router-redux@next`，运行 `npm dist-tag ls react-router-redux` 查看 `next` 是什么的别名。

## 如何工作

This library allows you to use React Router's APIs as they are documented. And, you can use redux like you normally would, with a single app state. The library simply enhances a history instance to allow it to synchronize any changes it receives into application state.

你可以直接使用 React Router 文档所描述的 API，和使用 redux 改变单个应用程序的状态就像之前已经习惯的方式。

这个库简单的增强了 history 实例使他可以同步任何从应用程序状态更改接收到内容。

[history](https://github.com/reactjs/history) + store ([redux](https://github.com/reactjs/redux)) → [react-router-redux](https://github.com/reactjs/react-router-redux) → enhanced [history](https://github.com/reactjs/history) → [react-router](https://github.com/reactjs/react-router)

## 使用指南

让我们来看一个简单例子：

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import { createStore, combineReducers, applyMiddleware } from 'redux'
import { Provider } from 'react-redux'
import { Router, Route, browserHistory } from 'react-router'
import { syncHistoryWithStore, routerReducer } from 'react-router-redux'

import reducers from '<project-path>/reducers'

// Add the reducer to your store on the `routing` key
const store = createStore(
  combineReducers({
    ...reducers,
    routing: routerReducer
  })
)

// Create an enhanced history that syncs navigation events with the store
const history = syncHistoryWithStore(browserHistory, store)

ReactDOM.render(
  <Provider store={store}>
    { /* Tell the Router to use our enhanced history */ }
    <Router history={history}>
      <Route path="/" component={App}>
        <Route path="foo" component={Foo}/>
        <Route path="bar" component={Bar}/>
      </Route>
    </Router>
  </Provider>,
  document.getElementById('mount')
)
```

Now any time you navigate, which can come from pressing browser buttons or navigating in your application code, the enhanced history will first pass the new location through the Redux store and then on to React Router to update the component tree. If you time travel, it will also pass the new state to React Router to update the component tree again.

现在所有的导航操作，如按下浏览器的导航按钮或通过程序代码导航，增强型 history 对象首先传递一个新的位置信息到 redux store 然后再传递给 react router 更新组件树。如果执行时间旅行操作，他会传递新的 state 给 react router 再次更新组件树。

## 如何监视导航事件，例如需要分析用户操作？

Simply listen to the enhanced history via `history.listen`. This takes in a function that will receive a `location` any time the store updates. This includes any time travel activity performed on the store.

最简单监视增强型 history 对象的方式是通过 `history.listen`。传递给他的函数将会在 store 更新时接收到  `location` 对象。包含时间旅行操作对 store 的操作。

```javascript
const history = syncHistoryWithStore(browserHistory, store)

history.listen(location => analyticsService.track(location.pathname))
```

系统中其他类型的事件，你可以使用 Redux middleware 观察所有 dispatch 给 action 给 store 的操作。

## 如果在我的 Redux store 使用了 Immutable.js 或其他 state wrapper 怎么办？

When using a wrapper for your store's state, such as Immutable.js, you will need to change two things from the standard setup:

    - By default, the library expects to find the history state at `state.routing`. If your wrapper prevents accessing properties directly, or you want to put the routing state elsewhere, pass a selector function to access the historystate via the `selectLocationState` option on `syncHistoryWithStore`.
    - Provide your own reducer function that will receive actions of type `LOCATION_CHANGE` and return the payload merged into the `locationBeforeTransitions` property of the routing state. For example, state.set("routing", {locationBeforeTransitions: action.payload}).

当你为 store 的 state 使用了 wrapper，例如 Immutable.js，你需要改变标准步骤的两处位置：
    - 这个默认库会在 `state.routing` 寻找 history state。如果你的 wrapper 阻止直接访问 state 属性，或你想把 routeing state 放到其他地方，请传递一个 selector function 给 `syncHistoryWithStore` 的 `selectLocationState` 参数从而访问 history state。
    - 提供你自己的 reducer function 并接收类型为 `LOCATION_CHANGE` 的 action，然后返回的 payload 给 rouing state 的 `locationBeforeTransitions` 属性。例如  `state.set("routing",{locationBeforeTransitions:action.payload})`。

These two hooks will allow you to store the state that this library uses in whatever format or wrapper you would like.

这两个 hook 让你的 store 可以保持 state 的同步，无论使用了哪些格式的 wrapper。

## 如何在容器组件访问 router state？

React Router [provides route information via a route component's props](https://github.com/reactjs/react-router/blob/latest/docs/Introduction.md#getting-url-parameters). This makes it easy to access them from a container component. When using [react-redux](https://github.com/rackt/react-redux) to connect() your components to state, you can access the router's props from the [2nd argument of mapStateToProps](https://github.com/rackt/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options):

React Router 通过 route 组件的 props 提供 route 信息。使他可以轻松的从容器组件访问他们。当使用 react-redux 的 `connect()` 连接组件和 state 时，你可以通过 mapStateToProps 的第二个参数访问 router 的 props：

```javascript
function mapStateToProps(state, ownProps) {
 return {
   id: ownProps.params.id,
   filter: ownProps.location.query.filter
 };
}
```

You should not read the location state directly from the Redux store. This is because React Router operates asynchronously (to handle things such as dynamically-loaded components) and your component tree may not yet be updated in sync with your Redux state. You should rely on the props passed by React Router, as they are only updated after it has processed all asynchronous code.

你不应该直接从 Redux store 直接读取 location state。因为 React Router 运算是异步的 (就像动态加载组件一样) 并且你的组件树可能没有与 Redux state 同步更新。你应该依据 React Router 传递的 props 值判断，只有当所有异步代码处理完成后他才会更新。

## 如果我想通过 Redux action 实现导航应该怎么做？

React Router provides singleton versions of history (`browserHistory` and `hashHistory`) that you can import and use from anywhere in your application. However, if you prefer Redux style actions, the library also provides a set of action creators and a middleware to capture them and redirect them to your history instance.

React Router 提供了单例版本的 history (`browserHistory` 和 `hashHistory`) 你可以在应用程序任意位置导入和使用他们。但如果你准备使用 Redux 风格的 action，这个库也提供了一系列 action creators 集合和 middleware 实现捕获和重定向到你的 history 实例。

```javascript
import { routerMiddleware, push } from 'react-router-redux'

// Apply the middleware to the store
const middleware = routerMiddleware(browserHistory)
const store = createStore(
  reducers,
  applyMiddleware(middleware)
)

// Dispatch from anywhere like normal.
store.dispatch(push('/foo'))
```

## 例子

[examples/basic](https://github.com/reactjs/react-router-redux/blob/master/examples/basic) - basic reference implementation

Examples from the community:

- [shakacode/react-webpack-rails-tutorial](https://github.com/shakacode/react-webpack-rails-tutorial) - react-router-redux including **Server Rendering** using [React on Rails](https://github.com/shakacode/react_on_rails/), live at [www.reactrails.com](http://www.reactrails.com/).
- [davezuko/react-redux-starter-kit](https://github.com/davezuko/react-redux-starter-kit) - popular redux starter kit
    **tip**: migrating from react-router-redux ^3.0.0? use [this commit](https://github.com/davezuko/react-redux-starter-kit/commit/0df26907) as a reference
- [svrcekmichal/universal-react](https://github.com/svrcekmichal/universal-react) - Universal react app with async actions provided by [svrcekmichal/reasync](https://github.com/svrcekmichal/reasync) package
- [steveniseki/react-router-redux-example](https://github.com/StevenIseki/react-router-redux-example) - minimal react-router-redux example includes css modules and universal rendering
- [choonkending/react-webpack-node](https://github.com/choonkending/react-webpack-node) - Full-stack universal Redux App
- [kuy/treemap-with-router](https://github.com/kuy/treemap-with-router) - An example for react-router-redux with d3's treemap.

_→ Have an example to add? Send us a PR! ←_

## API

### `routerReducer()`

**You must add this reducer to your store for syncing to work.**

你必须添加这个 reducer 到你的 store 实现同步工作

A reducer function that stores location updates from `history`. If you use `combineReducers`, it should be nested under the `routing` key.

sotres location 的 reducer function 从 `history` 更新。如果你使用了 `combineReducers`，他需要有一个 `routing` key。

### history = syncHistoryWithStore(history, store, [options])

Creates an enhanced history from the provided history. This history changes `history.listen` to pass all location updates through the provided store first. This ensures if the store is updated either from a navigation event or from a time travel action, such as a replay, the listeners of the enhanced history will stay in sync.

从给定的 history 创建增强型 history。这个 history 会更改 `history.listen` ，所有的 location 更新首先会传递给所提供的 store。确保了发生导航事件或时间旅行操作 action，例如重现 action 后 store 是已更新的，增强型 history 的 listener 将会保持同步。

**You must provide the enhanced history to your `<Router>` component.** This ensures your routes stay in sync with your location and your store at the same time.

你必须把增强型 history 传递给你的 `<Router>` 组件。确保你的 routes 保持与 location 和 store 的同时同步。

The options object takes in the following optional keys:
    - `selectLocationState` - (default state => state.routing) A selector function to obtain the history state from your store. Useful when not using the provided routerReducer to store history state. Allows you to use wrappers, such as Immutable.js.
    - `adjustUrlOnReplay` - (default true) When false, the URL will not be kept in sync during time travel. This is useful when using persistState from Redux DevTools and not wanting to maintain the URL state when restoring state.


`options` 对象接受以下的选项 key：
    - `selectLocationState`-(默认值： `state => state.routing`) 一个 selector 函数，从 store 获取 history state。当不使用所提供的 routerReducer 到 store history state 有用。允许你使用 wrappers，例如 Immutable.js。
    - `adjustUrlOnReplay`- (默认值：`true`) 当是 false 时，URL 将不会保持与时间旅行操作一致。当使用 Redux DevToos 的 persistState 并且不想在恢复 state 时修改 URL state 有用。

## push(location), replace(location), go(number), goBack(), goForward()

**你需要安装 `routerMiddleware` 这些 action 才能工作。**

Action creators that correspond with the [history methods of the same name](。). For reference they are defined as follows:

    - push - Pushes a new location to history, becoming the current location.
    - replace - Replaces the current location in history.
    - go - Moves backwards or forwards a relative number of locations in history.
    - goForward - Moves forward one location. Equivalent to go(1)
    - goBack - Moves backwards one location. Equivalent to go(-1)

Both push and replace take in a location descriptor, which can be an object describing the URL or a plain string URL.

These action creators are also available in one single object as routerActions, which can be used as a convenience when using Redux's bindActionCreators().

这些 action creator 的作用与 history 方法同名，他们的参考作用在下方定义：

    - push -  推送一个新的 location 到 history,变为当前 location。
    - replace - 替换 hisrory 的当前 location。
    - go - 根据相对数字后退或前进 history location。
    - goForward - 前进一个 location。等于 go(1);
    - goBack - 后退一个 location。等于 go(-1);

push 和 replace 在 [location descriptor](。) 用到了，他可以是一个描述 URL 的 object 或原生字符串 URL。

这个 action creator 也可以在一个单独的 object 使用：`routerActions`，当使用 Redux 的 `bindActionCreator()` 时他可以被方便的使用。

## routerMiddleware(history)

A middleware you can apply to your Redux store to capture dispatched actions created by the action creators. It will redirect those actions to the provided history instance.

一个中间件，你可以应用到你的 Redux store 中以捕获由 action creator 发出的 actions。他将会重定向这个 action 到你提供的 history 实例。

## `LOCATION_CHANGE`

An action type that you can listen for in your reducers to be notified of route updates. Fires after any changes to history.

一个 action 类型，你可以在你的 reducer 监听以通知 route 更新，会在任意 history 更新后触发。
