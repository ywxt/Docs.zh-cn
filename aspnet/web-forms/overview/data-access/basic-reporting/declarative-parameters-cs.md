---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
title: 声明性参数 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将演示了如何将参数设置为硬编码值用于选择要显示的 DetailsView 控件中的数据。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 603c9bd3-b895-4ec6-853b-0c81ff36d580
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c2798ed1ac768a5103bbdc50db73ba6c3eed07f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365365"
---
<a name="declarative-parameters-c"></a>声明性参数 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_5_CS.exe)或[下载 PDF](declarative-parameters-cs/_static/datatutorial05cs1.pdf)

> 在本教程中我们将演示了如何将参数设置为硬编码值用于选择要显示的 DetailsView 控件中的数据。


## <a name="introduction"></a>介绍

在中[最后一个教程](displaying-data-with-the-objectdatasource-cs.md)我们在使用绑定到调用的 ObjectDataSource 控件的 GridView、 DetailsView 和 FormView 控件显示数据`GetProducts()`方法从`ProductsBLL`类。 `GetProducts()`方法返回填充的 Northwind 数据库中记录所有的强类型化 DataTable`Products`表。 `ProductsBLL`类包含用于返回只需子集的产品的其他方法`GetProductByProductID(productID)`， `GetProductsByCategoryID(categoryID)`，和`GetProductsBySupplierID(supplierID)`。 这三种方法需要输入的参数，该值指示如何筛选返回的产品信息。

调用方法的预期的输入的参数，但为了实现这一点我们必须指定这些参数的值来自何处，可以使用对象数据源。 参数值可以是硬编码，也可以来自各种动态源，包括： 查询字符串值，会话变量上页上，或其他人的 Web 控件的属性值。

对于本教程首先阐释如何使用一个参数设置为硬编码值。 具体而言，我们将介绍添加到显示有关特定产品，即 Chef 秋葵汤，它具有的信息的页面的 DetailsView`ProductID`为 5。 接下来，我们将了解如何设置基于 Web 控件的参数值。 具体而言，我们将使用一个文本框，用户可在一个国家/地区，此后它们可以单击按钮以查看驻留在该国家/地区的供应商提供的列表中键入。

## <a name="using-a-hard-coded-parameter-value"></a>使用硬编码参数值

第一个示例中，首先，通过添加到的 DetailsView 控件`DeclarativeParams.aspx`页中`BasicReporting`文件夹。 从 DetailsView 的智能标记上，选择&lt;新数据源&gt;从下拉列表，然后选择要添加对象数据源。


[![将对象数据源添加到页面](declarative-parameters-cs/_static/image2.png)](declarative-parameters-cs/_static/image1.png)

**图 1**： 将对象数据源添加到页 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image3.png))


这将自动启动 ObjectDataSource 控件选择数据源向导。 选择`ProductsBLL`向导的第一个屏幕中的类。


[![选择 ProductsBLL 类](declarative-parameters-cs/_static/image5.png)](declarative-parameters-cs/_static/image4.png)

**图 2**： 选择`ProductsBLL`类 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image6.png))


由于我们想要显示有关特定产品的信息，因此我们想要使用`GetProductByProductID(productID)`方法。


[![选择 GetProductByProductID(productID) 方法](declarative-parameters-cs/_static/image8.png)](declarative-parameters-cs/_static/image7.png)

**图 3**： 选择`GetProductByProductID(productID)`方法 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image9.png))


由于我们选择的方法包括参数，没有一个向导，其中我们需要定义要用于参数的值的多个屏幕。 在左侧的列表显示所有所选方法的参数。 有关`GetProductByProductID(productID)`只有一个`productID`。 在右侧，我们可以指定所选的参数的值。 参数源下拉列表枚举为参数值的各种可能来源。 由于我们想要指定硬编码值为 5`productID`参数保留为无参数源和默认值文本框中输入 5。


[![Hard-Coded 参数值的 5 将用于产品 id 参数](declarative-parameters-cs/_static/image11.png)](declarative-parameters-cs/_static/image10.png)

