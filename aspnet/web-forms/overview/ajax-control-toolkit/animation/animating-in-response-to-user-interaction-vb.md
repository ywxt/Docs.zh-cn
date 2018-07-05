---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 以响应用户交互 (VB) 进行动画处理 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 动画可以星型...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 4b774a058e715e4a98e767daf92886f24e627822
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815520"
---
<a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="d3df1-104">以响应用户交互 (VB) 进行动画处理</span><span class="sxs-lookup"><span data-stu-id="d3df1-104">Animating in Response To User Interaction (VB)</span></span>
====================
<span data-ttu-id="d3df1-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d3df1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d3df1-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d3df1-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="d3df1-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="d3df1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d3df1-108">动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="d3df1-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="d3df1-109">概述</span><span class="sxs-lookup"><span data-stu-id="d3df1-109">Overview</span></span>

<span data-ttu-id="d3df1-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="d3df1-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="d3df1-111">动画可以自动启动，也可能会触发由用户交互，例如通过使用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="d3df1-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="d3df1-112">步骤</span><span class="sxs-lookup"><span data-stu-id="d3df1-112">Steps</span></span>

<span data-ttu-id="d3df1-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="d3df1-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="d3df1-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="d3df1-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="d3df1-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="d3df1-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="d3df1-116">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="d3df1-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="d3df1-117">内`<Animations>`节点中，有五种方法来启动通过用户交互动画 (缺少的元素是`<OnLoad>`整个页面完全加载后执行):</span><span class="sxs-lookup"><span data-stu-id="d3df1-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="d3df1-118">`<OnClick>` （在控件上的鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="d3df1-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="d3df1-119">`<OnHoverOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="d3df1-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="d3df1-120">`<OnHoverOver>` (鼠标悬停在控件，停止`<OnHoverOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="d3df1-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="d3df1-121">`<OnMouseOut>` （鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="d3df1-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="d3df1-122">`<OnMouseOver>` (鼠标悬停在控件，不会停止`<OnMouseOut>`动画)</span><span class="sxs-lookup"><span data-stu-id="d3df1-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="d3df1-123">在此方案中，`<OnClick>`使用。</span><span class="sxs-lookup"><span data-stu-id="d3df1-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="d3df1-124">当用户单击的面板中时，它将调整大小并同时淡出。</span><span class="sxs-lookup"><span data-stu-id="d3df1-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


<span data-ttu-id="d3df1-125">[![鼠标单击启动动画](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d3df1-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="d3df1-126">鼠标单击启动动画 ([单击此项可查看原尺寸图像](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d3df1-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d3df1-127">[上一页](picking-one-animation-out-of-a-list-vb.md)
> [下一页](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d3df1-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
