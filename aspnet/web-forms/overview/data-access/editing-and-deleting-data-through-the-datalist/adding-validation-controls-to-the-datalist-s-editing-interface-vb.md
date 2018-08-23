---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
title: 将验证控件添加到 DataList 的编辑界面 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何轻松将验证控件添加到 DataList 的 EditItemTemplate，以提供更能做到万无一失编辑用户 int。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 6b073fc6-524d-453d-be7c-0c30986de391
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 6fe5fcba322f3d3a37b862f0a85810d8b4dda5f4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824245"
---
<a name="adding-validation-controls-to-the-datalists-editing-interface-vb"></a>向 DataList 的编辑界面 (VB) 中添加验证控件
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_VB.exe)或[下载 PDF](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/datatutorial39vb1.pdf)

> 在本教程中我们将看到将验证控件添加到 DataList 的 EditItemTemplate，以提供更能做到万无一失编辑的用户界面是多么容易。


## <a name="introduction"></a>介绍

DataList 编辑教程到目前为止，在编辑接口 DataLists 具有不包含任何主动用户输入的验证，即使无效的用户输入如缺少的产品名称或负的价格会引发异常。 在中[前面的教程](handling-bll-and-dal-level-exceptions-vb.md)介绍了如何添加异常处理代码，DataList 的`UpdateCommand`事件处理程序以捕获并适当地显示有关已引发任何异常的信息。 但是，理想情况下，编辑界面将包括验证控件，以阻止用户从第一个位置中输入此类无效数据。

在本教程中我们将看到验证控件添加到 DataList s 是多么`EditItemTemplate`为了提供更能做到万无一失编辑的用户界面。 具体而言，本教程采用前面教程中创建的示例，并补充了编辑界面包括适当的验证。

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-vbmd"></a>步骤 1： 复制中的示例[处理 BLL 和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-vb.md)

在中[处理 BLL-和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-vb.md)教程中，我们创建所列的名称和两个列中，可编辑 DataList 中的产品价格的页面。 对于本教程旨在扩充 DataList s 编辑界面，包括验证控件。 具体而言，我们验证逻辑将：

- 要求提供产品的名称
- 请确保输入的价格的值是一种有效的货币格式
- 确保输入的价格是大于或等于零，因为负的值`UnitPrice`值是非法的

我们可以看看扩充一示例，包括验证之前，我们首先需要复制中的示例`ErrorHandling.aspx`页中`EditDeleteDataList`用于本教程中，逐页文件夹`UIValidation.aspx`。 若要实现此，我们需要通过同时复制`ErrorHandling.aspx`页面 s 声明性标记和其源代码。 将复制的声明性标记，请执行以下步骤：

1. 打开`ErrorHandling.aspx`Visual Studio 中的页
2. 请转到页面 s 声明性标记 （在页面底部的源按钮单击）
3. 复制中的文本`<asp:Content>`和`</asp:Content>`标记 （行 3 到 32），作为图 1 所示。


[![复制文本内&lt;asp: Content&gt;控件](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image1.png)

**图 2**： 复制文本内`<asp:Content>`控件 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image3.png))


1. 打开`UIValidation.aspx`页
2. 请转到页面 s 声明性标记
3. 中的文本将粘贴`<asp:Content>`控件。

若要复制的源代码，请打开`ErrorHandling.aspx.vb`页上，并将复制只是文本*内*`EditDeleteDataList_ErrorHandling`类。 将复制的三个事件处理程序 (`Products_EditCommand`， `Products_CancelCommand`，并`Products_UpdateCommand`) 连同`DisplayExceptionDetails`方法，但**不**复制类声明或`using`语句。 粘贴复制的文本*内*`EditDeleteDataList_UIValidation`类中`UIValidation.aspx.vb`。

移动的内容和从代码转移后`ErrorHandling.aspx`到`UIValidation.aspx`，花点时间来测试在浏览器中的页。 你应看到相同的输出和体验每个 （请参见图 2） 这些两个页中相同的功能。


