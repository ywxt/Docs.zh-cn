---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET MVC 控制器概述 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 向您介绍 ASP.NET MVC 控制器。 了解如何创建新的控制器，并返回不同类型的操作 res...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: e9ec460d323866e231072ce587c25239141da711
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825068"
---
<a name="aspnet-mvc-controller-overview-c"></a><span data-ttu-id="2b6c2-104">ASP.NET MVC 控制器概述 (C#)</span><span class="sxs-lookup"><span data-stu-id="2b6c2-104">ASP.NET MVC Controller Overview (C#)</span></span>
====================
<span data-ttu-id="2b6c2-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="2b6c2-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="2b6c2-106">在本教程中，Stephen Walther 向您介绍 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="2b6c2-107">了解如何创建新的控制器，并返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-107">You learn how to create new controllers and return different types of action results.</span></span>


<span data-ttu-id="2b6c2-108">本教程探讨了 ASP.NET MVC 控制器、 控制器操作和操作结果的主题。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="2b6c2-109">完成本教程后，你将了解如何使用控制器控制与 ASP.NET MVC 网站访问者进行交互的方式。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="2b6c2-110">了解控制器</span><span class="sxs-lookup"><span data-stu-id="2b6c2-110">Understanding Controllers</span></span>

<span data-ttu-id="2b6c2-111">MVC 控制器负责响应对 ASP.NET MVC 网站发出的请求。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="2b6c2-112">每个浏览器请求映射到特定控制器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="2b6c2-113">例如，假设您的浏览器的地址栏中输入以下 URL:</span><span class="sxs-lookup"><span data-stu-id="2b6c2-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="2b6c2-114">在这种情况下，将调用名为 ProductController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="2b6c2-115">ProductController 负责生成对浏览器请求的响应。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="2b6c2-116">例如，在控制器可能会返回到浏览器返回的特定视图或控制器可能会将用户重定向到另一个控制器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="2b6c2-117">代码清单 1 包含名为 ProductController 的简单控制器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="2b6c2-118">**Listing1 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="2b6c2-118">**Listing1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

<span data-ttu-id="2b6c2-119">您可以看到从列表 1 中，控制器是只是一个类 （Visual Basic.NET 或 C# 类）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="2b6c2-120">控制器是从 system.web.mvc.controller 中衍生基类派生的类。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="2b6c2-121">由于从这个基类继承控制器，控制器将免费继承多个有用的方法 （我们将讨论在一段时间中这些方法）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="2b6c2-122">了解控制器操作</span><span class="sxs-lookup"><span data-stu-id="2b6c2-122">Understanding Controller Actions</span></span>

<span data-ttu-id="2b6c2-123">在控制器公开控制器操作。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-123">A controller exposes controller actions.</span></span> <span data-ttu-id="2b6c2-124">操作是在浏览器地址栏中输入特定的 URL 时调用的控制器上的方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="2b6c2-125">例如，假设以下 URL 发出请求：</span><span class="sxs-lookup"><span data-stu-id="2b6c2-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="2b6c2-126">在这种情况下，在 ProductController 类调用 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="2b6c2-127">Index （） 方法是控制器操作的示例。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="2b6c2-128">控制器操作必须是控制器类的公共方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="2b6c2-129">默认情况下，C# 方法，为私有方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-129">C# methods, by default, are private methods.</span></span> <span data-ttu-id="2b6c2-130">请注意到控制器类添加任何公共方法自动公开为控制器操作 （您必须小心这由于控制器操作可以调用 universe 中的任何人只需通过浏览器地址栏中键入正确的 URL）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="2b6c2-131">有一些必须满足的控制器操作的其他要求。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="2b6c2-132">不能重载用作控制器操作的方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="2b6c2-133">此外，控制器操作不能是静态方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="2b6c2-134">除此之外，可以使用任何方法作为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="2b6c2-135">了解操作结果</span><span class="sxs-lookup"><span data-stu-id="2b6c2-135">Understanding Action Results</span></span>

<span data-ttu-id="2b6c2-136">控制器操作返回所谓*操作结果*。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="2b6c2-137">操作结果是控制器操作返回到浏览器请求的响应中。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="2b6c2-138">ASP.NET MVC 框架支持多种类型的操作的结果，包括：</span><span class="sxs-lookup"><span data-stu-id="2b6c2-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="2b6c2-139">ViewResult-表示 HTML 和标记。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="2b6c2-140">EmptyResult-表示没有结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="2b6c2-141">RedirectResult-表示重定向到新 URL。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="2b6c2-142">JsonResult-表示可在 AJAX 应用程序的 JavaScript 对象表示法结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="2b6c2-143">JavaScriptResult-表示 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="2b6c2-144">ContentResult-表示文本结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="2b6c2-145">FileContentResult-表示可下载的文件 （具有二进制内容）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="2b6c2-146">FilePathResult-表示可下载的文件 （包括路径）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="2b6c2-147">FileStreamResult-表示一个可下载文件 （使用文件流）。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="2b6c2-148">所有这些操作的结果从 ActionResult 类的基类继承。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="2b6c2-149">在大多数情况下，控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="2b6c2-150">例如，在代码清单 2 中的索引控制器操作返回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="2b6c2-151">**代码清单 2-Controllers\BookController.cs**</span><span class="sxs-lookup"><span data-stu-id="2b6c2-151">**Listing 2 - Controllers\BookController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

<span data-ttu-id="2b6c2-152">当操作返回 ViewResult 时，HTML 返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="2b6c2-153">代码清单 2 中的 index （） 方法返回到浏览器名为 Index 的视图。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="2b6c2-154">请注意，代码清单 2 中的 index （） 操作不会返回 ViewResult()。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="2b6c2-155">相反，调用控制器的基类的 View() 方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="2b6c2-156">通常情况下，您不会返回一个操作结果直接。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="2b6c2-157">相反，您调用控制器的基类的以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="2b6c2-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="2b6c2-158">查看-返回一个 ViewResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="2b6c2-159">重定向-返回 RedirectResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="2b6c2-160">RedirectToAction-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="2b6c2-161">RedirectToRoute-返回 RedirectToRouteResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="2b6c2-162">Json-返回 JsonResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="2b6c2-163">JavaScriptResult-返回 JavaScriptResult。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="2b6c2-164">内容-返回 ContentResult 操作结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="2b6c2-165">文件-FileContentResult、 FilePathResult 或 FileStreamResult 具体取决于参数传递给该方法返回。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="2b6c2-166">因此，如果你想要返回到浏览器的视图，则调用 View() 方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="2b6c2-167">如果你想要从一个控制器操作到另一个将用户重定向，则调用 RedirectToAction() 方法。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="2b6c2-168">例如，清单 3 中的 Details() 操作显示的视图或将用户重定向到 index （） 操作，具体取决于 Id 参数是否具有值。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="2b6c2-169">**代码清单 3-CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="2b6c2-169">**Listing 3 - CustomerController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

<span data-ttu-id="2b6c2-170">ContentResult 操作结果比较特殊。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-170">The ContentResult action result is special.</span></span> <span data-ttu-id="2b6c2-171">您可以使用 ContentResult 操作结果返回操作结果以纯文本格式。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="2b6c2-172">例如，列表 4 中的 index （） 方法返回一条消息以明文形式而不是作为 HTML。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="2b6c2-173">**列表 4-Controllers\StatusController.cs**</span><span class="sxs-lookup"><span data-stu-id="2b6c2-173">**Listing 4 - Controllers\StatusController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

<span data-ttu-id="2b6c2-174">当调用 StatusController.Index() 操作时，则不会返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-174">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="2b6c2-175">相反，原始文本"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="2b6c2-175">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="2b6c2-176">返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-176">is returned to the browser.</span></span>

<span data-ttu-id="2b6c2-177">如果控制器操作返回的结果是不是一个操作结果-例如，日期或整数-然后将结果包装在 ContentResult 自动。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-177">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="2b6c2-178">例如，调用 WorkController 列表 5 中的 index （） 操作时，返回的日期是 ContentResult 为自动。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-178">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="2b6c2-179">**列表 5-WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="2b6c2-179">**Listing 5 - WorkController.cs**</span></span>

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

<span data-ttu-id="2b6c2-180">列表 5 中的 index （） 操作返回一个 DateTime 对象。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-180">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="2b6c2-181">ASP.NET MVC 框架将 DateTime 对象转换为字符串和日期时间值中 ContentResult 可以自动换行。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-181">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="2b6c2-182">在浏览器接收的日期和时间以纯文本格式。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-182">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="2b6c2-183">总结</span><span class="sxs-lookup"><span data-stu-id="2b6c2-183">Summary</span></span>

<span data-ttu-id="2b6c2-184">本教程的目的是向您介绍了 ASP.NET MVC 控制器、 控制器操作和控制器操作结果的概念。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-184">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="2b6c2-185">在第一个部分中，您学习了如何将新的控制器添加到 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-185">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="2b6c2-186">接下来，您学习了如何公共控制器方法被称为宇宙到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-186">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="2b6c2-187">最后，我们讨论了不同类型的操作可以从控制器操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-187">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="2b6c2-188">具体而言，我们讨论了如何从控制器操作返回一个 ViewResult，RedirectToActionResult 和 ContentResult。</span><span class="sxs-lookup"><span data-stu-id="2b6c2-188">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2b6c2-189">[上一页](creating-an-action-vb.md)
> [下一页](creating-custom-routes-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2b6c2-189">[Previous](creating-an-action-vb.md)
[Next](creating-custom-routes-cs.md)</span></span>
