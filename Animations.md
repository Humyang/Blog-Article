layout: [post]
title: "iOS 笔记 《View Programming Guide for iOS：Animations》"
date: 2015-05-12 23:29:32
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-View-Programming-Guide-for-iOS-Animations"

---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503-CH1-SW2)

---

#动画效果
动画效果提供用户界面不同状态之间提供流体视觉过渡。在 iOS 中，动画效果在重新定位视图，更改视图的尺寸，从视图层次结构移除视图，和隐藏视图中广泛使用。你可以使用动画效果对用户传递反馈或实现有趣的视觉效果。

在 iOS 中，创建复杂的动画效果不需要你写任何绘制代码。这个章节描述的所有动画效果技术是使用 Core Animation 提供的内置支持。你要做的只是触发动画效果并让 Core Animation 处理单个框架的渲染。只需要简单的几行代码就可以创建非常复杂的动画效果。

##什么可以动画？
UIKit 和 Core Animation 都提供了动画效果的支持，但每个技术所提供支持的级别都有变化。在 UIKit 中，动画效果是使用 [UIView](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/cl/UIView) 对象执行。视图支持的动画效果基础集合覆盖许多常用任务。例如，你可以动画更改视图的属性或使用过渡动画效果把一个视图集合替换为另一个。

表 4-1 列出可动画的属性－有内置的动画效果支持的属性－由 UIView 类支持。可动画不意味着
动画效果会自动发生。更改这些属性的值正常的只会立刻更新属性 (和视图) 而没有动画效果。需要以动画更改，你必须在动画块内部更改属性的值。这在 [Animating Property Changes in a View](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW3) 中描述。

属性  | 你能做的更改
------------- | -------------
[frame](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/frame)  | 修改这个属性更改视图的尺寸和相对它的父视图的坐标系统的位置。(如果 transform 属性不包含恒等转换，修改 bounds 或 center 属性作为替代。)
[bounds](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/bounds)  | 修改这个属性更改视图的尺寸。
[center](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/center)  | 修改这个属性更改视图相对于它的父视图的坐标系统的位置。
[transform](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/transform)  | 修改这个属性相对于视图的中心点拉伸，旋转，或翻转。这个属性的转换效果总是在 2D 空间执行。(要执行 3D 的转换效果，你必须使用 Core Animation 动画视图的层对象。)
[alpha](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/alpha)  | 修改这个属性渐变视图的透明度。
[backgroundColor](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/backgroundColor)  | 修改这个属性更改视图的背景颜色。
[contentStretch](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/contentStretch)  | 修改这个属性更改视图的内容拉伸填充可用空间时的方式。

动画视图过渡是让你更改视图层次结构一种的方式，它在视图控制器提供的方式之外。尽管你应该使用视图控制器管理简明的视图层次结构，但许多时候你想替换视图层次结构的所有或一部分。在这种情况下，你可以使用基于视图的过渡效果动画视图的添加或移除。

在你想执行更复杂的动画效果的地方，或 UIView 类不支持的动画效果，你可以使用 Core Animation 和类的底层的层来创建动画效果。因为视图和层对象是紧密关联在一起的，更改视图的层会影响到视图它自己。使用 Core Animation，你可以为你的视图的层动画以下类型的变更：

- 层的尺寸和位置
- 在执行过渡效果时被用到的中心点
- 在 3D 空间过渡层或子层
- 从层的层次结构添加或移除层
- 层相对于兄弟层的 Z 字序。
- 层的阴影
- 层的边界 (包含层的边角是否为圆角)
- 调整尺寸操作期间拉伸层的一部分
- 层的不透明度
- 位于层的边界外部的子层的裁剪行为
- 当前的层内容
- 层的光栅化行为

> **说明：** 如果你的视图承载自定义层对象－意思是，层对象没有关联的视图－你必须使用 Core Animation 对它们动画更改。

虽然该章节涉及少数 Core Animation 行为，它只涉及到从视图的代码中初始化它们。更多完整的关于如何使用 Core Animation 动画层的信息，见 [*Core Animation Programming Guide*](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004514) 和 *Core Animations Cookbook*。

