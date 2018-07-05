---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
title: 在 GridView 的页脚 (VB) 中显示的摘要信息 |Microsoft Docs
author: rick-anderson
description: 通常在汇总行中的报表的底部显示摘要信息。 GridView 控件可以包含为其单元格，我们可以 pr 的页脚行...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 41c818b7-603a-402b-8847-890a63547b6f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 4299cf7dc684c1080600789a91349011e495d391
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400634"
---
<a name="displaying-summary-information-in-the-gridviews-footer-vb"></a>在 GridView 的页脚 (VB) 中显示的摘要信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe)或[下载 PDF](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)

> 通常在汇总行中的报表的底部显示摘要信息。 GridView 控件可以包含到其单元格中我们可以以编程方式插入聚合数据的页脚行。 在本教程中我们将了解如何在此脚注行中显示聚合数据。


## <a name="introduction"></a>介绍

除了查看每个产品的价格、 库存、 单位顺序和重新排序级别上，用户可能还会对感兴趣聚合信息，如平均价格，在库存单位总数，依此类推。 此类的摘要信息通常显示底部的摘要行中的报表。 GridView 控件可以包含到其单元格中我们可以以编程方式插入聚合数据的页脚行。

此任务将向我们提供三个挑战：

1. 配置 GridView 显示其脚注行
2. 确定的汇总数据;它是如何执行操作，我们计算平均价格或库存单位的总数？
3. 将摘要数据注入到脚注行的相应单元格

在本教程中我们将了解如何解决这些难题。 具体而言，我们将创建列出的 GridView 中显示所选的类别产品的下拉列表中的类别的页面。 GridView 将包括显示平均价格和总单位数的库存数量和该类别中的产品的订购的页脚行。


[![在 GridView 的页脚行中显示摘要信息](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image1.png)

**图 1**: GridView 的页脚行中显示摘要信息 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png))


本教程中，对产品的母版/详细信息接口，其类别是基于在早期版本中介绍的概念[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教程。 如果你尚未使用过通过前面的教程，请先完成才能继续上进行此。

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>步骤 1： 添加类别 DropDownList 和产品 GridView

在以前与自己有关将摘要信息添加到 GridView 的页脚，让我们首先只需生成母版/详细信息报表。 我们已完成第一步，我们将介绍如何包含摘要数据。

首先打开`SummaryDataInFooter.aspx`页中`CustomFormatting`文件夹。 添加 DropDownList 控件并设置其`ID`到`Categories`。 接下来，单击从 DropDownList 的智能标记的选择数据源链接并选择要添加名为新 ObjectDataSource `CategoriesDataSource` ，它调用`CategoriesBLL`类的`GetCategories()`方法。


[![添加名为 CategoriesDataSource 新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image4.png)

**图 2**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png))


[![具有 ObjectDataSource 调用 CategoriesBLL 类 GetCategories() 方法](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image7.png)

**图 3**： 具有 ObjectDataSource 调用`CategoriesBLL`类的`GetCategories()`方法 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))


配置 ObjectDataSource 之后, 该向导将返回我们 DropDownList 的数据源配置向导，我们需要指定哪些数据字段值应显示和哪一种应与对应的值的下拉列表的`ListItem` s。 具有`CategoryName`显示的字段并使用`CategoryID`作为值。


[![为文本，Listitem，值分别使用类别名称和类别 id 字段](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image10.png)

**图 4**： 使用`CategoryName`并`CategoryID`字段为`Text`并`Value`有关`ListItem`s，分别 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png))


现在我们有 DropDownList (`Categories`) 的系统中列出的类别。 现在，我们需要添加一个 GridView，列出了这些属于所选类别的产品。 这样做了，不过之前, 请花费片刻时间来检查 DropDownList 的智能标记中的启用自动回发复选框。 如中所述*母版/详细信息筛选与 DropDownList*教程中，通过设置 DropDownList`AutoPostBack`属性设置为`True`将回发每次更改 DropDownList 值时页。 这将导致 GridView 来刷新，显示这些产品的新选择的类别。 如果`AutoPostBack`属性设置为`False`（默认值），更改类别不会导致回发，因此不会更新列出的产品。


[![检查在 DropDownList 的智能标记启用自动回发复选框](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image13.png)

**图 5**： 检查启用自动回发中的复选框 DropDownList 的智能标记 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png))


