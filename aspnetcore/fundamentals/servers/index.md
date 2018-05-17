---
title: ASP.NET Core 中的 Web 服务器实现
author: rick-anderson
description: 发现适用于 ASP.NET Core 的 Web 服务器 Kestrel 和 HTTP.sys。 了解如何选择服务器以及何时使用反向代理服务器。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/index
ms.openlocfilehash: 38af9d0206d66ac7fd2dc13a5a8245e8f66df41e
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
---
# <a name="web-server-implementations-in-aspnet-core"></a><span data-ttu-id="3548d-104">ASP.NET Core 中的 Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="3548d-104">Web server implementations in ASP.NET Core</span></span>

<span data-ttu-id="3548d-105">作者：[Tom Dykstra](https://github.com/tdykstra)、 [Steve Smith](https://ardalis.com/)、[Stephen Halter](https://twitter.com/halter73) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="3548d-105">By [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73), and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="3548d-106">ASP.NET Core 应用与进程内 HTTP 服务器实现一起运行。</span><span class="sxs-lookup"><span data-stu-id="3548d-106">An ASP.NET Core app runs with an in-process HTTP server implementation.</span></span> <span data-ttu-id="3548d-107">服务器实现侦听 HTTP 请求，并在一系列[请求功能](xref:fundamentals/request-features)被撰写到 [HttpContext](/dotnet/api/system.web.httpcontext) 时将这些请求展现到应用中。</span><span class="sxs-lookup"><span data-stu-id="3548d-107">The server implementation listens for HTTP requests and surfaces them to the app as sets of [request features](xref:fundamentals/request-features) composed into an [HttpContext](/dotnet/api/system.web.httpcontext).</span></span>

<span data-ttu-id="3548d-108">ASP.NET Core 交付两种服务器实现：</span><span class="sxs-lookup"><span data-stu-id="3548d-108">ASP.NET Core ships two server implementations:</span></span>

* <span data-ttu-id="3548d-109">[Kestrel](xref:fundamentals/servers/kestrel) 是适用于 ASP.NET Core 的默认跨平台 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="3548d-109">[Kestrel](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server for ASP.NET Core.</span></span>
* <span data-ttu-id="3548d-110">[HTTP.sys](xref:fundamentals/servers/httpsys) 是仅适用于 Windows 的 HTTP 服务器，它基于 [ 核心驱动程序和 HTTP 服务器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3548d-110">[HTTP.sys](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="3548d-111">（HTTP.sys 在 ASP.NET 1.x 中被命名为 [WebListener](xref:fundamentals/servers/weblistener)。）</span><span class="sxs-lookup"><span data-stu-id="3548d-111">(HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.)</span></span>

## <a name="kestrel"></a><span data-ttu-id="3548d-112">Kestrel</span><span class="sxs-lookup"><span data-stu-id="3548d-112">Kestrel</span></span>

<span data-ttu-id="3548d-113">Kestrel 是 ASP.NET Core 项目模板中包括的默认 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="3548d-113">Kestrel is the default web server included in ASP.NET Core project templates.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3548d-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3548d-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3548d-115">Kestrel 可以单独使用，也可以与反向代理服务器（如 IIS、Nginx 或 Apache）一起使用。</span><span class="sxs-lookup"><span data-stu-id="3548d-115">Kestrel can be used by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="3548d-116">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="3548d-116">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="3548d-119">如果仅向内部网络公开 Kestrel，可以使用任一配置（无需考虑是否使用反向代理服务器）。</span><span class="sxs-lookup"><span data-stu-id="3548d-119">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is only exposed to an internal network.</span></span>

<span data-ttu-id="3548d-120">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="3548d-120">For information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3548d-121">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3548d-121">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3548d-122">如果应用仅接受来自内部网络的请求，则可单独使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="3548d-122">If the app only accepts requests from an internal network, Kestrel can be used by itself.</span></span>

![Kestrel 直接与内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="3548d-124">如果将应用公开到 Internet，则必须将 IIS、Nginx 或 Apache 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="3548d-124">If the app is exposed to the Internet, Kestrel must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="3548d-125">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将其转发到 Kestrel，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="3548d-125">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling, as shown in the following diagram:</span></span>

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="3548d-127">为边缘部署使用反向代理的最重要的原因（从 Internet 公开到流量）是出于安全考虑。</span><span class="sxs-lookup"><span data-stu-id="3548d-127">The most important reason for using a reverse proxy for edge deployments (exposed to traffic from the Internet) is security.</span></span> <span data-ttu-id="3548d-128">Kestrel 的 1.x 版本不包含防御来自 Internet 的攻击的重要安全功能。</span><span class="sxs-lookup"><span data-stu-id="3548d-128">The 1.x versions of Kestrel don't have important security features to defend against attacks from the Internet.</span></span> <span data-ttu-id="3548d-129">这包括但不限于相应的超时、请求大小限制和并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="3548d-129">This includes, but isn't limited to, appropriate timeouts, request size limits, and concurrent connection limits.</span></span>

<span data-ttu-id="3548d-130">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="3548d-130">For information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

---

<span data-ttu-id="3548d-131">在没有 Kestrel 或[自定义服务器实现](#custom-servers)的情况下，不能使用 IIS、Nginx 和 Apache。</span><span class="sxs-lookup"><span data-stu-id="3548d-131">IIS, Nginx, and Apache can't be used without Kestrel or a [custom server implementation](#custom-servers).</span></span> <span data-ttu-id="3548d-132">ASP.NET Core 设计为在其自己的进程中运行，以实现跨平台统一操作。</span><span class="sxs-lookup"><span data-stu-id="3548d-132">ASP.NET Core was designed to run in its own process so that it can behave consistently across platforms.</span></span> <span data-ttu-id="3548d-133">IIS、Nginx 和 Apache 规定自己的启动过程和环境。</span><span class="sxs-lookup"><span data-stu-id="3548d-133">IIS, Nginx, and Apache dictate their own startup procedure and environment.</span></span> <span data-ttu-id="3548d-134">若要直接使用这些服务器技术，ASP.NET Core 必须满足每个服务器的需求。</span><span class="sxs-lookup"><span data-stu-id="3548d-134">To use these server technologies directly, ASP.NET Core would need to adapt to the requirements of each server.</span></span> <span data-ttu-id="3548d-135">使用 Kestrel 等 Web 服务器实现时，ASP.NET Core 可以控制托管在不同服务器技术上的启动过程和环境。</span><span class="sxs-lookup"><span data-stu-id="3548d-135">Using a web server implementation, such as Kestrel, ASP.NET Core has control over the startup process and environment when hosted on different server technologies.</span></span>

### <a name="iis-with-kestrel"></a><span data-ttu-id="3548d-136">IIS 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="3548d-136">IIS with Kestrel</span></span>

<span data-ttu-id="3548d-137">将 [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 或 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 用作 ASP.NET Core 的反向代理时，ASP.NET Core 应用在独立于 IIS 工作进程的某个进程中运行。</span><span class="sxs-lookup"><span data-stu-id="3548d-137">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) as a reverse proxy for ASP.NET Core, the ASP.NET Core app runs in a process separate from the IIS worker process.</span></span> <span data-ttu-id="3548d-138">在 IIS 进程中，[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)协调反向代理关系。</span><span class="sxs-lookup"><span data-stu-id="3548d-138">In the IIS process, the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) coordinates the reverse proxy relationship.</span></span> <span data-ttu-id="3548d-139">ASP.NET Core 模块的主要功能是启动 ASP.NET Core 应用，在其出现故障时重启应用，并向应用转发 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="3548d-139">The primary functions of the ASP.NET Core Module are to start the ASP.NET Core app, restart the app when it crashes, and forward HTTP traffic to the app.</span></span> <span data-ttu-id="3548d-140">有关详细信息，请参阅 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="3548d-140">For more information, see [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> 

### <a name="nginx-with-kestrel"></a><span data-ttu-id="3548d-141">Nginx 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="3548d-141">Nginx with Kestrel</span></span>

<span data-ttu-id="3548d-142">若要了解如何在 Linux 上使用 Nginx 作为 Kestrel 的反向代理服务器，请参阅[在 Linux 上使用 Nginx 进行托管](xref:host-and-deploy/linux-nginx)。</span><span class="sxs-lookup"><span data-stu-id="3548d-142">For information on how to use Nginx on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Nginx](xref:host-and-deploy/linux-nginx).</span></span>

### <a name="apache-with-kestrel"></a><span data-ttu-id="3548d-143">Apache 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="3548d-143">Apache with Kestrel</span></span>

<span data-ttu-id="3548d-144">若要了解如何在 Linux 上使用 Apache 作为 Kestrel 的反向代理服务器，请参阅[在 Linux 上使用 Apache 进行托管](xref:host-and-deploy/linux-apache)。</span><span class="sxs-lookup"><span data-stu-id="3548d-144">For information on how to use Apache on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Apache](xref:host-and-deploy/linux-apache).</span></span>

## <a name="httpsys"></a><span data-ttu-id="3548d-145">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="3548d-145">HTTP.sys</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3548d-146">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3548d-146">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3548d-147">如果 ASP.NET Core 应用在 Windows 上运行，则 HTTP.sys 是 Kestrel 的替代选项。</span><span class="sxs-lookup"><span data-stu-id="3548d-147">If ASP.NET Core apps are run on Windows, HTTP.sys is an alternative to Kestrel.</span></span> <span data-ttu-id="3548d-148">为了获得最佳性能，通常建议使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="3548d-148">Kestrel is generally recommended for best performance.</span></span> <span data-ttu-id="3548d-149">在向 Internet 公开应用且所需功能受 HTTP.sys 支持（而不是 Kestrel）的方案中，可以使用 HTTP.sys。</span><span class="sxs-lookup"><span data-stu-id="3548d-149">HTTP.sys can be used in scenarios where the app is exposed to the Internet and required features are supported by HTTP.sys but not Kestrel.</span></span> <span data-ttu-id="3548d-150">有关 HTTP.sys 功能的信息，请参阅 [HTTP.sys](xref:fundamentals/servers/httpsys)。</span><span class="sxs-lookup"><span data-stu-id="3548d-150">For information on HTTP.sys features, see [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

![HTTP.sys 直接与 Internet 进行通信](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="3548d-152">对于仅向内部网络公开的应用，HTTP.sys 同样适用。</span><span class="sxs-lookup"><span data-stu-id="3548d-152">HTTP.sys can also be used for apps that are only exposed to an internal network.</span></span> 

![HTTP.sys 直接与内部网络进行通信](httpsys/_static/httpsys-to-internal.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3548d-154">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3548d-154">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3548d-155">HTTP.sys 在 ASP.NET Core 1.x 中被命名为 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="3548d-155">HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span> <span data-ttu-id="3548d-156">对于 IIS 不可用于托管应用的方案，如果 ASP.NET Core 应用在 Windows 上运行，则 WebListener 可用作替代选项。</span><span class="sxs-lookup"><span data-stu-id="3548d-156">If ASP.NET Core apps are run on Windows, WebListener is an alternative for scenarios where IIS isn't available to host apps.</span></span>

![Weblistener 直接与 Internet 进行通信](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="3548d-158">如果所需功能受 WebListener 支持（而不是 Kestrel），则对于仅向内部网络公开的应用而言，还可以使用 WebListener 来替代 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="3548d-158">WebListener can also be used in place of Kestrel for apps that are only exposed to an internal network, if required features are supported by WebListener but not Kestrel.</span></span> <span data-ttu-id="3548d-159">有关 WebListener 功能的信息，请参阅 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="3548d-159">For information on WebListener features, see [WebListener](xref:fundamentals/servers/weblistener).</span></span>

![Weblistener 直接与内部网络进行通信](weblistener/_static/weblistener-to-internal.png)

---

## <a name="aspnet-core-server-infrastructure"></a><span data-ttu-id="3548d-161">ASP.NET Core 服务器基础结构</span><span class="sxs-lookup"><span data-stu-id="3548d-161">ASP.NET Core server infrastructure</span></span>

<span data-ttu-id="3548d-162">`Startup.Configure` 方法中提供的 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 公开了类型 [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection) 的 [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) 属性。</span><span class="sxs-lookup"><span data-stu-id="3548d-162">The [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) available in the `Startup.Configure` method exposes the [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) property of type [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection).</span></span> <span data-ttu-id="3548d-163">Kestrel 和 HTTP.sys（在 ASP.NET Core 1.x 中为 WebListener）各自仅公开单个功能，即 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)，但是不同的服务器实现可能公开其他功能。</span><span class="sxs-lookup"><span data-stu-id="3548d-163">Kestrel and HTTP.sys (WebListener in ASP.NET Core 1.x) only expose a single feature each, [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature), but different server implementations may expose additional functionality.</span></span>

<span data-ttu-id="3548d-164">`IServerAddressesFeature` 可用于查找服务器实现在运行时绑定的端口。</span><span class="sxs-lookup"><span data-stu-id="3548d-164">`IServerAddressesFeature` can be used to find out which port the server implementation has bound at runtime.</span></span>

## <a name="custom-servers"></a><span data-ttu-id="3548d-165">自定义服务器</span><span class="sxs-lookup"><span data-stu-id="3548d-165">Custom servers</span></span>

<span data-ttu-id="3548d-166">如果内置服务器无法满足应用需求，可以创建一个自定义服务器实现。</span><span class="sxs-lookup"><span data-stu-id="3548d-166">If the built-in servers don't meet the app's requirements, a custom server implementation can be created.</span></span> <span data-ttu-id="3548d-167">[.NET 的开放 Web 接口 (OWIN) 指南](xref:fundamentals/owin) 演示了如何编写基于 [Nowin](https://github.com/Bobris/Nowin) 的 [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) 实现。</span><span class="sxs-lookup"><span data-stu-id="3548d-167">The [Open Web Interface for .NET (OWIN) guide](xref:fundamentals/owin) demonstrates how to write a [Nowin](https://github.com/Bobris/Nowin)-based [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) implementation.</span></span> <span data-ttu-id="3548d-168">只有应用使用的功能接口需要实现，但至少必须支持 [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) 和 [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature)。</span><span class="sxs-lookup"><span data-stu-id="3548d-168">Only the feature interfaces that the app uses require implementation, though at a minimum [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) and [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature) must be supported.</span></span>

## <a name="server-startup"></a><span data-ttu-id="3548d-169">服务器启动</span><span class="sxs-lookup"><span data-stu-id="3548d-169">Server startup</span></span>

<span data-ttu-id="3548d-170">如果使用 [Visual Studio](https://www.visualstudio.com/vs/)、[Visual Studio for Mac](https://www.visualstudio.com/vs/mac/) 或 [Visual Studio Code](https://code.visualstudio.com/)，则服务器将在集成开发环境 (IDE) 启动应用时启动。</span><span class="sxs-lookup"><span data-stu-id="3548d-170">When using [Visual Studio](https://www.visualstudio.com/vs/), [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/), or [Visual Studio Code](https://code.visualstudio.com/), the server is launched when the app is started by the Integrated Development Environment (IDE).</span></span> <span data-ttu-id="3548d-171">在 Windows 上的 Visual Studio 中，可使用启动配置文件通过 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)或控制台来启动应用和服务器。</span><span class="sxs-lookup"><span data-stu-id="3548d-171">In Visual Studio on Windows, launch profiles can be used to start the app and server with either [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) or the console.</span></span> <span data-ttu-id="3548d-172">在 Visual Studio Code 中，应用和服务器由 [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode) 启动，这会激活 CoreCLR 调试程序。</span><span class="sxs-lookup"><span data-stu-id="3548d-172">In Visual Studio Code, the app and server are started by [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode), which activates the CoreCLR debugger.</span></span> <span data-ttu-id="3548d-173">使用 Visual Studio for Mac 时，应用和服务器由 [Mono Soft-Mode 调试程序](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)启动。</span><span class="sxs-lookup"><span data-stu-id="3548d-173">Using Visual Studio for Mac, the app and server are started by the [Mono Soft-Mode Debugger](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/).</span></span>

<span data-ttu-id="3548d-174">从项目文件夹中的命令提示符启动应用时，[dotnet run](/dotnet/core/tools/dotnet-run) 会启动该应用和服务器（仅 Kestrel 和 HTTP.sys）。</span><span class="sxs-lookup"><span data-stu-id="3548d-174">When launching an app from a command prompt in the project's folder, [dotnet run](/dotnet/core/tools/dotnet-run) launches the app and server (Kestrel and HTTP.sys only).</span></span> <span data-ttu-id="3548d-175">可通过 `-c|--configuration` 选项指定此配置，该选项设置为 `Debug`（默认值）或 `Release`。</span><span class="sxs-lookup"><span data-stu-id="3548d-175">The configuration is specified by the `-c|--configuration` option, which is set to either `Debug` (default) or `Release`.</span></span> <span data-ttu-id="3548d-176">如果启动配置文件位于 launchSettings.json 文件中，请使用 `--launch-profile <NAME>` 选项设置启动配置文件（例如 `Development` 或 `Production`）。</span><span class="sxs-lookup"><span data-stu-id="3548d-176">If launch profiles are present in a *launchSettings.json* file, use the `--launch-profile <NAME>` option to set the launch profile (for example, `Development` or `Production`).</span></span> <span data-ttu-id="3548d-177">有关详细信息，请参阅 [dotnet run](/dotnet/core/tools/dotnet-run) 和 [.NET Core 分发打包](/dotnet/core/build/distribution-packaging)主题。</span><span class="sxs-lookup"><span data-stu-id="3548d-177">For more information, see the [dotnet run](/dotnet/core/tools/dotnet-run) and [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging) topics.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3548d-178">其他资源</span><span class="sxs-lookup"><span data-stu-id="3548d-178">Additional resources</span></span>

* [<span data-ttu-id="3548d-179">Kestrel</span><span class="sxs-lookup"><span data-stu-id="3548d-179">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="3548d-180">Kestrel 与 IIS</span><span class="sxs-lookup"><span data-stu-id="3548d-180">Kestrel with IIS</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="3548d-181">在 Linux 上使用 Nginx 进行托管</span><span class="sxs-lookup"><span data-stu-id="3548d-181">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="3548d-182">在 Linux 上使用 Apache 进行托管</span><span class="sxs-lookup"><span data-stu-id="3548d-182">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* <span data-ttu-id="3548d-183">[HTTP.sys](xref:fundamentals/servers/httpsys)（对于 ASP.NET Core 1.x，请参阅 [WebListener](xref:fundamentals/servers/weblistener)）</span><span class="sxs-lookup"><span data-stu-id="3548d-183">[HTTP.sys](xref:fundamentals/servers/httpsys) (for ASP.NET Core 1.x, see [WebListener](xref:fundamentals/servers/weblistener))</span></span>
