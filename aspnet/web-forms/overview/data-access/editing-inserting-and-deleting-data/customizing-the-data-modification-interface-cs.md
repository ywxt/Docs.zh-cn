---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs
title: 自定义数据修改界面 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将介绍如何自定义的接口的可编辑的 GridView，替换标准文本框和复选框控件 alternati...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 22e99600-8d18-4a94-a20e-a3a62bb63798
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: f7004192edd636f4660f3184c3e725a6bfda865c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831679"
---
<a name="customizing-the-data-modification-interface-c"></a>自定义数据修改界面 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_CS.exe)或[下载 PDF](customizing-the-data-modification-interface-cs/_static/datatutorial20cs1.pdf)

> 在本教程中我们将介绍如何自定义的接口的可编辑的 GridView，替换标准文本框和复选框控件替代输入的 Web 控件。


## <a name="introduction"></a>介绍

BoundFields CheckBoxFields GridView 和 DetailsView 控件使用简化的过程修改数据，因为其呈现只读的、 可编辑，以及可插入接口的能力。 这些接口可以呈现而无需添加任何其他声明性标记或代码。 但是，BoundField 和 CheckBoxField 的接口缺乏真实应用方案中，通常需要的可自定义性。 若要自定义 GridView 或我们需要改为使用 TemplateField DetailsView 中的可编辑或可插入接口。

在中[前面的教程](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)我们已了解如何通过添加验证 Web 控件自定义数据修改接口。 在本教程中我们将介绍如何自定义的实际数据集合 Web 控件，替换 BoundField 和 CheckBoxField 的标准文本框和复选框控件与其他输入 Web 控件。 具体而言，我们将构建可编辑的 GridView 允许产品的名称、 类别、 供应商和已停止使用的状态更新。 在编辑时的特定行，category 和 supplier 字段将呈现为 Dropdownlist 中,，它包含可用类别和供应商可供选择的组。 此外，我们将用替换 CheckBoxField 的默认复选框提供两个选项的 RadioButtonList 控件:"活动"和"停止"。


[![GridView 的编辑界面包括 Dropdownlist 和单选按钮](customizing-the-data-modification-interface-cs/_static/image2.png)](customizing-the-data-modification-interface-cs/_static/image1.png)

**图 1**： 的 GridView 编辑接口包括 Dropdownlist 和单选按钮 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image3.png))


## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>步骤 1： 创建相应`UpdateProduct`重载

在本教程中我们将生成可编辑的 GridView 允许编辑产品的名称、 类别、 供应商，并停用状态。 因此，我们需要`UpdateProduct`接受这些四类产品值由五个输入参数的重载以及`ProductID`。 在我们以前的重载，这样一个中所示：

1. 从指定的数据库中检索产品信息`ProductID`，
2. 更新`ProductName`， `CategoryID`， `SupplierID`，和`Discontinued`字段，并
3. 将更新请求发送到通过 TableAdapter 的 DAL`Update()`方法。

为简洁起见，用于该特定重载我省略了业务规则检查，以确保被标记为停止使用的产品不是唯一的产品及其供应商提供。 您添加它中，如果您愿意，或者，理想情况下，重构到一个单独的方法的逻辑。

下面的代码演示新`UpdateProduct`重载中`ProductsBLL`类：


[!code-csharp[Main](customizing-the-data-modification-interface-cs/samples/sample1.cs)]

## <a name="step-2-crafting-the-editable-gridview"></a>步骤 2： 创建可编辑的 GridView

使用`UpdateProduct`重载添加，我们已准备好创建我们可编辑的 GridView。 打开`CustomizedUI.aspx`页中`EditInsertDelete`文件夹并将 GridView 控件添加到设计器。 从 GridView 的智能标记，接下来，创建新对象数据源。 配置对象数据源以检索产品信息通过`ProductBLL`类的`GetProducts()`方法以及更新产品数据使用`UpdateProduct`我们刚刚创建的重载。 从 INSERT 和 DELETE 的选项卡，从下拉列表中选择 （无）。


