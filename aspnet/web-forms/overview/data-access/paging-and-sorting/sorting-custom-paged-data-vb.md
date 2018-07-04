---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
title: 排序自定义分页数据 (VB) |Microsoft Docs
author: rick-anderson
description: 上一教程中我们介绍了如何实现自定义分页时 presentating web 页上的数据。 在本教程中我们将了解如何扩展前面...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 4823a186-caaf-4116-a318-c7ff4d955ddc
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9921b541e0160054f080ff08468ddfc5cc92373b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363648"
---
<a name="sorting-custom-paged-data-vb"></a>排序自定义分页数据 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_VB.exe)或[下载 PDF](sorting-custom-paged-data-vb/_static/datatutorial26vb1.pdf)

> 上一教程中我们介绍了如何实现自定义分页时 presentating web 页上的数据。 在本教程中我们将了解如何扩展前面的示例中包括排序自定义分页支持。


## <a name="introduction"></a>介绍

与默认的分页，比较自定义分页可以通过几个数量级，使自定义分页事实上分页实现可以选择通过大量的数据分页时提高性能的数据分页。 实现自定义分页是比实现默认的分页，但是，尤其是在添加到组合排序更复杂。 在本教程中，我们将扩展以支持排序的前一次从示例*和*自定义分页。

> [!NOTE]
> 由于本教程基于前一次，一段时间来复制中的声明性语法开头才`<asp:Content>`元素从前面的教程的网页 (`EfficientPaging.aspx`) 并将其之间粘贴`<asp:Content>`中的元素`SortParameter.aspx`页。 请返回到的步骤 1[向编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)教程，了解复制到另一个 ASP.NET 页的功能的更多详细讨论。


## <a name="step-1-reexamining-the-custom-paging-technique"></a>步骤 1： 重新检查自定义分页方法

对于自定义分页才能正常工作，我们必须实现一些技术，可以有效地获取给定的起始行索引和最大行数参数的记录的特定子集。 有少量的可用于实现此目标的技术。 在前面的教程，我们在实现这个目的使用 Microsoft SQL Server 2005 s 新`ROW_NUMBER()`排名函数。 简单地说，`ROW_NUMBER()`排名函数将行号分配给指定的排序顺序按排名的查询返回的每个行。 然后通过返回带编号的结果的特定部分，获取记录的相应的子集。 以下查询说明了如何使用此方法返回时按排名结果按字母顺序排序编号为 11 到 20 的那些产品`ProductName`:


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample1.sql)]

此方法非常适用于使用特定的排序顺序的分页 (`ProductName`按字母顺序排列，在这种情况下)，但需要对查询进行修改，以显示按不同的排序表达式的结果。 理想情况下，上述查询可重写以使用中的参数`OVER`子句，如下所示：


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample2.sql)]

遗憾的是，参数化`ORDER BY`子句不允许。 相反，我们必须创建存储的过程接受`@sortExpression`输入的参数，但使用同一种的以下解决方法：

