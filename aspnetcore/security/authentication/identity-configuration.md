---
title: 配置 ASP.NET Core 标识
author: AdrienTorris
description: 了解 ASP.NET Core 标识默认值，并了解如何配置要使用自定义值的标识属性。
ms.author: riande
ms.date: 08/14/2018
uid: security/authentication/identity-configuration
ms.openlocfilehash: 02441cd28c2a99eda7b50ed54f4437d4b52ca5d9
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48911927"
---
# <a name="configure-aspnet-core-identity"></a><span data-ttu-id="f2c8c-103">配置 ASP.NET Core 标识</span><span class="sxs-lookup"><span data-stu-id="f2c8c-103">Configure ASP.NET Core Identity</span></span>

<span data-ttu-id="f2c8c-104">ASP.NET Core 标识设置，例如密码策略、 锁定和 cookie 配置使用默认值。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-104">ASP.NET Core Identity uses default values for settings such as password policy, lockout, and cookie configuration.</span></span> <span data-ttu-id="f2c8c-105">在中，可以重写这些设置`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-105">These settings can be overridden in the `Startup` class.</span></span>

## <a name="identity-options"></a><span data-ttu-id="f2c8c-106">标识选项</span><span class="sxs-lookup"><span data-stu-id="f2c8c-106">Identity options</span></span>

<span data-ttu-id="f2c8c-107">[IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions)类表示可用于标识系统配置的选项。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-107">The [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) class represents the options that can be used to configure the Identity system.</span></span> <span data-ttu-id="f2c8c-108">`IdentityOptions` 必须设置**后**调用`AddIdentity`或`AddDefaultIdentity`。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-108">`IdentityOptions` must be set **after** calling `AddIdentity` or `AddDefaultIdentity`.</span></span>

### <a name="claims-identity"></a><span data-ttu-id="f2c8c-109">声明标识</span><span class="sxs-lookup"><span data-stu-id="f2c8c-109">Claims Identity</span></span>

<span data-ttu-id="f2c8c-110">[IdentityOptions.ClaimsIdentity](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.claimsidentity)指定[ClaimsIdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions)与下表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-110">[IdentityOptions.ClaimsIdentity](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.claimsidentity) specifies the [ClaimsIdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions) with the properties shown in the following table.</span></span>

| <span data-ttu-id="f2c8c-111">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-111">Property</span></span> | <span data-ttu-id="f2c8c-112">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-112">Description</span></span> | <span data-ttu-id="f2c8c-113">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-113">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-114">RoleClaimType</span><span class="sxs-lookup"><span data-stu-id="f2c8c-114">RoleClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.roleclaimtype) | <span data-ttu-id="f2c8c-115">获取或设置用于为角色声明的声明类型。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-115">Gets or sets the claim type used for a role claim.</span></span> | [<span data-ttu-id="f2c8c-116">ClaimTypes.Role</span><span class="sxs-lookup"><span data-stu-id="f2c8c-116">ClaimTypes.Role</span></span>](/dotnet/api/system.security.claims.claimtypes.role) |
| [<span data-ttu-id="f2c8c-117">SecurityStampClaimType</span><span class="sxs-lookup"><span data-stu-id="f2c8c-117">SecurityStampClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.securitystampclaimtype) | <span data-ttu-id="f2c8c-118">获取或设置用于安全戳声明的声明类型。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-118">Gets or sets the claim type used for the security stamp claim.</span></span> | `AspNet.Identity.SecurityStamp` |
| [<span data-ttu-id="f2c8c-119">UserIdClaimType</span><span class="sxs-lookup"><span data-stu-id="f2c8c-119">UserIdClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.useridclaimtype) | <span data-ttu-id="f2c8c-120">获取或设置用于的用户标识符声明的声明类型。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-120">Gets or sets the claim type used for the user identifier claim.</span></span> | [<span data-ttu-id="f2c8c-121">ClaimTypes.NameIdentifier</span><span class="sxs-lookup"><span data-stu-id="f2c8c-121">ClaimTypes.NameIdentifier</span></span>](/dotnet/api/system.security.claims.claimtypes.nameidentifier) |
| [<span data-ttu-id="f2c8c-122">UserNameClaimType</span><span class="sxs-lookup"><span data-stu-id="f2c8c-122">UserNameClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.usernameclaimtype) | <span data-ttu-id="f2c8c-123">获取或设置用于用户名称声明的声明类型。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-123">Gets or sets the claim type used for the user name claim.</span></span> | [<span data-ttu-id="f2c8c-124">ClaimTypes.Name</span><span class="sxs-lookup"><span data-stu-id="f2c8c-124">ClaimTypes.Name</span></span>](/dotnet/api/system.security.claims.claimtypes.name) |

