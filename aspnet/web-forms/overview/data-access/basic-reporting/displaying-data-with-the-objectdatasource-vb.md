---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: 使用 ObjectDataSource (VB) 显示数据 |Microsoft Docs
author: rick-anderson
description: 本教程讨论 ObjectDataSource 控件使用此控件可以绑定 BLL 而无需 havi 在上一教程中创建从检索数据...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: f49cbf19b090917c170b025c269f825cf486c31a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832527"
---
<a name="displaying-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource (VB) 显示数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe)或[下载 PDF](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> 本教程讨论 ObjectDataSource 控件使用此控件可以绑定从 BLL 而无需编写一行代码创建上一教程中检索的数据 ！


## <a name="introduction"></a>介绍

我们应用程序体系结构和网站页的布局完成，我们准备开始探索如何完成各种常见数据和报告相关的任务。 在前面的教程，我们已了解如何以编程方式将数据从 DAL 和 BLL 绑定到数据 Web 控件在 ASP.NET 页中。 分配的数据 Web 控件的此语法`DataSource`属性设置为将数据显示，然后再调用控件的`DataBind()`方法已在 ASP.NET 1.x 应用程序中使用的模式，可以继续在 2.0 应用程序中使用。 但是，ASP.NET 2.0 的新数据源控件提供的声明性方式处理数据。 使用这些控件可以绑定从 BLL 而无需编写一行代码创建上一教程中检索的数据 ！

ASP.NET 2.0 附带有五个内置数据源控件[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)， [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)， [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)， [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)，并[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)尽管您可以构建你自己[自定义数据源控件](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)，如果需要。 由于我们开发了一种体系结构，我们的教程应用程序，我们将使用 ObjectDataSource 针对我们 BLL 类。