[![UIValidation.aspx 页模仿 ErrorHandling.aspx 中的功能](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image4.png)

**图 2**:`UIValidation.aspx`页上模拟中的功能`ErrorHandling.aspx`([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image6.png))


## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>步骤 2： 向 DataList 的 EditItemTemplate 添加验证控件

在构造时数据输入窗体，务必用户输入所有必填的字段和所有其提供的输入是合法的格式正确的值。 为了帮助确保用户的输入有效，ASP.NET 提供了五个内置的验证控件的设计来验证单个输入 Web 控件的值：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)可确保已提供一个值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)验证值与另一个 Web 控件值或常量的值，或确保值的格式是合法的指定的数据类型
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可确保一个值，值范围内
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)来验证针对值[正则表达式](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)验证值与自定义、 用户定义方法

有关这些五个控件的详细信息请参阅重新[向编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)教程或签出[验证控件部分](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx)的[ASP.NET 快速入门教程](https://quickstarts.asp.net)。

本教程中我们将需要使用一个 RequiredFieldValidator 以确保已提供的产品名称的值和 CompareValidator 以确保输入的价格的值大于或等于 0，并以有效的货币格式显示。

> [!NOTE]
> 尽管 ASP.NET 1.x 有这些相同的五个验证控件、 ASP.NET 2.0 增添了大量改进，两人是客户端脚本包括 Internet Explorer 的浏览器和分区到页面上的验证控件的功能支持的主要验证组。 有关 2.0 中新的验证控件功能的详细信息，请参阅[仔细分析 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。


让我们来首先将必要的验证控件添加到 DataList 的`EditItemTemplate`。 通过单击编辑模板链接通过 DataList s 智能标记，在设计器或通过声明性语法，可以执行此任务。 允许 s 步骤通过使用设计视图中的编辑模板选项的过程。 在选择要编辑 DataList s 之后`EditItemTemplate`，通过从工具箱拖动到模板编辑界面中，添加一个 RequiredFieldValidator 将其之后放置`ProductName`文本框中。


[![在产品名称文本框之后向 EditItemTemplate 添加一个 RequiredFieldValidator](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image7.png)

**图 3**： 添加到一个 RequiredFieldValidator `EditItemTemplate After` `ProductName`文本框中 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image9.png))


通过验证单个 ASP.NET Web 控件的输入处理的所有验证控件。 因此，我们需要指示应验证我们刚添加的 RequiredFieldValidator`ProductName`文本框中; 这是通过设置验证控件 s [ `ControlToValidate`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)到`ID`的相应的 Web 控件 (`ProductName`，在这种情况)。 接下来，设置[`ErrorMessage`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)必须为提供的产品的名称并[`Text`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)到\*。 `Text`属性值，如果提供，则如果验证失败的验证控件显示的文本。 `ErrorMessage`属性值，该值是必需的由 ValidationSummary 控件; 如果`Text`省略属性值，则`ErrorMessage`属性值显示由验证控件在输入无效。

以后设置 RequiredFieldValidator 这三个属性，您的屏幕看起来应类似于图 4。


[![设置 RequiredFieldValidator 的 ControlToValidate、 错误消息和文本属性](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image10.png)

**图 4**： 设置 RequiredFieldValidator s `ControlToValidate`， `ErrorMessage`，和`Text`属性 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image12.png))


使用添加到 RequiredFieldValidator `EditItemTemplate`，则所有剩下是有必要为添加验证产品的价格文本框中。 由于`UnitPrice`取决于您在编辑记录时，我们不需要添加一个 RequiredFieldValidator。 我们执行操作，但是，需要添加 CompareValidator，确保`UnitPrice`，如果提供，作为一种货币格式正确，大于或等于 0。

添加到 CompareValidator`EditItemTemplate`并设置其`ControlToValidate`属性设置为`UnitPrice`，将其`ErrorMessage`属性设置为价格必须大于或等于零，并且不能包括货币符号，并将其`Text`属性\*. 若要指示`UnitPrice`值必须是大于或等于 0，设置 CompareValidator s [ `Operator`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)到`GreaterThanEqual`，将其[`ValueToCompare`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)为 0，并其[`Type`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)到`Currency`。

之后添加以下两个验证控件，DataList 的`EditItemTemplate`s 声明性语法应看起来如下所示：


