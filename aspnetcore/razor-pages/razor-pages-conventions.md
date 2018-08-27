---
title: ASP.NET Core 中 Razor 页面的路由和应用约定
author: guardrex
description: 了解路由和应用模型提供程序约定如何帮助控制页面路由、发现和处理。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 04/12/2018
uid: razor-pages/razor-pages-conventions
ms.openlocfilehash: 5a5d580b4260767e411571ccacc19d6e8fe12559
ms.sourcegitcommit: 028ad28c546de706ace98066c76774de33e4ad20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/08/2018
ms.locfileid: "42909741"
---
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a><span data-ttu-id="943cc-103">ASP.NET Core 中 Razor 页面的路由和应用约定</span><span class="sxs-lookup"><span data-stu-id="943cc-103">Razor Pages route and app conventions in ASP.NET Core</span></span>

<span data-ttu-id="943cc-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="943cc-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="943cc-105">了解如何使用[页面路由和应用模型提供程序约定](xref:mvc/controllers/application-model#conventions)来控制 Razor 页面应用中的页面路由、发现和处理。</span><span class="sxs-lookup"><span data-stu-id="943cc-105">Learn how to use page [route and app model provider conventions](xref:mvc/controllers/application-model#conventions) to control page routing, discovery, and processing in Razor Pages apps.</span></span>

<span data-ttu-id="943cc-106">需要为各个页面配置自定义页面路由时，可使用本主题稍后所述的 [AddPageRoute 约定](#configure-a-page-route)配置页面路由。</span><span class="sxs-lookup"><span data-stu-id="943cc-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="943cc-107">若要指定页面路由、 添加路由段，或将参数添加到路由，请使用页面的`@page`指令。</span><span class="sxs-lookup"><span data-stu-id="943cc-107">To specify a page route, add route segments, or add parameters to a route, use the page's `@page` directive.</span></span> <span data-ttu-id="943cc-108">有关详细信息，请参阅[自定义路由](xref:razor-pages/index#custom-routes)。</span><span class="sxs-lookup"><span data-stu-id="943cc-108">For more information, see [Custom routes](xref:razor-pages/index#custom-routes).</span></span>

<span data-ttu-id="943cc-109">有不能用作路由段或参数名称的保留的字。</span><span class="sxs-lookup"><span data-stu-id="943cc-109">There are reserved words that can't be used as route segments or parameter names.</span></span> <span data-ttu-id="943cc-110">有关详细信息，请参阅[路由： 保留路由名称](xref:fundamentals/routing#reserved-routing-names)。</span><span class="sxs-lookup"><span data-stu-id="943cc-110">For more information, see [Routing: Reserved routing names](xref:fundamentals/routing#reserved-routing-names).</span></span>

<span data-ttu-id="943cc-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="943cc-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range="= aspnetcore-2.0"

| <span data-ttu-id="943cc-112">方案</span><span class="sxs-lookup"><span data-stu-id="943cc-112">Scenario</span></span> | <span data-ttu-id="943cc-113">示例演示...</span><span class="sxs-lookup"><span data-stu-id="943cc-113">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="943cc-114">模型约定</span><span class="sxs-lookup"><span data-stu-id="943cc-114">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="943cc-115">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="943cc-115">Conventions.Add</span></span><ul><li><span data-ttu-id="943cc-116">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-116">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-117">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-117">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="943cc-118">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-118">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="943cc-119">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-119">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="943cc-120">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-120">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-121">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-121">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-122">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="943cc-122">AddPageRoute</span></span></li></ul> | <span data-ttu-id="943cc-123">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-123">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="943cc-124">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-124">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="943cc-125">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-125">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="943cc-126">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-126">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="943cc-127">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="943cc-127">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="943cc-128">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-128">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="943cc-129">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="943cc-129">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="943cc-130">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-130">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

| <span data-ttu-id="943cc-131">方案</span><span class="sxs-lookup"><span data-stu-id="943cc-131">Scenario</span></span> | <span data-ttu-id="943cc-132">示例演示...</span><span class="sxs-lookup"><span data-stu-id="943cc-132">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="943cc-133">模型约定</span><span class="sxs-lookup"><span data-stu-id="943cc-133">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="943cc-134">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="943cc-134">Conventions.Add</span></span><ul><li><span data-ttu-id="943cc-135">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-135">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-136">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-136">IPageApplicationModelConvention</span></span></li><li><span data-ttu-id="943cc-137">IPageHandlerModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-137">IPageHandlerModelConvention</span></span></li></ul> | <span data-ttu-id="943cc-138">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-138">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="943cc-139">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-139">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="943cc-140">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-140">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-141">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-141">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="943cc-142">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="943cc-142">AddPageRoute</span></span></li></ul> | <span data-ttu-id="943cc-143">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-143">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="943cc-144">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-144">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="943cc-145">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-145">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="943cc-146">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="943cc-146">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="943cc-147">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="943cc-147">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="943cc-148">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-148">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="943cc-149">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="943cc-149">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="943cc-150">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-150">Replace the default page model provider to change the conventions for handler names.</span></span> |

::: moniker-end

<span data-ttu-id="943cc-151">使用 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 扩展方法向 `Startup` 类中服务集合的 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) 添加和配置 Razor 页面约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-151">Razor Pages conventions are added and configured using the [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) extension method to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) on the service collection in the `Startup` class.</span></span> <span data-ttu-id="943cc-152">本主题稍后会介绍以下约定示例：</span><span class="sxs-lookup"><span data-stu-id="943cc-152">The following convention examples are explained later in this topic:</span></span>

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

## <a name="model-conventions"></a><span data-ttu-id="943cc-153">模型约定</span><span class="sxs-lookup"><span data-stu-id="943cc-153">Model conventions</span></span>

<span data-ttu-id="943cc-154">为 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 添加委托，以添加应用于 Razor 页面的[模型约定](xref:mvc/controllers/application-model#conventions)。</span><span class="sxs-lookup"><span data-stu-id="943cc-154">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add [model conventions](xref:mvc/controllers/application-model#conventions) that apply to Razor Pages.</span></span>

<span data-ttu-id="943cc-155">**将路由模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="943cc-155">**Add a route model convention to all pages**</span></span>

<span data-ttu-id="943cc-156">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面路由模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="943cc-156">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page route model construction.</span></span>

<span data-ttu-id="943cc-157">示例应用将 `{globalTemplate?}` 路由模板添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-157">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="943cc-158">`AttributeRouteModel` 的 `Order` 属性设置为 `-1`。</span><span class="sxs-lookup"><span data-stu-id="943cc-158">The `Order` property for the `AttributeRouteModel` is set to `-1`.</span></span> <span data-ttu-id="943cc-159">这确保了当提供单个路由值时，该模板被赋予第一个路由数据值位置的优先级，并且它将优先于自动生成的 Razor 页面路由。</span><span class="sxs-lookup"><span data-stu-id="943cc-159">This ensures that this template is given priority for the first route data value position when a single route value is provided and also that it would have priority over automatically generated Razor Pages routes.</span></span> <span data-ttu-id="943cc-160">例如，示例在本主题的后面部分添加了一个 `{aboutTemplate?}` 路由模板。</span><span class="sxs-lookup"><span data-stu-id="943cc-160">For example, the sample adds an `{aboutTemplate?}` route template later in the topic.</span></span> <span data-ttu-id="943cc-161">为 `{aboutTemplate?}` 模板指定的 `Order` 为 `1`。</span><span class="sxs-lookup"><span data-stu-id="943cc-161">The `{aboutTemplate?}` template is given an `Order` of `1`.</span></span> <span data-ttu-id="943cc-162">当在 `/About/RouteDataValue` 中请求“关于”页面时，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="943cc-162">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="943cc-163">将 MVC 添加到 `Startup.ConfigureServices` 中的服务集合时，会添加 Razor 页面选项，例如添加[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)。</span><span class="sxs-lookup"><span data-stu-id="943cc-163">Razor Pages options, such as adding [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions), are added when MVC is added to the service collection in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="943cc-164">有关示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)。</span><span class="sxs-lookup"><span data-stu-id="943cc-164">For an example, see the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/).</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="943cc-165">在 `localhost:5000/About/GlobalRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-165">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-template.png)

<span data-ttu-id="943cc-168">**将应用模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="943cc-168">**Add an app model convention to all pages**</span></span>

<span data-ttu-id="943cc-169">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面应用模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="943cc-169">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page app model construction.</span></span>

<span data-ttu-id="943cc-170">为了演示此约定以及本主题后面的其他约定，示例应用包含了一个 `AddHeaderAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="943cc-170">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="943cc-171">类构造函数采用 `name` 字符串和 `values` 字符串数组。</span><span class="sxs-lookup"><span data-stu-id="943cc-171">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="943cc-172">将在其 `OnResultExecuting` 方法中使用这些值来设置响应标头。</span><span class="sxs-lookup"><span data-stu-id="943cc-172">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="943cc-173">本主题后面的[页面模型操作约定](#page-model-action-conventions)部分展示了完整的类。</span><span class="sxs-lookup"><span data-stu-id="943cc-173">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="943cc-174">示例应用使用 `AddHeaderAttribute` 类将标头 `GlobalHeader` 添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-174">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="943cc-175">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="943cc-175">*Startup.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="943cc-176">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-176">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 GlobalHeader。](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="943cc-178">**将处理程序模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="943cc-178">**Add a handler model convention to all pages**</span></span>

<span data-ttu-id="943cc-179">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面处理程序模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="943cc-179">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page handler model construction.</span></span>

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

<span data-ttu-id="943cc-180">`Startup.ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="943cc-180">`Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```
::: moniker-end

## <a name="page-route-action-conventions"></a><span data-ttu-id="943cc-181">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-181">Page route action conventions</span></span>

<span data-ttu-id="943cc-182">默认路由模型提供程序派生自 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)，可调用旨在为页面路由配置提供扩展点的约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-182">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

