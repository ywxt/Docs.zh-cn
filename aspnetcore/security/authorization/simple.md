---
title: "简单的授权"
author: rick-anderson
description: "本文档说明如何使用 Authorize 属性限制对 ASP.NET Core 控制器和操作的访问。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/simple
ms.openlocfilehash: f1d5671785da815f2f4fcf5bef1352f4c9e62877
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="simple-authorization"></a>简单的授权

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

你还可以使用`AllowAnonymousAttribute`特性以允许使用的未经身份验证用户添加到各个操作进行访问。 例如:

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

>[!WARNING]
> `[AllowAnonymous]`绕过所有授权语句。 如果将应用组合`[AllowAnonymous]`和任何`[Authorize]`属性然后 Authorize 属性将始终忽略。 例如，如果将应用`[AllowAnonymous]`在控制器级别任何`[Authorize]`特性在同一个控制器上，或其中的任何操作都将被忽略。
