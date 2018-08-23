---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: 自定义格式设置取决于数据 (C#) |Microsoft Docs
author: rick-anderson
description: 可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。 在本教程中，我们将 l...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: ee9cdf19769ea63388fd9dd18a82bb2b4dcdef87
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834568"
---
<a name="custom-formatting-based-upon-data-c"></a>自定义格式设置取决于数据 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe)或[下载 PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)

> 可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。 在本教程中我们将介绍如何完成数据绑定通过使用 DataBound 和 RowDataBound 事件处理程序格式设置。


## <a name="introduction"></a>介绍

可以通过大量与样式有关的属性的自定义 GridView、 DetailsView 和 FormView 控件的外观。 属性，如`CssClass`， `Font`， `BorderWidth`， `BorderStyle`， `BorderColor`， `Width`，和`Height`，等等，指示呈现的控件的常规外观。 属性包括`HeaderStyle`， `RowStyle`， `AlternatingRowStyle`，和其他允许这些相同的样式设置将应用于特定部分。 同样，可以在字段级别应用这些样式设置。

在许多情况下，格式设置要求取决于所显示的数据的值。 例如，若要绘制注意若要查看的常用产品，一个报告，列出产品信息可能背景颜色设置为对这些产品的黄色`UnitsInStock`和`UnitsOnOrder`字段都等于 0。 若要突出显示的成本更高的产品，我们可能想要显示多个为加粗字体中 75.00 美元的成本计算这些产品的价格。

可以通过多种方式来调整的 GridView、 detailsview 和 FormView 取决于绑定到它的数据格式。 在本教程中我们将介绍如何完成数据绑定使用格式设置`DataBound`和`RowDataBound`事件处理程序。 在下一教程中，我们将探讨一种替代方法。

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>使用 DetailsView 控件`DataBound`事件处理程序

当数据绑定到 DetailsView，从数据源控件或通过以编程方式将数据分配给控件的`DataSource`属性并调用其`DataBind()`方法时，执行以下步骤序列：

1. 数据 Web 控件的`DataBinding`事件触发。
2. 数据绑定到数据 Web 控件。
3. 数据 Web 控件的`DataBound`事件触发。

可以通过事件处理程序的步骤 1 和 3 后立即插入自定义逻辑。 通过创建的事件处理程序`DataBound`我们可以以编程方式确定已被数据绑定到数据 Web 控件并调整的格式设置的按需的事件。 为了说明这一点让我们创建的将列出关于某种产品的常规信息，但会显示 DetailsView`UnitPrice`中的值***加粗、 倾斜字体***如果超过 $75.00。

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>步骤 1： 在 DetailsView 中显示的产品信息

打开`CustomColors.aspx`页中`CustomFormatting`文件夹中，将从工具箱拖到设计器的 DetailsView 控件，设置其`ID`属性值设置为`ExpensiveProductsPriceInBoldItalic`，并将其绑定到新的 ObjectDataSource 控件调用`ProductsBLL`类的`GetProducts()`方法。 实现此目的的详细的步骤为简洁起见，我们探讨这些详细信息中在前面的教程中由于此处省略。

一旦您已绑定到 DetailsView 的 ObjectDataSource，花点时间来修改字段列表。 我选择要删除`ProductID`， `SupplierID`， `CategoryID`， `UnitsInStock`， `UnitsOnOrder`， `ReorderLevel`，和`Discontinued`BoundFields 和重命名和重新格式化剩余 BoundFields。 我也被清除`Width`和`Height`设置。 由于 DetailsView 显示单个记录，我们需要启用分页，才能允许最终用户可以查看所有产品。 通过检查 DetailsView 的智能标记中的启用分页复选框来实现。


[![检查 DetailsView 的智能标记中的启用分页复选框](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)

**图 1**： 检查启用分页中的复选框 DetailsView 的智能标记 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image3.png))


更改后，将为 DetailsView 标记：


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

请花费片刻时间来查看此页在浏览器中测试。


