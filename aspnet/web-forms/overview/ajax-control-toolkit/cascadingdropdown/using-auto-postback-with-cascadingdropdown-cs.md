---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: 使用 CascadingDropDown (C#) 的自动回发 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 04e0914dd1057f9ce490f68ae3fa9c56766beafb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="1c71b-103">自动回发使用 CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="1c71b-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>
====================
<span data-ttu-id="1c71b-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1c71b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1c71b-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1c71b-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="1c71b-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="1c71b-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1c71b-107">但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件的有些功能不起作用，因为以异步方式将数据加载到列表生成的 （不必要的） 的回发本身。</span><span class="sxs-lookup"><span data-stu-id="1c71b-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="1c71b-108">使用的一些 JavaScript 代码，可以避免这种效果。</span><span class="sxs-lookup"><span data-stu-id="1c71b-108">With some JavaScript code, this effect can be avoided.</span></span>


## <a name="overview"></a><span data-ttu-id="1c71b-109">概述</span><span class="sxs-lookup"><span data-stu-id="1c71b-109">Overview</span></span>

<span data-ttu-id="1c71b-110">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="1c71b-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="1c71b-111">（例如，一个列表提供了一份我们状态，并且用处于该状态的主要城市然后填充下一个列表。）但是使用 CascadingDropDown 控件，ASP 时。NET 的 DropDownList 控件的有些功能不起作用，因为以异步方式将数据加载到列表生成的 （不必要的） 的回发本身。</span><span class="sxs-lookup"><span data-stu-id="1c71b-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="1c71b-112">使用的一些 JavaScript 代码，可以避免这种效果。</span><span class="sxs-lookup"><span data-stu-id="1c71b-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="1c71b-113">步骤</span><span class="sxs-lookup"><span data-stu-id="1c71b-113">Steps</span></span>

<span data-ttu-id="1c71b-114">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内&lt; `form` &gt;元素):</span><span class="sxs-lookup"><span data-stu-id="1c71b-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="1c71b-115">然后，需要进行的 DropDownList 控制：</span><span class="sxs-lookup"><span data-stu-id="1c71b-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="1c71b-116">对于此列表中，添加 CascadingDropDown 扩展程序以提供 web 服务 URL 和方法的信息：</span><span class="sxs-lookup"><span data-stu-id="1c71b-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="1c71b-117">然后 CascadingDropDown 扩展程序以异步方式调用具有以下方法签名的 web 服务：</span><span class="sxs-lookup"><span data-stu-id="1c71b-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="1c71b-118">该方法返回类型 CascadingDropDown 值的数组。</span><span class="sxs-lookup"><span data-stu-id="1c71b-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="1c71b-119">该类型的构造函数首先需要列表项的标题，然后值 (HTML`value`属性)。</span><span class="sxs-lookup"><span data-stu-id="1c71b-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="1c71b-120">加载浏览器中将填充下拉列表中的与三个供应商，第二个正在预先选定状态。</span><span class="sxs-lookup"><span data-stu-id="1c71b-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="1c71b-121">此外，ASP.NET 定义`__doPostBack()`JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="1c71b-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="1c71b-122">一旦已加载页面，此 JavaScript 调用添加到下拉列表中，但仅中是否存在元素它。</span><span class="sxs-lookup"><span data-stu-id="1c71b-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="1c71b-123">如果在列表中没有元素，该控件工具包当前正在加载它们，以便 JavaScript 代码使用超时，并尝试再次在半秒。</span><span class="sxs-lookup"><span data-stu-id="1c71b-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="1c71b-124">这样一来，在列表中没有实际元素且用户选择一个条目时，回发只执行。</span><span class="sxs-lookup"><span data-stu-id="1c71b-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>


<span data-ttu-id="1c71b-125">[![选择一个列表元素将导致回发](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1c71b-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="1c71b-126">选择一个列表元素将导致回发 ([单击以查看实际尺寸的图像](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1c71b-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c71b-127">[上一页](presetting-list-entries-with-cascadingdropdown-cs.md)
> [下一页](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1c71b-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
