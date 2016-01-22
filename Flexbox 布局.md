# Background

> The Flexbox Layout (Flexible Box) module (currently a W3C Last Call Working Draft) aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word "flex").

Flexbox 布局  (Flexible 盒子) 模块  (W3C 当前的最终草案)  皆在提供更灵活的布局方式，为容器中的项目对齐和分配空间，即使他们的尺寸是未知的或者动态的  (因此他们叫做 flex)。

> The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate to all kind of display devices and screen sizes). A flex container expands items to fill available free space, or shrinks them to prevent overflow.

flex 布局背后的主要想法是能让容器可以更改他的 “项目” 的宽度/高度  (或顺序)，获取最合适的可用空间  (尽可能容纳所有设备和屏幕尺寸)。flex 容器拓展它的项目适应所有可用空间，或收缩他们防止益出。

> Most importantly, the flexbox layout is direction-agnostic as opposed to the regular layouts (block which is vertically-based and inline which is horizontally-based). While those work well for pages, they lack flexibility (no pun intended) to support large or complex applications (especially when it comes to orientation changing, resizing, stretching, shrinking, etc.).

最重要的，flexbox 布局是与方向无关的不是常规的布局  (块元素布局是基于垂直方向而内联元素基于水平方向)。虽然他们在页面能良好的工作，但他们缺少一些灵活性  (不是双关) 支持大型或复杂的应用程序   (特别是当他面对页面方向更改，缩放，拉伸，收缩等)。

> Note: Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.

注意：Flexbox 布局最适合用到应用程序的组件，和小规模布局，而 Grid 布局更适合大规模布局。



# Basics & Terminology

> Since flexbox is a whole module and not a single property, it involves a lot of things including its whole set of properties. Some of them are meant to be set on the container (parent element, known as "flex container") whereas the others are meant to be set on the children (said "flex items").

因为 flexbox 是一个完整的模块，他不仅仅只有一个属性，他涉及到大量包含整个属性集的操作。他们之中一些用作操作容器  (父元素，例如 “flex container”) 而其他一些用来操作子元素  (成为 “flex items”)。

> If regular layout is based on both block and inline flow directions, the flex layout is based on "flex-flow directions". Please have a look at this figure from the specification, explaining the main idea behind the flex layout.

如果传统布局是基于块和内联流方向，那么 flex 布局则基于 “flex-flow 方向”。请看下图，图中指明了规范，解释了 flex 布局背后的思想。

![](/images/2016/01/flexbox.png)

> Basically, items will be laid out following either the main axis (from main-start to main-end) or the cross axis (from cross-start to cross-end).

基本上，项目将会随着 main axis 布局 (从 main-start 到 main-end) 或 cross axis  (从 cross-start 到 cross-end)。  

> - main axis - The main axis of a flex container is the primary axis along which flex items are laid out. Beware, it is not necessarily horizontal; it depends on the flex-direction property (see below).
> - main-start | main-end - The flex items are placed within the container starting from main-start and going to main-end.
> - main size - A flex item's width or height, whichever is in the main dimension, is the item's main size. The flex item's main size property is either the ‘width’ or ‘height’ property, whichever is in the main dimension.
> - cross axis - The axis perpendicular to the main axis is called the cross axis. Its direction depends on the main axis direction.
> - cross-start | cross-end - Flex lines are filled with items and placed into the container starting on the cross-start side of the flex container and going toward the cross-end side.
> - cross size - The width or height of a flex item, whichever is in the cross dimension, is the item's cross size. The cross size property is whichever of ‘width’ or ‘height’ that is in the cross dimension.

- main axis - flex 容器的主轴是基础的轴线，容器内的项目沿着这条轴线布局。但注意，他不是必须为水平的；他以来与 flex-direction 属性  (见下面)。
- main-start | main-end - 容器内的 flex 项的位置从 main-start 开始到 main-end 结束。
- main size - flex 项的宽度或高度，无论他是否处于主尺寸，他都是项的主要尺寸。flex 项的主要尺寸属性是 ‘width’ 或 ‘height’，无论是否处于主尺寸。
- cross axis - 与主轴垂直的轴线成为 cross axis，他的方向依赖主轴的方向。
- cross-start  | cross-end - 这个线条指示如何填充容器内的项，从 cross-start 开始到 cross-end 结束。
- cross size - flex 项的宽度和高度，无论是否处在 cross 尺寸，他是项的 cross size。cross size 属性无论是 ‘width’ 或 ‘height’ 都是在 cross dimension。

