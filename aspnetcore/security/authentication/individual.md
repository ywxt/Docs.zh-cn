---
title: 基于 ASP.NET Core 项目使用单个用户帐户创建项目
author: rick-anderson
description: 发现基于 ASP.NET Core 项目使用单个用户帐户创建的文章。
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: f7fb9e8cd1b5c4cc3283ddd7606a0bbd30f554d5
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274422"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a><span data-ttu-id="43c9b-103">基于 ASP.NET Core 项目使用单个用户帐户创建项目</span><span class="sxs-lookup"><span data-stu-id="43c9b-103">Articles based on ASP.NET Core projects created with individual user accounts</span></span>

<span data-ttu-id="43c9b-104">ASP.NET Core 标识包含在 Visual Studio 中使用"单个用户帐户"选项的项目模板中。</span><span class="sxs-lookup"><span data-stu-id="43c9b-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="43c9b-105">中使用的.NET Core CLI 中可用的身份验证模板`-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="43c9b-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new webapp -au Individual
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new webapi -au Individual
dotnet new razor -au Individual
```

::: moniker-end

<span data-ttu-id="43c9b-107">以下文章演示了如何使用 ASP.NET Core 使用单个用户帐户的模板中生成的代码：</span><span class="sxs-lookup"><span data-stu-id="43c9b-107">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="43c9b-108">使用 SMS 设置双因素身份验证</span><span class="sxs-lookup"><span data-stu-id="43c9b-108">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="43c9b-109">ASP.NET Core 中的帐户确认和密码恢复</span><span class="sxs-lookup"><span data-stu-id="43c9b-109">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="43c9b-110">使用受授权的用户数据创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="43c9b-110">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
