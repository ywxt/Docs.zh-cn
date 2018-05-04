---
title: 使用 cookie 而无需 ASP.NET 核心标识的身份验证
author: rick-anderson
description: 使用 cookie 而无需 ASP.NET 核心标识的身份验证的说明
manager: wpickett
ms.author: riande
ms.date: 10/11/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/cookie
ms.openlocfilehash: b251aa3ff0b4d0c08f9885cd73a111b7c2008766
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="use-cookie-authentication-without-aspnet-core-identity"></a><span data-ttu-id="3475c-103">使用 cookie 而无需 ASP.NET 核心标识的身份验证</span><span class="sxs-lookup"><span data-stu-id="3475c-103">Use cookie authentication without ASP.NET Core Identity</span></span>

<span data-ttu-id="3475c-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="3475c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="3475c-105">如你所见在早期的身份验证主题中， [ASP.NET 核心标识](xref:security/authentication/identity)完成、 功能完备的身份验证提供程序是用于创建和维护登录名。</span><span class="sxs-lookup"><span data-stu-id="3475c-105">As you've seen in the earlier authentication topics, [ASP.NET Core Identity](xref:security/authentication/identity) is a complete, full-featured authentication provider for creating and maintaining logins.</span></span> <span data-ttu-id="3475c-106">但是，你可能想要使用基于 cookie 的身份验证有时使用您自己的自定义身份验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="3475c-106">However, you may want to use your own custom authentication logic with cookie-based authentication at times.</span></span> <span data-ttu-id="3475c-107">你可以使用基于 cookie 的身份验证作为独立身份验证提供程序，没有 ASP.NET 核心标识。</span><span class="sxs-lookup"><span data-stu-id="3475c-107">You can use cookie-based authentication as a standalone authentication provider without ASP.NET Core Identity.</span></span>

<span data-ttu-id="3475c-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="3475c-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3475c-109">有关从 ASP.NET Core 迁移基于 cookie 的身份验证信息 1.x 到 2.0，请参阅[迁移身份验证和标识到 ASP.NET 核心 2.0 主题 （基于 Cookie 的身份验证）](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication)。</span><span class="sxs-lookup"><span data-stu-id="3475c-109">For information on migrating cookie-based authentication from ASP.NET Core 1.x to 2.0, see [Migrate Authentication and Identity to ASP.NET Core 2.0 topic (Cookie-based Authentication)](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication).</span></span>

