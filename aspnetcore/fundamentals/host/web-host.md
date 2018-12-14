---
title: ASP.NET Core Web 主机
author: guardrex
description: 了解有关 ASP.NET Core 中负责应用启动和生存期管理的 Web 主机。
ms.author: riande
ms.custom: mvc
ms.date: 12/01/2018
uid: fundamentals/host/web-host
ms.openlocfilehash: bc77413127273aba207e68e7fbcb8ad916267e8e
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862273"
---
# <a name="aspnet-core-web-host"></a><span data-ttu-id="02237-103">ASP.NET Core Web 主机</span><span class="sxs-lookup"><span data-stu-id="02237-103">ASP.NET Core Web Host</span></span>

<span data-ttu-id="02237-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="02237-104">By [Luke Latham](https://github.com/guardrex)</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="02237-105">对于本主题的 1.1 版本，请下载 [ASP.NET Core Web 主机（版本 1.1，PDF）](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Web-Host_1.1.pdf)。</span><span class="sxs-lookup"><span data-stu-id="02237-105">For the 1.1 version of this topic, download [ASP.NET Core Web Host (version 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Web-Host_1.1.pdf).</span></span>

::: moniker-end

<span data-ttu-id="02237-106">ASP.NET Core 应用配置和启动“主机”。</span><span class="sxs-lookup"><span data-stu-id="02237-106">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="02237-107">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="02237-107">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="02237-108">至少，主机配置服务器和请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="02237-108">At a minimum, the host configures a server and a request processing pipeline.</span></span> <span data-ttu-id="02237-109">本主题介绍 ASP.NET Core Web 主机 ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder))，它可用于托管 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="02237-109">This topic covers the ASP.NET Core Web Host ([IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)), which is useful for hosting web apps.</span></span> <span data-ttu-id="02237-110">有关 .NET 通用主机 ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)) 的介绍，请参阅 <xref:fundamentals/host/generic-host>。</span><span class="sxs-lookup"><span data-stu-id="02237-110">For coverage of the .NET Generic Host ([IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder)), see <xref:fundamentals/host/generic-host>.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="02237-111">设置主机</span><span class="sxs-lookup"><span data-stu-id="02237-111">Set up a host</span></span>

<span data-ttu-id="02237-112">创建使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 实例的主机。</span><span class="sxs-lookup"><span data-stu-id="02237-112">Create a host using an instance of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="02237-113">通常在应用的入口点来执行 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="02237-113">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="02237-114">在项目模板中，`Main` 位于 Program.cs。</span><span class="sxs-lookup"><span data-stu-id="02237-114">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="02237-115">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机：</span><span class="sxs-lookup"><span data-stu-id="02237-115">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

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

