layout: [post]
title: "iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》"
date: 2015-07-02 18:12:56
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "VCP10"
---

iOS 视图控制器编程指南：通过其它视图控制器呈现视图控制器


<!-- more -->

[原文地址](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457-CH1-SW1)

记录关于学习过的 iOS 文档

---

# 通过其它视图控制器呈现视图控制器

这种呈现视图控制器的能力可以让你中断当前的工作流程并显示新的视图集合。大部分情况下，应用程序呈现视图控制器临时中断工作流程是为了向用户获取重要数据。但你也可以使应用程序在特定的时间显示备用界面通过使用被呈现的视图控制器。

## 视图控制器如何呈现其它视图控制器

被呈现的视图控制器不是特定的 [UIViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/cl/UIViewController) 子类 (如 `UITabBarController` 或 `UINavigationController` 之类)。任意视图控制器都可以通过你的应用程序呈现，例如标签栏和导航控制器，当你想传达旧视图层次结构和新视图层次结构之间的关系的特定含义时你可以呈现视图控制器。

当你呈现模态视图控制器时，系统会在呈现中的视图控制器和将要被呈现的视图控制器之间创建关系。进一步解释，呈现中的视图控制器会更新它的 [presentedViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/presentedViewController) 属性指向被呈现的视图控制器。同样，被呈现的视图控制器会更新它的 [presentingViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/presentingViewController) 属性往回指向呈现它的视图控制器。图 10-1 展示在日历应用程序中管理主屏幕的视图控制器和被用作创建新事件的被呈现视图控制器之间的关系。

**图 10-1** 日历应用程序中被呈现的视图。

![](./connections_made_when_a_controller_is_presented_2x.png)

任何视图控制器对象都可以在同一时间内呈现一个单独的视图控制器，即使视图控制器它们自己就是通过其它视图控制器呈现的。换句话说，你可以以队列的方式呈现的视图控制器，根据需要在其它视图控制器的顶部呈现新的视图控制器。图 10-2 是队列的过程和触发的动作的可视化展示。在这个例子中，当用户点击相机视图中的图标时，应用程序会呈现带有用户照片的视图控制器。点击图像库的工具栏中的动作按钮会提示用户选择相应的动作然后对该动作呈现另一个视图控制器 (这里是人员选取器)。选择联系人后 (或点击取消后) 会退出该界面并回到图像库中。点击完成按钮会退出图像库并回到相机界面。

**图 10-2** 创建模态视图控制器的队列
![](./modal_chains.jpg)

在呈现视图控制器的队列中的每个视图控制器都有指它在向队列中周围的其它对象。换句话说，呈现其它视图控制器的被呈现视图控制器的 [presentingViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/presentingViewController) 和 [presentedViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/presentedViewController) 属性都拥有有效对象。你可以根据需要使用这些关系追踪队列中的视图控制器。例如，如果用户取消当前的操作，你可以通过解散第一个被呈现的视图控制器来移除队列中的所有对象。解散视图控制器时所解散的不仅仅是视图控制器，也会解散所有由它呈现的视图控制器。

