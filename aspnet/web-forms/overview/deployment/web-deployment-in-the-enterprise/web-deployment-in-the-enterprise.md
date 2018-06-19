---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Web 部署在企业中的 |Microsoft 文档
author: jrjlee
description: 本教程介绍如何迎接大量管理的企业级 web 应用程序到 devel 部署时遇到的难题...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: fc463cb689f4f63a12788b80958c9fc8fe20119d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890458"
---
<a name="web-deployment-in-the-enterprise"></a><span data-ttu-id="a4f6c-103">企业中的 web 部署</span><span class="sxs-lookup"><span data-stu-id="a4f6c-103">Web Deployment in the Enterprise</span></span>
====================
<span data-ttu-id="a4f6c-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a4f6c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a4f6c-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a4f6c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a4f6c-106">本教程介绍如何满足大量管理的企业级 web 应用程序到开发、 测试、 过渡和生产环境部署时遇到的难题。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-106">This tutorial describes how to meet lots of the challenges you'll encounter when you manage the deployment of enterprise-scale web applications to development, test, staging, and production environments.</span></span> <span data-ttu-id="a4f6c-107">本教程包括参考解决方案，以及混合的概念性和面向任务的内容，以指导你确定各种常见任务和过程。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-107">The tutorial includes a reference solution together with a mixture of conceptual and task-oriented content to guide you through various common tasks and procedures.</span></span>
> 
> <span data-ttu-id="a4f6c-108">这些教程的意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-108">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


## <a name="enterprise-deployment-challenges"></a><span data-ttu-id="a4f6c-109">企业部署难题</span><span class="sxs-lookup"><span data-stu-id="a4f6c-109">Enterprise Deployment Challenges</span></span>

<span data-ttu-id="a4f6c-110">它们看起来复杂，企业级解决方案的部署进行管理时，组织通常会遇到这些挑战：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-110">Organizations often encounter these challenges when they look to manage the deployment of complex, enterprise-scale solutions:</span></span>

- <span data-ttu-id="a4f6c-111">你需要能够将项目部署到多个环境，如开发人员或测试环境中，暂存平台和生产服务器。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-111">You need to be able to deploy projects to multiple environments, like developer or test environments, staging platforms, and production servers.</span></span> <span data-ttu-id="a4f6c-112">需要使用不同的配置设置为每个环境中部署的解决方案。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-112">The solution needs to be deployed with different configuration settings for each environment.</span></span>
- <span data-ttu-id="a4f6c-113">需要单步执行或自动生成和部署过程的一部分同时部署多个依赖项目。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-113">You need to deploy multiple dependent projects simultaneously as part of a single-step or automated build and deployment process.</span></span>
- <span data-ttu-id="a4f6c-114">你需要能够到驱动器部署从一个自动化过程。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-114">You need to be able to drive deployment from an automated process.</span></span> <span data-ttu-id="a4f6c-115">例如，你想要使用持续集成 (CI) 进程时在签入新代码部署到测试环境的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-115">For example, you want to use a continuous integration (CI) process to deploy web applications to a test environment when new code is checked in.</span></span>
- <span data-ttu-id="a4f6c-116">你需要能够控制部署过程并从 Visual Studio 外部，设置部署变量如开发人员一般不具备正确的配置设置或为每个目标环境所需的凭据。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-116">You need to be able to control the deployment process and set deployment variables from outside Visual Studio, as developers are unlikely to have the correct configuration settings or the necessary credentials for every target environment.</span></span>
- <span data-ttu-id="a4f6c-117">你需要部署基于架构的数据库项目并保留在后续部署上的现有数据。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-117">You need to deploy schema-based database projects and preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="a4f6c-118">你需要部署上临时成员资格数据库而不部署用户帐户数据。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-118">You need to deploy membership databases on an ad hoc basis without deploying user account data.</span></span> <span data-ttu-id="a4f6c-119">你可能还需要更新已部署的成员资格数据库的架构，而不会丢失现有用户帐户数据。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-119">You may also need to update the schema of deployed membership databases without losing existing user account data.</span></span>
- <span data-ttu-id="a4f6c-120">你需要在将内容部署到各种目标环境时排除特定文件或文件夹。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-120">You need to exclude certain files or folders when you deploy content to various target environments.</span></span>

