---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 配置用于 Web 部署的 Team Foundation Server |Microsoft Docs
author: jrjlee
description: 本教程将演示如何配置 Team Foundation Server (TFS) 2010年构建解决方案并将 web 内容部署到各种目标环境。 这...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 0155f8dc4ca05a91ed8921f83aa6fa1b0b59c1a5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829682"
---
<a name="configuring-team-foundation-server-for-web-deployment"></a>Team Foundation Server 配置用于 Web 部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将演示如何配置 Team Foundation Server (TFS) 2010年构建解决方案并将 web 内容部署到各种目标环境。 这包括持续集成 (CI) 方案，在其中部署内容自动每次一名开发人员进行了更改。 它还可以包含手动触发器方案中，管理员可能想要触发部署到过渡环境的特定生成，一旦经过验证并验证在测试环境中生成。 在本教程中的主题将指导您完成整个配置过程中，包括：
> 
> - 如何在 TFS 中创建新的团队项目。
> - 如何将内容添加到源代码管理。
> - 如何配置生成服务器以支持 CI 和部署。
> - 如何创建生成定义，包括部署逻辑。
> - 如何配置用于自动部署的权限。
> 
> 这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。


本教程假定已安装 TFS 2010 并创建初始配置过程的一部分的团队项目集合。 [Visual Studio 2010 的 Team Foundation 安装指南 》](https://go.microsoft.com/?linkid=9805132)这些任务提供全面的指导。

## <a name="context"></a>上下文

这就构成的系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求本系列教程将使用的示例解决方案&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="scenario-overview"></a>方案概述

这些教程中的高级方案所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。 我们建议在开始本教程为基础之前查看此主题。

## <a name="how-to-use-this-tutorial"></a>如何使用本教程

如果这是首次执行了本教程中所述的任务或如果你想要按照使用示例解决方案的示例，您应解决顺序中的教程主题。 或者，可以使用单个主题作为指南针对特定任务。 本教程包括以下主题：

- [在 TFS 中创建团队项目](creating-a-team-project-in-tfs.md)。 团队项目是源代码管理、 流程管理和生成在 TFS 中的核心单元。 您需要创建团队项目，然后才能添加源代码管理或创建生成定义的内容。
- [将内容添加到源代码管理](adding-content-to-source-control.md)。 一旦创建团队项目后，即可将内容添加到源代码管理。 你将需要添加的项目和解决方案，以及所有外部依赖项，然后才能开始配置生成。
- [配置 TFS 用于 Web 部署生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)。 如果你想要生成你的团队项目内容，您将需要配置生成服务器。 在大多数情况下，这应该是从 TFS 安装一台计算机上。 若要配置生成服务器，你需要安装和配置 TFS 生成服务，安装 Visual Studio 2010 中，创建生成控制器和生成代理，安装任何产品或你的代码为成功，生成并安装所需的组件Internet 信息服务 (IIS) Web 部署工具 （Web 部署）。
- [创建生成定义支持部署](creating-a-build-definition-that-supports-deployment.md)。 队列或触发在 TFS 中的生成开始之前，需要为你的团队项目创建至少一个生成定义。 生成定义用于定义该生成，包括应生成中包含哪些内容、 应触发生成，并在其中 Team Build 应发送生成输出的每个方面。 你可以配置生成定义以运行自定义 Microsoft Build Engine (MSBuild) 项目文件，从而允许您自动生成中包括部署逻辑。
- [部署特定生成](deploying-a-specific-build.md)。 在很多情况下，你将想要将特定生成的而不是最新版本部署到目标环境。 在这种情况下，你可以配置将从特定的放置文件夹的内容部署的生成定义。
- [配置权限的团队生成部署](configuring-permissions-for-team-build-deployment.md)。 如果生成服务是自动的生成过程的一部分部署的内容，您需要授予给任何目标 web 服务器和数据库服务器上的生成服务帐户的各种权限。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持自动化的生成和 web 部署：

- Visual Studio Team Foundation Server 2010
- 团队生成和 MSBuild
- Web Deploy

本教程，也提及的 Windows Server 2008 R2、 IIS 7.5、 SQL Server 2008 R2 中，ASP.NET 4.0 和 ASP.NET MVC 3 使用。

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这在企业级 web 部署窗体的一系列五个教程的一部分。 以下是其他教程系列中：

- [部署 Web 应用程序在企业方案中的](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容提供了为系列教程的上下文的背景。 它描述了教程的方案，并说明了任务和演练所述在整个系列如何适应更广泛的应用程序生命周期管理 (ALM) 过程。
- [Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程提供 MSBuild 项目文件的概念介绍，Web 发布管道 (WPP)、 Web 部署和其他相关的技术。 它介绍了如何使用这些工具一起管理复杂部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows 服务器以支持各种部署方案，包括使用 Web 部署代理服务 （远程代理） 或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 它提供有关选择适当的部署方法对您自己的环境的指导并介绍了如何使用 Web Farm Framework (WFF) 在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境中，从部署中排除文件和文件夹和在部署过程中将 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一篇](creating-a-team-project-in-tfs.md)
