layout: [post]
title: "iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controller’s Perspective》"
date: 2015-06-19 11:46:20
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "VCP9"

---

iOS 视图控制器编程指南：从视图控制器的角度看无障碍访问


<!-- more -->

[原文地址](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457-CH1-SW1)

记录关于学习过的 iOS 文档

---

# 从视图控制器的角度看无障碍访问

除了管理视图的行为，视图控制器也协助控制应用程序的无障碍访问。无障碍访问应用程序对每个人都可以使用，无论使用者是残疾人士或者身体功能障碍，它都可以作为有用的工具同时保持应用程序的功能和可用性。

要实现无障碍访问，iOS 应用程序必须对 VoiceOver 用户提供与它的用户界面元素有关的信息。VoiceOver,是一个被设计来协助阅读障碍人士的屏幕阅读技术，它可以大声念出在屏幕上显示的文本，图像，和 UI 控件，即使不能看到也可以与这些元素交互。UIKit 对象默认提供无障碍访问，但仍然需要你从视图控制器的角度做一些事情以解决无障碍访问。也就是说，你需要确保以下的实现：

* 每个可以与用户交互的用户界面元素都需要实现无障碍访问。包含仅提供信息的元素例如静态文本，以及执行动作的控件。
* 所有无障碍访问元素都提供准确和有用的信息。

除了这些基本方面，还可以通过编程方式设置 VoiceOver 的对焦环，响应特殊的 VoiceOver 手势，和观察无障碍访问通知，提高 VoiceOver 的用户体验。


## 移动 VoiceOver Cursor 到指定元素

当屏幕的布局变更时，VoiceOver 对焦环，也称为 *VoiceOver cursor*,会重置它的位置到在屏幕上从左到右，从上到下第一个显示的元素。当视图被呈现在屏幕上时你可以更改 VoiceOver cursor 所在的第一个元素。

例如，当导航控制器推送一个视图控制器到导航堆栈时，VoiceOver cursor 会落在导航栏的返回按钮上。根据你的应用程序的不同，移动到导航栏的标题可能更有意义，或者其它元素。 

