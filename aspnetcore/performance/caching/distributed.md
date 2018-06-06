---
title: 使用 ASP.NET Core 中分布式缓存
author: ardalis
description: 了解如何使用 ASP.NET Core 分布式缓存以提高应用性能和可伸缩性，尤其是在云或服务器场环境。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/distributed
ms.openlocfilehash: 6c595572641604d241c0c8f702d4f392afe34f71
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34734453"
---
# <a name="work-with-a-distributed-cache-in-aspnet-core"></a><span data-ttu-id="e18f4-103">使用 ASP.NET Core 中分布式缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-103">Work with a distributed cache in ASP.NET Core</span></span>

<span data-ttu-id="e18f4-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="e18f4-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="e18f4-105">分布式缓存可以提高 ASP.NET Core 应用的性能和可伸缩性，尤其是托管在云或服务器场环境中时。</span><span class="sxs-lookup"><span data-stu-id="e18f4-105">Distributed caches can improve the performance and scalability of ASP.NET Core apps, especially when hosted in a cloud or server farm environment.</span></span> <span data-ttu-id="e18f4-106">本文解释了如何使用 ASP.NET Core 的内置分布式缓存抽象和实现。</span><span class="sxs-lookup"><span data-stu-id="e18f4-106">This article explains how to work with ASP.NET Core's built-in distributed cache abstractions and implementations.</span></span>

<span data-ttu-id="e18f4-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="e18f4-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-a-distributed-cache"></a><span data-ttu-id="e18f4-108">什么是分布式的缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-108">What is a distributed cache</span></span>

