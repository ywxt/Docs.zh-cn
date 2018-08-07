---
title: ASP.NET Core Web 主机
author: guardrex
description: 了解有关 ASP.NET Core 中负责应用启动和生存期管理的 Web 主机。
ms.author: riande
ms.custom: mvc
ms.date: 06/19/2018
uid: fundamentals/host/web-host
ms.openlocfilehash: 476795645b0430962b61f7a61de29d5d1819602b
ms.sourcegitcommit: d99a8554c91f626cf5e466911cf504dcbff0e02e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39356709"
---
# <a name="aspnet-core-web-host"></a><span data-ttu-id="495e0-103">ASP.NET Core Web 主机</span><span class="sxs-lookup"><span data-stu-id="495e0-103">ASP.NET Core Web Host</span></span>

<span data-ttu-id="495e0-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="495e0-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="495e0-105">ASP.NET Core 应用配置和启动“主机”。</span><span class="sxs-lookup"><span data-stu-id="495e0-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="495e0-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="495e0-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="495e0-107">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="495e0-107">At a minimum, the host configures a server and a request processing pipeline.</span></span> <span data-ttu-id="495e0-108">本主题介绍 ASP.NET Core Web 主机 ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder))，它可用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="495e0-108">This topic covers the ASP.NET Core Web Host ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)), which is useful for hosting web apps.</span></span> <span data-ttu-id="495e0-109">有关 .NET 通用主机 ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)) 的介绍，请参阅 <xref:fundamentals/host/generic-host>。</span><span class="sxs-lookup"><span data-stu-id="495e0-109">For coverage of the .NET Generic Host ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)), see <xref:fundamentals/host/generic-host>.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="495e0-110">设置主机</span><span class="sxs-lookup"><span data-stu-id="495e0-110">Set up a host</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="495e0-111">创建使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-111">Create a host using an instance of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="495e0-112">通常在应用的入口点来执行 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-112">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="495e0-113">在项目模板中，`Main` 位于 Program.cs。</span><span class="sxs-lookup"><span data-stu-id="495e0-113">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="495e0-114">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="495e0-114">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>();
}
```

<span data-ttu-id="495e0-115">`CreateDefaultBuilder` 执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="495e0-115">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="495e0-116">使用应用的托管配置提供程序将 [Kestrel](xref:fundamentals/servers/kestrel) 配置为 Web 服务器并配置该服务器。</span><span class="sxs-lookup"><span data-stu-id="495e0-116">Configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and configures the server using the app's hosting configuration providers.</span></span> <span data-ttu-id="495e0-117">有关 Kestrel 默认选项，请参阅 <xref:fundamentals/servers/kestrel#kestrel-options>。</span><span class="sxs-lookup"><span data-stu-id="495e0-117">For the Kestrel default options, see <xref:fundamentals/servers/kestrel#kestrel-options>.</span></span>
* <span data-ttu-id="495e0-118">将内容根设置为由 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory) 返回的路径。</span><span class="sxs-lookup"><span data-stu-id="495e0-118">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="495e0-119">通过以下对象加载[主机配置](#host-configuration-values)：</span><span class="sxs-lookup"><span data-stu-id="495e0-119">Loads [host configuration](#host-configuration-values) from:</span></span>
  * <span data-ttu-id="495e0-120">前缀为 `ASPNETCORE_` 的环境变量（例如，`ASPNETCORE_ENVIRONMENT`）。</span><span class="sxs-lookup"><span data-stu-id="495e0-120">Environment variables prefixed with `ASPNETCORE_` (for example, `ASPNETCORE_ENVIRONMENT`).</span></span>
  * <span data-ttu-id="495e0-121">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="495e0-121">Command-line arguments.</span></span>
* <span data-ttu-id="495e0-122">通过以下对象加载应用配置：</span><span class="sxs-lookup"><span data-stu-id="495e0-122">Loads app configuration from:</span></span>
  * <span data-ttu-id="495e0-123">appsettings.json。</span><span class="sxs-lookup"><span data-stu-id="495e0-123">*appsettings.json*.</span></span>
  * <span data-ttu-id="495e0-124">appsettings.{Environment}.json。</span><span class="sxs-lookup"><span data-stu-id="495e0-124">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="495e0-125">应用在使用入口程序集的 `Development` 环境中运行时的[用户机密](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="495e0-125">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment using the entry assembly.</span></span>
  * <span data-ttu-id="495e0-126">环境变量。</span><span class="sxs-lookup"><span data-stu-id="495e0-126">Environment variables.</span></span>
  * <span data-ttu-id="495e0-127">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="495e0-127">Command-line arguments.</span></span>
* <span data-ttu-id="495e0-128">配置控制台和调试输出的[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="495e0-128">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="495e0-129">日志记录包含 appsettings.json 或 appsettings.{Environment}.json 文件的日志记录配置部分中指定的[日志筛选](xref:fundamentals/logging/index#log-filtering)规则。</span><span class="sxs-lookup"><span data-stu-id="495e0-129">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="495e0-130">在 IIS 后方运行时，启用 [IIS 集成](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="495e0-130">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="495e0-131">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)时配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="495e0-131">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="495e0-132">该模块创建 IIS 与 Kestrel 之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="495e0-132">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="495e0-133">还配置应用到[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="495e0-133">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="495e0-134">有关 IIS 默认选项，请参阅 <xref:host-and-deploy/iis/index#iis-options>。</span><span class="sxs-lookup"><span data-stu-id="495e0-134">For the IIS default options, see <xref:host-and-deploy/iis/index#iis-options>.</span></span>
* <span data-ttu-id="495e0-135">如果应用环境为“开发”，请将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="495e0-135">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="495e0-136">有关详细信息，请参阅[作用域验证](#scope-validation)。</span><span class="sxs-lookup"><span data-stu-id="495e0-136">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="495e0-137">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration)、[ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging) 以及 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 的其他方法和扩展方法可重写和增强 `CreateDefaultBuilder` 定义的配置。</span><span class="sxs-lookup"><span data-stu-id="495e0-137">The configuration defined by `CreateDefaultBuilder` can be overridden and augmented by [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging), and other methods and extension methods of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="495e0-138">下面是一些示例：</span><span class="sxs-lookup"><span data-stu-id="495e0-138">A few examples follow:</span></span>

* <span data-ttu-id="495e0-139">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) 用于指定应用的其他 `IConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="495e0-139">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) is used to specify additional `IConfiguration` for the app.</span></span> <span data-ttu-id="495e0-140">下面的 `ConfigureAppConfiguration` 调用添加委托，以在 appsettings.xml 文件中添加应用配置。</span><span class="sxs-lookup"><span data-stu-id="495e0-140">The following `ConfigureAppConfiguration` call adds a delegate to include app configuration in the *appsettings.xml* file.</span></span> <span data-ttu-id="495e0-141">可多次调用 `ConfigureAppConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="495e0-141">`ConfigureAppConfiguration` may be called multiple times.</span></span> <span data-ttu-id="495e0-142">请注意，此配置不适用于主机（例如，服务器 URL 或环境）。</span><span class="sxs-lookup"><span data-stu-id="495e0-142">Note that this configuration doesn't apply to the host (for example, server URLs or environment).</span></span> <span data-ttu-id="495e0-143">请参阅[主机配置值](#host-configuration-values)部分。</span><span class="sxs-lookup"><span data-stu-id="495e0-143">See the [Host configuration values](#host-configuration-values) section.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((hostingContext, config) =>
        {
            config.AddXmlFile("appsettings.xml", optional: true, reloadOnChange: true);
        })
        ...
    ```

