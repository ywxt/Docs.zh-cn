---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
title: 自定义 DataList 的编辑界面 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将创建更丰富的编辑界面 DataList，包括 Dropdownlist 和一个复选框。
ms.author: aspnetcontent
ms.date: 10/30/2006
ms.assetid: a5d13067-ddfb-4c36-8209-0f69fd40e45c
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: c76e3bc46c7d38140320834a27ec7710d289e7d3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826113"
---
<a name="customizing-the-datalists-editing-interface-c"></a>自定义 DataList 的编辑界面 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_CS.exe)或[下载 PDF](customizing-the-datalist-s-editing-interface-cs/_static/datatutorial40cs1.pdf)

> 在本教程中我们将创建更丰富的编辑界面 DataList，包括 Dropdownlist 和一个复选框。


## <a name="introduction"></a>介绍

标记和 DataList s 中的 Web 控件`EditItemTemplate`定义其编辑界面。 在所有可编辑的 DataList 示例中我们 ve 检查到目前为止，可编辑界面组成文本框 Web 控件。 在中[前面的教程](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)我们改进了通过添加验证控件的编辑时的用户体验。

`EditItemTemplate`可以进一步扩展到包括文本框中，如 Dropdownlist，RadioButtonLists，日历之外的 Web 控件等。 与文本框中，自定义以包括其他 Web 控件的编辑界面时，使用以下步骤：

1. 将 Web 控件添加到`EditItemTemplate`。
2. 使用数据绑定语法将相应的数据字段值分配给相应的属性。
3. 在`UpdateCommand`事件处理程序，以编程方式访问 Web 控制值并将其传递到适当的 BLL 方法。

在本教程中我们将创建更丰富的编辑界面 DataList，包括 Dropdownlist 和一个复选框。 具体而言，我们将创建 DataList，列出产品信息并允许 s 产品名称、 供应商、 类别和已停止使用的状态要更新 （请参阅图 1）。


[![编辑接口包含一个文本框中，两个 Dropdownlist 和一个复选框](customizing-the-datalist-s-editing-interface-cs/_static/image2.png)](customizing-the-datalist-s-editing-interface-cs/_static/image1.png)

**图 1**： 编辑接口包含一个文本框中，两个 Dropdownlist 和一个复选框 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image3.png))


## <a name="step-1-displaying-product-information"></a>步骤 1： 显示产品信息

我们可以创建 DataList s 可编辑接口之前，我们首先需要生成只读接口。 首先打开`CustomizedUI.aspx`页上，从`EditDeleteDataList`文件夹并从设计器中，将 DataList 添加到页上，设置其`ID`属性设置为`Products`。 从 DataList s 智能标记，创建新对象数据源。 命名此新 ObjectDataSource`ProductsDataSource`并将其配置为从`ProductsBLL`类的`GetProducts`方法。 作为上一个可编辑 DataList 教程中，我们将更新已编辑的产品的信息直接转到业务逻辑层。 相应地，设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![设置为 （无） 的更新、 插入和删除选项卡下拉列表](customizing-the-datalist-s-editing-interface-cs/_static/image5.png)](customizing-the-datalist-s-editing-interface-cs/_static/image4.png)

**图 2**： 将更新、 插入和删除选项卡下拉列表设置为 （无） ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image6.png))


在配置后 ObjectDataSource，Visual Studio 将创建默认值`ItemTemplate`DataList，来列出每个数据字段的名称和值返回。 修改`ItemTemplate`，以便在模板列表中的产品名称`<h4>`元素和类别名称、 供应商名称、 价格和已停止使用的状态。 此外，添加一个编辑按钮，并确保其`CommandName`属性设置为编辑。 声明性标记我`ItemTemplate`后面：


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

上述标记使用产品信息的布局&lt;h4&gt;产品的名称和四个列标题`<table>`其余字段。 `ProductPropertyLabel`并`ProductPropertyValue`中定义的 CSS 类`Styles.css`，在前面的教程讨论了。 图 3 显示了我们的浏览器查看时的进度。


