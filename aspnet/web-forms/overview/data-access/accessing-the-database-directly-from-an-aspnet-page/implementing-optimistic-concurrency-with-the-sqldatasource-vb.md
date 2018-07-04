---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: 使用 SqlDataSource (VB) 实现乐观并发 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们会查看的乐观并发控制 essentials，然后探索如何实现使用 SqlDataSource 控件。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: a71e5ee06e4a970e7e6d6c3b5b0351ad218e0253
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391042"
---
<a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>使用 SqlDataSource (VB) 实现乐观并发
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe)或[下载 PDF](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> 在本教程中我们会查看的乐观并发控制 essentials，然后探索如何实现使用 SqlDataSource 控件。


## <a name="introduction"></a>介绍

在前面的教程中，我们将探讨如何添加插入、 更新和删除 SqlDataSource 控件的功能。 简单地说，要提供这些功能我们需要指定相应`INSERT`， `UPDATE`，或`DELETE`控件 s 中的 SQL 语句`InsertCommand`， `UpdateCommand`，或`DeleteCommand`属性以及相应中的参数`InsertParameters`， `UpdateParameters`，和`DeleteParameters`集合。 尽管可以手动指定这些属性和集合，配置数据源向导 s 高级的按钮提供了生成`INSERT`， `UPDATE`，和`DELETE`语句复选框，将自动创建这些语句基于`SELECT`语句。

与生成一起`INSERT`， `UPDATE`，和`DELETE`语句复选框，高级 SQL 生成选项对话框中包括使用开放式并发选项 （请参阅图 1）。 选中之后，`WHERE`子句中自动生成`UPDATE`和`DELETE`语句经过修改，以仅执行更新或删除如果由于用户修改基础数据库数据功能，那么 t 最后将数据加载到网格。


![可以添加乐观并发支持从高级 SQL 生成选项对话框](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**图 1**： 可以添加乐观并发支持从高级 SQL 生成选项对话框


回到[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程中，我们探讨乐观并发控制和如何将其添加到对象数据源的基础知识。 在本教程中我们将进行修饰的乐观并发控制 essentials 上，然后了解如何使用 SqlDataSource 实现。

## <a name="a-recap-of-optimistic-concurrency"></a>简要概述乐观并发

Web 应用程序允许多个用户同时使用，以编辑或删除相同的数据，存在一个用户可能会意外覆盖另一个 s 更改的可能性。 在中[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程中，我提供了下面的示例：

想象一下，两个用户，Jisun 和 Sam，同时也已访问的应用程序允许访问者以更新和删除产品通过 GridView 控件中页。 同时单击编辑按钮 Chai 时间大致相同。 Jisun 更改为 Chai 茶的产品名称，并单击更新按钮。 最终结果是`UPDATE`语句发送到数据库，这会设置*所有*的产品 s 可更新字段 (即使 Jisun 仅更新一个字段， `ProductName`)。 在此时间点，数据库包含值 Chai 茶，类别饮料，供应商特殊液体等用于此特定产品。 但是，Sam 的屏幕上 GridView 仍显示产品名称可编辑的 GridView 行中为 Chai。 几秒钟后 Jisun 的更改已提交，Sam 调味品到更新类别，并单击更新。 这会导致`UPDATE`语句发送到的数据库的产品名称设置为 Chai，`CategoryID`到相应的调味品类别 ID 和等等。 Jisun 的更改到的产品名称已被覆盖。

图 2 说明了这种交互。


[![两个用户同时更新记录时那里一个用户 s 可能更改覆盖其他 s](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**图 2**： 当两个用户同时更新的记录那里 s 可能有一个用户 s 将更改为覆盖其他 s ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png))


若要防止这种情况下打开的窗体[并发控制](http://en.wikipedia.org/wiki/Concurrency_control)必须实现。 [乐观并发](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)本教程的重点工作可能会有并发冲突不时地，大多数的此类冲突结束-赢得 t 时间出现发生的假设。 因此，如果确实会发生冲突，乐观并发控制只需将通知用户其更改-无法进行保存，因为另一个用户已修改相同的数据。

> [!NOTE]
> 对于其中假定将是许多并发冲突或者如果此类冲突不容许的应用程序，然后悲观并发控制可以改用。 回头[实现乐观并发](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)教程，了解在保守式并发控制的更深入讨论。


乐观并发控制的工作原理是确保要更新或删除的记录具有相同的值，像以前那样也随之更新或删除进程启动时。 例如，单击编辑按钮可编辑的 GridView 中后，记录的值将从数据库读取并显示在文本框和其他 Web 控件。 GridView 情况保存这些原始值。 更高版本之后用户使她的更改，并单击更新按钮，,`UPDATE`使用语句必须考虑原始值加上的新值并仅更新底层数据库记录，如果原始值的用户已开始编辑是仍在数据库中的值相同的。 图 3 描绘了这一序列的事件。


[![若要成功执行 Update 或 Delete，对于原始值必须等于当前的数据库值](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**图 3**: For Update 或 Delete succeed，原始值必须为等于当前的数据库值 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png))


有多种方法实现乐观并发 (请参阅[Peter A.Bromberg](http://peterbromberg.net/) s [Optmistic 并发更新逻辑](http://www.eggheadcafe.com/articles/20050719.asp)的简要介绍一下使用多种)。 使用 SqlDataSource （以及 ADO.NET 类型化数据集在我们的数据访问层中使用） 的方法增强`WHERE`子句，以包括所有原始值的比较。 以下`UPDATE`语句，例如，更新的名称和产品的价格仅当当前的数据库值是否等于更新 GridView 中的记录时最初检索到的值。 `@ProductName`并`@UnitPrice`参数包含由用户输入的新值，而`@original_ProductName`和`@original_UnitPrice`包含最初加载到了 GridView 时单击编辑按钮的值：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

我们将看到在本教程中，启用乐观并发控制使用 SqlDataSource 是像选中一个复选框一样简单。

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>步骤 1： 创建 SqlDataSource 支持乐观并发

首先打开`OptimisticConcurrency.aspx`页上从`SqlDataSource`文件夹。 将一个 SqlDataSource 控件从工具箱拖到设计器中，设置其`ID`属性设置为`ProductsDataSourceWithOptimisticConcurrency`。 接下来，单击控件 s 智能标记中的配置数据源链接。 从向导中的第一个屏幕，选择要使用`NORTHWINDConnectionString`单击下一步。


[![选择以使用 NORTHWINDConnectionString](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**图 4**： 选择与工作`NORTHWINDConnectionString`([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png))


此示例中我们将添加一个 GridView，使用户能够编辑`Products`表。 因此，从配置 Select 语句屏幕中，选择`Products`表从下拉列表，然后选择`ProductID`， `ProductName`， `UnitPrice`，和`Discontinued`列，如图 5 中所示。


[![在产品表中，返回 ProductID、 ProductName、 UnitPrice 和已停止使用的列](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**图 5**： 从`Products`表中，返回`ProductID`， `ProductName`， `UnitPrice`，并且`Discontinued`列 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png))


列后，单击高级按钮以打开高级 SQL 生成选项对话框。 检查生成`INSERT`， `UPDATE`，和`DELETE`语句并使用乐观并发复选框，然后单击确定 （回头参考图 1 屏幕截图）。 通过单击下一步，完成该向导，然后完成。

完成配置数据源向导后，请花费片刻时间来检查生成`DeleteCommand`并`UpdateCommand`属性和`DeleteParameters`和`UpdateParameters`集合。 若要执行此操作的最简单方法是单击左下角以查看页面 s 声明性语法中的源选项卡。 可以在其中找到`UpdateCommand`的值：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

使用中的七个参数`UpdateParameters`集合：


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

同样，`DeleteCommand`属性和`DeleteParameters`集合应如下所示：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

有益补充`WHERE`子句`UpdateCommand`和`DeleteCommand`属性 （并将其他参数添加到各自的参数集合），选择使用乐观并发选项调整其他两个属性：

- 更改[`ConflictDetection`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx)从`OverwriteChanges`（默认值） 到 `CompareAllValues`
- 更改[`OldValuesParameterFormatString`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx)从{0}（默认值） 到原始图像\_{0} 。

当数据 Web 控件调用 SqlDataSource s`Update()`或`Delete()`方法，它将传入的原始值。 如果 SqlDataSource s`ConflictDetection`属性设置为`CompareAllValues`，这些原始值添加到该命令。 `OldValuesParameterFormatString`属性提供了用于这些原始值参数的命名模式。 配置数据源向导将使用原始\_{0}并将在每个原始参数`UpdateCommand`并`DeleteCommand`属性并`UpdateParameters`和`DeleteParameters`集合相应地。

> [!NOTE]
> 因为我们不使用 SqlDataSource 控件 s 插入功能，可以删除`InsertCommand`属性并将其`InsertParameters`集合。


## <a name="correctly-handlingnullvalues"></a>正确处理`NULL`值

遗憾的是，增强`UPDATE`并`DELETE`语句自动生成的配置数据源向导使用乐观并发时不要*不*记录，其中包含与工作`NULL`值。 要了解原因，请考虑我们 SqlDataSource 的`UpdateCommand`:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`UnitPrice`中的列`Products`表可以有`NULL`值。 如果特定的记录都`NULL`值`UnitPrice`，则`WHERE`子句部分`[UnitPrice] = @original_UnitPrice`会*始终*计算结果为 False，因为`NULL = NULL`始终返回 False。 因此，它包含的记录`NULL`值不能编辑或删除，作为`UPDATE`并`DELETE`语句`WHERE`子句结束-赢得 t 返回要更新或删除任何行。

> [!NOTE]
> 此 bug 第一次报告给 Microsoft 在 2004 年 6 月的中[SqlDataSource 生成错误的 SQL 语句](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937)和据说计划在下一版本的 ASP.NET 中予以解决。


若要解决此问题，我们必须手动更新`WHERE`子句中同时`UpdateCommand`并`DeleteCommand`属性**所有**列可以具有`NULL`值。 一般情况下，更改`[ColumnName] = @original_ColumnName`到：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

此修改可直接通过声明性标记中，通过从属性窗口的 UpdateQuery 或 DeleteQuery 选项或通过更新和删除自定义 SQL 语句或存储的过程中配置数据的选项中指定的选项卡源向导。 同样，必须进行此修改*每个*中的列`UpdateCommand`并`DeleteCommand`s`WHERE`子句可以包含`NULL`值。

将此应用到我们的示例生成以下修改`UpdateCommand`和`DeleteCommand`值：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>步骤 2： 添加 GridView 编辑和删除选项

使用 SqlDataSource 配置为支持乐观并发，所有的就是将数据 Web 控件添加到页面，它利用此并发控制。 对于本教程，让我们来添加一个 GridView，提供了这两个编辑和删除的功能。 若要完成此操作，将 GridView 从工具箱拖到设计器和组及其`ID`到`Products`。 从 GridView s 智能标记，将其绑定到`ProductsDataSourceWithOptimisticConcurrency`SqlDataSource 控件添加在步骤 1 中。 最后，检查从智能标记的启用编辑和启用删除选项。


[![将 GridView 绑定到 SqlDataSource 和支持编辑和删除](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**图 6**： 将 GridView 绑定到 SqlDataSource 和启用编辑和删除 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png))


添加 GridView 后, 通过删除来配置它的外观`ProductID`更改 BoundField `ProductName` BoundField s`HeaderText`属性设置为产品和更新`UnitPrice`BoundField，以便其`HeaderText`属性只需价格。 理想情况下，我们 d 增强编辑界面要包括的 RequiredFieldValidator`ProductName`值和为 CompareValidator`UnitPrice`值 （以确保它 s 格式正确的数字值）。 请参阅[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程，了解更深入了解如何自定义编辑界面的 GridView s。

> [!NOTE]
> 必须启用 s 视图状态，因为 GridView 从 SqlDataSource 到传递的原始值是的 GridView 视图中存储状态。


以后进行这些修改到 GridView，GridView 和 SqlDataSource 声明性标记看起来应类似于下面：


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

若要查看操作中的乐观并发控制，打开两个浏览器窗口，并加载`OptimisticConcurrency.aspx`在这两页。 单击两个浏览器中的第一个产品的编辑按钮。 在一个浏览器中更改产品名称并单击更新。 在浏览器将回发和 GridView 将返回到其预先编辑模式，其中显示刚编辑的记录的新产品名称。

在第二个浏览器窗口中，更改 （但保留其原始值形式的产品名称） 的价格，并单击更新。 在回发时，网格将返回到其预先编辑模式，但对价格的更改不会记录。 第二个浏览器中显示相同的值的第一个新的产品名称与旧的价格。 在第二个浏览器窗口中所做的更改已丢失。 此外，所做的更改已丢失而安静模式，因为没有任何异常或消息，指示只发生了并发冲突。


[![第二个浏览器窗口中的更改是以无提示方式丢失](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**图 7**： 在第二个浏览器窗口已以无提示方式丢失的更改 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png))


为什么未提交的第二个浏览器的更改的原因是因为`UPDATE`语句的`WHERE`子句筛选出所有记录，因此未影响任何行。 让我们来看一下`UPDATE`再次语句：


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

当第二个浏览器窗口中更新的记录时，原始产品名称中指定`WHERE`子句没有 t 匹配会与现有的产品名称 （因为它进行了更改的第一个浏览器）。 因此，该语句`[ProductName] = @original_ProductName`将返回 False，和`UPDATE`不会影响任何记录。

> [!NOTE]
> Delete 的工作方式相同的方式。 使用两个打开的浏览器窗口，首先编辑使用其中一个，给定的产品，然后保存其更改。 在保存后所做的更改在一个浏览器中，单击同一中的其他产品的删除按钮。 由于原始值 don t 中匹配`DELETE`语句的`WHERE`子句中，删除以静默方式失败。


从最终用户 s 的角度在第二个浏览器窗口中，单击网格中的更新按钮返回到预先编辑模式，但他们的更改已丢失。 但是，这里 s 其更改无效 t 坚持没有可视反馈。 理想情况下，如果用户的更改都将丢失到并发冲突，我们 d 通知他们并，这样一来，保留在编辑模式下的网格。 让我们来看看如何实现此目的。

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>步骤 3： 确定当发生并发冲突

由于并发冲突，拒绝了一个具有所做的更改就好了并发冲突发生时向用户发出警报。 向用户发出警报，让的标签 Web 控件添加到名为页面顶部`ConcurrencyViolationMessage`其`Text`属性将显示以下消息： 已尝试更新或删除已由另一个用户同时更新的记录。 请查看其他用户更改然后重做你的更新或删除。 设置标签控件 s`CssClass`属性设置为警告，这是一个 CSS 类中定义`Styles.css`以红色、 斜体、 粗体和大字体显示文本。 最后，设置标签 s`Visible`并`EnableViewState`属性设置为`False`。 这将隐藏除仅位置显式设置这些回发的标签及其`Visible`属性设置为`True`。


[![将标签控件添加到页后，可以显示该警告](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**图 8**： 将标签控件添加到要显示该警告的页面 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png))


当执行更新或删除，GridView s`RowUpdated`和`RowDeleted`其数据源控件已执行的请求的更新或删除后，会激发事件处理程序。 我们可以确定多少行受影响的从这些事件处理程序执行的操作。 如果受影响的零行，我们想要显示`ConcurrencyViolationMessage`标签。

为两者创建事件处理程序`RowUpdated`和`RowDeleted`事件，并添加以下代码：


[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

在这两个事件处理程序中，我们检查`e.AffectedRows`属性，如果它等于 0，设置`ConcurrencyViolationMessage`标签 s`Visible`属性设置为`True`。 在中`RowUpdated`事件处理程序，我们还指示 GridView 继续处于编辑模式下通过设置`KeepInEditMode`属性设为 true。 在此过程中，我们需要重新绑定到网格的数据，以便其他用户的数据加载到编辑界面。 这通过调用 GridView s 实现`DataBind()`方法。

如图 9 所示，使用这些两个事件处理程序中，每次发生并发冲突时显示非常明显的消息。


[![在遇到并发冲突时显示一条消息](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**图 9**： 在遇到并发冲突时显示消息 ([单击以查看实际尺寸的图像](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png))


## <a name="summary"></a>总结

创建 web 应用程序时其中多个并发用户可能正在编辑相同的数据，务必要考虑并发控制选项。 默认情况下，ASP.NET 数据 Web 控件和数据源控件不使用任何并发控制。 正如我们看到在本教程中，实现乐观并发控制使用 SqlDataSource 是相当快速和方便。 SqlDataSource 处理大部分先为你添加扩充`WHERE`自动生成的子句`UPDATE`并`DELETE`但没有语句是在处理一些微妙之处`NULL`值列，如中所述正确处理`NULL`值部分。

本教程最后，我们检查 SqlDataSource。 我们提供剩余的教程将返回到使用 ObjectDataSource 和分层体系结构处理数据。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一篇](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
