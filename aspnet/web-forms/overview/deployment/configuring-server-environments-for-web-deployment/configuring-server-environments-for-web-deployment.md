---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 配置用于 Web 部署的服务器环境 |Microsoft Docs
author: jrjlee
description: 本教程将演示如何设置支持一次单击，或自动、 网站部署和发布各种不同方案中的服务器环境...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 4f6433f0b8a9ad3b3634c9bcd8d95015eebaa865
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833464"
---
<a name="configuring-server-environments-for-web-deployment"></a><span data-ttu-id="60086-103">配置用于 Web 部署的服务器环境</span><span class="sxs-lookup"><span data-stu-id="60086-103">Configuring Server Environments for Web Deployment</span></span>
====================
<span data-ttu-id="60086-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="60086-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="60086-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="60086-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="60086-106">本教程将演示如何设置支持一次单击，或自动、 网站部署和发布各种不同方案中的服务器环境。</span><span class="sxs-lookup"><span data-stu-id="60086-106">This tutorial will show you how to set up server environments to support one-click, or automated, website deployment and publishing in various different scenarios.</span></span> <span data-ttu-id="60086-107">本教程包括主题向您逐步完成各种任务，如配置 web 服务器以支持部署和设置 Web Farm Framework (WFF) 服务器场中，提供的基于方案的概述以及特定方法更高级别的的端到端指南。</span><span class="sxs-lookup"><span data-stu-id="60086-107">The tutorial includes topics to walk you through completing various tasks, like configuring a web server to support specific approaches to deployment and setting up a Web Farm Framework (WFF) server farm, together with scenario-based overviews that provide higher-level end-to-end guidance.</span></span>
> 
> <span data-ttu-id="60086-108">本教程使用 Fabrikam，Inc.部署方案中所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)有关示例和网络基础结构的参考点。</span><span class="sxs-lookup"><span data-stu-id="60086-108">The tutorial uses the Fabrikam, Inc. deployment scenario described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) as a reference point for examples and network infrastructure.</span></span>
> 
> <span data-ttu-id="60086-109">这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="60086-109">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="60086-110">本教程包括以下主题：</span><span class="sxs-lookup"><span data-stu-id="60086-110">This tutorial includes these topics:</span></span>