<span data-ttu-id="e18f4-109">分布式的缓存共享由多个应用程序服务器 (请参阅[缓存基础知识](memory.md#caching-basics))。</span><span class="sxs-lookup"><span data-stu-id="e18f4-109">A distributed cache is shared by multiple app servers (see [Cache Basics](memory.md#caching-basics)).</span></span> <span data-ttu-id="e18f4-110">缓存中的信息不存储在单独的 Web 服务器的内存中，并且缓存的数据可用于所有应用服务器。这具有几个优点：</span><span class="sxs-lookup"><span data-stu-id="e18f4-110">The information in the cache isn't stored in the memory of individual web servers, and the cached data is available to all of the app's servers.</span></span> <span data-ttu-id="e18f4-111">这提供了几个优点：</span><span class="sxs-lookup"><span data-stu-id="e18f4-111">This provides several advantages:</span></span>

1. <span data-ttu-id="e18f4-112">所有 Web 服务器上的缓存数据都是一致的。</span><span class="sxs-lookup"><span data-stu-id="e18f4-112">Cached data is coherent on all web servers.</span></span> <span data-ttu-id="e18f4-113">用户不会因处理其请求的 Web 服务器的不同而看到不同的结果</span><span class="sxs-lookup"><span data-stu-id="e18f4-113">Users don't see different results depending on which web server handles their request</span></span>

2. <span data-ttu-id="e18f4-114">缓存的数据在 Web 服务器重新启动后和部署后仍然存在。</span><span class="sxs-lookup"><span data-stu-id="e18f4-114">Cached data survives web server restarts and deployments.</span></span> <span data-ttu-id="e18f4-115">删除或添加单独的 Web 服务器不会影响缓存。</span><span class="sxs-lookup"><span data-stu-id="e18f4-115">Individual web servers can be removed or added without impacting the cache.</span></span>

3. <span data-ttu-id="e18f4-116">源数据存储区具有对它 （不是使用多个内存中缓存或否缓存根本） 发出的少数几个请求。</span><span class="sxs-lookup"><span data-stu-id="e18f4-116">The source data store has fewer requests made to it (than with multiple in-memory caches or no cache at all).</span></span>

> [!NOTE]
> <span data-ttu-id="e18f4-117">如果使用 SQL Server 分布式缓存，则其中一些优势只有在为缓存而不是应用的源数据使用单独的数据库实例的情况下才会体现出来。</span><span class="sxs-lookup"><span data-stu-id="e18f4-117">If using a SQL Server Distributed Cache, some of these advantages are only true if a separate database instance is used for the cache than for the app's source data.</span></span>

<span data-ttu-id="e18f4-118">像任何缓存一样，分布式缓存可以显著提高应用的响应速度，因为通常情况下，数据从缓存中检索比从关系数据库（或 Web 服务）中检索快得多。</span><span class="sxs-lookup"><span data-stu-id="e18f4-118">Like any cache, a distributed cache can dramatically improve an app's responsiveness, since typically data can be retrieved from the cache much faster than from a relational database (or web service).</span></span>

<span data-ttu-id="e18f4-119">缓存配置是特定于实现的。</span><span class="sxs-lookup"><span data-stu-id="e18f4-119">Cache configuration is implementation specific.</span></span> <span data-ttu-id="e18f4-120">本文介绍如何配置 Redis 和 SQL Server 分布式缓存。</span><span class="sxs-lookup"><span data-stu-id="e18f4-120">This article describes how to configure both Redis and SQL Server distributed caches.</span></span> <span data-ttu-id="e18f4-121">无论选择哪一种实现，应用都使用通用的 `IDistributedCache` 接口与缓存交互。</span><span class="sxs-lookup"><span data-stu-id="e18f4-121">Regardless of which implementation is selected, the app interacts with the cache using a common `IDistributedCache` interface.</span></span>

## <a name="the-idistributedcache-interface"></a><span data-ttu-id="e18f4-122">IDistributedCache 接口</span><span class="sxs-lookup"><span data-stu-id="e18f4-122">The IDistributedCache Interface</span></span>

<span data-ttu-id="e18f4-123">`IDistributedCache`接口包含同步和异步方法。</span><span class="sxs-lookup"><span data-stu-id="e18f4-123">The `IDistributedCache` interface includes synchronous and asynchronous methods.</span></span> <span data-ttu-id="e18f4-124">接口允许在分布式缓存实现中添加、检索和删除项。</span><span class="sxs-lookup"><span data-stu-id="e18f4-124">The interface allows items to be added, retrieved, and removed from the distributed cache implementation.</span></span> <span data-ttu-id="e18f4-125">`IDistributedCache`接口包含以下方法：</span><span class="sxs-lookup"><span data-stu-id="e18f4-125">The `IDistributedCache` interface includes the following methods:</span></span>

<span data-ttu-id="e18f4-126">**Get、 GetAsync**</span><span class="sxs-lookup"><span data-stu-id="e18f4-126">**Get, GetAsync**</span></span>

<span data-ttu-id="e18f4-127">采用字符串键并以`byte[]`形式检索缓存项（如果在缓存中找到）。</span><span class="sxs-lookup"><span data-stu-id="e18f4-127">Takes a string key and retrieves a cached item as a `byte[]` if found in the cache.</span></span>

<span data-ttu-id="e18f4-128">**Set、SetAsync**</span><span class="sxs-lookup"><span data-stu-id="e18f4-128">**Set, SetAsync**</span></span>

<span data-ttu-id="e18f4-129">使用字符串键向缓存添加项`byte[]`形式）。 </span><span class="sxs-lookup"><span data-stu-id="e18f4-129">Adds an item (as `byte[]`) to the cache using a string key.</span></span>

<span data-ttu-id="e18f4-130">**Refresh、RefreshAsync**</span><span class="sxs-lookup"><span data-stu-id="e18f4-130">**Refresh, RefreshAsync**</span></span>

<span data-ttu-id="e18f4-131">根据键刷新缓存中的项，并重置其可调过期超时值（如果有）。</span><span class="sxs-lookup"><span data-stu-id="e18f4-131">Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>

<span data-ttu-id="e18f4-132">**Remove、RemoveAsync**</span><span class="sxs-lookup"><span data-stu-id="e18f4-132">**Remove, RemoveAsync**</span></span>

<span data-ttu-id="e18f4-133">根据键删除缓存项。</span><span class="sxs-lookup"><span data-stu-id="e18f4-133">Removes a cache entry based on its key.</span></span>

<span data-ttu-id="e18f4-134">若要使用`IDistributedCache`接口：</span><span class="sxs-lookup"><span data-stu-id="e18f4-134">To use the `IDistributedCache` interface:</span></span>

   1. <span data-ttu-id="e18f4-135">所需的 NuGet 包添加到项目文件。</span><span class="sxs-lookup"><span data-stu-id="e18f4-135">Add the required NuGet packages to your project file.</span></span>

   2. <span data-ttu-id="e18f4-136">在`Startup`类的`ConfigureServices`方法中配置`IDistributedCache`的具体实现，并将其添加到该处的容器中。</span><span class="sxs-lookup"><span data-stu-id="e18f4-136">Configure the specific implementation of `IDistributedCache` in your `Startup` class's `ConfigureServices` method, and add it to the container there.</span></span>

   3. <span data-ttu-id="e18f4-137">在应用的[中间件](xref:fundamentals/middleware/index)或 MVC 控制器类中，从构造函数请求 `IDistributedCache`的实例。</span><span class="sxs-lookup"><span data-stu-id="e18f4-137">From the app's [Middleware](xref:fundamentals/middleware/index) or MVC controller classes, request an instance of `IDistributedCache` from the constructor.</span></span> <span data-ttu-id="e18f4-138">实例将通过[依赖项注入](../../fundamentals/dependency-injection.md) (DI) 提供。</span><span class="sxs-lookup"><span data-stu-id="e18f4-138">The instance will be provided by [Dependency Injection](../../fundamentals/dependency-injection.md) (DI).</span></span>

> [!NOTE]
> <span data-ttu-id="e18f4-139">无需为`IDistributedCache`实例使用 Singleton 或 Scoped 生命周期（至少对内置实现来说是这样的）。</span><span class="sxs-lookup"><span data-stu-id="e18f4-139">There's no need to use a Singleton or Scoped lifetime for `IDistributedCache` instances (at least for the built-in implementations).</span></span> <span data-ttu-id="e18f4-140">你还可以创建一个实例，只要你可能需要一个 (而不是使用[依赖关系注入](../../fundamentals/dependency-injection.md))，但这会导致你的代码更难若要测试，并且与冲突[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。</span><span class="sxs-lookup"><span data-stu-id="e18f4-140">You can also create an instance wherever you might need one (instead of using [Dependency Injection](../../fundamentals/dependency-injection.md)), but this can make your code harder to test, and violates the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span>

<span data-ttu-id="e18f4-141">下面的示例演示如何在简单的中间件组件中使用`IDistributedCache` 实例：</span><span class="sxs-lookup"><span data-stu-id="e18f4-141">The following example shows how to use an instance of `IDistributedCache` in a simple middleware component:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/StartTimeHeader.cs)]

