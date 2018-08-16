---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
title: 创建使用母版页 (VB) 站点范围内布局 |Microsoft Docs
author: rick-anderson
description: 本教程会演示母版页基础知识。 也就是说，主页面，是什么如何一个创建主页面，什么是内容的占位符，如何执行一个 cr...
ms.author: aspnetcontent
ms.date: 05/21/2008
ms.assetid: 30945276-8ed9-4b27-8e50-4309244d3559
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 182f45c28dc37633b429fead333d401818299e36
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827817"
---
<a name="creating-a-site-wide-layout-using-master-pages-vb"></a>创建站点范围内布局使用母版页 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_VB.zip)或[下载 PDF](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_VB.pdf)

> 本教程会演示母版页基础知识。 也就是说，什么是主页面，其中一个会如何创建主页面，什么是内容的占位符，如何 does 之一创建的 ASP.NET 页使用母版页，如何修改母版页自动反映在其关联的内容页面，等等。


## <a name="introduction"></a>介绍

设计良好的一个属性是网站的一致的站点级页面布局。 以 www.asp.net 网站中，为例。 在撰写本文时，每个页都有相同的内容的顶部和页面的底部。 如图 1 所示，每个页面的顶部将显示包含一系列 Microsoft 社区的灰色栏。 下，它是站点徽标，其中该站点已翻译，语言和核心部分的列表： 主页、 入门、 学习、 下载和等。 同样，页面底部包括有关广告 www.asp.net、 版权声明和指向隐私声明的链接上的信息。


[![Www.asp.net 网站跨所有页面采用一致的外观](creating-a-site-wide-layout-using-master-pages-vb/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image1.png)

<strong>图 01</strong>: www.asp.net 网站采用一致的外观和感觉跨所有页面 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image3.png))


设计良好的另一个属性是站点的可用于更改站点的外观的易用性。 图 1 显示了自 2008 年 3 月起 www.asp.net 主页，但现在，本教程中的发布，可能已更改外观和感觉。 可能是沿着顶部的菜单项将展开以包括新的节的 MVC 框架。 也可能是揭秘是全新图案中带有不同的颜色、 字体和布局。 将此类更改应用于整个站点应快速而简单的过程不需要修改构成该站点的 web 页面的数千个。

在 ASP.NET 中创建的站点级页面模板是使用可能*母版页*。 简单地说，主页面是一种特殊的 ASP.NET 页，定义所有常见的标记*内容页*以及可自定义基于内容的页面的内容页面的区域。 （内容页面是 ASP.NET 页面绑定到主页面。）每当更改主页面的布局或格式化时，所有其内容页的输出是同样立即更新，这使得应用网站的外观更改为更新和部署单个文件 （即，母版页） 一样简单。

这是一系列教程，了解如何使用主页面中的第一个教程。 本系列教程的过程中我们：

- 检查创建主页面和其关联的内容页面
- 讨论各种提示、 技巧和陷阱，
- 识别母版页的常见问题和解决办法探索
- 请参阅如何从内容页和进行相反的转换访问主页面
- 了解如何指定在运行时，内容页面的母版页和
- 其他高级主页面主题。

这些教程旨在是简洁并提供引导你完成该过程以可视方式很大的屏幕截图的分步说明。 每个教程是在 C# 和 Visual Basic 版本中可用，包括使用的完整代码下载。

此开篇教程首先介绍在母版页基础知识。 我们讨论如何母版页的工作原理，将了解如何创建主页面和关联的内容页，使用 Visual Web Developer 中，并请参阅如何对母版页的更改将立即反映在其内容页面中。 让我们进入正题！

## <a name="understanding-how-master-pages-work"></a>了解如何母版页的工作原理

构建具有一致的站点级页面布局的网站，要求每个网页发出除了其自定义内容的常见格式设置标记。 例如， www.asp.net 上的每个教程或论坛帖子有自己唯一的内容，而每个这些页面还呈现了一系列常见`<div>`显示顶级部分链接的元素： 主页、 入门、 学习、 等等。

