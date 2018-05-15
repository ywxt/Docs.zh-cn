---
title: ASP.NET Core 中的托管
author: guardrex
description: 了解有关 ASP.NET Core 中负责应用启动和生存期管理的 Web 主机。
manager: wpickett
ms.author: riande
ms.date: 09/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/hosting
ms.openlocfilehash: 344bf5f0917f4c33d67eeb14176ff2aae3ae75da
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="b8fe6-103">ASP.NET Core 中的托管</span><span class="sxs-lookup"><span data-stu-id="b8fe6-103">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="b8fe6-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b8fe6-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b8fe6-105">ASP.NET Core 应用配置和启动“主机”。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="b8fe6-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="b8fe6-107">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-107">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="b8fe6-108">设置主机</span><span class="sxs-lookup"><span data-stu-id="b8fe6-108">Setting up a host</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
<span data-ttu-id="b8fe6-110">创建使用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-110">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="b8fe6-111">通常在应用的入口点来执行 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-111">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="b8fe6-112">在项目模板中，`Main` 位于 Program.cs。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-112">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="b8fe6-113">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-113">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="b8fe6-114">`CreateDefaultBuilder` 执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-114">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="b8fe6-115">配置 [Kestrel](servers/kestrel.md) 为 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-115">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="b8fe6-116">有关 Kestrel 默认选项，请参阅[在 ASP.NET Core 中 Kestrel Web 服务器实现的 Kestrel 选项部分](xref:fundamentals/servers/kestrel#kestrel-options)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-116">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="b8fe6-117">将内容根设置为由 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory) 返回的路径。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-117">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="b8fe6-118">从下列选项中加载可选配置：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-118">Loads optional configuration from:</span></span>
  * <span data-ttu-id="b8fe6-119">appsettings.json。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-119">*appsettings.json*.</span></span>
  * <span data-ttu-id="b8fe6-120">appsettings.{Environment}.json。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-120">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="b8fe6-121">应用在 `Development` 环境中运行时的[用户机密](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-121">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="b8fe6-122">环境变量。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-122">Environment variables.</span></span>
  * <span data-ttu-id="b8fe6-123">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-123">Command-line arguments.</span></span>
* <span data-ttu-id="b8fe6-124">配置控制台和调试输出的[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-124">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="b8fe6-125">日志记录包含 appsettings.json 或 appsettings.{Environment}.json 文件的日志记录配置部分中指定的[日志筛选](xref:fundamentals/logging/index#log-filtering)规则。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-125">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="b8fe6-126">在 IIS 后方运行时，启用 [IIS 集成](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-126">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="b8fe6-127">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)时配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-127">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="b8fe6-128">该模块创建 IIS 与 Kestrel 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-128">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="b8fe6-129">还配置应用到[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-129">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="b8fe6-130">有关 IIS 默认选项，请参阅[使用 IIS 在 Windows 上托管 ASP.NET Core 的 IIS 选项部分](xref:host-and-deploy/iis/index#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-130">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>
* <span data-ttu-id="b8fe6-131">如果应用环境为“开发”，请将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-131">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="b8fe6-132">有关详细信息，请参阅[作用域验证](#scope-validation)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-132">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="b8fe6-133">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-133">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="b8fe6-134">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-134">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="b8fe6-135">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-135">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="b8fe6-136">有关应用配置的详细信息，请参阅 [ ASP.NET Core 中的配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-136">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="b8fe6-137">作为使用静态 `CreateDefaultBuilder` 方法的替代方法，从 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 创建主机是一种受 ASP.NET Core 2.x 支持的方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-137">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="b8fe6-138">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-138">For more information, see the ASP.NET Core 1.x tab.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-139">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-139">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
<span data-ttu-id="b8fe6-140">创建使用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-140">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="b8fe6-141">通常执行 `Main` 方法，在应用的入口点来创建主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-141">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="b8fe6-142">在项目模板中，`Main` 位于 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-142">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="b8fe6-143">`WebHostBuilder` 需要[实现 IServer 的服务器](servers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-143">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="b8fe6-144">内置服务器是 [Kestrel](servers/kestrel.md) 和 [HTTP.sys](servers/httpsys.md)（在 ASP.NET Core 2.0 之前的版本中，HTTP.sys 叫做 [WebListener](xref:fundamentals/servers/weblistener)）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-144">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="b8fe6-145">在此示例中，[UseKestrel 扩展方法](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)指定 Kestrel 服务器。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-145">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="b8fe6-146">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-146">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="b8fe6-147">默认内容根通过 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1) 为 `UseContentRoot` 获得。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-147">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="b8fe6-148">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-148">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="b8fe6-149">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-149">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="b8fe6-150">若要使用 IIS 作为反向代理，调用 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) 作为生成主机的一部分。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-150">To use IIS as a reverse proxy, call [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="b8fe6-151">`UseIISIntegration` 不配置服务器，而 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 要配置。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-151">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="b8fe6-152">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)创建 Kestrel 和 IIS 之间的反向代理时，`UseIISIntegration` 配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-152">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="b8fe6-153">要在 ASP.NET Core 中使用 IIS，必须指定 `UseKestrel` 和 `UseIISIntegration`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-153">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="b8fe6-154">`UseIISIntegration` 仅在 IIS 或 IIS Express 后方运行时激活。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-154">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="b8fe6-155">有关详细信息，请参阅 [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)和 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-155">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="b8fe6-156">配置主机 （和 ASP.NET Core 应用） 的最小实现包括指定服务器和应用的请求管道的配置项：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-156">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

* * *
<span data-ttu-id="b8fe6-157">设置主机时，可以提供[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-157">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="b8fe6-158">如果指定 `Startup` 类，必须定义 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-158">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="b8fe6-159">有关详细信息，请参阅 [ASP.NET Core 中的应用程序启动](startup.md)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-159">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="b8fe6-160">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-160">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="b8fe6-161">多次调用 `WebHostBuilder` 上的 `Configure` 或 `UseStartup` 将替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-161">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="b8fe6-162">主机配置值</span><span class="sxs-lookup"><span data-stu-id="b8fe6-162">Host configuration values</span></span>

<span data-ttu-id="b8fe6-163">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 依赖于以下的方法设置主机配置值：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-163">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="b8fe6-164">主机生成器配置，其中包括格式 `ASPNETCORE_{configurationKey}` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-164">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="b8fe6-165">例如 `ASPNETCORE_URLS`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-165">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="b8fe6-166">显式方法，如 `CaptureStartupErrors`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-166">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="b8fe6-167">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 和关联键。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-167">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="b8fe6-168">使用 `UseSetting` 设置值时，该值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-168">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="b8fe6-169">主机使用任何一个选项设置上一个值。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-169">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="b8fe6-170">有关详细信息，请参阅下一部分中的[重写配置](#overriding-configuration)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-170">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="b8fe6-171">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="b8fe6-171">Capture Startup Errors</span></span>

<span data-ttu-id="b8fe6-172">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-172">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="b8fe6-173">**键**：captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="b8fe6-173">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="b8fe6-174">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="b8fe6-174">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b8fe6-175">**默认值**：默认为 `false`，除非应用使用 Kestrel 在 IIS 后方运行，其中默认值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-175">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="b8fe6-176">**设置使用**：`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-176">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="b8fe6-177">**环境变量**：`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-177">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="b8fe6-178">当 `false` 时，启动期间出错导致主机退出。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-178">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="b8fe6-179">当 `true` 时，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-179">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-180">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-180">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-181">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-181">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="b8fe6-182">内容根</span><span class="sxs-lookup"><span data-stu-id="b8fe6-182">Content Root</span></span>

<span data-ttu-id="b8fe6-183">此设置确定 ASP.NET Core 开始搜索内容文件，如 MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-183">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="b8fe6-184">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="b8fe6-184">**Key**: contentRoot</span></span>  
<span data-ttu-id="b8fe6-185">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-185">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-186">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-186">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="b8fe6-187">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-187">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="b8fe6-188">**环境变量**：`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-188">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="b8fe6-189">内容根也用作 [Web 根设置](#web-root)的基路径。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-189">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="b8fe6-190">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-190">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-191">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-191">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-192">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-192">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="b8fe6-193">详细错误</span><span class="sxs-lookup"><span data-stu-id="b8fe6-193">Detailed Errors</span></span>

<span data-ttu-id="b8fe6-194">确定是否应捕获详细错误。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-194">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="b8fe6-195">**键**：detailedErrors</span><span class="sxs-lookup"><span data-stu-id="b8fe6-195">**Key**: detailedErrors</span></span>  
<span data-ttu-id="b8fe6-196">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="b8fe6-196">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b8fe6-197">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="b8fe6-197">**Default**: false</span></span>  
<span data-ttu-id="b8fe6-198">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-198">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b8fe6-199">**环境变量**：`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-199">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="b8fe6-200">启用（或当<a href="#environment">环境</a>设置为 `Development` ）时，应用捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-200">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-201">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-201">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-202">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-202">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="b8fe6-203">环境</span><span class="sxs-lookup"><span data-stu-id="b8fe6-203">Environment</span></span>

<span data-ttu-id="b8fe6-204">设置应用的环境。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-204">Sets the app's environment.</span></span>

<span data-ttu-id="b8fe6-205">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="b8fe6-205">**Key**: environment</span></span>  
<span data-ttu-id="b8fe6-206">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-206">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-207">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="b8fe6-207">**Default**: Production</span></span>  
<span data-ttu-id="b8fe6-208">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-208">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="b8fe6-209">**环境变量**：`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-209">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="b8fe6-210">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-210">The environment can be set to any value.</span></span> <span data-ttu-id="b8fe6-211">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-211">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="b8fe6-212">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-212">Values aren't case sensitive.</span></span> <span data-ttu-id="b8fe6-213">默认情况下，从 `ASPNETCORE_ENVIRONMENT` 环境变量读取环境。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-213">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="b8fe6-214">使用 [Visual Studio](https://www.visualstudio.com/) 时，可能会在 launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-214">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="b8fe6-215">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-215">For more information, see [Work with multiple environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-216">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-216">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-217">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-217">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="b8fe6-218">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="b8fe6-218">Hosting Startup Assemblies</span></span>

<span data-ttu-id="b8fe6-219">设置应用的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-219">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="b8fe6-220">**键**：hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="b8fe6-220">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="b8fe6-221">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-221">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-222">**默认值**：空字符串</span><span class="sxs-lookup"><span data-stu-id="b8fe6-222">**Default**: Empty string</span></span>  
<span data-ttu-id="b8fe6-223">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-223">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b8fe6-224">**环境变量**：`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-224">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="b8fe6-225">承载启动程序集的以分号分隔的字符串在启动时加载。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-225">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="b8fe6-226">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-226">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="b8fe6-227">虽然配置值默认为空字符串，但是承载启动程序集会始终包含应用的程序集。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-227">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="b8fe6-228">提供承载启动程序集时，当应用在启动过程中生成其公用服务时将它们添加到应用的程序集加载。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-228">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-229">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-229">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-230">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-230">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-231">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-231">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="b8fe6-232">首选承载 URL</span><span class="sxs-lookup"><span data-stu-id="b8fe6-232">Prefer Hosting URLs</span></span>

<span data-ttu-id="b8fe6-233">指示主机是否应该侦听使用 `WebHostBuilder` 配置的 URL，而不是使用 `IServer` 实现配置的 URL。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-233">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="b8fe6-234">**键**：preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="b8fe6-234">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="b8fe6-235">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="b8fe6-235">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b8fe6-236">**默认值**：true</span><span class="sxs-lookup"><span data-stu-id="b8fe6-236">**Default**: true</span></span>  
<span data-ttu-id="b8fe6-237">**设置使用**：`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-237">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="b8fe6-238">**环境变量**：`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-238">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="b8fe6-239">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-239">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-240">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-240">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-241">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-241">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-242">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-242">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="b8fe6-243">阻止承载启动</span><span class="sxs-lookup"><span data-stu-id="b8fe6-243">Prevent Hosting Startup</span></span>

<span data-ttu-id="b8fe6-244">阻止承载启动程序集自动加载，包括应用的程序集所配置的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-244">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="b8fe6-245">请参阅[使用特定于平台的配置添加应用功能](xref:host-and-deploy/platform-specific-configuration)，获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-245">See [Add app features using a platform-specific configuration](xref:host-and-deploy/platform-specific-configuration) for more information.</span></span>

<span data-ttu-id="b8fe6-246">**键**：preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="b8fe6-246">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="b8fe6-247">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="b8fe6-247">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="b8fe6-248">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="b8fe6-248">**Default**: false</span></span>  
<span data-ttu-id="b8fe6-249">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-249">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="b8fe6-250">**环境变量**：`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-250">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="b8fe6-251">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-251">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-252">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-252">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-253">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-253">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-254">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-254">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="b8fe6-255">服务器 URL</span><span class="sxs-lookup"><span data-stu-id="b8fe6-255">Server URLs</span></span>

<span data-ttu-id="b8fe6-256">指示 IP 地址或主机地址，其中包含服务器应针对请求侦听的端口和协议。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-256">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="b8fe6-257">**键**：urls</span><span class="sxs-lookup"><span data-stu-id="b8fe6-257">**Key**: urls</span></span>  
<span data-ttu-id="b8fe6-258">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-258">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-259">**默认**：http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="b8fe6-259">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="b8fe6-260">**设置使用**：`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-260">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="b8fe6-261">**环境变量**：`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-261">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="b8fe6-262">设置为服务器应响应的以分号分隔 (;) 的 URL 前缀列表。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-262">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="b8fe6-263">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-263">For example, `http://localhost:123`.</span></span> <span data-ttu-id="b8fe6-264">使用“\*”指示服务器应针对请求侦听的使用特定端口和协议（例如 `http://*:5000`）的 IP 地址或主机名。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-264">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="b8fe6-265">协议（`http://` 或 `https://`）必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-265">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="b8fe6-266">不同的服务器支持的格式有所不同。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-266">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-267">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-267">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="b8fe6-268">Kestrel 具有自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-268">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="b8fe6-269">有关详细信息，请参阅 [ASP.NET Core 中的 Kestrel Web 服务器实现](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-269">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-270">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-270">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="b8fe6-271">关闭超时</span><span class="sxs-lookup"><span data-stu-id="b8fe6-271">Shutdown Timeout</span></span>

<span data-ttu-id="b8fe6-272">指定等待 Web 主机关闭的时长。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-272">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="b8fe6-273">**键**：shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="b8fe6-273">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="b8fe6-274">**类型**：int</span><span class="sxs-lookup"><span data-stu-id="b8fe6-274">**Type**: *int*</span></span>  
<span data-ttu-id="b8fe6-275">**默认值**：5</span><span class="sxs-lookup"><span data-stu-id="b8fe6-275">**Default**: 5</span></span>  
<span data-ttu-id="b8fe6-276">**设置使用**：`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-276">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="b8fe6-277">**环境变量**：`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-277">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="b8fe6-278">虽然键使用 `UseSetting` 接受 int（例如 `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`），但是 [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 扩展方法采用 [TimeSpan](/dotnet/api/system.timespan)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-278">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span> <span data-ttu-id="b8fe6-279">此功能是 ASP.NET Core 2.0 中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-279">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="b8fe6-280">在超时时间段中，托管：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-280">During the timeout period, hosting:</span></span>

* <span data-ttu-id="b8fe6-281">触发器 [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-281">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="b8fe6-282">尝试停止托管服务，对服务停止失败的任何错误进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-282">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="b8fe6-283">如果在所有托管服务停止之前就达到了超时时间，则会在应用关闭时会终止剩余的所有活动的服务。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-283">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="b8fe6-284">即使没有完成处理工作，服务也会停止。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-284">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="b8fe6-285">如果停止服务需要额外的时间，请增加超时时间。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-285">If services require additional time to stop, increase the timeout.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-286">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-286">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-287">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-287">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-288">此功能在 ASP.NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-288">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="b8fe6-289">启动程序集</span><span class="sxs-lookup"><span data-stu-id="b8fe6-289">Startup Assembly</span></span>

<span data-ttu-id="b8fe6-290">确定要在其中搜索 `Startup` 类的程序集。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-290">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="b8fe6-291">**键**：startupAssembly</span><span class="sxs-lookup"><span data-stu-id="b8fe6-291">**Key**: startupAssembly</span></span>  
<span data-ttu-id="b8fe6-292">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-292">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-293">**默认值**：应用的程序集</span><span class="sxs-lookup"><span data-stu-id="b8fe6-293">**Default**: The app's assembly</span></span>  
<span data-ttu-id="b8fe6-294">**设置使用**：`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-294">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="b8fe6-295">**环境变量**：`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-295">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="b8fe6-296">按名称（`string`）或类型（`TStartup`）的程序集可以引用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-296">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="b8fe6-297">如果调用多个 `UseStartup` 方法，优先选择最后一个方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-297">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-298">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-298">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-299">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-299">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

### <a name="web-root"></a><span data-ttu-id="b8fe6-300">Web 根路径</span><span class="sxs-lookup"><span data-stu-id="b8fe6-300">Web Root</span></span>

<span data-ttu-id="b8fe6-301">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-301">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="b8fe6-302">**键**：webroot</span><span class="sxs-lookup"><span data-stu-id="b8fe6-302">**Key**: webroot</span></span>  
<span data-ttu-id="b8fe6-303">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b8fe6-303">**Type**: *string*</span></span>  
<span data-ttu-id="b8fe6-304">**默认值**：如果未指定，默认值是“(Content Root)/wwwroot”（如果该路径存在）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-304">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="b8fe6-305">如果该路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-305">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="b8fe6-306">**设置使用**：`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-306">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="b8fe6-307">**环境变量**：`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="b8fe6-307">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-308">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-308">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-309">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-309">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="b8fe6-310">替代配置</span><span class="sxs-lookup"><span data-stu-id="b8fe6-310">Overriding configuration</span></span>

<span data-ttu-id="b8fe6-311">使用[配置](xref:fundamentals/configuration/index)以配置主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-311">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="b8fe6-312">在以下示例中，在 hosting.json 文件中指定主机配置（可选）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-312">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="b8fe6-313">从 hosting.json 文件加载的任何配置可能会由命令行参数替代。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-313">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="b8fe6-314">生成的配置（在 `config` 中）用于通过 `UseConfiguration` 配置主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-314">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-315">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-315">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b8fe6-316">hosting.json：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-316">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="b8fe6-317">首先用 hosting.json 配置替代 `UseUrls` 提供的配置，然后是命令行参数配置：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-317">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-318">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-318">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-319">hosting.json：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-319">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="b8fe6-320">首先用 hosting.json 配置替代 `UseUrls` 提供的配置，然后是命令行参数配置：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-320">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

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
> <span data-ttu-id="b8fe6-321">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 扩展方法当前不能分析由 `GetSection` 返回的配置部分（例如 `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-321">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="b8fe6-322">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:urls`、`section:environment`）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-322">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="b8fe6-323">`UseConfiguration` 方法需要键来匹配 `WebHostBuilder` 键（例如 `urls`、`environment`）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-323">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="b8fe6-324">键上存在的节名称阻止节的值配置主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-324">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="b8fe6-325">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-325">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="b8fe6-326">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-326">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="b8fe6-327">若要指定在特定的 URL 上运行的主机，所需的值可以在执行 [dotnet 运行](/dotnet/core/tools/dotnet-run)时从命令提示符传入。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-327">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="b8fe6-328">命令行参数替代 hosting.json 文件中的 `urls` 值，且服务器侦听端口 8080：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-328">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="b8fe6-329">启动主机</span><span class="sxs-lookup"><span data-stu-id="b8fe6-329">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b8fe6-330">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-330">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b8fe6-331">**运行**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-331">**Run**</span></span>

<span data-ttu-id="b8fe6-332">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-332">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="b8fe6-333">**Start**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-333">**Start**</span></span>

<span data-ttu-id="b8fe6-334">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-334">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="b8fe6-335">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-335">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="b8fe6-336">应用可以使用通过静态便捷方法预配置的 `CreateDefaultBuilder` 默认值初始化并启动新的主机。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-336">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="b8fe6-337">这些方法在没有控制台输出的情况下启动服务器，并使用 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) 等待中断（Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-337">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="b8fe6-338">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-338">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="b8fe6-339">从 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-339">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="b8fe6-340">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="b8fe6-340">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="b8fe6-341">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-341">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b8fe6-342">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-342">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b8fe6-343">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-343">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="b8fe6-344">从 URL 和 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-344">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="b8fe6-345">生成与 Start(RequestDelegate app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-345">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="b8fe6-346">**Start(Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-346">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="b8fe6-347">使用 `IRouteBuilder` 的实例 ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由中间件：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-347">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="b8fe6-348">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-348">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="b8fe6-349">请求</span><span class="sxs-lookup"><span data-stu-id="b8fe6-349">Request</span></span>                                    | <span data-ttu-id="b8fe6-350">响应</span><span class="sxs-lookup"><span data-stu-id="b8fe6-350">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="b8fe6-351">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="b8fe6-351">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="b8fe6-352">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="b8fe6-352">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="b8fe6-353">使用“ooops!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="b8fe6-353">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="b8fe6-354">使用“Uh oh!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="b8fe6-354">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="b8fe6-355">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="b8fe6-355">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="b8fe6-356">Hello World!</span><span class="sxs-lookup"><span data-stu-id="b8fe6-356">Hello World!</span></span>                             |

<span data-ttu-id="b8fe6-357">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-357">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b8fe6-358">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-358">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b8fe6-359">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-359">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="b8fe6-360">使用 URL 和 `IRouteBuilder` 实例：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-360">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="b8fe6-361">生成与 Start(Action<IRouteBuilder> routeBuilder) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-361">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="b8fe6-362">**StartWith(Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-362">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="b8fe6-363">提供委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-363">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="b8fe6-364">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="b8fe6-364">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="b8fe6-365">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-365">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="b8fe6-366">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-366">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="b8fe6-367">**StartWith(string url, Action<IApplicationBuilder> app)**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-367">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="b8fe6-368">提供 URL 和委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-368">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="b8fe6-369">生成与 StartWith(Action<IApplicationBuilder> app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-369">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b8fe6-370">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b8fe6-370">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b8fe6-371">**运行**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-371">**Run**</span></span>

<span data-ttu-id="b8fe6-372">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-372">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="b8fe6-373">**Start**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-373">**Start**</span></span>

<span data-ttu-id="b8fe6-374">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-374">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="b8fe6-375">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-375">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


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

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="b8fe6-376">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="b8fe6-376">IHostingEnvironment interface</span></span>

<span data-ttu-id="b8fe6-377">[IHostingEnvironment 接口](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用的 Web 承载环境的信息。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-377">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="b8fe6-378">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-378">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="b8fe6-379">[基于约定的方法](xref:fundamentals/environments#startup-conventions)可以用于在启动时基于环境配置应用。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-379">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="b8fe6-380">或者，将 `IHostingEnvironment` 注入到 `Startup` 构造函数用于 `ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-380">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="b8fe6-381">除了 `IsDevelopment` 扩展方法，`IHostingEnvironment` 提供 `IsStaging`、`IsProduction` 和 `IsEnvironment(string environmentName)` 方法。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-381">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="b8fe6-382">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-382">See [Work with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="b8fe6-383">`IHostingEnvironment` 服务还可以直接注入到 `Configure` 方法以设置处理管道：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-383">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="b8fe6-384">创建自定义[中间件](xref:fundamentals/middleware/index#writing-middleware)时可以将 `IHostingEnvironment` 注入 `Invoke` 方法：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-384">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="b8fe6-385">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="b8fe6-385">IApplicationLifetime interface</span></span>

<span data-ttu-id="b8fe6-386">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) 允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-386">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="b8fe6-387">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-387">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="b8fe6-388">取消标记</span><span class="sxs-lookup"><span data-stu-id="b8fe6-388">Cancellation Token</span></span>    | <span data-ttu-id="b8fe6-389">触发条件</span><span class="sxs-lookup"><span data-stu-id="b8fe6-389">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="b8fe6-390">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-390">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="b8fe6-391">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-391">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="b8fe6-392">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-392">Requests may still be processing.</span></span> <span data-ttu-id="b8fe6-393">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-393">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="b8fe6-394">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-394">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="b8fe6-395">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-395">All requests should be processed.</span></span> <span data-ttu-id="b8fe6-396">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-396">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="b8fe6-397">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) 请求应用终止。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-397">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="b8fe6-398">以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-398">The following class uses `StopApplication` to gracefully shutdown an app when the class's `Shutdown` method is called:</span></span>

```csharp
public class MyClass
{
    private readonly IApplicationLifetime _appLifetime;

    public MyClass(IApplicationLifetime appLifetime)
    {
        _appLifetime = appLifetime;
    }

    public void Shutdown()
    {
        _appLifetime.StopApplication();
    }
}
```

## <a name="scope-validation"></a><span data-ttu-id="b8fe6-399">作用域验证</span><span class="sxs-lookup"><span data-stu-id="b8fe6-399">Scope validation</span></span>

<span data-ttu-id="b8fe6-400">在 ASP.NET Core 2.0 或更高版本中，如果应用环境为“开发”，则 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-400">In ASP.NET Core 2.0 or later, [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

<span data-ttu-id="b8fe6-401">若将 `ValidateScopes` 设为 `true`，默认服务提供程序会执行检查来验证以下内容：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-401">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="b8fe6-402">没有从根服务提供程序直接或间接解析到有作用域的服务。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-402">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="b8fe6-403">未将有作用域的服务直接或间接注入到单一实例。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-403">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="b8fe6-404">调用 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) 时，会创建根服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-404">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="b8fe6-405">在启动提供程序和应用时，根服务提供程序的生存期对应于应用/服务的生存期，并在关闭应用时释放。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-405">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="b8fe6-406">有作用域的服务由创建它们的容器释放。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-406">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="b8fe6-407">如果作用域创建于根容器，则该服务的生存会有效地提升至单一实例，因为根容器只会在应用/服务关闭时将其释放。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-407">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="b8fe6-408">验证服务作用域，将在调用 `BuildServiceProvider` 时收集这类情况。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-408">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="b8fe6-409">若要始终验证作用域（包括在生存环境中验证），请使用主机生成器上的 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) 配置 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-409">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="b8fe6-410">疑难解答：System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="b8fe6-410">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="b8fe6-411">**仅适用于 ASP.NET Core 2.0**</span><span class="sxs-lookup"><span data-stu-id="b8fe6-411">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="b8fe6-412">主机可能通过将 `IStartup` 直接注入依赖关系注入容器生成，而不是调用 `UseStartup` 或 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-412">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="b8fe6-413">如果主机以这种方式生成，可能会发生以下错误：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-413">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="b8fe6-414">这是因为 [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey)（当前程序集）需扫描 `HostingStartupAttributes`。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-414">This occurs because the [applicationName(ApplicationKey)](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="b8fe6-415">如果应用手动将 `IStartup` 注入到依赖关系注入容器中，将以下调用添加到具有指定程序集名称的 `WebHostBuilder`：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-415">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="b8fe6-416">或者，将虚拟 `Configure` 添加到自动设置 `applicationName` (`ApplicationKey`) 的 `WebHostBuilder` 中：</span><span class="sxs-lookup"><span data-stu-id="b8fe6-416">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="b8fe6-417">**注意**：仅当使用 ASP.NET Core 2.0 发行版且应用不调用 `UseStartup` 或 `Configure` 时，需要执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-417">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="b8fe6-418">有关详细信息，请参阅[公告：已删除 Microsoft.Extensions.PlatformAbstractions（注释）](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938)和 [StartupInjection 示例](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)。</span><span class="sxs-lookup"><span data-stu-id="b8fe6-418">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8fe6-419">其他资源</span><span class="sxs-lookup"><span data-stu-id="b8fe6-419">Additional resources</span></span>

* [<span data-ttu-id="b8fe6-420">使用 IIS 在 Windows 上进行托管</span><span class="sxs-lookup"><span data-stu-id="b8fe6-420">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="b8fe6-421">在 Linux 上使用 Nginx 进行托管</span><span class="sxs-lookup"><span data-stu-id="b8fe6-421">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="b8fe6-422">在 Linux 上使用 Apache 进行托管</span><span class="sxs-lookup"><span data-stu-id="b8fe6-422">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="b8fe6-423">在 Windows 服务中进行托管</span><span class="sxs-lookup"><span data-stu-id="b8fe6-423">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)
