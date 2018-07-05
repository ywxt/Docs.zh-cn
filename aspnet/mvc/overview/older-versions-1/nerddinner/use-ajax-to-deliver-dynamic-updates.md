---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 提供动态更新 |Microsoft Docs
author: microsoft
description: 步骤 10 实现支持登录的用户到 RSVP 其感兴趣的参加 dinner，使用基于 Ajax 的方法集成中 dinner 详细信息...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 789c9880dc43c5d15ee510d9856a4c4378019b71
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372325"
---
<a name="use-ajax-to-deliver-dynamic-updates"></a>使用 AJAX 提供动态更新
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 10 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 10 实现支持登录的用户到 RSVP 其感兴趣的参加晚宴，使用集成在 dinner 详细信息页内基于 Ajax 的方法。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner 步骤 10： 启用 Rsvp 的 AJAX 接受

让我们现在实现对其感兴趣的参加 dinner 的 RSVP 登录的用户的支持。 我们将启用此选项使用集成在 dinner 详细信息页内基于 AJAX 的方法。

### <a name="indicating-whether-the-user-is-rsvpd"></a>该值指示是否接受用户

用户可以访问 */Dinners/详细信息 / [id*] URL 即可查看有关特定 dinner 的详细信息：

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

操作方法的实现的 Details() 如下所示：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

若要实现的 RSVP 支持我们第一步将是将"IsUserRegistered(username)"帮助程序方法添加到我们的 Dinner 对象 （在我们之前生成的 Dinner.cs 分部类）。 此帮助器方法返回 true 或 false 具体取决于用户是否当前接受的 Dinner:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

然后，我们可以向 Details.aspx 视图模板来显示相应的消息，指示用户是否注册或不为事件添加以下代码：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

和现在的用户访问的 Dinner 他们注册时它们会看到此消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

和用户访问的 Dinner 他们尚未注册于他们将看到如下消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>实现注册操作方法

现在让我们添加必要的功能，使用户到 dinner 的 RSVP 从详细信息页。

若要实现这一点，我们将创建一个新"RSVPController"类 \Controllers 目录上右键单击并选择添加-&gt;控制器菜单命令。

我们将实现所需 id 作为参数 Dinner，检索相应的 Dinner 对象检查，以查看是否已登录的用户当前处于已注册，用户的列表，如果新 RSVPController 类中的"注册"操作方法不为其添加 RSVP 对象：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

请注意上面作为操作方法的输出，我们就会返回一个简单的字符串。 我们无法嵌入由视图模板中的将此消息，但由于太小，因此我们就使用 Content() 帮助器方法的控制器基类和类似上面的字符串消息返回。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>调用使用 AJAX RSVPForEvent 操作方法

我们将使用 AJAX 调用的 Register 操作方法从我们的详细信息视图。 实现此过程非常简单。 首先，我们将添加两个脚本库引用：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

第一个库引用的核心 ASP.NET AJAX 客户端脚本库。 此文件为大约 24 k （压缩） 的大小，并包含核心客户端 AJAX 功能。 第二个库包含将与 ASP.NET MVC 内置 AJAX 帮助器方法 （我们稍后将使用） 相集成的实用工具函数。

我们可以然后更新视图模板代码我们之前添加，以便而不是输出"您未注册此事件的"消息，我们改为呈现链接的推送时将执行调用我们的 RSVP 控制器上我们 RSVPForEvent 操作方法的 AJAX 调用和 RSVPs 用户：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

使用上面的 Ajax.ActionLink() 帮助器方法是内置的 ASP.NET MVC，类似于 Html.ActionLink() 帮助器方法不同之处在于而不是执行标准的导航则通过 AJAX 调用到操作方法时单击该链接。 更高版本，我们已在"回复"控制器上调用"注册"操作方法并将 DinnerID 作为"id"参数传递给它。 我们传递的最后一个 AjaxOptions 参数指示我们想要采取的操作方法从返回的内容并更新 HTML &lt;div&gt;其 id 是"rsvpmsg"页上的元素。

和现在当用户浏览到 dinner 他们未注册，但他们将看到它的 RSVP 的链接：

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

如果他们单击"此事件的 RSVP"链接时它们的 RSVP 控制器上，使得对注册操作方法的 AJAX 调用和完成后，他们将看到更新后的消息如下所示：

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

