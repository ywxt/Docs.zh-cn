---
title: 缓存在内存中 ASP.NET 核心
author: rick-anderson
description: 了解如何在 ASP.NET Core 中的内存中缓存数据。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 12/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/memory
ms.openlocfilehash: eca6610caf4e0a654c9a31f89a42e2ac82e94d23
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34734479"
---
# <a name="cache-in-memory-in-aspnet-core"></a><span data-ttu-id="a6d22-103">缓存在内存中 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="a6d22-103">Cache in-memory in ASP.NET Core</span></span>

<span data-ttu-id="a6d22-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)， [John Luo](https://github.com/JunTaoLuo)，和[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="a6d22-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [John Luo](https://github.com/JunTaoLuo), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="a6d22-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="a6d22-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="caching-basics"></a><span data-ttu-id="a6d22-106">缓存的基础知识</span><span class="sxs-lookup"><span data-stu-id="a6d22-106">Caching basics</span></span>

<span data-ttu-id="a6d22-107">通过减少生成内容所需的工作，缓存可以显著提高应用的性能和可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="a6d22-107">Caching can significantly improve the performance and scalability of an app by reducing the work required to generate content.</span></span> <span data-ttu-id="a6d22-108">缓存对不经常更改的数据效果最佳。</span><span class="sxs-lookup"><span data-stu-id="a6d22-108">Caching works best with data that changes infrequently.</span></span> <span data-ttu-id="a6d22-109">缓存生成的数据副本的返回速度可以比从原始源返回更快。</span><span class="sxs-lookup"><span data-stu-id="a6d22-109">Caching makes a copy of data that can be returned much faster than from the original source.</span></span> <span data-ttu-id="a6d22-110">在编写并测试应用时，应避免依赖缓存的数据。</span><span class="sxs-lookup"><span data-stu-id="a6d22-110">You should write and test your app to never depend on cached data.</span></span>

<span data-ttu-id="a6d22-111">ASP.NET Core 支持多种不同的缓存。</span><span class="sxs-lookup"><span data-stu-id="a6d22-111">ASP.NET Core supports several different caches.</span></span> <span data-ttu-id="a6d22-112">最简单的缓存基于 [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)，它表示存储在 Web 服务器内存中的缓存。</span><span class="sxs-lookup"><span data-stu-id="a6d22-112">The simplest cache is based on the [IMemoryCache](/dotnet/api/microsoft.extensions.caching.memory.imemorycache), which represents a cache stored in the memory of the web server.</span></span> <span data-ttu-id="a6d22-113">在包含多个服务器的服务器场上运行的应用应确保在使用内存中缓存时，会话是粘性的。</span><span class="sxs-lookup"><span data-stu-id="a6d22-113">Apps which run on a server farm of multiple servers should ensure that sessions are sticky when using the in-memory cache.</span></span> <span data-ttu-id="a6d22-114">粘性会话可确保来自客户端的后续请求都转到同一台服务器。</span><span class="sxs-lookup"><span data-stu-id="a6d22-114">Sticky sessions ensure that subsequent requests from a client all go to the same server.</span></span> <span data-ttu-id="a6d22-115">例如，Azure Web 应用使用[应用程序请求路由](https://www.iis.net/learn/extensions/planning-for-arr)(ARR) 将所有的后续请求路由到同一台服务器。</span><span class="sxs-lookup"><span data-stu-id="a6d22-115">For example, Azure Web apps use [Application Request Routing](https://www.iis.net/learn/extensions/planning-for-arr) (ARR) to route all subsequent requests to the same server.</span></span>

<span data-ttu-id="a6d22-116">Web 场中的非粘性会话需要[分布式缓存](distributed.md)以避免缓存一致性问题。</span><span class="sxs-lookup"><span data-stu-id="a6d22-116">Non-sticky sessions in a web farm require a [distributed cache](distributed.md) to avoid cache consistency problems.</span></span> <span data-ttu-id="a6d22-117">对于某些应用来说，分布式缓存可以支持比内存中缓存更高程度的横向扩展。</span><span class="sxs-lookup"><span data-stu-id="a6d22-117">For some apps, a distributed cache can support higher scale out than an in-memory cache.</span></span> <span data-ttu-id="a6d22-118">使用分布式缓存可将缓存内存卸载到外部进程。</span><span class="sxs-lookup"><span data-stu-id="a6d22-118">Using a distributed cache offloads the cache memory to an external process.</span></span>

<span data-ttu-id="a6d22-119">除非将[CacheItemPriority](/dotnet/api/microsoft.extensions.caching.memory.cacheitempriority)设置为`CacheItemPriority.NeverRemove`, 否则`IMemoryCache`缓存会在内存压力下清除缓存条目。</span><span class="sxs-lookup"><span data-stu-id="a6d22-119">The `IMemoryCache` cache will evict cache entries under memory pressure unless the [cache priority](/dotnet/api/microsoft.extensions.caching.memory.cacheitempriority) is set to `CacheItemPriority.NeverRemove`.</span></span> <span data-ttu-id="a6d22-120">可以通过设置`CacheItemPriority`来调整缓存在内存压力下清除项目的优先级。</span><span class="sxs-lookup"><span data-stu-id="a6d22-120">You can set the `CacheItemPriority` to adjust the priority with which the cache evicts items under memory pressure.</span></span>

<span data-ttu-id="a6d22-121">内存中缓存可以存储任何对象；分布式缓存接口仅限于`byte[]`。</span><span class="sxs-lookup"><span data-stu-id="a6d22-121">The in-memory cache can store any object; the distributed cache interface is limited to `byte[]`.</span></span>

## <a name="using-imemorycache"></a><span data-ttu-id="a6d22-122">使用 IMemoryCache</span><span class="sxs-lookup"><span data-stu-id="a6d22-122">Using IMemoryCache</span></span>

<span data-ttu-id="a6d22-123">内存中缓存是使用[依赖关系注入](../../fundamentals/dependency-injection.md)从应用中引用的服务。</span><span class="sxs-lookup"><span data-stu-id="a6d22-123">In-memory caching is a *service* that's referenced from your app using [Dependency Injection](../../fundamentals/dependency-injection.md).</span></span> <span data-ttu-id="a6d22-124">请在`ConfigureServices`中调用`AddMemoryCache`:</span><span class="sxs-lookup"><span data-stu-id="a6d22-124">Call `AddMemoryCache` in `ConfigureServices`:</span></span>

[!code-csharp[](memory/sample/WebCache/Startup.cs?highlight=9)]

<span data-ttu-id="a6d22-125">在构造函数中请求 `IMemoryCache`实例：</span><span class="sxs-lookup"><span data-stu-id="a6d22-125">Request the `IMemoryCache` instance in the constructor:</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ctor)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a6d22-126">`IMemoryCache` 需要 NuGet 包[Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/)。</span><span class="sxs-lookup"><span data-stu-id="a6d22-126">`IMemoryCache` requires NuGet package [Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="a6d22-127">`IMemoryCache` 需要 NuGet 包[Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/)，这是可供使用的[Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)。</span><span class="sxs-lookup"><span data-stu-id="a6d22-127">`IMemoryCache` requires NuGet package [Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/), which is avaiable in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.0"

<span data-ttu-id="a6d22-128">`IMemoryCache` 需要 NuGet 包[Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/)，这是可供使用的[Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app)。</span><span class="sxs-lookup"><span data-stu-id="a6d22-128">`IMemoryCache` requires NuGet package [Microsoft.Extensions.Caching.Memory](https://www.nuget.org/packages/Microsoft.Extensions.Caching.Memory/), which is avaiable in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

<span data-ttu-id="a6d22-129">下面的代码使用[TryGetValue](/dotnet/api/microsoft.extensions.caching.memory.imemorycache.trygetvalue?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__)检查时间是否在缓存中。</span><span class="sxs-lookup"><span data-stu-id="a6d22-129">The following code uses [TryGetValue](/dotnet/api/microsoft.extensions.caching.memory.imemorycache.trygetvalue?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__) to check if a time is in the cache.</span></span> <span data-ttu-id="a6d22-130">如果未缓存的时间，创建并添加到缓存中，使用新的条目[设置](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.set?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_Microsoft_Extensions_Caching_Memory_MemoryCacheEntryOptions_)。</span><span class="sxs-lookup"><span data-stu-id="a6d22-130">If a time isn't cached, a new entry is created and added to the cache with [Set](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.set?view=aspnetcore-2.0#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_Microsoft_Extensions_Caching_Memory_MemoryCacheEntryOptions_).</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet1)]

<span data-ttu-id="a6d22-131">将会显示当前时间和缓存的时间：</span><span class="sxs-lookup"><span data-stu-id="a6d22-131">The current time and the cached time are displayed:</span></span>

[!code-cshtml[](memory/sample/WebCache/Views/Home/Cache.cshtml)]

<span data-ttu-id="a6d22-132">已缓存`DateTime`值保持在缓存中，尽管在超时期限 （和由于内存压力没有逐出） 的请求。</span><span class="sxs-lookup"><span data-stu-id="a6d22-132">The cached `DateTime` value remains in the cache while there are requests within the timeout period (and no eviction due to memory pressure).</span></span> <span data-ttu-id="a6d22-133">下图显示当前时间以及从缓存中检索的较早时间：</span><span class="sxs-lookup"><span data-stu-id="a6d22-133">The following image shows the current time and an older time retrieved from the cache:</span></span>

![显示了两个不同时间的索引视图](memory/_static/time.png)

<span data-ttu-id="a6d22-135">下面的代码使用[GetOrCreate](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__)和[GetOrCreateAsync](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___)缓存数据。</span><span class="sxs-lookup"><span data-stu-id="a6d22-135">The following code uses [GetOrCreate](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__) and [GetOrCreateAsync](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___) to cache data.</span></span> 

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet2&highlight=3-7,14-19)]

