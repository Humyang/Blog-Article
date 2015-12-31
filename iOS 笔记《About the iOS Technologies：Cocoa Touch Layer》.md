layout: [post]
title: "iOS 笔记《About the iOS Technologies：Cocoa Touch Layer》"
date: 2015-04-25 08:30:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-About-the-iOS-Technologies-Cocoa-Touch-Layer"

---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址][1]



-------------------
Cocoa Touch 层包含了构建 iOS app 的关键的框架。这些框架定义了 app 的外观。它们也提供了基础的 app 架构和一些关键的技术例如多任务，基础触碰输入，推送通知，和许多高级别系统服务。当你在设计 app 时，你应该首先研究这一层的技术是否可以满足你的需求。

# **High-Level Features**

下面的章节描述了可以在 Cocoa Touch 层使用的关键的技术。

## App Extensions
iOS 8 让你通过提供一个 *App extension* 来拓展系统的选择区域，它是一段代码可以启动自定义功能到用户任务范围内。你可以提供一个 *App extension* 帮助用户投递内容到你的社交网站分享页面。用户安装并启用该 *App extesion* 后，当他们在 app 中点击共享按钮时可以选择它。你自定义的分享功能拓展提供接收，验证，和投递用户提供的内容等功能的代码。系统会在分享菜单中列出拓展，当用户选中它之后还会实例化他们。

> 例如 safai 的分享按钮和 pocket 的发送到 pocket 功能。

在 Xcode 中，可以通过添加 preconfigured app extension target 到 app 中创建拓展，用户安装 app 后会包含该拓展，用户可以在 app 设置中启用这个拓展。当用户运行了其他 app，系统会让这个拓展变为可用并会出现在系统 UI 中，例如分享菜单。

iOS 支持以下区域的 app extensions，也称为拓展点：

- *Share.*    分享内容到社交网站或机构。
- *Action.*  在当前内容执行一些简单的任务。
- *Widget.* 提供快速更新或今日视图通知中心启用简短的任务。 
- *Photo editing.*  提供在 Photos app 内编辑图像或视频。
- *Document provider.*  提供可以被其他 app 访问的文档存储位置。App 可以使用 document picker view controller 打开文件并通过 Document Provider 管理文件或把文件移动到 Document Provider。
- *Custom keyboard.* 用户可以在系统键盘位置选择自定义键盘应用在设备上所有 app 中。

每一个拓展点的使用都定义了相应的 API。当你准备使用拓展模版开始进行开发，你会获得被你选择的拓展点定义的包含方法存根和属性列表设置的默认 target。

