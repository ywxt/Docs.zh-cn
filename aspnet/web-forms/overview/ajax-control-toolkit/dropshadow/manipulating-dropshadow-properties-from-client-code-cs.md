---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 操作 Dropshadow 从客户端代码 (C#) |Microsoft Docs
author: wenz
description: 自定义 DataList 的编辑界面
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: e3166b9da97a0f4097566b62ba52b6d672eab78f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377280"
---
<a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="06895-103">操作 Dropshadow 从客户端代码 (C#)</span><span class="sxs-lookup"><span data-stu-id="06895-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>
====================
<span data-ttu-id="06895-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="06895-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="06895-105">[下载代码](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="06895-105">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="06895-106">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="06895-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="06895-107">此外可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="06895-107">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="06895-108">概述</span><span class="sxs-lookup"><span data-stu-id="06895-108">Overview</span></span>

<span data-ttu-id="06895-109">AJAX 控件工具包中的 DropShadow 控件扩展具有投影的面板。</span><span class="sxs-lookup"><span data-stu-id="06895-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="06895-110">此外可以使用客户端 JavaScript 代码更改此扩展器的属性。</span><span class="sxs-lookup"><span data-stu-id="06895-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="06895-111">步骤</span><span class="sxs-lookup"><span data-stu-id="06895-111">Steps</span></span>

<span data-ttu-id="06895-112">代码开头包含几行文本的面板：</span><span class="sxs-lookup"><span data-stu-id="06895-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="06895-113">关联的 CSS 类为面板提供了一种很好的背景色：</span><span class="sxs-lookup"><span data-stu-id="06895-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="06895-114">`DropShadowExtender`添加进来以扩展面板中的投影效果，设置为 50%的不透明度：</span><span class="sxs-lookup"><span data-stu-id="06895-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="06895-115">然后，ASP.NET AJAX`ScriptManager`控件使控件工具包，以便：</span><span class="sxs-lookup"><span data-stu-id="06895-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="06895-116">另一个面板包含用于设置投影的不透明度的两个 JavaScript 链接： 减号链接会降低阴影的不透明度，加上链接会增加它。</span><span class="sxs-lookup"><span data-stu-id="06895-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="06895-117">JavaScript 函数`changeOpacity()`然后必须首先找到`DropShadowExtender`页上的控件。</span><span class="sxs-lookup"><span data-stu-id="06895-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="06895-118">ASP.NET AJAX 定义`$find()`完全该任务的方法。</span><span class="sxs-lookup"><span data-stu-id="06895-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="06895-119">然后，将`get_Opacity()`方法检索当前不透明度，`set_Opacity()`方法将其设置。</span><span class="sxs-lookup"><span data-stu-id="06895-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="06895-120">JavaScript 代码然后将当前的不透明度值放入`<label>`元素：</span><span class="sxs-lookup"><span data-stu-id="06895-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


<span data-ttu-id="06895-121">[![在客户端上更改不透明度](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="06895-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="06895-122">在客户端上更改不透明度 ([单击此项可查看原尺寸图像](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="06895-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="06895-123">[上一页](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [下一页](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="06895-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
