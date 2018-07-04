---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: 部署在企业方案中使用的 Visual Studio 2010 的 Web 应用程序 |Microsoft Docs
author: jrjlee
description: 本教程系列介绍工具和技术可用于部署各种企业方案中的 web 应用程序。 其中介绍了如何以充分利用...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 8412000e150f59911bb38f0147b1a487bef60c18
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376833"
---
<a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>部署在企业方案中使用的 Visual Studio 2010 的 Web 应用程序
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程系列介绍工具和技术可用于部署各种企业方案中的 web 应用程序。 其中介绍了如何以最适合使用 Visual Studio 2010 中，Microsoft Build Engine (MSBuild)、 Internet 信息服务 (IIS) 7.5、 IIS Web 部署工具 （Web 部署）、 Web Farm Framework (WFF) 和到 VSDBCMD.exe 等的实用程序等技术简化和管理部署过程。 它包括概念概述和面向任务的指导，可帮助你：
> 
> - 查看并建立的企业级 web 应用程序的部署要求。
> - 配置以支持 web 部署的测试、 过渡和生产 web 服务器环境。
> - 配置 Team Foundation Server (TFS) 的持续集成 (CI) 进程，以支持自动化的 web 部署。
> - 部署到不同服务器环境使用不同的要求和限制的企业级 web 应用程序。
> - 将更改部署到不同的服务器环境中运行的 web 应用程序。
> 
> > [!NOTE]
> > 虽然这些教程介绍了 TFS 用作 CI 服务器，该指南可以轻松适应任何 CI 服务器。 不需要 TFS 能够理解并利用这些教程的详细的知识。
> 
> 
> 这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。


## <a name="about-the-authors"></a>关于作者

Jason Lee 是使用的主体技术专家[内容 Master](http://www.contentmaster.com/) ，他一直从事 Microsoft 产品和技术，尤其是 SharePoint 和 ASP.NET，担任多年。 Jason 拥有在计算博士，目前 MCPD 和 MCTS 认证。 您可以阅读 Jason 的技术博客[www.jrjlee.com](http://www.jrjlee.com/)。

Benjamin Curry 是使用的主体技术专家[内容 Master](http://www.contentmaster.com/)谁编写了白皮书、 SDK 文档、 PowerPoint 演示文稿和教师指导的在线培训课程期间他的职业生涯。 ASP.NET 文档团队的原始成员，他已从事 Microsoft web 技术的十多年。

## <a name="target-audience"></a>目标受众

本教程系列适用于 ASP.NET web 应用程序开发人员和解决方案架构师而言使用 Visual Studio 2010 创建企业级 web 应用程序。 若要从内容中获取最大的价值，应该可以熟练地使用 Visual Studio 2010，并使用与 TFS，意识的 Microsoft web 平台技术，例如 ASP.NET MVC 3、 Windows Communication Foundation (WCF)、 IIS、 SQL 以及基本的了解服务器和 Visual Studio 数据库项目。 但是，您不需要熟悉部署工具和技术或需要了解如何设置 CI 系统。

## <a name="requirements"></a>要求

若要按照演练和执行这些教程介绍的任务，你将需要在开发计算机上安装此软件：

- Visual Studio 2010 Premium 或 Ultimate Edition Service pack 1
- .NET framework 4.0
- .NET framework 3.5 Service Pack 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

若要执行在所有这些演练所述的部署步骤，将需要有权访问示例 Web 应用程序的部署环境。 为获得最佳结果，这些环境应反映组织的企业部署模式。 然后，可以修改以反映的部署环境和您自己的组织要求此文档中提供的演练。

## <a name="series-contents"></a>系列内容

此介绍性部分包含两个其他主题。 这些服务设计为遵循本教程提供一些更广泛的上下文：

- [企业 Web 部署： 方案概述](enterprise-web-deployment-scenario-overview.md)。 本主题介绍支持每个本系列教程的方案。 此方案侧重于一家虚构公司 Fabrikam，Inc.的命名方式开发的企业级 web 应用程序的应用程序生命周期管理 (ALM) 要求。
- [应用程序生命周期管理： 从开发到生产](application-lifecycle-management-from-development-to-production.md)。 本主题提供了高级别，端到端的部署过程概述。 它说明了 Fabrikam，Inc.如何移动企业规模 ASP.NET web 应用程序通过测试、 过渡和生产环境持续开发过程的一部分。

本系列包括四个教程集。 每个重点介绍 web 部署的不同方面：

- [Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程提供 MSBuild 项目文件的概念介绍，Web 发布管道、 Web 部署和其他相关的技术。 它介绍了如何使用这些工具一起管理复杂部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows 服务器以支持各种部署方案，包括使用 Web 部署代理服务 （"远程代理"） 或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 它提供有关选择适当的部署方法对您自己的环境的指导并介绍了如何使用 WFF 在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [配置用于 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持多种部署方案，包括作为 CI 过程的一部分的自动的部署和手动触发部署的特定版本。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境中，从部署中排除文件和文件夹和在部署过程中将 web 应用程序脱机.

## <a name="where-to-start"></a>从何处着手

本系列教程使用示例解决方案使用真实的复杂性，虚构企业部署方案中，以及级别提供的参考实现，并为提供的任务和演练的通用上下文。 下一主题[企业 Web 部署： 方案概述](enterprise-web-deployment-scenario-overview.md)，引入了方案和示例解决方案。 从此处，可通过教程和主题的最接近你的需求。

> [!div class="step-by-step"]
> [下一篇](enterprise-web-deployment-scenario-overview.md)
