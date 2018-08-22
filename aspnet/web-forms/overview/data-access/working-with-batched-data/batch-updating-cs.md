---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
title: 批更新 (C#) |Microsoft Docs
author: rick-anderson
description: 了解如何更新单个操作中的多个数据库记录。 在用户界面层我们构建一个 GridView，其中每行都是可编辑。 在数据中...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4e849bcc-c557-4bc3-937e-f7453ee87265
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
msc.type: authoredcontent
ms.openlocfilehash: c878056273ea821e4dd4481fa1b6f7690f22b285
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823525"
---
<a name="batch-updating-c"></a>批更新 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_CS.zip)或[下载 PDF](batch-updating-cs/_static/datatutorial64cs1.pdf)

> 了解如何更新单个操作中的多个数据库记录。 在用户界面层我们构建一个 GridView，其中每行都是可编辑。 数据访问层中，我们将以确保所有更新都成功或所有更新都将都回滚的事务中的多个更新操作。


## <a name="introduction"></a>介绍

在中[前面的教程](wrapping-database-modifications-within-a-transaction-cs.md)我们已了解如何扩展数据访问层，以便添加对数据库事务的支持。 数据库事务保证一系列的数据修改语句将被视为一个原子操作，它可确保所有修改将都失败或所有将会成功。 使用此低级别 DAL 功能开，我们重新准备我们把注意力转向创建数据修改界面的批处理。

在本教程中我们将构建一个 GridView，其中每个行是可编辑 （请参阅图 1）。 由于无需进行编辑的列，每行均呈现在其编辑界面中，那里 s，更新和取消按钮。 相反，有两个更新的产品按钮的页上，单击时，枚举 GridView 行并更新数据库。


[![在 GridView 中的每一行都是可编辑](batch-updating-cs/_static/image1.gif)](batch-updating-cs/_static/image1.png)

**图 1**： 在 GridView 中的每个行是可编辑 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image2.png))


让我们来开始 ！

> [!NOTE]
> 在中[执行批处理更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)教程中，我们创建批处理编辑接口使用 DataList 控件。 本教程中不同于上一个中的其中一个是使用 GridView 和事务的作用域内执行批处理更新。 完成本教程后我鼓励您返回到早期的教程，并将其更新为使用在前面的教程中已添加的数据库与事务相关功能。


## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>检查建立所有 GridView 行可编辑的步骤

