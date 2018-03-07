---
title: "ASP.NET Core 中的 HTTP.sys Web 服务器实现"
author: tdykstra
description: "了解 Windows 上适用于 ASP.NET Core 的 Web 服务器 HTTP.sys。 HTTP.sys 构建于 HTTP.sys 内核模式驱动程序之上，是 Kestrel 的一种替代选择，可用来直接连接到 Internet，而无需使用 IIS。"
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/28/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: 730ecf12f718f6bbbdefb7cdc561481b126c995b
ms.sourcegitcommit: c5ecda3c5b1674b62294cfddcb104e7f0b9ce465
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="ccc7f-104">ASP.NET Core 中的 HTTP.sys Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="ccc7f-104">HTTP.sys web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="ccc7f-105">作者：[Tom Dykstra](https://github.com/tdykstra)、[Chris Ross](https://github.com/Tratcher) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ccc7f-105">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Luke Latham](https://github.com/guardrex)</span></span>

> [!NOTE]
> <span data-ttu-id="ccc7f-106">本主题仅适用于 ASP.NET Core 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-106">This topic applies to ASP.NET Core 2.0 or later.</span></span> <span data-ttu-id="ccc7f-107">在早期版本的 ASP.NET Core 的中，HTTP.sys 被命名为 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-107">In earlier versions of ASP.NET Core, HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener).</span></span>

<span data-ttu-id="ccc7f-108">[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) 是仅在 Windows 上运行的[适用于 ASP.NET Core 的 Web 服务器](xref:fundamentals/servers/index)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-108">[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys) is a [web server for ASP.NET Core](xref:fundamentals/servers/index) that only runs on Windows.</span></span> <span data-ttu-id="ccc7f-109">HTTP.sys 是 [Kestrel](xref:fundamentals/servers/kestrel) 的替代选择，提供了一些 Kestrel 不提供的功能。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-109">HTTP.sys is an alternative to [Kestrel](xref:fundamentals/servers/kestrel) and offers some features that Kestrel doesn't provide.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccc7f-110">HTTP.sys 与 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)不兼容，不能与 IIS 或 IIS Express 结合使用。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-110">HTTP.sys is incompatible with the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and can't be used with IIS or IIS Express.</span></span>

<span data-ttu-id="ccc7f-111">HTTP.sys 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-111">HTTP.sys supports the following features:</span></span>

