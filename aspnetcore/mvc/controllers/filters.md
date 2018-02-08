---
title: "筛选器"
author: ardalis
description: "了解*筛选器*的工作原理以及如何在 ASP.NET Core MVC 中使用它们。"
manager: wpickett
ms.author: tdykstra
ms.date: 12/12/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/controllers/filters
ms.openlocfilehash: 2ba3c226cc57f8a3fb26b4119ae9e575eff522f9
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="filters"></a><span data-ttu-id="5fd5b-103">筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-103">Filters</span></span>

<span data-ttu-id="5fd5b-104">作者：[Tom Dykstra](https://github.com/tdykstra/) 和 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="5fd5b-104">By [Tom Dykstra](https://github.com/tdykstra/) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5fd5b-105">ASP.NET Core MVC 中的*筛选器*允许在请求处理管道中的特定阶段之前或之后运行代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-105">*Filters* in ASP.NET Core MVC allow you to run code before or after certain stages in the request processing pipeline.</span></span>

 <span data-ttu-id="5fd5b-106">内置筛选器可处理以下任务：授权（阻止访问未向用户授权的资源），确保所有请求都使用 HTTPS，以及响应缓存（使请求管道短路以返回缓存的响应）等等。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-106">Built-in filters handle tasks such as authorization (preventing access to resources a user isn't authorized for), ensuring that all requests use HTTPS, and response caching (short-circuiting the request pipeline to return a cached response).</span></span> 

<span data-ttu-id="5fd5b-107">可以创建自定义筛选器来处理应用程序的各种跨领域问题。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-107">You can create custom filters to handle cross-cutting concerns for your application.</span></span> <span data-ttu-id="5fd5b-108">每当用户想要避免在所有操作中重复执行代码时，都可以使用筛选器作为解决方案。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-108">Anytime you want to avoid duplicating code across actions, filters are the solution.</span></span> <span data-ttu-id="5fd5b-109">例如，可以在异常筛选器中合并错误处理代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-109">For example, you can consolidate error handling code in a exception filter.</span></span>

<span data-ttu-id="5fd5b-110">[查看或下载 GitHub 中的示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample)。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-110">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample).</span></span>

## <a name="how-do-filters-work"></a><span data-ttu-id="5fd5b-111">筛选器的工作原理</span><span class="sxs-lookup"><span data-stu-id="5fd5b-111">How do filters work?</span></span>

<span data-ttu-id="5fd5b-112">筛选器在 *MVC 操作调用管道*（有时称为*筛选器管道*）内运行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-112">Filters run within the *MVC action invocation pipeline*, sometimes referred to as the *filter pipeline*.</span></span>  <span data-ttu-id="5fd5b-113">筛选器管道在 MVC 选择要执行的操作之后运行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-113">The filter pipeline runs after MVC selects the action to execute.</span></span>

![请求通过其他中间件、路由中间件、操作选择和 MVC 操作调用管道进行处理。](filters/_static/filter-pipeline-1.png)

### <a name="filter-types"></a><span data-ttu-id="5fd5b-116">筛选器类型</span><span class="sxs-lookup"><span data-stu-id="5fd5b-116">Filter types</span></span>

<span data-ttu-id="5fd5b-117">每种筛选器类型都在筛选器管道中的不同阶段执行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-117">Each filter type is executed at a different stage in the filter pipeline.</span></span>

* <span data-ttu-id="5fd5b-118">[授权筛选器](#authorization-filters)最先运行，用于确定是否已针对当前请求为当前用户授权。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-118">[Authorization filters](#authorization-filters) run first and are used to determine whether the current user is authorized for the current request.</span></span> <span data-ttu-id="5fd5b-119">如果请求未获授权，它们可以让管道短路。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-119">They can short-circuit the pipeline if a request is unauthorized.</span></span> 

* <span data-ttu-id="5fd5b-120">[资源筛选器](#resource-filters)是授权后最先处理请求的筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-120">[Resource filters](#resource-filters) are the first to handle a request after authorization.</span></span>  <span data-ttu-id="5fd5b-121">它们可以在筛选器管道的其余阶段运行之前以及管道的其余阶段完成之后运行代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-121">They can run code before the rest of the filter pipeline, and after the rest of the pipeline has completed.</span></span> <span data-ttu-id="5fd5b-122">出于性能方面的考虑，可以使用它们来实现缓存或以其他方式让筛选器管道短路。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-122">They're useful to implement caching or otherwise short-circuit the filter pipeline for performance reasons.</span></span> <span data-ttu-id="5fd5b-123">由于它们在模型绑定之前运行，因此可用于任何需要影响模型绑定的操作。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-123">Since they run before model binding, they're useful for anything that needs to influence model binding.</span></span>

* <span data-ttu-id="5fd5b-124">[操作筛选器](#action-filters)可以在调用单个操作方法之前和之后立即运行代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-124">[Action filters](#action-filters) can run code immediately before and after an individual action method is called.</span></span> <span data-ttu-id="5fd5b-125">它们可用于处理传入某个操作的参数以及从该操作返回的结果。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-125">They can be used to manipulate the arguments passed into an action and the result returned from the action.</span></span>

* <span data-ttu-id="5fd5b-126">[异常筛选器](#exception-filters)用于在向响应正文写入任何内容之前，对未经处理的异常应用全局策略。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-126">[Exception filters](#exception-filters) are used to apply global policies to unhandled exceptions that occur before anything has been written to the response body.</span></span>

* <span data-ttu-id="5fd5b-127">[结果筛选器](#result-filters)可以在执行单个操作结果之前和之后立即运行代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-127">[Result filters](#result-filters) can run code immediately before and after the execution of individual action results.</span></span> <span data-ttu-id="5fd5b-128">它们仅在操作方法成功执行后运行，并且可用于必须涵盖视图或格式化程序执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-128">They run only when the action method has executed successfully and are useful for logic that must surround view or formatter execution.</span></span>

<span data-ttu-id="5fd5b-129">下图展示了这些筛选器类型在筛选器管道中的交互方式。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-129">The following diagram shows how these filter types interact in the filter pipeline.</span></span>

![请求通过授权筛选器、资源筛选器、模型绑定、操作筛选器、操作执行和操作结果转换、异常筛选器、结果筛选器和结果执行进行处理。](filters/_static/filter-pipeline-2.png)

## <a name="implementation"></a><span data-ttu-id="5fd5b-132">实现</span><span class="sxs-lookup"><span data-stu-id="5fd5b-132">Implementation</span></span>

<span data-ttu-id="5fd5b-133">筛选器通过不同的接口定义支持同步和异步实现。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-133">Filters support both synchronous and asynchronous implementations through different interface definitions.</span></span> <span data-ttu-id="5fd5b-134">选择同步变体还是异步变体取决于所需执行的任务类型。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-134">Choose either the sync or async variant depending on the kind of task you need to perform.</span></span> 

<span data-ttu-id="5fd5b-135">可在其管道阶段之前和之后运行代码的同步筛选器定义 On*Stage*Executing 方法和 On*Stage*Executed 方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-135">Synchronous filters that can run code both before and after their pipeline stage define On*Stage*Executing and On*Stage*Executed methods.</span></span> <span data-ttu-id="5fd5b-136">例如，在调用操作方法之前调用 `OnActionExecuting`，在操作方法返回之后调用 `OnActionExecuted`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-136">For example, `OnActionExecuting` is called before the action method is called, and `OnActionExecuted` is called after the action method returns.</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/SampleActionFilter.cs?highlight=6,8,13)]

<span data-ttu-id="5fd5b-137">异步筛选器定义单一的 On*Stage*ExecutionAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-137">Asynchronous filters define a single On*Stage*ExecutionAsync method.</span></span> <span data-ttu-id="5fd5b-138">此方法采用 *FilterType*ExecutionDelegate 委托来执行筛选器的管道阶段。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-138">This method takes a *FilterType*ExecutionDelegate delegate which executes the filter's pipeline stage.</span></span> <span data-ttu-id="5fd5b-139">例如，`ActionExecutionDelegate` 调用该操作方法，用户可以在调用它之前和之后执行代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-139">For example, `ActionExecutionDelegate` calls the action method, and you can execute code before and after you call it.</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/SampleAsyncActionFilter.cs?highlight=6,8-10,13)]

<span data-ttu-id="5fd5b-140">可以在单个类中为多个筛选器阶段实现接口。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-140">You can implement interfaces for multiple filter stages in a single class.</span></span> <span data-ttu-id="5fd5b-141">例如，[ActionFilterAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute) 抽象类可实现 `IActionFilter` 和 `IResultFilter`，以及它们的异步等效接口。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-141">For example, the [ActionFilterAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute) abstract class implements both `IActionFilter` and `IResultFilter`, as well as their async equivalents.</span></span>

> [!NOTE]
> <span data-ttu-id="5fd5b-142">筛选器接口的同步和异步版本**任意**实现一个，而不是同时实现。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-142">Implement **either** the synchronous or the async version of a filter interface, not both.</span></span> <span data-ttu-id="5fd5b-143">该框架会先查看筛选器是否实现了异步接口，如果是，则调用该接口。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-143">The framework checks first to see if the filter implements the async interface, and if so, it calls that.</span></span> <span data-ttu-id="5fd5b-144">如果不是，则调用同步接口的方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-144">If not, it calls the synchronous interface's method(s).</span></span> <span data-ttu-id="5fd5b-145">如果在一个类中同时实现了这两种接口，则仅调用异步方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-145">If you were to implement both interfaces on one class, only the async method would be called.</span></span> <span data-ttu-id="5fd5b-146">使用抽象类时，比如 [ActionFilterAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute)，将为每种筛选器类型仅重写同步方法或仅重写异步方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-146">When using abstract classes like [ActionFilterAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionfilterattribute) you would override only the synchronous methods or the async method for each filter type.</span></span>

### <a name="ifilterfactory"></a><span data-ttu-id="5fd5b-147">IFilterFactory</span><span class="sxs-lookup"><span data-stu-id="5fd5b-147">IFilterFactory</span></span>

<span data-ttu-id="5fd5b-148">`IFilterFactory` 可实现 `IFilter`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-148">`IFilterFactory` implements `IFilter`.</span></span> <span data-ttu-id="5fd5b-149">因此，`IFilterFactory` 实例可在筛选器管道中的任意位置用作 `IFilter` 实例。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-149">Therefore, an `IFilterFactory` instance can be used as an `IFilter` instance anywhere in the filter pipeline.</span></span> <span data-ttu-id="5fd5b-150">当该框架准备调用筛选器时，它会尝试将其转换为 `IFilterFactory`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-150">When the framework prepares to invoke the filter, it attempts to cast it to an `IFilterFactory`.</span></span> <span data-ttu-id="5fd5b-151">如果转换成功，则调用 `CreateInstance` 方法来创建将调用的 `IFilter` 实例。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-151">If that cast succeeds, the `CreateInstance` method is called to create the `IFilter` instance that will be invoked.</span></span> <span data-ttu-id="5fd5b-152">这种设计非常灵活，因为无需在应用程序启动时显式设置精确的筛选器管道。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-152">This provides a very flexible design, since the precise filter pipeline doesn't need to be set explicitly when the application starts.</span></span>

<span data-ttu-id="5fd5b-153">用户可以在自己的属性实现上实现 `IFilterFactory` 作为另一种创建筛选器的方法：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-153">You can implement `IFilterFactory` on your own attribute implementations as another approach to creating filters:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/AddHeaderWithFactoryAttribute.cs?name=snippet_IFilterFactory&highlight=1,4,5,6,7)]

### <a name="built-in-filter-attributes"></a><span data-ttu-id="5fd5b-154">内置筛选器属性</span><span class="sxs-lookup"><span data-stu-id="5fd5b-154">Built-in filter attributes</span></span>

<span data-ttu-id="5fd5b-155">该框架包含许多可子类化和自定义的基于属性的内置筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-155">The framework includes built-in attribute-based filters that you can subclass and customize.</span></span> <span data-ttu-id="5fd5b-156">例如，以下结果筛选器会向响应添加标头。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-156">For example, the following Result filter adds a header to the response.</span></span>

<a name="add-header-attribute"></a>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/AddHeaderAttribute.cs?highlight=5,16)]

<span data-ttu-id="5fd5b-157">属性允许筛选器采用参数，如上面的示例所示。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-157">Attributes allow filters to accept arguments, as shown in the example above.</span></span> <span data-ttu-id="5fd5b-158">可将此属性添加到控制器或操作方法，并指定 HTTP 标头的名称和值：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-158">You would add this attribute to a controller or action method and specify the name and value of the HTTP header:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Controllers/SampleController.cs?name=snippet_AddHeader&highlight=1)]

