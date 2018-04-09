---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 使用 Web 服务后端 (VB) 中创建数值加/减控件 |Microsoft 文档
author: wenz
description: 而不是让用户在复选框中键入一个值，数字向上/向下 （即在 Windows 和其他操作系统的系统上存在） 的控件无法证明随着更多 c...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 690fd89c552407ec5d77419aae2488e4832efe44
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="4aaa8-103">使用 Web 服务后端 (VB) 中创建数值向上/向下控件</span><span class="sxs-lookup"><span data-stu-id="4aaa8-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>
====================
<span data-ttu-id="4aaa8-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4aaa8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4aaa8-105">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4aaa8-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="4aaa8-106">而不是让用户在复选框中键入一个值，数字加/减控件 （即在 Windows 和其他操作系统的系统上存在） 无法证明随着更多喜欢。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="4aaa8-107">默认情况下，NumericUpDown 控件始终增加或减少值 1，但 web 服务证明更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="4aaa8-108">概述</span><span class="sxs-lookup"><span data-stu-id="4aaa8-108">Overview</span></span>

<span data-ttu-id="4aaa8-109">而不是让用户在复选框中键入一个值，数字加/减控件 （即在 Windows 和其他操作系统的系统上存在） 无法证明随着更多喜欢。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="4aaa8-110">默认情况下，`NumericUpDown`控件始终增加或减少值 1，但 web 服务证明更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="4aaa8-111">步骤</span><span class="sxs-lookup"><span data-stu-id="4aaa8-111">Steps</span></span>

<span data-ttu-id="4aaa8-112">ASP.NET AJAX 控件工具包中包含`NumericUpDown`会自动将两个按钮添加到文本框中的扩展： 一个用于增加其值，一个用于减少它。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="4aaa8-113">但是该控件还支持的 web 服务调用 （或页方法调用）。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="4aaa8-114">每当向上或向下按钮单击后的 JavaScript 代码连接到 web 服务器并执行的方法存在。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="4aaa8-115">方法签名是以下之一：</span><span class="sxs-lookup"><span data-stu-id="4aaa8-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="4aaa8-116">`current`自变量是在文本框中; 的当前值`tag`属性是可以作为属性的设置的其他上下文数据`NumericUpDown`扩展程序 （但不是必需的）。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="4aaa8-117">对于此示例，数值加/减控件应仅允许为 2 的幂的值： 1、 2、 4、 8、 16、 32、 64，依次类推。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="4aaa8-118">因此，当用户想要增加值时执行的方法必须 double 的旧值;另一种方法必须将除以两个值。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="4aaa8-119">因此下面是完整的 web 服务：</span><span class="sxs-lookup"><span data-stu-id="4aaa8-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="4aaa8-120">最后，创建一个新的 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="4aaa8-121">像往常一样，你需要`ScriptManager`控件，`TextBox`控件和`NumericUpDownExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="4aaa8-122">对于后者，你需要提供 web 服务信息：</span><span class="sxs-lookup"><span data-stu-id="4aaa8-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="4aaa8-123">`ServiceDownMethod` 名称下的 web 方法或页面方法</span><span class="sxs-lookup"><span data-stu-id="4aaa8-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="4aaa8-124">`ServiceDownPath` 使用向下的服务方法; web 服务的路径如果你使用页方法，忽略</span><span class="sxs-lookup"><span data-stu-id="4aaa8-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="4aaa8-125">`ServiceUpMethod` 名称最多的 web 方法或页面方法</span><span class="sxs-lookup"><span data-stu-id="4aaa8-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="4aaa8-126">`ServiceUpPath` 具有最服务方法; web 服务的路径如果你使用页方法，忽略</span><span class="sxs-lookup"><span data-stu-id="4aaa8-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="4aaa8-127">下面是页的完整标记：</span><span class="sxs-lookup"><span data-stu-id="4aaa8-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="4aaa8-128">如果运行页面时，请注意如何在文本框中的值始终增加一倍时单击上限按钮，并单击较低的按钮时，减少了一半。</span><span class="sxs-lookup"><span data-stu-id="4aaa8-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="4aaa8-129">[![是 2 的幂的数字显示](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4aaa8-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="4aaa8-130">是 2 的幂的数字显示 ([单击以查看实际尺寸的图像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4aaa8-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4aaa8-131">上一篇</span><span class="sxs-lookup"><span data-stu-id="4aaa8-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
