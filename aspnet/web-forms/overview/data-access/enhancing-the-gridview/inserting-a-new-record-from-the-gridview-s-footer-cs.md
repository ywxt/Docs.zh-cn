---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
title: 插入新记录从 GridView 页脚 (C#) |Microsoft Docs
author: rick-anderson
description: 虽然 GridView 控件不提供用于插入数据的新记录的内置支持，本教程演示如何增强 GridView，其中包括...
ms.author: aspnetcontent
ms.date: 03/06/2007
ms.assetid: 49545652-98af-46ba-9dbc-9ab529805d9b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 3ce1c1ea83d2fc50d7cf9ab6cb64d1e76307c74b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830498"
---
<a name="inserting-a-new-record-from-the-gridviews-footer-c"></a>从 GridView 页脚 (C#) 插入新记录
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_CS.exe)或[下载 PDF](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/datatutorial53cs1.pdf)

> 虽然 GridView 控件不提供用于插入数据的新记录的内置支持，本教程演示如何增强 GridView，其中包含一个插入的界面。


## <a name="introduction"></a>介绍

如中所述[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程，GridView、 DetailsView 和 FormView Web 控制每个包括内置的数据修改功能。 如果用于声明性数据源控件，这三个 Web 控件可以快速轻松地配置为修改的数据-并在方案中而无需编写一行代码。 遗憾的是，只有 DetailsView 和 FormView 控件提供内置的插入、 编辑和删除功能。 编辑和删除的支持，仅提供了 GridView。 但是，一些与肘部油，我们可以提供了 GridView，其中包含一个插入的界面。

在将插入功能添加到 GridView，我们负责决定将添加新记录、 创建插入接口，以及编写代码来插入新记录。 在本教程中我们将探讨将插入界面添加到 GridView 的页脚行 （请参阅图 1）。 每个列的页脚单元格包含相应的数据集合用户界面元素 （s 产品名称文本框中，DropDownList 供应商，等等）。 我们还需要一列的添加按钮，单击时，将导致回发并插入新记录到`Products`表可使用提供的脚注行中的值。


[![脚注行中添加新的产品提供的接口](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.png)

**图 1**： 脚注行提供用于添加新产品的接口 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.png))


## <a name="step-1-displaying-product-information-in-a-gridview"></a>步骤 1： 在 GridView 中显示的产品信息

我们考虑自己创建 GridView 的页脚中插入接口之前，让 s 第一个专注于向列出数据库中的产品页添加 GridView。 首先打开`InsertThroughFooter.aspx`页中`EnhancedGridView`文件夹，然后从工具箱拖到设计器中，设置 GridView 的拖动 GridView`ID`属性设置为`Products`。 接下来，使用 GridView s 智能标记将其绑定到名为新 ObjectDataSource `ProductsDataSource`。


[![创建名为 ProductsDataSource 新 ObjectDataSource](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.png)

**图 2**： 创建新对象数据源命名`ProductsDataSource`([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.png))


配置要使用 ObjectDataSource`ProductsBLL`类的`GetProducts()`方法以检索产品信息。 对于本教程，让 s 专注于严格添加插入功能和不用再担心如何编辑和删除。 因此，请确保在插入选项卡中的下拉列表设置为`AddProduct()`并更新和删除选项卡中的下拉列表被设置为 （无）。


[![AddProduct 方法映射到 ObjectDataSource s insert （） 方法](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.png)

**图 3**： 映射`AddProduct`方法的 ObjectDataSource s`Insert()`方法 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.png))


[![将该更新设置和删除选项卡的下拉列表中的，以便 （无）](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.png)

**图 4**： 将更新和删除选项卡下拉列表设置为 （无） ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.png))


完成 ObjectDataSource s 配置数据源向导后，Visual Studio 会自动将字段添加到 GridView 为每个相应的数据字段。 现在，让所有由 Visual Studio 添加的字段。 在本教程中我们将随时可以返回并删除更高版本的某些字段的值不需要添加一条新记录时指定。

