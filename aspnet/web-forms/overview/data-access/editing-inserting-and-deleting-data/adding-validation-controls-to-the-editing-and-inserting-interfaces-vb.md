---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: 添加验证控件向编辑和插入界面 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将看到验证控件添加到 EditItemTemplate 和 InsertItemTemplate 数据 Web 控件，以便提供更是多么...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: a2fc00426022513c6e2adc49b0df30f943403302
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366224"
---
<a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>添加验证控件向编辑和插入界面 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe)或[下载 PDF](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> 在本教程中我们将看到 EditItemTemplate 和 InsertItemTemplate 数据 Web 控件，以提供更能做到万无一失的用户界面添加验证控件是多么容易。


## <a name="introduction"></a>介绍

在示例中的 GridView 和 DetailsView 控件我们已经探讨了三个教程具有所有已 BoundFields 和组成 CheckBoxFields （字段类型绑定到数据源的 GridView 或 DetailsView 时由 Visual Studio 会自动添加在过去控制通过智能标记）。 在编辑 GridView 或 DetailsView 中的行时，不是只读的这些 BoundFields 转换为文本框中，从该最终用户可以修改现有数据。 同样，当插入一个新记录到 DetailsView 控件，这些 BoundFields`InsertVisible`属性设置为`True`（默认值） 将呈现为空文本框中，用户可以在其中提供新记录的字段值。 同样，CheckBoxFields，将禁用标准的、 只读的界面中，将转换为的编辑和插入界面中的已启用复选框。

尽管默认编辑和插入界面 BoundField 和 CheckBoxField 可能很有帮助，接口中没有任何类型的验证。 如果用户是犯了数据条目-例如省略`ProductName`字段或输入的值无效`UnitsInStock`（如-50) 将引发异常从应用程序体系结构的深度中。 虽然此异常可以正常处理中所示[前一篇教程](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)，理想情况下编辑或插入用户界面将包括验证控制，以防止用户输入此类中的无效数据第一个位置。

为了提供自定义的编辑或插入的接口，我们需要使用 TemplateField 替换 BoundField 或 CheckBoxField。 Templatefield，所讨论的主题中[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)并[DetailsView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md)教程中，可以包含多个定义的模板将不同的行状态的接口。 TemplateField`ItemTemplate`而是用于呈现只读字段或 DetailsView 或 GridView 控件中的行时`EditItemTemplate`和`InsertItemTemplate`指示要用于编辑和插入模式下，分别使用的接口。

在本教程中我们将看到添加到 templatefield 进一步的验证控件是多么`EditItemTemplate`和`InsertItemTemplate`以提供更能做到万无一失的用户界面。 具体而言，本教程会引导创建中的示例[检查与插入、 更新和删除的事件相关联](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)教程和增强的编辑和插入界面，可包括适当的验证。

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-vbmd"></a>步骤 1： 复制中的示例[与插入、 更新和删除检查有关的事件相关联](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)

在中[检查与插入、 更新和删除的事件相关联](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)教程中，我们创建所列的名称和价格的可编辑的 GridView 中的产品页。 此外，页面包含 DetailsView 其`DefaultMode`属性设置为`Insert`，从而始终呈现在插入模式下。 此 DetailsView，从用户无法输入一个新的产品的名称和价格，单击插入，并将其添加到系统 （请参阅图 1）。


[![前面的示例，用户可以添加新产品并编辑现有的](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**图 1**: 上一示例允许用户添加的新产品和编辑现有的 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png))


对于本教程旨在扩充提供验证控件的 DetailsView 和 GridView。 具体而言，我们验证逻辑将：

- 要求在插入或编辑产品时提供的名称
- 要求插入一条记录; 时提供的价格当编辑记录，我们仍需要价格，但编程逻辑将在 GridView 的`RowUpdating`从前面的教程中已存在的事件处理程序
- 请确保输入的价格的值是一种有效的货币格式

我们可以看看扩充一示例，包括验证之前，我们首先需要复制中的示例`DataModificationEvents.aspx`到本教程中的页的页`UIValidation.aspx`。 若要完成此我们需要通过同时复制`DataModificationEvents.aspx`页面的声明性标记和其源代码。 将复制的声明性标记，请执行以下步骤：

1. 打开`DataModificationEvents.aspx`Visual Studio 中的页
2. 请转到页面的声明性标记 （在页面底部的源按钮单击）
3. 复制中的文本`<asp:Content>`和`</asp:Content>`标记 （3 至 44 行），图 2 中所示。