[![配置对象数据源以使用刚刚创建的 UpdateProduct 重载](customizing-the-data-modification-interface-cs/_static/image5.png)](customizing-the-data-modification-interface-cs/_static/image4.png)

**图 2**： 配置为使用 ObjectDataSource`UpdateProduct`重载只是创建 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image6.png))


正如我们所见整个数据修改教程，将分配 Visual Studio 创建的 ObjectDataSource 的声明性语法`OldValuesParameterFormatString`属性设置为`original_{0}`。 此操作，当然，不适用于我们的业务逻辑层由于我们方法不需要原始`ProductID`中传递值。 因此，像我们所做在前面的教程，请花费片刻时间来从声明性语法中删除此属性分配，或相反，将此属性的值设置为`{0}`。

此更改后 ObjectDataSource 的声明性标记应如下所示：


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample2.aspx)]

请注意，`OldValuesParameterFormatString`删除属性，以及是否有`Parameter`中`UpdateParameters`为每个所需的输入参数的集合我们`UpdateProduct`重载。

虽然 ObjectDataSource 配置来更新产品值的一个子集，当前显示 GridView*所有*的产品字段。 花点时间编辑 GridView，以便：

- 它只包括`ProductName`， `SupplierName`， `CategoryName` BoundFields 和`Discontinued`CheckBoxField
- `CategoryName`并`SupplierName`要在其之前显示 （到左侧） 的字段`Discontinued`CheckBoxField
- `CategoryName`并`SupplierName`BoundFields'`HeaderText`属性分别设置为"类别"和"供应商"
- 支持编辑功能 （检查 GridView 的智能标记中的启用编辑复选框）

更改后，在设计器将类似于图 3 使用 GridView 的声明性语法如下所示。


[![从 GridView 中删除不必要的字段](customizing-the-data-modification-interface-cs/_static/image8.png)](customizing-the-data-modification-interface-cs/_static/image7.png)

**图 3**： 从 GridView 中删除不必要的字段 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image9.png))


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample3.aspx)]

此时已完成 GridView 的只读的行为。 查看数据时，每个产品中呈现为显示产品的名称、 类别、 供应商，GridView 中的行和停用状态。


[![GridView 的只读接口已完成](customizing-the-data-modification-interface-cs/_static/image11.png)](customizing-the-data-modification-interface-cs/_static/image10.png)

**图 4**： 的 GridView 只读接口已完成 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image12.png))


