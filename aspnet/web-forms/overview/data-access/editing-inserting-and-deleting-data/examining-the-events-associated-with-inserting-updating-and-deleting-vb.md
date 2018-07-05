---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
title: 检查有关的事件与插入、 更新和删除 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将探讨使用发生之前、 期间和之后插入的事件，更新或删除操作的 ASP.NET 数据 Web 控件。 W...
ms.author: aspnetcontent
ms.date: 07/17/2006
ms.assetid: c9bd10a7-eff8-4d8c-bec9-963c2aef2d6e
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 548bfecc4215fbb2b36e0e2be42c7c08ee884270
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817157"
---
<a name="examining-the-events-associated-with-inserting-updating-and-deleting-vb"></a>检查与插入、 更新和删除 (VB) 关联的事件
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_VB.exe)或[下载 PDF](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/datatutorial17vb1.pdf)

> 在本教程中我们将探讨使用发生之前、 期间和之后插入的事件，更新或删除操作的 ASP.NET 数据 Web 控件。 我们还将了解如何自定义的编辑界面只更新产品字段的子集。


## <a name="introduction"></a>介绍

使用内置插入、 编辑或删除功能的 GridView、 detailsview 和 FormView 控件时，各种步骤暴露在最终用户完成添加新记录或更新或删除现有记录的过程。 如中所述[前一篇教程](an-overview-of-inserting-updating-and-deleting-data-vb.md)，在编辑按钮替换为更新和取消按钮并在文本框 BoundFields 打开 GridView 中编辑行时。 最终用户更新的数据，并单击更新后，在回发时执行以下步骤：

1. GridView 填充其 ObjectDataSource`UpdateParameters`使用已编辑的记录的唯一标识字段 (通过`DataKeyNames`属性) 以及由用户输入的值
2. GridView 调用其 ObjectDataSource`Update()`方法，后者又调用基础对象中合适的方法 (`ProductsDAL.UpdateProduct`，我们上一教程中)
3. 基础数据，现在包括更新后的更改，重新绑定到 GridView

在此过程的步骤中，多个事件触发，使我们能够创建事件处理程序以添加自定义逻辑在需要时。 例如，在步骤 1，GridView 之前`RowUpdating`事件触发。 如果某些验证错误，我们可以在此情况下，取消更新请求。 当`Update()`调用方法时，ObjectDataSource`Updating`事件触发时，提供添加或自定义的任何值的机会`UpdateParameters`。 对象的方法的基本 ObjectDataSource 后已完成执行，ObjectDataSource 的`Updated`引发事件。 事件处理程序`Updated`事件可以检查有关的更新操作，例如多少行受到影响，以及是否发生了异常的详细信息。 最后，在步骤 2，GridView`RowUpdated`触发事件; 检查执行只是更新操作的其他信息的事件处理程序会此事件。

图 1 所示更新 GridView 时这一系列的事件和步骤。 图 1 中的事件模式不是唯一的更新与 GridView。 插入、 更新或删除数据从 GridView、 detailsview 和 FormView precipitates 相同的数据 Web 控件和 ObjectDataSource 的前期和后期级别事件序列。


[![系列的预和事后事件触发更新的 GridView 中的数据时](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image1.png)

**图 1**: 系列的前和事后事件激发时更新的数据的 GridView 中 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image3.png))


在本教程中我们将探讨使用这些事件来扩展内置的插入、 更新和删除功能的 ASP.NET 数据 Web 控件。 我们还将了解如何自定义的编辑界面只更新产品字段的子集。

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>步骤 1： 更新的产品`ProductName`和`UnitPrice`字段

在上一教程中的编辑接口*所有*产品不是只读的已包含的字段。 如果我们要从中 GridView-删除字段说`QuantityPerUnit`-当更新数据的数据 Web 控件不会设置 ObjectDataSource `QuantityPerUnit` `UpdateParameters`值。 中的值然后传递 ObjectDataSource`Nothing`到`UpdateProduct`业务逻辑层 (BLL) 方法，更改已编辑的数据库记录`QuantityPerUnit`列`NULL`值。 同样，如果必填字段，如`ProductName`，删除从编辑界面，则更新将失败与"*列 'ProductName' 不允许使用 null*"异常。 此行为的原因是因为 ObjectDataSource 已配置为调用`ProductsBLL`类的`UpdateProduct`方法，每个产品字段预期的输入的参数。 因此，ObjectDataSource 的`UpdateParameters`集合包含一个参数为每个方法的输入参数。

