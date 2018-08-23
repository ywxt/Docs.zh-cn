---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 了解操作筛选器 (C#) |Microsoft Docs
author: microsoft
description: 本教程的目的是说明操作筛选器。 操作筛选器是可应用于控制器操作-或整个控制器的属性...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c7706d8252d5a0271f1b9243fa8eb282f722654
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834122"
---
<a name="understanding-action-filters-c"></a><span data-ttu-id="48a86-104">了解操作筛选器 (C#)</span><span class="sxs-lookup"><span data-stu-id="48a86-104">Understanding Action Filters (C#)</span></span>
====================
<span data-ttu-id="48a86-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="48a86-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="48a86-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="48a86-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="48a86-107">本教程的目的是说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="48a86-108">操作筛选器是可应用于控制器操作-或整个 controller--修改在其中执行此操作的方式的属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="48a86-109">了解操作筛选器</span><span class="sxs-lookup"><span data-stu-id="48a86-109">Understanding Action Filters</span></span>

<span data-ttu-id="48a86-110">本教程的目的是说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="48a86-111">操作筛选器是可应用于控制器操作-或整个 controller--修改在其中执行此操作的方式的属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="48a86-112">ASP.NET MVC 框架包括多个操作筛选器：</span><span class="sxs-lookup"><span data-stu-id="48a86-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="48a86-113">OutputCache – 此操作筛选器将缓存指定的时间内的控制器操作的输出。</span><span class="sxs-lookup"><span data-stu-id="48a86-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="48a86-114">HandleError – 此操作筛选器处理时，将执行控制器操作引发的错误。</span><span class="sxs-lookup"><span data-stu-id="48a86-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="48a86-115">授权 – 此操作筛选器，可限制对特定用户或角色的访问。</span><span class="sxs-lookup"><span data-stu-id="48a86-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="48a86-116">此外可以创建自己的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="48a86-117">例如，你可能想要创建自定义操作筛选器，以实现自定义身份验证系统。</span><span class="sxs-lookup"><span data-stu-id="48a86-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="48a86-118">或者，你可能想要创建操作筛选器修改的控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="48a86-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="48a86-119">在本教程中，您将了解如何构建的基础知识，操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="48a86-120">我们创建记录到 Visual Studio 输出窗口的操作处理的不同阶段的日志操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="48a86-121">使用操作筛选器</span><span class="sxs-lookup"><span data-stu-id="48a86-121">Using an Action Filter</span></span>

<span data-ttu-id="48a86-122">操作筛选器是一个属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-122">An action filter is an attribute.</span></span> <span data-ttu-id="48a86-123">可以将大多数操作筛选器应用到一个单独的控制器操作或整个控制器。</span><span class="sxs-lookup"><span data-stu-id="48a86-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="48a86-124">例如，在列表 1 中的数据控制器将公开名为操作`Index()`返回当前时间。</span><span class="sxs-lookup"><span data-stu-id="48a86-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="48a86-125">此操作用修饰`OutputCache`操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="48a86-126">此筛选器会导致要缓存的 10 秒的操作返回的值。</span><span class="sxs-lookup"><span data-stu-id="48a86-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="48a86-127">**代码清单 1 – `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="48a86-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="48a86-128">如果重复调用`Index()`操作通过你的浏览器的地址栏中输入 URL/数据/索引并点击刷新按钮多次，则会出现在同一时间为 10 秒。</span><span class="sxs-lookup"><span data-stu-id="48a86-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="48a86-129">输出`Index()`操作缓存 （见图 1） 的 10 秒。</span><span class="sxs-lookup"><span data-stu-id="48a86-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="48a86-130">[![缓存的时间](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="48a86-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="48a86-131">**图 01**： 缓存时间 ([单击以查看实际尺寸的图像](understanding-action-filters-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="48a86-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>


<span data-ttu-id="48a86-132">在列表 1 中，单个操作筛选器 –`OutputCache`操作筛选器 – 应用于`Index()`方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="48a86-133">如果需要可以将多个操作筛选器应用到相同的操作。</span><span class="sxs-lookup"><span data-stu-id="48a86-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="48a86-134">例如，你可能想要应用同时`OutputCache`和`HandleError`对同一操作的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="48a86-135">在列表 1 中，`OutputCache`操作筛选器应用于`Index()`操作。</span><span class="sxs-lookup"><span data-stu-id="48a86-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="48a86-136">您还可以应用到此特性`DataController`类本身。</span><span class="sxs-lookup"><span data-stu-id="48a86-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="48a86-137">在这种情况下，在控制器公开的任何操作返回的结果会缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="48a86-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="48a86-138">不同类型的筛选器</span><span class="sxs-lookup"><span data-stu-id="48a86-138">The Different Types of Filters</span></span>

<span data-ttu-id="48a86-139">ASP.NET MVC 框架支持四种不同类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="48a86-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="48a86-140">授权筛选器 – 实现`IAuthorizationFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="48a86-141">操作筛选器 – 实现`IActionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="48a86-142">结果筛选器 – 实现`IResultFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="48a86-143">异常筛选器 – 实现`IExceptionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="48a86-144">上面列出的顺序执行筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="48a86-145">例如，授权筛选器始终执行的操作筛选器之前和之后每种其他类型的筛选器始终执行异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="48a86-146">授权筛选器用于实现身份验证和授权控制器操作。</span><span class="sxs-lookup"><span data-stu-id="48a86-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="48a86-147">例如，授权筛选器是授权筛选器的示例。</span><span class="sxs-lookup"><span data-stu-id="48a86-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="48a86-148">操作筛选器包含之前和之后，将执行控制器操作执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="48a86-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="48a86-149">可用于操作筛选器，例如，修改控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="48a86-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="48a86-150">结果筛选器包含之前和之后执行视图结果执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="48a86-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="48a86-151">例如，你可能想要修改的视图结果之前呈现到浏览器视图。</span><span class="sxs-lookup"><span data-stu-id="48a86-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="48a86-152">异常筛选器是筛选器可运行的最后一个类型。</span><span class="sxs-lookup"><span data-stu-id="48a86-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="48a86-153">异常筛选器可用于处理由您的控制器操作或控制器操作结果引发的错误。</span><span class="sxs-lookup"><span data-stu-id="48a86-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="48a86-154">此外可以使用异常筛选器来记录错误。</span><span class="sxs-lookup"><span data-stu-id="48a86-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="48a86-155">按特定顺序执行每种不同类型的筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="48a86-156">如果你想要控制相同类型的筛选器的执行顺序则可以设置筛选器的顺序属性。</span><span class="sxs-lookup"><span data-stu-id="48a86-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="48a86-157">所有操作筛选器的基类是`System.Web.Mvc.FilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="48a86-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="48a86-158">如果您想要实现特定类型的筛选器，则您需要创建一个类继承自基本的筛选器类并实现一个或多个`IAuthorizationFilter`， `IActionFilter`， `IResultFilter`，或`IExceptionFilter`接口。</span><span class="sxs-lookup"><span data-stu-id="48a86-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="48a86-159">基本的 ActionFilterAttribute 类</span><span class="sxs-lookup"><span data-stu-id="48a86-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="48a86-160">为了使你更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包括基`ActionFilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="48a86-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="48a86-161">此类同时实现`IActionFilter`并`IResultFilter`接口，并继承`Filter`类。</span><span class="sxs-lookup"><span data-stu-id="48a86-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="48a86-162">本文中的术语不完全一致。</span><span class="sxs-lookup"><span data-stu-id="48a86-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="48a86-163">从技术上讲，从 ActionFilterAttribute 类继承的类是操作筛选器和结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="48a86-164">但是，松散的意义上，在 word 操作筛选器用于对任何类型的 ASP.NET MVC framework 中的筛选器，请参阅。</span><span class="sxs-lookup"><span data-stu-id="48a86-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="48a86-165">基`ActionFilterAttribute`类具有可重写以下方法：</span><span class="sxs-lookup"><span data-stu-id="48a86-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="48a86-166">OnActionExecuting – 在执行控制器操作之前，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="48a86-167">OnActionExecuted – 在执行控制器操作后，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="48a86-168">OnResultExecuting – 调用此方法在执行控制器操作结果之前。</span><span class="sxs-lookup"><span data-stu-id="48a86-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="48a86-169">OnResultExecuted – 调用此方法后在执行控制器操作结果。</span><span class="sxs-lookup"><span data-stu-id="48a86-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="48a86-170">在下一步部分中，我们将了解如何实现每种不同方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="48a86-171">创建日志操作筛选器</span><span class="sxs-lookup"><span data-stu-id="48a86-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="48a86-172">为了说明如何构建自定义操作筛选器，我们将创建自定义操作筛选器，以记录处理到 Visual Studio 输出窗口的控制器操作的阶段。</span><span class="sxs-lookup"><span data-stu-id="48a86-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="48a86-173">我们`LogActionFilter`代码清单 2 中包含。</span><span class="sxs-lookup"><span data-stu-id="48a86-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="48a86-174">**代码清单 2 – `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="48a86-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="48a86-175">列表 2 中`OnActionExecuting()`， `OnActionExecuted()`， `OnResultExecuting()`，和`OnResultExecuted()`方法都调用`Log()`方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="48a86-176">方法和当前的路由数据的名称传递给`Log()`方法。</span><span class="sxs-lookup"><span data-stu-id="48a86-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="48a86-177">`Log()`方法将一条消息写入到 Visual Studio 输出窗口 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="48a86-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="48a86-178">[![写入到 Visual Studio 输出窗口](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="48a86-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="48a86-179">**图 02**： 写入 Visual Studio 输出窗口 ([单击以查看实际尺寸的图像](understanding-action-filters-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="48a86-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>


<span data-ttu-id="48a86-180">主控制器中清单 3 说明了如何将日志操作筛选器应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="48a86-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="48a86-181">只要任何 Home 控制器公开的操作调用 – 要么`Index()`方法或`About()`方法 – 处理操作记录到 Visual Studio 输出窗口的阶段。</span><span class="sxs-lookup"><span data-stu-id="48a86-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="48a86-182">**代码清单 3 – `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="48a86-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="48a86-183">总结</span><span class="sxs-lookup"><span data-stu-id="48a86-183">Summary</span></span>

<span data-ttu-id="48a86-184">在本教程中，已向您介绍 ASP.NET MVC 操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="48a86-185">介绍了四个不同类型的筛选器： 授权筛选器、 操作筛选器、 结果筛选器和异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="48a86-186">你还了解了有关基本`ActionFilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="48a86-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="48a86-187">最后，您学习了如何实现简单的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="48a86-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="48a86-188">我们创建了日志的操作筛选器，在日志中记录的处理到 Visual Studio 输出窗口的控制器操作的阶段。</span><span class="sxs-lookup"><span data-stu-id="48a86-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="48a86-189">[上一页](asp-net-mvc-routing-overview-cs.md)
> [下一页](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="48a86-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