> [!NOTE]
> 如中所述[教程中概述的插入、 更新和删除数据](an-overview-of-inserting-updating-and-deleting-data-cs.md)，它是极其重要的 GridView 的视图状态是启用 （默认行为）。 如果设置 GridView s`EnableViewState`属性设置为`false`，运行的并发用户无意中删除或编辑记录风险。 请参阅[警告： 禁用并发问题与 ASP.NET 2.0 Gridview/DetailsView/FormViews 该支持编辑和/或删除和其视图状态](http://scottonwriting.net/sowblog/posts/10054.aspx)有关详细信息。


## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>步骤 3： 使用 DropDownList 的类别和供应商编辑接口

请记住，`ProductsRow`对象包含`CategoryID`， `CategoryName`， `SupplierID`，并`SupplierName`属性，其中提供实际的外键 ID 值中`Products`数据库表和相应`Name`中的值`Categories`和`Suppliers`表。 `ProductRow`的`CategoryID`并`SupplierID`可以同时进行读取和写入，而`CategoryName`和`SupplierName`属性标记为只读。

由于的只读状态`CategoryName`并`SupplierName`属性，必须相应 BoundFields 其`ReadOnly`属性设置为`true`，防止这些值被修改时编辑一个行。 虽然我们可以设置`ReadOnly`属性设置为`false`、 呈现`CategoryName`和`SupplierName`BoundFields 期间编辑的文本框，这种方法将导致引发异常时，用户尝试更新的产品，因为没有任何`UpdateProduct`采用的重载`CategoryName`和`SupplierName`输入。 事实上，我们不想创建此类重载有两个原因：

- `Products`表中没有`SupplierName`或`CategoryName`字段，但`SupplierID`和`CategoryID`。 因此，我们希望我们的方法来传递这些特定的 ID 值，不是其查找表的值。
- 要求用户键入的供应商或类别的名称是不太理想，因为它需要用户了解可用的类别和供应商和其正确拼写。

供应商和类别字段应显示该类别和供应商的名称在只读模式下 （就像现在） 和适用的选项编辑时的下拉列表。 使用下拉列表，最终用户可以快速查看哪些类别和供应商的可用于在其中进行选择和的详细信息可以轻松地做出其选择。

若要提供此行为，我们需要转换`SupplierName`和`CategoryName`BoundFields Templatefield 到其`ItemTemplate`发出`SupplierName`并`CategoryName`值和它的`EditItemTemplate`使用 DropDownList 控件到列表可用类别和供应商。

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>添加`Categories`和`Suppliers`Dropdownlist

通过转换启动`SupplierName`和`CategoryName`到通过 Templatefield BoundFields： 单击 GridView 的智能标记中的编辑列链接; 从左下方; 列表中选择 BoundField 并单击"将此字段转换TemplateField"链接。 转换过程将创建两个 TemplateField`ItemTemplate`和一个`EditItemTemplate`，下面的声明性语法中所示：


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample4.aspx)]

因为 BoundField 已标记为只读的同时`ItemTemplate`并`EditItemTemplate`包含标签 Web 控件`Text`属性绑定到适用的数据字段 (`CategoryName`，上面的语法中)。 我们需要修改`EditItemTemplate`，替换 DropDownList 控件标签 Web 控件。

如我们在前面的教程所见，可以通过设计器或直接从声明性语法编辑模板。 若要通过设计器中编辑它，请单击 GridView 的智能标记中的编辑模板链接并选择使用类别字段`EditItemTemplate`。 删除标签 Web 控件并替换 DropDownList 控件，将 DropDownList 的 ID 属性设置为`Categories`。


[![删除文本框中，并将 DropDownList 添加到 EditItemTemplate](customizing-the-data-modification-interface-cs/_static/image14.png)](customizing-the-data-modification-interface-cs/_static/image13.png)

**图 5**： 删除文本框中，并添加到 DropDownList `EditItemTemplate` ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image15.png))


接下来，我们需要填充 DropDownList 与可用的类别。 单击 DropDownList 的智能标记中的选择数据源链接，然后选择创建名为新 ObjectDataSource `CategoriesDataSource`。


[![创建一个名为 CategoriesDataSource 的新 ObjectDataSource 控件](customizing-the-data-modification-interface-cs/_static/image17.png)](customizing-the-data-modification-interface-cs/_static/image16.png)

**图 6**： 创建新的 ObjectDataSource 控件命名`CategoriesDataSource`([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image18.png))


若要让此 ObjectDataSource 返回所有类别，将其绑定到`CategoriesBLL`类的`GetCategories()`方法。


[![将对象数据源绑定到 CategoriesBLL GetCategories() 方法](customizing-the-data-modification-interface-cs/_static/image20.png)](customizing-the-data-modification-interface-cs/_static/image19.png)

**图 7**： 将绑定到 ObjectDataSource`CategoriesBLL`的`GetCategories()`方法 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image21.png))


最后，配置 DropDownList 的设置，以便`CategoryName`字段显示在每个 DropDownList`ListItem`与`CategoryID`用作值的字段。


[![已显示类别名称字段和类别 Id 用作值](customizing-the-data-modification-interface-cs/_static/image23.png)](customizing-the-data-modification-interface-cs/_static/image22.png)

**图 8**： 具有`CategoryName`显示字段和`CategoryID`作为值 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image24.png))


