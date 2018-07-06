---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
title: 概述插入、 更新和删除数据 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何将映射 ObjectDataSource 的 insert （），update （），和 delete （） 方法添加到的 BLL 方法类，以及如何配置...
ms.author: aspnetcontent
ms.date: 07/17/2006
ms.assetid: b651dc58-93c7-4f83-a74e-3b99f6d60848
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
msc.type: authoredcontent
ms.openlocfilehash: abe42d01cc31ea46c97888f31d768ebfede64abd
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821691"
---
<a name="an-overview-of-inserting-updating-and-deleting-data-c"></a>插入、 更新和删除数据 (C#) 的概述
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_CS.exe)或[下载 PDF](an-overview-of-inserting-updating-and-deleting-data-cs/_static/datatutorial16cs1.pdf)

> 在本教程中我们将了解如何将映射 ObjectDataSource 的 insert （），update （），和 delete （） 方法添加到的 BLL 方法类，以及如何配置 GridView、 DetailsView 和 FormView 控件，以提供数据修改功能。


## <a name="introduction"></a>介绍

通过过去的几个教程，我们探讨了如何在 ASP.NET 页使用 GridView、 DetailsView 和 FormView 控件中显示数据。 这些控件只需使用提供给它们的数据。 通常情况下，这些控件访问通过使用数据源控件，如 ObjectDataSource 的数据。 我们已经看到如何 ObjectDataSource 充当 ASP.NET 页面和基础数据之间的代理。 当需要显示数据的 GridView 时，它将调用其 ObjectDataSource 的`Select()`方法，它调用的方法从我们的业务逻辑层 (BLL)，该调用中相应数据访问层的 (DAL) 的方法 TableAdapter，将发送`SELECT`到 Northwind 数据库的查询。

请记住，当我们在 DAL 中创建 Tableadapter[我们第一篇教程](../introduction/creating-a-data-access-layer-cs.md)、 Visual Studio 自动添加方法用于插入、 更新和删除数据从基础数据库表。 此外，在[创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md)我们设计中向下名为 BLL 方法应用到这些数据修改 DAL 方法。

除了其`Select()`方法，还具有 ObjectDataSource `Insert()`， `Update()`，和`Delete()`方法。 如`Select()`方法，这三种方法可以映射到基础对象中的方法。 当配置为插入、 更新或删除数据，GridView、 DetailsView 和 FormView 控件用于修改基础数据提供用户界面。 此用户界面调用`Insert()`， `Update()`，和`Delete()`方法的 ObjectDataSource，然后调用基础对象的关联的方法 （请参阅图 1）。


[![ObjectDataSource 的 insert （）、 update （） 和 delete （） 方法提供为代理到 BLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image1.png)

**图 1**: ObjectDataSource `Insert()`， `Update()`，和`Delete()`方法充当代理，BLL ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image3.png))


在本教程中我们将了解如何将映射的 ObjectDataSource `Insert()`， `Update()`，和`Delete()`BLL，以及如何配置 GridView、 DetailsView 和 FormView 控件，以提供数据修改中类方法的方法功能。

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>步骤 1： 创建 Insert、 Update 和 Delete 教程网页

我们开始探索如何插入、 更新和删除数据之前，我们先来看一段时间来在我们的网站项目，我们需要为本教程下, 一步的几个源表创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`EditInsertDelete`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![将 ASP.NET 页添加的数据修改相关教程](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image4.png)

**图 2**： 添加 ASP.NET 页的数据修改相关教程


在其他文件夹中，喜欢`Default.aspx`在`EditInsertDelete`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面的设计视图上拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image5.png)

**图 3**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image7.png))


最后，将页面添加到条目为`Web.sitemap`文件。 具体而言，自定义格式设置后添加以下标记`<siteMapNode>`:


[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含用于编辑、 插入和删除教程的项。


![站点图现在包括项的编辑、 插入和删除教程](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image8.png)

**图 4**： 站点图现在包括项的编辑、 插入和删除教程


## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>步骤 2： 添加并配置 ObjectDataSource 控件

由于 GridView、 DetailsView 和在其数据修改功能和布局的每个不同的 FormView，让我们逐个检查每个。 而不是必须使用其自己的对象数据源的每个控件，但是，我们将创建所有三个控件示例可以共享单个对象数据源。

打开`Basics.aspx`页上，从工具箱拖到设计器中，拖动对象数据源并单击其智能标记中的配置数据源链接。 由于`ProductsBLL`是唯一的 BLL 类提供编辑、 插入和删除方法，配置对象数据源以使用此类。


[![配置对象数据源以使用 ProductsBLL 类](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image9.png)

**图 5**： 配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image11.png))


