---
title: ASP.NET Core 中 Razor 页面的路由和应用约定
author: guardrex
description: 了解路由和应用模型提供程序约定如何帮助控制页面路由、发现和处理。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 10/12/2018
uid: razor-pages/razor-pages-conventions
ms.openlocfilehash: f04e0930966c9aaf38543729565b1ef4a80a09e2
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207688"
---
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a><span data-ttu-id="b6860-103">ASP.NET Core 中 Razor 页面的路由和应用约定</span><span class="sxs-lookup"><span data-stu-id="b6860-103">Razor Pages route and app conventions in ASP.NET Core</span></span>

<span data-ttu-id="b6860-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b6860-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b6860-105">了解如何使用[页面路由和应用模型提供程序约定](xref:mvc/controllers/application-model#conventions)来控制 Razor 页面应用中的页面路由、发现和处理。</span><span class="sxs-lookup"><span data-stu-id="b6860-105">Learn how to use page [route and app model provider conventions](xref:mvc/controllers/application-model#conventions) to control page routing, discovery, and processing in Razor Pages apps.</span></span>

<span data-ttu-id="b6860-106">需要为各个页面配置自定义页面路由时，可使用本主题稍后所述的 [AddPageRoute 约定](#configure-a-page-route)配置页面路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="b6860-107">若要指定页面路由、 添加路由段，或将参数添加到路由，请使用页面的`@page`指令。</span><span class="sxs-lookup"><span data-stu-id="b6860-107">To specify a page route, add route segments, or add parameters to a route, use the page's `@page` directive.</span></span> <span data-ttu-id="b6860-108">有关详细信息，请参阅[自定义路由](xref:razor-pages/index#custom-routes)。</span><span class="sxs-lookup"><span data-stu-id="b6860-108">For more information, see [Custom routes](xref:razor-pages/index#custom-routes).</span></span>

<span data-ttu-id="b6860-109">有不能用作路由段或参数名称的保留的字。</span><span class="sxs-lookup"><span data-stu-id="b6860-109">There are reserved words that can't be used as route segments or parameter names.</span></span> <span data-ttu-id="b6860-110">有关详细信息，请参阅[路由： 保留路由名称](xref:fundamentals/routing#reserved-routing-names)。</span><span class="sxs-lookup"><span data-stu-id="b6860-110">For more information, see [Routing: Reserved routing names](xref:fundamentals/routing#reserved-routing-names).</span></span>

<span data-ttu-id="b6860-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="b6860-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

::: moniker range="= aspnetcore-2.0"

| <span data-ttu-id="b6860-112">方案</span><span class="sxs-lookup"><span data-stu-id="b6860-112">Scenario</span></span> | <span data-ttu-id="b6860-113">示例演示...</span><span class="sxs-lookup"><span data-stu-id="b6860-113">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="b6860-114">模型约定</span><span class="sxs-lookup"><span data-stu-id="b6860-114">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="b6860-115">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="b6860-115">Conventions.Add</span></span><ul><li><span data-ttu-id="b6860-116">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-116">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-117">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-117">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="b6860-118">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-118">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="b6860-119">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-119">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="b6860-120">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-120">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-121">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-121">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-122">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="b6860-122">AddPageRoute</span></span></li></ul> | <span data-ttu-id="b6860-123">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-123">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="b6860-124">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-124">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="b6860-125">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-125">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="b6860-126">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-126">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="b6860-127">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="b6860-127">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="b6860-128">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-128">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="b6860-129">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="b6860-129">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="b6860-130">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-130">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

| <span data-ttu-id="b6860-131">方案</span><span class="sxs-lookup"><span data-stu-id="b6860-131">Scenario</span></span> | <span data-ttu-id="b6860-132">示例演示...</span><span class="sxs-lookup"><span data-stu-id="b6860-132">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="b6860-133">模型约定</span><span class="sxs-lookup"><span data-stu-id="b6860-133">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="b6860-134">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="b6860-134">Conventions.Add</span></span><ul><li><span data-ttu-id="b6860-135">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-135">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-136">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-136">IPageApplicationModelConvention</span></span></li><li><span data-ttu-id="b6860-137">IPageHandlerModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-137">IPageHandlerModelConvention</span></span></li></ul> | <span data-ttu-id="b6860-138">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-138">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="b6860-139">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-139">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="b6860-140">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-140">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-141">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-141">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="b6860-142">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="b6860-142">AddPageRoute</span></span></li></ul> | <span data-ttu-id="b6860-143">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-143">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="b6860-144">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-144">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="b6860-145">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-145">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="b6860-146">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="b6860-146">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="b6860-147">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="b6860-147">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="b6860-148">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-148">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="b6860-149">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="b6860-149">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="b6860-150">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-150">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

<span data-ttu-id="b6860-151">使用 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 扩展方法向 `Startup` 类中服务集合的 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) 添加和配置 Razor 页面约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-151">Razor Pages conventions are added and configured using the [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) extension method to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) on the service collection in the `Startup` class.</span></span> <span data-ttu-id="b6860-152">本主题稍后会介绍以下约定示例：</span><span class="sxs-lookup"><span data-stu-id="b6860-152">The following convention examples are explained later in this topic:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddRazorPagesOptions(options =>
            {
                options.Conventions.Add( ... );
                options.Conventions.AddFolderRouteModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageRouteModelConvention("/About", model => { ... });
                options.Conventions.AddPageRoute("/Contact", "TheContactPage/{text?}");
                options.Conventions.AddFolderApplicationModelConvention("/OtherPages", model => { ... });
                options.Conventions.AddPageApplicationModelConvention("/About", model => { ... });
                options.Conventions.ConfigureFilter(model => { ... });
                options.Conventions.ConfigureFilter( ... );
            });
}
```

## <a name="route-order"></a><span data-ttu-id="b6860-153">路由顺序</span><span class="sxs-lookup"><span data-stu-id="b6860-153">Route order</span></span>

<span data-ttu-id="b6860-154">路由指定<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*>用于处理 （路由匹配）。</span><span class="sxs-lookup"><span data-stu-id="b6860-154">Routes specify an <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> for processing (route matching).</span></span>

| <span data-ttu-id="b6860-155">顺序</span><span class="sxs-lookup"><span data-stu-id="b6860-155">Order</span></span>            | <span data-ttu-id="b6860-156">行为</span><span class="sxs-lookup"><span data-stu-id="b6860-156">Behavior</span></span> |
| :--------------: | -------- |
| <span data-ttu-id="b6860-157">-1</span><span class="sxs-lookup"><span data-stu-id="b6860-157">-1</span></span>               | <span data-ttu-id="b6860-158">处理其他路由之前处理该路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-158">The route is processed before other routes are processed.</span></span> |
| <span data-ttu-id="b6860-159">0</span><span class="sxs-lookup"><span data-stu-id="b6860-159">0</span></span>                | <span data-ttu-id="b6860-160">未指定顺序 （默认值）。</span><span class="sxs-lookup"><span data-stu-id="b6860-160">Order isn't specified (default value).</span></span> <span data-ttu-id="b6860-161">不分配`Order`(`Order = null`) 将默认路由`Order`为 0 （零） 进行处理。</span><span class="sxs-lookup"><span data-stu-id="b6860-161">Not assigning `Order` (`Order = null`) defaults the route `Order` to 0 (zero) for processing.</span></span> |
| <span data-ttu-id="b6860-162">1、 2、 &hellip; n</span><span class="sxs-lookup"><span data-stu-id="b6860-162">1, 2, &hellip; n</span></span> | <span data-ttu-id="b6860-163">指定路由处理顺序。</span><span class="sxs-lookup"><span data-stu-id="b6860-163">Specifies the route processing order.</span></span> |

<span data-ttu-id="b6860-164">按照约定来建立路由处理：</span><span class="sxs-lookup"><span data-stu-id="b6860-164">Route processing is established by convention:</span></span>

* <span data-ttu-id="b6860-165">按顺序处理的路由 (-1、 0、 1、 2、 &hellip; n)。</span><span class="sxs-lookup"><span data-stu-id="b6860-165">Routes are processed in sequential order (-1, 0, 1, 2, &hellip; n).</span></span>
* <span data-ttu-id="b6860-166">当路由具有相同`Order`、 最具体的路由匹配跟有更具体的路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-166">When routes have the same `Order`, the most specific route is matched first followed by less specific routes.</span></span>
* <span data-ttu-id="b6860-167">当具有相同的路由`Order`和相同数量的参数匹配请求 URL，将它们添加到顺序处理路由<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.PageConventionCollection>。</span><span class="sxs-lookup"><span data-stu-id="b6860-167">When routes with the same `Order` and the same number of parameters match a request URL, routes are processed in the order that they're added to the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.PageConventionCollection>.</span></span>

<span data-ttu-id="b6860-168">如果可能，避免具体取决于已建立的路由处理顺序。</span><span class="sxs-lookup"><span data-stu-id="b6860-168">If possible, avoid depending on an established route processing order.</span></span> <span data-ttu-id="b6860-169">通常情况下，路由选择与 URL 匹配的正确路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-169">Generally, routing selects the correct route with URL matching.</span></span> <span data-ttu-id="b6860-170">如果必须设置路由`Order`属性路由请求是否正确，应用程序的路由方案，可能令人困惑，向客户端和脆弱来维护。</span><span class="sxs-lookup"><span data-stu-id="b6860-170">If you must set route `Order` properties to route requests correctly, the app's routing scheme is probably confusing to clients and fragile to maintain.</span></span> <span data-ttu-id="b6860-171">查找以简化应用程序的路由方案。</span><span class="sxs-lookup"><span data-stu-id="b6860-171">Seek to simplify the app's routing scheme.</span></span> <span data-ttu-id="b6860-172">示例应用程序需要处理订单，若要演示几个路由方案使用的单个应用程序的显式路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-172">The sample app requires an explicit route processing order to demonstrate several routing scenarios using a single app.</span></span> <span data-ttu-id="b6860-173">但是，您应尝试避免设置路由的做法`Order`生产应用中。</span><span class="sxs-lookup"><span data-stu-id="b6860-173">However, you should attempt to avoid the practice of setting route `Order` in production apps.</span></span>

<span data-ttu-id="b6860-174">Razor Pages 路由和 MVC 控制器路由共享一个实现。</span><span class="sxs-lookup"><span data-stu-id="b6860-174">Razor Pages routing and MVC controller routing share an implementation.</span></span> <span data-ttu-id="b6860-175">路由顺序 MVC 主题中的信息位于[路由到控制器操作： 对属性路由排序](xref:mvc/controllers/routing#ordering-attribute-routes)。</span><span class="sxs-lookup"><span data-stu-id="b6860-175">Information on route order in the MVC topics is available at [Routing to controller actions: Ordering attribute routes](xref:mvc/controllers/routing#ordering-attribute-routes).</span></span>

## <a name="model-conventions"></a><span data-ttu-id="b6860-176">模型约定</span><span class="sxs-lookup"><span data-stu-id="b6860-176">Model conventions</span></span>

<span data-ttu-id="b6860-177">为 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 添加委托，以添加应用于 Razor 页面的[模型约定](xref:mvc/controllers/application-model#conventions)。</span><span class="sxs-lookup"><span data-stu-id="b6860-177">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add [model conventions](xref:mvc/controllers/application-model#conventions) that apply to Razor Pages.</span></span>

### <a name="add-a-route-model-convention-to-all-pages"></a><span data-ttu-id="b6860-178">将路由模型约定添加到所有页面</span><span class="sxs-lookup"><span data-stu-id="b6860-178">Add a route model convention to all pages</span></span>

<span data-ttu-id="b6860-179">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面路由模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="b6860-179">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page route model construction.</span></span>

<span data-ttu-id="b6860-180">示例应用将 `{globalTemplate?}` 路由模板添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-180">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

<span data-ttu-id="b6860-181"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `1`。</span><span class="sxs-lookup"><span data-stu-id="b6860-181">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `1`.</span></span> <span data-ttu-id="b6860-182">这可确保匹配行为示例应用程序中的以下路由：</span><span class="sxs-lookup"><span data-stu-id="b6860-182">This ensures the following route matching behavior in the sample app:</span></span>

* <span data-ttu-id="b6860-183">路由模板`TheContactPage/{text?}`添加本主题后面。</span><span class="sxs-lookup"><span data-stu-id="b6860-183">A route template for `TheContactPage/{text?}` is added later in the topic.</span></span> <span data-ttu-id="b6860-184">联系人页面路由的默认顺序`null`(`Order = 0`)，因此它匹配之前`{globalTemplate?}`路由模板。</span><span class="sxs-lookup"><span data-stu-id="b6860-184">The Contact Page route has a default order of `null` (`Order = 0`), so it matches before the `{globalTemplate?}` route template.</span></span>
* <span data-ttu-id="b6860-185">`{aboutTemplate?}`路由模板添加本主题后面。</span><span class="sxs-lookup"><span data-stu-id="b6860-185">An `{aboutTemplate?}` route template is added later in the topic.</span></span> <span data-ttu-id="b6860-186">为 `{aboutTemplate?}` 模板指定的 `Order` 为 `2`。</span><span class="sxs-lookup"><span data-stu-id="b6860-186">The `{aboutTemplate?}` template is given an `Order` of `2`.</span></span> <span data-ttu-id="b6860-187">当在 `/About/RouteDataValue` 中请求“关于”页面时，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = 1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 2`) 中。</span><span class="sxs-lookup"><span data-stu-id="b6860-187">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>
* <span data-ttu-id="b6860-188">`{otherPagesTemplate?}`路由模板添加本主题后面。</span><span class="sxs-lookup"><span data-stu-id="b6860-188">An `{otherPagesTemplate?}` route template is added later in the topic.</span></span> <span data-ttu-id="b6860-189">为 `{otherPagesTemplate?}` 模板指定的 `Order` 为 `2`。</span><span class="sxs-lookup"><span data-stu-id="b6860-189">The `{otherPagesTemplate?}` template is given an `Order` of `2`.</span></span> <span data-ttu-id="b6860-190">中的任何页时*Pages/OtherPages*文件夹请求与路由参数 (例如， `/OtherPages/Page1/RouteDataValue`)，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["otherPagesTemplate"]`(`Order = 2`)由于设置`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="b6860-190">When any page in the *Pages/OtherPages* folder is requested with a route parameter (for example, `/OtherPages/Page1/RouteDataValue`), "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="b6860-191">如有可能，未设置`Order`，这会导致`Order = 0`。</span><span class="sxs-lookup"><span data-stu-id="b6860-191">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="b6860-192">依赖于路由，以选择正确的路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-192">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="b6860-193">将 MVC 添加到 `Startup.ConfigureServices` 中的服务集合时，会添加 Razor 页面选项，例如添加[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)。</span><span class="sxs-lookup"><span data-stu-id="b6860-193">Razor Pages options, such as adding [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions), are added when MVC is added to the service collection in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="b6860-194">有关示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)。</span><span class="sxs-lookup"><span data-stu-id="b6860-194">For an example, see the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/).</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="b6860-195">在 `localhost:5000/About/GlobalRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-195">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-template.png)

### <a name="add-an-app-model-convention-to-all-pages"></a><span data-ttu-id="b6860-198">将应用模型约定添加到所有页面</span><span class="sxs-lookup"><span data-stu-id="b6860-198">Add an app model convention to all pages</span></span>

<span data-ttu-id="b6860-199">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面应用模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="b6860-199">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page app model construction.</span></span>

<span data-ttu-id="b6860-200">为了演示此约定以及本主题后面的其他约定，示例应用包含了一个 `AddHeaderAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="b6860-200">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="b6860-201">类构造函数采用 `name` 字符串和 `values` 字符串数组。</span><span class="sxs-lookup"><span data-stu-id="b6860-201">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="b6860-202">将在其 `OnResultExecuting` 方法中使用这些值来设置响应标头。</span><span class="sxs-lookup"><span data-stu-id="b6860-202">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="b6860-203">本主题后面的[页面模型操作约定](#page-model-action-conventions)部分展示了完整的类。</span><span class="sxs-lookup"><span data-stu-id="b6860-203">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="b6860-204">示例应用使用 `AddHeaderAttribute` 类将标头 `GlobalHeader` 添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-204">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="b6860-205">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="b6860-205">*Startup.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="b6860-206">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-206">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 GlobalHeader。](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"

### <a name="add-a-handler-model-convention-to-all-pages"></a><span data-ttu-id="b6860-208">将处理程序模型约定添加到的所有页面</span><span class="sxs-lookup"><span data-stu-id="b6860-208">Add a handler model convention to all pages</span></span>

<span data-ttu-id="b6860-209">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面处理程序模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="b6860-209">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page handler model construction.</span></span>

```csharp
public class GlobalPageHandlerModelConvention
    : IPageHandlerModelConvention
{
    public void Apply(PageHandlerModel model)
    {
        ...
    }
}
```

<span data-ttu-id="b6860-210">`Startup.ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="b6860-210">`Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```

::: moniker-end

## <a name="page-route-action-conventions"></a><span data-ttu-id="b6860-211">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-211">Page route action conventions</span></span>

<span data-ttu-id="b6860-212">默认路由模型提供程序派生自 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)，可调用旨在为页面路由配置提供扩展点的约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-212">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

### <a name="folder-route-model-convention"></a><span data-ttu-id="b6860-213">文件夹路由模型约定</span><span class="sxs-lookup"><span data-stu-id="b6860-213">Folder route model convention</span></span>

<span data-ttu-id="b6860-214">使用 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="b6860-214">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="b6860-215">示例应用使用 `AddFolderRouteModelConvention` 将 `{otherPagesTemplate?}` 路由模板添加到 *OtherPages* 文件夹中的页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-215">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

<span data-ttu-id="b6860-216"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `2`。</span><span class="sxs-lookup"><span data-stu-id="b6860-216">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `2`.</span></span> <span data-ttu-id="b6860-217">这可以保证的模板`{globalTemplate?}`(设置到主题中前面`1`) 提供单个路由值时，第一个路由数据值位置分配优先级。</span><span class="sxs-lookup"><span data-stu-id="b6860-217">This ensures that the template for `{globalTemplate?}` (set earlier in the topic to `1`) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="b6860-218">如果在页*Pages/OtherPages*文件夹请求与路由参数值 (例如， `/OtherPages/Page1/RouteDataValue`)，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["otherPagesTemplate"]`(`Order = 2`)由于设置`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="b6860-218">If a page in the *Pages/OtherPages* folder is requested with a route parameter value (for example, `/OtherPages/Page1/RouteDataValue`), "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="b6860-219">如有可能，未设置`Order`，这会导致`Order = 0`。</span><span class="sxs-lookup"><span data-stu-id="b6860-219">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="b6860-220">依赖于路由，以选择正确的路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-220">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="b6860-221">在 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 中请求示例的 Page1 页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-221">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 OtherPagesRouteValue 路由段请求 OtherPages 文件夹中的 Page1。](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

### <a name="page-route-model-convention"></a><span data-ttu-id="b6860-224">页面路由模型约定</span><span class="sxs-lookup"><span data-stu-id="b6860-224">Page route model convention</span></span>

<span data-ttu-id="b6860-225">使用 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为具有指定名称的页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="b6860-225">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="b6860-226">示例应用使用 `AddPageRouteModelConvention` 将 `{aboutTemplate?}` 路由模板添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-226">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

<span data-ttu-id="b6860-227"><xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `2`。</span><span class="sxs-lookup"><span data-stu-id="b6860-227">The <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> property for the <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> is set to `2`.</span></span> <span data-ttu-id="b6860-228">这可以保证的模板`{globalTemplate?}`(设置到主题中前面`1`) 提供单个路由值时，第一个路由数据值位置分配优先级。</span><span class="sxs-lookup"><span data-stu-id="b6860-228">This ensures that the template for `{globalTemplate?}` (set earlier in the topic to `1`) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="b6860-229">如果使用路由参数值在请求关于页面`/About/RouteDataValue`，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["aboutTemplate"]`(`Order = 2`) 因设置而`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="b6860-229">If the About page is requested with a route parameter value at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 2`) due to setting the `Order` property.</span></span>