[![显示名称、 供应商、 类别、 停用状态和每个产品的价格](customizing-the-datalist-s-editing-interface-cs/_static/image8.png)](customizing-the-datalist-s-editing-interface-cs/_static/image7.png)

**图 3**： 显示名称、 供应商、 类别、 停用状态和每个产品的价格 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image9.png))


## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>步骤 2： 将 Web 控件添加到编辑界面

构建自定义的 DataList 的编辑界面是添加到所需的 Web 控件的第一步`EditItemTemplate`。 具体而言，我们需要 DropDownList 的类别，另一个用于供应商，并已停止使用的状态的复选框。 由于产品的价格不在此示例中可编辑，我们可以继续使用标签 Web 控件中显示。

若要自定义编辑界面，请单击 DataList s 智能标记中的编辑模板链接并选择`EditItemTemplate`从下拉列表选项。 添加到 DropDownList`EditItemTemplate`并设置其`ID`到`Categories`。


[![将 DropDownList 添加类别](customizing-the-datalist-s-editing-interface-cs/_static/image11.png)](customizing-the-datalist-s-editing-interface-cs/_static/image10.png)

**图 4**： 将 DropDownList 添加类别 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image12.png))


接下来，从 DropDownList s 智能标记，选择选择数据源选项并创建名为新 ObjectDataSource `CategoriesDataSource`。 配置要使用此 ObjectDataSource`CategoriesBLL`类的`GetCategories()`方法 （请参见图 5）。 接下来，DropDownList 的数据源配置向导提示输入要用于每个数据字段`ListItem`s`Text`和`Value`属性。 使 DropDownList 显示`CategoryName`数据字段并使用`CategoryID`作为值，如图 6 中所示。


[![创建名为 CategoriesDataSource 新 ObjectDataSource](customizing-the-datalist-s-editing-interface-cs/_static/image14.png)](customizing-the-datalist-s-editing-interface-cs/_static/image13.png)

**图 5**： 创建新对象数据源命名`CategoriesDataSource`([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image15.png))


[![配置 DropDownList 的显示和数值字段](customizing-the-datalist-s-editing-interface-cs/_static/image17.png)](customizing-the-datalist-s-editing-interface-cs/_static/image16.png)

**图 6**： 配置 DropDownList 的显示和值字段 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image18.png))


重复这一系列的步骤为供应商创建 DropDownList。 设置`ID`用于向此 DropDownList`Suppliers`并将命名其 ObjectDataSource `SuppliersDataSource`。

添加后两个 Dropdownlist，添加已停止使用的状态的复选框和文本框的产品的名称。 设置`ID`复选框的文本框中的为`Discontinued`和`ProductName`分别。 添加一个 RequiredFieldValidator 以确保用户提供的产品的名称值。

最后，添加更新和取消按钮。 请记住，这两个按钮是命令性，其`CommandName`属性设置为更新以及取消，分别。

你的喜好的接口，可随时进行布局的编辑。 我已选择使用相同的四列`<table>`布局从只读接口，作为以下声明性语法和屏幕截图演示了：


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample2.aspx)]


[![编辑界面将列出输出如只读接口](customizing-the-datalist-s-editing-interface-cs/_static/image20.png)](customizing-the-datalist-s-editing-interface-cs/_static/image19.png)

**图 7**: 编辑界面是列出出像只读接口一样 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image21.png))


## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>步骤 3： 创建 EditCommand 和 CancelCommand 事件处理程序

目前，没有在数据绑定语法`EditItemTemplate`(除了`UnitPriceLabel`，这按原样从复制`ItemTemplate`)。 我们将暂时不可用，添加数据绑定语法，但第一个让的 DataList s 为创建事件处理程序`EditCommand`和`CancelCommand`事件。 请记住的责任`EditCommand`事件处理程序来呈现其编辑按钮被单击，DataList 项的编辑界面，而`CancelCommand`的作业是要为其预编辑状态返回 DataList。

