---
title: "使用分布式缓存"
author: ardalis
description: 
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: 870f082d-6d43-453d-b311-45f3aeb4d2c5
ms.technology: aspnet
ms.prod: asp.net-core
uid: performance/caching/distributed
ms.openlocfilehash: abf680fef9de175082c1e4f4cebc2b9648f18a28
ms.sourcegitcommit: 9cdbfd0d670d70b9c354216aabee260c52dad5ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2017
---
# <a name="working-with-a-distributed-cache"></a>使用分布式缓存

作者：[Steve Smith](https://ardalis.com/)

分布式缓存可以提高ASP.NET Core应用程序的性能和可伸缩性，尤其是托管在云或服务器场环境中时。本文解释了如何使用ASP.NET Core的内置分布式缓存抽象和实现。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample)

## <a name="what-is-a-distributed-cache"></a>什么是分布式缓存

分布式缓存由多个应用程序服务器共享 (请参阅[缓存的基础知识](memory.md#caching-basics))。缓存中的信息不存储在单独的 web 服务器的内存中，并且缓存的数据可用于所有应用程序的服务器。这提供了几个优点：

1. 所有 web 服务器上的缓存数据都是一致的。用户看不到不同的结果，具体取决于哪个 web 服务器处理他们的请求

2. 缓存的数据在 web 服务器重新启动和部署中仍然存在。单独的 web 服务器可以被删除或添加而不会影响缓存。

3. 源数据存储对它的请求较少（比使用多个内存缓存或根本没有缓存）。

> [!NOTE]
> 如果使用 SQL Server 分布式缓存，那么其中一些优势只有为缓存而不是为应用程序的源数据使用单独的数据库实例时才会生效。

像任何缓存一样，分布式的缓存可以显著提高应用程序的响应速度，因为通常数据从缓存中检索比从关系数据库中（或 web 服务）快得多。

缓存配置是特定于实现的。本文介绍如何配置 Redis 和 SQL Server 分布式缓存。无论选择哪一种实现，应用程序都使用通用的`IDistributedCache`接口与缓存交互。

## <a name="the-idistributedcache-interface"></a>IDistributedCache 接口

`IDistributedCache`接口包含同步和异步方法。接口允许从分布式缓存实现中添加、检索和删除项。`IDistributedCache`接口包括以下方法：

**Get、 GetAsync**

采用字符串键并将缓存项检索为`byte[]`（如果在缓存中找到）。

**Set SetAsync**

使用字符串键向缓存添加项（作为`byte[]`）。

**Refresh RefreshAsync**

根据键刷新缓存中的项，并重置其滑动到期超时值（如果有）。

**Remove RemoveAsync**

根据键删除缓存项。

若要使用`IDistributedCache`接口：

   1. 将所需的 NuGet 包添加到您的项目文件。

   2. 在`Startup`类的`ConfigureServices`方法中配置`IDistributedCache`的具体实现，并将其添加到该容器中。

   3. 从应用程序的[中间件](../../fundamentals/middleware.md)或MVC控制器类中，从构造函数请求`IDistributedCache`的实例。 实例将由[依赖注入](../../fundamentals/dependency-injection.md)（DI）提供。

> [!NOTE]
> 无需为`IDistributedCache`实例使用Singleton或Scoped生命周期（至少对于内置实现）。您也可以在需要的地方创建一个实例（而不是使用[依赖关系注入](../../fundamentals/dependency-injection.md)），但是这会让您的代码更难测试，并且违反了[显式依赖原则](http://deviq.com/explicit-dependencies-principle/)。

下面的示例演示如何在简单中间件组件中使用`IDistributedCache`实例：

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/StartTimeHeader.cs?highlight=15,18,21,27,28,29,30,31)]

在上面的代码中，缓存值被读取，但从未写入。在此示例中，该值仅在服务器启动时设置，并且不会更改。在多服务器方案中，要启动的最新服务器将覆盖由其他服务器设置的以前的任何值。`Get`和`Set`方法使用`byte[]`类型。因此，字符串值必须使用`Encoding.UTF8.GetString`（对于`Get`）和`Encoding.UTF8.GetBytes`（对于`Set`）进行转换。

*Startup.cs*中的以下代码显示正在设置的值：

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=2,4,5,6&range=58-66)]