### <a name="lockout"></a><span data-ttu-id="f2c8c-125">锁定</span><span class="sxs-lookup"><span data-stu-id="f2c8c-125">Lockout</span></span>

<span data-ttu-id="f2c8c-126">在中设置锁定[PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync#Microsoft_AspNetCore_Identity_SignInManager_1_PasswordSignInAsync_System_String_System_String_System_Boolean_System_Boolean_)方法：</span><span class="sxs-lookup"><span data-stu-id="f2c8c-126">Lockout is set in the [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync#Microsoft_AspNetCore_Identity_SignInManager_1_PasswordSignInAsync_System_String_System_String_System_Boolean_System_Boolean_) method:</span></span>

[!code-csharp[](identity-configuration/sample/Areas/Identity/Pages/Account/Login.cshtml.cs?name=snippet&highlight=9)]

<span data-ttu-id="f2c8c-127">前面的代码基于`Login`标识模板。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-127">The preceding code is based on the `Login` Identity template.</span></span> 

<span data-ttu-id="f2c8c-128">在中设置锁定选项`StartUp.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="f2c8c-128">Lockout options are set in `StartUp.ConfigureServices`:</span></span>

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_lock)]

<span data-ttu-id="f2c8c-129">上述代码会设置[IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions)具有默认值。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-129">The preceding code sets the [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) with default values.</span></span>

<span data-ttu-id="f2c8c-130">成功的身份验证失败的访问尝试计数重置并重置时钟。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-130">A successful authentication resets the failed access attempts count and resets the clock.</span></span>

<span data-ttu-id="f2c8c-131">[IdentityOptions.Lockout](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.lockout)指定[LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions)与表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-131">[IdentityOptions.Lockout](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.lockout) specifies the [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="f2c8c-132">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-132">Property</span></span> | <span data-ttu-id="f2c8c-133">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-133">Description</span></span> | <span data-ttu-id="f2c8c-134">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-134">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-135">AllowedForNewUsers</span><span class="sxs-lookup"><span data-stu-id="f2c8c-135">AllowedForNewUsers</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.allowedfornewusers) | <span data-ttu-id="f2c8c-136">确定是否新用户会被锁定。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-136">Determines if a new user can be locked out.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-137">DefaultLockoutTimeSpan</span><span class="sxs-lookup"><span data-stu-id="f2c8c-137">DefaultLockoutTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan) | <span data-ttu-id="f2c8c-138">时间量用户已锁定时在锁定时发生。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-138">The amount of time a user is locked out when a lockout occurs.</span></span> | <span data-ttu-id="f2c8c-139">5 分钟</span><span class="sxs-lookup"><span data-stu-id="f2c8c-139">5 minutes</span></span> |
| [<span data-ttu-id="f2c8c-140">MaxFailedAccessAttempts</span><span class="sxs-lookup"><span data-stu-id="f2c8c-140">MaxFailedAccessAttempts</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) | <span data-ttu-id="f2c8c-141">用户已被锁定，如果启用了锁定前的失败的访问尝试数。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-141">The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span> | <span data-ttu-id="f2c8c-142">5</span><span class="sxs-lookup"><span data-stu-id="f2c8c-142">5</span></span> |

### <a name="password"></a><span data-ttu-id="f2c8c-143">Password</span><span class="sxs-lookup"><span data-stu-id="f2c8c-143">Password</span></span>

<span data-ttu-id="f2c8c-144">默认情况下，标识要求密码包含大写字符、 小写字符、 数字、 和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-144">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="f2c8c-145">密码必须至少为六个字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-145">Passwords must be at least six characters long.</span></span> <span data-ttu-id="f2c8c-146">[PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions)可以设置`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-146">[PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) can be set in `Startup.ConfigureServices`.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_pw)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

::: moniker-end

<span data-ttu-id="f2c8c-147">[IdentityOptions.Password](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.password)指定[PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions)与表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-147">[IdentityOptions.Password](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.password) specifies the [PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) with the properties shown in the table.</span></span>

::: moniker range=">= aspnetcore-2.0"

| <span data-ttu-id="f2c8c-148">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-148">Property</span></span> | <span data-ttu-id="f2c8c-149">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-149">Description</span></span> | <span data-ttu-id="f2c8c-150">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-150">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-151">RequireDigit</span><span class="sxs-lookup"><span data-stu-id="f2c8c-151">RequireDigit</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredigit) | <span data-ttu-id="f2c8c-152">需要介于 0-9 的密码。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-152">Requires a number between 0-9 in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-153">RequiredLength</span><span class="sxs-lookup"><span data-stu-id="f2c8c-153">RequiredLength</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredlength) | <span data-ttu-id="f2c8c-154">密码最小长度。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-154">The minimum length of the password.</span></span> | <span data-ttu-id="f2c8c-155">6</span><span class="sxs-lookup"><span data-stu-id="f2c8c-155">6</span></span> |
| [<span data-ttu-id="f2c8c-156">RequireLowercase</span><span class="sxs-lookup"><span data-stu-id="f2c8c-156">RequireLowercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirelowercase) | <span data-ttu-id="f2c8c-157">要求密码中的小写字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-157">Requires a lowercase character in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-158">RequireNonAlphanumeric</span><span class="sxs-lookup"><span data-stu-id="f2c8c-158">RequireNonAlphanumeric</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirenonalphanumeric) | <span data-ttu-id="f2c8c-159">需要在密码中的非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-159">Requires a non-alphanumeric character in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-160">RequiredUniqueChars</span><span class="sxs-lookup"><span data-stu-id="f2c8c-160">RequiredUniqueChars</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireduniquechars) | <span data-ttu-id="f2c8c-161">仅适用于 ASP.NET Core 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-161">Only applies to ASP.NET Core 2.0 or later.</span></span><br><br> <span data-ttu-id="f2c8c-162">要求在密码中非重复字符数。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-162">Requires the number of distinct characters in the password.</span></span> | <span data-ttu-id="f2c8c-163">1</span><span class="sxs-lookup"><span data-stu-id="f2c8c-163">1</span></span> |
| [<span data-ttu-id="f2c8c-164">RequireUppercase</span><span class="sxs-lookup"><span data-stu-id="f2c8c-164">RequireUppercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireuppercase) | <span data-ttu-id="f2c8c-165">需要大写字符的密码。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-165">Requires an uppercase character in the password.</span></span> | `true` |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| <span data-ttu-id="f2c8c-166">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-166">Property</span></span> | <span data-ttu-id="f2c8c-167">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-167">Description</span></span> | <span data-ttu-id="f2c8c-168">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-168">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-169">RequireDigit</span><span class="sxs-lookup"><span data-stu-id="f2c8c-169">RequireDigit</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredigit) | <span data-ttu-id="f2c8c-170">需要介于 0-9 的密码。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-170">Requires a number between 0-9 in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-171">RequiredLength</span><span class="sxs-lookup"><span data-stu-id="f2c8c-171">RequiredLength</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredlength) | <span data-ttu-id="f2c8c-172">密码最小长度。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-172">The minimum length of the password.</span></span> | <span data-ttu-id="f2c8c-173">6</span><span class="sxs-lookup"><span data-stu-id="f2c8c-173">6</span></span> |
| [<span data-ttu-id="f2c8c-174">RequireLowercase</span><span class="sxs-lookup"><span data-stu-id="f2c8c-174">RequireLowercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirelowercase) | <span data-ttu-id="f2c8c-175">要求密码中的小写字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-175">Requires a lowercase character in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-176">RequireNonAlphanumeric</span><span class="sxs-lookup"><span data-stu-id="f2c8c-176">RequireNonAlphanumeric</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirenonalphanumeric) | <span data-ttu-id="f2c8c-177">需要在密码中的非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-177">Requires a non-alphanumeric character in the password.</span></span> | `true` |
| [<span data-ttu-id="f2c8c-178">RequireUppercase</span><span class="sxs-lookup"><span data-stu-id="f2c8c-178">RequireUppercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireuppercase) | <span data-ttu-id="f2c8c-179">需要大写字符的密码。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-179">Requires an uppercase character in the password.</span></span> | `true` |

