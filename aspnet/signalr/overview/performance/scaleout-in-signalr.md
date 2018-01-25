---
uid: signalr/overview/performance/scaleout-in-signalr
title: "简介中 SignalR 的向外缩放 |Microsoft 文档"
author: MikeWasson
description: "Visual Studio 2013.NET 4.5 SignalR 本主题中使用软件版本的早期版本的信息的本主题的版本 2 早期版本..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: f1d15250682305f6d0512b72bd2e40cb4a8a18e5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="introduction-to-scaleout-in-signalr"></a><span data-ttu-id="94558-103">简介中 SignalR 的向外缩放</span><span class="sxs-lookup"><span data-stu-id="94558-103">Introduction to Scaleout in SignalR</span></span>
====================
<span data-ttu-id="94558-104">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="94558-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="94558-105">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="94558-105">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="94558-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="94558-106">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="94558-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="94558-107">.NET 4.5</span></span>
> - <span data-ttu-id="94558-108">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="94558-108">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="94558-109">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="94558-109">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="94558-110">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="94558-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="94558-111">问题和意见</span><span class="sxs-lookup"><span data-stu-id="94558-111">Questions and comments</span></span>
> 
> <span data-ttu-id="94558-112">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="94558-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="94558-113">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="94558-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="94558-114">一般情况下，有两种方法来扩展 web 应用程序：*向上扩展*和*向外扩展*。</span><span class="sxs-lookup"><span data-stu-id="94558-114">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="94558-115">使用更多 RAM、 Cpu、 等使用更大的服务器 （或较大的 VM） 的方式向上扩展。</span><span class="sxs-lookup"><span data-stu-id="94558-115">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="94558-116">扩展意味着添加更多服务器以处理负载。</span><span class="sxs-lookup"><span data-stu-id="94558-116">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="94558-117">向上扩展的问题是你快速命中了机的大小限制。</span><span class="sxs-lookup"><span data-stu-id="94558-117">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="94558-118">除此之外，你需要向外扩展。但是，当你向外扩展，客户端可以获取路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="94558-118">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="94558-119">连接到一台服务器的客户端不会收到从另一台服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="94558-119">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="94558-120">一种解决方案是将使用名为的组件，在服务器之间的消息转发*底板*。</span><span class="sxs-lookup"><span data-stu-id="94558-120">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="94558-121">启用底板，每个应用程序实例将消息发送到底板，与底板将其转发给其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="94558-121">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="94558-122">（在电子行业，底板是并行的连接器的组。</span><span class="sxs-lookup"><span data-stu-id="94558-122">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="94558-123">打比方，SignalR 基架连接多个服务器。）</span><span class="sxs-lookup"><span data-stu-id="94558-123">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="94558-124">SignalR 目前提供三个背板：</span><span class="sxs-lookup"><span data-stu-id="94558-124">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="94558-125">**Azure Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="94558-125">**Azure Service Bus**.</span></span> <span data-ttu-id="94558-126">Service Bus 是允许组件按松散耦合的方式发送消息的消息传递基础结构。</span><span class="sxs-lookup"><span data-stu-id="94558-126">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="94558-127">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="94558-127">**Redis**.</span></span> <span data-ttu-id="94558-128">Redis 是一个内存中键 / 值存储。</span><span class="sxs-lookup"><span data-stu-id="94558-128">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="94558-129">Redis 支持发布/订阅 ("pub/sub") 模式，用于将消息发送。</span><span class="sxs-lookup"><span data-stu-id="94558-129">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="94558-130">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="94558-130">**SQL Server**.</span></span> <span data-ttu-id="94558-131">SQL Server 底板将消息写入 SQL 表。</span><span class="sxs-lookup"><span data-stu-id="94558-131">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="94558-132">底板为有效的消息传递使用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="94558-132">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="94558-133">但是，它还适用如果未启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="94558-133">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="94558-134">如果你部署 Azure 上的应用程序，请考虑使用 Redis 底板使用[Azure Redis 缓存](https://azure.microsoft.com/services/cache/)。</span><span class="sxs-lookup"><span data-stu-id="94558-134">If you deploy your application on Azure, consider using the Redis backplane using [Azure Redis Cache](https://azure.microsoft.com/services/cache/).</span></span> <span data-ttu-id="94558-135">如果将部署到你自己的服务器场，请考虑 SQL Server 或 Redis 背板。</span><span class="sxs-lookup"><span data-stu-id="94558-135">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="94558-136">以下主题包含针对每个底板的分步教程：</span><span class="sxs-lookup"><span data-stu-id="94558-136">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="94558-137">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="94558-137">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="94558-138">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="94558-138">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="94558-139">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="94558-139">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="94558-140">实现</span><span class="sxs-lookup"><span data-stu-id="94558-140">Implementation</span></span>

<span data-ttu-id="94558-141">在 SignalR 通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="94558-141">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="94558-142">消息总线实现[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，从而提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="94558-142">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="94558-143">通过替换默认的工作的底板**IMessageBus**含总线为该底板设计的。</span><span class="sxs-lookup"><span data-stu-id="94558-143">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="94558-144">例如，Redis 消息总线是[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，并使用 Redis [pub/sub](http://redis.io/topics/pubsub)机制来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="94558-144">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="94558-145">每个服务器实例连接到通过总线底板。</span><span class="sxs-lookup"><span data-stu-id="94558-145">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="94558-146">发送一条消息，它将转到面板，并底板将其发送到每个服务器。</span><span class="sxs-lookup"><span data-stu-id="94558-146">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="94558-147">当服务器从底板获取一条消息时，它会在其本地缓存中将该消息。</span><span class="sxs-lookup"><span data-stu-id="94558-147">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="94558-148">服务器然后将从其本地缓存消息传送到客户端。</span><span class="sxs-lookup"><span data-stu-id="94558-148">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="94558-149">对于每个客户端连接，在读取消息流的客户端的进度被跟踪使用游标。</span><span class="sxs-lookup"><span data-stu-id="94558-149">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="94558-150">（游标表示消息流中的位置。）如果客户端断开连接并重新连接，但它会将总线要求提供任何客户端的光标在值后到达的消息。</span><span class="sxs-lookup"><span data-stu-id="94558-150">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="94558-151">连接使用时，会发生情况同样[长轮询](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="94558-151">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="94558-152">长时轮询请求完成后，客户端将打开一个新连接，并请求到达光标位置后的消息。</span><span class="sxs-lookup"><span data-stu-id="94558-152">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="94558-153">光标机制的工作方式即使客户端路由到不同的服务器上重新连接。</span><span class="sxs-lookup"><span data-stu-id="94558-153">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="94558-154">底板已意识到所有服务器，并且它并不重要的客户端连接到哪一台服务器。</span><span class="sxs-lookup"><span data-stu-id="94558-154">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="94558-155">限制</span><span class="sxs-lookup"><span data-stu-id="94558-155">Limitations</span></span>

<span data-ttu-id="94558-156">使用基架，则是低于客户端直接与单个服务器节点通信时的最大消息吞吐量。</span><span class="sxs-lookup"><span data-stu-id="94558-156">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="94558-157">这是因为底板将转发到每个节点，每条消息，因此底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="94558-157">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="94558-158">这一限制是否是问题取决于应用程序。</span><span class="sxs-lookup"><span data-stu-id="94558-158">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="94558-159">例如，下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="94558-159">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="94558-160">[服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)（例如，股票行情）： 背板很适合此方案中，因为该服务器控制速率发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="94558-160">[Server broadcast](../getting-started/tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="94558-161">[客户端到客户端](../getting-started/tutorial-getting-started-with-signalr.md)（如聊天）： 在此方案中，底板可能成为瓶颈如果的消息数会随着客户端的数量; 也就是说，如果消息的速率增长按比例随着越来越多的客户端将加入。</span><span class="sxs-lookup"><span data-stu-id="94558-161">[Client-to-client](../getting-started/tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="94558-162">[高频率实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）： 底板不建议用于此方案。</span><span class="sxs-lookup"><span data-stu-id="94558-162">[High-frequency realtime](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="94558-163">启用跟踪的 SignalR 扩展</span><span class="sxs-lookup"><span data-stu-id="94558-163">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="94558-164">若要启用跟踪背板，请将以下各节添加到 web.config 文件中，根下**配置**元素：</span><span class="sxs-lookup"><span data-stu-id="94558-164">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
