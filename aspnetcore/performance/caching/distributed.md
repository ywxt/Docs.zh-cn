---
title: 使用 ASP.NET Core 中分布式缓存
author: ardalis
description: 了解如何使用 ASP.NET Core 分布式缓存以提高应用性能和可伸缩性，尤其是在云或服务器场环境。
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/distributed
ms.openlocfilehash: 635c61cbb72a6a9eb822307bbc80936ee73bedc8
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="working-with-a-distributed-cache-in-aspnet-core"></a>使用 ASP.NET Core 中分布式缓存

作者：[Steve Smith](https://ardalis.com/)

分布式缓存可以提高 ASP.NET Core 应用的性能和可伸缩性，尤其是托管在云或服务器场环境中时。 本文解释了如何使用 ASP.NET Core 的内置分布式缓存抽象和实现。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="what-is-a-distributed-cache"></a>什么是分布式的缓存

分布式缓存由多个应用服务器共享 (请参阅[缓存基础知识](memory.md#caching-basics))。 缓存中的信息不存储在单独的 Web 服务器的内存中，并且缓存的数据可用于所有应用服务器。这具有几个优点： 这提供了几个优点：

1. 所有 Web 服务器上的缓存数据都是一致的。 用户不会因处理其请求的 Web 服务器的不同而看到不同的结果

2. 缓存的数据在 Web 服务器重新启动后和部署后仍然存在。 删除或添加单独的 Web 服务器不会影响缓存。

3. 源数据存储区具有对它 （不是使用多个内存中缓存或否缓存根本） 发出的少数几个请求。

> [!NOTE]
> 如果使用 SQL Server 分布式缓存，则其中一些优势只有在为缓存而不是应用的源数据使用单独的数据库实例的情况下才会体现出来。

像任何缓存一样，分布式缓存可以显著提高应用的响应速度，因为通常情况下，数据从缓存中检索比从关系数据库（或 Web 服务）中检索快得多。

缓存配置是特定于实现的。 本文介绍如何配置 Redis 和 SQL Server 分布式缓存。 无论选择哪一种实现，应用都使用通用的 `IDistributedCache` 接口与缓存交互。

## <a name="the-idistributedcache-interface"></a>IDistributedCache 接口

`IDistributedCache`接口包含同步和异步方法。 接口允许在分布式缓存实现中添加、检索和删除项。 `IDistributedCache`接口包含以下方法：

**Get、 GetAsync**

采用字符串键并以`byte[]`形式检索缓存项（如果在缓存中找到）。

**Set、SetAsync**

使用字符串键向缓存添加项`byte[]`形式）。 

**Refresh、RefreshAsync**

根据键刷新缓存中的项，并重置其可调过期超时值（如果有）。

**Remove、RemoveAsync**

根据键删除缓存项。

若要使用`IDistributedCache`接口：

   1. 所需的 NuGet 包添加到项目文件。

   2. 在`Startup`类的`ConfigureServices`方法中配置`IDistributedCache`的具体实现，并将其添加到该处的容器中。

   3. 在应用的[中间件](xref:fundamentals/middleware/index)或 MVC 控制器类中，从构造函数请求 `IDistributedCache`的实例。 实例将通过[依赖项注入](../../fundamentals/dependency-injection.md) (DI) 提供。

> [!NOTE]
> 无需为`IDistributedCache`实例使用 Singleton 或 Scoped 生命周期（至少对内置实现来说是这样的）。 你还可以创建一个实例，只要你可能需要一个 (而不是使用[依赖关系注入](../../fundamentals/dependency-injection.md))，但这会导致你的代码更难若要测试，并且与冲突[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)。

下面的示例演示如何在简单的中间件组件中使用`IDistributedCache` 实例：

[!code-csharp[](./distributed/sample/src/DistCacheSample/StartTimeHeader.cs?highlight=15,18,21,27,28,29,30,31)]

在上面的代码中，缓存值用于读取，不用于写入。 在此示例中，该值仅在服务器启动时设置，并且不会更改。 在多服务器方案中，要启动的最新服务器会覆盖由其他服务器设置的以前的任何值。 `Get`和`Set`方法使用 `byte[]`类型。 因此，字符串值必须使用 `Encoding.UTF8.GetString`(适用于`Get`) 和 `Encoding.UTF8.GetBytes`(适用于 `Set`)进行转换。

*Startup.cs*中的以下代码显示要设置的值：

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=2,4,5,6&range=58-66)]

> [!NOTE]
> 由于`IDistributedCache`是在`ConfigureServices`方法中配置的，因此它可以作为参数提供给`Configure`方法。 将其添加作为参数将允许通过 DI 提供配置的实例。

## <a name="using-a-redis-distributed-cache"></a>使用分布式的 Redis 缓存

[Redis](https://redis.io/)是一种开源的内存中数据存储，通常用作分布式缓存。 可以在本地使用它，并且可以为 Azure 托管的 ASP.NET Core 应用配置[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)为你的 Azure 托管的 ASP.NET Core 应用。 ASP.NET Core 应用使用 `RedisDistributedCache`实例配置缓存实现。

可在`ConfigureServices`中配置 Redis 实现，并可通过请求`IDistributedCache`实例（请参阅上面的代码）在应用代码中访问它。

在示例代码中，为`RedisCache`环境配置服务器时使用`Staging`实现。 因此，`ConfigureStagingServices`方法用于配置 `RedisCache`:

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=8,9,10,11,12,13&range=27-40)]