::: moniker-end

### <a name="sign-in"></a><span data-ttu-id="f2c8c-180">单一登录</span><span class="sxs-lookup"><span data-stu-id="f2c8c-180">Sign-in</span></span>

<span data-ttu-id="f2c8c-181">下面的代码设置`SignIn`（为默认值） 的设置：</span><span class="sxs-lookup"><span data-stu-id="f2c8c-181">The following code sets `SignIn` settings (to default values):</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_si)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)] 

::: moniker-end

<span data-ttu-id="f2c8c-182">[IdentityOptions.SignIn](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.signin)指定[SignInOptions](/dotnet/api/microsoft.aspnetcore.identity.signinoptions)与表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-182">[IdentityOptions.SignIn](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.signin) specifies the [SignInOptions](/dotnet/api/microsoft.aspnetcore.identity.signinoptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="f2c8c-183">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-183">Property</span></span> | <span data-ttu-id="f2c8c-184">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-184">Description</span></span> | <span data-ttu-id="f2c8c-185">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-185">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-186">RequireConfirmedEmail</span><span class="sxs-lookup"><span data-stu-id="f2c8c-186">RequireConfirmedEmail</span></span>](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedemail) | <span data-ttu-id="f2c8c-187">需要已确认的电子邮件，登录。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-187">Requires a confirmed email to sign in.</span></span> | `false` |
| [<span data-ttu-id="f2c8c-188">RequireConfirmedPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="f2c8c-188">RequireConfirmedPhoneNumber</span></span>](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedphonenumber) | <span data-ttu-id="f2c8c-189">需要确认的电话号码进行登录。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-189">Requires a confirmed phone number to sign in.</span></span> | `false` |

