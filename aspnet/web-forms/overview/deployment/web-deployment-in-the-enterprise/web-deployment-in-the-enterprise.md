---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Web 部署在企业中的 |Microsoft Docs
author: jrjlee
description: 本教程介绍如何满足大量的管理的企业级 web 应用程序开发到部署时，将会遇到的挑战...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: 07c1ea9728c0130b860c0e0a64eb0751245ff840
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371137"
---
<a name="web-deployment-in-the-enterprise"></a>在企业中的 web 部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教程介绍如何满足大量管理企业级 web 应用程序部署到开发、 测试、 过渡和生产环境时，将会遇到的挑战。 本教程包括一个引用解决方案，以及各种概念和面向任务的内容，以获得指导您完成各种常见任务和过程。
> 
> 这些教程意大利语翻译，请访问[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。


## <a name="enterprise-deployment-challenges"></a>企业部署难题

它们看起来复杂，企业级解决方案的部署进行管理时，组织通常会遇到这些难题：

- 您需要能够将项目部署到多个环境，如开发人员或测试环境中，暂存平台和生产服务器。 该解决方案需要与每个环境的不同的配置设置一起部署。
- 您需要将单步执行或自动生成和部署过程的一部分同时部署多个依赖项目。
- 需要无法将驱动器部署从自动化过程。 例如，想要使用持续集成 (CI) 过程时签入新代码部署到测试环境的 web 应用程序。
- 您需要能够控制部署过程并将部署变量设置从 Visual Studio 外部，如开发人员不太可能具有正确的配置设置或为每个目标环境所需的凭据。
- 您需要部署的基于架构的数据库项目并保留在后续部署上的现有数据。
- 您需要部署上临时成员资格数据库而不部署用户帐户数据。 您可能还需要更新已部署的成员资格数据库的架构，而不会丢失现有用户帐户数据。
- 需要时将内容部署到各种目标环境中排除某些文件或文件夹。

## <a name="overview-of-approach"></a>方法的概述

本教程中的，以及其他教程在本系列中，使用此高级方法来满足上文所述的挑战。

- **使用自定义 Microsoft Build Engine (MSBuild) 项目文件来控制整个生成和部署过程。**
- 这样可以生成和部署解决方案中的每个项目作为一个可编写脚本的操作的一部分。
- 使用简单的特定于环境的项目文件配置特定于环境的设置。 与 Visual Studio 为中心的方式来使用解决方案配置和发布配置文件配置不同的环境的部署，此方法允许您配置和管理从 Visual Studio 外部的部署过程。 这意味着开发人员不需要丰富的连接字符串、 服务终结点、 服务器凭据和目标环境的其他部署变量的知识。
- 可以通过 Team Build 的 Team Foundation Server (TFS) 工作流调用自定义项目文件。 这允许你配置 CI 方案的自动的部署。

**使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 来打包和部署 web 应用程序项目。**

- Web 部署提供了一个框架，使您打包并部署到目标 IIS web 服务器，以及依赖项、 配置设置、 安全设置和任何其他要求你的 web 应用程序内容。
- 在自定义 MSBuild 项目文件中，可以控制从整个的打包和部署过程。 您还可以操作伴随 web 部署包，如连接字符串、 服务终结点和 IIS 目标详细信息的配置设置。
- Web 部署，以及 Web 发布管道，提供了大量扩展点允许你自定义你的部署。 例如，很容易从您的 web 部署包中排除不需要的文件和文件夹。

**使用 VSDBCMD.exe 实用程序来部署和更新数据库架构。**

- VSDBCMD 可以部署数据库架构文件 (.dbschema)，这在生成时生成 Visual Studio 数据库项目中的数据库。 与此相反，将现有数据库从本地 SQL Server 实例部署到 Web 部署中包含的数据库部署功能是更适合。
- 与用于部署数据库项目的 Visual Studio 的功能，不同 VSDBCMD 可让你将差异更新部署到现有目标数据库。 这样，你可以升级数据库架构时保留的任何现有数据。
- 您可以在自定义 MSBuild 项目文件内执行从 VSDBCMD 命令。

## <a name="content-map"></a>内容映射

本教程包括在此四个主要区域内的主题。

这些主题介绍参考解决方案&#x2014;Contact Manager 解决方案&#x2014;并且描述了如何下载它并将其配置在本地计算机上：

- [Contact Manager 解决方案](the-contact-manager-solution.md)
- [设置 Contact Manager 解决方案](setting-up-the-contact-manager-solution.md)

这些主题介绍 MSBuild 项目文件中，介绍如何创建和使用自定义项目文件，并演练部署过程中的 Contact Manager 解决方案：

- [了解项目文件](understanding-the-project-file.md)
- [了解生成过程](understanding-the-build-process.md)

这些主题介绍了 web 应用程序部署，包括如何生成和打包进程的工作原理、 如何与 Web 发布管道集成生成过程、 如何修改部署参数，以及如何将 web 包部署到目标环境：

- [生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)
- [为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)
- [部署 Web 程序包](deploying-web-packages.md)

- [部署数据库项目](deploying-database-projects.md)介绍可用来部署 Visual Studio 数据库项目，以及每种方法的优缺点的不同技术。 [创建和运行部署命令文件](creating-and-running-a-deployment-command-file.md)介绍如何创建一个简单的命令文件，它封装您部署的逻辑，可让你以单步进程形式部署复杂的解决方案。
- 最后，[手动安装 Web 程序包](manually-installing-web-packages.md)最后本教程介绍了您 web 程序包导入到 IIS。

## <a name="key-technologies"></a>关键技术

在本教程中的主题主要使用这些技术来管理生成和部署：

- Visual Studio 2010
- MSBuild
- IIS 7.5
- Web Deploy 2.0
- VSDBCMD.exe 数据库部署实用工具

## <a name="other-tutorials-in-this-series"></a>本系列中的其他教程

这在企业级 web 部署窗体的一系列五个教程的一部分。 以下是其他教程系列中：

- [部署 Web 应用程序在企业方案中的](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此介绍性内容提供了为系列教程的上下文的背景。 它描述了教程的方案，并说明了任务和演练所述在整个系列如何适应更广泛的应用程序生命周期管理 (ALM) 过程。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程介绍如何配置 Windows 服务器以支持各种部署方案，包括使用 Web 部署代理服务 （远程代理） 或 Web 部署处理程序和远程数据库部署的远程 web 包部署。 它提供有关选择适当的部署方法对您自己的环境的指导并介绍了如何使用 Web Farm Framework (WFF) 在服务器场中的所有 web 服务器之间复制已部署的 web 应用程序。
- [配置用于 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程介绍如何配置 TFS 以支持多种部署方案，包括作为 CI 过程的一部分的自动的部署和手动触发部署的特定版本。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程介绍如何完成各种更高级的部署任务，如自定义数据库部署为多个环境中，从部署中排除文件和文件夹和在部署过程中将 web 应用程序脱机.

> [!div class="step-by-step"]
> [下一篇](the-contact-manager-solution.md)
