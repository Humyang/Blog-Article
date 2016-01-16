# Basic Visual Formatting

## The Containing Block

> Every element is laid out with respect to its containing block; in a very real way, the containing block is the “layout context” for an element. CSS2.1 defines a series of rules for determining an element’s containing block. I’ll cover only those rules that pertain to the concepts covered in this chapter and leave the rest for future chapters.

每个元素的布局规则都遵循所包含它的容器块；容器块是元素的布局上下文。CSS 2.1 为元素的容器块定义了几种规则。这个章节我会介绍覆盖这些规则的概念，其余的留给以后的章节。

> For an element in the normal, Western-style flow of text, the containing block is formed by the content edge of the nearest block-level, table cell, or inline-block ancestor box. Consider the following markup:

正常情况下的元素，西式的文本，容器块从最近的 block-level，table cell，或 inline-block 祖先 box 的内容的边缘形成，参考下面的标记：

```html
<body> <div>
       <p>This is a paragraph.</p>
      </div>
</body>
```

> In this very simple example, the containing block for the p element is the div element, as that is the closest ancestor element that is block-level, a table cell, or inline-block (in this case, it’s a block box). Similarly, the div’s containing block is the body. Thus, the layout of the p is dependent on the layout of the div, which is in turn dependent on the layout of the body.

在这个非常简单的例子中，p 元素的容器块是 div 元素，因为它最近的祖先元素是 block-level.table cell，或 inline-block (在这个例子中，它是块级盒子)。同理，div 元素的容器块是 body，因此，p 元素的布局是依赖 div 元素，div 元素又反过来以来 body 元素。

> You don’t need to worry about inline elements since the way they are laid out doesn’t depend directly on containing blocks. We’ll talk about them later in the chapter.

你不需要担心 inline 元素的布局方式是否直接以来容器块。我会在之后的章节谈论它们。

## A Quick Refresher

> Let’s quickly review the kinds of elements we’ll be discussing, as well as some important terms that are needed to follow the explanations in this chapter:

让我们快速预览我们将会谈论到的元素的种类，以及一些重要的术语，可以在这个章节查询。

### Normal flow

正常流

> The left-to-right, top-to-bottom rendering of text in Western languages and the familiar text layout of traditional HTML documents. Note that the flow direction may be changed in non-Western languages. Most elements are in the normal flow, and the only way for an element to leave it is to be floated or positioned (covered in Chapter 10). Remember, the discussions in this chapter cover only elements in the normal flow.

从左到右，顶部到底部渲染西方语言文字和传统 HTML 文档的文字布局。注意流的方向可以通过更改以非西方语言的方式渲染。大部分元素都是正常流，只有设置元素为浮动或 position 才能脱离 (在第 10 章讨论)。


### Nonreplaced element

非替代元素

> An element whose content is contained within the document. For example, a paragraph is a nonreplaced element because its textual content is found within the element itself.

元素的内容包含在文档内。例如段落 (`<p>`) 是非替代元素因为它的文本内容在元素自身内。

### Replaced element

替代元素

> An element that serves as a placeholder for something else. The classic example of a replaced element is the img element, which simply points to an image file that is then inserted into the document’s flow at the point where the img element itself is found. Most form elements are also replaced (e.g., <input type="radio">).

元素起类似占位符作用的。典型的替代元素是 img 元素，它简单的指向一个图像文件然后插入到文档流中 img 元素所在的位置。大部分 form 元素也是替代元素。

### Block-level element

块级元素

> An element such as a paragraph, heading, or a div. These elements generate “new lines” both before and after their boxes when in the normal flow, so that block-level elements in the normal flow stack vertically. An element can be made to generate a block-level box by declaring display: block.

如段落，标题，或 div 元素。当这些元素处于正常流时会在它们的前后盒子之间生成 “新行”，因此块级元素在正常流中垂直的堆放。元素可以通过 display:block 让自己生成块级盒子。

### Inline element

内联元素

> An element such as strong or span. These elements do not generate “line breaks” before or after themselves, and they are descendants of a block-level element. You can cause an element to generate an inline-level box by declaring display: inline.

如 strong 或 span 元素。这些元素不会在它们之前或之后生成 “换行符”，并且它们是块级元素的后代。你可以使用 display:inline 为元素生成内联级盒子。

### Root element

根元素

> The element at the top of the document tree. In HTML documents, this is the element html. In XML documents, it can be whatever the language permits.

在文档树顶端的元素。在 HTML 文档中，它是 `<html>` 元素。在 XML 文档，它可以是语言许可。
