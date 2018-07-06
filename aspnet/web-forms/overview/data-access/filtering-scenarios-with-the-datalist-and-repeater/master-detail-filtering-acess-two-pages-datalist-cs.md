---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
title: 母版/详细信息筛选跨两个页面 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程介绍如何隔离跨两个页面的母版/详细信息报表。 在母版页我们使用 Repeater 控件来呈现的 categ 列表...
ms.author: aspnetcontent
ms.date: 10/30/2010
ms.assetid: 68b8c023-92fa-4df6-9563-1764e16e4b04
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 1dc0c074ecc8ca6128376c8cdf5548028d9779e3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830728"
---
<a name="masterdetail-filtering-across-two-pages-c"></a>母版/详细信息筛选跨两个页面 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_CS.exe)或[下载 PDF](master-detail-filtering-acess-two-pages-datalist-cs/_static/datatutorial34cs1.pdf)

> 在本教程介绍如何隔离跨两个页面的母版/详细信息报表。 在"母版页"我们使用 Repeater 控件来呈现种类列表，当单击时，会将用户转到"详细信息"页两列 DataList 其中显示属于所选类别的那些产品。


## <a name="introduction"></a>介绍

在中[前面的教程](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)我们已了解如何在单个网页上使用 Dropdownlist 以显示"主"的记录和 DataList 以显示"详细信息"。 显示母版/详细信息报表 用于母版/详细信息报表的另一种常见模式是具有一个网页上的主记录和在另一台的详细信息。 在早期[母版/详细信息筛选跨两个页面](../masterdetail/master-detail-filtering-across-two-pages-cs.md)教程中，我们探讨了使用 GridView 显示所有供应商提供的系统中此模式。 此 GridView 包含 HyperLinkField，呈现为链接到第二个页面，传递`SupplierID`在查询字符串中。 使用 GridView，第二个页以列出所选的供应商提供的那些产品。

使用 DataList 和 Repeater 控件也可以完成此类的两页母版/详细信息报表。 唯一的区别是，DataList 和 Repeater 都不提供了支持 HyperLinkField 控件。 相反，我们必须添加超链接 Web 控件或 HTML 定位点元素 (`<a>`) 在控件内`ItemTemplate`。 超链接的`NavigateUrl`属性或定位点的`href`属性可以然后使用自定义声明性或编程方法。

在本教程中我们将探讨一个示例，其中列出了使用 Repeater 控件的一页上的项目符号列表中的类别。 每个列表项将包括该类别的名称和描述，具有指向第二页链接的形式显示的类别名称。 单击此链接将 whisk 到第二页上，用户将显示 DataList 的那些产品属于所选的类别。

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>步骤 1： 在项目符号列表中显示类别

创建任何母版/详细信息报表的第一步是首先显示的"主"的记录。 因此，我们的第一个任务是在"主"页中显示的类别。 打开`CategoryListMaster.aspx`页中`DataListRepeaterFiltering`文件夹中，添加一个 Repeater 控件，，和从智能标记中，选择要添加新对象数据源。 配置新对象数据源，以便访问其数据从`CategoriesBLL`类的`GetCategories`方法 （请参阅图 1）。


[![配置对象数据源使用 CategoriesBLL 类 GetCategories 方法](master-detail-filtering-acess-two-pages-datalist-cs/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image1.png)

**图 1**： 配置为使用 ObjectDataSource`CategoriesBLL`类的`GetCategories`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image3.png))


接下来，定义 Repeater 的模板，使它作为项目符号列表中的项将显示每个类别名称和说明。 让我们尚不担心每个类别的详细信息页的链接。 下面演示的 Repeater 和 ObjectDataSource 的声明性标记：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample1.aspx)]

使用此完整的标记，花点时间查看我们通过浏览器的进度。 如图 2 所示，Repeater 将呈现为一个项目符号列表，显示每个类别的名称和说明。


[![每个类别显示为项目符号列表项](master-detail-filtering-acess-two-pages-datalist-cs/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image4.png)

**图 2**： 每个类别显示为项目符号列表项 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image6.png))


## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>步骤 2： 将类别名称转变为详细信息页的链接