创建以下两个事件处理程序，并让他们使用以下代码：


[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample3.cs)]

使用这些两个事件处理程序中的位置，单击编辑按钮显示的编辑界面，并单击取消按钮返回到其只读模式下编辑的项。 图 8 显示了 DataList 后 Chef Anton s 秋葵组合已单击编辑按钮。 由于我们 ve 目前进行的编辑界面，添加任何数据绑定语法`ProductName`文本框中为空白，`Discontinued`从中选择复选框未选中和第一个项`Categories`和`Suppliers`Dropdownlist。


[![单击编辑按钮显示的编辑界面](customizing-the-datalist-s-editing-interface-cs/_static/image23.png)](customizing-the-datalist-s-editing-interface-cs/_static/image22.png)

**图 8**： 单击编辑按钮将显示编辑界面 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image24.png))


## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>步骤 4： 将数据绑定语法添加到编辑界面

若要显示的当前产品的值的编辑界面，我们需要使用数据绑定语法将数据字段值指定为适当的 Web 控件值。 可以通过转到编辑模板屏幕设计器通过应用的数据绑定语法，并选择编辑 DataBindings 链接从 Web 控制智能标记。 或者，数据绑定语法可以直接添加到声明性标记。

分配`ProductName`数据字段值`ProductName`文本框 s`Text`属性，`CategoryID`并`SupplierID`数据字段值与`Categories`和`Suppliers`Dropdownlist`SelectedValue`属性，并`Discontinued`数据字段值`Discontinued`复选框的`Checked`属性。 进行这些更改，通过在设计器或直接通过声明性标记之后, 重新访问通过浏览器页并单击 Chef Anton s 秋葵汤编辑按钮。 如图 9 所示，数据绑定语法已添加到 TextBox、 Dropdownlist 和复选框中的当前值。


[![单击编辑按钮显示的编辑界面](customizing-the-datalist-s-editing-interface-cs/_static/image26.png)](customizing-the-datalist-s-editing-interface-cs/_static/image25.png)

**图 9**： 单击编辑按钮将显示编辑界面 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image27.png))


## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>步骤 5： 将用户的更改保存在 UpdateCommand 事件处理程序

当用户编辑产品并单击更新按钮，产生的回发和 DataList 的`UpdateCommand`事件触发。 在事件处理程序中，我们需要能够读取的值中的 Web 控件从`EditItemTemplate`并与 BLL 来更新数据库中的产品。 正如我们在前面的教程，了解 ve`ProductID`的更新的产品是可通过访问`DataKeys`集合。 用户输入字段通过以编程方式引用使用的 Web 控件访问`FindControl("controlID")`，如下面的代码所示：


[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample4.cs)]

代码首先咨询`Page.IsValid`属性以确保页面上的所有验证控件有效。 如果`Page.IsValid`是`True`，编辑的产品 s`ProductID`值从读取`DataKeys`收集和 Web 控件中的数据条目`EditItemTemplate`以编程方式引用。 接下来，将从这些 Web 控件的值读取到变量，然后传递到相应`UpdateProduct`重载。 在更新后的数据，DataList 回到其预先编辑状态。

> [!NOTE]
> 我已省略了异常处理逻辑中添加[处理 BLL-和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-cs.md)为了使代码和此示例的教程已设定焦点。 作为一个练习，完成本教程后添加此功能。


## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>步骤 6： 处理 NULL CategoryID 和供应商 Id 值

Northwind 数据库中允许`NULL`值为`Products`表 s`CategoryID`和`SupplierID`列。 但是，我们编辑接口没有 t 当前适应`NULL`值。 如果我们尝试编辑的产品的`NULL`值是其`CategoryID`或`SupplierID`列，我们将得到`ArgumentOutOfRangeException`具有类似的错误消息：*类别具有无效，因为它执行的 SelectedValue中的项列表不存在。* 此外，有 s 目前没有办法更改产品的类别或供应商值从非`NULL`值设为`NULL`之一。