- [<span data-ttu-id="60086-111">选择 Web 部署的适当方法</span><span class="sxs-lookup"><span data-stu-id="60086-111">Choosing the Right Approach to Web Deployment</span></span>](choosing-the-right-approach-to-web-deployment.md)
- [<span data-ttu-id="60086-112">方案：配置用于 Web 部署的测试环境</span><span class="sxs-lookup"><span data-stu-id="60086-112">Scenario: Configuring a Test Environment for Web Deployment</span></span>](scenario-configuring-a-test-environment-for-web-deployment.md)
- [<span data-ttu-id="60086-113">方案：配置用于 Web 部署的过渡环境</span><span class="sxs-lookup"><span data-stu-id="60086-113">Scenario: Configuring a Staging Environment for Web Deployment</span></span>](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [<span data-ttu-id="60086-114">方案：配置用于 Web 部署的生产环境</span><span class="sxs-lookup"><span data-stu-id="60086-114">Scenario: Configuring a Production Environment for Web Deployment</span></span>](scenario-configuring-a-production-environment-for-web-deployment.md)
- [<span data-ttu-id="60086-115">配置用于 Web 部署发布的 Web 服务器（远程代理）</span><span class="sxs-lookup"><span data-stu-id="60086-115">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [<span data-ttu-id="60086-116">配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）</span><span class="sxs-lookup"><span data-stu-id="60086-116">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [<span data-ttu-id="60086-117">配置用于 Web 部署发布的 Web 服务器（离线部署）</span><span class="sxs-lookup"><span data-stu-id="60086-117">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [<span data-ttu-id="60086-118">配置用于 Web 部署发布的数据库服务器</span><span class="sxs-lookup"><span data-stu-id="60086-118">Configuring a Database Server for Web Deploy Publishing</span></span>](configuring-a-database-server-for-web-deploy-publishing.md)
- [<span data-ttu-id="60086-119">使用 Web Farm Framework 创建服务器场</span><span class="sxs-lookup"><span data-stu-id="60086-119">Creating a Server Farm with the Web Farm Framework</span></span>](creating-a-server-farm-with-the-web-farm-framework.md)
- [<span data-ttu-id="60086-120">配置目标环境的部署属性</span><span class="sxs-lookup"><span data-stu-id="60086-120">Configuring Deployment Properties for a Target Environment</span></span>](configuring-deployment-properties-for-a-target-environment.md)

<span data-ttu-id="60086-121">第一个主题[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)，介绍主要方法可用于发布 web 应用程序通过使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0。</span><span class="sxs-lookup"><span data-stu-id="60086-121">The first topic, [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md), describes the main approaches you can use to publish web applications by using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0.</span></span> <span data-ttu-id="60086-122">它还标识将映射到每种方法的方案。</span><span class="sxs-lookup"><span data-stu-id="60086-122">It also identifies the scenarios that map to each approach.</span></span> <span data-ttu-id="60086-123">从此处，每个方案主题提供所需完成的任务的高级概述，并标识你将需要通过工作，以帮助您完成这些任务的主题。</span><span class="sxs-lookup"><span data-stu-id="60086-123">From here, each scenario topic provides a high-level overview of the tasks you need to complete and identifies the topics you'll need to work through to help you complete these tasks.</span></span>

<span data-ttu-id="60086-124">如果您正使用拆分项目文件方法中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)生成和部署你的解决方案，最后一个主题，[为目标环境配置部署属性](configuring-deployment-properties-for-a-target-environment.md)，介绍如何配置部署到不同目标环境的特定于环境的项目文件。</span><span class="sxs-lookup"><span data-stu-id="60086-124">If you're using the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md) to build and deploy your solution, the final topic, [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md), describes how to configure environment-specific project files for deployment to different destination environments.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="60086-125">关键技术</span><span class="sxs-lookup"><span data-stu-id="60086-125">Key Technologies</span></span>

<span data-ttu-id="60086-126">本教程重点介绍如何使用这些产品和技术来支持 web 部署：</span><span class="sxs-lookup"><span data-stu-id="60086-126">This tutorial focuses on how to use these products and technologies to support web deployment:</span></span>

- <span data-ttu-id="60086-127">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="60086-127">IIS 7.5</span></span>
- <span data-ttu-id="60086-128">Web 部署 2.x</span><span class="sxs-lookup"><span data-stu-id="60086-128">Web Deploy 2.x</span></span>
- <span data-ttu-id="60086-129">WFF 2.x</span><span class="sxs-lookup"><span data-stu-id="60086-129">WFF 2.x</span></span>
- <span data-ttu-id="60086-130">IIS Web 管理服务 (WMSvc)</span><span class="sxs-lookup"><span data-stu-id="60086-130">IIS Web Management Service (WMSvc)</span></span>

<span data-ttu-id="60086-131">本教程还涉及使用 Windows Server 2008 R2、 SQL Server 2008 R2、 ASP.NET 4.0 中，和 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="60086-131">The tutorial also touches on the use of Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="60086-132">本系列中的其他教程</span><span class="sxs-lookup"><span data-stu-id="60086-132">Other Tutorials in This Series</span></span>

<span data-ttu-id="60086-133">这在企业级 web 部署窗体的一系列五个教程的一部分。</span><span class="sxs-lookup"><span data-stu-id="60086-133">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="60086-134">以下是其他教程系列中：</span><span class="sxs-lookup"><span data-stu-id="60086-134">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="60086-135">[部署 Web 应用程序在企业方案中的](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="60086-135">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="60086-136">此介绍性内容提供了为系列教程的上下文的背景。</span><span class="sxs-lookup"><span data-stu-id="60086-136">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="60086-137">它描述了教程的方案，并说明了任务和演练所述在整个系列如何适应更广泛的应用程序生命周期管理 (ALM) 过程。</span><span class="sxs-lookup"><span data-stu-id="60086-137">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="60086-138">[Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="60086-138">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="60086-139">本教程提供了 Microsoft Build Engine (MSBuild) 项目文件的概念介绍，Web 发布管道、 Web 部署和其他相关的技术。</span><span class="sxs-lookup"><span data-stu-id="60086-139">This tutorial provides a conceptual introduction to Microsoft Build Engine (MSBuild) project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="60086-140">它介绍了如何使用这些工具一起管理复杂部署过程。</span><span class="sxs-lookup"><span data-stu-id="60086-140">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="60086-141">[配置用于 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="60086-141">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="60086-142">本教程介绍如何配置 Team Foundation Server (TFS) 以支持多种部署方案，包括持续集成 (CI) 过程的一部分的自动的部署和手动触发部署的特定版本。</span><span class="sxs-lookup"><span data-stu-id="60086-142">This tutorial describes how to configure Team Foundation Server (TFS) to support various deployment scenarios, including automated deployment as part of a continuous integration (CI) process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="60086-143">[高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="60086-143">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="60086-144">本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境中，从部署中排除文件和文件夹和在部署过程中将 web 应用程序脱机.</span><span class="sxs-lookup"><span data-stu-id="60086-144">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="60086-145">下一篇</span><span class="sxs-lookup"><span data-stu-id="60086-145">Next</span></span>](choosing-the-right-approach-to-web-deployment.md)
