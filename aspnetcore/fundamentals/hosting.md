---
title: "在 ASP.NET Core 中承载"
author: guardrex
description: "了解有关 ASP.NET 核心，负责应用程序启动和生存期管理中的 web 主机信息。"
keywords: "ASP.NET 核心 web 主机，IWebHost、 WebHostBuilder、 IHostingEnvironment、 IApplicationLifetime"
ms.author: riande
manager: wpickett
ms.date: 09/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/hosting
ms.openlocfilehash: 054b60206cafc3d6dd5775436995638d7f5700cf
ms.sourcegitcommit: 2d23ea501e0213bbacf65298acf1c8bd17209540
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="ab039-104">在 ASP.NET Core 中承载</span><span class="sxs-lookup"><span data-stu-id="ab039-104">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="ab039-105">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ab039-105">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ab039-106">ASP.NET Core 应用配置和启动*主机*。</span><span class="sxs-lookup"><span data-stu-id="ab039-106">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="ab039-107">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="ab039-107">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="ab039-108">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="ab039-108">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="ab039-109">设置主机</span><span class="sxs-lookup"><span data-stu-id="ab039-109">Setting up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ab039-111">创建使用的实例的主机[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)。</span><span class="sxs-lookup"><span data-stu-id="ab039-111">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="ab039-112">这通常在应用程序的入口点，来执行`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-112">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="ab039-113">在项目模板`Main`位于*Program.cs*。</span><span class="sxs-lookup"><span data-stu-id="ab039-113">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="ab039-114">典型*Program.cs*调用[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)来开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="ab039-114">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="ab039-115">`CreateDefaultBuilder`执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="ab039-115">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="ab039-116">配置[Kestrel](servers/kestrel.md)为 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ab039-116">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="ab039-117">有关 Kestrel 默认选项，请参阅[Kestrel 选项部分中 ASP.NET Core Kestrel web 服务器实现](xref:fundamentals/servers/kestrel#kestrel-options)。</span><span class="sxs-lookup"><span data-stu-id="ab039-117">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="ab039-118">将内容的根设置为返回的路径[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)。</span><span class="sxs-lookup"><span data-stu-id="ab039-118">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="ab039-119">从加载可选配置：</span><span class="sxs-lookup"><span data-stu-id="ab039-119">Loads optional configuration from:</span></span>
  * <span data-ttu-id="ab039-120">*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="ab039-120">*appsettings.json*.</span></span>
  * <span data-ttu-id="ab039-121">*appsettings。{环境}.json*。</span><span class="sxs-lookup"><span data-stu-id="ab039-121">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="ab039-122">[用户的机密信息](xref:security/app-secrets)运行的应用`Development`环境。</span><span class="sxs-lookup"><span data-stu-id="ab039-122">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="ab039-123">环境变量。</span><span class="sxs-lookup"><span data-stu-id="ab039-123">Environment variables.</span></span>
  * <span data-ttu-id="ab039-124">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="ab039-124">Command-line arguments.</span></span>
