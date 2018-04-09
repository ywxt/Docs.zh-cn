---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 控制器概述 (VB) |Microsoft 文档
author: StephenWalther
description: 在本教程中，Stephen Walther 向你介绍 ASP.NET MVC 控制器。 了解如何创建新的控制器，并返回不同类型的操作 res...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: 0a45630e8f2d5ae0548bb6b8496df08ca5877a40
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="e5cf4-104">ASP.NET MVC 控制器概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="e5cf4-104">ASP.NET MVC Controller Overview (VB)</span></span>
====================
<span data-ttu-id="e5cf4-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e5cf4-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e5cf4-106">在本教程中，Stephen Walther 向你介绍 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="e5cf4-107">了解如何创建新的控制器，并返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-107">You learn how to create new controllers and return different types of action results.</span></span>


<span data-ttu-id="e5cf4-108">本教程介绍了 ASP.NET MVC 控制器、 控制器操作和操作结果的主题。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="e5cf4-109">完成本教程后，你将了解如何使用控制器来控制访问者与 ASP.NET MVC 网站交互的方式。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="e5cf4-110">了解控制器</span><span class="sxs-lookup"><span data-stu-id="e5cf4-110">Understanding Controllers</span></span>

<span data-ttu-id="e5cf4-111">MVC 控制器负责对针对 ASP.NET MVC 网站发出的请求的响应。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="e5cf4-112">每个浏览器请求映射到特定的控制器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="e5cf4-113">例如，假设你到你的浏览器的地址栏中输入以下 URL:</span><span class="sxs-lookup"><span data-stu-id="e5cf4-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e5cf4-114">在这种情况下，将调用名为 ProductController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="e5cf4-115">ProductController 负责生成对浏览器请求的响应。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="e5cf4-116">例如，在控制器可能会返回到浏览器返回的特定视图或控制器可能会将用户重定向到另一个控制器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="e5cf4-117">列表 1 包含名为 ProductController 的简单控制器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="e5cf4-118">**Listing1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="e5cf4-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="e5cf4-119">正如您可以看到从清单 1，控制器将是只是一个类 （Visual Basic.NET 或 C# 类）。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="e5cf4-120">控制器是从 System.Web.Mvc.Controller 基类派生的类。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="e5cf4-121">控制器由于控制器继承自这个基类，免费继承几个有用的方法 （我们将讨论在稍后这些方法）。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="e5cf4-122">了解控制器操作</span><span class="sxs-lookup"><span data-stu-id="e5cf4-122">Understanding Controller Actions</span></span>

<span data-ttu-id="e5cf4-123">控制器公开控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-123">A controller exposes controller actions.</span></span> <span data-ttu-id="e5cf4-124">操作是在浏览器地址栏中输入特定 URL 时被调用的控制器上的方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="e5cf4-125">例如，假设以下 url 发出请求：</span><span class="sxs-lookup"><span data-stu-id="e5cf4-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e5cf4-126">在这种情况下，ProductController 类上调用 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="e5cf4-127">Index （） 方法是控制器操作的示例。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="e5cf4-128">控制器操作必须是了控制器类的公共方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="e5cf4-129">Visual Basic.NET 方法，默认情况下，都是公共方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="e5cf4-130">请注意添加到控制器类中任何公共方法自动公开为控制器操作 （你务必要小心这由于控制器操作可以调用该领域的任何人都只需通过浏览器地址栏中键入正确的 URL）。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="e5cf4-131">没有控制器操作必须满足一些附加要求。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="e5cf4-132">用作控制器操作的方法不能重载。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="e5cf4-133">此外，控制器操作不能为静态方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="e5cf4-134">除此之外，你可以使用的控制器操作几乎任何方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="e5cf4-135">了解操作结果</span><span class="sxs-lookup"><span data-stu-id="e5cf4-135">Understanding Action Results</span></span>

