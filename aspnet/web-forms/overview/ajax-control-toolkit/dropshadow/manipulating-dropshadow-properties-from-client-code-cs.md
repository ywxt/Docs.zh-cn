---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 操作从客户端代码 (C#) 的 DropShadow 属性 |Microsoft 文档
author: wenz
description: 自定义 DataList 的编辑界面
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 37a7784e1d42477e31938e1d15495993ac86fc56
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870331"
---
<a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="5588a-103">操作从客户端代码 (C#) 的 DropShadow 属性</span><span class="sxs-lookup"><span data-stu-id="5588a-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>
====================
<span data-ttu-id="5588a-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5588a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5588a-105">[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5588a-105">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="5588a-106">AJAX 控件工具包中的 DropShadow 控件扩展带投影一个面板。</span><span class="sxs-lookup"><span data-stu-id="5588a-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5588a-107">此外可以使用客户端 JavaScript 代码更改的此扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="5588a-107">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="5588a-108">概述</span><span class="sxs-lookup"><span data-stu-id="5588a-108">Overview</span></span>

<span data-ttu-id="5588a-109">AJAX 控件工具包中的 DropShadow 控件扩展带投影一个面板。</span><span class="sxs-lookup"><span data-stu-id="5588a-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="5588a-110">此外可以使用客户端 JavaScript 代码更改的此扩展的属性。</span><span class="sxs-lookup"><span data-stu-id="5588a-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="5588a-111">步骤</span><span class="sxs-lookup"><span data-stu-id="5588a-111">Steps</span></span>

<span data-ttu-id="5588a-112">代码开头面板包含某些行的文本：</span><span class="sxs-lookup"><span data-stu-id="5588a-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="5588a-113">关联的 CSS 类为面板提供了一种很好的背景色：</span><span class="sxs-lookup"><span data-stu-id="5588a-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="5588a-114">`DropShadowExtender`加以扩展与投影效果，设置为 50%的不透明度面板：</span><span class="sxs-lookup"><span data-stu-id="5588a-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="5588a-115">然后，ASP.NET AJAX`ScriptManager`控件使控件工具包工作：</span><span class="sxs-lookup"><span data-stu-id="5588a-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="5588a-116">另一个面板包含两个设置的不透明度的投影的 JavaScript 链接： 减号链接减少阴影的不透明度，加号链接会增加它。</span><span class="sxs-lookup"><span data-stu-id="5588a-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="5588a-117">JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。</span><span class="sxs-lookup"><span data-stu-id="5588a-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="5588a-118">ASP.NET AJAX 定义`$find()`完全该任务的方法。</span><span class="sxs-lookup"><span data-stu-id="5588a-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="5588a-119">然后，`get_Opacity()`方法检索当前的不透明度，`set_Opacity()`方法将其设置。</span><span class="sxs-lookup"><span data-stu-id="5588a-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="5588a-120">然后，JavaScript 代码将当前的不透明度值放入`<label>`元素：</span><span class="sxs-lookup"><span data-stu-id="5588a-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


<span data-ttu-id="5588a-121">[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5588a-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="5588a-122">在客户端上更改不透明度 ([单击以查看实际尺寸的图像](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5588a-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5588a-123">[上一页](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [下一页](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5588a-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
