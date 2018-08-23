---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 高级企业 Web 部署 |Microsoft Docs
author: jrjlee
description: 本教程将演示如何执行各种必需或在很多企业部署方案所需的任务。 对于意大利语 translati...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 34f1bf3bc2c37afc66f458a60a29fe5ce8f6c018
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833724"
---
<a name="advanced-enterprise-web-deployment"></a>高级的企业 Web 部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程将演示如何执行各种必需或在很多企业部署方案所需的任务。
> 
> 这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。


这就构成的系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求本系列教程将使用的示例解决方案&#x2014;[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="scenario-overview"></a>方案概述

这些教程中的高级方案所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。 我们建议在开始本教程为基础之前查看此主题。

## <a name="how-to-use-this-tutorial"></a>如何使用本教程

- 在本教程中的主题的每个是自包含，以及处理的特定挑战或企业部署方案中出现问题。 无需完成任何特定顺序中的以下主题。 但是，本教程介绍一些高级的任务。 在这种情况下，您应该熟悉的概念和技术的[企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)教程介绍如何才能获得此内容的最大效益。
- 本教程包括以下主题：
- [执行"假设"部署](performing-a-what-if-deployment.md)。 在很多情况下，您需要实际进行任何更改之前确定目标环境或任何现有内容建议的部署的影响。 本主题介绍如何运行"假设"部署以生成日志文件和数据库的更新脚本，相当有到目标环境中部署内容而不实际进行任何更改。 分析这些资源可以帮助您找出任何潜在问题之前实时部署。
- [自定义多个环境的数据库部署](customizing-database-deployments-for-multiple-environments.md)。 在数据库项目部署到多个目标时，通常需要自定义每个目标环境的部署属性。 例如，在测试环境中你将通常重新创建数据库上每个部署，而在过渡或生产环境中，您可能是一种更有可能进行增量更新，以保留您的数据。 本主题介绍如何才能将这些属性更改为你的部署逻辑通过创建用于每个目标环境的特定于环境的部署配置 (.sqldeployment) 文件。
- 部署到测试环境的数据库角色成员身份。 重新创建每个部署上的数据库&#x2014;例如，作为持续集成 (CI) 的一部分生成并部署到测试环境&#x2014;通常需要配置每个时间的数据库角色成员身份。 例如，您通常需要向与 web 应用程序关联的应用程序池标识授予权限。 本主题介绍如何通过将后期部署 SQL 脚本添加到你的部署逻辑自动执行此过程。
- [将成员资格数据库部署到企业环境](deploying-membership-databases-to-enterprise-environments.md)。 ASP.NET 成员资格数据库具有各种特征，可以使部署过程变得复杂。 例如，仅限架构的部署将使数据库处于不可操作状态的状态。 在大多数情况下，最好直接在每个目标环境中创建成员资格数据库。 但是，如果你确实必须将成员资格数据库部署，本主题介绍的一些方法可用于满足固有的挑战。
- [从部署中排除文件和文件夹](excluding-files-and-folders-from-deployment.md)。 在某些情况下，你将想要调整到特定的目标环境 web 程序包的内容。 例如，你可能想要部署到测试环境中，以支持客户端调试，但在部署到过渡或生产环境时使用缩小的版本的库时包括的 JavaScript 库的完整版本。 本主题介绍如何您可以排除特定文件和文件夹从包创建过程。
- [使 Web 应用程序脱机使用 Web 部署](taking-web-applications-offline-with-web-deploy.md)。 当你将解决方案部署到过渡或生产环境时，通常需要执行部署过程的持续时间内的 web 应用程序脱机。 本主题介绍如何将添加*应用程序\_offline.htm*对 web 应用程序在启动部署过程的文件，并在结束时将其删除。 虽然*应用程序\_offline.htm*文件的位置中，浏览到 web 应用程序的任何用户自动重定向到*应用\_offline.htm*文件。
- [运行 Windows PowerShell 脚本从 MSBuild](running-windows-powershell-scripts-from-msbuild-project-files.md)。 许多部署方案需要更复杂的部署后操作，如将自定义事件源添加到注册表或配置 SQL Server 实例之间进行复制。 这些操作通常通过 Windows PowerShell 脚本。 本主题介绍如何从 Microsoft Build Engine (MSBuild) 项目文件生成和部署过程的一部分运行的 Windows PowerShell 脚本。
- [打包过程故障排除](troubleshooting-the-packaging-process.md)。 Web 发布管道 (WPP) 定义一个名为 MSBuild 属性**EnablePackageProcessLoggingAndAssert**可用于生成 web 应用程序项目的打包过程有关的详细信息。 本主题介绍了该属性的用途以及如何使用它。

## <a name="key-technologies"></a>关键技术

本教程重点介绍如何使用这些产品和技术来支持自动化的生成和 web 部署：

- Visual Studio 2010 和 Team Foundation Server (TFS) 2010
- MSBuild 和 TFS Team Build
- Internet 信息服务 (IIS) 7.5
- IIS Web 部署工具 （Web 部署） 2.1
- VSDBCMD.exe 数据库部署实用工具

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这在企业级 web 部署窗体的一系列五个教程的一部分。 以下是该系列中的其他教程：

- [部署 Web 应用程序在企业方案中的](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容提供了为系列教程的上下文的背景。 它描述了教程的方案，并说明了任务和演练所述在整个系列如何适应更广泛的应用程序生命周期管理 (ALM) 过程。
- [Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程提供 MSBuild 项目文件的概念介绍、 WPP、 Web 部署，和其他相关的技术。 它介绍了如何使用这些工具一起管理复杂部署过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows 服务器以支持各种部署方案，包括使用 Web 部署代理服务 （远程代理） 或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 它提供有关选择适当的部署方法对您自己的环境的指导并介绍了如何使用 Web Farm Framework (WFF) 在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [配置用于 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持多种部署方案，包括作为 CI 过程的一部分的自动的部署和手动触发部署的特定版本。

> [!div class="step-by-step"]
> [下一篇](performing-a-what-if-deployment.md)
