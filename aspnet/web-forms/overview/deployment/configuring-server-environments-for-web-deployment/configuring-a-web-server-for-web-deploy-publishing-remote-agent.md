---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 配置 Web 服务器的 Web 部署发布 （远程代理） |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置 Internet 信息服务 (IIS) web 服务器以支持 web 发布和部署使用 IIS Web 部署...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: 348c618fe6ec726e8087b4f3acb66cddbef1d225
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819638"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a><span data-ttu-id="bca1e-103">配置用于 Web 部署发布 （远程代理） 的 Web 服务器</span><span class="sxs-lookup"><span data-stu-id="bca1e-103">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>
====================
<span data-ttu-id="bca1e-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="bca1e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="bca1e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="bca1e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="bca1e-106">本主题介绍如何配置 Internet 信息服务 (IIS) web 服务器以支持 web 发布和部署使用 IIS Web 部署工具 （Web 部署） 的远程代理服务。</span><span class="sxs-lookup"><span data-stu-id="bca1e-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deployment Tool (Web Deploy) Remote Agent Service.</span></span>
> 
> <span data-ttu-id="bca1e-107">在处理 Web Deploy 2.0 或更高版本时，有三种主要方法可用于获取你的应用程序或 web 服务器上的站点。</span><span class="sxs-lookup"><span data-stu-id="bca1e-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="bca1e-108">你可以：</span><span class="sxs-lookup"><span data-stu-id="bca1e-108">You can:</span></span>
> 
> - <span data-ttu-id="bca1e-109">使用*Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="bca1e-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="bca1e-110">这种方法需要较少配置 web 服务器，但您需要提供的本地服务器管理员凭据才能将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="bca1e-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="bca1e-111">使用*Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="bca1e-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="bca1e-112">这种方法更复杂，需要更多的初始工作来设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="bca1e-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="bca1e-113">但是，在使用此方法时，你可以配置 IIS 以允许非管理员用户来执行部署。</span><span class="sxs-lookup"><span data-stu-id="bca1e-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="bca1e-114">Web 部署处理程序只是在 IIS 7 或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="bca1e-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="bca1e-115">使用*离线部署*。</span><span class="sxs-lookup"><span data-stu-id="bca1e-115">Use *offline deployment*.</span></span> <span data-ttu-id="bca1e-116">这种方法需要 web 服务器的最低配置，但服务器管理员必须手动复制到服务器上的 web 包并将其导入通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="bca1e-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="bca1e-117">主要功能、 优势和一种方法的缺点的详细信息，请参阅[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a><span data-ttu-id="bca1e-118">是为您的 Web 部署远程代理的正确方法？</span><span class="sxs-lookup"><span data-stu-id="bca1e-118">Is the Web Deploy Remote Agent the Right Approach for You?</span></span>

<span data-ttu-id="bca1e-119">是，如果将部署内容的用户可以提供的目标服务器上凭据。</span><span class="sxs-lookup"><span data-stu-id="bca1e-119">Yes, if the user who will deploy the content can supply the credentials of an administrator on the destination server.</span></span> <span data-ttu-id="bca1e-120">这种方法通常是这些类型的方案中所需的：</span><span class="sxs-lookup"><span data-stu-id="bca1e-120">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="bca1e-121">开发或测试环境，其中的开发人员具有对目标 web 服务器和数据库服务器的完全控制。</span><span class="sxs-lookup"><span data-stu-id="bca1e-121">Development or test environments, where the developer has full control over the destination web server and database server.</span></span>
- <span data-ttu-id="bca1e-122">单个用户或一组少量用户具有控制整个应用程序生命周期较小的组织。</span><span class="sxs-lookup"><span data-stu-id="bca1e-122">Smaller organizations in which a single user or a small group of users has control over the entire application lifecycle.</span></span>

<span data-ttu-id="bca1e-123">在很多的大型组织，并特别是对于过渡或生产环境，它是通常不现实的向用户授予 web 服务器上的管理员权限。</span><span class="sxs-lookup"><span data-stu-id="bca1e-123">In lots of larger organizations, and particularly for staging or production environments, it's often not realistic to give users administrator rights on web servers.</span></span> <span data-ttu-id="bca1e-124">在托管的 web 服务器的情况下，这是更不可能出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="bca1e-124">In the case of hosted web servers, this is especially unlikely to be the case.</span></span> <span data-ttu-id="bca1e-125">此外，如果您打算自动执行从生成服务器的部署，可能不想要使用管理员凭据以及部署过程。</span><span class="sxs-lookup"><span data-stu-id="bca1e-125">In addition, if you're planning to automate deployment from a build server, you may not want to use administrator credentials for the deployment process.</span></span> <span data-ttu-id="bca1e-126">在这些情况下，在 web 服务器配置为支持部署使用的[Web 部署处理程序](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)可能会提供一个更令人满意的选择。</span><span class="sxs-lookup"><span data-stu-id="bca1e-126">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Handler](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) may provide a more satisfactory choice.</span></span>

