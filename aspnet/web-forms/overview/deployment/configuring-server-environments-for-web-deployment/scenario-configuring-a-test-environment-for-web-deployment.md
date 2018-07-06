---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 方案： 配置用于 Web 部署测试环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍典型的 web 部署方案中为开发人员或测试环境并说明为了设置 si 完成所需的任务...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: ba77c944378245ed82d1cee92b668e31acc51a81
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822365"
---
<a name="scenario-configuring-a-test-environment-for-web-deployment"></a>方案： 配置用于 Web 部署测试环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍典型的 web 部署方案中为开发人员或测试环境并说明完成若要设置类似的环境所需的任务。


当开发人员的 web 应用程序时，它们通常是到它们可用于在现实设置中测试对其应用程序的更改的服务器环境中授予访问权限。 这种类型的开发或测试环境通常具有以下特征：

- 环境由单个 web 服务器和单个数据库服务器组成。
- 开发人员通常在服务器上，以允许用户配置其应用程序的要求环境中具有管理员权限。
- 更改应用程序将部署频繁，因此环境必须支持单步或自动部署。

例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Matt 婷是 Fabrikam，Inc.的开发人员Matt 致力于 Contact Manager 解决方案，并经常需要更改部署到测试环境。 Matt 是测试 web 服务器和测试数据库服务器上的管理员。 最初，Matt 需要能够将解决方案直接部署到测试环境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

作为工作进度以及更多开发人员加入团队，解决方案配置持续集成 (CI) Team Foundation Server (TFS) 中的联系人管理器。 只要开发人员签入内容，Team Build 应生成解决方案、 运行任何单元测试和自动将解决方案部署到测试环境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>解决方案概述

在测试环境需要支持单步执行或自动化从远程计算机的部署，因此，您可以选择两种主要方法。 你可以：

- 测试 web 服务器以支持使用 Web 部署代理服务 （"远程代理"） 的部署配置。
- 测试 web 服务器以支持使用 Web 部署处理程序的部署配置。

> [!NOTE]
> 您还可以使用[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx) （"临时代理"）。 这是类似于要求和约束方面的远程代理方法。


在这种情况下，开发人员在目标服务器上具有管理员权限，测试环境无需遵守严格的安全约束，因此，逻辑的选择是将测试 web 服务器配置为支持使用远程代理的部署。 这是不太复杂，需要比 Web 部署处理程序方法不太初始配置。 此外需要配置你的数据库服务器以支持远程访问和部署。

这些主题提供完成这些任务所需的所有信息：

- [配置 Web 服务器，用于 Web 部署发布 （远程代理）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。 本主题介绍如何构建支持 Web 部署发布，使用远程代理方法中，从干净的 Windows Server 2008 R2 生成的 web 服务器。
- [配置数据库服务器，用于 Web 部署发布](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。

## <a name="further-reading"></a>其他阅读材料

有关配置典型的过渡环境的指导，请参阅[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。 有关配置典型的生产环境的指导，请参阅[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](choosing-the-right-approach-to-web-deployment.md)
> [下一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
