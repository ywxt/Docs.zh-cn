---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: "配置 Web 服务器的 Web 部署发布 （Web 部署处理程序） |Microsoft 文档"
author: jrjlee
description: "本主题介绍如何配置 Internet 信息服务 (IIS) web 服务器以支持 web 发布和部署使用 IIS Web 部署汉字..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: 81848c683fb9ddaa8942f030a520847a3c89fde0
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="94ca5-103">配置 Web 服务器的 Web 部署发布 （Web 部署处理程序）</span><span class="sxs-lookup"><span data-stu-id="94ca5-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>
====================
<span data-ttu-id="94ca5-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="94ca5-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="94ca5-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="94ca5-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="94ca5-106">本主题介绍如何配置 Internet 信息服务 (IIS) web 服务器以支持 web 发布和使用 IIS Web 部署处理程序的部署。</span><span class="sxs-lookup"><span data-stu-id="94ca5-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="94ca5-107">在处理 Web Deploy 2.0 或更高版本时，有三种主要方法可用于获取应用程序或 web 服务器上的站点。</span><span class="sxs-lookup"><span data-stu-id="94ca5-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="94ca5-108">你可以：</span><span class="sxs-lookup"><span data-stu-id="94ca5-108">You can:</span></span>
> 
> - <span data-ttu-id="94ca5-109">使用*Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="94ca5-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="94ca5-110">此方法需要较少配置 web 服务器，但你需要提供本地服务器管理员的凭据，以便将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="94ca5-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="94ca5-111">使用*Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="94ca5-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="94ca5-112">此方法更加复杂，并且需要更多的初始工作来设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="94ca5-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="94ca5-113">但是，当你使用此方法时，你可以配置 IIS 以允许非管理员用户执行部署。</span><span class="sxs-lookup"><span data-stu-id="94ca5-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="94ca5-114">Web 部署处理程序只是在 IIS 7 或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="94ca5-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="94ca5-115">使用*脱机部署*。</span><span class="sxs-lookup"><span data-stu-id="94ca5-115">Use *offline deployment*.</span></span> <span data-ttu-id="94ca5-116">此方法需要 web 服务器，最小配置，但服务器管理员必须手动复制到服务器上的 web 包并将其导入通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="94ca5-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="94ca5-117">主要功能的优点，这些方法的缺点的详细信息，请参阅[选择用于 Web 部署的右方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


<span data-ttu-id="94ca5-118">是，如果你想要允许非管理员用户将内容部署到特定的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="94ca5-118">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="94ca5-119">此方法通常是这些类型的方案中所需的：</span><span class="sxs-lookup"><span data-stu-id="94ca5-119">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="94ca5-120">过渡环境或生产环境，其中的人员或服务帐户的触发远程部署不太可能有权访问服务器管理员的凭据。</span><span class="sxs-lookup"><span data-stu-id="94ca5-120">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="94ca5-121">托管的环境中，你想要允许远程攻击者能够更新自己的网站，而不授予其 web 服务器 （或到其他任何人的网站的访问） 的完全控制。</span><span class="sxs-lookup"><span data-stu-id="94ca5-121">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="94ca5-122">在开发或测试方案中，或在较小的组织，使用服务器管理员凭据的部署内容通常是小于争议。</span><span class="sxs-lookup"><span data-stu-id="94ca5-122">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="94ca5-123">在这些情况下，配置 web 服务器以支持部署使用[Web 部署远程代理服务](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)提供更为直接的方法。</span><span class="sxs-lookup"><span data-stu-id="94ca5-123">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="94ca5-124">任务概述</span><span class="sxs-lookup"><span data-stu-id="94ca5-124">Task Overview</span></span>

