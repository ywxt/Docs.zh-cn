---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
title: 编辑和删除 DataList (VB) 中的数据的概述 |Microsoft Docs
author: rick-anderson
description: DataList 缺少内置编辑和删除功能，而在本教程中我们将了解如何创建支持编辑和删除 o DataList...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 9410a23c-9697-4f07-bd71-e62b0ceac655
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: b1c7834e67f7682f82ecd0b2b5140260d104aecc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834258"
---
<a name="an-overview-of-editing-and-deleting-data-in-the-datalist-vb"></a>编辑和删除 DataList (VB) 中的数据的概述
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_VB.exe)或[下载 PDF](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/datatutorial36vb1.pdf)

> DataList 缺少内置编辑和删除功能，而在本教程将介绍如何创建支持编辑和删除其基础数据的 DataList。


## <a name="introduction"></a>介绍

在中[概述的插入、 更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中我们介绍了如何插入、 更新和删除数据使用的应用程序体系结构、 ObjectDataSource 和 GridView、 DetailsView 和 FormView控件。 使用 ObjectDataSource 和以下三个数据 Web 控件，实现简单的数据修改接口是管理单元和涉及只勾选复选框从智能标记。 所需编写任何代码。

遗憾的是，DataList 缺少内置编辑和删除在 GridView 控件中的固有功能。 此缺少的功能是部分由于 DataList 是从以前版本的 ASP.NET，relic 时，声明性数据源控件和无代码数据修改的页都不可用。 虽然 DataList ASP.NET 2.0 中的不提供现成的相同数据修改功能作为 GridView，我们可以使用 ASP.NET 1.x 技术以包含此类功能。 这种方法需要一小段代码，但 DataList 到位，以帮助在此过程中我们将看到在本教程中，有一些事件和属性。

在本教程中我们将了解如何创建支持编辑和删除其基础数据的 DataList。 将来的教程将介绍更高级的编辑和删除方案 （包括输入的字段验证），适当地处理从数据访问或业务逻辑层等引发的异常。

> [!NOTE]
> 如 DataList 和 Repeater 控件缺少用于插入、 更新或删除功能的扩展。 虽然可以添加此类功能，但是 DataList 包括属性和事件中继器中找不到，简化添加此类功能。 因此，本教程，并看看编辑和删除的未来的重点严格 DataList。


## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>步骤 1： 创建编辑和删除教程网页

我们开始探索如何更新和删除 DataList 中的数据之前，让 s 先花点时间在我们的网站项目，我们需要为本教程下, 一步的几个源表创建的 ASP.NET 页面。 首先，通过添加一个名为的新文件夹`EditDeleteDataList`。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将与每个页面相关联`Site.master`母版页：

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![为了使教程添加 ASP.NET 页面](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image1.png)

**图 1**： 为了使教程添加 ASP.NET 页面


在其他文件夹中，喜欢`Default.aspx`在`EditDeleteDataList`文件夹在其部分中列出的教程。 请记住，`SectionLevelTutorialListing.ascx`用户控件提供了此功能。 因此，此用户控件添加到`Default.aspx`通过从解决方案资源管理器中拖到页面上的设计视图中拖动。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image2.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image4.png))


最后，将页面添加到条目为`Web.sitemap`文件。 具体而言，在母版/详细信息报表后添加以下标记，使用 DataList 和 Repeater `<siteMapNode>`:


[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample1.xml)]

更新后`Web.sitemap`，花点时间查看通过浏览器网站的教程。 现在，在左侧菜单的 DataList 编辑和删除教程包括项。


![站点图现在包括项的 DataList 编辑和删除教程](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image5.png)

**图 3**： 站点图现在包括项的 DataList 编辑和删除教程


## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>步骤 2： 正在检查技术中的更新和删除数据

编辑和删除使用 GridView 数据是非常简单，因为实际上，GridView 和 ObjectDataSource 协同工作。 如中所述[检查与插入、 更新和删除的事件相关联](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)教程中，单击行的更新按钮时，GridView 自动分配使用双向数据绑定到其字段`UpdateParameters`其对象数据源的集合，然后调用该 ObjectDataSource 的`Update()`方法。

遗憾的是，DataList 不提供任何此内置功能。 我们有责任确保用户 s 的赋值为 ObjectDataSource 的参数，并且其`Update()`调用方法。 为了实现我们这个目标，DataList 提供了以下属性和事件：

