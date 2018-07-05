---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 部署具有 SQL Server Compact 使用 Visual Studio 的 ASP.NET Web 应用程序： 简介-1 的 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: 4a790fa72568caafdb2fab5efd9f334919c23719
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398266"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>部署具有 SQL Server Compact 使用 Visual Studio 的 ASP.NET Web 应用程序： 简介-1 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。
> 
> 这些教程将指导你完成第一次部署到用于测试，在本地开发计算机上的 IIS，再到第三方托管提供商。 将部署的应用程序使用的应用程序数据库和 ASP.NET 成员资格数据库。 开始使用 SQL Server Compact 和部署到 SQL Server Compact 和更高版本的教程介绍了如何将数据库更改部署以及如何迁移到 SQL Server。
> 
> 这些教程假定您知道如何使用 Visual Studio 中的 ASP.NET。 如果不这样做，是一个良好起点[基本的 ASP.NET Web 窗体教程](../tailspin-spyworks/tailspin-spyworks-part-1.md)或[基本的 ASP.NET MVC 教程](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)。
> 
> 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET 部署论坛](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)。


## <a name="overview"></a>概述

这些教程将指导你完成第一次部署到用于测试，在本地开发计算机上的 IIS，再到第三方托管提供商。 将部署的应用程序使用的应用程序数据库和 ASP.NET 成员资格数据库。 开始使用 SQL Server Compact 和部署到 SQL Server Compact 和更高版本的教程介绍了如何将数据库更改部署以及如何迁移到 SQL Server。

数的教程 – 在所有 11 以及故障排除页 – 可能会使部署过程令人望而生畏。 实际上，部署站点的基本过程构成了相对较小教程系列的一部分。 但是，在实际情况下，您通常需要部署的一些小的但很重要的额外方面有关的信息 — 例如，在目标服务器上设置文件夹权限。 我们在教程中，使用这些教程省略一些可能会阻止您成功部署实际的应用程序的信息，不希望包含的许多其他技术。

教程设计为在序列中，运行并在前一部分生成的每个部分。 但是，可以跳过不到您的具体情况相关的部分。 （跳过部分可能会要求你在后续教程中调整这些过程。）

## <a name="intended-audience"></a>目标的受众

本教程旨在 ASP.NET 开发人员在小型组织或其他环境中工作的：

- 不使用持续集成过程 （自动的生成和部署）。
- 在生产环境是第三方托管提供商。
- 一个人通常会充当多个角色 （同一人开发，测试，并部署）。

