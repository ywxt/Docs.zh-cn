---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
title: 添加 GridView 列的单选按钮 (C#) |Microsoft Docs
author: rick-anderson
description: 本教程讨论如何将单选按钮的列添加到 GridView 控件，以便为用户提供更直观的方式选择的单个行的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 32377145-ec25-4715-8370-a1c590a331d5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
msc.type: authoredcontent
ms.openlocfilehash: 1e1691b3c0c5fb576f25b84e8f4d7125a8d0c698
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366911"
---
<a name="adding-a-gridview-column-of-radio-buttons-c"></a>添加 GridView 列的单选按钮 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_CS.exe)或[下载 PDF](adding-a-gridview-column-of-radio-buttons-cs/_static/datatutorial51cs1.pdf)

> 本教程介绍如何将单选按钮的列添加到 GridView 控件，以便为用户提供选择的 GridView 的单个行的更直观的方式。


## <a name="introduction"></a>介绍

GridView 控件提供了大量的内置功能。 它包括多个用于显示文本、 图像、 超链接和按钮的不同字段。 它支持进一步的自定义的模板。 只需单击几下鼠标，它可能使其中的每一行可以选择通过一个按钮，GridView 或启用编辑或删除功能的 s。 尽管数不清的提供的功能，通常会在其中附加，不支持的功能将需要添加的情况。 在本教程和下一步的两个我们将介绍如何增强 GridView 的功能，以包括其他功能。

