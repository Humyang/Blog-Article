layout: [post]
title: Flexbox 布局  (二) Container
date: 2016-01-24 18:23:48
id: "Flexbox2"
tags:
- 前端
- 翻译
categories:
- CSS
- 布局
---

介绍 Flexbox 的概念，和 Child 能应用哪些属性。

<!-- more -->


---




# Properties for the Children (flex items)

![](./flex-items.svg)

## order

![](./order-2.svg)

> By default, flex items are laid out in the source `order`. However, the order property controls the order in which they appear in the flex container.

flex Item 顺序默认按照源顺序排序。而 `order` 属性可以控制他们的排列顺序。

```css
.item {
  order: integer;
}
```

## flex-grow

![](./flex-grow.svg)

> This defines the ability for a flex item to grow if necessary. It accepts a unitless value that serves as a proportion. It dictates what amount of the available space inside the flex container the item should take up.

可以使用这个属性根据需要增大 flex Item 。他接受无单位的值作为比例。他根据比例将 flex  Container 可用的空间分配给 flex Item 。

> If all items have flex-grow set to 1, the remaining space in the container will be distributed equally to all children. If one of the children a value of 2, the remaining space would take up twice as much space as the others (or it will try to, at least).

如果所有的 Item 的 flex-grow 属性设置为 1， Container 剩余的空间将会平均分配给 flex Item 。如果一个值是 2，剩余的空间将会为此 Item 分配比其他 Item 一倍的空间  (会尝试)。

```css
.item {
  flex-grow: <number>; /* default 0 */
}
```

> Negative numbers are invalid.

负数是无效的。

## flex-shrink

> This defines the ability for a flex item to shrink if necessary.

如果需要可以缩小 flex Item 。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

> Negative numbers are invalid.

负数是无效的。

## flex-basis

> This defines the default size of an element before the remaining space is distributed. It can be a length (e.g. 20%, 5rem, etc.) or a keyword. The `auto` keyword means "look at my width or height property" (which was temporarily done by the `main-size` keyword until deprecated). The `content` keyword means "size it based on the item's content" - this keyword isn't well supported yet, so it's hard to test and harder to know what it's brethren `max-content`, `min-content`, and `fit-content` do.

分配空间前指定元素的默认尺寸。他可以是一个长度  (如 20%，5rem 等) 或关键字。关键字 `auto` 意味着 “根据我的 width 或 height 属性”  (曾经临时使用关键字 `main-size`，现已弃用)。 关键字 `content` 意味着 “尺寸是基于 Item 的内容” - 这个关键字不是很好的被支持，因此他很难测试并且更难知道他的哪些兄弟有效果：`max-content`,`min-content` 和 `fit-content`。

```css
.item {
  flex-basis: [length] | auto; /* default auto */
}
```

> If set to `0`, the extra space around content isn't factored in. If set to `auto`, the extra space is distributed based on its `flex-grow` value. See this graphic.

如果设置为 `0`，环绕内容的额外空间则不会算上。如果设置为 `auto`，额外空间的分配基于他的 `flex-grow` 值。见此图：

![](./rel-vs-abs-flex.svg)

## flex

> This is the shorthand for `flex-grow`, `flex-shrink` and `flex-basis` combined. The second and third parameters (`flex-shrink` and `flex-basis`) are optional. Default is `0 1 auto`.

这是 `flex-grow`,`flex-shrink` 和 `flex-basis` 组合的缩写。第二和第三个参数是可写的。默认是 `0 1 auto`。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

**It is recommended that you use this shorthand property** rather than set the individual properties. The short hand sets the other values intelligently.

**推荐使用这个缩写属性** 而不要使用单个属性。这个缩写更加智能的设置其他值。

## align-self

![](./align-self.svg)

> This allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.

使单个 flex Item 可以覆盖默认的对齐方式  (或通过 `align-items` 指定一个)。

> Please see the `align-items` explanation to understand the available values.

请参照 `align-items` 了解可用值。

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

> Note that `float`, `clear` and `vertical-align` have no effect on a flex item.

注意 `float`，`clear`，和 `vertical-align` 在 flex Item  没有效果。