有各种用于创建具有一致的外观的网页的技术。 一个幼稚的做法是只需复制并粘贴到所有网页的常见布局标记，但这种方法有许多缺点。 对于初学者而言，每次创建一个新页面时，您必须记住复制并粘贴到页的共享的内容。 此类复制和粘贴操作是错误的时机已经成熟，因为你可能会意外地将共享标记的一个子集复制到新页。 从而为了彻底，这种方法使用新建一个真正的困难因为每个站点中的单个页面必须编辑才能使用新的外观和感觉替换现有的网站的外观。

在 ASP.NET 2.0 版中之前, 页开发人员通常放在常见标记[用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)并随后添加到每个页面的这些用户控件。 这种方法所需页面开发人员记住手动将用户控件添加到每个新页，但允许更轻松的站点范围内修改，因为更新的常见标记时仅由用户控件所需进行修改。 遗憾的是，Visual Studio.NET 2002年和 2003 的 Visual Studio 版本的用于创建 ASP.NET 1.x 应用程序的用户控件在设计视图中呈现为灰色的框。 因此，页面开发人员使用这种方法并没有享受所见即所得设计时环境。

使用用户控件的不足之处已解决在 ASP.NET 2.0 版和 Visual Studio 2005 中引入*母版页*。 主页面是一种特殊的 ASP.NET 页，定义这两个网站的标记和*区域*位置相关联*内容页*定义它们的自定义标记。 我们将在步骤 1 中看到的由 ContentPlaceHolder 控件定义这些区域。 ContentPlaceHolder 控件只是表示主页面的控件层次结构中的内容页面可以在其中注入自定义内容的位置。

> [!NOTE]
> ASP.NET 2.0 版以来未更改的核心概念和功能的主页面。 但是，Visual Studio 2008 提供设计时支持嵌套的母版页，缺少对 Visual Studio 2005 中的功能。 我们将介绍如何在以后的教程中使用嵌套的母版页。


图 2 显示了为 www.asp.net 母版页可能如下所示。 请注意，主页面以及中间的左侧，每个单独的 web 页面的独特内容所在的位置中 ContentPlaceHolder 定义常见网站的布局的顶部、 底部，和每个页面的右侧的标记的。


![母版页内容页面的内容页基于定义站点范围内布局和可编辑区域](creating-a-site-wide-layout-using-master-pages-vb/_static/image4.png)

**图 02**： 母版页上内容的页面的内容页来定义站点范围内布局和可编辑区域


定义一个母版页后它可以绑定到新的 ASP.NET 页面，通过一个复选框的刻度线。 这些 ASP.NET 页面-称为内容页面的每个母版页的 ContentPlaceHolder 控件包括内容控件。 通过浏览器访问内容页时 ASP.NET 引擎创建主页面的控件层次结构和内容页面的控件层次结构注入到相应的位置。 呈现此组合的控件层次结构和生成的 HTML 返回到最终用户的浏览器。 因此，内容页会发出其母版页之外 ContentPlaceHolder 控件中定义的常见标记和其自己的内容控件中定义的特定于页面的标记。 图 3 说明了这一概念。


[![请求的页面的标记融合到母版页](creating-a-site-wide-layout-using-master-pages-vb/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image5.png)

**图 03**: 请求的页面的标记融合到母版页 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image7.png))


现在，我们已讨论了如何母版页的工作原理，让我们看一看创建主页面和使用 Visual Web Developer 的关联内容页。