##在视图中动画更改属性
为了动画更改 [UIView](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/cl/UIView) 类的属性，你必须在动画效果块内部包裹这些更改。术语动画效果块 (*animation block*) 一般指代指定动画变化的代码。在 iOS 4 和以后版本，你可以使用块对象创建一个动画效果块。在早期的 iOS 版本，是使用 UIView 类指定的类方法标记动画效果块的开始和结束。这些技术都支持同样的配置选项和提供相同控制数量的动画执行过程。不管怎样，基于块的方法有可能的情况下是首选的。

下面章节的焦点在为了动画更改视图属性而使用的代码。关于如何在视图之间创建动画过渡效果，见 [Creating Animated Transitions Between Views](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW9)。

###使用基于块的方法开始动画
在 iOS 4 之后的版本，可以使用基于块的类方法开始动画效果。这里是几个为动画效果块提供了不同配置级别的基于块的方法。

- [animateWithDuration:animations:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/animateWithDuration:animations:)
- [animateWithDuration:animations:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/animateWithDuration:animations:completion:)
- [animateWithDuration:delay:options:animations:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/animateWithDuration:delay:options:animations:completion:)

因为这些是类方法，这些动画效果块创建后是没绑定到单个视图的。因此，你可以使用这些方法创建涉及多个视图更改的单个动画效果。例如，清单 4-1 的代码用超过一秒的时间周期在淡出另一个视图同时淡入一个视图。当这个代码执行时，指定的动画效果立刻在另一个线程开始以避免锁定当前线程或应用程序主线程。

**清单 4-1** 执行简单的基于块的动画效果

```objc
[UIView animateWithDuration:1.0 animations:^{
        firstView.alpha = 0.0;
        secondView.alpha = 1.0;
}];

```

上面例子中的动画效果只执行一次使用 Easy-in,Easy-out 的动画效果曲线。如果你想更改默认动画效果参数，你必须使用 animateWithDuration:delay:options:animations:completion: 方法执行你的动画效果。这个方法让你自定义下面的动画效果参数：

- 开始动画效果之前延迟使用
- 动画效果期间使用的时间曲线类型
- 动画效果应该重复的时间数字
- 当动画效果结束后是否应当自动倒转它自己
- 当动画效果正在处理时触摸事件是否应当发出
- 动画效果在开始之前是应该打断正在处理的动画效果或等待执行完成

其它的 animateWithDuration:animations:completion: 和 animateWithDuration:delay:options:animations:completion: 方法可以指定完后的处理块。你可以使用完成处理为你的应用程序指定动画效果完成后的操作。完成处理也是连结单个动画效果到一起的一种方式。

清单 4-2 显示第一个动画执行完成之后使用完成处理初始化新的动画效果的例子。首先调用 animateWithDuration:delay:options:animations:completion: 设置淡出动画效果和配置一些自定义选项。当动画效果完成时，它的完成处理开始运行并设置第二半动画效果，延迟之后淡回视图。

使用完成处理时连结多个动画效果的主要方式。

**清单 4-2** 创建一个动画效果块和自定义选项。

```objc

- (IBAction)showHideView:(id)sender
{
    // Fade out the view right away
    [UIView animateWithDuration:1.0
        delay: 0.0
        options: UIViewAnimationOptionCurveEaseIn
        animations:^{
             thirdView.alpha = 0.0;
        }
        completion:^(BOOL finished){
            // Wait one second and then fade in the view
            [UIView animateWithDuration:1.0
                 delay: 1.0
                 options:UIViewAnimationOptionCurveEaseOut
                 animations:^{
                    thirdView.alpha = 1.0;
                 }
                 completion:nil];
        }];
}


```

> **重要提示:**修改一个属性的值而属性涉及到的动画效果已经在处理中它不会停止当前的动画效果。而且，当前的动画效果会继续并且会动画到你已分配给属性的新值。


###使用 begin/commit 方法开始动画效果
如果你的应用程序运行在 iOS 3.2 之前的版本，你必须使用 UIView 的类方法 [beginAnimations:context:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/beginAnimations:context:) 和 [commitAnimations](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/commitAnimations) 定义你的动画效果块。这些方法标记了你的动画效果块的开始和结束。在 commitAnimations 方法调用之后在这些方法之间修改的属性会动画成新值。动画效果的执行在次要的线程中避免锁定当前线程或应用程序的主线程。

