---
title: "ASP.NET Core 中的会话和应用程序状态"
author: rick-anderson
description: "保留请求之间的应用程序和用户（会话）状态的方法。"
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 11/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/app-state
ms.openlocfilehash: 7aa200d3612f766ab633ccab807421b9c5393975
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-session-and-application-state-in-aspnet-core"></a><span data-ttu-id="9a323-103">ASP.NET Core 中的会话和应用程序状态简介</span><span class="sxs-lookup"><span data-stu-id="9a323-103">Introduction to session and application state in ASP.NET Core</span></span>

<span data-ttu-id="9a323-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)、[Steve Smith](https://ardalis.com/) 和 [Diana LaRose](https://github.com/DianaLaRose)</span><span class="sxs-lookup"><span data-stu-id="9a323-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), and [Diana LaRose](https://github.com/DianaLaRose)</span></span>

<span data-ttu-id="9a323-105">HTTP 是无状态的协议。</span><span class="sxs-lookup"><span data-stu-id="9a323-105">HTTP is a stateless protocol.</span></span> <span data-ttu-id="9a323-106">Web 服务器将每个 HTTP 请求视为独立的请求，并不会保留以前请求中的用户值。</span><span class="sxs-lookup"><span data-stu-id="9a323-106">A web server treats each HTTP request as an independent request and doesn't retain user values from previous requests.</span></span> <span data-ttu-id="9a323-107">本文讨论保留请求之间的应用程序和会话状态的不同方式。</span><span class="sxs-lookup"><span data-stu-id="9a323-107">This article discusses different ways to preserve application and session state between requests.</span></span> 

## <a name="session-state"></a><span data-ttu-id="9a323-108">会话状态</span><span class="sxs-lookup"><span data-stu-id="9a323-108">Session state</span></span>

<span data-ttu-id="9a323-109">会话状态是 ASP.NET Core 中的一项功能，可用于在用户浏览 Web 应用时保存和存储用户数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-109">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span> <span data-ttu-id="9a323-110">会话状态由服务器上的字典或哈希表组成，在浏览器的请求中保持数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-110">Consisting of a dictionary or hash table on the server, session state persists data across requests from a browser.</span></span> <span data-ttu-id="9a323-111">会话数据由缓存支持。</span><span class="sxs-lookup"><span data-stu-id="9a323-111">The session data is backed by a cache.</span></span>

<span data-ttu-id="9a323-112">ASP.NET Core 通过向客户端提供包含会话 ID 的 Cookie 来维护会话状态，该会话 ID 与每个请求一起发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="9a323-112">ASP.NET Core maintains session state by giving the client a cookie that contains the session ID, which is sent to the server with each request.</span></span> <span data-ttu-id="9a323-113">服务器使用会话 ID 来获取会话数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-113">The server uses the session ID to fetch the session data.</span></span> <span data-ttu-id="9a323-114">因为会话 Cookie 是特定于浏览器的，所以不能跨浏览器中共享会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-114">Because the session cookie is specific to the browser, you cannot share sessions across browsers.</span></span> <span data-ttu-id="9a323-115">仅当浏览器会话结束时才能删除会话 Cookie。</span><span class="sxs-lookup"><span data-stu-id="9a323-115">Session cookies are deleted only when the browser session ends.</span></span> <span data-ttu-id="9a323-116">如果收到过期的会话 Cookie，则创建使用相同会话 Cookie 的新会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-116">If a cookie is received for an expired session, a new session that uses the same session cookie  is created.</span></span> 

<span data-ttu-id="9a323-117">服务器在上次请求后保留会话的时间有限。</span><span class="sxs-lookup"><span data-stu-id="9a323-117">The server retains a session for a limited time after the last request.</span></span> <span data-ttu-id="9a323-118">设置会话超时，或者使用 20 分钟的默认值。</span><span class="sxs-lookup"><span data-stu-id="9a323-118">Either set the session timeout or use the default value of 20 minutes.</span></span> <span data-ttu-id="9a323-119">会话状态非常适合用于存储特定于特定会话但并不需要永久保留的用户数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-119">Session state is ideal for storing user data that's specific to a particular session but doesn't need to be persisted permanently.</span></span> <span data-ttu-id="9a323-120">在调用 `Session.Clear` 时或数据存储中会话到期时将删除后备存储中的数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-120">Data is deleted from the backing store either when calling `Session.Clear` or when the session expires in the data store.</span></span> <span data-ttu-id="9a323-121">服务器不知道关闭浏览器或删除会话 Cookie 的时间。</span><span class="sxs-lookup"><span data-stu-id="9a323-121">The server doesn't know when the browser is closed or when the session cookie is deleted.</span></span>

> [!WARNING]
> <span data-ttu-id="9a323-122">请勿将敏感数据存储在会话中。</span><span class="sxs-lookup"><span data-stu-id="9a323-122">Don't store sensitive data in session.</span></span> <span data-ttu-id="9a323-123">客户端可能不会关闭浏览器并清除会话 Cookie（某些浏览器在多个窗口中保持会话 Cookie）。</span><span class="sxs-lookup"><span data-stu-id="9a323-123">The client might not close the browser and clear the session cookie (and some browsers keep session cookies alive across windows).</span></span> <span data-ttu-id="9a323-124">另外，会话可能不限于单个用户；下一个用户可能继续同一个会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-124">Also, a session might not be restricted to a single user; the next user might continue with the same session.</span></span>

<span data-ttu-id="9a323-125">内存中会话提供程序将会话数据存储在本地服务器上。</span><span class="sxs-lookup"><span data-stu-id="9a323-125">The in-memory session provider stores session data on the local server.</span></span> <span data-ttu-id="9a323-126">如果计划在服务器场上运行 Web 应用，则必须使用粘性会话将每个会话绑定到特定的服务器上。</span><span class="sxs-lookup"><span data-stu-id="9a323-126">If you plan to run your web app on a server farm, you must use sticky sessions to tie each session to a specific server.</span></span> <span data-ttu-id="9a323-127">Microsoft Azure 网站平台默认设置为粘性会话（应用程序请求路由或 ARR）。</span><span class="sxs-lookup"><span data-stu-id="9a323-127">The Windows Azure Web Sites platform defaults to sticky sessions (Application Request Routing or ARR).</span></span> <span data-ttu-id="9a323-128">然而，粘性会话可能会影响可伸缩性，并使 Web 应用更新变得复杂。</span><span class="sxs-lookup"><span data-stu-id="9a323-128">However, sticky sessions can affect scalability and complicate web app updates.</span></span> <span data-ttu-id="9a323-129">更好的选择是使用 Redis 或 SQL Server 分布式缓存，它们不需要粘性会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-129">A better option is to use the Redis or SQL Server distributed caches, which don't require sticky sessions.</span></span> <span data-ttu-id="9a323-130">有关详细信息，请参阅[使用分布式缓存](xref:performance/caching/distributed)。</span><span class="sxs-lookup"><span data-stu-id="9a323-130">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed).</span></span> <span data-ttu-id="9a323-131">有关服务提供程序设置的详细信息，请参阅本文后续部分中的[配置会话](#configuring-session)。</span><span class="sxs-lookup"><span data-stu-id="9a323-131">For details on setting up service providers, see [Configuring Session](#configuring-session) later in this article.</span></span>

<a name="temp"></a>
## <a name="tempdata"></a><span data-ttu-id="9a323-132">TempData</span><span class="sxs-lookup"><span data-stu-id="9a323-132">TempData</span></span>

<span data-ttu-id="9a323-133">ASP.NET Core MVC 在[控制器](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0)上公开了 [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 属性。</span><span class="sxs-lookup"><span data-stu-id="9a323-133">ASP.NET Core MVC exposes the [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0).</span></span> <span data-ttu-id="9a323-134">此属性存储未读取的数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-134">This property stores data until it's read.</span></span> <span data-ttu-id="9a323-135">`Keep` 和 `Peek` 方法可用于检查数据，而不执行删除。</span><span class="sxs-lookup"><span data-stu-id="9a323-135">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="9a323-136">多个请求需要数据时，`TempData` 非常有助于进行重定向。</span><span class="sxs-lookup"><span data-stu-id="9a323-136">`TempData` is particularly useful for redirection, when data is needed for more than a single request.</span></span> <span data-ttu-id="9a323-137">通过 TempData 提供程序实现 `TempData`，例如，使用 Cookie 或会话状态。</span><span class="sxs-lookup"><span data-stu-id="9a323-137">`TempData` is implemented by TempData providers, for example, using either cookies or session state.</span></span>

<a name="tempdata-providers"></a>
### <a name="tempdata-providers"></a><span data-ttu-id="9a323-138">TempData 提供程序</span><span class="sxs-lookup"><span data-stu-id="9a323-138">TempData providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9a323-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9a323-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9a323-140">ASP.NET Core 2.0 及更高版本中，基于 Cookie 的 TempData 提供程序在默认情况下使用，将 TempData 存储在 Cookie 中。</span><span class="sxs-lookup"><span data-stu-id="9a323-140">In ASP.NET Core 2.0 and later, the cookie-based TempData provider is used by default to store TempData in cookies.</span></span>

<span data-ttu-id="9a323-141">使用 [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0) 对 Cookie 数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="9a323-141">The cookie data is encoded with the [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0).</span></span> <span data-ttu-id="9a323-142">因为 Cookie 被加密并分块，所以 ASP.NET Core 1.x 中的单个 Cookie 大小限制不适用。</span><span class="sxs-lookup"><span data-stu-id="9a323-142">Because the cookie is encrypted and chunked, the single cookie size limit found in ASP.NET Core 1.x does not apply.</span></span> <span data-ttu-id="9a323-143">未压缩 Cookie 数据，因为压缩加密的数据会导致安全问题，如 [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) 和 [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) 攻击。</span><span class="sxs-lookup"><span data-stu-id="9a323-143">The cookie data is not compressed because compressing encrypted data can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span> <span data-ttu-id="9a323-144">有关基于 Cookie 的 TempData 提供程序的详细信息，请参阅 [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs)。</span><span class="sxs-lookup"><span data-stu-id="9a323-144">For more information on the cookie-based TempData provider, see [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9a323-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9a323-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9a323-146">在 ASP.NET Core 1.0 和 1.1 中，会话状态 TempData 提供程序是默认值。</span><span class="sxs-lookup"><span data-stu-id="9a323-146">In ASP.NET Core 1.0 and 1.1, the session state TempData provider is the default.</span></span>

--------------

<a name="choose-temp"></a>
### <a name="choosing-a-tempdata-provider"></a><span data-ttu-id="9a323-147">选择 TempData 提供程序</span><span class="sxs-lookup"><span data-stu-id="9a323-147">Choosing a TempData provider</span></span>

<span data-ttu-id="9a323-148">选择 TempData 提供程序涉及几个注意事项，例如：</span><span class="sxs-lookup"><span data-stu-id="9a323-148">Choosing a TempData provider involves several considerations, such as:</span></span>

1. <span data-ttu-id="9a323-149">应用程序是否已经将会话状态用于其他目的？</span><span class="sxs-lookup"><span data-stu-id="9a323-149">Does the application already use session state for other purposes?</span></span> <span data-ttu-id="9a323-150">如果是，使用会话状态 TempData 提供程序对应用程序没有额外的成本（除了数据的大小）。</span><span class="sxs-lookup"><span data-stu-id="9a323-150">If so, using the session state TempData provider has no additional cost to the application (aside from the size of the data).</span></span>
2. <span data-ttu-id="9a323-151">应用程序是否只对相对较小的数据量（最多 500 个字节）使用 TempData？</span><span class="sxs-lookup"><span data-stu-id="9a323-151">Does the application use TempData only sparingly, for relatively small amounts of data (up to 500 bytes)?</span></span> <span data-ttu-id="9a323-152">如果是，Cookie TempData 提供程序将为每个携带 TempData 的请求增加较小的成本。</span><span class="sxs-lookup"><span data-stu-id="9a323-152">If so, the cookie TempData provider will add a small cost to each request that carries TempData.</span></span> <span data-ttu-id="9a323-153">如果不是，会话状态 TempData 提供程序有助于在使用 TempData 前，避免在每个请求中来回切换大量数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-153">If not, the session state TempData provider can be beneficial to avoid round-tripping a large amount of data in each request until the TempData is consumed.</span></span>
3. <span data-ttu-id="9a323-154">应用程序是否在 Web 场（多个服务器）中运行？</span><span class="sxs-lookup"><span data-stu-id="9a323-154">Does the application run in a web farm (multiple servers)?</span></span> <span data-ttu-id="9a323-155">如果是，则使用 Cookie TempData 提供程序无需额外配置。</span><span class="sxs-lookup"><span data-stu-id="9a323-155">If so, there's no additional configuration needed to use the cookie TempData provider.</span></span>

> [!NOTE]
> <span data-ttu-id="9a323-156">大多数 Web 客户端（如 Web 浏览器）针对每个 Cookie 的最大大小和/或 Cookie 总数强制实施限制。</span><span class="sxs-lookup"><span data-stu-id="9a323-156">Most web clients (such as web browsers) enforce limits on the maximum size of each cookie, the total number of cookies, or both.</span></span> <span data-ttu-id="9a323-157">因此，使用 Cookie TempData 提供程序时，请验证应用程序未超过这些限制。</span><span class="sxs-lookup"><span data-stu-id="9a323-157">Therefore, when using the cookie TempData provider, verify the app won't exceed these limits.</span></span> <span data-ttu-id="9a323-158">请考虑数据的总大小，将加密和分块的开销考虑在内。</span><span class="sxs-lookup"><span data-stu-id="9a323-158">Consider the total size of the data, accounting for the overheads of encryption and chunking.</span></span>

<a name="config-temp"></a>
### <a name="configure-the-tempdata-provider"></a><span data-ttu-id="9a323-159">配置 TempData 提供程序</span><span class="sxs-lookup"><span data-stu-id="9a323-159">Configure the TempData provider</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9a323-160">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9a323-160">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9a323-161">默认情况下启用基于 Cookie 的 TempData 提供程序。</span><span class="sxs-lookup"><span data-stu-id="9a323-161">The cookie-based TempData provider is enabled by default.</span></span> <span data-ttu-id="9a323-162">以下 `Startup` 类代码配置基于会话的 TempData 提供程序：</span><span class="sxs-lookup"><span data-stu-id="9a323-162">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,6,11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9a323-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9a323-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9a323-164">以下 `Startup` 类代码配置基于会话的 TempData 提供程序：</span><span class="sxs-lookup"><span data-stu-id="9a323-164">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSession/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,9)]

---

<span data-ttu-id="9a323-165">排序对于中间件组件至关重要。</span><span class="sxs-lookup"><span data-stu-id="9a323-165">Ordering is critical for middleware components.</span></span> <span data-ttu-id="9a323-166">在前面的示例中，在 `UseMvcWithDefaultRoute` 之后调用 `UseSession` 时会发生 `InvalidOperationException` 类型的异常。</span><span class="sxs-lookup"><span data-stu-id="9a323-166">In the preceding example, an exception of type `InvalidOperationException` occurs when `UseSession` is invoked after `UseMvcWithDefaultRoute`.</span></span> <span data-ttu-id="9a323-167">有关详细信息，请参阅[中间件排序](xref:fundamentals/middleware#ordering)。</span><span class="sxs-lookup"><span data-stu-id="9a323-167">See [Middleware Ordering](xref:fundamentals/middleware#ordering) for more detail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a323-168">如果面向 .NET Framework 和使用基于会话的提供程序，将 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet 包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="9a323-168">If targeting .NET Framework and using the session-based provider, add the [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet package to your project.</span></span>

## <a name="query-strings"></a><span data-ttu-id="9a323-169">查询字符串</span><span class="sxs-lookup"><span data-stu-id="9a323-169">Query strings</span></span>

<span data-ttu-id="9a323-170">可以将有限的数据从一个请求传递到另一个请求，方法是将其添加到新请求的查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="9a323-170">You can pass a limited amount of data from one request to another by adding it to the new request's query string.</span></span> <span data-ttu-id="9a323-171">这有利于以一种持久的方式捕获状态，这种方式允许通过电子邮件或社交网络共享嵌入式状态的链接。</span><span class="sxs-lookup"><span data-stu-id="9a323-171">This is useful for capturing state in a persistent manner that allows links with embedded state to be shared through email or social networks.</span></span> <span data-ttu-id="9a323-172">但是，为此，不可将查询字符串用于敏感数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-172">However, for this reason, you should never use query strings for sensitive data.</span></span> <span data-ttu-id="9a323-173">在查询字符串中包含数据除了易于共享，还为[跨站点请求伪造 (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 攻击创造了机会，可以欺骗用户在通过身份验证时访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="9a323-173">In addition to being easily shared, including data in query strings can create opportunities for [Cross-Site Request Forgery (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) attacks, which can trick users into visiting malicious sites while authenticated.</span></span> <span data-ttu-id="9a323-174">然后，攻击者可以从应用程序中窃取用户数据，或者代表用户采取恶意操作。</span><span class="sxs-lookup"><span data-stu-id="9a323-174">Attackers can then steal user data from your app or take malicious actions on behalf of the user.</span></span> <span data-ttu-id="9a323-175">任何保留的应用程序或会话状态必须防止 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="9a323-175">Any preserved application or session state must protect against CSRF attacks.</span></span> <span data-ttu-id="9a323-176">有关 CSRF 攻击的详细信息，请参阅[在 ASP.NET Core 中预防跨网站请求伪造 (XSRF/CSRF) 攻击](../security/anti-request-forgery.md)。</span><span class="sxs-lookup"><span data-stu-id="9a323-176">For more information on CSRF attacks, see [Preventing Cross-Site Request Forgery (XSRF/CSRF) Attacks in ASP.NET Core](../security/anti-request-forgery.md).</span></span>

## <a name="post-data-and-hidden-fields"></a><span data-ttu-id="9a323-177">后期数据和隐藏字段</span><span class="sxs-lookup"><span data-stu-id="9a323-177">Post data and hidden fields</span></span>

<span data-ttu-id="9a323-178">数据可以保存在隐藏的表单域中，并在下一个请求上回发。</span><span class="sxs-lookup"><span data-stu-id="9a323-178">Data can be saved in hidden form fields and posted back on the next request.</span></span> <span data-ttu-id="9a323-179">这在多页窗体中很常见。</span><span class="sxs-lookup"><span data-stu-id="9a323-179">This is common in multi-page forms.</span></span> <span data-ttu-id="9a323-180">但是，由于客户端可能会篡改数据，因此服务器必须始终重新验证数据。</span><span class="sxs-lookup"><span data-stu-id="9a323-180">However, because the client can potentially tamper with the data, the server must always revalidate it.</span></span> 

## <a name="cookies"></a><span data-ttu-id="9a323-181">Cookie</span><span class="sxs-lookup"><span data-stu-id="9a323-181">Cookies</span></span>

<span data-ttu-id="9a323-182">Cookie 提供了一种在 Web 应用程序中存储用户特定数据的方法。</span><span class="sxs-lookup"><span data-stu-id="9a323-182">Cookies provide a way to store user-specific data in web applications.</span></span> <span data-ttu-id="9a323-183">因为 Cookie 是随每个请求发送的，所以它们的大小应该保持在最低限度。</span><span class="sxs-lookup"><span data-stu-id="9a323-183">Because cookies are sent with every request, their size should be kept to a minimum.</span></span> <span data-ttu-id="9a323-184">理想情况下，仅标识符应存储在 Cookie 中，而实际数据存储在服务器上。</span><span class="sxs-lookup"><span data-stu-id="9a323-184">Ideally, only an identifier should be stored in a cookie with the actual data stored on the server.</span></span> <span data-ttu-id="9a323-185">大多数浏览器将 Cookie 限制为 4096 个字节。</span><span class="sxs-lookup"><span data-stu-id="9a323-185">Most browsers restrict cookies to 4096 bytes.</span></span> <span data-ttu-id="9a323-186">此外，每个域仅有有限数量的 Cookie 可用。</span><span class="sxs-lookup"><span data-stu-id="9a323-186">In addition, only a limited number of cookies are available for each domain.</span></span>  

<span data-ttu-id="9a323-187">因为 Cookie 易被篡改，所以它们必须在服务器上进行验证。</span><span class="sxs-lookup"><span data-stu-id="9a323-187">Because cookies are subject to tampering, they must be validated on the server.</span></span> <span data-ttu-id="9a323-188">尽管在客户端的 Cookie 的持续性是受用户干预并到期，但它们通常是客户端上最持久的数据持久形式。</span><span class="sxs-lookup"><span data-stu-id="9a323-188">Although the durability of the cookie on a client is subject to user intervention and expiration, they're generally the most durable form of data persistence on the client.</span></span>

<span data-ttu-id="9a323-189">Cookie 通常用于个性化设置，其中的内容是为已知用户定制的。</span><span class="sxs-lookup"><span data-stu-id="9a323-189">Cookies are often used for personalization, where content is customized for a known user.</span></span> <span data-ttu-id="9a323-190">因为在大多数情况下，用户仅被标识且未经过身份验证，所以通常可以通过在 Cookie 中存储用户名、帐户名或唯一用户 ID（例如 GUID）来保护 Cookie。</span><span class="sxs-lookup"><span data-stu-id="9a323-190">Because the user is only identified and not authenticated in most cases, you can typically secure a cookie by storing the user name, account name, or a unique user ID (such as a GUID) in the cookie.</span></span> <span data-ttu-id="9a323-191">然后可以使用 Cookie 来访问站点的用户个性化设置基础结构。</span><span class="sxs-lookup"><span data-stu-id="9a323-191">You can then use the cookie to access the user personalization infrastructure of a site.</span></span>

## <a name="httpcontextitems"></a><span data-ttu-id="9a323-192">HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="9a323-192">HttpContext.Items</span></span>

<span data-ttu-id="9a323-193">`Items` 集合是存储仅在处理一个特定请求时才需要的数据的理想位置。</span><span class="sxs-lookup"><span data-stu-id="9a323-193">The `Items` collection is a good location to store data that's needed only while processing one particular request.</span></span> <span data-ttu-id="9a323-194">集合的内容在每次请求后被放弃。</span><span class="sxs-lookup"><span data-stu-id="9a323-194">The collection's contents are discarded after each request.</span></span> <span data-ttu-id="9a323-195">`Items` 集合最好用作组件或中间件在请求期间在不同时间点操作且没有直接传递参数的方法时进行通信的方式。</span><span class="sxs-lookup"><span data-stu-id="9a323-195">The `Items` collection is best used as a way for components or middleware to communicate when they operate at different points in time during a request and have no direct way to pass parameters.</span></span> <span data-ttu-id="9a323-196">有关详细信息，请参阅本文后面的[使用 HttpContext.Items](#working-with-httpcontextitems)。</span><span class="sxs-lookup"><span data-stu-id="9a323-196">For more information, see [Working with HttpContext.Items](#working-with-httpcontextitems), later in this article.</span></span>

## <a name="cache"></a><span data-ttu-id="9a323-197">缓存</span><span class="sxs-lookup"><span data-stu-id="9a323-197">Cache</span></span>

<span data-ttu-id="9a323-198">缓存是存储和检索数据的有效方法。</span><span class="sxs-lookup"><span data-stu-id="9a323-198">Caching is an efficient way to store and retrieve data.</span></span> <span data-ttu-id="9a323-199">可以根据时间和其他注意事项控制缓存项的生存期。</span><span class="sxs-lookup"><span data-stu-id="9a323-199">You can control the lifetime of cached items based on time and other considerations.</span></span> <span data-ttu-id="9a323-200">了解有关 [缓存](../performance/caching/index.md)的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9a323-200">Learn more about [Caching](../performance/caching/index.md).</span></span>

<a name="session"></a>
## <a name="working-with-session-state"></a><span data-ttu-id="9a323-201">使用会话状态</span><span class="sxs-lookup"><span data-stu-id="9a323-201">Working with Session State</span></span>

### <a name="configuring-session"></a><span data-ttu-id="9a323-202">配置会话</span><span class="sxs-lookup"><span data-stu-id="9a323-202">Configuring Session</span></span>

<span data-ttu-id="9a323-203">`Microsoft.AspNetCore.Session` 包提供用于管理会话状态的中间件。</span><span class="sxs-lookup"><span data-stu-id="9a323-203">The `Microsoft.AspNetCore.Session` package provides middleware for managing session state.</span></span> <span data-ttu-id="9a323-204">若要启用会话中间件，`Startup` 必须包含：</span><span class="sxs-lookup"><span data-stu-id="9a323-204">To enable the session middleware, `Startup` must contain:</span></span>

- <span data-ttu-id="9a323-205">任一 [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 内存缓存。</span><span class="sxs-lookup"><span data-stu-id="9a323-205">Any of the [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) memory caches.</span></span> <span data-ttu-id="9a323-206">`IDistributedCache` 实现用作会话后备存储。</span><span class="sxs-lookup"><span data-stu-id="9a323-206">The `IDistributedCache` implementation is used as a backing store for session.</span></span>
- <span data-ttu-id="9a323-207">[AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 调用，要求 NuGet 包“Microsoft.AspNetCore.Session”。</span><span class="sxs-lookup"><span data-stu-id="9a323-207">[AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) call, which requires NuGet package "Microsoft.AspNetCore.Session".</span></span>
- <span data-ttu-id="9a323-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) 调用。</span><span class="sxs-lookup"><span data-stu-id="9a323-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) call.</span></span>

<span data-ttu-id="9a323-209">下面的代码演示如何设置内存中的会话提供程序。</span><span class="sxs-lookup"><span data-stu-id="9a323-209">The following code shows how to set up the in-memory session provider.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9a323-210">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9a323-210">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/Startup.cs?highlight=11-19,24)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9a323-211">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9a323-211">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/Startup.cs?highlight=11-19,24)]

---

<span data-ttu-id="9a323-212">一旦 `HttpContext` 安装并配置，可以从它引用会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-212">You can reference Session from `HttpContext` once it's installed and configured.</span></span>

<span data-ttu-id="9a323-213">如果在 `UseSession` 被调用前尝试访问 `Session`，将引发异常 `InvalidOperationException: Session has not been configured for this application or request`。</span><span class="sxs-lookup"><span data-stu-id="9a323-213">If you try to access `Session` before `UseSession` has been called, the exception `InvalidOperationException: Session has not been configured for this application or request` is thrown.</span></span>

<span data-ttu-id="9a323-214">如果在已经开始写入 `Response` 流后尝试创建一个新 `Session`（即，未创建会话 Cookie），将引发异常 `InvalidOperationException: The session cannot be established after the response has started`。</span><span class="sxs-lookup"><span data-stu-id="9a323-214">If you try to create a new `Session` (that is, no session cookie has been created) after you have already begun writing to the `Response` stream, the exception `InvalidOperationException: The session cannot be established after the response has started` is thrown.</span></span> <span data-ttu-id="9a323-215">此异常可在 Web 服务器日志中找到；它将不会在浏览器中显示。</span><span class="sxs-lookup"><span data-stu-id="9a323-215">The exception can be found in the web server log; it will not be displayed in the browser.</span></span>

### <a name="loading-session-asynchronously"></a><span data-ttu-id="9a323-216">以异步方式加载会话</span><span class="sxs-lookup"><span data-stu-id="9a323-216">Loading Session asynchronously</span></span> 

<span data-ttu-id="9a323-217">只有在 `TryGetValue`、`Set` 或 `Remove` 方法之前显式调用 [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) 方法，ASP.NET Core 中的默认会话提供程序才会从基础 [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 存储以异步方式加载会话记录。</span><span class="sxs-lookup"><span data-stu-id="9a323-217">The default session provider in ASP.NET Core loads the session record from the underlying [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) store asynchronously only if the [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) method is explicitly called before  the `TryGetValue`, `Set`, or `Remove` methods.</span></span> <span data-ttu-id="9a323-218">如果不首先调用 `LoadAsync`，基础会话记录以同步方式加载，这可能影响应用的扩展能力。</span><span class="sxs-lookup"><span data-stu-id="9a323-218">If `LoadAsync` isn't called first, the underlying session record is loaded synchronously, which could potentially impact the ability of the app to scale.</span></span>

<span data-ttu-id="9a323-219">若要让应用程序强制实施此模式，如果未在`TryGetValue`、`Set` 或 `Remove`之前调用 `LoadAsync` 方法，将 [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) 和 [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession)实现包装在引起异常的版本。</span><span class="sxs-lookup"><span data-stu-id="9a323-219">To have applications enforce this pattern, wrap the [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) and [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession) implementations with versions that throw an exception if the `LoadAsync` method isn't called before `TryGetValue`, `Set`, or `Remove`.</span></span> <span data-ttu-id="9a323-220">在服务容器中注册的已包装的版本。</span><span class="sxs-lookup"><span data-stu-id="9a323-220">Register the wrapped versions in the services container.</span></span>

### <a name="implementation-details"></a><span data-ttu-id="9a323-221">实现的详细信息</span><span class="sxs-lookup"><span data-stu-id="9a323-221">Implementation details</span></span>

<span data-ttu-id="9a323-222">会话使用 Cookie 跟踪和标识来自单个浏览器的请求。</span><span class="sxs-lookup"><span data-stu-id="9a323-222">Session uses a cookie to track and identify requests from a single browser.</span></span> <span data-ttu-id="9a323-223">默认情况下，此 Cookie 名为“.AspNet.Session”，并使用路径“/”。</span><span class="sxs-lookup"><span data-stu-id="9a323-223">By default, this cookie is named ".AspNet.Session", and it uses a path of "/".</span></span> <span data-ttu-id="9a323-224">因为 Cookie 默认值不指定域，所以它不提供页上的客户端脚本（因为 `CookieHttpOnly` 默认为 `true`）。</span><span class="sxs-lookup"><span data-stu-id="9a323-224">Because the cookie default doesn't specify a domain, it's not made available to the client-side script on the page (because `CookieHttpOnly` defaults to `true`).</span></span>

<span data-ttu-id="9a323-225">若要重写会话默认值，使用 `SessionOptions`：</span><span class="sxs-lookup"><span data-stu-id="9a323-225">To override session defaults, use `SessionOptions`:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9a323-226">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9a323-226">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupCopy.cs?name=snippet1&highlight=8-12)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9a323-227">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9a323-227">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/StartupCopy.cs?name=snippet1&highlight=8-12)]

---

<span data-ttu-id="9a323-228">服务器使用 `IdleTimeout` 属性来确定在放弃会话内容之前可以保持空闲的时间长短。</span><span class="sxs-lookup"><span data-stu-id="9a323-228">The server uses the `IdleTimeout` property to determine how long a session can be idle before its contents are abandoned.</span></span> <span data-ttu-id="9a323-229">此属性独立于 Cookie 到期时间。</span><span class="sxs-lookup"><span data-stu-id="9a323-229">This property is independent of the cookie expiration.</span></span> <span data-ttu-id="9a323-230">通过会话中间件（从会话中间件读取或写入）传递每个请求都会重置超时。</span><span class="sxs-lookup"><span data-stu-id="9a323-230">Each request that passes through the Session middleware (read from or written to) resets the timeout.</span></span>

<span data-ttu-id="9a323-231">因为 `Session` 是非锁定的，如果两个请求都试图修改会话内容，最后一个内容会重写第一个内容。</span><span class="sxs-lookup"><span data-stu-id="9a323-231">Because `Session` is *non-locking*, if two requests both attempt to modify the contents of session, the last one overrides the first.</span></span> <span data-ttu-id="9a323-232">`Session` 是作为一个连贯会话实现的，这意味着所有内容都存储在一起。</span><span class="sxs-lookup"><span data-stu-id="9a323-232">`Session` is implemented as a *coherent session*, which means that all the contents are stored together.</span></span> <span data-ttu-id="9a323-233">正在修改会话的不同部分（不同键）的两个请求仍可能会相互影响。</span><span class="sxs-lookup"><span data-stu-id="9a323-233">Two requests that are modifying different parts of the session (different keys) might still impact each other.</span></span>

### <a name="setting-and-getting-session-values"></a><span data-ttu-id="9a323-234">设置和获取会话值</span><span class="sxs-lookup"><span data-stu-id="9a323-234">Setting and getting Session values</span></span>

<span data-ttu-id="9a323-235">通过 `HttpContext` 的 `Session` 属性访问会话。</span><span class="sxs-lookup"><span data-stu-id="9a323-235">Session is accessed through the `Session` property on `HttpContext`.</span></span> <span data-ttu-id="9a323-236">此属性是 [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) 实现。</span><span class="sxs-lookup"><span data-stu-id="9a323-236">This property is an [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) implementation.</span></span>

<span data-ttu-id="9a323-237">下面的示例演示了设置和获取 int 和字符串：</span><span class="sxs-lookup"><span data-stu-id="9a323-237">The following example shows setting and getting an int and a string:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?range=8-27,49)]

