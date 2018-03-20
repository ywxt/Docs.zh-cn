---
title: "ASP .NET Core 中的内存中缓存"
author: rick-anderson
description: "演示如何在 ASP.NET Core 中的内存中缓存数据。"
keywords: "ASP.NET Core，缓存中的内存性能"
ms.author: riande
manager: wpickett
ms.date: 12/14/2016
ms.topic: article
ms.assetid: 819511cf-d33e-410a-b5a9-bef7fa64d2f3
ms.technology: aspnet
ms.prod: asp.net-core
uid: performance/caching/memory
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce865427b6ca44c76888908fdeea9cd45c881c4
ms.sourcegitcommit: 732cd2684246e49e796836596643a8d37e20c46d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2017
---
# <a name="introduction-to-in-memory-caching-in-aspnet-core"></a>ASP .NET Core 中的内存中缓存简介

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)、[John Luo](https://github.com/JunTaoLuo) 和 [Steve Smith](https://ardalis.com/)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample)([如何下载](xref:tutorials/index#how-to-download-a-sample))

## <a name="caching-basics"></a>缓存的基础知识

通过减少生成内容所需的工作，缓存可以显著提高应用的性能和可伸缩性。缓存对不经常更改的数据效果最佳。缓存生成的数据副本的返回速度可以比从原始源返回更快。在编写并测试应用时，应避免依赖缓存的数据。

ASP.NET Core 支持多种不同的缓存。最简单的缓存基于[IMemoryCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)，它表示存储在 web 服务器内存中的缓存。在多个服务器的服务器场上运行的应用程序应确保使用内存缓存时，会话是粘性的。粘性会话确保所有来自客户端的后续请求都会转到同一台服务器。例如，Azure Web 应用程序使用[应用程序请求路由](https://www.iis.net/learn/extensions/planning-for-arr)(ARR) 将所有的后续请求路由到同一台服务器。

Web 场中的非粘性会话需要[分布式缓存](distributed.md)以避免缓存一致性问题。对于某些应用来说，分布式缓存可以支持比内存中缓存更高程度的横向扩展。使用分布式缓存可将缓存内存卸载到外部进程。

除非将 [CacheItemPriority](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheitempriority) 设置为 `CacheItemPriority.NeverRemove`，否则`IMemoryCache` 缓存会在内存压力下清除缓存条目。可以通过设置 `CacheItemPriority` 来调整缓存在内存压力下清除项目的优先级。

内存中缓存可以存储任何对象；分布式缓存接口仅限于 `byte[]`。

## <a name="using-imemorycache"></a>使用 IMemoryCache

内存中缓存是使用[依赖关系注入](../../fundamentals/dependency-injection.md)从应用中引用的服务**。请在 `ConfigureServices` 中调用 `AddMemoryCache`：

[!code-csharp[Main](memory/sample/WebCache/Startup.cs?highlight=8)] 

在构造函数中请求 `IMemoryCache` 实例：

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ctor&highlight=3,5-)] 

`IMemoryCache`需要 NuGet 包"Microsoft.Extensions.Caching.Memory"。

以下代码使用 [TryGetValue](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__) 检查是否对时间进行了缓存。如果未缓存时间，则会创建一个新条目并使用 [Set](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_) 将其添加到缓存中。

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet1)]

将会显示当前时间和缓存的时间：

[!code-html[Main](memory/sample/WebCache/Views/Home/Cache.cshtml)]

在超时期限内，只要有请求，缓存的 `DateTime` 值就会保留在缓存中（不会因为内存压力而将其清除）。下图显示当前时间以及从缓存中检索的较早时间：

![显示了两个不同时间的索引视图](memory/_static/time.png)

下面的代码使用[GetOrCreate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__)和[GetOrCreateAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___)缓存数据。 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet2&highlight=3-7,14-19)]

以下代码调用 [Get](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_) 来提取缓存的时间：

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_gct)]

有关缓存方法的说明，请参阅 [IMemoryCache 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)和 [CacheExtensions 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions)。

## <a name="using-memorycacheentryoptions"></a>使用 MemoryCacheEntryOptions

下面的示例执行以下操作：

- 设置绝对到期时间。这是条目可以被缓存的最长时间，防止可调过期持续更新时该条目过时太多。
- 设置可调过期时间。 访问此缓存项的请求将重置可调过期时钟。
- 将缓存优先级设置为`CacheItemPriority.NeverRemove`。 
- 设置一个 [PostEvictionDelegate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.postevictiondelegate)，它将在条目从缓存中清除后调用。在代码中运行该回调的线程不同于从缓存中移除条目的线程。

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_et&highlight=14-20)]

## <a name="cache-dependencies"></a>缓存依赖项

以下示例演示在依赖项过期时如何使缓存项过期。会将 `CancellationChangeToken`添加到缓存项。在 `CancellationTokenSource` 上调用 `Cancel` 时，这两个缓存条目都将被清除。 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ed)]

使用 `CancellationTokenSource` 可以将多个缓存条目作为一个组来清除。使用上面代码中的 `using` 模式时，在 `using` 块中创建的缓存条目会继承触发器和过期时间设置。

### <a name="additional-notes"></a>附加说明

- 使用回调重新填充缓存项时：

  - 多个请求可能会发现缓存的键值为空，因为回调尚未完成。
  - 这可能导致多个线程重新填充缓存项。

- 使用一个缓存条目创建另一个缓存条目时，子条目会复制父条目的过期令牌以及基于时间的过期设置。手动删除或更新父条目不会导致子条目过期。

### <a name="other-resources"></a>其他资源

* [使用分布式缓存](xref:performance/caching/distributed)
* [使用更改令牌检测更改](xref:fundamentals/primitives/change-tokens)
* [响应缓存](xref:performance/caching/response)
* [响应缓存中间件](xref:performance/caching/middleware)
* [缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [分布式缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
