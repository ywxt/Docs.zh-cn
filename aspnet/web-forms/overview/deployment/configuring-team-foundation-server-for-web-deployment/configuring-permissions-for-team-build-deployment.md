---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 配置权限的团队生成部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置权限，以使您的生成服务器将自动 b 的一部分内容部署到 web 服务器和数据库服务器...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 0142be694a4e7d601625022f6fbfe39971823d03
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834523"
---
<a name="configuring-permissions-for-team-build-deployment"></a>配置权限的团队生成部署
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置权限，以使您的生成服务器将自动的生成过程的一部分内容部署到 web 服务器和数据库服务器。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

在安装 Team Foundation Server (TFS) 2010年生成服务时，你指定想要运行的服务的标识。 默认情况下，这是网络服务帐户。 或者，可以配置生成服务使用域帐户运行。

需要 Windows 身份验证，并且打算使用 Team Build，自动执行的任何部署任务将使用生成服务标识运行。 在这种情况下，你将需要授予你的 web 服务器和数据库服务器上任何所需的权限的生成服务标识。

> [!NOTE]
> 网络服务帐户使用计算机帐户对其他计算机进行身份验证。 计算机帐户需要在窗体 * [域名]\[计算机名称] ***$**&#x2014;等**FABRIKAM\TFSBUILD$**。 在这种情况下，如果生成服务运行时使用网络服务标识，则应授予计算机帐户标识为任何所需的权限为您的生成服务器。


## <a name="configuring-web-server-permissions"></a>配置 Web 服务器权限

如中所述[选择右方法对 Web 部署](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)，如果你想要将 web 包部署到远程 web 服务器可以使用两种主要方法：

- 将从远程位置应用程序部署通过面向*Web 部署代理服务*（也称为远程代理） 目标服务器上。
- 将从远程位置应用程序部署通过面向*Internet 信息服务*(*IIS) Web 部署处理程序*目标服务器上。

远程代理在这种情况下具有两个关键限制：

- 远程代理仅支持 NTLM 身份验证。 换而言之，部署必须使用生成服务标识&#x2014;不能模拟另一个帐户。
- 若要使用远程代理，执行部署的帐户必须是目标服务器上的管理员。

总之，这些两个限制使远程代理方法不可取的 Team Build 的自动化部署。 若要使用此方法，您需要使生成服务帐户在任何目标 web 服务器上的管理员。

与此相反，Web 部署处理程序方法提供了各种优势：

- Web 部署处理程序通过 HTTPS，以便您可以将备用帐户的凭据传递给 IIS Web 部署工具 （Web 部署） 支持基本身份验证。
- 可以配置目标 web 服务器以允许非管理员用户将内容部署到使用 Web 部署处理程序的特定 IIS 网站。

因此，很显然更可取的方法时自动执行从 Team Build web 包部署的目标 Web 部署处理程序。 这是建议采用的过程：

1. 创建要用于部署的低特权域帐户。
2. 配置 Web 部署处理程序并为帐户授予所需的权限将内容部署到特定的 IIS 网站，如中所述[用于 Web 部署发布 （Web 部署处理程序） 配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。
3. 调用 Web 部署和目标 Web 部署处理程序，使用基本身份验证并提供域帐户的凭据创建，来执行部署。

在中[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案，你指定的身份验证类型 (基本或 NTLM)，Web 部署凭据和特定于环境的项目文件中的终结点地址 （远程代理或 Web 部署处理程序）。 这些值用于构建和执行项目文件时运行 Web 部署命令。 有关详细信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。

有关详细信息配置 Web 部署处理程序，包括如何配置权限，请参阅[用于 Web 部署发布 （Web 部署处理程序） 配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 有关配置远程代理的详细信息，请参阅[配置 Web 服务器的 Web 部署发布 （远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。

## <a name="configuring-database-server-permissions"></a>配置数据库服务器权限

若要将数据库部署到 SQL Server，必须：

- SQL Server 实例上创建部署帐户的登录名。
- 授予该登录名**DBCreator** SQL Server 实例上的权限。
- 在初始部署后添加到的登录名**db\_所有者**对目标数据库的角色。 这是必需的因为在后续部署，您要修改现有数据库而不是创建新的数据库。

您可以进行身份验证到使用 NTLM 身份验证或 SQL Server 身份验证的 SQL Server 实例：

- 如果使用 NTLM 身份验证，需要授予上述生成服务帐户的权限。
- 如果使用 SQL Server 身份验证，需要授予上述 SQL Server 帐户的权限。 此外需要用于部署的数据库连接字符串中包含的 SQL Server 用户名和密码。

有关如何配置权限的数据库部署的分步详细信息，请参阅[配置数据库服务器的 Web 部署发布](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。

## <a name="conclusion"></a>结束语

此时，应了解所需的权限，以及打开您的身份验证选项时自动从 Team Build 的 web 应用程序和数据库部署。 此外应能够在 IIS web 服务器和 SQL Server 数据库服务器上实现所需的权限。

## <a name="further-reading"></a>其他阅读材料

有关配置 Windows server 环境，以支持远程部署的详细信息，请参阅[用于 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一篇](deploying-a-specific-build.md)
