---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 路由概述 (VB) |Microsoft 文档
author: StephenWalther
description: 在本教程中，Stephen Walther 演示 ASP.NET MVC framework 如何映射到控制器操作的浏览器请求。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: 3de0e21552a4aa03aa21f21a4e26028f1475f3e9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879200"
---
<a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="9e617-103">ASP.NET MVC 路由概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="9e617-103">ASP.NET MVC Routing Overview (VB)</span></span>
====================
<span data-ttu-id="9e617-104">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9e617-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9e617-105">在本教程中，Stephen Walther 演示 ASP.NET MVC framework 如何映射到控制器操作的浏览器请求。</span><span class="sxs-lookup"><span data-stu-id="9e617-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>


<span data-ttu-id="9e617-106">在本教程中，将向您介绍调用每个 ASP.NET MVC 应用程序的一个重要特征*ASP.NET 路由*。</span><span class="sxs-lookup"><span data-stu-id="9e617-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="9e617-107">ASP.NET 路由模块负责将传入的浏览器请求映射到特定的 MVC 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9e617-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="9e617-108">本教程结束时，你将了解如何标准路由表将请求映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9e617-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="9e617-109">使用默认路由表</span><span class="sxs-lookup"><span data-stu-id="9e617-109">Using the Default Route Table</span></span>

<span data-ttu-id="9e617-110">在创建新的 ASP.NET MVC 应用程序时，应用程序已配置为使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="9e617-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="9e617-111">ASP.NET 路由是在两个位置设置的。</span><span class="sxs-lookup"><span data-stu-id="9e617-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="9e617-112">首先，应用程序的 Web 配置文件（Web.config 文件）启用了 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="9e617-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="9e617-113">配置文件中有四个部分与路由相关：system.web.httpModules 节、system.web.httpHandlers 节、system.webserver.modules 节和 system.webserver.handlers 节。</span><span class="sxs-lookup"><span data-stu-id="9e617-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="9e617-114">请注意不要删除这些节，因为如果没有这些节，路由将不再起作用。</span><span class="sxs-lookup"><span data-stu-id="9e617-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="9e617-115">其次，更重要的是，路由表是在应用程序的 Global.asax 文件中创建的。</span><span class="sxs-lookup"><span data-stu-id="9e617-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="9e617-116">Global.asax 文件是一个特殊文件，其中包含 ASP.NET 应用程序生命周期事件的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="9e617-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="9e617-117">路由表在 Application Start 事件中创建。</span><span class="sxs-lookup"><span data-stu-id="9e617-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="9e617-118">列表 1 中的文件包含 ASP.NET MVC 应用程序的默认 Global.asax 文件。</span><span class="sxs-lookup"><span data-stu-id="9e617-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="9e617-119">**列表 1-Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="9e617-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="9e617-120">MVC 应用程序第一次启动时，会调用 Application\_Start() 方法。</span><span class="sxs-lookup"><span data-stu-id="9e617-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="9e617-121">此方法反过来会调用 RegisterRoutes() 方法。</span><span class="sxs-lookup"><span data-stu-id="9e617-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="9e617-122">RegisterRoutes() 方法负责创建路由表。</span><span class="sxs-lookup"><span data-stu-id="9e617-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="9e617-123">默认路由表包含一个路由（名为 Default）。</span><span class="sxs-lookup"><span data-stu-id="9e617-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="9e617-124">Default 路由将 URL 的第一个段映射到控制器名称、第二个段映射到控制器操作，第三个段映射到名为 **id** 的参数。</span><span class="sxs-lookup"><span data-stu-id="9e617-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="9e617-125">假设你为 web 浏览器的地址栏中输入以下 URL:</span><span class="sxs-lookup"><span data-stu-id="9e617-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="9e617-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="9e617-126">/Home/Index/3</span></span>

<span data-ttu-id="9e617-127">默认路由将此 URL 映射到以下参数：</span><span class="sxs-lookup"><span data-stu-id="9e617-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="9e617-128">控制器 = 主页</span><span class="sxs-lookup"><span data-stu-id="9e617-128">controller = Home</span></span>

- <span data-ttu-id="9e617-129">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="9e617-129">action = Index</span></span>

- <span data-ttu-id="9e617-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="9e617-130">id = 3</span></span>

<span data-ttu-id="9e617-131">在请求 URL /Home/索引/3 时，将执行下面的代码：</span><span class="sxs-lookup"><span data-stu-id="9e617-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="9e617-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="9e617-132">HomeController.Index(3)</span></span>

