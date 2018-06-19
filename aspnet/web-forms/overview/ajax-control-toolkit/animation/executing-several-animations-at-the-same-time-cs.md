---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 在同一时间 (C#) 执行几个动画 |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 它允许运行跌落造成的严重...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ecd822f7fa00a24e97b9aa14888798825624617
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869356"
---
<a name="executing-several-animations-at-the-same-time-c"></a><span data-ttu-id="dab88-104">在同一时间 (C#) 执行几个动画</span><span class="sxs-lookup"><span data-stu-id="dab88-104">Executing Several Animations at The Same Time (C#)</span></span>
====================
<span data-ttu-id="dab88-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dab88-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dab88-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="dab88-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)</span></span>

> <span data-ttu-id="dab88-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="dab88-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dab88-108">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="dab88-108">It allows to run several animations in a parallel fashion.</span></span>


## <a name="overview"></a><span data-ttu-id="dab88-109">概述</span><span class="sxs-lookup"><span data-stu-id="dab88-109">Overview</span></span>

<span data-ttu-id="dab88-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="dab88-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dab88-111">它允许以并行方式运行多个动画。</span><span class="sxs-lookup"><span data-stu-id="dab88-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="dab88-112">步骤</span><span class="sxs-lookup"><span data-stu-id="dab88-112">Steps</span></span>

<span data-ttu-id="dab88-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="dab88-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

<span data-ttu-id="dab88-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="dab88-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

<span data-ttu-id="dab88-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="dab88-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

<span data-ttu-id="dab88-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="dab88-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

<span data-ttu-id="dab88-117">在`<Animations>`节点，请使用`<OnLoad>`以运行动画，一旦页已完全加载。</span><span class="sxs-lookup"><span data-stu-id="dab88-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="dab88-118">通常情况下，`<OnLoad>`仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="dab88-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="dab88-119">动画框架允许你加入到一个使用多个动画`<Parallel>`元素。</span><span class="sxs-lookup"><span data-stu-id="dab88-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="dab88-120">中的所有动画`<Parallel>`在同一时间执行。</span><span class="sxs-lookup"><span data-stu-id="dab88-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="dab88-121">下面是有关可能的标记`AnimationExtender`控件，淡出以及调整面板大小在同一时间：</span><span class="sxs-lookup"><span data-stu-id="dab88-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

<span data-ttu-id="dab88-122">和确实： 运行此脚本时，面板会显示，然后调整大小时 (超过 threefolding 其宽度和 halfing 窗体的高度) 和在同一时间淡出。</span><span class="sxs-lookup"><span data-stu-id="dab88-122">And indeed: when you run this script, the panel is displayed, then resizes (more than threefolding its width and halfing its height) and fades out at the same time.</span></span>


<span data-ttu-id="dab88-123">[![面板是淡出和调整大小 （包括其内容，感谢浏览器的呈现引擎）](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dab88-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)</span></span>

<span data-ttu-id="dab88-124">面板是淡出和调整大小 （包括其内容，浏览器的呈现引擎感谢） ([单击以查看实际尺寸的图像](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="dab88-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dab88-125">[上一页](adding-animation-to-a-control-cs.md)
> [下一页](executing-several-animations-after-each-other-cs.md)</span><span class="sxs-lookup"><span data-stu-id="dab88-125">[Previous](adding-animation-to-a-control-cs.md)
[Next](executing-several-animations-after-each-other-cs.md)</span></span>
