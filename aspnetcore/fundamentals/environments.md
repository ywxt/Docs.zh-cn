---
title: 在 ASP.NET Core 中使用多个环境
author: rick-anderson
description: 了解如何在 ASP.NET Core 应用中控制多个环境的应用行为。
ms.author: riande
ms.date: 07/03/2018
uid: fundamentals/environments
ms.openlocfilehash: 8983a0ce81beb16d68c799d30bfbfce6e7b693b1
ms.sourcegitcommit: 18339e3cb5a891a3ca36d8146fa83cf91c32e707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433943"
---
# <a name="use-multiple-environments-in-aspnet-core"></a><span data-ttu-id="b27a7-103">在 ASP.NET Core 中使用多个环境</span><span class="sxs-lookup"><span data-stu-id="b27a7-103">Use multiple environments in ASP.NET Core</span></span>

<span data-ttu-id="b27a7-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b27a7-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="b27a7-105">ASP.NET Core 基于使用环境变量的运行时环境配置应用行为。</span><span class="sxs-lookup"><span data-stu-id="b27a7-105">ASP.NET Core configures app behavior based on the runtime environment using an environment variable.</span></span>

<span data-ttu-id="b27a7-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="b27a7-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="b27a7-107">环境</span><span class="sxs-lookup"><span data-stu-id="b27a7-107">Environments</span></span>

<span data-ttu-id="b27a7-108">ASP.NET Core 在应用启动时读取环境变量 `ASPNETCORE_ENVIRONMENT`，并将该值存储在 [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname) 中。</span><span class="sxs-lookup"><span data-stu-id="b27a7-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at app startup and stores the value in [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname).</span></span> <span data-ttu-id="b27a7-109">`ASPNETCORE_ENVIRONMENT` 可设置为任意值，但框架支持[三个值](/dotnet/api/microsoft.aspnetcore.hosting.environmentname)：[Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development)、[Staging](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging) 和 [Production](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-109">You can set `ASPNETCORE_ENVIRONMENT` to any value, but [three values](/dotnet/api/microsoft.aspnetcore.hosting.environmentname) are supported by the framework: [Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [Staging](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging), and [Production](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production).</span></span> <span data-ttu-id="b27a7-110">如果未设置 `ASPNETCORE_ENVIRONMENT`，则默认为 `Production`。</span><span class="sxs-lookup"><span data-stu-id="b27a7-110">If `ASPNETCORE_ENVIRONMENT` isn't set, it defaults to `Production`.</span></span>

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet)]

<span data-ttu-id="b27a7-111">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="b27a7-111">The preceding code:</span></span>

