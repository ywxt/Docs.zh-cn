---
title: ASP.NET Core 中的 Web 服务器实现
author: rick-anderson
description: 发现适用于 ASP.NET Core 的 Web 服务器 Kestrel 和 HTTP.sys。 了解如何选择服务器以及何时使用反向代理服务器。
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/21/2018
uid: fundamentals/servers/index
ms.openlocfilehash: 161ab3fdf48e58d8c9af991dc5531e46d9c5adff
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325856"
---
# <a name="web-server-implementations-in-aspnet-core"></a><span data-ttu-id="a692b-104">ASP.NET Core 中的 Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="a692b-104">Web server implementations in ASP.NET Core</span></span>

<span data-ttu-id="a692b-105">作者：[Tom Dykstra](https://github.com/tdykstra)、 [Steve Smith](https://ardalis.com/)、[Stephen Halter](https://twitter.com/halter73) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="a692b-105">By [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73), and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="a692b-106">ASP.NET Core 应用与进程内 HTTP 服务器实现一起运行。</span><span class="sxs-lookup"><span data-stu-id="a692b-106">An ASP.NET Core app runs with an in-process HTTP server implementation.</span></span> <span data-ttu-id="a692b-107">服务器实现侦听 HTTP 请求，并将它们作为由 <xref:Microsoft.AspNetCore.Http.HttpContext> 组成的[请求功能](xref:fundamentals/request-features)的集合呈现给应用。</span><span class="sxs-lookup"><span data-stu-id="a692b-107">The server implementation listens for HTTP requests and surfaces them to the app as sets of [request features](xref:fundamentals/request-features) composed into an <xref:Microsoft.AspNetCore.Http.HttpContext>.</span></span>

<span data-ttu-id="a692b-108">ASP.NET Core 交付三种服务器实现：</span><span class="sxs-lookup"><span data-stu-id="a692b-108">ASP.NET Core ships three server implementations:</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="a692b-109">[Kestrel](xref:fundamentals/servers/kestrel) 是适用于 ASP.NET Core 的默认跨平台 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="a692b-109">[Kestrel](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server for ASP.NET Core.</span></span>
* <span data-ttu-id="a692b-110">`IISHttpServer` 与 Windows 上的[进程内托管模型](xref:fundamentals/servers/aspnet-core-module#in-process-hosting-model)和 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)一起使用。</span><span class="sxs-lookup"><span data-stu-id="a692b-110">`IISHttpServer` is used with the [in-process hosting model](xref:fundamentals/servers/aspnet-core-module#in-process-hosting-model) and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) on Windows.</span></span>
* <span data-ttu-id="a692b-111">[HTTP.sys](xref:fundamentals/servers/httpsys) 是仅适用于 Windows 的 HTTP 服务器，它基于 [ 核心驱动程序和 HTTP 服务器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a692b-111">[HTTP.sys](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="a692b-112">（HTTP.sys 在 ASP.NET 1.x 中被命名为 [WebListener](xref:fundamentals/servers/weblistener)。）</span><span class="sxs-lookup"><span data-stu-id="a692b-112">(HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.)</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="a692b-113">[Kestrel](xref:fundamentals/servers/kestrel) 是适用于 ASP.NET Core 的默认跨平台 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="a692b-113">[Kestrel](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server for ASP.NET Core.</span></span>
* <span data-ttu-id="a692b-114">[HTTP.sys](xref:fundamentals/servers/httpsys) 是仅适用于 Windows 的 HTTP 服务器，它基于 [ 核心驱动程序和 HTTP 服务器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a692b-114">[HTTP.sys](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="a692b-115">（HTTP.sys 在 ASP.NET 1.x 中被命名为 [WebListener](xref:fundamentals/servers/weblistener)。）</span><span class="sxs-lookup"><span data-stu-id="a692b-115">(HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.)</span></span>

::: moniker-end

## <a name="kestrel"></a><span data-ttu-id="a692b-116">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a692b-116">Kestrel</span></span>

<span data-ttu-id="a692b-117">Kestrel 是 ASP.NET Core 项目模板中包括的默认 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="a692b-117">Kestrel is the default web server included in ASP.NET Core project templates.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="a692b-118">Kestrel 可以单独使用，也可以与反向代理服务器（如 IIS、Nginx 或 Apache）一起使用。</span><span class="sxs-lookup"><span data-stu-id="a692b-118">Kestrel can be used by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="a692b-119">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="a692b-119">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="a692b-122">使用或不使用反向代理服务器进行配置对 ASP.NET Core 2.0 或更高版本的应用来说都是有效且受支持的托管配置。</span><span class="sxs-lookup"><span data-stu-id="a692b-122">Either configuration&mdash;with or without a reverse proxy server&mdash;is a valid and supported hosting configuration for ASP.NET Core 2.0 or later apps.</span></span> <span data-ttu-id="a692b-123">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="a692b-123">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a692b-124">如果应用仅接受来自内部网络的请求，则可单独使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="a692b-124">If the app only accepts requests from an internal network, Kestrel can be used by itself.</span></span>

![Kestrel 直接与内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="a692b-126">如果将应用公开到 Internet，则必须将 IIS、Nginx 或 Apache 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="a692b-126">If the app is exposed to the Internet, Kestrel must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="a692b-127">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将其转发到 Kestrel，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a692b-127">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling, as shown in the following diagram:</span></span>

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="a692b-129">为公共边缘服务器部署（直接公开到 Internet）使用反向代理的最重要的原因是出于安全考虑。</span><span class="sxs-lookup"><span data-stu-id="a692b-129">The most important reason for using a reverse proxy for public-facing edge server deployments that are exposed directly the Internet is security.</span></span> <span data-ttu-id="a692b-130">Kestrel 的 1.x 版本不包含防御来自 Internet 的攻击的重要安全功能。</span><span class="sxs-lookup"><span data-stu-id="a692b-130">The 1.x versions of Kestrel don't have important security features to defend against attacks from the Internet.</span></span> <span data-ttu-id="a692b-131">这包括但不限于相应的超时、请求大小限制和并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="a692b-131">This includes, but isn't limited to, appropriate timeouts, request size limits, and concurrent connection limits.</span></span>

<span data-ttu-id="a692b-132">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="a692b-132">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

<span data-ttu-id="a692b-133">在没有 Kestrel 或[自定义服务器实现](#custom-servers)的情况下，不能使用 IIS、Nginx 和 Apache。</span><span class="sxs-lookup"><span data-stu-id="a692b-133">IIS, Nginx, and Apache can't be used without Kestrel or a [custom server implementation](#custom-servers).</span></span> <span data-ttu-id="a692b-134">ASP.NET Core 设计为在其自己的进程中运行，以实现跨平台统一操作。</span><span class="sxs-lookup"><span data-stu-id="a692b-134">ASP.NET Core was designed to run in its own process so that it can behave consistently across platforms.</span></span> <span data-ttu-id="a692b-135">IIS、Nginx 和 Apache 规定自己的启动过程和环境。</span><span class="sxs-lookup"><span data-stu-id="a692b-135">IIS, Nginx, and Apache dictate their own startup procedure and environment.</span></span> <span data-ttu-id="a692b-136">若要直接使用这些服务器技术，ASP.NET Core 必须满足每个服务器的需求。</span><span class="sxs-lookup"><span data-stu-id="a692b-136">To use these server technologies directly, ASP.NET Core would need to adapt to the requirements of each server.</span></span> <span data-ttu-id="a692b-137">使用 Kestrel 等 Web 服务器实现时，ASP.NET Core 可以控制托管在不同服务器技术上的启动过程和环境。</span><span class="sxs-lookup"><span data-stu-id="a692b-137">Using a web server implementation, such as Kestrel, ASP.NET Core has control over the startup process and environment when hosted on different server technologies.</span></span>

### <a name="iis-with-kestrel"></a><span data-ttu-id="a692b-138">IIS 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a692b-138">IIS with Kestrel</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="a692b-139">使用 [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 或 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 时，ASP.NET Core 应用在与 IIS 工作进程（进程内托管模型）相同的进程中运行或者在与 IIS 工作进程分离的进程中运行（进程外托管模型）。</span><span class="sxs-lookup"><span data-stu-id="a692b-139">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), the ASP.NET Core app either runs in the same process as the IIS worker process (the *in-process* hosting model) or in a process separate from the IIS worker process (the *out-of-process* hosting model).</span></span>

<span data-ttu-id="a692b-140">[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)是一个本机 IIS 模块，用于处理进程内 IIS Http 服务器或进程外 Kestrel 服务器之间的本机 IIS 请求。</span><span class="sxs-lookup"><span data-stu-id="a692b-140">The [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) is a native IIS module that handles native IIS requests between either the in-process IIS Http Server or the out-of-process Kestrel server.</span></span> <span data-ttu-id="a692b-141">有关更多信息，请参见<xref:fundamentals/servers/aspnet-core-module>。</span><span class="sxs-lookup"><span data-stu-id="a692b-141">For more information, see <xref:fundamentals/servers/aspnet-core-module>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="a692b-142">将 [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 或 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 用作 ASP.NET Core 的反向代理时，ASP.NET Core 应用在独立于 IIS 工作进程的某个进程中运行。</span><span class="sxs-lookup"><span data-stu-id="a692b-142">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) as a reverse proxy for ASP.NET Core, the ASP.NET Core app runs in a process separate from the IIS worker process.</span></span> <span data-ttu-id="a692b-143">在 IIS 进程中，[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)协调反向代理关系。</span><span class="sxs-lookup"><span data-stu-id="a692b-143">In the IIS process, the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) coordinates the reverse proxy relationship.</span></span> <span data-ttu-id="a692b-144">ASP.NET Core 模块的主要功能是启动 ASP.NET Core 应用，在其出现故障时重启应用，并向应用转发 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="a692b-144">The primary functions of the ASP.NET Core Module are to start the ASP.NET Core app, restart the app when it crashes, and forward HTTP traffic to the app.</span></span> <span data-ttu-id="a692b-145">有关更多信息，请参见<xref:fundamentals/servers/aspnet-core-module>。</span><span class="sxs-lookup"><span data-stu-id="a692b-145">For more information, see <xref:fundamentals/servers/aspnet-core-module>.</span></span>

::: moniker-end

### <a name="nginx-with-kestrel"></a><span data-ttu-id="a692b-146">Nginx 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a692b-146">Nginx with Kestrel</span></span>

<span data-ttu-id="a692b-147">若要了解如何在 Linux 上使用 Nginx 作为 Kestrel 的反向代理服务器，请参阅[在 Linux 上使用 Nginx 进行托管](xref:host-and-deploy/linux-nginx)。</span><span class="sxs-lookup"><span data-stu-id="a692b-147">For information on how to use Nginx on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Nginx](xref:host-and-deploy/linux-nginx).</span></span>

### <a name="apache-with-kestrel"></a><span data-ttu-id="a692b-148">Apache 与 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a692b-148">Apache with Kestrel</span></span>

<span data-ttu-id="a692b-149">若要了解如何在 Linux 上使用 Apache 作为 Kestrel 的反向代理服务器，请参阅[在 Linux 上使用 Apache 进行托管](xref:host-and-deploy/linux-apache)。</span><span class="sxs-lookup"><span data-stu-id="a692b-149">For information on how to use Apache on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Apache](xref:host-and-deploy/linux-apache).</span></span>

## <a name="httpsys"></a><span data-ttu-id="a692b-150">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a692b-150">HTTP.sys</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="a692b-151">如果 ASP.NET Core 应用在 Windows 上运行，则 HTTP.sys 是 Kestrel 的替代选项。</span><span class="sxs-lookup"><span data-stu-id="a692b-151">If ASP.NET Core apps are run on Windows, HTTP.sys is an alternative to Kestrel.</span></span> <span data-ttu-id="a692b-152">为了获得最佳性能，通常建议使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="a692b-152">Kestrel is generally recommended for best performance.</span></span> <span data-ttu-id="a692b-153">在应用向 Internet 公开且所需功能受 HTTP.sys（而不是 Kestrel）支持的方案中，可以使用 HTTP.sys。</span><span class="sxs-lookup"><span data-stu-id="a692b-153">HTTP.sys can be used in scenarios where the app is exposed to the Internet and required capabilities are supported by HTTP.sys but not Kestrel.</span></span> <span data-ttu-id="a692b-154">有关 HTTP.sys 的信息，请参阅 [HTTP.sys](xref:fundamentals/servers/httpsys)。</span><span class="sxs-lookup"><span data-stu-id="a692b-154">For information on HTTP.sys, see [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

![HTTP.sys 直接与 Internet 进行通信](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="a692b-156">对于仅向内部网络公开的应用，HTTP.sys 同样适用。</span><span class="sxs-lookup"><span data-stu-id="a692b-156">HTTP.sys can also be used for apps that are only exposed to an internal network.</span></span>

![HTTP.sys 直接与内部网络进行通信](httpsys/_static/httpsys-to-internal.png)

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a692b-158">HTTP.sys 在 ASP.NET Core 1.x 中被命名为 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="a692b-158">HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span> <span data-ttu-id="a692b-159">对于 IIS 不可用于托管应用的方案，如果 ASP.NET Core 应用在 Windows 上运行，则 WebListener 可用作替代选项。</span><span class="sxs-lookup"><span data-stu-id="a692b-159">If ASP.NET Core apps are run on Windows, WebListener is an alternative for scenarios where IIS isn't available to host apps.</span></span>

![Weblistener 直接与 Internet 进行通信](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="a692b-161">如果所需功能受 WebListener（而不是 Kestrel）支持，则对于仅向内部网络公开的应用而言，还可以使用 WebListener 来替代 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="a692b-161">WebListener can also be used in place of Kestrel for apps that are only exposed to an internal network, if required capabilities are supported by WebListener but not Kestrel.</span></span> <span data-ttu-id="a692b-162">有关 WebListener 的信息，请参阅 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="a692b-162">For information on WebListener, see [WebListener](xref:fundamentals/servers/weblistener).</span></span>

![Weblistener 直接与内部网络进行通信](weblistener/_static/weblistener-to-internal.png)

::: moniker-end

## <a name="aspnet-core-server-infrastructure"></a><span data-ttu-id="a692b-164">ASP.NET Core 服务器基础结构</span><span class="sxs-lookup"><span data-stu-id="a692b-164">ASP.NET Core server infrastructure</span></span>

<span data-ttu-id="a692b-165">`Startup.Configure` 方法中提供的 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 公开了类型 [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection) 的 [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) 属性。</span><span class="sxs-lookup"><span data-stu-id="a692b-165">The [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) available in the `Startup.Configure` method exposes the [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) property of type [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection).</span></span> <span data-ttu-id="a692b-166">Kestrel 和 HTTP.sys（在 ASP.NET Core 1.x 中为 WebListener）各自仅公开单个功能，即 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)，但是不同的服务器实现可能公开其他功能。</span><span class="sxs-lookup"><span data-stu-id="a692b-166">Kestrel and HTTP.sys (WebListener in ASP.NET Core 1.x) only expose a single feature each, [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature), but different server implementations may expose additional functionality.</span></span>

<span data-ttu-id="a692b-167">`IServerAddressesFeature` 可用于查找服务器实现在运行时绑定的端口。</span><span class="sxs-lookup"><span data-stu-id="a692b-167">`IServerAddressesFeature` can be used to find out which port the server implementation has bound at runtime.</span></span>

## <a name="custom-servers"></a><span data-ttu-id="a692b-168">自定义服务器</span><span class="sxs-lookup"><span data-stu-id="a692b-168">Custom servers</span></span>

<span data-ttu-id="a692b-169">如果内置服务器无法满足应用需求，可以创建一个自定义服务器实现。</span><span class="sxs-lookup"><span data-stu-id="a692b-169">If the built-in servers don't meet the app's requirements, a custom server implementation can be created.</span></span> <span data-ttu-id="a692b-170">[.NET 的开放 Web 接口 (OWIN) 指南](xref:fundamentals/owin) 演示了如何编写基于 [Nowin](https://github.com/Bobris/Nowin) 的 [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) 实现。</span><span class="sxs-lookup"><span data-stu-id="a692b-170">The [Open Web Interface for .NET (OWIN) guide](xref:fundamentals/owin) demonstrates how to write a [Nowin](https://github.com/Bobris/Nowin)-based [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) implementation.</span></span> <span data-ttu-id="a692b-171">只有应用使用的功能接口需要实现，但至少必须支持 [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) 和 [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature)。</span><span class="sxs-lookup"><span data-stu-id="a692b-171">Only the feature interfaces that the app uses require implementation, though at a minimum [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) and [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature) must be supported.</span></span>

## <a name="server-startup"></a><span data-ttu-id="a692b-172">服务器启动</span><span class="sxs-lookup"><span data-stu-id="a692b-172">Server startup</span></span>

<span data-ttu-id="a692b-173">如果使用 [Visual Studio](https://www.visualstudio.com/vs/)、[Visual Studio for Mac](https://www.visualstudio.com/vs/mac/) 或 [Visual Studio Code](https://code.visualstudio.com/)，则服务器将在集成开发环境 (IDE) 启动应用时启动。</span><span class="sxs-lookup"><span data-stu-id="a692b-173">When using [Visual Studio](https://www.visualstudio.com/vs/), [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/), or [Visual Studio Code](https://code.visualstudio.com/), the server is launched when the app is started by the Integrated Development Environment (IDE).</span></span> <span data-ttu-id="a692b-174">在 Windows 上的 Visual Studio 中，可使用启动配置文件通过 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)或控制台来启动应用和服务器。</span><span class="sxs-lookup"><span data-stu-id="a692b-174">In Visual Studio on Windows, launch profiles can be used to start the app and server with either [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) or the console.</span></span> <span data-ttu-id="a692b-175">在 Visual Studio Code 中，应用和服务器由 [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode) 启动，这会激活 CoreCLR 调试程序。</span><span class="sxs-lookup"><span data-stu-id="a692b-175">In Visual Studio Code, the app and server are started by [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode), which activates the CoreCLR debugger.</span></span> <span data-ttu-id="a692b-176">使用 Visual Studio for Mac 时，应用和服务器由 [Mono Soft-Mode 调试程序](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)启动。</span><span class="sxs-lookup"><span data-stu-id="a692b-176">Using Visual Studio for Mac, the app and server are started by the [Mono Soft-Mode Debugger](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/).</span></span>

<span data-ttu-id="a692b-177">从项目文件夹中的命令提示符启动应用时，[dotnet run](/dotnet/core/tools/dotnet-run) 会启动该应用和服务器（仅 Kestrel 和 HTTP.sys）。</span><span class="sxs-lookup"><span data-stu-id="a692b-177">When launching an app from a command prompt in the project's folder, [dotnet run](/dotnet/core/tools/dotnet-run) launches the app and server (Kestrel and HTTP.sys only).</span></span> <span data-ttu-id="a692b-178">可通过 `-c|--configuration` 选项指定此配置，该选项设置为 `Debug`（默认值）或 `Release`。</span><span class="sxs-lookup"><span data-stu-id="a692b-178">The configuration is specified by the `-c|--configuration` option, which is set to either `Debug` (default) or `Release`.</span></span> <span data-ttu-id="a692b-179">如果启动配置文件位于 launchSettings.json 文件中，请使用 `--launch-profile <NAME>` 选项设置启动配置文件（例如 `Development` 或 `Production`）。</span><span class="sxs-lookup"><span data-stu-id="a692b-179">If launch profiles are present in a *launchSettings.json* file, use the `--launch-profile <NAME>` option to set the launch profile (for example, `Development` or `Production`).</span></span> <span data-ttu-id="a692b-180">有关详细信息，请参阅 [dotnet run](/dotnet/core/tools/dotnet-run) 和 [.NET Core 分发打包](/dotnet/core/build/distribution-packaging)主题。</span><span class="sxs-lookup"><span data-stu-id="a692b-180">For more information, see the [dotnet run](/dotnet/core/tools/dotnet-run) and [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging) topics.</span></span>

## <a name="http2-support"></a><span data-ttu-id="a692b-181">HTTP/2 支持</span><span class="sxs-lookup"><span data-stu-id="a692b-181">HTTP/2 support</span></span>

<span data-ttu-id="a692b-182">以下部署方案中的 ASP.NET Core 支持 [HTTP/2](https://httpwg.org/specs/rfc7540.html)：</span><span class="sxs-lookup"><span data-stu-id="a692b-182">[HTTP/2](https://httpwg.org/specs/rfc7540.html) is supported with ASP.NET Core in the following deployment scenarios:</span></span>

::: moniker range=">= aspnetcore-2.2"

* [<span data-ttu-id="a692b-183">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a692b-183">Kestrel</span></span>](xref:fundamentals/servers/kestrel#http2-support)
  * <span data-ttu-id="a692b-184">操作系统</span><span class="sxs-lookup"><span data-stu-id="a692b-184">Operating system</span></span>
    * <span data-ttu-id="a692b-185">Windows Server 2012 R2/Windows 8.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-185">Windows Server 2012 R2/Windows 8.1 or later</span></span>
    * <span data-ttu-id="a692b-186">具有 OpenSSL 1.0.2 或更高版本的 Linux（例如，Ubuntu 16.04 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="a692b-186">Linux with OpenSSL 1.0.2 or later (for example, Ubuntu 16.04 or later)</span></span>
    * <span data-ttu-id="a692b-187">macOS 的未来版本将支持 HTTP/2。</span><span class="sxs-lookup"><span data-stu-id="a692b-187">HTTP/2 will be supported on macOS in a future release.</span></span>
  * <span data-ttu-id="a692b-188">目标框架：.NET Core 2.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-188">Target framework: .NET Core 2.2 or later</span></span>
* [<span data-ttu-id="a692b-189">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a692b-189">HTTP.sys</span></span>](xref:fundamentals/servers/httpsys#http2-support)
  * <span data-ttu-id="a692b-190">Windows Server 2016/Windows 10 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-190">Windows Server 2016/Windows 10 or later</span></span>
  * <span data-ttu-id="a692b-191">目标框架：不适用于 HTTP.sys 部署。</span><span class="sxs-lookup"><span data-stu-id="a692b-191">Target framework: Not applicable to HTTP.sys deployments.</span></span>
* [<span data-ttu-id="a692b-192">IIS（进程内）</span><span class="sxs-lookup"><span data-stu-id="a692b-192">IIS (in-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a692b-193">Windows Server 2016/Windows 10 或更高版本；IIS 10 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-193">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a692b-194">目标框架：.NET Core 2.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-194">Target framework: .NET Core 2.2 or later</span></span>
* [<span data-ttu-id="a692b-195">IIS（进程外）</span><span class="sxs-lookup"><span data-stu-id="a692b-195">IIS (out-of-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a692b-196">Windows Server 2016/Windows 10 或更高版本；IIS 10 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-196">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a692b-197">面向公众的边缘服务器连接使用 HTTP/2，但与 Kestrel 的反向代理连接使用 HTTP/1.1。</span><span class="sxs-lookup"><span data-stu-id="a692b-197">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to Kestrel uses HTTP/1.1.</span></span>
  * <span data-ttu-id="a692b-198">目标框架：不适用于 IIS 进程外部署。</span><span class="sxs-lookup"><span data-stu-id="a692b-198">Target framework: Not applicable to IIS out-of-process deployments.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* [<span data-ttu-id="a692b-199">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a692b-199">HTTP.sys</span></span>](xref:fundamentals/servers/httpsys#http2-support)
  * <span data-ttu-id="a692b-200">Windows Server 2016/Windows 10 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-200">Windows Server 2016/Windows 10 or later</span></span>
  * <span data-ttu-id="a692b-201">目标框架：不适用于 HTTP.sys 部署。</span><span class="sxs-lookup"><span data-stu-id="a692b-201">Target framework: Not applicable to HTTP.sys deployments.</span></span>
* [<span data-ttu-id="a692b-202">IIS（进程外）</span><span class="sxs-lookup"><span data-stu-id="a692b-202">IIS (out-of-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a692b-203">Windows Server 2016/Windows 10 或更高版本；IIS 10 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a692b-203">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a692b-204">面向公众的边缘服务器连接使用 HTTP/2，但与 Kestrel 的反向代理连接使用 HTTP/1.1。</span><span class="sxs-lookup"><span data-stu-id="a692b-204">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to Kestrel uses HTTP/1.1.</span></span>
  * <span data-ttu-id="a692b-205">目标框架：不适用于 IIS 进程外部署。</span><span class="sxs-lookup"><span data-stu-id="a692b-205">Target framework: Not applicable to IIS out-of-process deployments.</span></span>

::: moniker-end

<span data-ttu-id="a692b-206">HTTP/2 连接必须使用[应用程序层协议协商 (ALPN)](https://tools.ietf.org/html/rfc7301#section-3) 和 TLS 1.2 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="a692b-206">An HTTP/2 connection must use [Application-Layer Protocol Negotiation (ALPN)](https://tools.ietf.org/html/rfc7301#section-3) and TLS 1.2 or later.</span></span> <span data-ttu-id="a692b-207">有关详细信息，请参阅与服务器部署方案相关的主题。</span><span class="sxs-lookup"><span data-stu-id="a692b-207">For more information, see the topics that pertain to your server deployment scenarios.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a692b-208">其他资源</span><span class="sxs-lookup"><span data-stu-id="a692b-208">Additional resources</span></span>

* <xref:fundamentals/servers/kestrel>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/azure-apps/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <span data-ttu-id="a692b-209"><xref:fundamentals/servers/httpsys>（对于 ASP.NET Core 1.x，请参阅 <xref:fundamentals/servers/weblistener>）</span><span class="sxs-lookup"><span data-stu-id="a692b-209"><xref:fundamentals/servers/httpsys> (for ASP.NET Core 1.x, see <xref:fundamentals/servers/weblistener>)</span></span>
