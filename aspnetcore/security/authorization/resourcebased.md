---
title: ASP.NET Core 中基于资源的授权
author: scottaddie
description: 了解如何在 ASP.NET Core 应用程序中实现的基于资源的授权，Authorize 属性不会满足要求。
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
uid: security/authorization/resourcebased
ms.openlocfilehash: 2cb3844a38f7482c27fb471343109d51a516ea20
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206691"
---
# <a name="resource-based-authorization-in-aspnet-core"></a>ASP.NET Core 中基于资源的授权

授权策略取决于要访问的资源。 请考虑具有作者属性的文档。 允许仅作者更新文档。 因此，文档必须检索从数据存储区进行授权评估之前。

数据绑定之前和之后，页面处理程序或将文档加载操作的执行进行属性评估。 出于这些原因，使用声明性授权`[Authorize]`属性不能。 相反，可以调用自定义授权方法&mdash;称为命令性授权的样式。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples)（[如何下载](xref:index#how-to-download-a-sample)）。

[使用受授权的用户数据创建 ASP.NET Core 应用](xref:security/authorization/secure-data)包含的示例应用程序使用的基于资源的授权。

## <a name="use-imperative-authorization"></a>使用命令性授权

授权作为实现[IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice)服务并注册内的服务集合中`Startup`类。 该服务可通过[依赖关系注入](xref:fundamentals/dependency-injection)页面处理程序或进行操作。

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

`IAuthorizationService` 具有两个`AuthorizeAsync`方法重载： 一个接受资源和策略名称和其他接受资源和要求来评估的列表。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

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

在以下示例中，要保护的资源加载到自定义`Document`对象。 `AuthorizeAsync`重载进行调用以确定当前用户是否允许编辑提供的文档。 自定义"EditPolicy"授权策略可分解为决策。 请参阅[自定义基于策略的授权](xref:security/authorization/policies)创建授权策略的详细信息。

> [!NOTE]
> 下面的代码示例假定已经运行了身份验证和组`User`属性。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a>编写基于资源的处理程序

编写处理程序的基于资源的授权没有太大区别比[编写普通要求处理程序](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler)。 创建自定义要求类，并实现要求处理程序类。 处理程序类指定的要求和资源类型。 例如，处理程序利用`SameAuthorRequirement`要求和`Document`资源如下所示：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

注册的要求和处理程序中的`Startup.ConfigureServices`方法：

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a>操作要求

若要进行决策基于 CRUD （创建、 读取、 更新、 删除） 操作的结果，请使用[OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement)帮助器类。 此类，可为每个操作类型编写单个处理程序而不是单独的类。 若要使用它，提供一些操作名称：

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

处理程序的实现，如下所示，使用`OperationAuthorizationRequirement`要求和`Document`资源：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

前面的处理程序验证该操作使用的资源、 用户的标识和需求的`Name`属性。

若要调用的操作的资源处理程序，指定该操作时调用`AuthorizeAsync`页面处理程序或操作中。 下面的示例确定是否允许经过身份验证的用户若要查看提供的文档。

> [!NOTE]
> 下面的代码示例假定已经运行了身份验证和组`User`属性。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

如果授权成功，则返回查看文档的页。 如果授权失败而用户进行身份验证，返回`ForbidResult`通知授权失败的任何身份验证中间件。 一个`ChallengeResult`时必须执行身份验证，将返回。 对于交互式浏览器客户端，可能需要将用户重定向到登录页。

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

如果授权成功，则返回文档的视图。 如果授权失败，返回`ChallengeResult`授权失败，并将中间件可以采取适当的响应将通知任何身份验证中间件。 相应的响应可能返回 401 或 403 状态代码。 对于交互式浏览器客户端，这可能意味着将用户重定向到登录页。

---
