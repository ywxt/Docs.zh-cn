---
title: "Razor 页路由和应用程序中 ASP.NET Core 的约定功能"
author: guardrex
description: "发现如何路由和应用程序模型提供程序约定功能帮助你控制页路由、 发现和处理。"
ms.author: riande
manager: wpickett
ms.date: 10/23/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/razor-pages-convention-features
ms.openlocfilehash: 69475ca9abd4e732dc704ad6a8a2fffe219984f7
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="razor-pages-route-and-app-convention-features-in-aspnet-core"></a><span data-ttu-id="144df-103">Razor 页路由和应用程序中 ASP.NET Core 的约定功能</span><span class="sxs-lookup"><span data-stu-id="144df-103">Razor Pages route and app convention features in ASP.NET Core</span></span>

<span data-ttu-id="144df-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="144df-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="144df-105">了解如何使用页路由和应用程序模型提供程序约定功能来控制页路由、 发现和 Razor 页应用中的处理。</span><span class="sxs-lookup"><span data-stu-id="144df-105">Learn how to use page route and app model provider convention features to control page routing, discovery, and processing in Razor Pages apps.</span></span> <span data-ttu-id="144df-106">当你需要进行自定义页为配置路由各个页时，配置路由至页面[AddPageRoute 约定](#configure-a-page-route)本主题稍后所述。</span><span class="sxs-lookup"><span data-stu-id="144df-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="144df-107">使用[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample)([如何下载](xref:tutorials/index#how-to-download-a-sample)) 来浏览本主题中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="144df-107">Use the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

| <span data-ttu-id="144df-108">功能</span><span class="sxs-lookup"><span data-stu-id="144df-108">Features</span></span> | <span data-ttu-id="144df-109">此示例演示如何...</span><span class="sxs-lookup"><span data-stu-id="144df-109">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="144df-110">路由和应用程序模型约定</span><span class="sxs-lookup"><span data-stu-id="144df-110">Route and app model conventions</span></span>](#add-route-and-app-model-conventions)<br><br><span data-ttu-id="144df-111">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="144df-111">Conventions.Add</span></span><ul><li><span data-ttu-id="144df-112">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-112">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="144df-113">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-113">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="144df-114">将路由模板和标头添加到应用程序的页面。</span><span class="sxs-lookup"><span data-stu-id="144df-114">Adding a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="144df-115">页路由操作约定</span><span class="sxs-lookup"><span data-stu-id="144df-115">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="144df-116">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-116">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="144df-117">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-117">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="144df-118">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="144df-118">AddPageRoute</span></span></li></ul> | <span data-ttu-id="144df-119">将路由模板添加到文件夹中的页和单个页面。</span><span class="sxs-lookup"><span data-stu-id="144df-119">Adding a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="144df-120">页模型操作约定</span><span class="sxs-lookup"><span data-stu-id="144df-120">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="144df-121">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-121">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="144df-122">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="144df-122">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="144df-123">ConfigureFilter （筛选器类、 lambda 表达式或筛选器工厂）</span><span class="sxs-lookup"><span data-stu-id="144df-123">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="144df-124">将一个标头添加到文件夹中的页，将一个标头添加到单个页面，和配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)将标头添加到应用程序的页面。</span><span class="sxs-lookup"><span data-stu-id="144df-124">Adding a header to pages in a folder, adding a header to a single page, and configuring a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="144df-125">默认页应用程序模型提供程序</span><span class="sxs-lookup"><span data-stu-id="144df-125">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="144df-126">替换默认页模型提供程序来更改处理程序命名约定。</span><span class="sxs-lookup"><span data-stu-id="144df-126">Replacing the default page model provider to change the conventions for handler naming.</span></span> |

## <a name="add-route-and-app-model-conventions"></a><span data-ttu-id="144df-127">添加路由和应用程序模型约定</span><span class="sxs-lookup"><span data-stu-id="144df-127">Add route and app model conventions</span></span>

<span data-ttu-id="144df-128">添加的委托[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)添加路由和应用程序将应用于 Razor 页面的模型约定。</span><span class="sxs-lookup"><span data-stu-id="144df-128">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add route and app model conventions that apply to Razor Pages.</span></span>

<span data-ttu-id="144df-129">**将路由模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="144df-129">**Add a route model convention to all pages**</span></span>

<span data-ttu-id="144df-130">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建并添加[IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)到的集合[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)在路由和页模型过程中应用的实例构造。</span><span class="sxs-lookup"><span data-stu-id="144df-130">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="144df-131">示例应用添加`{globalTemplate?}`到所有应用程序中的页的路由模板：</span><span class="sxs-lookup"><span data-stu-id="144df-131">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="144df-132">`Order`属性`AttributeRouteModel`设置为`0`（零）。</span><span class="sxs-lookup"><span data-stu-id="144df-132">The `Order` property for the `AttributeRouteModel` is set to `0` (zero).</span></span> <span data-ttu-id="144df-133">这可确保提供了一个路由值时，指定此模板的第一个路由数据值位置的优先级。</span><span class="sxs-lookup"><span data-stu-id="144df-133">This ensures that this template is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="144df-134">例如，此示例将添加`{aboutTemplate?}`在本主题后面的路由模板。</span><span class="sxs-lookup"><span data-stu-id="144df-134">For example, the sample adds an `{aboutTemplate?}` route template later in the topic.</span></span> <span data-ttu-id="144df-135">`{aboutTemplate?}`模板提供`Order`的`1`。</span><span class="sxs-lookup"><span data-stu-id="144df-135">The `{aboutTemplate?}` template is given an `Order` of `1`.</span></span> <span data-ttu-id="144df-136">关于页面上的请求时`/About/RouteDataValue`，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 0`) 而不`RouteData.Values["aboutTemplate"]`(`Order = 1`) 由于设置`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="144df-136">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="144df-137">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="144df-137">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="144df-138">请求在示例的有关页`localhost:5000/About/GlobalRouteValue`并检查结果：</span><span class="sxs-lookup"><span data-stu-id="144df-138">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![关于页面，其中使用 GlobalRouteValue 路由段请求。](razor-pages-convention-features/_static/about-page-global-template.png)

<span data-ttu-id="144df-141">**将应用程序模型约定添加到所有页面**</span><span class="sxs-lookup"><span data-stu-id="144df-141">**Add an app model convention to all pages**</span></span>

<span data-ttu-id="144df-142">使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)到的集合[IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention)在路由和页过程中应用的实例模型构建。</span><span class="sxs-lookup"><span data-stu-id="144df-142">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="144df-143">为了演示这和在本主题后面的其他约定，示例应用程序包括`AddHeaderAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="144df-143">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="144df-144">类构造函数接受`name`字符串和`values`字符串数组。</span><span class="sxs-lookup"><span data-stu-id="144df-144">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="144df-145">在使用这些值其`OnResultExecuting`方法以设置响应标头。</span><span class="sxs-lookup"><span data-stu-id="144df-145">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="144df-146">完整类所示[页上模型操作约定](#page-model-action-conventions)在本主题后面的部分。</span><span class="sxs-lookup"><span data-stu-id="144df-146">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="144df-147">此示例应用程序使用`AddHeaderAttribute`类添加标头， `GlobalHeader`，对所有应用程序中的页：</span><span class="sxs-lookup"><span data-stu-id="144df-147">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="144df-148">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="144df-148">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="144df-149">请求在示例的有关页`localhost:5000/About`并检查要查看的结果的标头：</span><span class="sxs-lookup"><span data-stu-id="144df-149">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![响应标头的关于页面显示 GlobalHeader 验证已添加。](razor-pages-convention-features/_static/about-page-global-header.png)

## <a name="page-route-action-conventions"></a><span data-ttu-id="144df-151">页路由操作约定</span><span class="sxs-lookup"><span data-stu-id="144df-151">Page route action conventions</span></span>

<span data-ttu-id="144df-152">默认路由模型提供程序派生自[IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)调用约定，它们可为配置页的路由提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="144df-152">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

<span data-ttu-id="144df-153">**文件夹路由模型的约定**</span><span class="sxs-lookup"><span data-stu-id="144df-153">**Folder route model convention**</span></span>

<span data-ttu-id="144df-154">使用[AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention)创建并添加[IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) ，它在调用操作[PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)下的页面的所有指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="144df-154">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="144df-155">此示例应用程序使用`AddFolderRouteModelConvention`添加`{otherPagesTemplate?}`路由模板中的页*OtherPages*文件夹：</span><span class="sxs-lookup"><span data-stu-id="144df-155">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="144df-156">`Order`属性`AttributeRouteModel`设置为`1`。</span><span class="sxs-lookup"><span data-stu-id="144df-156">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="144df-157">这就保证了模板`{globalTemplate?}`（在本主题中前面设置） 分配的优先级为第一个路由数据值位置时提供一个路由值。</span><span class="sxs-lookup"><span data-stu-id="144df-157">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="144df-158">如果在请求页 1 该页`/OtherPages/Page1/RouteDataValue`，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 0`) 而不`RouteData.Values["otherPagesTemplate"]`(`Order = 1`) 由于设置`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="144df-158">If the Page1 page is requested at `/OtherPages/Page1/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="144df-159">请求的示例页 1 页在`localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue`并检查结果：</span><span class="sxs-lookup"><span data-stu-id="144df-159">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![带 GlobalRouteValue 和 OtherPagesRouteValue 路由段请求页 1 OtherPages 文件夹中。](razor-pages-convention-features/_static/otherpages-page1-global-and-otherpages-templates.png)

