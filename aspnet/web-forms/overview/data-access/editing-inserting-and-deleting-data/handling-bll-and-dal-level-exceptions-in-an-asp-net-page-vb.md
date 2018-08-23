---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: 处理 BLL 和 DAL 级别 ASP.NET 页面 (VB) 中的异常 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将了解如何显示一条友好、 信息性错误消息应在插入、 更新或删除操作期间会发生异常...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 86b8bb00e83f311d311a51a747086356833a8c93
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825277"
---
<a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>处理 BLL 和 DAL 级别 ASP.NET 页面 (VB) 中的异常
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe)或[下载 PDF](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> 在本教程中我们将了解如何显示一条友好、 信息性错误消息应在插入、 更新或删除操作的 ASP.NET 数据 Web 控件期间会发生异常。


## <a name="introduction"></a>介绍

使用 ASP.NET web 应用程序使用分层应用程序体系结构中的数据的工作涉及以下三个常规步骤：

1. 确定哪种业务逻辑层方法需要调用，以及要向其传递哪些参数值。 参数值可以是硬编码，以编程方式分配，或由用户输入的输入。
2. 调用方法。
3. 处理结果。 在调用返回数据的 BLL 方法时，这可能涉及到将数据绑定到数据 Web 控件。 有关修改数据的 BLL 方法，这可能包括在执行某些操作基于返回值或适当地处理在步骤 2 中出现任何异常。

中可以看到[前一篇教程](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)，ObjectDataSource 和数据 Web 控件提供的扩展点的步骤 1 和 3。 GridView 中，例如，激发其`RowUpdating`事件之前将其字段值分配给其 ObjectDataSource`UpdateParameters`集合; 它`RowUpdated`ObjectDataSource 完成该操作后引发事件。

我们已经探讨了过程步骤 1 中激发并已全面了解如何使用它们以自定义的输入的参数或取消操作的事件。 在本教程中我们要将注意力转移到在操作完成后触发的事件。 与我们可以除此之外，这些后级别事件处理程序确定在操作期间是否发生了异常和正常地处理在屏幕上显示一条友好、 信息性错误消息，而不是默认设置为标准的 ASP.NET异常页。

为了说明使用这些后级别事件，让我们创建列出的产品可编辑的 GridView 中的页面。 更新产品，如果异常引发时我们 ASP.NET 页将显示一条短消息上面 GridView 说明出现问题。 让我们进入正题！

## <a name="step-1-creating-an-editable-gridview-of-products"></a>步骤 1： 创建可编辑产品的 GridView

上一教程中我们创建可编辑的 GridView 与仅使用两个字段`ProductName`和`UnitPrice`。 这需要创建的其他重载`ProductsBLL`类的`UpdateProduct`方法，即： 按相反的每个产品字段参数，才接受三个输入的参数 （该产品的名称、 单价和 ID）。 本教程中，让我们来练习此技术同样，创建可编辑的 GridView 显示产品的名称，每个单元、 单价和单位数量库存数量，但在要编辑的库存中仅允许的名称、 单价和单位。

为了适应这种情况下，我们需要的另一个重载`UpdateProduct`方法中，一个接受四个参数： 产品的名称、 单价、 量股票和 id。 添加以下方法`ProductsBLL`类：


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

完成此方法中，我们就准备好创建允许进行编辑这四个特定产品字段的 ASP.NET 页。 打开`ErrorHandling.aspx`页中`EditInsertDelete`文件夹，并在设计器中翻页添加 GridView。 将 GridView 绑定到新的对象数据源，映射`Select()`方法`ProductsBLL`类的`GetProducts()`方法并`Update()`方法`UpdateProduct`刚创建的重载。


[![使用接受四个输入的参数的 UpdateProduct 方法重载](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**图 1**： 使用`UpdateProduct`方法重载，接受四个输入参数 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png))


这将创建与 ObjectDataSource`UpdateParameters`具有四个参数和字段与 GridView 每个产品字段的集合。 ObjectDataSource 的声明性标记将分配`OldValuesParameterFormatString`属性值`original_{0}`，这将导致异常，因为我们的 BLL 类不预期输入的参数名为`original_productID`中传递。 不要忘了删除此设置完全从声明性语法 (或将其设置为默认值为`{0}`)。

接下来，削减 GridView，其中仅包含`ProductName`， `QuantityPerUnit`， `UnitPrice`，和`UnitsInStock`BoundFields。 此外可以随时以应用你认为所必要的任何字段级别格式 (例如，更改`HeaderText`属性)。

上一教程中我们介绍了如何设置格式`UnitPrice`BoundField 为货币在只读模式和编辑模式中。 让我们来做同一此处。 回想一下，这需要设置 BoundField`DataFormatString`属性设置为`{0:c}`，将其`HtmlEncode`属性设置为`false`，并将其`ApplyFormatInEditMode`到`true`，如图 2 所示。


[![将显示单价 BoundField 配置为一种货币](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**图 2**： 配置`UnitPrice`显示为一种货币的 BoundField ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png))


格式设置`UnitPrice`因为编辑界面中的货币需要创建一个事件处理程序的 GridView`RowUpdating`货币格式将字符串分析成事件`decimal`值。 请记住，`RowUpdating`最后一个教程中的事件处理程序还检查以确保用户提供`UnitPrice`值。 但是，本教程中我们允许用户省略价格。


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

我们 GridView 包括`QuantityPerUnit`BoundField，但此 BoundField 应仅出于显示目的，不应由用户可编辑。 若要这样安排，只需设置 BoundFields'`ReadOnly`属性设置为`true`。


[![使 QuantityPerUnit BoundField 成为只读](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**图 3**： 请`QuantityPerUnit`BoundField 只读的 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png))


最后，检查从 GridView 的智能标记启用编辑复选框。 完成这些步骤后`ErrorHandling.aspx`页面的设计器应类似于图 4。


[![删除所有但时需要 BoundFields 并检查编辑复选框启用](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**图 4**： 删除以外的所有所需 BoundFields 并选中启用编辑复选框 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png))


现在我们有一系列的产品的所有`ProductName`， `QuantityPerUnit`， `UnitPrice`，和`UnitsInStock`字段; 但是，仅`ProductName`， `UnitPrice`，和`UnitsInStock`可编辑字段。


[![用户现在可以轻松地编辑产品的名称、 价格和库存字段中的单元](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**图 5**： 用户可立即轻松地编辑产品的名称、 价格和库存字段中的单元 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png))


## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>步骤 2： 正常处理 DAL 级别的异常

尽管我们可编辑的 GridView 浅显有效用户时输入的已编辑的产品的名称、 价格和库存数量的合法值，输入非法值会导致异常。 例如，省略`ProductName`值的原因[NoNullAllowedException](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp)以来引发`ProductName`中的属性`ProdcutsRow`类具有其`AllowDBNull`属性设置为`false`; 如果数据库已关闭，`SqlException`尝试连接到数据库时，TableAdapter 将引发。 不采取任何措施，这些异常向上冒泡从数据访问层业务逻辑层，则 ASP.NET 页中，最后到 ASP.NET 运行时。

具体取决于如何配置 web 应用程序以及是否正在访问应用程序从`localhost`，未处理的异常可能会导致常规服务器错误页、 详细的错误报表或用户友好的网页。 请参阅[Web 应用程序中的错误处理 ASP.NET](http://www.15seconds.com/issue/030102.htm)并[customErrors 元素](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx)为 ASP.NET 运行时如何响应未捕获的异常的详细信息。

图 6 显示了屏幕时尝试将产品更新而无需指定遇到`ProductName`值。 这是通过显示详细的错误报告的默认`localhost`。


[![省略产品的名称将显示异常详细信息](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**图 6**： 忽略该产品的名称将显示异常详细信息 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png))


虽然测试应用程序时，此类异常详细信息很有用，向最终用户显示此类屏幕在遇到异常时是不太理想。 最终用户可能不知道什么`NoNullAllowedException`是或原因所致。 更好的方法是向用户显示一条说明时出现问题尝试更新的产品的更加友好的用户消息。

如果执行操作时出现异常，ObjectDataSource 和数据 Web 控件中的后续级别事件提供一种方法对其进行检测并取消从向上冒泡到 ASP.NET 运行时异常。 对于我们的示例，让我们将创建为 GridView 的事件处理程序`RowUpdated`确定异常触发，如果是这样，在标签 Web 控件中显示异常详细信息的事件。

首先，将标签添加到 ASP.NET 页上，设置其`ID`属性设置为`ExceptionDetails`并清除其`Text`属性。 若要绘制到此消息的用户的关注，设置其`CssClass`属性设置为`Warning`，它是我们添加到一个 CSS 类`Styles.css`上一教程中的文件。 回想一下，此 CSS 类会导致将标签的文本以红色、 斜体、 粗体、 特大型字体显示。


[![向页面添加一个标签 Web 控件](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**图 7**： 向页面添加一个标签 Web 控件 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png))


由于我们希望此标签 Web 控件可见仅立即后发生了异常，设置其`Visible`属性设置为 false 在`Page_Load`事件处理程序：


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

使用此代码，第一次页面访问和后续回发`ExceptionDetails`控件将具有其`Visible`属性设置为`false`。 DAL 或 BLL 级别异常，这可以检测到 GridView 中遇到`RowUpdated`事件处理程序，我们将把`ExceptionDetails`控件的`Visible`属性设为 true。 因为 Web 控件事件处理程序后会发生`Page_Load`页面生命周期中的事件处理程序，将显示标签。 但是，在下一个回发`Page_Load`事件处理程序将恢复`Visible`属性改回`false`，再次从视图中隐藏。

> [!NOTE]
> 或者，我们可以删除设置的必要性`ExceptionDetails`控件的`Visible`属性中的`Page_Load`通过将分配其`Visible`属性`false`中的声明性语法和禁用 （设置其其视图状态`EnableViewState`属性设置为`false`)。 我们将在以后的教程中使用此另一种方法。


下一步是为 GridView 的创建事件处理程序添加的标签控件，与`RowUpdated`事件。 在设计器中选择 GridView，转到属性窗口中，然后单击闪电形图标，列出 GridView 的事件。 应该已有的条目的 GridView 的`RowUpdating`事件，如我们前面在本教程中创建此事件的事件处理程序。 创建事件处理程序`RowUpdated`以及事件。


![GridView 的 RowUpdated 事件创建事件处理程序](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**图 8**： 创建 GridView 的事件处理程序`RowUpdated`事件


> [!NOTE]
> 此外可以在代码隐藏类文件的顶部创建通过下拉列表的事件处理程序。 从左侧的下拉列表中选择 GridView 和`RowUpdated`从右侧的一个事件。


创建此事件处理程序后，将以下代码添加到 ASP.NET 页面的代码隐藏类中：


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

此事件处理程序的第二个输入的参数是类型的对象[GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)，其中包含用于处理异常的感兴趣的三个属性：

- `Exception` 对引发的异常; 的引用如果已不引发任何异常，此属性将具有的值 `null`
- `ExceptionHandled` 一个布尔值，指示是否在处理异常`RowUpdated`事件处理程序; 如果`false`（默认值），例外情况是重新引发，ASP.NET 运行时决定沸沸扬扬
- `KeepInEditMode` 如果设置为`true`编辑过的 GridView 行保持在编辑模式下; 如果`false`（默认值），GridView 行会还原为其只读模式

我们的代码，然后，应检查以查看是否`Exception`不是`null`，这意味着时执行操作时引发了异常。 如果是这样，我们希望：

- 显示用户友好消息`ExceptionDetails`标签
- 指示已处理该异常
- GridView 行保留在编辑模式下

此下面的代码来实现这些目标：


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

此事件处理程序首先会检查是否`e.Exception`是`null`。 如果不是，`ExceptionDetails`标签的`Visible`属性设置为`true`并将其`Text`属性设置为"时出现问题更新产品。" 实际引发的异常的详细信息位于`e.Exception`对象的`InnerException`属性。 此内部异常进行检查; 如果它是特定类型，其他的、 有帮助的消息追加到`ExceptionDetails`标签的`Text`属性。 最后，`ExceptionHandled`并`KeepInEditMode`属性均设置为`true`。

图 9 显示了此页的屏幕截图时省略产品; 的名称图 10 显示了结果，如果输入非法`UnitPrice`值 (-50)。


[![ProductName BoundField 必须包含值](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**图 9**: `ProductName` BoundField 必须包含值 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png))


[![负单价值是不允许](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**图 10**： 负`UnitPrice`的值为不允许 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png))


通过设置`e.ExceptionHandled`属性设置为`true`，则`RowUpdated`事件处理程序已指明它已处理异常。 因此，该异常不会传播到 ASP.NET 运行时。

> [!NOTE]
> 图 9 和 10 显示妥善的方式来处理由于无效的用户输入而引发的异常。 理想情况下，不过，此类的输入无效将永远不会市场宣传业务逻辑层的初衷，因为 ASP.NET 页中，应确保在调用之前的用户的输入是否有效`ProductsBLL`类的`UpdateProduct`方法。 在我们下一教程中我们将了解如何将验证控件添加到要确保提交到业务逻辑层的数据的编辑和插入接口符合业务规则。 验证控件不只是防止调用`UpdateProduct`方法，直到用户提供的数据有效，但还提供用于标识数据输入问题的信息更丰富的用户体验。


## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>步骤 3： 正常处理 BLL 级别的异常

插入时，更新或删除数据，数据访问层可能会引发在遇到与数据相关的错误时出现异常。 数据库可能处于脱机状态、 所需的数据库表列可能不具有指定的值或表级约束可能违反了。 除了严格与数据相关的异常，业务逻辑层可以使用异常以指示何时违反了业务规则。 在中[创建业务逻辑层](../introduction/creating-a-business-logic-layer-vb.md)教程中，例如，我们添加到原始业务规则检查`UpdateProduct`重载。 具体而言，如果用户已将产品标记为停止使用，我们需要产品不是唯一一个其供应商提供。 如果违反了这种情况，`ApplicationException`抛出。

有关`UpdateProduct`重载创建在本教程中，让我们添加的业务规则，禁止`UnitPrice`字段从设置为新值的两倍以上的原始`UnitPrice`值。 若要实现此目的，调整`UpdateProduct`重载，以便它来执行此检查并引发`ApplicationException`如果违反该规则。 更新后的方法如下所示：


[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

此更改是两次以上的现有价格的任何价格更新将导致`ApplicationException`引发。 就像从 DAL，此 BLL 引发所引发的异常`ApplicationException`可以检测到并且在 GridView 中处理`RowUpdated`事件处理程序。 事实上，`RowUpdated`事件处理程序的代码编写的如将正确检测到此异常并显示`ApplicationException`的`Message`属性值。 图 11 显示了屏幕快照时用户尝试更新 Chai 的价格为 50.00 美元，这是多个双精度 19.95 美元及其当前股价。


[![业务规则不允许产品的价格一倍以上的价格上调](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**图 11**: 业务规则禁止产品的价格一倍以上的价格增加 ([单击以查看实际尺寸的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png))


> [!NOTE]
> 理想情况下我们的业务逻辑规则进行重构共`UpdateProduct`方法重载并进入一种常用方法。 这是留给大家练练手为读取器。


## <a name="summary"></a>总结

在插入、 更新和删除操作，数据 Web 控件和所涉及对象的数据源触发前和后级别事件的书档实际操作。 正如我们看到在本教程并前一次时使用的可编辑的 GridView GridView`RowUpdating`事件触发时后, 跟 ObjectDataSource 的`Updating`事件，此时 update 命令对 ObjectDataSource 的基础对象。 操作完成后，ObjectDataSource 的后`Updated`事件触发时后, 跟 GridView 的`RowUpdated`事件。

我们可以创建以自定义的输入的参数预级别的事件，或者为了检查和响应操作的结果后级别的事件的事件处理程序。 后级别事件处理程序通常用于检测是否在操作期间发生了异常。 遇到异常，这些后级别事件处理程序可以根据需要处理上其自己的异常。 在本教程中我们已了解如何通过显示友好的错误消息来处理此类异常。

在下一教程中，我们将了解如何降低因数据格式设置问题的异常的可能性 (例如输入为负`UnitPrice`)。 具体而言，我们将介绍如何向编辑和插入界面添加验证控件。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [下一页](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
