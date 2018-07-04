---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 方案： 配置用于 Web 部署的过渡环境 |Microsoft Docs
author: jrjlee
description: 本主题描述过渡环境的典型的 web 部署方案，并说明才能设置类似 env 完成所需的任务...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: fda4f056eebb77df3e93c63bdd4fabb071c0a0a9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365222"
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="79d90-103">方案： 配置用于 Web 部署的过渡环境</span><span class="sxs-lookup"><span data-stu-id="79d90-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>
====================
<span data-ttu-id="79d90-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="79d90-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="79d90-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="79d90-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="79d90-106">本主题介绍过渡环境的典型的 web 部署方案，并说明所需设置类似的环境才能完成的任务。</span><span class="sxs-lookup"><span data-stu-id="79d90-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="79d90-107">许多组织使用过渡环境来预览对 web 应用程序或网站的更新。</span><span class="sxs-lookup"><span data-stu-id="79d90-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="79d90-108">这使组织内的人有机会浏览和之前的站点"会运行，"，或换句话说部署到生产环境，请查看新功能或内容。</span><span class="sxs-lookup"><span data-stu-id="79d90-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="79d90-109">在过渡环境旨在尽可能真实地复制生产环境，以便提供真实的预览。</span><span class="sxs-lookup"><span data-stu-id="79d90-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="79d90-110">这种过渡环境通常具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="79d90-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="79d90-111">环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常使用故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="79d90-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="79d90-112">由开发团队或自动由 Team Build 的服务器，可以手动部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d90-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="79d90-113">部署应用程序的进程帐户的用户不太可能的过渡服务器上具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="79d90-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="79d90-114">更改应用程序将部署频繁，因此环境必须支持单步或自动部署。</span><span class="sxs-lookup"><span data-stu-id="79d90-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="79d90-115">跨多个服务器横向扩展数据库部署不在本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="79d90-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="79d90-116">此区域的详细信息，请查阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="79d90-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="79d90-117">例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Foundation Server (TFS) 管理 Contact Manager 解决方案。</span><span class="sxs-lookup"><span data-stu-id="79d90-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="79d90-118">TFS 管理员，Rob Walters 创建了使开发人员能够触发部署到过渡环境所需的生成定义。</span><span class="sxs-lookup"><span data-stu-id="79d90-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="79d90-119">请注意，在大多数情况下，不一定要将最新版本部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="79d90-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="79d90-120">相反，您想要部署特定生成的验证和测试环境中的验证程序已进行了很多可能。</span><span class="sxs-lookup"><span data-stu-id="79d90-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="79d90-121">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="79d90-121">Solution Overview</span></span>

<span data-ttu-id="79d90-122">在此方案中，您可以推断出的部署要求分析从这些事实：</span><span class="sxs-lookup"><span data-stu-id="79d90-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="79d90-123">执行部署的用户或进程帐户不会在过渡服务器上具有管理员权限，因此临时 web 服务器必须支持非管理员部署。</span><span class="sxs-lookup"><span data-stu-id="79d90-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="79d90-124">在这种情况下，你将需要临时 web 服务器配置为使用 Web 部署处理程序而不是远程代理。</span><span class="sxs-lookup"><span data-stu-id="79d90-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="79d90-125">在过渡环境中包含多个 web 服务器，但它需要支持一次单击或自动部署，因此将需要使用 Web Farm Framework (WFF) 创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="79d90-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="79d90-126">使用此方法，可以部署一个 web server （主服务器） 的应用程序和 WFF 将复制在过渡环境中的所有其他 web 服务器上部署。</span><span class="sxs-lookup"><span data-stu-id="79d90-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="79d90-127">执行部署的进程帐户的用户必须有权创建数据库。</span><span class="sxs-lookup"><span data-stu-id="79d90-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="79d90-128">在这种情况下，你将需要将帐户添加到**dbcreator**上数据库服务器，除了配置数据库服务器以支持远程访问和部署服务器角色。</span><span class="sxs-lookup"><span data-stu-id="79d90-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="79d90-129">这些主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="79d90-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="79d90-130">[使用 Web Farm Framework 创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="79d90-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="79d90-131">本主题介绍如何创建和配置使用 WFF，服务器场，以使 web 平台产品和组件、 配置设置和网站和应用程序复制到多个负载平衡的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="79d90-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="79d90-132">[配置用于 Web 部署发布的 Web 服务器 （Web 部署处理程序）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="79d90-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="79d90-133">本主题介绍如何构建支持 Web 部署发布，使用远程代理方法中，从干净的 Windows Server 2008 R2 生成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="79d90-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="79d90-134">[配置数据库服务器，用于 Web 部署发布](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="79d90-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="79d90-135">本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。</span><span class="sxs-lookup"><span data-stu-id="79d90-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="79d90-136">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="79d90-136">Further Reading</span></span>

<span data-ttu-id="79d90-137">有关配置典型的开发人员的测试环境的指导，请参阅[方案： 配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="79d90-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="79d90-138">有关配置典型的生产环境的指导，请参阅[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="79d90-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="79d90-139">[上一页](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一页](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="79d90-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