<span data-ttu-id="94ca5-125">若要配置 web 服务器来接受和部署 web 包从远程计算机使用 Web 部署处理程序方法，你将需要：</span><span class="sxs-lookup"><span data-stu-id="94ca5-125">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="94ca5-126">创建或选择域用户帐户 （"非管理员用户"） 将用于执行部署其凭据。</span><span class="sxs-lookup"><span data-stu-id="94ca5-126">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="94ca5-127">安装 IIS 7.5，包括 Web 管理服务和基本身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="94ca5-127">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="94ca5-128">安装 Web 部署 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="94ca5-128">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="94ca5-129">配置 Web 管理服务，以允许远程连接，并启动服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-129">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="94ca5-130">创建一个 IIS 网站来承载部署的内容。</span><span class="sxs-lookup"><span data-stu-id="94ca5-130">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="94ca5-131">授予您在 IIS 管理器在网站上的非管理员用户权限。</span><span class="sxs-lookup"><span data-stu-id="94ca5-131">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="94ca5-132">请确保 Web 管理服务委派规则允许服务可以添加和更改网站内容使用你的非管理员用户帐户。</span><span class="sxs-lookup"><span data-stu-id="94ca5-132">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="94ca5-133">任何将防火墙配置为允许端口 8172 上的传入连接。</span><span class="sxs-lookup"><span data-stu-id="94ca5-133">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="94ca5-134">若要专门承载 ContactManager 示例解决方案，你将还需要：</span><span class="sxs-lookup"><span data-stu-id="94ca5-134">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="94ca5-135">安装.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="94ca5-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="94ca5-136">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="94ca5-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="94ca5-137">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="94ca5-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="94ca5-138">任务和本主题中的演练假定你刚开始使用干净服务器生成运行 Windows Server 2008 R2。</span><span class="sxs-lookup"><span data-stu-id="94ca5-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="94ca5-139">在继续之前，确保：</span><span class="sxs-lookup"><span data-stu-id="94ca5-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="94ca5-140">安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="94ca5-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="94ca5-141">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="94ca5-141">The server is domain-joined.</span></span>
- <span data-ttu-id="94ca5-142">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="94ca5-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="94ca5-143">有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="94ca5-144">有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="94ca5-145">安装产品和组件</span><span class="sxs-lookup"><span data-stu-id="94ca5-145">Install Products and Components</span></span>

<span data-ttu-id="94ca5-146">本部分将指导你完成 web 服务器上安装必需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="94ca5-146">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="94ca5-147">在开始之前，很好的做法是运行 Windows 更新，以确保你的服务器是完全最新。</span><span class="sxs-lookup"><span data-stu-id="94ca5-147">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="94ca5-148">在这种情况下，你需要安装以下操作：</span><span class="sxs-lookup"><span data-stu-id="94ca5-148">In this case, you need to install these things:</span></span>

- <span data-ttu-id="94ca5-149">**IIS 7 建议的配置**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-149">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="94ca5-150">这使**Web 服务器 (IIS)** web 服务器上的角色和安装的 IIS 模块和托管 ASP.NET 应用程序所需的组件组。</span><span class="sxs-lookup"><span data-stu-id="94ca5-150">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="94ca5-151">**IIS： 管理服务**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-151">**IIS: Management Service**.</span></span> <span data-ttu-id="94ca5-152">这将在 IIS 中安装 Web 管理服务 (WMSvc)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-152">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="94ca5-153">此服务启用的 IIS 网站远程管理，并公开给客户端的 Web 部署处理程序终结点。</span><span class="sxs-lookup"><span data-stu-id="94ca5-153">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="94ca5-154">**IIS： 基本身份验证**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-154">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="94ca5-155">这将安装 IIS 基本身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="94ca5-155">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="94ca5-156">此允许 Web 管理服务 (WMSvc) 进行身份验证你提供的凭据。</span><span class="sxs-lookup"><span data-stu-id="94ca5-156">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="94ca5-157">**Web 部署工具 2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-157">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="94ca5-158">这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="94ca5-158">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="94ca5-159">作为此过程的一部分，它将安装 Web 部署处理程序，并与 Web 管理服务集成它。</span><span class="sxs-lookup"><span data-stu-id="94ca5-159">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="94ca5-160">**.NET framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-160">**.NET Framework 4.0**.</span></span> <span data-ttu-id="94ca5-161">这是运行在此版本的.NET Framework 生成的应用程序所需要的。</span><span class="sxs-lookup"><span data-stu-id="94ca5-161">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="94ca5-162">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-162">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="94ca5-163">这将安装你需要运行 MVC 3 应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="94ca5-163">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="94ca5-164">本演练介绍了利用 Web 平台安装程序来安装和配置各种组件。</span><span class="sxs-lookup"><span data-stu-id="94ca5-164">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="94ca5-165">尽管你无需使用 Web 平台安装程序，它，从而简化安装过程自动检测依赖关系并确保你始终获得最新的产品版本。</span><span class="sxs-lookup"><span data-stu-id="94ca5-165">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="94ca5-166">有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-166">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="94ca5-167">**若要安装必需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="94ca5-167">**To install the required products and components**</span></span>

