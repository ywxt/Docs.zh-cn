---
title: "配置 ASP.NET 核心标识"
author: AdrienTorris
description: "了解 ASP.NET 核心标识默认值，并配置要使用自定义值的各种标识属性。"
keywords: "ASP.NET 核心，标识、 身份验证安全性"
ms.author: scaddie
manager: wpickett
ms.date: 01/11/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-configuration
ms.openlocfilehash: ac204cb89aac1f90adc64c4f0bec4e946cb8c4d9
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="configure-identity"></a><span data-ttu-id="83cea-104">配置标识</span><span class="sxs-lookup"><span data-stu-id="83cea-104">Configure Identity</span></span>

<span data-ttu-id="83cea-105">ASP.NET 核心标识等密码策略、 锁定时间和可以在你的应用程序中轻松地重写的 cookie 设置应用程序中具有常见行为`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="83cea-105">ASP.NET Core Identity has common behaviors in applications such as password policy, lockout time, and cookie settings that you can override easily in your application's `Startup` class.</span></span>

## <a name="passwords-policy"></a><span data-ttu-id="83cea-106">密码策略</span><span class="sxs-lookup"><span data-stu-id="83cea-106">Passwords policy</span></span>

<span data-ttu-id="83cea-107">默认情况下，标识要求密码包含大写字符、 小写字符、 数字和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="83cea-107">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="83cea-108">此外，还有一些其他限制。</span><span class="sxs-lookup"><span data-stu-id="83cea-108">There are also some other restrictions.</span></span> <span data-ttu-id="83cea-109">若要简化密码限制，修改`ConfigureServices`方法`Startup`的你的应用程序的类。</span><span class="sxs-lookup"><span data-stu-id="83cea-109">To simplify password restrictions, modify the `ConfigureServices` method of the `Startup` class of your application.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="83cea-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="83cea-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="83cea-111">ASP.NET 核心 2.0 增加`RequiredUniqueChars`属性。</span><span class="sxs-lookup"><span data-stu-id="83cea-111">ASP.NET Core 2.0 added the `RequiredUniqueChars` property.</span></span> <span data-ttu-id="83cea-112">否则，选项是从 ASP.NET Core 相同 1.x。</span><span class="sxs-lookup"><span data-stu-id="83cea-112">Otherwise, the options are the same from ASP.NET Core 1.x.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="83cea-113">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="83cea-113">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

---

<span data-ttu-id="83cea-114">`IdentityOptions.Password`具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="83cea-114">`IdentityOptions.Password` has the following properties:</span></span>

| <span data-ttu-id="83cea-115">属性</span><span class="sxs-lookup"><span data-stu-id="83cea-115">Property</span></span>                | <span data-ttu-id="83cea-116">描述</span><span class="sxs-lookup"><span data-stu-id="83cea-116">Description</span></span>                       | <span data-ttu-id="83cea-117">默认</span><span class="sxs-lookup"><span data-stu-id="83cea-117">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireDigit`          | <span data-ttu-id="83cea-118">需要介于 0-9 中的密码。</span><span class="sxs-lookup"><span data-stu-id="83cea-118">Requires a number between 0-9 in the password.</span></span> | <span data-ttu-id="83cea-119">true</span><span class="sxs-lookup"><span data-stu-id="83cea-119">true</span></span> |
| `RequiredLength`        | <span data-ttu-id="83cea-120">密码最小长度。</span><span class="sxs-lookup"><span data-stu-id="83cea-120">The minimum length of the password.</span></span> | <span data-ttu-id="83cea-121">6</span><span class="sxs-lookup"><span data-stu-id="83cea-121">6</span></span> |
| `RequireNonAlphanumeric`| <span data-ttu-id="83cea-122">需要密码中的非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="83cea-122">Requires a non-alphanumeric character in the password.</span></span> | <span data-ttu-id="83cea-123">true</span><span class="sxs-lookup"><span data-stu-id="83cea-123">true</span></span> |
| `RequireUppercase`      | <span data-ttu-id="83cea-124">需要密码中的大写字符。</span><span class="sxs-lookup"><span data-stu-id="83cea-124">Requires an upper case character in the password.</span></span> | <span data-ttu-id="83cea-125">true</span><span class="sxs-lookup"><span data-stu-id="83cea-125">true</span></span> |
| `RequireLowercase`      | <span data-ttu-id="83cea-126">需要密码中的小写字符。</span><span class="sxs-lookup"><span data-stu-id="83cea-126">Requires a lower case character in the password.</span></span> | <span data-ttu-id="83cea-127">true</span><span class="sxs-lookup"><span data-stu-id="83cea-127">true</span></span> |
| `RequiredUniqueChars`   | <span data-ttu-id="83cea-128">需要密码中的非重复字符数。</span><span class="sxs-lookup"><span data-stu-id="83cea-128">Requires the number of distinct characters in the password.</span></span> | <span data-ttu-id="83cea-129">1</span><span class="sxs-lookup"><span data-stu-id="83cea-129">1</span></span> |


