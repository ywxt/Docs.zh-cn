---
title: "ASP.NET 核心中的内存中缓存"
author: rick-anderson
description: "了解如何在 ASP.NET Core 中的内存中缓存数据。"
ms.author: riande
manager: wpickett
ms.date: 12/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: performance/caching/memory
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12d3982ce1abf74a575dae5362b037bd4ecc3d0f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="in-memory-caching-in-aspnet-core"></a><span data-ttu-id="8a67e-103">ASP.NET 核心中的内存中缓存</span><span class="sxs-lookup"><span data-stu-id="8a67e-103">In-memory caching in ASP.NET Core</span></span>

<span data-ttu-id="8a67e-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)， [John Luo](https://github.com/JunTaoLuo)，和[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="8a67e-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [John Luo](https://github.com/JunTaoLuo), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="8a67e-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8a67e-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="caching-basics"></a><span data-ttu-id="8a67e-106">缓存的基础知识</span><span class="sxs-lookup"><span data-stu-id="8a67e-106">Caching basics</span></span>

<span data-ttu-id="8a67e-107">缓存可以显著提高性能和可伸缩性的应用程序通过减少生成内容所需的工作量。</span><span class="sxs-lookup"><span data-stu-id="8a67e-107">Caching can significantly improve the performance and scalability of an app by reducing the work required to generate content.</span></span> <span data-ttu-id="8a67e-108">最适合于不经常更改的数据的缓存工作方式。</span><span class="sxs-lookup"><span data-stu-id="8a67e-108">Caching works best with data that changes infrequently.</span></span> <span data-ttu-id="8a67e-109">缓存可一份很多可以返回的数据比从原始源更快。</span><span class="sxs-lookup"><span data-stu-id="8a67e-109">Caching makes a copy of data that can be returned much faster than from the original source.</span></span> <span data-ttu-id="8a67e-110">你应编写并测试你的应用程序永远不会依赖于缓存的数据。</span><span class="sxs-lookup"><span data-stu-id="8a67e-110">You should write and test your app to never depend on cached data.</span></span>

<span data-ttu-id="8a67e-111">ASP.NET 核心支持几个不同的缓存。</span><span class="sxs-lookup"><span data-stu-id="8a67e-111">ASP.NET Core supports several different caches.</span></span> <span data-ttu-id="8a67e-112">最简单的缓存基于[IMemoryCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)，它表示存储在内存中的 web 服务器的缓存。</span><span class="sxs-lookup"><span data-stu-id="8a67e-112">The simplest cache is based on the [IMemoryCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache), which represents a cache stored in the memory of the web server.</span></span> <span data-ttu-id="8a67e-113">在服务器场的多个服务器运行的应用程序应确保使用内存中缓存时，会粘性会话。</span><span class="sxs-lookup"><span data-stu-id="8a67e-113">Apps which run on a server farm of multiple servers should ensure that sessions are sticky when using the in-memory cache.</span></span> <span data-ttu-id="8a67e-114">粘性会话确保所有客户端的后续请求转到同一台服务器。</span><span class="sxs-lookup"><span data-stu-id="8a67e-114">Sticky sessions ensure that subsequent requests from a client all go to the same server.</span></span> <span data-ttu-id="8a67e-115">例如，Azure Web 应用使用[应用程序请求路由](https://www.iis.net/learn/extensions/planning-for-arr)(ARR) 将所有的后续请求路由到同一台服务器。</span><span class="sxs-lookup"><span data-stu-id="8a67e-115">For example, Azure Web apps use [Application Request Routing](https://www.iis.net/learn/extensions/planning-for-arr) (ARR) to route all subsequent requests to the same server.</span></span>

<span data-ttu-id="8a67e-116">Web 场中的非粘性会话需要[分布式缓存](distributed.md)以避免缓存一致性问题。</span><span class="sxs-lookup"><span data-stu-id="8a67e-116">Non-sticky sessions in a web farm require a [distributed cache](distributed.md) to avoid cache consistency problems.</span></span> <span data-ttu-id="8a67e-117">对于某些应用，分布式的缓存可以支持更高版本横向扩展比内存中缓存。</span><span class="sxs-lookup"><span data-stu-id="8a67e-117">For some apps, a distributed cache can support higher scale out than an in-memory cache.</span></span> <span data-ttu-id="8a67e-118">使用分布式的缓存将卸载到外部进程缓存内存。</span><span class="sxs-lookup"><span data-stu-id="8a67e-118">Using a distributed cache offloads the cache memory to an external process.</span></span> 

<span data-ttu-id="8a67e-119">`IMemoryCache`缓存将逐出缓存条目内存压力下的，除非[缓存优先级](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheitempriority)设置为`CacheItemPriority.NeverRemove`。</span><span class="sxs-lookup"><span data-stu-id="8a67e-119">The `IMemoryCache` cache will evict cache entries under memory pressure unless the [cache priority](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheitempriority) is set to `CacheItemPriority.NeverRemove`.</span></span> <span data-ttu-id="8a67e-120">你可以设置`CacheItemPriority`调整优先级缓存逐出内存压力下的项。</span><span class="sxs-lookup"><span data-stu-id="8a67e-120">You can set the `CacheItemPriority` to adjust the priority the cache evicts items under memory pressure.</span></span>

<span data-ttu-id="8a67e-121">内存中缓存中可以存储任何对象;分布式的缓存接口仅限于`byte[]`。</span><span class="sxs-lookup"><span data-stu-id="8a67e-121">The in-memory cache can store any object; the distributed cache interface is limited to `byte[]`.</span></span>

## <a name="using-imemorycache"></a><span data-ttu-id="8a67e-122">使用 IMemoryCache</span><span class="sxs-lookup"><span data-stu-id="8a67e-122">Using IMemoryCache</span></span>

<span data-ttu-id="8a67e-123">内存中缓存是*服务*引用从你的应用使用[依赖关系注入](../../fundamentals/dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="8a67e-123">In-memory caching is a *service* that's referenced from your app using [Dependency Injection](../../fundamentals/dependency-injection.md).</span></span> <span data-ttu-id="8a67e-124">调用`AddMemoryCache`中`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="8a67e-124">Call `AddMemoryCache` in `ConfigureServices`:</span></span>

[!code-csharp[Main](memory/sample/WebCache/Startup.cs?highlight=8)] 

<span data-ttu-id="8a67e-125">请求`IMemoryCache`构造函数中的实例：</span><span class="sxs-lookup"><span data-stu-id="8a67e-125">Request the `IMemoryCache` instance in the constructor:</span></span>

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ctor&highlight=3,5-)] 

<span data-ttu-id="8a67e-126">`IMemoryCache`需要 NuGet 包"Microsoft.Extensions.Caching.Memory"。</span><span class="sxs-lookup"><span data-stu-id="8a67e-126">`IMemoryCache` requires NuGet package "Microsoft.Extensions.Caching.Memory".</span></span>

<span data-ttu-id="8a67e-127">下面的代码使用[TryGetValue](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__)检查当前时间是否在缓存中。</span><span class="sxs-lookup"><span data-stu-id="8a67e-127">The following code uses [TryGetValue](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__) to check if the current time is in the cache.</span></span> <span data-ttu-id="8a67e-128">如果未缓存项，创建并添加到缓存中，使用新的条目[设置](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_)。</span><span class="sxs-lookup"><span data-stu-id="8a67e-128">If the item isn't cached, a new entry is created and added to the cache with [Set](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_).</span></span>

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet1)]

