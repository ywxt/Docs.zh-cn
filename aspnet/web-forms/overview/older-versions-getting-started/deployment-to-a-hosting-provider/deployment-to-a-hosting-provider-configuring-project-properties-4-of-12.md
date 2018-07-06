---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 配置项目属性-4 个 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: cb496c31ba09030087180ac67647c8c0854c372b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814192"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 配置项目属性-4 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

在项目文件中存储的项目属性中配置一些部署选项 ( *.csproj*或 *.vbproj*文件)。 在大多数情况下，这些设置的默认值是您的需要，但你可以使用**项目属性**UI 内置到 Visual Studio 以使用这些设置，如果需要更改它们。 在本教程中查看中的部署设置**项目属性**。 你还创建会导致要部署的空文件夹的占位符文件。

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>在项目属性窗口中配置部署设置

会影响部署过程中发生的大多数设置包含在发布配置文件，您将看到以下教程。 您应注意的几个设置位于**打包/发布**选项卡**项目属性**窗口。 每个生成配置指定这些设置，即具有不同的设置发布版本不是必须的调试版本。

在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，选择**属性**，然后选择**打包/发布 Web**选项卡。

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

当显示窗口时，则默认为显示设置的任何生成配置当前处于活动状态的解决方案。 如果**配置**框中并不表示**处于活动状态 （发布）**，选择**版本**以显示发布生成配置设置。 你将部署到您的测试和生产环境的发布版本。

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

与**处于活动状态 （发布）** 或**发行**选择，请参阅部署使用发布生成配置时有效的值：

- 在中**要部署的项**框中，**仅运行该应用程序所需的文件**处于选中状态。 其他选项包括**此项目中的所有文件**或**此项目文件夹中的所有文件**。 通过保留默认选择保持不变，避免部署源代码文件，例如。 此设置是为何包含 SQL Server Compact 的二进制文件的文件夹必须包含在项目的原因。 有关此设置的详细信息，请参阅**为什么不所有我的项目文件夹中的文件进行部署？** 中[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx)。
- **排除生成调试符号**处于选中状态。 您不会使用此生成配置时调试。
- **将应用程序中排除文件\_数据文件夹**未选中。 用于成员资格数据库的 SQL Server Compact 文件是在该文件夹中，您必须将其部署。 在部署更新，其中不包括数据库更改时，将选中此复选框。
- **预编译此应用程序发布前的**未选中。 在大多数情况下，没有必要预编译 web 应用程序项目。 有关此选项的详细信息，请参阅[项目属性打包/发布 Web 选项卡](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx)并[高级预编译设置对话框](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)。
- **包括在打包/发布 SQL 选项卡中配置的所有数据库**选择，则此选项没有任何影响现在因为未配置，但**打包/发布 SQL**选项卡。该选项卡适用于要部署的 SQL Server 数据库的唯一选项使用的旧数据库部署方法。 将使用**打包/发布 SQL**选项卡[迁移到 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)教程。
- **Web 部署包设置**部分不适用于正在使用单击一次，因此在这些教程中发布。

更改**配置**下拉列表框中为调试若要查看默认设置的调试版本。 值都相同，除了**排除生成的调试符号**被清除，以便您可以调试时部署的调试版本。

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>从而确保 Elmah 文件夹获取部署

与在上一教程中看到[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)提供的错误日志记录和报告功能。 Contoso University 应用程序中 Elmah 已配置为将错误详细信息存储在名为的文件夹*Elmah*:

![Elmah 文件夹](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

从部署中排除特定文件或文件夹是一个常见要求;另一个示例是用户可以上传到文件的文件夹。 您不希望日志文件或上传到开发环境部署到生产环境中创建的文件。 而如果您要更新部署到生产环境不希望部署过程，删除在生产环境中存在的文件。 （具体取决于如何设置部署选项，如果在目标站点，但不是在源站点中存在的文件在部署时，Web 部署将其删除从目标。）

在本教程前面所示**要部署的项**选项**打包/发布 Web**选项卡设置为**只需运行此应用程序文件**。 因此，在开发过程中创建的 Elmah 的日志文件将不部署，这是你想要发生这种情况。 (若要部署，它们必须包含在项目及其**生成操作**属性必须设置为**内容**。 有关详细信息，请参阅**为什么不所有我的项目文件夹中的文件进行部署？** 中[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx))。 但是，Web 部署不会创建一个文件夹在目标站点中除非存在至少一个文件复制到它。 因此，你将添加 *.txt*要充当占位符，以便将复制该文件夹的文件夹的文件。

在中**解决方案资源管理器**，右键单击*Elmah*文件夹，选择**添加新项**，并创建名为的文件*Placeholder.txt*。 将以下文本放入该:"这是一个占位符文件，以确保获取部署在文件夹"。 并保存文件。 这就是您只需这样可确保 Visual Studio 部署此文件和文件夹中，是因为一切**生成操作**的属性 *.txt*文件设置为**内容**默认情况下。

现在已完成的所有部署设置任务。 在下一步的教程中，将部署到测试环境的 Contoso 大学站点，并对其进行测试。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
