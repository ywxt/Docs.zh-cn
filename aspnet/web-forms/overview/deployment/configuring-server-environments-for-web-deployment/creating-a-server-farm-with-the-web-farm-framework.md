---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 使用 Web Farm Framework 创建服务器场 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 Web Farm Framework (WFF) 2.0 创建和配置 web 服务器场中服务器的集合。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: ad557306cb4d3c62932c640b598f82d692bc74cf
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388288"
---
<a name="creating-a-server-farm-with-the-web-farm-framework"></a><span data-ttu-id="afa4e-103">使用 Web Farm Framework 创建服务器场</span><span class="sxs-lookup"><span data-stu-id="afa4e-103">Creating a Server Farm with the Web Farm Framework</span></span>
====================
<span data-ttu-id="afa4e-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="afa4e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="afa4e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="afa4e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="afa4e-106">本主题介绍如何使用 Web Farm Framework (WFF) 2.0 创建和配置 web 服务器场中服务器的集合。</span><span class="sxs-lookup"><span data-stu-id="afa4e-106">This topic describes how to use the Web Farm Framework (WFF) 2.0 to create and configure a web server farm from a collection of servers.</span></span>


<span data-ttu-id="afa4e-107">WFF，可以跨多个负载平衡的 web 服务器同步 web 平台产品和组件、 web 应用程序、 网站和配置设置。</span><span class="sxs-lookup"><span data-stu-id="afa4e-107">WFF lets you synchronize web platform products and components, web applications, websites, and configuration settings across multiple load-balanced web servers.</span></span> <span data-ttu-id="afa4e-108">在方案中需要多个 web 服务器，例如过渡和生产环境，这可以极大地简化部署和配置过程。</span><span class="sxs-lookup"><span data-stu-id="afa4e-108">In scenarios where you need more than one web server, like staging and production environments, this can vastly simplify your deployment and configuration process.</span></span> <span data-ttu-id="afa4e-109">可以部署到一台服务器的 web 应用程序&#x2014;*主服务器*&#x2014;和 WFF 都将自动复制在服务器场中的所有其他 web 服务器上该 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="afa4e-109">You can deploy a web application to a single server&#x2014;the *primary server*&#x2014;and WFF will automatically replicate that web application on all the other web servers in the server farm.</span></span>

## <a name="understanding-the-web-farm-framework"></a><span data-ttu-id="afa4e-110">了解 Web 场框架</span><span class="sxs-lookup"><span data-stu-id="afa4e-110">Understanding the Web Farm Framework</span></span>

<span data-ttu-id="afa4e-111">WFF 2.0 可用于预配、 管理和将内容部署到一组 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-111">You can use WFF 2.0 to provision, manage, and deploy content to a group of web servers.</span></span> <span data-ttu-id="afa4e-112">WFF 部署包括三个关键的服务器角色：</span><span class="sxs-lookup"><span data-stu-id="afa4e-112">A WFF deployment consists of three key server roles:</span></span>

- <span data-ttu-id="afa4e-113">*控制器服务器*。</span><span class="sxs-lookup"><span data-stu-id="afa4e-113">The *controller server*.</span></span> <span data-ttu-id="afa4e-114">使用此服务器来创建和配置 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-114">You use this server to create and configure WFF server farms.</span></span> <span data-ttu-id="afa4e-115">控制器服务器管理的 web 平台组件、 配置设置和应用程序在服务器场的 web 服务器之间的同步。</span><span class="sxs-lookup"><span data-stu-id="afa4e-115">The controller server manages the synchronization of web platform components, configuration settings, and applications between the web servers in a server farm.</span></span> <span data-ttu-id="afa4e-116">在控制器服务器上，安装 WFF 2.0 和控制器服务器反过来将每个服务器场中的服务器上安装 WFF 代理。</span><span class="sxs-lookup"><span data-stu-id="afa4e-116">You install WFF 2.0 on the controller server, and the controller server will in turn install the WFF agent on each of the servers in a server farm.</span></span> <span data-ttu-id="afa4e-117">控制器服务器从概念上讲不属于任何 WFF 服务器场中，并且单个控制器服务器可以管理多个服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-117">The controller server does not conceptually belong to any WFF server farm, and a single controller server can manage multiple server farms.</span></span> <span data-ttu-id="afa4e-118">在此方案中，使用单个 WFF 控制器服务器来创建和管理的过渡服务器场和生产服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-118">In this scenario, you use a single WFF controller server to create and manage the staging server farm and the production server farm.</span></span>
- <span data-ttu-id="afa4e-119">*主服务器*。</span><span class="sxs-lookup"><span data-stu-id="afa4e-119">The *primary server*.</span></span> <span data-ttu-id="afa4e-120">每个 WFF 服务器场包括一个主服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-120">Each WFF server farm includes a single primary server.</span></span> <span data-ttu-id="afa4e-121">当你安装 web 平台组件或应用程序部署到主服务器时，WFF 将同步到服务器场中的所有其他服务器所做的更改。</span><span class="sxs-lookup"><span data-stu-id="afa4e-121">When you install web platform components or deploy applications to the primary server, the WFF synchronizes your changes to all the other servers in the server farm.</span></span>
- <span data-ttu-id="afa4e-122">*辅助服务器*。</span><span class="sxs-lookup"><span data-stu-id="afa4e-122">The *secondary server*.</span></span> <span data-ttu-id="afa4e-123">每个 WFF 服务器场包含一个或多个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-123">Each WFF server farm includes one or more secondary servers.</span></span> <span data-ttu-id="afa4e-124">对主服务器进行任何更改复制到服务器场中每个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-124">Any changes you make to the primary server are replicated to every secondary server within the server farm.</span></span>

