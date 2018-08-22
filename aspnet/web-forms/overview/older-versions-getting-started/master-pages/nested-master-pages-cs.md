---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 嵌套母版页 (C#) |Microsoft Docs
author: rick-anderson
description: 演示如何嵌套在另一个主页面。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1b60b0b7ce4be66bc24ccbc1d25ce4dc56766815
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830466"
---
<a name="nested-master-pages-c"></a>嵌套的母版页 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip)或[下载 PDF](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 演示如何嵌套在另一个主页面。


## <a name="introduction"></a>介绍

在过去的过去的九个教程中，我们已了解如何实现具有主页面的网站的布局。 简单地说，母版页允许我们，页面开发人员，以及可以自定义基于内容的页面的内容页面的特定区域母版页中定义常见的标记。 ContentPlaceHolder 控件在母版页中的指示的可自定义的区域;内容控件通过内容页中定义的 ContentPlaceHolder 控件的自定义的标记。

我们为止已探索的母版页技术非常棒，如果您有一个在整个站点上使用的布局。 但是，许多大型网站在多个部分能够自定义的站点布局。 例如，考虑医院员工用于管理患者信息、 活动和计费的卫生保健应用程序。 可能有三种类型的此应用程序中的网页：

- 人员特定成员的页面，员工可以更新可用性，查看计划，或请求休假时间。
- 员工在其中查看或编辑特定位患者的信息特定于患者的页。
- 特定于计费的页会计师查看当前声明状态和财务报告。

每一页可能会共享一个通用布局，如跨顶部和底部的频繁使用链接的一系列菜单。 但是，人员、 患者和特定于计费的页可能需要自定义此通用的布局。 例如，可能是所有特定于员工的页面应包含一个日历和任务列表，显示当前登录的用户的可用性和每日计划。 可能需要显示名称、 地址和患者正在编辑其信息的保险信息所有特定于患者的页。

可以通过创建此类自定义的布局*嵌套的母版页*。 若要实现上述情况中，我们将首先创建使用 Contentplaceholder 定义可自定义区域定义整个站点布局、 菜单和页脚内容的母版页。 然后，将创建三个嵌套的母版页，一个用于每种类型的网页。 每个嵌套的母版页定义之间使用的母版页的内容页面的类型的内容。 换而言之，嵌套的母版页的特定于患者的内容页将包括标记和用于显示有关正在编辑患者信息的编程逻辑。 创建一个新的特定于患者的页面时我们会将其绑定到此嵌套的母版页。

本教程首先会突出显示嵌套的母版页的好处。 然后，它显示了如何创建和使用嵌套的母版页。

> [!NOTE]
> .NET Framework 2.0 版以来，已可以嵌套的母版页。 但是，Visual Studio 2005 不包括嵌套的母版页的设计时支持。 值得高兴的是，Visual Studio 2008 提供了丰富的设计时体验的嵌套的母版页。 如果使用嵌套的母版页感兴趣，但仍在使用 Visual Studio 2005，请查看[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[VS 2005 设计时在嵌套的母版页的技巧](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)。


## <a name="the-benefits-of-nested-master-pages"></a>嵌套的母版页的优点

很多网站有总体的站点设计，以及更多的自定义的设计特定于某些类型的页。 例如，在我们的演示 web 应用程序中我们创建了一个基本的管理部分 (中的页`~/Admin`文件夹)。 当前在 web 页面`~/Admin`文件夹为这些页面不在管理部分中使用相同的母版页 (即`Site.master`或`Alternate.master`，取决于用户的选择)。

> [!NOTE]
> 现在，假设我们的站点具有一个母版页`Site.master`。 我们将解决本教程后面使用嵌套的母版页与两个 （或多个） 正在启动与"使用嵌套 Master 页的管理部分"的主页面。


想象一下，我们需要自定义布局管理页，以包含其他信息或不应存在于站点中其他页面的链接。 有四个技术来实现此要求：

1. 手动将特定于管理的信息和链接添加到每个内容页面中`~/Admin`文件夹。
2. 更新`Site.master`母版页要包含的管理部分特定的信息和链接，然后将代码添加到母版页中以显示或隐藏这些部分基于有关是否访问管理页面之一。
3. 创建新的主页面专门针对管理部分中，复制从标记`Site.master`，添加管理特定于部分的信息和链接，并更新中的内容页`~/Admin`要使用此新的主文件夹页。
4. 创建绑定到一个嵌套的母版页`Site.master`并且具有内容的页面中`~/Admin`文件夹使用这个新嵌套母版页。 此嵌套的母版页将包括只需其他信息和特定于的管理页面的链接，而不需要重复已在中定义的标记`Site.master`。

第一个选项是至少愉快。 使用母版页的全部意义是将从无需手动复制并粘贴到新的 ASP.NET 页面的常见标记移开。 第二个选项是可以接受的但使应用程序不太易于维护，因为它使用标记，只是偶尔显示并且需要开发人员可以编辑母版页若要解决此标记并要记得时，主页面向上 bulks完全正确，某些标记时将显示与其处于隐藏状态。 此方法将不太 tenable 作为自定义项从越来越多类型的此使用单个母版页满足所需的网页。

第三个选项可以删除混乱和复杂性问题可与第二个选项。 但是，选项 3 的主要缺点是它需要我们进行复制和粘贴的常见布局从`Site.master`到新的管理部分特定于主页面。 如果我们稍后决定更改站点范围内布局我们必须记住要在两个位置更改它。

第四个选项中，嵌套的母版页，让我们获得的第二个和第三个选项。 特定于特定区域的内容分离到不同的文件时，站点范围内布局信息保留在一个文件中的顶层母版页的。

本教程首先介绍在创建和使用简单的嵌套的母版页。 我们创建全新的顶层母版页、 两个嵌套的主页面和两个内容页面。 从"使用嵌套 Master 页的管理部分"开始，我们介绍更新我们现有的主页面体系结构，以包括使用嵌套的母版页。 具体而言，我们创建嵌套的母版页并使用它来包括其他自定义内容中的内容页`~/Admin`文件夹。

## <a name="step-1-creating-a-simple-top-level-master-page"></a>步骤 1： 创建简单的顶层母版页

创建嵌套的母版基于其中一个现有的主页面，然后更新现有的内容页，以便使用此新的嵌套的母版页，而不是顶层母版页需要某种程度的复杂性，因为现有内容页面已需要某些ContentPlaceHolder 控件在顶层母版页中定义。 因此，嵌套的母版页还必须包括具有相同名称的相同 ContentPlaceHolder 控件。 此外，我们演示特定的应用程序可以有两个母版页 (`Site.master`和`Alternate.master`) 的动态分配到内容页基于用户的首选项，从而进一步将添加到这种复杂性。 我们将探讨更新现有应用程序中，若要在本教程后面使用嵌套的母版页，但让我们首先应当集中一个简单的嵌套主页面示例。

创建一个名为的新文件夹`NestedMasterPages`然后将新的主页面文件添加到该文件夹名为`Simple.master`。 （请参阅图 1 在解决方案资源管理器的屏幕截图后已添加此文件夹和文件。）拖动`AlternateStyles.css`从解决方案资源管理器中拖动到设计器的样式表文件。 这将添加`<link>`样式表文件中的元素`<head>`其后元素的母版页`<head>`元素的标记应如下所示：


[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

接下来，添加以下标记中的 Web 窗体`Simple.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

此标记中深蓝色背景上的大型白色字体的页面顶部显示标题为"嵌套母版页 （简单）"的链接。 下面的`MainContent`ContentPlaceHolder。 图 1 显示了`Simple.master`母版页时在 Visual Studio 设计器中加载。


[![嵌套的母版页定义特定于内容到管理部分中的页](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**图 01**: 嵌套 Master 页定义内容特定于管理部分中的页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image3.png))


## <a name="step-2-creating-a-simple-nested-master-page"></a>步骤 2： 创建简单的嵌套的母版页

`Simple.master` 包含两个 ContentPlaceHolder 控件：`MainContent`我们在与 Web 窗体中添加了的 ContentPlaceHolder `head` ContentPlaceHolder 中的`<head>`元素。 如果我们要创建内容页面并将其绑定到`Simple.master`内容页必须引用两个 Contentplaceholder 的两个内容控件。 同样，如果我们创建嵌套的母版页，并将其绑定到`Simple.master`则嵌套的母版页将具有两个内容控件。

让我们添加到新的嵌套母版页上`NestedMasterPages`文件夹名为`SimpleNested.master`。 右键单击`NestedMasterPages`文件夹，然后选择添加新项。 此时将显示在图 2 所示的添加新项对话框。 选择母版页模板类型和键入新的主页面的名称。 若要指示新的主页面应为嵌套的母版页，选中"选择母版页"复选框。

接下来，单击添加按钮。 这将显示相同的 Select 绑定到母版页的内容页面时，将显示一个母版页对话框 （参见图 3）。 选择`Simple.master`母版页中的`NestedMasterPages`文件夹并单击确定。

> [!NOTE]
> 如果您创建了在 ASP.NET 网站中使用 Web 应用程序项目模型而不网站项目模型则不会在图 2 中所示的添加新项对话框中的"选择母版页"复选框。 若要创建嵌套的母版页使用 Web 应用程序项目模型时必须选择嵌套的母版页模板 （而不是母版页模板中）。 选择嵌套的母版页模板并单击添加后, 相同选择图 3 所示的对话框将出现一个母版页。


[![检查&quot;选择母版页&quot;复选框，添加嵌套母版页](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**图 02**： 选中"选择母版页"复选框可添加嵌套的母版页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image6.png))


[![将嵌套的母版页绑定到 Simple.master 母版页](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**图 03**： 将绑定到嵌套母版页`Simple.master`母版页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image9.png))


嵌套的母版页的声明性标记，如下所示，包含两个引用顶层母版页的两个 ContentPlaceHolder 控件的内容控件。


[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

除`<%@ Master %>`指令，嵌套的母版页的初始声明性标记等同于最初生成绑定到同一个顶层母版页的内容页面时的标记。 像的内容页面`<%@ Page %>`指令，`<%@ Master %>`此处指令中包含了`MasterPageFile`指定嵌套的母版页的父级母版页的属性。 嵌套的母版页和绑定到同一个顶层母版页的内容页面的主要区别是嵌套的母版页可以包括 ContentPlaceHolder 控件。 嵌套的母版页的 ContentPlaceHolder 控件定义其中内容的页面可以自定义标记的区域。

更新此嵌套的母版页，使其显示文本"Hello，from SimpleNested ！" 对应于在内容控件中`MainContent`ContentPlaceHolder 控件。


[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

进行此添加后, 保存嵌套的母版页，然后添加到新的内容页`NestedMasterPages`名为的文件夹`Default.aspx`，并将其绑定到`SimpleNested.master`母版页。 添加此页面时可能会惊讶地发现它包含任何内容控件 （请参阅图 4） ！ 内容页只能访问其*父*主页面的 Contentplaceholder。 `SimpleNested.master` 不包含任何 ContentPlaceHolder 控件;因此，任何绑定到此母版页的内容页不能包含任何内容控件。


[![新的内容页面不包含任何内容控件](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**图 04**: 新内容页包含无内容控件 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image12.png))


我们需要做什么是更新嵌套的母版页 (`SimpleNested.master`) 若要包括 ContentPlaceHolder 控件。 建议您嵌套的母版页，以便将包含在由其父级母版页，从而使其子级母版页的页面或内容页后，可以使用任何顶级母版页的 ContentPlaceHolder 每个 ContentPlaceHolder ContentPlaceHolder控件。

更新`SimpleNested.master`母版页 ContentPlaceHolder 纳入其两个内容控件。 为 ContentPlaceHolder 控件作为其内容控件是指 ContentPlaceHolder 控件相同的名称。 也就是说，添加一个名为 ContentPlaceHolder 控件`MainContent`的内容控件中`SimpleNested.master`引用`MainContent`ContentPlaceHolder 中的`Simple.master`。 执行相同的操作中引用的内容控件`head`ContentPlaceHolder。

> [!NOTE]
> 尽管我建议命名中嵌套的母版页的 ContentPlaceHolder 控件在顶层母版页 Contentplaceholder 相同，则不需要此命名对称性。 您可以为 ContentPlaceHolder 控件嵌套母版页中任何喜欢的名称。 但是，我发现更容易记住 Contentplaceholder 相对应使用哪些区域页上，如果我的顶层母版页和嵌套的母版页使用相同的名称。


建立这些新增功能后你`SimpleNested.master`母版页的声明性标记应如下所示：


[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

删除`Default.aspx`内容的页我们刚刚创建并随后重新添加它，将其绑定到`SimpleNested.master`母版页。 这一次 Visual Studio 将添加两个内容控件添加到`Default.aspx`，现在引用 Contentplaceholder 中定义`SimpleNested.master`（请参阅图 6）。 添加文本"Hello，from Default.aspx ！" 在内容中，控制引用`MainContent`。

图 5 显示了所涉及的三个实体`Simple.master`， `SimpleNested.master`，和`Default.aspx`-和它们之间的相互。 如图所示，嵌套的母版页上为其父级的 ContentPlaceHolder 实施内容控件。 如果需要可供内容页访问这些区域，嵌套的母版页必须将其自身 Contentplaceholder 添加到内容控件。


[![顶层和嵌套的母版页规定内容页面的布局](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**图 05**： 顶层和嵌套的母版页规定内容页面的布局 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image15.png))


此行为说明了如何内容页或母版页是仅了解其父级母版页。 Visual Studio 设计器也可指示此行为。 图 6 显示的设计器`Default.aspx`。 同时，哪些区域是从内容页可编辑，部分不，清楚地显示了在设计器，它不会消除歧义不可编辑的区域是从嵌套的母版页和区域是从顶级的母版页。


[![内容页现在包含嵌套的母版页的 Contentplaceholder 内容控件](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**图 06**: 内容页现在包含内容控件的嵌套母版页的 Contentplaceholder ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image18.png))


## <a name="step-3-adding-a-second-simple-nested-master-page"></a>步骤 3： 添加第二个简单嵌套的母版页

当有多个嵌套的母版页时，嵌套的母版页的好处是更为明显。 为了说明这一优势，创建中的另一个嵌套的母版页`NestedMasterPages`文件夹; 将这个新嵌套母版页`SimpleNestedAlternate.master`并将其绑定到`Simple.master`母版页。 嵌套的母版页的两个内容控件中添加 ContentPlaceHolder 控件，像在步骤 2 中执行。 此外将添加文本"Hello，from SimpleNestedAlternate ！" 对应于顶层母版页的内容控件中`MainContent`ContentPlaceHolder。 以后进行这些更改新嵌套的母版页的声明性标记看起来应类似于下面：


[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

创建一个名为的内容页`Alternate.aspx`中`NestedMasterPages`文件夹并将其绑定到`SimpleNestedAlternate.master`嵌套的母版页。 添加文本"Hello，from 备用 ！" 对应于在内容控件中`MainContent`。 图 7 显示了`Alternate.aspx`查看通过 Visual Studio 设计器时。


[![Alternate.aspx 绑定到 SimpleNestedAlternate.master 母版页](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**图 07**:`Alternate.aspx`绑定到`SimpleNestedAlternate.master`母版页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image21.png))


比较图 7 到图 6 中的设计器中的设计器。 这两个内容页面共享同一顶层母版页中定义的布局 (`Simple.master`)，即"嵌套 Master Pages 教程 （简单）"标题。 尚未都具有不同内容在其父主页面-中定义的文本"Hello，from SimpleNested ！" 图 6 和"Hello，from SimpleNestedAlternate ！"中 在图 7。 当然，此处的这些差异是微不足道的但您可以扩展此示例，包括更有意义的差异。 例如，`SimpleNested.master`页可能包含具有特定于其内容页面的选项的菜单，而`SimpleNestedAlternate.master`可能具有绑定到它的内容页面相关的信息。

现在，假设我们需要对总体站点布局进行更改。 例如，假设我们想要将一组公共链接添加到所有内容页面。 若要完成此我们更新顶层母版页`Simple.master`。 存在的任何更改将立即反映在其嵌套的母版页，并通过扩展，其内容的页面。

若要演示的易用性与我们可以更改总体站点布局，打开`Simple.master`母版页并添加以下标记之间`topContent`并`mainContent``<div>`元素：


[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

这会向绑定到每个页的顶部添加两个链接`Simple.master`， `SimpleNested.master`，或`SimpleNestedAlternate.master`; 这些更改将立即应用于所有嵌套的母版页和其内容的页面。 图 8 显示了`Alternate.aspx`时的浏览器查看。 请注意添加的顶部 （图 7 相比） 的页的链接。


[![更改为顶级母版页会立即反映在其嵌套母版页和及其内容页面](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**图 08**： 更改为顶级母版页会立即反映在其嵌套母版页和及其内容页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image24.png))


## <a name="using-a-nested-master-page-for-the-administration-section"></a>对于管理部分中使用嵌套的母版页

此时我们已经探讨的嵌套的主优点的页面并已全面了解如何创建和 ASP.NET 应用程序中使用它们。 但是，步骤 1、 2 和 3 中的示例涉及到创建新的顶层母版页、 新嵌套的母版页和新的内容页。 如何添加新嵌套的母版页的网站与现有顶级母版页和内容页面？

将嵌套的母版页集成到现有的网站并将其关联到现有内容页面需要比从零开始的更多工作。 步骤 4、 5、 6 和 7 浏览这些挑战，因为我们提供了我们的演示应用程序，以包括新嵌套的母版页，名为`AdminNested.master`，其中包含有关管理员的说明，使用由 ASP.NET 页`~/Admin`文件夹。

将嵌套的母版页集成到我们的演示应用程序引入了以下障碍：

- 中的现有内容页面`~/Admin`文件夹有特定的预期从其主页面。 对于初学者而言，他们期望存在某些 ContentPlaceHolder 控件。 此外，`~/Admin/AddProduct.aspx`和`~/Admin/Products.aspx`页面调用主页面的公共`RefreshRecentProductsGrid`方法，并将其`GridMessageText`属性，或使用事件处理程序为其`PricesDoubled`事件。 因此，我们嵌套的母版页必须提供相同 Contentplaceholder 和公共成员。
- 在前面的教程中，我们将增强`BasePage`类来动态地设置`Page`对象的`MasterPageFile`属性基于会话变量。 我们如何为支持动态母版页使用嵌套的母版页时？

如我们生成嵌套的母版页并从现有内容页面中使用它将呈现这些两个挑战。 我们将调查并克服了这些问题出现。

## <a name="step-4-creating-the-nested-master-page"></a>步骤 4： 创建嵌套的母版页

我们的第一个任务是创建嵌套的母版页中以供管理部分中的页。 当添加新嵌套母版页中步骤 2 中，可以看到我们需要指定嵌套的母版页的父级母版页。 但我们有两个顶层的主页面：`Site.master`和`Alternate.master`。 回想一下，我们创建了`Alternate.master`在前面的教程和代码中编写过`BasePage`设置 Page 对象的类`MasterPageFile`属性在运行时为`Site.master`或`Alternate.master`具体取决于值`MyMasterPage`会话变量。

我们如何实现配置我们嵌套的母版页，使其使用适当的顶层母版页？ 我们有两个选项：

- 创建两个嵌套的母版页`AdminNestedSite.master`并`AdminNestedAlternate.master`，并将其绑定到顶级的母版页`Site.master`和`Alternate.master`分别。 在中`BasePage`，然后，我们将设置`Page`对象的`MasterPageFile`到适当的嵌套母版页。
- 创建单个嵌套的母版页和内容页使用此特定的母版页。 然后，在运行时，我们将需要设置嵌套的母版页的`MasterPageFile`属性设置为适当在运行时的顶层母版页。 (您可能已想到了目前为止，如主页面还有`MasterPageFile`属性。)

让我们使用第二个选项。 创建单个嵌套母版页文件中的`~/Admin`文件夹名为`AdminNested.master`。 因为这两`Site.master`并`Alternate.master`具有相同的 ContentPlaceHolder 控件集，并不重要主页面，将其绑定到，尽管我建议您将其绑定到`Site.master`一致性的起见。


[![向 ~/Admin 文件夹中添加嵌套的母版页。](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**图 09**： 添加到嵌套的母版页`~/Admin`文件夹。 ([单击此项可查看原尺寸图像](nested-master-pages-cs/_static/image27.png))


因为嵌套的母版页绑定到具有四个 ContentPlaceHolder 控件母版页，Visual Studio 添加了四个内容控件添加到新嵌套的母版页文件的初始标记。 我们在步骤 2 和 3，在每个内容控件中添加 ContentPlaceHolder 控件为其提供与顶级主页面的 ContentPlaceHolder 控件相同的名称。 此外将以下标记添加到内容控件对应于`MainContent`ContentPlaceHolder:


[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

接下来，定义`instructions`CSS 类中`Styles.css`和`AlternateStyles.css`CSS 文件。 下面的 CSS 规则会引发样式与 HTML 元素`instructions`类，以显示时带有浅黄色背景颜色，黑色的实线边框：


[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

此标记已添加到嵌套的母版页，因为它将仅出现在使用此嵌套的母版页 （即，在管理部分中的页） 的页面。

以后进行到嵌套母版页这些新增功能，其声明性标记看起来应类似于下面：


[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

请注意，每个内容控件有 ContentPlaceHolder 控件并且 ContentPlaceHolder 控件的`ID`属性分配与顶层母版页中的相应 ContentPlaceHolder 控件相同的值。 此外，管理特定于部分的标记出现在`MainContent`ContentPlaceHolder。

图 10 显示了`AdminNested.master`嵌套的母版页时通过 Visual Studio 设计器中查看。 可以看到在顶部的黄色框中的说明`MainContent`内容控件。


[![嵌套的母版页扩展顶层的主页面，以包括有关管理员的说明。](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**图 10**： 嵌套的母版页扩展顶层的主页面，以包括有关管理员的说明。 ([单击此项可查看原尺寸图像](nested-master-pages-cs/_static/image30.png))


## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>步骤 5： 更新现有的内容页面以使用新的嵌套的母版页

只要我们将新的内容页面添加到我们需要将其绑定到管理部分`AdminNested.master`我们刚刚创建的主页面。 但是，哪些有关现有内容页？ 目前，在站点中的所有内容页派生自`BasePage`类，该类以编程方式在运行时设置内容页面的母版页。 这不是我们想要在管理部分中的内容页面的行为。 相反，我们希望始终使用这些内容页面`AdminNested.master`页。 它将嵌套母版页中以选择在运行时的右顶级内容页的责任。

最佳的方式来实现这所需的行为是创建一个名为的新自定义基本页类`AdminBasePage`该项`BasePage`类。 `AdminBasePage` 然后，可以覆盖`SetMasterPageFile`并设置`Page`对象的`MasterPageFile`为硬编码值"~ / Admin/AdminNested.master"。 这样一来，任何页面的派生`AdminBasePage`将使用`AdminNested.master`，而从派生的任何页面`BasePage`将具有其`MasterPageFile`属性设置动态地为"~ / Site.master"或"~ / Alternate.master"值的基础`MyMasterPage`会话变量。

首先，通过添加到新的类文件`App_Code`文件夹名为`AdminBasePage.cs`。 具有`AdminBasePage`扩展`BasePage`，然后重写`SetMasterPageFile`方法。 在该方法将`MasterPageFile`值"~ / Admin/AdminNested.master"。 您的类进行这些更改后文件应该看起来类似于下面：


[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

我们现在需要在管理部分派生的现有的内容页面`AdminBasePage`而不是`BasePage`。 转到每个内容页面中的代码隐藏类文件`~/Admin`文件夹并进行此更改。 例如，在`~/Admin/Default.aspx`将更改从代码隐藏类声明：


[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

到:


[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

图 11 显示了如何顶层母版页 (`Site.master`或`Alternate.master`)，嵌套的母版页 (`AdminNested.master`)，并与另一个相关联的管理部分内容页面。


[![嵌套的母版页定义特定于内容到管理部分中的页](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**图 11**: 嵌套 Master 页定义内容特定于管理部分中的页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image33.png))


## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>步骤 6： 镜像母版页的公共方法和属性

请记住，`~/Admin/AddProduct.aspx`和`~/Admin/Products.aspx`页与母版页以编程方式进行交互：`~/Admin/AddProduct.aspx`调用母版页的公钥`RefreshRecentProductsGrid`方法并设置其`GridMessageText`属性;`~/Admin/Products.aspx`具有的事件处理程序`PricesDoubled`事件。 在前面的教程，我们创建一个抽象`BaseMasterPage`定义这些公共成员的类。

`~/Admin/AddProduct.aspx`并`~/Admin/Products.aspx`页面假定其母版页派生`BaseMasterPage`类。 `AdminNested.master`页上，但是，当前扩展`System.Web.UI.MasterPage`类。 因此，当来访`~/Admin/Products.aspx``InvalidCastException`引发并显示消息:"找不到类型的对象强制转换 ASP.admin\_adminnested\_主键入 BaseMasterPage。"

若要解决此我们需要能够`AdminNested.master`代码隐藏类扩展`BaseMasterPage`。 更新从嵌套的母版页的代码隐藏类声明：


[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

到:


[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

我们还未完成。 因为`BaseMasterPage`类是抽象的我们需要重写`abstract`成员`RefreshRecentProductsGrid`和`GridMessageText`。 顶层母版页使用这些成员来更新其用户界面。 (实际上，只有`Site.master`母版页使用这些方法，尽管这两个顶层的主页面实现的这些方法，因为同时扩展`BaseMasterPage`。)

而我们需要实现中的这些成员`AdminNested.master`，这些实现需要做的就是只需使用嵌套的母版页的顶层母版页中调用相同的成员。 例如，当管理部分中的内容页调用嵌套母版页上`RefreshRecentProductsGrid`方法，所有需要执行嵌套的母版页，反过来，则调用`Site.master`或`Alternate.master`的`RefreshRecentProductsGrid`方法。

若要实现此目的，首先添加以下`@MasterType`指令的页首`AdminNested.master`:


[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

请记住，`@MasterType`指令将强类型属性添加到代码隐藏类名为`Master`。 然后，重写`RefreshRecentProductsGrid`并`GridMessageText`成员和只需委托调用`Master`的相应方法：


[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

利用此代码，您应能够访问并使用管理部分中的内容页。 图 12 显示了`~/Admin/Products.aspx`页面的浏览器查看时。 正如您所看到的此页包含管理说明框中，嵌套的母版页中定义。


[![在管理部分中的内容页包括在每个页面顶部的说明](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**图 12**： 在每个页面顶部的管理部分包含说明中的内容页 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image36.png))


## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>步骤 7： 在运行时使用相应的顶层母版页

当在管理部分中的所有内容页面完全可用时，它们都使用相同的顶级母版页并忽略母版页在用户选择`ChooseMasterPage.aspx`。 此行为是因为，嵌套的母版页及其`MasterPageFile`属性以静态方式设置为`Site.master`在其`<%@ Master %>`指令。

若要使用由我们需要设置最终用户选择顶层母版页`AdminNested.master`的`MasterPageFile`属性中的值为`MyMasterPage`会话变量。 因为我们将设置内容页的`MasterPageFile`中的属性`BasePage`，您可能会认为我们会将嵌套的母版页的设置`MasterPageFile`中的属性`BaseMasterPage`中或在`AdminNested.master`的代码隐藏类。 这不会起作用，但是，因为我们需要设置`MasterPageFile`PreInit 阶段结束时通过属性。 我们可以以编程方式利用从母版页的页面生命周期的最早时间是 Init 阶段 （发生此情况的 PreInit 阶段）。

因此，我们需要设置嵌套的母版页的`MasterPageFile`从内容页的属性。 只有内容页面，使用`AdminNested.master`母版页派生`AdminBasePage`。 因此，我们可以那里放置此逻辑。 步骤 5 中我们重写`SetMasterPageFile`方法，设置`Page`对象的`MasterPageFile`属性设置为"~ / Admin/AdminNested.master"。 更新`SetMasterPageFile`还要设置母版页的`MasterPageFile`属性设置为结果存储在会话中：


[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

`GetMasterPageFileFromSession`方法，我们将添加到`BasePage`在前面的教程中，返回适当的母版页文件路径基于会话的变量值的类。

与此更改后，用户的主页面选择内容将被传递到管理部分。 图 13 显示了在同一页，图 12，但之后，用户已更改到其主页面选择`Alternate.master`。


[![嵌套的管理页使用用户选定的顶层母版页](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**图 13**： 嵌套管理页使用顶级 Master 页中选择用户 ([单击以查看实际尺寸的图像](nested-master-pages-cs/_static/image39.png))


## <a name="summary"></a>总结

多 like 如何在内容页面可以绑定到主页面，则可以创建嵌套的子级的母版页的母版页绑定到一个父级母版页。 子主页面可能为每个其父级的 Contentplaceholder; 定义内容控件它然后可以将其自身 ContentPlaceHolder 控件 （以及其他标记） 添加到这些内容控件。 嵌套的母版页是在其中所有页面都共享首要的外观和感觉，但站点的某些部分需要唯一自定义项的大型 web 应用程序中非常有用。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [嵌套的 ASP.NET 母版页](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [嵌套的母版页和 VS 2005 设计时的提示](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 嵌套 Master 页支持](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](specifying-the-master-page-programmatically-cs.md)
> [下一页](creating-a-site-wide-layout-using-master-pages-vb.md)
