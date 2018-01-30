---
title: "使用 ASP.NET Core 中分布式缓存"
author: ardalis
description: "了解如何使用分布式缓存来提高性能和可伸缩性的 ASP.NET Core 应用，尤其是在托管在云中或服务器场环境中时，才。"
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/distributed
ms.openlocfilehash: 86fd40863f6eeef3c129335141d704769d36b4c1
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="working-with-a-distributed-cache-in-aspnet-core"></a><span data-ttu-id="34004-103">使用 ASP.NET Core 中分布式缓存</span><span class="sxs-lookup"><span data-stu-id="34004-103">Working with a distributed cache in ASP.NET Core</span></span>

<span data-ttu-id="34004-104">通过[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="34004-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="34004-105">分布式的缓存可以提高性能和可伸缩性的 ASP.NET Core 应用，尤其是在托管在云中或服务器场环境中。</span><span class="sxs-lookup"><span data-stu-id="34004-105">Distributed caches can improve the performance and scalability of ASP.NET Core apps, especially when hosted in a cloud or server farm environment.</span></span> <span data-ttu-id="34004-106">此文章介绍了如何使用 ASP.NET 核心内置的分布式的缓存抽象和实现。</span><span class="sxs-lookup"><span data-stu-id="34004-106">This article explains how to work with ASP.NET Core's built-in distributed cache abstractions and implementations.</span></span>

<span data-ttu-id="34004-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="34004-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-a-distributed-cache"></a><span data-ttu-id="34004-108">什么是分布式的缓存</span><span class="sxs-lookup"><span data-stu-id="34004-108">What is a distributed cache</span></span>

<span data-ttu-id="34004-109">分布式的缓存共享由多个应用程序服务器 (请参阅[缓存的基础知识](memory.md#caching-basics))。</span><span class="sxs-lookup"><span data-stu-id="34004-109">A distributed cache is shared by multiple app servers (see [Caching Basics](memory.md#caching-basics)).</span></span> <span data-ttu-id="34004-110">在缓存中的信息不存储在单独的 web 服务器的内存和缓存的数据可供所有应用程序的服务器。</span><span class="sxs-lookup"><span data-stu-id="34004-110">The information in the cache isn't stored in the memory of individual web servers, and the cached data is available to all of the app's servers.</span></span> <span data-ttu-id="34004-111">这提供了几个优点：</span><span class="sxs-lookup"><span data-stu-id="34004-111">This provides several advantages:</span></span>

1. <span data-ttu-id="34004-112">缓存的数据是所有 web 服务器上一致。</span><span class="sxs-lookup"><span data-stu-id="34004-112">Cached data is coherent on all web servers.</span></span> <span data-ttu-id="34004-113">用户看不到不同的结果，具体取决于哪个 web 服务器处理他们的请求</span><span class="sxs-lookup"><span data-stu-id="34004-113">Users don't see different results depending on which web server handles their request</span></span>

2. <span data-ttu-id="34004-114">缓存的数据在 web 服务器重新启动和部署能存在。</span><span class="sxs-lookup"><span data-stu-id="34004-114">Cached data survives web server restarts and deployments.</span></span> <span data-ttu-id="34004-115">单独的 web 服务器可以删除或添加而不会影响缓存。</span><span class="sxs-lookup"><span data-stu-id="34004-115">Individual web servers can be removed or added without impacting the cache.</span></span>

3. <span data-ttu-id="34004-116">源数据存储区具有对它 （不是使用多个内存中缓存或否缓存根本） 发出的少数几个请求。</span><span class="sxs-lookup"><span data-stu-id="34004-116">The source data store has fewer requests made to it (than with multiple in-memory caches or no cache at all).</span></span>

> [!NOTE]
> <span data-ttu-id="34004-117">如果使用 SQL Server 分发的缓存，但某些带来如下好处是仅当对应用程序的源数据的缓存比使用单独的数据库实例，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="34004-117">If using a SQL Server Distributed Cache, some of these advantages are only true if a separate database instance is used for the cache than for the app's source data.</span></span>

<span data-ttu-id="34004-118">任何缓存，如分布式的缓存可以显著提高应用的响应能力，因为通常可以从比快得多的关系数据库 （或 web 服务） 从缓存中检索数据。</span><span class="sxs-lookup"><span data-stu-id="34004-118">Like any cache, a distributed cache can dramatically improve an app's responsiveness, since typically data can be retrieved from the cache much faster than from a relational database (or web service).</span></span>

<span data-ttu-id="34004-119">缓存配置是特定的实现。</span><span class="sxs-lookup"><span data-stu-id="34004-119">Cache configuration is implementation specific.</span></span> <span data-ttu-id="34004-120">本文介绍如何配置同时 Redis 和 SQL Server 分布式缓存。</span><span class="sxs-lookup"><span data-stu-id="34004-120">This article describes how to configure both Redis and SQL Server distributed caches.</span></span> <span data-ttu-id="34004-121">无论选择哪一种实现，则应用程序与使用一组公共缓存交互`IDistributedCache`接口。</span><span class="sxs-lookup"><span data-stu-id="34004-121">Regardless of which implementation is selected, the app interacts with the cache using a common `IDistributedCache` interface.</span></span>

## <a name="the-idistributedcache-interface"></a><span data-ttu-id="34004-122">IDistributedCache 接口</span><span class="sxs-lookup"><span data-stu-id="34004-122">The IDistributedCache Interface</span></span>

<span data-ttu-id="34004-123">`IDistributedCache`接口包含同步和异步方法。</span><span class="sxs-lookup"><span data-stu-id="34004-123">The `IDistributedCache` interface includes synchronous and asynchronous methods.</span></span> <span data-ttu-id="34004-124">接口允许添加、 检索和删除从分布式的缓存实现的项。</span><span class="sxs-lookup"><span data-stu-id="34004-124">The interface allows items to be added, retrieved, and removed from the distributed cache implementation.</span></span> <span data-ttu-id="34004-125">`IDistributedCache`接口包括以下方法：</span><span class="sxs-lookup"><span data-stu-id="34004-125">The `IDistributedCache` interface includes the following methods:</span></span>

<span data-ttu-id="34004-126">**Get、 GetAsync**</span><span class="sxs-lookup"><span data-stu-id="34004-126">**Get, GetAsync**</span></span>

<span data-ttu-id="34004-127">采用字符串键和检索缓存的项作为`byte[]`如果缓存中找到。</span><span class="sxs-lookup"><span data-stu-id="34004-127">Takes a string key and retrieves a cached item as a `byte[]` if found in the cache.</span></span>

<span data-ttu-id="34004-128">**集 SetAsync**</span><span class="sxs-lookup"><span data-stu-id="34004-128">**Set, SetAsync**</span></span>

<span data-ttu-id="34004-129">添加一项 (作为`byte[]`) 到使用字符串键的缓存。</span><span class="sxs-lookup"><span data-stu-id="34004-129">Adds an item (as `byte[]`) to the cache using a string key.</span></span>

<span data-ttu-id="34004-130">**刷新 RefreshAsync**</span><span class="sxs-lookup"><span data-stu-id="34004-130">**Refresh, RefreshAsync**</span></span>

<span data-ttu-id="34004-131">刷新缓存基于其密钥，重置其滑动到期超时值 （如果有） 中的项。</span><span class="sxs-lookup"><span data-stu-id="34004-131">Refreshes an item in the cache based on its key, resetting its sliding expiration timeout (if any).</span></span>

<span data-ttu-id="34004-132">**删除 RemoveAsync**</span><span class="sxs-lookup"><span data-stu-id="34004-132">**Remove, RemoveAsync**</span></span>

<span data-ttu-id="34004-133">删除基于其键在某个缓存项。</span><span class="sxs-lookup"><span data-stu-id="34004-133">Removes a cache entry based on its key.</span></span>

<span data-ttu-id="34004-134">若要使用`IDistributedCache`接口：</span><span class="sxs-lookup"><span data-stu-id="34004-134">To use the `IDistributedCache` interface:</span></span>

   1. <span data-ttu-id="34004-135">将所需的 NuGet 包添加到你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="34004-135">Add the required NuGet packages to your project file.</span></span>

   2. <span data-ttu-id="34004-136">配置的特定实现`IDistributedCache`中你`Startup`类的`ConfigureServices`方法，并将其添加到容器存在。</span><span class="sxs-lookup"><span data-stu-id="34004-136">Configure the specific implementation of `IDistributedCache` in your `Startup` class's `ConfigureServices` method, and add it to the container there.</span></span>

   3. <span data-ttu-id="34004-137">从应用程序的[中间件](../../fundamentals/middleware.md)MVC 控制器类，请求的实例或`IDistributedCache`从构造函数。</span><span class="sxs-lookup"><span data-stu-id="34004-137">From the app's [Middleware](../../fundamentals/middleware.md) or MVC controller classes, request an instance of `IDistributedCache` from the constructor.</span></span> <span data-ttu-id="34004-138">实例将由提供[依赖关系注入](../../fundamentals/dependency-injection.md)(DI)。</span><span class="sxs-lookup"><span data-stu-id="34004-138">The instance will be provided by [Dependency Injection](../../fundamentals/dependency-injection.md) (DI).</span></span>

> [!NOTE]
> <span data-ttu-id="34004-139">没有无需使用的单一实例或作用域生存期`IDistributedCache`实例 (至少对于内置实现)。</span><span class="sxs-lookup"><span data-stu-id="34004-139">There's no need to use a Singleton or Scoped lifetime for `IDistributedCache` instances (at least for the built-in implementations).</span></span> <span data-ttu-id="34004-140">你还可以创建一个实例，只要你可能需要一个 (而不是使用[依赖关系注入](../../fundamentals/dependency-injection.md))，但这会导致你的代码更难若要测试，并且与冲突[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。</span><span class="sxs-lookup"><span data-stu-id="34004-140">You can also create an instance wherever you might need one (instead of using [Dependency Injection](../../fundamentals/dependency-injection.md)), but this can make your code harder to test, and violates the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span>

<span data-ttu-id="34004-141">下面的示例演示如何使用的实例`IDistributedCache`简单中间件组件中：</span><span class="sxs-lookup"><span data-stu-id="34004-141">The following example shows how to use an instance of `IDistributedCache` in a simple middleware component:</span></span>

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/StartTimeHeader.cs?highlight=15,18,21,27,28,29,30,31)]

<span data-ttu-id="34004-142">在上面的代码中，缓存的值是读取，但永远不会写入。</span><span class="sxs-lookup"><span data-stu-id="34004-142">In the code above, the cached value is read, but never written.</span></span> <span data-ttu-id="34004-143">在此示例中，值只能设置当服务器启动，并不会更改。</span><span class="sxs-lookup"><span data-stu-id="34004-143">In this sample, the value is only set when a server starts up, and doesn't change.</span></span> <span data-ttu-id="34004-144">在多服务器方案中，最新的服务器以开始将覆盖任何以前的值已设置的其他服务器。</span><span class="sxs-lookup"><span data-stu-id="34004-144">In a multi-server scenario, the most recent server to start will overwrite any previous values that were set by other servers.</span></span> <span data-ttu-id="34004-145">`Get`和`Set`方法使用`byte[]`类型。</span><span class="sxs-lookup"><span data-stu-id="34004-145">The `Get` and `Set` methods use the `byte[]` type.</span></span> <span data-ttu-id="34004-146">因此，字符串必须将值转换使用`Encoding.UTF8.GetString`(有关`Get`) 和`Encoding.UTF8.GetBytes`(有关`Set`)。</span><span class="sxs-lookup"><span data-stu-id="34004-146">Therefore, the string value must be converted using `Encoding.UTF8.GetString` (for `Get`) and `Encoding.UTF8.GetBytes` (for `Set`).</span></span>

<span data-ttu-id="34004-147">下面的代码从*Startup.cs*显示设置的值：</span><span class="sxs-lookup"><span data-stu-id="34004-147">The following code from *Startup.cs* shows the value being set:</span></span>

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=2,4,5,6&range=58-66)]

