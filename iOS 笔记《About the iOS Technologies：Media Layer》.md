layout: [post]
title: "iOS 笔记《About the iOS Technologies：Media Layer》"
date: 2015-04-25 08:31:26
tags: 
- iOS
categories: 
- iOS
- 翻译
id: "iOS-Note-About-the-iOS-Technologies-Media-Layer"
---

记录关于学习过的 iOS 文档

<!-- more -->

[原文地址][1]




-------------------
Media layer 包含了图形，音频，和视频技术，可以实现你的 apps 的多媒体体验。这些技术在该层中使你非常简单的建立美观和动听的 app。
<!-- more -->
#**Graphics Technologies**
高质量的图形是所有 app 中重要的一部分，iOS 提供了众多技术帮助你摆放自定义的艺术品和屏幕图形。iOS 图像技术提供了广泛的支持，与 UIKit view architecture 无缝工作使得它轻松的提供内容。你可以使用这些标准的 views 快速呈现出高质量的界面，或者你可以创建你自己的自定义视图和使用下面任意的技术呈现出更丰富的图形体验。

##UIKit Graphic
UIKit 定义了 high-level 的支持来绘制图像和贝塞尔路径，和你的 views 的内容的动画。此外还提供了类来实现绘图的支持，UIKit views 提供了快速和高效方式渲染图像和基于文本内容。Views 也可以是动画形式的，明确的使用 UIKit dynamics，提供反馈和加强与用户的互动。

