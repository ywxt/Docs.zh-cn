---
title: ASP.NET 核心 mvc 视图基于授权
author: rick-anderson
description: 本文档演示如何将注入和利用 ASP.NET 核心 Razor 视图内的授权服务。
manager: wpickett
ms.author: riande
ms.date: 10/30/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/views
ms.openlocfilehash: dad59a297efb4648755436fbd07742f95af97fb2
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
ms.locfileid: "30076628"
---
# <a name="view-based-authorization-in-aspnet-core-mvc"></a><span data-ttu-id="35cd5-103">ASP.NET 核心 mvc 视图基于授权</span><span class="sxs-lookup"><span data-stu-id="35cd5-103">View-based authorization in ASP.NET Core MVC</span></span>

<span data-ttu-id="35cd5-104">开发人员通常需要显示、 隐藏或修改基于当前的用户标识的用户界面。</span><span class="sxs-lookup"><span data-stu-id="35cd5-104">A developer often wants to show, hide, or otherwise modify a UI based on the current user identity.</span></span> <span data-ttu-id="35cd5-105">你可以访问授权服务在服务内通过的 MVC 视图[依赖关系注入](xref:fundamentals/dependency-injection#fundamentals-dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="35cd5-105">You can access the authorization service within MVC views via [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection).</span></span> <span data-ttu-id="35cd5-106">若要将授权服务注入到 Razor 视图中，使用`@inject`指令：</span><span class="sxs-lookup"><span data-stu-id="35cd5-106">To inject the authorization service into a Razor view, use the `@inject` directive:</span></span>

```cshtml
@using Microsoft.AspNetCore.Authorization
@inject IAuthorizationService AuthorizationService
```

<span data-ttu-id="35cd5-107">如果希望每个视图中的授权服务，将放置`@inject`指令插入 *_ViewImports.cshtml*文件*视图*目录。</span><span class="sxs-lookup"><span data-stu-id="35cd5-107">If you want the authorization service in every view, place the `@inject` directive into the *_ViewImports.cshtml* file of the *Views* directory.</span></span> <span data-ttu-id="35cd5-108">有关详细信息，请参阅[视图中的依赖关系注入](xref:mvc/views/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="35cd5-108">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

<span data-ttu-id="35cd5-109">使用插入的授权服务来调用`AuthorizeAsync`中完全相同的方式将检查期间[基于资源的授权](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span><span class="sxs-lookup"><span data-stu-id="35cd5-109">Use the injected authorization service to invoke `AuthorizeAsync` in exactly the same way you would check during [resource-based authorization](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="35cd5-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="35cd5-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, "PolicyName")).Succeeded)
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="35cd5-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="35cd5-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, "PolicyName"))
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

---

<span data-ttu-id="35cd5-112">在某些情况下，资源将视图模型。</span><span class="sxs-lookup"><span data-stu-id="35cd5-112">In some cases, the resource will be your view model.</span></span> <span data-ttu-id="35cd5-113">调用`AuthorizeAsync`中完全相同的方式将检查期间[基于资源的授权](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span><span class="sxs-lookup"><span data-stu-id="35cd5-113">Invoke `AuthorizeAsync` in exactly the same way you would check during [resource-based authorization](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="35cd5-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="35cd5-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit)).Succeeded)
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="35cd5-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="35cd5-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit))
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

---

<span data-ttu-id="35cd5-116">在前面的代码中，该模型作为资源应采取的策略评估传递纳入考虑范围。</span><span class="sxs-lookup"><span data-stu-id="35cd5-116">In the preceding code, the model is passed as a resource the policy evaluation should take into consideration.</span></span>

> [!WARNING]
> <span data-ttu-id="35cd5-117">不要依赖于与唯一的授权检查的应用程序的 UI 元素的切换可见性。</span><span class="sxs-lookup"><span data-stu-id="35cd5-117">Don't rely on toggling visibility of your app's UI elements as the sole authorization check.</span></span> <span data-ttu-id="35cd5-118">隐藏的 UI 元素可能无法完全阻止访问到其关联的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="35cd5-118">Hiding a UI element may not completely prevent access to its associated controller action.</span></span> <span data-ttu-id="35cd5-119">例如，考虑前面的代码段中的按钮。</span><span class="sxs-lookup"><span data-stu-id="35cd5-119">For example, consider the button in the preceding code snippet.</span></span> <span data-ttu-id="35cd5-120">用户可以调用`Edit`操作方法如果他或她知道的相对资源 URL 是 */Document/Edit/1*。</span><span class="sxs-lookup"><span data-stu-id="35cd5-120">A user can invoke the `Edit` action method if he or she knows the relative resource URL is */Document/Edit/1*.</span></span> <span data-ttu-id="35cd5-121">为此，`Edit`操作方法应执行其自己的授权检查。</span><span class="sxs-lookup"><span data-stu-id="35cd5-121">For this reason, the `Edit` action method should perform its own authorization check.</span></span>
