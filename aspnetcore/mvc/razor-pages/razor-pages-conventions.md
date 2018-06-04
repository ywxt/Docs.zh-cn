---
title: ASP.NET Core 中 Razor 页面的路由和应用约定
author: guardrex
description: 了解路由和应用模型提供程序约定如何帮助控制页面路由、发现和处理。
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 04/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/razor-pages/razor-pages-conventions
ms.openlocfilehash: eba3422fbf46ac181a783b7f8cc605c2a549b4b7
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729738"
---
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a><span data-ttu-id="75d5f-103">ASP.NET Core 中 Razor 页面的路由和应用约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-103">Razor Pages route and app conventions in ASP.NET Core</span></span>

<span data-ttu-id="75d5f-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="75d5f-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="75d5f-105">了解如何使用[页面路由和应用模型提供程序约定](xref:mvc/controllers/application-model#conventions)来控制 Razor 页面应用中的页面路由、发现和处理。</span><span class="sxs-lookup"><span data-stu-id="75d5f-105">Learn how to use page [route and app model provider conventions](xref:mvc/controllers/application-model#conventions) to control page routing, discovery, and processing in Razor Pages apps.</span></span> <span data-ttu-id="75d5f-106">需要为各个页面配置自定义页面路由时，可使用本主题稍后所述的 [AddPageRoute 约定](#configure-a-page-route)配置页面路由。</span><span class="sxs-lookup"><span data-stu-id="75d5f-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="75d5f-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="75d5f-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range="= aspnetcore-2.0"
| <span data-ttu-id="75d5f-108">方案</span><span class="sxs-lookup"><span data-stu-id="75d5f-108">Scenario</span></span> | <span data-ttu-id="75d5f-109">示例演示...</span><span class="sxs-lookup"><span data-stu-id="75d5f-109">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="75d5f-110">模型约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-110">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="75d5f-111">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="75d5f-111">Conventions.Add</span></span><ul><li><span data-ttu-id="75d5f-112">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-112">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-113">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-113">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="75d5f-114">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-114">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="75d5f-115">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-115">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="75d5f-116">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-116">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-117">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-117">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-118">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="75d5f-118">AddPageRoute</span></span></li></ul> | <span data-ttu-id="75d5f-119">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-119">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="75d5f-120">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-120">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="75d5f-121">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-121">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="75d5f-122">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-122">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="75d5f-123">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="75d5f-123">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="75d5f-124">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-124">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="75d5f-125">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="75d5f-125">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="75d5f-126">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-126">Replace the default page model provider to change the conventions for handler names.</span></span> |
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
| <span data-ttu-id="75d5f-127">方案</span><span class="sxs-lookup"><span data-stu-id="75d5f-127">Scenario</span></span> | <span data-ttu-id="75d5f-128">示例演示...</span><span class="sxs-lookup"><span data-stu-id="75d5f-128">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="75d5f-129">模型约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-129">Model conventions</span></span>](#model-conventions)<br><br><span data-ttu-id="75d5f-130">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="75d5f-130">Conventions.Add</span></span><ul><li><span data-ttu-id="75d5f-131">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-131">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-132">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-132">IPageApplicationModelConvention</span></span></li><li><span data-ttu-id="75d5f-133">IPageHandlerModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-133">IPageHandlerModelConvention</span></span></li></ul> | <span data-ttu-id="75d5f-134">将路由模板和标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-134">Add a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="75d5f-135">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-135">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="75d5f-136">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-136">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-137">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-137">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="75d5f-138">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="75d5f-138">AddPageRoute</span></span></li></ul> | <span data-ttu-id="75d5f-139">将路由模板添加到某个文件夹中的页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-139">Add a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="75d5f-140">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-140">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="75d5f-141">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-141">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="75d5f-142">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="75d5f-142">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="75d5f-143">ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="75d5f-143">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="75d5f-144">将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-144">Add a header to pages in a folder, add a header to a single page, and configure a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="75d5f-145">默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="75d5f-145">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="75d5f-146">取代默认页面模型提供程序，用于更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-146">Replace the default page model provider to change the conventions for handler names.</span></span> |
::: moniker-end

<span data-ttu-id="75d5f-147">使用 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 扩展方法向 `Startup` 类中服务集合的 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) 添加和配置 Razor 页面约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-147">Razor Pages conventions are added and configured using the [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) extension method to [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) on the service collection in the `Startup` class.</span></span> <span data-ttu-id="75d5f-148">本主题稍后会介绍以下约定示例：</span><span class="sxs-lookup"><span data-stu-id="75d5f-148">The following convention examples are explained later in this topic:</span></span>

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

