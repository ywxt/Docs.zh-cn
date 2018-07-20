---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: 什么是 ASP.NET 和 Visual Studio 2012 中的 Web 开发中的新增功能 |Microsoft Docs
author: rick-anderson
description: Visual Studio 的新版本引入了一些增强功能专注于改善体验和性能，使用 Web 技术时...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 474df5c8e2cee820a3bdd80ba45e6504a025cdf1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823603"
---
<a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>什么是 ASP.NET 和 Visual Studio 2012 中的 Web 开发中的新增功能
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

> Visual Studio 的新版本引入了一些侧重于使用 Web 技术时提高的体验和性能的增强功能。 CSS、 JavaScript 和 HTML 的 visual Studio 编辑器已彻底改观，以包括许多最需代码辅助工具，例如智能感知和自动缩进。 至于性能方面，如内置功能，可轻松地将减少页面加载时间，则现在已集成捆绑和缩小。
> 
> Visual Studio，可使用最新的网站技术。 跨浏览器 CSS3 代码段可用于确保网站同时还充分利用新的 HTML5 元素和功能正常工作而不考虑客户端平台。
> 
> 应与此 Visual Studio 版本更容易编写和分析 JavaScript 代码。 智能感知列表集成的 XML 文档和导航功能现已推出的 JavaScript 代码。 您现在可以从您能够轻松利用 JavaScript 目录。 此外，可以检查 ECMAScript5 合规性与您的脚本，并在早期阶段检测语法错误。
> 
> 最后但同样重要的是，此 Visual Studio 版本可实现内置绑定和缩减。 您的脚本文件和样式表将打包和压缩，以便站点执行速度更快。
> 
> 此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)。


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验，你将了解如何：

