---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 配置 TFS 生成服务器用于 Web 部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何准备 Team Foundation Server (TFS) 生成服务器生成和部署你的解决方案使用 Team Build 和 Internet 信息...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 12a18f601a75b607c97c46ecb7f68947ca3a342b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382528"
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a><span data-ttu-id="3662d-103">配置用于 Web 部署的 TFS 生成服务器</span><span class="sxs-lookup"><span data-stu-id="3662d-103">Configuring a TFS Build Server for Web Deployment</span></span>
====================
<span data-ttu-id="3662d-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="3662d-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="3662d-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="3662d-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="3662d-106">本主题介绍如何准备用于生成和部署你使用 Team Build 和 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 的解决方案的 Team Foundation Server (TFS) 生成服务器。</span><span class="sxs-lookup"><span data-stu-id="3662d-106">This topic describes how to prepare a Team Foundation Server (TFS) build server to build and deploy your solutions using Team Build and the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>


<span data-ttu-id="3662d-107">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="3662d-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="3662d-108">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="3662d-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="3662d-109">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="3662d-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="3662d-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="3662d-110">Task Overview</span></span>

<span data-ttu-id="3662d-111">若要准备用于生成和部署你的解决方案的生成服务器，你将需要：</span><span class="sxs-lookup"><span data-stu-id="3662d-111">To prepare a build server to build and deploy your solutions, you'll need to:</span></span>

- <span data-ttu-id="3662d-112">安装和配置 TFS 生成服务。</span><span class="sxs-lookup"><span data-stu-id="3662d-112">Install and configure the TFS build service.</span></span>
- <span data-ttu-id="3662d-113">安装 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="3662d-113">Install Visual Studio 2010.</span></span>
- <span data-ttu-id="3662d-114">安装任何产品或生成你的解决方案，类似于 ASP.NET MVC 的.NET Framework 的版本所需的组件。</span><span class="sxs-lookup"><span data-stu-id="3662d-114">Install any products or components that are required to build your solution, like versions of the .NET Framework or ASP.NET MVC.</span></span>
- <span data-ttu-id="3662d-115">安装 Web 部署 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3662d-115">Install Web Deploy 2.0 or later.</span></span>

<span data-ttu-id="3662d-116">本主题将演示如何执行这些过程，或指向在它们存在的其他资源。</span><span class="sxs-lookup"><span data-stu-id="3662d-116">This topic will show you how to perform these procedures or point to other resources where they exist.</span></span> <span data-ttu-id="3662d-117">任务和本主题中的演练假设：</span><span class="sxs-lookup"><span data-stu-id="3662d-117">The tasks and walkthroughs in this topic assume that:</span></span>

- <span data-ttu-id="3662d-118">刚开始使用运行 Windows Server 2008 R2 Service Pack 1 的干净的服务器内部版本。</span><span class="sxs-lookup"><span data-stu-id="3662d-118">You're starting with a clean server build running Windows Server 2008 R2 Service Pack 1.</span></span>
- <span data-ttu-id="3662d-119">服务器已加入域具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="3662d-119">The server is domain-joined with a static IP address.</span></span>
- <span data-ttu-id="3662d-120">你已在单独服务器上，安装 TFS 应用层，如中所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3662d-120">You've installed the TFS application tier on a separate server, as described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="3662d-121">谁将执行以下步骤？</span><span class="sxs-lookup"><span data-stu-id="3662d-121">Who Performs These Procedures?</span></span>

<span data-ttu-id="3662d-122">在大多数情况下，TFS 管理员将负责配置生成服务器。</span><span class="sxs-lookup"><span data-stu-id="3662d-122">In most cases, a TFS administrator will be responsible for configuring build servers.</span></span> <span data-ttu-id="3662d-123">在某些情况下，开发人员团队可能需要特定的生成服务器的所有权。</span><span class="sxs-lookup"><span data-stu-id="3662d-123">In some cases, the developer team may take ownership of specific build servers.</span></span>

## <a name="install-and-configure-the-tfs-build-service"></a><span data-ttu-id="3662d-124">安装和配置 TFS 生成服务</span><span class="sxs-lookup"><span data-stu-id="3662d-124">Install and Configure the TFS Build Service</span></span>

<span data-ttu-id="3662d-125">在配置生成服务器时，您的首要任务是安装和配置 TFS 生成服务。</span><span class="sxs-lookup"><span data-stu-id="3662d-125">When you configure a build server, your first task is to install and configure the TFS build service.</span></span> <span data-ttu-id="3662d-126">作为此过程的一部分，你将需要：</span><span class="sxs-lookup"><span data-stu-id="3662d-126">As part of this process, you'll need to:</span></span>