**图 4**: A Hard-Coded 参数值的 5 将用于`productID`参数 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image12.png))


完成配置数据源向导后，ObjectDataSource 控件声明性标记包含`Parameter`中的对象`SelectParameters`集合中定义的方法所需的输入参数的每个`SelectMethod`属性。 由于我们在此示例中使用的方法应只的单个输入的参数， `parameterID`，这里只有一个条目。 `SelectParameters`集合可以包含任何类都派生自`Parameter`类中`System.Web.UI.WebControls`命名空间。 硬编码参数值基`Parameter`类，但源选项的其他参数派生`Parameter`类; 您也可以创建你自己[自定义参数类型](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)，如果需要。

[!code-aspx[Main](declarative-parameters-cs/samples/sample1.aspx)]

> [!NOTE]
> 如果您要按照你自己的计算机上声明性标记你此时看到可能包括值`InsertMethod`， `UpdateMethod`，并`DeleteMethod`属性，以及`DeleteParameters`。 ObjectDataSource 的选择数据源向导自动指定的方法从`ProductBLL`要用于插入、 更新和删除，因此除非你显式清除了这些情况，则它们将包含在上面的标记。


Web 控件的数据时访问此页，将调用 ObjectDataSource`Select`方法，将调用`ProductsBLL`类的`GetProductByProductID(productID)`方法使用硬编码值为 5`productID`输入的参数。 该方法将返回一个强类型`ProductDataTable`对象，其中包含一个行，以了解 Chef 秋葵汤 (与产品`ProductID`5)。


[![显示信息有关 Chef 秋葵汤](declarative-parameters-cs/_static/image14.png)](declarative-parameters-cs/_static/image13.png)

**图 5**： 显示信息有关 Chef 秋葵汤 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image15.png))


## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>将参数值设置为 Web 控件的属性值

ObjectDataSource 的参数值也可以设置基于页上的 Web 控件的值。 若要说明这一点，让我们具有一个 GridView，列出所有用户指定的国家/地区中的供应商。 若要完成本教程通过将文本框添加到用户可以在其中输入国家/地区名称页。 设置此文本框控件`ID`属性设置为`CountryName`。 此外添加一个按钮 Web 控件。


[![将文本框添加到具有 ID 国家/地区名称的页面](declarative-parameters-cs/_static/image17.png)](declarative-parameters-cs/_static/image16.png)

**图 6**： 将 TextBox 添加到包含的页`ID` `CountryName` ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image18.png))


接下来，添加一个 GridView，页上，并从智能标记中，选择添加新对象数据源。 由于我们想要显示供应商信息选择`SuppliersBLL`从向导的第一个屏幕的类。 从第二个屏幕上，选择`GetSuppliersByCountry(country)`方法。


[![选择 GetSuppliersByCountry(country) 方法](declarative-parameters-cs/_static/image20.png)](declarative-parameters-cs/_static/image19.png)

**图 7**： 选择`GetSuppliersByCountry(country)`方法 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image21.png))


由于`GetSuppliersByCountry(country)`方法具有一个输入的参数，该向导再一次包括选择参数值的最后一个屏幕。 这一次，设置参数源为控件。 这将填充 ControlID 下拉列表的页面; 上的控件名称选择`CountryName`从列表中的控件。 首次访问页面时`CountryName`文本框将为空白，因此不返回任何结果并不显示任何内容。 如果你想要显示一些结果，默认情况下，请相应地设置默认值文本框中。


[![将参数值设置为国家/地区名称控件值](declarative-parameters-cs/_static/image23.png)](declarative-parameters-cs/_static/image22.png)

**图 8**： 将参数值设置为`CountryName`控制值 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image24.png))