<span data-ttu-id="9a323-238">如果添加以下扩展方法，可以设置并获取可序列化的对象到会话：</span><span class="sxs-lookup"><span data-stu-id="9a323-238">If you add the following extension methods, you can set and get serializable objects to Session:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Extensions/SessionExtensions.cs)]

<span data-ttu-id="9a323-239">下面的示例演示如何设置和获取可序列化的对象：</span><span class="sxs-lookup"><span data-stu-id="9a323-239">The following sample shows how to set and get a serializable object:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?name=snippet2)]


## <a name="working-with-httpcontextitems"></a><span data-ttu-id="9a323-240">使用 HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="9a323-240">Working with HttpContext.Items</span></span>

<span data-ttu-id="9a323-241">`HttpContext` 抽象为名为 `Items` 的 `IDictionary<object, object>` 类型字典集合提供支持。</span><span class="sxs-lookup"><span data-stu-id="9a323-241">The `HttpContext` abstraction provides support for a dictionary collection of type `IDictionary<object, object>`, called `Items`.</span></span> <span data-ttu-id="9a323-242">此集合在 HttpRequest 开始时可用并在每个请求的末尾被放弃。</span><span class="sxs-lookup"><span data-stu-id="9a323-242">This collection is available from the start of an *HttpRequest* and is discarded at the end of each request.</span></span> <span data-ttu-id="9a323-243">可以通过给键控的项分配值或为特定键请求值来访问它。</span><span class="sxs-lookup"><span data-stu-id="9a323-243">You can access it by  assigning a value to a keyed entry, or by requesting the value for a particular key.</span></span>

