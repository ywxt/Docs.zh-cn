---
title: ASP.NET Core 中的 Web 主机和通用主机
author: guardrex
description: 了解有关 ASP.NET Core Web 主机和 .NET 通用主机的信息，它们负责应用启动和生存期管理。
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 08/28/2018
uid: fundamentals/host/index
ms.openlocfilehash: 43a68f67368ce37a1fb4032579c6c4e4c05d2719
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284573"
---
# <a name="web-host-and-generic-host-in-aspnet-core"></a><span data-ttu-id="98852-103">ASP.NET Core 中的 Web 主机和通用主机</span><span class="sxs-lookup"><span data-stu-id="98852-103">Web Host and Generic Host in ASP.NET Core</span></span>

<span data-ttu-id="98852-104">.NET 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="98852-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="98852-105">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="98852-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="98852-106">两个主机 API 可供使用：</span><span class="sxs-lookup"><span data-stu-id="98852-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="98852-107">[Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="98852-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="98852-108">[通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。</span><span class="sxs-lookup"><span data-stu-id="98852-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="98852-109">在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="98852-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="98852-110">通用主机最终将取代 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="98852-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="98852-111">为托管 ASP.NET Core Web 应用，开发人员应使用基于 <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder> 的 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="98852-111">For hosting ASP.NET Core *web apps*, developers should use the Web Host based on <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>.</span></span> <span data-ttu-id="98852-112">为托管非 Web 应用，开发人员应使用基于 <xref:Microsoft.Extensions.Hosting.HostBuilder> 的通用主机。</span><span class="sxs-lookup"><span data-stu-id="98852-112">For hosting *non-web apps*, developers should use the Generic Host based on <xref:Microsoft.Extensions.Hosting.HostBuilder>.</span></span>

<xref:fundamentals/host/hosted-services>  
<span data-ttu-id="98852-113">了解如何在 ASP.NET Core 中使用托管服务实现后台任务。</span><span class="sxs-lookup"><span data-stu-id="98852-113">Learn how to implement background tasks with hosted services in ASP.NET Core.</span></span>

<xref:fundamentals/configuration/platform-specific-configuration>  
<span data-ttu-id="98852-114">了解如何使用 <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> 实现从引用或未引用程序集增强 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="98852-114">Discover how to enhance an ASP.NET Core app from a referenced or unreferenced assembly using an <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> implementation.</span></span>
