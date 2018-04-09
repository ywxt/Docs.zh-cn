---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: 使用 ReorderList (VB) 的回发 |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供可由用户通过拖放重新排序的列表。 每当列表重新排序后，采购订单...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: ef43471f7d8cc94c1a82a368e27acef05f474f81
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="381fd-104">回发使用 ReorderList (VB)</span><span class="sxs-lookup"><span data-stu-id="381fd-104">Using Postbacks with ReorderList (VB)</span></span>
====================
<span data-ttu-id="381fd-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="381fd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="381fd-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="381fd-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="381fd-107">AJAX 控件工具包中的 ReorderList 控件提供可由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="381fd-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="381fd-108">列表重新排序后，每当回发应通知的更改的服务器。</span><span class="sxs-lookup"><span data-stu-id="381fd-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="381fd-109">概述</span><span class="sxs-lookup"><span data-stu-id="381fd-109">Overview</span></span>

<span data-ttu-id="381fd-110">`ReorderList` AJAX 控件工具包中的控件提供可由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="381fd-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="381fd-111">列表重新排序后，每当回发应通知的更改的服务器。</span><span class="sxs-lookup"><span data-stu-id="381fd-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="381fd-112">步骤</span><span class="sxs-lookup"><span data-stu-id="381fd-112">Steps</span></span>

<span data-ttu-id="381fd-113">有几个可能的数据源`ReorderList`控件。</span><span class="sxs-lookup"><span data-stu-id="381fd-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="381fd-114">一个是使用`XmlDataSource`控件：</span><span class="sxs-lookup"><span data-stu-id="381fd-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="381fd-115">若要将绑定到此 XML`ReorderList`必须设置控制并启用回发，以下属性：</span><span class="sxs-lookup"><span data-stu-id="381fd-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="381fd-116">`DataSourceID`： 数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="381fd-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="381fd-117">`SortOrderField`： 要作为排序依据的属性</span><span class="sxs-lookup"><span data-stu-id="381fd-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="381fd-118">`AllowReorder`： 是否允许用户重新排列列表元素</span><span class="sxs-lookup"><span data-stu-id="381fd-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="381fd-119">`PostBackOnReorder`： 是否创建回发时重新排列列表</span><span class="sxs-lookup"><span data-stu-id="381fd-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="381fd-120">下面是相应的控件的标记：</span><span class="sxs-lookup"><span data-stu-id="381fd-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="381fd-121">在`ReorderList`可能使用绑定控件，数据源中的特定数据`Eval()`方法：</span><span class="sxs-lookup"><span data-stu-id="381fd-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="381fd-122">在页面上任意位置，标签将在实际应用最后一个重新排序发生时保存的信息：</span><span class="sxs-lookup"><span data-stu-id="381fd-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="381fd-123">此标签填入处理回发的服务器端代码中的文本：</span><span class="sxs-lookup"><span data-stu-id="381fd-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="381fd-124">最后，以便激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`控件必须放置在页面上：</span><span class="sxs-lookup"><span data-stu-id="381fd-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


<span data-ttu-id="381fd-125">[![每个重新排序触发回发](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="381fd-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="381fd-126">每个重新排序触发回发 ([单击以查看实际尺寸的图像](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="381fd-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="381fd-127">[上一页](drag-and-drop-via-reorderlist-cs.md)
> [下一页](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="381fd-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
