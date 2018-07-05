---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
title: 嵌套的数据 Web 控件 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将探讨如何使用 Repeater 嵌套在另一个 Repeater。 这些示例将演示了如何以填充内部 Repeater 这两个 d...
ms.author: aspnetcontent
ms.date: 09/13/2006
ms.assetid: 8b7fcf7b-722b-498d-a4e4-7c93701e0c95
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 45e460edb09fe9398d204e0f280dfb088a44946d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803173"
---
<a name="nested-data-web-controls-vb"></a>嵌套的数据 Web 控件 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_VB.exe)或[下载 PDF](nested-data-web-controls-vb/_static/datatutorial32vb1.pdf)

> 在本教程中我们将探讨如何使用 Repeater 嵌套在另一个 Repeater。 这些示例将演示了如何以声明方式和以编程方式填充内部 Repeater。


## <a name="introduction"></a>介绍

除了静态 HTML 和数据绑定语法，模板还可包含 Web 控件和用户控件。 这些 Web 控件可以有其属性分配通过声明性数据绑定语法，或可以在相应的服务器端事件处理程序中以编程方式访问。

通过嵌入在模板中的控件，可自定义和改进的外观和用户体验。 例如，在[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)教程中，我们已了解如何通过在 TemplateField 来显示雇员的雇佣日期; 中添加一个日历控件自定义 GridView 的显示[添加验证控件的编辑和插入接口](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)并[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程，我们已了解如何自定义的编辑和插入界面添加验证控件、 文本框、 Dropdownlist 和其他 Web 控件。

模板还可以包含其他数据 Web 控件。 也就是说，我们可以让其模板中包含另一个 DataList （或转发器或 GridView 或 DetailsView，等等） DataList。 此类接口的挑战适当的数据绑定到的内部数据 Web 控件。 有几个不同的方法可用，范围为从使用于编程的 ObjectDataSource 的声明性选项。

在本教程中我们将探讨如何使用 Repeater 嵌套在另一个 Repeater。 外部 Repeater 将包含在数据库中，每个类别的项显示类别名称和说明。 每个类别项 s 内部 Repeater 将显示属于该类别的每个产品的信息 （请参阅图 1） 中的项目符号列表。 我们的示例将演示了如何以声明方式和以编程方式填充内部 Repeater。


[![列出每个类别，以及其产品，](nested-data-web-controls-vb/_static/image2.png)](nested-data-web-controls-vb/_static/image1.png)

**图 1**： 列出每个类别，以及其产品，([单击以查看实际尺寸的图像](nested-data-web-controls-vb/_static/image3.png))


## <a name="step-1-creating-the-category-listing"></a>步骤 1： 创建的类别列表

当生成使用嵌套数据 Web 控件时，我发现非常有用的设计、 创建和测试最外面的数据 Web 控件第一次，而无需担心内部嵌套的控件甚至。 因此，让我们来开始将 Repeater 添加到列表的名称和每个类别的说明页所需的步骤执行每个步骤。

首先打开`NestedControls.aspx`页中`DataListRepeaterBasics`文件夹并将 Repeater 控件添加到页上，设置其`ID`属性设置为`CategoryList`。 从 Repeater s 智能标记中，选择创建名为新 ObjectDataSource `CategoriesDataSource`。


[![命名新 ObjectDataSource CategoriesDataSource](nested-data-web-controls-vb/_static/image5.png)](nested-data-web-controls-vb/_static/image4.png)

**图 2**： 命名新 ObjectDataSource `CategoriesDataSource` ([单击以查看实际尺寸的图像](nested-data-web-controls-vb/_static/image6.png))


以便它将从其数据配置 ObjectDataSource`CategoriesBLL`类的`GetCategories`方法。


[![配置对象数据源使用 CategoriesBLL 类的 GetCategories 方法](nested-data-web-controls-vb/_static/image8.png)](nested-data-web-controls-vb/_static/image7.png)

**图 3**： 配置为使用 ObjectDataSource`CategoriesBLL`类 s`GetCategories`方法 ([单击以查看实际尺寸的图像](nested-data-web-controls-vb/_static/image9.png))


若要指定 Repeater 的模板内容需要转到源视图并手动输入的声明性语法。 添加`ItemTemplate`，它显示在类别的名称`<h4>`元素和一个段落元素中的类别的说明 (`<p>`)。 此外，let s 用水平标尺分隔每个类别 (`<hr>`)。 进行这些更改后您的页面应包含用于 Repeater 和类似于以下的 ObjectDataSource 声明性语法：


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample1.aspx)]

