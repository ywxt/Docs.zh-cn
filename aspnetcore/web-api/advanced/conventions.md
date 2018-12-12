---
title: 使用 Web API 约定
author: pranavkm
description: 了解 ASP.NET Core 中的 Web API 约定。
monikerRange: '>= aspnetcore-2.2'
ms.author: pranavkm
ms.custom: mvc
ms.date: 11/13/2018
uid: web-api/advanced/conventions
ms.openlocfilehash: ede9a46c160cf6a49aa93da710af0bf0b8f59acc
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710070"
---
# <a name="use-web-api-conventions"></a><span data-ttu-id="e22a9-103">使用 Web API 约定</span><span class="sxs-lookup"><span data-stu-id="e22a9-103">Use web API conventions</span></span>

<span data-ttu-id="e22a9-104">ASP.NET Core 2.2 引入了一种方法，可提取常见的 [API 文档](xref:tutorials/web-api-help-pages-using-swagger)并将其应用于多个操作、控制器或某程序集内的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="e22a9-104">ASP.NET Core 2.2 introduces a way to extract common [API documentation](xref:tutorials/web-api-help-pages-using-swagger) and apply it to multiple actions, controllers, or all controllers within an assembly.</span></span> <span data-ttu-id="e22a9-105">Web API 约定可替代使用 [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute) 来装饰单个操作。</span><span class="sxs-lookup"><span data-stu-id="e22a9-105">Web API conventions are a substitute for decorating individual actions with [[ProducesResponseType]](xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute).</span></span> <span data-ttu-id="e22a9-106">使用该约定，可定义从操作返回的最通用的“常规”返回类型和状态代码，并选择适用于某个操作的约定方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-106">It allows you to define the most common "conventional" return types and status codes that you return from your action with a way to select the convention method that applies to an action.</span></span>

<span data-ttu-id="e22a9-107">默认情况下，ASP.NET Core MVC 2.2 附带一组默认约定，`Microsoft.AspNetCore.Mvc.DefaultApiConventions`。</span><span class="sxs-lookup"><span data-stu-id="e22a9-107">By default, ASP.NET Core MVC 2.2 ships with a set of default conventions, `Microsoft.AspNetCore.Mvc.DefaultApiConventions`.</span></span> <span data-ttu-id="e22a9-108">这些约定基于 ASP.NET Core 为其提供基架的控制器。</span><span class="sxs-lookup"><span data-stu-id="e22a9-108">The conventions are based on the controller that ASP.NET Core scaffolds.</span></span> <span data-ttu-id="e22a9-109">若操作遵循基架产生的模式，则应成功使用默认约定。</span><span class="sxs-lookup"><span data-stu-id="e22a9-109">If your actions follow the pattern that scaffolding produces, you should be successful using the default conventions.</span></span>

