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
ms.openlocfilehash: c2675f73880a41ee75f6ec13155419945387e109
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="bfe5c-103">在 Azure 应用服务上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bfe5c-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="bfe5c-104">[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于托管 Web 应用（包括 ASP.NET Core）的 [Microsoft 云计算平台服务](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="bfe5c-105">有用资源</span><span class="sxs-lookup"><span data-stu-id="bfe5c-105">Useful resources</span></span>

<span data-ttu-id="bfe5c-106">Azure 应用文档、教程、示例、操作指南和其他资源由 Azure [Web 应用文档](/azure/app-service/)提供。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="bfe5c-107">两个有关托管 ASP.NET Core 应用的重要教程为：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="bfe5c-108">快速入门：在 Azure 中创建 ASP.NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="bfe5c-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="bfe5c-109">使用 Visual Studio 创建 ASP.NET Core Web 应用，并将其部署到 Windows 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="bfe5c-110">快速入门：在 Linux 上的应用服务中创建 .NET Core Web 应用</span><span class="sxs-lookup"><span data-stu-id="bfe5c-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="bfe5c-111">使用命令行创建 ASP.NET Core Web 应用，并将其部署到 Linux 上的 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="bfe5c-112">ASP.NET Core 文档中提供以下文章：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="bfe5c-113">使用 Visual Studio 发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5c-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="bfe5c-114">了解如何使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="bfe5c-115">使用 CLI 工具发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5c-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="bfe5c-116">了解如何使用 Git 命令行客户端将 ASP.NET Core 应用发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="bfe5c-117">使用 Visual Studio 和 Git 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5c-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="bfe5c-118">了解如何使用 Visual Studio 创建 ASP.NET Core Web 应用并使用 Git 将它部署到 Azure 应用服务以实现持续部署。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="bfe5c-119">使用 VSTS 持续部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bfe5c-119">Continuous deployment to Azure with VSTS</span></span>](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
<span data-ttu-id="bfe5c-120">为 ASP.NET Core 应用设置 CI 生成，然后创建针对 Azure 应用服务的持续部署发布。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="bfe5c-121">Azure Web 应用沙盒</span><span class="sxs-lookup"><span data-stu-id="bfe5c-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="bfe5c-122">探索 Azure Apps 平台强制实施的 Azure 应用服务运行时执行限制。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="bfe5c-123">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="bfe5c-123">Application configuration</span></span>

<span data-ttu-id="bfe5c-124">在 ASP.NET Core 2.0 和更高版本中，[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中的三个包为部署到 Azure 应用服务的应用提供自动日志记录功能：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-124">With ASP.NET Core 2.0 and later, three packages in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="bfe5c-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) 使用 [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) 提供 ASP.NET Core 与 Azure 应用服务的启动集成。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) to provide ASP.NET Core lightup integration with Azure App Service.</span></span> <span data-ttu-id="bfe5c-126">添加的日志记录功能由 `Microsoft.AspNetCore.AzureAppServicesIntegration` 包提供。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="bfe5c-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) 执行 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)，在 `Microsoft.Extensions.Logging.AzureAppServices` 包中添加 Azure 应用服务诊断日志记录提供程序。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="bfe5c-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) 提供记录器实现，支持 Azure 应用服务诊断日志和日志流式处理功能。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="bfe5c-129">代理服务器和负载均衡器方案</span><span class="sxs-lookup"><span data-stu-id="bfe5c-129">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="bfe5c-130">配置转发头中间件的 IIS 集成中间件和 ASP.NET Core 模块将配置为转发方案 (HTTP/HTTPS) 和发出请求的远程 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-130">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="bfe5c-131">对于托管在其他代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-131">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="bfe5c-132">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-132">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="bfe5c-133">监视和日志记录</span><span class="sxs-lookup"><span data-stu-id="bfe5c-133">Monitoring and logging</span></span>

