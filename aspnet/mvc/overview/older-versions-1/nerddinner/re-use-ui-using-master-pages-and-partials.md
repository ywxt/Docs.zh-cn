---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 重复使用 UI 使用母版页和部分 |Microsoft Docs
author: microsoft
description: 步骤 7 中我们的视图模板以消除代码重复，使用分部视图模板和母版页探讨我们可以将应用 DRY 原则的方式。
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 961378d6d710c678a0cd223a5c31544f014ace7f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839589"
---
<a name="re-use-ui-using-master-pages-and-partials"></a>重复使用 UI 使用母版页和部分
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 7 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 7 中我们的视图模板以消除代码重复，使用分部视图模板和母版页探讨我们可以将应用"DRY 原则"的方式。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner 步骤 7： 分区和母版页

一个 ASP.NET MVC 包含内容的设计理念是"执行不自我重复"原则 （通常称为"模拟"）。 DRY 设计可帮助消除重复的代码和逻辑，最终使应用程序更快构建更容易维护。

我们已经看到 DRY 原则应用于多个我们 NerdDinner 的方案。 几个示例： 在我们的模型层，使它能够跨这两个编辑强制执行并在控制器; 中创建方案中实现我们的验证逻辑我们重新编辑、 详细信息和删除操作方法; 在使用"NotFound"查看模板我们使用我们的视图模板，而不需要显式指定的名称，当我们调用 View() 帮助器方法; 时使用的约定的命名模式我们重新将 DinnerFormViewModel 类用于这两个编辑和创建操作方案。

让我们现在看看我们可以将应用"DRY 原则"的方式在我们的视图模板，以及消除出现代码重复。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>重新访问我们的编辑和创建视图模板

目前我们正在使用两个不同的视图模板-"Edit.aspx"和"Create.aspx"– 显示我们 Dinner 窗体 UI。 这些快速直观的比较突出显示相似程度。 下面是创建窗体如下所示：

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

而以下是我们"的编辑"窗体如下所示：

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

不大同小异的程度有吗？ 以外的标题和页眉文本，窗体布局和输入控件是相同的。

如果我们打开"Edit.aspx"和"Create.aspx"视图模板，我们会发现它们包含相同的窗体布局和输入控件的代码。 这种重复意味着我们最终有两次只要我们引入或更改新的 Dinner 属性-不正常时，才进行更改。

### <a name="using-partial-view-templates"></a>使用分部视图模板

ASP.NET MVC 支持的功能来定义可用于封装视图呈现逻辑的页面的一个子部分的"分部视图"模板。 "分区"一次，定义视图呈现逻辑的有用方法，然后重新使用它在多个位置跨应用程序。

若要帮助"DRY 向上"我们 Edit.aspx 和 Create.aspx 视图模板重复数据删除，我们可以创建一个名为"DinnerForm.ascx"，用于封装窗体布局和输入的元素共有的分部视图模板。 我们将为此，我们/视图/Dinners 目录上右键单击并选择"添加-&gt;视图"菜单命令：

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

这将显示"添加视图"对话框。 我们将命名为我们想要创建"DinnerForm"，选择"创建分部视图"复选框在对话框中，并指示，我们会将它传递 DinnerFormViewModel 类的新视图：

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

当我们单击"添加"按钮时，Visual Studio 将创建一个新"DinnerForm.ascx"视图模板为我们"\Views\Dinners"目录中。

我们可以再复制/粘贴重复窗体布局 / 我们新的"DinnerForm.ascx"的分部视图模板中输入从我们 Edit.aspx/ Create.aspx 视图模板的控件代码：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

然后，我们可以更新我们编辑和创建的视图模板，调用 DinnerForm 局部模板，并消除窗体重复。 可以为此，我们调用 Html.RenderPartial("DinnerForm") 我们视图模板中：

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

