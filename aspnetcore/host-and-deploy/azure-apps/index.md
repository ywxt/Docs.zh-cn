---
title: "在 Azure 应用服务上托管 ASP.NET Core"
author: guardrex
description: "通过指向有用资源的链接，了解如何在 Azure 应用服务中托管 ASP.NET Core 应用。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: cefbc27c8091a2ed1441663e3779d67aae2c64dd
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="5665a-103">在 Azure 应用服务上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5665a-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="5665a-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="5665a-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

[!INCLUDE[Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

## <a name="useful-resources"></a><span data-ttu-id="5665a-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="5665a-105">Useful resources</span></span>

<span data-ttu-id="5665a-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="5665a-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="5665a-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="5665a-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="5665a-108">快速入门：在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="5665a-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="5665a-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="5665a-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="5665a-110">快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="5665a-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="5665a-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="5665a-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="5665a-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="5665a-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="5665a-113">使用 Visual Studio 发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="5665a-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="5665a-114">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="5665a-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="5665a-115">使用 CLI 工具发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="5665a-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="5665a-116">了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="5665a-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="5665a-117">使用 Visual Studio 和 Git 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="5665a-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="5665a-118">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="5665a-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="5665a-119">使用 VSTS 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="5665a-119">Continuous deployment to Azure with VSTS</span></span>](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
<span data-ttu-id="5665a-120">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="5665a-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="5665a-121">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="5665a-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="5665a-122">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="5665a-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="5665a-123">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="5665a-123">Application configuration</span></span>

<span data-ttu-id="5665a-124">在 ASP.NET Core 2.0 和更高版本中，[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中的三个包为部署到 Azure 应用服务的应用提供自动日志记录功能：</span><span class="sxs-lookup"><span data-stu-id="5665a-124">With ASP.NET Core 2.0 and later, three packages in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="5665a-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="5665a-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) to provide ASP.NET Core lightup integration with Azure App Service.</span></span> <span data-ttu-id="5665a-126">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="5665a-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="5665a-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="5665a-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="5665a-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="5665a-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="5665a-129">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="5665a-129">Monitoring and logging</span></span>

<span data-ttu-id="5665a-130">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="5665a-130">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="5665a-131">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="5665a-131">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="5665a-132">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="5665a-132">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="5665a-133">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="5665a-133">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="5665a-134">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="5665a-134">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="5665a-135">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="5665a-135">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="5665a-136">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="5665a-136">Understand common appoaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="5665a-137">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="5665a-137">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="5665a-138">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="5665a-138">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="5665a-139">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="5665a-139">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="5665a-140">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="5665a-140">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="5665a-141">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="5665a-141">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="5665a-142">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5665a-142">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="5665a-143">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="5665a-143">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="5665a-144">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="5665a-144">Keys aren't protected at rest.</span></span> <span data-ttu-id="5665a-145">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="5665a-145">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="5665a-146">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="5665a-146">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="5665a-147">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="5665a-147">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="5665a-148">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="5665a-148">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="5665a-149">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="5665a-149">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="5665a-150">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="5665a-150">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="5665a-151">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="5665a-151">Azure Blob Storage</span></span>
* <span data-ttu-id="5665a-152">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="5665a-152">Azure Key Vault</span></span>
* <span data-ttu-id="5665a-153">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="5665a-153">SQL store</span></span>
* <span data-ttu-id="5665a-154">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="5665a-154">Redis cache</span></span>

<span data-ttu-id="5665a-155">有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。</span><span class="sxs-lookup"><span data-stu-id="5665a-155">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5665a-156">其他资源</span><span class="sxs-lookup"><span data-stu-id="5665a-156">Additional resources</span></span>

* [<span data-ttu-id="5665a-157">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="5665a-157">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="5665a-158">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="5665a-158">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="5665a-159">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="5665a-159">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="5665a-160">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="5665a-160">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)

<span data-ttu-id="5665a-161">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="5665a-161">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="5665a-162">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="5665a-162">The following topics pertain to the underlying IIS technology:</span></span>

* [<span data-ttu-id="5665a-163">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5665a-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="5665a-164">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="5665a-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="5665a-165">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="5665a-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="5665a-166">配合使用 IIS 模块与 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5665a-166">Using IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="5665a-167">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="5665a-167">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
