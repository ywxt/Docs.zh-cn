---
title: "在 ASP.NET 核心的自定义基于策略的授权"
author: rick-anderson
description: "了解如何创建和使用自定义授权策略处理程序，用于实施 ASP.NET Core 应用程序中的授权要求。"
ms.author: riande
ms.custom: mvc
manager: wpickett
ms.date: 11/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/policies
ms.openlocfilehash: c249985a6266483d47f447ac4a232546ed2b2708
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="custom-policy-based-authorization"></a><span data-ttu-id="b3af8-103">自定义的基于策略的授权</span><span class="sxs-lookup"><span data-stu-id="b3af8-103">Custom policy-based authorization</span></span>

<span data-ttu-id="b3af8-104">实际上，[基于角色的授权](xref:security/authorization/roles)和[基于声明的授权](xref:security/authorization/claims)使用要求，要求处理程序，并预先配置的策略。</span><span class="sxs-lookup"><span data-stu-id="b3af8-104">Underneath the covers, [role-based authorization](xref:security/authorization/roles) and [claims-based authorization](xref:security/authorization/claims) use a requirement, a requirement handler, and a pre-configured policy.</span></span> <span data-ttu-id="b3af8-105">这些构建基块支持在代码中的授权评估表达式。</span><span class="sxs-lookup"><span data-stu-id="b3af8-105">These building blocks support the expression of authorization evaluations in code.</span></span> <span data-ttu-id="b3af8-106">结果是一个更丰富、 可重复使用、 可测试授权结构。</span><span class="sxs-lookup"><span data-stu-id="b3af8-106">The result is a richer, reusable, testable authorization structure.</span></span>

<span data-ttu-id="b3af8-107">授权策略包含一个或多个要求。</span><span class="sxs-lookup"><span data-stu-id="b3af8-107">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="b3af8-108">在中注册的授权服务配置中，一部分`ConfigureServices`方法`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="b3af8-108">It's registered as part of the authorization service configuration, in the `ConfigureServices` method of the `Startup` class:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

<span data-ttu-id="b3af8-109">在前面的示例中，创建一个"AtLeast21"策略。</span><span class="sxs-lookup"><span data-stu-id="b3af8-109">In the preceding example, an "AtLeast21" policy is created.</span></span> <span data-ttu-id="b3af8-110">它具有一个要求，的最小存在时间，这作为参数提供到需求。</span><span class="sxs-lookup"><span data-stu-id="b3af8-110">It has a single requirement, that of a minimum age, which is supplied as a parameter to the requirement.</span></span>

<span data-ttu-id="b3af8-111">通过使用应用策略`[Authorize]`具有策略名称属性。</span><span class="sxs-lookup"><span data-stu-id="b3af8-111">Policies are applied by using the `[Authorize]` attribute with the policy name.</span></span> <span data-ttu-id="b3af8-112">例如:</span><span class="sxs-lookup"><span data-stu-id="b3af8-112">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a><span data-ttu-id="b3af8-113">惠?</span><span class="sxs-lookup"><span data-stu-id="b3af8-113">Requirements</span></span>

<span data-ttu-id="b3af8-114">授权要求是一个策略可用于评估当前的用户主体的数据参数的集合。</span><span class="sxs-lookup"><span data-stu-id="b3af8-114">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="b3af8-115">在我们的"AtLeast21"策略的要求是单个参数&mdash;最小存在时间。</span><span class="sxs-lookup"><span data-stu-id="b3af8-115">In our "AtLeast21" policy, the requirement is a single parameter&mdash;the minimum age.</span></span> <span data-ttu-id="b3af8-116">要求实现`IAuthorizationRequirement`，这是一个空标记接口。</span><span class="sxs-lookup"><span data-stu-id="b3af8-116">A requirement implements `IAuthorizationRequirement`, which is an empty marker interface.</span></span> <span data-ttu-id="b3af8-117">参数化的最小年龄要求无法实现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3af8-117">A parameterized minimum age requirement could be implemented as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> <span data-ttu-id="b3af8-118">一项要求不需要具有数据或属性。</span><span class="sxs-lookup"><span data-stu-id="b3af8-118">A requirement doesn't need to have data or properties.</span></span>

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a><span data-ttu-id="b3af8-119">授权处理程序</span><span class="sxs-lookup"><span data-stu-id="b3af8-119">Authorization handlers</span></span>

<span data-ttu-id="b3af8-120">授权处理程序负责的要求的属性求值。</span><span class="sxs-lookup"><span data-stu-id="b3af8-120">An authorization handler is responsible for the evaluation of a requirement's properties.</span></span> <span data-ttu-id="b3af8-121">授权处理程序会评估要求，针对提供`AuthorizationHandlerContext`以确定是否允许访问。</span><span class="sxs-lookup"><span data-stu-id="b3af8-121">The authorization handler evaluates the requirements against a provided `AuthorizationHandlerContext` to determine if access is allowed.</span></span> <span data-ttu-id="b3af8-122">可以有一项要求[多个处理程序](#security-authorization-policies-based-multiple-handlers)。</span><span class="sxs-lookup"><span data-stu-id="b3af8-122">A requirement can have [multiple handlers](#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="b3af8-123">处理程序继承`AuthorizationHandler<T>`，其中`T`是要处理的要求。</span><span class="sxs-lookup"><span data-stu-id="b3af8-123">Handlers inherit `AuthorizationHandler<T>`, where `T` is the requirement to be handled.</span></span>

<a name="security-authorization-handler-example"></a>

<span data-ttu-id="b3af8-124">最小存在时间处理程序可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3af8-124">The minimum age handler might look like this:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

<span data-ttu-id="b3af8-125">前面的代码确定当前的用户主体是否声明已知且受信任的颁发者已发出的出生日期。</span><span class="sxs-lookup"><span data-stu-id="b3af8-125">The preceding code determines if the current user principal has a date of birth claim which has been issued by a known and trusted Issuer.</span></span> <span data-ttu-id="b3af8-126">授权不能出现缺少声明时，在这种情况下返回的已完成的任务。</span><span class="sxs-lookup"><span data-stu-id="b3af8-126">Authorization can't occur when the claim is missing, in which case a completed task is returned.</span></span> <span data-ttu-id="b3af8-127">在不存在声明，计算用户的年龄。</span><span class="sxs-lookup"><span data-stu-id="b3af8-127">When a claim is present, the user's age is calculated.</span></span> <span data-ttu-id="b3af8-128">如果该用户满足定义的要求的最短期限，授权视为成功。</span><span class="sxs-lookup"><span data-stu-id="b3af8-128">If the user meets the minimum age defined by the requirement, authorization is deemed successful.</span></span> <span data-ttu-id="b3af8-129">授权成功后，`context.Succeed`调用与作为参数满足要求。</span><span class="sxs-lookup"><span data-stu-id="b3af8-129">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as a parameter.</span></span>

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a><span data-ttu-id="b3af8-130">处理程序注册</span><span class="sxs-lookup"><span data-stu-id="b3af8-130">Handler registration</span></span>

<span data-ttu-id="b3af8-131">在配置期间服务集合中注册处理程序。</span><span class="sxs-lookup"><span data-stu-id="b3af8-131">Handlers are registered in the services collection during configuration.</span></span> <span data-ttu-id="b3af8-132">例如:</span><span class="sxs-lookup"><span data-stu-id="b3af8-132">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

<span data-ttu-id="b3af8-133">每个处理程序添加到服务集合，通过调用`services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`。</span><span class="sxs-lookup"><span data-stu-id="b3af8-133">Each handler is added to the services collection by invoking `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="b3af8-134">处理程序应返回？</span><span class="sxs-lookup"><span data-stu-id="b3af8-134">What should a handler return?</span></span>

