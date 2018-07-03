---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 多个动画逐一执行 (C#) |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它允许运行跌落造成的严重...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: 49d33ee28984981c7757f14fe7c16fb2dc8f744e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362146"
---
<a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="9a8aa-104">多个动画逐一执行 (C#)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-104">Executing Several Animations after Each Other (C#)</span></span>
====================
<span data-ttu-id="9a8aa-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9a8aa-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="9a8aa-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9a8aa-108">它允许在它们运行多个动画一个。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-108">It allows to run several animations one after the other.</span></span>


<span data-ttu-id="9a8aa-109">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="9a8aa-110">它允许在它们运行多个动画一个。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="9a8aa-111">步骤</span><span class="sxs-lookup"><span data-stu-id="9a8aa-111">Steps</span></span>

<span data-ttu-id="9a8aa-112">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="9a8aa-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="9a8aa-113">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="9a8aa-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="9a8aa-114">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="9a8aa-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="9a8aa-115">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="9a8aa-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="9a8aa-116">内`<Animations>`节点，请使用`<OnLoad>`页面完全加载后运行动画。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="9a8aa-117">通常情况下，`<OnLoad>`只接受一个动画。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="9a8aa-118">此动画框架允许你联接为一个，并使用多个动画`<Sequence>`元素。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="9a8aa-119">中的所有动画`<Sequence>`是执行一个接一个。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="9a8aa-120">下面是有关可能的标记`AnimationExtender`控件，首先进行更广泛的面板和增大或减小其高度：</span><span class="sxs-lookup"><span data-stu-id="9a8aa-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="9a8aa-121">当您运行此脚本，面板第一次获得更宽且然后较小。</span><span class="sxs-lookup"><span data-stu-id="9a8aa-121">When you run this script, the panel first gets wider and then smaller.</span></span>


<span data-ttu-id="9a8aa-122">[![第一次增加宽度](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="9a8aa-123">第一次增加宽度 ([单击此项可查看原尺寸图像](executing-several-animations-after-each-other-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9a8aa-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>


<span data-ttu-id="9a8aa-124">[![再减少高度](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="9a8aa-125">然后减小高度 ([单击此项可查看原尺寸图像](executing-several-animations-after-each-other-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9a8aa-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a8aa-126">[上一页](executing-several-animations-at-the-same-time-cs.md)
> [下一页](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9a8aa-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