<span data-ttu-id="02237-116">`CreateDefaultBuilder` 执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="02237-116">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="02237-117">使用应用的托管配置提供程序将 [Kestrel](xref:fundamentals/servers/kestrel) 服务器配置为 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="02237-117">Configures [Kestrel](xref:fundamentals/servers/kestrel) server as the web server using the app's hosting configuration providers.</span></span> <span data-ttu-id="02237-118">有关 Kestrel 服务器默认选项，请参阅 <xref:fundamentals/servers/kestrel#kestrel-options>。</span><span class="sxs-lookup"><span data-stu-id="02237-118">For the Kestrel server's default options, see <xref:fundamentals/servers/kestrel#kestrel-options>.</span></span>
* <span data-ttu-id="02237-119">将内容根设置为由 [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory) 返回的路径。</span><span class="sxs-lookup"><span data-stu-id="02237-119">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="02237-120">通过以下对象加载[主机配置](#host-configuration-values)：</span><span class="sxs-lookup"><span data-stu-id="02237-120">Loads [host configuration](#host-configuration-values) from:</span></span>
  * <span data-ttu-id="02237-121">前缀为 `ASPNETCORE_` 的环境变量（例如，`ASPNETCORE_ENVIRONMENT`）。</span><span class="sxs-lookup"><span data-stu-id="02237-121">Environment variables prefixed with `ASPNETCORE_` (for example, `ASPNETCORE_ENVIRONMENT`).</span></span>
  * <span data-ttu-id="02237-122">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="02237-122">Command-line arguments.</span></span>
* <span data-ttu-id="02237-123">按以下顺序加载应用配置：</span><span class="sxs-lookup"><span data-stu-id="02237-123">Loads app configuration in the following order from:</span></span>
  * <span data-ttu-id="02237-124">appsettings.json。</span><span class="sxs-lookup"><span data-stu-id="02237-124">*appsettings.json*.</span></span>
  * <span data-ttu-id="02237-125">appsettings.{Environment}.json。</span><span class="sxs-lookup"><span data-stu-id="02237-125">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="02237-126">应用在使用入口程序集的 `Development` 环境中运行时的[机密管理器](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="02237-126">[Secret Manager](xref:security/app-secrets) when the app runs in the `Development` environment using the entry assembly.</span></span>
  * <span data-ttu-id="02237-127">环境变量。</span><span class="sxs-lookup"><span data-stu-id="02237-127">Environment variables.</span></span>
  * <span data-ttu-id="02237-128">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="02237-128">Command-line arguments.</span></span>
* <span data-ttu-id="02237-129">配置控制台和调试输出的[日志记录](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="02237-129">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="02237-130">日志记录包含 appsettings.json 或 appsettings.{Environment}.json 文件的日志记录配置部分中指定的[日志筛选](xref:fundamentals/logging/index#log-filtering)规则。</span><span class="sxs-lookup"><span data-stu-id="02237-130">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="02237-131">使用 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)在 IIS 后面运行时，`CreateDefaultBuilder` 会启用 [IIS 集成](xref:host-and-deploy/iis/index)，这会配置应用的基址和端口。</span><span class="sxs-lookup"><span data-stu-id="02237-131">When running behind IIS with the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), `CreateDefaultBuilder` enables [IIS Integration](xref:host-and-deploy/iis/index), which configures the app's base address and port.</span></span> <span data-ttu-id="02237-132">IIS 集成还配置应用以[捕获启动错误](#capture-startup-errors)。</span><span class="sxs-lookup"><span data-stu-id="02237-132">IIS Integration also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="02237-133">有关 IIS 默认选项，请参阅 <xref:host-and-deploy/iis/index#iis-options>。</span><span class="sxs-lookup"><span data-stu-id="02237-133">For the IIS default options, see <xref:host-and-deploy/iis/index#iis-options>.</span></span>
* <span data-ttu-id="02237-134">如果应用环境为“开发”，请将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="02237-134">Sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span> <span data-ttu-id="02237-135">有关详细信息，请参阅[作用域验证](#scope-validation)。</span><span class="sxs-lookup"><span data-stu-id="02237-135">For more information, see [Scope validation](#scope-validation).</span></span>

<span data-ttu-id="02237-136">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration)、[ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging) 以及 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 的其他方法和扩展方法可重写和增强 `CreateDefaultBuilder` 定义的配置。</span><span class="sxs-lookup"><span data-stu-id="02237-136">The configuration defined by `CreateDefaultBuilder` can be overridden and augmented by [ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration), [ConfigureLogging](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configurelogging), and other methods and extension methods of [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="02237-137">下面是一些示例：</span><span class="sxs-lookup"><span data-stu-id="02237-137">A few examples follow:</span></span>

* <span data-ttu-id="02237-138">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) 用于指定应用的其他 `IConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="02237-138">[ConfigureAppConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configureappconfiguration) is used to specify additional `IConfiguration` for the app.</span></span> <span data-ttu-id="02237-139">下面的 `ConfigureAppConfiguration` 调用添加委托，以在 appsettings.xml 文件中添加应用配置。</span><span class="sxs-lookup"><span data-stu-id="02237-139">The following `ConfigureAppConfiguration` call adds a delegate to include app configuration in the *appsettings.xml* file.</span></span> <span data-ttu-id="02237-140">可多次调用 `ConfigureAppConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="02237-140">`ConfigureAppConfiguration` may be called multiple times.</span></span> <span data-ttu-id="02237-141">请注意，此配置不适用于主机（例如，服务器 URL 或环境）。</span><span class="sxs-lookup"><span data-stu-id="02237-141">Note that this configuration doesn't apply to the host (for example, server URLs or environment).</span></span> <span data-ttu-id="02237-142">请参阅[主机配置值](#host-configuration-values)部分。</span><span class="sxs-lookup"><span data-stu-id="02237-142">See the [Host configuration values](#host-configuration-values) section.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureAppConfiguration((hostingContext, config) =>
        {
            config.AddXmlFile("appsettings.xml", optional: true, reloadOnChange: true);
        })
        ...
    ```

* <span data-ttu-id="02237-143">下面的 `ConfigureLogging` 调用添加委托，以将最小日志记录级别 ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) 配置为 [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel)。</span><span class="sxs-lookup"><span data-stu-id="02237-143">The following `ConfigureLogging` call adds a delegate to configure the minimum logging level ([SetMinimumLevel](/dotnet/api/microsoft.extensions.logging.loggingbuilderextensions.setminimumlevel)) to [LogLevel.Warning](/dotnet/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="02237-144">此设置重写 `CreateDefaultBuilder` 在 appsettings.Development.json 和 appsettings.Production.json 中配置的设置，分别为 `LogLevel.Debug` 和 `LogLevel.Error`。</span><span class="sxs-lookup"><span data-stu-id="02237-144">This setting overrides the settings in *appsettings.Development.json* (`LogLevel.Debug`) and *appsettings.Production.json* (`LogLevel.Error`) configured by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="02237-145">可多次调用 `ConfigureLogging`。</span><span class="sxs-lookup"><span data-stu-id="02237-145">`ConfigureLogging` may be called multiple times.</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureLogging(logging => 
        {
            logging.SetMinimumLevel(LogLevel.Warning);
        })
        ...
    ```

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="02237-146">下面调用 `ConfigureKestrel` 来重写 `CreateDefaultBuilder` 在配置 Kestrel 时建立的 30,000,000 字节默认 [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)：</span><span class="sxs-lookup"><span data-stu-id="02237-146">The following call to `ConfigureKestrel` overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .ConfigureKestrel((context, options) =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="02237-147">下面调用 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 来重写 `CreateDefaultBuilder` 在配置 Kestrel 时建立的 30,000,000 字节默认 [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)：</span><span class="sxs-lookup"><span data-stu-id="02237-147">The following call to [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) overrides the default [Limits.MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize) of 30,000,000 bytes established when Kestrel was configured by `CreateDefaultBuilder`:</span></span>

    ```csharp
    WebHost.CreateDefaultBuilder(args)
        .UseKestrel(options =>
        {
            options.Limits.MaxRequestBodySize = 20000000;
        });
    ```

::: moniker-end

<span data-ttu-id="02237-148">内容根确定主机搜索内容文件（如 MVC 视图文件）的位置。</span><span class="sxs-lookup"><span data-stu-id="02237-148">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="02237-149">应用从项目的根文件夹启动时，会将项目的根文件夹用作内容根。</span><span class="sxs-lookup"><span data-stu-id="02237-149">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="02237-150">这是 [Visual Studio](https://www.visualstudio.com/) 和 [dotnet new 模板](/dotnet/core/tools/dotnet-new)中使用的默认值。</span><span class="sxs-lookup"><span data-stu-id="02237-150">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="02237-151">有关应用配置的详细信息，请参阅 <xref:fundamentals/configuration/index>。</span><span class="sxs-lookup"><span data-stu-id="02237-151">For more information on app configuration, see <xref:fundamentals/configuration/index>.</span></span>

> [!NOTE]
> <span data-ttu-id="02237-152">作为使用静态 `CreateDefaultBuilder` 方法的替代方法，从 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 创建主机是一种受 ASP.NET Core 2.x 支持的方法。</span><span class="sxs-lookup"><span data-stu-id="02237-152">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="02237-153">有关详细信息，请参阅 ASP.NET Core 1.x 选项卡。</span><span class="sxs-lookup"><span data-stu-id="02237-153">For more information, see the ASP.NET Core 1.x tab.</span></span>

<span data-ttu-id="02237-154">设置主机时，可以提供[配置](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1)和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) 方法。</span><span class="sxs-lookup"><span data-stu-id="02237-154">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="02237-155">如果指定 `Startup` 类，必须定义 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="02237-155">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="02237-156">有关更多信息，请参见<xref:fundamentals/startup>。</span><span class="sxs-lookup"><span data-stu-id="02237-156">For more information, see <xref:fundamentals/startup>.</span></span> <span data-ttu-id="02237-157">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="02237-157">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="02237-158">多次调用 `WebHostBuilder` 上的 `Configure` 或 `UseStartup` 将替换以前的设置。</span><span class="sxs-lookup"><span data-stu-id="02237-158">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="02237-159">主机配置值</span><span class="sxs-lookup"><span data-stu-id="02237-159">Host configuration values</span></span>

<span data-ttu-id="02237-160">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) 依赖于以下的方法设置主机配置值：</span><span class="sxs-lookup"><span data-stu-id="02237-160">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="02237-161">主机生成器配置，其中包括格式 `ASPNETCORE_{configurationKey}` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="02237-161">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="02237-162">例如 `ASPNETCORE_ENVIRONMENT`。</span><span class="sxs-lookup"><span data-stu-id="02237-162">For example, `ASPNETCORE_ENVIRONMENT`.</span></span>
* <span data-ttu-id="02237-163">[UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) 和 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 等扩展（请参阅[重写配置](#override-configuration)部分）。</span><span class="sxs-lookup"><span data-stu-id="02237-163">Extensions such as [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot) and [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) (see the [Override configuration](#override-configuration) section).</span></span>
* <span data-ttu-id="02237-164">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) 和关联键。</span><span class="sxs-lookup"><span data-stu-id="02237-164">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="02237-165">使用 `UseSetting` 设置值时，该值设置为无论何种类型的字符串。</span><span class="sxs-lookup"><span data-stu-id="02237-165">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="02237-166">主机使用任何一个选项设置上一个值。</span><span class="sxs-lookup"><span data-stu-id="02237-166">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="02237-167">有关详细信息，请参阅下一部分中的[重写配置](#override-configuration)。</span><span class="sxs-lookup"><span data-stu-id="02237-167">For more information, see [Override configuration](#override-configuration) in the next section.</span></span>

### <a name="application-key-name"></a><span data-ttu-id="02237-168">应用程序键（名称）</span><span class="sxs-lookup"><span data-stu-id="02237-168">Application Key (Name)</span></span>

<span data-ttu-id="02237-169">在主机构造期间调用 [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) 或 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) 时，会自动设置 [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) 属性。</span><span class="sxs-lookup"><span data-stu-id="02237-169">The [IHostingEnvironment.ApplicationName](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.applicationname) property is automatically set when [UseStartup](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup) or [Configure](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configure) is called during host construction.</span></span> <span data-ttu-id="02237-170">该值设置为包含应用入口点的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="02237-170">The value is set to the name of the assembly containing the app's entry point.</span></span> <span data-ttu-id="02237-171">要显式设置值，请使用 [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey)：</span><span class="sxs-lookup"><span data-stu-id="02237-171">To set the value explicitly, use the [WebHostDefaults.ApplicationKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.applicationkey):</span></span>

<span data-ttu-id="02237-172">**密钥**：applicationName</span><span class="sxs-lookup"><span data-stu-id="02237-172">**Key**: applicationName</span></span>  
<span data-ttu-id="02237-173">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-173">**Type**: *string*</span></span>  
<span data-ttu-id="02237-174">**默认**：包含应用入口点的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="02237-174">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="02237-175">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="02237-175">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="02237-176">**环境变量**：`ASPNETCORE_APPLICATIONNAME`</span><span class="sxs-lookup"><span data-stu-id="02237-176">**Environment variable**: `ASPNETCORE_APPLICATIONNAME`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.ApplicationKey, "CustomApplicationName")
```

### <a name="capture-startup-errors"></a><span data-ttu-id="02237-177">捕获启动错误</span><span class="sxs-lookup"><span data-stu-id="02237-177">Capture Startup Errors</span></span>

<span data-ttu-id="02237-178">此设置控制启动错误的捕获。</span><span class="sxs-lookup"><span data-stu-id="02237-178">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="02237-179">**键**：captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="02237-179">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="02237-180">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="02237-180">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="02237-181">**默认值**：默认为 `false`，除非应用使用 Kestrel 在 IIS 后方运行，其中默认值是 `true`。</span><span class="sxs-lookup"><span data-stu-id="02237-181">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="02237-182">**设置使用**：`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="02237-182">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="02237-183">**环境变量**：`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="02237-183">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="02237-184">当 `false` 时，启动期间出错导致主机退出。</span><span class="sxs-lookup"><span data-stu-id="02237-184">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="02237-185">当 `true` 时，主机在启动期间捕获异常并尝试启动服务器。</span><span class="sxs-lookup"><span data-stu-id="02237-185">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
```

### <a name="content-root"></a><span data-ttu-id="02237-186">内容根</span><span class="sxs-lookup"><span data-stu-id="02237-186">Content Root</span></span>

<span data-ttu-id="02237-187">此设置确定 ASP.NET Core 开始搜索内容文件，如 MVC 视图等。</span><span class="sxs-lookup"><span data-stu-id="02237-187">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="02237-188">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="02237-188">**Key**: contentRoot</span></span>  
<span data-ttu-id="02237-189">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-189">**Type**: *string*</span></span>  
<span data-ttu-id="02237-190">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="02237-190">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="02237-191">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="02237-191">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="02237-192">**环境变量**：`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="02237-192">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="02237-193">内容根也用作 [Web 根设置](#web-root)的基路径。</span><span class="sxs-lookup"><span data-stu-id="02237-193">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="02237-194">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="02237-194">If the path doesn't exist, the host fails to start.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\<content-root>")
```

### <a name="detailed-errors"></a><span data-ttu-id="02237-195">详细错误</span><span class="sxs-lookup"><span data-stu-id="02237-195">Detailed Errors</span></span>

<span data-ttu-id="02237-196">确定是否应捕获详细错误。</span><span class="sxs-lookup"><span data-stu-id="02237-196">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="02237-197">**键**：detailedErrors</span><span class="sxs-lookup"><span data-stu-id="02237-197">**Key**: detailedErrors</span></span>  
<span data-ttu-id="02237-198">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="02237-198">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="02237-199">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="02237-199">**Default**: false</span></span>  
<span data-ttu-id="02237-200">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="02237-200">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="02237-201">**环境变量**：`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="02237-201">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="02237-202">启用（或当<a href="#environment">环境</a>设置为 `Development` ）时，应用捕获详细的异常。</span><span class="sxs-lookup"><span data-stu-id="02237-202">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
```

### <a name="environment"></a><span data-ttu-id="02237-203">环境</span><span class="sxs-lookup"><span data-stu-id="02237-203">Environment</span></span>

<span data-ttu-id="02237-204">设置应用的环境。</span><span class="sxs-lookup"><span data-stu-id="02237-204">Sets the app's environment.</span></span>

<span data-ttu-id="02237-205">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="02237-205">**Key**: environment</span></span>  
<span data-ttu-id="02237-206">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-206">**Type**: *string*</span></span>  
<span data-ttu-id="02237-207">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="02237-207">**Default**: Production</span></span>  
<span data-ttu-id="02237-208">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="02237-208">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="02237-209">**环境变量**：`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="02237-209">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="02237-210">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="02237-210">The environment can be set to any value.</span></span> <span data-ttu-id="02237-211">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="02237-211">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="02237-212">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="02237-212">Values aren't case sensitive.</span></span> <span data-ttu-id="02237-213">默认情况下，从 `ASPNETCORE_ENVIRONMENT` 环境变量读取环境。</span><span class="sxs-lookup"><span data-stu-id="02237-213">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="02237-214">使用 [Visual Studio](https://www.visualstudio.com/) 时，可能会在 launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="02237-214">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="02237-215">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="02237-215">For more information, see <xref:fundamentals/environments>.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment(EnvironmentName.Development)
```

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="02237-216">承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="02237-216">Hosting Startup Assemblies</span></span>

<span data-ttu-id="02237-217">设置应用的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="02237-217">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="02237-218">**键**：hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="02237-218">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="02237-219">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-219">**Type**: *string*</span></span>  
<span data-ttu-id="02237-220">**默认值**：空字符串</span><span class="sxs-lookup"><span data-stu-id="02237-220">**Default**: Empty string</span></span>  
<span data-ttu-id="02237-221">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="02237-221">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="02237-222">**环境变量**：`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="02237-222">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="02237-223">承载启动程序集的以分号分隔的字符串在启动时加载。</span><span class="sxs-lookup"><span data-stu-id="02237-223">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span>

<span data-ttu-id="02237-224">虽然配置值默认为空字符串，但是承载启动程序集会始终包含应用的程序集。</span><span class="sxs-lookup"><span data-stu-id="02237-224">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="02237-225">提供承载启动程序集时，当应用在启动过程中生成其公用服务时将它们添加到应用的程序集加载。</span><span class="sxs-lookup"><span data-stu-id="02237-225">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
```

### <a name="https-port"></a><span data-ttu-id="02237-226">HTTPS 端口</span><span class="sxs-lookup"><span data-stu-id="02237-226">HTTPS Port</span></span>

<span data-ttu-id="02237-227">设置 HTTPS 重定向端口。</span><span class="sxs-lookup"><span data-stu-id="02237-227">Set the HTTPS redirect port.</span></span> <span data-ttu-id="02237-228">用于[强制实施 HTTPS](xref:security/enforcing-ssl)。</span><span class="sxs-lookup"><span data-stu-id="02237-228">Used in [enforcing HTTPS](xref:security/enforcing-ssl).</span></span>

<span data-ttu-id="02237-229">键：https_port；类型：字符串；
默认值：未设置默认值。</span><span class="sxs-lookup"><span data-stu-id="02237-229">**Key**: https_port **Type**: *string*
**Default**: A default value isn't set.</span></span>
<span data-ttu-id="02237-230">使用的设置：`UseSetting`
环境变量：`ASPNETCORE_HTTPS_PORT`</span><span class="sxs-lookup"><span data-stu-id="02237-230">**Set using**: `UseSetting`
**Environment variable**: `ASPNETCORE_HTTPS_PORT`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

### <a name="hosting-startup-exclude-assemblies"></a><span data-ttu-id="02237-231">承载启动排除程序集</span><span class="sxs-lookup"><span data-stu-id="02237-231">Hosting Startup Exclude Assemblies</span></span>

<span data-ttu-id="02237-232">承载启动程序集的以分号分隔的字符串在启动时排除。</span><span class="sxs-lookup"><span data-stu-id="02237-232">A semicolon-delimited string of hosting startup assemblies to exclude on startup.</span></span>

<span data-ttu-id="02237-233">键：hostingStartupExcludeAssemblies</span><span class="sxs-lookup"><span data-stu-id="02237-233">**Key**: hostingStartupExcludeAssemblies</span></span>  
<span data-ttu-id="02237-234">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-234">**Type**: *string*</span></span>  
<span data-ttu-id="02237-235">**默认值**：空字符串</span><span class="sxs-lookup"><span data-stu-id="02237-235">**Default**: Empty string</span></span>  
<span data-ttu-id="02237-236">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="02237-236">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="02237-237">**环境变量**：`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="02237-237">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupExcludeAssembliesKey, "assembly1;assembly2")
```

### <a name="prefer-hosting-urls"></a><span data-ttu-id="02237-238">首选承载 URL</span><span class="sxs-lookup"><span data-stu-id="02237-238">Prefer Hosting URLs</span></span>

<span data-ttu-id="02237-239">指示主机是否应该侦听使用 `WebHostBuilder` 配置的 URL，而不是使用 `IServer` 实现配置的 URL。</span><span class="sxs-lookup"><span data-stu-id="02237-239">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="02237-240">**键**：preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="02237-240">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="02237-241">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="02237-241">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="02237-242">**默认值**：true</span><span class="sxs-lookup"><span data-stu-id="02237-242">**Default**: true</span></span>  
<span data-ttu-id="02237-243">**设置使用**：`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="02237-243">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="02237-244">**环境变量**：`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="02237-244">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
```

### <a name="prevent-hosting-startup"></a><span data-ttu-id="02237-245">阻止承载启动</span><span class="sxs-lookup"><span data-stu-id="02237-245">Prevent Hosting Startup</span></span>

<span data-ttu-id="02237-246">阻止承载启动程序集自动加载，包括应用的程序集所配置的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="02237-246">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="02237-247">有关更多信息，请参见<xref:fundamentals/configuration/platform-specific-configuration>。</span><span class="sxs-lookup"><span data-stu-id="02237-247">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

<span data-ttu-id="02237-248">**键**：preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="02237-248">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="02237-249">**类型**：布尔型（`true` 或 `1`）</span><span class="sxs-lookup"><span data-stu-id="02237-249">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="02237-250">**默认值**：false</span><span class="sxs-lookup"><span data-stu-id="02237-250">**Default**: false</span></span>  
<span data-ttu-id="02237-251">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="02237-251">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="02237-252">**环境变量**：`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="02237-252">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
```

### <a name="server-urls"></a><span data-ttu-id="02237-253">服务器 URL</span><span class="sxs-lookup"><span data-stu-id="02237-253">Server URLs</span></span>

<span data-ttu-id="02237-254">指示 IP 地址或主机地址，其中包含服务器应针对请求侦听的端口和协议。</span><span class="sxs-lookup"><span data-stu-id="02237-254">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="02237-255">**键**：urls</span><span class="sxs-lookup"><span data-stu-id="02237-255">**Key**: urls</span></span>  
<span data-ttu-id="02237-256">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-256">**Type**: *string*</span></span>  
<span data-ttu-id="02237-257">**默认**： http://localhost:5000</span><span class="sxs-lookup"><span data-stu-id="02237-257">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="02237-258">**设置使用**：`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="02237-258">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="02237-259">**环境变量**：`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="02237-259">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="02237-260">设置为服务器应响应的以分号分隔 (;) 的 URL 前缀列表。</span><span class="sxs-lookup"><span data-stu-id="02237-260">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="02237-261">例如 `http://localhost:123`。</span><span class="sxs-lookup"><span data-stu-id="02237-261">For example, `http://localhost:123`.</span></span> <span data-ttu-id="02237-262">使用“\*”指示服务器应针对请求侦听的使用特定端口和协议（例如 `http://*:5000`）的 IP 地址或主机名。</span><span class="sxs-lookup"><span data-stu-id="02237-262">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="02237-263">协议（`http://` 或 `https://`）必须包含每个 URL。</span><span class="sxs-lookup"><span data-stu-id="02237-263">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="02237-264">不同的服务器支持的格式有所不同。</span><span class="sxs-lookup"><span data-stu-id="02237-264">Supported formats vary among servers.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
```

<span data-ttu-id="02237-265">Kestrel 具有自己的终结点配置 API。</span><span class="sxs-lookup"><span data-stu-id="02237-265">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="02237-266">有关更多信息，请参见<xref:fundamentals/servers/kestrel#endpoint-configuration>。</span><span class="sxs-lookup"><span data-stu-id="02237-266">For more information, see <xref:fundamentals/servers/kestrel#endpoint-configuration>.</span></span>

### <a name="shutdown-timeout"></a><span data-ttu-id="02237-267">关闭超时</span><span class="sxs-lookup"><span data-stu-id="02237-267">Shutdown Timeout</span></span>

<span data-ttu-id="02237-268">指定等待 Web 主机关闭的时长。</span><span class="sxs-lookup"><span data-stu-id="02237-268">Specifies the amount of time to wait for the web host to shut down.</span></span>

<span data-ttu-id="02237-269">**键**：shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="02237-269">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="02237-270">**类型**：int</span><span class="sxs-lookup"><span data-stu-id="02237-270">**Type**: *int*</span></span>  
<span data-ttu-id="02237-271">**默认值**：5</span><span class="sxs-lookup"><span data-stu-id="02237-271">**Default**: 5</span></span>  
<span data-ttu-id="02237-272">**设置使用**：`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="02237-272">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="02237-273">**环境变量**：`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="02237-273">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="02237-274">虽然键使用 `UseSetting` 接受 int（例如 `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`），但是 [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) 扩展方法采用 [TimeSpan](/dotnet/api/system.timespan)。</span><span class="sxs-lookup"><span data-stu-id="02237-274">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the [UseShutdownTimeout](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useshutdowntimeout) extension method takes a [TimeSpan](/dotnet/api/system.timespan).</span></span>

<span data-ttu-id="02237-275">在超时时间段中，托管：</span><span class="sxs-lookup"><span data-stu-id="02237-275">During the timeout period, hosting:</span></span>

* <span data-ttu-id="02237-276">触发器 [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping)。</span><span class="sxs-lookup"><span data-stu-id="02237-276">Triggers [IApplicationLifetime.ApplicationStopping](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstopping).</span></span>
* <span data-ttu-id="02237-277">尝试停止托管服务，对服务停止失败的任何错误进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="02237-277">Attempts to stop hosted services, logging any errors for services that fail to stop.</span></span>

<span data-ttu-id="02237-278">如果在所有托管服务停止之前就达到了超时时间，则会在应用关闭时会终止剩余的所有活动的服务。</span><span class="sxs-lookup"><span data-stu-id="02237-278">If the timeout period expires before all of the hosted services stop, any remaining active services are stopped when the app shuts down.</span></span> <span data-ttu-id="02237-279">即使没有完成处理工作，服务也会停止。</span><span class="sxs-lookup"><span data-stu-id="02237-279">The services stop even if they haven't finished processing.</span></span> <span data-ttu-id="02237-280">如果停止服务需要额外的时间，请增加超时时间。</span><span class="sxs-lookup"><span data-stu-id="02237-280">If services require additional time to stop, increase the timeout.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
```

### <a name="startup-assembly"></a><span data-ttu-id="02237-281">启动程序集</span><span class="sxs-lookup"><span data-stu-id="02237-281">Startup Assembly</span></span>

<span data-ttu-id="02237-282">确定要在其中搜索 `Startup` 类的程序集。</span><span class="sxs-lookup"><span data-stu-id="02237-282">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="02237-283">**键**：startupAssembly</span><span class="sxs-lookup"><span data-stu-id="02237-283">**Key**: startupAssembly</span></span>  
<span data-ttu-id="02237-284">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-284">**Type**: *string*</span></span>  
<span data-ttu-id="02237-285">**默认值**：应用的程序集</span><span class="sxs-lookup"><span data-stu-id="02237-285">**Default**: The app's assembly</span></span>  
<span data-ttu-id="02237-286">**设置使用**：`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="02237-286">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="02237-287">**环境变量**：`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="02237-287">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="02237-288">按名称（`string`）或类型（`TStartup`）的程序集可以引用。</span><span class="sxs-lookup"><span data-stu-id="02237-288">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="02237-289">如果调用多个 `UseStartup` 方法，优先选择最后一个方法。</span><span class="sxs-lookup"><span data-stu-id="02237-289">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
```

### <a name="web-root"></a><span data-ttu-id="02237-290">Web 根路径</span><span class="sxs-lookup"><span data-stu-id="02237-290">Web Root</span></span>

<span data-ttu-id="02237-291">设置应用的静态资产的相对路径。</span><span class="sxs-lookup"><span data-stu-id="02237-291">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="02237-292">**键**：webroot</span><span class="sxs-lookup"><span data-stu-id="02237-292">**Key**: webroot</span></span>  
<span data-ttu-id="02237-293">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="02237-293">**Type**: *string*</span></span>  
<span data-ttu-id="02237-294">**默认值**：如果未指定，默认值是“(Content Root)/wwwroot”（如果该路径存在）。</span><span class="sxs-lookup"><span data-stu-id="02237-294">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="02237-295">如果该路径不存在，则使用无操作文件提供程序。</span><span class="sxs-lookup"><span data-stu-id="02237-295">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="02237-296">**设置使用**：`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="02237-296">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="02237-297">**环境变量**：`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="02237-297">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
```

## <a name="override-configuration"></a><span data-ttu-id="02237-298">重写配置</span><span class="sxs-lookup"><span data-stu-id="02237-298">Override configuration</span></span>

<span data-ttu-id="02237-299">[配置](xref:fundamentals/configuration/index)可用于配置 Web 主机。</span><span class="sxs-lookup"><span data-stu-id="02237-299">Use [Configuration](xref:fundamentals/configuration/index) to configure the web host.</span></span> <span data-ttu-id="02237-300">在下面的示例中，主机配置是根据需要在 hostsettings.json 文件中指定。</span><span class="sxs-lookup"><span data-stu-id="02237-300">In the following example, host configuration is optionally specified in a *hostsettings.json* file.</span></span> <span data-ttu-id="02237-301">命令行参数可能会重写从 hostsettings.json 文件加载的任何配置。</span><span class="sxs-lookup"><span data-stu-id="02237-301">Any configuration loaded from the *hostsettings.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="02237-302">生成的配置（在 `config` 中）用于通过 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 配置主机。</span><span class="sxs-lookup"><span data-stu-id="02237-302">The built configuration (in `config`) is used to configure the host with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration).</span></span> <span data-ttu-id="02237-303">`IWebHostBuilder` 配置会添加到应用配置中，但反之不亦然&mdash;`ConfigureAppConfiguration` 不影响 `IWebHostBuilder` 配置。</span><span class="sxs-lookup"><span data-stu-id="02237-303">`IWebHostBuilder` configuration is added to the app's configuration, but the converse isn't true&mdash;`ConfigureAppConfiguration` doesn't affect the `IWebHostBuilder` configuration.</span></span>

<span data-ttu-id="02237-304">先用 hostsettings.json config 重写 `UseUrls` 提供的配置，再用命令行参数 config：</span><span class="sxs-lookup"><span data-stu-id="02237-304">Overriding the configuration provided by `UseUrls` with *hostsettings.json* config first, command-line argument config second:</span></span>

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
            });
    }
}
```

<span data-ttu-id="02237-305">hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="02237-305">*hostsettings.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

> [!NOTE]
> <span data-ttu-id="02237-306">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) 扩展方法当前不能分析由 `GetSection` 返回的配置部分（例如 `.UseConfiguration(Configuration.GetSection("section"))`。</span><span class="sxs-lookup"><span data-stu-id="02237-306">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="02237-307">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:urls`、`section:environment`）。</span><span class="sxs-lookup"><span data-stu-id="02237-307">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="02237-308">`UseConfiguration` 方法需要键来匹配 `WebHostBuilder` 键（例如 `urls`、`environment`）。</span><span class="sxs-lookup"><span data-stu-id="02237-308">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="02237-309">键上存在的节名称阻止节的值配置主机。</span><span class="sxs-lookup"><span data-stu-id="02237-309">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="02237-310">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="02237-310">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="02237-311">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="02237-311">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>
>
> <span data-ttu-id="02237-312">`UseConfiguration` 只将所提供的 `IConfiguration` 中的密钥复制到主机生成器配置中。</span><span class="sxs-lookup"><span data-stu-id="02237-312">`UseConfiguration` only copies keys from the provided `IConfiguration` to the host builder configuration.</span></span> <span data-ttu-id="02237-313">因此，JSON、INI 和 XML 设置文件的设置 `reloadOnChange: true` 没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="02237-313">Therefore, setting `reloadOnChange: true` for JSON, INI, and XML settings files has no effect.</span></span>

