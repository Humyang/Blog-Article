layout: [post]
title: "iOS 翻译 《View Controller Programming Guide for iOS：Introduction》"
date: 2015-05-14 08:34:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "VCP0"

---

iOS 视图控制器编程指南：介绍

<!-- more -->

[原文地址](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457-CH1-SW1)

记录关于学习过的 iOS 文档

---

# 关于视图控制器

视图控制器是连接应用程序的数据和它的视觉外观之间的重要环节。每当一个 iOS 应用程序显示用户界面，显示的内容通过一个视图控制器或一组视图控制器管理，彼此之间协调。因此，视图控制器为你构建你的应用程序提供了骨骼框架。

iOS 提供了许多内置的视图控制器类对标准用户界面的支持，例如导航栏和标签栏。作为开发应用程序的一部分，你也可以实现一个或多个自定义控制器显示特定的内容。

![](./navigation_interface_2x.png)

## 一览
视图控制器在 Model-View-Controller (MVC) 设计模式中是传统的控制器对象，但它们做得更多。视图控制器对所有 iOS 应用程序提供许多常用行为。对于某些行为，基础类提供解决方案的一部分，在你的视图控制器子类实现自定义代码完成剩余部分。例如，当用户旋转设备时，标准的实现过程会尝试旋转用户界面；但是，你的子类决定用户界面是否应该旋转，如果是，应该对视图配置如何应对新方向的更改。因此，结构化基础类和与具体子类的组合使你轻松的自定义应用程序的行为同时符合平台设计准则。

### 视图控制器管理视图的集合
视图控制器管理你的应用程序的用户界面分离部分。根据要求，它提供可以显示或交互的视图。通常，这个视图是复杂的视图层次结构的根视图－按钮，开关，和其它在 iOS 已有实现的用户界面元素。视图控制器扮演视图层次结构的中央协调机构，处理视图和任意相应的控制器或数据对象之间的交换。