>**说明：**如果你在 iOS 4 或之后的版本，你应该使用基于块的方法动画你的内容。关于如何使用这些方法，见 [Starting Animations Using the Block-based Methods](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW4)。

清单 4-3 显示的代码实现与清单 4-1 相同的行为但使用的是 begin/commit 方法。如清单 4-1，这个代码用超过一秒的时间在另一个视图淡出时淡入一个视图。不管怎样，在这个例子中，你必须使用单独的方法设置动画的长短。

**清单 4-3** 执行一个简单的 begin/commit 动画效果

```objc
    [UIView beginAnimations:@"ToggleViews" context:nil];
    [UIView setAnimationDuration:1.0];
 
    // Make the animatable changes.
    firstView.alpha = 0.0;
    secondView.alpha = 1.0;
 
    // Commit the changes and perform the animation.
    [UIView commitAnimations];

```

默认情况下，所有可动画的属性在动画效果块内的更改都会被动画。如果你只想动画一些更改但其他的不动画，使用 [setAnimationsEnabled:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationsEnabled:) 方法暂时禁用动画效果，更改你不想被动画的属性，然后再次调用 setAnimationsEnabled: 重新启用动画效果。你可以调用类方法 [areAnimationsEnabled](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/areAnimationsEnabled) 判断动画效果当前是否启用。

> **说明：**修改一个属性的值而属性涉及到的动画效果已经在处理中它不会停止当前的动画效果。而且，当前的动画效果会继续并且会动画到你已分配给属性的新值。

####配置 Begin/Commit 动画效果参数
要为 begin/commit 动画效果块配置动画效果参数，你可以任意使用几个 UIView 的类方法。表 4-2 列出这些方法和描述如何使用它们配置你的动画效果。大多数这些方法只能从 begin/commit 动画效果内部被调用但一些也可以被基于块的动画效果使用。如果你没在动画效果中调用这些方法中的一个，相应的属性会使用默认值。更多关于每个方法关联的默认值，见 [UIView Class Reference](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/doc/uid/TP40006816) 中这些方法的描述。


**表 4-2**配置动画效果块的方法

方法 | 用途 
------------ | ------------- 
[setAnimationStartDate:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationStartDate:) <br /> [setAnimationDelay:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDelay:) | 使用这些方法中的一个指定执行过程什么时候开始执行。如果指定的开始时间已经超过 (或延时为 0)，动画效果会尽可能早开始。
[setAnimationDuration:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDuration:) | 使用这个方法设置在执行动画效果时的时间周期
[setAnimationCurve:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationCurve:) | 使用这个方法设置动画效果的时间曲线。这个控制动画效果是否线性执行或在某些时候改变速度。
[setAnimationRepeatCount:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationRepeatCount:) <br /> [setAnimationRepeatAutoreverses:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationRepeatAutoreverses:) | 使用这个方法设置动画效果的重复时间的数字和每次动画效果的完整周期结束是否逆转执行。更多关于使用这些方法的信息，见  [Implementing Animations That Reverse Themselves](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW15)。
[setAnimationDelegate:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDelegate:) <br />[setAnimationWillStartSelector:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationWillStartSelector:) <br />[setAnimationDidStopSelector:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDidStopSelector:) | 使用这些方法在动画效果之前或之后立即执行代码。更多关于使用委托的信息，见 [Configuring an Animation Delegate](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW8)
[setAnimationBeginsFromCurrentState:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationBeginsFromCurrentState:) | 使用这个方法立刻停止所有之前的动画效果并从停止的地方开始新的动画效果。如果你传入 NO 到方法中，而不是 YES，新的动画效果不会立刻开始执行直到之前的动画效果停止。

清单 4-4 显示的代码被用作实现与清单 4-2 中的代码的相同的行为但使用 begin/commit 方法。如前，代码淡出一个视图，等待一秒，然后淡化它回来。为了实现动画效果的第二部分，代码设置动画效果委托和实现停止处理方法。这个处理方法然后设置动画效果的第二部分然后运行它。

**清单 4-4** 使用 begin/commit 方法配置动画效果参数

