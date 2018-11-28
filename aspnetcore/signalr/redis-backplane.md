---
title: Redis 的 ASP.NET Core SignalR 横向扩展的底板
author: tdykstra
description: 了解如何设置 Redis 底板以启用 ASP.NET Core SignalR 应用程序的横向扩展。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/redis-backplane
ms.openlocfilehash: c8b09c0d482da344b54d167c0c9757167eaa6186
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52452923"
---
# <a name="set-up-a-redis-backplane-for-aspnet-core-signalr-scale-out"></a><span data-ttu-id="99d7d-103">设置 ASP.NET Core SignalR 横向扩展 Redis 底板</span><span class="sxs-lookup"><span data-stu-id="99d7d-103">Set up a Redis backplane for ASP.NET Core SignalR scale-out</span></span>

<span data-ttu-id="99d7d-104">通过[Andrew Stanton-nurse](https://twitter.com/anurse)， [Brady Gaster](https://twitter.com/bradygaster)，并[Tom Dykstra](https://github.com/tdykstra)，</span><span class="sxs-lookup"><span data-stu-id="99d7d-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), and [Tom Dykstra](https://github.com/tdykstra),</span></span>

<span data-ttu-id="99d7d-105">此文章介绍了设置的特定于 SignalR 的方面[Redis](https://redis.io/)要用于横向扩展 ASP.NET Core SignalR 应用程序服务器。</span><span class="sxs-lookup"><span data-stu-id="99d7d-105">This article explains SignalR-specific aspects of setting up a [Redis](https://redis.io/) server to use for scaling out an ASP.NET Core SignalR app.</span></span>

## <a name="set-up-a-redis-backplane"></a><span data-ttu-id="99d7d-106">设置 Redis 底板</span><span class="sxs-lookup"><span data-stu-id="99d7d-106">Set up a Redis backplane</span></span>

* <span data-ttu-id="99d7d-107">部署 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="99d7d-107">Deploy a Redis server.</span></span>

  <span data-ttu-id="99d7d-108">对于生产用途，Redis 底板建议仅用于在本地基础结构。</span><span class="sxs-lookup"><span data-stu-id="99d7d-108">For production use, a Redis backplane is recommended only for on-premises infrastructure.</span></span> <span data-ttu-id="99d7d-109">若要最小化滞后时间，Redis 服务器应是 SignalR 应用程序所在的同一数据中心。</span><span class="sxs-lookup"><span data-stu-id="99d7d-109">To minimize latency, the Redis server should be in the same data center as the SignalR app.</span></span> <span data-ttu-id="99d7d-110">如果您的 SignalR 应用程序运行在 Azure 云中，我们将建议 Azure SignalR 服务而不是 Redis 底板。</span><span class="sxs-lookup"><span data-stu-id="99d7d-110">If your SignalR app is running in the Azure cloud, we recommend Azure SignalR Service instead of a Redis backplane.</span></span> <span data-ttu-id="99d7d-111">可以使用 Azure Redis 缓存服务进行开发和测试环境。</span><span class="sxs-lookup"><span data-stu-id="99d7d-111">You can use the Azure Redis Cache Service for development and test environments.</span></span> <span data-ttu-id="99d7d-112">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="99d7d-112">For more information, see the following resources:</span></span>

  * <xref:signalr/scale>
  * [<span data-ttu-id="99d7d-113">Redis 文档</span><span class="sxs-lookup"><span data-stu-id="99d7d-113">Redis documentation</span></span>](https://redis.io/)
  * [<span data-ttu-id="99d7d-114">Azure Redis 缓存文档</span><span class="sxs-lookup"><span data-stu-id="99d7d-114">Azure Redis Cache documentation</span></span>](https://docs.microsoft.com/en-us/azure/redis-cache/)

::: moniker range="= aspnetcore-2.1"

* <span data-ttu-id="99d7d-115">在 SignalR 应用程序中，将安装`Microsoft.AspNetCore.SignalR.Redis`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="99d7d-115">In the SignalR app, install the `Microsoft.AspNetCore.SignalR.Redis` NuGet package.</span></span>

* <span data-ttu-id="99d7d-116">在中`Startup.ConfigureServices`方法中，调用`AddRedis`后`AddSignalR`:</span><span class="sxs-lookup"><span data-stu-id="99d7d-116">In the `Startup.ConfigureServices` method, call `AddRedis` after `AddSignalR`:</span></span>

  ```csharp
  services.AddSignalR().AddRedis("<your_Redis_connection_string>");
  ```

* <span data-ttu-id="99d7d-117">根据需要配置选项：</span><span class="sxs-lookup"><span data-stu-id="99d7d-117">Configure options as needed:</span></span>
 
  <span data-ttu-id="99d7d-118">可以设置大多数选项，在连接字符串中或在[ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options)对象。</span><span class="sxs-lookup"><span data-stu-id="99d7d-118">Most options can be set in the connection string or in the [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) object.</span></span> <span data-ttu-id="99d7d-119">中指定的选项`ConfigurationOptions`在连接字符串中设置的替代。</span><span class="sxs-lookup"><span data-stu-id="99d7d-119">Options specified in `ConfigurationOptions` override the ones set in the connection string.</span></span>

  <span data-ttu-id="99d7d-120">下面的示例演示如何在中设置选项`ConfigurationOptions`对象。</span><span class="sxs-lookup"><span data-stu-id="99d7d-120">The following example shows how to set options in the `ConfigurationOptions` object.</span></span> <span data-ttu-id="99d7d-121">此示例添加通道前缀，以便多个应用程序可以共享同一 Redis 实例下, 一步中所述。</span><span class="sxs-lookup"><span data-stu-id="99d7d-121">This example adds a channel prefix so that multiple apps can share the same Redis instance, as explained in the following step.</span></span>

  ```csharp
  services.AddSignalR()
    .AddRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  <span data-ttu-id="99d7d-122">在前面的代码，`options.Configuration`使用连接字符串中指定了任何初始化。</span><span class="sxs-lookup"><span data-stu-id="99d7d-122">In the preceding code, `options.Configuration` is initialized with whatever was specified in the connection string.</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.1"

* <span data-ttu-id="99d7d-123">在 SignalR 应用程序中，将安装`Microsoft.AspNetCore.SignalR.StackExchangeRedis`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="99d7d-123">In the SignalR app, install the `Microsoft.AspNetCore.SignalR.StackExchangeRedis` NuGet package.</span></span>

* <span data-ttu-id="99d7d-124">在中`Startup.ConfigureServices`方法中，调用`AddStackExchangeRedis`后`AddSignalR`:</span><span class="sxs-lookup"><span data-stu-id="99d7d-124">In the `Startup.ConfigureServices` method, call `AddStackExchangeRedis` after `AddSignalR`:</span></span>

  ```csharp
  services.AddSignalR().AddStackExchangeRedis("<your_Redis_connection_string>");
  ```

* <span data-ttu-id="99d7d-125">根据需要配置选项：</span><span class="sxs-lookup"><span data-stu-id="99d7d-125">Configure options as needed:</span></span>
 
  <span data-ttu-id="99d7d-126">可以设置大多数选项，在连接字符串中或在[ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options)对象。</span><span class="sxs-lookup"><span data-stu-id="99d7d-126">Most options can be set in the connection string or in the [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) object.</span></span> <span data-ttu-id="99d7d-127">中指定的选项`ConfigurationOptions`在连接字符串中设置的替代。</span><span class="sxs-lookup"><span data-stu-id="99d7d-127">Options specified in `ConfigurationOptions` override the ones set in the connection string.</span></span>

  <span data-ttu-id="99d7d-128">下面的示例演示如何在中设置选项`ConfigurationOptions`对象。</span><span class="sxs-lookup"><span data-stu-id="99d7d-128">The following example shows how to set options in the `ConfigurationOptions` object.</span></span> <span data-ttu-id="99d7d-129">此示例添加通道前缀，以便多个应用程序可以共享同一 Redis 实例下, 一步中所述。</span><span class="sxs-lookup"><span data-stu-id="99d7d-129">This example adds a channel prefix so that multiple apps can share the same Redis instance, as explained in the following step.</span></span>

  ```csharp
  services.AddSignalR()
    .AddStackExchangeRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  <span data-ttu-id="99d7d-130">在前面的代码，`options.Configuration`使用连接字符串中指定了任何初始化。</span><span class="sxs-lookup"><span data-stu-id="99d7d-130">In the preceding code, `options.Configuration` is initialized with whatever was specified in the connection string.</span></span>

  <span data-ttu-id="99d7d-131">有关 Redis 选项的信息，请参阅[StackExchange Redis 文档](https://stackexchange.github.io/StackExchange.Redis/Configuration.html)。</span><span class="sxs-lookup"><span data-stu-id="99d7d-131">For information about Redis options, see the [StackExchange Redis documentation](https://stackexchange.github.io/StackExchange.Redis/Configuration.html).</span></span>

::: moniker-end

* <span data-ttu-id="99d7d-132">如果您正在使用多个 SignalR 应用一个 Redis 服务器，为每个 SignalR 应用使用不同的通道前缀。</span><span class="sxs-lookup"><span data-stu-id="99d7d-132">If you're using one Redis server for multiple SignalR apps, use a different channel prefix for each SignalR app.</span></span>

  <span data-ttu-id="99d7d-133">设置通道前缀将从其他人使用不同的通道前缀的一个 SignalR 应用程序隔离开来。</span><span class="sxs-lookup"><span data-stu-id="99d7d-133">Setting a channel prefix isolates one SignalR app from others that use different channel prefixes.</span></span> <span data-ttu-id="99d7d-134">如果没有分配不同的前缀，从一个应用到所有其自己的客户端发送的消息将转到用作基架使用 Redis 服务器的所有应用的所有客户端。</span><span class="sxs-lookup"><span data-stu-id="99d7d-134">If you don't assign different prefixes, a message sent from one app to all of its own clients will go to all clients of all apps that use the Redis server as a backplane.</span></span>

* <span data-ttu-id="99d7d-135">配置服务器场负载平衡软件为粘性会话。</span><span class="sxs-lookup"><span data-stu-id="99d7d-135">Configure your server farm load balancing software for sticky sessions.</span></span> <span data-ttu-id="99d7d-136">下面是文档的有关如何执行该操作的一些示例：</span><span class="sxs-lookup"><span data-stu-id="99d7d-136">Here are some examples of documentation on how to do that:</span></span>

  * [<span data-ttu-id="99d7d-137">IIS</span><span class="sxs-lookup"><span data-stu-id="99d7d-137">IIS</span></span>](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing)
  * [<span data-ttu-id="99d7d-138">HAProxy</span><span class="sxs-lookup"><span data-stu-id="99d7d-138">HAProxy</span></span>](https://www.haproxy.com/blog/load-balancing-affinity-persistence-sticky-sessions-what-you-need-to-know/)
  * [<span data-ttu-id="99d7d-139">Nginx</span><span class="sxs-lookup"><span data-stu-id="99d7d-139">Nginx</span></span>](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/#sticky)
  * [<span data-ttu-id="99d7d-140">pfSense</span><span class="sxs-lookup"><span data-stu-id="99d7d-140">pfSense</span></span>](https://www.netgate.com/docs/pfsense/loadbalancing/inbound-load-balancing.html#sticky-connections)

## <a name="redis-server-errors"></a><span data-ttu-id="99d7d-141">Redis 服务器错误</span><span class="sxs-lookup"><span data-stu-id="99d7d-141">Redis server errors</span></span>

<span data-ttu-id="99d7d-142">当 Redis 服务器出现故障时，SignalR 会引发异常，指示不会将消息传递。</span><span class="sxs-lookup"><span data-stu-id="99d7d-142">When a Redis server goes down, SignalR throws exceptions that indicate messages won't be delivered.</span></span> <span data-ttu-id="99d7d-143">一些典型异常消息：</span><span class="sxs-lookup"><span data-stu-id="99d7d-143">Some typical exception messages:</span></span>

* <span data-ttu-id="99d7d-144">*失败的编写消息*</span><span class="sxs-lookup"><span data-stu-id="99d7d-144">*Failed writing message*</span></span>
* <span data-ttu-id="99d7d-145">*无法调用集线器方法 MethodName*</span><span class="sxs-lookup"><span data-stu-id="99d7d-145">*Failed to invoke hub method 'MethodName'*</span></span>
* <span data-ttu-id="99d7d-146">*未能连接到 Redis*</span><span class="sxs-lookup"><span data-stu-id="99d7d-146">*Connection to Redis failed*</span></span>

<span data-ttu-id="99d7d-147">SignalR 不缓冲消息，当服务器重新启动后发送它们。</span><span class="sxs-lookup"><span data-stu-id="99d7d-147">SignalR doesn't buffer messages to send them when the server comes back up.</span></span> <span data-ttu-id="99d7d-148">Redis 服务器已关闭时发送任何消息都将丢失。</span><span class="sxs-lookup"><span data-stu-id="99d7d-148">Any messages sent while the Redis server is down are lost.</span></span>

<span data-ttu-id="99d7d-149">当 Redis 服务器再次可用时，自动重新连接 SignalR。</span><span class="sxs-lookup"><span data-stu-id="99d7d-149">SignalR automatically reconnects when the Redis server is available again.</span></span>

### <a name="custom-behavior-for-connection-failures"></a><span data-ttu-id="99d7d-150">连接失败的自定义行为</span><span class="sxs-lookup"><span data-stu-id="99d7d-150">Custom behavior for connection failures</span></span>

<span data-ttu-id="99d7d-151">下面是一个示例，演示如何处理 Redis 连接失败事件。</span><span class="sxs-lookup"><span data-stu-id="99d7d-151">Here's an example that shows how to handle Redis connection failure events.</span></span>

::: moniker range="= aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

::: moniker range="> aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddMessagePackProtocol()
        .AddStackExchangeRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

## <a name="clustering"></a><span data-ttu-id="99d7d-152">聚类分析</span><span class="sxs-lookup"><span data-stu-id="99d7d-152">Clustering</span></span>

<span data-ttu-id="99d7d-153">聚类分析是一种方法使用多个 Redis 服务器实现高可用性。</span><span class="sxs-lookup"><span data-stu-id="99d7d-153">Clustering is a method for achieving high availability by using multiple Redis servers.</span></span> <span data-ttu-id="99d7d-154">聚类分析不正式支持，但它可能起作用。</span><span class="sxs-lookup"><span data-stu-id="99d7d-154">Clustering isn't officially supported, but it might work.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d7d-155">后续步骤</span><span class="sxs-lookup"><span data-stu-id="99d7d-155">Next steps</span></span>

<span data-ttu-id="99d7d-156">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="99d7d-156">For more information, see the following resources:</span></span>

* <xref:signalr/scale>
* [<span data-ttu-id="99d7d-157">Redis 文档</span><span class="sxs-lookup"><span data-stu-id="99d7d-157">Redis documentation</span></span>](https://redis.io/documentation)
* [<span data-ttu-id="99d7d-158">StackExchange Redis 文档</span><span class="sxs-lookup"><span data-stu-id="99d7d-158">StackExchange Redis documentation</span></span>](https://stackexchange.github.io/StackExchange.Redis/)
* [<span data-ttu-id="99d7d-159">Azure Redis 缓存文档</span><span class="sxs-lookup"><span data-stu-id="99d7d-159">Azure Redis Cache documentation</span></span>](https://docs.microsoft.com/en-us/azure/redis-cache/)