> [!NOTE]
> 若要访问尽可能多的受众，我们在整个教程系列中生成 ASP.NET 网站将创建与 Microsoft 的免费版本的 Visual Studio 2008 中，使用 ASP.NET 3.5 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)。 如果你尚未升级到 ASP.NET 3.5 中，别担心-在这些教程工作中讨论的概念同样有效的 ASP.NET 2.0 和 Visual Studio 2005。 但是，一些演示应用程序可以使用.NET framework 3.5; 版新增功能当使用特定于 3.5 的功能时，我会包含一条说明，介绍了如何在版本 2.0 中实现类似的功能。 执行操作请记住，可用于演示应用程序从每个教程的目标.NET Framework 3.5 版中，这会导致下载`Web.config`文件，其中包含特定于 3.5 的配置元素。 长话短说，如果你尚未然后可下载的 web 应用程序在计算机上安装.NET 3.5 未事先删除中的特定于 3.5 的标记将无法工作`Web.config`。 请参阅[仔细分析 ASP.NET 3.5 版的`Web.config`文件](http://www.4guysfromrolla.com/articles/121207-1.aspx)有关本主题的详细信息。


## <a name="step-1-creating-a-master-page"></a>步骤 1： 创建主页面

我们可以了解创建和使用母版页和内容页之前，我们首先需要将 ASP.NET 网站。 首先创建一个新文件系统基于 ASP.NET 网站。 若要完成此操作，启动 Visual Web Developer 中，然后转到文件菜单并选择新网站，显示新建网站对话框 （请参见图 4）。 选择 ASP.NET 网站模板、 将位置下拉列表设置为文件系统、 选择一个文件夹以将该 web 站点，并将语言设置为 Visual Basic。 这将创建与新的 web 站点`Default.aspx`ASP.NET 页面`App_Data`文件夹中，和一个`Web.config`文件。

> [!NOTE]
> Visual Studio 支持的项目管理的两种模式： 网站项目和 Web 应用程序项目。 网站项目缺少项目文件中，而 Web 应用程序项目模拟项目体系结构在 Visual Studio.NET 2002/2003年-它们包括项目文件并将项目的源代码编译到单个程序集，该值将被放`/bin`文件夹。 Visual Studio 2005 最初唯一受支持的 Web 站点项目，尽管 Web 应用程序项目模型已重新引入 Service Pack 1;Visual Studio 2008 提供了这两种项目模型。 Visual Web Developer 2005 和 2008年版本，但是，仅支持网站项目。 我使用我在本系列教程中演示的网站项目模型。 如果你使用的是非速成版，并想要使用[Web 应用程序项目模型](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)相反，随时执行此操作，但请注意您所见的屏幕，而不是必须执行的步骤之间可能存在某些差异屏幕截图所示，在这些教程中提供的说明。


[![创建新的文件基于系统的 Web 站点](creating-a-site-wide-layout-using-master-pages-vb/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image8.png)

**图 04**： 创建 New File System-Based 网站 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image10.png))


接下来，添加一个母版页到站点的根目录中右键单击项目名称，选择添加新项，然后选择母版页模板。 请注意母版页的扩展名结尾`.master`。 命名此新的主页面`Site.master`并单击添加。


[![添加母版页名为 Site.master 到网站](creating-a-site-wide-layout-using-master-pages-vb/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image11.png)

**图 05**： 添加主页面命名`Site.master`到网站 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image13.png))


添加 Visual Web Developer 中通过新的主页面文件使用以下声明性标记创建主页面：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample1.aspx)]

声明性标记中的第一行是[`@Master`指令](https://msdn.microsoft.com/library/ms228176.aspx)。 `@Master`指令是类似于[`@Page`指令](https://msdn.microsoft.com/library/ydy4x04a.aspx)的 ASP.NET 页中显示。 它定义的服务器端的语言 (VB) 和信息的位置和主页面的代码隐藏类继承。

`DOCTYPE`和下会显示在页面的声明性标记`@Master`指令。 此页包含四个服务器端控件以及静态 HTML:

- **Web 窗体 ( `<form runat="server">`)** -因为所有 ASP.NET 页面通常具有 Web 窗体的因为主页面可能包含必须出现在 Web 窗体的 Web 控件，所以一定要将 Web 窗体添加到主页面 （而不是将 Web 窗体添加到 e支票内容页）。
- **一个名为 ContentPlaceHolder 控件`ContentPlaceHolder1` ** -此 ContentPlaceHolder 控件将显示在 Web 窗体，并作为内容页面的用户界面的区域。
- **服务器端`<head>`元素**-`<head>`元素具有`runat="server"`属性，使其可通过服务器端代码访问。 `<head>`元素实现这种方式，以便页面的标题和其他`<head>`的相关标记可能添加或以编程方式调整。 例如，设置 ASP.NET 页的`Title`属性更改`<title>`元素呈现的`<head>`服务器控件。
- **一个名为 ContentPlaceHolder 控件`head` ** -此 ContentPlaceHolder 控件出现在`<head>`服务器控件，并可用于以声明方式将内容添加到`<head>`元素。

此默认母版页声明性标记作为一个起始点，在设计主页面。 随时编辑 HTML 或将其他 Web 控件或 Contentplaceholder 添加到母版页。

> [!NOTE]
> 当设计母版页请确保包含 Web 窗体母版页和至少一个 ContentPlaceHolder 控件将显示在该 Web 窗体。


### <a name="creating-a-simple-site-layout"></a>创建简单的站点布局

让我们展开`Site.master`的默认声明性标记来创建站点布局，其中所有页面都共享： 常见标头; 的导航、 新闻和其他站点范围的内容; 和页脚显示"提供支持的 Microsoft ASP.NET"图标左侧的列。 图 6 显示了母版页的最终结果时的浏览器查看其内容的页面之一。 图 6 中的红色圆圈的区域是特定于正在访问过的网页 (`Default.aspx`); 其他内容跨所有内容页面的母版页中定义和因此一致性。


[![母版页的顶部、 左侧和底部部分定义标记](creating-a-site-wide-layout-using-master-pages-vb/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image14.png)

**图 06**: 母版页的顶部、 左侧和底部部分定义标记 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image16.png))


