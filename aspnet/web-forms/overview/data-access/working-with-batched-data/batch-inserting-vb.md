---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: 批插入 (VB) |Microsoft Docs
author: rick-anderson
description: 了解如何在单个操作中插入多个数据库记录。 在用户界面层中我们将扩展以允许用户输入多个 n GridView...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: 17a077ed0124a0a9e06c90d0ac137958693fc30e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390079"
---
<a name="batch-inserting-vb"></a>批量插入 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip)或[下载 PDF](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> 了解如何在单个操作中插入多个数据库记录。 在用户界面层我们扩展 GridView 以允许用户输入多个新记录。 数据访问层中，我们将以确保所有插入都成功，或者所有插入都将都回滚的事务中的多个插入操作。


## <a name="introduction"></a>介绍

在中[方式成批更新](batch-updating-vb.md)教程探讨了自定义 GridView 控件以呈现多个记录的可编辑的接口。 用户访问的页面无法进行一系列更改，然后，单击一次按钮，使用执行批处理更新。 用户通常更新一次性许多记录的情况下，此类接口可以节省无数次单击和键盘鼠标上下文切换为默认值进行比较时每行都首先返回进行了研究的编辑功能[插入、 更新和删除数据概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程。

添加记录时，还可以应用这一概念。 想象一下，这里 Northwind traders 我们通常接收发货从供应商所包含的特定类别的产品数量。 作为示例，我们可能会从东京 Traders 收到六个不同茶和 coffee 产品的发货。 如果用户输入的 DetailsView 控件通过一次一个的六个产品，它们将必须反复地选择许多相同的值： 它们将需要选择同一类别 （饮料） 同一个供应商 (东京 Traders)、 相同废止的值 （False)，和顺序值 (0) 上的相同单位。 此重复的数据项不是仅较长时间，但容易发生错误。

只要下一点功夫，我们可以创建一批插入接口，使用户能够选择供应商和类别一次，输入一系列的产品名称和单位价格，然后单击按钮以向数据库添加新的产品 （参见图 1）。 添加每个产品，其`ProductName`并`UnitPrice`数据字段分配了的文本框中输入的值时其`CategoryID`和`SupplierID`值从顶部 fo 窗体在 Dropdownlist 分配的值。 `Discontinued`并`UnitsOnOrder`值设置为硬编码值`False`和 0，分别。


[![批插入接口](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**图 1**: 批插入接口 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image3.png))


在本教程中我们将创建实现批处理插入接口中图 1 所示的页面。 作为与前面的两个教程，我们将包装插入事务以确保原子性的作用域内。 让我们来开始 ！

## <a name="step-1-creating-the-display-interface"></a>步骤 1： 创建显示接口

本教程将由一个页面，分为两个区域组成： 一个显示区域和插入的区域。 显示接口，我们将创建在此步骤中，在 GridView 中显示的产品，并包含标题为进程产品发货的按钮。 单击此按钮时，显示接口将被替换为插入的接口，这图 1 所示。 添加产品后返回从发货的显示界面，或单击取消按钮。 我们将在步骤 2 中创建插入接口。

当创建页有两个接口，一次可见时只有一个圆圈，每个接口通常放在[面板 Web 控件](http://www.w3schools.com/aspnet/control_panel.asp)，它可作为其他控件的容器。 因此，我们的页面将具有两个面板控件一个为每个接口。

首先打开`BatchInsert.aspx`页中`BatchData`文件夹，然后拖动一个面板从工具箱拖到设计器 （请参见图 2）。 设置面板 s`ID`属性设置为`DisplayInterface`。 在将面板添加到设计器中，其`Height`和`Width`属性分别设置为 50px 和 125px。 清除这些属性值从属性窗口。


[![将面板拖到设计器工具箱中](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**图 2**： 将面板拖到设计器工具箱中 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image6.png))


接下来，将按钮和 GridView 控件拖到面板。 设置按钮 s`ID`属性设置为`ProcessShipment`并将其`Text`与进程产品发货的属性。 设置 GridView s`ID`属性设置为`ProductsGrid`并从其智能标记，请将其绑定到名为新 ObjectDataSource `ProductsDataSource`。 配置对象数据源以提取其数据从`ProductsBLL`类的`GetProducts`方法。 由于此 GridView 仅用于显示数据，设置下拉列表中插入、 更新和删除选项卡添加到 （无）。 单击完成以完成配置数据源向导。


[![显示从 ProductsBLL 类的 GetProducts 方法返回的数据](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**图 3**： 显示从返回的数据`ProductsBLL`类 s`GetProducts`方法 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image9.png))


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**图 4**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image12.png))


