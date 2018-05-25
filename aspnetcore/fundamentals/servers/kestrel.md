---
title: ASP.NET Core 中的 Kestrel Web 服务器实现
author: rick-anderson
description: 了解跨平台 ASP.NET Core Web 服务器 Kestrel。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/02/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: 251385b268e75cfadb815c293be52176297ed3e4
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="701c3-103">ASP.NET Core 中的 Kestrel Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="701c3-103">Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="701c3-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Chris Ross](https://github.com/Tratcher) 和 [Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="701c3-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="701c3-105">Kestrel 是一个跨平台的[适用于 ASP.NET Core 的 Web 服务器](xref:fundamentals/servers/index)。</span><span class="sxs-lookup"><span data-stu-id="701c3-105">Kestrel is a cross-platform [web server for ASP.NET Core](xref:fundamentals/servers/index).</span></span> <span data-ttu-id="701c3-106">Kestrel 是 Web 服务器，默认包括在 ASP.NET Core 项目模板中。</span><span class="sxs-lookup"><span data-stu-id="701c3-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span>

<span data-ttu-id="701c3-107">Kestrel 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="701c3-107">Kestrel supports the following features:</span></span>

* <span data-ttu-id="701c3-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="701c3-108">HTTPS</span></span>
* <span data-ttu-id="701c3-109">用于启用 [WebSocket](https://github.com/aspnet/websockets) 的不透明升级</span><span class="sxs-lookup"><span data-stu-id="701c3-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
* <span data-ttu-id="701c3-110">用于获得 Nginx 高性能的 Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="701c3-110">Unix sockets for high performance behind Nginx</span></span>

<span data-ttu-id="701c3-111">.NET Core 支持的所有平台和版本均支持 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

<span data-ttu-id="701c3-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="701c3-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="701c3-113">何时结合使用 Kestrel 和反向代理</span><span class="sxs-lookup"><span data-stu-id="701c3-113">When to use Kestrel with a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="701c3-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="701c3-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="701c3-115">可以单独使用 Kestrel，也可以将其与反向代理服务器（如 IIS、Nginx 或 Apache）结合使用。</span><span class="sxs-lookup"><span data-stu-id="701c3-115">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="701c3-116">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-116">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 直接与 Internet 通信，不使用反向代理服务器](kestrel/_static/kestrel-to-internet2.png)

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="701c3-119">建议通过反向代理服务器使用 Kestrel，除非 Kestrel 只对内部网络公开。</span><span class="sxs-lookup"><span data-stu-id="701c3-119">We recommend using Kestrel with a reverse proxy server unless Kestrel is only exposed to an internal network.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="701c3-120">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="701c3-120">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="701c3-121">如果应用仅接受来自内部网络的请求，则可以将 Kestrel 直接用作该应用的服务器。</span><span class="sxs-lookup"><span data-stu-id="701c3-121">If an app accepts requests only from an internal network, Kestrel can be used directly as the app's server.</span></span>

![Kestrel 直接与你的内部网络进行通信](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="701c3-123">如果将应用公开到 Internet，则将 IIS、Nginx 或 Apache 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="701c3-123">If you expose your app to the Internet, use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="701c3-124">反向代理服务器接收到来自 Internet 的 HTTP 请求，并在进行一些初步处理后将这些请求转发到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-124">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel 通过反向代理服务器（如 IIS、Nginx 或 Apache）间接与 Internet 进行通信](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="701c3-126">出于安全考虑，边缘部署需要使用反向代理（从 Internet 公开到流量）。</span><span class="sxs-lookup"><span data-stu-id="701c3-126">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="701c3-127">Kestrel 的 1.x 版本没有防御攻击的完整补充，例如适当的超时、大小限制以及并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="701c3-127">The 1.x versions of Kestrel don't have a full complement of defenses against attacks, such as appropriate timeouts, size limits, and concurrent connection limits.</span></span>

---

<span data-ttu-id="701c3-128">具有共享在单个服务器上运行的相同 IP 和端口的多个应用时，需要一个反向代理方案。</span><span class="sxs-lookup"><span data-stu-id="701c3-128">A reverse proxy scenario exists when there are multiple apps that share the same IP and port running on a single server.</span></span> <span data-ttu-id="701c3-129">Kestrel 不支持此方案，因为 Kestrel 不支持在多个进程之间共享相同的 IP 和端口。</span><span class="sxs-lookup"><span data-stu-id="701c3-129">Kestrel doesn't support this scenario because Kestrel doesn't support sharing the same IP and port among multiple processes.</span></span> <span data-ttu-id="701c3-130">如果将 Kestrel 配置为侦听某个端口，Kestrel 会处理该端口的所有流量（无视请求的主机标头）。</span><span class="sxs-lookup"><span data-stu-id="701c3-130">When Kestrel is configured to listen on a port, Kestrel handles all of the traffic for that port regardless of requests' host header.</span></span> <span data-ttu-id="701c3-131">可以共享端口的反向代理能在唯一的 IP 和端口上将请求转发至 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-131">A reverse proxy that can share ports has the ability to forward requests to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="701c3-132">即使不需要反向代理服务器，使用反向代理服务器可能也是个不错的选择：</span><span class="sxs-lookup"><span data-stu-id="701c3-132">Even if a reverse proxy server isn't required, using a reverse proxy server might be a good choice:</span></span>

* <span data-ttu-id="701c3-133">它可以限制所承载的应用中的公开的公共外围应用。</span><span class="sxs-lookup"><span data-stu-id="701c3-133">It can limit the exposed public surface area of the apps that it hosts.</span></span>
* <span data-ttu-id="701c3-134">它可以提供额外的配置和防护层。</span><span class="sxs-lookup"><span data-stu-id="701c3-134">It provides an additional layer of configuration and defense.</span></span>
* <span data-ttu-id="701c3-135">它可以更好地与现有基础结构集成。</span><span class="sxs-lookup"><span data-stu-id="701c3-135">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="701c3-136">它可以简化负载均衡和 SSL 配置。</span><span class="sxs-lookup"><span data-stu-id="701c3-136">It simplifies load balancing and SSL configuration.</span></span> <span data-ttu-id="701c3-137">仅反向代理服务器需要 SSL 证书，并且该服务器可使用普通 HTTP 在内部网络上与应用服务器通信。</span><span class="sxs-lookup"><span data-stu-id="701c3-137">Only the reverse proxy server requires an SSL certificate, and that server can communicate with your app servers on the internal network using plain HTTP.</span></span>

> [!WARNING]
> <span data-ttu-id="701c3-138">如果在启用了主机筛选的情况下不使用反向代理，则必须启用[“主机筛选”](#host-filtering)。</span><span class="sxs-lookup"><span data-stu-id="701c3-138">If not using a reverse proxy with host filtering enabled, [host filtering](#host-filtering) must be enabled.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="701c3-139">如何在 ASP.NET Core 应用中使用 Kestrel</span><span class="sxs-lookup"><span data-stu-id="701c3-139">How to use Kestrel in ASP.NET Core apps</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="701c3-140">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="701c3-140">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="701c3-141">[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中包括 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 包。</span><span class="sxs-lookup"><span data-stu-id="701c3-141">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="701c3-142">默认情况下，ASP.NET Core 项目模板使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-142">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="701c3-143">在 Program.cs 中，模板代码调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)，后者在后台调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel)。</span><span class="sxs-lookup"><span data-stu-id="701c3-143">In *Program.cs*, the template code calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), which calls [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) behind the scenes.</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="701c3-144">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="701c3-144">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="701c3-145">安装 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="701c3-145">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="701c3-146">在 `Main` 方法中的 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1) 上调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 扩展方法，指定所需的任何 [Kestrel 选项](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)，如下一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="701c3-146">Call the [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) extension method on [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1) in the `Main` method, specifying any [Kestrel options](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1) required, as shown in the next section.</span></span>

[!code-csharp[](kestrel/samples/1.x/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a><span data-ttu-id="701c3-147">Kestrel 选项</span><span class="sxs-lookup"><span data-stu-id="701c3-147">Kestrel options</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="701c3-148">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="701c3-148">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="701c3-149">Kestrel Web 服务器具有约束配置选项，这些选项在面向 Internet 的部署中尤其有用。</span><span class="sxs-lookup"><span data-stu-id="701c3-149">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="701c3-150">可以自定义的一些重要限制：</span><span class="sxs-lookup"><span data-stu-id="701c3-150">A few important limits that can be customized:</span></span>

* <span data-ttu-id="701c3-151">客户端最大连接数</span><span class="sxs-lookup"><span data-stu-id="701c3-151">Maximum client connections</span></span>
* <span data-ttu-id="701c3-152">请求正文最大大小</span><span class="sxs-lookup"><span data-stu-id="701c3-152">Maximum request body size</span></span>
* <span data-ttu-id="701c3-153">请求正文最小数据速率</span><span class="sxs-lookup"><span data-stu-id="701c3-153">Minimum request body data rate</span></span>

<span data-ttu-id="701c3-154">可在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 类的 [Limits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) 属性上设置这些约束和其他约束。</span><span class="sxs-lookup"><span data-stu-id="701c3-154">Set these and other constraints on the [Limits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) property of the [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) class.</span></span> <span data-ttu-id="701c3-155">`Limits` 属性包含 [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) 类的实例。</span><span class="sxs-lookup"><span data-stu-id="701c3-155">The `Limits` property holds an instance of the [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) class.</span></span>

<span data-ttu-id="701c3-156">**客户端最大连接数**</span><span class="sxs-lookup"><span data-stu-id="701c3-156">**Maximum client connections**</span></span>

[<span data-ttu-id="701c3-157">MaxConcurrentConnections</span><span class="sxs-lookup"><span data-stu-id="701c3-157">MaxConcurrentConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentconnections)  
[<span data-ttu-id="701c3-158">MaxConcurrentUpgradedConnections</span><span class="sxs-lookup"><span data-stu-id="701c3-158">MaxConcurrentUpgradedConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentupgradedconnections)

<span data-ttu-id="701c3-159">可使用以下代码为整个应用设置并发打开的最大 TCP 连接数：</span><span class="sxs-lookup"><span data-stu-id="701c3-159">The maximum number of concurrent open TCP connections can be set for the entire app with the following code:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=3)]

<span data-ttu-id="701c3-160">对于已从 HTTP 或 HTTPS 升级到另一个协议（例如，Websocket 请求）的连接，有一个单独的限制。</span><span class="sxs-lookup"><span data-stu-id="701c3-160">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="701c3-161">连接升级后，不会计入 `MaxConcurrentConnections` 限制。</span><span class="sxs-lookup"><span data-stu-id="701c3-161">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=4)]

<span data-ttu-id="701c3-162">默认情况下，最大连接数不受限制 (NULL)。</span><span class="sxs-lookup"><span data-stu-id="701c3-162">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="701c3-163">**请求正文最大大小**</span><span class="sxs-lookup"><span data-stu-id="701c3-163">**Maximum request body size**</span></span>

[<span data-ttu-id="701c3-164">MaxRequestBodySize</span><span class="sxs-lookup"><span data-stu-id="701c3-164">MaxRequestBodySize</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)

<span data-ttu-id="701c3-165">默认的请求正文最大大小为 30,000,000 字节，大约 28.6 MB。</span><span class="sxs-lookup"><span data-stu-id="701c3-165">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6 MB.</span></span>

<span data-ttu-id="701c3-166">在 ASP.NET Core MVC 应用中替代限制的推荐方法是在操作方法上使用 [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 属性：</span><span class="sxs-lookup"><span data-stu-id="701c3-166">The recommended approach to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="701c3-167">以下示例演示如何为每个请求上的应用配置约束：</span><span class="sxs-lookup"><span data-stu-id="701c3-167">Here's an example that shows how to configure the constraint for the app on every request:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="701c3-168">可在中间件中替代特定请求的设置：</span><span class="sxs-lookup"><span data-stu-id="701c3-168">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="701c3-169">如果在应用开始读取请求后尝试配置请求限制，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="701c3-169">An exception is thrown if you attempt to configure the limit on a request after the app has started to read the request.</span></span> <span data-ttu-id="701c3-170">`IsReadOnly` 属性指示 `MaxRequestBodySize` 属性处于只读状态，意味已经无法再配置限制。</span><span class="sxs-lookup"><span data-stu-id="701c3-170">There's an `IsReadOnly` property that indicates if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="701c3-171">**请求正文最小数据速率**</span><span class="sxs-lookup"><span data-stu-id="701c3-171">**Minimum request body data rate**</span></span>

[<span data-ttu-id="701c3-172">MinRequestBodyDataRate</span><span class="sxs-lookup"><span data-stu-id="701c3-172">MinRequestBodyDataRate</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minrequestbodydatarate)  
[<span data-ttu-id="701c3-173">MinResponseDataRate</span><span class="sxs-lookup"><span data-stu-id="701c3-173">MinResponseDataRate</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minresponsedatarate)

<span data-ttu-id="701c3-174">Kestrel 每秒检查一次数据是否以指定的速率（字节/秒）传入。</span><span class="sxs-lookup"><span data-stu-id="701c3-174">Kestrel checks every second if data is arriving at the specified rate in bytes/second.</span></span> <span data-ttu-id="701c3-175">如果速率低于最小值，则连接超时。宽限期是 Kestrel 提供给客户端用于将其发送速率提升到最小值的时间量；在此期间不会检查速率。</span><span class="sxs-lookup"><span data-stu-id="701c3-175">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="701c3-176">宽限期有助于避免最初由于 TCP 慢启动而以较慢速率发送数据的连接中断。</span><span class="sxs-lookup"><span data-stu-id="701c3-176">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="701c3-177">默认的最小速率为 240 字节/秒，包含 5 秒的宽限期。</span><span class="sxs-lookup"><span data-stu-id="701c3-177">The default minimum rate is 240 bytes/second with a 5 second grace period.</span></span>

<span data-ttu-id="701c3-178">最小速率也适用于响应。</span><span class="sxs-lookup"><span data-stu-id="701c3-178">A minimum rate also applies to the response.</span></span> <span data-ttu-id="701c3-179">除了属性和接口名称中具有 `RequestBody` 或 `Response` 以外，用于设置请求限制和响应限制的代码相同。</span><span class="sxs-lookup"><span data-stu-id="701c3-179">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span>

<span data-ttu-id="701c3-180">以下示例演示如何在 Program.cs 中配置最小数据速率：</span><span class="sxs-lookup"><span data-stu-id="701c3-180">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=6-7)]