- **[ `DataKeyField`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)** 更新或删除时，我们需要能够唯一地标识 DataList 中的每个项。 将此属性设置为显示的数据的主键字段。 执行此操作将填充 DataList s [ `DataKeys`集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx)具有指定`DataKeyField`DataList 中的每个项的值。
- **[ `EditCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** 触发或按钮时，LinkButton、 ImageButton 其`CommandName`属性设置为单击编辑。
- **[ `CancelCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** 触发或按钮时，LinkButton、 ImageButton 其`CommandName`属性设置为在单击取消。
- **[ `UpdateCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** 触发或按钮时，LinkButton、 ImageButton 其`CommandName`属性设置为在单击更新。
- **[ `DeleteCommand`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** 触发或按钮时，LinkButton、 ImageButton 其`CommandName`属性设置为单击删除。

使用这些属性和事件，有四种方法可用于更新和删除 DataList 中的数据：

1. **使用 ASP.NET 1.x 技术**DataList ASP.NET 2.0 和 Objectdatasource 之前存在并已能够更新和删除数据完全通过编程方式。 此方法完全 ditches ObjectDataSource 和要求，我们将数据绑定到 DataList 直接从业务逻辑层，同时在检索数据时要显示和更新或删除一条记录时。
2. **用于选择、 更新和删除的页上的单个 ObjectDataSource 控件**DataList 缺少 GridView s 固有编辑和删除功能，而有 s 我们可以 t 没有理由将它们添加我们自己。 使用此方法时，我们使用 ObjectDataSource 就像在 GridView 示例中，但必须为 DataList s 创建事件处理程序`UpdateCommand`事件中： 我们在其中设置 ObjectDataSource 的参数和调用其`Update()`方法。
3. **使用 ObjectDataSource 控件进行选择，但更新和删除直接针对 BLL**使用选项 2 时，我们需要编写几行代码中`UpdateCommand`事件，将分配参数值，等等。 相反，我们可以坚持使用 ObjectDataSource 用于选择，但请直接对 BLL （例如，使用选项 1） 的更新和删除调用。 在我看来，更新直接与 BLL 交互的数据会导致更具可读性的代码比分配的 ObjectDataSource s`UpdateParameters`并调用其`Update()`方法。
4. **使用通过多个 Objectdatasource 的声明性方式**以前所有的三种方法需要一小段代码。 如果你 d 而继续使用作为尽可能多的声明性语法，最后一个选项是包含在页上的多个 Objectdatasource。 第一个对象数据源从 BLL 中检索数据，并将其绑定到 DataList。 进行更新，添加，但直接在 DataList s 中添加另一个 ObjectDataSource `EditItemTemplate`。 若要包含删除的支持，尚未另一个对象数据源，需要在`ItemTemplate`。 使用此方法时，这些嵌入使用 ObjectDataSource`ControlParameters`若要以声明方式将 ObjectDataSource 的参数绑定到用户输入控件 (而不是无需 DataList s 中以编程方式指定`UpdateCommand`事件处理程序)。 这种方法仍需要一小段代码需要调用嵌入的 ObjectDataSource s`Update()`或`Delete()`命令，但需要远小于使用其他的三种方法。 此处的缺点是，多个 Objectdatasource 做得很散乱页上，使整体可读性。

如果强制只使用其中一种方法，我选择选项 1，因为它提供了最大的灵活性，因为 DataList 最初设计用于满足这种模式。 DataList 已扩展，可以使用 ASP.NET 2.0 数据源控件，但它没有的所有可扩展性点或官方 ASP.NET 2.0 数据 Web 控件 （GridView、 DetailsView 和 FormView） 的功能。 选项 2 至 4 并非不值得，不过。

此软件和将来编辑和删除教程将使用 ObjectDataSource 用于检索数据来显示，并将对 BLL 更新和删除数据 （选项 3） 的调用。

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>步骤 3： 添加 DataList 并配置其对象数据源

在本教程中我们将创建 DataList，列出产品信息，并为每个产品，提供用户功能编辑名称和价格以及若要完全删除的产品。 具体而言，我们将检索的记录，以显示使用 ObjectDataSource，但执行更新和删除操作通过直接与 BLL 交互。 我们担心实现 DataList 的编辑和删除功能之前，让 s 首先获取页后，可以在只读的界面中显示的产品。 因为我们已将检查这些步骤在上一教程中，我将继续执行它们快速。

首先打开`Basics.aspx`页中`EditDeleteDataList`文件夹和设计视图中，从向页面添加 DataList。 接下来，从 DataList s 智能标记，创建新对象数据源。 由于我们正在与产品数据，将其配置为使用`ProductsBLL`类。 若要检索*所有*产品，选择`GetProducts()`选择选项卡中的方法。


[![配置对象数据源以使用 ProductsBLL 类](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image6.png)

**图 4**： 配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image8.png))


[![返回使用 GetProducts() 方法的产品信息](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image9.png)

**图 5**： 返回产品的信息使用`GetProducts()`方法 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image11.png))


DataList，如 GridView，不用于插入新数据;因此，请选择 (None) 选项从插入选项卡中的下拉列表。此外选择 （无） 为 UPDATE 和 DELETE 选项卡由于将通过 BLL 以编程方式执行更新和删除操作。


[![确认下拉列表中的 ObjectDataSource s 插入、 更新和删除选项卡设置为 （无）](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image12.png)

**图 6**： 确认 ObjectDataSource 的插入、 更新和删除选项卡中的下拉列表列出了已设置为 （无） ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image14.png))


在配置 ObjectDataSource 之后, 单击完成，返回到设计器。 正如我们已自动完成对象数据源配置，Visual Studio 时看到在过去示例中，创建`ItemTemplate`的下拉列表中，显示每个数据字段。 将此替换`ItemTemplate`与一个显示产品的名称和价格。 此外，还要设置`RepeatColumns`属性设置为 2。

> [!NOTE]
> 如中所述*概述的插入、 更新和删除数据*教程中，修改数据使用我们的体系结构要求，我们删除的 ObjectDataSource 时`OldValuesParameterFormatString`从 ObjectDataSource 的属性声明性标记 (或其重置为其默认值， `{0}`)。 在本教程中，但是，我们将使用 ObjectDataSource 仅用于检索数据。 因此，我们不需要修改 ObjectDataSource 的`OldValuesParameterFormatString`属性值 (尽管它不会损害，若要执行此操作)。


替换默认 DataList 后`ItemTemplate`用自定义页面上的声明性标记应如下所示：


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample2.aspx)]

花点时间查看我们通过浏览器的进度。 如图 7 所示，DataList 两列中显示每个产品的产品名称和单位价格。


[![在两个列 DataList 中显示的产品名称和价格](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image15.png)

**图 7**： 在两个列 DataList 显示产品名称和价格 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image17.png))


> [!NOTE]
> DataList 具有多个属性所需的更新和删除过程中，并且这些值存储在视图状态。 因此，如果构建 DataList 支持编辑或删除数据，很重要，启用 DataList 的视图状态。  
>   
>  敏锐的读者可能还记得我们能够创建可编辑的 Gridview、 DetailsViews 和 FormViews 时禁用视图状态。 这是因为 ASP.NET 2.0 Web 控件可以包括*控制状态*，这类似于视图状态，但认为重要的回发之间保留状态。


禁用视图状态 GridView 中的只是省略了简单的状态信息，但维护控件状态 （其中包括用于编辑和删除所需的状态）。 DataList，在 ASP.NET 1.x 的时间范围内，创建不使用控件状态，因此必须将启用视图状态。 请参阅[控件状态 vs。视图状态](https://msdn.microsoft.com/library/1whwt1k7.aspx)有关的控件状态，如果从视图状态的不同用途的详细信息。

## <a name="step-4-adding-an-editing-user-interface"></a>步骤 4： 添加用于编辑的用户界面

GridView 控件组成的字段 （BoundFields、 CheckBoxFields、 Templatefield，等） 的集合。 这些字段可以调整其呈现的标记，具体取决于其模式。 例如，如果处于只读模式，BoundField 其数据字段值显示为文本;在编辑模式下，它将呈现文本框 Web 控件`Text`属性分配数据字段值。

DataList，另一方面，呈现其使用模板的项。 使用呈现只读项`ItemTemplate`通过呈现在编辑模式下的项而`EditItemTemplate`。 此时，我们 DataList 仅具有`ItemTemplate`。 若要支持项目级编辑功能，我们需要添加`EditItemTemplate`，其中包含要为可编辑的项显示的标记。 对于本教程，我们将用于编辑产品的名称和单位价格来使用 TextBox Web 控件。

`EditItemTemplate`可以 （通过选择编辑模板选项从 DataList s 智能标记） 以声明方式或通过设计器创建。 要使用编辑模板选项，请首先单击智能标记中的编辑模板链接，然后选择`EditItemTemplate`从下拉列表中的项。


[![使用 DataList 的 EditItemTemplate，从而选择启用](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image18.png)

**图 8**： 选择以使用 DataList s `EditItemTemplate` ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image20.png))


接下来，键入产品名称中: 和价格:，然后将两个 TextBox 控件从工具箱到`EditItemTemplate`设计器上的接口。 设置文本框`ID`属性设置为`ProductName`和`UnitPrice`。


[![将 TextBox 添加的产品名称和价格](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image21.png)

**图 9**： 添加文本框中的产品名称和价格 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image23.png))


我们需要将绑定到的相应产品数据字段值`Text`两个文本框的属性。 从文本框智能标记中，单击编辑 DataBindings 链接，然后将关联的适当的数据字段`Text`属性，如图 10 中所示。

> [!NOTE]
> 绑定时`UnitPrice`数据字段为价格文本框 s`Text`字段中，您可能会将其格式化为货币值 (`{0:C}`)，常规数字 (`{0:N}`)，或将其保留为未格式化。


![将产品名称和单价数据字段绑定到文本框的 Text 属性](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image24.png)

**图 10**： 将绑定`ProductName`并`UnitPrice`数据字段到`Text`文本框的属性


请注意，图 10 中的编辑数据绑定对话框的工作原理*不*包括编辑 TemplateField GridView 或 DetailsView 或在 FormView 的模板时存在的双向数据绑定复选框。 允许使用双向数据绑定功能的值输入到输入的 Web 控件，若要自动分配到相应的 ObjectDataSource s`InsertParameters`或`UpdateParameters`插入或更新数据时。 DataList 不支持双向数据绑定，正如我们将有更高版本上，在本教程中，看到的建立她更改并已准备好更新的数据的用户后，我们将需要以编程方式访问这些文本框`Text`属性并传递到值适当`UpdateProduct`中的方法`ProductsBLL`类。

最后，我们需要添加更新和取消按钮`EditItemTemplate`。 中可以看到[母版/详细信息的详细信息 DataList 使用母版记录项目符号列表](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)教程中，或按钮时，LinkButton、 ImageButton 其`CommandName`属性设置中的 Repeater 或 DataList，单击从Repeater 或 DataList 的`ItemCommand`引发事件。 有关 DataList，如果`CommandName`属性设置为某个值，也可能会引发其他事件。 这两个特殊`CommandName`以及其他属性值包括：

- 取消引发`CancelCommand`事件
- 编辑引发`EditCommand`事件
- 更新引发`UpdateCommand`事件

请记住，会引发这些事件*除了*`ItemCommand`事件。

将添加到`EditItemTemplate`两个按钮 Web 控件、 一个其`CommandName`设置为更新和其他设置为取消。 以后将添加这两个按钮 Web 控件在设计器看起来应类似于下面：


[![添加更新和取消按钮 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image25.png)

**图 11**： 添加更新和取消按钮添加到`EditItemTemplate`([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image27.png))


使用`EditItemTemplate`完整 DataList s 声明性标记应如下所示：


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>步骤 5： 添加探测功能，可进入编辑模式

此时我们 DataList 具有用于编辑的界面，通过定义其`EditItemTemplate`; 但是，这里 s 目前没有办法为用户访问我们的页面指示他想要编辑产品的信息。 我们需要将编辑按钮添加到每个产品，单击时，呈现该 DataList 项处于编辑模式。 首先，通过添加到一个编辑按钮`ItemTemplate`，通过设计器或以声明方式。 设置编辑按钮的`CommandName`编辑的属性。

已添加此编辑按钮后，需要一段时间来查看通过浏览器页面。 添加此元素后，每个产品列表应包括一个编辑按钮。


[![添加更新和取消按钮 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image28.png)

**图 12**： 添加更新和取消按钮添加到`EditItemTemplate`([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image30.png))


单击按钮会导致回发，但*不*将置于编辑模式下所列出的产品。 若要使该产品可编辑，我们需要：

1. 设置 DataList s [ `EditItemIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)的索引的`DataListItem`只需单击其编辑按钮。
2. 重新绑定到 DataList 的数据。 DataList 时重新呈现`DataListItem`其`ItemIndex`对应于 DataList s`EditItemIndex`将使用呈现其`EditItemTemplate`。

由于 DataList s`EditCommand`单击编辑按钮时触发事件，创建`EditCommand`事件处理程序使用以下代码：


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample4.vb)]