* <span data-ttu-id="b27a7-112">当 `ASPNETCORE_ENVIRONMENT` 设置为 `Development` 时，调用 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 和 [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-112">Calls [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) and [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="b27a7-113">当 `ASPNETCORE_ENVIRONMENT` 的值设置为下列之一时，调用 [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler)：</span><span class="sxs-lookup"><span data-stu-id="b27a7-113">Calls [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="b27a7-114">[环境标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)使用 `IHostingEnvironment.EnvironmentName` 的值来包含或排除元素中的标记：</span><span class="sxs-lookup"><span data-stu-id="b27a7-114">The [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-cshtml[](environments/sample-snapshot/EnvironmentsSample/Pages/About.cshtml)]

<span data-ttu-id="b27a7-115">在 Windows 和 macOS 上，环境变量和值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b27a7-115">On Windows and macOS, environment variables and values aren't case sensitive.</span></span> <span data-ttu-id="b27a7-116">默认情况下，Linux 环境变量和值要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b27a7-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="b27a7-117">开发</span><span class="sxs-lookup"><span data-stu-id="b27a7-117">Development</span></span>

<span data-ttu-id="b27a7-118">开发环境可以启用不应该在生产中公开的功能。</span><span class="sxs-lookup"><span data-stu-id="b27a7-118">The development environment can enable features that shouldn't be exposed in production.</span></span> <span data-ttu-id="b27a7-119">例如，ASP.NET Core 模板在开发环境中启用了[开发人员异常页](xref:fundamentals/error-handling#the-developer-exception-page)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="b27a7-120">本地计算机开发环境可以在项目的 Properties\launchSettings.json 文件中设置。</span><span class="sxs-lookup"><span data-stu-id="b27a7-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="b27a7-121">在 launchSettings.json 中设置的环境值替代在系统环境中设置的值。</span><span class="sxs-lookup"><span data-stu-id="b27a7-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="b27a7-122">以下 JSON 显示 launchSettings.json 文件中的三个配置文件：</span><span class="sxs-lookup"><span data-stu-id="b27a7-122">The following JSON shows three profiles from a *launchSettings.json* file:</span></span>

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:54339/",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      }
    },
    "EnvironmentsSample": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:54340/"
    },
    "Kestrel Staging": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_My_Environment": "1",
        "ASPNETCORE_DETAILEDERRORS": "1",
        "ASPNETCORE_ENVIRONMENT": "Staging"
      },
      "applicationUrl": "http://localhost:51997/"
    }
  }
}
```

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="b27a7-123">launchSettings.json 中的 `applicationUrl` 属性可指定服务器 URL 的列表。</span><span class="sxs-lookup"><span data-stu-id="b27a7-123">The `applicationUrl` property in *launchSettings.json* can specify a list of server URLs.</span></span> <span data-ttu-id="b27a7-124">在列表中的 URL 之间使用分号：</span><span class="sxs-lookup"><span data-stu-id="b27a7-124">Use a semicolon between the URLs in the list:</span></span>
>
> ```json
> "EnvironmentsSample": {
>    "commandName": "Project",
>    "launchBrowser": true,
>    "applicationUrl": "https://localhost:5001;http://localhost:5000",
>    "environmentVariables": {
>      "ASPNETCORE_ENVIRONMENT": "Development"
>    }
> }
> ```

::: moniker-end

<span data-ttu-id="b27a7-125">使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动应用时，使用具有 `"commandName": "Project"` 的第一个配置文件。</span><span class="sxs-lookup"><span data-stu-id="b27a7-125">When the app is launched with [dotnet run](/dotnet/core/tools/dotnet-run), the first profile with `"commandName": "Project"` is used.</span></span> <span data-ttu-id="b27a7-126">`commandName` 的值指定要启动的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b27a7-126">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="b27a7-127">`commandName` 可为以下任一项：</span><span class="sxs-lookup"><span data-stu-id="b27a7-127">`commandName` can be any one of the following:</span></span>

* <span data-ttu-id="b27a7-128">IIS Express</span><span class="sxs-lookup"><span data-stu-id="b27a7-128">IIS Express</span></span>
* <span data-ttu-id="b27a7-129">IIS</span><span class="sxs-lookup"><span data-stu-id="b27a7-129">IIS</span></span>
* <span data-ttu-id="b27a7-130">Project（启动 Kestrel 的项目）</span><span class="sxs-lookup"><span data-stu-id="b27a7-130">Project (which launches Kestrel)</span></span>

<span data-ttu-id="b27a7-131">使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动应用时：</span><span class="sxs-lookup"><span data-stu-id="b27a7-131">When an app is launched with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

* <span data-ttu-id="b27a7-132">如果可用，读取 launchSettings.json。</span><span class="sxs-lookup"><span data-stu-id="b27a7-132">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="b27a7-133">launchSettings.json 中的 `environmentVariables` 设置会替代环境变量。</span><span class="sxs-lookup"><span data-stu-id="b27a7-133">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="b27a7-134">此时显示承载环境。</span><span class="sxs-lookup"><span data-stu-id="b27a7-134">The hosting environment is displayed.</span></span>

<span data-ttu-id="b27a7-135">以下输出显示了使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动的应用：</span><span class="sxs-lookup"><span data-stu-id="b27a7-135">The following output shows an app started with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

```bash
PS C:\Websites\EnvironmentsSample> dotnet run
Using launch settings from C:\Websites\EnvironmentsSample\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Websites\EnvironmentsSample
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="b27a7-136">Visual Studio 项目属性“调试”选项卡提供 GUI 来编辑 launchSettings.json 文件：</span><span class="sxs-lookup"><span data-stu-id="b27a7-136">The Visual Studio project properties **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![项目属性设置环境变量](environments/_static/project-properties-debug.png)

<span data-ttu-id="b27a7-138">在 Web 服务器重新启动之前，对项目配置文件所做的更改可能不会生效。</span><span class="sxs-lookup"><span data-stu-id="b27a7-138">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="b27a7-139">必须重新启动 Kestrel 才能检测到对其环境所做的更改。</span><span class="sxs-lookup"><span data-stu-id="b27a7-139">Kestrel must be restarted before it can detect changes made to its environment.</span></span>

> [!WARNING]
> <span data-ttu-id="b27a7-140">launchSettings.json 不应存储机密。</span><span class="sxs-lookup"><span data-stu-id="b27a7-140">*launchSettings.json* shouldn't store secrets.</span></span> <span data-ttu-id="b27a7-141">[机密管理器工具](xref:security/app-secrets)可用于存储本地开发的机密。</span><span class="sxs-lookup"><span data-stu-id="b27a7-141">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

