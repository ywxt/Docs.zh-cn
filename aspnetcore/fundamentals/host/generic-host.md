---
title: .NET 通用主机
author: guardrex
description: 了解有关 .NET 中负责应用启动和生存期管理的通用主机。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: 33e5829ce4a09e132743b4174a588cf232a44775
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276249"
---
# <a name="net-generic-host"></a><span data-ttu-id="c4423-103">.NET 通用主机</span><span class="sxs-lookup"><span data-stu-id="c4423-103">.NET Generic Host</span></span>

<span data-ttu-id="c4423-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="c4423-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c4423-105">.NET 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="c4423-105">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="c4423-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="c4423-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="c4423-107">本主题介绍 ASP.NET Core 通用主机 ([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder))，该主机对于托管不处理 HTTP 请求的应用非常有用。</span><span class="sxs-lookup"><span data-stu-id="c4423-107">This topic covers the ASP.NET Core Generic Host ([HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)), which is useful for hosting apps that don't process HTTP requests.</span></span> <span data-ttu-id="c4423-108">有关 Web 主机 ([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)) 的介绍，请参阅 [Web 主机](xref:fundamentals/host/web-host)主题。</span><span class="sxs-lookup"><span data-stu-id="c4423-108">For coverage of the Web Host ([WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)), see the [Web Host](xref:fundamentals/host/web-host) topic.</span></span>

<span data-ttu-id="c4423-109">通用主机的目标是将 HTTP 管道从 Web 主机 API 中分离出来，从而启用更多的主机方案。</span><span class="sxs-lookup"><span data-stu-id="c4423-109">The goal of the Generic Host is to decouple the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="c4423-110">基于通用主机的消息、后台任务和其他非 HTTP 工作负载可从横切功能（如配置、依赖关系注入 [DI] 和日志记录）中受益。</span><span class="sxs-lookup"><span data-stu-id="c4423-110">Messaging, background tasks, and other non-HTTP workloads based on the Generic Host benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="c4423-111">通用主机是 ASP.NET Core 2.1 中的新增功能，不适用于 Web 承载方案。</span><span class="sxs-lookup"><span data-stu-id="c4423-111">The Generic Host is new in ASP.NET Core 2.1 and isn't suitable for web hosting scenarios.</span></span> <span data-ttu-id="c4423-112">对于 Web 承载方案，请使用 [Web 主机](xref:fundamentals/host/web-host)。</span><span class="sxs-lookup"><span data-stu-id="c4423-112">For web hosting scenarios, use the [Web Host](xref:fundamentals/host/web-host).</span></span> <span data-ttu-id="c4423-113">通用主机正处于开发阶段，用于在未来版本中替换 Web 主机，并在 HTTP 和非 HTTP 方案中充当主要的主机 API。</span><span class="sxs-lookup"><span data-stu-id="c4423-113">The Generic Host is under development to replace the Web Host in a future release and act as the primary host API in both HTTP and non-HTTP scenarios.</span></span>

<span data-ttu-id="c4423-114">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="c4423-114">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="c4423-115">在 [Visual Studio Code](https://code.visualstudio.com/) 中运行示例应用时，请使用外部或集成终端。</span><span class="sxs-lookup"><span data-stu-id="c4423-115">When running the sample app in [Visual Studio Code](https://code.visualstudio.com/), use an *external or integrated terminal*.</span></span> <span data-ttu-id="c4423-116">请勿在 `internalConsole` 中运行示例。</span><span class="sxs-lookup"><span data-stu-id="c4423-116">Don't run the sample in an `internalConsole`.</span></span>

<span data-ttu-id="c4423-117">在 Visual Studio Code 中设置控制台：</span><span class="sxs-lookup"><span data-stu-id="c4423-117">To set the console in Visual Studio Code:</span></span>

1. <span data-ttu-id="c4423-118">打开 .vscode/launch.json 文件。</span><span class="sxs-lookup"><span data-stu-id="c4423-118">Open the *.vscode/launch.json* file.</span></span>
1. <span data-ttu-id="c4423-119">在 .NET Core 启动（控制台）配置中，找到控制台条目。</span><span class="sxs-lookup"><span data-stu-id="c4423-119">In the **.NET Core Launch (console)** configuration, locate the **console** entry.</span></span> <span data-ttu-id="c4423-120">将值设置为 `externalTerminal` 或 `integratedTerminal`。</span><span class="sxs-lookup"><span data-stu-id="c4423-120">Set the value to either `externalTerminal` or `integratedTerminal`.</span></span>

## <a name="introduction"></a><span data-ttu-id="c4423-121">介绍</span><span class="sxs-lookup"><span data-stu-id="c4423-121">Introduction</span></span>

<span data-ttu-id="c4423-122">通用主机库位于 [Microsoft.Extensions.Hosting 命名空间](/dotnet/api/microsoft.extensions.hosting)中，由 [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="c4423-122">The Generic Host library is available in the [Microsoft.Extensions.Hosting namespace](/dotnet/api/microsoft.extensions.hosting) and provided by the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) package.</span></span> <span data-ttu-id="c4423-123">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)（ASP.NET Core 2.1 或更高版本）中包括 `Microsoft.Extensions.Hosting` 包。</span><span class="sxs-lookup"><span data-stu-id="c4423-123">The `Microsoft.Extensions.Hosting` package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later).</span></span>

