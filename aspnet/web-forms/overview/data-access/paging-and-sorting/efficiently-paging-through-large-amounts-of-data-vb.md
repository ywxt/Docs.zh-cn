---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: 通过大量的数据 (VB) 有效分页 |Microsoft Docs
author: rick-anderson
description: 使用大量的数据，作为其基础数据源控件 retriev 时，数据呈现控件的默认分页选项是不合适...
ms.author: aspnetcontent
ms.date: 08/15/2006
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b00e18287bdb791a353b7ebd1bbb6cc0ab586b5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805501"
---
<a name="efficiently-paging-through-large-amounts-of-data-vb"></a>有效分页通过大量数据 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe)或[下载 PDF](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> 默认分页选项的数据呈现控件是不合适时使用的大量数据，当其基础数据源控件中检索所有记录，即使显示数据的子集。 在这种情况下，我们必须将与自定义分页。


## <a name="introduction"></a>介绍

如我们在前面的教程中所述，可以通过两种方式之一中实现分页：

- **默认的分页**可以通过只需选中启用分页选项中的数据 Web 控件 s 智能标记; 但是，只要查看的数据页，ObjectDataSource 检索*所有*的记录，即使但在页中显示它们的子集
- **自定义分页**提高了默认通过从需要为所请求的用户数据的特定页显示的数据库中检索仅这些记录分页但是，自定义分页涉及更多工作才能实现比默认的分页

由于实现只需检查一个复选框，并重新容易完成 ！ 默认分页是一个不错的选择。 其 na ve 方法中检索所有记录，但它并不可信的选择时非常与许多并发用户进行分页的数据或站点足够大的量。 在这种情况下，我们必须将自定义分页才能提供响应的系统。

自定义分页的挑战能够编写返回精确的所需的特定数据页的记录集的查询。 幸运的是，Microsoft SQL Server 2005 提供了一个新的关键字为排名结果，这使我们能够编写可以高效地检索记录的正确子集的查询。 在本教程中我们将了解如何使用此新的 SQL Server 2005 关键字 GridView 控件中实现自定义分页。 自定义分页的用户界面是相同的默认分页，单步执行从一个页面到下一步使用自定义分页可以比默认的分页是几个数量级。

> [!NOTE]
> 由自定义分页表现出的确切的性能提升取决于正在通过用寻呼发送的记录和数据库服务器施加的负载的总数。 在本教程末尾我们将介绍某些展示通过自定义分页而获得的性能优势的粗略度量值。


## <a name="step-1-understanding-the-custom-paging-process"></a>步骤 1： 了解自定义分页过程

时分页浏览数据，在页面中显示的精确记录，取决于所请求的数据的页和每页显示的记录数。 例如，假设我们想要通过 81 产品页上显示每页 10 种产品。 查看第一个页面时，我们 d 希望产品 1 到 10;查看第二页时 d 我们感兴趣的产品 11 到 20，依次类推。

有三个变量指示需要检索的记录和分页界面的呈现方式的：

- **起始行索引**要显示的数据页中的第一行的索引，通过乘以记录每页显示的页索引并添加一个计算该索引可以。 例如，当分页浏览记录 10 次，第一页 （页索引为 0），开始的行索引为 0 \* 10 + 1 或 1; 第二页 （页索引为 1），开始的行索引为 1 \* 10 + 1或 11。
- **最大行数**的最大可显示每页的记录数。 此变量称为最大行数，因为过去页有可能是更少的页大小比返回的记录。 例如，通过每个页面的 81 产品 10 记录分页，当第九个和最后一页将具有只是一条记录。 但是，任何页上，将不显示比最大行数的值的更多记录。
- **总记录计数**正在通过用寻呼发送的记录总数。 确定要检索的某一给定页的记录所需的该变量并不是 t，尽管它 does 规定的分页界面。 例如，如果有 81 正在通过换种产品，分页界面知道在分页用户界面中显示九个页码。

使用默认分页开始的行索引将计算为产品的页索引和页大小加 1，而最大行数是只是页面大小。 由于默认的分页检索所有从记录是已知数据库呈现任何数据页中，每个行的索引时，从而使移动到一个简单的任务的开始行索引行。 此外，总记录计数是易于使用，因为它 s 只需在 DataTable （或任何对象用于存储数据库结果） 中的记录数。

给定的起始行索引和最大行数的变量，自定义分页实现必须仅返回后的起始处开始的行索引和最多记录的最大行数的记录的精确的子集。 自定义分页提供了两个质询：

- 我们必须能够有效地将行索引，以便我们可以开始返回指定的开始行索引处的记录通过正在分页的全部数据中的每一行与相关联
- 我们需要提供正在通过用寻呼发送的记录总数

在接下来两个步骤中，我们将检查这些两个质询响应所需的 SQL 脚本。 除了 SQL 脚本，我们还需要在 DAL 和 BLL 中实现方法。

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>步骤 2： 返回正在通过用寻呼发送的记录总数

我们说明如何检索精确子集的记录所显示的页面之前，让 s 首先看一下如何返回正在通过用寻呼发送的记录总数。 为了正确配置的分页用户界面时需要此信息。 可以通过使用获取特定的 SQL 查询返回的记录总数[`COUNT`聚合函数](https://msdn.microsoft.com/library/ms175997.aspx)。 例如，若要确定中的记录总数`Products`表中，我们可以使用以下查询：


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

让我们来添加方法以返回此信息我们 DAL。 具体而言，我们将创建一个名为 DAL 方法`TotalNumberOfProducts()`，可执行`SELECT`如上所示的语句。

首先打开`Northwind.xsd`中的类型化数据集文件`App_Code/DAL`文件夹。 接下来，右键单击`ProductsTableAdapter`在设计器中，然后选择添加查询。 正如我们已看到在上一教程中，这将使我们能够将新方法添加到 DAL，调用时，将执行特定 SQL 语句或存储的过程。 与我们在前面的教程的 TableAdapter 方法，在此选择使用临时 SQL 语句。


![使用临时 SQL 语句](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**图 1**： 使用临时 SQL 语句


在下一个屏幕中，我们可以指定哪些类型的查询来创建。 由于此查询将返回单个标量值中的记录总数`Products`表选择`SELECT`表示返回单个值选项。


![配置要使用返回单个值的 SELECT 语句的查询](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**图 2**： 配置要使用返回单个值的 SELECT 语句的查询


指示要使用的查询类型之后, 我们接下来必须指定的查询。


![使用从产品查询选择 COUNT(*)](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**图 3**： 使用选择的计数 (\*) FROM 产品查询


最后，指定该方法的名称。 使用前面提到，可让 s `TotalNumberOfProducts`。


![命名为 DAL 方法 TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**图 4**： 命名为 DAL 方法 TotalNumberOfProducts


单击完成之后, 该向导将添加`TotalNumberOfProducts`对 DAL 的方法。 DAL 中的标量返回方法返回 null 的类型，如果 SQL 查询的结果是`NULL`。 我们`COUNT`查询，但是，将始终返回非`NULL`值; 无论如何，DAL 方法将返回一个可以为 null 的整数。

除了 DAL 方法中，我们还需要在 BLL 中的方法。 打开`ProductsBLL`类文件，并添加`TotalNumberOfProducts`方法，只需向下调用 DAL s`TotalNumberOfProducts`方法：


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

DAL s`TotalNumberOfProducts`方法返回一个可以为 null 的整数; 但是，我们创建的 ve`ProductsBLL`类的`TotalNumberOfProducts`方法，以便它返回标准的整数。 因此，我们需要能够`ProductsBLL`类 s`TotalNumberOfProducts`方法返回的 DAL s 返回的可以为 null 的整数的值部分`TotalNumberOfProducts`方法。 在调用`GetValueOrDefault()`返回的值可为 null 的整数，如果存在; 如果可以为 null 的整数`null`，但是，它将返回默认的整数值为 0。

## <a name="step-3-returning-the-precise-subset-of-records"></a>步骤 3： 返回记录的精确的子集

我们的下一个任务是在 DAL 和 BLL 接受开始的行索引的创建方法和最大行数变量前面所述，并返回相应的记录。 在此之前，让 s 先来看一下所需的 SQL 脚本。 我们面临的挑战是，我们必须能够有效地分配到整个结果，以便我们可以返回从开始处开始的行索引 （和最多的记录的最大记录数） 仅对这些记录正在换通过中的每一行的索引。

如果已存在一个列用作行索引的数据库表中，这不是一个挑战。 乍一看我们可能会认为`Products`表 s`ProductID`字段便已足够，因为第一个产品有`ProductID`为 1，2，第二个，依此类推。 但是，删除产品会使序列，其此方法中的存在间隔。

有两种常规方法用于有效地将行索引相关联的数据进行分页，从而允许通过记录要检索的精确子集：

- **使用 SQL Server 2005 s`ROW_NUMBER()`关键字**到 SQL Server 2005 新`ROW_NUMBER()`关键字将排名基于某个排序每个返回的记录与相关联。 此排名可用作每个行的行索引。
- **使用表变量和`SET ROWCOUNT`**  SQL Server s [ `SET ROWCOUNT`语句](https://msdn.microsoft.com/library/ms188774.aspx)可用于指定查询应终止; 之前处理的总记录数[表变量](http://www.sqlteam.com/item.asp?ItemID=9454)akin 到可以保存表格数据的本地 T-SQL 变量[临时表](http://www.sqlteam.com/item.asp?ItemID=2029)。 这种方法同样适用于 Microsoft SQL Server 2005 和 SQL Server 2000 (而`ROW_NUMBER()`的方法仅适用于 SQL Server 2005)。  
  
  这里的思路是，创建具有一个表变量`IDENTITY`列和通过换其数据时的表的主键列。 接下来，通过调其数据时的表的内容转储到表变量，从而将连续的行索引相关联 (通过`IDENTITY`列) 的表中每个记录。 一旦填充表变量，`SELECT`语句对表变量中，与基础表联接，可执行以拉出特定记录。 `SET ROWCOUNT`语句用于智能地限制需要被转储到表变量的记录数。  
  
  此方法的效率取决于所请求的页号为`SET ROWCOUNT`值分配的值开始的行索引以及最大行数。 分页浏览如第一个编号较低的页数据的若干页时这种方法是非常有效。 但是，它展示默认类似于分页的性能时检索快要结束页。

本教程通过实现自定义分页使用`ROW_NUMBER()`关键字。 有关使用表变量的详细信息和`SET ROWCOUNT`技术，请参阅[多个有效的方法对于分页通过大型结果集](http://www.4guysfromrolla.com/webtech/042606-1.shtml)。

`ROW_NUMBER()`关键字与上一特定的排序方式使用以下语法返回每个记录相关联排名：


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` 返回一个数字值，指定每个记录方面指示排序的排名。 例如，若要查看每个产品，按照从最顺序排列的排名代价高昂的最少，我们可以使用以下查询：


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

图 5 显示了此查询的结果通过 Visual Studio 中的查询窗口运行时。 请注意，订购价格，以及每个行的价格排位的产品。


![价格排名所包含的每个返回的记录](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**图 5**: 价格排名所包含的每个返回的记录


> [!NOTE]
> `ROW_NUMBER()` 只有一种新的多个排名函数是在 SQL Server 2005 中可用。 有关更全面的讨论`ROW_NUMBER()`，以及其他排名函数，读取[Microsoft SQL Server 2005 返回排名结果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)。


当由指定排名结果`ORDER BY`中的列`OVER`子句 (`UnitPrice`，在上面的示例)，SQL Server 必须对结果进行排序。 这是一种快捷操作，如果有聚集的索引的列的结果排序，通过，或者如果没有覆盖索引，但可以否则成本更高。 若要帮助我们改进足够大的查询的性能，请考虑添加按对结果排序所依据的列的非聚集索引。 请参阅[排名函数和 SQL Server 2005 中的性能](http://www.sql-server-performance.com/ak_ranking_functions.asp)有关性能注意事项的更详细信息。

返回的排名信息`ROW_NUMBER()`不能直接用于`WHERE`子句。 但是，派生的表可以用于返回`ROW_NUMBER()`结果，然后可以出现在`WHERE`子句。 例如，以下查询使用派生的表与返回产品名称和单价列中，`ROW_NUMBER()`结果，然后使用`WHERE`子句仅返回其价格排名的那些产品将 11 到 20 之间：


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

扩展此概念有点延伸远，我们可以利用这种方法来检索给定的所需的起始行索引和最大行值的数据的特定页面：


[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> 正如在本教程中，我们将看到的更高版本上*`StartRowIndex`* 提供的对象数据源编制索引的索引从零，开始而`ROW_NUMBER()`返回 SQL Server 2005 值编制索引的索引从 1 开始。 因此，`WHERE`子句将返回这些记录其中`PriceRank`严格大于*`StartRowIndex`* 且小于或等于*`StartRowIndex`*  + *`MaximumRows`*.


现在，我们已讨论过如何`ROW_NUMBER()`可以是用于检索给定的起始行索引和最大行数的值的数据的特定页，我们现在需要实现此逻辑作为 DAL 和 BLL 中的方法。

创建此查询，我们必须决定在排序时的结果将被排名;让我们来按其名称的字母顺序对产品进行排序。 这意味着，如果使用自定义分页实现在本教程中我们将不是能够创建自定义分页的报表，不是还可以进行排序。 在下一步的教程中，不过，我们将了解如何可以提供此类功能。

在上一部分中我们创建 DAL 方法作为临时 SQL 语句。 遗憾的是，使用 TableAdapter 向导不等的 Visual Studio 中的 T-SQL 分析器`OVER`使用语法`ROW_NUMBER()`函数。 因此，我们必须为存储过程来创建此 DAL 方法。 从视图菜单 （或命中的 Ctrl + Alt + S） 中选择服务器资源管理器并展开`NORTHWND.MDF`节点。 若要添加新的存储的过程，右键单击存储过程节点并选择添加新的存储过程 （请参阅图 6）。


![添加新的存储的过程通过产品的分页](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**图 6**： 添加新的存储的过程通过产品的分页


此存储的过程应接受两个整数输入的参数的`@startRowIndex`并`@maximumRows`，并使用`ROW_NUMBER()`函数按排序`ProductName`字段中，返回大于指定的那些行`@startRowIndex`和小于或等于`@startRowIndex`  +  `@maximumRow` s。 到新的存储过程中输入以下脚本，然后单击保存图标以将存储的过程添加到数据库。


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

在创建后的存储的过程，请花费片刻时间对它进行测试。右键单击`GetProductsPaged`存储的过程中在服务器资源管理器的名称并选择执行选项。 Visual Studio 随后会提示您为输入参数`@startRowIndex`和`@maximumRow`s （请参阅图 7）。 请尝试不同的值，并检查结果。


![输入一个值@startRowIndex和@maximumRows参数](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>图 7</strong>： 输入一个值@startRowIndex和@maximumRows参数


之后选择这些输入参数值，输出窗口将显示结果。 图 8 显示了两个 10 中传递时的结果`@startRowIndex`和`@maximumRows`参数。


[![返回记录，将显示在第二个数据页](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**图 8**： 返回记录，将显示在第二个数据页 ([单击以查看实际尺寸的图像](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png))


与此存储过程创建的我们已准备好创建 re`ProductsTableAdapter`方法。 打开`Northwind.xsd`类型化数据集，在中单击右键`ProductsTableAdapter`，然后选择添加查询选项。 而不是创建使用的临时 SQL 语句的查询，创建使用现有的存储的过程。


![创建使用现有的存储的过程的 DAL 方法](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**图 9**： 创建使用现有的存储的过程的 DAL 方法


接下来，我们会提示选择要调用的存储的过程。 选取`GetProductsPaged`存储过程从下拉列表。


![选择 GetProductsPaged 存储过程从下拉列表](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**图 10**： 选择 GetProductsPaged 存储过程从下拉列表


下一屏幕中，将要求您的数据类型返回的存储过程： 表格数据、 单个值或没有值。 由于`GetProductsPaged`存储的过程可以返回多个记录，指示它返回表格格式数据。


![指示存储的过程返回表格格式数据](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**图 11**： 指示存储的过程返回表格格式数据


最后，指示你想要创建的方法的名称。 与我们前面的教程中，请继续并创建方法使用这两种填充 DataTable 返回 DataTable。 第一个方法命名`FillPaged`，第二个`GetProductsPaged`。


![名称方法 FillPaged 和 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**图 12**： 名称方法 FillPaged 和 GetProductsPaged


除了创建 DAL 方法返回的产品特定页，我们还需要提供 BLL 中的此类功能。 DAL 与方法一样，BLL 的 GetProductsPaged 方法必须接受用于指定起始行索引和最大行数的两个整数输入，并且必须返回只在指定范围内的记录。 只是调用向下的到 DAL 的 GetProductsPaged 方法，就像这样在 ProductsBLL 类中创建此类的 BLL 方法：


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

可以使用任何名称为 BLL 的方法的输入参数，但是正如我们稍后将看到的选择要使用`startRowIndex`和`maximumRows`我们节省从一个额外的配置对象数据源，才能使用此方法时的工作。

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>步骤 4： 配置 ObjectDataSource 用于自定义分页

使用用于访问完整的记录的特定子集的 BLL 和 DAL 方法，我们准备就绪后，若要创建 GridView 控制其使用自定义分页的基础记录通过该页面。 首先打开`EfficientPaging.aspx`页中`PagingAndSorting`文件夹中，将 GridView 添加到页上，并将其配置为使用新的 ObjectDataSource 控件。 在我们过去的教程，我们通常必须配置为使用 ObjectDataSource`ProductsBLL`类的`GetProducts`方法。 这一次，但是，我们想要使用`GetProductsPaged`方法相反，因为`GetProducts`方法将返回*所有*数据库中的产品而`GetProductsPaged`返回只记录的特定子集。


![配置对象数据源使用 ProductsBLL 类的 GetProductsPaged 方法](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**图 13**： 配置 ObjectDataSource 使用 ProductsBLL 类的 GetProductsPaged 方法


由于我们重新创建只读的 GridView，花一点时间设置方法下拉列表中的 INSERT、 UPDATE，并删除选项卡添加到 （无）。

接下来，ObjectDataSource 向导提示我们输入的源`GetProductsPaged`s 方法`startRowIndex`和`maximumRows`输入参数值。 这些输入的参数实际上将会通过 GridView 自动，因此只需将源设置为 None 并单击完成。


![将保留为无输入的参数源](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**图 14**： 保留为无输入的参数源


完成 ObjectDataSource 向导后，命令将 BoundField 或 CheckBoxField 每个产品的数据字段包含 GridView。 随时根据需要定制 GridView 的外观。 我已选择仅显示`ProductName`， `CategoryName`， `SupplierName`， `QuantityPerUnit`，和`UnitPrice`BoundFields。 此外，配置 GridView 支持分页，通过检查其智能标记中的启用分页复选框。 更改后，GridView 和 ObjectDataSource 声明性标记应类似于下面：


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

如果在访问通过浏览器页面，但是，这个 GridView 已经没有任何地方进行查找。


![这个 GridView 已经不显示](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**图 15**： 的 GridView 是不会显示


这个 GridView 已经丢失，因为 ObjectDataSource 当前使用 0 作为值的两个`GetProductsPaged``startRowIndex`和`maximumRows`输入参数。 因此，生成的 SQL 查询返回任何记录，并因此不显示 GridView。

若要解决此问题，我们需要配置对象数据源以使用自定义分页。 这可以通过以下步骤完成：

1. **设置 ObjectDataSource s`EnablePaging`属性设置为`true`** 这会指示必须将传递给 ObjectDataSource`SelectMethod`其他两个参数： 一个用于指定开始的行索引 ([ `StartRowIndexParameterName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx))，另一个用于指定最大行数 ([`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx))。
2. **设置 ObjectDataSource s`StartRowIndexParameterName`并`MaximumRowsParameterName`属性相应地**`StartRowIndexParameterName`并`MaximumRowsParameterName`属性指示传入的输入参数的名称`SelectMethod`用于自定义分页目的。 默认情况下，这些参数名称是`startIndexRow`并`maximumRows`，这就是为什么，创建时`GetProductsPaged`方法在 BLL，我使用了这些值用于输入参数。 如果选择了使用不同的参数名称的 BLL s`GetProductsPaged`等方法`startIndex`并`maxRows`，您需要的示例设置 ObjectDataSource s`StartRowIndexParameterName`和`MaximumRowsParameterName`属性相应地 （例如为 startIndex`StartRowIndexParameterName`和最大行数为`MaximumRowsParameterName`)。
3. **设置 ObjectDataSource s [ `SelectCountMethod`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx)总数量的记录被分页通过返回的方法的名称 (`TotalNumberOfProducts`)** 回想一下，`ProductsBLL`类的`TotalNumberOfProducts`方法返回通过使用执行的 DAL 方法正在分页的记录总数`SELECT COUNT(*) FROM Products`查询。 ObjectDataSource 需要此信息以正确呈现分页界面。
4. **删除`startRowIndex`并`maximumRows` `<asp:Parameter>` ObjectDataSource s 声明性标记中的元素**在配置向导通过对象数据源时，Visual Studio 会自动添加了两个`<asp:Parameter>`元素有关`GetProductsPaged`的方法的输入参数。 通过设置`EnablePaging`到`true`，将自动传递这些参数; 如果它们也出现在声明性语法，ObjectDataSource 将尝试传递*四个*参数`GetProductsPaged`方法和两个参数`TotalNumberOfProducts`方法。 如果你忘记了以删除这些`<asp:Parameter>`元素，当访问通过浏览器，你将收到错误消息的页面： *ObjectDataSource ObjectDataSource1 找不到非泛型方法 TotalNumberOfProducts 具有参数： startRowIndex，值*。

进行这些更改后，ObjectDataSource s 声明性语法应如以下所示：


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

请注意，`EnablePaging`并`SelectCountMethod`已设置属性和`<asp:Parameter>`元素已被删除。 进行这些更改之后，图 16 所示属性窗口的屏幕的截图。


![若要使用自定义分页，配置 ObjectDataSource 控件](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**图 16**： 若要使用自定义分页，配置 ObjectDataSource 控件


进行这些更改后，请访问此页上的通过浏览器。 应会看到 10 种产品列出，请按字母顺序排序。 请花费片刻时间逐步一次一页数据。 虽然默认的分页和自定义分页之间没有可见差异从最终用户 s 角度来看，自定义分页更有效地页，通过大量的数据因为它仅检索那些需要为某一给定页显示的记录。


[![数据、 Ordered 按产品名称，是分页使用自定义分页](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**图 17**: 数据、 Ordered 按产品名称，是分页使用自定义分页 ([单击以查看实际尺寸的图像](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png))


> [!NOTE]
> 使用自定义分页，页计数值返回的 ObjectDataSource 的`SelectCountMethod`GridView 的视图状态中存储。 其他 GridView 变量`PageIndex`， `EditIndex`， `SelectedIndex`，`DataKeys`集合中，依次类推存储在*控制状态*，其中保留而不考虑 GridView 的值`EnableViewState`属性。 由于`PageCount`值被存储在回发期间使用的分页界面中包括用于将您带到最后一页的链接时使用视图状态，则必须启用 GridView 的视图状态。 （如果分页界面不包含的直接链接到最后一页上，然后你可以禁用视图状态。）


单击最后一页链接导致回发，并指示 GridView 来更新其`PageIndex`属性。 如果单击最后一页链接，GridView 会分配其`PageIndex`属性的值之一不会早于其`PageCount`属性。 使用视图状态已禁用，`PageCount`值会丢失在经过回发和`PageIndex`改为分配的最大整数值。 接下来，尝试确定的起始行索引乘以 GridView`PageSize`和`PageCount`属性。 这会导致`OverflowException`由于产品超出了允许的最大整数大小。

## <a name="implement-custom-paging-and-sorting"></a>实现自定义分页和排序

我们当前的自定义分页实现要求通过换数据时所依据的顺序指定以静态方式创建时`GetProductsPaged`存储过程。 但是，你可能已记下 GridView s 智能标记包含除了启用分页选项启用排序复选框。 遗憾的是，将排序支持添加到我们当前的自定义分页实现 GridView 仅将排序数据的当前正在查看页上的记录。 例如，如果配置 GridView 也支持分页和查看数据，第一页时按降序排序，产品名称的排序然后，它将在第 1 页上反转产品的顺序。 如图 18 所示，此类显示了墨鱼作为第一个产品时按反向字母顺序，将忽略的 71 其他产品按字母顺序; 晚墨鱼，排序排序操作中被视为第一页上的这些记录。


[![仅显示数据当前页上进行排序](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**图 18**： 仅显示数据当前页上进行排序 ([单击以查看实际尺寸的图像](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))


排序仅适用于数据的当前页后已从 BLL s 检索的数据的排序发生因为`GetProductsPaged`方法，而此方法仅返回的特定页中的记录。 若要实现正确排序，我们需要传递到排序表达式`GetProductsPaged`方法，以便返回数据的特定页之前适当排名数据。 我们将了解如何实现此目的在我们下一步的教程。

## <a name="implementing-custom-paging-and-deleting"></a>实现自定义分页和删除

如果您启用使用自定义分页技术，您会发现从最后一页中删除最后一条记录时分页的数据的 GridView 中删除功能，GridView 消失而不是适当递减 GridView 的`PageIndex`. 若要重现此错误，启用删除本教程只是我们刚刚创建的。 转到最后一页 （页 9），其中应看到一个产品，因为我们都分页通过 81 产品，每次 10 种产品。 删除此产品。

在删除最后一个产品，GridView*应*自动转到第八个页上，并使用默认的分页时，会出现此类功能。 使用自定义分页，但是，删除的最后一页的最后一个产品后 GridView 只需从屏幕上消失完全。 确切原因*为什么*发生这种情况有点超出了本教程的范围; 请参阅[从使用自定义分页 GridView 中删除最后一页上的最后一个记录](http://scottonwriting.net/sowblog/posts/7326.aspx)并与来源的低级别的详细信息此问题。 在摘要中它由于以下一系列步骤，单击删除按钮时执行的 GridView 的 s:

1. 删除的记录
2. 获取相应的记录，以显示指定`PageIndex`和 `PageSize`
3. 检查以确保`PageIndex`不超出数据源; 中的数据的页数，如果它存在，自动递减 GridView 的`PageIndex`属性
4. 绑定到 GridView 使用在步骤 2 中获取的记录的数据的相应页

此问题的根源，在步骤 2`PageIndex`时获取要显示的记录仍是使用`PageIndex`只删除其唯一记录的最后一页。 因此，在步骤 2*没有*将返回的记录，因为数据的最后一页不再包含任何记录。 然后，在步骤 3 中，GridView 认识到，其`PageIndex`属性大于数据源中的页的总数 （因为我们已删除的最后一页中的最后一个记录） 并因此减少其`PageIndex`属性。 在步骤 4 中 GridView 尝试将其本身绑定到在步骤 2 中; 检索到的数据但是，在步骤 2 中不返回任何记录，因此导致空 GridView。 使用默认的分页，此问题不是 t surface 因为在步骤 2 中*所有*从数据源中检索记录。

若要解决此问题，我们有两个选项。 第一个步骤是创建事件处理程序的 GridView s`RowDeleted`确定只需删除的页中显示多少条记录的事件处理程序。 如果出现只有一条记录，则只需删除的记录必须被最后一个，我们需要递减 GridView 的`PageIndex`。 当然，我们只想更新`PageIndex`如果删除操作是否实际成功，这可以确定通过确保`e.Exception`属性是`null`。

这种方法有效，因为它会更新`PageIndex`步骤 1 之后但在步骤 2 之前。 因此，在步骤 2 中，相应的记录集将返回。 若要实现此目的，使用以下代码：


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

备用解决方法是创建事件处理程序的 ObjectDataSource s`RowDeleted`事件，以及设置`AffectedRows`属性的值为 1。 删除在步骤 1 中 （但之前重新检索在步骤 2 中的数据） 的记录后, GridView 更新其`PageIndex`属性，如果一个或多个行受影响的操作。 但是， `AffectedRows` ObjectDataSource 通过不设置属性，因此忽略此步骤。 具有执行此步骤的一种方法是手动设置`AffectedRows`属性如果删除操作成功完成。 可以使用如下所示的代码完成此：


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

这两个这些事件处理程序的代码可在代码隐藏类的`EfficientPaging.aspx`示例。

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>默认和自定义分页的性能比较

由于自定义分页仅检索所需的记录，而返回默认的分页*所有*的每个页面，查看记录它 s 清除自定义分页，比默认的分页更有效。 但只是如何更高效是自定义分页？ 通过将从默认的分页移到自定义分页，可以查看哪种提高性能？

遗憾的是，有 s 没有一种款式满足所有在此处回答。 性能提升取决于多种因素，最突出两人是正在通过用寻呼发送的记录和负载的数字置于 web 服务器和数据库服务器之间的数据库服务器和通信通道。 对于包含少量几十个记录的小型表，性能差异可能可以忽略不计。 但是，对于大型表，具有数千个到成千上万的行，性能差异是很严重的。

我的项目[ASP.NET 2.0 与 SQL Server 2005 中的自定义分页](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)，包含一些性能测试，我运行来表现出这两种分页方法时分页通过与数据库表之间的性能差异50,000 个记录。 在这些测试中，我研究了这两个时间来执行 SQL Server 级别的查询 (使用[SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)) 并在 ASP.NET 页使用[ASP.NET 的跟踪功能](https://msdn.microsoft.com/library/y13fw6we.aspx)。 请记住，这些测试是在单个活动用户，我开发机器上运行，并因此是一百和不模拟典型网站的负载模式。 无论如何，结果说明了执行时间的默认实例和自定义分页的相对差异时使用足够大量的数据。


|  | **Avg.持续时间 （秒）** | **读取** |
| --- | --- | --- |
| **默认分页 SQL Profiler** | 1.411 | 383 |
| **自定义分页 SQL Profiler** | 0.002 | 29 |
| **默认分页 ASP.NET 跟踪** | 2.379 | *N/A* |
| **自定义分页 ASP.NET 跟踪** | 0.029 | *N/A* |


正如您所看到的检索数据的特定页所需数量累计为 354 小于读取的平均和中所花时间完成。 在 ASP.NET 页上，自定义的页面是能够接近于 1/100 中呈现<sup>th</sup>花费的时间使用默认的分页时。 请参阅[我的文章](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)对于这些结果与代码和数据库的详细信息，可以下载重现您自己的环境中的这些测试。

## <a name="summary"></a>总结

默认分页很容易做到在数据 Web 控件 s 智能标记中实现只是检查启用分页复选框，但此类简单起见，但代价是性能。 使用默认分页，当用户请求数据的任何页*所有*返回记录，即使仅极小一部分它们可能会显示。 为了应对这项性能开销，ObjectDataSource 提供了可选的分页选项自定义分页。

尽管在默认通过检索需要显示，这些记录分页 s 性能问题时改进了自定义分页它更为复杂，若要实现自定义分页的 s。 首先，必须正确 （有效地） 访问所请求的记录的特定子集编写查询。 这可以实现多种方式;在本教程中，我们探讨的一个是使用 SQL Server 2005 s 新`ROW_NUMBER()`排名的函数的结果，，并返回只是那些结果的排名处于指定范围内。 此外，我们需要添加一种方法来确定正在通过用寻呼发送的记录总数。 在创建后这些 DAL 和 BLL 方法，我们还需要配置对象数据源，以便它可以确定总记录数将被分页通过以及正确传递给 BLL 的起始行索引和最大行数的值。

实现自定义分页确实需要多个步骤，并与默认的分页不几乎一样简单，而自定义分页是必不可少的分页的数据量足够大时。 结果检查作为显示的自定义分页可以减轻秒从 ASP.NET 页呈现时间，并可由一个或多个数量级淡化数据库服务器上的负载。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](paging-and-sorting-report-data-vb.md)
> [下一页](sorting-custom-paged-data-vb.md)
