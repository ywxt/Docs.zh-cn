---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 方案： 配置用于 Web 部署的生产环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍适用于生产环境的典型的 web 部署方案，并介绍了所需完成若要设置类似的任务...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 3627d18e1b102c574726282780239464be04c04b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834125"
---
<a name="scenario-configuring-a-production-environment-for-web-deployment"></a><span data-ttu-id="e736b-103">方案： 配置用于 Web 部署的生产环境</span><span class="sxs-lookup"><span data-stu-id="e736b-103">Scenario: Configuring a Production Environment for Web Deployment</span></span>
====================
<span data-ttu-id="e736b-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e736b-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e736b-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e736b-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e736b-106">本主题介绍适用于生产环境的典型的 web 部署方案，并说明完成若要设置类似的环境所需的任务。</span><span class="sxs-lookup"><span data-stu-id="e736b-106">This topic describes a typical web deployment scenario for a production environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="e736b-107">在生产环境是 web 应用程序或网站的最终目标。</span><span class="sxs-lookup"><span data-stu-id="e736b-107">The production environment is the final destination for a web application or a website.</span></span> <span data-ttu-id="e736b-108">此时，你的应用程序将已通过测试，已部署到过渡环境，并已准备好"go live。"</span><span class="sxs-lookup"><span data-stu-id="e736b-108">By this point, your application has been through testing, has been deployed to a staging environment, and is ready to "go live."</span></span> <span data-ttu-id="e736b-109">生产环境中的特征可能会因广泛的性质和用途的 web 内容、 组织、 目标受众和很多其他因素的大小。</span><span class="sxs-lookup"><span data-stu-id="e736b-109">The characteristics of a production environment can vary widely according to the nature and purpose of your web content, the size of your organization, your target audience, and lots of other factors.</span></span> <span data-ttu-id="e736b-110">在企业级方案中，在生产环境可能具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="e736b-110">In an enterprise-scale scenario, the production environment may have these characteristics:</span></span>

- <span data-ttu-id="e736b-111">环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常使用故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="e736b-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="e736b-112">如果环境是面向 Internet 的很可能从内部网络隔离。</span><span class="sxs-lookup"><span data-stu-id="e736b-112">If the environment is Internet-facing, it's likely to be segregated from your internal network.</span></span> <span data-ttu-id="e736b-113">不同的子网外围网络中可能会、 在不同域中，可能会和它可能是完全不同的网络基础结构上。</span><span class="sxs-lookup"><span data-stu-id="e736b-113">It may be on a different subnet in a perimeter network, it may be on a different domain, and it may be on an entirely different network infrastructure.</span></span>
- <span data-ttu-id="e736b-114">开发人员和生成服务器进程帐户是高度不大可能在生产服务器上具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="e736b-114">Developers and build server process accounts are highly unlikely to have administrator privileges on the production servers.</span></span>
- <span data-ttu-id="e736b-115">更改应用程序比测试或过渡部署不太频繁地部署。</span><span class="sxs-lookup"><span data-stu-id="e736b-115">Changes to applications are deployed on a less frequent basis than test or staging deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="e736b-116">跨多个服务器横向扩展数据库部署不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="e736b-116">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="e736b-117">此区域的详细信息，请查阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e736b-117">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="e736b-118">例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Build 服务器包括让用户构建 Contact Manager 解决方案，并将其部署到过渡环境中单个步骤的生成定义。</span><span class="sxs-lookup"><span data-stu-id="e736b-118">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), a Team Build server includes build definitions that let users build the Contact Manager solution and deploy it to a staging environment in a single step.</span></span> <span data-ttu-id="e736b-119">准备好部署到生产环境中，由于施加的安全要求和网络基础结构，限制应用程序时必须手动复制到生产 web 服务器上的 web 包并导入生产环境管理员它通过 Internet 信息服务 (IIS) 管理器。</span><span class="sxs-lookup"><span data-stu-id="e736b-119">When the application is ready to be deployed to production, due to the constraints imposed by security requirements and the network infrastructure, the production environment administrator must manually copy the web package onto a production web server and import it through Internet Information Services (IIS) Manager.</span></span>

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a><span data-ttu-id="e736b-120">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="e736b-120">Solution Overview</span></span>

<span data-ttu-id="e736b-121">在此方案中，您可以推断出的部署要求分析从这些事实：</span><span class="sxs-lookup"><span data-stu-id="e736b-121">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="e736b-122">由于安全限制和网络配置，不能配置为支持一次单击或自动部署在生产环境。</span><span class="sxs-lookup"><span data-stu-id="e736b-122">Due to security restrictions and the network configuration, you can't configure the production environment to support one-click or automated deployment.</span></span> <span data-ttu-id="e736b-123">离线部署是在此方案中唯一的可行的方法。</span><span class="sxs-lookup"><span data-stu-id="e736b-123">Offline deployment is the only viable approach in this scenario.</span></span>
- <span data-ttu-id="e736b-124">在生产环境包括多个 web 服务器，因此可以使用 Web Farm Framework (WFF) 来创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="e736b-124">The production environment includes multiple web servers, so you can use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="e736b-125">使用此方法，管理员只需导入应用程序部署到一个 web 服务器 （主服务器），并在 WFF 复制生产环境中的所有其他 web 服务器上部署。</span><span class="sxs-lookup"><span data-stu-id="e736b-125">Using this approach, the administrator only needs to import the application onto one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the production environment.</span></span>

<span data-ttu-id="e736b-126">这些主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="e736b-126">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="e736b-127">[使用 Web Farm Framework 创建服务器场](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-127">[Create a Server Farm with the Web Farm Framework](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="e736b-128">本主题介绍如何创建和配置使用 WFF，服务器场，以使 web 平台产品和组件、 配置设置和网站和应用程序复制到多个负载平衡的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="e736b-128">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="e736b-129">[配置 Web 服务器，用于 Web 部署发布 （离线部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-129">[Configure a Web Server for Web Deploy Publishing (Offline Deployment)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="e736b-130">本主题介绍如何构建可让管理员导入和部署 web 包手动从干净的 Windows Server 2008 R2 生成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="e736b-130">This topic describes how to build a web server that lets administrators import and deploy web packages manually, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="e736b-131">[配置数据库服务器，用于 Web 部署发布](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-131">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="e736b-132">本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。</span><span class="sxs-lookup"><span data-stu-id="e736b-132">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="e736b-133">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="e736b-133">Further Reading</span></span>

<span data-ttu-id="e736b-134">有关配置典型的开发人员的测试环境的指导，请参阅[方案： 配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-134">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="e736b-135">有关配置典型的过渡环境的指导，请参阅[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="e736b-135">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e736b-136">[上一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span><span class="sxs-lookup"><span data-stu-id="e736b-136">[Previous](scenario-configuring-a-staging-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span></span>