<span data-ttu-id="c4423-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 是执行代码的入口点。</span><span class="sxs-lookup"><span data-stu-id="c4423-124">[IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) is the entry point to code execution.</span></span> <span data-ttu-id="c4423-125">每个 `IHostedService` 实现都按照 [ConfigureServices 中服务注册](#configureservices)的顺序执行。</span><span class="sxs-lookup"><span data-stu-id="c4423-125">Each `IHostedService` implementation is executed in the order of [service registration in ConfigureServices](#configureservices).</span></span> <span data-ttu-id="c4423-126">主机启动时，每个 `IHostedService` 上都会调用 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync)主机正常关闭时，以反向注册顺序调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync)。</span><span class="sxs-lookup"><span data-stu-id="c4423-126">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) is called on each `IHostedService` when the host starts, and [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) is called in reverse registration order when the host shuts down gracefully.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="c4423-127">设置主机</span><span class="sxs-lookup"><span data-stu-id="c4423-127">Set up a host</span></span>

<span data-ttu-id="c4423-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 是供库和应用初始化、生成和运行主机的主要组件：</span><span class="sxs-lookup"><span data-stu-id="c4423-128">[IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) is the main component that libraries and apps use to initialize, build, and run the host:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="host-configuration"></a><span data-ttu-id="c4423-129">主机配置</span><span class="sxs-lookup"><span data-stu-id="c4423-129">Host configuration</span></span>

<span data-ttu-id="c4423-130">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) 依赖于以下方法来设置主机配置值：</span><span class="sxs-lookup"><span data-stu-id="c4423-130">[HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="c4423-131">配置生成器</span><span class="sxs-lookup"><span data-stu-id="c4423-131">Configuration builder</span></span>
* <span data-ttu-id="c4423-132">扩展方法配置</span><span class="sxs-lookup"><span data-stu-id="c4423-132">Extension method configuration</span></span>

### <a name="configuration-builder"></a><span data-ttu-id="c4423-133">配置生成器</span><span class="sxs-lookup"><span data-stu-id="c4423-133">Configuration builder</span></span>

<span data-ttu-id="c4423-134">通过在 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 实现上调用 [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration) 来创建主机生成器配置。</span><span class="sxs-lookup"><span data-stu-id="c4423-134">Host builder configuration is created by calling [ConfigureHostConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configurehostconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="c4423-135">`ConfigureHostConfiguration` 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 为主机创建 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="c4423-135">`ConfigureHostConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the host.</span></span> <span data-ttu-id="c4423-136">配置生成器初始化 [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment)，以在应用程序的生成过程中使用。</span><span class="sxs-lookup"><span data-stu-id="c4423-136">The configuration builder initializes the [IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) for use in the app's build process.</span></span>

<span data-ttu-id="c4423-137">默认情况下，不添加环境变量配置。</span><span class="sxs-lookup"><span data-stu-id="c4423-137">Environment variable configuration isn't added by default.</span></span> <span data-ttu-id="c4423-138">对主机生成器调用 [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) 可以通过环境变量配置主机。</span><span class="sxs-lookup"><span data-stu-id="c4423-138">Call [AddEnvironmentVariables](/dotnet/api/microsoft.extensions.configuration.environmentvariablesextensions.addenvironmentvariables) on the host builder to configure the host from environment variables.</span></span> <span data-ttu-id="c4423-139">`AddEnvironmentVariables` 接受用户定义的前缀（可选）。</span><span class="sxs-lookup"><span data-stu-id="c4423-139">`AddEnvironmentVariables` accepts an optional user-defined prefix.</span></span> <span data-ttu-id="c4423-140">示例应用使用前缀 `PREFIX_`。</span><span class="sxs-lookup"><span data-stu-id="c4423-140">The sample app uses a prefix of `PREFIX_`.</span></span> <span data-ttu-id="c4423-141">当系统读取环境变量时，便会删除前缀。</span><span class="sxs-lookup"><span data-stu-id="c4423-141">The prefix is removed when the environment variables are read.</span></span> <span data-ttu-id="c4423-142">配置示例应用的主机后，`PREFIX_ENVIRONMENT` 的环境变量值就变成 `environment` 密钥的主机配置值。</span><span class="sxs-lookup"><span data-stu-id="c4423-142">When the sample app's host is configured, the environment variable value for `PREFIX_ENVIRONMENT` becomes the host configuration value for the `environment` key.</span></span>

<span data-ttu-id="c4423-143">在开发过程中，如果使用 [Visual Studio](https://www.visualstudio.com/) 或通过 `dotnet run` 运行应用，可能会在 Properties/launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="c4423-143">During development when using [Visual Studio](https://www.visualstudio.com/) or running an app with `dotnet run`, environment variables may be set in the *Properties/launchSettings.json* file.</span></span> <span data-ttu-id="c4423-144">若在开发过程中使用 [Visual Studio Code](https://code.visualstudio.com/)，可能会在 .vscode/launch.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="c4423-144">In [Visual Studio Code](https://code.visualstudio.com/), environment variables may be set in the *.vscode/launch.json* file during development.</span></span> <span data-ttu-id="c4423-145">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="c4423-145">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="c4423-146">可多次调用 `ConfigureHostConfiguration`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="c4423-146">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="c4423-147">主机使用任何一个选项设置上一个值。</span><span class="sxs-lookup"><span data-stu-id="c4423-147">The host uses whichever option sets a value last.</span></span>

<span data-ttu-id="c4423-148">hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="c4423-148">*hostsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

<span data-ttu-id="c4423-149">示例 `HostBuilder` 配置使用 `ConfigureHostConfiguration`：</span><span class="sxs-lookup"><span data-stu-id="c4423-149">Example `HostBuilder` configuration using `ConfigureHostConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

> [!NOTE]
> <span data-ttu-id="c4423-150">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 扩展方法当前不能分析由 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) 返回的配置部分（例如 `.AddConfiguration(Configuration.GetSection("section"))`）。</span><span class="sxs-lookup"><span data-stu-id="c4423-150">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="c4423-151">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:environment`）。</span><span class="sxs-lookup"><span data-stu-id="c4423-151">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:environment`).</span></span> <span data-ttu-id="c4423-152">`AddConfiguration` 方法需要键来匹配 `HostBuilder` 键（例如 `environment`）。</span><span class="sxs-lookup"><span data-stu-id="c4423-152">The `AddConfiguration` method expects the keys to match the `HostBuilder` keys (for example, `environment`).</span></span> <span data-ttu-id="c4423-153">键上存在的节名称阻止节的值配置主机。</span><span class="sxs-lookup"><span data-stu-id="c4423-153">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="c4423-154">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="c4423-154">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="c4423-155">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="c4423-155">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

