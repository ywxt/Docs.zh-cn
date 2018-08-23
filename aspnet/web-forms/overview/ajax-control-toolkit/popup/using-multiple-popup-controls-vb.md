---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 使用多个弹出控件 (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 还有可能要使用 m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 81b0dbd794d31bc3c55bff4ba8110c590b88b509
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833734"
---
<a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="92a43-104">使用多个弹出控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="92a43-104">Using Multiple Popup Controls (VB)</span></span>
====================
<span data-ttu-id="92a43-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="92a43-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="92a43-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="92a43-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="92a43-107">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="92a43-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="92a43-108">还有可能要使用在同一页上的多个弹出控件。</span><span class="sxs-lookup"><span data-stu-id="92a43-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="92a43-109">概述</span><span class="sxs-lookup"><span data-stu-id="92a43-109">Overview</span></span>

<span data-ttu-id="92a43-110">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="92a43-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="92a43-111">还有可能要使用在同一页上的多个弹出控件。</span><span class="sxs-lookup"><span data-stu-id="92a43-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="92a43-112">步骤</span><span class="sxs-lookup"><span data-stu-id="92a43-112">Steps</span></span>

<span data-ttu-id="92a43-113">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="92a43-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="92a43-114">接下来，添加一个面板作为弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="92a43-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="92a43-115">在当前的方案中，面板包含`Calendar`控件。</span><span class="sxs-lookup"><span data-stu-id="92a43-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="92a43-116">为了避免引起的日历的回发页面刷新，面板都会放到`UpdatePanel`控件：</span><span class="sxs-lookup"><span data-stu-id="92a43-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="92a43-117">该页还包含两个文本框。</span><span class="sxs-lookup"><span data-stu-id="92a43-117">The page also contains two text boxes.</span></span> <span data-ttu-id="92a43-118">对于每个文本框，文本框中激活后，应显示日历弹出框。</span><span class="sxs-lookup"><span data-stu-id="92a43-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="92a43-119">现在扩展使用的两个文本框的每个`PopupControlExtender`。</span><span class="sxs-lookup"><span data-stu-id="92a43-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="92a43-120">`TargetControlID`属性提供绑定到扩展器控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="92a43-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="92a43-121">`PopupControlID`属性包含的弹出面板的 ID。</span><span class="sxs-lookup"><span data-stu-id="92a43-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="92a43-122">在这种情况下，这两个扩展程序显示相同的面板中，但也是可能的不同的面板。</span><span class="sxs-lookup"><span data-stu-id="92a43-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="92a43-123">现在只要您在文本字段内单击，日历显示字段的下方，您可以选择一个日期。</span><span class="sxs-lookup"><span data-stu-id="92a43-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="92a43-124">（所选的日期取回到文本框中将介绍在不同的教程。）</span><span class="sxs-lookup"><span data-stu-id="92a43-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="92a43-125">[![当用户单击文本框中，将显示日历](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="92a43-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="92a43-126">当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="92a43-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="92a43-127">[上一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [下一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="92a43-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
