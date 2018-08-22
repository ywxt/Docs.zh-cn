---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 对 UpdatePanel 控件 (C#) 进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 内容的...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3021da80635b8648d3119b939f2bdee77d858754
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830454"
---
<a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="70528-104">对 UpdatePanel 控件 (C#) 进行动画处理</span><span class="sxs-lookup"><span data-stu-id="70528-104">Animating an UpdatePanel Control (C#)</span></span>
====================
<span data-ttu-id="70528-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="70528-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="70528-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="70528-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="70528-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="70528-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="70528-108">UpdatePanel 的内容，一个特殊的扩展程序存在的严重依赖于此动画框架： UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="70528-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="70528-109">本教程演示如何为 UpdatePanel 设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="70528-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="70528-110">概述</span><span class="sxs-lookup"><span data-stu-id="70528-110">Overview</span></span>

<span data-ttu-id="70528-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="70528-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="70528-112">有关的内容`UpdatePanel`，一个特殊的扩展程序存在的严重依赖于此动画框架： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="70528-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="70528-113">本教程演示如何设置此类动画，以`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="70528-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="70528-114">步骤</span><span class="sxs-lookup"><span data-stu-id="70528-114">Steps</span></span>

<span data-ttu-id="70528-115">第一步是像往常一样包括`ScriptManager`页中，以便加载 ASP.NET AJAX 库，可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="70528-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="70528-116">在此方案中的动画将应用于 ASP.NET`Wizard`驻留在 web 控件`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="70528-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="70528-117">（任意） 的三个步骤提供足够的选项来触发回发：</span><span class="sxs-lookup"><span data-stu-id="70528-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="70528-118">所需的标记`UpdatePanelAnimationExtender`控件是非常类似于用于标记`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="70528-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="70528-119">在`TargetControlID`我们提供的特性`ID`的`UpdatePanel`进行动画处理; 内`UpdatePanelAnimationExtender`控件，`<Animations>`元素保留的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="70528-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="70528-120">但是还有一个区别： 事件和事件处理程序的数量是有限与`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="70528-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="70528-121">有关`UpdatePanels`，只有两个其中存在：</span><span class="sxs-lookup"><span data-stu-id="70528-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="70528-122">`<OnUpdated>` UpdatePanel 更新时</span><span class="sxs-lookup"><span data-stu-id="70528-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="70528-123">`<OnUpdating>` 当 UpdatePanel 启动更新</span><span class="sxs-lookup"><span data-stu-id="70528-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="70528-124">在此方案中，新的内容`UpdatePanel`（之后在回发） 应淡入。</span><span class="sxs-lookup"><span data-stu-id="70528-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="70528-125">这是为此，时必需的标记：</span><span class="sxs-lookup"><span data-stu-id="70528-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="70528-126">现在每次回发的 UpdatePanel 中发生时，新的面板内容淡入顺利。</span><span class="sxs-lookup"><span data-stu-id="70528-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="70528-127">[![淡入淡出下一步的向导步骤](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="70528-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="70528-128">淡入淡出下一步的向导步骤 ([单击此项可查看原尺寸图像](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="70528-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="70528-129">[上一页](changing-an-animation-using-client-side-code-cs.md)
> [下一页](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="70528-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