我们可以在下一屏幕中指定的哪些方法`ProductsBLL`类映射到的 ObjectDataSource `Select()`， `Insert()`， `Update()`，和`Delete()`通过选择相应的选项卡并从下拉列表中选择该方法。 图 6 中，现在应该很熟悉，映射的 ObjectDataSource`Select()`方法`ProductsBLL`类的`GetProducts()`方法。 `Insert()`， `Update()`，和`Delete()`方法可以通过从顶部列表中选择相应的选项卡配置。


[![具有对象数据源返回的所有产品](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image12.png)

**图 6**： 具有对象数据源返回所有产品的 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image14.png))


图 7、 8 和 9 显示 ObjectDataSource 的更新、 插入和删除选项卡。 配置这些选项卡，以便`Insert()`， `Update()`，并`Delete()`方法调用`ProductsBLL`类的`UpdateProduct`， `AddProduct`，和`DeleteProduct`方法，分别。


[![将 ObjectDataSource 的 update （） 方法映射到 ProductBLL 类的 UpdateProduct 方法](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image15.png)

**图 7**： 映射的 ObjectDataSource`Update()`方法`ProductBLL`类的`UpdateProduct`方法 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image17.png))


[![将 ObjectDataSource 的 insert （） 方法映射到 ProductBLL 类的 AddProduct 方法](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image18.png)

**图 8**： 映射的 ObjectDataSource`Insert()`方法`ProductBLL`类的添加`Product`方法 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image20.png))


[![将 ObjectDataSource 的 delete （） 方法映射到 ProductBLL 类的 DeleteProduct 方法](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image21.png)

**图 9**： 映射的 ObjectDataSource`Delete()`方法`ProductBLL`类的`DeleteProduct`方法 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image23.png))


您可能已经注意到更新、 插入和删除选项卡中的下拉列表已选择这些方法。 这得归功于我们利用`DataObjectMethodAttribute`修饰的方法`ProducstBLL`。 例如，DeleteProduct 方法具有以下签名：


[!code-csharp[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample2.cs)]

`DataObjectMethodAttribute`属性指示每个方法的用途，它是用于选择、 插入、 更新或删除和它是否是默认值。 如果您省略这些属性，创建您的 BLL 类时，你将需要手动从更新中，选择方法插入和删除选项卡。

之后，确保相应`ProductsBLL`方法映射到的 ObjectDataSource `Insert()`， `Update()`，和`Delete()`方法，单击完成以完成向导。

## <a name="examining-the-objectdatasources-markup"></a>检查 ObjectDataSource 的标记

配置后其向导通过对象数据源，请转到源视图来检查生成的声明性标记。 `<asp:ObjectDataSource>`标记指定的基础对象和要调用的方法。 此外，还有`DeleteParameters`， `UpdateParameters`，并`InsertParameters`，它将映射到的输入参数的`ProductsBLL`类的`AddProduct`， `UpdateProduct`，和`DeleteProduct`方法：


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample3.aspx)]

ObjectDataSource 包括其关联的方法，就像一系列的输入参数的每个参数`SelectParameter`s 是的存在时配置 ObjectDataSource 调用 select 方法所需的输入的参数 (如`GetProductsByCategoryID(categoryID)`). 我们稍后将看到，这些值`DeleteParameters`， `UpdateParameters`，并`InsertParameters`将自动设置的 GridView、 DetailsView 和 FormView 调用 ObjectDataSource 的之前`Insert()`， `Update()`，或`Delete()`方法。 这些值在我们将讨论在将来的教程中还可以根据需要以编程方式设置。

使用该向导将配置为 ObjectDataSource 的一个副作用是 Visual Studio 将设置[OldValuesParameterFormatString 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx)到`original_{0}`。 此属性的值用于包含正在编辑的数据的原始值，并可在两个方案中：

- 如果在编辑记录时，用户就能够更改主键值。 在这种情况下，新的主键值和原始的主键值必须提供，以便使用原始的主键值的记录可以找到并将相应地更新其值。
- 当使用乐观并发。 乐观并发是一种技术，以确保两个用户同时使用不会覆盖彼此发生的变化，并且是以后的教程主题。