<span data-ttu-id="5fd5b-159">`Index` 操作的结果如下所示：响应标头显示在右下角。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-159">The result of the `Index` action is shown below - the response headers are displayed on the bottom right.</span></span>

![显示响应标头（包括 Author Steve Smith @ardalis）的 Microsoft Edge 开发人员工具](filters/_static/add-header.png)

<span data-ttu-id="5fd5b-161">多种筛选器接口具有相应属性，这些属性可用作自定义实现的基类。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-161">Several of the filter interfaces have corresponding attributes that can be used as base classes for custom implementations.</span></span>

<span data-ttu-id="5fd5b-162">筛选器属性：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-162">Filter attributes:</span></span>

* `ActionFilterAttribute`
* `ExceptionFilterAttribute`
* `ResultFilterAttribute`
* `FormatFilterAttribute`
* `ServiceFilterAttribute`
* `TypeFilterAttribute`

<span data-ttu-id="5fd5b-163">[本文稍后](#dependency-injection)会对 `TypeFilterAttribute` 和 `ServiceFilterAttribute` 进行介绍。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-163">`TypeFilterAttribute` and `ServiceFilterAttribute` are explained [later in this article](#dependency-injection).</span></span>

## <a name="filter-scopes-and-order-of-execution"></a><span data-ttu-id="5fd5b-164">筛选器作用域和执行顺序</span><span class="sxs-lookup"><span data-stu-id="5fd5b-164">Filter scopes and order of execution</span></span>

<span data-ttu-id="5fd5b-165">可以将筛选器添加到管道中的三个*作用域*之一。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-165">A filter can be added to the pipeline at one of three *scopes*.</span></span> <span data-ttu-id="5fd5b-166">可以使用属性将筛选器添加到特定的操作方法或控制器类。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-166">You can add a filter to a particular action method or to a controller class by using an attribute.</span></span> <span data-ttu-id="5fd5b-167">也可以通过将筛选器添加到 `Startup` 类的 `ConfigureServices` 方法中的 `MvcOptions.Filters` 集合，对其进行全局注册（针对所有控制器和操作）：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-167">Or you can register a filter globally (for all controllers and actions) by adding it to the `MvcOptions.Filters` collection in the `ConfigureServices` method in the `Startup` class:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Startup.cs?name=snippet_ConfigureServices&highlight=5-8)]

### <a name="default-order-of-execution"></a><span data-ttu-id="5fd5b-168">默认执行顺序</span><span class="sxs-lookup"><span data-stu-id="5fd5b-168">Default order of execution</span></span>

<span data-ttu-id="5fd5b-169">当管道的某个特定阶段有多个筛选器时，作用域可确定筛选器执行的默认顺序。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-169">When there are multiple filters for a particular stage of the pipeline, scope determines the default order of filter execution.</span></span>  <span data-ttu-id="5fd5b-170">全局筛选器涵盖类筛选器，类筛选器又涵盖方法筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-170">Global filters surround class filters, which in turn surround method filters.</span></span> <span data-ttu-id="5fd5b-171">这种模式有时称为“俄罗斯套娃”嵌套，因为增加的每个作用域都包装在前一个作用域中，就像[套娃](https://wikipedia.org/wiki/Matryoshka_doll)一样。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-171">This is sometimes referred to as "Russian doll" nesting, as each increase in scope is wrapped around the previous scope, like a [nesting doll](https://wikipedia.org/wiki/Matryoshka_doll).</span></span> <span data-ttu-id="5fd5b-172">通常情况下，无需显式确定排序便可获得所需的重写行为。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-172">You generally get the desired overriding behavior without having to explicitly determine ordering.</span></span>

<span data-ttu-id="5fd5b-173">在这种嵌套模式下，筛选器的 *after* 代码会按照与 *before* 代码相反的顺序运行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-173">As a result of this nesting, the *after* code of filters runs in the reverse order of the *before* code.</span></span> <span data-ttu-id="5fd5b-174">其序列如下所示：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-174">The sequence looks like this:</span></span>

* <span data-ttu-id="5fd5b-175">筛选器的 *before* 代码应用于全局</span><span class="sxs-lookup"><span data-stu-id="5fd5b-175">The *before* code of filters applied globally</span></span>
  * <span data-ttu-id="5fd5b-176">筛选器的 *before* 代码应用于控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-176">The *before* code of filters applied to controllers</span></span>
    * <span data-ttu-id="5fd5b-177">筛选器的 *before* 代码应用于操作方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-177">The *before* code of filters applied to action methods</span></span>
    * <span data-ttu-id="5fd5b-178">筛选器的 *after* 代码应用于操作方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-178">The *after* code of filters applied to action methods</span></span>
  * <span data-ttu-id="5fd5b-179">筛选器的 *after* 代码应用于控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-179">The *after* code of filters applied to controllers</span></span>
* <span data-ttu-id="5fd5b-180">筛选器的 *after* 代码应用于全局</span><span class="sxs-lookup"><span data-stu-id="5fd5b-180">The *after* code of filters applied globally</span></span>
  
<span data-ttu-id="5fd5b-181">下面的示例阐释了为同步操作筛选器调用筛选器方法的顺序。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-181">Here's an example that illustrates the order in which filter methods are called for synchronous Action filters.</span></span>

| <span data-ttu-id="5fd5b-182">序列</span><span class="sxs-lookup"><span data-stu-id="5fd5b-182">Sequence</span></span> | <span data-ttu-id="5fd5b-183">筛选器作用域</span><span class="sxs-lookup"><span data-stu-id="5fd5b-183">Filter scope</span></span> | <span data-ttu-id="5fd5b-184">筛选器方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-184">Filter method</span></span> |
|:--------:|:------------:|:-------------:|
| <span data-ttu-id="5fd5b-185">1</span><span class="sxs-lookup"><span data-stu-id="5fd5b-185">1</span></span> | <span data-ttu-id="5fd5b-186">Global</span><span class="sxs-lookup"><span data-stu-id="5fd5b-186">Global</span></span> | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-187">2</span><span class="sxs-lookup"><span data-stu-id="5fd5b-187">2</span></span> | <span data-ttu-id="5fd5b-188">控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-188">Controller</span></span> | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-189">3</span><span class="sxs-lookup"><span data-stu-id="5fd5b-189">3</span></span> | <span data-ttu-id="5fd5b-190">方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-190">Method</span></span> | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-191">4</span><span class="sxs-lookup"><span data-stu-id="5fd5b-191">4</span></span> | <span data-ttu-id="5fd5b-192">方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-192">Method</span></span> | `OnActionExecuted` |
| <span data-ttu-id="5fd5b-193">5</span><span class="sxs-lookup"><span data-stu-id="5fd5b-193">5</span></span> | <span data-ttu-id="5fd5b-194">控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-194">Controller</span></span> | `OnActionExecuted` |
| <span data-ttu-id="5fd5b-195">6</span><span class="sxs-lookup"><span data-stu-id="5fd5b-195">6</span></span> | <span data-ttu-id="5fd5b-196">Global</span><span class="sxs-lookup"><span data-stu-id="5fd5b-196">Global</span></span> | `OnActionExecuted` |

<span data-ttu-id="5fd5b-197">此序列表明，方法筛选器嵌套在控制器筛选器内，而控制器筛选器嵌套在全局筛选器内。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-197">This sequence shows that the method filter is nested within the controller filter, and the controller filter is nested within the global filter.</span></span> <span data-ttu-id="5fd5b-198">换句话说，如果处于异步筛选器的 On*Stage*ExecutionAsync 方法内，则当代码位于堆栈上时，所有筛选器都在更严格的作用域中运行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-198">To put it another way, if you're inside an async filter's On*Stage*ExecutionAsync method, all of the filters with a tighter scope run while your code is on the stack.</span></span>

> [!NOTE]
> <span data-ttu-id="5fd5b-199">继承自 `Controller` 基类的每个控制器都包括 `OnActionExecuting` 和 `OnActionExecuted` 方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-199">Every controller that inherits from the `Controller` base class includes `OnActionExecuting` and `OnActionExecuted` methods.</span></span> <span data-ttu-id="5fd5b-200">这些方法包装针对某项给定操作运行的筛选器：`OnActionExecuting` 在所有筛选器之前调用，`OnActionExecuted` 在所有筛选器之后调用。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-200">These methods wrap the filters that run for a given action:  `OnActionExecuting` is called before any of the filters, and `OnActionExecuted` is called after all of the filters.</span></span>

### <a name="overriding-the-default-order"></a><span data-ttu-id="5fd5b-201">重写默认顺序</span><span class="sxs-lookup"><span data-stu-id="5fd5b-201">Overriding the default order</span></span>

<span data-ttu-id="5fd5b-202">可以通过实现 `IOrderedFilter` 来重写默认执行序列。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-202">You can override the default sequence of execution by implementing `IOrderedFilter`.</span></span> <span data-ttu-id="5fd5b-203">此接口公开了一个 `Order` 属性来确定执行顺序，该属性优先于作用域。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-203">This interface exposes an `Order` property that takes precedence over scope to determine the order of execution.</span></span> <span data-ttu-id="5fd5b-204">具有较低 `Order` 值的筛选器会在具有较高 `Order` 值的筛选器之前执行其 *before* 代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-204">A filter with a lower `Order` value will have its *before* code executed before that of a filter with a higher value of `Order`.</span></span> <span data-ttu-id="5fd5b-205">具有较低 `Order` 值的筛选器会在具有较高 `Order` 值的筛选器之后执行其 *after* 代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-205">A filter with a lower `Order` value will have its *after* code executed after that of a filter with a higher `Order` value.</span></span> <span data-ttu-id="5fd5b-206">可使用构造函数参数来设置 `Order` 属性：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-206">You can set the `Order` property by using a constructor parameter:</span></span>

```csharp
[MyFilter(Name = "Controller Level Attribute", Order=1)]
```

<span data-ttu-id="5fd5b-207">如果具有上述示例中所示的 3 个相同的操作筛选器，但将控制器和全局筛选器的 `Order` 属性分别设置为 1 和 2，则会反转执行顺序。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-207">If you have the same 3 Action filters shown in the preceding example but set the `Order` property of the controller and global filters to 1 and 2 respectively, the order of execution would be reversed.</span></span>

| <span data-ttu-id="5fd5b-208">序列</span><span class="sxs-lookup"><span data-stu-id="5fd5b-208">Sequence</span></span> | <span data-ttu-id="5fd5b-209">筛选器作用域</span><span class="sxs-lookup"><span data-stu-id="5fd5b-209">Filter scope</span></span> | <span data-ttu-id="5fd5b-210">`Order` 属性</span><span class="sxs-lookup"><span data-stu-id="5fd5b-210">`Order` property</span></span> | <span data-ttu-id="5fd5b-211">筛选器方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-211">Filter method</span></span> |
|:--------:|:------------:|:-----------------:|:-------------:|
| <span data-ttu-id="5fd5b-212">1</span><span class="sxs-lookup"><span data-stu-id="5fd5b-212">1</span></span> | <span data-ttu-id="5fd5b-213">方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-213">Method</span></span> | <span data-ttu-id="5fd5b-214">0</span><span class="sxs-lookup"><span data-stu-id="5fd5b-214">0</span></span> | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-215">2</span><span class="sxs-lookup"><span data-stu-id="5fd5b-215">2</span></span> | <span data-ttu-id="5fd5b-216">控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-216">Controller</span></span> | <span data-ttu-id="5fd5b-217">1</span><span class="sxs-lookup"><span data-stu-id="5fd5b-217">1</span></span>  | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-218">3</span><span class="sxs-lookup"><span data-stu-id="5fd5b-218">3</span></span> | <span data-ttu-id="5fd5b-219">Global</span><span class="sxs-lookup"><span data-stu-id="5fd5b-219">Global</span></span> | <span data-ttu-id="5fd5b-220">2</span><span class="sxs-lookup"><span data-stu-id="5fd5b-220">2</span></span>  | `OnActionExecuting` |
| <span data-ttu-id="5fd5b-221">4</span><span class="sxs-lookup"><span data-stu-id="5fd5b-221">4</span></span> | <span data-ttu-id="5fd5b-222">Global</span><span class="sxs-lookup"><span data-stu-id="5fd5b-222">Global</span></span> | <span data-ttu-id="5fd5b-223">2</span><span class="sxs-lookup"><span data-stu-id="5fd5b-223">2</span></span>  | `OnActionExecuted` |
| <span data-ttu-id="5fd5b-224">5</span><span class="sxs-lookup"><span data-stu-id="5fd5b-224">5</span></span> | <span data-ttu-id="5fd5b-225">控制器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-225">Controller</span></span> | <span data-ttu-id="5fd5b-226">1</span><span class="sxs-lookup"><span data-stu-id="5fd5b-226">1</span></span>  | `OnActionExecuted` |
| <span data-ttu-id="5fd5b-227">6</span><span class="sxs-lookup"><span data-stu-id="5fd5b-227">6</span></span> | <span data-ttu-id="5fd5b-228">方法</span><span class="sxs-lookup"><span data-stu-id="5fd5b-228">Method</span></span> | <span data-ttu-id="5fd5b-229">0</span><span class="sxs-lookup"><span data-stu-id="5fd5b-229">0</span></span>  | `OnActionExecuted` |

<span data-ttu-id="5fd5b-230">在确定筛选器的运行顺序时，`Order` 属性优先于作用域。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-230">The `Order` property trumps scope when determining the order in which filters will run.</span></span> <span data-ttu-id="5fd5b-231">先按顺序对筛选器排序，然后使用作用域消除并列问题。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-231">Filters are sorted first by order, then scope is used to break ties.</span></span> <span data-ttu-id="5fd5b-232">所有内置筛选器都可实现 `IOrderedFilter` 并将默认 `Order` 值设置为 0，因此，除非将 `Order` 设置为非零值，否则将由作用域确定顺序。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-232">All of the built-in filters implement `IOrderedFilter` and set the default `Order` value to 0, so scope determines order unless you set `Order` to a non-zero value.</span></span>

## <a name="cancellation-and-short-circuiting"></a><span data-ttu-id="5fd5b-233">取消和设置短路</span><span class="sxs-lookup"><span data-stu-id="5fd5b-233">Cancellation and short circuiting</span></span>

<span data-ttu-id="5fd5b-234">通过设置提供给筛选器方法的 `context` 参数上的 `Result` 属性，可以在筛选器管道的任意位置设置短路。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-234">You can short-circuit the filter pipeline at any point by setting the `Result` property on the `context` parameter provided to the filter method.</span></span> <span data-ttu-id="5fd5b-235">例如，以下资源筛选器将阻止执行管道的其余阶段。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-235">For instance, the following Resource filter prevents the rest of the pipeline from executing.</span></span>

<a name="short-circuiting-resource-filter"></a>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/ShortCircuitingResourceFilterAttribute.cs?highlight=12,13,14,15)]