## <a name="users-lockout"></a><span data-ttu-id="83cea-130">用户的锁定</span><span class="sxs-lookup"><span data-stu-id="83cea-130">User's lockout</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,39-42,50-52)]

<span data-ttu-id="83cea-131">`IdentityOptions.Lockout`具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="83cea-131">`IdentityOptions.Lockout` has the following properties:</span></span>

| <span data-ttu-id="83cea-132">属性</span><span class="sxs-lookup"><span data-stu-id="83cea-132">Property</span></span>                | <span data-ttu-id="83cea-133">描述</span><span class="sxs-lookup"><span data-stu-id="83cea-133">Description</span></span>                       | <span data-ttu-id="83cea-134">默认</span><span class="sxs-lookup"><span data-stu-id="83cea-134">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `DefaultLockoutTimeSpan` | <span data-ttu-id="83cea-135">时间量锁定用户锁定发生时。</span><span class="sxs-lookup"><span data-stu-id="83cea-135">The amount of time a user is locked out when a lockout occurs.</span></span>  | <span data-ttu-id="83cea-136">5 分钟</span><span class="sxs-lookup"><span data-stu-id="83cea-136">5 minutes</span></span>  |
| `MaxFailedAccessAttempts` | <span data-ttu-id="83cea-137">失败的访问尝试，直到用户已被锁定，如果启用了锁定次数。</span><span class="sxs-lookup"><span data-stu-id="83cea-137">The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span>  | <span data-ttu-id="83cea-138">5</span><span class="sxs-lookup"><span data-stu-id="83cea-138">5</span></span> |
| `AllowedForNewUsers` | <span data-ttu-id="83cea-139">确定是否新用户会被锁定。</span><span class="sxs-lookup"><span data-stu-id="83cea-139">Determines if a new user can be locked out.</span></span>  | <span data-ttu-id="83cea-140">true</span><span class="sxs-lookup"><span data-stu-id="83cea-140">true</span></span> |

## <a name="sign-in-settings"></a><span data-ttu-id="83cea-141">登录设置</span><span class="sxs-lookup"><span data-stu-id="83cea-141">Sign in settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)]

<span data-ttu-id="83cea-142">`IdentityOptions.SignIn`具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="83cea-142">`IdentityOptions.SignIn` has the following properties:</span></span>