`OldValuesParameterFormatString`属性指示的基础对象的更新和删除方法的原始值中的输入参数的名称。 我们将探讨乐观并发，我们将讨论此属性，更详细地介绍其用途。 我将其启动现在，但是，因为我们 BLL 方法不需要原始值，因此很重要，我们删除此属性。 离开`OldValuesParameterFormatString`属性设置为默认值之外的任何内容 (`{0}`) 会导致错误，当尝试调用 ObjectDataSource 的数据 Web 控件`Update()`或`Delete()`方法因为 ObjectDataSource 将尝试将这两`UpdateParameters`或`DeleteParameters`以及原始值参数指定。

如果这不是十分清楚此时，必须查明，别担心，我们将在以后的教程中检查此属性和它的实用。 现在，只是一定要完全从声明性语法中删除此属性声明或将值设置为默认值 ({0})。

> [!NOTE]
> 如果只需清除`OldValuesParameterFormatString`属性值从属性窗口在设计视图中，该属性仍将存在于声明性语法，但将设置为空字符串。 此操作，遗憾的是，仍会导致上面讨论的相同问题。 因此，删除该属性完全声明性语法中，或从属性窗口中，将值设置为默认情况下， `{0}`。


## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>步骤 3： 添加数据 Web 控件并将其配置针对数据修改

ObjectDataSource 具有已添加到页并配置后，我们就可以将数据 Web 控件添加到页后，可以同时显示的数据，并提供一个使最终用户对其进行修改。 我们将介绍的 GridView、 DetailsView 和 FormView 分开，因为这些数据 Web 控件在其数据修改功能和配置不同。

我们将看到这篇文章的其余部分中添加非常基本的编辑、 插入和删除通过 GridView、 DetailsView，支持和 FormView 控件是非常简单，检查几个复选框。 有许多细微问题和在现实世界中的边缘情况，请提供此类不是只需指向和单击更为复杂的功能。 本教程中，但是，主要依靠证明简单数据修改功能。 将来的教程将探讨会实际设置中出现的问题。

## <a name="deleting-data-from-the-gridview"></a>从 GridView 中删除数据

首先，从工具箱拖到设计器中拖动 GridView。 接下来，将对象数据源绑定到 GridView，GridView 的智能标记中的下拉列表中选择。 此时将为 GridView 的声明性标记：


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample4.aspx)]

将 GridView 绑定到通过其智能标记 ObjectDataSource 有两个好处：

- 为每个对象数据源返回的字段自动创建 BoundFields 和 CheckBoxFields。 此外，BoundField 和 CheckBoxField 的属性会根据设置的基础字段元数据。 例如， `ProductID`， `CategoryName`，并`SupplierName`字段都标记为只读的中`ProductsDataTable`，因此不应是可更新编辑时。 若要容纳此，则这些 BoundFields[只读属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx)设置为`true`。
- [DataKeyNames 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx)分配给基础对象的主键字段。 这是必不可少的时使用 GridView 编辑或删除数据，此属性指示的字段 （或组的字段），它唯一标识每条记录。 有关详细信息`DataKeyNames`属性，将回指[母版/详细信息使用详细信息 DetailView 的可选母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程。

虽然可将 GridView 绑定到通过属性窗口或声明性语法 ObjectDataSource，这样做需要你手动添加相应 BoundField 和`DataKeyNames`标记。

GridView 控件为行级编辑和删除提供内置支持。 配置一个 GridView，支持删除添加删除按钮的列。 当最终用户单击特定行的删除按钮时，才会进行回发和 GridView 将执行以下步骤：

1. ObjectDataSource 的`DeleteParameters`分配值
2. ObjectDataSource 的`Delete()`调用方法时，删除指定的记录
3. GridView 重新绑定本身到对象数据源通过调用其`Select()`方法

分配给的值`DeleteParameters`的值`DataKeyNames`其删除按钮被单击的行的字段。 因此很重要的 GridView 的`DataKeyNames`属性正确设置。 如果缺失，`DeleteParameters`将分配`null`值在步骤 1，又不会导致任何删除在步骤 2 中的记录。

> [!NOTE]
> `DataKeys`集合存储在 GridView 的控件状态，也就是说，`DataKeys`值将记住在回发之间，即使已禁用的 GridView 的视图状态。 但是，它是非常重要的 Gridview 支持编辑或删除 （默认行为） 的视图状态保持启用状态。 如果设置 GridView s`EnableViewState`属性设置为`false`、 编辑和删除行为将适用于单个用户，能够正常工作，但如果删除数据的并发用户，存在这些并发的用户可能意外的可能性删除或编辑记录该它们无效 t 计划。 请参阅我博客文章[警告： 禁用并发问题与 ASP.NET 2.0 Gridview/DetailsView/FormViews 该支持编辑和/或删除和其视图状态](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)，有关详细信息。


此相同的警告也适用于 DetailsViews 和 FormViews。

若要将删除的功能添加到 GridView，只需转到其智能标记，并选中启用删除复选框。


![检查删除复选框启用](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image24.png)

**图 10**： 检查删除复选框启用


从智能标记的启用删除复选框将 CommandField 添加到 GridView。 CommandField 呈现按钮，用于执行一个或多个以下任务使用 GridView 中的列： 选择的记录，编辑记录，并删除一条记录。 我们以前看到的那样在操作选择中的记录 CommandField[母版/详细信息使用详细信息 DetailView 的可选母版 GridView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程。

CommandField 包含大量`ShowXButton`指示哪些系列按钮显示在 CommandField 属性。 通过选中启用删除复选框 CommandField 其`ShowDeleteButton`属性是`true`已添加到 GridView 的列集合。


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample5.aspx)]