1. <span data-ttu-id="94ca5-168">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-168">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="94ca5-169">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="94ca5-169">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94ca5-170">你现在可以随时从启动 Web 平台安装程序**启动**菜单。</span><span class="sxs-lookup"><span data-stu-id="94ca5-170">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="94ca5-171">若要执行此操作，在**启动**菜单上，单击**所有程序**，然后单击**Microsoft Web 平台安装程序**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-171">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="94ca5-172">在顶部**Web Platform Installer 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-172">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="94ca5-173">在左侧的窗口中，在导航窗格中，单击**框架**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-173">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="94ca5-174">在**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，请单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-174">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94ca5-175">你可能已安装.NET Framework 4.0 通过 Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="94ca5-175">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="94ca5-176">如果已安装的产品或组件，则 Web 平台安装程序将指示这一点通过将**添加**按钮，其文本**已安装**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-176">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="94ca5-177">在**ASP.NET MVC 3 (Visual Studio 2010)**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-177">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="94ca5-178">在导航窗格中，单击**服务器**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-178">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="94ca5-179">在**IIS 7 建议配置**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-179">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="94ca5-180">在**Web 部署工具 2.1**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-180">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="94ca5-181">在**IIS： 基本身份验证**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-181">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="94ca5-182">在**IIS： 管理服务**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-182">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="94ca5-183">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="94ca5-183">Click **Install**.</span></span> <span data-ttu-id="94ca5-184">Web 平台安装程序将显示列表的产品和 #x 2014年; 以及要安装任何关联的依赖关系 （&） #x 2014; 并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="94ca5-184">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="94ca5-185">查看许可条款，然后如果同意条款，单击**我接受**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-185">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="94ca5-186">安装完成后，单击**完成**，然后关闭**Web Platform Installer 3.0**窗口。</span><span class="sxs-lookup"><span data-stu-id="94ca5-186">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="94ca5-187">如果你安装.NET Framework 4.0 安装 IIS 之前，你将需要运行[ASP.NET IIS 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)(aspnet\_regiis.exe) 以向 IIS 注册 ASP.NET 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="94ca5-187">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="94ca5-188">如果不这样做，你将找到 IIS 将 （如 HTML 文件） 中提供静态内容而无需任何问题，但它将返回**HTTP 错误 404.0-未找到**当你尝试浏览到 ASP.NET 内容。</span><span class="sxs-lookup"><span data-stu-id="94ca5-188">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="94ca5-189">下一步过程可用于确保注册 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="94ca5-189">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="94ca5-190">**若要向 IIS 注册 ASP.NET 4.0**</span><span class="sxs-lookup"><span data-stu-id="94ca5-190">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="94ca5-191">单击**启动**，然后键入**命令提示符**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-191">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="94ca5-192">在搜索结果中，右键单击**命令提示符**，然后单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-192">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="94ca5-193">在命令提示符窗口中，导航到**%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目录。</span><span class="sxs-lookup"><span data-stu-id="94ca5-193">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="94ca5-194">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="94ca5-194">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="94ca5-195">如果你计划到托管 64 位 web 应用程序的任何时刻，你应该向 IIS 注册 ASP.NET 的 64 位版本。</span><span class="sxs-lookup"><span data-stu-id="94ca5-195">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="94ca5-196">为此，请在命令提示符窗口中，导航到**%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目录。</span><span class="sxs-lookup"><span data-stu-id="94ca5-196">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="94ca5-197">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="94ca5-197">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="94ca5-198">作为一种良好做法，Windows Update 再次使用此时若要下载并安装的新产品和组件已安装所有可用更新。</span><span class="sxs-lookup"><span data-stu-id="94ca5-198">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="94ca5-199">配置 Web 管理服务</span><span class="sxs-lookup"><span data-stu-id="94ca5-199">Configure the Web Management Service</span></span>

