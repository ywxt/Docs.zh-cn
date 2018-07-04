---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
title: 设置 DataList 和 Repeater 的格式取决于数据 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将逐步了解我们设置 DataList 和 Repeater 控件，通过使用格式设置的函数的外观的格式的示例...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 83e3d759-82b8-41e6-8d62-f0f4b3edec41
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: bc595064de2910dc25077d0241ef9a150fdd4cd1
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368335"
---
<a name="formatting-the-datalist-and-repeater-based-upon-data-c"></a>格式设置 DataList 和 Repeater 取决于数据 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_CS.exe)或[下载 PDF](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/datatutorial30cs1.pdf)

> 在本教程中我们将逐步了解我们设置 DataList 和 Repeater 控件，通过使用模板中的格式设置函数或通过处理数据绑定事件的外观的格式的示例。


## <a name="introduction"></a>介绍

正如我们看到在前面的教程，DataList 提供了多个与样式有关的属性影响其外观。 具体而言，我们已了解如何将默认的 CSS 类分配到 DataList s `HeaderStyle`， `ItemStyle`， `AlternatingItemStyle`，和`SelectedItemStyle`属性。 除了这四个属性，DataList 包括大量其他样式相关的属性，如`Font`， `ForeColor`， `BackColor`，和`BorderWidth`，仅举几例。 Repeater 控件不包含任何与样式有关的属性。 必须直接在 Repeater 的模板中的标记中进行任何此类样式设置。

通常情况下，不过，应如何格式化数据取决于数据本身。 例如，列出产品时我们可能想要以浅灰色字体颜色显示产品信息，如果它已停止使用，或者我们可能想要突出显示`UnitsInStock`值如果为零。 正如我们看到在前面的教程，GridView、 DetailsView 和 FormView 提供了两个截然不同的方法来格式化它们根据其数据的外观：

- **`DataBound`事件**创建的事件处理程序的相应`DataBound`触发后数据已绑定到每个项的事件 (它是 gridview`RowDataBound`事件; 对于 DataList 和 Repeater 中，它将是`ItemDataBound`事件)。 在这种情况可以进行检查，处理程序，只是数据绑定进行格式设置决定。 此方法中的，我们探讨[自定义格式设置基于数据的](../custom-formatting/custom-formatting-based-upon-data-cs.md)教程。
- **格式设置函数模板中的**DetailsView 或 GridView 控件中或在 FormView 控件模板中使用 Templatefield，我们可以将格式设置函数添加到 ASP.NET 页面 + s 代码隐藏类、 业务逻辑层，或任意可从 web 应用程序访问其他类库。 此格式设置函数可以接受任意数量的输入参数，但必须返回要在模板中呈现的 HTML。 格式设置函数已在中首先检查[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)教程。

使用 DataList 和 Repeater 控件提供这两种格式设置的技巧。 在本教程中我们将逐步了解有关这两个控件使用这两种技术的示例。

## <a name="using-theitemdataboundevent-handler"></a>使用`ItemDataBound`事件处理程序

