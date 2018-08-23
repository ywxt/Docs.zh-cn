---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: 添加 GridView 列的复选框 (C#) |Microsoft Docs
author: rick-anderson
description: 本教程讨论如何将复选框的列添加到 GridView 控件，以便为用户提供的选择多个行的 G.以直观的方式...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: 1921ceeb33197299f3cedb0eef082af0fd8fa960
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832905"
---
<a name="adding-a-gridview-column-of-checkboxes-c"></a>添加 GridView 列的复选框 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe)或[下载 PDF](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> 本教程介绍如何将复选框的列添加到 GridView 控件，以便为用户提供的选择多个行的 GridView 以直观的方式。


## <a name="introduction"></a>介绍

在前面的教程中，我们将探讨如何将单选按钮的列添加到用于选择特定记录 GridView。 当用户从网格中进行选择最多一项限制时，单选按钮的列是合适的用户界面。 有时，但是，我们可能想要允许用户选择任意数目的网格中的项。 例如，基于 web 的电子邮件客户端，通常显示的复选框列包含的消息列表。 用户可以选择任意数目的消息，然后执行一些操作，如电子邮件移动到另一个文件夹或删除它们。

在本教程中，我们将了解如何添加复选框列以及如何确定哪些复选框已选中在回发。 具体而言，我们将构建的示例，精确模拟基于 web 的电子邮件客户端用户界面。 我们的示例中将包括一个列表中的产品的分页的 GridView`Products`数据库表中每个复选框为行 （请参阅图 1）。 删除所选产品按钮，单击时，将删除所选的那些产品。


[![每个产品行包含一个复选框](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**图 1**： 每个产品行包含一个复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png))


## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>步骤 1： 添加分页的 GridView，其中列出了产品信息

我们担心如何添加复选框列之前，让 s 上列出的产品支持分页的 GridView 中的第一个焦点。 首先打开`CheckBoxField.aspx`页中`EnhancedGridView`文件夹，然后拖动 GridView 从工具箱拖到设计器中，设置其`ID`到`Products`。 接下来，选择要绑定到名为新对象数据源的 GridView `ProductsDataSource`。 配置要使用 ObjectDataSource`ProductsBLL`类，调用`GetProducts()`方法以返回数据。 由于此 GridView 将是只读的设置下拉列表中插入、 更新和删除选项卡添加到 （无）。


[![创建名为 ProductsDataSource 新 ObjectDataSource](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**图 2**： 创建新对象数据源命名`ProductsDataSource`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))


[![配置对象数据源检索数据使用 GetProducts() 方法](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**图 3**： 配置检索数据使用 ObjectDataSource`GetProducts()`方法 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))


[![设置下拉列表中插入、 更新和删除选项卡为 （无）](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**图 4**： 设置下拉列表列出了在更新、 插入和删除选项卡中为 （无） ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))


完成配置数据源向导后，Visual Studio 将自动创建 BoundColumns 和 CheckBoxColumn 与产品相关的数据字段。 如我们在上一教程，请删除以外的所有`ProductName`， `CategoryName`，并`UnitPrice`BoundFields，并将更改`HeaderText`产品、 类别和价格的属性。 配置`UnitPrice`BoundField 以便其值设置为货币的格式。 此外配置 GridView 支持分页，通过从智能标记的启用分页复选框。

允许 s 还将添加用于删除所选的产品的用户界面。 添加 GridView 中，设置下的一个按钮 Web 控件及其`ID`到`DeleteSelectedProducts`并将其`Text`删除所选产品的属性。 而不是实际从数据库中删除产品，此示例中我们将只显示一条消息指出已删除的产品。 若要解决此问题，将添加在按钮下方的标签 Web 控件。 将其 ID 设置为`DeleteResults`，清除出其`Text`属性，并设置其`Visible`并`EnableViewState`属性设置为`false`。

进行这些更改后，应类似于以下的 GridView、 对象数据源、 按钮和标签 s 声明性标记：


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

请花费片刻时间浏览器中查看该页面 （请参见图 5）。 此时应看到名称、 类别和价格的前十个产品。


[![列出名称、 类别和第十个产品的价格](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**图 5**： 列出的名称、 类别和第十个产品的价格 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png))


## <a name="step-2-adding-a-column-of-checkboxes"></a>步骤 2： 添加的列的复选框

由于 ASP.NET 2.0 包括 CheckBoxField，有人可能认为它可以用于将复选框列添加到 GridView。 遗憾的是，不这样，如 CheckBoxField 设计为使用布尔数据字段。 也就是说，为了使用 CheckBoxField 我们必须指定其值以确定是否检查呈现复选框可查阅的基础数据字段。 我们不能使用 CheckBoxField 只需包含的列取消选中复选框。

相反，我们必须添加 TemplateField 和复选框 Web 控件添加到其`ItemTemplate`。 请继续并添加到 TemplateField `Products` GridView，并使其第一个 （最左侧） 字段。 从 GridView s 智能标记，单击编辑模板链接，并从工具箱拖到将复选框 Web 控件`ItemTemplate`。 设置此复选框 s`ID`属性设置为`ProductSelector`。


[![添加名为 TemplateField 的 ItemTemplate 的 ProductSelector 的复选框 Web 控件](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**图 6**： 添加复选框 Web 控件命名为`ProductSelector`为 TemplateField s `ItemTemplate` ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png))


与添加的 TemplateField 和复选框 Web 控件，每个行现在包含一个复选框。 图 7 显示了此页上，添加了 TemplateField 和复选框后，通过浏览器中，查看时。


[![每个产品行现在包含一个复选框](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**图 7**： 每个产品行现在包含一个复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png))


## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>步骤 3： 确定哪些复选框已选中在回发

现在我们具有一个列的复选框，但无法确定哪些复选框已选中在回发。 单击删除所选产品按钮时，不过，我们需要知道哪些复选框已选中状态，以便删除这些产品。

GridView s [ `Rows`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx)提供对 GridView 中的数据行的访问。 我们可以循环访问这些行，以编程方式访问复选框控件，并请查阅其`Checked`属性来确定是否已选中该复选框。

创建事件处理程序`DeleteSelectedProducts`Button Web 控件的`Click`事件，并添加以下代码：


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

`Rows`属性返回的集合`GridViewRow`实例该构成 GridView 的数据行。 `foreach`此处循环枚举此集合。 每个`GridViewRow`对象，以编程方式使用访问行 s 复选框`row.FindControl("controlID")`。 如果选中此复选框，行 s 对应`ProductID`值从检索`DataKeys`集合。 在此练习中，我们只是显示信息性消息中的`DeleteResults`标签，尽管我们 d 改为工作应用程序中进行调用`ProductsBLL`类的`DeleteProduct(productID)`方法。

与此事件处理程序添加后，单击删除所选产品按钮现在显示`ProductID`s 的所选产品。


[![单击删除所选产品按钮时列出所选产品 Productid](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**图 8**： 当删除所选产品在单击按钮选择产品`ProductID`列 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png))


## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>步骤 4： 添加检查所有并取消选中所有按钮

如果用户想要删除当前页上的所有产品，它们必须检查每个 10 个复选框。 我们可以帮助加快此过程通过添加检查所有按钮，单击时，在网格中选择所有复选框。 取消选中所有按钮将都会同样有用。

将两个按钮 Web 控件添加到页上，将其置于上方 GridView。 设置第一个 s`ID`到`CheckAll`并将其`Text`属性设置为检查所有; 将设置第二个 s`ID`到`UncheckAll`并将其`Text`取消选中所有属性。


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

接下来，创建名为的代码隐藏类中的一种方法`ToggleCheckState(checkState)`，调用时，枚举`Products`GridView s`Rows`集合，并设置每个复选框 s`Checked`属性设置为与传递的值在*checkState*参数。


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

接下来，创建`Click`事件处理程序`CheckAll`和`UncheckAll`按钮。 在中`CheckAll`s 事件处理程序，只需调用`ToggleCheckState(true)`; 在`UncheckAll`，调用`ToggleCheckState(false)`。


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

使用此代码中，单击查看全部按钮导致回发，并会检查所有 GridView 中的复选框。 同样，单击取消选中所有取消选择所有复选框。 图 9 在选中全部查看按钮后显示的屏幕。


[![单击全部按钮的检查会选择所有复选框](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**图 9**： 单击检查所有按钮选择所有复选框 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png))


> [!NOTE]
> 当显示的列的复选框，选中或取消选中所有复选框的一种方法是通过标题行中的复选框。 此外，当前全选/取消选中所有实现所都需的回发。 复选框可以选中或取消选中之后，但是，完全通过客户端脚本，从而提供了更为迅捷的用户体验。 若要了解详细信息，以及使用客户端技术的讨论中的所有检查和取消选中所有使用标头行复选框签出[GridView 使用客户端脚本和选中所有复选框中选中所有复选框](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)。


## <a name="summary"></a>总结

在需要使用户可以继续操作之前 GridView 从选择任意数目的行的情况下，添加复选框列是一个选项。 正如我们看到在本教程中，包括的列的 GridView 中的复选框时，需要添加一个复选框 Web 控件使用 TemplateField。 通过使用 Web 控件 （而不是与我们在上一教程中，直接在模板中，插入标记） ASP.NET 自动记住复选框已和不在回发之间签入。 我们可以以编程方式访问中的复选框的代码以确定是否检查给定的复选框，或更改的选中的状态。

本教程，最后一个介绍了添加到 GridView 行选择器列。 在我们的下一教程中，我们将介绍如何操作，请使用少量的工作，我们可以插入将功能添加到 GridView。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](adding-a-gridview-column-of-radio-buttons-cs.md)
> [下一页](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
