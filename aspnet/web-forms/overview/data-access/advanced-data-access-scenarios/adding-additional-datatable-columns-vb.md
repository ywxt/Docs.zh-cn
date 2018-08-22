---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: 添加其他 DataTable 列 (VB) |Microsoft Docs
author: rick-anderson
description: 使用 TableAdapter 向导时创建的类型化数据集，相应的数据表中的主数据库查询返回的列。 但有...
ms.author: aspnetcontent
ms.date: 07/18/2007
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: a36f7267591e01ac2bd552385eeb22e1fda68c6e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803228"
---
<a name="adding-additional-datatable-columns-vb"></a>添加其他 DataTable 列 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip)或[下载 PDF](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> 使用 TableAdapter 向导时创建的类型化数据集，相应的数据表中的主数据库查询返回的列。 但有时 DataTable 需要包含额外的列。 在本教程中我们了解为什么存储的过程时，建议使用我们需要其他 DataTable 列。


## <a name="introduction"></a>介绍

向类型化数据集添加 TableAdapter 时, 由 TableAdapter s 主查询确定相应的 DataTable 的架构。 例如，如果主查询返回的数据字段*A*， *B*，并*C*，DataTable 将具有三个名为的相应列*一个*，*B*，并*C*。除了其主查询 TableAdapter 可以包含附加的查询，这样一来，返回基于某个参数的数据的子集。 例如，于`ProductsTableAdapter`s 的主查询，它将返回有关所有产品的信息，它还包含等方法`GetProductsByCategoryID(categoryID)`和`GetProductByProductID(productID)`，它返回基于提供的参数的特定产品信息。

将 DataTable 的架构反映 TableAdapter s 主查询的模型也适用于所有 TableAdapter 的方法将返回相同或比主查询中指定更少的数据字段。 如果 TableAdapter 方法需要返回其他数据字段，然后我们应 DataTable 的架构也相应扩展。 在中[母版/详细信息的详细信息 DataList 使用母版记录项目符号列表](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)我们添加了一种对方法的教程`CategoriesTableAdapter`返回`CategoryID`， `CategoryName`，和`Description`中定义的数据字段加上的主查询`NumberOfProducts`，报告与每个类别相关联的产品数量的其他数据字段。 我们手动添加到一个新列`CategoriesDataTable`为了捕获`NumberOfProducts`数据字段值从这种新方法。

如中所述[将文件上载](../working-with-binary-files/uploading-files-vb.md)教程，但是必须谨慎使用 Tableadapter 使用临时 SQL 语句并具有其数据字段不会精确匹配主查询的方法。 如果重新运行 TableAdapter 配置向导，它将更新所有 TableAdapter 的方法，使其数据字段列表与匹配主查询。 因此，使用自定义的列列表的任何方法将恢复到主查询的列列表并且不返回预期的数据。 使用存储的过程时不会出现此问题。

在本教程中我们将探讨如何扩展以包括其他列的 DataTable 的架构。 由于脆弱性 TableAdapter 使用临时 SQL 语句时，在本教程中我们将使用存储的过程。 请参阅[创建新存储过程的类型化数据集 s Tableadapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)并[使用现有存储过程的类型化数据集 s Tableadapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)教程的详细信息配置 TableAdapter 以使用存储的过程。

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>步骤 1： 添加`PriceQuartile`列`ProductsDataTable`

在中*创建新存储过程的类型化数据集 s Tableadapter*教程中，我们创建名为类型化数据集`NorthwindWithSprocs`。 此数据集目前包含两个数据表：`ProductsDataTable`和`EmployeesDataTable`。 `ProductsTableAdapter`有以下三个方法：

- `GetProducts` -返回所有记录从主查询`Products`表
- `GetProductsByCategoryID(categoryID)` -返回具有指定的所有产品*categoryID*。
- `GetProductByProductID(productID)` -返回具有指定的特定产品*productID*。

主查询和两个其他方法都返回相同的数据字段，即所有的列集`Products`表。 有任何相关子查询或`JOIN`提取相关的数据的 s`Categories`或`Suppliers`表。 因此，`ProductsDataTable`对应的列中每个字段`Products`表。

对于本教程中，let s 添加到方法`ProductsTableAdapter`名为`GetProductsWithPriceQuartile`，它返回的所有产品。 除了标准产品数据字段中，`GetProductsWithPriceQuartile`还将包括`PriceQuartile`数据字段，它指示产品的价格落下的四分位数。 例如，其价格中成本最高的 25%的这些产品将具有`PriceQuartile`值为 1，而其价格分为底部 25%的那些有的值为 4。 我们担心如何创建存储的过程来返回此信息之前，但是，我们首先需要更新`ProductsDataTable`若要包括的列来保存`PriceQuartile`结果时`GetProductsWithPriceQuartile`使用方法。

打开`NorthwindWithSprocs`数据集，然后右键单击`ProductsDataTable`。 从上下文菜单中选择添加，然后选择列。


[![将新列添加到 ProductsDataTable](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**图 1**： 添加到一个新列`ProductsDataTable`([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image3.png))


这会将新列添加到名为的类型的 Column1 的 DataTable `System.String`。 我们需要更新到 PriceQuartile 和其类型设置为此列的名称`System.Int32`因为它将用于保存介于 1 和 4 之间的数字。 选择中的新添加列`ProductsDataTable`并从属性窗口中，设置`Name`属性设置为 PriceQuartile 和`DataType`属性设置为`System.Int32`。


[![设置新 s 列名和数据类型属性](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**图 2**： 设置新列 s`Name`并`DataType`属性 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image6.png))


如图 2 所示，提供了可以设置，例如是否列中的值必须是唯一的如果列是自动递增列的其他属性，该值指示是否确保数据库`NULL`值允许，依次类推。 将这些值设置为其默认值。

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>步骤 2： 创建`GetProductsWithPriceQuartile`方法

既然`ProductsDataTable`已更新以包括`PriceQuartile`列中，我们已准备好创建`GetProductsWithPriceQuartile`方法。 启动 TableAdapter 上右键单击并从上下文菜单中选择添加查询。 这将打开 TableAdapter 查询配置向导中，首先让我们是否我们要使用的临时 SQL 语句或新的或现有的存储的过程。 由于我们不尚未有一个存储的过程返回价格四分位数数据，让我们来允许 TableAdapter 来为我们创建此存储的过程。 选择创建新存储的过程选项，然后单击下一步。


[![指示 TableAdapter 向导为我们创建的存储的过程](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**图 3**： 指示 TableAdapter 向导以创建存储过程为我们 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image9.png))


在后续屏幕中，图 4 所示向导将询问我们要添加查询的类型。 由于`GetProductsWithPriceQuartile`方法将返回所有列和记录从`Products`表中，选择它将返回行选项，然后单击下一步。


[![我们的查询将 SELECT 语句，返回多个行](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**图 4**： 我们的查询将`SELECT`该返回多行语句 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image12.png))


接下来我们将提示您输入`SELECT`查询。 向导中输入以下查询：


[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

上述查询使用 SQL Server 2005 s 新[`NTILE`函数](https://msdn.microsoft.com/library/ms175126.aspx)若要将结果划分为四个组组由`UnitPrice`值降序排序。

遗憾的是，查询生成器不知道如何解析`OVER`关键字和分析上面的查询时，将显示错误。 因此，上述查询在向导中的文本框中直接输入而无需使用查询生成器。

> [!NOTE]
> 有关详细信息 NTILE 和 SQL Server 2005 s 其他排名函数，请参阅[返回包含 Microsoft SQL Server 2005 的排名结果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)并[排名函数部分](https://msdn.microsoft.com/library/ms189798.aspx)从[SQLServer 2005 联机丛书](https://msdn.microsoft.com/library/ms189798.aspx)。


输入后`SELECT`查询并单击下一步，向导将询问我们提供，它将创建该存储过程的名称。 命名新的存储的过程`Products_SelectWithPriceQuartile`单击下一步。


[![命名存储的过程 Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**图 5**： 命名存储过程`Products_SelectWithPriceQuartile`([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image15.png))


最后，我们会提示命名 TableAdapter 方法。 退出这两种填充 DataTable，并返回 DataTable 复选框选中和名称方法`FillWithPriceQuartile`和`GetProductsWithPriceQuartile`。


[![名称的 TableAdapter s 方法，然后单击完成](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**图 6**： 命名 TableAdapter 的方法并单击完成 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image18.png))


使用`SELECT`指定查询和存储的过程和 TableAdapter 方法命名，单击完成以完成向导。 此时可能会收到一条警告，或指示该向导中的两个`OVER`不支持 SQL 构造或语句。 可以忽略这些警告。

完成向导后，应包括 TableAdapter`FillWithPriceQuartile`并`GetProductsWithPriceQuartile`方法和数据库应包含一个名为的存储的过程`Products_SelectWithPriceQuartile`。 请花费片刻时间来验证 TableAdapter，确实包含这一新方法和存储的过程已正常添加到数据库。 当检查数据库，如果您看不到存储的过程尝试右键单击存储过程文件夹并选择刷新。


![验证已向 TableAdapter 添加新方法](adding-additional-datatable-columns-vb/_static/image19.png)

**图 7**： 验证是否已向 TableAdapter 添加新方法


[![请确保该数据库包含 Products_SelectWithPriceQuartile 存储过程](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**图 8**： 确保数据库包含`Products_SelectWithPriceQuartile`存储过程 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image22.png))


> [!NOTE]
> 而不临时 SQL 语句中使用存储的过程的好处之一是，重新运行 TableAdapter 配置向导将不会修改存储的过程列列表。 通过右键单击 TableAdapter 上，从上下文菜单以启动向导，选择配置选项，然后单击完成以完成它对此进行验证。 接下来，请转到该数据库并查看`Products_SelectWithPriceQuartile`存储过程。 请注意尚未修改为其列列表。 以前我们一直在使用临时 SQL 语句，重新运行 TableAdapter 配置向导将恢复此查询的列列表，以与主查询列列表，从而删除 NTILE 语句中使用的查询匹配`GetProductsWithPriceQuartile`方法。


当数据访问层 s`GetProductsWithPriceQuartile`调用方法，将执行 TableAdapter`Products_SelectWithPriceQuartile`存储过程，并将行添加到`ProductsDataTable`为每个返回的记录。 存储过程返回的数据字段映射到`ProductsDataTable`的列。 由于没有`PriceQuartile`数据字段从存储过程，返回其值分配给`ProductsDataTable`s`PriceQuartile`列。

为其查询不会返回这些 TableAdapter 方法`PriceQuartile`数据字段`PriceQuartile`列 s 的值是由指定的值及其`DefaultValue`属性。 如图 2 所示，此值设置为`DBNull`，默认值。 如果您希望不同的默认值，只需设置`DefaultValue`属性相应地。 只需确保`DefaultValue`值是有效的给定列 s `DataType` (即`System.Int32`为`PriceQuartile`列)。

现在我们已向数据表添加一个额外的列执行所需的步骤。 若要验证此附加列按预期方式工作，让我们来创建显示每个产品名称、 价格和价格四分位数的 ASP.NET 页。 在此之前，不过，我们首先需要更新业务逻辑层包括为 DAL s 向下调用的方法，`GetProductsWithPriceQuartile`方法。 我们将在步骤 3 中，接下来，更新 BLL，然后在步骤 4 中创建 ASP.NET 页面。

## <a name="step-3-augmenting-the-business-logic-layer"></a>步骤 3： 扩充业务逻辑层

我们使用新之前`GetProductsWithPriceQuartile`方法从表示层中，我们首先应添加相应的方法向 BLL。 打开`ProductsBLLWithSprocs`类文件，并添加以下代码：


[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

与中的其他数据检索方法类似`ProductsBLLWithSprocs`，则`GetProductsWithPriceQuartile`方法只是调用 DAL s 对应`GetProductsWithPriceQuartile`方法，并返回其结果。

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>步骤 4： 在 ASP.NET 网页中显示的价格四分位数信息

BLL 加准备就绪后，若要创建显示每个产品的价格四分位数的 ASP.NET 页完成我们。 打开`AddingColumns.aspx`页中`AdvancedDAL`文件夹，然后拖动 GridView 从工具箱拖到设计器中，设置其`ID`属性设置为`Products`。 从 GridView s 智能标记，请将其绑定到名为新 ObjectDataSource `ProductsDataSource`。 配置要使用 ObjectDataSource`ProductsBLLWithSprocs`类的`GetProductsWithPriceQuartile`方法。 因为这将是只读的网格，设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![配置对象数据源以使用 ProductsBLLWithSprocs 类](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**图 9**： 配置为使用 ObjectDataSource`ProductsBLLWithSprocs`类 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image25.png))


[![GetProductsWithPriceQuartile 方法中检索产品信息](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**图 10**： 从检索产品信息`GetProductsWithPriceQuartile`方法 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image28.png))


完成配置数据源向导后，Visual Studio 将自动添加 BoundField 或 CheckBoxField 到 GridView 为每个方法返回的数据字段。 其中一个数据字段是`PriceQuartile`，这是我们添加到列`ProductsDataTable`在步骤 1 中。

编辑删除的 GridView 的字段以外的所有`ProductName`， `UnitPrice`，和`PriceQuartile`BoundFields。 配置`UnitPrice`BoundField 设置其值作为一种货币的格式，并让`UnitPrice`和`PriceQuartile`BoundFields 右对齐和居中对齐，分别。 最后，更新剩余 BoundFields`HeaderText`属性设置为产品、 价格和价格的四分位数，分别。 另外，检查从 GridView s 智能标记启用排序复选框。

这些修改后的 GridView 和 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

图 11 显示了当通过浏览器访问此页。 请注意，最初，产品进行排序以降序与分配相应的每个产品及其价格`PriceQuartile`值。 当然此数据可以进行排序的其他条件与价格四分位数列仍专用于反映将与价格相关产品的排名的值 （请参阅图 12）。


[![通过其价格订购的产品](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**图 11**： 通过其价格订购的产品 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image31.png))


[![产品按其名称进行排序](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**图 12**： 按其名称进行排序的产品 ([单击以查看实际尺寸的图像](adding-additional-datatable-columns-vb/_static/image34.png))


> [!NOTE]
> 少量的代码行我们无法提供了 GridView，以便着色产品列基于其`PriceQuartile`值。 我们可能会在第一个四分位数浅绿色，第二个四分位数淡黄色中的这些产品的颜色等。 建议您花点时间来添加此功能。 如果是这样， [给我在行](../custom-formatting/custom-formatting-based-upon-data-vb.md) 。


## <a name="an-alternative-approach---creating-another-tableadapter"></a>一种替代方法-创建另一个 TableAdapter

正如我们看到在本教程中，主查询会将方法添加到 TableAdapter 返回以外的数据字段的拼写出时，我们可以将相应的列添加到 DataTable。 这种方法，但是，发挥作用，仅当有少量的 TableAdapter 中返回不同的数据字段的方法和这些备用数据字段不变得太厉害从主查询。

而不是将列添加到 DataTable，可以改为将另一个 TableAdapter 添加到包含可返回不同的数据字段的方法的第一个 TableAdapter 方法的数据集。 对于本教程中，而不是添加`PriceQuartile`列添加到`ProductsDataTable`(其中仅使用通过`GetProductsWithPriceQuartile`方法)，我们可以对名为数据集添加更多 TableAdapter`ProductsWithPriceQuartileTableAdapter`使用`Products_SelectWithPriceQuartile`存储作为其主查询的过程。 获取与价格四分位数的产品信息所需的 ASP.NET 页面将使用`ProductsWithPriceQuartileTableAdapter`，而那些没有可以继续使用`ProductsTableAdapter`。

通过添加新的 TableAdapter，DataTables 保持 untarnished 和它们的列精确地反映其 TableAdapter 的方法返回的数据字段。 但是，重复执行的任务和功能，可以引入更多 Tableadapter。 例如，如果这些 ASP.NET 页的显示`PriceQuartile`列还需要提供插入、 更新和删除支持`ProductsWithPriceQuartileTableAdapter`则需要拥有其`InsertCommand`， `UpdateCommand`，和`DeleteCommand`属性正确配置。 尽管这些属性可反映`ProductsTableAdapter`s，此配置引入了一个额外的步骤。 此外，现在有两种方法更新，请删除，或通过将产品添加到数据库-`ProductsTableAdapter`和`ProductsWithPriceQuartileTableAdapter`类。

本教程中下载内容还包括`ProductsWithPriceQuartileTableAdapter`类中`NorthwindWithSprocs`说明了此另一种方法的数据集。

## <a name="summary"></a>总结

在大多数情况下，所有的 TableAdapter 中的方法将返回组相同的数据字段，但有特定方法或两个可能的需要返回的附加字段。 例如，在[母版/详细信息的详细信息 DataList 使用母版记录项目符号列表](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)我们添加了一种对方法的教程`CategoriesTableAdapter`，，除了返回的主查询的数据字段`NumberOfProducts`字段，报告与每个类别相关联的产品数量。 在本教程中我们介绍了中的方法中添加`ProductsTableAdapter`返回`PriceQuartile`除了主查询的数据字段的字段。 若要捕获的其他数据字段返回 TableAdapter 的方法我们需要将相应的列添加到 DataTable。

如果您计划手动将列添加到 DataTable，它建议 TableAdapter 使用存储的过程。 如果 TableAdapter 使用临时 SQL 语句，任何时候 TableAdapter 配置向导会运行所有数据字段列表恢复到主查询所返回的数据字段的方法。 此问题不会扩展到存储过程，这就是为什么它们，建议使用，在本教程中使用了。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Randy Schmidt、 Jacky Goor、 伯纳黛特 Leigh 和 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](updating-the-tableadapter-to-use-joins-vb.md)
> [下一页](working-with-computed-columns-vb.md)