<span data-ttu-id="943cc-183">**文件夹路由模型约定**</span><span class="sxs-lookup"><span data-stu-id="943cc-183">**Folder route model convention**</span></span>

<span data-ttu-id="943cc-184">使用 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="943cc-184">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="943cc-185">示例应用使用 `AddFolderRouteModelConvention` 将 `{otherPagesTemplate?}` 路由模板添加到 *OtherPages* 文件夹中的页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-185">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="943cc-186">`AttributeRouteModel` 的 `Order` 属性设置为 `1`。</span><span class="sxs-lookup"><span data-stu-id="943cc-186">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="943cc-187">这样可确保，当提供单个路由值时，优先将 `{globalTemplate?}` 的模板（已在本主题的前面部分设置）作为第一个路由数据值位置。</span><span class="sxs-lookup"><span data-stu-id="943cc-187">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="943cc-188">如果在 `/OtherPages/Page1/RouteDataValue` 中请求 Page1 页面，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="943cc-188">If the Page1 page is requested at `/OtherPages/Page1/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="943cc-189">在 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 中请求示例的 Page1 页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-189">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 OtherPagesRouteValue 路由段请求 OtherPages 文件夹中的 Page1。](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

<span data-ttu-id="943cc-192">**页面路由模型约定**</span><span class="sxs-lookup"><span data-stu-id="943cc-192">**Page route model convention**</span></span>

<span data-ttu-id="943cc-193">使用 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为具有指定名称的页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="943cc-193">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="943cc-194">示例应用使用 `AddPageRouteModelConvention` 将 `{aboutTemplate?}` 路由模板添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-194">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> <span data-ttu-id="943cc-195">`AttributeRouteModel` 的 `Order` 属性设置为 `1`。</span><span class="sxs-lookup"><span data-stu-id="943cc-195">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="943cc-196">这样可确保，当提供单个路由值时，优先将 `{globalTemplate?}` 的模板（已在本主题的前面部分设置）作为第一个路由数据值位置。</span><span class="sxs-lookup"><span data-stu-id="943cc-196">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="943cc-197">如果在 `/About/RouteDataValue` 中请求“关于”页面，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="943cc-197">If the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="943cc-198">在 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-198">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 AboutRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a><span data-ttu-id="943cc-201">配置页面路由</span><span class="sxs-lookup"><span data-stu-id="943cc-201">Configure a page route</span></span>

<span data-ttu-id="943cc-202">使用 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 配置路由，该路由指向指定页面路径中的页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-202">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="943cc-203">生成的页面链接使用指定的路由。</span><span class="sxs-lookup"><span data-stu-id="943cc-203">Generated links to the page use your specified route.</span></span> <span data-ttu-id="943cc-204">`AddPageRoute` 使用 `AddPageRouteModelConvention` 建立路由。</span><span class="sxs-lookup"><span data-stu-id="943cc-204">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="943cc-205">示例应用为 *Contact.cshtml* 创建指向 `/TheContactPage` 的路由：</span><span class="sxs-lookup"><span data-stu-id="943cc-205">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="943cc-206">还可在 `/Contact` 中通过默认路由访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-206">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="943cc-207">示例应用的“联系人”页面自定义路由允许使用可选的 `text` 路由段 (`{text?}`)。</span><span class="sxs-lookup"><span data-stu-id="943cc-207">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="943cc-208">该页面还在其 `@page` 指令中包含此可选段，以便访问者在 `/Contact` 路由中访问该页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-208">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="943cc-209">请注意，在呈现的页面中，为**联系人**链接生成的 URL 反映了已更新的路由：</span><span class="sxs-lookup"><span data-stu-id="943cc-209">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![导航栏中的示例应用“联系人”链接](razor-pages-conventions/_static/contact-link.png)

![检查呈现的 HTML 中的“联系人”链接，可看到 href 设置为“/TheContactPage”](razor-pages-conventions/_static/contact-link-source.png)

<span data-ttu-id="943cc-212">在常规路由 `/Contact` 或自定义路由 `/TheContactPage` 中访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-212">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="943cc-213">如果提供附加的 `text` 路由段，该页面会显示所提供的 HTML 编码段：</span><span class="sxs-lookup"><span data-stu-id="943cc-213">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![在 URL 中提供可选“'text”路由段“TextValue”的 Microsoft Edge 浏览器示例。](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="943cc-216">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="943cc-216">Page model action conventions</span></span>

<span data-ttu-id="943cc-217">实现 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 的默认页面模型提供程序可调用约定，这些约定旨在为页面模型配置提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="943cc-217">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="943cc-218">在生成和修改页面发现及处理方案时，可使用这些约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-218">These conventions are useful when building and modifying page discovery and processing scenarios.</span></span>

<span data-ttu-id="943cc-219">对于此部分中的示例，示例应用使用 `AddHeaderAttribute` 类（一个 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)）来应用响应标头：</span><span class="sxs-lookup"><span data-stu-id="943cc-219">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="943cc-220">示例演示了如何使用约定将该属性应用于某个文件夹中的所有页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-220">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="943cc-221">**文件夹应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="943cc-221">**Folder app model convention**</span></span>

