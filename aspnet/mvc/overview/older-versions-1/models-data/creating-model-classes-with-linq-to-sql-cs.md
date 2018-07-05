---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: 创建模型类使用 LINQ to SQL (C#) |Microsoft Docs
author: microsoft
description: 本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。 在本教程中，您将学习如何构建模型 c...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: 01a8443326807ff784999288761de85b6ea976b9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395355"
---
<a name="creating-model-classes-with-linq-to-sql-c"></a>使用 LINQ to SQL (C#) 创建模型类
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> 本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。 在本教程中，您将学习如何生成模型的类和执行通过利用 Microsoft LINQ 到 SQL 数据库访问权限。


本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。 在本教程中，了解如何生成模型的类和执行通过利用 Microsoft LINQ 到 SQL 数据库访问权限

在本教程中，我们构建一个基本的电影数据库应用程序。 我们先创建电影数据库应用程序中的最快且最简单的方法可能。 我们将执行我们的数据访问的所有直接从控制器操作。

接下来，您将了解如何使用存储库模式。 使用存储库模式需要更多工作。 但是，采用此模式的优点是它使你能够构建到自适应应用程序更改，可以轻松地测试。

## <a name="what-is-a-model-class"></a>什么是 Model 类？

MVC 模型包含所有未包含在 MVC 视图或 MVC 控制器中的应用程序逻辑。 具体而言，MVC 模型包含的所有应用程序业务和数据访问逻辑。

可以使用各种不同的技术来实现数据访问逻辑。 例如，您可以构建使用 Microsoft 实体框架、 NHibernate、 Subsonic 或 ADO.NET 类的数据访问类。

在本教程中，我使用 LINQ to SQL 来查询和更新数据库。 LINQ to SQL 提供的与 Microsoft SQL Server 数据库进行交互非常简单的方法。 但是，务必了解 ASP.NET MVC framework 不绑定到 LINQ to SQL 以任何方式。 ASP.NET MVC 是与任何数据访问技术兼容。

## <a name="create-a-movie-database"></a>创建电影数据库

在此教程--为了说明如何构建模型类-我们构建一个简单的电影数据库应用程序。 第一步是创建新的数据库。 右键单击该应用\_在解决方案资源管理器窗口中，选择菜单选项的数据文件夹**添加、 新项**。 选择**SQL Server 数据库**模板，为其提供名称 MoviesDB.mdf，然后单击**添加**按钮 （请参见图 1）。


[![添加新的 SQL Server 数据库](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**图 01**： 添加新的 SQL Server 数据库 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))


创建新的数据库后，可以通过双击 MoviesDB.mdf 文件在应用中的打开数据库\_数据文件夹。 双击 MoviesDB.mdf 文件会打开服务器资源管理器窗口 （请参见图 2）。

使用 Visual Web Developer 时，服务器资源管理器窗口称为数据库资源管理器窗口。


[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**图 02**： 使用服务器资源管理器窗口 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))


我们需要将表添加到我们代表我们的电影的数据库。 右键单击表文件夹，然后选择菜单选项**添加新表**。 选择此菜单选项打开表设计器 （请参见图 3）。


[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**图 03**： 表设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))


我们需要向数据库表添加以下列：

| **列名称** | **数据类型** | **允许 null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(200) | False |
| 主管 | nvarchar （50) | False |

需要两个特殊对执行的操作 Id 列。 首先，需要将 Id 列作为主键列标记通过在表设计器中选择列并单击密钥图标。 LINQ to SQL 要求您在执行插入或更新对数据库时指定主键列。

接下来，需要将 Id 列标记为标识列中，通过是将值分配给**是标识**属性 （请参见图 3）。 标识列是自动分配新的数字，只要将新的数据行添加到表的列。

## <a name="create-linq-to-sql-classes"></a>创建 LINQ to SQL 类

我们的 MVC 模型将包含 LINQ to SQL 类表示 tblMovie 数据库表。 若要创建这些 LINQ to SQL 类的最简单方法是右键单击 Models 文件夹中，选择**添加、 新建项**，选择的 LINQ to SQL 类模板，为指定类名称 Movie.dbml，然后单击**添加**按钮 （请参见图 4）。


