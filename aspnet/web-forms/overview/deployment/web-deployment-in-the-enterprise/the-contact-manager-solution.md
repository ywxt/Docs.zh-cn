---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 本系列教程将使用的示例解决方案&#x2014;Contact Manager 解决方案&#x2014;来表示具有真实的更深层的企业级应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 8187766190da43ded52359892601f8129b9940ce
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388103"
---
<a name="the-contact-manager-solution"></a><span data-ttu-id="1ce83-103">Contact Manager 解决方案</span><span class="sxs-lookup"><span data-stu-id="1ce83-103">The Contact Manager Solution</span></span>
====================
<span data-ttu-id="1ce83-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="1ce83-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="1ce83-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="1ce83-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="1ce83-106">这[系列教程](web-deployment-in-the-enterprise.md)将使用的示例解决方案&#x2014;Contact Manager 解决方案&#x2014;来表示真实程度的企业级应用程序。</span><span class="sxs-lookup"><span data-stu-id="1ce83-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="1ce83-107">本主题介绍 Contact Manager 解决方案，介绍了该解决方案的关键组件，并标识部署此类企业环境中的各种目标平台的应用程序所面临的挑战。</span><span class="sxs-lookup"><span data-stu-id="1ce83-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="1ce83-108">在这些教程中处理整个主题，可以将 Contact Manager 解决方案用作演示了如何可以满足企业部署方案的特定需求的参考实现。</span><span class="sxs-lookup"><span data-stu-id="1ce83-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="1ce83-109">下一主题[设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)，介绍如何下载并在开发人员工作站上运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="1ce83-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>


## <a name="solution-overview"></a><span data-ttu-id="1ce83-110">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="1ce83-110">Solution Overview</span></span>

<span data-ttu-id="1ce83-111">Contact Manager 解决方案包含四个单独项目：</span><span class="sxs-lookup"><span data-stu-id="1ce83-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="1ce83-112">**ContactManager.Mvc**。</span><span class="sxs-lookup"><span data-stu-id="1ce83-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="1ce83-113">这是表示解决方案的入口点的 ASP.NET MVC 3 web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="1ce83-114">它提供了一些基本的 web 应用程序功能，如向用户提供的功能来创建和查看联系人详细信息。</span><span class="sxs-lookup"><span data-stu-id="1ce83-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="1ce83-115">应用程序依赖于用于管理联系人和 ASP.NET 应用程序服务数据库来管理身份验证和授权的 Windows Communication Foundation (WCF) 服务。</span><span class="sxs-lookup"><span data-stu-id="1ce83-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="1ce83-116">**ContactManager.Database**。</span><span class="sxs-lookup"><span data-stu-id="1ce83-116">**ContactManager.Database**.</span></span> <span data-ttu-id="1ce83-117">这是 Visual Studio 数据库项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="1ce83-118">项目定义存储联系人详细信息的数据库的架构。</span><span class="sxs-lookup"><span data-stu-id="1ce83-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="1ce83-119">**ContactManager.Service**。</span><span class="sxs-lookup"><span data-stu-id="1ce83-119">**ContactManager.Service**.</span></span> <span data-ttu-id="1ce83-120">这是 WCF web 服务项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-120">This is a WCF web service project.</span></span> <span data-ttu-id="1ce83-121">WCF 服务公开的终结点，允许调用方执行创建、 检索、 更新和删除 (CRUD) 操作上**ContactManager**数据库。</span><span class="sxs-lookup"><span data-stu-id="1ce83-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="1ce83-122">该服务依赖**ContactManager**数据库并**ContactManager.Common.dll**程序集。</span><span class="sxs-lookup"><span data-stu-id="1ce83-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="1ce83-123">**ContactManager.Common**。</span><span class="sxs-lookup"><span data-stu-id="1ce83-123">**ContactManager.Common**.</span></span> <span data-ttu-id="1ce83-124">这是一个类库项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-124">This is a class library project.</span></span> <span data-ttu-id="1ce83-125">WCF 服务依赖于此程序集中定义的类型。</span><span class="sxs-lookup"><span data-stu-id="1ce83-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="1ce83-126">该解决方案还包括一个名为发布的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="1ce83-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="1ce83-127">这包含各种自定义项目文件和演示如何控制和操作生成和部署过程的命令文件。</span><span class="sxs-lookup"><span data-stu-id="1ce83-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="1ce83-128">这些内容在本教程后面介绍更多详细信息中。</span><span class="sxs-lookup"><span data-stu-id="1ce83-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="1ce83-129">从概念上讲，解决方案的组件组合在一起如下：</span><span class="sxs-lookup"><span data-stu-id="1ce83-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="1ce83-130">ASP.NET MVC 3 web 应用程序使用 ASP.NET 成员资格提供程序，而 web 应用程序内的所有页面将都允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="1ce83-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="1ce83-131">这显然不是实际配置。</span><span class="sxs-lookup"><span data-stu-id="1ce83-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="1ce83-132">但是，该解决方案是设置以这种方式，以使你更轻松地部署和测试解决方案，而不配置用户帐户和角色。</span><span class="sxs-lookup"><span data-stu-id="1ce83-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>


## <a name="deployment-challenges"></a><span data-ttu-id="1ce83-133">部署难题</span><span class="sxs-lookup"><span data-stu-id="1ce83-133">Deployment Challenges</span></span>

<span data-ttu-id="1ce83-134">Contact Manager 解决方案演示了几个部署难题所共有的许多企业部署方案：</span><span class="sxs-lookup"><span data-stu-id="1ce83-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="1ce83-135">解决方案包含多个依赖项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="1ce83-136">需要同时部署这些项目。</span><span class="sxs-lookup"><span data-stu-id="1ce83-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="1ce83-137">需要为每个环境中，更新连接字符串和服务终结点并在许多情况下此信息将不能供开发人员。</span><span class="sxs-lookup"><span data-stu-id="1ce83-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="1ce83-138">当你部署**ContactManager**数据库需要以保留现有数据后续部署到过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="1ce83-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="1ce83-139">在部署 ASP.NET 应用程序服务数据库时，您需要部署某些配置数据，但省略任何用户帐户数据。</span><span class="sxs-lookup"><span data-stu-id="1ce83-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="1ce83-140">项目包含某些文件和不应部署的文件夹。</span><span class="sxs-lookup"><span data-stu-id="1ce83-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="1ce83-141">你需要在部署过程中排除这些文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="1ce83-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="1ce83-142">需求的解决方案，以支持来自 Team Foundation Server (TFS) 生成服务器的自动的部署。</span><span class="sxs-lookup"><span data-stu-id="1ce83-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1ce83-143">结束语</span><span class="sxs-lookup"><span data-stu-id="1ce83-143">Conclusion</span></span>

<span data-ttu-id="1ce83-144">本主题提供 Contact Manager 解决方案的概述以及一些固有的部署问题所共有的许多企业部署方案。</span><span class="sxs-lookup"><span data-stu-id="1ce83-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="1ce83-145">在本教程的其余主题介绍了一些可用来应对这些挑战的技术。</span><span class="sxs-lookup"><span data-stu-id="1ce83-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="1ce83-146">下一主题[设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)，介绍如何下载并在开发人员工作站上运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="1ce83-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ce83-147">[上一页](web-deployment-in-the-enterprise.md)
> [下一页](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="1ce83-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