<span data-ttu-id="9e617-133">Default 路由包括所有三个参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="9e617-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="9e617-134">如果不提供控制器，控制器参数将默认为 **Home**。</span><span class="sxs-lookup"><span data-stu-id="9e617-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="9e617-135">如果不提供操作，action 参数将默认为 **Index**。</span><span class="sxs-lookup"><span data-stu-id="9e617-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="9e617-136">最后，如果不提供 id，id 参数将默认为空字符串。</span><span class="sxs-lookup"><span data-stu-id="9e617-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="9e617-137">让我们看一下几个示例的默认路由如何映射到控制器操作的 Url。</span><span class="sxs-lookup"><span data-stu-id="9e617-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="9e617-138">假设以下 URL 输入到浏览器地址栏：</span><span class="sxs-lookup"><span data-stu-id="9e617-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="9e617-139">/Home</span><span class="sxs-lookup"><span data-stu-id="9e617-139">/Home</span></span>

<span data-ttu-id="9e617-140">由于 Default 路由参数存在默认值，输入此 URL 将导致 HomeController 类的 Index() 方法在列表 2 中被调用。</span><span class="sxs-lookup"><span data-stu-id="9e617-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="9e617-141">**列出 2-HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="9e617-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="9e617-142">在列出 2 中，HomeController 类包括一个名为接受单个参数名为 id。 的 index （） 方法URL /Home 导致 index （） 调用的方法将值作为 Id 参数的值执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="9e617-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="9e617-143">由于 MVC 框架调用控制器操作的方法，URL /Home 还将匹配中列出的 3 的 HomeController 类的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="9e617-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="9e617-144">**列出 3-HomeController.vb （不带参数的索引操作）**</span><span class="sxs-lookup"><span data-stu-id="9e617-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="9e617-145">中列出的 3 的 index （） 方法不接受任何参数。</span><span class="sxs-lookup"><span data-stu-id="9e617-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="9e617-146">URL /Home 会导致此 index （） 方法调用。</span><span class="sxs-lookup"><span data-stu-id="9e617-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="9e617-147">URL /Home/索引/3 也会调用此方法 （Id 将被忽略）。</span><span class="sxs-lookup"><span data-stu-id="9e617-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="9e617-148">URL /Home 还列出 4 中的 HomeController 类 index （） 方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="9e617-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="9e617-149">**列出 4-HomeController.vb （使用可以为 null 的参数的索引操作）**</span><span class="sxs-lookup"><span data-stu-id="9e617-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="9e617-150">在列出 4 中，index （） 方法具有一个整数参数。</span><span class="sxs-lookup"><span data-stu-id="9e617-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="9e617-151">由于该参数是可以为 null 的参数 （可具有值执行任何操作），则 index （） 可以调用而不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="9e617-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="9e617-152">最后，调用中使用 URL /Home 列出 5 的 index （） 方法将导致自 Id 参数异常*不*可以为 null 的参数。</span><span class="sxs-lookup"><span data-stu-id="9e617-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="9e617-153">如果你尝试调用 index （） 方法你获取所显示在图 1 中的错误。</span><span class="sxs-lookup"><span data-stu-id="9e617-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="9e617-154">**列出 5-HomeController.vb （使用 Id 参数的索引操作）**</span><span class="sxs-lookup"><span data-stu-id="9e617-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]


<span data-ttu-id="9e617-155">[![调用需要参数值的控制器操作](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9e617-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="9e617-156">**图 01**： 调用需要参数值的控制器操作 ([单击以查看实际尺寸的图像](asp-net-mvc-routing-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9e617-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>


<span data-ttu-id="9e617-157">URL /Home/索引/3 另一方面，会顺利运行，与列出 5 中的索引控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9e617-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="9e617-158">请求 /Home/Index/3 会导致具有值 3 的 Id 参数调用的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="9e617-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="9e617-159">总结</span><span class="sxs-lookup"><span data-stu-id="9e617-159">Summary</span></span>

<span data-ttu-id="9e617-160">本教程的目的是为你提供对 ASP.NET 路由的简短介绍。</span><span class="sxs-lookup"><span data-stu-id="9e617-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="9e617-161">获取与新的 ASP.NET MVC 应用程序的默认路由表，我们探讨。</span><span class="sxs-lookup"><span data-stu-id="9e617-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="9e617-162">你已了解默认路由如何映射到控制器操作的 Url。</span><span class="sxs-lookup"><span data-stu-id="9e617-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9e617-163">[上一页](creating-an-action-cs.md)
> [下一页](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9e617-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