<span data-ttu-id="701c3-181">可在中间件中配置每个请求的速率：</span><span class="sxs-lookup"><span data-stu-id="701c3-181">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="701c3-182">有关其他 Kestrel 选项和限制的信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="701c3-182">For information about other Kestrel options and limits, see:</span></span>

* [<span data-ttu-id="701c3-183">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="701c3-183">KestrelServerOptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)
* [<span data-ttu-id="701c3-184">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="701c3-184">KestrelServerLimits</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits)
* [<span data-ttu-id="701c3-185">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="701c3-185">ListenOptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="701c3-186">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="701c3-186">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="701c3-187">有关 Kestrel 选项和限制的信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="701c3-187">For information about Kestrel options and limits, see:</span></span>

* [<span data-ttu-id="701c3-188">KestrelServerOptions 类</span><span class="sxs-lookup"><span data-stu-id="701c3-188">KestrelServerOptions class</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)
* [<span data-ttu-id="701c3-189">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="701c3-189">KestrelServerLimits</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserverlimits?view=aspnetcore-1.1)

---

### <a name="endpoint-configuration"></a><span data-ttu-id="701c3-190">终结点配置</span><span class="sxs-lookup"><span data-stu-id="701c3-190">Endpoint configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="701c3-191">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="701c3-191">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

::: moniker range="= aspnetcore-2.0"
<span data-ttu-id="701c3-192">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="701c3-192">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="701c3-193">在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 上调用 [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 或 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 方法，从而配置 Kestrel 的 URL 前缀和端口。</span><span class="sxs-lookup"><span data-stu-id="701c3-193">Call [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) or [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) methods on [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) to configure URL prefixes and ports for Kestrel.</span></span> <span data-ttu-id="701c3-194">`UseUrls`、`--urls` 命令行参数、`urls` 主机配置键以及 `ASPNETCORE_URLS` 环境变量也有用，但具有本节后面注明的限制。</span><span class="sxs-lookup"><span data-stu-id="701c3-194">`UseUrls`, the `--urls` command-line argument, `urls` host configuration key, and the `ASPNETCORE_URLS` environment variable also work but have the limitations noted later in this section.</span></span>

<span data-ttu-id="701c3-195">`urls` 主机配置键必须来自主机配置，而不是应用配置。</span><span class="sxs-lookup"><span data-stu-id="701c3-195">The `urls` host configuration key must come from the host configuration, not the app configuration.</span></span> <span data-ttu-id="701c3-196">将 `urls` 键和值添加到 appsettings.json 不影响主机配置，因为是在从配置文件读取配置时对主机进行完全初始化的。</span><span class="sxs-lookup"><span data-stu-id="701c3-196">Adding a `urls` key and value to *appsettings.json* doesn't affect host configuration because the host is completely initialized by the time the configuration is read from the configuration file.</span></span> <span data-ttu-id="701c3-197">但是，在主机生成器上可以使用 appsettings.json 中的 `urls` 键以及 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 来配置主机：</span><span class="sxs-lookup"><span data-stu-id="701c3-197">However, a `urls` key in *appsettings.json* can be used with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) on the host builder to configure the host:</span></span>

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appSettings.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseKestrel()
    .UseConfiguration(config)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseStartup<Startup>()
    .Build();
```

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="701c3-198">默认情况下，ASP.NET Core 绑定到：</span><span class="sxs-lookup"><span data-stu-id="701c3-198">By default, ASP.NET Core binds to:</span></span>

* `http://localhost:5000`
* <span data-ttu-id="701c3-199">`https://localhost:5001`（存在本地开发证书时）</span><span class="sxs-lookup"><span data-stu-id="701c3-199">`https://localhost:5001` (when a local development certificate is present)</span></span>

<span data-ttu-id="701c3-200">开发证书会创建于以下情况：</span><span class="sxs-lookup"><span data-stu-id="701c3-200">A development certificate is created:</span></span>

* <span data-ttu-id="701c3-201">安装了 [.NET Core SDK](/dotnet/core/sdk) 时。</span><span class="sxs-lookup"><span data-stu-id="701c3-201">When the [.NET Core SDK](/dotnet/core/sdk) is installed.</span></span>
* <span data-ttu-id="701c3-202">[dev-certs tool](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-dev-certs) 用于创建证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-202">The [dev-certs tool](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-dev-certs) is used to create a certificate.</span></span>

<span data-ttu-id="701c3-203">部分浏览器需要获取信任本地开发证书的显示权限。</span><span class="sxs-lookup"><span data-stu-id="701c3-203">Some browsers require that you grant explicit permission to the browser to trust the local development certificate.</span></span>

<span data-ttu-id="701c3-204">ASP.NET Core 2.1 及更高版本的项目模板将应用配置为默认情况下在 HTTPS 上运行，并包括 [HTTPS 重定向和 HSTS 支持](xref:security/enforcing-ssl)。</span><span class="sxs-lookup"><span data-stu-id="701c3-204">ASP.NET Core 2.1 and later project templates configure apps to run on HTTPS by default and include [HTTPS redirection and HSTS support](xref:security/enforcing-ssl).</span></span>

<span data-ttu-id="701c3-205">在 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 上调用 [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 或 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 方法，从而配置 Kestrel 的 URL 前缀和端口。</span><span class="sxs-lookup"><span data-stu-id="701c3-205">Call [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) or [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) methods on [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) to configure URL prefixes and ports for Kestrel.</span></span>

<span data-ttu-id="701c3-206">`UseUrls`、`--urls` 命令行参数、`urls` 主机配置键以及 `ASPNETCORE_URLS` 环境变量也有用，但具有本节后面注明的限制（必须要有可用于 HTTPS 终结点配置的默认证书）。</span><span class="sxs-lookup"><span data-stu-id="701c3-206">`UseUrls`, the `--urls` command-line argument, `urls` host configuration key, and the `ASPNETCORE_URLS` environment variable also work but have the limitations noted later in this section (a default certificate must be available for HTTPS endpoint configuration).</span></span>

<span data-ttu-id="701c3-207">ASP.NET Core 2.1 `KestrelServerOptions` 配置：</span><span class="sxs-lookup"><span data-stu-id="701c3-207">ASP.NET Core 2.1 `KestrelServerOptions` configuration:</span></span>

<span data-ttu-id="701c3-208">**ConfigureEndpointDefaults(Action&lt;ListenOptions&gt;)**</span><span class="sxs-lookup"><span data-stu-id="701c3-208">**ConfigureEndpointDefaults(Action&lt;ListenOptions&gt;)**</span></span>  
<span data-ttu-id="701c3-209">指定一个为每个指定的终结点运行的配置 `Action`。</span><span class="sxs-lookup"><span data-stu-id="701c3-209">Specifies a configuration `Action` to run for each specified endpoint.</span></span> <span data-ttu-id="701c3-210">多次调用 `ConfigureEndpointDefaults`，用最新指定的 `Action` 替换之前的 `Action`。</span><span class="sxs-lookup"><span data-stu-id="701c3-210">Calling `ConfigureEndpointDefaults` multiple times replaces prior `Action`s with the last `Action` specified.</span></span>

<span data-ttu-id="701c3-211">**ConfigureHttpsDefaults(Action&lt;HttpsConnectionAdapterOptions&gt;)**</span><span class="sxs-lookup"><span data-stu-id="701c3-211">**ConfigureHttpsDefaults(Action&lt;HttpsConnectionAdapterOptions&gt;)**</span></span>  
<span data-ttu-id="701c3-212">指定一个为每个 HTTPS 终结点运行的配置 `Action`。</span><span class="sxs-lookup"><span data-stu-id="701c3-212">Specifies a configuration `Action` to run for each HTTPS endpoint.</span></span> <span data-ttu-id="701c3-213">多次调用 `ConfigureHttpsDefaults`，用最新指定的 `Action` 替换之前的 `Action`。</span><span class="sxs-lookup"><span data-stu-id="701c3-213">Calling `ConfigureHttpsDefaults` multiple times replaces prior `Action`s with the last `Action` specified.</span></span>

<span data-ttu-id="701c3-214">**Configure(IConfiguration)**</span><span class="sxs-lookup"><span data-stu-id="701c3-214">**Configure(IConfiguration)**</span></span>  
<span data-ttu-id="701c3-215">创建配置加载程序，用于设置将 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) 作为输入的 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="701c3-215">Creates a configuration loader for setting up Kestrel that takes an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) as input.</span></span> <span data-ttu-id="701c3-216">配置必须针对 Kestrel 的配置节。</span><span class="sxs-lookup"><span data-stu-id="701c3-216">The configuration must be scoped to the configuration section for Kestrel.</span></span>

<span data-ttu-id="701c3-217">**ListenOptions.UseHttps**</span><span class="sxs-lookup"><span data-stu-id="701c3-217">**ListenOptions.UseHttps**</span></span>  
<span data-ttu-id="701c3-218">将 Kestrel 配置为使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="701c3-218">Configure Kestrel to use HTTPS.</span></span>

<span data-ttu-id="701c3-219">`ListenOptions.UseHttps` 扩展：</span><span class="sxs-lookup"><span data-stu-id="701c3-219">`ListenOptions.UseHttps` extensions:</span></span>

* <span data-ttu-id="701c3-220">`UseHttps` &ndash; 将 Kestrel 配置为使用 HTTPS，采用默认证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-220">`UseHttps` &ndash; Configure Kestrel to use HTTPS with the default certificate.</span></span> <span data-ttu-id="701c3-221">如果没有配置默认证书，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="701c3-221">Throws an exception if no default certificate is configured.</span></span>
* `UseHttps(string fileName)`
* `UseHttps(string fileName, string password)`
* `UseHttps(string fileName, string password, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(StoreName storeName, string subject)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(X509Certificate2 serverCertificate)`
* `UseHttps(X509Certificate2 serverCertificate, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(Action<HttpsConnectionAdapterOptions> configureOptions)`

<span data-ttu-id="701c3-222">`ListenOptions.UseHttps` 参数：</span><span class="sxs-lookup"><span data-stu-id="701c3-222">`ListenOptions.UseHttps` parameters:</span></span>

* <span data-ttu-id="701c3-223">`filename` 是证书文件的路径和文件名，关联包含应用内容文件的目录。</span><span class="sxs-lookup"><span data-stu-id="701c3-223">`filename` is the path and file name of a certificate file, relative to the directory that contains the app's content files.</span></span>
* <span data-ttu-id="701c3-224">`password` 是访问 X.509 证书数据所需的密码。</span><span class="sxs-lookup"><span data-stu-id="701c3-224">`password` is the password required to access the X.509 certificate data.</span></span>
* <span data-ttu-id="701c3-225">`configureOptions` 是配置 `HttpsConnectionAdapterOptions` 的 `Action`。</span><span class="sxs-lookup"><span data-stu-id="701c3-225">`configureOptions` is an `Action` to configure the `HttpsConnectionAdapterOptions`.</span></span> <span data-ttu-id="701c3-226">返回 `ListenOptions`。</span><span class="sxs-lookup"><span data-stu-id="701c3-226">Returns the `ListenOptions`.</span></span>
* <span data-ttu-id="701c3-227">`storeName` 是从中加载证书的证书存储。</span><span class="sxs-lookup"><span data-stu-id="701c3-227">`storeName` is the certificate store from which to load the certificate.</span></span>
* <span data-ttu-id="701c3-228">`subject` 是证书的主题名称。</span><span class="sxs-lookup"><span data-stu-id="701c3-228">`subject` is the subject name for the certificate.</span></span>
* <span data-ttu-id="701c3-229">`allowInvalid` 指示是否存在需要留意的无效证书，例如自签名证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-229">`allowInvalid` indicates if invalid certificates should be considered, such as self-signed certificates.</span></span>
* <span data-ttu-id="701c3-230">`location` 是从中加载证书的存储位置。</span><span class="sxs-lookup"><span data-stu-id="701c3-230">`location` is the store location to load the certificate from.</span></span>
* <span data-ttu-id="701c3-231">`serverCertificate` 是 X.509 证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-231">`serverCertificate` is the X.509 certificate.</span></span>

<span data-ttu-id="701c3-232">在生产中，必须显式配置 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="701c3-232">In production, HTTPS must be explicitly configured.</span></span> <span data-ttu-id="701c3-233">至少必须提供默认证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-233">At a minimum, a default certificate must be provided.</span></span>

<span data-ttu-id="701c3-234">下面要描述的支持的配置：</span><span class="sxs-lookup"><span data-stu-id="701c3-234">Supported configurations described next:</span></span>

* <span data-ttu-id="701c3-235">无配置</span><span class="sxs-lookup"><span data-stu-id="701c3-235">No configuration</span></span>
* <span data-ttu-id="701c3-236">从配置中替换默认证书</span><span class="sxs-lookup"><span data-stu-id="701c3-236">Replace the default certificate from configuration</span></span>
* <span data-ttu-id="701c3-237">更改代码中的默认值</span><span class="sxs-lookup"><span data-stu-id="701c3-237">Change the defaults in code</span></span>

<span data-ttu-id="701c3-238">*无配置*</span><span class="sxs-lookup"><span data-stu-id="701c3-238">*No configuration*</span></span>

<span data-ttu-id="701c3-239">Kestrel 在 `http://localhost:5000` 和 `https://localhost:5001` 上进行侦听（如果默认证书可用）。</span><span class="sxs-lookup"><span data-stu-id="701c3-239">Kestrel listens on `http://localhost:5000` and `https://localhost:5001` (if a default cert is available).</span></span>

<span data-ttu-id="701c3-240">使用以下内容指定 URL：</span><span class="sxs-lookup"><span data-stu-id="701c3-240">Specify URLs using the:</span></span>

* <span data-ttu-id="701c3-241">`ASPNETCORE_URLS` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="701c3-241">`ASPNETCORE_URLS` environment variable.</span></span>
* <span data-ttu-id="701c3-242">`--urls` 命令行参数。</span><span class="sxs-lookup"><span data-stu-id="701c3-242">`--urls` command-line argument.</span></span>
* <span data-ttu-id="701c3-243">`urls` 主机配置键。</span><span class="sxs-lookup"><span data-stu-id="701c3-243">`urls` host configuration key.</span></span>
* <span data-ttu-id="701c3-244">`UseUrls` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="701c3-244">`UseUrls` extension method.</span></span>

<span data-ttu-id="701c3-245">有关详细信息，请参阅[服务器 URL](xref:fundamentals/host/web-host#server-urls) 和[重写配置](xref:fundamentals/host/web-host#override-configuration)。</span><span class="sxs-lookup"><span data-stu-id="701c3-245">For more information, see [Server URLs](xref:fundamentals/host/web-host#server-urls) and [Override configuration](xref:fundamentals/host/web-host#override-configuration).</span></span>

<span data-ttu-id="701c3-246">采用这些方法提供的值可以是一个或多个 HTTP 和 HTTPS 终结点（如果默认证书可用，则为 HTTPS）。</span><span class="sxs-lookup"><span data-stu-id="701c3-246">The value provided using these approaches can be one or more HTTP and HTTPS endpoints (HTTPS if a default cert is available).</span></span> <span data-ttu-id="701c3-247">将值配置为以分号分隔的列表（例如 `"Urls": "http://localhost:8000;http://localhost:8001"`）。</span><span class="sxs-lookup"><span data-stu-id="701c3-247">Configure the value as a semicolon-separated list (for example, `"Urls": "http://localhost:8000;http://localhost:8001"`).</span></span>

<span data-ttu-id="701c3-248">*从配置中替换默认证书*</span><span class="sxs-lookup"><span data-stu-id="701c3-248">*Replace the default certificate from configuration*</span></span>

<span data-ttu-id="701c3-249">[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 在默认情况下调用 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 来加载 Kestrel 配置。</span><span class="sxs-lookup"><span data-stu-id="701c3-249">[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) calls `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` by default to load Kestrel configuration.</span></span> <span data-ttu-id="701c3-250">Kestrel 可以使用默认 HTTPS 应用设置配置架构。</span><span class="sxs-lookup"><span data-stu-id="701c3-250">A default HTTPS app settings configuration schema is available for Kestrel.</span></span> <span data-ttu-id="701c3-251">从磁盘上的文件或从证书存储中配置多个终结点，包括要使用的 URL 和证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-251">Configure multiple endpoints, including the URLs and the certificates to use, either from a file on disk or from a certificate store.</span></span>

<span data-ttu-id="701c3-252">在以下 appsettings.json 示例中：</span><span class="sxs-lookup"><span data-stu-id="701c3-252">In the following *appsettings.json* example:</span></span>

* <span data-ttu-id="701c3-253">将 AllowInvalid 设置为 `true`，从而允许使用无效证书（例如自签名证书）。</span><span class="sxs-lookup"><span data-stu-id="701c3-253">Set **AllowInvalid** to `true` to permit the use of invalid certificates (for example, self-signed certificates).</span></span>
* <span data-ttu-id="701c3-254">任何未指定证书的 HTTPS 终结点（下例中的 HttpsDefaultCert）会回退至在 Certificates > Default 下定义的证书或开发证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-254">Any HTTPS endpoint that doesn't specify a certificate (**HttpsDefaultCert** in the example that follows) falls back to the cert defined under **Certificates** > **Default** or the development certificate.</span></span>

```json
{
"Kestrel": {
  "EndPoints": {
    "Http": {
      "Url": "http://localhost:5000"
    },

    "HttpsInlineCertFile": {
      "Url": "https://localhost:5001",
      "Certificate": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    },

    "HttpsInlineCertStore": {
      "Url": "https://localhost:5002",
      "Certificate": {
        "Subject": "<subject; required>",
        "Store": "<certificate store; defaults to My>",
        "Location": "<location; defaults to CurrentUser>",
        "AllowInvalid": "<true or false; defaults to false>"
      }
    },

    "HttpsDefaultCert": {
      "Url": "https://localhost:5003"
    },

    "Https": {
      "Url": "https://*:5004",
      "Certificate": {
      "Path": "<path to .pfx file>",
      "Password": "<certificate password>"
      }
    }
    },
    "Certificates": {
      "Default": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    }
  }
}
```

<span data-ttu-id="701c3-255">此外还可以使用任何证书节点的 Path 和 Password，采用证书存储字段指定证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-255">An alternative to using **Path** and **Password** for any certificate node is to specify the certificate using certificate store fields.</span></span> <span data-ttu-id="701c3-256">例如，可将 Certificates > Default 证书指定为：</span><span class="sxs-lookup"><span data-stu-id="701c3-256">For example, the **Certificates** > **Default** certificate can be specified as:</span></span>

```json
"Default": {
  "Subject": "<subject; required>",
  "Store": "<cert store; defaults to My>",
  "Location": "<location; defaults to CurrentUser>",
  "AllowInvalid": "<true or false; defaults to false>"
}
```

<span data-ttu-id="701c3-257">架构的注意事项：</span><span class="sxs-lookup"><span data-stu-id="701c3-257">Schema notes:</span></span>

* <span data-ttu-id="701c3-258">终结点的名称不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="701c3-258">Endpoints names are case-insensitive.</span></span> <span data-ttu-id="701c3-259">例如，`HTTPS` 和 `Https` 都是有效的。</span><span class="sxs-lookup"><span data-stu-id="701c3-259">For example, `HTTPS` and `Https` are valid.</span></span>
* <span data-ttu-id="701c3-260">每个终结点都要具备 `Url` 参数。</span><span class="sxs-lookup"><span data-stu-id="701c3-260">The `Url` parameter is required for each endpoint.</span></span> <span data-ttu-id="701c3-261">此参数的格式和顶层 `Urls` 配置参数一样，只不过它只能有单个值。</span><span class="sxs-lookup"><span data-stu-id="701c3-261">The format for this parameter is the same as the top-level `Urls` configuration parameter except that it's limited to a single value.</span></span>
* <span data-ttu-id="701c3-262">这些终结点不会添加进顶层 `Urls` 配置中定义的终结点，而是替换它们。</span><span class="sxs-lookup"><span data-stu-id="701c3-262">These endpoints replace those defined in the top-level `Urls` configuration rather than adding to them.</span></span> <span data-ttu-id="701c3-263">通过 `Listen` 在代码中定义的终结点与在配置节中定义的终结点相累积。</span><span class="sxs-lookup"><span data-stu-id="701c3-263">Endpoints defined in code via `Listen` are cumulative with the endpoints defined in the configuration section.</span></span>
* <span data-ttu-id="701c3-264">`Certificate` 部分是可选的。</span><span class="sxs-lookup"><span data-stu-id="701c3-264">The `Certificate` section is optional.</span></span> <span data-ttu-id="701c3-265">如果为指定 `Certificate` 部分，则使用在之前的方案中定义的默认值。</span><span class="sxs-lookup"><span data-stu-id="701c3-265">If the `Certificate` section isn't specified, the defaults defined in earlier scenarios are used.</span></span> <span data-ttu-id="701c3-266">如果没有可用的默认值，服务器会引发异常且无法启动。</span><span class="sxs-lookup"><span data-stu-id="701c3-266">If no defaults are available, the server throws an exception and fails to start.</span></span>
* <span data-ttu-id="701c3-267">`Certificate` 支持 Path&ndash;Password 和 Subject&ndash;Store 证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-267">The `Certificate` section supports both **Path**&ndash;**Password** and **Subject**&ndash;**Store** certificates.</span></span>
* <span data-ttu-id="701c3-268">只要不会导致端口冲突，就能以这种方式定义任何数量的终结点。</span><span class="sxs-lookup"><span data-stu-id="701c3-268">Any number of endpoints may be defined in this way so long as they don't cause port conflicts.</span></span>
* <span data-ttu-id="701c3-269">`serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 通过 `.Endpoint(string name, options => { })` 方法返回 `KestrelConfigurationLoader`，可以用于补充已配置的终结点设置：</span><span class="sxs-lookup"><span data-stu-id="701c3-269">`serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` returns a `KestrelConfigurationLoader` with an `.Endpoint(string name, options => { })` method that can be used to supplement a configured endpoint's settings:</span></span>

  ```csharp
  serverOptions.Configure(context.Configuration.GetSection("Kestrel"))
      .Endpoint("HTTPS", opt =>
      {
          opt.HttpsOptions.SslProtocols = SslProtocols.Tls12;
      });
  ```

  <span data-ttu-id="701c3-270">也可以直接访问 `KestrelServerOptions.ConfigurationLoader` 来保持现有加载程序上的迭代，例如由 `WebHost.CreatedDeafaultBuilder` 提供的加载程序。</span><span class="sxs-lookup"><span data-stu-id="701c3-270">You can also directly access `KestrelServerOptions.ConfigurationLoader` to keep iterating on the existing loader, such as the one provided by `WebHost.CreatedDeafaultBuilder`.</span></span>

* <span data-ttu-id="701c3-271">每个终结点的配置节都可用于 `Endpoint` 方法中的选项，以便读取自定义设置。</span><span class="sxs-lookup"><span data-stu-id="701c3-271">The configuration section for each endpoint is a available on the options in the `Endpoint` method so that custom settings may be read.</span></span>
* <span data-ttu-id="701c3-272">通过另一节再次调用 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` 可能加载多个配置。</span><span class="sxs-lookup"><span data-stu-id="701c3-272">Multiple configurations may be loaded by calling `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` again with another section.</span></span> <span data-ttu-id="701c3-273">只使用最新配置，除非之前的实例上显式调用了 `Load`。</span><span class="sxs-lookup"><span data-stu-id="701c3-273">Only the last configuration is used, unless `Load` is explicitly called on prior instances.</span></span> <span data-ttu-id="701c3-274">元包不会调用 `Load`，所以可能会替换它的默认配置节。</span><span class="sxs-lookup"><span data-stu-id="701c3-274">The metapackage doesn't call `Load` so that its default configuration section may be replaced.</span></span>
* <span data-ttu-id="701c3-275">`KestrelConfigurationLoader` 从 `KestrelServerOptions` 将 API 的 `Listen` 簇反射为 `Endpoint` 重载，因此可在同样的位置配置代码和配置终结点。</span><span class="sxs-lookup"><span data-stu-id="701c3-275">`KestrelConfigurationLoader` mirrors the `Listen` family of APIs from `KestrelServerOptions` as `Endpoint` overloads, so code and config endpoints may be configured in the same place.</span></span> <span data-ttu-id="701c3-276">这些重载不使用名称，且只使用配置中的默认设置。</span><span class="sxs-lookup"><span data-stu-id="701c3-276">These overloads don't use names and only consume default settings from configuration.</span></span>

<span data-ttu-id="701c3-277">*更改代码中的默认值*</span><span class="sxs-lookup"><span data-stu-id="701c3-277">*Change the defaults in code*</span></span>

<span data-ttu-id="701c3-278">可以使用 `ConfigureEndpointDefaults` 和 `ConfigureHttpsDefaults` 更改 `ListenOptions` 和 `HttpsConnectionAdapterOptions` 的默认设置，包括重写之前的方案指定的默认证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-278">`ConfigureEndpointDefaults` and `ConfigureHttpsDefaults` can be used to change default settings for `ListenOptions` and `HttpsConnectionAdapterOptions`, including overriding the default certificate specified in the prior scenario.</span></span> <span data-ttu-id="701c3-279">需要在配置任何终结点之前调用 `ConfigureEndpointDefaults` 和 `ConfigureHttpsDefaults`。</span><span class="sxs-lookup"><span data-stu-id="701c3-279">`ConfigureEndpointDefaults` and `ConfigureHttpsDefaults` should be called before any endpoints are configured.</span></span>

```csharp
options.ConfigureEndpointDefaults(opt =>
{
    opt.NoDelay = true;
});

options.ConfigureHttpsDefaults(httpsOptions =>
{
    httpsOptions.SslProtocols = SslProtocols.Tls12;
});
```

<span data-ttu-id="701c3-280">*SNI 的 Kestrel 支持*</span><span class="sxs-lookup"><span data-stu-id="701c3-280">*Kestrel support for SNI*</span></span>

<span data-ttu-id="701c3-281">[服务器名称指示 (SNI)](https://tools.ietf.org/html/rfc6066#section-3) 可用于承载相同 IP 地址和端口上的多个域。</span><span class="sxs-lookup"><span data-stu-id="701c3-281">[Server Name Indication (SNI)](https://tools.ietf.org/html/rfc6066#section-3) can be used to host multiple domains on the same IP address and port.</span></span> <span data-ttu-id="701c3-282">为了运行 SNI，客户端在 TLS 握手过程中将进行安全会话的主机名发送至服务器，从而让服务器可以提供正确的证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-282">For SNI to function, the client sends the host name for the secure session to the server during the TLS handshake so that the server can provide the correct certificate.</span></span> <span data-ttu-id="701c3-283">在 TLS 握手后的安全会话期间，客户端将服务器提供的证书用于与服务器进行加密通信。</span><span class="sxs-lookup"><span data-stu-id="701c3-283">The client uses the furnished certificate for encrypted communication with the server during the secure session that follows the TLS handshake.</span></span>

<span data-ttu-id="701c3-284">Kestrel 通过 `ServerCertificateSelector` 回调支持 SNI。</span><span class="sxs-lookup"><span data-stu-id="701c3-284">Kestrel supports SNI via the `ServerCertificateSelector` callback.</span></span> <span data-ttu-id="701c3-285">每次连接调用一次回调，从而允许应用检查主机名并选择合适的证书。</span><span class="sxs-lookup"><span data-stu-id="701c3-285">The callback is invoked once per connection to allow the app to inspect the host name and select the appropriate certificate.</span></span>

<span data-ttu-id="701c3-286">SNI 支持需要在目标框架 `netcoreapp2.1` 上允许。</span><span class="sxs-lookup"><span data-stu-id="701c3-286">SNI support requires running on target framework `netcoreapp2.1`.</span></span> <span data-ttu-id="701c3-287">在 `netcoreapp2.0` 和 `net461` 上，回调也会调用，但是 `name` 始终为 `null`。</span><span class="sxs-lookup"><span data-stu-id="701c3-287">On `netcoreapp2.0` and `net461`, the callback is invoked but the `name` is always `null`.</span></span> <span data-ttu-id="701c3-288">如果客户端未在 TLS 握手过程中提供主机名参数，则 `name` 也为 `null`。</span><span class="sxs-lookup"><span data-stu-id="701c3-288">The `name` is also `null` if the client doesn't provide the host name parameter in the TLS handshake.</span></span>

```csharp
WebHost.CreateDefaultBuilder()
    .UseKestrel((context, options) =>
    {
        options.ListenAnyIP(5005, listenOptions =>
        {
            listenOptions.UseHttps(httpsOptions =>
            {
                var localhostCert = CertificateLoader.LoadFromStoreCert(
                    "localhost", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var exampleCert = CertificateLoader.LoadFromStoreCert(
                    "example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var subExampleCert = CertificateLoader.LoadFromStoreCert(
                    "sub.example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var certs = new Dictionary(StringComparer.OrdinalIgnoreCase);
                certs["localhost"] = localhostCert;
                certs["example.com"] = exampleCert;
                certs["sub.example.com"] = subExampleCert;

                httpsOptions.ServerCertificateSelector = (connectionContext, name) =>
                {
                    if (name != null && certs.TryGetValue(name, out var cert))
                    {
                        return cert;
                    }

                    return exampleCert;
                };
            });
        });
    });
```

::: moniker-end

<span data-ttu-id="701c3-289">**绑定到 TCP 套接字**</span><span class="sxs-lookup"><span data-stu-id="701c3-289">**Bind to a TCP socket**</span></span>

<span data-ttu-id="701c3-290">[Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 方法绑定至 TCP 套接字，并可通过选项 lambda 配置 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="701c3-290">The [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) method binds to a TCP socket, and an options lambda permits SSL certificate configuration:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="701c3-291">请注意此示例如何使用 [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions) 为特定终结点配置 SSL。</span><span class="sxs-lookup"><span data-stu-id="701c3-291">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions).</span></span> <span data-ttu-id="701c3-292">可使用相同 API 为特定终结点配置其他 Kestrel 设置。</span><span class="sxs-lookup"><span data-stu-id="701c3-292">Use the same API to configure other Kestrel settings for specific endpoints.</span></span>

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

<span data-ttu-id="701c3-293">**绑定到 Unix 套接字**</span><span class="sxs-lookup"><span data-stu-id="701c3-293">**Bind to a Unix socket**</span></span>

<span data-ttu-id="701c3-294">可通过 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 侦听 Unix 套接字以提高 Nginx 的性能，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="701c3-294">Listen on a Unix socket with [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="701c3-295">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="701c3-295">**Port 0**</span></span>

<span data-ttu-id="701c3-296">如果指定端口号 `0`，Kestrel 将动态绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="701c3-296">When the port number `0` is specified, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="701c3-297">以下示例演示如何确定 Kestrel 在运行时实际绑定到的端口：</span><span class="sxs-lookup"><span data-stu-id="701c3-297">The following example shows how to determine which port Kestrel actually bound at runtime:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Port0&highlight=3)]

<span data-ttu-id="701c3-298">在应用运行时，控制台窗口输出指示可用于访问应用的动态端口：</span><span class="sxs-lookup"><span data-stu-id="701c3-298">When the app is run, the console window output indicates the dynamic port where the app can be reached:</span></span>

```console
Now listening on: http://127.0.0.1:48508
```

<span data-ttu-id="701c3-299">**UseUrls、--urls 命令行参数、urls 主机配置键以及 ASPNETCORE_URLS 环境变量的限制**</span><span class="sxs-lookup"><span data-stu-id="701c3-299">**UseUrls, --urls command-line argument, urls host configuration key, and ASPNETCORE_URLS environment variable limitations**</span></span>

<span data-ttu-id="701c3-300">使用以下方法配置终结点：</span><span class="sxs-lookup"><span data-stu-id="701c3-300">Configure endpoints with the following approaches:</span></span>

* [<span data-ttu-id="701c3-301">UseUrls</span><span class="sxs-lookup"><span data-stu-id="701c3-301">UseUrls</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
* <span data-ttu-id="701c3-302">`--urls` 命令行参数</span><span class="sxs-lookup"><span data-stu-id="701c3-302">`--urls` command-line argument</span></span>
* <span data-ttu-id="701c3-303">`urls` 主机配置键</span><span class="sxs-lookup"><span data-stu-id="701c3-303">`urls` host configuration key</span></span>
* <span data-ttu-id="701c3-304">`ASPNETCORE_URLS` 环境变量</span><span class="sxs-lookup"><span data-stu-id="701c3-304">`ASPNETCORE_URLS` environment variable</span></span>

<span data-ttu-id="701c3-305">若要将代码用于 Kestrel 以外的服务器，这些方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="701c3-305">These methods are useful for making code work with servers other than Kestrel.</span></span> <span data-ttu-id="701c3-306">但是，请注意以下限制：</span><span class="sxs-lookup"><span data-stu-id="701c3-306">However, be aware of these limitations:</span></span>

* <span data-ttu-id="701c3-307">SSL 不能使用这些方法，除非 HTTPS 终结点配置中提供了默认证书（如本主题前面的部分所示，使用 `KestrelServerOptions` 配置或配置文件）。</span><span class="sxs-lookup"><span data-stu-id="701c3-307">SSL can't be used with these approaches unless a default certificate is provided in the HTTPS endpoint configuration (for example, using `KestrelServerOptions` configuration or a configuration file as shown earlier in this topic).</span></span>
* <span data-ttu-id="701c3-308">如果同时使用 `Listen` 和 `UseUrls` 方法，`Listen` 终结点将覆盖 `UseUrls` 终结点。</span><span class="sxs-lookup"><span data-stu-id="701c3-308">When both the `Listen` and `UseUrls` approaches are used simultaneously, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="701c3-309">**IIS 终结点配置**</span><span class="sxs-lookup"><span data-stu-id="701c3-309">**IIS endpoint configuration**</span></span>

<span data-ttu-id="701c3-310">使用 IIS 时，由 `Listen` 或 `UseUrls` 设置用于 IIS 覆盖绑定的 URL 绑定。</span><span class="sxs-lookup"><span data-stu-id="701c3-310">When using IIS, the URL bindings for IIS override bindings are set by either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="701c3-311">有关详细信息，请参阅 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)主题。</span><span class="sxs-lookup"><span data-stu-id="701c3-311">For more information, see the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="701c3-312">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="701c3-312">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="701c3-313">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="701c3-313">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="701c3-314">配置 URL 前缀和 Kestrel 使用的端口：</span><span class="sxs-lookup"><span data-stu-id="701c3-314">Configure URL prefixes and ports for Kestrel using:</span></span>

* <span data-ttu-id="701c3-315">[UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) 扩展方法</span><span class="sxs-lookup"><span data-stu-id="701c3-315">[UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) extension method</span></span>
* <span data-ttu-id="701c3-316">`--urls` 命令行参数</span><span class="sxs-lookup"><span data-stu-id="701c3-316">`--urls` command-line argument</span></span>
* <span data-ttu-id="701c3-317">`urls` 主机配置键</span><span class="sxs-lookup"><span data-stu-id="701c3-317">`urls` host configuration key</span></span>
* <span data-ttu-id="701c3-318">ASP.NET Core 配置系统，包括 `ASPNETCORE_URLS` 环境变量</span><span class="sxs-lookup"><span data-stu-id="701c3-318">ASP.NET Core configuration system, including `ASPNETCORE_URLS` environment variable</span></span>

<span data-ttu-id="701c3-319">有关这些方法的详细信息，请参阅[承载](xref:fundamentals/host/index)。</span><span class="sxs-lookup"><span data-stu-id="701c3-319">For more information on these methods, see [Hosting](xref:fundamentals/host/index).</span></span>

<span data-ttu-id="701c3-320">**IIS 终结点配置**</span><span class="sxs-lookup"><span data-stu-id="701c3-320">**IIS endpoint configuration**</span></span>

<span data-ttu-id="701c3-321">使用 IIS 时，由 `UseUrls` 设置用于 IIS 覆盖绑定的 URL 绑定。</span><span class="sxs-lookup"><span data-stu-id="701c3-321">When using IIS, the URL bindings for IIS override bindings set by `UseUrls`.</span></span> <span data-ttu-id="701c3-322">有关详细信息，请参阅 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)主题。</span><span class="sxs-lookup"><span data-stu-id="701c3-322">For more information, see the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic.</span></span>

---

::: moniker range=">= aspnetcore-2.1"

## <a name="transport-configuration"></a><span data-ttu-id="701c3-323">传输配置</span><span class="sxs-lookup"><span data-stu-id="701c3-323">Transport configuration</span></span>

<span data-ttu-id="701c3-324">对于 ASP.NET Core 2.1 版，Kestrel 默认传输不再基于 Libuv，而是基于托管的套接字。</span><span class="sxs-lookup"><span data-stu-id="701c3-324">With the release of ASP.NET Core 2.1, Kestrel's default transport is no longer based on Libuv but instead based on managed sockets.</span></span> <span data-ttu-id="701c3-325">这是 ASP.NET Core 2.0 应用升级到 2.1 时的一个重大更改，它调用 [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv) 并依赖于以下包中的一个：</span><span class="sxs-lookup"><span data-stu-id="701c3-325">This is a breaking change for ASP.NET Core 2.0 apps upgrading to 2.1 that call [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv) and depend on either of the following packages:</span></span>

* <span data-ttu-id="701c3-326">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/)（直接包引用）</span><span class="sxs-lookup"><span data-stu-id="701c3-326">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) (direct package reference)</span></span>
* [<span data-ttu-id="701c3-327">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="701c3-327">Microsoft.AspNetCore.App</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)

