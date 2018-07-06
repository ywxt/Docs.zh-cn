---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
title: 添加和响应 gridview (VB) 的按钮的 |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将介绍如何将自定义按钮，添加到模板和 GridView 或 DetailsView 控件的字段。 具体而言，我们将标示...
ms.author: aspnetcontent
ms.date: 09/13/2006
ms.assetid: 06c6bbd2-4bdc-435b-87a3-df2c868f4baa
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1e35c6655506b5ec79efe8a5000e136e865854f2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831688"
---
<a name="adding-and-responding-to-buttons-to-a-gridview-vb"></a>添加和响应的按钮 GridView (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_VB.exe)或[下载 PDF](adding-and-responding-to-buttons-to-a-gridview-vb/_static/datatutorial28vb1.pdf)

> 在本教程中我们将介绍如何将自定义按钮，添加到模板和 GridView 或 DetailsView 控件的字段。 具体而言，我们将构建具有允许用户翻页查看供应商 FormView 的接口。


## <a name="introduction"></a>介绍

虽然许多报告方案涉及到报表数据的只读访问它 s 不常见的报表才能包括执行操作的能力取决于显示的数据。 通常这涉及到添加按钮、 LinkButton 或 ImageButton Web 控件与在报表中显示每个记录，单击，导致回发并调用一些服务器端代码。 编辑和删除记录的基础上的数据是最常见的例子。 实际上，正如我们看到的开头[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程中，编辑和删除很常见的 GridView、 DetailsView 和 FormView 控件可以支持此类功能而不用需要编写一行代码。

除了编辑和删除按钮、 GridView、 DetailsView 和 FormView 控件还可以包括按钮、 Linkbutton 或 ImageButtons，单击时，执行一些自定义服务器端逻辑。 在本教程中我们将介绍如何将自定义按钮，添加到模板和 GridView 或 DetailsView 控件的字段。 具体而言，我们将构建具有允许用户翻页查看供应商 FormView 的接口。 对于给定的供应商，FormView 将显示一个按钮 Web 控件，如停止使用，如果单击，将标记所有其关联的产品以及供应商有关的信息。 此外，GridView 列出了这些产品的所选的供应商，提供与每个行包含增加价格和折扣价格的按钮，如果单击，引发或降低产品的`UnitPrice`（参见图 1） 的 10%。


[![FormView 和 GridView 包含执行自定义操作的按钮](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image1.png)

**图 1**： 这两个 FormView 和 GridView 包含按钮，执行自定义操作 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image3.png))


## <a name="step-1-adding-the-button-tutorial-web-pages"></a>步骤 1： 添加按钮教程 Web 页

我们看看如何添加自定义按钮之前，让 s 先花点时间在我们的网站项目，我们需要在本教程中创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`CustomButtons`。 接下来，将以下两个 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `CustomButtons.aspx`


![将 ASP.NET 页面添加自定义与按钮相关的教程](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image4.png)

**图 2**： 将 ASP.NET 页面添加自定义与按钮相关的教程


在其他文件夹中，喜欢`Default.aspx`在`CustomButtons`文件夹将在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image5.png)

**图 3**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image7.png))


最后，将页面添加到条目为`Web.sitemap`文件。 具体而言，在分页和排序之后添加以下标记`<siteMapNode>`:


[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 在左侧菜单现在包含用于编辑、 插入和删除教程的项。


![站点图现在包括自定义按钮教程的条目](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image8.png)

**图 4**： 站点图现在包括自定义按钮教程的条目


## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>步骤 2： 添加列出供应商 FormView

让我们来开始使用本教程通过添加 FormView，其中列出了供应商。 如简介中所述，此 FormView 将允许用户逐页浏览供应商，显示在 GridView 中的供应商提供的产品。 此外，此 FormView 将包括一个按钮，单击时，会将标记的所有供应商的产品为停止使用。 我们将自定义按钮添加到 FormView 在意自己之前，让，使其显示的供应商信息的第一次只需创建 FormView 的 s。

首先打开`CustomButtons.aspx`页中`CustomButtons`文件夹。 通过从工具箱拖到设计器和组拖动到页面添加 FormView 及其`ID`属性设置为`Suppliers`。 从 FormView s 智能标记，选择创建名为新 ObjectDataSource `SuppliersDataSource`。


[![创建名为 SuppliersDataSource 新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image9.png)

**图 5**： 创建新对象数据源命名`SuppliersDataSource`([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image11.png))


配置此新对象数据源，以便它将查询从`SuppliersBLL`类的`GetSuppliers()`方法 （请参阅图 6）。 由于此 FormView 不用于更新供应商信息，请选择更新选项卡中的下拉列表从 (None) 选项提供一个接口。


[![配置数据源以使用 SuppliersBLL 类的 GetSuppliers() 方法](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image12.png)

**图 6**： 配置要使用的数据源`SuppliersBLL`类 s`GetSuppliers()`方法 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image14.png))


在配置后 ObjectDataSource，Visual Studio 将生成`InsertItemTemplate`， `EditItemTemplate`，和`ItemTemplate`FormView 的。 删除`InsertItemTemplate`并`EditItemTemplate`并修改`ItemTemplate`，以便它显示只是供应商的公司名称和电话号码。 最后，打开 FormView 的分页支持从其智能标记的启用分页复选框 (或通过设置其`AllowPaging`属性设置为`True`)。 以后这些更改将页面 s 声明性标记看起来应类似于下面：


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample2.aspx)]

图 7 显示了 CustomButtons.aspx 页时的浏览器查看。


[![FormView 列出了公司名称和从当前所选的供应商的电话号码字段](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image15.png)

**图 7**： 列出了 FormView`CompanyName`和`Phone`字段从当前所选供应商 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image17.png))


## <a name="step-3-adding-a-gridview-that-lists-the-selected-supplier-s-products"></a>步骤 3： 添加一个 GridView，列出了所选供应商的产品

我们将停止所有产品按钮都添加到 FormView 的模板之前，让第一次都添加一个 GridView 下方列出的所选的供应商提供的产品 FormView 的 s。 若要实现此目的，向页面添加一个 GridView，设置其`ID`属性设置为`SuppliersProducts`，并添加名为新 ObjectDataSource `SuppliersProductsDataSource`。


[![创建名为 SuppliersProductsDataSource 新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image18.png)

**图 8**： 创建新对象数据源命名`SuppliersProductsDataSource`([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image20.png))


配置此 ObjectDataSource 使用 ProductsBLL 类的`GetProductsBySupplierID(supplierID)`方法 （请参阅图 9）。 虽然产品的价格调整将允许此 GridView，赢得 t 使用内置编辑或删除从 GridView 的功能。 因此，我们可以设置为 （无） 下拉列表的 ObjectDataSource s 更新、 插入和删除选项卡。


[![配置数据源以使用 ProductsBLL 类的 GetProductsBySupplierID(supplierID) 方法](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image21.png)

**图 9**： 配置要使用的数据源`ProductsBLL`类 s`GetProductsBySupplierID(supplierID)`方法 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image23.png))


由于`GetProductsBySupplierID(supplierID)`方法接受一个输入的参数、 ObjectDataSource 向导提示我们输入此参数值的源。 要传入`SupplierID`FormView 从值时，请将参数源下拉列表设置为控制和 ControlID 下拉列表到`Suppliers`（在步骤 2 中创建的 FormView ID）。


[![指示，供应商 Id 参数应来自于供应商 FormView 控件](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image24.png)

**图 10**： 指示*`supplierID`* 参数应该来自于`Suppliers`FormView 控件 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image26.png))


完成 ObjectDataSource 向导后，命令将 BoundField 或 CheckBoxField 每个产品的数据字段包含 GridView。 允许 s 修整一下此显示只`ProductName`和`UnitPrice`连同 BoundFields `Discontinued` CheckBoxField; 此外，让 s 格式`UnitPrice`BoundField，使其文本设置为货币格式，如。 在 GridView 和`SuppliersProductsDataSource`ObjectDataSource s 声明性标记应类似于以下标记：


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample3.aspx)]

