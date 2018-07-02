---
title: 在 ASP.NET Core 中使用多个环境
author: rick-anderson
description: 了解如何在 ASP.NET Core 应用中控制多个环境的应用行为。
ms.author: riande
ms.date: 06/21/2018
uid: fundamentals/environments
ms.openlocfilehash: 505f19d8b4df6e476b46a1fe7c49872d3c4acc1a
ms.sourcegitcommit: e22097b84d26a812cd1380a6b2d12c93e522c125
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314099"
---
# <a name="use-multiple-environments-in-aspnet-core"></a>在 ASP.NET Core 中使用多个环境

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core 基于使用环境变量的运行时环境配置应用行为。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="environments"></a>环境

ASP.NET Core 在应用启动时读取环境变量 `ASPNETCORE_ENVIRONMENT`，并将该值存储在 [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname) 中。 `ASPNETCORE_ENVIRONMENT` 可设置为任意值，但框架支持[三个值](/dotnet/api/microsoft.aspnetcore.hosting.environmentname)：[Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development)、[Staging](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging) 和 [Production](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production)。 如果未设置 `ASPNETCORE_ENVIRONMENT`，则默认为 `Production`。

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet)]

前面的代码：

* 当 `ASPNETCORE_ENVIRONMENT` 设置为 `Development` 时，调用 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 和 [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink)。
* 当 `ASPNETCORE_ENVIRONMENT` 的值设置为下列之一时，调用 [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler)：

    * `Staging`
    * `Production`
    * `Staging_2`

[环境标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)使用 `IHostingEnvironment.EnvironmentName` 的值来包含或排除元素中的标记：

[!code-cshtml[](environments/sample-snapshot/WebApp1/Pages/About.cshtml)]

在 Windows 和 macOS 上，环境变量和值不区分大小写。 默认情况下，Linux 环境变量和值要区分大小写。

### <a name="development"></a>开发