## <a name="task-overview"></a><span data-ttu-id="bca1e-127">任务概述</span><span class="sxs-lookup"><span data-stu-id="bca1e-127">Task Overview</span></span>

<span data-ttu-id="bca1e-128">本主题介绍如何配置 Internet 信息服务 (IIS) 7.5 web 服务器来接受和部署 web 包从远程计算机使用 Web 部署远程代理方法。</span><span class="sxs-lookup"><span data-stu-id="bca1e-128">This topic describes how to configure an Internet Information Services (IIS) 7.5 web server to accept and deploy web packages from a remote computer using the Web Deploy Remote Agent approach.</span></span> <span data-ttu-id="bca1e-129">你将需要：</span><span class="sxs-lookup"><span data-stu-id="bca1e-129">You'll need to:</span></span>

- <span data-ttu-id="bca1e-130">安装 IIS 7.5 和 IIS 7 建议的配置。</span><span class="sxs-lookup"><span data-stu-id="bca1e-130">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="bca1e-131">安装 Web 部署 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="bca1e-131">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="bca1e-132">创建一个 IIS 网站来承载部署的内容。</span><span class="sxs-lookup"><span data-stu-id="bca1e-132">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="bca1e-133">确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="bca1e-133">Ensure that the Web Deployment Agent Service is running.</span></span>

<span data-ttu-id="bca1e-134">若要专门托管示例解决方案，还需要为：</span><span class="sxs-lookup"><span data-stu-id="bca1e-134">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="bca1e-135">安装.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="bca1e-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="bca1e-136">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="bca1e-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="bca1e-137">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="bca1e-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="bca1e-138">任务和本主题中的演练假定您正在使用运行 Windows Server 2008 R2 的全新服务器内部版本。</span><span class="sxs-lookup"><span data-stu-id="bca1e-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="bca1e-139">在继续之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="bca1e-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="bca1e-140">安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="bca1e-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="bca1e-141">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="bca1e-141">The server is domain-joined.</span></span>
- <span data-ttu-id="bca1e-142">在服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="bca1e-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="bca1e-143">有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="bca1e-144">有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="bca1e-145">远程代理服务支持的 IIS 6 及更高版本，并且不需要您加入到域。</span><span class="sxs-lookup"><span data-stu-id="bca1e-145">The Remote Agent service is supported by IIS 6 onwards and does not require you to be joined to a domain.</span></span> <span data-ttu-id="bca1e-146">但是，在本教程中的步骤已开发且在 IIS 7.5 上进行测试，对于其他版本的过程可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="bca1e-146">However, the steps in this tutorial were developed and tested on IIS 7.5 and procedures for other versions may vary.</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="bca1e-147">安装的产品和组件</span><span class="sxs-lookup"><span data-stu-id="bca1e-147">Install Products and Components</span></span>

<span data-ttu-id="bca1e-148">本部分将指导您完成在 web 服务器上安装所需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="bca1e-148">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="bca1e-149">在开始之前，一个好的做法是运行 Windows 更新，以确保你的服务器是完全保持最新。</span><span class="sxs-lookup"><span data-stu-id="bca1e-149">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="bca1e-150">在这种情况下，你需要安装以下事项：</span><span class="sxs-lookup"><span data-stu-id="bca1e-150">In this case, you need to install these things:</span></span>

