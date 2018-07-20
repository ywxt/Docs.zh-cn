---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
title: 使用两个 Dropdownlist (C#) 进行筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 本教程将延伸的母版/详细信息关系添加第三个层，使用两个 DropDownList 控件来选择所需的父级和祖父录制...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: ac4b0d77-4816-4ded-afd0-88dab667aedd
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
msc.type: authoredcontent
ms.openlocfilehash: f8f216689494e0f80902c42f425883558c1e21ce
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842252"
---
<a name="masterdetail-filtering-with-two-dropdownlists-c"></a>使用两个 Dropdownlist (C#) 进行筛选母版/详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_8_CS.exe)或[下载 PDF](master-detail-filtering-with-two-dropdownlists-cs/_static/datatutorial08cs1.pdf)

> 本教程将延伸添加第三个层，使用两个 DropDownList 控件来选择所需的父级和祖父记录的母版/详细信息关系。


## <a name="introduction"></a>介绍

在中[前一篇教程](master-detail-filtering-with-a-dropdownlist-cs.md)中，我们探讨如何显示使用单个 DropDownList 填入的类别和 GridView 显示属于所选类别这些产品的简单母版/详细信息报表。 此报表模式适用于显示有一个对多关系，并且可以轻松扩展为包括多个到多关系的情况下工作的记录。 例如，订单输入系统必须与客户、 订单和订单行各项相对应的表。 给定的客户可能有多个与包含多个项的每个订单的订单。 此类数据可以显示具有两个 Dropdownlist 和 GridView 的用户。 第一个下拉列表将具有与第二个数据库中每个客户的列表项的内容正在所选客户的订单。 GridView 将列出所选订单中的行项。

虽然 Northwind 数据库包含中的规范客户/顺序/订单详细信息及其`Customers`， `Orders`，和`Order Details`表，这些表不在我们的体系结构中捕获。 尽管如此，我们仍可以说明使用两个依赖 Dropdownlist。 第一个下拉列表将列出的类别和第二个属于所选类别的产品。 在 DetailsView 将列出所选产品的详细信息。

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>步骤 1： 创建和填充类别 DropDownList

我们的第一个目标是添加列出的类别 DropDownList。 这些步骤已在前面的教程中，在详细信息中检查，但出于完整性的考虑摘要如下。

打开`MasterDetailsDetails.aspx`页中`Filtering`文件夹中，将 DropDownList 添加到页上，设置其`ID`属性设置为`Categories`，然后单击其智能标记中的配置数据源链接。 从数据源配置向导选择要添加新的数据源。


[![为 DropDownList 添加新的数据源](master-detail-filtering-with-two-dropdownlists-cs/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image1.png)

**图 1**： 为 DropDownList 添加新的数据源 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image3.png))


新的数据源正常情况下，应 ObjectDataSource。 命名此新 ObjectDataSource `CategoriesDataSource` ，并将其调用`CategoriesBLL`对象的`GetCategories()`方法。


[![选择使用 CategoriesBLL 类](master-detail-filtering-with-two-dropdownlists-cs/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image4.png)

**图 2**： 选择使用`CategoriesBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image6.png))


[![配置对象数据源使用 GetCategories() 方法](master-detail-filtering-with-two-dropdownlists-cs/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image7.png)

**图 3**： 配置为使用 ObjectDataSource`GetCategories()`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image9.png))


配置 ObjectDataSource 后我们仍然需要指定哪些数据源字段应显示在`Categories`DropDownList 和哪一种应配置为列表项的值。 设置`CategoryName`字段与显示和`CategoryID`为每个列表项的值。


[![作为值的类别名称字段和使用 CategoryID 使 DropDownList 显示](master-detail-filtering-with-two-dropdownlists-cs/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image10.png)

**图 4**： 使 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image12.png))


现在我们有 DropDownList 控件 (`Categories`)，从记录将填充`Categories`表。 当用户选择从 DropDownList 我们要回发发生才能刷新产品 DropDownList，我们将在步骤 2 中创建新类别。 因此，应检查从启用自动回发选项`categories`DropDownList 的智能标记。


[![启用的类别 DropDownList 的 AutoPostBack](master-detail-filtering-with-two-dropdownlists-cs/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image13.png)

**图 5**： 用于启用 AutoPostBack `Categories` DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image15.png))


## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>步骤 2： 在第二个 DropDownList 中显示所选的类别产品

使用`Categories`DropDownList 完成后，我们下一步将显示属于所选类别产品的 DropDownList。 若要完成此操作，将另一个 DropDownList 添加到名为页`ProductsByCategory`。 如同`Categories`下拉列表中，创建的新 ObjectDataSource `ProductsByCategory` DropDownList 名为`ProductsByCategoryDataSource`。


[![为 ProductsByCategory DropDownList 添加新的数据源](master-detail-filtering-with-two-dropdownlists-cs/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image16.png)

**图 6**： 添加新的数据源`ProductsByCategory`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image18.png))


[![创建名为 ProductsByCategoryDataSource 新 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image19.png)

**图 7**： 创建新对象数据源命名`ProductsByCategoryDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image21.png))


