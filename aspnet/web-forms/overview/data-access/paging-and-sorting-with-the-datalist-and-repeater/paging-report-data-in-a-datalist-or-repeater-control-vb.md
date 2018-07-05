---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
title: 分页 DataList 或 Repeater 控件 (VB) 中的报表数据 |Microsoft Docs
author: rick-anderson
description: 在 DataList 和 Repeater 都不产品/服务自动分页或排序支持时，本教程演示如何将分页支持添加到 DataList 或 Repeater...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: bbd6b7f7-b98a-48b4-93f3-341d6a4f53c0
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/paging-report-data-in-a-datalist-or-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: da3c851a8752d4ef5c210a6d8fe552412ecbc9b0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385387"
---
<a name="paging-report-data-in-a-datalist-or-repeater-control-vb"></a>分页 DataList 或 Repeater 控件 (VB) 中的报表数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_44_VB.exe)或[下载 PDF](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/datatutorial44vb1.pdf)

> 虽然 DataList 和 Repeater 都不提供自动分页或排序的支持，本教程演示如何将分页支持添加到 DataList 或 Repeater，允许更灵活的分页和数据显示接口。


## <a name="introduction"></a>介绍

分页和排序是两个非常常见的功能，在一个在线应用程序中显示数据时。 例如，搜索的一家网上书店在 ASP.NET 书籍时，可能有数百个此类书籍，但搜索结果中列出该报表列出每页的十个匹配项。 此外，可以按标题、 价格、 页数、 作者姓名等对结果进行排序。 如中所述[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程，所有都提供内置的分页支持，还可以启用一个复选框的刻度线在 GridView、 DetailsView 和 FormView 控件。 GridView 还包括排序支持。

遗憾的是，DataList 和 Repeater 都不提供自动分页或排序的支持。 在本教程中我们将介绍如何添加到 DataList 或 Repeater 分页支持。 我们必须手动创建的分页界面，显示相应的页的记录，并请记住在回发之间被访问过的网页。 虽然这里确实需要采取更多时间和代码比使用 GridView、 detailsview 和 FormView，DataList 和 Repeater 允许更灵活的分页和数据显示接口。

> [!NOTE]
> 本教程以独占方式重点分页。 在下一教程中我们要将注意力转移到添加排序功能。


## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步骤 1： 添加分页和排序教程网页

在开始本教程之前，让我们来首先请花费片刻时间以添加我们需要用于本教程中下, 一步的一个 ASP.NET 页面。 首先，创建一个新的文件夹在项目中名为`PagingSortingDataListRepeater`。 接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:

- `Default.aspx`
- `Paging.aspx`
- `Sorting.aspx`
- `SortingWithDefaultPaging.aspx`
- `SortingWithCustomPaging.aspx`


![创建 PagingSortingDataListRepeater 文件夹并添加教程 ASP.NET 页面](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image1.png)

**图 1**： 创建`PagingSortingDataListRepeater`文件夹并添加教程 ASP.NET 页面


接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。 此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并在项目符号列表中的当前部分中显示这些教程。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image3.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image2.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image4.png))


为了使显示分页和排序的教程中我们将创建的项目符号列表，我们需要将它们添加到的站点映射。 打开`Web.sitemap`文件，并使用 DataList 站点映射节点标记在编辑和删除之后添加以下标记：