`EditCommand`事件处理程序类型的对象中传递`DataListCommandEventArgs`作为其第二个输入参数，其中包括对引用`DataListItem`的编辑按钮被单击 (`e.Item`)。 事件处理程序首先设置 DataList s`EditItemIndex`到`ItemIndex`的可编辑`DataListItem`，然后将数据到 DataList 重新绑定通过调用 DataList 的`DataBind()`方法。

添加此事件处理程序后, 重新访问浏览器中的页。 单击编辑按钮现在可以被单击的产品可编辑 （请参阅图 13）。


[![单击可编辑产品建立的编辑按钮](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image31.png)

**图 13**： 单击编辑按钮使产品可编辑 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image33.png))


## <a name="step-6-saving-the-user-s-changes"></a>步骤 6： 保存用户的更改

单击编辑的产品 s 更新或取消按钮现在; 没有执行任何操作若要将此功能，我们需要为 DataList s 创建事件处理程序添加`UpdateCommand`和`CancelCommand`事件。 首先创建`CancelCommand`事件处理程序，单击编辑的产品 s 取消按钮和它执行任务的 DataList 回到其预先编辑状态时，将执行。

若要让 DataList 呈现的所有项在只读模式下，我们需要：

1. 设置 DataList s [ `EditItemIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)的索引不存在的`DataListItem`索引。 `-1` 是一个安全的选择，因为`DataListItem`索引开始`0`。
2. 重新绑定到 DataList 的数据。 由于无`DataListItem` `ItemIndex` es 对应于 DataList 的`EditItemIndex`，将在只读模式下呈现整个 DataList。

可以使用以下事件处理程序代码中完成以下步骤：


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample5.vb)]

添加此元素后，单击取消按钮返回 DataList 为其预编辑状态。

我们需要完成的最后一个事件处理程序是`UpdateCommand`事件处理程序。 此事件处理程序需要：

1. 以编程方式访问的用户输入产品名称和价格，以及编辑的产品的`ProductID`。
2. 启动更新过程，通过调用适当`UpdateProduct`重载中`ProductsBLL`类。
3. 设置 DataList s [ `EditItemIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)的索引不存在的`DataListItem`索引。 `-1` 是一个安全的选择，因为`DataListItem`索引开始`0`。
4. 重新绑定到 DataList 的数据。 由于无`DataListItem` `ItemIndex` es 对应于 DataList 的`EditItemIndex`，将在只读模式下呈现整个 DataList。

