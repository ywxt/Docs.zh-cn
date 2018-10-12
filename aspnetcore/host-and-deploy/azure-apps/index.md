---
title: 将 ASP.NET Core 应用部署到 Azure 应用服务
author: guardrex
description: 本文包含 Azure 主机和部署资源的链接。
ms.author: riande
ms.custom: mvc
ms.date: 08/29/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: f2de81af4bd2992aec76a287484d0057021231d8
ms.sourcegitcommit: 13940eb53c68664b11a2d685ee17c78faab1945d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860961"
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a><span data-ttu-id="c0ac4-103">将 ASP.NET Core 应用部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="c0ac4-103">Deploy ASP.NET Core apps to Azure App Service</span></span>

<span data-ttu-id="c0ac4-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="c0ac4-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="c0ac4-105">Useful resources</span></span>

<span data-ttu-id="c0ac4-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="c0ac4-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="c0ac4-108">快速入门：在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="c0ac4-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="c0ac4-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="c0ac4-110">快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="c0ac4-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="c0ac4-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="c0ac4-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="c0ac4-113">使用 Visual Studio 发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="c0ac4-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="c0ac4-114">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="c0ac4-115">使用 Visual Studio 和 Git 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="c0ac4-115">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="c0ac4-116">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-116">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="c0ac4-117">使用 Azure Pipelines 创建你的第一个管道</span><span class="sxs-lookup"><span data-stu-id="c0ac4-117">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)  
<span data-ttu-id="c0ac4-118">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-118">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="c0ac4-119">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="c0ac4-119">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="c0ac4-120">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-120">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a><span data-ttu-id="c0ac4-121">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="c0ac4-121">Application configuration</span></span>

