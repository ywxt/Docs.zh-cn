---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 创建分级控件 (C#) |Microsoft Docs
author: wenz
description: 很多网站，电子商务到社区站点，从其用户提供到速率项目或项。 这通常需要一些编码工作，但我们确实有...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5776101d9e40f999806aefa5a9529dbef21af161
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824247"
---
<a name="creating-a-rating-control-c"></a><span data-ttu-id="19a2e-104">创建分级控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="19a2e-104">Creating a Rating Control (C#)</span></span>
====================
<span data-ttu-id="19a2e-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="19a2e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="19a2e-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="19a2e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="19a2e-107">很多网站，电子商务到社区站点，从其用户提供到速率项目或项。</span><span class="sxs-lookup"><span data-stu-id="19a2e-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="19a2e-108">这通常需要一些编码工作，但我们确实为我们提供有控件工具包。</span><span class="sxs-lookup"><span data-stu-id="19a2e-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="19a2e-109">概述</span><span class="sxs-lookup"><span data-stu-id="19a2e-109">Overview</span></span>

<span data-ttu-id="19a2e-110">很多网站，电子商务到社区站点，从其用户提供到速率项目或项。</span><span class="sxs-lookup"><span data-stu-id="19a2e-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="19a2e-111">这通常需要一些编码工作，但我们确实为我们提供有控件工具包。</span><span class="sxs-lookup"><span data-stu-id="19a2e-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="19a2e-112">步骤</span><span class="sxs-lookup"><span data-stu-id="19a2e-112">Steps</span></span>

<span data-ttu-id="19a2e-113">首先，需要 （至少） 两种类型的映像： 一个用于已填充评级项和一个用于空评级项。</span><span class="sxs-lookup"><span data-stu-id="19a2e-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="19a2e-114">评级项通常是一个星号或笑脸。</span><span class="sxs-lookup"><span data-stu-id="19a2e-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="19a2e-115">对于此方案，作为本教程中的源的代码下载内容的一部分找到三个文件、 smiley.png 和 empty.png 和笑脸 done.png。</span><span class="sxs-lookup"><span data-stu-id="19a2e-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="19a2e-116">然后，创建一个新的 ASP.NET 文件并开始添加`ScriptManager`对它控制：</span><span class="sxs-lookup"><span data-stu-id="19a2e-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="19a2e-117">然后，添加`Rating`ASP.NET AJAX 控件工具包中的控件。</span><span class="sxs-lookup"><span data-stu-id="19a2e-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="19a2e-118">以下属性需要为此示例设置：</span><span class="sxs-lookup"><span data-stu-id="19a2e-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="19a2e-119">`CurrentRating` 若要使用初始分级</span><span class="sxs-lookup"><span data-stu-id="19a2e-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="19a2e-120">`MaxRating` 最大评级</span><span class="sxs-lookup"><span data-stu-id="19a2e-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="19a2e-121">`EmptyStarCssClass` 要使用的分级项 (star) 时的 CSS 类为空</span><span class="sxs-lookup"><span data-stu-id="19a2e-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="19a2e-122">`FilledStarCssClass` 填写要使用的分级项 (star) 时的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="19a2e-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="19a2e-123">`StarCssClass` 要使用的可见状态的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="19a2e-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="19a2e-124">`WaitingStarCssClass` 要使用而星评级发送回发到服务器的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="19a2e-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="19a2e-125">下面是用于创建具有五个评级控件的标记和其中无填充，最初的项 （表情符号）：</span><span class="sxs-lookup"><span data-stu-id="19a2e-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="19a2e-126">三个引用的 CSS 类现在需要显示适当的图像文件，这是易于使用 CSS 来执行操作：</span><span class="sxs-lookup"><span data-stu-id="19a2e-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="19a2e-127">请确保提供的宽度和高度的三个映像，否则显示可能看起来有点 messed 向上。</span><span class="sxs-lookup"><span data-stu-id="19a2e-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="19a2e-128">最后，分级的结果应是向用户显示 （或至少保存在数据库中）。</span><span class="sxs-lookup"><span data-stu-id="19a2e-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="19a2e-129">因此，添加用于输出的回发到服务器分级窗体的文本消息和一个提交按钮的标签：</span><span class="sxs-lookup"><span data-stu-id="19a2e-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="19a2e-130">在服务器端代码中，访问分级控件通过其`ID`，然后访问其`CurrentRating`属性的所选的评级项目，在我们的示例值介于 0 到 5 之间的数。</span><span class="sxs-lookup"><span data-stu-id="19a2e-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="19a2e-131">保存页面，并将其加载到你的浏览器。</span><span class="sxs-lookup"><span data-stu-id="19a2e-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="19a2e-132">当将鼠标悬停 （最初为空） 分级项时，会发生 JavaScript 效果： 分级更改。</span><span class="sxs-lookup"><span data-stu-id="19a2e-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="19a2e-133">单击组星级，保留当前的分级。</span><span class="sxs-lookup"><span data-stu-id="19a2e-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="19a2e-134">最后，当用户提交窗体，服务器端代码将输出的所选的分级。</span><span class="sxs-lookup"><span data-stu-id="19a2e-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="19a2e-135">[![创建具有最少的代码的分级系统](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="19a2e-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="19a2e-136">创建分级系统具有最少的代码 ([单击此项可查看原尺寸图像](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="19a2e-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="19a2e-137">下一篇</span><span class="sxs-lookup"><span data-stu-id="19a2e-137">Next</span></span>](creating-a-rating-control-vb.md)
