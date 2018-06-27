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
# <a name="simple-authorization-in-aspnet-core"></a>在 ASP.NET Core 中的简单授权

<a name="security-authorization-simple"></a>

通过控制在 MVC 中的授权`AuthorizeAttribute`属性和其各种参数。 简单地说，应用`AuthorizeAttribute`属性设为到控制器的控制器或操作限制访问或对任何经过身份验证的用户的操作。

例如，下面的代码可访问的限制`AccountController`到任何经过身份验证的用户。

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

如果你想要应用于操作，而不是控制器的授权，应用`AuthorizeAttribute`属性设为操作本身：

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

现在，只有经过身份验证的用户可以访问`Logout`函数。

你还可以使用`AllowAnonymous`特性以允许使用的未经身份验证用户添加到各个操作进行访问。 例如：

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

这将允许仅经过身份验证的用户到`AccountController`，除`Login`操作，这是可访问的所有用户，而不考虑其经过身份验证或未经身份验证 / 匿名状态。

> [!WARNING]
> `[AllowAnonymous]` 绕过所有授权语句。 如果合并`[AllowAnonymous]`和任何`[Authorize]`属性，`[Authorize]`属性将被忽略。 例如，如果将应用`[AllowAnonymous]`控制器级别中，任何`[Authorize]`属性在同一个控制器上 （或其中的任何操作） 将被忽略。