## <a name="overview-of-approach"></a><span data-ttu-id="a4f6c-121">方法的概述</span><span class="sxs-lookup"><span data-stu-id="a4f6c-121">Overview of Approach</span></span>

<span data-ttu-id="a4f6c-122">本教程中，以及此系列中的其他教程使用此高级的方法来满足上文所述的挑战。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-122">This tutorial, together with the other tutorials in this series, uses this high-level approach to meet the challenges described above.</span></span>

- <span data-ttu-id="a4f6c-123">**使用自定义 Microsoft Build Engine (MSBuild) 项目文件来控制整个生成和部署过程。**</span><span class="sxs-lookup"><span data-stu-id="a4f6c-123">**Use custom Microsoft Build Engine (MSBuild) project files to control the overall build and deployment process.**</span></span>
- <span data-ttu-id="a4f6c-124">这样可以生成和部署解决方案中的每个项目作为一个可编脚本的操作的一部分。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-124">This lets you build and deploy every project in the solution as part of a single, scriptable operation.</span></span>
- <span data-ttu-id="a4f6c-125">使用简单的特定于环境的项目文件配置特定于环境的设置。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-125">Environment-specific settings are configured using simple environment-specific project files.</span></span> <span data-ttu-id="a4f6c-126">与使用解决方案配置的 Visual Studio – 以中心的方法和发布配置文件配置不同的环境的部署，此方法允许你配置和管理从 Visual Studio 外部的部署过程。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-126">In contrast to the Visual Studio–centric approach of using solution configurations and publish profiles to configure deployments for different environments, this approach lets you configure and manage the deployment process from outside Visual Studio.</span></span> <span data-ttu-id="a4f6c-127">这意味着开发人员不需要提前知道连接字符串、 服务终结点、 服务器凭据和目标环境的其他部署变量。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-127">This means that developers don't need advance knowledge of connection strings, service endpoints, server credentials, and other deployment variables for destination environments.</span></span>
- <span data-ttu-id="a4f6c-128">Team Build Team Foundation Server (TFS) 工作流的一部分，可以调用自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-128">The custom project files can be invoked by Team Build as part of a Team Foundation Server (TFS) workflow.</span></span> <span data-ttu-id="a4f6c-129">这允许您配置 CI 方案的自动的部署。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-129">This lets you configure automated deployment for CI scenarios.</span></span>

<span data-ttu-id="a4f6c-130">**使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 打包和部署 web 应用程序项目。**</span><span class="sxs-lookup"><span data-stu-id="a4f6c-130">**Use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to package and deploy web application projects.**</span></span>

- <span data-ttu-id="a4f6c-131">Web 部署提供一个框架，允许您打包并将你的 web 应用程序内容部署到的目标 IIS web 服务器，以及依赖项、 配置设置、 安全设置和任何其他要求。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-131">Web Deploy provides a framework that lets you package and deploy your web application content to a destination IIS web server, together with dependencies, configuration settings, security settings, and any other requirements.</span></span>
- <span data-ttu-id="a4f6c-132">在自定义 MSBuild 项目文件中，可以控制从整个的打包和部署过程。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-132">You can control the entire packaging and deployment process from within your custom MSBuild project files.</span></span> <span data-ttu-id="a4f6c-133">您还可以操作伴随 web 部署包，如连接字符串、 服务终结点和 IIS 目标详细信息的配置设置。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-133">You can also manipulate the configuration settings that accompany your web deployment package, like connection strings, service endpoints, and IIS destination details.</span></span>
- <span data-ttu-id="a4f6c-134">Web 部署，以及 Web 发布管道，提供大量扩展点允许你自定义你的部署。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-134">Web Deploy, together with the Web Publishing Pipeline, offers lots of extensibility points that let you customize your deployments.</span></span> <span data-ttu-id="a4f6c-135">例如，很容易从您的 web 部署包中排除不需要的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-135">For example, it's easy to exclude unwanted files and folders from your web deployment packages.</span></span>

<span data-ttu-id="a4f6c-136">**使用 VSDBCMD.exe 实用程序来部署和更新数据库架构。**</span><span class="sxs-lookup"><span data-stu-id="a4f6c-136">**Use the VSDBCMD.exe utility to deploy and update database schemas.**</span></span>

