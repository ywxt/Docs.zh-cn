---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 创建自定义路由 (C#) |Microsoft Docs
author: microsoft
description: 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。
ms.author: aspnetcontent
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: c8ba653579c5f983a7086d15cf6245eff527bfcf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827658"
---
<a name="creating-custom-routes-c"></a><span data-ttu-id="5a3cd-104">创建自定义路由 (C#)</span><span class="sxs-lookup"><span data-stu-id="5a3cd-104">Creating Custom Routes (C#)</span></span>
====================
<span data-ttu-id="5a3cd-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5a3cd-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5a3cd-106">了解如何将自定义路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="5a3cd-107">在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="5a3cd-108">在本教程中，您将学习如何将自定义的路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="5a3cd-109">了解如何修改自定义的路由在 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="5a3cd-110">对于许多简单的 ASP.NET MVC 应用程序，默认路由表将就可以正常工作。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="5a3cd-111">但是，可能会发现有专门的路由的需要。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="5a3cd-112">在这种情况下，可以创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="5a3cd-113">例如，假设您要生成的博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="5a3cd-114">你可能想要处理传入的请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5a3cd-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="5a3cd-115">/ 存档/12-25-2009 年</span><span class="sxs-lookup"><span data-stu-id="5a3cd-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="5a3cd-116">当用户输入此请求时，你想要返回到日期相对应的博客条目 2009 年 12 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="5a3cd-117">若要处理这种类型的请求，需要创建一个自定义路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="5a3cd-118">在列表 1 中的 Global.asax 文件包含一个新的自定义路由，名为博客，看起来像 /Archive/ 哪些句柄请求*条目日期*。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="5a3cd-119">**代码清单 1-Global.asax （具有自定义路由）**</span><span class="sxs-lookup"><span data-stu-id="5a3cd-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="5a3cd-120">您将添加到路由表路由的顺序非常重要。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="5a3cd-121">我们新的自定义博客路由添加到之前的现有默认路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="5a3cd-122">如果您颠倒顺序，则默认路由始终将获取调用而不是自定义路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="5a3cd-123">自定义博客路由匹配的开头/存档/任何请求。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="5a3cd-124">因此，它与匹配所有以下 Url:</span><span class="sxs-lookup"><span data-stu-id="5a3cd-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="5a3cd-125">/ 存档/12-25-2009 年</span><span class="sxs-lookup"><span data-stu-id="5a3cd-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="5a3cd-126">/ 存档/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="5a3cd-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="5a3cd-127">/ 存档/apple</span><span class="sxs-lookup"><span data-stu-id="5a3cd-127">/Archive/apple</span></span>

<span data-ttu-id="5a3cd-128">自定义的路由将传入请求映射到名为存档的控制器，并调用 Entry() 操作。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="5a3cd-129">当调用 Entry() 方法时，条目日期在作为一个名为 entryDate 参数传递。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="5a3cd-130">可以使用在代码清单 2 中的控制器使用博客自定义路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="5a3cd-131">**代码清单 2-ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="5a3cd-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="5a3cd-132">请注意，代码清单 2 中的 Entry() 方法接受类型为 DateTime 的参数。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="5a3cd-133">MVC 框架非常智能，可自动将条目日期从 URL 转换 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="5a3cd-134">如果 URL 中的条目日期参数不能转换为日期时间，将引发错误 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="5a3cd-135">**图 1-通过转换参数错误**</span><span class="sxs-lookup"><span data-stu-id="5a3cd-135">**Figure 1 - Error from converting parameter**</span></span>


<span data-ttu-id="5a3cd-136">[![新建项目对话框](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5a3cd-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="5a3cd-137">**图 01**： 通过转换参数的错误 ([单击以查看实际尺寸的图像](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5a3cd-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="5a3cd-138">总结</span><span class="sxs-lookup"><span data-stu-id="5a3cd-138">Summary</span></span>

<span data-ttu-id="5a3cd-139">本教程的目的是演示如何创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="5a3cd-140">您学习了如何将自定义的路由添加到表示博客条目在 Global.asax 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="5a3cd-141">我们讨论了如何将请求的博客条目映射到名为 ArchiveController 的控制器和名为 Entry() 的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="5a3cd-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5a3cd-142">[上一页](aspnet-mvc-controllers-overview-cs.md)
> [下一页](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5a3cd-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