本教程和下一个侧重于增强行选择过程。 检查中作为[母版/详细信息使用详细信息 DetailView 的可选母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)，我们可以将 CommandField 添加到 GridView 包含选择按钮。 单击时，回发时，才会和 GridView 的`SelectedIndex`属性更新为其选择按钮被单击的行的索引。 在中[母版/详细信息使用详细信息 DetailView 的可选母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程，我们已了解如何使用此功能可显示所选的 GridView 行的详细信息。

当选择按钮在许多情况下，它可能无法为其他人也工作。 而不是使用一个按钮，两个其他用户界面元素通常用于进行选择： 单选按钮和复选框。 因此，而不是选择按钮，每一行都包含单选按钮或复选框，我们可以提供 GridView。 在其中用户可以仅选择一个 GridView 记录的情况下，单选按钮可能选择按钮上方首选。 可以在其中用户可能选择的情况下在如基于 web 的电子邮件应用程序，用户可能想要选择要删除相应的复选框的多个消息中的多个记录提供了不是可从选择按钮或单选按钮的功能用户界面。

本教程介绍如何将单选按钮的列添加到 GridView。 继续下一步教程将探讨如何使用复选框。

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>步骤 1： 创建增强 GridView 网页

增强 GridView，其中包括的单选按钮列在开始之前，让我们来先花点时间在我们的网站项目，我们需要为本教程和下一步的两个创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`EnhancedGridView`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`


![将 ASP.NET 页面添加与 SqlDataSource 相关的教程](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.gif)

**图 1**： 将 ASP.NET 页面添加与 SqlDataSource 相关的教程


在其他文件夹中，喜欢`Default.aspx`在`EnhancedGridView`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.png))


最后，将这四个页面添加到条目为`Web.sitemap`文件。 具体而言，在使用后添加以下标记 SqlDataSource 控件`<siteMapNode>`:


[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含用于编辑、 插入和删除教程的项。


![站点图现在包括用于增强 GridView 教程项](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.gif)

**图 3**： 站点图现在包括用于增强 GridView 教程项


## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>步骤 2： 在 GridView 中显示供应商

对于本教程让我们来构建一个 GridView，与提供的单选按钮，每个 GridView 行列出了从美国，供应商。 选择通过单选按钮的供应商提供之后, 用户可以通过单击一个按钮查看供应商的产品。 此任务可能听起来很简单，虽然有大量使其特别棘手的微妙之处。 我们深入了解这些细节之前，让 s 首先会出现一个 GridView，列出供应商。

首先打开`RadioButtonField.aspx`页中`EnhancedGridView`通过将 GridView 从工具箱拖到设计器的文件夹。 设置 GridView s`ID`到`Suppliers`和从其智能标记上，选择创建新的数据源。 具体而言，创建名为 ObjectDataSource`SuppliersDataSource`提取其数据从`SuppliersBLL`对象。


[![创建名为 SuppliersDataSource 新 ObjectDataSource](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.png)

**图 4**： 创建新对象数据源命名`SuppliersDataSource`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.png))


[![配置对象数据源以使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.png)

**图 5**： 配置为使用 ObjectDataSource`SuppliersBLL`类 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.png))


由于我们只想要列出这些供应商在 USA 中的，选择`GetSuppliersByCountry(country)`从下拉列表中选择的选项卡的方法。


[![配置对象数据源以使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.png)

**图 6**： 配置为使用 ObjectDataSource`SuppliersBLL`类 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.png))


从更新选项卡，选择 （无） 选项，并单击下一步。


[![配置对象数据源以使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.png)

**图 7**： 配置为使用 ObjectDataSource`SuppliersBLL`类 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.png))


由于`GetSuppliersByCountry(country)`方法接受参数、 配置数据源向导提示我们输入该参数的源。 若要指定硬编码的值 （美国，在此示例中），将源下拉列表设置为 None，在文本框中输入的默认值的参数。 单击完成以完成向导。


[![使用默认值作为美国国家/地区参数](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.png)

**图 8**： 使用默认值为美国`country`参数 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.png))


完成向导后，GridView 将每个供应商数据字段包含 BoundField。 删除以外的所有`CompanyName`， `City`，并`Country`BoundFields，并将重命名`CompanyName`BoundFields`HeaderText`向供应商的属性。 这样做之后，应类似于以下的 GridView 和 ObjectDataSource 的声明性语法。


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample2.aspx)]

对于本教程，让我们来允许用户查看所选的供应商的产品与供应商列表中，相同的页面或不同的页上。 若要解决此问题，请向页面添加两个按钮 Web 控件。 我 ve 集`ID`到这两个按钮的 s`ListProducts`和`SendToProducts`，这样的想法，当`ListProducts`单击将发生回发，并且将在同一页上，但是当列出所选供应商的产品`SendToProducts`单击时，用户将 whisked 到的另一个页面中列出的产品。

图 9 显示了`Suppliers`GridView 和两个按钮 Web 控件的浏览器查看时。


[![从美国这些供应商有其名称、 城市和国家/地区信息列出](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.png)

**图 9**： 这些供应商 USA 具有及其名称、 城市和国家/地区列出的信息 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.png))


## <a name="step-3-adding-a-column-of-radio-buttons"></a>步骤 3： 添加单选按钮的列

此时`Suppliers`GridView 有三个 BoundFields 在 USA 中显示公司名称、 城市和国家/地区的每个供应商。 它仍然但是缺少单选按钮的列。 遗憾的是，GridView 不包括内置 RadioButtonField，否则为我们可能只需将它添加到网格并完成。 相反，我们可以添加 TemplateField 并配置其`ItemTemplate`呈现单选按钮，从而导致每个 GridView 行的单选按钮。

最初，我们可能认为，可以通过添加到 RadioButton Web 控件实现所需的用户界面`ItemTemplate`TemplateField。 虽然这确实将添加到 GridView 中的每一行的单个单选按钮，单选按钮无法分组在一起，并因此不互相排斥。 也就是说，最终用户是能够从 GridView 中同时选择多个单选按钮。

即使使用 TemplateField RadioButton Web 控件不提供我们所需的功能，让 s 实现这种方法，因为它 s 物有所值来检查生成的单选按钮未分组的原因。 首先，通过添加 TemplateField 到供应商 GridView，使其最左边的字段。 接下来，从 GridView s 智能标记，单击编辑模板链接并将 RadioButton Web 控件从工具箱拖到 TemplateField 的`ItemTemplate`（请参阅图 10）。 设置 RadioButton s`ID`属性设置为`RowSelector`并`GroupName`属性设置为`SuppliersGroup`。


[![将单选按钮 Web 控件添加到 ItemTemplate](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.png)

**图 10**： 添加到 RadioButton Web 控件`ItemTemplate`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.png))


以后进行通过设计器的这些新增功能，您的 GridView 的标记看起来应类似于以下：


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample3.aspx)]

RadioButton s [ `GroupName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx)什么是用于将一系列单选按钮。 具有相同的所有单选按钮控件`GroupName`值被视为分组; 只有一个单选按钮可以一次选择从一个组。 `GroupName`属性指定的值呈现的单选按钮的`name`属性。 在浏览器将检查单选按钮`name`属性来确定单选按钮分组。