- 为每个可能使用; 的排序表达式编写硬编码的查询然后，使用`IF/ELSE`T-SQL 语句，以确定要执行的查询。
- 使用`CASE`语句，以提供动态`ORDER BY`表达式基于`@sortExpressio`n 输入参数; 请参阅动态排序查询结果中的部分用[的 SQL Power`CASE`语句](http://www.4guysfromrolla.com/webtech/102704-1.shtml)有关详细信息。
- 作为字符串存储过程中创建相应的查询，然后使用[`sp_executesql`系统存储过程](https://msdn.microsoft.com/library/ms188001.aspx)来执行动态查询。

每个这些解决方法有一些缺点。 第一个选项是不与其他两个因为它需要创建每个可能的排序表达式的查询，可维护。 因此，如果以后决定要将新的、 可排序的字段添加到 GridView 也需要返回并更新存储的过程。 第二种方法都有一些微妙之处按非字符串数据库列进行排序时带来性能问题，还存在与第一个相同的可维护性问题。 和第三个选项，它使用动态 SQL，引入了 SQL 注入攻击的风险，如果攻击者能够执行存储的过程在其选择的输入的参数值传递。

虽然这些方法都是完美无缺的我认为是最好的三个方法的第三个选项。 借助其使用动态 SQL，它提供某种程度的灵活性另外两个不这样做。 此外，如果攻击者能够执行在其选择的输入参数中传递该存储的过程可能仅利用 SQL 注入攻击。 由于 DAL 使用参数化的查询，ADO.NET 会保护发送到数据库中通过体系结构，这些参数，这意味着如果攻击者可以直接执行存储的过程，仅存在 SQL 注入攻击漏洞。

若要实现此功能，在名为 Northwind 数据库中创建新的存储的过程`GetProductsPagedAndSorted`。 此存储的过程应接受三个输入参数： `@sortExpression`，输入的参数的类型`nvarchar(100`)，用于指定如何将结果应进行排序和后直接注入`ORDER BY`中的文本`OVER`子句; 并且`@startRowIndex`并`@maximumRows`，从相同的两个整数输入的参数`GetProductsPaged`存储过程检查在前面的教程。 创建`GetProductsPagedAndSorted`存储过程中使用以下脚本：


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample3.sql)]

存储的过程启动，确保值为`@sortExpression`指定参数。 如果缺少，结果进行排名的`ProductID`。 接下来，构造动态 SQL 查询。 请注意这里的动态 SQL 查询从我们用来从 Products 表中检索所有行的上一个查询会稍有不同。 在之前示例中，我们获取每个产品 s 关联的类别和供应商的名称使用子查询。 做出此决定是回到[创建数据访问层](../introduction/creating-a-data-access-layer-vb.md)教程和已完成而非使用`JOIN`s 因为 TableAdapter 不能自动创建的关联的插入、 更新和删除此类方法查询。 `GetProductsPagedAndSorted`存储的过程，但是，必须使用`JOIN`s，结果才会按类别或供应商名称进行排序。

此动态查询旨在通过串联静态查询部分和`@sortExpression`， `@startRowIndex`，和`@maximumRows`参数。 由于`@startRowIndex`和`@maximumRows`整数参数，它们都必须转换为 nvarchar 为了正确连接。 一旦此动态 SQL 查询构造完成后，它执行通过`sp_executesql`。

请花费片刻时间来测试不同的值与此存储的过程`@sortExpression`， `@startRowIndex`，和`@maximumRows`参数。 从服务器资源管理器，右键单击存储的过程名称并选择执行。 此时会弹出运行存储过程对话框中，可以在其中输入 （请参阅图 1） 的输入的参数。 若要对结果进行排序的类别名称，使用为 CategoryName`@sortExpression`参数值; 若要按供应商的公司名称进行排序，请使用公司名称。 提供的参数值之后, 单击确定。 在输出窗口中显示结果。 图 2 显示了结果时排序时，返回产品排名 11 到 20`UnitPrice`降序排序。


![对于存储的过程 s 三个输入参数尝试不同的值](sorting-custom-paged-data-vb/_static/image1.png)

**图 1**： 尝试不同的值对于存储的过程 s 三个输入参数


[![存储过程的结果显示在输出窗口](sorting-custom-paged-data-vb/_static/image3.png)](sorting-custom-paged-data-vb/_static/image2.png)

**图 2**: 存储过程的结果显示在输出窗口 ([单击以查看实际尺寸的图像](sorting-custom-paged-data-vb/_static/image4.png))