此时将在本教程中显示母版/详细信息报表，这样就允许用户从顶部 FormView 选取一个供应商并查看底部 GridView 通过该供应商提供的产品。 图 11 从 FormView 选择为全供应商时显示此页的屏幕截图。


[![GridView 中显示所选供应商的产品](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image27.png)

**图 11**: GridView 中显示所选供应商产品 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image29.png))


## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>步骤 4： 创建 DAL 和 BLL 方法，以停止所有产品的供应商

我们可以将按钮添加到 FormView 之前，单击时，会终止所有的供应商的产品中，我们首先需要将方法添加到 DAL 和执行此操作的 BLL。 具体而言，此方法将被命名为`DiscontinueAllProductsForSupplier(supplierID)`。 单击 FormView 的按钮时，我们将调用此方法在业务逻辑层中，传递在所选的供应商 s `SupplierID`; BLL 将然后向下调用相应的数据访问层方法将发出到`UPDATE`语句终止指定供应商的产品数据库。

因为我们已经在我们前面的教程，我们将使用一种自下而上的方法，开始创建 DAL 方法，然后 BLL 方法，并最后在 ASP.NET 页面中实现的功能。 打开`Northwind.xsd`类型中的数据集`App_Code/DAL`文件夹并添加到新方法`ProductsTableAdapter`(右键单击`ProductsTableAdapter`，然后选择添加查询)。 执行此操作将打开 TableAdapter 查询配置向导中，我们介绍了添加新方法的过程。 首先，该值指示我们 DAL 方法将使用的临时 SQL 语句。


[![创建 DAL 方法使用的临时 SQL 语句](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image30.png)

**图 12**： 创建 DAL 的方法使用一个临时 SQL 语句 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image32.png))


接下来，向导会提示我们关于哪些类型的查询来创建。 由于`DiscontinueAllProductsForSupplier(supplierID)`方法将需要更新`Products`设置的数据库表`Discontinued`为 1 的所有产品提供的指定字段*`supplierID`*，我们需要创建更新数据的查询。


[![选择更新查询类型](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image33.png)

**图 13**： 选择更新查询类型 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image35.png))


下一个向导屏幕提供现有 TableAdapter s`UPDATE`语句，更新每个字段中定义`Products`DataTable。 此查询文本替换为以下语句：


[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample4.sql)]

输入此查询，然后单击下一步，最后一个向导屏幕要求提供的新方法的名称后使用`DiscontinueAllProductsForSupplier`。 单击完成按钮完成该向导。 返回到数据集设计器时，您应看到中的新方法`ProductsTableAdapter`名为`DiscontinueAllProductsForSupplier(@SupplierID)`。


[![命名新的 DAL 方法 DiscontinueAllProductsForSupplier](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image36.png)

**图 14**： 新的 DAL 方法命名`DiscontinueAllProductsForSupplier`([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image38.png))


与`DiscontinueAllProductsForSupplier(supplierID)`数据访问层中创建的方法，我们的下一个任务是创建`DiscontinueAllProductsForSupplier(supplierID)`业务逻辑层中的方法。 若要完成此操作，请打开`ProductsBLL`类文件并添加以下：


[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample5.vb)]

此方法只是调用直至`DiscontinueAllProductsForSupplier(supplierID)`方法中传递所提供的 DAL *`supplierID`* 参数值。 如果没有任何只允许供应商的产品，在某些情况下停止使用的业务规则，这些规则应 BLL 中此处，实现。

