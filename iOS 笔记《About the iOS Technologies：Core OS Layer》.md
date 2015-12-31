layout: [post]
title: "iOS 笔记《About the iOS Technologies：Core OS Layer》"
date: 2015-04-25 08:33:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-About-the-iOS-Technologies-Core-OS-Layer"
---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址][1]



-------------------
Core OS layer 包含大部分其他建立在其之上的技术的低级别功能。即使你没有在 app 中直接使用这些技术，它们也很有可能已经在其他的框架使用。当你有明确的安全需要或与外部硬件配件通信，你可以使用这层中的框架。

##Accelerate Framework
Accelerate framework (*Accelerate.framework*) 包含执行数字信号处理 (DSP)，线性代数，和图像处理计算的接口。使用这个框架比你自己写的这些接口版本有优势它们已为所有在 iOS 设备出现的硬件配置优化。因此，你可以只写一次你的代码就可以确保它可以在所有设备有效。

##Core Bluetooth Framework
Core Bluetooth framework (*CoreBluetooth.framework*) 允许开发者与蓝牙低功耗配件互动。这个框架的 Objective-C  接口允许你做以下事情：

- 扫描蓝牙配件并与你找到的配件连接或断开连接
- 提供你的 app 服务，为其他蓝牙设备打开 iOS 设备到周边
- 对其他 iOS 广播 iBeacon 信息
- 保持你的蓝牙连接状态和在你的 app 再次启动时恢复这些连接
- 外部可用的蓝牙设备变化时发出通知

