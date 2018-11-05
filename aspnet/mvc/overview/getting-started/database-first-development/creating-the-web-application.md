---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 创建 Web 应用程序和数据模型 |Microsoft Docs
author: Rick-Anderson
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: riande
ms.date: 10/01/2014
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 6679b61326bd016481d96a4b5d58ec006f86b633
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020792"
---
<a name="ef-database-first-with-aspnet-mvc-creating-the-web-application-and-data-models"></a>第一种使用 ASP.NET MVC 的 EF 数据库： 创建 Web 应用程序和数据模型
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。
> 
> 本系列的此部分重点介绍创建 web 应用程序，并生成基于数据库表的数据模型。


## <a name="create-a-new-aspnet-web-application"></a>创建新的 ASP.NET Web 应用程序

在新的解决方案或与数据库项目相同的解决方案中，创建 Visual Studio 中的新项目，然后选择**ASP.NET Web 应用程序**模板。 将项目命名**ContosoSite**。

![创建项目](creating-the-web-application/_static/image1.png)

单击 **“确定”**。

在新建 ASP.NET 项目窗口中，选择**MVC**模板。 您可以清除**在云中托管**现在选项，因为你将部署到云的应用程序更高版本。 单击**确定**创建应用程序。

![选择 mvc 模板](creating-the-web-application/_static/image2.png)

使用默认文件和文件夹创建项目。

在本教程中，将使用 Entity Framework 6。 可以通过管理 NuGet 包窗口在项目中，请仔细检查 Entity Framework 的版本。 如果有必要，请更新你的实体框架版本。

![显示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>生成模型

现在将从数据库表创建实体框架模型。 这些模型是将用于处理的数据的类。 每个模型反映数据库中的表，并包含对应于表中的列的属性。

右键单击**模型**文件夹，然后选择**添加**并**新项**。

![添加新项](creating-the-web-application/_static/image4.png)

在添加新项窗口中，选择**数据**的左窗格中并**ADO.NET 实体数据模型**从中间窗格中的选项。 将新的模型文件**ContosoModel**。

![创建模型](creating-the-web-application/_static/image5.png)

单击 **添加**。

在实体数据模型向导中，选择**EF 设计器从数据库**。

![从数据库生成](creating-the-web-application/_static/image6.png)

单击 **“下一步”**。

如果必须在开发环境中定义的数据库连接，可能会看到其中一个预先选择这些连接。 但是，你想要创建新的连接到在本教程的第一部分创建的数据库。 单击**新的连接**按钮。

![连接到数据库](creating-the-web-application/_static/image7.png)

在连接属性窗口中，提供了创建数据库时所在的本地服务器的名称 (在这种情况下 **(localdb) \ProjectsV12**)。 提供服务器名称后, 从可用数据库中选择 ContosoUniversityData。

![设置连接属性](creating-the-web-application/_static/image8.png)

单击 **“确定”**。

此时将显示正确的连接属性。 可以在 Web.Config 文件中使用连接的默认名称

![连接设置](creating-the-web-application/_static/image9.png)

单击 **“下一步”**。

选择**表**来生成模型的所有三个表。

![选择表](creating-the-web-application/_static/image10.png)

单击 **“完成”**。

如果你收到一条安全警告，选择**确定**继续运行模板。

从数据库表生成模型和关系图显示，其中显示的属性和表之间的关系。

![模型的关系图](creating-the-web-application/_static/image11.png)

模型文件夹现在包括许多与从数据库生成的模型相关的新文件。

![显示新的模型文件](creating-the-web-application/_static/image12.png)

**ContosoModel.Context.cs**文件包含的类的派生自**DbContext**类，并提供了用于每个对应于数据库表的 model 类属性。 **Course.cs**， **Enrollment.cs**，并**Student.cs**文件包含表示数据库表的模型类。 使用基架时，将使用上下文类和模型类。

本教程前，生成项目。 在下一步部分中，将生成基于数据模型代码，但如果未生成项目，将无法工作部分。

> [!div class="step-by-step"]
> [上一页](setting-up-database.md)
> [下一页](generating-views.md)
