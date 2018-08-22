---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 方案： 配置用于 Web 部署的过渡环境 |Microsoft Docs
author: jrjlee
description: 本主题描述过渡环境的典型的 web 部署方案，并说明才能设置类似 env 完成所需的任务...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bee856c2ece6fda90ec35a87d111715def990603
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830894"
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>方案： 配置用于 Web 部署的过渡环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍过渡环境的典型的 web 部署方案，并说明所需设置类似的环境才能完成的任务。


许多组织使用过渡环境来预览对 web 应用程序或网站的更新。 这使组织内的人有机会浏览和之前的站点"会运行，"，或换句话说部署到生产环境，请查看新功能或内容。 在过渡环境旨在尽可能真实地复制生产环境，以便提供真实的预览。 这种过渡环境通常具有以下特征：

- 环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常使用故障转移群集和数据库镜像。
- 由开发团队或自动由 Team Build 的服务器，可以手动部署应用程序。
- 部署应用程序的进程帐户的用户不太可能的过渡服务器上具有管理员权限。
- 更改应用程序将部署频繁，因此环境必须支持单步或自动部署。

> [!NOTE]
> 跨多个服务器横向扩展数据库部署不在本教程的范围。 此区域的详细信息，请查阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。


例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Foundation Server (TFS) 管理 Contact Manager 解决方案。 TFS 管理员，Rob Walters 创建了使开发人员能够触发部署到过渡环境所需的生成定义。

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

请注意，在大多数情况下，不一定要将最新版本部署到过渡环境。 相反，您想要部署特定生成的验证和测试环境中的验证程序已进行了很多可能。

## <a name="solution-overview"></a>解决方案概述

在此方案中，您可以推断出的部署要求分析从这些事实：

- 执行部署的用户或进程帐户不会在过渡服务器上具有管理员权限，因此临时 web 服务器必须支持非管理员部署。 在这种情况下，你将需要临时 web 服务器配置为使用 Web 部署处理程序而不是远程代理。
- 在过渡环境中包含多个 web 服务器，但它需要支持一次单击或自动部署，因此将需要使用 Web Farm Framework (WFF) 创建服务器场。 使用此方法，可以部署一个 web server （主服务器） 的应用程序和 WFF 将复制在过渡环境中的所有其他 web 服务器上部署。
- 执行部署的进程帐户的用户必须有权创建数据库。 在这种情况下，你将需要将帐户添加到**dbcreator**上数据库服务器，除了配置数据库服务器以支持远程访问和部署服务器角色。

这些主题提供完成这些任务所需的所有信息：

- [使用 Web Farm Framework 创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)。 本主题介绍如何创建和配置使用 WFF，服务器场，以使 web 平台产品和组件、 配置设置和网站和应用程序复制到多个负载平衡的 web 服务器。
- [配置用于 Web 部署发布的 Web 服务器 （Web 部署处理程序）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 本主题介绍如何构建支持 Web 部署发布，使用远程代理方法中，从干净的 Windows Server 2008 R2 生成的 web 服务器。
- [配置数据库服务器，用于 Web 部署发布](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。

## <a name="further-reading"></a>其他阅读材料

有关配置典型的开发人员的测试环境的指导，请参阅[方案： 配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。 有关配置典型的生产环境的指导，请参阅[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一页](scenario-configuring-a-production-environment-for-web-deployment.md)