- <span data-ttu-id="3662d-127">安装 TFS 生成服务和配置服务帐户。</span><span class="sxs-lookup"><span data-stu-id="3662d-127">Install the TFS build service and configure a service account.</span></span> <span data-ttu-id="3662d-128">任何生成任务，包括部署中，将使用的生成服务帐户身份运行。</span><span class="sxs-lookup"><span data-stu-id="3662d-128">Any build tasks, including deployment, will run using the identity of the build service account.</span></span>
- <span data-ttu-id="3662d-129">创建*生成控制器*和一个或多个*生成代理*。</span><span class="sxs-lookup"><span data-stu-id="3662d-129">Create a *build controller* and one or more *build agents*.</span></span> <span data-ttu-id="3662d-130">每个生成控制器管理一组生成代理。</span><span class="sxs-lookup"><span data-stu-id="3662d-130">Each build controller manages a set of build agents.</span></span> <span data-ttu-id="3662d-131">当您对生成进行排队时，生成控制器将生成任务分配给可用的生成代理。</span><span class="sxs-lookup"><span data-stu-id="3662d-131">When you queue a build, the build controller assigns the build task to an available build agent.</span></span> <span data-ttu-id="3662d-132">在 TFS 中的每个团队项目集合映射到单个生成控制器。</span><span class="sxs-lookup"><span data-stu-id="3662d-132">Each team project collection in TFS is mapped to a single build controller.</span></span>
- <span data-ttu-id="3662d-133">配置生成输出的放置文件夹。</span><span class="sxs-lookup"><span data-stu-id="3662d-133">Configure a drop folder for your build outputs.</span></span> <span data-ttu-id="3662d-134">这是网络共享。</span><span class="sxs-lookup"><span data-stu-id="3662d-134">This is a network share.</span></span> <span data-ttu-id="3662d-135">任何生成输出，如 web 部署包时，被发送到放置文件夹。</span><span class="sxs-lookup"><span data-stu-id="3662d-135">Any build outputs, like web deployment packages, are sent to the drop folder.</span></span>

<span data-ttu-id="3662d-136">[管理 Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) MSDN 上的一章包含所需执行这些任务的所有资源：</span><span class="sxs-lookup"><span data-stu-id="3662d-136">The [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) chapter on MSDN contains all the resources you need in order to perform these tasks:</span></span>