进行更改的声明性标记后`EditItemTemplate`在`CategoryName`templatefield 进一步将包括 DropDownList 和 ObjectDataSource:


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> 在 DropDownList`EditItemTemplate`必须具有启用了其视图状态。 我们很快就会添加数据绑定语法 DropDownList 的声明性语法和数据绑定命令，如`Eval()`和`Bind()`只能出现在控件中启用了其视图状态。


重复上述步骤，添加名为 DropDownList`Suppliers`到`SupplierName`TemplateField 的`EditItemTemplate`。 这将涉及到添加到 DropDownList`EditItemTemplate`并创建另一个对象数据源。 `Suppliers` DropDownList 的对象数据源，但是，应配置为调用`SuppliersBLL`类的`GetSuppliers()`方法。 此外，配置`Suppliers`DropDownList 以显示`CompanyName`字段，并使用`SupplierID`字段的值作为其`ListItem`s。

添加到两个 Dropdownlist 后`EditItemTemplate`s，浏览器中加载的页面和单击 Chef Anton Cajun Seasoning 产品的编辑按钮。 如图 9 所示，该产品的类别和供应商列呈现为包含可用类别和供应商可供选择的下拉列表。 但请注意，*第一个*这两个下拉列表中的项选择默认情况下，（饮料类别） 和特殊液体作为供应商，即使 Chef Anton Cajun Seasoning 是提供的新奥尔良 Cajun Condiment带来快乐。


[![默认情况下选择下拉列表中的第一个项](customizing-the-data-modification-interface-cs/_static/image26.png)](customizing-the-data-modification-interface-cs/_static/image25.png)

**图 9**： 默认情况下选择下拉列表中的第一项 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image27.png))


此外，如果单击更新，您会发现，该产品`CategoryID`并`SupplierID`值设置为`NULL`。 这两种不需要的引发的行为，因为在 Dropdownlist `EditItemTemplate` s 从基础产品数据未绑定到任何数据字段。

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>绑定到 Dropdownlist`CategoryID`和`SupplierID`数据字段

需已编辑的产品的类别和供应商下拉列表设置为适当的值，并具有这些值发送回 BLL`UpdateProduct`方法中的单击更新时，我们需要将绑定 Dropdownlist`SelectedValue`属性`CategoryID`和`SupplierID`使用双向数据绑定的数据字段。 若要实现此目的`Categories`下拉列表中，您可以添加`SelectedValue='<%# Bind("CategoryID") %>'`直接与声明性语法。

或者，您可以通过在设计器编辑模板并单击 DropDownList 的智能标记中的编辑 DataBindings 链接通过设置 DropDownList 的数据绑定。 接下来，指示`SelectedValue`应将属性绑定到`CategoryID`字段使用双向数据绑定 （请参阅图 10）。 重复在声明性或设计器进程绑定`SupplierID`数据字段到`Suppliers`DropDownList。


[![将 CategoryID 绑定到使用双向数据绑定的 DropDownList 的 SelectedValue 属性](customizing-the-data-modification-interface-cs/_static/image29.png)](customizing-the-data-modification-interface-cs/_static/image28.png)

**图 10**： 将绑定`CategoryID`到 DropDownList`SelectedValue`属性使用双向数据绑定 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image30.png))


绑定到应用后`SelectedValue`的两个 Dropdownlist 属性中，编辑的产品的类别和供应商列将默认为当前产品的值。 单击更新，`CategoryID`并`SupplierID`下拉列表中选定的项的值将传递到`UpdateProduct`方法。 图 11 显示了本教程后已添加的数据绑定语句;请注意如何 Chef Anton Cajun Seasoning 的所选的下拉列表项已正确 Condiment 和新奥尔良 Cajun 带来快乐。


[![默认情况下选择编辑产品的当前类别和供应商的值](customizing-the-data-modification-interface-cs/_static/image32.png)](customizing-the-data-modification-interface-cs/_static/image31.png)

