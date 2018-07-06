---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: 部署数据库项目 |Microsoft Docs
author: jrjlee
description: 注意： 在许多企业部署情况下，你需要将增量更新发布到已部署的数据库的功能。 替代方法是重新创建...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 1e5af29a91f5f432f9241dc3ba0c8fc0bfcf773f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804978"
---
<a name="deploying-database-projects"></a>部署数据库项目
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 在许多企业部署情况下，您需要能够将增量更新发布到已部署的数据库。 替代方法是重新创建每个部署，这意味着您丢失现有的数据库中的任何数据上的数据库。 使用 Visual Studio 2010 时，使用 VSDBCMD 是增量数据库发布到建议的方法。 但是，Visual Studio 和 Web 发布管道 (WPP) 的下一版本将包括支持增量发布直接的工具。


如果您在 Visual Studio 2010 中打开联系人管理器示例解决方案，您将看到数据库项目包括一个包含四个文件的属性文件夹。

![](deploying-database-projects/_static/image1.png)

与项目文件 (*ContactManager.Database.dbproj*这种情况下)，这些文件控制的生成和部署过程的各个方面：

- *Database.sqlcmdvars*文件提供在部署项目时使用的任何 SQLCMD 变量的值。 每个解决方案配置 （例如，调试和发布） 可以指定不同.sqlcmdvars 文件。
- *Database.sqldeployment*文件提供了特定于部署的设置，例如是否使用在你的项目或目标服务器的排序规则中定义的排序规则是否要重新创建目标数据库。 每个时间，或者只需修改现有的数据库，以使其最新状态，等等。 每个解决方案配置可以指定不同.sqldeployment 文件。
- *Database.sqlpermissions*文件是可用于定义你想要添加到目标数据库的任何权限的 XML 文档。 所有解决方案配置将都共享同一.sqlpermissions 文件。
- *Database.sqlsettings*文件指定要创建的数据库，如要使用的比较运算符的行为和其他操作的排序规则时使用的数据库级别属性。 所有解决方案配置将都共享同一.sqlsettings 文件。

有必要先了解一段时间来在 Visual Studio 中打开这些文件并使自己熟悉的内容。

生成数据库项目时，生成过程创建两个文件：

- 一个*数据库架构*（.dbschema 文件）。 这说明您想要以 XML 格式创建的数据库的架构。
- 一个*部署清单*（.deploymanifest 文件）。 其中包含创建和部署你的数据库所需的所有信息。 它引用.dbschema 文件以及其他资源，如部署说明 （.sqldeployment 文件） 和任何预先部署或后期部署 SQL 脚本。

这显示了这些资源之间的关系：

![](deploying-database-projects/_static/image2.png)

如您所见，.sqlsettings 文件和.sqlpermissions 文件将是生成过程的输入。 数据库项目文件，以及这些文件用于创建数据库架构文件。 .Sqldeployment 文件和.sqlcmdvars 文件传递整个生成过程保持不变。 部署清单指示的数据库架构、.sqldeployment 文件、.sqlcmdvars 文件和任何预先部署或后期部署 SQL 脚本的位置。

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>为什么使用 VSDBCMD 来部署数据库项目？

有各种不同方法可用于部署数据库项目。 但是，并非所有都适用于将数据库项目部署到企业环境中的远程服务器。 请考虑希望从数据库项目部署。 在企业部署方案中，您可能希望：

- 部署数据库项目从远程位置的功能。
- 向现有数据库进行增量更新的功能。
- 包含预先部署脚本或后期部署脚本功能。
- 能够定制部署到多个目标环境。
- 部署数据库项目的较大、 一部分的能力通常编写脚本，单步执行解决方案部署。

有三种主要方法可用于部署数据库项目：

