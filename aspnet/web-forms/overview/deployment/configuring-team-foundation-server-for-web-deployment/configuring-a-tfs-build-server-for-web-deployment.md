---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 配置 TFS 生成服务器用于 Web 部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何准备 Team Foundation Server (TFS) 生成服务器生成和部署你的解决方案使用 Team Build 和 Internet 信息...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 534a0edf5c26dd2daec3c44e41410f8c5de96c15
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824835"
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a>配置用于 Web 部署的 TFS 生成服务器
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何准备用于生成和部署你使用 Team Build 和 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 的解决方案的 Team Foundation Server (TFS) 生成服务器。


本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。

这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。 在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

若要准备用于生成和部署你的解决方案的生成服务器，你将需要：

- 安装和配置 TFS 生成服务。
- 安装 Visual Studio 2010。
- 安装任何产品或生成你的解决方案，类似于 ASP.NET MVC 的.NET Framework 的版本所需的组件。
- 安装 Web 部署 2.0 或更高版本。

本主题将演示如何执行这些过程，或指向在它们存在的其他资源。 任务和本主题中的演练假设：

- 刚开始使用运行 Windows Server 2008 R2 Service Pack 1 的干净的服务器内部版本。
- 服务器已加入域具有静态 IP 地址。
- 你已在单独服务器上，安装 TFS 应用层，如中所述[企业 Web 部署： 方案概述](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。

### <a name="who-performs-these-procedures"></a>谁将执行以下步骤？

在大多数情况下，TFS 管理员将负责配置生成服务器。 在某些情况下，开发人员团队可能需要特定的生成服务器的所有权。

## <a name="install-and-configure-the-tfs-build-service"></a>安装和配置 TFS 生成服务

在配置生成服务器时，您的首要任务是安装和配置 TFS 生成服务。 作为此过程的一部分，你将需要：

- 安装 TFS 生成服务和配置服务帐户。 任何生成任务，包括部署中，将使用的生成服务帐户身份运行。
- 创建*生成控制器*和一个或多个*生成代理*。 每个生成控制器管理一组生成代理。 当您对生成进行排队时，生成控制器将生成任务分配给可用的生成代理。 在 TFS 中的每个团队项目集合映射到单个生成控制器。
- 配置生成输出的放置文件夹。 这是网络共享。 任何生成输出，如 web 部署包时，被发送到放置文件夹。

[管理 Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) MSDN 上的一章包含所需执行这些任务的所有资源：

- 有关 Team Foundation Build 的概念性概述，包括生成服务、 生成控制器和生成代理，请参阅[了解 Team Foundation Build 系统](https://msdn.microsoft.com/library/dd793166.aspx)。
- 有关安装和配置生成服务的信息，请参阅[配置生成计算机](https://msdn.microsoft.com/library/ms181712.aspx)。
- 创建生成控制器的信息，请参阅[创建和使用生成控制器工作](https://msdn.microsoft.com/library/ee330987.aspx)。
- 创建生成代理的信息，请参阅[创建和使用生成代理工作](https://msdn.microsoft.com/library/bb399135.aspx)。
- 有关创建和配置的放置文件夹的信息，请参阅[设置放置文件夹](https://msdn.microsoft.com/library/bb778394.aspx)。

## <a name="install-required-products-and-components"></a>安装所需的产品和组件

若要启用要生成你的解决方案的生成服务器，必须安装任何产品、 组件或您的解决方案需要的程序集。 在安装任何 web 平台组件之前，应在生成服务器上安装 Visual Studio 2010 （任何版本）。 这可确保将生成服务使用的核心 Microsoft Build Engine (MSBuild) 目标文件及 Web 发布管道 (WPP) 目标文件。 在 Visual Studio 安装程序还应安装 Web 部署，但需要您如果你打算将 web 包部署为生成过程的一部分。

安装常用的 web 平台组件的最佳方法是使用[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。 这确保要安装最新版本的每个产品，并且它还会自动检测并安装所有必备组件的每个产品。 情况下[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解决方案中，您应使用 Web 平台安装程序来安装这些产品和组件：

- **.NET framework 4.0**。 这是运行此版本的.NET Framework 生成的应用程序所需要的。
- **Web 部署工具 2.1 或更高版本**。 这在你的服务器上安装 Web 部署 （和其基础可执行文件，MSDeploy.exe）。 作为此过程的一部分，它会安装并启动 Web 部署代理服务。 此服务允许你部署 web 包从远程计算机。
- **ASP.NET MVC 3**。 这会安装您需要运行 ASP.NET MVC 3 应用程序的程序集。

**若要安装必需的产品和组件**

1. 安装 Visual Studio 2010。 当系统提示选择要安装的功能，您应包括：

    1. 您需要编译任何编程语言。
    2. Visual Web 开发人员。 这可确保 WPP 目标都添加到您的生成服务器。

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 的安装完成后，下载并安装[Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) （如果它尚不存在包含安装介质中）。

    > [!NOTE]
    > Visual Studio 2010 Service Pack 1 解决了一个 bug，可以防止 MSBuild 查找 MSDeploy 可执行文件。
3. 下载并启动[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。
4. 在顶部**Web 平台安装程序 3.0**窗口中，单击**产品**。
5. 在左侧和右侧的窗口中，在导航窗格中，单击**框架**。
6. 在中**Microsoft.NET Framework 4**行，如果尚未安装.NET Framework，单击**添加**。

    > [!NOTE]
    > 你可能已安装.NET Framework 4.0 到 Windows 更新。 如果已安装的产品或组件，Web 平台安装程序将此信息指示通过替换**外**按钮，其文本**已安装**。

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. 在中**ASP.NET MVC 3 (Visual Studio 2010)** 行中，单击**添加**。
8. 在导航窗格中，单击**Server**。
9. 在中**Web 部署工具 2.1**行中，单击**添加**。
10. 单击“安装” 。 Web 平台安装程序将显示产品列表&#x2014;以及任何关联的依赖关系&#x2014;安装，并将提示你接受许可条款。
11. 查看许可条款，如果同意条款，单击**我接受**。
12. 安装完成后，单击**完成**，然后关闭**Web 平台安装程序 3.0**窗口。

> [!NOTE]
> 如果在部署过程包括 VSDBCMD.exe 或 SQLCMD.exe 等工具使用，您将需要确保这些在生成服务器上安装。 VSDBCMD.exe 是 Visual Studio 工具，并在安装 Team Foundation Build 时通常添加到服务器。 SQLCMD.exe 是 SQL Server 工具。 可以下载独立版本从 SQLCMD.exe [Microsoft SQL Server 2008 R2 功能包](https://go.microsoft.com/?linkid=9805134)页。


## <a name="conclusion"></a>结束语

此时，您的生成服务器已准备好开始构建和部署您的 web 应用程序项目。 下一主题[创建生成定义，支持部署](creating-a-build-definition-that-supports-deployment.md)，介绍如何创建和配置生成定义来控制何时以及如何生成和部署你的项目。

## <a name="further-reading"></a>其他阅读材料

有关如何使用 Team Build 的更多常规指南，请参阅[管理 Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx)。

> [!div class="step-by-step"]
> [上一页](adding-content-to-source-control.md)
> [下一页](creating-a-build-definition-that-supports-deployment.md)