<span data-ttu-id="9a323-244">在下面示例中，[中间件](middleware.md)添加 `isVerified` 到 `Items` 集合。</span><span class="sxs-lookup"><span data-stu-id="9a323-244">In the sample below, [Middleware](middleware.md) adds `isVerified` to the `Items` collection.</span></span>

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

<span data-ttu-id="9a323-245">在更高版本的管道中，另一个中间件无法访问它：</span><span class="sxs-lookup"><span data-stu-id="9a323-245">Later in the pipeline, another middleware could access it:</span></span>

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Verified request? " + 
        context.Items["isVerified"]);
});
```

<span data-ttu-id="9a323-246">对于只供单个应用程序使用的中间件，`string` 键是可以接受的。</span><span class="sxs-lookup"><span data-stu-id="9a323-246">For middleware that will only be used by a single app, `string` keys are acceptable.</span></span> <span data-ttu-id="9a323-247">但是，应用程序之间共享的中间件应使用唯一的对象键以避免键冲突的可能性。</span><span class="sxs-lookup"><span data-stu-id="9a323-247">However, middleware that will be shared between applications should use unique object keys to avoid any chance of key collisions.</span></span> <span data-ttu-id="9a323-248">如果正在开发必须跨多个应用程序工作的中间件，使用中间件类中定义的唯一对象键，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a323-248">If you are developing middleware that must work across multiple applications, use a unique object key defined in your middleware class as shown below:</span></span>

```csharp
public class SampleMiddleware
{
    public static readonly object SampleKey = new Object();