## <a name="model-conventions"></a><span data-ttu-id="75d5f-149">模型约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-149">Model conventions</span></span>

<span data-ttu-id="75d5f-150">为 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 添加委托，以添加应用于 Razor 页面的[模型约定](xref:mvc/controllers/application-model#conventions)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-150">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add [model conventions](xref:mvc/controllers/application-model#conventions) that apply to Razor Pages.</span></span>

<span data-ttu-id="75d5f-151">**将路由模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="75d5f-151">**Add a route model convention to all pages**</span></span>

<span data-ttu-id="75d5f-152">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面路由模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-152">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page route model construction.</span></span>

<span data-ttu-id="75d5f-153">示例应用将 `{globalTemplate?}` 路由模板添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-153">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="75d5f-154">`AttributeRouteModel` 的 `Order` 属性设置为 `-1`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-154">The `Order` property for the `AttributeRouteModel` is set to `-1`.</span></span> <span data-ttu-id="75d5f-155">这确保了当提供单个路由值时，该模板被赋予第一个路由数据值位置的优先级，并且它将优先于自动生成的 Razor 页面路由。</span><span class="sxs-lookup"><span data-stu-id="75d5f-155">This ensures that this template is given priority for the first route data value position when a single route value is provided and also that it would have priority over automatically generated Razor Pages routes.</span></span> <span data-ttu-id="75d5f-156">例如，示例在本主题的后面部分添加了一个 `{aboutTemplate?}` 路由模板。</span><span class="sxs-lookup"><span data-stu-id="75d5f-156">For example, the sample adds an `{aboutTemplate?}` route template later in the topic.</span></span> <span data-ttu-id="75d5f-157">为 `{aboutTemplate?}` 模板指定的 `Order` 为 `1`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-157">The `{aboutTemplate?}` template is given an `Order` of `1`.</span></span> <span data-ttu-id="75d5f-158">当在 `/About/RouteDataValue` 中请求“关于”页面时，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="75d5f-158">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="75d5f-159">将 MVC 添加到 `Startup.ConfigureServices` 中的服务集合时，会添加 Razor 页面选项，例如添加[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-159">Razor Pages options, such as adding [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions), are added when MVC is added to the service collection in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="75d5f-160">有关示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-160">For an example, see the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-conventions/sample/).</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="75d5f-161">在 `localhost:5000/About/GlobalRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-161">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-template.png)

<span data-ttu-id="75d5f-164">**将应用模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="75d5f-164">**Add an app model convention to all pages**</span></span>

<span data-ttu-id="75d5f-165">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面应用模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-165">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page app model construction.</span></span>