[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

进行这些更改后，在浏览器中打开的网页。 如果尝试省略名称或编辑产品时输入无效的价格值文本框旁边将出现一个星号。 如图 5 所示，包含货币符号，例如 19.95 美元的价格值将被视为无效。 CompareValidator s `Currency` `Type`允许数字分隔符 （如逗号或句点，具体取决于的区域性设置） 和前导加号或减号，但不*不*允许货币符号。 此行为可能 perplex 用户编辑界面当前呈现`UnitPrice`使用货币格式。


[![使用无效的输入文本框旁边会显示一个星号](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image13.png)

**图 5**: 星号显示下一步使用无效的输入文本框 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image15.png))


尽管验证可充当的是，用户必须手动编辑一个记录，这不是可接受时删除的货币符号。 此外，如果有无效输入中的编辑的接口都不更新，也不取消按钮，当单击时，将调用回发。 理想情况下，取消按钮将为其预编辑而不考虑用户的输入数据的有效性状态返回 DataList。 此外，我们需要确保更新 DataList s 中的产品信息之前，s 的页面数据是有效`UpdateCommand`事件处理程序，作为其浏览器不支持 JavaScript 或具有的用户可以跳过客户端逻辑的验证控件禁用其支持。

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>从 EditItemTemplate s 单价文本框中删除的货币符号

当使用 CompareValidator 的`Currency``Type`，所验证的输入不能包含任何货币符号。 此类符号存在导致 CompareValidator 将标记为无效的输入。 但是，我们的编辑界面当前包括中的货币符号`UnitPrice`文本框中，这意味着用户必须显式保存其更改前删除的货币符号。 若要解决此问题，我们有三个选项：

1. 配置`EditItemTemplate`，以便`UnitPrice`文本框值未格式化为货币。
2. 允许用户通过删除 CompareValidator 并将它替换为正确格式的货币值检查 RegularExpressionValidator 输入货币符号。 此处的挑战就是要验证的货币值的正则表达式不是像简单 CompareValidator，如果我们想要合并的区域性设置则需要编写代码。
3. 完全删除的验证控件和 GridView s 中的自定义服务器端验证逻辑依赖于`RowUpdating`事件处理程序。

让我们来使用本教程中的选项 1。 目前`UnitPrice`格式化为货币值的文本框中的数据绑定表达式由于`EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`。 更改`Eval`语句`Eval("UnitPrice", "{0:n2}")`，其中将结果格式化为带两位数字的精度的数字。 这可以通过声明性语法直接或通过单击从编辑 DataBindings 链接`UnitPrice`DataList s 中的文本框`EditItemTemplate`。

进行此更改后，编辑界面中的格式化的价格包含组分隔符为逗号和句点作为小数分隔符，但哪儿货币符号。

> [!NOTE]
> 删除时的货币格式从可编辑的接口，我发现有助于将作为外部文本框的文本放在货币符号。 这将作为对它们不需要提供的货币符号的用户的提示。


## <a name="fixing-the-cancel-button"></a>修复取消按钮

默认情况下，验证 Web 控件发出 JavaScript 客户端上执行验证。 单击按钮、 LinkButton 或 ImageButton 时，发生回发之前，要在客户端检查的页上的验证控件。 如果没有任何无效的数据，则取消回发。 对于某些按钮，不过，这些数据的有效性可能无关紧要;在这种情况下，由于数据无效而取消在回发是麻烦。

取消按钮是此类示例。 假设用户输入无效数据，例如省略 s 产品名称，，，然后决定她没有 t 要保存该产品毕竟并点击取消按钮。 目前，取消按钮触发验证控件的页上，该报告的产品名称缺失，并防止在回发。 我们的用户必须键入一些文本`ProductName`文本框只是为了取消编辑过程。

幸运的是，具有按钮、 LinkButton 和 ImageButton [ `CausesValidation`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx)，可以指示是否单击该按钮应启动的验证逻辑 (默认为`True`)。 设置的取消按钮 s`CausesValidation`属性设置为`False`。

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>确保输入是在 UpdateCommand 事件处理程序中有效

