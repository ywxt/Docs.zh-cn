---
title: "ASP.NET Core 中的 WebListener Web 服务器实现"
author: rick-anderson
description: "介绍适用于 Windows 上 ASP.NET Core 的 Web 服务器 WebListener。 WebListener 构建于 Http.Sys 内核模式驱动程序之上，是 Kestrel 的一种替代选择，可用来直接连接到 Internet，而无需 IIS。"
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/weblistener
ms.openlocfilehash: fb2e0621645a48f4e603d754d8babbc07a78cae4
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="weblistener-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="2f6f3-104">ASP.NET Core 中的 WebListener Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="2f6f3-104">WebListener web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="2f6f3-105">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="2f6f3-105">By [Tom Dykstra](https://github.com/tdykstra) and [Chris Ross](https://github.com/Tratcher)</span></span>

> [!NOTE]
> <span data-ttu-id="2f6f3-106">本主题仅适用于 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-106">This topic applies only to ASP.NET Core 1.x.</span></span> <span data-ttu-id="2f6f3-107">在 ASP.NET Core 2.0 中，WebListener 被命名为 [HTTP.sys](httpsys.md)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-107">In ASP.NET Core 2.0, WebListener is named [HTTP.sys](httpsys.md).</span></span>

<span data-ttu-id="2f6f3-108">WebListener 是仅在 Windows 上运行的[适用于 ASP.NET Core 的 Web 服务器](index.md)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-108">WebListener is a [web server for ASP.NET Core](index.md) that runs only on Windows.</span></span> <span data-ttu-id="2f6f3-109">它构建于 [Http.Sys 内核模式驱动程序](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)之上。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-109">It's built on the [Http.Sys kernel mode driver](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="2f6f3-110">WebListener 是 [Kestrel](kestrel.md) 的一种替代选择，可用来直接连接到 Internet，而无需依赖 IIS 作为反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-110">WebListener is an alternative to [Kestrel](kestrel.md) that can be used for direct connection to the Internet without relying on IIS as a reverse proxy server.</span></span> <span data-ttu-id="2f6f3-111">事实上，WebListener 不能与 IIS 或 IIS Express 结合使用，因为它与 [ASP.NET Core 模块](aspnet-core-module.md)不兼容。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-111">In fact, **WebListener can't be used with IIS or IIS Express, as it isn't compatible with the [ASP.NET Core Module](aspnet-core-module.md).**</span></span>

<span data-ttu-id="2f6f3-112">尽管 ASP.NET Core 针对 WebListener 开发，但是它可以通过 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 包直接在任何 .NET Core 或 .NET Framework 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-112">Although WebListener was developed for ASP.NET Core, it can be used directly in any .NET Core or .NET Framework application via the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

<span data-ttu-id="2f6f3-113">WebListener 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-113">WebListener supports the following features:</span></span>