<span data-ttu-id="943cc-222">使用 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 创建并添加 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 实例上的操作。</span><span class="sxs-lookup"><span data-stu-id="943cc-222">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="943cc-223">示例演示了如何使用 `AddFolderApplicationModelConvention` 将标头 `OtherPagesHeader` 添加到应用的 *OtherPages* 文件夹内的页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-223">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="943cc-224">在 `localhost:5000/OtherPages/Page1` 中请求示例的 Page1 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-224">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/Page1 页面的响应标头显示已添加 OtherPagesHeader。](razor-pages-conventions/_static/page1-otherpages-header.png)

<span data-ttu-id="943cc-226">**页面应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="943cc-226">**Page app model convention**</span></span>

<span data-ttu-id="943cc-227">使用[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) ，它在调用操作[PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)页使用指定的名称。</span><span class="sxs-lookup"><span data-stu-id="943cc-227">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the specified name.</span></span>

<span data-ttu-id="943cc-228">示例演示了如何使用 `AddPageApplicationModelConvention` 将标头 `AboutHeader` 添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-228">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="943cc-229">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-229">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 AboutHeader。](razor-pages-conventions/_static/about-page-about-header.png)

<span data-ttu-id="943cc-231">**配置筛选器**</span><span class="sxs-lookup"><span data-stu-id="943cc-231">**Configure a filter**</span></span>

