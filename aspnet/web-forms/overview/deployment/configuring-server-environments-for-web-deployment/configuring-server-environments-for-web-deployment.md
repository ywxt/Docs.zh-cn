---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 用于 Web 部署配置服务器环境 |Microsoft 文档
author: jrjlee
description: 本教程将演示如何设置支持一次单击，或自动、 网站部署和如何在各种不同 scen 中的发布的服务器环境...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: ff6118be618a170ac76d66a9de24a7b5cc2d840a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="configuring-server-environments-for-web-deployment"></a><span data-ttu-id="accf3-103">用于 Web 部署配置服务器环境</span><span class="sxs-lookup"><span data-stu-id="accf3-103">Configuring Server Environments for Web Deployment</span></span>
====================
<span data-ttu-id="accf3-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="accf3-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="accf3-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="accf3-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="accf3-106">本教程将演示如何设置支持一次单击，或自动、 网站部署和如何在各种不同方案中的发布的服务器环境。</span><span class="sxs-lookup"><span data-stu-id="accf3-106">This tutorial will show you how to set up server environments to support one-click, or automated, website deployment and publishing in various different scenarios.</span></span> <span data-ttu-id="accf3-107">本教程包括主题，以指导您完成各种任务，例如，配置 web 服务器以支持特定的方法来部署和设置 Web Farm Framework (WFF) 服务器场中，以及提供的基于方案的概述更高级别的端到端指南。</span><span class="sxs-lookup"><span data-stu-id="accf3-107">The tutorial includes topics to walk you through completing various tasks, like configuring a web server to support specific approaches to deployment and setting up a Web Farm Framework (WFF) server farm, together with scenario-based overviews that provide higher-level end-to-end guidance.</span></span>
> 
> <span data-ttu-id="accf3-108">本教程使用 Fabrikam，Inc.部署方案中所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)作为示例和网络基础结构的引用点。</span><span class="sxs-lookup"><span data-stu-id="accf3-108">The tutorial uses the Fabrikam, Inc. deployment scenario described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) as a reference point for examples and network infrastructure.</span></span>
> 
> <span data-ttu-id="accf3-109">这些教程的意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="accf3-109">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="accf3-110">本教程包括以下主题：</span><span class="sxs-lookup"><span data-stu-id="accf3-110">This tutorial includes these topics:</span></span>