[![在 DetailsView 控件一次显示一种产品](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)

**图 2**： 根据 DetailsView 控件显示一个产品一次 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image6.png))


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步骤 2： 以编程方式确定数据绑定事件处理程序中的数据的值

若要对这些产品加粗、 倾斜字体显示价格其`UnitPrice`值超过 $75.00，我们需要首先能以编程方式确定`UnitPrice`值。 对于 DetailsView，这可以完成`DataBound`事件处理程序。 若要创建事件处理程序在设计器中 DetailsView 单击，然后导航到属性窗口。 按 F4 以显示它，如果不可见，或转到视图菜单并选择属性窗口的菜单选项。 在属性窗口中，单击闪电形图标以列出 DetailsView 的事件。 接下来，双击`DataBound`事件或键入你想要创建的事件处理程序的名称。


![为数据绑定事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image7.png)

**图 3**： 创建的事件处理程序`DataBound`事件


执行此操作将自动创建事件处理程序，并将您带到的代码部分添加的位置。 此时会看到：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

可以通过访问数据绑定到 DetailsView`DataItem`属性。 回想一下，我们将我们控件绑定到的强类型化 DataRow 实例的集合组成的强类型化 DataTable。 在 DataTable 绑定到 DetailsView，DataTable 中的第一个 DataRow 分配给 DetailsView`DataItem`属性。 具体而言，`DataItem`属性分配`DataRowView`对象。 我们可以使用`DataRowView`的`Row`属性来访问基础 DataRow 对象，它是实际`ProductsRow`实例。 一旦我们有这`ProductsRow`我们可以通过简单地检查对象的属性值使我们决策的实例。

下面的代码演示如何确定是否`UnitPrice`绑定到 DetailsView 控件的值是否大于 $75.00:


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> 由于`UnitPrice`可以有`NULL`数据库中的值，我们首先检查以确保，我们并没有解决`NULL`值，然后才能访问`ProductsRow`的`UnitPrice`属性。 此检查非常重要因为如果我们尝试访问`UnitPrice`属性时它具有`NULL`值`ProductsRow`对象将引发[StrongTypingException 异常](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)。


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>步骤 3： 设置 DetailsView 中的单价值的格式

现在我们可以确定是否`UnitPrice`值绑定到 DetailsView 具有某个值超过 $75.00，不过我们但若要了解如何以编程方式调整 DetailsView 的格式设置相应地。 若要修改在 DetailsView 中整个行的格式设置，以编程方式访问行使用`DetailsViewID.Rows[index]`; 若要修改特定单元格，访问，请使用`DetailsViewID.Rows[index].Cells[index]`。 一旦我们有对我们然后可以通过设置其样式相关的属性来调整其外观的单元格的行的引用。

访问行以编程方式要求你知道的行的索引，从 0 开始。 `UnitPrice`行是 DetailsView，向其提供的 4 索引并使其以编程方式访问中的第五个行使用`ExpensiveProductsPriceInBoldItalic.Rows[4]`。 现在我们可以使用以下代码显示加粗、 倾斜字体中的整个行的内容：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

但是，这将使*同时*标签 （价格） 和粗体和斜体的值。 如果我们想要使只是值粗体和斜体我们需要将此应用到的第二个单元格的行，可以使用以下格式：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

由于我们的教程到目前为止已使用样式表来维护与样式有关的信息呈现的标记之间完全分离，而不是设置特定的样式属性，如上所示让我们改为使用 CSS 类。 打开`Styles.css`样式表并添加一个名为的新 CSS 类`ExpensivePriceEmphasis`以下定义：


[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

然后，在`DataBound`事件处理程序设置的单元格`CssClass`属性设置为`ExpensivePriceEmphasis`。 下面的代码演示`DataBound`完整的事件处理程序：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

时查看 Chai，小于 75.00 美元的费用，价格显示为正常字体 （请参阅图 4）。 但是，当查看 Mishi Kobe Niku，具有 97.00 美元的价格，价格会显示在加粗、 倾斜字体 （请参见图 5）。


[![价格小于 $75.00 将显示在普通字体](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)

**图 4**： 价格小于 $75.00 将显示在普通字体 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image10.png))