在图 10-2 中，值得提到的一点是被呈现的视图控制器都是导航控制器。你可以使用与呈现的内容视图控制器相同的方式呈现 [UINavigationController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UINavigationController_Class/index.html#//apple_ref/occ/cl/UINavigationController) 对象。

当呈现导航控制器时，你需要呈现的总是 `UINavigationController` 对象本身，而不是呈现位于导航堆栈的视图控制器。但是，个别位于导航堆栈的视图控制器可能会呈现其它视图控制器，包括导航控制器。图 10-3 展示在前面涉及的例子中更详细的对象。如你所见，人员选择器不是被图像库的导航控制器呈现而是通过导航堆栈 (图像库的导航堆栈) 中的一个内容视图控制器呈现。

**图 10-3** 模态呈现导航视图控制器

![](./modal_chains_objects_2x.png)

## 模态视图的呈现风格

对于 iPad 应用程序，你可以使用几种不同的风格呈现内容。在 iPhone 应用程序中，被呈现的视图总是会覆盖窗口的可见部分，但当它运行在 iPad 上时，视图控制器会使用它的 [modalPresentationStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/modalPresentationStyle) 属性中的值决定它们被呈现时的外观。这个属性的不同选项让你呈现的视图控制器可以完全填充屏幕或只填充一部分屏幕。

图 10-4 展示了可用的核心呈现风格。([UIModalPresentationCurrentContext](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/c/econst/UIModalPresentationCurrentContext) 风格使视图控制器遵循它的父辈的风格。)在每个呈现风格中，变暗的区域显示的是底下的内容但不允许点击内容。因此，不像 popover，你所呈现的视图必须拥有一个控件使用户可以退出该视图。

**图 10-4** iPad 的呈现风格

![](./modal_styles_2x.png)

更多使用不同的呈现风格的指导，见 [Modal View](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/ContentViews.html#//apple_ref/doc/uid/TP40006556-CH13-SW18)。

## 呈现视图控制器并选择过渡风格

当使用故事板的 segue 呈现视图控制器时，它会自动实例化并呈现。呈现中的视图控制器可以在目标视图控制器被呈现之前对它进行配置。更多信息，见 [Configuring the Destination Controller When a Segue is Triggered](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ManagingDataFlowBetweenViewControllers/ManagingDataFlowBetweenViewControllers.html#//apple_ref/doc/uid/TP40007457-CH8-SW4)。

如果你需要以编程方式呈现视图控制器，你必需做以下的事情：

1.创建你想要呈现的视图控制器。
2.设置视图控制器的 [modalTransitionStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/modalTransitionStyle) 属性为期望值。
3.对视图控制器分配委托对象。通常，委托是呈现中的视图控制器。这个委托由被呈现的视图控制器使用当它准备消失时通知呈现中的视图控制器。它也可以传达其它信息返回给委托。
4.调用当前视图控制器的 [presentViewController:animated:completion:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/presentViewController:animated:completion:) 方法，将你想要呈现的视图控制器传递进去。

`presentViewController:animated:completion:` 方法为指定的视图控制器对象呈现视图并在当前的视图控制器和新的视图控制器之间配置"呈现中－被呈现 (presenting-presented)" 关系。除了恢复之前的状态，我们一般都想动画新视图控制器的外观。你应该使用的过渡风格取决于你计划如何使用被呈现的视图控制器。表 10-1 列出你可以分配到被呈现的视图控制器的 [modalTransitionStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/modalTransitionStyle) 属性的过渡风格并且描述了如何使用每一个。

过渡风格  | 用途
------------- | -------------
[UIModalTransitionStyleCoverVertical](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/c/econst/UIModalTransitionStyleCoverVertical)  | 当你想中断当前的工作流程向用户收集信息时使用这个风格。你也可以使用它呈现用户可以或不可以修改的内容。对于这个过渡风格，内容视图控制器应该提供明显的按钮使用户可以退出这个视图控制器。通常这些按钮是取消按钮或完成按钮。如果你没有明确的设置过渡风格，那么这个是默认风格。
[UIModalTransitionStyleFlipHorizontal](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/c/econst/UIModalTransitionStyleFlipHorizontal)  | 使用这个风格临时更改应用程序的工作模式。这个风格的大部分用途是显示可能频繁更改的设置，例如股票和天气应用程序。这些设置可以对整个应用程序有意义或只对当前屏幕有特定意义。对于这个过渡风格，通常会提供一些有序的按钮使用户回到应用程序的正常运行模式。
[UIModalTransitionStyleCrossDissolve](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/c/econst/UIModalTransitionStyleCrossDissolve) | 当设备方向更改时使用这个风格呈现备用的界面。在这种情况下，你的应用程序在响应方向更改通知时复制呈现和解散备用界面。多媒体应用程序也可以使用这个风格淡入屏幕显示多媒体内容。如何实现响应界面方向更改时使用备用界面的例子，见 [Creating an Alternate Landscape Interface](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/RespondingtoDeviceOrientationChanges/RespondingtoDeviceOrientationChanges.html#//apple_ref/doc/uid/TP40007457-CH7-SW14)。

清单 10-1 展示如何以编程方式呈现视图控制器。当用户添加新食谱时，应用程序通过呈现一个导航视图控制器提示用户输入关于食谱的基本信息。被呈现的是导航视图控制器所以会在标准的位置摆放取消和完成按钮。使用导航控制器也使未来需要拓展新食谱界面时变得轻松。所有你需要做的只是把新的视图控制器推送到导航堆栈中。

清单 10-1 编程方式呈现视图控制器。

```objc

- (void)add:(id)sender {
   // Create the root view controller for the navigation controller
   // The new view controller configures a Cancel and Done button for the
   // navigation bar.
   RecipeAddViewController *addController = [[RecipeAddViewController alloc]
                       init];
 
   // Configure the RecipeAddViewController. In this case, it reports any
   // changes to a custom delegate object.
   addController.delegate = self;
 
   // Create the navigation controller and present it.
   UINavigationController *navigationController = [[UINavigationController alloc]
                             initWithRootViewController:addController];
   [self presentViewController:navigationController animated:YES completion: nil];
}

```

当用户在新食谱输入界面点击完成或取消其中一个按钮时，应用程序会退出视图控制器并回到主窗口。见 [Dismissing a Presented View Controller](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ModalViewControllers/ModalViewControllers.html#//apple_ref/doc/uid/TP40007457-CH111-SW14)。

## 呈现上下文提供被呈现的视图控制器覆盖的区域

由呈现上下文定义用作呈现区域的屏幕区域。默认情况下，呈现上下文由根视图控制器提供，它的 frame 会被用作定义呈现上下文的 frame。但是，呈现中的视图控制器或者在视图层次结构中的其它父辈，都可以选者由它们提供呈现上下文。在这种情况下，当呈现上下文是由其它视图控制器提供时，它们的 frame 会被用作决定被呈现的视图的 frame。这种灵活的方式可以让限制模态呈现成屏幕的一小部分，让其它内容可以显示。

当视图控制器呈现后，iOS 会搜索它的呈现上下文。首先由读取呈现中的视图控制器的 [definePresentationContext](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/definesPresentationContext) 属性开始。如果这个属性的值是 YES，那么由呈现中的视图控制器定义呈现上下文。否则，它会继续往视图控制器的层次结构上方搜索直到有视图控制器返回 YES 或者到达窗口的根视图控制器。

当视图控制器定义呈现上下文时，它也可以选择定义呈现风格。通常，被呈现的视图控制器使用它的 [modalTransitionStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/modalTransitionStyle) 属性决定如何呈现。设置了 [definesPresentationContext](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/definesPresentationContext) 为 YES 的视图控制器也可以设置它的 [providesPresentationContextTransitionStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/providesPresentationContextTransitionStyle) 为 YES。如果 [providesPresentationContextTransitionStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/providesPresentationContextTransitionStyle) 设置成了 YES，iOS 会使用呈现上下文的 [modalPresentationStyle](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instp/UIViewController/modalPresentationStyle) 决定如何呈现新的视图控制器。


## 解散被呈现的视图控制器

当需要解散被呈现的视图控制器时，最好的方式是让呈现中的视图控制器解散它。换句话说，最要有可能，都应该由同一个视图控制器负责解散它。尽管有几种方法可以通知呈现中的视图控制器解散被呈现的视图控制器，但是最好的技术是使用委托。更多信息，见 [Using Delegation to Communicate with Other Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/ManagingDataFlowBetweenViewControllers/ManagingDataFlowBetweenViewControllers.html#//apple_ref/doc/uid/TP40007457-CH8-SW9)。

## 呈现标准系统视图控制器

有几个标准的系统视图控制器设计供你的应用程序呈现。呈现这些视图控制器的基础规则与呈现你的自定义内容视图控制器规则相同。但是，因为你的应用程序不可以访问系统视图控制器管理的视图层次结构，你不能简单的实现视图中控件的动作。要与系统视图控制器交互通常通过委托对象进行。

每个系统视图控制器都定义了相应的协议，在你的委托对象中实现这些方法。每个委托通常都实现方法接收项被选中或取消的操作。你的委托对象应该始终准备处理这两种情况。最重要的一件事是委托必须要实现通过调用正在呈现的视图控制器的 [dismissModalViewControllerAnimated:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/instm/UIViewController/dismissModalViewControllerAnimated:) 方法 (换句话说，被呈现的视图控制器的父辈) 解散被呈现的视图控制器。

表 10-2 列出几个 iOS 中的标准系统视图控制器，更多关于这些类的信息，包括它们提供的功能，见相应的类引用文档。

**表 10-2** 标准系统视图控制器

框架  | 视图控制器
------------- | -------------
Address Book UI | [ABNewPersonViewController](https://developer.apple.com/library/ios/documentation/AddressBookUI/Reference/ABNewPersonViewController_Class/index.html#//apple_ref/occ/cl/ABNewPersonViewController)<br />[ABPeoplePickerNavigationController](https://developer.apple.com/library/ios/documentation/AddressBookUI/Reference/ABPeoplePickerNavigationController_Class/index.html#//apple_ref/occ/cl/ABPeoplePickerNavigationController)<br />[ABPersonViewController](https://developer.apple.com/library/ios/documentation/AddressBookUI/Reference/ABPersonViewController_Class/index.html#//apple_ref/occ/cl/ABPersonViewController)<br />[ABUnknownPersonViewController](https://developer.apple.com/library/ios/documentation/AddressBookUI/Reference/ABUnknownPersonViewController_Class/index.html#//apple_ref/occ/cl/ABUnknownPersonViewController)
Event Kit UI | [EKEventEditViewController](https://developer.apple.com/library/ios/documentation/EventKitUI/Reference/EKEventEditViewControllerClassRef/index.html#//apple_ref/occ/cl/EKEventEditViewController)<br />[EKEventViewController](https://developer.apple.com/library/ios/documentation/EventKitUI/Reference/EKEventViewControllerClassRef/index.html#//apple_ref/occ/cl/EKEventViewController)<br />
Game Kit | [GKAchievementViewController](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GKAchievementViewController_Ref/index.html#//apple_ref/occ/cl/GKAchievementViewController)<br />[GKLeaderboardViewController](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GKLeaderboardViewController_Ref/index.html#//apple_ref/occ/cl/GKLeaderboardViewController)<br />[GKMatchmakerViewController](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GKMatchmakerViewController_Ref/index.html#//apple_ref/occ/cl/GKMatchmakerViewController)<br />[GKPeerPickerController](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GKPeerPickerController_Class/index.html#//apple_ref/occ/cl/GKPeerPickerController)<br />[GKTurnBasedMatchmakerViewController](https://developer.apple.com/library/ios/documentation/GameKit/Reference/GKTurnBasedMatchmakerViewController_Ref/index.html#//apple_ref/occ/cl/GKTurnBasedMatchmakerViewController)<br />
Message UI | [MFMailComposeViewController](https://developer.apple.com/library/ios/documentation/MessageUI/Reference/MFMailComposeViewController_class/index.html#//apple_ref/occ/cl/MFMailComposeViewController)<br />[MFMessageComposeViewController](https://developer.apple.com/library/ios/documentation/MessageUI/Reference/MFMessageComposeViewController_class/index.html#//apple_ref/occ/cl/MFMessageComposeViewController)
Media Player | [MPMediaPickerController](https://developer.apple.com/library/ios/documentation/MediaPlayer/Reference/MPMediaPickerController_ClassReference/index.html#//apple_ref/occ/cl/MPMediaPickerController)<br />[MPMoviePlayerViewController](https://developer.apple.com/library/ios/documentation/MediaPlayer/Reference/MPMoviePlayerViewController_class/index.html#//apple_ref/occ/cl/MPMoviePlayerViewController)
UIKit | [UIImagePickerController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIImagePickerController_Class/index.html#//apple_ref/occ/cl/UIImagePickerController)<br />[UIVideoEditorController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIVideoEditorController_ClassReference/index.html#//apple_ref/occ/cl/UIVideoEditorController)


**说明：** 尽管 [MPMoviePlayerController](https://developer.apple.com/library/ios/documentation/MediaPlayer/Reference/MPMoviePlayerController_Class/index.html#//apple_ref/occ/cl/MPMoviePlayerController) 类是在 Media Player 框架中可以在技术上被认为是模态视图控制器，但在语法的使用上略有不同。对于呈现中视图控制器，你需要初始化它并告诉它将要播放的多媒体文件。然后由视图控制器处理其它方面的呈现和解散它的视图。(但是，[MPMoviePlayerViewController](https://developer.apple.com/library/ios/documentation/MediaPlayer/Reference/MPMoviePlayerViewController_class/index.html#//apple_ref/occ/cl/MPMoviePlayerViewController) 类用作 `MPMoviePlayerController` 的替代作为播放影片的标准视图控制器。)

---

系列文章

[*iOS 翻译 《View Controller Programming Guide for iOS：Introduction》*](../VCP0)

[*iOS 翻译 《View Controller Programming Guide for iOS：View Controller Basics》*](../VCP1)

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 


[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Content View Controllers》*](../VCP3) 
[*iOS 翻译 《View Controller Programming Guide for iOS：Resource Management in View Controllers》*](../VCP4) 



[*iOS 翻译 《View Controller Programming Guide for iOS：Responding to Display-Related Notifications》*](../VCP5) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controller's Views》*](../VCP6) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》*](../VCP7) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Supporting Multiple Interface Orientations》*](../VCP8) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controllers's Perspective》*](../VCP9) 

iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》* 

[*iOS 翻译 《View Controller Programming Guide for iOS：Coordinating Efforts Between View Controllers》*](../VCP11) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Enabling Edit Mode in a View Controller》*](../VCP12) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Segues》*](../VCP13) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Container View Controllers》*](../VCP14)