要想这样做，调用 [UIAccessibilityPostNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIKitFunctionReference/index.html#//apple_ref/c/func/UIAccessibilityPostNotification) 并共同使用通知 [UIAccessibilityScreenChangedNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/index.html#//apple_ref/c/data/UIAccessibilityScreenChangedNotification) (它告示 VoiceOver 屏幕的内容已发生变更) 和你想对焦的元素，如在清单 9-1 所示。

**清单 9-1** 投递一个无障碍访问通知更改第一个念出的元素

```objc

@implementation MyViewController
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
 
    UIAccessibilityPostNotification(UIAccessibilityScreenChangedNotification,
                                    self.myFirstElement);
}
@end


```

如果只是布局的更改而不是屏幕的内容更改，例如从竖屏切换到横屏，使用通知 [UIAccessibilityLayoutChangeNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/index.html#//apple_ref/c/data/UIAccessibilityLayoutChangedNotification) 替代 `UIAccessibilityScreenChangeNotification`。

> **说明：**设备方向旋转会触发布局更改，这会重置 VoiceOver cursor 的位置。

## 响应特定的 VoiceOver 手势

这里有几个 VoiceOver 用户可以执行触发自定义动作的特殊手势。这些手势是特殊的因为你可以定义它们的行为，不像标准化的 VoiceOver 手势。你可以通过在视图控制器重写某些方法检测手势。

手势会首先为指令检测拥有 VoiceOver cursor 的视图并沿着响应链向上遍历直到找到相应的 VoiceOver 手势方法的实现。如果没找到实现，手势会触发系统默认手势动作。例如，Magic Tap 手势如果没有从应用程序委托找到当前视图的 Magic Tap 实现，那么 Magic Tap 会从音乐应用的播放列表中播放和暂停音乐。

尽管你可以提供任意你想要的自定义逻辑，但 VoiceOver 用户期望这些特殊动作能够遵循某些准则，像其它手势一样，你的 VoiceOver 手势的实现应该遵循下面的模式使用户可以直观的与无障碍访问应用程序交互。

这里有五个特殊 VoiceOver 手势：

* **Escape。**两个手指以 Z 字形扫动，退出模态窗口，或返回导航层次结构上一级。
* **Magic Tap。**两个手指双击执行最有意义的动作。
* **Three-Finger Scroll。**三根手指轻扫使垂直或水平的内容滚动。
* **Increment and Decrement。**一个手指往上或往下轻扫在可调整的元素中增加或减去给定的值。无障碍访问应用程序中可调整的元素必须实现这些方法。

> **说明：**所有特殊 VoiceOver 手势方法会返回用来决定是否传播到响应链的一个布尔值。要禁止传播，返回 YES；否则，返回 NO。

### Escape

如果你呈现了覆盖内容的视图－例如模态窗口或弹出提示，你应该重写 [accessibilityPerformEscape](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/occ/instm/NSObject/accessibilityPerformEscape) 方法使覆盖视图退出。Escape 手势的功能与电脑键盘上 `ESC` 键的功能类似；它可以取消临时对话框或标签使主内容显示。

重写 Escape 手势的另一个使用情况是返回导航层次结构的上一级。`UINavigationController` 默认实现了这个方法。如果你正在设计自己的导航控制器，你应该设置 Escape 手势使它可以在你的导航堆栈中移动一级，因为这个是 VoiceOver 用户期望的功能。

### Magic Tap

Magic Tap 的目的是快速执行一些常用的或最有意义的动作。例如，在图像应用程序，它可以接听或挂断电话。在时钟应用程序，它可以启动和停止秒表。如果你想通过手势触发一个动作而不管 VoiceOver cursor 是否位于视图上，你应该在你的视图控制器实现 [accessibilityPerformMagicTap](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/occ/instm/NSObject/accessibilityPerformMagicTap) 方法。

说明：如果你不喜欢 Magic Tap 手势执行与应用程序内其它位置相同的动作，最适当的方式是在应用程序委托实现 `accessibilityPerformMagicTap` 方法。

### Three-Finger Scroll

当 VoiceOver 用户执行三根手指滚动时会触发 [accessibilityScroll:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/occ/instm/NSObject/accessibilityScroll:) 方法。它会接收 [UIAccessibilityScrollDirection](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/c/tdef/UIAccessibilityScrollDirection) 参数，你可以用来判断滚动的方向。如果你有自定义滚动视图，可能更适合在视图自身实现这个方法。

### Increment and Decrement

可调整数值的元素需要 [accessibilityIncreament](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/occ/instm/NSObject/accessibilityIncrement) 和 [accessibilityDecrement](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityAction_Protocol/index.html#//apple_ref/occ/instm/NSObject/accessibilityDecrement) 方法并应该在视图自身中实现。

## 观测无障碍访问通知

你可以监听无障碍访问通知触发回调函数。某些情况下，UIKit 会发出无障碍访问通知，你的应用程序可以观测这些通知拓展应用程序的无障碍访问功能。

例如，如果你监听了 [UIAccessibilityAnnouncementDidFinishNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/index.html#//apple_ref/c/data/UIAccessibilityAnnouncementDidFinishNotification) 通知，你可以触发一个方法在 VoiceOver 的语音结束时执行。Apple 在 iBooks 应用程序实现了这个功能。当 VoiceOver 完成电子书的其中一行的阅读时 iBooks 会发出通知触发下一行的阅读。如果是本页的最后一行，回调中的逻辑会告诉 iBooks 让它翻页并继续阅读一旦到达文章最后一行就结束阅读。这种一行接一行的跟随执行使 VoiceOver 在导航文本的同时为用户提供了无缝，不间断的阅读体验。

要注册成无障碍访问通知观测者，可以使用默认的通知中心。然后创建一个与 `selector` 参数中所提供的方法的同名方法，如清单 9-2 所示。

**清单 9-2**注册成为无障碍访问通知观测者。

```objc

@implementation MyViewController
- (void)viewDidLoad
{
    [super viewDidLoad];
 
    [[NSNotificationCenter defaultCenter]
        addObserver:self
           selector:@selector(didFinishAnnouncement:)
               name:UIAccessibilityAnnouncementDidFinishNotification
             object:nil];
}
 
- (void)didFinishAnnouncement:(NSNotification *)dict
{
    NSString *valueSpoken = [[dict userInfo] objectForKey:UIAccessibilityAnnouncementKeyStringValue];
    NSString *wasSuccessful = [[dict userInfo] objectForKey:UIAccessibilityAnnouncementKeyWasSuccessful];
    // ...
}
@end


```

`UIAccessibilityAnnouncementDidFinishNotification` 预计会有一个 [NSNotification](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/index.html#//apple_ref/occ/cl/NSNotification) 字典作为参数你可以判断语音的值并判断是否已经连续的说完。语音可能会中断，例如 VoiceOver 使用者执行停止语音手势或者在语音结束之前扫到另一个元素。

另一个有用的通知是 [UIAccessibilityVoiceOverStatusChanged](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/index.html#//apple_ref/c/data/UIAccessibilityVoiceOverStatusChanged)。它可以检测 VoiceOver 的打开或关闭切换。如果 VoiceOver 在应用程序的外部切换开关，当你的应用程序重新回到前台时会接收到这个通知。因为 `UIAccessibilityVoiceOverStatusChanged` 不期望接收任何参数，所以在 selector 中的方法不需要附加冒号 (`:`)。

需要可以观测的通知的完整列表，可以阅读 [*UIAccessibility Protocol Reference*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/index.html#//apple_ref/doc/uid/TP40008786) 中的 "Notifications"。记住你可能只会观测到可以通过 UIKit 发布的通知，它是 `NSString` 对象，而没有通过你的应用程序发布的通知，它们是 `int` 类型的通知。


---

[*iOS 翻译 《View Controller Programming Guide for iOS：Introduction》*](../VCP0) 

[*iOS 翻译 《View Controller Programming Guide for iOS：View Controller Basics》*](../VCP1) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in Your App》*](../VCP2) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Content View Controllers》*](../VCP3)

[*iOS 翻译 《View Controller Programming Guide for iOS：Resource Management in View Controllers》*](../VCP4) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Responding to Display-Related Notifications》*](../VCP5) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Resizing the View Controller's Views》*](../VCP6) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Using View Controllers in the Responder Chain》*](../VCP7) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Supporting Multiple Interface Orientations》*](../VCP8) 

*iOS 翻译 《View Controller Programming Guide for iOS：Accessibility from the View Controllers's Perspective》*

[*iOS 翻译 《View Controller Programming Guide for iOS：Presenting View Controllers from Other View Controllers》*](../VCP10) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Coordinating Efforts Between View Controllers》*](../VCP11) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Enabling Edit Mode in a View Controller》*](../VCP12) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Segues》*](../VCP13) 

[*iOS 翻译 《View Controller Programming Guide for iOS：Creating Custom Container View Controllers》*](../VCP14)