* <span data-ttu-id="495e0-144">下面的 `ConfigureLogging` 调用添加委托，以将最小日志记录级别 ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) 配置为 [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel)。</span><span class="sxs-lookup"><span data-stu-id="495e0-144">The following `ConfigureLogging` call adds a delegate to configure the minimum logging level ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) to [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="495e0-145">此设置重写 `CreateDefaultBuilder` 在 appsettings.Development.json 和 appsettings.Production.json 中配置的设置，分别为 `LogLevel.Debug` 和 `LogLevel.Error`。</span><span class="sxs-lookup"><span data-stu-id="495e0-145">This setting overrides the settings in *appsettings.Development.json* (`LogLevel.Debug`) and *appsettings.Production.json* (`LogLevel.Error`) configured by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="495e0-146">可多次调用 `ConfigureLogging`。</span><span class="sxs-lookup"><span data-stu-id="495e0-146">`ConfigureLogging` may be called multiple times.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureLogging(logging => 
        {
            logging.SetMinimumLevel(LogLevel.Warning);
        })
        ...
    ```

* <span data-ttu-id="495e0-147">下面调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 来重写 `CreateDefaultBuilder` 在配置 Kestrel 时建立的 30,000,000 字节默认 [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)：</span><span class="sxs-lookup"><span data-stu-id="495e0-147">The following call to [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .UseKestrel(options =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
        ...
    ```

<span data-ttu-id="495e0-148">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="495e0-148">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="495e0-149">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="495e0-149">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="495e0-150">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="495e0-150">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="495e0-151">有关应用配置的详细信息，请参阅 <xref:fundamentals/configuration/index>。</span><span class="sxs-lookup"><span data-stu-id="495e0-151">For more information on app configuration, see <xref:fundamentals/configuration/index>.</span></span>

> [!NOTE]
> <span data-ttu-id="495e0-152">作为使用静态 `CreateDefaultBuilder` 方法的替代方法，从 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 创建主机是一种受 ASP.NET Core 2.x 支持的方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-152">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="495e0-153">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="495e0-153">For more information, see the ASP.NET Core 1.x tab.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="495e0-154">创建使用 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-154">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="495e0-155">通常执行 `Main` 方法，在应用的入口点来创建主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-155">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="495e0-156">在项目模板中，`Main` 位于 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="495e0-156">In the project templates, `Main` is located in *Program.cs*:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .UseStartup<Startup>()
            .Build();
}
```

<span data-ttu-id="495e0-157">`WebHostBuilder` 需要[实现 IServer 的服务器](xref:fundamentals/servers/index)。</span><span class="sxs-lookup"><span data-stu-id="495e0-157">`WebHostBuilder` requires a [server that implements IServer](xref:fundamentals/servers/index).</span></span> <span data-ttu-id="495e0-158">内置服务器是 [Kestrel](xref:fundamentals/servers/kestrel) 和 [HTTP.sys](xref:fundamentals/servers/httpsys)（在 ASP.NET Core 2.0 之前的版本中，HTTP.sys 叫做 [WebListener](xref:fundamentals/servers/weblistener)）。</span><span class="sxs-lookup"><span data-stu-id="495e0-158">The built-in servers are [Kestrel](xref:fundamentals/servers/kestrel) and [HTTP.sys](xref:fundamentals/servers/httpsys) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="495e0-159">在此示例中，[UseKestrel 扩展方法](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1)指定 Kestrel 服务器。</span><span class="sxs-lookup"><span data-stu-id="495e0-159">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="495e0-160">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="495e0-160">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="495e0-161">默认内容根通过 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1) 为 `UseContentRoot` 获得。</span><span class="sxs-lookup"><span data-stu-id="495e0-161">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="495e0-162">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="495e0-162">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="495e0-163">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="495e0-163">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="495e0-164">若要使用 IIS 作为反向代理，调用 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) 作为生成主机的一部分。</span><span class="sxs-lookup"><span data-stu-id="495e0-164">To use IIS as a reverse proxy, call [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="495e0-165">`UseIISIntegration` 不配置服务器，而 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 要配置。</span><span class="sxs-lookup"><span data-stu-id="495e0-165">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="495e0-166">当使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)创建 Kestrel 和 IIS 之间的反向代理时，`UseIISIntegration` 配置基路径和被服务器侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="495e0-166">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="495e0-167">要在 ASP.NET Core 中使用 IIS，必须指定 `UseKestrel` 和 `UseIISIntegration`。</span><span class="sxs-lookup"><span data-stu-id="495e0-167">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="495e0-168">`UseIISIntegration` 仅在 IIS 或 IIS Express 后方运行时激活。</span><span class="sxs-lookup"><span data-stu-id="495e0-168">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="495e0-169">有关详细信息，请参阅 <xref:fundamentals/servers/aspnet-core-module> 和 <xref:host-and-deploy/aspnet-core-module>。</span><span class="sxs-lookup"><span data-stu-id="495e0-169">For more information, see <xref:fundamentals/servers/aspnet-core-module> and <xref:host-and-deploy/aspnet-core-module>.</span></span>

<span data-ttu-id="495e0-170">配置主机 （和 ASP.NET Core 应用） 的最小实现包括指定服务器和应用的请求管道的配置项：</span><span class="sxs-lookup"><span data-stu-id="495e0-170">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

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

::: moniker-end

<span data-ttu-id="495e0-171">设置主机时，可以提供[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-171">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="495e0-172">如果指定 `Startup` 类，必须定义 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-172">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="495e0-173">有关更多信息，请参见<xref:fundamentals/startup>。</span><span class="sxs-lookup"><span data-stu-id="495e0-173">For more information, see <xref:fundamentals/startup>.</span></span> <span data-ttu-id="495e0-174">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="495e0-174">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="495e0-175">多次调用 `WebHostBuilder` 上的 `Configure` 或 `UseStartup` 将替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="495e0-175">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="495e0-176">主机配置值</span><span class="sxs-lookup"><span data-stu-id="495e0-176">Host configuration values</span></span>

<span data-ttu-id="495e0-177">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 依赖于以下的方法设置主机配置值：</span><span class="sxs-lookup"><span data-stu-id="495e0-177">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="495e0-178">主机生成器配置，其中包括格式 `ASPNETCORE_{configurationKey}` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="495e0-178">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="495e0-179">例如 `ASPNETCORE_ENVIRONMENT`。</span><span class="sxs-lookup"><span data-stu-id="495e0-179">For example, `ASPNETCORE_ENVIRONMENT`.</span></span>
* <span data-ttu-id="495e0-180">[UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) 和 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 等扩展（请参阅[重写配置](#override-configuration)部分）。</span><span class="sxs-lookup"><span data-stu-id="495e0-180">Extensions such as [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) and [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (see the [Override configuration](#override-configuration) section).</span></span>
* <span data-ttu-id="495e0-181">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 和关联键。</span><span class="sxs-lookup"><span data-stu-id="495e0-181">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="495e0-182">使用 `UseSetting` 设置值时，该值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="495e0-182">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="495e0-183">主机使用任何一个选项设置上一个值。</span><span class="sxs-lookup"><span data-stu-id="495e0-183">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="495e0-184">有关详细信息，请参阅下一部分中的[重写配置](#override-configuration)。</span><span class="sxs-lookup"><span data-stu-id="495e0-184">For more information, see [Override configuration](#override-configuration) in the next section.</span></span>

### <a name="application-key-name"></a><span data-ttu-id="495e0-185">应用程序键（名称）</span><span class="sxs-lookup"><span data-stu-id="495e0-185">Application Key (Name)</span></span>

<span data-ttu-id="495e0-186">在主机构造期间调用 [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) 或 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) 时，会自动设置 [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) 属性。</span><span class="sxs-lookup"><span data-stu-id="495e0-186">The [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) property is automatically set when [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) or [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) is called during host construction.</span></span> <span data-ttu-id="495e0-187">该值设置为包含应用入口点的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="495e0-187">The value is set to the name of the assembly containing the app's entry point.</span></span> <span data-ttu-id="495e0-188">要显式设置值，请使用 [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey)：</span><span class="sxs-lookup"><span data-stu-id="495e0-188">To set the value explicitly, use the [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey):</span></span>

<span data-ttu-id="495e0-189">**密钥**：applicationName</span><span class="sxs-lookup"><span data-stu-id="495e0-189">**Key**: applicationName</span></span>  
<span data-ttu-id="495e0-190">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-190">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-191">**默认**：包含应用入口点的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="495e0-191">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="495e0-192">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="495e0-192">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="495e0-193">**环境变量**：`ASPNETCORE_APPLICATIONKEY`</span><span class="sxs-lookup"><span data-stu-id="495e0-193">**Environment variable**: `ASPNETCORE_APPLICATIONKEY`</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.ApplicationKey, "CustomApplicationName")
```