图 4 显示了我们的浏览器查看时的进度。


[![每个类别名称和描述列出，则分隔水平标尺](nested-data-web-controls-vb/_static/image11.png)](nested-data-web-controls-vb/_static/image10.png)

**图 4**： 每个类别的名称和描述列出，则用水平标尺分隔 ([单击以查看实际尺寸的图像](nested-data-web-controls-vb/_static/image12.png))


## <a name="step-2-adding-the-nested-product-repeater"></a>步骤 2： 添加嵌套的产品 Repeater

列出完整的类别，与我们的下一个任务是将添加到 Repeater `CategoryList` s`ItemTemplate`显示有关这些产品属于相应的类别的信息。 有多种方式，我们可以为此内部 Repeater，其中两个我们很快就会检索数据。 现在，让 s 只需创建产品 Repeater 中`CategoryList`Repeater 的`ItemTemplate`。 具体而言，让我们来安装产品 Repeater 显示项目符号列表中的每个产品与每个列表项包括产品的名称和价格。

若要创建我们需要手动输入的内部 Repeater s 声明性语法和模板到此 Repeater `CategoryList` s `ItemTemplate`。 添加以下标记内的`CategoryList`Repeater 的`ItemTemplate`:


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>步骤 3： 绑定到 ProductsByCategoryList Repeater 的特定于类别的产品

如果您在这里访问通过浏览器页面，屏幕将显示如图 4 所示相同因为我们尚未将任何数据绑定到 Repeater 的 ve。 有几种方法，我们可以获取相应的产品记录并将其绑定到 Repeater，比其他一些更高效。 此处的主要挑战取回指定类别的相应产品。

要将绑定到内部 Repeater 控件的数据可以访问以声明方式，通过在 ObjectDataSource `CategoryList` Repeater 的`ItemTemplate`，或以编程方式，从 ASP.NET 页的代码隐藏页。 同样，此数据可绑定到内部 Repeater 或者以声明方式-通过内部 Repeater s`DataSourceID`属性或通过声明性数据绑定语法或以编程方式通过引用在内部 Repeater `CategoryList` Repeater s`ItemDataBound`事件处理程序，以编程方式设置其`DataSource`属性，并调用其`DataBind()`方法。 让我们来探讨每一个这些方法。

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>访问数据以声明方式使用 ObjectDataSource 控件和`ItemDataBound`事件处理程序

自我们已使用在本系列教程的最适合用于访问数据，此示例中坚持使用 ObjectDataSource 整个广泛 ObjectDataSource。 `ProductsBLL`类具有`GetProductsByCategoryID(categoryID)`方法，它返回有关属于指定这些产品的信息*`categoryID`*。 因此，我们可以添加到 ObjectDataSource `CategoryList` Repeater 的`ItemTemplate`并将其配置为从此类的方法访问其数据。

遗憾的是，Repeater 不允许其模板无法通过设计视图编辑，因此我们需要手动添加此 ObjectDataSource 控件声明性语法。 下面的语法演示`CategoryList`Repeater s`ItemTemplate`后添加此新对象数据源 (`ProductsByCategoryDataSource`):


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample3.aspx)]

使用 ObjectDataSource 方法时，我们需要设置`ProductsByCategoryList`Repeater s`DataSourceID`属性设置为`ID`的 ObjectDataSource (`ProductsByCategoryDataSource`)。 另请注意，我们 ObjectDataSource 已`<asp:Parameter>`指定的元素*`categoryID`* 值将传递到`GetProductsByCategoryID(categoryID)`方法。 但如何指定此值呢？ 理想情况下，我们 d 能够只需将设置`DefaultValue`属性的`<asp:Parameter>`元素使用数据绑定语法如下所示：


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample4.aspx)]

遗憾的是，数据绑定语法才有效中具有控件`DataBinding`事件。 `Parameter`类缺少这种情况下，因此上述语法是非法的并将导致运行时错误。