更多关于 UIKit 框架的信息，见 [*UIKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIKit_Framework/index.html#//apple_ref/doc/uid/TP40006955)。

##Core Graphics framework
*Core Graphics* (也称为 *Quartz*) 是 iOS apps 的原生绘图引擎，支持自定义的 2D 矢量和基于图像的渲染。尽管渲染速度不像 OpenGL ES 一般快捷，但这个框架也是渲染 2D 图形和动态图像的一种非常适合的选择。

更多相关的信息，见 [*Core Graphics Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW9)。

##Core Animation
*Core Animation* ( Quartz Core framework 的一部分) 是可优化你的 apps 的动画体验的基础技术。UIKit views 使用 Core Animation 提供 view-level 的动画支持。当你想要加强控制你的动画效果时可以使用直接使用 Core Animation。

更多相关信息，见 [*Quartz Core Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW17)。

##Core Image
*Core Image* 为操作视频和以无损方式显示静止图像的高级支持。

更多相关信息，见 [*Core Image Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW20)。

##OpenGL ES and GLKit
*OpenGL ES* 使用硬件加速的接口，先进的处理 2D 和 3D渲染。这个框架是游戏开发者传统上使用的，或者其他想实现酷炫的图形体验的开发者使用。这个框架给你完全的控制渲染处理和创建流程动画所需要用到的帧速率。

更多相关的信息，见 [*OpenGL ES Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW15)

*GLKit* 是 Objective-C 类的集合，使用了面相对象接口对 OpenGL ES 提供了强力的支持。

更多相关的信息，见 [*GLKit Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW21)。

##Metal
*Metal* 提供了以极低的开销 (low-overhead) 访问 A7 GPU，使得你的复杂的动画渲染和计算任务获得难以置信的性能。Metal 消除了非常多的性能瓶颈 －例如昂贵的状态验证：在传统的图形 APIs 发现了这个问题。

更多相关的信息，见 [*Metal Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW28)。

##TextKit and Core Text
*TextKit* 是 UIKit 系列类的家族成员，用作执行精美排版和文本管理，如果你的 app 需要一些进阶的文本操作，TextKit 提供了与你的视图区域无缝集成。

更多相关信息， [*Text Kit*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/iPhoneOSTechnologies/iPhoneOSTechnologies.html#//apple_ref/doc/uid/TP40007898-CH3-SW11)。

*Core Text* 是基于 C 语言的 lower-level 框架，为处理高阶的排版和布局。

更多相关信息，见 [*Core Text Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW10)。

##Image I/O
*Image I/O* 为大量的图像格式读写提供了接口。

更多相关信息，见 [*Image I/O Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW16)。

##Photos Library
*Photos* 和 *PhotosUI* 框架提供了访问用户的照片，影像，和多媒体。当你想集成用户的内容到你的 app 中你可以使用该框架。

更多相关的信息，见 [*Photos Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW29) 和 [*Photos UI Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW30)。



##额外设备的支持
iOS 提供了构建 apps 到其他 Retina 显示器或标准分辨率显示的支持。对于基于矢量的绘图，系统自动使用额外的像素点在 Retina 显示屏上提高你的内容的 crispness。如果你在你的 app 中使用图像，UIKit 为你存在的图像自动化加载高分辨率变化 (high-resolution variants)。

更多关于如何支持高分辨率屏幕的信息，见 [*App Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007072) 中的 [*App-Relate Resource*](https://developer.apple.com/library/prerelease/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html#//apple_ref/doc/uid/TP40007072-CH6)。

#**Audio Technologies**
iOS 音频技术在底层硬件中工作，为用户提供了丰富的音频体验。这些体验包含播放和录制高质量的音频，处理 MIDI 内容，并与设备内置的声音工作。

如果你的 app 用到了音频，这里有几种技术可供使用。下面是这些框架和对使用场景的描述。

##Media Player framework
这是一个高级别 (high-level) 的框架提供了简单的访问 iTunes 库的方法和对播放曲目和播放列表的支持。当你想快速的集成音频到你的 app 中并且你不需要控制播放行为时，可以使用这个框架。

更多相关信息，见 [*Media Player Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW12)。

##AV Foundation
*AV Foundation* 是管理录音和播放音频和视频的 Objective-C 的接口。当你需要录音和对音频播放进行精细的控制时，使用这个框架。

更多相关信息，见 [*AV Foundation Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW7)。

## OpenAL
*OpenAL* 是一个提供音频定位的行业标准技术。游戏开发者会频繁使用这个技术的跨平台接口提供高质量的音频。

更多相关的信息，见 [*OpenAL Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW13)。

##Core Audio
*Core Audio* 是一系列框架的集合，提供了简单复杂的接口来录制和播放音频和 MIDI 内容。这个框架是为需要精细控制音频的高阶开发者提供。

更多相关信息，见 [*Core Audio*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW8)

##iOS 支持的音频格式
iOS 支持许多行业标准和 Apple 特有的音频格式，包括以下的：

- AAC
- Apple Lossless (ALAC)
- A-law
- IMA/ADPCM (IMA4)
- Linear PCM
- µ-law
- DVI/Intel IMA ADPCM
- Microsoft GSM 6.10
- AES3-2003

#**Video Technologies**
iOS 视频技术提供了在你的 app 中管理静态视频内容或从互联网播放流媒体内容。对某些可用的录制硬件，你可以录制并合并到你的 app 中。下面的技术提供了视频的播放和录制的支持。

##UIImagePickerController
[*UIImagePickerController*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIImagePickerController_Class/index.html#//apple_ref/occ/cl/UIImagePickerController) 类是一个选择用户媒体文件的 UIKit view controller。你可以使用这个 view controller 提示让用户选择一个已经存在的图片或视频或者让用户拍摄新的内容。

更多相关信息，见 [*Camera Programming Topics for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/CameraAndPhotoLib_TopicsForIOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010400)。

##AVKit
AVKit 框架提供了简便实用的接口集合来展示视频。这个框架提供全屏幕和局部屏幕 (partial-screen) 进行视频播放，和为用户提供播放控制选择。

更多喜庆关信息，见 [*AVKit Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW27)。

##AV Foundation
AV Foundation 提供了高阶的视频播放和录制功能。当你需要更多的控制视频的演示和录制的情况时，使用这个框架。例如，增强现实功能的 apps 可以使用这个框架分层显示现实的内容和其他 app 提供的内容。

更多相关信息，见 [*AV Foundation Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW7)。

##Core Media
Core Media 框架定义了低级别 (low-level) 数据类型和操纵媒体的接口。大多数 app 不会直接使用这个框架，但当你需要最高的权限的控制你的 app 的视频内容时，是可以使用它的。

更多相关信息，见 [*Core Media Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW17)。


##支持的视频格式和压缩标准
iOS 支持许多行业标准的视频格式和压缩标准，包含以下：

- H.264 video, up to 1.5 Mbps, 640 by 480 pixels, 30 frames per second, Low-Complexity version of the H.264 Baseline Profile with AAC-LC audio up to 160 Kbps, 48 kHz, stereo audio in .m4v, .mp4, and .mov file formats
H.264 video, up to 768 Kbps, 320 by 240 pixels, 30 frames per second, Baseline Profile
- up to Level 1.3 with AAC-LC audio up to 160 Kbps, 48 kHz, stereo audio in .m4v, .mp4, and .mov file formats
- MPEG-4 video, up to 2.5 Mbps, 640 by 480 pixels, 30 frames per second, Simple Profile with AAC-LC audio up to 160 Kbps, 48 kHz, stereo audio in .m4v, .mp4, and .mov file formats
- 更多大量的视频格式,见 [*Audio Technologies*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/MediaLayer/MediaLayer.html#//apple_ref/doc/uid/TP40007898-CH9-SW2)。

#**AirPlay**
*AirPlay* 能让你 app 发送 (stream) 视频和音频内容到 Apple TV 中和发送音频内容到第三方的 AirPlay 扬声器和接收器。AirPlay 支持众多的内置框架 - UIKit 框架，Media Player 框架，AV Foundation 框架，和 Core Audio 家族的框架，因此在大多数情况下你不需要特别的去做某些事情来获得支持。你使用这些框架播放的任何内容会自动取得 AirPlay 资格。当用户选择用 AirPlay 播放你的内容时，它会通过系统自动路由。

交付内容给 AirPlay 的附加方案：

- 通过 iOS 设备显示拓展的内容，创建第二个窗口对象并且分配它到任何的通过 AirPlay 连接到设备上的 [*UIScreen*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIScreen_Class/index.html#//apple_ref/occ/cl/UIScreen) 对象。当你的内容在附加屏幕的显示不同于内容在 iOS 设备上显示的时候，使用这个技术。
- 媒体播放框架的播放类自动支持 AirPlay，你也可以使用 AirPaly 在已连接的 Apple TV 显示当前播放的内容。
- 在 AV Foundation 中使用 [*AVPlayer*](https://developer.apple.com/library/prerelease/ios/documentation/AVFoundation/Reference/AVPlayer_Class/index.html#//apple_ref/occ/cl/AVPlayer) 类管理你的 app 的音频和视频内容。这个类支持通过 AirPlay  streaming 他的内容，当用户启用了 AirPlay 的时候。
- 对于基于网络的音频和视频，可以允许内容在 AirPlay 播放，通过包含 *ember* 标签和 *airplay* 属性。[*UIWebView*](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIWebView_Class/index.html#//apple_ref/occ/cl/UIWebView) 类也支持使用 AirPlay 的多媒体播放。

更多关于如何在你的 apps 中利用 AirPlay，见 [*AirPlay Overview*](https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AirPlayGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011045)。

#**Media Layer Frameworks**
下面的章节描述了 Media Layer 的框架和它们提供的服务。

##Assets Library Framework
Assets Library framework (*AssetsLibrary.framework*) 提供访问图片和视频以便通过设备上的图片 app 管理。使用这个框架访问已保存的图片专辑 (album) 项目或已导入到该这个设备专辑。你也可以保存新的照片和视频到用户已保存的图片专辑。

更多关于这个框架的类集和方法的信息，见 [*Assets Library Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/AssetsLibrary/Reference/AssetsLibraryFramework/index.html#//apple_ref/doc/uid/TP40009730)。

##AV Foundation Framework
AV Foundation framework (*AVFoundation.framework*) 为播放，录音，和管理音频和视频内容而提供的 Objective-C 类的集合。当你想要无缝集成多媒体到你的 app 的界面中时，使用这个框架。你也可以使用它进行更高级的媒体处理。例如，你可以使用这个框架同时播放多个声音，和控制播放和录制过程的多个方面。

这个框架提供的服务包括：

- 音频会话管理，包括支持声明你的 app 的音频功能到系统中。
- 管理你的 app 的媒体资源。
- 支持编辑媒体内容。
- 录制视频和音频的能力
- 播放视频和音频的能力
- 跟踪管理 (Track management)
- 媒体项目的原数据管理
- 立体声声像
- 声音的精确同步
- 判断关于声音文件的细节的 Objective-C 的接口，例如数据格式，采样率，和频道数字
- 支持 streaming 到 AirPlay

更多关于如何使用 AV Foundation，见 [*AV Foundation Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/00_Introduction.html#//apple_ref/doc/uid/TP40010188)。

关于 AV Foundation framework 的类的信息，见 [*AV Foundation Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/AVFoundation/Reference/AVFoundationFramework/index.html#//apple_ref/doc/uid/TP40008072)。


##AVKit Framework
AVKit framework (*AVKit.framework*) 充分利用 AV Foundation 现有的对象管理设备上呈现的视频。当你需要显示视频内容时它作为多媒体播放框架的代替选择。

更多关于这个框架的信息，见它的头文件。

##Core Audio
Core Audio 是一个框架的家族。它提供了原生的音频处理支持。这些框架支持在你的 app 中生成，录制，混合，和播放音频。你也可以使用这些接口与 MIDI 内容一起工作，和 stream 音频和 MIDI 内容到其他 app。下面是成员介绍：

- CoreAudio.framework，定义了整个 Core Audio 使用的音频数据类型。更多相关信息，见 [*Core Audio Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MusicAudio/Reference/CACoreAudioReference/index.html#//apple_ref/doc/uid/TP40002090)。
- AudioToolbox.framework，为 streams 和音频文件提供了播放和录制服务。这个框架也提供支持管理音频文件，播放系统警报声音，和触发某些设备的震动。更多相关的信息，见 [*Audio Toolbox Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MusicAudio/Reference/CAAudioTooboxRef/index.html#//apple_ref/doc/uid/TP40002089)。
- AudioUnit.framework，为使用内置的音频单元提供服务，它是音频处理模块。这个框架也支持 vending 你的 app 的 音频内容作为音频组件在其他的 app 中显示。更多信息，见 [*Audio Unit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/AudioUnit/Reference/AudioUnit_Framework/index.html#//apple_ref/doc/uid/TP40007295)。
- CoreMIDI.framework，提供了与 MIDI 设备通信的标准方式，包括硬件键盘和合成器。使用该框架发送和接收 MIDI 信息，和使用基座连接器或网络使得 iOS 设备 (iOS-based) 与 MIDI 外设进行交互。更多相关信息，见 [*Core MIDI Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MusicAudio/Reference/CACoreMIDIRef/index.html#//apple_ref/doc/uid/TP40002091)。
- MediaToolbox.framework,提供访问音频点击界面。 

更多关于 Core Audio 信息，见 [*Core Audio Overview*](https://developer.apple.com/library/prerelease/ios/documentation/MusicAudio/Conceptual/CoreAudioOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40003577)。

更多关于如何使用 Audio Toolbox framework 播放声音，见 [*Audio Queue Services Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/MusicAudio/Conceptual/AudioQueueProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005343)。

##CoreAudioKit Framework
CoreAudioKit framework (CoreAudioKit.framework) 为跨 app 的音频提供标准视图进行管理。一个视图提供显示已连接上的 app 的图标的开关 (switcher) ，其他的视图显示传输控制，使得用户可以通过主 app 控制音频。

更多相关信息，见框架的头文件。

##Core Graphics Framework
Core Graphics framework (CoreGraphics.framework) 包含了 Quartz 2D 绘制 API 的接口。*Quartz* 是用在 OS X 上的一个同样先进，基于矢量的绘制引擎。它只是基于路径的绘制，抗锯齿渲染，渐变，图像，颜色，坐标空间转换，和 PDF 文档创建，显示，和粘贴。尽管这个 API 是基于 C 语言的，但它使用基于对象的抽象来表现基本的绘图对象，使得它容易的保存和重用你的图像内容。

更多关于如何使用 Quartz 绘制内容，见 [*Quartz 2D Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/Introduction/Introduction.html#//apple_ref/doc/uid/TP30001066) 和 [*Core Graphics Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/CoreGraphics/Reference/CoreGraphics_Framework/index.html#//apple_ref/doc/uid/TP40007127)。

##Core Image Framework
Core Image framework (CoreImage.framework) 为管理视频和静态图像提供了强大的内置过滤器集合。你可以对任何事情使用内置过滤器，如通过触摸修正照片的脸部，特点，和 QR 码检测等。这个过滤器的优点是他们以无损的方式处理，去除过滤器后你的原始图像不会改变。因为这个过滤器优化了底层硬件，它们非常快捷和有效率。

更多关于 Core Image framework 的过滤器和类，见  [*Core Image Reference Collection*](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsImaging/Reference/CoreImagingRef/index.html#//apple_ref/doc/uid/TP40001171)。 

##Core Text Framework
Core Text framework (CoreText.framework) 提供了使用简单，基于 C 语言接口的高性能布局文本和字体处理。这个框架为不使用 TextKit 但仍旧想拥有进阶的文字处理能力的文字处理 app 支持。这个框架提供了复杂的文字布局引擎，包括文本环绕其他内容的能力。它也支持使用多种字体和渲染属性的先进文本样式。

更多关于 Core Text 接口，见 [*Core Text Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/StringsTextFonts/Conceptual/CoreText_Programming/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005533) 和 [*Core Text Reference Collection*](https://developer.apple.com/library/prerelease/ios/documentation/Carbon/Reference/CoreText_Framework_Ref/index.html#//apple_ref/doc/uid/TP40005304)。

##Core Video Framework
Core Viewo framework (CoreVideo.framework) 为 Core Media framework (在 [*Core Media Framework*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW17) 描述) 提供了缓冲和缓冲池支持。大多数 app 不需要直接使用这个框架。

##Game Controller Framework
Game Controller framework (GameController.framework) 在你的 app 中让你发现和配置 Made-for-iPhone/iPod/iPad (MFi) 游戏的控制器硬件。Game controller 可以使设备物理连接或通过无线蓝牙连接到 iOS 设备。当控制器变为可用时 Game Controller framework 会通知你的 app，让你指定控制器输入的内容对应你的 app 。

更多关于 game controller 的配套信息，见 [*Game Controller Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40013276)。

##GLKit Framework
GLKit framework (GLKit.framework) 包含了基于 Objective-C 高效工具类集合，简化了创建一个 OpenGL ES app 的需要做的工作。GLKit 支持一下 app 开发的关键方面：

- [*GLKView*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKView_ClassReference/index.html#//apple_ref/occ/cl/GLKView) 和 [*GLKViewController*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKViewController_ClassRef/index.html#//apple_ref/occ/cl/GLKViewController) 类提供了一个 OpenGL ES 的启用视图和相关渲染的循环的标准实现。这个 view 管理代表 app 上的底层帧缓冲区对象。你的 app 只需要在上面绘制。
- [*GLKTextureLoader*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKTextureLoader_ClassRef/index.html#//apple_ref/occ/cl/GLKTextureLoader) 类提供图像转换和加载到程序 (loading routines) 到你的 app,允许它自动化加载贴图图像到你 context。它可以同步加载贴图或异步加载。当是异步加载贴图时，当贴图完成在你的 context 加载后你的 app 提供一个完整的处理程序块供其调用。
- *GLKit framework* 提供了矢量，矩阵，和 quaternions 的声明，以及在 OpenGL ES 1.1 中提供的相同功能的矩阵堆栈操作。
- [*GLKBaseEffect*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKBaseEffect_ClassRef/index.html#//apple_ref/occ/cl/GLKBaseEffect),[*GLKSkyboxEffect*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKSkyboxEffect_ClassRef/index.html#//apple_ref/occ/cl/GLKSkyboxEffect),和 [*GLKReflectionMapEffect*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKReflectionEffect_ClassRef/index.html#//apple_ref/occ/cl/GLKReflectionMapEffect) 类提供已有的，实现常用的图形运算的可配置的图形着色引擎。特别是，GLKBaseEffect 类实现了 OpenGL ES 1.1 specification 的高光和材料模型，简化了 app 从 OpenGL ES 1.1 迁移到之后的 OpenGl ES 版本的工作量。

更多关于 GLKit framework 的类的信息，见 [*GLKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/GLkit/Reference/GLKit_Collection/index.html#//apple_ref/doc/uid/TP40010915).。

##Image I/O Framework
Image I/O framework (ImageIO.framework) 为导入和导出图像数据和图像元数据提供了接口。这个框架利用了 Core Graphics 的数据类型和功能，支持在 iOS 使用所有标准图像格式。你也可以使用这个框架访问图像的 Exif 和 IPTC 元数据属性。

更多关于这个框架在数据类型和功能，见 [*Image I/O Reference Collection*](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsImaging/Reference/ImageIORefCollection/index.html#//apple_ref/doc/uid/TP40005102)。

##Media Accessibility Framework
Media Accessibility framework (MediaAccessibility.framework) 管理你的媒体文件的隐蔽字幕内容的呈现。在用户的设置显示禁用隐蔽字幕使用到这个框架。

更多这个框见内容的相关信息，见头文件。

##Media Player Framework
Media Plyaer framework (MediaPlayer.framework) 为你的 app 的音频和视频内容提供了高级别支持。你可以使用这个框架做以下事情：

- 在用户的屏幕播放视频或通过 AirPlay 在其他设备播放视频。你可以以全屏幕或可调整尺寸方式播放视频。
- 访问用户的 iTunes 音乐库。可以播放音乐曲目和播放列表，查找歌曲，和呈现媒体选择界面给用户。
- 配置和管理电影播放。
- 在锁定屏幕下和 App 切换器中显示正在播放的信息。当内容是通过 AirPlay 传送时你也可以在 Apple TV 显示信息。
- 当视频时正在 steamed over AirPlay时的检测。

更多关于 Media Player framework 的类的信息，见 [*Media Player Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/MediaPlayer/Reference/MediaPlayer_Framework/index.html#//apple_ref/doc/uid/TP40006952)。更多关于如何使用这些类访问用户的 iTunes library，见 [*iPod Library Access Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Audio/Conceptual/iPodLibraryAccess_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008765)。

##Metal Framework
Metal 提供以极地的开销访问 A7 GPU 为你的复杂的图形渲染和计算任务提供难以置信的性能。Metal 消除了许多性能瓶颈 - 例如代价高昂的状态验证 - 传统的图形 APIs 中有这个问题。Metal 是明确设计来为移除所有高昂的状态转换和编译运算出你最影响性能的渲染代码的关键路径。Metal 提供了预编译 shaders,状态对象，和清晰的命令调度来确保你的应用程序实现最高的性能，和提升你的 GPU 图形和运算任务的效率。这个设计理念拓展到使用工具构建你的 app 上。当你的 app 构建完成，Xcode 在项目中编译 Metal shaders 到默认的库中，消除大多数为准备这些  shaders 造成的 runtime 损耗。

图形，计算，和内存命令是被设计为一起使用，可以实现无缝的和高效的。Metal 是充分利用现代架构考虑的特别设计，例如多处理器和共享的内存，使得轻松的并行创建 GPU 命令。

在 Metal，你拥有精简的 API，和统一的图形和计算的 shaders 语言，基于 Xcode 的同居，因此你不需要学习多种框架，语言和工具也可以在你的游戏或 app 中充分利用 GPU。

更多关于如何使用 Metal，见 [*Metal Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/MetalProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40014221)，[*Metal Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Metal/Reference/MetalFrameworkReference/index.html#//apple_ref/doc/uid/TP40014161)，和 [*Metal shading Language Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Metal/Reference/MetalShadingLanguageGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40014364)。

##OpenAL Framework
Open Audio Library (*Open AL*) 是在 app 中音频定位的跨平台标准接口。你可以用它在游戏或其他需要定位音频输出的程序实现高性能，高质量的音频。因为 OpenAL 是跨平台标准，你在 iOS 使用的 OpenAL 的代码模块可以轻松的移植到其他平台。

更多关于 OpenAL 的信息，包括如何使用它，见 [*www.openal.org*](http://www.openal.org/)。

##OpenGL ES Framework
OpenGL ES framework (OpenGLES.framework) 提供了绘制 2D 和 3D 内容的工具。它是与设备硬件紧密合作提供细精度图形控制和为全屏幕融入式 app 如游戏提供高帧率的基于 C 语言的框架。你可以使用 OpenGL framework 与 EAGL 接口结合，它在 OpenGL ES 绘制调用和 UIKit 的原生窗口对象之间提供接口。

这个框架支持 OpenGL ES 1.1，2.0 和 3.0。2.0 规范添加了 fragment 和 vertext  shaders，3.0 规范添加了许多功能，包括多重渲染目标和变换反馈。

更多关于如何在 apps 中使用 OpenGL ES，见 [*OpenGL ES Programming Guide for iOS*](https://developer.apple.com/library/prerelease/ios/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008793)。

更多关于参考信息，见 [*OpenGL ES Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/OpenGLES/Reference/OpenGLES_Framework/index.html#//apple_ref/doc/uid/TP40007628)。

##Photos Framework
Photo framework (*Photos.framework*) 提供与图片和视频资源工作的新的 API，包括 iCloud 图片资源，它通过 Phptos app 管理。此框架是 Assets Library 框架更有力的替代。关键的功能包括为了读取的和缓存缩略图和完整尺寸资源的线程安全架构，需要修改资源，观察其他 app 所做的修改，和可恢复的编辑中的资源内容。

更多关于这个框架的接口信息，见 [*Photos Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/Photos/Reference/Photos_Framework/index.html#//apple_ref/doc/uid/TP40014408)。

##Photos UI Framework
Photos UI framework (*PhotosUI.framework*) 让你创建在 Photos app 内编辑图片和视频资源的 app 拓展。

更多关于如何创建图片编辑拓展，见 [*App Extension Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/ExtensibilityPG/index.html#//apple_ref/doc/uid/TP40014214)。

##Quartz Core Framework
Quartz Core framework (*QuartzCore.framework*) 包含 Core Animation 接口。Core Animation 是一个先进的合成技术使它轻松的快速和效率的创建基于视图的动画。合成引擎利用了底层硬件的优势高效的和实时的操纵你的视图的内容。指定动画的开始和结束点，然后让 Core Animation 完成剩下的工作。因为 Core Animation 是内置到底层的 UIView 架构，所以它总是可用的。

更多关于如何在你的 app 中使用 Core Animation 的信息，见 [*Core Animation Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004514) 和 [*Core Animation Reference Collection*](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/CoreAnimation_framework/index.html#//apple_ref/doc/uid/TP40004513)。

##SceneKit Framework
SceneKit 是一个为构建简单的游戏和丰富的 3D 图形的 app 用户界面，结合高性能的渲染引擎，和描述性 API 的 Objective-C 框架。SceneKit 在 OS X v10.8  开始可用和在 iOS 可用。低级别 API (例如 OpenGL ES) 需要你实现显示精确的细节的场景的渲染算法。相比之下，SceneKit 让你描述你的场景内容的项 - 几何形状，材质，光源和照相机，然后描述改变这些对象使它动画。

SceneKit 的 3D 物理引擎通过模拟重力，力量，刚体碰撞，和关节使你的 app 或 game 变得生动。高级别特性使得它轻松的在场景中使用轮式车辆例如汽车和加入应用迳向重力，电磁，或震荡的对象的物理字段到一个影响的范围内。

使用 OpenGL ES 呈现更多的内容到一个场景中，或者提供 GLSL 着色器的替换或增强 SceneKit 的渲染。你也可以增加基于着色器的后置处理技术到 SceneKit 渲染，例如颜色分级或屏幕空间环境光遮蔽。

更多关于这个框架的接口的信息，见 [*SceneKit Framework Reference*](https://developer.apple.com/library/prerelease/ios/documentation/SceneKit/Reference/SceneKit_Framework/index.html#//apple_ref/doc/uid/TP40012283)。

##SpriteKit Framework
SpriteKit framework (SpriteKit.framework) 为 2D 或 2.5D 游戏提供了硬件加速动画系统。SpriteKit 提供了大多游戏需要的基础架构，包含图像渲染和动画系统，声音播放支持，和物理模拟引擎。使用 SpriteKit 你可以自己自由的创建这些事情和让你专注于内容的设计和为内容带来高层次交互。

内容在 SpriteKit app 中被组织到场景中。一个场景可以包含贴图对象，视频，基于路径的形状，核心图像过滤器，和其他指定的效果。SpriteKit 获取这些对象，并决定最有效的方式将他们渲染到一个屏幕上。当它在你的场景的内容中动画时，你可以使用 SpriteKit 明确的指定你想要执行的动作或使用物理引擎为你的对象定义一些物理行为 (例如重量，引力，或推斥)。

除了 SpriteKit 框架外，Xcode 工具也可以创建粒子发射特效和选择纹理。你可以使用 Xcode 工具管理 app 资源和快速更新 SpriteKit 场景。

更多关于如何使用 SpriteKit 的信息，见 [*SpriteKit Programming Guide*](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsAnimation/Conceptual/SpriteKit_PG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40013043)。

更多关于如何使用 SpriteKit 构建 app，见 [*code:Explanied Adventure*](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsAnimation/Conceptual/CodeExplainedAdventure/AdventureArchitecture/AdventureArchitecture.html#//apple_ref/doc/uid/TP40013140)。

#**系列文章**
[*iOS 笔记《About the iOS Technologies：Cocoa Touch Layer》*](../iOS-Note-About-the-iOS-Technologies-Cocoa-Touch-Layer)
*iOS 笔记《About the iOS Technologies：Media Layer》*
[*iOS 笔记《About the iOS Technologies：Core Service Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-Service-Layer)
[*iOS 笔记《About the iOS Technologies：Core OS Layer》*](../iOS-Note-About-the-iOS-Technologies-Core-OS-Layer) 



---------

[1]: https://developer.apple.com/library/prerelease/ios/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007898-CH1-SW1