<span data-ttu-id="e5cf4-136">控制器操作返回称为*操作结果*。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="e5cf4-137">操作结果是对浏览器请求响应中返回内容的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="e5cf4-138">ASP.NET MVC framework 支持几种类型的操作的结果，包括：</span><span class="sxs-lookup"><span data-stu-id="e5cf4-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="e5cf4-139">ViewResult-表示 HTML 和标记。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="e5cf4-140">EmptyResult-表示任何结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="e5cf4-141">RedirectResult-表示重定向到新 URL。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="e5cf4-142">JsonResult-表示可在 AJAX 应用程序的 JavaScript 对象表示法结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="e5cf4-143">JavaScriptResult-表示 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="e5cf4-144">ContentResult-表示文本结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="e5cf4-145">FileContentResult-表示一个可下载文件 （使用二进制内容）。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="e5cf4-146">FilePathResult-表示 （包括路径） 的可下载文件。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="e5cf4-147">FileStreamResult-表示一个可下载文件 （使用文件流）。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="e5cf4-148">所有这些操作结果从 ActionResult 基类继承。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="e5cf4-149">在大多数情况下，控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="e5cf4-150">例如，清单 2 中的索引控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="e5cf4-151">**Listing 2 - Controllers\BookController.vb**</span><span class="sxs-lookup"><span data-stu-id="e5cf4-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="e5cf4-152">当操作返回 ViewResult 时，HTML 返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="e5cf4-153">中列出的 2 的 index （） 方法返回到浏览器命名索引的视图。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="e5cf4-154">请注意中列出的 2 的 index （） 操作不返回 ViewResult()。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="e5cf4-155">相反，控制器基类的 View() 方法被调用。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="e5cf4-156">通常情况下，你不会返回操作结果直接。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="e5cf4-157">相反，你调用控制器基类的以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="e5cf4-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="e5cf4-158">查看-返回 ViewResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="e5cf4-159">重定向-返回 RedirectResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="e5cf4-160">RedirectToAction-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="e5cf4-161">RedirectToRoute-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="e5cf4-162">Json-返回 JsonResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="e5cf4-163">JavaScriptResult-返回 JavaScriptResult。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="e5cf4-164">内容-返回 ContentResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="e5cf4-165">文件-返回 FileContentResult、 FilePathResult 或 FileStreamResult 具体取决于参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="e5cf4-166">因此，如果你想要返回到浏览器的视图，则调用 View() 方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="e5cf4-167">如果你想要重定向到另一个控制器操作的用户，则调用 RedirectToAction() 方法。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="e5cf4-168">例如，清单 3 中的 Details() 操作显示的视图或将用户重定向到的 index （） 操作，具体取决于是否 Id 参数具有一个值。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="e5cf4-169">**列出 3-CustomerController.vb**</span><span class="sxs-lookup"><span data-stu-id="e5cf4-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="e5cf4-170">特殊的 ContentResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-170">The ContentResult action result is special.</span></span> <span data-ttu-id="e5cf4-171">你可以使用 ContentResult 操作结果返回为纯文本操作结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="e5cf4-172">例如，清单 4 中的 index （） 方法返回一条消息，以纯文本，而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="e5cf4-173">**列出 4-Controllers\StatusController.vb**</span><span class="sxs-lookup"><span data-stu-id="e5cf4-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="e5cf4-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="e5cf4-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="e5cf4-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="e5cf4-175">System.Web.Mvc.Controller</span></span>


[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="e5cf4-176">当调用 StatusController.Index() 操作时，则不会返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="e5cf4-177">相反，原始文本"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="e5cf4-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="e5cf4-178">返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-178">is returned to the browser.</span></span>

<span data-ttu-id="e5cf4-179">如果控制器操作返回的结果是不操作结果-例如，日期或整数-然后结果都包装在 ContentResult 自动。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="e5cf4-180">例如，在列出 5 WorkController index （） 操作调用时，日期是作为返回 ContentResult 自动。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="e5cf4-181">**列出 5-WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="e5cf4-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="e5cf4-182">列出 5 中的 index （） 操作返回的 DateTime 对象。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="e5cf4-183">ASP.NET MVC 框架将 DateTime 对象转换为字符串，并自动在 ContentResult 包装的日期时间值。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="e5cf4-184">浏览器接收的日期和时间作为纯文本。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="e5cf4-185">总结</span><span class="sxs-lookup"><span data-stu-id="e5cf4-185">Summary</span></span>

<span data-ttu-id="e5cf4-186">本教程的目的是为了向你介绍 ASP.NET MVC 控制器、 控制器操作和控制器操作结果的概念。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="e5cf4-187">在第一个部分中，您学习了如何将新的控制器添加到 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="e5cf4-188">接下来，您学习了如何公共方法的一个控制器到 universe 公开为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="e5cf4-189">最后，我们讨论了不同类型的操作可从控制器操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="e5cf4-190">具体而言，我们讨论了如何返回 ViewResult、 RedirectToActionResult 和 ContentResult 的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e5cf4-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e5cf4-191">[上一页](creating-a-custom-route-constraint-cs.md)
> [下一页](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e5cf4-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
