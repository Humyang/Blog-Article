layout: [post]
title: React 的 context 和 childContext
date: 2015-12-31 17:17:50
tags: 
- 前端
categories: 
- 前端 
- React
---

介绍如何使用 React 的 context 

<!-- more -->


---

[原文地址](http://javascript.tutorialhorizon.com/2015/06/06/using-context-and-childcontext-in-react/)

# Using context and childContext in React

在 React 使用 context 和 childContext

> When work­ing with React in a deeply nested hier­ar­chy, often times you will find your­self in a sit­u­a­tion where you need to pass down props from the par­ent as is to the chil­dren and the grand­chil­dren. Although pass­ing down prop­er­ties is great, but writ­ing code in such a man­ner encour­ages rely­ing on mem­ory to pass down the nec­es­sary props, and that’s not really a good use of your brain.Fortunately, React pro­vides a way to make this task easier.

在操作 React 中深层嵌套的层次结构时，当你需要从父组件获取 props 传递到子组件时，通常你需要找到自己所在的位置。尽管传递 properties 是好的做法，但在写代码时却要依靠记忆传递所需要的 props，这对大脑来说不怎么友好。幸运的是，React 提供了一种方式使得这些工作简单完成。

> React has some­thing called as Child contexts that allows a par­ent ele­ment to spec­ify a con­text — aka a set of prop­er­ties — which can be accessed from all of its chil­dren and grand­chil­dren via the this.context object.

React 有一些叫做 Child context 的东西，允许父元素指定一个 context - 等于设置一个属性 － 它可以通过 `this.context` 对象访问它所有的 children 和 grandchildren。


> There are 2 aspects to how you would go about imple­ment­ing this in your code.

在代码实现需要处理两方面。

> 1.In the par­ent, the getChild­Con­text method is used to return an object that is passed own as the child con­text. The prop types of all the keys in this object must also be defined in the childContextTypes prop­erty of the parent.
> 2.Any child that needs to con­sume the prop­er­ties passed down from its par­ents must whitelist the prop­er­ties it wants to access via the ‘con­text­Types’ property.
> Here’s an exam­ple of how this works

1.在父组件，getChildContext 方法返回一个对象，这个对象把自己传给 child context。这个对象中所有的 key 的 prop types 也必须在父组件的 childContextType 属性中定义。
2.任何 child 想访问从 parent 传递过来的 properties，都需要通过将 properties 添加到 contextTypes 属性进行访问。


这里是一段它们如何工作的代码：

```javascript

var Grandparent = React.createClass({

    childContextTypes: {
         foo: React.PropTypes.string.isRequired
    },

    getChildContext: function() {
         return { foo: "I m the grandparent" };
    },

    render: function() {
         return <Parent />;
    }
});


var Parent = React.createClass({

    childContextTypes: {
         bar: React.PropTypes.string.isRequired
    },

    getChildContext: function() {
         return { bar: "I am the parent" };
    },

    render: function() {
         return <Child />;
    }
});

var Child = React.createClass({

    contextTypes: {
        foo: React.PropTypes.string.isRequired,
        bar: React.PropTypes.string.isRequired
    },

    render: function() {
        return (
          <div>
            <div>My name is: {this.context.foo}</div>
            <div>My name is: {this.context.bar}</div>
          </div>
        )
    }
});

// Finally you render the grandparent
React.render(<Grandparent />, document.body);

```

One may argue that this makes the code a bit more ver­bose, because now you end up cre­at­ing an addi­tional key contextTypes on every child com­po­nent. How­ever, the real­ity is that you can spec­ify the ‘con­text­Types’ prop­erty on a mixin. That way you can avoid rewrit­ing the whitelist­ing boil­er­plate code by sim­ply using the mixin on all the child com­po­nents that need to access those prop­er­ties from its context.

有人可能会说这使得代码更复杂，因为现在要在每个子组件额外的添加 `contextTypes` 属性。但是，其实你可以把 contextTypes 属性的代码放到 mixin。通过简单的在所有子组件使用 mixin 可以避免重写白名单的代码，这样所有子组件都可以通过 context 访问父组件的属性了。