<span data-ttu-id="701c3-328">对于 ASP.NET Core 2.1 或更高版本，项目使用 `Microsoft.AspNetCore.App` 元包并需要使用 Libuv：</span><span class="sxs-lookup"><span data-stu-id="701c3-328">For ASP.NET Core 2.1 or later projects that use the `Microsoft.AspNetCore.App` metapackage and require the use of Libuv:</span></span>

* <span data-ttu-id="701c3-329">将用于 [Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv/) 包的依赖项添加到应用的项目文件：</span><span class="sxs-lookup"><span data-stu-id="701c3-329">Add a dependency for the [Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv/) package to the app's project file:</span></span>

    ```xml
    <PackageReference Include="Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv" 
                    Version="2.1.0" />
    ```

* <span data-ttu-id="701c3-330">调用 [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv)：</span><span class="sxs-lookup"><span data-stu-id="701c3-330">Call [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv):</span></span>

    ```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseLibuv()
                .UseStartup<Startup>();
    }
    ```

::: moniker-end

### <a name="url-prefixes"></a><span data-ttu-id="701c3-331">URL 前缀</span><span class="sxs-lookup"><span data-stu-id="701c3-331">URL prefixes</span></span>

<span data-ttu-id="701c3-332">如果使用 `UseUrls`、`--urls` 命令行参数、`urls` 主机配置键或 `ASPNETCORE_URLS` 环境变量，URL 前缀可采用以下任意格式。</span><span class="sxs-lookup"><span data-stu-id="701c3-332">When using `UseUrls`, `--urls` command-line argument, `urls` host configuration key, or `ASPNETCORE_URLS` environment variable, the URL prefixes can be in any of the following formats.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="701c3-333">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="701c3-333">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="701c3-334">仅 HTTP URL 前缀是有效的。</span><span class="sxs-lookup"><span data-stu-id="701c3-334">Only HTTP URL prefixes are valid.</span></span> <span data-ttu-id="701c3-335">使用 `UseUrls` 配置 URL 绑定时，Kestrel 不支持 SSL。</span><span class="sxs-lookup"><span data-stu-id="701c3-335">Kestrel doesn't support SSL when configuring URL bindings using `UseUrls`.</span></span>