若要允许的用户以显示给定类别的"详细信息"信息，我们需要添加为每个项目符号列表项，当单击时，将用户转到第二个页面的链接 (`ProductsForCategoryDetails.aspx`)。 然后，此第二个页面将显示使用 DataList 所选类别的产品。 若要确定其链接被单击的类别，我们需要向单击的类别`CategoryID`通过一些机制的第二页。 从一页的标量数据传输到另一个的最简单、 最简单方法是通过在查询字符串，它是我们将在本教程中使用的选项。 具体而言，`ProductsForCategoryDetails.aspx`页将预期所选*`categoryID`* 通过名为的查询字符串字段的值`CategoryID`。 例如，若要查看饮料类别的产品具有`CategoryID`为 1，用户需要访问`ProductsForCategoryDetails.aspx?CategoryID=1`。

在 Repeater 我们需要添加超链接 Web 控件或 HTML 定位点元素中创建每个项目符号列表项的超链接 (`<a>`) 到`ItemTemplate`。 在场景中，超链接是显示每个行相同，这两种方法就足够了。 为重复字符，我更愿意使用定位点元素。 若要使用的定位点元素，请更新到 Repeater 的 ItemTemplate:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample2.aspx)]

请注意，`CategoryID`可以直接在定位点元素中注入`href`属性; 不过，若要执行因此一定要分隔`href`属性的值与撇号 （和注意引号），因为`Eval`方法内`href`属性分隔其字符串 (`"CategoryID"`) 加上引号。 或者，可以改为使用超链接 Web 控件：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample3.aspx)]

请注意如何 URL 的静态部分 — `ProductsForCategoryDetails.aspx?CategoryID` -的结果末尾追加`Eval("CategoryID")`直接在使用字符串串联的数据绑定语法中。

使用超链接控件的一个好处是，它可以以编程方式访问从 Repeater 的`ItemDataBound`事件处理程序，如果需要。 例如，你可能想要为文本而不是与任何关联的产品类别的链接的形式显示的类别名称。 无法在以编程方式执行此类检查`ItemDataBound`事件处理程序; 对于不使用的类别关联的产品，超链接`NavigateUrl`属性可以设置为空白字符串，从而导致该特定类别名称呈现为纯文本 （而不以链接形式)。 回头[设置 DataList 和 Repeater 基于数据的格式](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md)有关详细信息 DataList 和 Repeater 的内容设置格式的教程基于通过编程逻辑`ItemDataBound`事件处理程序。

如果您按照此过程，随意在页面中使用的定位点元素或超链接控件的实现方式。 而不考虑的方法，查看通过浏览器的每个类别名称应呈现为链接到网页时`ProductsForCategoryDetails.aspx`，并传入适用`CategoryID`值 （请参见图 3）。


[![类别名称现在链接到 ProductsForCategoryDetails.aspx](master-detail-filtering-acess-two-pages-datalist-cs/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image7.png)

**图 3**: 类别名称现在链接到`ProductsForCategoryDetails.aspx`([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image9.png))


## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>步骤 3： 列出了所有属于所选类别产品

与`CategoryListMaster.aspx`页上完成，我们已准备好将实现"详细信息"页中，我们重点处理`ProductsForCategoryDetails.aspx`。 打开此页，将从工具箱拖到设计器中，拖动 DataList 并设置其`ID`属性设置为`ProductsInCategory`。 接下来，从 DataList 的智能标记选择将新对象数据源添加到页上，其命名为`ProductsInCategoryDataSource`。 将其配置，以便它将调用`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法; 将设置为 （无） INSERT、 UPDATE 和 DELETE 选项卡中列出的下拉列表。


[![配置对象数据源使用 ProductsBLL 类 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-acess-two-pages-datalist-cs/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image10.png)

**图 4**： 配置为使用 ObjectDataSource`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image12.png))


由于`GetProductsByCategoryID(categoryID)`方法接受一个输入的参数 (*`categoryID`*)，选择数据源向导为我们提供了可以指定参数的源。 设置参数源为查询字符串使用 QueryStringField `CategoryID`。


