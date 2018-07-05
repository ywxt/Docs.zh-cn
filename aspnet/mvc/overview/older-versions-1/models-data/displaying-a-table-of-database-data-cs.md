---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表 (C#) |Microsoft Docs
author: microsoft
description: 在本教程中，我将演示两种方法显示的一组数据库记录。 我将介绍两种方法的格式设置的一组数据库记录在 HTML ta...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 06dc5c9398adb45d5a5ff8f57ff42816c983ee04
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395975"
---
<a name="displaying-a-table-of-database-data-c"></a>显示数据库数据表 (C#)
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> 在本教程中，我将演示两种方法显示的一组数据库记录。 我将介绍两种方法的格式设置的一组 HTML 表中的数据库记录。 首先，我介绍如何设置格式直接在视图中的数据库记录。 接下来，我演示了如何可以充分利用分区，设置格式的数据库记录时。


本教程的目的是说明如何在 ASP.NET MVC 应用程序中显示一个 HTML 表的数据库数据。 首先，您将学习如何使用 Visual Studio 中包含的基架工具生成一个视图，它会自动显示的一组记录。 接下来，您将学习如何设置格式的数据库记录时将用作模板的部分。

## <a name="create-the-model-classes"></a>创建模型类

我们要显示的电影数据库表中的记录集。 电影数据库表包含以下列：

<a id="0.3_table01"></a>


| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(200) | False |
| 主管 | Nvarchar （50) | False |
| DateReleased | DateTime | False |


若要表示电影表在 ASP.NET MVC 应用程序中，我们需要创建一个模型的类。 在本教程中，我们可以使用 Microsoft Entity Framework 创建我们模型类。

> [!NOTE] 
> 
> 在本教程中，我们使用 Microsoft Entity Framework。 但是，务必了解你可以使用各种不同的技术与 ASP.NET MVC 应用程序包括 LINQ to SQL、 NHibernate 或 ADO.NET 从数据库进行交互。


请按照下列步骤以启动实体数据模型向导：

1. 右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。
2. 选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。
3. 为你的数据模型提供名称*MoviesDBModel.edmx*然后单击**添加**按钮。

单击添加按钮后，会显示实体数据模型向导 （参见图 1）。 请按照下列步骤以完成向导：

1. 在中**选择模型内容**步骤中，选择**从数据库生成**选项。
2. 在中**选择数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*的连接设置。 单击**下一步**按钮。
3. 在中**选择数据库对象**步骤中，展开表节点中，选择电影表。 输入的命名空间*模型*然后单击**完成**按钮。


[![创建 LINQ to SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**图 01**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image2.png))


完成实体数据模型向导后，会打开实体数据模型设计器。 在设计器应显示电影实体 （请参见图 2）。


[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**图 02**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image4.png))


我们需要做出一项更改，然后我们继续。 实体数据向导生成一个名为的模型类*电影*表示电影数据库表。 由于我们将使用电影类来表示特定电影，我们需要修改这个类为名称*电影*而不是*电影*（单数而非复数形式）。

双击设计器图面上的类的名称并将影片中的类的名称更改为电影。 此更改后，单击**保存**按钮 （软盘图标） 以生成电影类。

## <a name="create-the-movies-controller"></a>创建电影控制器

现在，我们已有一种方法来表示我们的数据库记录，我们可以创建一个控制器，返回的电影集合。 在 Visual Studio 解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**（参见图 3）。


[![添加控制器菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**图 03**: 添加的控制器菜单 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image6.png))


当**添加控制器**对话框出现时，输入控制器名称 MovieController （请参阅图 4）。 单击**添加**按钮以添加新控制器。


[![添加控制器对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**图 04**: 添加控制器对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image8.png))


我们需要进行修改，以便其返回的数据库记录集公开的电影控制器的 index （） 操作。 修改控制器，使它看起来像列表 1 中的控制器。

