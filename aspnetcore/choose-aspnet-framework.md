---
title: 在 ASP.NET 和 ASP.NET Core 之间进行选择
author: rick-anderson
description: 了解如何在 ASP.NET 和 ASP.NET Core 之间进行选择。
manager: wpickett
ms.author: riande
ms.date: 03/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: e6ac9f54ef623895b81eea33d90791e5f0ad5120
ms.sourcegitcommit: 71b93b42cbce8a9b1a12c4d88391e75a4dfb6162
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="choose-between-aspnet-and-aspnet-core"></a><span data-ttu-id="64bfd-103">在 ASP.NET 和 ASP.NET Core 之间进行选择</span><span class="sxs-lookup"><span data-stu-id="64bfd-103">Choose between ASP.NET and ASP.NET Core</span></span>

<span data-ttu-id="64bfd-104">不论创建怎样的 Web 应用，ASP.NET 都可提供解决方案：从面向 Windows Server 的企业 Web 应用到面向 Linux 容器的小微服务，以及中间的所有应用。</span><span class="sxs-lookup"><span data-stu-id="64bfd-104">No matter the web app you're creating, ASP.NET has a solution for you: from enterprise web apps targeting Windows Server, to small microservices targeting Linux containers, and everything in between.</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="64bfd-105">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="64bfd-105">ASP.NET Core</span></span>

<span data-ttu-id="64bfd-106">ASP.NET Core 是一个跨平台的开源框架，用于在 Windows、macOS 或 Linux 上生成基于云的新式 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="64bfd-106">ASP.NET Core is an open-source, cross-platform framework for building modern, cloud-based web apps on Windows, macOS, or Linux.</span></span>

## <a name="aspnet"></a><span data-ttu-id="64bfd-107">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="64bfd-107">ASP.NET</span></span>

<span data-ttu-id="64bfd-108">ASP.NET 是一个成熟的框架，提供在 Windows 上生成基于服务器的企业级 Web 应用所需的所有服务。</span><span class="sxs-lookup"><span data-stu-id="64bfd-108">ASP.NET is a mature framework that provides all the services needed to build enterprise-class, server-based web apps on Windows.</span></span>

## <a name="which-one-is-right-for-me"></a><span data-ttu-id="64bfd-109">哪一个适合我？</span><span class="sxs-lookup"><span data-stu-id="64bfd-109">Which one is right for me?</span></span>