<span data-ttu-id="8a67e-129">显示当前时间和缓存的时间：</span><span class="sxs-lookup"><span data-stu-id="8a67e-129">The current time and the cached time is displayed:</span></span>

[!code-html[Main](memory/sample/WebCache/Views/Home/Cache.cshtml)]

<span data-ttu-id="8a67e-130">已缓存`DateTime`值将保留在缓存中，尽管在超时期限 （和由于内存压力没有逐出） 的请求。</span><span class="sxs-lookup"><span data-stu-id="8a67e-130">The cached `DateTime` value will remain in the cache while there are requests within the timeout period (and no eviction due to memory pressure).</span></span> <span data-ttu-id="8a67e-131">下图显示当前时间和较旧时间从缓存中检索：</span><span class="sxs-lookup"><span data-stu-id="8a67e-131">The image below shows the current time and an older time retrieved from cache:</span></span>

![具有两个不同的时间显示的索引视图](memory/_static/time.png)

<span data-ttu-id="8a67e-133">下面的代码使用[GetOrCreate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__)和[GetOrCreateAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___)缓存数据。</span><span class="sxs-lookup"><span data-stu-id="8a67e-133">The following code uses [GetOrCreate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__) and [GetOrCreateAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___) to cache data.</span></span> 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet2&highlight=3-7,14-19)]

<span data-ttu-id="8a67e-134">下面的代码调用[获取](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_)提取缓存的时间：</span><span class="sxs-lookup"><span data-stu-id="8a67e-134">The following code calls [Get](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_) to fetch the cached time:</span></span>

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_gct)]

<span data-ttu-id="8a67e-135">请参阅[IMemoryCache 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)和[CacheExtensions 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions)有关缓存方法的说明。</span><span class="sxs-lookup"><span data-stu-id="8a67e-135">See [IMemoryCache methods](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache) and [CacheExtensions methods](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions) for a description of the cache methods.</span></span>

## <a name="using-memorycacheentryoptions"></a><span data-ttu-id="8a67e-136">使用 MemoryCacheEntryOptions</span><span class="sxs-lookup"><span data-stu-id="8a67e-136">Using MemoryCacheEntryOptions</span></span>

<span data-ttu-id="8a67e-137">下面的示例：</span><span class="sxs-lookup"><span data-stu-id="8a67e-137">The following sample:</span></span>

