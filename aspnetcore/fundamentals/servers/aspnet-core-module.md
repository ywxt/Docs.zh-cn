---
title: ASP.NET Core 模块
author: guardrex
description: 了解 ASP.NET Core 模块如何使 Kestrel Web 服务器可以使用 IIS 或 IIS Express。
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/30/2018
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: d3f3a42dd7aebc425905b865376a584bcf0e5153
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861454"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="4f89f-103">ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="4f89f-103">ASP.NET Core Module</span></span>

<span data-ttu-id="4f89f-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Rick Strahl](https://github.com/RickStrahl) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="4f89f-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="4f89f-105">ASP.NET Core 模块允许 ASP.NET Core 应用在 IIS 工作进程中运行（进程内）或在采用反向代理配置的 IIS 后运行（进程外）。</span><span class="sxs-lookup"><span data-stu-id="4f89f-105">The ASP.NET Core Module allows ASP.NET Core apps to run in an IIS worker process (*in-process*) or behind IIS in a reverse proxy configuration (*out-of-process*).</span></span> <span data-ttu-id="4f89f-106">IIS 具有高级 Web 应用安全性和易管理性。</span><span class="sxs-lookup"><span data-stu-id="4f89f-106">IIS provides advanced web app security and manageability features.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="4f89f-107">ASP.NET Core 模块允许 ASP.NET Core 应用在采用反向代理配置的 IIS 后运行。</span><span class="sxs-lookup"><span data-stu-id="4f89f-107">The ASP.NET Core Module allows ASP.NET Core apps to run behind IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="4f89f-108">IIS 具有高级 Web 应用安全性和易管理性。</span><span class="sxs-lookup"><span data-stu-id="4f89f-108">IIS provides advanced web app security and manageability features.</span></span>

::: moniker-end

<span data-ttu-id="4f89f-109">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="4f89f-109">Supported Windows versions:</span></span>