* <span data-ttu-id="ab039-125">配置[日志记录](xref:fundamentals/logging/index)控制台和调试输出。</span><span class="sxs-lookup"><span data-stu-id="ab039-125">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="ab039-126">日志记录包含[日志筛选](xref:fundamentals/logging/index#log-filtering)日志记录配置部分中指定的规则*appsettings.json*或*appsettings。 {环境}.json*文件。</span><span class="sxs-lookup"><span data-stu-id="ab039-126">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="ab039-127">当运行 IIS 之后，可让[IIS 集成](xref:publishing/iis)。</span><span class="sxs-lookup"><span data-stu-id="ab039-127">When running behind IIS, enables [IIS integration](xref:publishing/iis).</span></span> <span data-ttu-id="ab039-128">配置的基路径和服务器应对其侦听时使用的端口[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="ab039-128">Configures the base path and port the server should listen on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="ab039-129">该模块将创建 IIS 和 Kestrel 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="ab039-129">The module creates a reverse-proxy between IIS and Kestrel.</span></span> <span data-ttu-id="ab039-130">此外可以配置应用到[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="ab039-130">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="ab039-131">有关 IIS 默认选项，请参阅[IIS 选项部分中的主机与 IIS 的 Windows 上的 ASP.NET 核心](xref:publishing/iis#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="ab039-131">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:publishing/iis#iis-options).</span></span>

<span data-ttu-id="ab039-132">*内容根*确定主机搜索内容的文件，如 MVC 视图文件的位置。</span><span class="sxs-lookup"><span data-stu-id="ab039-132">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="ab039-133">应用程序启动时从项目的根文件夹，则会将项目的根文件夹用作内容的根。</span><span class="sxs-lookup"><span data-stu-id="ab039-133">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="ab039-134">这是默认值中使用[Visual Studio](https://www.visualstudio.com/)和[dotnet 新模板](/dotnet/core/tools/dotnet-new)。</span><span class="sxs-lookup"><span data-stu-id="ab039-134">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="ab039-135">应用配置的详细信息，请参阅[ASP.NET 核心中的配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="ab039-135">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="ab039-136">作为使用静态的替代方法`CreateDefaultBuilder`方法，创建从宿主[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)是一种受支持的方法与 ASP.NET 核心 2.x。</span><span class="sxs-lookup"><span data-stu-id="ab039-136">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="ab039-137">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ab039-137">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-139">创建使用的实例的主机[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)。</span><span class="sxs-lookup"><span data-stu-id="ab039-139">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="ab039-140">创建宿主应用程序的入口点，通常执行`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-140">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="ab039-141">在项目模板`Main`位于*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="ab039-141">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="ab039-142">`WebHostBuilder`需要[服务器实现 IServer](servers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ab039-142">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="ab039-143">内置服务器[Kestrel](servers/kestrel.md)和[HTTP.sys](servers/httpsys.md) (之前的 ASP.NET 核心 2.0 版本中，HTTP.sys 调用[WebListener](xref:fundamentals/servers/weblistener))。</span><span class="sxs-lookup"><span data-stu-id="ab039-143">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="ab039-144">在此示例中， [UseKestrel 扩展方法](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)指定的 Kestrel 服务器。</span><span class="sxs-lookup"><span data-stu-id="ab039-144">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="ab039-145">*内容根*确定主机搜索内容的文件，如 MVC 视图文件的位置。</span><span class="sxs-lookup"><span data-stu-id="ab039-145">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="ab039-146">默认内容根获得的`UseContentRoot`通过[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)。</span><span class="sxs-lookup"><span data-stu-id="ab039-146">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="ab039-147">应用程序启动时从项目的根文件夹，则会将项目的根文件夹用作内容的根。</span><span class="sxs-lookup"><span data-stu-id="ab039-147">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="ab039-148">这是默认值中使用[Visual Studio](https://www.visualstudio.com/)和[dotnet 新模板](/dotnet/core/tools/dotnet-new)。</span><span class="sxs-lookup"><span data-stu-id="ab039-148">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="ab039-149">若要使用 IIS 的反向代理，调用[UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)生成主机的一部分。</span><span class="sxs-lookup"><span data-stu-id="ab039-149">To use IIS as a reverse proxy, call [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="ab039-150">`UseIISIntegration`不配置*服务器*、 like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)未。</span><span class="sxs-lookup"><span data-stu-id="ab039-150">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="ab039-151">`UseIISIntegration`配置的基路径和服务器应对其侦听时使用的端口[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)创建 Kestrel 和 IIS 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="ab039-151">`UseIISIntegration` configures the base path and port the server should listen on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse-proxy between Kestrel and IIS.</span></span> <span data-ttu-id="ab039-152">要 IIS 用于 ASP.NET Core`UseKestrel`和`UseIISIntegration`必须指定。</span><span class="sxs-lookup"><span data-stu-id="ab039-152">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="ab039-153">`UseIISIntegration`仅当在 IIS 或 IIS Express 后面运行时激活。</span><span class="sxs-lookup"><span data-stu-id="ab039-153">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="ab039-154">有关详细信息，请参阅[简介 ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)和[ASP.NET 核心模块配置引用](xref:hosting/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="ab039-154">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:hosting/aspnet-core-module).</span></span>

<span data-ttu-id="ab039-155">配置主机 （和 ASP.NET Core 应用） 的最小实现包括指定服务器和应用程序的请求管道的配置项：</span><span class="sxs-lookup"><span data-stu-id="ab039-155">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .Configure(app =>
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    })
    .Build();

host.Run();
```

---

<span data-ttu-id="ab039-156">设置主机时[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1)可以提供方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-156">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="ab039-157">如果`Startup`指定类，它必须定义`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-157">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="ab039-158">有关详细信息，请参阅[在 ASP.NET Core 中的应用程序启动](startup.md)。</span><span class="sxs-lookup"><span data-stu-id="ab039-158">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="ab039-159">多次调用`ConfigureServices`将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="ab039-159">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="ab039-160">多次调用`Configure`或`UseStartup`上`WebHostBuilder`替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="ab039-160">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="ab039-161">主机配置值</span><span class="sxs-lookup"><span data-stu-id="ab039-161">Host configuration values</span></span>

<span data-ttu-id="ab039-162">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)依赖于以下的方法，以将该主机设置配置值：</span><span class="sxs-lookup"><span data-stu-id="ab039-162">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="ab039-163">主机生成器配置，其中包括与格式的环境变量`ASPNETCORE_{configurationKey}`。</span><span class="sxs-lookup"><span data-stu-id="ab039-163">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="ab039-164">例如 `ASPNETCORE_URLS`。</span><span class="sxs-lookup"><span data-stu-id="ab039-164">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="ab039-165">显式方法，如`CaptureStartupErrors`。</span><span class="sxs-lookup"><span data-stu-id="ab039-165">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="ab039-166">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting)和关联的密钥。</span><span class="sxs-lookup"><span data-stu-id="ab039-166">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="ab039-167">设置一个值，该值时`UseSetting`，值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="ab039-167">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="ab039-168">主机使用无论选项上次设置一个值。</span><span class="sxs-lookup"><span data-stu-id="ab039-168">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="ab039-169">有关详细信息，请参阅[重写配置](#overriding-configuration)下一部分中。</span><span class="sxs-lookup"><span data-stu-id="ab039-169">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="ab039-170">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="ab039-170">Capture Startup Errors</span></span>

<span data-ttu-id="ab039-171">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="ab039-171">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="ab039-172">**密钥**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="ab039-172">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="ab039-173">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="ab039-173">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="ab039-174">**默认**： 默认为`false`除非应用程序下运行的 IIS，其中默认值是后面的 Kestrel `true`。</span><span class="sxs-lookup"><span data-stu-id="ab039-174">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="ab039-175">**使用设置**:`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="ab039-175">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="ab039-176">**环境变量**:`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="ab039-176">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="ab039-177">当`false`，退出主机中启动结果时出错。</span><span class="sxs-lookup"><span data-stu-id="ab039-177">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="ab039-178">当`true`，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="ab039-178">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-179">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-179">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-180">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-180">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="ab039-181">内容的根</span><span class="sxs-lookup"><span data-stu-id="ab039-181">Content Root</span></span>

<span data-ttu-id="ab039-182">此设置确定 ASP.NET Core 开始搜索内容的文件，MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="ab039-182">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="ab039-183">**密钥**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="ab039-183">**Key**: contentRoot</span></span>  
<span data-ttu-id="ab039-184">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-184">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-185">**默认**： 默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ab039-185">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="ab039-186">**使用设置**:`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="ab039-186">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="ab039-187">**环境变量**:`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="ab039-187">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="ab039-188">内容的根也用作的基路径[Web 根目录设置](#web-root)。</span><span class="sxs-lookup"><span data-stu-id="ab039-188">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="ab039-189">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="ab039-189">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-190">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-190">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-191">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-191">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="ab039-192">详细的错误</span><span class="sxs-lookup"><span data-stu-id="ab039-192">Detailed Errors</span></span>

<span data-ttu-id="ab039-193">确定详细应该捕获错误。</span><span class="sxs-lookup"><span data-stu-id="ab039-193">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="ab039-194">**密钥**： 之后，请</span><span class="sxs-lookup"><span data-stu-id="ab039-194">**Key**: detailedErrors</span></span>  
<span data-ttu-id="ab039-195">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="ab039-195">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="ab039-196">**默认**: false</span><span class="sxs-lookup"><span data-stu-id="ab039-196">**Default**: false</span></span>  
<span data-ttu-id="ab039-197">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="ab039-197">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="ab039-198">**环境变量**:`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="ab039-198">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="ab039-199">启用 (或当<a href="#environment">环境</a>设置为`Development`)，应用程序捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="ab039-199">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-200">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-200">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-201">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-201">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="ab039-202">环境</span><span class="sxs-lookup"><span data-stu-id="ab039-202">Environment</span></span>

<span data-ttu-id="ab039-203">设置应用程序的环境。</span><span class="sxs-lookup"><span data-stu-id="ab039-203">Sets the app's environment.</span></span>

<span data-ttu-id="ab039-204">**密钥**： 环境</span><span class="sxs-lookup"><span data-stu-id="ab039-204">**Key**: environment</span></span>  
<span data-ttu-id="ab039-205">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-205">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-206">**默认**： 生产</span><span class="sxs-lookup"><span data-stu-id="ab039-206">**Default**: Production</span></span>  
<span data-ttu-id="ab039-207">**使用设置**:`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="ab039-207">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="ab039-208">**环境变量**:`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="ab039-208">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="ab039-209">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="ab039-209">The environment can be set to any value.</span></span> <span data-ttu-id="ab039-210">框架定义的值包括`Development`， `Staging`，和`Production`。</span><span class="sxs-lookup"><span data-stu-id="ab039-210">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="ab039-211">值都不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="ab039-211">Values aren't case sensitive.</span></span> <span data-ttu-id="ab039-212">默认情况下，*环境*从读取`ASPNETCORE_ENVIRONMENT`环境变量。</span><span class="sxs-lookup"><span data-stu-id="ab039-212">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="ab039-213">使用时[Visual Studio](https://www.visualstudio.com/)，可能会设置环境变量*launchSettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="ab039-213">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="ab039-214">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="ab039-214">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-215">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-215">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-216">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-216">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="ab039-217">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="ab039-217">Hosting Startup Assemblies</span></span>

<span data-ttu-id="ab039-218">设置应用程序的宿主启动程序集。</span><span class="sxs-lookup"><span data-stu-id="ab039-218">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="ab039-219">**密钥**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="ab039-219">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="ab039-220">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-220">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-221">**默认**： 空字符串</span><span class="sxs-lookup"><span data-stu-id="ab039-221">**Default**: Empty string</span></span>  
<span data-ttu-id="ab039-222">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="ab039-222">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="ab039-223">**环境变量**:`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="ab039-223">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="ab039-224">托管要在启动时加载的启动程序集的以分号分隔的字符串。</span><span class="sxs-lookup"><span data-stu-id="ab039-224">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="ab039-225">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="ab039-225">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="ab039-226">虽然配置值默认为空字符串，宿主启动程序集将始终包括应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="ab039-226">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="ab039-227">宿主启动程序集提供时，它们正在加载应用程序在启动过程中生成其公共服务时添加到应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="ab039-227">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-228">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-228">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-229">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-229">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-230">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="ab039-230">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="ab039-231">选择承载 Url</span><span class="sxs-lookup"><span data-stu-id="ab039-231">Prefer Hosting URLs</span></span>

<span data-ttu-id="ab039-232">指示是否应在使用配置的 Url 上侦听主机`WebHostBuilder`而不使用配置`IServer`实现。</span><span class="sxs-lookup"><span data-stu-id="ab039-232">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="ab039-233">**密钥**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="ab039-233">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="ab039-234">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="ab039-234">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="ab039-235">**默认**: true</span><span class="sxs-lookup"><span data-stu-id="ab039-235">**Default**: true</span></span>  
<span data-ttu-id="ab039-236">**使用设置**:`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="ab039-236">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="ab039-237">**环境变量**:`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="ab039-237">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="ab039-238">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="ab039-238">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-239">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-239">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-240">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-240">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-241">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="ab039-241">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="ab039-242">阻止托管启动</span><span class="sxs-lookup"><span data-stu-id="ab039-242">Prevent Hosting Startup</span></span>

<span data-ttu-id="ab039-243">可防止托管启动程序集，包括承载应用程序的程序集所配置的启动程序集的自动加载。</span><span class="sxs-lookup"><span data-stu-id="ab039-243">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="ab039-244">请参阅[从外部程序集使用 IHostingStartup 添加应用程序功能](xref:hosting/ihostingstartup)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="ab039-244">See [Add app features from an external assembly using IHostingStartup](xref:hosting/ihostingstartup) for more information.</span></span>

<span data-ttu-id="ab039-245">**密钥**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="ab039-245">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="ab039-246">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="ab039-246">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="ab039-247">**默认**: false</span><span class="sxs-lookup"><span data-stu-id="ab039-247">**Default**: false</span></span>  
<span data-ttu-id="ab039-248">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="ab039-248">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="ab039-249">**环境变量**:`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="ab039-249">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="ab039-250">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="ab039-250">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-251">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-251">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-252">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-252">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-253">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="ab039-253">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="ab039-254">服务器 Url</span><span class="sxs-lookup"><span data-stu-id="ab039-254">Server URLs</span></span>

<span data-ttu-id="ab039-255">指示的 IP 地址或主机地址的端口和服务器应侦听的请求的协议。</span><span class="sxs-lookup"><span data-stu-id="ab039-255">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="ab039-256">**密钥**: url</span><span class="sxs-lookup"><span data-stu-id="ab039-256">**Key**: urls</span></span>  
<span data-ttu-id="ab039-257">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-257">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-258">**默认**: http://localhost:5000/</span><span class="sxs-lookup"><span data-stu-id="ab039-258">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="ab039-259">**使用设置**:`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="ab039-259">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="ab039-260">**环境变量**:`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="ab039-260">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="ab039-261">设置为以分号分隔 （;） 的 URL 的列表添加到服务器应响应以下前缀。</span><span class="sxs-lookup"><span data-stu-id="ab039-261">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="ab039-262">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="ab039-262">For example, `http://localhost:123`.</span></span> <span data-ttu-id="ab039-263">使用"\*"以指示服务器应侦听上任何 IP 地址或主机名使用指定的端口和协议的请求 (例如， `http://*:5000`)。</span><span class="sxs-lookup"><span data-stu-id="ab039-263">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="ab039-264">协议 (`http://`或`https://`) 必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="ab039-264">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="ab039-265">支持的格式有所不同服务器。</span><span class="sxs-lookup"><span data-stu-id="ab039-265">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-266">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-266">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="ab039-267">Kestrel 具有其自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="ab039-267">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="ab039-268">有关详细信息，请参阅 [ASP.NET Core 中的 Kestrel Web 服务器实现](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="ab039-268">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-269">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-269">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="ab039-270">关闭超时</span><span class="sxs-lookup"><span data-stu-id="ab039-270">Shutdown Timeout</span></span>

<span data-ttu-id="ab039-271">指定等待 web 主机关闭的时间量。</span><span class="sxs-lookup"><span data-stu-id="ab039-271">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="ab039-272">**密钥**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="ab039-272">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="ab039-273">**类型**: *int*</span><span class="sxs-lookup"><span data-stu-id="ab039-273">**Type**: *int*</span></span>  
<span data-ttu-id="ab039-274">**默认**: 5</span><span class="sxs-lookup"><span data-stu-id="ab039-274">**Default**: 5</span></span>  
<span data-ttu-id="ab039-275">**使用设置**:`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="ab039-275">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="ab039-276">**环境变量**:`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="ab039-276">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="ab039-277">虽然密钥接受*int*与`UseSetting`(例如， `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`)，则`UseShutdownTimeout`扩展方法采用`TimeSpan`。</span><span class="sxs-lookup"><span data-stu-id="ab039-277">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the `UseShutdownTimeout` extension method takes a `TimeSpan`.</span></span> <span data-ttu-id="ab039-278">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="ab039-278">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-279">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-279">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-280">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-280">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-281">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="ab039-281">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="ab039-282">启动程序集</span><span class="sxs-lookup"><span data-stu-id="ab039-282">Startup Assembly</span></span>

<span data-ttu-id="ab039-283">确定要搜索的程序集`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="ab039-283">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="ab039-284">**密钥**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="ab039-284">**Key**: startupAssembly</span></span>  
<span data-ttu-id="ab039-285">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-285">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-286">**默认**： 应用程序的程序集</span><span class="sxs-lookup"><span data-stu-id="ab039-286">**Default**: The app's assembly</span></span>  
<span data-ttu-id="ab039-287">**使用设置**:`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="ab039-287">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="ab039-288">**环境变量**:`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="ab039-288">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="ab039-289">按名称的程序集 (`string`) 或类型 (`TStartup`) 可以引用。</span><span class="sxs-lookup"><span data-stu-id="ab039-289">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="ab039-290">如果选择多个`UseStartup`调用方法，最后一个将优先。</span><span class="sxs-lookup"><span data-stu-id="ab039-290">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-291">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-291">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-292">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-292">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
    ...
```

---

### <a name="web-root"></a><span data-ttu-id="ab039-293">Web 根目录</span><span class="sxs-lookup"><span data-stu-id="ab039-293">Web Root</span></span>

<span data-ttu-id="ab039-294">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="ab039-294">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="ab039-295">**密钥**: webroot</span><span class="sxs-lookup"><span data-stu-id="ab039-295">**Key**: webroot</span></span>  
<span data-ttu-id="ab039-296">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="ab039-296">**Type**: *string*</span></span>  
<span data-ttu-id="ab039-297">**默认**： 如果未指定，默认值是"(Content Root)/wwwroot"，如果该路径存在。</span><span class="sxs-lookup"><span data-stu-id="ab039-297">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="ab039-298">如果路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="ab039-298">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="ab039-299">**使用设置**:`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="ab039-299">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="ab039-300">**环境变量**:`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="ab039-300">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-301">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-301">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-302">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-302">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="ab039-303">重写配置</span><span class="sxs-lookup"><span data-stu-id="ab039-303">Overriding configuration</span></span>

<span data-ttu-id="ab039-304">使用[配置](xref:fundamentals/configuration/index)如何配置主机。</span><span class="sxs-lookup"><span data-stu-id="ab039-304">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="ab039-305">在以下示例中，主机配置 （可选） 中指定*hosting.json*文件。</span><span class="sxs-lookup"><span data-stu-id="ab039-305">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="ab039-306">从加载的任何配置*hosting.json*文件可能会重写通过命令行自变量。</span><span class="sxs-lookup"><span data-stu-id="ab039-306">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="ab039-307">生成的配置 (在`config`) 用于配置与主机`UseConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="ab039-307">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-308">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-308">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ab039-309">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="ab039-309">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="ab039-310">重写提供的配置`UseUrls`与*hosting.json*配置第一个、 命令行自变量配置第二个：</span><span class="sxs-lookup"><span data-stu-id="ab039-310">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();
    }
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-311">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-311">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-312">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="ab039-312">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="ab039-313">重写提供的配置`UseUrls`与*hosting.json*配置第一个、 命令行自变量配置第二个：</span><span class="sxs-lookup"><span data-stu-id="ab039-313">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        var host = new WebHostBuilder()
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .UseKestrel()
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();

        host.Run();
    }
}
```

---

> [!NOTE]
> <span data-ttu-id="ab039-314">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration)扩展方法不是当前能够分析返回的一个配置节`GetSection`(例如， `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="ab039-314">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="ab039-315">`GetSection`方法筛选到请求的节的配置密钥，但会键上的节名称 (例如， `section:urls`， `section:environment`)。</span><span class="sxs-lookup"><span data-stu-id="ab039-315">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="ab039-316">`UseConfiguration`方法需要要匹配的键`WebHostBuilder`密钥 (例如， `urls`， `environment`)。</span><span class="sxs-lookup"><span data-stu-id="ab039-316">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="ab039-317">键的节名称存在阻止从配置主机部分的值。</span><span class="sxs-lookup"><span data-stu-id="ab039-317">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="ab039-318">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="ab039-318">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="ab039-319">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的密钥](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="ab039-319">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="ab039-320">若要指定特定的 URL 上运行的主机，所需的值可以传入在命令提示符下执行时`dotnet run`。</span><span class="sxs-lookup"><span data-stu-id="ab039-320">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing `dotnet run`.</span></span> <span data-ttu-id="ab039-321">命令行参数重写`urls`值从*hosting.json*文件和服务器侦听端口 8080:</span><span class="sxs-lookup"><span data-stu-id="ab039-321">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="ab039-322">正在启动主机</span><span class="sxs-lookup"><span data-stu-id="ab039-322">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ab039-323">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ab039-323">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ab039-324">**运行**</span><span class="sxs-lookup"><span data-stu-id="ab039-324">**Run**</span></span>

<span data-ttu-id="ab039-325">`Run`方法会启动 web 应用，并阻止调用线程，直到该主机是关闭：</span><span class="sxs-lookup"><span data-stu-id="ab039-325">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="ab039-326">**Start**</span><span class="sxs-lookup"><span data-stu-id="ab039-326">**Start**</span></span>

<span data-ttu-id="ab039-327">通过调用非阻止方式运行主机其`Start`方法：</span><span class="sxs-lookup"><span data-stu-id="ab039-327">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="ab039-328">如果 Url 的列表传递给`Start`方法，它侦听指定的 Url:</span><span class="sxs-lookup"><span data-stu-id="ab039-328">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

<span data-ttu-id="ab039-329">应用程序可以初始化并启动新的主机使用的预配置的默认值`CreateDefaultBuilder`使用静态便捷方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-329">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="ab039-330">这些方法启动服务器控制台输出而无需与[WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)等待中断 （Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="ab039-330">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="ab039-331">**开始 （RequestDelegate 应用程序）**</span><span class="sxs-lookup"><span data-stu-id="ab039-331">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="ab039-332">开头`RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="ab039-332">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-333">在浏览器向发出请求`http://localhost:5000`接收响应"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="ab039-333">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="ab039-334">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="ab039-334">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="ab039-335">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="ab039-335">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="ab039-336">**启动 (字符串 url，RequestDelegate 应用)**</span><span class="sxs-lookup"><span data-stu-id="ab039-336">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="ab039-337">使用 URL 启动和`RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="ab039-337">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-338">生成与相同的结果**开始 （RequestDelegate 应用程序）**，除应用程序响应上`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="ab039-338">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="ab039-339">**启动 (操作<IRouteBuilder>routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="ab039-339">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="ab039-340">使用的实例`IRouteBuilder`([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由的中间件：</span><span class="sxs-lookup"><span data-stu-id="ab039-340">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-341">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="ab039-341">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="ab039-342">请求</span><span class="sxs-lookup"><span data-stu-id="ab039-342">Request</span></span>                                    | <span data-ttu-id="ab039-343">响应</span><span class="sxs-lookup"><span data-stu-id="ab039-343">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="ab039-344">Hello，Martin ！</span><span class="sxs-lookup"><span data-stu-id="ab039-344">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="ab039-345">布宜诺斯艾利斯 dias，Catrina ！</span><span class="sxs-lookup"><span data-stu-id="ab039-345">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="ab039-346">引发"ooops ！"的字符串与异常</span><span class="sxs-lookup"><span data-stu-id="ab039-346">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="ab039-347">用字符串引发异常"不过这噢 ！"</span><span class="sxs-lookup"><span data-stu-id="ab039-347">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="ab039-348">Sante，Kevin ！</span><span class="sxs-lookup"><span data-stu-id="ab039-348">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="ab039-349">Hello World!</span><span class="sxs-lookup"><span data-stu-id="ab039-349">Hello World!</span></span>                             |

<span data-ttu-id="ab039-350">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="ab039-350">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="ab039-351">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="ab039-351">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="ab039-352">**启动 (字符串 url，操作<IRouteBuilder>routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="ab039-352">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="ab039-353">使用 URL 和的实例`IRouteBuilder`:</span><span class="sxs-lookup"><span data-stu-id="ab039-353">Use a URL and an instance of `IRouteBuilder`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-354">生成与相同的结果**启动 (操作<IRouteBuilder>routeBuilder)**，除应用程序响应在`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="ab039-354">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="ab039-355">**StartWith (操作<IApplicationBuilder>应用)**</span><span class="sxs-lookup"><span data-stu-id="ab039-355">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="ab039-356">提供一个委托，以配置`IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="ab039-356">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-357">在浏览器向发出请求`http://localhost:5000`接收响应"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="ab039-357">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="ab039-358">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="ab039-358">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="ab039-359">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="ab039-359">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="ab039-360">**StartWith (字符串 url，操作<IApplicationBuilder>应用)**</span><span class="sxs-lookup"><span data-stu-id="ab039-360">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="ab039-361">提供一个 URL，另一个委托，以配置`IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="ab039-361">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="ab039-362">生成与相同的结果**StartWith (操作<IApplicationBuilder>应用)**，除应用程序响应上`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="ab039-362">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ab039-363">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ab039-363">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ab039-364">**运行**</span><span class="sxs-lookup"><span data-stu-id="ab039-364">**Run**</span></span>

<span data-ttu-id="ab039-365">`Run`方法会启动 web 应用，并阻止调用线程，直到主机关闭的情况下：</span><span class="sxs-lookup"><span data-stu-id="ab039-365">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="ab039-366">**Start**</span><span class="sxs-lookup"><span data-stu-id="ab039-366">**Start**</span></span>

<span data-ttu-id="ab039-367">通过调用非阻止方式运行主机其`Start`方法：</span><span class="sxs-lookup"><span data-stu-id="ab039-367">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="ab039-368">如果 Url 的列表传递给`Start`方法，它侦听指定的 Url:</span><span class="sxs-lookup"><span data-stu-id="ab039-368">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

---

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="ab039-369">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="ab039-369">IHostingEnvironment interface</span></span>

<span data-ttu-id="ab039-370">[IHostingEnvironment 接口](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用程序的 web 宿主环境的信息。</span><span class="sxs-lookup"><span data-stu-id="ab039-370">The [IHostingEnvironment interface](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="ab039-371">使用[构造函数注入](xref:fundamentals/dependency-injection)获取`IHostingEnvironment`才能使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="ab039-371">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

<span data-ttu-id="ab039-372">A[基于约定的方法](xref:fundamentals/environments#startup-conventions)可以用于在启动时基于环境配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="ab039-372">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="ab039-373">或者，将注入`IHostingEnvironment`到`Startup`构造函数用于`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ab039-373">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> <span data-ttu-id="ab039-374">除了`IsDevelopment`扩展方法，`IHostingEnvironment`提供`IsStaging`， `IsProduction`，和`IsEnvironment(string environmentName)`方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-374">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="ab039-375">请参阅[使用多个环境](xref:fundamentals/environments)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="ab039-375">See [Working with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="ab039-376">`IHostingEnvironment`服务还可以被注入直接到`Configure`设置处理管道的方法：</span><span class="sxs-lookup"><span data-stu-id="ab039-376">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

<span data-ttu-id="ab039-377">`IHostingEnvironment`可以将其插入`Invoke`方法时创建自定义[中间件](xref:fundamentals/middleware#writing-middleware):</span><span class="sxs-lookup"><span data-stu-id="ab039-377">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware#writing-middleware):</span></span>

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="ab039-378">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="ab039-378">IApplicationLifetime interface</span></span>

<span data-ttu-id="ab039-379">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime)允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="ab039-379">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="ab039-380">在接口上的三个属性是用于注册的取消标记`Action`定义启动和关闭事件的方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-380">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span> <span data-ttu-id="ab039-381">此外，还有`StopApplication`方法。</span><span class="sxs-lookup"><span data-stu-id="ab039-381">There's also a `StopApplication` method.</span></span>

| <span data-ttu-id="ab039-382">取消标记</span><span class="sxs-lookup"><span data-stu-id="ab039-382">Cancellation Token</span></span>    | <span data-ttu-id="ab039-383">触发时 &#8230;</span><span class="sxs-lookup"><span data-stu-id="ab039-383">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="ab039-384">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="ab039-384">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="ab039-385">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="ab039-385">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="ab039-386">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="ab039-386">Requests may still be processing.</span></span> <span data-ttu-id="ab039-387">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="ab039-387">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="ab039-388">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="ab039-388">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="ab039-389">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="ab039-389">All requests should be processed.</span></span> <span data-ttu-id="ab039-390">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="ab039-390">Shutdown blocks until this event completes.</span></span> |

| <span data-ttu-id="ab039-391">方法</span><span class="sxs-lookup"><span data-stu-id="ab039-391">Method</span></span>            | <span data-ttu-id="ab039-392">操作</span><span class="sxs-lookup"><span data-stu-id="ab039-392">Action</span></span>                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | <span data-ttu-id="ab039-393">当前应用程序请求终止。</span><span class="sxs-lookup"><span data-stu-id="ab039-393">Requests termination of the current application.</span></span> |

```csharp
public class Startup 
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime) 
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="ab039-394">故障排除 System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="ab039-394">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="ab039-395">**适用于仅 ASP.NET Core 2.0**</span><span class="sxs-lookup"><span data-stu-id="ab039-395">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="ab039-396">主机可能生成的将注入`IStartup`直接插入依赖关系注入容器而不是调用`UseStartup`或`Configure`:</span><span class="sxs-lookup"><span data-stu-id="ab039-396">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="ab039-397">如果主机生成这种方式，可能会发生以下错误：</span><span class="sxs-lookup"><span data-stu-id="ab039-397">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="ab039-398">这是因为[applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) （当前程序集） 需扫描`HostingStartupAttributes`。</span><span class="sxs-lookup"><span data-stu-id="ab039-398">This occurs because the [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="ab039-399">如果应用程序手动插入`IStartup`到依赖关系注入容器中，添加对的以下调用`WebHostBuilder`具有指定的程序集名称：</span><span class="sxs-lookup"><span data-stu-id="ab039-399">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="ab039-400">或者，将添加虚拟`Configure`到`WebHostBuilder`，哪些集`applicationName`(`ApplicationKey`) 自动：</span><span class="sxs-lookup"><span data-stu-id="ab039-400">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="ab039-401">**请注意**： 这是仅需要 ASP.NET 核心 2.0 发行版，只有当应用程序不会调用`UseStartup`或`Configure`。</span><span class="sxs-lookup"><span data-stu-id="ab039-401">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="ab039-402">有关详细信息，请参阅[公告： Microsoft.Extensions.PlatformAbstractions 已被删除 （注释）](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938)和[StartupInjection 示例](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)。</span><span class="sxs-lookup"><span data-stu-id="ab039-402">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab039-403">其他资源</span><span class="sxs-lookup"><span data-stu-id="ab039-403">Additional resources</span></span>

* [<span data-ttu-id="ab039-404">发布到使用 IIS 的 Windows</span><span class="sxs-lookup"><span data-stu-id="ab039-404">Publish to Windows using IIS</span></span>](../publishing/iis.md)
* [<span data-ttu-id="ab039-405">将发布到 Linux 使用 Nginx</span><span class="sxs-lookup"><span data-stu-id="ab039-405">Publish to Linux using Nginx</span></span>](../publishing/linuxproduction.md)
* [<span data-ttu-id="ab039-406">将发布到使用 Apache 的 Linux</span><span class="sxs-lookup"><span data-stu-id="ab039-406">Publish to Linux using Apache</span></span>](../publishing/apache-proxy.md)
* [<span data-ttu-id="ab039-407">在 Windows 服务中的主机</span><span class="sxs-lookup"><span data-stu-id="ab039-407">Host in a Windows Service</span></span>](xref:hosting/windows-service)
