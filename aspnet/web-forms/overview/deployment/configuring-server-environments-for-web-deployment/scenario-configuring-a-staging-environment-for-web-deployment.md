---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 方案： 配置 Web 部署的过渡环境 |Microsoft 文档
author: jrjlee
description: 本主题介绍典型 web 部署方案中的过渡环境，并说明需要为了设置类似 env 完成的任务...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 3864559b0599091beeacb87e90e80a51285039df
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892317"
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="10a91-103">方案： 配置 Web 部署的过渡环境</span><span class="sxs-lookup"><span data-stu-id="10a91-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>
====================
<span data-ttu-id="10a91-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="10a91-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="10a91-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="10a91-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="10a91-106">本主题介绍典型 web 部署方案中的过渡环境，并说明需要为了设置相似的环境中完成的任务。</span><span class="sxs-lookup"><span data-stu-id="10a91-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="10a91-107">很多组织使用过渡环境来预览更新对 web 应用程序或网站。</span><span class="sxs-lookup"><span data-stu-id="10a91-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="10a91-108">这样，组织内的人员有机会浏览并查看新功能或内容之前的站点"实时，在显示"或换而言之部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="10a91-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="10a91-109">过渡环境旨在尽可能真实地复制生产环境，以便提供真实的预览。</span><span class="sxs-lookup"><span data-stu-id="10a91-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="10a91-110">这种过渡环境通常具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="10a91-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="10a91-111">环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常与故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="10a91-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="10a91-112">由开发团队或自动由 Team Build 服务器可能手动部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="10a91-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="10a91-113">用户或部署应用程序的进程帐户不太可能可以临时服务器上具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="10a91-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="10a91-114">更改应用程序将部署频繁，因此环境需要支持单步执行或自动部署。</span><span class="sxs-lookup"><span data-stu-id="10a91-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="10a91-115">扩展跨多个服务器的数据库部署不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="10a91-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="10a91-116">有关此区域的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="10a91-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="10a91-117">例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Foundation Server (TFS) 管理联系人管理器解决方案。</span><span class="sxs-lookup"><span data-stu-id="10a91-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="10a91-118">TFS 管理员，Rob Walters 已创建，触发部署到过渡环境所需的开发人员可以生成定义。</span><span class="sxs-lookup"><span data-stu-id="10a91-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="10a91-119">请注意，在大多数情况下，你将不一定需要将最新版本部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="10a91-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="10a91-120">相反，你很多更有可能想要部署已进行了验证和验证在测试环境中的特定版本。</span><span class="sxs-lookup"><span data-stu-id="10a91-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="10a91-121">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="10a91-121">Solution Overview</span></span>

<span data-ttu-id="10a91-122">在此方案中，你可以推断出的部署要求分析从这些事实：</span><span class="sxs-lookup"><span data-stu-id="10a91-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="10a91-123">执行部署的用户或进程帐户不会在暂存服务器上拥有管理员权限，以便过渡的 web 服务器必须支持非管理员部署。</span><span class="sxs-lookup"><span data-stu-id="10a91-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="10a91-124">在这种情况下，你将需要配置过渡的 web 服务器，使用 Web 部署处理程序，而不是远程代理。</span><span class="sxs-lookup"><span data-stu-id="10a91-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="10a91-125">过渡环境包括多个 web 服务器，但它需要支持一次单击或自动部署，因此将需要使用 Web Farm Framework (WFF) 来创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="10a91-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="10a91-126">使用此方法，你可以部署到一个 web 服务器 （主服务器），应用程序和 WFF 将复制在过渡环境中的所有 web 服务器上的部署。</span><span class="sxs-lookup"><span data-stu-id="10a91-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="10a91-127">用户或执行部署的进程帐户必须有权创建数据库。</span><span class="sxs-lookup"><span data-stu-id="10a91-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="10a91-128">在这种情况下，你将需要将帐户添加到**dbcreator**在数据库服务器上，除了配置数据库服务器来支持远程访问和部署的服务器角色。</span><span class="sxs-lookup"><span data-stu-id="10a91-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="10a91-129">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="10a91-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="10a91-130">[使用 Web 场框架创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="10a91-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="10a91-131">本主题介绍如何创建和配置服务器场使用 WFF，以便跨多个负载平衡的 web 服务器复制的 web 平台产品和组件、 配置设置和网站和应用程序。</span><span class="sxs-lookup"><span data-stu-id="10a91-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="10a91-132">[Web 部署发布更改配置 Web 服务器 （Web 部署处理程序）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="10a91-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="10a91-133">本主题介绍如何生成支持 Web 部署发布，使用远程代理方法中，从干净的 Windows Server 2008 R2 生成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="10a91-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="10a91-134">[配置数据库服务器的 Web 部署发布更改](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="10a91-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="10a91-135">本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。</span><span class="sxs-lookup"><span data-stu-id="10a91-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="10a91-136">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="10a91-136">Further Reading</span></span>

<span data-ttu-id="10a91-137">有关配置的典型的开发人员测试环境的指南，请参阅[方案： 为 Web 部署配置测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="10a91-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="10a91-138">有关配置的典型生产环境的指南，请参阅[方案： 配置 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="10a91-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="10a91-139">[上一页](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一页](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="10a91-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
