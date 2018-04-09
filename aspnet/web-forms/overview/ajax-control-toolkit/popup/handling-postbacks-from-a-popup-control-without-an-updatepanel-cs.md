---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: 处理从没有 UpdatePanel (C#) 的弹出窗口控件的回发 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。 当回发发生在 su...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 59ffa05945289de6e01e2c21dd5a0f82ca1fa374
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="f87d8-104">处理从没有 UpdatePanel (C#) 的弹出窗口控件的回发</span><span class="sxs-lookup"><span data-stu-id="f87d8-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>
====================
<span data-ttu-id="f87d8-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f87d8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f87d8-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f87d8-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="f87d8-107">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="f87d8-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f87d8-108">此类面板中的回发发生并页上有多个面板时很难确定被单击的面板。</span><span class="sxs-lookup"><span data-stu-id="f87d8-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="f87d8-109">概述</span><span class="sxs-lookup"><span data-stu-id="f87d8-109">Overview</span></span>

<span data-ttu-id="f87d8-110">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="f87d8-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f87d8-111">此类面板中的回发发生并页上有多个面板时很难确定被单击的面板。</span><span class="sxs-lookup"><span data-stu-id="f87d8-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="f87d8-112">步骤</span><span class="sxs-lookup"><span data-stu-id="f87d8-112">Steps</span></span>

<span data-ttu-id="f87d8-113">使用时`PopupControl`回发时，但无`UpdatePanel`在页上，控件工具包不提供任何方法来确定哪些客户端元素已触发反过来导致回发的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="f87d8-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="f87d8-114">但是了小技巧，可以提供一种解决方法实现此方案。</span><span class="sxs-lookup"><span data-stu-id="f87d8-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="f87d8-115">首先，下面是基本安装程序： 两个文本框中，这两者都触发相同的弹出窗口，日历。</span><span class="sxs-lookup"><span data-stu-id="f87d8-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="f87d8-116">两个`PopupControlExtenders`将文本框和弹出项组合在一起。</span><span class="sxs-lookup"><span data-stu-id="f87d8-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="f87d8-117">基本理念都是隐藏的表单字段中添加&lt; `form` &gt;保存启动弹出项的文本框元素：</span><span class="sxs-lookup"><span data-stu-id="f87d8-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="f87d8-118">当加载页时，JavaScript 代码会将事件处理程序添加到两个文本框内： 在用户单击一个对文本框中，其名称写入到隐藏的表单字段：</span><span class="sxs-lookup"><span data-stu-id="f87d8-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="f87d8-119">在服务器端代码中，必须读取的隐藏字段的值。</span><span class="sxs-lookup"><span data-stu-id="f87d8-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="f87d8-120">由于隐藏的表单字段进行了一些无关紧要操作，一种白名单方法验证隐藏的值是必需的。</span><span class="sxs-lookup"><span data-stu-id="f87d8-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="f87d8-121">一旦已确定正确的文本框中，从日历日期被写入到它。</span><span class="sxs-lookup"><span data-stu-id="f87d8-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]


<span data-ttu-id="f87d8-122">[![当用户单击的文本框，会显示日历](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f87d8-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="f87d8-123">当用户单击的文本框，会显示日历 ([单击以查看实际尺寸的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f87d8-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>


<span data-ttu-id="f87d8-124">[![单击在日期将其放在文本框中](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f87d8-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="f87d8-125">单击在日期将其放在文本框中 ([单击以查看实际尺寸的图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f87d8-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f87d8-126">[上一页](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [下一页](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f87d8-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