[![粗体、 斜体字体显示昂贵产品的价格](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)

**图 5**： 中加粗、 倾斜字体显示昂贵产品的价格 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image13.png))


## <a name="using-the-formview-controlsdataboundevent-handler"></a>使用 FormView 控件`DataBound`事件处理程序

确定基础数据绑定到 FormView 的步骤是相同的 DetailsView 创建`DataBound`事件处理程序，强制转换`DataItem`为适当的对象类型的属性绑定到控件，并确定如何继续执行。 FormView 和 DetailsView 有所不同，但是，在如何更新用户界面的外观。

FormView 不包含任何 BoundFields 并因此缺少`Rows`集合。 相反，FormView 组成的模板，可以包含多种静态 HTML，Web 控件和数据绑定语法。 调整的 FormView 样式通常涉及调整一个或多个 FormView 的模板中的 Web 控件的样式。

若要说明这一点，让我们使用 FormView 到产品列表中上一示例中，但这次让我们喜欢显示只是产品名称和单位以红色字体显示，如果它小于或等于 10 的库存数量的库存数量。

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>步骤 4： 在 FormView 中显示的产品信息

添加到 FormView`CustomColors.aspx`页下的 DetailsView 并设置其`ID`属性设置为`LowStockedProductsInRed`。 将 FormView 绑定到上一步中创建的 ObjectDataSource 控件。 这将创建`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`FormView 的。 删除`EditItemTemplate`和`InsertItemTemplate`并简化`ItemTemplate`包括只需`ProductName`和`UnitsInStock`值，每个在其自己适当地命名为标签控件中。 与前面的示例从 DetailsView，还检查 FormView 的智能标记中的启用分页复选框。

以后这些编辑 FormView 的标记看起来应类似于下面：


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

请注意，`ItemTemplate`包含：

- **静态 HTML**文本"产品:"和"库存数量:"连同`<br />`和`<b>`元素。
- **Web 控件**两个标签控件，`ProductNameLabel`和`UnitsInStockLabel`。
- **数据绑定语法**`<%# Bind("ProductName") %>`并`<%# Bind("UnitsInStock") %>`语法，将从这些字段的值分配给标签控件的`Text`属性。

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步骤 5： 以编程方式确定数据绑定事件处理程序中的数据的值

使用 FormView 的标记完成下, 一步是以编程方式确定如果`UnitsInStock`值是否小于或等于 10。 完成此操作完全相同的方式与 FormView 中使用 DetailsView 一样。 首先，创建一个事件处理程序的 FormView 的`DataBound`事件。


![创建数据绑定事件处理程序](custom-formatting-based-upon-data-cs/_static/image14.png)

**图 6**： 创建`DataBound`事件处理程序


在事件处理程序转换 FormView`DataItem`属性设置为`ProductsRow`实例，并确定是否`UnitsInPrice`值是这样，我们需要以红色字体显示。


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>步骤 6： 格式设置在 FormView ItemTemplate UnitsInStockLabel 标签控件

最后一步是设置的格式显示`UnitsInStock`以红色字体值，如果值为 10 或更少。 若要完成此我们需要以编程方式访问`UnitsInStockLabel`控件中`ItemTemplate`并设置其样式属性，以便显示其文本为红色。 若要访问的 Web 控件模板中，使用`FindControl("controlID")`方法如下：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

对于我们的示例中我们想要访问标签控件`ID`值是`UnitsInStockLabel`，因此，我们将使用：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

对 Web 控件的编程引用后，我们可以根据需要修改其与样式有关的属性。 如前面的示例中，我创建了中的 CSS 类`Styles.css`名为`LowUnitsInStockEmphasis`。 若要将此样式应用于标签 Web 控件，设置其`CssClass`属性相应地。


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> 格式设置以编程方式访问使用在 Web 控件模板的语法`FindControl("controlID")`，然后设置其样式相关的属性还可用使用时[Templatefield](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 或 GridView 中控件。 我们将在下一教程中我们介绍 Templatefield。


图 7 显示了 FormView 查看产品时其`UnitsInStock`值大于 10，而图 8 中的产品具有其值小于 10。


[![对于产品具有足够大 Units In Stock，无自定义格式设置将应用](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)

**图 7**： 应用的产品具有足够大 Units In Stock、 无自定义格式设置 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image17.png))


