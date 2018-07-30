---
title: ASP.NET Core 中基于资源的授权
author: scottaddie
description: 了解如何在 ASP.NET Core 应用程序中实现的基于资源的授权，Authorize 属性不会满足要求。
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
uid: security/authorization/resourcebased
ms.openlocfilehash: 6a110a69c58d5e20a15198378510486daec3d452
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342284"
---
# <a name="resource-based-authorization-in-aspnet-core"></a><span data-ttu-id="ba10e-103">ASP.NET Core 中基于资源的授权</span><span class="sxs-lookup"><span data-stu-id="ba10e-103">Resource-based authorization in ASP.NET Core</span></span>

<span data-ttu-id="ba10e-104">授权策略取决于要访问的资源。</span><span class="sxs-lookup"><span data-stu-id="ba10e-104">Authorization strategy depends upon the resource being accessed.</span></span> <span data-ttu-id="ba10e-105">请考虑具有作者属性的文档。</span><span class="sxs-lookup"><span data-stu-id="ba10e-105">Consider a document which has an author property.</span></span> <span data-ttu-id="ba10e-106">允许仅作者更新文档。</span><span class="sxs-lookup"><span data-stu-id="ba10e-106">Only the author is allowed to update the document.</span></span> <span data-ttu-id="ba10e-107">因此，文档必须检索从数据存储区进行授权评估之前。</span><span class="sxs-lookup"><span data-stu-id="ba10e-107">Consequently, the document must be retrieved from the data store before authorization evaluation can occur.</span></span>

<span data-ttu-id="ba10e-108">数据绑定之前和之后，页面处理程序或将文档加载操作的执行进行属性评估。</span><span class="sxs-lookup"><span data-stu-id="ba10e-108">Attribute evaluation occurs before data binding and before execution of the page handler or action which loads the document.</span></span> <span data-ttu-id="ba10e-109">出于这些原因，使用声明性授权`[Authorize]`属性不能。</span><span class="sxs-lookup"><span data-stu-id="ba10e-109">For these reasons, declarative authorization with an `[Authorize]` attribute won't suffice.</span></span> <span data-ttu-id="ba10e-110">相反，可以调用自定义授权方法&mdash;称为命令性授权的样式。</span><span class="sxs-lookup"><span data-stu-id="ba10e-110">Instead, you can invoke a custom authorization method&mdash;a style known as imperative authorization.</span></span>