[!code-xml[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image5.png)

**图 3**： 更新包括新的 ASP.NET 页面的站点图


## <a name="a-review-of-paging"></a>评审的分页

在前面的教程中，我们已了解如何通过 GridView、 DetailsView 和 FormView 控件中的数据页上。 这三个控件提供分页调用的简单窗体*默认分页*，可以通过只需选中启用分页选项中的控件 s 智能标记。 使用默认的分页，每次请求的数据页的第一页上访问或当用户导航到另一页数据的 GridView、 DetailsView，或 FormView 控件重新请求*所有*中的数据对象数据源。 它然后代码段的记录，以显示特定的一组给定请求的页索引和要每页显示的记录数。 我们讨论了中的详细信息中的默认分页[分页和排序报表数据](../paging-and-sorting/paging-and-sorting-report-data-vb.md)教程。

默认分页重新请求时为每个页面的所有记录，因为它不可行时足够大量的数据进行分页。 例如，假设使用页面大小的 10 50,000 个记录进行分页。 每次用户移到新的页上，必须检索所有 50,000 个记录从数据库中，尽管唯一十个，其中会显示。

*自定义分页*可默认分页的性能问题解决方法是获取请求的页上显示的记录只精确的子集。 在实现自定义分页时，我们必须编写高效地将返回只是正确的记录集的 SQL 查询。 我们已了解如何创建使用 SQL Server 2005 s 新查询[`ROW_NUMBER()`关键字](http://www.4guysfromrolla.com/webtech/010406-1.shtml)回到[有效地分页通过大容量数据的](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)教程。

若要实现默认的分页 DataList 或 Repeater 控件中，我们可以使用[`PagedDataSource`类](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.aspx)周围的包装器作为`ProductsDataTable`其内容将被分页。 `PagedDataSource`类具有`DataSource`可以分配给任何可枚举对象的属性和[ `PageSize` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.pagesize.aspx)并[ `CurrentPageIndex` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.currentpageindex.aspx)属性用来指示到的记录数显示每个页面和当前的页索引。 设置这些属性后`PagedDataSource`可以用作数据源的任何数据 Web 控件。 `PagedDataSource`，当枚举时，将只返回其内部的记录的相应子集`DataSource`基于`PageSize`和`CurrentPageIndex`属性。 图 4 演示的功能`PagedDataSource`类。


![PagedDataSource 包装具有可分页接口的可枚举对象](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image6.png)

**图 4**:`PagedDataSource`包装具有可分页接口的可枚举对象


`PagedDataSource`对象可以是创建和配置直接从业务逻辑层和绑定到 DataList 或 Repeater 通过对象数据源，或可以创建并配置直接在 ASP.NET 页面 + s 代码隐藏类中。 如果使用后一种方法，我们必须放弃使用 ObjectDataSource 并改为绑定到 DataList 或 Repeater 分页的数据，以编程方式。

`PagedDataSource`对象还具有属性，以支持自定义分页。 但是，我们可以绕过使用`PagedDataSource`进行自定义分页，因为我们已有的 BLL 方法的`ProductsBLL`类用于返回精确的记录，若要显示的自定义分页。

在本教程中我们将介绍在 DataList 中通过添加到新的方法来实现默认的分页`ProductsBLL`返回适当配置的类`PagedDataSource`对象。 在下一步的教程中，我们将了解如何使用自定义分页。

## <a name="step-2-adding-a-default-paging-method-in-the-business-logic-layer"></a>步骤 2： 在业务逻辑层中添加默认分页方法

`ProductsBLL`类目前有一个方法用于返回所有产品信息`GetProducts()`，另一个用于都返回起始索引处的产品的特定子集`GetProductsPaged(startRowIndex, maximumRows)`。 使用默认分页的 GridView、 DetailsView 和 FormView 控件所有使用`GetProducts()`方法来检索所有产品，但然后使用`PagedDataSource`在内部以显示记录的正确子集。 若要复制的 DataList 和 Repeater 控件使用此功能，我们可以模拟此行为在 BLL 中创建一个新的方法。

将方法添加到`ProductsBLL`类名为`GetProductsAsPagedDataSource`采用两个整数输入参数：

- `pageIndex` 若要显示，页的索引编制索引为零，并
- `pageSize` 要每页显示的记录数。

`GetProductsAsPagedDataSource` 首先检索*所有*的记录从`GetProducts()`。 然后，创建`PagedDataSource`对象，并设置其`CurrentPageIndex`并`PageSize`的传入的值的属性`pageIndex`和`pageSize`参数。 该方法最后返回此配置`PagedDataSource`:


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample2.vb)]

## <a name="step-3-displaying-product-information-in-a-datalist-using-default-paging"></a>步骤 3： 在使用默认的分页 DataList 中显示的产品信息

与`GetProductsAsPagedDataSource`方法添加到`ProductsBLL`类中，我们现在可以创建 DataList 或 Repeater 提供默认的分页。 首先打开`Paging.aspx`页中`PagingSortingDataListRepeater`文件夹，然后从工具箱拖到设计器中，设置 DataList 的拖动 DataList`ID`属性设置为`ProductsDefaultPaging`。 从 DataList s 智能标记，创建名为新 ObjectDataSource`ProductsDefaultPagingDataSource`并将其配置，以便它检索的数据使用`GetProductsAsPagedDataSource`方法。


