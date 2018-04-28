---
title: 使用 IIS 在 Windows 上托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows Server Internet Information Services (IIS) 上托管 ASP.NET Core 应用。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/index
ms.openlocfilehash: 9f164b6e1f3cc520b704cbb5ffdaadb99cebdc57
ms.sourcegitcommit: 01db73f2f7ac22b11ea48a947131d6176b0fe9ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="host-aspnet-core-on-windows-with-iis"></a><span data-ttu-id="2a047-103">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2a047-103">Host ASP.NET Core on Windows with IIS</span></span>

<span data-ttu-id="2a047-104">作者：[Luke Latham](https://github.com/guardrex) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2a047-104">By [Luke Latham](https://github.com/guardrex) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="2a047-105">支持的操作系统</span><span class="sxs-lookup"><span data-stu-id="2a047-105">Supported operating systems</span></span>

<span data-ttu-id="2a047-106">支持下列操作系统：</span><span class="sxs-lookup"><span data-stu-id="2a047-106">The following operating systems are supported:</span></span>

* <span data-ttu-id="2a047-107">Windows 7 或更高版本</span><span class="sxs-lookup"><span data-stu-id="2a047-107">Windows 7 or later</span></span>
* <span data-ttu-id="2a047-108">Windows Server 2008 R2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="2a047-108">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="2a047-109">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）在使用 IIS 的反向代理配置中不起作用。</span><span class="sxs-lookup"><span data-stu-id="2a047-109">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)) doesn't work in a reverse proxy configuration with IIS.</span></span> <span data-ttu-id="2a047-110">请使用 [Kestrel 服务器](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="2a047-110">Use the [Kestrel server](xref:fundamentals/servers/kestrel).</span></span>

## <a name="application-configuration"></a><span data-ttu-id="2a047-111">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="2a047-111">Application configuration</span></span>

### <a name="enable-the-iisintegration-components"></a><span data-ttu-id="2a047-112">启用 IISIntegration 组件</span><span class="sxs-lookup"><span data-stu-id="2a047-112">Enable the IISIntegration components</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2a047-113">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2a047-113">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="2a047-114">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机。</span><span class="sxs-lookup"><span data-stu-id="2a047-114">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to begin setting up a host.</span></span> <span data-ttu-id="2a047-115">`CreateDefaultBuilder` 将 [Kestrel](xref:fundamentals/servers/kestrel) 配置为 Web 服务器，并通过配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)的基路径和端口来实现 IIS 集成：</span><span class="sxs-lookup"><span data-stu-id="2a047-115">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module):</span></span>

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