[![复制文本内&lt;asp: Content&gt;控件](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**图 2**： 复制文本内`<asp:Content>`控件 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png))


1. 打开`UIValidation.aspx`页
2. 请转到页面的声明性标记
3. 中的文本将粘贴`<asp:Content>`控件。

若要复制的源代码，请打开`DataModificationEvents.aspx.vb`页上，并将复制只是文本*内*`EditInsertDelete_DataModificationEvents`类。 将复制的三个事件处理程序 (`Page_Load`， `GridView1_RowUpdating`，并`ObjectDataSource1_Inserting`)，但不要**不**复制类声明。 粘贴复制的文本*内*`EditInsertDelete_UIValidation`类中`UIValidation.aspx.vb`。

移动的内容和从代码转移后`DataModificationEvents.aspx`到`UIValidation.aspx`，花点时间来测试您的浏览器中的进度。 你应看到相同输出和体验每个这些两个页中相同的功能 (回头查看图 1 的屏幕截图的`DataModificationEvents.aspx`操作中)。

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>步骤 2： 将 BoundFields 转换为 Templatefield

要向编辑和插入界面添加验证控件，需要将转换为 Templatefield BoundFields DetailsView 和 GridView 控件使用。 若要实现此目的，单击编辑列和编辑字段中链接的 GridView 和 DetailsView 的智能标记，分别。 选择每个 BoundFields 并单击"将此字段转换为 TemplateField"链接。


[![每个 DetailsView 的和 GridView 的 BoundFields 转换为 Templatefield](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**图 3**： 将每个 DetailsView 的和 GridView 的 BoundFields 到 Templatefield 转换 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png))


BoundField 转换为 TemplateField 字段对话框通过生成 TemplateField 表现出作为 BoundField 本身相同的只读、 编辑以及插入接口。 以下标记显示的声明性语法`ProductName`字段中 DetailsView 转换转换为 TemplateField 后：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

请注意此 TemplateField 有三个模板自动创建`ItemTemplate`， `EditItemTemplate`，和`InsertItemTemplate`。 `ItemTemplate`显示单个数据字段值 (`ProductName`) 使用标签 Web 控件，而`EditItemTemplate`并`InsertItemTemplate`将数据字段与文本框的相关联的文本框中 Web 控件中显示数据字段值`Text`使用双向数据绑定的属性。 由于我们只用于插入，在此页中使用 DetailsView，可能会删除`ItemTemplate`和`EditItemTemplate`从两个 Templatefield，尽管它们保留没有什么坏处。

因为 GridView 不支持内置插入的 DetailsView 功能、 转换 GridView`ProductName`仅在结果字段转换为 TemplateField`ItemTemplate`和`EditItemTemplate`:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

通过单击"转换此字段转换为 TemplateField"，Visual Studio 创建的模板模拟的用户界面的已转换 BoundField TemplateField。 可以通过访问此页上的通过浏览器对此进行验证。 您会发现的外观和行为的 Templatefield 是相同的体验 BoundFields 改为使用时。

> [!NOTE]
> 随意自定义中的模板，根据需要编辑的接口。 例如，我们可能想要在文本框中`UnitPrice`Templatefield 呈现为较小文本框比`ProductName`文本框中。 若要完成此操作可以设置文本框的`Columns`属性设置为适当的值或提供通过的绝对宽度`Width`属性。 在下一教程中我们将了解如何通过 Web 控件的备用数据条目替换文本框中编辑界面完全自定义。


## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>步骤 3： 将验证控件添加到 GridView 的`EditItemTemplate`s

在构造时数据输入窗体，务必用户输入所有必填的字段和所有提供的输入是合法的格式正确的值。 若要帮助确保用户的输入有效，ASP.NET 提供了五个内置的验证控件旨在用于验证的输入控件的值：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)可确保已提供一个值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)验证值与另一个 Web 控件值或常量的值，或确保值的格式是合法的指定的数据类型
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可确保一个值，值范围内
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)来验证针对值[正则表达式](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)验证值与自定义、 用户定义方法

