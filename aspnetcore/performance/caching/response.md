---
title: 响应缓存在 ASP.NET Core
author: rick-anderson
description: 了解如何使用缓存到较低带宽要求的响应，并增加的 ASP.NET Core 应用的性能。
ms.author: riande
ms.date: 09/20/2017
uid: performance/caching/response
ms.openlocfilehash: 4bf61502738d70760679ec98c8f2f303eca9d504
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477484"
---
# <a name="response-caching-in-aspnet-core"></a><span data-ttu-id="94425-103">响应缓存在 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="94425-103">Response caching in ASP.NET Core</span></span>

<span data-ttu-id="94425-104">通过[John 卢奥语](https://github.com/JunTaoLuo)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Steve Smith](https://ardalis.com/)，和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="94425-104">By [John Luo](https://github.com/JunTaoLuo), [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), and [Luke Latham](https://github.com/guardrex)</span></span>

> [!NOTE]
> <span data-ttu-id="94425-105">响应缓存在 Razor 页中是位于 ASP.NET Core 2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="94425-105">Response caching in Razor Pages is available in ASP.NET Core 2.1 or later.</span></span>

<span data-ttu-id="94425-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="94425-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/response/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="94425-107">响应缓存可减少客户端或代理到 web 服务器发出的请求数。</span><span class="sxs-lookup"><span data-stu-id="94425-107">Response caching reduces the number of requests a client or proxy makes to a web server.</span></span> <span data-ttu-id="94425-108">响应缓存还减少了工作的 web 服务器执行以生成响应。</span><span class="sxs-lookup"><span data-stu-id="94425-108">Response caching also reduces the amount of work the web server performs to generate a response.</span></span> <span data-ttu-id="94425-109">响应缓存控制标头，指定要如何客户端、 代理和响应缓存中间件。</span><span class="sxs-lookup"><span data-stu-id="94425-109">Response caching is controlled by headers that specify how you want client, proxy, and middleware to cache responses.</span></span>

<span data-ttu-id="94425-110">添加时，web 服务器可以缓存响应[响应缓存中间件](xref:performance/caching/middleware)。</span><span class="sxs-lookup"><span data-stu-id="94425-110">The web server can cache responses when you add [Response Caching Middleware](xref:performance/caching/middleware).</span></span>

## <a name="http-based-response-caching"></a><span data-ttu-id="94425-111">基于 HTTP 的响应缓存</span><span class="sxs-lookup"><span data-stu-id="94425-111">HTTP-based response caching</span></span>

<span data-ttu-id="94425-112">[HTTP 1.1 缓存规范](https://tools.ietf.org/html/rfc7234)介绍 Internet 缓存的行为方式。</span><span class="sxs-lookup"><span data-stu-id="94425-112">The [HTTP 1.1 Caching specification](https://tools.ietf.org/html/rfc7234) describes how Internet caches should behave.</span></span> <span data-ttu-id="94425-113">是用于缓存的主 HTTP 标头[Cache-control](https://tools.ietf.org/html/rfc7234#section-5.2)，用于指定缓存*指令*。</span><span class="sxs-lookup"><span data-stu-id="94425-113">The primary HTTP header used for caching is [Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2), which is used to specify cache *directives*.</span></span> <span data-ttu-id="94425-114">指令控制缓存行为，随着请求来自客户端对服务器进行自己的方式以及响应回客户端从服务器进行自己的方式。</span><span class="sxs-lookup"><span data-stu-id="94425-114">The directives control caching behavior as requests make their way from clients to servers and as reponses make their way from servers back to clients.</span></span> <span data-ttu-id="94425-115">请求和响应将通过代理服务器和代理服务器还必须符合 HTTP 1.1 缓存规范。</span><span class="sxs-lookup"><span data-stu-id="94425-115">Requests and responses move through proxy servers, and proxy servers must also conform to the HTTP 1.1 Caching specification.</span></span>

<span data-ttu-id="94425-116">常见`Cache-Control`指令下表中所示。</span><span class="sxs-lookup"><span data-stu-id="94425-116">Common `Cache-Control` directives are shown in the following table.</span></span>

| <span data-ttu-id="94425-117">指令</span><span class="sxs-lookup"><span data-stu-id="94425-117">Directive</span></span>                                                       | <span data-ttu-id="94425-118">操作</span><span class="sxs-lookup"><span data-stu-id="94425-118">Action</span></span> |
| --------------------------------------------------------------- | ------ |
| [<span data-ttu-id="94425-119">public</span><span class="sxs-lookup"><span data-stu-id="94425-119">public</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.2.5)   | <span data-ttu-id="94425-120">缓存可能会存储响应。</span><span class="sxs-lookup"><span data-stu-id="94425-120">A cache may store the response.</span></span> |
| [<span data-ttu-id="94425-121">private</span><span class="sxs-lookup"><span data-stu-id="94425-121">private</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.2.6)  | <span data-ttu-id="94425-122">响应不是由共享缓存存储。</span><span class="sxs-lookup"><span data-stu-id="94425-122">The response must not be stored by a shared cache.</span></span> <span data-ttu-id="94425-123">专用缓存可能会存储和重用响应。</span><span class="sxs-lookup"><span data-stu-id="94425-123">A private cache may store and reuse the response.</span></span> |
| [<span data-ttu-id="94425-124">max-age</span><span class="sxs-lookup"><span data-stu-id="94425-124">max-age</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.1)  | <span data-ttu-id="94425-125">客户端将不会接受其年龄大于指定的秒数的响应。</span><span class="sxs-lookup"><span data-stu-id="94425-125">The client won't accept a response whose age is greater than the specified number of seconds.</span></span> <span data-ttu-id="94425-126">示例： `max-age=60` （60 秒）， `max-age=2592000` （1 个月）</span><span class="sxs-lookup"><span data-stu-id="94425-126">Examples: `max-age=60` (60 seconds), `max-age=2592000` (1 month)</span></span> |
| [<span data-ttu-id="94425-127">no-cache</span><span class="sxs-lookup"><span data-stu-id="94425-127">no-cache</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.4) | <span data-ttu-id="94425-128">**在请求**： 缓存必须使用存储的响应来满足请求。</span><span class="sxs-lookup"><span data-stu-id="94425-128">**On requests**: A cache must not use a stored response to satisfy the request.</span></span> <span data-ttu-id="94425-129">注意： 源服务器为客户端，将重新生成响应，并将中间件更新其缓存中存储的响应。</span><span class="sxs-lookup"><span data-stu-id="94425-129">Note: The origin server re-generates the response for the client, and the middleware updates the stored response in its cache.</span></span><br><br><span data-ttu-id="94425-130">**响应**： 响应必须不应用于不带验证的源服务器上的后续请求。</span><span class="sxs-lookup"><span data-stu-id="94425-130">**On responses**: The response must not be used for a subsequent request without validation on the origin server.</span></span> |
| [<span data-ttu-id="94425-131">no-store</span><span class="sxs-lookup"><span data-stu-id="94425-131">no-store</span></span>](https://tools.ietf.org/html/rfc7234#section-5.2.1.5) | <span data-ttu-id="94425-132">**在请求**： 缓存不得存储请求。</span><span class="sxs-lookup"><span data-stu-id="94425-132">**On requests**: A cache must not store the request.</span></span><br><br><span data-ttu-id="94425-133">**响应**： 缓存不得存储任何响应的一部分。</span><span class="sxs-lookup"><span data-stu-id="94425-133">**On responses**: A cache must not store any part of the response.</span></span> |

<span data-ttu-id="94425-134">下表中显示其他播放的角色中缓存的缓存标头。</span><span class="sxs-lookup"><span data-stu-id="94425-134">Other cache headers that play a role in caching are shown in the following table.</span></span>

| <span data-ttu-id="94425-135">Header</span><span class="sxs-lookup"><span data-stu-id="94425-135">Header</span></span>                                                     | <span data-ttu-id="94425-136">函数</span><span class="sxs-lookup"><span data-stu-id="94425-136">Function</span></span> |
| ---------------------------------------------------------- | -------- |
| [<span data-ttu-id="94425-137">年龄</span><span class="sxs-lookup"><span data-stu-id="94425-137">Age</span></span>](https://tools.ietf.org/html/rfc7234#section-5.1)     | <span data-ttu-id="94425-138">以秒为单位因为响应已生成或在源服务器已成功验证的时间量的估计值。</span><span class="sxs-lookup"><span data-stu-id="94425-138">An estimate of the amount of time in seconds since the response was generated or successfully validated at the origin server.</span></span> |
| [<span data-ttu-id="94425-139">过期</span><span class="sxs-lookup"><span data-stu-id="94425-139">Expires</span></span>](https://tools.ietf.org/html/rfc7234#section-5.3) | <span data-ttu-id="94425-140">日期/时间后，响应被视为过时的内容。</span><span class="sxs-lookup"><span data-stu-id="94425-140">The date/time after which the response is considered stale.</span></span> |
| [<span data-ttu-id="94425-141">杂注</span><span class="sxs-lookup"><span data-stu-id="94425-141">Pragma</span></span>](https://tools.ietf.org/html/rfc7234#section-5.4)  | <span data-ttu-id="94425-142">存在向后兼容性，使用 HTTP/1.0 缓存设置`no-cache`行为。</span><span class="sxs-lookup"><span data-stu-id="94425-142">Exists for backwards compatibility with HTTP/1.0 caches for setting `no-cache` behavior.</span></span> <span data-ttu-id="94425-143">如果`Cache-Control`标头存在，则`Pragma`忽略标头。</span><span class="sxs-lookup"><span data-stu-id="94425-143">If the `Cache-Control` header is present, the `Pragma` header is ignored.</span></span> |
| [<span data-ttu-id="94425-144">改变</span><span class="sxs-lookup"><span data-stu-id="94425-144">Vary</span></span>](https://tools.ietf.org/html/rfc7231#section-7.1.4)  | <span data-ttu-id="94425-145">指定缓存的响应必须不发送除非所有的`Vary`中缓存的响应的原始请求和新的请求标头字段匹配。</span><span class="sxs-lookup"><span data-stu-id="94425-145">Specifies that a cached response must not be sent unless all of the `Vary` header fields match in both the cached response's original request and the new request.</span></span> |

## <a name="http-based-caching-respects-request-cache-control-directives"></a><span data-ttu-id="94425-146">基于 HTTP 的缓存方面请求缓存控制指令</span><span class="sxs-lookup"><span data-stu-id="94425-146">HTTP-based caching respects request Cache-Control directives</span></span>

<span data-ttu-id="94425-147">[HTTP 1.1 缓存的缓存控制标头的规范](https://tools.ietf.org/html/rfc7234#section-5.2)需要接受是有效的缓存`Cache-Control`客户端发送的标头。</span><span class="sxs-lookup"><span data-stu-id="94425-147">The [HTTP 1.1 Caching specification for the Cache-Control header](https://tools.ietf.org/html/rfc7234#section-5.2) requires a cache to honor a valid `Cache-Control` header sent by the client.</span></span> <span data-ttu-id="94425-148">客户端可以发出请求的`no-cache`标头值和强制服务器生成的每个请求的新响应。</span><span class="sxs-lookup"><span data-stu-id="94425-148">A client can make requests with a `no-cache` header value and force the server to generate a new response for every request.</span></span>

<span data-ttu-id="94425-149">始终遵循客户端`Cache-Control`请求标头是有意义，如果您考虑 HTTP 缓存的目标。</span><span class="sxs-lookup"><span data-stu-id="94425-149">Always honoring client `Cache-Control` request headers makes sense if you consider the goal of HTTP caching.</span></span> <span data-ttu-id="94425-150">在正式规范，缓存旨在减少的满足请求的客户端、 代理和服务器的网络延迟和网络开销。</span><span class="sxs-lookup"><span data-stu-id="94425-150">Under the official specification, caching is meant to reduce the latency and network overhead of satisfying requests across a network of clients, proxies, and servers.</span></span> <span data-ttu-id="94425-151">它不一定是一种方法来控制源服务器上的负载。</span><span class="sxs-lookup"><span data-stu-id="94425-151">It isn't necessarily a way to control the load on an origin server.</span></span>

<span data-ttu-id="94425-152">没有任何当前开发人员可以控制此缓存的行为使用时[响应缓存中间件](xref:performance/caching/middleware)因为中间件遵循正式缓存规范。</span><span class="sxs-lookup"><span data-stu-id="94425-152">There's no current developer control over this caching behavior when using the [Response Caching Middleware](xref:performance/caching/middleware) because the middleware adheres to the official caching specification.</span></span> <span data-ttu-id="94425-153">[未来的增强功能到中间件](https://github.com/aspnet/ResponseCaching/issues/96)将允许配置中间件，若要忽略的请求`Cache-Control`标头决定用于缓存的响应时。</span><span class="sxs-lookup"><span data-stu-id="94425-153">[Future enhancements to the middleware](https://github.com/aspnet/ResponseCaching/issues/96) will permit configuring the middleware to ignore a request's `Cache-Control` header when deciding to serve a cached response.</span></span> <span data-ttu-id="94425-154">使用中间件时，这将为您提供更好地控制负载在服务器上的机会。</span><span class="sxs-lookup"><span data-stu-id="94425-154">This will offer you an opportunity to better control the load on your server when you use the middleware.</span></span>

## <a name="other-caching-technology-in-aspnet-core"></a><span data-ttu-id="94425-155">在 ASP.NET Core 中其他缓存技术</span><span class="sxs-lookup"><span data-stu-id="94425-155">Other caching technology in ASP.NET Core</span></span>

### <a name="in-memory-caching"></a><span data-ttu-id="94425-156">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="94425-156">In-memory caching</span></span>

<span data-ttu-id="94425-157">内存中缓存使用的服务器内存来存储缓存的数据。</span><span class="sxs-lookup"><span data-stu-id="94425-157">In-memory caching uses server memory to store cached data.</span></span> <span data-ttu-id="94425-158">此类型的缓存是适用于单个服务器或多个服务器使用*粘性会话*。</span><span class="sxs-lookup"><span data-stu-id="94425-158">This type of caching is suitable for a single server or multiple servers using *sticky sessions*.</span></span> <span data-ttu-id="94425-159">粘性会话意味着，客户端的请求始终路由到同一个服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="94425-159">Sticky sessions means that the requests from a client are always routed to the same server for processing.</span></span>

<span data-ttu-id="94425-160">有关详细信息，请参阅[缓存在内存](xref:performance/caching/memory)。</span><span class="sxs-lookup"><span data-stu-id="94425-160">For more information, see [Cache in-memory](xref:performance/caching/memory).</span></span>

### <a name="distributed-cache"></a><span data-ttu-id="94425-161">分布式的缓存</span><span class="sxs-lookup"><span data-stu-id="94425-161">Distributed Cache</span></span>

<span data-ttu-id="94425-162">使用分布式的缓存在云或服务器场中托管应用时，将数据存储在内存中。</span><span class="sxs-lookup"><span data-stu-id="94425-162">Use a distributed cache to store data in memory when the app is hosted in a cloud or server farm.</span></span> <span data-ttu-id="94425-163">处理请求的服务器之间共享缓存。</span><span class="sxs-lookup"><span data-stu-id="94425-163">The cache is shared across the servers that process requests.</span></span> <span data-ttu-id="94425-164">客户端可以提交的请求，如果客户端的缓存的数据可由任何组中的服务器。</span><span class="sxs-lookup"><span data-stu-id="94425-164">A client can submit a request that's handled by any server in the group if cached data for the client is available.</span></span> <span data-ttu-id="94425-165">ASP.NET Core 提供 SQL Server 和分布式的 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="94425-165">ASP.NET Core offers SQL Server and Redis distributed caches.</span></span>

<span data-ttu-id="94425-166">有关详细信息，请参阅[使用分布式缓存](xref:performance/caching/distributed)。</span><span class="sxs-lookup"><span data-stu-id="94425-166">For more information, see [Work with a distributed cache](xref:performance/caching/distributed).</span></span>

### <a name="cache-tag-helper"></a><span data-ttu-id="94425-167">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="94425-167">Cache Tag Helper</span></span>

<span data-ttu-id="94425-168">可以使用缓存标记帮助程序缓存中的 MVC 视图或 Razor 页面的内容。</span><span class="sxs-lookup"><span data-stu-id="94425-168">You can cache the content from an MVC view or Razor Page with the Cache Tag Helper.</span></span> <span data-ttu-id="94425-169">缓存标记帮助程序使用内存中缓存来存储数据。</span><span class="sxs-lookup"><span data-stu-id="94425-169">The Cache Tag Helper uses in-memory caching to store data.</span></span>

<span data-ttu-id="94425-170">有关详细信息，请参阅[ASP.NET Core mvc 缓存标记帮助器](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="94425-170">For more information, see [Cache Tag Helper in ASP.NET Core MVC](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper).</span></span>

### <a name="distributed-cache-tag-helper"></a><span data-ttu-id="94425-171">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="94425-171">Distributed Cache Tag Helper</span></span>

<span data-ttu-id="94425-172">可以使用分布式缓存标记帮助程序缓存中的 MVC 视图或分布式的云或 web 场方案中的 Razor 页面的内容。</span><span class="sxs-lookup"><span data-stu-id="94425-172">You can cache the content from an MVC view or Razor Page in distributed cloud or web farm scenarios with the Distributed Cache Tag Helper.</span></span> <span data-ttu-id="94425-173">分布式缓存标记帮助程序使用 SQL Server 或 Redis 存储数据。</span><span class="sxs-lookup"><span data-stu-id="94425-173">The Distributed Cache Tag Helper uses SQL Server or Redis to store data.</span></span>

<span data-ttu-id="94425-174">有关详细信息，请参阅[分布式缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="94425-174">For more information, see [Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper).</span></span>

## <a name="responsecache-attribute"></a><span data-ttu-id="94425-175">ResponseCache 属性</span><span class="sxs-lookup"><span data-stu-id="94425-175">ResponseCache attribute</span></span>

<span data-ttu-id="94425-176">[ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute)指定缓存响应中设置相应的标头所需的参数。</span><span class="sxs-lookup"><span data-stu-id="94425-176">The [ResponseCacheAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.ResponseCacheAttribute) specifies the parameters necessary for setting appropriate headers in response caching.</span></span>

> [!WARNING]
> <span data-ttu-id="94425-177">禁用缓存的内容，其中包含已经过身份验证的客户端的信息。</span><span class="sxs-lookup"><span data-stu-id="94425-177">Disable caching for content that contains information for authenticated clients.</span></span> <span data-ttu-id="94425-178">仅应为不会更改基于用户的标识或是否在用户登录的内容启用缓存。</span><span class="sxs-lookup"><span data-stu-id="94425-178">Caching should only be enabled for content that doesn't change based on a user's identity or whether a user is signed in.</span></span>

<span data-ttu-id="94425-179">[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys)存储的响应因查询密钥的指定列表的值。</span><span class="sxs-lookup"><span data-stu-id="94425-179">[VaryByQueryKeys](/dotnet/api/microsoft.aspnetcore.mvc.responsecacheattribute.varybyquerykeys) varies the stored response by the values of the given list of query keys.</span></span> <span data-ttu-id="94425-180">时的单个值`*`是所有的响应请求查询字符串参数提供中间件会有所不同。</span><span class="sxs-lookup"><span data-stu-id="94425-180">When a single value of `*` is provided, the middleware varies responses by all request query string parameters.</span></span> <span data-ttu-id="94425-181">`VaryByQueryKeys` 需要 ASP.NET Core 1.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="94425-181">`VaryByQueryKeys` requires ASP.NET Core 1.1 or later.</span></span>

<span data-ttu-id="94425-182">必须启用响应缓存中间件设置`VaryByQueryKeys`属性; 否则，会引发运行时异常。</span><span class="sxs-lookup"><span data-stu-id="94425-182">The Response Caching Middleware must be enabled to set the `VaryByQueryKeys` property; otherwise, a runtime exception is thrown.</span></span> <span data-ttu-id="94425-183">没有为相应的 HTTP 标头`VaryByQueryKeys`属性。</span><span class="sxs-lookup"><span data-stu-id="94425-183">There isn't a corresponding HTTP header for the `VaryByQueryKeys` property.</span></span> <span data-ttu-id="94425-184">该属性是由响应缓存中间件处理的 HTTP 功能。</span><span class="sxs-lookup"><span data-stu-id="94425-184">The property is an HTTP feature handled by the Response Caching Middleware.</span></span> <span data-ttu-id="94425-185">中间件来提供缓存的响应，查询字符串和查询字符串值必须匹配上一个请求。</span><span class="sxs-lookup"><span data-stu-id="94425-185">For the middleware to serve a cached response, the query string and query string value must match a previous request.</span></span> <span data-ttu-id="94425-186">例如，考虑请求和下表中所示的结果的序列。</span><span class="sxs-lookup"><span data-stu-id="94425-186">For example, consider the sequence of requests and results shown in the following table.</span></span>

| <span data-ttu-id="94425-187">请求</span><span class="sxs-lookup"><span data-stu-id="94425-187">Request</span></span>                          | <span data-ttu-id="94425-188">结果</span><span class="sxs-lookup"><span data-stu-id="94425-188">Result</span></span>                   |
| -------------------------------- | ------------------------ |
| `http://example.com?key1=value1` | <span data-ttu-id="94425-189">从服务器返回</span><span class="sxs-lookup"><span data-stu-id="94425-189">Returned from server</span></span>     |
| `http://example.com?key1=value1` | <span data-ttu-id="94425-190">返回从中间件</span><span class="sxs-lookup"><span data-stu-id="94425-190">Returned from middleware</span></span> |
| `http://example.com?key1=value2` | <span data-ttu-id="94425-191">从服务器返回</span><span class="sxs-lookup"><span data-stu-id="94425-191">Returned from server</span></span>     |

<span data-ttu-id="94425-192">第一个请求将由服务器返回并缓存在中间件中。</span><span class="sxs-lookup"><span data-stu-id="94425-192">The first request is returned by the server and cached in middleware.</span></span> <span data-ttu-id="94425-193">因为查询字符串匹配上一个请求，中间件会返回第二个请求。</span><span class="sxs-lookup"><span data-stu-id="94425-193">The second request is returned by middleware because the query string matches the previous request.</span></span> <span data-ttu-id="94425-194">因为查询字符串值不匹配上一个请求，第三个请求不是中间件缓存中。</span><span class="sxs-lookup"><span data-stu-id="94425-194">The third request isn't in the middleware cache because the query string value doesn't match a previous request.</span></span> 

<span data-ttu-id="94425-195">`ResponseCacheAttribute`用于配置和创建 (通过`IFilterFactory`) [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter)。</span><span class="sxs-lookup"><span data-stu-id="94425-195">The `ResponseCacheAttribute` is used to configure and create (via `IFilterFactory`) a [ResponseCacheFilter](/dotnet/api/microsoft.aspnetcore.mvc.internal.responsecachefilter).</span></span> <span data-ttu-id="94425-196">`ResponseCacheFilter`执行更新的适当的 HTTP 标头和响应的功能的工作。</span><span class="sxs-lookup"><span data-stu-id="94425-196">The `ResponseCacheFilter` performs the work of updating the appropriate HTTP headers and features of the response.</span></span> <span data-ttu-id="94425-197">筛选器：</span><span class="sxs-lookup"><span data-stu-id="94425-197">The filter:</span></span>

* <span data-ttu-id="94425-198">删除任何现有标头`Vary`， `Cache-Control`，和`Pragma`。</span><span class="sxs-lookup"><span data-stu-id="94425-198">Removes any existing headers for `Vary`, `Cache-Control`, and `Pragma`.</span></span> 
* <span data-ttu-id="94425-199">写出适当的标头中设置的属性上基于`ResponseCacheAttribute`。</span><span class="sxs-lookup"><span data-stu-id="94425-199">Writes out the appropriate headers based on the properties set in the `ResponseCacheAttribute`.</span></span> 
* <span data-ttu-id="94425-200">更新缓存项 HTTP 功能中，如果响应`VaryByQueryKeys`设置。</span><span class="sxs-lookup"><span data-stu-id="94425-200">Updates the response caching HTTP feature if `VaryByQueryKeys` is set.</span></span>

### <a name="vary"></a><span data-ttu-id="94425-201">改变</span><span class="sxs-lookup"><span data-stu-id="94425-201">Vary</span></span>

<span data-ttu-id="94425-202">此标头时仅写入`VaryByHeader`属性设置。</span><span class="sxs-lookup"><span data-stu-id="94425-202">This header is only written when the `VaryByHeader` property is set.</span></span> <span data-ttu-id="94425-203">设置为`Vary`属性的值。</span><span class="sxs-lookup"><span data-stu-id="94425-203">It's set to the `Vary` property's value.</span></span> <span data-ttu-id="94425-204">下面的示例使用`VaryByHeader`属性：</span><span class="sxs-lookup"><span data-stu-id="94425-204">The following sample uses the `VaryByHeader` property:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_VaryByHeader&highlight=1)]

::: moniker-end

<span data-ttu-id="94425-205">您可以查看浏览器的网络工具的响应标头。</span><span class="sxs-lookup"><span data-stu-id="94425-205">You can view the response headers with your browser's network tools.</span></span> <span data-ttu-id="94425-206">下图显示了输出上边缘 F12**网络**选项卡时`About2`刷新操作方法：</span><span class="sxs-lookup"><span data-stu-id="94425-206">The following image shows the Edge F12 output on the **Network** tab when the `About2` action method is refreshed:</span></span>

![在网络选项卡上边缘 F12 输出时调用 About2 操作方法](response/_static/vary.png)

### <a name="nostore-and-locationnone"></a><span data-ttu-id="94425-208">NoStore 和 Location.None</span><span class="sxs-lookup"><span data-stu-id="94425-208">NoStore and Location.None</span></span>

<span data-ttu-id="94425-209">`NoStore` 重写的大多数其他属性。</span><span class="sxs-lookup"><span data-stu-id="94425-209">`NoStore` overrides most of the other properties.</span></span> <span data-ttu-id="94425-210">当此属性设置为`true`，则`Cache-Control`标头设置为`no-store`。</span><span class="sxs-lookup"><span data-stu-id="94425-210">When this property is set to `true`, the `Cache-Control` header is set to `no-store`.</span></span> <span data-ttu-id="94425-211">如果`Location`设置为`None`:</span><span class="sxs-lookup"><span data-stu-id="94425-211">If `Location` is set to `None`:</span></span>

* <span data-ttu-id="94425-212">将 `Cache-Control` 设置为 `no-store,no-cache`。</span><span class="sxs-lookup"><span data-stu-id="94425-212">`Cache-Control` is set to `no-store,no-cache`.</span></span>
* <span data-ttu-id="94425-213">将 `Pragma` 设置为 `no-cache`。</span><span class="sxs-lookup"><span data-stu-id="94425-213">`Pragma` is set to `no-cache`.</span></span>

<span data-ttu-id="94425-214">如果`NoStore`是`false`并`Location`是`None`，`Cache-Control`并`Pragma`设置为`no-cache`。</span><span class="sxs-lookup"><span data-stu-id="94425-214">If `NoStore` is `false` and `Location` is `None`, `Cache-Control` and `Pragma` are set to `no-cache`.</span></span>

<span data-ttu-id="94425-215">通常设置`NoStore`到`true`错误页上。</span><span class="sxs-lookup"><span data-stu-id="94425-215">You typically set `NoStore` to `true` on error pages.</span></span> <span data-ttu-id="94425-216">例如：</span><span class="sxs-lookup"><span data-stu-id="94425-216">For example:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet1&highlight=1)]

::: moniker-end

<span data-ttu-id="94425-217">这会导致以下标头：</span><span class="sxs-lookup"><span data-stu-id="94425-217">This results in the following headers:</span></span>

```
Cache-Control: no-store,no-cache
Pragma: no-cache
```

### <a name="location-and-duration"></a><span data-ttu-id="94425-218">位置和持续时间</span><span class="sxs-lookup"><span data-stu-id="94425-218">Location and Duration</span></span>

<span data-ttu-id="94425-219">若要启用缓存，`Duration`必须设置为正值和`Location`必须是`Any`（默认值） 或`Client`。</span><span class="sxs-lookup"><span data-stu-id="94425-219">To enable caching, `Duration` must be set to a positive value and `Location` must be either `Any` (the default) or `Client`.</span></span> <span data-ttu-id="94425-220">在这种情况下，`Cache-Control`标头设置为位置值后, 接`max-age`的响应。</span><span class="sxs-lookup"><span data-stu-id="94425-220">In this case, the `Cache-Control` header is set to the location value followed by the `max-age` of the response.</span></span>

> [!NOTE]
> <span data-ttu-id="94425-221">`Location`选项`Any`并`Client`转换为`Cache-Control`标头值的`public`和`private`分别。</span><span class="sxs-lookup"><span data-stu-id="94425-221">`Location`'s options of `Any` and `Client` translate into `Cache-Control` header values of `public` and `private`, respectively.</span></span> <span data-ttu-id="94425-222">按前面所述，设置`Location`到`None`设置同时`Cache-Control`并`Pragma`标头`no-cache`。</span><span class="sxs-lookup"><span data-stu-id="94425-222">As noted previously, setting `Location` to `None` sets both `Cache-Control` and `Pragma` headers to `no-cache`.</span></span>

<span data-ttu-id="94425-223">下面生成通过设置显示标头的示例`Duration`并保留默认值`Location`值：</span><span class="sxs-lookup"><span data-stu-id="94425-223">Below is an example showing the headers produced by setting `Duration` and leaving the default `Location` value:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_duration&highlight=1)]

::: moniker-end

<span data-ttu-id="94425-224">这将产生以下标头：</span><span class="sxs-lookup"><span data-stu-id="94425-224">This produces the following header:</span></span>

```
Cache-Control: public,max-age=60
```

### <a name="cache-profiles"></a><span data-ttu-id="94425-225">缓存配置文件</span><span class="sxs-lookup"><span data-stu-id="94425-225">Cache profiles</span></span>

<span data-ttu-id="94425-226">而不是重复`ResponseCache`设置中的 MVC 时多个控制器操作属性，缓存配置文件上的设置可以配置为选项`ConfigureServices`中的方法`Startup`。</span><span class="sxs-lookup"><span data-stu-id="94425-226">Instead of duplicating `ResponseCache` settings on many controller action attributes, cache profiles can be configured as options when setting up MVC in the `ConfigureServices` method in `Startup`.</span></span> <span data-ttu-id="94425-227">引用的缓存配置文件中找到的值用作默认值由`ResponseCache`属性，并由属性指定任何属性重写。</span><span class="sxs-lookup"><span data-stu-id="94425-227">Values found in a referenced cache profile are used as the defaults by the `ResponseCache` attribute and are overridden by any properties specified on the attribute.</span></span>

<span data-ttu-id="94425-228">设置缓存配置文件：</span><span class="sxs-lookup"><span data-stu-id="94425-228">Setting up a cache profile:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Startup.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="94425-229">引用缓存配置文件：</span><span class="sxs-lookup"><span data-stu-id="94425-229">Referencing a cache profile:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](response/samples/2.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](response/samples/1.x/ResponseCacheSample/Controllers/HomeController.cs?name=snippet_controller&highlight=1,4)]

::: moniker-end

<span data-ttu-id="94425-230">`ResponseCache`特性可应用于操作 （方法） 和控制器 （类）。</span><span class="sxs-lookup"><span data-stu-id="94425-230">The `ResponseCache` attribute can be applied both to actions (methods) and controllers (classes).</span></span> <span data-ttu-id="94425-231">方法级属性重写在类级别特性中指定的设置。</span><span class="sxs-lookup"><span data-stu-id="94425-231">Method-level attributes override the settings specified in class-level attributes.</span></span>

<span data-ttu-id="94425-232">在上述示例中，类级别属性指定持续时间为 30 秒，同时持续时间设置为 60 秒，方法级属性引用的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="94425-232">In the above example, a class-level attribute specifies a duration of 30 seconds, while a method-level attribute references a cache profile with a duration set to 60 seconds.</span></span>

<span data-ttu-id="94425-233">生成的标头：</span><span class="sxs-lookup"><span data-stu-id="94425-233">The resulting header:</span></span>

```
Cache-Control: public,max-age=60
```

## <a name="additional-resources"></a><span data-ttu-id="94425-234">其他资源</span><span class="sxs-lookup"><span data-stu-id="94425-234">Additional resources</span></span>

* [<span data-ttu-id="94425-235">在缓存中存储的响应</span><span class="sxs-lookup"><span data-stu-id="94425-235">Storing Responses in Caches</span></span>](https://tools.ietf.org/html/rfc7234#section-3)
* [<span data-ttu-id="94425-236">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="94425-236">Cache-Control</span></span>](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="94425-237">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="94425-237">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="94425-238">使用分布式缓存</span><span class="sxs-lookup"><span data-stu-id="94425-238">Work with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="94425-239">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="94425-239">Detect changes with change tokens</span></span>](xref:fundamentals/change-tokens)
* [<span data-ttu-id="94425-240">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="94425-240">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="94425-241">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="94425-241">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="94425-242">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="94425-242">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