如果我们想要提供数据 Web 控件，它允许最终用户只更新字段的子集，则需要以编程方式设置缺失`UpdateParameters`ObjectDataSource 的中值`Updating`事件处理程序或创建和调用 BLL 方法预期的字段的子集。 我们来探讨这后一种方法。

具体而言，让我们创建一个显示页面只`ProductName`和`UnitPrice`可编辑的 GridView 中的字段。 此 GridView 编辑界面仅允许用户更新两个显示的字段`ProductName`和`UnitPrice`。 由于此编辑界面仅提供产品的字段的子集，我们也需要创建使用现有 BLL ObjectDataSource`UpdateProduct`方法中，并且缺少产品字段值设置以编程方式在其`Updating`事件处理程序，或者我们需要创建新的 BLL 方法需要仅在 GridView 中定义的字段的子集。 对于本教程，让我们使用后一种选择和创建的重载`UpdateProduct`方法，只需三个输入参数中的一个： `productName`， `unitPrice`，和`productID`:


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample1.vb)]

像原始`UpdateProduct`方法，此重载开始时检查，以查看具有指定数据库中是否存在产品`ProductID`。 如果不是，它返回`False`，指示更新的产品信息的请求失败。 否则它会更新现有产品记录`ProductName`并`UnitPrice`相应地字段并提交更新通过调用 TableAdpater`Update()`方法，传入`ProductsRow`实例。

通过这一附加到我们`ProductsBLL`类中，我们已准备好创建简化的 GridView 界面。 打开`DataModificationEvents.aspx`在`EditInsertDelete`文件夹和向页添加 GridView。 创建新对象数据源，并将其配置为使用`ProductsBLL`类的其`Select()`方法映射到`GetProducts`并将其`Update()`方法映射到`UpdateProduct`重载仅采用`productName`， `unitPrice`，和`productID`输入参数。 图 2 显示了创建数据源向导时映射 ObjectDataSource`Update()`方法`ProductsBLL`类的新`UpdateProduct`方法重载。


[![将 ObjectDataSource 的 update （） 方法映射到新的 UpdateProduct 重载](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image4.png)

**图 2**： 映射的 ObjectDataSource`Update()`方法新建`UpdateProduct`重载 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image6.png))


由于我们的示例将最初只需要编辑数据，但不是能插入或删除记录的功能，请花费片刻时间以显式指示 ObjectDataSource 的`Insert()`并`Delete()`方法不应映射到的任何`ProductsBLL`通过转到插入和删除选项卡并从下拉列表中选择 （无） 的类的方法。


[![从插入和删除选项卡的下拉列表中选择 （无）](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image7.png)

**图 3**： 选择 （无） 从下拉列表中的插入和删除选项卡的 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image9.png))


完成此向导后检查从 GridView 的智能标记启用编辑复选框。

创建数据源向导和绑定到 GridView 完成时，Visual Studio 创建了这两个控件的声明性语法。 请转到源视图以检查 ObjectDataSource 的声明性标记，其如下所示：


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample2.aspx)]

由于不没有为 ObjectDataSource 的任何映射`Insert()`并`Delete()`方法，有没有`InsertParameters`或`DeleteParameters`部分。 此外，由于`Update()`方法映射到`UpdateProduct`只接受三个输入的参数的方法重载`UpdateParameters`部分具有只需三个`Parameter`实例。

请注意，ObjectDataSource`OldValuesParameterFormatString`属性设置为`original_{0}`。 使用配置数据源向导时，此属性是由 Visual Studio 自动进行设置。 但是，由于我们 BLL 方法不需要原始`ProductID`要传递中，从 ObjectDataSource 的声明性语法中完全删除此属性分配值。

> [!NOTE]
> 如果只需清除`OldValuesParameterFormatString`属性值从属性窗口在设计视图中，该属性仍将存在于声明性语法，但将设置为空字符串。 删除属性完全声明性语法中，或从属性窗口中，将值设置为默认情况下， `{0}`。


虽然 ObjectDataSource 只有`UpdateParameters`有关产品的名称、 价格和 ID，Visual Studio 添加了 BoundField 或 CheckBoxField GridView 中每个产品的字段。