- <span data-ttu-id="3662d-137">有关 Team Foundation Build 的概念性概述，包括生成服务、 生成控制器和生成代理，请参阅[了解 Team Foundation Build 系统](https://msdn.microsoft.com/library/dd793166.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-137">For a conceptual overview of Team Foundation Build, including the build service, build controllers, and build agents, see [Understanding a Team Foundation Build System](https://msdn.microsoft.com/library/dd793166.aspx).</span></span>
- <span data-ttu-id="3662d-138">有关安装和配置生成服务的信息，请参阅[配置生成计算机](https://msdn.microsoft.com/library/ms181712.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-138">For information on installing and configuring the build service, see [Configure a Build Machine](https://msdn.microsoft.com/library/ms181712.aspx).</span></span>
- <span data-ttu-id="3662d-139">创建生成控制器的信息，请参阅[创建和使用生成控制器工作](https://msdn.microsoft.com/library/ee330987.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-139">For information on creating build controllers, see [Create and Work with a Build Controller](https://msdn.microsoft.com/library/ee330987.aspx).</span></span>
- <span data-ttu-id="3662d-140">创建生成代理的信息，请参阅[创建和使用生成代理工作](https://msdn.microsoft.com/library/bb399135.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-140">For information on creating build agents, see [Create and Work with Build Agents](https://msdn.microsoft.com/library/bb399135.aspx).</span></span>
- <span data-ttu-id="3662d-141">有关创建和配置的放置文件夹的信息，请参阅[设置放置文件夹](https://msdn.microsoft.com/library/bb778394.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-141">For information on creating and configuring drop folders, see [Set Up Drop Folders](https://msdn.microsoft.com/library/bb778394.aspx).</span></span>

## <a name="install-required-products-and-components"></a><span data-ttu-id="3662d-142">安装所需的产品和组件</span><span class="sxs-lookup"><span data-stu-id="3662d-142">Install Required Products and Components</span></span>

<span data-ttu-id="3662d-143">若要启用要生成你的解决方案的生成服务器，必须安装任何产品、 组件或您的解决方案需要的程序集。</span><span class="sxs-lookup"><span data-stu-id="3662d-143">To enable the build server to build your solutions, you must install any products, components, or assemblies that your solution requires.</span></span> <span data-ttu-id="3662d-144">在安装任何 web 平台组件之前，应在生成服务器上安装 Visual Studio 2010 （任何版本）。</span><span class="sxs-lookup"><span data-stu-id="3662d-144">Before you install any web platform components, you should install Visual Studio 2010 (any version) on the build server.</span></span> <span data-ttu-id="3662d-145">这可确保将生成服务使用的核心 Microsoft Build Engine (MSBuild) 目标文件及 Web 发布管道 (WPP) 目标文件。</span><span class="sxs-lookup"><span data-stu-id="3662d-145">This ensures that the core Microsoft Build Engine (MSBuild) target files and the Web Publishing Pipeline (WPP) target files are available to the build service.</span></span> <span data-ttu-id="3662d-146">在 Visual Studio 安装程序还应安装 Web 部署，但需要您如果你打算将 web 包部署为生成过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="3662d-146">The Visual Studio installer should also install Web Deploy, which you'll need if you plan to deploy web packages as part of your build process.</span></span>

<span data-ttu-id="3662d-147">安装常用的 web 平台组件的最佳方法是使用[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="3662d-147">The best way to install common web platform components is to use the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span> <span data-ttu-id="3662d-148">这确保要安装最新版本的每个产品，并且它还会自动检测并安装所有必备组件的每个产品。</span><span class="sxs-lookup"><span data-stu-id="3662d-148">This ensures that you're installing the latest version of each product, and it also automatically detects and installs any prerequisites for each product.</span></span> <span data-ttu-id="3662d-149">情况下[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案中，您应使用 Web 平台安装程序来安装这些产品和组件：</span><span class="sxs-lookup"><span data-stu-id="3662d-149">In the case of the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution, you should use the Web Platform Installer to install these products and components:</span></span>

- <span data-ttu-id="3662d-150">**.NET framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="3662d-150">**.NET Framework 4.0**.</span></span> <span data-ttu-id="3662d-151">这是运行此版本的.NET Framework 生成的应用程序所需要的。</span><span class="sxs-lookup"><span data-stu-id="3662d-151">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="3662d-152">**Web 部署工具 2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="3662d-152">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="3662d-153">这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="3662d-153">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="3662d-154">作为此过程的一部分，它会安装并启动 Web 部署代理服务。</span><span class="sxs-lookup"><span data-stu-id="3662d-154">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="3662d-155">此服务允许你部署 web 包从远程计算机。</span><span class="sxs-lookup"><span data-stu-id="3662d-155">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="3662d-156">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="3662d-156">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="3662d-157">这会安装您需要运行 ASP.NET MVC 3 应用程序的程序集。</span><span class="sxs-lookup"><span data-stu-id="3662d-157">This installs the assemblies you need to run ASP.NET MVC 3 applications.</span></span>

<span data-ttu-id="3662d-158">**若要安装必需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="3662d-158">**To install the required products and components**</span></span>

1. <span data-ttu-id="3662d-159">安装 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="3662d-159">Install Visual Studio 2010.</span></span> <span data-ttu-id="3662d-160">当系统提示选择要安装的功能，您应包括：</span><span class="sxs-lookup"><span data-stu-id="3662d-160">When prompted to select features to install, you should include:</span></span>

    1. <span data-ttu-id="3662d-161">您需要编译任何编程语言。</span><span class="sxs-lookup"><span data-stu-id="3662d-161">Any programming languages that you need to compile.</span></span>
    2. <span data-ttu-id="3662d-162">Visual Web 开发人员。</span><span class="sxs-lookup"><span data-stu-id="3662d-162">Visual Web Developer.</span></span> <span data-ttu-id="3662d-163">这可确保 WPP 目标都添加到您的生成服务器。</span><span class="sxs-lookup"><span data-stu-id="3662d-163">This ensures that the WPP targets are added to your build server.</span></span>

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. <span data-ttu-id="3662d-164">Visual Studio 2010 的安装完成后，下载并安装[Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) （如果它尚不存在包含安装介质中）。</span><span class="sxs-lookup"><span data-stu-id="3662d-164">When the installation of Visual Studio 2010 is complete, download and install [Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (if it's not already included in your installation media).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3662d-165">Visual Studio 2010 Service Pack 1 解决了一个 bug，可以防止 MSBuild 查找 MSDeploy 可执行文件。</span><span class="sxs-lookup"><span data-stu-id="3662d-165">Visual Studio 2010 Service Pack 1 resolves a bug that can prevent MSBuild from locating the MSDeploy executable.</span></span>
3. <span data-ttu-id="3662d-166">下载并启动[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="3662d-166">Download and launch the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
4. <span data-ttu-id="3662d-167">在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。</span><span class="sxs-lookup"><span data-stu-id="3662d-167">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
5. <span data-ttu-id="3662d-168">在左侧和右侧的窗口中，在导航窗格中，单击**框架**。</span><span class="sxs-lookup"><span data-stu-id="3662d-168">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
6. <span data-ttu-id="3662d-169">在中**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="3662d-169">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3662d-170">你可能已安装.NET Framework 4.0 到 Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="3662d-170">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="3662d-171">如果已安装的产品或组件，Web 平台安装程序将此信息指示通过替换**外**按钮，其文本**已安装**。</span><span class="sxs-lookup"><span data-stu-id="3662d-171">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. <span data-ttu-id="3662d-172">在中**ASP.NET MVC 3 (Visual Studio 2010)** 行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="3662d-172">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
8. <span data-ttu-id="3662d-173">在导航窗格中，单击**Server**。</span><span class="sxs-lookup"><span data-stu-id="3662d-173">In the navigation pane, click **Server**.</span></span>
9. <span data-ttu-id="3662d-174">在中**Web 部署工具 2.1**行中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="3662d-174">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="3662d-175">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="3662d-175">Click **Install**.</span></span> <span data-ttu-id="3662d-176">Web 平台安装程序将显示产品列表&#x2014;以及任何关联的依赖关系&#x2014;安装，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="3662d-176">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>
11. <span data-ttu-id="3662d-177">查看许可条款，如果同意条款，单击**我接受**。</span><span class="sxs-lookup"><span data-stu-id="3662d-177">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="3662d-178">安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。</span><span class="sxs-lookup"><span data-stu-id="3662d-178">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

> [!NOTE]
> <span data-ttu-id="3662d-179">如果在部署过程包括 VSDBCMD.exe 或 SQLCMD.exe 等工具使用，您将需要确保这些在生成服务器上安装。</span><span class="sxs-lookup"><span data-stu-id="3662d-179">If your deployment process includes the use of tools like VSDBCMD.exe or SQLCMD.exe, you'll need to ensure that these are installed on your build server.</span></span> <span data-ttu-id="3662d-180">VSDBCMD.exe 是 Visual Studio 工具，并在安装 Team Foundation Build 时通常添加到服务器。</span><span class="sxs-lookup"><span data-stu-id="3662d-180">VSDBCMD.exe is a Visual Studio tool and is typically added to the server when you install Team Foundation Build.</span></span> <span data-ttu-id="3662d-181">SQLCMD.exe 是 SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="3662d-181">SQLCMD.exe is a SQL Server tool.</span></span> <span data-ttu-id="3662d-182">可以下载独立版本从 SQLCMD.exe [Microsoft SQL Server 2008 R2 功能包](https://go.microsoft.com/?linkid=9805134)页。</span><span class="sxs-lookup"><span data-stu-id="3662d-182">You can download a stand-alone version of SQLCMD.exe from the [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) page.</span></span>


## <a name="conclusion"></a><span data-ttu-id="3662d-183">结束语</span><span class="sxs-lookup"><span data-stu-id="3662d-183">Conclusion</span></span>

<span data-ttu-id="3662d-184">此时，您的生成服务器已准备好开始构建和部署您的 web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="3662d-184">At this point, your build server is ready to start building and deploying your web application projects.</span></span> <span data-ttu-id="3662d-185">下一主题[创建生成定义，支持部署](creating-a-build-definition-that-supports-deployment.md)，介绍如何创建和配置生成定义来控制何时以及如何生成和部署你的项目。</span><span class="sxs-lookup"><span data-stu-id="3662d-185">The next topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md), describes how to create and configure a build definition to control when and how your projects are built and deployed.</span></span>

## <a name="further-reading"></a><span data-ttu-id="3662d-186">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="3662d-186">Further Reading</span></span>

<span data-ttu-id="3662d-187">有关如何使用 Team Build 的更多常规指南，请参阅[管理 Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3662d-187">For more general guidance on working with Team Build, see [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3662d-188">[上一页](adding-content-to-source-control.md)
> [下一页](creating-a-build-definition-that-supports-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="3662d-188">[Previous](adding-content-to-source-control.md)
[Next](creating-a-build-definition-that-supports-deployment.md)</span></span>
