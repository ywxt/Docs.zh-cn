---
title: "ASP.NET Core 中的 Kestrel Web 服务器实现"
author: tdykstra
description: "介绍基于 libuv 的跨平台 ASP.NET Core Web 服务器 Kestrel。"
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: bfe7644891296c7c3485c9a870d90951ba87e9e8
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="24e91-103">ASP.NET Core 中的 Kestrel Web 服务器实现简介</span><span class="sxs-lookup"><span data-stu-id="24e91-103">Introduction to Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="24e91-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Chris Ross](https://github.com/Tratcher) 和 [Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="24e91-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="24e91-105">Kestrel 是跨平台 [ASP.NET Core Web 服务器](index.md)，它基于 [libuv](https://github.com/libuv/libuv)（一个跨平台异步 I/O 库）。</span><span class="sxs-lookup"><span data-stu-id="24e91-105">Kestrel is a cross-platform [web server for ASP.NET Core](index.md) based on [libuv](https://github.com/libuv/libuv), a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="24e91-106">Kestrel 是 Web 服务器，默认包括在 ASP.NET Core 项目模板中。</span><span class="sxs-lookup"><span data-stu-id="24e91-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span> 

<span data-ttu-id="24e91-107">Kestrel 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="24e91-107">Kestrel supports the following features:</span></span>

  * <span data-ttu-id="24e91-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="24e91-108">HTTPS</span></span>
  * <span data-ttu-id="24e91-109">用于启用 [WebSocket](https://github.com/aspnet/websockets) 的不透明升级</span><span class="sxs-lookup"><span data-stu-id="24e91-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
  * <span data-ttu-id="24e91-110">用于获得 Nginx 高性能的 Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="24e91-110">Unix sockets for high performance behind Nginx</span></span> 

<span data-ttu-id="24e91-111">.NET Core 支持的所有平台和版本均支持 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-112">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-112">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-113">[查看或下载 2.x 示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="24e91-113">[View or download sample code for 2.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-114">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-114">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="24e91-115">[查看或下载 1.x 示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="24e91-115">[View or download sample code for 1.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="24e91-116">何时结合使用 Kestrel 和反向代理</span><span class="sxs-lookup"><span data-stu-id="24e91-116">When to use Kestrel with a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-118">可以单独使用 Kestrel，也可以将其与反向代理服务器（如 IIS、Nginx 或 Apache）结合使用。</span><span class="sxs-lookup"><span data-stu-id="24e91-118">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="24e91-119">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-119">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="24e91-122">如果仅向内部网络公开 Kestrel，可以使用任一配置（无需考虑是否使用反向代理服务器）。</span><span class="sxs-lookup"><span data-stu-id="24e91-122">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is exposed only to an internal network.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-123">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-123">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="24e91-124">如果应用程序仅接受来自内部网络的请求，则可以单独使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-124">If your application accepts requests only from an internal network, you can use Kestrel by itself.</span></span>

![Kestrel 直接与你的内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="24e91-126">如果将应用程序公开到 Internet，则必须将 IIS、Nginx 或 Apache 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="24e91-126">If you expose your application to the Internet, you must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="24e91-127">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-127">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="24e91-129">出于安全考虑，边缘部署需要使用反向代理（从 Internet 公开到流量）。</span><span class="sxs-lookup"><span data-stu-id="24e91-129">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="24e91-130">Kestrel 的 1.x 版本不包含对防御攻击的充分补充。</span><span class="sxs-lookup"><span data-stu-id="24e91-130">The 1.x versions of Kestrel don't have a full complement of defenses against attacks.</span></span> <span data-ttu-id="24e91-131">这包括但不限于相应的超时、大小限制和并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="24e91-131">This includes but isn't limited to appropriate timeouts, size limits, and concurrent connection limits.</span></span>

---

<span data-ttu-id="24e91-132">需要反向代理的一种方案是，具有共享在单个服务器上运行的相同 IP 和端口的多个应用程序。</span><span class="sxs-lookup"><span data-stu-id="24e91-132">A scenario that requires a reverse proxy is when you have multiple applications that share the same IP and port running on a single server.</span></span> <span data-ttu-id="24e91-133">此方案无法直接使用 Kestrel，因为 Kestrel 不支持在多个进程之间共享相同 IP 和端口。</span><span class="sxs-lookup"><span data-stu-id="24e91-133">That doesn't work with Kestrel directly because Kestrel doesn't support sharing the same IP and port between multiple processes.</span></span> <span data-ttu-id="24e91-134">配置 Kestrel 来侦听端口时，它会处理该端口的所有流量而不考虑主机头。</span><span class="sxs-lookup"><span data-stu-id="24e91-134">When you configure Kestrel to listen on a port, it handles all traffic for that port regardless of host header.</span></span> <span data-ttu-id="24e91-135">可共享端口的反向代理随后必须通过唯一 IP 和端口转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-135">A reverse proxy that can share ports must then forward to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="24e91-136">即使不需要反向代理服务器，但出于以下其他原因，使用反向代理服务器可能是一个不错的选择：</span><span class="sxs-lookup"><span data-stu-id="24e91-136">Even if a reverse proxy server isn't required, using one might be a good choice for other reasons:</span></span>

* <span data-ttu-id="24e91-137">它可以限制公开的外围应用。</span><span class="sxs-lookup"><span data-stu-id="24e91-137">It can limit your exposed surface area.</span></span>
* <span data-ttu-id="24e91-138">它可以提供额外的可选配置和防护层。</span><span class="sxs-lookup"><span data-stu-id="24e91-138">It provides an optional additional layer of configuration and defense.</span></span>
* <span data-ttu-id="24e91-139">它可以更好地与现有基础结构集成。</span><span class="sxs-lookup"><span data-stu-id="24e91-139">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="24e91-140">它可以简化负载均衡和 SSL 设置。</span><span class="sxs-lookup"><span data-stu-id="24e91-140">It simplifies load balancing and SSL set-up.</span></span> <span data-ttu-id="24e91-141">仅反向代理服务器需要 SSL 证书，并且该服务器可使用普通 HTTP 在内部网络上与应用程序服务器通信。</span><span class="sxs-lookup"><span data-stu-id="24e91-141">Only your reverse proxy server requires an SSL certificate, and that server can communicate with your application servers on the internal network using plain HTTP.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="24e91-142">如何在 ASP.NET Core 应用中使用 Kestrel</span><span class="sxs-lookup"><span data-stu-id="24e91-142">How to use Kestrel in ASP.NET Core apps</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-144">[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中包括 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 包。</span><span class="sxs-lookup"><span data-stu-id="24e91-144">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="24e91-145">默认情况下，ASP.NET Core 项目模板使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="24e91-145">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="24e91-146">在 Program.cs 中，模板代码调用 `CreateDefaultBuilder`，后者在后台调用 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)。</span><span class="sxs-lookup"><span data-stu-id="24e91-146">In *Program.cs*, the template code calls `CreateDefaultBuilder`, which calls [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) behind the scenes.</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

<span data-ttu-id="24e91-147">如果需要配置 Kestrel 选项，请调用 Program.cs 中的 `UseKestrel`，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="24e91-147">If you need to configure Kestrel options, call `UseKestrel` in *Program.cs* as shown in the following example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="24e91-149">安装 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="24e91-149">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="24e91-150">在 `WebHostBuilder` 上调用 `Main` 方法中的 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 扩展方法，指定所需的任何 [Kestrel 选项](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)，如下一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="24e91-150">Call the [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) extension method on `WebHostBuilder` in your `Main` method, specifying any [Kestrel options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions) that you need, as shown in the next section.</span></span>

[!code-csharp[](kestrel/sample1/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a><span data-ttu-id="24e91-151">Kestrel 选项</span><span class="sxs-lookup"><span data-stu-id="24e91-151">Kestrel options</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-153">Kestrel Web 服务器具有约束配置选项，这些选项在面向 Internet 的部署中尤其有用。</span><span class="sxs-lookup"><span data-stu-id="24e91-153">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="24e91-154">下面是一些可以设置的限制：</span><span class="sxs-lookup"><span data-stu-id="24e91-154">Here are some of the limits you can set:</span></span>

- <span data-ttu-id="24e91-155">客户端最大连接数</span><span class="sxs-lookup"><span data-stu-id="24e91-155">Maximum client connections</span></span>
- <span data-ttu-id="24e91-156">请求正文最大大小</span><span class="sxs-lookup"><span data-stu-id="24e91-156">Maximum request body size</span></span>
- <span data-ttu-id="24e91-157">请求正文最小数据速率</span><span class="sxs-lookup"><span data-stu-id="24e91-157">Minimum request body data rate</span></span>

<span data-ttu-id="24e91-158">可在 [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) 类的 `Limits` 属性中设置这些约束和其他约束。</span><span class="sxs-lookup"><span data-stu-id="24e91-158">You set these constraints and others in the `Limits` property of the [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) class.</span></span> <span data-ttu-id="24e91-159">`Limits` 属性包含 [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) 类的实例。</span><span class="sxs-lookup"><span data-stu-id="24e91-159">The `Limits` property holds an instance of the [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) class.</span></span> 

<span data-ttu-id="24e91-160">**客户端最大连接数**</span><span class="sxs-lookup"><span data-stu-id="24e91-160">**Maximum client connections**</span></span>

<span data-ttu-id="24e91-161">可使用以下代码为整个应用程序设置并发打开 TCP 的最大连接数：</span><span class="sxs-lookup"><span data-stu-id="24e91-161">The maximum number of concurrent open TCP connections can be set for the entire application with the following code:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="24e91-162">对于已从 HTTP 或 HTTPS 升级到另一个协议（例如，Websocket 请求）的连接，有一个单独的限制。</span><span class="sxs-lookup"><span data-stu-id="24e91-162">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="24e91-163">连接升级后，不会计入 `MaxConcurrentConnections` 限制。</span><span class="sxs-lookup"><span data-stu-id="24e91-163">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span> 

<span data-ttu-id="24e91-164">默认情况下，最大连接数不受限制 (NULL)。</span><span class="sxs-lookup"><span data-stu-id="24e91-164">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="24e91-165">**请求正文最大大小**</span><span class="sxs-lookup"><span data-stu-id="24e91-165">**Maximum request body size**</span></span>

<span data-ttu-id="24e91-166">默认的请求正文最大大小为 30,000,000 字节，大约 28.6MB。</span><span class="sxs-lookup"><span data-stu-id="24e91-166">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span> 

<span data-ttu-id="24e91-167">在 ASP.NET Core MVC 应用中替代限制的推荐方法是在操作方法上使用 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 属性：</span><span class="sxs-lookup"><span data-stu-id="24e91-167">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="24e91-168">以下示例演示如何为整个应用程序和每个请求配置约束：</span><span class="sxs-lookup"><span data-stu-id="24e91-168">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="24e91-169">可在中间件中替代特定请求的设置：</span><span class="sxs-lookup"><span data-stu-id="24e91-169">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=3-4)]
 
<span data-ttu-id="24e91-170">如果在应用程序开始读取请求后尝试配置请求限制，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="24e91-170">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="24e91-171">通过 `IsReadOnly` 属性可知道，如果 `MaxRequestBodySize` 属性处于只读状态，则意味着配置限制已经太迟了。</span><span class="sxs-lookup"><span data-stu-id="24e91-171">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="24e91-172">**请求正文最小数据速率**</span><span class="sxs-lookup"><span data-stu-id="24e91-172">**Minimum request body data rate**</span></span>

<span data-ttu-id="24e91-173">Kestrel 每秒检查一次数据是否以指定的速率（字节/秒）进入。</span><span class="sxs-lookup"><span data-stu-id="24e91-173">Kestrel checks every second if data is coming in at the specified rate in bytes/second.</span></span> <span data-ttu-id="24e91-174">如果速率低于最小值，则连接超时。宽限期是 Kestrel 提供给客户端用于将其发送速率提升到最小值的时间量；在此期间不会检查速率。</span><span class="sxs-lookup"><span data-stu-id="24e91-174">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="24e91-175">宽限期有助于避免最初由于 TCP 慢启动而以较慢速率发送数据的连接中断。</span><span class="sxs-lookup"><span data-stu-id="24e91-175">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="24e91-176">默认的最小速率为 240 字节/秒，包含 5 秒的宽限期。</span><span class="sxs-lookup"><span data-stu-id="24e91-176">The default minimum rate is 240 bytes/second, with a 5 second grace period.</span></span>

<span data-ttu-id="24e91-177">最小速率也适用于响应。</span><span class="sxs-lookup"><span data-stu-id="24e91-177">A minimum rate also applies to the response.</span></span> <span data-ttu-id="24e91-178">除了属性和接口名称中具有 `RequestBody` 或 `Response` 以外，用于设置请求限制和响应限制的代码相同。</span><span class="sxs-lookup"><span data-stu-id="24e91-178">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span> 

<span data-ttu-id="24e91-179">以下示例演示如何在 Program.cs 中配置最小数据速率：</span><span class="sxs-lookup"><span data-stu-id="24e91-179">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=6-9)]

<span data-ttu-id="24e91-180">可在中间件中配置每个请求的速率：</span><span class="sxs-lookup"><span data-stu-id="24e91-180">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="24e91-181">有关其他 Kestrel 选项的信息，请参阅以下类：</span><span class="sxs-lookup"><span data-stu-id="24e91-181">For information about other Kestrel options, see the following classes:</span></span>

* [<span data-ttu-id="24e91-182">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="24e91-182">KestrelServerOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)
* [<span data-ttu-id="24e91-183">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="24e91-183">KestrelServerLimits</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)
* [<span data-ttu-id="24e91-184">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="24e91-184">ListenOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-185">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-185">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="24e91-186">有关 Kestrel 选项的信息，请参阅 [KestrelServerOptions class](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)（KestrelServerOptions 类）。</span><span class="sxs-lookup"><span data-stu-id="24e91-186">For information about Kestrel options, see [KestrelServerOptions class](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions).</span></span>

---

### <a name="endpoint-configuration"></a><span data-ttu-id="24e91-187">终结点配置</span><span class="sxs-lookup"><span data-stu-id="24e91-187">Endpoint configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-188">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-188">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-189">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="24e91-189">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="24e91-190">通过调用 `KestrelServerOptions` 上的 `Listen` 或 `ListenUnixSocket` 方法，配置 URL 前缀和 Kestrel 要侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="24e91-190">You configure URL prefixes and ports for Kestrel to listen on by calling `Listen` or `ListenUnixSocket` methods on `KestrelServerOptions`.</span></span> <span data-ttu-id="24e91-191">（`UseUrls`、`urls` 命令行参数以及 ASPNETCORE_URLS 环境变量也有用，但具有[本文后面](#useurls-limitations)注明的限制。）</span><span class="sxs-lookup"><span data-stu-id="24e91-191">(`UseUrls`, the `urls` command-line argument, and the ASPNETCORE_URLS environment variable also work but have the limitations noted [later in this article](#useurls-limitations).)</span></span>

<span data-ttu-id="24e91-192">**绑定到 TCP 套接字**</span><span class="sxs-lookup"><span data-stu-id="24e91-192">**Bind to a TCP socket**</span></span>

<span data-ttu-id="24e91-193">使用 `Listen` 方法绑定到 TCP 套接字，并可通过选项 lambda 配置 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="24e91-193">The `Listen` method binds to a TCP socket, and an options lambda lets you configure an SSL certificate:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="24e91-194">请注意此示例如何使用 [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs) 为特定终结点配置 SSL。</span><span class="sxs-lookup"><span data-stu-id="24e91-194">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs).</span></span> <span data-ttu-id="24e91-195">可使用相同 API 为特定终结点配置其他 Kestrel 设置。</span><span class="sxs-lookup"><span data-stu-id="24e91-195">You can use the same API to configure other Kestrel settings for particular endpoints.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

<span data-ttu-id="24e91-196">**绑定到 Unix 套接字**</span><span class="sxs-lookup"><span data-stu-id="24e91-196">**Bind to a Unix socket**</span></span>

<span data-ttu-id="24e91-197">可侦听 Unix 套接字以提高 Nginx 的性能，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="24e91-197">You can listen on a Unix socket for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="24e91-198">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="24e91-198">**Port 0**</span></span>

<span data-ttu-id="24e91-199">如果指定端口号 0，Kestrel 将动态绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="24e91-199">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="24e91-200">以下示例演示如何确定 Kestrel 在运行时实际绑定到的端口：</span><span class="sxs-lookup"><span data-stu-id="24e91-200">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Configure&highlight=3,13,16-17)]

