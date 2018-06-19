---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 在每个其他 (VB) 后执行几个动画 |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 它允许运行跌落造成的严重...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 700946b9f32c5ed2dcb8586e7c0e84d2238ff103
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873753"
---
<a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="990a4-104">在每个其他 (VB) 后执行几个动画</span><span class="sxs-lookup"><span data-stu-id="990a4-104">Executing Several Animations after Each Other (VB)</span></span>
====================
<span data-ttu-id="990a4-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="990a4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="990a4-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="990a4-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="990a4-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="990a4-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="990a4-108">它允许在其他后运行几个动画一个。</span><span class="sxs-lookup"><span data-stu-id="990a4-108">It allows to run several animations one after the other.</span></span>


## <a name="overview"></a><span data-ttu-id="990a4-109">概述</span><span class="sxs-lookup"><span data-stu-id="990a4-109">Overview</span></span>

<span data-ttu-id="990a4-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="990a4-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="990a4-111">它允许在其他后运行几个动画一个。</span><span class="sxs-lookup"><span data-stu-id="990a4-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="990a4-112">步骤</span><span class="sxs-lookup"><span data-stu-id="990a4-112">Steps</span></span>

<span data-ttu-id="990a4-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="990a4-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="990a4-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="990a4-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="990a4-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="990a4-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="990a4-116">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="990a4-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="990a4-117">在`<Animations>`节点，请使用`<OnLoad>`以运行动画，一旦页已完全加载。</span><span class="sxs-lookup"><span data-stu-id="990a4-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="990a4-118">通常情况下，`<OnLoad>`仅接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="990a4-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="990a4-119">动画框架允许你加入到一个使用多个动画`<Sequence>`元素。</span><span class="sxs-lookup"><span data-stu-id="990a4-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="990a4-120">中的所有动画`<Sequence>`执行后另一个。</span><span class="sxs-lookup"><span data-stu-id="990a4-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="990a4-121">下面是有关可能的标记`AnimationExtender`控件，首先进行更宽的面板以及增大或减小其高度：</span><span class="sxs-lookup"><span data-stu-id="990a4-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="990a4-122">当你运行此脚本，面板中第一次获得更宽且然后较小。</span><span class="sxs-lookup"><span data-stu-id="990a4-122">When you run this script, the panel first gets wider and then smaller.</span></span>


<span data-ttu-id="990a4-123">[![首先增加了宽度](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="990a4-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="990a4-124">第一次增加宽度 ([单击以查看实际尺寸的图像](executing-several-animations-after-each-other-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="990a4-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>


<span data-ttu-id="990a4-125">[![然后减少高度](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="990a4-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="990a4-126">然后减少高度 ([单击以查看实际尺寸的图像](executing-several-animations-after-each-other-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="990a4-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="990a4-127">[上一页](executing-several-animations-at-the-same-time-vb.md)
> [下一页](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="990a4-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