若要支持`NULL`类别和供应商 Dropdownlist 的值，我们需要添加其他`ListItem`。 我选择使用 （无） 作为 ve`Text`值为`ListItem`，但您可以如 d 将其更改为其他内容 （如空字符串）。 最后，请别忘记设置 Dropdownlist`AppendDataBoundItems`到`True`; 如果你忘记了为此，请将类别并绑定到 DropDownList 的供应商将覆盖静态地添加`ListItem`。

进行这些更改，DataList s 中的 Dropdownlist 标记之后`EditItemTemplate`应如下所示：


[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> 静态`ListItem`s 可以添加到 DropDownList 通过设计器或直接通过声明性语法。 添加表示数据库的 DropDownList 项时`NULL`值时，请务必添加`ListItem`通过声明性语法。 如果您使用`ListItem`集合编辑器中在设计器中，将忽略生成的声明性语法`Value`完全设置何时分配一个空字符串，创建类似的声明性标记： `<asp:ListItem>(None)</asp:ListItem>`。 虽然这可能看起来无害，缺少`Value`导致要使用 DropDownList`Text`来代替属性值。 这意味着，如果这`NULL``ListItem`是选择，值 （无），将尝试分配给产品数据字段 (`CategoryID`或`SupplierID`，在本教程中)，这将导致异常。 通过显式设置`Value=""`、 一个`NULL`值将分配给该产品的数据字段`NULL``ListItem`处于选中状态。


花点时间查看我们通过浏览器的进度。 在编辑某个产品时，请注意，`Categories`和`Suppliers`Dropdownlist 这两个具有 （无） 开始处的 DropDownList 的选项。


[![类别和供应商 Dropdownlist 包括 （无） 选项](customizing-the-datalist-s-editing-interface-cs/_static/image29.png)](customizing-the-datalist-s-editing-interface-cs/_static/image28.png)

**图 10**:`Categories`并`Suppliers`Dropdownlist 包括 （无） 选项 ([单击以查看实际尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image30.png))


若要保存 (None) 选项作为数据库`NULL`值，我们需要返回到`UpdateCommand`事件处理程序。 更改`categoryIDValue`并`supplierIDValue`变量是可以为 null 的整数，并将其分配一个值，而不`Nothing`仅当 DropDownList 的`SelectedValue`不为空字符串：


[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample6.cs)]

进行此更改后，值为`Nothing`将传递到`UpdateProduct`BLL 方法，如果用户选择了 （无） 选项的下拉列表中，它对应于任一`NULL`数据库值。

## <a name="summary"></a>总结

在本教程中我们已了解如何创建一个更复杂的 DataList 编辑界面，包含三个不同的输入的 Web 控件的 TextBox、 两个 Dropdownlist 和验证控件以及一个复选框。 在生成时编辑界面，步骤都而不考虑所使用的 Web 控件相同： 首先将 Web 控件添加到 DataList 的`EditItemTemplate`; 使用数据绑定语法将分配对应的数据字段值与相应的 Web控件属性;然后，在`UpdateCommand`事件处理程序，以编程方式访问的 Web 控件和其相应的属性，将其值传递到 BLL。

时是否创建用于编辑的界面，它只是文本框或一系列不同的 Web 控件的 s 组成，请务必正确处理数据库`NULL`值。 当考虑`NULL`s，它是命令性，仅未正确显示的现有`NULL`中编辑界面，但你的值提供一种用于将值标为`NULL`。 对于在 DataLists Dropdownlist，这通常意味着添加一个静态`ListItem`其`Value`属性显式设置为空字符串 (`Value=""`)，并添加一些代码到`UpdateCommand`事件处理程序，以确定是否`NULL``ListItem`选择。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Dennis Patterson、 David Suru 和 Randy Schmidt。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
> [下一页](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