<span data-ttu-id="5fd5b-236">在下面的代码中，`ShortCircuitingResourceFilter` 和 `AddHeader` 筛选器都以 `SomeResource` 操作方法为目标。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-236">In the following code, both the `ShortCircuitingResourceFilter` and the `AddHeader` filter target the `SomeResource` action method.</span></span> <span data-ttu-id="5fd5b-237">但是，由于 `ShortCircuitingResourceFilter` 先运行（因为它是资源筛选器，而 `AddHeader` 是操作筛选器）并使管道的其余阶段短路，因此，永远不会为 `SomeResource` 操作运行 `AddHeader` 筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-237">However, because the `ShortCircuitingResourceFilter` runs first (because it's a Resource Filter and `AddHeader` is an Action Filter) and short-circuits the rest of the pipeline, the `AddHeader` filter never runs for the `SomeResource` action.</span></span> <span data-ttu-id="5fd5b-238">如果这两个筛选器都应用于操作方法级别，只要 `ShortCircuitingResourceFilter` 先运行（比如，由于其筛选器类型或显式使用 `Order` 属性），此行为就不会变。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-238">This behavior would be the same if both filters were applied at the action method level, provided the `ShortCircuitingResourceFilter` ran first (because of its filter type, or explicit use of `Order` property, for instance).</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Controllers/SampleController.cs?name=snippet_AddHeader&highlight=1,9)]

## <a name="dependency-injection"></a><span data-ttu-id="5fd5b-239">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="5fd5b-239">Dependency injection</span></span>

<span data-ttu-id="5fd5b-240">可按类型或实例添加筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-240">Filters can be added by type or by instance.</span></span> <span data-ttu-id="5fd5b-241">如果添加实例，该实例将用于每个请求。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-241">If you add an instance, that instance will be used for every request.</span></span> <span data-ttu-id="5fd5b-242">如果添加类型，则将激活该类型，这意味着将为每个请求创建一个实例，并且[依赖关系注入](../../fundamentals/dependency-injection.md) (DI) 将填充所有构造函数依赖项。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-242">If you add a type, it will be type-activated, meaning an instance will be created for each request and any constructor dependencies will be populated by [dependency injection](../../fundamentals/dependency-injection.md) (DI).</span></span> <span data-ttu-id="5fd5b-243">按类型添加筛选器等效于 `filters.Add(new TypeFilterAttribute(typeof(MyFilter)))`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-243">Adding a filter by type is equivalent to `filters.Add(new TypeFilterAttribute(typeof(MyFilter)))`.</span></span>

<span data-ttu-id="5fd5b-244">如果将筛选器作为属性实现并直接添加到控制器类或操作方法中，则该筛选器不能由[依赖关系注入](../../fundamentals/dependency-injection.md) (DI) 提供构造函数依赖项。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-244">Filters that are implemented as attributes and added directly to controller classes or action methods cannot have constructor dependencies provided by [dependency injection](../../fundamentals/dependency-injection.md) (DI).</span></span> <span data-ttu-id="5fd5b-245">这是因为属性在应用时必须提供自己的构造函数参数。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-245">This is because attributes must have their constructor parameters supplied where they're applied.</span></span> <span data-ttu-id="5fd5b-246">这是属性工作原理上的限制。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-246">This is a limitation of how attributes work.</span></span>

<span data-ttu-id="5fd5b-247">如果筛选器具有一些需要从 DI 访问的依赖项，有几种受支持的方法可用。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-247">If your filters have dependencies that you need to access from DI, there are several supported approaches.</span></span> <span data-ttu-id="5fd5b-248">可以使用以下接口之一，将筛选器应用于类或操作方法：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-248">You can apply your filter to a class or action method using one of the following:</span></span>

* `ServiceFilterAttribute`
* `TypeFilterAttribute`
* <span data-ttu-id="5fd5b-249">在属性上实现的 `IFilterFactory`</span><span class="sxs-lookup"><span data-stu-id="5fd5b-249">`IFilterFactory` implemented on your attribute</span></span>

> [!NOTE]
> <span data-ttu-id="5fd5b-250">记录器就是一种可能需要从 DI 获取的依赖项。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-250">One dependency you might want to get from DI is a logger.</span></span> <span data-ttu-id="5fd5b-251">但是，应避免单纯为进行日志记录而创建和使用筛选器，因为[内置的框架日志记录功能](xref:fundamentals/logging/index)可能已经提供用户所需。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-251">However, avoid creating and using filters purely for logging purposes, since the [built-in framework logging features](xref:fundamentals/logging/index) may already provide what you need.</span></span> <span data-ttu-id="5fd5b-252">如果要将日志记录功能添加到筛选器，它应重点关注业务领域问题或特定于筛选器的行为，而非 MVC 操作或其他框架事件。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-252">If you're going to add logging to your filters, it should focus on business domain concerns or behavior specific to your filter, rather than MVC actions or other framework events.</span></span>

### <a name="servicefilterattribute"></a><span data-ttu-id="5fd5b-253">ServiceFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="5fd5b-253">ServiceFilterAttribute</span></span>

<span data-ttu-id="5fd5b-254">`ServiceFilter` 可从 DI 检索筛选器实例。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-254">A `ServiceFilter` retrieves an instance of the filter from DI.</span></span> <span data-ttu-id="5fd5b-255">将筛选器添加到该容器的 `ConfigureServices` 中，并在 `ServiceFilter` 属性中引用它</span><span class="sxs-lookup"><span data-stu-id="5fd5b-255">You add the filter to the container in `ConfigureServices`, and reference it in a `ServiceFilter` attribute</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Startup.cs?name=snippet_ConfigureServices&highlight=11)]

[!code-csharp[Main](../../mvc/controllers/filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_ServiceFilter&highlight=1)]

<span data-ttu-id="5fd5b-256">使用 `ServiceFilter` 时不注册筛选器类型会引发异常：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-256">Using `ServiceFilter` without registering the filter type results in an exception:</span></span>

```
System.InvalidOperationException: No service for type
'FiltersSample.Filters.AddHeaderFilterWithDI' has been registered.
```

<span data-ttu-id="5fd5b-257">`ServiceFilterAttribute` 可实现 `IFilterFactory`，后者为创建 `IFilter` 实例公开了一个方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-257">`ServiceFilterAttribute` implements `IFilterFactory`, which exposes a single method for creating an `IFilter` instance.</span></span> <span data-ttu-id="5fd5b-258">使用 `ServiceFilterAttribute` 时，可通过实现 `IFilterFactory` 接口的 `CreateInstance` 方法，从服务容器 (DI) 中加载指定的类型。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-258">In the case of `ServiceFilterAttribute`, the `IFilterFactory` interface's `CreateInstance` method is implemented to load the specified type from the services container (DI).</span></span>

### <a name="typefilterattribute"></a><span data-ttu-id="5fd5b-259">TypeFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="5fd5b-259">TypeFilterAttribute</span></span>

<span data-ttu-id="5fd5b-260">`TypeFilterAttribute` 与 `ServiceFilterAttribute` 非常类似（也能实现 `IFilterFactory`），但不会直接从 DI 容器解析其类型，</span><span class="sxs-lookup"><span data-stu-id="5fd5b-260">`TypeFilterAttribute` is very similar to `ServiceFilterAttribute` (and also implements `IFilterFactory`), but its type isn't resolved directly from the DI container.</span></span> <span data-ttu-id="5fd5b-261">而是使用 `Microsoft.Extensions.DependencyInjection.ObjectFactory` 对类型进行实例化。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-261">Instead, it instantiates the type by using `Microsoft.Extensions.DependencyInjection.ObjectFactory`.</span></span>

<span data-ttu-id="5fd5b-262">由于存在这一差别，使用 `TypeFilterAttribute` 引用的类型无需先向容器注册（但仍由容器提供其依赖项）。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-262">Because of this difference, types that are referenced using the `TypeFilterAttribute` don't need to be registered with the container first (but they will still have their dependencies fulfilled by the container).</span></span> <span data-ttu-id="5fd5b-263">此外，`TypeFilterAttribute` 还可以选择为上述类型采用构造函数参数。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-263">Also, `TypeFilterAttribute` can optionally accept constructor arguments for the type in question.</span></span> <span data-ttu-id="5fd5b-264">下面的示例演示如何使用 `TypeFilterAttribute` 将参数传递到类型：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-264">The following example demonstrates how to pass arguments to a type using `TypeFilterAttribute`:</span></span>

[!code-csharp[Main](../../mvc/controllers/filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_TypeFilter&highlight=1,2)]

<span data-ttu-id="5fd5b-265">如果某个筛选器不需要任何参数，但具有需要由 DI 填充的构造函数依赖项，则可以在类和方法上使用自己的命名属性，而非使用 `[TypeFilter(typeof(FilterType))]`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-265">If you have a filter that doesn't require any arguments, but which has constructor dependencies that need to be filled by DI, you can use your own named attribute on classes and methods instead of `[TypeFilter(typeof(FilterType))]`).</span></span> <span data-ttu-id="5fd5b-266">下面的筛选器展示了如何实现此操作：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-266">The following filter shows how this can be implemented:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/SampleActionFilterAttribute.cs?name=snippet_TypeFilterAttribute&highlight=1,3,7)]