<span data-ttu-id="94ca5-200">现在，你已安装所需的一切下, 一步是在 IIS 中配置 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-200">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="94ca5-201">在高级别中，你将需要完成这些任务：</span><span class="sxs-lookup"><span data-stu-id="94ca5-201">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="94ca5-202">启用基本身份验证在服务器级别。</span><span class="sxs-lookup"><span data-stu-id="94ca5-202">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="94ca5-203">配置 Web 管理服务，以便接受远程连接。</span><span class="sxs-lookup"><span data-stu-id="94ca5-203">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="94ca5-204">启动 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-204">Start the Web Management Service.</span></span>
- <span data-ttu-id="94ca5-205">检查所需的 Web 管理服务委派规则位于的位置。</span><span class="sxs-lookup"><span data-stu-id="94ca5-205">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="94ca5-206">**若要配置 Web 管理服务**</span><span class="sxs-lookup"><span data-stu-id="94ca5-206">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="94ca5-207">上**启动**菜单上，指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-207">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="94ca5-208">在 IIS 管理器中，在**连接**窗格中，单击服务器节点 (例如， **STAGEWEB1**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-208">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="94ca5-209">在中心窗格中，在**IIS**，双击**身份验证**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-209">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image4.png)
4. <span data-ttu-id="94ca5-210">右键单击**基本身份验证**，然后单击**启用**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-210">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="94ca5-211">在**连接**窗格中，单击服务器节点，再次以返回到顶级的设置。</span><span class="sxs-lookup"><span data-stu-id="94ca5-211">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="94ca5-212">在中心窗格中，在**管理**，双击**管理服务**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-212">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="94ca5-213">在中心窗格中，选择**启用远程连接**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-213">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94ca5-214">如果已在运行 Web 管理服务，你将需要首先停止。</span><span class="sxs-lookup"><span data-stu-id="94ca5-214">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="94ca5-215">在**操作**窗格中，单击**启动**启动 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-215">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="94ca5-216">如果系统提示你保存设置，请单击**是**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-216">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="94ca5-217">你可能还想要配置为自动启动服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-217">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="94ca5-218">若要执行此操作，打开服务控制台中，右键单击**Web 管理服务**，然后单击**属性**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-218">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="94ca5-219">在**启动类型**下拉列表中，选择**自动**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-219">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="94ca5-220">在**连接**窗格中，单击服务器节点，再次以返回到顶级的设置。</span><span class="sxs-lookup"><span data-stu-id="94ca5-220">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="94ca5-221">在中心窗格中，在**管理**，双击**管理服务的委派**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-221">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="94ca5-222">验证中间窗格中包含一组规则。</span><span class="sxs-lookup"><span data-stu-id="94ca5-222">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="94ca5-223">这些规则允许授权的 Web 管理服务用户使用各种 Web Deploy 提供程序。</span><span class="sxs-lookup"><span data-stu-id="94ca5-223">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="94ca5-224">例如，若要将 web 应用程序和内容部署到 IIS 通过 Web 部署处理程序，则必须将允许所有经过身份验证 Web 管理服务用户使用的委派规则**contentPath**和**iisApp**提供程序 （你可以看到的屏幕截图中的最后一个规则）。</span><span class="sxs-lookup"><span data-stu-id="94ca5-224">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="94ca5-225">如果你按照本主题中介绍的顺序安装产品和组件，Web 部署的最新版本自动应将所有所需的委派规则添加到 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-225">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="94ca5-226">如果管理服务的委派页未显示任何规则，你需要自行创建。</span><span class="sxs-lookup"><span data-stu-id="94ca5-226">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="94ca5-227">有关如何执行此操作的说明，请参阅[配置 Web 部署处理](https://go.microsoft.com/?linkid=9805124)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-227">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="94ca5-228">在**连接**窗格中，单击服务器节点，再次以返回到顶级的设置。</span><span class="sxs-lookup"><span data-stu-id="94ca5-228">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="94ca5-229">创建和配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="94ca5-229">Create and Configure an IIS Website</span></span>

