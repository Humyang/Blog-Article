layout: [post]
title: "iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controler's Views》"
date: 2015-06-10 18:01:02
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "VCP6"

---

iOS 视图控制器编程指南：调整视图控制器的视图


<!-- more -->

[原文地址](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457-CH1-SW1)

记录关于学习过的 iOS 文档

---

# 调整视图控制器的视图

视图控制器拥有它自己的视图并管理着这些视图的内容。在处理中，视图控制器也管理着视图的子视图。但在大多数情况下，视图的 frame 不直接通过视图控制器设置。而是取决于视图控制器的视图如何显示。直接的说，它通过被用作显示它的对象配置。其它在应用程序中的条件，如状态栏的存在，也会引起 frame 的更改。因为这个原因，你的视图控制器应该准备好在视图的 frame 更改时调整它的视图的内容。

## 窗口设置它的根视图控制器的视图的 Frame

与窗口的根视图控制器关联的视图得到的 frame 基于窗口的特点。通过窗口设置的 frame 能基于以下几个因素更改：

* 窗口的 frame
* 状态栏是否显示
* 状态栏是否显示额外的信息 (例如处理来电时)
* 用户界面的方向 (横屏或竖屏)
* 保存在根视图控制器的属性 [wantsFullScreenLayout](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/wantsFullScreenLayout) 中的值

如果你的应用程序显示状态栏，应该收缩视图避免与状态栏重叠。因为如果状态栏是不透明的，这样就无法见到在它下面的内容或者与之交互。如果你的应用程序显示半透明的状态栏，你可以将视图控制器的属性 [wantsFullScreenLayout](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/wantsFullScreenLayout) 的值设置为 YES 使你的视图被显示为全屏幕。状态栏会绘制在视图的顶端的上方。

当你想最大化利用可用空间显示内容时全屏幕是很有用的。当内容显示在状态栏之下时，把内容放置在滚动视图内部使用户可以将内容从状态栏下方滚动出来。能够滚动你的视图是非常重要的因为用户无法与位于状态栏或其它半透明视图 (例如半透明导航栏和工具栏) 背后的内容交互。导航栏会自动添加滚动内容嵌入到你的滚动视图 (假设它是你的视图控制器的根视图) 填充导航栏所占据的高度；否则，你必须手动修改你的滚动视图的 [contentInset](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScrollView_Class/index.html#//apple_ref/occ/instp/UIScrollView/contentInset) 属性。

## 容器设置它的子级的视图的 Frame

当视图控制器是容器视图控制器的子级时，由它的父辈决定哪些子级可以显示。当它想显示视图时，它需要将视图作为子视图添加到它的视图层次结构中并设置它的 frame 适应它的界面。例如：

* 标签视图控制器为标签栏在视图的底部预留空间，它使用剩余的空间显示当前可见子级的视图。
* 导航视图控制器为导航栏在顶部预留空间。如果当前可见子级想让导航栏显示，它会把视图放置在屏幕的底部。视图的其余部分给子级填充。

子级获取它的 frame 从父辈一直到根视图控制器，根视图从窗口获取 frame。

## 被呈现的视图控制器使用 Presentation Context

当视图控制器通过其它视图控制器呈现时，它接收的 frame 是基于一个用作显示视图控制器的 presentation content。见 [Presentation Contexts Provide the Area Covered by the Pressented View Controller](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ModalViewControllers/ModalViewControllers.html#//apple_ref/doc/uid/TP40007457-CH111-SW17)。

## 弹出控制器设置所显示的视图的尺寸

由弹出控制器显示的视图控制器可以通过设置它自己的 [contentSizeForViewInPopover](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/contentSizeForViewInPopover) 属性决定想要的视图区域的尺寸。如果弹出控制器设置它自己的 [popoverContentSize](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIPopoverController_class/index.html#//apple_ref/occ/instm/UIPopoverController/popoverContentSize) 属性为不同尺寸，那么它的尺寸值会覆盖视图控制器所设置的值。要适配其他视图控制器使用的型号，可以使用弹出控制器的属性控制它的尺寸和位置。

## 视图控制器如何参与视图布局处理

当视图控制器的视图的尺寸更改时，它的子视图会响应适应新的可用空间。控制器的视图层次结构中的视图自己执行大部分工作通过使用布局约束和 autoresizing masks。不过，视图控制器也在不同的点被调用使它可以参与到布局处理中，这里是发生的事情：

1.视图控制器的视图调整为新的尺寸。
2.如果没使用自动布局，视图会根据它们的 autoresizing masks 调整。
3.视图控制器的方法 [viewWillLayoutSubviews](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/viewWillLayoutSubviews) 被调用。
4.视图的方法 [layoutSubviews](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instm/UIView/layoutSubviews) 被调用。如果自动布局被用作配置视图层次结构，它会通过执行下面的步骤更新布局约束：
	a.视图控制器的方法 [updateViewConstraints](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/updateViewConstraints) 被调用。
	b.[UIViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/cl/UIViewController) 类的方法 [updateViewConstraints](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/updateViewConstraints) 的实现调用视图的 [updateConstraints](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instm/UIView/updateConstraints) 方法。
	c.布局约束更新之后，重新计算新的布局并且重新定位视图。
5.视图控制器的方法 [viewDidLayoutSubVIews](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/viewDidLayoutSubviews) 被调用。

在理想情况下，视图自己执行所有需要的工作去重新定位它们自己，完全不需要视图控制器参与到布局处理中。通常，你可以在界面构造器内配置全部布局。但如果，视图控制器动态添加和移除视图，在界面构造器中配置的静态约束可能不工作。在这种情况下，视图控制器是一个很好的控制处理位置，因为通常视图它们自己在场景中只有有限的其它视图画面。这里是在视图控制器完成操作的最佳途径：

* 使用布局约束自动定位视图 (iOS 6 和之后)。通过重写 [updateViewConstraints](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/updateViewConstraints) 添加视图尚未配置的必须的布局约束。这个方法的实现必须调用 `[super updateViewConstraints]`。<br /> 更多关于自动布局的信息，见 [Auto Layout Guide](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010853)。
* 使用 autoresizing masks 的组合与代码手动定位视图 (iOS 5.x)。重写 [layoutSubviews](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instm/UIView/layoutSubviews) 并使用它重新定位不能通过调整 masks 自动定位的视图。<br />更多关于视图的自动调整属性和它们如何影响视图，见 [View Programming Guide for iOS](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)。

---

[*iOS 翻译 《View Controller Programming Guide for iOS：Introduction》*](../VCP0) 

[*iOS 翻译 《View Controller Programming Guide for iOS：View Controller Basics》*](../VCP1) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Content View Controllers》*](../VCP3)

[*iOS 翻译 《View Controller Programming Guide for iOS：Resource Management in View Controllers》*](../VCP4) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Responding to Display-Related Notifications》*](../VCP5) 

*iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controller's Views》*

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》*](../VCP7) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Supporting Multiple Interface Orientations》*](../VCP8) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controllers's Perspective》*](../VCP9) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》*](../VCP10) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Coordinating Efforts Between View Controllers》*](../VCP11) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Enabling Edit Mode in a View Controller》*](../VCP12) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Segues》*](../VCP13) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Container View Controllers》*](../VCP14)


