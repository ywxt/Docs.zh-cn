---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: 使用 DataList 和 Repeater 控件 (VB) 显示数据 |Microsoft Docs
author: rick-anderson
description: 在前面的教程中我们使用了 GridView 控件以显示数据。 开始本教程中，我们看一下生成使用的常见报告模式...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ece899d4c9f3277fc27cdfc9c3f3e25ab7809fb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834157"
---
<a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>使用 DataList 和 Repeater 控件 (VB) 显示数据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用程序](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe)或[下载 PDF](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> 在前面的教程中我们使用了 GridView 控件以显示数据。 开始本教程中，我们介绍构建使用 DataList 和 Repeater 控件的常见报告模式从开始使用这些控件显示数据的基础知识。


## <a name="introduction"></a>介绍

在过去的所有示例中的所有 28 教程中，如果我们需要显示我们转向了 GridView 控件的数据源的多个记录。 GridView 呈现在列中显示的记录的数据字段的数据源中的每个记录的行。 虽然 GridView 可以显示、 分页、 排序、 编辑和删除数据的管理单元，其外观是有点 boxy。 此外，标记负责 GridView 的结构是固定包括对应的 HTML`<table>`与表行 (`<tr>`) 的每个记录和表格单元格 (`<td>`) 的每个字段。

若要提供更高的外观和呈现的标记中的自定义显示多个记录时，ASP.NET 2.0，提供了 DataList 和 Repeater 控件 (这两种也已推出 ASP.NET 版本 1.x)。 DataList 和 Repeater 控件呈现其内容使用模板而不是不是 BoundFields，CheckBoxFields，ButtonFields，等等。 如 GridView，DataList 呈现为 HTML `<table>`，但允许多个数据源记录要显示每个行。 Repeater，另一方面，呈现任何其他标记，而不仅仅什么显式指定，并在需要精确控制发出的标记时使用的理想候选项。

通过接下来几十教程中，我们将介绍在构建使用 DataList 和 Repeater 控件的常见报告模式开始显示与这些控件模板的数据的基础知识。 我们将了解如何设置这些控件的格式如何更改数据源中的记录 DataList、 常见的母版/详细信息方案、 方式编辑和删除数据，布局如何通过记录页上，依次类推。

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>步骤 1： 添加 DataList 和 Repeater 教程网页

在开始本教程之前，让我们来首先请花费片刻时间，将 ASP.NET 页面，我们需要为本教程，并显示使用 DataList 和 Repeater 的数据处理的下一步的几个教程。 首先，创建一个新的文件夹在项目中名为`DataListRepeaterBasics`。 接下来，将以下五个 ASP.NET 页添加到此文件夹中，无需让他们配置为使用母版页`Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`


![创建 DataListRepeaterBasics 文件夹并添加教程 ASP.NET 页面](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**图 1**： 创建`DataListRepeaterBasics`文件夹并添加教程 ASP.NET 页面


打开`Default.aspx`页上，并将其拖`SectionLevelTutorialListing.ascx`从用户控制`UserControls`文件夹拖到设计图面。 此用户控件，我们在中创建[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中，枚举站点图，并从项目符号列表中的当前部分显示这些教程。


[![将 SectionLevelTutorialListing.ascx 用户控件添加到 Default.aspx](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**图 2**： 添加`SectionLevelTutorialListing.ascx`到用户控件`Default.aspx`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))


为了使项目符号列表显示 DataList 和 Repeater 教程中我们将创建，我们需要将它们添加到的站点映射。 打开`Web.sitemap`文件，并添加自定义按钮站点映射节点标记后添加以下标记：


[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]


![更新包括新的 ASP.NET 页面的站点图](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**图 3**： 更新包括新的 ASP.NET 页面的站点图


## <a name="step-2-displaying-product-information-with-the-datalist"></a>步骤 2： 显示 DataList 产品信息

类似于 FormView，DataList 控件 s 呈现的输出取决于模板而不是 BoundFields、 CheckBoxFields，等等。 与 FormView 不同 DataList 旨在显示记录而不是一个孤立的一组。 让我们来开始学习本教程介绍将产品信息绑定到 DataList。 首先打开`Basics.aspx`页中`DataListRepeaterBasics`文件夹。 接下来，将从工具箱拖到设计器的 DataList。 如图 4 所示之前指定 DataList 的模板，, 在设计器会将其显示为灰色框。


[![从工具箱拖到设计器中拖动 DataList](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**图 4**： 拖动 DataList 从工具箱拖到设计器 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))


DataList s 从智能标记，添加新对象数据源并将其配置为使用`ProductsBLL`类的`GetProducts`方法。 由于我们在本教程中创建只读 DataList 重新设置为 （无） 下拉列表中的向导的插入，更新和删除选项卡。


[![选择创建新对象数据源](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**图 5**： 选择创建新对象数据源 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))


[![配置对象数据源以使用 ProductsBLL 类](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**图 6**： 配置为使用 ObjectDataSource`ProductsBLL`类 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))


[![检索有关所有使用 GetProducts 方法的产品信息](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**图 7**： 检索信息有关所有的产品使用`GetProducts`方法 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))


配置对象数据源并将其与 DataList 通过其智能标记关联之后, Visual Studio 自动创建`ItemTemplate`DataList 的显示名称和值的数据源返回每个数据字段中 (请参阅下面的标记）。 此默认`ItemTemplate`的外观等同于将数据源绑定到 FormView 通过设计器时自动创建的模板。


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> 回想一下，在将数据源绑定到 FormView 控件通过 FormView s 智能标记，Visual Studio 创建`ItemTemplate`， `InsertItemTemplate`，和`EditItemTemplate`。 使用 DataList，但是，仅`ItemTemplate`创建。 这是因为 DataList 不具有相同的内置编辑和插入 FormView 提供支持。 DataList 中确实包含编辑和删除相关的事件，且编辑和删除支持可以通过添加少量的代码，但有 s 简单开箱不支持任何作为 FormView。 我们将了解如何为包含编辑和在以后的教程中使用 DataList 删除支持。


允许 s 请花费片刻时间来提高此模板的外观。 而不是显示的所有数据字段，让我们来仅显示产品名称、 供应商、 类别、 每个计价单位和单价数量。 此外，let s 显示中的名称`<h4>`标题并使用剩余的字段布局`<table>`标题的下面。

若要进行这些更改可以是使用模板编辑 DataList s 智能标记单击编辑模板链接，或者可以修改模板页 s 声明性语法通过手动从设计器中的功能。 如果在设计器中使用编辑模板选项，您生成的标记可能不以下标记完全匹配，但通过查看时浏览器应看起来非常类似于屏幕截图中图 8 所示。


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> 上面的示例使用标签 Web 控制其`Text`属性分配数据绑定语法的值。 或者，可以省略了标签，只是数据绑定语法中键入。 也就是说，而不是使用`<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />`我们也可以改为使用声明性语法`<%# Eval("CategoryName") %>`。


在标签 Web 控件保留，但是，提供两个优势。 首先，它提供一种更容易的方法的格式设置数据，所基于的数据，正如我们将在下一教程中看到。 其次，设计器不会 t 显示声明性数据绑定语法中的编辑模板选项显示在某些 Web 控件之外。 相反，编辑模板接口旨在便于处理静态标记和 Web 控件，并假定任何数据绑定将通过编辑数据绑定对话框中，可从 Web 控件的智能标记进行访问。

因此，使用 DataList，可选择编辑通过设计器的模板时我更喜欢使用标签 Web 控件，以便可通过编辑模板接口访问的内容。 我们稍后将看到，Repeater 将需要从源视图进行编辑的模板的内容。 因此，如果我不知道我将需要设置的格式编写我通常会忽略标签 Web Repeater 的模板控制数据的外观绑定文本根据编程逻辑。


[![每个产品的输出是呈现使用 DataList 的 ItemTemplate](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**图 8**： 每个产品的输出是呈现使用 DataList s `ItemTemplate` ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))


## <a name="step-3-improving-the-appearance-of-the-datalist"></a>步骤 3： 改善 DataList 的外观

如 GridView，DataList 提供了多个与样式有关的属性，如`Font`， `ForeColor`， `BackColor`， `CssClass`， `ItemStyle`， `AlternatingItemStyle`， `SelectedItemStyle`，依次类推。 当使用 GridView 和 DetailsView 控件时，我们创建外观文件中的`DataWebControls`预定义的主题`CssClass`这两个控件的属性和`CssClass`及其子属性的多个属性 (`RowStyle``HeaderStyle`，依此类推)。 让我们来执行相同操作的 DataList。

如中所述[显示数据使用 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)教程中，将外观文件指定的默认 Web 控件与外观相关属性; 一个主题是定义的外观、 CSS、 图像和 JavaScript 文件的集合网站具有特定外观和风格。 中*显示数据使用 ObjectDataSource*教程中，我们创建`DataWebControls`主题 (这作为一个文件夹内`App_Themes`文件夹) 的有，目前，两个外观文件-`GridView.skin`和`DetailsView.skin`. 让我们来添加三个外观文件来指定 DataList 的预定义的样式设置。

若要添加将外观文件，请右键单击`App_Themes/DataWebControls`文件夹中，选择添加新项，并从列表中选择的外观文件选项。 为 `DataList.skin` 文件命名。


[![创建一个名为 DataList.skin 的新外观文件](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**图 9**： 创建新的外观文件命名`DataList.skin`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))


使用以下标记为`DataList.skin`文件：


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

这些设置将相同的 CSS 类分配给相应的 DataList 属性，如 GridView 和 DetailsView 控件采用了。 此处使用的 CSS 类`DataWebControlStyle`， `AlternatingRowStyle`， `RowStyle`，依次类推中定义`Styles.css`文件，并已添加在前面的教程。

通过此外观文件添加，DataList 的外观会更新在设计器中 （可能需要刷新设计器视图以查看影响新外观文件; 从视图菜单中，选择刷新）。 如图 10 所示，每个交替的产品具有浅粉色背景颜色。


[![创建一个名为 DataList.skin 的新外观文件](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**图 10**： 创建新的外观文件命名`DataList.skin`([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))


## <a name="step-4-exploring-the-datalist-s-other-templates"></a>步骤 4： 了解 DataList s 其他模板

除了`ItemTemplate`，DataList 支持六种其他可选模板：

- `HeaderTemplate` 如果提供，将标题行添加到输出，并用于呈现此行
- `AlternatingItemTemplate` 用于呈现交替项
- `SelectedItemTemplate` 用于呈现所选的项;所选的项是的项的索引对应于 DataList s [ `SelectedIndex`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)
- `EditItemTemplate` 用于呈现所编辑的项
- `SeparatorTemplate` 如果提供，将添加每个项之间的分隔符，并用于呈现此分隔符
- `FooterTemplate` -如果提供，将脚注行添加到输出，并用于呈现此行

指定时`HeaderTemplate`或`FooterTemplate`，DataList 将一个附加的页眉或页脚行添加到呈现的输出。 如 GridView 的页眉和页脚行、 页眉和页脚中 DataList 未绑定到数据。 因此，在任何数据绑定语法`HeaderTemplate`或`FooterTemplate`尝试访问绑定的数据将返回空字符串。

> [!NOTE]
> 中可以看到[GridView 的页脚中显示摘要信息](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)教程中，虽然页眉和页脚行不 t 支持数据绑定语法，特定于数据的信息可直接注入中的这些行GridView 的`RowDataBound`事件处理程序。 此方法可用于同时计算运行总计或来自数据的其他信息绑定到控件，以及将该信息分配给页脚。 此相同的概念可以应用于的 DataList 和 Repeater 控件;唯一的区别是 DataList 和 Repeater 创建的事件处理程序`ItemDataBound`事件 (而不是为`RowDataBound`事件)。


对于本示例中，let s 具有标题中的 DataList 的结果顶部显示的产品信息`<h3>`标题。 若要完成此操作，将添加`HeaderTemplate`包含相应的标记。 从设计器中，可以通过单击 DataList s 智能标记中的编辑模板链接，选择从下拉列表中，页眉模板并选取样式下拉列表中的标题 3 选项之后的文本中键入列表 （请参阅图 11）。


[![添加与文本产品信息 HeaderTemplate](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**图 11**： 添加`HeaderTemplate`与文本产品信息 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))


或者，可以在添加该声明的方式通过输入中的以下标记`<asp:DataList>`标记：


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

若要添加的每个产品列表之间的空间位，让我们来添加`SeparatorTemplate`包括每个部分之间的直线。 水平标尺标记 (`<hr>`)，将添加一个此类分隔线。 创建`SeparatorTemplate`以使其具有以下标记：


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> 像`HeaderTemplate`并`FooterTemplates`，则`SeparatorTemplate`未绑定到任何记录从数据源，因此不能直接访问的数据源绑定到 DataList 的记录。


进行此添加后, 查看通过浏览器页面时它应类似于图 12。 请注意标题行和每个产品列表之间的线。


[![DataList 包括标头行和每个产品列表之间的水平规则](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**图 12**: DataList 包括标头行和水平规则之间每个产品清单 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))


## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>步骤 5： 呈现 Repeater 控件使用的特定标记

如果访问图 12 中的 DataList 示例时，可以从你的浏览器执行视图/源代码，您将看到 DataList 发出对应的 HTML `<table>` ，其中包含一个表行 (`<tr>`) 与一个表格单元格 (`<td>`) 为每个项绑定到DataList。 此输出，事实上，等同于内容将被发送从单个 templatefield 进一步使用 GridView。 我们将在以后的教程中看到的 DataList 允许进一步自定义的输出中，使我们能够显示每个行的多个数据源记录。

如果您不想要发出对应的 HTML `<table>`，但？ 生成数据 Web 控件的标记的总计和完全控制，我们必须使用 Repeater 控件。 如 DataList 和 Repeater 是基于模板构造的。 Repeater，但是，仅提供以下五个模板：

- `HeaderTemplate` 如果提供，将添加在项的前面指定的标记
- `ItemTemplate` 用于呈现项
- `AlternatingItemTemplate` 如果提供，，用于呈现交替项
- `SeparatorTemplate` 如果提供，将添加每个项之间指定的标记
- `FooterTemplate` -如果提供，将指定的标记添加的项目之后

在 ASP.NET 1.x 中，Repeater 控件通常用于显示其数据来自某些数据源的项目符号列表。 在这种情况下，`HeaderTemplate`并`FooterTemplates`将包含在开始和结束`<ul>`标记，分别，而`ItemTemplate`将包含`<li>`具有数据绑定语法元素。 这种方法仍可在 ASP.NET 2.0 中的两个示例中可以看到[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程：

- 在`Site.master`主页面上，Repeater 用于显示顶层站点映射内容 （基本报告、 筛选报表、 自定义格式设置等） 的项目符号列表; 另一个嵌套的 Repeater 用于显示的子部分顶级部分
- 在`SectionLevelTutorialListing.ascx`，Repeater 用于显示当前站点映射部分的子部分的项目符号列表

> [!NOTE]
> ASP.NET 2.0 引入了新[BulletedList 控件](https://msdn.microsoft.com/library/ms228101.aspx)，这可以绑定到数据源控件以显示一个简单的项目符号列表。 我们不需要与 BulletedList 控件指定任何相关列表的 HTML 中;相反，我们只用于表示要显示为每个列表项的文本的数据字段。


Repeater 将所有数据 Web 控件都充当一个问题。 如果不是生成所需的标记的现有控件，可以使用 Repeater 控件。 为了说明使用 Repeater，让 s 已在步骤 2 中创建的产品信息 DataList 上方显示的类别的列表。 具体而言，let s 具有类别中的单行 HTML 显示`<table>`每个类别都显示为表中的列。

若要完成此操作，先从工具箱拖到设计器中，上述产品信息 DataList 拖动 Repeater 控件。 如同 DataList 和 Repeater 最初显示为灰色框定义它的模板之前。


[![添加到设计器的 Repeater](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**图 13**： 将 Repeater 添加到设计器 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))


在 Repeater s 智能标记那里 s 只提供一个选项： 选择数据源。 选择创建新对象数据源，并将其配置为使用`CategoriesBLL`类的`GetCategories`方法。


[![创建新对象数据源](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**图 14**： 创建新对象数据源 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))


[![配置对象数据源以使用 CategoriesBLL 类](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**图 15**： 配置为使用 ObjectDataSource`CategoriesBLL`类 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))


[![检索有关所有类别使用 GetCategories 方法的信息](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**图 16**： 检索信息有关所有类别使用的`GetCategories`方法 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))


DataList，与 Visual Studio 不自动创建 ItemTemplate 为 Repeater 后将其绑定到数据源。 此外，Repeater 的模板不能通过设计器配置，并且必须以声明方式指定。

若要为单个行中显示的类别`<table>`与每个类别列，我们需要 Repeater 发出标记如下所示：


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

由于`<td>Category X</td>`文本是重复发生，这会在 Repeater 的 ItemTemplate 中的部分。 将出现在它之前的标记`<table><tr>`-将被放入`HeaderTemplate`时的结束标记- `</tr></table>` -将放入`FooterTemplate`。 若要输入这些模板设置，请转到 ASP.NET 页面的声明性部分通过单击左下角中的源按钮并键入以下语法：


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

Repeater 发出指定的它的模板，没有其他任何，执行任何操作更少的精确标记。 图 17 显示了 Repeater 的输出时的浏览器查看。


[![只包含一行 HTML&lt;表&gt;在一个单独的列中列出了每个类别](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**图 17**: 只包含一行 HTML`<table>`列出了在一个单独的列中的每个类别 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))


## <a name="step-6-improving-the-appearance-of-the-repeater"></a>步骤 6： 改进中继器的外观

由于 Repeater 发出精确地指定它的模板的标记，它应提供果然不出所料没有为 Repeater 与样式有关的属性。 若要更改生成 Repeater 的内容的外观，我们必须手动添加到 Repeater 的模板直接的所需的 HTML 或 CSS 内容。

对于本示例中，让 s 具有备用背景颜色，如使用 DataList 中的交替行的类别列。 若要实现此目的，我们需要将分配`RowStyle`到 Repeater 中的每个项的 CSS 类和`AlternatingRowStyle`通过每个交替中继器项的 CSS 类`ItemTemplate`和`AlternatingItemTemplate`模板，如下所示：


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

允许 s 还将标头行添加到包含产品类别的文本的输出。 因为我们不知道多少列我们从而`<table>`将组成的生成保证跨所有列标题行的最简单方法是使用*两个* `<table>` s。 第一个`<table>`将包含两行的标头行和将包含第二个，只包含一行的行`<table>`的系统中有一列用于每个类别。 也就是说，我们想要发送以下标记：


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

以下`HeaderTemplate`和`FooterTemplate`产生所需的标记：


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

图 18 显示了 Repeater 后进行了这些更改。


[![类别列交替出现在背景色和包含一个标题行](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**图 18**: 类别列备用背景色，包括标题行中 ([单击以查看实际尺寸的图像](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))


## <a name="summary"></a>总结

虽然 GridView 控件，可以更容易地显示，编辑、 删除、 排序和分页浏览数据，外观是非常 boxy 和类似网格的。 对消息的外观的更多控制，我们需要打开到 DataList 或 Repeater 控件。 这两种控件显示一的组记录使用模板而不 BoundFields、 CheckBoxFields，等等。

DataList 呈现为 HTML `<table>` ，默认情况下，显示每个数据源记录中单个表行，就像使用单个 TemplateField GridView。 我们将在以后的教程中看到的但是，DataList 允许多个记录，以显示每个行。 Repeater，但是，严格地发出其模板; 中指定的标记它不会添加任何附加标记并因此通常用于在 HTML 元素而不显示数据`<table>`（如项目符号列表）。

虽然 DataList 和 Repeater 提供更灵活地呈现的输出，它们没有很多 GridView 中的内置功能。 因为我们将介绍在即将发布的教程中，其中一些功能可返回插入，而无需太多工作，但不要继续记住，使用 DataList 或 Repeater 代替 GridView 不会限制可使用而无需实现这些功能的功能您自己。

快乐编程 ！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Yaakov Ellis、 Liz Shulok、 Randy Schmidt 和 Stacy Park。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](nested-data-web-controls-cs.md)
> [下一页](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