- <span data-ttu-id="bca1e-151">**IIS 7 推荐配置**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-151">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="bca1e-152">这使得**Web 服务器 (IIS)** 角色在 web 服务器上的和安装的 IIS 模块和托管的 ASP.NET 应用程序所需的组件组。</span><span class="sxs-lookup"><span data-stu-id="bca1e-152">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="bca1e-153">**.NET framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-153">**.NET Framework 4.0**.</span></span> <span data-ttu-id="bca1e-154">这是运行此版本的.NET Framework 生成的应用程序所需要的。</span><span class="sxs-lookup"><span data-stu-id="bca1e-154">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="bca1e-155">**Web 部署工具 2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-155">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="bca1e-156">这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="bca1e-156">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="bca1e-157">作为此过程的一部分，它会安装并启动 Web 部署代理服务。</span><span class="sxs-lookup"><span data-stu-id="bca1e-157">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="bca1e-158">此服务允许你部署 web 包从远程计算机。</span><span class="sxs-lookup"><span data-stu-id="bca1e-158">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="bca1e-159">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-159">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="bca1e-160">这会安装您需要运行 MVC 3 应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="bca1e-160">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="bca1e-161">本演练介绍如何使用 Web 平台安装程序来安装和配置所需的组件。</span><span class="sxs-lookup"><span data-stu-id="bca1e-161">This walkthrough describes the use of the Web Platform Installer to install and configure the required components.</span></span> <span data-ttu-id="bca1e-162">尽管不一定要使用 Web 平台安装程序，它通过简化了安装过程会自动检测的依赖关系以及确保始终获得最新的产品版本。</span><span class="sxs-lookup"><span data-stu-id="bca1e-162">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="bca1e-163">有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-163">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="bca1e-164">**若要安装必需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="bca1e-164">**To install the required products and components**</span></span>

1. <span data-ttu-id="bca1e-165">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-165">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="bca1e-166">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="bca1e-166">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bca1e-167">现在可以在任何时候从启动 Web 平台安装程序**启动**菜单。</span><span class="sxs-lookup"><span data-stu-id="bca1e-167">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="bca1e-168">为此，请在**启动**菜单上，单击**所有程序**，然后单击**Microsoft Web 平台安装程序**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-168">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="bca1e-169">在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-169">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="bca1e-170">在左侧和右侧的窗口中，在导航窗格中，单击**框架**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-170">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="bca1e-171">在中**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-171">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bca1e-172">你可能已安装.NET Framework 4.0 到 Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="bca1e-172">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="bca1e-173">如果已安装的产品或组件，Web 平台安装程序将此信息指示通过替换**外**按钮，其文本**已安装**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-173">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. <span data-ttu-id="bca1e-174">在中**ASP.NET MVC 3 (Visual Studio 2010)** 行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-174">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="bca1e-175">在导航窗格中，单击**Server**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-175">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="bca1e-176">在 **IIS 7 建议配置** 行中，单击 **添加** 。</span><span class="sxs-lookup"><span data-stu-id="bca1e-176">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="bca1e-177">在中**Web 部署工具 2.1**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-177">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="bca1e-178">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="bca1e-178">Click **Install**.</span></span> <span data-ttu-id="bca1e-179">Web 平台安装程序将显示产品列表&#x2014;以及任何关联的依赖关系&#x2014;安装，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="bca1e-179">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. <span data-ttu-id="bca1e-180">查看许可条款，如果同意条款，单击**我接受**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-180">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="bca1e-181">安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。</span><span class="sxs-lookup"><span data-stu-id="bca1e-181">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="bca1e-182">如果在安装 IIS 之前安装.NET Framework 4.0，您将需要运行[ASP.NET IIS 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)(aspnet\_regiis.exe) 若要向 IIS 注册 ASP.NET 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="bca1e-182">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="bca1e-183">如果不这样做，您会发现 IIS 将 （如 HTML 文件） 中提供静态内容没有任何问题，但它将返回**HTTP 错误 404.0-未找到**尝试浏览到 ASP.NET 内容时。</span><span class="sxs-lookup"><span data-stu-id="bca1e-183">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="bca1e-184">此过程可用于确保在注册 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="bca1e-184">You can use this procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="bca1e-185">**若要向 IIS 注册 ASP.NET 4.0**</span><span class="sxs-lookup"><span data-stu-id="bca1e-185">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="bca1e-186">单击**启动**，然后键入**命令提示符下**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-186">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="bca1e-187">在搜索结果中，右键单击**命令提示符**，然后单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-187">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="bca1e-188">在命令提示符窗口中， 导航到 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目录。</span><span class="sxs-lookup"><span data-stu-id="bca1e-188">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="bca1e-189">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="bca1e-189">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. <span data-ttu-id="bca1e-190">如果计划托管 64 位 web 应用程序，任何时候，则应该向 IIS 注册 ASP.NET 的 64 位版本。</span><span class="sxs-lookup"><span data-stu-id="bca1e-190">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="bca1e-191">为此，请在命令提示符窗口中，导航到 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目录。</span><span class="sxs-lookup"><span data-stu-id="bca1e-191">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="bca1e-192">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="bca1e-192">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