```objc
// This method begins the first animation.
- (IBAction)showHideView:(id)sender
{
    [UIView beginAnimations:@"ShowHideView" context:nil];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseIn];
    [UIView setAnimationDuration:1.0];
    [UIView setAnimationDelegate:self];
    [UIView setAnimationDidStopSelector:@selector(showHideDidStop:finished:context:)];
 
    // Make the animatable changes.
    thirdView.alpha = 0.0;
 
    // Commit the changes and perform the animation.
    [UIView commitAnimations];
}
 
// Called at the end of the preceding animation.
- (void)showHideDidStop:(NSString *)animationID finished:(NSNumber *)finished context:(void *)context
{
    [UIView beginAnimations:@"ShowHideView2" context:nil];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseOut];
    [UIView setAnimationDuration:1.0];
    [UIView setAnimationDelay:1.0];
 
    thirdView.alpha = 1.0;
 
    [UIView commitAnimations];
}



```

####配置动画效果委托
如果你想在动画效果之前或之后立即执行一些代码，你必须为你的 begin/commit 动画效果块关联一个委托对象和一个开始或停止选择器。使用 UIVIew 的类方法 [setAnimationDelegate:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDelegate:) 设置委托对象和用类方法 [setAnimationWillSelector:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationWillStartSelector:) 和 [setAnimationDidStopSelector:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationDidStopSelector:) 设置开始和停止选择器。在动画效果的期间，动画效果系统在相应的时间调用你的委托对象给你机会执行你的代码。

你的动画效果委托方法特征需要像下面一样：

```objc
- (void)animationWillStart:(NSString *)animationID context:(void *)context;
- (void)animationDidStop:(NSString *)animationID finished:(NSNumber *)finished context:(void *)context;

```

两个方法中的参数 *animationID* 和 *context* 都是你在动画效果块开始时传递给 beginAnimations:context: 的相同参数：

- *animationID*－应用程序提供的字符串用来标识一个动画效果。
- *context*－应用程序提供的对象你可以对委托传递额外的信息。

setAnimationDidStopSelector: 选择器方法有一个额外的参数－一个布尔值如果是 YES 动画效果会运行完成。如果这个参数的值是 NO，动画效果会过早的被另一个动画效果取消或停止。

>**说明：** 尽管动画效果委托能用在基于块的方法中，但那里通常不需要使用它们。作为代替，把想在动画效果之前运行的代码放置在块的开始和把想在动画效果结束后运行的代码放置在完成处理。


###嵌套动画效果块
你可以对动画效果块的一部分指定不同的计时和配置选项通过嵌套额外的动画效果块。如名称所示，嵌入动画效果块是在已有的动画效果块内部创建一个新的动画效果块。已嵌入的动画效果与它的父动画效果同时开始但根据它自己的配置选项运行 (大部分)。默认情况下，嵌套动画效果继承父辈的持续时间和动画曲线但即使是这些选项也可以按需要重写。

清单 4-5 的说明如何使用嵌套动画效果修改计时，持续时间，和一些动画效果在整个组中的行为。在这个例子中，两个视图开始淡化直到完全透明，但 anotherView 对象的透明度在最终隐藏之前会来回变更一段时间。[UiViewAnimationOptionOverrideInheritedCurve](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/c/econst/UIViewAnimationOptionOverrideInheritedCurve) 和 [UIViewAnimationOptionOverrideInheritedDuration](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/c/econst/UIViewAnimationOptionOverrideInheritedDuration) 键用作在嵌套动画效果块中允许第一个动画效果的曲线和持续时间值被第二个动画效果修改。如果没有这些键，外部动画效果块的持续时间和曲线值会被用作代替。

**清单 4-5** 拥有不同配置信息的嵌套动画效果

```objc
[UIView animateWithDuration:1.0
        delay: 1.0
        options:UIViewAnimationOptionCurveEaseOut
        animations:^{
            aView.alpha = 0.0;
 
            // Create a nested animation that has a different
            // duration, timing curve, and configuration.
            [UIView animateWithDuration:0.2
                 delay:0.0
                 options: UIViewAnimationOptionOverrideInheritedCurve |
                          UIViewAnimationOptionCurveLinear |
                          UIViewAnimationOptionOverrideInheritedDuration |
                          UIViewAnimationOptionRepeat |
                          UIViewAnimationOptionAutoreverse
                 animations:^{
                      [UIView setAnimationRepeatCount:2.5];
                      anotherView.alpha = 0.0;
                 }
                 completion:nil];
 
        }
        completion:nil];


```