> [!NOTE]
> <span data-ttu-id="34004-148">由于`IDistributedCache`中配置`ConfigureServices`方法，它可供`Configure`作为参数的方法。</span><span class="sxs-lookup"><span data-stu-id="34004-148">Since `IDistributedCache` is configured in the `ConfigureServices` method, it's available to the `Configure` method as a parameter.</span></span> <span data-ttu-id="34004-149">将其添加作为参数将允许通过 DI 提供配置的实例。</span><span class="sxs-lookup"><span data-stu-id="34004-149">Adding it as a parameter will allow the configured instance to be provided through DI.</span></span>

## <a name="using-a-redis-distributed-cache"></a><span data-ttu-id="34004-150">使用分布式的 Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="34004-150">Using a Redis distributed cache</span></span>

<span data-ttu-id="34004-151">[Redis](https://redis.io/)是一个开放源代码内存中数据存储区，通常用来作为分布式缓存。</span><span class="sxs-lookup"><span data-stu-id="34004-151">[Redis](https://redis.io/) is an open source in-memory data store, which is often used as a distributed cache.</span></span> <span data-ttu-id="34004-152">你可以在本地，使用它，并且你可以配置[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)为你的 Azure 托管的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="34004-152">You can use it locally, and you can configure an [Azure Redis Cache](https://azure.microsoft.com/services/cache/) for your Azure-hosted ASP.NET Core apps.</span></span> <span data-ttu-id="34004-153">ASP.NET Core 应用程序将配置为使用缓存实现`RedisDistributedCache`实例。</span><span class="sxs-lookup"><span data-stu-id="34004-153">Your ASP.NET Core app configures the cache implementation using a `RedisDistributedCache` instance.</span></span>

<span data-ttu-id="34004-154">配置中的 Redis 实现`ConfigureServices`和通过请求的实例应用程序代码中访问它`IDistributedCache`（请参阅上面的代码）。</span><span class="sxs-lookup"><span data-stu-id="34004-154">You configure the Redis implementation in `ConfigureServices` and access it in your app code by requesting an instance of `IDistributedCache` (see the code above).</span></span>

<span data-ttu-id="34004-155">在示例代码中，`RedisCache`时服务器配置为使用实现`Staging`环境。</span><span class="sxs-lookup"><span data-stu-id="34004-155">In the sample code, a `RedisCache` implementation is used when the server is configured for a `Staging` environment.</span></span> <span data-ttu-id="34004-156">因此`ConfigureStagingServices`方法配置`RedisCache`:</span><span class="sxs-lookup"><span data-stu-id="34004-156">Thus the `ConfigureStagingServices` method configures the `RedisCache`:</span></span>

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=8,9,10,11,12,13&range=27-40)]

