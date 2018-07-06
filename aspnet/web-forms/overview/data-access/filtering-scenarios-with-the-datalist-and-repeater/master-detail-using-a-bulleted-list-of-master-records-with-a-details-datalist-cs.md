---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
title: 母版/详细信息的母版记录项目符号列表通过 DataList 使用母详细信息 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将压缩上一教程两页母版/详细信息的报告到单个页面，t 上显示类别名称的项目符号列表...
ms.author: aspnetcontent
ms.date: 10/17/2006
ms.assetid: c727bb73-7b59-41a1-8dc3-623c6d69e7c2
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 0be6a03b2fbbf71a1f1d1e13bd4b9118981d0715
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841058"
---
<a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-c"></a>母版/详细信息的母版记录项目符号列表通过 DataList 使用母详细信息 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_CS.exe)或[下载 PDF](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/datatutorial35cs1.pdf)

> 在本教程中我们将压缩上一教程两页母版/详细信息的报告到单个页面，显示在左侧和右侧的屏幕，并在屏幕右侧的所选的类别的产品类别名称的项目符号列表。


## <a name="introduction"></a>介绍

在中[前面的教程](master-detail-filtering-acess-two-pages-datalist-cs.md)我们介绍了如何单独跨两个页面的母版/详细信息报表。 主页面中我们使用 Repeater 控件来呈现项目符号列表的类别。 每个类别名称为超链接，单击时，将采用指向详细信息页，其中两列 DataList 介绍了这些产品的用户属于所选的类别。

在本教程中我们将压缩两页教程到单个页面，每个类别名称作为 LinkButton 呈现在屏幕的左侧显示类别名称的项目符号列表。 单击其中一个类别名称 Linkbutton 引发回发，并将所选的类别的产品绑定到屏幕的右侧两列 DataList。 除了显示每个类别的名称，在左侧 Repeater 显示有多少总产品是给定的类别 （请参阅图 1）。


[![在左侧显示的类别名称和产品的总计数](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image1.png)

**图 1**： 在左侧显示类别的名称和产品总计数 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image3.png))


## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>步骤 1： 在屏幕的左侧部分中显示 Repeater

本教程中，我们需要能够显示所选的类别产品的左侧的类别项目符号列表。 可使用标准 HTML 元素段落标记，非换行空格，定位到 web 页中的内容`<table>`s，依次类推或通过级联样式表 (CSS) 技术。 我们的教程到目前为止已使用所有 CSS 技术用于定位。 当我们构建我们在母版页中的导航用户界面[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中我们使用了*绝对定位*，指示精确像素偏移量的导航列表和主要内容。 或者，使用 CSS 来定位一个元素到另一个通过左或向右*浮动*。 我们可以通过浮点左侧的 DataList Repeater 显示所选的类别产品的左侧的类别项目符号列表

打开`CategoriesAndProducts.aspx`页上从`DataListRepeaterFiltering`文件夹并添加到页面 Repeater 和 DataList。 设置 Repeater s`ID`到`Categories`和到 DataList 的`CategoryProducts`。 转到源视图，并将其自身的 Repeater 和 DataList 控件放`<div>`元素。 也就是说，将括在 Repeater`<div>`元素第一个，然后在自己 DataList `<div>` Repeater 之后紧邻的元素。 您的标记现在应类似于下面：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample1.aspx)]

若要 float 左侧的 DataList Repeater，我们需要使用`float`CSS 样式属性，如下所示：


[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample2.html)]

`float: left;`浮动第一个`<div>`左侧的第二个元素。 `width`并`padding-right`设置指示第一个`<div>`s`width`之间添加填充量和`<div>`元素的内容和其右边距。 有关浮点 CSS 中的元素的详细信息，请查看[Floatutorial](http://css.maxdesign.com.au/floatutorial/)。

而不是指定的样式设置直接通过第一个`<p>`元素 s`style`属性，请让改为创建一个新的 CSS 类中的 s`Styles.css`名为`FloatLeft`:


[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample3.css)]

然后我们可以替换`<div>`与`<div class="FloatLeft">`。

添加 CSS 类和配置中的标记后`CategoriesAndProducts.aspx`页上，转到设计器。 应会看到 Repeater 浮点到左侧的 DataList （尽管右现在这两项只是出现如以来我们 ve 尚未若要配置其数据源或模板灰色框）。