[![GridView 包含 BoundField 或 CheckBoxField 每个产品的字段](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image10.png)

**图 4**: GridView 包含 BoundField 或 CheckBoxField 每个产品的字段 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image12.png))


当最终用户编辑产品并单击其更新按钮时，GridView 枚举不是只读的这些字段。 然后将相应参数的值设置为 ObjectDataSource 的`UpdateParameters`由用户输入的值的集合。 如果没有对应的参数，则将添加 GridView 向该集合。 因此，如果我们 GridView 包含 BoundFields 和 CheckBoxFields 所有产品的字段，ObjectDataSource 将结束调用`UpdateProduct`在所有这些参数，尽管使用重载的 ObjectDataSource 的声明性标记指定只有三个输入的参数 （参见图 5）。 同样，如果没有非只读的某种组合产品字段中都不对应的输入参数的 GridView`UpdateProduct`重载，尝试更新时，将引发异常。


[![GridView 会将参数添加到为 ObjectDataSource 的 UpdateParameters 集合](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image13.png)

**图 5**: GridView 将向添加参数的 ObjectDataSource`UpdateParameters`集合 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image15.png))


以确保 ObjectDataSource 调用`UpdateProduct`重载采用只是该产品的名称、 价格和 ID，我们需要将 GridView 限制为具有可编辑字段只`ProductName`和`UnitPrice`。 这可以通过删除其他 BoundFields 和 CheckBoxFields，通过设置这些其他字段来实现`ReadOnly`属性设置为`True`，或两者的某些组合。 本教程中我们只需删除之外的所有 GridView 字段`ProductName`和`UnitPrice`BoundFields，其后 GridView 的声明性标记将如下所示：


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample3.aspx)]

即使`UpdateProduct`重载需要三个输入的参数，我们只能具有两个 BoundFields 我们 GridView 中。 这是因为`productID`输入的参数是主键值和传递的值通过`DataKeyNames`编辑过的行的属性。

我们 GridView，连同`UpdateProduct`重载，允许用户编辑而不会丢失的任何其他产品字段只是名称和产品价格。


[![此接口允许编辑只是该产品的名称和价格](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image16.png)

**图 6**： 编辑只是该产品的名称和价格接口允许 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image18.png))


> [!NOTE]
> 在上一教程中所述，是极其重要的 GridView 的视图状态是启用 （默认行为）。 如果设置 GridView s`EnableViewState`属性设置为`false`，运行的并发用户无意中删除或编辑记录风险。 请参阅[警告： 禁用并发问题与 ASP.NET 2.0 Gridview/DetailsView/FormViews 该支持编辑和/或删除和其视图状态](http://scottonwriting.net/sowblog/posts/10054.aspx)有关详细信息。


## <a name="improving-theunitpriceformatting"></a>提高`UnitPrice`格式设置

尽管图 6 works 中所示的 GridView 示例`UnitPrice`根本不设置格式字段，导致在价格显示模式中缺少任何货币符号并且具有四个小数位。 若要应用的货币格式设置为不可编辑的行，只需设置`UnitPrice`BoundField 的`DataFormatString`属性设置为`{0:c}`并将其`HtmlEncode`属性设置为`False`。


[![相应地设置单价的数据和 HtmlEncode 属性](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image19.png)

**图 7**： 设置`UnitPrice`的`DataFormatString`并`HtmlEncode`相应属性 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image21.png))


进行此更改后，不可编辑的行设置价格的格式为货币;编辑过的行，但是，仍显示没有货币符号，使用了四个小数位的值。


[![非可编辑的行是现进行格式设置为货币值](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image22.png)

**图 8**: 非可编辑的行是现在的格式为货币值 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image24.png))


中指定的格式设置说明`DataFormatString`属性可以通过设置 BoundField 应用于编辑界面`ApplyFormatInEditMode`属性设置为`True`(默认值是`False`)。 请花费片刻时间来将此属性设置为`True`。


[![将单价 BoundField ApplyFormatInEditMode 属性设置为 True](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image25.png)

**图 9**： 设置`UnitPrice`BoundField 的`ApplyFormatInEditMode`属性设置为`True`([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image27.png))


此更改的值与`UnitPrice`显示在编辑行也设置为货币格式。


[![编辑行的单价值是格式为货币](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image28.png)

**图 10**: 编辑行`UnitPrice`值是现在的格式为货币 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image30.png))