有关这些五个控件的详细信息，请参阅[验证控件部分](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx)的[ASP.NET 快速入门教程](https://asp.net/QuickStart/aspnet/)。

本教程中，我们将需要使用在 DetailsView 和 GridView 的 RequiredFieldValidator `ProductName` Templatefield 和 DetailsView 中的 RequiredFieldValidator `UnitPrice` TemplateField。 此外，我们将需要为这两个控件的添加 CompareValidator `UnitPrice` Templatefield，以确保输入的价格的值大于或等于 0，并以一种有效的货币格式表示。

> [!NOTE]
> 尽管 ASP.NET 1.x 有这些相同的五个验证控件、 ASP.NET 2.0 增添了大量改进、 主两人是客户端侧脚本支持 Internet Explorer 以外的浏览器和分区到页面上的验证控件的功能验证组。 有关 2.0 中新的验证控件功能的详细信息，请参阅[仔细分析 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。


让我们首先，通过添加必要的验证控件到`EditItemTemplate`GridView 的 Templatefield。 若要完成此操作，单击 GridView 的智能标记，以显示模板编辑界面中的编辑模板链接。 在这里，可以选择要从下拉列表中编辑的模板。 由于我们想要增强的编辑界面，因此我们需要验证将控件添加到`ProductName`并`UnitPrice`的`EditItemTemplate`s。


[![我们需要将产品名称和单价的 EditItemTemplates 扩展](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**图 4**： 我们需要扩展`ProductName`并`UnitPrice`的`EditItemTemplate`s ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png))


在中`ProductName` `EditItemTemplate`，通过从工具箱拖动到模板编辑界面中，添加一个 RequiredFieldValidator 放置后文本框中。


[![将一个 RequiredFieldValidator 添加到产品名称 EditItemTemplate](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**图 5**： 添加到一个 RequiredFieldValidator `ProductName` `EditItemTemplate` ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png))


通过验证单个 ASP.NET Web 控件的输入处理的所有验证控件。 因此，我们需要指出我们刚添加的 RequiredFieldValidator 应验证中文本框`EditItemTemplate`; 这通过设置验证控件的实现[ControlToValidate 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)到`ID`适当的 Web 控件。 文本框中当前具有而不是无明显特征`ID`的`TextBox1`，但让我们将它更改为更合适。 单击该模板中的文本框，然后，从属性窗口中，更改`ID`从`TextBox1`到`EditProductName`。


[![将文本框的 ID 更改为 EditProductName](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**图 6**： 更改文本框的`ID`到`EditProductName`([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png))


接下来，设置 RequiredFieldValidator`ControlToValidate`属性设置为`EditProductName`。 最后，设置[ErrorMessage 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)到"必须提供产品的名称"和[Text 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)到"\*"。 `Text`属性值，如果提供，则如果验证失败的验证控件显示的文本。 `ErrorMessage`属性值，该值是必需的由 ValidationSummary 控件; 如果`Text`省略属性值，则`ErrorMessage`属性值也是无效的输入上的验证控件显示的文本。

在设置后 RequiredFieldValidator 这三个属性，您的屏幕应类似于图 7。


[![设置 RequiredFieldValidator 的 ControlToValidate、 错误消息和文本属性](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**图 7**： 设置 RequiredFieldValidator `ControlToValidate`， `ErrorMessage`，和`Text`属性 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png))


使用添加到 RequiredFieldValidator `ProductName` `EditItemTemplate`，则所有剩下是添加到需要验证`UnitPrice` `EditItemTemplate`。 由于我们已决定的此页上，为`UnitPrice`可选时，编辑记录，我们无需添加一个 RequiredFieldValidator。 我们执行操作，但是，需要添加 CompareValidator，确保`UnitPrice`，如果提供，作为一种货币格式正确，大于或等于 0。

我们将添加到 CompareValidator 之前`UnitPrice` `EditItemTemplate`，让我们首先将更改从 TextBox Web 控件的 ID`TextBox2`到`EditUnitPrice`。 此更改后，添加 CompareValidator，设置其`ControlToValidate`属性设置为`EditUnitPrice`，将其`ErrorMessage`属性设置为"价格必须大于或等于零，并且不能包含货币符号"并将其`Text`属性"\*".

若要指示`UnitPrice`值必须是大于或等于 0，设置 CompareValidator[运算符属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)到`GreaterThanEqual`，将其[ValueToCompare 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)为"0"，并其[类型属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)到`Currency`。 下面的声明性语法演示`UnitPrice`TemplateField 的`EditItemTemplate`在进行这些更改后：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

进行这些更改后，在浏览器中打开的网页。 如果尝试省略名称或编辑产品时输入无效的价格值文本框旁边将出现一个星号。 如图 8 所示，包含货币符号，例如 19.95 美元的价格值将被视为无效。 CompareValidator `Currency` `Type`允许数字分隔符 （如逗号或句点，具体取决于的区域性设置） 和前导加号或减号，但不*不*允许货币符号。 此行为可能 perplex 用户编辑界面当前呈现`UnitPrice`使用货币格式。

> [!NOTE]
> 回想一下，在*与插入、 更新和删除事件相关联*教程中，我们将设置 BoundField`DataFormatString`属性设置为`{0:c}`才能设置其格式为货币。 此外，我们将设置`ApplyFormatInEditMode`属性设为 true，从而导致 GridView 的编辑界面要设置格式`UnitPrice`作为一种货币。 Visual Studio 将 BoundField 转换为 TemplateField，记下这些设置和格式的文本框`Text`属性设置为使用数据绑定语法货币`<%# Bind("UnitPrice", "{0:c}") %>`。


[![使用无效的输入文本框旁边会显示一个星号](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**图 8**: 星号显示下一步使用无效的输入文本框 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png))


尽管验证可充当的是，用户必须手动编辑一个记录，这不是可接受时删除的货币符号。 若要解决此问题，我们有三个选项：

1. 配置`EditItemTemplate`，以便`UnitPrice`值未格式化为货币。
2. 允许用户通过删除 CompareValidator 并将它替换为正确的格式正确的货币值检查 RegularExpressionValidator 输入货币符号。 此处的问题是，要验证的货币值的正则表达式不是漂亮，需要编写代码如果我们想要合并的区域性设置。
3. 完全删除的验证控件和 GridView 中的服务器端验证逻辑依赖于`RowUpdating`事件处理程序。

让我们使用选项 #1 对于此练习。 目前`UnitPrice`格式化为货币的文本框中的数据绑定表达式由于`EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`。 绑定将语句更改为`Bind("UnitPrice", "{0:n2}")`，其中将结果格式化为带两位数字的精度的数字。 这可以通过声明性语法直接或通过单击从编辑 DataBindings 链接`EditUnitPrice`文本框中的`UnitPrice`TemplateField 的`EditItemTemplate`（请参阅图 9 和 10）。


[![单击文本框的编辑 DataBindings 链接](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**图 9**： 单击文本框的编辑 DataBindings 链接 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png))


[![在绑定语句中指定的格式说明符](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**图 10**： 指定在格式说明符`Bind`语句 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png))


进行此更改后，编辑界面中的格式化的价格包含组分隔符为逗号和句点作为小数分隔符，但哪儿货币符号。

> [!NOTE]
> `UnitPrice` `EditItemTemplate`不包括允许会随之发生回发和更新的逻辑，开始一个 RequiredFieldValidator。 但是，`RowUpdating`事件处理程序从复制*检查与插入、 更新和删除的事件相关联*教程包括可确保以编程方式检查`UnitPrice`提供。 随意删除此逻辑，请将其作为保留的或添加到一个 RequiredFieldValidator `UnitPrice` `EditItemTemplate`。


## <a name="step-4-summarizing-data-entry-problems"></a>步骤 4： 汇总数据输入问题

ASP.NET 包括五个验证控件中，除了[ValidationSummary 控件](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，其中显示`ErrorMessage`s 检测到无效数据这些验证控件。 此摘要数据可以显示为文本在网页上或通过模式、 客户端的消息框。 让我们来改进此教程，包括汇总的任何验证问题的客户端的 messagebox。

若要实现此目的，请从工具箱拖到设计器拖动 ValidationSummary 控件。 验证控件的位置无关紧要，因为我们要将其配置为仅显示为一个消息框的摘要。 添加控件之后, 设置其[ShowSummary 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)到`False`并将其[ShowMessageBox 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)到`True`。 添加此元素后，客户端的 messagebox 中总结了任何验证错误。


[![客户端的 Messagebox 中总结了验证错误](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**图 11**： 客户端的 Messagebox 中总结了验证错误 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png))


## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>步骤 5： 向 DetailsView 添加验证控件`InsertItemTemplate`

所有的本教程中的就是向 DetailsView 插入界面添加验证控件。 向 DetailsView 的模板添加验证控件的过程等同于检查在步骤 3; 的因此，我们将轻松处理通过此步骤中的任务。 正如我们做 gridview `EditItemTemplate` s，我建议您重命名`ID`s 从无明显特征文本框`TextBox1`和`TextBox2`到`InsertProductName`和`InsertUnitPrice`。

添加到一个 RequiredFieldValidator `ProductName` `InsertItemTemplate`。 设置`ControlToValidate`到`ID`在模板中，文本框的其`Text`属性设置为"\*"并将其`ErrorMessage`属性设置为"您必须提供产品的名称"。

由于`UnitPrice`是添加新记录时，所需的此页，添加到一个 RequiredFieldValidator `UnitPrice` `InsertItemTemplate`，并设置其`ControlToValidate`， `Text`，和`ErrorMessage`属性正确。 最后，添加到 CompareValidator `UnitPrice` `InsertItemTemplate`以及配置其`ControlToValidate`， `Text`， `ErrorMessage`， `Type`， `Operator`，和`ValueToCompare`属性就像我们一样`UnitPrice`的 GridView 中的 CompareValidator `EditItemTemplate`。

添加这些验证控件之后, 不能添加到系统中，如果未提供其名称或它的价格是负数或非法格式化新产品。


[![验证逻辑已添加到 DetailsView 插入接口](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**图 12**： 验证逻辑已添加到 DetailsView 插入接口 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png))


## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>步骤 6： 分区到验证组的验证控件

我们的页面包含验证控件的两个逻辑上不同的集： 这些对应于 GridView 的编辑界面和那些与 DetailsView 相对应的插入接口。 默认情况下，为在回发发生时*所有*检查页上的验证控件。 但是，编辑记录时我们不希望 DetailsView 插入接口的验证控件验证。 图 13 说明了我们当前的难题，当用户编辑与完全合法值的产品，单击更新将导致验证错误，因为插入接口中的名称和价格值为空。


[![正在更新产品用于引发导致插入接口的验证控件](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**图 13**： 更新产品用于引发导致插入接口的验证控件 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png))


ASP.NET 2.0 中的验证控件可以分区为验证组通过其`ValidationGroup`属性。 若要将组中的验证控件的一组相关联，只需设置其`ValidationGroup`属性设置为相同的值。 对于本教程中，设置`ValidationGroup`GridView 的 Templatefield 到中的验证控件的属性`EditValidationControls`并`ValidationGroup`到 DetailsView Templatefield 属性`InsertValidationControls`。 这些更改可以在声明性标记中直接或通过属性窗口时使用设计器的编辑模板界面。

除了验证控件、 按钮和按钮相关控件在 ASP.NET 2.0 中的还包含`ValidationGroup`属性。 验证组的验证程序检查的有效性仅为在回发引起的具有相同的按钮`ValidationGroup`属性设置。 例如，为了使 DetailsView 的插入按钮来触发`InsertValidationControls`验证组我们需要设置 CommandField`ValidationGroup`属性设置为`InsertValidationControls`（请参阅图 14）。 此外，设置 GridView 的 CommandField 的`ValidationGroup`属性设置为`EditValidationControls`。


[![集 DetailsView 的 InsertValidationControls CommandField 的 ValidationGroup 属性](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**图 14**： 设置 DetailsView CommandField 的`ValidationGroup`属性设置为`InsertValidationControls`([单击以查看实际尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png))


更改后，DetailsView 和 GridView 的 Templatefield 和命令应类似于下面：

DetailsView Templatefield 和 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView CommandField 和 Templatefield

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

现在编辑特定的验证控件激发仅在单击 GridView 的更新按钮时和特定于插入的验证控件即发即仅当单击 DetailsView 的插入按钮时，解决图 13 的突出显示了此问题时。 但是，进行此更改后我们 ValidationSummary 控件不再显示在输入无效数据时。 ValidationSummary 控件还包含`ValidationGroup`属性并仅显示这些验证控件在其验证组的摘要信息。 因此，我们需要在此页中，一个用于具有两个验证控件`InsertValidationControls`验证组，另一个用于`EditValidationControls`。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

添加此元素在本教程中已完成 ！

## <a name="summary"></a>总结

虽然 BoundFields 可以提供同时插入和编辑接口，该接口不是可自定义的。 通常情况下，我们想要将验证控件添加到的编辑和插入界面以确保用户在法律格式输入所需的输入。 若要实现此目的我们必须 BoundFields 转换为 Templatefield 并将验证控件添加到合适的模板。 在本教程中我们扩展中的示例*检查与插入、 更新和删除的事件相关联*教程中，为这两个 DetailsView 添加验证控件的插入接口和 GridView编辑界面。 此外，我们了解了如何显示验证摘要信息使用 ValidationSummary 控件以及如何进行分区的页上的验证控件为不同的验证组。

正如我们看到在本教程中，Templatefield 允许进行扩充以包括验证控件的编辑和插入的接口。 Templatefield 还可以扩展以包括其他输入的 Web 控件，使文本框将替换为更适合的 Web 控件。 在我们的下一个教程将介绍如何使用数据绑定 DropDownList 控件，这是很理想，编辑外键时替换 TextBox 控件 (如`CategoryID`或`SupplierID`中`Products`表)。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Liz Shulok 和 Zack Jones。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [下一页](customizing-the-data-modification-interface-vb.md)
