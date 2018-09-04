---
title: 在 Azure 应用服务上托管 ASP.NET Core
author: guardrex
description: 通过指向有用资源的链接，了解如何在 Azure 应用服务中托管 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 08/29/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: bc2a686c5ddc44fded135c9eed5caf676218773a
ms.sourcegitcommit: ecf2cd4e0613569025b28e12de3baa21d86d4258
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43312065"
---
# <a name="host-aspnet-core-on-azure-app-service"></a>在 Azure 应用服务上托管 ASP.NET Core

[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。

## <a name="useful-resources"></a>有用资源

Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。 两个有关托管 ASP.NET Core 应用的重要教程为：

[快速入门：在 Azure 中创建 ASP.NET Core Web 应用](/azure/app-service/app-service-web-get-started-dotnet)  
使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。

[快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用](/azure/app-service/containers/quickstart-dotnetcore)  
使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。

ASP.NET Core 文档中提供以下文章：

[使用 Visual Studio 发布到 Azure](xref:tutorials/publish-to-azure-webapp-using-vs)  
了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。

[使用 CLI 工具发布到 Azure](xref:tutorials/publish-to-azure-webapp-using-cli)  
了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。

[使用 Visual Studio 和 Git 持续部署到 Azure](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。

[使用 VSTS 持续部署到 Azure](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。

[Azure Web 应用沙盒](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a>应用程序配置

在 ASP.NET Core 2.0 或更高版本中，以下 NuGet 包可为部署到 Azure 应用服务的应用提供自动登录功能。

* [Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。 添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。
* [Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。
* [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。

如果面向 .NET Core 且引用 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)，则已经包括这些包。 这些包不包括在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中。 如果面向 .NET Framework 或引用 `Microsoft.AspNetCore.App` 元包，请引用单个登录包。

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a>使用 Azure 门户重写应用配置

“应用程序设置”边栏选项卡的“应用设置”区域允许你为应用设置环境变量。 可以通过[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)来使用环境变量。

当应用使用 [Web 主机](xref:fundamentals/host/web-host)并使用 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 构建主机时，配置主机的环境变量使用 `ASPNETCORE_` 前缀。 有关详细信息，请参阅 <xref:fundamentals/host/web-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。

当应用使用[通用主机](xref:fundamentals/host/generic-host)时，环境变量在默认情况下不会加载到应用的配置，且配置提供程序必须由开发人员添加。 在添加配置提供程序时，开发人员将确定环境变量前缀。 有关详细信息，请参阅 <xref:fundamentals/host/generic-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。

## <a name="proxy-server-and-load-balancer-scenarios"></a>代理服务器和负载均衡器方案

配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。 对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。 有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。

## <a name="monitoring-and-logging"></a>监视和日志记录

有关监视、日志记录和故障排除的信息，请参阅以下文章：

[如何：在 Azure 应用服务中监视应用](/azure/app-service/web-sites-monitor)  
了解如何查看应用和应用服务计划的配额和指标。

[在 Azure 应用服务中为应用启用诊断日志记录](/azure/app-service/web-sites-enable-diagnostic-log)  
了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。

[ASP.NET Core 中的错误处理简介](xref:fundamentals/error-handling)  
了解在 ASP.NET Core 应用中处理错误的常见方法。

[对 Azure 应用服务上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/azure-apps/troubleshoot)  
了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。

[Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)  
使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。

## <a name="data-protection-key-ring-and-deployment-slots"></a>数据保护密钥环和部署槽位

[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。 此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。 密钥不是静态保护的。 此文件夹向单个部署槽位中应用的所有实例提供密钥环。 各部署槽位（例如过渡槽和生成槽）不共享密钥环。

在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。 ASP.NET Cookie 中间件使用数据保护来保护其 cookie。 这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。 对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：

* Azure Blob 存储
* Azure Key Vault
* SQL 存储
* Redis 缓存

有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a>将 ASP.NET Core 预览版部署到 Azure 应用服务

可通过以下方法将 ASP.NET Core 预览应用部署到 Azure 应用服务：

* [安装预览站点扩展](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) -->
* [对用于容器的 Web 应用使用 Docker](#use-docker-with-web-apps-for-containers)

### <a name="install-the-preview-site-extension"></a>安装预览站点扩展

如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。

1. 从 Azure 门户导航到“应用服务”边栏选项卡。
1. 选择 Web 应用。
1. 在搜索框中键入“ex”或向下滚动管理部分列表，到达“开发工具”。
1. 选择“开发工具” > “扩展”。
1. 选择“添加”。
1. 从列表选择“ASP.NET Core &lt;x.y&gt; (x86) 运行时”扩展，其中 `<x.y>` 是 ASP.NET Core 预览版本（例如，ASP.NET Core 2.2 (x86) 运行时）。 x86 运行时适用于[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，这种部署依赖于 ASP.NET Core 模块的进程外托管。
1. 选择“确定”以接受法律条款。
1. 选择“确定”安装扩展。

操作完成时，即表示已安装最新的 .NET Core 预览版。 验证安装：

1. 选择“开发工具”下的“高级工具”。
1. 在“高级工具”边栏选项卡上，选择“转到”。
1. 选择“调试控制台” > “PowerShell”菜单项。
1. 从 PowerShell 命令提示符处执行以下命令。 在以下命令中，将 ASP.NET Core 运行时版本替换为 `<x.y>` ：

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x86\
   ```
   如果已安装的预览版运行时为 ASP.NET Core 2.2，则命令是：
   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x86\
   ```
   如果安装 x64 预览版运行时，该命令将返回`True`。

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> 对于在 A 系列计算机上或更高级托管层上托管的应用，可在“常规设置”下的“应用程序设置”中设置应用服务应用的平台体系结构 (x86/x64)。 如果应用在进程内模式下运行并且平台体系结构配置为 64 位 (x64)，则 ASP.NET Core 模块会使用 64 位预览版运行时（如存在）。 安装 ASP.NET Core &lt;x.y&gt; (x64) 运行时扩展 （例如，ASP.NET Core 2.2 (x64) 运行时）。
>
> 安装 x64 预览版运行时后，在 Kudu PowerShell 命令窗口中运行以下命令以验证该安装。 在以下命令中，将 ASP.NET Core 运行时版本替换为 `<x.y>` ：
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x64\
> ```
> 如果已安装的预览版运行时为 ASP.NET Core 2.2，则命令是：
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x64\
> ```
> 如果安装 x64 预览版运行时，该命令将返回`True`。

::: moniker-end

> [!NOTE]
> ASP.NET Core 扩展可为 Azure 应用服务上的 ASP.NET Core 启用附加功能，例如启用 Azure 日志记录。 从 Visual Studio 进行部署时，将自动安装该扩展。 如果未安装该扩展，请为应用安装它。

**通过 ARM 模板使用预览站点扩展**

如果使用 ARM 模板创建和部署应用，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。 例如:

[!code-json[Main](index/sample/arm.json?highlight=2)]

<!--
### Deploy the app self-contained

A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment. When deploying a self-contained app:

* The site doesn't need to be prepared.
* The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.

Self-contained apps are an option for all ASP.NET Core apps.
-->

### <a name="use-docker-with-web-apps-for-containers"></a>对用于容器的 Web 应用使用 Docker

[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的预览 Docker 映像。 这些映像可以用作基础映像。 按常规方法使用映像并部署到用于容器的 Web 应用。

## <a name="additional-resources"></a>其他资源

* [Web 应用概述（5 分钟概述视频）](/azure/app-service/app-service-web-overview)
* [Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [Azure 应用服务诊断概述](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。 以下是基础 IIS 技术的相关主题：

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [Microsoft TechNet 库：Windows Server](/windows-server/windows-server-versions)
