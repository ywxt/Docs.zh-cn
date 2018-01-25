---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: "方案： 配置 Web 部署的生产环境 |Microsoft 文档"
author: jrjlee
description: "本主题介绍典型 web 部署方案中的为生产环境，并说明需要完成为了设置类似的任务..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: cdd13f96ddf08ff86b01ef9de17ea82cf038ab28
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="scenario-configuring-a-production-environment-for-web-deployment"></a><span data-ttu-id="95308-103">方案： 配置 Web 部署的生产环境</span><span class="sxs-lookup"><span data-stu-id="95308-103">Scenario: Configuring a Production Environment for Web Deployment</span></span>
====================
<span data-ttu-id="95308-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="95308-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="95308-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="95308-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="95308-106">本主题介绍典型 web 部署方案中的为生产环境，并说明需要为了设置相似的环境中完成的任务。</span><span class="sxs-lookup"><span data-stu-id="95308-106">This topic describes a typical web deployment scenario for a production environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="95308-107">生产环境是为 web 应用程序或网站的最终目标。</span><span class="sxs-lookup"><span data-stu-id="95308-107">The production environment is the final destination for a web application or a website.</span></span> <span data-ttu-id="95308-108">此时，你的应用程序将已通过测试、 已部署到过渡环境，和已准备好"进入正常运行状态。"</span><span class="sxs-lookup"><span data-stu-id="95308-108">By this point, your application has been through testing, has been deployed to a staging environment, and is ready to "go live."</span></span> <span data-ttu-id="95308-109">生产环境中的特征可能会因广泛的性质和你的 web 内容的目的，你的组织，目标受众和许多其他因素的大小。</span><span class="sxs-lookup"><span data-stu-id="95308-109">The characteristics of a production environment can vary widely according to the nature and purpose of your web content, the size of your organization, your target audience, and lots of other factors.</span></span> <span data-ttu-id="95308-110">在企业级方案中，生产环境可能具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="95308-110">In an enterprise-scale scenario, the production environment may have these characteristics:</span></span>

- <span data-ttu-id="95308-111">环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常与故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="95308-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="95308-112">如果环境处于面向 Internet 的则很可能以从内部网络隔离。</span><span class="sxs-lookup"><span data-stu-id="95308-112">If the environment is Internet-facing, it's likely to be segregated from your internal network.</span></span> <span data-ttu-id="95308-113">也可能在外围网络中的不同子网，它可能位于不同的域，和它可能完全不同的网络基础结构。</span><span class="sxs-lookup"><span data-stu-id="95308-113">It may be on a different subnet in a perimeter network, it may be on a different domain, and it may be on an entirely different network infrastructure.</span></span>
- <span data-ttu-id="95308-114">开发人员和生成服务器的进程帐户是极有可能不在生产服务器上具有管理员特权。</span><span class="sxs-lookup"><span data-stu-id="95308-114">Developers and build server process accounts are highly unlikely to have administrator privileges on the production servers.</span></span>
- <span data-ttu-id="95308-115">更改应用程序部署不太频繁地比测试或过渡部署。</span><span class="sxs-lookup"><span data-stu-id="95308-115">Changes to applications are deployed on a less frequent basis than test or staging deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="95308-116">扩展跨多个服务器的数据库部署不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="95308-116">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="95308-117">有关此区域的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="95308-117">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="95308-118">例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Build 服务器包括让用户生成联系人管理器解决方案并将其部署到过渡环境中单个步骤的生成定义。</span><span class="sxs-lookup"><span data-stu-id="95308-118">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), a Team Build server includes build definitions that let users build the Contact Manager solution and deploy it to a staging environment in a single step.</span></span> <span data-ttu-id="95308-119">应用程序准备好可部署到生产环境中，由于安全要求和网络基础结构，施加的约束时生产环境管理员必须手动复制到生产 web 服务器上的 web 包并导入它通过 Internet 信息服务 (IIS) 管理器。</span><span class="sxs-lookup"><span data-stu-id="95308-119">When the application is ready to be deployed to production, due to the constraints imposed by security requirements and the network infrastructure, the production environment administrator must manually copy the web package onto a production web server and import it through Internet Information Services (IIS) Manager.</span></span>

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a><span data-ttu-id="95308-120">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="95308-120">Solution Overview</span></span>

<span data-ttu-id="95308-121">在此方案中，你可以推断出的部署要求分析从这些事实：</span><span class="sxs-lookup"><span data-stu-id="95308-121">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="95308-122">由于安全限制和网络配置，你无法配置要支持一次单击或自动部署的生产环境。</span><span class="sxs-lookup"><span data-stu-id="95308-122">Due to security restrictions and the network configuration, you can't configure the production environment to support one-click or automated deployment.</span></span> <span data-ttu-id="95308-123">脱机部署是在此方案中的唯一可行方法。</span><span class="sxs-lookup"><span data-stu-id="95308-123">Offline deployment is the only viable approach in this scenario.</span></span>
- <span data-ttu-id="95308-124">生产环境包含多个 web 服务器，因此你可以使用 Web Farm Framework (WFF) 来创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="95308-124">The production environment includes multiple web servers, so you can use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="95308-125">使用此方法，管理员只需导入到一个 web 服务器 （主服务器），应用程序和 WFF 将复制生产环境中的所有 web 服务器上的部署。</span><span class="sxs-lookup"><span data-stu-id="95308-125">Using this approach, the administrator only needs to import the application onto one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the production environment.</span></span>

<span data-ttu-id="95308-126">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="95308-126">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="95308-127">[使用 Web 场框架创建服务器场](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="95308-127">[Create a Server Farm with the Web Farm Framework](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="95308-128">本主题介绍如何创建和配置服务器场使用 WFF，以便跨多个负载平衡的 web 服务器复制的 web 平台产品和组件、 配置设置和网站和应用程序。</span><span class="sxs-lookup"><span data-stu-id="95308-128">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="95308-129">[Web 部署发布 （脱机部署） 配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="95308-129">[Configure a Web Server for Web Deploy Publishing (Offline Deployment)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="95308-130">本主题介绍如何生成该允许管理员导入和部署 web 包，手动从干净的 Windows Server 2008 R2 生成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="95308-130">This topic describes how to build a web server that lets administrators import and deploy web packages manually, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="95308-131">[配置数据库服务器的 Web 部署发布更改](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="95308-131">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="95308-132">本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。</span><span class="sxs-lookup"><span data-stu-id="95308-132">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="95308-133">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="95308-133">Further Reading</span></span>

<span data-ttu-id="95308-134">有关配置的典型的开发人员测试环境的指南，请参阅[方案： 为 Web 部署配置测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="95308-134">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="95308-135">有关配置的典型的过渡环境的指南，请参阅[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="95308-135">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="95308-136">[上一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
[下一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span><span class="sxs-lookup"><span data-stu-id="95308-136">[Previous](scenario-configuring-a-staging-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span></span>