[![向 DataList 左浮动 Repeater](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image4.png)

**图 2**： 向 DataList 左浮动 Repeater ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image6.png))


## <a name="step-2-determining-the-number-of-products-for-each-category"></a>步骤 2： 确定每个类别的产品数量

Repeater 和 DataList s 周围标记完成，我们准备就绪后，若要将类别数据绑定到 Repeater 控件。 但是，如图 1 中的类别的项目符号列表所示，除了每个类别的名我们还需要显示与类别关联的产品数量。 若要访问此信息，我们可以：

- **确定此信息从 ASP.NET page s 代码隐藏类。** 给定的特定*`categoryID`* 我们可以通过调用确定关联的产品数量`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。 此方法返回`ProductsDataTable`对象，其`Count`属性指示多少`ProductsRow`s 存在，这是个指定的产品数量*`categoryID`*。 我们可以创建`ItemDataBound`Repeater，对于绑定到 Repeater，每个类别的调用的事件处理程序`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法并在输出中包含其计数。
- **更新`CategoriesDataTable`中要包括的类型化数据集`NumberOfProducts`列。** 然后，我们可以更新`GetCategories()`中的方法`CategoriesDataTable`若要包括此信息或，或者，将保留`GetCategories()`作为-并且创建一个新`CategoriesDataTable`调用方法`GetCategoriesAndNumberOfProducts()`。

让我们来了解这两种方法。 第一种方法更容易实现的因为我们不需要更新数据访问层;但是，它需要多个与数据库通信。 在调用`ProductsBLL`类 s`GetProductsByCategoryID(categoryID)`中的方法`ItemDataBound`事件处理程序会添加用于显示中继器中每个类别的额外数据库调用。 使用此技术有*N* + 1 个数据库调用，其中*N*是显示中继器中的类别数。 第二种方法，产品计数会返回有关从每个类别的信息`CategoriesBLL`类 s `GetCategories()` (或`GetCategoriesAndNumberOfProducts()`) 方法，因而只需一次访问数据库。

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>确定 ItemDataBound 事件处理程序中的产品数量

确定对于 Repeater s 中的每个类别的产品数量`ItemDataBound`事件处理程序不需要对现有数据访问层进行任何修改。 可以直接在进行所有修改`CategoriesAndProducts.aspx`页。 首先，通过添加名为新 ObjectDataSource`CategoriesDataSource`通过 Repeater s 智能标记。 接下来，配置`CategoriesDataSource`以便其检索从其数据的 ObjectDataSource`CategoriesBLL`类的`GetCategories()`方法。


[![配置对象数据源以使用 CategoriesBLL 类的 GetCategories() 方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image7.png)

**图 3**： 配置为使用 ObjectDataSource`CategoriesBLL`类 s`GetCategories()`方法 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image9.png))


中的每项`Categories`Repeater 需要是可单击，并单击时，会导致`CategoryProducts`DataList 以显示所选类别产品。 这可以通过发出一个超链接，链接回此同一页面的每个类别 (`CategoriesAndProducts.aspx`)，但传递`CategoryID`通过查询字符串，就像我们在上一教程中看到。 此方法的优点是可以添加书签和搜索引擎编制索引显示特定类别的产品页面。

或者，我们可以使每个类别 LinkButton，这是我们将在本教程使用的方法。 LinkButton 呈现为超链接在 s 用户浏览器中，但单击时，引发一个回发;在回发时，DataList 的 ObjectDataSource 需要刷新以显示属于所选类别的那些产品。 对于本教程，使用超链接更有意义比使用 LinkButton;但是，可能有其他场景中，使用 LinkButton 是更为有利。 尽管超链接方法是适用于此示例中，使改为尝试使用 LinkButton 的 s。 我们将看到，使用 LinkButton 引入了一些挑战，否则不会出现与超链接。 因此，在本教程中使用 LinkButton 将突出显示这些挑战并帮助我们可能想要使用 LinkButton 而不是一个超链接的情况下提供解决方案。

> [!NOTE]
> 建议重复本教程中使用超链接控件或`<a>`而非 LinkButton 的元素。