> [!NOTE]
> 当由指定排名结果`ORDER BY`中的列`OVER`子句，SQL Server 必须对结果进行排序。 这是一种快捷操作，如果有聚集的索引的结果的排序的列通过，或者如果没有覆盖索引，但可以否则成本更高。 若要提高足够大的查询的性能，请考虑添加按对结果排序所依据的列的非聚集索引。 请参阅[排名函数和 SQL Server 2005 中的性能](http://www.sql-server-performance.com/ak_ranking_functions.asp)的更多详细信息。


## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>步骤 2： 扩充数据访问和业务逻辑层

使用`GetProductsPagedAndSorted`创建的存储的过程，我们下一步是提供一种方法来执行该存储的过程通过我们的应用程序体系结构。 这需要将适当的方法添加到 DAL 和 BLL。 让我们来首先添加对 DAL 的一种方法。 打开`Northwind.xsd`类型化数据集，右键单击`ProductsTableAdapter`，并从上下文菜单中选择添加查询选项。 与我们在前面的教程中，我们想要配置此新的 DAL 方法以使用现有的存储的过程- `GetProductsPagedAndSorted`，在这种情况下。 首先，该值指示你想要使用现有的存储的过程的新的 TableAdapter 方法。


![选择使用现有的存储的过程](sorting-custom-paged-data-vb/_static/image5.png)

**图 3**： 选择使用现有的存储的过程


若要指定要使用的存储的过程，请选择`GetProductsPagedAndSorted`下一个屏幕中的存储过程从下拉列表。


![使用 GetProductsPagedAndSorted 存储过程](sorting-custom-paged-data-vb/_static/image6.png)

**图 4**： 使用 GetProductsPagedAndSorted 存储过程


此存储的过程返回一组记录，因为其结果，在下一屏幕中，指示它返回表格格式数据。


![指示存储的过程返回表格格式数据](sorting-custom-paged-data-vb/_static/image7.png)

**图 5**： 指示存储的过程返回表格格式数据


最后，创建 DAL 方法使用这两个填充的 DataTable，并返回 DataTable 模式、 命名方法`FillPagedAndSorted`和`GetProductsPagedAndSorted`分别。


![选择的方法名称](sorting-custom-paged-data-vb/_static/image8.png)

**图 6**： 选择方法名称


现在，我们已扩展 DAL，我们准备好向 BLL。 打开`ProductsBLL`类文件并添加新方法， `GetProductsPagedAndSorted`。 此方法必须接受三个输入参数`sortExpression`， `startRowIndex`，并`maximumRows`并应只需向下调用 DAL s 到`GetProductsPagedAndSorted`方法，如下所示：


[!code-vb[Main](sorting-custom-paged-data-vb/samples/sample4.vb)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>步骤 3： 配置 SortExpression 参数中传递到 ObjectDataSource

要包括使用的方法的 DAL 和 BLL 无扩充`GetProductsPagedAndSorted`存储的过程，所有剩余的是配置中的 ObjectDataSource`SortParameter.aspx`页以使用新的 BLL 方法并传入`SortExpression`参数基于用户已请求的结果进行排序的列。

首先更改 ObjectDataSource s`SelectMethod`从`GetProductsPaged`到`GetProductsPagedAndSorted`。 这可以通过配置数据源向导，从属性窗口中，或直接通过声明性语法。 接下来，我们需要为 ObjectDataSource s 提供值[`SortParameterName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)。 如果设置此属性，尝试传入 GridView 的 ObjectDataSource`SortExpression`属性设置为`SelectMethod`。 具体而言，ObjectDataSource 查找的输入参数，其名称是等于的值`SortParameterName`属性。 由于 BLL s`GetProductsPagedAndSorted`方法具有名为排序表达式输入的参数`sortExpression`，设置 ObjectDataSource 的`SortExpression`sortExpression 属性。

以后进行这两项更改，ObjectDataSource s 声明性语法看起来应类似于下面：


[!code-aspx[Main](sorting-custom-paged-data-vb/samples/sample5.aspx)]

> [!NOTE]
> 如前面的教程中，确保 ObjectDataSource*不*SelectParameters 集合中包括的 sortExpression、 startRowIndex 或值的输入的参数。


若要启用在 GridView 中进行排序，只需选中 GridView s 智能标记，这会设置 GridView s 中的启用排序复选框`AllowSorting`属性设置为`true`，导致了要作为 LinkButton 呈现每个列的标头文本。 当最终用户单击 Linkbutton 的标头之一时，才会进行回发和要经过以下步骤：

1. GridView 更新其[`SortExpression`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)的值`SortExpression`其标头链接被单击的字段
2. ObjectDataSource 调用 s 的 BLL`GetProductsPagedAndSorted`方法，传入的 GridView s`SortExpression`属性的值为 s 方法作为`sortExpression`输入的参数 (以及相应`startRowIndex`和`maximumRows`输入参数值)
3. BLL 调用 DAL 的`GetProductsPagedAndSorted`方法
4. DAL 执行`GetProductsPagedAndSorted`传递存储过程中，在`@sortExpression`参数 (连同`@startRowIndex`和`@maximumRows`输入参数值)
5. 存储的过程向 BLL，将其返回给 ObjectDataSource; 返回适当的数据子集此数据然后绑定到 GridView，呈现为 HTML，并将发送给最终用户

图 7 显示了结果排序时的第一页`UnitPrice`按升序排序。


[![对结果进行排序单价](sorting-custom-paged-data-vb/_static/image10.png)](sorting-custom-paged-data-vb/_static/image9.png)

**图 7**: 结果按单价 ([单击以查看实际尺寸的图像](sorting-custom-paged-data-vb/_static/image11.png))


尽管当前实现可以正确对按产品名称、 类别名称、 每个计价单位和单价数量对结果进行排序，尝试对结果进行排序的供应商名称结果在运行时异常 （请参阅图 8）。


![尝试对由供应商可能会导致以下运行时异常结果进行排序](sorting-custom-paged-data-vb/_static/image12.png)

**图 8**： 尝试对由供应商可能会导致以下运行时异常结果进行排序


发生此异常的原因`SortExpression`的 GridView s `SupplierName` BoundField 设置为`SupplierName`。 但是，供应商 s 中的名称`Suppliers`实际调用表`CompanyName`我们已使用别名作为此列的列名`SupplierName`。 但是，`OVER`子句由`ROW_NUMBER()`函数不能使用别名，并且必须使用实际的列名称。 因此，更改`SupplierName`BoundField 的`SortExpression`从供应商名称为公司名称 （请参阅图 9）。 如图 10 所示，此更改之后可以按结果进行排序供应商。


![将供应商名称 BoundField 的 SortExpression 更改为公司名称](sorting-custom-paged-data-vb/_static/image13.png)

**图 9**： 将供应商名称 BoundField 的 SortExpression 更改为公司名称


[![现在可以按供应商排序结果](sorting-custom-paged-data-vb/_static/image15.png)](sorting-custom-paged-data-vb/_static/image14.png)

**图 10**: 可以现在按结果进行排序供应商 ([单击以查看实际尺寸的图像](sorting-custom-paged-data-vb/_static/image16.png))


## <a name="summary"></a>总结

在前面的教程中，我们探讨的自定义分页实现所需结果打算进行排序所依据的顺序在设计时指定。 简单地说，这意味着，我们实现的自定义分页实现可能不是，一次提供排序功能。 在本教程中我们可以克服此限制了通过从第一个包含扩展存储的过程`@sortExpression`无法按其对结果进行排序的输入的参数。

创建此存储过程和 BLL 和 DAL 中创建新的方法后，我们能够实现一个 GridView，提供这两个排序和自定义分页通过配置对象数据源传入的 GridView s 当前`SortExpression`向 BLL 属性`SelectMethod`.

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Carlos Santos。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](efficiently-paging-through-large-amounts-of-data-vb.md)
> [下一页](creating-a-customized-sorting-user-interface-vb.md)