<span data-ttu-id="e18f4-142">在上面的代码中，缓存值用于读取，不用于写入。</span><span class="sxs-lookup"><span data-stu-id="e18f4-142">In the code above, the cached value is read, but never written.</span></span> <span data-ttu-id="e18f4-143">在此示例中，该值仅在服务器启动时设置，并且不会更改。</span><span class="sxs-lookup"><span data-stu-id="e18f4-143">In this sample, the value is only set when a server starts up, and doesn't change.</span></span> <span data-ttu-id="e18f4-144">在多服务器方案中，要启动的最新服务器会覆盖由其他服务器设置的以前的任何值。</span><span class="sxs-lookup"><span data-stu-id="e18f4-144">In a multi-server scenario, the most recent server to start will overwrite any previous values that were set by other servers.</span></span> <span data-ttu-id="e18f4-145">`Get`和`Set`方法使用 `byte[]`类型。</span><span class="sxs-lookup"><span data-stu-id="e18f4-145">The `Get` and `Set` methods use the `byte[]` type.</span></span> <span data-ttu-id="e18f4-146">因此，字符串值必须使用 `Encoding.UTF8.GetString`(适用于`Get`) 和 `Encoding.UTF8.GetBytes`(适用于 `Set`)进行转换。</span><span class="sxs-lookup"><span data-stu-id="e18f4-146">Therefore, the string value must be converted using `Encoding.UTF8.GetString` (for `Get`) and `Encoding.UTF8.GetBytes` (for `Set`).</span></span>

