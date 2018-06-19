---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 选取列表 (C#) 之中的一个动画 |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 框架还允许...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2d4aac447fcdfbf296560091cfcdf5eb51997a7b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871657"
---
<a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="ff111-104">选取列表 (C#) 之中的一个动画</span><span class="sxs-lookup"><span data-stu-id="ff111-104">Picking One Animation Out Of a List (C#)</span></span>
====================
<span data-ttu-id="ff111-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ff111-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ff111-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ff111-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="ff111-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="ff111-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ff111-108">该框架还允许程序员也要选取列表之中的一个动画的动画，具体取决于一些 JavaScript 代码的计算。</span><span class="sxs-lookup"><span data-stu-id="ff111-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="ff111-109">概述</span><span class="sxs-lookup"><span data-stu-id="ff111-109">Overview</span></span>

<span data-ttu-id="ff111-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="ff111-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ff111-111">该框架还允许程序员也要选取列表之中的一个动画的动画，具体取决于一些 JavaScript 代码的计算。</span><span class="sxs-lookup"><span data-stu-id="ff111-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="ff111-112">步骤</span><span class="sxs-lookup"><span data-stu-id="ff111-112">Steps</span></span>

<span data-ttu-id="ff111-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="ff111-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="ff111-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="ff111-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="ff111-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="ff111-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="ff111-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="ff111-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="ff111-117">在`<Animations>`节点，请使用`<OnLoad>`以运行动画，一旦页已完全加载。</span><span class="sxs-lookup"><span data-stu-id="ff111-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="ff111-118">而不是一个正则动画，`<Case>`元素派上用场。</span><span class="sxs-lookup"><span data-stu-id="ff111-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="ff111-119">计算其 SelectScript 属性的值;返回值必须是数字。</span><span class="sxs-lookup"><span data-stu-id="ff111-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="ff111-120">根据此数量，其中一个内子动画&lt;用例&gt;执行。</span><span class="sxs-lookup"><span data-stu-id="ff111-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="ff111-121">例如，如果 SelectScript 计算结果为 2，该控件工具包将运行中的第三个动画&lt;用例&gt;（计数 0 开始）。</span><span class="sxs-lookup"><span data-stu-id="ff111-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="ff111-122">下面的标记定义三个子动画： 调整大小的宽度、 高度，调整大小和淡出。JavaScript 代码 (`Math.floor(3 * Math.random())`) 然后选取介于 0 和 2，以便的三个动画之一运行：</span><span class="sxs-lookup"><span data-stu-id="ff111-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


<span data-ttu-id="ff111-123">[![可能的三个动画之一: 面板获取更宽](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ff111-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="ff111-124">可能的三个动画之一: 面板获取更宽 ([单击以查看实际尺寸的图像](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ff111-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ff111-125">[上一页](animation-depending-on-a-condition-cs.md)
> [下一页](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ff111-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>
