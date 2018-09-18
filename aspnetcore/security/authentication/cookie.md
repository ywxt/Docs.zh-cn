---
title: 使用 cookie 而无需 ASP.NET Core 标识的身份验证
author: rick-anderson
description: 使用 cookie 而无需 ASP.NET Core 标识的身份验证的说明
ms.author: riande
ms.date: 10/11/2017
uid: security/authentication/cookie
ms.openlocfilehash: 8045a1bf27853ff5f03166e7cf10d89e2ad38fd1
ms.sourcegitcommit: b2723654af4969a24545f09ebe32004cb5e84a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2018
ms.locfileid: "46011831"
---
# <a name="use-cookie-authentication-without-aspnet-core-identity"></a><span data-ttu-id="8fc87-103">使用 cookie 而无需 ASP.NET Core 标识的身份验证</span><span class="sxs-lookup"><span data-stu-id="8fc87-103">Use cookie authentication without ASP.NET Core Identity</span></span>

<span data-ttu-id="8fc87-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="8fc87-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="8fc87-105">如你所见在早期的身份验证主题中， [ASP.NET Core 标识](xref:security/authentication/identity)完成、 功能完备的身份验证提供程序是用于创建和维护登录名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-105">As you've seen in the earlier authentication topics, [ASP.NET Core Identity](xref:security/authentication/identity) is a complete, full-featured authentication provider for creating and maintaining logins.</span></span> <span data-ttu-id="8fc87-106">但是，你可能想要使用基于 cookie 的身份验证有时使用您自己的自定义身份验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="8fc87-106">However, you may want to use your own custom authentication logic with cookie-based authentication at times.</span></span> <span data-ttu-id="8fc87-107">你可以使用基于 cookie 的身份验证作为独立身份验证提供程序，没有 ASP.NET Core 标识。</span><span class="sxs-lookup"><span data-stu-id="8fc87-107">You can use cookie-based authentication as a standalone authentication provider without ASP.NET Core Identity.</span></span>

<span data-ttu-id="8fc87-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8fc87-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/cookie/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="8fc87-109">出于演示目的，示例应用程序中，假设用户、 Maria Rodriguez 的用户帐户是硬编码到应用程序。</span><span class="sxs-lookup"><span data-stu-id="8fc87-109">For demonstration purposes in the sample app, the user account for the hypothetical user, Maria Rodriguez, is hardcoded into the app.</span></span> <span data-ttu-id="8fc87-110">使用电子邮件用户名"maria.rodriguez@contoso.com"和任何密码以登录用户。</span><span class="sxs-lookup"><span data-stu-id="8fc87-110">Use the Email username "maria.rodriguez@contoso.com" and any password to sign in the user.</span></span> <span data-ttu-id="8fc87-111">用户进行身份验证中`AuthenticateUser`中的方法*Pages/Account/Login.cshtml.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8fc87-111">The user is authenticated in the `AuthenticateUser` method in the *Pages/Account/Login.cshtml.cs* file.</span></span> <span data-ttu-id="8fc87-112">在实际示例中，用户会根据数据库身份验证。</span><span class="sxs-lookup"><span data-stu-id="8fc87-112">In a real-world example, the user would be authenticated against a database.</span></span>

<span data-ttu-id="8fc87-113">有关从 ASP.NET Core 迁移基于 cookie 的身份验证信息 1.x 到 2.0，请参阅[迁移身份验证和标识到 ASP.NET Core 2.0 主题 （基于 Cookie 的身份验证）](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-113">For information on migrating cookie-based authentication from ASP.NET Core 1.x to 2.0, see [Migrate Authentication and Identity to ASP.NET Core 2.0 topic (Cookie-based Authentication)](xref:migration/1x-to-2x/identity-2x#cookie-based-authentication).</span></span>

<span data-ttu-id="8fc87-114">若要使用 ASP.NET Core 标识，请参阅[标识简介](xref:security/authentication/identity)主题。</span><span class="sxs-lookup"><span data-stu-id="8fc87-114">To use ASP.NET Core Identity, see the [Introduction to Identity](xref:security/authentication/identity) topic.</span></span>

## <a name="configuration"></a><span data-ttu-id="8fc87-115">配置</span><span class="sxs-lookup"><span data-stu-id="8fc87-115">Configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-116">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-116">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="8fc87-117">如果应用不使用[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)，在项目文件中创建的包引用[Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/)包 (版本 2.1.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="8fc87-117">If the app doesn't use the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app), create a package reference in the project file for the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) package (version 2.1.0 or later).</span></span>

<span data-ttu-id="8fc87-118">在中`ConfigureServices`方法中，创建具有的身份验证中间件服务`AddAuthentication`和`AddCookie`方法：</span><span class="sxs-lookup"><span data-stu-id="8fc87-118">In the `ConfigureServices` method, create the Authentication Middleware service with the `AddAuthentication` and `AddCookie` methods:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet1)]

<span data-ttu-id="8fc87-119">`AuthenticationScheme` 传递给`AddAuthentication`设置应用程序的默认身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-119">`AuthenticationScheme` passed to `AddAuthentication` sets the default authentication scheme for the app.</span></span> <span data-ttu-id="8fc87-120">`AuthenticationScheme` 有多个实例的 cookie 身份验证并要时很有用[与特定方案授权](xref:security/authorization/limitingidentitybyscheme)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-120">`AuthenticationScheme` is useful when there are multiple instances of cookie authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="8fc87-121">设置`AuthenticationScheme`到`CookieAuthenticationDefaults.AuthenticationScheme`方案提供的值为"Cookie"。</span><span class="sxs-lookup"><span data-stu-id="8fc87-121">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="8fc87-122">你可以提供任何字符串值，用于区分方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-122">You can supply any string value that distinguishes the scheme.</span></span>

<span data-ttu-id="8fc87-123">应用程序的身份验证方案是不同的应用程序的 cookie 身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-123">The app's authentication scheme is different from the app's cookie authentication scheme.</span></span> <span data-ttu-id="8fc87-124">当 cookie 身份验证方案不提供给<xref:Microsoft.Extensions.DependencyInjection.CookieExtensions.AddCookie*>，它使用[CookieAuthenticationDefaults.AuthenticationScheme](xref:Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationDefaults.AuthenticationScheme) ("Cookie")。</span><span class="sxs-lookup"><span data-stu-id="8fc87-124">When a cookie authentication scheme isn't provided to <xref:Microsoft.Extensions.DependencyInjection.CookieExtensions.AddCookie*>, it uses [CookieAuthenticationDefaults.AuthenticationScheme](xref:Microsoft.AspNetCore.Authentication.Cookies.CookieAuthenticationDefaults.AuthenticationScheme) ("Cookies").</span></span>

<span data-ttu-id="8fc87-125">在中`Configure`方法，请使用`UseAuthentication`方法调用设置身份验证中间件`HttpContext.User`属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-125">In the `Configure` method, use the `UseAuthentication` method to invoke the Authentication Middleware that sets the `HttpContext.User` property.</span></span> <span data-ttu-id="8fc87-126">调用`UseAuthentication`方法之前调用`UseMvcWithDefaultRoute`或`UseMvc`:</span><span class="sxs-lookup"><span data-stu-id="8fc87-126">Call the `UseAuthentication` method before calling `UseMvcWithDefaultRoute` or `UseMvc`:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Startup.cs?name=snippet2)]

<span data-ttu-id="8fc87-127">**AddCookie 选项**</span><span class="sxs-lookup"><span data-stu-id="8fc87-127">**AddCookie Options**</span></span>