* <span data-ttu-id="701c3-336">包含端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="701c3-336">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="701c3-337">`0.0.0.0` 是一种绑定到所有 IPv4 地址的特殊情况。</span><span class="sxs-lookup"><span data-stu-id="701c3-337">`0.0.0.0` is a special case that binds to all IPv4 addresses.</span></span>

* <span data-ttu-id="701c3-338">包含端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="701c3-338">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  ```

  <span data-ttu-id="701c3-339">`[::]` 是 IPv4 `0.0.0.0` 的 IPv6 等效项。</span><span class="sxs-lookup"><span data-stu-id="701c3-339">`[::]` is the IPv6 equivalent of IPv4 `0.0.0.0`.</span></span>

* <span data-ttu-id="701c3-340">包含端口号的主机名</span><span class="sxs-lookup"><span data-stu-id="701c3-340">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="701c3-341">主机名、`*`和 `+` 并不特殊。</span><span class="sxs-lookup"><span data-stu-id="701c3-341">Host names, `*`, and `+`, aren't special.</span></span> <span data-ttu-id="701c3-342">没有识别为有效 IP 地址或 `localhost` 的任何内容都将绑定到所有 IPv4 和 IPv6 IP。</span><span class="sxs-lookup"><span data-stu-id="701c3-342">Anything not recognized as a valid IP address or `localhost` binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="701c3-343">若要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用，请使用 [HTTP.sys](xref:fundamentals/servers/httpsys) 或 IIS、Nginx 或 Apache 等反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="701c3-343">To bind different host names to different ASP.NET Core apps on the same port, use [HTTP.sys](xref:fundamentals/servers/httpsys) or a reverse proxy server, such as IIS, Nginx, or Apache.</span></span>

  > [!WARNING]
  > <span data-ttu-id="701c3-344">如果在启用了主机筛选的情况下不使用反向代理，请启用[主机筛选](#host-filtering)。</span><span class="sxs-lookup"><span data-stu-id="701c3-344">If not using a reverse proxy with host filtering enabled, enable [host filtering](#host-filtering).</span></span>

* <span data-ttu-id="701c3-345">包含端口号的主机 `localhost` 名称或包含端口号的环回 IP</span><span class="sxs-lookup"><span data-stu-id="701c3-345">Host `localhost` name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="701c3-346">指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。</span><span class="sxs-lookup"><span data-stu-id="701c3-346">When `localhost` is specified, Kestrel attempts to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="701c3-347">如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="701c3-347">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="701c3-348">如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="701c3-348">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="701c3-349">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="701c3-349">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

* <span data-ttu-id="701c3-350">包含端口号的 IPv4 地址</span><span class="sxs-lookup"><span data-stu-id="701c3-350">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="701c3-351">`0.0.0.0` 是一种绑定到所有 IPv4 地址的特殊情况。</span><span class="sxs-lookup"><span data-stu-id="701c3-351">`0.0.0.0` is a special case that binds to all IPv4 addresses.</span></span>

* <span data-ttu-id="701c3-352">包含端口号的 IPv6 地址</span><span class="sxs-lookup"><span data-stu-id="701c3-352">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  https://[0:0:0:0:0:ffff:4137:270a]:443/
  ```

  <span data-ttu-id="701c3-353">`[::]` 是 IPv4 `0.0.0.0` 的 IPv6 等效项。</span><span class="sxs-lookup"><span data-stu-id="701c3-353">`[::]` is the IPv6 equivalent of IPv4 `0.0.0.0`.</span></span>

