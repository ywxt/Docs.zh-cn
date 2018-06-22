---
title: ASP.NET 核心中基于资源的授权
author: scottaddie
description: 了解如何在 ASP.NET Core 应用程序中实现的基于资源的授权，Authorize 属性不会满足要求。
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
uid: security/authorization/resourcebased
ms.openlocfilehash: 577af3ba45361aec715a49fa59b9ec9869ced851
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273342"
---
# <a name="resource-based-authorization-in-aspnet-core"></a><span data-ttu-id="88eae-103">ASP.NET 核心中基于资源的授权</span><span class="sxs-lookup"><span data-stu-id="88eae-103">Resource-based authorization in ASP.NET Core</span></span>

<span data-ttu-id="88eae-104">授权策略取决于要访问的资源。</span><span class="sxs-lookup"><span data-stu-id="88eae-104">Authorization strategy depends upon the resource being accessed.</span></span> <span data-ttu-id="88eae-105">请考虑具有 author 属性的文档。</span><span class="sxs-lookup"><span data-stu-id="88eae-105">Consider a document which has an author property.</span></span> <span data-ttu-id="88eae-106">仅作者允许更新文档。</span><span class="sxs-lookup"><span data-stu-id="88eae-106">Only the author is allowed to update the document.</span></span> <span data-ttu-id="88eae-107">因此，该文档必须检索从数据存储区授权评估才能发生。</span><span class="sxs-lookup"><span data-stu-id="88eae-107">Consequently, the document must be retrieved from the data store before authorization evaluation can occur.</span></span>

<span data-ttu-id="88eae-108">在绑定数据之前和的页处理或加载文档的操作执行之前会进行属性评估。</span><span class="sxs-lookup"><span data-stu-id="88eae-108">Attribute evaluation occurs before data binding and before execution of the page handler or action which loads the document.</span></span> <span data-ttu-id="88eae-109">出于这些原因，使用的声明性授权`[Authorize]`属性不能满足要求。</span><span class="sxs-lookup"><span data-stu-id="88eae-109">For these reasons, declarative authorization with an `[Authorize]` attribute won't suffice.</span></span> <span data-ttu-id="88eae-110">相反，你可以调用自定义授权方法&mdash;称为命令性授权的样式。</span><span class="sxs-lookup"><span data-stu-id="88eae-110">Instead, you can invoke a custom authorization method&mdash;a style known as imperative authorization.</span></span>