* <span data-ttu-id="4f89f-110">Windows 7 或更高版本</span><span class="sxs-lookup"><span data-stu-id="4f89f-110">Windows 7 or later</span></span>
* <span data-ttu-id="4f89f-111">Windows Server 2008 R2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="4f89f-111">Windows Server 2008 R2 or later</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="4f89f-112">正在进行托管时，该模块会使用 IIS 进程内服务器实现，即 IIS HTTP 服务器 (`IISHttpServer`)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-112">When hosting in-process, the module uses an IIS in-process server implementation, IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="4f89f-113">在进程外托管时，该模块仅适用于 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-113">When hosting out-of-process, the module only works with Kestrel.</span></span> <span data-ttu-id="4f89f-114">该模块与 [HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）不兼容。</span><span class="sxs-lookup"><span data-stu-id="4f89f-114">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="4f89f-115">该模块仅适用于 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-115">The module only works with Kestrel.</span></span> <span data-ttu-id="4f89f-116">该模块与 [HTTP.sys](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）不兼容。</span><span class="sxs-lookup"><span data-stu-id="4f89f-116">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

::: moniker-end

## <a name="aspnet-core-module-description"></a><span data-ttu-id="4f89f-117">ASP.NET Core 模块说明</span><span class="sxs-lookup"><span data-stu-id="4f89f-117">ASP.NET Core Module description</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="4f89f-118">ASP.NET Core 模块是插入 IIS 管道的本机 IIS 模块，用于：</span><span class="sxs-lookup"><span data-stu-id="4f89f-118">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to either:</span></span>

* <span data-ttu-id="4f89f-119">在 IIS 工作进程 (`w3wp.exe`) 内托管 ASP.NET Core 应用，称为[进程内托管模型](#in-process-hosting-model)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-119">Host an ASP.NET Core app inside of the IIS worker process (`w3wp.exe`), called the [in-process hosting model](#in-process-hosting-model).</span></span>

* <span data-ttu-id="4f89f-120">将 Web 请求转发到运行 [Kestrel 服务器](xref:fundamentals/servers/kestrel)的后端 ASP.NET Core 应用，称为[进程外托管模型](#out-of-process-hosting-model)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-120">Forward web requests to a backend ASP.NET Core app running the [Kestrel server](xref:fundamentals/servers/kestrel), called the [out-of-process hosting model](#out-of-process-hosting-model).</span></span>

### <a name="in-process-hosting-model"></a><span data-ttu-id="4f89f-121">进程内托管模型</span><span class="sxs-lookup"><span data-stu-id="4f89f-121">In-process hosting model</span></span>

<span data-ttu-id="4f89f-122">使用进程内托管，ASP.NET Core 在与其 IIS 工作进程相同的进程中运行。</span><span class="sxs-lookup"><span data-stu-id="4f89f-122">Using in-process hosting, an ASP.NET Core app runs in the same process as its IIS worker process.</span></span> <span data-ttu-id="4f89f-123">这样可以避免在使用进程外托管模型时通过环回适配器代理请求的性能损失。</span><span class="sxs-lookup"><span data-stu-id="4f89f-123">This removes the performance penalty of proxying requests over the loopback adapter when using the out-of-process hosting model.</span></span> <span data-ttu-id="4f89f-124">IIS 使用 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 处理进程管理。</span><span class="sxs-lookup"><span data-stu-id="4f89f-124">IIS handles process management with the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="4f89f-125">ASP.NET Core 模块：</span><span class="sxs-lookup"><span data-stu-id="4f89f-125">The ASP.NET Core Module:</span></span>

* <span data-ttu-id="4f89f-126">执行应用初始化。</span><span class="sxs-lookup"><span data-stu-id="4f89f-126">Performs app initialization.</span></span>
  * <span data-ttu-id="4f89f-127">加载 [CoreCLR](/dotnet/standard/glossary#coreclr)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-127">Loads the [CoreCLR](/dotnet/standard/glossary#coreclr).</span></span>
  * <span data-ttu-id="4f89f-128">调用 `Program.Main`。</span><span class="sxs-lookup"><span data-stu-id="4f89f-128">Calls `Program.Main`.</span></span>
* <span data-ttu-id="4f89f-129">处理 IIS 本机请求的生存期。</span><span class="sxs-lookup"><span data-stu-id="4f89f-129">Handles the lifetime of the IIS native request.</span></span>

<span data-ttu-id="4f89f-130">下图说明了 IIS、ASP.NET Core 模块和进程内托管的应用之间的关系：</span><span class="sxs-lookup"><span data-stu-id="4f89f-130">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app hosted in-process:</span></span>

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-inprocess.png)

<span data-ttu-id="4f89f-132">请求从 Web 到达内核模式 HTTP.sys 驱动程序。</span><span class="sxs-lookup"><span data-stu-id="4f89f-132">A request arrives from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="4f89f-133">驱动程序将本机请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-133">The driver routes the native request to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="4f89f-134">该模块接收本机请求，并将它传递给 IIS HTTP 服务器 (`IISHttpServer`)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-134">The module receives the native request and passes it to IIS HTTP Server (`IISHttpServer`).</span></span> <span data-ttu-id="4f89f-135">IIS HTTP 服务器是将请求从本机转换为托管的 IIS 进程内服务器实现。</span><span class="sxs-lookup"><span data-stu-id="4f89f-135">IIS HTTP Server is an IIS in-process server implementation that converts the request from native to managed.</span></span>

<span data-ttu-id="4f89f-136">IIS HTTP 服务器处理请求之后，请求会被推送到 ASP.NET Core 中间件管道中。</span><span class="sxs-lookup"><span data-stu-id="4f89f-136">After the IIS HTTP Server processes the request, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="4f89f-137">中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="4f89f-137">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="4f89f-138">应用的响应传递回 IIS，IIS 将响应推送回发起请求的客户端。</span><span class="sxs-lookup"><span data-stu-id="4f89f-138">The app's response is passed back to IIS, which pushes it back out to the client that initiated the request.</span></span>

### <a name="out-of-process-hosting-model"></a><span data-ttu-id="4f89f-139">进程外托管模型</span><span class="sxs-lookup"><span data-stu-id="4f89f-139">Out-of-process hosting model</span></span>

<span data-ttu-id="4f89f-140">由于 ASP.NET Core 应用在独立于 IIS 工作进程的进程中运行，因此该模块会处理进程管理。</span><span class="sxs-lookup"><span data-stu-id="4f89f-140">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module handles process management.</span></span> <span data-ttu-id="4f89f-141">该模块在第一个请求到达时启动 ASP.NET Core 应用的进程，并在应用关闭或崩溃时重新启动该应用。</span><span class="sxs-lookup"><span data-stu-id="4f89f-141">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it shuts down or crashes.</span></span> <span data-ttu-id="4f89f-142">这基本上与在 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 托管的进程内运行的应用中出现的行为相同。</span><span class="sxs-lookup"><span data-stu-id="4f89f-142">This is essentially the same behavior as seen with apps that run in-process that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="4f89f-143">下图说明了 IIS、ASP.NET Core 模块和进程外托管的应用之间的关系：</span><span class="sxs-lookup"><span data-stu-id="4f89f-143">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app hosted out-of-process:</span></span>

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="4f89f-145">请求从 Web 到达内核模式 HTTP.sys 驱动程序。</span><span class="sxs-lookup"><span data-stu-id="4f89f-145">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="4f89f-146">驱动程序将请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-146">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="4f89f-147">该模块将该请求转发到应用的随机端口（非端口 80/443）上的 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-147">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="4f89f-148">该模块在启动时通过环境变量指定端口，IIS 集成中间件将服务器配置为侦听 `http://localhost:{port}`。</span><span class="sxs-lookup"><span data-stu-id="4f89f-148">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="4f89f-149">执行其他检查，拒绝不是来自该模块的请求。</span><span class="sxs-lookup"><span data-stu-id="4f89f-149">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="4f89f-150">该模块不支持 HTTPS 转发，因此即使请求由 IIS 通过 HTTPS 接收，它们还是通过 HTTP 转发。</span><span class="sxs-lookup"><span data-stu-id="4f89f-150">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="4f89f-151">Kestrel 从模块获取请求后，请求会被推送到 ASP.NET Core 中间件管道中。</span><span class="sxs-lookup"><span data-stu-id="4f89f-151">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="4f89f-152">中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="4f89f-152">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="4f89f-153">IIS 集成添加的中间件会将方案、远程 IP 和 pathbase 更新到帐户以将请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-153">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="4f89f-154">应用的响应传递回 IIS，IIS 将响应推送回发起请求的 HTTP 客户端。</span><span class="sxs-lookup"><span data-stu-id="4f89f-154">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="4f89f-155">ASP.NET Core 模块是插入 IIS 管道的本机 IIS 模块，用于将 Web 请求转发到后端 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="4f89f-155">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to forward web requests to backend ASP.NET Core apps.</span></span>

<span data-ttu-id="4f89f-156">由于 ASP.NET Core 应用在独立于 IIS 辅助进程的进程中运行，因此该模块还处理进程管理。</span><span class="sxs-lookup"><span data-stu-id="4f89f-156">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="4f89f-157">该模块在第一个请求到达时启动 ASP.NET Core 应用的进程，并在应用崩溃时重新启动该应用。</span><span class="sxs-lookup"><span data-stu-id="4f89f-157">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="4f89f-158">这基本上与在 [Windows 进程激活服务 (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was) 托管的 IIS 中在进程内运行的 ASP.NET 4.x 应用中出现的行为相同。</span><span class="sxs-lookup"><span data-stu-id="4f89f-158">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="4f89f-159">下图说明了 IIS、ASP.NET Core 模块和应用之间的关系：</span><span class="sxs-lookup"><span data-stu-id="4f89f-159">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app:</span></span>

![ASP.NET Core 模块](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="4f89f-161">请求从 Web 到达内核模式 HTTP.sys 驱动程序。</span><span class="sxs-lookup"><span data-stu-id="4f89f-161">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="4f89f-162">驱动程序将请求路由到网站的配置端口上的 IIS，通常为 80 (HTTP) 或 443 (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="4f89f-162">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="4f89f-163">该模块将该请求转发到应用的随机端口（非端口 80/443）上的 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-163">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="4f89f-164">该模块在启动时通过环境变量指定端口，IIS 集成中间件将服务器配置为侦听 `http://localhost:{port}`。</span><span class="sxs-lookup"><span data-stu-id="4f89f-164">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="4f89f-165">执行其他检查，拒绝不是来自该模块的请求。</span><span class="sxs-lookup"><span data-stu-id="4f89f-165">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="4f89f-166">该模块不支持 HTTPS 转发，因此即使请求由 IIS 通过 HTTPS 接收，它们还是通过 HTTP 转发。</span><span class="sxs-lookup"><span data-stu-id="4f89f-166">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="4f89f-167">Kestrel 从模块获取请求后，请求会被推送到 ASP.NET Core 中间件管道中。</span><span class="sxs-lookup"><span data-stu-id="4f89f-167">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="4f89f-168">中间件管道处理该请求并将其作为 `HttpContext` 实例传递给应用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="4f89f-168">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="4f89f-169">IIS 集成添加的中间件会将方案、远程 IP 和 pathbase 更新到帐户以将请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="4f89f-169">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="4f89f-170">应用的响应传递回 IIS，IIS 将响应推送回发起请求的 HTTP 客户端。</span><span class="sxs-lookup"><span data-stu-id="4f89f-170">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

<span data-ttu-id="4f89f-171">许多本机模块（如 Windows 身份验证）仍处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="4f89f-171">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="4f89f-172">要详细了解随该模块活动的 IIS 模块，请参阅 <xref:host-and-deploy/iis/modules>。</span><span class="sxs-lookup"><span data-stu-id="4f89f-172">To learn more about IIS modules active with the module, see <xref:host-and-deploy/iis/modules>.</span></span>

<span data-ttu-id="4f89f-173">ASP.NET Core 模块具有一些其他功能。</span><span class="sxs-lookup"><span data-stu-id="4f89f-173">The ASP.NET Core Module has a few other functions.</span></span> <span data-ttu-id="4f89f-174">该模块可以：</span><span class="sxs-lookup"><span data-stu-id="4f89f-174">The module can:</span></span>

* <span data-ttu-id="4f89f-175">为工作进程设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="4f89f-175">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="4f89f-176">将 stdout 输出记录到文件存储器，以解决启动问题。</span><span class="sxs-lookup"><span data-stu-id="4f89f-176">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="4f89f-177">转发 Windows 身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="4f89f-177">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="4f89f-178">如何安装和使用 ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="4f89f-178">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="4f89f-179">有关如何安装和使用 ASP.NET Core 模块的详细说明，请参阅 <xref:host-and-deploy/iis/index>。</span><span class="sxs-lookup"><span data-stu-id="4f89f-179">For detailed instructions on how to install and use the ASP.NET Core Module, see <xref:host-and-deploy/iis/index>.</span></span> <span data-ttu-id="4f89f-180">有关配置模块的信息，请参阅 <xref:host-and-deploy/aspnet-core-module>。</span><span class="sxs-lookup"><span data-stu-id="4f89f-180">For information on configuring the module, see the <xref:host-and-deploy/aspnet-core-module>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f89f-181">其他资源</span><span class="sxs-lookup"><span data-stu-id="4f89f-181">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* [<span data-ttu-id="4f89f-182">ASP.NET Core 模块 GitHub 存储库（源代码）</span><span class="sxs-lookup"><span data-stu-id="4f89f-182">ASP.NET Core Module GitHub repository (source code)</span></span>](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