- <span data-ttu-id="a4f6c-137">VSDBCMD 可以部署中生成 Visual Studio 数据库项目时，生成的数据库架构文件 (.dbschema) 的数据库。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-137">VSDBCMD allows you to deploy databases from a database schema file (.dbschema), which is generated when you build a Visual Studio database project.</span></span> <span data-ttu-id="a4f6c-138">与此相反，Web 部署中包含的数据库部署功能是更适合为从本地 SQL Server 实例部署现有数据库。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-138">In contrast, the database deployment functionality included in Web Deploy is more suited to deploying existing databases from a local SQL Server instance.</span></span>
- <span data-ttu-id="a4f6c-139">与用于部署数据库项目的 Visual Studio 的功能，不同 VSDBCMD 可让你部署到现有的目标数据库的差异的更新。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-139">Unlike Visual Studio's functionality for deploying database projects, VSDBCMD lets you deploy differential updates to an existing target database.</span></span> <span data-ttu-id="a4f6c-140">这样，你可以升级数据库架构时保留任何现有数据。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-140">This allows you to preserve any existing data while you upgrade the database schema.</span></span>
- <span data-ttu-id="a4f6c-141">你可以在自定义 MSBuild 项目文件中执行从 VSDBCMD 命令。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-141">You can execute VSDBCMD commands from within your custom MSBuild project files.</span></span>

## <a name="content-map"></a><span data-ttu-id="a4f6c-142">内容地图</span><span class="sxs-lookup"><span data-stu-id="a4f6c-142">Content Map</span></span>

<span data-ttu-id="a4f6c-143">本教程包括分为四个主要方面的主题。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-143">This tutorial includes topics that fall into four main areas.</span></span>

<span data-ttu-id="a4f6c-144">这些主题还将介绍参考解决方案&#x2014;联系人管理器解决方案&#x2014;并描述如何下载它并将其配置本地计算机上：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-144">These topics introduce the reference solution&#x2014;the Contact Manager solution&#x2014;and describe how to download it and configure it on your local machine:</span></span>

- [<span data-ttu-id="a4f6c-145">Contact Manager 解决方案</span><span class="sxs-lookup"><span data-stu-id="a4f6c-145">The Contact Manager Solution</span></span>](the-contact-manager-solution.md)
- [<span data-ttu-id="a4f6c-146">设置 Contact Manager 解决方案</span><span class="sxs-lookup"><span data-stu-id="a4f6c-146">Setting Up the Contact Manager Solution</span></span>](setting-up-the-contact-manager-solution.md)

<span data-ttu-id="a4f6c-147">这些主题介绍 MSBuild 项目文件，描述如何创建和使用自定义项目文件和演练联系人管理器解决方案的部署过程：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-147">These topics introduce MSBuild project files, describe how you can create and use custom project files, and walk through the deployment process for the Contact Manager solution:</span></span>

- [<span data-ttu-id="a4f6c-148">了解项目文件</span><span class="sxs-lookup"><span data-stu-id="a4f6c-148">Understanding the Project File</span></span>](understanding-the-project-file.md)
- [<span data-ttu-id="a4f6c-149">了解生成过程</span><span class="sxs-lookup"><span data-stu-id="a4f6c-149">Understanding the Build Process</span></span>](understanding-the-build-process.md)

<span data-ttu-id="a4f6c-150">这些主题描述 web 应用程序部署，包括如何生成和打包进程的工作原理、 如何与 Web 发布管道集成生成过程、 如何修改部署参数和如何将 web 包部署到目标环境：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-150">These topics describe web application deployment, including how the build and packaging process works, how the build process integrates with the Web Publishing Pipeline, how to modify deployment parameters, and how to deploy web packages to destination environments:</span></span>

- [<span data-ttu-id="a4f6c-151">生成和打包 Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="a4f6c-151">Building and Packaging Web Application Projects</span></span>](building-and-packaging-web-application-projects.md)
- [<span data-ttu-id="a4f6c-152">为 Web 程序包部署配置参数</span><span class="sxs-lookup"><span data-stu-id="a4f6c-152">Configuring Parameters for Web Package Deployment</span></span>](configuring-parameters-for-web-package-deployment.md)
- [<span data-ttu-id="a4f6c-153">部署 Web 程序包</span><span class="sxs-lookup"><span data-stu-id="a4f6c-153">Deploying Web Packages</span></span>](deploying-web-packages.md)