| <span data-ttu-id="83cea-143">属性</span><span class="sxs-lookup"><span data-stu-id="83cea-143">Property</span></span>                | <span data-ttu-id="83cea-144">描述</span><span class="sxs-lookup"><span data-stu-id="83cea-144">Description</span></span>                       | <span data-ttu-id="83cea-145">默认</span><span class="sxs-lookup"><span data-stu-id="83cea-145">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireConfirmedEmail` | <span data-ttu-id="83cea-146">需要登录的确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="83cea-146">Requires a confirmed email to sign in.</span></span> | <span data-ttu-id="83cea-147">False</span><span class="sxs-lookup"><span data-stu-id="83cea-147">false</span></span>  |
| `RequireConfirmedPhoneNumber` |  <span data-ttu-id="83cea-148">需要一个确认的电话号码来登录。</span><span class="sxs-lookup"><span data-stu-id="83cea-148">Requires a confirmed phone number to sign in.</span></span> | <span data-ttu-id="83cea-149">False</span><span class="sxs-lookup"><span data-stu-id="83cea-149">false</span></span>  |

## <a name="user-validation-settings"></a><span data-ttu-id="83cea-150">用户验证设置</span><span class="sxs-lookup"><span data-stu-id="83cea-150">User validation settings</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,48-52)]

<span data-ttu-id="83cea-151">`IdentityOptions.User`具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="83cea-151">`IdentityOptions.User` has the following properties:</span></span>

| <span data-ttu-id="83cea-152">属性</span><span class="sxs-lookup"><span data-stu-id="83cea-152">Property</span></span>                | <span data-ttu-id="83cea-153">描述</span><span class="sxs-lookup"><span data-stu-id="83cea-153">Description</span></span>                       | <span data-ttu-id="83cea-154">默认</span><span class="sxs-lookup"><span data-stu-id="83cea-154">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `RequireUniqueEmail`  | <span data-ttu-id="83cea-155">要求每个用户具有唯一的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="83cea-155">Requires each User to have a unique email.</span></span> | <span data-ttu-id="83cea-156">False</span><span class="sxs-lookup"><span data-stu-id="83cea-156">false</span></span>  |
| `AllowedUserNameCharacters`  | <span data-ttu-id="83cea-157">允许使用的用户名中的字符。</span><span class="sxs-lookup"><span data-stu-id="83cea-157">Allowed characters in the username.</span></span> | <span data-ttu-id="83cea-158">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span><span class="sxs-lookup"><span data-stu-id="83cea-158">abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+</span></span> |


## <a name="applications-cookie-settings"></a><span data-ttu-id="83cea-159">应用程序的 cookie 设置</span><span class="sxs-lookup"><span data-stu-id="83cea-159">Application's cookie settings</span></span>

<span data-ttu-id="83cea-160">密码策略，如应用程序的 cookie 的所有设置可以都更改在`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="83cea-160">Like the passwords policy, all the settings of the application's cookie can be changed in the `Startup` class.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="83cea-161">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="83cea-161">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="83cea-162">下`ConfigureServices`中`Startup`类，你可以配置应用程序的 cookie。</span><span class="sxs-lookup"><span data-stu-id="83cea-162">Under `ConfigureServices` in the `Startup` class, you can configure the application's cookie.</span></span>

