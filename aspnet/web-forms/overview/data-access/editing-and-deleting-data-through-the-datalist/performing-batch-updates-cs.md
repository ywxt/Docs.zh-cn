---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
title: 执行批量更新 (C#) |Microsoft Docs
author: rick-anderson
description: 了解如何创建完全编辑 DataList 的所有项处于编辑模式和其值可以通过单击全部更新按钮保存...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 57743ca7-5695-4e07-aed1-44b297f245a9
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
msc.type: authoredcontent
ms.openlocfilehash: 2ca91baa87d5bb748695b56bb8bf19698b0858f2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830880"
---
<a name="performing-batch-updates-c"></a>执行批量更新 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_CS.exe)或[下载 PDF](performing-batch-updates-cs/_static/datatutorial37cs1.pdf)

> 了解如何创建完全编辑 DataList 的所有项处于编辑模式，可以通过单击页上的"全部更新"按钮保存其值。


## <a name="introduction"></a>介绍

在中[前面的教程](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)介绍了如何创建项目级 DataList。 像标准的可编辑 GridView DataList 中的每个项包含编辑按钮，当单击时，会使项可编辑。 虽然这项级别编辑适用于仅偶尔更新的数据，某些用例场景要求用户编辑多个记录。 如果用户需要编辑数十个记录，并强制，单击编辑，使他们的更改，然后单击为每个更新，则单击量可能妨碍她的工作效率。 在这种情况下，更好的选择是要提供完全可编辑的 DataList，其中*所有*已在编辑模式，其值可以通过单击页上的全部更新按钮进行编辑的项 （请参阅图 1）。


[![可以修改完全可编辑的 DataList 中的每个项](performing-batch-updates-cs/_static/image2.png)](performing-batch-updates-cs/_static/image1.png)

**图 1**： 可以修改完全可编辑的 DataList 中的每个项 ([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image3.png))


在本教程中我们将介绍如何使用户能够更新供应商的地址信息完全可编辑的 DataList。

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>步骤 1： 创建可编辑的用户界面中 DataList 的 ItemTemplate

在前面的教程，其中我们创建标准的项级别的可编辑 DataList，我们使用两个模板：

- `ItemTemplate` 包含只读的用户界面 （标签 Web 控件用于显示每个产品名称和价格）。
- `EditItemTemplate` 包含编辑模式用户界面 （两个 TextBox Web 控件）。

DataList s`EditItemIndex`属性决定了什么`DataListItem`（如果有） 使用呈现`EditItemTemplate`。 具体而言，`DataListItem`其`ItemIndex`值与匹配 DataList s`EditItemIndex`使用呈现属性`EditItemTemplate`。 此模型适用于创建完全可编辑 DataList 时，可以在时间，但现在相隔编辑只有一项。

对于完全可编辑的 DataList，我们希望*所有*的`DataListItem`s 使用的可编辑界面来呈现。 若要实现此目的的最简单方法是定义中的可编辑界面`ItemTemplate`。 用于修改供应商地址信息，可编辑接口包含地址、 城市和国家/地区值为文本，然后选择文本框的供应商名称。

首先打开`BatchUpdate.aspx`页上，添加 DataList 控件，并设置其`ID`属性设置为`Suppliers`。 通过 DataList s 智能标记中，选择要添加一个名为的新 ObjectDataSource 控件`SuppliersDataSource`。


[![创建名为 SuppliersDataSource 新 ObjectDataSource](performing-batch-updates-cs/_static/image5.png)](performing-batch-updates-cs/_static/image4.png)

**图 2**： 创建新对象数据源命名`SuppliersDataSource`([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image6.png))


配置对象数据源检索数据使用`SuppliersBLL`类的`GetSuppliers()`方法 （请参见图 3）。 与前面的教程中，而不更新通过 ObjectDataSource 的供应商信息，我们将直接与业务逻辑层进行合作。 因此，在更新选项卡中设置为 （无） 下拉列表 （请参阅图 4）。


[![检索使用 GetSuppliers() 方法供应商信息](performing-batch-updates-cs/_static/image8.png)](performing-batch-updates-cs/_static/image7.png)

**图 3**： 检索供应商信息使用`GetSuppliers()`方法 ([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image9.png))


