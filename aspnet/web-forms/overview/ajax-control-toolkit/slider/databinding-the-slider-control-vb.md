---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 数据绑定滑块控件 (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 就可以将绑定当前 positio...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: aeaca2ebf61f49a5c081a3a1df188aa1541192d9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37376302"
---
<a name="databinding-the-slider-control-vb"></a><span data-ttu-id="88ee1-104">数据绑定滑块控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="88ee1-104">Databinding the Slider Control (VB)</span></span>
====================
<span data-ttu-id="88ee1-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="88ee1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="88ee1-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="88ee1-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="88ee1-107">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="88ee1-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="88ee1-108">就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="88ee1-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="88ee1-109">概述</span><span class="sxs-lookup"><span data-stu-id="88ee1-109">Overview</span></span>

<span data-ttu-id="88ee1-110">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="88ee1-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="88ee1-111">就可以绑定到另一个 ASP.NET 控件的当前滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="88ee1-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="88ee1-112">步骤</span><span class="sxs-lookup"><span data-stu-id="88ee1-112">Steps</span></span>

<span data-ttu-id="88ee1-113">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (但在`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="88ee1-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="88ee1-114">接下来，添加两个`TextBox`到页面的控件。</span><span class="sxs-lookup"><span data-stu-id="88ee1-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="88ee1-115">一个将转换为图形滑块，和另一个将保存的滑块位置。</span><span class="sxs-lookup"><span data-stu-id="88ee1-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="88ee1-116">下一步已是最后一步。</span><span class="sxs-lookup"><span data-stu-id="88ee1-116">The next step is already the final step.</span></span> <span data-ttu-id="88ee1-117">`SliderExtender`从 ASP.NET AJAX 控件工具包控件使一个滑块，从第一个文本框和滑块位置更改时，会自动更新第二个文本框。</span><span class="sxs-lookup"><span data-stu-id="88ee1-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="88ee1-118">要使其工作，以便`SliderExtender`的`TargetControlID`属性必须设置为第一个文本框; ID`BoundControlID`属性必须设置为第二个文本框的 ID。</span><span class="sxs-lookup"><span data-stu-id="88ee1-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="88ee1-119">您可以看到在浏览器中，数据绑定的工作在两个方向： 在文本框中输入新值更新滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="88ee1-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="88ee1-120">如果仅读取第二个文本框中，可以这样就更难用户手动更新中有值与文本字段添加较弱的保护。</span><span class="sxs-lookup"><span data-stu-id="88ee1-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


<span data-ttu-id="88ee1-121">[![滑块和文本框都保持同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="88ee1-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="88ee1-122">滑块和文本框都是同步 ([单击此项可查看原尺寸图像](databinding-the-slider-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="88ee1-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="88ee1-123">上一篇</span><span class="sxs-lookup"><span data-stu-id="88ee1-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
