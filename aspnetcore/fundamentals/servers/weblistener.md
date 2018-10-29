---
title: ASP.NET Core 中的 WebListener Web 服务器实现
author: rick-anderson
description: 了解 WebListener，它是 Windows 上 ASP.NET Core 的 Web 服务器，可用于无需 IIS，直接连接到 Internet。
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: fundamentals/servers/weblistener
ms.openlocfilehash: 5d72672cc48243f8ee17df615e3379143ed868f6
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206437"
---
# <a name="weblistener-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="f0799-103">ASP.NET Core 中的 WebListener Web 服务器实现</span><span class="sxs-lookup"><span data-stu-id="f0799-103">WebListener web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="f0799-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="f0799-104">By [Tom Dykstra](https://github.com/tdykstra) and [Chris Ross](https://github.com/Tratcher)</span></span>

> [!NOTE]
> <span data-ttu-id="f0799-105">本主题仅适用于 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="f0799-105">This topic applies only to ASP.NET Core 1.x.</span></span> <span data-ttu-id="f0799-106">在 ASP.NET Core 2.0 中，WebListener 被命名为 [HTTP.sys](httpsys.md)。</span><span class="sxs-lookup"><span data-stu-id="f0799-106">In ASP.NET Core 2.0, WebListener is named [HTTP.sys](httpsys.md).</span></span>

<span data-ttu-id="f0799-107">WebListener 是仅在 Windows 上运行的[适用于 ASP.NET Core 的 Web 服务器](index.md)。</span><span class="sxs-lookup"><span data-stu-id="f0799-107">WebListener is a [web server for ASP.NET Core](index.md) that runs only on Windows.</span></span> <span data-ttu-id="f0799-108">它构建于 [Http.Sys 内核模式驱动程序](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)之上。</span><span class="sxs-lookup"><span data-stu-id="f0799-108">It's built on the [Http.Sys kernel mode driver](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="f0799-109">WebListener 是 [Kestrel](kestrel.md) 的一种替代选择，可用来直接连接到 Internet，而无需依赖 IIS 作为反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="f0799-109">WebListener is an alternative to [Kestrel](kestrel.md) that can be used for direct connection to the Internet without relying on IIS as a reverse proxy server.</span></span> <span data-ttu-id="f0799-110">事实上，WebListener 不能与 IIS 或 IIS Express 结合使用，因为它与 [ASP.NET Core 模块](aspnet-core-module.md)不兼容。</span><span class="sxs-lookup"><span data-stu-id="f0799-110">In fact, **WebListener can't be used with IIS or IIS Express, as it isn't compatible with the [ASP.NET Core Module](aspnet-core-module.md).**</span></span>

<span data-ttu-id="f0799-111">尽管 ASP.NET Core 针对 WebListener 开发，但是它可以通过 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 包直接在任何 .NET Core 或 .NET Framework 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="f0799-111">Although WebListener was developed for ASP.NET Core, it can be used directly in any .NET Core or .NET Framework application via the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

<span data-ttu-id="f0799-112">WebListener 支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="f0799-112">WebListener supports the following features:</span></span>

- [<span data-ttu-id="f0799-113">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="f0799-113">Windows Authentication</span></span>](xref:security/authentication/windowsauth)
- <span data-ttu-id="f0799-114">端口共享</span><span class="sxs-lookup"><span data-stu-id="f0799-114">Port sharing</span></span>
- <span data-ttu-id="f0799-115">具有 SNI 的 HTTPS</span><span class="sxs-lookup"><span data-stu-id="f0799-115">HTTPS with SNI</span></span>
- <span data-ttu-id="f0799-116">基于 TLS 的 HTTP/2 (Windows 10)</span><span class="sxs-lookup"><span data-stu-id="f0799-116">HTTP/2 over TLS (Windows 10)</span></span>
- <span data-ttu-id="f0799-117">直接文件传输</span><span class="sxs-lookup"><span data-stu-id="f0799-117">Direct file transmission</span></span>
- <span data-ttu-id="f0799-118">响应缓存</span><span class="sxs-lookup"><span data-stu-id="f0799-118">Response caching</span></span>
- <span data-ttu-id="f0799-119">WebSocket (Windows 8)</span><span class="sxs-lookup"><span data-stu-id="f0799-119">WebSockets (Windows 8)</span></span>

