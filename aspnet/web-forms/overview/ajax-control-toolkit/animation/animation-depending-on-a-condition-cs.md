---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 根据条件 (C#) 的动画 |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 动画是否...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: b530239e76654bc68a8fa6ac900a20df1d5699b0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="8e5d5-104">动画根据条件 (C#)</span><span class="sxs-lookup"><span data-stu-id="8e5d5-104">Animation Depending On a Condition (C#)</span></span>
====================
<span data-ttu-id="8e5d5-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8e5d5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8e5d5-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8e5d5-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="8e5d5-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8e5d5-108">动画是否运行或不可以还依赖于某些 JavaScript 代码形式的条件。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="8e5d5-109">概述</span><span class="sxs-lookup"><span data-stu-id="8e5d5-109">Overview</span></span>

<span data-ttu-id="8e5d5-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8e5d5-111">动画是否运行或不可以还依赖于某些 JavaScript 代码形式的条件。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8e5d5-112">步骤</span><span class="sxs-lookup"><span data-stu-id="8e5d5-112">Steps</span></span>

<span data-ttu-id="8e5d5-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="8e5d5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="8e5d5-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="8e5d5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="8e5d5-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="8e5d5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="8e5d5-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="8e5d5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="8e5d5-117">在`<Animations>`节点，请使用`<OnLoad>`以运行动画，一旦页已完全加载。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="8e5d5-118">而不是一个正则动画，`<Condition>`元素派上用场。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="8e5d5-119">作为值提供的 JavaScript 代码`ConditionScript`在运行时执行属性。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="8e5d5-120">如果其计算结果为 true 时，动画将执行，否则不。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="8e5d5-121">以下标记提供了两个动画，每个要在 50%的情况下在随机时执行。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="8e5d5-122">因为可能只在一个动画`<OnLoad>`，这两个`<Condition>`一起使用来联接动画`<Sequence>`元素：</span><span class="sxs-lookup"><span data-stu-id="8e5d5-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="8e5d5-123">请注意，小于号 (`<`) 中`ConditionScript`属性必须是转义 （）。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="8e5d5-124">当你运行此脚本，没有动画运行或这两个空格，或同时执行操作。</span><span class="sxs-lookup"><span data-stu-id="8e5d5-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="8e5d5-125">[![面板淡出而不调整大小，因此第二个动画运行，第一个未](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8e5d5-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="8e5d5-126">面板淡出而不调整大小，因此第二个动画运行，第一个未 ([单击以查看实际尺寸的图像](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8e5d5-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8e5d5-127">[上一页](executing-several-animations-after-each-other-cs.md)
> [下一页](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8e5d5-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
