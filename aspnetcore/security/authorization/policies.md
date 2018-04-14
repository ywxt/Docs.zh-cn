---
title: ASP.NET Core中基于策略的授权
author: rick-anderson
description: 了解如何创建和使用授权策略处理程序，用于实施 ASP.NET Core 应用程序中的授权要求。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 11/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/policies
ms.openlocfilehash: 411fee90bdccfb45c33f5d4ccd7864c83c614e70
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="policy-based-authorization-in-aspnet-core"></a>ASP.NET Core中基于策略的授权

实际上，[基于角色的授权](xref:security/authorization/roles)和[基于声明的授权](xref:security/authorization/claims)使用要求，要求处理程序，并预先配置的策略。 这些构建基块支持在代码中的授权运算表达式。 结果是一个更丰富、 可重复使用、 可测试授权结构。

授权策略包含一个或多个要求。 并注册在`Startup.ConfigureServices`方法中作为授权服务配置的一部分：[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

在前面的示例中，创建一个"AtLeast21"策略。 它具有单个要求&mdash;的最低年龄，它提供作为参数传递给要求。

通过使用`[Authorize]`属性和策略名称应用策略。 例如：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a>要求

授权要求是一个策略可用于运算当前的用户主体的数据参数的集合。 在我们的"AtLeast21"策略的要求是单个参数&mdash;最低年龄。 要求实现[IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement)，这是一个空标记接口。 参数化的最低年龄要求实现如下所示：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> 一项要求不需要具有数据或属性。

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a>授权处理程序

授权处理程序负责的要求的属性求值。 授权处理程序会运算要求，针对提供[AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext)以确定是否允许访问。

一项要求可以有[多个处理程序](#security-authorization-policies-based-multiple-handlers)。 处理程序可以继承[AuthorizationHandler\<TRequirement >](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1)，其中`TRequirement`是要处理的要求。 或者，一个处理程序可以实现[IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler)以处理多个类型的要求。

### <a name="use-a-handler-for-one-requirement"></a>为一个要求使用一个处理程序

<a name="security-authorization-handler-example"></a>

下面是单个最低年龄要求处理程序使用单个要求的一对一关系的一个示例：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

前面的代码确定当前的用户主体是否声明已知且受信任的颁发者已发出的出生日期。 授权不能出现缺少声明时，在这种情况下返回的已完成的任务。 当存在声明时，运算用户的年龄。 如果该用户满足定义要求的最低年龄，授权视为成功。 当授权成功后，`context.Succeed`调用作为与其唯一参数的满足要求。

### <a name="use-a-handler-for-multiple-requirements"></a>用于多个要求的处理程序

下面是单个权限处理程序使用三个要求一对多关系的一个示例：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/PermissionHandler.cs?name=snippet_PermissionHandlerClass)]

前面的代码遍历[PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;一个包含不标记为成功要求的属性。 如果用户具有读取权限，他或她必须是所有者或发起人访问请求资源。 如果用户有编辑或删除权限，他或她必须所有者权限才能访问请求的资源。 授权成功后，`context.Succeed`调用与作为其唯一的参数满足要求。

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a>处理程序注册

在配置的服务集合中注册处理程序。 例如：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

每个处理程序通过调用`services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`添加到服务集合。

## <a name="what-should-a-handler-return"></a>处理程序应返回什么？

请注意，`Handle`中的方法[处理程序示例](#security-authorization-handler-example)不返回值。 如何表明处理结果状态是成功还是失败？

* 处理程序通过调用中表明成功`context.Succeed(IAuthorizationRequirement requirement)`，通过已成功验证的要求。

* 处理程序通常不需要处理失败，因为其他处理程序相同的要求可能会成功。

* 若要确保失败，即使其他要求处理程序成功，调用`context.Fail`。

当设置为`false`、 [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure)属性 （位于 ASP.NET Core 1.1 和更高版本） 会在调用`context.Fail`时短路执行的处理程序。 `InvokeHandlersAfterFailure` 默认为`true`，在这种情况下调用所有处理程序。 这样可以使要求产生副作用，例如日志记录，它始终发生即使`context.Fail`已被另一个处理程序调用。

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a>为什么需要一项要求对应多个处理程序？

在要运算一个或可继承要求的情况下，实现单个要求对应多个处理程序。 例如，Microsoft 的门只能使用门禁卡打开。 如果你将门禁卡丢在家中，前台会打印一张临时不干胶标签，并为你打开大门。 在此方案中，您将需要一个要求， *BuildingEntry*，但多个处理程序，每个处理程序都检查一个单一要求。

*BuildingEntryRequirement.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

*BadgeEntryHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

*TemporaryStickerHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

确保这两个处理程序[注册](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)。 如果当一个策略运算`BuildingEntryRequirement`时有一个处理程序成功，策略运算成功。

## <a name="using-a-func-to-fulfill-a-policy"></a>使用 func 来实现策略

有些情况下，策略很容易用代码实现。 可以提供`Func<AuthorizationHandlerContext, bool>`配置你的策略和`RequireAssertion`策略生成器。

例如，上一个 `BadgeEntryHandler` 可以如下重写：

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a>访问处理程序中的 MVC 请求上下文

在授权处理程序中实现的 `HandleRequirementAsync` 方法有两个参数：`AuthorizationHandlerContext` 以及你正在处理的 `TRequirement`。 MVC 或 Jabbr 之类的框架可以自由地将任何对象添加到 `Resource` 中的 `AuthorizationHandlerContext` 属性，以便传递额外信息。

例如，MVC 在`Resource`属性中传递[AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)实例。 此属性提供对`HttpContext`的访问权限， `RouteData`，以及其他和提供的 MVC和Razor页的所有内容。

使用`Resource`属性是框架独有的。 使用`Resource`属性中信息限制特定框架上你的授权策略。 应使用`Resource`关键字强制转换`as`属性，然后确认该强制转换是否成功以确保你的代码不因为其他框架抛出`InvalidCastException`异常产生崩溃：

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
