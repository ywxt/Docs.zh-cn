---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
title: 使用 SqlDataSource 控件 (C#) 查询数据 |Microsoft Docs
author: rick-anderson
description: 在前面的教程中我们使用 ObjectDataSource 控件完全分开的数据访问层的表示层。 与此教师正在启动...
ms.author: aspnetcontent
ms.date: 02/20/2007
ms.assetid: 60512d6a-b572-4b7a-beb3-3e44b4d2020c
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b9ca474b7a085302d287a223c08abe2fa5336b0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815286"
---
<a name="querying-data-with-the-sqldatasource-control-c"></a>使用 SqlDataSource 控件 (C#) 查询数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_CS.exe)或[下载 PDF](querying-data-with-the-sqldatasource-control-cs/_static/datatutorial47cs1.pdf)

> 在前面的教程中我们使用 ObjectDataSource 控件完全分开的数据访问层的表示层。 我们从开始本教程，了解如何为不需要这种严格分离演示文稿和数据访问的简单应用程序使用 SqlDataSource 控件。


## <a name="introduction"></a>介绍

所有这些教程我们 ve 检查到目前为止已使用分层体系结构，包含演示文稿、 业务逻辑和数据访问层。 数据访问层 (DAL) 用在第一个教程 ([创建数据访问层](../introduction/creating-a-data-access-layer-cs.md)) 和业务逻辑层中第二个 ([创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md))。 从开始[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程，我们已了解如何使用 ASP.NET 2.0 s 新 ObjectDataSource 控件来以声明方式与从表示层体系结构进行交互。

虽然使用体系结构，所有教程到目前为止已处理数据，还有可能要访问、 插入、 更新和删除数据库数据直接从 ASP.NET 页中，从而绕过体系结构。 执行此操作将直接在 web 页面中的特定数据库查询和业务逻辑。 对于足够大或太复杂的应用程序，设计、 实现和使用分层体系结构是至关重要的成功、 可更新性，与应用程序的可维护性。 开发可靠的体系结构，但是，可能会不必要时创建非常简单的一次性应用程序。

ASP.NET 2.0 提供了五个内置数据源控件[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)， [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)， [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)， [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)，并[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)。 SqlDataSource 可以用于访问和修改数据直接从关系数据库中，包括 Microsoft SQL Server、 Microsoft Access、 Oracle、 MySQL 和其他人。 在本教程的下一步的三个，我们将介绍如何使用 SqlDataSource 控件，探索如何查询和筛选数据库数据，以及如何使用到 SqlDataSource 插入、 更新和删除数据。


![ASP.NET 2.0 包括五个内置数据源控件](querying-data-with-the-sqldatasource-control-cs/_static/image1.gif)

**图 1**: ASP.NET 2.0 包括五个内置数据源控件


## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>比较 ObjectDataSource 和 SqlDataSource

从概念上讲，ObjectDataSource 和 SqlDataSource 控件是只需对数据的代理。 如中所述[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程中，ObjectDataSource 具有指示提供数据和方法调用选择、 插入、 更新和删除数据的对象类型的属性从基础对象类型。 一旦配置了 ObjectDataSource 的属性，数据如 GridView、 DetailsView 或 DataList Web 控件可以绑定到控件，使用 ObjectDataSource s `Select()`， `Insert()`， `Delete()`，和`Update()`方法基础体系结构进行交互。

SqlDataSource 提供相同的功能，但操作针对关系数据库而不是对象库。 使用 SqlDataSource，我们必须指定数据库连接字符串和即席 SQL 查询或存储过程来执行插入、 更新、 删除和检索数据。 SqlDataSource s `Select()`， `Insert()`， `Update()`，和`Delete()`方法，调用时，连接到指定的数据库，并发出相应的 SQL 查询。 如以下关系图所示，这些方法执行连接到数据库中，发出查询，并返回结果的单调工作。


![SqlDataSource 充当数据库的代理](querying-data-with-the-sqldatasource-control-cs/_static/image2.gif)

**图 2**: SqlDataSource 充当数据库的代理


> [!NOTE]
> 在本教程中我们将重点从数据库检索数据。 在中[插入、 更新和删除数据使用 SqlDataSource 控件](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)教程，我们将了解如何配置 SqlDataSource 以支持插入、 更新和删除。


## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 和 AccessDataSource 控件

除了 SqlDataSource 控件，ASP.NET 2.0 还包括 AccessDataSource 控件。 这两个不同的控件导致很多开发人员熟悉 ASP.NET 2.0 怀疑 AccessDataSource 控件旨在以独占方式使用 Microsoft Access 使用 SqlDataSource 控件旨在以独占方式与 Microsoft SQL Server。 尽管 AccessDataSource 能够专门使用 Microsoft Access，SqlDataSource 控件配合*任何*，可以通过.NET 访问关系数据库。 这包括任何符合 OleDb 或 ODBC 数据存储，如 Microsoft SQL Server、 Microsoft Access、 Oracle、 Informix、 MySQL 和 PostgreSQL，此外还有许多其他。

AccessDataSource 和 SqlDataSource 控件之间的唯一区别是指定的数据库连接信息的方式。 AccessDataSource 控件需要只是访问数据库文件的文件路径。 SqlDataSource，但是，需要完整的连接字符串。

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>步骤 1： 创建 SqlDataSource 网页

我们开始探索如何直接使用数据库数据，使用 SqlDataSource 控件之前，让 s 先花点时间在我们的网站项目，我们需要为本教程中下, 一步 3 中创建 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`SqlDataSource`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`


![将 ASP.NET 页面添加与 SqlDataSource 相关的教程](querying-data-with-the-sqldatasource-control-cs/_static/image3.gif)

**图 3**： 将 ASP.NET 页面添加与 SqlDataSource 相关的教程


在其他文件夹中，喜欢`Default.aspx`在`SqlDataSource`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](querying-data-with-the-sqldatasource-control-cs/_static/image5.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image4.gif)

**图 4**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](querying-data-with-the-sqldatasource-control-cs/_static/image6.gif))


最后，将这四个页面添加到条目为`Web.sitemap`文件。 具体而言，将以下标记添加自定义按钮之后添加到 DataList 和 Repeater `<siteMapNode>`:


[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample1.sql)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含用于编辑、 插入和删除教程的项。


![站点图现在包括项 SqlDataSource 学习教程](querying-data-with-the-sqldatasource-control-cs/_static/image7.gif)

**图 5**： 站点图现在包括项 SqlDataSource 学习教程


## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>步骤 2： 添加并配置 SqlDataSource 控件

首先打开`Querying.aspx`页中`SqlDataSource`文件夹，然后切换到设计视图。 将一个 SqlDataSource 控件从工具箱拖到设计器和组及其`ID`到`ProductsDataSource`。 如在 ObjectDataSource，SqlDataSource 不会生成任何呈现的输出，并因此将显示为灰色框，在设计图面上。 若要配置 SqlDataSource，单击从 SqlDataSource s 智能标记的配置数据源链接。


![单击配置从 SqlDataSource s 智能标记的数据源链接](querying-data-with-the-sqldatasource-control-cs/_static/image8.gif)

**图 6**： 单击配置从 SqlDataSource s 智能标记的数据源链接


此时会打开 SqlDataSource 控件 s 配置数据源向导。 尽管向导的步骤从 ObjectDataSource 控件 s 不同，但最终目标是相同，提供有关如何检索、 插入、 更新和删除数据通过数据源的详细信息。 对于 SqlDataSource 这必然指定要使用的基础数据库，并提供临时 SQL 语句或存储的过程。

向导第一步会提示我们的数据库。 下拉列表包含在 web 应用程序 s 中找到这些数据库`App_Data`文件夹和已添加到服务器资源管理器中的数据连接节点。 因为我们 ve 已添加的连接字符串`NORTHWIND.MDF`数据库中`App_Data`到我们的项目的文件夹`Web.config`文件，下拉列表包括对该连接字符串，引用`NORTHWINDConnectionString`。 从下拉列表中选择此项，然后单击下一步。


![从下拉列表中选择 NORTHWINDConnectionString](querying-data-with-the-sqldatasource-control-cs/_static/image9.gif)

**图 7**： 选择`NORTHWINDConnectionString`从下拉列表


选择后数据库，向导将询问要返回的数据的查询。 我们可以指定表或视图以返回或可以输入自定义 SQL 语句或指定存储的过程的列。 您可以切换此选择通过指定自定义 SQL 语句或存储的过程和表中的指定列或查看单选按钮。

> [!NOTE]
> 对于此第一个示例，让我们来使用指定的列从表或视图的选项。 我们将在本教程后面返回到向导并浏览指定的自定义 SQL 语句或存储的过程选项。


图 8 显示配置选择指定来自表或视图的单选按钮的列时，此 Select 语句屏幕。 下拉列表包含 Northwind 数据库，与所选的表或视图的列显示在下面的复选框列表中的表和视图集。 对于此示例中，let s 返回`ProductID`， `ProductName`，并`UnitPrice`中的列`Products`表。 如图 8 所示，进行这些选择向导显示了生成的 SQL 语句后`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`。


![返回 Products 表中的数据](querying-data-with-the-sqldatasource-control-cs/_static/image10.gif)

**图 8**： 返回数据自`Products`表


配置向导以返回后`ProductID`， `ProductName`，并`UnitPrice`中的列`Products`表中，单击下一步按钮。 此最终屏幕提供了有机会检查上一步中配置的查询的结果。 单击测试查询按钮执行的已配置`SELECT`语句并显示在网格中的结果。


![单击测试查询按钮以查看您的选择查询](querying-data-with-the-sqldatasource-control-cs/_static/image11.gif)

**图 9**： 单击测试查询按钮查看到您`SELECT`查询


若要完成该向导，单击完成。

像使用 ObjectDataSource，SqlDataSource 的向导只是将值分配给控件的属性，即[ `ConnectionString` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx)并[ `SelectCommand` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx)属性。 完成向导后，你 SqlDataSource 控件 s 声明性标记应类似于下面：


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample2.aspx)]

`ConnectionString`属性提供有关如何连接到数据库的信息。 此属性可以分配一个完整的硬编码连接字符串值，或者可以指向中的连接字符串`Web.config`。 若要引用在 Web.config 中的连接字符串值，请使用语法`<%$ expressionPrefix:expressionValue %>`。 通常情况下， *expressionPrefix*是 ConnectionStrings 和*expressionValue*中的连接字符串的名称`Web.config` [ `<connectionStrings>`部分](https://msdn.microsoft.com/library/bf7sd233.aspx)。 但是，可以使用的语法引用`<appSettings>`元素或从资源文件的内容。 请参阅[ASP.NET 表达式概述](https://msdn.microsoft.com/library/d5bd1tad.aspx)有关此语法的详细信息。

`SelectCommand`属性指定的临时 SQL 语句或存储的过程来执行以返回数据。

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>步骤 3： 添加数据 Web 控件并将其绑定到 SqlDataSource

SqlDataSource 配置之后，它可以绑定到数据 Web 控件，如 GridView、 DetailsView。 对于本教程，让我们来显示 GridView 中的数据。 从工具箱中，将 GridView 拖到绘图页上，并将其绑定到`ProductsDataSource`SqlDataSource 通过从 GridView s 智能标记中的下拉列表中选择数据源。


[![添加一个 GridView，并将其绑定到 SqlDataSource 控件](querying-data-with-the-sqldatasource-control-cs/_static/image13.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image12.gif)

**图 10**： 添加一个 GridView，并将其绑定到 SqlDataSource 控件 ([单击以查看实际尺寸的图像](querying-data-with-the-sqldatasource-control-cs/_static/image14.gif))


一旦您已从 GridView s 智能标记中的下拉列表中选择 SqlDataSource 控件，Visual Studio 将自动添加 BoundField 或 CheckBoxField 到 GridView 为每个数据源控件返回的列。 由于 SqlDataSource 返回三个数据库列`ProductID`， `ProductName`，和`UnitPrice`GridView 中有三个字段。

请花费片刻时间来配置 GridView 的三 BoundFields。 更改`ProductName`字段 s`HeaderText`属性设置为产品名称和`UnitPrice`价格字段 s。 此外设置格式`UnitPrice`字段作为一种货币。 以后进行这些修改，GridView s 声明性标记看起来应类似于下面：


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample3.aspx)]

访问本页可通过浏览器。 如图 11 所示，GridView 列出了每个产品 s `ProductID`， `ProductName`，和`UnitPrice`值。


[![GridView 显示每个产品 s 产品 id、 产品名称和单价值](querying-data-with-the-sqldatasource-control-cs/_static/image16.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image15.gif)

**图 11**： 根据 GridView 显示每个产品 s `ProductID`， `ProductName`，和`UnitPrice`值 ([单击以查看实际尺寸的图像](querying-data-with-the-sqldatasource-control-cs/_static/image17.gif))


GridView 时访问页面时调用其数据源控件的`Select()`方法。 如果我们使用 ObjectDataSource 控件，这称为`ProductsBLL`类的`GetProducts()`方法。 使用 SqlDataSource，但是，`Select()`方法建立与指定的数据库和问题`SelectCommand`(`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`，在此示例中)。 SqlDataSource 返回其结果可 GridView 然后枚举，在返回每个数据库记录 GridView 中创建一行。

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>内置数据 Web 控件功能和 SqlDataSource 控件

通常，功能所固有的数据 Web 控件分页、 排序、 编辑、 删除、 插入，等特定于数据 Web 控件和不依赖于使用的数据源控件。 也就是说，GridView 可以利用其内置分页、 排序、 编辑和删除是否绑定到对象数据源或 SqlDataSource。 但是，某些数据 Web 控件功能是写到正在使用的数据源控件或数据源控件的配置的。

例如，在[有效地分页通过大数量的数据](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)教程中我们讨论了如何，默认情况下，Web 的数据的分页逻辑控制段返回*所有*从基础的记录数据源，然后显示仅给定当前页索引和要每页显示的记录数的记录的相应子集。 分页通过足够大的结果集时，此模型是效率非常低。 幸运的是，可以配置 ObjectDataSource 为支持自定义分页，它将返回仅可显示的记录的精确子集。 SqlDataSource 控件，但是，缺少的属性实现自定义分页。

通过 SqlDataSource，会出现另一种微妙之处使用分页和排序。 默认情况下，可以分页或排序通过 GridView 从 SqlDataSource 返回的数据。 若要演示此操作，检查 GridView s 中的智能标记中的启用分页和启用排序选项`Querying.aspx`并验证这是否按预期方式工作。

排序和分页有效，因为 SqlDataSource 到松散类型化数据集检索的数据库数据。 可以从数据集已确定的总记录数由查询返回一个必不可少的方面实现分页。 此外，数据集的结果可以通过 DataView 进行排序。 这些功能会自动使用 SqlDataSource GridView 请求分页或排序后的数据时。

SqlDataSource 可以配置为通过更改返回而不是数据集 DataReader 及其[`DataSourceMode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)从`DataSet`（默认值） 到`DataReader`。 使用 DataReader 可能被首选的情况下将 SqlDataSource 的结果传递到需要 DataReader 的现有代码时。 此外，由于 DataReaders 是相当简单对象比数据集，它们提供更好的性能。 如果进行此更改，但是，数据 Web 控件可以既不进行排序，也因为 SqlDataSource 不能确定查询，返回多少条记录，也不 DataReader 的页提供对返回的数据进行排序的任何方法。

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>步骤 4： 使用自定义 SQL 语句或存储过程

在配置 SqlDataSource 控件，用于返回数据的查询可以指定两种方法之一用作自定义 SQL 语句或存储的过程，或从现有的表或视图的列。 在步骤 2 中，我们探讨选择中的列`Products`表。 让我们来看如何使用自定义 SQL 语句。

添加到另一个 GridView 控件`Querying.aspx`页上，选择创建新的数据源，从下拉列表中的智能标记。 接下来，指示，数据将会从数据库中提取这将创建一个新的 SqlDataSource 控件。 将控件`ProductsWithCategoryInfoDataSource`。


![创建一个名为 ProductsWithCategoryInfoDataSource 的新 SqlDataSource 控件](querying-data-with-the-sqldatasource-control-cs/_static/image18.gif)

**图 12**： 创建一个名为的新 SqlDataSource 控件 `ProductsWithCategoryInfoDataSource`


下一个屏幕要求我们指定的数据库。 与我们回到在图 7 中，选择`NORTHWINDConnectionString`从下拉列表中，单击下一步。 在配置 Select 语句屏幕，选择指定自定义 SQL 语句或存储的过程单选按钮，然后单击下一步。 此时会弹出定义自定义语句或存储过程的屏幕，其中提供标有 SELECT、 UPDATE、 INSERT 和 DELETE 的选项卡。 在每个选项卡可以在文本框中输入自定义 SQL 语句，或从下拉列表中选择存储的过程。 在本教程介绍如何输入自定义 SQL 语句;下一教程包括使用存储的过程的示例。


![输入自定义 SQL 语句，或选择存储的过程](querying-data-with-the-sqldatasource-control-cs/_static/image19.gif)

**图 13**： 输入自定义 SQL 语句，或选择存储的过程


自定义 SQL 语句可以手动输入到 textbox 或可以通过单击查询生成器按钮以图形方式构造。 从查询生成器或文本框中，使用以下查询返回`ProductID`并`ProductName`字段从`Products`表可使用`JOIN`检索产品 s`CategoryName`从`Categories`表：


[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample4.sql)]


![您可以以图形方式构造查询使用查询生成器](querying-data-with-the-sqldatasource-control-cs/_static/image20.gif)

**图 14**： 你可以以图形方式构造查询使用查询生成器


指定的查询之后, 单击下一步转到测试查询屏幕。 单击完成以完成 SqlDataSource 向导。

完成向导后，GridView 将已添加到它显示三个 BoundFields `ProductID`， `ProductName`，和`CategoryName`从查询返回和生成的以下声明性标记中的列：


[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample5.aspx)]


[![GridView 显示每个产品的 ID、 名称和关联的类别名称](querying-data-with-the-sqldatasource-control-cs/_static/image22.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image21.gif)

**图 15**： 根据 GridView 显示了每个产品的 ID、 名称和关联的类别名称 ([单击以查看实际尺寸的图像](querying-data-with-the-sqldatasource-control-cs/_static/image23.gif))


## <a name="summary"></a>总结

在本教程中我们已了解如何查询和使用 SqlDataSource 控件显示数据。 对象数据源，例如 SqlDataSource 充当代理，提供声明性方法进行访问的数据。 其属性指定要连接到的数据库和 SQL`SELECT`要执行的查询; 通过属性窗口或使用配置数据源向导可以指定它们。

`SELECT`查询示例本教程中，我们探讨从指定的查询返回的所有记录。 SqlDataSource 控件，但是，可以包括`WHERE`子句和参数的值将以编程方式分配，或从指定的数据源自动提取。 我们将介绍如何创建并在下一教程中使用参数化的查询 ！

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问关系数据库数据](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 控件概述](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 快速入门教程： SqlDataSource 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config`<connectionStrings>`元素](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [数据库连接字符串引用](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Susan Connery、 伯纳黛特 Leigh 和 David Suru。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一篇](using-parameterized-queries-with-the-sqldatasource-cs.md)