<span data-ttu-id="b6860-230">如有可能，未设置`Order`，这会导致`Order = 0`。</span><span class="sxs-lookup"><span data-stu-id="b6860-230">Wherever possible, don't set the `Order`, which results in `Order = 0`.</span></span> <span data-ttu-id="b6860-231">依赖于路由，以选择正确的路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-231">Rely on routing to select the correct route.</span></span>

<span data-ttu-id="b6860-232">在 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-232">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 AboutRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

::: moniker range=">= aspnetcore-2.2"

## <a name="use-a-parameter-transformer-to-customize-page-routes"></a><span data-ttu-id="b6860-235">参数转换器用于自定义页面路由</span><span class="sxs-lookup"><span data-stu-id="b6860-235">Use a parameter transformer to customize page routes</span></span>

<span data-ttu-id="b6860-236">使用参数转换器可以自定义页面路由生成的 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="b6860-236">Page routes generated by ASP.NET Core can be customized using a parameter transformer.</span></span> <span data-ttu-id="b6860-237">参数转换程序实现 `IOutboundParameterTransformer` 并转换参数值。</span><span class="sxs-lookup"><span data-stu-id="b6860-237">A parameter transformer implements `IOutboundParameterTransformer` and transforms the value of parameters.</span></span> <span data-ttu-id="b6860-238">例如，一个自定义 `SlugifyParameterTransformer` 参数转换程序可将 `SubscriptionManagement` 路由值更改为 `subscription-management`。</span><span class="sxs-lookup"><span data-stu-id="b6860-238">For example, a custom `SlugifyParameterTransformer` parameter transformer changes the `SubscriptionManagement` route value to `subscription-management`.</span></span>