<a id="useurls-limitations"></a>

<span data-ttu-id="24e91-201">**UseUrls 限制**</span><span class="sxs-lookup"><span data-stu-id="24e91-201">**UseUrls limitations**</span></span>

<span data-ttu-id="24e91-202">可通过调用 `UseUrls` 方法或使用 `urls` 命令行参数或 ASPNETCORE_URLS 环境变量来配置终结点。</span><span class="sxs-lookup"><span data-stu-id="24e91-202">You can configure endpoints by calling the `UseUrls` method or using the `urls` command-line argument or the ASPNETCORE_URLS environment variable.</span></span> <span data-ttu-id="24e91-203">如果希望将代码用于 Kestrel 以外的服务器，这些方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="24e91-203">These methods are useful if you want your code to work with servers other than Kestrel.</span></span> <span data-ttu-id="24e91-204">但是，请注意以下限制：</span><span class="sxs-lookup"><span data-stu-id="24e91-204">However, be aware of these limitations:</span></span>

* <span data-ttu-id="24e91-205">不能将这些方法与 SSL 结合使用。</span><span class="sxs-lookup"><span data-stu-id="24e91-205">You can't use SSL with these methods.</span></span>
* <span data-ttu-id="24e91-206">如果同时使用 `Listen` 方法和 `UseUrls`，`Listen` 终结点将替代 `UseUrls` 终结点。</span><span class="sxs-lookup"><span data-stu-id="24e91-206">If you use both the `Listen` method and `UseUrls`, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="24e91-207">**IIS 的终结点配置**</span><span class="sxs-lookup"><span data-stu-id="24e91-207">**Endpoint configuration for IIS**</span></span>

