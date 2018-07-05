---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 动画 (VB) 过程中禁用操作 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 它还支持操作...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 824eb8f0a219df08044bc62d7ad020c53e1ee792
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37399569"
---
<a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="85a30-104">动画 (VB) 过程中禁用操作</span><span class="sxs-lookup"><span data-stu-id="85a30-104">Disabling Actions during Animation (VB)</span></span>
====================
<span data-ttu-id="85a30-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="85a30-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="85a30-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="85a30-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="85a30-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="85a30-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="85a30-108">它还支持的操作，例如鼠标点击操作。</span><span class="sxs-lookup"><span data-stu-id="85a30-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="85a30-109">但是时鼠标单击启动动画，最好在动画期间禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="85a30-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>


## <a name="overview"></a><span data-ttu-id="85a30-110">概述</span><span class="sxs-lookup"><span data-stu-id="85a30-110">Overview</span></span>

<span data-ttu-id="85a30-111">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="85a30-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="85a30-112">它还支持的操作，例如鼠标点击操作。</span><span class="sxs-lookup"><span data-stu-id="85a30-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="85a30-113">但是时鼠标单击启动动画，最好在动画期间禁用鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="85a30-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="85a30-114">步骤</span><span class="sxs-lookup"><span data-stu-id="85a30-114">Steps</span></span>

<span data-ttu-id="85a30-115">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="85a30-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="85a30-116">动画将应用于如下的 HTML 按钮：</span><span class="sxs-lookup"><span data-stu-id="85a30-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="85a30-117">请注意，由于我们不希望按钮以创建一个回发; 而不是 Web 控件使用 HTML 控件它应只需启动为我们的客户端的动画。</span><span class="sxs-lookup"><span data-stu-id="85a30-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="85a30-118">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="85a30-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="85a30-119">内`<Animations>`节点，`<OnClick>`是正确的元素，用于处理鼠标单击。</span><span class="sxs-lookup"><span data-stu-id="85a30-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="85a30-120">但是，在动画期间，可以单击该按钮。</span><span class="sxs-lookup"><span data-stu-id="85a30-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="85a30-121">`<EnableAction>`元素可以考虑到这一点。</span><span class="sxs-lookup"><span data-stu-id="85a30-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="85a30-122">设置`Enabled="false"`动画的一部分禁用的按钮。</span><span class="sxs-lookup"><span data-stu-id="85a30-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="85a30-123">因为我们要使用多个单独的动画 （禁用按钮和实际的动画）`<Parallel>`元素必须为粘合连接成一个单一的动画。</span><span class="sxs-lookup"><span data-stu-id="85a30-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="85a30-124">下面是完整标记`AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="85a30-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="85a30-125">它还可以在列表的末尾使用下面的 XML 元素的动画结束后重新启用到按钮：</span><span class="sxs-lookup"><span data-stu-id="85a30-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="85a30-126">但是在给定方案这将是没有用自按钮淡出，并且不在动画结束时可见。</span><span class="sxs-lookup"><span data-stu-id="85a30-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>


<span data-ttu-id="85a30-127">[![动画运行时，将禁用的按钮](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="85a30-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="85a30-128">动画运行时，将禁用的按钮 ([单击此项可查看原尺寸图像](disabling-actions-during-animation-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="85a30-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85a30-129">[上一页](animating-in-response-to-user-interaction-vb.md)
> [下一页](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="85a30-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>