<span data-ttu-id="2a047-116">ASP.NET Core 模块生成分配给后端进程的动态端口。</span><span class="sxs-lookup"><span data-stu-id="2a047-116">The ASP.NET Core Module generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="2a047-117">`UseIISIntegration` 方法获取该动态端口，并将 Kestrel 配置为侦听 `http://localhost:{dynamicPort}/`。</span><span class="sxs-lookup"><span data-stu-id="2a047-117">The `UseIISIntegration` method picks up the dynamic port and configures Kestrel to listen on `http://localhost:{dynamicPort}/`.</span></span> <span data-ttu-id="2a047-118">这将替代其他 URL 配置，如对 `UseUrls` 或 [Kestrel 的侦听 API](xref:fundamentals/servers/kestrel#endpoint-configuration) 的调用。</span><span class="sxs-lookup"><span data-stu-id="2a047-118">This overrides other URL configurations, such as calls to `UseUrls` or [Kestrel's Listen API](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span> <span data-ttu-id="2a047-119">因此，使用模块时，不需要调用 `UseUrls` 或 Kestrel 的 `Listen` API。</span><span class="sxs-lookup"><span data-stu-id="2a047-119">Therefore, calls to `UseUrls` or Kestrel's `Listen` API aren't required when using the module.</span></span> <span data-ttu-id="2a047-120">如果调用 `UseUrls` 或 `Listen`，则 Kestrel 会侦听在没有 IIS 的情况下运行应用时指定的端口。</span><span class="sxs-lookup"><span data-stu-id="2a047-120">If `UseUrls` or `Listen` is called, Kestrel listens on the port specified when running the app without IIS.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2a047-121">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2a047-121">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2a047-122">在应用依赖项中加入对 [Microsoft.AspNetCore.Server.IISIntegration ](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="2a047-122">Include a dependency on the [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package in the app's dependencies.</span></span> <span data-ttu-id="2a047-123">通过向 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 添加 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 扩展方法来使用 IIS 集成中间件：</span><span class="sxs-lookup"><span data-stu-id="2a047-123">Use IIS Integration middleware by adding the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) extension method to [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder):</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<span data-ttu-id="2a047-124">同时需要 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 和 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration)。</span><span class="sxs-lookup"><span data-stu-id="2a047-124">Both [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) and [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) are required.</span></span> <span data-ttu-id="2a047-125">调用 `UseIISIntegration` 的代码不会影响代码可移植性。</span><span class="sxs-lookup"><span data-stu-id="2a047-125">Code calling `UseIISIntegration` doesn't affect code portability.</span></span> <span data-ttu-id="2a047-126">如果应用不在 IIS 后面运行（例如，应用直接在 Kestrel 上运行），则 `UseIISIntegration` 不会运行。</span><span class="sxs-lookup"><span data-stu-id="2a047-126">If the app isn't run behind IIS (for example, the app is run directly on Kestrel), `UseIISIntegration` doesn't operate.</span></span>

<span data-ttu-id="2a047-127">ASP.NET Core 模块生成分配给后端进程的动态端口。</span><span class="sxs-lookup"><span data-stu-id="2a047-127">The ASP.NET Core Module generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="2a047-128">`UseIISIntegration` 方法获取该动态端口，并将 Kestrel 配置为侦听 `http://locahost:{dynamicPort}/`。</span><span class="sxs-lookup"><span data-stu-id="2a047-128">The `UseIISIntegration` method picks up the dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="2a047-129">这将替代其他 URL 配置，如对 `UseUrls` 的调用。</span><span class="sxs-lookup"><span data-stu-id="2a047-129">This overrides other URL configurations, such as calls to `UseUrls`.</span></span> <span data-ttu-id="2a047-130">因此，使用模块时无需调用 `UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="2a047-130">Therefore, a call to `UseUrls` isn't required when using the module.</span></span> <span data-ttu-id="2a047-131">如果调用 `UseUrls`，则 Kestrel 会侦听在没有 IIS 的情况下运行应用时指定的端口。</span><span class="sxs-lookup"><span data-stu-id="2a047-131">If `UseUrls` is called, Kestrel listens on the port specified when running the app without IIS.</span></span>

<span data-ttu-id="2a047-132">如果在 ASP.NET Core 1.0 应用中调用 `UseUrls`，请在调用 `UseIISIntegration` 前调用它，使模块配置的端口不会被覆盖。</span><span class="sxs-lookup"><span data-stu-id="2a047-132">If `UseUrls` is called in an ASP.NET Core 1.0 app, call it **before** calling `UseIISIntegration` so that the module-configured port isn't overwritten.</span></span> <span data-ttu-id="2a047-133">ASP.NET Core 1.1 不需要此调用顺序，因为模块设置会重写 `UseUrls`。</span><span class="sxs-lookup"><span data-stu-id="2a047-133">This calling order isn't required with ASP.NET Core 1.1 because the module setting overrides `UseUrls`.</span></span>

---

<span data-ttu-id="2a047-134">有关托管的详细信息，请参阅 [ASP.NET Core 中的托管](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="2a047-134">For more information on hosting, see [Hosting in ASP.NET Core](xref:fundamentals/hosting).</span></span>

### <a name="iis-options"></a><span data-ttu-id="2a047-135">IIS 选项</span><span class="sxs-lookup"><span data-stu-id="2a047-135">IIS options</span></span>

<span data-ttu-id="2a047-136">若要配置 IIS 选项，请在 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices) 中加入适用于 [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions) 的服务配置。</span><span class="sxs-lookup"><span data-stu-id="2a047-136">To configure IIS options, include a service configuration for [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions) in [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices).</span></span> <span data-ttu-id="2a047-137">在下面的示例中，禁用将客户端证书转发到应用以填充 `HttpContext.Connection.ClientCertificate`：</span><span class="sxs-lookup"><span data-stu-id="2a047-137">In the following example, forwarding client certificates to the app to populate `HttpContext.Connection.ClientCertificate` is disabled:</span></span>

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| <span data-ttu-id="2a047-138">选项</span><span class="sxs-lookup"><span data-stu-id="2a047-138">Option</span></span>                         | <span data-ttu-id="2a047-139">默认</span><span class="sxs-lookup"><span data-stu-id="2a047-139">Default</span></span> | <span data-ttu-id="2a047-140">设置</span><span class="sxs-lookup"><span data-stu-id="2a047-140">Setting</span></span> |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="2a047-141">若为 `true`，IIS 集成中间件将设置经过 [Windows 身份验证](xref:security/authentication/windowsauth)进行身份验证的 `HttpContext.User`。</span><span class="sxs-lookup"><span data-stu-id="2a047-141">If `true`, IIS Integration Middleware sets the `HttpContext.User` authenticated by [Windows Authentication](xref:security/authentication/windowsauth).</span></span> <span data-ttu-id="2a047-142">若为 `false`，中间件仅提供 `HttpContext.User` 的标识并在 `AuthenticationScheme` 显式请求时响应质询。</span><span class="sxs-lookup"><span data-stu-id="2a047-142">If `false`, the middleware only provides an identity for `HttpContext.User` and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="2a047-143">必须在 IIS 中启用 Windows 身份验证使 `AutomaticAuthentication` 得以运行。</span><span class="sxs-lookup"><span data-stu-id="2a047-143">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> <span data-ttu-id="2a047-144">有关详细信息，请参阅 [Windows 身份验证](xref:security/authentication/windowsauth)主题。</span><span class="sxs-lookup"><span data-stu-id="2a047-144">For more information, see the [Windows Authentication](xref:security/authentication/windowsauth) topic.</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="2a047-145">设置在登录页上向用户显示的显示名。</span><span class="sxs-lookup"><span data-stu-id="2a047-145">Sets the display name shown to users on login pages.</span></span> |
| `ForwardClientCertificate`     | `true`  | <span data-ttu-id="2a047-146">若为 `true`，且存在 `MS-ASPNETCORE-CLIENTCERT` 请求头，则填充 `HttpContext.Connection.ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="2a047-146">If `true` and the `MS-ASPNETCORE-CLIENTCERT` request header is present, the `HttpContext.Connection.ClientCertificate` is populated.</span></span> |

### <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="2a047-147">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="2a047-147">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="2a047-148">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="2a047-148">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="2a047-149">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="2a047-149">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="2a047-150">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="2a047-150">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="webconfig-file"></a><span data-ttu-id="2a047-151">web.config 文件</span><span class="sxs-lookup"><span data-stu-id="2a047-151">web.config file</span></span>

<span data-ttu-id="2a047-152">web.config 文件配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2a047-152">The *web.config* file configures the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="2a047-153">web.config 的创建、转换和发布 由 .NET Core Web SDK (`Microsoft.NET.Sdk.Web`) 处理。</span><span class="sxs-lookup"><span data-stu-id="2a047-153">Creating, transforming, and publishing *web.config* is handled by the .NET Core Web SDK (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="2a047-154">SDK 设置在项目文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="2a047-154">The SDK is set  at the top of the project file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

<span data-ttu-id="2a047-155">如果项目中不存在 web.config 文件，则会使用正确的 processPath 和参数创建该文件，以便配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，并将该文件移动到[已发布的输出](xref:host-and-deploy/directory-structure)。</span><span class="sxs-lookup"><span data-stu-id="2a047-155">If a *web.config* file isn't present in the project, the file is created with the correct *processPath* and *arguments* to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and moved to [published output](xref:host-and-deploy/directory-structure).</span></span>

<span data-ttu-id="2a047-156">如果项目中存在 web.config 文件，则会使用正确的 processPath 和参数转换该文件，以便配置 ASP.NET Core 模块，并将该文件移动到已发布的输出。</span><span class="sxs-lookup"><span data-stu-id="2a047-156">If a *web.config* file is present in the project, the file is transformed with the correct *processPath* and *arguments* to configure the ASP.NET Core Module and moved to published output.</span></span> <span data-ttu-id="2a047-157">转换不会修改文件中的 IIS 配置设置。</span><span class="sxs-lookup"><span data-stu-id="2a047-157">The transformation doesn't modify IIS configuration settings in the file.</span></span>

<span data-ttu-id="2a047-158">web.config 文件可能会提供其他 IIS 配置设置，以控制活动的 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="2a047-158">The *web.config* file may provide additional IIS configuration settings that control active IIS modules.</span></span> <span data-ttu-id="2a047-159">有关能够处理 ASP.NET Core 应用请求的 IIS 模块的信息，请参阅 [IIS 模块](xref:host-and-deploy/iis/modules)主题。</span><span class="sxs-lookup"><span data-stu-id="2a047-159">For information on IIS modules that are capable of processing requests with ASP.NET Core apps, see the [IIS modules](xref:host-and-deploy/iis/modules) topic.</span></span>

<span data-ttu-id="2a047-160">要防止 Web SDK 转换 web.config 文件，请使用项目文件中的 \<IsTransformWebConfigDisabled> 属性：</span><span class="sxs-lookup"><span data-stu-id="2a047-160">To prevent the Web SDK from transforming the *web.config* file, use the **\<IsTransformWebConfigDisabled>** property in the project file:</span></span>

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="2a047-161">在禁用 Web SDK 转换文件时，开发人员应手动设置 processPath 和参数。</span><span class="sxs-lookup"><span data-stu-id="2a047-161">When disabling the Web SDK from transforming the file, the *processPath* and *arguments* should be manually set by the developer.</span></span> <span data-ttu-id="2a047-162">有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2a047-162">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

### <a name="webconfig-file-location"></a><span data-ttu-id="2a047-163">web.config 文件位置</span><span class="sxs-lookup"><span data-stu-id="2a047-163">web.config file location</span></span>

<span data-ttu-id="2a047-164">ASP.NET Core 应用在 IIS 与 Kestrel 服务器之间的反向代理中托管。</span><span class="sxs-lookup"><span data-stu-id="2a047-164">ASP.NET Core apps are hosted in a reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="2a047-165">为了创建反向代理，web.config 文件必须存在于已部署应用的内容根路径（通常为应用基路径）中。</span><span class="sxs-lookup"><span data-stu-id="2a047-165">In order to create the reverse proxy, the *web.config* file must be present at the content root path (typically the app base path) of the deployed app.</span></span> <span data-ttu-id="2a047-166">该位置与向 IIS 提供的网站物理路径相同。</span><span class="sxs-lookup"><span data-stu-id="2a047-166">This is the same location as the website physical path provided to IIS.</span></span> <span data-ttu-id="2a047-167">若要使用 Web 部署发布多个应用，应用的根路径中需要包含 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-167">The *web.config* file is required at the root of the app to enable the publishing of multiple apps using Web Deploy.</span></span>

<span data-ttu-id="2a047-168">敏感文件存在于应用的物理路径中，如 \<assembly>.runtimeconfig.json、\<assembly>.xml（XML 文档注释）和 \<assembly>.deps.json。</span><span class="sxs-lookup"><span data-stu-id="2a047-168">Sensitive files exist on the app's physical path, such as *\<assembly>.runtimeconfig.json*, *\<assembly>.xml* (XML Documentation comments), and *\<assembly>.deps.json*.</span></span> <span data-ttu-id="2a047-169">当存在 web.config 文件且站点正常启动的情况下，若要请求获取这些敏感文件，IIS 不会提供。</span><span class="sxs-lookup"><span data-stu-id="2a047-169">When the *web.config* file is present and and the site starts normally, IIS doesn't serve these sensitive files if they're requested.</span></span> <span data-ttu-id="2a047-170">如果缺少 web.config 文件、命名不正确，或无法配置站点以正常启动，IIS 可能会公开提供敏感文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-170">If the *web.config* file is missing, incorrectly named, or unable to configure the site for normal startup, IIS may serve sensitive files publicly.</span></span>

<span data-ttu-id="2a047-171">部署中必须始终存在 web.config 文件且正确命名，并可以配置站点以正常启动。**请勿从生产部署中删除 web.config 文件。**</span><span class="sxs-lookup"><span data-stu-id="2a047-171">**The *web.config* file must be present in the deployment at all times, correctly named, and able to configure the site for normal start up. Never remove the *web.config* file from a production deployment.**</span></span>

## <a name="iis-configuration"></a><span data-ttu-id="2a047-172">IIS 配置</span><span class="sxs-lookup"><span data-stu-id="2a047-172">IIS configuration</span></span>

<span data-ttu-id="2a047-173">**Windows Server 操作系统**</span><span class="sxs-lookup"><span data-stu-id="2a047-173">**Windows Server operating systems**</span></span>

<span data-ttu-id="2a047-174">启用 Web 服务器 (IIS) 服务器角色并建立角色服务。</span><span class="sxs-lookup"><span data-stu-id="2a047-174">Enable the **Web Server (IIS)** server role and establish role services.</span></span>

1. <span data-ttu-id="2a047-175">通过“管理”菜单或“服务器管理器”中的链接使用“添加角色和功能”向导。</span><span class="sxs-lookup"><span data-stu-id="2a047-175">Use the **Add Roles and Features** wizard from the **Manage** menu or the link in **Server Manager**.</span></span> <span data-ttu-id="2a047-176">在“服务器角色”步骤中，选中“Web 服务器(IIS)”框。</span><span class="sxs-lookup"><span data-stu-id="2a047-176">On the **Server Roles** step, check the box for **Web Server (IIS)**.</span></span>

   ![在选择服务器角色步骤中选择了“Web 服务器 IIS”角色。](index/_static/server-roles-ws2016.png)

1. <span data-ttu-id="2a047-178">在“功能”步骤后，为 Web 服务器 (IIS) 加载“角色服务”步骤。</span><span class="sxs-lookup"><span data-stu-id="2a047-178">After the **Features** step, the **Role services** step loads for Web Server (IIS).</span></span> <span data-ttu-id="2a047-179">选择所需 IIS 角色服务，或接受提供的默认角色服务。</span><span class="sxs-lookup"><span data-stu-id="2a047-179">Select the IIS role services desired or accept the default role services provided.</span></span>

   ![在选择角色服务步骤中选择了默认角色服务。](index/_static/role-services-ws2016.png)

   <span data-ttu-id="2a047-181">**Windows 身份验证（可选）**</span><span class="sxs-lookup"><span data-stu-id="2a047-181">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="2a047-182">若要启用 Windows 身份验证，请展开以下节点：“Web 服务器” > “安全”。</span><span class="sxs-lookup"><span data-stu-id="2a047-182">To enable Windows Authentication, expand the following nodes: **Web Server** > **Security**.</span></span> <span data-ttu-id="2a047-183">选择“Windows 身份验证”功能。</span><span class="sxs-lookup"><span data-stu-id="2a047-183">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="2a047-184">有关详细信息，请参阅 [Windows 身份验证 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 和[配置 Windows 身份验证](xref:security/authentication/windowsauth)。</span><span class="sxs-lookup"><span data-stu-id="2a047-184">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="2a047-185">**Websocket（可选）**</span><span class="sxs-lookup"><span data-stu-id="2a047-185">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="2a047-186">Websocket 支持 ASP.NET Core 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2a047-186">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="2a047-187">若要启用 Websocket，请展开以下节点：“Web 服务器” > “应用程序开发”。</span><span class="sxs-lookup"><span data-stu-id="2a047-187">To enable WebSockets, expand the following nodes: **Web Server** > **Application Development**.</span></span> <span data-ttu-id="2a047-188">选择“WebSocket 协议”功能。</span><span class="sxs-lookup"><span data-stu-id="2a047-188">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="2a047-189">有关详细信息，请参阅 [WebSockets](xref:fundamentals/websockets)。</span><span class="sxs-lookup"><span data-stu-id="2a047-189">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="2a047-190">继续执行“确认”步骤，安装 Web 服务器角色和服务。</span><span class="sxs-lookup"><span data-stu-id="2a047-190">Proceed through the **Confirmation** step to install the web server role and services.</span></span> <span data-ttu-id="2a047-191">安装 Web 服务器 (IIS) 角色后无需重启服务器/IIS。</span><span class="sxs-lookup"><span data-stu-id="2a047-191">A server/IIS restart isn't required after installing the **Web Server (IIS)** role.</span></span>

<span data-ttu-id="2a047-192">**Windows 桌面操作系统**</span><span class="sxs-lookup"><span data-stu-id="2a047-192">**Windows desktop operating systems**</span></span>

<span data-ttu-id="2a047-193">启用“IIS 管理控制台”和“万维网服务”。</span><span class="sxs-lookup"><span data-stu-id="2a047-193">Enable the **IIS Management Console** and **World Wide Web Services**.</span></span>

1. <span data-ttu-id="2a047-194">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="2a047-194">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>

1. <span data-ttu-id="2a047-195">打开“Internet Information Services”节点。</span><span class="sxs-lookup"><span data-stu-id="2a047-195">Open the **Internet Information Services** node.</span></span> <span data-ttu-id="2a047-196">打开“Web 管理工具”节点。</span><span class="sxs-lookup"><span data-stu-id="2a047-196">Open the **Web Management Tools** node.</span></span>

1. <span data-ttu-id="2a047-197">选中“IIS 管理控制台”框。</span><span class="sxs-lookup"><span data-stu-id="2a047-197">Check the box for **IIS Management Console**.</span></span>

1. <span data-ttu-id="2a047-198">选中“万维网服务”框。</span><span class="sxs-lookup"><span data-stu-id="2a047-198">Check the box for **World Wide Web Services**.</span></span>

1. <span data-ttu-id="2a047-199">接受“万维网服务”的默认功能，或自定义 IIS 功能。</span><span class="sxs-lookup"><span data-stu-id="2a047-199">Accept the default features for **World Wide Web Services** or customize the IIS features.</span></span>

   <span data-ttu-id="2a047-200">**Windows 身份验证（可选）**</span><span class="sxs-lookup"><span data-stu-id="2a047-200">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="2a047-201">若要启用 Windows 身份验证，请展开以下节点：“万维网服务” > “安全”。</span><span class="sxs-lookup"><span data-stu-id="2a047-201">To enable Windows Authentication, expand the following nodes: **World Wide Web Services** > **Security**.</span></span> <span data-ttu-id="2a047-202">选择“Windows 身份验证”功能。</span><span class="sxs-lookup"><span data-stu-id="2a047-202">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="2a047-203">有关详细信息，请参阅 [Windows 身份验证 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 和[配置 Windows 身份验证](xref:security/authentication/windowsauth)。</span><span class="sxs-lookup"><span data-stu-id="2a047-203">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="2a047-204">**Websocket（可选）**</span><span class="sxs-lookup"><span data-stu-id="2a047-204">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="2a047-205">Websocket 支持 ASP.NET Core 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2a047-205">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="2a047-206">若要启用 Websocket，请展开以下节点：“万维网服务” > “应用程序开发功能”。</span><span class="sxs-lookup"><span data-stu-id="2a047-206">To enable WebSockets, expand the following nodes: **World Wide Web Services** > **Application Development Features**.</span></span> <span data-ttu-id="2a047-207">选择“WebSocket 协议”功能。</span><span class="sxs-lookup"><span data-stu-id="2a047-207">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="2a047-208">有关详细信息，请参阅 [WebSockets](xref:fundamentals/websockets)。</span><span class="sxs-lookup"><span data-stu-id="2a047-208">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="2a047-209">如果 IIS 安装需要重新启动，则重新启动系统。</span><span class="sxs-lookup"><span data-stu-id="2a047-209">If the IIS installation requires a restart, restart the system.</span></span>

![在“Windows 功能”中选择了“IIS 管理控制台”和“万维网服务”。](index/_static/windows-features-win10.png)

---

## <a name="install-the-net-core-hosting-bundle"></a><span data-ttu-id="2a047-211">安装 .NET Core 托管捆绑包</span><span class="sxs-lookup"><span data-stu-id="2a047-211">Install the .NET Core Hosting Bundle</span></span>

1. <span data-ttu-id="2a047-212">在托管系统上安装 .NET Core 托管捆绑包。</span><span class="sxs-lookup"><span data-stu-id="2a047-212">Install the *.NET Core Hosting Bundle* on the hosting system.</span></span> <span data-ttu-id="2a047-213">捆绑包可安装 .NET Core 运行时、.NET Core 库和 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2a047-213">The bundle installs the .NET Core Runtime, .NET Core Library, and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="2a047-214">该模块创建 IIS 与 Kestrel 服务器之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="2a047-214">The module creates the reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="2a047-215">如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，然后再安装 .NET Core 托管捆绑包。</span><span class="sxs-lookup"><span data-stu-id="2a047-215">If the system doesn't have an Internet connection, obtain and install the [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840) before installing the .NET Core Hosting Bundle.</span></span>

   1. <span data-ttu-id="2a047-216">导航到 [.NET“所有下载”页](https://www.microsoft.com/net/download/all)。</span><span class="sxs-lookup"><span data-stu-id="2a047-216">Navigate to the [.NET All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="2a047-217">从列表中选择最新的非预览 .NET Core 运行时（.NET Core > 运行时 > .NET Core 运行时 x.y.z）。</span><span class="sxs-lookup"><span data-stu-id="2a047-217">Select the latest non-preview .NET Core runtime from the list (**.NET Core** > **Runtime** > **.NET Core Runtime x.y.z**).</span></span> <span data-ttu-id="2a047-218">除非你想要使用预览软件，否则请避免选择其链接文本中包含“预览”一词的运行时。</span><span class="sxs-lookup"><span data-stu-id="2a047-218">Unless you intend to work with preview software, avoid runtimes that have the word "preview" in their link text.</span></span>
   1. <span data-ttu-id="2a047-219">在 Windows 下的 .NET Core 运行时下载页上，选择“托管捆绑包安装程序”链接以下载 .NET Core 托管捆绑包。</span><span class="sxs-lookup"><span data-stu-id="2a047-219">On the .NET Core runtime download page under **Windows**, select the **Hosting Bundle Installer** link to download the *.NET Core Hosting Bundle*.</span></span>

   <span data-ttu-id="2a047-220">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="2a047-220">**Important!**</span></span> <span data-ttu-id="2a047-221">如果在 IIS 之前安装了托管捆绑包，则必须修复捆绑包安装。</span><span class="sxs-lookup"><span data-stu-id="2a047-221">If the Hosting Bundle is installed before IIS, the bundle installation must be repaired.</span></span> <span data-ttu-id="2a047-222">在安装 IIS 后再次运行托管捆绑包安装程序。</span><span class="sxs-lookup"><span data-stu-id="2a047-222">Run the Hosting Bundle installer again after installing IIS.</span></span>
   
   <span data-ttu-id="2a047-223">若要防止安装程序在 x64 操作系统上安装 x86 程序包，请通过管理员命令提示符使用开关 `OPT_NO_X86=1` 来运行安装程序。</span><span class="sxs-lookup"><span data-stu-id="2a047-223">To prevent the installer from installing x86 packages on an x64 OS, run the installer from an administrator command prompt with the switch `OPT_NO_X86=1`.</span></span>

1. <span data-ttu-id="2a047-224">重启系统，或从命令提示符处依次执行 net stop was /y 和 net start w3svc。</span><span class="sxs-lookup"><span data-stu-id="2a047-224">Restart the system or execute **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span> <span data-ttu-id="2a047-225">重新启动 IIS 将选取安装程序对系统 PATH 所作的更改。</span><span class="sxs-lookup"><span data-stu-id="2a047-225">Restarting IIS picks up a change to the system PATH made by the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="2a047-226">有关 IIS 共享配置的信息，请参阅[使用 IIS 共享配置的 ASP.NET Core 模块](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)。</span><span class="sxs-lookup"><span data-stu-id="2a047-226">For information on IIS Shared Configuration, see [ASP.NET Core Module with IIS Shared Configuration](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).</span></span>

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a><span data-ttu-id="2a047-227">使用 Visual Studio 进行发布时安装 Web 部署</span><span class="sxs-lookup"><span data-stu-id="2a047-227">Install Web Deploy when publishing with Visual Studio</span></span>

<span data-ttu-id="2a047-228">使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)将应用部署到服务器时，请在服务器上安装最新版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="2a047-228">When deploying apps to servers with [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy), install the latest version of Web Deploy on the server.</span></span> <span data-ttu-id="2a047-229">要安装 Web 部署，请使用 [Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) 或直接从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=43717)获取安装程序。</span><span class="sxs-lookup"><span data-stu-id="2a047-229">To install Web Deploy, use the [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) or obtain an installer directly from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43717).</span></span> <span data-ttu-id="2a047-230">建议使用 WebPI。</span><span class="sxs-lookup"><span data-stu-id="2a047-230">The preferred method is to use WebPI.</span></span> <span data-ttu-id="2a047-231">WebPI 为托管提供程序提供独立的安装程序和配置。</span><span class="sxs-lookup"><span data-stu-id="2a047-231">WebPI offers a standalone setup and a configuration for hosting providers.</span></span>

## <a name="create-the-iis-site"></a><span data-ttu-id="2a047-232">创建 IIS 站点</span><span class="sxs-lookup"><span data-stu-id="2a047-232">Create the IIS site</span></span>

1. <span data-ttu-id="2a047-233">在托管系统上，创建一个文件夹以包含应用已发布的文件夹和文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-233">On the hosting system, create a folder to contain the app's published folders and files.</span></span> <span data-ttu-id="2a047-234">[目录结构](xref:host-and-deploy/directory-structure)主题中介绍了应用的部署布局。</span><span class="sxs-lookup"><span data-stu-id="2a047-234">An app's deployment layout is described in the [Directory Structure](xref:host-and-deploy/directory-structure) topic.</span></span>

1. <span data-ttu-id="2a047-235">在新文件夹中创建一个“日志”文件夹，用于在启用 stdout 日志记录时保存 ASP.NET Core 模块 stdout 日志。</span><span class="sxs-lookup"><span data-stu-id="2a047-235">Within the new folder, create a *logs* folder to hold ASP.NET Core Module stdout logs when stdout logging is enabled.</span></span> <span data-ttu-id="2a047-236">如果部署应用时有效负载中包含了“日志”文件夹，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="2a047-236">If the app is deployed with a *logs* folder in the payload, skip this step.</span></span> <span data-ttu-id="2a047-237">有关如何启用 MSBuild 以在本地生成项目时自动创建“日志”文件夹的说明，请参阅[目录结构](xref:host-and-deploy/directory-structure)主题。</span><span class="sxs-lookup"><span data-stu-id="2a047-237">For instructions on how to enable MSBuild to create the *logs* folder automatically when the project is built locally, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2a047-238">仅使用 stdout 日志来解决应用启动失败的问题。</span><span class="sxs-lookup"><span data-stu-id="2a047-238">Only use the stdout log to troubleshoot app startup failures.</span></span> <span data-ttu-id="2a047-239">请勿使用 stdout 日志记录进行常规应用日志记录。</span><span class="sxs-lookup"><span data-stu-id="2a047-239">Never use stdout logging for routine app logging.</span></span> <span data-ttu-id="2a047-240">日志文件大小或创建的日志文件数没有限制。</span><span class="sxs-lookup"><span data-stu-id="2a047-240">There's no limit on log file size or the number of log files created.</span></span> <span data-ttu-id="2a047-241">应用池必须对写入日志的位置具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="2a047-241">The app pool must have write access to the location where the logs are written.</span></span> <span data-ttu-id="2a047-242">日志位置路径上的所有文件夹都必须存在。</span><span class="sxs-lookup"><span data-stu-id="2a047-242">All of the folders on the path to the log location must exist.</span></span> <span data-ttu-id="2a047-243">有关 stdout 日志的详细信息，请参阅[日志创建和重定向](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)。</span><span class="sxs-lookup"><span data-stu-id="2a047-243">For more information on the stdout log, see [Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection).</span></span> <span data-ttu-id="2a047-244">有关 ASP.NET Core 应用中的日志记录信息，请参阅[日志记录](xref:fundamentals/logging/index)主题。</span><span class="sxs-lookup"><span data-stu-id="2a047-244">For information on logging in an ASP.NET Core app, see the [Logging](xref:fundamentals/logging/index) topic.</span></span>

1. <span data-ttu-id="2a047-245">在“IIS 管理器”中，打开“连接”面板中的服务器节点。</span><span class="sxs-lookup"><span data-stu-id="2a047-245">In **IIS Manager**, open the server's node in the **Connections** panel.</span></span> <span data-ttu-id="2a047-246">右键单击“站点”文件夹。</span><span class="sxs-lookup"><span data-stu-id="2a047-246">Right-click the **Sites** folder.</span></span> <span data-ttu-id="2a047-247">选择上下文菜单中的“添加网站”。</span><span class="sxs-lookup"><span data-stu-id="2a047-247">Select **Add Website** from the contextual menu.</span></span>

1. <span data-ttu-id="2a047-248">提供网站名称，并将物理路径设置为应用的部署文件夹。</span><span class="sxs-lookup"><span data-stu-id="2a047-248">Provide a **Site name** and set the **Physical path** to the app's deployment folder.</span></span> <span data-ttu-id="2a047-249">提供“绑定”配置，并通过选择“确定”创建网站：</span><span class="sxs-lookup"><span data-stu-id="2a047-249">Provide the **Binding** configuration and create the website by selecting **OK**:</span></span>

   ![在“添加网站”步骤中提供网站名称、物理路径和主机名。](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > <span data-ttu-id="2a047-251">不应使用顶级通配符绑定（`http://*:80/` 和 `http://+:80`）。</span><span class="sxs-lookup"><span data-stu-id="2a047-251">Top-level wildcard bindings (`http://*:80/` and `http://+:80`) should **not** be used.</span></span> <span data-ttu-id="2a047-252">顶级通配符绑定可能会为应用带来安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="2a047-252">Top-level wildcard bindings can open up your app to security vulnerabilities.</span></span> <span data-ttu-id="2a047-253">此行为同时适用于强通配符和弱通配符。</span><span class="sxs-lookup"><span data-stu-id="2a047-253">This applies to both strong and weak wildcards.</span></span> <span data-ttu-id="2a047-254">使用显式主机名而不是通配符。</span><span class="sxs-lookup"><span data-stu-id="2a047-254">Use explicit host names rather than wildcards.</span></span> <span data-ttu-id="2a047-255">如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.mysub.com`）不具有此安全风险。</span><span class="sxs-lookup"><span data-stu-id="2a047-255">Subdomain wildcard binding (for example, `*.mysub.com`) doesn't have this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="2a047-256">有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。</span><span class="sxs-lookup"><span data-stu-id="2a047-256">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

1. <span data-ttu-id="2a047-257">在服务器节点下，选择“应用程序池”。</span><span class="sxs-lookup"><span data-stu-id="2a047-257">Under the server's node, select **Application Pools**.</span></span>

1. <span data-ttu-id="2a047-258">右键单击站点的应用池，然后从上下文菜单中选择“基本设置”。</span><span class="sxs-lookup"><span data-stu-id="2a047-258">Right-click the site's app pool and select **Basic Settings** from the contextual menu.</span></span>

1. <span data-ttu-id="2a047-259">在“编辑应用程序池”窗口中，将“.NET CLR 版本”设置为“无托管代码”：</span><span class="sxs-lookup"><span data-stu-id="2a047-259">In the **Edit Application Pool** window, set the **.NET CLR version** to **No Managed Code**:</span></span>

   ![将“.NET CLR 版本”设置为“无托管代码”。](index/_static/edit-apppool-ws2016.png)

    <span data-ttu-id="2a047-261">ASP.NET Core 在单独的进程中运行，并管理运行时。</span><span class="sxs-lookup"><span data-stu-id="2a047-261">ASP.NET Core runs in a separate process and manages the runtime.</span></span> <span data-ttu-id="2a047-262">ASP.NET Core 不依赖加载桌面 CLR。</span><span class="sxs-lookup"><span data-stu-id="2a047-262">ASP.NET Core doesn't rely on loading the desktop CLR.</span></span> <span data-ttu-id="2a047-263">将“.NET CLR 版本”设置为“无托管代码”为可选步骤。</span><span class="sxs-lookup"><span data-stu-id="2a047-263">Setting the **.NET CLR version** to **No Managed Code** is optional.</span></span>

1. <span data-ttu-id="2a047-264">确认进程模型标识拥有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="2a047-264">Confirm the process model identity has the proper permissions.</span></span>

   <span data-ttu-id="2a047-265">如果将应用池的默认标识（“进程模型” > “标识”）从 ApplicationPoolIdentity 更改为另一标识，请验证新标识拥有所需的权限，可访问应用的文件夹、数据库和其他所需资源。</span><span class="sxs-lookup"><span data-stu-id="2a047-265">If the default identity of the app pool (**Process Model** > **Identity**) is changed from **ApplicationPoolIdentity** to another identity, verify that the new identity has the required permissions to access the app's folder, database, and other required resources.</span></span> <span data-ttu-id="2a047-266">例如，应用池需要对文件夹的读取和写入权限，以便应用在其中读取和写入文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-266">For example, the app pool requires read and write access to folders where the app reads and writes files.</span></span>

<span data-ttu-id="2a047-267">**Windows 身份验证配置（可选）**</span><span class="sxs-lookup"><span data-stu-id="2a047-267">**Windows Authentication configuration (Optional)**</span></span>  
<span data-ttu-id="2a047-268">有关详细信息，请参阅[配置 Windows 身份验证](xref:security/authentication/windowsauth)。</span><span class="sxs-lookup"><span data-stu-id="2a047-268">For more information, see [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="2a047-269">部署应用</span><span class="sxs-lookup"><span data-stu-id="2a047-269">Deploy the app</span></span>

<span data-ttu-id="2a047-270">将应用部署到在托管系统上创建的文件夹。</span><span class="sxs-lookup"><span data-stu-id="2a047-270">Deploy the app to the folder created on the hosting system.</span></span> <span data-ttu-id="2a047-271">建议使用的部署机制是 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。</span><span class="sxs-lookup"><span data-stu-id="2a047-271">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) is the recommended mechanism for deployment.</span></span>

### <a name="web-deploy-with-visual-studio"></a><span data-ttu-id="2a047-272">在 Visual Studio 内使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="2a047-272">Web Deploy with Visual Studio</span></span>

<span data-ttu-id="2a047-273">要了解如何创建用于 Web 部署的发布配置文件，请参阅[用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles)。</span><span class="sxs-lookup"><span data-stu-id="2a047-273">See the [Visual Studio publish profiles for ASP.NET Core app deployment](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) topic to learn how to create a publish profile for use with Web Deploy.</span></span> <span data-ttu-id="2a047-274">如果托管提供程序提供了发布配置文件或支持创建发布配置文件，请下载配置文件并使用 Visual Studio 的“发布”对话框将其导入。</span><span class="sxs-lookup"><span data-stu-id="2a047-274">If the hosting provider provides a Publish Profile or support for creating one, download their profile and import it using the Visual Studio **Publish** dialog.</span></span>

![“发布”对话框页](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a><span data-ttu-id="2a047-276">在 Visual Studio 之外使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="2a047-276">Web Deploy outside of Visual Studio</span></span>

<span data-ttu-id="2a047-277">也可以在 Visual Studio 之外从命令行使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。</span><span class="sxs-lookup"><span data-stu-id="2a047-277">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) can also be used outside of Visual Studio from the command line.</span></span> <span data-ttu-id="2a047-278">有关详细信息，请参阅 [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool)（Web 部署工具）。</span><span class="sxs-lookup"><span data-stu-id="2a047-278">For more information, see [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool).</span></span>

### <a name="alternatives-to-web-deploy"></a><span data-ttu-id="2a047-279">Web 部署的替代方法</span><span class="sxs-lookup"><span data-stu-id="2a047-279">Alternatives to Web Deploy</span></span>

<span data-ttu-id="2a047-280">有多种方法可将应用移动到托管系统，例如手动复制、Xcopy、Robocopy 或 PowerShell，可使用其中任何一种方法。</span><span class="sxs-lookup"><span data-stu-id="2a047-280">Use any of several methods to move the app to the hosting system, such as manual copy, Xcopy, Robocopy, or PowerShell.</span></span>

<span data-ttu-id="2a047-281">有关将 ASP.NET Core 部署到 IIS 的详细信息，请参阅[面向 IIS 管理员的部署资源](#deployment-resources-for-iis-administrators)部分。</span><span class="sxs-lookup"><span data-stu-id="2a047-281">For more information on ASP.NET Core deployment to IIS, see the [Deployment resources for IIS administrators](#deployment-resources-for-iis-administrators) section.</span></span>

## <a name="browse-the-website"></a><span data-ttu-id="2a047-282">浏览网站</span><span class="sxs-lookup"><span data-stu-id="2a047-282">Browse the website</span></span>

![Microsoft Edge 浏览器已加载 IIS 启动页。](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a><span data-ttu-id="2a047-284">锁定的部署文件</span><span class="sxs-lookup"><span data-stu-id="2a047-284">Locked deployment files</span></span>

<span data-ttu-id="2a047-285">如果应用正在运行，部署文件夹中的文件会被锁定。</span><span class="sxs-lookup"><span data-stu-id="2a047-285">Files in the deployment folder are locked when the app is running.</span></span> <span data-ttu-id="2a047-286">在部署期间，无法覆盖已锁定的文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-286">Locked files can't be overwritten during deployment.</span></span> <span data-ttu-id="2a047-287">若要在部署中解除已锁定的文件，请使用以下方法之一停止应用池：</span><span class="sxs-lookup"><span data-stu-id="2a047-287">To release locked files in a deployment, stop the app pool using **one** of the following approaches:</span></span>

* <span data-ttu-id="2a047-288">使用 Web 部署并在项目文件中引用 `Microsoft.NET.Sdk.Web`。</span><span class="sxs-lookup"><span data-stu-id="2a047-288">Use Web Deploy and reference `Microsoft.NET.Sdk.Web` in the project file.</span></span> <span data-ttu-id="2a047-289">系统会在 Web 应用目录的根目录中放置一个 app_offline.htm 文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-289">An *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="2a047-290">该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-290">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="2a047-291">有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)。</span><span class="sxs-lookup"><span data-stu-id="2a047-291">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#app_offlinehtm).</span></span>
* <span data-ttu-id="2a047-292">在服务器上的 IIS 管理器中手动停止应用池。</span><span class="sxs-lookup"><span data-stu-id="2a047-292">Manually stop the app pool in the IIS Manager on the server.</span></span>
* <span data-ttu-id="2a047-293">使用 PowerShell 来停止和重新启动应用池（需要使用 PowerShell 5 或更高版本）：</span><span class="sxs-lookup"><span data-stu-id="2a047-293">Use PowerShell to stop and restart the app pool (requires PowerShell 5 or later):</span></span>

  ```PowerShell
  $webAppPoolName = 'APP_POOL_NAME'

  # Stop the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
      Stop-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Stopped
  }

  # Provide script commands here to deploy the app

  # Restart the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
      Start-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Started
  }
  ```

## <a name="data-protection"></a><span data-ttu-id="2a047-294">数据保护</span><span class="sxs-lookup"><span data-stu-id="2a047-294">Data protection</span></span>

<span data-ttu-id="2a047-295">[ASP.NET Core 数据保护堆栈](xref:security/data-protection/index)由多个 ASP.NET Core [中间件](xref:fundamentals/middleware/index)使用，包括用于身份验证的中间件。</span><span class="sxs-lookup"><span data-stu-id="2a047-295">The [ASP.NET Core Data Protection stack](xref:security/data-protection/index) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including middleware used in authentication.</span></span> <span data-ttu-id="2a047-296">即使用户代码不调用数据保护 API，也应该使用部署脚本或在用户代码中配置数据保护，以创建持久的加密[密钥存储](xref:security/data-protection/implementation/key-management)。</span><span class="sxs-lookup"><span data-stu-id="2a047-296">Even if Data Protection APIs aren't called by user code, data protection should be configured with a deployment script or in user code to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="2a047-297">如果不配置数据保护，则密钥存储在内存中。重启应用时，密钥会被丢弃。</span><span class="sxs-lookup"><span data-stu-id="2a047-297">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="2a047-298">如果密钥环存储于内存中，则在应用重启时：</span><span class="sxs-lookup"><span data-stu-id="2a047-298">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="2a047-299">所有基于 cookie 的身份验证令牌都无效。</span><span class="sxs-lookup"><span data-stu-id="2a047-299">All cookie-based authentication tokens are invalidated.</span></span> 
* <span data-ttu-id="2a047-300">用户需要在下一次请求时再次登录。</span><span class="sxs-lookup"><span data-stu-id="2a047-300">Users are required to sign in again on their next request.</span></span> 
* <span data-ttu-id="2a047-301">无法再解密使用密钥环保护的任何数据。</span><span class="sxs-lookup"><span data-stu-id="2a047-301">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="2a047-302">这可能包括 [CSRF 令牌](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration)和 [ASP.NET Core MVC TempData cookie](xref:fundamentals/app-state#tempdata)。</span><span class="sxs-lookup"><span data-stu-id="2a047-302">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="2a047-303">若要在 IIS 下配置数据保护以持久化密钥环，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="2a047-303">To configure data protection under IIS to persist the key ring, use **one** of the following approaches:</span></span>

* <span data-ttu-id="2a047-304">**创建数据保护注册表项**</span><span class="sxs-lookup"><span data-stu-id="2a047-304">**Create Data Protection Registry Keys**</span></span>

  <span data-ttu-id="2a047-305">ASP.NET Core 应用使用的数据保护密钥存储在应用外部的注册表中。</span><span class="sxs-lookup"><span data-stu-id="2a047-305">Data protection keys used by ASP.NET Core apps are stored in the registry external to the apps.</span></span> <span data-ttu-id="2a047-306">要持久保存给定应用的密钥，需为应用池创建注册表项。</span><span class="sxs-lookup"><span data-stu-id="2a047-306">To persist the keys for a given app, create registry keys for the app pool.</span></span>

  <span data-ttu-id="2a047-307">对于独立的非 Web 场 IIS 安装，可以对用于 ASP.NET Core 应用的每个应用池使用[数据保护 Provision-AutoGenKeys.ps1 PowerShell 脚本](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)。</span><span class="sxs-lookup"><span data-stu-id="2a047-307">For standalone, non-webfarm IIS installations, the [Data Protection Provision-AutoGenKeys.ps1 PowerShell script](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1) can be used for each app pool used with an ASP.NET Core app.</span></span> <span data-ttu-id="2a047-308">此脚本在 HKLM 注册表中创建注册表项，仅应用程序的应用池工作进程帐户可对其进行访问。</span><span class="sxs-lookup"><span data-stu-id="2a047-308">This script creates a registry key in the HKLM registry that's accessible only to the worker process account of the app's app pool.</span></span> <span data-ttu-id="2a047-309">通过计算机范围的密钥使用 DPAPI 对密钥静态加密。</span><span class="sxs-lookup"><span data-stu-id="2a047-309">Keys are encrypted at rest using DPAPI with a machine-wide key.</span></span>

  <span data-ttu-id="2a047-310">在 web 场方案中，可以将应用配置为使用 UNC 路径存储其数据保护密钥环。</span><span class="sxs-lookup"><span data-stu-id="2a047-310">In web farm scenarios, an app can be configured to use a UNC path to store its data protection key ring.</span></span> <span data-ttu-id="2a047-311">默认情况下，数据保护密钥未加密。</span><span class="sxs-lookup"><span data-stu-id="2a047-311">By default, the data protection keys aren't encrypted.</span></span> <span data-ttu-id="2a047-312">确保网络共享的文件权限仅限于应用在其下运行的 Windows 帐户。</span><span class="sxs-lookup"><span data-stu-id="2a047-312">Ensure that the file permissions for the network share are limited to the Windows account the app runs under.</span></span> <span data-ttu-id="2a047-313">可使用 X509 证书来保护静态密钥。</span><span class="sxs-lookup"><span data-stu-id="2a047-313">An X509 certificate can be used to protect keys at rest.</span></span> <span data-ttu-id="2a047-314">建议使用允许用户上传证书的机制：将证书放置在用户信任的证书存储中，并确保在运行用户应用的所有计算机上都可使用这些证书。</span><span class="sxs-lookup"><span data-stu-id="2a047-314">Consider a mechanism to allow users to upload certificates: Place certificates into the user's trusted certificate store and ensure they're available on all machines where the user's app runs.</span></span> <span data-ttu-id="2a047-315">有关详细信息，请参阅[配置 ASP.NET Core 数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="2a047-315">See [Configure ASP.NET Core Data Protection](xref:security/data-protection/configuration/overview) for details.</span></span>

* <span data-ttu-id="2a047-316">**配置 IIS 应用程序池以加载用户配置文件**</span><span class="sxs-lookup"><span data-stu-id="2a047-316">**Configure the IIS Application Pool to load the user profile**</span></span>

  <span data-ttu-id="2a047-317">此设置位于应用池“高级设置”下的“进程模型”部分。</span><span class="sxs-lookup"><span data-stu-id="2a047-317">This setting is in the **Process Model** section under the **Advanced Settings** for the app pool.</span></span> <span data-ttu-id="2a047-318">将“加载用户配置文件”设置为 `True`。</span><span class="sxs-lookup"><span data-stu-id="2a047-318">Set Load User Profile to `True`.</span></span> <span data-ttu-id="2a047-319">这会将密钥存储在用户配置文件目录下，并使用 DPAPI 和特定于用户帐户（用于应用池）的密钥进行保护。</span><span class="sxs-lookup"><span data-stu-id="2a047-319">This stores keys under the user profile directory and protects them using DPAPI with a key specific to the user account used by the app pool.</span></span>

* <span data-ttu-id="2a047-320">**将文件系统用作密钥环存储**</span><span class="sxs-lookup"><span data-stu-id="2a047-320">**Use the file system as a key ring store**</span></span>

  <span data-ttu-id="2a047-321">调整应用代码，[将文件系统用作密钥环存储](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="2a047-321">Adjust the app code to [use the file system as a key ring store](xref:security/data-protection/configuration/overview).</span></span> <span data-ttu-id="2a047-322">使用 X509 证书保护密钥环，并确保该证书是受信任的证书。</span><span class="sxs-lookup"><span data-stu-id="2a047-322">Use an X509 certificate to protect the key ring and ensure the certificate is a trusted certificate.</span></span> <span data-ttu-id="2a047-323">如果它是自签名证书，则将该证书放置于受信任的根存储中。</span><span class="sxs-lookup"><span data-stu-id="2a047-323">If the certificate is self-signed, place the certificate in the Trusted Root store.</span></span>

  <span data-ttu-id="2a047-324">当在 Web 场中使用 IIS 时：</span><span class="sxs-lookup"><span data-stu-id="2a047-324">When using IIS in a web farm:</span></span>

  * <span data-ttu-id="2a047-325">使用所有计算机都可以访问的文件共享。</span><span class="sxs-lookup"><span data-stu-id="2a047-325">Use a file share that all machines can access.</span></span>
  * <span data-ttu-id="2a047-326">将 X509 证书部署到每台计算机。</span><span class="sxs-lookup"><span data-stu-id="2a047-326">Deploy an X509 certificate to each machine.</span></span> <span data-ttu-id="2a047-327">[通过代码配置数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="2a047-327">Configure [data protection in code](xref:security/data-protection/configuration/overview).</span></span>

* <span data-ttu-id="2a047-328">**设置用于数据保护的计算机范围的策略**</span><span class="sxs-lookup"><span data-stu-id="2a047-328">**Set a machine-wide policy for data protection**</span></span>

  <span data-ttu-id="2a047-329">数据保护系统对以下操作提供有限支持：为使用数据保护 API 的所有应用设置默认[计算机范围的策略](xref:security/data-protection/configuration/machine-wide-policy)。</span><span class="sxs-lookup"><span data-stu-id="2a047-329">The data protection system has limited support for setting a default [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy) for all apps that consume the Data Protection APIs.</span></span> <span data-ttu-id="2a047-330">有关详细信息，请参阅[数据保护文档](xref:security/data-protection/index)。</span><span class="sxs-lookup"><span data-stu-id="2a047-330">See the [data protection documentation](xref:security/data-protection/index) for details.</span></span>

## <a name="sub-application-configuration"></a><span data-ttu-id="2a047-331">子应用程序配置</span><span class="sxs-lookup"><span data-stu-id="2a047-331">Sub-application configuration</span></span>

<span data-ttu-id="2a047-332">在根应用下添加的子应用不应将 ASP.NET Core 模块作为处理程序包含在其中。</span><span class="sxs-lookup"><span data-stu-id="2a047-332">Sub-apps added under the root app shouldn't include the ASP.NET Core Module as a handler.</span></span> <span data-ttu-id="2a047-333">如果在子应用的 web.config 文件中将该模块添加为处理程序，则在尝试浏览子应用时会收到“500.19 内部服务器错误”，即引用错误的配置文件。</span><span class="sxs-lookup"><span data-stu-id="2a047-333">If the module is added as a handler in a sub-app's *web.config* file, a *500.19 Internal Server Error* referencing the faulty config file is received when attempting to browse the sub-app.</span></span>

<span data-ttu-id="2a047-334">以下示例显示 ASP.NET Core 子应用的已发布 web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="2a047-334">The following example shows a published *web.config* file for an ASP.NET Core sub-app:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="2a047-335">在 ASP.NET Core 应用下托管非 ASP.NET Core 子应用时，需在子应用的 web.config 文件中显式删除继承的处理程序：</span><span class="sxs-lookup"><span data-stu-id="2a047-335">When hosting a non-ASP.NET Core sub-app underneath an ASP.NET Core app, explicitly remove the inherited handler in the sub-app *web.config* file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="2a047-336">有关配置 ASP.NET Core 模块的详细信息，请参阅 [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)和 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2a047-336">For more information on configuring the ASP.NET Core Module, see the [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic and the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="configuration-of-iis-with-webconfig"></a><span data-ttu-id="2a047-337">使用 web.config 配置 IIS</span><span class="sxs-lookup"><span data-stu-id="2a047-337">Configuration of IIS with web.config</span></span>

<span data-ttu-id="2a047-338">对于那些应用于反向代理配置的 IIS 功能，IIS 配置受 web.config 的 \<system.webServer> 部分影响。</span><span class="sxs-lookup"><span data-stu-id="2a047-338">IIS configuration is influenced by the **\<system.webServer>** section of *web.config* for those IIS features that apply to a reverse proxy configuration.</span></span> <span data-ttu-id="2a047-339">如果在服务器级别将 IIS 配置为使用动态压缩，则可通过应用的 web.config 文件中的 \<urlCompression> 元素禁用它。</span><span class="sxs-lookup"><span data-stu-id="2a047-339">If IIS is configured at the server level to use dynamic compression, the **\<urlCompression>** element in the app's *web.config* file can disable it.</span></span>

<span data-ttu-id="2a047-340">有关详细信息，请参阅 [\<system.webServer> 的配置参考](/iis/configuration/system.webServer/)、[ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)和[使用 ASP.NET Core 的 IIS 模块](xref:host-and-deploy/iis/modules)。</span><span class="sxs-lookup"><span data-stu-id="2a047-340">For more information, see the [configuration reference for \<system.webServer>](/iis/configuration/system.webServer/), [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module), and [IIS Modules with ASP.NET Core](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="2a047-341">若要为在独立应用池中运行的各应用设置环境变量（IIS 10.0 或更高版本中支持此操作），请参阅 IIS 参考文档的[环境变量 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。</span><span class="sxs-lookup"><span data-stu-id="2a047-341">To set environment variables for individual apps running in isolated app pools (supported for IIS 10.0 or later), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic in the IIS reference documentation.</span></span>

## <a name="configuration-sections-of-webconfig"></a><span data-ttu-id="2a047-342">web.config 的配置节</span><span class="sxs-lookup"><span data-stu-id="2a047-342">Configuration sections of web.config</span></span>

<span data-ttu-id="2a047-343">ASP.NET Core 应用不会使用 web.config 中的 ASP.NET 4.x 应用的配置部分进行配置：</span><span class="sxs-lookup"><span data-stu-id="2a047-343">Configuration sections of ASP.NET 4.x apps in *web.config* aren't used by ASP.NET Core apps for configuration:</span></span>

* <span data-ttu-id="2a047-344">**\<system.web>**</span><span class="sxs-lookup"><span data-stu-id="2a047-344">**\<system.web>**</span></span>
* <span data-ttu-id="2a047-345">\<appSettings></span><span class="sxs-lookup"><span data-stu-id="2a047-345">**\<appSettings>**</span></span>
* <span data-ttu-id="2a047-346">\<connectionStrings></span><span class="sxs-lookup"><span data-stu-id="2a047-346">**\<connectionStrings>**</span></span>
* <span data-ttu-id="2a047-347">\<location></span><span class="sxs-lookup"><span data-stu-id="2a047-347">**\<location>**</span></span>

<span data-ttu-id="2a047-348">会使用其他的配置提供程序配置 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="2a047-348">ASP.NET Core apps are configured using other configuration providers.</span></span> <span data-ttu-id="2a047-349">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="2a047-349">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="application-pools"></a><span data-ttu-id="2a047-350">应用程序池</span><span class="sxs-lookup"><span data-stu-id="2a047-350">Application Pools</span></span>

<span data-ttu-id="2a047-351">在服务器上托管多个网站时，需在每个应用自己的应用池中运行各应用，以彼此隔离。</span><span class="sxs-lookup"><span data-stu-id="2a047-351">When hosting multiple websites on a server, isolate the apps from each other by running each app in its own app pool.</span></span> <span data-ttu-id="2a047-352">IIS“添加网站”对话框默认执行此配置。</span><span class="sxs-lookup"><span data-stu-id="2a047-352">The IIS **Add Website** dialog defaults to this configuration.</span></span> <span data-ttu-id="2a047-353">提供了站点名称时，该文本会自动传输到“应用程序池”文本框。</span><span class="sxs-lookup"><span data-stu-id="2a047-353">When **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="2a047-354">添加站点时，会使用该站点名称创建新的应用池。</span><span class="sxs-lookup"><span data-stu-id="2a047-354">A new app pool is created using the site name when the site is added.</span></span>

## <a name="application-pool-identity"></a><span data-ttu-id="2a047-355">应用程序池标识</span><span class="sxs-lookup"><span data-stu-id="2a047-355">Application Pool Identity</span></span>

<span data-ttu-id="2a047-356">通过应用池标识帐户，可以在唯一帐户下运行应用，而无需创建和管理域或本地帐户。</span><span class="sxs-lookup"><span data-stu-id="2a047-356">An app pool identity account allows an app to run under a unique account without having to create and manage domains or local accounts.</span></span> <span data-ttu-id="2a047-357">在 IIS 8.0 或更高版本上，IIS 管理员工作进程 (WAS) 将使用新应用池的名称创建一个虚拟帐户，并默认在此帐户下运行应用池的工作进程。</span><span class="sxs-lookup"><span data-stu-id="2a047-357">On IIS 8.0 or later, the IIS Admin Worker Process (WAS) creates a virtual account with the name of the new app pool and runs the app pool's worker processes under this account by default.</span></span> <span data-ttu-id="2a047-358">在 IIS 管理控制台中，确保应用池“高级设置”下的“标识”设置为使用 ApplicationPoolIdentity：</span><span class="sxs-lookup"><span data-stu-id="2a047-358">In the IIS Management Console under **Advanced Settings** for the app pool, ensure that the **Identity** is set to use **ApplicationPoolIdentity**:</span></span>

![应用程序池“高级设置”对话框](index/_static/apppool-identity.png)

<span data-ttu-id="2a047-360">IIS 管理进程使用 Windows 安全系统中应用池的名称创建安全标识符。</span><span class="sxs-lookup"><span data-stu-id="2a047-360">The IIS management process creates a secure identifier with the name of the app pool in the Windows Security System.</span></span> <span data-ttu-id="2a047-361">可使用此标识保护资源。</span><span class="sxs-lookup"><span data-stu-id="2a047-361">Resources can be secured using this identity.</span></span> <span data-ttu-id="2a047-362">但是，此标识不是真实的用户帐户，不会在 Windows 用户管理控制台中显示。</span><span class="sxs-lookup"><span data-stu-id="2a047-362">However, this identity isn't a real user account and doesn't show up in the Windows User Management Console.</span></span>

<span data-ttu-id="2a047-363">如果 IIS 工作进程需要对应用的高级访问权限，请为包含该应用的目录修改访问控制列表 (ACL)：</span><span class="sxs-lookup"><span data-stu-id="2a047-363">If the IIS worker process requires elevated access to the app, modify the Access Control List (ACL) for the directory containing the app:</span></span>

1. <span data-ttu-id="2a047-364">打开 Windows 资源管理器并导航到目录。</span><span class="sxs-lookup"><span data-stu-id="2a047-364">Open Windows Explorer and navigate to the directory.</span></span>

1. <span data-ttu-id="2a047-365">右键单击该目录，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="2a047-365">Right-click on the directory and select **Properties**.</span></span>

1. <span data-ttu-id="2a047-366">在“安全”选项卡下，选择“编辑”按钮，然后单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="2a047-366">Under the **Security** tab, select the **Edit** button and then the **Add** button.</span></span>

1. <span data-ttu-id="2a047-367">选择“位置”按钮，并确保该系统处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="2a047-367">Select the **Locations** button and make sure the system is selected.</span></span>

1. <span data-ttu-id="2a047-368">在“输入要选择的对象名称”区域中输入“IIS AppPool\\<app_pool_name>”。</span><span class="sxs-lookup"><span data-stu-id="2a047-368">Enter **IIS AppPool\\<app_pool_name>** in **Enter the object names to select** area.</span></span> <span data-ttu-id="2a047-369">选择“检查名称”按钮。</span><span class="sxs-lookup"><span data-stu-id="2a047-369">Select the **Check Names** button.</span></span> <span data-ttu-id="2a047-370">有关 DefaultAppPool，请检查使用 IIS AppPool\DefaultAppPool 的名称。</span><span class="sxs-lookup"><span data-stu-id="2a047-370">For the *DefaultAppPool* check the names using **IIS AppPool\DefaultAppPool**.</span></span> <span data-ttu-id="2a047-371">当选择“检查名称”按钮时，对象名称区域中会显示 DefaultAppPool 的值。</span><span class="sxs-lookup"><span data-stu-id="2a047-371">When the **Check Names** button is selected, a value of **DefaultAppPool** is indicated in the object names area.</span></span> <span data-ttu-id="2a047-372">无法直接在对象名称区域中输入应用池名称。</span><span class="sxs-lookup"><span data-stu-id="2a047-372">It isn't possible to enter the app pool name directly into the object names area.</span></span> <span data-ttu-id="2a047-373">检查对象名称时，请使用 IIS AppPool\\<app_pool_name> 格式。</span><span class="sxs-lookup"><span data-stu-id="2a047-373">Use the **IIS AppPool\\<app_pool_name>** format when checking for the object name.</span></span>

   ![选择应用文件夹的用户或组对话框：在选择“检查名称”之前，将“DefaultAppPool”的应用池名称追加到对象名称区域中的“IIS AppPool\"。](index/_static/select-users-or-groups-1.png)

1. <span data-ttu-id="2a047-375">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="2a047-375">Select **OK**.</span></span>

   ![选择应用文件夹的用户或组对话框：选择“检查名称”后，对象名称“DefaultAppPool”会显示在对象名称区域中。](index/_static/select-users-or-groups-2.png)

1. <span data-ttu-id="2a047-377">默认情况下应授予读取 &amp; 执行权限。</span><span class="sxs-lookup"><span data-stu-id="2a047-377">Read &amp; execute permissions should be granted by default.</span></span> <span data-ttu-id="2a047-378">根据需要请提供其他权限。</span><span class="sxs-lookup"><span data-stu-id="2a047-378">Provide additional permissions as needed.</span></span>

<span data-ttu-id="2a047-379">也可使用 ICACLS 工具在命令提示符处授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="2a047-379">Access can also be granted at a command prompt using the **ICACLS** tool.</span></span> <span data-ttu-id="2a047-380">以 DefaultAppPool 为例，使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="2a047-380">Using the *DefaultAppPool* as an example, the following command is used:</span></span>

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

<span data-ttu-id="2a047-381">有关详细信息，请参阅 [icacls](/windows-server/administration/windows-commands/icacls) 主题。</span><span class="sxs-lookup"><span data-stu-id="2a047-381">For more information, see the [icacls](/windows-server/administration/windows-commands/icacls) topic.</span></span>

## <a name="deployment-resources-for-iis-administrators"></a><span data-ttu-id="2a047-382">面向 IIS 管理员的部署资源</span><span class="sxs-lookup"><span data-stu-id="2a047-382">Deployment resources for IIS administrators</span></span>

<span data-ttu-id="2a047-383">在 IIS 文档中深入了解 IIS。</span><span class="sxs-lookup"><span data-stu-id="2a047-383">Learn about IIS in-depth in the IIS documentation.</span></span>  
[<span data-ttu-id="2a047-384">IIS 文档</span><span class="sxs-lookup"><span data-stu-id="2a047-384">IIS documentation</span></span>](/iis)

<span data-ttu-id="2a047-385">了解 .NET Core 应用部署模型。</span><span class="sxs-lookup"><span data-stu-id="2a047-385">Learn about .NET Core app deployment models.</span></span>  
[<span data-ttu-id="2a047-386">.NET Core 应用程序部署</span><span class="sxs-lookup"><span data-stu-id="2a047-386">.NET Core application deployment</span></span>](/dotnet/core/deploying/)

<span data-ttu-id="2a047-387">了解 ASP.NET Core 模块如何使 Kestrel Web 服务器将 IIS 或 IIS Express 用作反向代理服务器。</span><span class="sxs-lookup"><span data-stu-id="2a047-387">Learn how the ASP.NET Core Module allows the Kestrel web server to use IIS or IIS Express as a reverse proxy server.</span></span>  
[<span data-ttu-id="2a047-388">ASP.NET Core 模块</span><span class="sxs-lookup"><span data-stu-id="2a047-388">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)

<span data-ttu-id="2a047-389">了解如何配置 ASP.NET Core 模块以托管 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="2a047-389">Learn how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span>  
[<span data-ttu-id="2a047-390">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="2a047-390">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)

<span data-ttu-id="2a047-391">了解已发布的 ASP.NET Core 应用的目录结构。</span><span class="sxs-lookup"><span data-stu-id="2a047-391">Learn about the directory structure of published ASP.NET Core apps.</span></span>  
[<span data-ttu-id="2a047-392">目录结构</span><span class="sxs-lookup"><span data-stu-id="2a047-392">Directory structure</span></span>](xref:host-and-deploy/directory-structure)

<span data-ttu-id="2a047-393">了解适用于 ASP.NET Core 应用的活动和非活动 IIS 模块以及如何管理 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="2a047-393">Discover active and inactive IIS modules for ASP.NET Core apps and how to manage IIS modules.</span></span>  
[<span data-ttu-id="2a047-394">IIS 模块</span><span class="sxs-lookup"><span data-stu-id="2a047-394">IIS modules</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="2a047-395">了解如何诊断 ASP.NET Core 应用的 IIS 部署的问题。</span><span class="sxs-lookup"><span data-stu-id="2a047-395">Learn how to diagnose problems with IIS deployments of ASP.NET Core apps.</span></span>  
[<span data-ttu-id="2a047-396">疑难解答</span><span class="sxs-lookup"><span data-stu-id="2a047-396">Troubleshoot</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="2a047-397">了解在 IIS 上托管 ASP.NET Core 应用的常见错误。</span><span class="sxs-lookup"><span data-stu-id="2a047-397">Distinguish common errors when hosting ASP.NET Core apps on IIS.</span></span>  
[<span data-ttu-id="2a047-398">Azure 应用服务和 IIS 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="2a047-398">Common errors reference for Azure App Service and IIS</span></span>](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a><span data-ttu-id="2a047-399">其他资源</span><span class="sxs-lookup"><span data-stu-id="2a047-399">Additional resources</span></span>

* [<span data-ttu-id="2a047-400">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="2a047-400">Introduction to ASP.NET Core</span></span>](xref:index)
* [<span data-ttu-id="2a047-401">Microsoft IIS 官方网站</span><span class="sxs-lookup"><span data-stu-id="2a047-401">The Official Microsoft IIS Site</span></span>](https://www.iis.net/)
* [<span data-ttu-id="2a047-402">Windows Server 技术内容库</span><span class="sxs-lookup"><span data-stu-id="2a047-402">Windows Server technical content library</span></span>](/windows-server/windows-server)