更多关于使用 Core Bluetooth framework 的信息，见 [*Core Bluetooth Programming*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternetWeb/Conceptual/CoreBluetooth_concepts/AboutCoreBluetooth/Introduction.html#//apple_ref/doc/uid/TP40013257) 和 [*Core Bluetooth Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreBluetooth/Reference/CoreBluetooth_Framework/index.html#//apple_ref/doc/uid/TP40011295)。

##External Accessory Framework
External Accessory (*ExternalAccessory.framework*) 提供已与基于 iOS 的设备连接的硬件配件的通信。配件可以通过设备的 30-pin dock 连接器或无线蓝牙连接。External Accessory framework 提供了获取每个可用配件的信息和初始通信会话的方式。之后，你可以自由的操作配件直接使用任何它支持的命令。

更多关于如何使用这个框架的信息，见 [*External Accessory Programming Topics*](https://developer.apple.com/library/prerelease/ios/featuredarticles/ExternalAccessoryPT/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009502)。

更多关于为基于 iOS 的设备开发配件，请到 [*Apple Developer website*](http://developer.apple.com/)。


##Generic Security Services Framework
Generic Security Services framework (*GSS.framework*) 为 iOS app 提供标准的安全相关的服务集合。这个框架的基础接口在 IETF [*RFC 2743*](http://www.ietf.org/rfc/rfc2743.txt) 和 [*RFC 4401*](http://tools.ietf.org/html/rfc4401) 规定。除了提供标准化接口，iOS 包含一些额外的管理凭据，它不是标准中规定的但在许多 app 中需要用到。

##Local Authentication Framework
Local Authentication Framework (*LocalAuthentication.framework*) 让你使用 Touch ID 来认证用户。一些 app 可能需要安全的访问它们所有的内容，其他的可能需要确保某些信息或选项的安全。在这两种情况下，你可以在处理之前需要用户认证。使用这个框架对用户弹出提醒并由应用程序指定需要认证的理由。当你的 app 获得回应，它可以基于用户是否成功认证进行应答。

更多关于这个框架的接口，见 [*Local Authentication Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/LocalAuthentication/Reference/LocalAuthentication_Framework/index.html#//apple_ref/doc/uid/TP40014520)。

##Network Extension Framwork
Network Extension framework (*NetworkExtension.framework*) 提供配置和控制虚拟私有网络 (VPN) 隧道的支持。可以使用这个框架创建 VPN 配置。然后你可以手动开启 VPN 隧道或者响应特定的事件按照规则开启 VPN 隧道。

更多关于这个框架的接口，见它的头文件。

##Security Framework
除了内置的安全功能，iOS 也提供了一个精密的安全框架 (*Security.framework*) 确保你的 app 管理的数据的安全。这个框架提供管理证书，公钥和私钥，和信任策略的接口。它支持新一代的加密安全伪随机数。它也支持在钥匙扣保存证书和加密密钥，这是为敏感用户信息服务的安全仓库。

Common Crypto library 提供了额外的对称加密，基于散列的消息验证码 (HMACs),和摘要的支持。摘要功能提供实质兼容那些在 OpenSSL library 中但不可以在 iOS 上使用的功能。

它可以在你创建的多个 app 之间分享钥匙扣项。共享项使它轻松的为同一套 app 顺利的互相操作。例如，你可以使用这个功能共享用户密码或其他可能在不同 app 中需要提示用户单独输入的元素。在它们之间共享数据，你必须配置每个 Xcode 项目适当的资格。

关于 Security framework 管理的函数和功能的信息，见 [*Security Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Security/Reference/SecurityFrameworkReference/index.html#//apple_ref/doc/uid/TP40004330)。

关于如何访问钥匙扣的信息，见 [*Keychain Services Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Security/Conceptual/keychainServConcepts/01introduction/introduction.html#//apple_ref/doc/uid/TP30000897)。

关于在 Xcode 项目中设置资格的信息，见 [*App Distribution Guide*](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582) 中的 [Adding Capabilities](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26)。

关于你可以配置的资格，见 [*Keychain Services Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Security/Reference/keychainservices/index.html#//apple_ref/doc/uid/TP30000898) 中的 [SecItemAdd](https://developer.apple.com/library/prerelease/ios/documentation/Security/Reference/keychainservices/index.html#//apple_ref/c/func/SecItemAdd) 函数所描述。

##System
system level 包含内核环境，驱动，和操作系统的低级别 UNIX 接口。内核是基于 Mach 的，负责操作系统的各个方面。它管理虚拟内存系统，线程，文件系统，网络，和进程间通讯。这层的驱动提供可用的硬件和系统框架之间的接口。为安全起见，系统框架集合和 app 限制了访问内核和驱动。

iOS 提供访问非常多操作系统的低级别功能的接口集合。你的 app 可以通过 LibSystem library 访问这些功能。接口是基于 C 语言的并且对以下提供支持：

- 并发 (POSIX 线程 和统一调度中心)
- 网络 (BSD sockets)
- 文件系统访问
- 标准化 I/O
- Bonjour 和 DNS 服务
- 本地信息
- 内存分配
- 数学运行

许多 Core OS 技术的头文件位置在 <*iOS_SDK*>/usr/include/ 目录，<*iOS_SDK*>是安装 Xcode 时设置的目标 SDK 路径目录。

更多关于这些技术相关联的函数，见 [*iOS Manual Pages*](https://developer.apple.com/library/prerelease/ios/documentation/System/Conceptual/ManPages_iPhoneOS/index.html#//apple_ref/doc/uid/TP40007259)。

##64-Bit Support
iOS 最初是设计为支持使用 32 位架构的设备的二进制文件。但在 iOS 7，引入对 64 架构的编译，链接，和二进制文件调试的支持。所有的库和框架已经为 64 位准备，意味着它们可以在 32 位和 64 位 app 中使用。当为 64 位运行库编译时，app 可能运行更快因为在 64 位模式有额外的处理器资源可以使用。

#**系列文章**
[*iOS 笔记《About the iOS Technologies：Cocoa Touch Layer》*](../iOS-Note-About-the-iOS-Technologies-Cocoa-Touch-Layer)
[*iOS 笔记《About the iOS Technologies：Media Layer》*](../iOS-Note-About-the-iOS-Technologies-Media-Layer)
[*iOS 笔记《About the iOS Technologies：Core Service Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-Service-Layer)
*iOS 笔记《About the iOS Technologies：Core OS Layer》*



---------

[1]: https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898-CH1-SW1