### <a name="extension-method-configuration"></a><span data-ttu-id="c4423-156">扩展方法配置</span><span class="sxs-lookup"><span data-stu-id="c4423-156">Extension method configuration</span></span>

<span data-ttu-id="c4423-157">在 `IHostBuilder` 实现上调用扩展方法，用于配置内容根和环境。</span><span class="sxs-lookup"><span data-stu-id="c4423-157">Extension methods are called on the `IHostBuilder` implementation to configure the content root and the environment.</span></span>

#### <a name="content-root"></a><span data-ttu-id="c4423-158">内容根</span><span class="sxs-lookup"><span data-stu-id="c4423-158">Content Root</span></span>

<span data-ttu-id="c4423-159">此设置确定主机从哪里开始搜索内容文件。</span><span class="sxs-lookup"><span data-stu-id="c4423-159">This setting determines where the host begins searching for content files.</span></span>

<span data-ttu-id="c4423-160">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="c4423-160">**Key**: contentRoot</span></span>  
<span data-ttu-id="c4423-161">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="c4423-161">**Type**: *string*</span></span>  
<span data-ttu-id="c4423-162">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4423-162">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="c4423-163">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="c4423-163">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="c4423-164">**环境变量**：`<PREFIX_>CONTENTROOT`（`<PREFIX_>` 是[用户定义的可选前缀](#configuration-builder)）</span><span class="sxs-lookup"><span data-stu-id="c4423-164">**Environment variable**: `<PREFIX_>CONTENTROOT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="c4423-165">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="c4423-165">If the path doesn't exist, the host fails to start.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

#### <a name="environment"></a><span data-ttu-id="c4423-166">环境</span><span class="sxs-lookup"><span data-stu-id="c4423-166">Environment</span></span>