<span data-ttu-id="b3af8-135">请注意，`Handle`中的方法[处理程序示例](#security-authorization-handler-example)不返回值。</span><span class="sxs-lookup"><span data-stu-id="b3af8-135">Note that the `Handle` method in the [handler example](#security-authorization-handler-example) returns no value.</span></span> <span data-ttu-id="b3af8-136">是的成功或失败指示的状态如何？</span><span class="sxs-lookup"><span data-stu-id="b3af8-136">How is a status of either success or failure indicated?</span></span>

* <span data-ttu-id="b3af8-137">处理程序通过调用中表示成功`context.Succeed(IAuthorizationRequirement requirement)`，将要求传递成功验证。</span><span class="sxs-lookup"><span data-stu-id="b3af8-137">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="b3af8-138">处理程序不需要一般情况下，处理失败，因为其他处理程序相同的要求可能会成功。</span><span class="sxs-lookup"><span data-stu-id="b3af8-138">A handler doesn't need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="b3af8-139">若要确保失败，即使其他要求处理程序成功，调用`context.Fail`。</span><span class="sxs-lookup"><span data-stu-id="b3af8-139">To guarantee failure, even if other requirement handlers succeed, call `context.Fail`.</span></span>

<span data-ttu-id="b3af8-140">无论什么调用在您的处理程序内的策略要求要求时，将调用要求的所有处理程序。</span><span class="sxs-lookup"><span data-stu-id="b3af8-140">Regardless of what you call inside your handler, all handlers for a requirement will be called when a policy requires the requirement.</span></span> <span data-ttu-id="b3af8-141">这样要求产生副作用，如日志记录，始终会进行即使`context.Fail()`已在另一个处理程序调用。</span><span class="sxs-lookup"><span data-stu-id="b3af8-141">This allows requirements to have side effects, such as logging, which will always take place even if `context.Fail()` has been called in another handler.</span></span>

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="b3af8-142">为什么将需要一项要求的多个处理程序？</span><span class="sxs-lookup"><span data-stu-id="b3af8-142">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="b3af8-143">在要评估上的情况下**或**基础，实现单个要求的多个处理程序。</span><span class="sxs-lookup"><span data-stu-id="b3af8-143">In cases where you want evaluation to be on an **OR** basis, implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="b3af8-144">例如，Microsoft 已使用密钥卡仅打开的门。</span><span class="sxs-lookup"><span data-stu-id="b3af8-144">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="b3af8-145">如果你在家离开你密钥卡，接线员打印临时不干胶标签，并为你打开大门。</span><span class="sxs-lookup"><span data-stu-id="b3af8-145">If you leave your key card at home, the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="b3af8-146">在此方案中，您将需要单个， *BuildingEntry*，但多个处理程序，每个检查单个要求。</span><span class="sxs-lookup"><span data-stu-id="b3af8-146">In this scenario, you'd have a single requirement, *BuildingEntry*, but multiple handlers, each one examining a single requirement.</span></span>

<span data-ttu-id="b3af8-147">*BuildingEntryRequirement.cs*</span><span class="sxs-lookup"><span data-stu-id="b3af8-147">*BuildingEntryRequirement.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

<span data-ttu-id="b3af8-148">*BadgeEntryHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="b3af8-148">*BadgeEntryHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

<span data-ttu-id="b3af8-149">*TemporaryStickerHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="b3af8-149">*TemporaryStickerHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

<span data-ttu-id="b3af8-150">确保这两个处理程序[注册](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)。</span><span class="sxs-lookup"><span data-stu-id="b3af8-150">Ensure that both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration).</span></span> <span data-ttu-id="b3af8-151">如果任一处理程序成功时策略的计算结果`BuildingEntryRequirement`，策略评估成功。</span><span class="sxs-lookup"><span data-stu-id="b3af8-151">If either handler succeeds when a policy evaluates the `BuildingEntryRequirement`, the policy evaluation succeeds.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="b3af8-152">使用 func 来实现策略</span><span class="sxs-lookup"><span data-stu-id="b3af8-152">Using a func to fulfill a policy</span></span>

