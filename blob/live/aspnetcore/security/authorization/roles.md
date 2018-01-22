---
title: "基于角色的授权"
author: rick-anderson
description: "本文档演示如何通过将角色传递给 Authorize 属性限制 ASP.NET Core 控制器和操作访问。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/roles
ms.openlocfilehash: 18964464fea76c91d716202d89ee3a3eb36c3078
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="role-based-authorization"></a><span data-ttu-id="37a95-103">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="37a95-103">Role based Authorization</span></span>

<a name="security-authorization-role-based"></a>

<span data-ttu-id="37a95-104">当创建标识它可能属于一个或多个角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-104">When an identity is created it may belong to one or more roles.</span></span> <span data-ttu-id="37a95-105">例如，Tracy 可能属于管理员和用户角色，同时 Scott 可能仅属于用户角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-105">For example, Tracy may belong to the Administrator and User roles whilst Scott may only belong to the User role.</span></span> <span data-ttu-id="37a95-106">如何创建和管理这些角色取决于授权过程的后备存储。</span><span class="sxs-lookup"><span data-stu-id="37a95-106">How these roles are created and managed depends on the backing store of the authorization process.</span></span> <span data-ttu-id="37a95-107">角色公开给开发人员通过[IsInRole](https://docs.microsoft.com/dotnet/api/system.security.principal.genericprincipal.isinrole)方法[ClaimsPrincipal](https://docs.microsoft.com/dotnet/api/system.security.claims.claimsprincipal)类。</span><span class="sxs-lookup"><span data-stu-id="37a95-107">Roles are exposed to the developer through the [IsInRole](https://docs.microsoft.com/dotnet/api/system.security.principal.genericprincipal.isinrole) method on the [ClaimsPrincipal](https://docs.microsoft.com/dotnet/api/system.security.claims.claimsprincipal) class.</span></span>

## <a name="adding-role-checks"></a><span data-ttu-id="37a95-108">添加角色检查</span><span class="sxs-lookup"><span data-stu-id="37a95-108">Adding role checks</span></span>

<span data-ttu-id="37a95-109">基于角色的授权检查均为声明性&mdash;开发人员将它们嵌入在其代码中，针对控制器或者控制器中的某个操作指定当前用户必须是的成员来访问请求的资源的角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-109">Role-based authorization checks are declarative&mdash;the developer embeds them within their code, against a controller or an action within a controller, specifying roles which the current user must be a member of to access the requested resource.</span></span>

<span data-ttu-id="37a95-110">例如，下面的代码可访问任何操作限制上`AdministrationController`谁是其成员的用户到`Administrator`角色：</span><span class="sxs-lookup"><span data-stu-id="37a95-110">For example, the following code limits access to any actions on the `AdministrationController` to users who are a member of the `Administrator` role:</span></span>

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

<span data-ttu-id="37a95-111">以逗号分隔的列表，可以指定多个角色：</span><span class="sxs-lookup"><span data-stu-id="37a95-111">You can specify multiple roles as a comma separated list:</span></span>

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

<span data-ttu-id="37a95-112">此控制器将作为仅可访问的成员的用户的`HRManager`角色或`Finance`角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-112">This controller would be only accessible by users who are members of the `HRManager` role or the `Finance` role.</span></span>

<span data-ttu-id="37a95-113">如果您将应用多个属性，则访问用户必须是指定; 的所有角色的成员下面的示例要求用户必须是的成员`PowerUser`和`ControlPanelUser`角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-113">If you apply multiple attributes then an accessing user must be a member of all the roles specified; the following sample requires that a user must be a member of both the `PowerUser` and `ControlPanelUser` role.</span></span>

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

<span data-ttu-id="37a95-114">通过应用在操作级别的其他角色授权属性，可以进一步限制访问：</span><span class="sxs-lookup"><span data-stu-id="37a95-114">You can further limit access by applying additional role authorization attributes at the action level:</span></span>

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

<span data-ttu-id="37a95-115">中的上一个代码段成员`Administrator`角色或`PowerUser`角色可以访问控制器和`SetTime`操作，但只有的成员`Administrator`角色可以访问`ShutDown`操作。</span><span class="sxs-lookup"><span data-stu-id="37a95-115">In the previous code snippet members of the `Administrator` role or the `PowerUser` role can access the controller and the `SetTime` action, but only members of the `Administrator` role can access the `ShutDown` action.</span></span>

<span data-ttu-id="37a95-116">您可以锁定控制器，但允许匿名、 未经身份验证访问各项操作。</span><span class="sxs-lookup"><span data-stu-id="37a95-116">You can also lock down a controller but allow anonymous, unauthenticated access to individual actions.</span></span>

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a><span data-ttu-id="37a95-117">基于策略角色检查</span><span class="sxs-lookup"><span data-stu-id="37a95-117">Policy based role checks</span></span>

<span data-ttu-id="37a95-118">此外可以使用新的策略语法中，开发人员将在启动策略注册为授权服务配置的一部分的其中表示角色的要求。</span><span class="sxs-lookup"><span data-stu-id="37a95-118">Role requirements can also be expressed using the new Policy syntax, where a developer registers a policy at startup as part of the Authorization service configuration.</span></span> <span data-ttu-id="37a95-119">这通常发生在`ConfigureServices()`中你*Startup.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="37a95-119">This normally occurs in `ConfigureServices()` in your *Startup.cs* file.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole", policy => policy.RequireRole("Administrator"));
    });
}
```

<span data-ttu-id="37a95-120">策略使用应用`Policy`属性`AuthorizeAttribute`属性：</span><span class="sxs-lookup"><span data-stu-id="37a95-120">Policies are applied using the `Policy` property on the `AuthorizeAttribute` attribute:</span></span>

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

<span data-ttu-id="37a95-121">如果你想要指定多个允许的角色中一项要求，则可作为参数来指定这些`RequireRole`方法：</span><span class="sxs-lookup"><span data-stu-id="37a95-121">If you want to specify multiple allowed roles in a requirement then you can specify them as parameters to the `RequireRole` method:</span></span>

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

<span data-ttu-id="37a95-122">此示例授权属于用户`Administrator`，`PowerUser`或`BackupAdministrator`角色。</span><span class="sxs-lookup"><span data-stu-id="37a95-122">This example authorizes users who belong to the `Administrator`, `PowerUser` or `BackupAdministrator` roles.</span></span>
