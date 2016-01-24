layout: [post]
title: Flexbox 布局  (一) Container
date: 2016-01-22 14:20:48
id: "Flexbox1"
tags:
- 前端
- 翻译
categories:
- CSS
- 布局
---

介绍 Flexbox 的概念，和 Container 能应用哪些属性。

<!-- more -->


---

# Background

> The Flexbox Layout (Flexible Box) module (currently a W3C Last Call Working Draft) aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word "flex").

Flexbox 布局  (Flexible 盒子) 模块  (当前是 W3C 最终草案)  皆在提供更灵活的布局方式，为对齐 Container 中的 Item 和分配空间，即使他们的尺寸是未知的或者动态的  (因此他被称为 flex)。

> The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate to all kind of display devices and screen sizes). A flex container expands items to fill available free space, or shrinks them to prevent overflow.

flex 布局背后主要想法是能让 Container 可以更改他的 “Item” 的宽度/高度  (和顺序)，得到最合适的可用空间  (尽可能适应所有设备的屏幕尺寸)。flex Container 会展开他的 Item 以占据所有可用空间，或收缩他们防止溢出。

> Most importantly, the flexbox layout is direction-agnostic as opposed to the regular layouts (block which is vertically-based and inline which is horizontally-based). While those work well for pages, they lack flexibility (no pun intended) to support large or complex applications (especially when it comes to orientation changing, resizing, stretching, shrinking, etc.).

最重要的，flexbox 布局是与方向无关的不是常规的布局  (块元素布局是基于垂直方向而内联元素基于水平方向)，虽然盒模型能良好的工作，但他们缺少一些灵活性  (不是双关) 支持大型或复杂的应用程序   (特别是当他面对页面方向更改，缩放，拉伸，收缩等)。

> Note: Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.

注意：Flexbox 布局最适合用到应用程序的组件，和小规模布局，而 Grid 布局更适合大规模布局。



# Basics & Terminology

基础 & 技术

> Since flexbox is a whole module and not a single property, it involves a lot of things including its whole set of properties. Some of them are meant to be set on the container (parent element, known as "flex container") whereas the others are meant to be set on the children (said "flex items").

因为 flexbox 是一个完整的模块，他不仅仅只有一个属性，他涉及到包含整个属性集大量的操作。他们之中一些负责操作 Container   (父元素，例如 “flex container”) 而其他一些负责操作子元素  (“flex items”)。

> If regular layout is based on both block and inline flow directions, the flex layout is based on "flex-flow directions". Please have a look at this figure from the specification, explaining the main idea behind the flex layout.

如果传统布局是基于块和内联流方向的，那么 flex 布局则是基于 “flex-flow 方向”。请看下图，图中指明了规范，解释了 flex 布局背后的思想。

![](./flexbox.png)

> Basically, items will be laid out following either the main axis (from main-start to main-end) or the cross axis (from cross-start to cross-end).

基本上， Item 将会随着 main axis 布局 (从 main-start 到 main-end) 或 cross axis  (从 cross-start 到 cross-end)。  

> - main axis - The main axis of a flex container is the primary axis along which flex items are laid out. Beware, it is not necessarily horizontal; it depends on the flex-direction property (see below).
> - main-start | main-end - The flex items are placed within the container starting from main-start and going to main-end.
> - main size - A flex item's width or height, whichever is in the main dimension, is the item's main size. The flex item's main size property is either the ‘width’ or ‘height’ property, whichever is in the main dimension.
> - cross axis - The axis perpendicular to the main axis is called the cross axis. Its direction depends on the main axis direction.
> - cross-start | cross-end - Flex lines are filled with items and placed into the container starting on the cross-start side of the flex container and going toward the cross-end side.
> - cross size - The width or height of a flex item, whichever is in the cross dimension, is the item's cross size. The cross size property is whichever of ‘width’ or ‘height’ that is in the cross dimension.

- main axis - flex Container 的主轴是基础的轴线， Container 内的 Item 沿着这条轴线布局。但注意，他不一定是水平的；他由 flex-direction 属性决定  (见下方)。
- main-start | main-end - Container 内的 flex Item 的位置从 main-start 开始到 main-end 结束。
- main size - flex Item 的宽度或高度，无论是否在 main dimension，他都是 Item 的主要尺寸。flex Item 的主要尺寸属性是 ‘width’ 或 ‘height’，无论是否处于 main dimension。
- cross axis - 与主轴垂直的轴线成为 cross axis，他的方向依赖主轴的方向。
- cross-start  | cross-end - 这个线条指示如何填充 Container 内的 Item ，从 cross-start 开始到 cross-end 结束。
- cross size - flex Item 的宽度和高度，无论是否处在 cross dimension，他都是 Item 的 cross size。cross size 属性无论是 ‘width’ 或 ‘height’ 都在 cross dimension。

# Properties for the Parent (flex container)

![](./flex-container.svg)

```css

.container {
  display: flex; /* or inline-flex */
}

```

## display



> This defines a flex container; inline or block depending on the given value. It enables a flex context for all its direct children.

该属性将元素定义为 flex Container ；依赖传入值变成内联或块级。设置后元素的直接子级全部变为的 flex 上下文。

> Note that CSS columns have no effect on a flex container.

注意 CSS 列在不会影响 flex Container 。

## flex-direction

![](./flex-direction1.svg)

> This establishes the main-axis, thus defining the direction flex items are placed in the flex container. Flexbox is (aside from optional wrapping) a single-direction layout concept. Think of flex items as primarily laying out either in horizontal rows or vertical columns.