与 RadioButton Web 控件添加到`ItemTemplate`，请访问此页上的通过浏览器，然后单击网格的行中的单选按钮。 请注意，如何未分组的单选按钮，从而可以选择的所有行，作为图 11 显示了。


[![GridView 的单选按钮是不分组在一起](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.png)

**图 11**： 的 GridView 的单选按钮是不分组在一起 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.png))


未分组的单选按钮的原因在于其呈现`name`属性是不同的尽管具有相同`GroupName`属性设置。 若要查看这些差异，请通过浏览器的执行视图/源代码并检查单选按钮标记：


[!code-html[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample4.html)]

请注意这两种`name`并`id`属性不在属性窗口中指定的确切值，但前面带有数目的其他`ID`值。 附加`ID`值添加到前面的呈现`id`并`name`属性是`ID`的单选按钮的父控件`GridViewRow`s `ID` s，GridView 的`ID`、内容控件 s `ID`，和 Web 窗体的`ID`。 这些`ID`s 添加，以便每个呈现 GridView 中的 Web 控件具有一个唯一`id`和`name`值。

每个呈现控制需求不同`name`和`id`由于这是如何在浏览器唯一地标识客户端和如何它标识为 web 服务器的操作的每个控件或在回发发生更改。 例如，假设我们想要每次 RadioButton s 签状态发生了更改时运行一些服务器端代码。 我们来实现这一点通过设置 RadioButton s`AutoPostBack`属性设置为`true`创建的事件处理程序和`CheckChanged`事件。 但是，如果呈现`name`和`id`值的所有单选按钮是相同的在回发我们无法确定哪些特定于单选按钮被单击。

简言之，就是我们不能在 GridView 使用 RadioButton Web 控件中创建的单选按钮的列。 相反，我们必须使用而不是陈旧的技术来确保相应的标记注入到每个 GridView 行。

> [!NOTE]
> 像 RadioButton Web 控件，单选按钮 HTML 控件时添加到模板，将包括的唯一`name`属性，在未分组的网格中进行的单选按钮。 如果您不熟悉 HTML 控件，随时将忽略此请注意，HTML 控件都很少使用，尤其是在 ASP.NET 2.0。 但如果您有兴趣学习的详细信息，请参阅[K.Scott Allen](http://odetocode.com/blogs/scott/default.aspx)的博客条目[Web 控件和 HTML 控件](http://www.odetocode.com/Articles/348.aspx)。


## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>使用文本控件将单选按钮标记

为了正确地将所有内 GridView 单选按钮的组合，我们需要手动插入到的单选按钮标记`ItemTemplate`。 每个单选按钮需要相同`name`属性，但应具有一个唯一`id`属性 （如果我们想要访问通过客户端脚本的单选按钮）。 在浏览器用户选择的单选按钮和回发的页面后，将发送回的选定的单选按钮的值`value`属性。 因此，每个单选按钮将需要一个唯一`value`属性。 最后，在回发时我们需要确保添加`checked`属性到后选中了，否则用户进行的选项并返回文章的一个单选按钮、 单选按钮将返回到其默认状态 （所有未选定）。

有两种方法，可以采取措施将低级别标记注入到模板。 一个是执行多个标记和调用格式设置方法的代码隐藏类中定义。 此方法首先中所述[GridView 控件中使用 Templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)教程。 在本例中它可能如下所示：


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample5.aspx)]

