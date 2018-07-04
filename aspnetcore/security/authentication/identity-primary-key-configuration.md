---
title: 在 ASP.NET Core 中配置标识主键数据类型
author: AdrienTorris
description: 了解有关配置用于 ASP.NET Core 标识为主键的所需的数据类型的步骤。
ms.author: scaddie
ms.date: 09/28/2017
uid: security/authentication/identity-primary-key-configuration
ms.openlocfilehash: cfec91e1194556385bb884ee44cf79c1fcbbcb56
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274351"
---
# <a name="configure-identity-primary-key-data-type-in-aspnet-core"></a>在 ASP.NET Core 中配置标识主键数据类型

ASP.NET Core 标识可以配置用于表示为主键的数据类型。 标识使用`string`默认的数据类型。 你可以重写此行为。

## <a name="customize-the-primary-key-data-type"></a>自定义的主键数据类型

1. 创建的自定义实现[IdentityUser](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser-1)类。 它表示要用于创建用户对象的类型。 在下面的示例中，默认值`string`类型将替换`Guid`。

    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationUser.cs?highlight=4&range=7-13)]

2. 创建的自定义实现[IdentityRole](/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityrole-1)类。 它表示要用于创建角色对象的类型。 在下面的示例中，默认值`string`类型将替换`Guid`。

    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Models/ApplicationRole.cs?highlight=3&range=7-12)]

3. 创建一个自定义数据库上下文类。 它继承自用于标识的实体框架数据库上下文类。 `TUser`和`TRole`自变量引用分别在前一步骤中创建的自定义用户和角色类。 `Guid`为主键定义的数据类型。

    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Data/ApplicationDbContext.cs?highlight=3&range=9-26)]

4. 在应用程序的启动类添加身份验证服务时，请注册自定义数据库上下文类。

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

   `AddEntityFrameworkStores`方法不接受`TKey`自变量，因为它未在 ASP.NET Core 1.x。 主键的数据类型推断通过分析`DbContext`对象。

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=6-8&range=25-37)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

   `AddEntityFrameworkStores`方法接受`TKey`，该值指示主键的数据类型的自变量。

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?highlight=9-11&range=39-55)]

   ---

## <a name="test-the-changes"></a>测试更改

在完成配置更改，表示为主键的属性将反映新的数据类型。 下面的示例演示如何访问一个 MVC 控制器中的属性。

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Controllers/AccountController.cs?name=snippet_GetCurrentUserId&highlight=6)]
