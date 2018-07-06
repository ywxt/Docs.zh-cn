---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
title: 使用 DropDownList (C#) 进行筛选母版/详细信息 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何使用 Dropdownlist 以显示用于显示 'master' 记录和 DataList 单个网页中显示母版/详细信息报表...
ms.author: aspnetcontent
ms.date: 07/18/2007
ms.assetid: 07fa47ae-e491-4a2f-b265-d342b9ddef46
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: ed2631e49786c81075099cca6941d98ba3b67e37
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818247"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a>使用 DropDownList (C#) 进行筛选母版/详细信息
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)

> 在本教程中我们将了解如何使用 Dropdownlist 以显示"主"的记录和显示的"详细信息"DataList 单个网页中显示母版/详细信息报表。


## <a name="introduction"></a>介绍

首次创建在早期版本中使用 GridView 的母版/详细信息报告[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教程中，首先会显示某些组的"主"的记录。 用户可以然后向下钻取到一个主机记录，从而查看该主记录的"详细信息。" 母版/详细信息报表是一个对多关系可视化和显示 （是有大量的列） 特别"宽型"的表中的详细的信息的理想之选。 我们已经探讨了如何实现在前面的教程中使用 GridView 和 DetailsView 控件的母版/详细信息报表。 在本教程和两个，我们将重新检查这些概念，但侧重于使用 DataList 和 Repeater 控件，而是。

在本教程中，我们将介绍使用 DropDownList 包含的"主"的记录，DataList 中显示的"详细信息"记录。

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>步骤 1： 添加母版/详细信息教程 Web 页

在开始本教程之前，我们先来看一段时间来添加的文件夹和我们需要为本教程，并使用 DataList 和 Repeater 控件的母版/详细信息报表处理两个 ASP.NET 页。 首先，创建一个新的文件夹在项目中名为`DataListRepeaterFiltering`。 接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![创建 DataListRepeaterFiltering 文件夹并添加教程 ASP.NET 页面](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image1.png)

**图 1**： 创建`DataListRepeaterFiltering`文件夹并添加教程 ASP.NET 页面


接下来，打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。 此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中，枚举站点图，并从项目符号列表中的当前部分显示这些教程。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))


为了使项目符号列表显示母版/详细信息教程，我们将创建，我们需要将它们添加到站点地图。 打开`Web.sitemap`文件，并在"显示数据使用 DataList 和 Repeater"站点映射节点标记之后添加以下标记：

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image5.png)

**图 3**： 更新包括新的 ASP.NET 页面的站点图


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>步骤 2： 在 DropDownList 中显示类别

我们的母版/详细信息报表将列出与所选的列表项的产品显示在下拉列表中，类别后面 DataList 中的页。 然后，领先于我们的第一个任务是已在 DropDownList 中显示的类别。 首先打开`FilterByDropDownList.aspx`页中`DataListRepeaterFiltering`文件夹，然后从工具箱拖动到页面的设计器将 DropDownList。 接下来，设置 DropDownList`ID`属性设置为`Categories`。 单击选择数据源链接从 DropDownList 的智能标记并创建名为新 ObjectDataSource `CategoriesDataSource`。