# Properties for the Parent (flex container)

![](/images/2016/01/flex-container.svg)

```css

.container {
  display: flex; /* or inline-flex */
}

```

## display



> This defines a flex container; inline or block depending on the given value. It enables a flex context for all its direct children.

将元素定义为 flex 容器；是内敛或块级依赖给定值。他使他的所有直接子级变成 flex 上下文。

> Note that CSS columns have no effect on a flex container.

注意 CSS 列在不影响 flex 容器。

## flex-direction

![](/images/2016/01/flex-direction1.svg)

> This establishes the main-axis, thus defining the direction flex items are placed in the flex container. Flexbox is (aside from optional wrapping) a single-direction layout concept. Think of flex items as primarily laying out either in horizontal rows or vertical columns.

这个属性构建了 main-axis，因此定义 flex 项的属性放到了 flex 容器中。Flexbox 是 (除了可选的 wrapping) 单方向的概念。记着 flex 项的基础布局也可以是水平的行垂直的列。



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

![](/images/2016/01/flex-wrap.svg)

```css
.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

> By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property. Direction also plays a role here, determining the direction new lines are stacked in.

默认，flex 项首先会尝试将所有放置在一行。你可以更改这个属性使项根据需要环绕。方向在这里也起到一定作用，确定新的线条的叠加方向。

> - nowrap (default): single-line / left to right in ltr; right to left in rtl
> - wrap: multi-line / left to right in ltr; right to left in rtl
> - wrap-reverse: multi-line / right to left in ltr; left to right in rtl

- nowrap  (默认)：单行 / 左到右  (ltr)；右到左 (rtl)
- wrap：多行 / 左到右  (ltr)；右到左  (rtl)
- wrap-reverse：多行 / 右到左  (ltr)；左到右  (rtl)       

## flex-flow (Applies to: parent flex container element)

> This is a shorthand flex-direction and flex-wrap properties, which together define the flex container's main and cross axes. Default is row nowrap.

flex-direction 和 flex-wrap 属性的缩写，集中定义 flex 容器的 main 和 cross 轴。默认值是 row nowrap。

```css

flex-flow: <‘flex-direction’> || <‘flex-wrap’>