开发环境可以启用不应该在生产中公开的功能。 例如，ASP.NET Core 模板在开发环境中启用了[开发人员异常页](xref:fundamentals/error-handling#the-developer-exception-page)。

本地计算机开发环境可以在项目的 Properties\launchSettings.json 文件中设置。 在 launchSettings.json 中设置的环境值替代在系统环境中设置的值。

以下 JSON 显示 launchSettings.json 文件中的三个配置文件：

[!code-json[](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> launchSettings.json 中的 `applicationUrl` 属性可指定服务器 URL 的列表。 在列表中的 URL 之间使用分号：
>
> ```json
> "WebApplication1": {
>    "commandName": "Project",
>    "launchBrowser": true,
>    "applicationUrl": "https://localhost:5001;http://localhost:5000",
>    "environmentVariables": {
>      "ASPNETCORE_ENVIRONMENT": "Development"
>    }
> }
> ```

::: moniker-end

使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动应用时，使用具有 `"commandName": "Project"` 的第一个配置文件。 `commandName` 的值指定要启动的 Web 服务器。 `commandName` 可为以下任一项：

* IIS Express
* IIS
* 项目（启动 Kestrel 的项目）

使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动应用时：

* 如果可用，读取 launchSettings.json。 launchSettings.json 中的 `environmentVariables` 设置会替代环境变量。
* 此时显示承载环境。

以下输出显示了使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动的应用：

```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

Visual Studio“调试”选项卡提供 GUI 来编辑 launchSettings.json 文件：

![项目属性设置环境变量](environments/_static/project-properties-debug.png)

在 Web 服务器重新启动之前，对项目配置文件所做的更改可能不会生效。 必须重新启动 Kestrel 才能检测到对其环境所做的更改。

> [!WARNING]
> launchSettings.json 不应存储机密。 [机密管理器工具](xref:security/app-secrets)可用于存储本地开发的机密。

使用 [Visual Studio Code](https://code.visualstudio.com/) 时，可以在 .vscode/launch.json 文件中设置环境变量。 以下示例将环境设置为 `Development`：

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

使用与 Properties/launchSettings.json 相同的方法通过 `dotnet run` 启动应用时，不读取项目中的 .vscode/launch.json 文件。 在没有 launchSettings.json 文件的 Development 环境中启动应用时，需要使用环境变量设置环境或者将命令行参数设为 `dotnet run` 命令。

### <a name="production"></a>生产

Production 环境应配置为最大限度地提高安全性、性能和应用可靠性。 不同于开发的一些通用设置包括：

* 缓存。
* 客户端资源被捆绑和缩小，并可能从 CDN 提供。
* 已禁用诊断错误页。
* 已启用友好错误页。
* 已启用生产记录和监视。 例如，[Application Insights](/azure/application-insights/app-insights-asp-net-core)。

## <a name="setting-the-environment"></a>设置环境

为测试设置特定环境通常很有用。 如果未设置环境，默认值为 `Production`，这会禁用大多数调试功能。 设置环境的方法取决于操作系统。

### <a name="azure-app-service"></a>Azure 应用服务

若要在 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)中设置环境，请执行以下步骤：

1. 从“应用服务”边栏选项卡中选择应用。
1. 在“设置”组中，选择“应用程序设置”边栏选项卡。
1. 在“应用程序设置”区域中，选择“添加新设置”。
1. 在“输入名称”中提供 `ASPNETCORE_ENVIRONMENT`。 在“输入值”中提供环境（例如 `Staging`）。
1. 交换部署槽位时，如果希望环境设置保持当前槽位，请选中“槽位设置”复选框。 有关详细信息，请参阅 [Azure 文档：交换了哪些设置？](/azure/app-service/web-sites-staged-publishing)。
1. 选择边栏选项卡顶部的“保存”。

在 Azure 门户中添加、更改或删除应用设置（环境变量）后，Azure 应用服务自动重启应用。

### <a name="windows"></a>Windows

若要在使用 [dotnet run](/dotnet/core/tools/dotnet-run) 启动该应用时为当前会话设置 `ASPNETCORE_ENVIRONMENT`，则使用以下命令：

**命令提示符**

```console
set ASPNETCORE_ENVIRONMENT=Development
```

**PowerShell**

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

这些命令仅对当前窗口有效。 窗口关闭时，`ASPNETCORE_ENVIRONMENT` 设置将恢复为默认设置或计算机值。 若要在 Windows 中全局设置该值，请打开“控制面板” > “系统” > “高级系统设置”并添加或编辑 `ASPNETCORE_ENVIRONMENT` 值：

![系统高级属性](environments/_static/systemsetting_environment.png)

![ASPNET Core 环境变量](environments/_static/windows_aspnetcore_environment.png)

**web.config**

请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)主题的“设置环境变量”部分。

**每个 IIS 应用程序池**

若要为独立应用程序池中运行的单个应用设置环境变量（IIS 10.0+ 中支持此操作），请参阅[环境变量 &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。

### <a name="macos"></a>macOS

设置 macOS 的当前环境可在运行应用时完成：

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

或者，在运行应用前使用 `export` 设置环境：

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

在 .bashrc 或 .bash_profile 文件中设置计算机级环境变量。 使用任意文本编辑器编辑文件。 添加以下语句：

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a>Linux

对于 Linux 发行版，请在命令提示符中使用 `export` 命令进行基于会话的变量设置，并使用 bash_profile 文件进行计算机级环境设置。

### <a name="configuration-by-environment"></a>按环境配置

有关详细信息，请参阅[按环境配置](xref:fundamentals/configuration/index#configuration-by-environment)。

## <a name="environment-based-startup-class-and-methods"></a>基于环境的 Startup 类和方法

当 ASP.NET Core 应用启动时，[Startup 类](xref:fundamentals/startup)启动应用。 如果存在 `Startup{EnvironmentName}` 类，则为该 `EnvironmentName` 调用该类：

[!code-csharp[](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

[WebHostBuilder.UseStartup<TStartup>](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 替代配置节。

[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 和 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) 支持窗体 `Configure{EnvironmentName}` 和 `Configure{EnvironmentName}Services` 的环境特定版本：

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a>其他资源

* [应用程序启动](xref:fundamentals/startup)
* [配置](xref:fundamentals/configuration/index)
* [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)