如果你使用 begin/commit方法创建你的动画效果，嵌套的工作与基于块的方法非常相似。每个连续调用 beginAnimations:context: 内已经打开一个动画效果块你可以按需要进行配置创建新的嵌套动画效果块。任何配置的更改都会在最近打开的动画效果块中应用。所有动画效果块在提交和执行之前都必须闭合和调用 [commitAnimations](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/commitAnimations)。


###实现逆转它自己的动画效果
当创建与重复计数关联的可逆转动画效果时，考虑为重复计数指定一个非整数值。对于一个自动逆转的动画效果，动画效果的每一个完整周期包含动画原始值到新值然后再返回。如果你想动画效果在新值结束，添加 0.5 到重复计数使动画效果完成所需的额外一半周期在新值结束。如果不包含这一半的步骤，你的动画效果将在原始值与新值之间重复，这可能不是你想要的视觉效果。


##创建视图之间的动画过渡效果
视图过渡效果帮助你掩盖视图层次结构中与增加，移除，隐藏或显示视图关联的突然变化。使用视图过渡效果实现下面类型的变更：

- **更改已有视图的子视图可见性。**当你想对已有的视图时做相对较小的更改时通常选择这个选项。
- **替换视图层次结构中的一个视图成不同的视图。**当你想替换屏幕上所有的或大部分的视图层次结构时通常选择这个选项。


>**重要提示：**视图的过渡效果不能与视图控制器开始的过渡效果混淆，例如模态视图控制器的呈现或推新的视图控制器到导航堆栈之上。视图过渡效果只影响到视图层次结构，而视图控制器过渡效果还能更改活跃的视图控制器。因此，对于视图过渡效果，当你开始过渡效果时视图控制器是活跃，当过渡效果完成时会保留活跃。<br /> 更多关于如何使用视图控制器呈现新的内容，见 [*View Controller Programming Guide for iOS*](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)。



###更改视图的子视图

更改视图的子视图使你可以对视图做适度的修改。例如，你可以通过添加或移除子视图切换父视图两个不同状态之间。动画效果完成时，显示的是同样的视图但它的内容是不同的。

在 iOS 4 和之后，使用 [transitionWithView:duration:options:animations:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/transitionWithView:duration:options:animations:completion:) 方法开始对视图的过渡动画效果。在动画效果块中传递这个方法，这个方法只会更改正常的动画与子视图相关的显示，隐藏，添加，或移除。动画效果的这个限制使视图可以创建动画前和动画后的视图快照版本并在在两个图像之间动画，这样更高效。如果你需要动画其他更改，当调用这个方法时你可以包含 [UIVIewAnimationOptionAllowAnimatedContent](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/c/econst/UIViewAnimationOptionAllowAnimatedContent) 选项。包含这个选项防止视图创建快照并直接动画所有更改。

清单 4-6 例子说明如何使用过度动画效果使它看起来像已经添加一个新的文本输入页面。在这个例子中，主视图包含两个嵌入式文本视图。文本视图使用相同的配置，但一个视图可见时其它总是隐藏。当用户触击按钮创建新页面时，这个方法切换两个视图的可见性，对用户显示一个新的空页面和一个空的文本视图准备接收文本。过渡效果完成之后，视图使用一个私有方法从旧页面保存文本并重置当前隐藏的文本视图使它可以稍后重用。视图然后整理它的指针当如果用户仍需要其他新页面时它可以做同样的事情。

**清单 4-6**将已存在的文本视图交换为空文本视图

```objc
- (IBAction)displayNewPage:(id)sender
{
    [UIView transitionWithView:self.view
        duration:1.0
        options:UIViewAnimationOptionTransitionCurlUp
        animations:^{
            currentTextView.hidden = YES;
            swapTextView.hidden = NO;
        }
        completion:^(BOOL finished){
            // Save the old text and then swap the views.
            [self saveNotes:temp];
 
            UIView*    temp = currentTextView;
            currentTextView = swapTextView;
            swapTextView = temp;
        }];
}

```

如果你需要在 iOS 3.2 或更早版本执行视图过渡效果，你可以使用 [setAnimationTransition:forView:cache:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/setAnimationTransition:forView:cache:) 方法为转换效果指定参数。你为这个方法传递的视图与传递给 transitionWithView:duration:options:animations:completion: 方法的第一个参数是相同一个。清单 4-7 显示你所需要创建的动画效果块的基础结构。注意实现完整的块在清单 4-6 中显示，你将需要配置一个动画效果委托与 did-stop 的处理，在 [Configuring an Animation Delegate](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW8) 中描述。

