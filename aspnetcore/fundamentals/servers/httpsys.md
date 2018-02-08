---
title: "ASP.NET Core 中的 HTTP.sys Web 服务器实现"
author: rick-anderson
description: "介绍 Windows 上适用于 ASP.NET Core 的 Web 服务器 HTTP.sys。 HTTP.sys 构建于 Http.Sys 内核模式驱动程序之上，是 Kestrel 的一种替代选择，可用来直接连接到 Internet，而无需使用 IIS。"
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: f36a86fc67e715165afd0c38992f9767f90cf3b4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="28f23-104">ASP.NET Core 中的 HTTP.sys Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="28f23-104">HTTP.sys web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="28f23-105">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="28f23-105">By [Tom Dykstra](https://github.com/tdykstra) and [Chris Ross](https://github.com/Tratcher)</span></span>

> [!NOTE]
> <span data-ttu-id="28f23-106">本主题仅适用于 ASP.NET Core 2.0 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="28f23-106">This topic applies only to ASP.NET Core 2.0 and later.</span></span> <span data-ttu-id="28f23-107">在早期版本的 ASP.NET Core 的中，HTTP.sys 被命名为 [WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="28f23-107">In earlier versions of ASP.NET Core, HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener).</span></span>

<span data-ttu-id="28f23-108">HTTP.sys 是仅在 Windows 上运行的[适用于 ASP.NET Core 的 Web 服务器](index.md)。</span><span class="sxs-lookup"><span data-stu-id="28f23-108">HTTP.sys is a [web server for ASP.NET Core](index.md) that runs only on Windows.</span></span> <span data-ttu-id="28f23-109">它构建于 [Http.Sys 内核模式驱动程序](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)之上。</span><span class="sxs-lookup"><span data-stu-id="28f23-109">It's built on the [Http.Sys kernel mode driver](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="28f23-110">HTTP.sys 是 [Kestrel](kestrel.md) 的替代选择，提供了一些 Kestel 所没有的功能。</span><span class="sxs-lookup"><span data-stu-id="28f23-110">HTTP.sys is an alternative to [Kestrel](kestrel.md) that offers some features that Kestel doesn't.</span></span> <span data-ttu-id="28f23-111">HTTP.sys 不能与 IIS 或 IIS Express 结合使用，因为它与 [ASP.NET Core 模块](aspnet-core-module.md)不兼容。</span><span class="sxs-lookup"><span data-stu-id="28f23-111">**HTTP.sys can't be used with IIS or IIS Express, as it's incompatible with the [ASP.NET Core Module](aspnet-core-module.md).**</span></span>

<span data-ttu-id="28f23-112">HTTP.sys 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="28f23-112">HTTP.sys supports the following features:</span></span>

- [<span data-ttu-id="28f23-113">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="28f23-113">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
- <span data-ttu-id="28f23-114">端口共享</span><span class="sxs-lookup"><span data-stu-id="28f23-114">Port sharing</span></span>
- <span data-ttu-id="28f23-115">具有 SNI 的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="28f23-115">HTTPS with SNI</span></span>
- <span data-ttu-id="28f23-116">基于 TLS 的 HTTP/2 (Windows 10)</span><span class="sxs-lookup"><span data-stu-id="28f23-116">HTTP/2 over TLS (Windows 10)</span></span>
- <span data-ttu-id="28f23-117">直接文件传输</span><span class="sxs-lookup"><span data-stu-id="28f23-117">Direct file transmission</span></span>
- <span data-ttu-id="28f23-118">响应缓存</span><span class="sxs-lookup"><span data-stu-id="28f23-118">Response caching</span></span>
- <span data-ttu-id="28f23-119">WebSocket (Windows 8)</span><span class="sxs-lookup"><span data-stu-id="28f23-119">WebSockets (Windows 8)</span></span>

<span data-ttu-id="28f23-120">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="28f23-120">Supported Windows versions:</span></span>

- <span data-ttu-id="28f23-121">Windows 7 和 Windows Server 2008 R2 及更高版本</span><span class="sxs-lookup"><span data-stu-id="28f23-121">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="28f23-122">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="28f23-122">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-httpsys"></a><span data-ttu-id="28f23-123">何时使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="28f23-123">When to use HTTP.sys</span></span>

<span data-ttu-id="28f23-124">对于需要将服务器直接公开到 Internet 而不使用 IIS 的部署，HTTP.sys 非常有用。</span><span class="sxs-lookup"><span data-stu-id="28f23-124">HTTP.sys is useful for deployments where you need to expose the server directly to the Internet without using IIS.</span></span>

![HTTP.sys 直接与 Internet 进行通信](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="28f23-126">由于 HTTP.sys 构建于 Http.Sys 之上，因此不需要反向代理服务器来抵御攻击。</span><span class="sxs-lookup"><span data-stu-id="28f23-126">Because it's built on Http.Sys, HTTP.sys doesn't require a reverse proxy server for protection against attacks.</span></span> <span data-ttu-id="28f23-127">Http.Sys 是一项成熟的技术，可以抵御多种攻击，并提供可靠、安全、可伸缩的全功能 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="28f23-127">Http.Sys is mature technology that protects against many kinds of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="28f23-128">IIS 本身作为 Http.Sys 之上的 HTTP 侦听器运行。</span><span class="sxs-lookup"><span data-stu-id="28f23-128">IIS itself runs as an HTTP listener on top of Http.Sys.</span></span> 

<span data-ttu-id="28f23-129">当你需要 Kestrel 中没有的功能（如 Windows 身份验证）时，HTTP.sys 是内部部署的不错选择。</span><span class="sxs-lookup"><span data-stu-id="28f23-129">HTTP.sys is a good choice for internal deployments when you need a feature not available in Kestrel, such as Windows authentication.</span></span>

![HTTP.sys 直接与你的内部网络进行通信](httpsys/_static/httpsys-to-internal.png)

## <a name="how-to-use-httpsys"></a><span data-ttu-id="28f23-131">如何使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="28f23-131">How to use HTTP.sys</span></span>

<span data-ttu-id="28f23-132">下面是主机操作系统和 ASP.NET Core 应用程序的安装任务概述。</span><span class="sxs-lookup"><span data-stu-id="28f23-132">Here's an overview of setup tasks for the host OS and your ASP.NET Core application.</span></span>

### <a name="configure-windows-server"></a><span data-ttu-id="28f23-133">配置 Windows Server</span><span class="sxs-lookup"><span data-stu-id="28f23-133">Configure Windows Server</span></span>

* <span data-ttu-id="28f23-134">安装应用程序要求的 .NET 版本，例如 [.NET Core](https://www.microsoft.com/net/download/core) 或 [.NET Framework](https://www.microsoft.com/net/download/framework)。</span><span class="sxs-lookup"><span data-stu-id="28f23-134">Install the version of .NET that your application requires, such as [.NET Core](https://www.microsoft.com/net/download/core) or [.NET Framework](https://www.microsoft.com/net/download/framework).</span></span>

* <span data-ttu-id="28f23-135">预先注册 URL 前缀以绑定到 HTTP.sys，并设置 SSL 证书</span><span class="sxs-lookup"><span data-stu-id="28f23-135">Preregister URL prefixes to bind to HTTP.sys, and set up SSL certificates</span></span>

   <span data-ttu-id="28f23-136">如果在 Windows 中不预先注册 URL 前缀，则必须使用管理员权限运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="28f23-136">If you don't preregister URL prefixes in Windows, you have to run your application with administrator privileges.</span></span> <span data-ttu-id="28f23-137">唯一的例外是，如果你使用端口号大于 1024 的 HTTP（不是 HTTPS）绑定到 localhost；在这种情况下不需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="28f23-137">The only exception is if you bind to localhost using HTTP (not HTTPS) with a port number greater than 1024; in that case, administrator privileges aren't required.</span></span>

   <span data-ttu-id="28f23-138">有关详细信息，请参阅本文后续部分的[如何预先注册前缀和配置 SSL](#preregister-url-prefixes-and-configure-ssl)。</span><span class="sxs-lookup"><span data-stu-id="28f23-138">For details, see [How to preregister prefixes and configure SSL](#preregister-url-prefixes-and-configure-ssl) later in this article.</span></span>

* <span data-ttu-id="28f23-139">打开防火墙端口以允许流量到达 HTTP.sys。</span><span class="sxs-lookup"><span data-stu-id="28f23-139">Open firewall ports to allow traffic to reach HTTP.sys.</span></span>

   <span data-ttu-id="28f23-140">可使用 netsh.exe 或 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)。</span><span class="sxs-lookup"><span data-stu-id="28f23-140">You can use *netsh.exe* or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

<span data-ttu-id="28f23-141">此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。</span><span class="sxs-lookup"><span data-stu-id="28f23-141">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>

### <a name="configure-your-aspnet-core-application-to-use-httpsys"></a><span data-ttu-id="28f23-142">配置 ASP.NET Core 应用程序以使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="28f23-142">Configure your ASP.NET Core application to use HTTP.sys</span></span>

* <span data-ttu-id="28f23-143">如果使用 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 元包，则不需要安装包。</span><span class="sxs-lookup"><span data-stu-id="28f23-143">No package install is needed if you use the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage.</span></span> <span data-ttu-id="28f23-144">元包中包括 [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) 包。</span><span class="sxs-lookup"><span data-stu-id="28f23-144">The [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/) package is included in the metapackage.</span></span>

* <span data-ttu-id="28f23-145">在 `WebHostBuilder` 上调用 `Main` 方法中的 `UseHttpSys` 扩展方法，指定所需的任何 [HTTP.sys 选项](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="28f23-145">Call the `UseHttpSys` extension method on `WebHostBuilder` in your `Main` method, specifying any [HTTP.sys options](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs) that you need, as shown in the following example:</span></span>

  [!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=11-19)]

### <a name="configure-httpsys-options"></a><span data-ttu-id="28f23-146">配置 HTTP.sys 选项</span><span class="sxs-lookup"><span data-stu-id="28f23-146">Configure HTTP.sys options</span></span>

<span data-ttu-id="28f23-147">以下是一些可以配置的 HTTP.sys 设置和限制。</span><span class="sxs-lookup"><span data-stu-id="28f23-147">Here are some of the HTTP.sys settings and limits that you can configure.</span></span>

<span data-ttu-id="28f23-148">**客户端最大连接数**</span><span class="sxs-lookup"><span data-stu-id="28f23-148">**Maximum client connections**</span></span>

<span data-ttu-id="28f23-149">可使用 Program.cs 中的以下代码为整个应用程序设置并发打开 TCP 的最大连接数：</span><span class="sxs-lookup"><span data-stu-id="28f23-149">The maximum number of concurrent open TCP connections can be set for the entire application with the following code in *Program.cs*:</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=5)]

<span data-ttu-id="28f23-150">默认情况下，最大连接数不受限制 (NULL)。</span><span class="sxs-lookup"><span data-stu-id="28f23-150">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="28f23-151">**请求正文最大大小**</span><span class="sxs-lookup"><span data-stu-id="28f23-151">**Maximum request body size**</span></span>

<span data-ttu-id="28f23-152">默认的请求正文最大大小为 30,000,000 字节，大约 28.6MB。</span><span class="sxs-lookup"><span data-stu-id="28f23-152">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span>

<span data-ttu-id="28f23-153">在 ASP.NET Core MVC 应用中替代限制的推荐方法是在操作方法上使用 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 属性：</span><span class="sxs-lookup"><span data-stu-id="28f23-153">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="28f23-154">以下示例演示如何为整个应用程序和每个请求配置约束：</span><span class="sxs-lookup"><span data-stu-id="28f23-154">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Options&highlight=6)]