* [<span data-ttu-id="ccc7f-112">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="ccc7f-112">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
* <span data-ttu-id="ccc7f-113">端口共享</span><span class="sxs-lookup"><span data-stu-id="ccc7f-113">Port sharing</span></span>
* <span data-ttu-id="ccc7f-114">具有 SNI 的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="ccc7f-114">HTTPS with SNI</span></span>
* <span data-ttu-id="ccc7f-115">基于 TLS 的 HTTP/2（Windows 10 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-115">HTTP/2 over TLS (Windows 10 or later)</span></span>
* <span data-ttu-id="ccc7f-116">直接文件传输</span><span class="sxs-lookup"><span data-stu-id="ccc7f-116">Direct file transmission</span></span>
* <span data-ttu-id="ccc7f-117">响应缓存</span><span class="sxs-lookup"><span data-stu-id="ccc7f-117">Response caching</span></span>
* <span data-ttu-id="ccc7f-118">WebSocket（Windows 8 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-118">WebSockets (Windows 8 or later)</span></span>

<span data-ttu-id="ccc7f-119">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-119">Supported Windows versions:</span></span>

* <span data-ttu-id="ccc7f-120">Windows 7 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ccc7f-120">Windows 7 or later</span></span>
* <span data-ttu-id="ccc7f-121">Windows Server 2008 R2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ccc7f-121">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="ccc7f-122">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-122">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-httpsys"></a><span data-ttu-id="ccc7f-123">何时使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="ccc7f-123">When to use HTTP.sys</span></span>

<span data-ttu-id="ccc7f-124">HTTP.sys 对于以下情形的部署来说很有用：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-124">HTTP.sys is useful for deployments where:</span></span>

* <span data-ttu-id="ccc7f-125">需要将服务器直接公开到 Internet 而不使用 IIS 的部署。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-125">There's a need to expose the server directly to the Internet without using IIS.</span></span>

  ![HTTP.sys 直接与 Internet 进行通信](httpsys/_static/httpsys-to-internet.png)

* <span data-ttu-id="ccc7f-127">内部部署需要 Kestrel 中没有的功能，如 [Windows 身份验证](xref:security/authentication/windowsauth)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-127">An internal deployment requires a feature not available in Kestrel, such as [Windows Authentication](xref:security/authentication/windowsauth).</span></span>

  ![HTTP.sys 直接与内部网络进行通信](httpsys/_static/httpsys-to-internal.png)

<span data-ttu-id="ccc7f-129">HTTP.sys 是一项成熟的技术，可以抵御多种攻击，并提供可靠、安全、可伸缩的全功能 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-129">HTTP.sys is mature technology that protects against many types of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="ccc7f-130">IIS 本身作为 HTTP.sys 之上的 HTTP 侦听器运行。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-130">IIS itself runs as an HTTP listener on top of HTTP.sys.</span></span> 

## <a name="how-to-use-httpsys"></a><span data-ttu-id="ccc7f-131">如何使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="ccc7f-131">How to use HTTP.sys</span></span>

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a><span data-ttu-id="ccc7f-132">配置 ASP.NET Core 应用以使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="ccc7f-132">Configure the ASP.NET Core app to use HTTP.sys</span></span>

1. <span data-ttu-id="ccc7f-133">使用 [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.All/))（ASP.NET Core 2.0 或更高版本）时，不需要项目文件中的包引用。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-133">A package reference in the project file isn't required when using the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) ([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.All/)) (ASP.NET Core 2.0 or later).</span></span> <span data-ttu-id="ccc7f-134">未使用 `Microsoft.AspNetCore.All` 元包时，向 [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) 添加包引用。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-134">When not using the `Microsoft.AspNetCore.All` metapackage, add a package reference to [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/).</span></span>