<span data-ttu-id="144df-162">**页路由模型的约定**</span><span class="sxs-lookup"><span data-stu-id="144df-162">**Page route model convention**</span></span>

<span data-ttu-id="144df-163">使用[AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention)创建并添加[IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) ，它在调用操作[PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel)具有指定页名称。</span><span class="sxs-lookup"><span data-stu-id="144df-163">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="144df-164">此示例应用程序使用`AddPageRouteModelConvention`添加`{aboutTemplate?}`路由到关于页面的模板：</span><span class="sxs-lookup"><span data-stu-id="144df-164">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> <span data-ttu-id="144df-165">`Order`属性`AttributeRouteModel`设置为`1`。</span><span class="sxs-lookup"><span data-stu-id="144df-165">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="144df-166">这就保证了模板`{globalTemplate?}`（在本主题中前面设置） 分配的优先级为第一个路由数据值位置时提供一个路由值。</span><span class="sxs-lookup"><span data-stu-id="144df-166">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="144df-167">如果关于页面请求在`/About/RouteDataValue`，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 0`) 而不`RouteData.Values["aboutTemplate"]`(`Order = 1`) 由于设置`Order`属性。</span><span class="sxs-lookup"><span data-stu-id="144df-167">If the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="144df-168">请求在示例的有关页`localhost:5000/About/GlobalRouteValue/AboutRouteValue`并检查结果：</span><span class="sxs-lookup"><span data-stu-id="144df-168">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![有关页面请求路由段 GlobalRouteValue 和 AboutRouteValue。](razor-pages-convention-features/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a><span data-ttu-id="144df-171">配置页路由</span><span class="sxs-lookup"><span data-stu-id="144df-171">Configure a page route</span></span>

<span data-ttu-id="144df-172">使用[AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute)若要配置路由到页上，在指定的页面的路径。</span><span class="sxs-lookup"><span data-stu-id="144df-172">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="144df-173">生成的链接到的页面使用你指定的路由。</span><span class="sxs-lookup"><span data-stu-id="144df-173">Generated links to the page use your specified route.</span></span> <span data-ttu-id="144df-174">`AddPageRoute`使用`AddPageRouteModelConvention`来建立路由。</span><span class="sxs-lookup"><span data-stu-id="144df-174">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="144df-175">示例应用程序创建的路由`/TheContactPage`为*Contact.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="144df-175">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="144df-176">在也能访问的联系人页`/Contact`通过其默认路由。</span><span class="sxs-lookup"><span data-stu-id="144df-176">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="144df-177">示例应用程序的自定义路由到联系人页面允许为可选`text`路由段 (`{text?}`)。</span><span class="sxs-lookup"><span data-stu-id="144df-177">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="144df-178">该页面还包括在此可选段其`@page`以防在距访客访问第一页的指令其`/Contact`路由：</span><span class="sxs-lookup"><span data-stu-id="144df-178">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="144df-179">请注意，URL 为生成**联系人**中呈现的页面的链接反映更新的路由：</span><span class="sxs-lookup"><span data-stu-id="144df-179">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![在导航栏中的示例应用联系人链接](razor-pages-convention-features/_static/contact-link.png)

![检查呈现的 HTML 中的联系人链接指示 href 是否设置为 / TheContactPage](razor-pages-convention-features/_static/contact-link-source.png)

<span data-ttu-id="144df-182">请在联系人页访问其普通的路由， `/Contact`，或自定义路由， `/TheContactPage`。</span><span class="sxs-lookup"><span data-stu-id="144df-182">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="144df-183">如果你提供附加`text`路由段，该页面显示的 HTML 编码的段，你提供：</span><span class="sxs-lookup"><span data-stu-id="144df-183">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![提供的 URL 中的 TextValue 可选 'text' 路由段的边缘浏览器示例。](razor-pages-convention-features/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="144df-186">页模型操作约定</span><span class="sxs-lookup"><span data-stu-id="144df-186">Page model action conventions</span></span>

<span data-ttu-id="144df-187">默认页模型实现的提供程序[IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider)调用约定，它们可用于配置页模型提供扩展点。</span><span class="sxs-lookup"><span data-stu-id="144df-187">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="144df-188">这些约定可在生成和修改页发现和处理功能时。</span><span class="sxs-lookup"><span data-stu-id="144df-188">These conventions are useful when building and modifying page discovery and processing features.</span></span>

<span data-ttu-id="144df-189">本部分中的示例，示例应用使用`AddHeaderAttribute`类，该类是[ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)，，它将应用的响应标头：</span><span class="sxs-lookup"><span data-stu-id="144df-189">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="144df-190">使用约定，此示例演示如何将该属性应用到所有文件夹中的网页和单个页面。</span><span class="sxs-lookup"><span data-stu-id="144df-190">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="144df-191">**文件夹应用模型的约定**</span><span class="sxs-lookup"><span data-stu-id="144df-191">**Folder app model convention**</span></span>

<span data-ttu-id="144df-192">使用[AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) ，它在调用操作[PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)的实例指定的文件夹下的所有页面。</span><span class="sxs-lookup"><span data-stu-id="144df-192">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="144df-193">此示例演示如何使用`AddFolderApplicationModelConvention`通过添加标头， `OtherPagesHeader`，到内的页面具有*OtherPages*的应用程序的文件夹：</span><span class="sxs-lookup"><span data-stu-id="144df-193">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="144df-194">请求的示例页 1 页在`localhost:5000/OtherPages/Page1`并检查要查看的结果的标头：</span><span class="sxs-lookup"><span data-stu-id="144df-194">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![OtherPages/页 1 页的响应标头显示 OtherPagesHeader 验证已添加。](razor-pages-convention-features/_static/page1-otherpages-header.png)

<span data-ttu-id="144df-196">**页应用模型的约定**</span><span class="sxs-lookup"><span data-stu-id="144df-196">**Page app model convention**</span></span>

<span data-ttu-id="144df-197">使用[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) ，它在调用操作[PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)页speciifed 同名。</span><span class="sxs-lookup"><span data-stu-id="144df-197">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the speciifed name.</span></span>

<span data-ttu-id="144df-198">此示例演示如何使用`AddPageApplicationModelConvention`通过添加标头， `AboutHeader`，到关于页面：</span><span class="sxs-lookup"><span data-stu-id="144df-198">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="144df-199">请求在示例的有关页`localhost:5000/About`并检查要查看的结果的标头：</span><span class="sxs-lookup"><span data-stu-id="144df-199">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![响应标头的关于页面显示 AboutHeader 验证已添加。](razor-pages-convention-features/_static/about-page-about-header.png)

<span data-ttu-id="144df-201">**配置一个筛选器**</span><span class="sxs-lookup"><span data-stu-id="144df-201">**Configure a filter**</span></span>

<span data-ttu-id="144df-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter)配置指定的筛选器应用。</span><span class="sxs-lookup"><span data-stu-id="144df-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="144df-203">你可以实现的筛选器类，但示例应用演示如何实现在 lambda 表达式中，实现幕后作为一个工厂，它返回的筛选器的筛选器：</span><span class="sxs-lookup"><span data-stu-id="144df-203">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="144df-204">页应用模型用于检查导致的 Page2 页中的段的相对路径*OtherPages*文件夹。</span><span class="sxs-lookup"><span data-stu-id="144df-204">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="144df-205">如果条件通过，添加标头。</span><span class="sxs-lookup"><span data-stu-id="144df-205">If the condition passes, a header is added.</span></span> <span data-ttu-id="144df-206">如果没有，则`EmptyFilter`应用。</span><span class="sxs-lookup"><span data-stu-id="144df-206">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="144df-207">`EmptyFilter`是[操作筛选器](xref:mvc/controllers/filters#action-filters)。</span><span class="sxs-lookup"><span data-stu-id="144df-207">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="144df-208">由于操作筛选器将忽略由 Razor 页`EmptyFilter`否 ops 按预期的路径不包含`OtherPages/Page2`。</span><span class="sxs-lookup"><span data-stu-id="144df-208">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="144df-209">请求在示例的 Page2 页`localhost:5000/OtherPages/Page2`并检查要查看的结果的标头：</span><span class="sxs-lookup"><span data-stu-id="144df-209">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![Page2 的情况下，OtherPagesPage2Header 添加到的响应。](razor-pages-convention-features/_static/page2-filter-header.png)

<span data-ttu-id="144df-211">**配置筛选器工厂**</span><span class="sxs-lookup"><span data-stu-id="144df-211">**Configure a filter factory**</span></span>

<span data-ttu-id="144df-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__)配置用于应用的指定的工厂[筛选器](xref:mvc/controllers/filters)到 Razor 的所有页面。</span><span class="sxs-lookup"><span data-stu-id="144df-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="144df-213">示例应用程序提供使用的示例[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)通过添加标头， `FilterFactoryHeader`，具有到应用程序的页面的两个值：</span><span class="sxs-lookup"><span data-stu-id="144df-213">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="144df-214">*AddHeaderWithFactory.cs*:</span><span class="sxs-lookup"><span data-stu-id="144df-214">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="144df-215">请求在示例的有关页`localhost:5000/About`并检查要查看的结果的标头：</span><span class="sxs-lookup"><span data-stu-id="144df-215">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![响应标头的关于页面显示已添加了两个 FilterFactoryHeader 标头。](razor-pages-convention-features/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="144df-217">替换默认页应用程序模型提供程序</span><span class="sxs-lookup"><span data-stu-id="144df-217">Replace the default page app model provider</span></span>

<span data-ttu-id="144df-218">使用 razor 页`IPageApplicationModelProvider`接口可创建[DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)。</span><span class="sxs-lookup"><span data-stu-id="144df-218">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="144df-219">你可以从默认的模型提供程序，以提供您自己的实现逻辑处理程序发现和处理继承。</span><span class="sxs-lookup"><span data-stu-id="144df-219">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="144df-220">默认实现 ([引用源](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) 建立约定*未命名*和*名为*命名，即下面所述的处理程序。</span><span class="sxs-lookup"><span data-stu-id="144df-220">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="144df-221">**默认未命名的处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="144df-221">**Default unnamed handler methods**</span></span>

<span data-ttu-id="144df-222">HTTP 谓词 （"未命名的"处理程序方法） 的处理程序方法都遵循约定： `On<HTTP verb>[Async]` (追加`Async`是可选但建议的异步方法)。</span><span class="sxs-lookup"><span data-stu-id="144df-222">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="144df-223">未命名的处理程序方法</span><span class="sxs-lookup"><span data-stu-id="144df-223">Unnamed handler method</span></span>     | <span data-ttu-id="144df-224">操作</span><span class="sxs-lookup"><span data-stu-id="144df-224">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="144df-225">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="144df-225">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="144df-226">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="144df-226">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="144df-227">句柄删除请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-227">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="144df-228">句柄 PUT 请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-228">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="144df-229">句柄 PATCH 请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-229">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="144df-230">&#8224;用于进行到页面的 API 调用。</span><span class="sxs-lookup"><span data-stu-id="144df-230">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="144df-231">**默认命名处理程序方法**</span><span class="sxs-lookup"><span data-stu-id="144df-231">**Default named handler methods**</span></span>

<span data-ttu-id="144df-232">提供由开发人员 （"名为"处理程序方法） 的处理程序方法遵循类似的约定。</span><span class="sxs-lookup"><span data-stu-id="144df-232">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="144df-233">处理程序名称出现的 HTTP 谓词之后或之间的 HTTP 谓词和`Async`: `On<HTTP verb><handler name>[Async]` (追加`Async`是可选但建议的异步方法)。</span><span class="sxs-lookup"><span data-stu-id="144df-233">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="144df-234">例如，处理消息的方法可能需要命名下表中所示。</span><span class="sxs-lookup"><span data-stu-id="144df-234">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="144df-235">名为处理程序方法的示例</span><span class="sxs-lookup"><span data-stu-id="144df-235">Example named handler method</span></span>             | <span data-ttu-id="144df-236">示例操作</span><span class="sxs-lookup"><span data-stu-id="144df-236">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="144df-237">获取一条消息。</span><span class="sxs-lookup"><span data-stu-id="144df-237">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="144df-238">将消息发送。</span><span class="sxs-lookup"><span data-stu-id="144df-238">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="144df-239">删除一条消息 （&） #8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-239">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="144df-240">将一条消息 （&） #8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-240">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="144df-241">一条消息 （&） #8224; 的修补程序。</span><span class="sxs-lookup"><span data-stu-id="144df-241">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="144df-242">&#8224;用于进行到页面的 API 调用。</span><span class="sxs-lookup"><span data-stu-id="144df-242">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="144df-243">**自定义处理程序方法的名称**</span><span class="sxs-lookup"><span data-stu-id="144df-243">**Customize handler method names**</span></span>

<span data-ttu-id="144df-244">假定您希望更改命名未命名和命名处理程序方法的方式。</span><span class="sxs-lookup"><span data-stu-id="144df-244">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="144df-245">可选的命名方案是避免启动与"On"的方法名称，并使用的第一个 word 段来确定的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="144df-245">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="144df-246">你可以进行其他更改，例如为删除，将转换谓词，PUT 和 POST 到修补程序。</span><span class="sxs-lookup"><span data-stu-id="144df-246">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="144df-247">这种方案提供下表中所示的方法名称。</span><span class="sxs-lookup"><span data-stu-id="144df-247">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="144df-248">处理程序方法</span><span class="sxs-lookup"><span data-stu-id="144df-248">Handler method</span></span>                       | <span data-ttu-id="144df-249">操作</span><span class="sxs-lookup"><span data-stu-id="144df-249">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="144df-250">初始化页面状态。</span><span class="sxs-lookup"><span data-stu-id="144df-250">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="144df-251">处理 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="144df-251">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="144df-252">句柄删除请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-252">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="144df-253">句柄 PUT 请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-253">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="144df-254">句柄 PATCH 请求 （&#8224;。</span><span class="sxs-lookup"><span data-stu-id="144df-254">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="144df-255">获取一条消息。</span><span class="sxs-lookup"><span data-stu-id="144df-255">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="144df-256">将消息发送。</span><span class="sxs-lookup"><span data-stu-id="144df-256">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="144df-257">文章要删除的消息。</span><span class="sxs-lookup"><span data-stu-id="144df-257">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="144df-258">文章将一条消息。</span><span class="sxs-lookup"><span data-stu-id="144df-258">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="144df-259">将消息发布到修补程序。</span><span class="sxs-lookup"><span data-stu-id="144df-259">POST a message to patch.</span></span>       |

<span data-ttu-id="144df-260">&#8224;用于进行到页面的 API 调用。</span><span class="sxs-lookup"><span data-stu-id="144df-260">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="144df-261">若要建立此方案，请从继承`DefaultPageApplicationModelProvider`类并重写[CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel)方法以提供用于解决的自定义逻辑[PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel)处理程序的名称。</span><span class="sxs-lookup"><span data-stu-id="144df-261">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="144df-262">示例应用演示如何做到这一点其`CustomPageApplicationModelProvider`类：</span><span class="sxs-lookup"><span data-stu-id="144df-262">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="144df-263">类的重要功能包括：</span><span class="sxs-lookup"><span data-stu-id="144df-263">Highlights of the class include:</span></span>

* <span data-ttu-id="144df-264">类继承自`DefaultPageApplicationModelProvider`。</span><span class="sxs-lookup"><span data-stu-id="144df-264">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="144df-265">`TryParseHandlerMethod`处理处理程序，以确定的 HTTP 谓词 (`httpMethod`) 和命名处理程序名称 (`handlerName`) 创建时`PageHandlerModel`。</span><span class="sxs-lookup"><span data-stu-id="144df-265">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="144df-266">`Async`后缀将被忽略，如果存在。</span><span class="sxs-lookup"><span data-stu-id="144df-266">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="144df-267">大小写用于分析与方法名称的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="144df-267">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="144df-268">当方法名称 (而无需`Async`) 是与名称相同的 HTTP 谓词，没有命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="144df-268">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="144df-269">`handlerName`设置为`null`，并且方法名称为`Get`， `Post`， `Delete`， `Put`，或`Patch`。</span><span class="sxs-lookup"><span data-stu-id="144df-269">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="144df-270">当方法名称 (而无需`Async`) 的长度超过 HTTP 谓词名称，没有命名处理程序。</span><span class="sxs-lookup"><span data-stu-id="144df-270">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="144df-271">`handlerName` 设置为 `<method name (less 'Async', if present)>`。</span><span class="sxs-lookup"><span data-stu-id="144df-271">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="144df-272">例如，"GetMessage"和"GetMessageAsync"产生"GetMessage"的处理程序名称。</span><span class="sxs-lookup"><span data-stu-id="144df-272">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="144df-273">删除、 PUT 和修补程序的 HTTP 谓词将转换为 POST。</span><span class="sxs-lookup"><span data-stu-id="144df-273">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="144df-274">注册`CustomPageApplicationModelProvider`中`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="144df-274">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="144df-275">代码隐藏文件*Index.cshtml.cs*演示普通的处理程序方法的命名约定中应用的页面的更改方式。</span><span class="sxs-lookup"><span data-stu-id="144df-275">The code-behind file *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="144df-276">"On"前缀命名 Razor 页与使用普通被删除。</span><span class="sxs-lookup"><span data-stu-id="144df-276">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="144df-277">初始化页面状态的方法现在名为`Get`。</span><span class="sxs-lookup"><span data-stu-id="144df-277">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="144df-278">你可以查看当你打开的所有页面进行任何代码隐藏文件整个应用使用此约定。</span><span class="sxs-lookup"><span data-stu-id="144df-278">You can see this convention used throughout the app if you open any code-behind file for any of the pages.</span></span>

