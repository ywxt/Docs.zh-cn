---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: 使用 ASP.NET MVC (VB) 创建电影数据库应用程序在 15 分钟 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。 本教程是很棒的介绍的人员将新 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: a64d140eba4ebf489486af1a0be6269a8b904c13
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372590"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>创建电影数据库应用程序在 15 分钟内使用 ASP.NET MVC (VB)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

[下载代码](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther 生成整个数据库驱动 ASP.NET MVC 应用程序从头到尾完成。 本教程是过程的谁不熟悉 ASP.NET MVC Framework 和想要了解的构建 ASP.NET MVC 应用程序的人员很棒的介绍。


本教程的目的是为您提供的"什么就像"的意义上构建的 ASP.NET MVC 应用程序。 在本教程中，我冲击生成整个 ASP.NET MVC 应用程序从头到尾完成。 我向您展示如何构建的简单数据库驱动应用程序说明了如何列出、 创建和编辑数据库记录。

若要简化构建我们的应用程序的过程，我们将利用 Visual Studio 2008 的基架功能。 我们将让 Visual Studio 生成的初始代码和我们的控制器、 模型和视图的内容。

如果您曾经使用 Active Server Pages 或 ASP.NET，然后应发现 ASP.NET MVC 非常熟悉。 ASP.NET MVC 视图是非常类似于 Active Server Pages 应用程序中的页。 并且，就像传统的 ASP.NET Web 窗体应用程序，ASP.NET MVC 提供具有丰富的语言和.NET framework 提供的类的完全访问权限。

我希望是本教程将为您提供一种构建的 ASP.NET MVC 应用程序体验的方式相似和不同于生成 Active Server Pages 或 ASP.NET Web 窗体应用程序的体验。

## <a name="overview-of-the-movie-database-application"></a>电影数据库应用程序的概述

由于我们的目标是为了简单起见，我们将构建一个非常简单的电影数据库应用程序。 我们简单的电影数据库应用程序将使我们可以做三件事：

1. 列出一组的电影数据库记录
2. 创建一个新的电影数据库记录
3. 编辑现有的电影数据库记录

同样，因为我们想要为简单起见，我们将充分利用 ASP.NET MVC framework 构建我们的应用程序所需的功能的最小数目。 例如，我们将不会利用测试驱动开发。

若要创建我们的应用程序，我们需要完成以下步骤：

1. 创建 ASP.NET MVC Web 应用程序项目
2. 创建数据库
3. 创建数据库模型
4. 创建 ASP.NET MVC 控制器
5. 创建 ASP.NET MVC 视图

## <a name="preliminaries"></a>初步操作

你将需要 Visual Studio 2008 或 Visual Web Developer 2008 Express 构建的 ASP.NET MVC 应用程序。 此外需要下载 ASP.NET MVC 框架。

如果你拥有 Visual Studio 2008，然后可以从该网站下载 Visual Studio 2008 的 90 天试用版：

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

或者，您可以创建 ASP.NET MVC 应用程序与 Visual Web Developer Express 2008。 如果您决定使用 Visual Web Developer 速成版，然后必须具有安装 Service Pack 1。 您可以从此网站中下载 Visual Web Developer 2008 速成版 Service Pack 1:

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&ampdisplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

安装 Visual Studio 2008 或 Visual Web Developer 2008 后，你需要安装 ASP.NET MVC 框架。 您可以从以下网站下载 ASP.NET MVC framework:

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> 而无需单独下载 ASP.NET framework 和 ASP.NET MVC 框架，可以充分利用 Web 平台安装程序。 Web 平台安装程序是使你能够轻松地管理已安装的应用程序的应用程序是您的计算机：
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a>创建 ASP.NET MVC Web 应用程序项目

让我们首先在 Visual Studio 2008 中创建新的 ASP.NET MVC Web 应用程序项目。 选择菜单选项**文件，新的项目**，你将看到在图 1 中的新项目对话框。 选择作为编程语言的 Visual Basic，并选择 ASP.NET MVC Web 应用程序项目模板。 为项目名称 MovieApp，然后单击确定按钮。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**图 01**: 新建项目对话框 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))


请确保从新项目对话框顶部的下拉列表中选择.NET Framework 3.5 或 ASP.NET MVC Web 应用程序项目模板不会显示。