### <a name="tokens"></a><span data-ttu-id="f2c8c-190">标记</span><span class="sxs-lookup"><span data-stu-id="f2c8c-190">Tokens</span></span>

<span data-ttu-id="f2c8c-191">[IdentityOptions.Tokens](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.tokens)指定[TokenOptions](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions)与表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-191">[IdentityOptions.Tokens](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.tokens) specifies the [TokenOptions](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions) with the properties shown in the table.</span></span>


|                                                        <span data-ttu-id="f2c8c-192">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-192">Property</span></span>                                                         |                                                                                      <span data-ttu-id="f2c8c-193">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-193">Description</span></span>                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     [<span data-ttu-id="f2c8c-194">AuthenticatorTokenProvider</span><span class="sxs-lookup"><span data-stu-id="f2c8c-194">AuthenticatorTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.authenticatortokenprovider)     |                                       <span data-ttu-id="f2c8c-195">获取或设置`AuthenticatorTokenProvider`用于验证身份验证器使用双因素登录名。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-195">Gets or sets the `AuthenticatorTokenProvider` used to validate two-factor sign-ins with an authenticator.</span></span>                                       |
|       [<span data-ttu-id="f2c8c-196">ChangeEmailTokenProvider</span><span class="sxs-lookup"><span data-stu-id="f2c8c-196">ChangeEmailTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changeemailtokenprovider)       |                                     <span data-ttu-id="f2c8c-197">获取或设置`ChangeEmailTokenProvider`用于生成电子邮件更改确认电子邮件中使用的令牌。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-197">Gets or sets the `ChangeEmailTokenProvider` used to generate tokens used in email change confirmation emails.</span></span>                                     |
| [<span data-ttu-id="f2c8c-198">ChangePhoneNumberTokenProvider</span><span class="sxs-lookup"><span data-stu-id="f2c8c-198">ChangePhoneNumberTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changephonenumbertokenprovider) |                                      <span data-ttu-id="f2c8c-199">获取或设置`ChangePhoneNumberTokenProvider`用于生成令牌更改电话号码时使用。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-199">Gets or sets the `ChangePhoneNumberTokenProvider` used to generate tokens used when changing phone numbers.</span></span>                                      |
| [<span data-ttu-id="f2c8c-200">EmailConfirmationTokenProvider</span><span class="sxs-lookup"><span data-stu-id="f2c8c-200">EmailConfirmationTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.emailconfirmationtokenprovider) |                                             <span data-ttu-id="f2c8c-201">获取或设置用于生成帐户确认电子邮件中使用的令牌的令牌提供程序。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-201">Gets or sets the token provider used to generate tokens used in account confirmation emails.</span></span>                                              |
|     [<span data-ttu-id="f2c8c-202">PasswordResetTokenProvider</span><span class="sxs-lookup"><span data-stu-id="f2c8c-202">PasswordResetTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.passwordresettokenprovider)     | <span data-ttu-id="f2c8c-203">获取或设置[IUserTwoFactorTokenProvider<TUser> ](/dotnet/api/microsoft.aspnetcore.identity.iusertwofactortokenprovider-1)用于生成在密码重置电子邮件中使用的令牌。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-203">Gets or sets the [IUserTwoFactorTokenProvider<TUser>](/dotnet/api/microsoft.aspnetcore.identity.iusertwofactortokenprovider-1) used to generate tokens used in password reset emails.</span></span> |
|                    [<span data-ttu-id="f2c8c-204">ProviderMap</span><span class="sxs-lookup"><span data-stu-id="f2c8c-204">ProviderMap</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.providermap)                    |                <span data-ttu-id="f2c8c-205">用于构造[用户令牌提供程序](/dotnet/api/microsoft.aspnetcore.identity.tokenproviderdescriptor)与键用作提供程序的名称。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-205">Used to construct a [User Token Provider](/dotnet/api/microsoft.aspnetcore.identity.tokenproviderdescriptor) with the key used as the provider's name.</span></span>                 |