在这里，`GetUniqueRadioButton`并`GetRadioButtonValue`会返回相应的代码隐藏类中定义的方法`id`和`value`属性值为每个单选按钮。 这种方法非常适用于将分配`id`并`value`属性，但不如人意时无需指定`checked`属性值，因为数据绑定语法仅执行时数据首先绑定到 GridView。 因此，如果这个 GridView 有启用视图状态，格式设置方法将仅时，会激发第一次加载页面 （或当 GridView 显式重新绑定到数据源），因此设置的函数和`checked`上调用结束-赢得 t 属性回发。 它 s 相当微妙的问题和有点超出了本文中，因此，我将保留在此范围。 但是，我执行鼓励您尝试使用上述方法，通过，其中将有疑问的点到工作。 虽然此类练习结束-赢得不能获得您更加接近的有效版本，它将帮助培养 GridView 和数据绑定生命周期的更深入地了解。

注入自定义的其他方法，低级别标记中的模板和本教程中，我们将使用的方法是添加[文本控件](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx)到模板。 然后，在 GridView s`RowCreated`或`RowDataBound`事件处理程序，可以以编程方式访问文字控件并将其`Text`属性设置为标记发出。

首先删除单选按钮从 TemplateField 的`ItemTemplate`，替换文字控件。 设置文本控件 s`ID`到`RadioButtonMarkup`。


[![将文本控件添加到 ItemTemplate](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.png)

**图 12**： 添加到文字控件`ItemTemplate`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.png))


接下来，创建事件处理程序的 GridView s`RowCreated`事件。 `RowCreated`事件触发后对于每个添加的行，该值指示是否数据正在重新绑定到 GridView。 这意味着，即使在回发时从视图状态重新加载数据`RowCreated`仍会触发事件，这是我们将使用它而不是原因`RowDataBound`（这会触发仅当数据显式绑定到数据 Web 控件）。

在此事件处理程序中，我们只想如果能继续进行我们重新处理数据行。 我们想要以编程方式引用每个数据行`RadioButtonMarkup`文本控件并设置其`Text`属性设置为用于发出的标记。 发出的标记如以下代码所示，创建单选按钮的`name`属性设置为`SuppliersGroup`，其`id`属性设置为`RowSelectorX`，其中*X*是 GridView 行的索引并且其`value`属性设置为 GridView 行的索引。


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample6.cs)]

当选择某个 GridView 行并为在回发时，我们感兴趣`SupplierID`的所选的供应商。 因此，有人可能认为，每个单选按钮的值应为实际`SupplierID`（而不是 GridView 行的索引）。 虽然这在某些情况下，将会带来安全风险会盲目地接受并处理`SupplierID`。 我们 GridView，例如，列出了仅在 USA 中的这些供应商。 但是，如果`SupplierID`直接从单选按钮，新增功能停止淘气用户从操作传递`SupplierID`发送回在回发值？ 通过使用作为行索引`value`，然后`SupplierID`在回发时从`DataKeys`集合中，我们可以确保用户只能使用其中一个`SupplierID`GridView 行之一相关联的值。

添加此事件处理程序代码后，花点时间查看页在浏览器中测试。 首先，请注意，只有一个单选按钮在网格中可以一次选择。 但是，当选择的单选按钮，然后单击其中一个按钮，产生的回发，并且所有单选按钮都恢复为其初始状态 （即，在回发时，选定的单选按钮将不再选择）。 若要解决此问题，我们需要扩充`RowCreated`事件处理程序，因此它会检查发送的回发的选定的单选按钮索引并将添加`checked="checked"`行索引匹配项的发出标记的属性。

当发生回发时，浏览器发送回`name`和`value`的选定的单选按钮。 检索的值可以以编程方式使用`Request.Form["name"]`。 [ `Request.Form`属性](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx)提供[ `NameValueCollection` ](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx)表示窗体变量。 窗体变量是名称和在网页中的窗体字段的值和每当回发时，才会发送回的 web 浏览器。 因为呈现`name`GridView 中的单选按钮的属性是`SuppliersGroup`，当 web 页面被发送的回浏览器会将`SuppliersGroup=valueOfSelectedRadioButton`返回到 web 服务器 （以及其他窗体字段）。 从可以访问此信息`Request.Form`属性使用： `Request.Form["SuppliersGroup"]`。