每当创建新的 MVC Web 应用程序项目时，Visual Studio 会提示您创建一个单独的单元测试项目。 图 2 中的对话框会显示。 由于我们不会在本教程中需要创建测试由于时间约束 （并且，是的我们应认为这有点歉疚） 选择**否**选项，然后单击**确定**按钮。

> [!NOTE] 
> 
> Visual Web Developer 不支持测试项目。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**图 02**: 创建单元测试项目对话框 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))


ASP.NET MVC 应用程序具有一组标准的文件夹： 模型、 视图和控制器的文件夹。 您可以看到此组标准的解决方案资源管理器窗口中的文件夹。 我们需要将文件添加到的每个模型、 视图和控制器文件夹中，以生成我们的电影数据库应用程序。

使用 Visual Studio 创建新的 MVC 应用程序，可以获取示例应用程序。 因为我们想要从头开始，我们需要删除此示例应用程序的内容。 您需要删除以下文件和以下文件夹：

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>创建数据库

我们需要创建一个数据库以包含我们的电影数据库记录。 幸运的是，Visual Studio 包含一个名为 SQL Server Express 的免费数据库。 请按照下列步骤来创建数据库：

1. 右键单击该应用\_在解决方案资源管理器窗口中，选择菜单选项的数据文件夹**添加、 新项**。
2. 选择**数据**类别，然后选择**SQL Server 数据库**模板 （参见图 3）。
3. 新数据库命名*MoviesDB.mdf*然后单击**添加**按钮。

创建数据库后，您可以通过双击 MoviesDB.mdf 文件应用中连接到数据库\_数据文件夹。 双击 MoviesDB.mdf 文件会打开服务器资源管理器窗口。

> [!NOTE] 
> 
> 服务器资源管理器窗口是名为在 Visual Web Developer 的情况下的数据库资源管理器窗口。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**图 03**： 创建 Microsoft SQL Server 数据库 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))


接下来，我们需要创建一个新的数据库表。 在服务器资源管理器窗口中，右键单击表文件夹并选择菜单选项**添加新表**。 选择此菜单选项打开的数据库表设计器。 创建数据库以下列：

<a id="0.2_table01"></a>


| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(100) | False |
| 主管 | Nvarchar(100) | False |
| DateReleased | DateTime | False |


第一列，Id 列中，有两个特殊属性。 首先，需要将 Id 列作为主键列标记。 选择 Id 列之后，单击**设置主键**（它是看起来像一个键的图标） 按钮。 其次，您需要将标记为标识列的 Id 列。 在列属性窗口中向下滚动到标识规范部分并展开它。 更改**是标识**属性设置为值**是**。 完成后，表应如图 4 所示。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**图 04**: 电影数据库表 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))


最后一步是将保存新表。 单击保存按钮 （软盘图标） 并为新的表名称电影。

完成创建表后，向表中添加某些电影记录。 右键单击服务器资源管理器窗口中的电影表，然后选择菜单选项**显示表数据**。 输入你最喜爱的电影 （请参见图 5） 的列表。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**图 05**： 输入电影记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))


## <a name="creating-the-model"></a>创建模型

接下来，我们需要创建一组类来表示我们的数据库。 我们需要创建数据库模型。 我们将充分利用 Microsoft Entity Framework 自动生成数据库模型的类。

> [!NOTE] 
> 
> ASP.NET MVC 框架不依赖于 Microsoft Entity Framework。 您也可以利用的各种对象关系映射创建你的数据库模型类 (或者 / M) 工具，包括 LINQ to SQL，Subsonic 和 NHibernate。


请按照下列步骤以启动实体数据模型向导：

1. 右键单击解决方案资源管理器窗口，然后选择菜单选项中的 Models 文件夹**添加、 新项**。
2. 选择**数据**类别，然后选择**ADO.NET 实体数据模型**模板。
3. 为你的数据模型提供名称*MoviesDBModel.edmx*然后单击**添加**按钮。

单击添加按钮后，会显示实体数据模型向导 （请参阅图 6）。 请按照下列步骤以完成向导：

1. 在中**选择模型内容**步骤中，选择**从数据库生成**选项。
2. 在中**选择数据连接**步骤中，使用*MoviesDB.mdf*数据连接和名称*MoviesDBEntities*的连接设置。 单击**下一步**按钮。
3. 在中**选择数据库对象**步骤中，展开表节点中，选择电影表。 输入的命名空间*MovieApp.Models*然后单击**完成**按钮。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**图 06**： 生成具有实体数据模型向导的数据库模型 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))


