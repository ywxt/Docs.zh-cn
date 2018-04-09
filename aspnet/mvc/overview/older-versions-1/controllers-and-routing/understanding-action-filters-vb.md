---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 了解操作筛选器 (VB) |Microsoft 文档
author: microsoft
description: 本教程旨在说明操作筛选器。 操作筛选器是可以应用到的控制器操作-或整个控制器的属性...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 2796b67cba6a2ddaee7a006a170dfb7e5ff89888
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="understanding-action-filters-vb"></a><span data-ttu-id="ceeec-104">了解操作筛选器 (VB)</span><span class="sxs-lookup"><span data-stu-id="ceeec-104">Understanding Action Filters (VB)</span></span>
====================
<span data-ttu-id="ceeec-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ceeec-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ceeec-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="ceeec-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="ceeec-107">本教程旨在说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="ceeec-108">操作筛选器是可以应用到的控制器操作-或整个 controller--修改将执行操作的方式的属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="ceeec-109">了解操作筛选器</span><span class="sxs-lookup"><span data-stu-id="ceeec-109">Understanding Action Filters</span></span>

<span data-ttu-id="ceeec-110">本教程旨在说明操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="ceeec-111">操作筛选器是可以应用到的控制器操作-或整个 controller--修改将执行操作的方式的属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="ceeec-112">ASP.NET MVC framework 包括多个操作筛选器：</span><span class="sxs-lookup"><span data-stu-id="ceeec-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="ceeec-113">OutputCache – 此操作筛选器缓存指定的时间量的控制器操作的输出。</span><span class="sxs-lookup"><span data-stu-id="ceeec-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="ceeec-114">HandleError – 此操作筛选器处理的控制器操作执行时引发的错误。</span><span class="sxs-lookup"><span data-stu-id="ceeec-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="ceeec-115">授权 – 此操作筛选器使您可以限制对特定用户或角色的访问。</span><span class="sxs-lookup"><span data-stu-id="ceeec-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="ceeec-116">您还可以创建你自己的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="ceeec-117">例如，你可能想要创建自定义操作筛选器以便实现一个自定义身份验证系统。</span><span class="sxs-lookup"><span data-stu-id="ceeec-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="ceeec-118">或者，你可能想要创建操作筛选器修改的控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="ceeec-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="ceeec-119">在本教程中，你将了解如何生成操作筛选器从零开始。</span><span class="sxs-lookup"><span data-stu-id="ceeec-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="ceeec-120">我们创建的日志操作筛选器将在处理操作的不同阶段记录到 Visual Studio 输出窗口。</span><span class="sxs-lookup"><span data-stu-id="ceeec-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="ceeec-121">使用操作筛选器</span><span class="sxs-lookup"><span data-stu-id="ceeec-121">Using an Action Filter</span></span>

