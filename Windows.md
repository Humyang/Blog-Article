layout: [post]
title: "iOS 翻译 《View Programming Guide for iOS：Windows》"
date: 2015-05-04 16:04:30
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-View-Programming-Guide-for-iOS-Windows"

---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503-CH1-SW2)


---
#窗口
每个应用程序都需要至少一个窗口－UIWindow 类的实例－有的可能包含不止一个窗口。窗口对象有几个职责：

- 包含应用程序的可见内容。
- 在触摸事件交出到你的视图和其他应用程序对象中扮演重要角色。
- 它与应用程序的视图控制器共同工作简化方向的更改。

在 iOS 中，窗口没有任何的标题栏，关闭栏，或其他任何可见部件。窗口总是一个或更多视图背后的白色的容器。同样，应用程序不会通过显示新的窗口来更改它的内容。当你想更改已显示的内容，你需要更改窗口最前面的视图。

大多数应用程序在它们的生命周期只创建和使用一个窗口。窗口跨越设备的整个主屏幕并且在应用程序生命周期中最早被加载比应用程序的主要 nib 文件(或编程方式创建) 还早。如果应用程序使用拓展显示器支持视频输出，它可以在拓展显示器创建额外的窗口中显示内容。其它的窗口通常由系统创建，并且通常为响应特定的事件创建，例如在电话呼叫来临时。

##涉及窗口的任务
许多应用程序只有在窗口启动时会与窗口交互。然而，你可以使用应用程序的窗口对象执行少数与应用程序相关的任务：

