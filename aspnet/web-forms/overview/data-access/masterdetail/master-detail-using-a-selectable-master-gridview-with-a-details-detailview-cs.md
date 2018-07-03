---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: 母版/详细信息可选择的母版 GridView 中使用的详细信息 DetailView (C#) |Microsoft Docs
author: rick-anderson
description: 本教程将具有的 GridView 中的行包括名称和选择按钮以及每个产品的价格。 单击选择按钮的 particu...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: e93461d566f827ff81dedf3651e7bd3d24c3583a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374932"
---
<a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>使用详细信息 DetailView (C#) 的可选母版 GridView 母版/详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe)或[下载 PDF](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> 本教程将具有的 GridView 中的行包括名称和选择按钮以及每个产品的价格。 单击某一特定产品选择按钮将导致要在同一页面上的 DetailsView 控件中显示其完整的详细信息。


## <a name="introduction"></a>介绍

在中[前一篇教程](master-detail-filtering-across-two-pages-cs.md)我们已了解如何创建使用两个 web 页面的母版/详细信息报表:"主"的 web 页面，从中我们显示供应商提供; 的列表和"详细信息"网页列出所选提供这些产品供应商。 此两个页面报告格式可以压缩到一个页面。 本教程将具有的 GridView 中的行包括名称和选择按钮以及每个产品的价格。 单击某一特定产品选择按钮将导致要在同一页面上的 DetailsView 控件中显示其完整的详细信息。


[![单击选择按钮将显示产品的详细信息](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**图 1**： 单击选择按钮将显示产品的详细信息 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png))


## <a name="step-1-creating-a-selectable-gridview"></a>步骤 1： 创建一个可选择的 GridView

回想一下，在两个页母版/详细信息报告每个主记录包含超链接，单击时，向用户发送到传递已单击的行的详细信息页`SupplierID`在查询字符串中的值。 这样的超链接添加到每个使用 HyperLinkField 的 GridView 行。 对于单个页面的母版/详细信息报表，我们将需要一个按钮，对每个 GridView 行，单击时，显示的详细信息。 可以将 GridView 控件配置为包括导致回发并将该行标记为 GridView 的每个行的选择按钮[SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)。

首先，通过添加到 GridView 控件`DetailsBySelecting.aspx`页中`Filtering`文件夹中，设置其`ID`属性设置为`ProductsGrid`。 接下来，添加名为新 ObjectDataSource `AllProductsDataSource` ，它调用`ProductsBLL`类的`GetProducts()`方法。


[![创建名为 AllProductsDataSource ObjectDataSource](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**图 2**： 创建的 ObjectDataSource 命名`AllProductsDataSource`([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))


[![使用 ProductsBLL 类](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**图 3**： 使用`ProductsBLL`类 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png))


[![配置 ObjectDataSource 调用 GetProducts() 方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**图 4**： 配置对 Invoke ObjectDataSource`GetProducts()`方法 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))


编辑删除 GridView 的字段以外的所有`ProductName`和`UnitPrice`BoundFields。 此外，随时根据需要如格式设置自定义这些 BoundFields`UnitPrice`作为一种货币 BoundField 和更改`HeaderText`BoundFields 的属性。 通过单击 GridView 的智能标记中的编辑列链接或通过手动配置的声明性语法，可以以图形方式，完成这些步骤。


[![删除除之外的所有产品名称和单价 BoundFields](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**图 5**： 删除以外的所有`ProductName`并`UnitPrice`BoundFields ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))


GridView 的最后一个标记是：


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

接下来，我们需要将标记为可选的这样会将选择按钮添加到每个行 GridView。 若要完成此操作，只需检查 GridView 的智能标记中的启用选定内容复选框。


[![确保 GridView 行选择](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**图 6**： 使 GridView 行可选 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png))


选中启用所选内容选项将添加到 CommandField `ProductsGrid` GridView 使用其`ShowSelectButton`属性设置为 True。 这会导致选择按钮每行的 GridView 中，如图 6 所示。 默认情况下，选择按钮呈现为 Linkbutton，但你可以使用按钮或 ImageButtons 改为通过 CommandField`ButtonType`属性。


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

单击某 GridView 一行的选择按钮时，才会回发和 GridView`SelectedRow`更新属性。 除了`SelectedRow`属性，提供了 GridView [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx)， [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)，并且[SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx)属性。 `SelectedIndex`属性返回所选行的索引，而`SelectedValue`并`SelectedDataKey`属性返回值基于 GridView [DataKeyNames 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)。

`DataKeyNames`属性用于将一个或多个数据字段值与每个行，并通常用于属性唯一地标识信息从基础数据与每个 GridView 行。 `SelectedValue`属性返回的值的第一个`DataKeyNames`所选行的数据字段作为 where`SelectedDataKey`属性返回所选的行`DataKey`对象，它包含的所有指定的数据键字段的值该行。

`DataKeyNames`属性自动设置为唯一标识数据字段，数据源绑定到 GridView、 detailsview 和 FormView 通过设计器时。 这些示例时设置此属性已为我们自动在前面的教程中，会不起作用`DataKeyNames`指定属性。 但是，在本教程中，可选择的 GridView 以及将来的教程中我们将检查插入、 更新和删除，`DataKeyNames`属性必须正确设置。 请花费片刻时间以确保你 GridView`DataKeyNames`属性设置为`ProductID`。

让我们查看一下我们到目前为止通过浏览器的进度。 请注意 GridView 列出的名称和所有选择的 LinkButton 以及产品的价格。 单击选择按钮会导致回发。 在步骤 2 中，我们将了解如何能够对此回发 DetailsView 响应通过显示所选产品的详细信息。


[![每个产品行包含选择 LinkButton](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**图 7**： 每个产品行包含选择 LinkButton ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png))


### <a name="highlighting-the-selected-row"></a>突出显示所选的行

`ProductsGrid` GridView 有`SelectedRowStyle`可用于指示所选行的视觉样式的属性。 使用得当，这可以通过多个清楚地显示当前选择的 GridView 的哪些行来提高用户的体验。 本教程中，让我们用黄色背景突出显示所选的行。

如我们之前的教程，让我们致力于以保存美学相关的设置定义为 CSS 类。 因此，创建一个新的 CSS 类中`Styles.css`名为`SelectedRowStyle`。


[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

若要应用到此 CSS 类`SelectedRowStyle`的属性*所有*我们教程系列中的 Gridview 编辑`GridView.skin`外观中`DataWebControls`要包括的主题`SelectedRowStyle`设置，如下所示：


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

添加此元素后，所选的 GridView 行现在已突出显示黄色背景颜色。


[![自定义所选的行的外观，可以使用 GridView 的 SelectedRowStyle 属性](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**图 8**： 使用自定义所选行的外观 GridView`SelectedRowStyle`属性 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))


## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>步骤 2： 在 DetailsView 中显示所选的产品的详细信息

使用`ProductsGrid`GridView 完成，所有要添加显示有关所选的特定产品的信息 DetailsView 就是。 添加 GridView 上面的 DetailsView 控件并创建名为新 ObjectDataSource `ProductDetailsDataSource`。 因为我们希望此 DetailsView 以显示有关所选产品的特定信息，请配置`ProductDetailsDataSource`若要使用`ProductsBLL`类的`GetProductByProductID(productID)`方法。


[![调用 ProductsBLL 类 GetProductByProductID(productID) 方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**图 9**： 调用`ProductsBLL`类的`GetProductByProductID(productID)`方法 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))


具有*`productID`* 参数的值从 GridView 控件获取`SelectedValue`属性。 如前面所述，GridView 的`SelectedValue`属性返回所选行的第一个数据键值。 因此，它是命令性的 GridView`DataKeyNames`属性设置为`ProductID`，因此，所选的行`ProductID`返回值`SelectedValue`。


[![将产品 id 参数设置为 GridView 的 SelectedValue 属性](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**图 10**： 设置*`productID`* GridView 的参数`SelectedValue`属性 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png))


一次`productDetailsDataSource`正确配置对象数据源并将其绑定到 DetailsView，本教程中已完成 ！ 当首次访问页面时未选择行，因此 GridView`SelectedValue`属性返回`null`。 由于不没有使用任何产品`NULL``ProductID`值，没有记录返回由`GetProductByProductID(productID)`方法，这意味着 DetailsView 不显示 （请参阅图 11）。 单击某 GridView 一行的选择按钮，才会进行回发和刷新 DetailsView。 这一次 GridView`SelectedValue`属性返回`ProductID`所选行的`GetProductByProductID(productID)`方法将返回`ProductsDataTable`以及有关该特定产品和 DetailsView 信息显示了这些详细信息 （请参阅图 12）。


[![第一个访问，仅 GridView 显示时](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**图 11**： 首次访问时，将显示仅 GridView ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png))


[![在选择某一行，显示产品的详细信息](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**图 12**： 在选择某一行，显示产品的详细信息 ([单击以查看实际尺寸的图像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png))


## <a name="summary"></a>总结

在此环境及前面的三个教程中，我们已经看到许多用于显示母版/详细信息报表的方法。 在本教程中，我们探讨使用可选择 GridView 来存放主记录和 DetailsView 相同页面上显示有关所选的主记录的详细信息。 在之前的教程介绍了如何显示母版/详细信息报表使用 Dropdownlist 和上一个 web 页面，详细信息记录在另一台显示主记录。

本教程最后会探讨母版/详细信息报表。 从下一步 tutorialwe 将开始我们的自定义格式设置使用 GridView、 DetailsView 和 FormView 的探索。 我们将看到如何自定义基于绑定到它们的数据在这些控件的外观、 如何汇总在 GridView 的页脚中的数据以及如何使用模板来获取更高的控制布局。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-across-two-pages-cs.md)
> [下一页](master-detail-filtering-with-a-dropdownlist-vb.md)
