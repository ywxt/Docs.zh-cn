---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: 企业 Web 部署： 方案概述 |Microsoft Docs
author: jrjlee
description: 本教程系列与现实级别的复杂性，以及虚构企业部署方案中，使用示例解决方案提供 ref...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: ec5b62f3991fa256bc8efe7abe9b953d61d1a515
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824652"
---
<a name="enterprise-web-deployment-scenario-overview"></a>企业 Web 部署： 方案概述
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本系列教程使用示例解决方案使用真实的复杂性，虚构企业部署方案中，以及级别提供的参考实现，并为提供的任务和演练的通用上下文。 本主题介绍了教程方案，并引入了示例解决方案。


## <a name="scenario-description"></a>应用场景说明

Fabrikam，Inc.，虚构公司，创建一种解决方案，可让远程销售团队存储和检索的 web 界面的联系信息。

在 Fabrikam，Inc.的应用程序生命周期管理 (ALM) 进程需要的软件开发过程的各个阶段中要部署到三个服务器环境的解决方案：

- 开发人员测试或"沙盒"环境。
- 基于 intranet 的过渡环境中。
- 面向 Internet 的生产环境。

每个环境都有不同的配置和安全要求，以及每个又带来了独特的部署挑战。

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam，inc.服务器基础结构

这是 Fabrikam，Inc.高级开发和部署基础结构

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

开发人员工作站、 源控制基础结构、 开发人员测试环境中和所有位于 Fabrikam.net 域内的 intranet 网络的过渡环境。 在生产环境驻留在外围网络 （也称为 DMZ、 外围安全区域和外围子网），这是通过防火墙与 intranet 网络隔离。 这是一种常见部署方案： 你通常将面向 Internet 的 web 服务器隔离从内部服务器基础结构通过防火墙或网关服务器使用。

在此示例中：

- 具有单独的生成服务器的 Team Foundation Server (TFS) 2010年服务器提供源代码管理和持续集成 (CI) 功能。
- 开发人员测试环境包括 Internet Information Services (IIS) 7.5 web 服务器和 SQL Server 2008 R2 数据库服务器。
- 在生产环境包括多个 IIS 7.5 web 服务器通过 Web Farm Framework (WFF) 控制器服务器，以及 SQL Server 2008 R2 数据库服务器同步。 在实践中，数据库服务器可能使用群集或镜像以提高可伸缩性和可用性。
- 在过渡环境旨在尽可能接近地复制生产环境的配置。
- 防火墙和网络隔离策略不允许直接的自动化部署从 intranet 到外围网络。

