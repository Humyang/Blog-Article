layout: [post]
title: CSS Margin (一) 负 Margin
date: 2016-01-13 14:28:21
tags:
- 前端
categories:
- 前端
- CSS
---

简单总结了对负 margin 的理解，和一些用途。

<!-- more -->

---

# CSS Margin (一) 负 Margin

偶然发现了两篇详细介绍 Marin 的文章：

http://www.hicss.net/i-know-you-do-not-know-the-negative-margin/

http://www.hicss.net/do-not-tell-me-you-understand-margin/

因为学到了熟悉的内容但陌生的知识，所以做一下总结。

## 总结

Margin 主要影响到元素与周边元素的关系，不管传入正数负数，所以一定程度上可以替代 relative 和 absolute。

这里对几种情况进行测试一下。

### 父子元素的关系

首先测试父子关系的 div 元素。有三个 div，其中一个为父 div，两个子 div，它们 的 display 都是 block。

下面第一个子 div 称为 A，第二个子 div 称为 B，主要修改 A 的 margin， B 主要作为参照物。


#### 测试， 修改 A 的 margin：

此时三个 div 的 display 都是 block。

修改 A 的 `margin: -10px 0 0 0; `，效果: 整体元素往上偏移。同理如果为正数则往下偏移。

若 A 的 `margin-top` 为 10px,如果父 div 的 `margin-top` 大于 10 px，则按照父 div 的数值移动。这现象被称为`垂直外边距合并`。

如果 A 和父 div 的正负数相反，则会进行相加，例如 A  `margin: -10px 0 0 0; `，父 `margin: 10px 0 0 0; `，那么元素 margin 被抵消，位置保持不变。



> 设置 A 的 display 为 **inline**,这时 A 的 margin-top 和 margin－bottom 都不起作用了。同时设置 B 的 display 为 inline， A 的 margin-top 和 margin－bottom 也是没作用。
> 但是 margin-left 和 margin-right 还是有作用的。 margin-right 正负值不会改变 A 的位置，但如果正数过大会影响 B 的位置。
> margin-left 正负数都可以影响 A 的位置。

> 设置 A 的 display 为 **inline-block** 时， 修改 A 的 margin 不会影响父 div 的位置，但会影响同级元素的位置。

继续测试时才发现元素组合太多了，根本测试不完，理解原理才最关键，在后面的文章中学习。


### 负 margin 用途

#### 负 margin 替代 relative/absolute

例如在 img 元素上显示另一个元素的内容，以前是用 relative 或 absolute 调整坐标的方式，现在也可以用负 margin 替代了。

#### Tab 选项卡

让元素上移一个像素点，使选项卡的下边界消失

#### 鳞片式导航

就是多个选项卡重叠在一起。