若要显示所选类别产品向页添加 GridView 控件。 设置 GridView`ID`到`ProductsInCategory`并将其绑定到名为新 ObjectDataSource `ProductsInCategoryDataSource`。


[![添加名为 ProductsInCategoryDataSource 新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image16.png)

**图 6**： 添加新对象数据源名为`ProductsInCategoryDataSource`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png))


配置对象数据源，以便它将调用`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。


[![具有 ObjectDataSource 调用 GetProductsByCategoryID(categoryID) 方法](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image19.png)

**图 7**： 具有 ObjectDataSource 调用`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png))


由于`GetProductsByCategoryID(categoryID)`方法采用一个输入参数，我们可以在向导的最后一步中指定参数值的源。 为了显示从所选类别产品，必须从提取的参数`Categories`DropDownList。


[![从所选类别 DropDownList 获取 categoryID 参数值](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image22.png)

**图 8**： 获取*`categoryID`* 从所选类别 DropDownList 的参数值 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))


完成向导后 GridView 将为每个产品属性具有 BoundField。 让我们来清理这些 BoundFields 以便仅`ProductName`， `UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`BoundFields 会显示。 可随意将任何字段级别设置添加到剩余 BoundFields (例如格式设置`UnitPrice`作为一种货币)。 进行这些更改后，GridView 的声明性标记应类似于下面：


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample1.aspx)]

现在我们有完全正常运行的母版/详细信息报表的显示名称、 单价、 存货单位和单位上对这些属于所选类别的产品的顺序。


[![从所选类别 DropDownList 获取 categoryID 参数值](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image25.png)

**图 9**： 获取*`categoryID`* 从所选类别 DropDownList 的参数值 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))


## <a name="step-2-displaying-a-footer-in-the-gridview"></a>步骤 2： 在 GridView 中显示页脚

GridView 控件可以显示页眉和页脚行。 这些行显示的值决定`ShowHeader`和`ShowFooter`属性，分别与`ShowHeader`默认值为`True`并`ShowFooter`到`False`。 若要只需包含在 GridView 的页脚设置其`ShowFooter`属性设置为`True`。


[![GridView 的 ShowFooter 属性设置为 True](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image28.png)

**图 10**： 设置 GridView`ShowFooter`属性设置为`True`([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png))


脚注行 GridView; 中定义的字段的每个都有一个单元格但是，这些单元格是默认情况下为空。 请花费片刻时间浏览器中查看我们的进度。 与`ShowFooter`属性现在将设置为`True`，GridView 包括一个空的页脚行。


[![GridView 现在包括脚注行](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image31.png)

**图 11**: GridView 现在包括脚注行 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png))


图 11 中的脚注行不会凸显出来，因为它具有白色背景。 让我们来创建`FooterStyle`CSS 类中`Styles.css`，指定深红色背景，然后配置`GridView.skin`外观文件中的`DataWebControls`主题要将此 CSS 类分配到 GridView`FooterStyle`的`CssClass`属性。 如果需要温习外观和主题，回头[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程。

首先，通过添加以下 CSS 类`Styles.css`:


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample2.css)]

`FooterStyle` CSS 类是在样式应用到类似`HeaderStyle`类，尽管`HeaderStyle`的背景色是种微妙之处更深和其文本以粗体显示。 此外，在页脚中的文本为右对齐; 而在标头的文本为居中。

接下来，要将此 CSS 类关联与每个 GridView 的页脚中，打开`GridView.skin`文件中`DataWebControls`主题和集`FooterStyle`的`CssClass`属性。 在此添加后文件的标记应如下所示：


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample3.aspx)]

如屏幕截图所示，这一变化使得页脚清晰地突显出来的详细信息。


[![GridView 的页脚行现在具有红色背景色](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image34.png)

**图 12**： 的 GridView 的页脚行现在具有红色背景色 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png))


## <a name="step-3-computing-the-summary-data"></a>步骤 3： 计算的汇总数据

使用 GridView 的页脚中显示，面向我们的下一个挑战是如何计算的汇总数据。 有两种方法来计算此聚合的信息：

1. 通过 SQL 查询，我们可以颁发其他查询为要计算特定类别的汇总数据的数据库。 SQL 包括大量的聚合函数以及`GROUP BY`子句以指定应通过该汇总数据的数据。 下面的 SQL 查询将恢复所需的信息：  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample4.sql)]

    当然，您可能不希望发出以下查询直接从`SummaryDataInFooter.aspx`页上，而通过创建中的方法`ProductsTableAdapter`和`ProductsBLL`。
