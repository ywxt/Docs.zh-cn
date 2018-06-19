---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: 定位 ModalPopup (C#) |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。 但是该控件不提供...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: bee5be84259231d8cd5efde74b610d72f5e250cc
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874143"
---
<a name="positioning-a-modalpopup-c"></a><span data-ttu-id="6d08e-104">定位 ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="6d08e-104">Positioning a ModalPopup (C#)</span></span>
====================
<span data-ttu-id="6d08e-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6d08e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6d08e-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6d08e-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="6d08e-107">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="6d08e-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="6d08e-108">但是该控件不提供内置的功能，用于定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6d08e-108">However the control does not offer a built-in functionality to position the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="6d08e-109">概述</span><span class="sxs-lookup"><span data-stu-id="6d08e-109">Overview</span></span>

<span data-ttu-id="6d08e-110">AJAX 控件工具包中的 ModalPopup 控制提供一种简单的方法，以创建模式的弹出项，使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="6d08e-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="6d08e-111">但是该控件不提供内置的功能，用于定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6d08e-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="6d08e-112">步骤</span><span class="sxs-lookup"><span data-stu-id="6d08e-112">Steps</span></span>

<span data-ttu-id="6d08e-113">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="6d08e-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="6d08e-114">必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="6d08e-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="6d08e-115">接下来，添加一个面板，它可作为模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6d08e-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="6d08e-116">一个按钮用于关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="6d08e-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="6d08e-117">每当显示弹出窗口，它应位于在页中的某个特定位置处。</span><span class="sxs-lookup"><span data-stu-id="6d08e-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="6d08e-118">对于此任务，创建一个客户端 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="6d08e-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="6d08e-119">它首先尝试访问面板。</span><span class="sxs-lookup"><span data-stu-id="6d08e-119">It first tries to access the panel.</span></span> <span data-ttu-id="6d08e-120">如果成功，使用 CSS 和 JavaScript （更改将在弹出窗口的位置） 设置面板的位置。</span><span class="sxs-lookup"><span data-stu-id="6d08e-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="6d08e-121">但是，`ModalPopupExtender`还会控制尝试定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="6d08e-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="6d08e-122">因此，JavaScript 代码重复定位弹出窗口中，每隔 10 秒。</span><span class="sxs-lookup"><span data-stu-id="6d08e-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="6d08e-123">如你所见的的返回值`setTimeout()`JavaScript 方法将保存在全局变量。</span><span class="sxs-lookup"><span data-stu-id="6d08e-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="6d08e-124">这样就可以停止按需、 弹出窗口的重复定位使用`clearTimeout()`方法：</span><span class="sxs-lookup"><span data-stu-id="6d08e-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="6d08e-125">现在剩下所要做的所有是使浏览器调用这些函数可能的情况。</span><span class="sxs-lookup"><span data-stu-id="6d08e-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="6d08e-126">`movePanel()`触发面板中单击该按钮时，必须调用 JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="6d08e-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="6d08e-127">与`stopMoving()`函数派上用场时，就可以在关闭弹出窗口中触发`ModalPopupExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="6d08e-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]


<span data-ttu-id="6d08e-128">[![模式的弹出窗口出现在指定的位置](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6d08e-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="6d08e-129">模式的弹出窗口出现在指定的位置 ([单击以查看实际尺寸的图像](positioning-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6d08e-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6d08e-130">[上一页](handling-postbacks-from-a-modalpopup-cs.md)
> [下一页](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6d08e-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
