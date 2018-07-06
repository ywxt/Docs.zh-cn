---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 动画取决于条件 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 无论动画是...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: cb08c330d6fbc86035a2f21ad382cc009411bcd6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808419"
---
<a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="7be07-104">动画取决于条件 (C#)</span><span class="sxs-lookup"><span data-stu-id="7be07-104">Animation Depending On a Condition (C#)</span></span>
====================
<span data-ttu-id="7be07-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7be07-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7be07-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7be07-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="7be07-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="7be07-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7be07-108">动画运行还取决于窗体的某些 JavaScript 代码中的条件。</span><span class="sxs-lookup"><span data-stu-id="7be07-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="7be07-109">概述</span><span class="sxs-lookup"><span data-stu-id="7be07-109">Overview</span></span>

<span data-ttu-id="7be07-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="7be07-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7be07-111">动画运行还取决于窗体的某些 JavaScript 代码中的条件。</span><span class="sxs-lookup"><span data-stu-id="7be07-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="7be07-112">步骤</span><span class="sxs-lookup"><span data-stu-id="7be07-112">Steps</span></span>

<span data-ttu-id="7be07-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="7be07-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="7be07-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="7be07-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="7be07-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="7be07-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="7be07-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="7be07-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="7be07-117">内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。</span><span class="sxs-lookup"><span data-stu-id="7be07-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="7be07-118">而不是一个常规的动画，`<Condition>`发挥作用的元素。</span><span class="sxs-lookup"><span data-stu-id="7be07-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="7be07-119">作为的值提供的 JavaScript 代码`ConditionScript`属性在运行时执行。</span><span class="sxs-lookup"><span data-stu-id="7be07-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="7be07-120">如果其计算结果为 true，动画执行，否则不。</span><span class="sxs-lookup"><span data-stu-id="7be07-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="7be07-121">以下标记提供了两个动画，每个正在执行时随机的情况下的 50%中。</span><span class="sxs-lookup"><span data-stu-id="7be07-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="7be07-122">因为可能仅在一个动画`<OnLoad>`，这两个`<Condition>`联接在一起使用的动画`<Sequence>`元素：</span><span class="sxs-lookup"><span data-stu-id="7be07-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="7be07-123">请注意，为小于号 (`<`) 中`ConditionScript`属性必须为转义 （）。</span><span class="sxs-lookup"><span data-stu-id="7be07-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="7be07-124">当您运行此脚本，无动画运行或两个空格，或同时执行操作。</span><span class="sxs-lookup"><span data-stu-id="7be07-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="7be07-125">[![在面板淡出而无需调整大小时，因此第二个动画运行第一个未](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7be07-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="7be07-126">在面板淡出而无需调整大小时，因此第二个动画运行第一个未 ([单击此项可查看原尺寸图像](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7be07-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7be07-127">[上一页](executing-several-animations-after-each-other-cs.md)
> [下一页](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7be07-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