<span data-ttu-id="ceeec-122">操作筛选器是一个特性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-122">An action filter is an attribute.</span></span> <span data-ttu-id="ceeec-123">可以对单个控制器操作或整个控制器来应用大多数操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="ceeec-124">例如，列表 1 中的数据控制器公开名为操作`Index()`返回当前时间。</span><span class="sxs-lookup"><span data-stu-id="ceeec-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="ceeec-125">此操作用修饰`OutputCache`操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="ceeec-126">此筛选器会导致要为 10 秒缓存的操作返回的值。</span><span class="sxs-lookup"><span data-stu-id="ceeec-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="ceeec-127">**列表 1 – `Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="ceeec-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="ceeec-128">如果反复调用`Index()`操作通过在你的浏览器的地址栏中输入 URL/数据/索引并按刷新按钮多次，则会出现在同一时间为 10 秒。</span><span class="sxs-lookup"><span data-stu-id="ceeec-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="ceeec-129">输出`Index()`操作缓存 （请参见图 1） 的 10 秒钟。</span><span class="sxs-lookup"><span data-stu-id="ceeec-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="ceeec-130">[![缓存的时间](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ceeec-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="ceeec-131">**图 01**： 缓存时间 ([单击以查看实际尺寸的图像](understanding-action-filters-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ceeec-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>


<span data-ttu-id="ceeec-132">在列出 1 中，单个操作筛选器 –`OutputCache`操作筛选器 – 应用到`Index()`方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="ceeec-133">如果需要可以将多个操作筛选器应用到同样的操作。</span><span class="sxs-lookup"><span data-stu-id="ceeec-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="ceeec-134">例如，你可能想要将同时应用`OutputCache`和`HandleError`到相同的操作的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="ceeec-135">列表 1 中`OutputCache`操作筛选器应用于`Index()`操作。</span><span class="sxs-lookup"><span data-stu-id="ceeec-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="ceeec-136">你还可以应用此属性与`DataController`类本身。</span><span class="sxs-lookup"><span data-stu-id="ceeec-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="ceeec-137">在这种情况下，将为 10 秒缓存在控制器公开任何操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="ceeec-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="ceeec-138">不同类型的筛选器</span><span class="sxs-lookup"><span data-stu-id="ceeec-138">The Different Types of Filters</span></span>

<span data-ttu-id="ceeec-139">ASP.NET MVC framework 支持四种不同类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="ceeec-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="ceeec-140">授权筛选器 – 实现`IAuthorizationFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="ceeec-141">操作筛选器 – 实现`IActionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="ceeec-142">导致筛选器 – 实现`IResultFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="ceeec-143">异常筛选器 – 实现`IExceptionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="ceeec-144">筛选器执行上面列出的顺序。</span><span class="sxs-lookup"><span data-stu-id="ceeec-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="ceeec-145">例如，授权筛选器始终执行的操作筛选器之前和之后每种其他类型的筛选器始终执行异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="ceeec-146">授权筛选器用于实现身份验证和授权的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ceeec-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="ceeec-147">例如，Authorize 筛选器是一种授权筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="ceeec-148">操作筛选器包含之前和之后执行控制器操作执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="ceeec-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="ceeec-149">可用于操作筛选器，例如，修改的控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="ceeec-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="ceeec-150">结果筛选器包含之前和之后执行视图结果执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="ceeec-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="ceeec-151">例如，你可能想要修改视图结果右键之前视图呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="ceeec-152">异常筛选器是筛选器以运行的最后一个类型。</span><span class="sxs-lookup"><span data-stu-id="ceeec-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="ceeec-153">异常筛选器可用于处理由你的控制器操作或控制器操作结果引发的错误。</span><span class="sxs-lookup"><span data-stu-id="ceeec-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="ceeec-154">此外可以使用异常筛选器以记录错误。</span><span class="sxs-lookup"><span data-stu-id="ceeec-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="ceeec-155">按特定顺序执行每种不同类型的筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="ceeec-156">如果你想要控制在其中执行的相同类型的筛选器的顺序，则可以设置筛选器的顺序属性。</span><span class="sxs-lookup"><span data-stu-id="ceeec-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="ceeec-157">所有操作筛选器的基类是`System.Web.Mvc.FilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="ceeec-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="ceeec-158">如果你想要实现特定类型的筛选器，则需要创建一个类，从筛选器的基类继承并实现一个或多个 IAuthorizationFilter、 IActionFilter、 IResultFilter，或 ExceptionFilter 接口。</span><span class="sxs-lookup"><span data-stu-id="ceeec-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="ceeec-159">ActionFilterAttribute 基类</span><span class="sxs-lookup"><span data-stu-id="ceeec-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="ceeec-160">ASP.NET MVC framework 以使其更轻松地实现自定义操作筛选器，包括基本`ActionFilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="ceeec-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="ceeec-161">此类同时实现`IActionFilter`和`IResultFilter`接口并继承自`Filter`类。</span><span class="sxs-lookup"><span data-stu-id="ceeec-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="ceeec-162">此处的术语不完全一致。</span><span class="sxs-lookup"><span data-stu-id="ceeec-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="ceeec-163">从技术上讲，从 ActionFilterAttribute 类继承的类是一个操作筛选器和结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="ceeec-164">但是，在松散的意义上，word 操作筛选器用于引用任何类型的 ASP.NET MVC framework 中的筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="ceeec-165">ActionFilterAttribute 基类具有您可以重写以下方法：</span><span class="sxs-lookup"><span data-stu-id="ceeec-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="ceeec-166">OnActionExecuting – 控制器操作执行之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="ceeec-167">OnActionExecuted – 控制器操作执行后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="ceeec-168">OnResultExecuting – 执行控制器操作结果之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="ceeec-169">OnResultExecuted – 控制器操作结果执行后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="ceeec-170">在下一步的部分中，我们将了解如何实现上述每种不同方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="ceeec-171">创建日志操作筛选器</span><span class="sxs-lookup"><span data-stu-id="ceeec-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="ceeec-172">为了说明如何生成自定义操作筛选器，我们将创建自定义操作筛选器来记录处理到 Visual Studio 输出窗口的控制器操作的阶段。</span><span class="sxs-lookup"><span data-stu-id="ceeec-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="ceeec-173">我们`LogActionFilter`中列出 2 包含。</span><span class="sxs-lookup"><span data-stu-id="ceeec-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="ceeec-174">**列出 2 – `ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="ceeec-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="ceeec-175">在列出 2 中， `OnActionExecuting()`， `OnActionExecuted()`， `OnResultExecuting()`，和`OnResultExecuted()`所有方法都调用`Log()`方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="ceeec-176">方法和当前的路由数据的名称传递给`Log()`方法。</span><span class="sxs-lookup"><span data-stu-id="ceeec-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="ceeec-177">`Log()`方法将消息写入 Visual Studio 输出窗口 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="ceeec-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="ceeec-178">[![写入 Visual Studio 输出窗口](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ceeec-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="ceeec-179">**图 02**： 写入 Visual Studio 输出窗口 ([单击以查看实际尺寸的图像](understanding-action-filters-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ceeec-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>


<span data-ttu-id="ceeec-180">列出 3 中的主页控制器演示了如何将日志操作筛选器应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="ceeec-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="ceeec-181">每当在主页控制器公开的任何的操作调用 – 或者`Index()`方法或`About()`方法 – 处理操作会记录到 Visual Studio 输出窗口的阶段。</span><span class="sxs-lookup"><span data-stu-id="ceeec-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="ceeec-182">**列出 3 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="ceeec-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="ceeec-183">总结</span><span class="sxs-lookup"><span data-stu-id="ceeec-183">Summary</span></span>

<span data-ttu-id="ceeec-184">在本教程中，已向您介绍 ASP.NET MVC 操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="ceeec-185">了解有关筛选器的四个不同类型： 授权筛选器、 操作筛选器、 结果筛选器和异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="ceeec-186">你还了解了有关基`ActionFilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="ceeec-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="ceeec-187">最后，您学习了如何实现简单的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="ceeec-188">我们创建了日志处理到 Visual Studio 输出窗口的控制器操作的阶段的日志操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ceeec-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ceeec-189">[上一页](asp-net-mvc-routing-overview-vb.md)
> [下一页](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ceeec-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>