现在，无论您相信与否，我们已经完成了将删除支持添加到 GridView ！ 如图 11 所示，当访问此页上通过浏览器删除按钮的列存在。


[![CommandField 添加删除按钮的列](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image25.png)

**图 11**: CommandField 添加了列的删除按钮 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image27.png))


如果您生成本教程中从零开始，自行时测试此页上，单击删除按钮将引发异常。 继续阅读以了解有关生成这些异常的原因以及如何解决这些问题。

> [!NOTE]
> 如果您一直使用此教程随附的下载，具有已被考虑这些问题。 但是，我鼓励您通读下面列出，以帮助识别可能出现的问题和合适的解决方法的详细信息。


如果在尝试删除某个产品时，获取的异常的消息是类似于"*ObjectDataSource ObjectDataSource1 找不到非泛型方法具有参数的 DeleteProduct: 产品 id，原始\_ProductID*，"您可能忘记删除`OldValuesParameterFormatString`ObjectDataSource 中的属性。 与`OldValuesParameterFormatString`属性指定，ObjectDataSource 尝试传递中均`productID`并`original_ProductID`输入参数`DeleteProduct`方法。 `DeleteProduct`但是，仅接受一个输入的参数，因此异常。 删除`OldValuesParameterFormatString`属性 (或将其设置为`{0}`) 指示对象数据源，不尝试将原始的输入参数中。


[![确保 OldValuesParameterFormatString 属性已被清除](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image28.png)

**图 12**： 确保`OldValuesParameterFormatString`属性已被清除出 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image30.png))


即使您已经删除`OldValuesParameterFormatString`属性，您仍将收到异常时尝试删除该消息与产品:"*DELETE 语句与引用约束冲突 FK\_顺序\_详细信息\_产品的*。"Northwind 数据库包含之间的外键约束`Order Details`并`Products`表，这表示如果存在一个或多个记录中为其产品不能从系统删除`Order Details`表。 由于在 Northwind 数据库中的每个产品具有至少一个记录`Order Details`，我们首先删除该产品关联的订单详细信息记录之前，我们不能删除任何产品。


[![外键约束禁止删除产品](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image31.png)

**图 13**： 外键约束禁止删除的产品 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image33.png))


本教程中，让我们只需删除所有从记录`Order Details`表。 在实际应用程序中我们将需要为：

- 具有另一个屏幕来管理订单详细信息
- 增强`DeleteProduct`方法以包括逻辑删除指定的产品的订单详细信息
- 修改 TableAdapter 用于包括删除的指定的产品的订单详细信息的 SQL 查询

让我们只需删除所有从记录`Order Details`来绕过的外键约束的表。 转到 Visual Studio 中的服务器资源管理器，右键单击`NORTHWND.MDF`节点，然后选择新查询。 然后，在查询窗口中，运行以下 SQL 语句： `DELETE FROM [Order Details]`


[![从订单详细信息表中删除所有记录](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image34.png)

**图 14**： 删除所有记录`Order Details`表 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image36.png))


