layout: [post]
title: Canvas API
date: 2016-03-08 23:43:21
tags:
- 前端
categories:
- 前端
- Canvas
---

Canvas

<!-- more -->


---



## Canvas 是什么

Canvas 是 HTML 5 的一个标签，在浏览器开辟一个区域作为画布，可以显示任意图形，图片，文字等。


这里收集了一些有关 Canvas 的站点：

- API https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/putImageData
- 两个 Canvas 合成的 DEMO http://media.chikuyonok.ru/canvas-blending/

这里是我做的[Nike 跑鞋定制](1)的 DEMO (很简陋) 。

## 其它资源

1. 合成 Canvas
http://media.chikuyonok.ru/canvas-blending/

提供了合成两个 Canvas 的 demo。

核心代码使用 getImageData() 获取像素点，然后遍历 ImagesObject 对象逐个修改像素点。

2. Canvas 框架

http://konvajs.github.io/docs/sandbox/Shape_Tooltips.html

没用过，功能挺多的。

## Canvas 能做什么

这里从 Canvas 的 API 入手，分析 Canvas 能完成的任务。

https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D

下面是 Canvas 的一些 API，但要注意兼容性问题，并且因为历史原因，有的功能当前可以使用，但未来会被替代。

### 画矩形

[CanvasRenderingContext2D.clearRect()](#)
Sets all pixels in the rectangle defined by starting point (x, y) and size (width, height) to transparent black, erasing any previously drawn content.
设置从起始点 (x,y) 开始的尺寸 (width,height) 内所有的像素点为透明的黑色，抹除所有之前设置的内容。
[CanvasRenderingContext2D.fillRect()](#)
Draws a filled rectangle at (x, y) position whose size is determined by width and height.
绘制和填充指定区域，从起始点开始指定的宽度和高度。
[CanvasRenderingContext2D.strokeRect()](#)
Paints a rectangle which has a starting point at (x, y) and has a w width and an h height onto the canvas, using the current stroke style.
在 Canvas 绘制一个矩形，从起始点开始的宽度和高度，使用当前的 stroke style。

### 画文本

The following methods are provided for drawing text. See also the [TextMetrics](#) object for text properties.
下面的方法用作绘制文本，见 TextMetrics 对象描述相关文本属性。

[CanvasRenderingContext2D.fillText()](#)
Draws (fills) a given text at the given (x,y) position.
在给定的位置 (x,y) 绘制 (填充) 给定的文本。
[CanvasRenderingContext2D.strokeText()](#)
Draws (strokes) a given text at the given (x, y) position.
在给定的位置 (x,y) 绘制 (描边) 给定的文本。  
[CanvasRenderingContext2D.measureText()](#)
Returns a TextMetrics object.
返回 TextMetrics 对象。

### 线条风格

The following methods and properties control how lines are drawn.
下面的方法和属性控制线条如何绘制。

[CanvasRenderingContext2D.lineWidth](#)
Width of lines. Default 1.0
线条的宽度，默认是 1.0
[CanvasRenderingContext2D.lineCap](#)
Type of endings on the end of lines. Possible values: butt (default), round, square.
线条结束时的结束种类。可用的值：butt (默认)，round，square。
[CanvasRenderingContext2D.lineJoin](#)
Defines the type of corners where two lines meet. Possible values: round, bevel, miter (default).
定义两条线条相交时边角的类型。可用的值：round，bevel，miter (defautl)。
[CanvasRenderingContext2D.miterLimit](#)
Miter limit ratio. Default 10.
斜接限制比率。默认是 10。具体是什么我也不了解，[这里](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors#A_demo_of_the_miterLimit_property)有介绍
[CanvasRenderingContext2D.getLineDash()](#)
Returns the current line dash pattern array containing an even number of non-negative numbers.
返回当前虚线线条图案数组，包含一组偶数的非负数数字。
[CanvasRenderingContext2D.setLineDash()](#)
Sets the current line dash pattern.
设置当前虚线线条图案。
[CanvasRenderingContext2D.lineDashOffset](#)
Specifies where to start a dash array on a line.
指定虚线图案从线条的哪个位置开始。

### 文本风格

The following properties control how text is laid out.
下面的属性控制文本如何布局。


[CanvasRenderingContext2D.font](#)
Font setting. Default value 10px sans-serif.
字体设置。默认值是 10px sans-serif。

[CanvasRenderingContext2D.textAlign](#)
Text alignment setting. Possible values: start (default), end, left, right or center.
文本对齐设置。可用的值：start  (默认值)，end，left，right 或 center。

[CanvasRenderingContext2D.textBaseline](#)
Baseline alignment setting. Possible values: top, hanging, middle, alphabetic (default), ideographic, bottom.
基线对齐设置。可用的值：top，hanging，middle，alphabetic (默认)，ideographic，bottom。

[CanvasRenderingContext2D.direction](#)
Directionality. Possible values: ltr, rtl, inherit (default).
文本方向。可用的值：ltr，rtl，继承 (默认)。

### 填充和描边风格

Fill styling is used for colors and styles inside shapes and stroke styling is used for the lines around shapes.
填充风格被用作图形内的风格和颜色，描边风格被用作环绕图形的线条的风格。

[CanvasRenderingContext2D.fillStyle](1)
Color or style to use inside shapes. Default #000 (black).
图形内的颜色和风格。默认是 #000 (黑色)。

[CanvasRenderingContext2D.strokeStyle](1)
Color or style to use for the lines around shapes. Default #000 (black).
围绕图形的线条的颜色和风格。默认是 #000 (黑色)。

### 渐变和图案

[CanvasRenderingContext2D.createLinearGradient()](1)
Creates a linear gradient along the line given by the coordinates represented by the parameters.
沿着参数给定坐标的线条创建线型渐变。

[CanvasRenderingContext2D.createRadialGradient()](1)
Creates a radial gradient given by the coordinates of the two circles represented by the parameters.
通过参数指定的两个圆形的坐标创建迳向渐变。

[CanvasRenderingContext2D.createPattern()](1)
Creates a pattern using the specified image (a CanvasImageSource). It repeats the source in the directions specified by the repetition argument. This method returns a CanvasPattern.
使用指定的图像创建图案。 如果指定了 repetition 参数他会在指定方向重复绘制图案。这个方法返回一个 CanvasPattern。

### 阴影

[CanvasRenderingContext2D.shadowBlur](1)
Specifies the blurring effect. Default 0
指定模糊效果。默认是 0.

[CanvasRenderingContext2D.shadowColor](1)
Color of the shadow. Default fully-transparent black.
阴影的颜色。默认是完全不透明的黑色。

[CanvasRenderingContext2D.shadowOffsetX](1)
Horizontal distance the shadow will be offset. Default 0.
阴影水平偏移的距离。默认是 0。

[CanvasRenderingContext2D.shadowOffsetY](1)
Vertical distance the shadow will be offset. Default 0.
阴影垂直偏移的距离。默认是 0。

### 路径

The following methods can be used to manipulate paths of objects.
下面的方法可以用作操作对象的路径。

[CanvasRenderingContext2D.beginPath()](1)
Starts a new path by emptying the list of sub-paths. Call this method when you want to create a new path.
从一个空的子路径列表开始设置新的路径。当你想创建新的路径请调用这个方法。

[CanvasRenderingContext2D.closePath()](1)
Causes the point of the pen to move back to the start of the current sub-path. It tries to draw a straight line from the current point to the start. If the shape has already been closed or has only one point, this function does nothing.
使画笔的当前点移动回当前子路径的起始位置。他会尝试绘制一条直线从当前点到起始点。如果图形已经闭合或只有一个点，这个方法不做任何事情。

[CanvasRenderingContext2D.moveTo()](1)
Moves the starting point of a new sub-path to the (x, y) coordinates.
使新子路径的当前点移动到 (x,y) 坐标。  

[CanvasRenderingContext2D.lineTo()](1)
Connects the last point in the subpath to the x, y coordinates with a straight line.
连接子路径最新的点到 x,y 座标并绘制直线。

[CanvasRenderingContext2D.bezierCurveTo()](1)
Adds a cubic Bézier curve to the path. It requires three points. The first two points are control points and the third one is the end point. The starting point is the last point in the current path, which can be changed using moveTo() before creating the Bézier curve.
增加贝塞尔曲线到路径。前两个点为控制点，第三个点是结束点。起始点是当前路径中最新的点，他可以使用在创建贝塞尔曲线之前使用 moveTo() 更改。

[CanvasRenderingContext2D.quadraticCurveTo()](1)
Adds a quadratic Bézier curve to the current path.
增加二次贝塞尔曲线到当前路径

[CanvasRenderingContext2D.arc()](1)
Adds an arc to the path which is centered at (x, y) position with radius r starting at startAngle and ending at endAngle going in the given direction by anticlockwise (defaulting to clockwise).
增加一个弧形到路径，他的中心在 (x,y) ，半径 r 从 startAngle 开始在 endAngle 结束，通过设置方向决定是顺时针还是逆时针 (默认是顺时针)。

[CanvasRenderingContext2D.arcTo()](1)
Adds an arc to the path with the given control points and radius, connected to the previous point by a straight line.
增加一个弧形到路径，可以传入控制点和半径，以直线连接上一个点。


[CanvasRenderingContext2D.ellipse() ](1)
Adds an ellipse to the path which is centered at (x, y) position with the radii radiusX and radiusY starting at startAngle and ending at endAngle going in the given direction by anticlockwise (defaulting to clockwise).
增加一个椭圆到路径他的中心在 (x,y)，他的半径是 radiusX 和 radiusY，从 startAngle 开始 到 endAngle 结束，设置方向决定是顺时针还是逆时针 (默认是顺时针)。

[CanvasRenderingContext2D.rect()](1)
Creates a path for a rectangle at position (x, y) with a size that is determined by width and height.
增加一个矩形到路径，位置在 (x,y)，由 width 和 height 决定宽高。

### 绘制路径

[CanvasRenderingContext2D.fill()](1)
Fills the subpaths with the current fill style.
以当前设置的 fill style 填充子路径

[CanvasRenderingContext2D.stroke()](1)
Strokes the subpaths with the current stroke style.
以当前的 stroke style 描边子路径。

[CanvasRenderingContext2D.drawFocusIfNeeded()](1)
If a given element is focused, this method draws a focus ring around the current path.
如果给定的元素是聚焦的，这个方法围绕当前路径绘制一个聚焦环。

[CanvasRenderingContext2D.scrollPathIntoView()](1)
Scrolls the current path or a given path into the view.
滚动当前路径或给定一个路径到 view。 (This is an experimental technology)

[CanvasRenderingContext2D.clip()](1)
Creates a clipping path from the current sub-paths. Everything drawn after clip() is called appears inside the clipping path only. For an example, see Clipping paths in the Canvas tutorial.
从当前子路径创建一个剪切路径。所有在调用 clip()  之后的绘制的内容只会出现在剪切路径内。例如，见 Canvas 指南中的[剪切路径](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Compositing)。

[CanvasRenderingContext2D.isPointInPath()](1)
Reports whether or not the specified point is contained in the current path.
检测指定的点是否包含于当前路径内。


[CanvasRenderingContext2D.isPointInStroke()](1)
Reports whether or not the specified point is inside the area contained by the stroking of a path.
检测指定的点是否在路径描边区域内。

### 转换过程

Objects in the CanvasRenderingContext2D rendering context have a current transformation matrix and methods to manipulate it. The transformation matrix is applied when creating the current default path, painting text, shapes and Path2D objects. The methods listed below remain for historical and compatibility reasons as SVGMatrix objects are used in most parts of the API nowadays and will be used in the future instead.

在 CanvasRenderingContext2D 渲染上下文中的对象拥有当前转换过程矩阵和方法操纵它。当创建当前默认路径，打印文本，图形和 2D 路径对象时会应用转换过程矩阵。下面的方法列表因为历史和兼容 SVGMatrix 对象的原因现在可以使用但会在未来被替代。

[CanvasRenderingContext2D.currentTransform](1)
Current transformation matrix (SVGMatrix object).
当前转换过程矩阵 (SVGMatrix 对象)。

[CanvasRenderingContext2D.rotate()](1)
Adds a rotation to the transformation matrix. The angle argument represents a clockwise rotation angle and is expressed in radians.
增加一个旋转动作到转换过程矩阵。angle 参数代表顺时针旋转，用弧度表示。

[CanvasRenderingContext2D.scale()](1)
Adds a scaling transformation to the canvas units by x horizontally and by y vertically.
增加一个伸缩转换过程到 canvas， x 表示水平缩放 y 表示垂直缩放的距离。

[CanvasRenderingContext2D.translate()](1)
Adds a translation transformation by moving the canvas and its origin x horzontally and y vertically on the grid.
增加一个移动转换过程通过移动 canvas，参数针对 grid 的初始点，x 为水平移动，y 为垂直移动。

[CanvasRenderingContext2D.transform()](1)
Multiplies the current transformation matrix with the matrix described by its arguments.
根据传入的参数描述修改当前转换过程矩阵。


[CanvasRenderingContext2D.setTransform()](1)
Resets the current transform to the identity matrix, and then invokes the transform() method with the same arguments.
重设当前 transform 为指定矩阵，然后以同样的参数触发 transform() 方法。

[CanvasRenderingContext2D.resetTransform() ](1)
Resets the current transform by the identity matrix.
以指定矩阵重置当前 tansform。

### 合成

[CanvasRenderingContext2D.globalAlpha](1)
Alpha value that is applied to shapes and images before they are composited onto the canvas. Default 1.0 (opaque).
他们合成到 canvas 之前应用的图形和图像的 Alpha 值。默认是 1.0 (不透明)。

[CanvasRenderingContext2D.globalCompositeOperation](1)
With globalAlpha applied this sets how shapes and images are drawn onto the existing bitmap.
globalAlpha 与这个设置一起决定如何讲图形和图像绘制到已有的位图。



### 绘制图像

[CanvasRenderingContext2D.drawImage()](1)
Draws the specified image. This method is available in multiple formats, providing a great deal of flexibility in its use.
绘制指定的图像。这个方法可以应用多种格式，提供很大的灵活性。


### 像素操作

See also the [ImageData](1) object.
见 ImageData 对象。

[CanvasRenderingContext2D.createImageData()](1)
Creates a new, blank ImageData object with the specified dimensions. All of the pixels in the new object are transparent black.
以指定尺寸创建一个新的，空白的 ImageData 对象。在这个对象的所有像素点都是透明的黑色。

[CanvasRenderingContext2D.getImageData()](1)
Returns an ImageData object representing the underlying pixel data for the area of the canvas denoted by the rectangle which starts at (sx, sy) and has an sw width and sh height.
返回一个 ImageData 对象，表示 Canvas 指定范围内底层像素数据，从 (sx,sy) 开始的宽高。

[CanvasRenderingContext2D.putImageData()](1)
Paints data from the given ImageData object onto the bitmap. If a dirty rectangle is provided, only the pixels from that rectangle are painted.
从给定的 ImageData 对象打印数据到位图。如果提供了矩形，那么只有矩形内的像素会打印。


### 图像平滑

[CanvasRenderingContext2D.imageSmoothingEnabled ](1)
Image smoothing mode; if disabled, images will not be smoothed if scaled.
图像平滑模式；如果禁用，伸缩图像时将不会平滑。

### Canvas 状态

The CanvasRenderingContext2D rendering context contains a variety of drawing style states (attributes for line styles, fill styles, shadow styles, text styles). The following methods help you to work with that state:
CanvasRenderingContext2D 渲染上下文包含各种绘制风格状态 (线条风格，填充风格，阴影风格，文字风格等的属性)。下面的方法帮助你操作这些状态。

[CanvasRenderingContext2D.save()](1)
Saves the current drawing style state using a stack so you can revert any change you make to it using restore().
使用堆栈保存当前绘制风给状态，因此你可以使用 restore() 回滚你做的任意更改。

[CanvasRenderingContext2D.restore()](1)
Restores the drawing style state to the last element on the 'state stack' saved by save().
在 “状态堆栈” 恢复之前通过 save() 保存的绘制风格状态到最新的元素。

[CanvasRenderingContext2D.canvas](1)
A read-only back-reference to the HTMLCanvasElement. Might be null if it is not associated with a <canvas> element.
指向 HTMLCanvasElement 元素的只读对象。如果没有与 <canvas> 元素关联那么他有可能是 null。


### 点击区域

[CanvasRenderingContext2D.addHitRegion() ](1)
Adds a hit region to the canvas.
添加点击区域到 canvas。

[CanvasRenderingContext2D.removeHitRegion() ](1)
Removes the hit region with the specified id from the canvas.
移除 canvas 中特定 id 的点击区域

[CanvasRenderingContext2D.clearHitRegions() ](1)
Removes all hit regions from the canvas.
移除 canvas 中所有点击区域。