> [!NOTE]
> <span data-ttu-id="34004-157">若要在本地计算机上安装 Redis，安装 chocolatey 程序包[https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/)并运行`redis-server`从命令提示符。</span><span class="sxs-lookup"><span data-stu-id="34004-157">To install Redis on your local machine, install the chocolatey package [https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/) and run `redis-server` from a command prompt.</span></span>

## <a name="using-a-sql-server-distributed-cache"></a><span data-ttu-id="34004-158">使用 SQL Server 分布式缓存</span><span class="sxs-lookup"><span data-stu-id="34004-158">Using a SQL Server distributed cache</span></span>

<span data-ttu-id="34004-159">SqlServerCache 实现允许分布式的缓存使用作为其后备存储的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="34004-159">The SqlServerCache implementation allows the distributed cache to use a SQL Server database as its backing store.</span></span> <span data-ttu-id="34004-160">若要创建 SQL Server 表中，可以使用 sql 缓存工具，该工具，请与你指定的名称和架构中创建一个表。</span><span class="sxs-lookup"><span data-stu-id="34004-160">To create SQL Server table you can use sql-cache tool, the tool creates a table with the name and schema you specify.</span></span>

<span data-ttu-id="34004-161">若要使用 sql 缓存工具，添加`SqlConfig.Tools`到`<ItemGroup>`元素*.csproj*文件，运行 dotnet 还原。</span><span class="sxs-lookup"><span data-stu-id="34004-161">To use the sql-cache tool, add `SqlConfig.Tools` to the `<ItemGroup>` element of the *.csproj* file and run dotnet restore.</span></span>

