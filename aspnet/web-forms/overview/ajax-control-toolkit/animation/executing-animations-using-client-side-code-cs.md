---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: 执行动画使用客户端代码 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画执行中...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 5dc5c0b49a3530988bf42d6d632a061622f0a217
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824457"
---
<a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="ac782-104">使用客户端代码 (C#) 执行动画</span><span class="sxs-lookup"><span data-stu-id="ac782-104">Executing Animations Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="ac782-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ac782-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ac782-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ac782-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="ac782-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="ac782-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ac782-108">此外可能使用自定义客户端的 JavaScript 代码会触发动画执行。</span><span class="sxs-lookup"><span data-stu-id="ac782-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="ac782-109">概述</span><span class="sxs-lookup"><span data-stu-id="ac782-109">Overview</span></span>

<span data-ttu-id="ac782-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="ac782-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ac782-111">此外可能使用自定义客户端的 JavaScript 代码会触发动画执行。</span><span class="sxs-lookup"><span data-stu-id="ac782-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ac782-112">步骤</span><span class="sxs-lookup"><span data-stu-id="ac782-112">Steps</span></span>

<span data-ttu-id="ac782-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="ac782-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="ac782-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="ac782-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="ac782-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="ac782-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="ac782-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="ac782-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="ac782-117">内`<Animations>`节点，请使用`<OnClick>`运行动画一次用户单击的面板。</span><span class="sxs-lookup"><span data-stu-id="ac782-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="ac782-118">添加两个动画 parallelly 执行：</span><span class="sxs-lookup"><span data-stu-id="ac782-118">Add two animations to be executed parallelly:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="ac782-119">为了演示目的，此动画 （和使用控件工具包创建的任何其他动画） 执行该页面运行后，使用 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="ac782-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="ac782-120">我们首先需要访问`AnimationExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="ac782-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="ac782-121">ASP.NET AJAX 库提供了`$find()`此任务的函数：</span><span class="sxs-lookup"><span data-stu-id="ac782-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="ac782-122">`AnimationExtender`控件公开一个丰富的 API，包括名称与在 XML 标记中使用的事件处理程序方法： `OnClick()`， `OnLoad()`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="ac782-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="ac782-123">例如，调用`OnClick()`方法将执行内的动画`<OnClick>`元素的`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="ac782-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="ac782-124">下面是模拟的面板中单击了页面完全加载后的完整客户端的 JavaScript 代码，请注意，`pageLoad()`都包括的 JavaScript 库一直和函数名称使用它在由调用 ASP.NET AJAX 一次页面加载。</span><span class="sxs-lookup"><span data-stu-id="ac782-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


<span data-ttu-id="ac782-125">[![动画立即运行而无需单击鼠标](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ac782-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="ac782-126">动画立即运行不带鼠标单击 ([单击此项可查看原尺寸图像](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ac782-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac782-127">[上一页](modifying-animations-from-the-server-side-cs.md)
> [下一页](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ac782-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>