<span data-ttu-id="bfe5c-134">有关监视、日志记录和故障排除的信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-134">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="bfe5c-135">如何：在 Azure 应用服务中监视应用</span><span class="sxs-lookup"><span data-stu-id="bfe5c-135">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="bfe5c-136">了解如何查看应用和应用服务计划的配额和指标。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-136">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="bfe5c-137">在 Azure 应用服务中为应用启用诊断日志记录</span><span class="sxs-lookup"><span data-stu-id="bfe5c-137">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="bfe5c-138">了解如何启用和访问 HTTP 状态代码、失败请求和 Web 服务器活动的诊断日志记录。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-138">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="bfe5c-139">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="bfe5c-139">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="bfe5c-140">了解在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-140">Understand common appoaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="bfe5c-141">对 Azure 应用服务上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="bfe5c-141">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="bfe5c-142">了解如何使用 ASP.NET Core 应用诊断 Azure 应用服务部署问题。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-142">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="bfe5c-143">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="bfe5c-143">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="bfe5c-144">使用故障排除建议查看 Azure 应用服务/IIS 托管的应用的常见部署配置错误。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-144">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="bfe5c-145">数据保护密钥环和部署槽位</span><span class="sxs-lookup"><span data-stu-id="bfe5c-145">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="bfe5c-146">[数据保护密钥](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)保存在 %HOME%\ASP.NET\DataProtection-Keys 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-146">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="bfe5c-147">此文件夹由网络存储提供支持，并跨托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-147">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="bfe5c-148">密钥不是静态保护的。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-148">Keys aren't protected at rest.</span></span> <span data-ttu-id="bfe5c-149">此文件夹向单个部署槽位中应用的所有实例提供密钥环。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-149">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="bfe5c-150">各部署槽位（例如过渡槽和生成槽）不共享密钥环。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-150">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="bfe5c-151">在部署槽位之间交换时，使用数据保护的任意系统都无法使用之前槽位中的密钥环来解密存储的数据。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-151">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="bfe5c-152">ASP.NET Cookie 中间件使用数据保护来保护其 cookie。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-152">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="bfe5c-153">这导致用户注销使用标准 ASP.NET Cookie 中间件的应用。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-153">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="bfe5c-154">对于独立于槽位的密钥环解决方案，请使用外部密钥环提供程序，例如：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-154">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="bfe5c-155">Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="bfe5c-155">Azure Blob Storage</span></span>
* <span data-ttu-id="bfe5c-156">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bfe5c-156">Azure Key Vault</span></span>
* <span data-ttu-id="bfe5c-157">SQL 存储</span><span class="sxs-lookup"><span data-stu-id="bfe5c-157">SQL store</span></span>
* <span data-ttu-id="bfe5c-158">Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="bfe5c-158">Redis cache</span></span>