> [!NOTE]
> 与不同`UpdateProduct`中重载`ProductsBLL`类，`DiscontinueAllProductsForSupplier(supplierID)`方法签名不包括`DataObjectMethodAttribute`属性 (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`)。 这将阻止`DiscontinueAllProductsForSupplier(supplierID)`从 ObjectDataSource s 配置数据源向导的下拉列表中更新选项卡的方法。我已省略此属性，因为我们将调用`DiscontinueAllProductsForSupplier(supplierID)`直接从我们的 ASP.NET 页面中的事件处理程序方法。


## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>步骤 5： 添加停止到 FormView 的所有产品按钮

与`DiscontinueAllProductsForSupplier(supplierID)`BLL 和 DAL 中的方法完成，添加所选的供应商是将一个按钮 Web 控件添加到 FormView s 停止所有产品的功能的最后一步`ItemTemplate`。 允许 s 添加与按钮文本，停止所有产品的供应商的电话号码下面这样的按钮和一个`ID`属性值为`DiscontinueAllProductsForSupplier`。 您可以通过单击 FormView s 智能标记中的编辑模板链接添加设计器通过此按钮 Web 控件 （请参阅图 15），或直接通过声明性语法。


[![添加停止所有产品按钮 Web 控件到 FormView 的 ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image39.png)

**图 15**： 将停止所有产品按钮 Web 控件都添加到 FormView s `ItemTemplate` ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image41.png))


当页面回发，才会进行用户访问和 FormView s 通过单击该按钮[`ItemCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx)激发。 若要执行的自定义代码以响应在单击此按钮，我们可以创建此事件的事件处理程序。 了解，不过，这`ItemCommand`事件时将触发*任何*FormView 内单击按钮、 LinkButton 或 ImageButton Web 控件。 这意味着，当用户从一个页面移动到另一个在 FormView`ItemCommand`触发事件; 当用户单击新建、 编辑或删除支持插入、 更新或删除 FormView 中相同的操作。

由于`ItemCommand`无论单击哪个按钮时，事件处理程序我们需要一种方法来确定已单击了停止所有产品按钮或某些其他按钮时触发。 若要实现此目的，我们可以设置按钮 Web 控件的`CommandName`为某些标识值的属性。 单击按钮时，这`CommandName`值传递到`ItemCommand`事件处理程序，使我们能够确定是否停止所有的产品按钮所单击的按钮。 将停止所有产品按钮 s 设置`CommandName`DiscontinueProducts 属性。

最后，让我们来使用客户端的确认对话框中，以确保用户确实想要停止所选供应商的产品。 中可以看到[删除时添加客户端确认](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb.md)教程中，这可以使用一些 JavaScript 完成。 具体而言，将按钮 Web 控件的 OnClientClick 属性设置为 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

进行这些更改后，FormView s 声明性语法应如以下所示：


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample6.aspx)]

接下来，创建事件处理程序的 FormView s`ItemCommand`事件。 此事件处理程序中，我们需要首先确定是否已单击停止所有产品按钮。 如果因此，我们想要创建的实例`ProductsBLL`类，并调用其`DiscontinueAllProductsForSupplier(supplierID)`方法，传入`SupplierID`的所选的 FormView:


[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample7.vb)]

请注意， `SupplierID` FormView 中当前所选的供应商可以访问使用 FormView s [ `SelectedValue`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)。 `SelectedValue`属性返回的第一个数据键值在 FormView 中显示该记录的值。 FormView s [ `DataKeyNames`属性](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)，指示的数据字段的数据从其键值值来自，已自动设置为`SupplierID`由 Visual Studio 时将对象数据源绑定到 FormView 后在步骤 2 中。

使用`ItemCommand`事件处理程序创建，请花费片刻时间来测试页。 浏览到 Cooperativa de Quesos Las Cabras 供应商 (它 s 中为我 FormView 第五个供应商)。 此供应商提供了两个产品，Queso Cabrales 和 Queso Manchego La Pastora，这两个*不*停止使用。

假设 Cooperativa de Quesos Las Cabras 已停止经营，因此其产品是停止使用。 单击停止所有产品的按钮。 这将显示客户端的确认对话框 （请参见图 16）。


[![Cooperativa de Quesos Las Cabras 提供两个活动产品](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image42.png)

**图 16**: Cooperativa de Quesos Las Cabras 提供两个活动产品 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image44.png))


如果单击确定在客户端的确认对话框中，提交窗体将继续，请在其中导致回发的 FormView s`ItemCommand`会触发事件。 我们创建的事件处理程序然后执行调用`DiscontinueAllProductsForSupplier(supplierID)`方法和不再使用的 Queso Cabrales 和 Queso Manchego La Pastora 产品。

