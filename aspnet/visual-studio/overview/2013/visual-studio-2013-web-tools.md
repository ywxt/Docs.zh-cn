---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 动手实验： Visual Studio 2013 Web 工具 |Microsoft Docs
author: rick-anderson
description: Visual Studio 是一个极好开发环境。基于 NET 的 Windows 和 web 项目。 它包括一个强大的文本编辑器，可轻松用于...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 8f0f19a184d50cdc6e8e5a2da0e55a0e8ca44dc5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399395"
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a>动手实验： Visual Studio 2013 Web 工具
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](http://aka.ms/webcamps-training-kit)

> Visual Studio 是一个极好开发环境。基于 NET 的 Windows 和 web 项目。 它包括一个强大的文本编辑器，可以轻松地用来编辑不含项目的独立文件。
> 
> 在编辑每个文件时，visual Studio 维护全面分析树。 这样，Visual Studio 以进行更快、 更舒适的开发体验的同时提供无与伦比的自动完成功能和基于文档的操作。 这些功能会特别大 HTML 和 CSS 文档中。
> 
> 所有这种能力也是可用于扩展，使其易于扩展，具有强大的新功能以满足你需求的编辑器。 Web Essentials 是一系列 （主要） 与 web 相关增强功能 Visual Studio。 它还包括了许多新的 IntelliSense 完成 （尤其是对于 CSS)、 新的浏览器链接功能、 自动 JSHint 的 JavaScript 文件、 HTML 和 CSS 和对新式 web 开发至关重要的许多其他功能的新的警告。
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。


<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 使用新的 HTML 编辑器功能，这些功能包含在 Web Essentials 等丰富的 HTML5 代码代码段和处理编码
- 使用颜色选取器和浏览器矩阵工具提示等 Web Essentials 中包括的新 CSS 编辑器功能
- 使用 Web Essentials 等中提取到文件和智能感知中包括的所有 HTML 元素的新 JavaScript 编辑器功能
- 你的浏览器和 Visual Studio 中使用浏览器链接之间交换数据

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下：

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行本动手实验中练习，需要先设置你的环境。

1. 打开 Windows 资源管理器窗口并浏览到本实验**源**文件夹。
2. 右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。
3. 如果显示用户帐户控制对话框中，确认要继续执行的操作。

> [!NOTE]
> 请确保您运行安装程序之前已为此实验室的所有依赖项。


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码片段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。

