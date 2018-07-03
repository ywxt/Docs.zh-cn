---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 部署到测试环境的数据库角色成员身份 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何将用户帐户添加到数据库角色作为解决方案部署到测试环境的一部分。 当你部署一个解决方案，其中包含...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: 42ceaa654c7f690f8455c0569e347cd5e9fccf7a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401855"
---
<a name="deploying-database-role-memberships-to-test-environments"></a>部署到测试环境的数据库角色成员身份
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何将用户帐户添加到数据库角色作为解决方案部署到测试环境的一部分。
> 
> 在部署包含到过渡或生产环境的数据库项目的解决方案时，您通常不希望开发人员自动添加到数据库角色的用户帐户。 在大多数情况下，开发人员不会知道哪些用户帐户需要添加到的数据库角色，并在任何时候无法更改这些要求。 但是，如果你部署一个包含到开发数据库项目的解决方案或测试环境，这种情况通常是不同：
> 
> - 开发人员通常重新部署解决方案，定期进行，通常几次一天。
> - 每次部署，这意味着必须创建并添加到角色中每个部署后的数据库用户通常重新创建数据库。
> - 开发人员通常具有完全控制目标开发或测试环境。
> 
> 在此方案中，通常很有利，可自动创建数据库用户并分配数据库角色成员身份作为部署过程的一部分。
> 
> 关键因素是，此操作需要是有条件的目标环境。 如果要部署到过渡或生产环境中，你想要跳过该操作。 如果要部署到开发人员或测试环境，你想要部署而无需进一步干预的角色成员身份。 本主题介绍可用于解决这一难题的一种方法。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

本主题假定：

- 如中所述使用解决方案部署到的项目文件方法拆分[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。
- 如中所述从项目文件以部署数据库项目时，调用 VSDBCMD[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

若要创建的数据库用户并分配角色成员身份数据库项目部署到测试环境时，将需要：

- 创建进行必要的数据库更改的 Transact 结构化查询语言 (Transact SQL) 脚本。
- 创建使用 sqlcmd.exe 实用工具来运行 SQL 脚本的 Microsoft Build Engine (MSBuild) 目标。
- 配置您的项目文件时要调用的目标将解决方案部署到测试环境。

本主题将演示如何执行每个这些过程。

## <a name="scripting-the-database-role-memberships"></a>脚本的数据库角色成员身份

可以在很多不同的方式，创建 TRANSACT-SQL 脚本，并选择在任何位置。 最简单的方法是在 Visual Studio 2010 中创建你的解决方案内的脚本。

**若要创建 SQL 脚本**

1. 在中**解决方案资源管理器**窗口中，展开你的数据库项目节点。
2. 右键单击**脚本**文件夹，指向**添加**，然后单击**新文件夹**。
3. 类型**测试**作为文件夹名称，然后按 Enter。
4. 右键单击**测试**文件夹，指向**添加**，然后单击**脚本**。
5. 在中**添加新项**对话框框中，为您的脚本提供一个有意义的名称 (例如， **AddRoleMemberships.sql**)，然后单击**添加**。

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. 在中*AddRoleMemberships.sql*文件中，添加 TRANSACT-SQL 语句的：

    1. 创建将访问你的数据库的 SQL Server 登录名的数据库用户。
    2. 将数据库用户添加到任何所需的数据库角色。
7. 该文件应类似如下：

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. 保存该文件。

## <a name="executing-the-script-on-the-target-database"></a>在目标数据库上执行脚本

理想情况下，在部署数据库项目时将作为后期部署脚本的一部分运行任何所需的 TRANSACT-SQL 脚本。 但是，部署后脚本不允许你执行有条件地根据解决方案配置或生成属性的逻辑。 替代方法是通过创建直接从 MSBuild 项目文件中，运行您的 SQL 脚本**目标**执行 sqlcmd.exe 命令的元素。 此命令可用于目标数据库上运行脚本：


[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]


> [!NOTE]
> Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。


在 MSBuild 目标中嵌入此命令之前，需要考虑在什么条件下你想要运行的脚本：

- 目标数据库必须存在才能更改其角色成员身份。 在这种情况下，您需要运行此脚本*后*数据库部署。
- 您需要包含一个条件，以便仅用于测试环境执行的脚本。
- 如果你正在运行"假设"部署&#x2014;换而言之，如果你正在生成部署脚本，但实际上未运行它们&#x2014;不应运行 SQL 脚本。

如果您正使用拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，如下所示的联系人管理器示例解决方案，可以拆分的生成说明 SQL 脚本如下：

- 任何所需的特定于环境的属性，属性，用于确定是否要部署的权限，以及应该在特定于环境的项目文件中 (例如， *Env Dev.proj*)。
- MSBuild 目标本身，以及将不会更改目标环境之间的任何属性应该在通用项目文件中 (例如， *Publish.proj*)。

在特定于环境的项目文件中，您需要定义数据库服务器名称、 目标数据库名称和一个布尔属性，使用户可以指定是否部署角色成员身份。


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]


在通用项目文件中，你需要提供 sqlcmd 可执行文件的位置以及你想要运行的 SQL 脚本的位置。 这些属性将保持不变而不考虑目标环境。 此外需要创建一个 MSBuild 目标执行 sqlcmd 命令。


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]


请注意将 sqlcmd 可执行文件的位置添加作为静态属性，因为这可能是到其他目标很有用。 与此相反，您定义 SQL 脚本的位置和 sqlcmd 命令的语法在目标内的动态属性作为它们将不会需要之前执行该目标。 在这种情况下， **DeployTestDBPermissions**满足这些条件时，才会执行目标：

- **DeployTestDBRoleMemberships**属性设置为**true**。
- 用户未指定**WhatIf = true**标志。

最后，别忘了调用目标。 在中*Publish.proj*文件中，您可以执行此操作通过将目标添加到默认值的依赖项列表**FullPublish**目标。 您需要确保**DeployTestDBPermissions**之前未执行目标**PublishDbPackages**执行目标。


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]


## <a name="conclusion"></a>结束语

本主题描述了在其中您可以添加数据库用户和角色成员身份作为后期部署操作部署数据库项目时的一种方法。 定期重新创建数据库在测试环境中，但通常当将数据库部署到过渡或生产环境时要避免这样做时，这是通常很有用。 在这种情况下，应确保使用所需的条件逻辑，以便适合要执行此操作时仅创建数据库用户和角色成员身份。

## <a name="further-reading"></a>其他阅读材料

有关使用 VSDBCMD 部署数据库项目的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 有关自定义不同的目标环境的数据库部署的指导，请参阅[多个环境自定义数据库部署](customizing-database-deployments-for-multiple-environments.md)。 使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。 Sqlcmd 命令行选项的详细信息，请参阅[sqlcmd 实用工具](https://msdn.microsoft.com/library/ms162773.aspx)。

> [!div class="step-by-step"]
> [上一页](customizing-database-deployments-for-multiple-environments.md)
> [下一页](deploying-membership-databases-to-enterprise-environments.md)
