---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: DataList 和 Repeater (VB) 中的自定义按钮 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将构建一个接口，使用 Repeater 要列出各个类别在系统中，每个类别都提供了一个按钮以显示其 associ...
ms.author: aspnetcontent
ms.date: 11/13/2006
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: ab580a706b76325fc4c0eccfc130ffa7db22fbd3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812942"
---
<a name="custom-buttons-in-the-datalist-and-repeater-vb"></a>DataList 和 Repeater (VB) 中的自定义按钮
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe)或[下载 PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)

> 在本教程中我们将构建一个接口，使用 Repeater 要列出在系统中，每个类别都提供了一个按钮以显示其相关联的产品使用 BulletedList 控件的各个类别。


## <a name="introduction"></a>介绍

在过去 17 个 DataList 和 Repeater 的教程，我们制作了只读的示例和编辑和删除示例。 为了便于编辑和删除 DataList 中的功能，我们添加按钮到 DataList s `ItemTemplate` ，单击，导致回发并引发对应的按钮 s DataList 事件`CommandName`属性。 例如，添加到按钮`ItemTemplate`与`CommandName`编辑的属性值会导致 DataList s`EditCommand`触发回发，则在另一个使用`CommandName`删除引发`DeleteCommand`。

除了编辑和删除按钮，DataList 和 Repeater 控件还可以包含按钮、 Linkbutton 或 ImageButtons，单击时，执行一些自定义服务器端逻辑。 在本教程中我们将构建一个使用 Repeater 来列出系统中的类别的接口。 对于每个类别，Repeater 将包括按钮以显示使用 BulletedList 控件的关联产品的类别 （请参阅图 1）。


[![单击显示的产品链接显示的项目符号列表中的类别 s 产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)

**图 1**： 单击显示的产品链接显示在项目符号列表中的 s 产品类别 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png))


## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>步骤 1： 添加自定义按钮教程 Web 页

我们看看如何添加自定义按钮之前，让 s 先花点时间在我们的网站项目，我们需要在本教程中创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`CustomButtonsDataListRepeater`。 接下来，将以下两个 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `CustomButtons.aspx`


![将 ASP.NET 页面添加自定义与按钮相关的教程](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

**图 2**： 将 ASP.NET 页面添加自定义与按钮相关的教程


在其他文件夹中，喜欢`Default.aspx`在`CustomButtonsDataListRepeater`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 添加到此用户控件`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)

**图 3**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png))


最后，将页面添加到条目为`Web.sitemap`文件。 具体而言，使用 DataList 和 Repeater 分页和排序后添加以下标记`<siteMapNode>`:


[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含用于编辑、 插入和删除教程的项。


![站点图现在包括自定义按钮教程的条目](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

**图 4**： 站点图现在包括自定义按钮教程的条目


## <a name="step-2-adding-the-list-of-categories"></a>步骤 2： 添加类别的列表

我们需要创建列出所有类别以及显示产品 LinkButton Repeater 本教程中，单击时，将显示关联的类别的产品项目符号列表中。 让我们来首先创建简单的 Repeater 的系统中列出的类别。 首先打开`CustomButtons.aspx`页中`CustomButtonsDataListRepeater`文件夹。 将从工具箱拖到设计器和组的 Repeater 及其`ID`属性设置为`Categories`。 接下来，从 Repeater s 智能标记创建新的数据源控件。 具体而言，创建一个名为的新对象数据源控件`CategoriesDataSource`，选择从其数据`CategoriesBLL`类的`GetCategories()`方法。


[![配置对象数据源使用 CategoriesBLL 类的 GetCategories() 方法](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)

**图 5**： 配置为使用 ObjectDataSource`CategoriesBLL`类 s`GetCategories()`方法 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png))


与 Visual Studio 将为其创建默认值的 DataList 控件不同`ItemTemplate`基于数据源，Repeater 的模板必须手动定义。 此外，必须创建和编辑以声明方式 Repeater 的模板 （即，有 s 没有编辑的模板选项中 Repeater s 智能标记）。

单击左下角的源选项卡上，并添加`ItemTemplate`，它显示在类别的名称`<h3>`元素和其说明中一个段落标记，包括`SeparatorTemplate`显示水平标尺 (`<hr />`) 每个之间类别。 此外将添加使用 LinkButton 其`Text`属性设置为显示产品。 完成这些步骤后，在页面 s 声明性标记应如下所示：


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

图 6 显示时的浏览器查看的页。 列出每个类别名称和说明。 显示产品按钮，单击，导致回发，但不会执行任何操作。


[![每个类别名称和说明会显示，以及显示产品 LinkButton](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)

**图 6**： 每个类别的名称和说明会显示，以及显示产品 LinkButton ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png))


## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>执行服务器端逻辑时显示产品 LinkButton 单击步骤 3:

任何时候单击按钮、 LinkButton 或 DataList 或 Repeater 中的模板中的 ImageButton 时，产生的回发和 DataList 或 Repeater 的`ItemCommand`事件触发。 除了`ItemCommand`事件时，DataList 控件还可能会引发更具体的另一个事件，如果按钮 s`CommandName`属性设置为一个保留的字符串 （删除，请编辑、 取消、 Update 或选择），但`ItemCommand`事件是*始终*激发。

DataList 或 Repeater 中单击一个按钮时，通常我们需要传递 （在可能有多个内的控件，如这两个编辑按钮和删除按钮的情况下） 被单击的按钮和可能的一些其他信息 （如主键值的按钮被单击的项）。 按钮、 LinkButton 和 ImageButton 提供两个属性的值传递给`ItemCommand`事件处理程序：

- `CommandName` 一个字符串，通常用来标识在模板中的每个按钮
- `CommandArgument` 通常用来保存某些数据字段，如主键值的值

对于此示例中，将设置 LinkButton s`CommandName`属性设置为 ShowProducts 和绑定的当前记录 s 主键值`CategoryID`到`CommandArgument`属性使用的数据绑定语法`CategoryArgument='<%# Eval("CategoryID") %>'`。 以后指定这两个属性，LinkButton s 声明性语法看起来应如下所示：


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

当单击该按钮，产生的回发和 DataList 或 Repeater 的`ItemCommand`事件触发。 事件处理程序传递按钮 s`CommandName`和`CommandArgument`值。

为 Repeater s 创建事件处理程序`ItemCommand`事件并记下第二个参数传递到事件处理程序 (名为`e`)。 此第二个参数的类型是[ `RepeaterCommandEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx)并且具有以下四个属性：