若要设置此值，我们需要创建的事件处理程序`CategoryList`Repeater 的`ItemDataBound`事件。 请记住，`ItemDataBound`事件触发一次绑定到 Repeater 的每个项。 因此，对于外部 Repeater 将引发此事件每次我们可以分配当前`CategoryID`值设为`ProductsByCategoryDataSource`ObjectDataSource 的`CategoryID`参数。

创建事件处理程序`CategoryList`Repeater 的`ItemDataBound`事件使用以下代码：


[!code-vb[Main](nested-data-web-controls-vb/samples/sample5.vb)]

此事件处理程序首先会确保我们重新处理数据项而不是标头、 页脚或分隔符项。 接下来，我们引用的实际`CategoriesRow`只需绑定到当前实例`RepeaterItem`。 最后，我们引用在 ObjectDataSource `ItemTemplate` ，并分配其`CategoryID`参数值为`CategoryID`的当前`RepeaterItem`。

与此事件处理程序中， `ProductsByCategoryList` Repeater 中每个`RepeaterItem`绑定到这些产品`RepeaterItem`的类别。 图 5 显示生成的输出的屏幕截图。


[![外部 Repeater 列出了每个类别;内部的一个为该类别中列出的产品](nested-data-web-controls-vb/_static/image14.png)](nested-data-web-controls-vb/_static/image13.png)

**图 5**: 外部 Repeater 列出了每个类别; 内部一个列出该类别的产品 ([单击以查看实际尺寸的图像](nested-data-web-controls-vb/_static/image15.png))


## <a name="accessing-the-products-by-category-data-programmatically"></a>以编程方式访问的产品类别数据

而不是使用 ObjectDataSource 来检索当前类别的产品，我们可以在我们的 ASP.NET 页面 + s 代码隐藏类中创建一种方法 (或在`App_Code`文件夹或在单独的类库项目) 返回相应的一组产品中传递时`CategoryID`。 假设我们有这样的方法，在我们的 ASP.NET 页面 + s 代码隐藏类中被命名为`GetProductsInCategory(categoryID)`。 使用此方法准备就绪后我们无法绑定到使用下面的声明性语法内部 Repeater 当前类别的产品：


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample6.aspx)]

Repeater s`DataSource`属性使用的数据绑定语法来指示其数据来自于`GetProductsInCategory(categoryID)`方法。 由于`Eval("CategoryID")`返回类型的值`Object`，我们将对象转换为`Integer`然后再将其传递`GetProductsInCategory(categoryID)`方法。 请注意，`CategoryID`访问下面的语法是通过数据绑定`CategoryID`中*外部*Repeater (`CategoryList`)，即该 s 绑定到的记录`Categories`表。 因此，我们知道`CategoryID`不能为数据库`NULL`值，该值就是我们可以隐式强制转换的原因`Eval`方法，而如果检查我们重新处理`DBNull`。

