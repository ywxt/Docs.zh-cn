---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 数据绑定滑块控件 (VB) |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。 就可以将绑定当前 positio...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ecd8598cd7fdcbbb4812e501bb30fa1f563a054
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="databinding-the-slider-control-vb"></a><span data-ttu-id="d8bfe-104">数据绑定滑块控件 (VB)</span><span class="sxs-lookup"><span data-stu-id="d8bfe-104">Databinding the Slider Control (VB)</span></span>
====================
<span data-ttu-id="d8bfe-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d8bfe-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d8bfe-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d8bfe-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)</span></span>

> <span data-ttu-id="d8bfe-107">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="d8bfe-108">很可能要绑定到另一个 ASP.NET 控件的滑块的当前位置。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="d8bfe-109">概述</span><span class="sxs-lookup"><span data-stu-id="d8bfe-109">Overview</span></span>

<span data-ttu-id="d8bfe-110">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="d8bfe-111">很可能要绑定到另一个 ASP.NET 控件的滑块的当前位置。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="d8bfe-112">步骤</span><span class="sxs-lookup"><span data-stu-id="d8bfe-112">Steps</span></span>

<span data-ttu-id="d8bfe-113">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内`<form>`元素):</span><span class="sxs-lookup"><span data-stu-id="d8bfe-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

<span data-ttu-id="d8bfe-114">接下来，添加两个`TextBox`到页面的控件。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="d8bfe-115">一个将转换为图形滑块，并且另一个将保留将滑块的位置。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

<span data-ttu-id="d8bfe-116">下一步已是最后一步。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-116">The next step is already the final step.</span></span> <span data-ttu-id="d8bfe-117">`SliderExtender` ASP.NET AJAX 控件工具包中的控制使滑块外的第一个文本框和滑块位置更改时自动更新第二个文本框。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="d8bfe-118">为了使让此操作生效，`SliderExtender`的`TargetControlID`属性必须设置为第一个文本框; 的 ID`BoundControlID`属性必须设置为第二个文本框的 ID。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

<span data-ttu-id="d8bfe-119">正如您可以看到在浏览器中，数据绑定的工作原理在两个方向： 在文本框中输入新值更新滚动条的位置。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="d8bfe-120">如果使只读第二个文本框中，可能先将弱保护添加到文本字段中，以便更难要手动更新也没有值的用户。</span><span class="sxs-lookup"><span data-stu-id="d8bfe-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


<span data-ttu-id="d8bfe-121">[![滑块和文本框是同步](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d8bfe-121">[![Slider and text box are in sync](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="d8bfe-122">滑块和文本框是同步 ([单击以查看实际尺寸的图像](databinding-the-slider-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d8bfe-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d8bfe-123">上一篇</span><span class="sxs-lookup"><span data-stu-id="d8bfe-123">Previous</span></span>](using-the-slider-control-with-auto-postback-vb.md)