<span data-ttu-id="c4423-167">设置应用的[环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="c4423-167">Sets the app's [environment](xref:fundamentals/environments).</span></span>

<span data-ttu-id="c4423-168">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="c4423-168">**Key**: environment</span></span>  
<span data-ttu-id="c4423-169">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="c4423-169">**Type**: *string*</span></span>  
<span data-ttu-id="c4423-170">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="c4423-170">**Default**: Production</span></span>  
<span data-ttu-id="c4423-171">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="c4423-171">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="c4423-172">**环境变量**：`<PREFIX_>ENVIRONMENT`（`<PREFIX_>` 是[用户定义的可选前缀](#configuration-builder)）</span><span class="sxs-lookup"><span data-stu-id="c4423-172">**Environment variable**: `<PREFIX_>ENVIRONMENT` (`<PREFIX_>` is [optional and user-defined](#configuration-builder))</span></span>

<span data-ttu-id="c4423-173">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="c4423-173">The environment can be set to any value.</span></span> <span data-ttu-id="c4423-174">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="c4423-174">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="c4423-175">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="c4423-175">Values aren't case sensitive.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

## <a name="configureappconfiguration"></a><span data-ttu-id="c4423-176">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="c4423-176">ConfigureAppConfiguration</span></span>

<span data-ttu-id="c4423-177">通过在 [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) 实现上调用 [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration) 来创建应用生成器配置。</span><span class="sxs-lookup"><span data-stu-id="c4423-177">App builder configuration is created by calling [ConfigureAppConfiguration](/dotnet/api/microsoft.extensions.hosting.ihostbuilder.configureappconfiguration) on the [IHostBuilder](/dotnet/api/microsoft.extensions.hosting.ihostbuilder) implementation.</span></span> <span data-ttu-id="c4423-178">`ConfigureAppConfiguration` 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 为应用创建 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="c4423-178">`ConfigureAppConfiguration` uses an [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) to create an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) for the app.</span></span> <span data-ttu-id="c4423-179">可多次调用 `ConfigureAppConfiguration`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="c4423-179">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="c4423-180">应用会使用最后设置值的选项。</span><span class="sxs-lookup"><span data-stu-id="c4423-180">The app uses whichever option sets a value last.</span></span> <span data-ttu-id="c4423-181">用于进行后续操作和 [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services) 中的 [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration) 中可以使用由 `ConfigureAppConfiguration` 创建的配置。</span><span class="sxs-lookup"><span data-stu-id="c4423-181">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](/dotnet/api/microsoft.extensions.hosting.hostbuildercontext.configuration) for subsequent operations and in [Services](/dotnet/api/microsoft.extensions.hosting.ihost.services).</span></span>