<span data-ttu-id="b6860-239">`PageRouteTransformerConvention`页面路由模型约定适用于在应用中自动生成的页路由文件夹和文件名称段参数转换器。</span><span class="sxs-lookup"><span data-stu-id="b6860-239">The `PageRouteTransformerConvention` page route model convention applies a parameter transformer to the folder and file name segments of automatically generated page routes in an app.</span></span> <span data-ttu-id="b6860-240">例如，Razor 页面文件位于 */Pages/SubscriptionManagement/ViewAll.cshtml*必须重写中其路由`/SubscriptionManagement/ViewAll`到`/subscription-management/view-all`。</span><span class="sxs-lookup"><span data-stu-id="b6860-240">For example, the Razor Pages file at */Pages/SubscriptionManagement/ViewAll.cshtml* would have its route rewritten from `/SubscriptionManagement/ViewAll` to `/subscription-management/view-all`.</span></span>

<span data-ttu-id="b6860-241">`PageRouteTransformerConvention` 仅将转换的页面路由来自 Razor 页面文件夹和文件名称自动生成的段。</span><span class="sxs-lookup"><span data-stu-id="b6860-241">`PageRouteTransformerConvention` only transforms the automatically generated segments of a page route that come from the Razor Pages folder and file name.</span></span> <span data-ttu-id="b6860-242">它不会转换与添加的路由段`@page`指令。</span><span class="sxs-lookup"><span data-stu-id="b6860-242">It doesn't transform route segments added with the `@page` directive.</span></span> <span data-ttu-id="b6860-243">约定也不会转换添加的路由<xref:Microsoft.Extensions.DependencyInjection.PageConventionCollectionExtensions.AddPageRoute*>。</span><span class="sxs-lookup"><span data-stu-id="b6860-243">The convention also doesn't transform routes added by <xref:Microsoft.Extensions.DependencyInjection.PageConventionCollectionExtensions.AddPageRoute*>.</span></span>