- [<span data-ttu-id="accf3-111">选择 Web 部署的适当方法</span><span class="sxs-lookup"><span data-stu-id="accf3-111">Choosing the Right Approach to Web Deployment</span></span>](choosing-the-right-approach-to-web-deployment.md)
- [<span data-ttu-id="accf3-112">方案：配置用于 Web 部署的测试环境</span><span class="sxs-lookup"><span data-stu-id="accf3-112">Scenario: Configuring a Test Environment for Web Deployment</span></span>](scenario-configuring-a-test-environment-for-web-deployment.md)
- [<span data-ttu-id="accf3-113">方案：配置用于 Web 部署的过渡环境</span><span class="sxs-lookup"><span data-stu-id="accf3-113">Scenario: Configuring a Staging Environment for Web Deployment</span></span>](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [<span data-ttu-id="accf3-114">方案：配置用于 Web 部署的生产环境</span><span class="sxs-lookup"><span data-stu-id="accf3-114">Scenario: Configuring a Production Environment for Web Deployment</span></span>](scenario-configuring-a-production-environment-for-web-deployment.md)
- [<span data-ttu-id="accf3-115">配置用于 Web 部署发布的 Web 服务器（远程代理）</span><span class="sxs-lookup"><span data-stu-id="accf3-115">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [<span data-ttu-id="accf3-116">配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）</span><span class="sxs-lookup"><span data-stu-id="accf3-116">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [<span data-ttu-id="accf3-117">配置用于 Web 部署发布的 Web 服务器（离线部署）</span><span class="sxs-lookup"><span data-stu-id="accf3-117">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [<span data-ttu-id="accf3-118">配置用于 Web 部署发布的数据库服务器</span><span class="sxs-lookup"><span data-stu-id="accf3-118">Configuring a Database Server for Web Deploy Publishing</span></span>](configuring-a-database-server-for-web-deploy-publishing.md)
- [<span data-ttu-id="accf3-119">使用 Web Farm Framework 创建服务器场</span><span class="sxs-lookup"><span data-stu-id="accf3-119">Creating a Server Farm with the Web Farm Framework</span></span>](creating-a-server-farm-with-the-web-farm-framework.md)
- [<span data-ttu-id="accf3-120">配置目标环境的部署属性</span><span class="sxs-lookup"><span data-stu-id="accf3-120">Configuring Deployment Properties for a Target Environment</span></span>](configuring-deployment-properties-for-a-target-environment.md)

<span data-ttu-id="accf3-121">第一个主题，[选择用于 Web 部署的右方法](choosing-the-right-approach-to-web-deployment.md)，描述可用于发布 web 应用程序通过使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 的主要方式 2.0。</span><span class="sxs-lookup"><span data-stu-id="accf3-121">The first topic, [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md), describes the main approaches you can use to publish web applications by using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0.</span></span> <span data-ttu-id="accf3-122">它还标识映射到每种方法的方案。</span><span class="sxs-lookup"><span data-stu-id="accf3-122">It also identifies the scenarios that map to each approach.</span></span> <span data-ttu-id="accf3-123">从此处，每个方案主题提供你需要完成的任务的高级概述，并确定你将需要通过工作，以便帮助你完成这些任务的主题。</span><span class="sxs-lookup"><span data-stu-id="accf3-123">From here, each scenario topic provides a high-level overview of the tasks you need to complete and identifies the topics you'll need to work through to help you complete these tasks.</span></span>

<span data-ttu-id="accf3-124">如果你使用的拆分项目文件方法中所述[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)生成和部署你的解决方案的最后一个主题，[将部署属性配置为目标环境](configuring-deployment-properties-for-a-target-environment.md)，描述如何配置以部署到不同的目标环境的特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="accf3-124">If you're using the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md) to build and deploy your solution, the final topic, [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md), describes how to configure environment-specific project files for deployment to different destination environments.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="accf3-125">主要的技术</span><span class="sxs-lookup"><span data-stu-id="accf3-125">Key Technologies</span></span>

<span data-ttu-id="accf3-126">本教程重点介绍如何使用这些产品和技术支持 web 部署：</span><span class="sxs-lookup"><span data-stu-id="accf3-126">This tutorial focuses on how to use these products and technologies to support web deployment:</span></span>

- <span data-ttu-id="accf3-127">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="accf3-127">IIS 7.5</span></span>
- <span data-ttu-id="accf3-128">Web 部署 2.x</span><span class="sxs-lookup"><span data-stu-id="accf3-128">Web Deploy 2.x</span></span>
- <span data-ttu-id="accf3-129">WFF 2.x</span><span class="sxs-lookup"><span data-stu-id="accf3-129">WFF 2.x</span></span>
- <span data-ttu-id="accf3-130">IIS Web 管理服务 (WMSvc)</span><span class="sxs-lookup"><span data-stu-id="accf3-130">IIS Web Management Service (WMSvc)</span></span>

<span data-ttu-id="accf3-131">本教程还涉及使用 Windows Server 2008 R2、 SQL Server 2008 R2、 ASP.NET 4.0 和 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="accf3-131">The tutorial also touches on the use of Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="accf3-132">在本系列中其他教程</span><span class="sxs-lookup"><span data-stu-id="accf3-132">Other Tutorials in This Series</span></span>

<span data-ttu-id="accf3-133">它在企业级 web 部署构成的五个教程系列中的一部分。</span><span class="sxs-lookup"><span data-stu-id="accf3-133">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="accf3-134">这些是序列中的其他教程：</span><span class="sxs-lookup"><span data-stu-id="accf3-134">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="accf3-135">[部署在企业方案中的 Web 应用程序](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="accf3-135">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="accf3-136">本介绍性内容的系列教程提供上下文的背景。</span><span class="sxs-lookup"><span data-stu-id="accf3-136">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="accf3-137">描述该教程的方案，以及它阐释了任务和在整个系列所述的演练如何适应更广泛的应用程序生命周期管理 (ALM) 过程。</span><span class="sxs-lookup"><span data-stu-id="accf3-137">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="accf3-138">[Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="accf3-138">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="accf3-139">本教程提供 Microsoft Build Engine (MSBuild) 项目文件的概念介绍、 Web 发布管道、 Web 部署和其他相关的技术。</span><span class="sxs-lookup"><span data-stu-id="accf3-139">This tutorial provides a conceptual introduction to Microsoft Build Engine (MSBuild) project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="accf3-140">它还说明了如何使用这些工具在一起来管理复杂部署进程。</span><span class="sxs-lookup"><span data-stu-id="accf3-140">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="accf3-141">[用于 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="accf3-141">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="accf3-142">本教程介绍如何配置 Team Foundation Server (TFS) 以支持各种部署方案，包括作为持续集成 (CI) 过程的一部分的自动的部署和手动触发的特定生成的部署。</span><span class="sxs-lookup"><span data-stu-id="accf3-142">This tutorial describes how to configure Team Foundation Server (TFS) to support various deployment scenarios, including automated deployment as part of a continuous integration (CI) process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="accf3-143">[高级企业级 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="accf3-143">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="accf3-144">本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境、 从部署中排除文件和文件夹以及在部署过程中将 web 应用程序脱机.</span><span class="sxs-lookup"><span data-stu-id="accf3-144">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="accf3-145">下一篇</span><span class="sxs-lookup"><span data-stu-id="accf3-145">Next</span></span>](choosing-the-right-approach-to-web-deployment.md)