<span data-ttu-id="943cc-232">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 可配置要应用的指定筛选器。</span><span class="sxs-lookup"><span data-stu-id="943cc-232">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="943cc-233">用户可以实现筛选器类，但示例应用演示了如何在 Lambda 表达式中实现筛选器，该筛选器在后台作为可返回筛选器的工厂实现：</span><span class="sxs-lookup"><span data-stu-id="943cc-233">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="943cc-234">页面应用模型用于检查指向 *OtherPages* 文件夹中 Page2 页面的段的相对路径。</span><span class="sxs-lookup"><span data-stu-id="943cc-234">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="943cc-235">如果条件通过，则添加标头。</span><span class="sxs-lookup"><span data-stu-id="943cc-235">If the condition passes, a header is added.</span></span> <span data-ttu-id="943cc-236">如果不通过，则应用 `EmptyFilter`。</span><span class="sxs-lookup"><span data-stu-id="943cc-236">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="943cc-237">`EmptyFilter` 是一种[操作筛选器](xref:mvc/controllers/filters#action-filters)。</span><span class="sxs-lookup"><span data-stu-id="943cc-237">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="943cc-238">由于 Razor 页面会忽略操作筛选器，因此，如果路径不包含 `OtherPages/Page2`，`EmptyFilter` 会按预期发出空操作指令。</span><span class="sxs-lookup"><span data-stu-id="943cc-238">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="943cc-239">在 `localhost:5000/OtherPages/Page2` 中请求示例的 Page2 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-239">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header 已添加到 Page2 的响应。](razor-pages-conventions/_static/page2-filter-header.png)

<span data-ttu-id="943cc-241">**配置筛选器工厂**</span><span class="sxs-lookup"><span data-stu-id="943cc-241">**Configure a filter factory**</span></span>

<span data-ttu-id="943cc-242">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 可配置指定的工厂，以将[筛选器](xref:mvc/controllers/filters)应用于所有 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="943cc-242">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="943cc-243">示例应用提供了一个示例，说明如何使用[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)将具有两个值的标头 `FilterFactoryHeader` 添加到应用的页面：</span><span class="sxs-lookup"><span data-stu-id="943cc-243">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="943cc-244">*AddHeaderWithFactory.cs*：</span><span class="sxs-lookup"><span data-stu-id="943cc-244">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="943cc-245">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="943cc-245">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加两个 FilterFactoryHeader 标头。](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="943cc-247">替换默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="943cc-247">Replace the default page app model provider</span></span>

<span data-ttu-id="943cc-248">Razor 页面使用 `IPageApplicationModelProvider` 接口创建 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)。</span><span class="sxs-lookup"><span data-stu-id="943cc-248">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="943cc-249">用户可以从默认模型提供程序继承，以便为处理程序发现和处理提供自己的实现逻辑。</span><span class="sxs-lookup"><span data-stu-id="943cc-249">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="943cc-250">默认实现（[引用源](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)）为*未命名*和*已命名*处理程序的命名建立了约定，如下所述。</span><span class="sxs-lookup"><span data-stu-id="943cc-250">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="943cc-251">**默认的未命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="943cc-251">**Default unnamed handler methods**</span></span>