<span data-ttu-id="75d5f-166">为了演示此约定以及本主题后面的其他约定，示例应用包含了一个 `AddHeaderAttribute` 类。</span><span class="sxs-lookup"><span data-stu-id="75d5f-166">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="75d5f-167">类构造函数采用 `name` 字符串和 `values` 字符串数组。</span><span class="sxs-lookup"><span data-stu-id="75d5f-167">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="75d5f-168">将在其 `OnResultExecuting` 方法中使用这些值来设置响应标头。</span><span class="sxs-lookup"><span data-stu-id="75d5f-168">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="75d5f-169">本主题后面的[页面模型操作约定](#page-model-action-conventions)部分展示了完整的类。</span><span class="sxs-lookup"><span data-stu-id="75d5f-169">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="75d5f-170">示例应用使用 `AddHeaderAttribute` 类将标头 `GlobalHeader` 添加到应用中的所有页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-170">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="75d5f-171">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="75d5f-171">*Startup.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="75d5f-172">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-172">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 GlobalHeader。](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="75d5f-174">**将处理程序模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="75d5f-174">**Add a handler model convention to all pages**</span></span>

<span data-ttu-id="75d5f-175">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面处理程序模型构造过程中应用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-175">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during page handler model construction.</span></span>

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

<span data-ttu-id="75d5f-176">`Startup.ConfigureServices`：</span><span class="sxs-lookup"><span data-stu-id="75d5f-176">`Startup.ConfigureServices`:</span></span>

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```
::: moniker-end

## <a name="page-route-action-conventions"></a><span data-ttu-id="75d5f-177">页面路由操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-177">Page route action conventions</span></span>

<span data-ttu-id="75d5f-178">默认路由模型提供程序派生自 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)，可调用旨在为页面路由配置提供扩展点的约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-178">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

<span data-ttu-id="75d5f-179">**文件夹路由模型约定**</span><span class="sxs-lookup"><span data-stu-id="75d5f-179">**Folder route model convention**</span></span>

<span data-ttu-id="75d5f-180">使用 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="75d5f-180">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="75d5f-181">示例应用使用 `AddFolderRouteModelConvention` 将 `{otherPagesTemplate?}` 路由模板添加到 *OtherPages* 文件夹中的页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-181">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="75d5f-182">`AttributeRouteModel` 的 `Order` 属性设置为 `1`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-182">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="75d5f-183">这样可确保，当提供单个路由值时，优先将 `{globalTemplate?}` 的模板（已在本主题的前面部分设置）作为第一个路由数据值位置。</span><span class="sxs-lookup"><span data-stu-id="75d5f-183">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="75d5f-184">如果在 `/OtherPages/Page1/RouteDataValue` 中请求 Page1 页面，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="75d5f-184">If the Page1 page is requested at `/OtherPages/Page1/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="75d5f-185">在 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 中请求示例的 Page1 页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-185">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 OtherPagesRouteValue 路由段请求 OtherPages 文件夹中的 Page1。](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

<span data-ttu-id="75d5f-188">**页面路由模型约定**</span><span class="sxs-lookup"><span data-stu-id="75d5f-188">**Page route model convention**</span></span>

<span data-ttu-id="75d5f-189">使用 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为具有指定名称的页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="75d5f-189">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="75d5f-190">示例应用使用 `AddPageRouteModelConvention` 将 `{aboutTemplate?}` 路由模板添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-190">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> <span data-ttu-id="75d5f-191">`AttributeRouteModel` 的 `Order` 属性设置为 `1`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-191">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="75d5f-192">这样可确保，当提供单个路由值时，优先将 `{globalTemplate?}` 的模板（已在本主题的前面部分设置）作为第一个路由数据值位置。</span><span class="sxs-lookup"><span data-stu-id="75d5f-192">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="75d5f-193">如果在 `/About/RouteDataValue` 中请求“关于”页面，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = -1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 1`) 中。</span><span class="sxs-lookup"><span data-stu-id="75d5f-193">If the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = -1`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="75d5f-194">在 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 中请求示例的“关于”页面并检查结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-194">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![使用 GlobalRouteValue 和 AboutRouteValue 路由段请求“关于”页面。](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a><span data-ttu-id="75d5f-197">配置页面路由</span><span class="sxs-lookup"><span data-stu-id="75d5f-197">Configure a page route</span></span>

<span data-ttu-id="75d5f-198">使用 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 配置路由，该路由指向指定页面路径中的页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-198">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="75d5f-199">生成的页面链接使用指定的路由。</span><span class="sxs-lookup"><span data-stu-id="75d5f-199">Generated links to the page use your specified route.</span></span> <span data-ttu-id="75d5f-200">`AddPageRoute` 使用 `AddPageRouteModelConvention` 建立路由。</span><span class="sxs-lookup"><span data-stu-id="75d5f-200">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="75d5f-201">示例应用为 *Contact.cshtml* 创建指向 `/TheContactPage` 的路由：</span><span class="sxs-lookup"><span data-stu-id="75d5f-201">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="75d5f-202">还可在 `/Contact` 中通过默认路由访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-202">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="75d5f-203">示例应用的“联系人”页面自定义路由允许使用可选的 `text` 路由段 (`{text?}`)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-203">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="75d5f-204">该页面还在其 `@page` 指令中包含此可选段，以便访问者在 `/Contact` 路由中访问该页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-204">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="75d5f-205">请注意，在呈现的页面中，为**联系人**链接生成的 URL 反映了已更新的路由：</span><span class="sxs-lookup"><span data-stu-id="75d5f-205">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![导航栏中的示例应用“联系人”链接](razor-pages-conventions/_static/contact-link.png)

![检查呈现的 HTML 中的“联系人”链接，可看到 href 设置为“/TheContactPage”](razor-pages-conventions/_static/contact-link-source.png)

<span data-ttu-id="75d5f-208">在常规路由 `/Contact` 或自定义路由 `/TheContactPage` 中访问“联系人”页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-208">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="75d5f-209">如果提供附加的 `text` 路由段，该页面会显示所提供的 HTML 编码段：</span><span class="sxs-lookup"><span data-stu-id="75d5f-209">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![在 URL 中提供可选“'text”路由段“TextValue”的 Microsoft Edge 浏览器示例。](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="75d5f-212">页面模型操作约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-212">Page model action conventions</span></span>

<span data-ttu-id="75d5f-213">实现 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 的默认页面模型提供程序可调用约定，这些约定旨在为页面模型配置提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="75d5f-213">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="75d5f-214">在生成和修改页面发现及处理方案时，可使用这些约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-214">These conventions are useful when building and modifying page discovery and processing scenarios.</span></span>

<span data-ttu-id="75d5f-215">对于此部分中的示例，示例应用使用 `AddHeaderAttribute` 类（一个 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)）来应用响应标头：</span><span class="sxs-lookup"><span data-stu-id="75d5f-215">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="75d5f-216">示例演示了如何使用约定将该属性应用于某个文件夹中的所有页面以及单个页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-216">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="75d5f-217">**文件夹应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="75d5f-217">**Folder app model convention**</span></span>