<span data-ttu-id="5fd5b-267">可以使用 `[SampleActionFilter]` 语法将此筛选器应用于类或方法，而不必使用 `[TypeFilter]` 或 `[ServiceFilter]`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-267">This filter can be applied to classes or methods using the `[SampleActionFilter]` syntax, instead of having to use `[TypeFilter]` or `[ServiceFilter]`.</span></span>

## <a name="authorization-filters"></a><span data-ttu-id="5fd5b-268">授权筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-268">Authorization filters</span></span>

<span data-ttu-id="5fd5b-269">*授权筛选器*用于控制对操作方法的访问，是筛选器管道内最先执行的筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-269">*Authorization filters* control access to action methods and are the first filters to be executed within the filter pipeline.</span></span> <span data-ttu-id="5fd5b-270">它们只有 before 方法，而不像大多数筛选器一样既支持 before 方法也支持 after 方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-270">They have only a before method, unlike most filters that support before and after methods.</span></span> <span data-ttu-id="5fd5b-271">用户只有在编写自己的授权框架时，才应编写自定义授权筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-271">You should only write a custom authorization filter if you are writing your own authorization framework.</span></span> <span data-ttu-id="5fd5b-272">建议配置授权策略或编写自定义授权策略，而不是编写自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-272">Prefer configuring your authorization policies or writing a custom authorization policy over writing a custom filter.</span></span> <span data-ttu-id="5fd5b-273">内置筛选器实现只负责调用授权系统。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-273">The built-in filter implementation is just responsible for calling the authorization system.</span></span>

