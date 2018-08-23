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
<a name="scenario-configuring-a-production-environment-for-web-deployment"></a>方案： 配置用于 Web 部署的生产环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍适用于生产环境的典型的 web 部署方案，并说明完成若要设置类似的环境所需的任务。


在生产环境是 web 应用程序或网站的最终目标。 此时，你的应用程序将已通过测试，已部署到过渡环境，并已准备好"go live。" 生产环境中的特征可能会因广泛的性质和用途的 web 内容、 组织、 目标受众和很多其他因素的大小。 在企业级方案中，在生产环境可能具有以下特征：

- 环境包含多个负载平衡的 web 服务器和一个或多个数据库服务器，通常使用故障转移群集和数据库镜像。
- 如果环境是面向 Internet 的很可能从内部网络隔离。 不同的子网外围网络中可能会、 在不同域中，可能会和它可能是完全不同的网络基础结构上。
- 开发人员和生成服务器进程帐户是高度不大可能在生产服务器上具有管理员权限。
- 更改应用程序比测试或过渡部署不太频繁地部署。

> [!NOTE]
> 跨多个服务器横向扩展数据库部署不在本教程的范围。 此区域的详细信息，请查阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。


例如，在我们[教程的情况下](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Build 服务器包括让用户构建 Contact Manager 解决方案，并将其部署到过渡环境中单个步骤的生成定义。 准备好部署到生产环境中，由于施加的安全要求和网络基础结构，限制应用程序时必须手动复制到生产 web 服务器上的 web 包并导入生产环境管理员它通过 Internet 信息服务 (IIS) 管理器。

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>解决方案概述

在此方案中，您可以推断出的部署要求分析从这些事实：

- 由于安全限制和网络配置，不能配置为支持一次单击或自动部署在生产环境。 离线部署是在此方案中唯一的可行的方法。
- 在生产环境包括多个 web 服务器，因此可以使用 Web Farm Framework (WFF) 来创建服务器场。 使用此方法，管理员只需导入应用程序部署到一个 web 服务器 （主服务器），并在 WFF 复制生产环境中的所有其他 web 服务器上部署。

这些主题提供完成这些任务所需的所有信息：

- [使用 Web Farm Framework 创建服务器场](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何创建和配置使用 WFF，服务器场，以使 web 平台产品和组件、 配置设置和网站和应用程序复制到多个负载平衡的 web 服务器。
- [配置 Web 服务器，用于 Web 部署发布 （离线部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 本主题介绍如何构建可让管理员导入和部署 web 包手动从干净的 Windows Server 2008 R2 生成的 web 服务器。
- [配置数据库服务器，用于 Web 部署发布](configuring-a-database-server-for-web-deploy-publishing.md)。 本主题介绍如何配置数据库服务器以支持远程访问和部署，从 SQL Server 2008 R2 的默认安装。

## <a name="further-reading"></a>其他阅读材料

有关配置典型的开发人员的测试环境的指导，请参阅[方案： 配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。 有关配置典型的过渡环境的指导，请参阅[方案： 配置用于 Web 部署的暂存环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