<span data-ttu-id="02237-314">若要指定在特定的 URL 上运行的主机，所需的值可以在执行 [dotnet 运行](/dotnet/core/tools/dotnet-run)时从命令提示符传入。</span><span class="sxs-lookup"><span data-stu-id="02237-314">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing [dotnet run](/dotnet/core/tools/dotnet-run).</span></span> <span data-ttu-id="02237-315">命令行参数重写 hostsettings.json 文件中的 `urls` 值，且服务器侦听端口 8080：</span><span class="sxs-lookup"><span data-stu-id="02237-315">The command-line argument overrides the `urls` value from the *hostsettings.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="manage-the-host"></a><span data-ttu-id="02237-316">管理主机</span><span class="sxs-lookup"><span data-stu-id="02237-316">Manage the host</span></span>

<span data-ttu-id="02237-317">**运行**</span><span class="sxs-lookup"><span data-stu-id="02237-317">**Run**</span></span>

<span data-ttu-id="02237-318">`Run` 方法启动 Web 应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="02237-318">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="02237-319">**Start**</span><span class="sxs-lookup"><span data-stu-id="02237-319">**Start**</span></span>

<span data-ttu-id="02237-320">通过调用 `Start` 方法以非阻止方式运行主机：</span><span class="sxs-lookup"><span data-stu-id="02237-320">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="02237-321">如果 URL 列表传递给 `Start` 方法，该列表侦听指定的 URL：</span><span class="sxs-lookup"><span data-stu-id="02237-321">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

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