<span data-ttu-id="c4423-182">示例应用配置使用 `ConfigureAppConfiguration`：</span><span class="sxs-lookup"><span data-stu-id="c4423-182">Example app configuration using `ConfigureAppConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

<span data-ttu-id="c4423-183">appsettings.json：</span><span class="sxs-lookup"><span data-stu-id="c4423-183">*appsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

<span data-ttu-id="c4423-184">appsettings.Development.json：</span><span class="sxs-lookup"><span data-stu-id="c4423-184">*appsettings.Development.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

<span data-ttu-id="c4423-185">appsettings.Production.json：</span><span class="sxs-lookup"><span data-stu-id="c4423-185">*appsettings.Production.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

> [!NOTE]
> <span data-ttu-id="c4423-186">[AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) 扩展方法当前不能分析由 [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) 返回的配置部分（例如 `.AddConfiguration(Configuration.GetSection("section"))`）。</span><span class="sxs-lookup"><span data-stu-id="c4423-186">The [AddConfiguration](/dotnet/api/microsoft.extensions.configuration.chainedbuilderextensions.addconfiguration) extension method isn't currently capable of parsing a configuration section returned by [GetSection](/dotnet/api/microsoft.extensions.configuration.iconfiguration.getsection) (for example, `.AddConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="c4423-187">`GetSection` 方法将配置键筛选到所请求的部分，但将节名称保留在键上（例如 `section:Logging:LogLevel:Default`）。</span><span class="sxs-lookup"><span data-stu-id="c4423-187">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:Logging:LogLevel:Default`).</span></span> <span data-ttu-id="c4423-188">`AddConfiguration` 方法预期得到配置键（例如 `Logging:LogLevel:Default`）的完全匹配项。</span><span class="sxs-lookup"><span data-stu-id="c4423-188">The `AddConfiguration` method expects an exact match to configuration keys (for example, `Logging:LogLevel:Default`).</span></span> <span data-ttu-id="c4423-189">键上存在的节名称阻止节的值配置应用。</span><span class="sxs-lookup"><span data-stu-id="c4423-189">The presence of the section name on the keys prevents the section's values from configuring the app.</span></span> <span data-ttu-id="c4423-190">将在即将发布的版本中解决此问题。</span><span class="sxs-lookup"><span data-stu-id="c4423-190">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="c4423-191">有关详细信息和解决方法，请参阅[将配置节传入到 WebHostBuilder.UseConfiguration 使用完整的键](https://github.com/aspnet/Hosting/issues/839)。</span><span class="sxs-lookup"><span data-stu-id="c4423-191">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

## <a name="configureservices"></a><span data-ttu-id="c4423-192">ConfigureServices</span><span class="sxs-lookup"><span data-stu-id="c4423-192">ConfigureServices</span></span>

<span data-ttu-id="c4423-193">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices) 将服务添加到应用的[依赖关系注入](xref:fundamentals/dependency-injection)容器。</span><span class="sxs-lookup"><span data-stu-id="c4423-193">[ConfigureServices](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configureservices) adds services to the app's [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="c4423-194">可多次调用 `ConfigureServices`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="c4423-194">`ConfigureServices` can be called multiple times with additive results.</span></span>

<span data-ttu-id="c4423-195">托管服务是一个类，具有实现 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="c4423-195">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="c4423-196">有关详细信息，请参阅[使用托管服务的后台任务](xref:fundamentals/host/hosted-services)主题。</span><span class="sxs-lookup"><span data-stu-id="c4423-196">For more information, see the [Background tasks with hosted services](xref:fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="c4423-197">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)使用 `AddHostedService` 扩展方法向应用添加生存期事件 `LifetimeEventsHostedService` 和定时后台任务 `TimedHostedService` 服务：</span><span class="sxs-lookup"><span data-stu-id="c4423-197">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses the `AddHostedService` extension method to add a service for lifetime events, `LifetimeEventsHostedService`, and a timed background task, `TimedHostedService`, to the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a><span data-ttu-id="c4423-198">ConfigureLogging</span><span class="sxs-lookup"><span data-stu-id="c4423-198">ConfigureLogging</span></span>

<span data-ttu-id="c4423-199">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging) 添加一个委托，用于配置提供的 [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder)。</span><span class="sxs-lookup"><span data-stu-id="c4423-199">[ConfigureLogging](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.configurelogging) adds a delegate for configuring the provided [ILoggingBuilder](/dotnet/api/microsoft.extensions.logging.iloggingbuilder).</span></span> <span data-ttu-id="c4423-200">可以利用相加结果多次调用 `ConfigureLogging`。</span><span class="sxs-lookup"><span data-stu-id="c4423-200">`ConfigureLogging` may be called multiple times with additive results.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a><span data-ttu-id="c4423-201">UseConsoleLifetime</span><span class="sxs-lookup"><span data-stu-id="c4423-201">UseConsoleLifetime</span></span>

<span data-ttu-id="c4423-202">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime) 侦听 `Ctrl+C`/SIGINT 或 SIGTERM 并调用 [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) 来启动关闭进程。</span><span class="sxs-lookup"><span data-stu-id="c4423-202">[UseConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.useconsolelifetime) listens for `Ctrl+C`/SIGINT or SIGTERM and calls [StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) to start the shutdown process.</span></span> <span data-ttu-id="c4423-203">`UseConsoleLifetime` 解除阻止 [ RunAsync](#runasync) 和 [WaitForShutdownAsync](#waitforshutdownasync) 等扩展。</span><span class="sxs-lookup"><span data-stu-id="c4423-203">`UseConsoleLifetime` unblocks extensions such as [RunAsync](#runasync) and [WaitForShutdownAsync](#waitforshutdownasync).</span></span> <span data-ttu-id="c4423-204">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) 预注册为默认生存期实现。</span><span class="sxs-lookup"><span data-stu-id="c4423-204">[ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) is pre-registered as the default lifetime implementation.</span></span> <span data-ttu-id="c4423-205">使用注册的最后一个生存期。</span><span class="sxs-lookup"><span data-stu-id="c4423-205">The last lifetime registered is used.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a><span data-ttu-id="c4423-206">容器配置</span><span class="sxs-lookup"><span data-stu-id="c4423-206">Container configuration</span></span>

<span data-ttu-id="c4423-207">为支持插入其他容器中，主机可以接受 [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1)。</span><span class="sxs-lookup"><span data-stu-id="c4423-207">To support plugging in other containers, the host can accept an [IServiceProviderFactory](/dotnet/api/microsoft.extensions.dependencyinjection.iserviceproviderfactory-1).</span></span> <span data-ttu-id="c4423-208">提供工厂不属于 DI 容器注册，而是用于创建具体 DI 容器的主机内部函数。</span><span class="sxs-lookup"><span data-stu-id="c4423-208">Providing a factory isn't part of the DI container registration but is instead a host intrinsic used to create the concrete DI container.</span></span> <span data-ttu-id="c4423-209">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory) 重写用于创建应用的服务提供程序的默认工厂。</span><span class="sxs-lookup"><span data-stu-id="c4423-209">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](/dotnet/api/microsoft.extensions.hosting.hostbuilder.useserviceproviderfactory) overrides the default factory used to create the app's service provider.</span></span>

<span data-ttu-id="c4423-210">[ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) 方法托管自定义容器配置。</span><span class="sxs-lookup"><span data-stu-id="c4423-210">Custom container configuration is managed by the [ConfigureContainer](/dotnet/api/microsoft.extensions.hosting.hostbuilder.configurecontainer) method.</span></span> <span data-ttu-id="c4423-211">`ConfigureContainer` 提供在基础主机 API 的基础之上配置容器的强类型体验。</span><span class="sxs-lookup"><span data-stu-id="c4423-211">`ConfigureContainer` provides a strongly-typed experience for configuring the container on top of the underlying host API.</span></span> <span data-ttu-id="c4423-212">可以利用相加结果多次调用 `ConfigureContainer`。</span><span class="sxs-lookup"><span data-stu-id="c4423-212">`ConfigureContainer` can be called multiple times with additive results.</span></span>

<span data-ttu-id="c4423-213">为应用创建服务容器：</span><span class="sxs-lookup"><span data-stu-id="c4423-213">Create a service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

<span data-ttu-id="c4423-214">提供服务容器工厂：</span><span class="sxs-lookup"><span data-stu-id="c4423-214">Provide a service container factory:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

<span data-ttu-id="c4423-215">使用该工厂并为应用配置自定义服务容器：</span><span class="sxs-lookup"><span data-stu-id="c4423-215">Use the factory and configure the custom service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a><span data-ttu-id="c4423-216">扩展性</span><span class="sxs-lookup"><span data-stu-id="c4423-216">Extensibility</span></span>

<span data-ttu-id="c4423-217">在 `IHostBuilder` 上使用扩展方法实现主机扩展性。</span><span class="sxs-lookup"><span data-stu-id="c4423-217">Host extensibility is performed with extension methods on `IHostBuilder`.</span></span> <span data-ttu-id="c4423-218">以下示例介绍扩展方法如何使用 [RabbitMQ](https://www.rabbitmq.com/) 扩展 `IHostBuilder` 实现。</span><span class="sxs-lookup"><span data-stu-id="c4423-218">The following example shows how an extension method extends an `IHostBuilder` implementation with [RabbitMQ](https://www.rabbitmq.com/).</span></span> <span data-ttu-id="c4423-219">该扩展方法（在应用中的其他位置）注册 RabbitMQ `IHostedService`：</span><span class="sxs-lookup"><span data-stu-id="c4423-219">The extension method (elsewhere in the app) registers a RabbitMQ `IHostedService`:</span></span>

```csharp
// UseRabbitMq is an extension method that sets up RabbitMQ to handle incoming
// messages.
var host = new HostBuilder()
    .UseRabbitMq<MyMessageHandler>()
    .Build();