在企业环境中更常见的以实现持续集成过程，并通过公司自己的服务器通常托管在生产环境。 不同的人通常还会执行不同的角色。 有关企业部署的信息，请参阅[企业方案中部署 Web 应用程序](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。

各种规模的组织还可以部署 web 应用程序到 Azure，并在这些教程中所示的过程的大多数还适用于 Azure 应用服务 Web 应用。 有关 Azure 的简介，请参阅[ https://azure.microsoft.com ](https://azure.microsoft.com)。

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>在教程中所示的宿主提供程序

这些教程将引导您完成设置具有托管公司的帐户和应用程序部署到该宿主提供程序的过程。 特定的托管公司选择是为了让这些教程无法说明部署到实时网站的完整的体验。 每个托管公司提供不同的功能，并将部署到他们的服务器的体验不同而异某种程度上;但是，在本教程中所述的过程是典型的整个过程。

用于本教程中，Cytanium.com，宿主提供程序是一个许多可用，并在本教程中的使用它不构成认可或推荐。

## <a name="deploying-web-site-projects"></a>部署网站项目

Contoso University 是 Visual Studio web 应用程序项目。 大多数部署方法和本教程中演示的工具不适用于[网站项目](https://msdn.microsoft.com/library/dd547590.aspx)。 有关如何部署网站项目的信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 项目

本教程中部署 ASP.NET Web 窗体项目，但了解如何执行的所有内容也适用于 ASP.NET MVC。 Visual Studio MVC 项目是另一种形式的 web 应用程序项目。 唯一的区别是，如果你正在部署到的宿主提供程序不支持 ASP.NET MVC 或它的目标版本，则必须确保已安装相应 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)或[MVC 4](http://nuget.org/packages/aspnetmvc)) 在项目中的 NuGet 包。

## <a name="programming-language"></a>编程语言

示例应用程序使用 C#，但这些教程不需要的 C# 的知识和的教程所示的部署技术不是特定于语言的。

## <a name="troubleshooting-during-this-tutorial"></a>在本教程过程故障排除

在部署期间，发生错误，或者如果已部署的站点不会正确运行的错误消息不始终提供一种解决方案。 若要通过一些常见的问题方案，帮助您[故障排除参考页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)可用。 如果收到错误消息或某些操作无法在完成教程，，请务必检查故障排除页。

## <a name="comments-welcome"></a>注释欢迎

对教程的注释很受欢迎，并且当教程更新时将进行每项工作要考虑到帐户更正或建议教程注释中提供的改进。

## <a name="prerequisites"></a>系统必备

在开始之前，请确保你有 Windows 7 或更高版本，并且您的计算机上安装以下产品之一：

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer 速成版 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web](https://go.microsoft.com/fwlink/?LinkId=240162)

如果你有 Visual Studio 2010 SP1 或 Visual Web Developer 速成版 2010 SP1，也安装以下产品：

- [Azure SDK for.NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) （包括 Web 发布更新）
- [Microsoft Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

为完成本教程中，需要一些其他软件，但不需要具有尚未加载的。 本教程将引导您完成在需要时安装它的步骤。

## <a name="downloading-the-sample-application"></a>下载示例应用程序

将部署应用程序名为 Contoso University 并已为你创建。 它是一个简化的版的大学网站上，基于松散 Contoso 大学应用程序中所述[ASP.NET 站点上的实体框架教程](https://asp.net/entity-framework/tutorials)。

安装必备组件后，下载[Contoso University web 应用程序](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)。 *.Zip*文件包含多个版本的项目和包含所有的 12 本教程的 PDF 文件。 若要完成本教程的步骤，开始为 ContosoUniversity 开始。 若要查看项目的教程结束时的显示效果，请打开 ContosoUniversity 结束。 若要查看该项目之前迁移到完整的 SQL Server 教程 10 中的显示效果，打开 ContosoUniversity AfterTutorial09。

若要准备用于演练教程中的步骤，将保存到用于处理 Visual Studio 项目使用任何文件夹的 ContosoUniversity Begin。 默认情况下，这是以下文件夹：

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(对于本教程中的屏幕截图，项目文件夹位于根目录上`C`： 驱动器。)

启动 Visual Studio 中，打开项目，并按 CTRL-F5 来运行它。

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

网站页可从菜单栏访问，并让您执行以下功能：

- 显示学生统计信息 （关于页）。
- 显示、 编辑、 删除和添加学生。
- 显示和编辑课程。
- 显示和编辑讲师。
- 显示和编辑部门。

以下是几个有代表性的页面的屏幕快照。

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>查看影响部署的应用程序功能

应用程序的以下功能会影响你部署的方式，或者您只需将其部署。 其中每项功能是在序列中的以下教程中详细地介绍您的问题。

- Contoso University 使用 SQL Server Compact 数据库来存储应用程序数据，例如 student 和 instructor 名称。 数据库包含多个测试数据和生产数据，并在部署到生产环境时需要排除测试数据。 在系列教程中稍后你将从迁移 SQL Server Compact 到 SQL Server。
- 应用程序使用 ASP.NET 成员资格系统，用于在 SQL Server Compact 数据库中存储的用户帐户信息。 应用程序定义的管理员用户有权访问某些受限制的信息。 需要部署成员资格数据库的测试帐户使用而非一个管理员帐户。
- 因为应用程序数据库和成员资格数据库则使用 SQL Server Compact 作为数据库引擎，必须将部署到托管提供商，以及数据库自身的数据库引擎。
- 应用程序使用 ASP.NET 通用成员资格提供程序，以便成员资格系统可以将其数据存储在 SQL Server Compact 数据库中。 包含通用成员资格提供程序的程序集必须与应用程序部署。
- 应用程序使用 Entity Framework 5.0 访问应用程序数据库中的数据。 包含实体框架 5.0 的程序集必须与应用程序部署。
- 应用程序使用第三方错误日志记录和报告实用程序。 程序集必须与应用程序部署中提供了此实用程序。
- 错误日志记录实用程序将 XML 文件中错误的信息写入到文件文件夹中。 您必须确保 ASP.NET 下运行已部署站点中的帐户对此文件夹具有写权限，您必须从部署中排除此文件夹。 （否则为测试环境中的错误日志数据可能会部署到生产环境和/或生产错误日志文件可能被删除。）
- 该应用程序包括必须更改某些设置中部署*Web.config*具体取决于目标环境 （测试或生产），具体取决于生成必须更改其他设置文件配置 （调试或发布）。
- Visual Studio 解决方案包括一个类库项目。 应该部署此项目生成的程序集，而不是项目本身。

在此系列中第一个教程中，已下载示例的 Visual Studio 项目并查看影响如何部署应用程序的网站功能。 在以下教程中，您为部署准备通过以下操作来自动处理的一些设置。 您可以手动处理的其他人。

> [!div class="step-by-step"]
> [下一篇](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