- `CommandArgument` 单击的按钮 s 的值`CommandArgument`属性
- `CommandName` 按钮 s 的值`CommandName`属性
- `CommandSource` 对被单击的按钮控件的引用
- `Item` 对引用[ `RepeaterItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) ，其中包含被单击的按钮; 绑定到 Repeater 每条记录显示为 `RepeaterItem`

由于所选类别 s`CategoryID`通过传入`CommandArgument`属性，我们可以获取与所选类别中关联的产品的集`ItemCommand`事件处理程序。 然后，这些产品可以绑定到中的 BulletedList 控件`ItemTemplate`(哪些我们 ve 目前进行添加)。 所有剩余，然后是添加 BulletedList，引用`ItemCommand`事件处理程序，并将绑定到它在步骤 4 中，我们将介绍所选类别产品的集。

> [!NOTE]
> DataList s`ItemCommand`事件处理程序传递类型的对象[ `DataListCommandEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)，它提供了四个属性与相同`RepeaterCommandEventArgs`类。


## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>步骤 4： 在项目符号列表中显示所选的类别的产品

所选的类别的产品可能显示在 Repeater 的`ItemTemplate`使用任意数量的控件。 我们可以添加另一个嵌套 Repeater、 DataList、 DropDownList、 GridView，等等。 由于我们想要作为项目符号列表中显示的产品，不过，我们将使用 BulletedList 控件。 返回到`CustomButtons.aspx`页上 s 声明性标记，添加到控件 BulletedList`ItemTemplate`后显示产品 LinkButton。 设置 BulletedLists s`ID`到`ProductsInCategory`。 BulletedList 显示通过指定的数据字段的值`DataTextField`属性; 因为此控件将具有产品信息绑定到它，设置`DataTextField`属性设置为`ProductName`。


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

在中`ItemCommand`事件处理程序引用此控件使用`e.Item.FindControl("ProductsInCategory")`并将其绑定到与所选类别关联的产品集。


[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

在执行中的任何操作之前`ItemCommand`事件处理程序，它首先检查传入的值比较明智的做法 s `CommandName`。 由于`ItemCommand`事件处理程序，则会激发*任何*单击按钮时，如果有多个按钮添加模板用`CommandName`值，以识别要执行的操作。 检查`CommandName`下面是没有实际意义，因为只有一个按钮，但它是一个好习惯到窗体。 下一步，`CategoryID`检索所选类别的`CommandArgument`属性。 在模板中的 BulletedList 控件是然后引用且绑定到的结果`ProductsBLL`类的`GetProductsByCategoryID(categoryID)`方法。

在前面的教程，如使用 DataList 中的按钮[概述的编辑和删除 DataList 中的数据](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)，我们确定通过给定的项目的主键值`DataKeys`集合。 虽然这种方法适用于 DataList，Repeater 不具有`DataKeys`属性。 相反，我们必须使用另一种方法提供的主键值，如通过按钮的`CommandArgument`属性或向隐藏标签 Web 控件模板中分配的主键值，并读取其值返回中`ItemCommand`事件处理程序使用`e.Item.FindControl("LabelID")`。

完成后`ItemCommand`事件处理程序，请花费片刻时间来查看此页在浏览器中测试。 如图 7 所示，单击显示产品链接导致回发并 BulletedList 中显示所选类别的产品。 此外，请注意，此产品的信息将保留，即使在单击其他类别显示产品的链接。

> [!NOTE]
> 如果你想要修改此报表的行为，以便只有一个类别的产品列出一次，只需设置 BulletedList 控件 s`EnableViewState`属性设置为`False`。


[![BulletedList 用于显示所选分类的产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)

**图 7**: BulletedList 用于显示所选分类的产品 ([单击以查看实际尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png))


## <a name="summary"></a>总结

DataList 和 Repeater 控件可以包含在其模板中任意数量的按钮、 Linkbutton 或 ImageButtons。 此类按钮，单击时，会导致回发和引发`ItemCommand`事件。 若要将自定义服务器端操作相关联所单击的按钮，创建的事件处理程序`ItemCommand`事件。 在此事件处理程序首先检查传入`CommandName`值以确定被单击的按钮。 （可选） 可以通过按钮 s 提供的其他信息`CommandArgument`属性。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Dennis Patterson。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](custom-buttons-in-the-datalist-and-repeater-cs.md)