<span data-ttu-id="a6d22-136">以下代码调用[Get](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.get#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_)来提取缓存的时间：</span><span class="sxs-lookup"><span data-stu-id="a6d22-136">The following code calls [Get](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions.get#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_) to fetch the cached time:</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_gct)]

<span data-ttu-id="a6d22-137">有关缓存方法的说明，请参阅[IMemoryCache 方法](/dotnet/api/microsoft.extensions.caching.memory.imemorycache)和[CacheExtensions 方法](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions)</span><span class="sxs-lookup"><span data-stu-id="a6d22-137">See [IMemoryCache methods](/dotnet/api/microsoft.extensions.caching.memory.imemorycache) and [CacheExtensions methods](/dotnet/api/microsoft.extensions.caching.memory.cacheextensions) for a description of the cache methods.</span></span>

## <a name="using-memorycacheentryoptions"></a><span data-ttu-id="a6d22-138">使用 MemoryCacheEntryOptions</span><span class="sxs-lookup"><span data-stu-id="a6d22-138">Using MemoryCacheEntryOptions</span></span>

<span data-ttu-id="a6d22-139">下面的示例执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a6d22-139">The following sample:</span></span>

- <span data-ttu-id="a6d22-140">设置绝对到期时间。</span><span class="sxs-lookup"><span data-stu-id="a6d22-140">Sets the absolute expiration time.</span></span> <span data-ttu-id="a6d22-141">这是条目可以被缓存的最长时间，防止可调过期持续更新时该条目过时太多。</span><span class="sxs-lookup"><span data-stu-id="a6d22-141">This is the maximum time the entry can be cached and prevents the item from becoming too stale when the sliding expiration is continuously renewed.</span></span>
- <span data-ttu-id="a6d22-142">设置可调过期时间。</span><span class="sxs-lookup"><span data-stu-id="a6d22-142">Sets a sliding expiration time.</span></span> <span data-ttu-id="a6d22-143">访问此缓存项的请求将重置可调过期时钟。</span><span class="sxs-lookup"><span data-stu-id="a6d22-143">Requests that access this cached item will reset the sliding expiration clock.</span></span>
- <span data-ttu-id="a6d22-144">将缓存优先级设置为`CacheItemPriority.NeverRemove`。</span><span class="sxs-lookup"><span data-stu-id="a6d22-144">Sets the cache priority to `CacheItemPriority.NeverRemove`.</span></span>
- <span data-ttu-id="a6d22-145">设置一个[PostEvictionDelegate](/dotnet/api/microsoft.extensions.caching.memory.postevictiondelegate)它将在条目从缓存中清除后调用。</span><span class="sxs-lookup"><span data-stu-id="a6d22-145">Sets a [PostEvictionDelegate](/dotnet/api/microsoft.extensions.caching.memory.postevictiondelegate) that will be called after the entry is evicted from the cache.</span></span> <span data-ttu-id="a6d22-146">在代码中运行该回调的线程不同于从缓存中移除条目的线程。</span><span class="sxs-lookup"><span data-stu-id="a6d22-146">The callback is run on a different thread from the code that removes the item from the cache.</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_et&highlight=14-21)]