1. <span data-ttu-id="ccc7f-135">构建 Web 主机时调用 [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) 扩展方法，同时指定所需的 [HTTP.sys 选项](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions)：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-135">Call the [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) extension method when building the web host, specifying any required [HTTP.sys options](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions):</span></span>

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   <span data-ttu-id="ccc7f-136">通过[注册表设置](https://support.microsoft.com/kb/820129)处理其他 HTTP.sys 配置。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-136">Additional HTTP.sys configuration is handled through [registry settings](https://support.microsoft.com/kb/820129).</span></span>

   <span data-ttu-id="ccc7f-137">**HTTP.sys 选项**</span><span class="sxs-lookup"><span data-stu-id="ccc7f-137">**HTTP.sys options**</span></span>

   | <span data-ttu-id="ccc7f-138">属性</span><span class="sxs-lookup"><span data-stu-id="ccc7f-138">Property</span></span> | <span data-ttu-id="ccc7f-139">描述</span><span class="sxs-lookup"><span data-stu-id="ccc7f-139">Description</span></span> | <span data-ttu-id="ccc7f-140">默认</span><span class="sxs-lookup"><span data-stu-id="ccc7f-140">Default</span></span> |
   | -------- | ----------- | :-----: |
   | [<span data-ttu-id="ccc7f-141">AllowSynchronousIO</span><span class="sxs-lookup"><span data-stu-id="ccc7f-141">AllowSynchronousIO</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.allowsynchronousio) | <span data-ttu-id="ccc7f-142">控制是否允许 `HttpContext.Request.Body` 和 `HttpContext.Response.Body` 的同步输入/输出。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-142">Control whether synchronous input/output is allowed for the `HttpContext.Request.Body` and `HttpContext.Response.Body`.</span></span> | `true` |
   | [<span data-ttu-id="ccc7f-143">Authentication.AllowAnonymous</span><span class="sxs-lookup"><span data-stu-id="ccc7f-143">Authentication.AllowAnonymous</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.allowanonymous) | <span data-ttu-id="ccc7f-144">允许匿名请求。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-144">Allow anonymous requests.</span></span> | `true` |
   | [<span data-ttu-id="ccc7f-145">Authentication.Schemes</span><span class="sxs-lookup"><span data-stu-id="ccc7f-145">Authentication.Schemes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.schemes) | <span data-ttu-id="ccc7f-146">指定允许的身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-146">Specify the allowed authentication schemes.</span></span> <span data-ttu-id="ccc7f-147">可能在处理侦听器之前随时修改。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-147">May be modified at any time prior to disposing the listener.</span></span> <span data-ttu-id="ccc7f-148">通过 [AuthenticationSchemes 枚举](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes) `Basic`、`Kerberos`、`Negotiate`、`None` 和 `NTLM` 提供值。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-148">Values are provided by the [AuthenticationSchemes enum](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes): `Basic`, `Kerberos`, `Negotiate`, `None`, and `NTLM`.</span></span> | `None` |
   | [<span data-ttu-id="ccc7f-149">EnableResponseCaching</span><span class="sxs-lookup"><span data-stu-id="ccc7f-149">EnableResponseCaching</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.enableresponsecaching) | <span data-ttu-id="ccc7f-150">尝试[内核模式](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)缓存，响应合格的标头。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-150">Attempt [kernel-mode](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) caching for responses with eligible headers.</span></span> <span data-ttu-id="ccc7f-151">该响应可能不包括 `Set-Cookie`、`Vary` 或 `Pragma` 标头。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-151">The response may not include `Set-Cookie`, `Vary`, or `Pragma` headers.</span></span> <span data-ttu-id="ccc7f-152">它必须包括属性为 `public` 的 `Cache-Control` 标头和 `shared-max-age` 或 `max-age` 值，或 `Expires` 标头。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-152">It must include a `Cache-Control` header that's `public` and either a `shared-max-age` or `max-age` value, or an `Expires` header.</span></span> | `true` |
   | [<span data-ttu-id="ccc7f-153">MaxAccepts</span><span class="sxs-lookup"><span data-stu-id="ccc7f-153">MaxAccepts</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxaccepts) | <span data-ttu-id="ccc7f-154">最大并发接受数量。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-154">The maximum number of concurrent accepts.</span></span> | <span data-ttu-id="ccc7f-155">5 &times; [环境。<br>ProcessorCount](/dotnet/api/system.environment.processorcount)</span><span class="sxs-lookup"><span data-stu-id="ccc7f-155">5 &times; [Environment.<br>ProcessorCount](/dotnet/api/system.environment.processorcount)</span></span> |
   | [<span data-ttu-id="ccc7f-156">MaxConnections</span><span class="sxs-lookup"><span data-stu-id="ccc7f-156">MaxConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxconnections) | <span data-ttu-id="ccc7f-157">要接受的最大并发连接数。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-157">The maximum number of concurrent connections to accept.</span></span> <span data-ttu-id="ccc7f-158">使用 `-1` 实现无限。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-158">Use `-1` for infinite.</span></span> <span data-ttu-id="ccc7f-159">通过 `null` 使用注册表的计算机范围内的设置。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-159">Use `null` to use the registry's machine-wide setting.</span></span> | `null`<br><span data-ttu-id="ccc7f-160">（无限制）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-160">(unlimited)</span></span> |
   | [<span data-ttu-id="ccc7f-161">MaxRequestBodySize</span><span class="sxs-lookup"><span data-stu-id="ccc7f-161">MaxRequestBodySize</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) | <span data-ttu-id="ccc7f-162">请参阅 <a href="#maxrequestbodysize">MaxRequestBodySize</a> 部分。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-162">See the <a href="#maxrequestbodysize">MaxRequestBodySize</a> section.</span></span> | <span data-ttu-id="ccc7f-163">30000000 个字节</span><span class="sxs-lookup"><span data-stu-id="ccc7f-163">30000000 bytes</span></span><br><span data-ttu-id="ccc7f-164">(~28.6 MB)</span><span class="sxs-lookup"><span data-stu-id="ccc7f-164">(~28.6 MB)</span></span> |
   | [<span data-ttu-id="ccc7f-165">RequestQueueLimit</span><span class="sxs-lookup"><span data-stu-id="ccc7f-165">RequestQueueLimit</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.requestqueuelimit) | <span data-ttu-id="ccc7f-166">队列中允许的最大请求数。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-166">The maximum number of requests that can be queued.</span></span> | <span data-ttu-id="ccc7f-167">1000</span><span class="sxs-lookup"><span data-stu-id="ccc7f-167">1000</span></span> |
   | [<span data-ttu-id="ccc7f-168">ThrowWriteExceptions</span><span class="sxs-lookup"><span data-stu-id="ccc7f-168">ThrowWriteExceptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.throwwriteexceptions) | <span data-ttu-id="ccc7f-169">指示由于客户端断开连接而失败的响应主体写入应引发异常还是正常完成。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-169">Indicate if response body writes that fail due to client disconnects should throw exceptions or complete normally.</span></span> | `false`<br><span data-ttu-id="ccc7f-170">（正常完成）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-170">(complete normally)</span></span> |
   | [<span data-ttu-id="ccc7f-171">超时</span><span class="sxs-lookup"><span data-stu-id="ccc7f-171">Timeouts</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts) | <span data-ttu-id="ccc7f-172">公开 HTTP.sys [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) 配置，也可以在注册表中进行配置。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-172">Expose the HTTP.sys [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) configuration, which may also be configured in the registry.</span></span> <span data-ttu-id="ccc7f-173">请访问 API 链接详细了解每个设置，包括默认值：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-173">Follow the API links to learn more about each setting, including default values:</span></span><ul><li><span data-ttu-id="ccc7f-174">[Timeouts.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.drainentitybody) &ndash; 允许 HTTP 服务器 API 在保持活动的连接上排出实体正文的时间。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-174">[Timeouts.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.drainentitybody) &ndash; Time allowed for the HTTP Server API to drain the entity body on a Keep-Alive connection.</span></span></li><li><span data-ttu-id="ccc7f-175">[Timeouts.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.entitybody) &ndash; 允许请求实体正文到达的时间。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-175">[Timeouts.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.entitybody) &ndash; Time allowed for the request entity body to arrive.</span></span></li><li><span data-ttu-id="ccc7f-176">[Timeouts.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.headerwait) &ndash; 允许 HTTP 服务器 API 分析请求头的时间。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-176">[Timeouts.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.headerwait) &ndash; Time allowed for the HTTP Server API to parse the request header.</span></span></li><li><span data-ttu-id="ccc7f-177">[Timeouts.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.idleconnection) &ndash; 对空闲连接允许的时间。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-177">[Timeouts.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.idleconnection) &ndash; Time allowed for an idle connection.</span></span></li><li><span data-ttu-id="ccc7f-178">[Timeouts.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.minsendbytespersecond) &ndash; 响应的最小发送速率。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-178">[Timeouts.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.minsendbytespersecond) &ndash; The minimum send rate for the response.</span></span></li><li><span data-ttu-id="ccc7f-179">[Timeouts.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.requestqueue) &ndash; 在应用选取请求前，允许请求在请求队列中停留的时间。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-179">[Timeouts.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.requestqueue) &ndash; Time allowed for the request to remain in the request queue before the app picks it up.</span></span></li></ul> |  |
   | [<span data-ttu-id="ccc7f-180">UrlPrefixes</span><span class="sxs-lookup"><span data-stu-id="ccc7f-180">UrlPrefixes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes) | <span data-ttu-id="ccc7f-181">指定 [UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection) 以注册 HTTP.sys。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-181">Specify the [UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection) to register with HTTP.sys.</span></span> <span data-ttu-id="ccc7f-182">最有用的是 [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add)，它用于将前缀添加到集合中。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-182">The most useful is [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add), which is used to add a prefix to the collection.</span></span> <span data-ttu-id="ccc7f-183">可能在处理侦听器之前随时对这些设置进行修改。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-183">These may be modified at any time prior to disposing the listener.</span></span> |  |

   <a name="maxrequestbodysize"></a>
   <span data-ttu-id="ccc7f-184">**MaxRequestBodySize**</span><span class="sxs-lookup"><span data-stu-id="ccc7f-184">**MaxRequestBodySize**</span></span>

   <span data-ttu-id="ccc7f-185">允许的请求正文的最大大小（以字节计）。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-185">The maximum allowed size of any request body in bytes.</span></span> <span data-ttu-id="ccc7f-186">当设置为 `null` 时，最大请求正文大小不受限制。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-186">When set to `null`, the maximum request body size is unlimited.</span></span> <span data-ttu-id="ccc7f-187">此限制不会影响升级后的连接，这始终不受限制。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-187">This limit has no effect on upgraded connections, which are always unlimited.</span></span>

   <span data-ttu-id="ccc7f-188">在 ASP.NET Core MVC 应用中为单个 `IActionResult` 替代限制的推荐方法是在操作方法上使用 [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 属性：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-188">The recommended method to override the limit in an ASP.NET Core MVC app for a single `IActionResult` is to use the [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) attribute on an action method:</span></span>
   
   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   <span data-ttu-id="ccc7f-189">如果在应用开始读取请求后尝试配置请求限制，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-189">An exception is thrown if the app attempts to configure the limit on a request after the app has started reading the request.</span></span> <span data-ttu-id="ccc7f-190">`IsReadOnly` 属性可用于指示 `MaxRequestBodySize` 属性是否处于只读状态。只读状态意味着已经太迟了，无法配置限制。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-190">An `IsReadOnly` property can be used to indicate if the `MaxRequestBodySize` property is in a read-only state, meaning it's too late to configure the limit.</span></span>

   <span data-ttu-id="ccc7f-191">如果应用应替代每个请求的 [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize)，则使用 [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature)：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-191">If the app should override [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) per-request, use the [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature):</span></span>

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

1. <span data-ttu-id="ccc7f-192">如果使用的是 Visual Studio，请确保应用未经配置以运行 IIS 或 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-192">If using Visual Studio, make sure the app isn't configured to run IIS or IIS Express.</span></span>

   <span data-ttu-id="ccc7f-193">在 Visual Studio 中，默认启动配置文件是针对 IIS Express 的。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-193">In Visual Studio, the default launch profile is for IIS Express.</span></span> <span data-ttu-id="ccc7f-194">若要作为控制台应用运行该项目，请手动更改所选配置文件，如以下屏幕截图中所示：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-194">To run the project as a console app, manually change the selected profile, as shown in the following screen shot:</span></span>

   ![选择控制台应用配置文件](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a><span data-ttu-id="ccc7f-196">配置 Windows Server</span><span class="sxs-lookup"><span data-stu-id="ccc7f-196">Configure Windows Server</span></span>

1. <span data-ttu-id="ccc7f-197">如果应用为[框架相关部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，则安装 .NET Core、.NET Framework 或两者（如果应用是面向 .NET Framework 的 .NET Core 应用）。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-197">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd), install .NET Core, .NET Framework, or both (if the app is a .NET Core app targeting the .NET Framework).</span></span>

   * <span data-ttu-id="ccc7f-198">**.NET Core** &ndash; 如果应用需要 .NET Core，则从 [.NET 下载](https://www.microsoft.com/net/download/windows)获取并运行 .NET Core 安装程序。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-198">**.NET Core** &ndash; If the app requires .NET Core, obtain and run the .NET Core installer from [.NET Downloads](https://www.microsoft.com/net/download/windows).</span></span>
   * <span data-ttu-id="ccc7f-199">**.NET Framework** &ndash; 如果应用需要 .NET Framework，请参阅 [.NET Framework：安装指南](/dotnet/framework/install/)查找安装说明。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-199">**.NET Framework** &ndash; If the app requires .NET Framework, see [.NET Framework: Installation guide](/dotnet/framework/install/) to find installation instructions.</span></span> <span data-ttu-id="ccc7f-200">安装所需的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-200">Install the required .NET Framework.</span></span> <span data-ttu-id="ccc7f-201">最新的 .NET Framework 的安装程序可从 [.NET 下载](https://www.microsoft.com/net/download/windows)中找到。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-201">The installer for the latest .NET Framework can be found at [.NET Downloads](https://www.microsoft.com/net/download/windows).</span></span>

1. <span data-ttu-id="ccc7f-202">配置应用的 URL 和端口。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-202">Configure URLs and ports for the app.</span></span>

   <span data-ttu-id="ccc7f-203">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-203">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="ccc7f-204">若要配置 URL 前缀和端口，选项包括使用：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-204">To configure URL prefixes and ports, options include using:</span></span>

   * [<span data-ttu-id="ccc7f-205">UseUrls</span><span class="sxs-lookup"><span data-stu-id="ccc7f-205">UseUrls</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
   * <span data-ttu-id="ccc7f-206">`urls` 命令行参数</span><span class="sxs-lookup"><span data-stu-id="ccc7f-206">`urls` command-line argument</span></span>
   * <span data-ttu-id="ccc7f-207">`ASPNETCORE_URLS` 环境变量</span><span class="sxs-lookup"><span data-stu-id="ccc7f-207">`ASPNETCORE_URLS` environment variable</span></span>
   * [<span data-ttu-id="ccc7f-208">UrlPrefixes</span><span class="sxs-lookup"><span data-stu-id="ccc7f-208">UrlPrefixes</span></span>](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)

   <span data-ttu-id="ccc7f-209">下方的代码示例演示了如何使用 [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-209">The following code example shows how to use [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes):</span></span>

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=11)]

   <span data-ttu-id="ccc7f-210">`UrlPrefixes` 的一个优点是会为格式不正确的前缀立即生成一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-210">An advantage of `UrlPrefixes` is that an error message is generated immediately for improperly formatted prefixes.</span></span>

   <span data-ttu-id="ccc7f-211">`UrlPrefixes` 中的设置替代 `UseUrls`/`urls`/`ASPNETCORE_URLS` 设置。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-211">The settings in `UrlPrefixes` override `UseUrls`/`urls`/`ASPNETCORE_URLS` settings.</span></span> <span data-ttu-id="ccc7f-212">因此，`UseUrls`、`urls` 和 `ASPNETCORE_URLS` 环境变量的一个优点是在 Kestrel 和 HTTP.sys 之间切换变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-212">Therefore, an advantage of `UseUrls`, `urls`, and the `ASPNETCORE_URLS` environment variable is that it's easier to switch between Kestrel and HTTP.sys.</span></span> <span data-ttu-id="ccc7f-213">有关 `UseUrls`、`urls` 和 `ASPNETCORE_URLS` 的更多信息，请参阅[托管](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-213">For more information on `UseUrls`, `urls`, and `ASPNETCORE_URLS`, see [Hosting](xref:fundamentals/hosting).</span></span>

   <span data-ttu-id="ccc7f-214">HTTP.sys 使用 [HTTP 服务器 API UrlPrefix 字符串格式](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-214">HTTP.sys uses the [HTTP Server API UrlPrefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span>

1. <span data-ttu-id="ccc7f-215">预先注册 URL 前缀以绑定到 HTTP.sys，并设置 x.509 证书。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-215">Preregister URL prefixes to bind to HTTP.sys and set up x.509 certificates.</span></span>

   <span data-ttu-id="ccc7f-216">如果未在 Windows 中预先注册 URL 前缀，请使用管理员特权运行应用。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-216">If URL prefixes aren't preregistered in Windows, run the app with administrator privileges.</span></span> <span data-ttu-id="ccc7f-217">唯一的例外是当使用端口号大于 1024 的 HTTP（而非 HTTPS）绑定到 localhost 时。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-217">The only exception is when binding to localhost using HTTP (not HTTPS) with a port number greater than 1024.</span></span> <span data-ttu-id="ccc7f-218">在这种情况下，无需使用管理员特权。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-218">In that case, administrator privileges aren't required.</span></span>

   1. <span data-ttu-id="ccc7f-219">用于配置 HTTP.sys 的内置工具为 *netsh.exe*。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-219">The built-in tool for configuring HTTP.sys is *netsh.exe*.</span></span> <span data-ttu-id="ccc7f-220">*netsh.exe* 用于保留 URL 前缀并分配 X.509 证书。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-220">*netsh.exe* is used to reserve URL prefixes and assign X.509 certificates.</span></span> <span data-ttu-id="ccc7f-221">此工具需要管理员特权。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-221">The tool requires administrator privileges.</span></span>

      <span data-ttu-id="ccc7f-222">以下示例显示了保留端口 80 和 443 的 URL 前缀的命令：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-222">The following example shows the commands to reserve URL prefixes for ports 80 and 443:</span></span>

      ```console
      netsh http add urlacl url=http://+:80/ user=Users
      netsh http add urlacl url=https://+:443/ user=Users
      ```

      <span data-ttu-id="ccc7f-223">以下示例显示了如何分配 X.509 证书：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-223">The following example shows how to assign an X.509 certificate:</span></span>

      ```console
      netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
      ```

      <span data-ttu-id="ccc7f-224">*netsh.exe* 的参考文档：</span><span class="sxs-lookup"><span data-stu-id="ccc7f-224">Reference documentation for *netsh.exe*:</span></span>

      * <span data-ttu-id="ccc7f-225">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)（超文本传输协议 (HTTP) 的 Netsh 命令）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-225">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)</span></span>
      * <span data-ttu-id="ccc7f-226">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)（UrlPrefix 字符串）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-226">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)</span></span>

   1. <span data-ttu-id="ccc7f-227">如果需要，请创建自签名的 X.509 证书。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-227">Create self-signed X.509 certificates, if required.</span></span>

     [!INCLUDE[How to make an X.509 cert](../../includes/make-x509-cert.md)]

1. <span data-ttu-id="ccc7f-228">打开防火墙端口以允许流量到达 HTTP.sys。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-228">Open firewall ports to allow traffic to reach HTTP.sys.</span></span> <span data-ttu-id="ccc7f-229">使用 *netsh.exe* 或 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)。</span><span class="sxs-lookup"><span data-stu-id="ccc7f-229">Use *netsh.exe* or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ccc7f-230">其他资源</span><span class="sxs-lookup"><span data-stu-id="ccc7f-230">Additional resources</span></span>

* [<span data-ttu-id="ccc7f-231">HTTP 服务器 API</span><span class="sxs-lookup"><span data-stu-id="ccc7f-231">HTTP Server API</span></span>](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)
* [<span data-ttu-id="ccc7f-232">aspnet/HttpSysServer GitHub 存储库（源代码）</span><span class="sxs-lookup"><span data-stu-id="ccc7f-232">aspnet/HttpSysServer GitHub repository (source code)</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="ccc7f-233">承载</span><span class="sxs-lookup"><span data-stu-id="ccc7f-233">Hosting</span></span>](xref:fundamentals/hosting)