[!code-xml[Main](./distributed/sample/src/DistCacheSample/DistCacheSample.csproj?range=23-25)]

<span data-ttu-id="34004-162">通过运行以下命令来测试 SqlConfig.Tools</span><span class="sxs-lookup"><span data-stu-id="34004-162">Test SqlConfig.Tools by running the following command</span></span>

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create --help
   ```

<span data-ttu-id="34004-163">现在，你可以运行"创建 sql 缓存"命令入 sql server，创建表，sql 缓存工具将显示使用情况、 选项和命令的帮助：</span><span class="sxs-lookup"><span data-stu-id="34004-163">sql-cache tool  will display usage, options and command help, now you can create tables into sql server, running "sql-cache create" command :</span></span>

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
   info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
       Table and index were created successfully.
   ```

<span data-ttu-id="34004-164">创建的表具有以下架构：</span><span class="sxs-lookup"><span data-stu-id="34004-164">The created table has the following schema:</span></span>

![Sql Server 缓存表](distributed/_static/SqlServerCacheTable.png)

<span data-ttu-id="34004-166">所有的缓存实现，如你的应用程序应获取和设置缓存值，使用的实例`IDistributedCache`，而不`SqlServerCache`。</span><span class="sxs-lookup"><span data-stu-id="34004-166">Like all cache implementations, your app should get and set cache values using an instance of `IDistributedCache`, not a `SqlServerCache`.</span></span> <span data-ttu-id="34004-167">此示例实现`SqlServerCache`中`Production`环境 (以便在配置`ConfigureProductionServices`)。</span><span class="sxs-lookup"><span data-stu-id="34004-167">The sample implements `SqlServerCache` in the `Production` environment (so it's configured in `ConfigureProductionServices`).</span></span>

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=7,8,9,10,11,12&range=42-56)]

