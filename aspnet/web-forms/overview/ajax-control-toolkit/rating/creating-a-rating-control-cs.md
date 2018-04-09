---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 创建分级控件 (C#) |Microsoft 文档
author: wenz
description: 很多网站中，从电子商务到社区站点，其为用户提供到速率文章或项目。 这通常需要某些编码工作，但是我们具有...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: a48cf0ed9402e2875e87ba7bdb76afc5f501a670
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-rating-control-c"></a><span data-ttu-id="a714a-104">创建分级控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="a714a-104">Creating a Rating Control (C#)</span></span>
====================
<span data-ttu-id="a714a-105">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a714a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a714a-106">[下载代码](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a714a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="a714a-107">很多网站中，从电子商务到社区站点，其为用户提供到速率文章或项目。</span><span class="sxs-lookup"><span data-stu-id="a714a-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="a714a-108">这通常需要某些编码工作，但我们尚未控件工具包到我们的处理方法。</span><span class="sxs-lookup"><span data-stu-id="a714a-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="a714a-109">概述</span><span class="sxs-lookup"><span data-stu-id="a714a-109">Overview</span></span>

<span data-ttu-id="a714a-110">很多网站中，从电子商务到社区站点，其为用户提供到速率文章或项目。</span><span class="sxs-lookup"><span data-stu-id="a714a-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="a714a-111">这通常需要某些编码工作，但我们尚未控件工具包到我们的处理方法。</span><span class="sxs-lookup"><span data-stu-id="a714a-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="a714a-112">步骤</span><span class="sxs-lookup"><span data-stu-id="a714a-112">Steps</span></span>

<span data-ttu-id="a714a-113">首先，你需要 （至少） 两种类型的映像： 一个用于填充出分级项和空分级项。</span><span class="sxs-lookup"><span data-stu-id="a714a-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="a714a-114">分级项通常是星型或笑脸。</span><span class="sxs-lookup"><span data-stu-id="a714a-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="a714a-115">对于此方案中，源代码下载本教程的一部分找到三个文件、 smiley.png 和 empty.png 和 smiley done.png。</span><span class="sxs-lookup"><span data-stu-id="a714a-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="a714a-116">然后，创建一个新的 ASP.NET 文件并开始添加`ScriptManager`对它控制：</span><span class="sxs-lookup"><span data-stu-id="a714a-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="a714a-117">然后，将添加`Rating`ASP.NET AJAX 控件工具包中的控件。</span><span class="sxs-lookup"><span data-stu-id="a714a-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="a714a-118">需要为此示例设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="a714a-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="a714a-119">`CurrentRating` 要使用初始分级</span><span class="sxs-lookup"><span data-stu-id="a714a-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="a714a-120">`MaxRating` 最高评级</span><span class="sxs-lookup"><span data-stu-id="a714a-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="a714a-121">`EmptyStarCssClass` 要使用的分级项 （星号） 时的 CSS 类为空</span><span class="sxs-lookup"><span data-stu-id="a714a-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="a714a-122">`FilledStarCssClass` 填写要使用的分级项 （星号） 时的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="a714a-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="a714a-123">`StarCssClass` 要用于可见 stat 的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="a714a-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="a714a-124">`WaitingStarCssClass` 要使用星级发送回发到服务器时的 CSS 类</span><span class="sxs-lookup"><span data-stu-id="a714a-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="a714a-125">这是将创建具有五个级别控件的标记的其中一个填写最初的项 （表情符号）：</span><span class="sxs-lookup"><span data-stu-id="a714a-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="a714a-126">三个引用的 CSS 类现在需要显示相应的图像文件，这是很简单的操作使用 CSS:</span><span class="sxs-lookup"><span data-stu-id="a714a-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="a714a-127">请确保你提供的宽度和高度这三个图像，否则显示可能看起来有点 messed 向上。</span><span class="sxs-lookup"><span data-stu-id="a714a-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="a714a-128">最后，此级别的结果应是向用户显示 （或至少保存在数据库）。</span><span class="sxs-lookup"><span data-stu-id="a714a-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="a714a-129">因此，添加回发到服务器分级窗体的文本消息和提交按钮的输出的标签：</span><span class="sxs-lookup"><span data-stu-id="a714a-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="a714a-130">在服务器端代码中，访问级别控制通过其`ID`，然后访问其`CurrentRating`属性，它是所选的评级项，在我们的示例 0 和 5 之间的值的数目。</span><span class="sxs-lookup"><span data-stu-id="a714a-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="a714a-131">保存页，并将其加载到你的浏览器。</span><span class="sxs-lookup"><span data-stu-id="a714a-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="a714a-132">当鼠标悬停在 （最初为空） 评级项时，JavaScript 效果发生情况： 分级更改。</span><span class="sxs-lookup"><span data-stu-id="a714a-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="a714a-133">单击上的一套星，会保留当前的分级。</span><span class="sxs-lookup"><span data-stu-id="a714a-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="a714a-134">最后，在提交窗体时，服务器端代码将输出所选的评级。</span><span class="sxs-lookup"><span data-stu-id="a714a-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="a714a-135">[![使用最少的代码创建的分级系统](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a714a-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="a714a-136">使用最少的代码创建的分级系统 ([单击以查看实际尺寸的图像](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a714a-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a714a-137">下一篇</span><span class="sxs-lookup"><span data-stu-id="a714a-137">Next</span></span>](creating-a-rating-control-vb.md)