- <span data-ttu-id="8a67e-138">设置绝对到期时间。</span><span class="sxs-lookup"><span data-stu-id="8a67e-138">Sets the absolute expiration time.</span></span> <span data-ttu-id="8a67e-139">这是可以缓存条目的最长时间，可防止项持续续订滑动过期时变得太陈旧。</span><span class="sxs-lookup"><span data-stu-id="8a67e-139">This is the maximum time the entry can be cached and prevents the item from becoming too stale when the sliding expiration is continuously renewed.</span></span>
- <span data-ttu-id="8a67e-140">设置滑动过期时间。</span><span class="sxs-lookup"><span data-stu-id="8a67e-140">Sets a sliding expiration time.</span></span> <span data-ttu-id="8a67e-141">访问此缓存的项的请求将重置滑动到期时钟。</span><span class="sxs-lookup"><span data-stu-id="8a67e-141">Requests that access this cached item will reset the sliding expiration clock.</span></span>
- <span data-ttu-id="8a67e-142">将缓存优先级设置为`CacheItemPriority.NeverRemove`。</span><span class="sxs-lookup"><span data-stu-id="8a67e-142">Sets the cache priority to `CacheItemPriority.NeverRemove`.</span></span> 
- <span data-ttu-id="8a67e-143">集[PostEvictionDelegate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.postevictiondelegate)后从缓存逐出项，将调用的。</span><span class="sxs-lookup"><span data-stu-id="8a67e-143">Sets a [PostEvictionDelegate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.postevictiondelegate) that will be called after the entry is evicted from the cache.</span></span> <span data-ttu-id="8a67e-144">回调是在从缓存中移除的项的代码与不同的线程上运行。</span><span class="sxs-lookup"><span data-stu-id="8a67e-144">The callback is run on a different thread from the code that removes the item from the cache.</span></span>

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_et&highlight=14-20)]

## <a name="cache-dependencies"></a><span data-ttu-id="8a67e-145">缓存依赖项</span><span class="sxs-lookup"><span data-stu-id="8a67e-145">Cache dependencies</span></span>

<span data-ttu-id="8a67e-146">下面的示例演示如何过期的缓存项，如果依赖项将过期。</span><span class="sxs-lookup"><span data-stu-id="8a67e-146">The following sample shows how to expire a cache entry if a dependent entry expires.</span></span> <span data-ttu-id="8a67e-147">A`CancellationChangeToken`添加到缓存的项。</span><span class="sxs-lookup"><span data-stu-id="8a67e-147">A `CancellationChangeToken` is added to the cached item.</span></span> <span data-ttu-id="8a67e-148">当`Cancel`上调用`CancellationTokenSource`，这两个缓存条目被逐出。</span><span class="sxs-lookup"><span data-stu-id="8a67e-148">When `Cancel` is called on the `CancellationTokenSource`, both cache entries are evicted.</span></span> 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ed)]

<span data-ttu-id="8a67e-149">使用`CancellationTokenSource`允许多个缓存条目被逐出作为一个组。</span><span class="sxs-lookup"><span data-stu-id="8a67e-149">Using a `CancellationTokenSource` allows multiple cache entries to be evicted as a group.</span></span> <span data-ttu-id="8a67e-150">与`using`在上面的代码的模式，在内部创建的缓存条目`using`块将继承触发器和过期时间设置。</span><span class="sxs-lookup"><span data-stu-id="8a67e-150">With the `using` pattern in the code above, cache entries created inside the `using` block will inherit triggers and expiration settings.</span></span>

## <a name="additional-notes"></a><span data-ttu-id="8a67e-151">附加说明</span><span class="sxs-lookup"><span data-stu-id="8a67e-151">Additional notes</span></span>

- <span data-ttu-id="8a67e-152">当使用的回调以重新填充缓存项：</span><span class="sxs-lookup"><span data-stu-id="8a67e-152">When using a callback to repopulate a cache item:</span></span>

  - <span data-ttu-id="8a67e-153">多个请求可以查找缓存的键值空因为尚未完成的回调。</span><span class="sxs-lookup"><span data-stu-id="8a67e-153">Multiple requests can find the cached key value empty because the callback hasn't completed.</span></span> 
  - <span data-ttu-id="8a67e-154">这可能导致重新填充缓存的项的多个线程。</span><span class="sxs-lookup"><span data-stu-id="8a67e-154">This can result in several threads repopulating the cached item.</span></span>

- <span data-ttu-id="8a67e-155">当一个缓存条目用于创建另一个时，子复制父项的过期的令牌和基于时间的过期时间设置。</span><span class="sxs-lookup"><span data-stu-id="8a67e-155">When one cache entry is used to create another, the child copies the parent entry's expiration tokens and time-based expiration settings.</span></span> <span data-ttu-id="8a67e-156">子不过期通过手动删除或更新的父项。</span><span class="sxs-lookup"><span data-stu-id="8a67e-156">The child isn't expired by manual removal or updating of the parent entry.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a67e-157">其他资源</span><span class="sxs-lookup"><span data-stu-id="8a67e-157">Additional resources</span></span>

* [<span data-ttu-id="8a67e-158">使用分布式缓存</span><span class="sxs-lookup"><span data-stu-id="8a67e-158">Working with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="8a67e-159">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="8a67e-159">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="8a67e-160">响应缓存</span><span class="sxs-lookup"><span data-stu-id="8a67e-160">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="8a67e-161">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="8a67e-161">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="8a67e-162">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="8a67e-162">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="8a67e-163">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="8a67e-163">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