## <a name="cache-dependencies"></a><span data-ttu-id="a6d22-147">缓存依赖项</span><span class="sxs-lookup"><span data-stu-id="a6d22-147">Cache dependencies</span></span>

<span data-ttu-id="a6d22-148">以下示例演示在依赖项过期时如何使缓存项过期。</span><span class="sxs-lookup"><span data-stu-id="a6d22-148">The following sample shows how to expire a cache entry if a dependent entry expires.</span></span> <span data-ttu-id="a6d22-149">会将 `CancellationChangeToken`添加到缓存项。</span><span class="sxs-lookup"><span data-stu-id="a6d22-149">A `CancellationChangeToken` is added to the cached item.</span></span> <span data-ttu-id="a6d22-150">在 `Cancel`上调用 `CancellationTokenSource`，时，这两个缓存条目都将被清除。</span><span class="sxs-lookup"><span data-stu-id="a6d22-150">When `Cancel` is called on the `CancellationTokenSource`, both cache entries are evicted.</span></span>

[!code-csharp[](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ed)]

<span data-ttu-id="a6d22-151">使用`CancellationTokenSource`可以将多个缓存条目作为一个组来清除。</span><span class="sxs-lookup"><span data-stu-id="a6d22-151">Using a `CancellationTokenSource` allows multiple cache entries to be evicted as a group.</span></span> <span data-ttu-id="a6d22-152">使用上面代码中的 `using`模式时`using`块中创建的缓存条目会继承触发器和过期时间设置。</span><span class="sxs-lookup"><span data-stu-id="a6d22-152">With the `using` pattern in the code above, cache entries created inside the `using` block will inherit triggers and expiration settings.</span></span>

