---
title: ASP.NET 核心中的自定义授权策略提供程序
author: mjrousos
description: 了解如何在 ASP.NET Core 应用程序中使用自定义 IAuthorizationPolicyProvider 动态生成的授权策略。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/02/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/iauthorizationpolicyprovider
ms.openlocfilehash: a5bad88b37d38b819b960b1eb27808d891268c01
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34233438"
---
# <a name="custom-authorization-policy-providers-using-iauthorizationpolicyprovider-in-aspnet-core"></a><span data-ttu-id="8ceb7-103">在 ASP.NET 核心中使用 IAuthorizationPolicyProvider 的自定义授权策略提供程序</span><span class="sxs-lookup"><span data-stu-id="8ceb7-103">Custom Authorization Policy Providers using IAuthorizationPolicyProvider in ASP.NET Core</span></span> 

<span data-ttu-id="8ceb7-104">通过[Mike Rousos](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="8ceb7-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="8ceb7-105">通常使用时[基于策略的授权](xref:security/authorization/policies)，通过调用注册策略`AuthorizationOptions.AddPolicy`授权服务配置的一部分。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-105">Typically when using [policy-based authorization](xref:security/authorization/policies), policies are registered by calling `AuthorizationOptions.AddPolicy` as part of authorization service configuration.</span></span> <span data-ttu-id="8ceb7-106">在某些情况下，可能无法可能 （或最好） 以这种方式注册的所有授权策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-106">In some scenarios, it may not be possible (or desirable) to register all authorization policies in this way.</span></span> <span data-ttu-id="8ceb7-107">在这些情况下，你可以使用自定义`IAuthorizationPolicyProvider`来控制提供授权策略的方式。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-107">In those cases, you can use a custom `IAuthorizationPolicyProvider` to control how authorization policies are supplied.</span></span>

<span data-ttu-id="8ceb7-108">方案的示例在一个自定义[IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider)可能会很有用包括：</span><span class="sxs-lookup"><span data-stu-id="8ceb7-108">Examples of scenarios where a custom [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) may be useful include:</span></span>

* <span data-ttu-id="8ceb7-109">使用外部服务提供的策略评估。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-109">Using an external service to provide policy evaluation.</span></span>
* <span data-ttu-id="8ceb7-110">（用于不同的房间号或年龄，例如） 使用大量的策略，因此它没有意义将与每个单个授权策略添加`AuthorizationOptions.AddPolicy`调用。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-110">Using a large range of policies (for different room numbers or ages, for example), so it doesn’t make sense to add each individual authorization policy with an `AuthorizationOptions.AddPolicy` call.</span></span>
* <span data-ttu-id="8ceb7-111">在运行时基于外部数据源 （如数据库） 中的信息创建策略或通过另一种机制动态确定授权要求。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-111">Creating policies at runtime based on information in an external data source (like a database) or determining authorization requirements dynamically through another mechanism.</span></span>

## <a name="customizing-policy-retrieval"></a><span data-ttu-id="8ceb7-112">自定义策略检索</span><span class="sxs-lookup"><span data-stu-id="8ceb7-112">Customizing policy retrieval</span></span>

<span data-ttu-id="8ceb7-113">ASP.NET Core 应用使用的实现`IAuthorizationPolicyProvider`接口以检索授权策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-113">ASP.NET Core apps use an implementation of the `IAuthorizationPolicyProvider` interface to retrieve authorization policies.</span></span> <span data-ttu-id="8ceb7-114">默认情况下， [DefaultAuthorizationPolicyProvider](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider)已注册并使用。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-114">By default, [DefaultAuthorizationPolicyProvider](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) is registered and used.</span></span> <span data-ttu-id="8ceb7-115">`DefaultAuthorizationPolicyProvider` 返回从策略`AuthorizationOptions`中提供`IServiceCollection.AddAuthorization`调用。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-115">`DefaultAuthorizationPolicyProvider` returns policies from the `AuthorizationOptions` provided in an `IServiceCollection.AddAuthorization` call.</span></span>

<span data-ttu-id="8ceb7-116">你可以注册其他自定义此行为`IAuthorizationPolicyProvider`中应用程序的实现[依赖关系注入](xref:fundamentals/dependency-injection)容器。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-116">You can customize this behavior by registering a different `IAuthorizationPolicyProvider` implementation in the app’s [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> 

<span data-ttu-id="8ceb7-117">`IAuthorizationPolicyProvider`接口包含两个 Api:</span><span class="sxs-lookup"><span data-stu-id="8ceb7-117">The `IAuthorizationPolicyProvider` interface contains two APIs:</span></span>

* <span data-ttu-id="8ceb7-118">[GetPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_)返回具有给定名称的授权策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-118">[GetPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) returns an authorization policy for a given name.</span></span>
* <span data-ttu-id="8ceb7-119">[GetDefaultPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync?view=aspnetcore-2.0)返回默认授权策略 (用于策略`[Authorize]`而无需指定策略的属性)。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-119">[GetDefaultPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync?view=aspnetcore-2.0) returns the default authorization policy (the policy used for `[Authorize]` attributes without a policy specified).</span></span> 

<span data-ttu-id="8ceb7-120">通过实现这些两个 Api，你可以自定义提供授权策略的方式。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-120">By implementing these two APIs, you can customize how authorization policies are provided.</span></span>

## <a name="parameterized-authorize-attribute-example"></a><span data-ttu-id="8ceb7-121">参数化授权特性的示例</span><span class="sxs-lookup"><span data-stu-id="8ceb7-121">Parameterized authorize attribute example</span></span>

<span data-ttu-id="8ceb7-122">一种情况其中`IAuthorizationPolicyProvider`可启用自定义`[Authorize]`其要求取决于参数的属性。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-122">One scenario where `IAuthorizationPolicyProvider` is useful is enabling custom `[Authorize]` attributes whose requirements depend on a parameter.</span></span> <span data-ttu-id="8ceb7-123">例如，在[基于策略的授权](xref:security/authorization/policies)文档，基于年龄的 ("AtLeast21") 策略已用作示例。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-123">For example, in [policy-based authorization](xref:security/authorization/policies) documentation, an age-based (“AtLeast21”) policy was used as a sample.</span></span> <span data-ttu-id="8ceb7-124">如果在应用程序的不同控制器操作应可供用户的*不同*年龄，它可能会很有用具有许多不同的基于年龄的策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-124">If different controller actions in an app should be made available to users of *different* ages, it might be useful to have many different age-based policies.</span></span> <span data-ttu-id="8ceb7-125">而不是注册所有不同年龄基于策略的应用程序将需要在`AuthorizationOptions`，你可以生成动态与自定义策略`IAuthorizationPolicyProvider`。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-125">Instead of registering all the different age-based policies that the application will need in `AuthorizationOptions`, you can generate the policies dynamically with a custom `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="8ceb7-126">若要使使用策略更轻松，可批注由于使用自定义授权属性，如操作`[MinimumAgeAuthorize(20)]`。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-126">To make using the policies easier, you can annotate actions with custom authorization attribute like `[MinimumAgeAuthorize(20)]`.</span></span>

## <a name="custom-authorization-attributes"></a><span data-ttu-id="8ceb7-127">自定义授权属性</span><span class="sxs-lookup"><span data-stu-id="8ceb7-127">Custom Authorization Attributes</span></span>

<span data-ttu-id="8ceb7-128">授权策略由其名称标识。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-128">Authorization policies are identified by their names.</span></span> <span data-ttu-id="8ceb7-129">自定义`MinimumAgeAuthorizeAttribute`所述之前需要将参数映射到可以用于检索相应的授权策略的字符串。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-129">The custom `MinimumAgeAuthorizeAttribute` described previously needs to map arguments into a string that can be used to retrieve the corresponding authorization policy.</span></span> <span data-ttu-id="8ceb7-130">你可以执行此操作通过从派生`AuthorizeAttribute`并使`Age`属性包装`AuthorizeAttribute.Policy`属性。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-130">You can do this by deriving from `AuthorizeAttribute` and making the `Age` property wrap the `AuthorizeAttribute.Policy` property.</span></span>

```CSharp
internal class MinimumAgeAuthorizeAttribute : AuthorizeAttribute
{
    const string POLICY_PREFIX = "MinimumAge";

    public MinimumAgeAuthorizeAttribute(int age) => Age = age;

    // Get or set the Age property by manipulating the underlying Policy property
    public int Age
    {
        get
        {
            if (int.TryParse(Policy.Substring(POLICY_PREFIX.Length), out var age))
            {
                return age;
            }
            return default(int);
        }
        set
        {
            Policy = $"{POLICY_PREFIX}{value.ToString()}";
        }
    }
}
```

<span data-ttu-id="8ceb7-131">此特性类型具有`Policy`字符串基于硬编码前缀 (`"MinimumAge"`) 字符，在通过构造函数传递一个整数。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-131">This attribute type has a `Policy` string based on the hard-coded prefix (`"MinimumAge"`) and an integer passed in via the constructor.</span></span>

<span data-ttu-id="8ceb7-132">你可以将其应用于中方式不同于其他的操作`Authorize`属性，但前者将作为参数的整数。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-132">You can apply it to actions in the same way as other `Authorize` attributes except that it takes an integer as a parameter.</span></span>

```CSharp
[MinimumAgeAuthorize(10)]
public IActionResult RequiresMinimumAge10()
```

## <a name="custom-iauthorizationpolicyprovider"></a><span data-ttu-id="8ceb7-133">自定义 IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="8ceb7-133">Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="8ceb7-134">自定义`MinimumAgeAuthorizeAttribute`可以方便地对请求授权策略的任何所需的最小存在时间。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-134">The custom `MinimumAgeAuthorizeAttribute` makes it easy to request authorization policies for any minimum age desired.</span></span> <span data-ttu-id="8ceb7-135">要解决的下一步问题时，必须确保为所有这些不同的年龄段可以找到授权策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-135">The next problem to solve is making sure that authorization policies are available for all of those different ages.</span></span> <span data-ttu-id="8ceb7-136">这就是`IAuthorizationPolicyProvider`很有用。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-136">This is where an `IAuthorizationPolicyProvider` is useful.</span></span>

<span data-ttu-id="8ceb7-137">使用时`MinimumAgeAuthorizationAttribute`，授权策略名称将遵循的模式`"MinimumAge" + Age`，因此自定义`IAuthorizationPolicyProvider`应生成授权策略：</span><span class="sxs-lookup"><span data-stu-id="8ceb7-137">When using `MinimumAgeAuthorizationAttribute`, the authorization policy names will follow the pattern `"MinimumAge" + Age`, so the custom `IAuthorizationPolicyProvider` should generate authorization policies by:</span></span>

* <span data-ttu-id="8ceb7-138">分析将年龄字段从策略名称。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-138">Parsing the age from the policy name.</span></span>
* <span data-ttu-id="8ceb7-139">使用`AuthorizationPolicyBuiler`创建新 `AuthorizationPolicy`</span><span class="sxs-lookup"><span data-stu-id="8ceb7-139">Using `AuthorizationPolicyBuiler` to create a new `AuthorizationPolicy`</span></span>
* <span data-ttu-id="8ceb7-140">将要求添加到策略根据保留时间与`AuthorizationPolicyBuilder.AddRequirements`。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-140">Adding requirements to the policy based on the age with `AuthorizationPolicyBuilder.AddRequirements`.</span></span> <span data-ttu-id="8ceb7-141">在其他情况下，你可以使用`RequireClaim`， `RequireRole`，或`RequireUserName`相反。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-141">In other scenarios, you might use `RequireClaim`, `RequireRole`, or `RequireUserName` instead.</span></span>

```CSharp
internal class MinimumAgePolicyProvider : IAuthorizationPolicyProvider
{
    const string POLICY_PREFIX = "MinimumAge";

    // Policies are looked up by string name, so expect 'parameters' (like age)
    // to be embedded in the policy names. This is abstracted away from developers
    // by the more strongly-typed attributes derived from AuthorizeAttribute
    // (like [MinimumAgeAuthorize()] in this sample)
    public Task<AuthorizationPolicy> GetPolicyAsync(string policyName)
    {
        if (policyName.StartsWith(POLICY_PREFIX, StringComparison.OrdinalIgnoreCase) &&
            int.TryParse(policyName.Substring(POLICY_PREFIX.Length), out var age))
        {
            var policy = new AuthorizationPolicyBuilder();
            policy.AddRequirements(new MinimumAgeRequirement(age));
            return Task.FromResult(policy.Build());
        }

        return Task.FromResult<AuthorizationPolicy>(null);
    }
}
```

## <a name="multiple-authorization-policy-providers"></a><span data-ttu-id="8ceb7-142">多个授权策略提供程序</span><span class="sxs-lookup"><span data-stu-id="8ceb7-142">Multiple authorization policy providers</span></span>

<span data-ttu-id="8ceb7-143">使用自定义时`IAuthorizationPolicyProvider`实现中，请记住，ASP.NET Core 仅使用的一个实例`IAuthorizationPolicyProvider`。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-143">When using custom `IAuthorizationPolicyProvider` implementations, keep in mind that ASP.NET Core only uses one instance of `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="8ceb7-144">如果自定义提供程序无法提供的所有策略名称的授权策略，它应回退到备份提供程序。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-144">If a custom provider isn't able to provide authorization policies for all policy names, it should fall back to a backup provider.</span></span> <span data-ttu-id="8ceb7-145">策略名称可能包括那些来自的默认策略`[Authorize]`没有名称的属性。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-145">Policy names might include those that come from a default policy for `[Authorize]` attributes without a name.</span></span>

<span data-ttu-id="8ceb7-146">例如，考虑应用程序需要自定义保留时间策略和更传统的基于角色的策略检索。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-146">For example, consider an application needed both custom age policies and more traditional role-based policy retrieval.</span></span> <span data-ttu-id="8ceb7-147">此类应用程序可以使用自定义授权策略提供程序的：</span><span class="sxs-lookup"><span data-stu-id="8ceb7-147">Such an app could use a custom authorization policy provider that:</span></span>

* <span data-ttu-id="8ceb7-148">试图分析策略名称。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-148">Attempts to parse policy names.</span></span> 
* <span data-ttu-id="8ceb7-149">调入不同的策略提供程序 (如`DefaultAuthorizationPolicyProvider`) 如果策略名称不包含 age。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-149">Calls into a different policy provider (like `DefaultAuthorizationPolicyProvider`) if the policy name doesn't contain an age.</span></span>

## <a name="default-policy"></a><span data-ttu-id="8ceb7-150">默认策略</span><span class="sxs-lookup"><span data-stu-id="8ceb7-150">Default policy</span></span>

<span data-ttu-id="8ceb7-151">除了提供命名的授权策略，自定义`IAuthorizationPolicyProvider`需要实现`GetDefaultPolicyAsync`提供的授权策略`[Authorize]`没有指定策略名称的属性。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-151">In addition to providing named authorization policies, a custom `IAuthorizationPolicyProvider` needs to implement `GetDefaultPolicyAsync` to provide an authorization policy for `[Authorize]` attributes without a policy name specified.</span></span>

<span data-ttu-id="8ceb7-152">在许多情况下，此授权属性仅需要经过身份验证的用户，因此你可以通过调用必要的策略`RequireAuthenticatedUser`:</span><span class="sxs-lookup"><span data-stu-id="8ceb7-152">In many cases, this authorization attribute only requires an authenticated user, so you can make the necessary policy with a call to `RequireAuthenticatedUser`:</span></span>

```CSharp
public Task<AuthorizationPolicy> GetDefaultPolicyAsync() => 
    Task.FromResult(new AuthorizationPolicyBuilder().RequireAuthenticatedUser().Build());
```

<span data-ttu-id="8ceb7-153">自定义的所有方面与`IAuthorizationPolicyProvider`，你可以自定义此操作，请根据需要。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-153">As with all aspects of a custom `IAuthorizationPolicyProvider`, you can customize this, as needed.</span></span> <span data-ttu-id="8ceb7-154">在某些情况下：</span><span class="sxs-lookup"><span data-stu-id="8ceb7-154">In some cases:</span></span>

* <span data-ttu-id="8ceb7-155">可能不使用默认的授权策略。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-155">Default authorization policies might not be used.</span></span>
* <span data-ttu-id="8ceb7-156">检索默认策略可以委派给回退`IAuthorizationPolicyProvider`。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-156">Retrieving the default policy can be delegated to a fallback `IAuthorizationPolicyProvider`.</span></span>

## <a name="using-a-custom-iauthorizationpolicyprovider"></a><span data-ttu-id="8ceb7-157">使用自定义 IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="8ceb7-157">Using a Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="8ceb7-158">若要使用自定义策略从`IAuthorizationPolicyProvider`，你必须：</span><span class="sxs-lookup"><span data-stu-id="8ceb7-158">To use custom policies from an `IAuthorizationPolicyProvider`, you must:</span></span>

* <span data-ttu-id="8ceb7-159">注册相应`AuthorizationHandler`具有依赖关系注入类型 (中所述[基于策略的授权](xref:security/authorization/policies#authorization-handlers))，如同处理所有基于策略的授权方案。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-159">Register the appropriate `AuthorizationHandler` types with dependency injection (described in [policy-based authorization](xref:security/authorization/policies#authorization-handlers)), as with all policy-based authorization scenarios.</span></span>
* <span data-ttu-id="8ceb7-160">注册自定义`IAuthorizationPolicyProvider`应用程序的依赖关系注入服务集合中的类型 (在`Startup.ConfigureServices`) 以替换默认策略提供程序。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-160">Register the custom `IAuthorizationPolicyProvider` type in the app's dependency injection service collection (in `Startup.ConfigureServices`) to replace the default policy provider.</span></span>

```CSharp
services.AddTransient<IAuthorizationPolicyProvider, MinimumAgePolicyProvider>();
```

<span data-ttu-id="8ceb7-161">完成自定义`IAuthorizationPolicyProvider`示例位于[aspnet/AuthSamples GitHub 存储库](https://github.com/aspnet/AuthSamples/tree/dev/samples/CustomPolicyProvider)。</span><span class="sxs-lookup"><span data-stu-id="8ceb7-161">A complete custom `IAuthorizationPolicyProvider` sample is available in the [aspnet/AuthSamples GitHub repository](https://github.com/aspnet/AuthSamples/tree/dev/samples/CustomPolicyProvider).</span></span>
