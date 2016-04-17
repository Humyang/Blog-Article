layout: [post]
title: Redux (一) 介绍
date: 2016-04-17 01:00:32
tags:
- 前端
categories:
- 前端
- Redux
---

简单介绍 Redux 的作用和概念。

<!-- more -->


---

# Redux 介绍

## 什么是 Redux

Redux 是替你管理应用程序状态 (如 React 中的 State) 的类库，不单只有 React 程序能用，事实上所有程序都能使用 Redux，但配合 React 这种响应式程序使用更佳。

## Redux 如何工作？

通过分发一个对象 (Action) 通知程序产生了哪些动作，然后由一个函数 (Reducer) 决定如何操作更改程序的 State。

## 为什么使用 Redux


React 程序的 render 方法内不再需要写一大堆判断 State 的代码。
使程序架构更清晰，易维护及拓展。
Redux 提供可预见的 State  (所有 State 可能变化的操作统一写在一个函数中 (Reducer) 。通过 Redux Devtool，使错误可以重现，并使调试变得简单)。
State 可以存储本地，或从服务器恢复，前后端开发更加方便。


## 基础概念

Redux 有三个基本概念：Store，Reducer，Action。

### Store

整个应用程序的状态以 Object Tree 的形式保存在唯一的 Store 中，Object Tree 的类型是原生 JavaScript  Object 。

唯一能更改 Object Tree 值的方式是 Dispatch Action。

因为这个 Object Tree 是原生 JavaScript Object 类型，所以可以存放任何数据。

### Action

Action 是原生 JavaScript Object 类型，内部必须有 type 属性，表明 Action 执行什么操作。

Object 内部除了 type，其它结构取决于你，Reducer 根据 Action 操作 State (只有在 Reducer 内才能操作 State，并且不能直接修改而是返回一个新的 State)。

Action 通过 Dispatch 分发。

Action 可以预定义，也可以由方法根据参数生成返回动态的 Action。

### Reducer

Reducer 是纯函数 (`(state, Action) => state`)，描述了如何将  Action 转换为实际的操作，并返回新的 state。

与 Store 一样，整个应用程序只有一个根 Reducer，这个 Reducer 的参数会传入当前 State，返回下一个 State，注意是返回下一个 State，一定不能修改当前 State！

可以创建多个 Reducer，分别修改 Store 的子属性，达到模块化的目的。

可以使用 `combineReducers` 将多个 function 合并成一个 Reducer。


##  相关资料

[调试工具](https://github.com/gaearon/Redux-devtools/blob/master/docs/Walkthrough.md)
[文档](http://Redux.js.org/docs/basics/Reducers.html)
[项目主页](https://github.com/reactjs/Redux)