这个属性构建 main-axis，因而定义 flex Item 方向的属性放到了 flex Container 中。Flexbox 是 (除了可选的 wrapping) 单方向的概念。记住 flex Item 的基础布局可以是水平的行或垂直的列。

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

> - row (default): left to right in ltr; right to left in rtl
> - row-reverse: right to left in ltr; left to right in rtl
> - column: same as row but top to bottom
> - column-reverse: same as row-reverse but bottom to top

- row  (默认值)：左到右  (从左到右的语言)；右到左  (右到左的语言)
- row-reverse：  右到左  (从左到右的语言)；左到右  (右到左的语言)
- column：与 row 相同但从顶部到底部
- column-reverse：与 row-reverse 相同但从底部到顶部

## flex-wrap

![](./flex-wrap.svg)

```css
.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

> By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property. Direction also plays a role here, determining the direction new lines are stacked in.

默认情况，flex Item 首先会尝试将在一行放置所有 item。你可以根据需要更改这个属性使 Item 环绕。方向在这里也起到作用，决定新的线条的叠加方向。

> - nowrap (default): single-line / left to right in ltr; right to left in rtl
> - wrap: multi-line / left to right in ltr; right to left in rtl
> - wrap-reverse: multi-line / right to left in ltr; left to right in rtl

- nowrap  (默认)：单行 / 左到右  (ltr)；右到左 (rtl)
- wrap：多行 / 左到右  (ltr)；右到左  (rtl)
- wrap-reverse：多行 / 右到左  (ltr)；左到右  (rtl)       

## flex-flow (Applies to: parent flex container element)

> This is a shorthand flex-direction and flex-wrap properties, which together define the flex container's main and cross axes. Default is row nowrap.

flex-direction 和 flex-wrap 属性的缩写，集合定义 flex Container 的 main 和 cross 轴。默认值是 row nowrap。

```css

flex-flow: <‘flex-direction’> || <‘flex-wrap’>

```

## justify-content

![](./justify-content.svg)

> This defines the alignment along the main axis. It helps distribute extra free space left over when either all the flex items on a line are inflexible, or are flexible but have reached their maximum size. It also exerts some control over the alignment of items when they overflow the line.

定义 main 轴的 Item 的对齐方式。这个属性帮助分配额外的自由空间，当线上的 flex Item 不够灵活或虽然灵活但达到最大尺寸。并且当 Item 超出了线的范围他也可以帮忙控制对齐。

```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

> - flex-start (default): items are packed toward the start line
> - flex-end: items are packed toward to end line
> - center: items are centered along the line
> - space-between: items are evenly distributed in the line; first item is on the start line, last item on the end line
> - space-around: items are evenly distributed in the line with equal space around them. Note that visually the spaces aren't equal, since all the items have equal space on both sides. The first item will have one unit of space against the container edge, but two units of space between the next item because that next item has its own spacing that applies.

- flex-start  (默认)： Item 从 start line 起包装
- flex-end： Item 从 end line 起包装
- center： Item 从 line 中心开始
- space-between： Item 尽可能占满 line，第一个 Item 在 start line ，最后一个 Item 在 end line
- space-around： Item 尽可能占满 line 并且彼此之间的距离相同。注意看起来是不相同的，因为所有的 Item 都有相同的空间在两侧，但第一个 Item 相对于 Container 只有一个单位的空间，但距离下一个 Item 有两个单位的空间因为下一个 Item 也有自己的单位空间。


## align-items

![](./align-items.svg)

> This defines the default behaviour for how flex items are laid out along the cross axis on the current line. Think of it as the justify-content version for the cross-axis (perpendicular to the main-axis).

定义 flex Item 在当前 line 如何沿着 cross aix 布局的默认行为。可以认为他是 justify-content 的 cross-axis 版本  (垂直于 main-axis)。

```css
.container {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

> - flex-start: cross-start margin edge of the items is placed on the cross-start line
> - flex-end: cross-end margin edge of the items is placed on the cross-end line
> - center: items are centered in the cross-axis
> - baseline: items are aligned such as their baselines align
> - stretch (default): stretch to fill the container (still respect min-width/max-width)

- flex-start： Item 的 cross-start 外边距边缘放置 cross-start line
- flex-end：item 的 cross-end 外边距放置到 cross-end line
- center： Item 在 cross-axis 的中心
- baseline：对齐 items ，例如根据他们的 baseline 对齐
- stretch (默认) ：拉伸填充 Container   (仍遵循 min-width/max-width)

## align-content

![](./align-content.svg)

> This aligns a flex container's lines within when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.

这个属性用作当 cross-axis 有额外的空间时对齐 Container 的 line，类似 justify-content 对齐 main-axis 中的单个 item。

> Note: this property has no effect when there is only one line of flex items.

注意：当只有一条 flex Item 的 line 时这个属性不起作用。

```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

> - flex-start: lines packed to the start of the container
> - flex-end: lines packed to the end of the container
> - center: lines packed to the center of the container
> - space-between: lines evenly distributed; the first line is at the start of the container while the last one is at the end
> - space-around: lines evenly distributed with equal space around each line
> - stretch (default): lines stretch to take up the remaining space

- flex-start： line 从 Container 的起始位置包装
- flex-end：line 从 Container 的结束位置包装
- center：line 在 Container 的中间包装
- space-between：line 尽可能分散；第一个 line 在 Container 的开始位置最后一个 line 在 Container 的结束位置
- space-around：line 尽可能分散并且彼此之间的空白空间相同
- stretch  (默认)：line 拉伸占据满剩余空间
