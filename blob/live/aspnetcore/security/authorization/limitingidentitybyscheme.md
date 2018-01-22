---
title: "具有特定的方案-授权 ASP.NET 核心"
author: rick-anderson
description: "此文章介绍了如何使用多个身份验证方法时限制为特定方案的标识。"
ms.author: riande
manager: wpickett
ms.date: 10/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/limitingidentitybyscheme
ms.openlocfilehash: 099dba1a4235ef62ea298748645b99e2d6d12d44
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="authorize-with-a-specific-scheme"></a><span data-ttu-id="4a45c-103">具有特定方案授权</span><span class="sxs-lookup"><span data-stu-id="4a45c-103">Authorize with a specific scheme</span></span>

<span data-ttu-id="4a45c-104">在某些情况下，如单页面应用程序 (Spa) 很常见的是使用多个身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="4a45c-104">In some scenarios, such as Single Page Applications (SPAs), it's common to use multiple authentication methods.</span></span> <span data-ttu-id="4a45c-105">例如，应用可能会使用基于 cookie 的身份验证登录和 JWT 持有者身份验证的 JavaScript 请求。</span><span class="sxs-lookup"><span data-stu-id="4a45c-105">For example, the app may use cookie-based authentication to log in and JWT bearer authentication for JavaScript requests.</span></span> <span data-ttu-id="4a45c-106">在某些情况下，应用程序可能具有身份验证处理程序的多个的实例。</span><span class="sxs-lookup"><span data-stu-id="4a45c-106">In some cases, the app may have multiple instances of an authentication handler.</span></span> <span data-ttu-id="4a45c-107">例如，其中一个包含基本标识的两个 cookie 处理程序，另一个时创建已触发多因素身份验证 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="4a45c-107">For example, two cookie handlers where one contains a basic identity and one is created when a multi-factor authentication (MFA) has been triggered.</span></span> <span data-ttu-id="4a45c-108">用户请求要求额外的安全的操作，因此，可能会触发 MFA。</span><span class="sxs-lookup"><span data-stu-id="4a45c-108">MFA may be triggered because the user requested an operation that requires extra security.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="4a45c-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="4a45c-110">当在身份验证过程中配置身份验证服务，名为身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="4a45c-110">An authentication scheme is named when the authentication service is configured during authentication.</span></span> <span data-ttu-id="4a45c-111">例如:</span><span class="sxs-lookup"><span data-stu-id="4a45c-111">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication()
        .AddCookie(options => {
            options.LoginPath = "/Account/Unauthorized/";
            options.AccessDeniedPath = "/Account/Forbidden/";
        })
        .AddJwtBearer(options => {
            options.Audience = "http://localhost:5001/";
            options.Authority = "http://localhost:5000/";
        });
```

<span data-ttu-id="4a45c-112">已在前面的代码中，添加两个身份验证处理程序： 一个用于 cookie，一个用于持有者。</span><span class="sxs-lookup"><span data-stu-id="4a45c-112">In the preceding code, two authentication handlers have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="4a45c-113">指定的默认方案会导致`HttpContext.User`属性设置为该标识。</span><span class="sxs-lookup"><span data-stu-id="4a45c-113">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="4a45c-114">如果不需要该行为，禁用调用的无参数形式`AddAuthentication`。</span><span class="sxs-lookup"><span data-stu-id="4a45c-114">If that behavior isn't desired, disable it by invoking the parameterless form of `AddAuthentication`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="4a45c-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="4a45c-116">身份验证方案进行命名时在身份验证过程配置身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="4a45c-116">Authentication schemes are named when authentication middlewares are configured during authentication.</span></span> <span data-ttu-id="4a45c-117">例如:</span><span class="sxs-lookup"><span data-stu-id="4a45c-117">For example:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // Code omitted for brevity

    app.UseCookieAuthentication(new CookieAuthenticationOptions()
    {
        AuthenticationScheme = "Cookie",
        LoginPath = "/Account/Unauthorized/",
        AccessDeniedPath = "/Account/Forbidden/",
        AutomaticAuthenticate = false
    });
    
    app.UseJwtBearerAuthentication(new JwtBearerOptions()
    {
        AuthenticationScheme = "Bearer",
        AutomaticAuthenticate = false,
        Audience = "http://localhost:5001/",
        Authority = "http://localhost:5000/",
        RequireHttpsMetadata = false
    });
```

