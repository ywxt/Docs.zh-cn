---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: 删除 (C#) 时添加客户端确认 |Microsoft Docs
author: rick-anderson
description: 在我们到目前为止已创建的接口，用户可以数据意外删除时它们应单击编辑按钮，单击删除按钮。 在此，t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: b8cca6ece2eb008170192dc1774a6f88c1b37a21
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831112"
---
<a name="adding-client-side-confirmation-when-deleting-c"></a>删除 (C#) 时添加客户端的确认
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe)或[下载 PDF](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> 在我们到目前为止已创建的接口，用户可以数据意外删除时它们应单击编辑按钮，单击删除按钮。 在本教程中我们将添加一个客户端的确认对话框，单击删除按钮时出现的。


## <a name="introduction"></a>介绍

在过去的几个教程通过我们已看到了如何使用我们的应用程序体系结构、 对象、 数据源和数据 Web 控件配合使用来提供插入、 编辑和删除功能。 删除接口我们 ve 检查到目前为止已组成一个删除按钮，单击、 导致回发和调用 ObjectDataSource 的`Delete()`方法。 `Delete()`方法调用的业务逻辑层，将传播到数据访问层，发出的实际调用的配置的方法`DELETE`到数据库的语句。

虽然此用户界面可用于删除记录的 GridView、 detailsview 和 FormView 控件之间的访问者，但是它缺乏任何类型的确认，当用户单击删除按钮。 如果用户意外地单击删除按钮时它们应单击编辑，它们是要更新的记录将改为删除。 为了帮助避免此情形，在本教程中我们将添加一个客户端的确认对话框，单击删除按钮时出现的。

JavaScript`confirm(string)`函数将其字符串输入的参数显示为模式对话框，配备了两个按钮的确定和取消 （参见图 1） 内的文本。 `confirm(string)`函数将返回一个布尔值，具体取决于单击哪个按钮 (`true`，如果用户单击确定，并`false`如果他们单击取消)。


![JavaScript confirm(string) 方法显示在安装结束时，客户端的消息框](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**图 1**: JavaScript`confirm(string)`方法显示一个模式，客户端的消息框


在窗体提交，如果值为`false`返回，则从客户端事件处理程序已取消提交窗体。 使用此功能，我们可以让删除按钮的客户端`onclick`事件处理程序返回的值对的调用`confirm("Are you sure you want to delete this product?")`。 如果用户单击取消，`confirm(string)`将返回 false，从而导致取消提交窗体。 无回发时，删除结束-赢得 t 的删除按钮被单击的产品。 如果，但是，用户单击确定确认对话框中的，回发将继续减弱，将删除该产品。 请查阅[使用 JavaScript s`confirm()`方法控制窗体提交到](http://www.webreference.com/programming/javascript/confirm/)有关此技术的详细信息。

会稍有添加所需的客户端脚本不同，如果使用的模板与使用 CommandField 相比。 因此，在本教程中我们将看 FormView 和 GridView 示例。

> [!NOTE]
> 使用客户端确认技术，所讨论在本教程中，假定您的用户正在使用支持 JavaScript 的浏览器访问，并且必须启用 JavaScript。 如果这些假设任一特定用户，则返回 true，单击删除按钮将立即导致回发 （不显示确认消息框）。


## <a name="step-1-creating-a-formview-that-supports-deletion"></a>步骤 1： 创建 FormView 支持删除

首先，通过添加到 FormView`ConfirmationOnDelete.aspx`页中`EditInsertDelete`文件夹中，将其绑定到通过产品信息会提取新 ObjectDataSource`ProductsBLL`类的`GetProducts()`方法。 此外配置对象数据源，以便`ProductsBLL`类 s`DeleteProduct(productID)`方法映射到 ObjectDataSource 的`Delete()`方法; 确保下拉列表设置为 （无） INSERT 和 UPDATE 选项卡。 最后，检查 FormView s 智能标记中的启用分页复选框。

这些步骤之后，新 ObjectDataSource s 声明性标记将如下所示：


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

如我们在过去的示例未使用乐观并发，请花费片刻时间来清除 ObjectDataSource 的`OldValuesParameterFormatString`属性。

因为它已绑定到 ObjectDataSource 控件，仅支持删除 FormView 的`ItemTemplate`提供仅删除按钮，缺少的新建和更新按钮。 FormView s 声明性标记，但是，包含多余`EditItemTemplate`和`InsertItemTemplate`，可以删除的。 请花费片刻时间自定义`ItemTemplate`就是显示数据字段的产品的一个子集。 我已配置我的显示中的产品的名称`<h3>`标题上方 （以及删除按钮） 其供应商和类别名称。


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

这些更改，我们有一个完全正常运行的 web 页面，允许用户一次通过产品一个切换能够只需单击删除按钮删除产品。 图 2 显示了我们的进度的屏幕截图为止时的浏览器查看。


[![FormView 显示单个产品的信息](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**图 2**： 根据 FormView 显示信息有关单个产品 ([单击以查看实际尺寸的图像](adding-client-side-confirmation-when-deleting-cs/_static/image4.png))


## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>步骤 2： 从删除按钮的客户端 onclick 事件中调用 confirm(string) 函数

使用 FormView 创建，最后一步是配置此类删除按钮，当它访问者，JavaScript 单击 s`confirm(string)`调用函数。 将客户端侧脚本添加到按钮、 LinkButton 或 ImageButton 的客户端`onclick`事件，可以使用`OnClientClick property`，这是 ASP.NET 2.0 中新增。 由于我们想要具有的值`confirm(string)`函数返回，只需将此属性设置为： `return confirm('Are you certain that you want to delete this product?');`

此更改后删除 LinkButton s 声明性语法应如下所示：


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

该 s 都在这里就简单 ！ 图 3 所示为正在运行的此确认的屏幕截图。 单击删除按钮将显示确认对话框。 如果用户单击取消时，会取消回发并不会删除该产品。 如果，但是，用户单击确定，在回发继续和 ObjectDataSource 的`Delete()`调用方法时，通过在要删除的数据库记录。

> [!NOTE]
> 将字符串传递到`confirm(string)`用撇号 （而不是引号） 分隔的 JavaScript 函数。 在 JavaScript 中，可以使用任一字符分隔的字符串。 这样的分隔符的字符串传递到此处使用撇号`confirm(string)`不会产生歧义引入使用用于分隔符`OnClientClick`属性值。


[![一条确认信息是现在显示时单击删除按钮](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**图 3**: 确认是现在显示时单击删除按钮 ([单击以查看实际尺寸的图像](adding-client-side-confirmation-when-deleting-cs/_static/image7.png))


## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>步骤 3： 在 CommandField 中配置删除按钮的 OnClientClick 属性

确认对话框中使用时的按钮、 LinkButton 或 ImageButton 直接在模板中，可以通过只需配置是与之关联其`OnClientClick`属性以返回结果的 JavaScript`confirm(string)`函数。 但是，CommandField-这将删除按钮的字段添加到 GridView 或 DetailsView-没有`OnClientClick`可以以声明方式设置的属性。 相反，我们必须以编程方式引用在相应的 GridView 或 DetailsView s 中的删除按钮`DataBound`事件处理程序，然后将设置其`OnClientClick`那里属性。

> [!NOTE]
> 设置删除按钮 s 时`OnClientClick`中的相应属性`DataBound`事件处理程序，我们有权访问数据被绑定到当前记录。 这意味着我们可以扩展的确认消息包括有关的特定记录的详细信息如下所述，"确实要删除的 Chai 产品？" 此类自定义，也可以在模板中使用数据绑定语法。


做法是设置到`OnClientClick`CommandField，let s 中删除按钮的属性向页添加 GridView。 配置为使用相同的 ObjectDataSource 控件 FormView 使用此 GridView。 此外限制 GridView 的 BoundFields 将只包括产品的名称、 类别和供应商。 最后，检查从 GridView s 智能标记启用删除复选框。 这将为 GridView s 添加 CommandField`Columns`集合，其`ShowDeleteButton`属性设置为`true`。

进行这些更改后，您的 GridView s 声明性标记应如下所示：


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField 包含单个删除 LinkButton 实例可以以编程方式访问从 GridView 的`RowDataBound`事件处理程序。 一旦引用，我们可以设置其`OnClientClick`属性相应地。 创建事件处理程序`RowDataBound`事件使用以下代码：


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

此事件处理程序适用于数据行 （那些将具有删除按钮），并开始通过以编程方式引用删除按钮。 在常规使用以下模式：


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType*是 CommandField-按钮、 LinkButton 或 ImageButton 正在使用的按钮的类型。 默认情况下，CommandField 使用 Linkbutton，但这可以通过 CommandField s 自定义`ButtonType property`。 *CommandFieldIndex*是中的 GridView s CommandField 的序号索引`Columns`集合，而*controlIndex*是 CommandField s 中的删除按钮的索引`Controls`集合。 *ControlIndex*值取决于在 CommandField 中按钮 s 的位置相对于其他按钮。 例如，如果 CommandField 中显示的唯一按钮是删除按钮，使用的索引为 0。 不过，如果有 s 位于删除按钮，一个编辑按钮使用的索引 2。 使用索引为 2 的原因是因为两个控件添加的删除按钮之前 CommandField: 编辑按钮和 LiteralControl s 用来添加编辑和删除按钮之间的一些空间。

特定示例中，CommandField 使用 Linkbutton 和，最左侧的字段中，具有*commandFieldIndex*为 0。 由于没有任何其他按钮，但在 CommandField 删除按钮，我们使用*controlIndex*为 0。

在引用中 CommandField 删除按钮之后, 我们接下来获取绑定到当前的 GridView 行的产品有关的信息。 最后，我们将设置删除按钮的`OnClientClick`适当的 javascript 中，其中包括产品的名称的属性。 由于 JavaScript 字符串传递到`confirm(string)`使用的撇号我们必须转义产品的名称中出现的任何撇号分隔函数。 任何撇号产品的名称中使用的转义具体而言，"`\'`"。

完成这些更改中，单击删除按钮 GridView 显示一个自定义的确认对话框中 （见图 4） 中。 作为与确认 messagebox 从 FormView，如果用户单击取消按钮在回发被取消时，从而防止发生删除操作。

> [!NOTE]
> 此外可以使用此方法以编程方式访问在 DetailsView 中 CommandField 删除按钮。 对于 DetailsView，但是，d 你创建的事件处理程序`DataBound`事件，因为 DetailsView 没有`RowDataBound`事件。


[![单击 GridView s 删除按钮将显示一个自定义的确认对话框](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**图 4**： 单击删除按钮的 GridView s 显示自定义确认对话框 ([单击以查看实际尺寸的图像](adding-client-side-confirmation-when-deleting-cs/_static/image10.png))


## <a name="using-templatefields"></a>使用 Templatefield

CommandField 的缺点之一是其按钮必须通过索引来访问和生成的对象，必须强制转换为相应的按钮类型 （按钮、 LinkButton 或 ImageButton）。 使用"幻数"和硬编码类型邀请直到运行时将不能发现的问题。 例如，如果你或其他开发人员将新的按钮添加到在某个时间点以后 （例如编辑按钮） 或更改 CommandField`ButtonType`属性，现有的代码仍将编译没有错误，但访问的页面可能会引发异常或意外的行为，具体取决于如何编写您的代码和所做的更改。

另一种方法是将 GridView 和 DetailsView 的命令转换为 Templatefield。 这将生成与 TemplateField `ItemTemplate` CommandField 中每个按钮具有 LinkButton （或按钮或 ImageButton）。 这些按钮`OnClientClick`属性可以以声明方式分配，如我们看到的 FormView，或可以以编程方式访问在相应`DataBound`事件处理程序使用以下模式：


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

其中*controlID*是按钮 s 的值`ID`属性。 虽然此模式仍需要硬编码的类型强制转换，它无需为编制索引，允许布局更改不会导致运行时错误。

## <a name="summary"></a>总结

JavaScript`confirm(string)`函数是用于控制窗体提交工作流的常用的技术。 执行时，该函数显示模式，客户端的对话框，其中包含两个按钮，确定和取消。 如果用户单击确定，`confirm(string)`函数返回`true`; 单击取消返回`false`。 此功能，结合一个浏览器的行为来取消提交窗体，如果在提交过程中的事件处理程序返回`false`，可以用于删除一条记录时显示确认消息框。

`confirm(string)`函数可与一个按钮 Web 控件的客户端相关联`onclick`事件处理程序通过控件的`OnClientClick`属性。 使用模板-FormView 的模板之一或在 detailsview GridView-TemplateField 中的删除按钮时设置此属性可以是以声明方式或以编程方式，在本教程中所示。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一页](implementing-optimistic-concurrency-cs.md)
> [下一页](limiting-data-modification-functionality-based-on-the-user-cs.md)