<span data-ttu-id="ba10e-111">使用[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples)([如何下载](xref:tutorials/index#how-to-download-a-sample)) 若要了解本主题中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="ba10e-111">Use the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

<span data-ttu-id="ba10e-112">[使用受授权的用户数据创建 ASP.NET Core 应用](xref:security/authorization/secure-data)包含的示例应用程序使用的基于资源的授权。</span><span class="sxs-lookup"><span data-stu-id="ba10e-112">[Create an ASP.NET Core app with user data protected by authorization](xref:security/authorization/secure-data) contains a sample app that uses resource-based authorization.</span></span>

## <a name="use-imperative-authorization"></a><span data-ttu-id="ba10e-113">使用命令性授权</span><span class="sxs-lookup"><span data-stu-id="ba10e-113">Use imperative authorization</span></span>

<span data-ttu-id="ba10e-114">授权作为实现[IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice)服务并注册内的服务集合中`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="ba10e-114">Authorization is implemented as an [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) service and is registered in the service collection within the `Startup` class.</span></span> <span data-ttu-id="ba10e-115">该服务可通过[依赖关系注入](xref:fundamentals/dependency-injection)页面处理程序或进行操作。</span><span class="sxs-lookup"><span data-stu-id="ba10e-115">The service is made available via [dependency injection](xref:fundamentals/dependency-injection) to page handlers or actions.</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

<span data-ttu-id="ba10e-116">`IAuthorizationService` 具有两个`AuthorizeAsync`方法重载： 一个接受资源和策略名称和其他接受资源和要求来评估的列表。</span><span class="sxs-lookup"><span data-stu-id="ba10e-116">`IAuthorizationService` has two `AuthorizeAsync` method overloads: one accepting the resource and the policy name and the other accepting the resource and a list of requirements to evaluate.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ba10e-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ba10e-118">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-118">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

---

<a name="security-authorization-resource-based-imperative"></a>

<span data-ttu-id="ba10e-119">在以下示例中，要保护的资源加载到自定义`Document`对象。</span><span class="sxs-lookup"><span data-stu-id="ba10e-119">In the following example, the resource to be secured is loaded into a custom `Document` object.</span></span> <span data-ttu-id="ba10e-120">`AuthorizeAsync`重载进行调用以确定当前用户是否允许编辑提供的文档。</span><span class="sxs-lookup"><span data-stu-id="ba10e-120">An `AuthorizeAsync` overload is invoked to determine whether the current user is allowed to edit the provided document.</span></span> <span data-ttu-id="ba10e-121">自定义"EditPolicy"授权策略可分解为决策。</span><span class="sxs-lookup"><span data-stu-id="ba10e-121">A custom "EditPolicy" authorization policy is factored into the decision.</span></span> <span data-ttu-id="ba10e-122">请参阅[自定义基于策略的授权](xref:security/authorization/policies)创建授权策略的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ba10e-122">See [Custom policy-based authorization](xref:security/authorization/policies) for more on creating authorization policies.</span></span>

> [!NOTE]
> <span data-ttu-id="ba10e-123">下面的代码示例假定已经运行了身份验证和组`User`属性。</span><span class="sxs-lookup"><span data-stu-id="ba10e-123">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ba10e-124">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-124">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ba10e-125">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-125">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a><span data-ttu-id="ba10e-126">编写基于资源的处理程序</span><span class="sxs-lookup"><span data-stu-id="ba10e-126">Write a resource-based handler</span></span>

<span data-ttu-id="ba10e-127">编写处理程序的基于资源的授权没有太大区别比[编写普通要求处理程序](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler)。</span><span class="sxs-lookup"><span data-stu-id="ba10e-127">Writing a handler for resource-based authorization isn't much different than [writing a plain requirements handler](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler).</span></span> <span data-ttu-id="ba10e-128">创建自定义要求类，并实现要求处理程序类。</span><span class="sxs-lookup"><span data-stu-id="ba10e-128">Create a custom requirement class, and implement a requirement handler class.</span></span> <span data-ttu-id="ba10e-129">处理程序类指定的要求和资源类型。</span><span class="sxs-lookup"><span data-stu-id="ba10e-129">The handler class specifies both the requirement and resource type.</span></span> <span data-ttu-id="ba10e-130">例如，处理程序利用`SameAuthorRequirement`要求和`Document`资源如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba10e-130">For example, a handler utilizing a `SameAuthorRequirement` requirement and a `Document` resource looks as follows:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ba10e-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ba10e-132">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-132">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

<span data-ttu-id="ba10e-133">注册的要求和处理程序中的`Startup.ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="ba10e-133">Register the requirement and handler in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a><span data-ttu-id="ba10e-134">操作要求</span><span class="sxs-lookup"><span data-stu-id="ba10e-134">Operational requirements</span></span>

<span data-ttu-id="ba10e-135">若要进行决策基于 CRUD （创建、 读取、 更新、 删除） 操作的结果，请使用[OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement)帮助器类。</span><span class="sxs-lookup"><span data-stu-id="ba10e-135">If you're making decisions based on the outcomes of CRUD (Create, Read, Update, Delete) operations, use the [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) helper class.</span></span> <span data-ttu-id="ba10e-136">此类，可为每个操作类型编写单个处理程序而不是单独的类。</span><span class="sxs-lookup"><span data-stu-id="ba10e-136">This class enables you to write a single handler instead of an individual class for each operation type.</span></span> <span data-ttu-id="ba10e-137">若要使用它，提供一些操作名称：</span><span class="sxs-lookup"><span data-stu-id="ba10e-137">To use it, provide some operation names:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

<span data-ttu-id="ba10e-138">处理程序的实现，如下所示，使用`OperationAuthorizationRequirement`要求和`Document`资源：</span><span class="sxs-lookup"><span data-stu-id="ba10e-138">The handler is implemented as follows, using an `OperationAuthorizationRequirement` requirement and a `Document` resource:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ba10e-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ba10e-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

<span data-ttu-id="ba10e-141">前面的处理程序验证该操作使用的资源、 用户的标识和需求的`Name`属性。</span><span class="sxs-lookup"><span data-stu-id="ba10e-141">The preceding handler validates the operation using the resource, the user's identity, and the requirement's `Name` property.</span></span>

<span data-ttu-id="ba10e-142">若要调用的操作的资源处理程序，指定该操作时调用`AuthorizeAsync`页面处理程序或操作中。</span><span class="sxs-lookup"><span data-stu-id="ba10e-142">To call an operational resource handler, specify the operation when invoking `AuthorizeAsync` in your page handler or action.</span></span> <span data-ttu-id="ba10e-143">下面的示例确定是否允许经过身份验证的用户若要查看提供的文档。</span><span class="sxs-lookup"><span data-stu-id="ba10e-143">The following example determines whether the authenticated user is permitted to view the provided document.</span></span>

> [!NOTE]
> <span data-ttu-id="ba10e-144">下面的代码示例假定已经运行了身份验证和组`User`属性。</span><span class="sxs-lookup"><span data-stu-id="ba10e-144">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ba10e-145">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

<span data-ttu-id="ba10e-146">如果授权成功，则返回查看文档的页。</span><span class="sxs-lookup"><span data-stu-id="ba10e-146">If authorization succeeds, the page for viewing the document is returned.</span></span> <span data-ttu-id="ba10e-147">如果授权失败而用户进行身份验证，返回`ForbidResult`通知授权失败的任何身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="ba10e-147">If authorization fails but the user is authenticated, returning `ForbidResult` informs any authentication middleware that authorization failed.</span></span> <span data-ttu-id="ba10e-148">一个`ChallengeResult`时必须执行身份验证，将返回。</span><span class="sxs-lookup"><span data-stu-id="ba10e-148">A `ChallengeResult` is returned when authentication must be performed.</span></span> <span data-ttu-id="ba10e-149">对于交互式浏览器客户端，可能需要将用户重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="ba10e-149">For interactive browser clients, it may be appropriate to redirect the user to a login page.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ba10e-150">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ba10e-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

<span data-ttu-id="ba10e-151">如果授权成功，则返回文档的视图。</span><span class="sxs-lookup"><span data-stu-id="ba10e-151">If authorization succeeds, the view for the document is returned.</span></span> <span data-ttu-id="ba10e-152">如果授权失败，返回`ChallengeResult`授权失败，并将中间件可以采取适当的响应将通知任何身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="ba10e-152">If authorization fails, returning `ChallengeResult` informs any authentication middleware that authorization failed, and the middleware can take the appropriate response.</span></span> <span data-ttu-id="ba10e-153">相应的响应可能返回 401 或 403 状态代码。</span><span class="sxs-lookup"><span data-stu-id="ba10e-153">An appropriate response could be returning a 401 or 403 status code.</span></span> <span data-ttu-id="ba10e-154">对于交互式浏览器客户端，这可能意味着将用户重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="ba10e-154">For interactive browser clients, it could mean redirecting the user to a login page.</span></span>

---
