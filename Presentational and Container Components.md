# Presentational and Container Components

表现层组件和容器组件

There’s a simple pattern I find immensely useful when writing React applications. If you’ve been doing React for a while, you have probably already discovered it. This article explains it well, but I want to add a few more points.

这是我在写 React 应用程序时找到的非常有用并简单的模式。[如果你已经使用过 React 一段时间](http://facebook.github.io/react/blog/2015/03/19/building-the-facebook-news-feed-with-relay.html)，你可能已经发现了。[这篇文章解释得很好](https://medium.com/@learnreact/container-components-c0e67432e005)，但我想添加一些东西。

You’ll find your components much easier to reuse and reason about if you divide them into two categories. I call them Container and Presentational components* but I also heard Fat and Skinny, Smart and Dumb, Stateful and Pure, Screens and Components, etc. These all are not exactly the same, but the core idea is similar.

你的组件将会更易重用和合理如果你将他们分成两大类。我把他们称为`容器组件`和`表现层组件`，我也听说了  Fat and Skinny, Smart and Dumb, Stateful and Pure, Screens and Components, 等。他们都不完全一样，但核心的理念是一样的。


My **presentational** components:
- Are concerned with how things look.
- May contain both presentational and container components** inside, and usually have some DOM markup and styles of their own.
- Often allow containment via this.props.children.
- Have no dependencies on the rest of the app, such as Flux actions or stores.
- Don’t specify how the data is loaded or mutated.
- Receive data and callbacks exclusively via props.
- Rarely have their own state (when they do, it’s UI state rather than data).
- Are written as functional components unless they need state, lifecycle hooks, or performance optimizations.
- Examples: Page, Sidebar, Story, UserInfo, List.

我的表现层组件：

- 是关心事物看起来如何的。
- 内部可以包含表现层组件和容器组件，并通常有一些属于自己的 DOM 标记和样式。
- 通常允许通过 this.props.children 实现容器化。
- 不依赖 app 其余部分，例如 Flux action 或 stores。
- 不用指定数据如何加载或修改。
- 接收数据和回调方法只通过 `props`。
- 很少有属于自己的 state (当有时，他们是 UI state 而不是数据)。
- 是写成功能组件的，除非他们需要 state，挂钩生命周期，或执行优化。
- 例如：页面，侧边栏，用户信息，列表。

My **container** components:

- Are concerned with how things work.
- May contain both presentational and container components** inside but usually don’t have any DOM markup of their own except for some wrapping divs, and never have any styles.
- Provide the data and behavior to presentational or other container components.
- Call Flux actions and provide these as callbacks to dumb components.
- Are often stateful, as they tend to serve as data sources.
- Are usually generated using higher order components such as connect() from React Redux, createContainer() from Relay, or Container.create() from Flux Utils, rather than written by hand.
- Examples: UserPage, FollowersSidebar, StoryContainer, FollowedUserList.

I put them in different folders to make this distinction clear.

我的容器组件：

- 是关心事物如何工作的。
- 内部可以包含表现层组件和容器组件但通常没有任何他们自己的 DOM 标记除了一些作为包裹的 `div`，且永远没有任何样式。
- 提供数据和行为给表现层或其它容器组件。
- 调用 Flux action 和提供这些作为回调给哑组件。
- 通常是有状态的，因为他们通常被作为数据源。
- 通常使用[高阶组件](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)生成例如 React redux 的 connect()，Relay 的 createContainer(),或 Flux Utils 的 Container.create(),而不是直接手写。
- 例如：UserPage, FollowersSidebar, StoryContainer, FollowedUserList。

我把他们放在不同的文件夹来进行区分清楚。

## Benefits of This Approach

这种实现的优点

- Better separation of concerns. You understand your app and your UI better by writing components this way.
- Better reusability. You can use the same presentational component with completely different state sources, and turn those into separate container components that can be further reused.
- Presentational components are essentially your app’s “palette”. You can put them on a single page and let the designer tweak all their variations without touching the app’s logic. You can run screenshot regression tests on that page.
- This forces you to extract “layout components” such as Sidebar, Page, ContextMenu and use this.props.children instead of duplicating the same markup and layout in several container components.

> Remember, components don’t have to emit DOM. They only need to provide composition boundaries between UI concerns.

Take advantage of that.

- 更好的分离关注点。这种方式写组件更能了解你的 app 和 UI。
- 更好的复用。你可以使用相同的表现层组件在完全不同的 state 来源，并切把这些放到分离的容器组件使他们能在将来复用。
- 表现层组件实质上是你的 app 的 “调色板”。你可以把他们放到单独的页面和让他们的设计者调整所有变化而无需接触 app 的逻辑。你可以在这个页面运行 screenshot regression tests 。
- 强制你提取布局组件例如 Sidebar,Page,COntextMenu 和使用 this.props.children 替代几个组件重复相同的标记和布局。

记住，容器组件没有 DOM。他只需要提供组合不同 UI 所需要的边界。

利用这个优势。



## When to Introduce Containers?

开始介绍容器组件？

I suggest you to start building your app with just presentational components first. Eventually you’ll realize that you are passing too many props down the intermediate components. When you notice that some components don’t use the props they receive but merely forward them down and you have to rewire all those intermediate components any time the children need more data, it’s a good time to introduce some container components. This way you can get the data and the behavior props to the leaf components without burdening the unrelated components in the middle of the tree.

我猜测你开始构建你的 app 时首先创建的是表现层组件。最后你会发现传递了太多 props 到中间组件。当你注意到一些组件不需要用到他们接收到的 props 但只是要转发他们下去并且你重写了所有这些中间组件他们的子组件需要的更多数据，那时介绍一些容器组件的好时间。通过这种方式你可以获取数据和行为 props 给叶组件而不需要麻烦树结构中间无关的组件。

This is an ongoing process of refactoring so don’t try to get it right the first time. As you experiment with this pattern, you will develop an intuitive sense for when it’s time to extract some containers, just like you know when it’s time to extract a function. My free Redux Egghead series might help you with that too!

这是一个持续重构的过程所以不用设法第一时间就得到完美答案。当你尝试这种模式时，你会有一种直观的感觉，在需要提取容器时，就像当你明白要如何提取函数时的感觉。我的 [free Redux Egghead series](https://egghead.io/series/getting-started-with-redux) 可能也可以帮助你。

## Other Dichotomies

其他区分方法

It’s important that you understand that the distinction between the presentational components and the containers is not a technical one. Rather, it is a distinction in their purpose.

你要清楚表现层组件和容器组件这种区分方式不是唯一的技术。相反它是区分组件的目的。

By contrast, here are a few related (but different!) technical distinctions:

对比一下，这里是一些关联的 (但不一样的) 区分技术

- **Stateful and Stateless.** Some components use React setState() method and some don’t. While container components tend to be stateful and presentational components tend to be stateless, this is not a hard rule. Presentational components can be stateful, and containers can be stateless too.
- **Classes and Functions.** Since React 0.14, components can be declared both as classes and as functions. Functional components are simpler to define but they lack certain features currently available only to class components. Some of these restrictions may go away in the future but they exist today. Because functional components are easier to understand, I suggest you to use them unless you need state, lifecycle hooks, or performance optimizations, which are only available to the class components at this time.
- **Pure and Impure.** People say that a component is pure if it is guaranteed to return the same result given the same props and state. Pure components can be defined both as classes and functions, and can be both stateful and stateless. Another important aspect of pure components is that they don’t rely on deep mutations in props or state, so their rendering performance can be optimized by a shallow comparison in their shouldComponentUpdate() hook. Currently only classes can define shouldComponentUpdate() but that may change in the future.

- **状态和无状态。** 一些组件使用了 React 的 setState() 方法而一些没使用。容器组件倾向于有状态而表现层组件倾向于无状态，但这不是固定的规则。表现层组件可以是有状态的，而容器也可以是无状态的。
- **类和函数。** 从 React 0.14 起，组件可以被声明为类和函数。函数组件定义较简单但他们缺乏某些当前只能在类使用的功能。这些限制可能在未来解决但现在还是存在的。因为函数组件更容易明白，我建议你使用他们除非你需要 state，挂钩生命周期，或性能优化，他们只能在类组件中使用。
- **纯与不纯。** 人们称如果组件保证返回与传入相同的 props 和 state 那么他是纯的。纯组件可以被定义为类和函数，也可以是有状态和无状态的。纯组件另一重要的方面是他们不依靠 props 或 state 的深度改变，因此他们的渲染性能可以通过他们的 shouldComponentUpdate() hoot 浅层比较进行优化。当前只有类可以定义 shouldComponentUpdate() hook 但可能在未来发生变化。


Both presentational components and containers can fall into either of those buckets. In my experience, presentational components tend to be stateless pure functions, and containers tend to be stateful pure classes. However this is not a rule but an observation, and I’ve seen the exact opposite cases that made sense in specific circumstances.

表现层组件和容器组件都可以分为这些两种种类。以我的经验，表现层容器倾向于无状态纯函数，容器倾向于有状态纯类。但这不是规则但根据观察，且我已经发现在特定的情况下会出现完全相反的情况。

Don’t take the presentational and container component separation as a dogma. Sometimes it doesn’t matter or it’s hard to draw the line. If you feel unsure about whether a specific component should be presentational or a container, it might be too early to decide. Don’t sweat it!

不要把表现层组件和容器组件的分离作为教条。有时候他并不重要或者他很难绘制一条线条。如果你感到不确定特定的组件应是表现层组件或容器组件，那么不用太早决定。不用浪费太多汗水！

## Example

This [gist ](https://gist.github.com/chantastic/fc9e3853464dffdb1e3c)by [Michael Chan](https://twitter.com/chantastic) pretty much nails it.

## Further Reading

- [Getting Started with Redux](https://egghead.io/series/getting-started-with-redux)
- [Mixins are Dead, Long Live Composition](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)
- [Container Components](https://medium.com/@learnreact/container-components-c0e67432e005)
- [Atomic Web Design](http://bradfrost.com/blog/post/atomic-web-design/)
- [Building the Facebook News Feed with Relay](http://facebook.github.io/react/blog/2015/03/19/building-the-facebook-news-feed-with-relay.html)

## Footnotes

> * In an earlier version of this article I called them “smart” and “dumb” components but this was overly harsh to the presentational components and, most importantly, didn’t really explain the difference in their purpose. I enjoy the new terms much better, and I hope that you do too!
> ** In an earlier version of this article I claimed that presentational components should only contain other presentational components. I no longer think this is the case. Whether a component is a presentational component or a container is its implementation detail. You should be able to replace a presentational component with a container without modifying any of the call sites. Therefore, both presentational and container components can contain other presentational or container components just fine.