<span data-ttu-id="b6860-244">`PageRouteTransformerConvention`注册中的一个选项为`Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="b6860-244">The `PageRouteTransformerConvention` is registered as an option in `Startup.ConfigureServices`:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc()
        .AddRazorPagesOptions(options =>
            {
                options.Conventions.Add(
                    new PageRouteTransformerConvention(
                        new SlugifyParameterTransformer()));
            });
}

public class SlugifyParameterTransformer : IOutboundParameterTransformer
{
    public string TransformOutbound(object value)
    {
        if (value == null) { return null; }

        // Slugify value
        return Regex.Replace(value.ToString(), "([a-z])([A-Z])", "$1-$2").ToLower();
    }
}
```

::: moniker-end

## <a name="configure-a-page-route"></a><span data-ttu-id="b6860-245">配置页面路由</span><span class="sxs-lookup"><span data-stu-id="b6860-245">Configure a page route</span></span>

<span data-ttu-id="b6860-246">使用 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 配置路由，该路由指向指定页面路径中的页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-246">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="b6860-247">生成的页面链接使用指定的路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-247">Generated links to the page use your specified route.</span></span> <span data-ttu-id="b6860-248">`AddPageRoute` 使用 `AddPageRouteModelConvention` 建立路由。</span><span class="sxs-lookup"><span data-stu-id="b6860-248">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="b6860-249">示例应用为 *Contact.cshtml* 创建指向 `/TheContactPage` 的路由：</span><span class="sxs-lookup"><span data-stu-id="b6860-249">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="b6860-250">还可在 `/Contact` 中通过默认路由访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-250">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="b6860-251">示例应用的“联系人”页面自定义路由允许使用可选的 `text` 路由段 (`{text?}`)。</span><span class="sxs-lookup"><span data-stu-id="b6860-251">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="b6860-252">该页面还在其 `@page` 指令中包含此可选段，以便访问者在 `/Contact` 路由中访问该页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-252">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="b6860-253">请注意，在呈现的页面中，为**联系人**链接生成的 URL 反映了已更新的路由：</span><span class="sxs-lookup"><span data-stu-id="b6860-253">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![导航栏中的示例应用“联系人”链接](razor-pages-conventions/_static/contact-link.png)