::: moniker-end

::: moniker range="< aspnetcore-2.1"

```csharp
var host = new WebHostBuilder()
    .UseSetting("applicationName", "CustomApplicationName")
```

::: moniker-end

### <a name="capture-startup-errors"></a><span data-ttu-id="495e0-194">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="495e0-194">Capture Startup Errors</span></span>

<span data-ttu-id="495e0-195">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="495e0-195">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="495e0-196">**键**：captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="495e0-196">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="495e0-197">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="495e0-197">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="495e0-198">**默认值**：默认为 `false`，除非应用使用 Kestrel 在 IIS 后方运行，其中默认值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="495e0-198">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="495e0-199">**设置使用**：`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="495e0-199">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="495e0-200">**环境变量**：`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="495e0-200">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="495e0-201">当 `false` 时，启动期间出错导致主机退出。</span><span class="sxs-lookup"><span data-stu-id="495e0-201">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="495e0-202">当 `true` 时，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="495e0-202">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
```

::: moniker-end

### <a name="content-root"></a><span data-ttu-id="495e0-203">内容根</span><span class="sxs-lookup"><span data-stu-id="495e0-203">Content Root</span></span>

<span data-ttu-id="495e0-204">此设置确定 ASP.NET Core 开始搜索内容文件，如 MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="495e0-204">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="495e0-205">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="495e0-205">**Key**: contentRoot</span></span>  
<span data-ttu-id="495e0-206">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-206">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-207">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="495e0-207">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="495e0-208">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="495e0-208">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="495e0-209">**环境变量**：`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="495e0-209">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="495e0-210">内容根也用作 [Web 根设置](#web-root)的基路径。</span><span class="sxs-lookup"><span data-stu-id="495e0-210">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="495e0-211">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="495e0-211">If the path doesn't exist, the host fails to start.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\<content-root>")
```

::: moniker-end

### <a name="detailed-errors"></a><span data-ttu-id="495e0-212">详细错误</span><span class="sxs-lookup"><span data-stu-id="495e0-212">Detailed Errors</span></span>

<span data-ttu-id="495e0-213">确定是否应捕获详细错误。</span><span class="sxs-lookup"><span data-stu-id="495e0-213">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="495e0-214">**键**：detailedErrors</span><span class="sxs-lookup"><span data-stu-id="495e0-214">**Key**: detailedErrors</span></span>  
<span data-ttu-id="495e0-215">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="495e0-215">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="495e0-216">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="495e0-216">**Default**: false</span></span>  
<span data-ttu-id="495e0-217">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="495e0-217">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="495e0-218">**环境变量**：`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="495e0-218">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="495e0-219">启用（或当<a href="#environment">环境</a>设置为 `Development` ）时，应用捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="495e0-219">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

::: moniker-end

### <a name="environment"></a><span data-ttu-id="495e0-220">环境</span><span class="sxs-lookup"><span data-stu-id="495e0-220">Environment</span></span>

<span data-ttu-id="495e0-221">设置应用的环境。</span><span class="sxs-lookup"><span data-stu-id="495e0-221">Sets the app's environment.</span></span>

<span data-ttu-id="495e0-222">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="495e0-222">**Key**: environment</span></span>  
<span data-ttu-id="495e0-223">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-223">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-224">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="495e0-224">**Default**: Production</span></span>  
<span data-ttu-id="495e0-225">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="495e0-225">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="495e0-226">**环境变量**：`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="495e0-226">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="495e0-227">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="495e0-227">The environment can be set to any value.</span></span> <span data-ttu-id="495e0-228">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="495e0-228">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="495e0-229">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="495e0-229">Values aren't case sensitive.</span></span> <span data-ttu-id="495e0-230">默认情况下，从 `ASPNETCORE_ENVIRONMENT` 环境变量读取环境。</span><span class="sxs-lookup"><span data-stu-id="495e0-230">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="495e0-231">使用 [Visual Studio](https://www.visualstudio.com/) 时，可能会在 launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="495e0-231">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="495e0-232">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="495e0-232">For more information, see <xref:fundamentals/environments>.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseEnvironment(EnvironmentName.Development)
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="495e0-233">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="495e0-233">Hosting Startup Assemblies</span></span>

<span data-ttu-id="495e0-234">设置应用的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="495e0-234">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="495e0-235">**键**：hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="495e0-235">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="495e0-236">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-236">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-237">**默认值**：空字符串</span><span class="sxs-lookup"><span data-stu-id="495e0-237">**Default**: Empty string</span></span>  
<span data-ttu-id="495e0-238">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="495e0-238">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="495e0-239">**环境变量**：`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="495e0-239">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="495e0-240">承载启动程序集的以分号分隔的字符串在启动时加载。</span><span class="sxs-lookup"><span data-stu-id="495e0-240">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span>

<span data-ttu-id="495e0-241">虽然配置值默认为空字符串，但是承载启动程序集会始终包含应用的程序集。</span><span class="sxs-lookup"><span data-stu-id="495e0-241">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="495e0-242">提供承载启动程序集时，当应用在启动过程中生成其公用服务时将它们添加到应用的程序集加载。</span><span class="sxs-lookup"><span data-stu-id="495e0-242">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="https-port"></a><span data-ttu-id="495e0-243">HTTPS 端口</span><span class="sxs-lookup"><span data-stu-id="495e0-243">HTTPS Port</span></span>

<span data-ttu-id="495e0-244">设置 HTTPS 重定向端口。</span><span class="sxs-lookup"><span data-stu-id="495e0-244">Set the HTTPS redirect port.</span></span> <span data-ttu-id="495e0-245">用于[强制实施 HTTPS](xref:security/enforcing-ssl)。</span><span class="sxs-lookup"><span data-stu-id="495e0-245">Used in [enforcing HTTPS](xref:security/enforcing-ssl).</span></span>

<span data-ttu-id="495e0-246">键：https_port；类型：字符串；
默认值：未设置默认值。</span><span class="sxs-lookup"><span data-stu-id="495e0-246">**Key**: https_port **Type**: *string*
**Default**: A default value isn't set.</span></span>
<span data-ttu-id="495e0-247">使用的设置：`UseSetting`
环境变量：`ASPNETCORE_HTTPS_PORT`</span><span class="sxs-lookup"><span data-stu-id="495e0-247">**Set using**: `UseSetting`
**Environment variable**: `ASPNETCORE_HTTPS_PORT`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="prefer-hosting-urls"></a><span data-ttu-id="495e0-248">首选承载 URL</span><span class="sxs-lookup"><span data-stu-id="495e0-248">Prefer Hosting URLs</span></span>

<span data-ttu-id="495e0-249">指示主机是否应该侦听使用 `WebHostBuilder` 配置的 URL，而不是使用 `IServer` 实现配置的 URL。</span><span class="sxs-lookup"><span data-stu-id="495e0-249">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="495e0-250">**键**：preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="495e0-250">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="495e0-251">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="495e0-251">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="495e0-252">**默认值**：true</span><span class="sxs-lookup"><span data-stu-id="495e0-252">**Default**: true</span></span>  
<span data-ttu-id="495e0-253">**设置使用**：`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="495e0-253">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="495e0-254">**环境变量**：`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="495e0-254">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="prevent-hosting-startup"></a><span data-ttu-id="495e0-255">阻止承载启动</span><span class="sxs-lookup"><span data-stu-id="495e0-255">Prevent Hosting Startup</span></span>

<span data-ttu-id="495e0-256">阻止承载启动程序集自动加载，包括应用的程序集所配置的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="495e0-256">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="495e0-257">有关更多信息，请参见<xref:fundamentals/configuration/platform-specific-configuration>。</span><span class="sxs-lookup"><span data-stu-id="495e0-257">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

<span data-ttu-id="495e0-258">**键**：preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="495e0-258">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="495e0-259">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="495e0-259">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="495e0-260">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="495e0-260">**Default**: false</span></span>  
<span data-ttu-id="495e0-261">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="495e0-261">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="495e0-262">**环境变量**：`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="495e0-262">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

::: moniker-end

### <a name="server-urls"></a><span data-ttu-id="495e0-263">服务器 URL</span><span class="sxs-lookup"><span data-stu-id="495e0-263">Server URLs</span></span>

<span data-ttu-id="495e0-264">指示 IP 地址或主机地址，其中包含服务器应针对请求侦听的端口和协议。</span><span class="sxs-lookup"><span data-stu-id="495e0-264">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="495e0-265">**键**：urls</span><span class="sxs-lookup"><span data-stu-id="495e0-265">**Key**: urls</span></span>  
<span data-ttu-id="495e0-266">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-266">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-267">**默认**：http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="495e0-267">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="495e0-268">**设置使用**：`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="495e0-268">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="495e0-269">**环境变量**：`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="495e0-269">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="495e0-270">设置为服务器应响应的以分号分隔 (;) 的 URL 前缀列表。</span><span class="sxs-lookup"><span data-stu-id="495e0-270">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="495e0-271">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="495e0-271">For example, `http://localhost:123`.</span></span> <span data-ttu-id="495e0-272">使用“\*”指示服务器应针对请求侦听的使用特定端口和协议（例如 `http://*:5000`）的 IP 地址或主机名。</span><span class="sxs-lookup"><span data-stu-id="495e0-272">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="495e0-273">协议（`http://` 或 `https://`）必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="495e0-273">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="495e0-274">不同的服务器支持的格式有所不同。</span><span class="sxs-lookup"><span data-stu-id="495e0-274">Supported formats vary between servers.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

<span data-ttu-id="495e0-275">Kestrel 具有自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="495e0-275">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="495e0-276">有关更多信息，请参见<xref:fundamentals/servers/kestrel#endpoint-configuration>。</span><span class="sxs-lookup"><span data-stu-id="495e0-276">For more information, see <xref:fundamentals/servers/kestrel#endpoint-configuration>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="shutdown-timeout"></a><span data-ttu-id="495e0-277">关闭超时</span><span class="sxs-lookup"><span data-stu-id="495e0-277">Shutdown Timeout</span></span>

<span data-ttu-id="495e0-278">指定等待 Web 主机关闭的时长。</span><span class="sxs-lookup"><span data-stu-id="495e0-278">Specifies the amount of time to wait for the web host to shut down.</span></span>

<span data-ttu-id="495e0-279">**键**：shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="495e0-279">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="495e0-280">**类型**：int</span><span class="sxs-lookup"><span data-stu-id="495e0-280">**Type**: *int*</span></span>  
<span data-ttu-id="495e0-281">**默认值**：5</span><span class="sxs-lookup"><span data-stu-id="495e0-281">**Default**: 5</span></span>  
<span data-ttu-id="495e0-282">**设置使用**：`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="495e0-282">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="495e0-283">**环境变量**：`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="495e0-283">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="495e0-284">虽然键使用 `UseSetting` 接受 int（例如 `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`），但是 [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 扩展方法采用 [TimeSpan](/dotnet/api/system.timespan)。</span><span class="sxs-lookup"><span data-stu-id="495e0-284">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span>

<span data-ttu-id="495e0-285">在超时时间段中，托管：</span><span class="sxs-lookup"><span data-stu-id="495e0-285">During the timeout period, hosting:</span></span>

* <span data-ttu-id="495e0-286">触发器 [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)。</span><span class="sxs-lookup"><span data-stu-id="495e0-286">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="495e0-287">尝试停止托管服务，对服务停止失败的任何错误进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="495e0-287">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="495e0-288">如果在所有托管服务停止之前就达到了超时时间，则会在应用关闭时会终止剩余的所有活动的服务。</span><span class="sxs-lookup"><span data-stu-id="495e0-288">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="495e0-289">即使没有完成处理工作，服务也会停止。</span><span class="sxs-lookup"><span data-stu-id="495e0-289">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="495e0-290">如果停止服务需要额外的时间，请增加超时时间。</span><span class="sxs-lookup"><span data-stu-id="495e0-290">If services require additional time to stop, increase the timeout.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

::: moniker-end

### <a name="startup-assembly"></a><span data-ttu-id="495e0-291">启动程序集</span><span class="sxs-lookup"><span data-stu-id="495e0-291">Startup Assembly</span></span>

<span data-ttu-id="495e0-292">确定要在其中搜索 `Startup` 类的程序集。</span><span class="sxs-lookup"><span data-stu-id="495e0-292">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="495e0-293">**键**：startupAssembly</span><span class="sxs-lookup"><span data-stu-id="495e0-293">**Key**: startupAssembly</span></span>  
<span data-ttu-id="495e0-294">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-294">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-295">**默认值**：应用的程序集</span><span class="sxs-lookup"><span data-stu-id="495e0-295">**Default**: The app's assembly</span></span>  
<span data-ttu-id="495e0-296">**设置使用**：`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="495e0-296">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="495e0-297">**环境变量**：`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="495e0-297">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="495e0-298">按名称（`string`）或类型（`TStartup`）的程序集可以引用。</span><span class="sxs-lookup"><span data-stu-id="495e0-298">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="495e0-299">如果调用多个 `UseStartup` 方法，优先选择最后一个方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-299">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
```

::: moniker-end

### <a name="web-root"></a><span data-ttu-id="495e0-300">Web 根路径</span><span class="sxs-lookup"><span data-stu-id="495e0-300">Web Root</span></span>

<span data-ttu-id="495e0-301">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="495e0-301">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="495e0-302">**键**：webroot</span><span class="sxs-lookup"><span data-stu-id="495e0-302">**Key**: webroot</span></span>  
<span data-ttu-id="495e0-303">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="495e0-303">**Type**: *string*</span></span>  
<span data-ttu-id="495e0-304">**默认值**：如果未指定，默认值是“(Content Root)/wwwroot”（如果该路径存在）。</span><span class="sxs-lookup"><span data-stu-id="495e0-304">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="495e0-305">如果该路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="495e0-305">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="495e0-306">**设置使用**：`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="495e0-306">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="495e0-307">**环境变量**：`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="495e0-307">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
```

::: moniker-end

## <a name="override-configuration"></a><span data-ttu-id="495e0-308">重写配置</span><span class="sxs-lookup"><span data-stu-id="495e0-308">Override configuration</span></span>

<span data-ttu-id="495e0-309">[配置](xref:fundamentals/configuration/index)可用于配置 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-309">Use [Configuration](xref:fundamentals/configuration/index) to configure the web host.</span></span> <span data-ttu-id="495e0-310">在下面的示例中，主机配置是根据需要在 hostsettings.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="495e0-310">In the following example, host configuration is optionally specified in a *hostsettings.json* file.</span></span> <span data-ttu-id="495e0-311">命令行参数可能会重写从 hostsettings.json 文件加载的任何配置。</span><span class="sxs-lookup"><span data-stu-id="495e0-311">Any configuration loaded from the *hostsettings.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="495e0-312">生成的配置（在 `config` 中）用于通过 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 配置主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-312">The built configuration (in `config`) is used to configure the host with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration).</span></span> <span data-ttu-id="495e0-313">`IWebHostBuilder` 配置会添加到应用配置中，但反之不亦然&mdash;`ConfigureAppConfiguration` 不影响 `IWebHostBuilder` 配置。</span><span class="sxs-lookup"><span data-stu-id="495e0-313">`IWebHostBuilder` configuration is added to the app's configuration, but the converse isn't true&mdash;`ConfigureAppConfiguration` doesn't affect the `IWebHostBuilder` configuration.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="495e0-314">先用 hostsettings.json config 重写 `UseUrls` 提供的配置，再用命令行参数 config：</span><span class="sxs-lookup"><span data-stu-id="495e0-314">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hostsettings.json", optional: true)
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

<span data-ttu-id="495e0-315">hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="495e0-315">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="495e0-316">先用 hostsettings.json config 重写 `UseUrls` 提供的配置，再用命令行参数 config：</span><span class="sxs-lookup"><span data-stu-id="495e0-316">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hostsettings.json", optional: true)
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

<span data-ttu-id="495e0-317">hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="495e0-317">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

::: moniker-end

> [!NOTE]
> <span data-ttu-id="495e0-318">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 扩展方法当前不能分析由 `GetSection` 返回的配置部分（例如 `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="495e0-318">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="495e0-319">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:urls`、`section:environment`）。</span><span class="sxs-lookup"><span data-stu-id="495e0-319">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="495e0-320">`UseConfiguration` 方法需要键来匹配 `WebHostBuilder` 键（例如 `urls`、`environment`）。</span><span class="sxs-lookup"><span data-stu-id="495e0-320">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="495e0-321">键上存在的节名称阻止节的值配置主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-321">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="495e0-322">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="495e0-322">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="495e0-323">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="495e0-323">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>
>
> <span data-ttu-id="495e0-324">`UseConfiguration` 只将所提供的 `IConfiguration` 中的密钥复制到主机生成器配置中。</span><span class="sxs-lookup"><span data-stu-id="495e0-324">`UseConfiguration` only copies keys from the provided `IConfiguration` to the host builder configuration.</span></span> <span data-ttu-id="495e0-325">因此，JSON、INI 和 XML 设置文件的设置 `reloadOnChange: true` 没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="495e0-325">Therefore, setting `reloadOnChange: true` for JSON, INI, and XML settings files has no effect.</span></span>

<span data-ttu-id="495e0-326">若要指定在特定的 URL 上运行的主机，所需的值可以在执行 [dotnet 运行](/dotnet/core/tools/dotnet-run)时从命令提示符传入。</span><span class="sxs-lookup"><span data-stu-id="495e0-326">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="495e0-327">命令行参数重写 hostsettings.json 文件中的 `urls` 值，且服务器侦听端口 8080：</span><span class="sxs-lookup"><span data-stu-id="495e0-327">The command-line argument overrides the `urls` value from the *hostsettings.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a><span data-ttu-id="495e0-328">管理主机</span><span class="sxs-lookup"><span data-stu-id="495e0-328">Manage the host</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="495e0-329">**运行**</span><span class="sxs-lookup"><span data-stu-id="495e0-329">**Run**</span></span>

<span data-ttu-id="495e0-330">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="495e0-330">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="495e0-331">**Start**</span><span class="sxs-lookup"><span data-stu-id="495e0-331">**Start**</span></span>

<span data-ttu-id="495e0-332">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="495e0-332">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="495e0-333">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="495e0-333">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="495e0-334">应用可以使用通过静态便捷方法预配置的 `CreateDefaultBuilder` 默认值初始化并启动新的主机。</span><span class="sxs-lookup"><span data-stu-id="495e0-334">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="495e0-335">这些方法在没有控制台输出的情况下启动服务器，并使用 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) 等待中断（Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="495e0-335">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="495e0-336">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="495e0-336">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="495e0-337">从 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="495e0-337">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="495e0-338">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="495e0-338">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="495e0-339">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="495e0-339">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="495e0-340">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="495e0-340">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="495e0-341">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="495e0-341">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="495e0-342">从 URL 和 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="495e0-342">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="495e0-343">生成与 Start(RequestDelegate app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="495e0-343">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="495e0-344">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="495e0-344">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="495e0-345">使用 `IRouteBuilder` 的实例 ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由中间件：</span><span class="sxs-lookup"><span data-stu-id="495e0-345">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="495e0-346">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="495e0-346">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="495e0-347">请求</span><span class="sxs-lookup"><span data-stu-id="495e0-347">Request</span></span>                                    | <span data-ttu-id="495e0-348">响应</span><span class="sxs-lookup"><span data-stu-id="495e0-348">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="495e0-349">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="495e0-349">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="495e0-350">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="495e0-350">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="495e0-351">使用“ooops!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="495e0-351">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="495e0-352">使用“Uh oh!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="495e0-352">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="495e0-353">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="495e0-353">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="495e0-354">Hello World!</span><span class="sxs-lookup"><span data-stu-id="495e0-354">Hello World!</span></span>                             |

<span data-ttu-id="495e0-355">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="495e0-355">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="495e0-356">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="495e0-356">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="495e0-357">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="495e0-357">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="495e0-358">使用 URL 和 `IRouteBuilder` 实例：</span><span class="sxs-lookup"><span data-stu-id="495e0-358">Use a URL and an instance of `IRouteBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="495e0-359">生成与 Start(Action&lt;IRouteBuilder&gt; routeBuilder) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="495e0-359">Produces the same result as **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="495e0-360">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="495e0-360">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="495e0-361">提供委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="495e0-361">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="495e0-362">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="495e0-362">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="495e0-363">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="495e0-363">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="495e0-364">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="495e0-364">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="495e0-365">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="495e0-365">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="495e0-366">提供 URL 和委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="495e0-366">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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
    Console.WriteLine("Use Ctrl-C to shut down the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="495e0-367">生成与 StartWith(Action&lt;IApplicationBuilder&gt; app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="495e0-367">Produces the same result as **StartWith(Action&lt;IApplicationBuilder&gt; app)**, except the app responds on `http://localhost:8080`.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="495e0-368">**运行**</span><span class="sxs-lookup"><span data-stu-id="495e0-368">**Run**</span></span>

<span data-ttu-id="495e0-369">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="495e0-369">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="495e0-370">**Start**</span><span class="sxs-lookup"><span data-stu-id="495e0-370">**Start**</span></span>

<span data-ttu-id="495e0-371">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="495e0-371">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="495e0-372">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="495e0-372">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

::: moniker-end

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="495e0-373">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="495e0-373">IHostingEnvironment interface</span></span>

<span data-ttu-id="495e0-374">[IHostingEnvironment 接口](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用的 Web 承载环境的信息。</span><span class="sxs-lookup"><span data-stu-id="495e0-374">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="495e0-375">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="495e0-375">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="495e0-376">[基于约定的方法](xref:fundamentals/environments#environment-based-startup-class-and-methods)可以用于在启动时基于环境配置应用。</span><span class="sxs-lookup"><span data-stu-id="495e0-376">A [convention-based approach](xref:fundamentals/environments#environment-based-startup-class-and-methods) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="495e0-377">或者，将 `IHostingEnvironment` 注入到 `Startup` 构造函数用于 `ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="495e0-377">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="495e0-378">除了 `IsDevelopment` 扩展方法，`IHostingEnvironment` 提供 `IsStaging`、`IsProduction` 和 `IsEnvironment(string environmentName)` 方法。</span><span class="sxs-lookup"><span data-stu-id="495e0-378">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="495e0-379">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="495e0-379">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="495e0-380">`IHostingEnvironment` 服务还可以直接注入到 `Configure` 方法以设置处理管道：</span><span class="sxs-lookup"><span data-stu-id="495e0-380">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="495e0-381">创建自定义[中间件](xref:fundamentals/middleware/index#writing-middleware)时可以将 `IHostingEnvironment` 注入 `Invoke` 方法：</span><span class="sxs-lookup"><span data-stu-id="495e0-381">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#writing-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="495e0-382">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="495e0-382">IApplicationLifetime interface</span></span>

<span data-ttu-id="495e0-383">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) 允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="495e0-383">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="495e0-384">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="495e0-384">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="495e0-385">取消标记</span><span class="sxs-lookup"><span data-stu-id="495e0-385">Cancellation Token</span></span>    | <span data-ttu-id="495e0-386">触发条件</span><span class="sxs-lookup"><span data-stu-id="495e0-386">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| [<span data-ttu-id="495e0-387">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="495e0-387">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="495e0-388">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="495e0-388">The host has fully started.</span></span> |
| [<span data-ttu-id="495e0-389">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="495e0-389">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="495e0-390">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="495e0-390">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="495e0-391">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="495e0-391">All requests should be processed.</span></span> <span data-ttu-id="495e0-392">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="495e0-392">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="495e0-393">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="495e0-393">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="495e0-394">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="495e0-394">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="495e0-395">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="495e0-395">Requests may still be processing.</span></span> <span data-ttu-id="495e0-396">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="495e0-396">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="495e0-397">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) 请求应用终止。</span><span class="sxs-lookup"><span data-stu-id="495e0-397">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="495e0-398">以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：</span><span class="sxs-lookup"><span data-stu-id="495e0-398">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="scope-validation"></a><span data-ttu-id="495e0-399">作用域验证</span><span class="sxs-lookup"><span data-stu-id="495e0-399">Scope validation</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="495e0-400">如果应用环境为“开发”，则 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="495e0-400">[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

::: moniker-end

<span data-ttu-id="495e0-401">若将 `ValidateScopes` 设为 `true`，默认服务提供程序会执行检查来验证以下内容：</span><span class="sxs-lookup"><span data-stu-id="495e0-401">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="495e0-402">没有从根服务提供程序直接或间接解析到有作用域的服务。</span><span class="sxs-lookup"><span data-stu-id="495e0-402">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="495e0-403">未将有作用域的服务直接或间接注入到单一实例。</span><span class="sxs-lookup"><span data-stu-id="495e0-403">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="495e0-404">调用 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) 时，会创建根服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="495e0-404">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="495e0-405">在启动提供程序和应用时，根服务提供程序的生存期对应于应用/服务的生存期，并在关闭应用时释放。</span><span class="sxs-lookup"><span data-stu-id="495e0-405">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="495e0-406">有作用域的服务由创建它们的容器释放。</span><span class="sxs-lookup"><span data-stu-id="495e0-406">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="495e0-407">如果作用域创建于根容器，则该服务的生存会有效地提升至单一实例，因为根容器只会在应用/服务关闭时将其释放。</span><span class="sxs-lookup"><span data-stu-id="495e0-407">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="495e0-408">验证服务作用域，将在调用 `BuildServiceProvider` 时收集这类情况。</span><span class="sxs-lookup"><span data-stu-id="495e0-408">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="495e0-409">若要始终验证作用域（包括在生存环境中验证），请使用主机生成器上的 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) 配置 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)：</span><span class="sxs-lookup"><span data-stu-id="495e0-409">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

::: moniker range="= aspnetcore-2.0"

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="495e0-410">疑难解答：System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="495e0-410">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="495e0-411">**在应用不调用 `UseStartup` 或 `Configure` 时，以下项仅适用于 ASP.NET Core 2.0 应用。**</span><span class="sxs-lookup"><span data-stu-id="495e0-411">**The following only applies to ASP.NET Core 2.0 apps when the app doesn't call `UseStartup` or `Configure`.**</span></span>

<span data-ttu-id="495e0-412">主机可能通过将 `IStartup` 直接注入依赖关系注入容器生成，而不是调用 `UseStartup` 或 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="495e0-412">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="495e0-413">如果主机以这种方式生成，可能会发生以下错误：</span><span class="sxs-lookup"><span data-stu-id="495e0-413">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="495e0-414">这是因为应用名称（当前程序集的名称）需要扫描 `HostingStartupAttributes`。</span><span class="sxs-lookup"><span data-stu-id="495e0-414">This occurs because the app name (the name of the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="495e0-415">如果应用手动将 `IStartup` 注入到依赖关系注入容器中，将以下调用添加到具有指定程序集名称的 `WebHostBuilder`：</span><span class="sxs-lookup"><span data-stu-id="495e0-415">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "AssemblyName")
```

<span data-ttu-id="495e0-416">或者，将虚拟 `Configure` 添加到自动设置应用名称的 `WebHostBuilder` 中：</span><span class="sxs-lookup"><span data-stu-id="495e0-416">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the app name automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
```

<span data-ttu-id="495e0-417">有关详细信息，请参阅[公告：已删除 Microsoft.Extensions.PlatformAbstractions（注释）](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938)和 [StartupInjection 示例](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs)。</span><span class="sxs-lookup"><span data-stu-id="495e0-417">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="495e0-418">其他资源</span><span class="sxs-lookup"><span data-stu-id="495e0-418">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:host-and-deploy/windows-service>