**图 11**： 默认情况下选择根据编辑产品当前类别和供应商值 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image33.png))


## <a name="handlingnullvalues"></a>处理`NULL`值

`CategoryID`并`SupplierID`中的列`Products`表可以`NULL`，但在 Dropdownlist`EditItemTemplate`不包括列表项来表示`NULL`值。 这样做有两种后果：

- 用户不能使用我们的接口从非更改产品的类别或供应商`NULL`值设为`NULL`一个
- 如果某个产品拥有`NULL``CategoryID`或`SupplierID`，单击编辑按钮将导致异常。 这是因为`NULL`返回值`CategoryID`(或`SupplierID`) 中`Bind()`语句不映射到在 DropDownList 中的值 (DropDownList 将引发异常时其`SelectedValue`属性设置为值*不*列表项的集合中)。

为了支持`NULL``CategoryID`并`SupplierID`值，我们需要添加另一个`ListItem`到来表示每个 DropDownList`NULL`值。 在中[母版/详细信息筛选与 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教程，我们已了解如何添加其他`ListItem`到数据绑定的 DropDownList，这涉及设置 DropDownList`AppendDataBoundItems`属性设置为`true`和手动添加的额外`ListItem`。 在该上一教程中，不过，我们添加了`ListItem`与`Value`的`-1`。 数据绑定逻辑在 ASP.NET 中，但是，将自动保留为空字符串转换为`NULL`值和进行相反的转换。 因此，本教程中我们想`ListItem`的`Value`为空字符串。

通过设置这两个 Dropdownlist 的起始`AppendDataBoundItems`属性设置为`true`。 接下来，添加`NULL``ListItem`通过将以下内容添加`<asp:ListItem>`到每个 DropDownList 的元素，以便声明性标记看起来类似于：


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample6.aspx)]

我选择了使用"(None)"作为文本值为此`ListItem`，但可以将其也作为空白字符串，如果想要进行更改。

> [!NOTE]
> 中可以看到*母版/详细信息筛选与 DropDownList*教程中， `ListItem` s 可以通过单击 DropDownList 添加到设计器通过 DropDownList`Items`属性窗口中的属性 (将显示`ListItem`集合编辑器)。 但是，务必添加`NULL``ListItem`本教程中通过声明性语法。 如果您使用`ListItem`集合编辑器中，将忽略生成的声明性语法`Value`完全设置何时分配一个空字符串，创建类似的声明性标记： `<asp:ListItem>(None)</asp:ListItem>`。 虽然这可能看起来无害，缺失值会导致使用 DropDownList`Text`来代替属性值。 这意味着，如果这`NULL``ListItem`是选择，"(None)"的值，将尝试分配给`CategoryID`，这将导致异常。 通过显式设置`Value=""`、 一个`NULL`值将分配给`CategoryID`时`NULL``ListItem`处于选中状态。


对供应商 DropDownList 重复这些步骤。

与此额外`ListItem`，现在可以分配编辑界面`NULL`到产品的值`CategoryID`和`SupplierID`字段，如图 12 中所示。


[![选择 （无） 将 NULL 值分配为产品的类别或供应商](customizing-the-data-modification-interface-cs/_static/image35.png)](customizing-the-data-modification-interface-cs/_static/image34.png)

**图 12**： 选择 （无） 待分配`NULL`产品的类别或供应商的值 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image36.png))


## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>步骤 4： 使用单选按钮用于停止使用的状态

当前产品的`Discontinued`使用 CheckBoxField，呈现禁用的复选框为只读的行和所编辑的行的已启用对应的复选框表示数据字段。 通常适合此用户界面时，我们可以根据需要使用 templatefield 进一步定制它。 对于本教程中，让我们更改 CheckBoxField 转换为 TemplateField RadioButtonList 控件使用两个选项"活动"和"停止使用"用户可以从中指定产品的`Discontinued`值。

