# CSS Margin (一) 负 Margin

在一次开发时想使用 Marin 合并但不记得具体细节，就 Google 了一下资料，发现了这两篇详细介绍 Marin 的文章。

http://www.hicss.net/i-know-you-do-not-know-the-negative-margin/

http://www.hicss.net/do-not-tell-me-you-understand-margin/

因为 Margin 用得挺多了，所以基础的不记录了，只做一下以前不知道的知识的笔记。

## 总结

Margin 主要影响到元素与周边元素的关系，不管传入正数负数，所以一定程度上可以替代 relative 和 absolute。

这里对几种情况进行测试一下。

### 父子元素的关系

首先测试父子关系的 div 元素。有三个 div，其中一个为父 div，两个子 div，它们 的 display 都是 block。

下面第一个子 div 称为**老大**，第二个子 div 称为**老二**，主要修改老大的 margin，老二主要作为参照物。


#### 测试 1

修改老大的 `margin: -10px 0 0 0; `，效果: 整体元素往上偏移。同理如果为正数则往下偏移。

加上老大的 `margin-top` 为 10px,如果设置父 div 的 `margin-top` 大于 10 px，则按照父 div 的数值移动。这现象被称为`垂直外边距合并`。

如果老大和父 div 的正负数相反，则会进行相加，例如老大 `margin: -10px 0 0 0; `，父 `margin: 10px 0 0 0; `，那么元素 margin 被抵消，位置保持不变。



> 设置老大的 display 为 **inline**,这时老大的 margin-top 和 margin－bottom 都不起作用了。同时设置老二的 display 为 inline，老大的 margin-top 和 margin－bottom 也是没作用。
> 但是 margin-left 和 margin-right 还是有作用的。


> 设置老大的 display 为 **inline-block** 时，不会影响父 div 的位置，但还是会影响同级元素的位置。



### 用途

#### 负 margin 替代 relative/absolute

#### Tab 选项卡

#### 鳞片式导航