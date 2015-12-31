layout: [post]
title: "iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》"
date: 2015-06-10 18:01:03
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "VCP7"

---

iOS 视图控制器编程指南：在响应链中使用视图控制器


<!-- more -->

[原文地址](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457-CH1-SW1)

记录关于学习过的 iOS 文档

---

# 在响应链中使用视图控制器

视图控制器是 [UIResponder](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIResponder_Class/index.html#//apple_ref/occ/cl/UIResponder) 类的后代因此它有处理各种事件的能力。当视图不处理给定的事件时，它会传递事件给它的父视图，逐渐往视图层次结构的上方传递一直到根视图。不过，如果队列中的视图由视图控制器管理，它会把事件传递给它的父视图之前传递给视图控制器对象。因此，视图控制器可以响应它的不由它的视图处理的事件。如果视图控制器也不处理该事件，通常该事件会移动到视图的父视图。

## 响应链定义事件如何被传播到应用程序

图 7-1 演示视图层次结构内的事件流程。假设你有一个嵌入到屏幕尺寸大小的通用视图对象中的自定义视图，而它们又是被视图控制器管理。到达自定义视图 frame 的事件会交由视图处理。如果你的视图不处理这个事件，它会继续传递到父视图。**因为通用视图对象不处理事件**，它会首先传递这些事件到它的视图控制器。如果视图控制器不处理事件，事件会继续传递到通用视图对象 `UIView` 的父视图，在这个例子中它是 window 对象。

**图 7-1** 响应链中的视图控制器
![](./event_passing_2x.png)

> **注意：**视图控制器和它的视图之间的消息传递关系被视图控制器私有管理并且不能通过应用程序以编程方式更改。

虽然你可能不想在视图控制器中处理特殊的触摸事件，你可以用它处理基于运动的事件。你也可以使用它协调第一个响应者的设置和更改。更多关于事件如何在 iOS 应用程序中分布和处理，见 [Event Handling Guide for iOS](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)。

---

[*iOS 翻译 《View Controller Programming Guide for iOS：Introduction》*](../VCP0) 

[*iOS 翻译 《View Controller Programming Guide for iOS：View Controller Basics》*](../VCP1) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Content View Controllers》*](../VCP3)

[*iOS 翻译 《View Controller Programming Guide for iOS：Resource Management in View Controllers》*](../VCP4) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Responding to Display-Related Notifications》*](../VCP5) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controller's Views》*](../VCP6) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》*

[*iOS 翻译 《View Controller Programming Guide for iOS：Supporting Multiple Interface Orientations》*](../VCP8) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controllers's Perspective》*](../VCP9) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》*](../VCP10) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Coordinating Efforts Between View Controllers》*](../VCP11) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Enabling Edit Mode in a View Controller》*](../VCP12) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Segues》*](../VCP13) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Container View Controllers》*](../VCP14)