    public async Task Invoke(HttpContext httpContext)
    {
        httpContext.Items[SampleKey] = "some value";
        // additional code omitted
    }
}
```

<span data-ttu-id="9a323-249">其他代码可以使用通过中间件类公开的键访问存储在 `HttpContext.Items` 中的值：</span><span class="sxs-lookup"><span data-stu-id="9a323-249">Other code can access the value stored in `HttpContext.Items` using the key exposed by the middleware class:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        string value = HttpContext.Items[SampleMiddleware.SampleKey];
    }
}
```

<span data-ttu-id="9a323-250">这种方法还具有消除代码中多个位置重复使用“神奇字符串”的优点。</span><span class="sxs-lookup"><span data-stu-id="9a323-250">This approach also has the advantage of eliminating repetition of "magic strings" in multiple places in the code.</span></span>

<a name="appstate-errors"></a>

## <a name="application-state-data"></a><span data-ttu-id="9a323-251">应用程序状态数据</span><span class="sxs-lookup"><span data-stu-id="9a323-251">Application state data</span></span>

<span data-ttu-id="9a323-252">使用[依赖关系注入](xref:fundamentals/dependency-injection)可向所有用户提供数据：</span><span class="sxs-lookup"><span data-stu-id="9a323-252">Use [Dependency Injection](xref:fundamentals/dependency-injection) to make data available to all users:</span></span>