<span data-ttu-id="28f23-155">可在 Startup.cs 中替代特定请求的设置：</span><span class="sxs-lookup"><span data-stu-id="28f23-155">You can override the setting on a specific request in *Startup.cs*:</span></span>

[!code-csharp[](httpsys/sample/Startup.cs?name=snippet_Configure&highlight=9-10)]
 
<span data-ttu-id="28f23-156">如果在应用程序开始读取请求后尝试配置请求限制，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="28f23-156">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="28f23-157">通过 `IsReadOnly` 属性可知道，如果 `MaxRequestBodySize` 属性处于只读状态，则意味着配置限制已经太迟了。</span><span class="sxs-lookup"><span data-stu-id="28f23-157">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="28f23-158">有关其他 HTTP.sys 选项的信息，请参阅 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs)。</span><span class="sxs-lookup"><span data-stu-id="28f23-158">For information about other HTTP.sys options, see [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs).</span></span> 

### <a name="configure-urls-and-ports-to-listen-on"></a><span data-ttu-id="28f23-159">配置要侦听的 URL 和端口</span><span class="sxs-lookup"><span data-stu-id="28f23-159">Configure URLs and ports to listen on</span></span> 

<span data-ttu-id="28f23-160">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="28f23-160">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="28f23-161">要配置 URL 前缀和端口，可使用 `UseUrls` 扩展方法、`urls` 命令行参数、ASPNETCORE_URLS 环境变量或 [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs) 上的 `UrlPrefixes` 属性。</span><span class="sxs-lookup"><span data-stu-id="28f23-161">To configure URL prefixes and ports, you can use the `UseUrls` extension method, the `urls` command-line argument, the ASPNETCORE_URLS environment variable, or the `UrlPrefixes` property on [HttpSysOptions](https://github.com/aspnet/HttpSysServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.HttpSys/HttpSysOptions.cs).</span></span> <span data-ttu-id="28f23-162">下面的代码示例使用 `UrlPrefixes`。</span><span class="sxs-lookup"><span data-stu-id="28f23-162">The following code example uses `UrlPrefixes`.</span></span>

[!code-csharp[](httpsys/sample/Program.cs?name=snippet_Main&highlight=17)]

<span data-ttu-id="28f23-163">`UrlPrefixes` 的优点是，如果尝试添加格式错误的前缀，则会立即收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="28f23-163">An advantage of `UrlPrefixes` is that you get an error message immediately if you try to add a prefix that's formatted wrong.</span></span> <span data-ttu-id="28f23-164">`UseUrls`（与 `urls` 和 ASPNETCORE_URLS 共享）的优点是，可在 Kestrel 和 HTTP.sys 之间更轻松地切换。</span><span class="sxs-lookup"><span data-stu-id="28f23-164">An advantage of `UseUrls` (shared with `urls` and ASPNETCORE_URLS) is that you can more easily switch between Kestrel and HTTP.sys.</span></span>

<span data-ttu-id="28f23-165">如果同时使用 `UseUrls`（`urls` 或 ASPNETCORE_URLS）和 `UrlPrefixes`，`UrlPrefixes` 中的设置会替代 `UseUrls` 中的设置。</span><span class="sxs-lookup"><span data-stu-id="28f23-165">If you use both `UseUrls` (or `urls` or ASPNETCORE_URLS) and `UrlPrefixes`, the settings in `UrlPrefixes` override the ones in `UseUrls`.</span></span> <span data-ttu-id="28f23-166">有关详细信息，请参阅[托管](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="28f23-166">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

<span data-ttu-id="28f23-167">HTTP.sys 使用 [HTTP 服务器 API UrlPrefix 字符串格式](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28f23-167">HTTP.sys uses the [HTTP Server API UrlPrefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="28f23-168">请确保在服务器上预先注册的 `UseUrls` 或 `UrlPrefixes` 中指定相同的前缀字符串。</span><span class="sxs-lookup"><span data-stu-id="28f23-168">Make sure that you specify the same prefix strings in `UseUrls` or `UrlPrefixes` that you preregister on the server.</span></span> 

### <a name="dont-use-iis"></a><span data-ttu-id="28f23-169">不使用 IIS</span><span class="sxs-lookup"><span data-stu-id="28f23-169">Don't use IIS</span></span>

<span data-ttu-id="28f23-170">请确保应用程序未配置为运行 IIS 或 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="28f23-170">Make sure your application isn't configured to run IIS or IIS Express.</span></span>

<span data-ttu-id="28f23-171">在 Visual Studio 中，默认启动配置文件是针对 IIS Express 的。</span><span class="sxs-lookup"><span data-stu-id="28f23-171">In Visual Studio, the default launch profile is for IIS Express.</span></span> <span data-ttu-id="28f23-172">若要作为控制台应用程序运行该项目，请手动更改所选配置文件，如以下屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="28f23-172">To run the project as a console application, manually change the selected profile, as shown in the following screen shot.</span></span>

![选择控制台应用配置文件](httpsys/_static/vs-choose-profile.png)

## <a name="preregister-url-prefixes-and-configure-ssl"></a><span data-ttu-id="28f23-174">预先注册 URL 前缀和配置 SSL</span><span class="sxs-lookup"><span data-stu-id="28f23-174">Preregister URL prefixes and configure SSL</span></span>

<span data-ttu-id="28f23-175">IIS 和 HTTP.sys 都依赖于基础 Http.Sys 内核模式驱动程序，以便侦听请求和执行初始化处理。</span><span class="sxs-lookup"><span data-stu-id="28f23-175">Both IIS and HTTP.sys rely on the underlying Http.Sys kernel mode driver to listen for requests and do initial processing.</span></span> <span data-ttu-id="28f23-176">在 IIS 中，管理 UI 提供一种相对简单的方法来配置所有内容。</span><span class="sxs-lookup"><span data-stu-id="28f23-176">In IIS, the management UI gives you a relatively easy way to configure everything.</span></span> <span data-ttu-id="28f23-177">但是，需要自己配置 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="28f23-177">However, you need to configure Http.Sys yourself.</span></span> <span data-ttu-id="28f23-178">执行该操作的内置工具是 netsh.exe。</span><span class="sxs-lookup"><span data-stu-id="28f23-178">The built-in tool for doing that's *netsh.exe*.</span></span> 

<span data-ttu-id="28f23-179">通过 netsh.exe，可保留 URL 前缀并分配 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="28f23-179">With *netsh.exe* you can reserve URL prefixes and assign SSL certificates.</span></span> <span data-ttu-id="28f23-180">该工具需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="28f23-180">The tool requires administrative privileges.</span></span>

<span data-ttu-id="28f23-181">以下示例演示保留 80 和 443 端口的 URL 前缀所需的最低要求：</span><span class="sxs-lookup"><span data-stu-id="28f23-181">The following example shows the minimum needed to reserve URL prefixes for ports 80 and 443:</span></span>

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

<span data-ttu-id="28f23-182">以下示例演示如何分配 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="28f23-182">The following example shows how to assign an SSL certificate:</span></span>

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
```

<span data-ttu-id="28f23-183">下面是 netsh.exe 的参考文档：</span><span class="sxs-lookup"><span data-stu-id="28f23-183">Here is the reference documentation for *netsh.exe*:</span></span>

* <span data-ttu-id="28f23-184">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)（超文本传输协议 (HTTP) 的 Netsh 命令）</span><span class="sxs-lookup"><span data-stu-id="28f23-184">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)</span></span>
* <span data-ttu-id="28f23-185">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)（UrlPrefix 字符串）</span><span class="sxs-lookup"><span data-stu-id="28f23-185">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)</span></span>

<span data-ttu-id="28f23-186">以下资源提供几个方案的详细说明。</span><span class="sxs-lookup"><span data-stu-id="28f23-186">The following resources provide detailed instructions for several scenarios.</span></span> <span data-ttu-id="28f23-187">涉及 HttpListener 的文章同样适用于 HTTP.sys，因为两者都基于 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="28f23-187">Articles that refer to HttpListener apply equally to HTTP.sys, as both are based on Http.Sys.</span></span>

* [<span data-ttu-id="28f23-188">如何：使用 SSL 证书配置端口</span><span class="sxs-lookup"><span data-stu-id="28f23-188">How to: Configure a Port with an SSL Certificate</span></span>](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* <span data-ttu-id="28f23-189">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html)（HTTPS 通信 - 基于 HttpListener 的托管和客户端证书）这是很久之前的一个第三方博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="28f23-189">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) This is a third-party blog and is fairly old but still has useful information.</span></span>
* <span data-ttu-id="28f23-190">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/)（如何：使用 HttpListener 或 HTTP 服务器非托管代码 (C++) 作为 SSL 简单服务器进行演练），这也是很久之前的一个博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="28f23-190">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) This too is an older blog with useful information.</span></span>

<span data-ttu-id="28f23-191">以下是一些比 netsh.exe 命令行更易使用的第三方工具。</span><span class="sxs-lookup"><span data-stu-id="28f23-191">Here are some third-party tools that can be easier to use than the *netsh.exe* command line.</span></span> <span data-ttu-id="28f23-192">它们不是由 Microsoft 提供或认可的。</span><span class="sxs-lookup"><span data-stu-id="28f23-192">These are not provided by or endorsed by Microsoft.</span></span> <span data-ttu-id="28f23-193">默认情况下，这些工具以管理员身份运行，因为 netsh.exe 本身需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="28f23-193">The tools run as administrator by default, since *netsh.exe* itself requires administrator privileges.</span></span>

* <span data-ttu-id="28f23-194">[http.sys 管理器](http://httpsysmanager.codeplex.com/)提供用于列出和配置 SSL 证书和选项、前缀保留和证书信任列表的 UI。</span><span class="sxs-lookup"><span data-stu-id="28f23-194">[http.sys Manager](http://httpsysmanager.codeplex.com/) provides UI for listing and configuring SSL certificates and options, prefix reservations, and certificate trust lists.</span></span> 
* <span data-ttu-id="28f23-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) 允许用户列出或配置 SSL 证书和 URL 前缀。</span><span class="sxs-lookup"><span data-stu-id="28f23-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) lets you list or configure SSL certificates and URL prefixes.</span></span> <span data-ttu-id="28f23-196">UI 比 http.sys 管理器更加完善并且提供更多的配置选项，但在其他方面它提供类似的功能。</span><span class="sxs-lookup"><span data-stu-id="28f23-196">The UI is more refined than http.sys Manager and exposes a few more configuration options, but otherwise it provides similar functionality.</span></span> <span data-ttu-id="28f23-197">它不能创建新的证书信任列表 (CTL)，但可以分配现有证书信任列表。</span><span class="sxs-lookup"><span data-stu-id="28f23-197">It cannot create a new certificate trust list (CTL), but can assign existing ones.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

## <a name="next-steps"></a><span data-ttu-id="28f23-198">后续步骤</span><span class="sxs-lookup"><span data-stu-id="28f23-198">Next steps</span></span>

<span data-ttu-id="28f23-199">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="28f23-199">For more information, see the following resources:</span></span>

* [<span data-ttu-id="28f23-200">本文的示例应用</span><span class="sxs-lookup"><span data-stu-id="28f23-200">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)
* [<span data-ttu-id="28f23-201">HTTP.sys 源代码</span><span class="sxs-lookup"><span data-stu-id="28f23-201">HTTP.sys source code</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="28f23-202">承载</span><span class="sxs-lookup"><span data-stu-id="28f23-202">Hosting</span></span>](xref:fundamentals/hosting)
