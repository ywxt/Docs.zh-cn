---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: 了解 ASP.NET AJAX UpdatePanel 触发器 |Microsoft Docs
author: scottcate
description: Visual Studio 中的标记编辑器中工作时，你可能会注意到 （从智能感知） 有两个 UpdatePanel 控件的子元素。 以下值时的一个...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2008
ms.topic: article
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: 180491b6aee188a9dca750d6d325217f1ad5212c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363716"
---
<a name="understanding-aspnet-ajax-updatepanel-triggers"></a>了解 ASP.NET AJAX UpdatePanel 触发器
====================
通过[Scott Cate](https://github.com/scottcate)

[下载 PDF](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio 中的标记编辑器中工作时，你可能会注意到 （从智能感知） 有两个 UpdatePanel 控件的子元素。 其中之一是触发器元素，它指定页 （或用户控件，如果您正在使用它） 上的控件，将触发该元素所在的 UpdatePanel 控件部分呈现。


## <a name="introduction"></a>介绍

Microsoft 的 ASP.NET 技术带来了面向对象和事件驱动的编程模型，并将其与已编译的代码的好处结合在一起。 但是，其服务器端处理模型有几个缺点固有的技术，其中很多可以通过 Microsoft ASP.NET 3.5 AJAX Extensions 中包含的新功能进行寻址。 使用这些扩展，许多新的丰富的客户端功能，而无需整页刷新，通过客户端脚本 （包括 ASP.NET 分析 API） 和广泛的客户端 API 访问 Web 服务的功能包括部分呈现的页面用于镜像许多 ASP.NET 服务器端控件集所示的控制方案。

本白皮书探讨 ASP.NET AJAX 的 XML 触发器功能`UpdatePanel`组件。 XML 触发器提供精细的控制可能会导致特定的 UpdatePanel 控件的部分呈现的组件。

此白皮书基于 Beta 2 版本的.NET Framework 3.5 和 Visual Studio 2008。 ASP.NET AJAX Extensions，以前针对 ASP.NET 2.0 中，外接程序程序集现已集成到.NET Framework 基类库。 本白皮书还假定你将使用 Visual Studio 2008 中，不 Visual Web Developer 速成版，并将提供根据 Visual Studio 的用户界面的演练 （尽管将完全兼容而不考虑代码列表开发环境）。

## <a name="triggers"></a>*触发器*

对于给定的 UpdatePanel，默认情况下，触发器会自动包括调用的回发，包括 （例如） 文本框控件，具有任何子控件及其`AutoPostBack`属性设置为**true**。 但是，触发器也可以包含以声明方式使用标记;这是在`<triggers>`UpdatePanel 控件声明的部分。 尽管可以通过访问触发器`Triggers`集合属性，则建议 （例如，如果控件在设计时不可用） 注册在运行时的任何部分呈现触发器使用`RegisterAsyncPostBackControl(Control)`方法ScriptManager 对象为您的页面，在`Page_Load`事件。 请记住，页是无状态，因此你应重新注册这些控件每次创建它们。

自动子触发器包含也可禁用 （以便创建回发的子控件不会自动触发部分呈现） 通过设置`ChildrenAsTriggers`属性设置为**false**。 这样可以最大的灵活性分配哪些特定控件可能调用页呈现，并建议，以便开发人员将参加来响应某个事件，而不是处理可能会出现任何事件。

请注意，当 UpdatePanel 控件嵌套时，如果 UpdateMode 设置为**条件**，如果触发 UpdatePanel 的子级，但父无效，则仅将刷新 UpdatePanel 的子级。 但是，如果父 UpdatePanel 刷新，然后子 UpdatePanel 也会刷新。

## <a name="the-lttriggersgt-element"></a>*&lt;触发器&gt;元素*

Visual Studio 中的标记编辑器中工作时，你可能会注意到 （从智能感知） 有两个子元素的`UpdatePanel`控件。 最常见的元素是`<ContentTemplate>`元素，它实质上是封装将持有的更新面板的内容 （我们要为其启用部分呈现的内容）。 其他元素是`<Triggers>`元素，它指定页 （或用户控件，如果您正在使用它） 上的控件，将触发 UpdatePanel 控件在其中的部分呈现&lt;触发器&gt;元素驻留。

`<Triggers>`元素可以包含两个子节点的任意数量每个：`<asp:AsyncPostBackTrigger>`和`<asp:PostBackTrigger>`。 它们都接受两个属性`ControlID`和`EventName`，可以指定封装的当前单位中的任何控件 （例如，UpdatePanel 控件位于 Web 用户控件内，如果您不应尝试在引用的控件用户控件将在其驻留的页确定）。

`<asp:AsyncPostBackTrigger>`元素是特别有用，因为它可以为目标的子级作为存在的控件中的任何事件*任何*UpdatePanel 控件封装，而不仅仅是此触发器在其下的子 UpdatePanel 单位. 因此，可以进行的任何控件，以触发部分页面更新。

同样，`<asp:PostBackTrigger>`元素可用于的触发器部分页面呈现，但需要完整往返服务器。 此触发器元素还可用于控制将否则通常会触发部分页面呈现时强制执行整页呈现器 (例如，当`Button`控件中存在`<ContentTemplate>`UpdatePanel 控件元素)。 同样，PostBackTrigger 元素可以指定是在当前的单元中封装任何 UpdatePanel 控件的子级的任何控件。

## <a name="lttriggersgt-element-reference"></a>*&lt;触发器&gt;元素引用*

*标记后代：*

| **标记** | **说明** |
| --- | --- |
| &lt;asp:AsyncPostBackTrigger&gt; | 指定控件并将导致部分页面更新的 UpdatePanel，其中包含此触发器引用的事件。 |
| &lt;asp:PostBackTrigger&gt; | 指定的控件和事件将导致整页更新 （整页刷新）。 此标记可用于强制完全刷新时控件否则会触发部分呈现。 |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*演练： 跨 UpdatePanel 触发器*

1. 使用设置为启用部分呈现 ScriptManager 对象创建一个新的 ASP.NET 页面。 将两个 Updatepanel 添加到此页-在第一个，包括 Label 控件 (Label1) 和两个按钮控件 （Button1 和 Button2）。 应该在 Button1 单击此项可同时更新和 Button2 应显示单击此项可更新，或类似。 在第二个 UpdatePanel，包括仅标签控件 (Label2)，但其 ForeColor 属性设置为默认值对其进行区分以外。
2. 这两个 UpdatePanel 标记的 UpdateMode 属性设置**条件**。

**列表 1: default.aspx 标记：** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. 在 Button1 单击事件处理程序，设置 Label1.Text 和 Label2.Text 为有依赖于时间的 （例如 DateTime.Now.ToLongTimeString())。 Button2 的单击事件处理程序，将仅 Label1.Text 设为依赖于时间的值。

**列表 2： 代码隐藏文件 default.aspx.cs 中 （剪裁）：** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. 按 F5 生成并运行项目。 请注意，当您单击更新同时面板，这两个标签将更改属性。但是，当您单击更新此面板，仅 Label1 更新。


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))


