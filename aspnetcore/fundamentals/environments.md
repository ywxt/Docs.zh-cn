---
title: "在 ASP.NET Core 中使用多个环境"
author: rick-anderson
description: "了解 ASP.NET Core 如何为控制多个环境中的应用行为提供支持。"
manager: wpickett
ms.author: riande
ms.date: 12/25/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/environments
ms.openlocfilehash: b40ee9b1c6feae4942f05d22dab776d3cf6c26a0
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="working-with-multiple-environments"></a><span data-ttu-id="0627d-103">使用多个环境</span><span class="sxs-lookup"><span data-stu-id="0627d-103">Working with multiple environments</span></span>

<span data-ttu-id="0627d-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0627d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0627d-105">ASP.NET Core 提供通过环境变量在运行时针对设置应用程序行为的支持。</span><span class="sxs-lookup"><span data-stu-id="0627d-105">ASP.NET Core provides support for setting application behavior at runtime with environment variables.</span></span>

<span data-ttu-id="0627d-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0627d-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="0627d-107">环境</span><span class="sxs-lookup"><span data-stu-id="0627d-107">Environments</span></span>

<span data-ttu-id="0627d-108">ASP.NET Core 在应用程序启动时读取环境变量 `ASPNETCORE_ENVIRONMENT`，并将该值存储在 [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName) 中。</span><span class="sxs-lookup"><span data-stu-id="0627d-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at application startup and stores that value in [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName).</span></span> <span data-ttu-id="0627d-109">`ASPNETCORE_ENVIRONMENT` 可设置为任意值，但框架支持[三个值](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0)：[开发](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0)、[暂存](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0)和[生产](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)。</span><span class="sxs-lookup"><span data-stu-id="0627d-109">`ASPNETCORE_ENVIRONMENT` can be set to any value, but [three values](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0) are supported by the framework: [Development](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [Staging](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0), and [Production](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0).</span></span> <span data-ttu-id="0627d-110">如果未设置 `ASPNETCORE_ENVIRONMENT`，将默认为 `Production`。</span><span class="sxs-lookup"><span data-stu-id="0627d-110">If `ASPNETCORE_ENVIRONMENT` isn't set, it will default to `Production`.</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet)]

<span data-ttu-id="0627d-111">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="0627d-111">The preceding code:</span></span>