[![使用查询字符串字段 CategoryID 作为参数的源](master-detail-filtering-acess-two-pages-datalist-cs/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image13.png)

**图 5**： 使用查询字符串字段`CategoryID`作为参数的源 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image15.png))


正如我们已经完成选择数据源向导后看到在上一教程中，Visual Studio 将自动创建`ItemTemplate`的 DataList，其中列出了每个数据字段名称和值。 替换此模板，其中列出了仅对产品的名称、 供应商和价格。 此外，还要设置 DataList 的`RepeatColumns`属性设置为 2。 更改后，DataList 和 ObjectDataSource 的声明性标记应类似于下面：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample4.aspx)]

若要在操作中查看此页，从启动`CategoryListMaster.aspx`页; 接下来，单击类别项目符号列表中的链接。 执行此操作会转到`ProductsForCategoryDetails.aspx`，并传递沿`CategoryID`通过在查询字符串。 `ProductsInCategoryDataSource`中的 ObjectDataSource`ProductsForCategoryDetails.aspx`然后将获取指定类别的产品并将其显示 DataList，呈现每个行的两个产品中。 图 6 所示的屏幕截图`ProductsForCategoryDetails.aspx`查看饮料时。


[![显示饮料，每行的两个](master-detail-filtering-acess-two-pages-datalist-cs/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image16.png)

**图 6**： 显示饮料，每行的两个 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image18.png))


## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>步骤 4: ProductsForCategoryDetails.aspx 上显示类别信息

当用户单击中的类别`CategoryListMaster.aspx`，他们所转到`ProductsForCategoryDetails.aspx`并显示属于所选类别的产品。 但是，在`ProductsForCategoryDetails.aspx`有关于选择哪种类别没有视觉提示。 用户应单击饮料，但会意外地被单击的调味品，具有无法意识到他们的错误操作，一旦它们达到`ProductsForCategoryDetails.aspx`。 若要缓解这种潜在问题，我们可以显示有关所选类别的信息 — 其名称和说明，在顶部`ProductsForCategoryDetails.aspx`页。

若要实现此目的，将添加在 Repeater 控件的上方 FormView `ProductsForCategoryDetails.aspx`。 接下来，从名为的 FormView 的智能标记向页面添加新 ObjectDataSource`CategoryDataSource`并将其配置为使用`CategoriesBLL`类的`GetCategoryByCategoryID(categoryID)`方法。


