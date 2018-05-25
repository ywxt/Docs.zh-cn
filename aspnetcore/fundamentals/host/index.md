---
title: 在 ASP.NET Core 中托管
author: guardrex
description: 了解有关 ASP.NET Core Web 主机和 .NET 通用主机的信息，它们负责应用启动和生存期管理。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/index
ms.openlocfilehash: 7ad059e39866f59040c12b7ac15e9fa3405a9aad
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="host-in-aspnet-core"></a><span data-ttu-id="597ba-103">在 ASP.NET Core 中托管</span><span class="sxs-lookup"><span data-stu-id="597ba-103">Host in ASP.NET Core</span></span>

<span data-ttu-id="597ba-104">.NET 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="597ba-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="597ba-105">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="597ba-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="597ba-106">两个主机 API 可供使用：</span><span class="sxs-lookup"><span data-stu-id="597ba-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="597ba-107">[Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="597ba-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="597ba-108">[通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。</span><span class="sxs-lookup"><span data-stu-id="597ba-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="597ba-109">在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="597ba-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="597ba-110">通用主机最终将取代 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="597ba-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="597ba-111">目前，开发人员应基于 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 使用 [Web 主机](xref:fundamentals/host/web-host)，来托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="597ba-111">At this time, developers should use the [Web Host](xref:fundamentals/host/web-host) based on [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) for hosting ASP.NET Core apps.</span></span>