完成实体数据模型向导后，会打开实体数据模型设计器。 在设计器应显示电影数据库表 （请参阅图 7）。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**图 07**: 实体数据模型设计器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))


我们需要做出一项更改，然后我们继续。 实体数据向导生成一个名为电影模型类，表示电影数据库表。 由于我们将使用电影类来表示特定电影，我们需要修改这个类为名称*电影*而不是*电影*（单数而非复数形式）。

双击设计器图面上的类的名称并将影片中的类的名称更改为电影。 此更改后，单击**保存**按钮 （软盘图标） 以生成电影类。

## <a name="creating-the-aspnet-mvc-controller"></a>创建 ASP.NET MVC 控制器

下一步是创建 ASP.NET MVC 控制器。 控制器负责控制用户如何与 ASP.NET MVC 应用程序交互。

请执行这些步骤：

1. 在解决方案资源管理器窗口中，右键单击 Controllers 文件夹，然后选择菜单选项**添加、 控制器**。
2. 在添加控制器对话框中，输入名称*HomeController* ，并检查标记为复选框**添加操作方法用于创建、 更新和的详细信息方案**（请参阅图 8）。
3. 单击**添加**按钮将新控制器添加到你的项目。

完成这些步骤后，将创建在列表 1 中的控制器。 请注意，它包含名为 Index，详细信息，创建、 方法和编辑。 在以下部分中，我们将添加必要的代码来获取这些方法才能起作用。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**图 08**： 添加新的 ASP.NET MVC 控制器 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))


**代码清单 1 – Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>列出数据库记录

主控制器的 index （） 方法是 ASP.NET MVC 应用程序的默认方法。 当您运行的 ASP.NET MVC 应用程序时，index （） 方法是调用的第一个控制器方法。

我们将使用 index （） 方法以显示电影数据库表中的记录的列表。 我们将充分利用数据库模型类我们之前创建的电影数据库记录检索使用 index （） 方法。

我已修改 HomeController 类在代码清单 2 中的，使其包含名为的新私有字段\_db。 MoviesDBEntities 类表示我们的数据库模型，我们将使用此类与我们的数据库进行通信。

我已修改代码清单 2 中的 index （） 方法。 Index （） 方法使用 MoviesDBEntities 类从电影数据库表中检索的所有电影记录。 表达式 *\_db。MovieSet.ToList()* 从电影数据库表中返回所有电影记录的列表。

电影列表传递给视图。 获取传递给 View() 方法的任何内容获取传递给视图作为视图数据。

**代码清单 2 – Controllers/HomeController.vb （已修改索引方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index （） 方法返回名为 Index 的视图。 我们需要创建此视图以显示电影数据库记录的列表。 请执行这些步骤：


应生成项目 (选择菜单选项**生成，生成解决方案**) 打开之前**添加视图**中将出现对话框或没有类**查看数据类**下拉列表中。


1. 右键单击代码编辑器中的 index （） 方法，然后选择菜单选项**添加视图**（请参阅图 9）。
2. 在添加视图对话框中，验证相应的复选框标记为**创建强类型化视图**检查。
3. 从**查看内容**下拉列表中，选择的值*列表*。
4. 从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。
5. 单击添加按钮以创建新查看 （请参阅图 10）。

完成这些步骤后，名为 Index.aspx 的新视图添加到 views/home 文件夹中。 索引视图的内容包含在列表 3 中。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**图 09**： 添加的视图的控制器操作 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**图 10**： 使用添加视图对话框中创建新视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

索引视图显示的所有电影记录从 HTML 表内的电影数据库表。 该视图包含一个 For Each 循环，循环访问由 ViewData.Model 属性表示每个电影。 如果按 F5 键运行应用程序，您将看到在图 11 网页。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**图 11**： 该索引视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))


## <a name="creating-new-database-records"></a>创建新的数据库记录

我们在上一节中创建的索引视图包含用于创建新的数据库记录的链接。 让我们继续并实现的逻辑和创建视图所需创建新的电影数据库记录。

主控制器包含名为 create （） 的两个方法。 第一个 create （） 方法没有任何参数。 Create （） 方法的此重载用于显示用于创建新的电影数据库记录的 HTML 窗体。

