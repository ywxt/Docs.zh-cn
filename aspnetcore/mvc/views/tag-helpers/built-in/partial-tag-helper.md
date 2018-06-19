---
title: ASP.NET Core 中的部分标记帮助程序
author: scottaddie
description: 发现 ASP.NET Core 部分标记帮助程序以及每个属性在呈现分部视图时所扮演的角色。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 04/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
ms.openlocfilehash: 786c333980db89a9a5a60dc70c0bd1998ca159cd
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "33962589"
---
# <a name="partial-tag-helper-in-aspnet-core"></a><span data-ttu-id="a0b41-103">ASP.NET Core 中的部分标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="a0b41-103">Partial Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="a0b41-104">作者：[Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="a0b41-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="a0b41-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="a0b41-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="overview"></a><span data-ttu-id="a0b41-106">概述</span><span class="sxs-lookup"><span data-stu-id="a0b41-106">Overview</span></span>

<span data-ttu-id="a0b41-107">Partial 标记帮助程序用于在 Razor 页面和 MVC 应用中呈现[分部视图](xref:mvc/views/partial)。</span><span class="sxs-lookup"><span data-stu-id="a0b41-107">The Partial Tag Helper is used for rendering a [partial view](xref:mvc/views/partial) in Razor Pages and MVC apps.</span></span> <span data-ttu-id="a0b41-108">请考虑：</span><span class="sxs-lookup"><span data-stu-id="a0b41-108">Consider that it:</span></span>