1. <span data-ttu-id="9a323-253">定义包含数据的服务（例如，一个名为 `MyAppData` 的类）。</span><span class="sxs-lookup"><span data-stu-id="9a323-253">Define a service containing the data (for example, a class named `MyAppData`).</span></span>

```csharp
public class MyAppData
{
    // Declare properties/methods/etc.
} 
```
2. <span data-ttu-id="9a323-254">添加服务类到 `ConfigureServices`（例如 `services.AddSingleton<MyAppData>();`）。</span><span class="sxs-lookup"><span data-stu-id="9a323-254">Add the service class to `ConfigureServices` (for example `services.AddSingleton<MyAppData>();`).</span></span>
3. <span data-ttu-id="9a323-255">使用每个控制器中的数据服务类：</span><span class="sxs-lookup"><span data-stu-id="9a323-255">Consume the data service class in each controller:</span></span>

```csharp
public class MyController : Controller
{
    public MyController(MyAppData myService)
    {
        // Do something with the service (read some data from it, 
        // store it in a private field/property, etc.)
    }
} 
```

## <a name="common-errors-when-working-with-session"></a><span data-ttu-id="9a323-256">使用会话时的常见错误</span><span class="sxs-lookup"><span data-stu-id="9a323-256">Common errors when working with session</span></span>

