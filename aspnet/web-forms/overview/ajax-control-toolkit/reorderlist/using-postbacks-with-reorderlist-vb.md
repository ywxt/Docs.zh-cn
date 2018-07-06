---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: 通过 ReorderList (VB) 使用回发 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 ReorderList 控件提供了可以由用户通过拖放重新排序的列表。 只要列表重新排序，采购订单...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 20214db1c038f417944bd374bdaa8ce55d6d44aa
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838994"
---
<a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="d2158-104">通过 ReorderList (VB) 使用回发</span><span class="sxs-lookup"><span data-stu-id="d2158-104">Using Postbacks with ReorderList (VB)</span></span>
====================
<span data-ttu-id="d2158-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d2158-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d2158-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d2158-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="d2158-107">AJAX 控件工具包中的 ReorderList 控件提供了可以由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="d2158-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="d2158-108">只要列表重新排序，回发应通知更改的服务器。</span><span class="sxs-lookup"><span data-stu-id="d2158-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="d2158-109">概述</span><span class="sxs-lookup"><span data-stu-id="d2158-109">Overview</span></span>

<span data-ttu-id="d2158-110">`ReorderList` AJAX 控件工具包中的控件提供了可以由用户通过拖放重新排序的列表。</span><span class="sxs-lookup"><span data-stu-id="d2158-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="d2158-111">只要列表重新排序，回发应通知更改的服务器。</span><span class="sxs-lookup"><span data-stu-id="d2158-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="d2158-112">步骤</span><span class="sxs-lookup"><span data-stu-id="d2158-112">Steps</span></span>

<span data-ttu-id="d2158-113">有多个可能的数据来源的`ReorderList`控件。</span><span class="sxs-lookup"><span data-stu-id="d2158-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="d2158-114">一种是使用`XmlDataSource`控件：</span><span class="sxs-lookup"><span data-stu-id="d2158-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="d2158-115">若要将绑定到此 XML`ReorderList`必须设置控制和启用回发，以下属性：</span><span class="sxs-lookup"><span data-stu-id="d2158-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="d2158-116">`DataSourceID`： 数据源的 ID</span><span class="sxs-lookup"><span data-stu-id="d2158-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="d2158-117">`SortOrderField`： 要作为排序依据的属性</span><span class="sxs-lookup"><span data-stu-id="d2158-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="d2158-118">`AllowReorder`： 是否允许用户重新排列列表元素</span><span class="sxs-lookup"><span data-stu-id="d2158-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="d2158-119">`PostBackOnReorder`： 是否创建一个回发时重新排列列表</span><span class="sxs-lookup"><span data-stu-id="d2158-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="d2158-120">下面是控件的相应标记：</span><span class="sxs-lookup"><span data-stu-id="d2158-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="d2158-121">内`ReorderList`可能会使用绑定控件，数据源中的特定数据`Eval()`方法：</span><span class="sxs-lookup"><span data-stu-id="d2158-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="d2158-122">在任意位置的页上，标签将在实际应用的最后一个重新排序发生时保存的信息：</span><span class="sxs-lookup"><span data-stu-id="d2158-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="d2158-123">此标签填入处理回发的服务器端代码中的文本：</span><span class="sxs-lookup"><span data-stu-id="d2158-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="d2158-124">最后，若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须置于页面：</span><span class="sxs-lookup"><span data-stu-id="d2158-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


<span data-ttu-id="d2158-125">[![每个重新排序触发回发](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d2158-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="d2158-126">每个重新排序触发回发 ([单击此项可查看原尺寸图像](using-postbacks-with-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d2158-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2158-127">[上一页](drag-and-drop-via-reorderlist-cs.md)
> [下一页](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d2158-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
