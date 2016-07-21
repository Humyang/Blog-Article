layout: [post]
title: "React-可重用组件"
date: 2015-11-29 23:18:56
tags:
- 前端
categories:
- 前端
- React
id: "reusable-components"
---

Prop Validation，Default Prop Values，Transferring Props: A Shortcut，Single Child，Mixins，ES6 Classes，Stateless Functions。

<!-- more -->


---

[原文地址](http://air-2.local:55750/Dash/nwfpfmid/facebook.github.io/react/docs/reusable-components.html#//dash_ref_172/Section/Mixins/0)

看完 React 入门的评论组件项目后，尝试看 thoustonejs 的源代码，发现遇到问题挺多的，现在进一步了解 React。

因为在 touchstonejs 源代码入口就遇到了 mixins 和 propTypes 两个都不明白的参数，刚好篇文章两个属性都介绍到。

# Reusable Components

在设计界面时，分解常见设计的元素 (按钮，表单字段，布局组件等) 到可重用的组件作为良好设计的接口。因此，接来下我们来创建一些 UI，你只需要写很少的代码。这意味着快速开发的时间，减少 Bug，和文件大小。

## 属性验证

随着你的应用程序代码量增长它可以提供帮助确保你的组件被正确使用。我们通过让你指定 `propTypes` 实现。React.PropTypes 输出一系列验证可以用作确保你接收到有效数据。当无效的值提供给 prop 时，会在 JavaScript 控制台发出警告。注意因为性能原因 `propTypes` 只有在开发模式才会监测。这里是提供不同属性验证的案例文档：

```javascript

React.createClass({
  propTypes: {
    //你可以将 prop 定义为特定的 JS 原始类型。默认这些都是可选的
    optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,

    // 任何可以渲染的: numbers, strings, elements 或 array
    // (or fragment) 都包含在这个类型.
    optionalNode: React.PropTypes.node,

    // A React element.
    optionalElement: React.PropTypes.element,

    // 你也可以声明 prop 是一个类的实例。这里使用 JS 的 instanceof 运算符
    optionalMessage: React.PropTypes.instanceOf(Message),

    // 你可以确保你的 prop 限制为指定的值通过指定一个枚举
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

    // 对象可以是多个类型之一。
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),

    // 某些类型的数组
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

    // 对象的属性值是某些类型
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

    // An object 也接受特定形状
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),

    //上面提到的所有类型还能以链式添加 isRequired 指定该 prop 是必须的，如果没有提供则会报错
    requiredFunc: React.PropTypes.func.isRequired,

    // 指定为任意类型数据的值
    requiredAny: React.PropTypes.any.isRequired,

    // 你也可以指定自定义验证器。如果验证失败它应该返回一个错误。不要使用 `console.warn` 或 throw，因为不会在 `oneOfType` 内工作。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  },
  /* ... */
});

```

## 默认 Prop 值

React 让你以非常直观的方式定义你的 Prop 的默认值：

```javascript

var ComponentWithDefaultProps = React.createClass({
  getDefaultProps: function() {
    return {
      value: 'default value'
    };
  }
  /* ... */
});

```

`getDefaultProps()` 的结果将会被缓存并确保如果 `this.props.value` 没有被上级组件指定值它也会有值。这让你可以安全的使用 props 不用重复的写处理代码。

## 传输 Props:便捷方式

React 组件的常用类型是以简单的方式拓展基础 HTML 元素。通常你想复制 HTML 属性传递到你的组件中并把组件放到 HTML 元素下面。要减少输入，你可以使用 JSX 的括号语法实现：

```javascript

var CheckLink = React.createClass({
  render: function() {
    // This takes any props passed to CheckLink and copies them to <a>
    return <a {...this.props}>{'√ '}{this.props.children}</a>;
  }
});

ReactDOM.render(
  <CheckLink href="/checked.html">
    Click here!
  </CheckLink>,
  document.getElementById('example')
);

```

## Single Child

使用 `React.PropTypes.element` 你可以指定 props 只能有一个子级传递到组件作为子级。

```javascript

var MyComponent = React.createClass({
  propTypes: {
    children: React.PropTypes.element.isRequired
  },

  render: function() {
    return (
      <div>
        {this.props.children} // 必须精确为只有一个元素否则报错
      </div>
    );
  }

});

```

## Mixins

React 中实现代码复用最好的方式是创建组件，但有时候一些差别很大的组件可能想共享它们之间一些功能。这种情况被称为 [cross-cutting concerns](https://en.wikipedia.org/wiki/Cross-cutting_concern),React 提供了 `mixins` 解决这个问题。

一个最常见的使用场景是组件想每隔一段时间更新自身。它可以简单的使用 `setInterval()`，但你终止循环并释放内存。React 提供了 `lifecycle methods` 让你知道组件何时创建或销毁。让我们来创建一个简单的 mixin 使用这些方法提供一个简单的 `setInterval()` 方法在你的组件销毁时自动清理。

```javascript

var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.forEach(clearInterval);
  }
};

var TickTock = React.createClass({
  mixins: [SetIntervalMixin], // Use the mixin
  getInitialState: function() {
    return {seconds: 0};
  },
  componentDidMount: function() {
    this.setInterval(this.tick, 1000); // Call a method on the mixin
  },
  tick: function() {
    this.setState({seconds: this.state.seconds + 1});
  },
  render: function() {
    return (
      <p>
        React has been running for {this.state.seconds} seconds.
      </p>
    );
  }
});

ReactDOM.render(
  <TickTock />,
  document.getElementById('example')
);

```

mixins 一个很好的功能是如果组件使用多个 mixins 并且这几个都定义了相同的 lifecycle 方法 (例如几个 mixins 想在组件销毁时做一些清理)，所有 lifecycle methods 方法都会被调用到。在 mixins 定义的方法会按照 mixins 列表的顺序运行，跟随着方法在组件中调用。

## ES6 的类

你也可以将 React 的类定义成普通的 JavaScript 的类。例如使用 ES6 的 class 语法：

```javascript

class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

```

这个 API 与 `React.createClass` 类似但 `getInitialState` 例外。它分离了 `getInitialState` 方法使用替代方式，通过在 constructor 的 `state` 属性中设置。

另一个不同是 `propTypes` 和 `defaultProps` 是在 constructor 的属性中定义而不是在 class body。

```javascript

export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return (
      <div onClick={this.tick.bind(this)}>
        Clicks: {this.state.count}
      </div>
    );
  }
}
Counter.propTypes = { initialCount: React.PropTypes.number };
Counter.defaultProps = { initialCount: 0 };

```

### 没有自动绑定

方法跟随 ES6 class 相同的语义规则，意味着它不会自动绑定 `this` 到实例。你将要明确的使用 `.bind(this)` 或 arrow functions `=>` 将 this 绑定到实例中。

### 没有 Mixins

不幸的是 ES6 没有任何 mixin 的支持。因此，当你把 React 和 ES6 class 一起使用时不支持 mixins。作为替代，我们正努力使这种情境的使用变得更简单而不需要使用 mixins。

## 无状态方法

你也可以将你的 React 类定义为普通的 JavaScript 方法。例如使用下面无状态方法语法：

```javascript

function HelloMessage(props) {
  return <div>Hello {props.name}</div>;
}
ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

```

或者使用新的 ES6 箭头语法：

```javascript

var HelloMessage = (props) => <div>Hello {props.name}</div>;
ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);

```

简化了的组件 API 为 props 是纯方法的组件提供。这些组件必须没有保持内部状态，没有返回实例，和没有组件生命周期方法。它们是输入的纯方法转换，没有 boilerplate。

> 注意：因为无状态方法没有返回实例，你不能捆绑 ref 到无状态组件。通常这不是问题，因为无状态方法不能提供 imperative API。没有 imperative API，就没有太多实例可以做的事情。无论如何，如果用户想在无状态组件寻找 DOM 节点，它们必须把组件让有状态组件 (如 ES6 class 组件) 包裹和捆绑它们的 ref 到包裹着它的有状态组件。

理想在状态下，大部分组件都是有状态方法因为有状态组件可以跟随 React 核心的快速的代码，这是推荐的模式。