## <a name="additional-notes"></a><span data-ttu-id="a6d22-153">附加说明</span><span class="sxs-lookup"><span data-stu-id="a6d22-153">Additional notes</span></span>

- <span data-ttu-id="a6d22-154">使用回调重新填充缓存项时：</span><span class="sxs-lookup"><span data-stu-id="a6d22-154">When using a callback to repopulate a cache item:</span></span>

  - <span data-ttu-id="a6d22-155">多个请求可能会发现缓存的键值为空，因为回调尚未完成。</span><span class="sxs-lookup"><span data-stu-id="a6d22-155">Multiple requests can find the cached key value empty because the callback hasn't completed.</span></span>
  - <span data-ttu-id="a6d22-156">这可能导致重新填充缓存的项的多个线程。</span><span class="sxs-lookup"><span data-stu-id="a6d22-156">This can result in several threads repopulating the cached item.</span></span>

- <span data-ttu-id="a6d22-157">使用一个缓存条目创建另一个缓存条目时，子条目会复制父条目的过期令牌以及基于时间的过期设置。</span><span class="sxs-lookup"><span data-stu-id="a6d22-157">When one cache entry is used to create another, the child copies the parent entry's expiration tokens and time-based expiration settings.</span></span> <span data-ttu-id="a6d22-158">子不过期通过手动删除或更新的父项。</span><span class="sxs-lookup"><span data-stu-id="a6d22-158">The child isn't expired by manual removal or updating of the parent entry.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6d22-159">其他资源</span><span class="sxs-lookup"><span data-stu-id="a6d22-159">Additional resources</span></span>

* [<span data-ttu-id="a6d22-160">使用分布式缓存</span><span class="sxs-lookup"><span data-stu-id="a6d22-160">Work with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="a6d22-161">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="a6d22-161">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="a6d22-162">响应缓存</span><span class="sxs-lookup"><span data-stu-id="a6d22-162">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="a6d22-163">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="a6d22-163">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="a6d22-164">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="a6d22-164">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="a6d22-165">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="a6d22-165">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
