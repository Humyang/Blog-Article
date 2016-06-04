# 组件的设计

设计优先级：布局 > 样式

常用的提取出来，特例不考虑到组件，单独用低一级的组件拼装。

单为一个页面设计的组件不要跨页面使用

# 1.定义 state 和还是 props？

state 是可变的，props 是不可变的，在设计组件时，组件自身要操纵一些变化才使用 state，否则都应该使用 props。

改变 props 的工作交给组件调用者。

#  构建 HTML 的方式

## 数组

jsx 会自动将数组内的 html 标签转换

```javascript
let htmlArray = [];
htmlArray.push( <div></div>);

return <table>{ htmlArray }</table>
```

2. JavaScript 方式

在 render 函数的 return 的花括号中返回 html，例如：

```javascript

return <div >{
    [<div key={1}></div>,<div key={2}></div>,<div key={3}></div>].map((item)=>{
        return item
        })
    }</div>;

```
注意数组中的每个组件都需要关键字 key


# 写组件时明确设置默认值

有默认值的组件可以一目了然的知道要传递哪些值。

# 在 render 利用解构对象获取 props 的值  

可以清晰知道 props 内哪些值需要在 render 中使用。

如果 render 内有函数，使用参数的方式传递数据，不要直接在函数内使用 this.props.A。

let {A,B} = this.props;

# 严格区分上下级组件的关系

父组件不要直接传递 HTML 元素给子组件，如果子组件有需要根据 props 变化的部分，建议提取成一个组件，直接传递需要的值给新组件。



# 命名规则

class:  a-b-c
css id 或 class 命名结尾添加类型，如 label，input

组件属性名 props: a_b_c

全局变量：aaAA

组件名: AbcD

函数 aBcDe

不直接使用 object，使用解构对象的方式提取数据使用

const {a,b,c} = words;

# React 与 form 组件

https://facebook.github.io/react/docs/two-way-binding-helpers.html

https://facebook.github.io/react/docs/forms.html

ReactLink

valueLink