由于有接近 80 产品数据库中，用户必须一直到 web 页的底部滚动浏览才能添加新的记录。 因此，让我们来启用分页，使插入接口更可见且可访问。 若要启用分页，只需检查从 GridView s 智能标记启用分页复选框。

此时，GridView 和 ObjectDataSource s 声明性标记应类似以下：


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample1.aspx)]


[![将分页 GridView 中显示所有产品的数据字段](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.png)

**图 5**： 将已分页的 GridView 中显示所有产品数据字段 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.png))


## <a name="step-2-adding-a-footer-row"></a>步骤 2： 添加脚注行

除了其标头和数据行，GridView 包括脚注行。 页眉和页脚行显示 GridView s 的值决定[ `ShowHeader` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showheader.aspx)并[ `ShowFooter` ](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.gridview.showfooter.aspx)属性。 若要显示脚注行，只需设置`ShowFooter`属性设置为`true`。 如图 6 所示，设置`ShowFooter`属性设置为`true`将脚注行添加到网格。


[![若要显示脚注行，请将 ShowFooter 设置为 True](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.png)

**图 6**： 为显示脚注行中，设置`ShowFooter`到`True`([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.png))


请注意，页脚行深红色背景颜色。 这是因为我们创建并应用于所有页面 DataWebControls 主题回到[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程。 具体而言，`GridView.skin`文件用于配置`FooterStyle`此类属性，该属性是使用`FooterStyle`CSS 类。 `FooterStyle`类中定义`Styles.css`，如下所示：


[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample2.css)]

> [!NOTE]
> 我们已在前面的教程中使用 GridView 的脚注行浏览。 如果需要请回顾[GridView 的页脚中显示摘要信息](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md)教程，了解使用刷新程序。


设置后`ShowFooter`属性设置为`true`，花点时间在浏览器中查看输出。 当前页脚行不包含任何文本或 Web 控件。 在步骤 3 中我们将修改的页脚 GridView 中的每个字段，以使其包括在适当的插入接口。


[![空的脚注行是显示上面分页界面控件](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image13.png)

**图 7**: 空的脚注行是显示上面分页界面控件 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image14.png))


## <a name="step-3-customizing-the-footer-row"></a>步骤 3： 自定义页脚行

回到[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)教程中我们已了解如何极大地自定义特定的 GridView 列使用 Templatefield （而不是 BoundFields 或 CheckBoxFields） 显示; 在[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)我们了解了使用 Templatefield 自定义 GridView 中的编辑界面。 回想一下 TemplateField 组成大量模板定义多个标记、 Web 控件和数据绑定语法用于某些类型的行。 `ItemTemplate`，例如，指定的模板用于只读的行，尽管`EditItemTemplate`定义的可编辑的行的模板。

连同`ItemTemplate`并`EditItemTemplate`，还包括 TemplateField`FooterTemplate`指定页脚行的内容。 因此，我们可以添加所需的每个字段 s 插入到接口的 Web 控件`FooterTemplate`。 若要开始，转换为 Templatefield 所有 GridView 中的字段。 这可以单击 GridView s 智能标记，在左下角，选择每个字段并转换为 TemplateField 链接单击转换此字段中的编辑列链接。


![每个字段转换为 TemplateField](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.gif)

**图 8**： 每个字段转换为 TemplateField


此字段转换为 TemplateField 单击转换将等效 templatefield 进一步将当前字段类型。 例如，每个 BoundField 将替换为 TemplateField `ItemTemplate` ，其中包含显示相应的数据字段的标签和一个`EditItemTemplate`在文本框中显示数据字段。 `ProductName` BoundField 已转换为以下 TemplateField 标记：


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample3.aspx)]

同样， `Discontinued` CheckBoxField 已转换为 TemplateField 其`ItemTemplate`并`EditItemTemplate`包含一个复选框 Web 控件 (使用`ItemTemplate`s 禁用的复选框)。 只读`ProductID`BoundField 已转换为标签控件中使用 TemplateField`ItemTemplate`和`EditItemTemplate`。 字段转换为 TemplateField 转换现有的 GridView 简单地说，是功能的快速而简单的方法，而不会丢失任何现有字段切换到更定制化 TemplateField。

