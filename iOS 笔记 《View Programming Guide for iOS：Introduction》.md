layout: [post]
title: "iOS 翻译 《View Programming Guide for iOS：Introduction》"
date: 2015-04-25 08:34:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-View-Programming-Guide-for-iOS-Introduction"
---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503-CH1-SW2)





---
#关于窗口和视图
在 iOS 中，你会用到窗口和视图在屏幕上呈现你的应用程序内容。窗口没有任何可见的样式内容但它为应用程序的视图提供了基础容器。视图定义窗口上的你想填充一些内容的部分。例如，你可以用视图显示图片，文本，形状或一些它们的组合。你也可以使用视图组织和管理其他视图。

##一览
每个应用程序至少有一个窗口和一个视图呈现内容。UIKit 和其他系统框架提供预定义的视图让你呈现你的内容。这些视图的范围从简单按钮和文本标签到更多复杂的视图例如表格视图，选取视图，和滚动条视图。在预定义的视图无法满足你的需求的地方，你也可以自定义视图自己管理它的绘制和事件处理。

##视图管理你的应用程序的可见内容
视图是 [UIView](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/cl/UIView) 类 (或是它的子类) 的一个实例管理在你的应用程序窗口中的一个矩形区域。视图负责绘制内容，处理多点触碰事件，和管理子视图的布局。绘制用到的图形技术如 Core Graphic，OpenGL ES,或 UIKit 等在视图的矩形范围内绘制形状，图像，和文本。视图通过使用手势检测或直接处理触摸事件的方式响应矩形区域内的触摸事件。视图层次方面，父视图负责他们的子视图的定位和尺寸并且可以是动态化。子视图动态化修改的能力让你的视图适应不断变化的条件，例如界面旋转和动画效果。

你可以把视图作为能构造你的用户界面的积木。相对于只使用一个视图呈现你的所有内容，通常都是使用数个视图构造视图层次。每个层次的视图呈现你的用户界面的一部分和对特定的内容类型优化。例如，UIKit 有特定的视图分别呈现图像，文本或其他内容类型。

>相关章节：[View and Window Architecture](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/WindowsandViews/WindowsandViews.html#//apple_ref/doc/uid/TP40009503-CH2-SW1) ,[View](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW1)

##窗口协助视图显示
窗口是 [UIWindow](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/cl/UIWindow) 类的一个实例负责处理你的应用程序的用户界面总体呈现。窗口与视图 (或其他自己的视图控制器) 一起协作管理应用程序的互动，变更，可见的视图层次。大多数情况下，你的应用程序的窗口永远不用变更。在窗口被创建之后，它会一直保持原状并且只有通过它的变化显示视图。每一个应用程序至少有一个窗口在设备的主屏幕上显示应用程序的界面。如果有拓展显示设备连接到该设备，应用程序可以创建第二个窗口为拓展显示设备呈现内容。


>相关章节： [Windows](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingWindows/CreatingWindows.html#//apple_ref/doc/uid/TP40009503-CH4-SW1)

##动画效果为用户提供界面更改可见的信息反馈
动画效果为用户提供关于你的视图层次变化的可见反馈。系统为呈现模型视图和视图的不同分组之间的过渡定义了标准化的动画效果。并且，许多视图的属性也可以直接通过动画效果更改。例如你可以通过动画效果变更视图的透明度，屏幕的位置，它的尺寸，它的背景颜色，或其他属性。如果你直接对视图的底层的 Core Animation layer 对象工作，你还可以执行更多其他更好的动画效果。

>相关章节：[Animations](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW1)

##界面构造器的作用
界面生成器是一个让你使用图形化构造和配置你的应用程序窗口的视图的应用程序。通过使用界面生成器，你可以组合你的视图并把它们放置到 [nib 文件]()中,nib 是一个存储冻干版的视图和其他对象的资源文件。当你在运行时加载 nib 文件，这个对象的内部会重组到实际的对象让你的代码能以编程方式操作它们。

界面生成器可以非常简单的创建你的应用程序的用户界面。因为对界面生成器和 nib 文件的支持已被纳入了 iOS，只需要把一些 nib 文件合并到你的应用程序设计之中。

更多关于如何使用界面生成器的信息，见 *Interface Builder User Guide*。

关于如何用视图控制器管理它包含的视图的 nil 文件的信息，见 [View Controller Programming Guide for iOS](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457) 中的 [Creating Custom Content View Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101)。

##其他参考资料
因为视图是非常复杂和灵活的对象，它不可能再一个文档内覆盖它的所有行为，无论如何，其他的文档可以帮助你学习关于其他管理视图方面和你的整体用户界面。

视图控制器是管理你的应用程序的视图的重要一部分。在一个单一的视图层次中视图控制器管理所有的视图和在设备上呈现这些视图。更多关于视图控制器和他们扮演的角色信息，见 [*View Controller Programming Guide for iOS*](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)。

视图是你的应用程序中手势和触摸事件关键的接收者。更多关于使用手势检测和直接处理触摸事件的信息，见 [*Event Handling Guide for iOS*](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)。

自定义视图必须使用可绘制技术呈现它们的内容。关于使用这些技术绘制你的视图的信息，见 [*Drawing and Printing Guide for iOS*](https://developer.apple.com/library/ios/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010156)。

在标准化视图动画效果不能满足你的需求时，你可以使用 Core Animation。关于使用 Core Animation 实现动画效果的信息，见 [*Core Animation Programming Guide*](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004514)。


---
系列文章

*iOS 翻译 《View Programming Guide for iOS：Introduction》*

[*iOS 翻译 《View Programming Guide for iOS：View and Window Architecture》*](../iOS-Note-View-Programming-Guide-for-iOS-View-and-Window-Architecture) 

[*iOS 翻译 《View Programming Guide for iOS：Windows》*](../iOS-Note-View-Programming-Guide-for-iOS-Windows) 

[*iOS 翻译 《View Programming Guide for iOS：Views》* ](../iOS-Note-View-Programming-Guide-for-iOS-Views) 

[*iOS 翻译 《View Programming Guide for iOS：Animations》*](../iOS-Note-View-Programming-Guide-for-iOS-Animations) 

