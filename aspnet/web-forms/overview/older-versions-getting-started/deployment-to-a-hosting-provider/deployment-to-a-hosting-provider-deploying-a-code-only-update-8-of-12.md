---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 Code-Only 更新-8 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: 39075d2e979076f88200ea595c92f95f38f35911
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374008"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 Code-Only 更新-8 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

在初始部署后持续维护和开发您的网站的工作，并在长时间之前你将想要将更新部署。 本教程将指导你完成更新部署到应用程序代码的过程。 此更新不涉及数据库更改;您将看到有关部署下一教程中的数据库更改的差异。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="making-a-code-change"></a>进行代码更改

作为对应用程序更新的简单示例，你将添加到**讲师**页由所选讲师的课程列表。

如果在运行**讲师**页上，您会注意到，有**选择**链接在网格中，但他们不使以外的任何行背景变灰。

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

现在，你将添加代码运行时**选择**链接单击，并显示由所选讲师的课程列表。

在中*Instructors.aspx*，添加以下标记后立即**ErrorMessageLabel** `Label`控件：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

运行该页并选择讲师。 请参阅由讲师讲授的课程列表。

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>代码将更新部署到测试环境

部署到测试环境很简单，只需单击一次运行的重新发布。 若要使此过程更快，可以使用**Web 单键发布**工具栏。

在中**视图**菜单中，选择**工具栏**，然后选择**Web 单键发布**。

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

在中**解决方案资源管理器**，选择 ContosoUniversity 项目。

**Web 单键发布**工具栏上，选择**测试**发布配置文件，然后单击**发布 Web** （其箭头指向左侧和右侧的图标）。

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio 部署更新的应用程序，并在主页上会自动打开浏览器。 运行讲师页并选择一名讲师，若要验证已成功部署更新。

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

通常会同样进行回归测试 （也就是说，测试以确保新的更改不会破坏任何现有功能的站点的其余部分）。 但对于本教程将跳过该步骤并继续将更新部署到生产环境。

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>阻止重新部署到生产环境的初始数据库状态

在实际的应用程序，用户在初始部署之后与您的生产站点和数据库填充了实时数据。 因此，您不想要重新部署成员资格数据库中所有的实时数据会擦除其初始状态。 由于 SQL Server Compact 数据库中的文件*应用程序\_数据*文件夹中，您必须防止出现这种通过更改部署设置，因此，中的文件*应用\_数据*文件夹不被部署。

打开**项目属性**ContosoUniversity 项目，然后选择窗口**打包/发布 Web**选项卡。请确保**配置**下拉列表框已**处于活动状态 （发布）** 或**版本**选择，选择**将应用程序中排除文件\_数据文件夹**。

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

如果你决定在将来部署的调试版本，它最好进行调试生成配置的相同的更改： 更改**配置**到**调试**，然后选择**排除应用程序中的文件\_数据文件夹**。

保存并关闭**打包/发布 Web**选项卡。

> [!NOTE] 
> 
> [!IMPORTANT]
> 请确保不会**删除目标处的其他文件**选择发布配置文件中。 如果选择该选项时，部署过程将删除的数据库的应用中有\_中的数据已部署的站点，以及它将删除应用\_数据文件夹本身。


## <a name="preventing-user-access-to-the-production-site-during-update"></a>到生产站点更新的过程中阻止用户访问权限

要部署的更改现在是单个页面的简单更改。 但有时部署较大的更改，并在这种情况下该站点可以出现异常行为如果之前部署完成后，用户请求页面。 若要防止此情况，可以使用*应用程序\_offline.htm*文件。 当将名为的文件*应用程序\_offline.htm*在你的应用程序的根文件夹中，IIS 会自动显示该文件而不是运行你的应用程序。 因此为了防止访问在部署期间，您将放*应用程序\_offline.htm*根文件夹中运行部署过程中，，然后删除*应用\_offline.htm*。

在中**解决方案资源管理器**，右键单击该解决方案 （而不是项目的），然后选择**新解决方案文件夹**。

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

将文件夹命名为*SolutionFiles*。

在新文件夹中创建名为的 HTML 页*应用程序\_offline.htm*。 现有内容替换为以下标记：

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

可以将复制*应用程序\_offline.htm*通过使用 FTP 连接的站点的文件或**文件管理器**实用工具托管提供商的控制面板中。 对于本教程中，你将使用**文件管理器**。

打开控制面板，然后选择**文件管理器**中那样[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。 选择**contosouniversity.com** ，然后**wwwroot**以获取应用程序的根文件夹，然后单击**上载**。

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

在中**上传文件**对话框中，选择*应用\_offline.htm*文件，然后单击**上载**。

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

浏览到你网站的 URL。 可以看到*应用程序\_offline.htm*页现在显示而不是您的主页。

[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

现在你现可部署到生产环境。

## <a name="deploying-the-code-update-to-the-production-environment"></a>代码将更新部署到生产环境

在中**Web 单键发布**工具栏上，选择**生产**发布配置文件，然后单击**发布 Web**。

Visual Studio 部署更新的应用程序和网站的主页上浏览器中打开。 *应用程序\_offline.htm*显示文件。 您可以对其进行测试以验证是否成功的部署之前，必须删除*应用程序\_offline.htm*文件。

返回到**文件管理器**控制面板中的应用程序。 选择**contosouniversity.com**并**wwwroot**，选择**应用\_offline.htm**，然后单击**删除**。

[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

在浏览器中，在公共网站中，打开讲师页并选择讲师来验证已成功部署更新。

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

现在，你已部署不涉及数据库更改的应用程序更新。 下一步的教程演示了如何部署数据库更改。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