当数据绑定到 DataList 和从数据源控件或通过以编程方式将数据分配给控件 s`DataSource`属性并调用其`DataBind()`方法，DataList 的`DataBinding`触发事件时，枚举，该数据源而每个数据记录绑定到 DataList。 对于数据源中每个记录，请创建 DataList [ `DataListItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx)对象，该对象然后绑定到当前记录。 在此过程中，DataList 引发两个事件：

- **`ItemCreated`** 之后才激发`DataListItem`已创建
- **`ItemDataBound`** 已绑定到当前记录后触发 `DataListItem`

以下步骤概述 DataList 控件数据绑定过程。

1. DataList s [ `DataBinding`事件](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx)激发
2. 数据绑定到 DataList  
  
   为数据源中的每个记录 

    1. 创建`DataListItem`对象
    2. 激发[`ItemCreated`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. 将绑定到的记录 `DataListItem`
    4. 激发[`ItemDataBound`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. 添加`DataListItem`到`Items`集合

当数据绑定到 Repeater 控件，它进一步完成完全相同的步骤序列。 唯一的区别是，而不是`DataListItem`正在创建的实例，使用 Repeater [ `RepeaterItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s。

> [!NOTE]
> 敏锐的读者可能已经注意到的暴露 DataList 和 Repeater 绑定到数据与 GridView 绑定到数据时的步骤顺序之间稍有异常。 在数据绑定过程的结尾结束时，引发 GridView`DataBound`事件; 但是，DataList 和 Repeater 都不控件具有此类事件。 这是因为之前检测前和后级别事件处理程序模式已成为常见 DataList 和 Repeater 控件在 ASP.NET 1.x 的时间范围内，创建。


格式设置数据的基础之上的一个选项是创建的事件处理程序使用 GridView，正如`ItemDataBound`事件。 此事件处理程序会检查必须只绑定到的数据`DataListItem`或`RepeaterItem`和影响控件的格式，根据需要。

DataList 控件格式设置更改为可以使用实现整个项`DataListItem`s 与样式有关的属性，其中包括标准`Font`， `ForeColor`， `BackColor`， `CssClass`，依次类推。 若要影响 DataList 的模板中的特定 Web 控件的格式设置，我们需要以编程方式访问和修改这些 Web 控件的样式。 我们已了解如何完成此过去*自定义格式设置基于数据的*教程。 与 Repeater 控件`RepeaterItem`类具有不与样式有关的属性; 因此，所有与样式有关的更改`RepeaterItem`中`ItemDataBound`事件处理程序必须通过以编程方式访问和更新中的 Web 控件该模板。

由于`ItemDataBound`DataList 和 Repeater 的几乎完全相同，我们的示例将重点介绍使用 DataList 格式设置方法。

## <a name="step-1-displaying-product-information-in-the-datalist"></a>步骤 1： 在 DataList 中显示的产品信息

我们担心的格式设置之前，让 s 首次创建使用 DataList 来显示产品信息页。 在中[前一篇教程](displaying-data-with-the-datalist-and-repeater-controls-cs.md)我们创建了 DataList 其`ItemTemplate`显示每个产品的名称、 类别、 供应商、 每个计价单位和价格的数量。 允许在本教程中重复此功能下面的 s。 若要实现此目的，你也可以重新创建 DataList 和从零开始，其对象数据源或可以复制这些控件从上一教程中创建的页 (`Basics.aspx`) 和本教程中将其粘贴到页面 (`Formatting.aspx`)。

一旦已复制的 DataList 和 ObjectDataSource 的功能，从`Basics.aspx`到`Formatting.aspx`，请花费片刻时间更改 DataList s`ID`属性从`DataList1`到更具描述性`ItemDataBoundFormattingExample`。 接下来，在浏览器中查看 DataList。 如图 1 所示，每个产品之间的唯一格式设置区别是，交替的背景色。


[![DataList 控件中列出的产品](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image1.png)

**图 1**: DataList 控件中列出了产品 ([单击以查看实际尺寸的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image3.png))


对于本教程，让我们来设置 DataList 格式，使其小于 20.00 美元的价格的任何产品将具有两个其名称和单位价格黄色突出显示。

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>步骤 2： 以编程方式确定 ItemDataBound 事件处理程序中的数据的值

由于仅这些下 20.00 美元将价格的产品有应用的自定义格式，我们必须能够确定每个产品的价格。 当数据绑定到 DataList，DataList 枚举其数据源中的记录和，对于每个记录创建`DataListItem`实例，绑定到数据源记录`DataListItem`。 在特定记录 s 后数据已绑定到当前`DataListItem`对象，DataList 的`ItemDataBound`触发事件。 我们可以创建此事件来检查当前的数据值的事件处理程序`DataListItem`并根据这些值，进行必要的格式设置更改。

创建`ItemDataBound`DataList 的事件，并添加以下代码：


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample1.cs)]

尽管概念和 DataList s 背后的语义`ItemDataBound`事件处理程序将与所使用的 GridView s 相同`RowDataBound`中的事件处理程序*自定义格式设置基于数据的*教程中，语法不同稍有。 当`ItemDataBound`事件触发时，`DataListItem`只需绑定到数据传递到相应事件处理程序通过`e.Item`(而不是`e.Row`，如同处理 GridView 的`RowDataBound`事件处理程序)。 DataList s`ItemDataBound`事件处理程序触发*每个*行添加到 DataList，包括标题行、 页脚行和行分隔符。 但是，产品信息仅绑定到的数据行中。 因此，当使用`ItemDataBound`事件来检查的数据绑定到 DataList，我们需要先确保我们重新处理的数据项。 这可以通过检查来实现`DataListItem`s [ `ItemType`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)，它可以具有之一[以下 8 个值](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx):

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

这两`Item`和`AlternatingItem``DataListItem`的组成的 DataList s 数据项。 假定我们使用重新`Item`或`AlternatingItem`，我们访问的实际`ProductsRow`绑定到当前实例`DataListItem`。 `DataListItem` S [ `DataItem`属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx)包含对引用`DataRowView`对象，其`Row`属性提供对实际引用`ProductsRow`对象。

