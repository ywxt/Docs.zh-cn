---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 滑块控件使用自动回发 (C#) |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。 它是可以进行滑块自动过帐...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: e347d20c5c2ee48e6ed801e95459af6f0bcd2667
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="57cbd-104">滑块控件使用自动回发 (C#)</span><span class="sxs-lookup"><span data-stu-id="57cbd-104">Using the Slider Control With Auto-Postback (C#)</span></span>
====================
<span data-ttu-id="57cbd-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="57cbd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="57cbd-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="57cbd-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="57cbd-107">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="57cbd-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="57cbd-108">它是可以进行滑块有些一次将其值更改。</span><span class="sxs-lookup"><span data-stu-id="57cbd-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="57cbd-109">概述</span><span class="sxs-lookup"><span data-stu-id="57cbd-109">Overview</span></span>

<span data-ttu-id="57cbd-110">AJAX 控件工具包中的滑块控件提供图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="57cbd-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="57cbd-111">它是可以进行滑块有些一次将其值更改。</span><span class="sxs-lookup"><span data-stu-id="57cbd-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="57cbd-112">步骤</span><span class="sxs-lookup"><span data-stu-id="57cbd-112">Steps</span></span>

<span data-ttu-id="57cbd-113">为了使滑块更改时自动回发，两个文本框内需要的特性`AutoPostBack="true"`： 文本框将成为滑块本身，并包含滑块的位置的文本框。</span><span class="sxs-lookup"><span data-stu-id="57cbd-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="57cbd-114">下面是该所需的标记：</span><span class="sxs-lookup"><span data-stu-id="57cbd-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="57cbd-115">`SliderExtender` ASP.NET AJAX 控件工具包中的控件将滑块功能分配给两个文本框中：</span><span class="sxs-lookup"><span data-stu-id="57cbd-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="57cbd-116">其他标签元素以后可用于通知的回发用户：</span><span class="sxs-lookup"><span data-stu-id="57cbd-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="57cbd-117">最后，`ScriptManager`控件的 ASP.NET AJAX 加载控件工具包工作所需的 JavaScript:</span><span class="sxs-lookup"><span data-stu-id="57cbd-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="57cbd-118">现在返回; 发布滑块在服务器端，可能捕获到此事件，并采取行动中：</span><span class="sxs-lookup"><span data-stu-id="57cbd-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


<span data-ttu-id="57cbd-119">[![将滑块移动触发回发](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="57cbd-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="57cbd-120">将滑块移动触发回发 ([单击以查看实际尺寸的图像](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="57cbd-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>


<span data-ttu-id="57cbd-121">[![然后，此更改的日期写入标签中](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="57cbd-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="57cbd-122">然后，此更改的日期写入标签中 ([单击以查看实际尺寸的图像](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="57cbd-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="57cbd-123">下一篇</span><span class="sxs-lookup"><span data-stu-id="57cbd-123">Next</span></span>](databinding-the-slider-control-cs.md)