<span data-ttu-id="5fd5b-274">请注意，切勿在授权筛选器内引发异常，因为没有任何能处理该异常的组件（异常筛选器不会进行处理）。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-274">Note that you shouldn't throw exceptions within authorization filters, since nothing will handle the exception (exception filters won't handle them).</span></span> <span data-ttu-id="5fd5b-275">应发出质询或寻找其他方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-275">Instead, issue a challenge or find another way.</span></span>

<span data-ttu-id="5fd5b-276">详细了解[授权](../../security/authorization/index.md)。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-276">Learn more about [Authorization](../../security/authorization/index.md).</span></span>

## <a name="resource-filters"></a><span data-ttu-id="5fd5b-277">资源筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-277">Resource filters</span></span>

<span data-ttu-id="5fd5b-278">*资源筛选器*可实现 `IResourceFilter` 或 `IAsyncResourceFilter` 接口，其执行包装了筛选器管道的大多数阶段。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-278">*Resource filters* implement either the `IResourceFilter` or `IAsyncResourceFilter` interface, and their execution wraps most of the filter pipeline.</span></span> <span data-ttu-id="5fd5b-279">（只有[授权筛选器](#authorization-filters)在它们之前运行。）如果需要使某个请求正在执行的大部分工作短路，资源筛选器特别有用。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-279">(Only [Authorization filters](#authorization-filters) run before them.) Resource filters are especially useful if you need to short-circuit most of the work a request is doing.</span></span> <span data-ttu-id="5fd5b-280">例如，如果响应已在缓存中，则缓存筛选器可以绕开管道的其余阶段。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-280">For example, a caching filter can avoid the rest of the pipeline if the response is already in the cache.</span></span>

<span data-ttu-id="5fd5b-281">前面所示的[短路资源筛选器](#short-circuiting-resource-filter)便是一种资源筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-281">The [short circuiting resource filter](#short-circuiting-resource-filter) shown earlier is one example of a resource filter.</span></span> <span data-ttu-id="5fd5b-282">还有就是 [DisableFormValueModelBindingAttribute](https://github.com/aspnet/Entropy/blob/rel/1.1.1/samples/Mvc.FileUpload/Filters/DisableFormValueModelBindingAttribute.cs)，它可阻止模型绑定访问表单数据。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-282">Another example is [DisableFormValueModelBindingAttribute](https://github.com/aspnet/Entropy/blob/rel/1.1.1/samples/Mvc.FileUpload/Filters/DisableFormValueModelBindingAttribute.cs), which prevents model binding from accessing the form data.</span></span> <span data-ttu-id="5fd5b-283">如果用户知道将要接收大型文件上传，想阻止表单读入内存，则可使用此筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-283">It's useful for cases where you know that you're going to receive large file uploads and want to prevent the form from being read into memory.</span></span>

## <a name="action-filters"></a><span data-ttu-id="5fd5b-284">操作筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-284">Action filters</span></span>

<span data-ttu-id="5fd5b-285">*操作筛选器*可实现 `IActionFilter` 或 `IAsyncActionFilter` 接口，其执行涵盖操作方法的执行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-285">*Action filters* implement either the `IActionFilter` or `IAsyncActionFilter` interface, and their execution surrounds the execution of action methods.</span></span>

<span data-ttu-id="5fd5b-286">下面是一个操作筛选器示例：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-286">Here's a sample action filter:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/SampleActionFilter.cs?name=snippet_ActionFilter)]

<span data-ttu-id="5fd5b-287">[ActionExecutingContext](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionexecutingcontext) 提供以下属性：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-287">The [ActionExecutingContext](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionexecutingcontext) provides the following properties:</span></span>

* <span data-ttu-id="5fd5b-288">`ActionArguments`：用于处理对操作的输入。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-288">`ActionArguments` - lets you manipulate the inputs to the action.</span></span>
* <span data-ttu-id="5fd5b-289">`Controller`：用于处理控制器实例。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-289">`Controller` - lets you manipulate the controller instance.</span></span> 
* <span data-ttu-id="5fd5b-290">`Result`：设置此属性会使操作方法和后续操作筛选器的执行短路。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-290">`Result` - setting this short-circuits execution of the action method and subsequent action filters.</span></span> <span data-ttu-id="5fd5b-291">引发异常也会阻止操作方法和后续筛选器的执行，但会被视为失败，而不是一个成功的结果。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-291">Throwing an exception also prevents execution of the action method and subsequent filters, but is treated as a failure instead of a successful result.</span></span>

<span data-ttu-id="5fd5b-292">[ActionExecutedContext](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionexecutedcontext) 提供 `Controller` 和 `Result` 以及下列属性：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-292">The [ActionExecutedContext](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.filters.actionexecutedcontext) provides `Controller` and `Result` plus the following properties:</span></span>

* <span data-ttu-id="5fd5b-293">`Canceled`：如果操作执行已被另一个筛选器设置短路，则为 true。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-293">`Canceled` - will be true if the action execution was short-circuited by another filter.</span></span>
* <span data-ttu-id="5fd5b-294">`Exception`：如果操作或后续操作筛选器引发了异常，则为非 NULL 值。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-294">`Exception` - will be non-null if the action or a subsequent action filter threw an exception.</span></span> <span data-ttu-id="5fd5b-295">将此属性设置为 NULL 可有效地“处理”异常，并且将执行 `Result`，就像它是从操作方法正常返回的一样。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-295">Setting this property to null effectively 'handles' an exception, and `Result` will be executed as if it were returned from the action method normally.</span></span>

<span data-ttu-id="5fd5b-296">对于 `IAsyncActionFilter`，通过调用 `ActionExecutionDelegate` 可执行所有后续操作筛选器和操作方法，并返回 `ActionExecutedContext`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-296">For an `IAsyncActionFilter`, a call to the `ActionExecutionDelegate` executes any subsequent action filters and the action method, returning an `ActionExecutedContext`.</span></span> <span data-ttu-id="5fd5b-297">若要设置短路，可将 `ActionExecutingContext.Result` 分配到某个结果实例，并且不调用 `ActionExecutionDelegate`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-297">To short-circuit, assign `ActionExecutingContext.Result` to some result instance and don't call the `ActionExecutionDelegate`.</span></span>

<span data-ttu-id="5fd5b-298">该框架提供一个可子类化的抽象 `ActionFilterAttribute`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-298">The framework provides an abstract `ActionFilterAttribute` that you can subclass.</span></span> 

<span data-ttu-id="5fd5b-299">操作筛选器可用于自动验证模型状态，并在状态为无效时返回任何错误：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-299">You can use an action filter to automatically validate model state and return any errors if the state is invalid:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/ValidateModelAttribute.cs)]

<span data-ttu-id="5fd5b-300">`OnActionExecuted` 方法在操作方法之后运行，可通过 `ActionExecutedContext.Result` 属性查看和处理操作结果。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-300">The `OnActionExecuted` method runs after the action method and can see and manipulate the results of the action through the `ActionExecutedContext.Result` property.</span></span> <span data-ttu-id="5fd5b-301">如果操作执行已被另一个筛选器设置短路，则 `ActionExecutedContext.Canceled` 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-301">`ActionExecutedContext.Canceled` will be set to true if the action execution was short-circuited by another filter.</span></span> <span data-ttu-id="5fd5b-302">如果操作或后续操作筛选器引发了异常，则 `ActionExecutedContext.Exception` 设置为非 NULL 值。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-302">`ActionExecutedContext.Exception` will be set to a non-null value if the action or a subsequent action filter threw an exception.</span></span> <span data-ttu-id="5fd5b-303">将 `ActionExecutedContext.Exception` 设置为 NULL 可有效地“处理”异常，然后将执行 `ActionExectedContext.Result`，就像它是从操作方法正常返回的一样。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-303">Setting `ActionExecutedContext.Exception` to null effectively 'handles' an exception, and `ActionExectedContext.Result` will then be executed as if it were returned from the action method normally.</span></span>

## <a name="exception-filters"></a><span data-ttu-id="5fd5b-304">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-304">Exception filters</span></span>

<span data-ttu-id="5fd5b-305">*异常筛选器*可实现 `IExceptionFilter` 或 `IAsyncExceptionFilter` 接口。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-305">*Exception filters* implement either the `IExceptionFilter` or `IAsyncExceptionFilter` interface.</span></span> <span data-ttu-id="5fd5b-306">它们可用于为应用实现常见的错误处理策略。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-306">They can be used to implement common error handling policies for an app.</span></span> 

<span data-ttu-id="5fd5b-307">下面的异常筛选器示例使用自定义开发人员错误视图，显示在开发应用程序时发生的异常的相关详细信息：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-307">The following sample exception filter uses a custom developer error view to display details about exceptions that occur when the application is in development:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/CustomExceptionFilterAttribute.cs?name=snippet_ExceptionFilter&highlight=1,14)]

<span data-ttu-id="5fd5b-308">异常筛选器没有两个事件（对于 before 和 after），它们仅实现 `OnException`（或 `OnExceptionAsync`）。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-308">Exception filters don't have two events (for before and after) - they only implement `OnException` (or `OnExceptionAsync`).</span></span> 

<span data-ttu-id="5fd5b-309">异常筛选器用于处理控制器创建、[模型绑定](../models/model-binding.md)、操作筛选器或操作方法中发生的未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-309">Exception filters handle unhandled exceptions that occur in controller creation, [model binding](../models/model-binding.md), action filters, or action methods.</span></span> <span data-ttu-id="5fd5b-310">它们不会捕获资源筛选器、结果筛选器或 MVC 结果执行中发生的异常。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-310">They won't catch exceptions that occur in Resource filters, Result filters, or MVC Result execution.</span></span>

<span data-ttu-id="5fd5b-311">若要处理异常，请将 `ExceptionContext.ExceptionHandled` 属性设置为 true，或编写响应。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-311">To handle an exception, set the `ExceptionContext.ExceptionHandled` property to true or write a response.</span></span> <span data-ttu-id="5fd5b-312">这将停止传播异常。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-312">This stops propagation of the exception.</span></span> <span data-ttu-id="5fd5b-313">请注意，异常筛选器无法将异常转变为“成功”。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-313">Note that an Exception filter can't turn an exception into a "success".</span></span> <span data-ttu-id="5fd5b-314">只有操作筛选器才能执行该转变。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-314">Only an Action filter can do that.</span></span>

> [!NOTE]
> <span data-ttu-id="5fd5b-315">在 ASP.NET 1.1 中，如果将 `ExceptionHandled` 设置为 true **并**编写响应，则不会发送响应。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-315">In ASP.NET 1.1, the response isn't sent if you set `ExceptionHandled` to true **and** write a response.</span></span> <span data-ttu-id="5fd5b-316">在这种情况下，ASP.NET Core 1.0 不发送响应，ASP.NET Core 1.1.2 则恢复为 1.0 的行为。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-316">In that scenario, ASP.NET Core 1.0 does send the response, and ASP.NET Core 1.1.2 will return to the 1.0 behavior.</span></span> <span data-ttu-id="5fd5b-317">有关详细信息，请参阅 GitHub 存储库中的[问题编号 5594](https://github.com/aspnet/Mvc/issues/5594)。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-317">For more information, see [issue #5594](https://github.com/aspnet/Mvc/issues/5594) in the GitHub repository.</span></span> 

<span data-ttu-id="5fd5b-318">异常筛选器适合捕获 MVC 操作内发生的异常，但它们不如错误处理中间件灵活。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-318">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="5fd5b-319">一般情况下建议使用中间件；仅在需要根据所选 MVC 操作以不同方式执行错误处理时，才使用筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-319">Prefer middleware for the general case, and use filters only where you need to do error handling *differently* based on which MVC action was chosen.</span></span> <span data-ttu-id="5fd5b-320">例如，应用可能具有用于 API 终结点和视图/HTML 的操作方法。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-320">For example, your app might have action methods for both API endpoints and for views/HTML.</span></span> <span data-ttu-id="5fd5b-321">API 终结点可能返回 JSON 形式的错误信息，而基于视图的操作可能返回 HTML 形式的错误页。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-321">The API endpoints could return error information as JSON, while the view-based actions could return an error page as HTML.</span></span>

<span data-ttu-id="5fd5b-322">该框架提供一个可子类化的抽象 `ExceptionFilterAttribute`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-322">The framework provides an abstract `ExceptionFilterAttribute` that you can subclass.</span></span> 

## <a name="result-filters"></a><span data-ttu-id="5fd5b-323">结果筛选器</span><span class="sxs-lookup"><span data-stu-id="5fd5b-323">Result filters</span></span>

<span data-ttu-id="5fd5b-324">*结果筛选器*可实现 `IResultFilter` 或 `IAsyncResultFilter` 接口，其执行涵盖操作结果的执行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-324">*Result filters* implement either the `IResultFilter` or `IAsyncResultFilter` interface, and their execution surrounds the execution of action results.</span></span> 

<span data-ttu-id="5fd5b-325">下面是一个添加 HTTP 标头的结果筛选器示例。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-325">Here's an example of a Result filter that adds an HTTP header.</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/LoggingAddHeaderFilter.cs?name=snippet_ResultFilter)]

<span data-ttu-id="5fd5b-326">要执行的结果类型取决于所执行的操作。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-326">The kind of result being executed depends on the action in question.</span></span> <span data-ttu-id="5fd5b-327">返回视图的 MVC 操作会将所有 Razor 处理作为要执行的 `ViewResult` 的一部分。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-327">An MVC action returning a view would include all razor processing as part of the `ViewResult` being executed.</span></span> <span data-ttu-id="5fd5b-328">API 方法可能会将某些序列化操作作为结果执行的一部分。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-328">An API method might perform some serialization as part of the execution of the result.</span></span> <span data-ttu-id="5fd5b-329">详细了解[操作结果](actions.md)</span><span class="sxs-lookup"><span data-stu-id="5fd5b-329">Learn more about [action results](actions.md)</span></span>

<span data-ttu-id="5fd5b-330">当操作或操作筛选器生成操作结果时，仅针对成功的结果执行结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-330">Result filters are only executed for successful results - when the action or action filters produce an action result.</span></span> <span data-ttu-id="5fd5b-331">当异常筛选器处理异常时，不执行结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-331">Result filters are not executed when exception filters handle an exception.</span></span>

<span data-ttu-id="5fd5b-332">`OnResultExecuting` 方法可以将 `ResultExecutingContext.Cancel` 设置为 true，使操作结果和后续结果筛选器的执行短路。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-332">The `OnResultExecuting` method can short-circuit execution of the action result and subsequent result filters by setting `ResultExecutingContext.Cancel` to true.</span></span> <span data-ttu-id="5fd5b-333">设置短路时，通常应写入响应对象，以免生成空响应。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-333">You should generally write to the response object when short-circuiting to avoid generating an empty response.</span></span> <span data-ttu-id="5fd5b-334">引发异常也将阻止操作结果和后续筛选器的执行，但会被视为失败，而不是一个成功的结果。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-334">Throwing an exception will also prevent execution of the action result and subsequent filters, but will be treated as a failure instead of a successful result.</span></span>

<span data-ttu-id="5fd5b-335">当 `OnResultExecuted` 方法运行时，响应可能已发送到客户端，而且不能再更改（除非引发了异常）。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-335">When the `OnResultExecuted` method runs, the response has likely been sent to the client and cannot be changed further (unless an exception was thrown).</span></span> <span data-ttu-id="5fd5b-336">如果操作结果执行已被另一个筛选器设置短路，则 `ResultExecutedContext.Canceled` 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-336">`ResultExecutedContext.Canceled` will be set to true if the action result execution was short-circuited by another filter.</span></span>

<span data-ttu-id="5fd5b-337">如果操作结果或后续结果筛选器引发了异常，则 `ResultExecutedContext.Exception` 设置为非 NULL 值。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-337">`ResultExecutedContext.Exception` will be set to a non-null value if the action result or a subsequent result filter threw an exception.</span></span> <span data-ttu-id="5fd5b-338">将 `Exception` 设置为 NULL 可有效地“处理”异常，并防止 MVC 在管道的后续阶段重新引发该异常。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-338">Setting `Exception` to null effectively 'handles' an exception and prevents the exception from being rethrown by MVC later in the pipeline.</span></span> <span data-ttu-id="5fd5b-339">在处理结果筛选器中的异常时，可能无法向响应写入任何数据。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-339">When you're handling an exception in a result filter, you might not be able to write any data to the response.</span></span> <span data-ttu-id="5fd5b-340">如果操作结果在其执行过程中引发异常，并且标头已刷新到客户端，则没有任何可靠的机制可用于发送失败代码。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-340">If the action result throws partway through its execution, and the headers have already been flushed to the client, there's no reliable mechanism to send a failure code.</span></span>

<span data-ttu-id="5fd5b-341">对于 `IAsyncResultFilter`，通过调用 `ResultExecutionDelegate` 上的 `await next()` 可执行所有后续结果筛选器和操作结果。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-341">For an `IAsyncResultFilter` a call to `await next()` on the `ResultExecutionDelegate` executes any subsequent result filters and the action result.</span></span> <span data-ttu-id="5fd5b-342">若要设置短路，可将 `ResultExecutingContext.Cancel` 设置为 true，并且不调用 `ResultExectionDelegate`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-342">To short-circuit, set `ResultExecutingContext.Cancel` to true and don't call the `ResultExectionDelegate`.</span></span>

<span data-ttu-id="5fd5b-343">该框架提供一个可子类化的抽象 `ResultFilterAttribute`。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-343">The framework provides an abstract `ResultFilterAttribute` that you can subclass.</span></span> <span data-ttu-id="5fd5b-344">前面所示的 [AddHeaderAttribute](#add-header-attribute) 类是一种结果筛选器属性。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-344">The [AddHeaderAttribute](#add-header-attribute) class shown earlier is an example of a result filter attribute.</span></span>

## <a name="using-middleware-in-the-filter-pipeline"></a><span data-ttu-id="5fd5b-345">在筛选器管道中使用中间件</span><span class="sxs-lookup"><span data-stu-id="5fd5b-345">Using middleware in the filter pipeline</span></span>

<span data-ttu-id="5fd5b-346">资源筛选器的工作方式与[中间件](xref:fundamentals/middleware/index)类似，即涵盖管道中的所有后续执行。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-346">Resource filters work like [middleware](xref:fundamentals/middleware/index) in that they surround the execution of everything that comes later in the pipeline.</span></span> <span data-ttu-id="5fd5b-347">但筛选器又不同于中间件，它们是 MVC 的一部分，这意味着它们有权访问 MVC 上下文和构造。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-347">But filters differ from middleware in that they're part of MVC, which means that they have access to MVC context and constructs.</span></span>

<span data-ttu-id="5fd5b-348">在 ASP.NET Core 1.1 中，可以在筛选器管道中使用中间件。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-348">In ASP.NET Core 1.1, you can use middleware in the filter pipeline.</span></span> <span data-ttu-id="5fd5b-349">如果有一个中间件组件，该组件需要访问 MVC 路由数据，或者只能针对特定控制器或操作运行，则可能需要这样做。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-349">You might want to do that if you have a middleware component that needs access to MVC route data, or one that should run only for certain controllers or actions.</span></span>

<span data-ttu-id="5fd5b-350">若要将中间件用作筛选器，可创建一个具有 `Configure` 方法的类型，该方法可指定要注入到筛选器管道的中间件。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-350">To use middleware as a filter, create a type with a `Configure` method that specifies the middleware that you want to inject into the filter pipeline.</span></span> <span data-ttu-id="5fd5b-351">下面的示例使用本地化中间件为请求建立当前区域性：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-351">Here's an example that uses the localization middleware to establish the current culture for a request:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Filters/LocalizationPipeline.cs?name=snippet_MiddlewareFilter&highlight=3,21)]

<span data-ttu-id="5fd5b-352">然后，可以使用 `MiddlewareFilterAttribute` 为所选控制器或操作或者在全局范围内运行中间件：</span><span class="sxs-lookup"><span data-stu-id="5fd5b-352">You can then use the `MiddlewareFilterAttribute` to run the middleware for a selected controller or action or globally:</span></span>

[!code-csharp[Main](./filters/sample/src/FiltersSample/Controllers/HomeController.cs?name=snippet_MiddlewareFilter&highlight=2)]

<span data-ttu-id="5fd5b-353">中间件筛选器与资源筛选器在筛选器管道的相同阶段运行，即，在模型绑定之前以及管道的其余阶段之后。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-353">Middleware filters run at the same stage of the filter pipeline as Resource filters, before model binding and after the rest of the pipeline.</span></span>

## <a name="next-actions"></a><span data-ttu-id="5fd5b-354">后续操作</span><span class="sxs-lookup"><span data-stu-id="5fd5b-354">Next actions</span></span>

<span data-ttu-id="5fd5b-355">若要尝试使用筛选器，请[下载、测试并修改该示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample)。</span><span class="sxs-lookup"><span data-stu-id="5fd5b-355">To experiment with filters, [download, test and modify the sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/filters/sample).</span></span>