但是，在文本框中的货币符号与更新产品，如美元 19.00 引发`FormatException`。 当尝试将用户提供的值分配给 ObjectDataSource 的 GridView`UpdateParameters`不能进行转换的集合`UnitPrice`到字符串"$19.00"`Decimal`所需的参数 （请参阅图 11）。 若要纠正此我们可以为 GridView 的创建事件处理程序`RowUpdating`事件，并将其分析的用户提供`UnitPrice`为货币格式`Decimal`。

GridView`RowUpdating`事件接受作为其第二个参数类型的对象[GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)，其中包括`NewValues`作为包含准备好的用户提供值的属性之一的字典分配给 ObjectDataSource 的`UpdateParameters`集合。 我们可以覆盖现有`UnitPrice`中的值`NewValues`分析十进制值的集合，用以下行中的代码使用货币格式`RowUpdating`事件处理程序：


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample4.vb)]

如果用户已提供`UnitPrice`值 （例如"$19.00")，覆盖此值与计算的十进制值[Decimal.Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)，作为一种货币值的分析。 这将正确地分析任何货币符号、 逗号、 小数点和等等，发生在小数点，并使用[NumberStyles 枚举](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx)中[System.Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx)命名空间。

图 11 显示了这两个问题引起的中的用户提供的货币符号`UnitPrice`，以及如何 GridView 的`RowUpdating`可利用事件处理程序可以正确地分析此类输入。


[![编辑行的单价值是格式为货币](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image31.png)

**图 11**: 编辑行`UnitPrice`值是现在的格式为货币 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image33.png))


## <a name="step-2-prohibitingnull-unitprices"></a>步骤 2： 禁止`NULL UnitPrices`

尽管数据库配置为允许`NULL`中的值以`Products`表的`UnitPrice`列中，我们可能希望阻止用户访问此特定页，指定从`NULL``UnitPrice`值。 也就是说，如果用户无法输入`UnitPrice`值时编辑产品行，而不是将结果保存到我们想要显示一条消息，通知用户，通过此页上，任何已编辑的产品必须具有指定的价格的数据库。

`GridViewUpdateEventArgs`对象传递到 GridView`RowUpdating`事件处理程序包含`Cancel`属性，如果设置为`True`，终止更新的过程。 让我们扩展`RowUpdating`事件处理程序设置`e.Cancel`到`True`并显示一条说明原因，如果消息`UnitPrice`中的值`NewValues`集合的值为`Nothing`。

首先将标签 Web 控件添加到名为的页`MustProvideUnitPriceMessage`。 如果用户无法指定，则会显示此标签控件`UnitPrice`值更新产品时。 设置标签的`Text`属性设置为"您必须提供价格的产品。" 我还创建了一个新的 CSS 类中`Styles.css`名为`Warning`以下定义：


[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample5.css)]

最后，设置的标签`CssClass`属性设置为`Warning`。 此时设计器应显示的警告消息，以红色、 粗体、 斜体、 特大型字体大小高于 GridView，如图 12 中所示。


[![上面 GridView 中添加标签](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image34.png)

**图 12**: 标签具有已添加上面的 GridView ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image36.png))


默认情况下，此标签应隐藏，因此可将其`Visible`属性设置为`False`中`Page_Load`事件处理程序：


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample6.vb)]

如果用户尝试将产品更新而无需指定`UnitPrice`，我们想要取消更新并显示警告标签。 增强 GridView 的`RowUpdating`事件处理程序，如下所示：


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample7.vb)]

如果用户尝试保存产品而无需指定价格，会取消更新并显示有用的消息。 数据库 （和业务逻辑） 时允许`NULL` `UnitPrice` s，此特定的 ASP.NET 页却没有。


[![用户不能离开单价为空](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image37.png)

**图 13**: 用户不能离开`UnitPrice`保留为空 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image39.png))


到目前为止，我们已了解如何使用 GridView`RowUpdating`事件以编程方式更改分配给 ObjectDataSource 的参数值`UpdateParameters`集合以及如何取消更新处理完全。 这些概念延续到 DetailsView 和 FormView 控件，并且还应用于插入和删除。

这些任务也可以在对象数据源级别事件处理程序通过其`Inserting`， `Updating`，和`Deleting`事件。 这些事件触发之前调用关联的基础对象的方法，并提供修改输入的参数集合或取消操作完全是最后一个机会。 这三个事件的事件处理程序传递类型的对象[ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx)具有感兴趣的两个属性：