<span data-ttu-id="88eae-111">使用[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples)([如何下载](xref:tutorials/index#how-to-download-a-sample)) 来浏览本主题中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="88eae-111">Use the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

<span data-ttu-id="88eae-112">[使用受授权的用户数据创建 ASP.NET Core 应用](xref:security/authorization/secure-data)包含的示例应用程序使用的基于资源的授权。</span><span class="sxs-lookup"><span data-stu-id="88eae-112">[Create an ASP.NET Core app with user data protected by authorization](xref:security/authorization/secure-data) contains a sample app that uses resource-based authorization.</span></span>

## <a name="use-imperative-authorization"></a><span data-ttu-id="88eae-113">使用命令性授权</span><span class="sxs-lookup"><span data-stu-id="88eae-113">Use imperative authorization</span></span>

<span data-ttu-id="88eae-114">作为实现授权[IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice)服务并在服务集合中注册`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="88eae-114">Authorization is implemented as an [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) service and is registered in the service collection within the `Startup` class.</span></span> <span data-ttu-id="88eae-115">该服务可通过[依赖关系注入](xref:fundamentals/dependency-injection#fundamentals-dependency-injection)对页处理程序或操作。</span><span class="sxs-lookup"><span data-stu-id="88eae-115">The service is made available via [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) to page handlers or actions.</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

<span data-ttu-id="88eae-116">`IAuthorizationService` 有两个`AuthorizeAsync`方法重载： 一个接收资源和策略名称和其他接受资源和要求来评估的列表。</span><span class="sxs-lookup"><span data-stu-id="88eae-116">`IAuthorizationService` has two `AuthorizeAsync` method overloads: one accepting the resource and the policy name and the other accepting the resource and a list of requirements to evaluate.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="88eae-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="88eae-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="88eae-118">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="88eae-118">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

<span data-ttu-id="88eae-119">在下面的示例中，要保护的资源加载到一个自定义`Document`对象。</span><span class="sxs-lookup"><span data-stu-id="88eae-119">In the following example, the resource to be secured is loaded into a custom `Document` object.</span></span> <span data-ttu-id="88eae-120">`AuthorizeAsync`重载进行调用以确定是否允许当前用户编辑提供的文档。</span><span class="sxs-lookup"><span data-stu-id="88eae-120">An `AuthorizeAsync` overload is invoked to determine whether the current user is allowed to edit the provided document.</span></span> <span data-ttu-id="88eae-121">自定义"EditPolicy"授权策略被分解为决策因子。</span><span class="sxs-lookup"><span data-stu-id="88eae-121">A custom "EditPolicy" authorization policy is factored into the decision.</span></span> <span data-ttu-id="88eae-122">请参阅[自定义基于策略的授权](xref:security/authorization/policies)创建授权策略的详细信息。</span><span class="sxs-lookup"><span data-stu-id="88eae-122">See [Custom policy-based authorization](xref:security/authorization/policies) for more on creating authorization policies.</span></span>

> [!NOTE]
> <span data-ttu-id="88eae-123">下面的代码示例假定已经运行了身份验证和集`User`属性。</span><span class="sxs-lookup"><span data-stu-id="88eae-123">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="88eae-124">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="88eae-124">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="88eae-125">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="88eae-125">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a><span data-ttu-id="88eae-126">基于资源的处理程序编写</span><span class="sxs-lookup"><span data-stu-id="88eae-126">Write a resource-based handler</span></span>

<span data-ttu-id="88eae-127">编写处理程序的基于资源的授权不大的不同比[编写纯要求处理程序](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler)。</span><span class="sxs-lookup"><span data-stu-id="88eae-127">Writing a handler for resource-based authorization isn't much different than [writing a plain requirements handler](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler).</span></span> <span data-ttu-id="88eae-128">创建自定义要求类，并实现要求处理程序类。</span><span class="sxs-lookup"><span data-stu-id="88eae-128">Create a custom requirement class, and implement a requirement handler class.</span></span> <span data-ttu-id="88eae-129">处理程序类指定的要求和资源类型。</span><span class="sxs-lookup"><span data-stu-id="88eae-129">The handler class specifies both the requirement and resource type.</span></span> <span data-ttu-id="88eae-130">例如，处理程序利用`SameAuthorRequirement`要求和`Document`资源将如下所示：</span><span class="sxs-lookup"><span data-stu-id="88eae-130">For example, a handler utilizing a `SameAuthorRequirement` requirement and a `Document` resource looks as follows:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="88eae-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="88eae-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="88eae-132">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="88eae-132">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

<span data-ttu-id="88eae-133">注册的要求和中的处理程序`Startup.ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="88eae-133">Register the requirement and handler in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a><span data-ttu-id="88eae-134">操作要求</span><span class="sxs-lookup"><span data-stu-id="88eae-134">Operational requirements</span></span>

<span data-ttu-id="88eae-135">如果你正在进行决策基于 CRUD （创建、 读取、 更新、 删除） 操作的结果，使用[OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement)帮助器类。</span><span class="sxs-lookup"><span data-stu-id="88eae-135">If you're making decisions based on the outcomes of CRUD (Create, Read, Update, Delete) operations, use the [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) helper class.</span></span> <span data-ttu-id="88eae-136">此类，可为每个操作类型编写单个处理程序而不是单独的类。</span><span class="sxs-lookup"><span data-stu-id="88eae-136">This class enables you to write a single handler instead of an individual class for each operation type.</span></span> <span data-ttu-id="88eae-137">若要使用此选项，提供一些操作名称：</span><span class="sxs-lookup"><span data-stu-id="88eae-137">To use it, provide some operation names:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

<span data-ttu-id="88eae-138">处理程序实现，如下所示，使用`OperationAuthorizationRequirement`要求和`Document`资源：</span><span class="sxs-lookup"><span data-stu-id="88eae-138">The handler is implemented as follows, using an `OperationAuthorizationRequirement` requirement and a `Document` resource:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="88eae-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="88eae-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="88eae-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="88eae-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

<span data-ttu-id="88eae-141">前面的处理程序验证使用的资源、 用户的标识和要求的操作`Name`属性。</span><span class="sxs-lookup"><span data-stu-id="88eae-141">The preceding handler validates the operation using the resource, the user's identity, and the requirement's `Name` property.</span></span>

<span data-ttu-id="88eae-142">若要调用的操作资源处理程序，指定该操作时调用`AuthorizeAsync`在页处理程序或操作。</span><span class="sxs-lookup"><span data-stu-id="88eae-142">To call an operational resource handler, specify the operation when invoking `AuthorizeAsync` in your page handler or action.</span></span> <span data-ttu-id="88eae-143">下面的示例确定是否允许经过身份验证的用户若要查看提供的文档。</span><span class="sxs-lookup"><span data-stu-id="88eae-143">The following example determines whether the authenticated user is permitted to view the provided document.</span></span>

> [!NOTE]
> <span data-ttu-id="88eae-144">下面的代码示例假定已经运行了身份验证和集`User`属性。</span><span class="sxs-lookup"><span data-stu-id="88eae-144">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="88eae-145">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="88eae-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

<span data-ttu-id="88eae-146">如果授权成功，则返回查看文档的页。</span><span class="sxs-lookup"><span data-stu-id="88eae-146">If authorization succeeds, the page for viewing the document is returned.</span></span> <span data-ttu-id="88eae-147">如果授权失败而用户进行身份验证，返回`ForbidResult`通知授权失败的任何身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="88eae-147">If authorization fails but the user is authenticated, returning `ForbidResult` informs any authentication middleware that authorization failed.</span></span> <span data-ttu-id="88eae-148">A`ChallengeResult`时必须执行身份验证返回。</span><span class="sxs-lookup"><span data-stu-id="88eae-148">A `ChallengeResult` is returned when authentication must be performed.</span></span> <span data-ttu-id="88eae-149">对于交互式浏览器客户端，可能适合将用户重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="88eae-149">For interactive browser clients, it may be appropriate to redirect the user to a login page.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="88eae-150">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="88eae-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

<span data-ttu-id="88eae-151">如果授权成功，则返回文档的视图。</span><span class="sxs-lookup"><span data-stu-id="88eae-151">If authorization succeeds, the view for the document is returned.</span></span> <span data-ttu-id="88eae-152">如果授权失败，返回`ChallengeResult`通知的任何身份验证中间件： 授权失败，并该中间件可以采取适当的响应。</span><span class="sxs-lookup"><span data-stu-id="88eae-152">If authorization fails, returning `ChallengeResult` informs any authentication middleware that authorization failed, and the middleware can take the appropriate response.</span></span> <span data-ttu-id="88eae-153">适当的响应无法返回状态代码为 401 或 403。</span><span class="sxs-lookup"><span data-stu-id="88eae-153">An appropriate response could be returning a 401 or 403 status code.</span></span> <span data-ttu-id="88eae-154">对于交互式浏览器客户端，这可能意味着将用户重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="88eae-154">For interactive browser clients, it could mean redirecting the user to a login page.</span></span>

---