<span data-ttu-id="c0ac4-122">在 ASP.NET Core 2.0 或更高版本中，以下 NuGet 包可为部署到 Azure 应用服务的应用提供自动登录功能。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-122">In ASP.NET Core 2.0 or later, the following NuGet packages provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="c0ac4-123">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-123">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="c0ac4-124">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-124">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="c0ac4-125">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-125">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="c0ac4-126">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-126">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="c0ac4-127">如果面向 .NET Core 且引用 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)，则已经包括这些包。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-127">If targeting .NET Core and referencing the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage), the packages are already included.</span></span> <span data-ttu-id="c0ac4-128">这些包不包括在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-128">The packages are absent from the newer [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="c0ac4-129">如果面向 .NET Framework 或引用 `Microsoft.AspNetCore.App` 元包，请引用单个登录包。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-129">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, reference the individual logging packages.</span></span>

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="c0ac4-130">使用 Azure 门户重写应用配置</span><span class="sxs-lookup"><span data-stu-id="c0ac4-130">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="c0ac4-131">“应用程序设置”边栏选项卡的“应用设置”区域允许你为应用设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-131">The **App Settings** area of the **Application settings** blade permits you to set environment variables for the app.</span></span> <span data-ttu-id="c0ac4-132">可以通过[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)来使用环境变量。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-132">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="c0ac4-133">当应用使用 [Web 主机](xref:fundamentals/host/web-host)并使用 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 构建主机时，配置主机的环境变量使用 `ASPNETCORE_` 前缀。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-133">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="c0ac4-134">有关详细信息，请参阅 <xref:fundamentals/host/web-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-134">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="c0ac4-135">当应用使用[通用主机](xref:fundamentals/host/generic-host)时，环境变量在默认情况下不会加载到应用的配置，且配置提供程序必须由开发人员添加。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-135">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="c0ac4-136">在添加配置提供程序时，开发人员将确定环境变量前缀。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-136">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="c0ac4-137">有关详细信息，请参阅 <xref:fundamentals/host/generic-host> 和[环境变量配置提供程序](xref:fundamentals/configuration/index#environment-variables-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-137">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="c0ac4-138">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="c0ac4-138">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="c0ac4-139">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-139">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="c0ac4-140">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-140">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="c0ac4-141">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-141">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="c0ac4-142">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="c0ac4-142">Monitoring and logging</span></span>

<span data-ttu-id="c0ac4-143">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-143">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="c0ac4-144">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="c0ac4-144">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="c0ac4-145">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-145">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="c0ac4-146">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="c0ac4-146">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="c0ac4-147">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-147">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="c0ac4-148">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="c0ac4-148">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="c0ac4-149">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-149">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="c0ac4-150">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="c0ac4-150">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="c0ac4-151">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-151">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="c0ac4-152">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="c0ac4-152">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="c0ac4-153">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-153">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="c0ac4-154">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="c0ac4-154">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="c0ac4-155">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-155">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="c0ac4-156">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-156">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="c0ac4-157">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-157">Keys aren't protected at rest.</span></span> <span data-ttu-id="c0ac4-158">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-158">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="c0ac4-159">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-159">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="c0ac4-160">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-160">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="c0ac4-161">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-161">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="c0ac4-162">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-162">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="c0ac4-163">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-163">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="c0ac4-164">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="c0ac4-164">Azure Blob Storage</span></span>
* <span data-ttu-id="c0ac4-165">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c0ac4-165">Azure Key Vault</span></span>
* <span data-ttu-id="c0ac4-166">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="c0ac4-166">SQL store</span></span>
* <span data-ttu-id="c0ac4-167">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="c0ac4-167">Redis cache</span></span>

<span data-ttu-id="c0ac4-168">有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-168">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="c0ac4-169">将 ASP.NET Core 预览版部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="c0ac4-169">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="c0ac4-170">可通过以下方法将 ASP.NET Core 预览应用部署到 Azure 应用服务：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-170">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* <span data-ttu-id="c0ac4-171">[安装预览站点扩展](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span><span class="sxs-lookup"><span data-stu-id="c0ac4-171">[Install the preview site extension](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span></span>
* [<span data-ttu-id="c0ac4-172">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="c0ac4-172">Use Docker with Web Apps for containers</span></span>](#use-docker-with-web-apps-for-containers)

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="c0ac4-173">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="c0ac4-173">Install the preview site extension</span></span>

<span data-ttu-id="c0ac4-174">如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-174">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

1. <span data-ttu-id="c0ac4-175">从 Azure 门户导航到“应用服务”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-175">From the Azure portal, navigate to the App Service blade.</span></span>
1. <span data-ttu-id="c0ac4-176">选择 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-176">Select the web app.</span></span>
1. <span data-ttu-id="c0ac4-177">在搜索框中键入“ex”或向下滚动管理部分列表，到达“开发工具”。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-177">Type "ex" in the search box or scroll down the list of management sections to **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="c0ac4-178">选择“开发工具” > “扩展”。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-178">Select **DEVELOPMENT TOOLS** > **Extensions**.</span></span>
1. <span data-ttu-id="c0ac4-179">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-179">Select **Add**.</span></span>
1. <span data-ttu-id="c0ac4-180">从列表选择“ASP.NET Core &lt;x.y&gt; (x86) 运行时”扩展，其中 `<x.y>` 是 ASP.NET Core 预览版本（例如，ASP.NET Core 2.2 (x86) 运行时）。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-180">Select the **ASP.NET Core &lt;x.y&gt; (x86) Runtime** extension from the list, where `<x.y>` is the ASP.NET Core preview version (for example, **ASP.NET Core 2.2 (x86) Runtime**).</span></span> <span data-ttu-id="c0ac4-181">x86 运行时适用于[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)，这种部署依赖于 ASP.NET Core 模块的进程外托管。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-181">The x86 runtime is appropriate for [framework-dependent deployments](/dotnet/core/deploying/#framework-dependent-deployments-fdd) that rely on out-of-process hosting by the ASP.NET Core Module.</span></span>
1. <span data-ttu-id="c0ac4-182">选择“确定”以接受法律条款。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-182">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="c0ac4-183">选择“确定”安装扩展。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-183">Select **OK** to install the extension.</span></span>

<span data-ttu-id="c0ac4-184">操作完成时，即表示已安装最新的 .NET Core 预览版。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-184">When the operation completes, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="c0ac4-185">验证安装：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-185">Verify the installation:</span></span>

1. <span data-ttu-id="c0ac4-186">选择“开发工具”下的“高级工具”。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-186">Select **Advanced Tools** under **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="c0ac4-187">在“高级工具”边栏选项卡上，选择“转到”。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-187">Select **Go** on the **Advanced Tools** blade.</span></span>
1. <span data-ttu-id="c0ac4-188">选择“调试控制台” > “PowerShell”菜单项。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-188">Select the **Debug console** > **PowerShell** menu item.</span></span>
1. <span data-ttu-id="c0ac4-189">从 PowerShell 命令提示符处执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-189">At the PowerShell prompt, execute the following command.</span></span> <span data-ttu-id="c0ac4-190">在以下命令中，将 ASP.NET Core 运行时版本替换为 `<x.y>` ：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-190">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x86\
   ```
   <span data-ttu-id="c0ac4-191">如果已安装的预览版运行时为 ASP.NET Core 2.2，则命令是：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-191">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x86\
   ```
   <span data-ttu-id="c0ac4-192">如果安装 x64 预览版运行时，该命令将返回`True`。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-192">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="c0ac4-193">对于在 A 系列计算机上或更高级托管层上托管的应用，可在“常规设置”下的“应用程序设置”中设置应用服务应用的平台体系结构 (x86/x64)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-193">The platform architecture (x86/x64) of an App Services app is set in the **Application Settings** blade under **General Settings** for apps that are hosted on an A-series compute or better hosting tier.</span></span> <span data-ttu-id="c0ac4-194">如果应用在进程内模式下运行并且平台体系结构配置为 64 位 (x64)，则 ASP.NET Core 模块会使用 64 位预览版运行时（如存在）。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-194">If the app is run in in-process mode and the platform architecture is configured for 64-bit (x64), the ASP.NET Core Module uses the 64-bit preview runtime, if present.</span></span> <span data-ttu-id="c0ac4-195">安装 ASP.NET Core &lt;x.y&gt; (x64) 运行时扩展 （例如，ASP.NET Core 2.2 (x64) 运行时）。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-195">Install the **ASP.NET Core &lt;x.y&gt; (x64) Runtime** extension (for example, **ASP.NET Core 2.2 (x64) Runtime**).</span></span>
>
> <span data-ttu-id="c0ac4-196">安装 x64 预览版运行时后，在 Kudu PowerShell 命令窗口中运行以下命令以验证该安装。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-196">After installing the x64 preview runtime, run the following command in the Kudu PowerShell command window to verify the installation.</span></span> <span data-ttu-id="c0ac4-197">在以下命令中，将 ASP.NET Core 运行时版本替换为 `<x.y>` ：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-197">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x64\
> ```
> <span data-ttu-id="c0ac4-198">如果已安装的预览版运行时为 ASP.NET Core 2.2，则命令是：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-198">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x64\
> ```
> <span data-ttu-id="c0ac4-199">如果安装 x64 预览版运行时，该命令将返回`True`。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-199">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker-end

> [!NOTE]
> <span data-ttu-id="c0ac4-200">ASP.NET Core 扩展可为 Azure 应用服务上的 ASP.NET Core 启用附加功能，例如启用 Azure 日志记录。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-200">**ASP.NET Core Extensions** enables additional functionality for ASP.NET Core on Azure App Services, such as enabling Azure logging.</span></span> <span data-ttu-id="c0ac4-201">从 Visual Studio 进行部署时，将自动安装该扩展。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-201">The extension is installed automatically when deploying from Visual Studio.</span></span> <span data-ttu-id="c0ac4-202">如果未安装该扩展，请为应用安装它。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-202">If the extension isn't installed, install it for the app.</span></span>

<span data-ttu-id="c0ac4-203">**通过 ARM 模板使用预览站点扩展**</span><span class="sxs-lookup"><span data-stu-id="c0ac4-203">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="c0ac4-204">如果使用 ARM 模板创建和部署应用，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-204">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="c0ac4-205">例如:</span><span class="sxs-lookup"><span data-stu-id="c0ac4-205">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

<!--
### Deploy the app self-contained

A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment. When deploying a self-contained app:

* The site doesn't need to be prepared.
* The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.

Self-contained apps are an option for all ASP.NET Core apps.
-->

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="c0ac4-206">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="c0ac4-206">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="c0ac4-207">[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的预览 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-207">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="c0ac4-208">这些映像可以用作基础映像。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-208">The images can be used as a base image.</span></span> <span data-ttu-id="c0ac4-209">按常规方法使用映像并部署到用于容器的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-209">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0ac4-210">其他资源</span><span class="sxs-lookup"><span data-stu-id="c0ac4-210">Additional resources</span></span>

* [<span data-ttu-id="c0ac4-211">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="c0ac4-211">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="c0ac4-212">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="c0ac4-212">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="c0ac4-213">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="c0ac4-213">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="c0ac4-214">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="c0ac4-214">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="c0ac4-215">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="c0ac4-215">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="c0ac4-216">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="c0ac4-216">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="c0ac4-217">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="c0ac4-217">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