通过转换启动`Discontinued`转换为 TemplateField，将创建使用 TemplateField CheckBoxField`ItemTemplate`和`EditItemTemplate`。 这两个模板包含一个具有复选框及其`Checked`属性绑定到`Discontinued`数据字段中，唯一的区别是，两者之间`ItemTemplate`的复选框的`Enabled`属性设置为`false`。

将为两者中的复选框`ItemTemplate`并`EditItemTemplate`RadioButtonList 控件后，设置这两个 RadioButtonLists'`ID`属性设置为`DiscontinuedChoice`。 接下来，指示 RadioButtonLists 应每个包含两个单选按钮，一个标记为"活动"，值为"False"，另一个标记为"停用"，值为"True"。 若要完成此您可以输入`<asp:ListItem>`元素中的直接通过声明性语法或使用`ListItem`从设计器的集合编辑器。 图 13 显示了`ListItem`集合编辑器后两个单选按钮选项已指定。


[![添加](customizing-the-data-modification-interface-cs/_static/image38.png)](customizing-the-data-modification-interface-cs/_static/image37.png)

**图 13**： 将"活动"和"停止"选项添加到 RadioButtonList ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image39.png))


由于在 RadioButtonList`ItemTemplate`不应为可编辑，设置其`Enabled`属性设置为`false`、 离开`Enabled`属性设置为`true`（默认值） 中 RadioButtonList 为`EditItemTemplate`。 这将使非编辑为只读的行中的单选按钮，但将允许用户更改编辑过的行的单选按钮值。

我们仍需分配 RadioButtonList 控件的`SelectedValue`属性，以便在相应的单选按钮选择基于产品的`Discontinued`数据字段。 直接在声明性标记或通过 RadioButtonLists 的智能标记中的编辑 DataBindings 链接，或者可以与 Dropdownlist 检查此前在本教程中，添加此数据绑定语法。

之后添加两个 RadioButtonLists 和配置它们， `Discontinued` TemplateField 的声明性标记应如下所示：


[!code-aspx[Main](customizing-the-data-modification-interface-cs/samples/sample7.aspx)]

这些更改，`Discontinued`列的复选框列表从转换到的 （请参阅图 14） 的单选按钮对列表。 在编辑某个产品时，相应的单选按钮处于选中状态，并选择其他单选按钮，然后单击更新可以更新产品的已停止使用的状态。


[![单选按钮对已替换为已停止使用复选框](customizing-the-data-modification-interface-cs/_static/image41.png)](customizing-the-data-modification-interface-cs/_static/image40.png)

**图 14**: 停止使用复选框已替换为单选按钮对 ([单击以查看实际尺寸的图像](customizing-the-data-modification-interface-cs/_static/image42.png))


> [!NOTE]
> 由于`Discontinued`中的列`Products`数据库不能具有`NULL`值，我们不需要担心如何捕获`NULL`界面中的信息。 如果，但是，`Discontinued`列可能包含`NULL`值，我们想要添加第三个单选按钮与向列表及其`Value`设置为空字符串 (`Value=""`)，就像使用类别和供应商 Dropdownlist。


## <a name="summary"></a>总结

虽然 BoundField 和 CheckBoxField 自动呈现只读、 编辑以及插入接口，它们都不能在自定义项。 通常情况下，不过，我们将需要自定义编辑或插入接口，可能添加验证控件 （如在前面的教程中看到的） 或通过自定义数据收集用户界面 （如我们在本教程中看到）。 自定义使用 TemplateField 界面可将其概括中的以下步骤：

1. 添加 TemplateField 或将现有 BoundField 或 CheckBoxField 转换转换为 TemplateField
2. 根据需要增加接口
3. 将相应的数据字段绑定到新添加的 Web 控件使用双向数据绑定

除了使用内置的 ASP.NET Web 控件，您可以自定义 TemplateField 与已编译的自定义服务器控件和用户控件的模板。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)
> [下一页](implementing-optimistic-concurrency-cs.md)