您可以显式限定调用 Html.RenderPartial 时所需的部分模板的路径 (例如: ~ Views/Dinners/DinnerForm.ascx")。 在上述代码中，不过，我们是利用在 ASP.NET MVC 中的基于约定的命名模式，只需指定"DinnerForm"作为分部呈现的名称。 当我们执行此操作 ASP.NET MVC 将查找基于约定的 views 目录中的第一行 （这将是/视图/Dinners DinnersController)。 如果找不到局部模板那里它然后看它在 /Views/Shared 目录中。

只需分部视图的名称调用 Html.RenderPartial() 时，ASP.NET MVC 将传递到分部视图调用视图模板所使用的相同模型和 ViewData 字典对象。 此外，有的 Html.RenderPartial()，可以传递其他模型对象和/或要使用的分部视图的 ViewData 字典的重载的版本。 这非常有用的情况下，您只希望传递完整模型视图的子集。

| **端主题： 为什么&lt;%%&gt;而不是&lt;%= %&gt;？** |
| --- |
| 您可能已经注意到上面的代码具有细微优势之一是，我们将使用&lt;%%&gt;而不是阻止&lt;%= %&gt;阻止调用 Html.RenderPartial() 时。 &lt;%= %&gt;在 ASP.NET 中的块指示开发人员希望呈现指定的值 (例如： &lt;%="Hello"%&gt;将会呈现"Hello")。 &lt;%%&gt;块改为指示开发人员想要执行的代码，并且必须显式完成任何呈现的输出中的 (例如： &lt;%response.write("hello")%&gt;。 我们将使用的原因&lt;%%&gt;上述我们 Html.RenderPartial 代码块是因为 Html.RenderPartial() 方法不会返回一个字符串，而是将输出直接向调用的视图模板内容的输出流。 这样做效率由于性能原因，并且这样就无需创建一个临时的 （可能非常大） 字符串对象。 这可减少内存使用量并提高应用程序的整体吞吐量。 一个常见的错误时使用 Html.RenderPartial() 是忘了内时调用的末尾添加分号&lt;%%&gt;块。 例如，此代码将导致编译器错误： &lt;%html.renderpartial("dinnerform")%&gt;而是需要编写： &lt;%html.renderpartial("dinnerform"); %&gt;这是因为&lt;%%&gt;块都是自包含的代码语句，并使用 C# 代码语句需要使用分号终止时。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>使用分部视图模板以阐明代码

我们创建了"DinnerForm"的分部视图模板，以避免重复多个位置中的视图呈现逻辑。 这是创建分部视图模板的最常见原因。

有时仍最好创建分部视图，即使它们在一个位置被调用。 非常复杂的视图模板经常成为更易于阅读其视图呈现逻辑是提取和分区到一个或多也名为模板部分。

例如，考虑下面的代码段从我们的项目 （其中我们将稍后查看） 中的 Site.master 文件。 代码是相对简单直接读取 – 部分原因是因为用于显示登录/注销的逻辑链接顶部屏幕的右侧封装在"LogOnUserControl"部分中：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

每当您发现自己会混淆尝试了解视图模板中的 html/代码标记，请考虑是否它不会就更为明显，如果它的某些提取并重构为抢眼的分部视图。

### <a name="master-pages"></a>母版页

除了支持分部视图，ASP.NET MVC 还支持创建可用于定义常见的布局和站点的顶级 html 的"母版页"模板的功能。 内容的占位符控件然后添加到母版页来标识可重写或"由填充的"视图可更换部件区域。 这提供了非常有效 （DRY） 方法将一个通用布局应用跨应用程序。

默认情况下，新的 ASP.NET MVC 项目具有自动添加到它们的主页面模板。 此母版页是名为"Site.master"和存在于 \Views\Shared\ 文件夹：

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

默认 Site.master 文件类似于下面。 它定义外部站点，以及用于在顶部导航菜单的 html。 它包含两个可替换内容占位符控件 – 一个为标题，以及另一个用于应替换为一个页面的主要内容：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

我们已经创建了 NerdDinner 应用程序 （"列出"、"详细信息"、"编辑"、"创建"、"NotFound"等） 的视图模板的所有具有已在基于此 Site.master 模板。 通过默认情况下添加到顶部的"MasterPageFile"属性会指示这一点&lt;%@ 页 %&gt;指令时我们创建了我们使用"添加视图"对话框的视图：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

这意味着，我们可以更改 Site.master 内容，并且有所做的更改自动进行应用，而且使用时我们呈现任何我们视图模板。

让我们更新我们 Site.master 标头部分，以便我们的应用程序的标头"NerdDinner"而不是"My MVC Application"。 让我们还更新我们导航菜单使第一个选项卡是"查找 Dinner"（由了 HomeController 的 index （） 操作方法处理），然后添加名为"主机 Dinner"（由 DinnersController 的 create （） 操作方法处理） 的新选项卡：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

当我们保存 Site.master 文件并刷新浏览器将介绍我们标头更改显示于我们的应用程序中的所有视图。 例如：

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

且 */Dinners/编辑 / [id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>下一步

分区和主页面提供了非常灵活的选项，可使您能够完全组织视图。 您会发现它们可以帮助你避免重复视图内容 / 编码，并使视图模板更易于阅读和维护。

现在让我们重新访问我们之前生成的列表方案并启用可缩放的分页支持。

> [!div class="step-by-step"]
> [上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)