[![添加名为 CategoriesDataSource 新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)

**图 4**： 添加新对象数据源名为`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))


配置新对象数据源，以便它将调用`CategoriesBLL`类的`GetCategories()`方法。 配置的 ObjectDataSource 我们仍然需要指定应在 DropDownList 中显示哪些数据源字段和后一个应为每个列表项的值相关联。 具有`CategoryName`字段与显示和`CategoryID`为每个列表项的值。


[![作为值的类别名称字段和使用 CategoryID 使 DropDownList 显示](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)

**图 5**： 使 DropDownList 显示`CategoryName`字段并使用`CategoryID`作为值 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))


现在我们有从记录将填充 DropDownList 控件`Categories`表 （全部在大约六秒钟内完成）。 图 6 显示了我们到目前为止的浏览器查看时。


[![下拉列表列出了当前类别](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)

**图 6**: 下拉列表列出了当前类别 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png))


## <a name="step-2-adding-the-products-datalist"></a>步骤 2： 添加产品 DataList

我们的母版/详细信息报表的最后一步是列出与所选类别关联的产品。 若要实现此目的，向页面添加 DataList 并创建名为新 ObjectDataSource `ProductsByCategoryDataSource`。 具有`ProductsByCategoryDataSource`控件检索其数据从`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。 由于此母版/详细信息报表是只读的选择 (None) 选项中的 INSERT、 UPDATE 和 DELETE 的选项卡。


[![选择 GetProductsByCategoryID(categoryID) 方法](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)

**图 7**： 选择`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))


单击下一步后, ObjectDataSource 向导提示我们输入的值的源`GetProductsByCategoryID(categoryID)`方法的*`categoryID`* 参数。 若要使用的所选的值`categories`DropDownList 项设置参数源为控件和到 ControlID `Categories`。


[![将类别 id 参数设置为 Categories DropDownList 的值](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)

**图 8**： 设置*`categoryID`* 的值的参数`Categories`DropDownList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))


Visual Studio 将自动生成完成之后配置数据源向导，`ItemTemplate`的显示名称和值的每个数据字段的 DataList。 让我们来改进要改为使用 DataList `ItemTemplate` ，它显示只需产品的名称、 类别、 供应商，每个单元和价格和数量`SeparatorTemplate`的注入`<hr>`每个项之间的元素。 我将使用`ItemTemplate`从示例，请参见[使用 DataList 和 Repeater 控件显示数据](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md)教程中，但可随时使用查找最引人注目的任何模板标记。

进行这些更改后，你 DataList 和其 ObjectDataSource 的标记应类似于下面：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample2.aspx)]

请花费片刻时间来了解我们在浏览器中的进度。 当首次访问的页面，属于所选的类别 （饮料） 这些产品会显示 （如图 9 中所示），但更改 DropDownList 不会更新数据。 这是因为必须 DataList 更新在回发。 若要完成此我们可以设置 DropDownList`AutoPostBack`属性设置为`true`或向页面添加一个按钮 Web 控件。 对于本教程中，我选择要设置 DropDownList`AutoPostBack`属性设置为`true`。

图 9 和 10 说明了操作中的母版/详细信息报表。


[![当首次访问的页面，显示饮料产品](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)

**图 9**： 当首次访问的页面，显示饮料产品 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png))


[![选择一种新产品 （生成） 将自动导致回发，更新 DataList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)

**图 10**： 选择一种新产品 （生成） 将自动导致回发，更新 DataList ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))


## <a name="adding-a----choose-a-category----list-item"></a>添加"--选择一个类别-"列表项

首次访问时`FilterByDropDownList.aspx`页 DropDownList 的第一个列表项 （饮料） 选择默认情况下，显示 DataList 中的饮料产品的类别。 在中*母版/详细信息筛选与 DropDownList*教程中我们向 DropDownList，已选择默认情况下，选中后，显示添加"--选择一个类别-"选项*所有*的在数据库中的产品。 这种方法是可管理时列出的产品在 GridView 中后，因为每个产品行占据了少量的屏幕空间。 使用 DataList，但是，每个产品的信息使用较大块的屏幕。 我们仍将添加"--选择一个类别-"选项和让它默认情况下，选择但而不是让它显示的所有产品时选择，让我们将其配置，使之显示任何产品。

若要向 DropDownList 添加新列表项，请转到属性窗口，然后单击中的椭圆`Items`属性。 添加的新列表项`Text`"--选择一个类别-"和`Value` `0`。


![添加](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image27.png)

**图 11**： 添加"--选择一个类别-"列表项


或者，可以通过将以下标记添加到下拉列表添加列表项：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample3.aspx)]

此外，我们需要设置 DropDownList 控件`AppendDataBoundItems`到`true`由于如果设置为`false`（默认值），将类别从 ObjectDataSource 绑定到 DropDownList 时这些更改会覆盖任何手动添加列表项。


![AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image28.png)

**图 12**： 设置`AppendDataBoundItems`属性设为 True


因此我们选择了值`0`对于"--选择一个类别-"列表项都是因为值为系统中不有任何类别`0`，因此任何产品记录时，将返回选定了"--选择一个类别-"的列表项。 若要确认这一点，请花费片刻时间访问通过浏览器页面。 如图 13 所示，当最初查看页上选定了"--选择一个类别-"的列表项并不显示任何产品。


[![时](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)

**图 13**： 否产品时选择"--选择一个类别-"列表项时，会显示 ([单击以查看实际尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png))


如果您而是会显示*所有*的产品时选择"--选择一个类别-"选项，则使用值为`-1`相反。 敏锐的读者都记得中的该重新*母版/详细信息筛选与 DropDownList*教程中，我们更新`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法，以便如果*`categoryID`* 值`-1`返回记录的所有产品中传递。

## <a name="summary"></a>总结

显示按层次结构相关数据时，它通常用于呈现使用主/详细信息报表，用户可以从中启动仔细阅读的层次结构顶部的数据和向下钻取到详细信息数据。 在本教程中，我们探讨构建一个简单的母版/详细信息报告，显示所选的类别的产品。 这被通过使用 DropDownList 的类别和 DataList 属于所选类别的产品列表。

在下一教程中我们将介绍分隔跨两个页面的母版和详细信息记录。 在第一页中，"主"记录的列表将显示，包含用于查看详细信息的链接。 单击链接将 whisk 到第二页上，将显示为所选的主记录的详细信息的用户。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Randy Schmidt。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一篇](master-detail-filtering-acess-two-pages-datalist-cs.md)