<span data-ttu-id="75d5f-218">使用 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 创建并添加 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 实例上的操作。</span><span class="sxs-lookup"><span data-stu-id="75d5f-218">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="75d5f-219">示例演示了如何使用 `AddFolderApplicationModelConvention` 将标头 `OtherPagesHeader` 添加到应用的 *OtherPages* 文件夹内的页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-219">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="75d5f-220">在 `localhost:5000/OtherPages/Page1` 中请求示例的 Page1 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-220">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/Page1 页面的响应标头显示已添加 OtherPagesHeader。](razor-pages-conventions/_static/page1-otherpages-header.png)

<span data-ttu-id="75d5f-222">**页面应用模型约定**</span><span class="sxs-lookup"><span data-stu-id="75d5f-222">**Page app model convention**</span></span>

<span data-ttu-id="75d5f-223">使用 [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) 创建并添加 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)，后者可以为具有指定名称的页面调用 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 上的操作。</span><span class="sxs-lookup"><span data-stu-id="75d5f-223">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the speciifed name.</span></span>

<span data-ttu-id="75d5f-224">示例演示了如何使用 `AddPageApplicationModelConvention` 将标头 `AboutHeader` 添加到“关于”页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-224">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="75d5f-225">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-225">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加 AboutHeader。](razor-pages-conventions/_static/about-page-about-header.png)

<span data-ttu-id="75d5f-227">**配置筛选器**</span><span class="sxs-lookup"><span data-stu-id="75d5f-227">**Configure a filter**</span></span>

<span data-ttu-id="75d5f-228">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 可配置要应用的指定筛选器。</span><span class="sxs-lookup"><span data-stu-id="75d5f-228">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="75d5f-229">用户可以实现筛选器类，但示例应用演示了如何在 Lambda 表达式中实现筛选器，该筛选器在后台作为可返回筛选器的工厂实现：</span><span class="sxs-lookup"><span data-stu-id="75d5f-229">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="75d5f-230">页面应用模型用于检查指向 *OtherPages* 文件夹中 Page2 页面的段的相对路径。</span><span class="sxs-lookup"><span data-stu-id="75d5f-230">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="75d5f-231">如果条件通过，则添加标头。</span><span class="sxs-lookup"><span data-stu-id="75d5f-231">If the condition passes, a header is added.</span></span> <span data-ttu-id="75d5f-232">如果不通过，则应用 `EmptyFilter`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-232">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="75d5f-233">`EmptyFilter` 是一种[操作筛选器](xref:mvc/controllers/filters#action-filters)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-233">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="75d5f-234">由于 Razor 页面会忽略操作筛选器，因此，如果路径不包含 `OtherPages/Page2`，`EmptyFilter` 会按预期发出空操作指令。</span><span class="sxs-lookup"><span data-stu-id="75d5f-234">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="75d5f-235">在 `localhost:5000/OtherPages/Page2` 中请求示例的 Page2 页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-235">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header 已添加到 Page2 的响应。](razor-pages-conventions/_static/page2-filter-header.png)