- 在 CSS 编辑器中使用的新功能和改进
- 在 HTML 编辑器中使用的新功能和改进
- 在 JavaScript 编辑器中使用的新功能和改进
- 配置和使用绑定和缩减

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) （适用于安装程序脚本-已安装在 Windows 8 和 Windows Server 2008 R2）
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) -或符合 HTML5 的浏览器

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [练习 1： 什么是 CSS 编辑器中的新增功能](#Exercise1)
2. [练习 2： 什么是新的 HTML 编辑器](#Exercise2)
3. [练习 3： 什么是 JavaScript 编辑器中的新增功能](#Exercise3)
4. [练习 4： 捆绑和缩小](#Exercise4)

估计的时间才能完成此实验： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>练习 1： 什么是 CSS 编辑器中的新增功能

Web 开发人员应熟悉许多与 CSS 编辑相关的困难。 CSS 样式的最大问题之一是跨浏览器兼容性。 经常会发生，将样式应用于你的站点之后, 您注意到它看起来不同如果打开另一个浏览器或设备中。 因此，您可能修复意识到，最后进行了它在一个浏览器中工作时它是在中无效，其他这些 visual 问题上花费相当长的时间。

Visual Studio 现在包含功能，可帮助开发人员访问、 工作和有效地组织 CSS 样式表。 在本练习中，将满足的新功能，以有效的组织和版本，以及跨浏览器兼容性 CSS3 代码片段。

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>任务 1-新的编辑器功能

在此任务中，您将发现的新功能的 CSS 编辑器中。 这一新编辑器将帮助你提高工作效率，通过利用新的智能缩进、 改进的代码注释和增强的 IntelliSense 列表。

1. 启动**Visual Studio** ，然后打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**本实验的文件夹。
2. 在解决方案资源管理器中打开**Site.css**下的文件**样式**文件夹。 请确保**文本编辑器**工具是在工具栏上可见。 为此，请选择**视图** | **工具栏**菜单选项，并检查**文本编辑器**选项。 您将会发现，由于此新版本**注释**按钮 (![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) 和**取消注释**按钮 (![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)) 也已启用了 CSS 编辑器。

    ![启用编辑器和 CSS 工具](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "启用编辑器和 CSS 工具")

    *启用编辑器和 CSS 工具*
3. 滚动代码并选择任何 CSS 类定义。 单击**注释**(![注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) 按钮以添加所选的行的注释。 然后，单击**取消注释**(![取消注释按钮](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) 按钮以撤消所做的更改。
4. 单击**折叠**(![折叠](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) 和**展开**(![展开](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) 按钮位于文本的左边距。 请注意，您现在可以隐藏不使用具有更清晰的视图的样式。

    ![折叠的 CSS 类](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "折叠 CSS 类")

    *折叠的 CSS 类*
5. 确保已启用智能缩进功能。 选择**工具** | **选项**菜单选项，然后选择**文本编辑器** | **CSS**  | **格式设置**屏幕的左窗格中的页面。 检查**分层缩进**选项。

    ![启用分层缩进](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "启用分层缩进")

    *启用分层缩进*
6. 找到主类定义 (.main) 并追加到的 div 元素的样式。 您会注意到该代码将自动对齐帮助用户快速查找父级的类。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![在 CSS 中的层次结构对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 中的层次结构对齐方式")

    *在 CSS 层次结构的对齐方式*
7. 内部 **.main div**类中，在末尾处找到光标**边框： 0px;** 然后按**Enter**以显示 IntelliSense 列表。 开始键入**顶部**并请注意，当您键入筛选列表的方式。 列表中将显示包含的元素**顶部**在单词的任何部分 (在以前版本的 Visual Studio 中，对列表进行筛选的项的*开始*一词的)。

    ![IntelliSense 增强功能中 CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 中的 IntelliSense 增强功能")

    *在 CSS 中的 IntelliSense 增强功能*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>任务 2-颜色选取器

在此任务中，你会发现新的 CSS 颜色选取器集成到 Visual Studio IntelliSense。

1. 在中**Site.css，** 找到标头类定义 (.header) 并将光标放在下一步**背景色**属性，则之间&quot;:&quot;和&quot; #&quot;上的代码行的字符 **。**

    ![定位光标](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "定位光标")

    *定位光标*
2. 删除**冒号**（:） 和写入其再次显示颜色选取器。 请注意，您将看到的第一个颜色是你的站点的最常见的颜色。 如果您单击的白色的颜色，其 HTML 颜色代码 (#fff) 将替换样式表中的当前颜色代码。

    ![颜色选取器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "颜色选取器")

    *颜色选取器*
3. 按**Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) 颜色选取器，以显示的颜色渐变，然后拖动要选择不同的颜色的渐变光标上的按钮。 之后，单击**取色器**按钮，然后从屏幕中选择任何颜色。 请注意，将光标移动时，背景颜色值发生动态更改。

    ![颜色选取器渐变](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "颜色选取器渐变")

    *颜色选取器渐变*
4. 在中**不透明度**滑块，以减少不透明度的栏的中心移动选择器。 请注意，背景颜色值现在为 RGBA 更改其小数位数。

    ![颜色选取器不透明度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "颜色选取器不透明度")

    *颜色选取器不透明度*

    > [!NOTE]
    > CSS3 中的 RGBA （红色、 绿色、 蓝色、 Alpha） 颜色定义可以定义单个项的颜色不透明度值。 与不同**不透明度-** 类似 CSS 特性**-** RGBA 颜色也是与最新的浏览器兼容。

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>任务 3-CSS 兼容代码片段

在本任务中，您将学习如何使用跨浏览器兼容 CSS3 代码段来在你的网站中实现某些功能。

1. 在中**Site.css**文件中，找到**标头**CSS 类定义 (.header) 并将以下光标 **/\*边框半径\*/** 占位符，用于添加新的代码段。 按**Enter**若要显示的智能感知列表和类型**radius**来筛选列表。 选择**边框半径**从列表中双击，使用选项，然后按**选项卡**键以插入代码段。 然后，键入 radius 大小像素为单位，然后按**Enter**。 例如，键入**15px**。

    添加代码段的 CSS3 属性将呈现大多数 HTML5 法规遵从性浏览器，包括 Mozilla 和基于 WebKit 的浏览器中的圆角的边框。

    ![使用边框半径代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "使用边框半径代码段")

    *使用边框半径代码段*
2. 将相同的应用**边框**页样式 (.page) 中的代码段。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. 按**F5**运行该解决方案。 请注意，每个页面现在已舍入边框。

    ![圆角](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "圆角")

    *圆的角*
4. 关闭浏览器并返回到 Visual Studio。
5. 打开**Custom.css**下的文件**样式**文件夹并将光标置于**div.images u l l i i m g**类定义。
6. 按 enter 以显示 IntelliSense 列表中，类型**框阴影**然后按**选项卡**键两次以插入默认卷影的代码片段的类定义中。 将卷影值设置为**10px 10px 5px #888**。 然后，键入**边框半径**和插入的代码片段。 类型**15px**若要设置半径大小，然后按**ENTER**。

    ![圆角具有阴影](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "圆角具有阴影")

    *具有阴影的圆的角*

    > [!NOTE]
    > 此时，影子属性将插入相应的前缀 （moz、 易于使用的功能，o） 以支持 Mozilla 和易于使用的功能 (Chrome、 Safari，Konkeror) 浏览器。
7. 创建一个新类**div.images u l l i img:hover**如下**div.images u l l i i m g**类定义，并将光标置于括号 **。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. 类型**转换**然后按**选项卡**两次，以便插入转换代码片段的键。 然后，输入**rotate(-15deg)** 图像光标悬停上时更改旋转角度值。

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. 按**F5**若要运行解决方案并浏览到 CSS3 页。 请注意，映像有了圆形角和框阴影。 将鼠标悬停鼠标悬停在图像并观看这些旋转。

    ![转换旋转图像的代码片段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "转换代码片段旋转图像")

    *转换代码片段旋转图像*

    > [!NOTE]
    > 如果使用的 Internet Explorer 10 和不可以看到阴影，请确保文档模式设置为 IE10 标准。 按**F12**若要打开 Internet Explorer 开发人员工具，然后单击**文档模式**更改为 IE10 标准。

    ![有关-我们](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>练习 2： 什么是新的 HTML 编辑器

Visual Studio 提供了改进的 HTML 编辑器。 某些包含在此版本中的增强功能是 HTML 文档、 HTML5 代码段、 HTML 开始和结束标记匹配，和 HTML 验证的智能缩进。 在此练习中，会看到在网站标记中工作时，这些更改如何改善你熟练使用。

CSS 编辑器，如 HTML 编辑器还改进了。 这些改进大部分都是小的源表，使 Web 开发人员的生活更轻松。 如更多代码片段 HTML5，智能缩进时编辑和验证面向 HTML 文档 DOCTYPE 是这些改进的一些匹配开始和结束标记。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>任务 1-改进了的 DOCTYPE 验证

HTML 编辑器现在有能够检查您的页面，DOCTYPE，即使在定义可能在母版页中。 具体取决于您的页面的 DOCTYPE，HTML 编辑器将验证与正确的规则集，并将筛选考虑 DOCTYPE 元素的智能感知列表。

在本任务中，您将更改页面的 DOCTYPE 来查看 HTML 编辑器行为如何相应地变化。

1. 如果尚未打开，启动**Visual Studio** ，然后打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**本实验的文件夹。
2. 打开**Site.Master**页。
3. 验证工具栏，请注意，目标架构。 HTML 编辑器的行为 （验证、 IntelliSense 等） 的方法将正确更改以适应选择 Doctype。

    ![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML 源编辑工具栏中的使用 Doctype")

    *在 HTML 源编辑工具栏中使用 Doctype*
4. 将目标架构更改为 HTML 4.01。

    ![在 HTML 源编辑工具栏中更改 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML 源编辑工具栏中更改文档类型")

    *在 HTML 源编辑工具栏中更改文档类型*
5. 将在光标**正文**元素，并开始键入 HTML5 元素的名称 (例如，**视频**)。 请注意，该元素不可用的 IntelliSense 列表中。

    ![未列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "未列出的 HTML5 元素")

    *未列出的 HTML5 元素*
6. 有关验证工具栏中，选择 DOCTYPE 撤销对目标架构的更改： XHTML5 从下拉列表中。

    ![在 HTML 源编辑工具栏中使用 Doctype](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML 源编辑工具栏中的使用 Doctype")

    *在 HTML 源编辑工具栏中的重置 Doctype*
7. 将在光标**正文**元素并开始再次键入 HTML5 元素 (例如，像**视频**)。 请注意，HTML5 元素现在在 IntelliSense 列表中可用。

    ![所列出的 HTML5 元素](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "所列出的 HTML5 元素")

    *所列出的 HTML5 元素*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>任务 2-开始/结束标记自动更新

Visual Studio 现在可以更新打开或关闭正在编辑相互匹配的元素的标记的 HTML。 编辑 HTML 标记时，这一新功能将提高工作效率。

1. 上**Default.aspx**页上，添加**H3**具有标题 (例如，Visual Studio 2012 Rocks ！) 的元素。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. 更改**H3**标记和类型**H2**或**H1。**

    请注意，结束标记会自动更新。 此外可以修改以查看，开始标记会相应地更新过的结束标记。

    ![结束标记的自动更新](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "的结束标记的自动更新")

    *自动更新的结束标记*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>任务 3-新的 HTML5 代码片段

Visual Studio 现在包含几个 HTML5 代码片段。 在本任务中，您将使用这些代码段的一些。

1. 添加名为的新文件夹**音频**到网站文件夹的根目录。 打开 Windows 资源管理器，并复制到任何音频文件**音频**的文件夹**WhatsNewASPNET.sln**解决方案。
2. 在中**Default.aspx**页上，找到下 Web11 Rocks 游标!! 标头。 类型**音频**按 TAB 键。

    新的 HTML 编辑器包含 HTML5 内容的代码的片段。 请记住使用正确的 DOCTYPE 定义来启用 HTML5 片段。

    ![插入 HTML5 代码段](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "插入 HTML5 代码段")

    *插入 HTML5 代码段*
3. 更新为指向现有的音频文件的音频源。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > 你将需要向解决方案添加音频文件。
4. 按**F5**来运行网站和播放音频。

    ![运行音频控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "运行音频控件")

    *运行音频控件*

    > [!NOTE]
    > 此外可以尝试更多代码段包含在 Visual Studio 中，例如视频、 图，等等。
5. 现在，请尝试插入控件页的某些部分。 例如，尝试插入**GridView**控件，但无需键入**&lt;网格，** 开始键入 **&lt;GV**。 请注意，IntelliSense 列表显示了**asp: GridView**控件。

    HTML 编辑器中 IntelliSense 现在提供了标题大小写搜索，以及部分匹配 （检索包含术语的所有元素）。

    ![插入智能感知列表与 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "插入智能感知列表与 GridView")

    *插入智能感知列表与 GridView*

    如果键入**&lt;网格**将获取词匹配的所有项，但 Visual Studio 将建议**gridview**控件：

    ![插入与 IntelliSense 列表和部分匹配 GridView](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "插入与 IntelliSense 列表和部分匹配的 GridView")

    *插入与 IntelliSense 列表和部分匹配的 GridView*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>任务 4-HTML 编辑器智能标记

HTML 编辑器中的另一个改进是智能标记功能。 智能标记，使其可以轻松地在每个控件的基础上执行常见或重复的开发任务。 此功能已可在 HTML 设计器中，但不是在 HTML 编辑器中。

1. 打开**Site.Master**并找到**asp： 菜单**元素。 将光标置于开始标记，可以看到小的标志符号显示在元素的底部单击它以打开智能任务菜单。 请注意，您可以快速访问与菜单控件相关的一些任务。

    ![智能的菜单控件任务](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "智能菜单控件任务")

    *菜单控件的智能任务*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>任务 5-智能缩进

以 html 格式的最佳做法之一缩进使代码保持为可读的嵌套的元素。 在 Visual Studio 2012 中，您将注意到，编辑器会自动缩进元素你正在编写代码。

> [!NOTE]
> 在以前版本的 Visual Studio，提供智能缩进的 XML 编辑器中，但不是在 HTML 编辑器中。


1. 请确保在 HTML 编辑器中的缩进配置设置为智能缩进。 为此，请选择**工具 |选项**菜单选项，然后选择**文本编辑器 |HTML |选项卡**屏幕的左窗格中的页面。 选择智能缩进选项。

    ![HTML 编辑器设置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 编辑器设置")

    *HTML 编辑器设置*
2. 上**Default.aspx**页上，删除音频元素下的所有内容。
3. 将光标放在打开的末尾**音频**元素并点击**ENTER**。

    请注意，新光标位置包含一个额外的缩进级别。

    ![智能缩进的 HTML 编辑器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "智能缩进的 HTML 编辑器")

    *智能缩进的 HTML 编辑器*
4. 还原已删除，或关闭的内容的音频标记**Default.aspx**而不保存所做的更改。

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>任务 6-中提取到用户控件

包含在 Visual Studio 中，如提取了一部分的函数代码的重构工具是促进改善和重构现有代码的强大功能。 对应的 ASP.NET 页面会提取到用户控件的 HTML 代码。 手动执行操作将涉及几个步骤，如创建新的用户控件，将在代码部分移动到用户控件、 注册用户控件标记前缀和，最后，实例化页面上的用户控件。 现在，新*提取到用户控件*工具将为您自动执行所有这些步骤。

在此任务中，将使用新提取到用户控件上下文操作从所选的代码生成新的用户控件。

1. 上**Default.aspx**页上，选择**H2**并**音频**元素。
2. 右键单击并选择**提取到用户控件**。

    ![提取到用户控件菜单选项](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "提取到用户控件菜单选项")

    *提取到用户控件菜单选项*
3. 键入新的用户控件的名称。 例如， **Jukebox.ascx**，然后单击**确定**。

    ![正在保存提取的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "保存提取的用户控件")

    *正在保存提取的用户控件*
4. 请注意，所选的代码提取到用户控件，且所选代码的原始位置被替换的新的用户控件实例。

    ![页自动更新为使用新的用户控件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "页自动更新为使用新的用户控件")

    *页自动更新为使用新的用户控件*
5. 按**F5**以运行该页并验证控件是否正常工作。

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>练习 3： 什么是 JavaScript 编辑器中的新增功能

编写或编辑 JavaScript 代码不是简单的任务，尤其是在启动应用程序大小增大，您发现自己处理长文件和数百个函数。 脚本开发人员通常需要执行一些额外的工作保持代码以增强可读性并在文件之间导航。 包含的类似 jQuery 的 JavaScript 库，脚本导航变得艰巨本身由于代码长度。

Visual Studio 已续订，它有望使代码模式，可访问和组织使用的 JavaScript 编辑器。 C# 或 VB 编辑器中已存在的许多 Visual Studio 功能现在已实现 JavaScript 编辑器中： 转到定义、 自动缩进、 文档和验证在编写时。 使用续订的智能感知列表就能够轻松获得相关 JavaScript 函数目录。

在此练习中，您将学习一些新功能和改进的 JavaScript 编辑器。 浏览示例文件，并将发现每个将提高 JavaScript 编程的效率 Visual Studio 2012 中的新特征。

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>任务 1-JavaScript 编辑器新增功能

此任务将向您介绍的一些新的 JavaScript 编辑器功能，重点组织你的代码并将更好的用户体验。

1. 如果尚未打开，启动**Visual Studio** ，然后打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**本实验的文件夹。
2. 按**F5**若要运行该应用程序，然后单击导航栏中的 JavaScript 链接。 刷新页面几次并检查如何此计数器会递增。

    ![页计数器](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "页计数器")

    *页计数器*
3. 关闭浏览器并返回到 Visual Studio。
4. 打开**JavaScript.aspx**页上，找到**&lt;脚本&gt;** 块 （如下所示）。

    下面的代码使用 HTML5 本地存储来存储*pageLoadCount*变量，用于存储当前用户访问页的次数。 本地存储是引入了 HTML5 标准的客户端的键 / 值数据库。 在用户的浏览器在本地计算机上保存的数据。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > 请确保在继续进行下一步骤之前设置为 XHTML5 DOCTYPE。
5. 编辑代码，并请注意，适用于 JavaScript 的 IntelliSense，包括 HTML5 功能，如本地存储区和其内部方法。

    ![在 JavaScript 中的 HTML5 JavaScript 功能](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "在 JavaScript 中的 HTML5 JavaScript 功能")

    *在 JavaScript 中的 HTML5 JavaScript 功能*
6. 单击任何左大括号 (**{**) 从脚本代码，并请注意，括号会突出显示。

    ![突出显示括号](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "括号突出显示")

    *括号突出显示*
7. 取消注释该函数**testAutoAlign()** (选择三行，可以使用**CTRL** + **K**;**CTRL** + **U**) 并找到光标置于函数代码。 按 enter 将第二个代码行追加。 请注意，代码现**对齐**并**自动缩进**。

    ![JavaScript 代码将自动对齐](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 代码将自动对齐")

    *JavaScript 代码将自动对齐*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>任务 2-验证 JavaScript

在此任务中，你会发现 ECMAScript5 标准的新 JavaScript 验证。 此功能将帮助你编写符合 JavaScript 代码，而站点部署前阻止脚本问题。

> [!NOTE]
> Visual Studio 2010 实现 ECMAStript3 法规遵从性，而 Visual Studio 2012 提供 ECMAScript5 法规遵从性。


1. 打开**ECMA5script5.js**位于**Scripts\custom**项目文件夹。 现在，您将测试针对 ECMAScript5 标准的验证。

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    您可以签出&quot;**使用严格**&quot;文件，使 ECMAScript5 的第一行中的方向**严格模式下**。 此模式下包括阐明了从过去的版本，二义性和对象属性上添加了一些新功能，如 getter 和 setter、 JSON 和更完整的反射的库支持的语言的子集。
2. 打开**错误列表**如果尚未打开 (**视图**菜单 |**错误列表**)。 请注意**函数**声明是否带下划线。 这是因为在 ECMA5 标准函数不能嵌套在语言结构。 在错误列表下面将看到警告详细信息。

    ![JavaScript 验证错误消息](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 验证错误消息")

    *JavaScript 验证错误消息*
3. 注释掉**&quot;使用严格&quot;** 方向和错误消失，但警告保留的注意。
4. 在该文件的最后一行，编写任何字符串，如**&quot;测试&quot;** （包括引号以指示它是作为字符串）。 编写一段字符串可以显示 IntelliSense 列表中，并选择旁边**剪裁**选项。

    在 ECMAScript5 标准中，字符串值和变量也有定义，如裁剪、 大写、 搜索和替换的字符串方法。

    ![在 JavaScript 中的 IntelliSense 列表](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "在 JavaScript 中的 IntelliSense 列表")

    *在 JavaScript 中的 IntelliSense 列表*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>任务 3-适用于 JavaScript 的 XML 文档

在本任务中，您将了解有关在 JavaScript 中的 XML 文档的 Visual Studio 功能。 你将看到 JavaScript IntelliSense 列表现在显示每个函数的 XML 文档。 此外，你会发现在 JavaScript 中的导航功能。

1. 打开**XMLDoc.js**文件位于**自定义脚本/** 项目文件夹。 此文件包含有关每个 JavaScript 函数的 XML 文档。

    ![JavaScript XML 文档中集成智能感知](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "intellisense 集成 JavaScript XML 文档")

    *IntelliSense 中集成的 JavaScript XML 文档*
2. 下面**添加**函数，在**XMLDoc.js**文件中，创建一个名为的新函数**测试**。
3. 在中**测试**函数中，调用**multiply**接收两个参数的函数。 请注意，在显示工具提示框**乘**函数文档。

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![对于 JavaScript 函数的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "对于 JavaScript 函数的 XML 文档")

    *对于 JavaScript 函数的 XML 文档*
4. 完成的函数调用语句和类型*点*打开智能感知列表上返回的值。 请注意，Visual Studio 检测**返回**在文档中，将该值视为一个数字值。

    ![返回类型的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "返回类型的 XML 文档")

    *返回类型的 XML 文档*
5. 现在，插入添加函数的调用。 请注意，JavaScript 编辑器现在支持的函数重载。 当您编写的函数名称时，你将能够选择任何可用的文档中指定的重载。

    ![重载的 XML 文档](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "重载的 XML 文档")

    *重载的 XML 文档*
6. 打开**GotoDefinition.js**文件，找到 **$().html()** 函数调用。 上定位光标**html**。
7. 按**F12**和导航到的定义。 请注意，现在可以访问，并浏览您的 JavaScript 代码，而不使用**查找**工具。
8. 在底部的代码文件的签名块之前的 jQuery 指令上找到光标。 按**F12**。 您将导航到 jQuery 库文件。 请注意，还可以在使用 jQuery 文件之间导航**F12**。

    ![导航到 jQuery 定义](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "导航到 jQuery 定义")

    *导航到 jQuery 定义*

> [!NOTE]
> 请确保 GotoDefinition.js 保存该文件之前具有没有语法错误。


<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>练习 4： 捆绑和缩小

多少次你的网站是否包含多个 JavaScript 或 CSS 文件？ 这是非常常见的方案的捆绑和缩小可帮助以减小文件大小并使站点执行速度更快。 ASP.NET 4.5 中的新绑定功能 JS 或 CSS 文件的一组包为单个元素，并通过缩小内容 （即删除不是必需的空白区域，删除注释，减少标识符） 来减小其大小。

捆绑和缩小 ASP.NET 4.5 中的执行在运行时，以便过程可以识别用户代理 （例如 IE、 Mozilla 等） 并因此，通过面向用户浏览器 （例如，删除内容 Mozilla 特定改进压缩当请求来自 IE）。

在此练习中，您将了解如何启用和 ASP.NET 4.5 中使用不同类型的绑定和缩减。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>任务 1-安装捆绑和缩小从 NuGet 包

1. 如果尚未打开，启动**Visual Studio** ，然后打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**本实验的文件夹。
2. 打开 NuGet 包管理器控制台。 若要执行此操作，使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。

    ![打开包管理器 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "打开包管理器控制台")

    *打开包管理器控制台*
3. 在**程序包管理器控制台**类型**Install-package Microsoft.Web.Optimization**然后按**ENTER**。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>任务 2-默认捆绑包

使用绑定和缩减的最简单方法是启用的默认捆绑包。 此方法使用约定来让你引用的文件夹中的 JS 和 CSS 文件的捆绑和缩小化版本。

在本任务中，您将学习如何启用和引用捆绑和缩小 JS 和 CSS 文件和查看生成的输出。

1. 如果尚未打开，启动**Visual Studio** ，然后打开**WhatsNewASPNET.sln**解决方案位于**Source\WhatsNewASPNET**本实验的文件夹。
2. 在中**解决方案资源管理器**，展开**样式**， **Scripts\custom**并**Scripts\bundle**文件夹。

    请注意，该应用程序使用多个 CSS 和 JS 文件。

    ![在应用程序中的多个样式表和 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "应用程序中的多个样式表和 JavaScript 文件")

    *在应用程序中的多个样式表和 JavaScript 文件*
3. 打开**Global.asax.cs**文件。

    请注意，新**Microsoft.Web.Optimization**命名空间已被注释掉文件开头。 取消注释的 using 指令以包括捆绑和缩小功能。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. 找到**应用程序\_启动**方法。

    在此方法中，取消注释 EnableDefaultBundles 调用，如下面的代码段中所示。 这使我们能够通过使用到该文件夹的路径中引用捆绑的集合文件夹中的 CSS 文件再加上&quot;CSS&quot;或&quot;JS&quot;后缀。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. 打开**Optimization.aspx**文件，找到的内容控件**HeadContent**。

    请注意，CSS 文件和 JS 文件具有单个引用的标记。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > 此代码是出于演示目的。 理想情况下，将引用 Site.Master 文件中的捆绑包。 在此示例代码中，您将发现一些绑定的文件，也正在 Site.Master 文件中，通过引用进行此最后一个引用冗余。
6. 请注意，使用链接中的绑定约定**href**属性从样式和 Scripts\custom 获取所有 CSS 或 JS 文件文件夹分别。

    可以使用路径**脚本/自定义/JS**捆绑和缩小内的所有 JS 文件如下所示**自定义脚本/** 文件夹。 这是默认捆绑包的默认行为。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. 打开**Styles\Site.css**文件。

    请注意，原始的 CSS 文件包含缩进的代码、 空格和扩大文件的注释。 （还 JavaScript 文件包含空格和注释）。

    ![脚本文件夹中的一个原始的 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "脚本文件夹中的一个原始的 CSS 文件")

    *在脚本文件夹中的原始 CSS 文件之一*
8. 按**F5**运行该应用程序并导航到**优化**页。
9. 单击**CSS 捆绑包**链接以下载并打开文件。

    签出缩小捆绑文件。 您会注意到，已删除所有空格、 注释和缩进字符，生成较小的文件。

    ![在绑定的 CSS 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "捆绑 CSS 文件")

    *绑定的 CSS 文件*
10. 现在，单击**JS 捆绑**链接以打开捆绑在一起的 JavaScript 文件。 你可以安全地忽略警告的资源管理器。 请注意下的 JavaScript 文件**自定义**文件夹也捆绑和缩小。

    ![在绑定的 JavaScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "捆绑 JavaScript 文件")

    *绑定的 JavaScript 文件*

    启用 CSS 或 JS 文件的压缩是复杂得多早期 ASP.NET 版本中。 现在，如您所见，您只需添加中的一行*Global.asax*文件启用绑定，并从你的站点引用捆绑的文件。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>任务 3-静态捆绑包

静态捆绑包方法，可自定义捆绑包、 引用和缩小方法用于将文件组。

在此任务中，您将配置一个静态的捆绑包来定义一组特定的捆绑和缩小的文件。

1. 关闭浏览器。
2. 打开**Global.asax.cs**文件，找到**应用程序\_启动**方法。
3. 取消注释下面的代码中所示的静态绑定代码。

    要定义了将使用引用的静态捆绑&quot; **~/StaticBundle** &quot;虚拟路径和使用**JsMinify**与所有指定文件缩减为**AddFile**方法。 最后，要添加到静态捆绑**BundleTable**和启用它。

    请注意，文件不位于同一位置;这是通过默认绑定的另一个优点。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. 打开**Optimization.aspx**文件。

    请注意，指向**静态 JS 捆绑**正在使用时在 Global.asax.cs 文件中配置静态捆绑包已声明的路径： **/StaticBundle**。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. 按**F5**若要运行该应用程序，然后导航到**优化**页。
6. 单击**静态 JS 捆绑**链接以打开该文件。

    请注意，缩小捆绑 JavaScript 文件是在路径下的静态绑定文件中配置的所有 JavaScript 文件的输出&quot;/StaticBundle&quot;。

    ![静态 JavaScript 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "静态 JavaScript 文件捆绑包")

    *静态 JavaScript 文件捆绑在一起*
7. 关闭浏览器并返回到 Visual Studio。

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>任务 4-动态文件夹捆绑包

在本任务中，您将学习如何配置动态文件夹捆绑包。 动态绑定的强大功能是可以包含静态 JavaScript，以及其他文件中将编译为 JavaScript 的语言，因此，需要进行一些处理绑定执行之前。

在此示例中，您将学习如何使用**DynamicFolderBundle**类，以创建用于写入 CofeeScript 中的文件的动态捆绑包。 CofeeScript 是一种编程语言，将编译为 JavaScript，提供更简单的语法来编写 JavaScript 代码，从而加强 JavaScript 的简洁和可读性。

1. 打开**Global.asax.cs**文件，找到**应用程序\_启动**方法。
2. 取消注释以下代码中所示的动态绑定代码。

    定义了将使用的动态文件夹捆绑**CoffeeMinify**将仅应用到的文件的自定义缩小处理器&quot; **.coffee** &quot;扩展 (CoffeeScript 文件）。 请注意，您可以使用搜索模式来选择要在文件夹中，如捆绑的文件\*.coffee。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. 打开 NuGet 包管理器控制台。 若要执行此操作，使用菜单**视图** | **其他 Windows** | **程序包管理器控制台**。
4. 在**程序包管理器控制台**类型**Install-package CoffeeSharp**然后按**ENTER**。
5. 单击**显示所有文件**按钮**解决方案资源管理器**窗口

    ![显示所有文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "都显示所有文件")

    *显示所有文件*
6. 右键单击**CoffeeMinify.cs**中的文件**解决方案资源管理器**，然后选择**包括在项目**

    ![在项目中包含 CoffeeMinify.cs 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "在项目中包含 CoffeeMinify.cs 文件")

    *在项目中包含 CoffeeMinify.cs 文件*
7. 打开**CoffeeMinify.cs**文件。

    此类继承自 JsMinify 来缩小由 CoffeeScript 代码编译产生的 JavaScript 输出。 它将调用 CoffeeScript 编译器首先，生成的 JavaScript 代码，然后将其发送给 JsMinify.Process 方法，以缩小生成的代码。

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. 打开**Script1.coffee**并**Script2.coffee**从文件**脚本/捆绑**文件夹。

    这些文件将包括 CoffeScript 代码执行与 CoffeeMinify 类绑定时编译。

    为简单起见，提供的 CoffeeScript 文件仅包含 CoffeeScript 示例代码。 注释不由 JsMinify 进程。

    ![CoffeeScript 文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 文件")

    *CoffeeScript 文件*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/)提供更简单的语法来编写 JavaScript 代码、 增强了 JavaScript 的简洁和可读性，以及添加其他功能，如数组理解和模式匹配。
9. 打开**Optimization.aspx**文件，找到的捆绑包链接。

    请注意，到链接**动态 JS 捆绑**引用的**脚本/捆绑包**使用文件夹 **/咖啡**动态文件夹绑定配置的后缀。

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. 按**F5**若要运行该应用程序，然后导航到**优化**页。
11. 单击**动态 JS 捆绑**链接以打开生成的文件。

    请注意，此捆绑包中包含的内容仅包含 **.coffee**文件。 此外可以看到 CoffeeScript 代码编译为 JavaScript 且已删除注释掉的行。

    ![动态 JS 文件捆绑](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "动态 JS 文件捆绑包")

    *动态 JS 文件捆绑在一起*

> [!NOTE]
> 此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。


<a id="Summary"></a>
## <a name="summary"></a>总结

此实验室可帮助你了解什么是 ASP.NET 中的新增功能和 Visual Studio 2012 中的 Web 开发以及如何利用 Visual Studio 2012 中的许多增强功能。

通过完成本动手实验，你已了解到如何在 Visual Studio 2012 编辑器中使用的新功能和改进，CSS、 JavaScript 和 HTML。 此外，你已了解到 Visual Studio 2012 如何实现内置绑定和缩减。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *VS Express for Web 磁贴*

* * *

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-创建新的 Web 站点从 Windows Azure 门户

1. 转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。 快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。

    ![正在下载网站发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。

    ![保存发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "保存发布配置文件")

    *保存发布配置文件*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框。 输入规则的名称，然后单击![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)按钮。

    ![添加客户端 IP 地址](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *确认更改*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![配置目标连接字符串](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

    ![应用程序发布到 Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "应用程序发布到 Windows Azure")

    *应用程序发布到 Windows Azure*