完成 ObjectDataSource 向导后，Visual Studio 将添加 BoundFields 和产品数据字段 CheckBoxField。 删除所有除`ProductName`， `CategoryName`， `SupplierName`， `UnitPrice`，和`Discontinued`字段。 随意调整美观的任何自定义。 我决定要设置格式`UnitPrice`作为货币值的字段重新排序字段，并且重命名的若干字段`HeaderText`值。 此外配置 GridView，其中包括分页和排序支持的 GridView s 智能标记启用分页和启用排序复选框。

以后添加面板、 按钮、 GridView 和 ObjectDataSource 控件和自定义 GridView 的字段，您的页面 + s 声明性标记看起来应类似于下面：


[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

请注意，按钮和 GridView 的标记出现在打开和关闭`<asp:Panel>`标记。 由于这些控件是内`DisplayInterface`面板中，我们可以隐藏起来，方法只需设置面板 s`Visible`属性设置为`False`。 步骤 3 所示在以编程方式更改面板的`Visible`属性以响应一个按钮单击此项可显示同时隐藏了另一个接口。

花点时间查看我们通过浏览器的进度。 图 5 所示，你应该看到一个 GridView，一次列出产品十个以上的进程，产品交付按钮。


[![GridView 列出的产品并提供排序和分页功能](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**图 5**: GridView 列出的产品并提供了排序和分页功能 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image15.png))


## <a name="step-2-creating-the-inserting-interface"></a>步骤 2： 创建插入接口

显示界面完成后，我们准备就绪后，若要创建插入接口。 对于本教程，让我们来创建一个插入接口来提示输入一个单一的供应商和类别值，然后允许用户输入最多五个产品名称和单位价格值。 与此接口，用户可以添加一到五个新产品的所有共享相同的类别和供应商，但具有唯一的产品名称和价格。

通过从工具箱拖到设计器中，将其放在现有下面拖动面板开始`DisplayInterface`面板。 设置`ID`属性的新添加到面板`InsertingInterface`并设置其`Visible`属性设置为`False`。 我们将添加代码，用于设置`InsertingInterface`面板 s`Visible`属性设置为`True`在步骤 3 中。 清除面板 s 还`Height`和`Width`属性值。

接下来，我们需要创建插入回中图 1 所示的接口。 此接口可创建通过一系列 HTML 技术，但我们将使用一个非常简单： 四个列、 七行的表。

> [!NOTE]
> 输入 HTML 标记时`<table>`元素，我更喜欢使用源视图。 虽然 Visual Studio 具有用于添加的工具`<table>`通过设计器的元素，在设计器似乎所有太愿意注入未经请求的`style`到标记的设置。 当我创建了后`<table>`标记中，我通常返回到设计器添加 Web 控件并设置其属性。 创建包含预先确定的列和行的表时我更愿意使用静态 HTML 而非[Table Web 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx)因为任何放置在表 Web 控件中的 Web 控件只能访问使用`FindControl("controlID")`模式。 我执行操作，但是，用于表 Web 控件动态调整大小表 （其行或列根据一些数据库或用户指定的条件的），因为表 Web 控件可用于以编程方式构造。


输入中的以下标记`<asp:Panel>`标记的`InsertingInterface`面板：


[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

这`<table>`标记不包含任何 Web 控件，但我们将添加那些暂时不可用。 请注意，每个`<tr>`元素包含特定的 CSS 类设置：`BatchInsertHeaderRow`标题行的供应商和类别 Dropdownlist 将在哪里;`BatchInsertFooterRow`发货和取消按钮中的添加产品将在哪里; 的脚注行和交替`BatchInsertRow`和`BatchInsertAlternatingRow`值将包含的产品和单元的行的价格文本框控件。 我制作了相应的 CSS 类中`Styles.css`文件以使插入接口具有的外观类似于 GridView 和 DetailsView 控件我们 ve 整个这些教程中使用。 下面显示了这些 CSS 类。


[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

与此输入的标记返回到设计视图。 这`<table>`应显示为设计器中的四列、 七行的表，如图 6 所示。


[![插入接口组成的四列七行的表](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**图 6**: 插入接口由四个列七行的表的 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image18.png))


我们重新现在可以随时将 Web 控件添加到插入的接口。 将两个 Dropdownlist 从工具箱拖到表一用于供应商，另一个类别中的相应单元格。

设置供应商 DropDownList s`ID`属性设置为`Suppliers`并将其绑定到名为新 ObjectDataSource `SuppliersDataSource`。 配置要检索其数据的新 ObjectDataSource`SuppliersBLL`类的`GetSuppliers`方法，设置更新选项卡上为 （无） s 下拉列表。 单击完成以完成向导。


[![配置对象数据源使用 SuppliersBLL 类的 GetSuppliers 方法](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**图 7**： 配置为使用 ObjectDataSource`SuppliersBLL`类 s`GetSuppliers`方法 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image21.png))


具有`Suppliers`DropDownList 显示`CompanyName`数据字段并使用`SupplierID`数据字段作为其`ListItem`的值。


[![显示公司名称数据字段，并作为值使用供应商 Id](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**图 8**： 显示`CompanyName`数据字段并使用`SupplierID`作为值 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image24.png))


命名第二个 DropDownList`Categories`并将其绑定到名为新 ObjectDataSource `CategoriesDataSource`。 配置`CategoriesDataSource`若要使用的 ObjectDataSource`CategoriesBLL`类的`GetCategories`方法; 将设置下拉列表列出了在 UPDATE 和 DELETE 选项卡添加到 （无） 单击完成以完成向导。 最后，使 DropDownList 显示`CategoryName`数据字段并使用`CategoryID`作为值。

已添加这些两个 Dropdownlist 并将其绑定到适当的已配置 Objectdatasource 后，屏幕应类似于图 9。


[![标头行现在包含供应商和类别 Dropdownlist](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**图 9**: 标头行现在包含`Suppliers`并`Categories`Dropdownlist ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image27.png))


我们现在需要创建要收集的名称和每个新的产品价格的文本框。 将 TextBox 控件从工具箱拖到设计器为每个五个产品名称和价格行。 设置`ID`到文本框的属性`ProductName1`， `UnitPrice1`， `ProductName2`， `UnitPrice2`， `ProductName3`， `UnitPrice3`，依次类推。

单位价格文本框中，设置每轮之后添加 CompareValidator`ControlToValidate`属性设置为相应`ID`。 此外设置`Operator`属性设置为`GreaterThanEqual`，`ValueToCompare`为 0，并且`Type`到`Currency`。 这些设置指示 CompareValidator 以确保价格，如果输入，大于或等于零的有效货币值。 设置`Text`属性设置为\*，和`ErrorMessage`价格必须是大于或等于零。 此外，请省略任何货币符号。

> [!NOTE]
> 插入的接口不包括任何 RequiredFieldValidator 控件，即使`ProductName`字段中`Products`数据库表不允许`NULL`值。 这是因为我们想要让用户输入最多五个产品。 例如，如果用户已为前三个行提供的产品名称和单位价格，将最后两行留空，d 我们只需添加三个新产品到系统。 由于`ProductName`是必需的但是，我们将需要以编程方式检查以确保如果单位价格输入提供相应的产品名称值。 我们将解决在步骤 4 中的此检查。


验证用户的输入，CompareValidator 报告这些无效数据，如果值包含货币符号。 添加 $ 前面每单位价格文本框作为一个视觉提示，指示用户输入价格时省略的货币符号。

最后，将添加验证摘要控件内的`InsertingInterface`面板中，设置其`ShowMessageBox`属性设置为`True`并将其`ShowSummary`属性设置为`False`。 使用这些设置，如果用户输入无效的单位价格值，将有问题的文本框控件旁边将出现一个星号和 ValidationSummary 将显示一个显示我们在前面指定的错误消息的客户端的消息框。

此时，你的屏幕应类似于图 10。


[![插入的接口现在包含文本框的产品名称和价格](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**图 10**: 插入接口现在包含文本框的产品名称和价格 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image30.png))


接下来我们需要将添加产品发货和取消按钮添加到的脚注行。 将两个按钮控件从工具箱插入页脚插入接口，设置按钮`ID`属性设置为`AddProducts`并`CancelButton`和`Text`属性分别从发货和取消，添加产品。 此外，设置`CancelButton`控制 s`CausesValidation`属性设置为`false`。

最后，我们需要添加将显示两个接口的状态消息的标签 Web 控件。 例如，当用户已成功添加一批新的产品，我们想要返回到显示接口并显示一条确认消息。 如果，但是，用户提供价格为的新产品，但不关闭产品名称的改变，我们需要显示一条警告消息，因为`ProductName`字段为必填项。 因为我们需要针对这两个接口显示此消息，请将其放置在外部面板页的顶部。

将标签 Web 控件从工具箱拖到设计器中页的顶部。 设置`ID`属性设置为`StatusLabel`，清除出`Text`属性，并设置`Visible`并`EnableViewState`属性设置为`False`。 如我们在前面的教程所见，设置`EnableViewState`属性设置为`False`使我们能够以编程方式更改标签的属性值并将它们自动还原为其默认值在后续回发。 这简化了用于显示状态消息的响应将在后续回发时消失某些用户操作的代码。 最后，设置`StatusLabel`控制 s`CssClass`中定义的警告，这是 CSS 类的名称的属性`Styles.css`以大型、 斜体、 粗体、 红色字体显示文本。

添加标签并将其配置之后，图 11 显示了 Visual Studio 设计器。


[![将两个面板控件上方的 statuslabel 设置控件](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**图 11**： 位置`StatusLabel`控制上面两个面板控件 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image33.png))


## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>步骤 3： 显示之间切换和插入界面

现在我们已经为我们显示和插入两个任务仍会余下接口，但我们重新完成标记：

- 在显示之间切换和插入界面
- 发货再转为在数据库中添加产品

目前，显示接口是可见，但插入接口处于隐藏状态。 这是因为`DisplayInterface`面板 s`Visible`属性设置为`True`（默认值），而`InsertingInterface`面板 s`Visible`属性设置为`False`。 我们只需切换 s 的每个控件的两个接口之间进行切换`Visible`属性值。

我们想要从转为显示接口插入接口过程产品发货按钮。 因此，此按钮 s 为创建事件处理程序`Click`事件，其中包含以下代码：


[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

此代码只是隐藏`DisplayInterface`面板并显示`InsertingInterface`面板。

接下来，为插入的界面中的发货和取消按钮控件中的添加产品创建事件处理程序。 单击任一按钮时，我们需要还原到显示接口。 创建`Click`两个事件处理程序按钮的控件，使它们调用`ReturnToDisplayInterface`，我们将暂时不可用的方法。 除了隐藏`InsertingInterface`面板，显示`DisplayInterface`面板中，`ReturnToDisplayInterface`方法需要返回到其预先编辑状态的 Web 控件。 这涉及到设置 Dropdownlist`SelectedIndex`属性设置为 0 和清除`Text`文本框控件的属性。

> [!NOTE]
> 可能会发生什么情况，请考虑如果我们无效 t 返回到显示接口之前将控件返回到其预先编辑状态。 用户可能会单击进程，产品交付按钮，输入从发货的产品，然后单击添加从发货的产品。 这会将产品添加并将用户返回到显示接口。 此时，用户可能想要添加另一次寄。 单击它们将返回到插入接口，但 DropDownList 的过程，产品交付按钮时选择和文本框值仍会使用其以前的值填充。


[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

这两`Click`事件处理程序只需调用`ReturnToDisplayInterface`方法，尽管我们将返回到添加产品从发货`Click`步骤 4 中的事件处理程序，并添加代码以保存。 `ReturnToDisplayInterface` 首先会返回`Suppliers`和`Categories`Dropdownlist 其第一个选项。 两个常量`firstControlID`并`lastControlID`标记的起始和结束命名文本框中插入接口，并使用的边界中的的产品名称和单位价格中使用的控件索引值`For`设置循环`Text`文本框控件的属性返回空字符串。 最后，面板`Visible`属性重置，以便隐藏插入界面和所示的显示界面。

请花费片刻时间来查看此页在浏览器中测试。 首次访问页面时可看到显示接口，如图 5 中所示。 单击进程，产品交付按钮。 页面将回发，如图 12 中所示，现在应看到插入接口。 单击任一添加中的产品发货或取消按钮返回到显示接口。

> [!NOTE]
> 在查看插入的接口，请花费片刻时间的单位价格文本框上 CompareValidators 测试。 应会看到一个警告，单击发货按钮具有无效的货币值或值小于零的价格中的添加产品的客户端的 messagebox。


[![单击处理产品发货按钮后显示的插入界面](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**图 12**： 单击处理产品发货按钮后显示插入的界面 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image36.png))


## <a name="step-4-adding-the-products"></a>步骤 4： 添加产品

保持本教程是从发货按钮 s 保存到数据库中添加产品的产品的所有`Click`事件处理程序。 这可以通过创建`ProductsDataTable`并添加`ProductsRow`提供的产品名称的每个实例。 一次这些`ProductsRow`中添加了我们将调用`ProductsBLL`类 s`UpdateWithTransaction`方法并传入`ProductsDataTable`。 请记住，`UpdateWithTransaction`方法，它返回中创建[包装事务内的数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)教程中，传递`ProductsDataTable`到`ProductsTableAdapter`s`UpdateWithTransaction`方法。 在这里，ADO.NET 事务中启动和 TableAdatper 问题`INSERT`数据库中为每个添加到语句`ProductsRow`DataTable 中。 假定所有产品都添加未生成错误，则在提交事务，否则它将回滚。

用于从发货按钮 s 添加产品代码`Click`事件处理程序还需要执行一些错误检查。 由于没有任何 RequiredFieldValidators 插入接口中使用，则用户可以输入价格为的产品时省略其名称。 由于产品的名称是必需的如果此类情况展开需要提醒用户，并不继续执行插入操作。 完整`Click`事件处理程序代码如下所示：


[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

事件处理程序首先会确保`Page.IsValid`属性返回的值为`True`。 如果它返回`False`、 然后这意味着一个或多个 CompareValidators 报告无效的数据; 我们不希望在此情况下尝试插入的输入的产品或我们就会引发异常时尝试分配的用户输入的单位价格值设置为`ProductsRow`s`UnitPrice`属性。

接下来，一个新`ProductsDataTable`创建实例 (`products`)。 一个`For`循环用于循环访问产品名称和单位价格文本框和`Text`属性读取到的本地变量`productName`和`unitPrice`。 如果用户输入一个值的单位价格为而不是相应的产品名称，`StatusLabel`显示的消息，如果提供一个单位价格您还必须包括的产品名称和退出事件处理程序。

如果已提供的产品名称，一个新`ProductsRow`使用创建实例`ProductsDataTable`s`NewProductsRow`方法。 这一新`ProductsRow`实例 s`ProductName`属性设置为当前的产品名称文本框时`SupplierID`并`CategoryID`属性分配给`SelectedValue`Dropdownlist 插入接口 s 标头中的属性。 如果用户输入的产品的价格的值，则将它分配给`ProductsRow`实例 s`UnitPrice`属性; 否则，该属性是左侧未分配值，这将导致`NULL`值`UnitPrice`数据库中。 最后，`Discontinued`并`UnitsOnOrder`属性分配给硬编码值`False`和 0，分别。

为分配了属性后`ProductsRow`实例添加到`ProductsDataTable`。

在完成`For`循环中，我们将检查是否已添加的任何产品。 用户可能，毕竟，单击进入任何产品名称或价格之前的发货中的添加产品。 如果在至少一个产品`ProductsDataTable`，则`ProductsBLL`类的`UpdateWithTransaction`调用方法。 将数据重新绑定到接下来， `ProductsGrid` GridView，以便显示界面中显示新添加的产品。 `StatusLabel`更新为显示一条确认消息和`ReturnToDisplayInterface`隐藏插入接口和显示显示接口的调用。

如果未不输入任何产品，插入接口仍然显示但没有产品已添加的消息。 请输入产品名称，并显示在文本框中的单位价格。

图的 13、 14 和 15 显示插入，在操作中显示接口。 在图 13 中，用户输入的单位价格值没有相应的产品名称。 图 14 显示了显示界面后三个新产品已成功添加，虽然图 15 显示了两个新添加的产品 GridView （第三个是前一页） 中。


[![产品名称是所需时输入的单位价格](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**图 13**: 产品名称是所需时输入的单位价格 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image39.png))


[![供应商添加了三个新 Veggies Mayumi s](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**图 14**： 三个新 Veggies 中添加了供应商 Mayumi s ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image42.png))


[![可以在 GridView 的最后一页中找到的新产品](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**图 15**: 新产品可在 GridView 的最后一页 ([单击以查看实际尺寸的图像](batch-inserting-vb/_static/image45.png))


> [!NOTE]
> 批插入本教程中使用的逻辑包装在事务的作用域内插入。 若要验证这一点，故意引入一个数据库级错误。 例如，而不必分配新`ProductsRow`实例 s`CategoryID`属性设置为在所选值`Categories`下拉列表中，分配到一个值，如`i * 5`。 此处`i`循环索引器，且是介于 1 到 5 的值。 因此，当添加两个或多个产品在批处理中的插入的第一个产品必须是有效`CategoryID`将具有值 (5)，但后续产品`CategoryID`最多不匹配的值`CategoryID`中的值以`Categories`表。 净效果是，同时第一`INSERT`将成功，但后续条件将因违反外键约束。 由于批插入是原子的因此第一个`INSERT`将被回滚，返回到之前批插入过程的状态数据库中，开始。


## <a name="summary"></a>总结

这和前面的两个教程中我们已创建接口，以便在更新，允许删除和插入数据的批处理，这些用于添加到数据访问层中的事务支持[包装数据库修改在事务内](wrapping-database-modifications-within-a-transaction-vb.md)教程。 对于某些情况下，此类批处理处理用户界面极大地提高最终用户效率通过降低数次单击、 回发和键盘鼠标上下文切换，同时还能保留的基础数据的完整性。

本教程中完成我们了解了如何使用批处理的数据。 下一组教程探讨了各种高级数据访问层方案，包括使用存储的过程在 TableAdapter 的方法中，在 DAL、 加密连接字符串和的详细信息中配置连接和命令级别的设置 ！

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程是 Hilton giesenow 为您和 S ren Jacob Lauritsen 导致审阅者。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](batch-deleting-vb.md)