<span data-ttu-id="f0799-120">受支持的 Windows 版本：</span><span class="sxs-lookup"><span data-stu-id="f0799-120">Supported Windows versions:</span></span>

- <span data-ttu-id="f0799-121">Windows 7 和 Windows Server 2008 R2 及更高版本</span><span class="sxs-lookup"><span data-stu-id="f0799-121">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="f0799-122">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="f0799-122">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-weblistener"></a><span data-ttu-id="f0799-123">何时使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="f0799-123">When to use WebListener</span></span>

<span data-ttu-id="f0799-124">WebListener 对于在无需使用 IIS 的情况下直接向 Internet 公开服务器的部署非常有用。</span><span class="sxs-lookup"><span data-stu-id="f0799-124">WebListener is useful for deployments where you need to expose the server directly to the Internet without using IIS.</span></span>

![Weblistener 直接与 Internet 进行通信](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="f0799-126">由于 WebListener 构建于 Http.Sys 之上，因此它不需要反向代理服务器来抵御攻击。</span><span class="sxs-lookup"><span data-stu-id="f0799-126">Because it's built on Http.Sys, WebListener doesn't require a reverse proxy server for protection against attacks.</span></span> <span data-ttu-id="f0799-127">Http.Sys 是一项成熟的技术，可以抵御多种攻击，并提供可靠、安全、可伸缩的全功能 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f0799-127">Http.Sys is mature technology that protects against many kinds of attacks and provides the robustness, security, and scalability of a full-featured web server.</span></span> <span data-ttu-id="f0799-128">IIS 本身作为 Http.Sys 之上的 HTTP 侦听器运行。</span><span class="sxs-lookup"><span data-stu-id="f0799-128">IIS itself runs as an HTTP listener on top of Http.Sys.</span></span>

<span data-ttu-id="f0799-129">当你无法通过 Kestrel 获取它提供的某个功能时，WebListener 对于内部部署也是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="f0799-129">WebListener is also a good choice for internal deployments when you need one of the features it offers that you can't get by using Kestrel.</span></span>

![Weblistener 直接与你的内部网络进行通信](weblistener/_static/weblistener-to-internal.png)

## <a name="kernel-mode-authentication-with-kerberos"></a><span data-ttu-id="f0799-131">对 Kerberos 进行内核模式身份验证</span><span class="sxs-lookup"><span data-stu-id="f0799-131">Kernel mode authentication with Kerberos</span></span>

<span data-ttu-id="f0799-132">WebListener 通过 Kerberos 身份验证协议委托给内核模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="f0799-132">WebListener delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="f0799-133">Kerberos 和 WebListener 不支持用户模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="f0799-133">User mode authentication isn't supported with Kerberos and WebListener.</span></span> <span data-ttu-id="f0799-134">必须使用计算机帐户来解密从 Active Directory 获取的并由客户端转发到服务器的 Kerberos 令牌/票证，以便对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="f0799-134">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="f0799-135">注册主机的服务主体名称 (SPN)，而不是应用的用户。</span><span class="sxs-lookup"><span data-stu-id="f0799-135">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

## <a name="how-to-use-weblistener"></a><span data-ttu-id="f0799-136">如何使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="f0799-136">How to use WebListener</span></span>

<span data-ttu-id="f0799-137">下面是主机操作系统和 ASP.NET Core 应用程序的安装任务概述。</span><span class="sxs-lookup"><span data-stu-id="f0799-137">Here's an overview of setup tasks for the host OS and your ASP.NET Core application.</span></span>

### <a name="configure-windows-server"></a><span data-ttu-id="f0799-138">配置 Windows Server</span><span class="sxs-lookup"><span data-stu-id="f0799-138">Configure Windows Server</span></span>

* <span data-ttu-id="f0799-139">安装应用程序要求的 .NET 版本，例如 [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) 或 .NET Framework 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="f0799-139">Install the version of .NET that your application requires, such as [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) or .NET Framework 4.5.1.</span></span>

* <span data-ttu-id="f0799-140">预先注册 URL 前缀以绑定到 WebListener，并设置 SSL 证书</span><span class="sxs-lookup"><span data-stu-id="f0799-140">Preregister URL prefixes to bind to WebListener, and set up SSL certificates</span></span>

   <span data-ttu-id="f0799-141">如果在 Windows 中不预先注册 URL 前缀，则必须使用管理员权限运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f0799-141">If you don't preregister URL prefixes in Windows, you have to run your application with administrator privileges.</span></span> <span data-ttu-id="f0799-142">唯一的例外是，如果你使用端口号大于 1024 的 HTTP（不是 HTTPS）绑定到 localhost，在这种情况下不需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="f0799-142">The only exception is if you bind to localhost using HTTP (not HTTPS) with a port number greater than 1024; in that case administrator privileges aren't required.</span></span>

   <span data-ttu-id="f0799-143">有关详细信息，请参阅本文后续部分的[如何预先注册前缀和配置 SSL](#preregister-url-prefixes-and-configure-ssl)。</span><span class="sxs-lookup"><span data-stu-id="f0799-143">For details, see [How to preregister prefixes and configure SSL](#preregister-url-prefixes-and-configure-ssl) later in this article.</span></span>

* <span data-ttu-id="f0799-144">打开防火墙端口以允许流量到达 WebListener。</span><span class="sxs-lookup"><span data-stu-id="f0799-144">Open firewall ports to allow traffic to reach WebListener.</span></span>

   <span data-ttu-id="f0799-145">你可以使用 netsh.exe 或 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)。</span><span class="sxs-lookup"><span data-stu-id="f0799-145">You can use netsh.exe or [PowerShell cmdlets](https://technet.microsoft.com/library/jj554906).</span></span>

<span data-ttu-id="f0799-146">此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。</span><span class="sxs-lookup"><span data-stu-id="f0799-146">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>

### <a name="configure-your-aspnet-core-application"></a><span data-ttu-id="f0799-147">配置 ASP.NET Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="f0799-147">Configure your ASP.NET Core application</span></span>

* <span data-ttu-id="f0799-148">安装 NuGet 包 [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/)。</span><span class="sxs-lookup"><span data-stu-id="f0799-148">Install the NuGet package [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/).</span></span> <span data-ttu-id="f0799-149">这还将安装 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) 作为依赖项。</span><span class="sxs-lookup"><span data-stu-id="f0799-149">This also installs [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) as a dependency.</span></span>

* <span data-ttu-id="f0799-150">在 `Main` 方法中，调用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 上的 `UseWebListener` 扩展方法，指定所需的任何 WebListener [选项](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs)和[设置](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs)，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f0799-150">Call the `UseWebListener` extension method on [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) in your `Main` method, specifying any WebListener [options](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) and [settings](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs) that you need, as shown in the following example:</span></span>

  [!code-csharp[](weblistener/sample/Program.cs?name=snippet_Main&highlight=13-17)]

* <span data-ttu-id="f0799-151">配置要侦听的 URL 和端口</span><span class="sxs-lookup"><span data-stu-id="f0799-151">Configure URLs and ports to listen on</span></span> 

  <span data-ttu-id="f0799-152">默认情况下，ASP.NET Core 绑定到 `http://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="f0799-152">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="f0799-153">若要配置 URL 前缀和端口，可以使用 `UseURLs` 扩展方法、`urls` 命令行参数或 ASP.NET Core 配置系统。</span><span class="sxs-lookup"><span data-stu-id="f0799-153">To configure URL prefixes and ports, you can use the `UseURLs` extension method, the `urls` command-line argument or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="f0799-154">有关详细信息，请参阅[在 ASP.NET Core 中托管(xref:fundamentals/host/index)。</span><span class="sxs-lookup"><span data-stu-id="f0799-154">For more information, see [Host in ASP.NET Core(xref:fundamentals/host/index).</span></span>

  <span data-ttu-id="f0799-155">Web 侦听器使用 [Http.Sys 前缀字符串格式](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f0799-155">Web Listener uses the [Http.Sys prefix string formats](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx).</span></span> <span data-ttu-id="f0799-156">没有特定于 WebListener 的前缀字符串格式要求。</span><span class="sxs-lookup"><span data-stu-id="f0799-156">There are no prefix string format requirements that are specific to WebListener.</span></span>

  > [!WARNING]
  > <span data-ttu-id="f0799-157">不应使用顶级通配符绑定（`http://*:80/` 和 `http://+:80`）。</span><span class="sxs-lookup"><span data-stu-id="f0799-157">Top-level wildcard bindings (`http://*:80/` and `http://+:80`) should **not** be used.</span></span> <span data-ttu-id="f0799-158">顶级通配符绑定可能会为应用带来安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="f0799-158">Top-level wildcard bindings can open up your app to security vulnerabilities.</span></span> <span data-ttu-id="f0799-159">此行为同时适用于强通配符和弱通配符。</span><span class="sxs-lookup"><span data-stu-id="f0799-159">This applies to both strong and weak wildcards.</span></span> <span data-ttu-id="f0799-160">使用显式主机名而不是通配符。</span><span class="sxs-lookup"><span data-stu-id="f0799-160">Use explicit host names rather than wildcards.</span></span> <span data-ttu-id="f0799-161">如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.mysub.com`）不具有此安全风险。</span><span class="sxs-lookup"><span data-stu-id="f0799-161">Subdomain wildcard binding (for example, `*.mysub.com`) doesn't have this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="f0799-162">有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。</span><span class="sxs-lookup"><span data-stu-id="f0799-162">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f0799-163">请确保在服务器上预先注册的 `UseUrls` 中指定相同的前缀字符串。</span><span class="sxs-lookup"><span data-stu-id="f0799-163">Make sure that you specify the same prefix strings in `UseUrls` that you preregister on the server.</span></span> 

* <span data-ttu-id="f0799-164">请确保应用程序未配置为运行 IIS 或 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="f0799-164">Make sure your application isn't configured to run IIS or IIS Express.</span></span>

  <span data-ttu-id="f0799-165">在 Visual Studio 中，默认启动配置文件是针对 IIS Express 的。</span><span class="sxs-lookup"><span data-stu-id="f0799-165">In Visual Studio, the default launch profile is for IIS Express.</span></span>  <span data-ttu-id="f0799-166">若要作为控制台应用程序运行该项目，必须手动更改所选配置文件，如以下屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="f0799-166">To run the project as a console application you have to manually change the selected profile, as shown in the following screen shot.</span></span>

  ![选择控制台应用配置文件](weblistener/_static/vs-choose-profile.png)

## <a name="how-to-use-weblistener-outside-of-aspnet-core"></a><span data-ttu-id="f0799-168">如何在 ASP.NET Core 之外使用 WebListener</span><span class="sxs-lookup"><span data-stu-id="f0799-168">How to use WebListener outside of ASP.NET Core</span></span>

* <span data-ttu-id="f0799-169">安装 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f0799-169">Install the [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet package.</span></span>

* <span data-ttu-id="f0799-170">[预先注册 URL 前缀以绑定到 WebListener，并设置 SSL 证书](#preregister-url-prefixes-and-configure-ssl)，因为在 ASP.NET Core 中会使用到。</span><span class="sxs-lookup"><span data-stu-id="f0799-170">[Preregister URL prefixes to bind to WebListener, and set up SSL certificates](#preregister-url-prefixes-and-configure-ssl) as you would for use in ASP.NET Core.</span></span>

<span data-ttu-id="f0799-171">此外，还有 [Http.Sys 注册表设置](https://support.microsoft.com/kb/820129)。</span><span class="sxs-lookup"><span data-stu-id="f0799-171">There are also [Http.Sys registry settings](https://support.microsoft.com/kb/820129).</span></span>


<span data-ttu-id="f0799-172">下面的代码示例演示在 ASP.NET Core 之外使用 WebListener：</span><span class="sxs-lookup"><span data-stu-id="f0799-172">Here's a code sample that demonstrates WebListener use outside of ASP.NET Core:</span></span>

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

## <a name="preregister-url-prefixes-and-configure-ssl"></a><span data-ttu-id="f0799-173">预先注册 URL 前缀和配置 SSL</span><span class="sxs-lookup"><span data-stu-id="f0799-173">Preregister URL prefixes and configure SSL</span></span>

<span data-ttu-id="f0799-174">IIS 和 WebListener 都依赖于基础 Http.Sys 内核模式驱动程序，以便侦听请求和执行初始化处理。</span><span class="sxs-lookup"><span data-stu-id="f0799-174">Both IIS and WebListener rely on the underlying Http.Sys kernel mode driver to listen for requests and do initial processing.</span></span> <span data-ttu-id="f0799-175">在 IIS 中，管理 UI 提供一种相对简单的方法来配置所有内容。</span><span class="sxs-lookup"><span data-stu-id="f0799-175">In IIS, the management UI gives you a relatively easy way to configure everything.</span></span> <span data-ttu-id="f0799-176">但是，如果正在使用 WebListener，则需要自行配置 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="f0799-176">However, if you're using WebListener you need to configure Http.Sys yourself.</span></span> <span data-ttu-id="f0799-177">执行该操作的内置工具是 netsh.exe。</span><span class="sxs-lookup"><span data-stu-id="f0799-177">The built-in tool for doing that's netsh.exe.</span></span> 

<span data-ttu-id="f0799-178">需要用到 netsh.exe 的最常见的任务是保留 URL 前缀和分配 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="f0799-178">The most common tasks you need to use netsh.exe for are reserving URL prefixes and assigning SSL certificates.</span></span>

<span data-ttu-id="f0799-179">对于初学者来说，NetSh.exe 并不是一个简单的工具。</span><span class="sxs-lookup"><span data-stu-id="f0799-179">NetSh.exe isn't an easy tool to use for beginners.</span></span> <span data-ttu-id="f0799-180">以下示例演示保留 80 和 443 端口的 URL 前缀所需的最低要求：</span><span class="sxs-lookup"><span data-stu-id="f0799-180">The following example shows the bare minimum needed to reserve URL prefixes for ports 80 and 443:</span></span>

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

<span data-ttu-id="f0799-181">以下示例演示如何分配 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="f0799-181">The following example shows how to assign an SSL certificate:</span></span>

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid="{00000000-0000-0000-0000-000000000000}".
```

<span data-ttu-id="f0799-182">下面是官方的参考文档：</span><span class="sxs-lookup"><span data-stu-id="f0799-182">Here is the official reference documentation:</span></span>

* <span data-ttu-id="f0799-183">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)（超文本传输协议 (HTTP) 的 Netsh 命令）</span><span class="sxs-lookup"><span data-stu-id="f0799-183">[Netsh Commands for Hypertext Transfer Protocol (HTTP)](https://technet.microsoft.com/library/cc725882.aspx)</span></span>
* <span data-ttu-id="f0799-184">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)（UrlPrefix 字符串）</span><span class="sxs-lookup"><span data-stu-id="f0799-184">[UrlPrefix Strings](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)</span></span>

<span data-ttu-id="f0799-185">以下资源提供几个方案的详细说明。</span><span class="sxs-lookup"><span data-stu-id="f0799-185">The following resources provide detailed instructions for several scenarios.</span></span> <span data-ttu-id="f0799-186">涉及 `HttpListener` 的文章同样适用于 `WebListener`，因为两者都基于 Http.Sys。</span><span class="sxs-lookup"><span data-stu-id="f0799-186">Articles that refer to `HttpListener` apply equally to `WebListener`, as both are based on Http.Sys.</span></span>

* [<span data-ttu-id="f0799-187">如何：使用 SSL 证书配置端口</span><span class="sxs-lookup"><span data-stu-id="f0799-187">How to: Configure a Port with an SSL Certificate</span></span>](/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* <span data-ttu-id="f0799-188">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html)（HTTPS 通信 - 基于 HttpListener 的托管和客户端证书）这是很久之前的一个第三方博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="f0799-188">[HTTPS Communication - HttpListener based Hosting and Client Certification](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) This is a third-party blog and is fairly old but still has useful information.</span></span>
* <span data-ttu-id="f0799-189">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/)（如何：使用 HttpListener 或 Http 服务器非托管代码 (C++) 作为 SSL 简单服务器进行演练），这也是很久之前的一个博客，但仍有一些有用的信息。</span><span class="sxs-lookup"><span data-stu-id="f0799-189">[How To: Walkthrough Using HttpListener or Http Server unmanaged code (C++) as an SSL Simple Server](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) This too is an older blog with useful information.</span></span>
* <span data-ttu-id="f0799-190">[How Do I Set Up A .NET Core WebListener With SSL?](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)（如何使用 SSL 设置 .NET Core WebListener？）</span><span class="sxs-lookup"><span data-stu-id="f0799-190">[How Do I Set Up A .NET Core WebListener With SSL?](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)</span></span>

<span data-ttu-id="f0799-191">以下是一些比 netsh.exe 命令行更易使用的第三方工具。</span><span class="sxs-lookup"><span data-stu-id="f0799-191">Here are some third-party tools that can be easier to use than the netsh.exe command line.</span></span> <span data-ttu-id="f0799-192">它们不是由 Microsoft 提供或认可的。</span><span class="sxs-lookup"><span data-stu-id="f0799-192">These are not provided by or endorsed by Microsoft.</span></span> <span data-ttu-id="f0799-193">默认情况下，这些工具以管理员身份运行，因为 netsh.exe 本身需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="f0799-193">The tools run as administrator by default, since netsh.exe itself requires administrator privileges.</span></span>

* <span data-ttu-id="f0799-194">[http.sys 管理器](http://httpsysmanager.codeplex.com/)提供用于列出和配置 SSL 证书和选项、前缀预留和证书信任列表的 UI。</span><span class="sxs-lookup"><span data-stu-id="f0799-194">[http.sys Manager](http://httpsysmanager.codeplex.com/) provides UI for listing and configuring SSL certificates and options, prefix reservations, and certificate trust lists.</span></span> 
* <span data-ttu-id="f0799-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) 允许用户列出或配置 SSL 证书和 URL 前缀。</span><span class="sxs-lookup"><span data-stu-id="f0799-195">[HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) lets you list or configure SSL certificates and URL prefixes.</span></span> <span data-ttu-id="f0799-196">UI 比 http.sys 管理器更加完善并且提供更多的配置选项，但在其他方面它提供类似的功能。</span><span class="sxs-lookup"><span data-stu-id="f0799-196">The UI is more refined than http.sys Manager and exposes a few more configuration options, but otherwise it provides similar functionality.</span></span> <span data-ttu-id="f0799-197">它不能创建新的证书信任列表 (CTL)，但可以分配现有证书信任列表。</span><span class="sxs-lookup"><span data-stu-id="f0799-197">It cannot create a new certificate trust list (CTL), but can assign existing ones.</span></span>

<span data-ttu-id="f0799-198">为生成自签名 SSL 证书，Microsoft 提供命令行工具：[MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) 和 PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="f0799-198">For generating self-signed SSL certificates, Microsoft provides command-line tools: [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) and the PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate).</span></span> <span data-ttu-id="f0799-199">此外，还提供第三方 UI 工具，可让你更加轻松地生成自签名 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="f0799-199">There are also third-party UI tools that make it easier for you to generate self-signed SSL certificates:</span></span>

* [<span data-ttu-id="f0799-200">SelfCert</span><span class="sxs-lookup"><span data-stu-id="f0799-200">SelfCert</span></span>](https://www.pluralsight.com/blog/software-development/selfcert-create-a-self-signed-certificate-interactively-gui-or-programmatically-in-net)
* [<span data-ttu-id="f0799-201">Makecert UI</span><span class="sxs-lookup"><span data-stu-id="f0799-201">Makecert UI</span></span>](http://makecertui.codeplex.com/)

## <a name="next-steps"></a><span data-ttu-id="f0799-202">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f0799-202">Next steps</span></span>

<span data-ttu-id="f0799-203">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="f0799-203">For more information, see the following resources:</span></span>

* [<span data-ttu-id="f0799-204">本文的示例应用</span><span class="sxs-lookup"><span data-stu-id="f0799-204">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)
* [<span data-ttu-id="f0799-205">WebListener 源代码</span><span class="sxs-lookup"><span data-stu-id="f0799-205">WebListener source code</span></span>](https://github.com/aspnet/HttpSysServer/)
* [<span data-ttu-id="f0799-206">承载</span><span class="sxs-lookup"><span data-stu-id="f0799-206">Hosting</span></span>](xref:fundamentals/host/index)