- 可使用 Visual Studio 2010 中的数据库项目类型的部署功能。 当生成和部署数据库项目在 Visual Studio 2010 中的时，部署过程将使用部署清单来生成特定于生成配置的基于 SQL 的部署文件。 如果它已不存在，或者如果已存在对数据库进行任何必要的更改，这将创建数据库。 可以使用 SQLCMD.exe 来运行此文件在目标服务器上，或者可以设置 Visual Studio 创建和运行该文件。 此方法的缺点是，你只能有限地控制部署设置。 通常还可能需要修改 SQL 部署文件，以提供特定于环境的变量值。 使用 Visual Studio 2010 安装，只能使用此方法从一台计算机，而开发人员需要知道并为所有目标环境中提供连接字符串和凭据。
- 您可以使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 到[将数据库部署为 web 应用程序项目的一部分](https://msdn.microsoft.com/library/dd465343.aspx)。 但是，这种方法是更复杂，如果你想要部署数据库项目而不只是复制的目标服务器上的现有本地数据库。 可以配置 Web 部署运行的 SQL 部署脚本中生成数据库项目，但是，为了执行此操作，您需要创建你的 web 应用程序项目的自定义 WPP 目标文件。 这将添加大量复杂的部署过程。 此外，Web 部署不直接支持增量更新到现有的数据库。 这种方法的详细信息，请参阅[扩展到包的数据库项目的 Web 发布管道部署 SQL 文件](https://go.microsoft.com/?linkid=9805121)。
- VSDBCMD 实用程序可用于部署的数据库，使用数据库架构或部署清单。 可以从 MSBuild 目标，这样就可以将数据库发布作为较大的脚本化部署过程的一部分调用 VSDBCMD.exe。 您可以重写.sqlcmdvars 文件和大量 VSDBCMD 命令，以便您可以自定义而无需创建多个生成配置的不同环境的部署中其他数据库的属性中的变量。 VSDBCMD 提供差异化功能，这意味着它将仅对齐具有您的数据库架构的目标数据库的必要更改。 VSDBCMD 还提供了各种命令行选项，让你精细控制部署过程。

此概述中，从您所见，MSBuild 中使用 VSDBCMD 是典型的企业部署方案最适合的方法：

|  | Visual Studio 2010 | Web Deploy 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| 支持远程部署？ | 是 | 是 | 是 |
| 支持增量更新？ | 是 | No | 是 |
| 支持预先部署/后期部署脚本？ | 是 | 是 | 是 |
| 支持多环境部署？ | 有限 | 有限 | 是 |
| 支持脚本化的部署？ | 有限 | 是 | 是 |

此主题的其余部分介绍如何使用 MSBuild 来部署数据库项目 VSDBCMD 使用。

## <a name="understanding-the-deployment-process"></a>了解部署过程

VSDBCMD 实用程序允许你部署使用的数据库架构 （.dbschema 文件） 或部署清单 （.deploymanifest 文件） 的数据库。 在实践中，您几乎总是将使用部署清单，如部署清单允许您为部署的各种属性提供默认值并确定你想要运行任何预先部署或后期部署 SQL 脚本。 例如，使用此 VSDBCMD 命令来部署**ContactManager**数据库添加到测试环境中的数据库服务器：


[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]


这种情况下：

- **/A** (或 **/Action**) 开关可指定希望 VSDBCMD 来执行操作。 可以将此设置为**导入**或**部署**。 **导入**选项用于生成.dbschema 文件从现有数据库，并**部署**选项用于将.dbschema 文件部署到目标数据库。
- **/Manifest** (或**了 /ManifestFile**) 开关标识你想要部署的.deploymanifest 文件。 如果你想要改为使用.dbschema 文件，则可以使用 **/model** (或 **/ModelFile**) 切换。
- **/Cs** (或 **/ConnectionString**) 交换机提供对目标数据库服务器的连接字符串。 请注意，这并不包含的数据库的名称&#x2014;VSDBCMD 需要连接到服务器，以创建该数据库。它不需要连接到单个数据库。 如果.deploymanifest 文件包括一个连接字符串，则可以省略此开关。 如果您仍要使用开关，开关值将覆盖.deploymanifest 值。
- <strong>/P:TargetDatabase</strong>属性提供你想要分配到目标数据库上创建的名称。 这会重写的值<strong>TargetDatabase</strong> .deploymanifest 文件中的属性。 可以使用<strong>/p:</strong> <em>[属性名称]</em>.sqlcmdvars 文件中声明的语法来设置各种部署属性并覆盖任何 SQLCMD 变量。
- **/Dd+** (或 **/DeployToDatabase+**) 开关指示你想要创建部署，并将其部署到目标环境。 如果指定 **/dd-**，或省略开关，VSDBCMD 将生成部署脚本，但将不将其部署到目标环境。 此开关通常是困惑的源下, 一节中更详细地介绍。
- **/Script** (或 **/DeploymentScriptFile**) 开关指定你想要生成部署脚本。 此值不会影响部署过程。

VSDBCMD 的详细信息，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)和[如何： 为准备数据库部署从命令提示符下使用 VSDBCMD。EXE](https://msdn.microsoft.com/library/dd193258.aspx)。

有关如何使用 VSDBCMD 从 MSBuild 项目文件的示例，请参阅[了解构建过程](understanding-the-build-process.md)。 有关如何配置数据库部署设置多个环境的示例，请参阅[多个环境自定义数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。

## <a name="understanding-the-deploytodatabase-switch"></a>了解 DeployToDatabase 开关

行为 **/dd**或 **/DeployToDatabase**开关取决于是否使用 VSDBCMD.dbschema 文件或.deploymanifest 文件。 如果您使用.dbschema 文件，则行为是非常简单：

- 如果指定 **/dd+** 或 **/dd**，VSDBCMD 将生成部署脚本和部署数据库。
- 如果指定 **/dd-** 或省略开关，VSDBCMD 将生成部署脚本。

如果您使用.deploymanifest 文件，则行为是复杂得多。 这是因为.deploymanifest 文件包含属性名称**DeployToDatabase** ，它还确定是否部署该数据库。


[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]


根据数据库项目的属性设置此属性的值。 如果您设置**部署操作**到**创建部署脚本 (.sql)**，值将是**False**。 如果您设置**部署操作**到**创建部署脚本 (.sql) 并将其部署到数据库**，值将是**True**。

> [!NOTE]
> 这些设置与相关联的特定生成配置和平台。 例如，如果你配置的设置**调试**配置，然后将发布使用**发行**配置中，不会使用你的设置。


![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> 在此方案中，**部署操作**应始终设置为**创建部署脚本 (.sql)**，因为您不希望 Visual Studio 2010 将数据库部署。 换而言之， **DeployToDatabase**属性应始终为**False**。


当**DeployToDatabase**指定属性，则 **/dd**开关将仅重写属性的属性值是否**false**:

- 如果**DeployToDatabase**属性是**False**，并指定 **/dd+** 或 **/dd**，将覆盖 VSDBCMD **DeployToDatabase**属性并将其部署数据库。
- 如果**DeployToDatabase**属性是**False**，并指定 **/dd-** 或省略开关，VSDBCMD 不会将部署数据库。
- 如果**DeployToDatabase**属性是**True**，VSDBCMD 将忽略此开关并将数据库部署。
- 每种情况下，而不考虑是否要部署数据库以及生成部署脚本。

## <a name="conclusion"></a>结束语

本主题提供有关 Visual Studio 2010 中的数据库项目生成和部署过程的概述。 它还介绍了如何使用 VSDBCMD.exe 使用 MSBuild 来支持企业级数据库部署。

这在实践中的工作方式的详细信息，请参阅[多个环境自定义数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。

## <a name="further-reading"></a>其他阅读材料

有关如何通过创建单独的部署配置文件为每个环境自定义数据库部署的信息，请参阅[多个环境自定义数据库部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。 有关如何通过运行后期部署脚本来配置数据库角色成员身份的指导，请参阅[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 数据库施加有关该成员身份管理一些独特的挑战的指南，请参阅[的成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

MSDN 上的以下主题提供更广泛的指南和 Visual Studio 数据库项目的背景信息和数据库部署过程：

- [Visual Studio 2010 SQL Server 数据库项目](https://msdn.microsoft.com/library/ff678491.aspx)
- [管理数据库更改](https://msdn.microsoft.com/library/aa833404.aspx)
- [如何： 为准备数据库部署从命令提示符下使用 VSDBCMD。EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [数据库生成和部署的概述](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-web-packages.md)
> [下一页](creating-and-running-a-deployment-command-file.md)