每个环境的配置更详细地介绍第二个教程中，[用于 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。

### <a name="team-roles-for-alm"></a>ALM 的团队角色

这些是所涉及的用户创建、 管理、 生成和发布 Contact Manager 解决方案：

- Matt 婷是 Fabrikam，Inc.的 web 应用程序开发人员他是团队的通过使用 Visual Studio 2010 开发 Contact Manager 解决方案的一部分。 Matt 允许自身环境配置为满足其需求的开发人员测试环境中的服务器上具有完全管理员权限。 另外，他还有到他在其中存储 Contact Manager 解决方案的源代码的 Visual Studio 2010 的 TFS 实例的用户访问权限。
- Rob Walters 是 Fabrikam，Inc.开发团队的服务器管理员。 Rob TFS 服务器上具有管理访问权限，以便他可以配置 TFS 和 Team Build 的所有方面。 Rob 还具有管理访问权限的测试和过渡 web 服务器，并且在测试和过渡环境中的数据库服务器可作为数据库管理员 (DBA)。 Rob 具有 Team Build 服务器上配置 TFS 以执行这些任务：

    - 生成并运行单元测试应用程序，每当用户签入到 TFS 的文件。 这称为 CI。
    - 应用程序通过单元测试后自动部署到测试环境 Contact Manager 应用程序。 这包括在初始部署之后将数据库发布到在初始部署和对数据库的任何更新的测试服务器。
    - 联系人管理器应用程序部署到过渡环境中单步过程。
    - 创建 Web 服务器管理员和 DBA 可以使用应用程序发布到生产环境的 Web 包。
- Lisa Andrews 是服务器管理员，负责应用程序部署到 Fabrikam，Inc.生产服务器。 她具有读取访问权限的 TFS Team Build 存储的位置的 web 部署包后生成的联系人管理器应用程序的共享。 她还具有流向生产 web 服务器的管理访问权限，使她可以部署到生产环境的应用程序。 此外，她充当 DBA，他将数据库和数据库更新部署到生产环境中的数据库服务器。

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Contact Manager 解决方案

联系人管理器解决方案旨在让已注册、 登录的用户添加和编辑通过 web 界面的联系信息。 Contact Manager 解决方案包含四个单独项目：

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager.Mvc**。 这是表示解决方案的入口点的 ASP.NET MVC3 web 应用程序项目。 它提供了一些基本的 web 应用程序功能，如向用户提供的功能来创建和查看联系人详细信息。 应用程序依赖于用于管理联系人和 ASP.NET 应用程序服务数据库来管理身份验证和授权的 Windows Communication Foundation (WCF) 服务。
- **ContactManager.Database**。 这是 Visual Studio 2010 数据库项目。 项目定义存储联系人详细信息的数据库的架构。
- **ContactManager.Service**。 这是 WCF web 服务项目。 WCF 公开终结点，允许调用方执行创建、 检索、 更新和删除 (CRUD) 操作在联系人管理器数据库。 该服务依赖于联系人管理器数据库和 ContactManager.Common.dll 程序集。
- **ContactManager.Common**。 这是一个类库项目。 WCF 服务依赖于此程序集中定义的类型。

本系列中的第一个教程中提供了该解决方案，其部署要求的全面审查[企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>部署任务

有几个不同的任务涉及的应用程序部署到在大型组织中不同的环境。 这些是教程涵盖的关键任务：

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

下面是部署过程中从本文档前面所述的用户的角度来看，每个步骤的列表：

1. 所有团队成员都查看来确定关键部署要求和问题的 Visual Studio 2010 中的 Contact Manager 解决方案。
2. Matt 婷可以部署到开发人员测试环境，若要执行的部署逻辑初始测试 Contact Manager 解决方案直接从开发人员工作站。
3. Matt 婷在 TFS 中添加到源代码管理应用程序。
4. Rob Walters Team Build 中创建各种 Contact Manager 解决方案的生成定义。 一个生成定义使用 CI 解决方案部署到开发人员测试环境，只要用户签入新代码。 另一个生成定义允许到过渡环境所需的用户触发器部署。
5. 每次用户签入新代码，Team Build 自动生成的解决方案组件、 运行单元测试，并将解决方案部署到开发人员测试环境中，如果生成成功并且已通过单元测试。
6. 当用户触发部署到过渡环境时，该解决方案是打包和部署在单步过程。 此过程还会生成以手动部署到生产环境的包。
7. Lisa Andrews 手动导入在步骤 6 中创建的 web 包部署到生产环境的应用程序。

### <a name="key-deployment-issues"></a>关键的部署问题

Contact Manager 解决方案和 Fabrikam，Inc.方案重点介绍各种常见的问题和部署复杂的企业级解决方案时可能遇到的难题。 例如：

- 您需要能够将项目部署到多个环境，如开发人员或测试环境中，暂存平台和生产服务器。 该解决方案需要与每个环境的不同的配置设置一起部署。
- 您需要将单步执行或自动生成和部署过程的一部分同时部署多个依赖项目。
- 需要无法将驱动器部署从自动化过程。 例如，想要使用 CI 过程时签入新代码部署到过渡环境的 web 应用程序。
- 您需要能够控制部署过程并将部署变量设置从 Visual Studio 外部，如开发人员不太可能具有正确的配置设置或为每个目标环境所需的凭据。
- 您需要部署的基于架构的数据库项目并保留在后续部署上的现有数据。
- 您需要部署上临时成员资格数据库而不部署用户帐户数据。 您可能还需要更新已部署的成员资格数据库的架构，而不会丢失现有用户帐户数据。
- 需要时将内容部署到各种目标环境中排除某些文件或文件夹。

此外，管理部署频繁和增量更新时引发了一些其他挑战。 例如：

- 每次一名开发人员签入新代码运行单元测试。 你只想要部署解决方案，如果该代码将单元测试。
- 在部署到过渡或生产环境的 web 应用程序时，你想要将用户重定向*应用程序\_offline.htm*部署过程的持续时间的文件。
- 你想要记录部署活动。 部署过程应将成功或失败部署的电子邮件通知发送给指定收件人。
- 自动的部署失败时，部署过程应重试当前部署或改为部署以前的 web 包。

> [!div class="step-by-step"]
> [上一页](deploying-web-applications-in-enterprise-scenarios.md)
> [下一页](application-lifecycle-management-from-development-to-production.md)