[![在更新选项卡中设置为 （无） 下拉列表](performing-batch-updates-cs/_static/image11.png)](performing-batch-updates-cs/_static/image10.png)

**图 4**： 在更新选项卡中设置为 （无） 下拉列表 ([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image12.png))


完成向导后，Visual Studio 会自动生成 DataList 的`ItemTemplate`显示标签 Web 控件中的数据源返回的每个数据字段。 我们需要修改此模板，可改为提供的编辑界面。 `ItemTemplate`可以通过使用 DataList s 智能标记中的编辑模板选项的设计器或直接通过声明性语法的自定义。

请花费片刻时间来创建用于编辑界面显示供应商的名为文本，但包括供应商的地址、 城市和国家/地区值的文本框。 进行这些更改后，在页 s 声明性语法应看起来类似于下面：


[!code-aspx[Main](performing-batch-updates-cs/samples/sample1.aspx)]

> [!NOTE]
> 与前面的教程中，在本教程中 DataList 必须具有启用了其视图状态。


中`ItemTemplate`我使用两个新的 CSS 类，m`SupplierPropertyLabel`并`SupplierPropertyValue`，其中已添加到`Styles.css`类，并配置为使用相同的样式设置`ProductPropertyLabel`和`ProductPropertyValue`CSS 类。


[!code-css[Main](performing-batch-updates-cs/samples/sample2.css)]

进行这些更改后，请访问此页上的通过浏览器。 如图 5 所示，每个 DataList 项供应商名称显示为文本，并使用文本框来显示地址、 城市和国家/地区。


[![DataList 中的每个供应商是可编辑](performing-batch-updates-cs/_static/image14.png)](performing-batch-updates-cs/_static/image13.png)

**图 5**: DataList 中的每个供应商是可编辑 ([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image15.png))


## <a name="step-2-adding-an-update-all-button"></a>步骤 2： 添加更新所有按钮

图 5 中的每个供应商有其地址、 城市和国家/地区字段显示在文本框中，当前没有任何更新按钮可用。 而不是让每个项的更新按钮，使用完全可编辑 DataLists 没有通常一次更新所有按钮的页上，单击时，更新*所有*DataList 中的记录。 对于本教程，让我们来添加两个更新所有按钮-一个在页面顶部，一个在底部 （尽管单击任一按钮将具有相同的效果）。

首先添加一个按钮 Web 控件上面的 DataList 并设置其`ID`属性设置为`UpdateAll1`。 接下来，添加第二个按钮 Web 控件下方 DataList，设置其`ID`到`UpdateAll2`。 设置`Text`到更新所有的两个按钮的属性。 最后，为这两个按钮创建事件处理程序`Click`事件。 而不会复制每个事件处理程序中的更新逻辑，let s 重构到第三种方法，该逻辑`UpdateAllSupplierAddresses`，具有事件处理程序只需调用此第三个方法。


[!code-csharp[Main](performing-batch-updates-cs/samples/sample3.cs)]

图 6 添加更新所有按钮后显示的页。


[![两个更新所有按钮已都添加到页面](performing-batch-updates-cs/_static/image17.png)](performing-batch-updates-cs/_static/image16.png)

**图 6**： 两个更新所有按钮已都添加到页面 ([单击以查看实际尺寸的图像](performing-batch-updates-cs/_static/image18.png))


## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>步骤 3： 更新所有供应商地址信息

与所有显示的编辑界面的 DataList 的项和添加的所有更新的按钮，所有这些仍编写代码来执行批处理更新。 具体而言，我们需要循环访问的 DataList 的项和调用`SuppliersBLL`类的`UpdateSupplierAddress`为每个方法。

集合`DataListItem`实例可以通过 DataList s 访问 DataList 该构成[`Items`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)。 对引用`DataListItem`，我们可以获取相应`SupplierID`从`DataKeys`集合和以编程方式引用文本框 Web 控件内`ItemTemplate`如以下代码所示：


[!code-csharp[Main](performing-batch-updates-cs/samples/sample4.cs)]

当用户单击全部更新按钮，之一`UpdateAllSupplierAddresses`方法循环访问每个`DataListItem`中`Suppliers`DataList 和调用`SuppliersBLL`类的`UpdateSupplierAddress`方法，传入相应的值。 地址、 城市或国家/地区传递的非输入值是值为`Nothing`到`UpdateSupplierAddress`（而不是空字符串），这会导致数据库`NULL`基础记录 s 字段。

