---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 以响应用户交互 (C#) 进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画可以星型...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: 9de99b3194a5517047e40922d89c28e341ba8e20
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831712"
---
<a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="452b2-104">以响应用户交互 (C#) 进行动画处理</span><span class="sxs-lookup"><span data-stu-id="452b2-104">Animating in Response To User Interaction (C#)</span></span>
====================
<span data-ttu-id="452b2-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="452b2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="452b2-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="452b2-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="452b2-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="452b2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="452b2-108">动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="452b2-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="452b2-109">概述</span><span class="sxs-lookup"><span data-stu-id="452b2-109">Overview</span></span>

<span data-ttu-id="452b2-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="452b2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="452b2-111">动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="452b2-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="452b2-112">步骤</span><span class="sxs-lookup"><span data-stu-id="452b2-112">Steps</span></span>

<span data-ttu-id="452b2-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="452b2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="452b2-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="452b2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="452b2-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="452b2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="452b2-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="452b2-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="452b2-117">内`<Animations>`节点中，有五种方法来启动通过用户交互动画 (缺少的元素是`<OnLoad>`整个页面完全加载后执行):</span><span class="sxs-lookup"><span data-stu-id="452b2-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="452b2-118">`<OnClick>` （在控件上的鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="452b2-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="452b2-119">`<OnHoverOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="452b2-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="452b2-120">`<OnHoverOver>` (鼠标悬停在控件，停止`<OnHoverOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="452b2-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="452b2-121">`<OnMouseOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="452b2-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="452b2-122">`<OnMouseOver>` (鼠标悬停在控件，不会停止`<OnMouseOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="452b2-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="452b2-123">在此方案中，`<OnClick>`使用。</span><span class="sxs-lookup"><span data-stu-id="452b2-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="452b2-124">当用户单击的面板中时，它将调整大小并同时淡出。</span><span class="sxs-lookup"><span data-stu-id="452b2-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]


<span data-ttu-id="452b2-125">[![鼠标单击启动动画](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="452b2-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="452b2-126">鼠标单击启动动画 ([单击此项可查看原尺寸图像](animating-in-response-to-user-interaction-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="452b2-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="452b2-127">[上一页](picking-one-animation-out-of-a-list-cs.md)
> [下一页](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="452b2-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