* <span data-ttu-id="701c3-354">包含端口号的主机名</span><span class="sxs-lookup"><span data-stu-id="701c3-354">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="701c3-355">主机名、`*` 和 `+` 并不特殊。</span><span class="sxs-lookup"><span data-stu-id="701c3-355">Host names, `*`, and `+` aren't special.</span></span> <span data-ttu-id="701c3-356">不是已识别 IP 地址或 `localhost` 的任何内容都将绑定到所有 IPv4 和 IPv6 IP。</span><span class="sxs-lookup"><span data-stu-id="701c3-356">Anything that isn't a recognized IP address or `localhost` binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="701c3-357">若要将不同主机名绑定到相同端口上的不同 ASP.NET Core 应用，请使用 [WebListener](xref:fundamentals/servers/weblistener) 或 IIS、Nginx 或 Apache 等反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="701c3-357">To bind different host names to different ASP.NET Core apps on the same port, use [WebListener](xref:fundamentals/servers/weblistener) or a reverse proxy server, such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="701c3-358">包含端口号的主机 `localhost` 名称或包含端口号的环回 IP</span><span class="sxs-lookup"><span data-stu-id="701c3-358">Host `localhost` name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="701c3-359">指定 `localhost` 后，Kestrel 将尝试绑定到 IPv4 和 IPv6 环回接口。</span><span class="sxs-lookup"><span data-stu-id="701c3-359">When `localhost` is specified, Kestrel attempts to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="701c3-360">如果其他服务正在任一环回接口上使用请求的端口，则 Kestrel 将无法启动。</span><span class="sxs-lookup"><span data-stu-id="701c3-360">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="701c3-361">如果任一环回接口出于任何其他原因（通常是因为 IPv6 不受支持）而不可用，则 Kestrel 将记录一个警告。</span><span class="sxs-lookup"><span data-stu-id="701c3-361">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span>

