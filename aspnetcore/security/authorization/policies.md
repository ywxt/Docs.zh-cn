---
title: "ASP.NET 核心中基于策略的授权"
author: rick-anderson
description: "了解如何创建和使用授权策略处理程序，用于实施 ASP.NET Core 应用程序中的授权要求。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 11/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/policies
ms.openlocfilehash: a9ee7e6fd06fa88485d7f578a9df74cbf87d9540
ms.sourcegitcommit: 7ee6e7582421195cbd675355c970d3d292ee668d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="policy-based-authorization"></a><span data-ttu-id="87267-103">基于策略的授权</span><span class="sxs-lookup"><span data-stu-id="87267-103">Policy-based authorization</span></span>

<span data-ttu-id="87267-104">实际上，[基于角色的授权](xref:security/authorization/roles)和[基于声明的授权](xref:security/authorization/claims)使用要求，要求处理程序，并预先配置的策略。</span><span class="sxs-lookup"><span data-stu-id="87267-104">Underneath the covers, [role-based authorization](xref:security/authorization/roles) and [claims-based authorization](xref:security/authorization/claims) use a requirement, a requirement handler, and a pre-configured policy.</span></span> <span data-ttu-id="87267-105">这些构建基块支持在代码中的授权评估表达式。</span><span class="sxs-lookup"><span data-stu-id="87267-105">These building blocks support the expression of authorization evaluations in code.</span></span> <span data-ttu-id="87267-106">结果是一个更丰富、 可重复使用、 可测试授权结构。</span><span class="sxs-lookup"><span data-stu-id="87267-106">The result is a richer, reusable, testable authorization structure.</span></span>

