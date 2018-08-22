---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署数据库更新-9 12 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的 SQL Server Compact 数据库使用包含的 Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: b15d27a07207110187b897624814125c9e030493
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830478"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>使用 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer 将 ASP.NET Web 应用程序部署： 部署数据库更新-9 12
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程演示如何将部署 （发布） ASP.NET web 应用程序项目的情况下使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 数据库。 如果在安装 Web 发布更新，还可以使用 Visual Studio 2010。 该系列的简介，请参阅[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 显示了 Visual Studio 2012 RC 版后引入的部署功能，演示如何部署 SQL Server Compact 以外的 SQL Server 版本并显示了如何将部署到 Azure 应用服务 Web 应用的教程，请参阅[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。


## <a name="overview"></a>概述

在本教程中，将生成数据库更改和相关的代码的更改，在 Visual Studio 中，测试所做的更改，然后将更新部署到测试和生产环境。

提醒： 如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>将新列添加到表

在本部分中，您将添加到的出生日期列`Person`的基类`Student`和`Instructor`实体。 然后更新，以便它将显示新的列显示讲师数据的页面。

在中*ContosoUniversity.DAL*项目中，打开*Person.cs* ，并在末尾添加以下属性`Person`类 （应两个右大括号后面）：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

接下来，更新 Seed 方法，以便它向新列提供值。 打开*migrations\ configuration.cs*并将代码块的开始为`var instructors = new List<Instructor>`与下面的代码块，其中包括出生日期信息：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

在 ContosoUniversity 项目中，打开*Instructors.aspx*并添加新的模板字段来显示出生日期。 将其添加之间雇佣日期和 office 分配的：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

（如果代码缩进进行同步，你可以按 CTRL-K，然后选择 CTRL-D 以便自动重新格式化该文件。）

生成解决方案，然后打开**程序包管理器控制台**窗口。 请确保 ContosoUniversity.DAL 仍处于选中状态作为**默认项目**。

在中**程序包管理器控制台**窗口中，选择**ContosoUniversity.DAL**作为**默认项目**，然后输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`类，然后在`Up`方法您可以看到创建的新列的代码。

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

生成解决方案，并输入以下命令中的**程序包管理器控制台**窗口 （请确保 ContosoUniversity.DAL 项目仍处于选中状态）：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

此命令完成后，运行该应用程序，并选择讲师页。 当页面加载时，您看到它有新的出生日期字段。

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>数据库将更新部署到测试环境

在中**解决方案资源管理器**选择 ContosoUniversity 项目。

在中**Web 单键发布**工具栏中，选择**测试**发布配置文件，然后依次**发布 Web**。 (如果禁用工具栏，则选择中的 ContosoUniversity 项目**解决方案资源管理器**。)

Visual Studio 将部署更新的应用程序，并在浏览器打开到主页页面。 运行讲师页以验证已成功部署更新。 当应用程序尝试访问此页的数据库时，Code First，更新数据库架构，并运行`Seed`方法。 显示页时，您看到的预期**出生日期**中它的日期的列。

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>数据库将更新部署到生产环境

你现在可以部署到生产环境。 唯一的区别是，将使用*应用程序\_offline.htm*以防止用户访问站点并因此更新数据库时要部署的更改。 对于生产部署中，执行以下步骤：

- 上传*应用程序\_offline.htm*到生产站点的文件。
- 在 Visual Studio 中，选择中的生产配置文件**Web 单键发布**工具栏，然后单击**发布 Web**。
- 删除*应用程序\_offline.htm*生产站点中的文件。

> [!NOTE]
> 在生产环境中使用你的应用程序时，应实施备份计划。 也就是说，你应将定期复制*学校 Prod.sdf*并*aspnet Prod.sdf*文件从生产站点到安全存储位置，并应会保持此类的多个代备份。 更新数据库时，应进行更改之前立即从备份副本。 然后，如果您有误并部署到生产环境后不发现它之前，您将仍将能够将数据库恢复到其损坏之前的状态。


当 Visual Studio 在浏览器中打开主页 URL*应用程序\_offline.htm*显示页。 删除后*应用程序\_offline.htm*文件中，您可以浏览到您的主页上，以验证已成功部署更新。

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

现在，你已部署包含对测试和生产的数据库更改的应用程序更新。 下一步的教程演示如何从 SQL Server Compact 将数据库迁移到 SQL Server Express 和 SQL Server。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
