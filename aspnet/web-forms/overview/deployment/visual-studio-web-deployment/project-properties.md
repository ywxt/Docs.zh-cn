---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 使用 Visual Studio 的 ASP.NET Web 部署： 项目属性 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: aspnetcontent
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: 86e4e3ef5f126a5bf8abc91c2d5ce3d14b1e1c6c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837660"
---
<a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>使用 Visual Studio 的 ASP.NET Web 部署： 项目属性
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。 有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。


## <a name="overview"></a>概述

在项目文件中存储的项目属性中配置一些部署选项 ( *.csproj*或 *.vbproj*文件)。 在大多数情况下，这些设置的默认值是您的需要，但你可以使用**项目属性**UI 内置到 Visual Studio 以使用这些设置，如果需要更改它们。 在本教程中查看中的部署设置**项目属性**。 你还创建会导致要部署的空文件夹的占位符文件。

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>在项目属性窗口中配置部署设置

会影响部署过程中发生的大多数设置包含在发布配置文件，您将看到以下教程。 您应注意的几个设置位于**打包/发布**选项卡**项目属性**窗口。 每个生成配置指定这些设置，即具有不同的设置发布版本不是必须的调试版本。

在中**解决方案资源管理器**，右键单击**ContosoUniversity**项目，选择**属性**，然后选择**打包/发布 Web**选项卡。

![“打包/发布 Web”选项卡](project-properties/_static/image1.png)

当显示窗口时，则默认为显示设置的任何生成配置当前处于活动状态的解决方案。 如果**配置**框中并不表示**处于活动状态 （发布）**，选择**版本**以显示发布生成配置设置。 你将部署到您的测试和生产环境的发布版本。

![选择发布生成配置](project-properties/_static/image2.png)

与**处于活动状态 （发布）** 或**发行**选择，请参阅部署使用发布生成配置时有效的值：

- 在中**要部署的项**框中，**仅运行该应用程序所需的文件**处于选中状态。 其他选项包括**此项目中的所有文件**或**此项目文件夹中的所有文件**。 通过保留默认选择保持不变，避免部署源代码文件，例如。 此设置是为何包含 SQL Server Compact 的二进制文件的文件夹必须包含在项目的原因。 有关此设置的详细信息，请参阅**为什么不所有我的项目文件夹中的文件进行部署？** 中[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx)。
- **排除生成调试符号**处于选中状态。 您不会使用此生成配置时调试。
- **包括在打包/发布 SQL 选项卡中配置的所有数据库**处于选中状态。 指定 Visual Studio 将部署的数据库以及文件。 尽管复选框标签仅提及**打包/发布 SQL**选项卡上，清除此复选框将还禁用的发布配置文件中配置的数据库部署。 你将执行的更高版本，因此必须选中复选框。 **打包/发布 SQL**选项卡上用于发布方法不会在这些教程中使用的旧数据库。
- **Web 部署包设置**部分不适用于正在使用单击一次，因此在这些教程中发布。

更改**配置**下拉列表框中为调试若要查看默认设置的调试版本。 值都相同，除了**排除生成的调试符号**被清除，以便您可以调试时部署的调试版本。

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>请确保 Elmah 文件夹获取部署

与在上一教程中看到[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)提供的错误日志记录和报告功能。 Contoso University 应用程序中 Elmah 已配置为将错误详细信息存储在名为的文件夹*Elmah*:

![Elmah 文件夹](project-properties/_static/image3.png)

从部署中排除特定文件或文件夹是一个常见要求;另一个示例是用户可以上传到文件的文件夹。 您不希望日志文件或上传到开发环境部署到生产环境中创建的文件。 而如果您要更新部署到生产环境不希望部署过程，删除在生产环境中存在的文件。 （具体取决于如何设置部署选项，如果在目标站点，但不是在源站点中存在的文件在部署时，Web 部署将其删除从目标。）

在本教程前面所示**要部署的项**选项**打包/发布 Web**选项卡设置为**只需运行此应用程序文件**。 因此，在开发过程中创建的 Elmah 的日志文件将不部署，这是你想要发生这种情况。 (若要部署，它们必须包含在项目及其**生成操作**属性必须设置为**内容**。 有关详细信息，请参阅**为什么不所有我的项目文件夹中的文件进行部署？** 中[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx))。 但是，Web 部署不会创建一个文件夹在目标站点中除非存在至少一个文件复制到它。 因此，你将添加 *.txt*要充当占位符，以便将复制该文件夹的文件夹的文件。

在中**解决方案资源管理器**，右键单击*Elmah*文件夹，选择**添加新项**，并创建一个名为文本文件*Placeholder.txt*。 将以下文本放入该:"这是一个占位符文件，以确保获取部署在文件夹"。 并保存文件。 这就是您只需这样可确保 Visual Studio 部署此文件和文件夹中，是因为一切**生成操作**的属性 *.txt*文件设置为**内容**默认情况下。

## <a name="summary"></a>总结

现在已完成的所有部署设置任务。 在下一步的教程中，将部署到测试环境的 Contoso 大学站点，并对其进行测试。

> [!div class="step-by-step"]
> [上一页](web-config-transformations.md)
> [下一页](deploying-to-iis.md)