<span data-ttu-id="87267-107">授权策略包含一个或多个要求。</span><span class="sxs-lookup"><span data-stu-id="87267-107">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="87267-108">在中注册的授权服务配置中，一部分`Startup.ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="87267-108">It's registered as part of the authorization service configuration, in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

<span data-ttu-id="87267-109">在前面的示例中，创建一个"AtLeast21"策略。</span><span class="sxs-lookup"><span data-stu-id="87267-109">In the preceding example, an "AtLeast21" policy is created.</span></span> <span data-ttu-id="87267-110">它具有单个要求&mdash;的最短期限，它提供作为参数传递给要求。</span><span class="sxs-lookup"><span data-stu-id="87267-110">It has a single requirement&mdash;that of a minimum age, which is supplied as a parameter to the requirement.</span></span>

<span data-ttu-id="87267-111">通过使用应用策略`[Authorize]`具有策略名称属性。</span><span class="sxs-lookup"><span data-stu-id="87267-111">Policies are applied by using the `[Authorize]` attribute with the policy name.</span></span> <span data-ttu-id="87267-112">例如:</span><span class="sxs-lookup"><span data-stu-id="87267-112">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a><span data-ttu-id="87267-113">惠?</span><span class="sxs-lookup"><span data-stu-id="87267-113">Requirements</span></span>

<span data-ttu-id="87267-114">授权要求是一个策略可用于评估当前的用户主体的数据参数的集合。</span><span class="sxs-lookup"><span data-stu-id="87267-114">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="87267-115">在我们的"AtLeast21"策略的要求是单个参数&mdash;最小存在时间。</span><span class="sxs-lookup"><span data-stu-id="87267-115">In our "AtLeast21" policy, the requirement is a single parameter&mdash;the minimum age.</span></span> <span data-ttu-id="87267-116">要求实现[IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement)，这是一个空标记接口。</span><span class="sxs-lookup"><span data-stu-id="87267-116">A requirement implements [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), which is an empty marker interface.</span></span> <span data-ttu-id="87267-117">参数化的最小年龄要求无法实现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87267-117">A parameterized minimum age requirement could be implemented as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> <span data-ttu-id="87267-118">一项要求不需要具有数据或属性。</span><span class="sxs-lookup"><span data-stu-id="87267-118">A requirement doesn't need to have data or properties.</span></span>

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a><span data-ttu-id="87267-119">授权处理程序</span><span class="sxs-lookup"><span data-stu-id="87267-119">Authorization handlers</span></span>

<span data-ttu-id="87267-120">授权处理程序负责的要求的属性求值。</span><span class="sxs-lookup"><span data-stu-id="87267-120">An authorization handler is responsible for the evaluation of a requirement's properties.</span></span> <span data-ttu-id="87267-121">授权处理程序会评估要求，针对提供[AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext)以确定是否允许访问。</span><span class="sxs-lookup"><span data-stu-id="87267-121">The authorization handler evaluates the requirements against a provided [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext) to determine if access is allowed.</span></span>

<span data-ttu-id="87267-122">可以有一项要求[多个处理程序](#security-authorization-policies-based-multiple-handlers)。</span><span class="sxs-lookup"><span data-stu-id="87267-122">A requirement can have [multiple handlers](#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="87267-123">处理程序可以继承[AuthorizationHandler\<TRequirement >](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1)，其中`TRequirement`是要处理的要求。</span><span class="sxs-lookup"><span data-stu-id="87267-123">A handler may inherit [AuthorizationHandler\<TRequirement>](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1), where `TRequirement` is the requirement to be handled.</span></span> <span data-ttu-id="87267-124">或者，可以实现一个处理程序[IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler)以处理多个类型的要求。</span><span class="sxs-lookup"><span data-stu-id="87267-124">Alternatively, a handler may implement [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) to handle more than one type of requirement.</span></span>

### <a name="use-a-handler-for-one-requirement"></a><span data-ttu-id="87267-125">为一个要求使用一个处理程序</span><span class="sxs-lookup"><span data-stu-id="87267-125">Use a handler for one requirement</span></span>

<a name="security-authorization-handler-example"></a>

<span data-ttu-id="87267-126">下面是在其中的最小存在时间处理利用单个要求一对一关系的一个示例：</span><span class="sxs-lookup"><span data-stu-id="87267-126">The following is an example of a one-to-one relationship in which a minimum age handler utilizes a single requirement:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

<span data-ttu-id="87267-127">前面的代码确定当前的用户主体是否声明已知且受信任的颁发者已发出的出生日期。</span><span class="sxs-lookup"><span data-stu-id="87267-127">The preceding code determines if the current user principal has a date of birth claim which has been issued by a known and trusted Issuer.</span></span> <span data-ttu-id="87267-128">授权不能出现缺少声明时，在这种情况下返回的已完成的任务。</span><span class="sxs-lookup"><span data-stu-id="87267-128">Authorization can't occur when the claim is missing, in which case a completed task is returned.</span></span> <span data-ttu-id="87267-129">在不存在声明，计算用户的年龄。</span><span class="sxs-lookup"><span data-stu-id="87267-129">When a claim is present, the user's age is calculated.</span></span> <span data-ttu-id="87267-130">如果该用户满足定义的要求的最短期限，授权视为成功。</span><span class="sxs-lookup"><span data-stu-id="87267-130">If the user meets the minimum age defined by the requirement, authorization is deemed successful.</span></span> <span data-ttu-id="87267-131">授权成功后，`context.Succeed`调用与作为其唯一的参数满足要求。</span><span class="sxs-lookup"><span data-stu-id="87267-131">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

### <a name="use-a-handler-for-multiple-requirements"></a><span data-ttu-id="87267-132">用于多个要求的处理程序</span><span class="sxs-lookup"><span data-stu-id="87267-132">Use a handler for multiple requirements</span></span>

<span data-ttu-id="87267-133">下面是在其中权限处理程序使用三个要求一个对多关系的一个示例：</span><span class="sxs-lookup"><span data-stu-id="87267-133">The following is an example of a one-to-many relationship in which a permission handler utilizes three requirements:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/PermissionHandler.cs?name=snippet_PermissionHandlerClass)]

<span data-ttu-id="87267-134">前面的代码遍历[PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;不包含要求的属性标记为成功。</span><span class="sxs-lookup"><span data-stu-id="87267-134">The preceding code traverses [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;a property containing requirements not marked as successful.</span></span> <span data-ttu-id="87267-135">如果用户具有读取权限，他或她必须是所有者或发起人访问请求的资源。</span><span class="sxs-lookup"><span data-stu-id="87267-135">If the user has read permission, he or she must be either an owner or a sponsor to access the requested resource.</span></span> <span data-ttu-id="87267-136">如果用户已编辑或删除权限，他或她必须所有者才能访问请求的资源。</span><span class="sxs-lookup"><span data-stu-id="87267-136">If the user has edit or delete permission, he or she must be an owner to access the requested resource.</span></span> <span data-ttu-id="87267-137">授权成功后，`context.Succeed`调用与作为其唯一的参数满足要求。</span><span class="sxs-lookup"><span data-stu-id="87267-137">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a><span data-ttu-id="87267-138">处理程序注册</span><span class="sxs-lookup"><span data-stu-id="87267-138">Handler registration</span></span>

<span data-ttu-id="87267-139">在配置期间服务集合中注册处理程序。</span><span class="sxs-lookup"><span data-stu-id="87267-139">Handlers are registered in the services collection during configuration.</span></span> <span data-ttu-id="87267-140">例如:</span><span class="sxs-lookup"><span data-stu-id="87267-140">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

<span data-ttu-id="87267-141">每个处理程序添加到服务集合，通过调用`services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`。</span><span class="sxs-lookup"><span data-stu-id="87267-141">Each handler is added to the services collection by invoking `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="87267-142">处理程序应返回？</span><span class="sxs-lookup"><span data-stu-id="87267-142">What should a handler return?</span></span>