![检查呈现的 HTML 中的“联系人”链接，可看到 href 设置为“/TheContactPage”](razor-pages-conventions/_static/contact-link-source.png)

<span data-ttu-id="b6860-256">在常规路由 `/Contact` 或自定义路由 `/TheContactPage` 中访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-256">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="b6860-257">如果提供附加的 `text` 路由段，该页面会显示所提供的 HTML 编码段：</span><span class="sxs-lookup"><span data-stu-id="b6860-257">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![在 URL 中提供可选“'text”路由段“TextValue”的 Microsoft Edge 浏览器示例。](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="b6860-260">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="b6860-260">Page model action conventions</span></span>

<span data-ttu-id="b6860-261">实现 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 的默认页面模型提供程序可调用约定，这些约定旨在为页面模型配置提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="b6860-261">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="b6860-262">在生成和修改页面发现及处理方案时，可使用这些约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-262">These conventions are useful when building and modifying page discovery and processing scenarios.</span></span>

<span data-ttu-id="b6860-263">对于此部分中的示例，示例应用使用 `AddHeaderAttribute` 类（一个 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)）来应用响应标头：</span><span class="sxs-lookup"><span data-stu-id="b6860-263">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="b6860-264">示例演示了如何使用约定将该属性应用于某个文件夹中的所有页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-264">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="b6860-265">**文件夹应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="b6860-265">**Folder app model convention**</span></span>