以下标记显示了 Repeater 和 ObjectDataSource 的声明性语法。 请注意 Repeater 的模板呈现 LinkButton 作为每个项的项目符号列表：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample4.aspx)]

> [!NOTE]
> 对于本教程 Repeater 必须具有启用了其视图状态 (请注意省略`EnableViewState="False"`Repeater s 声明性语法中)。 在步骤 3 中我们将创建一个事件处理程序为 Repeater s`ItemCommand`事件在其中我们将更新 DataList 的 ObjectDataSource 的`SelectParameters`集合。 Repeater 的`ItemCommand`，但是，如果禁用视图状态赢得 t 激发。 请参阅[ASP.NET 问题的问题贴](http://scottonwriting.net/sowblog/posts/1263.aspx)并[其解决方案](http://scottonwriting.net/sowBlog/posts/1268.aspx)的原因的详细信息必须为 Repeater s 启用视图状态`ItemCommand`激发的事件。


使用 LinkButton`ID`属性值为`ViewCategory`不具有其`Text`属性集。 如果我们只需有想要显示的类别名称，我们将具有设置的 Text 属性以声明方式，通过数据绑定语法如下所示：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample5.aspx)]

但是，我们想要显示这两个类别的名称*和*属于该类别的产品数量。 可以检索此信息从 Repeater s`ItemDataBound`事件处理程序，方法调用`ProductBLL`类 s`GetCategoriesByProductID(categoryID)`方法，并确定在生成返回多少条记录`ProductsDataTable`，如以下代码说明：


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample6.cs)]

首先，确保我们重新使用数据项 (一个其`ItemType`是`Item`或`AlternatingItem`)，然后引用`CategoriesRow`只绑定到当前实例`RepeaterItem`。 接下来，我们通过创建的实例来确定此类别的产品数量`ProductsBLL`类，调用其`GetCategoriesByProductID(categoryID)`方法，并确定使用返回的记录数`Count`属性。 最后， `ViewCategory` LinkButton 的 ItemTemplate 中是引用并将其`Text`属性设置为*CategoryName* (*NumberOfProductsInCategory*)，其中*NumberOfProductsInCategory*格式化为带小数位数为零的数字。

> [!NOTE]
> 或者，可以添加我们*格式设置函数*到 ASP.NET 页面 + s 代码隐藏类接受类别 s`CategoryName`并`CategoryID`值，并返回`CategoryName`加上的数字产品类别中的 (由调用`GetCategoriesByProductID(categoryID)`方法)。 此类格式设置函数的结果无法以声明方式分配给 Text 属性替换为要使用的 LinkButton s`ItemDataBound`事件处理程序。 请参阅[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)或[设置 DataList 和 Repeater 基于数据的格式](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md)教程有关使用格式设置函数的详细信息。


添加后此事件处理程序，请花费片刻时间来测试通过浏览器页面。 请注意如何在项目符号列表中，显示类别的名称和与类别关联的产品数列出每个类别 （请参阅图 4）。


[![显示每个类别名称和数量的产品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image10.png)

**图 4**： 显示每个类别名称和数量的产品 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image12.png))


## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>正在更新`CategoriesDataTable`和`CategoriesTableAdapter`中要包含的每个类别的产品数量

而不是确定的每个类别的产品数 s 绑定到 Repeater 中，我们可以简化此过程通过调整`CategoriesDataTable`和`CategoriesTableAdapter`中数据访问层为本机包含此信息。 若要实现此目的，我们必须添加到一个新列`CategoriesDataTable`来保存关联的产品数量。 若要将新列添加到数据表中，打开类型化数据集 (`App_Code\DAL\Northwind.xsd`)，右键单击 DataTable，若要修改，然后选择添加 / 列。 添加到一个新列`CategoriesDataTable`（请参见图 5）。