[![有关通过 CategoriesBLL 类 GetCategoryByCategoryID(categoryID) 方法类别的访问信息](master-detail-filtering-acess-two-pages-datalist-cs/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image19.png)

**图 7**： 访问通过类别有关的信息`CategoriesBLL`类的`GetCategoryByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image21.png))


如同`ProductsInCategoryDataSource`添加在步骤 3 中的 ObjectDataSource`CategoryDataSource`的配置数据源向导提示我们输入的源`GetCategoryByCategoryID(categoryID)`方法的输入参数。 使用完全相同的设置与之前一样，参数源设置为查询字符串和 QueryStringField 值`CategoryID`（回头查看图 5）。

完成向导后，Visual Studio 会自动创建`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`FormView 的。 由于我们要提供只读接口，放心删除`EditItemTemplate`和`InsertItemTemplate`。 此外，随意自定义 FormView 的`ItemTemplate`。 以后删除多余的模板和自定义 ItemTemplate，FormView 和 ObjectDataSource 的声明性标记看起来应类似于下面：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample5.aspx)]

图 8 显示了屏幕快照时查看通过浏览器的此页。

> [!NOTE]
> 除了 FormView，我还添加了超链接控件上面，将引导用户返回到列表类别 FormView (`CategoryListMaster.aspx`)。 任意其他位置放置此链接或者完全忽略它。


[![类别信息是现在显示在页面的顶部](master-detail-filtering-acess-two-pages-datalist-cs/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image22.png)

**图 8**： 类别信息是现在显示在页面的顶部 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image24.png))


## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>步骤 5： 显示一条消息，如果没有产品属于所选类别

`CategoryListMaster.aspx`页列出所有类别在系统中，而不考虑是否存在相关联的产品。 如果用户单击没有关联的产品中 DataList 类别`ProductsForCategoryDetails.aspx`将不会呈现，因为其数据源没有任何项。 正如我们已经看到在过去的教程中，提供了 GridView`EmptyDataText`属性，可用于指定在其数据源中没有记录时要显示的文本消息。 遗憾的是，DataList 和 Repeater 都不具有此类的属性。

若要显示一条消息，通知用户所选类别中的没有匹配产品产品，我们需要添加一个标签控件到页`Text`属性分配要显示的事件中没有匹配产品的消息。 然后，我们需要以编程方式设置其`Visible`属性基于 DataList 是否包含任何项。

若要完成此操作，首先添加 DataList 下方的标签。 设置其`ID`属性设置为`NoProductsMessage`并将其`Text`属性设置为"没有所选的类别的产品"接下来，我们需要以编程方式设置此标签`Visible`属性基于是否任何数据被绑定到`ProductsInCategory`DataList。 必须进行此赋值后的数据已绑定到 DataList。 对于 GridView、 DetailsView 和 FormView，可以创建为控件的事件处理程序`DataBound`数据绑定完成后触发的事件。 但是，DataList 和 Repeater 都不具有`DataBound`事件可用。

对于此特定示例中我们可以将标签的分配`Visible`中的属性`Page_Load`事件处理程序，因为数据将被分配给之前页面的 DataList`Load`事件。 但是，这种方法将无法在一般情况下，按对象数据源中的数据可能会绑定到 DataList 页面的生命周期中更高版本。 例如，如果显示的数据根据另一个控件中的值，例如它是显示使用 DropDownList 以保存"主"的记录的母版/详细信息报表时，数据可能不重新绑定到之前的数据 Web 控件`PreRender`中暂存在页生命周期。

这将适用于所有情况下的一种解决方案是将分配`Visible`属性设置为`False`中 DataList `ItemDataBound` (或`ItemCreated`) 事件处理程序绑定的项类型时`Item`或`AlternatingItem`。 这种情况下我们知道，没有至少一个数据在数据源中项，并因此可以隐藏`NoProductsMessage`标签。 除了此事件处理程序中，我们还需要一个事件处理程序的 DataList`DataBinding`事件，其中我们初始化的标签`Visible`属性设置为`True`。 由于`DataBinding`事件之前激发`ItemDataBound`事件，该标签`Visible`最初将属性设置为`True`; 如果没有任何数据项，但是，它将设置为`False`。 下面的代码实现此逻辑：

[!code-csharp[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample6.cs)]

Northwind 数据库中的类别的所有对一个或多个产品相关联。 若要测试此功能，我已经手动调整 Northwind 数据库为本教程中，重新分配与生成类别相关联的所有产品 (`CategoryID` = 7) 到 Seafood 类别 (`CategoryID` = 8)。 这可以实现从服务器资源管理器通过选择新查询并使用以下`UPDATE`语句：

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample7.sql)]

相应地更新数据库之后, 返回到`CategoryListMaster.aspx`页上，单击生成链接。 由于不再有任何属于生成类别的产品，您应看到"没有所选的类别的产品"消息，如图 9 中所示。


[![如果有任何产品属于所选分类，显示一条消息](master-detail-filtering-acess-two-pages-datalist-cs/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image25.png)

**图 9**： 如果有无产品属于所选分类将显示消息 ([单击以查看实际尺寸的图像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image27.png))


## <a name="summary"></a>总结

虽然母版/详细信息报告可以在单个页面上显示母版和详细信息记录，很多网站在它们之间用在两个 web 页面。 在本教程中我们介绍了如何通过将"主"网页中使用 Repeater 的项目符号列表中列出的类别和"详细信息"页中列出的关联的产品实现此类母版/详细信息报告。 主网页中的每个列表项包含指向传递的行的详细信息页的`CategoryID`值。

在详细信息页中指定的供应商检索这些产品已通过完成`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。 *`categoryID`* 使用以声明方式指定参数值`CategoryID`参数源的查询字符串值。 我们还了解了如何使用 FormView 的详细信息页中显示类别详细信息以及如何显示一条消息，如果存在不属于所选类别的产品。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones 和 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)
> [下一页](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