<span data-ttu-id="b6860-266">使用 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 创建并添加 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 实例上的操作。</span><span class="sxs-lookup"><span data-stu-id="b6860-266">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="b6860-267">示例演示了如何使用 `AddFolderApplicationModelConvention` 将标头 `OtherPagesHeader` 添加到应用的 *OtherPages* 文件夹内的页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-267">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="b6860-268">在 `localhost:5000/OtherPages/Page1` 中请求示例的 Page1 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-268">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/Page1 页面的响应标头显示已添加 OtherPagesHeader。](razor-pages-conventions/_static/page1-otherpages-header.png)

<span data-ttu-id="b6860-270">**页面应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="b6860-270">**Page app model convention**</span></span>

<span data-ttu-id="b6860-271">使用[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) ，它在调用操作[PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)页使用指定的名称。</span><span class="sxs-lookup"><span data-stu-id="b6860-271">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the specified name.</span></span>

<span data-ttu-id="b6860-272">示例演示了如何使用 `AddPageApplicationModelConvention` 将标头 `AboutHeader` 添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-272">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="b6860-273">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-273">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 AboutHeader。](razor-pages-conventions/_static/about-page-about-header.png)

<span data-ttu-id="b6860-275">**配置筛选器**</span><span class="sxs-lookup"><span data-stu-id="b6860-275">**Configure a filter**</span></span>

<span data-ttu-id="b6860-276">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 可配置要应用的指定筛选器。</span><span class="sxs-lookup"><span data-stu-id="b6860-276">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="b6860-277">用户可以实现筛选器类，但示例应用演示了如何在 Lambda 表达式中实现筛选器，该筛选器在后台作为可返回筛选器的工厂实现：</span><span class="sxs-lookup"><span data-stu-id="b6860-277">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="b6860-278">页面应用模型用于检查指向 *OtherPages* 文件夹中 Page2 页面的段的相对路径。</span><span class="sxs-lookup"><span data-stu-id="b6860-278">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="b6860-279">如果条件通过，则添加标头。</span><span class="sxs-lookup"><span data-stu-id="b6860-279">If the condition passes, a header is added.</span></span> <span data-ttu-id="b6860-280">如果不通过，则应用 `EmptyFilter`。</span><span class="sxs-lookup"><span data-stu-id="b6860-280">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="b6860-281">`EmptyFilter` 是一种[操作筛选器](xref:mvc/controllers/filters#action-filters)。</span><span class="sxs-lookup"><span data-stu-id="b6860-281">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="b6860-282">由于 Razor 页面会忽略操作筛选器，因此，如果路径不包含 `OtherPages/Page2`，`EmptyFilter` 会按预期发出空操作指令。</span><span class="sxs-lookup"><span data-stu-id="b6860-282">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="b6860-283">在 `localhost:5000/OtherPages/Page2` 中请求示例的 Page2 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-283">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header 已添加到 Page2 的响应。](razor-pages-conventions/_static/page2-filter-header.png)

<span data-ttu-id="b6860-285">**配置筛选器工厂**</span><span class="sxs-lookup"><span data-stu-id="b6860-285">**Configure a filter factory**</span></span>

<span data-ttu-id="b6860-286">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 可配置指定的工厂，以将[筛选器](xref:mvc/controllers/filters)应用于所有 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="b6860-286">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="b6860-287">示例应用提供了一个示例，说明如何使用[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)将具有两个值的标头 `FilterFactoryHeader` 添加到应用的页面：</span><span class="sxs-lookup"><span data-stu-id="b6860-287">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="b6860-288">*AddHeaderWithFactory.cs*：</span><span class="sxs-lookup"><span data-stu-id="b6860-288">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="b6860-289">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="b6860-289">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加两个 FilterFactoryHeader 标头。](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="b6860-291">替换默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="b6860-291">Replace the default page app model provider</span></span>

<span data-ttu-id="b6860-292">Razor 页面使用 `IPageApplicationModelProvider` 接口创建 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)。</span><span class="sxs-lookup"><span data-stu-id="b6860-292">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="b6860-293">用户可以从默认模型提供程序继承，以便为处理程序发现和处理提供自己的实现逻辑。</span><span class="sxs-lookup"><span data-stu-id="b6860-293">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="b6860-294">默认实现（[引用源](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)）为*未命名*和*已命名*处理程序的命名建立了约定，如下所述。</span><span class="sxs-lookup"><span data-stu-id="b6860-294">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="b6860-295">**默认的未命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="b6860-295">**Default unnamed handler methods**</span></span>