<span data-ttu-id="144df-279">每个其他方法开头描述其处理的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="144df-279">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="144df-280">以开头的两个方法`Delete`将通常被视为 DELETE HTTP 谓词，但在逻辑`TryParseHandlerMethod`显式设置的谓词为 POST 为这两个处理程序。</span><span class="sxs-lookup"><span data-stu-id="144df-280">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="144df-281">请注意，`Async`是可选之间`DeleteAllMessages`和`DeleteMessageAsync`。</span><span class="sxs-lookup"><span data-stu-id="144df-281">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="144df-282">它们这两种异步方法，但你可以选择使用`Async`后缀或不; 我们建议你执行。</span><span class="sxs-lookup"><span data-stu-id="144df-282">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="144df-283">`DeleteAllMessages`出于演示目的，此处使用但我们建议你将此类方法`DeleteAllMessagesAsync`。</span><span class="sxs-lookup"><span data-stu-id="144df-283">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="144df-284">它不会影响处理的示例的实现，但使用`Async`后缀调出它是异步方法。</span><span class="sxs-lookup"><span data-stu-id="144df-284">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="144df-285">请注意处理程序的名称中提供*Index.cshtml*匹配`DeleteAllMessages`和`DeleteMessageAsync`处理程序方法：</span><span class="sxs-lookup"><span data-stu-id="144df-285">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="144df-286">`Async`在处理程序方法名称`DeleteMessageAsync`通过注销分解`TryParseHandlerMethod`匹配的方法的 POST 请求的处理程序。</span><span class="sxs-lookup"><span data-stu-id="144df-286">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="144df-287">`asp-page-handler`名称`DeleteMessage`的处理程序方法与匹配`DeleteMessageAsync`。</span><span class="sxs-lookup"><span data-stu-id="144df-287">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="144df-288">MVC 筛选器和页面筛选器 (IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="144df-288">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="144df-289">MVC[操作筛选器](xref:mvc/controllers/filters#action-filters)将被忽略由 Razor 页，因为 Razor 页使用处理程序方法。</span><span class="sxs-lookup"><span data-stu-id="144df-289">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="144df-290">并可供你使用其他类型的 MVC 筛选器：[授权](xref:mvc/controllers/filters#authorization-filters)，[异常](xref:mvc/controllers/filters#exception-filters)，[资源](xref:mvc/controllers/filters#resource-filters)，和[结果](xref:mvc/controllers/filters#result-filters)。</span><span class="sxs-lookup"><span data-stu-id="144df-290">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="144df-291">有关详细信息，请参阅[筛选器](xref:mvc/controllers/filters)主题。</span><span class="sxs-lookup"><span data-stu-id="144df-291">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="144df-292">页面筛选器 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) 是适用于 Razor 页的筛选器。</span><span class="sxs-lookup"><span data-stu-id="144df-292">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="144df-293">它在页处理程序方法的执行。</span><span class="sxs-lookup"><span data-stu-id="144df-293">It surrounds the execution of a page handler method.</span></span> <span data-ttu-id="144df-294">它可以在页处理程序方法执行的阶段处理自定义代码。</span><span class="sxs-lookup"><span data-stu-id="144df-294">It allows you to process custom code at stages of page handler method execution.</span></span> <span data-ttu-id="144df-295">下面是示例应用程序的一个示例：</span><span class="sxs-lookup"><span data-stu-id="144df-295">Here's an example from the sample app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/ReplaceRouteValueFilterAttribute.cs?name=snippet1)]

<span data-ttu-id="144df-296">此筛选器检查`globalTemplate`中"ReplacementValue"路由"TriggerValue"和交换的值。</span><span class="sxs-lookup"><span data-stu-id="144df-296">This filter checks for a `globalTemplate` route value of "TriggerValue" and swaps in "ReplacementValue".</span></span>

<span data-ttu-id="144df-297">`ReplaceRouteValueFilter`特性可以直接应用`PageModel`代码隐藏文件中：</span><span class="sxs-lookup"><span data-stu-id="144df-297">The `ReplaceRouteValueFilter` attribute can be applied directly to a `PageModel` in code-behind:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/OtherPages/Page3.cshtml.cs?range=10-12&highlight=1)]

<span data-ttu-id="144df-298">从示例应用程序与在请求页面 3 页`localhost:5000/OtherPages/Page3/TriggerValue`。</span><span class="sxs-lookup"><span data-stu-id="144df-298">Request the Page3 page from the sample app with at `localhost:5000/OtherPages/Page3/TriggerValue`.</span></span> <span data-ttu-id="144df-299">请注意筛选器将路由值的替换：</span><span class="sxs-lookup"><span data-stu-id="144df-299">Notice how the filter replaces the route value:</span></span>

![对 OtherPages/页面 3 的请求与在筛选器将路由值替换为 ReplacementValue TriggerValue 路径段结果。](razor-pages-convention-features/_static/otherpages-page3-filter-replacement-value.png)

## <a name="see-also"></a><span data-ttu-id="144df-301">请参阅</span><span class="sxs-lookup"><span data-stu-id="144df-301">See also</span></span>

* [<span data-ttu-id="144df-302">Razor 页面授权约定</span><span class="sxs-lookup"><span data-stu-id="144df-302">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)
