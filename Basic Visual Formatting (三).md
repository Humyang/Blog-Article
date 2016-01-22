layout: [post]
title: 文章标题
date: 2016-01-21 15:59:39
tags:
- 标签
categories:
- 分类
- 子分类
---

文章简介

<!-- more -->


---

Basic Visual Formatting (三)

# Block-Level Elements

块级元素

> Block-level elements can behave in both predictable and surprising ways. The handling of element placement along the horizontal and vertical axes can differ, for example. To fully understand how block-level elements are handled, you must clearly understand a number of boundaries and areas. They are shown in detail in Figure 7-2.

块级元素的行为即可预测又有些惊奇，元素位置的处理在水平和垂直轴线的表现有所不同，例如。要完全明白块级元素如何处理，你必须清晰明白几个边界和区域。他们的细节在图 7-2 列出。

![](/images/2016/01/7-2.png)
<small>图 7-2. 完整的盒模型</small>

> In general, the width of an element is defined as the distance from the left inner edge to the right inner edge, and the height is the distance from the inner top to the inner bottom. Both of these properties can be applied to an element.

通常，元素的宽度定义为左内边缘到右内边缘的距离，高度是顶部内边缘到底部内边缘的距离。这些属性都可以应用到元素。

> The various widths, heights, padding, and margins combine to determine how a document is laid out. In most cases, the height and width of the document are automatically determined by the browser and are based on the available display region and other factors. Under CSS, of course, you can assert more direct control over the way elements are sized and displayed. You can select different effects for horizontal and vertical layouts, so we’ll tackle them separately.

这几个宽度，高度，内边距和外边距的组合决定了文档如何布局。大部分情况，文档的高度和宽度是由浏览器和基于可见显示区域和其它因素自动判断。在 CSS 中，当然，你可以直接的控制元素的尺寸和显示方式。你可以为水平和垂直布局选择不同效果，因此我们将这些分开单独来讲。


## Horizontal Formatting

水平格式化

> Horizontal formatting is often more complex than you’d think. Part of the complexity has to do with how width affects the width of the content area, not the entire visible element box. Consider the following example:

水平格式化比你想的还要负责。复杂的部分是处理宽度如何影响内容区域宽度，不是整个可见元素盒子，例如下面的例子：

```html
     <p style="width: 200px;">wideness?</p>
```

> This line of code will make the paragraph’s content 200 pixels wide. If you gave the element a background, this would be quite obvious. However, any padding, bor- ders, or margins you specify are added to the width value. Suppose you do this:

这一行代码设置段落宽度为 200px 宽，如果你设置了元素的背景颜色，那么效果是很明显的。接着，你添加内边距，外边距，边框到段落增大他的宽度值，如：

```html
<p style="width: 200px; padding: 10px; margin: 20px;">wideness?</p>
```

> The visible element box is now 220 pixels wide since you’ve added 10 pixels of padding to the right and left of the content. The margins will now extend another 20 pixels to both sides for an overall element box width of 260 pixels.

元素盒子现在的可见宽度是 220 px，因为分别添加了 10 px 内边距到内容的左边和右边。而外边距拓展了元素盒子 20px 的整体宽度，现在元素盒子的宽度是 260px。


> Understanding the hidden additions to width is critical. Most users think that width refers to the width of the visible element box, and that if they declare an element to have padding, borders, and a width, the value they supply for the width will be the distance from the outer left border edge to the outer right border edge. This is not the case in CSS. Keep this fact firmly in mind to avoid confusion later.

弄清楚隐藏的宽度是至关重要的。大部分使用者认为宽度只是指元素盒子的可见宽度，如果他们声明了一个拥有内边距，边框，和宽度的元素盒子，他们为宽度提供的值是从外左边缘到外右边缘的距离。在 CSS 中不是这样的。请牢记这一点避免在后面的章节产生困惑。

> <small>As of this writing, the Box Model module of CSS includes proposals for ways to let authors choose whether width refers to the content width or the visible box width.</small>

<small>在撰写此书时，CSS 的盒模型模块包含一个提议：能让使用者选择宽度指为内容宽度或盒子可见宽度。</small>


> Almost as simple is the rule that says that the sum of the horizontal components of a block-level element box in the normal flow always equals the width of the parent. Take two paragraphs within a div whose margins have been set to 1em. The content width (the value of width) of the paragraph, plus its left and right padding, borders, and margins, always add up to the width of the div’s content area.

最简单的解释块级元素盒子的规则是在正常流中他的水平部件的宽度总和总是与父元素的宽度相同。把两个段落放到已经设置了外边距为 1em 的 div 中。段落的内容宽度  (宽度的值) ，加上他的左右内边距，边框，和外边距，加起来总是等于 div 的内容区域的宽度。

> Let’s say the width of the div is 30em, making the sum total of the content width, padding, borders, and margins of each paragraph 30em. In Figure 7-3, the “blank” space around the paragraphs is actually their margins. If the div had any padding, there would be even more blank space, but that isn’t the case here. I’ll discuss padding soon.

如果 div 的宽度是 30em，使每个有 30em 宽的段落的内容宽度，内边距，外边距，边框相加。如图 7-3 中，围绕着段落的 “空白” 空间实际上是他们的外边距。如果 div 有内边距，这里将会有更多空白空间，先不在这里介绍，我会在后面讨论内边距时说明。

![](/images/2016/01/7-3.png)
图 7-3. 元素盒子的宽度与他们的父元素一样宽。

### Horizontal properties

水平属性

