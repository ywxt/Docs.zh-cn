---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 使用多个弹出控件 (C#) |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。 它还可使用 m...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 7acd1b53e1b3e3e0d09d248b68941b166da3e81e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-multiple-popup-controls-c"></a><span data-ttu-id="bf8b7-104">使用多个弹出控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="bf8b7-104">Using Multiple Popup Controls (C#)</span></span>
====================
<span data-ttu-id="bf8b7-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="bf8b7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="bf8b7-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="bf8b7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="bf8b7-107">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="bf8b7-108">还有可能要使用多个在一页上的弹出窗口控件。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="bf8b7-109">概述</span><span class="sxs-lookup"><span data-stu-id="bf8b7-109">Overview</span></span>

<span data-ttu-id="bf8b7-110">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="bf8b7-111">还有可能要使用多个在一页上的弹出窗口控件。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="bf8b7-112">步骤</span><span class="sxs-lookup"><span data-stu-id="bf8b7-112">Steps</span></span>

<span data-ttu-id="bf8b7-113">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="bf8b7-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="bf8b7-114">接下来，添加一个面板，它可作为弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="bf8b7-115">在当前的方案中，面板包含`Calendar`控件。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="bf8b7-116">为了避免引起的日历的回发页面将刷新，面板将内`UpdatePanel`控件：</span><span class="sxs-lookup"><span data-stu-id="bf8b7-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="bf8b7-117">此页还包含两个文本框。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-117">The page also contains two text boxes.</span></span> <span data-ttu-id="bf8b7-118">对于每个文本框中，一旦激活文本框中应显示日历弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="bf8b7-119">现在扩展与两个文本框中的每个`PopupControlExtender`。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="bf8b7-120">`TargetControlID`属性提供绑定到扩展程序控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="bf8b7-121">`PopupControlID`属性包含弹出面板中的 ID。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="bf8b7-122">在这种情况下，这两个扩展器显示相同的面板中，但不同的面板也有可能。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="bf8b7-123">现在只要你单击某个文本字段中，会显示日历的字段下允许您选择一个日期。</span><span class="sxs-lookup"><span data-stu-id="bf8b7-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="bf8b7-124">（在选定的日期取回向文本框中介绍了在不同的教程。）</span><span class="sxs-lookup"><span data-stu-id="bf8b7-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="bf8b7-125">[![当用户单击的文本框，会显示日历](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bf8b7-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="bf8b7-126">当用户单击的文本框，会显示日历 ([单击以查看实际尺寸的图像](using-multiple-popup-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="bf8b7-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bf8b7-127">下一篇</span><span class="sxs-lookup"><span data-stu-id="bf8b7-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