[![创建对象数据源，并将其配置为使用 GetProductsAsPagedDataSource （） 方法](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image8.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image7.png)

**图 5**： 创建对象数据源，并将其配置为使用`GetProductsAsPagedDataSource``()`方法 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image9.png))


设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![设置下拉列表中插入、 更新和删除选项卡添加到 （无）](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image11.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image10.png)

**图 6**： 设置的下拉列表中插入、 更新和删除选项卡添加到 （无） ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image12.png))


由于`GetProductsAsPagedDataSource`方法需要两个输入的参数，该向导将提示我们为这些参数值的源。

必须在回发之间记住的页索引和页大小值。 它们可以存储在视图状态、 持久保存到在查询字符串、 会话变量中存储或记住使用某些其他方法。 对于本教程中，我们将使用查询字符串，这样做的好处是允许要设置为书签的数据的特定页面。

具体而言，使用的查询字符串字段 pageIndex 和的 pageSize`pageIndex`和`pageSize`参数，分别 （请参阅图 7）。 请花费片刻时间来设置这些参数的默认值，如赢得 t 的查询字符串值时必须存在的用户首次访问此页。 有关`pageIndex`，默认值设置为 0 （这将显示数据的第一页） 和`pageSize`的默认值为 4。


[![使用查询字符串作为源的 pageIndex 和 pageSize 参数](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image14.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image13.png)

**图 7**： 在查询字符串用作源`pageIndex`并`pageSize`参数 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image15.png))


在配置后 ObjectDataSource，Visual Studio 会自动创建`ItemTemplate`的 DataList。 自定义`ItemTemplate`以便显示产品的名称、 类别和供应商。 此外设置 DataList s`RepeatColumns`属性设置为 2，其`Width`为 100%，并将其`ItemStyle`s`Width`为 50%。 这些宽度设置将提供两个列的间距相等。

以后进行这些更改，DataList 和 ObjectDataSource 的标记看起来应类似于下面：


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample3.aspx)]

> [!NOTE]
> 因为我们不执行任何更新或删除在本教程中的功能，你可以禁用 DataList 的视图状态，以减少呈现的页面大小。


最初都不访问浏览器中，通过此页时`pageIndex`也不`pageSize`提供查询字符串参数。 因此，使用默认值为 0 和 4。 如图 8 所示，这会导致显示的前四个产品 DataList。


[![列出了第四个产品](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image17.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image16.png)

**图 8**： 列出了第四个产品 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image18.png))


没有分页界面，那里 s 当前不简单意味着用户可以导航到第二个数据页。 我们将在步骤 4 中创建分页界面。 现在，不过，分页仅可通过直接在查询字符串中指定的分页条件。 例如，若要查看的第二页，更改从浏览器的地址栏中的 URL`Paging.aspx`到`Paging.aspx?pageIndex=2`并按 Enter。 这会导致数据要显示的第二页 （请参阅图 9）。


[![显示第二个数据页](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image20.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image19.png)

**图 9**： 显示第二个页面的数据 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image21.png))


## <a name="step-4-creating-the-paging-interface"></a>步骤 4： 创建的分页界面

有各种不同的分页界面，可实现。 GridView、 DetailsView 和 FormView 控件提供四个不同的接口之间进行选择：

- **接下来上, 一**用户下, 一个或上一次移动一页。
- **下一步上, 一步中，第一个，最后一个**除了下一步和上一步按钮，该接口包含用于移动到第一个或最后一页的第一个和最后一个按钮。
- **数值**列出了中的页码分页界面，允许用户快速跳转到特定页面。
- **数值，首先上, 一次**数值的页码，除了包括用于移动到第一个或最后一页的按钮。

对于 DataList 和 Repeater 中，我们需负责决定时分页接口以及实现该功能。 这涉及到创建所需的 Web 控件在页和单击特定的分页界面按钮时显示请求的页面。 此外，可能需要禁用某些分页界面控件。 例如，查看时数据使用下一步的第一页上, 一步，首先，最后一个接口，第一个和上一步按钮，将禁用。

对于本教程，让的使用下一步上, 一步，首先上, 一次的接口。 向页面添加四个按钮 Web 控件并设置其`ID`向`FirstPage`， `PrevPage`， `NextPage`，和`LastPage`。 设置`Text`属性设置为&lt;&lt;第一， &lt; Prev、 下一步&gt;，和最后一个&gt; &gt; 。