<span data-ttu-id="94ca5-230">可以将 web 内容部署到你的服务器之前，你需要创建和配置 IIS 网站来承载的内容。</span><span class="sxs-lookup"><span data-stu-id="94ca5-230">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="94ca5-231">Web 部署可以仅将 web 包部署到现有 IIS 网站;它不能为你创建的网站。</span><span class="sxs-lookup"><span data-stu-id="94ca5-231">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="94ca5-232">你还需要执行小的额外配置，以允许你远程部署内容的非管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="94ca5-232">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="94ca5-233">在高级别中，你将需要完成这些任务：</span><span class="sxs-lookup"><span data-stu-id="94ca5-233">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="94ca5-234">在要承载内容的文件系统上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="94ca5-234">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="94ca5-235">创建 IIS 网站来提供的内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="94ca5-235">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="94ca5-236">授予读取权限的本地文件夹上的应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="94ca5-236">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="94ca5-237">授予必要的 IIS 权限来将部署 web 应用程序的域帐户。</span><span class="sxs-lookup"><span data-stu-id="94ca5-237">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="94ca5-238">尽管没有执行任何操作停止您从将内容部署到 IIS 中的默认网站，但不建议使用此方法对于测试或演示方案以外的任何内容。</span><span class="sxs-lookup"><span data-stu-id="94ca5-238">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="94ca5-239">若要模拟生产环境，应使用特定于你的应用程序的要求的设置创建新的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="94ca5-239">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="94ca5-240">**若要创建的 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="94ca5-240">**To create an IIS website**</span></span>