因为我们将需要确定选定的单选按钮索引不能仅在`RowCreated`事件处理程序，但在`Click`按钮 Web 控件的事件处理程序，让 s 添加`SuppliersSelectedIndex`属性设置为返回的代码隐藏类`-1`如果已选择不单选按钮和所选的索引，如果选择了一个单选按钮。


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample7.cs)]

通过添加此属性，我们知道要添加`checked="checked"`中的标记`RowCreated`事件处理程序时`SuppliersSelectedIndex`等于`e.Row.RowIndex`。 更新要将此逻辑包含的事件处理程序：


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample8.cs)]

进行此更改后，所选的单选按钮可以在回发后处于选定状态。 现在，我们已能够指定哪些单选按钮处于选中状态，我们无法更改的行为，以便当首次访问页面，选择第一个 GridView 行的单选按钮 （而不是有没有默认情况下选择的单选按钮，即当前行为）。 若要让默认情况下选择第一个单选按钮，只需更改`if (SuppliersSelectedIndex == e.Row.RowIndex)`以下语句： `if (SuppliersSelectedIndex == e.Row.RowIndex || (!Page.IsPostBack && e.Row.RowIndex == 0))`。

现在我们已添加到允许单个 GridView 行选择并记住跨回发的 GridView 的分组的单选按钮的列。 我们下一步是要显示的所选的供应商提供的产品。 在步骤 4 中我们将了解如何将用户重定向到另一个页面，沿所选发送`SupplierID`。 在步骤 5 中，我们将了解如何在同一页面上 GridView 中显示所选供应商的产品。

> [!NOTE]
> 而不是使用 TemplateField （此耗时较长的步骤 3 的焦点），我们可以创建自定义`DataControlField`呈现相应的用户界面和功能的类。 [ `DataControlField`类](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx)BoundField、 CheckBoxField、 TemplateField 和其他内置的 GridView 和 DetailsView 字段派生的类的基类。 创建自定义`DataControlField`类将表示在单选按钮列可能只需使用声明性语法中，添加并还会使复制其他网页和其他更加便捷的 web 应用程序的功能。


如果已创建自定义，编译 ASP.NET 中的控件，但是，您知道这样做，因此需要大量的琐碎工作，并且具有以来的微妙之处和必须谨慎处理的边缘情况的主机。 因此，我们将会放弃实现为自定义的单选按钮的列`DataControlField`类目前并坚持使用 templatefield 进一步选项。 也许我们将有机会来了解创建、 使用和部署自定义`DataControlField`以后的教程中的类 ！

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>步骤 4： 在一个单独的页中显示所选供应商的产品

用户已经选择了 GridView 行后，我们需要显示所选的供应商的产品。 在某些情况下，我们可能想要在单独的页上，在其他我们可能更愿意在同一页中执行此操作中显示这些产品。 让我们来首先检查如何在单独的页面; 中显示的产品步骤 5 中我们将介绍添加到 GridView`RadioButtonField.aspx`以显示所选供应商的产品。

目前有两个页面上的按钮 Web 控件`ListProducts`和`SendToProducts`。 当`SendToProducts`单击按钮时，我们想要发送到用户`~/Filtering/ProductsForSupplierDetails.aspx`。 此页中创建[母版/详细信息筛选跨两个页面](../masterdetail/master-detail-filtering-across-two-pages-cs.md)教程中，并显示该供应商的产品其`SupplierID`通过名为的查询字符串字段传递`SupplierID`。

若要提供此功能，创建的事件处理程序`SendToProducts`按钮的`Click`事件。 在步骤 3 中我们添加了`SuppliersSelectedIndex`选择属性，它将返回的行的索引的单选按钮。 在相应`SupplierID`可以检索从 GridView s`DataKeys`集合和用户然后可以发送到`~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`使用`Response.Redirect("url")`。


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample9.cs)]

