---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 执行动画使用客户端代码 (VB) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 动画执行中...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: e2b8c499edaccc70d439a576feb80e91cb28c1c7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="60a9d-104">执行动画使用客户端代码 (VB)</span><span class="sxs-lookup"><span data-stu-id="60a9d-104">Executing Animations Using Client-Side Code (VB)</span></span>
====================
<span data-ttu-id="60a9d-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="60a9d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="60a9d-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="60a9d-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="60a9d-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="60a9d-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="60a9d-108">此外可能使用自定义客户端 JavaScript 代码会触发动画执行。</span><span class="sxs-lookup"><span data-stu-id="60a9d-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="60a9d-109">概述</span><span class="sxs-lookup"><span data-stu-id="60a9d-109">Overview</span></span>

<span data-ttu-id="60a9d-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="60a9d-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="60a9d-111">此外可能使用自定义客户端 JavaScript 代码会触发动画执行。</span><span class="sxs-lookup"><span data-stu-id="60a9d-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="60a9d-112">步骤</span><span class="sxs-lookup"><span data-stu-id="60a9d-112">Steps</span></span>

<span data-ttu-id="60a9d-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="60a9d-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="60a9d-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="60a9d-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="60a9d-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="60a9d-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="60a9d-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="60a9d-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="60a9d-117">在`<Animations>`节点，请使用`<OnClick>`运行动画一次用户单击面板上。</span><span class="sxs-lookup"><span data-stu-id="60a9d-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="60a9d-118">添加两个动画 parallelly 执行：</span><span class="sxs-lookup"><span data-stu-id="60a9d-118">Add two animations to be executed parallelly:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="60a9d-119">为了演示，此动画 （和使用控件工具包创建的任何其他动画） 将被执行后页将运行使用 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="60a9d-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="60a9d-120">我们首先需要访问`AnimationExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="60a9d-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="60a9d-121">ASP.NET AJAX 库提供了`$find()`对此任务的函数：</span><span class="sxs-lookup"><span data-stu-id="60a9d-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="60a9d-122">`AnimationExtender`控件可公开一个丰富 API，包括使用名称相同的 XML 标记中使用的事件处理程序方法： `OnClick()`， `OnLoad()`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="60a9d-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="60a9d-123">例如，调用`OnClick()`方法执行内的动画`<OnClick>`元素`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="60a9d-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="60a9d-124">下面是模拟的面板上，单击页面完全加载后的完整客户端 JavaScript 代码，请注意，`pageLoad()`它由调用 ASP.NET AJAX 一次页使用函数名称和所有包含库已的 JavaScript加载。</span><span class="sxs-lookup"><span data-stu-id="60a9d-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]


<span data-ttu-id="60a9d-125">[![动画运行立即，而无需单击鼠标](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="60a9d-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="60a9d-126">动画会立即，运行没有鼠标单击 ([单击以查看实际尺寸的图像](executing-animations-using-client-side-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="60a9d-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60a9d-127">[上一页](modifying-animations-from-the-server-side-vb.md)
> [下一页](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="60a9d-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
