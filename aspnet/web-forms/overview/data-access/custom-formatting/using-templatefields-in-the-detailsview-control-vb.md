---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: DetailsView 控件 (VB) 中使用 Templatefield |Microsoft Docs
author: rick-anderson
description: 使用 GridView 提供的相同 Templatefield 功能，还提供与 DetailsView 控件。 在本教程中我们将显示一个产品...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 1c18e8be25369d6e7d1703e71b80e75adb9f15fa
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827235"
---
<a name="using-templatefields-in-the-detailsview-control-vb"></a>DetailsView 控件 (VB) 中使用 Templatefield
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe)或[下载 PDF](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> 使用 GridView 提供的相同 Templatefield 功能，还提供与 DetailsView 控件。 在本教程中我们将使用包含 Templatefield DetailsView 一次显示一个产品。


## <a name="introduction"></a>介绍

Templatefield 进一步提供了比 BoundField、 CheckBoxField、 HyperLinkField 和其他数据字段控件更高程度的灵活地呈现数据。 在中[前一篇教程](using-templatefields-in-the-gridview-control-vb.md)我们了解了在 GridView 中使用 templatefield 进一步：

- 在一列中显示多个数据字段值。 具体而言，这两`FirstName`和`LastName`字段已合并为一个 GridView 列。
- 使用备用的 Web 控件表示数据字段值。 我们已了解如何显示`HiredDate`值使用日历控件。
- 显示基于对基础数据的状态信息。 虽然`Employees`表不包含的列，返回的员工已在该作业的天数，我们能够在 GridView 的示例中使用 templatefield 进一步和格式设置方法与前面的教程中显示此类信息。

使用 GridView 提供的相同 Templatefield 功能，还提供与 DetailsView 控件。 在本教程中我们将使用包含两个 Templatefield DetailsView 一次显示一个产品。 将合并第一个 TemplateField `UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`到 DetailsView 一行的数据字段。 值将显示第二个 TemplateField`Discontinued`字段，但将使用的格式设置方法以显示"是"如果`Discontinued`是`True`，否则"NO"。


[![两个 Templatefield 用于自定义显示内容](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**图 1**： 两个 Templatefield 用于自定义显示 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image3.png))


让我们进入正题！

## <a name="step-1-binding-the-data-to-the-detailsview"></a>步骤 1： 将数据绑定到 DetailsView

如所述在上一教程中使用的 Templatefield 通常是最简单的方法首先创建包含只 BoundFields 的 DetailsView 控件然后添加新 Templatefield 或将现有 BoundFields 转换为 Templatefield 作为时需要. 因此，通过将 DetailsView 添加到通过设计器页面并将其绑定到返回的产品列表 ObjectDataSource 开始本教程。 这些步骤将为每个产品的非布尔值字段和一个布尔值字段 (Discontinued) CheckBoxField 与 BoundFields 创建 DetailsView。

打开`DetailsViewTemplateField.aspx`页上，将从工具箱拖到设计器的 DetailsView。 在 DetailsView 的智能标记选择添加新的 ObjectDataSource 控件，调用`ProductsBLL`类的`GetProducts()`方法。


[![添加新的 ObjectDataSource 控件，它调用 GetProducts() 方法](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**图 2**： 添加新的 ObjectDataSource 控件的 Invoke`GetProducts()`方法 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image6.png))


为此报表中删除`ProductID`， `SupplierID`， `CategoryID`，和`ReorderLevel`BoundFields。 接下来，对 BoundFields 重新排序，以便`CategoryName`并`SupplierName`BoundFields 紧跟`ProductName`BoundField。 可随意调整`HeaderText`属性和格式设置属性作为您 BoundFields 认为合适。 正如 gridview，通过字段对话框 （可通过单击 DetailsView 的智能标记中的编辑字段链接访问） 或通过声明性语法，可以执行这些 BoundField 级别编辑。 最后，清除 DetailsView`Height`和`Width`属性值，以允许 DetailsView 控件以展开根据显示的数据，并检查智能标记中的启用分页复选框。

进行这些更改后，DetailsView 控件的声明性标记应类似于下面：


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

花点时间查看通过浏览器页面。 此时应看到显示产品的名称、 类别、 供应商、 价格、 库存数量、 顺序上的单位和其已停止使用的状态行的一个产品列出 (Chai)。


[![使用一系列 BoundFields 显示产品的详细信息](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**图 3**： 根据产品的详细信息会显示使用 BoundFields 系列 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image9.png))


## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>步骤 2： 将价格、 存货单位和订货量合并为一行

在 DetailsView 具有对应的行`UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`字段。 我们可以将合并这些数据字段到单个行使用 TemplateField 通过添加新 TemplateField 或通过将一个现有转换`UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`转换为 TemplateField BoundFields。 尽管我个人更偏爱转换现有 BoundFields，让我们通过添加新 TemplateField 练习。

通过单击 DetailsView 的智能标记，以打开字段对话框中的编辑字段链接启动。 接下来，添加新 TemplateField 并设置其`HeaderText`属性设置为"价格和清单"并移动新 TemplateField 以便它位于上面`UnitPrice`BoundField。


[![将新 TemplateField 添加到 DetailsView 控件](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**图 4**： 将新 TemplateField 添加到 DetailsView 控件 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image12.png))


由于此新 templatefield 进一步将包含在当前显示的值`UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`BoundFields，让我们将其删除。

此步骤中的最后一个任务是定义`ItemTemplate`的价格和库存 TemplateField，可以是标记来通过 DetailsView 的模板通过控件的声明性语法编辑接口在设计器或手动实现。 GridView、 DetailsView 的模板编辑界面可以访问通过单击智能标记中的编辑模板链接。 从此处可以选择要编辑从下拉列表以及如何从工具箱将任何 Web 控件的模板。

对于本教程中，首先将标签控件添加到的价格和库存 TemplateField `ItemTemplate`。 接下来，单击编辑 DataBindings 链接从标签 Web 控件的智能标记并将绑定`Text`属性设置为`UnitPrice`字段。


[![将标签的 Text 属性绑定到单价数据字段](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**图 5**： 将标签的绑定`Text`属性设置为`UnitPrice`数据字段 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image15.png))


## <a name="formatting-the-price-as-a-currency"></a>作为一种货币格式设置价格

添加此元素后，标签 Web 控件价格和库存 TemplateField 现在会显示仅所选产品的价格。 图 6 显示了我们的进度的屏幕截图为止时的浏览器查看。


[![价格和库存 templatefield 进一步显示的价格](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**图 6**: 价格和库存 templatefield 进一步显示的价格 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image18.png))


请注意该产品的价格未格式化为货币。 使用 BoundField 格式设置是可以通过设置`HtmlEncode`属性设置为`False`并`DataFormatString`属性设置为`{0:formatSpecifier}`。 对于 TemplateField，但是，格式设置的说明进行操作必须指定数据绑定语法中或通过使用应用程序的代码 （如 ASP.NET 页面的代码隐藏类） 中的某一位置定义的格式设置方法。

若要指定标签 Web 控件中使用的数据绑定语法的格式设置，返回到数据绑定对话框中，通过单击标签的智能标记中的编辑 DataBindings 链接。 可以直接在格式下拉列表中键入的格式设置的说明进行操作，或选择一个定义的格式字符串。 喜欢使用 BoundField`DataFormatString`属性，指定格式设置是使用`{0:formatSpecifier}`。

有关`UnitPrice`字段的使用货币格式指定通过选择相应的下拉列表值或通过键入`{0:C}`手动。


[![设置价格的格式为货币](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**图 7**： 设置为货币价格的格式 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image21.png))


以声明方式，到第二个参数指示的格式规范`Bind`或`Eval`方法。 只需通过声明性标记中的以下数据绑定表达式中的设计器结果所做的设置：


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>将其余数据字段添加到 TemplateField

我们在此处显示并格式化`UnitPrice`数据字段中的价格和库存 TemplateField，但仍需要显示`UnitsInStock`和`UnitsOnOrder`字段。 让我们来显示这些行下面的价格，并在括号中。 从设计器中的模板编辑界面，可以将此类标记添加模板中将光标并只需在要显示的文本中键入。 或者，可以直接在声明性语法中输入此标记。

添加静态标记、 标签 Web 控件和数据绑定语法，以便价格和库存 templatefield 进一步显示的价格和库存信息如下所示：

*UnitPrice*  
(**库存 / Order:** *UnitsInStock* / *UnitsOnOrder*)

以后执行此任务 DetailsView 的声明性标记看起来应类似于下面：


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

使用这些更改，我们已经合并到单个 DetailsView 行的价格和库存信息。


[![在单行中显示的价格和清单信息](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**图 8**: 价格和库存信息会显示在单个行 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image24.png))


## <a name="step-3-customizing-the-discontinued-field-information"></a>步骤 3： 自定义中断的字段信息

`Products`表的`Discontinued`列是一个位值，指示是否已停止使用该产品。 布尔值字段中，当绑定到数据源控件的 DetailsView （或 GridView），如`Discontinued`，而非布尔值字段，如实现为 CheckBoxFields `ProductID`， `ProductName`，依此类推，作为实现BoundFields。 CheckBoxField 将呈现为一个已禁用的复选框，如果数据字段的值为 True，则取消选中否则检查。

而不是显示 CheckBoxField 我们可能想要改为显示文本，该值指示已停止使用该产品。 若要实现此目的我们无法从 DetailsView 删除 CheckBoxField，然后添加 BoundField 其`DataField`属性设置为`Discontinued`。 请花费片刻时间来执行此操作。 此更改后 DetailsView 显示的文本"True"停产的产品和"False"仍处于活动状态的产品。


[![字符串 True 和 False 用于显示已停止使用的状态](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**图 9**: 字符串 True 和使用 False 以显示已中断状态 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image27.png))


想象我们不想要的字符串"True"或"False"改为使用，但"YES"和"NO"。 此类自定义可以借助 TemplateField 和格式设置方法的执行。 格式设置方法可以采用任意数量的输入参数，但必须返回 HTML （作为字符串） 注入到模板。

添加到的格式设置方法`DetailsViewTemplateField.aspx`页面的代码隐藏类名为`DisplayDiscontinuedAsYESorNO`接受`Northwind.ProductsRow`对象作为输入参数并返回一个字符串。 前面的教程，此方法中所述*必须*标记为`Protected`或`Public`以便可从该模板。


[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

此方法检查输入的参数 (`discontinued`)，并返回"YES"，如果它是`True`，否则为"否"。

> [!NOTE]
> 在按以前的教程回想一下，我们也可能包含的数据字段会通过检查的格式设置方法`NULL`s，因此需要检查是否该雇员的`HiredDate`属性值有一个数据库`NULL`之前的值访问`EmployeesRow`的`HiredDate`属性。 此类检查不需要此处因为`Discontinued`列不能有数据库`NULL`分配的值。 此外，这就是原因的方法可以接受一个布尔值输入参数，而不是无需接受`ProductsRow`实例或类型参数的`Object`。


使用此格式设置方法完成，剩下的就是调用从 TemplateField `ItemTemplate`。 若要创建删除的 TemplateField `Discontinued` BoundField 和添加新 TemplateField 或转换`Discontinued`转换为 TemplateField BoundField。 然后，从声明性标记视图中，编辑 TemplateField，使其包含只需调用 ItemTemplate`DisplayDiscontinuedAsYESorNO`方法，传入的当前值`ProductRow`实例的`Discontinued`属性。 这可以通过访问`Eval`方法。 具体而言，TemplateField 标记应如下所示：


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

这将导致`DisplayDiscontinuedAsYESorNO`呈现 DetailsView 时要调用方法并传入`ProductRow`实例的`Discontinued`值。 由于`Eval`方法返回类型的值`Object`，但`DisplayDiscontinuedAsYESorNO`方法需要输入的参数的类型`Boolean`，我们将强制转换`Eval`方法返回值为`Boolean`。 `DisplayDiscontinuedAsYESorNO`方法会返回"YES"或"否"根据值接收。 返回的值是此 DetailsView 中显示的内容行 （请参阅图 10）。


[![是或否的值为现在 Discontinued 行中所示](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**图 10**: 是或否的值为现在 Discontinued 行中所示 ([单击以查看实际尺寸的图像](using-templatefields-in-the-detailsview-control-vb/_static/image30.png))


## <a name="summary"></a>总结

在 DetailsView 控件中的 TemplateField 允许灵活地显示数据，不是可与其他字段控件，并且非常适合的情况下使用更高位置：

- 多个数据字段需要一个 GridView 列中显示
- 最好使用 Web 控件，而不是纯文本格式表示数据
- 输出取决于基础数据，例如显示元数据或重新格式化数据

Templatefield 所考虑的更高的灵活性在 DetailsView 的基础数据的呈现，DetailsView 输出仍让人感觉有点 boxy 每个字段呈现为 HTML 中的一行`<table>`。

FormView 控件提供了更高的灵活地配置呈现的输出。 FormView 不包含字段，但而是一系列模板 (`ItemTemplate`， `EditItemTemplate`， `HeaderTemplate`，依此类推)。 我们将了解如何使用 FormView 我们下一步的教程中实现更多控制的呈现的布局。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Dan Jagers。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-templatefields-in-the-gridview-control-vb.md)
> [下一页](using-the-formview-s-templates-vb.md)