<span data-ttu-id="e22a9-110">在运行时，<xref:Microsoft.AspNetCore.Mvc.ApiExplorer> 会了解约定。</span><span class="sxs-lookup"><span data-stu-id="e22a9-110">At runtime, <xref:Microsoft.AspNetCore.Mvc.ApiExplorer> understands conventions.</span></span> <span data-ttu-id="e22a9-111">`ApiExplorer` 是 MVC 与开放 API 文档生成器进行通信的抽象内容。</span><span class="sxs-lookup"><span data-stu-id="e22a9-111">`ApiExplorer` is MVC's abstraction to communicate with Open API document generators.</span></span> <span data-ttu-id="e22a9-112">已应用的约定中的属性与某个操作相关联，并包含在操作的 Swagger 文档中。</span><span class="sxs-lookup"><span data-stu-id="e22a9-112">Attributes from the applied convention get associated with an action and are included in the action's Swagger documentation.</span></span> <span data-ttu-id="e22a9-113">API 分析器也会了解约定。</span><span class="sxs-lookup"><span data-stu-id="e22a9-113">API analyzers also understand conventions.</span></span> <span data-ttu-id="e22a9-114">若操作为非常规操作（例如，它返回已应用的约定未记录的状态代码），则会生成警告，建议记录该操作。</span><span class="sxs-lookup"><span data-stu-id="e22a9-114">If your action is unconventional (for example, it returns a status code that isn't documented by the applied convention), it produces a warning, encouraging you to document it.</span></span>

<span data-ttu-id="e22a9-115">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="e22a9-115">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/advanced/conventions/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="apply-web-api-conventions"></a><span data-ttu-id="e22a9-116">应用 Web API 约定</span><span class="sxs-lookup"><span data-stu-id="e22a9-116">Apply web API conventions</span></span>

<span data-ttu-id="e22a9-117">应用约定有三种方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-117">There are three ways to apply a convention.</span></span> <span data-ttu-id="e22a9-118">约定不是组合而成的。</span><span class="sxs-lookup"><span data-stu-id="e22a9-118">Conventions don't compose.</span></span> <span data-ttu-id="e22a9-119">每个操作可能只与一个约定相关联。</span><span class="sxs-lookup"><span data-stu-id="e22a9-119">Each action may be associated with exactly one convention.</span></span> <span data-ttu-id="e22a9-120">更明确的约定（详见下文）优先于不太明确的约定。</span><span class="sxs-lookup"><span data-stu-id="e22a9-120">More specific conventions (detailed below) take precedence over less specific ones.</span></span> <span data-ttu-id="e22a9-121">当具有相同优先级的两个或更多约定应用于某个操作时，选择是不确定的。</span><span class="sxs-lookup"><span data-stu-id="e22a9-121">The selection is non-deterministic when two or more conventions of the same priority apply to an action.</span></span> <span data-ttu-id="e22a9-122">存在以下可将约定应用于操作的选项，明确性依次降低：</span><span class="sxs-lookup"><span data-stu-id="e22a9-122">The following options exist to apply a convention to an action, from the most specific to the least specific:</span></span>

1. <span data-ttu-id="e22a9-123">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; 适用于单独的操作，并指定适用的约定类型和约定方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-123">`Microsoft.AspNetCore.Mvc.ApiConventionMethodAttribute` &mdash; Applies to individual actions and specifies the convention type and the convention method that applies.</span></span> <span data-ttu-id="e22a9-124">在以下示例中，将约定方法 `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` 应用于 `Update` 操作：</span><span class="sxs-lookup"><span data-stu-id="e22a9-124">In the following sample, the convention method `Microsoft.AspNetCore.Mvc.DefaultApiConventions.Put` is applied to the `Update` action:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventionmethod&highlight=2-3)]

1. <span data-ttu-id="e22a9-125">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` 应用于控制器 &mdash; 将约定类型应用于控制器上的所有操作。</span><span class="sxs-lookup"><span data-stu-id="e22a9-125">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to a controller &mdash; Applies the convention type to all actions on the controller.</span></span> <span data-ttu-id="e22a9-126">约定方法通过确定将应用于哪些操作的提示进行装饰（作为创作约定的一部分的详细信息）。</span><span class="sxs-lookup"><span data-stu-id="e22a9-126">Convention methods are decorated with hints that determine which actions it would apply to (details as part of authoring conventions).</span></span> <span data-ttu-id="e22a9-127">例如:</span><span class="sxs-lookup"><span data-stu-id="e22a9-127">For example:</span></span>

    [!code-csharp[](conventions/sample/Controllers/ContactsConventionController.cs?name=apiconventiontypeattribute)]

1. <span data-ttu-id="e22a9-128">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` 应用于程序集 &mdash; 将约定类型应用于当前程序集的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="e22a9-128">`Microsoft.AspNetCore.Mvc.ApiConventionTypeAttribute` applied to an assembly &mdash; Applies the convention type to all controllers in the current assembly.</span></span> <span data-ttu-id="e22a9-129">例如:</span><span class="sxs-lookup"><span data-stu-id="e22a9-129">For example:</span></span>

    [!code-csharp[](conventions/sample/Startup.cs?name=apiconventiontypeattribute)]

## <a name="create-web-api-conventions"></a><span data-ttu-id="e22a9-130">创建 Web API 约定</span><span class="sxs-lookup"><span data-stu-id="e22a9-130">Create web API conventions</span></span>

<span data-ttu-id="e22a9-131">约定是带有方法的静态类型。</span><span class="sxs-lookup"><span data-stu-id="e22a9-131">A convention is a static type with methods.</span></span> <span data-ttu-id="e22a9-132">这些方法使用 `[ProducesResponseType]` 或 `[ProducesDefaultResponseType]` 属性进行批注。</span><span class="sxs-lookup"><span data-stu-id="e22a9-132">These methods are annotated with `[ProducesResponseType]` or `[ProducesDefaultResponseType]` attributes.</span></span>

```csharp
public static class MyAppConventions
{
    [ProducesResponseType(200)]
    [ProducesResponseType(404)]
    public static void Find(int id)
    {
    }
}
```

<span data-ttu-id="e22a9-133">将此约定应用于程序集会导致约定方法应用于名称为 `Find` 的任何操作，并且在这些约定方法不具有其他更明确的元数据属性情况下，它们只有一个名为 `id` 的参数。</span><span class="sxs-lookup"><span data-stu-id="e22a9-133">Applying this convention to an assembly results in the convention method applying to any action with the name `Find` and having exactly one parameter named `id`, as long as they don't have other more specific metadata attributes.</span></span>

<span data-ttu-id="e22a9-134">除了 `[ProducesResponseType]` 和 `[ProducesDefaultResponseType]` 之外，`[ApiConventionNameMatch]` 和 `[ApiConventionTypeMatch]` 还可应用于确定它们所适用的方法的约定方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-134">In addition to `[ProducesResponseType]` and `[ProducesDefaultResponseType]`, `[ApiConventionNameMatch]` and `[ApiConventionTypeMatch]` can be applied to the convention method that determines the methods they apply to.</span></span> <span data-ttu-id="e22a9-135">例如:</span><span class="sxs-lookup"><span data-stu-id="e22a9-135">For example:</span></span>

```csharp
[ProducesResponseType(200)]
[ProducesResponseType(404)]
[ApiConventionNameMatch(ApiConventionNameMatchBehavior.Prefix)]
public static void Find(
    [ApiConventionNameMatch(ApiConventionNameMatchBehavior.Suffix)]
    int id)
{ }
```

* <span data-ttu-id="e22a9-136">应用于该方法的 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` 选项表示该约定可匹配任何操作，前提是以“Find”作为前缀。</span><span class="sxs-lookup"><span data-stu-id="e22a9-136">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Prefix` option applied to the method, indicates that the convention can match any action as long as it's prefixed with "Find".</span></span> <span data-ttu-id="e22a9-137">这包括 `Find`、`FindPet` 或 `FindById` 等方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-137">This includes methods such as `Find`, `FindPet`, or `FindById`.</span></span>
* <span data-ttu-id="e22a9-138">应用于该参数的 `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix` 表示该约定可匹配以标识符作为后缀结尾的唯一参数的方法。</span><span class="sxs-lookup"><span data-stu-id="e22a9-138">The `Microsoft.AspNetCore.Mvc.ApiExplorer.ApiConventionNameMatchBehavior.Suffix` applied to the parameter indicates that the convention can match methods with exactly one parameter ending in the suffix identifier.</span></span> <span data-ttu-id="e22a9-139">这包括 `id` 或 `petId` 等参数。</span><span class="sxs-lookup"><span data-stu-id="e22a9-139">This includes parameters such as `id` or `petId`.</span></span> <span data-ttu-id="e22a9-140">与此类似，可将 `ApiConventionTypeMatch` 应用于类型，以约束参数的类型。</span><span class="sxs-lookup"><span data-stu-id="e22a9-140">`ApiConventionTypeMatch` can be similarly applied to types to constrain the type of the parameter.</span></span> <span data-ttu-id="e22a9-141">`params[]` 参数可用于指示无需显式匹配的剩余参数。</span><span class="sxs-lookup"><span data-stu-id="e22a9-141">A `params[]` argument can be used to indicate remaining parameters that don't need to be explicitly matched.</span></span>
