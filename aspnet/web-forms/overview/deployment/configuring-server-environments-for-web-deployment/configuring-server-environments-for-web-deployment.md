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
<a name="configuring-server-environments-for-web-deployment"></a>配置用于 Web 部署的服务器环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将演示如何设置支持一次单击，或自动、 网站部署和发布各种不同方案中的服务器环境。 本教程包括主题向您逐步完成各种任务，如配置 web 服务器以支持部署和设置 Web Farm Framework (WFF) 服务器场中，提供的基于方案的概述以及特定方法更高级别的的端到端指南。
> 
> 本教程使用 Fabrikam，Inc.部署方案中所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)有关示例和网络基础结构的参考点。
> 
> 这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。


本教程包括以下主题：

- [选择 Web 部署的适当方法](choosing-the-right-approach-to-web-deployment.md)
- [方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)
- [方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)
- [配置用于 Web 部署发布的 Web 服务器（远程代理）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [配置用于 Web 部署发布的 Web 服务器（离线部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [配置用于 Web 部署发布的数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)
- [使用 Web Farm Framework 创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)
- [配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)

第一个主题[选择右方法对 Web 部署](choosing-the-right-approach-to-web-deployment.md)，介绍主要方法可用于发布 web 应用程序通过使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0。 它还标识将映射到每种方法的方案。 从此处，每个方案主题提供所需完成的任务的高级概述，并标识你将需要通过工作，以帮助您完成这些任务的主题。

如果您正使用拆分项目文件方法中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)生成和部署你的解决方案，最后一个主题，[为目标环境配置部署属性](configuring-deployment-properties-for-a-target-environment.md)，介绍如何配置部署到不同目标环境的特定于环境的项目文件。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持 web 部署：

- IIS 7.5
- Web 部署 2.x
- WFF 2.x
- IIS Web 管理服务 (WMSvc)

本教程还涉及使用 Windows Server 2008 R2、 SQL Server 2008 R2、 ASP.NET 4.0 中，和 ASP.NET MVC 3。

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这在企业级 web 部署窗体的一系列五个教程的一部分。 以下是其他教程系列中：

- [部署 Web 应用程序在企业方案中的](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容提供了为系列教程的上下文的背景。 它描述了教程的方案，并说明了任务和演练所述在整个系列如何适应更广泛的应用程序生命周期管理 (ALM) 过程。
- [Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程提供了 Microsoft Build Engine (MSBuild) 项目文件的概念介绍，Web 发布管道、 Web 部署和其他相关的技术。 它介绍了如何使用这些工具一起管理复杂部署过程。
- [配置用于 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 Team Foundation Server (TFS) 以支持多种部署方案，包括持续集成 (CI) 过程的一部分的自动的部署和手动触发部署的特定版本。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境中，从部署中排除文件和文件夹和在部署过程中将 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一篇](choosing-the-right-approach-to-web-deployment.md)