**代码清单 1 – Controllers\MovieController.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

在列表 1 中，MoviesDBEntities 类用于表示 MoviesDB 数据库。 若要使用此类，需要导入如下 MvcApplication1.Models 命名空间：

使用 MvcApplication1.Models;

表达式*实体。MovieSet.ToList()* 从电影数据库表返回所有电影的组。

## <a name="create-the-view"></a>创建视图

若要在 HTML 表中显示的一组数据库记录的最简单方法是利用 Visual Studio 提供的基架。

通过选择菜单选项来生成你的应用程序**生成，生成解决方案**。 您必须生成应用程序打开之前**添加视图**对话框或数据类不会显示在该对话框。

右键单击 index （） 操作，然后选择菜单选项**添加视图**（请参见图 5）。


[![添加视图](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**图 05**： 添加视图 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image10.png))


在中**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。 选择作为 Movie 类**查看数据类**。 选择*列表*作为**查看内容**（请参阅图 6）。 选择这些选项将生成一个强类型化视图，显示电影列表。


[![添加视图对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**图 06**: 添加视图对话框 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image12.png))


单击后**添加**自动生成的按钮，代码清单 2 中的视图。 此视图包含循环的电影集合并显示每个电影属性所需的代码。

**代码清单 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

可以通过选择菜单选项来运行应用程序**调试、 启动调试**（或按 F5 键）。 运行应用程序将启动 Internet Explorer。 如果导航到 /Movie URL，那么您将看到图 7 中的页。


[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**图 07**： 电影的表 ([单击以查看实际尺寸的图像](displaying-a-table-of-database-data-cs/_static/image14.png))


如果您不喜欢在图 7 中的数据库记录的网格的外观有关的任何信息则可以只需修改索引视图。 例如，可以更改*DateReleased*标头*发布日期*通过修改索引视图。

## <a name="create-a-template-with-a-partial"></a>使用部分创建一个模板

当视图获取过于复杂时，它最好开始分解为分区的视图。 使用分区可以更轻松地理解和维护你的视图。 我们将创建一个分部，我们可以使用作为模板来设置每个电影数据库记录的格式。

请按照以下步骤创建分部操作：

1. 右键单击 Views\Movie 文件夹，然后选择菜单选项**添加视图**。
2. 选中复选框标记为*创建分部视图 (.ascx)*。
3. 命名分部*MovieTemplate*。
4. 选中复选框标记为**创建强类型化视图**。
5. 选择作为电影*查看数据类*。
6. 选择为空*查看内容*。
7. 单击**添加**按钮将部分添加到你的项目。

完成这些步骤后，修改部分 MovieTemplate 与列表 3 类似的形式。

**代码清单 3 – Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

列表 3 中的部分包含的记录单个行的模板。

列表 4 中已修改的索引视图使用 MovieTemplate 部分。

**列表 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

列表 4 中的该视图包含 foreach 循环遍历所有电影。 为每个电影 MovieTemplate 部分用于设置格式的电影。 通过调用 RenderPartial() 帮助器方法呈现 MovieTemplate。

已修改的索引视图呈现数据库记录完全相同的 HTML 的表。 但是，已极大地简化视图。


RenderPartial() 方法是不同于大多数其他帮助器方法，因为它不会返回一个字符串。 因此，您必须调用 RenderPartial() 方法使用&lt;%html.renderpartial(); %&gt;而不是&lt;%= Html.RenderPartial(); %&gt;。


## <a name="summary"></a>总结

本教程的目的是说明如何在 HTML 表中显示的一组数据库记录。 首先，您学习了如何通过利用 Microsoft 实体框架的控制器操作返回的一组数据库记录。 接下来，您学习了如何使用 Visual Studio 基架生成一个视图，它会自动显示的项的集合。 最后，您学习了如何通过利用一个分部的简化视图。 您学习了如何使用部分作为模板，以便您可以设置每个数据库记录的格式。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)
