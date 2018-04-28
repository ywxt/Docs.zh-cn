---
title: 在 Azure 应用服务上托管 ASP.NET Core
author: guardrex
description: 通过指向有用资源的链接，了解如何在 Azure 应用服务中托管 ASP.NET Core 应用。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: f53f77d342cc59094a80e8667db6ef345a6e8305
ms.sourcegitcommit: 01db73f2f7ac22b11ea48a947131d6176b0fe9ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="6ea0e-103">在 Azure 应用服务上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6ea0e-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="6ea0e-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="6ea0e-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="6ea0e-105">Useful resources</span></span>

<span data-ttu-id="6ea0e-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="6ea0e-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="6ea0e-108">快速入门：在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="6ea0e-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="6ea0e-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="6ea0e-110">快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="6ea0e-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="6ea0e-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="6ea0e-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="6ea0e-113">使用 Visual Studio 发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="6ea0e-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="6ea0e-114">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="6ea0e-115">使用 CLI 工具发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="6ea0e-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="6ea0e-116">了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="6ea0e-117">使用 Visual Studio 和 Git 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="6ea0e-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="6ea0e-118">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="6ea0e-119">使用 VSTS 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="6ea0e-119">Continuous deployment to Azure with VSTS</span></span>](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
<span data-ttu-id="6ea0e-120">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="6ea0e-121">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="6ea0e-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="6ea0e-122">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="6ea0e-123">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="6ea0e-123">Application configuration</span></span>

<span data-ttu-id="6ea0e-124">在 ASP.NET Core 2.0 和更高版本中，[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中的三个包为部署到 Azure 应用服务的应用提供自动日志记录功能：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-124">With ASP.NET Core 2.0 and later, three packages in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="6ea0e-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) to provide ASP.NET Core lightup integration with Azure App Service.</span></span> <span data-ttu-id="6ea0e-126">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="6ea0e-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="6ea0e-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="6ea0e-129">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="6ea0e-129">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="6ea0e-130">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-130">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="6ea0e-131">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-131">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="6ea0e-132">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-132">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="6ea0e-133">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="6ea0e-133">Monitoring and logging</span></span>

<span data-ttu-id="6ea0e-134">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-134">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="6ea0e-135">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="6ea0e-135">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="6ea0e-136">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-136">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="6ea0e-137">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="6ea0e-137">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="6ea0e-138">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-138">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="6ea0e-139">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="6ea0e-139">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="6ea0e-140">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-140">Understand common appoaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="6ea0e-141">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="6ea0e-141">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="6ea0e-142">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-142">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="6ea0e-143">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="6ea0e-143">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="6ea0e-144">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-144">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="6ea0e-145">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="6ea0e-145">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="6ea0e-146">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-146">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="6ea0e-147">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-147">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="6ea0e-148">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-148">Keys aren't protected at rest.</span></span> <span data-ttu-id="6ea0e-149">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-149">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="6ea0e-150">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-150">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="6ea0e-151">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-151">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="6ea0e-152">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-152">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="6ea0e-153">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-153">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="6ea0e-154">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-154">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="6ea0e-155">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="6ea0e-155">Azure Blob Storage</span></span>
* <span data-ttu-id="6ea0e-156">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6ea0e-156">Azure Key Vault</span></span>
* <span data-ttu-id="6ea0e-157">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="6ea0e-157">SQL store</span></span>
* <span data-ttu-id="6ea0e-158">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="6ea0e-158">Redis cache</span></span>

<span data-ttu-id="6ea0e-159">有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-159">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="6ea0e-160">将 ASP.NET Core 预览版部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="6ea0e-160">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="6ea0e-161">可通过以下方法将 ASP.NET Core 预览应用部署到 Azure 应用服务：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-161">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* [<span data-ttu-id="6ea0e-162">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="6ea0e-162">Install the preview site extension</span></span>](#install-the-preview-site-extension)
* [<span data-ttu-id="6ea0e-163">部署自包含应用</span><span class="sxs-lookup"><span data-stu-id="6ea0e-163">Deploy the app self-contained</span></span>](#deploy-the-app-self-contained)
* [<span data-ttu-id="6ea0e-164">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="6ea0e-164">Use Docker with Web Apps for containers</span></span>](#use-docker-with-web-apps-for-containers)

<span data-ttu-id="6ea0e-165">如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-165">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="6ea0e-166">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="6ea0e-166">Install the preview site extension</span></span>

* <span data-ttu-id="6ea0e-167">从 Azure 门户导航到“应用服务”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-167">From the Azure portal, navigate to the App Service blade.</span></span>
* <span data-ttu-id="6ea0e-168">在搜索框中输入“ex”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-168">Enter "ex" in the search box.</span></span>
* <span data-ttu-id="6ea0e-169">选择“扩展”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-169">Select **Extensions**.</span></span>
* <span data-ttu-id="6ea0e-170">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-170">Select "Add".</span></span>

![显示上述部署的 Azure 应用边栏选项卡](index/_static/x1.png)

* <span data-ttu-id="6ea0e-172">选择“ASP.NET Core 2.1 (x86) 运行时”或“ASP.NET Core 2.1 (x64)”运行时。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-172">Select **ASP.NET Core 2.1 (x86) Runtime** or **ASP.NET Core 2.1 (x64) Runtime**.</span></span>
* <span data-ttu-id="6ea0e-173">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-173">Select **OK**.</span></span> <span data-ttu-id="6ea0e-174">再次选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-174">Select **OK** again.</span></span>

<span data-ttu-id="6ea0e-175">添加操作完成时，即表示已安装最新的 .NET Core 2.1 预览。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-175">When the add operations complete, the latest .NET Core 2.1 preview is installed.</span></span> <span data-ttu-id="6ea0e-176">通过在控制台中运行 `dotnet --info` 来验证安装。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-176">Verify the installation by running `dotnet --info` in the console.</span></span> <span data-ttu-id="6ea0e-177">从“应用服务”边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-177">From the **App Service** blade:</span></span>

* <span data-ttu-id="6ea0e-178">在搜索框中输入“con”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-178">Enter "con" in the search box.</span></span>
* <span data-ttu-id="6ea0e-179">选择“控制台”。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-179">Select **Console**.</span></span>
* <span data-ttu-id="6ea0e-180">在控制台中输入 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-180">Enter `dotnet --info` in the console.</span></span>

![显示上述部署的 Azure 应用边栏选项卡](index/_static/cons.png)

<span data-ttu-id="6ea0e-182">前面的图像在写入时是最新的。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-182">The preceding image was current at the time this was written.</span></span> <span data-ttu-id="6ea0e-183">你可能会看到不同的版本。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-183">You may see a different version.</span></span>

<span data-ttu-id="6ea0e-184">`dotnet --info` 显示已安装该预览的站点扩展的路径。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-184">The `dotnet --info` displays the the path to the site extension where the Preview has been installed.</span></span> <span data-ttu-id="6ea0e-185">它显示应用从该站点扩展运行，而不是从默认的 ProgramFiles 位置运行。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-185">It shows the app is running from the site extension instead of from the default *ProgramFiles* location.</span></span> <span data-ttu-id="6ea0e-186">如果看到 ProgramFiles，请重启该站点并运行 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-186">If you see *ProgramFiles*, restart the site and run `dotnet --info`.</span></span>

<span data-ttu-id="6ea0e-187">**通过 ARM 模板使用预览站点扩展**</span><span class="sxs-lookup"><span data-stu-id="6ea0e-187">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="6ea0e-188">如果使用 ARM 模板创建和部署应用，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-188">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="6ea0e-189">例如:</span><span class="sxs-lookup"><span data-stu-id="6ea0e-189">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="6ea0e-190">部署自包含应用</span><span class="sxs-lookup"><span data-stu-id="6ea0e-190">Deploy the app self-contained</span></span>

<span data-ttu-id="6ea0e-191">可以部署在部署中携带部署预览运行时的[自包含应用](/dotnet/core/deploying/#self-contained-deployments-scd)。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-191">A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment.</span></span> <span data-ttu-id="6ea0e-192">部署自包含应用时：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-192">When deploying a self-contained app:</span></span>

* <span data-ttu-id="6ea0e-193">不需要准备站点。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-193">The site doesn't need to be prepared.</span></span>
* <span data-ttu-id="6ea0e-194">相较于依赖框架的部署（使用服务器上的共享运行时和主机）的发布方式，必须以不同的方式发布此类应用。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-194">The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.</span></span>

<span data-ttu-id="6ea0e-195">对所有 ASP.NET Core 应用而言，自包含应用都是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-195">Self-contained apps are an option for all ASP.NET Core apps.</span></span>

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="6ea0e-196">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="6ea0e-196">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="6ea0e-197">[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的 2.1 预览 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-197">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest 2.1 preview Docker images.</span></span> <span data-ttu-id="6ea0e-198">这些映像可以用作基础映像。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-198">The images can be used as a base image.</span></span> <span data-ttu-id="6ea0e-199">按常规方法使用映像并部署到用于容器的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-199">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ea0e-200">其他资源</span><span class="sxs-lookup"><span data-stu-id="6ea0e-200">Additional resources</span></span>

* [<span data-ttu-id="6ea0e-201">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="6ea0e-201">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="6ea0e-202">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="6ea0e-202">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="6ea0e-203">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="6ea0e-203">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="6ea0e-204">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="6ea0e-204">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)

<span data-ttu-id="6ea0e-205">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="6ea0e-205">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="6ea0e-206">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="6ea0e-206">The following topics pertain to the underlying IIS technology:</span></span>

* [<span data-ttu-id="6ea0e-207">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6ea0e-207">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="6ea0e-208">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="6ea0e-208">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="6ea0e-209">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="6ea0e-209">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="6ea0e-210">IIS Modules 与 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6ea0e-210">IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="6ea0e-211">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="6ea0e-211">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