| <span data-ttu-id="64bfd-110">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="64bfd-110">ASP.NET Core</span></span> | <span data-ttu-id="64bfd-111">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="64bfd-111">ASP.NET</span></span> |
|---|---|
|<span data-ttu-id="64bfd-112">针对 Windows、macOS 或 Linux 进行生成</span><span class="sxs-lookup"><span data-stu-id="64bfd-112">Build for Windows, macOS, or Linux</span></span>|<span data-ttu-id="64bfd-113">针对 Windows 进行生成</span><span class="sxs-lookup"><span data-stu-id="64bfd-113">Build for Windows</span></span>|
|<span data-ttu-id="64bfd-114">[Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="64bfd-114">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span> <span data-ttu-id="64bfd-115">另请参阅 [MVC](xref:mvc/overview)[Web API](xref:tutorials/first-web-api) 和 [SignalR](xref:signalr/introduction)。</span><span class="sxs-lookup"><span data-stu-id="64bfd-115">See also [MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api), and [SignalR](xref:signalr/introduction).</span></span>|<span data-ttu-id="64bfd-116">使用 [Web 窗体](/aspnet/web-forms)、[SignalR](/aspnet/signalr)、[MVC](/aspnet/mvc)、[Web API](/aspnet/web-api/) 或[网页](/aspnet/web-pages)</span><span class="sxs-lookup"><span data-stu-id="64bfd-116">Use [Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/), or [Web Pages](/aspnet/web-pages)</span></span>|
|<span data-ttu-id="64bfd-117">每个计算机多个版本</span><span class="sxs-lookup"><span data-stu-id="64bfd-117">Multiple versions per machine</span></span>|<span data-ttu-id="64bfd-118">每个计算机一个版本</span><span class="sxs-lookup"><span data-stu-id="64bfd-118">One version per machine</span></span>|
|<span data-ttu-id="64bfd-119">使用 C# 或 F# 通过 Visual Studio、[Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/) 或 [Visual Studio Code](https://code.visualstudio.com/) 进行开发</span><span class="sxs-lookup"><span data-stu-id="64bfd-119">Develop with Visual Studio, [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/), or [Visual Studio Code](https://code.visualstudio.com/) using C# or F#</span></span>|<span data-ttu-id="64bfd-120">使用 C#、VB 或 F# 通过 Visual Studio 进行开发</span><span class="sxs-lookup"><span data-stu-id="64bfd-120">Develop with Visual Studio using C#, VB, or F#</span></span>|
|<span data-ttu-id="64bfd-121">比 ASP.NET 性能更高</span><span class="sxs-lookup"><span data-stu-id="64bfd-121">Higher performance than ASP.NET</span></span>|<span data-ttu-id="64bfd-122">良好的性能</span><span class="sxs-lookup"><span data-stu-id="64bfd-122">Good performance</span></span>|
|[<span data-ttu-id="64bfd-123">选择 .NET Framework 或 .NET Core 运行时</span><span class="sxs-lookup"><span data-stu-id="64bfd-123">Choose .NET Framework or .NET Core runtime</span></span>](/dotnet/articles/standard/choosing-core-framework-server)|<span data-ttu-id="64bfd-124">使用 .NET Framework 运行时</span><span class="sxs-lookup"><span data-stu-id="64bfd-124">Use .NET Framework runtime</span></span>|

## <a name="aspnet-core-scenarios"></a><span data-ttu-id="64bfd-125">ASP.NET Core 方案</span><span class="sxs-lookup"><span data-stu-id="64bfd-125">ASP.NET Core scenarios</span></span>

<!-- update link to Razor Pages mvc movie series when done -->
* <span data-ttu-id="64bfd-126">[Razor 页面](xref:mvc/razor-pages/index) 是在 ASP.NET Core 2.x 及更高版本中创建 Web UI 时建议使用的方法。</span><span class="sxs-lookup"><span data-stu-id="64bfd-126">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span>
* [<span data-ttu-id="64bfd-127">网站</span><span class="sxs-lookup"><span data-stu-id="64bfd-127">Websites</span></span>](xref:tutorials/first-mvc-app/index)
* [<span data-ttu-id="64bfd-128">API</span><span class="sxs-lookup"><span data-stu-id="64bfd-128">APIs</span></span>](xref:tutorials/first-web-api)
* [<span data-ttu-id="64bfd-129">实时</span><span class="sxs-lookup"><span data-stu-id="64bfd-129">Real-time</span></span>](xref:signalr/index)

## <a name="aspnet-scenarios"></a><span data-ttu-id="64bfd-130">ASP.NET 方案</span><span class="sxs-lookup"><span data-stu-id="64bfd-130">ASP.NET scenarios</span></span>

* [<span data-ttu-id="64bfd-131">网站</span><span class="sxs-lookup"><span data-stu-id="64bfd-131">Websites</span></span>](/aspnet/mvc)
* [<span data-ttu-id="64bfd-132">API</span><span class="sxs-lookup"><span data-stu-id="64bfd-132">APIs</span></span>](/aspnet/web-api)
* [<span data-ttu-id="64bfd-133">实时</span><span class="sxs-lookup"><span data-stu-id="64bfd-133">Real-time</span></span>](/aspnet/signalr)

## <a name="resources"></a><span data-ttu-id="64bfd-134">资源</span><span class="sxs-lookup"><span data-stu-id="64bfd-134">Resources</span></span>

* [<span data-ttu-id="64bfd-135">ASP.NET 简介</span><span class="sxs-lookup"><span data-stu-id="64bfd-135">Introduction to ASP.NET</span></span>](/aspnet/overview)
* [<span data-ttu-id="64bfd-136">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="64bfd-136">Introduction to ASP.NET Core</span></span>](xref:index)
