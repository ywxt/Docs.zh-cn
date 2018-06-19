---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 方案： 配置 Web 部署的测试环境 |Microsoft 文档
author: jrjlee
description: 本主题介绍典型 web 部署方案中的为开发人员或测试环境并说明需要为了设置 si 完成的任务...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2976be642815e715ac19bd9db34485cf5474cb32
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879850"
---
<a name="scenario-configuring-a-test-environment-for-web-deployment"></a><span data-ttu-id="928c9-103">方案： 配置 Web 部署的测试环境</span><span class="sxs-lookup"><span data-stu-id="928c9-103">Scenario: Configuring a Test Environment for Web Deployment</span></span>
====================
<span data-ttu-id="928c9-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="928c9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="928c9-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="928c9-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="928c9-106">本主题介绍典型 web 部署方案中的为开发人员或测试环境并说明需要为了设置相似的环境中完成的任务。</span><span class="sxs-lookup"><span data-stu-id="928c9-106">This topic describes a typical web deployment scenario for developer or test environments and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="928c9-107">当开发人员 web 应用程序时，它们通常将向它们可用于在实际设置中测试更改向其应用程序的服务器环境中获得访问。</span><span class="sxs-lookup"><span data-stu-id="928c9-107">When developers work on web applications, they're often given access to a server environment that they can use to test changes to their applications in a realistic setting.</span></span> <span data-ttu-id="928c9-108">这种类型的开发或测试环境通常具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="928c9-108">This kind of development or test environment typically has these characteristics:</span></span>

- <span data-ttu-id="928c9-109">环境由单个 web 服务器和单个数据库服务器组成。</span><span class="sxs-lookup"><span data-stu-id="928c9-109">The environment consists of a single web server and a single database server.</span></span>
- <span data-ttu-id="928c9-110">开发人员通常在服务器上，以允许这些配置环境到其应用程序的要求有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="928c9-110">The developers usually have administrator privileges on the servers, to let them configure the environment to the requirements of their applications.</span></span>
- <span data-ttu-id="928c9-111">更改应用程序将部署频繁，因此环境需要支持单步执行或自动部署。</span><span class="sxs-lookup"><span data-stu-id="928c9-111">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

<span data-ttu-id="928c9-112">例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Matt 婷是开发人员在 Fabrikam，inc.Matt 从事联系人管理器解决方案，并定期需要将更改部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="928c9-112">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink is a developer at Fabrikam, Inc. Matt is working on the Contact Manager solution and regularly needs to deploy changes to a test environment.</span></span> <span data-ttu-id="928c9-113">Matt 是测试 web 服务器和测试数据库服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="928c9-113">Matt is an administrator on the test web server and the test database server.</span></span> <span data-ttu-id="928c9-114">最初，Matt 需要能够直接将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="928c9-114">Initially, Matt needs to be able to deploy the solution to the test environment directly.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="928c9-115">与工作的进展和多个开发人员加入团队解决方案配置为连续集成 (CI) 在 Team Foundation Server (TFS) 联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="928c9-115">As work progresses and more developers join the team, the Contact Manager solution is configured for continuous integration (CI) in Team Foundation Server (TFS).</span></span> <span data-ttu-id="928c9-116">只要开发人员将签入内容，团队生成应生成解决方案，运行任何单元测试，并自动将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="928c9-116">Whenever a developer checks in content, Team Build should build the solution, run any unit tests, and automatically deploy the solution to the test environment.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a><span data-ttu-id="928c9-117">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="928c9-117">Solution Overview</span></span>

<span data-ttu-id="928c9-118">测试环境需要支持单步执行或自动部署从远程计算机，因此你可以选择的两种主要方法。</span><span class="sxs-lookup"><span data-stu-id="928c9-118">The test environment needs to support single-step or automated deployment from a remote computer, so you have a choice of two main approaches.</span></span> <span data-ttu-id="928c9-119">你可以：</span><span class="sxs-lookup"><span data-stu-id="928c9-119">You can:</span></span>

- <span data-ttu-id="928c9-120">配置测试 web 服务器以支持使用 Web 部署代理服务 （"远程代理"） 的部署。</span><span class="sxs-lookup"><span data-stu-id="928c9-120">Configure the test web server to support deployment using the Web Deployment Agent Service (the "remote agent").</span></span>
- <span data-ttu-id="928c9-121">配置测试 web 服务器以支持使用 Web 部署的处理程序的部署。</span><span class="sxs-lookup"><span data-stu-id="928c9-121">Configure the test web server to support deployment using the Web Deploy handler.</span></span>

> [!NOTE]
> <span data-ttu-id="928c9-122">你也可以使用[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx) （"临时代理"）。</span><span class="sxs-lookup"><span data-stu-id="928c9-122">You could also use [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx) (the "temp agent").</span></span> <span data-ttu-id="928c9-123">这是类似于在要求和约束方面的远程代理方法。</span><span class="sxs-lookup"><span data-stu-id="928c9-123">This is similar to the remote agent approach in terms of requirements and constraints.</span></span>


<span data-ttu-id="928c9-124">在这种情况下，开发人员在目标服务器上，具有管理员权限，并且测试环境不是受严格的安全约束，因此合理的选择是要配置测试 web 服务器以支持使用远程代理的部署。</span><span class="sxs-lookup"><span data-stu-id="928c9-124">In this case, the developers have administrator privileges on the destination servers, and the test environment is not subject to strict security constraints, so the logical choice is to configure the test web server to support deployment using the remote agent.</span></span> <span data-ttu-id="928c9-125">这是不太复杂，要求不太初始配置与 Web 部署处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="928c9-125">This is less complex and requires less initial configuration than the Web Deploy Handler approach.</span></span> <span data-ttu-id="928c9-126">你还需要配置你的数据库服务器来支持远程访问和部署。</span><span class="sxs-lookup"><span data-stu-id="928c9-126">You'll also need to configure your database server to support remote access and deployment.</span></span>

<span data-ttu-id="928c9-127">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="928c9-127">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="928c9-128">[配置 Web 服务器的 Web 部署发布 （远程代理）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="928c9-128">[Configure a Web Server for Web Deploy Publishing (Remote Agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span> <span data-ttu-id="928c9-129">本主题介绍如何生成支持 Web 部署发布，使用远程代理方法中，从干净的 Windows Server 2008 R2 生成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="928c9-129">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="928c9-130">[配置数据库服务器的 Web 部署发布更改](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="928c9-130">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="928c9-131">本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。</span><span class="sxs-lookup"><span data-stu-id="928c9-131">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="928c9-132">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="928c9-132">Further Reading</span></span>

<span data-ttu-id="928c9-133">有关配置的典型的过渡环境的指南，请参阅[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="928c9-133">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span> <span data-ttu-id="928c9-134">有关配置的典型生产环境的指南，请参阅[方案： 配置 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="928c9-134">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="928c9-135">[上一页](choosing-the-right-approach-to-web-deployment.md)
> [下一页](scenario-configuring-a-staging-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="928c9-135">[Previous](choosing-the-right-approach-to-web-deployment.md)
[Next](scenario-configuring-a-staging-environment-for-web-deployment.md)</span></span>
