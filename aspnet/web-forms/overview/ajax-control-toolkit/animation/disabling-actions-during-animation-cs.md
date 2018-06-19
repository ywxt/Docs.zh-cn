---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: 期间动画 (C#) 禁用操作 |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 它还支持操作...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: 7862c5026a48fbee6eb48beb411e5e1d60c8b406
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870812"
---
<a name="disabling-actions-during-animation-c"></a><span data-ttu-id="faf2e-104">禁用操作期间动画 (C#)</span><span class="sxs-lookup"><span data-stu-id="faf2e-104">Disabling Actions during Animation (C#)</span></span>
====================
<span data-ttu-id="faf2e-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="faf2e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="faf2e-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="faf2e-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="faf2e-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="faf2e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="faf2e-108">它还支持操作，例如，鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="faf2e-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="faf2e-109">但是当鼠标单击启动一个动画，这是需要在动画期间禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="faf2e-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>


## <a name="overview"></a><span data-ttu-id="faf2e-110">概述</span><span class="sxs-lookup"><span data-stu-id="faf2e-110">Overview</span></span>

<span data-ttu-id="faf2e-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="faf2e-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="faf2e-112">它还支持操作，例如，鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="faf2e-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="faf2e-113">但是当鼠标单击启动一个动画，这是需要在动画期间禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="faf2e-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="faf2e-114">步骤</span><span class="sxs-lookup"><span data-stu-id="faf2e-114">Steps</span></span>

<span data-ttu-id="faf2e-115">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="faf2e-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="faf2e-116">动画将应用到一个 HTML 按钮如下：</span><span class="sxs-lookup"><span data-stu-id="faf2e-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="faf2e-117">请注意，由于我们不希望该按钮以创建回发; 而不是 Web 控件使用 HTML 控件它只应启动我们的客户端动画。</span><span class="sxs-lookup"><span data-stu-id="faf2e-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="faf2e-118">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="faf2e-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="faf2e-119">在`<Animations>`节点，`<OnClick>`是正确的元素，用于处理鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="faf2e-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="faf2e-120">但是，无法在动画期间单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="faf2e-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="faf2e-121">`<EnableAction>`元素可以负责。</span><span class="sxs-lookup"><span data-stu-id="faf2e-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="faf2e-122">设置`Enabled="false"`作为一部分动画禁用的按钮。</span><span class="sxs-lookup"><span data-stu-id="faf2e-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="faf2e-123">因为我们要使用多个 （禁用的按钮和实际的动画） 的单个动画`<Parallel>`元素必须为要在其中粘附组合在一起成为一个单个的动画。</span><span class="sxs-lookup"><span data-stu-id="faf2e-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="faf2e-124">下面是完整标记`AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="faf2e-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="faf2e-125">此外可以在动画，使用下面的 XML 元素列表的末尾后重新启用到按钮：</span><span class="sxs-lookup"><span data-stu-id="faf2e-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="faf2e-126">但是在给定方案这将是没有用处，因为按钮淡出，且不在动画末尾可见。</span><span class="sxs-lookup"><span data-stu-id="faf2e-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>


<span data-ttu-id="faf2e-127">[![动画运行时，就会立即将禁用的按钮](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="faf2e-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="faf2e-128">动画运行时，就会立即将禁用的按钮 ([单击以查看实际尺寸的图像](disabling-actions-during-animation-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="faf2e-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="faf2e-129">[上一页](animating-in-response-to-user-interaction-cs.md)
> [下一页](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="faf2e-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>
