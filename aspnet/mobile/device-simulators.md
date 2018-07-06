---
uid: mobile/device-simulators
title: 模拟常用移动设备进行测试 |Microsoft Docs
author: rick-anderson
description: 你可以通过访问以下链接下载受欢迎的移动设备和浏览器的仿真的程序
ms.author: aspnetcontent
ms.date: 01/28/2011
ms.assetid: bfb5612e-c3ec-4f28-b43b-63d781aa2272
msc.legacyurl: /mobile/device-simulators
msc.type: content
ms.openlocfilehash: 092186a48a304c1b9e3e140e74f65dbe5a035e66
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833680"
---
<a name="simulate-popular-mobile-devices-for-testing"></a>模拟常用移动设备进行测试
====================
> 你可以通过访问以下链接下载受欢迎的移动设备和浏览器的仿真的程序


| 设备或浏览器 | 仿真器 / 模拟器 |
| --- | --- |
| BrowserStack 托管浏览器的虚拟化 ![BrowserStack 托管浏览器的虚拟化](device-simulators/_static/image1.png) | [BrowserStack 上托管的浏览器虚拟化](http://browserstack.com)在任何平台上的任何浏览器中测试您的本地或生产环境。 托管虚拟机中，可以在计算机与 BrowserStack 网络之间创建隧道。 请确保获得[BrowserStack Visual Studio 扩展](https://visualstudiogallery.msdn.microsoft.com/2dfa32b1-3c47-439d-b1c5-9e28be18b81c)更加无缝体验。 |
| Windows Phone | [Windows Phone SDK 下载](https://dev.windowsphone.com/downloadsdk)Windows Phone 软件开发工具包 (SDK) 包括所有的 Windows Phone 开发应用程序和游戏所需的工具 |
| iPhone / iPod / iPad | [Electric Plum](http://www.electricplum.com/studio.aspx) iPhone 和 iPad 模拟器为 Windows，以及响应式设计工具。 可以与 VS 2012"与浏览..."选项集成。 |
| Android | [Android SDK 主页](https://developer.android.com/sdk) |
| Opera Mobile / Opera Mini | 最新版本： [Opera 开发人员工具家庭](http://www.opera.com/developer/tools/)Opera Mini 4.2:[联机 Java 基于模拟器](http://www.opera.com/mobile/demo/?ver=4) |
| Windows Mobile 6.5.3 | [Windows Mobile 6.5.3 Developer Tool Kit](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=c0213f68-2e01-4e5c-a8b2-35e081dcf1ca&amp;displaylang=en)请注意，为了让电话网络访问，还需要包含在 VPC 网络适配器[Virtual PC 2007](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=04d26402-3199-48a3-afa2-2dc0b40a73b6&amp;DisplayLang=en)。 若要连接 IE 的手机上 Visual Studio 开发服务器，请参阅[Kiran Patil 博客文章](http://kiranpatils.wordpress.com/2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/)。 |
| Windows Mobile 6.1 | [仿真程序映像的 Visual Studio 2005/2008](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=3d6f581e-c093-4b15-ab0c-a2ce5bffdb47) |

请注意，是否您想要查看你的应用程序 （这是完全测试 iPhone 或 iPad，因为 Windows 没有 true 模拟器的唯一选项） 在真实移动设备上你将需要托管在 IIS 或 IIS Express 中的应用程序。 不能轻松地为此，使用 Visual Studio 的内置 web 服务器，因为它不会响应来自其他计算机的请求。