> [!NOTE]
> <span data-ttu-id="34004-168">`ConnectionString` (和 （可选）`SchemaName`和`TableName`) 通常应在因为它们可能包含凭据存储在源控件 （如 UserSecrets)，之外。</span><span class="sxs-lookup"><span data-stu-id="34004-168">The `ConnectionString` (and optionally, `SchemaName` and `TableName`) should typically be stored outside of source control (such as UserSecrets), as they may contain credentials.</span></span>

## <a name="recommendations"></a><span data-ttu-id="34004-169">建议</span><span class="sxs-lookup"><span data-stu-id="34004-169">Recommendations</span></span>

<span data-ttu-id="34004-170">在决定的哪一种实现`IDistributedCache`是适合你的应用，选择 Redis 之间，SQL Server 基于现有基础结构和环境、 性能要求和你的团队的体验。</span><span class="sxs-lookup"><span data-stu-id="34004-170">When deciding which implementation of `IDistributedCache` is right for your app, choose between Redis and SQL Server based on your existing infrastructure and environment, your performance requirements, and your team's experience.</span></span> <span data-ttu-id="34004-171">如果你的团队更喜欢使用 Redis，它是一个理想的选择。</span><span class="sxs-lookup"><span data-stu-id="34004-171">If your team is more comfortable working with Redis, it's an excellent choice.</span></span> <span data-ttu-id="34004-172">如果你的团队倾向于 SQL Server，您可以确信中以及该实现。</span><span class="sxs-lookup"><span data-stu-id="34004-172">If your team prefers SQL Server, you can be confident in that implementation as well.</span></span> <span data-ttu-id="34004-173">请注意，传统的缓存解决方案将存储数据的内存中用于进行快速检索的数据。</span><span class="sxs-lookup"><span data-stu-id="34004-173">Note that A traditional caching solution stores data in-memory which allows for fast retrieval of data.</span></span> <span data-ttu-id="34004-174">你应在缓存中存储常用的数据并将整个数据存储在 SQL Server 或 Azure 存储空间等后端持久存储区中。</span><span class="sxs-lookup"><span data-stu-id="34004-174">You should store commonly used data in a cache and store the entire data in a backend persistent store such as SQL Server or Azure Storage.</span></span> <span data-ttu-id="34004-175">Redis 缓存是为你提供高吞吐量和低延迟相比 SQL 缓存的缓存解决方案。</span><span class="sxs-lookup"><span data-stu-id="34004-175">Redis Cache is a caching solution which gives you high throughput and low latency as compared to SQL Cache.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34004-176">其他资源</span><span class="sxs-lookup"><span data-stu-id="34004-176">Additional resources</span></span>

* [<span data-ttu-id="34004-177">Redis 在 Azure 上的缓存</span><span class="sxs-lookup"><span data-stu-id="34004-177">Redis Cache on Azure</span></span>](https://azure.microsoft.com/documentation/services/redis-cache/)
* [<span data-ttu-id="34004-178">在 Azure 上的 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="34004-178">SQL Database on Azure</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="34004-179">内存中缓存</span><span class="sxs-lookup"><span data-stu-id="34004-179">In-memory caching</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="34004-180">使用更改令牌检测更改</span><span class="sxs-lookup"><span data-stu-id="34004-180">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="34004-181">响应缓存</span><span class="sxs-lookup"><span data-stu-id="34004-181">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="34004-182">响应缓存中间件</span><span class="sxs-lookup"><span data-stu-id="34004-182">Response Caching Middleware</span></span>](xref:performance/caching/middleware)
* [<span data-ttu-id="34004-183">缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="34004-183">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="34004-184">分布式缓存标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="34004-184">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