* <span data-ttu-id="701c3-362">Unix 套接字</span><span class="sxs-lookup"><span data-stu-id="701c3-362">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock
  ```

<span data-ttu-id="701c3-363">**端口 0**</span><span class="sxs-lookup"><span data-stu-id="701c3-363">**Port 0**</span></span>

<span data-ttu-id="701c3-364">如果指定端口号 `0`，Kestrel 将动态绑定到可用端口。</span><span class="sxs-lookup"><span data-stu-id="701c3-364">When the port number is `0` is specified, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="701c3-365">除 `localhost`外，任何主机名或 IP 都可绑定到端口 `0`。</span><span class="sxs-lookup"><span data-stu-id="701c3-365">Binding to port `0` is allowed for any host name or IP except for `localhost`.</span></span>

<span data-ttu-id="701c3-366">在应用运行时，控制台窗口输出指示可用于访问应用的动态端口：</span><span class="sxs-lookup"><span data-stu-id="701c3-366">When the app is run, the console window output indicates the dynamic port where the app can be reached:</span></span>

```console
Now listening on: http://127.0.0.1:48508
```

<span data-ttu-id="701c3-367">**SSL 的 URL 前缀**</span><span class="sxs-lookup"><span data-stu-id="701c3-367">**URL prefixes for SSL**</span></span>

<span data-ttu-id="701c3-368">如果调用 `https:` 扩展方法，请务必在 URL 前缀中包括 `UseHttps`：</span><span class="sxs-lookup"><span data-stu-id="701c3-368">If calling the `UseHttps` extension method, be sure to include URL prefixes with `https:`:</span></span>

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
> <span data-ttu-id="701c3-369">不能在相同端口上托管 HTTPS 和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="701c3-369">HTTPS and HTTP can't be hosted on the same port.</span></span>

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

---

## <a name="host-filtering"></a><span data-ttu-id="701c3-370">主机筛选</span><span class="sxs-lookup"><span data-stu-id="701c3-370">Host filtering</span></span>

<span data-ttu-id="701c3-371">尽管 Kestrel 支持基于前缀的配置（例如 `http://example.com:5000`），但 Kestrel 在很大程度上会忽略主机名。</span><span class="sxs-lookup"><span data-stu-id="701c3-371">While Kestrel supports configuration based on prefixes such as `http://example.com:5000`, Kestrel largely ignores the host name.</span></span> <span data-ttu-id="701c3-372">主机 `localhost` 是一个特殊情况，用于绑定至环回地址。</span><span class="sxs-lookup"><span data-stu-id="701c3-372">Host `localhost` is a special case used for binding to loopback addresses.</span></span> <span data-ttu-id="701c3-373">除了显式 IP 地址以外的所有主机都绑定至所有公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="701c3-373">Any host other than an explicit IP address binds to all public IP addresses.</span></span> <span data-ttu-id="701c3-374">这些信息都不用于验证请求 `Host` 标头。</span><span class="sxs-lookup"><span data-stu-id="701c3-374">None of this information is used to validate request `Host` headers.</span></span>