[![将新列添加到 CategoriesDataSource](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image13.png)

**图 5**： 添加到一个新列`CategoriesDataSource`([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image15.png))


这将添加一个名为的新列`Column1`，你可以通过只需键入其他名称。 为此新列重命名`NumberOfProducts`。 接下来，我们需要配置此列的属性。 单击新列，并转到属性窗口。 更改列 s`DataType`属性从`System.String`到`System.Int32`并设置`ReadOnly`属性设置为`True`，如图 6 中所示。


![设置数据类型和新的列的 ReadOnly 属性](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image16.png)

**图 6**： 设置`DataType`和`ReadOnly`新列的属性


虽然`CategoriesDataTable`现在具有`NumberOfProducts`列中，未设置任何相应的 TableAdapter 的查询它的值。 我们可以更新`GetCategories()`方法以返回此信息，如果我们希望此类信息返回每次检索类别信息。 如果，但是，我们只需获取中极少数情况下 （例如，对于本教程，只需），类别相关联的产品数，则我们可以保留`GetCategories()`作为-并且创建一个返回此信息的新方法。 允许 s 使用此后一种方法，创建一个名为的新方法`GetCategoriesAndNumberOfProducts()`。

若要添加此新`GetCategoriesAndNumberOfProducts()`方法中，右键单击`CategoriesTableAdapter`，然后选择新查询。 此时将显示最多 TableAdapter 查询配置向导中，哪些我们已在前面的教程中多次使用。 此方法，该值指示该查询使用返回的行的临时 SQL 语句启动向导。


[![创建使用的临时 SQL 语句的方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image17.png)

**图 7**： 创建方法使用一个临时 SQL 语句 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image19.png))


[![SQL 语句返回的行](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image20.png)

**图 8**: SQL 语句返回行 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image22.png))


下一步的向导屏幕提示我们要使用的查询。 若要返回每个类别 s `CategoryID`， `CategoryName`，并`Description`字段，以及数量的类别，与关联的产品使用以下`SELECT`语句：


[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample7.sql)]


[![指定要使用的查询](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image23.png)

**图 9**： 指定使用的查询 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image25.png))


请注意，用于计算与类别关联的产品数量的子查询的别名为`NumberOfProducts`。 此命名的匹配项会使关联此子查询返回的值`CategoriesDataTable`s`NumberOfProducts`列。

输入此查询后, 的最后一步是选择新的方法的名称。 使用`FillWithNumberOfProducts`和`GetCategoriesAndNumberOfProducts`填充 DataTable 并返回数据表模式，分别。


[![新的 TableAdapter 的方法 FillWithNumberOfProducts 名称和 GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image26.png)

**图 10**： 命名新的 TableAdapter s 方法`FillWithNumberOfProducts`并`GetCategoriesAndNumberOfProducts`([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image28.png))


此时数据访问层已扩展为包含的每个类别的产品数目。 由于我们所有的表示层将路由到单独的业务逻辑层通过 DAL 的所有调用，因此我们需要添加相应`GetCategoriesAndNumberOfProducts`方法`CategoriesBLL`类：


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample8.cs)]

DAL 和 BLL 完成后，我们重新准备要绑定到此数据`Categories`Repeater 中的`CategoriesAndProducts.aspx`！ 如果你已创建 ObjectDataSource 用于确定从 Repeater 中的产品数量`ItemDataBound`事件处理程序部分中，删除此对象数据源，并删除 Repeater 的`DataSourceID`属性设置; 还无线免缠绕Repeater s`ItemDataBound`通过删除事件处理程序中的事件`Handles Categories.OnItemDataBound`ASP.NET 代码隐藏类中的语法。

返回在其原始状态 Repeater，添加名为新 ObjectDataSource`CategoriesDataSource`通过 Repeater s 智能标记。 配置要使用 ObjectDataSource`CategoriesBLL`类，而不是让它使用，但`GetCategories()`方法中，具有其使用`GetCategoriesAndNumberOfProducts()`改为 （请参阅图 11）。


[![配置对象数据源使用 GetCategoriesAndNumberOfProducts 方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image29.png)

**图 11**： 配置为使用 ObjectDataSource`GetCategoriesAndNumberOfProducts`方法 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image31.png))


接下来，更新`ItemTemplate`，以便 LinkButton s`Text`属性以声明方式分配使用数据绑定语法，并且同时包含`CategoryName`和`NumberOfProducts`数据字段。 中继器的完整声明性标记和`CategoriesDataSource`ObjectDataSource 按照：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample9.aspx)]

