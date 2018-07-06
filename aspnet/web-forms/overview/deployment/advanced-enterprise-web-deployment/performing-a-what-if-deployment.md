---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 如果执行什么部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何执行假设 （或模拟） 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 和 V 部署...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: f54a4d91ea0f735d3cd5b99c0dda5d83cbb5e5d4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830644"
---
<a name="performing-a-what-if-deployment"></a>执行"假设"部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何执行"假设"（或模拟） 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 和 VSDBCMD 的部署。 这样可以在实际部署你的应用程序之前确定部署逻辑对特定目标环境的影响。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="performing-a-what-if-deployment-for-web-packages"></a>执行"假设"部署 Web 包

Web 部署包括使你能够执行"假设"中的部署的功能 （或试用版） 模式。 在部署中"假设"模式下的项目时，Web 部署生成一个日志文件，像执行了部署，但它实际上不会更改目标服务器上的任何内容。 查看日志文件可帮助你了解你的部署将特别是对目标服务器上，产生的影响：

- 获取添加内容。
- 获取更新内容。
- 什么会被删除。

因为"假设"部署实际上不会更改内容始终不能在目标服务器上的任何内容是预测是否会成功部署。

如中所述[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)，你可以部署两种方式使用 Web 部署的 web 包&#x2014;使用 MSDeploy.exe 命令行实用程序直接或通过运行 *。 deploy.cmd*文件将生成的生成过程。

如果您直接使用 MSDeploy.exe，则可以通过添加运行"假设"部署 **– whatif**到命令中的标志。 例如，若要评估如果 ContactManager.Mvc.zip 包部署到过渡环境，会发生什么情况，MSDeploy 命令应类似如下：


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


"假设"部署的结果感到满意后，可以删除 **– whatif**标志来运行实时部署。

> [!NOTE]
> 有关 MSDeploy.exe 命令行选项的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。


如果您使用的 *。 deploy.cmd*文件中，您可以通过包含运行"假设"部署 **/t**标志 （试用模式） 而不是标志 **/y**中的标志 （"是，"或更新模式）你的命令。 例如，若要评估如果 ContactManager.Mvc.zip 包部署的运行，会发生什么情况 *。 deploy.cmd*文件中，您的命令应类似于下面：


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


"试用模式"部署的结果感到满意后，您可以替换 **/t**与标志 **/y**标志来运行实时部署：


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> 有关详细信息的命令行选项 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。 如果在运行 *。 deploy.cmd*文件而无需指定任何标志，命令提示符将显示可用标志的列表。


## <a name="performing-a-what-if-deployment-for-databases"></a>执行"假设"部署的数据库

本部分假设你使用的 VSDBCMD 实用程序来执行增量备份，基于架构的数据库部署。 此方法进行了更详细地[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 我们建议你了解与本主题之前应用此处所述的概念。

当你使用在 VSDBCMD**部署**模式下，可以使用 **/dd** (或 **/DeployToDatabase**) 标记，用于控制是否 VSDBCMD 实际部署数据库或只是生成部署脚本。 如果你正在部署.dbschema 文件，这是行为：

- 如果指定 **/dd+** 或 **/dd**，VSDBCMD 将生成部署脚本和部署数据库。
- 如果指定 **/dd-** 或省略开关，VSDBCMD 将生成部署脚本。

> [!NOTE]
> 如果你正在部署.deploymanifest 文件而不是.dbschema 文件的行为 **/dd**开关是复杂得多。 VSDBCMD 实质上，将忽略的值 **/dd**切换如果.deploymanifest 文件包含**DeployToDatabase**的值元素**True**。 [部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)描述完整此行为。


例如，若要生成的部署脚本**ContactManager**数据库而不实际部署的数据库，VSDBCMD 命令应类似于下面：


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


VSDBCMD 是差异数据库部署工具，并且这种情况下部署脚本动态生成以包含所有更新当前数据库中，如果存在，为指定的架构所需的 SQL 命令。 查看部署脚本是有用的方式来确定有何影响你的部署将对当前数据库和它所包含的数据。 例如，你可能想要确定：

- 是否将删除任何现有的表，并且是否这会导致数据丢失。
- 无论操作的顺序中会带来风险的数据丢失，例如，如果你拆分或合并表。

如果您愿意使用部署脚本，您可以重复使用 VSDBCMD **/dd+** 标志来进行更改。 或者，可以编辑部署脚本来满足您的要求，然后在数据库服务器上手动执行。

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>将"假设"功能集成到自定义项目文件

在更复杂的部署方案中，你将想要使用自定义的 Microsoft Build Engine (MSBuild) 项目文件来封装你生成和部署的逻辑，如中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 例如，在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案， *Publish.proj*文件：

- 生成解决方案。
- 使用 Web 部署来打包和部署 ContactManager.Mvc 应用程序。
- 使用 Web 部署来打包和部署 ContactManager.Service 应用程序。
- 部署**ContactManager**数据库。

集成时的多个 web 包和/或数据库部署到单步执行进程以这种方式，您还可以在"假设"模式下执行整个部署的选项。

*Publish.proj*文件演示了如何执行此操作。 首先，需要创建用于存储"假设"值的属性：


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


在这种情况下，创建名为的属性**WhatIf**默认值为**false**。 用户可通过将属性设置为覆盖此值 **，则返回 true**在命令行参数中，你很快将会介绍。

下一阶段是参数化任何 Web 部署和 VSDBCMD 命令，以便反映标志**WhatIf**属性值。 例如下, 一个目标 (摘自*Publish.proj*文件，并简化) 运行 *。 deploy.cmd*文件来部署 web 包。 默认情况下，该命令包含 **/Y**开关 （"是，"或更新模式）。 如果**WhatIf**设置为**true**，这将替换为 **/T**开关 （试用版或"假设"模式下）。


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


同样下, 一步目标使用 VSDBCMD 实用程序来部署数据库。 默认情况下 **/dd**不包含开关。 这意味着 VSDBCMD 将生成部署脚本，但不是会将数据库部署&#x2014;换而言之，"假设"方案。 如果**WhatIf**属性未设置为**true**即 **/dd**添加开关并将其 VSDBCMD 将部署数据库。


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


相同的方法可用于所有相关的命令参数化在项目文件中。 当你想要运行"假设"部署时，然后，可以只需提供**WhatIf**属性值从命令行：


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


这样一来，可以运行"假设"部署，以在单个步骤中的所有项目组件。

## <a name="conclusion"></a>结束语

本主题介绍了如何运行"假设"使用 Web 部署、 VSDBCMD 和 MSBuild 的部署。 "假设"部署可让你实际上到目标环境进行任何更改之前评估建议的部署的影响。

## <a name="further-reading"></a>其他阅读材料

Web 部署命令行语法的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 有关当你使用的命令行选项的指导 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。 有关 VSDBCMD 命令行语法的指导，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。

> [!div class="step-by-step"]
> [上一页](advanced-enterprise-web-deployment.md)
> [下一页](customizing-database-deployments-for-multiple-environments.md)