此代码将运行非常好，只要从 GridView 中选择一个单选按钮。 如果最初，GridView 不具有所选，任何单选按钮，并且用户单击`SendToProducts`按钮，`SuppliersSelectedIndex`将为`-1`，这将导致异常引发自`-1`的索引范围超出`DataKeys`集合。 这是一个问题，但是，如果您决定更新`RowCreated`以便具有最初选择 GridView 中的第一个单选按钮的步骤 3 中所述的事件处理程序。

若要容纳`SuppliersSelectedIndex`的值`-1`，将标签 Web 控件添加到页面上方 GridView。 设置其`ID`属性设置为`ChooseSupplierMsg`，将其`CssClass`属性设置为`Warning`，将其`EnableViewState`并`Visible`属性设置为`false`，并将其`Text`到请属性网格中选择一个供应商。 CSS 类`Warning`中定义，以红色、 斜体、 粗体、 大字体显示文本`Styles.css`。 通过设置`EnableViewState`并`Visible`属性设置为`false`，标签不呈现除外，对于只有回发的位置控制 s`Visible`属性以编程方式设置为`true`。


[![添加 GridView 上方的一个标签 Web 控件](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image21.png)

**图 13**： 添加标签 Web 控件上方的 GridView ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image22.png))


接下来，扩充`Click`事件处理程序以显示`ChooseSupplierMsg`标签如果`SuppliersSelectedIndex`是小于零，且用户重定向到`~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`否则为。


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample10.cs)]

访问在浏览器，并单击页面`SendToProducts`按钮，再从 GridView 中选择一个供应商。 如图 14 所示，这将显示`ChooseSupplierMsg`标签。 接下来，选择一个供应商，并单击`SendToProducts`按钮。 这将列出所选的供应商提供的产品的页面到 whisk 您。 图 15 显示了`ProductsForSupplierDetails.aspx`页面时选择了野人绑架了 Breweries 供应商。


[![如果选择无供应商，则显示 ChooseSupplierMsg 标签](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image23.png)

**图 14**:`ChooseSupplierMsg`如果否供应商选择显示标签 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image24.png))


[![选择供应商的产品显示在 ProductsForSupplierDetails.aspx](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image25.png)

**图 15**： 选择 Supplier 的产品显示在`ProductsForSupplierDetails.aspx`([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image26.png))


## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>步骤 5： 在同一页上显示所选供应商的产品

在步骤 4 中，我们已了解如何将用户发送到另一个 web 页面以显示所选的供应商的产品。 或者，可以在同一页上显示所选供应商的产品。 为了说明这一点，我们将添加到另一个 GridView`RadioButtonField.aspx`以显示所选供应商的产品。

因为我们仅希望此 GridView 的产品以显示选择供应商后，添加面板 Web 控件下方`Suppliers`GridView 中后，设置其`ID`到`ProductsBySupplierPanel`并将其`Visible`属性设置为`false`。 在面板内所选供应商，添加文本的产品后, 跟名为 GridView `ProductsBySupplier`。 从 GridView s 智能标记，选择要绑定到名为新 ObjectDataSource `ProductsBySupplierDataSource`。


[![将 ProductsBySupplier GridView 绑定到新对象数据源](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image27.png)

**图 16**： 将绑定`ProductsBySupplier`新 ObjectDataSource 的 GridView ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image28.png))


接下来，配置要使用 ObjectDataSource`ProductsBLL`类。 由于我们只想要检索的所选的供应商提供的那些产品，指定应调用 ObjectDataSource`GetProductsBySupplierID(supplierID)`方法来检索其数据。 选择 （无） 从下拉列表中插入、 更新和删除选项卡。


[![配置对象数据源使用 GetProductsBySupplierID(supplierID) 方法](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image29.png)

**图 17**： 配置为使用 ObjectDataSource`GetProductsBySupplierID(supplierID)`方法 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image30.png))


[![设置为 （无） 下拉列表中插入、 更新和删除选项卡](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image31.png)

**图 18**： 在更新、 插入和删除选项卡中设置为 （无） 的下拉列表列出 ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image32.png))