<span data-ttu-id="943cc-252">Http 谓词的处理程序方法（“未命名”的处理程序方法）遵循以下约定：`On<HTTP verb>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="943cc-252">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="943cc-253">未命名处理程序方法</span><span class="sxs-lookup"><span data-stu-id="943cc-253">Unnamed handler method</span></span>     | <span data-ttu-id="943cc-254">操作</span><span class="sxs-lookup"><span data-stu-id="943cc-254">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="943cc-255">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="943cc-255">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="943cc-256">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="943cc-256">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="943cc-257">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-257">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="943cc-258">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-258">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="943cc-259">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-259">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="943cc-260">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="943cc-260">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="943cc-261">**默认的已命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="943cc-261">**Default named handler methods**</span></span>

<span data-ttu-id="943cc-262">由开发人员提供的处理程序方法（“已命名”的处理程序方法）遵循类似的约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-262">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="943cc-263">处理程序名称出现在 Http 谓词之后或者 Http 谓词与 `Async` 之间：`On<HTTP verb><handler name>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="943cc-263">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="943cc-264">例如，用于处理消息的方法可能采用下表所示的命名。</span><span class="sxs-lookup"><span data-stu-id="943cc-264">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="943cc-265">已命名处理程序方法示例</span><span class="sxs-lookup"><span data-stu-id="943cc-265">Example named handler method</span></span>             | <span data-ttu-id="943cc-266">操作示例</span><span class="sxs-lookup"><span data-stu-id="943cc-266">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="943cc-267">获取消息。</span><span class="sxs-lookup"><span data-stu-id="943cc-267">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="943cc-268">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="943cc-268">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="943cc-269">DELETE 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-269">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="943cc-270">PUT 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-270">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="943cc-271">PATCH 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-271">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="943cc-272">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="943cc-272">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="943cc-273">**自定义处理程序方法名称**</span><span class="sxs-lookup"><span data-stu-id="943cc-273">**Customize handler method names**</span></span>