<span data-ttu-id="8fc87-128">[CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0)类用于配置身份验证提供程序选项。</span><span class="sxs-lookup"><span data-stu-id="8fc87-128">The [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions?view=aspnetcore-2.0) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="8fc87-129">选项</span><span class="sxs-lookup"><span data-stu-id="8fc87-129">Option</span></span> | <span data-ttu-id="8fc87-130">描述</span><span class="sxs-lookup"><span data-stu-id="8fc87-130">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="8fc87-131">AccessDeniedPath</span><span class="sxs-lookup"><span data-stu-id="8fc87-131">AccessDeniedPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.accessdeniedpath?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-132">提供的路径以提供 302 已找到 （URL 重定向） 时触发的`HttpContext.ForbidAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-132">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ForbidAsync`.</span></span> <span data-ttu-id="8fc87-133">默认值为 `/Account/AccessDenied`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-133">The default value is `/Account/AccessDenied`.</span></span> |
| [<span data-ttu-id="8fc87-134">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="8fc87-134">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.claimsissuer?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-135">要用于的颁发者[颁发者](/dotnet/api/system.security.claims.claim.issuer)上创建由 cookie 身份验证服务的任何声明的属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-135">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication service.</span></span> |
| [<span data-ttu-id="8fc87-136">Cookie.Domain</span><span class="sxs-lookup"><span data-stu-id="8fc87-136">Cookie.Domain</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.domain?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-137">Cookie 提供服务位置的域名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-137">The domain name where the cookie is served.</span></span> <span data-ttu-id="8fc87-138">默认情况下，这是请求的主机名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-138">By default, this is the host name of the request.</span></span> <span data-ttu-id="8fc87-139">在浏览器仅将 cookie 在请求中发送到匹配的主机名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-139">The browser only sends the cookie in requests to a matching host name.</span></span> <span data-ttu-id="8fc87-140">您可能希望调整此项是在你的域中有 cookie 提供给任何主机。</span><span class="sxs-lookup"><span data-stu-id="8fc87-140">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="8fc87-141">例如，将 cookie 域设置为`.contoso.com`使其可供`contoso.com`， `www.contoso.com`，和`staging.www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-141">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="8fc87-142">Cookie.Expiration</span><span class="sxs-lookup"><span data-stu-id="8fc87-142">Cookie.Expiration</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.expiration?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-143">获取或设置 cookie 的生命期。</span><span class="sxs-lookup"><span data-stu-id="8fc87-143">Gets or sets the lifespan of a cookie.</span></span> <span data-ttu-id="8fc87-144">目前，此选项没有 ops，并且将会过时中 ASP.NET Core 2.1 +。</span><span class="sxs-lookup"><span data-stu-id="8fc87-144">Currently, this option no-ops and will become obsolete in ASP.NET Core 2.1+.</span></span> <span data-ttu-id="8fc87-145">使用`ExpireTimeSpan`选项可以设置 cookie 到期时间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-145">Use the `ExpireTimeSpan` option to set cookie expiration.</span></span> <span data-ttu-id="8fc87-146">有关详细信息，请参阅[阐明行为 CookieAuthenticationOptions.Cookie.Expiration](https://github.com/aspnet/Security/issues/1293)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-146">For more information, see [Clarify behavior of CookieAuthenticationOptions.Cookie.Expiration](https://github.com/aspnet/Security/issues/1293).</span></span> |
| [<span data-ttu-id="8fc87-147">Cookie.HttpOnly</span><span class="sxs-lookup"><span data-stu-id="8fc87-147">Cookie.HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.httponly?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-148">指示是否 cookie 应只允许到服务器可访问的标志。</span><span class="sxs-lookup"><span data-stu-id="8fc87-148">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="8fc87-149">此值更改为`false`允许客户端脚本访问 cookie，并可能会打开 cookie 被盗应用应您的应用程序具有[跨站点脚本 (XSS)](xref:security/cross-site-scripting)漏洞。</span><span class="sxs-lookup"><span data-stu-id="8fc87-149">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="8fc87-150">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-150">The default value is `true`.</span></span> |
| [<span data-ttu-id="8fc87-151">Cookie.Name</span><span class="sxs-lookup"><span data-stu-id="8fc87-151">Cookie.Name</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.name?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-152">设置的 cookie 的名称。</span><span class="sxs-lookup"><span data-stu-id="8fc87-152">Sets the name of the cookie.</span></span> |
| [<span data-ttu-id="8fc87-153">Cookie.Path</span><span class="sxs-lookup"><span data-stu-id="8fc87-153">Cookie.Path</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.path?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-154">用于隔离同一主机名上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-154">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="8fc87-155">如果必须在运行的应用`/app1`并且想要将 cookie 限制为该应用，设置`CookiePath`属性设置为`/app1`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-155">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="8fc87-156">通过此操作，cookie 是仅可在请求上`/app1`和其下的任何应用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-156">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="8fc87-157">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="8fc87-157">Cookie.SameSite</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.samesite?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-158">指示浏览器是否应允许要附加到同一站点的请求的 cookie (`SameSiteMode.Strict`) 或使用安全的 HTTP 方法和同一站点的请求的跨站点请求 (`SameSiteMode.Lax`)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-158">Indicates whether the browser should allow the cookie to be attached to same-site requests only (`SameSiteMode.Strict`) or cross-site requests using safe HTTP methods and same-site requests (`SameSiteMode.Lax`).</span></span> <span data-ttu-id="8fc87-159">如果设置为`SameSiteMode.None`，未设置的 cookie 标头值。</span><span class="sxs-lookup"><span data-stu-id="8fc87-159">When set to `SameSiteMode.None`, the cookie header value isn't set.</span></span> <span data-ttu-id="8fc87-160">请注意， [Cookie 策略中间件](#cookie-policy-middleware)可能会覆盖你提供的值。</span><span class="sxs-lookup"><span data-stu-id="8fc87-160">Note that [Cookie Policy Middleware](#cookie-policy-middleware) might overwrite the value that you provide.</span></span> <span data-ttu-id="8fc87-161">若要支持 OAuth 身份验证，默认值是`SameSiteMode.Lax`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-161">To support OAuth authentication, the default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="8fc87-162">有关详细信息，请参阅[OAuth 身份验证由于 SameSite cookie 策略中断](https://github.com/aspnet/Security/issues/1231)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-162">For more information, see [OAuth authentication broken due to SameSite cookie policy](https://github.com/aspnet/Security/issues/1231).</span></span> |
| [<span data-ttu-id="8fc87-163">Cookie.SecurePolicy</span><span class="sxs-lookup"><span data-stu-id="8fc87-163">Cookie.SecurePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.http.cookiebuilder.securepolicy?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-164">一个标志，指示是否创建的 cookie 应限制为 HTTPS (`CookieSecurePolicy.Always`)，HTTP 或 HTTPS (`CookieSecurePolicy.None`)，或与请求相同的协议 (`CookieSecurePolicy.SameAsRequest`)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-164">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="8fc87-165">默认值为 `CookieSecurePolicy.SameAsRequest`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-165">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="8fc87-166">DataProtectionProvider</span><span class="sxs-lookup"><span data-stu-id="8fc87-166">DataProtectionProvider</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-167">集`DataProtectionProvider`用于创建默认`TicketDataFormat`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-167">Sets the `DataProtectionProvider` that's used to create the default `TicketDataFormat`.</span></span> <span data-ttu-id="8fc87-168">如果`TicketDataFormat`属性设置，`DataProtectionProvider`选项不会继续使用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-168">If the `TicketDataFormat` property is set, the `DataProtectionProvider` option isn't used.</span></span> <span data-ttu-id="8fc87-169">如果未提供，则使用应用程序的默认数据保护提供程序。</span><span class="sxs-lookup"><span data-stu-id="8fc87-169">If not provided, the app's default data protection provider is used.</span></span> |
| [<span data-ttu-id="8fc87-170">事件</span><span class="sxs-lookup"><span data-stu-id="8fc87-170">Events</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.events?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-171">该处理程序处理的特定点上提供的应用程序控制的提供程序上调用方法。</span><span class="sxs-lookup"><span data-stu-id="8fc87-171">The handler calls methods on the provider that give the app control at certain processing points.</span></span> <span data-ttu-id="8fc87-172">如果`Events`不提供的默认实例提供时才调用这些方法不执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="8fc87-172">If `Events` aren't provided, a default instance is supplied that does nothing when the methods are called.</span></span> |
| [<span data-ttu-id="8fc87-173">EventsType</span><span class="sxs-lookup"><span data-stu-id="8fc87-173">EventsType</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.eventstype?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-174">用作服务类型，以获取`Events`实例而不是属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-174">Used as the service type to get the `Events` instance instead of the property.</span></span> |
| [<span data-ttu-id="8fc87-175">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="8fc87-175">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.expiretimespan?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-176">`TimeSpan`后将存储在 cookie 的身份验证票证到期。</span><span class="sxs-lookup"><span data-stu-id="8fc87-176">The `TimeSpan` after which the authentication ticket stored inside the cookie expires.</span></span> <span data-ttu-id="8fc87-177">`ExpireTimeSpan` 添加到当前时间来创建票证的到期时间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-177">`ExpireTimeSpan` is added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="8fc87-178">`ExpiredTimeSpan`值始终会进入加密 AuthTicket 验证服务器。</span><span class="sxs-lookup"><span data-stu-id="8fc87-178">The `ExpiredTimeSpan` value always goes into the encrypted AuthTicket verified by the server.</span></span> <span data-ttu-id="8fc87-179">此外可能进入[Set-cookie](https://tools.ietf.org/html/rfc6265#section-4.1)标头，但仅当`IsPersistent`设置。</span><span class="sxs-lookup"><span data-stu-id="8fc87-179">It may also go into the [Set-Cookie](https://tools.ietf.org/html/rfc6265#section-4.1) header, but only if `IsPersistent` is set.</span></span> <span data-ttu-id="8fc87-180">若要设置`IsPersistent`到`true`，配置[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties)传递给`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-180">To set `IsPersistent` to `true`, configure the [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties) passed to `SignInAsync`.</span></span> <span data-ttu-id="8fc87-181">默认值`ExpireTimeSpan`为 14 天。</span><span class="sxs-lookup"><span data-stu-id="8fc87-181">The default value of `ExpireTimeSpan` is 14 days.</span></span> |
| [<span data-ttu-id="8fc87-182">LoginPath</span><span class="sxs-lookup"><span data-stu-id="8fc87-182">LoginPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.loginpath?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-183">提供的路径以提供 302 已找到 （URL 重定向） 时触发的`HttpContext.ChallengeAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-183">Provides the path to supply with a 302 Found (URL redirect) when triggered by `HttpContext.ChallengeAsync`.</span></span> <span data-ttu-id="8fc87-184">生成 401 的当前 URL 添加到`LoginPath`作为查询字符串参数的名为`ReturnUrlParameter`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-184">The current URL that generated the 401 is added to the `LoginPath` as a query string parameter named by the `ReturnUrlParameter`.</span></span> <span data-ttu-id="8fc87-185">一次请求`LoginPath`授予新登录标识，`ReturnUrlParameter`值用于将浏览器重定向回导致原始未授权的状态代码的 URL。</span><span class="sxs-lookup"><span data-stu-id="8fc87-185">Once a request to the `LoginPath` grants a new sign-in identity, the `ReturnUrlParameter` value is used to redirect the browser back to the URL that caused the original unauthorized status code.</span></span> <span data-ttu-id="8fc87-186">默认值为 `/Account/Login`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-186">The default value is `/Account/Login`.</span></span> |
| [<span data-ttu-id="8fc87-187">LogoutPath</span><span class="sxs-lookup"><span data-stu-id="8fc87-187">LogoutPath</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.logoutpath?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-188">如果`LogoutPath`提供给处理程序，则将重定向到该路径的请求值的基础`ReturnUrlParameter`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-188">If the `LogoutPath` is provided to the handler, then a request to that path redirects based on the value of the `ReturnUrlParameter`.</span></span> <span data-ttu-id="8fc87-189">默认值为 `/Account/Logout`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-189">The default value is `/Account/Logout`.</span></span> |
| [<span data-ttu-id="8fc87-190">ReturnUrlParameter</span><span class="sxs-lookup"><span data-stu-id="8fc87-190">ReturnUrlParameter</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.returnurlparameter?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-191">确定由 302 已找到 （URL 重定向） 响应的处理程序追加查询字符串参数的名称。</span><span class="sxs-lookup"><span data-stu-id="8fc87-191">Determines the name of the query string parameter that's appended by the handler for a 302 Found (URL redirect) response.</span></span> <span data-ttu-id="8fc87-192">`ReturnUrlParameter` 请求到达时，将使用`LoginPath`或`LogoutPath`来执行登录或注销操作后返回到原始 URL 的浏览器。</span><span class="sxs-lookup"><span data-stu-id="8fc87-192">`ReturnUrlParameter` is used when a request arrives on the `LoginPath` or `LogoutPath` to return the browser to the original URL after the login or logout action is performed.</span></span> <span data-ttu-id="8fc87-193">默认值为 `ReturnUrl`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-193">The default value is `ReturnUrl`.</span></span> |
| [<span data-ttu-id="8fc87-194">SessionStore</span><span class="sxs-lookup"><span data-stu-id="8fc87-194">SessionStore</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.sessionstore?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-195">一个可选容器，用于标识存储在请求之间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-195">An optional container used to store identity across requests.</span></span> <span data-ttu-id="8fc87-196">使用时，只将会话标识符发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="8fc87-196">When used, only a session identifier is sent to the client.</span></span> <span data-ttu-id="8fc87-197">`SessionStore` 可以用于缓解大型标识的潜在问题。</span><span class="sxs-lookup"><span data-stu-id="8fc87-197">`SessionStore` can be used to mitigate potential problems with large identities.</span></span> |
| [<span data-ttu-id="8fc87-198">slidingExpiration</span><span class="sxs-lookup"><span data-stu-id="8fc87-198">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-199">指示是否应动态颁发包含更新的到期时间的新 cookie 的标志。</span><span class="sxs-lookup"><span data-stu-id="8fc87-199">A flag indicating if a new cookie with an updated expiration time should be issued dynamically.</span></span> <span data-ttu-id="8fc87-200">这可以在任何请求，其中当前 cookie 过期时间已超过 50%过期。</span><span class="sxs-lookup"><span data-stu-id="8fc87-200">This can happen on any request where the current cookie expiration period is more than 50% expired.</span></span> <span data-ttu-id="8fc87-201">向前移动新的到期日期为当前日期加上`ExpireTimespan`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-201">The new expiration date is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="8fc87-202">[绝对 cookie 到期时间](xref:security/authentication/cookie#absolute-cookie-expiration)可以通过使用设置`AuthenticationProperties`类调用时`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-202">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="8fc87-203">绝对过期时间可以通过限制身份验证 cookie 是有效的时间量来提高您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-203">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="8fc87-204">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-204">The default value is `true`.</span></span> |
| [<span data-ttu-id="8fc87-205">TicketDataFormat</span><span class="sxs-lookup"><span data-stu-id="8fc87-205">TicketDataFormat</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.ticketdataformat?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-206">`TicketDataFormat`用于保护和取消保护标识和存储在 cookie 值中的其他属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-206">The `TicketDataFormat` is used to protect and unprotect the identity and other properties that are stored in the cookie value.</span></span> <span data-ttu-id="8fc87-207">如果未提供，`TicketDataFormat`使用创建[DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-207">If not provided, a `TicketDataFormat` is created using the [DataProtectionProvider](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions.dataprotectionprovider?view=aspnetcore-2.0).</span></span> |
| [<span data-ttu-id="8fc87-208">验证</span><span class="sxs-lookup"><span data-stu-id="8fc87-208">Validate</span></span>](/dotnet/api/microsoft.aspnetcore.authentication.authenticationschemeoptions.validate?view=aspnetcore-2.0) | <span data-ttu-id="8fc87-209">检查的选项是有效的方法。</span><span class="sxs-lookup"><span data-stu-id="8fc87-209">Method that checks that the options are valid.</span></span> |

<span data-ttu-id="8fc87-210">设置`CookieAuthenticationOptions`中的身份验证的服务配置中`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="8fc87-210">Set `CookieAuthenticationOptions` in the service configuration for authentication in the `ConfigureServices` method:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        ...
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-211">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-211">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="8fc87-212">ASP.NET Core 1.x 使用 cookie[中间件](xref:fundamentals/middleware/index)，序列化为一个用户主体的加密 cookie。</span><span class="sxs-lookup"><span data-stu-id="8fc87-212">ASP.NET Core 1.x uses cookie [middleware](xref:fundamentals/middleware/index) that serializes a user principal into an encrypted cookie.</span></span> <span data-ttu-id="8fc87-213">在后续请求中，对 cookie 进行验证，并重新创建和分配给主体`HttpContext.User`属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-213">On subsequent requests, the cookie is validated, and the principal is recreated and assigned to the `HttpContext.User` property.</span></span>

<span data-ttu-id="8fc87-214">安装[Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/)在项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8fc87-214">Install the [Microsoft.AspNetCore.Authentication.Cookies](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Cookies/) NuGet package in your project.</span></span> <span data-ttu-id="8fc87-215">此包包含 cookie 中间件。</span><span class="sxs-lookup"><span data-stu-id="8fc87-215">This package contains the cookie middleware.</span></span>

<span data-ttu-id="8fc87-216">使用`UseCookieAuthentication`中的方法`Configure`中的方法您*Startup.cs*文件，然后`UseMvc`或`UseMvcWithDefaultRoute`:</span><span class="sxs-lookup"><span data-stu-id="8fc87-216">Use the `UseCookieAuthentication` method in the `Configure` method in your *Startup.cs* file before `UseMvc` or `UseMvcWithDefaultRoute`:</span></span>

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

<span data-ttu-id="8fc87-217">**CookieAuthenticationOptions 选项**</span><span class="sxs-lookup"><span data-stu-id="8fc87-217">**CookieAuthenticationOptions Options**</span></span>

<span data-ttu-id="8fc87-218">[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1)类用于配置身份验证提供程序选项。</span><span class="sxs-lookup"><span data-stu-id="8fc87-218">The [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions?view=aspnetcore-1.1) class is used to configure the authentication provider options.</span></span>

| <span data-ttu-id="8fc87-219">选项</span><span class="sxs-lookup"><span data-stu-id="8fc87-219">Option</span></span> | <span data-ttu-id="8fc87-220">描述</span><span class="sxs-lookup"><span data-stu-id="8fc87-220">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="8fc87-221">AuthenticationScheme</span><span class="sxs-lookup"><span data-stu-id="8fc87-221">AuthenticationScheme</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.authenticationscheme?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-222">设置身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-222">Sets the authentication scheme.</span></span> <span data-ttu-id="8fc87-223">`AuthenticationScheme` 时，可以有多个实例的身份验证，并且你想要[与特定方案授权](xref:security/authorization/limitingidentitybyscheme)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-223">`AuthenticationScheme` is useful when there are multiple instances of authentication and you want to [authorize with a specific scheme](xref:security/authorization/limitingidentitybyscheme).</span></span> <span data-ttu-id="8fc87-224">设置`AuthenticationScheme`到`CookieAuthenticationDefaults.AuthenticationScheme`方案提供的值为"Cookie"。</span><span class="sxs-lookup"><span data-stu-id="8fc87-224">Setting the `AuthenticationScheme` to `CookieAuthenticationDefaults.AuthenticationScheme` provides a value of "Cookies" for the scheme.</span></span> <span data-ttu-id="8fc87-225">你可以提供任何字符串值，用于区分方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-225">You can supply any string value that distinguishes the scheme.</span></span> |
| [<span data-ttu-id="8fc87-226">AutomaticAuthenticate</span><span class="sxs-lookup"><span data-stu-id="8fc87-226">AutomaticAuthenticate</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticauthenticate?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-227">设置一个值，以指示 cookie 身份验证应在每个请求上运行并尝试验证并重新构造它创建的任何序列化的主体。</span><span class="sxs-lookup"><span data-stu-id="8fc87-227">Sets a value to indicate that the cookie authentication should run on every request and attempt to validate and reconstruct any serialized principal it created.</span></span> |
| [<span data-ttu-id="8fc87-228">AutomaticChallenge</span><span class="sxs-lookup"><span data-stu-id="8fc87-228">AutomaticChallenge</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.automaticchallenge?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-229">如果为 true，则身份验证中间件处理自动挑战。</span><span class="sxs-lookup"><span data-stu-id="8fc87-229">If true, the authentication middleware handles automatic challenges.</span></span> <span data-ttu-id="8fc87-230">如果为 false，身份验证中间件仅更改时进行显式指定响应`AuthenticationScheme`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-230">If false, the authentication middleware only alters responses when explicitly indicated by the `AuthenticationScheme`.</span></span> |
| [<span data-ttu-id="8fc87-231">ClaimsIssuer</span><span class="sxs-lookup"><span data-stu-id="8fc87-231">ClaimsIssuer</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.claimsissuer?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-232">要用于的颁发者[颁发者](/dotnet/api/system.security.claims.claim.issuer)上创建的 cookie 身份验证中间件的任何声明的属性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-232">The issuer to use for the [Issuer](/dotnet/api/system.security.claims.claim.issuer) property on any claims created by the cookie authentication middleware.</span></span> |
| [<span data-ttu-id="8fc87-233">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="8fc87-233">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiedomain?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-234">Cookie 提供服务位置的域名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-234">The domain name where the cookie is served.</span></span> <span data-ttu-id="8fc87-235">默认情况下，这是请求的主机名。</span><span class="sxs-lookup"><span data-stu-id="8fc87-235">By default, this is the host name of the request.</span></span> <span data-ttu-id="8fc87-236">在浏览器只起到匹配的主机名的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8fc87-236">The browser only serves the cookie to a matching host name.</span></span> <span data-ttu-id="8fc87-237">您可能希望调整此项是在你的域中有 cookie 提供给任何主机。</span><span class="sxs-lookup"><span data-stu-id="8fc87-237">You may wish to adjust this to have cookies available to any host in your domain.</span></span> <span data-ttu-id="8fc87-238">例如，将 cookie 域设置为`.contoso.com`使其可供`contoso.com`， `www.contoso.com`，和`staging.www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-238">For example, setting the cookie domain to `.contoso.com` makes it available to `contoso.com`, `www.contoso.com`, and `staging.www.contoso.com`.</span></span> |
| [<span data-ttu-id="8fc87-239">CookieHttpOnly</span><span class="sxs-lookup"><span data-stu-id="8fc87-239">CookieHttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiehttponly?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-240">指示是否 cookie 应只允许到服务器可访问的标志。</span><span class="sxs-lookup"><span data-stu-id="8fc87-240">A flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="8fc87-241">此值更改为`false`允许客户端脚本访问 cookie，并可能会打开 cookie 被盗应用应您的应用程序具有[跨站点脚本 (XSS)](xref:security/cross-site-scripting)漏洞。</span><span class="sxs-lookup"><span data-stu-id="8fc87-241">Changing this value to `false` permits client-side scripts to access the cookie and may open your app to cookie theft should your app have a [Cross-site scripting (XSS)](xref:security/cross-site-scripting) vulnerability.</span></span> <span data-ttu-id="8fc87-242">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-242">The default value is `true`.</span></span> |
| [<span data-ttu-id="8fc87-243">CookiePath</span><span class="sxs-lookup"><span data-stu-id="8fc87-243">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiepath?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-244">用于隔离同一主机名上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-244">Used to isolate apps running on the same host name.</span></span> <span data-ttu-id="8fc87-245">如果必须在运行的应用`/app1`并且想要将 cookie 限制为该应用，设置`CookiePath`属性设置为`/app1`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-245">If you have an app running at `/app1` and want to restrict cookies to that app, set the `CookiePath` property to `/app1`.</span></span> <span data-ttu-id="8fc87-246">通过此操作，cookie 是仅可在请求上`/app1`和其下的任何应用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-246">By doing so, the cookie is only available on requests to `/app1` and any app underneath it.</span></span> |
| [<span data-ttu-id="8fc87-247">CookieSecure</span><span class="sxs-lookup"><span data-stu-id="8fc87-247">CookieSecure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.cookiesecure?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-248">一个标志，指示是否创建的 cookie 应限制为 HTTPS (`CookieSecurePolicy.Always`)，HTTP 或 HTTPS (`CookieSecurePolicy.None`)，或与请求相同的协议 (`CookieSecurePolicy.SameAsRequest`)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-248">A flag indicating if the cookie created should be limited to HTTPS (`CookieSecurePolicy.Always`), HTTP or HTTPS (`CookieSecurePolicy.None`), or the same protocol as the request (`CookieSecurePolicy.SameAsRequest`).</span></span> <span data-ttu-id="8fc87-249">默认值为 `CookieSecurePolicy.SameAsRequest`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-249">The default value is `CookieSecurePolicy.SameAsRequest`.</span></span> |
| [<span data-ttu-id="8fc87-250">说明</span><span class="sxs-lookup"><span data-stu-id="8fc87-250">Description</span></span>](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions.description?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-251">有关提供给应用程序的身份验证类型的其他信息。</span><span class="sxs-lookup"><span data-stu-id="8fc87-251">Additional information about the authentication type which is made available to the app.</span></span> |
| [<span data-ttu-id="8fc87-252">ExpireTimeSpan</span><span class="sxs-lookup"><span data-stu-id="8fc87-252">ExpireTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.expiretimespan?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-253">`TimeSpan`后将身份验证票证到期。</span><span class="sxs-lookup"><span data-stu-id="8fc87-253">The `TimeSpan` after which the authentication ticket expires.</span></span> <span data-ttu-id="8fc87-254">它被添加到当前时间来创建票证的到期时间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-254">It's added to the current time to create the expiration time for the ticket.</span></span> <span data-ttu-id="8fc87-255">若要使用`ExpireTimeSpan`，则必须设置`IsPersistent`到`true`中`AuthenticationProperties`传递给`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-255">To use `ExpireTimeSpan`, you must set `IsPersistent` to `true` in the `AuthenticationProperties` passed to `SignInAsync`.</span></span> <span data-ttu-id="8fc87-256">默认值为 14 天。</span><span class="sxs-lookup"><span data-stu-id="8fc87-256">The default value is 14 days.</span></span> |
| [<span data-ttu-id="8fc87-257">slidingExpiration</span><span class="sxs-lookup"><span data-stu-id="8fc87-257">SlidingExpiration</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookieauthenticationoptions.slidingexpiration?view=aspnetcore-1.1) | <span data-ttu-id="8fc87-258">一个标志，指示 cookie 的到期日期重置多个的下半部分`ExpireTimeSpan`经过一段时间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-258">A flag indicating whether the cookie expiration date resets when more than half of the `ExpireTimeSpan` interval has passed.</span></span> <span data-ttu-id="8fc87-259">新的 exipiration 时间向前移动，为当前日期加上`ExpireTimespan`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-259">The new exipiration time is moved forward to be the current date plus the `ExpireTimespan`.</span></span> <span data-ttu-id="8fc87-260">[绝对 cookie 到期时间](xref:security/authentication/cookie#absolute-cookie-expiration)可以通过使用设置`AuthenticationProperties`类调用时`SignInAsync`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-260">An [absolute cookie expiration time](xref:security/authentication/cookie#absolute-cookie-expiration) can be set by using the `AuthenticationProperties` class when calling `SignInAsync`.</span></span> <span data-ttu-id="8fc87-261">绝对过期时间可以通过限制身份验证 cookie 是有效的时间量来提高您的应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="8fc87-261">An absolute expiration time can improve the security of your app by limiting the amount of time that the authentication cookie is valid.</span></span> <span data-ttu-id="8fc87-262">默认值为 `true`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-262">The default value is `true`.</span></span> |

<span data-ttu-id="8fc87-263">设置`CookieAuthenticationOptions`Cookie 身份验证中间件中`Configure`方法：</span><span class="sxs-lookup"><span data-stu-id="8fc87-263">Set `CookieAuthenticationOptions` for the Cookie Authentication Middleware in the `Configure` method:</span></span>

```csharp
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    ...
});
```

---

## <a name="cookie-policy-middleware"></a><span data-ttu-id="8fc87-264">Cookie 策略中间件</span><span class="sxs-lookup"><span data-stu-id="8fc87-264">Cookie Policy Middleware</span></span>

<span data-ttu-id="8fc87-265">[Cookie 策略中间件](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware)使应用程序中的 cookie 策略功能。</span><span class="sxs-lookup"><span data-stu-id="8fc87-265">[Cookie Policy Middleware](/dotnet/api/microsoft.aspnetcore.cookiepolicy.cookiepolicymiddleware) enables cookie policy capabilities in an app.</span></span> <span data-ttu-id="8fc87-266">到应用程序处理管道添加中间件是顺序敏感;它只影响在管道中注册后的组件。</span><span class="sxs-lookup"><span data-stu-id="8fc87-266">Adding the middleware to the app processing pipeline is order sensitive; it only affects components registered after it in the pipeline.</span></span>

```csharp
app.UseCookiePolicy(cookiePolicyOptions);
```

 <span data-ttu-id="8fc87-267">[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions)提供给 Cookie 策略中间件可用于控制时追加或删除 cookie 的 cookie 处理和挂钩全局特性 cookie 处理程序。</span><span class="sxs-lookup"><span data-stu-id="8fc87-267">The [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions) provided to the Cookie Policy Middleware allow you to control global characteristics of cookie processing and hook into cookie processing handlers when cookies are appended or deleted.</span></span>

| <span data-ttu-id="8fc87-268">属性</span><span class="sxs-lookup"><span data-stu-id="8fc87-268">Property</span></span> | <span data-ttu-id="8fc87-269">描述</span><span class="sxs-lookup"><span data-stu-id="8fc87-269">Description</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="8fc87-270">HttpOnly</span><span class="sxs-lookup"><span data-stu-id="8fc87-270">HttpOnly</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.httponly) | <span data-ttu-id="8fc87-271">会影响是否 cookie 必须 HttpOnly，该值一个标志，指示是否 cookie 应只允许到服务器可访问。</span><span class="sxs-lookup"><span data-stu-id="8fc87-271">Affects whether cookies must be HttpOnly, which is a flag indicating if the cookie should be accessible only to servers.</span></span> <span data-ttu-id="8fc87-272">默认值为 `HttpOnlyPolicy.None`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-272">The default value is `HttpOnlyPolicy.None`.</span></span> |
| [<span data-ttu-id="8fc87-273">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="8fc87-273">MinimumSameSitePolicy</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.minimumsamesitepolicy) | <span data-ttu-id="8fc87-274">影响的 cookie 的同一站点属性 （见下文）。</span><span class="sxs-lookup"><span data-stu-id="8fc87-274">Affects the cookie's same-site attribute (see below).</span></span> <span data-ttu-id="8fc87-275">默认值为 `SameSiteMode.Lax`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-275">The default value is `SameSiteMode.Lax`.</span></span> <span data-ttu-id="8fc87-276">此选项仅供 ASP.NET Core 2.0 +。</span><span class="sxs-lookup"><span data-stu-id="8fc87-276">This option is available for ASP.NET Core 2.0+.</span></span> |
| [<span data-ttu-id="8fc87-277">OnAppendCookie</span><span class="sxs-lookup"><span data-stu-id="8fc87-277">OnAppendCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.onappendcookie) | <span data-ttu-id="8fc87-278">当会追加一个 cookie 时调用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-278">Called when a cookie is appended.</span></span> |
| [<span data-ttu-id="8fc87-279">OnDeleteCookie</span><span class="sxs-lookup"><span data-stu-id="8fc87-279">OnDeleteCookie</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.ondeletecookie) | <span data-ttu-id="8fc87-280">当删除 cookie 时调用。</span><span class="sxs-lookup"><span data-stu-id="8fc87-280">Called when a cookie is deleted.</span></span> |
| [<span data-ttu-id="8fc87-281">安全</span><span class="sxs-lookup"><span data-stu-id="8fc87-281">Secure</span></span>](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.secure) | <span data-ttu-id="8fc87-282">会影响是否 cookie 必须是安全。</span><span class="sxs-lookup"><span data-stu-id="8fc87-282">Affects whether cookies must be Secure.</span></span> <span data-ttu-id="8fc87-283">默认值为 `CookieSecurePolicy.None`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-283">The default value is `CookieSecurePolicy.None`.</span></span> |

<span data-ttu-id="8fc87-284">**MinimumSameSitePolicy** (ASP.NET Core 2.0 + 仅)</span><span class="sxs-lookup"><span data-stu-id="8fc87-284">**MinimumSameSitePolicy** (ASP.NET Core 2.0+ only)</span></span>

<span data-ttu-id="8fc87-285">默认值`MinimumSameSitePolicy`值是`SameSiteMode.Lax`允许 OAuth2 身份验证。</span><span class="sxs-lookup"><span data-stu-id="8fc87-285">The default `MinimumSameSitePolicy` value is `SameSiteMode.Lax` to permit OAuth2 authentication.</span></span> <span data-ttu-id="8fc87-286">若要严格强制实施的同一站点策略`SameSiteMode.Strict`，请将`MinimumSameSitePolicy`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-286">To strictly enforce a same-site policy of `SameSiteMode.Strict`, set the `MinimumSameSitePolicy`.</span></span> <span data-ttu-id="8fc87-287">尽管此设置会中断的 OAuth2 和其他跨域身份验证方案，它会提升为其他类型的应用不依赖于跨域请求处理的 cookie 安全级别。</span><span class="sxs-lookup"><span data-stu-id="8fc87-287">Although this setting breaks OAuth2 and other cross-origin authentication schemes, it elevates the level of cookie security for other types of apps that don't rely on cross-origin request processing.</span></span>

```csharp
var cookiePolicyOptions = new CookiePolicyOptions
{
    MinimumSameSitePolicy = SameSiteMode.Strict,
};
```

<span data-ttu-id="8fc87-288">Cookie 策略中间件设置`MinimumSameSitePolicy`可能会影响您的设置的`Cookie.SameSite`中`CookieAuthenticationOptions`根据下面的表格的设置。</span><span class="sxs-lookup"><span data-stu-id="8fc87-288">The Cookie Policy Middleware setting for `MinimumSameSitePolicy` can affect your setting of `Cookie.SameSite` in `CookieAuthenticationOptions` settings according to the matrix below.</span></span>

| <span data-ttu-id="8fc87-289">MinimumSameSitePolicy</span><span class="sxs-lookup"><span data-stu-id="8fc87-289">MinimumSameSitePolicy</span></span> | <span data-ttu-id="8fc87-290">Cookie.SameSite</span><span class="sxs-lookup"><span data-stu-id="8fc87-290">Cookie.SameSite</span></span> | <span data-ttu-id="8fc87-291">最终的 Cookie.SameSite 设置</span><span class="sxs-lookup"><span data-stu-id="8fc87-291">Resultant Cookie.SameSite setting</span></span> |
| --------------------- | --------------- | --------------------------------- |
| <span data-ttu-id="8fc87-292">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="8fc87-292">SameSiteMode.None</span></span>     | <span data-ttu-id="8fc87-293">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="8fc87-293">SameSiteMode.None</span></span><br><span data-ttu-id="8fc87-294">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-294">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-295">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-295">SameSiteMode.Strict</span></span> | <span data-ttu-id="8fc87-296">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="8fc87-296">SameSiteMode.None</span></span><br><span data-ttu-id="8fc87-297">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-297">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-298">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-298">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="8fc87-299">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-299">SameSiteMode.Lax</span></span>      | <span data-ttu-id="8fc87-300">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="8fc87-300">SameSiteMode.None</span></span><br><span data-ttu-id="8fc87-301">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-301">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-302">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-302">SameSiteMode.Strict</span></span> | <span data-ttu-id="8fc87-303">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-303">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-304">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-304">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-305">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-305">SameSiteMode.Strict</span></span> |
| <span data-ttu-id="8fc87-306">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-306">SameSiteMode.Strict</span></span>   | <span data-ttu-id="8fc87-307">SameSiteMode.None</span><span class="sxs-lookup"><span data-stu-id="8fc87-307">SameSiteMode.None</span></span><br><span data-ttu-id="8fc87-308">SameSiteMode.Lax</span><span class="sxs-lookup"><span data-stu-id="8fc87-308">SameSiteMode.Lax</span></span><br><span data-ttu-id="8fc87-309">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-309">SameSiteMode.Strict</span></span> | <span data-ttu-id="8fc87-310">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-310">SameSiteMode.Strict</span></span><br><span data-ttu-id="8fc87-311">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-311">SameSiteMode.Strict</span></span><br><span data-ttu-id="8fc87-312">SameSiteMode.Strict</span><span class="sxs-lookup"><span data-stu-id="8fc87-312">SameSiteMode.Strict</span></span> |

## <a name="create-an-authentication-cookie"></a><span data-ttu-id="8fc87-313">创建身份验证 cookie</span><span class="sxs-lookup"><span data-stu-id="8fc87-313">Create an authentication cookie</span></span>

<span data-ttu-id="8fc87-314">若要创建保存用户信息的 cookie，必须构造[ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-314">To create a cookie holding user information, you must construct a [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal).</span></span> <span data-ttu-id="8fc87-315">用户信息序列化并存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="8fc87-315">The user information is serialized and stored in the cookie.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-316">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-316">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="8fc87-317">创建[ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity)包含任何必需[声明](/dotnet/api/system.security.claims.claim)s 和调用[SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0)以登录用户：</span><span class="sxs-lookup"><span data-stu-id="8fc87-317">Create a [ClaimsIdentity](/dotnet/api/system.security.claims.claimsidentity) with any required [Claim](/dotnet/api/system.security.claims.claim)s and call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-2.0) to sign in the user:</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-318">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-318">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="8fc87-319">调用[SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1)以登录用户：</span><span class="sxs-lookup"><span data-stu-id="8fc87-319">Call [SignInAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signinasync?view=aspnetcore-1.1) to sign in the user:</span></span>

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity));
```

---

<span data-ttu-id="8fc87-320">`SignInAsync` 创建一个加密的 cookie，并将其添加到当前响应。</span><span class="sxs-lookup"><span data-stu-id="8fc87-320">`SignInAsync` creates an encrypted cookie and adds it to the current response.</span></span> <span data-ttu-id="8fc87-321">如果未指定`AuthenticationScheme`，则使用默认方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-321">If you don't specify an `AuthenticationScheme`, the default scheme is used.</span></span>

<span data-ttu-id="8fc87-322">事实上，使用的加密是 ASP.NET Core[数据保护](xref:security/data-protection/using-data-protection#security-data-protection-getting-started)系统。</span><span class="sxs-lookup"><span data-stu-id="8fc87-322">Under the covers, the encryption used is ASP.NET Core's [Data Protection](xref:security/data-protection/using-data-protection#security-data-protection-getting-started) system.</span></span> <span data-ttu-id="8fc87-323">如果托管应用在多台计算机、 负载平衡跨应用程序，或使用 web 场，则必须[配置数据保护](xref:security/data-protection/configuration/overview)使用相同密钥环和应用程序标识符。</span><span class="sxs-lookup"><span data-stu-id="8fc87-323">If you're hosting app on multiple machines, load balancing across apps, or using a web farm, then you must [configure data protection](xref:security/data-protection/configuration/overview) to use the same key ring and app identifier.</span></span>

## <a name="sign-out"></a><span data-ttu-id="8fc87-324">注销</span><span class="sxs-lookup"><span data-stu-id="8fc87-324">Sign out</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-325">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-325">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="8fc87-326">若要注销当前用户，然后删除其 cookie，调用[SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span><span class="sxs-lookup"><span data-stu-id="8fc87-326">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signoutasync?view=aspnetcore-2.0):</span></span>

[!code-csharp[](cookie/samples/2.x/CookieSample/Pages/Account/Login.cshtml.cs?name=snippet2)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-327">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-327">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="8fc87-328">若要注销当前用户，然后删除其 cookie，调用[SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span><span class="sxs-lookup"><span data-stu-id="8fc87-328">To sign out the current user and delete their cookie, call [SignOutAsync](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1.signoutasync?view=aspnetcore-1.1):</span></span>

```csharp
await HttpContext.Authentication.SignOutAsync(
    CookieAuthenticationDefaults.AuthenticationScheme);
```

---

<span data-ttu-id="8fc87-329">如果不使用`CookieAuthenticationDefaults.AuthenticationScheme`（或"Cookie"） 作为方案 (例如，"ContosoCookie")，提供配置身份验证提供程序时使用的方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-329">If you aren't using `CookieAuthenticationDefaults.AuthenticationScheme` (or "Cookies") as the scheme (for example, "ContosoCookie"), supply the scheme you used when configuring the authentication provider.</span></span> <span data-ttu-id="8fc87-330">否则，使用默认方案。</span><span class="sxs-lookup"><span data-stu-id="8fc87-330">Otherwise, the default scheme is used.</span></span>

## <a name="react-to-back-end-changes"></a><span data-ttu-id="8fc87-331">对后端更改做出响应</span><span class="sxs-lookup"><span data-stu-id="8fc87-331">React to back-end changes</span></span>

<span data-ttu-id="8fc87-332">一旦创建了 cookie，它将成为标识的单个来源。</span><span class="sxs-lookup"><span data-stu-id="8fc87-332">Once a cookie is created, it becomes the single source of identity.</span></span> <span data-ttu-id="8fc87-333">即使在后端系统中禁用用户，cookie 身份验证系统不了解，并且用户保持登录状态，只要其 cookie 有效。</span><span class="sxs-lookup"><span data-stu-id="8fc87-333">Even if you disable a user in your back-end systems, the cookie authentication system has no knowledge of this, and a user stays logged in as long as their cookie is valid.</span></span>

<span data-ttu-id="8fc87-334">[ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal)中 ASP.NET Core 事件 2.x 或[ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1)中 ASP.NET Core 1.x 可用来截获和重写的 cookie 身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="8fc87-334">The [ValidatePrincipal](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents.validateprincipal) event in ASP.NET Core 2.x or the [ValidateAsync](/dotnet/api/microsoft.aspnetcore.identity.isecuritystampvalidator.validateasync?view=aspnetcore-1.1) method in ASP.NET Core 1.x can be used to intercept and override validation of the cookie identity.</span></span> <span data-ttu-id="8fc87-335">此方法可减轻已吊销的用户访问应用的风险。</span><span class="sxs-lookup"><span data-stu-id="8fc87-335">This approach mitigates the risk of revoked users accessing the app.</span></span>

<span data-ttu-id="8fc87-336">Cookie 验证的一种方法取决于跟踪的更改用户数据库时。</span><span class="sxs-lookup"><span data-stu-id="8fc87-336">One approach to cookie validation is based on keeping track of when the user database has been changed.</span></span> <span data-ttu-id="8fc87-337">如果数据库未已发生更改，因为发布用户的 cookie，则无需重新验证用户，如果其 cookie 仍然有效。</span><span class="sxs-lookup"><span data-stu-id="8fc87-337">If the database hasn't been changed since the user's cookie was issued, there's no need to re-authenticate the user if their cookie is still valid.</span></span> <span data-ttu-id="8fc87-338">若要实现此方案中，数据库中实现`IUserRepository`对于此示例中，存储`LastChanged`值。</span><span class="sxs-lookup"><span data-stu-id="8fc87-338">To implement this scenario, the database, which is implemented in `IUserRepository` for this example, stores a `LastChanged` value.</span></span> <span data-ttu-id="8fc87-339">在数据库中，更新的任何用户时`LastChanged`值设置为当前时间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-339">When any user is updated in the database, the `LastChanged` value is set to the current time.</span></span>

<span data-ttu-id="8fc87-340">为了使 cookie 无效时的数据库更改基于`LastChanged`值时，请创建与 cookie`LastChanged`包含当前声明`LastChanged`值位于数据库中：</span><span class="sxs-lookup"><span data-stu-id="8fc87-340">In order to invalidate a cookie when the database changes based on the `LastChanged` value, create the cookie with a `LastChanged` claim containing the current `LastChanged` value from the database:</span></span>

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

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-341">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-341">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="8fc87-342">若要实现的替代`ValidatePrincipal`事件，编写一个方法具有以下签名在从派生类中[CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span><span class="sxs-lookup"><span data-stu-id="8fc87-342">To implement an override for the `ValidatePrincipal` event, write a method with the following signature in a class that you derive from [CookieAuthenticationEvents](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationevents):</span></span>

```csharp
ValidatePrincipal(CookieValidatePrincipalContext)
```

<span data-ttu-id="8fc87-343">示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fc87-343">An example looks like the following:</span></span>

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

<span data-ttu-id="8fc87-344">在中的 cookie 服务注册期间注册的事件实例`ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="8fc87-344">Register the events instance during cookie service registration in the `ConfigureServices` method.</span></span> <span data-ttu-id="8fc87-345">提供的作用域内的服务注册你`CustomCookieAuthenticationEvents`类：</span><span class="sxs-lookup"><span data-stu-id="8fc87-345">Provide a scoped service registration for your `CustomCookieAuthenticationEvents` class:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
    .AddCookie(options =>
    {
        options.EventsType = typeof(CustomCookieAuthenticationEvents);
    });

services.AddScoped<CustomCookieAuthenticationEvents>();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-346">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-346">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="8fc87-347">若要实现的替代`ValidateAsync`事件，编写一个方法具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="8fc87-347">To implement an override for the `ValidateAsync` event, write a method with the following signature:</span></span>

```csharp
ValidateAsync(CookieValidatePrincipalContext)
```

<span data-ttu-id="8fc87-348">ASP.NET Core 标识作为的一部分实现这一检查其[SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync)。</span><span class="sxs-lookup"><span data-stu-id="8fc87-348">ASP.NET Core Identity implements this check as part of its [SecurityStampValidator](/dotnet/api/microsoft.aspnetcore.identity.securitystampvalidator-1.validateasync).</span></span> <span data-ttu-id="8fc87-349">示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fc87-349">An example looks like the following:</span></span>

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

<span data-ttu-id="8fc87-350">在中的 cookie 身份验证配置期间注册事件`Configure`方法：</span><span class="sxs-lookup"><span data-stu-id="8fc87-350">Register the event during cookie authentication configuration in the `Configure` method:</span></span>

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

<span data-ttu-id="8fc87-351">请考虑在其中更新用户的名称的情况下&mdash;不会影响任何方式的安全决策。</span><span class="sxs-lookup"><span data-stu-id="8fc87-351">Consider a situation in which the user's name is updated &mdash; a decision that doesn't affect security in any way.</span></span> <span data-ttu-id="8fc87-352">如果您需要非破坏性地更新用户主体，请调用`context.ReplacePrincipal`并设置`context.ShouldRenew`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-352">If you want to non-destructively update the user principal, call `context.ReplacePrincipal` and set the `context.ShouldRenew` property to `true`.</span></span>

> [!WARNING]
> <span data-ttu-id="8fc87-353">此处所述的方法上的每个请求触发。</span><span class="sxs-lookup"><span data-stu-id="8fc87-353">The approach described here is triggered on every request.</span></span> <span data-ttu-id="8fc87-354">这可能导致应用程序对较大性能产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="8fc87-354">This can result in a large performance penalty for the app.</span></span>

## <a name="persistent-cookies"></a><span data-ttu-id="8fc87-355">永久 cookie</span><span class="sxs-lookup"><span data-stu-id="8fc87-355">Persistent cookies</span></span>

<span data-ttu-id="8fc87-356">你可能想要在浏览器会话之间持久保存的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8fc87-356">You may want the cookie to persist across browser sessions.</span></span> <span data-ttu-id="8fc87-357">此持久性仅应启用"记住我"复选框为登录名或类似机制在显式用户同意。</span><span class="sxs-lookup"><span data-stu-id="8fc87-357">This persistence should only be enabled with explicit user consent with a "Remember Me" checkbox on login or a similar mechanism.</span></span> 

<span data-ttu-id="8fc87-358">下面的代码段创建的标识和相应可以幸存，但通过浏览器闭包的 cookie。</span><span class="sxs-lookup"><span data-stu-id="8fc87-358">The following code snippet creates an identity and corresponding cookie that survives through browser closures.</span></span> <span data-ttu-id="8fc87-359">遵循以前配置任何滑动过期设置。</span><span class="sxs-lookup"><span data-stu-id="8fc87-359">Any sliding expiration settings previously configured are honored.</span></span> <span data-ttu-id="8fc87-360">如果 cookie 已过期浏览器处于关闭状态时，浏览器中清除 cookie 后重新启动它。</span><span class="sxs-lookup"><span data-stu-id="8fc87-360">If the cookie expires while the browser is closed, the browser clears the cookie once it's restarted.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-361">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-361">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
await HttpContext.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="8fc87-362">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0)类驻留在`Microsoft.AspNetCore.Authentication`命名空间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-362">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.authentication.authenticationproperties?view=aspnetcore-2.0) class resides in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-363">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-363">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
await HttpContext.Authentication.SignInAsync(
    CookieAuthenticationDefaults.AuthenticationScheme,
    new ClaimsPrincipal(claimsIdentity),
    new AuthenticationProperties
    {
        IsPersistent = true
    });
```

<span data-ttu-id="8fc87-364">[AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1)类驻留在`Microsoft.AspNetCore.Http.Authentication`命名空间。</span><span class="sxs-lookup"><span data-stu-id="8fc87-364">The [AuthenticationProperties](/dotnet/api/microsoft.aspnetcore.http.authentication.authenticationproperties?view=aspnetcore-1.1) class resides in the `Microsoft.AspNetCore.Http.Authentication` namespace.</span></span>

---

## <a name="absolute-cookie-expiration"></a><span data-ttu-id="8fc87-365">绝对 cookie 到期时间</span><span class="sxs-lookup"><span data-stu-id="8fc87-365">Absolute cookie expiration</span></span>

<span data-ttu-id="8fc87-366">可以设置使用绝对到期时间`ExpiresUtc`。</span><span class="sxs-lookup"><span data-stu-id="8fc87-366">You can set an absolute expiration time with `ExpiresUtc`.</span></span> <span data-ttu-id="8fc87-367">您还必须设置`IsPersistent`; 否则为`ExpiresUtc`将被忽略，并创建一个单会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="8fc87-367">You must also set `IsPersistent`; otherwise, `ExpiresUtc` is ignored and a single-session cookie is created.</span></span> <span data-ttu-id="8fc87-368">当`ExpiresUtc`上设置`SignInAsync`，它将重写的值`ExpireTimeSpan`的选项`CookieAuthenticationOptions`，如果设置。</span><span class="sxs-lookup"><span data-stu-id="8fc87-368">When `ExpiresUtc` is set on `SignInAsync`, it overrides the value of the `ExpireTimeSpan` option of `CookieAuthenticationOptions`, if set.</span></span>

<span data-ttu-id="8fc87-369">下面的代码段创建的标识和相应的 cookie 的持续时间为 20 分钟。</span><span class="sxs-lookup"><span data-stu-id="8fc87-369">The following code snippet creates an identity and corresponding cookie that lasts for 20 minutes.</span></span> <span data-ttu-id="8fc87-370">这会忽略以前配置的任何滑动过期设置。</span><span class="sxs-lookup"><span data-stu-id="8fc87-370">This ignores any sliding expiration settings previously configured.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8fc87-371">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-371">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8fc87-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8fc87-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

## <a name="additional-resources"></a><span data-ttu-id="8fc87-373">其他资源</span><span class="sxs-lookup"><span data-stu-id="8fc87-373">Additional resources</span></span>

* [<span data-ttu-id="8fc87-374">身份验证 2.0 更改 / 迁移公告</span><span class="sxs-lookup"><span data-stu-id="8fc87-374">Auth 2.0 Changes / Migration Announcement</span></span>](https://github.com/aspnet/Announcements/issues/262)
* <xref:security/authorization/limitingidentitybyscheme>
* <xref:security/authorization/claims>
* [<span data-ttu-id="8fc87-375">基于策略的角色检查</span><span class="sxs-lookup"><span data-stu-id="8fc87-375">Policy-based role checks</span></span>](xref:security/authorization/roles#policy-based-role-checks)
* <xref:host-and-deploy/web-farm>