> [!NOTE]
> 是增强，您可能想要将状态标签 Web 控件添加到提供一些确认消息，执行批处理更新后的页面。


## <a name="updating-only-those-addresses-that-have-been-modified"></a>更新已修改这些地址

用于此教程的调用的批处理更新算法`UpdateSupplierAddress`方法*每个*DataList，无论是否已更改其地址信息中的供应商。 而此类 blind 更新计划运行 t 通常性能问题，它们可能会导致多余记录如果您重新审核更改为数据库表。 例如，如果你使用触发器来记录所有`UPDATE`到`Suppliers`到审核表，每次用户单击全部更新按钮将在系统中，而不管用户是否进行任何为每个供应商创建一个新的审核记录的表更改。

ADO.NET DataTable 和 DataAdapter 类旨在支持批量更新，其中仅修改、 删除和新记录结果中的任何数据库通信。 DataTable 中的每一行都具有[`RowState`属性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)，该值指示行是否已添加到 DataTable，从它，修改、 删除或保持不变。 当最初填充数据表时，所有标记的行不变。 更改任何行的列的值标记为已修改。

在中`SuppliersBLL`我们通过一个供应商记录到中的第一个读取更新指定供应商的地址信息的类`SuppliersDataTable`，然后设置`Address`， `City`，和`Country`列的值使用以下代码：


[!code-csharp[Main](performing-batch-updates-cs/samples/sample5.cs)]

传入的地址、 城市和国家/地区值，此代码段将分配`SuppliersRow`在`SuppliersDataTable`而不考虑值没有变化。 这些修改会导致`SuppliersRow`s`RowState`属性被标记为已修改。 当数据访问层 s`Update`方法调用时，它发现`SupplierRow`已被修改，因此发送`UPDATE`命令到数据库。

假设，我们将代码添加到此方法以仅分配传入的地址、 城市和国家/地区值，如果它们与不同`SuppliersRow`s 现有值。 其中的地址、 城市和国家/地区将与现有的数据相同的情况下，在进行任何更改并`SupplierRow`s`RowState`将保留标记为不变。 最终结果是，当 DAL s`Update`调用方法，将对任何数据库调用，因为`SuppliersRow`尚未修改。

若要执行此更改，将为传入的地址、 城市和国家/地区值使用以下代码会盲目地将分配的语句：


[!code-csharp[Main](performing-batch-updates-cs/samples/sample6.cs)]

与此添加代码，DAL s`Update`方法发送`UPDATE`到只有那些其与地址相关的值已更改的记录的数据库的语句。

或者，我们无法跟踪是否有传入的地址字段和数据库数据之间的差异和，如果没有任何表，只需跳过对 DAL 的调用`Update`方法。 如果您重新使用 DB 定向方法，因为 DB 直接方法并不是 t 传递，此方法适用`SuppliersRow`实例，它的`RowState`可以进行检查，以确定是否实际需要的数据库调用。

> [!NOTE]
> 每次`UpdateSupplierAddress`调用方法、 调用数据库以检索有关已更新记录的信息。 然后，如果数据中有任何更改，另一个到数据库进行调用以更新表行。 可以通过创建优化此工作流`UpdateSupplierAddress`方法重载，接受`EmployeesDataTable`具有实例*所有*中的更改的`BatchUpdate.aspx`页。 然后，它可以进行一次调用到数据库，若要获取所有从记录`Suppliers`表。 然后可以枚举两个结果集，无法更新只有那些已发生更改的记录。


## <a name="summary"></a>总结

在本教程中我们已了解如何创建完全可编辑的 DataList，从而使用户可快速修改多个供应商的地址信息。 我们通过 DataList s 中定义的供应商的地址、 城市和国家/地区值的文本框中 Web 控件的编辑界面启动`ItemTemplate`。 接下来，我们添加了更新所有按钮的上方和下方 DataList。 用户已进行他的更改并单击全部更新按钮，之一后`DataListItem`s 枚举和调用`SuppliersBLL`类的`UpdateSupplierAddress`方法由。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Zack Jones 和 Ken Pespisa。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)
> [下一页](handling-bll-and-dal-level-exceptions-cs.md)