**清单 4-7**使用 begin/commit 方法更改子视图

```objc
    [UIView beginAnimations:@"ToggleSiblings" context:nil];
    [UIView setAnimationTransition:UIViewAnimationTransitionCurlUp forView:self.view cache:YES];
    [UIView setAnimationDuration:1.0];
 
    // Make your changes
 
    [UIView commitAnimations];



```


###将视图替换成不同视图
当你想界面发生显著变化时可以使用替换视图。因为这个技术只交换视图 (不是视图控制器)，你需要负责设计你的应用程序的相应的控制器对象。这个技术使用一些标准的过渡效果用简单的方式快速呈现新视图。

在 iOS 4 和之后，使用 [transitionFromView:toView:duration:options:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/transitionFromView:toView:duration:options:completion:) 方法过渡两个视图之间。这个方法实际上从你的视图层次结构移除第一个视图并插入其他的，因此如果你想保持第一个视图你应该确认有对它的引用。如果你想隐藏视图而不是从视图层次结构移除它们，传入 [UIViewAnimationOptionShowHideTransitionViews](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/c/econst/UIViewAnimationOptionShowHideTransitionViews) 键作为选项之一。

清单 4-8 的代码用作交换被单独视图控制器管理的两个主视图之间。在这个例子中视图控制器的根视图总是显示两个子视图中的一个 (primaryView 或 secondaryView)。每个视图都呈现同样的内容但都以不同的方式。视图控制器使用成员变量 displayingPrimary (一个布尔值) 追踪在给定时间显示哪一个视图是显示的。翻转方向的更改根据哪个视图正在显示。

**清单 4-8**在视图控制器中的两个视图之间切换

```objc

- (IBAction)toggleMainViews:(id)sender {
    [UIView transitionFromView:(displayingPrimary ? primaryView : secondaryView)
        toView:(displayingPrimary ? secondaryView : primaryView)
        duration:1.0
        options:(displayingPrimary ? UIViewAnimationOptionTransitionFlipFromRight :
                    UIViewAnimationOptionTransitionFlipFromLeft)
        completion:^(BOOL finished) {
            if (finished) {
                displayingPrimary = !displayingPrimary;
            }
    }];
}

```

>**说明：**除了交换视图外，你的视图控制器代码还需要管理主视图和次视图的读取和卸载。关于如何使用视通控制器加载和卸载，见 [*View Controller Programming Guide for iOS*](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)。


##连结多个动画效果到一起
UIView 动画效果接口提供连结单个动画效果块的支持使它们能按顺序执行替代同时执行。如何处理连结动画效果块取决于你是使用基于块的动画效果方法或 begin/commit 方法：

- 对使用基于块的动画效果，使用 [animateWithDuration:animations:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/animateWithDuration:animations:completion:) 和[animateWithDuration:delay:options:animations:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/clm/UIView/animateWithDuration:delay:options:animations:completion:) 方法提供的完成处理执行任意后续动画效果。
- 对使用 begin/commit 动画效果，对动画效果分配一个委托对象和一个 did-stop 选择器。关于如何对你的动画效果分配委托对象，见 [Configuring an Animation Delegate](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW8)。

一个替代连结多个动画效果到一起的方式是使用嵌套动画效果设置不同的延迟系数在不同时间开始动画效果。更多关于如何嵌套动画效果的信息，见 [Nesting Animation Blocks](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW11)。

##一起动画视图和层的更改

应用程序可以按需要自由的混合基于视图和基于层的动画效果代码但处理动画效果参数的配置取决于谁是层的拥有者。更改视图拥有的层等于更改视图它自己，任何你对层的属性应用的动画效果都遵从当前基于视图的动画效果块的动画效果参数。如果是自己创建的层这说法不正确。自定义层对象忽略基于视图的动画效果块的参数并使用默认的核心动画效果参数作为替代。