第二个 create （） 方法有一个 FormCollection 参数。 用于创建新的电影的 HTML 窗体发布到服务器时，调用 create （） 方法的此重载。 请注意，此第二个 create （） 方法具有 AcceptVerbs 属性，以防止方法被调用，除非执行 HTTP Post 操作。

此第二个 create （） 方法已在列表 4 中更新 HomeController 类中被修改。 Create （） 方法的新版本接受电影参数，并包含用于电影数据库表中插入新电影的逻辑。

> [!NOTE] 
> 
> 请注意，绑定属性。 因为我们不想要更新从 HTML 窗体的电影 Id 属性，我们需要此属性中显式排除。


**列表 4 – Controllers\HomeController.vb （已修改 Create 方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio，可以轻松地创建用于创建新的电影数据库窗体记录 （请参阅图 12）。 请执行这些步骤：

1. 右键单击代码编辑器中的 create （） 方法，然后选择菜单选项**添加视图**。
2. 验证相应的复选框标记为**创建强类型化视图**检查。
3. 从**查看内容**下拉列表中，选择的值*创建*。
4. 从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。
5. 单击**添加**按钮以创建新视图。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**图 12**： 添加创建视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))


Visual Studio 查看在列表 5 中会自动生成。 此视图包含 HTML 窗体包括的字段对应于每个电影类的属性。

**列表 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> 生成的添加视图对话框中的 HTML 窗体生成 Id 窗体字段。 Id 列是标识列，因为我们不需要此窗体字段，并且可以放心删除它。


添加 Create 视图后，您可以向数据库添加新电影记录。 通过按 F5 键运行应用程序，并单击新创建的链接以查看图 13 中的窗体。 如果完成并提交表单时，会创建新的电影数据库记录。

请注意，自动获取窗体验证。 如果没有输入一个 movie，发布日期，或者输入无效的发布日期，然后重新显示该窗体，并突出显示发布日期字段。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**图 13**： 创建新的电影数据库记录 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))


## <a name="editing-existing-database-records"></a>编辑现有的数据库记录

在前面部分中，我们讨论了如何列出和创建新的数据库记录。 在此最后一节中，我们将讨论如何可以编辑现有的数据库记录。

首先，我们需要生成编辑窗体。 此步骤很容易，因为 Visual Studio 将生成为我们的编辑窗体自动。 在 Visual Studio 代码编辑器中打开 HomeController.vb 类，并按照以下步骤：

1. 右键单击代码编辑器中的 edit （） 方法，然后选择菜单选项**添加视图**（请参阅图 14）。
2. 选中复选框标记为**创建强类型化视图**。
3. 从**查看内容**下拉列表中，选择的值*编辑*。
4. 从**查看数据类**下拉列表中，选择的值*MovieApp.Movie*。
5. 单击**添加**按钮以创建新视图。

完成这些步骤将添加到 views/home 文件夹中名为 Edit.aspx 的新视图。 此视图包含 HTML 窗体以编辑电影记录。


[![新建项目对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**图 14**： 添加编辑视图 ([单击以查看实际尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))


> [!NOTE] 
> 
> 编辑视图包含电影 Id 属性与对应的 HTML 窗体字段。 由于您不希望人们编辑 Id 属性的值，则应删除此窗体字段。


最后，我们需要修改主控制器，以便它也支持编辑的数据库记录。 更新的 HomeController 类都包含在列表 6。

**代码清单 6 – Controllers\HomeController.vb （编辑方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

列表 6 中我到 edit （） 方法的这两个重载添加其他逻辑。 第一种 edit （） 方法返回给传递给方法的 Id 参数相对应的电影数据库记录。 第二个重载在数据库中执行到电影记录的更新。

请注意，您必须检索原始电影，然后调用 ApplyPropertyChanges()，以更新数据库中已有的电影。

## <a name="summary"></a>总结

本教程的目的是让您构建的 ASP.NET MVC 应用程序体验的了解。 我希望您发现构建 ASP.NET MVC web 应用程序是非常类似于生成 Active Server Pages 或 ASP.NET 应用程序的体验。

在本教程中，我们检查只 ASP.NET MVC 框架的最基本功能。 在将来的教程中，我们深入控制器、 控制器操作、 视图、 视图数据，以及 HTML 帮助程序等主题。

> [!div class="step-by-step"]
> [上一篇](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