<span data-ttu-id="24e91-208">如果使用 IIS，IIS 的 URL 绑定将替代通过调用 `Listen` 或 `UseUrls` 设置的任何绑定。</span><span class="sxs-lookup"><span data-stu-id="24e91-208">If you use IIS, the URL bindings for IIS override any bindings that you set by calling either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="24e91-209">有关详细信息，请参阅 [ASP.NET Core 模块简介](aspnet-core-module.md)。</span><span class="sxs-lookup"><span data-stu-id="24e91-209">For more information, see [Introduction to ASP.NET Core Module](aspnet-core-module.md).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-210">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-210">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="24e91-211">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="24e91-211">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="24e91-212">可使用 `UseUrls` 扩展方法、`urls` 命令行参数或 ASP.NET Core 配置系统来配置 URL 前缀和 Kestrel 要侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="24e91-212">You can configure URL prefixes and ports for Kestrel to listen on by using the `UseUrls` extension method, the `urls` command-line argument, or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="24e91-213">有关这些方法的详细信息，请参阅[承载](../../fundamentals/hosting.md)。</span><span class="sxs-lookup"><span data-stu-id="24e91-213">For more information about these methods, see [Hosting](../../fundamentals/hosting.md).</span></span> <span data-ttu-id="24e91-214">要了解使用 IIS 作为反向代理时 URL 绑定的工作原理，请参阅 [ASP.NET Core 模块](aspnet-core-module.md)。</span><span class="sxs-lookup"><span data-stu-id="24e91-214">For information about how URL binding works when you use IIS as a reverse proxy, see [ASP.NET Core Module](aspnet-core-module.md).</span></span> 

