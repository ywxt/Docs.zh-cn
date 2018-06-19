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
ms.locfileid: "34094430"
---
# <a name="choose-between-aspnet-and-aspnet-core"></a><span data-ttu-id="18955-103">在 ASP.NET 和 ASP.NET Core 之间进行选择</span><span class="sxs-lookup"><span data-stu-id="18955-103">Choose between ASP.NET and ASP.NET Core</span></span>

<span data-ttu-id="18955-104">不论创建怎样的 Web 应用，ASP.NET 都可提供解决方案：从面向 Windows Server 的企业 Web 应用到面向 Linux 容器的小微服务，以及中间的所有应用。</span><span class="sxs-lookup"><span data-stu-id="18955-104">No matter the web app you're creating, ASP.NET has a solution for you: from enterprise web apps targeting Windows Server, to small microservices targeting Linux containers, and everything in between.</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="18955-105">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="18955-105">ASP.NET Core</span></span>

<span data-ttu-id="18955-106">ASP.NET Core 是一个跨平台的开源框架，用于在 Windows、macOS 或 Linux 上生成基于云的新式 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="18955-106">ASP.NET Core is an open-source, cross-platform framework for building modern, cloud-based web apps on Windows, macOS, or Linux.</span></span>

## <a name="aspnet"></a><span data-ttu-id="18955-107">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="18955-107">ASP.NET</span></span>

<span data-ttu-id="18955-108">ASP.NET 是一个成熟的框架，提供在 Windows 上生成基于服务器的企业级 Web 应用所需的所有服务。</span><span class="sxs-lookup"><span data-stu-id="18955-108">ASP.NET is a mature framework that provides all the services needed to build enterprise-grade, server-based web apps on Windows.</span></span>

## <a name="framework-selection"></a><span data-ttu-id="18955-109">框架选择</span><span class="sxs-lookup"><span data-stu-id="18955-109">Framework selection</span></span>

<span data-ttu-id="18955-110">查看下表，确定最适合需求的框架。</span><span class="sxs-lookup"><span data-stu-id="18955-110">Review the table below to determine which framework is most appropriate for your needs.</span></span>

| <span data-ttu-id="18955-111">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="18955-111">ASP.NET Core</span></span> | <span data-ttu-id="18955-112">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="18955-112">ASP.NET</span></span> |
|---|---|
|<span data-ttu-id="18955-113">针对 Windows、macOS 或 Linux 进行生成</span><span class="sxs-lookup"><span data-stu-id="18955-113">Build for Windows, macOS, or Linux</span></span>|<span data-ttu-id="18955-114">针对 Windows 进行生成</span><span class="sxs-lookup"><span data-stu-id="18955-114">Build for Windows</span></span>|
|<span data-ttu-id="18955-115">[Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="18955-115">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span> <span data-ttu-id="18955-116">另请参阅 [MVC](xref:mvc/overview)[Web API](xref:tutorials/first-web-api) 和 [SignalR](xref:signalr/introduction)。</span><span class="sxs-lookup"><span data-stu-id="18955-116">See also [MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api), and [SignalR](xref:signalr/introduction).</span></span>|<span data-ttu-id="18955-117">使用 [Web 窗体](/aspnet/web-forms)、[SignalR](/aspnet/signalr)、[MVC](/aspnet/mvc)、[Web API](/aspnet/web-api/)、[WebHooks](/aspnet/webhooks/) 或[网页](/aspnet/web-pages)</span><span class="sxs-lookup"><span data-stu-id="18955-117">Use [Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/), [WebHooks](/aspnet/webhooks/), or [Web Pages](/aspnet/web-pages)</span></span>|
|<span data-ttu-id="18955-118">每个计算机多个版本</span><span class="sxs-lookup"><span data-stu-id="18955-118">Multiple versions per machine</span></span>|<span data-ttu-id="18955-119">每个计算机一个版本</span><span class="sxs-lookup"><span data-stu-id="18955-119">One version per machine</span></span>|
|<span data-ttu-id="18955-120">使用 C# 或 F# 通过 Visual Studio、[Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/) 或 [Visual Studio Code](https://code.visualstudio.com/) 进行开发</span><span class="sxs-lookup"><span data-stu-id="18955-120">Develop with Visual Studio, [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/), or [Visual Studio Code](https://code.visualstudio.com/) using C# or F#</span></span>|<span data-ttu-id="18955-121">使用 C#、VB 或 F# 通过 Visual Studio 进行开发</span><span class="sxs-lookup"><span data-stu-id="18955-121">Develop with Visual Studio using C#, VB, or F#</span></span>|
|<span data-ttu-id="18955-122">比 ASP.NET 性能更高</span><span class="sxs-lookup"><span data-stu-id="18955-122">Higher performance than ASP.NET</span></span>|<span data-ttu-id="18955-123">良好的性能</span><span class="sxs-lookup"><span data-stu-id="18955-123">Good performance</span></span>|
|[<span data-ttu-id="18955-124">选择 .NET Framework 或 .NET Core 运行时</span><span class="sxs-lookup"><span data-stu-id="18955-124">Choose .NET Framework or .NET Core runtime</span></span>](/dotnet/articles/standard/choosing-core-framework-server)|<span data-ttu-id="18955-125">使用 .NET Framework 运行时</span><span class="sxs-lookup"><span data-stu-id="18955-125">Use .NET Framework runtime</span></span>|

## <a name="aspnet-core-scenarios"></a><span data-ttu-id="18955-126">ASP.NET Core 方案</span><span class="sxs-lookup"><span data-stu-id="18955-126">ASP.NET Core scenarios</span></span>

* <span data-ttu-id="18955-127">[Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="18955-127">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span>
* [<span data-ttu-id="18955-128">网站</span><span class="sxs-lookup"><span data-stu-id="18955-128">Websites</span></span>](xref:tutorials/first-mvc-app/index)
* [<span data-ttu-id="18955-129">API</span><span class="sxs-lookup"><span data-stu-id="18955-129">APIs</span></span>](xref:tutorials/first-web-api)
* [<span data-ttu-id="18955-130">实时</span><span class="sxs-lookup"><span data-stu-id="18955-130">Real-time</span></span>](xref:signalr/index)

## <a name="aspnet-scenarios"></a><span data-ttu-id="18955-131">ASP.NET 方案</span><span class="sxs-lookup"><span data-stu-id="18955-131">ASP.NET scenarios</span></span>

* [<span data-ttu-id="18955-132">网站</span><span class="sxs-lookup"><span data-stu-id="18955-132">Websites</span></span>](/aspnet/mvc)
* [<span data-ttu-id="18955-133">API</span><span class="sxs-lookup"><span data-stu-id="18955-133">APIs</span></span>](/aspnet/web-api)
* [<span data-ttu-id="18955-134">实时</span><span class="sxs-lookup"><span data-stu-id="18955-134">Real-time</span></span>](/aspnet/signalr)

## <a name="resources"></a><span data-ttu-id="18955-135">资源</span><span class="sxs-lookup"><span data-stu-id="18955-135">Resources</span></span>

* [<span data-ttu-id="18955-136">ASP.NET 简介</span><span class="sxs-lookup"><span data-stu-id="18955-136">Introduction to ASP.NET</span></span>](/aspnet/overview)
* [<span data-ttu-id="18955-137">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="18955-137">Introduction to ASP.NET Core</span></span>](xref:index)
