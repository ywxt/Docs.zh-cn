---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 应用程序生命周期管理： 从开发到生产环境 |Microsoft Docs
author: jrjlee
description: 本主题说明了一个虚构的公司如何管理作为 par 通过测试、 过渡和生产环境将 ASP.NET web 应用程序部署...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 47af9504bdef294b987cdd23ab1bcefbeadd4681
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808974"
---
<a name="application-lifecycle-management-from-development-to-production"></a>应用程序生命周期管理： 从开发到生产环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题说明了一个虚构的公司管理的持续开发过程的一部分通过测试、 过渡和生产环境的 ASP.NET web 应用程序部署的方式。 在主题中，提供指向详细信息和有关如何执行特定任务的演练的链接。
> 
> 本主题旨在提供的高级概述[系列教程](deploying-web-applications-in-enterprise-scenarios.md)在企业中的 web 部署。 如果您不熟悉一些此处所述的概念，不用担心&#x2014;按照这些教程提供有关的所有这些任务和技术的详细的信息。
> 
> > [!NOTE]
> > 为了简单起见为起见，本主题不讨论更新数据库，作为部署过程的一部分。 但是，对数据库功能进行增量更新，是许多企业部署方案的要求和有关如何实现这一点稍后在本教程系列中的指南。 有关详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。


## <a name="overview"></a>概述

如下图所示的部署过程基于 Fabrikam，Inc.部署方案中所述[企业 Web 部署： 方案概述](enterprise-web-deployment-scenario-overview.md)。 在研究本主题前，应阅读方案概述。 从根本上来说，该方案会检查组织如何管理部署相当复杂的 web 应用程序， [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)，通过在典型的企业环境中的各个阶段。

在高级别 Contact Manager 解决方案将经历这些阶段作为开发和部署过程的一部分：

1. 开发人员检查一些代码到 Team Foundation Server (TFS) 2010年。
2. TFS 生成代码并运行任何团队项目相关联的单元测试。
3. TFS 将解决方案部署到测试环境。
4. 开发人员团队进行验证并对测试环境中的解决方案。
5. 过渡环境管理员执行"假设"部署到过渡环境中，若要建立部署是否会导致任何问题。
6. 过渡环境管理员执行实时部署到过渡环境。
7. 该解决方案将进行用户验收测试过渡环境中。
8. Web 部署包将手动导入到生产环境。

这些阶段构成连续开发周期的一部分。

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

在实践中，过程是能力，稍微复杂一些，正如您将看到当我们查看更多详细信息的每个阶段。 Fabrikam，Inc.的每个目标环境中使用部署到不同的方法。

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

本主题的其余部分检查此部署生命周期的这些关键阶段：

- **先决条件**： 需要先配置服务器基础结构，然后将你的部署逻辑放在位置。
- **初始开发和部署**： 需要在您首次部署解决方案之前执行操作。
- **部署以供测试**： 如何打包并将内容部署到测试环境自动开发人员签入新代码时。
- **部署到过渡环境**： 如何部署特定版本到过渡环境以及如何执行"假设"部署，以确保部署不会导致任何问题。
- **部署到生产环境**： 如何将 web 程序包导入生产环境时的网络基础结构将阻止远程部署。

## <a name="prerequisites"></a>系统必备

在任何部署方案中的第一个任务是确保服务器基础结构满足你的部署工具和技术的要求。 在这种情况下，Fabrikam，Inc.已配置其服务器基础结构如下：