[![在库存数量的单位以红色显示的那些产品使用的值小于或等于 10](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)

**图 8**： 内库存数量的设备以红色显示的那些产品使用的值小于或等于 10 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image20.png))


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>使用 GridView 的格式设置`RowDataBound`事件

前面部分中，我们探讨的一系列步骤 DetailsView 和 FormView 控件在数据绑定期间通过进度。 让我们看这些步骤再一次作为刷新程序。

1. 数据 Web 控件的`DataBinding`事件触发。
2. 数据绑定到数据 Web 控件。
3. 数据 Web 控件的`DataBound`事件触发。

这三个简单步骤便足以针对 DetailsView 和 FormView，因为它们显示单个记录。 对于 GridView，其中显示*所有*记录绑定到它 （而不仅仅是第一个），第 2 步是稍微要复杂。

步骤的 2 GridView 枚举数据源，并为每个记录创建`GridViewRow`实例并对其绑定的当前记录。 每个`GridViewRow`添加到 GridView，会引发两个事件：

- **`RowCreated`** 之后才激发`GridViewRow`已创建
- **`RowDataBound`** 已绑定到当前记录之后激发`GridViewRow`。

对于 GridView 中，然后，数据绑定更准确地描述了通过以下步骤序列：

1. GridView 的`DataBinding`事件触发。
2. 将数据绑定到 GridView。   
  
   为数据源中的每个记录 

    1. 创建`GridViewRow`对象
    2. 激发`RowCreated`事件
    3. 将绑定到的记录 `GridViewRow`
    4. 激发`RowDataBound`事件
    5. 添加`GridViewRow`到`Rows`集合
3. GridView 的`DataBound`事件触发。

若要自定义 GridView 的单个记录的格式，然后，我们需要创建的事件处理程序`RowDataBound`事件。 若要说明这一点，让我们将添加到 GridView`CustomColors.aspx`页面列出了名称、 类别和每个产品，突出显示的价格是不超过 10.00 美元的部分用黄色背景颜色的那些产品价格。

## <a name="step-7-displaying-product-information-in-a-gridview"></a>步骤 7： 在 GridView 中显示的产品信息

上一示例中添加下 FormView GridView，并设置其`ID`属性设置为`HighlightCheapProducts`。 因为我们已经有 ObjectDataSource，返回所有产品页上，将 GridView 绑定到的。 最后，编辑 GridView 的 BoundFields 包括只需产品的名称、 类别和价格。 在这些编辑后 GridView 的标记应如下所示：


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

图 9 显示了我们到目前为止的浏览器查看时的进度。


[![GridView 列出名称、 类别和每个产品的价格](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)

**图 9**: GridView 列出名称、 类别和每个产品的价格 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image23.png))


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>步骤 8： 以编程方式确定 RowDataBound 事件处理程序中的数据的值

当`ProductsDataTable`绑定到 GridView 其`ProductsRow`已枚举，并为每个实例`ProductsRow``GridViewRow`创建。 `GridViewRow`的`DataItem`属性分配给特定`ProductRow`，在其后 GridView 的`RowDataBound`引发事件处理程序。 若要确定`UnitPrice`每个产品的值绑定到 GridView，然后，我们需要为 GridView 的创建事件处理程序`RowDataBound`事件。 在此事件处理程序可以检查`UnitPrice`值为当前`GridViewRow`，并为该行格式设置决定。

可以使用 FormView 和 DetailsView 中使用相同的一系列步骤作为创建此事件处理程序。


![GridView 的 RowDataBound 事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image24.png)

**图 10**： 创建 GridView 的事件处理程序`RowDataBound`事件


以这种方式创建的事件处理程序将导致自动添加到 ASP.NET 页面的代码部分的以下代码：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