2. 计算此信息，因为它将被添加到 GridView，如中所述[自定义格式设置基于数据的](custom-formatting-based-upon-data-cs.md)教程，GridView`RowDataBound`事件处理程序为每个行添加到 GridView 后引发一次其已数据绑定。 可以通过创建此事件的事件处理程序将是正在运行的总我们想要的值的聚合。 上次数据行已绑定到 GridView 我们有总计和用于计算平均值所需的信息。

通常，我使用了第二种方法，因为它将行程保存到数据库和数据访问层和业务逻辑层中实现的摘要功能所需的工作量，但这两种方法都能满足需求。 对于本教程让我们使用第二个选项和跟踪的累加总计使用`RowDataBound`事件处理程序。

创建`RowDataBound`事件处理程序通过在设计器中选择 GridView，单击属性窗口中的闪电形图标，双击 GridView`RowDataBound`事件。 或者，可以从 ASP.NET 代码隐藏类文件顶部的下拉列表中选择 GridView 和其 RowDataBound 事件。 这将创建名为新的事件处理程序`ProductsInCategory_RowDataBound`在`SummaryDataInFooter.aspx`页面的代码隐藏类。


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample5.vb)]

为了维护运行总和，我们需要定义事件处理程序的范围之外的变量。 创建以下四个页面级别的变量：

- `_totalUnitPrice`类型的 `Decimal`
- `_totalNonNullUnitPriceCount`类型的 `Integer`
- `_totalUnitsInStock`类型的 `Integer`
- `_totalUnitsOnOrder`类型的 `Integer`

接下来，编写代码以递增这三个变量，为每个数据行中遇到`RowDataBound`事件处理程序。


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample6.vb)]

`RowDataBound`事件处理程序首先确保我们正在处理数据行。 一旦已建立的`Northwind.ProductsRow`只需绑定到的实例`GridViewRow`对象中`e.Row`变量中存储`product`。 接下来，正在运行的总变量就会递增当前产品的相应值 1 (假设它们不包含数据库`NULL`值)。 我们跟踪的两个运行`UnitPrice`总计和的非数字`NULL``UnitPrice`记录的平均价格是这两个数字的商。

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>步骤 4： 在页脚中显示摘要数据

计算总计的摘要数据，最后一步是在 GridView 的页脚行中显示。 此任务中，也可以以编程方式通过`RowDataBound`事件处理程序。 请记住，`RowDataBound`事件处理程序触发*每个*绑定到 GridView，其中包括脚注行的行。 因此，我们可以提供了我们的事件处理程序，以显示中使用下面的代码的脚注行的数据：


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample7.vb)]

由于添加的所有数据行之后的脚注行添加到 GridView，我们可以确信，时我们已准备好将已完成的累加总计计算的脚注中显示摘要数据。 然后，最后一步是在表尾的单元格中设置这些值。

若要在特定的页脚单元格中显示文本，请使用`e.Row.Cells(index).Text = value`，其中`Cells`索引从 0 处开始。 以下代码计算平均价格 （除以的产品数量的总价格），并显示它的单位总数以及在股价图和相应的页脚单元格中的 GridView 订货量。


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample8.vb)]

图 13 显示了报表后添加此代码。 请注意如何`ToString("c")`会像一种货币格式将平均价格摘要信息。


[![GridView 的页脚行现在具有红色背景色](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image37.png)

**图 13**： 的 GridView 的页脚行现在具有红色背景色 ([单击以查看实际尺寸的图像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png))


## <a name="summary"></a>总结

显示摘要数据是常见的报表要求，并在 GridView 控件使其方便地在其脚注行中包含此类信息。 显示脚注行时 GridView`ShowFooter`属性设置为`True`并且可以在以编程方式通过设置其单元格中具有文本`RowDataBound`事件处理程序。 计算的汇总数据可通过重新查询数据库或在 ASP.NET 页面的代码隐藏类中使用代码来以编程方式计算的汇总数据。

本教程最后会探讨使用 GridView、 DetailsView 和 FormView 控件自定义格式设置。 我们的插入、 更新和删除使用这些相同的控件的数据的探索启动了我们下一步的教程。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一篇](using-the-formview-s-templates-vb.md)
