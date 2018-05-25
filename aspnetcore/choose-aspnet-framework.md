---
title: 在 ASP.NET 和 ASP.NET Core 之间进行选择
author: rick-anderson
description: 了解如何在 ASP.NET 和 ASP.NET Core 之间进行选择。
manager: wpickett
ms.author: riande
ms.date: 05/11/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: 0c6924d40b7327d2032a0278c56a0b4fa41d15a1
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
# <a name="choose-between-aspnet-and-aspnet-core"></a>在 ASP.NET 和 ASP.NET Core 之间进行选择

不论创建怎样的 Web 应用，ASP.NET 都可提供解决方案：从面向 Windows Server 的企业 Web 应用到面向 Linux 容器的小微服务，以及中间的所有应用。

## <a name="aspnet-core"></a>ASP.NET Core

ASP.NET Core 是一个跨平台的开源框架，用于在 Windows、macOS 或 Linux 上生成基于云的新式 Web 应用。

## <a name="aspnet"></a>ASP.NET

ASP.NET 是一个成熟的框架，提供在 Windows 上生成基于服务器的企业级 Web 应用所需的所有服务。

## <a name="framework-selection"></a>框架选择

查看下表，确定最适合需求的框架。

| ASP.NET Core | ASP.NET |
|---|---|
|针对 Windows、macOS 或 Linux 进行生成|针对 Windows 进行生成|
|[Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。 另请参阅 [MVC](xref:mvc/overview)[Web API](xref:tutorials/first-web-api) 和 [SignalR](xref:signalr/introduction)。|使用 [Web 窗体](/aspnet/web-forms)、[SignalR](/aspnet/signalr)、[MVC](/aspnet/mvc)、[Web API](/aspnet/web-api/)、[WebHooks](/aspnet/webhooks/) 或[网页](/aspnet/web-pages)|
|每个计算机多个版本|每个计算机一个版本|
|使用 C# 或 F# 通过 Visual Studio、[Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/) 或 [Visual Studio Code](https://code.visualstudio.com/) 进行开发|使用 C#、VB 或 F# 通过 Visual Studio 进行开发|
|比 ASP.NET 性能更高|良好的性能|
|[选择 .NET Framework 或 .NET Core 运行时](/dotnet/articles/standard/choosing-core-framework-server)|使用 .NET Framework 运行时|

## <a name="aspnet-core-scenarios"></a>ASP.NET Core 方案

* [Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。
* [网站](xref:tutorials/first-mvc-app/index)
* [API](xref:tutorials/first-web-api)
* [实时](xref:signalr/index)

## <a name="aspnet-scenarios"></a>ASP.NET 方案

* [网站](/aspnet/mvc)
* [API](/aspnet/web-api)
* [实时](/aspnet/signalr)

## <a name="resources"></a>资源

* [ASP.NET 简介](/aspnet/overview)
* [ASP.NET Core 简介](xref:index)