> **相关章节：**[View Controller Basics](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/AboutViewControllers/AboutViewControllers.html#//apple_ref/doc/uid/TP40007457-CH112-SW10)。

### 使用内容视图控制器管理你的内容
要在你的应用程序呈现特别的内容，可以实现自己的内容视图控制器。通过 [UIViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/cl/UIViewController) 类或 [UITableViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UITableViewController_Class/index.html#//apple_ref/occ/cl/UITableViewController) 类的子类创建新的视图控制器类，实现所需要的呈现和控制内容的方法。

> **相关章节：**[Creating Custom Content View Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101-SW1)


### 容器视图控制器管理其他视图控制器
容器视图控制器显示其它视图控制器的内容。容器与这些视图控制器是明确的父子关系。容器和内容视图控制器的组合创建了视图控制器对象与单个根视图控制器的层次结构。

每一种类型的容器都定义了它自己的接口管理它的子级。容器的方法有时候会定义子级之间特别的导航关系。它也可以让它的子级视图控制器提供额外的内容用作配置容器。

iOS 提供许多类型的内置容器视图控制器你可以用来组织你的用户界面。

> **相关章节：**[View Controller Basics](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101-SW1)

### 在呈现的视图控制器中临时呈现视图

有时视图控制器想对用户显示额外的信息。也许它想用户提供额外的信息或执行一个任务。受限于 iOS 设备的屏幕空间；设备也许没有足够空间同时显示所有用户界面元素。作为解决，iOS 应用程序临时显示其它视图与用户交互。视图显示足够长的时间能让用户完成请求的操作。

为了简化界面实现所需要做的工作，iOS 允许视图控制器*呈现*其它视图控制器的内容。在呈现后，新的视图控制器的视图在屏幕的一部分显示－通常是整个屏幕。当用户完成任务后，已呈现的视图控制器告诉呈现它的视图控制器任务已经完成。然后使已呈现的视图控制器退出，恢复屏幕之前的状态。

视图控制器的设计必须包含呈现行为使它可以被其他视图控制器呈现。

**相关章节：**[Presenting View Controllers from Other View Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ModalViewControllers/ModalViewControllers.html#//apple_ref/doc/uid/TP40007457-CH111-SW1)

### Storyboards 连接用户界面元素到应用程序界面
用户界面的设计非常复杂。每个视图控制器都引用许多视图，手势检测，和其他用户界面对象。反过来，这些对象需要保持对视图的引用或执行特定的代码段响应用户的动作。视图控制器很少使用。多个视图控制器之间的合作在你的应用程序定义了其他关系。简单来说，创建用户界面意味着实例化和配置许多对象和建立它们之间的关系，这种做法耗时且容易出错。

作为替代，使用界面构造器创建 *storyboards*。storyboard 保持已配置的视图控制器实例和它们关联的对象。每个对象的属性可以在界面构造器配置，也可以配置它们之间的关系。

在运行时，应用程序加载 storyboards 和使用它们驱动你的应用程序界面。当对象从 storyboards 加载后，它们恢复为在 stroyboards 已配置的状态。UIKit 也提供了方法重写不能直接从界面构造配置的自定义行为。

通过使用 storyboards，你可以轻松的看到对象如何在应用程序的用户界面结合。你也可以写很少的代码就可以创建和配置应用程序的用户界面对象。

**相关章节：**[View Controller Basics](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/AboutViewControllers/AboutViewControllers.html#//apple_ref/doc/uid/TP40007457-CH112-SW10)，[Using View Controllers in Your App](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/UsingViewControllersinYourApplication/UsingViewControllersinYourApplication.html#//apple_ref/doc/uid/TP40007457-CH6-SW1)


## 如何使用该文档
开始阅读 [View Controller Basics](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/AboutViewControllers/AboutViewControllers.html#//apple_ref/doc/uid/TP40007457-CH112-SW10)，它解释视图控制器如何创建应用程序的界面。接着，阅读 [Using View Controllers in Your App](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/UsingViewControllersinYourApplication/UsingViewControllersinYourApplication.html#//apple_ref/doc/uid/TP40007457-CH6-SW1) 弄清楚如何使用视图控制器，包括 iOS 内置的和你自己创建的。

当你准备实现应用程序的自定义视图控制器时，阅读 [Creating Custom Content View Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101-SW1) 关于视图控制器需要执行的任务的概述，然后阅读这个文档剩余的章节学习如何实现这些行为。

## 前提条件
阅读这个文档之前，你应该熟悉 [Start Developing iOS Apps Today](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/index.html#//apple_ref/doc/uid/TP40011343) 和 *Your Second iOS App：Storyboards* 的内容。storyboard 教程演示了许多这个文档内描述的技术，包含下面的 Cocoa 概念：

- 定义新的 Objective-C 类
- 委托对象在管理应用程序行为中的作用
- Model－View－Controller 范例


## 其他参看

更多信息关于 UIKit 提供的标准容器视图控制器，见 [View Controller Catalog for iOS](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Introduction.html#//apple_ref/doc/uid/TP40011313)。

如何在视图控制器处理视图的指南，见 [View Programming Guide for iOS](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)。

如何处理视图控制器的事件的指南，见 [Event Handling Guide for iOS](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)。

更多信息关于 iOS 应用程序的总体结构，见 [App Programming GUide for iOS](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)。

如何在项目中配置 storyboards 的指南。见 [Xcode Overview](https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/index.html#//apple_ref/doc/uid/TP40010215)。

---


系列文章

*iOS 翻译 《View Controller Programming Guide for iOS：Introduction》*

[*iOS 翻译 《View Controller Programming Guide for iOS：View Controller Basics》*](../VCP1) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Content View Controllers》*](../VCP3)

[*iOS 翻译 《View Controller Programming Guide for iOS：Resource Management in View Controllers》*](../VCP4) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Responding to Display-Related Notifications》*](../VCP5) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controller's Views》*](../VCP6) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》*](../VCP7) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Supporting Multiple Interface Orientations》*](../VCP8) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controllers's Perspective》*](../VCP9) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》*](../VCP10) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Coordinating Efforts Between View Controllers》*](../VCP11) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Enabling Edit Mode in a View Controller》*](../VCP12) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Segues》*](../VCP13) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Container View Controllers》*](../VCP14)



