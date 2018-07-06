---
title: 解决 ASP.NET Core 项目
author: Rick-Anderson
description: 理解 ASP.NET Core 项目的警告和错误，并对其进行故障排除。
ms.author: riande
ms.date: 04/05/2018
uid: test/troubleshoot
ms.openlocfilehash: ae4e6f191d8f856de60ecf21cb882b5ee9b02064
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274588"
---
# <a name="troubleshoot-aspnet-core-projects"></a>解决 ASP.NET Core 项目

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

以下链接提供了故障排除指导：

* [对 Azure 应用服务上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/azure-apps/troubleshoot)
* [对 IIS 上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/iis/troubleshoot)
* [Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 应用程序中 （ndc） 会议 （伦敦，2018年）： 诊断问题](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [ASP.NET 博客： 解决 ASP.NET Core 性能问题](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a>.NET Core SDK 警告

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a>安装的 32 位和 64 位版本的.NET Core SDK

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> 安装了.NET Core SDK 32 和 64 位版本。 仅从安装在 64 位版本的模板 c:\\Program Files\\dotnet\\sdk\\将显示。

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/both32and64bit.png)

时，此警告会出现 (x86) 32 位和 64 位 (x64) 版本的[.NET Core SDK](https://www.microsoft.com/net/download/all)安装。 可能安装这两个版本的常见原因包括：

* 你最初下载.NET Core SDK 安装程序使用 32 位计算机，但然后复制它跨并安装在 64 位计算机上。
* 由另一个应用程序安装了 32 位.NET Core SDK。
* 下载并安装了错误版本。

卸载 32 位.NET Core SDK，以防止出现此警告。 从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。 如果你了解为何会出现的警告和它的含义，你可以忽略该警告。

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a>.NET Core SDK 的安装在多个位置

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> .NET Core SDK 安装在多个位置中。 仅从安装在 SDK(s) 的模板 c:\\Program Files\\dotnet\\sdk\\将显示。

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/multiplelocations.png)

外部的一个目录中有至少一个安装的.NET Core SDK 时，将显示此消息*c:\\Program Files\\dotnet\\sdk\\*。 这通常发生在使用复制/粘贴，而不 MSI 安装程序的计算机上部署了.NET Core SDK 时。

卸载 32 位.NET Core SDK，以防止出现此警告。 从卸载**控制面板** > **程序和功能** > **卸载或更改程序**。 如果你了解为何会出现的警告和它的含义，你可以忽略该警告。

### <a name="no-net-core-sdks-were-detected"></a>检测到没有.NET Core Sdk

在**新项目**对话框为 ASP.NET Core，你可能会看到以下警告：

> 检测到没有.NET Core Sdk，请确保将它们包括在环境变量 PATH。

![显示警告消息 OneASP.NET 对话框的屏幕快照](troubleshoot/_static/NoNetCore.png)

时，此警告会出现的环境变量`PATH`没有指向计算机上任何.NET Core Sdk。 若要解决此问题：

* 安装或验证.NET Core SDK 的安装。
* 验证`PATH`环境变量指向 SDK 的安装位置。 安装程序通常设置`PATH`。

::: moniker range=">= aspnetcore-2.1"

### <a name="use-of-ihtmlhelperpartial-may-result-in-app-deadlocks"></a>利用 IHtmlHelper.Partial 可能会导致应用程序死锁

在 ASP.NET Core 2.1 及更高版本，则调用`Html.Partial`导致死锁的可能性由于分析器警告。 警告消息为：

> 利用 IHtmlHelper.Partial 可能会导致应用程序死锁。 请考虑使用`<partial>`标记帮助器或`IHtmlHelper.PartialAsync`。

调用`@Html.Partial`应替换为`@await Html.PartialAsync`或部分标记帮助器`<partial name="_Partial" />`。

::: moniker-end
