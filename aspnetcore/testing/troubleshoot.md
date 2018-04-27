---
title: 有关 ASP.NET 核心故障排除
author: Rick-Anderson
description: 了解和解决警告和错误与 ASP.NET 核心项目。
manager: wpickett
ms.author: riande
ms.date: 04/05/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: testing/troubleshoot
ms.openlocfilehash: a75dc666621600e1e2fe36c29acbe7484bae9229
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="troubleshoot-aspnet-core-projects"></a>解决 ASP.NET 核心项目

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

以下链接提供了故障排除指导：

* [对 Azure 应用服务上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/azure-apps/troubleshoot)
* [对 IIS 上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/iis/troubleshoot)
* [Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)
* [YouTube： 诊断 ASP.NET 核心应用程序中的问题](https://www.youtube.com/watch?v=RYI0DHoIVaA)

<a name="sdk"></a>
## <a name="net-core-sdk-warnings"></a>.NET 核心 SDK 警告

### <a name="both-the-32-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a>安装这两个 32 和 64 位版本的.NET 核心 SDK
在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告出现在的顶部： 

    Both 32 and 64 bit versions of the .NET Core SDK are installed. Only templates from the 64 bit version(s) installed at C:\Program Files\dotnet\sdk\" will be displayed.

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/both32and64bit.png)

时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET 核心 SDK](https://www.microsoft.com/net/download/all)安装。 可以安装两个版本的常见原因包括：

* 你最初下载.NET 核心 SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。 
* 由另一个应用程序安装了 32 位.NET 核心 SDK。
* 下载并安装了错误版本。

卸载 32 位.NET 核心 SDK，以防止出现此警告。 从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。 如果你了解为何会出现的警告和它的含义，你可以忽略该警告。

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a>.NET 核心 SDK 的安装在多个位置
在**新项目**ASP.NET Core 可能会看到以下警告顶部显示的对话框： 

 .NET 核心 SDK 安装在多个位置中。 从安装在 SDK(s) 的模板 C:\Program Files\dotnet\sdk\'将显示。

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/multiplelocations.png)

你看到此消息因为之外的一个目录中有至少一个安装的.NET 核心 SDK * C:\Program Files\dotnet\sdk\*。 通常，这发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET 核心 SDK 时。

卸载 32 位.NET 核心 SDK，以防止出现此警告。 从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。 如果你了解为何会出现的警告和它的含义，你可以忽略该警告。
