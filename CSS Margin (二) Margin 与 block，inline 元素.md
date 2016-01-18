CSS Margin (二) Margin 与 block，inline 元素

# Margin

## HTML 元素类型


HTML 有两种基本元素，即 block 和 inline。

block 元素占据一行，inline 元素与其它 inline 元素占据统同一行。




### Replaced element

除了上面两种基本类型外，Replaced element 也是常用的元素类型。

在 MDN 是这样介绍 Replace element 的：

> In CSS, a replaced element is an element whose representation is outside the scope of CSS. These are kind of external objects whose representation is independent of the CSS.
> 
> 在 CSS 中，replaced element 拥有 CSS 范围之外的属性 (例如 `img` 的 width 和 height 属性)，这是一种独立于 CSS 的拓展对象。

另外，使用 CSS 的 `content` 属性插入的元素也是一个匿名的 Replaced element (anonymous replaced elements)。

Replaced element 与 inline element 对应 (即 inline element 是 non-replaced element)，它与 inline element  的区别是：这些元素拥有内在尺寸(intrinsic dimensions),他们可以设置 width/height 属性。他们的性质同设置了 `display:inline-block` 的元素一致。

## Margin 与 HTML 元素类型

### Margin 与 Block element

margin 在块级元素下，他的性能可以完全体现，上下左右任你设定。且记住块级元素的 margin 的参照基准是前一个元素即相对于自身之前的元素有 margin 距离。如果元素是第一个元素，则就是相对于父元素的 margin 距离（但第一个元素相对于父元素 margin-top 而父元素又没有设定 padding-top/border-top 的话要需要印证上垂直外边距合并的知识)。

### Margin 与 Inline element

margin 也能用于内联元素，这是规范所允许的，但是 margin-top 和 margin-bottom 对内联元素（对行）的高度没有影响，并且由于边界效果(margin 效果)是透明的，他也没有任何的视觉影响。

这时因为边界应用于内联元素时**不改变元素的行高度**，如果你要改变内联元素的行高即类似文本的行间距，那么你只能使用这三个属性：`line-height`，`fong-size`，`vertical-align`。请记住，这个影响内联元素高度的是line-height而不是height，因为内联元素是一行行的，定一个height的话，那这到底是整段inline元素的高呢？还是inline元素一行的高呢？这都说不准，所以统一都给每行定一个高，只能是line-height了。

### Margin 与 Replace element

因为 replace element 相当于 inline-block，所以 Margin 的上下左右都有效果。


## HTML 元素类型参考
[block 元素:](https://developer.mozilla.org/en/docs/Web/HTML/Block-level_elements)

```html
<address>
Contact information.
<article> HTML5
Article content.
<aside> HTML5
Aside content.
<blockquote>
Long ("block") quotation.
<canvas> HTML5
Drawing canvas.
<dd>
Definition description.
<div>
Document division.
<dl>
Definition list.
<fieldset>
Field set label.
<figcaption> HTML5
Figure caption.
<figure> HTML5
Groups media content with a caption (see <figcaption>).
<footer> HTML5
Section or page footer.
<form>
Input form.
<h1>, <h2>, <h3>, <h4>, <h5>, <h6>
Heading levels 1-6.
<header> HTML5
Section or page header.
<hgroup> HTML5
Groups header information.
<hr>
Horizontal rule (dividing line).
<li>
List item.
<main>
Contains the central content unique to this document.
<nav>
Contains navigation links.
<noscript>
Content to use if scripting is not supported or turned off.
<ol>
Ordered list.
<output> HTML5
Form output.
<p>
Paragraph.
<pre>
Preformatted text.
<section> HTML5
Section of a web page.
<table>
Table.
<tfoot>
Table footer.
<ul>
Unordered list.
<video> HTML5
Video player.
```

[inline 元素:](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)

```html
b, big, i, small, tt
abbr, acronym, cite, code, dfn, em, kbd, strong, samp, time, var
a, bdo, br, img, map, object, q, script, span, sub, sup
button, input, label, select, textarea
```

[Replaced element:](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element)

```html
 Typical replaced elements are <img>, <object>, <video>
 form elements like <textarea> and <input>
 Some elements, like <audio> or <canvas> 
```