ObjectDataSource 的声明性标记稍有不同我们第一个示例中，使用[ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx)而不是标准`Parameter`对象。 一个`ControlParameter`具有其他属性来指定`ID`的 Web 控件和要使用的参数的属性值 (`PropertyName`)。 配置数据源向导很智能，可以确定，文本框中，我们可能想要使用`Text`参数值的属性。 如果你想要使用不同的属性值从 Web 控件的但是，可以更改`PropertyName`值此处或通过单击向导中的"显示高级属性"链接。

[!code-aspx[Main](declarative-parameters-cs/samples/sample2.aspx)]

第一次访问页面时`CountryName`文本框为空。 ObjectDataSource `Select` GridView 中，但值仍调用方法`null`传递到`GetSuppliersByCountry(country)`方法。 将转换 TableAdapter`null`到数据库`NULL`值 (`DBNull.Value`)，但使用的查询`GetSuppliersByCountry(country)`方法这样编写的它不会返回任何值时`NULL`为指定值`@CategoryID`参数。 简单地说，不返回的任何供应商。

访问者在国家/地区，但是，输入，并单击显示供应商按钮会导致回发中，ObjectDataSource 的后`Select`方法重新查询，在 TextBox 控件中传递`Text`值作为`country`参数。


[![显示来自加拿大这些供应商](declarative-parameters-cs/_static/image26.png)](declarative-parameters-cs/_static/image25.png)

**图 9**： 显示这些供应商来自加拿大 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image27.png))


## <a name="showing-all-suppliers-by-default"></a>显示默认情况下的所有供应商

而是不是首先查看网页时显示供应商提供的任何我们可能想要显示*所有*供应商在第一个，这样就允许用户通过在文本框中输入国家/地区名称列表中向下将端点。 当文本框为空，`SuppliersBLL`类的`GetSuppliersByCountry(country)`方法传入`null`值及其*`country`* 输入的参数。 这`null`值然后传到 DAL`GetSupplierByCountry(country)`方法，它将转换到的数据库`NULL`值`@Country`在下面的查询参数：

[!code-sql[Main](declarative-parameters-cs/samples/sample3.sql)]

表达式`Country = NULL`始终返回 False，即使对于记录其`Country`列为`NULL`值; 因此，返回任何记录。

若要返回*所有*供应商的国家/地区文本框为空时，我们可以增强`GetSuppliersByCountry(country)`中 BLL 要调用的方法`GetSuppliers()`方法及其国家/地区参数时`null`并调用 DAL 的`GetSuppliersByCountry(country)`否则为方法。 这会返回指定任何国家/地区的所有供应商和供应商提供的适当的子集，包括国家/地区参数时的效果。

更改`GetSuppliersByCountry(country)`中的方法`SuppliersBLL`类所示：

[!code-csharp[Main](declarative-parameters-cs/samples/sample4.cs)]

进行此更改后`DeclarativeParams.aspx`页面将显示所有供应商提供第一次访问时的 (或每当`CountryName`文本框为空)。


[![所有供应商是现在默认情况下显示](declarative-parameters-cs/_static/image29.png)](declarative-parameters-cs/_static/image28.png)

**图 10**： 所有供应商是现在默认情况下显示 ([单击以查看实际尺寸的图像](declarative-parameters-cs/_static/image30.png))


## <a name="summary"></a>总结

若要使用的输入参数使用方法，我们需要在 ObjectDataSource 的指定参数的值`SelectParameters`集合。 不同类型的参数允许从不同的源获得参数值。 默认参数类型使用硬编码的值，但正如轻松 （和无需编写一行代码） 可以从查询字符串、 会话变量、 cookie 和页上的 Web 控件中甚至用户输入的值获取参数值。

在本教程中介绍了我们的示例阐释了如何使用声明性参数值。 但是，可能会我们需要使用参数源不可用，例如当前日期和时间，或者，如果我们的站点使用的成员资格，访问者的用户 ID。 对于这种情况下我们可以设置参数值以编程方式在 ObjectDataSource 之前调用其基础对象的方法。 我们将了解如何实现此目标[下一教程](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-data-with-the-objectdatasource-cs.md)
> [下一页](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