<span data-ttu-id="bca1e-193">很好的做法是，Windows 更新再次使用此时若要下载并安装新的产品和组件已安装所有可用更新。</span><span class="sxs-lookup"><span data-stu-id="bca1e-193">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="bca1e-194">配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="bca1e-194">Configure the IIS Website</span></span>

<span data-ttu-id="bca1e-195">可以将 web 内容部署到你的服务器之前，您需要创建和配置 IIS 网站来承载的内容。</span><span class="sxs-lookup"><span data-stu-id="bca1e-195">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="bca1e-196">Web 部署可以仅将 web 包部署到现有 IIS 网站;它不能为您创建的网站。</span><span class="sxs-lookup"><span data-stu-id="bca1e-196">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="bca1e-197">在高级别中，将需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="bca1e-197">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="bca1e-198">在文件系统来托管你的内容上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="bca1e-198">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="bca1e-199">创建 IIS 网站提供内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="bca1e-199">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="bca1e-200">授予读取权限的本地文件夹上的应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="bca1e-200">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="bca1e-201">尽管没有什么措施可以阻止您从内容部署到 IIS 中的默认网站，但不建议使用此方法用于测试或演示方案之外的任何内容。</span><span class="sxs-lookup"><span data-stu-id="bca1e-201">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="bca1e-202">若要模拟生产环境中，应使用特定于应用程序的要求的设置创建新的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="bca1e-202">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="bca1e-203">**若要创建和配置 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="bca1e-203">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="bca1e-204">在本地文件系统上创建一个文件夹以存储你的内容 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-204">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="bca1e-205">上**启动**菜单，依次指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-205">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="bca1e-206">在 IIS 管理器中，在**连接**窗格中，展开服务器节点 (例如， **TESTWEB1**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-206">In IIS Manager, in the **Connections** pane, expand the server node (for example, **TESTWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. <span data-ttu-id="bca1e-207">右键单击**站点**节点，并单击**添加网站**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-207">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="bca1e-208">在中**站点名称**框中，键入为 IIS 网站的名称 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-208">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="bca1e-209">在中**物理路径**框中，键入 （或浏览到） 到本地文件夹的路径 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-209">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="bca1e-210">在中**端口**框中，键入你想要托管网站的端口号 (例如， **85**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-210">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="bca1e-211">标准端口号是 80 用于 HTTP 和 HTTPS 的 443。</span><span class="sxs-lookup"><span data-stu-id="bca1e-211">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="bca1e-212">但是，如果托管该网站在端口 80 上的，你需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="bca1e-212">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="bca1e-213">将保留**主机名**框保留为空，除非你想要配置该网站的域名系统 (DNS) 记录，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-213">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="bca1e-214">在生产环境中，你将很可能想要托管你的网站在端口 80 上并配置主机标头，以及匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="bca1e-214">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="bca1e-215">在 IIS 7 中配置主机标头的详细信息，请参阅[为网站 (IIS 7) 配置主机标头](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-215">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="bca1e-216">Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[DNS 服务器概述](https://technet.microsoft.com/en-gb/library/cc770392.aspx)并[DNS 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-216">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="bca1e-217">在中**操作**窗格下**编辑站点**，单击**绑定**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-217">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="bca1e-218">在中**站点绑定**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-218">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. <span data-ttu-id="bca1e-219">在中**添加网站绑定**对话框中，将**IP 地址**并**端口**以匹配您现有的站点配置。</span><span class="sxs-lookup"><span data-stu-id="bca1e-219">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="bca1e-220">在中**主机名**框中，键入你的 web 服务器的名称 (例如， **TESTWEB1**)，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-220">In the **Host name** box, type the name of your web server (for example, **TESTWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="bca1e-221">第一个站点绑定使你可以访问站点使用的 IP 地址和端口在本地或`http://localhost:85`。</span><span class="sxs-lookup"><span data-stu-id="bca1e-221">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="bca1e-222">第二个站点绑定使你可以使用计算机名称在域上的其他计算机访问站点 (例如， http://testweb1:85)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-222">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://testweb1:85).</span></span>
13. <span data-ttu-id="bca1e-223">在中**站点绑定**对话框中，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-223">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="bca1e-224">在中**连接**窗格中，单击**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-224">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="bca1e-225">在中**应用程序池**窗格中，右键单击你的应用程序池的名称，然后单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-225">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="bca1e-226">默认情况下，应用程序池的名称将与你的网站的名称匹配 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-226">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="bca1e-227">在 **.NET Framework 版本** 列表中，选择 **.NET Framework v4.0.30319** ，然后单击 **确定** 。</span><span class="sxs-lookup"><span data-stu-id="bca1e-227">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="bca1e-228">示例解决方案需要.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="bca1e-228">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="bca1e-229">这不是必需的 Web 部署一般情况下。</span><span class="sxs-lookup"><span data-stu-id="bca1e-229">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="bca1e-230">为了使你的网站提供内容，应用程序池标识必须具有读取存储内容的本地文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="bca1e-230">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="bca1e-231">在 IIS 7.5 应用程序池以运行唯一的应用程序池标识 （与以前版本的 IIS，其中应用程序池通常运行使用网络服务帐户） 默认情况下。</span><span class="sxs-lookup"><span data-stu-id="bca1e-231">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="bca1e-232">应用程序池标识不是真实的用户帐户和未出现在任何用户或组的列表&#x2014;相反，它动态启动时创建的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="bca1e-232">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="bca1e-233">每个应用程序池标识添加到本地**IIS\_IUSRS**隐藏项的安全组。</span><span class="sxs-lookup"><span data-stu-id="bca1e-233">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="bca1e-234">若要授予对文件或文件夹上的应用程序池标识的权限，您有两个选项：</span><span class="sxs-lookup"><span data-stu-id="bca1e-234">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="bca1e-235">将权限分配给应用程序池标识直接，使用格式<strong>IIS AppPool\</strong ><em>[应用程序池名称]</em>(例如， <strong>IIS AppPool\DemoSite</strong>).</span><span class="sxs-lookup"><span data-stu-id="bca1e-235">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="bca1e-236">向其分配权限**IIS\_IUSRS**组。</span><span class="sxs-lookup"><span data-stu-id="bca1e-236">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="bca1e-237">最常用的方法是将权限分配给本地**IIS\_IUSRS**组，因为这种方法允许您更改应用程序池，而无需重新配置的文件系统权限。</span><span class="sxs-lookup"><span data-stu-id="bca1e-237">The most common approach is to assign permissions to the local **IIS\_IUSRS** group because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="bca1e-238">下一个过程中使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="bca1e-238">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="bca1e-239">在 IIS 7.5 的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-239">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="bca1e-240">**若要配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="bca1e-240">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="bca1e-241">在 Windows 资源管理器，浏览到本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="bca1e-241">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="bca1e-242">右键单击文件夹，然后依次**属性**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-242">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="bca1e-243">上**安全**选项卡上，单击**编辑**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-243">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="bca1e-244">单击**位置**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-244">Click **Locations**.</span></span> <span data-ttu-id="bca1e-245">在中**位置**对话框中，选择本地服务器，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-245">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. <span data-ttu-id="bca1e-246">在中**选择用户或组**对话框中，键入**IIS\_IUSRS**，单击**检查名称**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-246">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="bca1e-247">在中<strong>的权限</strong><em>[文件夹名称]</em>对话框中，请注意，新的组已分配<strong>读取&amp;执行</strong>，<strong>列出文件夹内容</strong>，并<strong>读取</strong>默认情况下的权限。</span><span class="sxs-lookup"><span data-stu-id="bca1e-247">In the <strong>Permissions for</strong><em>[folder name]</em>dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="bca1e-248">保留此保持不变，然后单击<strong>确定</strong>。</span><span class="sxs-lookup"><span data-stu-id="bca1e-248">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="bca1e-249">单击<strong>确定</strong>以关闭<em>[文件夹名称]</em><strong>属性</strong>对话框。</span><span class="sxs-lookup"><span data-stu-id="bca1e-249">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

<span data-ttu-id="bca1e-250">作为最后一项任务之前尝试将任何 web 包部署到你的服务器，你应确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="bca1e-250">As a final task before you attempt to deploy any web packages to your server, you should ensure that the Web Deployment Agent Service is running.</span></span> <span data-ttu-id="bca1e-251">在部署包从远程计算机时，Web 部署代理服务负责提取并安装包的内容。</span><span class="sxs-lookup"><span data-stu-id="bca1e-251">When you deploy a package from a remote computer, the Web Deployment Agent Service is responsible for extracting and installing the contents of the package.</span></span> <span data-ttu-id="bca1e-252">该服务在安装 Web 部署工具时，默认情况下启动，并在 Network Service 标识下运行。</span><span class="sxs-lookup"><span data-stu-id="bca1e-252">The service is started by default when you install the Web Deployment Tool and runs under the Network Service identity.</span></span>

<span data-ttu-id="bca1e-253">您可以检查服务是否正在运行多个不同的方式，在使用各种命令行实用程序或 Windows PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bca1e-253">You can check whether a service is running in multiple different ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="bca1e-254">此过程介绍了简单的基于 UI 的方法。</span><span class="sxs-lookup"><span data-stu-id="bca1e-254">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="bca1e-255">**若要检查 Web 部署代理服务正在运行**</span><span class="sxs-lookup"><span data-stu-id="bca1e-255">**To check that the Web Deployment Agent Service is running**</span></span>

1. <span data-ttu-id="bca1e-256">在“开始”  菜单上，指向“管理工具” ，然后单击“服务” 。</span><span class="sxs-lookup"><span data-stu-id="bca1e-256">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="bca1e-257">找到**Web 部署代理服务**行，并确认**状态**设置为**已启动**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-257">Locate the **Web Deployment Agent Service** row, and verify that the **Status** is set to **Started**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. <span data-ttu-id="bca1e-258">如果该服务尚未启动，请单击**启动**。</span><span class="sxs-lookup"><span data-stu-id="bca1e-258">If the service is not already started, click **Start**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="bca1e-259">配置防火墙例外</span><span class="sxs-lookup"><span data-stu-id="bca1e-259">Configure Firewall Exceptions</span></span>

<span data-ttu-id="bca1e-260">默认情况下，远程代理服务侦听 TCP 端口 80，在此 URL:</span><span class="sxs-lookup"><span data-stu-id="bca1e-260">By default, the Remote Agent Service listens on TCP port 80, at this URL:</span></span>

<http://servername.com/MSDEPLOYAGENTSERVICE>

<span data-ttu-id="bca1e-261">在大多数情况下，不需要任何其他防火墙规则配置为远程代理服务，因为 web 服务器通常侦听的端口 80 上的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="bca1e-261">In most cases, you won't need to configure any additional firewall rules for the Remote Agent Service because web servers typically listen for HTTP requests on port 80.</span></span> <span data-ttu-id="bca1e-262">如果自定义您的安装以在使用了非标准端口上侦听时，你将需要根据需要配置防火墙例外。</span><span class="sxs-lookup"><span data-stu-id="bca1e-262">If you customized your installation to listen on a nonstandard port, you'll need to configure firewall exceptions as required.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bca1e-263">结束语</span><span class="sxs-lookup"><span data-stu-id="bca1e-263">Conclusion</span></span>

<span data-ttu-id="bca1e-264">此时，你的 web 服务器已准备好接受并从远程计算机上安装 web 程序包。</span><span class="sxs-lookup"><span data-stu-id="bca1e-264">At this point, your web server is ready to accept and install web packages from a remote computer.</span></span> <span data-ttu-id="bca1e-265">在尝试部署到服务器的 web 应用程序之前，你可能想要检查这些关键点：</span><span class="sxs-lookup"><span data-stu-id="bca1e-265">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="bca1e-266">已向 IIS 注册 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="bca1e-266">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="bca1e-267">没有应用程序池标识具有读取访问权限的源文件夹的你的网站？</span><span class="sxs-lookup"><span data-stu-id="bca1e-267">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="bca1e-268">Web 部署代理服务是否正在运行？</span><span class="sxs-lookup"><span data-stu-id="bca1e-268">Is the Web Deployment Agent Service running?</span></span>

## <a name="further-reading"></a><span data-ttu-id="bca1e-269">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="bca1e-269">Further Reading</span></span>

<span data-ttu-id="bca1e-270">有关如何配置自定义 Microsoft Build Engine (MSBuild) 项目文件，以将 web 包部署到远程代理服务的指导，请参阅[配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="bca1e-270">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Remote Agent Service, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bca1e-271">[上一页](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span><span class="sxs-lookup"><span data-stu-id="bca1e-271">[Previous](scenario-configuring-a-production-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span></span>