<span data-ttu-id="4a45c-118">已在前面的代码中，添加两个身份验证中间件： 一个用于 cookie，一个用于持有者。</span><span class="sxs-lookup"><span data-stu-id="4a45c-118">In the preceding code, two authentication middlewares have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="4a45c-119">指定的默认方案会导致`HttpContext.User`属性设置为该标识。</span><span class="sxs-lookup"><span data-stu-id="4a45c-119">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="4a45c-120">如果不需要该行为，禁用设置`AuthenticationOptions.AutomaticAuthenticate`属性`false`。</span><span class="sxs-lookup"><span data-stu-id="4a45c-120">If that behavior isn't desired, disable it by setting the `AuthenticationOptions.AutomaticAuthenticate` property to `false`.</span></span>

---

## <a name="selecting-the-scheme-with-the-authorize-attribute"></a><span data-ttu-id="4a45c-121">选择带有 Authorize 属性的方案</span><span class="sxs-lookup"><span data-stu-id="4a45c-121">Selecting the scheme with the Authorize attribute</span></span>

<span data-ttu-id="4a45c-122">在授权，终端应用指示要使用的处理程序。</span><span class="sxs-lookup"><span data-stu-id="4a45c-122">At the point of authorization, the app indicates the handler to be used.</span></span> <span data-ttu-id="4a45c-123">选择与应用程序将授权通过传递到身份验证方案的以逗号分隔列表的处理程序`[Authorize]`。</span><span class="sxs-lookup"><span data-stu-id="4a45c-123">Select the handler with which the app will authorize by passing a comma-delimited list of authentication schemes to `[Authorize]`.</span></span> <span data-ttu-id="4a45c-124">`[Authorize]`属性指定的身份验证方案或方案，可使用无论配置默认值。</span><span class="sxs-lookup"><span data-stu-id="4a45c-124">The `[Authorize]` attribute specifies the authentication scheme or schemes to use regardless of whether a default is configured.</span></span> <span data-ttu-id="4a45c-125">例如:</span><span class="sxs-lookup"><span data-stu-id="4a45c-125">For example:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="4a45c-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="4a45c-127">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-127">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

---

<span data-ttu-id="4a45c-128">在前面的示例中，cookie 和持有者处理程序运行，并有机会在创建并追加当前用户的标识。</span><span class="sxs-lookup"><span data-stu-id="4a45c-128">In the preceding example, both the cookie and bearer handlers run and have a chance to create and append an identity for the current user.</span></span> <span data-ttu-id="4a45c-129">通过指定一种方案，相应的处理程序运行。</span><span class="sxs-lookup"><span data-stu-id="4a45c-129">By specifying a single scheme only, the corresponding handler runs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="4a45c-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="4a45c-131">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="4a45c-131">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

---

<span data-ttu-id="4a45c-132">在前面的代码中，仅具有"Bearer"方案处理程序运行。</span><span class="sxs-lookup"><span data-stu-id="4a45c-132">In the preceding code, only the handler with the "Bearer" scheme runs.</span></span> <span data-ttu-id="4a45c-133">任何基于 cookie 的标识将被忽略。</span><span class="sxs-lookup"><span data-stu-id="4a45c-133">Any cookie-based identities are ignored.</span></span>

## <a name="selecting-the-scheme-with-policies"></a><span data-ttu-id="4a45c-134">选择使用策略的方案</span><span class="sxs-lookup"><span data-stu-id="4a45c-134">Selecting the scheme with policies</span></span>

<span data-ttu-id="4a45c-135">如果想要指定在所需的架构[策略](xref:security/authorization/policies)，你可以设置`AuthenticationSchemes`集合添加你的策略时：</span><span class="sxs-lookup"><span data-stu-id="4a45c-135">If you prefer to specify the desired schemes in [policy](xref:security/authorization/policies), you can set the `AuthenticationSchemes` collection when adding your policy:</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("Over18", policy =>
    {
        policy.AuthenticationSchemes.Add(JwtBearerDefaults.AuthenticationScheme);
        policy.RequireAuthenticatedUser();
        policy.Requirements.Add(new MinimumAgeRequirement());
    });
});
```

<span data-ttu-id="4a45c-136">在前面的示例中，"Over18"策略仅运行针对"Bearer"处理程序创建的标识。</span><span class="sxs-lookup"><span data-stu-id="4a45c-136">In the preceding example, the "Over18" policy only runs against the identity created by the "Bearer" handler.</span></span> <span data-ttu-id="4a45c-137">通过设置来使用策略`[Authorize]`特性的`Policy`属性：</span><span class="sxs-lookup"><span data-stu-id="4a45c-137">Use the policy by setting the `[Authorize]` attribute's `Policy` property:</span></span>

```csharp
[Authorize(Policy = "Over18")]
public class RegistrationController : Controller
```
