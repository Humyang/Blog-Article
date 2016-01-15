# CSS 布局之 Formatting Context (一) Block Formatting Context

首先来了解什么是 Formatting Context。


Formatting Context 是页面中的一块渲染区域，在这个区域内拥有它自己的渲染规则，决定了子元素如何定位，及元素之间如何相互作用。

不同的 Formatting Context 有不同的渲染规则，常见的有 `BFC` (Block Formatting Contextext)，`IFC` (Inline Formatting Context)，和 CSS 3 新增加的 `GFC` (Grid Formatting Context)，`FFC` (Flex Formatting Context)。 

与 Formatting Context 息息相关的是 Box，每个 HTML 元素作为 Box 通过 CSS 渲染，不同的类型的 Box 有不同的行为，CSS 中有两种 Box：Block 和 Inline，[这里有介绍]()。

## BFC

BFC 就是只有 Block-level Box 参与的 Formatting Context。它是一个独立的渲染区域，它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相干。


### 哪些元素会生成 BFC

以前我一直不知道有 Formatting Context 这个概念，以为 Box 负责了 Formatting Context 的职责，但这也说明了 Formatting Context 不用手动创建也会出现，那么它出现的规则是什么呢，或者说哪些元素会生成 BFC？

这些元素会生成 BFC：

> * the root element or something that contains it
> * floats (elements where float is not none)
> * absolutely positioned elements (elements where position is absolute or fixed)
> * inline-blocks (elements with display: inline-block)
> * table cells (elements with display: table-cell, which is the default for HTML table cells)
> * table captions (elements with display: table-caption, which is the default for HTML table captions)
> * elements where overflow has a value other than visible
> * flex boxes (elements with display: flex or inline-flex)

* root 元素或一些包含它的元素。
* floats 元素 (元素的 float 值不为 none)
* absolutely 定位的元素 (元素的 position 值是 absolute 或 fixed)
* inline-block 元素 (元素的 display 为 inline-block)
* table cell 元素 (元素的 display 为 table-cell, 它是HTML 的 table cell 的默认值)
* table captions (元素的 display 值为 table-caption,它是 HTML table captions 的默认值)
* 元素的 overflow 有非 visible 的值
* flex boxes (元素的 display 为 flex 或 inline-flex)

Block Formatting Context 包含创建它的元素的所有内部元素，但不包含会创建新的 Block Formatting Context 的后裔元素。

### BFC 的规则

Block Formatting Context 对于 positioning (见 [float](https://developer.mozilla.org/en-US/docs/Web/CSS/float)) 和 clear (见 [clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear)) 非常重要，这些规则只会在同一个 Block Formatting 中应用。

Floats 不会影响其它 block formatting context 的布局，clear 也只会清除同一个 block formatting context 的 float。


这里是其它博客看到的一个总结：

* 内部的Box会在垂直方向，一个接一个地放置。
* Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
* 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
* BFC的区域不会与float box重叠。
* BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
* 计算BFC的高度时，浮动元素也参与计算


## 参考资料

https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Visual_formatting_model#Block-level_elements_and_block_boxes

http://www.cnblogs.com/liugblog/p/4982684.html