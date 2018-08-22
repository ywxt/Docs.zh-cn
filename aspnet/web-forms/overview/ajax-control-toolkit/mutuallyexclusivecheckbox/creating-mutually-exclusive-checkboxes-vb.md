---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 创建互斥复选框 (VB) |Microsoft Docs
author: wenz
description: 可以选择仅一组选项之一，通常用于单选按钮。 但还有一个缺点： 选择一个单选按钮组中的后，...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd338b622779b64dd59f9cf6f3e2365ef5cb3ffb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824731"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="f177a-104">创建互斥复选框 (VB)</span><span class="sxs-lookup"><span data-stu-id="f177a-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>
====================
<span data-ttu-id="f177a-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f177a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f177a-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f177a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="f177a-107">可以选择仅一组选项之一，通常用于单选按钮。</span><span class="sxs-lookup"><span data-stu-id="f177a-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="f177a-108">但还有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="f177a-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="f177a-109">复选框可以在任何时候是未选中状态，但是不是互相排斥。</span><span class="sxs-lookup"><span data-stu-id="f177a-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="f177a-110">本教程提供了最佳的这两种方法： 是互斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="f177a-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="f177a-111">概述</span><span class="sxs-lookup"><span data-stu-id="f177a-111">Overview</span></span>

<span data-ttu-id="f177a-112">可以选择仅一组选项之一，通常用于单选按钮。</span><span class="sxs-lookup"><span data-stu-id="f177a-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="f177a-113">但还有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="f177a-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="f177a-114">复选框可以在任何时候是未选中状态，但是不是互相排斥。</span><span class="sxs-lookup"><span data-stu-id="f177a-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="f177a-115">本教程提供了最佳的这两种方法： 是互斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="f177a-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="f177a-116">步骤</span><span class="sxs-lookup"><span data-stu-id="f177a-116">Steps</span></span>

<span data-ttu-id="f177a-117">ASP.NET AJAX 控件工具包包含 MutuallyExclusiveCheckBox 扩展器。</span><span class="sxs-lookup"><span data-stu-id="f177a-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="f177a-118">这使程序员可以分配给组名称的任何复选框 (`Key`属性)。</span><span class="sxs-lookup"><span data-stu-id="f177a-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="f177a-119">从同一组中的所有复选框，只有一个可能一次选择。</span><span class="sxs-lookup"><span data-stu-id="f177a-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="f177a-120">让我们开始新的 ASP.NET 页面上放置两个复选框。</span><span class="sxs-lookup"><span data-stu-id="f177a-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="f177a-121">可以有多个，但其中的两个已足够用于演示的原则：</span><span class="sxs-lookup"><span data-stu-id="f177a-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="f177a-122">对于这两个复选框，必须将页上放 MutuallyExclusiveCheckBoxExtender 控件。</span><span class="sxs-lookup"><span data-stu-id="f177a-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="f177a-123">这两个键属性需要具有相同的值，就像 HTML 单选按钮元素的属性必须完全相同，表示一的组所属的值。</span><span class="sxs-lookup"><span data-stu-id="f177a-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="f177a-124">扩展器的 TargetControlID 属性指向复选框的 ID。</span><span class="sxs-lookup"><span data-stu-id="f177a-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="f177a-125">最后，包括 ASP.NET AJAX`ScriptManager`所需 ASP.NET AJAX 控件工具包中的所有元素：</span><span class="sxs-lookup"><span data-stu-id="f177a-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="f177a-126">保存并运行此页： 您可以选中和取消选中这两个复选框，但是在任何时间可以两个复选框进行检查。</span><span class="sxs-lookup"><span data-stu-id="f177a-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="f177a-127">[![可以一次选中一个复选框](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f177a-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="f177a-128">可以一次选中一个复选框 ([单击此项可查看原尺寸图像](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f177a-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f177a-129">上一篇</span><span class="sxs-lookup"><span data-stu-id="f177a-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
