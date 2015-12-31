layout: [post]
title: "CocoaReactive Framework Overview"
date: 2015-10-16 01:13:34
tags: 
- iOS
- CocoaReactive
categories: 
- iOS
- 翻译
id: "CocoaReactiveFrameworkOverview"
---

没校验，暂时放上来。

<!-- more -->

[原文地址](https://github.com/ReactiveCocoa/ReactiveCocoa/blob/master/Documentation/FrameworkOverview.md)

---



# Framework Overview

这个文档包含 ReactiveCocoa 框架中组件的高层次描述，并解释它们之间如何协同工作和各自职责。这意味着你需要开始学习新的模块并寻找更多制定文档。
需要帮助你明白什么是 RAC 的例子，请阅读 [READERME]() 或 [Design Guidelines]()。

## Event

**Event**,通过 [Event]() 类型表示，用来说明发生了一些事情。在 ReactiveCocoa 中，event 是通信的核心。event 可能代表按钮按下，从某个 API 接收到信息的一部分，发生了错误，或者一个长时间运行的计算完成了。在这些情况中，有时是通过 signal 生成 event 并发生它们给任意数量的 observers。

`Event` 是枚举类型表示为值或者三个中断 event 中的一个。

* `Next` event 表示来源提供了新值。
* `Error` event 标识 signal 处理完成之前发生了错误，Event 通过参数化 `ErrorType` 类型提供，它进行判断错误出现在 event 中是否合法的，如果不合法，event 可以使用 NoError 类型防止发生。
* `Completed` event 标识 signal 成功完成，将不会有任何的值从来源发送。
* `Interrupted` event 标识 signal 已经由于取消而中断，意味着操作可能成功也可能不成功。

## Signals

**Signal**,由 [Signal]() 类型表示，是任何时候都可以被 observers 观测到的系列 event。

Signal 通常被用作代表已经 "在处理" 的事件，例如通知，用户输入等等。在工作执行后或接收到数据，event 会通过 signal 发送，它会将 event 发送给所有observers。所有 observers 会同时接收到 event。

用户必须使用 signal 的 [observe]() 以进行 event 处理。Observing signal 不会触发任何异常效果。换句话说，signal 是完全由生产者驱动和基推送，消费者 (observers) 无法对它的生命周期造成任何影响。在观测 signal 时，用户只能根据与 signal 发出 event 相同的顺序处理，它们不会随机访问 signal 的值。

可以通过 [primitives]() 对 Signal 进行操纵，通常 primitives 操纵可以单个的 signal 例如 `filter`，`map`，和 `reduce`，以及 primitives 一次操作多个 signal (`zip`)。Primitives 运算只能在 signal 的 `Next` event。`|>` 运算符将 primitive 应用在 signal 上，它也可以用作组成多个基础 primitives 到为更复杂的操作。

signal 的生命周期由任意数量的 `Next` evnet 组成，跟随着一个中断 event，可能是 `Error`，`Completed`，或 `Interrupted` 中的一个 (但不会是组合)。Terminating event 不包含 signal 的值，它们必须特别处理。

## Pipes

**Pipe**，通过 `Signal.pipe()` 创建，是一个可以手动控制的 [signal]()。

这个方法返回一个 [signal]() 和一个 [observer]()。该 signal 可以通过发送 event 到 observer 控制。这对桥接 non-RAC 代码到  signal 的世界中非常有用。

例如，要替代在登陆处理使用的 block 回调函数，block 只需要简单的发送 event 到 observer。期间，signal 可以被返回，隐藏回调函数的实现细节。

## Signal Producers

**Signal producers**，由 [SignalProducer]() 类型代表，用作创建多个 [signal]() 和执行特殊效果。

它们可以用来表示运算或任务，例如网络请求，每个地方调用的 `start()` 都会创建新的底层请求，并运行调用者 observe 结果(多个)。使用 `startWithSignal()` 变种可以访问 produced signal，如果需要，它可以观测多次。

因为 `start()` 的行为，从相同 producer 创建的每个 signal 可能会见到不同顺序或版本的 event，stream 甚至会完全不同！不像简单的 signal，没有工作需要 `start()` (因此它们不会生成 event),直到有 observer 绑定进来，每个新增加的 observer 的工作都会重新启动重新开始。

Signal producer 开始后会返回 [disposable]()，它可以被用做打断或取消绑定在 produced signal 的工作。

像 signal 一样，signal producer 也可能通过如 `map`，`filter`，等等操纵。每个 signal primitive 可以使用 "lifted" 替代在 signal producer 上操作 ，使用 `lift` 方法，或隐式通过 `|>` 运算符。还有额外的 primitive 控制工作*几时*开始和*如何*工作，例如 `times`。

## Buffers

**buffer**,由 `SignalProducer.buffer()` 创建，它是一个 event 队列，当新的 [signals]() 从 producer 创建会重置这些 event。

与 pipe 相似，这个方法返回一个 observer。Event 发送到这个 observer 将会被添加到队列中。如果当新的值到达时 buffer 容量已经满了，最早的值(最旧的)将会被移除为新值提供空间。

## Observers

**Observer** 是一个从 [signal]() 等待 [event]() 东西。在 RAC 内，observer 由 `SinkType` 表示，它能接收 `Event` 值。

Observer 可以由基于回调版本的 `Signal.observe` 隐式创建，或者通过 SignalProducer.star 方法创建。

## Action

**action**，由 `Action` 类型表示，当执行输入时会做一些工作，在执行时，零或更多输出值 and/or 可能会生成错误。

Action 可以对用户交互执行非常有用的特别效果，例如当一个按钮按点击后，Action 可以基于 property 自动禁用按钮，这个禁用的状态可以表现为 UI 通过禁用任意控件关联的 action。

要与 `NSControl` 或 `UIControl` 交互，RAC 提供了 `CocoaAction` 类型与 Objective-C 的 action 进行桥接。


## Properties


**property**，由 `PropertyType` 协议表示，用来保存值和通知 observers 相关未来对值的更改。

property 当前的值可以通过 `value` getter 获取。`producer` getter 返回 [signal producer]()，它将会发送 property 的当前值，每当以后值的更改都会发送。

`<~` 运算符可以被用做不同的方式绑定 properties。记住下面的案例，目标必须是一个 `MutablePropertyType`。

* `property <~ signal` 绑定 signal 到 property，更新了 property 的值，最新的值会通过 signal 发送。
* `property <~ producer` 开启给定的 [signal producer]()，绑定 property 的值，最新的值会在已开始的 signal 发送。
* `property <~ otherProperty` 绑定一个 property 到另一个中，因此每当来源 property 的值发生变化，目标 property 的值也会更新。

`DynamicProperty` 类型可以被用做桥接 Objective-C API 的 Key-Value Coding (KVC) 或 Key-Value Observing (KVO)，例如 NSOperation。注意大部分 AppKit 和 UIKit 属性不支持 KVO，因此观测它们的值的更改需要依赖其它机制。对于动态属性使用 `MutableProperty` 是首选。

> 实践任务
> 自定义一个属性，绑定到一个 signal，观察属性值更改之后 signal 发出的 event。

## Disposables

**Disposable**,由 Disposable 协议代表，是一种内存管理和消除的机制。

当 signal producer 开始后将会返回 disposable。disablesable 可以被用调用者用做取消已经开始了的工作 (如后台处理，网络请求等等)，清理所有临时资源，然后发送 `Interrupted` event 给特定的已经创建了 [signal]()。

Observing signal 可能也返回 disposable。Disposing 它将会防止 observer 未来从 signal 接收到任何 event，当不会对 signal 有任何影响。

更多关于消除机制，见 RAC [Design Guidelines]()。

## Schedulers

**scheduler**，由 `SchedulerType` 协议表示，是一个串行执行队列，用做执行工作或交付结果。

[Signal]() 和 [signal producers]() 可以交付 event 给 scheduler 发出。[Signal producers]() 可以指定由 scheduler 开始它们的工作。

Schedulers 类似 Grand Central Dispatch 队列，但 schedulers 支持取消操作 (通过 disposables)，并总是连续执行。除了 `ImmediateScheduler` 外，scheduler 不提供同步执行。这有助于避免死锁，并鼓励使用 [signal]() 和 [signal producer primitive]() 替代 blocking。

Schedulers 也有些像 `NSOperationQueue`，但 schedulers 不允许任务重新排序或者依赖其中另一个。