<span data-ttu-id="02237-322">应用可以使用通过静态便捷方法预配置的 `CreateDefaultBuilder` 默认值初始化并启动新的主机。</span><span class="sxs-lookup"><span data-stu-id="02237-322">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="02237-323">这些方法在没有控制台输出的情况下启动服务器，并使用 [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) 等待中断（Ctrl-C/SIGINT 或 SIGTERM）：</span><span class="sxs-lookup"><span data-stu-id="02237-323">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="02237-324">**Start(RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="02237-324">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="02237-325">从 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="02237-325">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="02237-326">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="02237-326">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="02237-327">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="02237-327">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="02237-328">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="02237-328">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="02237-329">**Start(string url, RequestDelegate app)**</span><span class="sxs-lookup"><span data-stu-id="02237-329">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="02237-330">从 URL 和 `RequestDelegate` 开始：</span><span class="sxs-lookup"><span data-stu-id="02237-330">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="02237-331">生成与 Start(RequestDelegate app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="02237-331">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="02237-332">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="02237-332">**Start(Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="02237-333">使用 `IRouteBuilder` 的实例 ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) 用于路由中间件：</span><span class="sxs-lookup"><span data-stu-id="02237-333">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

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

<span data-ttu-id="02237-334">该示例中使用以下浏览器请求：</span><span class="sxs-lookup"><span data-stu-id="02237-334">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="02237-335">请求</span><span class="sxs-lookup"><span data-stu-id="02237-335">Request</span></span>                                    | <span data-ttu-id="02237-336">响应</span><span class="sxs-lookup"><span data-stu-id="02237-336">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="02237-337">Hello, Martin!</span><span class="sxs-lookup"><span data-stu-id="02237-337">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="02237-338">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="02237-338">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="02237-339">使用“ooops!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="02237-339">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="02237-340">使用“Uh oh!”字符串引发异常</span><span class="sxs-lookup"><span data-stu-id="02237-340">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="02237-341">Sante, Kevin!</span><span class="sxs-lookup"><span data-stu-id="02237-341">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="02237-342">Hello World!</span><span class="sxs-lookup"><span data-stu-id="02237-342">Hello World!</span></span>                             |

<span data-ttu-id="02237-343">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="02237-343">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="02237-344">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="02237-344">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="02237-345">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="02237-345">**Start(string url, Action&lt;IRouteBuilder&gt; routeBuilder)**</span></span>

<span data-ttu-id="02237-346">使用 URL 和 `IRouteBuilder` 实例：</span><span class="sxs-lookup"><span data-stu-id="02237-346">Use a URL and an instance of `IRouteBuilder`:</span></span>

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

<span data-ttu-id="02237-347">生成与 Start(Action&lt;IRouteBuilder&gt; routeBuilder) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="02237-347">Produces the same result as **Start(Action&lt;IRouteBuilder&gt; routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="02237-348">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="02237-348">**StartWith(Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="02237-349">提供委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="02237-349">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="02237-350">在浏览器中向 `http://localhost:5000` 发出请求，接收响应“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="02237-350">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="02237-351">`WaitForShutdown` 受到阻止，直到发出中断（Ctrl-C/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="02237-351">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="02237-352">应用显示 `Console.WriteLine` 消息并等待 keypress 退出。</span><span class="sxs-lookup"><span data-stu-id="02237-352">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="02237-353">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span><span class="sxs-lookup"><span data-stu-id="02237-353">**StartWith(string url, Action&lt;IApplicationBuilder&gt; app)**</span></span>

<span data-ttu-id="02237-354">提供 URL 和委托以配置 `IApplicationBuilder`：</span><span class="sxs-lookup"><span data-stu-id="02237-354">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

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

<span data-ttu-id="02237-355">生成与 StartWith(Action&lt;IApplicationBuilder&gt; app) 相同的结果，除非应用在 `http://localhost:8080` 上响应。</span><span class="sxs-lookup"><span data-stu-id="02237-355">Produces the same result as **StartWith(Action&lt;IApplicationBuilder&gt; app)**, except the app responds on `http://localhost:8080`.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="02237-356">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="02237-356">IHostingEnvironment interface</span></span>

<span data-ttu-id="02237-357">[IHostingEnvironment 接口](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment)提供有关应用的 Web 承载环境的信息。</span><span class="sxs-lookup"><span data-stu-id="02237-357">The [IHostingEnvironment interface](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="02237-358">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="02237-358">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

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

<span data-ttu-id="02237-359">[基于约定的方法](xref:fundamentals/environments#environment-based-startup-class-and-methods)可以用于在启动时基于环境配置应用。</span><span class="sxs-lookup"><span data-stu-id="02237-359">A [convention-based approach](xref:fundamentals/environments#environment-based-startup-class-and-methods) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="02237-360">或者，将 `IHostingEnvironment` 注入到 `Startup` 构造函数用于 `ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="02237-360">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

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
> <span data-ttu-id="02237-361">除了 `IsDevelopment` 扩展方法，`IHostingEnvironment` 提供 `IsStaging`、`IsProduction` 和 `IsEnvironment(string environmentName)` 方法。</span><span class="sxs-lookup"><span data-stu-id="02237-361">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="02237-362">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="02237-362">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="02237-363">`IHostingEnvironment` 服务还可以直接注入到 `Configure` 方法以设置处理管道：</span><span class="sxs-lookup"><span data-stu-id="02237-363">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

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

<span data-ttu-id="02237-364">创建自定义[中间件](xref:fundamentals/middleware/index#write-middleware)时可以将 `IHostingEnvironment` 注入 `Invoke` 方法：</span><span class="sxs-lookup"><span data-stu-id="02237-364">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware/index#write-middleware):</span></span>

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

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="02237-365">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="02237-365">IApplicationLifetime interface</span></span>

<span data-ttu-id="02237-366">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) 允许后启动和关闭活动。</span><span class="sxs-lookup"><span data-stu-id="02237-366">[IApplicationLifetime](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="02237-367">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="02237-367">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="02237-368">取消标记</span><span class="sxs-lookup"><span data-stu-id="02237-368">Cancellation Token</span></span>    | <span data-ttu-id="02237-369">触发条件</span><span class="sxs-lookup"><span data-stu-id="02237-369">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| [<span data-ttu-id="02237-370">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="02237-370">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="02237-371">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="02237-371">The host has fully started.</span></span> |
| [<span data-ttu-id="02237-372">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="02237-372">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="02237-373">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="02237-373">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="02237-374">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="02237-374">All requests should be processed.</span></span> <span data-ttu-id="02237-375">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="02237-375">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="02237-376">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="02237-376">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="02237-377">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="02237-377">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="02237-378">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="02237-378">Requests may still be processing.</span></span> <span data-ttu-id="02237-379">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="02237-379">Shutdown blocks until this event completes.</span></span> |

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

<span data-ttu-id="02237-380">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) 请求应用终止。</span><span class="sxs-lookup"><span data-stu-id="02237-380">[StopApplication](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="02237-381">以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：</span><span class="sxs-lookup"><span data-stu-id="02237-381">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="scope-validation"></a><span data-ttu-id="02237-382">作用域验证</span><span class="sxs-lookup"><span data-stu-id="02237-382">Scope validation</span></span>

<span data-ttu-id="02237-383">如果应用环境为“开发”，则 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 将 [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) 设为 `true`。</span><span class="sxs-lookup"><span data-stu-id="02237-383">[CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) sets [ServiceProviderOptions.ValidateScopes](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions.validatescopes) to `true` if the app's environment is Development.</span></span>

<span data-ttu-id="02237-384">若将 `ValidateScopes` 设为 `true`，默认服务提供程序会执行检查来验证以下内容：</span><span class="sxs-lookup"><span data-stu-id="02237-384">When `ValidateScopes` is set to `true`, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="02237-385">没有从根服务提供程序直接或间接解析到有作用域的服务。</span><span class="sxs-lookup"><span data-stu-id="02237-385">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="02237-386">未将有作用域的服务直接或间接注入到单一实例。</span><span class="sxs-lookup"><span data-stu-id="02237-386">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="02237-387">调用 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) 时，会创建根服务提供程序。</span><span class="sxs-lookup"><span data-stu-id="02237-387">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="02237-388">在启动提供程序和应用时，根服务提供程序的生存期对应于应用/服务的生存期，并在关闭应用时释放。</span><span class="sxs-lookup"><span data-stu-id="02237-388">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="02237-389">有作用域的服务由创建它们的容器释放。</span><span class="sxs-lookup"><span data-stu-id="02237-389">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="02237-390">如果作用域创建于根容器，则该服务的生存会有效地提升至单一实例，因为根容器只会在应用/服务关闭时将其释放。</span><span class="sxs-lookup"><span data-stu-id="02237-390">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="02237-391">验证服务作用域，将在调用 `BuildServiceProvider` 时收集这类情况。</span><span class="sxs-lookup"><span data-stu-id="02237-391">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="02237-392">若要始终验证作用域（包括在生存环境中验证），请使用主机生成器上的 [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) 配置 [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions)：</span><span class="sxs-lookup"><span data-stu-id="02237-392">To always validate scopes, including in the Production environment, configure the [ServiceProviderOptions](/dotnet/api/microsoft.extensions.dependencyinjection.serviceprovideroptions) with [UseDefaultServiceProvider](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usedefaultserviceprovider) on the host builder:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseDefaultServiceProvider((context, options) => {
        options.ValidateScopes = true;
    })
```

## <a name="additional-resources"></a><span data-ttu-id="02237-393">其他资源</span><span class="sxs-lookup"><span data-stu-id="02237-393">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:host-and-deploy/windows-service>