await host.StartAsync();
```

## <a name="manage-the-host"></a><span data-ttu-id="c4423-220">管理主机</span><span class="sxs-lookup"><span data-stu-id="c4423-220">Manage the host</span></span>

<span data-ttu-id="c4423-221">[IHost](/dotnet/api/microsoft.extensions.hosting.ihost) 实现负责启动和停止服务容器中注册的 `IHostedService` 实现。</span><span class="sxs-lookup"><span data-stu-id="c4423-221">The [IHost](/dotnet/api/microsoft.extensions.hosting.ihost) implementation is responsible for starting and stopping the `IHostedService` implementations that are registered in the service container.</span></span>

### <a name="run"></a><span data-ttu-id="c4423-222">运行</span><span class="sxs-lookup"><span data-stu-id="c4423-222">Run</span></span>

<span data-ttu-id="c4423-223">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run) 运行应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="c4423-223">[Run](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.run) runs the app and blocks the calling thread until the host is shut down:</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        host.Run();
    }
}
```

### <a name="runasync"></a><span data-ttu-id="c4423-224">RunAsync</span><span class="sxs-lookup"><span data-stu-id="c4423-224">RunAsync</span></span>

<span data-ttu-id="c4423-225">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync) 运行应用并返回在触发取消令牌或关闭时完成的 `Task`：</span><span class="sxs-lookup"><span data-stu-id="c4423-225">[RunAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.runasync) runs the app and returns a `Task` that completes when the cancellation token or shutdown is triggered:</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        await host.RunAsync();
    }
}
```

### <a name="runconsoleasync"></a><span data-ttu-id="c4423-226">RunConsoleAsync</span><span class="sxs-lookup"><span data-stu-id="c4423-226">RunConsoleAsync</span></span>

<span data-ttu-id="c4423-227">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync) 启用控制台、生成和启动主机，以及等待 `Ctrl+C`/SIGINT 或 SIGTERM 关闭。</span><span class="sxs-lookup"><span data-stu-id="c4423-227">[RunConsoleAsync](/dotnet/api/microsoft.extensions.hosting.hostinghostbuilderextensions.runconsoleasync) enables console support, builds and starts the host, and waits for `Ctrl+C`/SIGINT or SIGTERM to shut down.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var hostBuilder = new HostBuilder();

        await hostBuilder.RunConsoleAsync();
    }
}
```

