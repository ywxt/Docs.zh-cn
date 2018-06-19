---
title: ASP.NET Core 模块
author: rick-anderson
description: 了解 ASP.NET Core 模块如何使 Kestrel Web 服务器将 IIS 或 IIS Express 用作反向代理服务器。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/23/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: 789b0b2e74405256bb0e247ae5ea9697e3cb28e5
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
ms.locfileid: "34153700"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="6ee33-103">ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="6ee33-103">ASP.NET Core Module</span></span>

<span data-ttu-id="6ee33-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Rick Strahl](https://github.com/RickStrahl) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="6ee33-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span> 

<span data-ttu-id="6ee33-105">ASP.NET Core 模块允许 ASP.NET Core 应用在采用反向代理配置的 IIS 后运行。</span><span class="sxs-lookup"><span data-stu-id="6ee33-105">The ASP.NET Core Module allows ASP.NET Core apps to run behind IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="6ee33-106">IIS 具有高级 Web 应用安全性和易管理性。</span><span class="sxs-lookup"><span data-stu-id="6ee33-106">IIS provides advanced web app security and manageability features.</span></span>

<span data-ttu-id="6ee33-107">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="6ee33-107">Supported Windows versions:</span></span>

* <span data-ttu-id="6ee33-108">Windows 7 或更高版本</span><span class="sxs-lookup"><span data-stu-id="6ee33-108">Windows 7 or later</span></span>
* <span data-ttu-id="6ee33-109">Windows Server 2008 R2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="6ee33-109">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="6ee33-110">ASP.NET Core 模块仅适用于 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="6ee33-110">The ASP.NET Core Module only works with Kestrel.</span></span> <span data-ttu-id="6ee33-111">该模块与 [HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）不兼容。</span><span class="sxs-lookup"><span data-stu-id="6ee33-111">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

## <a name="aspnet-core-module-description"></a><span data-ttu-id="6ee33-112">ASP.NET Core 模块说明</span><span class="sxs-lookup"><span data-stu-id="6ee33-112">ASP.NET Core Module description</span></span>

<span data-ttu-id="6ee33-113">ASP.NET Core 模块是插入 IIS 管道的本机 IIS 模块，用于将 Web 请求重定向到后端 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="6ee33-113">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to redirect web requests to backend ASP.NET Core apps.</span></span> <span data-ttu-id="6ee33-114">许多本机模块（如 Windows 身份验证）仍处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="6ee33-114">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="6ee33-115">要详细了解随该模块活动的 IIS 模块，请参阅 [IIS 模块](xref:host-and-deploy/iis/modules)。</span><span class="sxs-lookup"><span data-stu-id="6ee33-115">To learn more about IIS modules active with the module, see [IIS modules](xref:host-and-deploy/iis/modules).</span></span>

<span data-ttu-id="6ee33-116">由于 ASP.NET Core 应用在独立于 IIS 辅助进程的进程中运行，因此该模块还处理进程管理。</span><span class="sxs-lookup"><span data-stu-id="6ee33-116">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="6ee33-117">该模块在第一个请求到达时启动 ASP.NET Core 应用的进程，并在应用崩溃时重新启动该应用。</span><span class="sxs-lookup"><span data-stu-id="6ee33-117">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="6ee33-118">这基本上与在 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 托管的 IIS 中在进程内运行的 ASP.NET 4.x 应用中出现的行为相同。</span><span class="sxs-lookup"><span data-stu-id="6ee33-118">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="6ee33-119">下图说明了 IIS、ASP.NET Core 模块和 ASP.NET Core 应用之间的关系：</span><span class="sxs-lookup"><span data-stu-id="6ee33-119">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and ASP.NET Core apps:</span></span>

![ASP.NET Core 模块](aspnet-core-module/_static/ancm.png)

<span data-ttu-id="6ee33-121">请求从 Web 到达内核模式 HTTP.sys 驱动程序。</span><span class="sxs-lookup"><span data-stu-id="6ee33-121">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="6ee33-122">驱动程序将请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="6ee33-122">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="6ee33-123">该模块将该请求转发到应用的随机端口（非端口 80/443）上的 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="6ee33-123">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="6ee33-124">该模块在启动时通过环境变量指定端口，IIS 集成中间件将服务器配置为侦听 `http://localhost:{port}`。</span><span class="sxs-lookup"><span data-stu-id="6ee33-124">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="6ee33-125">执行其他检查，拒绝不是来自该模块的请求。</span><span class="sxs-lookup"><span data-stu-id="6ee33-125">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="6ee33-126">该模块不支持 HTTPS 转发，因此即使请求由 IIS 通过 HTTPS 接收，它们还是通过 HTTP 转发。</span><span class="sxs-lookup"><span data-stu-id="6ee33-126">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="6ee33-127">Kestrel 从模块获取请求后，请求会被推送到 ASP.NET Core 中间件管道中。</span><span class="sxs-lookup"><span data-stu-id="6ee33-127">After Kestrel picks up a request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="6ee33-128">中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="6ee33-128">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="6ee33-129">应用的响应传递回 IIS，IIS 将响应推送回发起请求的 HTTP 客户端。</span><span class="sxs-lookup"><span data-stu-id="6ee33-129">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

<span data-ttu-id="6ee33-130">ASP.NET Core 模块具有一些其他功能。</span><span class="sxs-lookup"><span data-stu-id="6ee33-130">The ASP.NET Core Module has a few other functions.</span></span> <span data-ttu-id="6ee33-131">该模块可以：</span><span class="sxs-lookup"><span data-stu-id="6ee33-131">The module can:</span></span>

* <span data-ttu-id="6ee33-132">为工作进程设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="6ee33-132">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="6ee33-133">将 stdout 输出记录到文件存储器，以解决启动问题。</span><span class="sxs-lookup"><span data-stu-id="6ee33-133">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="6ee33-134">转发 Windows 身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="6ee33-134">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="6ee33-135">如何安装和使用 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="6ee33-135">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="6ee33-136">有关如何安装和使用 ASP.NET Core 模块的详细说明，请参阅[使用 IIS 在 Windows 上进行托管](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="6ee33-136">For detailed instructions on how to install and use the ASP.NET Core Module, see [Host on Windows with IIS](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="6ee33-137">有关配置模块的信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="6ee33-137">For information on configuring the module, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ee33-138">其他资源</span><span class="sxs-lookup"><span data-stu-id="6ee33-138">Additional resources</span></span>

* [<span data-ttu-id="6ee33-139">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="6ee33-139">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="6ee33-140">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="6ee33-140">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="6ee33-141">ASP.NET Core 模块 GitHub 存储库（源代码）</span><span class="sxs-lookup"><span data-stu-id="6ee33-141">ASP.NET Core Module GitHub repository (source code)</span></span>](https://github.com/aspnet/AspNetCoreModule)
