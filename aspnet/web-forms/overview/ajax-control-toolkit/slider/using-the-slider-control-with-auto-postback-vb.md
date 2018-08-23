---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 滑块控件中使用自动回发 (VB) |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。 它是可以进行滑块自动过帐...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: 403e8fa6e54d84eb091769cbdb6ef1003ad4245c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825462"
---
<a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="084ac-104">滑块控件中使用自动回发 (VB)</span><span class="sxs-lookup"><span data-stu-id="084ac-104">Using the Slider Control With Auto-Postback (VB)</span></span>
====================
<span data-ttu-id="084ac-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="084ac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="084ac-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="084ac-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="084ac-107">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="084ac-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="084ac-108">它是可以进行一次其值更改滑块自动回发。</span><span class="sxs-lookup"><span data-stu-id="084ac-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="084ac-109">概述</span><span class="sxs-lookup"><span data-stu-id="084ac-109">Overview</span></span>

<span data-ttu-id="084ac-110">AJAX 控件工具包中的滑块控件提供了一个图形滑块，可以使用鼠标进行控制。</span><span class="sxs-lookup"><span data-stu-id="084ac-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="084ac-111">它是可以进行一次其值更改滑块自动回发。</span><span class="sxs-lookup"><span data-stu-id="084ac-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="084ac-112">步骤</span><span class="sxs-lookup"><span data-stu-id="084ac-112">Steps</span></span>

<span data-ttu-id="084ac-113">为了进行更改时自动回发的滑块，这两个文本框特性，因此需要`AutoPostBack="true"`： 文本框中，在将成为滑块本身，以及包含滑块的位置的文本框。</span><span class="sxs-lookup"><span data-stu-id="084ac-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="084ac-114">下面是为此，所需的标记：</span><span class="sxs-lookup"><span data-stu-id="084ac-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="084ac-115">`SliderExtender`从 ASP.NET AJAX 控件工具包控件将滑块功能分配给两个文本框：</span><span class="sxs-lookup"><span data-stu-id="084ac-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="084ac-116">更高版本将使用其他标签元素回发的用户通知：</span><span class="sxs-lookup"><span data-stu-id="084ac-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="084ac-117">最后， `ScriptManager` ASP.NET ajax 控件将加载所需的 JavaScript 控件工具包，若要运行的：</span><span class="sxs-lookup"><span data-stu-id="084ac-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="084ac-118">现在，滑块回发;在服务器端，可能会捕获和处理此事件：</span><span class="sxs-lookup"><span data-stu-id="084ac-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]


<span data-ttu-id="084ac-119">[![将滑块移动触发回发](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="084ac-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="084ac-120">将滑块移动触发回发 ([单击此项可查看原尺寸图像](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="084ac-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>


<span data-ttu-id="084ac-121">[![然后，此更改的日期写入标签中](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="084ac-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="084ac-122">然后，此更改的日期写入标签中 ([单击此项可查看原尺寸图像](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="084ac-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="084ac-123">[上一页](databinding-the-slider-control-cs.md)
> [下一页](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="084ac-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