> [!NOTE]
> 每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。 请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。 在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。 如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [使用浏览器链接和 Web Essentials](#Exercise1)
2. [利用代码段和 IntelliSense](#Exercise2)

> [!NOTE]
> 在首次启动 Visual Studio，您必须选择一个预定义的设置集合。 每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。 此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。 如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>练习 1： 使用浏览器链接和 Web Essentials

**Web Essentials**是一个 Visual Studio 扩展，将添加各种新式 web 开发，主要侧重于使 web 开发体验更快、 更舒适的有用功能。 可以从 Visual Studio 中的扩展库安装 Web Essentials。

**浏览器链接**是提供你的 web 应用程序和 Visual Studio 之间交换数据的 Visual Studio IDE 和任何打开的浏览器之间通道的 Visual Studio 2013 中包含的新功能。 Web Essentials 扩展浏览器链接了用来操作 DOM 对象模型和您直接从浏览器的 web 页面的 CSS 样式的工具。

在此练习中，您将了解一些支持的功能**Web Essentials**并**浏览器链接**来增强简单的测验页。

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>任务 1-在多个浏览器中运行项目

在本任务中，将配置 web 应用程序以在多个浏览器在运行一次，这对于跨浏览器测试很有用。

1. 打开**Microsoft Visual Studio**。
2. 在中**文件**菜单中，选择**打开 |项目/解决方案...** 并浏览到**Ex1 WorkingwithBrowserLinkandWebEssentials\Begin**中**源**实验室 (C:\WebCampsTK\HOL\VSWebTooling\Source) 的文件夹。 选择**Begin.sln**然后单击**打开**。
3. 在 Visual Studio 工具栏中，展开浏览器菜单并选择**浏览方式...**.

    ![浏览与菜单选项](visual-studio-2013-web-tools/_static/image1.png "浏览与...在浏览器菜单")

    *浏览与菜单选项*
4. 中**浏览方式**对话框中，选择这两种**Google Chrome**并**Internet Explorer**通过按住**CTRL**键，然后单击**设置为默认值**。

    ![浏览方式对话框](visual-studio-2013-web-tools/_static/image2.png "浏览方式对话框")

    *选择多个默认浏览器*
5. Google Chrome 和 Internet Explorer 现在应显示为默认浏览器。 单击**取消**以关闭对话框。

    ![Google Chrome 和 Internet Explorer 设置为默认浏览器](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 的默认浏览器")

    *Google Chrome 和 Internet Explorer 设置为默认浏览器*

    > [!NOTE]
    > 配置默认浏览器之后,**多个浏览器**浏览器菜单中选择选项。
    > 
    > ![多个浏览器](visual-studio-2013-web-tools/_static/image4.png "多个浏览器")
6. 按**CTRL** + **F5**不进行调试直接运行该应用程序。
7. 这两个浏览器窗口打开时，请将其中一个上下放以便同时查看两个浏览器上的更新。 浏览器应显示具有浅蓝色矩形的 web 页。

    ![放置一个浏览器上下](visual-studio-2013-web-tools/_static/image5.png "放置上面另一个浏览器")

    *将上面另一个浏览器*
8. 不要关闭浏览器。 将在下一个任务中使用它们。

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>任务 2-使用 Zen 编码来创建 HTML 元素

**处理编码**是一种编辑器，适用于高速 HTML、 XML、 XSL （或任何其他结构化的代码格式） 插件编写代码和编辑。 此插件的核心是一个功能强大的缩写引擎可用于扩展到 HTML 代码-类似于 CSS 选择器的表达式。 处理编码是一种编写 HTML 使用 CSS 样式选择器语法的快速方法。

在此练习中，将使用提供的 Web Essentials Zen 编码功能来生成表示问题的选项的 HTML 按钮。

1. 切换回 Visual Studio。
2. 打开**Index.cshtml**文件位于**视图** | **主页**文件夹。
3. 替换**&lt;！-TODO： 添加选项-&gt;** 注释以下代码，然后按**选项卡**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. 代码应扩展到 HTML。

    ![扩展的 HTML](visual-studio-2013-web-tools/_static/image6.png "扩展 HTML")

    *扩展的 HTML*

    > [!NOTE]
    > 若要了解有关处理编码语法的详细信息，请参阅以下[一文](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。
5. 单击**刷新链接的浏览器**按钮更新两个浏览器。

    ![刷新链接的浏览器](visual-studio-2013-web-tools/_static/image7.png "刷新链接的浏览器")

    *刷新链接的浏览器*

    ![Internet Explorer-带四个按钮更新页](visual-studio-2013-web-tools/_static/image8.png "带四个按钮的 Internet 资源管理器-页面更新")

    *带四个按钮的 Internet 资源管理器-页面更新*

    ![Google Chrome-带四个按钮更新页](visual-studio-2013-web-tools/_static/image9.png "带四个按钮的 Google Chrome-页面更新")

    *带四个按钮的 Google Chrome-页面更新*
6. 切换回 Visual Studio。
7. 这些按钮添加到页上，但仍需要添加模板问题。 若要执行此操作，将使用一项新功能中调用的 Web Essentials**乱数假文生成器**。 找到**div**具有元素**类**特性**front**。
8. 添加以下代码作为第一个子元素**div**，然后按**选项卡**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. 代码应扩展到 HTML。

    ![乱数假文自动生成](visual-studio-2013-web-tools/_static/image10.png "乱数假文自动生成")

    *乱数假文自动生成*

    > [!NOTE]
    > 作为处理编码的一部分，现在可以直接在 HTML 编辑器中生成乱数假文代码。 只需键入**lorem**并点击**选项卡**和 30 字乱数假文将插入文本。 例如， *lorem10*插入 10 位乱数假文的单词。
10. 将顶部的问题添加徽标，使用另一项新功能中调用的 Web Essentials **Lorem 像素生成器**。 添加以下代码作为第一个子元素**div**具有元素**容器**作为**类**值，然后按**选项卡**。

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. 该代码应该扩展以 html 格式。

    ![Lorem 像素自动生成](visual-studio-2013-web-tools/_static/image11.png "Lorem 像素自动生成")

    *Lorem 像素自动生成*

    > [!NOTE]
    > 作为处理编码的一部分，还可以直接在 HTML 编辑器中生成 Lorem 像素的代码。 只需键入**pix 200x200 动物**并点击**选项卡**和一个**i m g**将插入动物的大小为 200x200 映像的标记。 有关详细信息，请参阅[Lorem 像素](http://www.lorempixel.com)。
12. 单击**刷新链接的浏览器**按钮更新两个浏览器。

    ![Internet Explorer-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自动生成的图像和文本")

    *Internet Explorer – 自动生成的图像和文本*

    ![Google Chrome-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自动生成的图像和文本")

    *Google Chrome-自动生成的图像和文本*

    > [!NOTE]
    > 添加代码段时，将随机选择映像，因为可能不同的浏览器中显示的图像。
13. 不要关闭浏览器。 将在下一个任务中使用它们。

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>任务 3-更新样式属性

在本任务中，您将使用浏览器链接**检查模式**功能检测生成特定的 DOM 元素的确切位置，然后更新使用颜色选取器通过 Web 提供该元素的颜色属性Essentials。

1. 在 Internet Explorer 浏览器中，按**CTRL** + **ALT** + **我**若要启用检查模式。
2. 将指针移动浅蓝色边框，然后单击。

    ![将指针移动到浅蓝色边框上方](visual-studio-2013-web-tools/_static/image14.png "浅蓝色边框上移动指针")

    *浅蓝色边框上移动指针*
3. 切换回 Visual Studio。 请注意如何在 Visual Studio HTML 编辑器中还选择在浏览器中选择 HTML 元素。

    ![在 Visual Studio HTML 编辑器中选择 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 编辑器中选择 HTML 元素")

    *在 Visual Studio HTML 编辑器中选择 HTML 元素*
4. 现在，你将更新**front**以更改所选元素的样式的 CSS 类。 若要执行此操作，按**CTRL** + **，** 以打开**导航到**搜索框中。 类型**site.css**然后按**ENTER**以打开该文件。

    ![打开文件 Site.css](visual-studio-2013-web-tools/_static/image16.png "打开 Site.css 文件")

    *打开文件 Site.css*
5. 按**CTRL** + **F**输 **.flip 容器.front**若要查找的 CSS 选择器。
6. 单击以打开颜色选取器的类的边框属性中的浅蓝色正方形。

    ![打开颜色选取器](visual-studio-2013-web-tools/_static/image17.png "打开颜色选取器")

    *打开颜色选取器*
7. 通过单击 v 形图标按钮展开颜色选取器并选择一种新颜色。

    ![展开颜色选取器](visual-studio-2013-web-tools/_static/image18.png "展开颜色选取器")

    *展开颜色选取器*
8. 按**CTRL** + **ALT** + **ENTER**刷新链接的浏览器。
9. 切换到 Internet 资源管理器，并请注意如何变化边框的颜色。

    ![Internet Explorer 的更新的边框颜色](visual-studio-2013-web-tools/_static/image19.png "Internet 资源管理器-更新的边框颜色")

    *Internet Explorer 的更新的边框颜色*
10. 切换到 Google Chrome，请注意如何变化边框的颜色。

    ![Google Chrome-更新的边框颜色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-更新的边框颜色")

    *Google Chrome-更新的边框颜色*
11. 切换回 Visual Studio。
12. 转到末尾**Site.css**文件，然后按**CTRL** + **F**查找 **.btn**选择器。
13. 请注意， **-webkit 边框半径**属性是否带下划线显示为绿色。

    ![-webkit 边框半径 btn 选择器的属性](visual-studio-2013-web-tools/_static/image21.png "btn 选择器-webkit 边框半径属性")

    *-webkit 边框半径属性的 btn 选择器*
14. 将在光标 **-webkit 边框半径**属性。 属性的第一个单词的第一个字母下应显示一条蓝线。 这是**智能标记**。
15. 按**CTRL** + **。** 若要打开建议菜单上，然后单击**缺少标准属性 （边框半径） 添加**。

    ![添加缺少的标准属性建议](visual-studio-2013-web-tools/_static/image22.png "添加缺少的标准属性建议")

    *添加缺失的标准属性建议*
16. **边框半径**属性将自动添加到 CSS 规则。

    ![添加的标准属性缺失](visual-studio-2013-web-tools/_static/image23.png "缺少添加的标准属性")

    *缺少添加的标准属性*
17. 将指针移**边框半径**属性来显示**浏览器矩阵工具提示**。 **浏览器矩阵工具提示**在每个浏览器中显示该属性的可用性。

    ![浏览器矩阵工具提示](visual-studio-2013-web-tools/_static/image24.png "浏览器矩阵工具提示")

    *浏览器矩阵工具提示*
18. 请注意，值**边框半径**属性是否仍带有下划线。 将指针移值以查看警告消息。

    ![边框半径属性值警告](visual-studio-2013-web-tools/_static/image25.png "边框半径属性值警告")

    *边框半径属性值警告*
19. 删除的单元**边框半径**作为工具提示所建议的属性值。
20. 作为**边框半径**是用于定义如何圆角的边框边角是，您可以删除的标准属性 **-webkit 边框半径**属性和值从 CSS 规则。
21. 将在光标**自动换行**属性，请注意，下面也会出现智能标记。
22. 打开菜单，然后单击**添加缺少的供应商具体内容**。

    ![添加缺少的供应商细节建议](visual-studio-2013-web-tools/_static/image26.png "添加缺少的供应商细节建议")

    *添加缺少的供应商细节建议*
23. **Ms 自动换行**属性将自动添加到 CSS 规则。

    ![供应商特定属性添加](visual-studio-2013-web-tools/_static/image27.png "添加供应商特定属性")

    *添加的供应商特定属性*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>任务 4-更新浏览器中的 HTML 代码

在本任务中，您将使用浏览器链接**设计模式下**编辑浏览器中的 DOM 对象并将所做的更改传输到 Visual Studio 中的 HTML 源代码文件的功能。

1. 在 Google Chrome 中，按**CTRL** + **ALT** + **D**若要启用设计模式。
2. 将指针移**Lorem Ipsum dolor sit amet**标记，单击。

    ![编辑问题](visual-studio-2013-web-tools/_static/image28.png "编辑问题")

    *编辑问题*
3. 应显示光标。 将原始文本替换为*什么它看起来像时我编写一个较长的问题？*，然后按**ESC**退出设计模式。

    ![编辑的问题](visual-studio-2013-web-tools/_static/image29.png "编辑的问题")

    *编辑的问题*
4. 切换回 Visual Studio 并打开**Index.cshtml**，如果尚未打开。 请注意的内部文本**&lt;p&gt;** 更新元素。

    ![在 HTML 页面中的最新问题](visual-studio-2013-web-tools/_static/image30.png "HTML 页中的更新问题")

    *在 HTML 页面中的更新的问题*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>任务 5-查看 SEO 相关警告

**搜索引擎优化**(SEO) 是网站排名更高版本上的搜索引擎结果列表中的过程。 更高版本站点进行排名和更连贯地列出，该站点将从该搜索引擎获取更多访问者。 Web Essentials 合并检查 HTML 的分析工具，报告问题，找到并提供了帮助来解决这些问题。

1. 转到**视图**菜单，然后单击**错误列表**以打开**错误列表**窗口。

    ![错误列表视图中菜单](visual-studio-2013-web-tools/_static/image31.png "视图菜单中的错误列表")

    *错误列表视图中菜单*
2. 请注意，没有通知的 SEO 警告**&lt;meta&gt;** 标记为缺少页说明。 双击 SEO 警告条目，以修复此错误。

    ![错误列表窗口](visual-studio-2013-web-tools/_static/image32.png "错误列表窗口")

    *错误列表窗口*
3. 在中**Web Essentials**对话框中，单击**是**插入说明&lt;元&gt;标记。

    ![Web Essentials 对话框](visual-studio-2013-web-tools/_static/image33.png "Web Essentials 对话框")

    *Web Essentials 对话框*
4. 编辑器 **\_Layout.cshtml**此时将打开并**&lt;元&gt;** 标记自动添加到**头**部分HTML 文件。

    ![自动添加 _Layout 页中的 Meta 标记](visual-studio-2013-web-tools/_static/image34.png "Meta 标记自动添加在 _Layout 页")

    *Meta 标记自动添加到\_布局页*
5. 更改的值**内容**归于*GeekQuiz*并保存该文件。

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>练习 2： 利用代码段和 IntelliSense

使用 Web Essentials HTML 编辑器已扩展具有额外功能。 在此练习中，你将看到一些新功能，开发 web 应用程序时很有用。

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>任务 1-在 HTML 文档中使用 IntelliSense

您将看到在本任务中的第一个新功能称为**动态 IntelliSense**。 动态 IntelliSense 读取其他标记和属性，以推断可能将使用的 id。

在本任务中，将创建新的 HTML 窗体元素包含一个标签和输入的字段。 然后，您将添加**为**属性为要将其绑定到的输入的标签，你将看到 IntelliSense 建议基于作用域中的输入的 id。

1. 打开**Visual Studio Express 2013 for Web**并**Begin.sln**解决方案位于**源/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/开始**文件夹。 或者，继续使用该解决方案并获得前一练习中。
2. 在中**解决方案资源管理器**，打开**Index.cshtml**文件位于**视图** | **主页**文件夹。
3. 添加以下形式内的**&lt;部分&gt;** 元素。

    (代码段- *VisualStudio2013WebTooling* - *Ex2* - *窗体*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. 输入的标记前面应带有标签的字段的一些说明。 添加以下标签之前输入的标记。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **有关**的属性**&lt;标签&gt;** 指定标签的窗体元素绑定到。 该属性的值应设置为相关的元素的 id。 添加**有关**归于**&lt;标签&gt;** 元素。 下图中所示&quot;名称&quot;值会弹出在 IntelliSense 中，基于相同的作用域内的元素的 id (封闭**&lt;窗体&gt;**)。

    ![在 IntelliSense 中显示 id](visual-studio-2013-web-tools/_static/image35.png "id 显示在 IntelliSense 中")

    *显示在 IntelliSense 中的 id*
6. 删除最近添加**&lt;窗体&gt;** 元素和其内容。

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>任务 2-使用 HTML 代码段

HTML5 引入了 25 个以上的新语义标记。 Visual Studio 已具有对这些标记的 IntelliSense 支持，但 Visual Studio 2013 可以更快、 更轻松地通过添加新的代码片段编写标记。 尽管这些标记不是复杂的但这会产生一些小的微妙之处，例如添加为正确的编解码器回退*音频*标记。 在此任务中，您将看到的音频的标记的 HTML 代码段。

1. 在中**Index.cshtml**文件中，键入 **&lt;aud**内**&lt;部分&gt;** 元素在下图中所示。

    ![插入音频元素](visual-studio-2013-web-tools/_static/image36.png "插入音频元素")

    *插入音频元素*
2. 按**选项卡**两次请注意如何在页上添加以下代码，并将光标置于**src**的第一个源的属性。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > 通过按**选项卡**键两次，插入代码段。 音频的代码段显示了标准使用情况*音频*具有改进的支持的两个源代码文件的标记。
3. 删除第二行，然后使用以下链接 WebCampsTV Katana 显示更新的第一行源： [ http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3 ](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。 生成的代码如下所示。

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > 源文件*KatanaProject.mp3*用作示例。 如果您愿意，可以使用另一个源。
4. 按**CTRL** + **S**保存该文件。
5. 按**CTRL** + **F5**启动应用程序。
6. 请注意音频播放机已添加到应用程序。

    ![在 Internet Explorer 中的音频播放器](visual-studio-2013-web-tools/_static/image37.png "在 Internet Explorer 中的音频播放机")

    *在 Internet Explorer 中的音频播放器*

    ![在 Google Chrome 中的音频播放器](visual-studio-2013-web-tools/_static/image38.png "音频播放机在 Google Chrome")

    *在 Google Chrome 中的音频播放器*
7. 不要关闭浏览器。 将在下一个任务中使用它们。

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>任务 3-使用 JavaScript 文档中的 IntelliSense

Web Essentials 2013，样式表和 HTML 页面生成 Id 和类名称的列表。 在本任务中，您将学习如何这些列表，从而改进 Web Essentials 2013 中的 JavaScript IntelliSense 支持。

1. 在中**Index.cshtml**文件中，添加以下代码以定义**脚本**标记的 JavaScript 代码。

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. 添加以下代码**脚本**标记定义准备就绪的回调函数。

    (代码段- *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. 将在光标**脚本**标记，然后按**CTRL** + **。** 若要打开建议菜单。
4. 单击**提取到文件**。

    ![JavaScript 将解压缩到文件的建议](visual-studio-2013-web-tools/_static/image39.png "JavaScript 提取到文件的建议")

    *JavaScript 将解压缩到文件的建议*
5. 在中**另存为**窗口中，选择**脚本**文件夹中，将文件命名**init.js**然后单击**保存**。

    ![另存为窗口](visual-studio-2013-web-tools/_static/image40.png "另存为窗口")

    *另存为窗口*

    > [!NOTE]
    > **Init.js**创建文件和脚本的内容移动到文件。
    > 
    > ![使用包含的内容创建 Init.js 文件](visual-studio-2013-web-tools/_static/image41.png "Init.js 文件包含的内容创建")
    > 
    > *使用包含的内容创建 Init.js 文件*
6. 打开**Index.cshtml**文件，然后检查脚本标记被替换的引用**init.js**文件。

    ![Init.js html 引用](visual-studio-2013-web-tools/_static/image42.png "Init.js html 引用")

    *Init.js html 引用*
7. 转到**解决方案资源管理器**您会发现**init.js**文件已自动包含在解决方案中。

    ![Init.js 文件包含在解决方案中](visual-studio-2013-web-tools/_static/image43.png "Init.js 文件包含在解决方案中")

    *Init.js 文件包含在解决方案中*
8. 切换回**init.js**文件以更新**准备**函数回调。
9. 在传递给函数回调定义*准备*，添加以下代码可以通过特定的类属性中获取所有元素。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. 按**CTRL** + **空间**内部引号之间**getElementsByClassName**函数调用。

    ![GetElementsByClassName 函数显示 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "getElementsByClassName 函数显示 IntelliSense")

    *显示 IntelliSense getElementsByClassName 函数*

    > [!NOTE]
    > 请注意，IntelliSense 会显示项目样式表中定义的类。
11. 已使用以下代码创建的行替换为。

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. 之后将光标置于**au**在引号内**getElementsByTagName**函数，并按**CTRL** + **空间**.

    ![GetElementByTagName 方法显示 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "getElementByTagName 方法显示 IntelliSense")

    *GetElementsByTagName 方法显示 IntelliSense*
13. 选择**&quot;音频&quot;** 列表然后按**ENTER**。 结果如下图所示。

    ![检索音频元素](visual-studio-2013-web-tools/_static/image46.png "检索音频元素")

    *检索音频元素*
14. 在中**解决方案资源管理器**，右键单击**init.js**文件中**脚本**文件夹，然后选择**缩小 JavaScript 文件**从**Web Essentials**菜单。

    ![缩小 JavaScript 文件](visual-studio-2013-web-tools/_static/image47.png "缩小 JavaScript 文件")

    *缩小 JavaScript 文件*
15. 当系统提示你单击源文件更改时启用自动缩减**是**。

    ![启用自动缩小警告](visual-studio-2013-web-tools/_static/image48.png "启用自动缩小警告")

    *启用自动缩小警告*

    > [!NOTE]
    > **Init.min.js**将创建并添加作为的依赖项**init.js**文件。
    > 
    > ![创建 Init.min.js 文件](visual-studio-2013-web-tools/_static/image49.png "Init.min.js 文件创建")
    > 
    > *创建 Init.min.js 文件*
16. 打开**init.min.js**文件，请注意，缩小该文件。

    ![Init.min.js 文件内容](visual-studio-2013-web-tools/_static/image50.png "Init.min.js 文件内容")

    *Init.min.js 文件内容*
17. 在中**init.js**文件中，添加以下代码**getElementsByTagName**函数调用播放音频的所有元素。

    (代码段- *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. 单击**CTRL** + **S**保存该文件。 由于缩小的文件已打开，您将看到对话框，指出，源编辑器外修改该文件。 单击 **“是”**。

    ![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
19. 切换回**init.min.js**文件以验证该文件已更新使用新的代码。

    ![Init.min.js 文件已更新](visual-studio-2013-web-tools/_static/image52.png "Init.min.js 文件已更新")

    *Init.min.js 文件已更新*
20. 单击**浏览器链接刷新**按钮。
21. 后两个浏览器会刷新在上一任务中看到的音频播放机将开始自动播放。

    ![视图中包含的音频播放器](visual-studio-2013-web-tools/_static/image53.png "视图中包含的音频播放机")

    *视图中包含的音频播放器*

* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了如何：

- 使用新的 HTML 编辑器功能，这些功能包含在 Web Essentials 等丰富的 HTML5 代码代码段和处理编码
- 使用颜色选取器和浏览器矩阵工具提示等 Web Essentials 中包括的新 CSS 编辑器功能
- 使用 Web Essentials 等中提取到文件和智能感知中包括的所有 HTML 元素的新 JavaScript 编辑器功能
- 你的浏览器和 Visual Studio 中使用浏览器链接之间交换数据