因为 GridView 重新使用此 t 编辑支持，我们可以删除`EditItemTemplate`只需从每个 TemplateField 离开`ItemTemplate`。 以后执行此操作，您的 GridView s 声明性标记看起来应如下所示：


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample4.aspx)]

现在，已转换为 TemplateField 转换 GridView 中的每个字段，我们可以输入相应的插入接口到每个字段的`FooterTemplate`。 某些字段不会插入接口 (`ProductID`，例如); 其他人使用，用于收集新的产品的信息 Web 控件中而异。

若要创建编辑界面，请从 GridView s 智能标记中选择编辑模板链接。 然后，从下拉列表中，选择相应字段的`FooterTemplate`并将相应控件从工具箱拖到设计器。


[![将相应的插入接口添加到每个字段的要](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image15.png)

**图 9**： 将相应的插入接口添加到每个字段 s `FooterTemplate` ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image16.png))


下列项目符号列表枚举 GridView 字段，指定要添加的插入接口：

- `ProductID` 无。
- `ProductName` 添加一个文本框，并设置其`ID`到`NewProductName`。 添加 RequiredFieldValidator 控件以确保用户的新产品的名输入一个值。
- `SupplierID` 无。
- `CategoryID` 无。
- `QuantityPerUnit` 添加文本框中，设置其`ID`到`NewQuantityPerUnit`。
- `UnitPrice` 添加名为文本框`NewUnitPrice`CompareValidator，以确保输入的值是大于或等于零的货币值。
- `UnitsInStock` 将 TextBox 其`ID`设置为`NewUnitsInStock`。 包括 CompareValidator，以确保输入的值是大于或等于零的整数值。
- `UnitsOnOrder` 将 TextBox 其`ID`设置为`NewUnitsOnOrder`。 包括 CompareValidator，以确保输入的值是大于或等于零的整数值。
- `ReorderLevel` 将 TextBox 其`ID`设置为`NewReorderLevel`。 包括 CompareValidator，以确保输入的值是大于或等于零的整数值。
- `Discontinued` 添加一个复选框，设置其`ID`到`NewDiscontinued`。
- `CategoryName` 添加 DropDownList，并设置其`ID`到`NewCategoryID`。 将其绑定到名为新 ObjectDataSource`CategoriesDataSource`并将其配置为使用`CategoriesBLL`类的`GetCategories()`方法。 具有 DropDownList s `ListItem` s 显示`CategoryName`数据字段中，使用`CategoryID`作为其值的数据字段。
- `SupplierName` 添加 DropDownList，并设置其`ID`到`NewSupplierID`。 将其绑定到名为新 ObjectDataSource`SuppliersDataSource`并将其配置为使用`SuppliersBLL`类的`GetSuppliers()`方法。 具有 DropDownList s `ListItem` s 显示`CompanyName`数据字段中，使用`SupplierID`作为其值的数据字段。

对于每个验证控件，清除`ForeColor`属性，以便`FooterStyle`CSS 类 s 白色的前景颜色将代替默认红色。 此外使用`ErrorMessage`属性的详细说明，但设置`Text`为星号的属性。 若要防止验证控件的文本导致换行到两行的插入接口，设置`FooterStyle`s`Wrap`属性设置为 false 的每个`FooterTemplate`的验证控件。 最后，添加验证摘要控件下方的 GridView 并设置其`ShowMessageBox`属性设置为`true`并将其`ShowSummary`属性设置为`false`。

在添加新产品时，我们需要提供`CategoryID`和`SupplierID`。 捕获此信息通过中的页脚单元 Dropdownlist`CategoryName`和`SupplierName`字段。 我选择使用这些字段而不是`CategoryID`和`SupplierID`Templatefield 因为网格的数据行用户是可能更希望中看到的类别和供应商名称而不是它们的 ID 值。 由于`CategoryID`并`SupplierID`中现在正在捕获值`CategoryName`并`SupplierName`字段 s 插入接口，我们可以删除`CategoryID`和`SupplierID`Templatefield 从 GridView。