* <span data-ttu-id="0627d-112">当 `ASPNETCORE_ENVIRONMENT` 设置为 `Development` 时，调用 [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 和 [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_)。</span><span class="sxs-lookup"><span data-stu-id="0627d-112">Calls [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="0627d-113">当 `ASPNETCORE_ENVIRONMENT` 的值设置为下列之一时，调用 [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_)：</span><span class="sxs-lookup"><span data-stu-id="0627d-113">Calls [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="0627d-114">[环境标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)使用 `IHostingEnvironment.EnvironmentName` 的值用于包含或排除元素中的标记：</span><span class="sxs-lookup"><span data-stu-id="0627d-114">The [Environment Tag Helper ](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-html[Main](environments/sample/WebApp1/Pages/About.cshtml)]

<span data-ttu-id="0627d-115">注意：在 Windows 和 macOS 上，环境变量和值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0627d-115">Note: On Windows and macOS, environment variables and values are not case sensitive.</span></span> <span data-ttu-id="0627d-116">默认情况下，Linux 环境变量和值要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0627d-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="0627d-117">开发</span><span class="sxs-lookup"><span data-stu-id="0627d-117">Development</span></span>

<span data-ttu-id="0627d-118">开发环境可以启用不应该在生产中公开的功能。</span><span class="sxs-lookup"><span data-stu-id="0627d-118">The development environment can enable features that shouldn't be exposed in production.</span></span> <span data-ttu-id="0627d-119">例如，ASP.NET Core 模板在开发环境中启用了[开发人员异常页](xref:fundamentals/error-handling#the-developer-exception-page)。</span><span class="sxs-lookup"><span data-stu-id="0627d-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="0627d-120">本地计算机开发环境可以在项目的 Properties\launchSettings.json 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="0627d-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="0627d-121">在 launchSettings.json 中设置的环境值替代在系统环境中设置的值。</span><span class="sxs-lookup"><span data-stu-id="0627d-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="0627d-122">以下 JSON 显示 launchSettings.json 文件中的三个配置文件：</span><span class="sxs-lookup"><span data-stu-id="0627d-122">The following JSON shows three profiles from a *launchSettings.json* file:</span></span>

[!code-json[Main](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

<span data-ttu-id="0627d-123">使用 `dotnet run` 启动应用程序时，将使用具有 `"commandName": "Project"` 的第一个配置文件。</span><span class="sxs-lookup"><span data-stu-id="0627d-123">When the application is launched with `dotnet run`, the first profile with `"commandName": "Project"` will be used.</span></span> <span data-ttu-id="0627d-124">`commandName` 的值指定要启动的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="0627d-124">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="0627d-125">`commandName` 可以是以下之一：</span><span class="sxs-lookup"><span data-stu-id="0627d-125">`commandName` can be one of :</span></span>

* <span data-ttu-id="0627d-126">IIS Express</span><span class="sxs-lookup"><span data-stu-id="0627d-126">IIS Express</span></span>
* <span data-ttu-id="0627d-127">IIS</span><span class="sxs-lookup"><span data-stu-id="0627d-127">IIS</span></span>
* <span data-ttu-id="0627d-128">项目（启动 Kestrel 的项目）</span><span class="sxs-lookup"><span data-stu-id="0627d-128">Project (which launches Kestrel)</span></span>

<span data-ttu-id="0627d-129">当使用 `dotnet run` 启动应用时：</span><span class="sxs-lookup"><span data-stu-id="0627d-129">When an app is launched with `dotnet run`:</span></span>

* <span data-ttu-id="0627d-130">如果可用，读取 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="0627d-130">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="0627d-131">launchSettings.json 中的 `environmentVariables` 设置会替代环境变量。</span><span class="sxs-lookup"><span data-stu-id="0627d-131">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="0627d-132">此时显示承载环境。</span><span class="sxs-lookup"><span data-stu-id="0627d-132">The hosting environment is displayed.</span></span>


<span data-ttu-id="0627d-133">以下输出显示了使用 `dotnet run` 启动的应用：</span><span class="sxs-lookup"><span data-stu-id="0627d-133">The following output shows an app started with `dotnet run`:</span></span>
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="0627d-134">Visual Studio“调试”选项卡提供 GUI 来编辑 launchSettings.json 文件：</span><span class="sxs-lookup"><span data-stu-id="0627d-134">The Visual Studio **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![项目属性设置环境变量](environments/_static/project-properties-debug.png)

<span data-ttu-id="0627d-136">在 Web 服务器重新启动之前，对项目配置文件所做的更改可能不会生效。</span><span class="sxs-lookup"><span data-stu-id="0627d-136">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="0627d-137">必须重新启动 Kestrel 才能检测到对其环境所做的更改。</span><span class="sxs-lookup"><span data-stu-id="0627d-137">Kestrel must be restarted before it will detect changes made to its environment.</span></span>

>[!WARNING]
> <span data-ttu-id="0627d-138">launchSettings.json 不应存储机密。</span><span class="sxs-lookup"><span data-stu-id="0627d-138">*launchSettings.json* shouldn't store secrets.</span></span> <span data-ttu-id="0627d-139">[机密管理器工具](xref:security/app-secrets)可用于存储本地开发的机密。</span><span class="sxs-lookup"><span data-stu-id="0627d-139">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

### <a name="production"></a><span data-ttu-id="0627d-140">生产</span><span class="sxs-lookup"><span data-stu-id="0627d-140">Production</span></span>

<span data-ttu-id="0627d-141">生产环境应配置为最大限度地提高安全性、性能和应用程序可靠性。</span><span class="sxs-lookup"><span data-stu-id="0627d-141">The production environment should be configured to maximize security, performance, and application robustness.</span></span> <span data-ttu-id="0627d-142">生产环境可能具有的某些常见设置可能与开发环境不同，其中包括：</span><span class="sxs-lookup"><span data-stu-id="0627d-142">Some common settings that a production environment might have that would differ from development include:</span></span>

* <span data-ttu-id="0627d-143">缓存。</span><span class="sxs-lookup"><span data-stu-id="0627d-143">Caching.</span></span>
* <span data-ttu-id="0627d-144">客户端资源被捆绑和缩小，并可能从 CDN 提供。</span><span class="sxs-lookup"><span data-stu-id="0627d-144">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="0627d-145">已禁用诊断错误页。</span><span class="sxs-lookup"><span data-stu-id="0627d-145">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="0627d-146">已启用友好错误页。</span><span class="sxs-lookup"><span data-stu-id="0627d-146">Friendly error pages enabled.</span></span>
* <span data-ttu-id="0627d-147">已启用生产记录和监视。</span><span class="sxs-lookup"><span data-stu-id="0627d-147">Production logging and monitoring enabled.</span></span> <span data-ttu-id="0627d-148">例如，[Application Insights](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="0627d-148">For example, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="setting-the-environment"></a><span data-ttu-id="0627d-149">设置环境</span><span class="sxs-lookup"><span data-stu-id="0627d-149">Setting the environment</span></span>

<span data-ttu-id="0627d-150">为测试设置特定环境通常很有用。</span><span class="sxs-lookup"><span data-stu-id="0627d-150">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="0627d-151">如果未设置环境，默认值为 `Production`，这会禁用大多数调试功能。</span><span class="sxs-lookup"><span data-stu-id="0627d-151">If the environment isn't set, it will default to `Production` which disables most debugging features.</span></span>

<span data-ttu-id="0627d-152">设置环境的方法取决于操作系统。</span><span class="sxs-lookup"><span data-stu-id="0627d-152">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure"></a><span data-ttu-id="0627d-153">Azure</span><span class="sxs-lookup"><span data-stu-id="0627d-153">Azure</span></span>

<span data-ttu-id="0627d-154">对于 Azure 应用服务：</span><span class="sxs-lookup"><span data-stu-id="0627d-154">For Azure app service:</span></span>

* <span data-ttu-id="0627d-155">选择“应用程序设置”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="0627d-155">Select the **Application settings** blade.</span></span>
* <span data-ttu-id="0627d-156">将键和值添加到“应用设置”。</span><span class="sxs-lookup"><span data-stu-id="0627d-156">Add the key and value in **App settings**.</span></span>


### <a name="windows"></a><span data-ttu-id="0627d-157">Windows</span><span class="sxs-lookup"><span data-stu-id="0627d-157">Windows</span></span>
<span data-ttu-id="0627d-158">若要为当前会话设置 `ASPNETCORE_ENVIRONMENT`，如果应用使用 `dotnet run` 启动，则使用以下命令</span><span class="sxs-lookup"><span data-stu-id="0627d-158">To set the `ASPNETCORE_ENVIRONMENT` for the current session, if the app is started using `dotnet run`, the following commands are used</span></span>

<span data-ttu-id="0627d-159">**命令行**</span><span class="sxs-lookup"><span data-stu-id="0627d-159">**Command line**</span></span>
```
set ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="0627d-160">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0627d-160">**PowerShell**</span></span>
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="0627d-161">这些命令仅对当前窗口有效。</span><span class="sxs-lookup"><span data-stu-id="0627d-161">These commands take effect only for the current window.</span></span> <span data-ttu-id="0627d-162">窗口关闭时，ASPNETCORE_ENVIRONMENT 设置将恢复为默认设置或计算机值。</span><span class="sxs-lookup"><span data-stu-id="0627d-162">When the window is closed, the ASPNETCORE_ENVIRONMENT setting reverts to the default setting or machine value.</span></span> <span data-ttu-id="0627d-163">若要在 Windows 上全局设置该值，请打开“控制面板” > “系统” > “高级系统设置”并添加或编辑 `ASPNETCORE_ENVIRONMENT` 值。</span><span class="sxs-lookup"><span data-stu-id="0627d-163">In order to set the value globally on Windows open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value.</span></span>

![系统高级属性](environments/_static/systemsetting_environment.png)

![ASPNET Core 环境变量](environments/_static/windows_aspnetcore_environment.png)


<span data-ttu-id="0627d-166">**web.config**</span><span class="sxs-lookup"><span data-stu-id="0627d-166">**web.config**</span></span>

<span data-ttu-id="0627d-167">请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)主题的“设置环境变量”部分。</span><span class="sxs-lookup"><span data-stu-id="0627d-167">See the *Setting environment variables* section of the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) topic.</span></span>

<span data-ttu-id="0627d-168">**每个 IIS 应用程序池**</span><span class="sxs-lookup"><span data-stu-id="0627d-168">**Per IIS Application Pool**</span></span>

<span data-ttu-id="0627d-169">若要为独立应用程序池中运行的单个应用设置环境变量（IIS 10.0+ 中支持此操作），请参阅[环境变量 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。</span><span class="sxs-lookup"><span data-stu-id="0627d-169">To set environment variables for individual apps running in isolated Application Pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span>

### <a name="macos"></a><span data-ttu-id="0627d-170">macOS</span><span class="sxs-lookup"><span data-stu-id="0627d-170">macOS</span></span>
<span data-ttu-id="0627d-171">设置 macOS 的当前环境可在运行应用程序时完成；</span><span class="sxs-lookup"><span data-stu-id="0627d-171">Setting the current environment for macOS can be done in-line when running the application;</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
<span data-ttu-id="0627d-172">或在运行应用之前使用 `export` 对其进行设置。</span><span class="sxs-lookup"><span data-stu-id="0627d-172">or using `export` to set it prior to running the app.</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="0627d-173">在 .bashrc 或 .bash_profile 文件中设置计算机级别环境变量。</span><span class="sxs-lookup"><span data-stu-id="0627d-173">Machine level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="0627d-174">使用任何文本编辑器编辑文件并添加以下语句。</span><span class="sxs-lookup"><span data-stu-id="0627d-174">Edit the file using any text editor and add the following statment.</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="0627d-175">Linux</span><span class="sxs-lookup"><span data-stu-id="0627d-175">Linux</span></span>
<span data-ttu-id="0627d-176">对于 Linux 发行版，请在命令行中使用 `export` 命令进行基于会话的变量设置，并使用 bash_profile 文件进行计算机级别环境设置。</span><span class="sxs-lookup"><span data-stu-id="0627d-176">For Linux distros, use the `export` command at the command line for session based variable settings and *bash_profile* file for machine level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="0627d-177">按环境配置</span><span class="sxs-lookup"><span data-stu-id="0627d-177">Configuration by environment</span></span>

<span data-ttu-id="0627d-178">有关详细信息，请参阅[按环境配置](xref:fundamentals/configuration/index#configuration-by-environment)。</span><span class="sxs-lookup"><span data-stu-id="0627d-178">See [Configuration by environment](xref:fundamentals/configuration/index#configuration-by-environment) for more information.</span></span>

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="0627d-179">基于环境的 Startup 类和方法</span><span class="sxs-lookup"><span data-stu-id="0627d-179">Environment based Startup class and methods</span></span>

<span data-ttu-id="0627d-180">当 ASP.NET Core 应用启动时，[Startup 类](xref:fundamentals/startup)启动应用。</span><span class="sxs-lookup"><span data-stu-id="0627d-180">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="0627d-181">如果类 `Startup{EnvironmentName}` 存在，那么将为类 `EnvironmentName` 调用该类：</span><span class="sxs-lookup"><span data-stu-id="0627d-181">If a class `Startup{EnvironmentName}` exists, that class will be called for that `EnvironmentName`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

<span data-ttu-id="0627d-182">注意：调用 [WebHostBuilder.UseStartup<TStartup>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 替代配置节。</span><span class="sxs-lookup"><span data-stu-id="0627d-182">Note: Calling [WebHostBuilder.UseStartup<TStartup>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) overrides configuration sections.</span></span>

<span data-ttu-id="0627d-183">[Configure](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 和 [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) 支持窗体 `Configure{EnvironmentName}` 和 `Configure{EnvironmentName}Services` 的环境特定版本：</span><span class="sxs-lookup"><span data-stu-id="0627d-183">[Configure](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) support environment specific versions of the form `Configure{EnvironmentName}` and `Configure{EnvironmentName}Services`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a><span data-ttu-id="0627d-184">其他资源</span><span class="sxs-lookup"><span data-stu-id="0627d-184">Additional resources</span></span>

* [<span data-ttu-id="0627d-185">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="0627d-185">Application startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="0627d-186">配置</span><span class="sxs-lookup"><span data-stu-id="0627d-186">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="0627d-187">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="0627d-187">IHostingEnvironment.EnvironmentName</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