<span data-ttu-id="b6860-296">Http 谓词的处理程序方法（“未命名”的处理程序方法）遵循以下约定：`On<HTTP verb>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="b6860-296">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="b6860-297">未命名处理程序方法</span><span class="sxs-lookup"><span data-stu-id="b6860-297">Unnamed handler method</span></span>     | <span data-ttu-id="b6860-298">操作</span><span class="sxs-lookup"><span data-stu-id="b6860-298">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="b6860-299">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="b6860-299">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="b6860-300">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="b6860-300">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="b6860-301">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-301">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="b6860-302">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-302">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="b6860-303">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-303">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="b6860-304">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="b6860-304">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="b6860-305">**默认的已命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="b6860-305">**Default named handler methods**</span></span>

<span data-ttu-id="b6860-306">由开发人员提供的处理程序方法（“已命名”的处理程序方法）遵循类似的约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-306">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="b6860-307">处理程序名称出现在 Http 谓词之后或者 Http 谓词与 `Async` 之间：`On<HTTP verb><handler name>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="b6860-307">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="b6860-308">例如，用于处理消息的方法可能采用下表所示的命名。</span><span class="sxs-lookup"><span data-stu-id="b6860-308">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="b6860-309">已命名处理程序方法示例</span><span class="sxs-lookup"><span data-stu-id="b6860-309">Example named handler method</span></span>             | <span data-ttu-id="b6860-310">操作示例</span><span class="sxs-lookup"><span data-stu-id="b6860-310">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="b6860-311">获取消息。</span><span class="sxs-lookup"><span data-stu-id="b6860-311">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="b6860-312">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="b6860-312">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="b6860-313">DELETE 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-313">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="b6860-314">PUT 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-314">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="b6860-315">PATCH 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-315">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="b6860-316">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="b6860-316">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="b6860-317">**自定义处理程序方法名称**</span><span class="sxs-lookup"><span data-stu-id="b6860-317">**Customize handler method names**</span></span>

<span data-ttu-id="b6860-318">假设用户想更改未命名和已命名处理程序方法的命名方式。</span><span class="sxs-lookup"><span data-stu-id="b6860-318">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="b6860-319">备选命名方案是避免让方法名称以“On”开头，并使用第一个分词来确定 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="b6860-319">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="b6860-320">也可以进行其他更改，比如将 DELETE、PUT 和 PATCH 的谓词转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="b6860-320">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="b6860-321">这种方案提供下表所示的方法名称。</span><span class="sxs-lookup"><span data-stu-id="b6860-321">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="b6860-322">处理程序方法</span><span class="sxs-lookup"><span data-stu-id="b6860-322">Handler method</span></span>                       | <span data-ttu-id="b6860-323">操作</span><span class="sxs-lookup"><span data-stu-id="b6860-323">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="b6860-324">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="b6860-324">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="b6860-325">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="b6860-325">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="b6860-326">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-326">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="b6860-327">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-327">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="b6860-328">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="b6860-328">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="b6860-329">获取消息。</span><span class="sxs-lookup"><span data-stu-id="b6860-329">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="b6860-330">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="b6860-330">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="b6860-331">POST 消息以进行删除。</span><span class="sxs-lookup"><span data-stu-id="b6860-331">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="b6860-332">POST 消息以进行放置。</span><span class="sxs-lookup"><span data-stu-id="b6860-332">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="b6860-333">POST 消息以进行修补。</span><span class="sxs-lookup"><span data-stu-id="b6860-333">POST a message to patch.</span></span>       |

<span data-ttu-id="b6860-334">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="b6860-334">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="b6860-335">若要建立此方案，请从 `DefaultPageApplicationModelProvider` 类继承并重写 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 方法，以提供自定义逻辑来解析 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 处理程序名称。</span><span class="sxs-lookup"><span data-stu-id="b6860-335">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="b6860-336">示例应用展示了如何在其 `CustomPageApplicationModelProvider` 类中执行此操作：</span><span class="sxs-lookup"><span data-stu-id="b6860-336">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="b6860-337">该类的要点包括：</span><span class="sxs-lookup"><span data-stu-id="b6860-337">Highlights of the class include:</span></span>