-  **使用窗口对象将点和矩形转换为窗口的本地坐标系统或从窗口的本地坐标系统转换点和矩形**。例如，如果你已提供了窗口坐标内的值，你可能想在尝试使用它之前将它转换为指定视图的坐标系统。关于如何使用转换坐标的信息，见 [Converting Coordinates in the View Hierarchy](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW40)。
-  **使用窗口的通知来追踪窗口相关的变化**。当窗口显示或隐藏时或当窗口接收或抛弃关键状态时，窗口会生成通知。你可以使用这些通知在应用程序的其他部分执行动作。更多信息，见 [Monitoring Window Changes](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingWindows/CreatingWindows.html#//apple_ref/doc/uid/TP40009503-CH4-SW13)。

##创建和配置窗口
你可以使用编程方式或使用界面构造器创建和配置应用程序窗口。在这两个情况中，窗口会在启动时创建并且停留，并且在应用程序的委托对象中保存着引用。如果应用程序创建了额外的窗口，应用程序会延迟到当它们需要时才创建。例如，如果应用程序支持在拓展显示器设备中显示内容，它会在创建相应的窗口之前一直等待直到显示设备被连接。

应用程序的主窗口应该总是在启动时创建无论应用程序将会在前台或后台运行。通过它自己创建和配置窗口不是一个昂贵的操作。如果应用程序启动后直接进入后台运行，那么你应该避免窗口可见直到应用程序进入前台之前。

###在界面构造器创建窗口
使用界面构造器可以非常简单的创建应用程序主窗口因为 Xcode 的项目模版为你完成了这些工作。每一个新的 Xcode 应用程序项目都包含一个主 nib 文件(名称通常是 MainWindow.xib 或它的变种) 包含了应用程序主窗口。除此之外，这些模版也在应用程序的委托对象中为窗口定义了一个 outlet。你可以使用 outlet 在你的代码中访问窗口对象。

>**重要提示：** 当你在界面构造器创建了窗口后，推荐在属性面板的运行选项中启用全屏幕。如果这个选项未启用并且你的窗口小于目标设备的屏幕，那么你的部分视图将不会接收到触摸事件。这是因为窗口 (跟所有视图一样) 不会接收边界矩形外部的触摸事件。因为视图默认不会剪切超过边界的部分，所以视图依旧可见但事件不会到达。在运行选项启用了全屏幕确保窗口的尺寸适合当前的屏幕。

如果你使用界面构造器改造项目，使用界面构造器创建窗口是非常简单的事情，只需要拖动一个窗口对象到你的 nib 文件中。当然，你也应该完成以下的工作：

- 要在运行时访问窗口，你应该将窗口连接到一个 outlet 中，通常被定义在应用程序委托或 nib 文件的文件所有者中。 
- 如果你的改造计划包括将新的 nib 文件改成应用程序的主 nib 文件，你必须将应用程序的 Info.plist 中的 NSMainNibFile 键设置为新的 nib 文件名称。更改这个键的值确保 nib 文件被加载并且可以在应用程序委托被调用时使用 [application:didFinishLaunchingWithOptions:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/index.html#//apple_ref/occ/intfm/UIApplicationDelegate/application:didFinishLaunchingWithOptions:) 方法。

更多关于创建和配置 nib 文件的信息，见 *Interface Builder User Guide*。关于如何在运行时加载 nib 文件到应用程序中，见 [Resource Programming](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/LoadingResources/Introduction/Introduction.html#//apple_ref/doc/uid/10000051i) 内的 [Nib File](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html#//apple_ref/doc/uid/10000051i-CH4)。

###使用编程方式创建窗口
如果你准备使用编程方式创建的应用程序主窗口，你应该在应用程序的委托方法 [application:didFinishLaunchingWithOptions:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/index.html#//apple_ref/occ/intfm/UIApplicationDelegate/application:didFinishLaunchingWithOptions:) 中包含类似以下的代码到：

```objc

self.window = [[[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]] autorelease];

```

上面的例子中，假设 self.window 是一个应用程序委托的已声明属性并已配置和保留的窗口对象。如果你创建了一个窗口当作拓展显示器，那么你应该为它分配不同的变量并且你需要指定非主 [UIScreen](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/cl/UIScreen) 对象的边界表示拓展显示器的边界。

在创建窗口时，你应该始终设置窗口的尺寸填充满屏幕的边界。不应该缩减窗口的尺寸去适应状态栏或其他项。状态栏总是浮在窗口上面，因此你需要做的只是收缩窗口的视图使其适应状态栏。如果你使用了视图控制器，视图控制器会自动处理你的视图尺寸。
 
###添加内容到窗口
 每一个窗口通常有一个单独根视图对象 (被相应的视图控制器管理) 它包含其他所有视图呈现你的内容。使用单独的根视图简化变更界面的处理；需要显示新内容，你只需要替换根视图。要在安装新视图到窗口，使用 [addSubview:](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instm/UIView/addSubview:) 方法。例如，安装一个通过视图控制器管理的视图，你可以使用类似下面的代码：
 
```objc
[window addSubview:viewController.view];
```

在上面的代码中，你也可以选择配置 nib 文件中窗口的 [rootViewController](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/instp/UIWindow/rootViewController) 属性。这个属性通过使用 nib 文件替代编程方式，提供便利的方式配置窗口的根视图。如果这个属性在窗口从 nib 文件加载后是已设置的，那么 UIKit 自动从已关联的视图控制器安装视图作为窗口的根视图。这个属性只用作安装根视图，不被用作窗口与视图控制器通信。

你可以使用任何你想使用的视图作为窗口的根视图。根据你界面设计，根视图可以是通用的 [UIView](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/cl/UIView) 对象作为一个或更多子视图的容器，根视图也可以是标准系统视图，或是你定义的自定义视图。一些标准系统视图通常都被用作根视图，包括滚动视图，表视图，和图像视图。

在配置窗口的根视图时，你负责设置它在窗口内的初始尺寸和位置。对于不包含状态栏的应用程序，或显示半透明的状态栏，需要设置视图的尺寸为适应窗口的尺寸。对显示不透明状态栏的应用程序，将视图定位在状态栏之下并且相应的缩减它的尺寸。用你的视图的高度减去状态栏的高度防止你的视图的顶部被遮盖。

> **说明：**如果你的窗口的根视图是通过容器视图控制器 (例如 标签栏控制器，导航控制器，或分割视图控制器) 提供，你不需要自己设置视图的初始值。容器视图控制器基于状态栏是否显示自动设置视图为适当尺寸。

 
###更改窗口级别
每一个 UIWindow 对象都有一个可配置的 [windowLevel](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/instp/UIWindow/windowLevel) 属性它决定窗口相对其他窗口的定位。大多数情况下，你不需要更改应用程序窗口的级别。新窗口在创建时会自动分配一个正常窗口级别。正常窗口级别指示窗口显示应用程序相关的内容。高级别窗口用于在应用程序内容上方浮动的信息，例如系统状态栏或提醒信息。尽管你可以自己为窗口分配级别，但使用特定的界面时系统通常会替你完成这些工作。例如，当你显示或隐藏状态栏或显示一个提醒视图时，系统会自动为显示这些项创建所需要的窗口。

##监视窗口变更
如果你想追踪应用程序内出现和消失的窗口，你可以使用下面这些窗口相关的通知：

- [UIWindowDidBecomeVisibleNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/c/data/UIWindowDidBecomeVisibleNotification)
- [UIWindowDidBecomeHiddenNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/c/data/UIWindowDidBecomeHiddenNotification)
- [UIWindowDidBecomeKeyNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/c/data/UIWindowDidBecomeKeyNotification)
- [UIWindowDidResignKeyNotification](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/c/data/UIWindowDidResignKeyNotification)

这些通知会在响应应用程序的窗口更改时发出。因此，当应用程序显示或隐藏窗口时，UIWindowDidBecomeVisibleNotification 和 UIWindowDidBecomeHiddenNotification 通知会因此发出。这些通知不会在应用程序移至后台执行状态时发出。即使应用程序在后台运行时窗口没有在屏幕上显示，也会一直认为在应用程序上下文内可见。

UIWindowDidBecomeKeyNotification 和 UIWindowDidResignKeyNotification 通知帮助应用程序保持对关键窗口 (*key window*) 的追踪－就是说，这个窗口是当前接收键盘事件和其他非触摸事件的窗口。而触摸事件是发给产生触摸的窗口，发给应用程序关键窗口的事件没有关联的坐标值。同时只有一个窗口能成为关键窗口。

##在拓展显示器中显示内容
要在拓展显示器上显示内容，你必须为应用程序创建一个额外的窗口并分配一个屏幕对象代表拓展显示器。新窗口通常默认的与主屏幕关联。更改窗口关联的屏幕对象会导致窗口的内容重新路由到相应的显示器。一旦窗口与相应的屏幕关联，你可以像操作主屏幕的一样为它添加视图和显示。

[UIScreen](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/cl/UIScreen) 类维护代表可用硬件显示器的屏幕对象的列表。通常只有一个表示 iOS 设备主显示器的屏幕对象，但如果设备支持拓展显示器那么可能有额外可用的屏幕对象。支持拓展显示器的设备包括拥有 Retina 显示屏的 iPhone 和 iPod touch 和 iPad。较旧的设备，例如 iPhone 3GS，不支持拓展显示器。

> 因为拓展显示器实际上是视频输出连接，你不需要等待被关联的拓展显示器的窗口中的视图和控件的触摸事件。此外，应用程序负责更新窗口需要的内容。若要镜像主窗口的内容，应用程序需要为拓展显示器的窗口创建视图集合的副本并与主窗口的视图串联更新。

拓展显示器上的显示内容的处理在下面的章节描述。下面是基本处理的步骤总结：

1. 在应用程序启动时，为屏幕的连接和断开通知注册。
2. 当需要在拓展显示器中显示内容时，创建和配置窗口。
    - 使用 UIScreen 的 [screens](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/clm/UIScreen/screens) 属性为拓展显示器获取屏幕对象。
    - 创建 [UIWindow](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/cl/UIWindow) 对象并为屏幕 (或内容) 设置适当的尺寸。
    - 分配拓展显示器的 UIScreen 对象到窗口的 [screen](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/instp/UIWindow/screen) 属性。
    - 为你的内容按需要调整屏幕对象的分辨率。
    - 添加适当的视图到窗口中。
3. 正常的显示窗口和更新。  

###处理屏幕连接和断开连接的通知
屏幕的连接和断开通知是优雅的处理拓展显示器变更的关键。当用户连接或断开显示器时，系统会发生相应的通知到应用程序中。你应该利用这些通知更新应用程序状态和创建或释放与窗口关联的拓展显示器。

重点记住关于连接和断开连接通知可以在任意时候来临，即使你的应用程序在后台被挂起。因此，最好在一个应用程序运行时一直存在的对象中检测通知，例如应用程序委托。如果应用程序被挂起，通知会排队等待直到应用程序退出挂起状态并且开始在前台或后台中运行。

清单 2-1 中的代码为连接和断开通知注册。这个方法在应用程序委托初始化时调用但你也可以在应用程序的其他地方注册这些通知。这些方法的实现处理在[清单 2-2](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingWindows/CreatingWindows.html#//apple_ref/doc/uid/TP40009503-CH4-SW15)
 
**清单 2-1** 为屏幕连接通知和断开连接通知注册

```objc
- (void)setupScreenConnectionNotificationHandlers
{
    NSNotificationCenter* center = [NSNotificationCenter defaultCenter];
 
    [center addObserver:self selector:@selector(handleScreenConnectNotification:)
            name:UIScreenDidConnectNotification object:nil];
    [center addObserver:self selector:@selector(handleScreenDisconnectNotification:)
            name:UIScreenDidDisconnectNotification object:nil];
}
```
如果拓展显示器被附加到设备时应用程序是活动的，那么它应该为显示器创建第二个窗并填充一些内容。这些内容不需要是你最终想呈现的内容。例如，如果应用程序未准备使用拓展屏幕，你可以在第二个窗口显示一些占位内容。如果你不为屏幕创建第二个窗口，或如果你创建了窗口但不显示它，拓展显示器会显示黑幕。

清单 2-2 说明如何创建第二个窗口并为它填充一些内容。在这个例子中，应用程序创建窗口的处理方法是用来接收屏幕连接通知。(需要为连接和断开通知注册，见[清单 2-1](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingWindows/CreatingWindows.html#//apple_ref/doc/uid/TP40009503-CH4-SW14)。)这个处理方法为连接通知创建第二个窗口，将它分配给新的已连接屏幕并调用应用程序主视图控制器的方法添加一些内容到窗口中并显示它。收到断开连接通知时释放窗口并通知主视图控制器使它能调整相应的图像。

<br />
** 清单 2-2** 处理连接和断开连接通知

```objc
- (void)handleScreenConnectNotification:(NSNotification*)aNotification
{
    UIScreen*    newScreen = [aNotification object];
    CGRect        screenBounds = newScreen.bounds;
 
    if (!_secondWindow)
    {
        _secondWindow = [[UIWindow alloc] initWithFrame:screenBounds];
        _secondWindow.screen = newScreen;
 
        // Set the initial UI for the window.
        [viewController displaySelectionInSecondaryWindow:_secondWindow];
    }
}
 
- (void)handleScreenDisconnectNotification:(NSNotification*)aNotification
{
    if (_secondWindow)
    {
        // Hide and then delete the window.
        _secondWindow.hidden = YES;
        [_secondWindow release];
        _secondWindow = nil;
 
        // Update the main screen based on what is showing here.
        [viewController displaySelectionOnMainScreen];
    }
 
}
```
###为拓展显示器配置窗口
要在拓展显示器上显示窗口，你必须为它关联相应的屏幕对象。这些处理涉及定位正确的 [UIScreen](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/cl/UIScreen) 对象并分配它到窗口的 [screen](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/instp/UIWindow/screen) 属性。你可以从 UIScreen 的类方法 [screens](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/clm/UIScreen/screens) 中获取屏幕对象的列表。这个方法返回的数组至少包含一个代表主屏幕的对象。如果出现第二个对象，那么这个对象代表已连接的拓展显示器。

清单 2-3 的方法在应用程序启动时被调用，用于查看拓展显示器是否已经关联。如果是，这个方法会创建窗口，为它关联拓展显示器，并在显示窗口前添加一些占位内容。在这个例子中，占位内容是白色的背景和一个说明没有内容显示的标题。要显示窗口，这个方法变更 [hidden](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/hidden) 属性的值而不是调用 makeKeyAndVisible。这样做是因为窗口只包含静态内容并且没有被用来处理事件。

<br />
** 清单 2-3** 为拓展显示器配置窗口

```objc
- (void)checkForExistingScreenAndInitializeIfPresent
{
    if ([[UIScreen screens] count] > 1)
    {
        // Associate the window with the second screen.
        // The main screen is always at index 0.
        UIScreen*    secondScreen = [[UIScreen screens] objectAtIndex:1];
        CGRect        screenBounds = secondScreen.bounds;
 
        _secondWindow = [[UIWindow alloc] initWithFrame:screenBounds];
        _secondWindow.screen = secondScreen;
 
        // Add a white background to the window
        UIView*            whiteField = [[UIView alloc] initWithFrame:screenBounds];
        whiteField.backgroundColor = [UIColor whiteColor];
 
        [_secondWindow addSubview:whiteField];
        [whiteField release];
 
        // Center a label in the view.
        NSString*    noContentString = [NSString stringWithFormat:@"<no content>"];
        CGSize        stringSize = [noContentString sizeWithFont:[UIFont systemFontOfSize:18]];
 
        CGRect        labelSize = CGRectMake((screenBounds.size.width - stringSize.width) / 2.0,
                                    (screenBounds.size.height - stringSize.height) / 2.0,
                                    stringSize.width, stringSize.height);
 
        UILabel*    noContentLabel = [[UILabel alloc] initWithFrame:labelSize];
        noContentLabel.text = noContentString;
        noContentLabel.font = [UIFont systemFontOfSize:18];
        [whiteField addSubview:noContentLabel];
 
        // Go ahead and show the window.
        _secondWindow.hidden = NO;
    }
}
```

> **重要提示：** 你应该总是在显示窗口之前使屏幕和窗口关联。虽然可以为当前显示的窗口更换屏幕，但这样是昂贵的操作应该尽量避免。

只要拓展屏幕的窗口被显示后，应用程序可以像其他窗口一样开始更新它。你可以按需要添加和移除子窗口，更改子窗口的内容，动画方式改变视图，和按需要使它们的内容无效。

###配置拓展显示器的屏幕模式
根据你的内容不同，你可能想在它关联窗口之前变更屏幕模式。许多屏幕支持多种分辨率，其中一些使用不同的像素长宽比。屏幕对象默认使用通用的屏幕模式，但你可以更改成更适合你的内容的模式。例如，如果你使用 OpenGL ES 实现游戏制作并且你的贴图是设计为 640*480 屏幕像素点，你可以更改屏幕模式使分辨率比默认的更高。

如果你计划使用非默认的屏幕模式，你应该在屏幕和窗口关联之前在 UIScree 对象应用这个模式。[UIScreenMode](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreenMode_class/index.html#//apple_ref/occ/cl/UIScreenMode) 类定义了单屏幕模式的属性。你可以从它的 [availableModes](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/instm/UIScreen/availableModes) 属性获取屏幕支持的模式的列表并且遍历列表获取适配你的需求的一个。

更多关于屏幕模式的信息，见 [*UIScreenMode Class Reference*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIScreenMode_class/index.html#//apple_ref/doc/uid/TP40009312)。


---
系列文章
[*iOS 翻译 《View Programming Guide for iOS：Introduction》*](../iOS-Note-View-Programming-Guide-for-iOS-Introduction) 

[*iOS 翻译 《View Programming Guide for iOS：View and Window Architecture》*](../iOS-Note-View-Programming-Guide-for-iOS-View-and-Window-Architecture)

*iOS 翻译 《View Programming Guide for iOS：Windows》*

[*iOS 翻译 《View Programming Guide for iOS：Views》* ](../iOS-Note-View-Programming-Guide-for-iOS-Views) 

[*iOS 翻译 《View Programming Guide for iOS：Animations》*](../iOS-Note-View-Programming-Guide-for-iOS-Animations) 