<span data-ttu-id="b3af8-153">可能有哪些履行策略是简单代码中表示的情况。</span><span class="sxs-lookup"><span data-stu-id="b3af8-153">There may be situations in which fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="b3af8-154">可以提供`Func<AuthorizationHandlerContext, bool>`配置与你的策略时`RequireAssertion`策略生成器。</span><span class="sxs-lookup"><span data-stu-id="b3af8-154">It's possible to supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="b3af8-155">例如，以前`BadgeEntryHandler`无法，如下所示重写：</span><span class="sxs-lookup"><span data-stu-id="b3af8-155">For example, the previous `BadgeEntryHandler` could be rewritten as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="b3af8-156">访问在处理程序的 MVC 请求上下文</span><span class="sxs-lookup"><span data-stu-id="b3af8-156">Accessing MVC request context in handlers</span></span>

<span data-ttu-id="b3af8-157">`HandleRequirementAsync`授权处理程序中实现的方法具有两个参数：`AuthorizationHandlerContext`和`TRequirement`正在处理。</span><span class="sxs-lookup"><span data-stu-id="b3af8-157">The `HandleRequirementAsync` method you implement in an authorization handler has two parameters: an `AuthorizationHandlerContext` and the `TRequirement` you are handling.</span></span> <span data-ttu-id="b3af8-158">框架，例如 MVC 或 Jabbr 可用于任何将对象添加到`Resource`属性`AuthorizationHandlerContext`传递额外信息。</span><span class="sxs-lookup"><span data-stu-id="b3af8-158">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationHandlerContext` to pass extra information.</span></span>

<span data-ttu-id="b3af8-159">例如，MVC 传递的实例的[AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)中`Resource`属性。</span><span class="sxs-lookup"><span data-stu-id="b3af8-159">For example, MVC passes an instance of [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) in the `Resource` property.</span></span> <span data-ttu-id="b3af8-160">此属性提供访问权限`HttpContext`， `RouteData`，以及其他和提供的 MVC Razor 页的所有内容。</span><span class="sxs-lookup"><span data-stu-id="b3af8-160">This property provides access to `HttpContext`, `RouteData`, and everything else provided by MVC and Razor Pages.</span></span>

<span data-ttu-id="b3af8-161">使用`Resource`属性是特定于框架。</span><span class="sxs-lookup"><span data-stu-id="b3af8-161">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="b3af8-162">使用中的信息`Resource`属性限制到特定的框架你授权策略。</span><span class="sxs-lookup"><span data-stu-id="b3af8-162">Using information in the `Resource` property limits your authorization policies to particular frameworks.</span></span> <span data-ttu-id="b3af8-163">应强制转换`Resource`属性使用`as`关键字，然后确认该强制转换具有成功以确保你的代码不崩溃与`InvalidCastException`其他框架上运行时：</span><span class="sxs-lookup"><span data-stu-id="b3af8-163">You should cast the `Resource` property using the `as` keyword, and then confirm the cast has succeed to ensure your code doesn't crash with an `InvalidCastException` when run on other frameworks:</span></span>

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
