---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 使用客户端代码 (VB) 更改动画 |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。 此外可以在动画...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: afb275e4e5155ceccb7e696cbf9d00de99a455f5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840727"
---
<a name="changing-an-animation-using-client-side-code-vb"></a><span data-ttu-id="11720-104">使用客户端代码 (VB) 更改动画</span><span class="sxs-lookup"><span data-stu-id="11720-104">Changing an Animation Using Client-Side Code (VB)</span></span>
====================
<span data-ttu-id="11720-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="11720-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="11720-106">[下载代码](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip)或[下载 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="11720-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)</span></span>

> <span data-ttu-id="11720-107">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="11720-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="11720-108">此外可以使用自定义客户端的 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="11720-108">The animation can also be changed using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="11720-109">概述</span><span class="sxs-lookup"><span data-stu-id="11720-109">Overview</span></span>

<span data-ttu-id="11720-110">ASP.NET AJAX 控件工具包中的动画控件不只是一个控件，但若要将动画添加到控件的整个框架。</span><span class="sxs-lookup"><span data-stu-id="11720-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="11720-111">此外可以使用自定义客户端的 JavaScript 代码更改动画。</span><span class="sxs-lookup"><span data-stu-id="11720-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="11720-112">步骤</span><span class="sxs-lookup"><span data-stu-id="11720-112">Steps</span></span>

<span data-ttu-id="11720-113">首先，包括`ScriptManager`在页中; 然后，ASP.NET AJAX 库加载时，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="11720-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="11720-114">动画将应用于文本的外观如下所示的面板：</span><span class="sxs-lookup"><span data-stu-id="11720-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="11720-115">在面板关联的 CSS 类，定义一种很好的背景色和还设置面板的固定的宽度：</span><span class="sxs-lookup"><span data-stu-id="11720-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="11720-116">通过 HTML 按钮会启动实际的动画：</span><span class="sxs-lookup"><span data-stu-id="11720-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="11720-117">然后，添加`AnimationExtender`到页上，提供`ID`，则`TargetControlID`属性和强制性`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="11720-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

<span data-ttu-id="11720-118">请注意，没有任何`<Animations>`中的节点`AnimationExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="11720-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="11720-119">自定义 JavaScript 代码用于提供与控件一起使用的动画。</span><span class="sxs-lookup"><span data-stu-id="11720-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="11720-120">与使用服务器 API 的`AnimationExtender`，没有无法轻松地将动画尚未分配给该扩展器。</span><span class="sxs-lookup"><span data-stu-id="11720-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="11720-121">但是扩展器确实公开了几种方法来读取和写入动画注册的各种事件 (`OnClick`， `OnLoad`，依此类推)。</span><span class="sxs-lookup"><span data-stu-id="11720-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="11720-122">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="11720-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="11720-123">返回值的格式`get_*()`函数和变量的格式`set_*()`函数是一个 JSON 字符串，提供的对象表示形式的 XML 标记是什么。</span><span class="sxs-lookup"><span data-stu-id="11720-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="11720-124">目前，没有方法来传递一个对象，但可以读取某个对象从给定的动画 (`get_OnXXXBehavior()`方法)。</span><span class="sxs-lookup"><span data-stu-id="11720-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="11720-125">下面是一个 JSON 字符串 (不带分隔引号和格式可以很好地) 表示动画触发的按钮，但调整其大小时和淡出在同一时间对面板进行动画处理：</span><span class="sxs-lookup"><span data-stu-id="11720-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

<span data-ttu-id="11720-126">以下 JavaScript 代码将分配到此 JSON descripting`OnClick`动画的当前扩展程序并运行它：</span><span class="sxs-lookup"><span data-stu-id="11720-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]


<span data-ttu-id="11720-127">[![动画立即运行而无需单击鼠标 （和使用很少标记）](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="11720-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="11720-128">动画立即运行不带鼠标单击 （和使用很少标记） ([单击此项可查看原尺寸图像](changing-an-animation-using-client-side-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="11720-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11720-129">[上一页](executing-animations-using-client-side-code-vb.md)
> [下一页](animating-an-updatepanel-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="11720-129">[Previous](executing-animations-using-client-side-code-vb.md)
[Next](animating-an-updatepanel-control-vb.md)</span></span>
