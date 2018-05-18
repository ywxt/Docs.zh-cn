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
---
# <a name="custom-authorization-policy-providers-using-iauthorizationpolicyprovider-in-aspnet-core"></a>在 ASP.NET 核心中使用 IAuthorizationPolicyProvider 的自定义授权策略提供程序 

通过[Mike Rousos](https://github.com/mjrousos)

通常使用时[基于策略的授权](xref:security/authorization/policies)，通过调用注册策略`AuthorizationOptions.AddPolicy`授权服务配置的一部分。 在某些情况下，可能无法可能 （或最好） 以这种方式注册的所有授权策略。 在这些情况下，你可以使用自定义`IAuthorizationPolicyProvider`来控制提供授权策略的方式。

方案的示例在一个自定义[IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider)可能会很有用包括：

* 使用外部服务提供的策略评估。
* （用于不同的房间号或年龄，例如） 使用大量的策略，因此它没有意义将与每个单个授权策略添加`AuthorizationOptions.AddPolicy`调用。
* 在运行时基于外部数据源 （如数据库） 中的信息创建策略或通过另一种机制动态确定授权要求。

## <a name="customizing-policy-retrieval"></a>自定义策略检索

ASP.NET Core 应用使用的实现`IAuthorizationPolicyProvider`接口以检索授权策略。 默认情况下， [DefaultAuthorizationPolicyProvider](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider)已注册并使用。 `DefaultAuthorizationPolicyProvider` 返回从策略`AuthorizationOptions`中提供`IServiceCollection.AddAuthorization`调用。

你可以注册其他自定义此行为`IAuthorizationPolicyProvider`中应用程序的实现[依赖关系注入](xref:fundamentals/dependency-injection)容器。 

`IAuthorizationPolicyProvider`接口包含两个 Api:

* [GetPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_)返回具有给定名称的授权策略。
* [GetDefaultPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync?view=aspnetcore-2.0)返回默认授权策略 (用于策略`[Authorize]`而无需指定策略的属性)。 

通过实现这些两个 Api，你可以自定义提供授权策略的方式。

## <a name="parameterized-authorize-attribute-example"></a>参数化授权特性的示例

一种情况其中`IAuthorizationPolicyProvider`可启用自定义`[Authorize]`其要求取决于参数的属性。 例如，在[基于策略的授权](xref:security/authorization/policies)文档，基于年龄的 ("AtLeast21") 策略已用作示例。 如果在应用程序的不同控制器操作应可供用户的*不同*年龄，它可能会很有用具有许多不同的基于年龄的策略。 而不是注册所有不同年龄基于策略的应用程序将需要在`AuthorizationOptions`，你可以生成动态与自定义策略`IAuthorizationPolicyProvider`。 若要使使用策略更轻松，可批注由于使用自定义授权属性，如操作`[MinimumAgeAuthorize(20)]`。

## <a name="custom-authorization-attributes"></a>自定义授权属性

授权策略由其名称标识。 自定义`MinimumAgeAuthorizeAttribute`所述之前需要将参数映射到可以用于检索相应的授权策略的字符串。 你可以执行此操作通过从派生`AuthorizeAttribute`并使`Age`属性包装`AuthorizeAttribute.Policy`属性。

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

此特性类型具有`Policy`字符串基于硬编码前缀 (`"MinimumAge"`) 字符，在通过构造函数传递一个整数。

你可以将其应用于中方式不同于其他的操作`Authorize`属性，但前者将作为参数的整数。

```CSharp
[MinimumAgeAuthorize(10)]
public IActionResult RequiresMinimumAge10()
```

## <a name="custom-iauthorizationpolicyprovider"></a>自定义 IAuthorizationPolicyProvider

自定义`MinimumAgeAuthorizeAttribute`可以方便地对请求授权策略的任何所需的最小存在时间。 要解决的下一步问题时，必须确保为所有这些不同的年龄段可以找到授权策略。 这就是`IAuthorizationPolicyProvider`很有用。

使用时`MinimumAgeAuthorizationAttribute`，授权策略名称将遵循的模式`"MinimumAge" + Age`，因此自定义`IAuthorizationPolicyProvider`应生成授权策略：

* 分析将年龄字段从策略名称。
* 使用`AuthorizationPolicyBuiler`创建新 `AuthorizationPolicy`
* 将要求添加到策略根据保留时间与`AuthorizationPolicyBuilder.AddRequirements`。 在其他情况下，你可以使用`RequireClaim`， `RequireRole`，或`RequireUserName`相反。

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

## <a name="multiple-authorization-policy-providers"></a>多个授权策略提供程序

使用自定义时`IAuthorizationPolicyProvider`实现中，请记住，ASP.NET Core 仅使用的一个实例`IAuthorizationPolicyProvider`。 如果自定义提供程序无法提供的所有策略名称的授权策略，它应回退到备份提供程序。 策略名称可能包括那些来自的默认策略`[Authorize]`没有名称的属性。

例如，考虑应用程序需要自定义保留时间策略和更传统的基于角色的策略检索。 此类应用程序可以使用自定义授权策略提供程序的：

* 试图分析策略名称。 
* 调入不同的策略提供程序 (如`DefaultAuthorizationPolicyProvider`) 如果策略名称不包含 age。

## <a name="default-policy"></a>默认策略

除了提供命名的授权策略，自定义`IAuthorizationPolicyProvider`需要实现`GetDefaultPolicyAsync`提供的授权策略`[Authorize]`没有指定策略名称的属性。

在许多情况下，此授权属性仅需要经过身份验证的用户，因此你可以通过调用必要的策略`RequireAuthenticatedUser`:

```CSharp
public Task<AuthorizationPolicy> GetDefaultPolicyAsync() => 
    Task.FromResult(new AuthorizationPolicyBuilder().RequireAuthenticatedUser().Build());
```

自定义的所有方面与`IAuthorizationPolicyProvider`，你可以自定义此操作，请根据需要。 在某些情况下：

* 可能不使用默认的授权策略。
* 检索默认策略可以委派给回退`IAuthorizationPolicyProvider`。

## <a name="using-a-custom-iauthorizationpolicyprovider"></a>使用自定义 IAuthorizationPolicyProvider

若要使用自定义策略从`IAuthorizationPolicyProvider`，你必须：

* 注册相应`AuthorizationHandler`具有依赖关系注入类型 (中所述[基于策略的授权](xref:security/authorization/policies#authorization-handlers))，如同处理所有基于策略的授权方案。
* 注册自定义`IAuthorizationPolicyProvider`应用程序的依赖关系注入服务集合中的类型 (在`Startup.ConfigureServices`) 以替换默认策略提供程序。

```CSharp
services.AddTransient<IAuthorizationPolicyProvider, MinimumAgePolicyProvider>();
```

完成自定义`IAuthorizationPolicyProvider`示例位于[aspnet/AuthSamples GitHub 存储库](https://github.com/aspnet/AuthSamples/tree/dev/samples/CustomPolicyProvider)。