<span data-ttu-id="701c3-375">有两种解决方法：</span><span class="sxs-lookup"><span data-stu-id="701c3-375">There are two workarounds:</span></span>

* <span data-ttu-id="701c3-376">使用主机标头筛选的反向代理的主机。</span><span class="sxs-lookup"><span data-stu-id="701c3-376">Host behind a reverse proxy with host header filtering.</span></span> <span data-ttu-id="701c3-377">这是 ASP.NET Core 1.x 中唯一的 Kestrel 支持方案。</span><span class="sxs-lookup"><span data-stu-id="701c3-377">This was the only supported scenario for Kestrel in ASP.NET Core 1.x.</span></span>
* <span data-ttu-id="701c3-378">使用中间件来根据 `Host` 标头筛选请求。</span><span class="sxs-lookup"><span data-stu-id="701c3-378">Use a middleware to filter requests by the `Host` header.</span></span> <span data-ttu-id="701c3-379">下面是中间件示例：</span><span class="sxs-lookup"><span data-stu-id="701c3-379">A sample middleware follows:</span></span>

```csharp
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Primitives;
using Microsoft.Net.Http.Headers;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

// A normal middleware would provide an options type, config binding, extension methods, etc..
// This intentionally does all of the work inside of the middleware so it can be
// easily copy-pasted into docs and other projects.
public class HostFilteringMiddleware
{
    private readonly RequestDelegate _next;
    private readonly IList<string> _hosts;
    private readonly ILogger<HostFilteringMiddleware> _logger;

    public HostFilteringMiddleware(RequestDelegate next, IConfiguration config, ILogger<HostFilteringMiddleware> logger)
    {
        if (config == null)
        {
            throw new ArgumentNullException(nameof(config));
        }

        _next = next ?? throw new ArgumentNullException(nameof(next));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));

        // A semicolon separated list of host names without the port numbers.
        // IPv6 addresses must use the bounding brackets and be in their normalized form.
        _hosts = config["AllowedHosts"]?.Split(new[] { ';' }, StringSplitOptions.RemoveEmptyEntries);
        if (_hosts == null || _hosts.Count == 0)
        {
            throw new InvalidOperationException("No configuration entry found for AllowedHosts.");
        }
    }

    public Task Invoke(HttpContext context)
    {
        if (!ValidateHost(context))
        {
            context.Response.StatusCode = 400;
            _logger.LogDebug("Request rejected due to incorrect Host header.");
            return Task.CompletedTask;
        }

        return _next(context);
    }

    // This does not duplicate format validations that are expected to be performed by the host.
    private bool ValidateHost(HttpContext context)
    {
        StringSegment host = context.Request.Headers[HeaderNames.Host].ToString().Trim();

        if (StringSegment.IsNullOrEmpty(host))
        {
            // Http/1.0 does not require the Host header.
            // Http/1.1 requires the header but the value may be empty.
            return true;
        }

        // Drop the port

        var colonIndex = host.LastIndexOf(':');

        // IPv6 special case
        if (host.StartsWith("[", StringComparison.Ordinal))
        {
            var endBracketIndex = host.IndexOf(']');
            if (endBracketIndex < 0)
            {
                // Invalid format
                return false;
            }
            if (colonIndex < endBracketIndex)
            {
                // No port, just the IPv6 Host
                colonIndex = -1;
            }
        }

        if (colonIndex > 0)
        {
            host = host.Subsegment(0, colonIndex);
        }

        foreach (var allowedHost in _hosts)
        {
            if (StringSegment.Equals(allowedHost, host, StringComparison.OrdinalIgnoreCase))
            {
                return true;
            }

            // Sub-domain wildcards: *.example.com
            if (allowedHost.StartsWith("*.", StringComparison.Ordinal) && host.Length >= allowedHost.Length)
            {
                // .example.com
                var allowedRoot = new StringSegment(allowedHost, 1, allowedHost.Length - 1);

                var hostRoot = host.Subsegment(host.Length - allowedRoot.Length, allowedRoot.Length);
                if (hostRoot.Equals(allowedRoot, StringComparison.OrdinalIgnoreCase))
                {
                    return true;
                }
            }
        }

        return false;
    }
}
```