---

### <a name="url-prefixes"></a><span data-ttu-id="24e91-215">URL 前缀</span><span class="sxs-lookup"><span data-stu-id="24e91-215">URL prefixes</span></span>

<span data-ttu-id="24e91-216">如果调用 `UseUrls` 或使用 `urls` 命令行参数或 ASPNETCORE_URLS 环境变量，URL 前缀可采用以下任意格式。</span><span class="sxs-lookup"><span data-stu-id="24e91-216">If you call `UseUrls` or use the `urls` command-line argument or ASPNETCORE_URLS environment variable, the URL prefixes can be in any of the following formats.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-217">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-217">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="24e91-218">仅 HTTP URL 前缀有效；使用 `UseUrls` 配置 URL 绑定时，Kestrel 不支持 SSL。</span><span class="sxs-lookup"><span data-stu-id="24e91-218">Only HTTP URL prefixes are valid; Kestrel doesn't support SSL when you configure URL bindings by using `UseUrls`.</span></span>

* <span data-ttu-id="24e91-219">包含端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="24e91-219">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="24e91-220">0.0.0.0 是一种绑定到所有 IPv4 地址的特殊情况。</span><span class="sxs-lookup"><span data-stu-id="24e91-220">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="24e91-221">包含端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="24e91-221">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  ```

  <span data-ttu-id="24e91-222">[::] 是 IPv4 0.0.0.0 的 IPv6 等效项。</span><span class="sxs-lookup"><span data-stu-id="24e91-222">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="24e91-223">包含端口号的主机名</span><span class="sxs-lookup"><span data-stu-id="24e91-223">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="24e91-224">主机名、\* 和 + 并不特殊。</span><span class="sxs-lookup"><span data-stu-id="24e91-224">Host names, \*, and +, are not special.</span></span> <span data-ttu-id="24e91-225">不是已识别 IP 地址或“localhost”的任何内容都将绑定到所有 IPv4 和 IPv6 IP。</span><span class="sxs-lookup"><span data-stu-id="24e91-225">Anything that's not a recognized IP address or "localhost" will bind to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="24e91-226">如果需要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用程序，请使用 [HTTP.sys](httpsys.md) 或 IIS、Nginx 或 Apache 等反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="24e91-226">If you need to bind different host names to different ASP.NET Core applications on the same port, use [HTTP.sys](httpsys.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="24e91-227">包含端口号的“Localhost”名称或包含端口号的环回 IP</span><span class="sxs-lookup"><span data-stu-id="24e91-227">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="24e91-228">指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。</span><span class="sxs-lookup"><span data-stu-id="24e91-228">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="24e91-229">如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="24e91-229">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="24e91-230">如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="24e91-230">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-231">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-231">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="24e91-232">包含端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="24e91-232">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="24e91-233">0.0.0.0 是一种绑定到所有 IPv4 地址的特殊情况。</span><span class="sxs-lookup"><span data-stu-id="24e91-233">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="24e91-234">包含端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="24e91-234">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  https://[0:0:0:0:0:ffff:4137:270a]:443/ 
  ```

  <span data-ttu-id="24e91-235">[::] 是 IPv4 0.0.0.0 的 IPv6 等效项。</span><span class="sxs-lookup"><span data-stu-id="24e91-235">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="24e91-236">包含端口号的主机名</span><span class="sxs-lookup"><span data-stu-id="24e91-236">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="24e91-237">主机名、\* 和 + 并不特殊。</span><span class="sxs-lookup"><span data-stu-id="24e91-237">Host names, \*, and + aren't special.</span></span> <span data-ttu-id="24e91-238">不是已识别 IP 地址或“localhost”的任何内容都将绑定到所有 IPv4 和 IPv6 IP。</span><span class="sxs-lookup"><span data-stu-id="24e91-238">Anything that isn't a recognized IP address or "localhost" binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="24e91-239">如果需要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用程序，请使用 [WebListener](weblistener.md) 或 IIS、Nginx 或 Apache 等反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="24e91-239">If you need to bind different host names to different ASP.NET Core applications on the same port, use [WebListener](weblistener.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="24e91-240">包含端口号的“Localhost”名称或包含端口号的环回 IP</span><span class="sxs-lookup"><span data-stu-id="24e91-240">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="24e91-241">指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。</span><span class="sxs-lookup"><span data-stu-id="24e91-241">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="24e91-242">如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="24e91-242">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="24e91-243">如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="24e91-243">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

* <span data-ttu-id="24e91-244">Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="24e91-244">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock  
  ```

<span data-ttu-id="24e91-245">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="24e91-245">**Port 0**</span></span>

<span data-ttu-id="24e91-246">如果指定端口号 0，Kestrel 将动态绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="24e91-246">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="24e91-247">除 `localhost` 名称外，任何主机名或 IP 都可绑定到端口 0。</span><span class="sxs-lookup"><span data-stu-id="24e91-247">Binding to port 0 is allowed for any host name or IP except for `localhost` name.</span></span>

<span data-ttu-id="24e91-248">以下示例演示如何确定 Kestrel 在运行时实际绑定到的端口：</span><span class="sxs-lookup"><span data-stu-id="24e91-248">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample1/Startup.cs?name=snippet_Configure)]

<span data-ttu-id="24e91-249">**SSL 的 URL 前缀**</span><span class="sxs-lookup"><span data-stu-id="24e91-249">**URL prefixes for SSL**</span></span>

<span data-ttu-id="24e91-250">如果调用 `UseHttps` 扩展方法，请务必在 URL 前缀中包括 `https:`，如下所示。</span><span class="sxs-lookup"><span data-stu-id="24e91-250">Be sure to include URL prefixes with `https:` if you call the `UseHttps` extension method, as shown below.</span></span>

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
> <span data-ttu-id="24e91-251">不能在相同端口上托管 HTTPS 和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="24e91-251">HTTPS and HTTP cannot be hosted on the same port.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

---
## <a name="next-steps"></a><span data-ttu-id="24e91-252">后续步骤</span><span class="sxs-lookup"><span data-stu-id="24e91-252">Next steps</span></span>

<span data-ttu-id="24e91-253">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="24e91-253">For more information, see the following resources:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="24e91-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="24e91-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* [<span data-ttu-id="24e91-255">针对 2.x 的示例应用</span><span class="sxs-lookup"><span data-stu-id="24e91-255">Sample app for 2.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)
* [<span data-ttu-id="24e91-256">Kestrel 源代码</span><span class="sxs-lookup"><span data-stu-id="24e91-256">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="24e91-257">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="24e91-257">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* [<span data-ttu-id="24e91-258">针对 1.x 的示例应用</span><span class="sxs-lookup"><span data-stu-id="24e91-258">Sample app for 1.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)
* [<span data-ttu-id="24e91-259">Kestrel 源代码</span><span class="sxs-lookup"><span data-stu-id="24e91-259">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

---