步骤 1 和 2 负责将用户保存 s 更改;步骤 3 和 4 DataList 后返回到其预先编辑状态更改已保存，并且在中执行的步骤相同`CancelCommand`事件处理程序。

若要获取的更新的产品名称和价格，我们需要使用`FindControl`方法以编程方式引用文本框 Web 控件内`EditItemTemplate`。 我们还需要获取已编辑的产品的`ProductID`值。 当我们最初绑定到 DataList ObjectDataSource 时，Visual Studio 分配 DataList s`DataKeyField`数据源的主键值的属性 (`ProductID`)。 然后可以从 DataList s 检索此值`DataKeys`集合。 请花费片刻时间来确保`DataKeyField`确实将属性设置为`ProductID`。

下面的代码实现的四个步骤：


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample6.vb)]

事件处理程序首先会在编辑产品 s 中读取`ProductID`从`DataKeys`集合。 下一步，在两个文本框`EditItemTemplate`引用和他们`Text`本地变量中存储属性`productNameValue`和`unitPriceValue`。 我们使用`Decimal.Parse()`方法来读取的值从`UnitPrice`文本框中，如果输入的值以便具有货币符号，仍可以正确地转换到`Decimal`值。

> [!NOTE]
> 中的值`ProductName`和`UnitPrice`文本框仅分配给 productNameValue 和 unitPriceValue 变量，如果文本框的文本属性具有指定的值。 否则为值为`Nothing`使用的变量，这与数据库中更新数据的影响`NULL`值。 也就是说，我们的代码将转换为空字符串转换为数据库`NULL`是 GridView、 DetailsView 和 FormView 控件中的编辑界面的默认行为的值。


