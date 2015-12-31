layout: [post]
title: "iOS 笔记《About the iOS Technologies：Core Service Layer》"
date: 2015-04-25 08:32:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-About-the-iOS-Technologies-Core-Service-Layer"
---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址][1]




-------------------
Core Services layer 包含了 apps 用到的基础系统服务。最关键的服务是 Core Foundation 和 Foundation 框架，它定义了所有 apps 都用到的基础类型。这层中也包含了单体技术 (individual technologies) 对一些功能的支持，例如位置，iCloud，社交媒体和网络。

#**High-Level Features**
下面的章节描述了一些可以在 Core Services layer 使用的 high-level 的功能。

##Peer-to-Peer Services
Multipeer Connectivity framework 提供了点对点蓝牙连接。你可以使用点对点蓝牙连接方式与邻近的设备开展通信会话。尽管点对点连接主要用于游戏中，但你也可以在其他类型的 apps 上使用这个功能。

更多关于如何在你的 app 使用 peer-to-peer 连接功能，见 [*Multipeer Connectivity framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MultipeerConnectivity/Reference/MultipeerConnectivityFramework/index.html#//apple_ref/doc/uid/TP40013328)。

##iCloud Storage
iCloud storage 让你的 app 把用户的文档和数据写入中心位置。用户以后就可以在他们所有的电脑和 iOS 设备中访问这些数据。用户的文档使用了 iCloud 意味着用户可以从任何设备浏览和修改这些文档而不再需要通过同步或传输文件。使用 iCloud 账户保存用户的文档为用户提供一层安全的保护。即使用户丢失了设备，设备上使用 iCloud 保存的文档也不会丢失。

下面是几种  iCloud 存储方式的优势，每个都有不同的预期用途：

- iCloud document storage。使用用户的 iCloud 账户保存文档和数据。
- iCloud key-value data storage。使用这个功能共享你的 app 的少量实例数据。
- CloudKit storage。当你想创建公有共享内容或管理自己的数据传输，使用这个功能。

大多数的 app 都使用 iCloud document storage 在用户的 iCloud 账户共享文档。(用户认为的 iCloud storage 功能。) 用户关心文档是否跨设备共享，在给定的设备上显示和管理这些文档。与之相反， iCloud key-value 保存一些用户看不到的数据。它为你的 app 与它自身的一些实例共享一些非常小量的数据 (几十kb) 。Apps 应该使用这个功能存储非关键的 app 数据例如喜好设置，而不是关键的 app 数据。

更多关于如何在你的 app 提供 iCloud 支持，见 [*iCloud Design Guide*](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/iCloudDesignGuide/Chapters/Introduction.html#//apple_ref/doc/uid/TP40012094)。

##Block Object
[Block objects]() 是 C-level 的语言结构，可以纳入到你的的 C 和 Objective-C 代码中。一个 block object 实际上是一个匿名函数和传入到函数后的数据，在其他语言中有时被称为 *closure* 或 *lambda*。Block 作为回调函数或你需要在一个地方简单的把将要被执行的代码和相关的数据结合时特别有用。

在 iOS，blocks 通常在下面的情景使用：

- 作为 delegate 和 delegates 方法替代
- 作为回调函数的替代
- 作为单次运算 (one-time operations) 的完成时处理
- 方便的在集合的所有的项执行任务
- 与调度队列一起执行异步任务。


更多 block object 的介绍和使用它们，见 [*A Short Practical Guide to Blocks*](https://developer.apple.com/library/prerelease/ios/featuredarticles/Short_Practical_Guide_Blocks/index.html#//apple_ref/doc/uid/TP40009758)。

更多关于 blocks 的信息，见 [*Blocks Programming Topics*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/Blocks/Articles/00_Introduction.html#//apple_ref/doc/uid/TP40007502)。



##Data Protection
Data Protection 让 app 为用户的敏感数据工作，发挥某些内置了加密装置的设备的优势。当你的 app 指定了特定的被保护文件，系统会以加密的方式保存该文件。当设备被锁定，这个文件的内容无法被你的 app 和任何潜在的入侵者访问。当设备被用户解锁，解密的密钥会被创建允许你的 app 访问文件。其他数据保护级别也可以供你使用。

想实现数据保护需要你考虑如何创建和管理你想保护的数据。Apps 在创建时间必须设计成安全数据和在为设备锁定解锁将要发生访问变化时做好准备。

更多关于如何在你的 app 为文件添加数据保护，见 [*App Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072)。

##File-Sharing Support
File-Sharing support 让 app 可以在 iTunes 9.1 及以后的版本使用用户数据。声明了支持文件共享的 app 可以把  */Document*  目录供用户使用。用户可以使用 iTunes 在这个目录移出和移入文件。该功能不允许你共享内容给同一个设备中的其他 app；使用这个功能需要黏贴板或文档交互控制器对象。

在你的 app 中启用共享需要做以下的事情：

1. 增加 UIFileSharingEnabled 键到你的 app 的 Info.plist 文件，然后设置值为 YES。
2. 放置你想分享的文件到你的 app 的 Documents 目录。
3. 当设备插入到用户的计算机，iTunes 在选中设备的 Apps 标签显示文件共享部分。
4. 用户可以增加文件到目录中或移动文件到桌面。

支持文件共享的 Apps 应该对 */Documents*  新增加的文件作出响应和识别。例如，你的 app 可以让新的文件在界面上显示并可用。永远不要向用户呈现目录文件的列表和询问用户设备应该如何处理这些文件。

更多额外的 UIFileSharingEnable 键的信息，见 [*Information Property List Key Reference*](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247)。

##Grand Central Dispatch
Grand Central Dispatch (GCD) 是 BSD-level 的技术，可以用来管理你的 app 的任务的执行。GCD 结合了异步编程模型和高度优化的核心，提供便利的 (和更高效的) 线程替代品。GCD 也为许多类型的 low-level 任务提供便利的替代品，例如读取和写入文件的描述符，实现定时器，和监控信号和处理事件。

更多关于如何在你的 app 中使用 GCD，见 [*Concurrency Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091)。

更多关于特定的 GCD 功能，见  [*Grand Central Dispatch (GCD) Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Performance/Reference/GCD_libdispatch_Ref/index.html#//apple_ref/doc/uid/TP40008079)。

##In-App Purchase
In-App Purchase 让你的 app 内部销售额外内容和服务和 iTunes 内容。这个框架使用了 StoreKit 框架实现，它提供了处理用户 iTunes 账户上金融交易所需要的基础设施。你负责处理 app 的整体用户体验和提供购买服务内容的介绍。对于可下载的内容，你可以自己托管相关内容或者使用 Apple 的服务器为你托管。

更多关于在 app 中的 in-app purchase 支持，见 [*In-App Purchase Programming GUide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/StoreKitGuide/Introduction.html#//apple_ref/doc/uid/TP40008267)。

更多关于使用 SotreKit framework 的额外信息，见 [*Store Kit Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW4)。

##SQLite
SQLite library 让你嵌入轻量级的数据库到你的 app 中而不需要运行独立的远程数据库服务器进程。在你的 app 中，你可以创建本地数据库文件并管理这些文件的表和记录。这个库为一般用途使用，但也为快速访问数据库记录提供了优化。

访问 SQLite 库的头文件位置在 <*iOS_SDK*>/usr/include/sqlite3.h，<*iOS_SDK*> 是你的 Xcode 安装路径的目标 SDK 位置。

更多关于使用 SQLite 的信息，见 [*SQLite Software Library*](http://www.sqlite.org/)。

##XML Support
Foundation framework 为检索 XML 文档的元素提供了 [NSXMLParset](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Classes/NSXMLParser_Class/index.html#//apple_ref/occ/cl/NSXMLParser) 类。操作 XML 内容的是 libxml2 库。这个是开源库，让你可以快速解析或写入任意 XML 数据和转换 XML 内容为 HTML。

 libxml2 库的头文件存在于 <*iOS_SDK*>/usr/include/libxml2/ 目录，<*iOS_SDK*> 是你的 Xcode 安装路径的目标 SDK 位置。

更多关于使用 libxml2 的信息，见 [*documentation for libxml2*](http://xmlsoft.org/index.html)。

#**Core Services Framework**
下面部分米描述了 Core Services layer 的框架和它们所提供的服务。

##Accounts Framework
Accounts framework (*Accounts.framework*) 为用户的某些账户提供了单点登陆模式。单点登陆使用户无需为多个账户多次输入而提升了用户体验。
它也为你的 app 管理账户授权过程而简化了开发模式。这个框架可以与 Social framework 结合使用。

更多关于 Accounts framework 的类的信息，见  [*Accounts Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Accounts/Reference/AccountsFrameworkRef/index.html#//apple_ref/doc/uid/TP40011024)。

##Address Book Framework
Address Book framework (*AddressBook.framework*) 提供了以编程的方式访问用户的联系人数据库。如果你的 app 用到了联系人信息，你可以使用这个框架访问和操作这些信息。例如，一个聊天程序可以使用这个框架取得可用的联系人列表，然后初始化聊天会话和在 view 中显示这些联系人。

> 重要提醒：访问用户的联系人数据必须有用户明确的授权。Apps 因此必须为用户拒绝这些权限所做准备。Apps 也应在 *Info.plist* 键中描述需要这个权限的原因。

更多关于 Address Book framework 的功能的信息，见 [*Address Book Framework Reference for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/AddressBook/Reference/AddressBook_iPhoneOS_Framework/index.html#//apple_ref/doc/uid/TP40007212)。

##Ad Support Framework
Ad Support framework (*AdSupport.framework*) 为 apps 提供一个用于广告目的 identifier 的访问。这个框架也提供一个说明用户是否已经选择退出广告追踪的标示。Apps 在需要读取和 honor 选择退出标示之前需要尝试访问广告 identifier。

更多关于使用这个框架的信息，见 [*Ad Support Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/DeviceInformation/Reference/AdSupport_Framework/index.html#//apple_ref/doc/uid/TP40012658)。

##CFNetwork Framework
CFNetwork framework (CFNetwork.framework) 是使用面向对象的抽象概念与网络协议一起工作的基于 C 语言的高性能的接口的集合。这些抽象概念给你详细控制协议堆栈和使它轻松的使用 lower-level 构造例如 BSD sockets。你可以使用这个框架简化任务例如和 FTP 和 HTTP 服务器通信或者解析 DNS hosts。使用 CFNetwork framework，你可以：

- 使用 BSD sockets
- 使用 SSL 或 TLS 创建加密连接
- 解析 DNS hosts
- 与 HTTP 服务器共同工作，认证 HTTP 服务器，和 HTTPS 服务器
- 与 FTP 服务器共同工作
- 发布，解析，和浏览 Bonjour 服务。

BSD sockets 是基于CFNetwork 的，物理上和理论上都是。

更多关于如何使用 CFNetwork 的信息，见 [*CFNetwork Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Networking/Conceptual/CFNetwork/Introduction/Introduction.html#//apple_ref/doc/uid/TP30001132) 和 [*CFNetwork Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CFNetwork/Reference/CFNetwork_Framework/index.html#//apple_ref/doc/uid/TP40007128)。

##CloudKit Framework
CloudKit (*CloudKit.framework*) 为你的 app 和 iCloud 之间移动数据提供了管道。它不像其他的 iCloud 技术在数据传输时是透明的，当数据传输时 CloudKit 能让你控制。你可以使用 CloudKit 管理所有数据的类型。

App 可以直接使用 CloudKit 在对所有用户共享的仓库里保存数据。公开的仓库是绑定到 app 的自身即使设备没有已注册的 iCloud 账户也可以使用。作为 app 的开发者，你可以直接在容器管理数据和通过 CloudKit dashboard 观察用户所做的任何改变。

更多有关这个框架的类的信息，见 [*CloudKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CloudKit/Reference/CloudKit_Framework_Reference/index.html#//apple_ref/doc/uid/TP40014064)。

##Core Data Framework
Core Data framework (CoreData.framework) 是为管理 Model-View-Controller 的 app 的数据模型的技术。Core Data 适应于数据模型已高度结构化的 apps 上。而不是用在定义数据结构的编程方式。使用 Xcode 的图形工具构建代表你的数据模型的架构。在 runtime 时，你的数据模型实体实例已经通过 Core Data framework 创建，管理和可用。

通过管理你的 app 数据模型，Core Data 显著的缩减了代码量。Core Data 也提供下面这些功能：

- 为获得最佳性能而使对象数据存储在 SQLite 数据库中。
- 一个为 table view 管理结果的 [*NSFetchedResultsController*](https://developer.apple.com/library/prerelease/ios/documentation/CoreData/Reference/NSFetchedResultsController_Class/index.html#//apple_ref/occ/cl/NSFetchedResultsController) 类
- 超越基本的文本编辑的 undo/redo 的管理
- 支持属性值的验证
- 传播变化 (propagating changes) 的支持和确保两个对象的关系保持一致
- 支持在内存的分组，过滤，和组织数据。

如果你准备开始开发一个新的 app 或者正在为已有的 app 准备一个重大的更新，你应该考虑使用 Core Data。关于如何在 app 中使用 Core Data 的案例，见 *Core Data Tutorial for iOS*。

更多关于 Core Data framework 的类的信息，见 [*Core Data Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/CoreData_ObjC/index.html#//apple_ref/doc/uid/TP40001181)。

##Core Foundation Framework
Core Foundation framework (*CoreFoundation.framework*) 是基于 C 语言的接口集合，为 iOS 的 apps 提供了基础数据管理和服务功能。这个框架包含了下面的支持：

- 集合数据类型 (array,set 等等)
- Bundles
- 字符串管理
- 日期和时间管理
- 原始数据块管理
- Preferences 管理
- URL 和 stream 操作
- 线程和运行循环
- 端口和套接字通信

Core Foundation framework 与 Foundation framework 密切相关，它为同样的基础功能提供了 Objective-C 的接口。当你需要混合使用 Foundation objects 和 Core Foundation types，你可以利用存在于两个框架之间 "toll-free bridging" 。*Toll-free bridging* 意味着你可以使一些 Core Foundation 和 Foundation types  在两个框架的方法和函数中互相转换。可用于非常多的数据类型，包括集合和字符串数据类型。为每一个框架声明的类和类型描述了对象是否可以被 toll-free bridge 的，如果可以，还会说明什么对象是可以被连接。

更多关于这个框架的信息，见 [*Core Foundation Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreFoundation/Reference/CoreFoundation_Collection/index.html#//apple_ref/doc/uid/TP40003849)。

##Core Location Framework
Core Location framework (*CoreLocation.framework*) 为 apps 提供位置和导航信息。对位置信息，框架使用了板载 GPS，手机信号，或 Wi-Fi 信号寻找用户当前的经度和纬度。你可以在 app 中整合这个技术提供基于位置信息的服务给用户。例如，可以获取用户当前的位置提供临近餐馆，商店，或其他设施的服务的地址给用户。Core Location 也提供以下功能：

- 访问 iOS 设备上的磁力仪提供基于指南针的导航信息
- 提供基于物理位置或蓝牙信标的区域检测支持
- 使用手机信号塔提供低功耗的位置监测。
- 与 MapKit 合作提高某些情景下的位置数据的质量，例如开车时。

更多关于如何使用 Core Location 采集位置和导航信息，见 [*Location and Maps Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/LocationAwarenessPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009497)  和 [*Core Location Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreLocation/Reference/CoreLocation_Framework/index.html#//apple_ref/doc/uid/TP40007123)。

##Core Media Framework
Core Media framework (*CoreMedia.framework*) 提供了用在 AV Foundation framework 上的低级别的媒体类型。大多数 app 永远不需要使用这个框架，少数需要精确的控制音频和音频内容的创建和呈现的开发者会使用。

更多关于这个框架的函数和数据类型的信息，见  [*Core Media Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreMedia/Reference/CoreMediaFramework/index.html#//apple_ref/doc/uid/TP40009756)。

##Core Motion Framework
Core Motion framework (*CoreMotion.framework*) 提供了访问设备上所有可用的基于监测的数据的独立接口集合。这个框架支持使新的 [block-based]() 接口集合访问原始的和已处理的加速器数据 (raw and processed accelerometer)。对于设备内置的陀螺仪 (gyroscope)，你可以获取原始陀螺数据以及已处理的反映设备的 attitude 和旋转速率 (rotation rates)的数据。你也可以为 games 或其他  app 同时使用加速器和陀螺仪数据作为输入的监测或作为增强用户体验的方式。对于拥有计步器设备，你可以访问它的数据并使用它追踪用户的健康相关活动。

更多关于这个框架的方法和类的信息，见 [*Core Motion Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreMotion/Reference/CoreMotion_Reference/index.html#//apple_ref/doc/uid/TP40009686)。

##Core Telephony Framework
Core Telephony framework (*Coretelephony.framework*) 提供有蜂窝无线设备的基于电话信息的交互接口。Apps 可以使用这个框架取得关于用户的蜂窝服务提供商的信息。对蜂窝呼叫事件感兴趣的 app (例如 VoIP apps)，当事件发生时可以被通知。


更多关于这个框架的方法和类的使用的信息，见 [*Core Telephony Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Reference/CoreTelephonyFrameworkReference/index.html#//apple_ref/doc/uid/TP40009603)。

##EventKit Framework
EventKit framework (*EventKit.framework*) 提供访问用户设备的日历活动的接口。你可以使用这个框架做以下事情：

- 从用户的日历获取已有的活动和提醒
- 在用户的日历上添加活动
- 为用户创建提醒并让它们在其他提醒的 app 中出现
- 为日历活动创建警报，包括被设置触发时的提醒规则。

> 重要提醒：访问用户日历和提醒数据需要用户明确的授权。Apps 必须为用户拒绝提供权限作准备。Apps 也因该提供 *Info.plist* 键说明需要这个权限的原因。

更多关于这个框架的方法和类的信息，见 [*EventKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/EventKit/Reference/EventKitFrameworkRef/index.html#//apple_ref/doc/uid/TP40009662) 和 [*Event Kit UI Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/iPhoneOSTechnologies/iPhoneOSTechnologies.html#//apple_ref/doc/uid/TP40007898-CH3-SW3)。

##Foundation Framework
Foundation framework (*Foundation.framework*) 用 Objective-C 封装了非常多的可以在 Core Foundation framework 中找到的功能，在 [*Core Foundation Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW1) 有描述。这个框架提供下面功能的支持：

-  集合数据类型 (array,sets 等等)
- Bundles
- 字符串管理
- 日期和时间管理
- 原始数据块管理
- Preference management
- URL 和 stream 操作
- 线程和运行循环
- Bonjour
- 通信端口管理
- Internationalization
- 正则表达式运算
- 缓存支持

更多关于 Foundation framework 的类信息，见  [*Foundation Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/ObjC_classic/index.html#//apple_ref/doc/uid/20001091)。

##HealthKit Framework
HealthKit (*HealthKit.framework*) 是新的管理用户健康相关的数据的框架。
随着追踪健康和健身信息的设备和 apps 的泛滥，用户难以获得清晰的他们在做什么的界面。HealthKit 使 apps 分享健康相关的信息变的简单，无论是来自连接到 iOS 设备的信息或用户手动录入的信息。用户的健康相关信息都被保存在集中的和安全的位置。然后用户可以在 Health app 中看到所有数据显示。

当你的 app 对 HealthKit 实现了支持，它会为用户获取与健康相关信息和提供关于用户的信息，不需要声明支持特定的健身追踪设备。用户可以决定数据是否共享给你的 app。一旦数据对你的 app 共享，可以申请当数据发生改变时通知你的 app。你可以对通知进行细致的设置。例如，每当用户取得了他或她的血压时你可以请求通知你的 app，或只在测量结果中的用户血压到达特定的读数时才被通知。

更多关于这个框架的接口的信息，见 [*HealthKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/HealthKit/Reference/HealthKit_Framework/index.html#//apple_ref/doc/uid/TP40014707)。

##HomeKit Framework
HomeKit (*HomeKit.framework*) 是新的与用户家庭的已连接设备的通信和控制的框架。为家庭准备新引入的设备提供更多连接方式和更好的用户体验。HomeKit 提供了标准化的方式与这些设备进行通信。

你的 app 可以使用 HomeKit 与用户家中已有的设备通信。用户可以使用你的 app 搜索家中的设备和配置他们，也可以创建操作控制这些设备。用户也可以一起聚合操作和使用 Siri 触发他们。一旦配置创建完成，用户可以邀请其他人对他的访问。例如，可以暂时给访客提供访问权限。

可以使用 HomeKit 配套的模拟器来测试你的 HomeKit app 与设备间的通信。

更多关于这个框架的接口信息，见 [*HomeKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/HomeKit/Reference/HomeKit_Framework/index.html#//apple_ref/doc/uid/TP40014519)。

##JavaScript Core Framework
JavaScript Core framework (*JavaScriptCore.framework*) 用 Objective-C 将许多标准 JavaScript 的对象封装成类。这个框架可以 evaluate JavaScript 的代码和解析 JSON 数据。

更多关于这个框架的类的信息，见它的头文件。

##Mobile Core Services Framework
Mobile Core Service framework (MobileCoreService.framework) 定义了被用在统一类型标识符 (UTIs) 的 low-level 类型。

更多关于这个框架定义的类型信息，见 [*Uniform Type Identifiers Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Reference/UTIRef/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009257)。


##Multipeer Connectivity Framework
Multipeer Connectivity framework (MultipeerConnectivity.framework) 提供了查找临近的设备并和它们直接通信而不需要通过网络连接。这个框架能轻松建立多点会话和传输可靠的有序数据和传输实时数据。在这个框架中，你的 app 可以与临近设备通信，和无缝交换数据。

这个框架提供了以编程的方式和基于 UI 选项的方式搜索和管理网络服务。Apps 可以整合 [*MCBrowserViewController*](https://developer.apple.com/library/prerelease/ios/documentation/MultipeerConnectivity/Reference/MCBrowserViewController_class/index.html#//apple_ref/occ/cl/MCBrowserViewController) 类到 UI 中显示每个设备的列表供用户选择。另外，你可以使用 [*MCNearbyServiceBrowser*](https://developer.apple.com/library/prerelease/ios/documentation/MultipeerConnectivity/Reference/MCNearbyServiceBrowserClassRef/index.html#//apple_ref/occ/cl/MCNearbyServiceBrowser) 类以编程的方式搜寻和管理对等设备。

更多关于这个框架的接口信息，见 [*Multipeer Connectivity Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MultipeerConnectivity/Reference/MultipeerConnectivityFramework/index.html#//apple_ref/doc/uid/TP40013328)。

##NewsstandKit Framework
Newsstand app 提供了一个阅读杂志和报纸的中心位置。出版社想要通过 Newsstand 推送他们的杂志和报纸内容可以通过使用 NewsstandKit framework (*NewsstandKit.framework*) 创建他们自己的 iOS apps，它让你开启新杂志和报纸发布的后台下载。当开始下载之后，系统操作下载处理和通知你的 app 有新的可用内容。

更多使用它来管理 Newsstand 下载的类的信息，见 [*NewsstandKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/StoreKit/Reference/NewsstandKit_Framework/index.html#//apple_ref/doc/uid/TP40010838)。

更多关于如何使用通知中心通知你的 apps，见 [*Local and Remote Notification Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html#//apple_ref/doc/uid/TP40008194)。

##PassKit Framework
Passbook app 为用户提供了保存优惠卷，登机牌，活动门票，和对企业打折卡的的位置。替代了以物理方式携带这些表示牌，用户可以将他们保存到 iOS 设备中并像以前一样使用它们。PassKit framework (*PassKit.framework*) 为你提供了 Objective-C 接口整合这些功能到你的 app 中。可以使用 web 接口和文件格式信息的组合中使用这个框架来创建和管理你的公司提供的通行证。

通行证是被你的公司的 web 服务创建并且通过 email，Safari或你自定义的应用程序投递到用户设备。通行证本身，是使用特定的文件格式，发送之前经过加密签名。文件格式鉴别服务所提供的信息使得用户清楚它是为什么服务的。它也许包含条码或其他信息可以把他作为验证卡用于兑换卷使用。

更多关于 PassKit 的信息和如何让你的 app 获得支持的信息，见 [*Passbook programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/PassKit_PG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40012195)。

##Quick Look Framework
Quick Look framework (QuickLook.framework) 提供了直观的界面预览你的 apps 不直接支持的文件内容。这个框架主要为提供网络下载文件的 app 和为来源不明的文件以其他方式工作的app提供。获得文件之后，可以使用框架提供的 view controller 直接在你的用户界面中显示文件内容。

更多关于这个框架的类的信息，见 [*Quick Look Framework Reference for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/QuickLook/Reference/QuickLookFrameworkReference_iPhoneOS/index.html#//apple_ref/doc/uid/TP40009672)。

##Safari Service Framework
Safari Service framework (SafariServices.framework) 提供了以编程的方式添加 URLs 到用户的阅读列表。

更多关于这个框架提供的类的信息，见框架的头文件。

##Social Framework
Social framework (Social.framework) 提供了简便的接口访问用户的社交媒体账户。这个框架取代了 Twitter framework 并增加了对其他社交账户的支持，包括 Facebook，Sina Weibi，和其他。Apps 可以使用这个框架投递状态更新和图像给用户的账户。这个框架与 Accounts framework 共同使用为用户提供单点登陆模式确保访问的用户账户是合法的。

更多关于 Social framework 的信息，见  [*Social Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Social/Reference/Social_Framework/index.html#//apple_ref/doc/uid/TP40012233)。

##SotreKit Framework
StoreKit framework (StoreKit.framework) 为你的 iOS apps 提供了内容和服务购买的支持，我们知道的对应的服务是 *In-App Purchase*。例如，你可以使用这个功能让用户解锁额外的 app 功能。或者如果你是游戏开发者，你可以使用它提供额外的游戏等级。zzai这两种案例中，StoreKit framework 处理财务交易，通过用户的 iTunes 商店用户和你的 app 提供的相关购买信息进行处理。

StoreKit 关注交易方面内容，确保交易的安全和正确。你处理其他方面的事务，包括购买界面的介绍和下载 (或解锁) 适当内容。这种分工可以掌控购买内容和加强用户体验。你可以决定何时呈现购买界面给用户并且要呈现怎样的界面给用户。你也可以选择最适合你的 app 的支付机制。

关于如何使用 StoreKit framework 的信息，见 [*In-App Purchase Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/NetworkingInternet/Conceptual/StoreKitGuide/Introduction.html#//apple_ref/doc/uid/TP40008267) 和 [*StoreKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/StoreKit/Reference/StoreKit_Collection/index.html#//apple_ref/doc/uid/TP40008300)。

##System Configuration Framework
System Configuration framework (*SystemConfiguration.framework*) 提供了 可 访问性接口，可以用它判断设备的网络配置。例如判断是否使用 Wi-Fi，或者是否在使用蜂窝连接，是否可以访问特定的主机服务器。

更多关于这个框架的接口，见 [*System Configuration Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Networking/Reference/SysConfig/index.html#//apple_ref/doc/uid/TP40001027)。

关于如何使用这个框架获得网络信息的示例，见 [*Reachability*](https://developer.apple.com/library/prerelease/ios/samplecode/Reachability/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007324) sample code project。

##WebKit Framework
WebKit framework (*WebKit.framework*) 可以在你的 app 中显示 HTML 内容。除了显示 HTML 内容，你还可以提供基本编辑支持，使用户可以替换文本和操作文档的文本和属性，包括 CSS 属性。WebKit 也支持在 HTML 文档的 DOM 级别创建和编辑内容。例如，你可以提取页面上的链接的列表，并修改他们，和在文档在 web view 显示之前替换掉他们。

关于这个框架的接口信息，见 [*WebKit Framework Referenec*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/WebKit/ObjC_classic/index.html#//apple_ref/doc/uid/TP30000745)。


#**系列文章**
[*iOS 笔记《About the iOS Technologies：Cocoa Touch Layer》*](../iOS-Note-About-the-iOS-Technologies-Cocoa-Touch-Layer)
[*iOS 笔记《About the iOS Technologies：Media Layer》*](../iOS-Note-About-the-iOS-Technologies-Media-Layer)
*iOS 笔记《About the iOS Technologies：Core Service Layer》*
[*iOS 笔记《About the iOS Technologies：Core OS Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-OS-Layer) 



---------

[1]: https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898-CH1-SW1