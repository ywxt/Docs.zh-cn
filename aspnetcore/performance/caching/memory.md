---
title: "ASP.NET Core中的内存缓存"
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
# <a name="introduction-to-in-memory-caching-in-aspnet-core"></a>ASP.NET Core 中的内存缓存简介

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)， [John Luo](https://github.com/JunTaoLuo)，和[Steve Smith](https://ardalis.com/)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/memory/sample)([如何下载](xref:tutorials/index#how-to-download-a-sample))

## <a name="caching-basics"></a>缓存的基础知识

通过减少生成内容所需的工作，缓存可以显著提高应用程序的性能和可伸缩性。缓存对不经常更改的数据效果最佳。缓存生成的数据副本可以比从原始数据源更快地返回。您应编写并测试您的应用程序，以避免依赖缓存的数据。

ASP.NET Core 支持多种不同的缓存。最简单的缓存基于[IMemoryCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)，它表示存储在 web 服务器内存中的缓存。在多个服务器的服务器场上运行的应用程序应确保使用内存缓存时，会话是粘性的。粘性会话确保所有来自客户端的后续请求都会转到同一台服务器。例如，Azure Web 应用程序使用[应用程序请求路由](https://www.iis.net/learn/extensions/planning-for-arr)(ARR) 将所有的后续请求路由到同一台服务器。

Web 场中的非粘性会话需要[分布式缓存](distributed.md)以避免缓存一致性问题。对于某些应用程序，分布式缓存可以支持比内存缓存更高的横向扩展。 使用分布式缓存将缓存内存卸载到外部进程。 

除非[CacheItemPriority](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheitempriority)设置为`CacheItemPriority.NeverRemove`，否则`IMemoryCache`缓存将在内存压力下清除缓存条目。您可以设置`CacheItemPriority`调整缓存在内存压力下清除项目的优先级。

内存缓存可以存储任何对象；分布式缓存接口仅限于`byte[]`。

## <a name="using-imemorycache"></a>使用 IMemoryCache

内存缓存是使用[依赖关系注入](../../fundamentals/dependency-injection.md)从您的应用程序中引用的*服务*。 在`ConfigureServices`中调用`AddMemoryCache`:

[!code-csharp[Main](memory/sample/WebCache/Startup.cs?highlight=8)] 

在构造函数中请求`IMemoryCache`实例：

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ctor&highlight=3,5-)] 

`IMemoryCache`需要 NuGet 包"Microsoft.Extensions.Caching.Memory"。

下面的代码使用[TryGetValue](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache#Microsoft_Extensions_Caching_Memory_IMemoryCache_TryGetValue_System_Object_System_Object__)检查当前时间是否在缓存中。 如果未缓存该项，则创建一个新条目并使用[Set](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Set__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object___0_)添加到缓存中。

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet1)]

当前时间和缓存的时间显示如下：

[!code-html[Main](memory/sample/WebCache/Views/Home/Cache.cshtml)]

在超时期限内（和由于内存压力没有清除）有请求的时候，已缓存的`DateTime`的值将保留在缓存中。下图显示当前时间和从缓存中检索的较早时间：

![具有两个不同时间显示的索引视图](memory/_static/time.png)

下面的代码使用[GetOrCreate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreate__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry___0__)和[GetOrCreateAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_GetOrCreateAsync__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_System_Func_Microsoft_Extensions_Caching_Memory_ICacheEntry_System_Threading_Tasks_Task___0___)缓存数据。 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet2&highlight=3-7,14-19)]

下面的代码调用[Get](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions#Microsoft_Extensions_Caching_Memory_CacheExtensions_Get__1_Microsoft_Extensions_Caching_Memory_IMemoryCache_System_Object_)获取缓存的时间：

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_gct)]

有关缓存方法的说明，请参阅[IMemoryCache 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.imemorycache)和[CacheExtensions 方法](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.cacheextensions)。

## <a name="using-memorycacheentryoptions"></a>使用 MemoryCacheEntryOptions

以下示例：

- 设置绝对到期时间。 这是条目可以被缓存的最长时间，可防止可调过期持续更新时该条目变得过时。
- 设置可调过期时间。 访问此缓存项的请求将重置可调过期时钟。
- 将缓存优先级设置为`CacheItemPriority.NeverRemove`。 
- 设置一个[PostEvictionDelegate](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.memory.postevictiondelegate)，它将在条目从缓存中清除后调用。 该回调在与从缓存中移除条目的代码不同的线程上运行。

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_et&highlight=14-20)]

## <a name="cache-dependencies"></a>缓存依赖项

下面的示例演示如果依赖项过期时如何使缓存项过期。将`CancellationChangeToken`添加到缓存项。当在`CancellationTokenSource`上调用`Cancel`时，这两个缓存条目都将被清除。 

[!code-csharp[Main](memory/sample/WebCache/Controllers/HomeController.cs?name=snippet_ed)]

使用`CancellationTokenSource`允许将多个缓存条目作为一个组被清除。使用上面代码中的`using`模式，在`using`块内部创建的缓存条目将继承触发器和过期时间设置。

### <a name="additional-notes"></a>附加说明

- 当使用回调以重新填充缓存项时：

  - 多个请求可以找到为空的缓存键值，因为回调尚未完成。 
  - 这可能导致多个线程重新填充缓存项。

- 当一个缓存条目用于创建另一个时，子级会复制父项的过期令牌和基于时间的过期时间设置。通过手动删除或更新父项，子级不会过期。

### <a name="other-resources"></a>其他资源

* [使用分布式缓存](xref:performance/caching/distributed)
* [使用更改令牌检测更改](xref:fundamentals/primitives/change-tokens)
* [响应缓存](xref:performance/caching/response)
* [响应缓存中间件](xref:performance/caching/middleware)
* [缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [分布式缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
