---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: 处理从具有 UpdatePanel (VB) 的弹出窗口控件的回发 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。 必须格外小心，要执行...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 312927e01911ea705d0614eac462cd034820c7b4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868472"
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="86536-104">处理从具有 UpdatePanel (VB) 的弹出窗口控件的回发</span><span class="sxs-lookup"><span data-stu-id="86536-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="86536-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="86536-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="86536-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="86536-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="86536-107">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="86536-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="86536-108">必须格外小心，要执行此类弹出窗口内的回发发生时。</span><span class="sxs-lookup"><span data-stu-id="86536-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="86536-109">概述</span><span class="sxs-lookup"><span data-stu-id="86536-109">Overview</span></span>

<span data-ttu-id="86536-110">AJAX 控件工具包中的 PopupControl 扩展程序提供的其他任何控件被激活时触发一个弹出窗口的简单办法。</span><span class="sxs-lookup"><span data-stu-id="86536-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="86536-111">必须格外小心，要执行此类弹出窗口内的回发发生时。</span><span class="sxs-lookup"><span data-stu-id="86536-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="86536-112">步骤</span><span class="sxs-lookup"><span data-stu-id="86536-112">Steps</span></span>

<span data-ttu-id="86536-113">使用时`PopupControl`回发时，`UpdatePanel`可以防止引起的回发页面刷新。</span><span class="sxs-lookup"><span data-stu-id="86536-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="86536-114">下面的标记定义几个重要元素：</span><span class="sxs-lookup"><span data-stu-id="86536-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="86536-115">A`ScriptManager`控制以便 ASP.NET AJAX 控件工具包能起作用</span><span class="sxs-lookup"><span data-stu-id="86536-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="86536-116">两个`TextBox`控件就会触发一个弹出窗口</span><span class="sxs-lookup"><span data-stu-id="86536-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="86536-117">A`Panel`将充当弹出窗口的控件</span><span class="sxs-lookup"><span data-stu-id="86536-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="86536-118">在面板中，`Calendar`中嵌入控件`UpdatePanel`控件</span><span class="sxs-lookup"><span data-stu-id="86536-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="86536-119">两个`PopupControlExtender`将该面板分配到的文本框中的控件</span><span class="sxs-lookup"><span data-stu-id="86536-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="86536-120">请注意，`OnSelectionChanged`属性`Calendar`控件设置。</span><span class="sxs-lookup"><span data-stu-id="86536-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="86536-121">因此，当用户选择在日历中的日期，产生的回发和服务器端方法`c1_SelectionChanged()`执行。</span><span class="sxs-lookup"><span data-stu-id="86536-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="86536-122">在该方法中，必须检索并回写到文本框中的当前日期。</span><span class="sxs-lookup"><span data-stu-id="86536-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="86536-123">如下所示的语法是： 首先，代理对象`PopupControlExtender`在页面上，必须生成。</span><span class="sxs-lookup"><span data-stu-id="86536-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="86536-124">ASP.NET AJAX 控件工具包提供`GetProxyForCurrentPopup()`方法。</span><span class="sxs-lookup"><span data-stu-id="86536-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="86536-125">此方法返回的对象支持`Commit()`将值发送回控件触发的弹出窗口 （不触发方法调用的控件 ！） 的方法。</span><span class="sxs-lookup"><span data-stu-id="86536-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="86536-126">下面的代码提供的自变量作为所选的日期`Commit()`方法，从而导致代码以便将所选的日期写回到文本框中：</span><span class="sxs-lookup"><span data-stu-id="86536-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="86536-127">现在只要你单击日历日期，所选的日期将显示在关联的文本框中，创建日期选取器控件可以当前找到许多网站上。</span><span class="sxs-lookup"><span data-stu-id="86536-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


<span data-ttu-id="86536-128">[![当用户单击的文本框，会显示日历](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="86536-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="86536-129">当用户单击的文本框，会显示日历 ([单击以查看实际尺寸的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="86536-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="86536-130">[![单击在日期将其放在文本框中](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="86536-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="86536-131">单击在日期将其放在文本框中 ([单击以查看实际尺寸的图像](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="86536-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86536-132">[上一页](using-multiple-popup-controls-vb.md)
> [下一页](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="86536-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