<span data-ttu-id="87267-143">请注意，`Handle`中的方法[处理程序示例](#security-authorization-handler-example)不返回值。</span><span class="sxs-lookup"><span data-stu-id="87267-143">Note that the `Handle` method in the [handler example](#security-authorization-handler-example) returns no value.</span></span> <span data-ttu-id="87267-144">是的成功或失败指示的状态如何？</span><span class="sxs-lookup"><span data-stu-id="87267-144">How is a status of either success or failure indicated?</span></span>

* <span data-ttu-id="87267-145">处理程序通过调用中表示成功`context.Succeed(IAuthorizationRequirement requirement)`，将要求传递成功验证。</span><span class="sxs-lookup"><span data-stu-id="87267-145">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="87267-146">处理程序不需要一般情况下，处理失败，因为其他处理程序相同的要求可能会成功。</span><span class="sxs-lookup"><span data-stu-id="87267-146">A handler doesn't need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="87267-147">若要确保失败，即使其他要求处理程序成功，调用`context.Fail`。</span><span class="sxs-lookup"><span data-stu-id="87267-147">To guarantee failure, even if other requirement handlers succeed, call `context.Fail`.</span></span>

<span data-ttu-id="87267-148">当设置为`false`、 [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure)属性 （位于 ASP.NET 核心 1.1 和更高版本） 会使短路执行的处理程序时`context.Fail`调用。</span><span class="sxs-lookup"><span data-stu-id="87267-148">When set to `false`, the [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) property (available in ASP.NET Core 1.1 and later) short-circuits the execution of handlers when `context.Fail` is called.</span></span> <span data-ttu-id="87267-149">`InvokeHandlersAfterFailure` 默认为`true`，在这种情况下调用所有处理程序。</span><span class="sxs-lookup"><span data-stu-id="87267-149">`InvokeHandlersAfterFailure` defaults to `true`, in which case all handlers are called.</span></span> <span data-ttu-id="87267-150">这样要求以产生副作用，例如日志记录，这些始终发生即使`context.Fail`已在另一个处理程序调用。</span><span class="sxs-lookup"><span data-stu-id="87267-150">This allows requirements to produce side effects, such as logging, which always take place even if `context.Fail` has been called in another handler.</span></span>

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="87267-151">为什么将需要一项要求的多个处理程序？</span><span class="sxs-lookup"><span data-stu-id="87267-151">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="87267-152">在要评估上的情况下**或**基础，实现单个要求的多个处理程序。</span><span class="sxs-lookup"><span data-stu-id="87267-152">In cases where you want evaluation to be on an **OR** basis, implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="87267-153">例如，Microsoft 已使用密钥卡仅打开的门。</span><span class="sxs-lookup"><span data-stu-id="87267-153">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="87267-154">如果你在家离开你密钥卡，接线员打印临时不干胶标签，并为你打开大门。</span><span class="sxs-lookup"><span data-stu-id="87267-154">If you leave your key card at home, the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="87267-155">在此方案中，您将需要单个， *BuildingEntry*，但多个处理程序，每个检查单个要求。</span><span class="sxs-lookup"><span data-stu-id="87267-155">In this scenario, you'd have a single requirement, *BuildingEntry*, but multiple handlers, each one examining a single requirement.</span></span>

<span data-ttu-id="87267-156">*BuildingEntryRequirement.cs*</span><span class="sxs-lookup"><span data-stu-id="87267-156">*BuildingEntryRequirement.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

<span data-ttu-id="87267-157">*BadgeEntryHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="87267-157">*BadgeEntryHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

<span data-ttu-id="87267-158">*TemporaryStickerHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="87267-158">*TemporaryStickerHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

<span data-ttu-id="87267-159">确保这两个处理程序[注册](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)。</span><span class="sxs-lookup"><span data-stu-id="87267-159">Ensure that both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration).</span></span> <span data-ttu-id="87267-160">如果任一处理程序成功时策略的计算结果`BuildingEntryRequirement`，策略评估成功。</span><span class="sxs-lookup"><span data-stu-id="87267-160">If either handler succeeds when a policy evaluates the `BuildingEntryRequirement`, the policy evaluation succeeds.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="87267-161">使用 func 来实现策略</span><span class="sxs-lookup"><span data-stu-id="87267-161">Using a func to fulfill a policy</span></span>

