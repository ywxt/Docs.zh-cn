---
title: "ASP.NET Core 中的托管"
author: guardrex
description: "了解有关 ASP.NET Core 中负责应用启动和生存期管理的 Web 主机。"
manager: wpickett
ms.author: riande
ms.date: 09/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/hosting
ms.openlocfilehash: 004487aebe5262a515e2375c30ccd2a84844dff6
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="3e750-103">ASP.NET Core 中的托管</span><span class="sxs-lookup"><span data-stu-id="3e750-103">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="3e750-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="3e750-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="3e750-105">ASP.NET Core 应用配置和启动“主机”。</span><span class="sxs-lookup"><span data-stu-id="3e750-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="3e750-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="3e750-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="3e750-107">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="3e750-107">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="3e750-108">设置主机</span><span class="sxs-lookup"><span data-stu-id="3e750-108">Setting up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3e750-110">创建使用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-110">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="3e750-111">通常在应用的入口点来执行 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-111">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="3e750-112">在项目模板中，`Main` 位于 Program.cs。</span><span class="sxs-lookup"><span data-stu-id="3e750-112">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="3e750-113">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="3e750-113">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="3e750-114">`CreateDefaultBuilder` 执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="3e750-114">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="3e750-115">配置 [Kestrel](servers/kestrel.md) 为 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="3e750-115">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="3e750-116">有关 Kestrel 默认选项，请参阅[在 ASP.NET Core 中 Kestrel Web 服务器实现的 Kestrel 选项部分](xref:fundamentals/servers/kestrel#kestrel-options)。</span><span class="sxs-lookup"><span data-stu-id="3e750-116">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="3e750-117">将内容根设置为由 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory) 返回的路径。</span><span class="sxs-lookup"><span data-stu-id="3e750-117">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="3e750-118">从下列选项中加载可选配置：</span><span class="sxs-lookup"><span data-stu-id="3e750-118">Loads optional configuration from:</span></span>
  * <span data-ttu-id="3e750-119">appsettings.json。</span><span class="sxs-lookup"><span data-stu-id="3e750-119">*appsettings.json*.</span></span>
  * <span data-ttu-id="3e750-120">appsettings.{Environment}.json。</span><span class="sxs-lookup"><span data-stu-id="3e750-120">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="3e750-121">应用在 `Development` 环境中运行时的[用户机密](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="3e750-121">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="3e750-122">环境变量。</span><span class="sxs-lookup"><span data-stu-id="3e750-122">Environment variables.</span></span>
  * <span data-ttu-id="3e750-123">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="3e750-123">Command-line arguments.</span></span>
* <span data-ttu-id="3e750-124">配置控制台和调试输出的[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="3e750-124">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="3e750-125">日志记录包含 appsettings.json 或 appsettings.{Environment}.json 文件的日志记录配置部分中指定的[日志筛选](xref:fundamentals/logging/index#log-filtering)规则。</span><span class="sxs-lookup"><span data-stu-id="3e750-125">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="3e750-126">在 IIS 后方运行时，启用 [IIS 集成](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="3e750-126">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="3e750-127">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)时配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="3e750-127">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="3e750-128">该模块创建 IIS 与 Kestrel 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="3e750-128">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="3e750-129">还配置应用到[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="3e750-129">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="3e750-130">有关 IIS 默认选项，请参阅[使用 IIS 在 Windows 上托管 ASP.NET Core 的 IIS 选项部分](xref:host-and-deploy/iis/index#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="3e750-130">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="3e750-131">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="3e750-131">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="3e750-132">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="3e750-132">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="3e750-133">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="3e750-133">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="3e750-134">有关应用配置的详细信息，请参阅 [ ASP.NET Core 中的配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="3e750-134">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="3e750-135">作为使用静态 `CreateDefaultBuilder` 方法的替代方法，从 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 创建主机是一种受 ASP.NET Core 2.x 支持的方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-135">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="3e750-136">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3e750-136">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-138">创建使用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-138">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="3e750-139">通常执行 `Main` 方法，在应用的入口点来创建主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-139">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="3e750-140">在项目模板中，`Main` 位于 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="3e750-140">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="3e750-141">`WebHostBuilder` 需要[实现 IServer 的服务器](servers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="3e750-141">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="3e750-142">内置服务器是 [Kestrel](servers/kestrel.md) 和 [HTTP.sys](servers/httpsys.md)（在 ASP.NET Core 2.0 之前的版本中，HTTP.sys 叫做 [WebListener](xref:fundamentals/servers/weblistener)）。</span><span class="sxs-lookup"><span data-stu-id="3e750-142">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="3e750-143">在此示例中，[UseKestrel 扩展方法](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)指定 Kestrel 服务器。</span><span class="sxs-lookup"><span data-stu-id="3e750-143">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="3e750-144">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="3e750-144">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="3e750-145">默认内容根通过 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1) 为 `UseContentRoot` 获得。</span><span class="sxs-lookup"><span data-stu-id="3e750-145">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="3e750-146">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="3e750-146">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="3e750-147">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="3e750-147">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="3e750-148">若要使用 IIS 作为反向代理，调用 [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) 作为生成主机的一部分。</span><span class="sxs-lookup"><span data-stu-id="3e750-148">To use IIS as a reverse proxy, call [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="3e750-149">`UseIISIntegration` 不配置服务器，而 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 要配置。</span><span class="sxs-lookup"><span data-stu-id="3e750-149">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="3e750-150">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)创建 Kestrel 和 IIS 之间的反向代理时，`UseIISIntegration` 配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="3e750-150">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="3e750-151">要在 ASP.NET Core 中使用 IIS，必须指定 `UseKestrel` 和 `UseIISIntegration`。</span><span class="sxs-lookup"><span data-stu-id="3e750-151">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="3e750-152">`UseIISIntegration` 仅在 IIS 或 IIS Express 后方运行时激活。</span><span class="sxs-lookup"><span data-stu-id="3e750-152">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="3e750-153">有关详细信息，请参阅 [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)和 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="3e750-153">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="3e750-154">配置主机 （和 ASP.NET Core 应用） 的最小实现包括指定服务器和应用的请求管道的配置项：</span><span class="sxs-lookup"><span data-stu-id="3e750-154">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

<span data-ttu-id="3e750-155">设置主机时，可以提供[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-155">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="3e750-156">如果指定 `Startup` 类，必须定义 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-156">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="3e750-157">有关详细信息，请参阅 [ASP.NET Core 中的应用程序启动](startup.md)。</span><span class="sxs-lookup"><span data-stu-id="3e750-157">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="3e750-158">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="3e750-158">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="3e750-159">多次调用 `WebHostBuilder` 上的 `Configure` 或 `UseStartup` 将替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="3e750-159">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="3e750-160">主机配置值</span><span class="sxs-lookup"><span data-stu-id="3e750-160">Host configuration values</span></span>

<span data-ttu-id="3e750-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 依赖于以下的方法设置主机配置值：</span><span class="sxs-lookup"><span data-stu-id="3e750-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="3e750-162">主机生成器配置，其中包括格式 `ASPNETCORE_{configurationKey}` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="3e750-162">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="3e750-163">例如 `ASPNETCORE_URLS`。</span><span class="sxs-lookup"><span data-stu-id="3e750-163">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="3e750-164">显式方法，如 `CaptureStartupErrors`。</span><span class="sxs-lookup"><span data-stu-id="3e750-164">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="3e750-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 和关联键。</span><span class="sxs-lookup"><span data-stu-id="3e750-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="3e750-166">使用 `UseSetting` 设置值时，该值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="3e750-166">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="3e750-167">主机使用任何一个选项设置上一个值。</span><span class="sxs-lookup"><span data-stu-id="3e750-167">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="3e750-168">有关详细信息，请参阅下一部分中的[重写配置](#overriding-configuration)。</span><span class="sxs-lookup"><span data-stu-id="3e750-168">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="3e750-169">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="3e750-169">Capture Startup Errors</span></span>

<span data-ttu-id="3e750-170">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="3e750-170">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="3e750-171">**键**：captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="3e750-171">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="3e750-172">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="3e750-172">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="3e750-173">**默认值**：默认为 `false`，除非应用使用 Kestrel 在 IIS 后方运行，其中默认值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="3e750-173">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="3e750-174">**设置使用**：`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="3e750-174">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="3e750-175">**环境变量**：`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="3e750-175">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="3e750-176">当 `false` 时，启动期间出错导致主机退出。</span><span class="sxs-lookup"><span data-stu-id="3e750-176">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="3e750-177">当 `true` 时，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="3e750-177">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-178">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-178">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-179">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-179">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="3e750-180">内容根</span><span class="sxs-lookup"><span data-stu-id="3e750-180">Content Root</span></span>

<span data-ttu-id="3e750-181">此设置确定 ASP.NET Core 开始搜索内容文件，如 MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="3e750-181">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="3e750-182">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="3e750-182">**Key**: contentRoot</span></span>  
<span data-ttu-id="3e750-183">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-183">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-184">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="3e750-184">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="3e750-185">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="3e750-185">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="3e750-186">**环境变量**：`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="3e750-186">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="3e750-187">内容根也用作 [Web 根设置](#web-root)的基路径。</span><span class="sxs-lookup"><span data-stu-id="3e750-187">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="3e750-188">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="3e750-188">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-189">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-189">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-190">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-190">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="3e750-191">详细错误</span><span class="sxs-lookup"><span data-stu-id="3e750-191">Detailed Errors</span></span>

<span data-ttu-id="3e750-192">确定是否应捕获详细错误。</span><span class="sxs-lookup"><span data-stu-id="3e750-192">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="3e750-193">**键**：detailedErrors</span><span class="sxs-lookup"><span data-stu-id="3e750-193">**Key**: detailedErrors</span></span>  
<span data-ttu-id="3e750-194">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="3e750-194">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="3e750-195">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="3e750-195">**Default**: false</span></span>  
<span data-ttu-id="3e750-196">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="3e750-196">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="3e750-197">**环境变量**：`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="3e750-197">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="3e750-198">启用（或当<a href="#environment">环境</a>设置为 `Development` ）时，应用捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="3e750-198">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-199">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-199">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-200">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-200">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="3e750-201">环境</span><span class="sxs-lookup"><span data-stu-id="3e750-201">Environment</span></span>

<span data-ttu-id="3e750-202">设置应用的环境。</span><span class="sxs-lookup"><span data-stu-id="3e750-202">Sets the app's environment.</span></span>

<span data-ttu-id="3e750-203">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="3e750-203">**Key**: environment</span></span>  
<span data-ttu-id="3e750-204">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-204">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-205">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="3e750-205">**Default**: Production</span></span>  
<span data-ttu-id="3e750-206">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="3e750-206">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="3e750-207">**环境变量**：`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="3e750-207">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="3e750-208">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="3e750-208">The environment can be set to any value.</span></span> <span data-ttu-id="3e750-209">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="3e750-209">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="3e750-210">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="3e750-210">Values aren't case sensitive.</span></span> <span data-ttu-id="3e750-211">默认情况下，从 `ASPNETCORE_ENVIRONMENT` 环境变量读取环境。</span><span class="sxs-lookup"><span data-stu-id="3e750-211">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="3e750-212">使用 [Visual Studio](https://www.visualstudio.com/) 时，可能会在 launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="3e750-212">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="3e750-213">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="3e750-213">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-214">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-214">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-215">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-215">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="3e750-216">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="3e750-216">Hosting Startup Assemblies</span></span>

<span data-ttu-id="3e750-217">设置应用的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="3e750-217">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="3e750-218">**键**：hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="3e750-218">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="3e750-219">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-219">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-220">**默认值**：空字符串</span><span class="sxs-lookup"><span data-stu-id="3e750-220">**Default**: Empty string</span></span>  
<span data-ttu-id="3e750-221">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="3e750-221">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="3e750-222">**环境变量**：`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="3e750-222">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="3e750-223">承载启动程序集的以分号分隔的字符串在启动时加载。</span><span class="sxs-lookup"><span data-stu-id="3e750-223">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="3e750-224">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="3e750-224">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="3e750-225">虽然配置值默认为空字符串，但是承载启动程序集会始终包含应用的程序集。</span><span class="sxs-lookup"><span data-stu-id="3e750-225">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="3e750-226">提供承载启动程序集时，当应用在启动过程中生成其公用服务时将它们添加到应用的程序集加载。</span><span class="sxs-lookup"><span data-stu-id="3e750-226">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-227">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-228">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-228">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-229">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="3e750-229">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="3e750-230">首选承载 URL</span><span class="sxs-lookup"><span data-stu-id="3e750-230">Prefer Hosting URLs</span></span>

<span data-ttu-id="3e750-231">指示主机是否应该侦听使用 `WebHostBuilder` 配置的 URL，而不是使用 `IServer` 实现配置的 URL。</span><span class="sxs-lookup"><span data-stu-id="3e750-231">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="3e750-232">**键**：preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="3e750-232">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="3e750-233">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="3e750-233">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="3e750-234">**默认值**：true</span><span class="sxs-lookup"><span data-stu-id="3e750-234">**Default**: true</span></span>  
<span data-ttu-id="3e750-235">**设置使用**：`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="3e750-235">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="3e750-236">**环境变量**：`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="3e750-236">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="3e750-237">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="3e750-237">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-238">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-238">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-239">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-239">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-240">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="3e750-240">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="3e750-241">阻止承载启动</span><span class="sxs-lookup"><span data-stu-id="3e750-241">Prevent Hosting Startup</span></span>

<span data-ttu-id="3e750-242">阻止承载启动程序集自动加载，包括应用的程序集所配置的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="3e750-242">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="3e750-243">有关详细信息，请参阅[使用 IHostingStartup 从外部程序集添加应用功能](xref:host-and-deploy/ihostingstartup)。</span><span class="sxs-lookup"><span data-stu-id="3e750-243">See [Add app features from an external assembly using IHostingStartup](xref:host-and-deploy/ihostingstartup) for more information.</span></span>

<span data-ttu-id="3e750-244">**键**：preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="3e750-244">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="3e750-245">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="3e750-245">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="3e750-246">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="3e750-246">**Default**: false</span></span>  
<span data-ttu-id="3e750-247">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="3e750-247">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="3e750-248">**环境变量**：`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="3e750-248">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="3e750-249">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="3e750-249">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-250">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-250">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-251">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-251">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-252">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="3e750-252">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="3e750-253">服务器 URL</span><span class="sxs-lookup"><span data-stu-id="3e750-253">Server URLs</span></span>

<span data-ttu-id="3e750-254">指示 IP 地址或主机地址，其中包含服务器应针对请求侦听的端口和协议。</span><span class="sxs-lookup"><span data-stu-id="3e750-254">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="3e750-255">**键**：urls</span><span class="sxs-lookup"><span data-stu-id="3e750-255">**Key**: urls</span></span>  
<span data-ttu-id="3e750-256">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-256">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-257">**默认值**：http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="3e750-257">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="3e750-258">**设置使用**：`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="3e750-258">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="3e750-259">**环境变量**：`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="3e750-259">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="3e750-260">设置为服务器应响应的以分号分隔 (;) 的 URL 前缀列表。</span><span class="sxs-lookup"><span data-stu-id="3e750-260">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="3e750-261">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="3e750-261">For example, `http://localhost:123`.</span></span> <span data-ttu-id="3e750-262">使用“\*”指示服务器应针对请求侦听的使用特定端口和协议（例如 `http://*:5000`）的 IP 地址或主机名。</span><span class="sxs-lookup"><span data-stu-id="3e750-262">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="3e750-263">协议（`http://` 或 `https://`）必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="3e750-263">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="3e750-264">不同的服务器支持的格式有所不同。</span><span class="sxs-lookup"><span data-stu-id="3e750-264">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-265">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-265">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="3e750-266">Kestrel 具有自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="3e750-266">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="3e750-267">有关详细信息，请参阅 [ASP.NET Core 中的 Kestrel Web 服务器实现](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="3e750-267">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-268">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-268">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="3e750-269">关闭超时</span><span class="sxs-lookup"><span data-stu-id="3e750-269">Shutdown Timeout</span></span>

<span data-ttu-id="3e750-270">指定等待 Web 主机关闭的时长。</span><span class="sxs-lookup"><span data-stu-id="3e750-270">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="3e750-271">**键**：shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="3e750-271">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="3e750-272">**类型**：int</span><span class="sxs-lookup"><span data-stu-id="3e750-272">**Type**: *int*</span></span>  
<span data-ttu-id="3e750-273">**默认值**：5</span><span class="sxs-lookup"><span data-stu-id="3e750-273">**Default**: 5</span></span>  
<span data-ttu-id="3e750-274">**设置使用**：`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="3e750-274">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="3e750-275">**环境变量**：`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="3e750-275">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="3e750-276">虽然键使用 `UseSetting` 接受 int（例如 `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`），但是 `UseShutdownTimeout` 扩展方法采用 `TimeSpan`。</span><span class="sxs-lookup"><span data-stu-id="3e750-276">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the `UseShutdownTimeout` extension method takes a `TimeSpan`.</span></span> <span data-ttu-id="3e750-277">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="3e750-277">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-278">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-278">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-279">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-279">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-280">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="3e750-280">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="3e750-281">启动程序集</span><span class="sxs-lookup"><span data-stu-id="3e750-281">Startup Assembly</span></span>

<span data-ttu-id="3e750-282">确定要在其中搜索 `Startup` 类的程序集。</span><span class="sxs-lookup"><span data-stu-id="3e750-282">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="3e750-283">**键**：startupAssembly</span><span class="sxs-lookup"><span data-stu-id="3e750-283">**Key**: startupAssembly</span></span>  
<span data-ttu-id="3e750-284">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-284">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-285">**默认值**：应用的程序集</span><span class="sxs-lookup"><span data-stu-id="3e750-285">**Default**: The app's assembly</span></span>  
<span data-ttu-id="3e750-286">**设置使用**：`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="3e750-286">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="3e750-287">**环境变量**：`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="3e750-287">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="3e750-288">按名称（`string`）或类型（`TStartup`）的程序集可以引用。</span><span class="sxs-lookup"><span data-stu-id="3e750-288">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="3e750-289">如果调用多个 `UseStartup` 方法，优先选择最后一个方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-289">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-290">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-290">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-291">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-291">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

### <a name="web-root"></a><span data-ttu-id="3e750-292">Web 根路径</span><span class="sxs-lookup"><span data-stu-id="3e750-292">Web Root</span></span>

<span data-ttu-id="3e750-293">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="3e750-293">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="3e750-294">**键**：webroot</span><span class="sxs-lookup"><span data-stu-id="3e750-294">**Key**: webroot</span></span>  
<span data-ttu-id="3e750-295">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="3e750-295">**Type**: *string*</span></span>  
<span data-ttu-id="3e750-296">**默认值**：如果未指定，默认值是“(Content Root)/wwwroot”（如果该路径存在）。</span><span class="sxs-lookup"><span data-stu-id="3e750-296">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="3e750-297">如果该路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="3e750-297">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="3e750-298">**设置使用**：`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="3e750-298">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="3e750-299">**环境变量**：`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="3e750-299">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-300">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-300">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="3e750-302">替代配置</span><span class="sxs-lookup"><span data-stu-id="3e750-302">Overriding configuration</span></span>

<span data-ttu-id="3e750-303">使用[配置](xref:fundamentals/configuration/index)以配置主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-303">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="3e750-304">在以下示例中，在 hosting.json 文件中指定主机配置（可选）。</span><span class="sxs-lookup"><span data-stu-id="3e750-304">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="3e750-305">从 hosting.json 文件加载的任何配置可能会由命令行参数替代。</span><span class="sxs-lookup"><span data-stu-id="3e750-305">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="3e750-306">生成的配置（在 `config` 中）用于通过 `UseConfiguration` 配置主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-306">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-307">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-307">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3e750-308">hosting.json：</span><span class="sxs-lookup"><span data-stu-id="3e750-308">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="3e750-309">首先用 hosting.json 配置替代 `UseUrls` 提供的配置，然后是命令行参数配置：</span><span class="sxs-lookup"><span data-stu-id="3e750-309">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-310">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-310">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-311">hosting.json：</span><span class="sxs-lookup"><span data-stu-id="3e750-311">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="3e750-312">首先用 hosting.json 配置替代 `UseUrls` 提供的配置，然后是命令行参数配置：</span><span class="sxs-lookup"><span data-stu-id="3e750-312">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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
> <span data-ttu-id="3e750-313">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 扩展方法当前不能分析由 `GetSection` 返回的配置部分（例如 `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="3e750-313">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="3e750-314">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:urls`、`section:environment`）。</span><span class="sxs-lookup"><span data-stu-id="3e750-314">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="3e750-315">`UseConfiguration` 方法需要键来匹配 `WebHostBuilder` 键（例如 `urls`、`environment`）。</span><span class="sxs-lookup"><span data-stu-id="3e750-315">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="3e750-316">键上存在的节名称阻止节的值配置主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-316">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="3e750-317">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="3e750-317">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="3e750-318">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="3e750-318">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="3e750-319">若要指定在特定的 URL 上运行的主机，所需的值可以在执行 `dotnet run` 时从命令提示符传入。</span><span class="sxs-lookup"><span data-stu-id="3e750-319">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing `dotnet run`.</span></span> <span data-ttu-id="3e750-320">命令行参数替代 hosting.json 文件中的 `urls` 值，且服务器侦听端口 8080：</span><span class="sxs-lookup"><span data-stu-id="3e750-320">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="3e750-321">启动主机</span><span class="sxs-lookup"><span data-stu-id="3e750-321">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3e750-322">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3e750-322">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3e750-323">**运行**</span><span class="sxs-lookup"><span data-stu-id="3e750-323">**Run**</span></span>

<span data-ttu-id="3e750-324">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="3e750-324">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="3e750-325">**Start**</span><span class="sxs-lookup"><span data-stu-id="3e750-325">**Start**</span></span>

<span data-ttu-id="3e750-326">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="3e750-326">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="3e750-327">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="3e750-327">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="3e750-328">应用可以使用通过静态便捷方法预配置的 `CreateDefaultBuilder` 默认值初始化并启动新的主机。</span><span class="sxs-lookup"><span data-stu-id="3e750-328">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="3e750-329">这些方法在没有控制台输出的情况下启动服务器，并使用 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) 等待中断（Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="3e750-329">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="3e750-330">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="3e750-330">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="3e750-331">从 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="3e750-331">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="3e750-332">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="3e750-332">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="3e750-333">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="3e750-333">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="3e750-334">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="3e750-334">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="3e750-335">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="3e750-335">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="3e750-336">从 URL 和 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="3e750-336">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="3e750-337">生成与 Start(RequestDelegate app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="3e750-337">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="3e750-338">**Start(Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="3e750-338">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="3e750-339">使用 `IRouteBuilder` 的实例 ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由中间件：</span><span class="sxs-lookup"><span data-stu-id="3e750-339">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="3e750-340">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="3e750-340">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="3e750-341">请求</span><span class="sxs-lookup"><span data-stu-id="3e750-341">Request</span></span>                                    | <span data-ttu-id="3e750-342">响应</span><span class="sxs-lookup"><span data-stu-id="3e750-342">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="3e750-343">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="3e750-343">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="3e750-344">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="3e750-344">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="3e750-345">使用“ooops!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="3e750-345">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="3e750-346">使用“Uh oh!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="3e750-346">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="3e750-347">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="3e750-347">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="3e750-348">Hello World!</span><span class="sxs-lookup"><span data-stu-id="3e750-348">Hello World!</span></span>                             |

<span data-ttu-id="3e750-349">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="3e750-349">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="3e750-350">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="3e750-350">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="3e750-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="3e750-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="3e750-352">使用 URL 和 `IRouteBuilder` 实例：</span><span class="sxs-lookup"><span data-stu-id="3e750-352">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="3e750-353">生成与 Start(Action<IRouteBuilder> routeBuilder) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="3e750-353">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="3e750-354">**StartWith(Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="3e750-354">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="3e750-355">提供委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="3e750-355">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="3e750-356">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="3e750-356">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="3e750-357">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="3e750-357">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="3e750-358">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="3e750-358">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="3e750-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="3e750-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="3e750-360">提供 URL 和委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="3e750-360">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="3e750-361">生成与 StartWith(Action<IApplicationBuilder> app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="3e750-361">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3e750-362">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3e750-362">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3e750-363">**运行**</span><span class="sxs-lookup"><span data-stu-id="3e750-363">**Run**</span></span>

<span data-ttu-id="3e750-364">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="3e750-364">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="3e750-365">**Start**</span><span class="sxs-lookup"><span data-stu-id="3e750-365">**Start**</span></span>

<span data-ttu-id="3e750-366">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="3e750-366">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="3e750-367">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="3e750-367">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


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

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="3e750-368">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="3e750-368">IHostingEnvironment interface</span></span>

<span data-ttu-id="3e750-369">[IHostingEnvironment 接口](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用的 Web 承载环境的信息。</span><span class="sxs-lookup"><span data-stu-id="3e750-369">The [IHostingEnvironment interface](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="3e750-370">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="3e750-370">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="3e750-371">[基于约定的方法](xref:fundamentals/environments#startup-conventions)可以用于在启动时基于环境配置应用。</span><span class="sxs-lookup"><span data-stu-id="3e750-371">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="3e750-372">或者，将 `IHostingEnvironment` 注入到 `Startup` 构造函数用于 `ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="3e750-372">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="3e750-373">除了 `IsDevelopment` 扩展方法，`IHostingEnvironment` 提供 `IsStaging`、`IsProduction` 和 `IsEnvironment(string environmentName)` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-373">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="3e750-374">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="3e750-374">See [Working with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="3e750-375">`IHostingEnvironment` 服务还可以直接注入到 `Configure` 方法以设置处理管道：</span><span class="sxs-lookup"><span data-stu-id="3e750-375">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="3e750-376">创建自定义[中间件](xref:fundamentals/middleware/index#writing-middleware)时可以将 `IHostingEnvironment` 注入 `Invoke` 方法：</span><span class="sxs-lookup"><span data-stu-id="3e750-376">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="3e750-377">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="3e750-377">IApplicationLifetime interface</span></span>

<span data-ttu-id="3e750-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) 允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="3e750-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="3e750-379">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="3e750-379">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span> <span data-ttu-id="3e750-380">此外，还有 `StopApplication` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e750-380">There's also a `StopApplication` method.</span></span>

| <span data-ttu-id="3e750-381">取消标记</span><span class="sxs-lookup"><span data-stu-id="3e750-381">Cancellation Token</span></span>    | <span data-ttu-id="3e750-382">触发条件</span><span class="sxs-lookup"><span data-stu-id="3e750-382">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="3e750-383">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="3e750-383">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="3e750-384">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="3e750-384">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="3e750-385">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="3e750-385">Requests may still be processing.</span></span> <span data-ttu-id="3e750-386">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="3e750-386">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="3e750-387">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="3e750-387">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="3e750-388">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="3e750-388">All requests should be processed.</span></span> <span data-ttu-id="3e750-389">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="3e750-389">Shutdown blocks until this event completes.</span></span> |

| <span data-ttu-id="3e750-390">方法</span><span class="sxs-lookup"><span data-stu-id="3e750-390">Method</span></span>            | <span data-ttu-id="3e750-391">操作</span><span class="sxs-lookup"><span data-stu-id="3e750-391">Action</span></span>                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | <span data-ttu-id="3e750-392">当前应用程序请求终止。</span><span class="sxs-lookup"><span data-stu-id="3e750-392">Requests termination of the current application.</span></span> |

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

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="3e750-393">疑难解答：System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="3e750-393">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="3e750-394">**仅适用于 ASP.NET Core 2.0**</span><span class="sxs-lookup"><span data-stu-id="3e750-394">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="3e750-395">主机可能通过将 `IStartup` 直接注入依赖关系注入容器生成，而不是调用 `UseStartup` 或 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="3e750-395">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="3e750-396">如果主机以这种方式生成，可能会发生以下错误：</span><span class="sxs-lookup"><span data-stu-id="3e750-396">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="3e750-397">这是因为 [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)（当前程序集）需扫描 `HostingStartupAttributes`。</span><span class="sxs-lookup"><span data-stu-id="3e750-397">This occurs because the [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="3e750-398">如果应用手动将 `IStartup` 注入到依赖关系注入容器中，将以下调用添加到具有指定程序集名称的 `WebHostBuilder`：</span><span class="sxs-lookup"><span data-stu-id="3e750-398">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="3e750-399">或者，将虚拟 `Configure` 添加到自动设置 `applicationName` (`ApplicationKey`) 的 `WebHostBuilder` 中：</span><span class="sxs-lookup"><span data-stu-id="3e750-399">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="3e750-400">**注意**：仅当使用 ASP.NET Core 2.0 发行版且应用不调用 `UseStartup` 或 `Configure` 时，需要执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3e750-400">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="3e750-401">有关详细信息，请参阅[公告：已删除 Microsoft.Extensions.PlatformAbstractions（注释）](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938)和 [StartupInjection 示例](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)。</span><span class="sxs-lookup"><span data-stu-id="3e750-401">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e750-402">其他资源</span><span class="sxs-lookup"><span data-stu-id="3e750-402">Additional resources</span></span>

* [<span data-ttu-id="3e750-403">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="3e750-403">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="3e750-404">在 Linux 上使用 Nginx 进行托管</span><span class="sxs-lookup"><span data-stu-id="3e750-404">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="3e750-405">在 Linux 上使用 Apache 进行托管</span><span class="sxs-lookup"><span data-stu-id="3e750-405">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="3e750-406">在 Windows 服务中进行托管</span><span class="sxs-lookup"><span data-stu-id="3e750-406">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