### <a name="start-and-stopasync"></a><span data-ttu-id="c4423-228">Start 和 StopAsync</span><span class="sxs-lookup"><span data-stu-id="c4423-228">Start and StopAsync</span></span>

<span data-ttu-id="c4423-229">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start) 同步启动主机。</span><span class="sxs-lookup"><span data-stu-id="c4423-229">[Start](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.start) starts the host synchronously.</span></span>

<span data-ttu-id="c4423-230">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync) 尝试在提供的超时时间内停止主机。</span><span class="sxs-lookup"><span data-stu-id="c4423-230">[StopAsync(TimeSpan)](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.stopasync) attempts to stop the host within the provided timeout.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            await host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

### <a name="startasync-and-stopasync"></a><span data-ttu-id="c4423-231">StartAsync 和 StopAsync</span><span class="sxs-lookup"><span data-stu-id="c4423-231">StartAsync and StopAsync</span></span>

<span data-ttu-id="c4423-232">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 启动应用。</span><span class="sxs-lookup"><span data-stu-id="c4423-232">[StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) starts the app.</span></span>

<span data-ttu-id="c4423-233">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) 停止应用。</span><span class="sxs-lookup"><span data-stu-id="c4423-233">[StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) stops the app.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.StopAsync();
        }
    }
}
```

### <a name="waitforshutdown"></a><span data-ttu-id="c4423-234">WaitForShutdown</span><span class="sxs-lookup"><span data-stu-id="c4423-234">WaitForShutdown</span></span>

<span data-ttu-id="c4423-235">通过 [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime)，如 [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime)（侦听 `Ctrl+C`/SIGINT 或 SIGTERM）来触发 [WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown)。</span><span class="sxs-lookup"><span data-stu-id="c4423-235">[WaitForShutdown](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdown) is triggered via the [IHostLifetime](/dotnet/api/microsoft.extensions.hosting.ihostlifetime), such as [ConsoleLifetime](/dotnet/api/microsoft.extensions.hosting.internal.consolelifetime) (listens for `Ctrl+C`/SIGINT or SIGTERM).</span></span> <span data-ttu-id="c4423-236">`WaitForShutdown` 调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync)。</span><span class="sxs-lookup"><span data-stu-id="c4423-236">`WaitForShutdown` calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            host.WaitForShutdown();
        }
    }
}
```

### <a name="waitforshutdownasync"></a><span data-ttu-id="c4423-237">WaitForShutdownAsync</span><span class="sxs-lookup"><span data-stu-id="c4423-237">WaitForShutdownAsync</span></span>

<span data-ttu-id="c4423-238">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync) 返回在通过给定的定牌和调用 [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync) 来触发关闭时完成的 `Task`。</span><span class="sxs-lookup"><span data-stu-id="c4423-238">[WaitForShutdownAsync](/dotnet/api/microsoft.extensions.hosting.hostingabstractionshostextensions.waitforshutdownasync) returns a `Task` that completes when shutdown is triggered via the given token and calls [StopAsync](/dotnet/api/microsoft.extensions.hosting.ihost.stopasync).</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.WaitForShutdownAsync();
        }

    }
}
```

### <a name="external-control"></a><span data-ttu-id="c4423-239">外部控件</span><span class="sxs-lookup"><span data-stu-id="c4423-239">External control</span></span>

<span data-ttu-id="c4423-240">使用可从外部调用的方法，能够实现主机的外部控件：</span><span class="sxs-lookup"><span data-stu-id="c4423-240">External control of the host can be achieved using methods that can be called externally:</span></span>

```csharp
public class Program
{
    private IHost _host;

    public Program()
    {
        _host = new HostBuilder()
            .Build();
    }

    public async Task StartAsync()
    {
        _host.StartAsync();
    }