- [取消](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)，而后者如果设置为`True`，取消正在执行的操作
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)，这是一系列`InsertParameters`， `UpdateParameters`，或`DeleteParameters`，具体取决于事件处理程序是否为`Inserting`， `Updating`，或`Deleting`事件

为了说明使用级别的 ObjectDataSource 的参数值，让我们在我们的页面，用户可添加新的产品中包含 DetailsView。 此 DetailsView 将用于提供用于将新产品快速添加到数据库的接口。 若要让我们添加的新产品，允许用户仅输入的值时保持一致的用户界面`ProductName`和`UnitPrice`字段。 默认情况下，DetailsView 插入界面中不提供这些值将设置为`NULL`数据库值。 但是，我们可以使用 ObjectDataSource 的`Inserting`注入不同的默认值，稍后我们将看到的事件。

## <a name="step-3-providing-an-interface-to-add-new-products"></a>步骤 3： 提供一个接口来添加新产品

将从工具箱拖到上面 GridView，设计器的 DetailsView 清除其`Height`和`Width`属性和绑定到对象数据源页已存在。 这将为每个产品的字段添加 BoundField 或 CheckBoxField。 由于我们想要使用此 DetailsView 若要添加的新产品，因此我们需要检查从智能标记; 启用插入选项但是，没有此类选项因为 ObjectDataSource`Insert()`方法未映射到方法中`ProductsBLL`类 （回想一下，我们设置此映射到 （无） 时配置数据源，请参见图 3）。

若要配置对象数据源，请从其智能标记上，启动该向导中选择的配置数据源链接。 第一个屏幕，可更改对象数据源绑定到; 的基础对象将保留设置为`ProductsBLL`。 下一屏幕中列出了从 ObjectDataSource 的方法的基础对象的映射。 即使显式指示`Insert()`和`Delete()`方法不应映射到任何方法，如果你转到插入和删除选项卡可以看到映射是否有。 这是因为`ProductsBLL`的`AddProduct`并`DeleteProduct`方法使用`DataObjectMethodAttribute`特性以指示它们是默认方法`Insert()`和`Delete()`分别。 因此，ObjectDataSource 向导会选择这些每次您运行向导，除非显式指定的一些其他值。

将保留`Insert()`方法指向`AddProduct`方法，但重新设置为 （无） 删除选项卡的下拉列表。


[![将插入选项卡的下拉列表设置为 AddProduct 方法](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image40.png)

**图 14**： 将插入选项卡的下拉列表设置为`AddProduct`方法 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image42.png))


[![设置为 （无） 删除选项卡的下拉列表](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image43.png)

**图 15**： 设置为 （无） 删除选项卡的下拉列表 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image45.png))


进行这些更改后，ObjectDataSource 的声明性语法将展开以包括`InsertParameters`集合，如下所示：


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample8.aspx)]

重新运行该向导添加回去`OldValuesParameterFormatString`属性。 请花费片刻时间来清除此属性设置为默认值 (`{0}`) 或从其删除完全声明性语法。

使用 ObjectDataSource 提供插入功能，DetailsView 的智能标记现在将包括启用插入复选框;返回到设计器，并选中此选项。 接下来，以便它仅有两个 BoundFields-削减 DetailsView`ProductName`和`UnitPrice`-和 CommandField。 此时 DetailsView 的声明性语法应如下所示：


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample9.aspx)]

图 16 将显示此页现在通过浏览器查看时。 如您所见，DetailsView 列出的名称和 (Chai) 的第一个产品的价格。 我们希望的但是，是提供一个使用户可以快速向数据库添加新产品插入接口。


[![在 DetailsView 是当前在只读模式下呈现](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image46.png)

**图 16**: DetailsView 是当前在只读模式下呈现 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image48.png))


为了在我们需要设置其插入模式下显示 DetailsView`DefaultMode`属性设置为`Inserting`。 这将呈现在插入模式下时首先访问 DetailsView，插入新记录后使其存在。 如图 17 所示，此类 DetailsView 提供快速的接口用于添加新记录。


[![在 DetailsView 快速添加一个新的产品提供的接口](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image49.png)

**图 17**: DetailsView 提供一个接口用于快速添加新产品 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image51.png))