> The “seven properties” of horizontal formatting are: margin-left, border-left, padding-left, width, padding-right, border-right, and margin-right. These properties, which are diagrammed in Figure 7-4, relate to the horizontal layout of block-level boxes.

水平格式化的 “七个属性”：左外边距，左边框，左内边距，宽度，右内边距，右边框，右外边距。这些属性，在图 7-4，关于块级盒子的水平布局的。

![](/images/2016/01/7-4.png)
图 7-4. 水平格式化的 “七个属性”

> The values of these seven properties must add up to the width of the element’s containing block, which is usually the value of width for a block element’s parent (since block-level elements nearly always have block-level elements for parents).

这七个属性的值一定会添加到元素的容器块的宽度，他通常是块元素的父元素的宽度  (块级元素的上级元素几乎总是块级元素)。

> Of these seven properties, only three may be set to auto: the width of the element’s content and the left and right margins. The remaining properties must be set either to specific values or default to a width of zero. Figure 7-5 shows which parts of the box can take a value of auto and which cannot.

这七个属性，只有三个可能设为 auto：元素的内容的宽度和左右外边距。剩余的属性必须设置为指定值或默认为零的宽度。图 7-5 显示演示盒子的部分哪些可以设置为 auto 哪些不能。

![](/images/2016/01/7-5.png)
图 7-5. 可以设置为 auto 的水平属性

> width must either be set to auto or a nonnegative value of some type. When you do use auto in horizontal formatting, different effects can result.

宽度必须设置为 auto 或某类非负数的值 (marin 可以是负数)。当你在水平格式化使用 auto，会产生不同的效果。

> <small>CSS allows browsers to set a minimum value for width; this is the value below which a block-level element’s width cannot drop. The value of this minimum can vary between browsers, as it is not defined in the specification.</small>

CSS 允许浏览器设置宽度的最小值；这个值能使块级元素的宽度无法抛弃。这个最小值在不同浏览器之间会有变化，因为他不是规范中定义的。

### Using auto

> If you set width, margin-left, or margin-right to a value of auto, and give the remaining two properties specific values, then the property that is set to auto determines the length required to make the element box’s width equal to the parent element’s width. In other words, let’s say the sum of the seven properties must equal 400 pixels, no padding or borders are set, the right margin and width are set to 100px, and the left margin is set to auto. The left margin will be 200 pixels wide:

如果你设置宽度，左外边距或右外边距的值为 auto，并指定剩余的两个属性为指定值，然后设置为 auto 的属性会判断所需要的长度使元素盒子的宽度等于父元素的宽度。换句话说，假设这七个属性的总和为 400 px，不设置内边距或边框，右外边距和宽度设置为 100px,左外边距设置为 auto。那么左外边距的宽度将会是 200px：

```html
p {margin-left: auto; margin-right: 100px;
     width: 100px;}   /* 'auto' left margin evaluates to 200px */
```

> In a sense, auto can be used to make up the difference between everything else and the required total. However, what if all three of these properties are set to 100px and none of them are set to auto?

在某种意义上，auto 可以被用作一切不同的东西之间需要的总和。不过，如果这三个属性都设置为 100px 而不是设置为 auto 呢？

> In the case where all three properties are set to something other than auto—or, in CSS terminology, when these formatting properties have been overconstrained— then margin-right is always forced to be auto. This means that if both margins and the width are set to 100px, then the user agent will reset the right margin to auto. The right margin’s width will then be set according to the rule that one auto value “fills in” the distance needed to make the element’s overall width equal that of its containing block. Figure 7-6 shows the result of the following markup:

这种三个属性除了设置为 auto 之外的情况－或在 CSS 技术中，当这个格式化属性已经超过约束条件－那么右外边距总是强制被设置为 auto。这意味着如果外边距和宽度都设置为 100px，那么用户代理会强制设置右外边距为 auto。右外边距的宽度将依照 “填充” 的规则自动设置一个距离值，使元素的总宽等于包含他的容器块的宽度。图 7-6 显示下面的 html 标记的结果：

```html
  p {margin-left: 100px; margin-right: 100px;
       width: 100px;}   /* right margin forced to be 200px */
```

![](/images/2016/01/7-6.png)
图 7-6. 覆盖右外边距的设置

> <small>margin-right is forced to be auto only for left-to-right languages such as English. In right-to-left languages, everything is reversed, so margin-left is forced to be auto, not margin-right.</small>

强制设置右外边距为 auto 只发生在从左到右的语言例如英语。在右到左的语言，所有都是相反，例如强制左外边距为 auto，而不是右外边距。

> If both margins are set explicitly, and width is set to auto, then the value of width will be set to whatever value is needed to reach the required total (which is the content width of the parent element). The results of the following markup are shown in Figure 7-7:

如果所有外边距都设置了明确值，而宽度设置为 auto，那么宽度的值会被设置为达到总宽所需要的大小  (父元素的内容宽度)。下面的标记的结果在图 7-7 ：

```html
     p {margin-left: 100px; margin-right: 100px; width: auto;}
```

![](/images/2016/01/7-7.png)
图 7-7. 自动宽度

> The case shown in Figure 7-7 is the most common since it is equivalent to setting the margins and not declaring anything for the width. The result of the following markup is exactly the same as that shown in Figure 7-7:

图 7-7 的例子是最常用的方式他相当于设置了外边距并没声明任何宽度。下面的标记的结果也会产生图 7-7 的效果。

```html
     p {margin-left: 100px; margin-right: 100px;} /* same as before */
```