    public async Task StopAsync()
    {
        using (_host)
        {
            await _host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

<span data-ttu-id="c4423-241">在 [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync) 开始时调用 [IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync)，在继续之前，会一直等待该操作完成。</span><span class="sxs-lookup"><span data-stu-id="c4423-241">[IHostLifetime.WaitForStartAsync](/dotnet/api/microsoft.extensions.hosting.ihostlifetime.waitforstartasync) is called at the start of [StartAsync](/dotnet/api/microsoft.extensions.hosting.ihost.startasync), which waits until it's complete before continuing.</span></span> <span data-ttu-id="c4423-242">它可用于延迟启动，直到外部事件发出信号。</span><span class="sxs-lookup"><span data-stu-id="c4423-242">This can be used to delay startup until signaled by an external event.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="c4423-243">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="c4423-243">IHostingEnvironment interface</span></span>

<span data-ttu-id="c4423-244">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) 提供有关应用托管环境的信息。</span><span class="sxs-lookup"><span data-stu-id="c4423-244">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) provides information about the app's hosting environment.</span></span> <span data-ttu-id="c4423-245">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="c4423-245">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class MyClass
{
    private readonly IHostingEnvironment _env;

    public MyClass(IHostingEnvironment env)
    {
        _env = env;
    }

    public void DoSomething()
    {
        var environmentName = _env.EnvironmentName;
    }
}
```

<span data-ttu-id="c4423-246">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="c4423-246">For more information, see [Use multiple environments](xref:fundamentals/environments).</span></span>

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="c4423-247">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="c4423-247">IApplicationLifetime interface</span></span>

<span data-ttu-id="c4423-248">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime) 允许启动后和关闭活动，包括正常关闭请求。</span><span class="sxs-lookup"><span data-stu-id="c4423-248">[IApplicationLifetime](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime) allows for post-startup and shutdown activities, including graceful shutdown requests.</span></span> <span data-ttu-id="c4423-249">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="c4423-249">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="c4423-250">取消标记</span><span class="sxs-lookup"><span data-stu-id="c4423-250">Cancellation Token</span></span> | <span data-ttu-id="c4423-251">触发条件</span><span class="sxs-lookup"><span data-stu-id="c4423-251">Triggered when&#8230;</span></span> |
| ------------------ | --------------------- |
| [<span data-ttu-id="c4423-252">ApplicationStarted</span><span class="sxs-lookup"><span data-stu-id="c4423-252">ApplicationStarted</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstarted) | <span data-ttu-id="c4423-253">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="c4423-253">The host has fully started.</span></span> |
| [<span data-ttu-id="c4423-254">ApplicationStopped</span><span class="sxs-lookup"><span data-stu-id="c4423-254">ApplicationStopped</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopped) | <span data-ttu-id="c4423-255">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="c4423-255">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="c4423-256">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="c4423-256">All requests should be processed.</span></span> <span data-ttu-id="c4423-257">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="c4423-257">Shutdown blocks until this event completes.</span></span> |
| [<span data-ttu-id="c4423-258">ApplicationStopping</span><span class="sxs-lookup"><span data-stu-id="c4423-258">ApplicationStopping</span></span>](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.applicationstopping) | <span data-ttu-id="c4423-259">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="c4423-259">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="c4423-260">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="c4423-260">Requests may still be processing.</span></span> <span data-ttu-id="c4423-261">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="c4423-261">Shutdown blocks until this event completes.</span></span> |

<span data-ttu-id="c4423-262">构造函数将 `IApplicationLifetime` 服务注入到任何类中。</span><span class="sxs-lookup"><span data-stu-id="c4423-262">Constructor-inject the `IApplicationLifetime` service into any class.</span></span> <span data-ttu-id="c4423-263">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)将构造函数注入到 `LifetimeEventsHostedService` 类（一个 `IHostedService` 实现）中，用于注册事件。</span><span class="sxs-lookup"><span data-stu-id="c4423-263">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses contructor injection into a `LifetimeEventsHostedService` class (an `IHostedService` implementation) to register the events.</span></span>

<span data-ttu-id="c4423-264">LifetimeEventsHostedService.cs：</span><span class="sxs-lookup"><span data-stu-id="c4423-264">*LifetimeEventsHostedService.cs*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

<span data-ttu-id="c4423-265">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) 请求应用终止。</span><span class="sxs-lookup"><span data-stu-id="c4423-265">[StopApplication](/dotnet/api/microsoft.extensions.hosting.iapplicationlifetime.stopapplication) requests termination of the app.</span></span> <span data-ttu-id="c4423-266">以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：</span><span class="sxs-lookup"><span data-stu-id="c4423-266">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="c4423-267">其他资源</span><span class="sxs-lookup"><span data-stu-id="c4423-267">Additional resources</span></span>

* [<span data-ttu-id="c4423-268">使用托管服务的后台任务</span><span class="sxs-lookup"><span data-stu-id="c4423-268">Background tasks with hosted services</span></span>](xref:fundamentals/host/hosted-services)
* [<span data-ttu-id="c4423-269">GitHub 上托管的存储库示例</span><span class="sxs-lookup"><span data-stu-id="c4423-269">Hosting repo samples on GitHub</span></span>](https://github.com/aspnet/Hosting/tree/release/2.1/samples)