* <span data-ttu-id="b6860-338">该类继承自 `DefaultPageApplicationModelProvider`。</span><span class="sxs-lookup"><span data-stu-id="b6860-338">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="b6860-339">`TryParseHandlerMethod` 对处理程序进行处理，以便在创建 `PageHandlerModel` 时确定 Http 谓词 (`httpMethod`) 和已命名处理程序名称 (`handlerName`)。</span><span class="sxs-lookup"><span data-stu-id="b6860-339">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="b6860-340">忽略 `Async` 后缀（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="b6860-340">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="b6860-341">使用大小写分析方法名称中的 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="b6860-341">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="b6860-342">当方法名称（不带 `Async`）与 Http 谓词名称相同时，就不存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="b6860-342">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="b6860-343">`handlerName` 设置为 `null`，且方法名称为 `Get`、`Post`、`Delete`、`Put` 或 `Patch`。</span><span class="sxs-lookup"><span data-stu-id="b6860-343">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="b6860-344">当方法名称（不带 `Async`）的长度超过 Http 谓词名称时，就存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="b6860-344">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="b6860-345">`handlerName` 设置为 `<method name (less 'Async', if present)>`。</span><span class="sxs-lookup"><span data-stu-id="b6860-345">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="b6860-346">例如，“GetMessage”和“GetMessageAsync”都生成处理程序名称“GetMessage”。</span><span class="sxs-lookup"><span data-stu-id="b6860-346">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="b6860-347">DELETE、PUT 和 PATCH Http 谓词都转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="b6860-347">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="b6860-348">在 `Startup` 类中注册 `CustomPageApplicationModelProvider`：</span><span class="sxs-lookup"><span data-stu-id="b6860-348">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="b6860-349">*Index.cshtml.cs* 中的页面模型演示了如何针对应用中的页面更改常规的处理程序方法命名约定。</span><span class="sxs-lookup"><span data-stu-id="b6860-349">The page model in *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="b6860-350">用于 Razor 页面的常规“On”前缀命名已被删除。</span><span class="sxs-lookup"><span data-stu-id="b6860-350">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="b6860-351">用于初始化页面状态的方法现在命名为 `Get`。</span><span class="sxs-lookup"><span data-stu-id="b6860-351">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="b6860-352">为任何页面打开任何页面模型时，都可以看到此约定贯穿于整个应用。</span><span class="sxs-lookup"><span data-stu-id="b6860-352">You can see this convention used throughout the app if you open any page model for any of the pages.</span></span>

<span data-ttu-id="b6860-353">其他各个方法均以描述其处理的 Http 谓词开头。</span><span class="sxs-lookup"><span data-stu-id="b6860-353">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="b6860-354">以 `Delete` 开头的两个方法通常被视为 DELETE Http 谓词，但 `TryParseHandlerMethod` 中的逻辑会针对这两种处理程序将该谓词显式设置为 POST。</span><span class="sxs-lookup"><span data-stu-id="b6860-354">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="b6860-355">请注意，`Async` 在 `DeleteAllMessages` 和 `DeleteMessageAsync` 之间是可选的。</span><span class="sxs-lookup"><span data-stu-id="b6860-355">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="b6860-356">它们都是异步方法，但用户可以选择是否使用 `Async` 后缀；我们建议使用。</span><span class="sxs-lookup"><span data-stu-id="b6860-356">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="b6860-357">此处使用 `DeleteAllMessages` 只是为了进行演示，但建议将此类方法命名为 `DeleteAllMessagesAsync`。</span><span class="sxs-lookup"><span data-stu-id="b6860-357">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="b6860-358">它对示例的实现处理没有影响，但使用 `Async` 后缀强调了它是异步方法的事实。</span><span class="sxs-lookup"><span data-stu-id="b6860-358">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="b6860-359">请注意，*Index.cshtml* 中提供的处理程序名称与 `DeleteAllMessages` 和 `DeleteMessageAsync` 处理程序方法相匹配：</span><span class="sxs-lookup"><span data-stu-id="b6860-359">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="b6860-360">为了方便处理程序将 POST 请求与方法进行匹配，`TryParseHandlerMethod` 剔除了处理程序方法名称 `DeleteMessageAsync` 中的 `Async`。</span><span class="sxs-lookup"><span data-stu-id="b6860-360">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="b6860-361">`DeleteMessage` 的 `asp-page-handler` 名称与处理程序方法 `DeleteMessageAsync` 匹配。</span><span class="sxs-lookup"><span data-stu-id="b6860-361">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="b6860-362">MVC 筛选器和页面筛选器 (IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="b6860-362">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="b6860-363">Razor 页面会忽略 MVC [操作筛选器](xref:mvc/controllers/filters#action-filters)，因为 Razor 页面使用处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="b6860-363">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="b6860-364">可使用其他类型的 MVC 筛选器：[授权](xref:mvc/controllers/filters#authorization-filters)、[异常](xref:mvc/controllers/filters#exception-filters)、[资源](xref:mvc/controllers/filters#resource-filters)和[结果](xref:mvc/controllers/filters#result-filters)。</span><span class="sxs-lookup"><span data-stu-id="b6860-364">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="b6860-365">有关详细信息，请参阅[筛选器](xref:mvc/controllers/filters)主题。</span><span class="sxs-lookup"><span data-stu-id="b6860-365">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="b6860-366">页面筛选器 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) 是应用于 Razor 页面的一种筛选器。</span><span class="sxs-lookup"><span data-stu-id="b6860-366">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="b6860-367">有关详细信息，请参阅 [Razor 页面的筛选方法](xref:razor-pages/filter)。</span><span class="sxs-lookup"><span data-stu-id="b6860-367">For more information, see [Filter methods for Razor Pages](xref:razor-pages/filter).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6860-368">其他资源</span><span class="sxs-lookup"><span data-stu-id="b6860-368">Additional resources</span></span>

* [<span data-ttu-id="b6860-369">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="b6860-369">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
