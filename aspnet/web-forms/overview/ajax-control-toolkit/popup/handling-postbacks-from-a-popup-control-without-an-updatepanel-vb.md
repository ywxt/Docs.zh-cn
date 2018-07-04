---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: 通过使用没有 UpdatePanel (VB) 的弹出控件处理回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。 当回发发生时 su...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 5ef1d0300cba42eefb5f6cda77693aeafb93a31a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363839"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="5aac2-104">通过使用没有 UpdatePanel (VB) 的弹出控件处理回发</span><span class="sxs-lookup"><span data-stu-id="5aac2-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="5aac2-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5aac2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5aac2-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5aac2-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="5aac2-107">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="5aac2-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5aac2-108">在这样的面板中产生的回发和页面上有多个面板时很难确定单击的面板。</span><span class="sxs-lookup"><span data-stu-id="5aac2-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="5aac2-109">概述</span><span class="sxs-lookup"><span data-stu-id="5aac2-109">Overview</span></span>

<span data-ttu-id="5aac2-110">AJAX 控件工具包中的 PopupControl 扩展程序提供简单的方法来激活任何其他控件时触发一个弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="5aac2-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="5aac2-111">在这样的面板中产生的回发和页面上有多个面板时很难确定单击的面板。</span><span class="sxs-lookup"><span data-stu-id="5aac2-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="5aac2-112">步骤</span><span class="sxs-lookup"><span data-stu-id="5aac2-112">Steps</span></span>

<span data-ttu-id="5aac2-113">使用时`PopupControl`带回发，但无`UpdatePanel`的页上，控件工具包不提供任何方法来确定哪些客户端元素已触发反过来引起回发的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="5aac2-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="5aac2-114">但是借助一个小技巧对于此方案提供一种解决方法。</span><span class="sxs-lookup"><span data-stu-id="5aac2-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="5aac2-115">首先，下面是基本设置： 这两个触发的同一个弹出窗口中，日历的两个文本框。</span><span class="sxs-lookup"><span data-stu-id="5aac2-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="5aac2-116">两个`PopupControlExtenders`将文本框和弹出项组合在一起。</span><span class="sxs-lookup"><span data-stu-id="5aac2-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="5aac2-117">基本理念是隐藏的窗体字段中添加&lt; `form` &gt;包含启动弹出项文本框中的元素：</span><span class="sxs-lookup"><span data-stu-id="5aac2-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="5aac2-118">加载页面时，JavaScript 代码会将事件处理程序添加到两个文本框： 每当用户单击文本框时，其名称写入隐藏窗体字段：</span><span class="sxs-lookup"><span data-stu-id="5aac2-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="5aac2-119">在服务器端代码中，必须读取的隐藏字段的值。</span><span class="sxs-lookup"><span data-stu-id="5aac2-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="5aac2-120">由于隐藏的表单字段进行了一些无关紧要操作，一种允许列表方法验证隐藏的值是必需的。</span><span class="sxs-lookup"><span data-stu-id="5aac2-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="5aac2-121">一旦确定正确的文本框中，从日历中的日期写入到它。</span><span class="sxs-lookup"><span data-stu-id="5aac2-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


<span data-ttu-id="5aac2-122">[![当用户单击文本框中，将显示日历](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5aac2-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="5aac2-123">当用户单击文本框中，将显示日历 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5aac2-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="5aac2-124">[![单击某个日期将其放入文本框](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5aac2-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="5aac2-125">单击某个日期将其放在文本框中 ([单击此项可查看原尺寸图像](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5aac2-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5aac2-126">上一篇</span><span class="sxs-lookup"><span data-stu-id="5aac2-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