<span data-ttu-id="943cc-274">假设用户想更改未命名和已命名处理程序方法的命名方式。</span><span class="sxs-lookup"><span data-stu-id="943cc-274">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="943cc-275">备选命名方案是避免让方法名称以“On”开头，并使用第一个分词来确定 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="943cc-275">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="943cc-276">也可以进行其他更改，比如将 DELETE、PUT 和 PATCH 的谓词转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="943cc-276">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="943cc-277">这种方案提供下表所示的方法名称。</span><span class="sxs-lookup"><span data-stu-id="943cc-277">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="943cc-278">处理程序方法</span><span class="sxs-lookup"><span data-stu-id="943cc-278">Handler method</span></span>                       | <span data-ttu-id="943cc-279">操作</span><span class="sxs-lookup"><span data-stu-id="943cc-279">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="943cc-280">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="943cc-280">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="943cc-281">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="943cc-281">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="943cc-282">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-282">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="943cc-283">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-283">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="943cc-284">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="943cc-284">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="943cc-285">获取消息。</span><span class="sxs-lookup"><span data-stu-id="943cc-285">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="943cc-286">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="943cc-286">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="943cc-287">POST 消息以进行删除。</span><span class="sxs-lookup"><span data-stu-id="943cc-287">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="943cc-288">POST 消息以进行放置。</span><span class="sxs-lookup"><span data-stu-id="943cc-288">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="943cc-289">POST 消息以进行修补。</span><span class="sxs-lookup"><span data-stu-id="943cc-289">POST a message to patch.</span></span>       |

<span data-ttu-id="943cc-290">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="943cc-290">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="943cc-291">若要建立此方案，请从 `DefaultPageApplicationModelProvider` 类继承并重写 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 方法，以提供自定义逻辑来解析 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 处理程序名称。</span><span class="sxs-lookup"><span data-stu-id="943cc-291">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="943cc-292">示例应用展示了如何在其 `CustomPageApplicationModelProvider` 类中执行此操作：</span><span class="sxs-lookup"><span data-stu-id="943cc-292">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="943cc-293">该类的要点包括：</span><span class="sxs-lookup"><span data-stu-id="943cc-293">Highlights of the class include:</span></span>

* <span data-ttu-id="943cc-294">该类继承自 `DefaultPageApplicationModelProvider`。</span><span class="sxs-lookup"><span data-stu-id="943cc-294">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="943cc-295">`TryParseHandlerMethod` 对处理程序进行处理，以便在创建 `PageHandlerModel` 时确定 Http 谓词 (`httpMethod`) 和已命名处理程序名称 (`handlerName`)。</span><span class="sxs-lookup"><span data-stu-id="943cc-295">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="943cc-296">忽略 `Async` 后缀（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="943cc-296">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="943cc-297">使用大小写分析方法名称中的 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="943cc-297">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="943cc-298">当方法名称（不带 `Async`）与 Http 谓词名称相同时，就不存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="943cc-298">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="943cc-299">`handlerName` 设置为 `null`，且方法名称为 `Get`、`Post`、`Delete`、`Put` 或 `Patch`。</span><span class="sxs-lookup"><span data-stu-id="943cc-299">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="943cc-300">当方法名称（不带 `Async`）的长度超过 Http 谓词名称时，就存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="943cc-300">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="943cc-301">`handlerName` 设置为 `<method name (less 'Async', if present)>`。</span><span class="sxs-lookup"><span data-stu-id="943cc-301">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="943cc-302">例如，“GetMessage”和“GetMessageAsync”都生成处理程序名称“GetMessage”。</span><span class="sxs-lookup"><span data-stu-id="943cc-302">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="943cc-303">DELETE、PUT 和 PATCH Http 谓词都转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="943cc-303">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="943cc-304">在 `Startup` 类中注册 `CustomPageApplicationModelProvider`：</span><span class="sxs-lookup"><span data-stu-id="943cc-304">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="943cc-305">*Index.cshtml.cs* 中的页面模型演示了如何针对应用中的页面更改常规的处理程序方法命名约定。</span><span class="sxs-lookup"><span data-stu-id="943cc-305">The page model in *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="943cc-306">用于 Razor 页面的常规“On”前缀命名已被删除。</span><span class="sxs-lookup"><span data-stu-id="943cc-306">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="943cc-307">用于初始化页面状态的方法现在命名为 `Get`。</span><span class="sxs-lookup"><span data-stu-id="943cc-307">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="943cc-308">为任何页面打开任何页面模型时，都可以看到此约定贯穿于整个应用。</span><span class="sxs-lookup"><span data-stu-id="943cc-308">You can see this convention used throughout the app if you open any page model for any of the pages.</span></span>