![ASP.NET 2.0 包括五个内置数据源控件](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**图 1**: ASP.NET 2.0 包括五个内置数据源控件


ObjectDataSource 用于处理与其他某些对象充当代理。 若要配置 ObjectDataSource 我们指定此基础对象和其方法如何映射到的 ObjectDataSource `Select`， `Insert`， `Update`，和`Delete`方法。 后指定了此基础对象，其方法映射到 ObjectDataSource 的我们然后可以将对象数据源绑定到数据 Web 控件。 ASP.NET 附带了很多数据 Web 控件，包括 GridView、 DetailsView、 RadioButtonList 和下拉列表中，等等。 在页生命周期中，Web 控件的数据可能需要访问的数据绑定，它将通过调用其 ObjectDataSource 完成`Select`方法; 如果数据 Web 控件支持插入、 更新或删除，调用可能会对其ObjectDataSource 的`Insert`， `Update`，或`Delete`方法。 这些调用被路由到适当的基础对象的方法的 ObjectDataSource 通过如以下关系图所示。


[![ObjectDataSource 充当代理](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**图 2**: ObjectDataSource 充当代理的 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image4.png))


尽管可以使用 ObjectDataSource 调用插入方法，更新或删除数据，让我们只需专注于返回的数据;将来的教程将探讨使用 ObjectDataSource 和数据修改的数据的 Web 控件。

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>步骤 1： 添加并配置 ObjectDataSource 控件

首先打开`SimpleDisplay.aspx`页中`BasicReporting`文件夹中，切换到设计视图中，并从工具箱拖到页面的设计图面将 ObjectDataSource 控件。 对象数据源将显示为灰色框，在设计图面上，因为它不会生成任何标记;它只需通过调用从指定的对象的方法访问数据。 返回对象数据源的数据可以显示数据 Web 控件，如 GridView、 DetailsView、 FormView 和等等。

> [!NOTE]
> 或者，你可能会先向页面添加数据 Web 控件，然后，从其智能标记上，选择&lt;新的数据源&gt;从下拉列表选项。


若要指定 ObjectDataSource 的基础对象和该对象的方法如何映射到 ObjectDataSource 的请单击 ObjectDataSource 的智能标记中的配置数据源链接。


[![单击配置从智能标记的数据源链接](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**图 3**： 单击智能标记中的配置数据源链接 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image7.png))


此时会打开配置数据源向导。 首先，我们必须指定要使用 ObjectDataSource 的对象。 如果选中"仅数据组件显示"复选框，在此屏幕上的下拉列表列出了这些对象`DataObject`属性。 目前我们的列表类型化数据集，我们在上一教程中创建的 BLL 类包括 Tableadapter。 如果你忘记添加`DataObject`属性的业务逻辑层类为您看不到他们在此列表中。 在这种情况下，取消选中"仅数据组件显示"复选框以查看所有对象，其中应包括 BLL 类 （和其他类中的类型化数据集 DataTables、 Datarow，依此类推）。

从第一个屏幕中选择`ProductsBLL`类从下拉列表，并单击下一步。


[![使用 ObjectDataSource 控件指定使用的对象](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**图 4**： 指定使用该对象具有 ObjectDataSource 控件 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image10.png))


在向导的下一个屏幕会提示您选择 ObjectDataSource 应调用什么方法。 下拉列表列出了从上一屏幕中选择的对象中返回数据的这些方法。 这里我们可以看到`GetProductByProductID`， `GetProducts`， `GetProductsByCategoryID`，和`GetProductsBySupplierID`。 选择`GetProducts`方法从该下拉列表并单击完成 (如果您添加`DataObjectMethodAttribute`到`ProductBLL`的方法，如前面的教程，此选项中所示将选择默认情况下)。


[![选择从选择选项卡，返回数据的方法](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**图 5**： 从选择选项卡中选择返回数据的方法 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image13.png))


## <a name="configure-the-objectdatasource-manually"></a>手动配置 ObjectDataSource

ObjectDataSource 的配置数据源向导提供了一种来指定它使用的对象并将关联的对象的哪些方法调用的快速方法。 但是，可以配置其属性，通过属性窗口或在声明性标记中直接通过对象数据源。 只需将设置`TypeName`属性设置为要使用的基础对象的类型和`SelectMethod`到检索数据时要调用的方法。


[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

即使您更喜欢可能存在，您需要手动配置对象数据源，因为该向导仅列出了开发人员创建类的配置数据源向导。 如果你想要将对象数据源绑定到.NET Framework 中的类如[成员资格类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)，以访问用户帐户信息，或[Directory 类](https://msdn.microsoft.com/library/system.io.directory.aspx)若要使用文件系统信息你将需要手动设置 ObjectDataSource 的属性。

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>步骤 2： 添加数据 Web 控件并将其绑定到对象数据源

ObjectDataSource 具有已添加到页并配置后，我们就可以将数据 Web 控件添加到要显示所返回的对象数据源的数据的页面`Select`方法。 可将任何数据 Web 控件绑定到对象数据源;让我们看看在 GridView、 DetailsView 和 FormView 中显示对象数据源的数据。

## <a name="binding-a-gridview-to-the-objectdatasource"></a>将 GridView 绑定到对象数据源

添加 GridView 控件从工具箱拖到`SimpleDisplay.aspx`的设计图面。 从 GridView 的智能标记上，选择我们在步骤 1 中添加的 ObjectDataSource 控件。 这会自动将每个属性返回的数据从 ObjectDataSource 的 GridView 中创建 BoundField`Select`方法 （即，由产品数据表中定义的属性）。


[![GridView 已添加到页面并将其绑定到对象数据源](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**图 6**: GridView 已添加到页上，然后绑定到对象数据源 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image16.png))


然后可以自定义、 重新排列，或单击智能标记中的编辑列选项删除 GridView 的 BoundFields。


[![管理 GridView 的 BoundFields 通过编辑列对话框](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**图 7**： 管理 GridView 的 BoundFields 通过编辑列对话框 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image19.png))


请花费片刻时间来修改 GridView 的 BoundFields，删除`ProductID`， `SupplierID`， `CategoryID`， `QuantityPerUnit`， `UnitsInStock`， `UnitsOnOrder`，和`ReorderLevel`BoundFields。 只需从左下角中的列表中选择 BoundField 并单击删除按钮 (红色的 X) 将其删除。 接下来，重新排列 BoundFields，以便`CategoryName`并`SupplierName`BoundFields 前加上`UnitPrice`BoundField 通过选择这些 BoundFields 并单击向上箭头。 设置`HeaderText`属性为剩余 BoundFields `Products`， `Category`， `Supplier`，和`Price`分别。 接下来，让`Price`BoundField 设置为货币格式设置 BoundField`HtmlEncode`属性设置为 False 并将其`DataFormatString`属性设置为`{0:c}`。 最后，水平对齐`Price`向右和`Discontinued`通过中心中的复选框`ItemStyle` / `HorizontalAlign`属性。


[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]


[![已自定义 GridView 的 BoundFields](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**图 8**： 的 GridView BoundFields 已自定义 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image22.png))


## <a name="using-themes-for-a-consistent-look"></a>使用一致的外观的主题

这些教程致力于删除任何控件级样式设置，而不使用级联样式表尽可能与外部文件中定义。 `Styles.css`文件包含`DataWebControlStyle`， `HeaderStyle`， `RowStyle`，和`AlternatingRowStyle`应该用于规定数据的外观的 CSS 类 Web 这些教程中使用的控件。 若要实现此目的，我们无法设置 GridView`CssClass`属性设置为`DataWebControlStyle`，并将其`HeaderStyle`， `RowStyle`，并`AlternatingRowStyle`属性的`CssClass`属性相应地。

如果将这些设置`CssClass`属性在 Web 控件需要记住来显式设置这些属性值为每个数据 Web 控件添加到我们的教程。 更易于管理的方法是为 GridView、 DetailsView，定义的默认 CSS 相关的属性和 FormView 控件使用的主题。 主题是一系列控制级别的属性设置、 图像和可应用于页面跨站点来强制执行常见的外观的 CSS 类。

我们的主题不包含任何图像或 CSS 文件 (我们将暂时使用样式表`Styles.css`为的，定义 web 应用程序的根文件夹中)，但将包括两个外观。 外观是定义 Web 控件的默认属性的文件。 具体而言，我们将使用 GridView 和 DetailsView 控件中，将外观文件默认值，该值指示`CssClass`-与相关的属性。

通过将新的外观文件添加到名为的项目启动`GridView.skin`通过右键单击解决方案资源管理器中的项目名称并选择添加新项。


[![添加名为 GridView.skin 的外观文件](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**图 9**： 添加外观文件命名为`GridView.skin`([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image25.png))


外观文件需要放在一个主题，其中位于`App_Themes`文件夹。 由于我们还没有这样的文件夹，将请先将其提供 Visual Studio 创建一个对我们添加我们的第一个外观时。 单击是以创建`App_Theme`文件夹和放置新`GridView.skin`文件存在。


[![让 Visual Studio 创建 App_Theme 文件夹](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**图 10**： 让 Visual Studio 创建`App_Theme`文件夹 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image28.png))


这将创建的新主题`App_Themes`外观文件中名为 GridView 文件夹`GridView.skin`。


![GridView 主题具有已添加到 App_Theme 文件夹](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**图 11**: GridView 主题都有已添加到`App_Theme`文件夹


将 GridView 主题重命名为 DataWebControls (右键单击 GridView 文件夹`App_Theme`文件夹，然后选择重命名)。 接下来，输入到以下标记`GridView.skin`文件：


[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

这将定义的默认属性`CssClass`-使用 DataWebControls 主题的所有页面中任何 GridView 的相关属性。 让我们添加另一个外观的 DetailsView，数据 Web 控件，我们将在稍后使用。 添加到名为 DataWebControls 主题的新外观`DetailsView.skin`并添加以下标记：


[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

使用我们定义的主题，最后一步是将主题应用到我们的 ASP.NET 页面。 可以将主题应用基于页的页或在网站中的所有页面。 让我们在网站中的所有页面中都使用此主题。 若要完成此操作，将添加到以下标记`Web.config`的`<system.web>`部分：


[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

这就是一切就这么简单 ！ `styleSheetTheme`主题中指定的属性应设置指示*不*重写在控件级别指定的属性。 若要指定主题设置应该也能带来控制设置，请使用`theme`属性来代替`styleSheetTheme`; 遗憾的是，在 Visual Studio 设计视图中未出现主题设置。 请参阅[ASP.NET 主题和外观概述](https://msdn.microsoft.com/library/ykzx33wh.aspx)并[服务器端样式使用主题](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)有关详细信息的主题和外观; 请参阅[How To： 应用 ASP.NET 主题](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx)有关的详细信息配置页后，可以使用主题。


[![GridView 显示产品的名称、 类别、 供应商、 价格和已停止使用的信息](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**图 12**: GridView 显示产品的名称、 类别、 供应商、 价格和停用信息 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image32.png))


## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>在 DetailsView 中一次显示一条记录

GridView 显示个返回的数据源控件绑定到每个记录都占一行。 有些的时候，但是，我们可能希望每次显示的唯一记录或只是一条记录。 [DetailsView 控件](https://msdn.microsoft.com/library/s3w1w7t4.aspx)提供此功能，以 HTML 形式呈现`<table>`包含两列和每个列或属性绑定到控件的一个行。 可以在 DetailsView 视为与单个记录的旋转 90 度 GridView。

首先，通过添加的 DetailsView 控件*上面*GridView 中的`SimpleDisplay.aspx`。 接下来，将其绑定到相同的 ObjectDataSource 控件为 GridView。 正如 gridview，BoundField 将添加到对象数据源返回的对象中每个属性 DetailsView`Select`方法。 唯一的区别是水平方向而不是垂直 DetailsView BoundFields 的布局方式。


[![添加到页面的 DetailsView 并将其绑定到对象数据源](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**图 13**： 添加到页面的 DetailsView 并将其绑定到对象数据源 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image35.png))


如 GridView、 DetailsView BoundFields，就可以调整以提供更多自定义的视图的对象数据源返回的数据。 图 14 显示后其 BoundFields DetailsView 和`CssClass`已配置属性，使其外观类似于 GridView 示例。


[![在 DetailsView 显示一条记录](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**图 14**: DetailsView 显示一条记录 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image38.png))


请注意，DetailsView 仅显示其数据源返回的第一个记录。 若要允许用户以单步执行的所有记录，一次一个地我们必须启用 DetailsView 的分页。 为此，请返回到 Visual Studio，并检查 DetailsView 的智能标记中的启用分页复选框。


[![在 DetailsView 控件中启用分页](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**图 15**： 在 DetailsView 控件中启用分页 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image41.png))


[![使用启用了分页，DetailsView 允许用户查看的任何产品](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**图 16**： 与已启用分页，DetailsView 允许用户查看的任何产品 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image44.png))


我们将详细介绍有关分页在将来的教程。

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>一次显示一条记录更灵活的布局

在 DetailsView 是非常严格中从对象数据源返回每个记录的显示方式。 我们可以更灵活的数据的视图。 例如，而不会在一个单独的行上显示产品的名称、 类别、 供应商、 价格和已停止使用的信息，我们可能想要显示产品名称和价格中`<h4>`标题，使其不显示的类别和供应商信息下面的名称和价格的较小的字体大小。 并且，我们可能不会介意以显示值旁边的属性名称 （产品、 类别和等等）。

[FormView 控件](https://msdn.microsoft.com/library/fyf1dk77.aspx)提供此级别的自定义项。 FormView 使用模板，允许混合使用 Web 控件，静态 HTML，而不是使用字段 （如 GridView 和 DetailsView 执行操作），并[数据绑定语法](http://www.15seconds.com/issue/040630.htm)。 如果您熟悉 Repeater 控件从 ASP.NET 1.x 中，您可以将 FormView 视为 Repeater 显示一条记录。

添加到 FormView 控件`SimpleDisplay.aspx`页面的设计图面。 最初 FormView 显示为灰色块，告知我们，我们需要提供，最小值，该控件的`ItemTemplate`。


[![FormView 必须包括 ItemTemplate](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**图 17**: 必须包括 FormView `ItemTemplate` ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image47.png))


可以对通过 FormView 的智能标记，将创建默认的数据源控件直接绑定 FormView`ItemTemplate`自动 (连同`EditItemTemplate`并`InsertItemTemplate`，如果 ObjectDatatSource 控件的`InsertMethod`和`UpdateMethod`属性设置)。 但是，对于此示例中让我们将数据绑定到 FormView，然后指定其`ItemTemplate`手动。 首先设置 FormView`DataSourceID`属性设置为`ID`的 ObjectDataSource 控件， `ObjectDataSource1`。 接下来，创建`ItemTemplate`，以便它显示产品的名称和价格`<h4>`元素以及类别和发运方名称下方的较小的字体大小。


[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]


[![第一个产品 (Chai) 显示在自定义格式](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**图 18**： 根据第一个产品 (Chai) 显示在自定义格式 ([单击以查看实际尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image50.png))


`<%# Eval(propertyName) %>`是数据绑定语法。 `Eval`方法将返回当前对象要绑定到 FormView 控件的指定属性的值。 请参阅 Alex Homer 文章[简体和扩展数据绑定语法在 ASP.NET 2.0](http://www.15seconds.com/issue/040630.htm)有关细节数据绑定的详细信息。

DetailsView，如 FormView 仅显示从 ObjectDataSource 返回的第一个记录。 您可以在中启用分页 FormView 以允许访问者，若要逐步执行产品一一次。

## <a name="summary"></a>总结

访问和显示业务逻辑层中的数据可以无需编写代码由于 ASP.NET 2.0 具有 ObjectDataSource 控件来实现。 ObjectDataSource 调用类的指定的方法并返回结果。 这些结果可以显示在数据绑定到对象数据源的 Web 控件。 在本教程中我们介绍了 GridView、 DetailsView 和 FormView 控件绑定到对象数据源。

到目前为止我们仅已了解如何使用 ObjectDataSource 调用无参数方法，但如果我们想要调用的方法需要输入参数，如`ProductBLL`类的`GetProductsByCategoryID(categoryID)`？ 若要调用的方法，要求一个或多个参数，我们必须配置对象数据源来指定这些参数的值。 我们将了解如何实现此目标我们[下一教程](declarative-parameters-vb.md)。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [创建你自己的数据源控件](https://msdn.microsoft.com/library/ms364049.aspx)
- [Asp.net 2.0 GridView 示例](https://msdn.microsoft.com/library/aa479339.aspx)
- [简化和扩展数据绑定 ASP.NET 2.0 中的语法](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0 中的主题](http://www.odetocode.com/Articles/423.aspx)
- [使用主题的服务器端的样式](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [如何： 以编程方式应用 ASP.NET 主题](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Hilton Giesenow。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [下一页](declarative-parameters-vb.md)