若要实现站点布局图 6 所示，通过更新开始`Site.master`母版页，使其包含以下声明性标记：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample2.aspx)]

使用一系列定义主页面的布局`<div>`HTML 元素。 `topContent` `<div>`包含每个页上，顶部显示的标记时`mainContent`， `leftContent`，并`footerContent` `<div>` s 用于显示页面的内容、 左侧的列中，以及"提供支持的 MicrosoftASP.NET"图标，分别。 除了添加这些`<div>`元素，我还将重命名`ID`属性中的主 ContentPlaceHolder 控件`ContentPlaceHolder1`到`MainContent`。

这些已分类的格式设置和布局规则`<div>`元素中的拼写是否[级联样式表 (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets)文件`Styles.css`，这通过指定`<link>`元素在母版页中的`<head>`元素。 这些内容的各种规则定义的每个外观`<div>`上面记下的元素。 例如， `topContent` `<div>`元素，后者将显示"主页面教程"文本和链接，具有其格式设置规则中指定`Styles.css`，如下所示：

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample3.css)]

如果遵循在您的计算机，则需要下载此教程随附的代码并将添加`Styles.css`到你的项目文件。 同样，还将需要创建一个名为`Images`并将"提供支持的 Microsoft ASP.NET"图标从下载的演示网站复制到你的项目。

> [!NOTE]
> CSS 和网页格式的讨论已超出本文的讨论范围。 有关 CSS 的详细信息，请参阅[CSS 教程](http://www.w3schools.com/css/default.asp)处[W3Schools.com](http://www.w3schools.com/)。 我还建议您下载本教程随附的代码并试用可以使用中的 CSS 设置`Styles.css`若要查看不同的格式设置规则的效果。


### <a name="creating-a-master-page-using-an-existing-design-template"></a>创建使用现有的设计模板的主页面

多年来我构建了大量的小型到中型公司的 ASP.NET web 应用程序。 我的客户端的某些公司使用了他们想要使用; 某个现有站点布局其他人雇用功能完善的图形设计器。 几个委托我设计网站布局。 图 6 中可以看到，任务调度程序员设计网站的布局通常为明智的做法是为具有执行 open-heart surgery，而您的医生却你的税额你会计。

幸运的是，有 innumerous 提供免费的 HTML 设计模板的网站-Google 搜索词"免费网站模板。"返回六个 100 万个结果 我最喜欢的之一是[OpenDesigns.org](http://opendesigns.org/)。一旦找到您喜欢的网站模板，将 CSS 文件和图像添加到你的网站项目并将模板的 HTML 集成到主页面。

> [!NOTE]
> Microsoft 还提供了多种[免费 ASP.NET 设计启动工具包模板](https://msdn.microsoft.com/asp.net/aa336613.aspx)，将集成到 Visual Studio 中的新建网站对话框。


## <a name="step-2-creating-associated-content-pages"></a>步骤 2： 创建关联的内容页

与创建母版页，我们就可以开始创建绑定到母版页的 ASP.NET 页。 这些页面称为*内容页面*。

让我们向项目添加新的 ASP.NET 页面并将其绑定到`Site.master`母版页。 右键单击解决方案资源管理器中的项目名称并选择添加新项选项。 选择 Web 窗体模板中，输入名称`About.aspx`，然后选中"选择母版页"复选框，如图 7 中所示。 执行此操作将显示选择母版页对话框框中，您可以从中选择要使用的母版页的 （请参阅图 8）。

> [!NOTE]
> 如果您创建了在 ASP.NET 网站中使用 Web 应用程序项目模型而不网站项目模型则不会在图 7 中所示的添加新项对话框中的"选择母版页"复选框。 若要创建内容页面时使用的 Web 应用程序项目模型，必须选择而不是 Web 窗体模板的 Web 内容窗体模板。 选择 Web 内容窗体模板并单击添加后, 相同选择图 8 所示的对话框将出现一个母版页。


[![添加新的内容页面](creating-a-site-wide-layout-using-master-pages-vb/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image17.png)

**图 07**： 添加新的内容页 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image19.png))


[![选择 Site.master 母版页](creating-a-site-wide-layout-using-master-pages-vb/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image20.png)

**图 08**： 选择`Site.master`母版页 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image22.png))


如下面的声明性标记所示，新的内容页包含`@Page`指令，指回其主页面和内容控件的每个母版页的 ContentPlaceHolder 控件。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample4.aspx)]

