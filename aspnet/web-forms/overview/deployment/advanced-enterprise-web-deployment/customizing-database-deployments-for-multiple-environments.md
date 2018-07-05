---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: 自定义数据库部署为多个环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何部署过程的一部分定制为特定的目标环境数据库的属性。 注意： 本主题假定第...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 3a368e5055f4921b68f5c5eb2739728a2f1fd4d2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378068"
---
<a name="customizing-database-deployments-for-multiple-environments"></a>自定义多个环境的数据库部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何部署过程的一部分定制为特定的目标环境数据库的属性。
> 
> > [!NOTE]
> > 本主题假定你要部署使用 MSBuild.exe 和 VSDBCMD.exe 的 Visual Studio 2010 数据库项目。 为什么可能会选择这种方法的详细信息，请参阅[企业中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)并[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。
> 
> 
> 在数据库项目部署到多个目标时，通常需要自定义每个目标环境的数据库部署属性。 例如，在测试环境中你将通常重新创建数据库上每个部署，而在过渡或生产环境中，您可能是一种更有可能进行增量更新，以保留您的数据。
> 
> 在 Visual Studio 2010 数据库项目中，部署设置包含在部署配置 (.sqldeployment) 文件。 本主题将演示如何创建特定于环境的部署配置文件，并指定你想要用作 VSDBCMD 参数的一个。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

本主题假定：

- 如中所述使用解决方案部署到的项目文件方法拆分[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。
- 如中所述从项目文件以部署数据库项目时，调用 VSDBCMD[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

若要创建支持不同的目标环境之间的数据库部署属性的部署系统，您将需要：

- 创建每个目标环境的部署配置 (.sqldeployment) 文件。
- 创建指定部署配置文件作为命令行开关的 VSDBCMD 命令。
- 参数化 VSDBCMD 命令在 Microsoft Build Engine (MSBuild) 项目文件中，以便 VSDBCMD 选项是适用于目标环境。

本主题将演示如何执行每个这些过程。

## <a name="creating-environment-specific-deployment-configuration-files"></a>创建特定于环境的部署配置文件

默认情况下，数据库项目包含名为的单个部署配置文件*Database.sqldeployment*。 如果您在 Visual Studio 2010 中打开此文件，您可以查看可供您的不同的部署选项：

- **部署比较排序规则**。 您可以选择是否使用你的项目的数据库排序规则 (*源*排序规则) 或你的目标服务器的数据库排序规则 (*目标*排序规则)。 在大多数情况下，你将想要将部署到开发或测试环境时使用源排序规则。 在部署到过渡或生产环境时，通常需要保留不变以避免任何互操作性问题的目标排序规则。
- **部署数据库属性**。 您可以选择是否要应用的数据库属性，如中所定义*Database.sqlsettings*文件。 在第一次部署数据库时，应该部署数据库属性。 如果正在更新现有数据库，属性应已就位，并且不应需要重新部署它们。
- **始终重新创建数据库**。 这允许您选择是否要重新创建目标数据库，每次部署或与您的架构进行增量更改，以使目标数据库保持最新。 如果重新创建数据库时，将会丢失现有数据库中的任何数据。 在这种情况下，您应通常设置为**false**以便部署到过渡或生产环境。
- **如果可能发生数据丢失则阻止增量部署**。 这允许您选择是否应停止部署，是否对数据库架构的更改将导致数据丢失。 通常将此设置为 **，则返回 true**以部署到生产环境中，以便为您提供机会介入并保护任何重要数据。 如果设置了**始终重新创建数据库**到**false**，此设置不起作用。
- **在单用户模式下执行部署**。 这通常不是开发或测试环境中的问题。 但是，您应通常设置为 **，则返回 true**以便部署到过渡或生产环境。 这可以防止用户进行部署时对数据库进行更改。
- **备份数据库之前部署**。 通常将此设置为 **，则返回 true**当你将部署到生产环境中，为防止数据丢失预防措施。 您可能还想要将其设置为 **，则返回 true**时你将部署到过渡环境中，如果临时数据库包含大量数据。
- **生成目标数据库中但不在数据库项目中的对象的 DROP 语句**。 在大多数情况下，这是对数据库进行增量更改的整型和重要的部分。 如果设置了**始终重新创建数据库**到**false**，此设置不起作用。
- **不使用 ALTER ASSEMBLY 语句更新 CLR 类型**。 此设置确定如何 SQL Server 应更新公共语言运行时 (CLR) 类型到较新的程序集版本。 这应设置为**false**在大多数情况下。

此表显示了不同的目标环境的典型的部署设置。 但是，你的设置可能根据确切需求而异。

|  | 开发人员/测试 | 过渡/集成 | 生产 |
| --- | --- | --- | --- |
| **部署比较排序规则** | 源 | 目标 | 目标 |
| **部署数据库属性** | True | 仅限首次 | 仅限首次 |
| **始终重新创建数据库** | True | False | False |
| **如果可能发生数据丢失则阻止增量部署** | False | 您可能 | True |
| **在单用户模式下执行部署脚本** | False | True | True |
| **部署前备份数据库** | False | 您可能 | True |
| **生成目标数据库中但不在数据库项目中的对象的 DROP 语句** | False | True | True |
| **不使用 ALTER ASSEMBLY 语句更新 CLR 类型** | False | False | False |
  

> [!NOTE]
> 有关数据库部署属性和环境注意事项的详细信息，请参阅[数据库项目设置概述](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)，[如何： 为部署详细信息配置属性](https://msdn.microsoft.com/library/dd172125.aspx)， [生成并将数据库部署到独立的开发环境](https://msdn.microsoft.com/library/dd193409.aspx)，并[生成并将数据库部署到过渡或生产环境](https://msdn.microsoft.com/library/dd193413.aspx)。


若要支持到多个目标数据库项目的部署，应创建每个目标环境的部署配置文件。

**若要创建的特定于环境的配置文件**

1. 在 Visual Studio 2010 中，在**解决方案资源管理器**窗口中，右键单击数据库项目，然后依次**属性**。
2. 在数据库项目属性页上，在**部署**选项卡上，在**部署配置文件**行中，单击**新建**。

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. 在中**新的部署配置文件**对话框框中，为该文件提供一个有意义的名称 (例如， **TestEnvironment.sqldeployment**)，然后单击**保存**。
4. 上 *[文件名]***.sqldeployment** 页上，设置部署属性以匹配你的目标环境的要求，然后保存该文件。

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. 请注意，新文件添加到您的数据库项目中的属性文件夹。

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>在 VSDBCMD 中指定部署配置文件

当使用 Visual Studio 2010 中的解决方案配置 （如调试和发布） 时，可以将部署配置文件关联与每个配置。 生成一个特定的配置时，生成过程会生成特定于配置的部署清单文件指向特定于配置的部署配置文件。 但是，在这些教程中所述的部署方法的主要目标之一是使用户能够控制部署过程，而无需使用 Visual Studio 2010 和解决方案配置。 在这种方法，将解决方案配置是相同而不考虑目标部署环境。 若要调整数据库部署到特定的目标环境，可以使用 VSDBCMD 命令行选项以指定你的部署配置文件。

若要在你 VSDBCMD 指定部署配置文件，请使用**p: / DeploymentConfigurationFile**开关并提供你的文件的完整路径。 这将重写的部署清单标识的部署配置文件。 例如，可以使用此 VSDBCMD 命令来部署**ContactManager**数据库添加到测试环境：


[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]


> [!NOTE]
> 请注意，生成过程可能会重命名.sqldeployment 文件时将文件复制到输出目录。


如果在您预先部署或后期部署的 SQL 脚本中使用的 SQL 命令变量，可以使用类似的方法来将特定于环境的.sqlcmdvars 文件与你的部署相关联。 在这种情况下，使用**p: / SqlCommandVariablesFile**开关来标识.sqlcmdvars 文件。

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>从 MSBuild 项目文件运行 VSDBCMD 命令

您可以通过使用调用 MSBuild 项目文件中的 VSDBCMD 命令**Exec** MSBuild 目标内的任务。 最简单形式，它将类似如下：


[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]


- 在实践中，以使你的项目文件更易于阅读和重复使用，你将想要创建用于存储的各种命令行参数的属性。 这使得更容易为用户提供特定于环境的项目文件中的属性值，或重写 MSBuild 命令行中的默认值。 如果使用拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，应相应地将您的生成说明和两个文件之间的属性：
- 特定于环境的设置，例如部署配置文件名、 数据库连接字符串和目标数据库名称，应该在特定于环境的项目文件中。
- 在通用项目文件中应该运行 VSDBCMD 命令，以及任何通用的属性，如 VSDBCMD 可执行文件的位置的 MSBuild 目标。

您还应确保生成数据库项目，然后调用 VSDBCMD 以便.deploymanifest 文件已创建，并可供使用。 可以看到这种方法在本主题中的完整示例[了解构建过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，将介绍项目文件[联系人管理器示例解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)。

## <a name="conclusion"></a>结束语

本主题介绍如何在部署数据库项目使用 MSBuild 和 VSDBCMD 时定制到不同的目标环境的数据库属性。 当您需要将数据库项目部署为更大的企业级解决方案的一部分时，此方法非常有用。 这些解决方案通常会部署到多个目标，例如沙盒开发或测试环境、 过渡或集成平台，以及生产或实时环境中。 每个目标环境通常需要一组唯一的数据库部署属性。

## <a name="further-reading"></a>其他阅读材料

部署数据库项目使用 VSDBCMD.exe 的详细信息，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)并[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

MSDN 上的这些文章提供有关数据库部署的更全面的指导：

- [数据库项目设置的概述](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [如何： 配置的部署详细信息属性](https://msdn.microsoft.com/library/dd172125.aspx)
- [生成并部署到独立的开发环境中的数据库](https://msdn.microsoft.com/library/dd193409.aspx)
- [生成并将数据库部署到过渡或生产环境](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [上一页](performing-a-what-if-deployment.md)
> [下一页](deploying-database-role-memberships-to-test-environments.md)