清除后`Order Details`表单击删除按钮将删除的产品不会出错。 如果单击删除按钮不会删除该产品，检查以确保的 GridView`DataKeyNames`属性设置为主键字段 (`ProductID`)。

> [!NOTE]
> 单击删除按钮时才会进行回发和删除该记录。 这可能会很危险，因为很容易意外地单击错误行的删除按钮。 在将来的教程中我们将了解如何删除一条记录时添加客户端的确认。


## <a name="editing-data-with-the-gridview"></a>编辑数据的 gridview

以及删除 GridView 控件还提供内置的行级编辑支持。 配置一个 GridView，支持编辑添加编辑按钮的列。 从最终用户的角度来看，单击某一行的编辑按钮，将使该行成为可编辑，转换包含的现有值并替换与更新编辑按钮和取消按钮的文本框单元格。 进行其所需的更改后，最终用户可以单击更新按钮提交所做的更改或弃用这些取消按钮。 在任一情况下，单击更新或取消按钮后 GridView 返回到其预先编辑状态。

从我们角度来看，作为页面开发人员，当最终用户单击特定行的编辑按钮时，回发时，才会和 GridView 将执行以下步骤：

1. GridView 的`EditItemIndex`属性分配给其编辑按钮被单击的行的索引
2. GridView 重新绑定本身到对象数据源通过调用其`Select()`方法
3. 匹配的行索引`EditItemIndex`呈现在"编辑模式。" 在此模式下，编辑按钮被替换为更新和取消按钮和 BoundFields 其`ReadOnly`属性均为 False （默认值） 作为文本框 Web 控件的呈现`Text`属性分配给数据字段的值。

此时标记返回到浏览器中，允许最终用户对行的数据进行任何更改。 当用户单击更新按钮时，产生的回发和 GridView 将执行以下步骤：

1. ObjectDataSource 的`UpdateParameters`值分配到 GridView 的编辑界面由最终用户输入的值
2. ObjectDataSource 的`Update()`调用方法时，更新指定的记录
3. GridView 重新绑定本身到对象数据源通过调用其`Select()`方法

分配到的主键值`UpdateParameters`在步骤 1 中来自中指定的值`DataKeyNames`属性，而非主键值来自中编辑过的行的文本框中 Web 控件的文本。 因为与删除，它是重要的 GridView 的`DataKeyNames`属性正确设置。 如果缺失，`UpdateParameters`将分配的主键值`null`在步骤 1，又不会导致任何值更新在步骤 2 中的记录。

可以通过只需检查 GridView 的智能标记中的启用编辑复选框激活编辑功能。


![检查编辑复选框启用](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image37.png)

**图 15**： 检查编辑复选框启用


检查启用编辑复选框将添加 CommandField （是否需要） 并设置其`ShowEditButton`属性设置为`true`。 CommandField 如我们前面看到的包含大量`ShowXButton`指示哪些系列按钮显示在 CommandField 属性。 选中启用编辑复选框添加`ShowEditButton`属性设置为现有 CommandField:


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample6.aspx)]

这就是一切就是添加基本编辑支持。 编辑界面是相当不成熟 Figure16 所示，每个 BoundField 其`ReadOnly`属性设置为`false`（默认值） 将呈现为一个文本框。 这包括字段，例如`CategoryID`和`SupplierID`，这是与其他表的键。


[![单击 Chai s 编辑按钮以编辑模式显示该行](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image38.png)

**图 16**： 单击 Chai s 编辑按钮以编辑模式显示该行 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image40.png))


除了让用户直接编辑外键值，编辑接口的接口缺少以下方面：

- 如果用户输入`CategoryID`或`SupplierID`不存在在数据库中，`UPDATE`将违反外键约束，从而导致引发异常。
- 编辑接口不包括任何验证。 如果未提供所需的值 (如`ProductName`)，或输入一个字符串值的地方的数字值 （例如，输入"过多 ！" 到`UnitPrice`文本框)，将引发异常。 以后的教程将介绍如何向编辑的用户界面添加验证控件。
- 目前，*所有*GridView 中必须包含产品字段不是只读的。 如果我们要从 GridView 中删除字段，说`UnitPrice`时不会设置更新数据的 GridView `UnitPrice` `UpdateParameters`值，更改的数据库记录`UnitPrice`到`NULL`值。 同样，如果必填字段，如`ProductName`，删除从 GridView 中，则更新将具有相同失败"*列 'ProductName' 不允许使用 null*"上面提到的异常。
- 编辑界面格式设置差强人意所希望的。 `UnitPrice`具有小数点后有 4 所示。 理想情况下`CategoryID`和`SupplierID`值将包含在系统中列出的类别和供应商的 Dropdownlist。

