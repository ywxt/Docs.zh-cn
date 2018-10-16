---
uid: mobile/device-simulators
title: 模拟常用移动设备进行测试 |Microsoft Docs
author: rick-anderson
description: 你可以通过访问以下链接下载受欢迎的移动设备和浏览器的仿真的程序
ms.author: riande
ms.date: 10/11/2018
ms.assetid: bfb5612e-c3ec-4f28-b43b-63d781aa2272
msc.legacyurl: /mobile/device-simulators
msc.type: content
ms.openlocfilehash: 8299295154d23f8fc430676b2c8ad8efc98ad185
ms.sourcegitcommit: 6e6002de467cd135a69e5518d4ba9422d693132a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348372"
---
# <a name="simulate-popular-mobile-devices-for-testing"></a>模拟常用移动设备进行测试

> 可以通过访问以下链接下载受欢迎的移动设备和浏览器的仿真的程序。

| 设备或浏览器 | 仿真器 / 模拟器 |
| --- | --- |
| BrowserStack 托管浏览器的虚拟化 ![BrowserStack 托管浏览器的虚拟化](device-simulators/_static/image1.png) | [BrowserStack 上托管的浏览器虚拟化](http://browserstack.com)在任何平台上的任何浏览器中测试您的本地或生产环境。 托管虚拟机中，可以在计算机与 BrowserStack 网络之间创建隧道。 请确保获得[BrowserStack Visual Studio 扩展](https://marketplace.visualstudio.com/items?itemName=browserstackcom.BrowserStack)更加无缝体验。 |
| iPhone / iPod / iPad | [电力移动 Studio](http://www.electricplum.com/studio.aspx) iPhone 和 iPad 模拟器为 Windows，以及响应式设计工具。 |
| Android | [Android Studio](https://developer.android.com/studio/)或[适用于 Android 的 Visual Studio 仿真程序](https://visualstudio.microsoft.com/vs/msft-android-emulator/) |
| Opera Mobile | [Opera 移动经典仿真程序](https://www.opera.com/developer/mobile-emulator) |
| Windows Mobile 6.5.3 | [Windows Mobile 6.5.3 Developer Tool Kit](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=c0213f68-2e01-4e5c-a8b2-35e081dcf1ca&amp;displaylang=en)请注意，为了让电话网络访问，还需要包含在 VPC 网络适配器[Virtual PC 2007](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=04d26402-3199-48a3-afa2-2dc0b40a73b6&amp;DisplayLang=en)。 若要连接 IE 的手机上 Visual Studio 开发服务器，请参阅[Kiran Patil 博客文章](http://kiranpatils.wordpress.com/2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/)。 |

> [!NOTE]
> 如果你想要查看你的应用程序 （这是完全测试 iPhone 或 iPad，因为 Windows 没有 true 模拟器的唯一选项） 在真实移动设备上将需要托管在 IIS 或 IIS Express 中的应用程序。 不能轻松地为此，使用 Visual Studio 的内置 web 服务器，因为它不会响应来自其他计算机的请求。