## <a name="configuration"></a><span data-ttu-id="3475c-110">配置</span><span class="sxs-lookup"><span data-stu-id="3475c-110">Configuration</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-111">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-111">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
<span data-ttu-id="3475c-112">如果你未使用[Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)，安装 2.0 以上版本的[Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="3475c-112">If you aren't using the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage), install version 2.0+ of the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) NuGet package.</span></span>

<span data-ttu-id="3475c-113">在`ConfigureServices`方法，创建具有的身份验证中间件服务`AddAuthentication`和`AddCookie`方法：</span><span class="sxs-lookup"><span data-stu-id="3475c-113">In the `ConfigureServices` method, create the Authentication Middleware service with the `AddAuthentication` and `AddCookie` methods:</span></span>

[!code-csharp[](cookie/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="3475c-114">`AuthenticationScheme` 传递给`AddAuthentication`设置应用程序的默认身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-114">`AuthenticationScheme` passed to `AddAuthentication` sets the default authentication scheme for the app.</span></span> <span data-ttu-id="3475c-115">`AuthenticationScheme` 当有多个实例的 cookie 身份验证，并且希望时非常有用[授权与特定方案](xref:security/authorization/limitingidentitybyscheme)。</span><span class="sxs-lookup"><span data-stu-id="3475c-115">`AuthenticationScheme` is useful when there are multiple instances of cookie authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="3475c-116">设置`AuthenticationScheme`到`CookieAuthenticationDefaults.AuthenticationScheme`方案提供的"Cookie"的值。</span><span class="sxs-lookup"><span data-stu-id="3475c-116">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="3475c-117">你可以提供任何字符串值，用于区分方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-117">You can supply any string value that distinguishes the scheme.</span></span>

<span data-ttu-id="3475c-118">在`Configure`方法，请使用`UseAuthentication`方法来调用设置身份验证中间件`HttpContext.User`属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-118">In the `Configure` method, use the `UseAuthentication` method to invoke the Authentication Middleware that sets the `HttpContext.User` property.</span></span> <span data-ttu-id="3475c-119">调用`UseAuthentication`方法之前调用`UseMvcWithDefaultRoute`或`UseMvc`:</span><span class="sxs-lookup"><span data-stu-id="3475c-119">Call the `UseAuthentication` method before calling `UseMvcWithDefaultRoute` or `UseMvc`:</span></span>

[!code-csharp[](cookie/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="3475c-120">**AddCookie 选项**</span><span class="sxs-lookup"><span data-stu-id="3475c-120">**AddCookie Options**</span></span>

<span data-ttu-id="3475c-121">[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0)类用于配置身份验证提供程序选项。</span><span class="sxs-lookup"><span data-stu-id="3475c-121">The [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="3475c-122">选项</span><span class="sxs-lookup"><span data-stu-id="3475c-122">Option</span></span> | <span data-ttu-id="3475c-123">描述</span><span class="sxs-lookup"><span data-stu-id="3475c-123">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="3475c-124">AccessDeniedPath</span><span class="sxs-lookup"><span data-stu-id="3475c-124">AccessDeniedPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath?view=aspnetcore-2.0) | <span data-ttu-id="3475c-125">提供的路径以提供 302 找到 （URL 重定向） 时触发的`HttpContext.ForbidAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-125">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ForbidAsync`.</span></span> <span data-ttu-id="3475c-126">默认值为 `/Account/AccessDenied`。</span><span class="sxs-lookup"><span data-stu-id="3475c-126">The default value is `/Account/AccessDenied`.</span></span> |
| [<span data-ttu-id="3475c-127">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="3475c-127">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.claimsissuer?view=aspnetcore-2.0) | <span data-ttu-id="3475c-128">要用于颁发者[颁发者](/dotnet/api/system.security.claims.claim.issuer)cookie 身份验证服务创建的任何声明上的属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-128">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication service.</span></span> |
| [<span data-ttu-id="3475c-129">Cookie.Domain</span><span class="sxs-lookup"><span data-stu-id="3475c-129">Cookie.Domain</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain?view=aspnetcore-2.0) | <span data-ttu-id="3475c-130">Cookie 提供服务位置的域名。</span><span class="sxs-lookup"><span data-stu-id="3475c-130">The domain name where the cookie is served.</span></span> <span data-ttu-id="3475c-131">默认情况下，这是请求的主机名。</span><span class="sxs-lookup"><span data-stu-id="3475c-131">By default, this is the host name of the request.</span></span> <span data-ttu-id="3475c-132">浏览器仅将 cookie 在请求中发送到匹配的主机名。</span><span class="sxs-lookup"><span data-stu-id="3475c-132">The browser only sends the cookie in requests to a matching host name.</span></span> <span data-ttu-id="3475c-133">你可能希望调整这在你的域中具有可用于任何主机的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-133">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="3475c-134">例如，将 cookie 域设置为`.contoso.com`使其可供`contoso.com`， `www.contoso.com`，和`staging.www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="3475c-134">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="3475c-135">Cookie.Expiration</span><span class="sxs-lookup"><span data-stu-id="3475c-135">Cookie.Expiration</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.expiration?view=aspnetcore-2.0) | <span data-ttu-id="3475c-136">获取或设置一个 cookie 的生存期。</span><span class="sxs-lookup"><span data-stu-id="3475c-136">Gets or sets the lifespan of a cookie.</span></span> <span data-ttu-id="3475c-137">目前，此选项没有 ops，并且将会过时中 ASP.NET Core 2.1 +。</span><span class="sxs-lookup"><span data-stu-id="3475c-137">Currently, this option no-ops and will become obsolete in ASP.NET Core 2.1+.</span></span> <span data-ttu-id="3475c-138">使用`ExpireTimeSpan`选项设置 cookie 到期时间。</span><span class="sxs-lookup"><span data-stu-id="3475c-138">Use the `ExpireTimeSpan` option to set cookie expiration.</span></span> <span data-ttu-id="3475c-139">有关详细信息，请参阅[阐明 CookieAuthenticationOptions.Cookie.Expiration 行为](https://github.com/aspnet/Security/issues/1293)。</span><span class="sxs-lookup"><span data-stu-id="3475c-139">For more information, see [Clarify behavior of CookieAuthenticationOptions.Cookie.Expiration](https://github.com/aspnet/Security/issues/1293).</span></span> |
| [<span data-ttu-id="3475c-140">Cookie.HttpOnly</span><span class="sxs-lookup"><span data-stu-id="3475c-140">Cookie.HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly?view=aspnetcore-2.0) | <span data-ttu-id="3475c-141">一个标志，指示该 cookie 应仅服务器访问。</span><span class="sxs-lookup"><span data-stu-id="3475c-141">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="3475c-142">更改此值与`false`允许客户端脚本来访问 cookie 和可能打开你的应用 cookie 被盗应你的应用具备[跨站点脚本 (XSS)](xref:security/cross-site-scripting)漏洞。</span><span class="sxs-lookup"><span data-stu-id="3475c-142">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="3475c-143">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3475c-143">The default value is `true`.</span></span> |
| [<span data-ttu-id="3475c-144">Cookie.Name</span><span class="sxs-lookup"><span data-stu-id="3475c-144">Cookie.Name</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name?view=aspnetcore-2.0) | <span data-ttu-id="3475c-145">设置的 cookie 的名称。</span><span class="sxs-lookup"><span data-stu-id="3475c-145">Sets the name of the cookie.</span></span> |
| [<span data-ttu-id="3475c-146">Cookie.Path</span><span class="sxs-lookup"><span data-stu-id="3475c-146">Cookie.Path</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path?view=aspnetcore-2.0) | <span data-ttu-id="3475c-147">用于隔离在相同的主机名上运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3475c-147">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="3475c-148">如果必须在运行的应用程序`/app1`并且想要限制对该应用的 cookie，请将设置`CookiePath`属性`/app1`。</span><span class="sxs-lookup"><span data-stu-id="3475c-148">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="3475c-149">通过这样做，cookie 是仅可在上找到对请求`/app1`和其下的任何应用程序。</span><span class="sxs-lookup"><span data-stu-id="3475c-149">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="3475c-150">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="3475c-150">Cookie.SameSite</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite?view=aspnetcore-2.0) | <span data-ttu-id="3475c-151">该值指示浏览器应允许 cookie 要附加到同一站点的请求 (`SameSiteMode.Strict`) 或使用安全的 HTTP 方法和同一站点请求的跨站点请求 (`SameSiteMode.Lax`)。</span><span class="sxs-lookup"><span data-stu-id="3475c-151">Indicates whether the browser should allow the cookie to be attached to same-site requests only (`SameSiteMode.Strict`) or cross-site requests using safe HTTP methods and same-site requests (`SameSiteMode.Lax`).</span></span> <span data-ttu-id="3475c-152">当设置为`SameSiteMode.None`，未设置的 cookie 标头值。</span><span class="sxs-lookup"><span data-stu-id="3475c-152">When set to `SameSiteMode.None`, the cookie header value isn't set.</span></span> <span data-ttu-id="3475c-153">请注意， [Cookie 策略中间件](#cookie-policy-middleware)可能会覆盖你提供的值。</span><span class="sxs-lookup"><span data-stu-id="3475c-153">Note that [Cookie Policy Middleware](#cookie-policy-middleware) might overwrite the value that you provide.</span></span> <span data-ttu-id="3475c-154">若要支持 OAuth 身份验证，默认值是`SameSiteMode.Lax`。</span><span class="sxs-lookup"><span data-stu-id="3475c-154">To support OAuth authentication, the default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="3475c-155">有关详细信息，请参阅[OAuth 身份验证由于 SameSite cookie 策略中断](https://github.com/aspnet/Security/issues/1231)。</span><span class="sxs-lookup"><span data-stu-id="3475c-155">For more information, see [OAuth authentication broken due to SameSite cookie policy](https://github.com/aspnet/Security/issues/1231).</span></span> |
| [<span data-ttu-id="3475c-156">Cookie.SecurePolicy</span><span class="sxs-lookup"><span data-stu-id="3475c-156">Cookie.SecurePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.securepolicy?view=aspnetcore-2.0) | <span data-ttu-id="3475c-157">一个标志，指示是否创建的 cookie 应被限制为 HTTPS (`CookieSecurePolicy.Always`)，HTTP 或 HTTPS (`CookieSecurePolicy.None`)，或请求的同一个协议 (`CookieSecurePolicy.SameAsRequest`)。</span><span class="sxs-lookup"><span data-stu-id="3475c-157">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="3475c-158">默认值为 `CookieSecurePolicy.SameAsRequest`。</span><span class="sxs-lookup"><span data-stu-id="3475c-158">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="3475c-159">DataProtectionProvider</span><span class="sxs-lookup"><span data-stu-id="3475c-159">DataProtectionProvider</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0) | <span data-ttu-id="3475c-160">集`DataProtectionProvider`用于创建默认值`TicketDataFormat`。</span><span class="sxs-lookup"><span data-stu-id="3475c-160">Sets the `DataProtectionProvider` that's used to create the default `TicketDataFormat`.</span></span> <span data-ttu-id="3475c-161">如果`TicketDataFormat`设置属性，`DataProtectionProvider`选项未使用。</span><span class="sxs-lookup"><span data-stu-id="3475c-161">If the `TicketDataFormat` property is set, the `DataProtectionProvider` option isn't used.</span></span> <span data-ttu-id="3475c-162">如果未提供，则使用应用程序的默认数据保护提供程序。</span><span class="sxs-lookup"><span data-stu-id="3475c-162">If not provided, the app's default data protection provider is used.</span></span> |
| [<span data-ttu-id="3475c-163">事件</span><span class="sxs-lookup"><span data-stu-id="3475c-163">Events</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.events?view=aspnetcore-2.0) | <span data-ttu-id="3475c-164">该处理程序在处理中的某些点提供的应用程序控制的提供程序上调用方法。</span><span class="sxs-lookup"><span data-stu-id="3475c-164">The handler calls methods on the provider that give the app control at certain processing points.</span></span> <span data-ttu-id="3475c-165">如果`Events`不提供的默认实例提供的方法在调用时不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="3475c-165">If `Events` aren't provided, a default instance is supplied that does nothing when the methods are called.</span></span> |
| [<span data-ttu-id="3475c-166">EventsType</span><span class="sxs-lookup"><span data-stu-id="3475c-166">EventsType</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.eventstype?view=aspnetcore-2.0) | <span data-ttu-id="3475c-167">用作服务类型，以获取`Events`实例而不是属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-167">Used as the service type to get the `Events` instance instead of the property.</span></span> |
| [<span data-ttu-id="3475c-168">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="3475c-168">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan?view=aspnetcore-2.0) | <span data-ttu-id="3475c-169">`TimeSpan`后将存储在 cookie 的身份验证票证到期。</span><span class="sxs-lookup"><span data-stu-id="3475c-169">The `TimeSpan` after which the authentication ticket stored inside the cookie expires.</span></span> <span data-ttu-id="3475c-170">`ExpireTimeSpan` 将添加到当前时间来创建票证的到期时间。</span><span class="sxs-lookup"><span data-stu-id="3475c-170">`ExpireTimeSpan` is added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="3475c-171">`ExpiredTimeSpan`值始终将验证由服务器加密 AuthTicket 进入。</span><span class="sxs-lookup"><span data-stu-id="3475c-171">The `ExpiredTimeSpan` value always goes into the encrypted AuthTicket verified by the server.</span></span> <span data-ttu-id="3475c-172">它可能还进入[Set-cookie](https://tools.ietf.org/html/rfc6265#section-4.1)标头，但仅当`IsPersistent`设置。</span><span class="sxs-lookup"><span data-stu-id="3475c-172">It may also go into the [Set-Cookie](https://tools.ietf.org/html/rfc6265#section-4.1) header, but only if `IsPersistent` is set.</span></span> <span data-ttu-id="3475c-173">若要设置`IsPersistent`到`true`，配置[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties)传递给`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-173">To set `IsPersistent` to `true`, configure the [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties) passed to `SignInAsync`.</span></span> <span data-ttu-id="3475c-174">默认值`ExpireTimeSpan`为 14 天。</span><span class="sxs-lookup"><span data-stu-id="3475c-174">The default value of `ExpireTimeSpan` is 14 days.</span></span> |
| [<span data-ttu-id="3475c-175">LoginPath</span><span class="sxs-lookup"><span data-stu-id="3475c-175">LoginPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath?view=aspnetcore-2.0) | <span data-ttu-id="3475c-176">提供的路径以提供 302 找到 （URL 重定向） 时触发的`HttpContext.ChallengeAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-176">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ChallengeAsync`.</span></span> <span data-ttu-id="3475c-177">当前生成 401 的 URL 添加到`LoginPath`作为查询字符串参数由名为`ReturnUrlParameter`。</span><span class="sxs-lookup"><span data-stu-id="3475c-177">The current URL that generated the 401 is added to the `LoginPath` as a query string parameter named by the `ReturnUrlParameter`.</span></span> <span data-ttu-id="3475c-178">一次请求`LoginPath`授予新登录标识，`ReturnUrlParameter`值用于将浏览器重定向回导致原始的未授权的状态代码的 URL。</span><span class="sxs-lookup"><span data-stu-id="3475c-178">Once a request to the `LoginPath` grants a new sign-in identity, the `ReturnUrlParameter` value is used to redirect the browser back to the URL that caused the original unauthorized status code.</span></span> <span data-ttu-id="3475c-179">默认值为 `/Account/Login`。</span><span class="sxs-lookup"><span data-stu-id="3475c-179">The default value is `/Account/Login`.</span></span> |
| [<span data-ttu-id="3475c-180">LogoutPath</span><span class="sxs-lookup"><span data-stu-id="3475c-180">LogoutPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath?view=aspnetcore-2.0) | <span data-ttu-id="3475c-181">如果`LogoutPath`然后对该路径的请求重定向到处理程序，提供的值基于`ReturnUrlParameter`。</span><span class="sxs-lookup"><span data-stu-id="3475c-181">If the `LogoutPath` is provided to the handler, then a request to that path redirects based on the value of the `ReturnUrlParameter`.</span></span> <span data-ttu-id="3475c-182">默认值为 `/Account/Logout`。</span><span class="sxs-lookup"><span data-stu-id="3475c-182">The default value is `/Account/Logout`.</span></span> |
| [<span data-ttu-id="3475c-183">ReturnUrlParameter</span><span class="sxs-lookup"><span data-stu-id="3475c-183">ReturnUrlParameter</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.returnurlparameter?view=aspnetcore-2.0) | <span data-ttu-id="3475c-184">确定追加通过处理程序 302 找到 （URL 重定向） 响应的查询字符串参数的名称。</span><span class="sxs-lookup"><span data-stu-id="3475c-184">Determines the name of the query string parameter that's appended by the handler for a 302 Found (URL redirect) response.</span></span> <span data-ttu-id="3475c-185">`ReturnUrlParameter` 请求到达时，将使用`LoginPath`或`LogoutPath`以返回到原始的 URL 的浏览器之后执行的登录或注销操作。</span><span class="sxs-lookup"><span data-stu-id="3475c-185">`ReturnUrlParameter` is used when a request arrives on the `LoginPath` or `LogoutPath` to return the browser to the original URL after the login or logout action is performed.</span></span> <span data-ttu-id="3475c-186">默认值为 `ReturnUrl`。</span><span class="sxs-lookup"><span data-stu-id="3475c-186">The default value is `ReturnUrl`.</span></span> |
| [<span data-ttu-id="3475c-187">SessionStore</span><span class="sxs-lookup"><span data-stu-id="3475c-187">SessionStore</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.sessionstore?view=aspnetcore-2.0) | <span data-ttu-id="3475c-188">用来存储标识跨请求可选容器。</span><span class="sxs-lookup"><span data-stu-id="3475c-188">An optional container used to store identity across requests.</span></span> <span data-ttu-id="3475c-189">使用时，仅一个会话标识符是发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="3475c-189">When used, only a session identifier is sent to the client.</span></span> <span data-ttu-id="3475c-190">`SessionStore` 可以用于缓解的大型标识潜在问题。</span><span class="sxs-lookup"><span data-stu-id="3475c-190">`SessionStore` can be used to mitigate potential problems with large identities.</span></span> |
| [<span data-ttu-id="3475c-191">SlidingExpiration</span><span class="sxs-lookup"><span data-stu-id="3475c-191">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-2.0) | <span data-ttu-id="3475c-192">应动态发出一个标志，指示如果具有更新的到期时间的新 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-192">A flag indicating if a new cookie with an updated expiration time should be issued dynamically.</span></span> <span data-ttu-id="3475c-193">这可能发生在当前的 cookie 过期时间已超过 50%过期任何请求。</span><span class="sxs-lookup"><span data-stu-id="3475c-193">This can happen on any request where the current cookie expiration period is more than 50% expired.</span></span> <span data-ttu-id="3475c-194">向前移动新的到期日期为当前日期加上`ExpireTimespan`。</span><span class="sxs-lookup"><span data-stu-id="3475c-194">The new expiration date is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="3475c-195">[绝对 cookie 到期时间](xref:security/authentication/cookie#absolute-cookie-expiration)可以通过使用设置`AuthenticationProperties`类调用时`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-195">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="3475c-196">绝对到期时间可通过限制的身份验证 cookie 是有效的时间量来提高您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="3475c-196">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="3475c-197">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3475c-197">The default value is `true`.</span></span> |
| [<span data-ttu-id="3475c-198">TicketDataFormat</span><span class="sxs-lookup"><span data-stu-id="3475c-198">TicketDataFormat</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.ticketdataformat?view=aspnetcore-2.0) | <span data-ttu-id="3475c-199">`TicketDataFormat`用于保护和取消保护的标识以及存储在 cookie 值中的其他属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-199">The `TicketDataFormat` is used to protect and unprotect the identity and other properties that are stored in the cookie value.</span></span> <span data-ttu-id="3475c-200">如果未提供，`TicketDataFormat`使用创建[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0)。</span><span class="sxs-lookup"><span data-stu-id="3475c-200">If not provided, a `TicketDataFormat` is created using the [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0).</span></span> |
| [<span data-ttu-id="3475c-201">验证</span><span class="sxs-lookup"><span data-stu-id="3475c-201">Validate</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.validate?view=aspnetcore-2.0) | <span data-ttu-id="3475c-202">检查的选项为有效的方法。</span><span class="sxs-lookup"><span data-stu-id="3475c-202">Method that checks that the options are valid.</span></span> |

<span data-ttu-id="3475c-203">设置`CookieAuthenticationOptions`中的身份验证的服务配置中`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="3475c-203">Set `CookieAuthenticationOptions` in the service configuration for authentication in the `ConfigureServices` method:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        ...
    });
```

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-204">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-204">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
<span data-ttu-id="3475c-205">ASP.NET 核心 1.x 使用 cookie[中间件](xref:fundamentals/middleware/index)，序列化为一个用户主体的加密 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-205">ASP.NET Core 1.x uses cookie [middleware](xref:fundamentals/middleware/index) that serializes a user principal into an encrypted cookie.</span></span> <span data-ttu-id="3475c-206">在后续请求中，验证 cookie，并重新创建主体并将其分配到`HttpContext.User`属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-206">On subsequent requests, the cookie is validated, and the principal is recreated and assigned to the `HttpContext.User` property.</span></span>

<span data-ttu-id="3475c-207">安装[Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/)项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="3475c-207">Install the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) NuGet package in your project.</span></span> <span data-ttu-id="3475c-208">此程序包包含 cookie 中间件。</span><span class="sxs-lookup"><span data-stu-id="3475c-208">This package contains the cookie middleware.</span></span>

<span data-ttu-id="3475c-209">使用`UseCookieAuthentication`中的方法`Configure`方法在你*Startup.cs*文件，然后`UseMvc`或`UseMvcWithDefaultRoute`:</span><span class="sxs-lookup"><span data-stu-id="3475c-209">Use the `UseCookieAuthentication` method in the `Configure` method in your *Startup.cs* file before `UseMvc` or `UseMvcWithDefaultRoute`:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions()
{
    AccessDeniedPath = "/Account/Forbidden/",
    AuthenticationScheme = CookieAuthenticationDefaults.AuthenticationScheme,
    AutomaticAuthenticate = true,
    AutomaticChallenge = true,
    LoginPath = "/Account/Unauthorized/"
});
```

<span data-ttu-id="3475c-210">**CookieAuthenticationOptions 选项**</span><span class="sxs-lookup"><span data-stu-id="3475c-210">**CookieAuthenticationOptions Options**</span></span>

<span data-ttu-id="3475c-211">[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1)类用于配置身份验证提供程序选项。</span><span class="sxs-lookup"><span data-stu-id="3475c-211">The [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="3475c-212">选项</span><span class="sxs-lookup"><span data-stu-id="3475c-212">Option</span></span> | <span data-ttu-id="3475c-213">描述</span><span class="sxs-lookup"><span data-stu-id="3475c-213">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="3475c-214">AuthenticationScheme</span><span class="sxs-lookup"><span data-stu-id="3475c-214">AuthenticationScheme</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.authenticationscheme?view=aspnetcore-1.1) | <span data-ttu-id="3475c-215">设置身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-215">Sets the authentication scheme.</span></span> <span data-ttu-id="3475c-216">`AuthenticationScheme` 当有多个实例的身份验证，并且希望时非常有用[授权与特定方案](xref:security/authorization/limitingidentitybyscheme)。</span><span class="sxs-lookup"><span data-stu-id="3475c-216">`AuthenticationScheme` is useful when there are multiple instances of authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="3475c-217">设置`AuthenticationScheme`到`CookieAuthenticationDefaults.AuthenticationScheme`方案提供的"Cookie"的值。</span><span class="sxs-lookup"><span data-stu-id="3475c-217">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="3475c-218">你可以提供任何字符串值，用于区分方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-218">You can supply any string value that distinguishes the scheme.</span></span> |
| [<span data-ttu-id="3475c-219">AutomaticAuthenticate</span><span class="sxs-lookup"><span data-stu-id="3475c-219">AutomaticAuthenticate</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticauthenticate?view=aspnetcore-1.1) | <span data-ttu-id="3475c-220">设置一个值以指示应在每个请求上运行并且尝试验证并重新构造它创建的任何序列化的主体 cookie 身份验证。</span><span class="sxs-lookup"><span data-stu-id="3475c-220">Sets a value to indicate that the cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span> |
| [<span data-ttu-id="3475c-221">AutomaticChallenge</span><span class="sxs-lookup"><span data-stu-id="3475c-221">AutomaticChallenge</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticchallenge?view=aspnetcore-1.1) | <span data-ttu-id="3475c-222">如果为 true，则身份验证中间件处理自动挑战。</span><span class="sxs-lookup"><span data-stu-id="3475c-222">If true, the authentication middleware handles automatic challenges.</span></span> <span data-ttu-id="3475c-223">如果为 false，身份验证中间件仅更改响应时显式由`AuthenticationScheme`。</span><span class="sxs-lookup"><span data-stu-id="3475c-223">If false, the authentication middleware only alters responses when explicitly indicated by the `AuthenticationScheme`.</span></span> |
| [<span data-ttu-id="3475c-224">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="3475c-224">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.claimsissuer?view=aspnetcore-1.1) | <span data-ttu-id="3475c-225">要用于颁发者[颁发者](/dotnet/api/system.security.claims.claim.issuer)创建 cookie 身份验证中间件的任何声明上的属性。</span><span class="sxs-lookup"><span data-stu-id="3475c-225">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication middleware.</span></span> |
| [<span data-ttu-id="3475c-226">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="3475c-226">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiedomain?view=aspnetcore-1.1) | <span data-ttu-id="3475c-227">Cookie 提供服务位置的域名。</span><span class="sxs-lookup"><span data-stu-id="3475c-227">The domain name where the cookie is served.</span></span> <span data-ttu-id="3475c-228">默认情况下，这是请求的主机名。</span><span class="sxs-lookup"><span data-stu-id="3475c-228">By default, this is the host name of the request.</span></span> <span data-ttu-id="3475c-229">浏览器只为服务为匹配的主机名称的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-229">The browser only serves the cookie to a matching host name.</span></span> <span data-ttu-id="3475c-230">你可能希望调整这在你的域中具有可用于任何主机的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-230">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="3475c-231">例如，将 cookie 域设置为`.contoso.com`使其可供`contoso.com`， `www.contoso.com`，和`staging.www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="3475c-231">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="3475c-232">CookieHttpOnly</span><span class="sxs-lookup"><span data-stu-id="3475c-232">CookieHttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiehttponly?view=aspnetcore-1.1) | <span data-ttu-id="3475c-233">一个标志，指示该 cookie 应仅服务器访问。</span><span class="sxs-lookup"><span data-stu-id="3475c-233">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="3475c-234">更改此值与`false`允许客户端脚本来访问 cookie 和可能打开你的应用 cookie 被盗应你的应用具备[跨站点脚本 (XSS)](xref:security/cross-site-scripting)漏洞。</span><span class="sxs-lookup"><span data-stu-id="3475c-234">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="3475c-235">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3475c-235">The default value is `true`.</span></span> |
| [<span data-ttu-id="3475c-236">CookiePath</span><span class="sxs-lookup"><span data-stu-id="3475c-236">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiepath?view=aspnetcore-1.1) | <span data-ttu-id="3475c-237">用于隔离在相同的主机名上运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3475c-237">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="3475c-238">如果必须在运行的应用程序`/app1`并且想要限制对该应用的 cookie，请将设置`CookiePath`属性`/app1`。</span><span class="sxs-lookup"><span data-stu-id="3475c-238">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="3475c-239">通过这样做，cookie 是仅可在上找到对请求`/app1`和其下的任何应用程序。</span><span class="sxs-lookup"><span data-stu-id="3475c-239">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="3475c-240">CookieSecure</span><span class="sxs-lookup"><span data-stu-id="3475c-240">CookieSecure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiesecure?view=aspnetcore-1.1) | <span data-ttu-id="3475c-241">一个标志，指示是否创建的 cookie 应被限制为 HTTPS (`CookieSecurePolicy.Always`)，HTTP 或 HTTPS (`CookieSecurePolicy.None`)，或请求的同一个协议 (`CookieSecurePolicy.SameAsRequest`)。</span><span class="sxs-lookup"><span data-stu-id="3475c-241">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="3475c-242">默认值为 `CookieSecurePolicy.SameAsRequest`。</span><span class="sxs-lookup"><span data-stu-id="3475c-242">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="3475c-243">说明</span><span class="sxs-lookup"><span data-stu-id="3475c-243">Description</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.description?view=aspnetcore-1.1) | <span data-ttu-id="3475c-244">有关提供给应用程序的身份验证类型的其他信息。</span><span class="sxs-lookup"><span data-stu-id="3475c-244">Additional information about the authentication type which is made available to the app.</span></span> |
| [<span data-ttu-id="3475c-245">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="3475c-245">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.expiretimespan?view=aspnetcore-1.1) | <span data-ttu-id="3475c-246">`TimeSpan`直到身份验证票证到期。</span><span class="sxs-lookup"><span data-stu-id="3475c-246">The `TimeSpan` after which the authentication ticket expires.</span></span> <span data-ttu-id="3475c-247">它添加到当前时间来创建票证的到期时间。</span><span class="sxs-lookup"><span data-stu-id="3475c-247">It's added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="3475c-248">若要使用`ExpireTimeSpan`，必须设置`IsPersistent`到`true`中`AuthenticationProperties`传递给`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-248">To use `ExpireTimeSpan`, you must set `IsPersistent` to `true` in the `AuthenticationProperties` passed to `SignInAsync`.</span></span> <span data-ttu-id="3475c-249">默认值为 14 天。</span><span class="sxs-lookup"><span data-stu-id="3475c-249">The default value is 14 days.</span></span> |
| [<span data-ttu-id="3475c-250">SlidingExpiration</span><span class="sxs-lookup"><span data-stu-id="3475c-250">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-1.1) | <span data-ttu-id="3475c-251">一个标志，指示是否重置时超过一半的 cookie 的到期日期`ExpireTimeSpan`时间间隔。</span><span class="sxs-lookup"><span data-stu-id="3475c-251">A flag indicating whether the cookie expiration date resets when more than half of the `ExpireTimeSpan` interval has passed.</span></span> <span data-ttu-id="3475c-252">新的 exipiration 时间向前移动，为当前日期加上`ExpireTimespan`。</span><span class="sxs-lookup"><span data-stu-id="3475c-252">The new exipiration time is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="3475c-253">[绝对 cookie 到期时间](xref:security/authentication/cookie#absolute-cookie-expiration)可以通过使用设置`AuthenticationProperties`类调用时`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="3475c-253">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="3475c-254">绝对到期时间可通过限制的身份验证 cookie 是有效的时间量来提高您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="3475c-254">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="3475c-255">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="3475c-255">The default value is `true`.</span></span> |

<span data-ttu-id="3475c-256">设置`CookieAuthenticationOptions`为在 Cookie 身份验证中间件`Configure`方法：</span><span class="sxs-lookup"><span data-stu-id="3475c-256">Set `CookieAuthenticationOptions` for the Cookie Authentication Middleware in the `Configure` method:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    ...
});
```

* * *
## <a name="cookie-policy-middleware"></a><span data-ttu-id="3475c-257">Cookie 策略中间件</span><span class="sxs-lookup"><span data-stu-id="3475c-257">Cookie Policy Middleware</span></span>

<span data-ttu-id="3475c-258">[Cookie 策略中间件](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware)启用应用程序中的 cookie 策略功能。</span><span class="sxs-lookup"><span data-stu-id="3475c-258">[Cookie Policy Middleware](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware) enables cookie policy capabilities in an app.</span></span> <span data-ttu-id="3475c-259">将该中间件添加到应用程序处理管道是顺序敏感;它只影响在管道中后它注册的组件。</span><span class="sxs-lookup"><span data-stu-id="3475c-259">Adding the middleware to the app processing pipeline is order sensitive; it only affects components registered after it in the pipeline.</span></span>

```csharp
app.UseCookiePolicy(cookiePolicyOptions);
```

 <span data-ttu-id="3475c-260">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions)到 Cookie 策略中间件提供可用于控制到 cookie 处理处理程序的 cookie 处理和挂钩全局特性，在追加或删除 cookie 的时间。</span><span class="sxs-lookup"><span data-stu-id="3475c-260">The [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) provided to the Cookie Policy Middleware allow you to control global characteristics of cookie processing and hook into cookie processing handlers when cookies are appended or deleted.</span></span>

| <span data-ttu-id="3475c-261">属性</span><span class="sxs-lookup"><span data-stu-id="3475c-261">Property</span></span> | <span data-ttu-id="3475c-262">描述</span><span class="sxs-lookup"><span data-stu-id="3475c-262">Description</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="3475c-263">HttpOnly</span><span class="sxs-lookup"><span data-stu-id="3475c-263">HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.httponly) | <span data-ttu-id="3475c-264">会影响是否必须为 cookie HttpOnly，该值一个标志，指示是否 cookie 应只允许到服务器可访问。</span><span class="sxs-lookup"><span data-stu-id="3475c-264">Affects whether cookies must be HttpOnly, which is a flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="3475c-265">默认值为 `HttpOnlyPolicy.None`。</span><span class="sxs-lookup"><span data-stu-id="3475c-265">The default value is `HttpOnlyPolicy.None`.</span></span> |
| [<span data-ttu-id="3475c-266">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="3475c-266">MinimumSameSitePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.minimumsamesitepolicy) | <span data-ttu-id="3475c-267">影响 cookie 的同一站点属性 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="3475c-267">Affects the cookie's same-site attribute (see below).</span></span> <span data-ttu-id="3475c-268">默认值为 `SameSiteMode.Lax`。</span><span class="sxs-lookup"><span data-stu-id="3475c-268">The default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="3475c-269">此选项仅供 ASP.NET Core 2.0 +。</span><span class="sxs-lookup"><span data-stu-id="3475c-269">This option is available for ASP.NET Core 2.0+.</span></span> |
| [<span data-ttu-id="3475c-270">OnAppendCookie</span><span class="sxs-lookup"><span data-stu-id="3475c-270">OnAppendCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.onappendcookie) | <span data-ttu-id="3475c-271">当追加 cookie 时调用。</span><span class="sxs-lookup"><span data-stu-id="3475c-271">Called when a cookie is appended.</span></span> |
| [<span data-ttu-id="3475c-272">OnDeleteCookie</span><span class="sxs-lookup"><span data-stu-id="3475c-272">OnDeleteCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.ondeletecookie) | <span data-ttu-id="3475c-273">当删除 cookie 时调用。</span><span class="sxs-lookup"><span data-stu-id="3475c-273">Called when a cookie is deleted.</span></span> |
| [<span data-ttu-id="3475c-274">安全</span><span class="sxs-lookup"><span data-stu-id="3475c-274">Secure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.secure) | <span data-ttu-id="3475c-275">会影响是否必须安全 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-275">Affects whether cookies must be Secure.</span></span> <span data-ttu-id="3475c-276">默认值为 `CookieSecurePolicy.None`。</span><span class="sxs-lookup"><span data-stu-id="3475c-276">The default value is `CookieSecurePolicy.None`.</span></span> |

<span data-ttu-id="3475c-277">**MinimumSameSitePolicy** （ASP.NET 2.0 + 仅内核）</span><span class="sxs-lookup"><span data-stu-id="3475c-277">**MinimumSameSitePolicy** (ASP.NET Core 2.0+ only)</span></span>

<span data-ttu-id="3475c-278">默认值`MinimumSameSitePolicy`值是`SameSiteMode.Lax`允许 OAuth2 身份验证。</span><span class="sxs-lookup"><span data-stu-id="3475c-278">The default `MinimumSameSitePolicy` value is `SameSiteMode.Lax` to permit OAuth2 authentication.</span></span> <span data-ttu-id="3475c-279">若要严格强制执行的同一站点策略`SameSiteMode.Strict`，将其设置`MinimumSameSitePolicy`。</span><span class="sxs-lookup"><span data-stu-id="3475c-279">To strictly enforce a same-site policy of `SameSiteMode.Strict`, set the `MinimumSameSitePolicy`.</span></span> <span data-ttu-id="3475c-280">虽然此设置将中断 OAuth2 和其他跨域身份验证方案，它将提升其他类型的应用程序不依赖于跨域请求处理的 cookie 安全的级别。</span><span class="sxs-lookup"><span data-stu-id="3475c-280">Although this setting breaks OAuth2 and other cross-origin authentication schemes, it elevates the level of cookie security for other types of apps that don't rely on cross-origin request processing.</span></span>

```csharp
var cookiePolicyOptions = new CookiePolicyOptions
{
    MinimumSameSitePolicy = SameSiteMode.Strict,
};
```

<span data-ttu-id="3475c-281">Cookie 策略中间件设置`MinimumSameSitePolicy`可能会影响你的设置的`Cookie.SameSite`中`CookieAuthenticationOptions`根据下面的矩阵的设置。</span><span class="sxs-lookup"><span data-stu-id="3475c-281">The Cookie Policy Middleware setting for `MinimumSameSitePolicy` can affect your setting of `Cookie.SameSite` in `CookieAuthenticationOptions` settings according to the matrix below.</span></span>

| <span data-ttu-id="3475c-282">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="3475c-282">MinimumSameSitePolicy</span></span> | <span data-ttu-id="3475c-283">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="3475c-283">Cookie.SameSite</span></span> | <span data-ttu-id="3475c-284">最终的 Cookie.SameSite 设置</span><span class="sxs-lookup"><span data-stu-id="3475c-284">Resultant Cookie.SameSite setting</span></span> |
| --------------------- | --------------- | --------------------------------- |
| <span data-ttu-id="3475c-285">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="3475c-285">SameSiteMode.None</span></span>     | <span data-ttu-id="3475c-286">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="3475c-286">SameSiteMode.None</span></span><br><span data-ttu-id="3475c-287">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-287">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-288">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-288">SameSiteMode.Strict</span></span> | <span data-ttu-id="3475c-289">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="3475c-289">SameSiteMode.None</span></span><br><span data-ttu-id="3475c-290">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-290">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-291">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-291">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="3475c-292">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-292">SameSiteMode.Lax</span></span>      | <span data-ttu-id="3475c-293">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="3475c-293">SameSiteMode.None</span></span><br><span data-ttu-id="3475c-294">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-294">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-295">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-295">SameSiteMode.Strict</span></span> | <span data-ttu-id="3475c-296">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-296">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-297">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-297">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-298">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-298">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="3475c-299">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-299">SameSiteMode.Strict</span></span>   | <span data-ttu-id="3475c-300">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="3475c-300">SameSiteMode.None</span></span><br><span data-ttu-id="3475c-301">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="3475c-301">SameSiteMode.Lax</span></span><br><span data-ttu-id="3475c-302">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-302">SameSiteMode.Strict</span></span> | <span data-ttu-id="3475c-303">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-303">SameSiteMode.Strict</span></span><br><span data-ttu-id="3475c-304">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-304">SameSiteMode.Strict</span></span><br><span data-ttu-id="3475c-305">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="3475c-305">SameSiteMode.Strict</span></span> |

## <a name="creating-an-authentication-cookie"></a><span data-ttu-id="3475c-306">创建身份验证 cookie</span><span class="sxs-lookup"><span data-stu-id="3475c-306">Creating an authentication cookie</span></span>

<span data-ttu-id="3475c-307">若要创建一个保存用户信息的 cookie，您必须先构造[ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal)。</span><span class="sxs-lookup"><span data-stu-id="3475c-307">To create a cookie holding user information, you must construct a [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal).</span></span> <span data-ttu-id="3475c-308">序列化用户信息并将其存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="3475c-308">The user information is serialized and stored in the cookie.</span></span> 

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-309">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-309">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
<span data-ttu-id="3475c-310">创建[ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity)与任何所需[声明](/dotnet/api/system.security.claims.claim)s 并调用[SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0)若要在用户登录：</span><span class="sxs-lookup"><span data-stu-id="3475c-310">Create a [ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity) with any required [Claim](/dotnet/api/system.security.claims.claim)s and call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0) to sign in the user:</span></span>

[!code-csharp[](cookie/sample/Pages/Account/Login.cshtml.cs?name=snippet1)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-311">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-311">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
<span data-ttu-id="3475c-312">调用[SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1)若要在用户登录：</span><span class="sxs-lookup"><span data-stu-id="3475c-312">Call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1) to sign in the user:</span></span>

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity));
```

* * *
<span data-ttu-id="3475c-313">`SignInAsync` 创建一个加密的 cookie，并将其添加到当前响应。</span><span class="sxs-lookup"><span data-stu-id="3475c-313">`SignInAsync` creates an encrypted cookie and adds it to the current response.</span></span> <span data-ttu-id="3475c-314">如果没有指定`AuthenticationScheme`，则使用默认方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-314">If you don't specify an `AuthenticationScheme`, the default scheme is used.</span></span>

<span data-ttu-id="3475c-315">事实上，使用的加密是 ASP.NET Core[数据保护](xref:security/data-protection/using-data-protection#security-data-protection-getting-started)系统。</span><span class="sxs-lookup"><span data-stu-id="3475c-315">Under the covers, the encryption used is ASP.NET Core's [Data Protection](xref:security/data-protection/using-data-protection#security-data-protection-getting-started) system.</span></span> <span data-ttu-id="3475c-316">如果您正在承载应用程序在多台计算机、 负载平衡应用程序，或使用 web 场，则必须[配置数据保护](xref:security/data-protection/configuration/overview)使用同一密钥链和应用程序标识符。</span><span class="sxs-lookup"><span data-stu-id="3475c-316">If you're hosting app on multiple machines, load balancing across apps, or using a web farm, then you must [configure data protection](xref:security/data-protection/configuration/overview) to use the same key ring and app identifier.</span></span>

## <a name="signing-out"></a><span data-ttu-id="3475c-317">注销</span><span class="sxs-lookup"><span data-stu-id="3475c-317">Signing out</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-318">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-318">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
<span data-ttu-id="3475c-319">若要注销当前用户，并删除其 cookie，调用[SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span><span class="sxs-lookup"><span data-stu-id="3475c-319">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span></span>

[!code-csharp[](cookie/sample/Pages/Account/Login.cshtml.cs?name=snippet2)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-320">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-320">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
<span data-ttu-id="3475c-321">若要注销当前用户，并删除其 cookie，调用[SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span><span class="sxs-lookup"><span data-stu-id="3475c-321">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span></span>

```csharp
await HttpContext.Authentication.SignOutAsync(
    CookieAuthenticationDefaults.AuthenticationScheme);
```

* * *
<span data-ttu-id="3475c-322">如果你未使用`CookieAuthenticationDefaults.AuthenticationScheme`（或"Cookie"） 的方案 (例如，"ContosoCookie")，提供你在配置身份验证提供程序时使用的方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-322">If you aren't using `CookieAuthenticationDefaults.AuthenticationScheme` (or "Cookies") as the scheme (for example, "ContosoCookie"), supply the scheme you used when configuring the authentication provider.</span></span> <span data-ttu-id="3475c-323">否则，使用的默认方案。</span><span class="sxs-lookup"><span data-stu-id="3475c-323">Otherwise, the default scheme is used.</span></span>

## <a name="reacting-to-back-end-changes"></a><span data-ttu-id="3475c-324">对后端更改的作出反应</span><span class="sxs-lookup"><span data-stu-id="3475c-324">Reacting to back-end changes</span></span>

<span data-ttu-id="3475c-325">一旦创建 cookie，它将成为标识的单个来源。</span><span class="sxs-lookup"><span data-stu-id="3475c-325">Once a cookie is created, it becomes the single source of identity.</span></span> <span data-ttu-id="3475c-326">即使在后端系统中禁用用户，cookie 身份验证系统不了解，并且用户一直保持登录，只要其 cookie 的有效期。</span><span class="sxs-lookup"><span data-stu-id="3475c-326">Even if you disable a user in your back-end systems, the cookie authentication system has no knowledge of this, and a user stays logged in as long as their cookie is valid.</span></span>

<span data-ttu-id="3475c-327">[ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal)中 ASP.NET 核心事件 2.x 或[ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1)中 ASP.NET Core 1.x 可用来截获和重写的 cookie 身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="3475c-327">The [ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal) event in ASP.NET Core 2.x or the [ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1) method in ASP.NET Core 1.x can be used to intercept and override validation of the cookie identity.</span></span> <span data-ttu-id="3475c-328">这种方法可以降低吊销用户访问应用程序的风险。</span><span class="sxs-lookup"><span data-stu-id="3475c-328">This approach mitigates the risk of revoked users accessing the app.</span></span>

<span data-ttu-id="3475c-329">Cookie 验证的一种方法取决于跟踪的用户数据库已更改时。</span><span class="sxs-lookup"><span data-stu-id="3475c-329">One approach to cookie validation is based on keeping track of when the user database has been changed.</span></span> <span data-ttu-id="3475c-330">如果颁发用户的 cookie 以来，数据库没有被更改，，则无需重新进行用户身份验证其 cookie 是否仍有效。</span><span class="sxs-lookup"><span data-stu-id="3475c-330">If the database hasn't been changed since the user's cookie was issued, there's no need to re-authenticate the user if their cookie is still valid.</span></span> <span data-ttu-id="3475c-331">若要实现此方案中，数据库中实现`IUserRepository`对于此示例中，存储`LastChanged`值。</span><span class="sxs-lookup"><span data-stu-id="3475c-331">To implement this scenario, the database, which is implemented in `IUserRepository` for this example, stores a `LastChanged` value.</span></span> <span data-ttu-id="3475c-332">在数据库中，更新的任何用户时`LastChanged`值设置为当前时间。</span><span class="sxs-lookup"><span data-stu-id="3475c-332">When any user is updated in the database, the `LastChanged` value is set to the current time.</span></span>

<span data-ttu-id="3475c-333">为了使 cookie 无效时的数据库更改基于`LastChanged`值时，请创建具有 cookie`LastChanged`声明包含当前`LastChanged`从数据库的值：</span><span class="sxs-lookup"><span data-stu-id="3475c-333">In order to invalidate a cookie when the database changes based on the `LastChanged` value, create the cookie with a `LastChanged` claim containing the current `LastChanged` value from the database:</span></span>

```csharp
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, user.Email),
    new Claim("LastChanged", {Database Value})
};

var claimsIdentity = new ClaimsIdentity(
    claims, 
    CookieAuthenticationDefaults.AuthenticationScheme);

await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme, 
    new ClaimsPrincipal(claimsIdentity));
```

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-334">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-334">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3475c-335">若要实现的替代`ValidatePrincipal`事件，带有以下签名的类中派生自方法写入[CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span><span class="sxs-lookup"><span data-stu-id="3475c-335">To implement an override for the `ValidatePrincipal` event, write a method with the following signature in a class that you derive from [CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span></span>

```csharp
ValidatePrincipal(CookieValidatePrincipalContext)
```

<span data-ttu-id="3475c-336">示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="3475c-336">An example looks like the following:</span></span>

```csharp
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Authentication;
using Microsoft.AspNetCore.Authentication.Cookies;

public class CustomCookieAuthenticationEvents : CookieAuthenticationEvents
{
    private readonly IUserRepository _userRepository;

    public CustomCookieAuthenticationEvents(IUserRepository userRepository)
    {
        // Get the database from registered DI services.
        _userRepository = userRepository;
    }

    public override async Task ValidatePrincipal(CookieValidatePrincipalContext context)
    {
        var userPrincipal = context.Principal;

        // Look for the LastChanged claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !_userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

<span data-ttu-id="3475c-337">在中的 cookie 服务注册期间注册的事件实例`ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="3475c-337">Register the events instance during cookie service registration in the `ConfigureServices` method.</span></span> <span data-ttu-id="3475c-338">提供有关指定了作用域的服务注册你`CustomCookieAuthenticationEvents`类：</span><span class="sxs-lookup"><span data-stu-id="3475c-338">Provide a scoped service registration for your `CustomCookieAuthenticationEvents` class:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        options.EventsType = typeof(CustomCookieAuthenticationEvents);
    });

services.AddScoped<CustomCookieAuthenticationEvents>();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-339">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-339">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3475c-340">若要实现的替代`ValidateAsync`事件，写入具有以下签名的方法：</span><span class="sxs-lookup"><span data-stu-id="3475c-340">To implement an override for the `ValidateAsync` event, write a method with the following signature:</span></span>

```csharp
ValidateAsync(CookieValidatePrincipalContext)
```

<span data-ttu-id="3475c-341">ASP.NET 核心标识作为的一部分实现这一检查其[SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync)。</span><span class="sxs-lookup"><span data-stu-id="3475c-341">ASP.NET Core Identity implements this check as part of its [SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync).</span></span> <span data-ttu-id="3475c-342">示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="3475c-342">An example looks like the following:</span></span>

```csharp
public static class LastChangedValidator
{
    public static async Task ValidateAsync(CookieValidatePrincipalContext context)
    {
        // Pull database from registered DI services.
        var userRepository = 
            context.HttpContext.RequestServices
                .GetRequiredService<IUserRepository>();
        var userPrincipal = context.Principal;

        // Look for the last changed claim.
        var lastChanged = (from c in userPrincipal.Claims
                           where c.Type == "LastChanged"
                           select c.Value).FirstOrDefault();

        if (string.IsNullOrEmpty(lastChanged) ||
            !userRepository.ValidateLastChanged(lastChanged))
        {
            context.RejectPrincipal();

            await context.HttpContext.SignOutAsync(
                CookieAuthenticationDefaults.AuthenticationScheme);
        }
    }
}
```

<span data-ttu-id="3475c-343">在中的 cookie 的身份验证配置期间注册事件`Configure`方法：</span><span class="sxs-lookup"><span data-stu-id="3475c-343">Register the event during cookie authentication configuration in the `Configure` method:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    Events = new CookieAuthenticationEvents
    {
        OnValidatePrincipal = LastChangedValidator.ValidateAsync
    }
});
```

---

<span data-ttu-id="3475c-344">请考虑在其中更新用户的名称的情况下&mdash;决策不会影响任何方式中的安全性。</span><span class="sxs-lookup"><span data-stu-id="3475c-344">Consider a situation in which the user's name is updated &mdash; a decision that doesn't affect security in any way.</span></span> <span data-ttu-id="3475c-345">如果你想要非破坏性地更新的用户主体，调用`context.ReplacePrincipal`并设置`context.ShouldRenew`属性`true`。</span><span class="sxs-lookup"><span data-stu-id="3475c-345">If you want to non-destructively update the user principal, call `context.ReplacePrincipal` and set the `context.ShouldRenew` property to `true`.</span></span>

> [!WARNING]
> <span data-ttu-id="3475c-346">此处介绍的方法上的每个请求触发。</span><span class="sxs-lookup"><span data-stu-id="3475c-346">The approach described here is triggered on every request.</span></span> <span data-ttu-id="3475c-347">这可能导致应用程序较大的性能损失。</span><span class="sxs-lookup"><span data-stu-id="3475c-347">This can result in a large performance penalty for the app.</span></span>

## <a name="persistent-cookies"></a><span data-ttu-id="3475c-348">永久 cookie</span><span class="sxs-lookup"><span data-stu-id="3475c-348">Persistent cookies</span></span>

<span data-ttu-id="3475c-349">你可能想要在浏览器会话之间保持的 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-349">You may want the cookie to persist across browser sessions.</span></span> <span data-ttu-id="3475c-350">仅应使用显式用户有一个"记住我"复选框上登录名或类似机制同意的情况下启用此持久性。</span><span class="sxs-lookup"><span data-stu-id="3475c-350">This persistence should only be enabled with explicit user consent with a "Remember Me" checkbox on login or a similar mechanism.</span></span> 

<span data-ttu-id="3475c-351">下面的代码段将创建的标识和能够通过浏览器闭包后保留下来的相应 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-351">The following code snippet creates an identity and corresponding cookie that survives through browser closures.</span></span> <span data-ttu-id="3475c-352">遵循任何以前配置的滑动过期设置。</span><span class="sxs-lookup"><span data-stu-id="3475c-352">Any sliding expiration settings previously configured are honored.</span></span> <span data-ttu-id="3475c-353">如果 cookie 过期浏览器处于关闭状态时，浏览器将它重新启动后清除 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-353">If the cookie expires while the browser is closed, the browser clears the cookie once it's restarted.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-354">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-354">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="3475c-355">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0)类驻留在`Microsoft.AspNetCore.Authentication`命名空间。</span><span class="sxs-lookup"><span data-stu-id="3475c-355">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0) class resides in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-356">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-356">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="3475c-357">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1)类驻留在`Microsoft.AspNetCore.Http.Authentication`命名空间。</span><span class="sxs-lookup"><span data-stu-id="3475c-357">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1) class resides in the `Microsoft.AspNetCore.Http.Authentication` namespace.</span></span>

---

## <a name="absolute-cookie-expiration"></a><span data-ttu-id="3475c-358">绝对 cookie 到期时间</span><span class="sxs-lookup"><span data-stu-id="3475c-358">Absolute cookie expiration</span></span>

<span data-ttu-id="3475c-359">你可以设置与绝对过期时间`ExpiresUtc`。</span><span class="sxs-lookup"><span data-stu-id="3475c-359">You can set an absolute expiration time with `ExpiresUtc`.</span></span> <span data-ttu-id="3475c-360">你还必须设置`IsPersistent`; 否则为`ExpiresUtc`将被忽略，并创建一个单会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-360">You must also set `IsPersistent`; otherwise, `ExpiresUtc` is ignored and a single-session cookie is created.</span></span> <span data-ttu-id="3475c-361">当`ExpiresUtc`上设置`SignInAsync`，它将重写的值`ExpireTimeSpan`选项`CookieAuthenticationOptions`，如果设置。</span><span class="sxs-lookup"><span data-stu-id="3475c-361">When `ExpiresUtc` is set on `SignInAsync`, it overrides the value of the `ExpireTimeSpan` option of `CookieAuthenticationOptions`, if set.</span></span>

<span data-ttu-id="3475c-362">下面的代码段将创建的标识和持续时间为 20 分钟的相应 cookie。</span><span class="sxs-lookup"><span data-stu-id="3475c-362">The following code snippet creates an identity and corresponding cookie that lasts for 20 minutes.</span></span> <span data-ttu-id="3475c-363">这将忽略任何以前配置的滑动过期设置。</span><span class="sxs-lookup"><span data-stu-id="3475c-363">This ignores any sliding expiration settings previously configured.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3475c-364">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="3475c-364">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3475c-365">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="3475c-365">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true,
        ExpiresUtc = DateTime.UtcNow.AddMinutes(20)
    });
```

---

## <a name="see-also"></a><span data-ttu-id="3475c-366">请参阅</span><span class="sxs-lookup"><span data-stu-id="3475c-366">See also</span></span>

* [<span data-ttu-id="3475c-367">身份验证 2.0 更改 / 迁移公告</span><span class="sxs-lookup"><span data-stu-id="3475c-367">Auth 2.0 Changes / Migration Announcement</span></span>](https://github.com/aspnet/Announcements/issues/262)
* [<span data-ttu-id="3475c-368">使用方案限制标识</span><span class="sxs-lookup"><span data-stu-id="3475c-368">Limit identity by scheme</span></span>](xref:security/authorization/limitingidentitybyscheme)
* [<span data-ttu-id="3475c-369">基于声明的授权</span><span class="sxs-lookup"><span data-stu-id="3475c-369">Claims-Based Authorization</span></span>](xref:security/authorization/claims)
* [<span data-ttu-id="3475c-370">基于策略的角色检查</span><span class="sxs-lookup"><span data-stu-id="3475c-370">Policy-based role checks</span></span>](xref:security/authorization/roles#policy-based-role-checks)