在读取值之后,`ProductsBLL`类 s`UpdateProduct`方法调用时，传入 s 产品名称、 价格和`ProductID`。 事件处理程序完成通过为使用完全相同的逻辑中作为其预编辑状态返回 DataList`CancelCommand`事件处理程序。

与`EditCommand`， `CancelCommand`，和`UpdateCommand`事件处理程序完成，访问者可以编辑名称和产品价格。 图 14-16 显示运行中的此编辑工作流。


[![第一个访问的页面，所有的产品时处于只读模式](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image34.png)

**图 14**： 当首次访问的页面，所有产品都都在只读模式下 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image36.png))


[![若要更新的产品名称的价格，请单击编辑按钮](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image37.png)

**图 15**： 若要更新的产品名称或价格，请单击编辑按钮 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image39.png))


[![在更改值后，请单击更新返回到只读模式](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image40.png)

**图 16**： 后更改的值中，单击更新返回到只读模式 ([单击以查看实际尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image42.png))


## <a name="step-7-adding-delete-capabilities"></a>步骤 7： 添加删除功能

向 DataList 添加删除功能的步骤是类似于添加编辑功能。 简单地说，我们需要添加到删除按钮`ItemTemplate`，单击时：

1. 在相应产品 s 中读取`ProductID`通过`DataKeys`集合。
2. 通过调用执行 delete`ProductsBLL`类的`DeleteProduct`方法。
3. 重新绑定到 DataList 的数据。

让我们来通过添加到删除按钮来启动`ItemTemplate`。

当单击按钮时其`CommandName`为编辑，更新或取消按钮将引发 DataList s`ItemCommand`事件与其他事件 (例如，当使用编辑`EditCommand`事件也会产生)。 同样，任何按钮、 LinkButton 或 DataList 中的 ImageButton 其`CommandName`属性设置为删除的原因`DeleteCommand`激发的事件 (连同`ItemCommand`)。

添加中的编辑按钮旁边的删除按钮`ItemTemplate`，并设置其`CommandName`属性设置为删除。 添加后此按钮控制你 DataList 的`ItemTemplate`声明性语法应如下所示：


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample7.aspx)]