如果禁用了 GridView 的视图状态，GridView 正在重新绑定到基础数据存储在每个回发时，，因此将立即更新以反映，这两种产品已现在不再使用 （请参阅图 17）。 如果，但是，不禁用了 GridView 中的视图状态，你将需要手动进行此更改后重新绑定到 GridView 数据。 若要完成此操作，只需进行到 GridView 的调用`DataBind()`方法后立即调用`DiscontinueAllProductsForSupplier(supplierID)`方法。


[![单击停止所有的产品按钮后，供应商的产品更新相应地受到了](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image45.png)

**图 17**： 单击停止所有的产品按钮后，供应商的产品更新相应地受到了 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image47.png))


## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-product-s-price"></a>步骤 6： 在调整产品的价格的业务逻辑层中创建的 UpdateProduct 重载

如停止所有产品按钮在 FormView 中使用为了添加按钮，用于增加和减少 GridView 中产品的价格我们需要首先将添加相应的数据访问层和业务逻辑层方法。 由于我们已更新 DAL 中的单个产品行的方法，我们可以通过创建新的重载，以提供此类功能`UpdateProduct`BLL 中的方法。

我们过去`UpdateProduct`重载已执行的产品字段为标量的输入值的某种组合中，并且然后更新指定的产品仅对这些字段。 为此重载中，我们将略有不同此标准并改为传入产品 s`ProductID`和用于调整百分比`UnitPrice`(而不是在新的传递，调整`UnitPrice`本身)。 将简化我们需要在 ASP.NET 页面代码隐藏类中编写的代码，这种方法，因为我们不需要确定当前产品 s 而费心 t `UnitPrice`。

`UpdateProduct`重载为本教程中如下所示：


[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample8.vb)]

此重载将检索有关通过 DAL s 指定的产品信息`GetProductByProductID(productID)`方法。 然后，它将检查是否产品 s`UnitPrice`分配数据库`NULL`值。 如果是，价格将保持不变。 如果，但是，有一个非`NULL``UnitPrice`值，该方法更新产品 s`UnitPrice`指定的 %(`unitPriceAdjustmentPercent`)。

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>步骤 7： 将增加和减少按钮添加到 GridView

