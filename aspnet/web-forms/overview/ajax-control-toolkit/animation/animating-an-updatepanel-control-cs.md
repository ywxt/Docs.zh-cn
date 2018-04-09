---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 对进行动画处理 UpdatePanel 控件 (C#) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 内容...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5d8d5b9c3f15b39045b5e01b455bdddfc9443a24
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="127ae-104">对进行动画处理 UpdatePanel 控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="127ae-104">Animating an UpdatePanel Control (C#)</span></span>
====================
<span data-ttu-id="127ae-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="127ae-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="127ae-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="127ae-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="127ae-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="127ae-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="127ae-108">UpdatePanel 的内容，对于一个特殊的扩展程序添加存在很大程度依赖于动画 framework: UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="127ae-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="127ae-109">本教程演示如何为 UpdatePanel 设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="127ae-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="127ae-110">概述</span><span class="sxs-lookup"><span data-stu-id="127ae-110">Overview</span></span>

<span data-ttu-id="127ae-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="127ae-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="127ae-112">内容`UpdatePanel`，特殊的扩展程序存在很大程度依赖于动画 framework: `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="127ae-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="127ae-113">本教程演示如何设置此类动画`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="127ae-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="127ae-114">步骤</span><span class="sxs-lookup"><span data-stu-id="127ae-114">Steps</span></span>

<span data-ttu-id="127ae-115">第一步是像往常一样包括`ScriptManager`在页中，以便加载 ASP.NET AJAX 库，并可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="127ae-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="127ae-116">在此方案中动画将应用到 ASP.NET`Wizard`驻留在的 web 控件`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="127ae-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="127ae-117">三个 （任意） 的步骤提供足够的选项来触发回发：</span><span class="sxs-lookup"><span data-stu-id="127ae-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="127ae-118">所需的标记`UpdatePanelAnimationExtender`控件是非常类似于用于标记`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="127ae-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="127ae-119">在`TargetControlID`我们提供的属性`ID`的`UpdatePanel`要进行动画处理; 在`UpdatePanelAnimationExtender`控件，`<Animations>`元素包含动画的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="127ae-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="127ae-120">但是没有一个区别： 事件和事件处理程序是有限的相对于`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="127ae-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="127ae-121">有关`UpdatePanels`，只有两个其中存在：</span><span class="sxs-lookup"><span data-stu-id="127ae-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="127ae-122">`<OnUpdated>` UpdatePanel 何时已更新</span><span class="sxs-lookup"><span data-stu-id="127ae-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="127ae-123">`<OnUpdating>` UpdatePanel 启动更新</span><span class="sxs-lookup"><span data-stu-id="127ae-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="127ae-124">在此方案中，新内容的`UpdatePanel`（之后回发） 应淡入。</span><span class="sxs-lookup"><span data-stu-id="127ae-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="127ae-125">这是为此时必需的标记：</span><span class="sxs-lookup"><span data-stu-id="127ae-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="127ae-126">现在每次回发发生 UpdatePanel 中时，面板中的新内容淡入平稳。</span><span class="sxs-lookup"><span data-stu-id="127ae-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="127ae-127">[![下一步的向导步骤淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="127ae-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="127ae-128">下一步的向导步骤淡入 ([单击以查看实际尺寸的图像](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="127ae-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="127ae-129">[上一页](changing-an-animation-using-client-side-code-cs.md)
> [下一页](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="127ae-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