<span data-ttu-id="bfe5c-159">有关详细信息，请参阅[密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-159">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="bfe5c-160">将 ASP.NET Core 预览版部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="bfe5c-160">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="bfe5c-161">可通过以下方法将 ASP.NET Core 预览应用部署到 Azure 应用服务：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-161">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* [<span data-ttu-id="bfe5c-162">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="bfe5c-162">Install the preview site extention</span></span>](#site-x)
* [<span data-ttu-id="bfe5c-163">部署自包含应用</span><span class="sxs-lookup"><span data-stu-id="bfe5c-163">Deploy the app self contained</span></span>](#self)
* [<span data-ttu-id="bfe5c-164">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="bfe5c-164">Use Docker with Web Apps for containers</span></span>](#docker)

<span data-ttu-id="bfe5c-165">如果使用预览站点扩展时遇到问题，请在 [GitHub](https://github.com/aspnet/azureintegration/issues/new) 上打开相应的问题。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-165">If you have a problem using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

<a name="site-x"></a>
### <a name="install-the-preview-site-extention"></a><span data-ttu-id="bfe5c-166">安装预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="bfe5c-166">Install the preview site extention</span></span>

* <span data-ttu-id="bfe5c-167">从 Azure 门户导航到“应用服务”边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-167">From the Azure portal, navigate to the App Service blade.</span></span>
* <span data-ttu-id="bfe5c-168">在搜索框中输入“ex”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-168">Enter "ex" in the search box.</span></span>
* <span data-ttu-id="bfe5c-169">选择“扩展”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-169">Select **Extensions**.</span></span>
* <span data-ttu-id="bfe5c-170">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-170">Select "Add".</span></span>

![显示上述部署的 Azure 应用边栏选项卡](index/_static/x1.png)

* <span data-ttu-id="bfe5c-172">选择“ASP.NET Core 运行时扩展”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-172">Select **ASP.NET Core Runtime Extensions**.</span></span>
* <span data-ttu-id="bfe5c-173">选择“确定” > “确定”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-173">Select **OK** > **OK**.</span></span>

<span data-ttu-id="bfe5c-174">添加操作完成时，即表示已安装最新的 .NET Core 2.1 预览。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-174">When the add operations completes, the latest .NET Core 2.1 preview is installed.</span></span> <span data-ttu-id="bfe5c-175">可通过在控制台中运行 `dotnet --info` 来验证安装。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-175">You can verify the installation by running `dotnet --info` in the console.</span></span> <span data-ttu-id="bfe5c-176">从“应用服务”边栏选项卡：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-176">From the App Service blade:</span></span>

* <span data-ttu-id="bfe5c-177">在搜索框中输入“con”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-177">Enter "con" in the search box.</span></span>
* <span data-ttu-id="bfe5c-178">选择“控制台”。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-178">Select **Console**.</span></span>
* <span data-ttu-id="bfe5c-179">在控制台中输入 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-179">Enter `dotnet --info` in the console.</span></span>

![显示上述部署的 Azure 应用边栏选项卡](index/_static/cons.png)

<span data-ttu-id="bfe5c-181">前面的图像在写入时是最新的。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-181">The preceding image was current at the time this was written.</span></span> <span data-ttu-id="bfe5c-182">你可能会看到不同的版本。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-182">You may see a different version.</span></span>

<span data-ttu-id="bfe5c-183">`dotnet --info` 显示已安装该预览的站点扩展的路径。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-183">The `dotnet --info` displays the the path to the site extension where the Preview has been installed.</span></span> <span data-ttu-id="bfe5c-184">它显示应用从该站点扩展运行，而不是从默认的 ProgramFiles 位置运行。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-184">It shows the app is running from the site extension instead of from the default *ProgramFiles* location.</span></span> <span data-ttu-id="bfe5c-185">如果看到 ProgramFiles，请重启该站点并运行 `dotnet --info`。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-185">If you see *ProgramFiles*, restart the site and run `dotnet --info`.</span></span>

#### <a name="use-the-preview-site-extention-with-an-arm-template"></a><span data-ttu-id="bfe5c-186">通过 ARM 模板使用预览站点扩展</span><span class="sxs-lookup"><span data-stu-id="bfe5c-186">Use the preview site extention with an ARM template</span></span>

<span data-ttu-id="bfe5c-187">如果使用 ARM 模板来创建和部署应用程序，则可使用 `siteextensions` 资源类型将站点扩展添加到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-187">If you are using an ARM template to create and deploy applications you can use the `siteextensions` resource type to add the site extension to a Web App.</span></span> <span data-ttu-id="bfe5c-188">例如:</span><span class="sxs-lookup"><span data-stu-id="bfe5c-188">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

<a name="self"></a>
### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="bfe5c-189">部署自包含应用</span><span class="sxs-lookup"><span data-stu-id="bfe5c-189">Deploy the app self contained</span></span>

<span data-ttu-id="bfe5c-190">可以部署[自包含应用](/dotnet/core/deploying/#self-contained-deployments-scd)，它在部署时附有预览运行时。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-190">You can deploy a [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) that carries the preview runtime with it when being deployed.</span></span> <span data-ttu-id="bfe5c-191">部署自包含应用时：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-191">When deploying a self contained app:</span></span>

* <span data-ttu-id="bfe5c-192">无需准备站点。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-192">You don’t need to prepare your site.</span></span>
* <span data-ttu-id="bfe5c-193">在服务器上安装 SDK 后，需要采用不同于部署应用时的方式来发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-193">Requires you to publish your application differently than you would when deploying an app once the SDK is installed on the server.</span></span>

<span data-ttu-id="bfe5c-194">对所有 .NET Core 应用程序而言，自包含应用都是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-194">Self-contained apps are an option for all .NET Core applications.</span></span>

<a name="docker"></a>
### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="bfe5c-195">对用于容器的 Web 应用使用 Docker</span><span class="sxs-lookup"><span data-stu-id="bfe5c-195">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="bfe5c-196">[Docker 中心](https://hub.docker.com/r/microsoft/aspnetcore/)包含最新的 2.1 预览 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-196">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest 2.1 preview Docker images.</span></span> <span data-ttu-id="bfe5c-197">可将这些映像用作基础映像，并像平常一样将其部署到用于容器的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-197">You can use them as your base image and deploy to Web Apps for Containers as you normally would.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfe5c-198">其他资源</span><span class="sxs-lookup"><span data-stu-id="bfe5c-198">Additional resources</span></span>

* [<span data-ttu-id="bfe5c-199">Web 应用概述（5 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="bfe5c-199">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="bfe5c-200">Azure 应用服务：托管 .NET 应用的最佳位置（55 分钟概述视频）</span><span class="sxs-lookup"><span data-stu-id="bfe5c-200">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="bfe5c-201">Azure Friday：Azure 应用服务诊断和故障排除体验（12 分钟视频）</span><span class="sxs-lookup"><span data-stu-id="bfe5c-201">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="bfe5c-202">Azure 应用服务诊断概述</span><span class="sxs-lookup"><span data-stu-id="bfe5c-202">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)

<span data-ttu-id="bfe5c-203">Windows Server 上的 Azure 应用服务使用 [Internet Information Services (IIS)](https://www.iis.net/)。</span><span class="sxs-lookup"><span data-stu-id="bfe5c-203">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="bfe5c-204">以下是基础 IIS 技术的相关主题：</span><span class="sxs-lookup"><span data-stu-id="bfe5c-204">The following topics pertain to the underlying IIS technology:</span></span>

* [<span data-ttu-id="bfe5c-205">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bfe5c-205">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="bfe5c-206">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="bfe5c-206">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="bfe5c-207">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="bfe5c-207">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="bfe5c-208">IIS Modules 与 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bfe5c-208">IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="bfe5c-209">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="bfe5c-209">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