由于`ProductsByCategory`DropDownList 需要显示属于所选类别的产品具有调用 ObjectDataSource`GetProductsByCategoryID(categoryID)`方法从`ProductsBLL`对象。


[![选择使用 ProductsBLL 类](master-detail-filtering-with-two-dropdownlists-cs/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image22.png)

**图 8**： 选择使用`ProductsBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image24.png))


[![配置对象数据源使用 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-two-dropdownlists-cs/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image25.png)

**图 9**： 配置为使用 ObjectDataSource`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image27.png))


我们需要在向导的最后一步中指定的值*`categoryID`* 参数。 将此参数分配到中的选定项`Categories`DropDownList。


[![从 Categories DropDownList 拉取 categoryID 参数值](master-detail-filtering-with-two-dropdownlists-cs/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image28.png)

**图 10**： 拉取*`categoryID`* 参数值来自`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image30.png))


使用 ObjectDataSource 配置，所有的就是以指定哪些数据源字段用于显示和 DropDownList 的项的值。 显示`ProductName`字段，并使用`ProductID`字段的值。


[![指定用于 DropDownList 的 Listitem 文本和值属性的数据源字段](master-detail-filtering-with-two-dropdownlists-cs/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image31.png)

**图 11**： 指定数据源字段使用 DropDownList `ListItem` s'`Text`和`Value`属性 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image33.png))


使用 ObjectDataSource 和`ProductsByCategory`DropDownList 配置我们的页面将显示两个 Dropdownlist： 第一个将所有类别列出，而第二个将列出属于所选类别的那些产品。 当用户从第一个下拉列表中选择新类别时，回发将会随之发生，并且第二个 DropDownList 将重新绑定，显示这些属于新选择的类别的产品。 图 12 和 13 显示`MasterDetailsDetails.aspx`中操作时的浏览器查看。


[![当首次访问的页面，选择饮料类别](master-detail-filtering-with-two-dropdownlists-cs/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image34.png)

**图 12**： 当首次访问的页面，选择饮料类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image36.png))


[![如果选择了不同的类别显示该新类别的产品](master-detail-filtering-with-two-dropdownlists-cs/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image37.png)

**图 13**： 选择不同的类别显示该新类别的产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image39.png))


目前`productsByCategory`下拉列表中，更改时，does*不*引起回发。 但是，我们想为在回发发生后我们将添加 DetailsView 以显示所选的产品的详细信息 (步骤 3)。 因此，选中从启用自动回发复选框`productsByCategory`DropDownList 的智能标记。


[![启用 productsByCategory DropDownList 的 AutoPostBack 功能](master-detail-filtering-with-two-dropdownlists-cs/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image40.png)

**图 14**： 启用自动回发功能以`productsByCategory`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image42.png))


## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>步骤 3： 使用 DetailsView 显示所选产品的详细信息

最后一步是在 DetailsView 中显示所选产品的详细信息。 若要实现此目的，添加到页面的 DetailsView，设置其`ID`属性设置为`ProductDetails`，并为其创建新对象数据源。 配置要从其数据提取此 ObjectDataSource`ProductsBLL`类的`GetProductByProductID(productID)`方法使用的所选的值`ProductsByCategory`的值的 DropDownList *`productID`* 参数。


[![选择使用 ProductsBLL 类](master-detail-filtering-with-two-dropdownlists-cs/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image43.png)

**图 15**： 选择使用`ProductsBLL`类 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image45.png))


[![配置对象数据源使用 GetProductByProductID(productID) 方法](master-detail-filtering-with-two-dropdownlists-cs/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image46.png)

**图 16**： 配置为使用 ObjectDataSource`GetProductByProductID(productID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image48.png))


[![从 ProductsByCategory DropDownList 拉取产品 id 参数值](master-detail-filtering-with-two-dropdownlists-cs/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image49.png)

**图 17**： 拉取*`productID`* 参数值来自`ProductsByCategory`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image51.png))


您可以选择在 DetailsView 中显示的任何可用字段。 我选择要删除`ProductID`， `SupplierID`，和`CategoryID`字段重新排序和格式设置剩余字段。 此外，我已清理 DetailsView`Height`和`Width`属性，允许 DetailsView 其数据，而不是让它大容量限制为指定的大小扩展到最佳显示效果所需的宽度。 完整的标记如下所示：


[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample1.aspx)]

请花费片刻时间来试用`MasterDetailsDetails.aspx`页在浏览器中。 乍一看上去一切根据需要，但没有一个细微的问题。 当你选择的新类别`ProductsByCategory`DropDownList 更新以包含所选的类别，这些产品，但`ProductDetails`DetailsView 继续显示以前的产品信息。 选择所选类别不同的产品时，会更新 DetailsView。 此外，如果不够全面测试，您会发现，如果你不断地选择新类别 (例如，选择从饮料`Categories`下拉列表中，然后调味品，然后糖果) 每个其他类别选择会导致`ProductDetails`DetailsView 刷新。

