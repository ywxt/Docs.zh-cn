---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 更改动画使用客户端代码 (VB) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。 此外可以动画...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f9b72576cc3a9e91827cfb40983821704621060
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="changing-an-animation-using-client-side-code-vb"></a><span data-ttu-id="72a70-104">更改动画使用客户端代码 (VB)</span><span class="sxs-lookup"><span data-stu-id="72a70-104">Changing an Animation Using Client-Side Code (VB)</span></span>
====================
<span data-ttu-id="72a70-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="72a70-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="72a70-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="72a70-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)</span></span>

> <span data-ttu-id="72a70-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="72a70-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="72a70-108">也可以使用自定义客户端 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="72a70-108">The animation can also be changed using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="72a70-109">概述</span><span class="sxs-lookup"><span data-stu-id="72a70-109">Overview</span></span>

<span data-ttu-id="72a70-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但一个整个框架，以向控件添加动画。</span><span class="sxs-lookup"><span data-stu-id="72a70-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="72a70-111">也可以使用自定义客户端 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="72a70-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="72a70-112">步骤</span><span class="sxs-lookup"><span data-stu-id="72a70-112">Steps</span></span>

<span data-ttu-id="72a70-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载后，使其可以使用该控件工具包：</span><span class="sxs-lookup"><span data-stu-id="72a70-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="72a70-114">动画将应用于如下所示的文本的一个面板中：</span><span class="sxs-lookup"><span data-stu-id="72a70-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="72a70-115">在关联 CSS 类中的面板，定义一种很好的背景色，并且还设置面板的宽度固定:</span><span class="sxs-lookup"><span data-stu-id="72a70-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="72a70-116">实际动画是由 HTML 按钮启动：</span><span class="sxs-lookup"><span data-stu-id="72a70-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="72a70-117">然后，将添加`AnimationExtender`到页中，提供`ID`、`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="72a70-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

<span data-ttu-id="72a70-118">请注意，没有任何`<Animations>`中的节点`AnimationExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="72a70-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="72a70-119">自定义 JavaScript 代码用于提供要用于该控件的动画。</span><span class="sxs-lookup"><span data-stu-id="72a70-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="72a70-120">服务器 API 与`AnimationExtender`，没有将动画尚未分配到扩展程序的轻松方法。</span><span class="sxs-lookup"><span data-stu-id="72a70-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="72a70-121">但是扩展程序确实公开了几种方法来读取和写入动画注册与各种事件 (`OnClick`， `OnLoad`，依次类推)。</span><span class="sxs-lookup"><span data-stu-id="72a70-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="72a70-122">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="72a70-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="72a70-123">返回值的格式`get_*()`函数和自变量的格式`set_*()`函数是一个 JSON 字符串，提供的对象表示形式的 XML 标记是什么。</span><span class="sxs-lookup"><span data-stu-id="72a70-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="72a70-124">目前，无法将传递一个对象，但可以从给定的动画读取某个对象 (`get_OnXXXBehavior()`方法)。</span><span class="sxs-lookup"><span data-stu-id="72a70-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="72a70-125">下面是一个 JSON 字符串 (不带分隔引号和精美格式) 表示动画触发了按钮，但通过调整其大小时和淡出在同一时间对面板进行动画处理：</span><span class="sxs-lookup"><span data-stu-id="72a70-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

<span data-ttu-id="72a70-126">下面的 JavaScript 代码将分配到此 JSON descripting`OnClick`动画的当前扩展程序并运行它：</span><span class="sxs-lookup"><span data-stu-id="72a70-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]


<span data-ttu-id="72a70-127">[![动画运行立即，无需单击鼠标 （，很少的标记）](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="72a70-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="72a70-128">动画会立即，运行没有鼠标单击 （且很少的标记） ([单击以查看实际尺寸的图像](changing-an-animation-using-client-side-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="72a70-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="72a70-129">[上一页](executing-animations-using-client-side-code-vb.md)
> [下一页](animating-an-updatepanel-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="72a70-129">[Previous](executing-animations-using-client-side-code-vb.md)
[Next](animating-an-updatepanel-control-vb.md)</span></span>
