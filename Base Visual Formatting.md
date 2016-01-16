来自 CSS The Definitive Guide Eric A Meyer。

# Base Visual Formatting

> In the previous chapters, we covered a great deal of practical information on how CSS handles text and fonts in a document. In this chapter, we’ll look at the theoretical side of visual rendering, answering many of the questions we skipped earlier in the interest of addressing how CSS is implemented.

在之前的章节，我们进行了大量的实践用 CSS 处理文字和文档的字体。在这章中，我们会学习外观呈现的理论，回答许多之前跳过的许多 CSS 如何实现的问题。
> Why is it necessary to spend an entire chapter on the theoretical underpinnings of visual rendering in CSS? The answer is that with a model as open and powerful as that contained within CSS, no book could hope to cover every possible way of combining properties and effects. You will obviously go on to discover new ways of using CSS for your own document effects.

为什么需要花费一整章在 CSS 视觉呈现的理论基础？因为它是开发的模式和强大的 CSS 容器，没有任何一本书可以覆盖所有属性组合的效果。明显你需要探索新的方式使用 CSS，实现你想要的效果。
> In the course of exploring CSS, you may encounter seemingly strange behaviors in user agents. With a thorough grasp of how the visual rendering model works in CSS, you’ll be able to determine whether a behavior is a correct (though unexpected) consequence of the rendering engine CSS defines, or whether you’ve stumbled across a bug that needs to be reported.

在探索 CSS 的过程中，你可能在 user agents 遇到看似奇怪的行为。深入的理解和掌握 CSS 中工作的视觉呈现模型，你就可以判断在哪些行为可以在 CSS 渲染引擎获取正确结果 (尽管看起来奇怪)，或者你偶然遇到一个需要提交的 bug。

## Basic Boxes
> CSS assumes that every element generates one or more rectangular boxes, called element boxes. (Future versions of the specification may allow for nonrectangular boxes, but for now everything is rectangular.) Each element box has a content area at its core. The content area is surrounded by optional amounts of padding, borders, and margins. These items are considered optional because they could all be set to a width of zero, effectively removing them from the element box. An example content area is shown in Figure 7-1, along with the surrounding regions of padding, border, and margins.

CSS 假设所有元素都会生成一个或多个矩形盒子，称为元素盒子 (未来的版本可能允许不规则形状的盒子，但现在所有都是矩形)。每一个元素盒子在它的核心都有一个内容区域。这个内容区域被可选的 padding，border，和 margin 包围。这些选项是可选的因为它们的宽度全都可以被设置为 0，有效的将它们从元素盒子移除。一个元素的内容区域如图 7-1 所示，围绕它的是 padding,border,和 margins 的区域。

图 7-1
![](./7-1.png)
> Each of the margins, borders, and padding can be set using various properties, such as margin-left or border-bottom. The content’s background a color or tiled image, for example is also applied to the padding. The margins are always transparent, revealing the background of any parent elements. Padding cannot be a negative value, but margins can. We’ll explore the effects of negative margins later in this chapter.

每个 margin，border，和 padding 可以使用单独的属性设置，例如 margin-left 或 border-bottom。内容的背景颜色或背景图像，也会应用到 padding。而 margin 总是透明的，露出父元素的背景颜色。Padding 不能是负值，但 margin 可以。我们会在后面的章节探索负 margin 的效果。
> Borders are generated using defined styles, such as solid or inset, and their colors are set using the border-color property. If no color is set, then the border takes on the foreground color of the element’s content. For example, if the text of a paragraph is white, then any borders around that paragraph will be white unless the author explicitly declares a different border color. If a border style has gaps of some type, then the element’s background is visible through those gaps. In other words, the border has the same background as the content and padding. Finally, the width of a border can never be negative.

border 使用自定义的样式生成，例如 solid 或 inset，它们的颜色使用 border-color 属性设置。如果没设置颜色，border 会使用元素内容的前景色。例如段落的文字是白色，那么 border 也会是白色除非作者明确指定了不同的 border 颜色。如果 border 的样式会出现一些缺口，那么元素背景会在通过这些缺口可见。换句话说，border 有一部分背景是内容和 padding。最后，border 的宽度永远不能是负数。

> The various components of an element box can be affected by a number of properties, such as width or border-right. Many of these properties will be used in this chapter, even though we haven’t discussed them yet. The actual property definitions are given in Chapter 8, which builds on the concepts set forth in this chapter.

元素盒子的各个部分可以被几个属性影响，例如 width 或 border-right。在这章我们会用到许多这些属性，尽管我们没有讨论过它们。实际上第 8 章才会探索它们，我们先在这一章了解它的概念。

> You will, however, find differences in how various types of elements are formatted. Block-level elements are treated differently than inline-level elements, while floated and positioned elements have their own ways of behaving.

最后你会发现几个不同类型元素的格式的不同。Block 级别元素与 inline-level 元素的区别，浮动元素 (float) 和定位元素 (positioned) 它们自己的行为。