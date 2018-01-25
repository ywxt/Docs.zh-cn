---
title: "使用 ASP.NET Core 中的多个环境"
author: rick-anderson
description: "了解如何 ASP.NET Core 提供支持用于跨多个环境中控制应用行为。"
ms.author: riande
manager: wpickett
ms.date: 12/25/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/environments
ms.openlocfilehash: 60a1543ce11d08490e6df0eb84f980672ecfe672
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="working-with-multiple-environments"></a>使用多个环境

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core 提供对使用环境变量在运行时设置应用程序行为的支持。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="environments"></a>环境

ASP.NET 核心读取环境变量`ASPNETCORE_ENVIRONMENT`在应用程序启动和中的值的存储[IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)。 `ASPNETCORE_ENVIRONMENT`可以将设置为任何值，但[三个值](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0)framework 支持：[开发](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0)，[过渡](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0)，和[生产](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)。 如果`ASPNETCORE_ENVIRONMENT`未设置，它将默认为`Production`。

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet)]

前面的代码：

* 调用[UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_)和[UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_)时`ASPNETCORE_ENVIRONMENT`设置为`Development`。
* 调用[UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_)时的值`ASPNETCORE_ENVIRONMENT`设置以下项之一：

    * `Staging`
    * `Production`
    * `Staging_2`

[环境标记帮助器](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)使用的值`IHostingEnvironment.EnvironmentName`用于包含或排除元素中的标记：

[!code-html[Main](environments/sample/WebApp1/Pages/About.cshtml)]

注意： 在 Windows 和 macOS 上，环境变量和值不区分大小写。 Linux 环境变量和值是**区分大小写**默认情况下。

### <a name="development"></a>开发

开发环境可以启用不应在生产中公开的功能。 例如，ASP.NET Core 模板启用[开发人员异常页](xref:fundamentals/error-handling#the-developer-exception-page)在开发环境中。

可以在设置用于本地计算机开发环境*Properties\launchSettings.json*项目文件。 在中设置环境值*launchSettings.json*重写系统环境中设置值。

下面的 XML 演示三个配置文件从*launchSettings.json*文件：

[!code-xml[Main](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

当应用程序启动与`dotnet run`，与第一个配置文件`"commandName": "Project"`将使用。 值`commandName`指定要启动的 web 服务器。 `commandName`可以是之一：

* IIS Express
* IIS
* 项目 （该操作将启动 Kestrel）

当应用程序启动与`dotnet run`:

* *launchSettings.json*读取如果可用。 `environmentVariables`中的设置*launchSettings.json*重写环境变量。
* 将显示该宿主环境。


下面的输出显示应用程序入门`dotnet run`:
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

Visual Studio**调试**选项卡提供了一个 GUI 以编辑*launchSettings.json*文件：

![项目属性设置环境变量](environments/_static/project-properties-debug.png)

在重新启动 web 服务器之前，对项目配置文件所做更改可能不会生效。 必须重启 kestrel，然后它将检测到其环境所做的更改。

>[!WARNING]
> *launchSettings.json*不应存储机密。 [机密管理器工具](xref:security/app-secrets)可以用于存储以进行本地开发的机密。

### <a name="production"></a>生产

生产环境应配置为最大程度提高安全性、 性能和应用程序的可靠性。 将不同于开发生产环境可能具有一些常见设置包括：

* 缓存。
* 客户端的资源捆绑在一起，缩减的并且可能从 CDN 提供。
* 禁用诊断错误页。
* 启用友好错误页。
* 生产日志记录和启用监视。 例如， [Application Insights](https://azure.microsoft.com/documentation/articles/app-insights-asp-net-five/)。

## <a name="setting-the-environment"></a>将环境设置

通常它可用于设置用于测试的特定环境。 如果未设置环境，它将默认为`Production`这将禁用大多数调试功能。

将环境设置的方法取决于操作系统。

### <a name="azure"></a>Azure

对 Azure app service:

* 选择**应用程序设置**边栏选项卡。
* 将键和值中**应用设置**。


### <a name="windows"></a>Windows
若要设置`ASPNETCORE_ENVIRONMENT`当前的会话中，如果应用程序将启动使用`dotnet run`，可以使用以下命令

**命令行**
```
set ASPNETCORE_ENVIRONMENT=Development
```
**PowerShell**
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

这些命令将仅为当前窗口的生效。 当窗口已关闭时，ASPNETCORE_ENVIRONMENT 设置将恢复为默认设置或计算机的值。 为了上 Windows 打开全局设置的值**控制面板** > **系统** > **高级系统设置**和添加或编辑`ASPNETCORE_ENVIRONMENT`值。

![高级属性的系统](environments/_static/systemsetting_environment.png)

![ASPNET 核心环境变量](environments/_static/windows_aspnetcore_environment.png)


**web.config**

请参阅*设置环境变量*部分[ASP.NET 核心模块配置引用](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)主题。

**每个 IIS 应用程序池**

若要设置对于在独立的应用程序池 （IIS 10.0 + 支持） 中运行的单个应用程序的环境变量，请参阅*AppCmd.exe 命令*部分[环境变量\<environmentVariables >](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe)主题。

### <a name="macos"></a>macOS
设置 macOS 的当前环境，可以进行串联时运行该应用程序;

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
也可以使用`export`若要在运行应用程序之前设置它。

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
设置计算机级别的环境变量*.bashrc*或*.bash_profile*文件。 使用任何文本编辑器编辑该文件并添加以下语句。

```
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a>Linux
对于 Linux 发行版本，使用`export`基于会话的变量设置在命令行命令和*bash_profile*机级别的环境设置的文件。

### <a name="configuration-by-environment"></a>按环境配置

请参阅[由环境配置](xref:fundamentals/configuration/index#configuration-by-environment)有关详细信息。

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a>环境基于 Startup 类和方法

当 ASP.NET Core 应用启动后时， [Startup 类](xref:fundamentals/startup)启动应用程序。 如果一个类`Startup{EnvironmentName}`存在，将该调用类`EnvironmentName`:

[!code-csharp[Main](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

注意： 调用[WebHostBuilder.UseStartup<TStartup> ](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)重写配置节。

[配置](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_)和[ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0)支持环境特定版本的表单`Configure{EnvironmentName}`和`Configure{EnvironmentName}Services`:

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a>其他资源

* [应用程序启动](xref:fundamentals/startup)
* [配置](xref:fundamentals/configuration/index)
* [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
