---
title: 在 Azure 应用服务上托管 ASP.NET Core
author: guardrex
description: 通过指向有用资源的链接，了解如何在 Azure 应用服务中托管 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 07/24/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: 42775bf4d3e88893260a5973f6f7bc9d3a006b5a
ms.sourcegitcommit: 25150f4398de83132965a89f12d3a030f6cce48d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2018
ms.locfileid: "42927823"
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="175c4-103">在 Azure 应用服务上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="175c4-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="175c4-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="175c4-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="175c4-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="175c4-105">Useful resources</span></span>

<span data-ttu-id="175c4-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="175c4-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="175c4-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="175c4-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="175c4-108">快速入门：在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="175c4-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="175c4-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="175c4-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="175c4-110">快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="175c4-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="175c4-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="175c4-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="175c4-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="175c4-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="175c4-113">使用 Visual Studio 发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="175c4-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="175c4-114">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="175c4-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="175c4-115">使用 CLI 工具发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="175c4-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="175c4-116">了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="175c4-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="175c4-117">使用 Visual Studio 和 Git 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="175c4-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="175c4-118">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="175c4-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="175c4-119">使用 VSTS 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="175c4-119">Continuous deployment to Azure with VSTS</span></span>](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
<span data-ttu-id="175c4-120">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="175c4-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="175c4-121">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="175c4-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="175c4-122">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="175c4-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a><span data-ttu-id="175c4-123">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="175c4-123">Application configuration</span></span>

<span data-ttu-id="175c4-124">在 ASP.NET Core 2.0 或更高版本中，以下 NuGet 包可为部署到 Azure 应用服务的应用提供自动登录功能。</span><span class="sxs-lookup"><span data-stu-id="175c4-124">In ASP.NET Core 2.0 or later, the following NuGet packages provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="175c4-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="175c4-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="175c4-126">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="175c4-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="175c4-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="175c4-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="175c4-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="175c4-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="175c4-129">如果面向 .NET Core 且引用 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)，则已经包括这些包。</span><span class="sxs-lookup"><span data-stu-id="175c4-129">If targeting .NET Core and referencing the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage), the packages are already included.</span></span> <span data-ttu-id="175c4-130">这些包不包括在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中。</span><span class="sxs-lookup"><span data-stu-id="175c4-130">The packages are absent from the newer [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="175c4-131">如果面向 .NET Framework 或引用 `Microsoft.AspNetCore.App` 元包，请引用单个登录包。</span><span class="sxs-lookup"><span data-stu-id="175c4-131">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, reference the individual logging packages.</span></span>

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="175c4-132">使用 Azure 门户重写应用配置</span><span class="sxs-lookup"><span data-stu-id="175c4-132">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="175c4-133">“应用程序设置”边栏选项卡的“应用设置”区域允许你为应用设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="175c4-133">The **App Settings** area of the **Application settings** blade permits you to set environment variables for the app.</span></span> <span data-ttu-id="175c4-134">可以通过[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)来使用环境变量。</span><span class="sxs-lookup"><span data-stu-id="175c4-134">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="175c4-135">当应用使用 [Web 主机](xref:fundamentals/host/web-host)并使用 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 构建主机时，配置主机的环境变量使用 `ASPNETCORE_` 前缀。</span><span class="sxs-lookup"><span data-stu-id="175c4-135">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="175c4-136">有关详细信息，请参阅 <xref:fundamentals/host/web-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="175c4-136">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="175c4-137">当应用使用[通用主机](xref:fundamentals/host/generic-host)时，环境变量在默认情况下不会加载到应用的配置，且配置提供程序必须由开发人员添加。</span><span class="sxs-lookup"><span data-stu-id="175c4-137">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="175c4-138">在添加配置提供程序时，开发人员将确定环境变量前缀。</span><span class="sxs-lookup"><span data-stu-id="175c4-138">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="175c4-139">有关详细信息，请参阅 <xref:fundamentals/host/generic-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="175c4-139">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="175c4-140">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="175c4-140">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="175c4-141">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="175c4-141">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="175c4-142">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="175c4-142">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="175c4-143">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="175c4-143">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="175c4-144">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="175c4-144">Monitoring and logging</span></span>

<span data-ttu-id="175c4-145">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="175c4-145">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="175c4-146">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="175c4-146">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="175c4-147">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="175c4-147">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="175c4-148">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="175c4-148">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="175c4-149">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="175c4-149">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="175c4-150">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="175c4-150">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="175c4-151">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="175c4-151">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="175c4-152">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="175c4-152">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="175c4-153">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="175c4-153">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="175c4-154">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="175c4-154">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="175c4-155">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="175c4-155">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="175c4-156">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="175c4-156">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="175c4-157">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="175c4-157">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="175c4-158">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="175c4-158">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="175c4-159">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="175c4-159">Keys aren't protected at rest.</span></span> <span data-ttu-id="175c4-160">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="175c4-160">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="175c4-161">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="175c4-161">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="175c4-162">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="175c4-162">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="175c4-163">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="175c4-163">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="175c4-164">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="175c4-164">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="175c4-165">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="175c4-165">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="175c4-166">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="175c4-166">Azure Blob Storage</span></span>
* <span data-ttu-id="175c4-167">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="175c4-167">Azure Key Vault</span></span>
* <span data-ttu-id="175c4-168">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="175c4-168">SQL store</span></span>
* <span data-ttu-id="175c4-169">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="175c4-169">Redis cache</span></span>

<span data-ttu-id="175c4-170">有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。</span><span class="sxs-lookup"><span data-stu-id="175c4-170">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="175c4-171">将 ASP.NET Core 预览版部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="175c4-171">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="175c4-172">可通过以下方法将 ASP.NET Core 预览应用部署到 Azure 应用服务：</span><span class="sxs-lookup"><span data-stu-id="175c4-172">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* <span data-ttu-id="175c4-173">[安装预览站点扩展](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span><span class="sxs-lookup"><span data-stu-id="175c4-173">[Install the preview site extension](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span></span>
* [<span data-ttu-id="175c4-174">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="175c4-174">Use Docker with Web Apps for containers</span></span>](#use-docker-with-web-apps-for-containers)

<span data-ttu-id="175c4-175">如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。</span><span class="sxs-lookup"><span data-stu-id="175c4-175">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="175c4-176">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="175c4-176">Install the preview site extension</span></span>

1. <span data-ttu-id="175c4-177">从 Azure 门户导航到“应用服务”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="175c4-177">From the Azure portal, navigate to the App Service blade.</span></span>
1. <span data-ttu-id="175c4-178">选择 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="175c4-178">Select the web app.</span></span>
1. <span data-ttu-id="175c4-179">在搜索框中输入“扩”或向下滚动到“开发工具”的管理窗格列表。</span><span class="sxs-lookup"><span data-stu-id="175c4-179">Enter "ex" in the search box or scroll down the list of management panes to **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="175c4-180">选择“开发工具” > “扩展”。</span><span class="sxs-lookup"><span data-stu-id="175c4-180">Select **DEVELOPMENT TOOLS** > **Extensions**.</span></span>
1. <span data-ttu-id="175c4-181">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="175c4-181">Select **Add**.</span></span>

   ![显示上述部署的 Azure 应用边栏选项卡](index/_static/x1.png)

1. <span data-ttu-id="175c4-183">选择“ASP.NET Core 扩展”。</span><span class="sxs-lookup"><span data-stu-id="175c4-183">Select **ASP.NET Core Extensions**.</span></span>
1. <span data-ttu-id="175c4-184">选择“确定”以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="175c4-184">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="175c4-185">选择“确定”安装扩展。</span><span class="sxs-lookup"><span data-stu-id="175c4-185">Select **OK** to install the extension.</span></span>

<span data-ttu-id="175c4-186">添加操作完成时，即表示已安装最新的 .NET Core 预览。</span><span class="sxs-lookup"><span data-stu-id="175c4-186">When the add operations complete, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="175c4-187">通过在控制台中运行 `dotnet --info` 来验证安装。</span><span class="sxs-lookup"><span data-stu-id="175c4-187">Verify the installation by running `dotnet --info` in the console.</span></span> <span data-ttu-id="175c4-188">从“应用服务”边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="175c4-188">From the **App Service** blade:</span></span>

1. <span data-ttu-id="175c4-189">在搜索框中输入“控”或向下滚动到“开发工具”的管理窗格列表。</span><span class="sxs-lookup"><span data-stu-id="175c4-189">Enter "con" in the search box or scroll down the list of management panes to **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="175c4-190">选择“开发工具” > “控制台”。</span><span class="sxs-lookup"><span data-stu-id="175c4-190">Select **DEVELOPMENT TOOLS** > **Console**.</span></span>
1. <span data-ttu-id="175c4-191">在控制台中输入 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="175c4-191">Enter `dotnet --info` in the console.</span></span>

<span data-ttu-id="175c4-192">如果版本 `2.1.300-preview1-008174` 是最新的预览版本，在命令提示符处运行 `dotnet --info` 将获得以下输出：</span><span class="sxs-lookup"><span data-stu-id="175c4-192">If version `2.1.300-preview1-008174` is the latest preview release, the following output is obtained by running `dotnet --info` at the command prompt:</span></span>

![显示上述部署的 Azure 应用边栏选项卡](index/_static/cons.png)

<span data-ttu-id="175c4-194">上图中显示的 ASP.NET Core 的版本 `2.1.300-preview1-008174` 就是一个示例。</span><span class="sxs-lookup"><span data-stu-id="175c4-194">The version of ASP.NET Core shown in the preceding image, `2.1.300-preview1-008174`, is an example.</span></span> <span data-ttu-id="175c4-195">执行 `dotnet --info` 时，将显示配置站点扩展时的 ASP.NET Core 的最新预览版本。</span><span class="sxs-lookup"><span data-stu-id="175c4-195">The latest preview version of ASP.NET Core at the time the site extension is configured appears when you execute `dotnet --info`.</span></span>

<span data-ttu-id="175c4-196">`dotnet --info` 显示已安装该预览的站点扩展的路径。</span><span class="sxs-lookup"><span data-stu-id="175c4-196">The `dotnet --info` displays the path to the site extension where the Preview has been installed.</span></span> <span data-ttu-id="175c4-197">它显示应用从该站点扩展运行，而不是从默认的 ProgramFiles 位置运行。</span><span class="sxs-lookup"><span data-stu-id="175c4-197">It shows the app is running from the site extension instead of from the default *ProgramFiles* location.</span></span> <span data-ttu-id="175c4-198">如果看到 ProgramFiles，请重启该站点并运行 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="175c4-198">If you see *ProgramFiles*, restart the site and run `dotnet --info`.</span></span>

<span data-ttu-id="175c4-199">**通过 ARM 模板使用预览站点扩展**</span><span class="sxs-lookup"><span data-stu-id="175c4-199">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="175c4-200">如果使用 ARM 模板创建和部署应用，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="175c4-200">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="175c4-201">例如:</span><span class="sxs-lookup"><span data-stu-id="175c4-201">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

<!--
### Deploy the app self-contained

A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment. When deploying a self-contained app:

* The site doesn't need to be prepared.
* The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.

Self-contained apps are an option for all ASP.NET Core apps.
-->

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="175c4-202">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="175c4-202">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="175c4-203">[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的预览 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="175c4-203">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="175c4-204">这些映像可以用作基础映像。</span><span class="sxs-lookup"><span data-stu-id="175c4-204">The images can be used as a base image.</span></span> <span data-ttu-id="175c4-205">按常规方法使用映像并部署到用于容器的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="175c4-205">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="175c4-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="175c4-206">Additional resources</span></span>

* [<span data-ttu-id="175c4-207">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="175c4-207">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="175c4-208">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="175c4-208">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="175c4-209">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="175c4-209">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="175c4-210">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="175c4-210">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="175c4-211">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="175c4-211">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="175c4-212">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="175c4-212">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="175c4-213">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="175c4-213">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