接下来，我们检查`ProductsRow`实例的`UnitPrice`属性。 由于 Products 表 s`UnitPrice`字段允许`NULL`值，然后再尝试访问`UnitPrice`属性我们应首先检查以查看其是否具有`NULL`值使用`IsUnitPriceNull()`方法。 如果`UnitPrice`的值不是`NULL`，然后，我们检查以查看是否它 s 小于 20.00 美元。 如果它确实下是 20.00 美元，我们则需要应用自定义格式设置。

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>步骤 3： 突出显示产品名称和价格

一旦我们知道产品的价格为小于 20.00 美元，所有的就是以突出显示其名称和价格。 若要实现此目的，我们必须先以编程方式引用中的标签控件`ItemTemplate`用于显示产品的名称和价格。 接下来，我们需要让其显示黄色背景。 可以通过直接修改标签来应用此格式设置信息`BackColor`属性 (`LabelID.BackColor = Color.Yellow`); 理想情况下，显示相关的所有相关问题，应将其表示通过级联样式表。 事实上，我们已提供所需的格式中定义的样式表`Styles.css`  -  `AffordablePriceEmphasis`，已创建并中所述*自定义格式设置基于数据的*教程。

若要应用的格式设置，只需设置两个标签 Web 控件`CssClass`属性设置为`AffordablePriceEmphasis`，如下面的代码中所示：


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample2.cs)]

与`ItemDataBound`事件处理程序完成后，重新访问`Formatting.aspx`页在浏览器中。 如图 2 所示，在下，20.00 美元的价格与这些产品具有其名称和突出显示的价格。


[![这些产品小于 20.00 美元突出显示](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image4.png)

**图 2**： 将突出显示那些产品小于 20.00 美元 ([单击以查看实际尺寸的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image6.png))


> [!NOTE]
> 由于以 HTML 形式呈现 DataList `<table>`，将其`DataListItem`实例具有与样式有关的属性，可设置为特定样式应用于整个项目。 例如，如果我们想要强调*整个*时其价格小于 20.00 美元项黄色，我们可能已经替换引用的标签的代码并设置其`CssClass`属性使用以下代码行： `e.Item.CssClass = "AffordablePriceEmphasis"`（请参见图 3）。


`RepeaterItem`构成了 Repeater 控件中，但是，don t s 提供此类样式级别的属性。 图 2 中一样，应用自定义格式设置为 Repeater 需要因此，应用到 Repeater 的模板中的 Web 控件的样式属性。


[![整个产品项突出显示的产品下 20.00 美元](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image7.png)

**图 3**: 整个产品项突出显示的产品下 20.00 美元 ([单击以查看实际尺寸的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image9.png))


## <a name="using-formatting-functions-from-within-the-template"></a>使用从模板中的格式设置函数

在中*GridView 控件中使用 Templatefield*教程中我们已了解如何使用 GridView TemplateField 内的某个格式设置函数来应用自定义格式取决于的数据绑定到 GridView 的行。 格式设置函数是一个方法，可以从模板调用并返回要在其原位置发出的 HTML。 格式设置函数可以驻留在 ASP.NET 页面 + s 代码隐藏类或到类文件可以集中式`App_Code`文件夹或在单独的类库项目。 移动从 ASP.NET 页的代码隐藏类的格式设置函数是理想选择，如果你计划在多个 ASP.NET 页或其他 ASP.NET web 应用程序中使用相同的格式设置函数。

若要演示格式设置函数，让 s 具有产品信息包括产品的名称旁边的文本 [DISCONTINUED]，如果它停止使用的 s。 此外，let s 具有价格突出显示黄色如果它 s 小于 20.00 美元 (正如我们做`ItemDataBound`事件处理程序示例); 如果价格为 $20.00 或更高版本，可让 s 不会显示实际的价格，但文本，请改为调用针对一个价格的报价。 图 4 显示了应用这些格式设置规则与列出的产品的屏幕截图。


[![对于昂贵的产品，价格将被替换为文本，请调用的报价单](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image10.png)

**图 4**： 对于昂贵的产品，价格将被替换的文本，请调用价格 quote ([单击以查看实际尺寸的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image12.png))


## <a name="step-1-create-the-formatting-functions"></a>步骤 1： 创建格式设置函数

我们需要两个格式设置函数，一个必要时，将显示产品名称以及文本 [DISCONTINUED]，另一个此示例中显示突出显示的价格，如果它小于 $20.00，还是文本，请调用的报价单否则为 s。 让我们来创建这些函数中的 ASP.NET 页面 + s 代码隐藏类并将它们命名`DisplayProductNameAndDiscontinuedStatus`和`DisplayPrice`。 这两种方法需要返回 HTML 字符串形式呈现和两者都需要标记`Protected`(或`Public`) 以便从 ASP.NET 页 s 声明性语法部分调用。 这两种方法的代码如下所示：


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample3.cs)]

请注意，`DisplayProductNameAndDiscontinuedStatus`方法接受的值`productName`并`discontinued`数据字段为标量值，而`DisplayPrice`方法接受`ProductsRow`实例 (而非`unitPrice`标量值)。 将使用以下两种方法; 如果但是，如果将格式设置函数使用可以包含数据库的标量值`NULL`值 (如`UnitPrice`; 都不`ProductName`也不`Discontinued`允许`NULL`值)，特殊必须谨慎地处理这些标量输入。

具体而言，输入的参数必须属于类型`Object`传入的值可能是由于`DBNull`而不是预期的数据类型的实例。 此外，必须进行检查以确定传入的值是否为数据库`NULL`值。 也就是说，如果我们想`DisplayPrice`方法以接受价格为标量值，d 我们必须使用以下代码：


[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample4.cs)]