* <span data-ttu-id="a0b41-109">需要 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="a0b41-109">Requires ASP.NET Core 2.1 or later.</span></span>
* <span data-ttu-id="a0b41-110">是 [HTML 帮助程序语法](xref:mvc/views/partial#referencing-a-partial-view)的替代方法。</span><span class="sxs-lookup"><span data-stu-id="a0b41-110">Is an alternative to [HTML Helper syntax](xref:mvc/views/partial#referencing-a-partial-view).</span></span>
* <span data-ttu-id="a0b41-111">以异步方式呈现分部视图。</span><span class="sxs-lookup"><span data-stu-id="a0b41-111">Renders the partial view asynchronously.</span></span>

<span data-ttu-id="a0b41-112">用于呈现分部视图的 HTML 帮助程序选项包括：</span><span class="sxs-lookup"><span data-stu-id="a0b41-112">The HTML Helper options for rendering a partial view include:</span></span>

* [<span data-ttu-id="a0b41-113">@await Html.PartialAsync</span><span class="sxs-lookup"><span data-stu-id="a0b41-113">@await Html.PartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [<span data-ttu-id="a0b41-114">@await Html.RenderPartialAsync</span><span class="sxs-lookup"><span data-stu-id="a0b41-114">@await Html.RenderPartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

<span data-ttu-id="a0b41-115">本文档中的示例均使用产品模型：</span><span class="sxs-lookup"><span data-stu-id="a0b41-115">The *Product* model is used in samples throughout this document:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

<span data-ttu-id="a0b41-116">以下是分部标记帮助程序属性的清单。</span><span class="sxs-lookup"><span data-stu-id="a0b41-116">An inventory of the Partial Tag Helper attributes follows.</span></span>

## <a name="name"></a><span data-ttu-id="a0b41-117">name</span><span class="sxs-lookup"><span data-stu-id="a0b41-117">name</span></span>

<span data-ttu-id="a0b41-118">需要 `name` 属性。</span><span class="sxs-lookup"><span data-stu-id="a0b41-118">The `name` attribute is required.</span></span> <span data-ttu-id="a0b41-119">它指示要呈现的分部视图的名称或路径。</span><span class="sxs-lookup"><span data-stu-id="a0b41-119">It indicates the name or the path of the partial view to be rendered.</span></span> <span data-ttu-id="a0b41-120">提供分部视图名称时，会启动[视图发现](xref:mvc/views/overview#view-discovery)进程。</span><span class="sxs-lookup"><span data-stu-id="a0b41-120">When a partial view name is provided, the [view discovery](xref:mvc/views/overview#view-discovery) process is initiated.</span></span> <span data-ttu-id="a0b41-121">提供显式路径时，将绕过该进程。</span><span class="sxs-lookup"><span data-stu-id="a0b41-121">That process is bypassed when an explicit path is provided.</span></span>

<span data-ttu-id="a0b41-122">以下标记使用显式路径，指示要从共享文件夹加载 _ProductPartial.cshtml。</span><span class="sxs-lookup"><span data-stu-id="a0b41-122">The following markup uses an explicit path, indicating that *_ProductPartial.cshtml* is to be loaded from the *Shared* folder.</span></span> <span data-ttu-id="a0b41-123">使用 [for](#for) 属性，将模型传递给分部视图进行绑定。</span><span class="sxs-lookup"><span data-stu-id="a0b41-123">Using the [for](#for) attribute, a model is passed to the partial view for binding.</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## <a name="for"></a><span data-ttu-id="a0b41-124">for</span><span class="sxs-lookup"><span data-stu-id="a0b41-124">for</span></span>

<span data-ttu-id="a0b41-125">`for` 属性分配要根据当前模型评估的 [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression)。</span><span class="sxs-lookup"><span data-stu-id="a0b41-125">The `for` attribute assigns a [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression) to be evaluated against the current model.</span></span> <span data-ttu-id="a0b41-126">`ModelExpression` 推断 `@Model.` 语法。</span><span class="sxs-lookup"><span data-stu-id="a0b41-126">A `ModelExpression` infers the `@Model.` syntax.</span></span> <span data-ttu-id="a0b41-127">例如，可使用 `for="Product"` 而非 `for="@Model.Product"`。</span><span class="sxs-lookup"><span data-stu-id="a0b41-127">For example, `for="Product"` can be used instead of `for="@Model.Product"`.</span></span> <span data-ttu-id="a0b41-128">通过使用 `@` 符号定义内联表达式来替代此默认推理行为。</span><span class="sxs-lookup"><span data-stu-id="a0b41-128">This default inference behavior is overridden by using the `@` symbol to define an inline expression.</span></span> <span data-ttu-id="a0b41-129">`for` 属性不能与 [model](#model) 属性一起使用。</span><span class="sxs-lookup"><span data-stu-id="a0b41-129">The `for` attribute can't be used with the [model](#model) attribute.</span></span>

<span data-ttu-id="a0b41-130">以下标记加载 _ProductPartial.cshtml：</span><span class="sxs-lookup"><span data-stu-id="a0b41-130">The following markup loads *_ProductPartial.cshtml*:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_For)]

<span data-ttu-id="a0b41-131">分部视图绑定到关联页模型的 `Product` 属性：</span><span class="sxs-lookup"><span data-stu-id="a0b41-131">The partial view is bound to the associated page model's `Product` property:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## <a name="model"></a><span data-ttu-id="a0b41-132">model</span><span class="sxs-lookup"><span data-stu-id="a0b41-132">model</span></span>

<span data-ttu-id="a0b41-133">`model` 属性分配模型实例，以传递到分部视图。</span><span class="sxs-lookup"><span data-stu-id="a0b41-133">The `model` attribute assigns a model instance to pass to the partial view.</span></span> <span data-ttu-id="a0b41-134">`model` 属性不能与 [for](#for) 属性一起使用。</span><span class="sxs-lookup"><span data-stu-id="a0b41-134">The `model` attribute can't be used with the [for](#for) attribute.</span></span>

<span data-ttu-id="a0b41-135">在以下标记中，实例化新的 `Product` 对象并将其传递给 `model` 属性进行绑定：</span><span class="sxs-lookup"><span data-stu-id="a0b41-135">In the following markup, a new `Product` object is instantiated and passed to the `model` attribute for binding:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Model)]

## <a name="view-data"></a><span data-ttu-id="a0b41-136">view-data</span><span class="sxs-lookup"><span data-stu-id="a0b41-136">view-data</span></span>

<span data-ttu-id="a0b41-137">`view-data` 属性分配 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)，以传递到分部视图。</span><span class="sxs-lookup"><span data-stu-id="a0b41-137">The `view-data` attribute assigns a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to pass to the partial view.</span></span> <span data-ttu-id="a0b41-138">以下标记使整个 ViewData 集合可访问分部视图：</span><span class="sxs-lookup"><span data-stu-id="a0b41-138">The following markup makes the entire ViewData collection accessible to the partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

<span data-ttu-id="a0b41-139">在前面的代码中，`IsNumberReadOnly` 键值设置为 `true` 并添加到 ViewData 集合中。</span><span class="sxs-lookup"><span data-stu-id="a0b41-139">In the preceding code, the `IsNumberReadOnly` key value is set to `true` and added to the ViewData collection.</span></span> <span data-ttu-id="a0b41-140">因此，在以下分部视图中可访问 `ViewData["IsNumberReadOnly"]`：</span><span class="sxs-lookup"><span data-stu-id="a0b41-140">Consequently, `ViewData["IsNumberReadOnly"]` is made accessible within the following partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

<span data-ttu-id="a0b41-141">在此示例中，`ViewData["IsNumberReadOnly"]` 的值确定 Number 字段是否显示为只读。</span><span class="sxs-lookup"><span data-stu-id="a0b41-141">In this example, the value of `ViewData["IsNumberReadOnly"]` determines whether the *Number* field is displayed as read only.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0b41-142">其他资源</span><span class="sxs-lookup"><span data-stu-id="a0b41-142">Additional resources</span></span>

* [<span data-ttu-id="a0b41-143">部分视图</span><span class="sxs-lookup"><span data-stu-id="a0b41-143">Partial views</span></span>](xref:mvc/views/partial)
* [<span data-ttu-id="a0b41-144">弱类型数据（ViewData、ViewData 属性和 ViewBag）</span><span class="sxs-lookup"><span data-stu-id="a0b41-144">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>](xref:mvc/views/overview#weakly-typed-data-viewdata-viewdata-attribute-and-viewbag)