当用户输入产品名称和价格 （如"Acme Water"和 1.99，如图 17 所示），并单击 Insert 时，回发时，才会和插入工作流开始，通过在新的产品记录添加到数据库。 在 DetailsView 维护其插入接口和 GridView 自动重新绑定到其数据源以便包括新产品，如图 18 中所示。


![该产品](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image52.png)

**图 18**： 产品"Acme Water"已添加到数据库


虽然图 18 中的 GridView 中未显示，从 DetailsView 接口缺少的产品字段`CategoryID`， `SupplierID`， `QuantityPerUnit`，依次类推分配`NULL`数据库值。 您可以看到这通过执行以下步骤：

1. 转到 Visual Studio 中的服务器资源管理器
2. 展开`NORTHWND.MDF`database 节点
3. 右键单击`Products`数据库表节点
4. 选择显示表数据

这将列出所有中的记录`Products`表。 如图 19 所示，所有我们新的产品列以外`ProductID`， `ProductName`，并`UnitPrice`具有`NULL`值。


[![在 DetailsView 中未提供产品字段是分配 NULL 值](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image53.png)

**图 19**： 分配产品字段中未提供 DetailsView`NULL`值 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image55.png))


我们可能想要提供默认值以外`NULL`的一个或多个列的值，或者因为`NULL`不是最佳的默认选项或因为自身的数据库列不允许`NULL`s。 若要实现此目的我们可以以编程方式设置的 DetailsView 的参数的值`InputParameters`集合。 此分配可能会出于要么在事件处理程序 DetailsView`ItemInserting`事件或 ObjectDataSource 的`Inserting`事件。 由于我们已介绍了在使用前和后级别事件的数据 Web 控制级别，我们来探讨一下使用这一次的 ObjectDataSource 的事件。

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>步骤 4： 赋值`CategoryID`和`SupplierID`参数

对于本教程假设，我们添加的新产品，通过此接口时的应用程序应将它分配`CategoryID`和`SupplierID`值为 1。 前面曾提到，ObjectDataSource 有一对预和后续级别事件的触发数据修改过程。 当其`Insert()`调用方法，首先将对象数据源引发其`Inserting`事件，然后调用的方法，其`Insert()`方法已映射到，并最后引发`Inserted`事件。 `Inserting`事件处理程序为我们提供了一个最后一个机会调整的输入的参数或取消操作结束。

> [!NOTE]
> 在实际应用程序中你可能想让用户指定的类别和供应商或将它们根据某些条件选取此值或业务逻辑 （而不是盲目地选择 ID 为 1）。 无论如何，该示例演示了如何以编程方式设置 ObjectDataSource 的预先级别事件从输入参数的值。


请花费片刻时间为 ObjectDataSource 的创建事件处理程序`Inserting`事件。 请注意，事件处理程序的第二个输入的参数是类型的对象`ObjectDataSourceMethodEventArgs`，其中包含要访问的参数集合的属性 (`InputParameters`) 和一个属性，以取消操作 (`Cancel`)。


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample10.vb)]

在此情况下，`InputParameters`属性包含 ObjectDataSource 的`InsertParameters`DetailsView 从分配的值的集合。 若要更改其中一个参数的值，只需使用： `e.InputParameters("paramName") = value`。 因此，若要设置`CategoryID`并`SupplierID`为 1 的值，调整`Inserting`事件处理程序如下所示：


[!code-vb[Main](examining-the-events-associated-with-inserting-updating-and-deleting-vb/samples/sample11.vb)]

此时间添加新产品 （例如 Acme Soda) 时`CategoryID`和`SupplierID`新产品的列将设置为 1 （请参阅图 20）。


[![新产品现在将具有其 CategoryID 和供应商 Id 为 1 的值集](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image56.png)

**图 20**： 新产品现在具有与其`CategoryID`并`SupplierID`的值设置为 1 ([单击以查看实际尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-vb/_static/image58.png))


## <a name="summary"></a>总结

在编辑、 插入和删除过程，数据 Web 控件和 ObjectDataSource 继续完成大量前期和后期级别事件。 在本教程中，我们检查预级别事件，已学习了如何使用这些自定义的输入的参数或取消数据修改操作完全同时从数据 Web 控件和对象数据源的事件。 在下一教程中我们将介绍创建和使用后级别事件的事件处理程序。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Jackie Goor 和 Liz Shulok。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](an-overview-of-inserting-updating-and-deleting-data-vb.md)
> [下一页](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