### <a name="user"></a><span data-ttu-id="f2c8c-206">“用户”</span><span class="sxs-lookup"><span data-stu-id="f2c8c-206">User</span></span>

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_user)]

<span data-ttu-id="f2c8c-207">[IdentityOptions.User](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.user)指定[UserOptions](/dotnet/api/microsoft.aspnetcore.identity.useroptions)与表中所示的属性。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-207">[IdentityOptions.User](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.user) specifies the [UserOptions](/dotnet/api/microsoft.aspnetcore.identity.useroptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="f2c8c-208">属性</span><span class="sxs-lookup"><span data-stu-id="f2c8c-208">Property</span></span> | <span data-ttu-id="f2c8c-209">描述</span><span class="sxs-lookup"><span data-stu-id="f2c8c-209">Description</span></span> | <span data-ttu-id="f2c8c-210">默认</span><span class="sxs-lookup"><span data-stu-id="f2c8c-210">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="f2c8c-211">AllowedUserNameCharacters</span><span class="sxs-lookup"><span data-stu-id="f2c8c-211">AllowedUserNameCharacters</span></span>](/dotnet/api/microsoft.aspnetcore.identity.useroptions.allowedusernamecharacters) | <span data-ttu-id="f2c8c-212">在用户名中允许的字符。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-212">Allowed characters in the username.</span></span> | <span data-ttu-id="f2c8c-213">abcdefghijklmnopqrstuvwxyz</span><span class="sxs-lookup"><span data-stu-id="f2c8c-213">abcdefghijklmnopqrstuvwxyz</span></span><br><span data-ttu-id="f2c8c-214">ABCDEFGHIJKLMNOPQRSTUVWXYZ</span><span class="sxs-lookup"><span data-stu-id="f2c8c-214">ABCDEFGHIJKLMNOPQRSTUVWXYZ</span></span><br><span data-ttu-id="f2c8c-215">0123456789</span><span class="sxs-lookup"><span data-stu-id="f2c8c-215">0123456789</span></span><br><span data-ttu-id="f2c8c-216">-.\_@+</span><span class="sxs-lookup"><span data-stu-id="f2c8c-216">-.\_@+</span></span> |
| [<span data-ttu-id="f2c8c-217">RequireUniqueEmail</span><span class="sxs-lookup"><span data-stu-id="f2c8c-217">RequireUniqueEmail</span></span>](/dotnet/api/microsoft.aspnetcore.identity.useroptions.requireuniqueemail) | <span data-ttu-id="f2c8c-218">要求每个用户必须拥有唯一的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-218">Requires each user to have a unique email.</span></span> | `false` |

### <a name="cookie-settings"></a><span data-ttu-id="f2c8c-219">Cookie 设置</span><span class="sxs-lookup"><span data-stu-id="f2c8c-219">Cookie settings</span></span>

<span data-ttu-id="f2c8c-220">配置中的应用程序的 cookie `Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-220">Configure the app's cookie in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="f2c8c-221">[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_ConfigureApplicationCookie_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_Cookies_CookieAuthenticationOptions__)必须在调用**后**调用`AddIdentity`或`AddDefaultIdentity`。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-221">[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_ConfigureApplicationCookie_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_Cookies_CookieAuthenticationOptions__) must be called **after** calling `AddIdentity` or `AddDefaultIdentity`.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_cookie)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

::: moniker-end

<span data-ttu-id="f2c8c-222">有关详细信息，请参阅[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions)。</span><span class="sxs-lookup"><span data-stu-id="f2c8c-222">For more information, see [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions).</span></span>