同样，`ProductID`添加一个新产品时不使用因此`ProductID`TemplateField 可以也删除。 但是，让我们来保留`ProductID`字段在网格中。 除了文本框、 Dropdownlist、 复选框，并验证控件的插入接口，我们还需要添加按钮，单击时，执行逻辑，以向数据库添加新的产品。 在步骤 4 中，我们将包含插入界面中的添加按钮`ProductID`TemplateField 的`FooterTemplate`。

随意改善各 GridView 字段的外观。 例如，你可能想要设置格式`UnitPrice`值作为一种货币，右对齐`UnitsInStock`， `UnitsOnOrder`，和`ReorderLevel`字段中，并更新`HeaderText`Templatefield 的值。

创建插入接口中的大量后`FooterTemplate`s，删除`SupplierID`，和`CategoryID`Templatefield，并提高通过格式和对齐方式 Templatefield，您声明性的 GridView s 网格的美学标记应类似于下面所示：


[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample5.aspx)]

当通过浏览器中查看，GridView 的脚注行现在将包括已完成插入接口 （请参阅图 10）。 此时，插入的接口不包括一个使用户以指示该她 s 输入数据的新产品并想要将新记录插入到数据库。 此外，我们 ve 有待解决如何输入到页脚中的数据将转换为新记录中`Products`数据库。 我们将介绍如何将包含插入界面添加按钮和如何对执行代码的步骤 4 中回发时它 s 单击。 第 5 步演示如何插入新记录使用在页脚中的数据。


[![GridView 页脚提供用于添加新记录的接口](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image17.png)

**图 10**: GridView 页脚提供用于添加新记录的接口 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image18.png))


## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>步骤 4： 插入界面中包括的添加按钮

我们需要的添加按钮位置在接口中包含插入因为当前插入接口的页脚行 s 中没有用户指出他们已完成输入新的产品的信息的方式。 这可以放在一个现有`FooterTemplate`s 或我们可以添加一个新列在网格实现此目的。 对于本教程中，let s 将放在添加按钮`ProductID`TemplateField 的`FooterTemplate`。

从设计器中，单击 GridView s 智能标记中的编辑模板链接，然后选择`ProductID`字段的`FooterTemplate`从下拉列表。 将按钮 Web 控件 （或 LinkButton 或 ImageButton，如果您愿意） 添加到模板，将其 ID 设置为`AddProduct`，将其`CommandName`插入，并将其`Text`属性设置为添加如图 11 中所示。


[![置于 ProductID TemplateField 的要添加按钮](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image19.png)

**图 11**： 将放置在添加按钮`ProductID`TemplateField s `FooterTemplate` ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image20.png))


一旦您已包括添加按钮，测试浏览器中的页。 请注意，单击添加按钮包含无效的数据插入接口后，简单地说 circuited 回发并且 ValidationSummary 控件表示无效的数据 （请参阅图 12）。 输入适当的数据，单击添加按钮会导致回发。 没有记录添加到数据库，但是。 我们需要编写一些代码来实际执行插入。


