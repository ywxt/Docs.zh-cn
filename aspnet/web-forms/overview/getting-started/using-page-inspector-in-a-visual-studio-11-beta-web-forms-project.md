---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Visual Studio 2012 中 ASP.NET Web 窗体使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: 适用于 Visual Studio 2012 的 Page Inspector 是一个 web 开发工具，使用集成浏览器。 集成的浏览器和 Page Inspector 中选择任何元素...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 1f1ac1072d33c85ed3e64c493b9cf7970695cea6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384470"
---
<a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>适用于 ASP.NET Web 窗体中的 Visual Studio 2012 中使用 Page Inspector
====================
由 Tim Ammann

> 适用于 Visual Studio 2012 的 Page Inspector 是一个 web 开发工具，使用集成浏览器。 在集成浏览器中选择任何元素和 Page Inspector 立即突出显示元素的源和 CSS。 可以在应用程序中浏览任何页面、 快速查找呈现的标记的源和使用 Visual Studio 环境中的浏览器工具。
> 
> 此教程 shwos 如何启用检查模式下，然后快速查找和编辑 CSS 规则和你的 web 项目中的文本。 本教程使用 Web 窗体应用程序项目中，但您也可以使用 Page Inspector 对于网站项目并[MVC](https://go.microsoft.com/?linkid=9802002)应用程序。
> 
> 本教程包含以下部分：
> 
> [先决条件](#_1_prerequisites)
> 
> [创建 Web 应用程序](#_2_creating_a)
> 
> [使用 Page Inspector 查看应用程序](#_3_using_page)
> 
> [启用检查模式](#_4_inspection_mode)
> 
> [使用 Page Inspector 对标记进行的更改](#_5_using_page)
> 
> [检查模式下和 HTML 窗口](#_6_inspection_mode)
> 
> [在样式窗口中预览 CSS 更改](#_7_previewing_css)
> 
> [CSS 自动同步](#css_auto_sync)
> 
> [使用 CSS 颜色选取器](#css_color_picker)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>系统必备

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。

> [!NOTE]
> 若要获取 Page Inspector 的最新版本，请使用[Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)要安装 Azure SDK for.NET 2.0。


Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。 最新版本是 1.3。 若要检查的版本，运行 Visual Studio 并选择**关于 Microsoft Visual Studio**从**帮助**菜单。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>创建 Web 应用程序

首先，将创建的 web 应用程序将使用与 Page Inspector。 在 Visual Studio 中，选择**文件** &gt; **新项目**。 在左侧，展开**Visual C#**，选择**Web**，然后选择**ASP.NET Web 窗体应用程序**。

![新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

单击 **“确定”**。

应用程序中打开**源**视图。

![在源视图中的新 Web 窗体应用程序](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

现在，已有要使用的应用程序，可以使用 Page Inspector 检查并对其进行修改。

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>使用 Page Inspector 查看应用程序

接下来，您将查看使用 Page Inspector 的应用程序。 在中**解决方案资源管理器**，右键单击该项目，然后选择**在 Page Inspector 中的查看**。

![在 Page Inspector 中的视图](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

默认情况下，Page Inspector 首次启动时它停靠在一个狭窄窗口作为 Visual Studio 环境的左侧。 将其停靠在左侧和右侧，并将其设置为宽度都能轻松地为你，或将它工具领域中的一个停靠在顶部、 底部或右侧：

![Page Inspector 停靠位置](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

如果您取消停靠该页面检查器窗口，您可以将其放置外部 Visual Studio 中，或即使在第二个监视器上如果有。 但是，按 ALT + TAB Page Inspector 和 Visual Studio 之间的顺序未停靠的页面检查器窗口时，请转到**工具** &gt; **选项** &gt; **环境** &gt; **选项卡和 Windows**，然后在**选项卡也**，则清除该复选框调用**浮动工具窗口始终掌握的主窗口**:

![清除 ALT + TAB Visual Studio 和停靠的页面检查器窗口之间的浮动工具 windows 复选框](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

页面检查器窗口的顶部窗格会显示在浏览器窗口中当前页。 底部窗格显示在左侧的 HTML 标记中的页，并允许您在右侧的某些选项卡检查页的不同方面。 在底部窗格是类似于[F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)Internet 资源管理器中。 （但是，与不同的开发人员工具，您可以使用 Page Inspector 直接在 Visual Studio。）

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

在本教程中，您将使用 Page Inspector 浏览器窗格中，并**HTML**并**样式**选项卡，有助于快速导航并对应用程序进行更改。

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>启用检查模式

接下来，你将看到 Page Inspector 的检查模式下的工作原理。 在页面检查器窗口中，单击**检查**按钮。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

若要查看操作中的检查模式下，将鼠标移动 Page Inspector 浏览器窗口中页面的不同部分。 执行操作时，鼠标指针更改为较大的加号，并突出显示下面的元素：

![悬停在 div.content 包装器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

移动鼠标指针时，请注意，

- 中的内容**源**查看发生变化，显示对应于页面上所选元素的标记。 突出显示相关的标记。 如果源是在另一个文件，该文件在源视图中打开与突出显示的相关标记。

- 在显示的标记**HTML**在 Page Inspector 中的选项卡也会更改以与页面上所选元素相对应。 在中**HTML**选项卡上，概述了相关的标记。

- **样式**选项卡显示与当前所选内容相关的 CSS 规则。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>使用 Page Inspector 对标记进行的更改

现在，将看到如何使用 Page Inspector 来查找和标记或其位置可能不是显而易见的文本进行更改。

Page Inspector 置于检查模式下，然后滚动到主页页面的底部。

一旦您输入的页脚区域，Page Inspector 将打开*Site.Master*中的布局文件**源**视图右侧的另一个临时选项卡中选项卡，并突出显示主节点的部分页上，您已选择。 此时会显示 Page Inspector 如何查找并可能实际上来自于不同的文件比最初打开的页面上显示的内容。

![在检查模式下的页脚重点推荐](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

在 Page Inspector 浏览器窗口中，将移动鼠标指针在行的版权<a id="a"></a>注意到。

在中*Site.Master*突出显示页面上，相应的行。

![页脚版权行突出显示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

将一些文本添加到中的行末尾*Site.Master*文件。

&lt;p&gt;&amp;复制;&lt;%: DateTime.Now.Year %&gt; -我的 ASP.NET 应用程序 Rocks ！&lt;/ p&gt;

现在，按 Ctrl + Alt + Enter 或单击更新条以查看 Page Inspector 浏览器窗口中的结果。

![我的 ASP.NET 应用程序 Rocks ！](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

您可能会想到上是页脚*Default.aspx*页上，但它原来在母版布局页中，并为你的 Page Inspector 找到它。

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>检查模式下和 HTML 窗口

接下来，您必须快速看一下 HTML 窗口以及它如何为您映射元素。

Page Inspector 置于检查模式。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

单击显示"your logo here"的页的上半部分。 正在检查中更多详细信息，因此您将鼠标指针移动无法再更改浏览器窗口中的显示的特定元素。

现在，转到鼠标指针**HTML**窗口。 移动鼠标指针时，Page Inspector 概述了中的元素**HTML**窗口，并突出显示浏览器窗口中的相应元素。

![HTML 窗口](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

如前面一样，Page Inspector 将打开*Site.Master*临时选项卡中为你的文件。单击 Site.Master 选项卡，并以突出显示相应的标记&lt;标头&gt;部分：

![突出显示的标记](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>在样式窗口中预览 CSS 更改

接下来，你将看到如何使用 Page Inspector**样式**窗口来预览对 CSS 的更改。

单击**检查**将 Page Inspector 置于检查模式下的按钮。

在 Page Inspector 浏览器窗口中，将鼠标指针移动到"主页"部分**div.content 包装**显示标签。

![悬停在元素上](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

单击后，div.content 包装器部分中，然后移动鼠标指针指向**样式**窗口。 下.featured.content 包装器类选择器中，清除并选择背景色属性旁的复选框。

![清除背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

请注意如何更改预览可立即在 Page Inspector 浏览器窗口。

再次选中的复选框，然后双击属性值并将其更改为`red`。 更改立即显示：

![红色背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

**样式**窗口进行，可以轻松地测试并预览 CSS 更改之前将更改提交到样式表本身。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自动同步

> [!NOTE]
> 此功能需要 Page Inspector 的 1.3 版。


CSS 自动同步功能，可直接编辑 CSS 文件并查看立即在 Page Inspector 浏览器中的更改。

单击**检查**将 Page Inspector 置于检查模式。

在 Page Inspector 浏览器中，将移动鼠标指针的"主页"部分直到**div.content 包装**显示标签。 单击一次以选择此元素。

**样式**窗口将显示所有此元素的 CSS 规则。 向下滚动到查找.featured.content 包装器类选择器。 单击"包装器.featured.content"。 Page Inspector 将打开定义此样式 (Site.css) 并突出显示相应的 CSS 样式的 CSS 文件。

![CSS 文件](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

现在，更改的值为`background-color`为"red"。 Page Inspector 浏览器中立即显示更改。

![Page Inspector 浏览器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>使用 CSS 颜色选取器

接下来，您将了解如何使用 Page Inspector 可以快速找到并更改默认应用程序中突出显示的文本的 CSS。 在此示例中，您已决定你不喜欢蓝色突出显示并想要将其更改为另一种颜色。

单击**检查**按钮。

![检查元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

在 Page Inspector 浏览器窗口中，将鼠标指针移动突出显示"视频、 教程和示例"，以便 CSS"标记"标签文本显示。

![悬停在标记元素](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

单击以选中它的文本。 相应的 CSS 标记选择器将显示在底部**样式**窗口。

![在样式窗口中的标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

单击标记选择器。 这将打开*Site.css* web 应用程序文件。 单击 Site.css 选项卡，并突出显示相应的 CSS 选择器：

![样式表中的标记选择器](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

选择并删除在行的背景色属性。

现在将使用新的 Visual Studio 2012 CSS 颜色选取器选择的新颜色**标记**背景颜色属性。

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>使用 Visual Studio 2012 CSS 颜色选取器

在 Visual Studio 2012 CSS 编辑器具有颜色选取器，轻松地选择和插入颜色。 它具有一个简单的颜色条和的"pop 停机"选取器，可提供更精细的控制。

颜色选取器包括一个标准颜色的调色板，支持标准颜色名称、 哈希代码、 RGB、 RGBA、 HSL 和 HSLA 颜色和维护已在文档中最近使用的颜色的列表。

上的背景色属性所在的行中，键入"bc"并一次按向下箭头。

连字符分隔的属性，如"背景色"中键入每个单词的第一个字符时，IntelliSense 将筛选要显示匹配的属性列表：

![Intellisense 筛选值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

现在，键入一个冒号。 执行操作时，将插入完整的背景色属性名称。 类型**#** 或**rgb (**，并显示颜色选取器条：

![CSS 颜色选取器栏](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

若要查看颜色选取器栏的工作原理，请单击它将鼠标指针的颜色或按向下箭头键，然后使用左侧和右侧的箭头键遍历颜色。 当您访问一种颜色时，预览的背景色属性的相应值：

![预览的背景色属性值](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

此时，可以按 enter 键以选择值，然后完成 CSS 输入分号 （;）。 现在，转到下一节，以便可以查看颜色选取器 pop 列表的工作原理。

#### <a name="using-the-color-picker-pop-down"></a>使用颜色选取器 Pop 列表

当在颜色栏不具有所需的确切颜色时，可以使用颜色选取器 pop 列表。

若要打开它，请单击颜色栏右侧的双 v 形图标或按键盘上一次或两次的向下箭头。

![CSS 颜色选取器 Pop 列表](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

单击从右侧的垂直条的颜色。 这将在主窗口中显示该颜色渐变。 通过按 Enter，直接从垂直条中选择一种颜色，或单击以选择具有更高的精度在主窗口中的任意点。

你想要使用的计算机屏幕上是否存在一种颜色 （不一定要在 Visual Studio 用户界面内），你可以通过使用取色器工具右下角中捕获它的值。

此外可以通过移动颜色选取器底部的滑块来更改一种颜色的不透明度。 这样做的更改颜色为 RGBA 值的值，因为 RGBA 格式可以表示不透明度。

选择一种颜色后，按 Enter，，然后键入分号完成中的背景色条目*Site.css*文件。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>页面检查器更新条

Page Inspector 立即检测到更改*Site.css*文件 （或应用程序中的任何文件），并显示更新条中的警报。

![更新条](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter 或单击更新条。 中的突出显示颜色更改显示在浏览器中：

![突出显示颜色更改](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>请注意，您可以方便地刷新 Page Inspector 浏览器直接从 Visual Studio 环境中。 而不外部浏览器中使用 Page Inspector 允许您在开发 web 应用程序时不会在编辑器中。

## <a name="see-also"></a>请参阅

[引入了 Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) （第 9 频道视频）

[Page Inspector 错误信息](https://go.microsoft.com/?linkid=9813062)(MSDN)