若要帮助具体化此问题，让我们看一下具体的示例。 当你首次访问页面时选择饮料类别和相关的产品加载中`ProductsByCategory`DropDownList。 Chai 是所选的产品，其详细信息显示在`ProductDetails`DetailsView，如图 18 中所示。


[![在 DetailsView 中显示所选产品的详细信息](master-detail-filtering-with-two-dropdownlists-cs/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image52.png)

**图 18**： 根据所选产品详细信息显示在 DetailsView ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image54.png))


如果更改类别选择从饮料为调味品，产生的回发和`ProductsByCategory`DropDownList 相应的更新，但 DetailsView 仍显示 Chai 的详细信息。


[![仍显示了以前所选产品的详细信息](master-detail-filtering-with-two-dropdownlists-cs/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image55.png)

**图 19**： 根据以前所选产品的详细信息是仍显示 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image57.png))


选择列表中的新产品刷新 DetailsView，按预期方式。 如果更改该产品后选取新的类别，DetailsView 试不会刷新。 但是，如果而不是选择一种新产品选择新类别，将刷新 DetailsView。 世界上什么呢？

问题是页面的生命周期中的计时问题。 每当请求页面时将经历多个步骤作为其呈现。 在以下步骤之一 ObjectDataSource 控制检查是否任何其`SelectParameters`值已更改。 如果这样，数据 Web 控件绑定到 ObjectDataSource 知道它需要刷新其显示。 例如，选择新类别时， `ProductsByCategoryDataSource` ObjectDataSource 检测到其参数值已更改和`ProductsByCategory`DropDownList 重新绑定本身，获取所选类别的产品。

在此情况下会出现的问题是 Objectdatasource 检查已更改的参数的页面生命周期中的点发生*之前*关联的数据 Web 控件的绑定。 因此，选择新类别时`ProductsByCategoryDataSource`ObjectDataSource 检测到更改时在其参数的值。 使用 ObjectDataSource `ProductDetails` DetailsView，但是，不会注意任何此类更改因为`ProductsByCategory`DropDownList 尚未重新绑定。 在生命周期中更高版本`ProductsByCategory`DropDownList 重新绑定到其对象数据源，获取新选定类别的产品。 虽然`ProductsByCategory`DropDownList 的值已更改， `ProductDetails` DetailsView 的 ObjectDataSource 已完成其参数值检查; 因此，DetailsView 显示其以前的结果。 这种交互如图 20 所示。


[![ProductsByCategory DropDownList 值更改后 ProductDetails DetailsView ObjectDataSource 检查更改](master-detail-filtering-with-two-dropdownlists-cs/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image58.png)

**图 20**: `ProductsByCategory` DropDownList 值更改后`ProductDetails`DetailsView 的 ObjectDataSource 检查更改 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image60.png))


若要纠正此我们需要显式重新绑定`ProductDetails`之后的 DetailsView`ProductsByCategory`已绑定 DropDownList。 我们可以完成此操作通过调用`ProductDetails`DetailsView 的`DataBind()`方法时`ProductsByCategory`DropDownList 的`DataBound`事件触发。 将以下事件处理程序代码添加到`MasterDetailsDetails.aspx`页面的代码隐藏类 (请参阅"[以编程方式设置 ObjectDataSource 的参数值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)"有关如何添加事件处理程序的讨论):


[!code-csharp[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample2.cs)]

此显式调用后`ProductDetails`DetailsView 的`DataBind()`方法已添加，本教程按预期方式工作。 图 21 突出显示此更改如何纠正我们早期的问题。


[![ProductDetails DetailsView 是显式刷新时 ProductsByCategory DropDownList 的数据绑定事件触发](master-detail-filtering-with-two-dropdownlists-cs/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image61.png)

**图 21**: `ProductDetails` DetailsView 时，可以显式刷新`ProductsByCategory`DropDownList 的`DataBound`事件将触发 ([单击以查看实际尺寸的图像](master-detail-filtering-with-two-dropdownlists-cs/_static/image63.png))


## <a name="summary"></a>总结

DropDownList 是母版/详细信息报告一个理想的用户界面元素的母版和详细信息记录之间的一对多关系。 在前面的教程中，我们已了解如何使用一个 DropDownList 来筛选显示的所选类别的产品。 在本教程中，我们替换下拉列表中，为产品的 GridView 和 DetailsView 用于显示所选产品的详细信息。 在本教程中讨论的概念可以轻松地扩展到数据模型涉及多个到多关系，如客户、 订单和订单项。 一般情况下，始终可以添加一个对多关系中的"一"实体的每个的 DropDownList。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-a-dropdownlist-cs.md)
> [下一页](master-detail-filtering-across-two-pages-cs.md)