配置选择之后, 更新、 插入和删除选项卡，单击下一步。 由于`GetProductsBySupplierID(supplierID)`方法需要一个输入的参数，创建数据源向导会提示我们指定的源参数的值。

我们有几个选项在此处在指定参数的值的源。 我们可以使用默认参数对象，并且以编程方式将指定的值`SuppliersSelectedIndex`属性设置为参数 s`DefaultValue`属性中的 ObjectDataSource 的`Selecting`事件处理程序。 回头[以编程方式设置 ObjectDataSource 的参数值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)教程，了解在以编程方式将值分配到 ObjectDataSource 的参数使用刷新程序。

或者，可以使用 ControlParameter 并指`Suppliers`GridView s [ `SelectedValue`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx)（请参阅图 19）。 GridView s`SelectedValue`属性返回`DataKey`值，对应于[`SelectedIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)。 为了使此选项才能工作，我们需要以编程方式设置 GridView s`SelectedIndex`属性设置为所选行时`ListProducts`单击按钮。 作为一项额外权益，通过设置`SelectedIndex`，将对其执行所选的记录`SelectedRowStyle`中定义`DataWebControls`主题 （黄色背景）。


[![使用 ControlParameter 指定为参数源的 GridView 的 SelectedValue](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image33.png)

**图 19**： 使用 ControlParameter 指定为参数源的 GridView 的 SelectedValue ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image34.png))


完成该向导，时 Visual Studio 将自动添加产品的数据字段的字段。 删除以外的所有`ProductName`， `CategoryName`，并`UnitPrice`BoundFields，并将更改`HeaderText`产品、 类别和价格的属性。 配置`UnitPrice`BoundField 以便其值设置为货币的格式。 进行这些更改后，在面板、 GridView 和 ObjectDataSource s 声明性标记应如下所示：


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample11.aspx)]

若要完成此练习中，我们需要设置 GridView s`SelectedIndex`属性设置为`SelectedSuppliersIndex`并`ProductsBySupplierPanel`面板 s`Visible`属性设置为`true`时`ListProducts`单击按钮。 若要实现此目的，创建的事件处理程序`ListProducts`Button Web 控件的`Click`事件，并添加以下代码：


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample12.cs)]

如果尚未选择 GridView 中，从供应商`ChooseSupplierMsg`显示标签和`ProductsBySupplierPanel`隐藏面板。 如果尚未选择供应商，否则为`ProductsBySupplierPanel`将显示和 GridView 的`SelectedIndex`更新属性。

图 20 显示结果后野人绑架了 Breweries 供应商已选择并单击页面按钮上的显示产品。


[![由野人绑架了 Breweries 产品提供相同的页面上列出](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image35.png)

**图 20**： 在同一页上列出了产品提供野人绑架了 Breweries ([单击以查看实际尺寸的图像](adding-a-gridview-column-of-radio-buttons-cs/_static/image36.png))


## <a name="summary"></a>总结

如中所述[母版/详细信息使用详细信息 DetailView 的可选母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程中，可从使用 CommandField GridView 中选择记录其`ShowSelectButton`属性设置为`true`。 但 CommandField 显示其按钮作为常规下压按钮、 链接或图像。 替代的行选择用户界面是提供单选按钮或每个 GridView 行中的复选框。 在本教程中介绍了如何添加单选按钮的列。

遗憾的，为简单或简单添加单选按钮并不是 t 的列，如您所料。 可以在单击按钮，添加任何内置 RadioButtonField 并且使用 TemplateField 内的 RadioButton Web 控件引入了自己的问题集。 最后，若提供此类接口我们必须创建自定义`DataControlField`类或将适当的 HTML 注入到 TemplateField 期间采用`RowCreated`事件。

具有探讨了如何添加单选按钮的列，让我们把注意力转向添加复选框列。 具有的列的复选框，用户可以选择一个或多个 GridView 行，然后执行某个操作上的所有所选行 （例如从基于 web 的电子邮件客户端，选择一组电子邮件，然后选择要删除所有所选电子邮件）。 在下一教程中我们将了解如何添加此类列。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 David Suru。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一篇](adding-a-gridview-column-of-checkboxes-cs.md)