> [!NOTE]
> 在步骤 1 中的"创建简单站点布局"部分我重命名`ContentPlaceHolder1`到`MainContent`。 如果没有重命名此 ContentPlaceHolder 控件`ID`中相同的方式，内容页面的声明性标记会略有不同，根据上面所示的标记。 也就是说，第二个内容控件的`ContentPlaceHolderID`将反映`ID`相应 ContentPlaceHolder 控件在母版页中。


当呈现内容页、 ASP.NET 引擎必须 fuse 页面的内容与其母版页 ContentPlaceHolder 控件的控件。 ASP.NET 引擎确定从内容页面的母版页`@Page`指令的`MasterPageFile`属性。 如上面的标记所示，此内容页面绑定到`~/Site.master`。

因为主页有两个 ContentPlaceHolder 控件-`head`和`MainContent`-Visual Web Developer 中生成两个内容控件。 每个内容控件引用通过特定 ContentPlaceHolder 其`ContentPlaceHolderID`属性。

其中一种站点范围模板技术通过母版页闪光是其设计时支持。 图 9 显示了`About.aspx`时通过 Visual Web Developer 设计视图中查看的内容页。 请注意，主页面内容可见时，它将灰显并且不能修改。 与母版页的 Contentplaceholder 相对应的内容控件，但是，一些可编辑。 就像使用任何其他 ASP.NET 页上，可以创建内容页面的接口通过添加 Web 控件通过源或设计视图。


[![内容页面的设计视图中显示这两个特定于页面的和主页面内容](creating-a-site-wide-layout-using-master-pages-vb/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image23.png)

**图 09**: 内容页面的设计视图显示的两个特定于页面的和主页面内容 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image25.png))


### <a name="adding-markup-and-web-controls-to-the-content-page"></a>将标记和 Web 控件添加到内容页

请花费片刻时间创建的某些内容`About.aspx`页。 如您所见图 10 中，我输入"有关作者"标题和几个段落的文本，但您太添加 Web 控件。 在创建后此接口，请访问`About.aspx`通过浏览器的页。


[![请访问 About.aspx 页通过浏览器](creating-a-site-wide-layout-using-master-pages-vb/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image26.png)

**图 10**： 请访问`About.aspx`通过浏览器页面 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image28.png))


请务必了解请求的内容页面和其关联的母版页是融合，作为一个整体的 web 服务器上完全呈现。 最终用户的浏览器然后发送生成、 浮点混合 HTML。 若要验证这一点，查看由浏览器转到视图菜单并选择数据源收到的 HTML。 请注意，有没有帧或用于单个窗口中显示两个不同的网页的其他任何专用的方法。

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>绑定到现有的 ASP.NET 页面的母版页