<span data-ttu-id="b27a7-142">使用 [Visual Studio Code](https://code.visualstudio.com/) 时，可以在 .vscode/launch.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="b27a7-142">When using [Visual Studio Code](https://code.visualstudio.com/), environment variables can be set in the *.vscode/launch.json* file.</span></span> <span data-ttu-id="b27a7-143">以下示例将环境设置为 `Development`：</span><span class="sxs-lookup"><span data-stu-id="b27a7-143">The following example sets the environment to `Development`:</span></span>

```json
{
   "version": "0.2.0",
   "configurations": [
        {
            "name": ".NET Core Launch (web)",

            ... additional VS Code configuration settings ...

            "env": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    ]
}
```

<span data-ttu-id="b27a7-144">使用与 Properties/launchSettings.json 相同的方法通过 `dotnet run` 启动应用时，不读取项目中的 .vscode/launch.json 文件。</span><span class="sxs-lookup"><span data-stu-id="b27a7-144">A *.vscode/launch.json* file in the project isn't read when starting the app with `dotnet run` in the same way as *Properties/launchSettings.json*.</span></span> <span data-ttu-id="b27a7-145">在没有 launchSettings.json 文件的 Development 环境中启动应用时，需要使用环境变量设置环境或者将命令行参数设为 `dotnet run` 命令。</span><span class="sxs-lookup"><span data-stu-id="b27a7-145">When launching an app in development that doesn't have a *launchSettings.json* file, either set the environment with an environment variable or a command-line argument to the `dotnet run` command.</span></span>

### <a name="production"></a><span data-ttu-id="b27a7-146">生产</span><span class="sxs-lookup"><span data-stu-id="b27a7-146">Production</span></span>

<span data-ttu-id="b27a7-147">Production 环境应配置为最大限度地提高安全性、性能和应用可靠性。</span><span class="sxs-lookup"><span data-stu-id="b27a7-147">The production environment should be configured to maximize security, performance, and app robustness.</span></span> <span data-ttu-id="b27a7-148">不同于开发的一些通用设置包括：</span><span class="sxs-lookup"><span data-stu-id="b27a7-148">Some common settings that differ from development include:</span></span>

* <span data-ttu-id="b27a7-149">缓存。</span><span class="sxs-lookup"><span data-stu-id="b27a7-149">Caching.</span></span>
* <span data-ttu-id="b27a7-150">客户端资源被捆绑和缩小，并可能从 CDN 提供。</span><span class="sxs-lookup"><span data-stu-id="b27a7-150">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="b27a7-151">已禁用诊断错误页。</span><span class="sxs-lookup"><span data-stu-id="b27a7-151">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="b27a7-152">已启用友好错误页。</span><span class="sxs-lookup"><span data-stu-id="b27a7-152">Friendly error pages enabled.</span></span>
* <span data-ttu-id="b27a7-153">已启用生产记录和监视。</span><span class="sxs-lookup"><span data-stu-id="b27a7-153">Production logging and monitoring enabled.</span></span> <span data-ttu-id="b27a7-154">例如，[Application Insights](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-154">For example, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="set-the-environment"></a><span data-ttu-id="b27a7-155">设置环境</span><span class="sxs-lookup"><span data-stu-id="b27a7-155">Set the environment</span></span>

<span data-ttu-id="b27a7-156">为测试设置特定环境通常很有用。</span><span class="sxs-lookup"><span data-stu-id="b27a7-156">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="b27a7-157">如果未设置环境，默认值为 `Production`，这会禁用大多数调试功能。</span><span class="sxs-lookup"><span data-stu-id="b27a7-157">If the environment isn't set, it defaults to `Production`, which disables most debugging features.</span></span> <span data-ttu-id="b27a7-158">设置环境的方法取决于操作系统。</span><span class="sxs-lookup"><span data-stu-id="b27a7-158">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure-app-service"></a><span data-ttu-id="b27a7-159">Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="b27a7-159">Azure App Service</span></span>

<span data-ttu-id="b27a7-160">若要在 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)中设置环境，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="b27a7-160">To set the environment in [Azure App Service](https://azure.microsoft.com/services/app-service/), perform the following steps:</span></span>

1. <span data-ttu-id="b27a7-161">从“应用服务”边栏选项卡中选择应用。</span><span class="sxs-lookup"><span data-stu-id="b27a7-161">Select the app from the **App Services** blade.</span></span>
1. <span data-ttu-id="b27a7-162">在“设置”组中，选择“应用程序设置”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="b27a7-162">In the **SETTINGS** group, select the **Application settings** blade.</span></span>
1. <span data-ttu-id="b27a7-163">在“应用程序设置”区域中，选择“添加新设置”。</span><span class="sxs-lookup"><span data-stu-id="b27a7-163">In the **Application settings** area, select **Add new setting**.</span></span>
1. <span data-ttu-id="b27a7-164">在“输入名称”中提供 `ASPNETCORE_ENVIRONMENT`。</span><span class="sxs-lookup"><span data-stu-id="b27a7-164">For **Enter a name**, provide `ASPNETCORE_ENVIRONMENT`.</span></span> <span data-ttu-id="b27a7-165">在“输入值”中提供环境（例如 `Staging`）。</span><span class="sxs-lookup"><span data-stu-id="b27a7-165">For **Enter a value**, provide the environment (for example, `Staging`).</span></span>
1. <span data-ttu-id="b27a7-166">交换部署槽位时，如果希望环境设置保持当前槽位，请选中“槽位设置”复选框。</span><span class="sxs-lookup"><span data-stu-id="b27a7-166">Select the **Slot Setting** check box if you wish the environment setting to remain with the current slot when deployment slots are swapped.</span></span> <span data-ttu-id="b27a7-167">有关详细信息，请参阅 [Azure 文档：交换了哪些设置？](/azure/app-service/web-sites-staged-publishing)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-167">For more information, see [Azure Documentation: Which settings are swapped?](/azure/app-service/web-sites-staged-publishing).</span></span>
1. <span data-ttu-id="b27a7-168">选择边栏选项卡顶部的“保存”。</span><span class="sxs-lookup"><span data-stu-id="b27a7-168">Select **Save** at the top of the blade.</span></span>

<span data-ttu-id="b27a7-169">在 Azure 门户中添加、更改或删除应用设置（环境变量）后，Azure 应用服务自动重启应用。</span><span class="sxs-lookup"><span data-stu-id="b27a7-169">Azure App Service automatically restarts the app after an app setting (environment variable) is added, changed, or deleted in the Azure portal.</span></span>

### <a name="windows"></a><span data-ttu-id="b27a7-170">Windows</span><span class="sxs-lookup"><span data-stu-id="b27a7-170">Windows</span></span>

<span data-ttu-id="b27a7-171">若要在使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动该应用时为当前会话设置 `ASPNETCORE_ENVIRONMENT`，则使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="b27a7-171">To set the `ASPNETCORE_ENVIRONMENT` for the current session when the app is started using [dotnet run](/dotnet/core/tools/dotnet-run), the following commands are used:</span></span>

<span data-ttu-id="b27a7-172">**命令提示符**</span><span class="sxs-lookup"><span data-stu-id="b27a7-172">**Command prompt**</span></span>

```console
set ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="b27a7-173">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b27a7-173">**PowerShell**</span></span>

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="b27a7-174">这些命令仅对当前窗口有效。</span><span class="sxs-lookup"><span data-stu-id="b27a7-174">These commands only take effect for the current window.</span></span> <span data-ttu-id="b27a7-175">窗口关闭时，`ASPNETCORE_ENVIRONMENT` 设置将恢复为默认设置或计算机值。</span><span class="sxs-lookup"><span data-stu-id="b27a7-175">When the window is closed, the `ASPNETCORE_ENVIRONMENT` setting reverts to the default setting or machine value.</span></span> <span data-ttu-id="b27a7-176">若要在 Windows 中全局设置该值，请打开“控制面板” > “系统” > “高级系统设置”并添加或编辑 `ASPNETCORE_ENVIRONMENT` 值：</span><span class="sxs-lookup"><span data-stu-id="b27a7-176">To set the value globally in Windows, open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value:</span></span>

![系统高级属性](environments/_static/systemsetting_environment.png)

![ASPNET Core 环境变量](environments/_static/windows_aspnetcore_environment.png)

<span data-ttu-id="b27a7-179">**web.config**</span><span class="sxs-lookup"><span data-stu-id="b27a7-179">**web.config**</span></span>

<span data-ttu-id="b27a7-180">请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)主题的“设置环境变量”部分。</span><span class="sxs-lookup"><span data-stu-id="b27a7-180">See the *Setting environment variables* section of the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) topic.</span></span>

<span data-ttu-id="b27a7-181">**每个 IIS 应用程序池**</span><span class="sxs-lookup"><span data-stu-id="b27a7-181">**Per IIS Application Pool**</span></span>

<span data-ttu-id="b27a7-182">若要为独立应用程序池中运行的单个应用设置环境变量（IIS 10.0+ 中支持此操作），请参阅[环境变量 &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。</span><span class="sxs-lookup"><span data-stu-id="b27a7-182">To set environment variables for individual apps running in isolated Application Pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span>

### <a name="macos"></a><span data-ttu-id="b27a7-183">macOS</span><span class="sxs-lookup"><span data-stu-id="b27a7-183">macOS</span></span>

<span data-ttu-id="b27a7-184">设置 macOS 的当前环境可在运行应用时完成：</span><span class="sxs-lookup"><span data-stu-id="b27a7-184">Setting the current environment for macOS can be performed in-line when running the app:</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

<span data-ttu-id="b27a7-185">或者，在运行应用前使用 `export` 设置环境：</span><span class="sxs-lookup"><span data-stu-id="b27a7-185">Alternatively, set the environment with `export` prior to running the app:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="b27a7-186">在 .bashrc 或 .bash_profile 文件中设置计算机级环境变量。</span><span class="sxs-lookup"><span data-stu-id="b27a7-186">Machine-level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="b27a7-187">使用任意文本编辑器编辑文件。</span><span class="sxs-lookup"><span data-stu-id="b27a7-187">Edit the file using any text editor.</span></span> <span data-ttu-id="b27a7-188">添加以下语句：</span><span class="sxs-lookup"><span data-stu-id="b27a7-188">Add the following statement:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="b27a7-189">Linux</span><span class="sxs-lookup"><span data-stu-id="b27a7-189">Linux</span></span>

<span data-ttu-id="b27a7-190">对于 Linux 发行版，请在命令提示符中使用 `export` 命令进行基于会话的变量设置，并使用 bash_profile 文件进行计算机级环境设置。</span><span class="sxs-lookup"><span data-stu-id="b27a7-190">For Linux distros, use the `export` command at a command prompt for session-based variable settings and *bash_profile* file for machine-level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="b27a7-191">按环境配置</span><span class="sxs-lookup"><span data-stu-id="b27a7-191">Configuration by environment</span></span>

<span data-ttu-id="b27a7-192">有关详细信息，请参阅[按环境配置](xref:fundamentals/configuration/index#configuration-by-environment)。</span><span class="sxs-lookup"><span data-stu-id="b27a7-192">See [Configuration by environment](xref:fundamentals/configuration/index#configuration-by-environment) for more information.</span></span>

## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="b27a7-193">基于环境的 Startup 类和方法</span><span class="sxs-lookup"><span data-stu-id="b27a7-193">Environment-based Startup class and methods</span></span>

<span data-ttu-id="b27a7-194">当 ASP.NET Core 应用启动时，[Startup 类](xref:fundamentals/startup)启动应用。</span><span class="sxs-lookup"><span data-stu-id="b27a7-194">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="b27a7-195">如果存在 `Startup{EnvironmentName}` 类，则为该 `EnvironmentName` 调用该类：</span><span class="sxs-lookup"><span data-stu-id="b27a7-195">If a `Startup{EnvironmentName}` class exists, the class is called for that `EnvironmentName`:</span></span>

[!code-csharp[](environments/sample/EnvironmentsSample/StartupDev.cs?name=snippet&highlight=1)]

<span data-ttu-id="b27a7-196">[WebHostBuilder.UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 替代配置部分。</span><span class="sxs-lookup"><span data-stu-id="b27a7-196">[WebHostBuilder.UseStartup&lt;TStartup&gt;](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) overrides configuration sections.</span></span>

<span data-ttu-id="b27a7-197">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 支持窗体 `Configure{EnvironmentName}` 和 `Configure{EnvironmentName}Services` 的环境特定版本：</span><span class="sxs-lookup"><span data-stu-id="b27a7-197">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) support environment-specific versions of the form `Configure{EnvironmentName}` and `Configure{EnvironmentName}Services`:</span></span>

[!code-csharp[](environments/sample/EnvironmentsSample/Startup.cs?name=snippet_all&highlight=15,51)]

## <a name="additional-resources"></a><span data-ttu-id="b27a7-198">其他资源</span><span class="sxs-lookup"><span data-stu-id="b27a7-198">Additional resources</span></span>

* <xref:fundamentals/startup>
* <xref:fundamentals/configuration/index>
* [<span data-ttu-id="b27a7-199">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="b27a7-199">IHostingEnvironment.EnvironmentName</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)
