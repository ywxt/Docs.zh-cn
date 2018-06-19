---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 提供动态更新 |Microsoft 文档
author: microsoft
description: 步骤 10 实现支持登录的用户的回复到其感兴趣的参加 dinner，使用基于 Ajax 的方法内 dinner 详细信息集成...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 7cea3ee2ec52261521941efac484e91a53f6310b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870175"
---
<a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="c9a9e-103">使用 AJAX 提供动态更新</span><span class="sxs-lookup"><span data-stu-id="c9a9e-103">Use AJAX to Deliver Dynamic Updates</span></span>
====================
<span data-ttu-id="c9a9e-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c9a9e-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c9a9e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="c9a9e-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c9a9e-106">这是一个免费的步骤 10 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c9a9e-107">步骤 10 实现支持登录的用户的回复到其感兴趣的参加 dinner，使用集成在 dinner 详细信息页内基于 Ajax 的方法。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="c9a9e-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="c9a9e-109">NerdDinner 步骤 10: AJAX 启用 RSVPs 接受</span><span class="sxs-lookup"><span data-stu-id="c9a9e-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="c9a9e-110">让我们现在可实现对登录的用户 RSVP 其感兴趣的参加 dinner 支持。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="c9a9e-111">我们将使用支持此集成在 dinner 详细信息页内的基于 AJAX 的方法。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="c9a9e-112">该值指示用户是否答复活动</span><span class="sxs-lookup"><span data-stu-id="c9a9e-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="c9a9e-113">用户可以访问 */Dinners/详细信息 / [id*] URL 以查看有关特定 dinner 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="c9a9e-114">操作方法实现 Details() 如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="c9a9e-115">若要实现的回复支持我们第一步是将"IsUserRegistered(username)"帮助程序方法添加到我们 Dinner 对象 （在我们之前生成的 Dinner.cs 分部类）。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="c9a9e-116">此帮助器方法返回 true 或 false，具体取决于是否用户当前答复活动为 Dinner:</span><span class="sxs-lookup"><span data-stu-id="c9a9e-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="c9a9e-117">然后我们可以将下面的代码添加到我们 Details.aspx 视图模板，以显示相应的消息，指示是否注册用户或不事件：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="c9a9e-118">然后，现在当用户访问为注册 Dinner 它们将看到以下消息：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="c9a9e-119">和当他们访问他们未注册为他们将看到 Dinner 以下信息：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="c9a9e-120">实现 Register 操作方法</span><span class="sxs-lookup"><span data-stu-id="c9a9e-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="c9a9e-121">让我们现在将添加必要的功能，使用户能够 dinner 的回复从详细信息页。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="c9a9e-122">若要实现这一点，我们将创建一个新"RSVPController"类 \Controllers 目录上右键单击并选择添加-&gt;控制器菜单命令。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="c9a9e-123">我们将实施的新的 RSVPController 类中作为自变量 Dinner 为采用 id，以检索相应的 Dinner 对象，将检查以确定如果登录的用户是当前在列表中的用户已注册的并且"注册"操作方法不将回复对象添加为它们：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="c9a9e-124">请注意上面作为操作方法的输出，我们就会返回一个简单的字符串。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="c9a9e-125">我们无法嵌入在视图模板 – 此消息，但因为它是太小只需将控制器基类和返回一个字符串消息类似上面使用的 Content() 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="c9a9e-126">调用使用 AJAX RSVPForEvent 操作方法</span><span class="sxs-lookup"><span data-stu-id="c9a9e-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="c9a9e-127">我们将使用 AJAX 调用 Register 操作方法从我们的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="c9a9e-128">实现这是这么简单。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="c9a9e-129">首先我们将添加两个脚本库引用：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="c9a9e-130">第一个库引用的核心 ASP.NET AJAX 客户端脚本库。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="c9a9e-131">此文件为大约 24 k （压缩） 的大小，并包含核心客户端 AJAX 功能。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="c9a9e-132">第二个库包含将与 ASP.NET MVC 的内置 AJAX 帮助器使用的方法 （我们将很快） 集成的实用工具函数。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="c9a9e-133">我们可以更新我们前面添加，以便而不是 outputing"你未注册此事件"消息，我们改为呈现一个链接，推送时查看模板代码执行时，将调用我们的回复控制器上我们 RSVPForEvent 操作方法的 AJAX 调用和 RSVPs 用户：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-133">We can then update the view template code we added earlier so that instead of outputing a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="c9a9e-134">上面使用的 Ajax.ActionLink() 帮助器方法是内置于 ASP.NET MVC，类似于 Html.ActionLink() 帮助器方法，只不过而不是执行标准导航它使 AJAX 调用对象的操作方法单击该链接时。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="c9a9e-135">更高版本，我们已调用"回复"控制器"注册"操作方法，并将 DinnerID 作为"id"参数传递给它。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="c9a9e-136">我们传递的最后一个 AjaxOptions 参数指示我们想要采取的操作方法从返回的内容并更新 HTML &lt;div&gt;其 id 是"rsvpmsg"页上的元素。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="c9a9e-137">而且，现在当用户浏览到 dinner 它们不为注册尚他们将看到它的回复的链接：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="c9a9e-138">如果他们单击"为此事件的回复"链接，它们将在回复控制器上，使 AJAX 调用对象的注册操作方法和在其完成后他们将看到更新的消息如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="c9a9e-139">网络带宽和流量时执行此 AJAX 调用涉及是真正轻量。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="c9a9e-140">当用户单击"为此事件的回复"链接时，对进行小的 HTTP POST 网络请求 */Dinners/Register/1*看起来与下面类似的网络的 URL:</span><span class="sxs-lookup"><span data-stu-id="c9a9e-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="c9a9e-141">只需为我们 Register 操作方法的响应：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="c9a9e-142">此轻型调用速度快，即使在慢速网络上将工作。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="c9a9e-143">添加 jQuery 动画</span><span class="sxs-lookup"><span data-stu-id="c9a9e-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="c9a9e-144">我们实现的 AJAX 功能可以很好地进行快速进行。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="c9a9e-145">有时也可能如此之快，不过，用户可能不到已替换的回复链接为使用新文本。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="c9a9e-146">若要使结果更明显我们可以添加以吸引人们关注更新消息的一个简单动画。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="c9a9e-147">默认情况下 ASP.NET MVC 项目模板包括 jQuery – Microsoft 也支持一个极好 （和非常受欢迎） 开源 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="c9a9e-148">jQuery 提供了大量功能，包括良好的 HTML DOM 选择和效果库。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="c9a9e-149">若要使用 jQuery 我们将先添加对它的脚本引用。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="c9a9e-150">因为我们要在我们的站点内使用 jQuery 在各种位置中的，我们将在我们 Site.master 主控页文件内添加脚本引用，以便所有页面可以都使用它。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="c9a9e-151">*提示： 请确保你已经安装了使 JavaScript 文件 （包括 jQuery） 的更好地 intellisense 支持的 VS 2008 SP1 的 JavaScript intellisense 修补程序。你可以下载它从： http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="c9a9e-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="c9a9e-152">通常使用 JQuery 编写的代码使用全局"$ （）"JavaScript 方法可检索一个或多个使用 CSS 选择器的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="c9a9e-153">例如， <em>$("#rsvpmsg")</em>选择 id 为 rsvpmsg，任何 HTML 元素时<em>$(".something")</em>将选择具有"内容"CSS 的所有元素类名。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-153">For example, <em>$("#rsvpmsg")</em> selects any HTML element with the id of rsvpmsg, while <em>$(".something")</em> would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="c9a9e-154">你还可以编写类似"返回所有选中的单选按钮"更多高级的查询使用类似的选择器查询： <em>$("输入 [@type= 单选] [@checked]")</em>。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: <em>$("input[@type=radio][@checked]")</em>.</span></span>