如果你想为你创建的层自定义动画效果参数，你必须直接使用 Core Animation。通常，使用 Core Animation 制作层动画涉及到创建 [CABasicAnimation](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CABasicAnimation_class/index.html#//apple_ref/occ/cl/CABasicAnimation) 对象或 [CAAnimation](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CAAnimation_class/index.html#//apple_ref/occ/cl/CAAnimation) 的具体子类。然后添加动画效果到相应的层。你可以在基于视图的动画效果块的外部或内部应用这个动画效果。

清单 4-9 显示在同一时间修改视图和自定义层的动画效果。视图在这个例子中包含一个在它的边界的中心的自定义 [CALayer](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CALayer_class/index.html#//apple_ref/occ/cl/CALayer) 对象。这个动画以逆时针旋转视图而层以顺时针旋转。因为是以相反方向旋转，层保存相对屏幕的原始方向并且不会出现明显旋转。视图在层的下面旋转 360 度并返回它的原始方向。这个例子主要演示如何混合视图和层的动画效果。这个类型的混合不应该用在需要精确定时的情景下。

**清单 4-9** 混合视图和层的动画效果

```objc

[UIView animateWithDuration:1.0
    delay:0.0
    options: UIViewAnimationOptionCurveLinear
    animations:^{
        // Animate the first half of the view rotation.
        CGAffineTransform  xform = CGAffineTransformMakeRotation(DEGREES_TO_RADIANS(-180));
        backingView.transform = xform;
 
        // Rotate the embedded CALayer in the opposite direction.
        CABasicAnimation*    layerAnimation = [CABasicAnimation animationWithKeyPath:@"transform"];
        layerAnimation.duration = 2.0;
        layerAnimation.beginTime = 0; //CACurrentMediaTime() + 1;
        layerAnimation.valueFunction = [CAValueFunction functionWithName:kCAValueFunctionRotateZ];
        layerAnimation.timingFunction = [CAMediaTimingFunction
                        functionWithName:kCAMediaTimingFunctionLinear];
        layerAnimation.fromValue = [NSNumber numberWithFloat:0.0];
        layerAnimation.toValue = [NSNumber numberWithFloat:DEGREES_TO_RADIANS(360.0)];
        layerAnimation.byValue = [NSNumber numberWithFloat:DEGREES_TO_RADIANS(180.0)];
        [manLayer addAnimation:layerAnimation forKey:@"layerAnimation"];
    }
    completion:^(BOOL finished){
        // Now do the second half of the view rotation.
        [UIView animateWithDuration:1.0
             delay: 0.0
             options: UIViewAnimationOptionCurveLinear
             animations:^{
                 CGAffineTransform  xform = CGAffineTransformMakeRotation(DEGREES_TO_RADIANS(-359));
                 backingView.transform = xform;
             }
             completion:^(BOOL finished){
                 backingView.transform = CGAffineTransformIdentity;
         }];
}];

```

>**说明：**在清单 4-9 中，你也可以在基于视图的动画效果块外部创建和应用 CABasicAnimation 对象实现同样的结果。所有的动画效果最终依靠 Core Animatino 为它们执行。因此，如果它们提交的时间大约相同，它们会一起运行。

如果需要精确定时基于视图与层之间的动画效果，推荐你使用 Core Animation 创建全部动画效果。你可能找到一些使用 Core Animation 更容易执行的动画效果。例如，在清单 4-9 中基于视图的旋转中需要多个步骤实现超过 180 度的旋转，而在 Core Animation 的部分使用旋转值函数通过一个中间值完成开始到结束的旋转。

更多关于如何使用 Core Animation 创建和配置动画效果的信息，见 [*Core Animation Programming Guide*](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004514) 和 **Core Animation Cookbook**。

---


系列文章

[*iOS 笔记 《View Programming Guide for iOS：Introduction》*](../iOS-Note-View-Programming-Guide-for-iOS-Introduction) 

[*iOS 笔记 《View Programming Guide for iOS：View and Window Architecture》*](../iOS-Note-View-Programming-Guide-for-iOS-View-and-Window-Architecture) 

[*iOS 笔记 《View Programming Guide for iOS：Windows》*](../iOS-Note-View-Programming-Guide-for-iOS-Windows) 

[*iOS 笔记 《View Programming Guide for iOS：Views》* ](../iOS-Note-View-Programming-Guide-for-iOS-Views) 

*iOS 笔记 《View Programming Guide for iOS：Animations》*