<span data-ttu-id="e18f4-147">*Startup.cs*中的以下代码显示要设置的值：</span><span class="sxs-lookup"><span data-stu-id="e18f4-147">The following code from *Startup.cs* shows the value being set:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="e18f4-148">由于`IDistributedCache`是在`ConfigureServices`方法中配置的，因此它可以作为参数提供给`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="e18f4-148">Since `IDistributedCache` is configured in the `ConfigureServices` method, it's available to the `Configure` method as a parameter.</span></span> <span data-ttu-id="e18f4-149">将其添加作为参数将允许通过 DI 提供配置的实例。</span><span class="sxs-lookup"><span data-stu-id="e18f4-149">Adding it as a parameter will allow the configured instance to be provided through DI.</span></span>

## <a name="using-a-redis-distributed-cache"></a><span data-ttu-id="e18f4-150">使用分布式的 Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-150">Using a Redis distributed cache</span></span>

<span data-ttu-id="e18f4-151">[Redis](https://redis.io/)是一种开源的内存中数据存储，通常用作分布式缓存。</span><span class="sxs-lookup"><span data-stu-id="e18f4-151">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="e18f4-152">可以在本地使用它，并且可以为 Azure 托管的 ASP.NET Core 应用配置[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)为你的 Azure 托管的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="e18f4-152">You can use it locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for your Azure-hosted ASP.NET Core apps.</span></span> <span data-ttu-id="e18f4-153">ASP.NET Core 应用使用 `RedisDistributedCache`实例配置缓存实现。</span><span class="sxs-lookup"><span data-stu-id="e18f4-153">Your ASP.NET Core app configures the cache implementation using a `RedisDistributedCache` instance.</span></span>

<span data-ttu-id="e18f4-154">可在`ConfigureServices`中配置 Redis 实现，并可通过请求`IDistributedCache`实例（请参阅上面的代码）在应用代码中访问它。</span><span class="sxs-lookup"><span data-stu-id="e18f4-154">You configure the Redis implementation in `ConfigureServices` and access it in your app code by requesting an instance of `IDistributedCache` (see the code above).</span></span>

<span data-ttu-id="e18f4-155">在示例代码中，为`RedisCache`环境配置服务器时使用`Staging`实现。</span><span class="sxs-lookup"><span data-stu-id="e18f4-155">In the sample code, a `RedisCache` implementation is used when the server is configured for a `Staging` environment.</span></span> <span data-ttu-id="e18f4-156">因此，`ConfigureStagingServices`方法用于配置 `RedisCache`:</span><span class="sxs-lookup"><span data-stu-id="e18f4-156">Thus the `ConfigureStagingServices` method configures the `RedisCache`:</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet2)]

> [!NOTE]
> <span data-ttu-id="e18f4-157">若要在本地计算机上安装 Redis，安装 chocolatey 程序包[ https://chocolatey.org/packages/redis-64/ ](https://chocolatey.org/packages/redis-64/)并运行`redis-server`从命令提示符。</span><span class="sxs-lookup"><span data-stu-id="e18f4-157">To install Redis on your local machine, install the chocolatey package [https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/) and run `redis-server` from a command prompt.</span></span>

## <a name="using-a-sql-server-distributed-cache"></a><span data-ttu-id="e18f4-158">使用 SQL Server 分布式缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-158">Using a SQL Server distributed cache</span></span>

<span data-ttu-id="e18f4-159">SqlServerCache 实现允许分布式缓存使用 SQL Server 数据库作为其后备存储。</span><span class="sxs-lookup"><span data-stu-id="e18f4-159">The SqlServerCache implementation allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="e18f4-160">若要创建 SQL Server 表，可以使用 sql-cache 工具，该工具将使用指定的名称和模式创建一个表。</span><span class="sxs-lookup"><span data-stu-id="e18f4-160">To create SQL Server table you can use sql-cache tool, the tool creates a table with the name and schema you specify.</span></span>

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="e18f4-161">添加`SqlConfig.Tools`到`<ItemGroup>`元素的项目文件和运行`dotnet restore`。</span><span class="sxs-lookup"><span data-stu-id="e18f4-161">Add `SqlConfig.Tools` to the `<ItemGroup>` element of the project file and run `dotnet restore`.</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.Extensions.Caching.SqlConfig.Tools" 
                          Version="2.0.2" />
</ItemGroup>
```

::: moniker-end

<span data-ttu-id="e18f4-162">通过运行以下命令来测试 SqlConfig.Tools:</span><span class="sxs-lookup"><span data-stu-id="e18f4-162">Test SqlConfig.Tools by running the following command:</span></span>

```console
dotnet sql-cache create --help
```

<span data-ttu-id="e18f4-163">SqlConfig.Tools 显示使用情况、 选项和命令的帮助。</span><span class="sxs-lookup"><span data-stu-id="e18f4-163">SqlConfig.Tools displays usage, options, and command help.</span></span>

<span data-ttu-id="e18f4-164">在 SQL Server 中创建表，通过运行`sql-cache create`命令：</span><span class="sxs-lookup"><span data-stu-id="e18f4-164">Create a table in SQL Server by running the `sql-cache create` command :</span></span>

