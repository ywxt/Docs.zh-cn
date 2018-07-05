---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 使用 Visual Studio 的 ASP.NET Web 部署： 简介 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 V...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: ad06639db9c5de78fb9926c7ab00e348bcbb20cb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382551"
---
<a name="aspnet-web-deployment-using-visual-studio-introduction"></a>使用 Visual Studio 的 ASP.NET Web 部署： 简介
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 的 Azure SDK for.NET。 大部分过程都是类似于 Visual Studio 2013。
> 
> 开发 web 应用程序，以便使其能够通过 Internet 的人员。 但 web 编程教程通常停止后它们已显示如何在开发计算机上工作。 本系列教程开始，将其他保持关闭状态： 已生成的 web 应用，进行测试，并已做好准备。 后续步骤 这些教程介绍如何首先部署到用于测试，在本地开发计算机上的 IIS，然后再到 Azure 或第三方托管提供商为过渡和生产。 将部署的示例应用程序是使用实体框架、 SQL Server 和 ASP.NET 成员资格系统的 web 应用程序项目。 示例应用程序使用 ASP.NET Web 窗体，但显示的过程也同样适用于 ASP.NET MVC 和 Web API。
> 
> 这些教程假定您知道如何使用 Visual Studio 中的 ASP.NET。 如果不这样做，是一个良好起点[基本的 ASP.NET Web 窗体教程](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md)或[基本的 ASP.NET MVC 教程](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。
> 
> 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 部署论坛](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)或[StackOverflow](http://stackoverflow.com)。
> 
> 此内容也是可作为免费电子书[TechNet 电子书库](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)。


## <a name="overview"></a>概述

这些教程将指导你完成部署包含 SQL Server 数据库的 ASP.NET web 应用程序。 用于测试，在本地开发计算机上的 IIS，然后再在 Azure 应用服务和 Azure SQL 数据库来暂存和生产环境中的 Web 应用，你将首先部署。 您将了解如何使用一键式发布，Visual Studio 部署，将看到如何使用命令行部署。

许多教程可能会使部署过程令人望而生畏。 事实上，基本的过程非常简单。 但是，在实际情况下，您通常需要执行额外的部署任务 — 例如，在目标服务器上设置文件夹权限。 我们已演示其中一些其他任务，以不省略一些可能会阻止您成功部署实际的应用程序的信息，这些教程期待。

教程设计为在序列中，运行并在前一部分生成的每个部分。 可以跳过不到您的具体情况，相关的部分，但然后可能需要调整在后续教程中的过程。

## <a name="intended-audience"></a>目标的受众

本教程旨在 ASP.NET 开发人员在环境中工作的：

- Azure 应用服务 Web 应用或第三方托管提供商，在生产环境。
- 部署并不局限于持续集成过程，但可能会直接从 Visual Studio 完成。

从部署[源代码管理](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)使用[持续交付](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)除了一本教程演示如何从命令行部署这些教程不介绍过程。 持续交付有关的信息，请参阅以下资源：

- [持续集成和持续交付 （使用 Windows Azure 构建实际云应用）](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [部署 Azure 应用服务中的 web 应用](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [部署 Web 应用程序在企业方案中](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)（较旧的集为 Visual Studio 2010，还有用于企业环境的有用信息编写的教程。）

## <a name="using-a-third-party-hosting-provider"></a>使用第三方托管提供商

这些教程将引导您完成设置 Azure 帐户和应用程序部署到 Azure 应用服务中的 Web 应用的过渡和生产的过程。 但是，可用于相同的基本过程部署到所选的第三方托管提供商。 在这些教程通过唯一进程转到 Azure 时，它们解释和建议时，会在第三方托管提供商有哪些不同。

## <a name="deploying-web-app-projects"></a>部署 web 应用程序项目

下载并部署这些教程的示例应用程序是一个 Visual Studio web 应用程序项目。 但是，如果安装最新[用于 Visual Studio Web 发布更新](https://msdn.microsoft.com/tr-tr/library/jj161045.aspx)，可以为 web 应用程序项目中使用相同的部署方法和工具。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 项目

示例应用程序是一个 ASP.NET Web 窗体项目，但了解如何执行的所有内容也适用于 ASP.NET MVC。 Visual Studio MVC 项目是另一种形式的 web 应用程序项目。 唯一的区别是，如果你正在部署到的宿主提供程序不支持 ASP.NET MVC 或它的目标版本，则必须确保已安装相应 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)， [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)或[MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) 在项目中的 NuGet 包。

## <a name="programming-language"></a>编程语言

示例应用程序使用 C#，但这些教程不需要的 C# 的知识和的教程所示的部署技术不是特定于语言的。

## <a name="database-deployment-methods"></a>数据库部署方法

有三种方法，可将部署 SQL Server 数据库和 Visual Studio 中的 web 部署：

- Entity Framework Code First 迁移
- DbDacFx Web 部署提供程序
- DbFullSql Web Deploy 提供程序

在本教程将使用这些方法的前两个。 DbFullSql Web Deploy 提供程序是不再建议除了某些特定情况下，例如从 SQL Server Compact 迁移到 SQL Server 的传统方法。

在本教程中所示的方法适用于 SQL Server 数据库，不 SQL Server Compact。 有关如何部署 SQL Server Compact 数据库的信息，请参阅[Visual Studio Web 部署使用 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。

在本教程中所示的方法都要求你使用 Web 部署发布方法。 如果希望其他发布方法，例如 FTP、 文件系统或 FPSE，请参阅[部署独立于 web 应用程序部署数据库](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate)for Visual Studio 和 ASP.NET Web 部署内容映射中。

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 迁移

在实体框架版本 4.3，Microsoft 引入了 Code First 迁移。 Code First 迁移会自动对数据模型进行增量更改并传播对数据库进行这些更改的过程。 在早期版本的代码优先，您通常让 Entity Framework 删除然后重新创建该数据库每次更改数据模型。 这不是开发中的问题，因为测试数据很轻松地重新创建，但在生产环境中通常需要更新数据库架构，而不删除数据库。 迁移功能，Code First 来更新数据库而无需删除并重新创建它。 您可以让代码优先自动决定如何进行所需的架构更改，或者可以编写自定义所做的更改的代码。 Code First 迁移的简介，请参阅[Code First 迁移](https://msdn.microsoft.com/library/hh770484.aspx)。

在部署 web 项目时，Visual Studio 可以自动执行部署的数据库中由 Code First 迁移的过程。 在创建发布配置文件时，选择一个复选框，将标记为执行 Code First 迁移 （应用程序启动时运行）。 此设置会导致部署过程会自动配置目标服务器上的应用程序 Web.config 文件，以便使用 Code First`MigrateDatabaseToLatestVersion`初始值设定项类。

Visual Studio 不会不执行任何操作与数据库在部署过程。 当部署的应用程序部署后首次访问数据库时，Code First 自动创建数据库或更新数据库架构到最新版本。 如果应用程序实现迁移 Seed 方法，该方法运行数据库创建或更新架构之后。

在本教程中，您将使用 Code First 迁移部署应用程序数据库。

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web 部署提供程序

对于不受 Entity Framework Code First 的 SQL Server 数据库，可以选择一个复选框，配置发布配置文件时，将标记更新数据库。 初始部署期间的 dbDacFx 提供程序在目标数据库以匹配源数据库中创建表和其他数据库对象。 在后续部署上的提供程序决定源和目标数据库之间的差异并更新目标数据库以匹配源数据库的架构。 默认情况下，该提供程序不会进行任何更改会导致数据丢失，例如当删除表或列。

此方法并不促使部署的数据库表中的数据，但可以创建脚本以执行此操作，并配置 Visual Studio 以在部署过程中运行。 在部署期间运行脚本的另一个原因是使架构更改，不能自动完成，因为它们可能会导致数据丢失。

在本教程中，您将使用 dbDacFx 提供程序以部署 ASP.NET 成员资格数据库。

## <a name="troubleshooting-during-this-tutorial"></a>在本教程过程故障排除

在部署期间，发生错误，或者如果已部署的站点不会正确运行的错误消息不始终提供最直接的解决方案。 若要通过一些常见的问题方案，帮助您[故障排除参考页](troubleshooting.md)可用。 如果收到错误消息或某些操作无法在完成教程，，请务必检查故障排除页。

## <a name="comments-welcome"></a>欢迎使用注释

对教程的注释很受欢迎，并且当教程更新时将进行每项工作要考虑到帐户更正或建议教程注释中提供的改进。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>系统必备

本教程专为以下产品：

- Windows 8 或 Windows 7。
- Visual Studio 2012 或 Visual Studio 2012 Express for Web[最新的更新](https://go.microsoft.com/fwlink/?LinkId=272486)。
- [用于 Visual Studio 2012 的 azure SDK](https://go.microsoft.com/fwlink/?LinkId=254364)

可以通过使用 Visual Studio 2010 SP1 或 Visual Studio 2013 中，按照本教程，但一些屏幕快照将会不同，某些功能将不同。

如果正在使用 Visual Studio 2013，安装[Azure SDK for Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkID=324322)。

如果您使用 Visual Studio 2010 SP1，安装以下软件：

- [用于 Visual Studio 2010 的 azure SDK](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx)。

具体取决于 SDK 依赖项数量的已在计算机上，安装 Azure SDK 可能耗时较长的时间，从几分钟到半小时或更多。 即使你打算将发布到第三方托管的提供程序而不是到 Azure，由于该 SDK 包括最新的更新到 Visual Studio web 发布功能需要 Azure SDK。

> [!NOTE]
> 本教程已用的 Azure sdk 版本 1.8.1 写入。 从那时起已经发布具有附加功能的较新版本。 已更新教程提及这些功能和对资源具有相关的详细信息的链接。


说明和屏幕截图都基于 Windows 8 中，但这些教程介绍适用于 Windows 7 的差异。

若要完成本教程中，要求一些其他软件，但无需使用，它尚未安装。 本教程将引导您完成在需要时安装它的步骤。

## <a name="download-the-sample-application"></a>下载示例应用程序

名为 Contoso University 并已为你创建将部署应用程序。 它是一个简化的版的大学网站上，基于松散 Contoso 大学应用程序中所述[ASP.NET 站点上的实体框架教程](https://asp.net/entity-framework/tutorials)。

安装必备组件后，下载[Contoso University web 应用程序](https://go.microsoft.com/fwlink/p/?LinkId=282627)。 *.Zip*文件包含多个版本的项目。 若要完成本教程的步骤，开始使用 C# 文件夹中的项目。 若要查看该项目的教程结束时的显示效果，请在 ContosoUniversity 端文件夹中打开项目。

若要准备通过教程中的步骤的工作项目，请执行以下步骤：

1. 从 C# 文件夹中名为 ContosoUniversity 用于使用 Visual Studio 项目的任何文件夹中的文件夹中保存为 ContosoUniversity 解决方案文件。

    默认情况下，这是 Visual Studio 2012 的以下文件夹：

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (对于本教程中的屏幕截图，项目文件夹位于根目录上`C`： 驱动器。)
2. 启动 Visual Studio 并打开该项目。
3. 在中**解决方案资源管理器**，右键单击该解决方案，然后单击**EnableNuGet 包还原**。
4. 生成解决方案。
5. 如果收到编译错误，手动还原 NuGet 包：

    1. 在中**解决方案资源管理器**，右键单击该解决方案，然后单击**为解决方案管理 NuGet 包**。
    2. 在顶部**管理 NuGet 包**对话框框中，将看到**是此解决方案中缺少某些 NuGet 包。单击此项可还原。** 单击**还原**按钮。
    3. 重新生成解决方案。
6. 按 CTRL-F5 运行该应用程序。

    应用程序将打开到 Contoso University 主页上。

    ![主页上开发](introduction/_static/image1.png)

    （虽然 Visual Studio 启动 SQL Server Express LocalDB 实例中，可能会等待时间和可能得到因超时错误的过程耗时太长。 在此情况下只需再次启动项目。）

网站页可从菜单栏访问，并让您执行以下功能：

- 显示学生统计信息 （关于页）。
- 显示、 编辑、 删除和添加学生。
- 显示和编辑课程。
- 显示和编辑讲师。
- 显示和编辑部门。

以下是几个有代表性的页面的屏幕快照。

![学生页面开发人员](introduction/_static/image2.png)

![添加学生页面开发人员](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>查看影响部署的应用程序功能

应用程序的以下功能会影响你部署的方式，或者您只需将其部署。 其中每项功能是在序列中的以下教程中详细地介绍您的问题。

- Contoso University 使用 SQL Server 数据库来存储应用程序数据，例如 student 和 instructor 名称。 数据库包含多个测试数据和生产数据，并在部署到生产环境时需要排除测试数据。
- 应用程序使用 ASP.NET 成员资格系统，用于在 SQL Server 数据库中存储的用户帐户信息。 应用程序定义的管理员用户有权访问某些受限制的信息。 需要部署成员资格数据库的测试帐户而不使用管理员帐户。
- 应用程序使用第三方错误日志记录和报告实用程序。 程序集必须与应用程序部署中提供了此实用程序。
- 错误日志记录实用程序将 XML 文件中错误的信息写入到文件文件夹中。 您必须确保 ASP.NET 下运行已部署站点中的帐户对此文件夹具有写权限，您必须从部署中排除此文件夹。 （否则为测试环境中的错误日志数据可能会部署到生产环境和/或生产错误日志文件可能被删除。）
- 该应用程序包括必须更改某些设置中部署*Web.config*具体取决于目标环境 （测试、 过渡或生产），具体取决于生成必须更改其他设置文件配置 （调试或发布）。
- Visual Studio 解决方案包括一个类库项目。 应该部署此项目生成的程序集，而不是项目本身。

## <a name="summary"></a>总结

在此系列中第一个教程中，已下载示例的 Visual Studio 项目并查看影响如何部署应用程序的网站功能。 在以下教程中，您为部署准备通过以下操作来自动处理的一些设置。 您可以手动处理的其他人。

> [!div class="step-by-step"]
> [下一篇](preparing-databases.md)