[!code-aspx[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample4.aspx)]

接下来，创建`Click`这些按钮的每个事件处理程序。 稍后我们将添加显示请求的页面所必需的代码。

## <a name="remembering-the-total-number-of-records-being-paged-through"></a>记住通过正在分页的记录总数

无论选择的分页界面，我们需要计算，请记住通过正在分页的记录总数。 总计行计数 （结合使用页面大小） 确定多少总页数的数据将被分页通过，用于确定分页界面控件添加或启用。 在下一步、 上一步、 第一个中，最后一个接口，我们要构建的页计数使用两种方式：

- 若要确定是否我们正在查看的最后一页，在这种情况下禁用下一步和最后一个按钮。
- 如果用户单击最后一个按钮，我们需要 whisk 它们的最后一页上，后者的索引是一个小于页计数。

总行数的上限除以页大小被计算页计数。 例如，如果我们都分页浏览 79 记录与每个页面的四个记录，则页计数是 20 (79 上限 / 4)。 如果我们将数值分页界面，此信息通知我们关于多少个数字页按钮显示;如果我们分页界面包括下一步或上一次按钮，，用于确定何时禁用下一步或最后一个按钮的页计数。

如果分页界面包括最后一个按钮，它是命令性，以便单击最后一个按钮时我们可以确定最后一页索引，在回发之间记住正在通过用寻呼发送的记录总数。 若要实现此目的，创建`TotalRowCount`中仍然存在其值以查看状态的 ASP.NET 页面 + s 代码隐藏类的属性：


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample5.vb)]

除了`TotalRowCount`、 花点时间创建只读的页级属性，用于轻松访问的页索引、 页大小和页计数：


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample6.vb)]

## <a name="determining-the-total-number-of-records-being-paged-through"></a>确定正在通过用寻呼发送的记录总数

`PagedDataSource`对象返回从 ObjectDataSource s`Select()`方法中它拥有*所有*条产品记录，即使它们的子集显示 DataList 中。 `PagedDataSource` S [ `Count`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.count.aspx)返回仅将 DataList; 中显示的项目数[`DataSourceCount`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.datasourcecount.aspx)返回中的项总数`PagedDataSource`. 因此，我们需要将 ASP.NET 页面 + s`TotalRowCount`属性值的`PagedDataSource`s`DataSourceCount`属性。

若要实现此目的，创建事件处理程序的 ObjectDataSource s`Selected`事件。 在中`Selected`事件处理程序有权访问的返回值的 ObjectDataSource s`Select()`方法在此情况下， `PagedDataSource`。


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample7.vb)]

## <a name="displaying-the-requested-page-of-data"></a>显示请求的数据页

当用户单击分页界面中的按钮之一时，我们需要显示请求的数据页。 由于分页参数指定通过在查询字符串，若要显示的数据，则使用请求的页面`Response.Redirect(url)`具有 s 用户浏览器重新请求`Paging.aspx`页使用适当的分页参数。 例如，若要显示的数据的第二页，我们会将用户重定向到`Paging.aspx?pageIndex=1`。

若要实现此目的，创建`RedirectUser(sendUserToPageIndex)`方法将重定向到用户`Paging.aspx?pageIndex=sendUserToPageIndex`。 然后，从四个按钮调用此方法`Click`事件处理程序。 中`FirstPage``Click`事件处理程序，请调用`RedirectUser(0)`，以将其发送到的第一页; 在`PrevPage``Click`事件处理程序，使用`PageIndex - 1`的页索引; 为，依此类推。


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample8.vb)]

使用`Click`事件处理程序完成，可以通过单击的按钮通过分页 DataList 的记录。 请花费片刻时间来试试看 ！

## <a name="disabling-paging-interface-controls"></a>禁用分页界面控件

