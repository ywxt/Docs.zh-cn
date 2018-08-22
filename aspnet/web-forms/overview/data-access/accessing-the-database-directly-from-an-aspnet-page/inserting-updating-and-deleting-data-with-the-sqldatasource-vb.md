---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: 插入、 更新和删除数据与 SqlDataSource (VB) |Microsoft Docs
author: rick-anderson
description: 在前面的教程中我们了解到如何 ObjectDataSource 控件允许插入、 更新和删除的数据。 SqlDataSource 控件支持 t...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 3124d53bad0040938c6a1090971ceecdf8c92333
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825793"
---
<a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>插入、 更新和删除数据与 SqlDataSource (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe)或[下载 PDF](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> 在前面的教程中我们了解到如何 ObjectDataSource 控件允许插入、 更新和删除的数据。 SqlDataSource 控件支持相同的操作，方法是不同的但本教程演示如何配置 SqlDataSource 插入、 更新和删除数据。


## <a name="introduction"></a>介绍

如中所述[概述的插入、 更新和删除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)、 GridView 控件提供了内置的更新和删除功能，而 DetailsView 和 FormView 控件包括插入和支持编辑和删除功能。 这些数据修改功能可直接插入到数据源控件无需编写一行代码无需编写。 [概述的插入、 更新和删除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)检查使用 ObjectDataSource 来支持插入、 更新和删除与 GridView、 DetailsView 和 FormView 控件。 或者，SqlDataSource ObjectDataSource 代替。

回想一下，以支持插入、 更新和删除使用 ObjectDataSource 我们需要指定的对象层方法调用来执行插入、 更新或删除操作。 使用 SqlDataSource，我们需要提供`INSERT`， `UPDATE`，和`DELETE`SQL 语句 （或存储的过程） 来执行。 我们将看到在本教程中，这些语句可以手动创建或 SqlDataSource s 配置数据源向导可以自动生成。

> [!NOTE]
> 因为我们 ve 已经讨论过插入、 编辑和删除功能的 GridView、 DetailsView，和 FormView 控件，本教程将重点介绍如何配置 SqlDataSource 控件以支持这些操作。 如果需要温习实施这些功能的 GridView、 DetailsView 和 FormView，返回到编辑、 插入、 和删除数据教程中，从开始[概述的插入、 更新和删除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)。


## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>步骤 1： 指定`INSERT`，`UPDATE`，和`DELETE`语句

正如我们看到在过去的两个教程中，我们需要使用 SqlDataSource 控件从检索数据的已设置两个属性：

1. `ConnectionString`它指定什么数据库发送到，查询和
2. `SelectCommand`它指定的临时 SQL 语句或存储的过程的名称为返回的结果而执行。

有关`SelectCommand`参数的值，通过 SqlDataSource s 指定的值的参数`SelectParameters`集合并可以包含硬编码值，通用参数的源值 (查询字符串字段中，会话变量 Web 控件值和等），或可以以编程方式分配。 当 SqlDataSource 控件 s`Select()`方法从数据 Web 控件调用以编程方式或自动建立到数据库的连接、 参数值分配给查询和命令关闭添加到数据库。 然后返回结果为数据集或 DataReader，具体取决于控件的值`DataSourceMode`属性。

除了选择数据，可以使用 SqlDataSource 控件以插入、 更新和删除数据，通过提供`INSERT`， `UPDATE`，和`DELETE`大致相同的方式中的 SQL 语句。 只需将分配`InsertCommand`， `UpdateCommand`，并`DeleteCommand`属性`INSERT`， `UPDATE`，并`DELETE`要执行的 SQL 语句。 如果语句有参数 （如最始终将它们），将它们包含在`InsertParameters`， `UpdateParameters`，和`DeleteParameters`集合。

一次`InsertCommand`， `UpdateCommand`，或`DeleteCommand`指定值，相应的数据 Web 控件 s 智能标记中的启用插入、 启用编辑或启用删除选项将变得可用。 若要说明这一点，让 s 执行中的示例`Querying.aspx`页中创建[使用 SqlDataSource 控件查询数据](querying-data-with-the-sqldatasource-control-vb.md)教程，并使之包括删除功能的补充。

首先打开`InsertUpdateDelete.aspx`并`Querying.aspx`从页`SqlDataSource`文件夹。 在设计器从`Querying.aspx`页上，从第一个示例中选择 SqlDataSource 和 GridView (`ProductsDataSource`和`GridView1`控件)。 选择两个控件后, 转到编辑菜单并选择复制 （或只需按 Ctrl + C）。 接下来，转到设计器中的`InsertUpdateDelete.aspx`并粘贴在控件中。 向移动两个控件后`InsertUpdateDelete.aspx`，测试浏览器中的页。 你应该会看到的值`ProductID`， `ProductName`，并`UnitPrice`列中的记录的所有`Products`数据库表。


[![所有产品都列出，请按 ProductID 排序](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**图 1**： 所有产品都列，按排序`ProductID`([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png))


## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>添加 SqlDataSource s`DeleteCommand`和`DeleteParameters`属性

现在我们有只是返回所有记录从 SqlDataSource`Products`表和一个 GridView，呈现此数据。 我们的目标是将此示例允许用户删除通过 GridView 的产品进行扩展。 若要完成此我们需要指定 SqlDataSource 控件 s 的值`DeleteCommand`和`DeleteParameters`属性，然后配置 GridView 来支持删除。

`DeleteCommand`和`DeleteParameters`可以多种方式指定属性：

- 通过声明性语法
- 于在设计器中的属性窗口
- 从指定自定义 SQL 语句或存储的过程中配置数据源向导屏幕
- 通过高级按钮从一个表中查看屏幕在配置数据源向导中指定列中，这实际上会自动将生成`DELETE`中使用的 SQL 语句和参数集合`DeleteCommand`和`DeleteParameters`属性

我们将介绍如何自动具有`DELETE`步骤 2 中创建的语句。 现在，允许使用设计器中，在属性窗口，尽管配置数据源向导或声明性语法选项就很合适。

中的设计器从`InsertUpdateDelete.aspx`，单击`ProductsDataSource`SqlDataSource 然后调出属性窗口 （从视图菜单中，选择属性窗口中，或只需按 F4）。 选择 DeleteQuery 属性，这将显示一系列省略号。


![从属性窗口中选择 DeleteQuery 属性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**图 2**： 从属性窗口中选择 DeleteQuery 属性


> [!NOTE]
> SqlDataSource 不具有 DeleteQuery 属性。 相反，DeleteQuery 是组成`DeleteCommand`和`DeleteParameters`属性并查看通过设计器窗口时仅列出在属性窗口中。 如果您查看时在源视图中属性窗口中，您会发现`DeleteCommand`属性改为。


单击要打开命令和参数编辑器对话框的 DeleteQuery 属性中的省略号框 （见图 3）。 在此对话框中，你可以指定`DELETE`SQL 语句指定的参数。 输入以下查询到`DELETE`命令文本框 (可以手动或使用查询生成器中，如果您愿意):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

接下来，单击刷新参数按钮以添加`@ProductID`到下面的参数列表的参数。


[![从属性窗口中选择 DeleteQuery 属性](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**图 3**： 从属性窗口中选择 DeleteQuery 属性 ([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png))


不要*不*提供此参数 （不定义其参数源位于 None） 的值。 一旦我们将删除支持添加到 GridView，GridView 将自动提供此参数值，使用的值及其`DataKeys`其删除按钮被单击的行的集合。

> [!NOTE]
> 中使用的参数名称`DELETE`查询*必须*的名称相同`DataKeyNames`GridView、 detailsview 和 FormView 中的值。 也就是说中的参数`DELETE`语句特意名为`@ProductID`(而不是，即`@ID`)，因为产品表 （和 GridView 中的 DataKeyNames 值） 中的主键列名称是`ProductID`。


如果参数名称和`DataKeyNames`值不匹配，GridView 不能自动分配参数值从`DataKeys`集合。

在命令和参数编辑器对话框中输入与删除相关的信息后单击确定并转到源视图来检查生成的声明性标记：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

请注意添加`DeleteCommand`属性并将`<DeleteParameters>`部分和名为的参数对象`productID`。

## <a name="configuring-the-gridview-for-deleting"></a>配置用于删除 GridView

使用`DeleteCommand`添加属性，GridView s 智能标记现在包含启用删除选项。 请继续并选中此复选框。 如中所述[概述的插入、 更新和删除](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)，这将导致 GridView 添加与 CommandField 其`ShowDeleteButton`属性设置为`True`。 如图 4 所示，通过浏览器访问页面时是包含一个删除按钮。 通过删除某些产品测试出此页。


[![每个 GridView 行现在包括一个删除按钮](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**图 4**： 每个 GridView 行现在包括一个删除按钮 ([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png))


单击删除按钮，产生的回发，GridView 将分配`ProductID`参数的值的`DataKeys`集合值的行的删除按钮被单击，并调用 SqlDataSource 的`Delete()`方法。 SqlDataSource 控件随后连接到数据库并执行`DELETE`语句。 然后，GridView 重新绑定到 SqlDataSource 取回，显示当前的产品集 （其中不再包括只是删除记录）。

> [!NOTE]
> 由于 GridView 使用其`DataKeys`集合来填充 SqlDataSource 参数，它 s 重要的 GridView s`DataKeyNames`属性设置为列构成的主键，SqlDataSource 的`SelectCommand`返回这些列。 此外，它非常重要的参数名中 SqlDataSource s`DeleteCommand`设置为`@ProductID`。 如果`DataKeyNames`属性未设置或未命名参数`@ProductsID`，单击删除按钮将导致回发，但实际上获胜的不会删除任何记录。


图 5 以图形方式描绘了这种交互。 回头[检查与插入、 更新和删除的事件相关联](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)教程，了解与插入、 更新和删除数据 Web 控件关联的事件链上的更多详细讨论。


![单击删除按钮在 GridView 中的调用 SqlDataSource s delete （） 方法](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**图 5**： 单击删除按钮在 GridView 中的调用 SqlDataSource 的`Delete()`方法


## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>步骤 2： 自动生成`INSERT`，`UPDATE`，和`DELETE`语句

为步骤 1，将检查`INSERT`， `UPDATE`，和`DELETE`可以通过属性窗口或控件 s 声明性语法指定 SQL 语句。 但是，此方法要求，我们手动写出 SQL 语句，将非常单调且容易出错。 幸运的是，配置数据源向导提供了一个选项，使`INSERT`， `UPDATE`，和`DELETE`使用指定的列从一个表中查看屏幕时自动生成的语句。

让我们来了解此自动生成选项。 向设计器中添加 DetailsView`InsertUpdateDelete.aspx`并设置其`ID`属性设置为`ManageProducts`。 接下来，从 DetailsView s 智能标记，选择创建新的数据源并创建名为 SqlDataSource `ManageProductsDataSource`。


[![创建名为 ManageProductsDataSource 新 SqlDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**图 6**： 创建新 SqlDataSource 命名`ManageProductsDataSource`([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png))


从配置数据源向导中，选择使用`NORTHWINDConnectionString`连接字符串，并单击下一步。 从配置 Select 语句屏幕中，将指定的列从表或视图的单选按钮处于选中状态并选取`Products`从下拉列表中的表。 选择`ProductID`， `ProductName`， `UnitPrice`，和`Discontinued`复选框列表中的列。


[![使用产品表，返回 ProductID、 ProductName、 UnitPrice 和已停止使用的列](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**图 7**： 使用`Products`表中，返回`ProductID`， `ProductName`， `UnitPrice`，并且`Discontinued`列 ([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png))


若要自动生成`INSERT`， `UPDATE`，并`DELETE`语句基于所选的表和列，单击高级按钮，然后检查生成`INSERT`， `UPDATE`，并`DELETE`语句复选框。


![检查生成 INSERT、 UPDATE 和 DELETE 语句复选框](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**图 8**： 检查生成`INSERT`， `UPDATE`，和`DELETE`语句复选框


将生成`INSERT`， `UPDATE`，和`DELETE`语句复选框仅将是可选中如果所选择的表具有主键，并且返回的列列表中包含的主键列 （或列）。 使用乐观并发复选框，这将成为可选择一次生成`INSERT`， `UPDATE`，并`DELETE`语句复选框已选中，将增加`WHERE`子句在随后出现`UPDATE`和`DELETE`语句，以提供乐观并发控制。 现在，将此复选框保留为未选中状态;在下一教程中，我们将介绍使用 SqlDataSource 控件的开放式并发。

在检查生成后`INSERT`， `UPDATE`，和`DELETE`语句复选框，单击确定以返回到配置 Select 语句屏幕中，然后单击下一步，并在完成，以完成配置数据源向导。 完成该向导，时 Visual Studio 会将 BoundFields 添加到的 DetailsView `ProductID`， `ProductName`，并`UnitPrice`列和有关 CheckBoxField`Discontinued`列。 从 DetailsView s 智能标记，以便用户访问此页可以单步执行产品检查启用分页选项。 清除 DetailsView s 还`Width`和`Height`属性。

请注意，智能标记有可用的启用插入、 启用编辑和启用删除选项。 这是因为 SqlDataSource 包含的值，其`InsertCommand`， `UpdateCommand`，和`DeleteCommand`，如下面的声明性语法所示：

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

请注意 SqlDataSource 控件已自动设置的值及其`InsertCommand`， `UpdateCommand`，和`DeleteCommand`属性。 中引用的列的一套`InsertCommand`并`UpdateCommand`属性基于中`SELECT`语句。 也就是说，而不是让*每个*产品中的列`InsertCommand`和`UpdateCommand`中, 指定这些列`SelectCommand`(更少`ProductID`，这省略，因为它 s [`IDENTITY`列](http://www.sqlteam.com/item.asp?ItemID=102)、 编辑时，不能更改其值并且其自动分配插入时)。 另外，若要在每个参数`InsertCommand`， `UpdateCommand`，并`DeleteCommand`属性中的相应参数`InsertParameters`， `UpdateParameters`，并`DeleteParameters`集合。

若要打开 DetailsView 的数据修改功能，请启用插入、 启用编辑和启用删除其智能标记中的选项。 这会添加与 CommandField 及其`ShowInsertButton`， `ShowEditButton`，并`ShowDeleteButton`属性设置为`True`。

访问在浏览器页面，并记下编辑、 删除和 DetailsView 中包含的新按钮。 单击编辑按钮将变为编辑模式，其中显示了每个 BoundField DetailsView 其`ReadOnly`属性设置为`False`（默认值） 作为文本框中，并为一个复选框 CheckBoxField。


[![在 DetailsView s 默认编辑界面](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**图 9**: DetailsView s 默认编辑界面 ([单击以查看实际尺寸的图像](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png))


同样，可以删除当前所选的产品，或向系统添加一个新的产品。 由于`InsertCommand`语句仅适用于`ProductName`， `UnitPrice`，和`Discontinued`列，其他列将可以`NULL`或插入时的数据库分配其默认值。 如果使用 ObjectDataSource，就像`InsertCommand`缺少列不允许任何数据库表`NULL`s 和 don t 具有默认值，将发生 SQL 错误时尝试执行`INSERT`语句。

> [!NOTE]
> 插入和编辑接口的 DetailsView s 缺乏任何类型的自定义项或验证。 若要添加验证控件或自定义接口，您需要将 BoundFields 转换为 Templatefield。 请参阅[向编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)并[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程的详细信息。


此外，请记住，用于更新和删除，说明如何使用当前产品 s`DataKey`值，该值时才存在`DataKeyNames`配置属性。 如果编辑或删除似乎不起作用，确保`DataKeyNames`属性设置。

## <a name="limitations-of-automatically-generating-sql-statements"></a>自动生成 SQL 语句的限制

由于生成`INSERT`， `UPDATE`，并`DELETE`语句选项才可用时变得更加复杂的查询用于选择从表中的列都必须写入自己`INSERT`， `UPDATE`，和`DELETE`像在步骤 1 中执行的语句。 通常情况下，SQL`SELECT`语句使用`JOIN`s 若要恢复的一个或多个查找表中的数据显示目的 (例如使重新`Categories`表的`CategoryName`字段中时显示的产品信息)。 同时，我们可能想要允许用户编辑、 更新或将数据插入到核心表 (`Products`，在这种情况下)。

虽然`INSERT`， `UPDATE`，和`DELETE`语句可以手动输入，请考虑以下省时的提示。 最初，以便它返回将仅从数据设置 SqlDataSource`Products`表。 使用配置数据源向导的指定的列从表或视图的屏幕，以便可以自动生成`INSERT`， `UPDATE`，和`DELETE`语句。 然后，完成向导后，选择要配置从属性窗口 SelectQuery （或者，或者，请返回到的配置数据源向导，但使用指定自定义 SQL 语句或存储的过程选项）。 然后更新`SELECT`语句以包括`JOIN`语法。 此方法的优点是省时的自动生成的 SQL 语句，并允许进行更多自定义`SELECT`语句。

自动生成的另一个限制`INSERT`， `UPDATE`，并`DELETE`语句是中的列`INSERT`并`UPDATE`语句基于返回的列`SELECT`语句。 我们可能需要更新或插入更多或更少的字段，但是。 例如，在步骤 2 中示例中，也许我们想要具有`UnitPrice`BoundField 是只读的。 在这种情况下，其长度应不 t 出现在`UpdateCommand`。 或者，我们可能想要在 GridView 中设置不会出现一个表字段的值。 例如，当添加新记录我们可能希望`QuantityPerUnit`值设置为待办事项。

如果此类自定义项是必需的则需要以手动，使其通过属性窗口中，指定自定义 SQL 语句或存储的过程选项在向导中，或通过声明性语法。

> [!NOTE]
> 当添加参数，而没有相应的字段的数据中的 Web 控件时，请记住，这些参数值将需要为分配以某种方式的值。 这些值可以是： 硬编码中直接`InsertCommand`或`UpdateCommand`; 可以来自一些预定义源 （查询字符串、 会话状态、 Web 控件在页上，依次类推）; 或者可以以编程方式分配，如我们在前面的教程中看到。


## <a name="summary"></a>总结

为了使数据 Web 控件以利用其内置的插入、 编辑和删除功能，它们绑定到数据源控件必须提供这种功能。 对于 SqlDataSource，这意味着`INSERT`， `UPDATE`，并`DELETE`SQL 语句必须分配给`InsertCommand`， `UpdateCommand`，并`DeleteCommand`属性。 这些属性和相应的参数集合，可以手动添加或通过配置数据源向导自动生成。 在本教程中，我们将探讨这两种技术。

我们探讨了与对象的数据源中使用乐观并发[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程。 SqlDataSource 控件还提供开放式并发支持。 如自动生成时在步骤 2 中所述`INSERT`， `UPDATE`，和`DELETE`语句，该向导提供了使用开放式并发选项。 我们将在下一教程中看到的通过 SqlDataSource 使用乐观并发修改`WHERE`中的子句`UPDATE`和`DELETE`语句，以确保其他列的值还 t 自上次数据更改在页面上显示。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [下一页](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