请注意，`unitPrice`输入的参数的类型是`Object`和已修改的条件语句以确定如果`unitPrice`是`DBNull`与否。 此外，由于`unitPrice`输入的参数传入作为`Object`，必须将它转换为十进制值。

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>步骤 2： 从 DataList 的 ItemTemplate 调用格式设置函数

添加到我们的 ASP.NET 页面 + s 代码隐藏类的格式设置函数，剩下的就是调用这些格式设置函数从 DataList 的`ItemTemplate`。 若要从模板调用格式设置函数，将函数调用中的数据绑定语法：


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample5.aspx)]

在 DataList s `ItemTemplate` `ProductNameLabel`标签 Web 控件当前显示的产品的名称通过分配其`Text`属性结果的`<%# Eval("ProductName") %>`。 若要使其显示名称和文本 [DISCONTINUED]，如果需要更新的声明性语法，以便它改为将分配`Text`属性值的`DisplayProductNameAndDiscontinuedStatus`方法。 这样做时，我们必须通过中的产品的名称和已停止使用的值使用`Eval("columnName")`语法。 `Eval` 返回类型的值`Object`，但`DisplayProductNameAndDiscontinuedStatus`方法需要输入的参数的类型`String`并`Boolean`; 因此，我们必须将返回的值强制转换`Eval`到预期的输入的参数类型，方法如下所示：


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample6.aspx)]

若要显示的价格，我们只是可以设置`UnitPriceLabel`标签 s`Text`属性设置为返回的值`DisplayPrice`方法，就像我们做用于显示产品的名称，然后 [停用] 文本。 但是，而不是传入`UnitPrice`作为标量输入参数，我们改为传入整个`ProductsRow`实例：


[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample7.aspx)]

使用就地格式设置函数的调用，请花费片刻时间浏览器中查看我们的进度。 屏幕应类似于图 5 中，已停止使用的产品包括文本 [DISCONTINUED]，这些产品成本超过 $20.00 具有其价格替换文本请的报价单的调用。


[![对于昂贵的产品，价格将被替换为文本，请调用的报价单](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image13.png)

**图 5**： 对于昂贵的产品，价格将被替换的文本，请调用价格 quote ([单击以查看实际尺寸的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image15.png))


## <a name="summary"></a>总结

可以使用两种技术完成基于数据的 DataList 或 Repeater 控件的内容设置格式。 第一种方法是创建的事件处理程序`ItemDataBound`触发的事件，因为每个记录中的数据源绑定到一个新`DataListItem`或`RepeaterItem`。 在中`ItemDataBound`事件处理程序，可以检查当前的 s 项数据，然后格式设置可以应用于内容的模板，或为`DataListItem`s，对整个项目本身。

或者，通过格式设置函数中实现自定义格式设置。 格式设置函数是方法可以通过 DataList 或 Repeater 的模板返回 HTML 以在其原位置发出的。 通常情况下，由绑定到当前项的值确定格式设置函数返回的 HTML。 为标量值或绑定到项的整个对象中传递这些值可以传递到格式设置函数 (如`ProductsRow`实例)。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Yaakov Ellis、 Randy Schmidt 和 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-data-with-the-datalist-and-repeater-controls-cs.md)
> [下一页](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
