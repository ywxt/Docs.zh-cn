---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 创建互斥复选框 (VB) |Microsoft 文档
author: wenz
description: 如果可以选择仅一组的选项之一，通常将使用单选按钮。 但没有一个缺点： 选择一个单选按钮组中的后，...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: cdb93a080fb62cfdc7e3ff0604a1447e2bb99071
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874247"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="2e96f-104">创建互斥复选框 (VB)</span><span class="sxs-lookup"><span data-stu-id="2e96f-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>
====================
<span data-ttu-id="2e96f-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2e96f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2e96f-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2e96f-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="2e96f-107">如果可以选择仅一组的选项之一，通常将使用单选按钮。</span><span class="sxs-lookup"><span data-stu-id="2e96f-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="2e96f-108">但没有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="2e96f-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="2e96f-109">复选框在任何时候可以是未选中状态，但是不互相排斥。</span><span class="sxs-lookup"><span data-stu-id="2e96f-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="2e96f-110">本教程提供这两种方法的最佳： 是互斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="2e96f-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="2e96f-111">概述</span><span class="sxs-lookup"><span data-stu-id="2e96f-111">Overview</span></span>

<span data-ttu-id="2e96f-112">如果可以选择仅一组的选项之一，通常将使用单选按钮。</span><span class="sxs-lookup"><span data-stu-id="2e96f-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="2e96f-113">但没有一个缺点： 选择一个单选按钮组中的后，不能取消选中所有单选按钮。</span><span class="sxs-lookup"><span data-stu-id="2e96f-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="2e96f-114">复选框在任何时候可以是未选中状态，但是不互相排斥。</span><span class="sxs-lookup"><span data-stu-id="2e96f-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="2e96f-115">本教程提供这两种方法的最佳： 是互斥的复选框。</span><span class="sxs-lookup"><span data-stu-id="2e96f-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="2e96f-116">步骤</span><span class="sxs-lookup"><span data-stu-id="2e96f-116">Steps</span></span>

<span data-ttu-id="2e96f-117">ASP.NET AJAX 控件工具包中包含的 MutuallyExclusiveCheckBox 扩展程序。</span><span class="sxs-lookup"><span data-stu-id="2e96f-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="2e96f-118">这使程序员要分配给组名称的任何复选框 (`Key`属性)。</span><span class="sxs-lookup"><span data-stu-id="2e96f-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="2e96f-119">从同一组中的所有复选框，只有一个可能一次选择。</span><span class="sxs-lookup"><span data-stu-id="2e96f-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="2e96f-120">让我们开始使用新的 ASP.NET 页上将两个复选框。</span><span class="sxs-lookup"><span data-stu-id="2e96f-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="2e96f-121">可以有多个，但其中两个已足够用于演示原则：</span><span class="sxs-lookup"><span data-stu-id="2e96f-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="2e96f-122">为这两个复选框，必须将在页面上置于 MutuallyExclusiveCheckBoxExtender 控件。</span><span class="sxs-lookup"><span data-stu-id="2e96f-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="2e96f-123">这两个键属性需要具有相同的值，就像 HTML 单选按钮元素的属性必须相同来表示它们所属的组的值。</span><span class="sxs-lookup"><span data-stu-id="2e96f-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="2e96f-124">扩展程序的 TargetControlID 属性指向的复选框的 ID。</span><span class="sxs-lookup"><span data-stu-id="2e96f-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="2e96f-125">最后，包括 ASP.NET AJAX`ScriptManager`所需的 ASP.NET AJAX 控件工具包的所有元素：</span><span class="sxs-lookup"><span data-stu-id="2e96f-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="2e96f-126">保存并运行此页： 你可以检查并取消选中这两个复选框，但是在任何时间都可以两个复选框检查。</span><span class="sxs-lookup"><span data-stu-id="2e96f-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="2e96f-127">[![只有一个复选框可以检查一次](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2e96f-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="2e96f-128">只有一个复选框可以检查一次 ([单击以查看实际尺寸的图像](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2e96f-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2e96f-129">上一篇</span><span class="sxs-lookup"><span data-stu-id="2e96f-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