[![添加按钮 s 回发是短 Circuited 如果插入界面中存在无效数据](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image21.png)

**图 12**: 添加按钮 s 回发是短 Circuited 如果插入界面中存在无效数据 ([单击以查看实际尺寸的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image22.png))


> [!NOTE]
> 插入的接口中的验证控件不被分配给验证组。 这很有效，只要插入接口是唯一一页上的验证控件组。 如果，但是，有其他验证控件 （如网格 s 编辑界面中的验证控件） 页上，验证控件中插入接口，并添加按钮的`ValidationGroup`属性应分配相同的值作为 so 到将这些控件与特定的验证组相关联。 请参阅[仔细分析 ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)有关分区的验证控件和页上的按钮为验证组的详细信息。


## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>步骤 5： 插入新记录到`Products`表

当使用 GridView 的内置编辑功能，GridView 自动处理所有执行更新所需的工作。 具体而言，单击更新按钮时它将复制从编辑界面输入到中的 ObjectDataSource s 的参数的值`UpdateParameters`集合，并通过调用 ObjectDataSource s 的更新，将启动`Update()`方法。 由于 GridView 不提供此类用于插入的内置功能，我们必须实现调用 ObjectDataSource 的代码`Insert()`方法，并为 ObjectDataSource s 接口中插入的值的副本`InsertParameters`集合.

单击添加按钮后，应执行此插入逻辑。 如中所述[添加和响应 GridView 中的按钮的](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs.md)教程中，只要按钮、 LinkButton 或在 GridView 中的 ImageButton 单击时，GridView 的`RowCommand`在回发事件触发。 是否按钮、 LinkButton、 ImageButton 已添加或显式如脚注行中的添加按钮或者如果它已自动添加通过 GridView，就会触发此事件 (如选中启用排序后，每个列顶部的 Linkbutton 或Linkbutton 在分页界面选择启用分页时)。

因此，若要响应用户单击添加按钮，我们需要创建的事件处理程序的 GridView s`RowCommand`事件。 由于此事件时将触发*任何*单击按钮、 LinkButton 或 ImageButton GridView 中的后，它 s 重要，我们即可继续进行插入的逻辑如果`CommandName`属性传递给事件处理程序映射到`CommandName`添加按钮 （插入） 的值。 此外，我们也只在才继续验证控件报告有效的数据。 若要解决此问题，创建的事件处理程序`RowCommand`事件使用以下代码：


[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample6.cs)]

> [!NOTE]
> 您可能想知道为什么事件处理程序很麻烦检查`Page.IsValid`属性。 毕竟，如果插入的界面中提供无效的数据，则取消获胜的 t 回发？ 这种假设是正确的只要用户未禁用 JavaScript，或采取了一些措施来绕过客户端验证逻辑。 简单地说，一个应永远不会依赖于严格客户端验证;应始终处理数据之前执行服务器端检查的有效性。


我们在步骤 1 中创建`ProductsDataSource`ObjectDataSource，以便其`Insert()`方法映射到`ProductsBLL`类的`AddProduct`方法。 要插入到新的记录`Products`表中，我们可以只需调用 ObjectDataSource 的`Insert()`方法：


[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample7.cs)]

既然`Insert()`调用方法，所有要插入的接口的值复制到的参数就是传递给`ProductsBLL`类的`AddProduct`方法。 返回中可以看到[检查与插入、 更新和删除的事件相关联](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)教程中，可以通过 ObjectDataSource 的`Inserting`事件。 在中`Inserting`我们需要以编程方式引用中的所有控件的事件`Products`GridView 的页脚行，并将分配到其值`e.InputParameters`集合。 如果用户省略一个值，例如离开`ReorderLevel`文本框留空，我们需要指定插入到数据库中的值应为`NULL`。 由于`AddProducts`方法接受为空的数据库字段为 null 的类型，只需使用可以为 null 的类型并将其值设置为`null`中其中省略用户输入的情况。


[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample8.cs)]

与`Inserting`事件处理程序已完成，新的记录可以添加到`Products`通过 GridView 的脚注行的数据库表。 请继续并尝试添加几个新产品。

## <a name="enhancing-and-customizing-the-add-operation"></a>增强和自定义添加操作

目前，单击添加按钮将新记录添加到数据库表，但不提供任何类型的可视反馈，已成功添加记录。 理想情况下，标签 Web 控件或客户端的警告框会通知用户其插入已成功完成。 我将此当作练习留给读者。

本教程中使用 GridView 不适用于任何排序顺序列出的产品，也不允许最终用户对数据进行排序。 因此，记录进行排序，因为它们位于其主键字段的数据库。 由于每个新记录具有`ProductID`大于最后一个，每次添加一个新的产品时它附加在网格的最终值。 因此，你可能想要自动将用户发送到 GridView 的最后一页，添加一条新记录后。 这可以通过调用后面添加以下代码行来实现`ProductsDataSource.Insert()`在`RowCommand`事件处理程序，以指示用户需要发送的最后一页之后将数据绑定到 GridView:


[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample9.cs)]

`SendUserToLastPage` 最初的页级布尔变量分配值为`false`。 在 GridView`DataBound`事件处理程序，如果`SendUserToLastPage`为 false，`PageIndex`属性进行更新，将用户发送到的最后一页。


[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample10.cs)]

原因`PageIndex`属性中设置`DataBound`事件处理程序 (而不是`RowCommand`事件处理程序) 是因为当`RowCommand`事件处理程序会触发我们 ve 尚未若要向其中添加新记录`Products`数据库表。 因此，在`RowCommand`事件处理程序的最后一页索引 (`PageCount - 1`) 表示最后一个页面索引*之前*已添加的新产品。 对于要添加的产品的大多数，最后一页索引是相同的后添加的新产品。 但是，当添加一项产品产生在新的最后一页索引中，如果我们不正确地更新`PageIndex`在`RowCommand`事件处理程序，我们将转到第二个到最后一页 （添加新产品之前的最后一个页面索引） 而不是新的最后一页 index。 由于`DataBound`事件处理程序触发已添加的新产品并将数据重新绑定到网格中，通过设置之后`PageIndex`那里的属性我们知道我们获取正确的最后一页索引。

最后，本教程中使用这个 GridView 已经有多个字段必须为添加的新产品，收集得很宽。 由于此宽度 DetailsView s 垂直布局可能是首选。 GridView s 可收集较少的输入通过减少总体宽度。 我们可能不需要收集`UnitsOnOrder`， `UnitsInStock`，和`ReorderLevel`字段添加一个新产品时从 GridView 中，在这种情况下无法删除这些字段。

若要调整收集的数据，我们可以使用两种方法之一：

- 继续使用`AddProduct`的值的方法`UnitsOnOrder`， `UnitsInStock`，和`ReorderLevel`字段。 在`Inserting`事件处理程序，提供硬编码，默认值用于已从插入接口中删除这些输入。
- 创建的新重载`AddProduct`中的方法`ProductsBLL`类不接受的输入`UnitsOnOrder`， `UnitsInStock`，和`ReorderLevel`字段。 然后，在 ASP.NET 页中，配置对象数据源以使用此新的重载。

同样也可以选择任一选项。 在过去的教程我们使用后一种选择，创建多个重载`ProductsBLL`类的`UpdateProduct`方法。

## <a name="summary"></a>总结

GridView 缺少 DetailsView 和 FormView 中, 找到的内置插入功能，但使用大量的精力插入接口可以添加到的脚注行。 若要只需在 GridView 中显示脚注行设置其`ShowFooter`属性设置为`true`。 添加插入到界面和页脚行内容可以自定义为每个字段通过将字段转换为 TemplateField `FooterTemplate`。 正如我们在本教程中，看到`FooterTemplate`可以包含按钮、 文本框、 Dropdownlist、 复选框，用于填充数据驱动的 Web 控件 （如 Dropdownlist)，数据源控件和验证控件。 以及用于收集用户的输入控件，需要添加按钮、 LinkButton 或 ImageButton。

单击添加按钮时，ObjectDataSource 的`Insert()`方法调用以启动插入工作流。 ObjectDataSource 然后调用配置的 insert 方法 (`ProductsBLL`类的`AddProduct`方法，在本教程中)。 我们必须将值插入到 ObjectDataSource 的接口的 GridView s 从复制`InsertParameters`集合之前被调用 insert 方法。 这可以通过以编程方式引用的 ObjectDataSource s 中插入的界面 Web 控件来实现`Inserting`事件处理程序。

本教程中完成增强 GridView 的外观的技术产品的外观。 教程的下一步一将介绍如何使用如图像、 Pdf、 Word 文档、 二进制数据和其他操作和数据 Web 控件。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已伯纳黛特 Leigh。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-a-gridview-column-of-checkboxes-cs.md)
> [下一页](adding-a-gridview-column-of-radio-buttons-vb.md)
