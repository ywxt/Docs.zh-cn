---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: 定位 ModalPopup (VB) |Microsoft Docs
author: wenz
description: 在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。 但是该控件不提供...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: a507cb173b6dba96ca532a249fa9d495ded7d4e8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835105"
---
<a name="positioning-a-modalpopup-vb"></a><span data-ttu-id="8dcf4-104">定位 ModalPopup (VB)</span><span class="sxs-lookup"><span data-stu-id="8dcf4-104">Positioning a ModalPopup (VB)</span></span>
====================
<span data-ttu-id="8dcf4-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8dcf4-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8dcf4-106">[下载代码](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8dcf4-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)</span></span>

> <span data-ttu-id="8dcf4-107">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8dcf4-108">但是该控件不提供内置的功能，用于定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-108">However the control does not offer a built-in functionality to position the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="8dcf4-109">概述</span><span class="sxs-lookup"><span data-stu-id="8dcf4-109">Overview</span></span>

<span data-ttu-id="8dcf4-110">在 AJAX 控件工具包的 ModalPopup 控件提供了简单的方法来创建模式弹出框使用客户端的方式。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="8dcf4-111">但是该控件不提供内置的功能，用于定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="8dcf4-112">步骤</span><span class="sxs-lookup"><span data-stu-id="8dcf4-112">Steps</span></span>

<span data-ttu-id="8dcf4-113">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="8dcf4-114">控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="8dcf4-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="8dcf4-115">接下来，添加一个面板作为模式弹出框。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="8dcf4-116">一个按钮用于关闭弹出窗口：</span><span class="sxs-lookup"><span data-stu-id="8dcf4-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="8dcf4-117">每当显示弹出窗口，它应定位在页中的某个特定位置中。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="8dcf4-118">对于此任务中，创建客户端的 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="8dcf4-119">它首先尝试访问面板。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-119">It first tries to access the panel.</span></span> <span data-ttu-id="8dcf4-120">如果成功，将使用 CSS 和 JavaScript （更改将在弹出窗口的位置） 设置面板的位置。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="8dcf4-121">但是，`ModalPopupExtender`还会控制尝试定位弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="8dcf4-122">因此，JavaScript 代码重复定位弹出窗口中，每隔 10 秒。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

<span data-ttu-id="8dcf4-123">正如您所看到的返回值的`setTimeout()`JavaScript 方法将保存在全局变量。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="8dcf4-124">这样就可以停止重复的按需、 弹出窗口定位使用`clearTimeout()`方法：</span><span class="sxs-lookup"><span data-stu-id="8dcf4-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

<span data-ttu-id="8dcf4-125">现在剩下要做的是使浏览器调用这些函数在可能的情况。</span><span class="sxs-lookup"><span data-stu-id="8dcf4-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="8dcf4-126">`movePanel()`触发面板中单击该按钮时，必须调用 JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="8dcf4-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

<span data-ttu-id="8dcf4-127">并`stopMoving()`函数发挥作用时这可能关闭弹出窗口中触发`ModalPopupExtender`控件：</span><span class="sxs-lookup"><span data-stu-id="8dcf4-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]


<span data-ttu-id="8dcf4-128">[![模式弹出框显示在指定的位置](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8dcf4-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="8dcf4-129">模式弹出框显示在指定的位置 ([单击此项可查看原尺寸图像](positioning-a-modalpopup-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8dcf4-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8dcf4-130">上一篇</span><span class="sxs-lookup"><span data-stu-id="8dcf4-130">Previous</span></span>](handling-postbacks-from-a-modalpopup-vb.md)