## <a name="under-the-hood"></a>*揭秘*

利用我们刚构建的示例，我们可以看看 ASP.NET AJAX 的作用以及我们 UpdatePanel 跨面板触发器的工作原理。 若要执行此操作，我们将使用生成的页源 HTML，以及使用它，调用 FireBug-Mozilla Firefox 扩展我们可以轻松地检查 AJAX 回发。 我们将使用由 Lutz Roeder 的.NET Reflector 工具。 这两种工具是免费提供联机，并可使用 internet 搜索找到。

检查页的源代码演示几乎没什么特别之;UpdatePanel 控件呈现为`<div>`容器，并且我们可以看到脚本资源包含提供由`<asp:ScriptManager>`。 也有一些新 AJAX 特定的调用到 PageRequestManager 内部的 AJAX 客户端脚本库。 最后，我们看到两个 UpdatePanel 容器-一个用于呈现`<input>`具有两个按钮`<asp:Label>`控件呈现为`<span>`容器。 （如果您检查 DOM 树在 FireBug 中的，您将注意到标签灰显以指示不能发出可见内容）。

单击更新此面板按钮，并注意顶部 UpdatePanel 将与当前服务器时间一起更新。 在 FireBug 中，选择控制台选项卡，以便你可以检查请求。 首先检查 POST 请求参数：


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))


请注意，UpdatePanel 已指明服务器端 AJAX 代码到精确的控件树已触发通过 ScriptManager1 参数：`Button1`的`UpdatePanel1`控件。 现在，单击更新两个面板按钮。 然后，检查响应，可看到竖线分隔的一系列变量在一个字符串; 中设置具体而言，我们看到顶部 UpdatePanel， `UpdatePanel1`，具有整个其发送到浏览器的 HTML。 AJAX 客户端脚本库替换 UpdatePanel 的原始 HTML 内容使用新的内容通过`.innerHTML`属性，因此，服务器将从为 HTML 的服务器发送更改的内容。

现在，单击更新两个面板按钮并检查来自服务器的结果。 结果是非常类似-这两个 Updatepanel 从服务器接收新的 html 代码。 与上一个回调，一样发送更多页面状态。

