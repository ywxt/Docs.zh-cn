---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 触发另一个控件 (VB) 的动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 通常情况下，启动...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 132f9f85eccabc890308984b9e78ed1d2212c57a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824660"
---
<a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="cf8dd-104">触发的动画中另一个控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="cf8dd-104">Triggering an Animation in another Control (VB)</span></span>
====================
<span data-ttu-id="cf8dd-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cf8dd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cf8dd-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="cf8dd-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="cf8dd-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf8dd-108">通常情况下，启动动画时触发用户与相同的控件的交互。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="cf8dd-109">但是也可以与一个控件，然后动画进行交互的另一个控件。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-109">It is however also possible to interact with one control and then animation another control.</span></span>


## <a name="overview"></a><span data-ttu-id="cf8dd-110">概述</span><span class="sxs-lookup"><span data-stu-id="cf8dd-110">Overview</span></span>

<span data-ttu-id="cf8dd-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="cf8dd-112">通常情况下，启动动画时触发用户与相同的控件的交互。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="cf8dd-113">但是也可以与一个控件，然后动画进行交互的另一个控件。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="cf8dd-114">步骤</span><span class="sxs-lookup"><span data-stu-id="cf8dd-114">Steps</span></span>

<span data-ttu-id="cf8dd-115">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="cf8dd-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="cf8dd-116">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="cf8dd-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="cf8dd-117">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="cf8dd-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="cf8dd-118">若要启动对面板进行动画处理，使用一个 HTML 按钮。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="cf8dd-119">请注意， `<input type="button" />` favoured 通过`<asp:Button />`因为我们不希望在回发，当用户单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="cf8dd-120">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="cf8dd-121">务必要设置`TargetControlID`按钮 （触发动画的元素） 的 id 不为面板 （要进行动画处理的元素） 的 ID</span><span class="sxs-lookup"><span data-stu-id="cf8dd-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="cf8dd-122">在`<Animations>`节点，照常位置动画。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="cf8dd-123">才能使这些更改面板，而不是按钮，设置`AnimationTarget`属性中的每个动画元素`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="cf8dd-124">值为`AnimationTarget`当然是在面板的 ID。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="cf8dd-125">这样一来，动画会发生与面板不与触发的按钮。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="cf8dd-126">下面是`AnimationExtender`对于此方案的标记：</span><span class="sxs-lookup"><span data-stu-id="cf8dd-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="cf8dd-127">请注意特殊单个动画的显示的顺序。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="cf8dd-128">首先，在动画运行后，获取停用按钮。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="cf8dd-129">由于没有任何`AnimationTarget`属性中`<EnableAction>`元素，此动画应用于原始控件: 按钮。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="cf8dd-130">接下来两个动画步骤应执行 parallelly (`<Parallel>`元素)。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-130">The next two animation steps shall be carried out parallelly (`<Parallel>` element).</span></span> <span data-ttu-id="cf8dd-131">两者都具有其`AnimationTarget`属性设置为`"Panel1"`，因此对面板中，而不是按钮进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="cf8dd-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>


<span data-ttu-id="cf8dd-132">[![按钮上的鼠标单击启动面板动画](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cf8dd-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="cf8dd-133">按钮上的鼠标单击启动面板动画 ([单击此项可查看原尺寸图像](triggering-an-animation-in-another-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cf8dd-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cf8dd-134">[上一页](disabling-actions-during-animation-vb.md)
> [下一页](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cf8dd-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
