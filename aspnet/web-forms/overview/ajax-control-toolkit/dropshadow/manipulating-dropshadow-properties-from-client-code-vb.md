---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 操作从客户端代码 (VB) DropShadow 属性 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 DropShadow 控件扩展带投影一个面板。 此外可以使用客户端 JavaScrip 更改此扩展程序属性...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b5b024811ea511e67ce180169de9f0b7e3ef51d9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870903"
---
<a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="8a7bc-104">操作从客户端代码 (VB) DropShadow 属性</span><span class="sxs-lookup"><span data-stu-id="8a7bc-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>
====================
<span data-ttu-id="8a7bc-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8a7bc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8a7bc-106">[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="8a7bc-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="8a7bc-107">AJAX 控件工具包中的 DropShadow 控件扩展带投影一个面板。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8a7bc-108">此外可以使用客户端 JavaScript 代码更改的此扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-108">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="8a7bc-109">概述</span><span class="sxs-lookup"><span data-stu-id="8a7bc-109">Overview</span></span>

<span data-ttu-id="8a7bc-110">AJAX 控件工具包中的 DropShadow 控件扩展带投影一个面板。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8a7bc-111">此外可以使用客户端 JavaScript 代码更改的此扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8a7bc-112">步骤</span><span class="sxs-lookup"><span data-stu-id="8a7bc-112">Steps</span></span>

<span data-ttu-id="8a7bc-113">代码开头面板包含某些行的文本：</span><span class="sxs-lookup"><span data-stu-id="8a7bc-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="8a7bc-114">关联的 CSS 类为面板提供了一种很好的背景色：</span><span class="sxs-lookup"><span data-stu-id="8a7bc-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="8a7bc-115">`DropShadowExtender`加以扩展与投影效果，设置为 50%的不透明度面板：</span><span class="sxs-lookup"><span data-stu-id="8a7bc-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="8a7bc-116">然后，ASP.NET AJAX`ScriptManager`控件使控件工具包工作：</span><span class="sxs-lookup"><span data-stu-id="8a7bc-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="8a7bc-117">另一个面板包含两个设置的不透明度的投影的 JavaScript 链接： 减号链接减少阴影的不透明度，加号链接会增加它。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="8a7bc-118">JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="8a7bc-119">ASP.NET AJAX 定义`$find()`完全该任务的方法。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="8a7bc-120">然后，`get_Opacity()`方法检索当前的不透明度，`set_Opacity()`方法将其设置。</span><span class="sxs-lookup"><span data-stu-id="8a7bc-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="8a7bc-121">然后，JavaScript 代码将当前的不透明度值放入`<label>`元素：</span><span class="sxs-lookup"><span data-stu-id="8a7bc-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


<span data-ttu-id="8a7bc-122">[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8a7bc-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="8a7bc-123">在客户端上更改不透明度 ([单击以查看实际尺寸的图像](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8a7bc-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8a7bc-124">上一篇</span><span class="sxs-lookup"><span data-stu-id="8a7bc-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