我们可以看到，因为没有特殊的代码用来执行 AJAX 回发，AJAX 客户端脚本库就能够截获窗体回发而无需任何其他代码。 服务器控件，以便它们不会自动提交窗体-ASP.NET 自动插入代码窗体验证和状态，主要通过自动脚本资源包含，PostBackOptions 类来实现自动利用 JavaScript和 ClientScriptManager 类。

例如，考虑一个复选框控件;检查在.NET Reflector 类反汇编。 为此，请确保在 System.Web 程序集已打开，并导航到`System.Web.UI.WebControls.CheckBox`类中，打开`RenderInputTag`方法。 检查的条件查找`AutoPostBack`属性：


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))


当在上启用自动回发`CheckBox`控制 （通过将 AutoPostBack 属性是否均为 true），所产生的`<input>`标记的因此呈现使用 ASP.NET 事件处理脚本在其`onclick`属性。 窗体的提交，然后，利用拦截，ASP.NET AJAX 注入到页 nonintrusively，帮助避免所有潜在的重大更改，可能出现的使用可能不精确的字符串替换。 此外，这使得*任何*自定义 ASP.NET 控件，以利用功能的 ASP.NET AJAX 无需任何其他代码以支持其使用 UpdatePanel 容器中的。

`<triggers>`功能对应于初始化 PageRequestManager 调用中的值\_updateControls （请注意，ASP.NET AJAX 客户端脚本库使用约定，该方法、 事件和字段名称以用下划线标记为内部，因此它们不能在库自身以外使用）。 使用它，我们可以观察到哪些控件旨在导致 AJAX 回发。

例如，让我们添加到页上，完全，使一个 Updatepanel 之外的控件并保留一个 UpdatePanel 内的两个其他控件。 我们将添加上部 UpdatePanel 内的复选框控件和列表中定义的颜色数与删除 DropDownList。 以下是新标记：

**代码清单 3： 新的标记**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

而以下是新的代码隐藏：

**列表 4： 代码隐藏文件**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

此页背后的理念是，下拉列表中选择一个三种颜色以显示第二个标签、 复选框确定它是否以粗体显示，和标签显示日期，以及时间。 复选框并不会导致 AJAX 更新，但应下拉列表，即使它不位于 UpdatePanel 中也是如此。


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([单击此项可查看原尺寸图像](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))


很明显在上面的屏幕截图，最新的按钮被单击时右侧的按钮更新此面板中，更新此订阅顶部时间独立于的底部时间。 日期也关闭了之间次单击，如日期是在底部标签中可见。 最后感兴趣的是底部标签的颜色： 它比标签的文本，演示，控件状态很重要，最近已更新，用户希望它将保留通过 AJAX 回发。 *但是*，不更新的时间。 时间已自动重新填充在的暂留\_\_时在服务器上重新呈现该控件时，ASP.NET 运行时所解释的页的视图状态字段。 ASP.NET AJAX 服务器代码中不能识别控件的方法在其中更改状态;它只需重新填充从视图状态，然后运行相应的事件。

它应前面所指出的但是，，具有我初始化页内的时间\_Load 事件中，时间会有已正确增加。 因此，开发人员应慎重考虑，将相应的代码运行在相应的事件处理程序，并避免使用页面\_加载时应适合使用控件事件处理程序。

## <a name="summary"></a>总结

ASP.NET AJAX 扩展 UpdatePanel 控件是用途多样，并可以使用多种方法来确定应将导致其更新的控件事件。 它支持子控件，通过自动更新，但也可以响应的页面上的其他位置的控件事件。

若要减少潜在的服务器处理负载，则建议`ChildrenAsTriggers`UpdatePanel 属性设置为`false`，事件会选择到而不是默认情况下包括和。 这还可以防止不需要的任何事件导致可能不需要的效果，包括验证和更改的输入字段。 这些类型的错误可能很难隔离，因为该页给用户，会更新以透明方式和原因因此可能不易察觉。

通过检查 ASP.NET AJAX 窗体的内部工作机制发布拦截模型，我们能够确定它利用 ASP.NET 已提供的框架。 这样，它将保留与控件使用同一个框架，设计的最大兼容性并干扰最少为页面编写任何其他 javascript。

## <a name="bio"></a>个人简介

Rob Paveza 是 Terralever 的高级.NET 应用程序开发人员 ([www.terralever.com](http://www.terralever.com))，在 Tempe，AZ.领先的交互式市场营销公司 他可以到达[ robpaveza@gmail.com ](mailto:robpaveza@gmail.com)，和他的博客位于[ http://geekswithblogs.net/robp/ ](http://geekswithblogs.net/robp/)。

Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。 可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一页](understanding-partial-page-updates-with-asp-net-ajax.md)
> [下一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