- TFS 配置为包括团队项目集合、 生成控制器和生成代理。 请参阅[用于自动执行 Web 部署配置 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)有关详细信息。
- 在测试环境配置为接受远程部署使用 Web 部署代理服务 （"远程代理"），如中所述[方案： 配置用于 Web 部署的测试环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md)和[配置 Web 服务器，用于 Web 部署发布 （远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。
- 在过渡环境配置为接受远程部署使用 Web 部署处理程序终结点，如中所述[方案： 配置用于 Web 部署的暂存环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md)和[配置 Web 服务器对于 Web 部署发布 （Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。
- 在生产环境配置为允许管理员手动导入 web 部署包到 Internet 信息服务 (IIS) 中所述[方案： 配置用于 Web 部署生产环境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md)并[用于 Web 部署发布 （离线部署） 配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。

## <a name="initial-development-and-deployment"></a>初始开发和部署

Fabrikam，Inc.开发团队可以将 Contact Manager 解决方案部署第一次之前，需要执行这些任务：

- 在 TFS 中创建新的团队项目。
- 创建的 Microsoft Build Engine (MSBuild) 项目文件包含部署逻辑。
- 创建触发的部署过程的 TFS 生成定义。

### <a name="create-a-new-team-project"></a>创建新的团队项目

- TFS 管理员，Rob Walters 创建新的团队项目的应用程序，如中所述[在 TFS 中创建团队项目](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)。 接下来，首席开发人员，Matt 婷，创建一个主干解决方案。 他在 TFS 中，新的团队项目检查他的文件，如中所述[内容添加到源代码管理](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)。

### <a name="create-the-deployment-logic"></a>创建部署逻辑

Matt 婷创建各种自定义 MSBuild 项目文件，其中使用拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 Matt 创建：

- 名为的项目文件*Publish.proj*运行部署过程。 此文件包含 MSBuild 目标，生成解决方案中的项目创建 web 包，并将包部署到目标服务器环境。
- 名为的特定于环境的项目文件*Env Dev.proj*并*Env Stage.proj*。 它们包含连接字符串、 服务终结点和将会收到 web 包的远程服务的详细信息等分别是特定于测试环境和过渡环境的设置。 有关选择特定的目标环境的正确设置的指导，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

若要运行部署，用户在执行*Publish.proj*文件中使用 MSBuild 或 Team Build 并指定相关的特定于环境的项目文件的位置 (*Env Dev.proj*或*Env Stage.proj*) 作为命令行参数。 *Publish.proj*文件然后导入特定于环境的项目文件以创建一组完整的发布有关每个目标环境的说明。

> [!NOTE]
> 这些自定义项目文件的工作的方式是机制的独立于用于调用 MSBuild。 例如，您可以使用 MSBuild 命令行直接，如中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 你可以从命令文件，运行项目文件，如中所述[创建并运行部署命令文件](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)。 或者，从生成定义在 TFS 中，运行项目文件，如中所述[创建该支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。  
> 在每种情况下，最终结果是相同&#x2014;MSBuild 执行合并的项目文件并将你的解决方案部署到目标环境。 这可带来大量的如何触发发布过程的灵活性。


后他创建了自定义项目文件，Matt 将它们添加到解决方案文件夹，并将其签入源代码管理。

### <a name="create-build-definitions"></a>创建生成定义

作为最后一个准备任务，Matt 和 Rob 协同工作，创建三个新的团队项目的生成定义：

- **DeployToTest**。 这将生成 Contact Manager 解决方案并将其部署到测试环境中，每次签入发生时。
- **DeployToStaging**。 开发人员生成排队时，这将部署到过渡环境中指定的上一个生成的资源。
- **DeployToStaging-WhatIf**。 开发人员生成排队时，这会执行"假设"部署到过渡环境。

以下各节提供更多详细信息，每个选项的生成定义。

## <a name="deployment-to-test"></a>部署到测试

在 Fabrikam，Inc.的开发团队维护的测试环境以执行各种测试活动，如验证和验证、 可用性测试、 兼容性测试和 ad hoc 或探索测试的软件。

开发团队在名为 TFS 中创建生成定义**DeployToTest**。 此生成定义使用持续集成触发器，这意味着每次签入 Fabrikam，Inc.开发团队的成员执行时，在运行生成过程。 触发生成后，将生成定义：

- 生成 ContactManager.sln 解决方案。 这反过来会生成解决方案中的每个项目。
- 在解决方案文件夹结构中运行任何单元测试 （如果已成功生成解决方案）。
- 运行 （如果该解决方案成功生成，并传递任何单元测试） 控制部署过程的自定义项目文件。

最终结果是，如果解决方案成功生成，并且通过单元测试后，web 程序包和部署的任何其他资源部署到测试环境。

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

**DeployToTest**生成定义提供给 MSBuild 的这些参数：


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]


**DeployOnBuild = true**并**DeployTarget = 包**Team Build 生成解决方案中的项目时使用属性。 在项目是 web 应用程序项目，这些属性将指示 MSBuild 创建 web 部署包的项目。 **TargetEnvPropsFile**属性会告知*Publish.proj*文件在哪里可以找到要导入的特定于环境的项目文件。

> [!NOTE]
> 有关如何创建此类的生成定义的详细演练，请参阅[创建该支持部署的生成定义](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。


*Publish.proj*文件包含生成解决方案中的每个项目的目标。 但是，它还包括条件逻辑，跳过这些生成的目标是在 Team Build 中执行该文件。 这样可以充分利用 Team Build 提供，例如，若要运行单元测试的其他生成功能。 如果解决方案生成或单元测试失败， *Publish.proj*将不会执行文件和应用程序将不会部署。

条件逻辑通过计算来实现**BuildingInTeamBuild**属性。 这是自动设置为 MSBuild 属性 **，则返回 true**当您使用 Team Build 来生成项目。

## <a name="deployment-to-staging"></a>部署到过渡环境

在生成符合所有的测试环境中的开发人员团队的要求时，团队可能想要将相同的内部版本部署到过渡环境。 过渡环境通常配置为匹配的生产或"实时"环境作为密切越好，例如，在服务器规范、 操作系统和软件和网络配置方面的特征。 过渡环境通常用于负载测试、 用户验收测试和更广泛的内部评审。 生成直接从生成服务器部署到过渡环境。

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

若要将解决方案部署到过渡环境中，所使用的生成定义**DeployToStaging-WhatIf**并**DeployToStaging**，具有这些特征：

- 它们实际上不生成任何内容。 当 Rob 将解决方案部署到过渡环境时，他想要部署特定的现有版本的已验证并验证在测试环境中。 只需运行控制部署过程的自定义项目文件的生成定义。
- 当 Rob 触发生成时，他使用生成参数来指定哪个生成包含他想要从生成服务器部署的资源。
- 不自动触发的生成定义。 Rob 手动生成进行排队时他想要将解决方案部署到过渡环境。

这是部署到过渡环境的高级别过程：

1. 过渡环境管理员，Rob Walters 排队生成中使用**DeployToStaging-WhatIf**生成定义。 Rob 使用生成定义参数来指定他想要部署的生成。
2. **DeployToStaging-WhatIf**生成定义运行"假设"模式中的自定义项目文件。 像 Rob 正在执行实际部署中，但它实际上不会对目标环境进行任何更改，这会生成日志文件。
3. Rob 审查该日志文件来确定在过渡环境部署的效果。 具体而言，Rob 想要检查将添加内容、 将更新内容，以及将删除的内容。
4. Rob 是否满足部署不会对现有资源或数据进行任何不必要的更改，他排队生成中使用**DeployToStaging**生成定义。
5. **DeployToStaging**生成定义运行的自定义项目文件。 这些发布到过渡环境中的主 web 服务器的部署资源。
6. Web Farm Framework (WFF) 控制器将在过渡环境中的 web 服务器进行同步。 这使应用程序可在服务器场中的所有 web 服务器上。

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

**DeployToStaging**生成定义提供给 MSBuild 的这些参数：


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]


**TargetEnvPropsFile**属性会告知*Publish.proj*文件在哪里可以找到要导入的特定于环境的项目文件。 **OutputRoot**属性重写内置值，指示包含你想要部署的资源的生成文件夹的位置。 当 Rob 队列生成时，他使用**参数**选项卡上提供的更新的值**OutputRoot**属性。

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 有关如何创建此类的生成定义的详细信息，请参阅[部署特定生成](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)。


**DeployToStaging-WhatIf**生成定义包含与相同的部署逻辑**DeployToStaging**生成定义。 但是，它包含其他参数**WhatIf = true**:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]


内*Publish.proj*文件中， **WhatIf**属性指示是否应在"假设"模式下发布部署的所有资源。 换而言之，像这样，已经过部署，但实际上，未更改目标环境中，会生成日志文件。 这样就可以评估建议的部署的影响&#x2014;在特定、 获取添加的内容、 获取更新内容，和内容会被删除&#x2014;实际进行任何更改之前。

> [!NOTE]
> 有关如何配置"假设"部署的详细信息，请参阅[执行"假设"部署](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)。


部署到过渡环境中的主 web 服务器应用程序后，WFF 会自动在服务器场中的所有服务器之间同步应用程序。

> [!NOTE]
> 有关配置 WFF 同步 web 服务器的详细信息，请参阅[使用 Web Farm Framework 创建服务器场](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)。


## <a name="deployment-to-production"></a>部署到生产环境

当生成已批准在过渡环境中时，Fabrikam，Inc.团队可以发布到生产环境的应用程序。 在生产环境是应用程序"活动"和达到它的目标受众的最终用户的位置。

在生产环境是面向 Internet 的外围网络中。 这是独立于包含在生成服务器的内部网络。 生产环境管理员，Lisa Andrews，必须手动将 web 部署包从生成服务器复制，并将其导入 IIS 主生产 web 服务器上。

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

这是部署到生产环境的高级别过程：

1. 开发人员团队建议 Lisa 生成已准备好部署到生产环境。 团队在生成服务器上建议 Lisa 放置文件夹中的 web 部署包的位置。
2. Lisa 从生成服务器收集的 web 包，并将它们复制到生产环境中的主 web 服务器。
3. Lisa 使用 IIS 管理器导入和发布主 web 服务器上的 web 包。
4. WFF 控制器将生产环境中的 web 服务器进行同步。 这使应用程序可在服务器场中的所有 web 服务器上。

### <a name="how-does-the-deployment-process-work"></a>部署过程是如何工作的？

IIS 管理器包括导入应用程序包向导，轻松地将 web 包发布到 IIS 网站。 有关如何执行此过程的演练，请参阅[手动安装 Web 程序包](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)。

## <a name="conclusion"></a>结束语

本主题提供举例说明了典型的企业级 web 应用程序的部署生命周期。

本主题窗体的 web 应用程序部署的各个方面提供指导的教程系列的一部分。 在实践中，在部署过程中，每个阶段有很多其他任务和注意事项，并不能用于实现这些功能都在单个的演练。 有关详细信息，请参考这些教程：

- [Web 部署在企业中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教程提供了使用 MSBuild 和 IIS Web 部署工具 （Web 部署） 的 web 部署技术的全面介绍。
- [配置用于 Web 部署的服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教程提供有关如何配置 Windows server 环境以支持多种部署方案的指南。
- [配置用于 Team Foundation Server 自动 Web 部署](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教程指导如何将部署逻辑集成到 TFS 的生成过程。
- [高级企业 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教程指导如何满足一些更复杂的部署难题组织面临的。

> [!div class="step-by-step"]
> [上一篇](enterprise-web-deployment-scenario-overview.md)