1. <span data-ttu-id="94ca5-241">在本地文件系统上，创建一个文件夹来存储你的内容 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-241">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="94ca5-242">上**启动**菜单上，指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-242">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="94ca5-243">在 IIS 管理器中，在**连接**窗格中，展开服务器节点 (例如， **STAGEWEB1**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-243">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="94ca5-244">右键单击**站点**节点，，然后单击**添加网站**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-244">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="94ca5-245">在**站点名称**框中，键入为 IIS 网站的名称 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-245">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="94ca5-246">在**物理路径**框中，键入 （或浏览到） 您的本地文件夹的路径 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-246">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="94ca5-247">在**端口**框中，键入你要在其托管网站的端口号 (例如， **85**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-247">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="94ca5-248">标准端口号为 80 用于 HTTP 和 HTTPS 的 443。</span><span class="sxs-lookup"><span data-stu-id="94ca5-248">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="94ca5-249">但是，如果承载此网站在端口 80 上的，你将需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="94ca5-249">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="94ca5-250">保留**主机名**框保留为空，除非你想要配置该网站的域名系统 (DNS) 记录，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-250">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="94ca5-251">在生产环境中，你可能需要托管你的网站在端口 80 上并配置主机标头，以及匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="94ca5-251">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="94ca5-252">在 IIS 7 中配置主机标头的详细信息，请参阅[网站 (IIS 7) 配置主机头](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-252">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="94ca5-253">Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[DNS 服务器概述](https://technet.microsoft.com/en-gb/library/cc770392.aspx)和[DNS 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-253">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="94ca5-254">在**操作**窗格中，在**编辑站点**，单击**绑定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-254">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="94ca5-255">在**站点绑定**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-255">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="94ca5-256">在**添加网站绑定**对话框中，设置**IP 地址**和**端口**以与你现有的站点配置匹配。</span><span class="sxs-lookup"><span data-stu-id="94ca5-256">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="94ca5-257">在**主机名**框中，键入你的 web 服务器的名称 (例如， **STAGEWEB1**)，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-257">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="94ca5-258">第一个站点绑定允许你访问本地使用的 IP 地址和端口的网站或`http://localhost:85`。</span><span class="sxs-lookup"><span data-stu-id="94ca5-258">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="94ca5-259">第二个站点绑定，可从其他计算机上使用计算机名称 (例如，http://stageweb1:85) 的域中访问站点。</span><span class="sxs-lookup"><span data-stu-id="94ca5-259">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="94ca5-260">在**站点绑定**对话框中，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-260">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="94ca5-261">在**连接**窗格中，单击**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-261">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="94ca5-262">在**应用程序池**窗格中，右键单击应用程序池的名称，然后单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-262">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="94ca5-263">默认情况下，应用程序池的名称将匹配你的网站的名称 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-263">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="94ca5-264">在**.NET Framework 版本**列表中，选择**.NET Framework v4.0.30319**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-264">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image14.png)

    > [!NOTE]
    > <span data-ttu-id="94ca5-265">示例解决方案需要.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="94ca5-265">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="94ca5-266">这是不要求用于 Web 部署一般情况下。</span><span class="sxs-lookup"><span data-stu-id="94ca5-266">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="94ca5-267">为了使你的网站以提供内容，应用程序池标识必须具有读取权限的本地文件夹，将内容存储。</span><span class="sxs-lookup"><span data-stu-id="94ca5-267">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="94ca5-268">在 IIS 7.5 中应用程序池具有唯一的应用程序池标识默认运行 （与以前版本的 IIS，其中应用程序池将通常使用的网络服务帐户运行）。</span><span class="sxs-lookup"><span data-stu-id="94ca5-268">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="94ca5-269">应用程序池标识不是真实的用户帐户和未显示于的用户或组和 #x 2014年任何列表; 相反，它动态启动时创建的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="94ca5-269">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="94ca5-270">每个应用程序池标识添加到本地**IIS\_IUSRS**作为隐藏的项的安全组。</span><span class="sxs-lookup"><span data-stu-id="94ca5-270">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="94ca5-271">若要授予对应用程序池标识的文件或文件夹上的权限，你有两个选项：</span><span class="sxs-lookup"><span data-stu-id="94ca5-271">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="94ca5-272">将权限分配给应用程序池标识直接，使用格式**IIS 应用程序池\***[应用程序池名称] * (例如， **IIS AppPool\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-272">Assign permissions to the application pool identity directly, using the format **IIS AppPool\***[application pool name]*(for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="94ca5-273">向其分配权限**IIS\_IUSRS**组。</span><span class="sxs-lookup"><span data-stu-id="94ca5-273">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="94ca5-274">最常用的方法是将权限分配给本地**IIS\_IUSRS**组，因为这种方法可让你更改应用程序池，而不用重新配置文件系统权限。</span><span class="sxs-lookup"><span data-stu-id="94ca5-274">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="94ca5-275">下一个过程中使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="94ca5-275">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="94ca5-276">IIS 7.5 中的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-276">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="94ca5-277">**若要配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="94ca5-277">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="94ca5-278">在 Windows 资源管理器，浏览到你的本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="94ca5-278">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="94ca5-279">右键单击文件夹，并依次**属性**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-279">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="94ca5-280">上**安全**选项卡上，单击**编辑**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-280">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="94ca5-281">单击**位置**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-281">Click **Locations**.</span></span> <span data-ttu-id="94ca5-282">在**位置**对话框中，选择本地服务器，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-282">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="94ca5-283">在**选择用户或组**对话框中，键入**IIS\_IUSRS**，单击**检查名称**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-283">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="94ca5-284">在 **权限 * * * [文件夹名称]*对话框中，请注意，在分配新组**读取&amp;执行**，**列出文件夹内容**，和**读取**默认情况下的权限。</span><span class="sxs-lookup"><span data-stu-id="94ca5-284">In the **Permissions for***[folder name]* dialog box, notice that the new group has been assigned the **Read &amp; execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="94ca5-285">保留此保持不变，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-285">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="94ca5-286">单击**确定**关闭*[文件夹名称] * * * 属性** 对话框。</span><span class="sxs-lookup"><span data-stu-id="94ca5-286">Click **OK** to close the *[folder name]***Properties** dialog box.</span></span>

<span data-ttu-id="94ca5-287">作为最后一项任务，你必须授予非管理员用户部署内容将使用其凭据的适当的权限。</span><span class="sxs-lookup"><span data-stu-id="94ca5-287">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="94ca5-288">此用户需要远程将内容部署到你的网站的权限。</span><span class="sxs-lookup"><span data-stu-id="94ca5-288">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="94ca5-289">**若要配置的 IIS 网站权限的非管理员域用户**</span><span class="sxs-lookup"><span data-stu-id="94ca5-289">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="94ca5-290">在 IIS 管理器中，在**连接**窗格中，右键单击你网站的节点 (例如， **DemoSite**)，指向**部署**，然后单击**配置 Web部署发布更改**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-290">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="94ca5-291">在**配置 Web 部署发布**对话框中，右侧**选择要授予发布权限的用户**列表中，单击省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="94ca5-291">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="94ca5-292">在**允许用户**对话框框中，键入你想要使用以部署内容，然后单击的帐户的域和用户**确定**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-292">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="94ca5-293">在**配置 Web 部署发布**对话框中，单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-293">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="94ca5-294">此操作执行一个步骤中的两个关键功能。</span><span class="sxs-lookup"><span data-stu-id="94ca5-294">This operation performs two key functions in one step.</span></span> <span data-ttu-id="94ca5-295">首先，它会根据上一节中检查委派规则授予用户权限来修改 Web 管理服务，通过远程网站。</span><span class="sxs-lookup"><span data-stu-id="94ca5-295">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="94ca5-296">其次，它会授予用户的网站，这样用户就可以添加、 修改和设置对网站内容的权限的源文件夹具有完全控制。</span><span class="sxs-lookup"><span data-stu-id="94ca5-296">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="94ca5-297">在**配置 Web 部署发布**对话框中，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="94ca5-297">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="94ca5-298">配置防火墙例外</span><span class="sxs-lookup"><span data-stu-id="94ca5-298">Configure Firewall Exceptions</span></span>

<span data-ttu-id="94ca5-299">默认情况下，IIS Web 管理服务侦听 TCP 端口 8172。</span><span class="sxs-lookup"><span data-stu-id="94ca5-299">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="94ca5-300">如果 web 服务器上启用 Windows 防火墙，你将需要创建新入站的规则，以允许 TCP 端口 8172 上的流量 （默认情况下，在 Windows 防火墙中允许所有出站流量）。</span><span class="sxs-lookup"><span data-stu-id="94ca5-300">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="94ca5-301">如果你使用第三方防火墙，你将需要创建规则以允许流量。</span><span class="sxs-lookup"><span data-stu-id="94ca5-301">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="94ca5-302">方向</span><span class="sxs-lookup"><span data-stu-id="94ca5-302">Direction</span></span> | <span data-ttu-id="94ca5-303">从端口</span><span class="sxs-lookup"><span data-stu-id="94ca5-303">From Port</span></span> | <span data-ttu-id="94ca5-304">到端口</span><span class="sxs-lookup"><span data-stu-id="94ca5-304">To Port</span></span> | <span data-ttu-id="94ca5-305">端口类型</span><span class="sxs-lookup"><span data-stu-id="94ca5-305">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94ca5-306">入站</span><span class="sxs-lookup"><span data-stu-id="94ca5-306">Inbound</span></span> | <span data-ttu-id="94ca5-307">任意</span><span class="sxs-lookup"><span data-stu-id="94ca5-307">Any</span></span> | <span data-ttu-id="94ca5-308">8172</span><span class="sxs-lookup"><span data-stu-id="94ca5-308">8172</span></span> | <span data-ttu-id="94ca5-309">TCP</span><span class="sxs-lookup"><span data-stu-id="94ca5-309">TCP</span></span> |
| <span data-ttu-id="94ca5-310">出站</span><span class="sxs-lookup"><span data-stu-id="94ca5-310">Outbound</span></span> | <span data-ttu-id="94ca5-311">8172</span><span class="sxs-lookup"><span data-stu-id="94ca5-311">8172</span></span> | <span data-ttu-id="94ca5-312">任意</span><span class="sxs-lookup"><span data-stu-id="94ca5-312">Any</span></span> | <span data-ttu-id="94ca5-313">TCP</span><span class="sxs-lookup"><span data-stu-id="94ca5-313">TCP</span></span> |
  

<span data-ttu-id="94ca5-314">在 Windows 防火墙中配置规则的详细信息，请参阅[配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-314">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="94ca5-315">有关第三方防火墙，请参阅产品文档。</span><span class="sxs-lookup"><span data-stu-id="94ca5-315">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="94ca5-316">结束语</span><span class="sxs-lookup"><span data-stu-id="94ca5-316">Conclusion</span></span>

<span data-ttu-id="94ca5-317">你的 web 服务器现在应该已准备好接受远程部署到 Web 部署处理程序中通过 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="94ca5-317">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="94ca5-318">在尝试部署到服务器的 web 应用程序之前，你可能想要检查这些要点：</span><span class="sxs-lookup"><span data-stu-id="94ca5-318">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="94ca5-319">已启用了在 IIS 中的服务器级别的基本身份验证？</span><span class="sxs-lookup"><span data-stu-id="94ca5-319">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="94ca5-320">已启用远程连接到 Web 管理服务？</span><span class="sxs-lookup"><span data-stu-id="94ca5-320">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="94ca5-321">已启动 Web 管理服务？</span><span class="sxs-lookup"><span data-stu-id="94ca5-321">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="94ca5-322">是否有管理服务委派规则就地？</span><span class="sxs-lookup"><span data-stu-id="94ca5-322">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="94ca5-323">应用程序池标识没有读取访问权限的源文件夹的你的网站？</span><span class="sxs-lookup"><span data-stu-id="94ca5-323">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="94ca5-324">非管理员用户帐户是否在 IIS 中拥有站点级别的权限？</span><span class="sxs-lookup"><span data-stu-id="94ca5-324">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="94ca5-325">你的防火墙是否允许传入连接到服务器的 TCP 端口 8172？</span><span class="sxs-lookup"><span data-stu-id="94ca5-325">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="94ca5-326">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="94ca5-326">Further Reading</span></span>

<span data-ttu-id="94ca5-327">有关如何配置自定义的 Microsoft Build Engine (MSBuild) 项目文件，将 web 包部署到 Web 部署处理程序的指南，请参阅[配置为目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="94ca5-327">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="94ca5-328">[上一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[下一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="94ca5-328">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