<span data-ttu-id="943cc-309">其他各个方法均以描述其处理的 Http 谓词开头。</span><span class="sxs-lookup"><span data-stu-id="943cc-309">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="943cc-310">以 `Delete` 开头的两个方法通常被视为 DELETE Http 谓词，但 `TryParseHandlerMethod` 中的逻辑会针对这两种处理程序将该谓词显式设置为 POST。</span><span class="sxs-lookup"><span data-stu-id="943cc-310">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="943cc-311">请注意，`Async` 在 `DeleteAllMessages` 和 `DeleteMessageAsync` 之间是可选的。</span><span class="sxs-lookup"><span data-stu-id="943cc-311">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="943cc-312">它们都是异步方法，但用户可以选择是否使用 `Async` 后缀；我们建议使用。</span><span class="sxs-lookup"><span data-stu-id="943cc-312">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="943cc-313">此处使用 `DeleteAllMessages` 只是为了进行演示，但建议将此类方法命名为 `DeleteAllMessagesAsync`。</span><span class="sxs-lookup"><span data-stu-id="943cc-313">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="943cc-314">它对示例的实现处理没有影响，但使用 `Async` 后缀强调了它是异步方法的事实。</span><span class="sxs-lookup"><span data-stu-id="943cc-314">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="943cc-315">请注意，*Index.cshtml* 中提供的处理程序名称与 `DeleteAllMessages` 和 `DeleteMessageAsync` 处理程序方法相匹配：</span><span class="sxs-lookup"><span data-stu-id="943cc-315">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="943cc-316">为了方便处理程序将 POST 请求与方法进行匹配，`TryParseHandlerMethod` 剔除了处理程序方法名称 `DeleteMessageAsync` 中的 `Async`。</span><span class="sxs-lookup"><span data-stu-id="943cc-316">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="943cc-317">`DeleteMessage` 的 `asp-page-handler` 名称与处理程序方法 `DeleteMessageAsync` 匹配。</span><span class="sxs-lookup"><span data-stu-id="943cc-317">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="943cc-318">MVC 筛选器和页面筛选器 (IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="943cc-318">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="943cc-319">Razor 页面会忽略 MVC [操作筛选器](xref:mvc/controllers/filters#action-filters)，因为 Razor 页面使用处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="943cc-319">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="943cc-320">可使用其他类型的 MVC 筛选器：[授权](xref:mvc/controllers/filters#authorization-filters)、[异常](xref:mvc/controllers/filters#exception-filters)、[资源](xref:mvc/controllers/filters#resource-filters)和[结果](xref:mvc/controllers/filters#result-filters)。</span><span class="sxs-lookup"><span data-stu-id="943cc-320">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="943cc-321">有关详细信息，请参阅[筛选器](xref:mvc/controllers/filters)主题。</span><span class="sxs-lookup"><span data-stu-id="943cc-321">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="943cc-322">页面筛选器 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) 是应用于 Razor 页面的一种筛选器。</span><span class="sxs-lookup"><span data-stu-id="943cc-322">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="943cc-323">有关详细信息，请参阅 [Razor 页面的筛选方法](xref:razor-pages/filter)。</span><span class="sxs-lookup"><span data-stu-id="943cc-323">For more information, see [Filter methods for Razor Pages](xref:razor-pages/filter).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="943cc-324">其他资源</span><span class="sxs-lookup"><span data-stu-id="943cc-324">Additional resources</span></span>

* [<span data-ttu-id="943cc-325">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="943cc-325">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