<span data-ttu-id="701c3-380">在 `Startup.Configure` 中注册上述 `HostFilteringMiddleware`。</span><span class="sxs-lookup"><span data-stu-id="701c3-380">Register the preceding `HostFilteringMiddleware` in `Startup.Configure`.</span></span> <span data-ttu-id="701c3-381">请注意，[中间件注册的排序](xref:fundamentals/middleware/index#ordering)非常重要。</span><span class="sxs-lookup"><span data-stu-id="701c3-381">Note that the [ordering of middleware registration](xref:fundamentals/middleware/index#ordering) is important.</span></span> <span data-ttu-id="701c3-382">应在诊断中间件（例如 `app.UseExceptionHandler`）注册完成后立即进行注册。</span><span class="sxs-lookup"><span data-stu-id="701c3-382">Registration should occur immediately after Diagnostic Middleware registration (for example, `app.UseExceptionHandler`).</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseBrowserLink();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseMiddleware<HostFilteringMiddleware>();

    app.UseMvcWithDefaultRoute();
}
```

<span data-ttu-id="701c3-383">上述中间件需要 appsettings.\<EnvironmentName>.json 中的 `AllowedHosts` 键。</span><span class="sxs-lookup"><span data-stu-id="701c3-383">The preceding middleware expects an `AllowedHosts` key in *appsettings.\<EnvironmentName>.json*.</span></span> <span data-ttu-id="701c3-384">此键的值是以分号分隔的不带端口号的主机名列表。</span><span class="sxs-lookup"><span data-stu-id="701c3-384">This key's value is a semicolon-delimited list of host names without the port numbers.</span></span> <span data-ttu-id="701c3-385">包括 appsettings.Production.json 中的 `AllowedHosts` 键值对：</span><span class="sxs-lookup"><span data-stu-id="701c3-385">Include the `AllowedHosts` key-value pair in *appsettings.Production.json*:</span></span>

```json
{
  "AllowedHosts": "example.com"
}
```

<span data-ttu-id="701c3-386">appsettings.Development.json（localhost 配置文件）：</span><span class="sxs-lookup"><span data-stu-id="701c3-386">*appsettings.Development.json* (localhost configuration file):</span></span>

```json
{
  "AllowedHosts": "localhost"
}
```

## <a name="additional-resources"></a><span data-ttu-id="701c3-387">其他资源</span><span class="sxs-lookup"><span data-stu-id="701c3-387">Additional resources</span></span>

* [<span data-ttu-id="701c3-388">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="701c3-388">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
* [<span data-ttu-id="701c3-389">Kestrel 源代码</span><span class="sxs-lookup"><span data-stu-id="701c3-389">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)