如中所述[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中，GridView 提供了用于编辑每个行按其基础数据的内置支持。 在内部，GridView 说明哪些行是可通过编辑其[`EditIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)。 正在将 GridView 绑定到其数据源，因为它会检查每个行可查看的行的索引是否等于的值`EditIndex`。 如果是这样，该行 s 呈现字段使用其编辑界面。 对于 BoundFields，编辑界面是文本框中其`Text`属性分配由 BoundField s 指定的数据字段的值`DataField`属性。 为 Templatefield，`EditItemTemplate`来代替使用`ItemTemplate`。

回想一下在编辑工作流启动时在用户单击行的编辑按钮。 这将导致回发，设置 GridView 的`EditIndex`s 被单击的行索引和重新绑定次数到网格的数据的属性。 当单击行 s 取消按钮，在回发`EditIndex`设置的值为`-1`之前重新绑定到网格的数据。 由于 GridView 的行开始编制索引为零，因此设置`EditIndex`到`-1`GridView 显示在只读模式下的影响。

`EditIndex`属性非常适用于每个行编辑，但不是用于批处理编辑。 若要使整个 GridView 可编辑，我们需要能够使用其编辑界面呈现每个行。 若要实现此目的的最简单方法是创建每个可编辑字段实现具有其编辑界面 TemplateField 中定义的位置`ItemTemplate`。

在接下来的几个步骤我们将创建一个完全可编辑的 GridView。 步骤 1 中我们首先创建 GridView 和其对象数据源，并将其 BoundFields 和 CheckBoxField 转换为 Templatefield。 步骤 2 和 3 中，我们将从 Templatefield 继续编辑接口`EditItemTemplate`向其`ItemTemplate`s。

## <a name="step-1-displaying-product-information"></a>步骤 1： 显示产品信息

我们担心如何创建 GridView 之前所在的行都是可编辑，让我们来首先只需显示产品信息。 打开`BatchUpdate.aspx`页中`BatchData`文件夹，然后拖动 GridView 从工具箱拖到设计器。 设置 GridView s`ID`到`ProductsGrid`，并从其智能标记，选择要绑定到名为新 ObjectDataSource `ProductsDataSource`。 配置要检索其数据从 ObjectDataSource`ProductsBLL`类的`GetProducts`方法。


[![配置对象数据源以使用 ProductsBLL 类](batch-updating-cs/_static/image2.gif)](batch-updating-cs/_static/image3.png)

**图 2**： 配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image4.png))


[![检索产品数据使用 GetProducts 方法](batch-updating-cs/_static/image3.gif)](batch-updating-cs/_static/image5.png)

**图 3**： 检索产品数据使用`GetProducts`方法 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image6.png))


如 GridView，ObjectDataSource 的修改功能旨在针对每个行而工作的。 若要更新的一组记录，我们将需要进行批处理数据，并将其传递给 BLL 的 ASP.NET 页面 + s 代码隐藏类中编写一些代码。 因此，设置下拉列表中的 ObjectDataSource 的更新、 插入和删除选项卡添加到 （无）。 单击完成以完成向导。


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](batch-updating-cs/_static/image4.gif)](batch-updating-cs/_static/image7.png)

**图 4**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image8.png))


完成配置数据源向导后，在 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](batch-updating-cs/samples/sample1.aspx)]

完成配置数据源向导还会导致 Visual Studio 在 GridView 中创建 BoundFields 和产品数据字段 CheckBoxField。 对于本教程，让我们来仅允许用户查看和编辑产品的名称、 类别、 价格和已停止使用的状态。 删除所有除`ProductName`， `CategoryName`， `UnitPrice`，和`Discontinued`字段和重命名`HeaderText`的前三个属性字段设置为产品、 类别和价格，分别。 最后，检查 GridView s 智能标记中的启用分页和启用排序复选框。

这个 GridView 现在有三个 BoundFields (`ProductName`， `CategoryName`，并`UnitPrice`) 和 CheckBoxField (`Discontinued`)。 我们需要将这四个字段转换为 Templatefield，然后将编辑界面移动从 TemplateField s`EditItemTemplate`到其`ItemTemplate`。

> [!NOTE]
> 我们探讨了创建和自定义中的 Templatefield[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程。 我们将演示 BoundFields 和 CheckBoxField 转换为 Templatefield 的步骤，并定义其编辑界面中其`ItemTemplate`s，但如果有疑问或需要刷新程序，不要欢迎回头参考此早期的教程。


从 GridView s 智能标记，单击编辑列链接以打开字段对话框。 接下来，选择每个字段，并单击转换此字段转换为 TemplateField 链接。


![将现有 BoundFields 和 CheckBoxField 转换为 TemplateField](batch-updating-cs/_static/image5.gif)

**图 5**： 现有 BoundFields 和 CheckBoxField 转换为 TemplateField


现在，每个字段都为 TemplateField，我们准备就绪后，若要移动的编辑界面`EditItemTemplate`到`ItemTemplate`s。

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>步骤 2： 创建`ProductName`，`UnitPrice`，和`Discontinued`编辑接口

创建`ProductName`， `UnitPrice`，并`Discontinued`编辑接口是此步骤的主题，每个接口已定义中的 TemplateField s 是相当简单， `EditItemTemplate`。 创建`CategoryName`编辑界面是稍微要复杂，因为我们需要创建 DropDownList 适用的类别。 这`CategoryName`编辑界面在步骤 3 中处理。

让我们来开始`ProductName`TemplateField。 单击 GridView s 智能标记中的编辑模板链接，然后向下钻取`ProductName`TemplateField 的`EditItemTemplate`。 选择文本框中，将其复制到剪贴板，然后再粘贴到`ProductName`TemplateField 的`ItemTemplate`。 更改文本框 s`ID`属性设置为`ProductName`。

接下来，添加到一个 RequiredFieldValidator`ItemTemplate`以确保用户为每个产品的名称提供一个值。 设置`ControlToValidate`属性设置为产品名称`ErrorMessage`属性设置为你必须提供产品的名称。 并`Text`属性设置为\*。 建立到这些新增功能后`ItemTemplate`，屏幕应类似于图 6。


[![ProductName TemplateField 现在包含一个文本框和一个 RequiredFieldValidator](batch-updating-cs/_static/image6.gif)](batch-updating-cs/_static/image9.png)

**图 6**: `ProductName` TemplateField 现在包含一个文本框和一个 RequiredFieldValidator ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image10.png))


有关`UnitPrice`编辑界面，首先复制从文本框`EditItemTemplate`到`ItemTemplate`。 接下来，将 $ 前面的文本框中并设置其`ID`属性设置为单价并将其`Columns`属性设置为 8。

此外将添加到 CompareValidator `UnitPrice` s`ItemTemplate`以确保用户输入的值是有效的货币值大于或等于为 0.00 美元。 设置验证程序 s`ControlToValidate`属性设置为单价，其`ErrorMessage`属性设置为您必须输入有效的货币值。 请省略任何货币符号。，其`Text`属性设置为\*，将其`Type`属性设置为`Currency`，将其`Operator`属性设置为`GreaterThanEqual`，并将其`ValueToCompare`属性设为 0。


[![添加 CompareValidator，确保价格输入是一个非负货币值](batch-updating-cs/_static/image7.gif)](batch-updating-cs/_static/image11.png)

**图 7**： 添加 CompareValidator，确保价格输入是一个非负货币值 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image12.png))


有关`Discontinued`TemplateField 可以使用已在中定义的复选框`ItemTemplate`。 只需设置其`ID`到已中断并且其`Enabled`属性设置为`true`。

## <a name="step-3-creating-thecategorynameediting-interface"></a>步骤 3： 创建`CategoryName`编辑接口

中的编辑界面`CategoryName`TemplateField s`EditItemTemplate`包含一个文本框，用于显示的值`CategoryName`数据字段。 我们需要此项替换 DropDownList，其中列出了可能的类别。

> [!NOTE]
> [自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程包含自定义模板以包括 DropDownList 而不是文本框的更全面、 完整讨论。 尽管此处的步骤都完成后，他们将看到 tersely。 有关创建和配置类别 DropDownList 的更深入信息，请参阅重新[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程。


从工具箱拖到拖 DropDownList `CategoryName` TemplateField s `ItemTemplate`，并设置其`ID`到`Categories`。 此时我们将通常定义 Dropdownlist 的数据源通过其智能标记，创建新对象数据源。 但是，这将添加在 ObjectDataSource `ItemTemplate`，这将导致为每个 GridView 行创建 ObjectDataSource 实例。 相反，允许创建外部 GridView 的 Templatefield ObjectDataSource 的 s。 结束模板编辑，并将从工具箱拖到设计器下方的 ObjectDataSource`ProductsDataSource`对象数据源。 命名新 ObjectDataSource`CategoriesDataSource`并将其配置为使用`CategoriesBLL`类的`GetCategories`方法。


[![配置为使用 CategoriesBLL Clas ObjectDataSource](batch-updating-cs/_static/image8.gif)](batch-updating-cs/_static/image13.png)

**图 8**： 配置为使用 ObjectDataSource `CategoriesBLL` Clas ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image14.png))


[![检索类别数据使用 GetCategories 方法](batch-updating-cs/_static/image9.gif)](batch-updating-cs/_static/image15.png)

**图 9**： 检索类别数据使用`GetCategories`方法 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image16.png))


由于此 ObjectDataSource 只是用于检索数据，设置为 （无） 更新和删除选项卡中的下拉列表。 单击完成以完成向导。


[![集更新和删除选项卡添加到 （无） 中的下拉列表](batch-updating-cs/_static/image10.gif)](batch-updating-cs/_static/image17.png)

**图 10**： 设置的下拉列表中的更新和删除选项卡为 （无） ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image18.png))


完成向导后`CategoriesDataSource`s 声明性标记应如下所示：


[!code-aspx[Main](batch-updating-cs/samples/sample2.aspx)]

与`CategoriesDataSource`创建并配置，返回到`CategoryName`TemplateField 的`ItemTemplate`，再从 DropDownList s 智能标记，单击选择数据源链接。 在数据源配置向导中，选择`CategoriesDataSource`选项从第一个下拉列表，然后选择能够`CategoryName`用于显示和`CategoryID`作为值。


[![绑定 DropDownList 到 CategoriesDataSource](batch-updating-cs/_static/image11.gif)](batch-updating-cs/_static/image19.png)

**图 11**： 将绑定到 DropDownList `CategoriesDataSource` ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image20.png))


此时`Categories`DropDownList 列出了所有类别，但它不会自动选择适当的绑定到 GridView 行的产品类别。 若要完成此我们需要设置`Categories`DropDownList s`SelectedValue`产品 s`CategoryID`值。 单击编辑 DataBindings 链接从 DropDownList s 智能标记，并将关联`SelectedValue`具有属性`CategoryID`数据字段，如图 12 中所示。


![将产品的 CategoryID 值绑定到 DropDownList 的 SelectedValue 属性](batch-updating-cs/_static/image12.gif)

**图 12**： 将绑定产品 s`CategoryID`值为 DropDownList 的`SelectedValue`属性


最后一个问题保持为一个： 如果产品不具有`CategoryID`指定值然后数据绑定语句上`SelectedValue`将导致异常。 这是因为 DropDownList 只包含项的类别，并且不提供对具有这些产品的选项`NULL`数据库值`CategoryID`。 若要解决此问题，设置 DropDownList s`AppendDataBoundItems`属性设置为`true`并将新项添加到下拉列表中，省略`Value`从声明性语法的属性。 也就是说，请确保`Categories`DropDownList s 声明性语法看起来如下所示：


[!code-aspx[Main](batch-updating-cs/samples/sample3.aspx)]

请注意如何`<asp:ListItem Value="">`-选择一个-具有其`Value`属性显式设置为空字符串。 回头[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程，了解为什么需要此额外的 DropDownList 项处理的更全面讨论`NULL`用例和原因的分配`Value`属性为空字符串是必不可少的。

> [!NOTE]
> 没有一个潜在性能和可伸缩性问题此处值得一提的。 因为每一行都具有使用 DropDownList`CategoriesDataSource`作为其数据源，`CategoriesBLL`类 s`GetCategories`将调用方法*n*页每次访问时，其中*n*是数在 GridView 中的行。 这些*n*调用`GetCategories`导致*n*对数据库的查询。 通过缓存返回的类别在每个请求缓存中或通过使用 SQL 缓存依赖项或在非常短的时间基于过期的缓存层，并且导致这种影响在数据库上的可能会降低。 有关每个请求的详细信息缓存选项，请参阅[`HttpContext.Items`每个请求缓存存储](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)。


## <a name="step-4-completing-the-editing-interface"></a>步骤 4： 完成编辑界面

我们已对所做的大量更改 GridView 的模板而不暂停以查看我们的进度。 花点时间查看我们通过浏览器的进度。 如图 13 所示，每行均呈现使用其`ItemTemplate`，其中包含的单元格 s 编辑界面。


[![每个 GridView 行是可编辑](batch-updating-cs/_static/image13.gif)](batch-updating-cs/_static/image21.png)

**图 13**： 每个 GridView 行是可编辑 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image22.png))


有一些我们需要采取措施的此时次要格式设置问题。 首先，请注意，`UnitPrice`值包含小数点后有 4。 若要解决此问题，返回到`UnitPrice`TemplateField 的`ItemTemplate`，再从文本框 s 智能标记，单击编辑 DataBindings 链接。 接下来，指定`Text`属性的格式应为数字。


![格式的 Text 属性设置为一个数字](batch-updating-cs/_static/image14.gif)

**图 14**： 格式`Text`数字形式的属性


其次，let s 中心中的复选框`Discontinued`列 （而不是让其左对齐）。 单击编辑列的 GridView s 智能标记，然后选择`Discontinued`TemplateField 从左下角中的字段列表。 向下钻取到`ItemStyle`并设置`HorizontalAlign`到中心，如图 15 中所示的属性。


![中心已停止使用复选框](batch-updating-cs/_static/image15.gif)

**图 15**: Center`Discontinued`复选框


接下来，向页面添加验证摘要控件并设置其`ShowMessageBox`属性设置为`true`并将其`ShowSummary`属性设置为`false`。 此外添加按钮 Web 控件，单击时，将更新用户 s 做的更改。 具体而言，添加一个上面 GridView，它下面的一个设置这两个控件的两个按钮 Web 控件`Text`更新产品的属性。

因为 GridView s 编辑接口中定义其 Templatefield `ItemTemplate` s，`EditItemTemplate`进行多余，可能会被删除。

使上面提到的格式设置更改后，将按钮控件添加和删除不必要`EditItemTemplate`s，页面 + s 声明性语法应如下所示：


[!code-aspx[Main](batch-updating-cs/samples/sample4.aspx)]

图 16 显示此页上，当后已添加按钮 Web 控件的浏览器查看和格式设置所做的更改。


[![页现在包含两个更新的产品按钮](batch-updating-cs/_static/image16.gif)](batch-updating-cs/_static/image23.png)

**图 16**: 页现在包含两个更新的产品按钮 ([单击以查看实际尺寸的图像](batch-updating-cs/_static/image24.png))


## <a name="step-5-updating-the-products"></a>步骤 5： 更新产品

用户访问此页时它们将使其修改，然后单击两个更新产品按钮之一。 此时，我们需要以某种方式保存到每个行的用户输入值`ProductsDataTable`实例，然后将其传递给将然后将其传递的 BLL 方法`ProductsDataTable`实例与 DAL 的`UpdateWithTransaction`方法。 `UpdateWithTransaction`方法，我们在中创建[前面的教程](wrapping-database-modifications-within-a-transaction-cs.md)，可以确保批更改，将更新作为一个原子操作。

创建一个名为方法`BatchUpdate`在`BatchUpdate.aspx.cs`并添加以下代码：


[!code-csharp[Main](batch-updating-cs/samples/sample5.cs)]

此方法首先获取的所有产品回到`ProductsDataTable`通过为 BLL 的调用`GetProducts`方法。 然后，它枚举`ProductGrid`GridView s [ `Rows`集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)。 `Rows`集合中包含[`GridViewRow`实例](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx)GridView 中显示每个行。 因为我们还展示了最多十个行，每页、 GridView 的`Rows`集合将会有不能超过 10 个项。

每个行`ProductID`获取从`DataKeys`集合和相应`ProductsRow`从选择`ProductsDataTable`。 四个 TemplateField 输入的控件以编程方式进行引用，而它们的值分配给`ProductsRow`实例 s 属性。 在每个 GridView 后行的值已用于更新`ProductsDataTable`，它传递给 BLL s`UpdateWithTransaction`方法，正如我们看到在上一教程中，只是调用向下 DAL 的`UpdateWithTransaction`方法。

本教程使用的批处理更新算法更新中的每一行`ProductsDataTable`GridView，无论是否已更改产品的信息中的行相对应。 而此类 blind 更新计划运行 t 通常性能问题，它们可能会导致多余记录如果您重新审核更改为数据库表。 回到[执行批处理更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)教程，我们探讨了使用 DataList 更新接口一批，并添加了代码，只会更新实际已由用户修改这些记录。 可使用从技术[执行批处理更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)更新代码，在本教程中，如果所需的。

> [!NOTE]
> 当数据源绑定到 GridView 通过其智能标记，Visual Studio 会自动向数据源 s 主值 GridView 的`DataKeyNames`属性。 如果您未绑定 ObjectDataSource 到 GridView s 智能标记通过 GridView 步骤 1 中所述，则将需要手动设置 GridView s`DataKeyNames`属性设置为产品 id 才能访问`ProductID`通过每一行的值`DataKeys`集合。


中使用的代码`BatchUpdate`类似于 BLL s 中用`UpdateProduct`方法，主要区别在于，在`UpdateProduct`方法只有一个`ProductRow`从体系结构中检索实例。 分配的属性的代码`ProductRow`之间是相同的`UpdateProducts`方法和中的代码`foreach`循环中`BatchUpdate`，如是总体模式。

若要完成本教程，我们必须具备`BatchUpdate`方法时调用任一更新产品按钮单击。 创建事件处理程序`Click`事件这两个按钮控件，然后在事件处理程序中添加以下代码：


[!code-csharp[Main](batch-updating-cs/samples/sample6.cs)]

第一次调用`BatchUpdate`。 下一步，`ClientScript property`用于注入 JavaScript，它将显示已更新的产品中读取一个消息框。

花点时间来测试此代码。 请访问`BatchUpdate.aspx`通过浏览器中，编辑的行数，并单击其中一个更新产品按钮。 假设没有任何输入的验证错误，应看到已更新的产品中读取一个消息框。 若要验证更新的原子性，请考虑添加一个随机`CHECK`约束，不允许类似`UnitPrice`1234.56 的值。 然后从`BatchUpdate.aspx`，编辑对多条记录，并确保设置一个产品的`UnitPrice`禁止使用的值 (1234.56) 的值。 在该批处理操作期间所做的更改与单击更新产品回滚到其原始值时，应导致错误。

## <a name="an-alternativebatchupdatemethod"></a>一种替代方法`BatchUpdate`方法

`BatchUpdate`方法，我们只需检查检索*所有*BLL s 中的产品的`GetProducts`方法，然后更新在 GridView 中显示的那些记录。 如果 GridView 不使用分页，但如果是这样，可能有数百、 数千个或成千上万的产品，但在 GridView 中的十个行，这种方法是理想之选。 在这种情况下，从仅要修改其中 10 家的数据库中获取的所有产品都是不太理想。

对于这些类型的情况下，请考虑使用以下`BatchUpdateAlternate`方法改为：


[!code-csharp[Main](batch-updating-cs/samples/sample7.cs)]

`BatchMethodAlternate` 首先创建一个新的空`ProductsDataTable`名为`products`。 然后，它通过 GridView s 的步骤`Rows`集合并为每一行获取特定产品信息使用 BLL 的`GetProductByProductID(productID)`方法。 检索到`ProductsRow`实例具有相同的方式更新其属性`BatchUpdate`，但更新导入的行后`products``ProductsDataTable`通过 DataTable s [ `ImportRow(DataRow)`方法](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)。

之后`foreach`循环完成后，`products`包含一个`ProductsRow`GridView 中的每一行的实例。 由于每个`ProductsRow`已添加到实例`products`（而不是已更新），如果我们会盲目地将其传递给`UpdateWithTransaction`方法`ProductsTableAdatper`将尝试将每个记录插入数据库。 相反，我们需要指定这些行的每个已修改了 （未添加）。

这可以通过将新方法添加到名为 BLL `UpdateProductsWithTransaction`。 `UpdateProductsWithTransaction`如下所示的设置`RowState`的每个`ProductsRow`实例中`ProductsDataTable`到`Modified`，然后将传递`ProductsDataTable`为 DAL 的`UpdateWithTransaction`方法。


[!code-csharp[Main](batch-updating-cs/samples/sample8.cs)]

## <a name="summary"></a>总结

GridView 提供内置的每行的编辑功能，但不能创建完全可编辑的接口的支持。 正如我们看到在本教程中，此类接口是可能的但需要的工作。 若要创建的每个行是可编辑一个 GridView，我们需要将转换为 Templatefield GridView 的字段并定义中的编辑界面`ItemTemplate`s。 此外，更新所有的按钮 Web 控件的类型必须被添加到页上，独立于 GridView。 这些按钮`Click`事件处理程序需要枚举 GridView s`Rows`集合中，存储中的更改`ProductsDataTable`，并将更新的信息传递到适当的 BLL 方法。

在下一教程中我们将了解如何创建用于方式成批删除的接口。 具体而言，每个 GridView 行将包含一个复选框和而不是更新所有的键入按钮，我们将删除所选行按钮。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和 David Suru。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](wrapping-database-modifications-within-a-transaction-cs.md)
> [下一页](batch-deleting-cs.md)
