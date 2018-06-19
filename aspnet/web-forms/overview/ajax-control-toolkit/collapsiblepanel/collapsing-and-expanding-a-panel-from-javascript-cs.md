---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: 展开和折叠的面板从 JavaScript (C#) |Microsoft 文档
author: wenz
description: ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展一个面板，并为它提供的功能折叠其内容，并将其展开...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 7baa3be7144946bde7d11afd9b1cb5f14ad9dede
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875534"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="6f09b-103">展开和折叠的面板从 JavaScript (C#)</span><span class="sxs-lookup"><span data-stu-id="6f09b-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>
====================
<span data-ttu-id="6f09b-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6f09b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6f09b-105">[下载代码](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6f09b-105">[Download Code](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="6f09b-106">ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展一个面板，并为它提供的功能折叠其内容，并再次将其展开。</span><span class="sxs-lookup"><span data-stu-id="6f09b-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="6f09b-107">这两个操作也可以通过自定义 JavaScript 代码来触发。</span><span class="sxs-lookup"><span data-stu-id="6f09b-107">These two actions can also be triggered from custom JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="6f09b-108">概述</span><span class="sxs-lookup"><span data-stu-id="6f09b-108">Overview</span></span>

<span data-ttu-id="6f09b-109">ASP.NET AJAX 控件工具包中的 CollapsiblePanel 控件扩展一个面板，并为它提供的功能折叠其内容，并再次将其展开。</span><span class="sxs-lookup"><span data-stu-id="6f09b-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="6f09b-110">这两个操作也可以通过自定义 JavaScript 代码来触发。</span><span class="sxs-lookup"><span data-stu-id="6f09b-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="6f09b-111">步骤</span><span class="sxs-lookup"><span data-stu-id="6f09b-111">Steps</span></span>

<span data-ttu-id="6f09b-112">首先，创建一个新的 ASP.NET 页并包括`ScriptManager`中`<form>`元素。</span><span class="sxs-lookup"><span data-stu-id="6f09b-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="6f09b-113">这将加载的 ASP.NET AJAX 库所需的控件工具包：</span><span class="sxs-lookup"><span data-stu-id="6f09b-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="6f09b-114">然后，使用一些文本创建一个面板，因此，可以看见折叠/展开效果：</span><span class="sxs-lookup"><span data-stu-id="6f09b-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="6f09b-115">如你所见，面板将引用的 CSS 类用于 （现在基本上定义背景色和面板的宽度） 如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f09b-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="6f09b-116">`CollapsiblePanelExtender`控件要求`TargetControlID`属性，以便该工具包知道哪个面板以折叠或展开发出请求后：</span><span class="sxs-lookup"><span data-stu-id="6f09b-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="6f09b-117">遗憾的是，扩展程序当前未公开特定 API 的折叠或展开面板中，但某些未记录的方法都将执行。</span><span class="sxs-lookup"><span data-stu-id="6f09b-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="6f09b-118">首先，将三个 HTML 按钮添加到然后触发客户端 JavaScript 以折叠或展开面板中的内容的页面：</span><span class="sxs-lookup"><span data-stu-id="6f09b-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="6f09b-119">在客户端 JavaScript 代码 (入门`<script type="text/javascript">`)，则`$find()`方法需要使用访问`CollapsiblePanelExtender`。</span><span class="sxs-lookup"><span data-stu-id="6f09b-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="6f09b-120">`$find("cpe")` 将返回对它的引用。</span><span class="sxs-lookup"><span data-stu-id="6f09b-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="6f09b-121">从该处上，特定的方法将解决手头的任务。</span><span class="sxs-lookup"><span data-stu-id="6f09b-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="6f09b-122">方法 （扩展） 中打开面板称为`_doOpen()`; 下面的代码实现`doOpen()`单击第一个按钮时调用的函数：</span><span class="sxs-lookup"><span data-stu-id="6f09b-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="6f09b-123">用于关闭，或折叠面板，`_doClose()`方法需要执行。</span><span class="sxs-lookup"><span data-stu-id="6f09b-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="6f09b-124">因此当用户单击第二个按钮上时，调用下面的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="6f09b-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="6f09b-125">第三个按钮切换面板的状态： 从折叠到已展开，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="6f09b-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="6f09b-126">`CollapsiblePanelExtender`公开`toggle()`后者执行具体的方法： 反转面板的状态。</span><span class="sxs-lookup"><span data-stu-id="6f09b-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="6f09b-127">但是还有另一种方法 (内部使用`toggle()`方法):`get_Collapsed()`方法`CollapsiblePanelExtender()`告诉我们是否折叠的面板。</span><span class="sxs-lookup"><span data-stu-id="6f09b-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="6f09b-128">根据此函数的返回值，面板为则可以展开 (`_doOpen()`方法) 或折叠 (`_doClose()`) 方法：</span><span class="sxs-lookup"><span data-stu-id="6f09b-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


<span data-ttu-id="6f09b-129">[![第三个按钮更改面板的状态： 从折叠到展开且后](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f09b-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f09b-130">第三个按钮更改面板的状态： 从折叠到展开且后 ([单击以查看实际尺寸的图像](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6f09b-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6f09b-131">下一篇</span><span class="sxs-lookup"><span data-stu-id="6f09b-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