网络带宽和流量进行此调用时所涉及的是非常轻量。 当用户单击"此事件的 RSVP"链接时，对进行小的 HTTP POST 网络请求 */Dinners/Register/1*看起来像下面在网络的 URL:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

而只需是来自我们的 Register 操作方法的响应：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

此轻量调用速度快，甚至在慢速网络上将工作。

### <a name="adding-a-jquery-animation"></a>添加 jQuery 动画

我们实现的 AJAX 功能的工作也和快速。 有时它可能会发生如此之快，但是，用户可能无法发现已替换的 RSVP 链接为的新文本。 若要使的结果更明显，我们可以添加一个简单的动画，以突出更新消息。

默认情况下 ASP.NET MVC 项目模板包括 jQuery – Microsoft 还支持很好 （和非常受欢迎） 的开放源代码 JavaScript 库。 jQuery 提供了许多功能，包括一个很好的 HTML DOM 选择和效果库。

使用 jQuery，我们将首先添加对它的脚本引用。 因为我们要在我们的站点内使用 jQuery 的多个位置中，我们将我们 Site.master 主控页文件中添加脚本引用，以便所有页面可以都使用它。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*提示： 请确保已安装 VS 2008 SP1，使更加丰富的 JavaScript 文件 （包括 jQuery） 的 intellisense 支持的 JavaScript intellisense 修补程序。您可以下载它从： http://tinyurl.com/vs2008javascripthotfix*

通常使用 JQuery 编写的代码使用全局"$ （）"检索使用 CSS 选择器的一个或多个 HTML 元素的 JavaScript 方法。 例如， <em>$("#rsvpmsg")</em>选择 id 为 rsvpmsg，任何 HTML 元素时<em>$(".something")</em>会选择所有元素与"内容"CSS 类名称。 您还可以编写更高级的查询像"返回所有选中的单选按钮"使用下面的选择器查询： <em>$("输入 [@type= 单选] [@checked]")</em>。

选择元素后，可以对其执行操作，如隐藏这些调用方法： *$("#rsvpmsg").hide();*

对于我们的 RSVP 的方案，我们将定义一个名为"AnimateRSVPMessage"，选择"rsvpmsg"的简单的 JavaScript 函数&lt;div&gt;和及其文本内容的大小进行动画处理。 下面的代码启动小型的文本，然后会导致它以增加一 400 毫秒的时间段：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

我们可以然后布置要在我们的 AJAX 调用已成功完成它的名称传递给我们 Ajax.ActionLink() 帮助器方法之后调用此 JavaScript 函数 (通过 AjaxOptions"OnSuccess"事件属性):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

和现在时单击"此事件的 RSVP"链接和我们的 AJAX 调用成功完成后，发送的内容消息后将进行动画处理，并变得很大：

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

除了提供"OnSuccess"事件，AjaxOptions 对象公开 OnBegin、 OnFailure 和 OnComplete 事件可处理 （以及各种其他属性和有用的选项）。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>清理-重构出 RSVP 的分部视图

我们详细信息视图模板着手会稍有很长，哪些加班，就有点难以理解。 若要帮助提高代码可读性，让我们最后创建封装了所有我们详细信息页的 RSVP 视图代码的分部视图 – RSVPStatus.ascx –。

我们可以执行此操作通过右键单击 \Views\Dinners 文件夹，然后选择添加-&gt;查看菜单命令。 我们将它采用 Dinner 对象作为其强类型化的 ViewModel。 我们可以再复制/粘贴 RSVP 内容从 Details.aspx 视图到其中。

我们已经完成的让我们还创建另一个分部视图 – EditAndDeleteLinks.ascx-封装我们编辑和删除链接查看代码。 我们还将它采用 Dinner 对象作为其强类型视图模型，并复制/粘贴到其中我们 Details.aspx 视图中的编辑和删除逻辑。

我们详细信息视图模板可以然后只需包含在底部的两个 Html.RenderPartial() 方法调用：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

这会使代码更简洁、 更易阅读和维护。

### <a name="next-step"></a>下一步

让我们现在看一下如何我们可以进一步使用 AJAX，并向我们的应用程序添加交互式映射支持。

> [!div class="step-by-step"]
> [上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)