[![创建 LINQ to SQL 类](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**图 04**： 创建 LINQ to SQL 类 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))


立即创建电影 LINQ to SQL 类后，将显示对象关系设计器。 可以将数据库表拖到对象关系设计器创建 LINQ to SQL 类表示特定的数据库表上服务器资源管理器窗口中。 我们需要添加到对象关系设计器上的 tblMovie 数据库表 （请参见图 5）。


[![使用对象关系设计器](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**图 05**： 使用对象关系设计器 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))


默认情况下，对象关系设计器创建一个类具有与数据库表拖到设计器上完全相同的名称。 但是，我们不想要调用我们的类`tblMovie`。 因此，单击设计器中的类的名称，并将类的名称更改为电影。

最后，请记住单击**保存**按钮 （将软盘保存图片） 以保存 LINQ to SQL 类。 否则，不会通过对象关系设计器生成 LINQ to SQL 类。

## <a name="using-linq-to-sql-in-a-controller-action"></a>在控制器操作中使用 LINQ to SQL

现在，我们有我们 LINQ to SQL 类，我们可以使用这些类以从数据库检索数据。 在本部分中，您将了解如何使用 LINQ to SQL 类直接在控制器操作中。 我们将一个 MVC 视图中显示 tblMovies 数据库表中的电影的列表。

首先，我们需要修改 HomeController 类。 可以在你的应用程序的控制器文件夹中找到此类。 修改类，以使它看起来像列表 1 中的类。

**代码清单 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

`Index()`在列表 1 中的操作使用 LINQ to SQL DataContext 类 ( `MovieDataContext`) 来表示`MoviesDB`数据库。 `MoveDataContext`类由 Visual Studio 对象关系设计器生成。

LINQ 查询执行针对 DataContext 检索所有从电影`tblMovies`数据库表。 电影列表分配给一个名为的本地变量`movies`。 最后，电影列表是通过传递给视图查看数据。

为了显示电影，我们接下来需要修改索引视图。 您可以发现中的索引视图`Views\Home\`文件夹。 更新索引视图，使它看起来像列表 2 中的视图。

**代码清单 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

请注意，已修改的索引视图包含`<%@ import namespace %>`指令在视图的顶部。 此指令将导入`MvcApplication1.Models namespace`。 我们需要才能使用此命名空间`model`类-具体而言，`Movie`类-在视图中的。

代码清单 2 中的视图包含`foreach`循环循环访问的所有项所表示的`ViewData.Model`属性。 值`Title`属性显示为每个`movie`。

请注意，值`ViewData.Model`属性强制转换为`IEnumerable`。 这是必要的以循环访问的内容`ViewData.Model`。 此处的另一个选项是创建一个强类型`view`。 当你创建一个强类型`view`，则转换`ViewData.Model`到视图的代码隐藏类中的特定类型的属性。

如果运行修改后的应用程序`HomeController`类和索引视图，则会收到一个空白页。 您将受到空白页，因为在没有电影记录`tblMovies`数据库表。

若要添加到记录`tblMovies`数据库表中，右键单击`tblMovies`数据库在服务器资源管理器窗口 （在 Visual Web Developer 中的数据库资源管理器窗口） 中的表并选择菜单选项显示表数据。 可以插入`movie`记录通过使用显示 （见图 6） 的网格。


[![插入电影](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**图 06**： 插入电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))


添加到某些数据库记录后`tblMovies`表，并且运行该应用程序，您会看到图 7 中的页。 项目符号列表中将显示所有电影数据库记录。


[![显示与索引视图的电影](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**图 07**： 显示与索引视图的电影 ([单击以查看实际尺寸的图像](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))


## <a name="using-the-repository-pattern"></a>使用存储库模式

在上一节中，我们使用 LINQ to SQL 类直接在控制器操作中。 我们使用了`MovieDataContext`类直接从`Index()`控制器操作。 没有什么不妥执行此操作在简单的应用程序的情况下。 但是，在控制器类中直接使用 LINQ to SQL 的工作会产生问题时构建更复杂的应用程序所需。

使用 LINQ to SQL 是控制器类中难以在将来切换数据访问技术。 例如，您可能决定切换到使用作为数据访问技术的 Microsoft 实体框架使用 Microsoft LINQ to SQL。 在这种情况下，你将需要重写访问该数据库在你的应用程序的每个控制器。

控制器类中使用 LINQ to SQL 还使得难以构建你的应用程序的单元测试。 通常情况下，您不想要执行单元测试时，与数据库交互。 你想要使用你的单元测试来测试应用程序逻辑并不是你的数据库服务器。

若要生成的 MVC 应用程序这是到未来的适应能力更强的更改和进行更轻松地测试，则应考虑使用存储库模式。 当您使用的存储库模式时，您将创建包含所有数据库访问逻辑的一个独立的存储库类。

在创建存储库类，您将创建表示的所有存储库类使用的方法的接口。 在你的控制器，您编写代码的依据而不是存储库的接口。 这样一来，您可以实现在将来使用不同的数据访问技术的存储库。

列表 3 中的接口名为`IMovieRepository`，它表示名为的单个方法`ListAll()`。

**代码清单 3 – `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