<span data-ttu-id="c9a9e-155">在你选择元素后，你可以对其执行操作，如隐藏它们调用方法： *$("#rsvpmsg").hide();*</span><span class="sxs-lookup"><span data-stu-id="c9a9e-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="c9a9e-156">对于我们的回复的方案，我们将定义一个名为"AnimateRSVPMessage"选择"rsvpmsg"的简单 JavaScript 函数&lt;div&gt;和进行动画处理其文本内容的大小。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="c9a9e-157">下面的代码启动小写的文本，然后原因它增加一 400 毫秒的时间段：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="c9a9e-158">我们可以然后网络型我们 AJAX 调用成功通过将其名称传递给我们 Ajax.ActionLink() 帮助器方法完成后调用此 JavaScript 函数 (通过 AjaxOptions"OnSuccess"事件属性):</span><span class="sxs-lookup"><span data-stu-id="c9a9e-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="c9a9e-159">和现在时单击"为此事件的回复"链接和我们 AJAX 调用已成功完成，发送的内容消息后将进行动画处理，并会变得大：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="c9a9e-160">除了提供"OnSuccess"事件，AjaxOptions 对象公开 OnBegin、 OnFailure 和 OnComplete 可以处理 （以及各种其他属性和有用的选项） 的事件。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="c9a9e-161">清理-重构出 RSVP 分部视图</span><span class="sxs-lookup"><span data-stu-id="c9a9e-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="c9a9e-162">我们的详细信息视图模板正在开始获取有点长，哪些加班将使其有点难以理解。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="c9a9e-163">为了帮助提高代码可读性，让我们最后创建封装了我们的详细信息页面的回复查看代码的所有分部视图 – RSVPStatus.ascx –。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="c9a9e-164">我们可以执行此操作通过右键单击 \Views\Dinners 文件夹，然后选择添加-&gt;查看菜单命令。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="c9a9e-165">我们将具有其采用将 Dinner 对象作为其强类型化视图模型。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="c9a9e-166">我们可以然后复制/粘贴的回复内容从到其中我们 Details.aspx 视图。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="c9a9e-167">一旦我们已完成该操作，让我们还创建另一个分部视图 – EditAndDeleteLinks.ascx-封装我们编辑和删除的链接查看代码。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="c9a9e-168">我们还将拥有它采用将 Dinner 对象作为其强类型视图模型，并复制/粘贴到其中我们 Details.aspx 视图的编辑和删除逻辑。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="c9a9e-169">我们详细信息查看模板，则只需包括在底部的两个 Html.RenderPartial() 方法调用：</span><span class="sxs-lookup"><span data-stu-id="c9a9e-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="c9a9e-170">这使代码更简洁读取和维护。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="c9a9e-171">下一步</span><span class="sxs-lookup"><span data-stu-id="c9a9e-171">Next Step</span></span>

<span data-ttu-id="c9a9e-172">让我们现在看一下我们可以进一步使用 AJAX 和将交互式映射支持添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c9a9e-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c9a9e-173">[上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="c9a9e-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
