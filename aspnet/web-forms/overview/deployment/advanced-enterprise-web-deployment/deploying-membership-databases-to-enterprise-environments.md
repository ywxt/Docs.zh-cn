---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 将成员资格数据库部署到企业环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍的重要注意事项和挑战都需要克服时设置 ASP.NET 应用程序服务数据库 （更常见...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 9df152866b54f55c2b00611331e868f98bd2f3e4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827183"
---
<a name="deploying-membership-databases-to-enterprise-environments"></a>将成员资格数据库部署到企业环境
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍的重要注意事项和挑战都需要克服设置 ASP.NET 应用程序的服务进行测试、 过渡或生产环境中 （通常称为成员身份数据库） 的数据库时。 它还介绍了可用来应对这些挑战的方法。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>在将成员资格数据库时，问题是什么？

在大多数情况下，当数据库中，通过部署策略时需要考虑的第一件事是你想要部署哪些的数据。 在开发或测试环境中，你可能想要将用户帐户数据，以便快速且轻松地测试部署。 在过渡或生产环境中，是不太可能想要将用户帐户数据部署。

遗憾的是，ASP.NET 成员资格数据库引入做出这一决定更复杂的一些特定挑战：

- 仅限架构的部署将使处于非正常运行状态的成员资格数据库。 这是因为成员资格数据库包含某些配置数据 (在**aspnet\_SchemaVersions**表) 的数据库正常运行。 在这种情况下，如果以排除用户帐户数据执行成员资格数据库的仅限架构的部署，你将需要运行后期部署脚本添加基本配置数据。
- 根据成员资格数据库的配置方式，成员资格提供程序可以使用计算机密钥对密码进行加密并将其存储在数据库中。 在这种情况下，与数据库部署的任何用户帐户数据将成为目标服务器上不可用。 出于此原因，用户帐户数据部署不受支持的方案。

## <a name="choosing-a-membership-database-strategy"></a>选择成员资格数据库策略

选择如何预配企业服务器环境中的成员资格数据库时，请使用以下准则：

- 如有可能，请不要部署成员资格数据库。 相反，在目标数据库服务器上手动创建成员资格数据库。 如果你未自定义成员资格数据库架构，您可以只需创建一个新就地在目标中使用[ASP.NET SQL Server 注册工具 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。
- 如果别无选择，但若要部署成员资格数据库&#x2014;例如，如果进行了大量修改对数据库架构&#x2014;您应该使用成员资格数据库，若要排除的用户帐户数据的仅限架构的部署，然后运行后期部署脚本来添加任何所需的配置数据。 您可以在这些方法中找到全面的指南[如何： 部署 ASP.NET 成员资格数据库而不包括用户帐户](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)。

务必要记住*的成员资格数据库架构很可能是较为静态*。 即使你已自定义成员资格数据库，也是不太可能需要更新定期架构&#x2014;不会更改 web 应用程序或数据库项目中的代码的频率相同。 在这种情况下，您无需在任何自动化或单步执行部署过程中包括的成员资格数据库。

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>使用 VSDBCMD 更新成员资格数据库架构

如果在第一次部署后修改的成员资格数据库结构，可能不想要使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 来重新部署该数据库。 Web 部署中的数据库部署功能不包括目标数据库进行差异更新的功能&#x2014;相反，Web 部署必须删除并重新创建数据库。 这意味着，您会丢失在过渡或生产环境中通常不需要任何现有用户帐户数据。

替代方法是使用 VSDBCMD 实用程序来更新您的目标数据库的架构。 VSDBCMD 包括两个重要功能。 首先，它可以导入.dbschema 文件的现有数据库的架构。 其次，它可以作为差异更新，这意味着它仅可以将最新的目标数据库所需的更改，并且不会丢失任何数据，对现有数据库中部署.dbschema 文件。

您可以使用以下高级步骤更新成员资格数据库架构：

1. 使用 VSDBCMD**导入**操作生成.dbschema 文件源成员资格数据库。 此过程所述[如何： 从命令提示符下导入架构](https://msdn.microsoft.com/library/dd172135.aspx)。
2. 使用 VSDBCMD**部署**.dbschema 文件部署到您的目标成员资格数据库的操作。 此过程所述[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。

## <a name="conclusion"></a>结束语

本主题介绍了一些需要进行预配不同目标环境中的 ASP.NET 成员资格数据库时可能会面临的挑战。 具体而言，它介绍了为什么仅限架构的部署将使成员资格数据库处于不可操作状态的状态和为什么用户帐户数据部署不支持。 本主题还提供指导如何预配、 部署和更新不同的方案中的成员资格数据库。

## <a name="further-reading"></a>其他阅读材料

有关更多指导和如何使用 VSDBCMD 的示例，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)并[如何： 从命令提示符下导入架构](https://msdn.microsoft.com/library/dd172135.aspx)。 有关详细信息使用 aspnet\_regsql.exe 创建成员资格数据库，请参阅[ASP.NET SQL Server 注册工具 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。 有关部署成员资格数据库的更多常规指南，请参阅[如何： 部署 ASP.NET 成员资格数据库而不包括用户帐户](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)。

> [!div class="step-by-step"]
> [上一页](deploying-database-role-memberships-to-test-environments.md)
> [下一页](excluding-files-and-folders-from-deployment.md)