```

## justify-content

![](/images/2016/01/justify-content.svg)

> This defines the alignment along the main axis. It helps distribute extra free space left over when either all the flex items on a line are inflexible, or are flexible but have reached their maximum size. It also exerts some control over the alignment of items when they overflow the line.

定义 main 轴的对齐方式。当线上的 flex 项不够灵活或者都很灵活但达到他们的最大尺寸，这个属性帮助分配额外的自由空间。当项超出了线的范围他还可以帮忙控制对齐。

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

- flex-start  (默认)：项从开始线起包装
- flex-end：项从结束线起包装
- center：项从线中心开始
- space-between：项尽可能占满线，第一个项在开始线，最后一个项在结束线
- space-around：项尽可能占满线并且彼此之间的距离相同。注意看起来是不相同的，因为所有的项都有相同的空间在两侧。第一个项相对于容器只有一个单位的空间，但距离下一个项有两个单位的空间因为下一个项也有自己的单位空间。


## align-items

![](/images/2016/01/align-items.svg)

> This defines the default behaviour for how flex items are laid out along the cross axis on the current line. Think of it as the justify-content version for the cross-axis (perpendicular to the main-axis).

定义 flex 项在当前线如何沿着 cross aix 布局的默认行为。可以认为他是 justify-content 的 cross-axis 版本  (垂直于 main-axis)。

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

- flex-start：项的 cross-start 外边距边缘放到 cross-start line
- flex-end：item 的 cross-end 外边距放置到 cross-end line
- center：项在 cross-axis 的中心
- baseline：对齐 items ，例如根据他们的 baseline 对齐
- stretch (默认) ：拉伸填充容器  (仍遵循 min-width/max-width)

## align-content

![](/images/2016/01/align-content.svg)

> This aligns a flex container's lines within when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.

这个属性用作当 cross-axis 有额外的空间时对齐容器的 line，类似 justify-content 对齐 main-axis 中的单个 item。

> Note: this property has no effect when there is only one line of flex items.

注意：当只有一条 flex 项的 line 时这个属性不起作用。

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

- flex-start： line 从容器的起始位置包装
- flex-end：line 从容器的结束位置包装
- center：line 在容器的中间包装
- space-between：line 尽可能分散；第一个 line 在容器的开始位置最后一个 line 在容器的结束位置
- space-around：line 尽可能分散并且彼此之间的空白空间相同
- stretch  (默认)：line 拉伸占据满剩余空间


# Properties for the Children (flex items)

![](/images/2016/01/flex-items.svg)

## order

![](/images/2016/01/order-2.svg)

> By default, flex items are laid out in the source `order`. However, the order property controls the order in which they appear in the flex container.

flex 项默认安装源代码顺序排序。而 `order` 属性可以控制他们出现在 flex 容器的顺序。

```css
.item {
  order: integer;
}
```

## flex-grow

![](/images/2016/01/flex-grow.svg)

> This defines the ability for a flex item to grow if necessary. It accepts a unitless value that serves as a proportion. It dictates what amount of the available space inside the flex container the item should take up.

可以使用这个属性根据需要扩大 flex 项。他接受无单位的值作为比例。他根据比例将 flex 容器可用的空间分配给 flex 项。

> If all items have flex-grow set to 1, the remaining space in the container will be distributed equally to all children. If one of the children a value of 2, the remaining space would take up twice as much space as the others (or it will try to, at least).

如果所有的项的 flex-grow 属性设置为 1，容器剩余的空间将会平均分配给 flex 项。如果一个值是 2，剩余的空间将会为此项分配多其他项一倍的空间  (会进行尝试)。

```css
.item {
  flex-grow: <number>; /* default 0 */
}
```

> Negative numbers are invalid.

负数是无效的。

## flex-shrink

> This defines the ability for a flex item to shrink if necessary.

根据需要缩小 flex 项。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

> Negative numbers are invalid.

负数是无效的。

## flex-basis

> This defines the default size of an element before the remaining space is distributed. It can be a length (e.g. 20%, 5rem, etc.) or a keyword. The `auto` keyword means "look at my width or height property" (which was temporarily done by the `main-size` keyword until deprecated). The `content` keyword means "size it based on the item's content" - this keyword isn't well supported yet, so it's hard to test and harder to know what it's brethren `max-content`, `min-content`, and `fit-content` do.

分配空间之前定义元素的默认尺寸。他可以是一个长度  (如 20%，5rem 等) 或关键字。关键字 `auto` 意味着 “根据我的 width 或 height 属性”  (曾经临时是用关键字 `main-size`，现在已被弃用)。 关键字 `content` 意味着 “尺寸是基于项的内容” - 这个关键字不是很好的被支持，因此他很难测试并且更难知道他的哪些兄弟有效果：`max-content`,`min-content` 和 `fit-content`。

```css
.item {
  flex-basis: [length] | auto; /* default auto */
}
```

> If set to `0`, the extra space around content isn't factored in. If set to `auto`, the extra space is distributed based on its `flex-grow` value. See this graphic.

如果设置为 `0`，内容的额外空间不回算上。如果设置为 `auto`，额外空间的分发基于他的 `flex-grow` 值。见此图：

![](/images/2016/01/rel-vs-abs-flex.svg)

## flex

> This is the shorthand for `flex-grow`, `flex-shrink` and `flex-basis` combined. The second and third parameters (`flex-shrink` and `flex-basis`) are optional. Default is `0 1 auto`.

这是 `flex-grow`,`flex-shrink` 和 `flex-basis` 组合的缩写。第二和第三个参数是可写的。默认是 `0 1 auto`。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

**It is recommended that you use this shorthand property** rather than set the individual properties. The short hand sets the other values intelligently.

**推荐使用这个缩写属性** 而不要使用单个属性。这个缩写设置值更加智能。

## align-self

![](/images/2016/01/align-self.svg)

> This allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.

使单个 flex 项可以覆盖默认的对齐方式  (或通过 `align-items` 指定一个)。

> Please see the `align-items` explanation to understand the available values.

请参照 `align-items` 了解可用值。

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

> Note that `float`, `clear` and `vertical-align` have no effect on a flex item.

注意 `float`，`clear`，和 `vertical-align` 在 flex 项 没有效果。