[!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="83cea-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="83cea-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

---

<span data-ttu-id="83cea-164">`CookieAuthenticationOptions`具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="83cea-164">`CookieAuthenticationOptions` has the following properties:</span></span>

| <span data-ttu-id="83cea-165">属性</span><span class="sxs-lookup"><span data-stu-id="83cea-165">Property</span></span>                | <span data-ttu-id="83cea-166">描述</span><span class="sxs-lookup"><span data-stu-id="83cea-166">Description</span></span>                       | <span data-ttu-id="83cea-167">默认</span><span class="sxs-lookup"><span data-stu-id="83cea-167">Default</span></span> |
| ----------------------- | --------------------------------- | ------- |
| `Cookie.Name`  | <span data-ttu-id="83cea-168">Cookie 的名称。</span><span class="sxs-lookup"><span data-stu-id="83cea-168">The name of the cookie.</span></span>  | <span data-ttu-id="83cea-169">.AspNetCore.Cookies。</span><span class="sxs-lookup"><span data-stu-id="83cea-169">.AspNetCore.Cookies.</span></span>  |
| `Cookie.HttpOnly`  | <span data-ttu-id="83cea-170">为 true 时，cookie 不能从客户端脚本访问。</span><span class="sxs-lookup"><span data-stu-id="83cea-170">When true, the cookie is not accessible from client-side scripts.</span></span>  |  <span data-ttu-id="83cea-171">true</span><span class="sxs-lookup"><span data-stu-id="83cea-171">true</span></span> |
| `ExpireTimeSpan`  | <span data-ttu-id="83cea-172">控制在 cookie 中存储身份验证票证的时间就会保持有效从它创建的点。</span><span class="sxs-lookup"><span data-stu-id="83cea-172">Controls how much time the authentication ticket stored in the cookie will remain valid from the point it is created.</span></span>  | <span data-ttu-id="83cea-173">14 天</span><span class="sxs-lookup"><span data-stu-id="83cea-173">14 days</span></span>  |
| `LoginPath`  | <span data-ttu-id="83cea-174">未授权用户时，他们将被重定向到登录到此路径。</span><span class="sxs-lookup"><span data-stu-id="83cea-174">When a user is unauthorized, they will be redirected to this path to login.</span></span> | <span data-ttu-id="83cea-175">/ 帐户/登录名</span><span class="sxs-lookup"><span data-stu-id="83cea-175">/Account/Login</span></span>  |
| `LogoutPath`  | <span data-ttu-id="83cea-176">当用户已注销时，则将被重定向到此路径。</span><span class="sxs-lookup"><span data-stu-id="83cea-176">When a user is logged out, they will be redirected to this path.</span></span>  | <span data-ttu-id="83cea-177">/ 帐户/注销</span><span class="sxs-lookup"><span data-stu-id="83cea-177">/Account/Logout</span></span>  |
| `AccessDeniedPath`  | <span data-ttu-id="83cea-178">当用户失败时授权检查时，则将被重定向到此路径。</span><span class="sxs-lookup"><span data-stu-id="83cea-178">When a user fails an authorization check, they will be redirected to this path.</span></span>  |   |
| `SlidingExpiration`  | <span data-ttu-id="83cea-179">为 true 时，将使用新的过期时间，当前 cookie 时通过到期窗口的多个中间颁发一个新的 cookie。</span><span class="sxs-lookup"><span data-stu-id="83cea-179">When true, a new cookie will be issued with a new expiration time when the current cookie is more than halfway through the expiration window.</span></span>  | <span data-ttu-id="83cea-180">/ 帐户/AccessDenied</span><span class="sxs-lookup"><span data-stu-id="83cea-180">/Account/AccessDenied</span></span> |
| `ReturnUrlParameter`  | <span data-ttu-id="83cea-181">确定其 401 未授权的状态代码更改为 302 重定向到登录名路径时，该中间件会追加查询字符串参数的名称。</span><span class="sxs-lookup"><span data-stu-id="83cea-181">Determines the name of the query string parameter which is appended by the middleware when a 401 Unauthorized status code is changed to a 302 redirect onto the login path.</span></span>  |  <span data-ttu-id="83cea-182">true</span><span class="sxs-lookup"><span data-stu-id="83cea-182">true</span></span> |
| `AuthenticationScheme`  | <span data-ttu-id="83cea-183">这是仅适用于 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="83cea-183">This is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="83cea-184">特定的身份验证方案逻辑名称。</span><span class="sxs-lookup"><span data-stu-id="83cea-184">The logical name for a particular authentication scheme.</span></span> |  |
| `AutomaticAuthenticate`  | <span data-ttu-id="83cea-185">此标志才适用于 ASP.NET Core 1.x。</span><span class="sxs-lookup"><span data-stu-id="83cea-185">This flag is only relevant for ASP.NET Core 1.x.</span></span> <span data-ttu-id="83cea-186">为 true 时，cookie 身份验证应在每个请求上运行并尝试验证并重新构造它创建的任何序列化的主体。</span><span class="sxs-lookup"><span data-stu-id="83cea-186">When true, cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span>  |  |