```console
dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
Table and index were created successfully.
```

<span data-ttu-id="e18f4-165">创建的表具有以下架构：</span><span class="sxs-lookup"><span data-stu-id="e18f4-165">The created table has the following schema:</span></span>

![Sql Server 缓存表](distributed/_static/SqlServerCacheTable.png)

<span data-ttu-id="e18f4-167">像所有缓存实现一样，应用应该使用`IDistributedCache`，实例来获取和设置缓存值，而不是使用`SqlServerCache`实例。</span><span class="sxs-lookup"><span data-stu-id="e18f4-167">Like all cache implementations, your app should get and set cache values using an instance of `IDistributedCache`, not a `SqlServerCache`.</span></span> <span data-ttu-id="e18f4-168">此示例实现`SqlServerCache`在生产环境中 (以便在配置`ConfigureProductionServices`)。</span><span class="sxs-lookup"><span data-stu-id="e18f4-168">The sample implements `SqlServerCache` in the Production environment (so it's configured in `ConfigureProductionServices`).</span></span>

[!code-csharp[](distributed/sample/src/DistCacheSample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="e18f4-169">`ConnectionString` (以及可选的`SchemaName`和`TableName`) 通常应该存储在源代码管理之外（例如存储在 UserSecrets 中），因为它们可能包含凭据。</span><span class="sxs-lookup"><span data-stu-id="e18f4-169">The `ConnectionString` (and optionally, `SchemaName` and `TableName`) should typically be stored outside of source control (such as UserSecrets), as they may contain credentials.</span></span>

## <a name="recommendations"></a><span data-ttu-id="e18f4-170">建议</span><span class="sxs-lookup"><span data-stu-id="e18f4-170">Recommendations</span></span>

<span data-ttu-id="e18f4-171">在决定哪种`IDistributedCache`实现适合应用时，请根据现有的基础架构和环境、性能要求和团队经验在 Redis 和 SQL Server 之间进行选择。</span><span class="sxs-lookup"><span data-stu-id="e18f4-171">When deciding which implementation of `IDistributedCache` is right for your app, choose between Redis and SQL Server based on your existing infrastructure and environment, your performance requirements, and your team's experience.</span></span> <span data-ttu-id="e18f4-172">如果团队更喜欢使用 Redis，那就使用它。</span><span class="sxs-lookup"><span data-stu-id="e18f4-172">If your team is more comfortable working with Redis, it's an excellent choice.</span></span> <span data-ttu-id="e18f4-173">如果团队倾向于 SQL Server，那么也应对这么做充满信心。</span><span class="sxs-lookup"><span data-stu-id="e18f4-173">If your team prefers SQL Server, you can be confident in that implementation as well.</span></span> <span data-ttu-id="e18f4-174">请注意，传统的缓存解决方案将存储数据的内存中用于进行快速检索的数据。</span><span class="sxs-lookup"><span data-stu-id="e18f4-174">Note that a traditional caching solution stores data in-memory which allows for fast retrieval of data.</span></span> <span data-ttu-id="e18f4-175">应该将常用数据存储在缓存中，将整个数据存储在后端持久性存储（如 SQL Server 或 Azure 存储）中。</span><span class="sxs-lookup"><span data-stu-id="e18f4-175">You should store commonly used data in a cache and store the entire data in a backend persistent store such as SQL Server or Azure Storage.</span></span> <span data-ttu-id="e18f4-176">与 SQL Cache 相比，Redis Cache 是一种吞吐量高且延迟轻微的缓存解决方案。</span><span class="sxs-lookup"><span data-stu-id="e18f4-176">Redis Cache is a caching solution which gives you high throughput and low latency as compared to SQL Cache.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e18f4-177">其他资源</span><span class="sxs-lookup"><span data-stu-id="e18f4-177">Additional resources</span></span>

* [<span data-ttu-id="e18f4-178">Redis 在 Azure 上的缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-178">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="e18f4-179">在 Azure 上的 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="e18f4-179">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="e18f4-180">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-180">Cache in-memory</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="e18f4-181">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="e18f4-181">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="e18f4-182">响应缓存</span><span class="sxs-lookup"><span data-stu-id="e18f4-182">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="e18f4-183">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="e18f4-183">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="e18f4-184">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="e18f4-184">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="e18f4-185">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="e18f4-185">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