GridView （和 DetailsView） 都由组成的字段的集合。 除了 BoundFields、 CheckBoxFields 和 Templatefield，ASP.NET 包括 ButtonField，其中，正如其名，将呈现为按钮、 LinkButton 或 ImageButton 的每一行的列。 类似于单击 FormView*任何*GridView 分页按钮、 编辑或删除按钮、 排序按钮等中的按钮导致回发，并引发 GridView s [ `RowCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)。

具有 ButtonField`CommandName`属性，可将指定的值分配给每个其按钮`CommandName`属性。 使用 FormView，喜欢`CommandName`所使用的值`RowCommand`事件处理程序，以确定被单击的按钮。

允许 s 将两个新 ButtonFields 添加到 GridView，另一个使用按钮文本价格 + 10%和另一个以文本价格介于-10%。 若要添加这些 ButtonFields，单击编辑列链接从 GridView s 智能标记，从左上角中的列表中选择 ButtonField 字段类型，单击添加按钮。


![将两个 ButtonFields 添加到 GridView](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image48.png)

**图 18**： 将两个 ButtonFields 添加到 GridView


移动两个 ButtonFields，以便它们显示为前两个 GridView 字段。 接下来，设置`Text`属性的这些两个 ButtonFields + 10%的价格和价格-10%和`CommandName`为 IncreasePrice 和 DecreasePrice，属性分别。 默认情况下，ButtonField Linkbutton 呈现其列的按钮。 这可以更改，但是，通过 ButtonField s [ `ButtonType`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)。 让具有呈现为常规下压按钮; 这些两个 ButtonFields s因此，设置`ButtonType`属性设置为`Button`。 图 19 显示的字段对话框的后进行了这些更改;后面的是 GridView s 声明性标记。


![配置 ButtonFields 文本、 CommandName 和 ButtonType 属性](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image49.png)

**图 19**： 配置 ButtonFields `Text`， `CommandName`，和`ButtonType`属性


[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample9.aspx)]

与创建这些 ButtonFields，最后一步是创建事件处理程序的 GridView s`RowCommand`事件。 此事件处理程序，如果因为而激发任一价格 + 10%或价格介于-10%按钮的单击，需要确定`ProductID`为其按钮被单击的行，然后调用`ProductsBLL`类的`UpdateProduct`方法，传入适当`UnitPrice`连同百分比调整`ProductID`。 下面的代码执行以下任务：

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample10.vb)]

若要确定`ProductID`行的价格 + 10%或价格介于-10%按钮被单击，我们需要查阅 GridView 的`DataKeys`集合。 此集合包含的值中指定的字段`DataKeyNames`每 GridView 行的属性。 因为 GridView s`DataKeyNames`属性设置为产品 id 通过 Visual Studio 时绑定到 GridView，ObjectDataSource`DataKeys(rowIndex).Value`提供`ProductID`指定*rowIndex*。

在自动传递 ButtonField *rowIndex*通过单击其按钮的行的`e.CommandArgument`参数。 因此，若要确定`ProductID`行的价格 + 10%或价格介于-10%按钮被单击，我们使用： `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`。

作为使用停止所有产品按钮，如果禁用了 GridView 的视图状态，GridView 正在重新绑定到基础数据存储在每个回发时，，因此将立即更新以反映，发生从单击的价格更改任一按钮。 如果，但是，不禁用了 GridView 中的视图状态，你将需要手动进行此更改后重新绑定到 GridView 数据。 若要完成此操作，只需进行到 GridView 的调用`DataBind()`方法后立即调用`UpdateProduct`方法。

图 20 显示的页时查看奶奶 Kelly 家居提供的产品。 图 21 显示结果后的价格 + 10%按钮点击两次以奶奶的梅分布和价格-10%按钮一次为 Cranberry 胡椒粉。


[![GridView 包括价格 + 10%和价格-10%按钮](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image50.png)

**图 20**: GridView 包括价格 + 10%和价格-10%按钮 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image52.png))


[![第一个和第三个产品的价格已更新通过价格 + 10%和价格-10%按钮](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image53.png)

**图 21**: 价格的第一个和第三个产品已更新通过价格 + 10%和价格-10%按钮 ([单击以查看实际尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image55.png))


> [!NOTE]
> 按钮、 Linkbutton 或添加到其 Templatefield ImageButtons 还可以具有的 GridView 和 DetailsView）。 如使用 BoundField 这些按钮，单击时，将引发一个回发，引发的 GridView s`RowCommand`事件。 当添加按钮 TemplateField，但是，按钮的`CommandArgument`不自动设置为的行的索引按原样使用 ButtonFields 时。 如果您需要确定在被单击的按钮的行索引`RowCommand`事件处理程序，你将需要手动设置按钮的`CommandArgument`TemplateField，使用类似的代码中其声明性语法中的属性：  
> `<asp:Button runat="server" ... CommandArgument='<%# CType(Container, GridViewRow).RowIndex %>' />`。


## <a name="summary"></a>总结

所有的 GridView、 DetailsView 和 FormView 控件可以包含按钮、 Linkbutton 或 ImageButtons。 此类按钮，单击时，会导致回发，并引发`ItemCommand`FormView 和 DetailsView 控件中的事件和`RowCommand`GridView 中的事件。 这些数据 Web 控件具有内置功能来处理常见的与命令相关的操作，如删除或编辑记录。 但是，我们可以还使用按钮，单击时，使用执行自己的自定义代码进行响应。

若要实现此目的，我们需要创建的事件处理程序`ItemCommand`或`RowCommand`事件。 此事件处理程序在我们首先检查传入`CommandName`值，以确定被单击的按钮，然后采取相应的自定义操作。 在本教程中我们已了解如何使用按钮和 ButtonFields 停止指定的供应商的所有产品，或以增加或减少 10%的某一特定产品的价格。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

> [!div class="step-by-step"]
> [上一篇](adding-and-responding-to-buttons-to-a-gridview-cs.md)
