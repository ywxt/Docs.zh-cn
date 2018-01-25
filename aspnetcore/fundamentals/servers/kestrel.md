---
title: "在 ASP.NET Core kestrel web 服务器实现"
author: tdykstra
description: "ASP.NET 核心基于 libuv，引入了 Kestrel，跨平台 web 服务器。"
ms.author: tdykstra
manager: wpickett
ms.date: 08/02/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/servers/kestrel
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e2b28f15e47789ac89213e57396060ee356ee33
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="96c53-103">在 ASP.NET Core Kestrel web 服务器实现简介</span><span class="sxs-lookup"><span data-stu-id="96c53-103">Introduction to Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="96c53-104">通过[Tom Dykstra](https://github.com/tdykstra)， [Chris 跨](https://github.com/Tratcher)，和[Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="96c53-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="96c53-105">Kestrel 是一个跨平台[ASP.NET Core 的 web 服务器](index.md)基于[libuv](https://github.com/libuv/libuv)，跨平台的异步 I/O 库。</span><span class="sxs-lookup"><span data-stu-id="96c53-105">Kestrel is a cross-platform [web server for ASP.NET Core](index.md) based on [libuv](https://github.com/libuv/libuv), a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="96c53-106">Kestrel 是默认情况下，ASP.NET Core 项目模板中包含的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="96c53-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span> 

<span data-ttu-id="96c53-107">Kestrel 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="96c53-107">Kestrel supports the following features:</span></span>

  * <span data-ttu-id="96c53-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="96c53-108">HTTPS</span></span>
  * <span data-ttu-id="96c53-109">用于启用的不透明升级[Websocket](https://github.com/aspnet/websockets)</span><span class="sxs-lookup"><span data-stu-id="96c53-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
  * <span data-ttu-id="96c53-110">为了获得高性能后面 Nginx Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="96c53-110">Unix sockets for high performance behind Nginx</span></span> 

<span data-ttu-id="96c53-111">Kestrel 支持所有平台和.NET 核心支持的版本。</span><span class="sxs-lookup"><span data-stu-id="96c53-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-112">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-112">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-113">[查看或下载 2.x 的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)([如何下载](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="96c53-113">[View or download sample code for 2.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-114">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-114">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="96c53-115">[查看或下载 1.x 的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)([如何下载](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="96c53-115">[View or download sample code for 1.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="96c53-116">何时使用反向代理使用 Kestrel</span><span class="sxs-lookup"><span data-stu-id="96c53-116">When to use Kestrel with a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-118">可以单独使用 Kestrel，也可以将其与反向代理服务器（如 IIS、Nginx 或 Apache）结合使用。</span><span class="sxs-lookup"><span data-stu-id="96c53-118">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="96c53-119">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="96c53-119">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="96c53-122">如果仅向内部网络公开 Kestrel，可以使用任一配置（无需考虑是否使用反向代理服务器）。</span><span class="sxs-lookup"><span data-stu-id="96c53-122">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is exposed only to an internal network.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-123">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-123">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="96c53-124">如果应用程序仅接受来自内部网络的请求，则可以单独使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="96c53-124">If your application accepts requests only from an internal network, you can use Kestrel by itself.</span></span>

![Kestrel 直接与你的内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="96c53-126">如果将应用程序公开到 Internet，则必须将 IIS、Nginx 或 Apache 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="96c53-126">If you expose your application to the Internet, you must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="96c53-127">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="96c53-127">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="96c53-129">反向代理是出于安全原因的边缘部署 （从 Internet 的流量到公开） 所必需的。</span><span class="sxs-lookup"><span data-stu-id="96c53-129">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="96c53-130">Kestrel 的 1.x 版本不包含对防御攻击的充分补充。</span><span class="sxs-lookup"><span data-stu-id="96c53-130">The 1.x versions of Kestrel don't have a full complement of defenses against attacks.</span></span> <span data-ttu-id="96c53-131">这包括但不限于适当超时、 大小限制和并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="96c53-131">This includes but isn't limited to appropriate timeouts, size limits, and concurrent connection limits.</span></span>

---

<span data-ttu-id="96c53-132">你有多个共享相同的 IP 和端口的单个服务器上运行的应用程序时需要反向代理的方案。</span><span class="sxs-lookup"><span data-stu-id="96c53-132">A scenario that requires a reverse proxy is when you have multiple applications that share the same IP and port running on a single server.</span></span> <span data-ttu-id="96c53-133">不能使用 Kestrel 直接因为 Kestrel 不支持共享相同的 IP 和多个进程之间的端口。</span><span class="sxs-lookup"><span data-stu-id="96c53-133">That doesn't work with Kestrel directly because Kestrel doesn't support sharing the same IP and port between multiple processes.</span></span> <span data-ttu-id="96c53-134">当配置 Kestrel 以在端口上侦听时，它将处理该端口而不考虑主机标头的所有流量。</span><span class="sxs-lookup"><span data-stu-id="96c53-134">When you configure Kestrel to listen on a port, it handles all traffic for that port regardless of host header.</span></span> <span data-ttu-id="96c53-135">可以共享端口的反向代理必须转发到 Kestrel 上唯一的 IP 和端口。</span><span class="sxs-lookup"><span data-stu-id="96c53-135">A reverse proxy that can share ports must then forward to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="96c53-136">即使反向代理服务器不是必需的则使用其中一个可能是出于其他原因的一个不错的选择：</span><span class="sxs-lookup"><span data-stu-id="96c53-136">Even if a reverse proxy server isn't required, using one might be a good choice for other reasons:</span></span>

* <span data-ttu-id="96c53-137">这样做可以防止你公开的外围应用。</span><span class="sxs-lookup"><span data-stu-id="96c53-137">It can limit your exposed surface area.</span></span>
* <span data-ttu-id="96c53-138">它提供一个可选的额外的配置和安全层。</span><span class="sxs-lookup"><span data-stu-id="96c53-138">It provides an optional additional layer of configuration and defense.</span></span>
* <span data-ttu-id="96c53-139">它可能与现有基础结构更好地集成。</span><span class="sxs-lookup"><span data-stu-id="96c53-139">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="96c53-140">它简化了负载平衡和 SSL 设置。</span><span class="sxs-lookup"><span data-stu-id="96c53-140">It simplifies load balancing and SSL set-up.</span></span> <span data-ttu-id="96c53-141">仅反向代理服务器需要 SSL 证书，并且该服务器可以与应用程序服务器内部网络上使用普通的 HTTP 通信。</span><span class="sxs-lookup"><span data-stu-id="96c53-141">Only your reverse proxy server requires an SSL certificate, and that server can communicate with your application servers on the internal network using plain HTTP.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="96c53-142">如何在 ASP.NET Core 应用中使用 Kestrel</span><span class="sxs-lookup"><span data-stu-id="96c53-142">How to use Kestrel in ASP.NET Core apps</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-144">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/)包包含在[Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)。</span><span class="sxs-lookup"><span data-stu-id="96c53-144">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="96c53-145">默认情况下，ASP.NET Core 项目模板使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="96c53-145">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="96c53-146">在*Program.cs*，模板代码调用`CreateDefaultBuilder`，哪些调用[UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)在后台。</span><span class="sxs-lookup"><span data-stu-id="96c53-146">In *Program.cs*, the template code calls `CreateDefaultBuilder`, which calls [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) behind the scenes.</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

<span data-ttu-id="96c53-147">如果你需要配置 Kestrel 选项，则调用`UseKestrel`中*Program.cs*下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="96c53-147">If you need to configure Kestrel options, call `UseKestrel` in *Program.cs* as shown in the following example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="96c53-149">安装[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="96c53-149">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="96c53-150">调用[UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)上的扩展方法`WebHostBuilder`中你`Main`方法，指定任何[Kestrel 选项](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)，你将需要在下一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="96c53-150">Call the [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) extension method on `WebHostBuilder` in your `Main` method, specifying any [Kestrel options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions) that you need, as shown in the next section.</span></span>

[!code-csharp[](kestrel/sample1/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a><span data-ttu-id="96c53-151">Kestrel 选项</span><span class="sxs-lookup"><span data-stu-id="96c53-151">Kestrel options</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-153">Kestrel web 服务器的约束配置选项，在面向 Internet 的部署中尤其有用。</span><span class="sxs-lookup"><span data-stu-id="96c53-153">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="96c53-154">下面是一些你可以设置的限制：</span><span class="sxs-lookup"><span data-stu-id="96c53-154">Here are some of the limits you can set:</span></span>

- <span data-ttu-id="96c53-155">客户端最大连接数</span><span class="sxs-lookup"><span data-stu-id="96c53-155">Maximum client connections</span></span>
- <span data-ttu-id="96c53-156">请求正文最大大小</span><span class="sxs-lookup"><span data-stu-id="96c53-156">Maximum request body size</span></span>
- <span data-ttu-id="96c53-157">请求正文最小数据速率</span><span class="sxs-lookup"><span data-stu-id="96c53-157">Minimum request body data rate</span></span>

<span data-ttu-id="96c53-158">你设置这些约束和中的其他人`Limits`属性[KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)类。</span><span class="sxs-lookup"><span data-stu-id="96c53-158">You set these constraints and others in the `Limits` property of the [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) class.</span></span> <span data-ttu-id="96c53-159">`Limits`属性包含的实例[KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)类。</span><span class="sxs-lookup"><span data-stu-id="96c53-159">The `Limits` property holds an instance of the [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) class.</span></span> 

<span data-ttu-id="96c53-160">**最大客户端连接**</span><span class="sxs-lookup"><span data-stu-id="96c53-160">**Maximum client connections**</span></span>

<span data-ttu-id="96c53-161">打开的并发 TCP 连接的最大数目可以设置整个应用程序替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="96c53-161">The maximum number of concurrent open TCP connections can be set for the entire application with the following code:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="96c53-162">没有已从 HTTP 或 HTTPS 升级到另一个协议 （例如，在 Websocket 请求） 的连接的单独限制。</span><span class="sxs-lookup"><span data-stu-id="96c53-162">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="96c53-163">升级连接后，它不会根据计数`MaxConcurrentConnections`限制。</span><span class="sxs-lookup"><span data-stu-id="96c53-163">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span> 

<span data-ttu-id="96c53-164">最大连接数为默认情况下的不限 (null)。</span><span class="sxs-lookup"><span data-stu-id="96c53-164">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="96c53-165">**最大请求正文大小**</span><span class="sxs-lookup"><span data-stu-id="96c53-165">**Maximum request body size**</span></span>

<span data-ttu-id="96c53-166">默认最大请求正文大小为 30,000,000 字节，这是大约 28.6 MB。</span><span class="sxs-lookup"><span data-stu-id="96c53-166">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span> 

<span data-ttu-id="96c53-167">重写中的 ASP.NET 核心 MVC 应用限制的建议的方法是使用[RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs)操作方法的特性：</span><span class="sxs-lookup"><span data-stu-id="96c53-167">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="96c53-168">下面是一个示例，演示如何配置整个应用程序，每个请求的约束：</span><span class="sxs-lookup"><span data-stu-id="96c53-168">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="96c53-169">您可以重写中中间件的特定请求上的设置：</span><span class="sxs-lookup"><span data-stu-id="96c53-169">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=3-4)]
 
<span data-ttu-id="96c53-170">如果你尝试在请求配置限制应用程序已开始读取请求后，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="96c53-170">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="96c53-171">没有`IsReadOnly`属性，告诉你如果`MaxRequestBodySize`属性处于只读状态，这意味着它太迟配置限制。</span><span class="sxs-lookup"><span data-stu-id="96c53-171">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="96c53-172">**最小的请求正文数据速率**</span><span class="sxs-lookup"><span data-stu-id="96c53-172">**Minimum request body data rate**</span></span>

<span data-ttu-id="96c53-173">如果数据即将推出的功能在指定的速率，单位为字节/秒，kestrel 检查每隔一秒。</span><span class="sxs-lookup"><span data-stu-id="96c53-173">Kestrel checks every second if data is coming in at the specified rate in bytes/second.</span></span> <span data-ttu-id="96c53-174">如果速率低于最小值，则会将连接操作已超时。宽限期是时间的 Kestrel 使客户端要增加到最小值; 其发送速率量在该时间段不检查速率。</span><span class="sxs-lookup"><span data-stu-id="96c53-174">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="96c53-175">宽限期有助于避免删除最初发送数据的比率较慢由于 TCP 缓慢启动的连接。</span><span class="sxs-lookup"><span data-stu-id="96c53-175">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="96c53-176">默认最小速度是 240 字节/秒、 5 秒宽限期。</span><span class="sxs-lookup"><span data-stu-id="96c53-176">The default minimum rate is 240 bytes/second, with a 5 second grace period.</span></span>

<span data-ttu-id="96c53-177">最小速度也适用于响应。</span><span class="sxs-lookup"><span data-stu-id="96c53-177">A minimum rate also applies to the response.</span></span> <span data-ttu-id="96c53-178">要设置的请求限制和响应上限的代码是除了具有相同`RequestBody`或`Response`中的属性和接口名称。</span><span class="sxs-lookup"><span data-stu-id="96c53-178">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span> 

<span data-ttu-id="96c53-179">下面是一个示例演示如何配置中的最小数据速率*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="96c53-179">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=6-9)]

<span data-ttu-id="96c53-180">你可以在中间件中配置每个请求的速率：</span><span class="sxs-lookup"><span data-stu-id="96c53-180">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="96c53-181">有关其他 Kestrel 选项的信息，请参阅以下类：</span><span class="sxs-lookup"><span data-stu-id="96c53-181">For information about other Kestrel options, see the following classes:</span></span>

* [<span data-ttu-id="96c53-182">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="96c53-182">KestrelServerOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)
* [<span data-ttu-id="96c53-183">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="96c53-183">KestrelServerLimits</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)
* [<span data-ttu-id="96c53-184">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="96c53-184">ListenOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-185">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-185">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="96c53-186">有关 Kestrel 选项的信息，请参阅[KestrelServerOptions 类](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)。</span><span class="sxs-lookup"><span data-stu-id="96c53-186">For information about Kestrel options, see [KestrelServerOptions class](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions).</span></span>

---

### <a name="endpoint-configuration"></a><span data-ttu-id="96c53-187">终结点配置</span><span class="sxs-lookup"><span data-stu-id="96c53-187">Endpoint configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-188">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-188">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-189">默认情况下 ASP.NET Core 将绑定到`http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="96c53-189">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="96c53-190">配置 URL 前缀和 Kestrel 通过调用侦听的端口`Listen`或`ListenUnixSocket`方法`KestrelServerOptions`。</span><span class="sxs-lookup"><span data-stu-id="96c53-190">You configure URL prefixes and ports for Kestrel to listen on by calling `Listen` or `ListenUnixSocket` methods on `KestrelServerOptions`.</span></span> <span data-ttu-id="96c53-191">(`UseUrls`、`urls`命令行参数，并且还工作 ASPNETCORE_URLS 环境变量但还有一些记下限制[本文稍后的](#useurls-limitations)。)</span><span class="sxs-lookup"><span data-stu-id="96c53-191">(`UseUrls`, the `urls` command-line argument, and the ASPNETCORE_URLS environment variable also work but have the limitations noted [later in this article](#useurls-limitations).)</span></span>

<span data-ttu-id="96c53-192">**将绑定到 TCP 套接字**</span><span class="sxs-lookup"><span data-stu-id="96c53-192">**Bind to a TCP socket**</span></span>

<span data-ttu-id="96c53-193">`Listen`方法绑定到 TCP 套接字，和选项 lambda 允许你配置的 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="96c53-193">The `Listen` method binds to a TCP socket, and an options lambda lets you configure an SSL certificate:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="96c53-194">请注意如何此示例将配置 SSL 特定终结点使用[ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)。</span><span class="sxs-lookup"><span data-stu-id="96c53-194">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs).</span></span> <span data-ttu-id="96c53-195">可以使用相同的 API 来配置其他 Kestrel 设置针对特定终结点。</span><span class="sxs-lookup"><span data-stu-id="96c53-195">You can use the same API to configure other Kestrel settings for particular endpoints.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

<span data-ttu-id="96c53-196">**将绑定到 Unix 套接字**</span><span class="sxs-lookup"><span data-stu-id="96c53-196">**Bind to a Unix socket**</span></span>

<span data-ttu-id="96c53-197">你可以侦听 Unix 套接字与 Nginx，提高了性能在此示例中所示：</span><span class="sxs-lookup"><span data-stu-id="96c53-197">You can listen on a Unix socket for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="96c53-198">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="96c53-198">**Port 0**</span></span>

<span data-ttu-id="96c53-199">如果指定端口号 0，Kestrel 动态将绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="96c53-199">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="96c53-200">下面的示例演示如何确定 Kestrel 实际绑定到在运行时的端口：</span><span class="sxs-lookup"><span data-stu-id="96c53-200">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Configure&highlight=3,13,16-17)]

<a id="useurls-limitations"></a>

<span data-ttu-id="96c53-201">**UseUrls 限制**</span><span class="sxs-lookup"><span data-stu-id="96c53-201">**UseUrls limitations**</span></span>

<span data-ttu-id="96c53-202">你可以通过调用配置终结点`UseUrls`方法或使用`urls`命令行自变量或 ASPNETCORE_URLS 环境变量。</span><span class="sxs-lookup"><span data-stu-id="96c53-202">You can configure endpoints by calling the `UseUrls` method or using the `urls` command-line argument or the ASPNETCORE_URLS environment variable.</span></span> <span data-ttu-id="96c53-203">这些方法都很有用，如果你想要代码适用于 Kestrel 以外的服务器。</span><span class="sxs-lookup"><span data-stu-id="96c53-203">These methods are useful if you want your code to work with servers other than Kestrel.</span></span> <span data-ttu-id="96c53-204">但是，请注意这些限制：</span><span class="sxs-lookup"><span data-stu-id="96c53-204">However, be aware of these limitations:</span></span>

* <span data-ttu-id="96c53-205">不能使用这些方法时使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="96c53-205">You can't use SSL with these methods.</span></span>
* <span data-ttu-id="96c53-206">如果你同时使用`Listen`方法和`UseUrls`、`Listen`终结点重写`UseUrls`终结点。</span><span class="sxs-lookup"><span data-stu-id="96c53-206">If you use both the `Listen` method and `UseUrls`, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="96c53-207">**IIS 的终结点配置**</span><span class="sxs-lookup"><span data-stu-id="96c53-207">**Endpoint configuration for IIS**</span></span>

<span data-ttu-id="96c53-208">如果你使用 IIS，IIS 的 URL 绑定重写通过调用设置的任何绑定`Listen`或`UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="96c53-208">If you use IIS, the URL bindings for IIS override any bindings that you set by calling either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="96c53-209">有关详细信息，请参阅[简介 ASP.NET 核心模块](aspnet-core-module.md)。</span><span class="sxs-lookup"><span data-stu-id="96c53-209">For more information, see [Introduction to ASP.NET Core Module](aspnet-core-module.md).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-210">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-210">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="96c53-211">默认情况下 ASP.NET Core 将绑定到`http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="96c53-211">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="96c53-212">你可以配置 URL 前缀和 Kestrel 使用侦听的端口`UseUrls`扩展方法，`urls`命令行参数或 ASP.NET 核心配置系统。</span><span class="sxs-lookup"><span data-stu-id="96c53-212">You can configure URL prefixes and ports for Kestrel to listen on by using the `UseUrls` extension method, the `urls` command-line argument, or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="96c53-213">有关这些方法的详细信息，请参阅[宿主](../../fundamentals/hosting.md)。</span><span class="sxs-lookup"><span data-stu-id="96c53-213">For more information about these methods, see [Hosting](../../fundamentals/hosting.md).</span></span> <span data-ttu-id="96c53-214">有关当你使用 IIS 的反向代理 URL 绑定的工作原理的信息，请参阅[ASP.NET 核心模块](aspnet-core-module.md)。</span><span class="sxs-lookup"><span data-stu-id="96c53-214">For information about how URL binding works when you use IIS as a reverse proxy, see [ASP.NET Core Module](aspnet-core-module.md).</span></span> 

---

### <a name="url-prefixes"></a><span data-ttu-id="96c53-215">URL 前缀</span><span class="sxs-lookup"><span data-stu-id="96c53-215">URL prefixes</span></span>

<span data-ttu-id="96c53-216">如果调用`UseUrls`或使用`urls`命令行自变量或 ASPNETCORE_URLS 环境变量，URL 前缀可以处于任何以下格式。</span><span class="sxs-lookup"><span data-stu-id="96c53-216">If you call `UseUrls` or use the `urls` command-line argument or ASPNETCORE_URLS environment variable, the URL prefixes can be in any of the following formats.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-217">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-217">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="96c53-218">HTTP URL 的前缀有效，则为Kestrel 不支持 SSL，当通过使用配置 URL 绑定`UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="96c53-218">Only HTTP URL prefixes are valid; Kestrel doesn't support SSL when you configure URL bindings by using `UseUrls`.</span></span>

* <span data-ttu-id="96c53-219">使用的端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="96c53-219">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="96c53-220">0.0.0.0 是一种特殊情况，将绑定到所有 IPv4 地址。</span><span class="sxs-lookup"><span data-stu-id="96c53-220">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="96c53-221">使用的端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="96c53-221">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  ```

  <span data-ttu-id="96c53-222">[:] 等同 IPv6 的 IPv4 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="96c53-222">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="96c53-223">主机名与端口号</span><span class="sxs-lookup"><span data-stu-id="96c53-223">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="96c53-224">主机名，\*，和 + 不是特殊。</span><span class="sxs-lookup"><span data-stu-id="96c53-224">Host names, \*, and +, are not special.</span></span> <span data-ttu-id="96c53-225">不是可识别的 IP 地址或"localhost"的任何内容将绑定到所有 IPv4 和 IPv6 Ip。</span><span class="sxs-lookup"><span data-stu-id="96c53-225">Anything that's not a recognized IP address or "localhost" will bind to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="96c53-226">如果你需要将不同的主机名绑定到不同的 ASP.NET Core 应用程序相同的端口上，使用[HTTP.sys](httpsys.md)或如 IIS、 Nginx 或 Apache 的反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="96c53-226">If you need to bind different host names to different ASP.NET Core applications on the same port, use [HTTP.sys](httpsys.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="96c53-227">使用端口号或环回 IP 与端口号的"Localhost"名称</span><span class="sxs-lookup"><span data-stu-id="96c53-227">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="96c53-228">当`localhost`Kestrel 尝试将绑定到 IPv4 和 IPv6 环回接口的指定。</span><span class="sxs-lookup"><span data-stu-id="96c53-228">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="96c53-229">如果请求的端口中使用任一环回接口上的其他服务，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="96c53-229">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="96c53-230">如果任一环回接口而不可用任何其他原因 （通常是因为不支持 IPv6 的大多数，） Kestrel 记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="96c53-230">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-231">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-231">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="96c53-232">使用的端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="96c53-232">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="96c53-233">0.0.0.0 是一种特殊情况，将绑定到所有 IPv4 地址。</span><span class="sxs-lookup"><span data-stu-id="96c53-233">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="96c53-234">使用的端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="96c53-234">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  https://[0:0:0:0:0:ffff:4137:270a]:443/ 
  ```

  <span data-ttu-id="96c53-235">[:] 等同 IPv6 的 IPv4 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="96c53-235">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="96c53-236">主机名与端口号</span><span class="sxs-lookup"><span data-stu-id="96c53-236">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="96c53-237">主机名， \*，并不特殊 +。</span><span class="sxs-lookup"><span data-stu-id="96c53-237">Host names, \*, and + aren't special.</span></span> <span data-ttu-id="96c53-238">不是可识别的 IP 地址或"localhost"的任何内容将绑定到所有 IPv4 和 IPv6 Ip。</span><span class="sxs-lookup"><span data-stu-id="96c53-238">Anything that isn't a recognized IP address or "localhost" binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="96c53-239">如果你需要将不同的主机名绑定到不同的 ASP.NET Core 应用程序相同的端口上，使用[WebListener](weblistener.md)或如 IIS、 Nginx 或 Apache 的反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="96c53-239">If you need to bind different host names to different ASP.NET Core applications on the same port, use [WebListener](weblistener.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="96c53-240">使用端口号或环回 IP 与端口号的"Localhost"名称</span><span class="sxs-lookup"><span data-stu-id="96c53-240">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="96c53-241">当`localhost`Kestrel 尝试将绑定到 IPv4 和 IPv6 环回接口的指定。</span><span class="sxs-lookup"><span data-stu-id="96c53-241">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="96c53-242">如果请求的端口中使用任一环回接口上的其他服务，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="96c53-242">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="96c53-243">如果任一环回接口而不可用任何其他原因 （通常是因为不支持 IPv6 的大多数，） Kestrel 记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="96c53-243">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

* <span data-ttu-id="96c53-244">Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="96c53-244">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock  
  ```

<span data-ttu-id="96c53-245">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="96c53-245">**Port 0**</span></span>

<span data-ttu-id="96c53-246">如果指定端口号 0，Kestrel 动态将绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="96c53-246">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="96c53-247">绑定到端口 0 允许任何主机名或 IP 除`localhost`名称。</span><span class="sxs-lookup"><span data-stu-id="96c53-247">Binding to port 0 is allowed for any host name or IP except for `localhost` name.</span></span>

<span data-ttu-id="96c53-248">下面的示例演示如何确定 Kestrel 实际绑定到在运行时的端口：</span><span class="sxs-lookup"><span data-stu-id="96c53-248">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample1/Startup.cs?name=snippet_Configure)]

<span data-ttu-id="96c53-249">**SSL 的 URL 前缀**</span><span class="sxs-lookup"><span data-stu-id="96c53-249">**URL prefixes for SSL**</span></span>

<span data-ttu-id="96c53-250">请务必包括使用的 URL 前缀`https:`如果调用`UseHttps`扩展方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96c53-250">Be sure to include URL prefixes with `https:` if you call the `UseHttps` extension method, as shown below.</span></span>

```csharp
var host = new WebHostBuilder() 
    .UseKestrel(options => 
    { 
        options.UseHttps("testCert.pfx", "testPassword"); 
    }) 
   .UseUrls("http://localhost:5000", "https://localhost:5001") 
   .UseContentRoot(Directory.GetCurrentDirectory()) 
   .UseStartup<Startup>() 
   .Build(); 
```

> [!NOTE]
> <span data-ttu-id="96c53-251">不在相同端口上承载 HTTPS 和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="96c53-251">HTTPS and HTTP cannot be hosted on the same port.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

---
## <a name="next-steps"></a><span data-ttu-id="96c53-252">后续步骤</span><span class="sxs-lookup"><span data-stu-id="96c53-252">Next steps</span></span>

<span data-ttu-id="96c53-253">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="96c53-253">For more information, see the following resources:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="96c53-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* [<span data-ttu-id="96c53-255">示例应用程序 2.x</span><span class="sxs-lookup"><span data-stu-id="96c53-255">Sample app for 2.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)
* [<span data-ttu-id="96c53-256">Kestrel 源代码</span><span class="sxs-lookup"><span data-stu-id="96c53-256">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="96c53-257">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="96c53-257">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* [<span data-ttu-id="96c53-258">1.x 的示例应用</span><span class="sxs-lookup"><span data-stu-id="96c53-258">Sample app for 1.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)
* [<span data-ttu-id="96c53-259">Kestrel 源代码</span><span class="sxs-lookup"><span data-stu-id="96c53-259">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

---