正如我们看到在此步骤中，将新的内容页面添加到 ASP.NET web 应用程序是只需选中"选择母版页"复选框并选择主页面。 遗憾的是，将现有的 ASP.NET 页面转换为母版页并不那么容易。

若要绑定到现有的 ASP.NET 页面的母版页需要执行以下步骤：

1. 添加`MasterPageFile`属性为 ASP.NET 页面的`@Page`指令，指向相应的主页面。
2. 为每个母版页中 Contentplaceholder 添加内容控件。
3. 有选择地剪切并粘贴到相应的内容控件的 ASP.NET 页面的现有内容。 我说"有选择地"在此处，ASP.NET 页面有可能因为包含标记表示已通过母版页，如`DOCTYPE`，则`<html>`元素和 Web 窗体。

屏幕快照以及此过程的分步说明，请查看[Scott Guthrie](https://weblogs.asp.net/scottgu/)的[使用母版页和站点导航](http://webproject.scottgu.com/VisualBasic/MasterPages/MasterPages.aspx)教程。 "更新`Default.aspx`和`DataSample.aspx`使用母版页"部分详细介绍这些步骤。

因为它是比要将现有 ASP.NET 页面转换成内容页面创建新的内容页面容易得多，我建议，每次创建新的 ASP.NET 网站添加母版页到站点。 将所有新的 ASP.NET 页面绑定到此母版页。 不必担心初始的主页面是非常简单的还是纯;您可以更高版本更新母版页。

> [!NOTE]
> 当创建新的 ASP.NET 应用程序，Visual Web Developer 将添加`Default.aspx`没有绑定到母版页的页面。 如果想要将现有的 ASP.NET 页面转换成内容页的做法，请继续并执行此操作与`Default.aspx`。 或者，可以删除`Default.aspx`并随后重新添加它，但这次，选中"选择母版页"复选框。


## <a name="step-3-updating-the-master-pages-markup"></a>步骤 3： 更新母版页的标记

主页面的主要优点之一是使用单个母版页，可用于在站点上定义的许多页面的整体布局。 因此，更新站点的外观和感觉需要更新单个文件的主页面。

为了演示此行为，让我们更新了主页，包括顶部的左侧列中的当前日期。 添加一个名为标签`DateDisplay`到`leftContent` `<div>`。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample5.aspx)]

接下来，创建`Page_Load`主事件处理程序页上，添加以下代码：

[!code-vb[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample6.vb)]

上面的代码中设置的标签`Text`属性设置为当前日期和时间格式为日期是星期几、 月和两位数日期的名称 （请参阅图 11）。 进行此更改后，重新访问您的内容页。 如图 11 所示，所得的标记是立即更新以包括对母版页的更改。


[![母版页的更改会反映时查看的内容页](creating-a-site-wide-layout-using-master-pages-vb/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image29.png)

**图 11**: 对母版页进行的更改反映时查看的内容页 ([单击以查看实际尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image31.png))


> [!NOTE]
> 如本示例所示，主页面可能包含服务器端 Web 控件、 代码和事件处理程序。


## <a name="summary"></a>总结

母版页使 ASP.NET 开发人员设计一致的网站的布局，可轻松地更新。 创建主页面和其关联的内容页面只需创建标准 ASP.NET 页，因为 Visual Web Developer 提供了丰富的设计时支持。

在本教程中创建的主页面示例有两个 ContentPlaceHolder 控件，头节点和主要内容。 我们仅 MainContent ContentPlaceHolder 控件标记中指定我们内容的页面，但是。 在下一教程中我们介绍如何使用多个内容控件中内容的页面。 我们还将了解如何定义默认内容标记控件的主页面，以及如何使用默认值之间进行切换标记中定义主页面并提供从内容页的自定义标记。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [面向设计人员的 ASP.NET： 使用 Web 标准构建 ASP.NET 网站上免费设计模板和指南](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 主机页面概述](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [级联样式表 (CSS) 教程](http://www.w3schools.com/css/default.asp)
- [动态设置页面的标题](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [在 ASP.NET 中的母版页](http://www.odetocode.com/articles/419.aspx)
- [母版页的快速入门教程](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](nested-master-pages-cs.md)
> [下一页](multiple-contentplaceholders-and-default-content-vb.md)