通过更新 DAL 包含呈现的输出`NumberOfProducts`列是使用相同`ItemDataBound`事件处理程序方法 (回头查看图 4，请参阅屏幕截图： 显示的类别名称和产品数量中继器)。

## <a name="step-3-displaying-the-selected-category-s-products"></a>步骤 3： 显示所选的类别的产品

现在我们有`Categories`Repeater 中每个类别中显示的类别以及数量的产品列表。 中继器的每个类别，单击时，会导致将回发时，在该点我们使用 LinkButton 需要显示在所选类别产品`CategoryProducts`DataList。

我们面临的难题之一是如何通过 DataList 显示只是这些所选类别的产品。 在中[母版/详细信息的详细信息说明如何通过使用可选择的母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)可以选择的教程，我们已了解如何生成 GridView 中的行、 与所选行 s 的详细信息显示在同一页面上 DetailsView。 GridView 的 ObjectDataSource 返回有关使用的所有产品的信息`ProductsBLL`s`GetProducts()`方法，同时 DetailsView s 对象数据源中检索有关所选的产品使用信息`GetProductsByProductID(productID)`方法。 *`productID`* 通过将它与 GridView s 的值相关联以声明方式提供参数值`SelectedValue`属性。 遗憾的是，Repeater 没有`SelectedValue`属性并不能用作参数源。

> [!NOTE]
> 这是显示在 Repeater 中使用 LinkButton 时这些挑战之一。 我们使用超链接以传入`CategoryID`通过在查询字符串相反，我们可以使用该查询字符串字段作为源参数 s 值。


之前我们担心缺乏`SelectedValue`Repeater 的属性，让我们来首先将 DataList 绑定到对象数据源并指定其`ItemTemplate`。

通过 DataList s 智能标记，选择要添加名为新 ObjectDataSource`CategoryProductsDataSource`并将其配置为使用`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。 在本教程中 DataList 提供了一个只读的接口，因为随意设置下拉列表中插入、 更新、 以及删除选项卡添加到 （无）。


[![配置对象数据源使用 ProductsBLL 类的 GetProductsByCategoryID(categoryID) 方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image32.png)

**图 12**： 配置为使用 ObjectDataSource`ProductsBLL`类 s`GetProductsByCategoryID(categoryID)`方法 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image34.png))


由于`GetProductsByCategoryID(categoryID)`方法需要一个输入的参数 (*`categoryID`*)，配置数据源向导可用于指定参数的源。 必须已在 GridView 或 DataList 中列出的类别，d 我们设置参数源下拉列表控件和到 ControlID`ID`的数据 Web 控件。 但是，由于 Repeater 缺少`SelectedValue`不能用作参数源属性。 如果选中，您会发现 ControlID 下拉列表仅包含一个控件`ID``CategoryProducts`，则`ID`的 DataList。

现在，为无设置参数源下拉列表。 我们将得到以编程方式指定此参数值时中继器中单击 LinkButton 的类别。


[![执行不指定参数的 categoryID 参数源](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image35.png)

**图 13**： 未指定的参数源*`categoryID`* 参数 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image37.png))


完成配置数据源向导后，Visual Studio 会自动生成 DataList 的`ItemTemplate`。 替换此默认值`ItemTemplate`模板与我们在前面的教程中使用; 此外，还要设置 DataList 的`RepeatColumns`属性设置为 2。 进行这些更改后你 DataList 和其关联的 ObjectDataSource 的声明性标记应如下所示：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample10.aspx)]

目前， `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 永远不会设置参数，以便查看网页时不显示任何产品。 我们需要做是有基于上设置此参数值`CategoryID`中继器中的被单击类别。 这就引入了两个质询： 首先，如何我们确定当中继器 s 中 LinkButton`ItemTemplate`已被单击; 和第二个，我们如何才能确定`CategoryID`其 LinkButton 被单击的相应类别的？

如按钮和 ImageButton 控件 LinkButton 已`Click`事件和一个[`Command`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)。 `Click`事件被设计为只需注意到已单击 LinkButton。 有时，但是，除了注意已单击 LinkButton 我们还需要将一些额外信息传递给事件处理程序。 如果出现这种情况，LinkButton s [ `CommandName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx)并[ `CommandArgument` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx)可以分配此额外信息的属性。 然后，当单击 LinkButton，其`Command`触发事件 (而不是其`Click`事件) 和事件处理程序传递的值`CommandName`和`CommandArgument`属性。

时`Command`中继器 Repeater s 中的模板内从引发事件[`ItemCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx)触发，并传递`CommandName`和`CommandArgument`单击 LinkButton 的值 (或按钮或ImageButton)。 因此，若要确定已单击 LinkButton 中继器中的类别时，我们需要执行以下操作：

