---
title: "在 ASP.NET Core 中承载"
author: guardrex
description: "了解有关 ASP.NET 核心，负责应用程序启动和生存期管理中的 web 主机信息。"
ms.author: riande
manager: wpickett
ms.date: 09/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/hosting
ms.openlocfilehash: 7f6712073002b73ca4ddd7586718c81e62cacbc2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="2132e-103">在 ASP.NET Core 中承载</span><span class="sxs-lookup"><span data-stu-id="2132e-103">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="2132e-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="2132e-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="2132e-105">ASP.NET Core 应用配置和启动*主机*。</span><span class="sxs-lookup"><span data-stu-id="2132e-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="2132e-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="2132e-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="2132e-107">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="2132e-107">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="2132e-108">设置主机</span><span class="sxs-lookup"><span data-stu-id="2132e-108">Setting up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="2132e-110">创建使用的实例的主机[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)。</span><span class="sxs-lookup"><span data-stu-id="2132e-110">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="2132e-111">这通常在应用程序的入口点，来执行`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-111">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="2132e-112">在项目模板`Main`位于*Program.cs*。</span><span class="sxs-lookup"><span data-stu-id="2132e-112">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="2132e-113">典型*Program.cs*调用[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)来开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="2132e-113">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="2132e-114">`CreateDefaultBuilder`执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="2132e-114">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="2132e-115">配置[Kestrel](servers/kestrel.md)为 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="2132e-115">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="2132e-116">有关 Kestrel 默认选项，请参阅[Kestrel 选项部分中 ASP.NET Core Kestrel web 服务器实现](xref:fundamentals/servers/kestrel#kestrel-options)。</span><span class="sxs-lookup"><span data-stu-id="2132e-116">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="2132e-117">将内容的根设置为返回的路径[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory)。</span><span class="sxs-lookup"><span data-stu-id="2132e-117">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="2132e-118">从加载可选配置：</span><span class="sxs-lookup"><span data-stu-id="2132e-118">Loads optional configuration from:</span></span>
  * <span data-ttu-id="2132e-119">*appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="2132e-119">*appsettings.json*.</span></span>
  * <span data-ttu-id="2132e-120">*appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="2132e-120">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="2132e-121">[用户的机密信息](xref:security/app-secrets)运行的应用`Development`环境。</span><span class="sxs-lookup"><span data-stu-id="2132e-121">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="2132e-122">环境变量。</span><span class="sxs-lookup"><span data-stu-id="2132e-122">Environment variables.</span></span>
  * <span data-ttu-id="2132e-123">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="2132e-123">Command-line arguments.</span></span>
* <span data-ttu-id="2132e-124">配置[日志记录](xref:fundamentals/logging/index)控制台和调试输出。</span><span class="sxs-lookup"><span data-stu-id="2132e-124">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="2132e-125">日志记录包含[日志筛选](xref:fundamentals/logging/index#log-filtering)日志记录配置部分中指定的规则*appsettings.json*或*appsettings。 {环境}.json*文件。</span><span class="sxs-lookup"><span data-stu-id="2132e-125">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="2132e-126">当运行 IIS 之后，可让[IIS 集成](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="2132e-126">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="2132e-127">配置的基路径和使用时，该服务器侦听的端口[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2132e-127">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="2132e-128">该模块将创建 IIS 和 Kestrel 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="2132e-128">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="2132e-129">此外可以配置应用到[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="2132e-129">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="2132e-130">有关 IIS 默认选项，请参阅[IIS 选项部分中的主机与 IIS 的 Windows 上的 ASP.NET 核心](xref:host-and-deploy/iis/index#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="2132e-130">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="2132e-131">*内容根*确定主机搜索内容的文件，如 MVC 视图文件的位置。</span><span class="sxs-lookup"><span data-stu-id="2132e-131">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="2132e-132">应用程序启动时从项目的根文件夹，则会将项目的根文件夹用作内容的根。</span><span class="sxs-lookup"><span data-stu-id="2132e-132">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="2132e-133">这是默认值中使用[Visual Studio](https://www.visualstudio.com/)和[dotnet 新模板](/dotnet/core/tools/dotnet-new)。</span><span class="sxs-lookup"><span data-stu-id="2132e-133">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="2132e-134">应用配置的详细信息，请参阅[ASP.NET 核心中的配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="2132e-134">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="2132e-135">作为使用静态的替代方法`CreateDefaultBuilder`方法，创建从宿主[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)是一种受支持的方法与 ASP.NET 核心 2.x。</span><span class="sxs-lookup"><span data-stu-id="2132e-135">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="2132e-136">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="2132e-136">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-138">创建使用的实例的主机[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)。</span><span class="sxs-lookup"><span data-stu-id="2132e-138">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="2132e-139">创建宿主应用程序的入口点，通常执行`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-139">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="2132e-140">在项目模板`Main`位于*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="2132e-140">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="2132e-141">`WebHostBuilder`需要[服务器实现 IServer](servers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2132e-141">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="2132e-142">内置服务器[Kestrel](servers/kestrel.md)和[HTTP.sys](servers/httpsys.md) (之前的 ASP.NET 核心 2.0 版本中，HTTP.sys 调用[WebListener](xref:fundamentals/servers/weblistener))。</span><span class="sxs-lookup"><span data-stu-id="2132e-142">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="2132e-143">在此示例中， [UseKestrel 扩展方法](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)指定的 Kestrel 服务器。</span><span class="sxs-lookup"><span data-stu-id="2132e-143">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="2132e-144">*内容根*确定主机搜索内容的文件，如 MVC 视图文件的位置。</span><span class="sxs-lookup"><span data-stu-id="2132e-144">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="2132e-145">默认内容根获得的`UseContentRoot`通过[Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1)。</span><span class="sxs-lookup"><span data-stu-id="2132e-145">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="2132e-146">应用程序启动时从项目的根文件夹，则会将项目的根文件夹用作内容的根。</span><span class="sxs-lookup"><span data-stu-id="2132e-146">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="2132e-147">这是默认值中使用[Visual Studio](https://www.visualstudio.com/)和[dotnet 新模板](/dotnet/core/tools/dotnet-new)。</span><span class="sxs-lookup"><span data-stu-id="2132e-147">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="2132e-148">若要使用 IIS 的反向代理，调用[UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions)生成主机的一部分。</span><span class="sxs-lookup"><span data-stu-id="2132e-148">To use IIS as a reverse proxy, call [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="2132e-149">`UseIISIntegration`不配置*服务器*、 like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)未。</span><span class="sxs-lookup"><span data-stu-id="2132e-149">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="2132e-150">`UseIISIntegration`配置的基路径和使用时，该服务器侦听的端口[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)创建 Kestrel 和 IIS 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="2132e-150">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="2132e-151">要 IIS 用于 ASP.NET Core`UseKestrel`和`UseIISIntegration`必须指定。</span><span class="sxs-lookup"><span data-stu-id="2132e-151">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="2132e-152">`UseIISIntegration`仅当在 IIS 或 IIS Express 后面运行时激活。</span><span class="sxs-lookup"><span data-stu-id="2132e-152">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="2132e-153">有关详细信息，请参阅[简介 ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)和[ASP.NET 核心模块配置引用](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="2132e-153">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="2132e-154">配置主机 （和 ASP.NET Core 应用） 的最小实现包括指定服务器和应用程序的请求管道的配置项：</span><span class="sxs-lookup"><span data-stu-id="2132e-154">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

<span data-ttu-id="2132e-155">设置主机时[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1)可以提供方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-155">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="2132e-156">如果`Startup`指定类，它必须定义`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-156">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="2132e-157">有关详细信息，请参阅[在 ASP.NET Core 中的应用程序启动](startup.md)。</span><span class="sxs-lookup"><span data-stu-id="2132e-157">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="2132e-158">多次调用`ConfigureServices`将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="2132e-158">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="2132e-159">多次调用`Configure`或`UseStartup`上`WebHostBuilder`替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="2132e-159">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="2132e-160">主机配置值</span><span class="sxs-lookup"><span data-stu-id="2132e-160">Host configuration values</span></span>

<span data-ttu-id="2132e-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)依赖于以下的方法，以将该主机设置配置值：</span><span class="sxs-lookup"><span data-stu-id="2132e-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="2132e-162">主机生成器配置，其中包括与格式的环境变量`ASPNETCORE_{configurationKey}`。</span><span class="sxs-lookup"><span data-stu-id="2132e-162">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="2132e-163">例如 `ASPNETCORE_URLS`。</span><span class="sxs-lookup"><span data-stu-id="2132e-163">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="2132e-164">显式方法，如`CaptureStartupErrors`。</span><span class="sxs-lookup"><span data-stu-id="2132e-164">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="2132e-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting)和关联的密钥。</span><span class="sxs-lookup"><span data-stu-id="2132e-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="2132e-166">设置一个值，该值时`UseSetting`，值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="2132e-166">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="2132e-167">主机使用无论选项上次设置一个值。</span><span class="sxs-lookup"><span data-stu-id="2132e-167">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="2132e-168">有关详细信息，请参阅[重写配置](#overriding-configuration)下一部分中。</span><span class="sxs-lookup"><span data-stu-id="2132e-168">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="2132e-169">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="2132e-169">Capture Startup Errors</span></span>

<span data-ttu-id="2132e-170">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="2132e-170">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="2132e-171">**密钥**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="2132e-171">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="2132e-172">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="2132e-172">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="2132e-173">**默认**： 默认为`false`除非应用程序下运行的 IIS，其中默认值是后面的 Kestrel `true`。</span><span class="sxs-lookup"><span data-stu-id="2132e-173">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="2132e-174">**使用设置**:`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="2132e-174">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="2132e-175">**环境变量**:`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="2132e-175">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="2132e-176">当`false`，退出主机中启动结果时出错。</span><span class="sxs-lookup"><span data-stu-id="2132e-176">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="2132e-177">当`true`，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="2132e-177">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-178">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-178">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-179">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-179">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="2132e-180">内容的根</span><span class="sxs-lookup"><span data-stu-id="2132e-180">Content Root</span></span>

<span data-ttu-id="2132e-181">此设置确定 ASP.NET Core 开始搜索内容的文件，MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="2132e-181">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="2132e-182">**密钥**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="2132e-182">**Key**: contentRoot</span></span>  
<span data-ttu-id="2132e-183">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-183">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-184">**默认**： 默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="2132e-184">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="2132e-185">**使用设置**:`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="2132e-185">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="2132e-186">**环境变量**:`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="2132e-186">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="2132e-187">内容的根也用作的基路径[Web 根目录设置](#web-root)。</span><span class="sxs-lookup"><span data-stu-id="2132e-187">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="2132e-188">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="2132e-188">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-189">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-189">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-190">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-190">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="2132e-191">详细的错误</span><span class="sxs-lookup"><span data-stu-id="2132e-191">Detailed Errors</span></span>

<span data-ttu-id="2132e-192">确定详细应该捕获错误。</span><span class="sxs-lookup"><span data-stu-id="2132e-192">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="2132e-193">**密钥**： 之后，请</span><span class="sxs-lookup"><span data-stu-id="2132e-193">**Key**: detailedErrors</span></span>  
<span data-ttu-id="2132e-194">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="2132e-194">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="2132e-195">**默认**: false</span><span class="sxs-lookup"><span data-stu-id="2132e-195">**Default**: false</span></span>  
<span data-ttu-id="2132e-196">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="2132e-196">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="2132e-197">**环境变量**:`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="2132e-197">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="2132e-198">启用 (或当<a href="#environment">环境</a>设置为`Development`)，应用程序捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="2132e-198">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-199">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-199">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-200">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-200">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="2132e-201">环境</span><span class="sxs-lookup"><span data-stu-id="2132e-201">Environment</span></span>

<span data-ttu-id="2132e-202">设置应用程序的环境。</span><span class="sxs-lookup"><span data-stu-id="2132e-202">Sets the app's environment.</span></span>

<span data-ttu-id="2132e-203">**密钥**： 环境</span><span class="sxs-lookup"><span data-stu-id="2132e-203">**Key**: environment</span></span>  
<span data-ttu-id="2132e-204">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-204">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-205">**默认**： 生产</span><span class="sxs-lookup"><span data-stu-id="2132e-205">**Default**: Production</span></span>  
<span data-ttu-id="2132e-206">**使用设置**:`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="2132e-206">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="2132e-207">**环境变量**:`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="2132e-207">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="2132e-208">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="2132e-208">The environment can be set to any value.</span></span> <span data-ttu-id="2132e-209">框架定义的值包括`Development`， `Staging`，和`Production`。</span><span class="sxs-lookup"><span data-stu-id="2132e-209">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="2132e-210">值都不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="2132e-210">Values aren't case sensitive.</span></span> <span data-ttu-id="2132e-211">默认情况下，*环境*从读取`ASPNETCORE_ENVIRONMENT`环境变量。</span><span class="sxs-lookup"><span data-stu-id="2132e-211">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="2132e-212">使用时[Visual Studio](https://www.visualstudio.com/)，可能会设置环境变量*launchSettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="2132e-212">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="2132e-213">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="2132e-213">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-214">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-214">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-215">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-215">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="2132e-216">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="2132e-216">Hosting Startup Assemblies</span></span>

<span data-ttu-id="2132e-217">设置应用程序的宿主启动程序集。</span><span class="sxs-lookup"><span data-stu-id="2132e-217">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="2132e-218">**密钥**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="2132e-218">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="2132e-219">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-219">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-220">**默认**： 空字符串</span><span class="sxs-lookup"><span data-stu-id="2132e-220">**Default**: Empty string</span></span>  
<span data-ttu-id="2132e-221">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="2132e-221">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="2132e-222">**环境变量**:`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="2132e-222">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="2132e-223">托管要在启动时加载的启动程序集的以分号分隔的字符串。</span><span class="sxs-lookup"><span data-stu-id="2132e-223">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="2132e-224">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="2132e-224">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="2132e-225">虽然配置值默认为空字符串，宿主启动程序集将始终包括应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="2132e-225">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="2132e-226">宿主启动程序集提供时，它们正在加载应用程序在启动过程中生成其公共服务时添加到应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="2132e-226">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-227">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-228">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-228">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-229">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="2132e-229">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="2132e-230">选择承载 Url</span><span class="sxs-lookup"><span data-stu-id="2132e-230">Prefer Hosting URLs</span></span>

<span data-ttu-id="2132e-231">指示是否应在使用配置的 Url 上侦听主机`WebHostBuilder`而不使用配置`IServer`实现。</span><span class="sxs-lookup"><span data-stu-id="2132e-231">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="2132e-232">**密钥**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="2132e-232">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="2132e-233">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="2132e-233">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="2132e-234">**默认**: true</span><span class="sxs-lookup"><span data-stu-id="2132e-234">**Default**: true</span></span>  
<span data-ttu-id="2132e-235">**使用设置**:`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="2132e-235">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="2132e-236">**环境变量**:`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="2132e-236">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="2132e-237">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="2132e-237">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-238">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-238">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-239">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-239">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-240">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="2132e-240">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="2132e-241">阻止托管启动</span><span class="sxs-lookup"><span data-stu-id="2132e-241">Prevent Hosting Startup</span></span>

<span data-ttu-id="2132e-242">可防止托管启动程序集，包括承载应用程序的程序集所配置的启动程序集的自动加载。</span><span class="sxs-lookup"><span data-stu-id="2132e-242">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="2132e-243">请参阅[从外部程序集使用 IHostingStartup 添加应用程序功能](xref:host-and-deploy/ihostingstartup)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2132e-243">See [Add app features from an external assembly using IHostingStartup](xref:host-and-deploy/ihostingstartup) for more information.</span></span>

<span data-ttu-id="2132e-244">**密钥**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="2132e-244">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="2132e-245">**类型**: *bool* (`true`或`1`)</span><span class="sxs-lookup"><span data-stu-id="2132e-245">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="2132e-246">**默认**: false</span><span class="sxs-lookup"><span data-stu-id="2132e-246">**Default**: false</span></span>  
<span data-ttu-id="2132e-247">**使用设置**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="2132e-247">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="2132e-248">**环境变量**:`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="2132e-248">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="2132e-249">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="2132e-249">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-250">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-250">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-251">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-251">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-252">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="2132e-252">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="2132e-253">服务器 Url</span><span class="sxs-lookup"><span data-stu-id="2132e-253">Server URLs</span></span>

<span data-ttu-id="2132e-254">指示的 IP 地址或主机地址的端口和服务器应侦听的请求的协议。</span><span class="sxs-lookup"><span data-stu-id="2132e-254">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="2132e-255">**密钥**: url</span><span class="sxs-lookup"><span data-stu-id="2132e-255">**Key**: urls</span></span>  
<span data-ttu-id="2132e-256">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-256">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-257">**默认**: http://localhost:5000/</span><span class="sxs-lookup"><span data-stu-id="2132e-257">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="2132e-258">**使用设置**:`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="2132e-258">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="2132e-259">**环境变量**:`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="2132e-259">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="2132e-260">设置为以分号分隔 （;） 的 URL 的列表添加到服务器应响应以下前缀。</span><span class="sxs-lookup"><span data-stu-id="2132e-260">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="2132e-261">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="2132e-261">For example, `http://localhost:123`.</span></span> <span data-ttu-id="2132e-262">使用"\*"以指示服务器应侦听上任何 IP 地址或主机名使用指定的端口和协议的请求 (例如， `http://*:5000`)。</span><span class="sxs-lookup"><span data-stu-id="2132e-262">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="2132e-263">协议 (`http://`或`https://`) 必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="2132e-263">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="2132e-264">支持的格式有所不同服务器。</span><span class="sxs-lookup"><span data-stu-id="2132e-264">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-265">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-265">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="2132e-266">Kestrel 具有其自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="2132e-266">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="2132e-267">有关详细信息，请参阅 [ASP.NET Core 中的 Kestrel Web 服务器实现](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="2132e-267">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-268">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-268">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="2132e-269">关闭超时</span><span class="sxs-lookup"><span data-stu-id="2132e-269">Shutdown Timeout</span></span>

<span data-ttu-id="2132e-270">指定等待 web 主机关闭的时间量。</span><span class="sxs-lookup"><span data-stu-id="2132e-270">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="2132e-271">**密钥**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="2132e-271">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="2132e-272">**类型**: *int*</span><span class="sxs-lookup"><span data-stu-id="2132e-272">**Type**: *int*</span></span>  
<span data-ttu-id="2132e-273">**默认**: 5</span><span class="sxs-lookup"><span data-stu-id="2132e-273">**Default**: 5</span></span>  
<span data-ttu-id="2132e-274">**使用设置**:`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="2132e-274">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="2132e-275">**环境变量**:`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="2132e-275">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="2132e-276">虽然密钥接受*int*与`UseSetting`(例如， `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`)，则`UseShutdownTimeout`扩展方法采用`TimeSpan`。</span><span class="sxs-lookup"><span data-stu-id="2132e-276">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the `UseShutdownTimeout` extension method takes a `TimeSpan`.</span></span> <span data-ttu-id="2132e-277">此功能是 ASP.NET 核心 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="2132e-277">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-278">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-278">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-279">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-279">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-280">此功能将不可用在 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="2132e-280">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="2132e-281">启动程序集</span><span class="sxs-lookup"><span data-stu-id="2132e-281">Startup Assembly</span></span>

<span data-ttu-id="2132e-282">确定要搜索的程序集`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="2132e-282">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="2132e-283">**密钥**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="2132e-283">**Key**: startupAssembly</span></span>  
<span data-ttu-id="2132e-284">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-284">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-285">**默认**： 应用程序的程序集</span><span class="sxs-lookup"><span data-stu-id="2132e-285">**Default**: The app's assembly</span></span>  
<span data-ttu-id="2132e-286">**使用设置**:`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="2132e-286">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="2132e-287">**环境变量**:`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="2132e-287">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="2132e-288">按名称的程序集 (`string`) 或类型 (`TStartup`) 可以引用。</span><span class="sxs-lookup"><span data-stu-id="2132e-288">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="2132e-289">如果选择多个`UseStartup`调用方法，最后一个将优先。</span><span class="sxs-lookup"><span data-stu-id="2132e-289">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-290">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-290">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-291">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-291">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

### <a name="web-root"></a><span data-ttu-id="2132e-292">Web 根目录</span><span class="sxs-lookup"><span data-stu-id="2132e-292">Web Root</span></span>

<span data-ttu-id="2132e-293">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="2132e-293">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="2132e-294">**密钥**: webroot</span><span class="sxs-lookup"><span data-stu-id="2132e-294">**Key**: webroot</span></span>  
<span data-ttu-id="2132e-295">**类型**:*字符串*</span><span class="sxs-lookup"><span data-stu-id="2132e-295">**Type**: *string*</span></span>  
<span data-ttu-id="2132e-296">**默认**： 如果未指定，默认值是"(Content Root)/wwwroot"，如果该路径存在。</span><span class="sxs-lookup"><span data-stu-id="2132e-296">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="2132e-297">如果路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="2132e-297">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="2132e-298">**使用设置**:`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="2132e-298">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="2132e-299">**环境变量**:`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="2132e-299">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-300">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-300">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="2132e-302">重写配置</span><span class="sxs-lookup"><span data-stu-id="2132e-302">Overriding configuration</span></span>

<span data-ttu-id="2132e-303">使用[配置](xref:fundamentals/configuration/index)如何配置主机。</span><span class="sxs-lookup"><span data-stu-id="2132e-303">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="2132e-304">在以下示例中，主机配置 （可选） 中指定*hosting.json*文件。</span><span class="sxs-lookup"><span data-stu-id="2132e-304">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="2132e-305">从加载的任何配置*hosting.json*文件可能会重写通过命令行自变量。</span><span class="sxs-lookup"><span data-stu-id="2132e-305">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="2132e-306">生成的配置 (在`config`) 用于配置与主机`UseConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="2132e-306">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-307">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-307">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="2132e-308">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="2132e-308">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="2132e-309">重写提供的配置`UseUrls`与*hosting.json*配置第一个、 命令行自变量配置第二个：</span><span class="sxs-lookup"><span data-stu-id="2132e-309">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-310">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-310">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-311">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="2132e-311">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="2132e-312">重写提供的配置`UseUrls`与*hosting.json*配置第一个、 命令行自变量配置第二个：</span><span class="sxs-lookup"><span data-stu-id="2132e-312">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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
> <span data-ttu-id="2132e-313">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration)扩展方法不是当前能够分析返回的一个配置节`GetSection`(例如， `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="2132e-313">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="2132e-314">`GetSection`方法筛选到请求的节的配置密钥，但会键上的节名称 (例如， `section:urls`， `section:environment`)。</span><span class="sxs-lookup"><span data-stu-id="2132e-314">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="2132e-315">`UseConfiguration`方法需要要匹配的键`WebHostBuilder`密钥 (例如， `urls`， `environment`)。</span><span class="sxs-lookup"><span data-stu-id="2132e-315">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="2132e-316">键的节名称存在阻止从配置主机部分的值。</span><span class="sxs-lookup"><span data-stu-id="2132e-316">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="2132e-317">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="2132e-317">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="2132e-318">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的密钥](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="2132e-318">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="2132e-319">若要指定特定的 URL 上运行的主机，所需的值可以传入在命令提示符下执行时`dotnet run`。</span><span class="sxs-lookup"><span data-stu-id="2132e-319">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing `dotnet run`.</span></span> <span data-ttu-id="2132e-320">命令行参数重写`urls`值从*hosting.json*文件和服务器侦听端口 8080:</span><span class="sxs-lookup"><span data-stu-id="2132e-320">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="2132e-321">正在启动主机</span><span class="sxs-lookup"><span data-stu-id="2132e-321">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2132e-322">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2132e-322">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="2132e-323">**运行**</span><span class="sxs-lookup"><span data-stu-id="2132e-323">**Run**</span></span>

<span data-ttu-id="2132e-324">`Run`方法会启动 web 应用，并阻止调用线程，直到该主机是关闭：</span><span class="sxs-lookup"><span data-stu-id="2132e-324">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="2132e-325">**Start**</span><span class="sxs-lookup"><span data-stu-id="2132e-325">**Start**</span></span>

<span data-ttu-id="2132e-326">通过调用非阻止方式运行主机其`Start`方法：</span><span class="sxs-lookup"><span data-stu-id="2132e-326">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="2132e-327">如果 Url 的列表传递给`Start`方法，它侦听指定的 Url:</span><span class="sxs-lookup"><span data-stu-id="2132e-327">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="2132e-328">应用程序可以初始化并启动新的主机使用的预配置的默认值`CreateDefaultBuilder`使用静态便捷方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-328">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="2132e-329">这些方法启动服务器控制台输出而无需与[WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown)等待中断 （Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="2132e-329">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="2132e-330">**开始 （RequestDelegate 应用程序）**</span><span class="sxs-lookup"><span data-stu-id="2132e-330">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="2132e-331">开头`RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="2132e-331">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="2132e-332">在浏览器向发出请求`http://localhost:5000`接收响应"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="2132e-332">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="2132e-333">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="2132e-333">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="2132e-334">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="2132e-334">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="2132e-335">**启动 (字符串 url，RequestDelegate 应用)**</span><span class="sxs-lookup"><span data-stu-id="2132e-335">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="2132e-336">使用 URL 启动和`RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="2132e-336">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="2132e-337">生成与相同的结果**开始 （RequestDelegate 应用程序）**，除应用程序响应上`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="2132e-337">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="2132e-338">**Start(Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="2132e-338">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="2132e-339">使用的实例`IRouteBuilder`([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由的中间件：</span><span class="sxs-lookup"><span data-stu-id="2132e-339">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="2132e-340">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="2132e-340">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="2132e-341">请求</span><span class="sxs-lookup"><span data-stu-id="2132e-341">Request</span></span>                                    | <span data-ttu-id="2132e-342">响应</span><span class="sxs-lookup"><span data-stu-id="2132e-342">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="2132e-343">Hello，Martin ！</span><span class="sxs-lookup"><span data-stu-id="2132e-343">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="2132e-344">布宜诺斯艾利斯 dias，Catrina ！</span><span class="sxs-lookup"><span data-stu-id="2132e-344">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="2132e-345">引发"ooops ！"的字符串与异常</span><span class="sxs-lookup"><span data-stu-id="2132e-345">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="2132e-346">用字符串引发异常"不过这噢 ！"</span><span class="sxs-lookup"><span data-stu-id="2132e-346">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="2132e-347">Sante，Kevin ！</span><span class="sxs-lookup"><span data-stu-id="2132e-347">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="2132e-348">Hello World!</span><span class="sxs-lookup"><span data-stu-id="2132e-348">Hello World!</span></span>                             |

<span data-ttu-id="2132e-349">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="2132e-349">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="2132e-350">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="2132e-350">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="2132e-351">**启动 (字符串 url，操作<IRouteBuilder>routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="2132e-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="2132e-352">使用 URL 和的实例`IRouteBuilder`:</span><span class="sxs-lookup"><span data-stu-id="2132e-352">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="2132e-353">生成与相同的结果**启动 (操作<IRouteBuilder>routeBuilder)**，除应用程序响应在`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="2132e-353">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="2132e-354">**StartWith(Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="2132e-354">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="2132e-355">提供一个委托，以配置`IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="2132e-355">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="2132e-356">在浏览器向发出请求`http://localhost:5000`接收响应"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="2132e-356">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="2132e-357">`WaitForShutdown`受到阻止，直到颁发中断 （Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="2132e-357">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="2132e-358">应用程序并显示`Console.WriteLine`消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="2132e-358">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="2132e-359">**StartWith (字符串 url，操作<IApplicationBuilder>应用)**</span><span class="sxs-lookup"><span data-stu-id="2132e-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="2132e-360">提供一个 URL，另一个委托，以配置`IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="2132e-360">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="2132e-361">生成与相同的结果**StartWith (操作<IApplicationBuilder>应用)**，除应用程序响应上`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="2132e-361">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2132e-362">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2132e-362">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2132e-363">**运行**</span><span class="sxs-lookup"><span data-stu-id="2132e-363">**Run**</span></span>

<span data-ttu-id="2132e-364">`Run`方法会启动 web 应用，并阻止调用线程，直到主机关闭的情况下：</span><span class="sxs-lookup"><span data-stu-id="2132e-364">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="2132e-365">**Start**</span><span class="sxs-lookup"><span data-stu-id="2132e-365">**Start**</span></span>

<span data-ttu-id="2132e-366">通过调用非阻止方式运行主机其`Start`方法：</span><span class="sxs-lookup"><span data-stu-id="2132e-366">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="2132e-367">如果 Url 的列表传递给`Start`方法，它侦听指定的 Url:</span><span class="sxs-lookup"><span data-stu-id="2132e-367">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


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

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="2132e-368">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="2132e-368">IHostingEnvironment interface</span></span>

<span data-ttu-id="2132e-369">[IHostingEnvironment 接口](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用程序的 web 宿主环境的信息。</span><span class="sxs-lookup"><span data-stu-id="2132e-369">The [IHostingEnvironment interface](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="2132e-370">使用[构造函数注入](xref:fundamentals/dependency-injection)获取`IHostingEnvironment`才能使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="2132e-370">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="2132e-371">A[基于约定的方法](xref:fundamentals/environments#startup-conventions)可以用于在启动时基于环境配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="2132e-371">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="2132e-372">或者，将注入`IHostingEnvironment`到`Startup`构造函数用于`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="2132e-372">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="2132e-373">除了`IsDevelopment`扩展方法，`IHostingEnvironment`提供`IsStaging`， `IsProduction`，和`IsEnvironment(string environmentName)`方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-373">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="2132e-374">请参阅[使用多个环境](xref:fundamentals/environments)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2132e-374">See [Working with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="2132e-375">`IHostingEnvironment`服务还可以被注入直接到`Configure`设置处理管道的方法：</span><span class="sxs-lookup"><span data-stu-id="2132e-375">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="2132e-376">`IHostingEnvironment`可以将其插入`Invoke`方法时创建自定义[中间件](xref:fundamentals/middleware#writing-middleware):</span><span class="sxs-lookup"><span data-stu-id="2132e-376">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="2132e-377">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="2132e-377">IApplicationLifetime interface</span></span>

<span data-ttu-id="2132e-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime)允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="2132e-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="2132e-379">在接口上的三个属性是用于注册的取消标记`Action`定义启动和关闭事件的方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-379">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span> <span data-ttu-id="2132e-380">此外，还有`StopApplication`方法。</span><span class="sxs-lookup"><span data-stu-id="2132e-380">There's also a `StopApplication` method.</span></span>

| <span data-ttu-id="2132e-381">取消标记</span><span class="sxs-lookup"><span data-stu-id="2132e-381">Cancellation Token</span></span>    | <span data-ttu-id="2132e-382">触发时 &#8230;</span><span class="sxs-lookup"><span data-stu-id="2132e-382">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="2132e-383">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="2132e-383">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="2132e-384">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="2132e-384">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="2132e-385">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="2132e-385">Requests may still be processing.</span></span> <span data-ttu-id="2132e-386">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="2132e-386">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="2132e-387">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="2132e-387">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="2132e-388">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="2132e-388">All requests should be processed.</span></span> <span data-ttu-id="2132e-389">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="2132e-389">Shutdown blocks until this event completes.</span></span> |

| <span data-ttu-id="2132e-390">方法</span><span class="sxs-lookup"><span data-stu-id="2132e-390">Method</span></span>            | <span data-ttu-id="2132e-391">操作</span><span class="sxs-lookup"><span data-stu-id="2132e-391">Action</span></span>                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | <span data-ttu-id="2132e-392">当前应用程序请求终止。</span><span class="sxs-lookup"><span data-stu-id="2132e-392">Requests termination of the current application.</span></span> |

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

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="2132e-393">故障排除 System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="2132e-393">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="2132e-394">**适用于仅 ASP.NET Core 2.0**</span><span class="sxs-lookup"><span data-stu-id="2132e-394">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="2132e-395">主机可能生成的将注入`IStartup`直接插入依赖关系注入容器而不是调用`UseStartup`或`Configure`:</span><span class="sxs-lookup"><span data-stu-id="2132e-395">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="2132e-396">如果主机生成这种方式，可能会发生以下错误：</span><span class="sxs-lookup"><span data-stu-id="2132e-396">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="2132e-397">这是因为[applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) （当前程序集） 需扫描`HostingStartupAttributes`。</span><span class="sxs-lookup"><span data-stu-id="2132e-397">This occurs because the [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="2132e-398">如果应用程序手动插入`IStartup`到依赖关系注入容器中，添加对的以下调用`WebHostBuilder`具有指定的程序集名称：</span><span class="sxs-lookup"><span data-stu-id="2132e-398">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="2132e-399">或者，将添加虚拟`Configure`到`WebHostBuilder`，哪些集`applicationName`(`ApplicationKey`) 自动：</span><span class="sxs-lookup"><span data-stu-id="2132e-399">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="2132e-400">**请注意**： 这是仅需要 ASP.NET 核心 2.0 发行版，只有当应用程序不会调用`UseStartup`或`Configure`。</span><span class="sxs-lookup"><span data-stu-id="2132e-400">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="2132e-401">有关详细信息，请参阅[公告： Microsoft.Extensions.PlatformAbstractions 已被删除 （注释）](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938)和[StartupInjection 示例](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)。</span><span class="sxs-lookup"><span data-stu-id="2132e-401">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2132e-402">其他资源</span><span class="sxs-lookup"><span data-stu-id="2132e-402">Additional resources</span></span>

* [<span data-ttu-id="2132e-403">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="2132e-403">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="2132e-404">在 Linux 上使用 Nginx 进行托管</span><span class="sxs-lookup"><span data-stu-id="2132e-404">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="2132e-405">在 Linux 上使用 Apache 进行托管</span><span class="sxs-lookup"><span data-stu-id="2132e-405">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="2132e-406">在 Windows 服务中的主机</span><span class="sxs-lookup"><span data-stu-id="2132e-406">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
