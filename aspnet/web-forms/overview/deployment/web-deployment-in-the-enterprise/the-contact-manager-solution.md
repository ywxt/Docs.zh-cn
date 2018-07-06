---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 本系列教程将使用的示例解决方案&#x2014;Contact Manager 解决方案&#x2014;来表示具有真实的更深层的企业级应用程序...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: c8044c37738e9d23ca83648a6b571059338dc1a3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835154"
---
<a name="the-contact-manager-solution"></a>Contact Manager 解决方案
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 这[系列教程](web-deployment-in-the-enterprise.md)将使用的示例解决方案&#x2014;Contact Manager 解决方案&#x2014;来表示真实程度的企业级应用程序。 本主题介绍 Contact Manager 解决方案，介绍了该解决方案的关键组件，并标识部署此类企业环境中的各种目标平台的应用程序所面临的挑战。
> 
> 在这些教程中处理整个主题，可以将 Contact Manager 解决方案用作演示了如何可以满足企业部署方案的特定需求的参考实现。 下一主题[设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)，介绍如何下载并在开发人员工作站上运行该解决方案。


## <a name="solution-overview"></a>解决方案概述

Contact Manager 解决方案包含四个单独项目：

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager.Mvc**。 这是表示解决方案的入口点的 ASP.NET MVC 3 web 应用程序项目。 它提供了一些基本的 web 应用程序功能，如向用户提供的功能来创建和查看联系人详细信息。 应用程序依赖于用于管理联系人和 ASP.NET 应用程序服务数据库来管理身份验证和授权的 Windows Communication Foundation (WCF) 服务。
- **ContactManager.Database**。 这是 Visual Studio 数据库项目。 项目定义存储联系人详细信息的数据库的架构。
- **ContactManager.Service**。 这是 WCF web 服务项目。 WCF 服务公开的终结点，允许调用方执行创建、 检索、 更新和删除 (CRUD) 操作上**ContactManager**数据库。 该服务依赖**ContactManager**数据库并**ContactManager.Common.dll**程序集。
- **ContactManager.Common**。 这是一个类库项目。 WCF 服务依赖于此程序集中定义的类型。

该解决方案还包括一个名为发布的解决方案文件夹。 这包含各种自定义项目文件和演示如何控制和操作生成和部署过程的命令文件。 这些内容在本教程后面介绍更多详细信息中。

从概念上讲，解决方案的组件组合在一起如下：

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET MVC 3 web 应用程序使用 ASP.NET 成员资格提供程序，而 web 应用程序内的所有页面将都允许匿名访问。 这显然不是实际配置。 但是，该解决方案是设置以这种方式，以使你更轻松地部署和测试解决方案，而不配置用户帐户和角色。


## <a name="deployment-challenges"></a>部署难题

Contact Manager 解决方案演示了几个部署难题所共有的许多企业部署方案：

- 解决方案包含多个依赖项目。 需要同时部署这些项目。
- 需要为每个环境中，更新连接字符串和服务终结点并在许多情况下此信息将不能供开发人员。
- 当你部署**ContactManager**数据库需要以保留现有数据后续部署到过渡和生产环境。
- 在部署 ASP.NET 应用程序服务数据库时，您需要部署某些配置数据，但省略任何用户帐户数据。
- 项目包含某些文件和不应部署的文件夹。 你需要在部署过程中排除这些文件和文件夹。
- 需求的解决方案，以支持来自 Team Foundation Server (TFS) 生成服务器的自动的部署。

## <a name="conclusion"></a>结束语

本主题提供 Contact Manager 解决方案的概述以及一些固有的部署问题所共有的许多企业部署方案。 在本教程的其余主题介绍了一些可用来应对这些挑战的技术。

下一主题[设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)，介绍如何下载并在开发人员工作站上运行该解决方案。

> [!div class="step-by-step"]
> [上一页](web-deployment-in-the-enterprise.md)
> [下一页](setting-up-the-contact-manager-solution.md)