接下来，为 DataList s 创建事件处理程序`DeleteCommand`事件，使用以下代码：


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample8.vb)]

单击删除按钮会导致回发并触发 DataList 的`DeleteCommand`事件。 事件处理程序中，单击产品 s`ProductID`值访问从`DataKeys`集合。 接下来，通过调用删除产品`ProductsBLL`类的`DeleteProduct`方法。

在删除该产品之后, 它非常重要，我们重新绑定到 DataList 数据 (`DataList1.DataBind()`)，否则 DataList 将继续显示只删除该产品。

## <a name="summary"></a>总结

DataList 缺少点，并单击编辑和删除支持通过 GridView 体验感到满意，而使用短少量的代码可增强以包括这些功能。 在本教程中我们已了解如何创建的产品可以删除，无法编辑其名称和价格的两个列列表。 添加编辑和删除支持是一种包括中的相应 Web 控件`ItemTemplate`和`EditItemTemplate`、 创建相应的事件处理程序、 读取用户输入和主要密钥值，和如何与业务交互逻辑层。

虽然我们已添加基本编辑和删除 DataList 的功能，它缺乏更高级的功能。 例如，没有任何输入的字段验证-如果用户输入过的价格昂贵，异常将引发`Decimal.Parse`时尝试将转换过昂贵到`Decimal`。 同样，如果在更新数据的业务逻辑或数据访问层中的问题将提供用户在标准错误屏幕。 而无需任何类型的删除按钮确认消息，是所有很可能发生意外删除产品。

在将来教程将介绍如何提高编辑的用户体验。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Zack Jones、 Ken Pespisa 和 Randy Schmidt。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](customizing-the-datalist-s-editing-interface-cs.md)
> [下一页](performing-batch-updates-vb.md)