1. 设置`CommandName`属性中 Repeater 的 LinkButton`ItemTemplate`为某个值 (我已使用 ListProducts)。 此值设置`CommandName`值，LinkButton 的`Command`单击 LinkButton 时激发的事件。
2. 设置 LinkButton s`CommandArgument`属性的值的当前项的`CategoryID`。
3. 为 Repeater s 创建事件处理程序`ItemCommand`事件。 在事件处理程序中，集中`CategoryProductsDataSource`ObjectDataSource s`CategoryID`参数的值的传入的`CommandArgument`。

以下`ItemTemplate`标记类别 Repeater 实现步骤 1 和 2。 请注意如何`CommandArgument`值分配数据项的`CategoryID`使用数据绑定语法：


[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample11.aspx)]

每当创建`ItemCommand`事件处理程序是比较明智的做法始终首先检查传入`CommandName`值，因为*任何*`Command`引发事件*任何*按钮、 LinkButton，或ImageButton Repeater 中的将导致`ItemCommand`激发的事件。 尽管我们当前仅有一个此类 LinkButton 现在，将来我们 （或我们的团队的其他开发人员） 可能会附加按钮 Web 将控件添加到 Repeater，单击时，将引发相同`ItemCommand`事件处理程序。 因此，它最好始终确保选中 s`CommandName`属性，如果它都匹配到预期的值，即可继续进行编程逻辑。

之后，确保传入的`CommandName`值等于 ListProducts，事件处理程序然后将分配`CategoryProductsDataSource`ObjectDataSource s`CategoryID`参数的值的传入的`CommandArgument`。 这种修改为 ObjectDataSource 的`SelectParameters`会自动导致 DataList 重新本身绑定到数据源，显示新选择的类别的产品。


[!code-csharp[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/samples/sample12.cs)]

使用这些新功能，在本教程中已完成 ！ 请花费片刻时间进行测试的浏览器中。 图 14 显示了在屏幕首次访问页面时。 由于类别具有尚未被选中，将不显示任何产品。 单击一个类别，如生成，显示这些产品的产品类别中的两个列视图 （请参阅图 15）。


[![无产品的显示时第一个访问的页面](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image38.png)

**图 14**： 否产品的显示时第一个访问的页面 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image40.png))


[![单击生成类别列表右侧的匹配产品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image41.png)

**图 15**： 单击生成类别列出右侧的匹配产品 ([单击以查看实际尺寸的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs/_static/image43.png))


## <a name="summary"></a>总结

正如我们看到在本教程并前一次，母版/详细信息报告可以分散到两个页面，或上一个合并。 在单页上显示母版/详细信息报表，但是，引入了一些挑战如何最到母版布局和页面上的详细信息记录。 在中*母版/详细信息的详细信息说明如何通过使用可选择的母版 GridView*我们上方的主记录的详细信息记录; 在本教程中我们使用 CSS 技术具有的主记录浮点型教程左侧的详细信息。

以及显示母版/详细信息报表，我们还必须有机会了解如何检索如何执行服务器端逻辑时，LinkButton （或按钮或 ImageButton） 单击内与以及每个类别相关联的产品数量Repeater。

本教程中完成我们的母版/详细信息报表使用 DataList 和 Repeater 的检查。 我们接下来的教程将说明如何添加编辑和删除 DataList 控件的功能。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [Floatutorial](http://css.maxdesign.com.au/floatutorial/)浮点 CSS 元素使用 CSS 的教程
- [CSS 定位](http://www.brainjar.com/css/positioning/)定位的元素使用 CSS 的详细信息
- [对进行布局出内容与 HTML](http://www.w3schools.com/html/html_layout.asp)使用`<table>`s 和用于定位其他 HTML 元素

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-acess-two-pages-datalist-cs.md)
> [下一页](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