列表 4 中的存储库类实现`IMovieRepository`接口。 请注意，它包含一个名为方法`ListAll()`所需的方法对应`IMovieRepository`接口。

**列表 4 – `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

最后，`MoviesController`列表 5 中的类使用的存储库模式。 它不能再使用 LINQ to SQL 类直接。

**列表 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

请注意，`MoviesController`列表 5 中的类具有两个构造函数。 第一个构造函数，无参数构造函数中，应用程序在运行时调用。 此构造函数创建的实例`MovieRepository`类，并将其传递给第二个构造函数。

第二个构造函数具有单个参数：`IMovieRepository`参数。 此构造函数只需将参数的值分配给一个名为的类级字段`_repository`。

`MoviesController`类利用称为依赖关系注入模式的软件设计模式。 具体而言，它使用称为构造函数依赖关系注入。 你可以阅读更多有关此模式通过阅读 Martin Fowler 的以下文章：

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

请注意，中的代码的所有`MoviesController`（除了第一个构造函数） 的类与交互`IMovieRepository`而不是实际接口`MovieRepository`类。 与而不是接口的具体实现的抽象接口进行交互的代码。

如果你想要修改应用程序使用的数据访问技术，则您可以仅实施`IMovieRepository`使用备用数据库访问技术的类的接口。 例如，可以创建`EntityFrameworkMovieRepository`类或`SubSonicMovieRepository`类。 由于控制器类针对接口进行编程，因此可以传递的新实现`IMovieRepository`到控制器类和类将继续运行。

此外，如果你想要测试`MoviesController`类，则您可以传递假电影存储库类中的，以便`HomeController`。 您可以实现`IMovieRepository`却没有实际访问数据库，但包含所有所需的方法的类的类`IMovieRepository`接口。 这样一来，进行单元测试`MoviesController`而无需实际访问的实际数据库的类。

## <a name="summary"></a>总结

本教程的目的是演示如何通过利用 Microsoft LINQ to SQL 创建 MVC 模型类。 在 ASP.NET MVC 应用程序中显示数据库数据的两种策略，我们探讨。 首先，创建 LINQ to SQL 类，并使用直接在控制器操作中的类。 使用 LINQ to SQL 类在控制器内使你能够快速并轻松地在 MVC 应用程序中显示数据库数据。

接下来，我们探讨了显示数据库数据的稍微有些困难，但绝对更为良性的路径。 我们利用了存储库模式，并放在单独的存储库类中的所有我们数据库访问逻辑。 在我们控制器中，我们编写了所有我们针对而不是具体类的接口的代码。 存储库模式的优点是它可让我们可以轻松地在将来更改数据库访问技术，并且它使我们能够轻松地测试了控制器类。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-the-entity-framework-cs.md)
> [下一页](displaying-a-table-of-database-data-cs.md)
