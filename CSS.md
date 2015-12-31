layout: [post]
title: "CSS"
date: 2015-11-15 04:46:06
tags: 
- 前端
categories: 
- 前端
- CSS
id: "fontCSS"
---

W3SCHOOL 的基础 CSS 教程。

<!-- more -->


---

[原文地址](http://www.w3schools.com/css/default.asp)

# CSS

## CSS Background

CSS background properties 用做定义元素的背景效果。

CS properties 使用了下面的背景效果：

* background-color
* background-image
* background-repeat
* background-attachment
* background-position

### Background-color

`background-color` 指定元素的背景颜色。

```css
body {
    background-color: #b0c4de;
}
```

在 CSS 中，颜色通常由下面的方式指定：

* a HEX value - like "#ff0000"
* an RGB value - like "rgb(255,0,0)"
* a valid color name - like "red"

[CSS Color Values](http://www.w3schools.com/cssref/css_colors_legal.asp) 列出了完整的颜色值列表。

### Background Image

`background-image` 指定元素的背景图像。

默认图像是重复的直到覆盖整个元素。

```css
body {
    background-image: url("paper.gif");
}
```

#### Repeat Horizontally or Vertically

`background-image` 属性默认是垂直与水平重复的。

有的图像只想水平或垂直重复，使效果更好。

可以通过下面的方式指定为垂直重复：

```css
body {
    background-image: url("gradient_bg.png");
    background-repeat: repeat-x;
}
```

`background-repeat: repeat-y;` 设置水平重复。


#### Set position and no-repeat

使用 `background-repeat: no-repeat;` 禁止图像重复。

使用 `background-position: right top;` 设置图像在背景中的定位。

#### Fixed position

要使图像的位置固定，不根据滚动条而改变，使用 `background-attachment` 属性。

[example](http://www.w3schools.com/css/tryit.asp?filename=trycss_background-image_attachment)

```css
body {
    background-image: url("img_tree.png");
    background-repeat: no-repeat;
    background-position: right top;
    background-attachment: fixed;
}
```


#### Shorthand property

The shorthand property for background is `background`:

```css
body {
    background: #ffffff url("img_tree.png") no-repeat right top;
}
```

When using the shorthand property the order of the property values is:

* background-color
* background-image
* background-repeat
* background-attachment
* background-position


Property	 | Description
------------- | -------------
[background](http://www.w3schools.com/cssref/css3_pr_background.asp)	 | Sets all the background properties in one declaration
[background-attachment](http://www.w3schools.com/cssref/pr_background-attachment.asp)	 | Sets whether a background image is fixed or scrolls with the rest of the page
[background-color](http://www.w3schools.com/cssref/pr_background-color.asp)	 | Sets the background color of an element
[background-image](http://www.w3schools.com/cssref/pr_background-image.asp)	 | Sets the background image for an element
[background-position](http://www.w3schools.com/cssref/pr_background-position.asp)	 | Sets the starting position of a background image
[background-repeat](http://www.w3schools.com/cssref/pr_background-repeat.asp)	 | Sets how a background image will be repeated

## CSS Text

### Text Color

`color` 用做设置文本的颜色。

在 CSS 中 `color` 通常通过下面的方式指定：

* a HEX value - like "#ff0000"
* an RGB value - like "rgb(255,0,0)"
* a color name - like "red"

 [CSS Color Values](http://www.w3schools.com/cssref/css_colors_legal.asp) 列出了完整的颜色值。

>  Note: For W3C compliant CSS: If you define the color property, you must also define the background-color property.
 

### Text Alignment

`text-align` 指定文本的水平对齐方式。

A text can be **left** or **right** aligned, **centered**, or **justified**.

**left** alignment is **default** if text direction is **left-to-right**, and right alignment is default if text direction is right-to-left

当 `text-align` 被指定为 "justify" 时，每一行都会拉伸因此每一行都等宽，并且每一行的左和右 margin 都相等。(效果就像报纸或杂志)。

### Text Decoration

`text-decoration` 用做设置或移除文本的装饰样式。 

`text-decoration: none;` 通常用做移除链接的下划线。

`text-decoration` 其它值用做装饰文本。

```css

h1 {
    text-decoration: overline;
}

h2 {
    text-decoration: line-through;
}

h3 {
    text-decoration: underline;
}

```

### Text Transformation

`text-transform` 属性用做指定文本字母为大写或小写

它可以用做指定所有字母转换为大写，使用 `uppercase` 或 `lowercase`，或使用 `capitalize` 指定每个单词的首字母为大写。

```css
p.uppercase {
    text-transform: uppercase;
}

p.lowercase {
    text-transform: lowercase;
}

p.capitalize {
    text-transform: capitalize;
}
```

### Text Indentation

`text-indent` 用于指定文本的首行缩进。

```css
p {
    text-indent: 50px;
}
```

### Letter Spacing

`letter-spacing` 属性用做指定文本中字母之间的距离。

```css
h1 {
    letter-spacing: 3px;
}

h2 {
    letter-spacing: -3px;
}
```

### Line Height

`line-height` 属性用做指定两行之间的距离：

```css
p.small {
    line-height: 0.8;
}

p.big {
    line-height: 1.8;
}
```

### Text Direction

`direction` 属性用做更改元素的文字方向。

```css
div {
    direction: rtl;
}
```

### Word Spacing

`word-spacing` 用做指定文本中文字之间的空间距离。

```css

h1 {
    word-spacing: 10px;
}

h2 {
    word-spacing: -5px;
}

```



### All CSS Text Properties

Property | Description
------------- | -------------
color	 | Sets the color of text
direction	 | Specifies the text direction/writing direction
letter-spacing | 	Increases or decreases the space between characters in a text
line-height | 	Sets the line height
text-align | 	Specifies the horizontal alignment of text
text-decoration | 	Specifies the decoration added to text
text-indent | 	Specifies the indentation of the first line in a text-block
text-shadow | 	Specifies the shadow effect added to text
text-transform | 	Controls the capitalization of text
unicode-bidi | 	Used together with the direction property to set or return whether the text should be overridden to support multiple languages in the same document
vertical-align | 	Sets the vertical alignment of an element
white-space | 	Specifies how white-space inside an element is handled
word-spacing | 	Increases or decreases the space between words in a text


## CSS Fonts

The CSS font properties define the font family, boldness, size, and the style of a text。

### Font Family

使用 `font-family` 设置 text 的 font family。

`font-family` 应当保留几个字体名称作为 “回退” 系统。如果浏览器不支持首选字体，会选择第二个字体，依此类推。

从你最想设置的开始指定到通用家族字体，让浏览器可以选择其它相似的字体代替，在没有可选的字体时。

如果 font family 超过一个，则需要用 `,` 区分，font family 必须由 `"` 包裹：

```css
p {
    font-family: "Times New Roman", Times, serif;
}
```

要获取常用的字体组合，可以查阅 [Web Safe Font Combinations](http://www.w3schools.com/cssref/css_websafe_fonts.asp)。

### Font Style

`font-style` 是最常用用做指定斜体文本。

该属性有三个值：

* normal - The text is shown normally
* italic - The text is shown in italics
* oblique - The text is "leaning" (oblique is very similar to italic, but less supported)

### Font Size

`font-size` 属性设置文本的尺寸。

管理文本的尺寸在 web design 中很重要。并且，你不应该使用 font size 调整 paragraphs 使其看起来像 heading，或使 heading 看起来像 paragraphs。

应该始终使用 `<h1> - <h6>` 作为 heading 和 `<p>` 作为 paragraphs。

font-size 的值可以是 absolute，或者 relative size。

Absolute size:

* 设置文本为指定尺寸
* 在所有浏览器中禁止用户更改文字尺寸 (不良好的可访问性得原因)
* Absolute 尺寸了解输出设备的物理尺寸时很好用

Relative size:

* 相对周围元素的设置尺寸
* 允许用户在浏览器中更改尺寸

> 注意：如果你不指定 font size，则是正常文本的默认尺寸，例如 paragraphs，是 16px (16px = 1em)。

#### Set Font Size With Pixels

设置文本尺寸为 pixels 让你可以完全的掌控文字尺寸：

```css
h1 {
    font-size: 40px;
}

h2 {
    font-size: 30px;
}

p {
    font-size: 14px;
}
```

**提示：**如果你使用 pixels，你仍可以使用缩放工具调整整个页面。

#### Set Font Size With Em

要允许用户调整文字尺寸 (在浏览器菜单),许多开发者使用 em 替代 pixels。

W3C 建议使用 em 作为单位。

1em 等于当前的 font size。在浏览器中默认的 text size 是 16px。因此 1em 默认的尺寸是 16px。

计算 em 的使用可以按照公式 pixels/16 = em。

```css
h1 {
    font-size: 2.5em; /* 40px/16=2.5em */
}

h2 {
    font-size: 1.875em; /* 30px/16=1.875em */
}

p {
    font-size: 0.875em; /* 14px/16=0.875em */
}
```

在上面的例子，与之前的例子效果相同，但是它可以在所有浏览器调整尺寸。

不幸的事，对于低版本的 IE 仍然出现问题，文本会变得比预计中要大，小的也变得比预计中要小。

#### Use a Combination of Percent and Em

这个解决方案在所有浏览器中都工作，通过设置 body 元素的默认 font-size 为百分比。

```css
body {
    font-size: 100%;
}

h1 {
    font-size: 2.5em;
}

h2 {
    font-size: 1.875em;
}

p {
    font-size: 0.875em;
}
```

现在的代码非常完美，它在所有浏览器表现出相同的 size，并且所有浏览器中都可以缩放或调整文本。


### Font Weight

`font-weight` 属性指定 font 的重量。

```css
p.normal {
    font-weight: normal;
}

p.thick {
    font-weight: bold;
}
``` 

### Font Variant

`font-variant` 指定文本是否应当显示为 small-caps font。

在 small-cap font 中，所有小写字母会转换为大写字母。转换后的大写字母在文本中会表现得比原来的小写字母更小。

```css
p.normal {
    font-variant: normal;
}

p.small {
    font-variant: small-caps;
}
```

### All CSS Font Properties

Property	 | Description
------------- | -------------
[font](http://www.w3schools.com/cssref/pr_font_font.asp)	 | Sets all the font properties in one declaration
[font-family](http://www.w3schools.com/cssref/pr_font_font-family.asp) | 	Specifies the font family for text
[font-size](http://www.w3schools.com/cssref/pr_font_font-size.asp) | 	Specifies the font size of text
[font-style](http://www.w3schools.com/cssref/pr_font_font-style.asp) | 	Specifies the font style for text
[font-variant](http://www.w3schools.com/cssref/pr_font_font-variant.asp) | 	Specifies whether or not a text should be displayed in a small-caps font
[font-weight](http://www.w3schools.com/cssref/pr_font_weight.asp) | 	Specifies the weight of a font


## CSS Links

### Styling Links

可以对 link 指定任何样式的属性 (如 `color`, `font-family`, `background` 等.)。

```css
a {
    color: hotpink;
}
```

除此之外，link 还可以依赖状态设置样式。

这里是四种 link 状态：

* `a:link` - a normal, unvisited link
* `a:visited` - a link the user has visited
* `a:hover` - a link when the user mouses over it
* `a:active` - a link the moment it is clicked

```css
/* unvisited link */
a:link {
    color: red;
}

/* visited link */
a:visited {
    color: green;
}

/* mouse over link */
a:hover {
    color: hotpink;
}

/* selected link */
a:active {
    color: blue;
}
```

When setting the style for several link states, there are some order rules:

* a:hover MUST come after a:link and a:visited
* a:active MUST come after a:hover

### Text Decoration

`text-decoration` 属性通常用做移除 link 的下划线。

```css
a:link {
    text-decoration: none;
}

a:visited {
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

a:active {
    text-decoration: underline;
}
```

### Background Color

`background-color` 属性可以被用做指定 link 的背景颜色:

```css
a:link {
    background-color: yellow;
}

a:visited {
    background-color: cyan;
}

a:hover {
    background-color: lightgreen;
}

a:active {
    background-color: hotpink;
} 
```

### Advanced - Create link boxes

```css
<style>
a:link, a:visited {
    display: block;
    font-weight: bold;
    color: #ffffff;
    background-color: #98bf21;
    width: 120px;
    text-align: center;
    padding: 4px;
    text-decoration: none;
}

a:hover, a:active {
    background-color: #7A991A;
}
</style>
</head>
<body>

<a href="default.asp" target="_blank">This is a link</a>
```

## CSS Lists

CSS list 属性让你可以：

* 为排序列表设置不同的列表项标记
* 为无序列表设置不同的列表项标记
* 设置图像作为列表项的标记

### HTML Lists

在 HTML 中，有两种类型的列表：

* 无序列表 (`<ul>`) - 列表项是圆点标记
* 有序列表 (`<ol>`) - 列表项是数字或字母标记

通过 CSS 列表的样式可以更进一步美化，图像也可以作为列表项标记。

### 不同的列表项标记

`list-style-type` 属性指定列表项标记的类型。

下面的例子展示一些可用的列表项标记：

```css
ul.a {
    list-style-type: circle;
}

ul.b {
    list-style-type: square;
}

ol.c {
    list-style-type: upper-roman;
}

ol.d {
    list-style-type: lower-alpha;
}
```

有的值为有序列表提供，有的为无序列表提供。

### 图像作为列表项标记

`list-style-image` 指定图像列表项标记:

```css
ul {
    list-style-image: url('sqpurple.gif');
}
```

### Position The List Item Markers

使用 list-style-position 属性指定列表项标记是否应该出现在内容流的内部或外部：

```css
ul {
    list-style-position: inside;
}
```

### List - Shorthand property

```css
ul {
    list-style: square inside url("sqpurple.gif");
}
```

When using the shorthand property, the order of the property values are:

* `list-style-type` (if a list-style-image is specified, the value of this property will be displayed if the image for some reason cannot be displayed)
* `list-style-position` (specifies whether the list-item markers should appear inside or outside the content flow)
* `list-style-image` (specifies an image as the list item marker)


If one of the property values above are missing, the default value for the missing property will be inserted, if any.

### All CSS List Properties

Property | 	Description
------------- | -------------
list-style | 	Sets all the properties for a list in one declaration
list-style-image | 	Specifies an image as the list-item marker
list-style-position | 	Specifies if the list-item markers should appear inside or outside the content flow
list-style-type | 	Specifies the type of list-item marker



## CSS Tables

### Table Borders

指定 table 的边框，使用 `border` 属性。

下面的例子为 `<table>`,`<th>`,和 `<td>` 元素指定黑色边框：

```css
table, th, td {
   border: 1px solid black;
}
```

注意上面的例子有两个边框，这是因为 table 和 `<th>` 和 `<td>` 元素有分开的边框。

### 合并 Table 边框

`border-collapse` 属性设置 table 的边框是否应该合并到单行：

```css
table {
    border-collapse: collapse;
}

table, th, td {
    border: 1px solid black;
}
```

### Table Width and Height

table 的宽度和高度通过 `width` 和 `height` 属性设置。

下面的例子设置 table 的宽度为 100%，而 `<th>` 元素的高度设置为 50px：

```css
table {
    width: 100%;
}

th {
    height: 50px;
}
```

### 水平对齐

`text-align` 属性设置 `<th>` 或 `<td>` 内容的水平对齐方式 (如左对齐或右对齐)。

默认,`<th>` 元素的内容是中心对齐而 `<td>` 元素的内容是左对齐。

下面的例子设置 `<th>` 元素的内容左对齐：

```css
th {
    text-align: left;
}
```

### 垂直对齐

`vertical-align` 属性设置 `<th>`,`<td>` 内容的垂直对齐 (如 top，bottom，或 middle)。

默认，table 的内容的垂直对齐是 middle (包括 `<td>`,`<td>` 元素)。

下面的例子设置 `<td>` 元素的垂直对齐为 bottom。

```css
td {
    height: 50px;
    vertical-align: bottom;
}
```

### Table Padding

要控制 table 内的内容与边框之间的空间，在 `<td>` 和 `<th>` 元素中使用 `padding` 属性：

```css
td {
    padding: 15px;
}
```

### Table Color

下面的例子指定 <th> 元素边框的颜色和文本内容和背景的颜色：

```css
table, td, th {
    border: 1px solid green;
}

th {
    background-color: green;
    color: white;
}
```

### 其它 

设置 table 的说明字幕，并设置在底部：

```css
<style>
table, td, th {
    border: 1px solid black;
}

caption {
    caption-side: bottom;
}
</style>
</head>
<body>

<table>
<caption>Table 1.1 Customers</caption>
  <tr>
    <th>Company</th>
    <th>Contact</th>
    <th>Country</th>
  </tr>

</table>
```


### CSS Table Properties

Property	 | Description
------------- | -------------
border	 | Sets all the border properties in one declaration
border-collapse | 	Specifies whether or not table borders should be collapsed
border-spacing | 	Specifies the distance between the borders of adjacent cells
caption-side | 	Specifies the placement of a table caption
empty-cells | 	Specifies whether or not to display borders and background on empty cells in a table
table-layout | 	Sets the layout algorithm to be used for a table



## CSS 盒模型

HTML 的元素可以被认作一个盒子，在 CSS 中，术语 "box model" 在谈论设计和布局时使用。

CSS box 实际上是一个 box，围绕着每个 HTML 元素。它由：margins,borders,padding 和实际内容组成。

下面是盒模型的图解：

![](./boxmodel.gif)

不同部分的解释：

* **Content** - 盒模型的内容，可以是 text 或 iamges
* **Padding** - 内容周围的空白区域，padding 是透明的
* **Border** - 围绕 padding 和 content 的边框
* **Margin** - 边框外部的空白区域，maigin 是透明的

box model 使我们可以添加围绕 element 的边框，和定义元素之间的空间。

```css
div {
    width: 300px;
    padding: 25px;
    border: 25px solid navy;
    margin: 25px;
}
```

### 元素的 Width 和 Height

为了正确的在所有浏览器设置元素正确的 width 和 height，你需要知道 box model 如何工作。

> **重要提示：**当你通过 CSS 设置元素的 width 和 height 属性，你设置的只是 content area 的 width 和 height。要计算元素的完整尺寸，你必须添加上 padding，borders，和 margins。

假设我想 <div> 元素样式的总共 width 为 350px：

```css
div {
    width: 320px;
    padding: 10px;
    border: 5px solid gray;
    margin: 0; 
}
```

Here is the math:
320px (width)
+ 20px (left + right padding)
+ 10px (left + right border)
+ 0px (left + right margin)
= 350px

The total width of an element should be calculated like this:

Total element width = width + left padding + right padding + left border + right border + left margin + right margin

The total height of an element should be calculated like this:

Total element height = height + top padding + bottom padding + top border + bottom border + top margin + bottom margin

> **Note for old IE**: Internet Explorer 8 and earlier versions, include padding and border in the width property. To fix this problem, add a <!DOCTYPE html> to the HTML page.

## CSS Border


CSS Border 属性允许你指定元素边框的样式，宽度，和颜色。

### Border Style

`border-style` 属性指定边框显示何种样式

The following values are allowed:

* **dotted** - Defines a dotted border
* **dashed** - Defines a dashed border
* **solid** - Defines a solid border
* **double** - Defines a double border
* **groove** - Defines a 3D grooved border. The effect depends on the border-color value
* **ridge** - Defines a 3D ridged border. The effect depends on the border-color value
* **inset** - Defines a 3D inset border. The effect depends on the border-color value
* **outset** - Defines a 3D outset border. The effect depends on the border-color value
* **none** - Defines no border
* **hidden** - Defines a hidden border

**border-style** 可以设置一到四个值 (top border,right border,bottom border,left border)。

```css
p.dotted {border-style: dotted;}
p.dashed {border-style: dashed;}
p.solid {border-style: solid;}
p.double {border-style: double;}
p.groove {border-style: groove;}
p.ridge {border-style: ridge;}
p.inset {border-style: inset;}
p.outset {border-style: outset;}
p.none {border-style: none;}
p.hidden {border-style: hidden;}
p.mix {border-style: dotted dashed solid double;}
```

> **注意：**下面描述的属性只有当 border-style 属性设置了才会有效果！

### Border Width

`border-width` 属性指定四条边框的宽度。

width 可以设置为指定尺寸 (px,pt,cm,em 等) 或通过三个预定值中的一个:thin,medium,thick。

`border-width` 属性可以设置一到四个值 (top border,right border,bottom border,left border)。

```css
p.one {
    border-style: solid;
    border-width: 5px;
}

p.two {
    border-style: solid;
    border-width: medium;
}

p.three {
    border-style: solid;
    border-width: 2px 10px 4px 20px;
}
```

### Border Color

`border-color` 属性用做设置四条边框的颜色。

颜色可以通过下面的方式设置：

* name - specify a color name, like "red"
* RGB - specify a RGB value, like "rgb(255,0,0)"
* Hex - specify a hex value, like "#ff0000"
* transparent

`border-color` 属性可以设置一到四个值 (top border,right border,bottom border,left border)。

如果 `border-color` 未设置，那么它会继承元素的颜色。

```css
p.one {
    border-style: solid;
    border-color: red;
}

p.two {
    border-style: solid;
    border-color: green;
}

p.three {
    border-style: solid;
    border-color: red green blue yellow;
}
```

### Border 单边样式

From the examples above you have seen that it is possible to specify a different border for each side.

In CSS, there is also properties for specifying each of the borders (top, right, bottom, and left):

```css
p {
    border-top-style: dotted;
    border-right-style: solid;
    border-bottom-style: dotted;
    border-left-style: solid;
}
```

The example above gives the same result as this:

```css
p {
    border-style: dotted solid;
}
```



** If the `border-style` property has four values: **

`border-style: dotted solid double dashed;`

* top border is dotted
* right border is solid
* bottom border is double
* left border is dashed

** If the `border-style` property has three values: **

`border-style: dotted solid double;`

* top border is dotted
* right and left borders are solid
* bottom border is double

** If the `border-style` property has two values: **

`border-style: dotted solid;`

* top and bottom borders are dotted
* right and left borders are solid


** If the `border-style` property has one value: **

`border-style: dotted;`

* all four borders are dotted


The `border-style` property is used in the example above. However, it also works with `border-width` and `border-color`.


### Border - Shorthand Property

As you can see from the examples above, there are many properties to consider when dealing with borders。

To shorten the code, it is also possible to specify all the individual border properties in one property.

The `border` property is a shorthand property for the following individual border properties:

* `border-width`
* `border-style` (required)
* `border-color`

```css
p {
    border: 5px solid red;
}
```

### All the top border properties in one declaration

```css
p {
    border-style: solid;
    border-top: thick double #ff0000;
}
```

### All CSS Border Properties

Property | 	Description
------------- | -------------
border | 	Sets all the border properties in one declaration
border-bottom	 | Sets all the bottom border properties in one declaration
border-bottom-color | 	Sets the color of the bottom border
border-bottom-style | 	Sets the style of the bottom border
border-bottom-width	 | Sets the width of the bottom border
border-color | 	Sets the color of the four borders
border-left | 	Sets all the left border properties in one declaration
border-left-color | 	Sets the color of the left border
border-left-style | 	Sets the style of the left border
border-left-width | 	Sets the width of the left border
border-right	 | Sets all the right border properties in one declaration
border-right-color | 	Sets the color of the right border
border-right-style | 	Sets the style of the right border
border-right-width | 	Sets the width of the right border
border-style | 	Sets the style of the four borders
border-top | 	Sets all the top border properties in one declaration
border-top-color	 | Sets the color of the top border
border-top-style	 | Sets the style of the top border
border-top-width	 | Sets the width of the top border
border-width	 | Sets the width of the four borders

## CSS Outline

outline 是围绕着元素绘制的线条 (边框外部)，使元素暴露。

但是 outline 属性与 border 属性不同 - outline 不是元素尺寸的一部分，元素的总宽高不受 outline 宽度影响。

![](./outline.gif)

### Outline Style

The `outline-style` property specifies the style of the outline.

The `outline-style` property can have one of the following values:

* `dotted` - Defines a dotted outline
* `dashed` - Defines a dashed outline
* `solid` - Defines a solid outline
* `double` - Defines a double outline
* `groove` - Defines a 3D grooved outline. The effect depends on the outline-color value
* `ridge` - Defines a 3D ridged outline. The effect depends on the outline-color value
* `inset` - Defines a 3D inset outline. The effect depends on the outline-color value
* `outset` - Defines a 3D outset outline. The effect depends on the outline-color value
* `none` - Defines no outline
* `hidden` - Defines a hidden outline


The following example first sets a thin red border around each `<p>` element, then it shows the different `outline-style` values:

```css
p {border: 1px solid red;}

p.dotted {outline-style: dotted solid;}
p.dashed {outline-style: dashed;}
p.solid {outline-style: solid;}
p.double {outline-style: double;}
p.groove {outline-style: groove;}
p.ridge {outline-style: ridge;}
p.inset {outline-style: inset;}
p.outset {outline-style: outset;}
```

> **Note**: None of the OTHER CSS outline properties described below will have ANY effect unless the `outline-style` property is set!

### Outline Width

The `outline-width` property specifies the width of the outline.

The width can be set as a specific size (in px, pt, cm, em, etc) or by using one of the three pre-defined values: thin, medium, or thick.

```css
p {border: 1px solid red;}

p.one {
    outline-style: solid;
    outline-width: thick;
}

p.two {
    outline-style: solid;
    outline-width: 5px;
}
```

### Outline Color

The `outline-color` property is used to set the color of the outline.

The color can be set by:

* name - specify a color name, like "red"
* RGB - specify a RGB value, like "rgb(255,0,0)"
* Hex - specify a hex value, like "#ff0000"
* invert - 执行颜色反转 (会确保 outline 可见，无论是否与背景颜色相同)

```css
p {
    border: 1px solid red;
    outline-style: solid;
    outline-color: lime;
}
```

### Outline - Shorthand property

To shorten the code, it is also possible to specify all the individual outline properties in one property.

The `outline` property is a shorthand property for the following individual outline properties:

* `outline-width`
* `outline-style` (required)
* `outline-color`

```css
p {
    outline: 5px dotted lime;
}
```

### All CSS Outline Properties

Property	 | Description
------------- | -------------
outline | 	Sets all the outline properties in one declaration
outline-color | 	Sets the color of an outline
outline-offset | Specifies the space between an outline and the edge or border of an element
outline-style	Sets |  the style of an outline
outline-width	Sets |  the width of an outline

## CSS Margins

CSS Margin 属性用做生成围绕元素的空间。

margin 属性设置边框外部白色空间的尺寸。

> **注意：**margin 是完全透明的，并且不能拥有背景颜色！

通过 CSS，你拥有完全控制 margin 的能力。可以通过 CSS 属性设置元素的 margin 的每一条边 (top,right,bottom,left)。

### Margin - Individual Sides

CSS has properties for specifying the margin for each side of an element:

* `margin-top`
* `margin-right`
* `margin-bottom`
* `margin-left`

所有 margin 属性都可以使用下列值：

* auto - 浏览器自动计算 margin 值
* length - 指定 margin 的特定单位 px, pt, cm, etc.
* % - 指定 maigin 的长度为包含它的元素的百分比宽度
* inherit - 指定 maigin 的长度通过父元素继承

> **注意：**也可以对 margin 使用负值，使内容重叠。

下面的例子为 `<p>` 元素的全部四条边设置不同的 margin 尺寸。

```css
p {
    margin-top: 100px;
    margin-bottom: 100px;
    margin-right: 150px;
    margin-left: 80px;
}
```

下面的例子使 left margin 从父元素继承：

```css
div.container {
    border: 1px solid red;
    margin-left: 100px;
}

p.one {
    margin-left: inherit;
}
```

### Margin - Shorthand Property

To shorten the code, it is possible to specify all the margin properties in one property.

The `margin` property is a shorthand property for the following individual margin properties:

* `margin-top`
* `margin-right`
* `margin-bottom`
* `margin-left`

```css
p {
    margin: 100px 150px 100px 80px;
}
```

### Use of The auto Value

你可以设置 margin 属性为 `auto` 使元素位于它的容器的水平中心。

元素将获根据指定宽度，剩余空间将会为 left 和 right margins 平均分配。

```css
div {
    width: 300px;
    margin: auto;
    border: 1px solid red;
}
```

### All CSS Margin Properties

Property | 	Description
------------- | -------------
margin | 	A shorthand property for setting the margin properties in one declaration
margin-bottom | 	Sets the bottom margin of an element
margin-left	 | Sets the left margin of an element
margin-right	 | Sets the right margin of an element
margin-top	 | Sets the top margin of an element

## CSS Padding

CSS Padding 属性定义元素内容和元素边框之间的空间距离。

> **注意：**padding 的背景颜色被元素的背景颜色影响

All the padding properties can have the following values:

* length - specifies a padding in px, pt, cm, etc.
* % - 指定为包含该元素的容器的百分比
* inherit - specifies that the padding should be inherited from the parent element

### All CSS Padding Properties

Property | 	Description
------------- | -------------
padding | 	A shorthand property for setting all the padding properties in one declaration
padding-bottom | 	Sets the bottom padding of an element
padding-left | 	Sets the left padding of an element
padding-right | 	Sets the right padding of an element
padding-top | 	Sets the top padding of an element

## CSS Dimensions

CSS Dimension 让你可以控制元素的高和宽。

`height` 和 `width` 用做设置元素的高度和宽度。

`height` 和 `width` 可以设置为 auto (这是默认值。意味着由浏览器计算宽度和高度)，或指定为长度值，例如 px,cm 等，或者容器块的百分比 (%)。

**注意：** `height` 和 `width` 属性不包含 padding，borders，或 margins;它所设置的是元素的 padding，border，和 margin 内区域的高和宽。

下面的例子的 `<div>` 元素 height 设置为 100px，width 设置为 500px：

```css
div {
    width: 500px;
    height: 100px;
    border: 3px solid #73AD21;
}
```

### Setting max-width

`max-width` 属性用做设置元素的最大宽度。

max-width 可以设置为指定长度，或百分比，或 none (默认值，意味着没有最大宽度)。

上面的例子当浏览器窗口小于元素的宽度 (500px) 会出现问题，浏览器会在页面上添加滚动条。

使用 max-width 替代 width，当出现这种情况，将会提高浏览器对小窗口的处理。

**注意：** `max-width` 属性值会覆盖 width 属性。

The following example shows a <div> element with a height of 100 pixels and a max-width of 500 pixels:

```css
div {
    max-width: 500px;
    height: 100px;
    border: 3px solid #73AD21;
}
```

### All CSS Dimension Properties


Property | 	Description
------------- | -------------
height | 	Sets the height of an element
max-height | 	Sets the maximum height of an element
max-width | 	Sets the maximum width of an element
min-height | 	Sets the minimum height of an element
min-width | 	Sets the minimum width of an element
width | 	Sets the width of an element

## CSS Layout - The display Property

`display` 属性是最重要的控制布局的 CSS 属性

`dispaly` property 指定一个元素如何显示。

每一个 HTML element 根据它的类型都有一个默认 display 值。这个默认值对于大部分 element 来说是 `block` 或 `inline`。

### Block-level Elements

block-level 的 element 总是由新行开始并占满行可用的宽度 (尽可能的伸展 left 和 right)。

block-level element 的例子：

* `<div>`
* `<h1> - <h6>`
* `<p>`
* `<form>`
* `<header>`
* `<footer>`
* `<section>`

### Inline Elements

Inlinw element 不会从新行开始并且只索取必要的宽度。

Inline element 的例子：

* `<span>`
* `<a>`
* `<img>`

### Display: none;

`display:none;` 是 JavaScrpit 常用隐藏和显示元素的方式，不用删除或重新创建元素。

`<script>` 元素默认使用 `display:none;`。

### Override The Default Display Value

之前提到，每个元素都有默认 display 值，不过，你可以重写它们。

更改 inline element 为 block element，或者反过来，可以有效的使页面以特定的方式显示，并且仍然遵循 web 标准。

常用的例子更改 `<li>` 元素为水平菜单：

```css
li {
    display: inline;
}
```

> 注意：设置 element 的 dispaly 属性只是更改**元素如何显示**，不是更改元素类型，因此，设置为 `display:block;` 的 inline element 的内部仍然不允许嵌套其它 block element。

### Hide an Element - display:none or visibility:hidden?

隐藏元素可以设置 `dispaly` 属性为 `none`。元素将会隐藏，在页面看起来从来没有过该元素L

```css
h1.hidden {
    display: none;
}
```

`visibility:hidden;` 也隐藏元素。

不过，该元素仍然占据之前的空间，元素虽然被隐藏，但仍影响布局。

```css
h1.hidden {
    visibility: hidden;
}
```

## CSS Layout - width and max-width

### Using width, max-width and margin: auto;

之前章节提到，block-level 的元素总是占满可用的宽度 (尽可能远的伸展 left 和 right)。

设置 block-level 元素的 `width` 属性将会避免它占据满容器的边界。然后，设置 margin 为 auto，元素将会定位到容器的水平中心。元素会设置为指定宽度，然后将剩余的空间平均分配给 left 和 right margin。

**注意：**上面的做法在浏览器窗口的宽度小于 `<div>` 元素的宽度时会出现滚动条。

使用 `max-width` 作为替代，当出现这种情景时，会改进浏览器对小窗口的处理。这样做对网站在小屏幕设备上的可读性非常重要。

## CSS Layout - The position Property

### The position Property

`position` 属性指定元素所使用的定位方式的类型。

有以下四个 `position` values：

* `static`
* `relative`
* `fixed`
* `absolute`

Element 然后使用 top，bottom，left，和 right 属性进行定位。但是，在 `position` 属性第一次设置值之前这些属性都没效果。并且它们的工作方式也依赖于 `position` value。

### position: static;

HTML element 的 position 的默认值是 static。

Static element 不受 top,bottom,left,right 属性影响。

`position: static` 不以任何特别方式定位；它总是依据页面的 normal flost 定位。

```css
div.static {
    position: static;
    border: 3px solid #73AD21;
}
```

### position: relative

`position: relative;` 的 element，它的定位是相对于它的正常位置。

设置 relative element 的 top，right，bottom，left 属性会使它从正常位置调整。其它内容不会根据 element 位置的调整而留出缝隙适应。

```css
div.relative {
    position: relative;
    left: 30px;
    border: 3px solid #73AD21;
}
```

### position: fixed

`position: fixed;` element 的定位是相对 viewport，这意味着它总是位于相同位置即使页面滚动。top，right，bottom，left 属性会被用做元素的定位。

fixed element 不会在页面与其它 element 产生间隙。

Notice the fixed element in the lower-right corner of the page. Here is the CSS that is used:

```css
div.fixed {
    position: fixed;
    bottom: 0;
    right: 0;
    width: 300px;
    border: 3px solid #73AD21;
}
```

### position: absolute;

`position: absolute;` element 是依据最接近它的祖先已 positioned 的 element 进行定位。(不像 fixed 相对于 viewport 定位)。

但如果一个 absolute positioned element 没有祖先 element，它会使用 document body，并跟随页面滚动。

注意：**positioned** element 是指出了 static 之外的任意 element。

```css
div.relative {
    position: relative;
    width: 400px;
    height: 200px;
    border: 3px solid #73AD21;
} 

div.absolute {
    position: absolute;
    top: 80px;
    right: 0;
    width: 200px;
    height: 100px;
    border: 3px solid #73AD21;
}
```

### 重叠 Elements

但 element positioned 后，它们可以于其它 element 重叠。

z-index property 指定 element 的排序堆 (哪个元素应该在前，和在后)

element 可以有正和负的 stack 顺序：

```css
img {
    position: absolute;
    left: 0px;
    top: 0px;
    z-index: -1;
}
```

更大的堆排序总在更小的堆排序后面。

> 注意：如果两个重叠的 positioned element 都没指定 z-index，在 HTML 代码之后的 element 将会显示在顶部。

### All CSS Positioning Properties

Property	 | Description
------------- | -------------
bottom | 	Sets the bottom margin edge for a positioned box
clip | 	Clips an absolutely positioned element
cursor | 	Specifies the type of cursor to be displayed
left | 	Sets the left margin edge for a positioned box
overflow | 	Specifies what happens if content overflows an element's box
overflow-x | 	Specifies what to do with the left/right edges of the content if it overflows the element's content area
overflow-y | 	Specifies what to do with the top/bottom edges of the content if it overflows the element's content area
position | 	Specifies the type of positioning for an element
right | 	Sets the right margin edge for a positioned box
top	 | Sets the top margin edge for a positioned box
z-index | 	Sets the stack order of an element

## CSS Layout - float and clear

`float` 属性指定 element 是否应该流动。

`clear` 属性用作控制 floating element 的行为。

### The float Property

使用 `float` 可以最简单的使文本环绕图像。

下面例子指定图像在文本的右边浮动：

```css
img {
    float: right;
    margin: 0 0 10px 10px;
}
```

### The clear Property

`clear` 属性用作控制流动中的 element 的行为。

Element 后面的 floating element 将会围绕它。要避免这种情况，可以使用 `clear` 属性。

`clear` 属性指定一个元素不允许内容在它附近浮动。


### The clearfix Hack - overflow: auto;

如果一个 element 高于容纳它的 element，并且该 element 是浮动的，那么它会溢出容器的外部。

我们可以添加 `overflow:auto;` 到容器 element 修复这个问题：

```css
.clearfix {
    overflow: auto;
}
``` 

### Web Layout Example

It is common to do entire web layouts using the float property:

```css
div {
    border: 3px solid blue;
}

.clearfix {
    overflow: auto;
}

nav {
    float: left;
    width: 200px;
    border: 3px solid #73AD21;
}

section {
    margin-left: 206px;
    border: 3px solid red;
}
```

### All CSS Float Properties

Property | 	Description
------------- | -------------
clear | 	Specifies on which sides of an element where floating elements are not allowed to float
float | 	Specifies whether or not an element should float
overflow | 	Specifies what happens if content overflows an element's box
overflow-x | 	Specifies what to do with the left/right edges of the content if it overflows the element's content area
overflow-y | 	Specifies what to do with the top/bottom edges of the content if it overflows the element's content area

## CSS Layout - inline-block

### The inline-block Value

通过使用 float 属性，我们可能会花费大量时间在创建格子填充满浏览器并作出样式精美的效果 (当浏览器调整尺寸时)。

不过，`display` 属性的 `inline-block` 使工作变得更简单。

inline-block 元素类似 inline 元素但它们可以拥有 width 和 height。

### Examples

The old way - using `float` (notice that we also need to specify a `clear` property for the element after the floating boxes):

```css
.floating-box {
    float: left;
    width: 150px;
    height: 75px;
    margin: 10px;
    border: 3px solid #73AD21; 
}

.after-box {
    clear: left;
}
```
The same effect can be achieved by using the `inline-block` value of the `display` property (notice that no `clear` property is needed):

```css
.floating-box {
    display: inline-block;
    width: 150px;
    height: 75px;
    margin: 10px;
    border: 3px solid #73AD21; 
}
```
## CSS Layout - Horizontal Align

### Center Align - Using margin

设置 block-level element 可以放置它向容器边缘外部延伸。使用 `margin:auto;`,使它在定位到容器内部水平中心。

元素会设置为特定的宽度，并将容器内剩余的空间平均分配给左右两边 margin：

```css
.center {
    margin: auto;
    width: 60%;
    border:3px solid #73AD21;
    padding: 10px;
}
```

[example](http://www.w3schools.com/css/tryit.asp?filename=trycss_align_container)

### Left and Right Align - Using position

One method for aligning elements is to use position: absolute;:

```css
.right {
    position: absolute;
    right: 0px;
    width: 300px;
    border:3px solid #73AD21;
    padding: 10px;
}
```

[example](http://www.w3schools.com/css/tryit.asp?filename=trycss_align_pos)

**Note:** **Absolute** positioned elements are removed from the normal flow, and can overlap elements.

**Tip:** When aligning elements with `position`, always define `margin` and `padding` for the `<body>` element. This is to avoid visual differences in different browsers.

上面的例子会在 IE8 和早期版本出现问题，但使用 `postion` 时，如果容器 element (例子中的 <div class="container">) 有指定的宽度，并缺少 !DOCTYPE 的声明,IE 8 和早期的版本将会添加 17px margin 在 right side。这是为滚动条预留的空间。因此，当使用 position 时，应该总是设置 !DOCTYPE 的定义。

### Left and Right Align - Using float

Another method for aligning elements is to use the `float` property:

```css
.right {
    float: right;
    width: 300px;
    border:3px solid #73AD21;
    padding: 10px;
}
```

**Tip**: When aligning elements with `float`, always define `margin` and `padding` for the `<body>` element. This is to avoid visual differences in different browsers.

There is also a problem with IE8 and earlier, when using `float`. If the !DOCTYPE declaration is missing, IE8 and earlier versions will add a 17px margin on the right side. This seems to be space reserved for a scrollbar. So, always set the !DOCTYPE declaration when using `float`:

## CSS Combinators

combinator 用来解释一些 selector 之间的关系。

A CSS selector can contain more than one simple selector. Between the simple selectors, we can include a combinator.

There are four different combinators in CSS3:

* 后裔选择器 (space)
* 子选择器 (>)
* 相邻兄弟选择器 (+)
* 一般兄弟选择器 (~)

### Descendant Selector

后裔选择器适配指定 element 的所有后裔 element。

下面的例子选择所有 `<div>` 元素内的 `<p>` 元素：

```css
div p {
    background-color: yellow;
}
```

### Child Selector

child selector 选择 element 所有的直接子元素。

下面的例子选择 <div> element 的所有为 `<p>` 元素的直接子元素：
 
```css
div > p {
    background-color: yellow;
}
```

### Adjacent Sibling Selector

相邻兄弟选择器选择指定元素的紧随的兄弟元素。

相邻兄弟元素必须有相同的父元素，"adjacent" 意味着 "immediately following"。

下面的例子选择所有紧随 <div> 元素的第一个 `<p>` 元素：

```css
div + p {
    background-color: yellow;
}
```

### General Sibling Selector

一般兄弟选择器选择与指定元素相邻的所有元素。

下面的例子选择所有与 <div> 相邻的 `<p>` 元素：

```css
div ~ p {
    background-color: yellow;
}
```

## CSS Pseudo-classes

### 什么是伪类？

伪类用来定义元素的特殊状态。

例如，可以用作：

* 当鼠标移动到元素上的颜色
* 已访问和未范围的链接之间的区别

### 语法

```css
selector:pseudo-class {
    property:value;
}
```

### Anchor Pseudo-classes

Link 可以被显示为不同方式：

```css
/* unvisited link */
a:link {
    color: #FF0000;
}

/* visited link */
a:visited {
    color: #00FF00;
}

/* mouse over link */
a:hover {
    color: #FF00FF;
}

/* selected link */
a:active {
    color: #0000FF;
}
```

> **Note:** `a:hover` MUST come after `a:link` and `a:visited` in the CSS definition in order to be effective! `a:active` MUST come after `a:hover` in the CSS definition in order to be effective! Pseudo-class names are not case-sensitive.

### Pseudo-classes and CSS Classes

Pseudo-classes can be combined with CSS classes:

```css
a.highlight:hover {
    color: #ff0000;
}
```

### CSS - The :first-child Pseudo-class

The `:first-child` pseudo-class matches a specified element that is the first child of another element.


In the following example, the selector matches any `<p>` element that is the first child of any element:

```css
p:first-child {
    color: blue;
}
```

#### Match the first `<i>` element in all `<p>` elements

```css
p i:first-child {
    color: blue;
}
```

#### Match all `<i>` elements in all first child `<p>` elements

In the following example, the selector matches all `<i>` elements in `<p>` elements that are the first child of another element:

```css
p:first-child i {
    color: blue;
}
```

### CSS - The :lang Pseudo-class


The `:lang` pseudo-class 允许你为不同的语言定义特殊的规则。

下面的例子，`:lang` 将 lang="no" 的 `<q>` 元素转换为 `"~" "~"`:

```html
<html>
<head>
<style>
q:lang(no) {
    quotes: "~" "~";
}
</style>
</head>

<body>
<p>Some text <q lang="no">A quote in a paragraph</q> Some text.</p>
</body>
</html>
```

### All CSS Pseudo Classes

Selector | 	Example | 	Example description
------------- | ------------ | -------------
:active | 	a:active | 	Selects the active link
:checked | 	input:checked | 	Selects every checked `<input>` element
:disabled | 	input:disabled | 	Selects every disabled `<input>` element
:empty	p:empty | 	Selects |  every `<p>` element that has no children
:enabled | 	input:enabled	 | Selects every enabled `<input>` element
:first-child | 	p:first-child	 | Selects every `<p>` elements that is the first child of its parent
:first-of-type | 	p:first-of-type | 	Selects every `<p>` element that is the first `<p>` element of its parent
:focus	 | input:focus | Selects the `<input>` element that has focus
:hover | 	a:hover | 	Selects links on mouse over
:in-range	 | input:in-range | 	Selects `<input>` elements with a value within a specified range
:invalid	 | input:invalid	 | Selects all `<input>` elements with an invalid value
:lang(language)	 | p:lang(it) | 	Selects every `<p>` element with a lang attribute value starting with "it"
:last-child | 	p:last-child | 	Selects every `<p>` elements that is the last child of its parent
:last-of-type	 | p:last-of-type | 	Selects every `<p>` element that is the last `<p>` element of its parent
:link	 | a:link	Selects |  all unvisited links
:not(selector) | 	:not(p) | 	Selects every element that is not a `<p>` element
:nth-child(n)	 | p:nth-child(2) | 	Selects every `<p>` element that is the second child of its parent
:nth-last-child(n) | 	p:nth-last-child(2)	 | Selects every <p> element that is the second child of its parent, counting from the last child
:nth-last-of-type(n) | 	p:nth-last-of-type(2) | 	Selects every <p> element that is the second `<p>` element of its parent, counting from the last child
:nth-of-type(n) | 	p:nth-of-type(2)	 | Selects every `<p>` element that is the second `<p>` element of its parent
:only-of-type	 | p:only-of-type | 	Selects every `<p>` element that is the only `<p>` element of its parent
:only-child | 	p:only-child | 	Selects every `<p>` element that is the only child of its parent
:optional	 | input:optional | 	Selects `<input>` elements with no "required" attribute
:out-of-range | 	input:out-of-range | 	Selects `<input>` elements with a value outside a specified range
:read-only | 	input:read-only	 | Selects `<input>` elements with a "readonly" attribute specified
:read-write | 	input:read-write	 | Selects `<input>` elements with no "readonly" attribute
:required	 | input:required | 	Selects `<input>` elements with a "required" attribute specified
:root	 | root	 | Selects the document's root element
:target | 	#news:target | 	Selects the current active #news element (clicked on a URL containing that anchor name)
:valid	 | input:valid | 	Selects all `<input>` elements with a valid value
:visited | 	a:visited | 	Selects all visited links


### All CSS Pseudo Elements

Selector | 	Example | 	Example description
------------- | ------------ | -------------
::after | 	p::after	 | Insert content after every `<p>` element
::before | 	p::before | 	Insert content before every `<p>` element
::first-letter | 	p::first-letter | 	Selects the first letter of every `<p>` element
::first-line	 | p::first-line | 	Selects the first line of every `<p>` element
::selection	 | p::selection | 	Selects the portion of an element that is selected by a user

[Link](http://www.w3schools.com/css/css_pseudo_classes.asp)。

## CSS Pseudo-elements

### 什么是伪类元素？

CSS 伪类元素用作更改一个元素特定部分的样式。

例如，可以用作：

* 更改元素的首字母，首行样式。
* 在元素内容之前，之后插入内容。

### Syntax

The syntax of pseudo-elements:

```css
selector::pseudo-element {
    property:value;
}
```

> **Notice the double colon notation -** `::first-line` versus `:first-line`

> The double colon replaced the single-colon notation for pseudo-elements in CSS3. This was an attempt from W3C to distinguish between `pseudo-classes` and `pseudo-elements`.

> The single-colon syntax was used for both pseudo-classes and pseudo-elements in CSS2 and CSS1.

> For backward compatibility, the single-colon syntax is acceptable for CSS2 and CSS1 pseudo-elements.

### The ::first-line Pseudo-element

The `::first-line` pseudo-element is used to add a special style to the first line of a text.

The following example formats the first line of the text in all `<p>` elements:

```css
p::first-line {
    color: #ff0000;
    font-variant: small-caps;
}
```

The following properties apply to the `::first-line` pseudo-element:

* font properties
* color properties
* background properties
* word-spacing
* letter-spacing
* text-decoration
* vertical-align
* text-transform
* line-height
* clear


### The ::first-letter Pseudo-element

The `::first-letter` pseudo-element is used to add a special style to the first letter of a text.

The following example formats the first letter of the text in all `<p>` elements: 

```css
p::first-letter {
    color: #ff0000;
    font-size: xx-large;
}
```

**Note: **The `::first-letter` pseudo-element can only be applied to **block-level elements**.

The following properties apply to the ::first-letter pseudo- element: 

* font properties
* color properties 
* background properties
* margin properties
* padding properties
* border properties
* text-decoration
* vertical-align (only if "float" is "none")
* text-transform
* line-height
* float
* clear

### Pseudo-elements and CSS Classes

Pseudo-elements can be combined with CSS classes: 

```css
p.intro::first-letter {
    color: #ff0000;
    font-size:200%;
}
```

### Multiple Pseudo-elements

Several pseudo-elements can also be combined：

```css
p::first-letter {
    color: #ff0000;
    font-size: xx-large;
}

p::first-line {
    color: #0000ff;
    font-variant: small-caps;
}
```

### CSS - The ::before Pseudo-element

The `::before` pseudo-element can be used to insert some content before the content of an element.

The following example inserts an image before the content of each `<h1>` element:

```css
h1::before {
    content: url(smiley.gif);
}
```

### CSS - The ::after Pseudo-element

The `::after` pseudo-element can be used to insert some content after the content of an element.

The following example inserts an image after the content of each `<h1>` element:

```css
h1::after {
    content: url(smiley.gif);
}
```

### CSS - The ::selection Pseudo-element

The `::selection` pseudo-element matches the portion of an element that is selected by a user.

The following CSS properties can be applied to `::selection`: `color`, `background`, `cursor`, and `outline`.

The following example makes the selected text red on a yellow background:

```css
::selection {
    color: red; 
    background: yellow;
}
```

## CSS Counters

### Using CSS Counters

CSS counters are like "variables".The variable values can be incremented by CSS rules (which will track how many times they are used).

To work with CSS counters we will use the following properties:

* `counter-reset` - Creates or resets a counter
* `counter-increment` - Increments a counter value
* `content` - Inserts generated content
* `counter()` or `counters()` function - Adds the value of a counter to an element

To use a CSS counter, it must first be created with `counter-reset`.

The following example creates a counter for the page (in the body selector), then increments the counter value for each `<h2>` element and adds "Section <value of the counter>:" to the beginning of each `<h2>` element:

```css
body {
    counter-reset: section;
}

h2::before {
    counter-increment: section;
    content: "Section " counter(section) ": ";
}
```

### Nesting Counters

The following example creates one counter for the page (section) and one counter for each `<h1>` element (subsection). The "section" counter will be counted for each `<h1>` element with "Section <*value of the section counter*>.", and the "subsection" counter will be counted for each `<h2>` element with "<*value of the section counter*>.<*value of the subsection counter*>":

```css
body {
    counter-reset: section;
}

h1 {
    counter-reset: subsection;
}

h1::before {
    counter-increment: section;
    content: "Section " counter(section) ". ";
}

h2::before {
    counter-increment: subsection;
    content: counter(section) "." counter(subsection) " ";
}
```

A counter can also be useful to make outlined lists because a new instance of a counter is automatically created in child elements. Here we use the `counters()` function to insert a string between different levels of nested counters:

```css
ol {
    counter-reset: section;
    list-style-type: none;
}

li::before {
    counter-increment: section;
    content: counters(section,".") " ";
}
```

### CSS Counter Properties


Property | 	Description
------------- | ------------ 
content | 	Used with the ::before and ::after pseudo-elements, to insert generated content
counter-increment | 	Increments one or more counter values
counter-reset	 | Creates or resets one or more counters



























































