<span data-ttu-id="75d5f-237">**配置筛选器工厂**</span><span class="sxs-lookup"><span data-stu-id="75d5f-237">**Configure a filter factory**</span></span>

<span data-ttu-id="75d5f-238">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 可配置指定的工厂，以将[筛选器](xref:mvc/controllers/filters)应用于所有 Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="75d5f-238">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="75d5f-239">示例应用提供了一个示例，说明如何使用[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)将具有两个值的标头 `FilterFactoryHeader` 添加到应用的页面：</span><span class="sxs-lookup"><span data-stu-id="75d5f-239">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="75d5f-240">*AddHeaderWithFactory.cs*：</span><span class="sxs-lookup"><span data-stu-id="75d5f-240">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="75d5f-241">在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：</span><span class="sxs-lookup"><span data-stu-id="75d5f-241">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![“关于”页面的响应标头显示已添加两个 FilterFactoryHeader 标头。](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="75d5f-243">替换默认页面应用模型提供程序</span><span class="sxs-lookup"><span data-stu-id="75d5f-243">Replace the default page app model provider</span></span>

<span data-ttu-id="75d5f-244">Razor 页面使用 `IPageApplicationModelProvider` 接口创建 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-244">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="75d5f-245">用户可以从默认模型提供程序继承，以便为处理程序发现和处理提供自己的实现逻辑。</span><span class="sxs-lookup"><span data-stu-id="75d5f-245">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="75d5f-246">默认实现（[引用源](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)）为*未命名*和*已命名*处理程序的命名建立了约定，如下所述。</span><span class="sxs-lookup"><span data-stu-id="75d5f-246">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="75d5f-247">**默认的未命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="75d5f-247">**Default unnamed handler methods**</span></span>

<span data-ttu-id="75d5f-248">Http 谓词的处理程序方法（“未命名”的处理程序方法）遵循以下约定：`On<HTTP verb>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="75d5f-248">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="75d5f-249">未命名处理程序方法</span><span class="sxs-lookup"><span data-stu-id="75d5f-249">Unnamed handler method</span></span>     | <span data-ttu-id="75d5f-250">操作</span><span class="sxs-lookup"><span data-stu-id="75d5f-250">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="75d5f-251">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="75d5f-251">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="75d5f-252">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="75d5f-252">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="75d5f-253">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-253">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="75d5f-254">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-254">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="75d5f-255">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-255">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="75d5f-256">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-256">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="75d5f-257">**默认的已命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="75d5f-257">**Default named handler methods**</span></span>

<span data-ttu-id="75d5f-258">由开发人员提供的处理程序方法（“已命名”的处理程序方法）遵循类似的约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-258">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="75d5f-259">处理程序名称出现在 Http 谓词之后或者 Http 谓词与 `Async` 之间：`On<HTTP verb><handler name>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="75d5f-259">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="75d5f-260">例如，用于处理消息的方法可能采用下表所示的命名。</span><span class="sxs-lookup"><span data-stu-id="75d5f-260">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="75d5f-261">已命名处理程序方法示例</span><span class="sxs-lookup"><span data-stu-id="75d5f-261">Example named handler method</span></span>             | <span data-ttu-id="75d5f-262">操作示例</span><span class="sxs-lookup"><span data-stu-id="75d5f-262">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="75d5f-263">获取消息。</span><span class="sxs-lookup"><span data-stu-id="75d5f-263">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="75d5f-264">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="75d5f-264">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="75d5f-265">DELETE 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-265">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="75d5f-266">PUT 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-266">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="75d5f-267">PATCH 消息&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-267">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="75d5f-268">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-268">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="75d5f-269">**自定义处理程序方法名称**</span><span class="sxs-lookup"><span data-stu-id="75d5f-269">**Customize handler method names**</span></span>

<span data-ttu-id="75d5f-270">假设用户想更改未命名和已命名处理程序方法的命名方式。</span><span class="sxs-lookup"><span data-stu-id="75d5f-270">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="75d5f-271">备选命名方案是避免让方法名称以“On”开头，并使用第一个分词来确定 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="75d5f-271">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="75d5f-272">也可以进行其他更改，比如将 DELETE、PUT 和 PATCH 的谓词转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="75d5f-272">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="75d5f-273">这种方案提供下表所示的方法名称。</span><span class="sxs-lookup"><span data-stu-id="75d5f-273">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="75d5f-274">处理程序方法</span><span class="sxs-lookup"><span data-stu-id="75d5f-274">Handler method</span></span>                       | <span data-ttu-id="75d5f-275">操作</span><span class="sxs-lookup"><span data-stu-id="75d5f-275">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="75d5f-276">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="75d5f-276">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="75d5f-277">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="75d5f-277">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="75d5f-278">处理 DELETE 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-278">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="75d5f-279">处理 PUT 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-279">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="75d5f-280">处理 PATCH 请求&#8224;。</span><span class="sxs-lookup"><span data-stu-id="75d5f-280">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="75d5f-281">获取消息。</span><span class="sxs-lookup"><span data-stu-id="75d5f-281">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="75d5f-282">POST 消息。</span><span class="sxs-lookup"><span data-stu-id="75d5f-282">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="75d5f-283">POST 消息以进行删除。</span><span class="sxs-lookup"><span data-stu-id="75d5f-283">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="75d5f-284">POST 消息以进行放置。</span><span class="sxs-lookup"><span data-stu-id="75d5f-284">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="75d5f-285">POST 消息以进行修补。</span><span class="sxs-lookup"><span data-stu-id="75d5f-285">POST a message to patch.</span></span>       |

<span data-ttu-id="75d5f-286">&#8224;用于向页面发出 API 调用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-286">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="75d5f-287">若要建立此方案，请从 `DefaultPageApplicationModelProvider` 类继承并重写 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 方法，以提供自定义逻辑来解析 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 处理程序名称。</span><span class="sxs-lookup"><span data-stu-id="75d5f-287">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="75d5f-288">示例应用展示了如何在其 `CustomPageApplicationModelProvider` 类中执行此操作：</span><span class="sxs-lookup"><span data-stu-id="75d5f-288">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="75d5f-289">该类的要点包括：</span><span class="sxs-lookup"><span data-stu-id="75d5f-289">Highlights of the class include:</span></span>

* <span data-ttu-id="75d5f-290">该类继承自 `DefaultPageApplicationModelProvider`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-290">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="75d5f-291">`TryParseHandlerMethod` 对处理程序进行处理，以便在创建 `PageHandlerModel` 时确定 Http 谓词 (`httpMethod`) 和已命名处理程序名称 (`handlerName`)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-291">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="75d5f-292">忽略 `Async` 后缀（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="75d5f-292">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="75d5f-293">使用大小写分析方法名称中的 Http 谓词。</span><span class="sxs-lookup"><span data-stu-id="75d5f-293">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="75d5f-294">当方法名称（不带 `Async`）与 Http 谓词名称相同时，就不存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="75d5f-294">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="75d5f-295">`handlerName` 设置为 `null`，且方法名称为 `Get`、`Post`、`Delete`、`Put` 或 `Patch`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-295">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="75d5f-296">当方法名称（不带 `Async`）的长度超过 Http 谓词名称时，就存在已命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="75d5f-296">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="75d5f-297">`handlerName` 设置为 `<method name (less 'Async', if present)>`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-297">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="75d5f-298">例如，“GetMessage”和“GetMessageAsync”都生成处理程序名称“GetMessage”。</span><span class="sxs-lookup"><span data-stu-id="75d5f-298">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="75d5f-299">DELETE、PUT 和 PATCH Http 谓词都转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="75d5f-299">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="75d5f-300">在 `Startup` 类中注册 `CustomPageApplicationModelProvider`：</span><span class="sxs-lookup"><span data-stu-id="75d5f-300">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="75d5f-301">*Index.cshtml.cs* 中的页面模型演示了如何针对应用中的页面更改常规的处理程序方法命名约定。</span><span class="sxs-lookup"><span data-stu-id="75d5f-301">The page model in *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="75d5f-302">用于 Razor 页面的常规“On”前缀命名已被删除。</span><span class="sxs-lookup"><span data-stu-id="75d5f-302">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="75d5f-303">用于初始化页面状态的方法现在命名为 `Get`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-303">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="75d5f-304">为任何页面打开任何页面模型时，都可以看到此约定贯穿于整个应用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-304">You can see this convention used throughout the app if you open any page model for any of the pages.</span></span>

<span data-ttu-id="75d5f-305">其他各个方法均以描述其处理的 Http 谓词开头。</span><span class="sxs-lookup"><span data-stu-id="75d5f-305">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="75d5f-306">以 `Delete` 开头的两个方法通常被视为 DELETE Http 谓词，但 `TryParseHandlerMethod` 中的逻辑会针对这两种处理程序将该谓词显式设置为 POST。</span><span class="sxs-lookup"><span data-stu-id="75d5f-306">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="75d5f-307">请注意，`Async` 在 `DeleteAllMessages` 和 `DeleteMessageAsync` 之间是可选的。</span><span class="sxs-lookup"><span data-stu-id="75d5f-307">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="75d5f-308">它们都是异步方法，但用户可以选择是否使用 `Async` 后缀；我们建议使用。</span><span class="sxs-lookup"><span data-stu-id="75d5f-308">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="75d5f-309">此处使用 `DeleteAllMessages` 只是为了进行演示，但建议将此类方法命名为 `DeleteAllMessagesAsync`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-309">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="75d5f-310">它对示例的实现处理没有影响，但使用 `Async` 后缀强调了它是异步方法的事实。</span><span class="sxs-lookup"><span data-stu-id="75d5f-310">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="75d5f-311">请注意，*Index.cshtml* 中提供的处理程序名称与 `DeleteAllMessages` 和 `DeleteMessageAsync` 处理程序方法相匹配：</span><span class="sxs-lookup"><span data-stu-id="75d5f-311">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="75d5f-312">为了方便处理程序将 POST 请求与方法进行匹配，`TryParseHandlerMethod` 剔除了处理程序方法名称 `DeleteMessageAsync` 中的 `Async`。</span><span class="sxs-lookup"><span data-stu-id="75d5f-312">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="75d5f-313">`DeleteMessage` 的 `asp-page-handler` 名称与处理程序方法 `DeleteMessageAsync` 匹配。</span><span class="sxs-lookup"><span data-stu-id="75d5f-313">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="75d5f-314">MVC 筛选器和页面筛选器 (IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="75d5f-314">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="75d5f-315">Razor 页面会忽略 MVC [操作筛选器](xref:mvc/controllers/filters#action-filters)，因为 Razor 页面使用处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="75d5f-315">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="75d5f-316">可使用其他类型的 MVC 筛选器：[授权](xref:mvc/controllers/filters#authorization-filters)、[异常](xref:mvc/controllers/filters#exception-filters)、[资源](xref:mvc/controllers/filters#resource-filters)和[结果](xref:mvc/controllers/filters#result-filters)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-316">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="75d5f-317">有关详细信息，请参阅[筛选器](xref:mvc/controllers/filters)主题。</span><span class="sxs-lookup"><span data-stu-id="75d5f-317">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="75d5f-318">页面筛选器 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) 是应用于 Razor 页面的一种筛选器。</span><span class="sxs-lookup"><span data-stu-id="75d5f-318">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="75d5f-319">有关详细信息，请参阅 [Razor 页面的筛选方法](xref:mvc/razor-pages/filter)。</span><span class="sxs-lookup"><span data-stu-id="75d5f-319">For more information, see [Filter methods for Razor Pages](xref:mvc/razor-pages/filter).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75d5f-320">其他资源</span><span class="sxs-lookup"><span data-stu-id="75d5f-320">Additional resources</span></span>

* [<span data-ttu-id="75d5f-321">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="75d5f-321">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