这些是所有的不足之处，我们将不得不接受目前为止，但会在将来的教程中得以解决。

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>插入、 编辑和删除数据与 DetailsView

正如我们已经看到在之前的教程，DetailsView 控件一次显示一条记录，并如 GridView，允许进行编辑和删除当前显示的记录。 这两个最终用户体验的编辑和删除 DetailsView 和从 ASP.NET 端工作流中的项目等同于 GridView。 DetailsView GridView 与不同的是它还提供内置插入支持。

若要演示的 GridView 的数据修改功能，首先添加到 DetailsView`Basics.aspx`上方现有 GridView 页上，并将其绑定到现有 ObjectDataSource 通过 DetailsView 的智能标记。 下一步，清除 DetailsView`Height`和`Width`属性，并检查从智能标记启用分页选项。 若要启用编辑，插入和删除的支持，只需检查智能标记中的启用编辑、 启用插入和启用删除复选框。


![配置为支持编辑、 插入和删除 DetailsView](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image41.png)

**图 17**： 配置为支持编辑、 插入和删除 DetailsView


作为使用 GridView，添加编辑，插入或删除支持向 CommandField DetailsView，如下所示的声明性语法：


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample7.aspx)]

请注意，对于 DetailsView CommandField 默认情况下，将显示在列集合的末尾。 由于 DetailsView 字段呈现为行，CommandField 显示为行与 Insert、 编辑和删除 DetailsView 底部的按钮。


[![配置为支持编辑、 插入和删除 DetailsView](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image42.png)

**图 18**： 配置为支持编辑、 插入和删除 DetailsView ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image44.png))


单击删除按钮与 GridView 一样启动相同的事件序列： 一个回发;跟填充其 ObjectDataSource 的 DetailsView`DeleteParameters`基于`DataKeyNames`值; 并已完成，但调用其 ObjectDataSource`Delete()`方法，它实际上从数据库中删除该产品。 在 DetailsView 中编辑也适用相同的 GridView 的方式。

用于插入，最终用户会看到新按钮，单击时，呈现 DetailsView 中"插入模式。" 使用"插入模式"新建按钮替换为 Insert 和取消按钮和仅这些 BoundFields 其`InsertVisible`属性设置为`true`（默认值） 显示。 如标识为自动递增字段，这些数据字段`ProductID`，具有其[InsertVisible 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx)设置为`false`DetailsView 绑定到数据源通过智能标记时。

Visual Studio 时将数据源绑定到 DetailsView 通过智能标记，将设置`InsertVisible`属性设置为`false`仅用于自动递增字段。 只读字段，如`CategoryName`并`SupplierName`，除非将"插入模式"用户界面中显示其`InsertVisible`属性显式设置为`false`。 请花费片刻时间设置这两个字段`InsertVisible`属性设置为`false`，通过 DetailsView 的声明性语法或编辑字段中的智能标记的链接。 图 19 显示设置`InsertVisible`属性设置为`false`编辑字段上单击链接。


[![Northwind Traders 现在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image45.png)

**图 19**: Northwind Traders 现在提供了 Acme 茶 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image47.png))


设置后`InsertVisible`属性，视图`Basics.aspx`页在浏览器中，单击新建按钮。 图 20 显示了 DetailsView 时添加新的饮料，Acme 茶，到我们的产品线。


[![Northwind Traders 现在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image48.png)

**图 20**: Northwind Traders 现在提供了 Acme 茶 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image50.png))


输入为 Acme 茶的详细信息，并单击插入按钮之后，才会回发和新记录添加到`Products`数据库表。 由于此 DetailsView 列出的顺序与它们存在于数据库表中的产品，我们必须页上的最后一个产品才能看到新的产品。


[![Acme 茶的详细信息](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image51.png)

**图 21**: Acme 茶的详细信息 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image53.png))


> [!NOTE]
> DetailsView [CurrentMode 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx)指示要显示的界面，可以是下列值之一： `Edit`， `Insert`，或`ReadOnly`。 [DefaultMode 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx)指示的模式 DetailsView 以在编辑后返回到或插入已完成，可用于显示 DetailsView 的永久处于编辑模式或插入模式。


