---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 使用 Web 服务后端 (VB) 创建数字加/减控件 |Microsoft Docs
author: wenz
description: 而不是让用户复选框中键入一个值，数字增大/减小控件 （它同时存在于 Windows 和其他操作系统） 可能会证明随着更多 c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: bf69b3e6932df528e8ccd2348ffa6f13132f99f8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833237"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="edc72-103">使用 Web 服务后端 (VB) 创建数字增大/减小控件</span><span class="sxs-lookup"><span data-stu-id="edc72-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>
====================
<span data-ttu-id="edc72-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="edc72-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="edc72-105">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="edc72-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="edc72-106">而不是让用户复选框中键入一个值，数值加/减控件 （即存在于 Windows 和其他操作系统） 可以证明随着更多熟练。</span><span class="sxs-lookup"><span data-stu-id="edc72-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="edc72-107">默认情况下，NumericUpDown 控件始终每增加或减少值 1，但 web 服务可证明更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="edc72-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="edc72-108">概述</span><span class="sxs-lookup"><span data-stu-id="edc72-108">Overview</span></span>

<span data-ttu-id="edc72-109">而不是让用户复选框中键入一个值，数值加/减控件 （即存在于 Windows 和其他操作系统） 可以证明随着更多熟练。</span><span class="sxs-lookup"><span data-stu-id="edc72-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="edc72-110">默认情况下，`NumericUpDown`控件始终每增加或减少值 1，但 web 服务可证明更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="edc72-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="edc72-111">步骤</span><span class="sxs-lookup"><span data-stu-id="edc72-111">Steps</span></span>

<span data-ttu-id="edc72-112">ASP.NET AJAX 控件工具包包含`NumericUpDown`扩展程序，其会自动添加到文本框中的两个按钮： 一个用于增加其值，一个用于减小其。</span><span class="sxs-lookup"><span data-stu-id="edc72-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="edc72-113">但是该控件还支持 web 服务调用 （或页面方法调用）。</span><span class="sxs-lookup"><span data-stu-id="edc72-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="edc72-114">每当向上或向下按钮单击时的 JavaScript 代码连接到 web 服务器和执行方法存在。</span><span class="sxs-lookup"><span data-stu-id="edc72-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="edc72-115">方法签名是如下：</span><span class="sxs-lookup"><span data-stu-id="edc72-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="edc72-116">`current`自变量是文本框; 中的当前值`tag`属性是可以设置为的一个属性的其他上下文数据`NumericUpDown`扩展器 （但不是必需的）。</span><span class="sxs-lookup"><span data-stu-id="edc72-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="edc72-117">对于此示例中，数值加/减控件应仅允许为 2 的幂的值： 1、 2、 4、 8、 16、 32、 64，依此类推。</span><span class="sxs-lookup"><span data-stu-id="edc72-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="edc72-118">因此，当用户想要增加的值时执行的方法必须两倍的旧值;另一种方法必须值除以两个。</span><span class="sxs-lookup"><span data-stu-id="edc72-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="edc72-119">这是完整的 web 服务：</span><span class="sxs-lookup"><span data-stu-id="edc72-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="edc72-120">最后，创建一个新的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="edc72-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="edc72-121">像往常一样，需要`ScriptManager`控件，`TextBox`控件和一个`NumericUpDownExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="edc72-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="edc72-122">对于后者，你必须提供 web 服务信息：</span><span class="sxs-lookup"><span data-stu-id="edc72-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="edc72-123">`ServiceDownMethod` web 方法或页面方法的列表名称</span><span class="sxs-lookup"><span data-stu-id="edc72-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="edc72-124">`ServiceDownPath` 向下的服务方法; 与 web 服务的路径如果使用的页面方法，忽略</span><span class="sxs-lookup"><span data-stu-id="edc72-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="edc72-125">`ServiceUpMethod` 名称最多的 web 方法或页面方法</span><span class="sxs-lookup"><span data-stu-id="edc72-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="edc72-126">`ServiceUpPath` 与最服务方法; web 服务的路径如果使用的页面方法，忽略</span><span class="sxs-lookup"><span data-stu-id="edc72-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="edc72-127">下面是页面的完整标记：</span><span class="sxs-lookup"><span data-stu-id="edc72-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="edc72-128">如果运行该页面，请注意如何在文本框中的值始终加倍时单击上部的按钮，并单击低按钮时，减少了一半。</span><span class="sxs-lookup"><span data-stu-id="edc72-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="edc72-129">[![出现是 2 的幂的数字](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="edc72-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="edc72-130">出现是 2 的幂的数字 ([单击此项可查看原尺寸图像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="edc72-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="edc72-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="edc72-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