<span data-ttu-id="87267-162">可能有哪些履行策略是简单代码中表示的情况。</span><span class="sxs-lookup"><span data-stu-id="87267-162">There may be situations in which fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="87267-163">可以提供`Func<AuthorizationHandlerContext, bool>`配置与你的策略时`RequireAssertion`策略生成器。</span><span class="sxs-lookup"><span data-stu-id="87267-163">It's possible to supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="87267-164">例如，以前`BadgeEntryHandler`无法，如下所示重写：</span><span class="sxs-lookup"><span data-stu-id="87267-164">For example, the previous `BadgeEntryHandler` could be rewritten as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="87267-165">访问在处理程序的 MVC 请求上下文</span><span class="sxs-lookup"><span data-stu-id="87267-165">Accessing MVC request context in handlers</span></span>

<span data-ttu-id="87267-166">`HandleRequirementAsync`授权处理程序中实现的方法具有两个参数：`AuthorizationHandlerContext`和`TRequirement`正在处理。</span><span class="sxs-lookup"><span data-stu-id="87267-166">The `HandleRequirementAsync` method you implement in an authorization handler has two parameters: an `AuthorizationHandlerContext` and the `TRequirement` you are handling.</span></span> <span data-ttu-id="87267-167">框架，例如 MVC 或 Jabbr 可用于任何将对象添加到`Resource`属性`AuthorizationHandlerContext`传递额外信息。</span><span class="sxs-lookup"><span data-stu-id="87267-167">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationHandlerContext` to pass extra information.</span></span>

<span data-ttu-id="87267-168">例如，MVC 传递的实例的[AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)中`Resource`属性。</span><span class="sxs-lookup"><span data-stu-id="87267-168">For example, MVC passes an instance of [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) in the `Resource` property.</span></span> <span data-ttu-id="87267-169">此属性提供访问权限`HttpContext`， `RouteData`，以及其他和提供的 MVC Razor 页的所有内容。</span><span class="sxs-lookup"><span data-stu-id="87267-169">This property provides access to `HttpContext`, `RouteData`, and everything else provided by MVC and Razor Pages.</span></span>

<span data-ttu-id="87267-170">使用`Resource`属性是特定于框架。</span><span class="sxs-lookup"><span data-stu-id="87267-170">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="87267-171">使用中的信息`Resource`属性限制到特定的框架你授权策略。</span><span class="sxs-lookup"><span data-stu-id="87267-171">Using information in the `Resource` property limits your authorization policies to particular frameworks.</span></span> <span data-ttu-id="87267-172">应强制转换`Resource`属性使用`as`关键字，然后确认该强制转换具有成功以确保你的代码不崩溃与`InvalidCastException`其他框架上运行时：</span><span class="sxs-lookup"><span data-stu-id="87267-172">You should cast the `Resource` property using the `as` keyword, and then confirm the cast has succeed to ensure your code doesn't crash with an `InvalidCastException` when run on other frameworks:</span></span>

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
