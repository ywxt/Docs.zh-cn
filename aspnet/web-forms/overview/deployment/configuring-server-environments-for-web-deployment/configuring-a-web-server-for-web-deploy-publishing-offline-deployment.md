---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 配置 Web 服务器的 Web 部署发布 （离线部署） |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置 IIS web 服务器以支持脱机 web 发布和部署。 当你处理的 Internet Information Services (我...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: 555b4b3c79d8efc641b1c179482993371735dbe2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397572"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="a1086-104">配置用于 Web 部署发布 （离线部署） 的 Web 服务器</span><span class="sxs-lookup"><span data-stu-id="a1086-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>
====================
<span data-ttu-id="a1086-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a1086-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a1086-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a1086-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a1086-107">本主题介绍如何配置 IIS web 服务器以支持脱机 web 发布和部署。</span><span class="sxs-lookup"><span data-stu-id="a1086-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="a1086-108">使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取你的应用程序或 web 服务器上的站点。</span><span class="sxs-lookup"><span data-stu-id="a1086-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="a1086-109">你可以：</span><span class="sxs-lookup"><span data-stu-id="a1086-109">You can:</span></span>
> 
> - <span data-ttu-id="a1086-110">使用*Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="a1086-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="a1086-111">这种方法需要较少配置 web 服务器，但您需要提供的本地服务器管理员凭据才能将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="a1086-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="a1086-112">使用*Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="a1086-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="a1086-113">这种方法更复杂，需要更多的初始工作来设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="a1086-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="a1086-114">但是，在使用此方法时，你可以配置 IIS 以允许非管理员用户来执行部署。</span><span class="sxs-lookup"><span data-stu-id="a1086-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="a1086-115">Web 部署处理程序只是在 IIS 7 或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="a1086-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="a1086-116">使用*离线部署*。</span><span class="sxs-lookup"><span data-stu-id="a1086-116">Use *offline deployment*.</span></span> <span data-ttu-id="a1086-117">这种方法需要 web 服务器的最低配置，但服务器管理员必须手动复制到服务器上的 web 包并将其导入通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="a1086-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="a1086-118">主要功能、 优势和一种方法的缺点的详细信息，请参阅[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a1086-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


<span data-ttu-id="a1086-119">是，如果你的网络基础结构或安全限制阻止远程部署。</span><span class="sxs-lookup"><span data-stu-id="a1086-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="a1086-120">这是最有可能出现这种情况在 web 服务器是独立的面向 Internet 的生产环境中，&#x2014;以物理方式或通过防火墙和子网&#x2014;服务器基础结构的其余部分。</span><span class="sxs-lookup"><span data-stu-id="a1086-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="a1086-121">显然，此方法变得不够理想，如果 web 应用程序会定期更新。</span><span class="sxs-lookup"><span data-stu-id="a1086-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="a1086-122">如果您的基础结构允许，可能想要启用远程部署，请考虑使用 Web 部署处理程序或 Web 部署远程代理服务。</span><span class="sxs-lookup"><span data-stu-id="a1086-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a1086-123">任务概述</span><span class="sxs-lookup"><span data-stu-id="a1086-123">Task Overview</span></span>

<span data-ttu-id="a1086-124">若要配置 web 服务器以支持脱机导入和部署 web 包，您将需要：</span><span class="sxs-lookup"><span data-stu-id="a1086-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="a1086-125">安装 IIS 7.5 和 IIS 7 建议的配置。</span><span class="sxs-lookup"><span data-stu-id="a1086-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="a1086-126">安装 Web 部署 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="a1086-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="a1086-127">创建一个 IIS 网站来承载部署的内容。</span><span class="sxs-lookup"><span data-stu-id="a1086-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="a1086-128">禁用 Web 部署代理服务。</span><span class="sxs-lookup"><span data-stu-id="a1086-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="a1086-129">若要专门托管示例解决方案，还需要为：</span><span class="sxs-lookup"><span data-stu-id="a1086-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="a1086-130">安装.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="a1086-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="a1086-131">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="a1086-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="a1086-132">本主题将演示如何执行每个这些过程。</span><span class="sxs-lookup"><span data-stu-id="a1086-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="a1086-133">任务和本主题中的演练假定您正在使用运行 Windows Server 2008 R2 的全新服务器内部版本。</span><span class="sxs-lookup"><span data-stu-id="a1086-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="a1086-134">在继续之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="a1086-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="a1086-135">安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="a1086-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="a1086-136">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="a1086-136">The server is domain-joined.</span></span>
- <span data-ttu-id="a1086-137">在服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="a1086-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="a1086-138">有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1086-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="a1086-139">有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1086-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="a1086-140">安装的产品和组件</span><span class="sxs-lookup"><span data-stu-id="a1086-140">Install Products and Components</span></span>

<span data-ttu-id="a1086-141">本部分将指导您完成在 web 服务器上安装所需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="a1086-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="a1086-142">在开始之前，一个好的做法是运行 Windows 更新，以确保你的服务器是完全保持最新。</span><span class="sxs-lookup"><span data-stu-id="a1086-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="a1086-143">在这种情况下，你需要安装以下事项：</span><span class="sxs-lookup"><span data-stu-id="a1086-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="a1086-144">**IIS 7 推荐配置**。</span><span class="sxs-lookup"><span data-stu-id="a1086-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="a1086-145">这使得**Web 服务器 (IIS)** 角色在 web 服务器上的和安装的 IIS 模块和托管的 ASP.NET 应用程序所需的组件组。</span><span class="sxs-lookup"><span data-stu-id="a1086-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="a1086-146">**.NET framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="a1086-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="a1086-147">这是运行此版本的.NET Framework 生成的应用程序所需要的。</span><span class="sxs-lookup"><span data-stu-id="a1086-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="a1086-148">**Web 部署工具 2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="a1086-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="a1086-149">这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="a1086-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="a1086-150">Web 部署与 IIS 集成，并允许您导入和导出 web 包。</span><span class="sxs-lookup"><span data-stu-id="a1086-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="a1086-151">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="a1086-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="a1086-152">这会安装您需要运行 MVC 3 应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="a1086-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="a1086-153">本演练介绍如何使用 Web 平台安装程序来安装和配置各种组件。</span><span class="sxs-lookup"><span data-stu-id="a1086-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="a1086-154">尽管不一定要使用 Web 平台安装程序，它通过简化了安装过程会自动检测的依赖关系以及确保始终获得最新的产品版本。</span><span class="sxs-lookup"><span data-stu-id="a1086-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="a1086-155">有关详细信息，请参阅[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="a1086-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="a1086-156">**若要安装必需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="a1086-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="a1086-157">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="a1086-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="a1086-158">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="a1086-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1086-159">现在可以在任何时候从启动 Web 平台安装程序**启动**菜单。</span><span class="sxs-lookup"><span data-stu-id="a1086-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="a1086-160">为此，请在**启动**菜单上，单击**所有程序**，然后单击**Microsoft Web 平台安装程序**。</span><span class="sxs-lookup"><span data-stu-id="a1086-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="a1086-161">在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="a1086-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="a1086-162">在左侧和右侧的窗口中，在导航窗格中，单击**框架**。</span><span class="sxs-lookup"><span data-stu-id="a1086-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="a1086-163">在中**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1086-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1086-164">你可能已安装.NET Framework 4.0 到 Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="a1086-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="a1086-165">如果已安装的产品或组件，Web 平台安装程序将此信息指示通过替换**外**按钮，其文本**已安装**。</span><span class="sxs-lookup"><span data-stu-id="a1086-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="a1086-166">在中**ASP.NET MVC 3 (Visual Studio 2010)** 行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1086-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="a1086-167">在导航窗格中，单击**Server**。</span><span class="sxs-lookup"><span data-stu-id="a1086-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="a1086-168">在 **IIS 7 建议配置** 行中，单击 **添加** 。</span><span class="sxs-lookup"><span data-stu-id="a1086-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="a1086-169">在中**Web 部署工具 2.1**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1086-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="a1086-170">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="a1086-170">Click **Install**.</span></span> <span data-ttu-id="a1086-171">Web 平台安装程序将显示产品列表&#x2014;以及任何关联的依赖关系&#x2014;安装，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="a1086-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="a1086-172">查看许可条款，如果同意条款，单击**我接受**。</span><span class="sxs-lookup"><span data-stu-id="a1086-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="a1086-173">安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。</span><span class="sxs-lookup"><span data-stu-id="a1086-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="a1086-174">如果在安装 IIS 之前安装.NET Framework 4.0，您将需要运行[ASP.NET IIS 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)(aspnet\_regiis.exe) 若要向 IIS 注册 ASP.NET 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="a1086-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="a1086-175">如果不这样做，您会发现 IIS 将 （如 HTML 文件） 中提供静态内容没有任何问题，但它将返回**HTTP 错误 404.0-未找到**尝试浏览到 ASP.NET 内容时。</span><span class="sxs-lookup"><span data-stu-id="a1086-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="a1086-176">下一步过程可用于确保在注册 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="a1086-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="a1086-177">**若要向 IIS 注册 ASP.NET 4.0**</span><span class="sxs-lookup"><span data-stu-id="a1086-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="a1086-178">单击**启动**，然后键入**命令提示符下**。</span><span class="sxs-lookup"><span data-stu-id="a1086-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="a1086-179">在搜索结果中，右键单击**命令提示符**，然后单击**以管理员身份运行**。</span><span class="sxs-lookup"><span data-stu-id="a1086-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="a1086-180">在命令提示符窗口中， 导航到 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目录。</span><span class="sxs-lookup"><span data-stu-id="a1086-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="a1086-181">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="a1086-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="a1086-182">如果计划托管 64 位 web 应用程序，任何时候，则应该向 IIS 注册 ASP.NET 的 64 位版本。</span><span class="sxs-lookup"><span data-stu-id="a1086-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="a1086-183">为此，请在命令提示符窗口中，导航到 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目录。</span><span class="sxs-lookup"><span data-stu-id="a1086-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="a1086-184">键入以下命令，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="a1086-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="a1086-185">很好的做法是，Windows 更新再次使用此时若要下载并安装新的产品和组件已安装所有可用更新。</span><span class="sxs-lookup"><span data-stu-id="a1086-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="a1086-186">配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="a1086-186">Configure the IIS Website</span></span>

<span data-ttu-id="a1086-187">可以将 web 内容部署到你的服务器之前，您需要创建和配置 IIS 网站来承载的内容。</span><span class="sxs-lookup"><span data-stu-id="a1086-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="a1086-188">Web 部署可以仅将 web 包部署到现有 IIS 网站;它不能为您创建的网站。</span><span class="sxs-lookup"><span data-stu-id="a1086-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="a1086-189">在高级别中，将需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="a1086-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="a1086-190">在文件系统来托管你的内容上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="a1086-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="a1086-191">创建 IIS 网站提供内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="a1086-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="a1086-192">授予读取权限的本地文件夹上的应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="a1086-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="a1086-193">尽管没有什么措施可以阻止您从内容部署到 IIS 中的默认网站，但不建议使用此方法用于测试或演示方案之外的任何内容。</span><span class="sxs-lookup"><span data-stu-id="a1086-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="a1086-194">若要模拟生产环境中，应使用特定于应用程序的要求的设置创建新的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="a1086-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="a1086-195">**若要创建和配置 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="a1086-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="a1086-196">在本地文件系统上创建一个文件夹以存储你的内容 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="a1086-197">上**启动**菜单，依次指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**。</span><span class="sxs-lookup"><span data-stu-id="a1086-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="a1086-198">在 IIS 管理器中，在**连接**窗格中，展开服务器节点 (例如， **PROWEB1**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="a1086-199">右键单击**站点**节点，并单击**添加网站**。</span><span class="sxs-lookup"><span data-stu-id="a1086-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="a1086-200">在中**站点名称**框中，键入为 IIS 网站的名称 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="a1086-201">在中**物理路径**框中，键入 （或浏览到） 到本地文件夹的路径 (例如， **C:\DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="a1086-202">在中**端口**框中，键入你想要托管网站的端口号 (例如， **85**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1086-203">标准端口号是 80 用于 HTTP 和 HTTPS 的 443。</span><span class="sxs-lookup"><span data-stu-id="a1086-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="a1086-204">但是，如果托管该网站在端口 80 上的，你需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="a1086-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="a1086-205">将保留**主机名**框保留为空，除非你想要配置该网站的域名系统 (DNS) 记录，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="a1086-206">在生产环境中，你将很可能想要托管你的网站在端口 80 上并配置主机标头，以及匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="a1086-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="a1086-207">在 IIS 7 中配置主机标头的详细信息，请参阅[为网站 (IIS 7) 配置主机标头](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a1086-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="a1086-208">Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅[DNS 服务器概述](https://technet.microsoft.com/en-gb/library/cc770392.aspx)并[DNS 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="a1086-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="a1086-209">在中**操作**窗格下**编辑站点**，单击**绑定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="a1086-210">在中**站点绑定**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1086-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="a1086-211">在中**添加网站绑定**对话框中，将**IP 地址**并**端口**以匹配您现有的站点配置。</span><span class="sxs-lookup"><span data-stu-id="a1086-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="a1086-212">在中**主机名**框中，键入你的 web 服务器的名称 (例如， **PROWEB1**)，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="a1086-213">第一个站点绑定使你可以访问站点使用的 IP 地址和端口在本地或`http://localhost:85`。</span><span class="sxs-lookup"><span data-stu-id="a1086-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="a1086-214">第二个站点绑定使你可以使用计算机名称在域上的其他计算机访问站点 (例如， http://proweb1:85)。</span><span class="sxs-lookup"><span data-stu-id="a1086-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="a1086-215">在中**站点绑定**对话框中，单击**关闭**。</span><span class="sxs-lookup"><span data-stu-id="a1086-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="a1086-216">在中**连接**窗格中，单击**应用程序池**。</span><span class="sxs-lookup"><span data-stu-id="a1086-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="a1086-217">在中**应用程序池**窗格中，右键单击你的应用程序池的名称，然后单击**基本设置**。</span><span class="sxs-lookup"><span data-stu-id="a1086-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="a1086-218">默认情况下，应用程序池的名称将与你的网站的名称匹配 (例如， **DemoSite**)。</span><span class="sxs-lookup"><span data-stu-id="a1086-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="a1086-219">在 **.NET Framework 版本** 列表中，选择 **.NET Framework v4.0.30319** ，然后单击 **确定** 。</span><span class="sxs-lookup"><span data-stu-id="a1086-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="a1086-220">示例解决方案需要.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="a1086-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="a1086-221">这不是必需的 Web 部署一般情况下。</span><span class="sxs-lookup"><span data-stu-id="a1086-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="a1086-222">为了使你的网站提供内容，应用程序池标识必须具有读取存储内容的本地文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="a1086-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="a1086-223">在 IIS 7.5 应用程序池以运行唯一的应用程序池标识 （与以前版本的 IIS，其中应用程序池通常运行使用网络服务帐户） 默认情况下。</span><span class="sxs-lookup"><span data-stu-id="a1086-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="a1086-224">应用程序池标识不是真实的用户帐户和未出现在任何用户或组的列表&#x2014;相反，它动态启动时创建的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="a1086-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="a1086-225">每个应用程序池标识添加到本地**IIS\_IUSRS**隐藏项的安全组。</span><span class="sxs-lookup"><span data-stu-id="a1086-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="a1086-226">若要授予对文件或文件夹上的应用程序池标识的权限，您有两个选项：</span><span class="sxs-lookup"><span data-stu-id="a1086-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="a1086-227">将权限分配给应用程序池标识直接，使用格式<strong>IIS AppPool\</strong ><em>[应用程序池名称]</em>(例如， <strong>IIS AppPool\DemoSite</strong>).</span><span class="sxs-lookup"><span data-stu-id="a1086-227">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="a1086-228">向其分配权限**IIS\_IUSRS**组。</span><span class="sxs-lookup"><span data-stu-id="a1086-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="a1086-229">最常用的方法是将权限分配给本地**IIS\_IUSRS**组，因为这种方法允许您更改应用程序池，而无需重新配置的文件系统权限。</span><span class="sxs-lookup"><span data-stu-id="a1086-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="a1086-230">下一个过程中使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="a1086-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="a1086-231">在 IIS 7.5 的应用程序池标识的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="a1086-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="a1086-232">**若要配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="a1086-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="a1086-233">在 Windows 资源管理器，浏览到本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="a1086-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="a1086-234">右键单击文件夹，然后依次**属性**。</span><span class="sxs-lookup"><span data-stu-id="a1086-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="a1086-235">上**安全**选项卡上，单击**编辑**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="a1086-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="a1086-236">单击**位置**。</span><span class="sxs-lookup"><span data-stu-id="a1086-236">Click **Locations**.</span></span> <span data-ttu-id="a1086-237">在中**位置**对话框中，选择本地服务器，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="a1086-238">在中**选择用户或组**对话框中，键入**IIS\_IUSRS**，单击**检查名称**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="a1086-239">在中<strong>的权限</strong><em>[文件夹名称]</em>对话框中，请注意，新的组已分配<strong>读取&amp;执行</strong>，<strong>列出文件夹内容</strong>，并<strong>读取</strong>默认情况下的权限。</span><span class="sxs-lookup"><span data-stu-id="a1086-239">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="a1086-240">保留此保持不变，然后单击<strong>确定</strong>。</span><span class="sxs-lookup"><span data-stu-id="a1086-240">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="a1086-241">单击<strong>确定</strong>以关闭<em>[文件夹名称]</em><strong>属性</strong>对话框。</span><span class="sxs-lookup"><span data-stu-id="a1086-241">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="a1086-242">禁用远程代理服务</span><span class="sxs-lookup"><span data-stu-id="a1086-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="a1086-243">在安装 Web Deploy，Web 部署代理服务安装，并自动启动。</span><span class="sxs-lookup"><span data-stu-id="a1086-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="a1086-244">此服务可以部署和发布远程位置中的 web 包。</span><span class="sxs-lookup"><span data-stu-id="a1086-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="a1086-245">您不会使用的远程部署功能在此方案中，因此应停止并禁用服务。</span><span class="sxs-lookup"><span data-stu-id="a1086-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="a1086-246">不需要停止远程代理服务才能导入和手动部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="a1086-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="a1086-247">但是，它是停止和禁用服务，如果不打算使用它的好办法。</span><span class="sxs-lookup"><span data-stu-id="a1086-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>


<span data-ttu-id="a1086-248">可以停止和禁用某项服务在多个方面，使用各种命令行实用程序或 Windows PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a1086-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="a1086-249">此过程介绍了简单的基于 UI 的方法。</span><span class="sxs-lookup"><span data-stu-id="a1086-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="a1086-250">**若要停止并禁用远程代理服务**</span><span class="sxs-lookup"><span data-stu-id="a1086-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="a1086-251">在“开始”  菜单上，指向“管理工具” ，然后单击“服务” 。</span><span class="sxs-lookup"><span data-stu-id="a1086-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="a1086-252">在服务控制台中，找到**Web 部署代理服务**行。</span><span class="sxs-lookup"><span data-stu-id="a1086-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="a1086-253">右键单击**Web 部署代理服务**，然后单击**属性**。</span><span class="sxs-lookup"><span data-stu-id="a1086-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="a1086-254">在中**Web 部署代理服务属性**对话框中，单击**停止**。</span><span class="sxs-lookup"><span data-stu-id="a1086-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="a1086-255">在中**启动类型**列表中，选择**禁用**，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="a1086-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="a1086-256">结束语</span><span class="sxs-lookup"><span data-stu-id="a1086-256">Conclusion</span></span>

<span data-ttu-id="a1086-257">此时，你的 web 服务器是脱机 web 包部署已准备就绪。</span><span class="sxs-lookup"><span data-stu-id="a1086-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="a1086-258">在尝试导入到 IIS 网站的 web 包之前，你可能想要检查这些关键点：</span><span class="sxs-lookup"><span data-stu-id="a1086-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="a1086-259">已向 IIS 注册 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="a1086-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="a1086-260">没有应用程序池标识具有读取访问权限的源文件夹的你的网站？</span><span class="sxs-lookup"><span data-stu-id="a1086-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="a1086-261">已停止 Web 部署代理服务？</span><span class="sxs-lookup"><span data-stu-id="a1086-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1086-262">[上一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [下一页](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="a1086-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
