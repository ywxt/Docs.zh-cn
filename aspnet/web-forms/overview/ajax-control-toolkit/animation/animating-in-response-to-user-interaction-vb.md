---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 对进行动画处理以响应用户交互 (VB) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 动画可以星...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: e12467bfeb88c2ab9d1cfb866506e9e8e7f9ae25
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="1825a-104">对进行动画处理以响应用户交互 (VB)</span><span class="sxs-lookup"><span data-stu-id="1825a-104">Animating in Response To User Interaction (VB)</span></span>
====================
<span data-ttu-id="1825a-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1825a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1825a-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1825a-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="1825a-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="1825a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1825a-108">动画会自动启动，或可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="1825a-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="1825a-109">概述</span><span class="sxs-lookup"><span data-stu-id="1825a-109">Overview</span></span>

<span data-ttu-id="1825a-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="1825a-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1825a-111">动画会自动启动，或可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="1825a-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="1825a-112">步骤</span><span class="sxs-lookup"><span data-stu-id="1825a-112">Steps</span></span>

<span data-ttu-id="1825a-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="1825a-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="1825a-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="1825a-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="1825a-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="1825a-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="1825a-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="1825a-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="1825a-117">在`<Animations>`节点，有五种方法可以启动动画通过用户交互 (缺少的元素是`<OnLoad>`整个页面完全加载后将执行它):</span><span class="sxs-lookup"><span data-stu-id="1825a-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="1825a-118">`<OnClick>` （在控件上的鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="1825a-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="1825a-119">`<OnHoverOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="1825a-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="1825a-120">`<OnHoverOver>` (鼠标悬停在一个控件，停止`<OnHoverOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="1825a-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="1825a-121">`<OnMouseOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="1825a-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="1825a-122">`<OnMouseOver>` (鼠标悬停在一个控件，不停止`<OnMouseOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="1825a-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="1825a-123">在此方案中，`<OnClick>`使用。</span><span class="sxs-lookup"><span data-stu-id="1825a-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="1825a-124">当用户单击面板上时，它调整大小，并在同一时间淡出。</span><span class="sxs-lookup"><span data-stu-id="1825a-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


<span data-ttu-id="1825a-125">[![鼠标单击启动动画](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1825a-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="1825a-126">鼠标单击启动动画 ([单击以查看实际尺寸的图像](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1825a-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1825a-127">[上一页](picking-one-animation-out-of-a-list-vb.md)
> [下一页](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1825a-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