使用此方法时，我们需要创建`GetProductsInCategory(categoryID)`方法，并将其检索相应的一组给定所提供的产品*`categoryID`*。 可以为此，我们只需返回`ProductsDataTable`返回的`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。 让我们来创建`GetProductsInCategory(categoryID)`中的代码隐藏类的方法我们`NestedControls.aspx`页。 完成此操作使用以下代码：


[!code-vb[Main](nested-data-web-controls-vb/samples/sample7.vb)]

此方法只需创建的实例`ProductsBLL`方法，并返回的结果`GetProductsByCategoryID(categoryID)`方法。 请注意该方法必须标记为`Public`或`Protected`; 如果该方法标记为`Private`，它将不能从 ASP.NET 页 s 声明性标记访问。

若要使用此新技术这些更改后，请花点时间查看通过浏览器页面。 输出应与输出相同时使用 ObjectDataSource 和`ItemDataBound`事件处理程序方法 （回头查看图 5，请参阅屏幕截图）。

> [!NOTE]
> 它可能看起来通话创建`GetProductsInCategory(categoryID)`ASP.NET 页面 + s 代码隐藏类中的方法。 毕竟，此方法只需创建的实例`ProductsBLL`类，并返回的结果及其`GetProductsByCategoryID(categoryID)`方法。 为什么不只是调用此方法直接从内部中继器中的数据绑定语法如： `DataSource='<%# ProductsBLL.GetProductsByCategoryID(CType(Eval("CategoryID"), Integer)) %>'`？ 尽管此语法赢得了我们的当前实现不起作用`ProductsBLL`类 (由于`GetProductsByCategoryID(categoryID)`方法是实例方法)，您可以修改`ProductsBLL`包括静态`GetProductsByCategoryID(categoryID)`方法或具有包括静态类`Instance()`方法返回的新实例`ProductsBLL`类。


虽然此类修改将不再需要`GetProductsInCategory(categoryID)`ASP.NET 页面 + s 代码隐藏类中的方法，代码隐藏类方法使我们更灵活地使用检索的数据，我们稍后将看到。

## <a name="retrieving-all-of-the-product-information-at-once"></a>检索所有次产品信息

两个早期技术我们检查已通过调用获取这些类别的产品的当前`ProductsBLL`类 s`GetProductsByCategoryID(categoryID)`方法 (第一种方法之所以这样做是通过对象数据源，通过第二个`GetProductsInCategory(categoryID)`中的方法代码隐藏类）。 每次调用此方法，直至数据访问层，业务逻辑层调用的查询返回行的 SQL 语句的数据库`Products`表`CategoryID`字段与匹配所提供的输入的参数。

给定*N*系统中的类别，这种方法网络*N* + 1 调用数据库数据库查询来获取所有类别，然后*N*调用以获取产品特定于每个类别。 但是，我们可以检索仅使用两个数据库调用一次调用获取所有各类别以及一个用于获取所有产品的所有所需的数据。 一旦我们有的所有产品，我们可以筛选这些产品因此，只有匹配当前的产品`CategoryID`绑定到该类别 s 内部 Repeater。

若要提供此功能，我们只需稍做修改到`GetProductsInCategory(categoryID)`中我们的 ASP.NET 页面 + s 代码隐藏类的方法。 而不是盲目地返回的结果`ProductsBLL`类 s`GetProductsByCategoryID(categoryID)`方法中，我们可以改为第一次访问*所有*的产品 (如果它们没有 t 已访问)，然后返回的只是筛选的视图产品基于传入的`CategoryID`。


[!code-vb[Main](nested-data-web-controls-vb/samples/sample8.vb)]

请注意页面级变量添加`allProducts`。 此保存有关的所有产品的信息，会填充第一次`GetProductsInCategory(categoryID)`调用方法。 之后，确保`allProducts`，创建对象并将其填充方法筛选器 DataTable 的结果，以便它的行只`CategoryID`匹配指定`CategoryID`可访问。 这种方法可以减少从访问数据库的次数*N* + 两到 1。

此增强功能不会引入到页面的呈现的标记的任何更改，也不会带来另一种方法比返回更少的记录。 它只是减少了对数据库的调用数。

> [!NOTE]
> 一个直观的方式可能原因减少数据库访问的数量也会肯定提高性能。 但是，这可能不是这种情况。 如果有大量的产品的`CategoryID`是`NULL`，有关示例，然后调用`GetProducts`方法返回的永远不会显示的产品数目。 此外，返回的所有产品会都很浪费如果您重新仅显示子集的类别，可能会都出现这种情况，如果已实现分页。


如往常一样，当涉及到分析两种技术的性能，仅欢心的度量值是运行适合你应用程序 s 的常见案例方案的受控的测试。

## <a name="summary"></a>总结

在本教程中我们已了解如何将嵌套一个数据 Web 控件在另一个，专门研究具有与列出的项目符号列表中每个类别的产品内部 Repeater 显示每个类别项外部 Repeater。 生成嵌套的用户界面的主要难题在于访问以及正确的数据绑定到的内部数据 Web 控件。 有各种技术可用，我们在本教程中探讨其中两个。 检查第一种方法中的外部数据 Web 控件 s 使用 ObjectDataSource`ItemTemplate`的已绑定到内部数据 Web 控件通过其`DataSourceID`属性。 第二种方法来访问这些数据通过 ASP.NET 页面的代码隐藏类中的方法。 然后，此方法可以绑定到的内部数据 Web 控件的`DataSource`通过数据绑定语法的属性。

尽管在本教程中检查嵌套的用户界面使用 Repeater Repeater 中嵌套，但这些技术可以扩展到其他数据 Web 控件。 您可以嵌套 GridView 或 DataList 内的 GridView 中 Repeater 等。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones 和 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