- [<span data-ttu-id="2f6f3-114">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="2f6f3-114">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
- <span data-ttu-id="2f6f3-115">端口共享</span><span class="sxs-lookup"><span data-stu-id="2f6f3-115">Port sharing</span></span>
- <span data-ttu-id="2f6f3-116">具有 SNI 的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f6f3-116">HTTPS with SNI</span></span>
- <span data-ttu-id="2f6f3-117">基于 TLS 的 HTTP/2 (Windows 10)</span><span class="sxs-lookup"><span data-stu-id="2f6f3-117">HTTP/2 over TLS (Windows 10)</span></span>
- <span data-ttu-id="2f6f3-118">直接文件传输</span><span class="sxs-lookup"><span data-stu-id="2f6f3-118">Direct file transmission</span></span>
- <span data-ttu-id="2f6f3-119">响应缓存</span><span class="sxs-lookup"><span data-stu-id="2f6f3-119">Response caching</span></span>
- <span data-ttu-id="2f6f3-120">WebSocket (Windows 8)</span><span class="sxs-lookup"><span data-stu-id="2f6f3-120">WebSockets (Windows 8)</span></span>

<span data-ttu-id="2f6f3-121">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-121">Supported Windows versions:</span></span>

- <span data-ttu-id="2f6f3-122">Windows 7 和 Windows Server 2008 R2 及更高版本</span><span class="sxs-lookup"><span data-stu-id="2f6f3-122">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="2f6f3-123">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="2f6f3-123">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-weblistener"></a><span data-ttu-id="2f6f3-124">何时使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="2f6f3-124">When to use WebListener</span></span>

<span data-ttu-id="2f6f3-125">WebListener 对于在无需使用 IIS 的情况下直接向 Internet 公开服务器的部署非常有用。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-125">WebListener is useful for deployments where you need to expose the server directly to the Internet without using IIS.</span></span>

![Weblistener 直接与 Internet 进行通信](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="2f6f3-127">由于 WebListener 构建于 Http.Sys 之上，因此它不需要反向代理服务器来抵御攻击。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-127">Because it's built on Http.Sys, WebListener doesn't require a reverse proxy server for protection against attacks.</span></span> <span data-ttu-id="2f6f3-128">Http.Sys 是一项成熟的技术，可以抵御多种攻击，并提供可靠、安全、可伸缩的全功能 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-128">Http.Sys is mature technology that protects against many kinds of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="2f6f3-129">IIS 本身作为 Http.Sys 之上的 HTTP 侦听器运行。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-129">IIS itself runs as an HTTP listener on top of Http.Sys.</span></span> 

<span data-ttu-id="2f6f3-130">当你无法通过 Kestrel 获取它提供的某个功能时，WebListener 对于内部部署也是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-130">WebListener is also a good choice for internal deployments when you need one of the features it offers that you can't get by using Kestrel.</span></span>

![Weblistener 直接与你的内部网络进行通信](weblistener/_static/weblistener-to-internal.png)

## <a name="how-to-use-weblistener"></a><span data-ttu-id="2f6f3-132">如何使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="2f6f3-132">How to use WebListener</span></span>

<span data-ttu-id="2f6f3-133">下面是主机操作系统和 ASP.NET Core 应用程序的安装任务概述。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-133">Here's an overview of setup tasks for the host OS and your ASP.NET Core application.</span></span>

### <a name="configure-windows-server"></a><span data-ttu-id="2f6f3-134">配置 Windows Server</span><span class="sxs-lookup"><span data-stu-id="2f6f3-134">Configure Windows Server</span></span>

* <span data-ttu-id="2f6f3-135">安装应用程序要求的 .NET 版本，例如 [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) 或 .NET Framework 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-135">Install the version of .NET that your application requires, such as [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) or .NET Framework 4.5.1.</span></span>

* <span data-ttu-id="2f6f3-136">预先注册 URL 前缀以绑定到 WebListener，并设置 SSL 证书</span><span class="sxs-lookup"><span data-stu-id="2f6f3-136">Preregister URL prefixes to bind to WebListener, and set up SSL certificates</span></span>

   <span data-ttu-id="2f6f3-137">如果在 Windows 中不预先注册 URL 前缀，则必须使用管理员权限运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-137">If you don't preregister URL prefixes in Windows, you have to run your application with administrator privileges.</span></span> <span data-ttu-id="2f6f3-138">唯一的例外是，如果你使用端口号大于 1024 的 HTTP（不是 HTTPS）绑定到 localhost，在这种情况下不需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-138">The only exception is if you bind to localhost using HTTP (not HTTPS) with a port number greater than 1024; in that case administrator privileges aren't required.</span></span>

   <span data-ttu-id="2f6f3-139">有关详细信息，请参阅本文后续部分的[如何预先注册前缀和配置 SSL](#preregister-url-prefixes-and-configure-ssl)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-139">For details, see [How to preregister prefixes and configure SSL](#preregister-url-prefixes-and-configure-ssl) later in this article.</span></span>

* <span data-ttu-id="2f6f3-140">打开防火墙端口以允许流量到达 WebListener。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-140">Open firewall ports to allow traffic to reach WebListener.</span></span>

   <span data-ttu-id="2f6f3-141">你可以使用 netsh.exe 或 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-141">You can use netsh.exe or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

<span data-ttu-id="2f6f3-142">此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-142">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>

### <a name="configure-your-aspnet-core-application"></a><span data-ttu-id="2f6f3-143">配置 ASP.NET Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="2f6f3-143">Configure your ASP.NET Core application</span></span>

* <span data-ttu-id="2f6f3-144">安装 NuGet 包 [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-144">Install the NuGet package [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/).</span></span> <span data-ttu-id="2f6f3-145">这还将安装 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) 作为依赖项。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-145">This also installs [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) as a dependency.</span></span>

* <span data-ttu-id="2f6f3-146">在 `Main` 方法中，调用 [WebHostBuilder](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) 上的 `UseWebListener` 扩展方法，指定所需的任何 WebListener [选项](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs)和[设置](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs)，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-146">Call the `UseWebListener` extension method on [WebHostBuilder](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) in your `Main` method, specifying any WebListener [options](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) and [settings](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs) that you need, as shown in the following example:</span></span>

  [!code-csharp[](weblistener/sample/Program.cs?name=snippet_Main&highlight=13-17)]

* <span data-ttu-id="2f6f3-147">配置要侦听的 Url 和端口</span><span class="sxs-lookup"><span data-stu-id="2f6f3-147">Configure URLs and ports to listen on</span></span> 

  <span data-ttu-id="2f6f3-148">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-148">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="2f6f3-149">若要配置 URL 前缀和端口，可以使用 `UseURLs` 扩展方法、`urls` 命令行参数或 ASP.NET Core 配置系统。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-149">To configure URL prefixes and ports, you can use the `UseURLs` extension method, the `urls` command-line argument or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="2f6f3-150">有关详细信息，请参阅[托管](../../fundamentals/hosting.md)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-150">For more information, see [Hosting](../../fundamentals/hosting.md).</span></span>

  <span data-ttu-id="2f6f3-151">Web 侦听器使用 [Http.Sys 前缀字符串格式](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-151">Web Listener uses the [Http.Sys prefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span> <span data-ttu-id="2f6f3-152">没有特定于 WebListener 的前缀字符串格式要求。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-152">There are no prefix string format requirements that are specific to WebListener.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2f6f3-153">请确保在服务器上预先注册的 `UseUrls` 中指定相同的前缀字符串。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-153">Make sure that you specify the same prefix strings in `UseUrls` that you preregister on the server.</span></span> 

* <span data-ttu-id="2f6f3-154">请确保应用程序未配置为运行 IIS 或 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-154">Make sure your application isn't configured to run IIS or IIS Express.</span></span>

  <span data-ttu-id="2f6f3-155">在 Visual Studio 中，默认启动配置文件是针对 IIS Express 的。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-155">In Visual Studio, the default launch profile is for IIS Express.</span></span>  <span data-ttu-id="2f6f3-156">若要作为控制台应用程序运行该项目，必须手动更改所选配置文件，如以下屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-156">To run the project as a console application you have to manually change the selected profile, as shown in the following screen shot.</span></span>

  ![选择控制台应用配置文件](weblistener/_static/vs-choose-profile.png)

## <a name="how-to-use-weblistener-outside-of-aspnet-core"></a><span data-ttu-id="2f6f3-158">如何在 ASP.NET Core 之外使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="2f6f3-158">How to use WebListener outside of ASP.NET Core</span></span>

* <span data-ttu-id="2f6f3-159">安装 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-159">Install the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

* <span data-ttu-id="2f6f3-160">[预先注册 URL 前缀以绑定到 WebListener，并设置 SSL 证书](#preregister-url-prefixes-and-configure-ssl)，因为在 ASP.NET Core 中会使用到。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-160">[Preregister URL prefixes to bind to WebListener, and set up SSL certificates](#preregister-url-prefixes-and-configure-ssl) as you would for use in ASP.NET Core.</span></span>

<span data-ttu-id="2f6f3-161">此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-161">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>


<span data-ttu-id="2f6f3-162">下面的代码示例演示在 ASP.NET Core 之外使用 WebListener：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-162">Here's a code sample that demonstrates WebListener use outside of ASP.NET Core:</span></span>

```csharp
var settings = new WebListenerSettings();
settings.UrlPrefixes.Add("http://localhost:8080");

using (WebListener listener = new WebListener(settings))
{
    listener.Start();

    while (true)
    {
        var context = await listener.AcceptAsync();
        byte[] bytes = Encoding.ASCII.GetBytes("Hello World: " + DateTime.Now);
        context.Response.ContentLength = bytes.Length;
        context.Response.ContentType = "text/plain";

        await context.Response.Body.WriteAsync(bytes, 0, bytes.Length);
        context.Dispose();
    }
}
```

## <a name="preregister-url-prefixes-and-configure-ssl"></a><span data-ttu-id="2f6f3-163">预先注册 URL 前缀和配置 SSL</span><span class="sxs-lookup"><span data-stu-id="2f6f3-163">Preregister URL prefixes and configure SSL</span></span>

<span data-ttu-id="2f6f3-164">IIS 和 WebListener 都依赖于基础 Http.Sys 内核模式驱动程序，以便侦听请求和执行初始化处理。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-164">Both IIS and WebListener rely on the underlying Http.Sys kernel mode driver to listen for requests and do initial processing.</span></span> <span data-ttu-id="2f6f3-165">在 IIS 中，管理 UI 提供一种相对简单的方法来配置所有内容。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-165">In IIS, the management UI gives you a relatively easy way to configure everything.</span></span> <span data-ttu-id="2f6f3-166">但是，如果正在使用 WebListener，则需要自行配置 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-166">However, if you're using WebListener you need to configure Http.Sys yourself.</span></span> <span data-ttu-id="2f6f3-167">执行该操作的内置工具是 netsh.exe。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-167">The built-in tool for doing that's netsh.exe.</span></span> 

<span data-ttu-id="2f6f3-168">需要用到 netsh.exe 的最常见的任务是保留 URL 前缀和分配 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-168">The most common tasks you need to use netsh.exe for are reserving URL prefixes and assigning SSL certificates.</span></span>

<span data-ttu-id="2f6f3-169">对于初学者来说，NetSh.exe 并不是一个简单的工具。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-169">NetSh.exe isn't an easy tool to use for beginners.</span></span> <span data-ttu-id="2f6f3-170">以下示例演示保留 80 和 443 端口的 URL 前缀所需的最低要求：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-170">The following example shows the bare minimum needed to reserve URL prefixes for ports 80 and 443:</span></span>

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

<span data-ttu-id="2f6f3-171">以下示例演示如何分配 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-171">The following example shows how to assign an SSL certificate:</span></span>

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}".
```

<span data-ttu-id="2f6f3-172">下面是官方的参考文档：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-172">Here is the official reference documentation:</span></span>

* <span data-ttu-id="2f6f3-173">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)（超文本传输协议 (HTTP) 的 Netsh 命令）</span><span class="sxs-lookup"><span data-stu-id="2f6f3-173">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)</span></span>
* <span data-ttu-id="2f6f3-174">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)（UrlPrefix 字符串）</span><span class="sxs-lookup"><span data-stu-id="2f6f3-174">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)</span></span>

<span data-ttu-id="2f6f3-175">以下资源提供几个方案的详细说明。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-175">The following resources provide detailed instructions for several scenarios.</span></span> <span data-ttu-id="2f6f3-176">涉及 `HttpListener` 的文章同样适用于 `WebListener`，因为两者都基于 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-176">Articles that refer to `HttpListener` apply equally to `WebListener`, as both are based on Http.Sys.</span></span>

* [<span data-ttu-id="2f6f3-177">如何：使用 SSL 证书配置端口</span><span class="sxs-lookup"><span data-stu-id="2f6f3-177">How to: Configure a Port with an SSL Certificate</span></span>](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* <span data-ttu-id="2f6f3-178">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html)（HTTPS 通信 - 基于 HttpListener 的托管和客户端证书）这是很久之前的一个第三方博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-178">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) This is a third-party blog and is fairly old but still has useful information.</span></span>
* <span data-ttu-id="2f6f3-179">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/)（如何：使用 HttpListener 或 Http 服务器非托管代码 (C++) 作为 SSL 简单服务器进行演练），这也是很久之前的一个博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-179">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) This too is an older blog with useful information.</span></span>
* <span data-ttu-id="2f6f3-180">[How Do I Set Up A .NET Core WebListener With SSL?](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)（如何使用 SSL 设置 .NET Core WebListener？）</span><span class="sxs-lookup"><span data-stu-id="2f6f3-180">[How Do I Set Up A .NET Core WebListener With SSL?](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)</span></span>

<span data-ttu-id="2f6f3-181">以下是一些比 netsh.exe 命令行更易使用的第三方工具。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-181">Here are some third-party tools that can be easier to use than the netsh.exe command line.</span></span> <span data-ttu-id="2f6f3-182">它们不是由 Microsoft 提供或认可的。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-182">These are not provided by or endorsed by Microsoft.</span></span> <span data-ttu-id="2f6f3-183">默认情况下，这些工具以管理员身份运行，因为 netsh.exe 本身需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-183">The tools run as administrator by default, since netsh.exe itself requires administrator privileges.</span></span>

* <span data-ttu-id="2f6f3-184">[http.sys 管理器](http://httpsysmanager.codeplex.com/)提供用于列出和配置 SSL 证书和选项、前缀保留和证书信任列表的 UI。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-184">[http.sys Manager](http://httpsysmanager.codeplex.com/) provides UI for listing and configuring SSL certificates and options, prefix reservations, and certificate trust lists.</span></span> 
* <span data-ttu-id="2f6f3-185">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) 允许用户列出或配置 SSL 证书和 URL 前缀。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-185">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) lets you list or configure SSL certificates and URL prefixes.</span></span> <span data-ttu-id="2f6f3-186">UI 比 http.sys 管理器更加完善并且提供更多的配置选项，但在其他方面它提供类似的功能。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-186">The UI is more refined than http.sys Manager and exposes a few more configuration options, but otherwise it provides similar functionality.</span></span> <span data-ttu-id="2f6f3-187">它不能创建新的证书信任列表 (CTL)，但可以分配现有证书信任列表。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-187">It cannot create a new certificate trust list (CTL), but can assign existing ones.</span></span>

<span data-ttu-id="2f6f3-188">为生成自签名 SSL 证书，Microsoft 提供命令行工具：[MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) 和 PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="2f6f3-188">For generating self-signed SSL certificates, Microsoft provides command-line tools: [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) and the PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate).</span></span> <span data-ttu-id="2f6f3-189">此外，还提供第三方 UI 工具，可让你更加轻松地生成自签名 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-189">There are also third-party UI tools that make it easier for you to generate self-signed SSL certificates:</span></span>

* [<span data-ttu-id="2f6f3-190">SelfCert</span><span class="sxs-lookup"><span data-stu-id="2f6f3-190">SelfCert</span></span>](https://www.pluralsight.com/blog/software-development/selfcert-create-a-self-signed-certificate-interactively-gui-or-programmatically-in-net)
* [<span data-ttu-id="2f6f3-191">Makecert UI</span><span class="sxs-lookup"><span data-stu-id="2f6f3-191">Makecert UI</span></span>](http://makecertui.codeplex.com/)

## <a name="next-steps"></a><span data-ttu-id="2f6f3-192">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2f6f3-192">Next steps</span></span>

<span data-ttu-id="2f6f3-193">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="2f6f3-193">For more information, see the following resources:</span></span>

* [<span data-ttu-id="2f6f3-194">本文的示例应用</span><span class="sxs-lookup"><span data-stu-id="2f6f3-194">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)
* [<span data-ttu-id="2f6f3-195">WebListener 源代码</span><span class="sxs-lookup"><span data-stu-id="2f6f3-195">WebListener source code</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="2f6f3-196">承载</span><span class="sxs-lookup"><span data-stu-id="2f6f3-196">Hosting</span></span>](../hosting.md)
