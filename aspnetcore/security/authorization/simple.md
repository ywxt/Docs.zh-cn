---
title: 在 ASP.NET Core 中的简单授权
author: rick-anderson
description: 了解如何使用 Authorize 属性限制对 ASP.NET Core 控制器和操作的访问。
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/simple
ms.openlocfilehash: 6409def0508b855d3d2a4a1f4d3a3d15bfe5dd32
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961118"
---
# <a name="simple-authorization-in-aspnet-core"></a><span data-ttu-id="88360-103">在 ASP.NET Core 中的简单授权</span><span class="sxs-lookup"><span data-stu-id="88360-103">Simple authorization in ASP.NET Core</span></span>

<a name="security-authorization-simple"></a>

<span data-ttu-id="88360-104">通过控制在 MVC 中的授权`AuthorizeAttribute`属性和其各种参数。</span><span class="sxs-lookup"><span data-stu-id="88360-104">Authorization in MVC is controlled through the `AuthorizeAttribute` attribute and its various parameters.</span></span> <span data-ttu-id="88360-105">简单地说，应用`AuthorizeAttribute`属性设为到控制器的控制器或操作限制访问或对任何经过身份验证的用户的操作。</span><span class="sxs-lookup"><span data-stu-id="88360-105">At its simplest, applying the `AuthorizeAttribute` attribute to a controller or action limits access to the controller or action to any authenticated user.</span></span>

<span data-ttu-id="88360-106">例如，下面的代码可访问的限制`AccountController`到任何经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="88360-106">For example, the following code limits access to the `AccountController` to any authenticated user.</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="88360-107">如果你想要应用于操作，而不是控制器的授权，应用`AuthorizeAttribute`属性设为操作本身：</span><span class="sxs-lookup"><span data-stu-id="88360-107">If you want to apply authorization to an action rather than the controller, apply the `AuthorizeAttribute` attribute to the action itself:</span></span>

```csharp
public class AccountController : Controller
{
   public ActionResult Login()
   {
   }

   [Authorize]
   public ActionResult Logout()
   {
   }
}
```

<span data-ttu-id="88360-108">现在，只有经过身份验证的用户可以访问`Logout`函数。</span><span class="sxs-lookup"><span data-stu-id="88360-108">Now only authenticated users can access the `Logout` function.</span></span>

<span data-ttu-id="88360-109">你还可以使用`AllowAnonymous`特性以允许使用的未经身份验证用户添加到各个操作进行访问。</span><span class="sxs-lookup"><span data-stu-id="88360-109">You can also use the `AllowAnonymous` attribute to allow access by non-authenticated users to individual actions.</span></span> <span data-ttu-id="88360-110">例如：</span><span class="sxs-lookup"><span data-stu-id="88360-110">For example:</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    [AllowAnonymous]
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="88360-111">这将允许仅经过身份验证的用户到`AccountController`，除`Login`操作，这是可访问的所有用户，而不考虑其经过身份验证或未经身份验证 / 匿名状态。</span><span class="sxs-lookup"><span data-stu-id="88360-111">This would allow only authenticated users to the `AccountController`, except for the `Login` action, which is accessible by everyone, regardless of their authenticated or unauthenticated / anonymous status.</span></span>

> [!WARNING]
> <span data-ttu-id="88360-112">`[AllowAnonymous]` 绕过所有授权语句。</span><span class="sxs-lookup"><span data-stu-id="88360-112">`[AllowAnonymous]` bypasses all authorization statements.</span></span> <span data-ttu-id="88360-113">如果合并`[AllowAnonymous]`和任何`[Authorize]`属性，`[Authorize]`属性将被忽略。</span><span class="sxs-lookup"><span data-stu-id="88360-113">If you combine `[AllowAnonymous]` and any `[Authorize]` attribute, the `[Authorize]` attributes are ignored.</span></span> <span data-ttu-id="88360-114">例如，如果将应用`[AllowAnonymous]`控制器级别中，任何`[Authorize]`属性在同一个控制器上 （或其中的任何操作） 将被忽略。</span><span class="sxs-lookup"><span data-stu-id="88360-114">For example if you apply `[AllowAnonymous]` at the controller level, any `[Authorize]` attributes on the same controller (or on any action within it) is ignored.</span></span>
