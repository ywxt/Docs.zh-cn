---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 将动画添加到控件 (C#) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 本教程演示如何...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ba122660045c3f5dd4b11f118df174a79de814a1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="adding-animation-to-a-control-c"></a><span data-ttu-id="437be-104">将动画添加到控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="437be-104">Adding Animation to a Control (C#)</span></span>
====================
<span data-ttu-id="437be-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="437be-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="437be-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="437be-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="437be-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="437be-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="437be-108">本教程演示如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="437be-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="437be-109">概述</span><span class="sxs-lookup"><span data-stu-id="437be-109">Overview</span></span>

<span data-ttu-id="437be-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="437be-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="437be-111">本教程演示如何设置此类动画。</span><span class="sxs-lookup"><span data-stu-id="437be-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="437be-112">步骤</span><span class="sxs-lookup"><span data-stu-id="437be-112">Steps</span></span>

<span data-ttu-id="437be-113">第一步是像往常一样包括`ScriptManager`在页中，以便加载 ASP.NET AJAX 库，并可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="437be-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="437be-114">在此方案中动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="437be-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="437be-115">面板关联的 CSS 类定义的背景颜色和宽度：</span><span class="sxs-lookup"><span data-stu-id="437be-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="437be-116">接下来，我们需要`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="437be-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="437be-117">后提供`ID`和常用`runat="server"`、`TargetControlID`属性必须设置为该控件，要进行动画处理，在本例中为面板：</span><span class="sxs-lookup"><span data-stu-id="437be-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="437be-118">使用遗憾的是当前不完全支持 Visual Studio IntelliSense 的 XML 语法以声明方式，应用整个动画。</span><span class="sxs-lookup"><span data-stu-id="437be-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="437be-119">根节点是`<Animations>;`在此节点中，这将决定当动画 take(s) 位置允许多个事件：</span><span class="sxs-lookup"><span data-stu-id="437be-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="437be-120">`OnClick` （鼠标单击）</span><span class="sxs-lookup"><span data-stu-id="437be-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="437be-121">`OnHoverOut` （当鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="437be-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="437be-122">`OnHoverOver` (当鼠标悬停在控件上，停止`OnHoverOut`动画)</span><span class="sxs-lookup"><span data-stu-id="437be-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="437be-123">`OnLoad` （如果已加载页）</span><span class="sxs-lookup"><span data-stu-id="437be-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="437be-124">`OnMouseOut` （当鼠标离开控件）</span><span class="sxs-lookup"><span data-stu-id="437be-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="437be-125">`OnMouseOver` (当鼠标悬停在控件上，不停止`OnMouseOut`动画)</span><span class="sxs-lookup"><span data-stu-id="437be-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="437be-126">框架附带的动画，每个由其自己的 XML 元素表示一组。</span><span class="sxs-lookup"><span data-stu-id="437be-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="437be-127">下面是所选内容：</span><span class="sxs-lookup"><span data-stu-id="437be-127">Here is a selection:</span></span>

- <span data-ttu-id="437be-128">`<Color>` （更改一种颜色）</span><span class="sxs-lookup"><span data-stu-id="437be-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="437be-129">`<FadeIn>` （淡入淡出中）</span><span class="sxs-lookup"><span data-stu-id="437be-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="437be-130">`<FadeOut>` （淡出）</span><span class="sxs-lookup"><span data-stu-id="437be-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="437be-131">`<Property>` （更改控件的属性）</span><span class="sxs-lookup"><span data-stu-id="437be-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="437be-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="437be-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="437be-133">`<Resize>` （更改大小）</span><span class="sxs-lookup"><span data-stu-id="437be-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="437be-134">`<Scale>` （按比例的大小发生更改）</span><span class="sxs-lookup"><span data-stu-id="437be-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="437be-135">在此示例中，面板应淡出。动画应该采取 1.5 秒 (`Duration`属性)，显示 24 （动画步骤） 每秒帧数 (`Fps` attributs)。</span><span class="sxs-lookup"><span data-stu-id="437be-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attributs).</span></span> <span data-ttu-id="437be-136">下面是完整标记`AnimationExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="437be-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="437be-137">运行此脚本时，面板会显示，并以一个半秒为单位淡出。</span><span class="sxs-lookup"><span data-stu-id="437be-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


<span data-ttu-id="437be-138">[![面板淡出](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="437be-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="437be-139">面板淡出 ([单击以查看实际尺寸的图像](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="437be-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="437be-140">下一篇</span><span class="sxs-lookup"><span data-stu-id="437be-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
