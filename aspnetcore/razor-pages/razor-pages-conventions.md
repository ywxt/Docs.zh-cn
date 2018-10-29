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
# <a name="razor-pages-route-and-app-conventions-in-aspnet-core"></a>ASP.NET Core 中 Razor 页面的路由和应用约定

作者：[Luke Latham](https://github.com/guardrex)

了解如何使用[页面路由和应用模型提供程序约定](xref:mvc/controllers/application-model#conventions)来控制 Razor 页面应用中的页面路由、发现和处理。

需要为各个页面配置自定义页面路由时，可使用本主题稍后所述的 [AddPageRoute 约定](#configure-a-page-route)配置页面路由。

若要指定页面路由、 添加路由段，或将参数添加到路由，请使用页面的`@page`指令。 有关详细信息，请参阅[自定义路由](xref:razor-pages/index#custom-routes)。

有不能用作路由段或参数名称的保留的字。 有关详细信息，请参阅[路由： 保留路由名称](xref:fundamentals/routing#reserved-routing-names)。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)（[如何下载](xref:index#how-to-download-a-sample)）

::: moniker range="= aspnetcore-2.0"

| 方案 | 示例演示... |
| -------- | --------------------------- |
| [模型约定](#model-conventions)<br><br>Conventions.Add<ul><li>IPageRouteModelConvention</li><li>IPageApplicationModelConvention</li></ul> | 将路由模板和标头添加到应用的页面。 |
| [页面路由操作约定](#page-route-action-conventions)<ul><li>AddFolderRouteModelConvention</li><li>AddPageRouteModelConvention</li><li>AddPageRoute</li></ul> | 将路由模板添加到某个文件夹中的页面以及单个页面。 |
| [页面模型操作约定](#page-model-action-conventions)<ul><li>AddFolderApplicationModelConvention</li><li>AddPageApplicationModelConvention</li><li>ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</li></ul> | 将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。 |
| [默认页面应用模型提供程序](#replace-the-default-page-app-model-provider) | 取代默认页面模型提供程序，用于更改处理程序命名约定。 |

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

| 方案 | 示例演示... |
| -------- | --------------------------- |
| [模型约定](#model-conventions)<br><br>Conventions.Add<ul><li>IPageRouteModelConvention</li><li>IPageApplicationModelConvention</li><li>IPageHandlerModelConvention</li></ul> | 将路由模板和标头添加到应用的页面。 |
| [页面路由操作约定](#page-route-action-conventions)<ul><li>AddFolderRouteModelConvention</li><li>AddPageRouteModelConvention</li><li>AddPageRoute</li></ul> | 将路由模板添加到某个文件夹中的页面以及单个页面。 |
| [页面模型操作约定](#page-model-action-conventions)<ul><li>AddFolderApplicationModelConvention</li><li>AddPageApplicationModelConvention</li><li>ConfigureFilter（筛选器类、Lambda 表达式或筛选器工厂）</li></ul> | 将标头添加到某个文件夹中的多个页面，将标头添加到单个页面，以及配置[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)以将标头添加到应用的页面。 |
| [默认页面应用模型提供程序](#replace-the-default-page-app-model-provider) | 取代默认页面模型提供程序，用于更改处理程序命名约定。 |

::: moniker-end

使用 [AddRazorPagesOptions](/dotnet/api/microsoft.extensions.dependencyinjection.mvcrazorpagesmvcbuilderextensions.addrazorpagesoptions) 扩展方法向 `Startup` 类中服务集合的 [AddMvc](/dotnet/api/microsoft.extensions.dependencyinjection.mvcservicecollectionextensions.addmvc) 添加和配置 Razor 页面约定。 本主题稍后会介绍以下约定示例：

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

## <a name="route-order"></a>路由顺序

路由指定<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*>用于处理 （路由匹配）。

| 顺序            | 行为 |
| :--------------: | -------- |
| -1               | 处理其他路由之前处理该路由。 |
| 0                | 未指定顺序 （默认值）。 不分配`Order`(`Order = null`) 将默认路由`Order`为 0 （零） 进行处理。 |
| 1、 2、 &hellip; n | 指定路由处理顺序。 |

按照约定来建立路由处理：

* 按顺序处理的路由 (-1、 0、 1、 2、 &hellip; n)。
* 当路由具有相同`Order`、 最具体的路由匹配跟有更具体的路由。
* 当具有相同的路由`Order`和相同数量的参数匹配请求 URL，将它们添加到顺序处理路由<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.PageConventionCollection>。

如果可能，避免具体取决于已建立的路由处理顺序。 通常情况下，路由选择与 URL 匹配的正确路由。 如果必须设置路由`Order`属性路由请求是否正确，应用程序的路由方案，可能令人困惑，向客户端和脆弱来维护。 查找以简化应用程序的路由方案。 示例应用程序需要处理订单，若要演示几个路由方案使用的单个应用程序的显式路由。 但是，您应尝试避免设置路由的做法`Order`生产应用中。

Razor Pages 路由和 MVC 控制器路由共享一个实现。 路由顺序 MVC 主题中的信息位于[路由到控制器操作： 对属性路由排序](xref:mvc/controllers/routing#ordering-attribute-routes)。

## <a name="model-conventions"></a>模型约定

为 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 添加委托，以添加应用于 Razor 页面的[模型约定](xref:mvc/controllers/application-model#conventions)。

### <a name="add-a-route-model-convention-to-all-pages"></a>将路由模型约定添加到所有页面

使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面路由模型构造过程中应用。

示例应用将 `{globalTemplate?}` 路由模板添加到应用中的所有页面：

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `1`。 这可确保匹配行为示例应用程序中的以下路由：

* 路由模板`TheContactPage/{text?}`添加本主题后面。 联系人页面路由的默认顺序`null`(`Order = 0`)，因此它匹配之前`{globalTemplate?}`路由模板。
* `{aboutTemplate?}`路由模板添加本主题后面。 为 `{aboutTemplate?}` 模板指定的 `Order` 为 `2`。 当在 `/About/RouteDataValue` 中请求“关于”页面时，由于设置了 `Order` 属性，“RouteDataValue”会加载到 `RouteData.Values["globalTemplate"]` (`Order = 1`) 而不是 `RouteData.Values["aboutTemplate"]` (`Order = 2`) 中。
* `{otherPagesTemplate?}`路由模板添加本主题后面。 为 `{otherPagesTemplate?}` 模板指定的 `Order` 为 `2`。 中的任何页时*Pages/OtherPages*文件夹请求与路由参数 (例如， `/OtherPages/Page1/RouteDataValue`)，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["otherPagesTemplate"]`(`Order = 2`)由于设置`Order`属性。

如有可能，未设置`Order`，这会导致`Order = 0`。 依赖于路由，以选择正确的路由。

将 MVC 添加到 `Startup.ConfigureServices` 中的服务集合时，会添加 Razor 页面选项，例如添加[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)。 有关示例，请参阅[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/razor-pages-conventions/sample/)。

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet1)]

在 `localhost:5000/About/GlobalRouteValue` 中请求示例的“关于”页面并检查结果：

![使用 GlobalRouteValue 路由段请求“关于”页面。 呈现的页面显示，在页面的 OnGet 方法中捕获了路由数据值。](razor-pages-conventions/_static/about-page-global-template.png)

### <a name="add-an-app-model-convention-to-all-pages"></a>将应用模型约定添加到所有页面

使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面应用模型构造过程中应用。

为了演示此约定以及本主题后面的其他约定，示例应用包含了一个 `AddHeaderAttribute` 类。 类构造函数采用 `name` 字符串和 `values` 字符串数组。 将在其 `OnResultExecuting` 方法中使用这些值来设置响应标头。 本主题后面的[页面模型操作约定](#page-model-action-conventions)部分展示了完整的类。

示例应用使用 `AddHeaderAttribute` 类将标头 `GlobalHeader` 添加到应用中的所有页面：

[!code-csharp[](razor-pages-conventions/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

*Startup.cs*：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet2)]

在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：

![“关于”页面的响应标头显示已添加 GlobalHeader。](razor-pages-conventions/_static/about-page-global-header.png)

::: moniker range=">= aspnetcore-2.1"

### <a name="add-a-handler-model-convention-to-all-pages"></a>将处理程序模型约定添加到的所有页面

使用[约定](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions)创建 [IPageHandlerModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipagehandlermodelconvention) 并将其添加到 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 实例集合中，这些实例将在页面处理程序模型构造过程中应用。

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

`Startup.ConfigureServices`：

```csharp
services.AddMvc()
    .AddRazorPagesOptions(options =>
        {
            options.Conventions.Add(new GlobalPageHandlerModelConvention());
        });
```

::: moniker-end

## <a name="page-route-action-conventions"></a>页面路由操作约定

默认路由模型提供程序派生自 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider)，可调用旨在为页面路由配置提供扩展点的约定。

### <a name="folder-route-model-convention"></a>文件夹路由模型约定

使用 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。

示例应用使用 `AddFolderRouteModelConvention` 将 `{otherPagesTemplate?}` 路由模板添加到 *OtherPages* 文件夹中的页面：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet3)]

<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `2`。 这可以保证的模板`{globalTemplate?}`(设置到主题中前面`1`) 提供单个路由值时，第一个路由数据值位置分配优先级。 如果在页*Pages/OtherPages*文件夹请求与路由参数值 (例如， `/OtherPages/Page1/RouteDataValue`)，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["otherPagesTemplate"]`(`Order = 2`)由于设置`Order`属性。

如有可能，未设置`Order`，这会导致`Order = 0`。 依赖于路由，以选择正确的路由。

在 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 中请求示例的 Page1 页面并检查结果：

![使用 GlobalRouteValue 和 OtherPagesRouteValue 路由段请求 OtherPages 文件夹中的 Page1。 呈现的页面显示，在页面的 OnGet 方法中捕获了路由数据值。](razor-pages-conventions/_static/otherpages-page1-global-and-otherpages-templates.png)

### <a name="page-route-model-convention"></a>页面路由模型约定

使用 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 创建并添加 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention)，后者可以为具有指定名称的页面调用 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 上的操作。

示例应用使用 `AddPageRouteModelConvention` 将 `{aboutTemplate?}` 路由模板添加到“关于”页面：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet4)]

<xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel> 的 <xref:Microsoft.AspNetCore.Mvc.ApplicationModels.AttributeRouteModel.Order*> 属性设置为 `2`。 这可以保证的模板`{globalTemplate?}`(设置到主题中前面`1`) 提供单个路由值时，第一个路由数据值位置分配优先级。 如果使用路由参数值在请求关于页面`/About/RouteDataValue`，"RouteDataValue"加载到`RouteData.Values["globalTemplate"]`(`Order = 1`)，而不`RouteData.Values["aboutTemplate"]`(`Order = 2`) 因设置而`Order`属性。

如有可能，未设置`Order`，这会导致`Order = 0`。 依赖于路由，以选择正确的路由。

在 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 中请求示例的“关于”页面并检查结果：

![使用 GlobalRouteValue 和 AboutRouteValue 路由段请求“关于”页面。 呈现的页面显示，在页面的 OnGet 方法中捕获了路由数据值。](razor-pages-conventions/_static/about-page-global-and-about-templates.png)

::: moniker range=">= aspnetcore-2.2"

## <a name="use-a-parameter-transformer-to-customize-page-routes"></a>参数转换器用于自定义页面路由

使用参数转换器可以自定义页面路由生成的 ASP.NET Core。 参数转换程序实现 `IOutboundParameterTransformer` 并转换参数值。 例如，一个自定义 `SlugifyParameterTransformer` 参数转换程序可将 `SubscriptionManagement` 路由值更改为 `subscription-management`。

`PageRouteTransformerConvention`页面路由模型约定适用于在应用中自动生成的页路由文件夹和文件名称段参数转换器。 例如，Razor 页面文件位于 */Pages/SubscriptionManagement/ViewAll.cshtml*必须重写中其路由`/SubscriptionManagement/ViewAll`到`/subscription-management/view-all`。

`PageRouteTransformerConvention` 仅将转换的页面路由来自 Razor 页面文件夹和文件名称自动生成的段。 它不会转换与添加的路由段`@page`指令。 约定也不会转换添加的路由<xref:Microsoft.Extensions.DependencyInjection.PageConventionCollectionExtensions.AddPageRoute*>。

`PageRouteTransformerConvention`注册中的一个选项为`Startup.ConfigureServices`:

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

## <a name="configure-a-page-route"></a>配置页面路由

使用 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 配置路由，该路由指向指定页面路径中的页面。 生成的页面链接使用指定的路由。 `AddPageRoute` 使用 `AddPageRouteModelConvention` 建立路由。

示例应用为 *Contact.cshtml* 创建指向 `/TheContactPage` 的路由：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet5)]

还可在 `/Contact` 中通过默认路由访问“联系人”页面。

示例应用的“联系人”页面自定义路由允许使用可选的 `text` 路由段 (`{text?}`)。 该页面还在其 `@page` 指令中包含此可选段，以便访问者在 `/Contact` 路由中访问该页面：

[!code-cshtml[](razor-pages-conventions/sample/Pages/Contact.cshtml?highlight=1)]

请注意，在呈现的页面中，为**联系人**链接生成的 URL 反映了已更新的路由：

![导航栏中的示例应用“联系人”链接](razor-pages-conventions/_static/contact-link.png)

![检查呈现的 HTML 中的“联系人”链接，可看到 href 设置为“/TheContactPage”](razor-pages-conventions/_static/contact-link-source.png)

在常规路由 `/Contact` 或自定义路由 `/TheContactPage` 中访问“联系人”页面。 如果提供附加的 `text` 路由段，该页面会显示所提供的 HTML 编码段：

![在 URL 中提供可选“'text”路由段“TextValue”的 Microsoft Edge 浏览器示例。 呈现的页面显示“text”段值。](razor-pages-conventions/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a>页面模型操作约定

实现 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 的默认页面模型提供程序可调用约定，这些约定旨在为页面模型配置提供扩展点。 在生成和修改页面发现及处理方案时，可使用这些约定。

对于此部分中的示例，示例应用使用 `AddHeaderAttribute` 类（一个 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute)）来应用响应标头：

[!code-csharp[](razor-pages-conventions/sample/Filters/AddHeader.cs?name=snippet1)]

示例演示了如何使用约定将该属性应用于某个文件夹中的所有页面以及单个页面。

**文件夹应用模型约定**

使用 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 创建并添加 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention)，后者可以为指定文件夹下的所有页面调用 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 实例上的操作。

示例演示了如何使用 `AddFolderApplicationModelConvention` 将标头 `OtherPagesHeader` 添加到应用的 *OtherPages* 文件夹内的页面：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet6)]

在 `localhost:5000/OtherPages/Page1` 中请求示例的 Page1 页面，并检查标头以查看结果：

![OtherPages/Page1 页面的响应标头显示已添加 OtherPagesHeader。](razor-pages-conventions/_static/page1-otherpages-header.png)

**页面应用模型约定**

使用[AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention)创建并添加[IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) ，它在调用操作[PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel)页使用指定的名称。

示例演示了如何使用 `AddPageApplicationModelConvention` 将标头 `AboutHeader` 添加到“关于”页面：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet7)]

在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：

![“关于”页面的响应标头显示已添加 AboutHeader。](razor-pages-conventions/_static/about-page-about-header.png)

**配置筛选器**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 可配置要应用的指定筛选器。 用户可以实现筛选器类，但示例应用演示了如何在 Lambda 表达式中实现筛选器，该筛选器在后台作为可返回筛选器的工厂实现：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet8)]

页面应用模型用于检查指向 *OtherPages* 文件夹中 Page2 页面的段的相对路径。 如果条件通过，则添加标头。 如果不通过，则应用 `EmptyFilter`。

`EmptyFilter` 是一种[操作筛选器](xref:mvc/controllers/filters#action-filters)。 由于 Razor 页面会忽略操作筛选器，因此，如果路径不包含 `OtherPages/Page2`，`EmptyFilter` 会按预期发出空操作指令。

在 `localhost:5000/OtherPages/Page2` 中请求示例的 Page2 页面，并检查标头以查看结果：

![OtherPagesPage2Header 已添加到 Page2 的响应。](razor-pages-conventions/_static/page2-filter-header.png)

**配置筛选器工厂**

[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 可配置指定的工厂，以将[筛选器](xref:mvc/controllers/filters)应用于所有 Razor 页面。

示例应用提供了一个示例，说明如何使用[筛选器工厂](xref:mvc/controllers/filters#ifilterfactory)将具有两个值的标头 `FilterFactoryHeader` 添加到应用的页面：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet9)]

*AddHeaderWithFactory.cs*：

[!code-csharp[](razor-pages-conventions/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

在 `localhost:5000/About` 中请求示例的“关于”页面，并检查标头以查看结果：

![“关于”页面的响应标头显示已添加两个 FilterFactoryHeader 标头。](razor-pages-conventions/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a>替换默认页面应用模型提供程序

Razor 页面使用 `IPageApplicationModelProvider` 接口创建 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)。 用户可以从默认模型提供程序继承，以便为处理程序发现和处理提供自己的实现逻辑。 默认实现（[引用源](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)）为*未命名*和*已命名*处理程序的命名建立了约定，如下所述。

**默认的未命名处理程序方法**

Http 谓词的处理程序方法（“未命名”的处理程序方法）遵循以下约定：`On<HTTP verb>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。

| 未命名处理程序方法     | 操作                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | 初始化页面状态。     |
| `OnPost`/`OnPostAsync`     | 处理 POST 请求。          |
| `OnDelete`/`OnDeleteAsync` | 处理 DELETE 请求&#8224;。 |
| `OnPut`/`OnPutAsync`       | 处理 PUT 请求&#8224;。    |
| `OnPatch`/`OnPatchAsync`   | 处理 PATCH 请求&#8224;。  |

&#8224;用于向页面发出 API 调用。

**默认的已命名处理程序方法**

由开发人员提供的处理程序方法（“已命名”的处理程序方法）遵循类似的约定。 处理程序名称出现在 Http 谓词之后或者 Http 谓词与 `Async` 之间：`On<HTTP verb><handler name>[Async]`（追加 `Async` 是可选操作，但建议为异步方法执行此操作）。 例如，用于处理消息的方法可能采用下表所示的命名。

| 已命名处理程序方法示例             | 操作示例        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | 获取消息。        |
| `OnPostMessage`/`OnPostMessageAsync`     | POST 消息。          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | DELETE 消息&#8224;。 |
| `OnPutMessage`/`OnPutMessageAsync`       | PUT 消息&#8224;。    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | PATCH 消息&#8224;。  |

&#8224;用于向页面发出 API 调用。

**自定义处理程序方法名称**

假设用户想更改未命名和已命名处理程序方法的命名方式。 备选命名方案是避免让方法名称以“On”开头，并使用第一个分词来确定 Http 谓词。 也可以进行其他更改，比如将 DELETE、PUT 和 PATCH 的谓词转换为 POST。 这种方案提供下表所示的方法名称。

| 处理程序方法                       | 操作                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | 初始化页面状态。     |
| `Post`/`PostAsync`                   | 处理 POST 请求。          |
| `Delete`/`DeleteAsync`               | 处理 DELETE 请求&#8224;。 |
| `Put`/`PutAsync`                     | 处理 PUT 请求&#8224;。    |
| `Patch`/`PatchAsync`                 | 处理 PATCH 请求&#8224;。  |
| `GetMessage`                         | 获取消息。              |
| `PostMessage`/`PostMessageAsync`     | POST 消息。                |
| `DeleteMessage`/`DeleteMessageAsync` | POST 消息以进行删除。      |
| `PutMessage`/`PutMessageAsync`       | POST 消息以进行放置。         |
| `PatchMessage`/`PatchMessageAsync`   | POST 消息以进行修补。       |

&#8224;用于向页面发出 API 调用。

若要建立此方案，请从 `DefaultPageApplicationModelProvider` 类继承并重写 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 方法，以提供自定义逻辑来解析 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 处理程序名称。 示例应用展示了如何在其 `CustomPageApplicationModelProvider` 类中执行此操作：

[!code-csharp[](razor-pages-conventions/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

该类的要点包括：

* 该类继承自 `DefaultPageApplicationModelProvider`。
* `TryParseHandlerMethod` 对处理程序进行处理，以便在创建 `PageHandlerModel` 时确定 Http 谓词 (`httpMethod`) 和已命名处理程序名称 (`handlerName`)。
  * 忽略 `Async` 后缀（如果存在）。
  * 使用大小写分析方法名称中的 Http 谓词。
  * 当方法名称（不带 `Async`）与 Http 谓词名称相同时，就不存在已命名处理程序。 `handlerName` 设置为 `null`，且方法名称为 `Get`、`Post`、`Delete`、`Put` 或 `Patch`。
  * 当方法名称（不带 `Async`）的长度超过 Http 谓词名称时，就存在已命名处理程序。 `handlerName` 设置为 `<method name (less 'Async', if present)>`。 例如，“GetMessage”和“GetMessageAsync”都生成处理程序名称“GetMessage”。
  * DELETE、PUT 和 PATCH Http 谓词都转换为 POST。

在 `Startup` 类中注册 `CustomPageApplicationModelProvider`：

[!code-csharp[](razor-pages-conventions/sample/Startup.cs?name=snippet10)]

*Index.cshtml.cs* 中的页面模型演示了如何针对应用中的页面更改常规的处理程序方法命名约定。 用于 Razor 页面的常规“On”前缀命名已被删除。 用于初始化页面状态的方法现在命名为 `Get`。 为任何页面打开任何页面模型时，都可以看到此约定贯穿于整个应用。

其他各个方法均以描述其处理的 Http 谓词开头。 以 `Delete` 开头的两个方法通常被视为 DELETE Http 谓词，但 `TryParseHandlerMethod` 中的逻辑会针对这两种处理程序将该谓词显式设置为 POST。

请注意，`Async` 在 `DeleteAllMessages` 和 `DeleteMessageAsync` 之间是可选的。 它们都是异步方法，但用户可以选择是否使用 `Async` 后缀；我们建议使用。 此处使用 `DeleteAllMessages` 只是为了进行演示，但建议将此类方法命名为 `DeleteAllMessagesAsync`。 它对示例的实现处理没有影响，但使用 `Async` 后缀强调了它是异步方法的事实。

[!code-csharp[](razor-pages-conventions/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

请注意，*Index.cshtml* 中提供的处理程序名称与 `DeleteAllMessages` 和 `DeleteMessageAsync` 处理程序方法相匹配：

[!code-cshtml[](razor-pages-conventions/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

为了方便处理程序将 POST 请求与方法进行匹配，`TryParseHandlerMethod` 剔除了处理程序方法名称 `DeleteMessageAsync` 中的 `Async`。 `DeleteMessage` 的 `asp-page-handler` 名称与处理程序方法 `DeleteMessageAsync` 匹配。

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a>MVC 筛选器和页面筛选器 (IPageFilter)

Razor 页面会忽略 MVC [操作筛选器](xref:mvc/controllers/filters#action-filters)，因为 Razor 页面使用处理程序方法。 可使用其他类型的 MVC 筛选器：[授权](xref:mvc/controllers/filters#authorization-filters)、[异常](xref:mvc/controllers/filters#exception-filters)、[资源](xref:mvc/controllers/filters#resource-filters)和[结果](xref:mvc/controllers/filters#result-filters)。 有关详细信息，请参阅[筛选器](xref:mvc/controllers/filters)主题。

页面筛选器 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) 是应用于 Razor 页面的一种筛选器。 有关详细信息，请参阅 [Razor 页面的筛选方法](xref:razor-pages/filter)。

## <a name="additional-resources"></a>其他资源

* [Razor 页面授权约定](xref:security/authorization/razor-pages-authorization)