指向并单击插入和编辑 DetailsView 功能会受到与 GridView 相同的限制： 用户必须输入现有`CategoryID`和`SupplierID`通过文本框的值; 接口没有任何验证逻辑; 所有不允许进行产品字段`NULL`值或不具有默认值在数据库级别指定的值必须包含在插入界面中，依次类推。

技术我们将介绍用于扩展和增强 GridView 的编辑界面在将来的文章可应用于 DetailsView 控件的编辑和插入界面以及。

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>使用 FormView 适用于更灵活的数据修改用户界面

FormView 提供内置支持用于插入、 编辑和删除数据，但因为它使用模板而不是字段没有添加 BoundFields 或 CommandField GridView 和 DetailsView 控件用于提供数据的位置修改接口。 相反，此接口用于收集用户的 Web 控件添加新项时输入或编辑现有新建，以及编辑、 删除、 插入、 更新和取消按钮必须手动添加到适当的模板。 幸运的是，Visual Studio 将自动创建所需的接口绑定到通过其智能标记中的下拉列表的数据源的 FormView 时。

若要说明了这些方法，首先添加到 FormView`Basics.aspx`页上，并从 FormView 的智能标记，请将其绑定到已创建的 ObjectDataSource。 这将生成`EditItemTemplate`， `InsertItemTemplate`，和`ItemTemplate`文本框 Web 控件，用于收集新的用户的输入和按钮 Web 控件与 FormView，用于编辑、 删除、 插入、 更新和取消按钮。 此外，FormView 的`DataKeyNames`属性设置为主键字段 (`ProductID`) 的对象数据源返回的对象。 最后，检查 FormView 的智能标记中的启用分页选项。

以下显示 FormView 的声明性标记`ItemTemplate`FormView 已绑定到 ObjectDataSource 后。 默认情况下，每个非布尔值产品字段绑定到`Text`标签 Web 控件时的布尔值的每个字段的属性 (`Discontinued`) 绑定到`Checked`已禁用的复选框 Web 控件的属性。 为了使新建、 编辑和删除按钮，以触发特定的 FormView 行为单击时，它是命令性，其`CommandName`的值设置为`New`， `Edit`，和`Delete`分别。


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample8.aspx)]

图 22 显示了 FormView 的`ItemTemplate`时的浏览器查看。 在底部的新建、 编辑和删除按钮将列出每个产品字段。


[![情况下 FormView ItemTemplate 列出了每个产品字段以及新增、 编辑和删除按钮](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image54.png)

**图 22**: 情况下 FormView`ItemTemplate`列出了每个产品字段沿使用新建、 编辑和删除按钮 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image56.png))


使用 GridView 和 DetailsView，单击删除按钮或任何按钮、 LinkButton 或 ImageButton 喜欢其`CommandName`属性设置为删除会导致回发，填充 ObjectDataSource 的`DeleteParameters`根据 FormView 的`DataKeyNames`值，并调用 ObjectDataSource 的`Delete()`方法。

单击编辑按钮时才会进行回发和将数据重新绑定到`EditItemTemplate`，这是负责呈现编辑界面。 此界面包含 Web 控件，用于编辑数据以及更新和取消按钮。 默认值`EditItemTemplate`生成的 Visual Studio 包含的任何自动递增字段的标签 (`ProductID`)、 一个的文本框中的每个非布尔值字段，以及每个布尔值字段对应的复选框。 此行为是非常类似于 GridView 和 DetailsView 控件中的自动生成 BoundFields。

> [!NOTE]
> 使用 FormView 的自动生成的一个小问题`EditItemTemplate`是，它将呈现文本框 Web 控件是只读的如这些字段`CategoryName`和`SupplierName`。 我们将了解如何考虑到这一点很快。


TextBox 控件中`EditItemTemplate`具有其`Text`属性绑定到其相应的数据字段使用的值*双向数据绑定*。 双向数据绑定，为由`<%# Bind("dataField") %>`，执行这两个数据绑定和填充 ObjectDataSource 的参数插入或编辑记录时将数据绑定到该模板。 也就是说，当用户单击编辑按钮从`ItemTemplate`，则`Bind()`方法将返回指定的数据字段值。 用户进行相应更改，然后单击更新后，这些值进行了对应的回发到使用指定的数据字段`Bind()`应用于 ObjectDataSource 的`UpdateParameters`。 或者，单向数据绑定，为由`<%# Eval("dataField") %>`，仅当数据绑定到模板中检索数据字段值并*不*上回发到数据源的参数返回用户输入的值。