当`RowDataBound`事件触发时，事件处理程序作为其第二个参数传递类型的对象`GridViewRowEventArgs`，其中有一个名为`Row`。 此属性返回的引用`GridViewRow`那只是数据绑定。 访问`ProductsRow`实例绑定到`GridViewRow`我们使用`DataItem`属性如下所示：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

使用时`RowDataBound`务必要记住 GridView 组成不同类型的行，为激发此事件的事件处理程序*所有*行类型。 一个`GridViewRow`的类型可以由其`RowType`属性，并且可以具有的可能值之一：

- `DataRow` 从 GridView 绑定到一个记录的行 `DataSource`
- `EmptyDataRow` 如果显示的行 GridView 的`DataSource`为空
- `Footer` 脚注行;显示的如果 GridView 的`ShowFooter`属性设置为 `true`
- `Header` 标头行中;显示是否 GridView 的 ShowHeader 属性设置为`true`（默认值）
- `Pager` 对于 GridView 的实现分页，显示分页界面的行
- `Separator` 未使用 GridView，但由`RowType`DataList 和 Repeater 的属性控制，两个数据 Web 控件，我们将讨论在将来教程

由于`EmptyDataRow`， `Header`， `Footer`，和`Pager`行不与关联`DataSource`记录，它们将始终具有`null`值及其`DataItem`属性。 出于此原因，然后再尝试使用当前`GridViewRow`的`DataItem`属性，我们首先必须确保我们正在处理与`DataRow`。 这可以通过检查来实现`GridViewRow`的`RowType`属性如下所示：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>步骤 9： 突出显示行黄色时单价值是小于 10.00 美元

最后一步是以编程方式突出显示整个`GridViewRow`如果`UnitPrice`值的行是不超过 10.00 美元的部分。 访问一个 GridView 行或单元格的语法是与 DetailsView 相同`GridViewID.Rows[index]`若要访问整个行，`GridViewID.Rows[index].Cells[index]`访问特定单元格。 但是，当`RowDataBound`事件处理程序会触发数据绑定`GridViewRow`尚未添加到 GridView 的`Rows`集合。 因此，您不能访问当前`GridViewRow`实例与`RowDataBound`事件处理程序使用的行集合。

而不是`GridViewID.Rows[index]`，我们可以引用当前`GridViewRow`实例中`RowDataBound`事件处理程序使用`e.Row`。 也就是说，为了突出显示当前`GridViewRow`实例与`RowDataBound`事件处理程序，我们将使用：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

而不是设置`GridViewRow`的`BackColor`属性直接，让我们坚持使用 CSS 类。 我创建了一个名为的 CSS 类`AffordablePriceEmphasis`，将背景色设置为黄色。 已完成`RowDataBound`事件处理程序遵循：


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]


[![最经济的产品是黄色突出显示](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)

**图 11**： 最经济的产品是黄色突出显示 ([单击以查看实际尺寸的图像](custom-formatting-based-upon-data-cs/_static/image27.png))


## <a name="summary"></a>总结

在本教程中我们已了解如何设置 GridView、 DetailsView 和 FormView 基于绑定到控件的数据的格式。 若要完成此我们创建的事件处理程序`DataBound`或`RowDataBound`事件，如果需要格式设置的更改，以及检查基础数据是其中。 若要访问绑定到 detailsview FormView 的数据，我们使用`DataItem`中的属性`DataBound`事件处理程序; 对于 GridView 中后，每个`GridViewRow`实例的`DataItem`属性包含的数据绑定到该行，可在`RowDataBound`事件处理程序。

以编程方式调整数据 Web 控件的格式设置的语法取决于 Web 控件和要设置格式的数据的显示方式。 在 DetailsView 和 GridView 控件、 行和单元格可以访问的序号索引。 有关使用模板，FormView`FindControl("controlID")`方法通常用于查找从 Web 控件模板中的。

在下一教程中我们将介绍如何使用 GridView 和 DetailsView 中使用模板。 此外，我们将看到另一种方法用于自定义基于基础数据的格式设置。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 E.R. Gilmore，Dennis Patterson 和 Dan Jagers。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一篇](using-templatefields-in-the-gridview-control-cs.md)