- <span data-ttu-id="a4f6c-154">[部署数据库项目](deploying-database-projects.md)介绍不同的技术可用于部署 Visual Studio 数据库项目，以及每种方法的优缺点。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-154">[Deploying Database Projects](deploying-database-projects.md) describes the different techniques you can use to deploy Visual Studio database projects, together with the advantages and disadvantages of each approach.</span></span> <span data-ttu-id="a4f6c-155">[创建并运行部署命令文件](creating-and-running-a-deployment-command-file.md)描述如何创建一个简单的命令文件，它封装你的部署逻辑，并可以为单步执行过程中部署复杂的解决方案。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-155">[Creating and Running a Deployment Command File](creating-and-running-a-deployment-command-file.md) describes how to create a simple command file that encapsulates your deployment logic and lets you deploy complex solutions as a single-step process.</span></span>
- <span data-ttu-id="a4f6c-156">最后，[手动安装 Web 包](manually-installing-web-packages.md)到教程结束通过显示你可以将 web 包导入到 IIS。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-156">Finally, [Manually Installing Web Packages](manually-installing-web-packages.md) concludes the tutorial by showing you to import web packages into IIS.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="a4f6c-157">主要的技术</span><span class="sxs-lookup"><span data-stu-id="a4f6c-157">Key Technologies</span></span>

<span data-ttu-id="a4f6c-158">在本教程中的主题主要使用这些技术来管理生成和部署：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-158">The topics in this tutorial primarily use these technologies to manage build and deployment:</span></span>

- <span data-ttu-id="a4f6c-159">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="a4f6c-159">Visual Studio 2010</span></span>
- <span data-ttu-id="a4f6c-160">MSBuild</span><span class="sxs-lookup"><span data-stu-id="a4f6c-160">MSBuild</span></span>
- <span data-ttu-id="a4f6c-161">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="a4f6c-161">IIS 7.5</span></span>
- <span data-ttu-id="a4f6c-162">Web Deploy 2.0</span><span class="sxs-lookup"><span data-stu-id="a4f6c-162">Web Deploy 2.0</span></span>
- <span data-ttu-id="a4f6c-163">VSDBCMD.exe 数据库部署实用工具</span><span class="sxs-lookup"><span data-stu-id="a4f6c-163">The VSDBCMD.exe database deployment utility</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="a4f6c-164">在本系列中其他教程</span><span class="sxs-lookup"><span data-stu-id="a4f6c-164">Other Tutorials in This Series</span></span>

<span data-ttu-id="a4f6c-165">它在企业级 web 部署构成的五个教程系列中的一部分。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-165">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="a4f6c-166">这些是序列中的其他教程：</span><span class="sxs-lookup"><span data-stu-id="a4f6c-166">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="a4f6c-167">[部署在企业方案中的 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-167">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="a4f6c-168">本介绍性内容的系列教程提供上下文的背景。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-168">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="a4f6c-169">描述该教程的方案，以及它阐释了任务和在整个系列所述的演练如何适应更广泛的应用程序生命周期管理 (ALM) 过程。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-169">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="a4f6c-170">[用于 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-170">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="a4f6c-171">本教程介绍如何配置 Windows server 以支持各种部署方案，包括使用 Web 部署代理服务 （远程代理） 或 Web 部署处理程序和远程数据库部署的远程 web 包部署。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-171">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the remote agent) or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="a4f6c-172">它提供有关选择你自己的环境的适当的部署方法的指导，并描述了如何使用 Web Farm Framework (WFF) 在服务器场中的所有 web 服务器上复制已部署的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-172">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the Web Farm Framework (WFF) to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="a4f6c-173">[用于 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-173">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="a4f6c-174">本教程介绍如何配置 TFS 以支持各种部署方案，包括 CI 过程的一部分的自动的部署和手动触发的特定生成的部署。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-174">This tutorial describes how to configure TFS to support various deployment scenarios, including automated deployment as part of a CI process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="a4f6c-175">[高级企业级 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a4f6c-175">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="a4f6c-176">本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境、 从部署中排除文件和文件夹以及在部署过程中将 web 应用程序脱机.</span><span class="sxs-lookup"><span data-stu-id="a4f6c-176">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a4f6c-177">下一篇</span><span class="sxs-lookup"><span data-stu-id="a4f6c-177">Next</span></span>](the-contact-manager-solution.md)
