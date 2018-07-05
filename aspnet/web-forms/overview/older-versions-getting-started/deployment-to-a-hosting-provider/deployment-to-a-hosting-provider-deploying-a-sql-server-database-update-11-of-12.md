---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server 数据库更新-11 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 866c871026709a7cccee5fc1c0937120a031d997
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370932"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署 SQL Server 数据库更新-11 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示部署功能的 Visual Studio 2012 RC 发布后，显示了如何部署 SQL Server Compact 以外的 SQL Server 版本并演示如何将部署到 Windows Azure 网站的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

本教程演示如何将数据库更新部署到完整的 SQL Server 数据库。 因为 Code First 迁移更新数据库的所有工作，该过程是几乎与你为 SQL Server Compact 中所做[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>将新列添加到表

在本教程的此部分将使更改的数据库和相应的代码更改，然后将它们在准备部署到测试和生产环境中测试在 Visual Studio 中。 更改涉及到添加`OfficeHours`列添加到`Instructor`实体并显示中的新信息**讲师**网页。

在 ContosoUniversity.DAL 项目中，打开*Instructor.cs* ，并添加以下属性之间`HireDate`和`Courses`属性：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

更新初始值设定项类，使其使用测试数据的新列来设定种子。 打开*migrations\ configuration.cs*并将代码块的开始为`var instructors = new List<Instructor>`与下面的代码块，其中包括新列：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

在 ContosoUniversity 项目中，打开*Instructors.aspx*并为工作时间结束之前添加新的模板字段`</Columns>`在第一个标记`GridView`控件：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

生成解决方案。

打开**程序包管理器控制台**窗口中，并选择作为 ContosoUniversity.DAL**默认项目**。

输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

运行应用程序，并选择**讲师**页。 页面需要稍长的时间比平常要加载，因为实体框架将重新创建数据库并设定其种子使用测试数据。

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>数据库将更新部署到测试环境

当您使用 Code First 迁移时，用于将数据库更改部署到 SQL Server 的方法是与 SQL Server Compact 相同。 但是，您必须更改测试发布配置文件，因为它仍设置为从 SQL Server Compact 迁移到 SQL Server。

第一步是删除在上一教程中创建的连接字符串转换。 不再需要使用这些操作因为你将发布配置文件中，指定连接字符串转换就像你在配置之前**打包/发布 SQL**迁移到 SQL Server 的选项卡。

打开*Web.Test.config*文件，移除`connectionStrings`元素。 中的唯一剩余转换*Web.Test.config*文件的用处`Environment`中的值`appSettings`元素。

现在你可以更新的发布配置文件和发布到测试环境。

打开**发布 Web**向导，然后再切换到**配置文件**选项卡。

选择**测试**发布配置文件。

选择**设置**选项卡。

单击**启用新的数据库发布改进**。

在连接字符串中的**SchoolContext**，输入相同的值中使用*Web.Test.config*上一教程中的转换文件：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

选择**执行 Code First 迁移 （应用程序启动时运行）**。 (在你的 Visual Studio 版本，可能会标记为复选框**应用 Code First 迁移**。)

在连接字符串中的**DefaultConnection**，输入相同的值中使用*Web.Test.config*上一教程中的转换文件：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

将保留**更新数据库**清除。

单击“发布” 。

Visual Studio 将代码更改部署到测试环境和 Contoso University 主页上的浏览器中打开。

选择讲师页。

应用程序运行时此页，它尝试访问数据库。 Code First 迁移检查的数据库是最新，并查找有尚不已应用最新的迁移。 Code First 迁移应用最新的迁移，在运行`Seed`方法，然后页面会正常运行。 请参阅植入的数据的新工作时间列。

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>数据库将更新部署到生产环境

您必须还更改生产环境的发布配置文件。 在这种情况下将删除现有配置文件，并创建一个新的导入更新后的.publishsettings 文件。 更新后的文件将包括 Cytanium 上的 SQL Server 数据库的连接字符串。

如您所见到测试环境部署时，不再需要连接字符串中的转换*Web.Production.config*转换文件。 打开的文件，移除`connectionStrings`元素。 剩余的转换适用于`Environment`中的值`appSettings`元素和`location`Elmah 错误报告中限制访问的元素。

在创建新的发布配置文件用于生产之前，下载更新后的.publishsettings 文件中较早像的一样[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程。 (在 Cytanium 控件面板中，单击**网站**，然后单击**contosouniversity.com**网站。 选择**Web 发布**选项卡，然后依次**下载发布配置文件添加为此网站**。)您这样做的原因是要选取的.publishsettings 文件中的数据库连接字符串。 第一次下载该文件，因为还在使用 SQL Server Compact 和没有 SQL Server 数据库在 Cytanium 尚未创建，连接字符串不是可用。

现在你可以更新的发布配置文件和发布到生产环境。

打开**发布 Web**向导，然后再切换到**配置文件**选项卡。

单击**管理配置文件**，然后删除生产配置文件。

关闭**发布 Web**向导以保存此更改。

打开**发布 Web**同样，向导，然后单击**导入**。

上**连接**选项卡上，更改**目标 URL**为适当的值，如果您使用的临时的 URL。

单击 **“下一步”**。

上**设置**选项卡上，单击**启用新的数据库发布改进**。

中的连接字符串下拉列表**SchoolContext**，选择 Cytanium 连接字符串。

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

选择**执行 Code First 迁移 （应用程序启动时运行）**。

中的连接字符串下拉列表**DefaultConnection**，选择 Cytanium 连接字符串。

选择**配置文件**选项卡上，单击**管理配置文件**，并将该配置文件重命名从"contosouniversity.com-Web 部署"，为"生产"。

关闭发布配置文件以保存更改，然后重新打开它。

单击“发布” 。 (对于实际的生产网站，会将复制*应用程序\_offline.htm*到生产环境并将置于前视情况下，项目文件夹中它然后将其删除部署完成后。)

Visual Studio 将代码更改部署到测试环境和 Contoso University 主页上的浏览器中打开。

选择讲师页。

Code First 迁移更新数据库像在测试环境中的相同方法。 请参阅植入的数据的新工作时间列。

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

你现在已成功部署应用程序更新的包含数据库更改，使用 SQL Server 数据库。

## <a name="more-information"></a>详细信息

这样就完成这一系列的教程，介绍 ASP.NET web 应用程序部署到第三方托管提供商。 任何在这些教程中所涉及的主题的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)MSDN 网站上。

## <a name="acknowledgements"></a>致谢

我想要感谢下列人员进行本系列教程的内容的重要贡献的人：

- [Alberto Poblacion、 MVP &amp; MCT、 西班牙](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson，数据平台开发 MVP，美国
- Harsh Mittal，Microsoft
- [Kristina Olson Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike 教皇 Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava Microsoft
- [Raffaele Rialdi，意大利](http://www.iamraf.net/)
- [Rick Anderson Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi、 Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))
- [Scott Hunter、 Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))
- [Srđan Božović，塞尔维亚共和国](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi、 Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