由于客户端脚本发出的验证控件中，如果用户输入无效的输入验证控件取消按钮，LinkButton，由启动任何回发或 ImageButton 控件`CausesValidation`属性是`True`(默认值）。 但是，如果用户访问弃用了早已过时浏览器或从一台支持其 JavaScript 已被禁用，不会执行客户端验证检查。

ASP.NET 验证控件的所有重复他们立即在回发时的验证逻辑并报告整体通过页面 + s 输入的有效性[`Page.IsValid`属性](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)。 但是，页面流不是中断或停止任何方式基于的值中`Page.IsValid`。 作为开发人员，它是我们有责任确保`Page.IsValid`属性的值为`True`继续进行假设有效的代码输入数据之前。

如果用户已禁用 JavaScript，访问我们的页面、 编辑产品、 输入过的价格值开销很大，并单击更新按钮，将跳过客户端验证和回发将会随之发生。 在回发时，ASP.NET 页面 + s`UpdateCommand`事件处理程序执行，并引发异常时尝试分析过代价高昂的`Decimal`。 由于我们具有异常处理，此类异常将正常处理，但我们无法防止无效的数据通过第一个位置中仅使用继续操作落后`UpdateCommand`事件处理程序如果`Page.IsValid`的值为`True`。

将以下代码添加到开头`UpdateCommand`事件处理程序之前`Try`块：


[!code-vb[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample2.vb)]

添加此元素，该产品将尝试提交的数据是有效时才进行更新。 大多数用户结束-赢得 t 能够回发无效数据，因为验证控件客户端脚本，但其浏览器不支持 JavaScript 或具有支持的 JavaScript 的用户禁用，可以跳过客户端检查和提交无效数据。

> [!NOTE]
> 敏锐的读者的 GridView 中，更新数据时将会记得，我们并没有无需显式检查`Page.IsValid`我们页的代码隐藏类中的属性。 这是因为 GridView 咨询`Page.IsValid`我们和仅继续进行更新，仅当返回的值的属性`True`。


## <a name="step-3-summarizing-data-entry-problems"></a>步骤 3： 汇总数据输入问题

ASP.NET 包括五个验证控件中，除了[ValidationSummary 控件](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，其中显示`ErrorMessage`s 检测到无效数据这些验证控件。 此摘要数据可以显示为文本在网页上或通过模式、 客户端的消息框。 让我们来增强此教程，包括汇总的任何验证问题的客户端的 messagebox。

若要实现此目的，请从工具箱拖到设计器拖动 ValidationSummary 控件。 ValidationSummary 控件不是 t 的位置非常重要，因为我们重新将它配置为仅显示为一个消息框的摘要。 添加控件之后, 设置其[`ShowSummary`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)到`False`并将其[`ShowMessageBox`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)到`True`。 添加此元素后，任何验证错误汇总客户端的 messagebox 中 （请参阅图 6）。


[![客户端的 Messagebox 中总结了验证错误](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image16.png)

**图 6**： 客户端的 Messagebox 中总结了验证错误 ([单击以查看实际尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image18.png))


## <a name="summary"></a>总结

在本教程中我们已了解如何通过使用验证控件以主动确保尝试更新工作流中使用它们之前，我们的用户输入有效减少异常的可能性。 ASP.NET 提供了五个验证 Web 控件，可用于检查特定 Web 控件 s 输入，并报告回输入的 s 有效性。 在本教程中我们使用这些五个控件的两个 RequiredFieldValidator 和 CompareValidator 来确保提供的产品的名称和价格，必须具有值大于或等于零的货币格式。

向 DataList s 编辑界面添加验证控件非常简单，将其拖到拖动`EditItemTemplate`从工具箱并设置少量的属性。 默认情况下，验证控件自动发出客户端验证脚本;它们还提供服务器端验证回发时，存储中的累积结果`Page.IsValid`属性。 若要在单击按钮、 LinkButton 或 ImageButton 时绕过客户端验证，请设置按钮 s`CausesValidation`属性设置为`False`。 此外，在与在回发时提交的数据执行任何任务之前，请确保`Page.IsValid`属性返回`True`。

所有编辑教程 DataList 我们 ve 检查到目前为止已经非常简单的编辑接口产品的名称的文本框，另一个用于价格。 但是，编辑界面，可以包含多种不同的 Web 控件，如 Dropdownlist、 日历、 单选按钮、 复选框，依次类推。 在我们的下一教程中，我们将了解构建一个接口，使用各种 Web 控件。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Dennis Patterson、 Ken Pespisa 和 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](handling-bll-and-dal-level-exceptions-vb.md)
> [下一页](customizing-the-datalist-s-editing-interface-vb.md)
