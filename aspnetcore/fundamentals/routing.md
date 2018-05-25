---
title: ASP.NET Core 中的路由
author: ardalis
description: 了解 ASP.NET Core 路由功能如何负责将传入请求映射到路由处理程序。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/routing
ms.openlocfilehash: d9d5a26b08f67fe4ee39d6b974027826a93e5d5f
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="routing-in-aspnet-core"></a><span data-ttu-id="65aec-103">ASP.NET Core 中的路由</span><span class="sxs-lookup"><span data-stu-id="65aec-103">Routing in ASP.NET Core</span></span>

<span data-ttu-id="65aec-104">撰写者：[Ryan Nowak](https://github.com/rynowak)、[Steve Smith](https://ardalis.com/) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="65aec-104">By [Ryan Nowak](https://github.com/rynowak), [Steve Smith](https://ardalis.com/), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="65aec-105">路由功能负责将传入请求映射到路由处理程序。</span><span class="sxs-lookup"><span data-stu-id="65aec-105">Routing functionality is responsible for mapping an incoming request to a route handler.</span></span> <span data-ttu-id="65aec-106">路由在 ASP.NET 应用中定义，并在应用启动时进行配置。</span><span class="sxs-lookup"><span data-stu-id="65aec-106">Routes are defined in the ASP.NET app and configured when the app starts up.</span></span> <span data-ttu-id="65aec-107">路由可以选择从请求包含的 URL 中提取值，然后这些值便可用于处理请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-107">A route can optionally extract values from the URL contained in the request, and these values can then be used for request processing.</span></span> <span data-ttu-id="65aec-108">使用 ASP.NET 应用中的路由信息，路由功能还能生成要映射到路由处理程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-108">Using route information from the ASP.NET app, the routing functionality is also able to generate URLs that map to route handlers.</span></span> <span data-ttu-id="65aec-109">因此，路由可以根据 URL 查找路由处理程序，或者根据路由处理程序信息查找给定路由处理程序对应的 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-109">Therefore, routing can find a route handler based on a URL, or the URL corresponding to a given route handler based on route handler information.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="65aec-110">本文档介绍较低级别的 ASP.NET Core 路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-110">This document covers the low level ASP.NET Core routing.</span></span> <span data-ttu-id="65aec-111">有关 ASP.NET Core MVC 路由的信息，请参阅[路由到控制器操作](../mvc/controllers/routing.md)</span><span class="sxs-lookup"><span data-stu-id="65aec-111">For ASP.NET Core MVC routing, see [Route to controller actions](../mvc/controllers/routing.md)</span></span>

<span data-ttu-id="65aec-112">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="65aec-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/routing/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="routing-basics"></a><span data-ttu-id="65aec-113">路由基础知识</span><span class="sxs-lookup"><span data-stu-id="65aec-113">Routing basics</span></span>

<span data-ttu-id="65aec-114">路由使用路由（[IRouter](/dotnet/api/microsoft.aspnetcore.routing.irouter) 的实现）来：</span><span class="sxs-lookup"><span data-stu-id="65aec-114">Routing uses *routes* (implementations of [IRouter](/dotnet/api/microsoft.aspnetcore.routing.irouter)) to:</span></span>

* <span data-ttu-id="65aec-115">将传入请求映射到路由处理程序</span><span class="sxs-lookup"><span data-stu-id="65aec-115">map incoming requests to *route handlers*</span></span>

* <span data-ttu-id="65aec-116">生成响应中使用的 URL</span><span class="sxs-lookup"><span data-stu-id="65aec-116">generate URLs used in responses</span></span>

<span data-ttu-id="65aec-117">通常情况下，应用具有一个路由集合。</span><span class="sxs-lookup"><span data-stu-id="65aec-117">Generally, an app has a single collection of routes.</span></span> <span data-ttu-id="65aec-118">请求到达时，将按顺序处理路由集合。</span><span class="sxs-lookup"><span data-stu-id="65aec-118">When a request arrives, the route collection is processed in order.</span></span> <span data-ttu-id="65aec-119">传入请求通过对路由集合中的每个可用路由调用 `RouteAsync` 方法来查找与请求 URL 匹配的路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-119">The incoming request looks for a route that matches the request URL by calling the `RouteAsync` method on each available route in the route collection.</span></span> <span data-ttu-id="65aec-120">与此相反，响应可根据路由信息使用路由生成 URL（例如，用于重定向或链接），并因此避免需要硬编码 URL，这有助于可维护性。</span><span class="sxs-lookup"><span data-stu-id="65aec-120">By contrast, a response can use routing to generate URLs (for example, for redirection or links) based on route information, and thus avoid having to hard-code URLs, which helps maintainability.</span></span>

<span data-ttu-id="65aec-121">路由通过 `RouterMiddleware` 类连接到[中间件](xref:fundamentals/middleware/index)管道。</span><span class="sxs-lookup"><span data-stu-id="65aec-121">Routing is connected to the [middleware](xref:fundamentals/middleware/index) pipeline by the `RouterMiddleware` class.</span></span> <span data-ttu-id="65aec-122">[ASP.NET Core MVC](xref:mvc/overview) 向中间件管道添加路由，作为其配置的一部分。</span><span class="sxs-lookup"><span data-stu-id="65aec-122">[ASP.NET Core MVC](xref:mvc/overview) adds routing to the middleware pipeline as part of its configuration.</span></span> <span data-ttu-id="65aec-123">若要了解如何使用路由作为独立组件，请参阅[使用路由中间件](#using-routing-middleware)。</span><span class="sxs-lookup"><span data-stu-id="65aec-123">To learn about using routing as a standalone component, see [Using routing middleware](#using-routing-middleware).</span></span>

<a name="url-matching-ref"></a>

### <a name="url-matching"></a><span data-ttu-id="65aec-124">URL 匹配</span><span class="sxs-lookup"><span data-stu-id="65aec-124">URL matching</span></span>

<span data-ttu-id="65aec-125">URL 匹配是一个过程，通过该过程，路由可向处理程序调度传入请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-125">URL matching is the process by which routing dispatches an incoming request to a *handler*.</span></span> <span data-ttu-id="65aec-126">此过程通常基于 URL 路径中的数据，但可进行扩展以考虑请求中的任何数据。</span><span class="sxs-lookup"><span data-stu-id="65aec-126">This process is generally based on data in the URL path, but can be extended to consider any data in the request.</span></span> <span data-ttu-id="65aec-127">向单独的处理程序调度请求的功能是缩放应用程序的大小和复杂性的关键。</span><span class="sxs-lookup"><span data-stu-id="65aec-127">The ability to dispatch requests to separate handlers is key to scaling the size and complexity of an application.</span></span>

<span data-ttu-id="65aec-128">传入请求将进入 `RouterMiddleware`，后者将对序列中的每个路由调用 `RouteAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="65aec-128">Incoming requests enter the `RouterMiddleware`, which calls the `RouteAsync` method on each route in sequence.</span></span> <span data-ttu-id="65aec-129">`IRouter` 实例将选择是否通过将 `RouteContext.Handler` 设置为非空 `RequestDelegate` 来处理请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-129">The `IRouter` instance chooses whether to *handle* the request by setting the `RouteContext.Handler` to a non-null `RequestDelegate`.</span></span> <span data-ttu-id="65aec-130">如果路由为请求设置处理程序，路由处理将停止，处理程序将被调用以处理该请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-130">If a route sets a handler for the request, route processing stops and the handler will be invoked to process the request.</span></span> <span data-ttu-id="65aec-131">如果尝试了所有路由，且请求未找到任何处理程序，中间件将调用 next，请求管道中的下一个中间件将被调用。</span><span class="sxs-lookup"><span data-stu-id="65aec-131">If all routes are tried and no handler is found for the request, the middleware calls *next* and the next middleware in the request pipeline is invoked.</span></span>

<span data-ttu-id="65aec-132">`RouteAsync` 的主要输入是与当前请求关联的 `RouteContext.HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="65aec-132">The primary input to `RouteAsync` is the `RouteContext.HttpContext` associated with the current request.</span></span> <span data-ttu-id="65aec-133">`RouteContext.Handler` 和 `RouteContext.RouteData` 是将在路由匹配后设置的输出。</span><span class="sxs-lookup"><span data-stu-id="65aec-133">The `RouteContext.Handler` and `RouteContext.RouteData` are outputs that will be set after a route matches.</span></span>

<span data-ttu-id="65aec-134">`RouteAsync` 期间的匹配还可根据迄今完成的请求处理将 `RouteContext.RouteData` 的属性设为适当的值。</span><span class="sxs-lookup"><span data-stu-id="65aec-134">A match during `RouteAsync` will also set the properties of the `RouteContext.RouteData` to appropriate values based on the request processing done so far.</span></span> <span data-ttu-id="65aec-135">如果路由与请求匹配，`RouteContext.RouteData` 将包含有关结果的重要状态信息。</span><span class="sxs-lookup"><span data-stu-id="65aec-135">If a route matches a request, the `RouteContext.RouteData` will contain important state information about the *result*.</span></span>

<span data-ttu-id="65aec-136">`RouteData.Values` 是从路由中生成的路由值的字典。</span><span class="sxs-lookup"><span data-stu-id="65aec-136">`RouteData.Values` is a dictionary of *route values* produced from the route.</span></span> <span data-ttu-id="65aec-137">这些值通常通过标记 URL 来确定，可用来接受用户输入，或者在应用程序内作出进一步的调度决策。</span><span class="sxs-lookup"><span data-stu-id="65aec-137">These values are usually determined by tokenizing the URL, and can be used to accept user input, or to make further dispatching decisions inside the application.</span></span>

<span data-ttu-id="65aec-138">`RouteData.DataTokens` 是一个与匹配的路由相关的其他数据的属性包。</span><span class="sxs-lookup"><span data-stu-id="65aec-138">`RouteData.DataTokens`  is a property bag of additional data related to the matched route.</span></span> <span data-ttu-id="65aec-139">提供 `DataTokens` 以支持将状态数据与每个路由相关联，以便应用程序稍后可根据所匹配的路由作出决策。</span><span class="sxs-lookup"><span data-stu-id="65aec-139">`DataTokens` are provided to support associating state data with each route so the application can make decisions later based on which route matched.</span></span> <span data-ttu-id="65aec-140">这些值是开发者定义的，不会影响通过任何方式路由的行为。</span><span class="sxs-lookup"><span data-stu-id="65aec-140">These values are developer-defined and do **not** affect the behavior of routing in any way.</span></span> <span data-ttu-id="65aec-141">此外，存储于数据令牌中的值可以属于任何类型，与路由值相反，后者必须能够轻松转换为字符串，或从字符串进行转换。</span><span class="sxs-lookup"><span data-stu-id="65aec-141">Additionally, values stashed in data tokens can be of any type, in contrast to route values, which must be easily convertible to and from strings.</span></span>

<span data-ttu-id="65aec-142">`RouteData.Routers` 是参与成功匹配请求的路由的列表。</span><span class="sxs-lookup"><span data-stu-id="65aec-142">`RouteData.Routers` is a list of the routes that took part in successfully matching the request.</span></span> <span data-ttu-id="65aec-143">路由可以嵌套在另一路由内，并且 `Routers` 属性可以通过导致匹配的逻辑路由树反映该路径。</span><span class="sxs-lookup"><span data-stu-id="65aec-143">Routes can be nested inside one another, and the `Routers` property reflects the path through the logical tree of routes that resulted in a match.</span></span> <span data-ttu-id="65aec-144">通常情况下，`Routers` 中的第一项是路由集合，应该用于生成 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-144">Generally the first item in `Routers` is the route collection, and should be used for URL generation.</span></span> <span data-ttu-id="65aec-145">`Routers` 中的最后一项是匹配的路由处理程序。</span><span class="sxs-lookup"><span data-stu-id="65aec-145">The last item in `Routers` is the route handler that matched.</span></span>

### <a name="url-generation"></a><span data-ttu-id="65aec-146">URL 生成</span><span class="sxs-lookup"><span data-stu-id="65aec-146">URL generation</span></span>

<span data-ttu-id="65aec-147">URL 生成是通过其可根据一组路由值创建 URL 路径的过程。</span><span class="sxs-lookup"><span data-stu-id="65aec-147">URL generation is the process by which routing can create a URL path based on a set of route values.</span></span> <span data-ttu-id="65aec-148">这需要考虑处理程序与访问它们的 URL 之间的逻辑分隔。</span><span class="sxs-lookup"><span data-stu-id="65aec-148">This allows for a logical separation between your handlers and the URLs that access them.</span></span>

<span data-ttu-id="65aec-149">URL 遵循类似的迭代过程，但开头是将用户或框架代码调用到路由集合的 `GetVirtualPath` 方法中。</span><span class="sxs-lookup"><span data-stu-id="65aec-149">URL generation follows a similar iterative process, but starts with user or framework code calling into the `GetVirtualPath` method of the route collection.</span></span> <span data-ttu-id="65aec-150">然后，每个路由会有序地调用其 `GetVirtualPath` 方法，直到返回非空的 `VirtualPathData`。</span><span class="sxs-lookup"><span data-stu-id="65aec-150">Each *route* will then have its `GetVirtualPath` method called in sequence until a non-null `VirtualPathData` is returned.</span></span>

<span data-ttu-id="65aec-151">`GetVirtualPath` 的主输入有：</span><span class="sxs-lookup"><span data-stu-id="65aec-151">The primary inputs to `GetVirtualPath` are:</span></span>

* `VirtualPathContext.HttpContext`

* `VirtualPathContext.Values`

* `VirtualPathContext.AmbientValues`

<span data-ttu-id="65aec-152">路由主要使用 `Values` 和 `AmbientValues` 提供的路由值来决定可能生成 URL 的位置以及要包括的值。</span><span class="sxs-lookup"><span data-stu-id="65aec-152">Routes primarily use the route values provided by the `Values` and `AmbientValues` to decide where it's possible to generate a URL and what values to include.</span></span> <span data-ttu-id="65aec-153">`AmbientValues` 是路由值的集合，这些值是通过将当前请求与路由系统相匹配而产生的。</span><span class="sxs-lookup"><span data-stu-id="65aec-153">The `AmbientValues` are the set of route values that were produced from matching the current request with the routing system.</span></span> <span data-ttu-id="65aec-154">与此相反，`Values` 是指定如何为当前操作生成所需 URL 的路由值。</span><span class="sxs-lookup"><span data-stu-id="65aec-154">In contrast, `Values` are the route values that specify how to generate the desired URL for the current operation.</span></span> <span data-ttu-id="65aec-155">当路由需要获取与当前上下文关联的服务或其他数据时，需提供 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="65aec-155">The `HttpContext` is provided in case a route needs to get services or additional data associated with the current context.</span></span>

<span data-ttu-id="65aec-156">提示：将 `Values` 作为 `AmbientValues` 的一组替代值。</span><span class="sxs-lookup"><span data-stu-id="65aec-156">Tip: Think of `Values` as being a set of overrides for the `AmbientValues`.</span></span> <span data-ttu-id="65aec-157">URL 生成尝试重复使用当前请求中的路由值，以便轻松使用相同路由或路由值生成链接的 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-157">URL generation tries to reuse route values from the current request to make it easy to generate URLs for links using the same route or route values.</span></span>

<span data-ttu-id="65aec-158">`GetVirtualPath` 的输出是 `VirtualPathData`。</span><span class="sxs-lookup"><span data-stu-id="65aec-158">The output of `GetVirtualPath` is a `VirtualPathData`.</span></span> <span data-ttu-id="65aec-159">`VirtualPathData` 是 `RouteData` 的并行值，它包含输出 URL 的 `VirtualPath` 以及路由应该设置的某些其他属性。</span><span class="sxs-lookup"><span data-stu-id="65aec-159">`VirtualPathData` is a parallel of `RouteData`; it contains the `VirtualPath` for the output URL and some additional properties that should be set by the route.</span></span>

<span data-ttu-id="65aec-160">`VirtualPathData.VirtualPath` 属性包含路由生成的虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="65aec-160">The `VirtualPathData.VirtualPath` property contains the *virtual path* produced by the route.</span></span> <span data-ttu-id="65aec-161">你可能需要进一步处理路径，具体取决于你的需求。</span><span class="sxs-lookup"><span data-stu-id="65aec-161">Depending on your needs you may need to process the path further.</span></span> <span data-ttu-id="65aec-162">例如，如果要在 HTML 中呈现生成的 URL，需要预先计算应用程序的基路径。</span><span class="sxs-lookup"><span data-stu-id="65aec-162">For instance, if you want to render the generated URL in HTML you need to prepend the base path of the application.</span></span>

<span data-ttu-id="65aec-163">`VirtualPathData.Router` 是对已成功生成 URL 的路由的引用。</span><span class="sxs-lookup"><span data-stu-id="65aec-163">The `VirtualPathData.Router` is a reference to the route that successfully generated the URL.</span></span>

<span data-ttu-id="65aec-164">`VirtualPathData.DataTokens` 属性是生成 URL 的路由的其他相关数据的字典。</span><span class="sxs-lookup"><span data-stu-id="65aec-164">The `VirtualPathData.DataTokens` properties is a dictionary of additional data related to the route that generated the URL.</span></span> <span data-ttu-id="65aec-165">它是 `RouteData.DataTokens` 的并行值。</span><span class="sxs-lookup"><span data-stu-id="65aec-165">This is the parallel of `RouteData.DataTokens`.</span></span>

### <a name="creating-routes"></a><span data-ttu-id="65aec-166">创建路由</span><span class="sxs-lookup"><span data-stu-id="65aec-166">Creating routes</span></span>

<span data-ttu-id="65aec-167">路由提供 `Route` 类，作为 `IRouter` 的标准实现。</span><span class="sxs-lookup"><span data-stu-id="65aec-167">Routing provides the `Route` class as the standard implementation of `IRouter`.</span></span> <span data-ttu-id="65aec-168">`Route` 使用 route template 语法来定义调用 `RouteAsync` 时将针对 URL 路径进行匹配的模式。</span><span class="sxs-lookup"><span data-stu-id="65aec-168">`Route` uses the *route template* syntax to define patterns that will match against the URL path when `RouteAsync` is called.</span></span> <span data-ttu-id="65aec-169">调用 `GetVirtualPath` 时，`Route` 将使用相同的路由模板生成 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-169">`Route` will use the same route template to generate a URL when `GetVirtualPath` is called.</span></span>

<span data-ttu-id="65aec-170">大多数应用程序通过调用 `MapRoute` 或 `IRouteBuilder` 上定义的一种类似的扩展方法来创建路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-170">Most applications will create routes by calling `MapRoute` or one of the similar extension methods defined on `IRouteBuilder`.</span></span> <span data-ttu-id="65aec-171">所有方法都将创建 `Route` 的实例，并将其添加到路由集合中。</span><span class="sxs-lookup"><span data-stu-id="65aec-171">All of these methods will create an instance of `Route` and add it to the route collection.</span></span>

<span data-ttu-id="65aec-172">注意：`MapRoute` 不采用任何路由处理程序参数，它只添加将由 `DefaultHandler` 处理的路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-172">Note: `MapRoute` doesn't take a route handler parameter - it only adds routes that will be handled by the `DefaultHandler`.</span></span> <span data-ttu-id="65aec-173">由于默认处理程序是 `IRouter`，它可能决定不处理该请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-173">Since the default handler is an `IRouter`, it may decide not to handle the request.</span></span> <span data-ttu-id="65aec-174">例如，Microsoft ASP.NET MVC 通常被配置为默认处理程序，仅处理与可用控制器和操作匹配的请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-174">For example, ASP.NET MVC is typically configured as a default handler that only handles requests that match an available controller and action.</span></span> <span data-ttu-id="65aec-175">要了解路由到 MVC 的详细信息，请参阅[路由到控制器操作](../mvc/controllers/routing.md)。</span><span class="sxs-lookup"><span data-stu-id="65aec-175">To learn more about routing to MVC, see [Route to controller actions](../mvc/controllers/routing.md).</span></span>

<span data-ttu-id="65aec-176">下面是典型 ASP.NET MVC 路由定义使用的一个 `MapRoute` 调用示例：</span><span class="sxs-lookup"><span data-stu-id="65aec-176">This is an example of a `MapRoute` call used by a typical ASP.NET MVC route definition:</span></span>

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

<span data-ttu-id="65aec-177">此模板将匹配类似 `/Products/Details/17` 的 URL 路径并提取路由值 `{ controller = Products, action = Details, id = 17 }`。</span><span class="sxs-lookup"><span data-stu-id="65aec-177">This template will match a URL path like `/Products/Details/17` and extract the route values `{ controller = Products, action = Details, id = 17 }`.</span></span> <span data-ttu-id="65aec-178">路由值是通过将 URL 路径拆分成段，并且将每段与路由模板中的路由参数名称相匹配来确定的。</span><span class="sxs-lookup"><span data-stu-id="65aec-178">The route values are determined by splitting the URL path into segments, and matching each segment with the *route parameter* name in the route template.</span></span> <span data-ttu-id="65aec-179">路由参数已命名。</span><span class="sxs-lookup"><span data-stu-id="65aec-179">Route parameters are named.</span></span> <span data-ttu-id="65aec-180">它们是通过将参数名称括在大括号 `{ }` 中进行定义的。</span><span class="sxs-lookup"><span data-stu-id="65aec-180">They're defined by enclosing the parameter name in braces `{ }`.</span></span>

<span data-ttu-id="65aec-181">上述模板还可匹配 URL 路径 `/`，并且将生成值 `{ controller = Home, action = Index }`。</span><span class="sxs-lookup"><span data-stu-id="65aec-181">The template above could also match the URL path `/` and would produce the values `{ controller = Home, action = Index }`.</span></span> <span data-ttu-id="65aec-182">这是因为 `{controller}` 和 `{action}` 路由参数具有默认值，而 `id` 路由参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="65aec-182">This happens because the `{controller}` and `{action}` route parameters have default values, and the `id` route parameter is optional.</span></span> <span data-ttu-id="65aec-183">路由参数名称为参数定义默认值后，等号 `=` 后将有一个值。</span><span class="sxs-lookup"><span data-stu-id="65aec-183">An equals `=` sign followed by a value after the route parameter name defines a default value for the parameter.</span></span> <span data-ttu-id="65aec-184">路由参数名称后的问号 `?` 将参数定义为可选。</span><span class="sxs-lookup"><span data-stu-id="65aec-184">A question mark `?` after the route parameter name defines the parameter as optional.</span></span> <span data-ttu-id="65aec-185">具有默认值“始终”的路由参数将在路由匹配时生成路由值，如果没有对应的 URL 路径段，可选参数不会生成路由值。</span><span class="sxs-lookup"><span data-stu-id="65aec-185">Route parameters with a default value *always* produce a route value when the route matches - optional parameters won't produce a route value if there was no corresponding URL path segment.</span></span>

<span data-ttu-id="65aec-186">有关路由模板功能和语法的详细说明，请参阅 [route-template-reference](#route-template-reference)。</span><span class="sxs-lookup"><span data-stu-id="65aec-186">See [route-template-reference](#route-template-reference) for a thorough description of route template features and syntax.</span></span>

<span data-ttu-id="65aec-187">此示例包括路由约束：</span><span class="sxs-lookup"><span data-stu-id="65aec-187">This example includes a *route constraint*:</span></span>

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id:int}");
```

<span data-ttu-id="65aec-188">此模板将匹配类似 `/Products/Details/17` 而不是 `/Products/Details/Apples` 的 URL 路径。</span><span class="sxs-lookup"><span data-stu-id="65aec-188">This template will match a URL path like `/Products/Details/17`, but not `/Products/Details/Apples`.</span></span> <span data-ttu-id="65aec-189">路由参数定义 `{id:int}` 为 `id` 路由参数定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="65aec-189">The route parameter definition `{id:int}` defines a *route constraint* for the `id` route parameter.</span></span> <span data-ttu-id="65aec-190">路由约束实现 `IRouteConstraint` 并检查路由值，以验证它们。</span><span class="sxs-lookup"><span data-stu-id="65aec-190">Route constraints implement `IRouteConstraint` and inspect route values to verify them.</span></span> <span data-ttu-id="65aec-191">在此示例中，路由值 `id` 必须可转换为整数。</span><span class="sxs-lookup"><span data-stu-id="65aec-191">In this example the route value `id` must be convertible to an integer.</span></span> <span data-ttu-id="65aec-192">有关框架提供的路由约束的更详细说明，请参阅 [route-constraint-reference](#route-constraint-reference)。</span><span class="sxs-lookup"><span data-stu-id="65aec-192">See [route-constraint-reference](#route-constraint-reference) for a more detailed explanation of route constraints that are provided by the framework.</span></span>

<span data-ttu-id="65aec-193">其他 `MapRoute` 重载接受 `constraints`、`dataTokens` 和 `defaults` 的值。</span><span class="sxs-lookup"><span data-stu-id="65aec-193">Additional overloads of `MapRoute` accept values for `constraints`, `dataTokens`, and `defaults`.</span></span> <span data-ttu-id="65aec-194">`MapRoute` 的此类附加参数被定义为 `object` 类型。</span><span class="sxs-lookup"><span data-stu-id="65aec-194">These additional parameters of `MapRoute` are defined as type `object`.</span></span> <span data-ttu-id="65aec-195">这些参数的典型用法是传递匿名类型化对象，其中匿名类型的属性名匹配路由参数名称。</span><span class="sxs-lookup"><span data-stu-id="65aec-195">The typical usage of these parameters is to pass an anonymously typed object, where the property names of the anonymous type match route parameter names.</span></span>

<span data-ttu-id="65aec-196">以下两个示例可创建等效路由：</span><span class="sxs-lookup"><span data-stu-id="65aec-196">The following two examples create equivalent routes:</span></span>

```csharp
routes.MapRoute(
    name: "default_route",
    template: "{controller}/{action}/{id?}",
    defaults: new { controller = "Home", action = "Index" });

routes.MapRoute(
    name: "default_route",
    template: "{controller=Home}/{action=Index}/{id?}");
```

<span data-ttu-id="65aec-197">提示：定义约束和默认值的内联语法对简单路由可以更方便。</span><span class="sxs-lookup"><span data-stu-id="65aec-197">Tip: The inline syntax for defining constraints and defaults can be more convenient for simple routes.</span></span> <span data-ttu-id="65aec-198">但是，存在内联语法不支持的功能，例如数据令牌。</span><span class="sxs-lookup"><span data-stu-id="65aec-198">However, there are features such as data tokens which are not supported by inline syntax.</span></span>

<span data-ttu-id="65aec-199">此示例演示其他几个功能：</span><span class="sxs-lookup"><span data-stu-id="65aec-199">This example demonstrates a few more features:</span></span>

```csharp
routes.MapRoute(
  name: "blog",
  template: "Blog/{*article}",
  defaults: new { controller = "Blog", action = "ReadArticle" });
```

<span data-ttu-id="65aec-200">此模板将匹配类似 `/Blog/All-About-Routing/Introduction` 的 URL 路径并提取值 `{ controller = Blog, action = ReadArticle, article = All-About-Routing/Introduction }`。</span><span class="sxs-lookup"><span data-stu-id="65aec-200">This template will match a URL path like `/Blog/All-About-Routing/Introduction` and will extract the values `{ controller = Blog, action = ReadArticle, article = All-About-Routing/Introduction }`.</span></span> <span data-ttu-id="65aec-201">`controller` 和 `action` 的默认路由值由路由生成，即便模板中没有对应的路由参数。</span><span class="sxs-lookup"><span data-stu-id="65aec-201">The default route values for `controller` and `action` are produced by the route even though there are no corresponding route parameters in the template.</span></span> <span data-ttu-id="65aec-202">可在路由模板中指定默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-202">Default values can be specified in the route template.</span></span> <span data-ttu-id="65aec-203">根据路由参数名称前的星号  *外观，`article` 路由参数被定义为全方位*`*`。</span><span class="sxs-lookup"><span data-stu-id="65aec-203">The `article` route parameter is defined as a *catch-all* by the appearance of an asterisk `*` before the route parameter name.</span></span> <span data-ttu-id="65aec-204">全方位路由参数可捕获 URL 路径的其余部分，也能匹配空白字符串。</span><span class="sxs-lookup"><span data-stu-id="65aec-204">Catch-all route parameters capture the remainder of the URL path, and can also match the empty string.</span></span>

<span data-ttu-id="65aec-205">此示例可添加路由约束和数据令牌：</span><span class="sxs-lookup"><span data-stu-id="65aec-205">This example adds route constraints and data tokens:</span></span>

```csharp
routes.MapRoute(
    name: "us_english_products",
    template: "en-US/Products/{id}",
    defaults: new { controller = "Products", action = "Details" },
    constraints: new { id = new IntRouteConstraint() },
    dataTokens: new { locale = "en-US" });
```

<span data-ttu-id="65aec-206">此模板将匹配类似 `/Products/5` 的 URL 路径并提取值 `{ controller = Products, action = Details, id = 5 }` 和数据令牌 `{ locale = en-US }`。</span><span class="sxs-lookup"><span data-stu-id="65aec-206">This template will match a URL path like `/Products/5` and will extract the values `{ controller = Products, action = Details, id = 5 }` and the data tokens `{ locale = en-US }`.</span></span>

![本地 Windows 令牌](routing/_static/tokens.png)

<a name="id1"></a>

### <a name="url-generation"></a><span data-ttu-id="65aec-208">URL 生成</span><span class="sxs-lookup"><span data-stu-id="65aec-208">URL generation</span></span>

<span data-ttu-id="65aec-209">`Route` 类还可通过将一组路由值与其路由模板组合来生成 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-209">The `Route` class can also perform URL generation by combining a set of route values with its route template.</span></span> <span data-ttu-id="65aec-210">从逻辑上来说，这是匹配 URL 路径的反向过程。</span><span class="sxs-lookup"><span data-stu-id="65aec-210">This is logically the reverse process of matching the URL path.</span></span>

<span data-ttu-id="65aec-211">提示：为更好了解 URL 生成，请想象你要生成的 URL，然后考虑路由模板将如何匹配该 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-211">Tip: To better understand URL generation, imagine what URL you want to generate and then think about how a route template would match that URL.</span></span> <span data-ttu-id="65aec-212">将生成什么值？</span><span class="sxs-lookup"><span data-stu-id="65aec-212">What values would be produced?</span></span> <span data-ttu-id="65aec-213">这大致相当于 URL 在 `Route` 类中的生成方式。</span><span class="sxs-lookup"><span data-stu-id="65aec-213">This is the rough equivalent of how URL generation works in the `Route` class.</span></span>

<span data-ttu-id="65aec-214">此示例使用基本的 ASP.NET MVC 样式路由：</span><span class="sxs-lookup"><span data-stu-id="65aec-214">This example uses a basic ASP.NET MVC style route:</span></span>

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
```

<span data-ttu-id="65aec-215">使用路由值 `{ controller = Products, action = List }`，此路由将生成 URL `/Products/List`。</span><span class="sxs-lookup"><span data-stu-id="65aec-215">With the route values `{ controller = Products, action = List }`, this route will generate the URL `/Products/List`.</span></span> <span data-ttu-id="65aec-216">路由值将替换为相应的路由参数，以形成 URL 路径。</span><span class="sxs-lookup"><span data-stu-id="65aec-216">The route values are substituted for the corresponding route parameters to form the URL path.</span></span> <span data-ttu-id="65aec-217">由于 `id` 属于可选路由参数，因此它可以没有值。</span><span class="sxs-lookup"><span data-stu-id="65aec-217">Since `id` is an optional route parameter, it's no problem that it doesn't have a value.</span></span>

<span data-ttu-id="65aec-218">使用路由值 `{ controller = Home, action = Index }`，此路由将生成 URL `/`。</span><span class="sxs-lookup"><span data-stu-id="65aec-218">With the route values `{ controller = Home, action = Index }`, this route will generate the URL `/`.</span></span> <span data-ttu-id="65aec-219">提供的路由值匹配默认值，因此可以安全忽略这些值对应的段。</span><span class="sxs-lookup"><span data-stu-id="65aec-219">The route values that were provided match the default values so the segments corresponding to those values can be safely omitted.</span></span> <span data-ttu-id="65aec-220">请注意，已生成的两个 URL 将往返这个路由定义，并生成用于生成该 URL 的相同路由值。</span><span class="sxs-lookup"><span data-stu-id="65aec-220">Note that both URLs generated would round-trip with this route definition and produce the same route values that were used to generate the URL.</span></span>

<span data-ttu-id="65aec-221">提示：使用 ASP.NET MVC 应用应该使用 `UrlHelper` 生成 URL，而不是直接调用到路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-221">Tip: An app using ASP.NET MVC should use `UrlHelper` to generate URLs instead of calling into routing directly.</span></span>

<span data-ttu-id="65aec-222">有关 URL 生成过程的更多详细信息，请参阅 [url-generation-reference](#url-generation-reference)。</span><span class="sxs-lookup"><span data-stu-id="65aec-222">For more details about the URL generation process, see [url-generation-reference](#url-generation-reference).</span></span>

## <a name="using-routing-middleware"></a><span data-ttu-id="65aec-223">使用路由中间件</span><span class="sxs-lookup"><span data-stu-id="65aec-223">Using Routing Middleware</span></span>

<span data-ttu-id="65aec-224">添加 NuGet 包“Microsoft.AspNetCore.Routing”。</span><span class="sxs-lookup"><span data-stu-id="65aec-224">Add the NuGet package "Microsoft.AspNetCore.Routing".</span></span>

<span data-ttu-id="65aec-225">将路由添加到 Startup.cs 中的服务容器：</span><span class="sxs-lookup"><span data-stu-id="65aec-225">Add routing to the service container in *Startup.cs*:</span></span>

[!code-csharp[](../fundamentals/routing/sample/RoutingSample/Startup.cs?highlight=3&start=11&end=14)]

<span data-ttu-id="65aec-226">必须在 `Startup` 类的 `Configure` 方法中配置路由。</span><span class="sxs-lookup"><span data-stu-id="65aec-226">Routes must be configured in the `Configure` method in the `Startup` class.</span></span> <span data-ttu-id="65aec-227">下面的示例使用这些 API：</span><span class="sxs-lookup"><span data-stu-id="65aec-227">The sample below uses these APIs:</span></span>

* `RouteBuilder`
* `Build`
* <span data-ttu-id="65aec-228">`MapGet` 仅匹配 HTTP GET 请求</span><span class="sxs-lookup"><span data-stu-id="65aec-228">`MapGet`  Matches only HTTP GET requests</span></span>
* `UseRouter`

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    var trackPackageRouteHandler = new RouteHandler(context =>
    {
        var routeValues = context.GetRouteData().Values;
        return context.Response.WriteAsync(
            $"Hello! Route values: {string.Join(", ", routeValues)}");
    });

    var routeBuilder = new RouteBuilder(app, trackPackageRouteHandler);

    routeBuilder.MapRoute(
        "Track Package Route",
        "package/{operation:regex(^(track|create|detonate)$)}/{id:int}");

    routeBuilder.MapGet("hello/{name}", context =>
    {
        var name = context.GetRouteValue("name");
        // This is the route handler when HTTP GET "hello/<anything>"  matches
        // To match HTTP GET "hello/<anything>/<anything>,
        // use routeBuilder.MapGet("hello/{*name}"
        return context.Response.WriteAsync($"Hi, {name}!");
    });

    var routes = routeBuilder.Build();
    app.UseRouter(routes);
}
```

<span data-ttu-id="65aec-229">下表显示了具有给定 URL 的响应。</span><span class="sxs-lookup"><span data-stu-id="65aec-229">The table below shows the responses with the given URIs.</span></span>

| <span data-ttu-id="65aec-230">URI</span><span class="sxs-lookup"><span data-stu-id="65aec-230">URI</span></span> | <span data-ttu-id="65aec-231">响应</span><span class="sxs-lookup"><span data-stu-id="65aec-231">Response</span></span>  |
| ------- | -------- |
| <span data-ttu-id="65aec-232">/package/create/3</span><span class="sxs-lookup"><span data-stu-id="65aec-232">/package/create/3</span></span>  | <span data-ttu-id="65aec-233">Hello!</span><span class="sxs-lookup"><span data-stu-id="65aec-233">Hello!</span></span> <span data-ttu-id="65aec-234">Route values: [operation, create], [id, 3]</span><span class="sxs-lookup"><span data-stu-id="65aec-234">Route values: [operation, create], [id, 3]</span></span> |
| <span data-ttu-id="65aec-235">/package/track/-3</span><span class="sxs-lookup"><span data-stu-id="65aec-235">/package/track/-3</span></span>  | <span data-ttu-id="65aec-236">Hello!</span><span class="sxs-lookup"><span data-stu-id="65aec-236">Hello!</span></span> <span data-ttu-id="65aec-237">Route values: [operation, track], [id, -3]</span><span class="sxs-lookup"><span data-stu-id="65aec-237">Route values: [operation, track], [id, -3]</span></span> |
| <span data-ttu-id="65aec-238">/package/track/-3/</span><span class="sxs-lookup"><span data-stu-id="65aec-238">/package/track/-3/</span></span> | <span data-ttu-id="65aec-239">Hello!</span><span class="sxs-lookup"><span data-stu-id="65aec-239">Hello!</span></span> <span data-ttu-id="65aec-240">Route values: [operation, track], [id, -3]</span><span class="sxs-lookup"><span data-stu-id="65aec-240">Route values: [operation, track], [id, -3]</span></span>  |
| <span data-ttu-id="65aec-241">/package/track/</span><span class="sxs-lookup"><span data-stu-id="65aec-241">/package/track/</span></span> | <span data-ttu-id="65aec-242">\<贯穿，无任何匹配></span><span class="sxs-lookup"><span data-stu-id="65aec-242">\<Fall through, no match></span></span> |
| <span data-ttu-id="65aec-243">GET /hello/Joe</span><span class="sxs-lookup"><span data-stu-id="65aec-243">GET /hello/Joe</span></span> | <span data-ttu-id="65aec-244">Hi, Joe!</span><span class="sxs-lookup"><span data-stu-id="65aec-244">Hi, Joe!</span></span> |
| <span data-ttu-id="65aec-245">POST /hello/Joe</span><span class="sxs-lookup"><span data-stu-id="65aec-245">POST /hello/Joe</span></span> | <span data-ttu-id="65aec-246">\<贯穿，仅匹配 HTTP GET></span><span class="sxs-lookup"><span data-stu-id="65aec-246">\<Fall through, matches HTTP GET only></span></span> |
| <span data-ttu-id="65aec-247">GET /hello/Joe/Smith</span><span class="sxs-lookup"><span data-stu-id="65aec-247">GET /hello/Joe/Smith</span></span> | <span data-ttu-id="65aec-248">\<贯穿，无任何匹配></span><span class="sxs-lookup"><span data-stu-id="65aec-248">\<Fall through, no match></span></span> |

<span data-ttu-id="65aec-249">如果要配置单个路由，请在 `IRouter` 实例中调用 `app.UseRouter` 传入。</span><span class="sxs-lookup"><span data-stu-id="65aec-249">If you are configuring a single route, call `app.UseRouter` passing in an `IRouter` instance.</span></span> <span data-ttu-id="65aec-250">无需调用 `RouteBuilder`。</span><span class="sxs-lookup"><span data-stu-id="65aec-250">You won't need to call `RouteBuilder`.</span></span>

<span data-ttu-id="65aec-251">框架可提供一组扩展方法，用于创建如下路由：</span><span class="sxs-lookup"><span data-stu-id="65aec-251">The framework provides a set of extension methods for creating routes such as:</span></span>

* `MapRoute`
* `MapGet`
* `MapPost`
* `MapPut`
* `MapDelete`
* `MapVerb`

<span data-ttu-id="65aec-252">某些方法（如 `MapGet`）需要提供 `RequestDelegate`。</span><span class="sxs-lookup"><span data-stu-id="65aec-252">Some of these methods such as `MapGet` require a `RequestDelegate` to be provided.</span></span> <span data-ttu-id="65aec-253">路由匹配时，`RequestDelegate` 将用作路由处理程序。</span><span class="sxs-lookup"><span data-stu-id="65aec-253">The `RequestDelegate` will be used as the *route handler* when the route matches.</span></span> <span data-ttu-id="65aec-254">此系列中的其他方法允许配置中间件管道，它将被用作路由处理程序。</span><span class="sxs-lookup"><span data-stu-id="65aec-254">Other methods in this family allow configuring a middleware pipeline which will be used as the route handler.</span></span> <span data-ttu-id="65aec-255">如果 Map 方法不接受处理程序（如 `MapRoute`），则它将使用 `DefaultHandler`。</span><span class="sxs-lookup"><span data-stu-id="65aec-255">If the *Map* method doesn't accept a handler, such as `MapRoute`, then it will use the `DefaultHandler`.</span></span>

<span data-ttu-id="65aec-256">`Map[Verb]` 方法将使用约束来将路由限制为方法名称中的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="65aec-256">The `Map[Verb]` methods use constraints to limit the route to the HTTP Verb in the method name.</span></span> <span data-ttu-id="65aec-257">有关示例，请参阅 [MapGet](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/RequestDelegateRouteBuilderExtensions.cs#L85-L88) 和 [MapVerb](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/RequestDelegateRouteBuilderExtensions.cs#L156-L180)。</span><span class="sxs-lookup"><span data-stu-id="65aec-257">For example, see [MapGet](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/RequestDelegateRouteBuilderExtensions.cs#L85-L88) and [MapVerb](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/RequestDelegateRouteBuilderExtensions.cs#L156-L180).</span></span>

## <a name="route-template-reference"></a><span data-ttu-id="65aec-258">路由模板参考</span><span class="sxs-lookup"><span data-stu-id="65aec-258">Route Template Reference</span></span>

<span data-ttu-id="65aec-259">如果路由找到匹配项，大括号 (`{ }`) 内的令牌定义将绑定的路由参数。</span><span class="sxs-lookup"><span data-stu-id="65aec-259">Tokens within curly braces (`{ }`) define *route parameters* which will be bound if the route is matched.</span></span> <span data-ttu-id="65aec-260">可在路由段中定义多个路由参数，但必须由文本值隔开。</span><span class="sxs-lookup"><span data-stu-id="65aec-260">You can define more than one route parameter in a route segment, but they must be separated by a literal value.</span></span> <span data-ttu-id="65aec-261">例如，`{controller=Home}{action=Index}` 不是有效的路由，因为 `{controller}` 和 `{action}` 之间没有文本值。</span><span class="sxs-lookup"><span data-stu-id="65aec-261">For example `{controller=Home}{action=Index}` wouldn't be a valid route, since there's no literal value between `{controller}` and `{action}`.</span></span> <span data-ttu-id="65aec-262">这些路由参数必须具有名称，且可能指定了其他属性。</span><span class="sxs-lookup"><span data-stu-id="65aec-262">These route parameters must have a name, and may have additional attributes specified.</span></span>

<span data-ttu-id="65aec-263">路由参数以外的文本（例如 `{id}`）和路径分隔符 `/` 必须匹配 URL 中的文本。</span><span class="sxs-lookup"><span data-stu-id="65aec-263">Literal text other than route parameters (for example, `{id}`) and the path separator `/` must match the text in the URL.</span></span> <span data-ttu-id="65aec-264">文本匹配区分大小写，并且基于 URL 路径已解码的表示形式。</span><span class="sxs-lookup"><span data-stu-id="65aec-264">Text matching is case-insensitive and based on the decoded representation of the URLs path.</span></span> <span data-ttu-id="65aec-265">若要匹配文本路由参数分隔符 `{` 或 `}`，可通过重复该字符（`{{` 或 `}}`）对其进行转义。</span><span class="sxs-lookup"><span data-stu-id="65aec-265">To match the literal route parameter delimiter `{` or  `}`, escape it by repeating the character (`{{` or `}}`).</span></span>

<span data-ttu-id="65aec-266">尝试捕获具有可选文件扩展名的文件名的 URL 模式还有其他注意事项。</span><span class="sxs-lookup"><span data-stu-id="65aec-266">URL patterns that attempt to capture a filename with an optional file extension have additional considerations.</span></span> <span data-ttu-id="65aec-267">例如，使用模板 `files/{filename}.{ext?}`，如果 `filename` 和 `ext` 同时存在，将同时填充这两个值。</span><span class="sxs-lookup"><span data-stu-id="65aec-267">For example, using the template `files/{filename}.{ext?}` - When both `filename` and `ext` exist, both values will be populated.</span></span> <span data-ttu-id="65aec-268">如果 URL 中仅存在 `filename`，则路由匹配，因为尾随句点 `.` 是可选的。</span><span class="sxs-lookup"><span data-stu-id="65aec-268">If only `filename` exists in the URL, the route matches because the trailing period `.` is  optional.</span></span> <span data-ttu-id="65aec-269">以下 URL 与此路由相匹配：</span><span class="sxs-lookup"><span data-stu-id="65aec-269">The following URLs would match this route:</span></span>

* `/files/myFile.txt`
* `/files/myFile.`
* `/files/myFile`

<span data-ttu-id="65aec-270">你可以使用 `*` 字符作为路由参数的前缀，以绑定到 URI 的其余部分，这称之为调用全方位参数。</span><span class="sxs-lookup"><span data-stu-id="65aec-270">You can use the `*` character as a prefix to a route parameter to bind to the rest of the URI - this is called a *catch-all* parameter.</span></span> <span data-ttu-id="65aec-271">例如，`blog/{*slug}` 将匹配以 `/blog` 开头且其后带有任何值（将分配给 `slug` 路由值）的 URI。</span><span class="sxs-lookup"><span data-stu-id="65aec-271">For example, `blog/{*slug}` would match any URI that started with `/blog` and had any value following it (which would be assigned to the `slug` route value).</span></span> <span data-ttu-id="65aec-272">全方位参数还可以匹配空字符串。</span><span class="sxs-lookup"><span data-stu-id="65aec-272">Catch-all parameters can also match the empty string.</span></span>

<span data-ttu-id="65aec-273">路由参数可能具有指定的默认值，方法是在参数名称后使用 `=` 隔开以指定默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-273">Route parameters may have *default values*, designated by specifying the default after the parameter name, separated by an `=`.</span></span> <span data-ttu-id="65aec-274">例如，`{controller=Home}` 将 `Home` 定义为 `controller` 的默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-274">For example, `{controller=Home}` would define `Home` as the default value for `controller`.</span></span> <span data-ttu-id="65aec-275">如果参数的 URL 中不存在任何值，则使用默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-275">The default value is used if no value is present in the URL for the parameter.</span></span> <span data-ttu-id="65aec-276">除默认值外，路由参数可能是可选的（如 `id?` 中所示，通过将 `?` 追加到参数名称末尾）。</span><span class="sxs-lookup"><span data-stu-id="65aec-276">In addition to default values, route parameters may be optional (specified by appending a `?` to the end of the parameter name, as in `id?`).</span></span> <span data-ttu-id="65aec-277">可选和“具有默认值”的区别在于具有默认值的路由参数始终会生成一个值，而可选参数仅当提供值时才会具有一个值。</span><span class="sxs-lookup"><span data-stu-id="65aec-277">The difference between optional and "has default" is that a route parameter with a default value always produces a value; an optional parameter has a value only when one is provided.</span></span>

<span data-ttu-id="65aec-278">路由参数也可能具有约束，必须匹配从 URL 中绑定的路由值。</span><span class="sxs-lookup"><span data-stu-id="65aec-278">Route parameters may also have constraints, which must match the route value bound from the URL.</span></span> <span data-ttu-id="65aec-279">在路由参数后面添加一个冒号 `:` 和约束名称可指定路由参数上的内联约束。</span><span class="sxs-lookup"><span data-stu-id="65aec-279">Adding a colon `:` and constraint name after the route parameter name specifies an *inline constraint* on a route parameter.</span></span> <span data-ttu-id="65aec-280">如果约束需要参数，将以在约束名称后括在括号中的形式 (`( )`) 提供。</span><span class="sxs-lookup"><span data-stu-id="65aec-280">If the constraint requires arguments those are provided enclosed in parentheses `( )` after the constraint name.</span></span> <span data-ttu-id="65aec-281">通过追加另一个冒号 `:` 和约束名称，可指定多个内联约束。</span><span class="sxs-lookup"><span data-stu-id="65aec-281">Multiple inline constraints can be specified by appending another colon `:` and constraint name.</span></span> <span data-ttu-id="65aec-282">约束名称将传递给 `IInlineConstraintResolver` 服务，以创建 `IRouteConstraint` 的实例，用于处理 URL。</span><span class="sxs-lookup"><span data-stu-id="65aec-282">The constraint name is passed to the `IInlineConstraintResolver` service to create an instance of `IRouteConstraint` to use in URL processing.</span></span> <span data-ttu-id="65aec-283">例如，路由模板 `blog/{article:minlength(10)}` 使用参数 `10` 指定 `minlength` 约束。</span><span class="sxs-lookup"><span data-stu-id="65aec-283">For example, the route template `blog/{article:minlength(10)}` specifies the `minlength` constraint with the argument `10`.</span></span> <span data-ttu-id="65aec-284">有关路由约束的详细说明以及框架提供的约束列表，请参阅 [route-constraint-reference](#route-constraint-reference)。</span><span class="sxs-lookup"><span data-stu-id="65aec-284">For more description route constraints, and a listing of the constraints provided by the framework, see [route-constraint-reference](#route-constraint-reference).</span></span>

<span data-ttu-id="65aec-285">下表演示某些路由模板及其行为。</span><span class="sxs-lookup"><span data-stu-id="65aec-285">The following table demonstrates some route templates and their behavior.</span></span>

| <span data-ttu-id="65aec-286">路由模板</span><span class="sxs-lookup"><span data-stu-id="65aec-286">Route Template</span></span> | <span data-ttu-id="65aec-287">匹配 URL 示例</span><span class="sxs-lookup"><span data-stu-id="65aec-287">Example Matching URL</span></span> | <span data-ttu-id="65aec-288">说明</span><span class="sxs-lookup"><span data-stu-id="65aec-288">Notes</span></span> |
| -------- | -------- | ------- |
| <span data-ttu-id="65aec-289">hello</span><span class="sxs-lookup"><span data-stu-id="65aec-289">hello</span></span>  | <span data-ttu-id="65aec-290">/hello</span><span class="sxs-lookup"><span data-stu-id="65aec-290">/hello</span></span>  | <span data-ttu-id="65aec-291">仅匹配单个路径 `/hello`</span><span class="sxs-lookup"><span data-stu-id="65aec-291">Only matches the single path `/hello`</span></span> |
| <span data-ttu-id="65aec-292">{Page=Home}</span><span class="sxs-lookup"><span data-stu-id="65aec-292">{Page=Home}</span></span> | / | <span data-ttu-id="65aec-293">匹配并将 `Page` 设置为 `Home`</span><span class="sxs-lookup"><span data-stu-id="65aec-293">Matches and sets `Page` to `Home`</span></span> |
| <span data-ttu-id="65aec-294">{Page=Home}</span><span class="sxs-lookup"><span data-stu-id="65aec-294">{Page=Home}</span></span>  | <span data-ttu-id="65aec-295">/Contact</span><span class="sxs-lookup"><span data-stu-id="65aec-295">/Contact</span></span>  | <span data-ttu-id="65aec-296">匹配并将 `Page` 设置为 `Contact`</span><span class="sxs-lookup"><span data-stu-id="65aec-296">Matches and sets `Page` to `Contact`</span></span> |
| <span data-ttu-id="65aec-297">{controller}/{action}/{id?}</span><span class="sxs-lookup"><span data-stu-id="65aec-297">{controller}/{action}/{id?}</span></span> | <span data-ttu-id="65aec-298">/Products/List</span><span class="sxs-lookup"><span data-stu-id="65aec-298">/Products/List</span></span> | <span data-ttu-id="65aec-299">映射到 `Products` 控制器和 `List` 操作</span><span class="sxs-lookup"><span data-stu-id="65aec-299">Maps to `Products` controller and `List`  action</span></span> |
| <span data-ttu-id="65aec-300">{controller}/{action}/{id?}</span><span class="sxs-lookup"><span data-stu-id="65aec-300">{controller}/{action}/{id?}</span></span> | <span data-ttu-id="65aec-301">/Products/Details/123</span><span class="sxs-lookup"><span data-stu-id="65aec-301">/Products/Details/123</span></span>  |  <span data-ttu-id="65aec-302">映射到 `Products` 控制器和 `Details` 操作。</span><span class="sxs-lookup"><span data-stu-id="65aec-302">Maps to `Products` controller and  `Details` action.</span></span>  <span data-ttu-id="65aec-303">将 `id` 设置为 123</span><span class="sxs-lookup"><span data-stu-id="65aec-303">`id` set to 123</span></span> |
| <span data-ttu-id="65aec-304">{controller=Home}/{action=Index}/{id?}</span><span class="sxs-lookup"><span data-stu-id="65aec-304">{controller=Home}/{action=Index}/{id?}</span></span> | /  |  <span data-ttu-id="65aec-305">映射到 `Home` 控制器和 `Index` 方法；将忽略 `id`。</span><span class="sxs-lookup"><span data-stu-id="65aec-305">Maps to `Home` controller and `Index`  method; `id` is ignored.</span></span> |

<span data-ttu-id="65aec-306">使用模板通常是进行路由最简单的方法。</span><span class="sxs-lookup"><span data-stu-id="65aec-306">Using a template is generally the simplest approach to routing.</span></span> <span data-ttu-id="65aec-307">还可在路由模板外指定约束和默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-307">Constraints and defaults can also be specified outside the route template.</span></span>

<span data-ttu-id="65aec-308">提示：启用[日志记录](xref:fundamentals/logging/index)查看内置路由实现（如 `Route`）如何匹配请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-308">Tip: Enable [Logging](xref:fundamentals/logging/index) to see how the built in routing implementations, such as `Route`, match requests.</span></span>

## <a name="route-constraint-reference"></a><span data-ttu-id="65aec-309">路由约束参考</span><span class="sxs-lookup"><span data-stu-id="65aec-309">Route Constraint Reference</span></span>

<span data-ttu-id="65aec-310">如果 `Route` 匹配传入 URL 的语法并将 URL 路径标记化为路由值，将执行路由约束。</span><span class="sxs-lookup"><span data-stu-id="65aec-310">Route constraints execute when a `Route` has matched the syntax of the incoming URL and tokenized the URL path into route values.</span></span> <span data-ttu-id="65aec-311">通常情况下，路由约束检查通过路由模板关联的路由值，并对该值是否可接受作出简单的是/否决策。</span><span class="sxs-lookup"><span data-stu-id="65aec-311">Route constraints generally inspect the route value associated via the route template and make a simple yes/no decision about whether or not the value is acceptable.</span></span> <span data-ttu-id="65aec-312">某些路由约束使用路由值以外的数据来考虑是否可以路由请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-312">Some route constraints use data outside the route value to consider whether the request can be routed.</span></span> <span data-ttu-id="65aec-313">例如，`HttpMethodRouteConstraint` 可以根据其 HTTP 谓词接受或拒绝请求。</span><span class="sxs-lookup"><span data-stu-id="65aec-313">For example, the `HttpMethodRouteConstraint` can accept or reject a request based on its HTTP verb.</span></span>

>[!WARNING]
> <span data-ttu-id="65aec-314">避免使用输入验证约束，因为这样意味着无效输入将导致 404 错误（未找到），而不是含相应错误消息的 400 错误。</span><span class="sxs-lookup"><span data-stu-id="65aec-314">Avoid using constraints for **input validation**, because doing so means that invalid input will result in a 404 (Not Found) instead of a 400 with an appropriate error message.</span></span> <span data-ttu-id="65aec-315">路由约束应用来消除类似路由间的歧义，而不是验证特定路由的输入。</span><span class="sxs-lookup"><span data-stu-id="65aec-315">Route constraints should be used to **disambiguate** between similar routes, not to validate the inputs for a particular route.</span></span>

<span data-ttu-id="65aec-316">下表演示某些路由约束及其预期行为。</span><span class="sxs-lookup"><span data-stu-id="65aec-316">The following table demonstrates some route constraints and their expected behavior.</span></span>

| <span data-ttu-id="65aec-317">约束</span><span class="sxs-lookup"><span data-stu-id="65aec-317">constraint</span></span> | <span data-ttu-id="65aec-318">示例</span><span class="sxs-lookup"><span data-stu-id="65aec-318">Example</span></span> | <span data-ttu-id="65aec-319">匹配项示例</span><span class="sxs-lookup"><span data-stu-id="65aec-319">Example Matches</span></span> | <span data-ttu-id="65aec-320">说明</span><span class="sxs-lookup"><span data-stu-id="65aec-320">Notes</span></span> |
| --------   | ------- | ------------- | ----- |
| `int` | `{id:int}` | <span data-ttu-id="65aec-321">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="65aec-321">`123456789`, `-123456789`</span></span>  | <span data-ttu-id="65aec-322">匹配任何整数</span><span class="sxs-lookup"><span data-stu-id="65aec-322">Matches any integer</span></span> |
| `bool`  | `{active:bool}` | <span data-ttu-id="65aec-323">`true`, `FALSE`</span><span class="sxs-lookup"><span data-stu-id="65aec-323">`true`, `FALSE`</span></span> | <span data-ttu-id="65aec-324">匹配 `true`或 `false`（区分大小写）</span><span class="sxs-lookup"><span data-stu-id="65aec-324">Matches `true` or `false` (case-insensitive)</span></span> |
| `datetime` | `{dob:datetime}` | <span data-ttu-id="65aec-325">`2016-12-31`, `2016-12-31 7:32pm`</span><span class="sxs-lookup"><span data-stu-id="65aec-325">`2016-12-31`, `2016-12-31 7:32pm`</span></span>  | <span data-ttu-id="65aec-326">匹配有效的 `DateTime` 值（位于固定区域性中 - 查看警告）</span><span class="sxs-lookup"><span data-stu-id="65aec-326">Matches a valid `DateTime` value (in the invariant culture - see warning)</span></span> |
| `decimal` | `{price:decimal}` | <span data-ttu-id="65aec-327">`49.99`, `-1,000.01`</span><span class="sxs-lookup"><span data-stu-id="65aec-327">`49.99`, `-1,000.01`</span></span> | <span data-ttu-id="65aec-328">匹配有效的 `decimal` 值（位于固定区域性中 - 查看警告）</span><span class="sxs-lookup"><span data-stu-id="65aec-328">Matches a valid `decimal` value (in the invariant culture - see warning)</span></span> |
| `double`  | `{weight:double}` | <span data-ttu-id="65aec-329">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="65aec-329">`1.234`, `-1,001.01e8`</span></span> | <span data-ttu-id="65aec-330">匹配有效的 `double` 值（位于固定区域性中 - 查看警告）</span><span class="sxs-lookup"><span data-stu-id="65aec-330">Matches a valid `double` value (in the invariant culture - see warning)</span></span> |
| `float`  | `{weight:float}` | <span data-ttu-id="65aec-331">`1.234`, `-1,001.01e8`</span><span class="sxs-lookup"><span data-stu-id="65aec-331">`1.234`, `-1,001.01e8`</span></span> | <span data-ttu-id="65aec-332">匹配有效的 `float` 值（位于固定区域性中 - 查看警告）</span><span class="sxs-lookup"><span data-stu-id="65aec-332">Matches a valid `float` value (in the invariant culture - see warning)</span></span> |
| `guid`  | `{id:guid}` | <span data-ttu-id="65aec-333">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span><span class="sxs-lookup"><span data-stu-id="65aec-333">`CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}`</span></span> | <span data-ttu-id="65aec-334">匹配有效的 `Guid` 值</span><span class="sxs-lookup"><span data-stu-id="65aec-334">Matches a valid `Guid` value</span></span> |
| `long` | `{ticks:long}` | <span data-ttu-id="65aec-335">`123456789`, `-123456789`</span><span class="sxs-lookup"><span data-stu-id="65aec-335">`123456789`, `-123456789`</span></span> | <span data-ttu-id="65aec-336">匹配有效的 `long` 值</span><span class="sxs-lookup"><span data-stu-id="65aec-336">Matches a valid `long` value</span></span> |
| `minlength(value)` | `{username:minlength(4)}` | `Rick` | <span data-ttu-id="65aec-337">字符串必须至少为 4 个字符</span><span class="sxs-lookup"><span data-stu-id="65aec-337">String must be at least 4 characters</span></span> |
| `maxlength(value)` | `{filename:maxlength(8)}` | `Richard` | <span data-ttu-id="65aec-338">字符串不得超过 8 个字符</span><span class="sxs-lookup"><span data-stu-id="65aec-338">String must be no more than 8 characters</span></span> |
| `length(length)` | `{filename:length(12)}` | `somefile.txt` | <span data-ttu-id="65aec-339">字符串必须正好为 12 个字符</span><span class="sxs-lookup"><span data-stu-id="65aec-339">String must be exactly 12 characters long</span></span> |
| `length(min,max)` | `{filename:length(8,16)}` | `somefile.txt` | <span data-ttu-id="65aec-340">字符串必须至少为 8 个字符，且不得超过 16 个字符</span><span class="sxs-lookup"><span data-stu-id="65aec-340">String must be at least 8 and no more than 16 characters long</span></span> |
| `min(value)` | `{age:min(18)}` | `19` | <span data-ttu-id="65aec-341">整数值必须至少为 18</span><span class="sxs-lookup"><span data-stu-id="65aec-341">Integer value must be at least 18</span></span> |
| `max(value)` | `{age:max(120)}` |  `91` | <span data-ttu-id="65aec-342">整数值不得超过 120</span><span class="sxs-lookup"><span data-stu-id="65aec-342">Integer value must be no more than 120</span></span> |
| `range(min,max)` | `{age:range(18,120)}` | `91` | <span data-ttu-id="65aec-343">整数值必须至少为 18，且不得超过 120</span><span class="sxs-lookup"><span data-stu-id="65aec-343">Integer value must be at least 18 but no more than 120</span></span> |
| `alpha` | `{name:alpha}` | `Rick` | <span data-ttu-id="65aec-344">字符串必须由一个或多个字母字符（`a`-`z`，区分大小写）组成</span><span class="sxs-lookup"><span data-stu-id="65aec-344">String must consist of one or more alphabetical characters (`a`-`z`, case-insensitive)</span></span> |
| `regex(expression)` | `{ssn:regex(^\\d{{3}}-\\d{{2}}-\\d{{4}}$)}` | `123-45-6789` | <span data-ttu-id="65aec-345">字符串必须匹配正则表达式（参见有关定义正则表达式的提示）</span><span class="sxs-lookup"><span data-stu-id="65aec-345">String must match the regular expression (see tips about defining a regular expression)</span></span> |
| `required`  | `{name:required}` | `Rick` |  <span data-ttu-id="65aec-346">用于强制在 URL 生成过程中存在非参数值</span><span class="sxs-lookup"><span data-stu-id="65aec-346">Used to enforce that a non-parameter value is present during URL generation</span></span> |

>[!WARNING]
> <span data-ttu-id="65aec-347">验证 URL 的路由约束可以转换为始终使用固定区域性的 CLR 类型（例如 `int` 或 `DateTime`），它们假定 URL 不可本地化。</span><span class="sxs-lookup"><span data-stu-id="65aec-347">Route constraints that verify the URL can be converted to a CLR type (such as `int` or `DateTime`) always use the invariant culture - they assume the URL is non-localizable.</span></span> <span data-ttu-id="65aec-348">框架提供的路由约束不会修改存储于路由值中的值。</span><span class="sxs-lookup"><span data-stu-id="65aec-348">The framework-provided route constraints don't modify the values stored in route values.</span></span> <span data-ttu-id="65aec-349">从 URL 中分析的所有路由值都将作为字符串进行存储。</span><span class="sxs-lookup"><span data-stu-id="65aec-349">All route values parsed from the URL will be stored as strings.</span></span> <span data-ttu-id="65aec-350">例如，[浮点数路由约束](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/Constraints/FloatRouteConstraint.cs#L44-L60)会尝试将路由值转换为浮点数，但转换后的值仅用来验证其是否可转换为浮点数。</span><span class="sxs-lookup"><span data-stu-id="65aec-350">For example, the [Float route constraint](https://github.com/aspnet/Routing/blob/1.0.0/src/Microsoft.AspNetCore.Routing/Constraints/FloatRouteConstraint.cs#L44-L60) will attempt to convert the route value to a float, but the converted value is used only to verify it can be converted to a float.</span></span>

## <a name="regular-expressions"></a><span data-ttu-id="65aec-351">正则表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-351">Regular expressions</span></span> 

<span data-ttu-id="65aec-352">ASP.NET Core 框架将向正则表达式构造函数添加 `RegexOptions.IgnoreCase | RegexOptions.Compiled | RegexOptions.CultureInvariant`。</span><span class="sxs-lookup"><span data-stu-id="65aec-352">The ASP.NET Core framework adds `RegexOptions.IgnoreCase | RegexOptions.Compiled | RegexOptions.CultureInvariant` to the regular expression constructor.</span></span> <span data-ttu-id="65aec-353">有关这些成员的介绍，请参阅 [RegexOptions 枚举](/dotnet/api/system.text.regularexpressions.regexoptions)。</span><span class="sxs-lookup"><span data-stu-id="65aec-353">See [RegexOptions Enumeration](/dotnet/api/system.text.regularexpressions.regexoptions) for a description of these members.</span></span>

<span data-ttu-id="65aec-354">正则表达式与路由和 C# 计算机语言使用的分隔符和令牌相似。</span><span class="sxs-lookup"><span data-stu-id="65aec-354">Regular expressions use delimiters and tokens similar to those used by Routing and the C# language.</span></span> <span data-ttu-id="65aec-355">必须对正则表达式令牌进行转义。</span><span class="sxs-lookup"><span data-stu-id="65aec-355">Regular expression tokens must be escaped.</span></span> <span data-ttu-id="65aec-356">例如，要在路由中使用正则表达式 `^\d{3}-\d{2}-\d{4}$`，需要如 C# 源文件中键入的 `\\` 一样的 `\` 字符，以转义 `\` 字符串转义字符（除非使用 [verbatim 字符串文本](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/string)）。</span><span class="sxs-lookup"><span data-stu-id="65aec-356">For example, to use the regular expression `^\d{3}-\d{2}-\d{4}$` in Routing, it needs to have the `\` characters typed in as `\\` in the C# source file to escape the `\` string escape character (unless using [verbatim string literals](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/string).</span></span> <span data-ttu-id="65aec-357">`{`、`}`、“[”和“]”字符需要成双进行转义，以转义路由参数分隔符字符。</span><span class="sxs-lookup"><span data-stu-id="65aec-357">The `{` , `}` , '[' and ']' characters need to be escaped by doubling them to escape the Routing parameter delimiter characters.</span></span>  <span data-ttu-id="65aec-358">下表显示正则表达式和转义的版本。</span><span class="sxs-lookup"><span data-stu-id="65aec-358">The table below shows a regular expression and the escaped version.</span></span>

| <span data-ttu-id="65aec-359">表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-359">Expression</span></span>               | <span data-ttu-id="65aec-360">说明</span><span class="sxs-lookup"><span data-stu-id="65aec-360">Note</span></span> |
| ----------------- | ------------ | 
| `^\d{3}-\d{2}-\d{4}$` | <span data-ttu-id="65aec-361">正则表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-361">Regular expression</span></span> |
| `^\\d{{3}}-\\d{{2}}-\\d{{4}}$` | <span data-ttu-id="65aec-362">已转义</span><span class="sxs-lookup"><span data-stu-id="65aec-362">Escaped</span></span>  |
| `^[a-z]{2}$` | <span data-ttu-id="65aec-363">正则表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-363">Regular expression</span></span> |
| `^[[a-z]]{{2}}$` | <span data-ttu-id="65aec-364">已转义</span><span class="sxs-lookup"><span data-stu-id="65aec-364">Escaped</span></span>  |

<span data-ttu-id="65aec-365">路由中使用的正则表达式通常以 `^` 字符（匹配字符串的起始位置）开头，以 `$` 字符（匹配字符串的结束位置）结尾。</span><span class="sxs-lookup"><span data-stu-id="65aec-365">Regular expressions used in routing will often start with the `^` character (match starting position of the string) and end with the `$` character (match ending position of the string).</span></span> <span data-ttu-id="65aec-366">`^` 和 `$` 字符可确保正则表达式匹配整个路由参数值。</span><span class="sxs-lookup"><span data-stu-id="65aec-366">The `^` and `$` characters ensure that the regular expression match the entire route parameter value.</span></span> <span data-ttu-id="65aec-367">如果没有 `^` 和 `$` 字符，正则表达式将匹配字符串内的所有子字符串，这些字符串通常不是你想要的。</span><span class="sxs-lookup"><span data-stu-id="65aec-367">Without the `^` and `$` characters the regular expression will match any sub-string within the string, which is often not what you want.</span></span> <span data-ttu-id="65aec-368">下表显示部分示例，并说明它们为何匹配或未能匹配。</span><span class="sxs-lookup"><span data-stu-id="65aec-368">The table below shows some examples and explains why they match or fail to match.</span></span>

| <span data-ttu-id="65aec-369">表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-369">Expression</span></span>               | <span data-ttu-id="65aec-370">String</span><span class="sxs-lookup"><span data-stu-id="65aec-370">String</span></span> | <span data-ttu-id="65aec-371">匹配</span><span class="sxs-lookup"><span data-stu-id="65aec-371">Match</span></span> | <span data-ttu-id="65aec-372">注释</span><span class="sxs-lookup"><span data-stu-id="65aec-372">Comment</span></span> |
| ----------------- | ------------ |  ------------ |  ------------ | 
| `[a-z]{2}` | <span data-ttu-id="65aec-373">hello</span><span class="sxs-lookup"><span data-stu-id="65aec-373">hello</span></span> | <span data-ttu-id="65aec-374">是</span><span class="sxs-lookup"><span data-stu-id="65aec-374">yes</span></span> | <span data-ttu-id="65aec-375">子字符串匹配</span><span class="sxs-lookup"><span data-stu-id="65aec-375">substring matches</span></span> |
| `[a-z]{2}` | <span data-ttu-id="65aec-376">123abc456</span><span class="sxs-lookup"><span data-stu-id="65aec-376">123abc456</span></span> | <span data-ttu-id="65aec-377">是</span><span class="sxs-lookup"><span data-stu-id="65aec-377">yes</span></span> | <span data-ttu-id="65aec-378">子字符串匹配</span><span class="sxs-lookup"><span data-stu-id="65aec-378">substring matches</span></span> |
| `[a-z]{2}` | <span data-ttu-id="65aec-379">mz</span><span class="sxs-lookup"><span data-stu-id="65aec-379">mz</span></span> | <span data-ttu-id="65aec-380">是</span><span class="sxs-lookup"><span data-stu-id="65aec-380">yes</span></span> | <span data-ttu-id="65aec-381">匹配表达式</span><span class="sxs-lookup"><span data-stu-id="65aec-381">matches expression</span></span> |
| `[a-z]{2}` | <span data-ttu-id="65aec-382">MZ</span><span class="sxs-lookup"><span data-stu-id="65aec-382">MZ</span></span> | <span data-ttu-id="65aec-383">是</span><span class="sxs-lookup"><span data-stu-id="65aec-383">yes</span></span> | <span data-ttu-id="65aec-384">不区分大小写</span><span class="sxs-lookup"><span data-stu-id="65aec-384">not case sensitive</span></span> |
| `^[a-z]{2}$` |  <span data-ttu-id="65aec-385">hello</span><span class="sxs-lookup"><span data-stu-id="65aec-385">hello</span></span> | <span data-ttu-id="65aec-386">否</span><span class="sxs-lookup"><span data-stu-id="65aec-386">no</span></span> | <span data-ttu-id="65aec-387">参阅上述 `^` 和 `$`</span><span class="sxs-lookup"><span data-stu-id="65aec-387">see `^` and `$` above</span></span> |
| `^[a-z]{2}$` |  <span data-ttu-id="65aec-388">123abc456</span><span class="sxs-lookup"><span data-stu-id="65aec-388">123abc456</span></span> | <span data-ttu-id="65aec-389">否</span><span class="sxs-lookup"><span data-stu-id="65aec-389">no</span></span> | <span data-ttu-id="65aec-390">参阅上述 `^` 和 `$`</span><span class="sxs-lookup"><span data-stu-id="65aec-390">see `^` and `$` above</span></span> |

<span data-ttu-id="65aec-391">有关正则表达式语法的详细信息，请参阅 [.NET Framework 正则表达式](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference)。</span><span class="sxs-lookup"><span data-stu-id="65aec-391">Refer to [.NET Framework Regular Expressions](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference) for more information on regular expression syntax.</span></span>

<span data-ttu-id="65aec-392">若要将参数限制为一组已知的可能值，可使用正则表达式。</span><span class="sxs-lookup"><span data-stu-id="65aec-392">To constrain a parameter to a known set of possible values, use a regular expression.</span></span> <span data-ttu-id="65aec-393">例如，`{action:regex(^(list|get|create)$)}` 仅将 `action` 路由值匹配到 `list`、`get` 或 `create`。</span><span class="sxs-lookup"><span data-stu-id="65aec-393">For example `{action:regex(^(list|get|create)$)}` only matches the `action` route value to `list`, `get`, or `create`.</span></span> <span data-ttu-id="65aec-394">如果传递到约束字典中，字符串“^(list|get|create)$”将等效。</span><span class="sxs-lookup"><span data-stu-id="65aec-394">If passed into the constraints dictionary, the string "^(list|get|create)$" would be equivalent.</span></span> <span data-ttu-id="65aec-395">已传递到约束字典（不与模板内联）且不匹配任何已知约束的约束还将被视为正则表达式。</span><span class="sxs-lookup"><span data-stu-id="65aec-395">Constraints that are passed in the constraints dictionary (not inline within a template) that don't match one of the known constraints are also treated as regular expressions.</span></span>

## <a name="url-generation-reference"></a><span data-ttu-id="65aec-396">URL 生成参考</span><span class="sxs-lookup"><span data-stu-id="65aec-396">URL Generation Reference</span></span>

<span data-ttu-id="65aec-397">下面的示例演示如何在给定路由值字典和 `RouteCollection` 的情况下生成路由链接。</span><span class="sxs-lookup"><span data-stu-id="65aec-397">The example below shows how to generate a link to a route given a dictionary of route values and a `RouteCollection`.</span></span>

[!code-csharp[](../fundamentals/routing/sample/RoutingSample/Startup.cs?range=45-59)]

<span data-ttu-id="65aec-398">上述示例末尾生成的 `VirtualPath` 为 `/package/create/123`。</span><span class="sxs-lookup"><span data-stu-id="65aec-398">The `VirtualPath` generated at the end of the sample above is `/package/create/123`.</span></span>

<span data-ttu-id="65aec-399">`VirtualPathContext` 构造函数的第二个参数是环境值的集合。</span><span class="sxs-lookup"><span data-stu-id="65aec-399">The second parameter to the `VirtualPathContext` constructor is a collection of *ambient values*.</span></span> <span data-ttu-id="65aec-400">通过限制特定请求上下文中开发者必须指定的值数，环境值可提供便利。</span><span class="sxs-lookup"><span data-stu-id="65aec-400">Ambient values provide convenience by limiting the number of values a developer must specify within a certain request context.</span></span> <span data-ttu-id="65aec-401">当前请求的当前路由值被视为链接生成的环境值。</span><span class="sxs-lookup"><span data-stu-id="65aec-401">The current route values of the current request are considered ambient values for link generation.</span></span> <span data-ttu-id="65aec-402">例如，在 ASP.NET MVC 应用中，如果处于 `HomeController` 的 `About` 操作中，则无需指定控制器路由值即可链接到 `Index` 操作（将使用 `Home` 环境值）。</span><span class="sxs-lookup"><span data-stu-id="65aec-402">For example, in an ASP.NET MVC app if you are in the `About` action of the `HomeController`, you don't need to specify the controller route value to link to the `Index` action (the ambient value of `Home` will be used).</span></span>

<span data-ttu-id="65aec-403">URL 中从左至右，将忽略不匹配参数的环境值，如果显式提供的值替代环境值，该环境值也将被忽略。</span><span class="sxs-lookup"><span data-stu-id="65aec-403">Ambient values that don't match a parameter are ignored, and ambient values are also ignored when an explicitly-provided value overrides it, going from left to right in the URL.</span></span>

<span data-ttu-id="65aec-404">显式提供但不匹配任何对象的值将添加到查询字符串。</span><span class="sxs-lookup"><span data-stu-id="65aec-404">Values that are explicitly provided but which don't match anything are added to the query string.</span></span> <span data-ttu-id="65aec-405">下表显示使用路由模板 `{controller}/{action}/{id?}` 时的结果。</span><span class="sxs-lookup"><span data-stu-id="65aec-405">The following table shows the result when using the route template `{controller}/{action}/{id?}`.</span></span>

| <span data-ttu-id="65aec-406">环境值</span><span class="sxs-lookup"><span data-stu-id="65aec-406">Ambient Values</span></span> | <span data-ttu-id="65aec-407">显式值</span><span class="sxs-lookup"><span data-stu-id="65aec-407">Explicit Values</span></span> | <span data-ttu-id="65aec-408">结果</span><span class="sxs-lookup"><span data-stu-id="65aec-408">Result</span></span> |
| -------------   | -------------- | ------ |
| <span data-ttu-id="65aec-409">controller="Home"</span><span class="sxs-lookup"><span data-stu-id="65aec-409">controller="Home"</span></span> | <span data-ttu-id="65aec-410">action="About"</span><span class="sxs-lookup"><span data-stu-id="65aec-410">action="About"</span></span> | `/Home/About` |
| <span data-ttu-id="65aec-411">controller="Home"</span><span class="sxs-lookup"><span data-stu-id="65aec-411">controller="Home"</span></span> | <span data-ttu-id="65aec-412">controller="Order",action="About"</span><span class="sxs-lookup"><span data-stu-id="65aec-412">controller="Order",action="About"</span></span> | `/Order/About` |
| <span data-ttu-id="65aec-413">controller="Home",color="Red"</span><span class="sxs-lookup"><span data-stu-id="65aec-413">controller="Home",color="Red"</span></span> | <span data-ttu-id="65aec-414">action="About"</span><span class="sxs-lookup"><span data-stu-id="65aec-414">action="About"</span></span> | `/Home/About` |
| <span data-ttu-id="65aec-415">controller="Home"</span><span class="sxs-lookup"><span data-stu-id="65aec-415">controller="Home"</span></span> | <span data-ttu-id="65aec-416">action="About",color="Red"</span><span class="sxs-lookup"><span data-stu-id="65aec-416">action="About",color="Red"</span></span> | `/Home/About?color=Red`

<span data-ttu-id="65aec-417">如果路由具有不对应参数的默认值，且该值以显示方式提供，则它必须匹配默认值。</span><span class="sxs-lookup"><span data-stu-id="65aec-417">If a route has a default value that doesn't correspond to a parameter and that value is explicitly provided, it must match the default value.</span></span> <span data-ttu-id="65aec-418">例如:</span><span class="sxs-lookup"><span data-stu-id="65aec-418">For example:</span></span>

```csharp
routes.MapRoute("blog_route", "blog/{*slug}",
  defaults: new { controller = "Blog", action = "ReadPost" });
```

<span data-ttu-id="65aec-419">当提供控制器和操作的匹配值时，链接生成将只生成此路由的链接。</span><span class="sxs-lookup"><span data-stu-id="65aec-419">Link generation would only generate a link for this route when the matching values for controller and action are provided.</span></span>