目前，所有四个按钮被启用而不考虑正在查看的页面。 但是，我们想要显示的最后一页时显示的数据，以及下一步和最后一个按钮的第一页时禁用第一个和上一步按钮。 `PagedDataSource`对象返回的 ObjectDataSource s`Select()`方法具有属性[ `IsFirstPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.isfirstpage.aspx)并[ `IsLastPage` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pageddatasource.islastpage.aspx) ，我们可以检查以确定是否我们正在查看数据的第一个或最后一页。

将以下代码添加到 ObjectDataSource 的`Selected`事件处理程序：


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample9.vb)]

添加此元素后，查看最后一页时，将禁用下一步和最后一个按钮时查看的第一页时，将禁用第一个和上一步按钮。

允许 s 完成分页界面通过告知用户分页的它们重新当前正在查看和存在多少总页数。 向页面添加标签 Web 控件并设置其`ID`属性设置为`CurrentPageNumber`。 设置其`Text`ObjectDataSource s 所选事件处理程序中此类的属性，它包含当前正在查看的页 (`PageIndex + 1`) 和总页数 (`PageCount`)。


[!code-vb[Main](paging-report-data-in-a-datalist-or-repeater-control-vb/samples/sample10.vb)]

图 10 显示了`Paging.aspx`首次访问时。 由于在查询字符串为空，DataList 默认显示前四个产品;第一个和上一步按钮已禁用。 单击下一步显示 （请参阅图 11） 的四个记录;第一个和上一步按钮现已启用。


[![显示第一个数据页](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image23.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image22.png)

**图 10**： 显示数据第一页 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image24.png))


[![显示第二个数据页](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image26.png)](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image25.png)

**图 11**： 显示第二个页面的数据 ([单击以查看实际尺寸的图像](paging-report-data-in-a-datalist-or-repeater-control-vb/_static/image27.png))


> [!NOTE]
> 分页界面，可以进一步增强通过允许用户指定多少页以查看每个页面。 例如，将 DropDownList 添加列表等 5、 10、 25、 50 和所有的页面大小选项。 选择页面大小，用户将需要重定向回`Paging.aspx?pageIndex=0&pageSize=selectedPageSize`。 我将保留留给读者作为练习实现此增强功能。


## <a name="using-custom-paging"></a>使用自定义分页

DataList 逐页浏览使用效率低下默认分页方法及其数据。 时分页的数据量足够大，则必须使用自定义分页。 尽管稍有不同的实现详细信息，在 DataList 中实现自定义分页背后的概念是为使用默认分页相同的。 使用自定义分页`ProductBLL`类 s`GetProductsPaged`方法 (而不是`GetProductsAsPagedDataSource`)。 如中所述[有效地分页通过大数量的数据](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md)教程中，`GetProductsPaged`必须传递要返回的行的起始行索引和最大号。 可以通过查询字符串就像一样维护这些参数`pageIndex`和`pageSize`默认分页所使用的参数。

由于有 s 没有`PagedDataSource`使用自定义分页，必须使用其他方法来确定通过以及是否正在分页的记录总数我们重新显示数据的第一个或最后一页。 `TotalNumberOfProducts()`中的方法`ProductsBLL`类返回产品通过正在分页的总数。 若要确定是否正在查看数据的第一页，检查的起始行索引如果它是零，然后查看第一页。 如果起始行索引和要返回的最大行是大于或等于正在通过用寻呼发送的记录总数正在查看的最后一页。

我们将探讨在下一教程中更详细地实现自定义分页。

## <a name="summary"></a>总结

尽管 DataList 和 Repeater 都不提供的扩展中 GridView、 DetailsView，找到框分页支持和 FormView 控件，可以非常简单地添加此类功能。 最简单的方法来实现的默认分页是包装中的产品的整个集`PagedDataSource`，然后将绑定`PagedDataSource`到 DataList 或 Repeater。 在本教程中我们添加了`GetProductsAsPagedDataSource`方法`ProductsBLL`类以返回`PagedDataSource`。 `ProductsBLL`类已经包含方法所需的自定义分页`GetProductsPaged`和`TotalNumberOfProducts`。

检索是精确的可显示的自定义分页的记录集或中的所有记录以及`PagedDataSource`对于默认的分页，我们还需要手动添加分页界面。 对于本教程中，我们将创建下一步上, 一步，首先，上次接口具有四个按钮 Web 控件。 此外，还添加标签控件显示当前页码和总页数。

在下一教程中我们将了解如何将排序支持添加到 DataList 和 Repeater。 我们还将了解如何创建 DataList 可以都分页和排序 （以及示例使用默认和自定义分页）。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Liz Shulok、 Ken Pespisa 和伯纳黛特 Leigh。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](sorting-data-in-a-datalist-or-repeater-control-cs.md)
> [下一页](sorting-data-in-a-datalist-or-repeater-control-vb.md)