* <span data-ttu-id="9a323-257">“在尝试激活‘Microsoft.AspNetCore.Session.DistributedSessionStore’时无法为类型‘Microsoft.Extensions.Caching.Distributed.IDistributedCache’解析服务。”</span><span class="sxs-lookup"><span data-stu-id="9a323-257">"Unable to resolve service for type 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' while attempting to activate 'Microsoft.AspNetCore.Session.DistributedSessionStore'."</span></span>

  <span data-ttu-id="9a323-258">这通常是由于不能配置至少一个 `IDistributedCache` 实现而造成的。</span><span class="sxs-lookup"><span data-stu-id="9a323-258">This is usually caused by failing to configure at least one `IDistributedCache` implementation.</span></span> <span data-ttu-id="9a323-259">有关详细信息，请参阅[使用分布式缓存](xref:performance/caching/distributed)和[内存缓存中](xref:performance/caching/memory)。</span><span class="sxs-lookup"><span data-stu-id="9a323-259">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed) and [In memory caching](xref:performance/caching/memory).</span></span>

* <span data-ttu-id="9a323-260">如果会话中间件无法保留会话（例如：如果数据库不可用），它将记录并吞并异常。</span><span class="sxs-lookup"><span data-stu-id="9a323-260">In the event that the session middleware fails to persist a session (for example: if the database isn't available), it logs the exception and swallows it.</span></span> <span data-ttu-id="9a323-261">然后，请求将继续正常运行，这会导致非常难以预料的行为。</span><span class="sxs-lookup"><span data-stu-id="9a323-261">The request will then continue normally, which leads to very unpredictable behavior.</span></span>

<span data-ttu-id="9a323-262">典型示例：</span><span class="sxs-lookup"><span data-stu-id="9a323-262">A typical example:</span></span>

<span data-ttu-id="9a323-263">有人将购物篮存储在会话中。</span><span class="sxs-lookup"><span data-stu-id="9a323-263">Someone stores a shopping basket in session.</span></span> <span data-ttu-id="9a323-264">用户添加项但提交失败。</span><span class="sxs-lookup"><span data-stu-id="9a323-264">The user adds an item but the commit fails.</span></span> <span data-ttu-id="9a323-265">应用不知道失败，因此报告消息“已添加项”，然而并不是如此。</span><span class="sxs-lookup"><span data-stu-id="9a323-265">The app doesn't know about the failure so it reports the message "The item has been added", which isn't true.</span></span>

<span data-ttu-id="9a323-266">检查是否存在此类错误的建议方法是完成写入到该会话后从应用代码调用 `await feature.Session.CommitAsync();`。</span><span class="sxs-lookup"><span data-stu-id="9a323-266">The recommended way to check for such errors is to call `await feature.Session.CommitAsync();` from app code when you're done writing to the session.</span></span> <span data-ttu-id="9a323-267">然后就可以随意处理错误。</span><span class="sxs-lookup"><span data-stu-id="9a323-267">Then you can do what you like with the error.</span></span> <span data-ttu-id="9a323-268">调用 `LoadAsync` 时同样适用。</span><span class="sxs-lookup"><span data-stu-id="9a323-268">It works the same way when calling `LoadAsync`.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="9a323-269">其他资源</span><span class="sxs-lookup"><span data-stu-id="9a323-269">Additional resources</span></span>

* [<span data-ttu-id="9a323-270">ASP.NET Core 1.x：本文档中使用的代码示例</span><span class="sxs-lookup"><span data-stu-id="9a323-270">ASP.NET Core 1.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSession)
* [<span data-ttu-id="9a323-271">ASP.NET Core 2.x：本文档中使用的代码示例</span><span class="sxs-lookup"><span data-stu-id="9a323-271">ASP.NET Core 2.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSessionDotNetCore2.0App)