> [!NOTE]
> 由于`IDistributedCache`是在`ConfigureServices`方法中配置的，因此它可以作为参数提供给`Configure`方法。将其作为参数添加将允许通过DI提供配置的实例。

## <a name="using-a-redis-distributed-cache"></a>使用 Redis 分布式缓存

[Redis](https://redis.io/)是一款开源的内存数据存储，通常用来作为分布式缓存。您可以在本地使用它，并且可以为Azure托管的ASP.NET Core应用程序配置[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)缓存。您的ASP.NET Core应用程序使用`RedisDistributedCache`实例配置缓存实现。

您可以在`ConfigureServices`中配置Redis实现，并通过请求`IDistributedCache`实例（请参阅上面的代码）在应用程序代码中访问它。

在示例代码中，将服务器配置为`Staging`环境时使用`RedisCache`实现。因此，`ConfigureStagingServices`方法配置`RedisCache`：

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=8,9,10,11,12,13&range=27-40)]

> [!NOTE]
> 若要在本地计算机上安装 Redis，请安装 chocolatey 程序包[https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/)并从命令提示符运行`redis-server`。

## <a name="using-a-sql-server-distributed-cache"></a>使用 SQL Server 分布式缓存

SqlServerCache实现允许分布式缓存使用SQL Server数据库作为其后备存储。要创建SQL Server表，您可以使用sql-cache工具，该工具将使用您指定的名称和模式创建一个表。

若要使用 sql-cache 工具，将`SqlConfig.Tools`添加到*.csproj*文件的`<ItemGroup>`元素，运行 dotnet restore。

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/DistCacheSample.csproj?range=23-25)]

通过运行以下命令来测试 SqlConfig.Tools

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create --help
   ```

sql-cache工具将显示用法，选项和命令帮助，现在你可以创建表到sql server中，运行“sql-cache create”命令：

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
   info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
       Table and index were created successfully.
   ```

创建的表具有以下架构：

![Sql Server 缓存表](distributed/_static/SqlServerCacheTable.png)

像所有缓存实现一样，您的应用程序应该使用`IDistributedCache`实例来获取和设置缓存值，而不是使用`SqlServerCache`。该示例在`Production`环境中实现了`SqlServerCache`（因此它在`ConfigureProductionServices`中进行了配置）。

[!code-csharp[Main](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=7,8,9,10,11,12&range=42-56)]

> [!NOTE]
> `ConnectionString`（以及可选的`SchemaName`和`TableName`）通常应该存储在源代码管理之外（例如UserSecrets），因为它们可能包含凭据。

## <a name="recommendations"></a>建议

在决定哪种`IDistributedCache`实现适合您的应用时，根据您现有的基础架构和环境，性能要求以及团队的经验，在Redis和SQL Server之间进行选择。如果你的团队更喜欢使用 Redis，那么这是一个很好的选择。 如果您的团队倾向于 SQL Server，那么您也可以对该实现充满信心。请注意，传统的缓存解决方案可将数据存储在内存中，以便快速检索数据。您应该将常用数据存储在缓存中，并将整个数据存储在后端持久性存储（如SQL Server或Azure Storage）中。与SQL Cache相比，Redis Cache是一种可为您提供高吞吐量和低延迟缓存的解决方案。

其他资源：

* [Azure 上的Redis缓存](https://azure.microsoft.com/documentation/services/redis-cache/)
* [在 Azure 上的 SQL 数据库](https://azure.microsoft.com/documentation/services/sql-database/)
* [内存缓存](memory.md)
* [使用更改令牌检测更改](https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/primitives/change-tokens)
* [响应缓存](https://docs.microsoft.com/zh-cn/aspnet/core/performance/caching/response)
* [响应缓存中间件][https://docs.microsoft.com/zh-cn/aspnet/core/performance/caching/middleware]
* [缓存标记帮助程序]
(https://docs.microsoft.com/zh-cn/aspnet/core/mvc/views/tag-helpers/built-in/cache-tag-helper)
* [分布式缓存标记帮助程序](https://docs.microsoft.com/zh-cn/aspnet/core/mvc/views/tag-helpers/built-in/distributed-cache-tag-helper)