更多相关的信息，见 [*App Extension Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/ExtensibilityPG/index.html#//apple_ref/doc/uid/TP40014214)


## Handoff
Handoff 是在 OS X 和 iOS 跨设备连续性的拓展的用户体验的功能。Handoff 使用户可以在一台设备中开始一个活动，然后切换到其他设备并在该设备恢复相同的活动。例如，某个用户从 Safari 移到登陆了相同的 Apple ID 账户的 iOS 设备浏览一篇很长的文章，相同的页面会在 iOS 的 Safari 打开，并且滚动条位置和启始设备相同，Handoff 使这个体验尽可能平稳顺畅。

App 想参与到 Handoff ，需要在 Foundation 中采用少量的 API。app 中每个正在进行的活动代表包含了需要在其他设备恢复活动的数据的用户活动对象。当用户选择恢复该活动，对象会发送到正在恢复的设备。每个用户活动对象都有一个在适当的时候被调用来刷新活动状态的委托对象，例如用户活动对象在两个设备之间发送之前。

如果持续的一个活动需要更多的数据它会很容易的被转换成用户活动对象，恢复中的 app 有打开一个 stream 到起始的 app 的选项。基于文档的 app 为用户基于 iColud 文档的工作自动的提供持续活动的支持。

更多相关的信息，见 [*Handoff Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/Handoff/HandoffFundamentals/HandoffFundamentals.html#//apple_ref/doc/uid/TP40014338)

## Document Picker
document picker view controller ([UIDocumentPickerViewController](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIDocumentPickerViewController_Class/index.html#//apple_ref/occ/cl/UIDocumentPickerViewController)) 授权用户访问你的应用程序的沙箱外的文件。这是两个 app 之间的简单分享文档机制。它也可以实现更加复杂的工作流程，因为用户可以在多个 app 之间编辑单个文档。

document picker 让你从 document providers 的数字访问的文件。例如，iCloud document provider 授权访问其他 app 存储在 iCloud 容器内的文档。
第三方开发者可以通过使用 Storage Provider extension 提供额外的 document provider。

更多关于如何使用 document picker 的信息，见 [*Document Picker Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/FileManagement/Conceptual/DocumentPickerProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40014451)。


## AirDrop
AirDrop 让用户分享图片，文档，URL，和其他类型的数据给邻近的设备。提供使用 AirDrop 发送文件到其他 iOS 设备的支持是内置现有的 [*UIActivityViewController*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIActivityViewController_Class/index.html#//apple_ref/occ/cl/UIActivityViewController)  类。该类为你指定的分享内容显示不同的选项。如果你没有在使用这个类，你应该考虑添加它到你的界面。

要接收使用 AirDrop 发送的文件，你的 app 必须做一下事情：

- 在 Xcode 声明支持适当的文件类型。(Xcode 添加适当的 keys 到你的 app 的 ```Info.plist``` 文件) 系统使用这些信息进行判断你的 app 是否可以打开给定的文件。
- 在你的 app delegate 声明 [application:openURL:sourceApplication:annotion:](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIActivityViewController_Class/index.html#//apple_ref/occ/cl/UIActivityViewController) 方法。(新的文件被接收后系统调用该方法)
 
发送给你的 app 的文件放置在 ```home``` 目录下的 ```Documents/Inbox```。如果你打算修改文件，你必须将文件移出该目录才可以执行此操作。(该目录内的文件系统只允许你的 app 读取和删除文件。) 保存在该目录下的文件使用了 data protection 加密，因此你必须为设备当前已被锁定文件无法访问做准备。

更多关于使用动态视图控制器共享数据，见 [*UIActivityViewController Class Reference*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIActivityViewController_Class/index.html#//apple_ref/doc/uid/TP40011976)。

##TextKit
TextKit 是一个功能齐全，高级别的文本处理和精美排版的类集合。使用 TextKit 你可以编排样式文本成段落，栏目，和页面；你可以使文本随意的环绕任何区域例如图像；你可以用它管理复合的字体。如果你正在考虑使用 Core Text 实现文本渲染，你应该考虑使用 TextKit 作为替代。TextKit 整合了所有 UIKit 基于文本的空间使 app 创建，编辑，显示和存储文本更轻松，在 iOS 相比以前可能更少的代码。

TextKit 包含新的 UIKit 类，并随着已存在的类拓展，包含了以下：

- [NSAttributedString](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Classes/NSAttributedString_Class/index.html#//apple_ref/occ/cl/NSAttributedString) 已经被拓展支持新的属性。
- [NSLayoutManager](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/NSLayoutManager_Class_TextKit/index.html#//apple_ref/occ/cl/NSLayoutManager) 生成字形和布局文本。
- [NSTextContainer](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/NSTextContainer_Class_TextKit/index.html#//apple_ref/occ/cl/NSTextContainer) 定义了文本被布局的区域
- [NSTextStorage](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/NSTextStorage_Class_TextKit/index.html#//apple_ref/occ/cl/NSTextStorage) 定义了管理基于文本内容的基本的接口。

更多关于 TextKit 的信息，见 [*Text Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009542)。



##UIKit Dynamics
app 现在可以为 UIView 对象和其他符合 [*UIDynamicItem*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIDynamicItem_Protocol/index.html#//apple_ref/occ/intf/UIDynamicItem) 协议的对象指定动态行为( 符合这个协议的对象被称为 *dynamic items*)。动态行为通过结合真实世界的行为和特点到你的 app 的用户界中提供了提升你的 app 用户体验的方式。UIKit dynamics 支持以下类型的行为。

- [UIAttachmentBehavior](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIAttachmentBehavior_Class/index.html#//apple_ref/occ/cl/UIAttachmentBehavior) 对象连接了两个动态项之间或动态项和一个点之间。当一个动态项 (或点) 移动了，绑定的项也会移动。连接不是完全静态。附加的行为有衰减和震动属性用来判断如何随着时间进行改变。
- [UICollisionBehavior](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UICollisionBehavior_Class/index.html#//apple_ref/occ/cl/UICollisionBehavior) 对象让动态项参与到彼此和被指定了边界的行为的碰撞。这行为也让这些项对碰撞做出恰当的响应。
- [UIGravityBehavior](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIGravityBehavior_Class/index.html#//apple_ref/occ/cl/UIGravityBehavior) 对象指定重力矢量给它的动态项。动态项在矢量的方向加速直到它们碰撞到了其他适当的已配置项或到达边界。
- [UIPushBehavior](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIPushBehavior_Class/index.html#//apple_ref/occ/cl/UIPushBehavior) 对象指定连续或瞬间的力矢量给它的动态项。
- [UISnapBehavior](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UISnapBehavior_Class/index.html#//apple_ref/occ/cl/UISnapBehavior) 对象指定了卡扣点给动态项。项以已配置的效果扣住一个点。例如，动态项可以扣住一个点就好像是被附加到弹簧一样。

当你增加他们到一个动画制作者对象时动态行为会变为活跃，它是 [*UIDynamicAnimator*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIDynamicAnimator_Class/index.html#//apple_ref/occ/cl/UIDynamicAnimator) 类的一个实例。动画制作者提供上下文给动态行为执行。给定的动态项可以有多个行为，但所有这些行为必须由同一个动画制作者对象动画化。

更多关于你可以应用的行为，见 [*UIKit Framework Reference *](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIKit_Framework/index.html#//apple_ref/doc/uid/TP40006955)

##Multitasking
电池续航时间是 iOS 设备的用户重要的考虑因素 iOS 的多任务模式被设计为最大化电池的续航时间同时给予 app 时间完成它们重要的工作。当用户按下 home 按钮，当前的 app 转移到后台执行上下文。如果该 app 没有更多的工作要做，那么它会暂停活动执行并投放入一个 “freeze-dried” 状态，它仍然遗留在内存但不执行任何代码。app 需要完成特殊类型的工作可以对系统要求在后台执行的时间。例如：

- app 可以请求一定量的时间完成重要的任务。
- app 需要支持特定的服务(例如音频播放)可以请求时间来提供这些服务。
- app 可以使用本地通知在特定的时间生成用户警报提示，无论 app 是否正在运行。
- app 可以定期的从网络下载内容。
- app 可以在一个对推送通知的响应的中下载内容。

更多如何支持 iOS 多任务模式的信息，见 [*App Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)

##Auto Layout
Auto layout 帮你用非常少的代码就可以构建动态界面。使用 Auto Layout 时，你要定义元素如何在你的界面上布局的规则。这些规则表示大量的阶级关系并且对比以前使用的 springs 和 struts 模式更加的直观。例如，你可以指定按钮在父视图的左边缘位置永远是 20 个点。

在实体使用的 Auto Layout 是一个 Objective-C 对象被称为约束 (*constraints*)。约束提供几个好处:

- 通过单独的字符串交换实现定位，而不需要你更新你的布局。
- 支持为右到左的语言把用户界面元素镜像，例如希伯来语和阿拉伯语。
- 更好的分离在视图层和控制器层之间的对象的职责。视图对象总是有标准尺寸的值，它在父视图内定位，并且对同级视图相对定位。如果有些不标准的需求视图控制器可以覆盖这些值。

更多关于如何使用 Auto Layout 的信息，见 [*Auto Layout Guide*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/AutolayoutPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010853)。

##Storyboards
Storyboards 是设计你的 app 的用户界面的推荐方式。Storyboards 把整个用户界面显示在一个地方使得你可以看到所有的你的视图和视图控制器和明白它们是如何一起工作的。Storyboards 重要的部分是能定义 segues，它是从一个视图控制器到另一个控制器的转换。这些转换让你捕获你的用户界面除了内容外的流程。你可以可以在 Xcode中或以编程的方式初始化他们来定义这些过渡效果。

你可以使用单个 storyboard 文件存储你的 app 的所有视图控制器和视图，或者你可以使用多个视图 storyboards 组织你的界面部分。在编译时间，Xcode 将 storyboards 文件的内容分为散块，使其能够单独的加载，获得更好的性能。你的 app 永远不需要直接操纵这些部分。UIKit 框架了提供方便的类从你的代码中访问 storyboards 的内容。

更多有关使用 storyboards 设计你的用户界面的内容，见 [*Xcode Overview*](https://developer.apple.com/library/prerelease/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/index.html#//apple_ref/doc/uid/TP40010215)。

更多关于如何从你的代码访问 storyboards，见 [*UIStoryboard Class Reference*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIStoryboard_Class/index.html#//apple_ref/doc/uid/TP40010909)。

##UI State Preservation
状态保存让你的 app 出现时像正在运行一样给用户完美的体验，即使当时 app 并没有运行。如果系统遇到内存方面的压力，它可能会默默的强制中断一个或多个后台 app。当一个 app 从前台转为后台，它可以保持它的视图和视图控制器的状态。在下一次运行周期，它可以使用已保持的视图和视图控制器使状态恢复使得 app 显示时就像从来没有退出过。

更多如何在你的 app 提供状态保存支持信息，见 [*App Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)。

##Apple Push Notification Service
Apple Push Notification Service 提供了提醒用户新信息的方法，即使你的 app 并没有正在运行活动。使用这个服务时，你可以推送文本通知，在你的 app 图标添加 badge，或者随时在用户设备上触发声音提醒。这些信息让用户知道应该打开你的 app 接收相关的信息。在 iOS 7，你甚至可以推送无声的通知让你的 app 知道有新的内容可以下载。

从设计的角度来说，有两个部分使推送通知为 iOS app 工作。首先，app 必须请求发出通知和一旦通知数据已经发出后的处理。第二，你需要提供一个服务器端进程在第一步生成通知。这个进程运行中你自己的服务器并为 Apple 推送通知服务器触发通知工作。

更多关于如何配置你的 app 使用远程通知的信息，见 [*Local and Remote Notificatino Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html#//apple_ref/doc/uid/TP40008194)。

##Local Notifications
Local notifications 通过给 app 生成本地通知而不是向外部服务器申请的方法补充了已有的推送通知机制。后台运行的 app 可以使用本地通知作为当重要事件发生时引起用户注意的方法。例如，在后台运行中的导航 app 可以使用本地通知提醒用户什么时候应该转弯。app 也可以为未来的日期和时间安排本地通知的发出，即使那时 app 并没有运行本地通知也会发出。

本地通知的优点是他们独立于你的 app 。提醒的通知是已安排好的，由系统管理他们的发出。你的 app 甚至不需要在当通知已交出后被运行。

更多关于使用本地通知的信息，见 [*Local and Remote Notification Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html#//apple_ref/doc/uid/TP40008194)。

##Gesture Recognizers
Gesture Recognizers 检测常见的手势类型，例如在你的 app 的视图中的刷(swipes)和捏(pinches)。因为它们使用相同的智能猜测作为检查手势系统,手势识别为你的 app 提供一致的行为。要使用一个手势，你可以附加该手势到你的视图中并在手势触发的时给它执行动作的方法。手势识别完成追踪原始触摸事件和判断他们是否构成有效手势的困难工作。

所有手势识别都是基于 [UIGestureRecognizer](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIGestureRecognizer_Class/index.html#//apple_ref/occ/cl/UIGestureRecognizer) 类，它定义了基础行为。UIKit 支持标准的手势识别子类检查 taps，pinches，pans，swipes，rotations。你也可以定制大多数手势识别的行为到你的 app 需要的地方。例如，你可以告诉 tap 手势识别检测调用你的动作方法之前检查指定的 tap 的数字。

更多关于可以使用的手势识别信息，见 [*Event Handling Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)。

##Standard System View Controllers
许多系统框架为标准系统界面定义了视图控制器。只要有可能，使用已提供的视图控制器而不是自己创建。我们鼓励你在 app 中使用这些视图控制器为用户呈现一致的用户体验。每当你需要执行以下的任务，你应该使用相应框架的视图控制器：

- **显示或编辑联系人信息**。使用 Address Book UI framework 的视图控制器。
- **创建或编辑日历事件**。使用 EventKit UI framework 的视图控制器。
- **编写邮件或 SMS 信息**。使用 Message UI framework 的视图控制器。
- **打开或预览文件的内容**。使用 UIKit 的 [UIDocumentInteractionComtroller](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIImagePickerController_Class/index.html#//apple_ref/occ/cl/UIImagePickerController) 类。
- **拍照或从用户相册选择照片**。使用 UIKit framework 的 [UIImagePickerController](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIImagePickerController_Class/index.html#//apple_ref/occ/cl/UIImagePickerController) 类。
- **拍摄视频短片**。 使用 UIKit framework 的 [UIImagePickerController](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIImagePickerController_Class/index.html#//apple_ref/occ/cl/UIImagePickerController)。

更多关于如何呈现和关闭视图控制器，见 [*View Controller Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)。

更多有关特定视图控制器的界面介绍，见 [*View Controller Catalog for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Introduction.html#//apple_ref/doc/uid/TP40011313)。

#**Cocoa Touch Frameworks**
下面的章节描述 Cocoa Touch 层中的框架和他们所提供的服务。

##Address Book UI Framework
Address Book UI framework (*AddressBookUI.framework*) 是一个 Objective-C 编程接口能让你用来为创建新的联系人和编辑选中的已有联系人显示标准系统界面。这个框架简化了你的 app 显示联系人信息的工作并确保了你的 app 与其他 app 使用相同的界面，从而确保了整个平台的一致性。

更多关于 Address Book UI framework 的类和如何使用它们，见 [*Add ress Book Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/ContactData/Conceptual/AddressBookProgrammingGuideforiPhone/Introduction.html#//apple_ref/doc/uid/TP40007744) 和 [*Address Book UI Framework Reference for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/AddressBookUI/Reference/AddressBookUI_Framework/index.html#//apple_ref/doc/uid/TP40007082) 。

##EventKit UI Framework
EventKit UI Framework (*EventKitUI.framework*) 提供为编辑和显示跟日历相关的事件呈现标准系统界面的视图控制器。这个框架建立在 EventKit framework 内的事件相关的数据之上，它在 [*Event Kit Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW2) 被描述。

更多有关这个框架的类和方法的信息，见 [*EventKit UI Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/EventKitUI/Reference/EventKitUIFrameworkRef/index.html#//apple_ref/doc/uid/TP40009663)。

##GameKit Framework
GameKit framework (*GameKit.framework*) 实现了对游戏中心的支持，它让用户共享他们的在线游戏相关信息。游戏中心提供以下功能的支持：

- Aliases，允许用户创建他们自己的游戏中心在线名称。用户登入游戏中心与其他用户互动时使用该别名。玩家可以设置状态信息以及标记其他人作为他们的好友。
- Leaderboards，允许你的 app 提交用户分数到游戏中心和在以后取回它们。你可以使用该功能展示你的 app 所有用户中最高分数。
- Matchmaking，让你通过连接已登录到游戏中心的用户创建多人游戏。加入多人游戏的玩家彼此不需要是本地的。
- Achievements，让你记录玩家在你的游戏中的进程。
- Challenges，允许玩家挑战朋友击败他们的成就或分数。(iOS 6 和之后)
- Turn-based gaming，创建持续性的比赛他们的状态被保存在 iCloud。

更多关于如何使用 GameKit framework，见 [*Game Center Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/GameKit_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008304) 和 [*GameKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/GameKit/Reference/GameKit_Collection/index.html#//apple_ref/doc/uid/TP40008303)。

##iAd Framework
iAd framework (*iAd.framework*) 让你从 app 中放出横幅型的广告。广告是被纳入标准视图的你可以整合到你的用户界面并在你想要的时间显示他们。这个视图他们自己与 Apple 的 iAd Service 工作自动化的处理所有关联的加载和显示丰富的多媒体广告工作和对这个广告的 tap 做出响应。

更多关于在你的 app 中使用 iAd 的信息，见 [*iAd Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/iAd_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009881) 和 [*iAd Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Reference/iAd_ReferenceCollection/index.html#//apple_ref/doc/uid/TP40009705)。

##MapKit Framework
MapKit framework (*MapKit.framework*) 提供了可滚动的地图你可以合并到你的 app 的用户界面。不仅仅是显示地图，你可以使用这个框架接口自定义地图的内容和外观。你可以使用注解 (annotations) 标记有趣的点，你还可以自定义覆盖层穿插在你自己的内容与地图内容。例如，你可能使用覆盖层画一个巴士站点，或者使用注解 (annotations) 突出显示临近的商店和餐馆。

除了显示地图，MapKit framework 还集成了 Maps app 和 Apple 的地图服务器到便捷路线 (directions)。对于 Maps app，用户可以委派提供的路线到任何支持路线的 app。App 提供指定路线类型 ，例如地铁路线，可以注册为当被询问时提供这些路线。App 也可以从 Apple 服务器请求步行和行驶路线并合并这些路线信息与他们的自定义的路线为用户提供完整的点对点体验。

更多关于使用 MapKit framework 的类的使用信息，见 [*Locations and Maps Programming*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009497) 和 [*MapKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MapKit/Reference/MapKit_Framework_Reference/index.html#//apple_ref/doc/uid/TP40008210)。

##Message UI Framework
Message UI framework (*MessageUI.framework*) 提供了从你的 app 中撰写 email 或 SMS 信息的支持。由出现在你的 app 的视图控制器界面支持撰写。你可以填写视图控制器的字段来设置收件人，主题，主要内容，和任意你想包含在信息中的附件。之后呈现的视图控制器，用户仍有在消息发送之前再次编辑的选项。

更多关于 Message UI framework 类的信息，见 [*Message UI Framework*](https://developer.apple.com/library/prerelease/ios/documentation/MessageUI/Reference/MessageUI_Framework_Reference/index.html#//apple_ref/doc/uid/TP40008274)。

更多关于使用这个框架的类的信息，见 [*System Messaging Programming Topic for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/SystemMessaging_TopicsForIOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010404)。

##Notification Center Framework
Notification Center framework (*NotificationCenter.framework*) 提供了在通知中心创建显示信息的部件的支持。

更多关于如何创建通知中心部件，见 [*App Extension Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/ExtensibilityPG/index.html#//apple_ref/doc/uid/TP40014214) 和 [*Notification Center Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/NotificationCenter/Reference/NotificationCenter_Framework/index.html#//apple_ref/doc/uid/TP40014443)。

##PushKit Framework
PushKit framework (*PushKit.framework*) 为网络电话 (VoIP) app 提供了注册的支持。这个框架替代了之前的注册网络电话的 app 的 API。替代保持持久连接打开，和因此造成的设备的电量消耗，App 可以使用这个框架在有来电的时候接收推送消息。

更多关于这个框架的接口信息，见此框架的头文件。

##Twitter Framework
Twitter framework (*Twitter.framework*) 已经被 Social framework 替代，它支持生成 twitter 的 UI 和支持创建一个 URLs 来访问 Twitter 的服务。

更多相关的信息， 见 [*Social Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW26) 。

##UIKit Framework
UIKit framework (*UIKit.framework*) 提供了生成图像的关键架构，在 iOS 中事件驱动 app，包含以下方面：

- 基础的 app 管理和架构，包括 app 的主运行循环
- 用户界面管理，包括 storyboards 和 nib 文件的支持
-  视图控制器模型封装你的用户界面的内容
- 表示标准系统视图和控件的对象
- 支持处理触摸和基于动画的事件
- 支持包含集成 iCloud 的文档模型，见 [*Document-Based App Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/DataManagement/Conceptual/DocumentBasedAppPGiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011149)。
- 图形和窗口支持，包括为拓展显示的支持；见 [*View Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)。
- 多任务的支持，见 [*Multitasking*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/iPhoneOSTechnologies/iPhoneOSTechnologies.html#//apple_ref/doc/uid/TP40007898-CH3-SW5)。
- 打印的支持，见 [*Drawing and Printing Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010156)。
- 支持自定义的标准 UIKit 控件的外观
- 支持文本和 web 内容
- 剪切，复制，和黏贴的支持
- 支持动画用户界面内容
- 通过 URL 架构和框架接口在系统中集成其他 app
- 残疾用户的可访问性支持
- 支持 Apple 推送通知服务，见 [*Apple Push Notification Service*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/iPhoneOSTechnologies/iPhoneOSTechnologies.html#//apple_ref/doc/uid/TP40007898-CH3-SW26)。
- 本地通知计划和交付，见 [*Local Notifications*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/iPhoneOSTechnologies/iPhoneOSTechnologies.html#//apple_ref/doc/uid/TP40007898-CH3-SW7)。
- 创建 PDF。
- 支持使用自定义的输入视图行为，如系统键盘。
- 支持创建自定义与系统键盘互动的文本视图。
- 支持通过 email，Twitter，Facebook或其他服务分享内容。

除了提供基本的代码构建你的 app 外，UIKit 也合并一些特定设备功能的支持，例如下面的：

- 内置照相机 (当存在时)。
- 用户的图片库。
- 设备名称和机型信息。
- 电池状态信息。
- 距离感应器信息。
- 已附加的耳机的远程控制信息。

更多有关 UIKit framework 类的信息，见 [*UIKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIKit_Framework/index.html#//apple_ref/doc/uid/TP40006955)。

#**系列文章**
*iOS 笔记《About the iOS Technologies：Cocoa Touch Layer》*
[*iOS 笔记《About the iOS Technologies：Media Layer》*](../iOS-Note-About-the-iOS-Technologies-Media-Layer) 
[*iOS 笔记《About the iOS Technologies：Core Service Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-Service-Layer)
[*iOS 笔记《About the iOS Technologies：Core OS Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-OS-Layer) 



---------

[1]: https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898-CH1-SW1