> [!NOTE]
> 若要在本地计算机上安装 Redis，请安装 chocolatey 包[https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/)然后从命令提示符处运行`redis-server`。

## <a name="using-a-sql-server-distributed-cache"></a>使用 SQL Server 分布式缓存

SqlServerCache 实现允许分布式缓存使用 SQL Server 数据库作为其后备存储。 若要创建 SQL Server 表，可以使用 sql-cache 工具，该工具将使用指定的名称和模式创建一个表。

若要使用 sql-cache 工具，请将 `SqlConfig.Tools`添加到`<ItemGroup>`文件的 *.csproj*元素，然后运行 dotnet restore。

[!code-xml[](./distributed/sample/src/DistCacheSample/DistCacheSample.csproj?range=23-25)]

通过运行以下命令来测试 SqlConfig.Tools

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create --help
   ```

sql-cache 工具将显示用法、选项和命令帮助。现在可以将表创建到 sql server 中，只需运行“sql-cache create”命令即可：

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
   info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
       Table and index were created successfully.
   ```

创建的表具有以下架构：

![Sql Server 缓存表](distributed/_static/SqlServerCacheTable.png)

像所有缓存实现一样，应用应该使用`IDistributedCache`，实例来获取和设置缓存值，而不是使用`SqlServerCache`实例。 此示例实现`SqlServerCache`中`Production`环境 (以便在配置`ConfigureProductionServices`)。

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=7,8,9,10,11,12&range=42-56)]

> [!NOTE]
> `ConnectionString` (以及可选的`SchemaName`和`TableName`) 通常应该存储在源代码管理之外（例如存储在 UserSecrets 中），因为它们可能包含凭据。

## <a name="recommendations"></a>建议

在决定哪种`IDistributedCache`实现适合应用时，请根据现有的基础架构和环境、性能要求和团队经验在 Redis 和 SQL Server 之间进行选择。 如果团队更喜欢使用 Redis，那就使用它。 如果团队倾向于 SQL Server，那么也应对这么做充满信心。 请注意，传统的缓存解决方案会将数据存储在内存中，以便快速检索数据。 应该将常用数据存储在缓存中，将整个数据存储在后端持久性存储（如 SQL Server 或 Azure 存储）中。 与 SQL Cache 相比，Redis Cache 是一种吞吐量高且延迟轻微的缓存解决方案。

## <a name="additional-resources"></a>其他资源

* [Redis 在 Azure 上的缓存](https://azure.microsoft.com/documentation/services/redis-cache/)
* [在 Azure 上的 SQL 数据库](https://azure.microsoft.com/documentation/services/sql-database/)
* [内存中缓存](xref:performance/caching/memory)
* [使用更改令牌检测更改](xref:fundamentals/primitives/change-tokens)
* [响应缓存](xref:performance/caching/response)
* [响应缓存中间件](xref:performance/caching/middleware)
* [缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [分布式缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
