---
title: 在 ASP.NET Core 中托管
author: guardrex
description: 了解有关 ASP.NET Core Web 主机和 .NET 通用主机的信息，它们负责应用启动和生存期管理。
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/index
ms.openlocfilehash: 365c679e789c07818c6eb007f40f6aef43b82c44
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276612"
---
# <a name="host-in-aspnet-core"></a><span data-ttu-id="ea3be-103">在 ASP.NET Core 中托管</span><span class="sxs-lookup"><span data-stu-id="ea3be-103">Host in ASP.NET Core</span></span>

<span data-ttu-id="ea3be-104">.NET 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="ea3be-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="ea3be-105">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="ea3be-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="ea3be-106">两个主机 API 可供使用：</span><span class="sxs-lookup"><span data-stu-id="ea3be-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="ea3be-107">[Web 主机](xref:fundamentals/host/web-host) &ndash; 适用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ea3be-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="ea3be-108">[通用主机](xref:fundamentals/host/generic-host)（ASP.NET Core 2.1 或更高版本）&ndash; 适用于托管非 Web 应用（例如，运行后台任务的应用）。</span><span class="sxs-lookup"><span data-stu-id="ea3be-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="ea3be-109">在未来的版本中，通用主机将适用于托管任何类型的应用，包括 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ea3be-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="ea3be-110">通用主机最终将取代 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="ea3be-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="ea3be-111">为托管 ASP.NET Core *Web 应用*，开发者应使用基于 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 的 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="ea3be-111">For hosting ASP.NET Core *web apps*, developers should use the Web Host based on [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="ea3be-112">为托管*非 Web 应用*，开发者应使用基于 [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) 的通用主机。</span><span class="sxs-lookup"><span data-stu-id="ea3be-112">For hosting *non-web apps*, developers should use the Generic Host based on [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder).</span></span>