下面的声明性标记显示 FormView 的`EditItemTemplate`。 请注意，`Bind()`此处的数据绑定语法中使用方法和更新和取消按钮 Web 控件具有其`CommandName`相应地设置的属性。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample9.aspx)]

我们`EditItemTemplate`，在此点，如果我们尝试使用它，则引发异常。 问题在于`CategoryName`并`SupplierName`作为文本框 Web 控件中呈现字段`EditItemTemplate`。 我们需要将这些文本框更改为标签或一起删除它们。 让我们只需删除它们完全从`EditItemTemplate`。

图 23 在浏览器中显示 FormView 后为 Chai 已单击编辑按钮。 请注意，`SupplierName`并`CategoryName`字段中所示`ItemTemplate`不再存在，因为我们只需删除它们从`EditItemTemplate`。 单击更新按钮时 FormView 将继续通过 GridView 和 DetailsView 控件相同的步骤序列。


[![默认情况下 EditItemTemplate 显示为文本框或复选框的每个可编辑产品字段](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image57.png)

**图 23**： 默认情况下`EditItemTemplate`显示了每个可编辑产品字段为文本框或复选框 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image59.png))


插入按钮单击 FormView 的时`ItemTemplate`回发时，才会。 但是，任何数据不绑定到 FormView 因为一条新记录将被添加。 `InsertItemTemplate`接口包括用于添加新记录以及插入和取消按钮的 Web 控件。 默认值`InsertItemTemplate`生成的 Visual Studio 包含一个文本框的每个非布尔值字段和每个布尔值字段，类似于自动生成一个复选框`EditItemTemplate`的接口。 将文本框控件具有其`Text`属性绑定到使用双向数据绑定其对应数据字段的值。

下面的声明性标记显示 FormView 的`InsertItemTemplate`。 请注意，`Bind()`此处的数据绑定语法中使用方法和插入和取消按钮 Web 控件具有其`CommandName`相应地设置的属性。


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample10.aspx)]

没有使用 FormView 的自动生成的微妙的地方`InsertItemTemplate`。 具体而言，甚至为是只读的如这些字段创建文本框 Web 控件`CategoryName`和`SupplierName`。 与处理方式一样`EditItemTemplate`，我们需要删除从这些文本框`InsertItemTemplate`。

图 24 显示 FormView 的浏览器中，添加一个新的产品 Acme 咖啡时。 请注意，`SupplierName`并`CategoryName`字段中所示`ItemTemplate`不再存在，因为我们只需删除它们。 单击插入按钮时，FormView 可继续通过 DetailsView 控件相同的步骤序列，添加新记录到`Products`表。 图 25 中 FormView 显示 Acme 咖啡产品的详细信息后已插入。


[![InsertItemTemplate 决定了 FormView 的插入接口](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image60.png)

**图 24**:`InsertItemTemplate`决定了 FormView 的插入接口 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image62.png))


[![在 FormView 中显示的新产品，Acme 咖啡，详细信息](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image63.png)

**图 25**： 在 FormView 中显示的新产品，Acme 咖啡的详细信息 ([单击以查看实际尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image65.png))


分离只读的通过编辑，并将接口插入三个单独的模板，FormView 允许比 DetailsView 和 GridView 更精细地控制这些接口。

> [!NOTE]
> DetailsView，FormView 的喜欢`CurrentMode`属性指示要显示的界面并将其`DefaultMode`属性指示的模式 FormView 返回到编辑后或插入已完成。


## <a name="summary"></a>总结

在本教程中，我们探讨插入、 编辑和删除数据使用 GridView、 DetailsView 和 FormView 基础的知识。 所有这三个这些控件提供一定级别的可利用而无需编写一行代码，借助数据 Web 控件和 ObjectDataSource ASP.NET 页中的内置数据修改功能。 但是，简单的指向和单击技术呈现相当 frail 和简单的数据修改用户界面。 提供验证，注入的编程值、 适当地处理异常、 自定义用户界面和依此类推，我们将需要依赖于一系列的下一步的多个教程通过将讨论的技术。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [下一篇](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