<span data-ttu-id="afa4e-125">这将显示这些服务器角色如何与 Fabrikam，Inc.过渡和生产环境相关联：</span><span class="sxs-lookup"><span data-stu-id="afa4e-125">This shows how these server roles relate to the Fabrikam, Inc. staging and production environments:</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

<span data-ttu-id="afa4e-126">在此方案中，在过渡环境和生产环境被配置为 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-126">In this scenario, the staging environment and the production environment are both configured as WFF server farms.</span></span> <span data-ttu-id="afa4e-127">单个 WFF 控制器服务器管理这两种场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-127">A single WFF controller server manages both farms.</span></span> <span data-ttu-id="afa4e-128">在每个服务器场，对主服务器的任何更改复制到每个辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-128">Within each server farm, any changes to the primary server are replicated to every secondary server.</span></span>

<span data-ttu-id="afa4e-129">在开始配置过渡和生产环境之前，我们建议阅读以下文章，熟悉 WFF 2.0 的关键概念：</span><span class="sxs-lookup"><span data-stu-id="afa4e-129">Before you start to configure your staging and production environments, we recommend that you read these articles to familiarize yourself with the key concepts of WFF 2.0:</span></span>

- [<span data-ttu-id="afa4e-130">IIS 7 的 Web 场框架 2.0 概述</span><span class="sxs-lookup"><span data-stu-id="afa4e-130">Overview of the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805126)
- [<span data-ttu-id="afa4e-131">设置适用于 IIS 7 Web Farm Framework 2.0 的服务器场</span><span class="sxs-lookup"><span data-stu-id="afa4e-131">Setting up a Server Farm with the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805127)
- [<span data-ttu-id="afa4e-132">系统和 iis 7 Web Farm Framework 2.0 的平台要求</span><span class="sxs-lookup"><span data-stu-id="afa4e-132">System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a><span data-ttu-id="afa4e-133">任务概述</span><span class="sxs-lookup"><span data-stu-id="afa4e-133">Task Overview</span></span>

<span data-ttu-id="afa4e-134">若要完成的任务和本主题中的演练，你将需要至少三个服务器&#x2014;一个 WFF 控制器、 服务器场中，一个主 web 服务器和服务器场的一个或多个辅助 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-134">To complete the tasks and walkthroughs in this topic, you'll need at least three servers&#x2014;one WFF controller, one primary web server for the server farm, and one or more secondary web servers for the server farm.</span></span> <span data-ttu-id="afa4e-135">您可以在任何时间将更多的辅助服务器添加到 WFF 服务器场中。</span><span class="sxs-lookup"><span data-stu-id="afa4e-135">You can add more secondary servers to a WFF server farm at any time.</span></span> <span data-ttu-id="afa4e-136">在高级别，来创建和配置，你需要在过渡或生产环境的 WFF 服务器场：</span><span class="sxs-lookup"><span data-stu-id="afa4e-136">At a high level, to create and configure a WFF server farm for your staging or production environment you'll need to:</span></span>

- <span data-ttu-id="afa4e-137">通过安装 Internet 信息服务 (IIS) 7.5 和 WFF 2.0 创建控制器服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-137">Create a controller server by installing Internet Information Services (IIS) 7.5 and WFF 2.0.</span></span>
- <span data-ttu-id="afa4e-138">准备通过创建常见的管理员帐户和配置防火墙例外的主要和辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-138">Prepare primary and secondary servers by creating a common administrator account and configuring firewall exceptions.</span></span>
- <span data-ttu-id="afa4e-139">在控制器服务器上使用 IIS 管理器配置服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-139">Configure the server farm by using IIS Manager on the controller server.</span></span>
- <span data-ttu-id="afa4e-140">配置负载均衡使用 IIS 应用程序请求路由 (ARR) 或其他负载平衡技术。</span><span class="sxs-lookup"><span data-stu-id="afa4e-140">Configure load balancing using IIS Application Request Routing (ARR) or an alternative load-balancing technology.</span></span>

<span data-ttu-id="afa4e-141">任务和本主题中的演练假定您正在使用运行 Windows Server 2008 R2 的全新的服务器生成。</span><span class="sxs-lookup"><span data-stu-id="afa4e-141">The tasks and walkthroughs in this topic assume that you're starting with clean server builds running Windows Server 2008 R2.</span></span> <span data-ttu-id="afa4e-142">在开始为每个服务器之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="afa4e-142">Before you begin, for each server, ensure that:</span></span>

- <span data-ttu-id="afa4e-143">安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="afa4e-143">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="afa4e-144">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="afa4e-144">The server is domain-joined.</span></span>
- <span data-ttu-id="afa4e-145">在服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="afa4e-145">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="afa4e-146">有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-146">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="afa4e-147">有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-147">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="create-the-wff-controller-server"></a><span data-ttu-id="afa4e-148">创建 WFF 控制器服务器</span><span class="sxs-lookup"><span data-stu-id="afa4e-148">Create the WFF Controller Server</span></span>

<span data-ttu-id="afa4e-149">若要创建 WFF 控制器服务器，你将需要安装 IIS 7 或更高版本和 WFF 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="afa4e-149">To create a WFF controller server, you'll need to install both IIS 7 or later and WFF 2.0 or later.</span></span> <span data-ttu-id="afa4e-150">实际上，WFF 使用 IIS Web 部署工具 （Web 部署） 2.x 同步您的服务器场中的服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-150">Under the covers, WFF uses the IIS Web Deployment Tool (Web Deploy) 2.x to synchronize the servers in your farm.</span></span> <span data-ttu-id="afa4e-151">如果使用 Web 平台安装程序来安装 WFF，安装程序将自动下载并安装适用于你的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="afa4e-151">If you use the Web Platform Installer to install WFF, the installer will automatically download and install Web Deploy for you.</span></span>

<span data-ttu-id="afa4e-152">**若要创建 WFF 控制器服务器**</span><span class="sxs-lookup"><span data-stu-id="afa4e-152">**To create the WFF controller server**</span></span>

1. <span data-ttu-id="afa4e-153">下载并安装[Web 平台安装程序](https://go.microsoft.com/?linkid=9739157)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-153">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9739157).</span></span>
2. <span data-ttu-id="afa4e-154">在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-154">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="afa4e-155">在左侧和右侧的窗口中，在导航窗格中，单击**Server**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-155">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="afa4e-156">在 **IIS 7 建议配置** 行中，单击 **添加** 。</span><span class="sxs-lookup"><span data-stu-id="afa4e-156">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
5. <span data-ttu-id="afa4e-157">在中<strong>Web 场框架 2。</strong><em>x</em>行中，单击<strong>添加</strong>。</span><span class="sxs-lookup"><span data-stu-id="afa4e-157">In the <strong>Web Farm Framework 2.</strong><em>x</em> row, click <strong>Add</strong>.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. <span data-ttu-id="afa4e-158">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="afa4e-158">Click **Install**.</span></span> <span data-ttu-id="afa4e-159">请注意，Web 平台安装程序具有 Web 部署工具，以及各种其他依赖项，添加到安装列表。</span><span class="sxs-lookup"><span data-stu-id="afa4e-159">Notice that the Web Platform Installer has added the Web Deployment Tool, along with various other dependencies, to the installation list.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. <span data-ttu-id="afa4e-160">查看许可条款，如果同意条款，单击**我接受**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-160">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
8. <span data-ttu-id="afa4e-161">安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。</span><span class="sxs-lookup"><span data-stu-id="afa4e-161">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

## <a name="configure-the-primary-and-secondary-servers"></a><span data-ttu-id="afa4e-162">配置主要和辅助服务器</span><span class="sxs-lookup"><span data-stu-id="afa4e-162">Configure the Primary and Secondary Servers</span></span>

<span data-ttu-id="afa4e-163">在创建 WFF 服务器场之前，应完成一些准备任务将构成该场的 web 服务器上：</span><span class="sxs-lookup"><span data-stu-id="afa4e-163">Before you create a WFF server farm, you should complete some preparation tasks on the web servers that will make up the farm:</span></span>

- <span data-ttu-id="afa4e-164">添加防火墙例外以允许**核心网络**，**远程管理**，并**文件和打印机共享**与 WFF 控制器服务器进行通信的功能.</span><span class="sxs-lookup"><span data-stu-id="afa4e-164">Add firewall exceptions to allow the **Core Networking**, **Remote Administration**, and **File and Printer Sharing** features to communicate with the WFF controller server.</span></span>
- <span data-ttu-id="afa4e-165">创建域帐户 (例如， **FABRIKAM\stagingfarm**) 在 Active Directory 中将其添加到每个服务器上的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="afa4e-165">Create a domain account (for example, **FABRIKAM\stagingfarm**) in Active Directory and add it to the local administrators group on each server.</span></span> <span data-ttu-id="afa4e-166">创建服务器场时，您将使用此帐户作为服务器场管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="afa4e-166">You'll use this account as the server farm administrator account when you create the server farm.</span></span>

<span data-ttu-id="afa4e-167">有关如何在 Windows 防火墙中配置这些防火墙例外的详细信息，请参阅[系统要求和 IIS 7 Web Farm Framework 2.0 的平台要求](https://go.microsoft.com/?linkid=9805128)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-167">For more information on how to configure these firewall exceptions in Windows Firewall, see [System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805128).</span></span> <span data-ttu-id="afa4e-168">其他防火墙系统，请参阅产品文档。</span><span class="sxs-lookup"><span data-stu-id="afa4e-168">For other firewall systems, consult your product documentation.</span></span>

<span data-ttu-id="afa4e-169">下一步过程可用于将域帐户添加到 Windows Server 2008 R2 中的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="afa4e-169">You can use the next procedure to add a domain account to the local administrators group in Windows Server 2008 R2.</span></span> <span data-ttu-id="afa4e-170">应在你想要添加到服务器场的每个服务器上执行此步骤&#x2014;换而言之，将相同的域帐户添加到主服务器和每个辅助服务器上的本地管理员组。</span><span class="sxs-lookup"><span data-stu-id="afa4e-170">You should perform this procedure on every server that you want to add to the server farm&#x2014;in other words, add the same domain account to the local administrators group on the primary server and on each secondary server.</span></span>

<span data-ttu-id="afa4e-171">**若要将域帐户添加到本地管理员组**</span><span class="sxs-lookup"><span data-stu-id="afa4e-171">**To add a domain account to the local administrators group**</span></span>

1. <span data-ttu-id="afa4e-172">上**启动**菜单，依次指向**管理工具**，然后单击**服务器管理器**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-172">On the **Start** menu, point to **Administrative Tools**, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="afa4e-173">在中**服务器管理器**窗口中的，在树视图窗格中，展开**配置**，展开**本地用户和组**，然后单击**组**.</span><span class="sxs-lookup"><span data-stu-id="afa4e-173">In the **Server Manager** window, in the tree view pane, expand **Configuration**, expand **Local Users and Groups**, and then click **Groups**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. <span data-ttu-id="afa4e-174">在中**组**窗格中，双击**管理员**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-174">In the **Groups** pane, double-click **Administrators**.</span></span>
4. <span data-ttu-id="afa4e-175">在中**Administrators 属性**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-175">In the **Administrators Properties** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="afa4e-176">在中**选择用户、 计算机、 服务帐户或组**对话框中，键入 （或浏览） 到您的域帐户 (例如， **FABRIKAM\stagingfarm**)，然后单击**确定**.</span><span class="sxs-lookup"><span data-stu-id="afa4e-176">In the **Select Users, Computers, Service Accounts, or Groups** dialog box, type (or browse) to your domain account (for example, **FABRIKAM\stagingfarm**), and then click **OK**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. <span data-ttu-id="afa4e-177">在中**Administrators 属性**对话框中，单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-177">In the **Administrators Properties** dialog box, click **OK**.</span></span>

<span data-ttu-id="afa4e-178">你的服务器现已准备好添加到服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-178">Your servers are now ready to be added to a server farm.</span></span> <span data-ttu-id="afa4e-179">如果主服务器，可以配置该服务器以满足应用程序的需求之前或之后创建的服务器场&#x2014;在这两种情况下，WFF 将通过部署相同的产品、 组件或配置同步服务器向辅助服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-179">In the case of the primary server, you can configure the server to meet your application requirements before or after you create the server farm&#x2014;in both cases, the WFF will synchronize the servers by deploying the same products, components, or configuration to your secondary servers.</span></span> <span data-ttu-id="afa4e-180">为简单起见，本教程假定已完成创建服务器场会配置主服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-180">For the sake of simplicity, this tutorial assumes that you'll configure the primary server when you've finished creating the server farm.</span></span>

## <a name="create-the-wff-server-farm"></a><span data-ttu-id="afa4e-181">创建 WFF 服务器场</span><span class="sxs-lookup"><span data-stu-id="afa4e-181">Create the WFF Server Farm</span></span>

<span data-ttu-id="afa4e-182">此时，所有服务器都已准备好添加到 WFF 服务器场：</span><span class="sxs-lookup"><span data-stu-id="afa4e-182">At this point, all your servers are ready to be added to a WFF server farm:</span></span>

- <span data-ttu-id="afa4e-183">已在控制器服务器上安装 WFF。</span><span class="sxs-lookup"><span data-stu-id="afa4e-183">You've installed WFF on the controller server.</span></span>
- <span data-ttu-id="afa4e-184">已在主要和次要的 web 服务器上配置防火墙例外。</span><span class="sxs-lookup"><span data-stu-id="afa4e-184">You've configured firewall exceptions on your primary and secondary web servers.</span></span>
- <span data-ttu-id="afa4e-185">在主要和次要的 web 服务器上，已添加到本地管理员组的域帐户。</span><span class="sxs-lookup"><span data-stu-id="afa4e-185">You've added a domain account to the local administrators group on your primary and secondary web servers.</span></span>

<span data-ttu-id="afa4e-186">下一步是在 WFF 中创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-186">The next step is to create the server farm in WFF.</span></span> <span data-ttu-id="afa4e-187">您可以执行此操作从 IIS 管理器 WFF 控制器服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-187">You can do this from IIS Manager on the WFF controller server.</span></span>

<span data-ttu-id="afa4e-188">**若要创建 WFF 服务器场**</span><span class="sxs-lookup"><span data-stu-id="afa4e-188">**To create a WFF server farm**</span></span>

1. <span data-ttu-id="afa4e-189">在 WFF 控制器服务器上，在**启动**菜单，依次指向**管理工具**，然后单击**Internet 信息服务 (IIS) 管理器**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-189">On the WFF controller server, on the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="afa4e-190">在中**连接**窗格中，展开本地服务器节点，右键单击**服务器场**，然后单击**创建服务器场**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-190">In the **Connections** pane, expand the local server node, right-click **Server Farms**, and then click **Create Server Farm**.</span></span>
3. <span data-ttu-id="afa4e-191">在**创建服务器场**对话框框中，键入服务器场有意义的名称 (例如，**过渡场**)，然后选择**配置服务器场**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-191">In the **Create Server Farm** dialog box, type a meaningful name for the server farm (for example, **Staging Farm**), and then select **Provision server farm**.</span></span>
4. <span data-ttu-id="afa4e-192">键入用户名和密码添加到每个服务器上的本地管理员组的域帐户。</span><span class="sxs-lookup"><span data-stu-id="afa4e-192">Type the user name and password of the domain account that you added to the local administrators group on each server.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. <span data-ttu-id="afa4e-193">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-193">Click **Next**.</span></span>
6. <span data-ttu-id="afa4e-194">上**添加服务器**页上，键入完全限定的域名 (FQDN) 的主服务器，选择**主服务器**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-194">On the **Add Servers** page, type the fully qualified domain name (FQDN) of the primary server, select **Primary Server**, and then click **Add**.</span></span>
7. <span data-ttu-id="afa4e-195">此时，WFF 将尝试联系主服务器使用你提供的凭据。</span><span class="sxs-lookup"><span data-stu-id="afa4e-195">At this point, WFF will attempt to contact the primary server using the credentials you provided.</span></span> <span data-ttu-id="afa4e-196">如果连接成功，将在添加到表的主服务器**添加服务器**页。</span><span class="sxs-lookup"><span data-stu-id="afa4e-196">If the connection succeeds, the primary server will be added to the table on the **Add Servers** page.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="afa4e-197">您可能已经注意到，**服务器是可用于负载平衡**默认处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="afa4e-197">You might have noticed that **Server is available for Load Balancing** is selected by default.</span></span> <span data-ttu-id="afa4e-198">WFF 使用 IIS ARR 模块来实现负载平衡，从而在服务器场中的 web 服务器间分发请求。</span><span class="sxs-lookup"><span data-stu-id="afa4e-198">WFF uses the IIS ARR module to implement load balancing and thereby distribute requests across the web servers in your server farm.</span></span> <span data-ttu-id="afa4e-199">在大多数情况下，只会清除**服务器是可用于负载平衡**选项如果想要使用第三方负载平衡解决方案来代替。</span><span class="sxs-lookup"><span data-stu-id="afa4e-199">In most scenarios, you'd only clear the **Server is available for Load Balancing** option if you wanted to use a third-party load balancing solution instead.</span></span>
8. <span data-ttu-id="afa4e-200">上**添加服务器**页上，键入第一个辅助服务器的 FQDN，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-200">On the **Add Servers** page, type the FQDN of your first secondary server, and then click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. <span data-ttu-id="afa4e-201">为您的服务器场中的任何其他辅助服务器重复步骤 7，然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-201">Repeat step 7 for any additional secondary servers in your farm, and then click **Finish**.</span></span>

<span data-ttu-id="afa4e-202">WFF 服务器场是正在运行。</span><span class="sxs-lookup"><span data-stu-id="afa4e-202">Your WFF server farm is now up and running.</span></span> <span data-ttu-id="afa4e-203">任何 web 平台产品或主服务器和所有 web 应用程序或内容部署到主服务器安装的组件，将自动配置所有辅助服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-203">Any web platform products or components that you install on the primary server, and any web applications or content that you deploy to the primary server, will be automatically provisioned on all your secondary servers.</span></span>

<span data-ttu-id="afa4e-204">WFF 是各种广泛而复杂的主题，并可以了解有关它的详细信息[适用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站。</span><span class="sxs-lookup"><span data-stu-id="afa4e-204">WFF is a broad and complex topic, and you can learn more about it on the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span> <span data-ttu-id="afa4e-205">目前，但是，有两个需要注意的功能区域：</span><span class="sxs-lookup"><span data-stu-id="afa4e-205">For the time being, however, there are two features areas that you need to be aware of:</span></span>

- <span data-ttu-id="afa4e-206">*应用程序预配*是跨服务器场中的所有辅助服务器从主服务器，例如 web 应用程序和配置设置复制内容的过程。</span><span class="sxs-lookup"><span data-stu-id="afa4e-206">*Application provisioning* is the process that replicates content from the primary server, like web applications and configuration settings, across all the secondary servers in the server farm.</span></span> <span data-ttu-id="afa4e-207">例如，如果联系人管理器示例解决方案部署到主暂存服务器时，WFF 应用程序预配过程将此将解决方案部署到所有辅助临时服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-207">For example, if you deploy the Contact Manager sample solution to your primary staging server, the WFF application provisioning process will deploy this solution to all your secondary staging servers.</span></span> <span data-ttu-id="afa4e-208">默认情况下，应用程序预配过程在运行每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="afa4e-208">By default, the application provisioning process runs every 30 seconds.</span></span>
- <span data-ttu-id="afa4e-209">*平台配置*是同步 web 平台产品和组件从主服务器到服务器场中的所有辅助服务器的过程。</span><span class="sxs-lookup"><span data-stu-id="afa4e-209">*Platform provisioning* is the process that synchronizes web platform products and components from the primary server to all the secondary servers in the server farm.</span></span> <span data-ttu-id="afa4e-210">例如，如果在主要的过渡服务器上安装 ASP.NET MVC 3，平台预配过程将使用 Web 平台安装程序在所有辅助临时服务器上安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="afa4e-210">For example, if you install ASP.NET MVC 3 on your primary staging server, the platform provisioning process will use the Web Platform Installer to install ASP.NET MVC 3 on all your secondary staging servers.</span></span> <span data-ttu-id="afa4e-211">默认情况下，平台预配过程运行每隔五分钟。</span><span class="sxs-lookup"><span data-stu-id="afa4e-211">By default, the platform provisioning process runs every five minutes.</span></span>

<span data-ttu-id="afa4e-212">你可以管理的基本应用程序和平台预配设置从 IIS 管理器 WFF 控制器服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-212">You can manage basic application and platform provisioning settings from IIS Manager on your WFF controller server.</span></span>

<span data-ttu-id="afa4e-213">**浏览应用程序和平台配置设置**</span><span class="sxs-lookup"><span data-stu-id="afa4e-213">**Explore application and platform provisioning settings**</span></span>

1. <span data-ttu-id="afa4e-214">在 IIS 管理器中，在**连接**窗格中，选择你的服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-214">In IIS Manager, in the **Connections** pane, select your server farm.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. <span data-ttu-id="afa4e-215">在中**服务器场**窗格中，双击**应用程序预配**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-215">In the **Server Farm** pane, double-click **Application Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. <span data-ttu-id="afa4e-216">正如您所看到的当前配置的服务器场以同步每隔 30 秒的主服务器和辅助服务器之间的 web 内容和配置设置。</span><span class="sxs-lookup"><span data-stu-id="afa4e-216">As you can see, the server farm is currently configured to synchronize web content and configuration settings between the primary server and the secondary servers every 30 seconds.</span></span>
4. <span data-ttu-id="afa4e-217">单击**回**，然后双击**平台配置**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-217">Click **Back**, and then double-click **Platform Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. <span data-ttu-id="afa4e-218">正如您所看到的当前配置的服务器场来同步 web 平台产品和组件之间的主服务器和辅助服务器每隔五分钟。</span><span class="sxs-lookup"><span data-stu-id="afa4e-218">As you can see, the server farm is currently configured to synchronize web platform products and components between the primary server and the secondary servers every five minutes.</span></span>
6. <span data-ttu-id="afa4e-219">单击**回**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-219">Click **Back**.</span></span>
7. <span data-ttu-id="afa4e-220">若要强制立即同步 web 平台产品的服务器场中**操作**窗格中，单击**预配平台**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-220">To force the server farm to synchronize web platform products immediately, in the **Actions** pane, click **Provision Platform**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > <span data-ttu-id="afa4e-221">平台配置可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="afa4e-221">Platform provisioning may take some time.</span></span> <span data-ttu-id="afa4e-222">安装程序进程在后台运行在服务器场中的辅助服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-222">The installer process runs in the background on the secondary servers in your server farm.</span></span>
8. <span data-ttu-id="afa4e-223">一旦已允许足够的时间才能完成预配过程，可以验证，产品和组件添加到主服务器现在已复制的辅助服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-223">Once you've allowed sufficient time for the provisioning process to complete, you can verify that the products and components that you added to the primary server have now been replicated on the secondary servers.</span></span> <span data-ttu-id="afa4e-224">例如，您可以登录到辅助服务器上，使用**服务器管理器**窗口以验证是否已安装 web 服务器角色。</span><span class="sxs-lookup"><span data-stu-id="afa4e-224">For example, you can log on to a secondary server and use the **Server Manager** window to verify that the web server role has been installed.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. <span data-ttu-id="afa4e-225">此外可以查看已安装的程序列表以验证已添加各种 web 平台组件。</span><span class="sxs-lookup"><span data-stu-id="afa4e-225">You can also check the installed programs list to verify that various web platform components have been added.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a><span data-ttu-id="afa4e-226">配置负载平衡</span><span class="sxs-lookup"><span data-stu-id="afa4e-226">Configure Load Balancing</span></span>

<span data-ttu-id="afa4e-227">在创建 web 场时，你需要设置某种形式的负载平衡能够将 web 服务器之间的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="afa4e-227">When you create a web farm, you need to set up some form of load balancing to distribute HTTP requests between your web servers.</span></span> <span data-ttu-id="afa4e-228">这可能是 Windows Server 2008 网络负载平衡，IIS ARR 或第三方基于软件的或基于硬件的负载平衡解决方案。</span><span class="sxs-lookup"><span data-stu-id="afa4e-228">This could be Windows Server 2008 network load balancing, IIS ARR, or a third-party software-based or hardware-based load balancing solution.</span></span>

<span data-ttu-id="afa4e-229">WFF 旨在与 IIS arr。 紧密集成</span><span class="sxs-lookup"><span data-stu-id="afa4e-229">WFF is designed to integrate closely with IIS ARR.</span></span> <span data-ttu-id="afa4e-230">若要充分利用此集成，需要在 WFF 控制器服务器上安装 ARR 模块。</span><span class="sxs-lookup"><span data-stu-id="afa4e-230">To take advantage of this integration, you need to install the ARR module on the WFF controller server.</span></span> <span data-ttu-id="afa4e-231">您然后定向到控制器服务器的所有 web 流量通常通过配置域名系统 (DNS) 记录。</span><span class="sxs-lookup"><span data-stu-id="afa4e-231">You then direct all your web traffic to the controller server, typically by configuring Domain Name System (DNS) records.</span></span> <span data-ttu-id="afa4e-232">控制器服务器然后会将分发在您的服务器场，基于服务器的可用性和各种其他条件的服务器之间的传入请求。</span><span class="sxs-lookup"><span data-stu-id="afa4e-232">The controller server will then distribute incoming requests among the servers in your farm, based on server availability and various other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="afa4e-233">无需使用 WFF; 使用 ARR你可以配置 WFF 使用第三方负载平衡解决方案。</span><span class="sxs-lookup"><span data-stu-id="afa4e-233">You don't have to use ARR with WFF; you can configure WFF to work with third-party load balancing solutions.</span></span> <span data-ttu-id="afa4e-234">有关详细信息，请参阅[概述适用于 IIS 7 Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805126)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-234">For more information, see [Overview of the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805126).</span></span>


<span data-ttu-id="afa4e-235">使用 ARR 负载平衡是一个复杂的主题，最的超出了本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="afa4e-235">Load balancing using ARR is a complex topic, most of which is beyond the scope of this tutorial.</span></span> <span data-ttu-id="afa4e-236">但是，可以使用下一个过程中安装 ARR 模块并开始使用负载平衡。</span><span class="sxs-lookup"><span data-stu-id="afa4e-236">However, you can use the next procedure to install the ARR module and get started with load balancing.</span></span>

<span data-ttu-id="afa4e-237">**若要设置的 WFF 控制器服务器进行负载均衡**</span><span class="sxs-lookup"><span data-stu-id="afa4e-237">**To set up load balancing on the WFF controller server**</span></span>

1. <span data-ttu-id="afa4e-238">WFF 控制器服务器上，启动 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="afa4e-238">On the WFF controller server, launch the Web Platform Installer.</span></span>
2. <span data-ttu-id="afa4e-239">在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-239">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="afa4e-240">在左侧和右侧的窗口中，在导航窗格中，单击**Server**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-240">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="afa4e-241">在中**应用程序请求路由 2.5**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-241">In the **Application Request Routing 2.5** row, click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. <span data-ttu-id="afa4e-242">单击**安装**，然后按照中的说明进行操作**Web 平台安装**窗口。</span><span class="sxs-lookup"><span data-stu-id="afa4e-242">Click **Install**, and then follow the instructions in the **Web Platform Installation** window.</span></span>
6. <span data-ttu-id="afa4e-243">安装完成后，启动 IIS 管理器中，然后在**连接**窗格中，单击你的服务器场节点。</span><span class="sxs-lookup"><span data-stu-id="afa4e-243">When the installation is complete, launch IIS Manager, and in the **Connections** pane, click your server farm node.</span></span> <span data-ttu-id="afa4e-244">请注意，有几个新图标已添加到**服务器场**窗格。</span><span class="sxs-lookup"><span data-stu-id="afa4e-244">Notice that several new icons have been added to the **Server Farm** pane.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. <span data-ttu-id="afa4e-245">在中**服务器场**窗格中，双击**负载平衡**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-245">In the **Server Farm** pane, double-click **Load Balance**.</span></span>
8. <span data-ttu-id="afa4e-246">在中**负载平衡**窗格中，选择一个负载平衡算法 (例如，**至少当前请求**)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-246">In the **Load Balance** pane, select a load balance algorithm (for example, **Least current request**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="afa4e-247">有关负载平衡算法和其他配置设置的详细信息，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-247">For more information on load balancing algorithms and other configuration settings, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. <span data-ttu-id="afa4e-248">在中**操作**窗格中，单击**应用**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-248">In the **Actions** pane, click **Apply**.</span></span>

<span data-ttu-id="afa4e-249">你现在已配置基本负载均衡的服务器场中的服务器。</span><span class="sxs-lookup"><span data-stu-id="afa4e-249">You have now configured basic load balancing for the servers in your server farm.</span></span> <span data-ttu-id="afa4e-250">如果您所有在 web 场将流量定向到的控制器服务器，将根据可用性场中的服务器与所选的负载平衡算法之间分发请求。</span><span class="sxs-lookup"><span data-stu-id="afa4e-250">If you direct all your web farm traffic to the controller server, the requests will be distributed between the servers in your farm according to availability and the load balancing algorithm you selected.</span></span>

<span data-ttu-id="afa4e-251">有关如何使用 ARR 配置负载平衡的详细信息，请参阅[应用程序请求路由模块](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="afa4e-251">For more information on how to configure load balancing with ARR, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

## <a name="monitor-the-server-farm"></a><span data-ttu-id="afa4e-252">监视服务器场</span><span class="sxs-lookup"><span data-stu-id="afa4e-252">Monitor the Server Farm</span></span>

<span data-ttu-id="afa4e-253">你可以随时通过 IIS 管理器控制器服务器上监视服务器场的运行的状况。</span><span class="sxs-lookup"><span data-stu-id="afa4e-253">You can monitor the health of your server farm at any time through IIS Manager on the controller server.</span></span> <span data-ttu-id="afa4e-254">在中**连接**窗格中，展开你的服务器场，然后单击**服务器**。</span><span class="sxs-lookup"><span data-stu-id="afa4e-254">In the **Connections** pane, expand your server farm, and then click **Servers**.</span></span> <span data-ttu-id="afa4e-255">中心窗格中将显示的最近的活动的跟踪日志以及服务器场中的每个服务器的摘要。</span><span class="sxs-lookup"><span data-stu-id="afa4e-255">The center pane will show a summary of each server in the farm together with a trace log of recent activity.</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a><span data-ttu-id="afa4e-256">结束语</span><span class="sxs-lookup"><span data-stu-id="afa4e-256">Conclusion</span></span>

<span data-ttu-id="afa4e-257">启动并运行，现在应为 WFF 服务器场。</span><span class="sxs-lookup"><span data-stu-id="afa4e-257">Your WFF server farm should now be up and running.</span></span> <span data-ttu-id="afa4e-258">可以配置主服务器以支持无论你更喜欢哪种部署方法&#x2014;请参阅更多参考资料部分了解详细信息&#x2014;，且你的配置将复制在服务器场中每个辅助服务器上。</span><span class="sxs-lookup"><span data-stu-id="afa4e-258">You can configure the primary server to support whichever deployment approach you prefer&#x2014;see the Further Reading section for details&#x2014;and your configuration will be replicated on each secondary server in the server farm.</span></span>

## <a name="further-reading"></a><span data-ttu-id="afa4e-259">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="afa4e-259">Further Reading</span></span>

<span data-ttu-id="afa4e-260">有关配置和使用 WFF 的所有方面的更多指导，请参阅[适用于 IIS 7 的 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129)网站。</span><span class="sxs-lookup"><span data-stu-id="afa4e-260">For more guidance on all aspects of configuring and using the WFF, see the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="afa4e-261">[上一页](configuring-a-database-server-for-web-deploy-publishing.md)
> [下一页](configuring-deployment-properties-for-a-target-environment.md)</span><span class="sxs-lookup"><span data-stu-id="afa4e-261">[Previous](configuring-a-database-server-for-web-deploy-publishing.md)
[Next](configuring-deployment-properties-for-a-target-environment.md)</span></span>
