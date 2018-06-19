---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: 简介中 SignalR 的向外缩放 1.x |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/29/2013
ms.topic: article
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: ee3384046bf8a0f363aa6801d7a46f68b2bf125a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28043741"
---
<a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="8dacf-102">简介中 SignalR 的向外缩放 1.x</span><span class="sxs-lookup"><span data-stu-id="8dacf-102">Introduction to Scaleout in SignalR 1.x</span></span>
====================
<span data-ttu-id="8dacf-103">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8dacf-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="8dacf-104">一般情况下，有两种方法来扩展 web 应用程序：*向上扩展*和*向外扩展*。</span><span class="sxs-lookup"><span data-stu-id="8dacf-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="8dacf-105">使用更多 RAM、 Cpu、 等使用更大的服务器 （或较大的 VM） 的方式向上扩展。</span><span class="sxs-lookup"><span data-stu-id="8dacf-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="8dacf-106">扩展意味着添加更多服务器以处理负载。</span><span class="sxs-lookup"><span data-stu-id="8dacf-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="8dacf-107">向上扩展的问题是你快速命中了机的大小限制。</span><span class="sxs-lookup"><span data-stu-id="8dacf-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="8dacf-108">除此之外，你需要向外扩展。但是，当你向外扩展，客户端可以获取路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="8dacf-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="8dacf-109">连接到一台服务器的客户端不会收到从另一台服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="8dacf-110">一种解决方案是将使用名为的组件，在服务器之间的消息转发*底板*。</span><span class="sxs-lookup"><span data-stu-id="8dacf-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="8dacf-111">启用底板，每个应用程序实例将消息发送到底板，与底板将其转发给其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="8dacf-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="8dacf-112">（在电子行业，底板是并行的连接器的组。</span><span class="sxs-lookup"><span data-stu-id="8dacf-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="8dacf-113">打比方，SignalR 基架连接多个服务器。）</span><span class="sxs-lookup"><span data-stu-id="8dacf-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="8dacf-114">SignalR 目前提供三个背板：</span><span class="sxs-lookup"><span data-stu-id="8dacf-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="8dacf-115">**Azure Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="8dacf-115">**Azure Service Bus**.</span></span> <span data-ttu-id="8dacf-116">Service Bus 是允许组件按松散耦合的方式发送消息的消息传递基础结构。</span><span class="sxs-lookup"><span data-stu-id="8dacf-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="8dacf-117">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="8dacf-117">**Redis**.</span></span> <span data-ttu-id="8dacf-118">Redis 是一个内存中键 / 值存储。</span><span class="sxs-lookup"><span data-stu-id="8dacf-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="8dacf-119">Redis 支持发布/订阅 ("pub/sub") 模式，用于将消息发送。</span><span class="sxs-lookup"><span data-stu-id="8dacf-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="8dacf-120">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="8dacf-120">**SQL Server**.</span></span> <span data-ttu-id="8dacf-121">SQL Server 底板将消息写入 SQL 表。</span><span class="sxs-lookup"><span data-stu-id="8dacf-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="8dacf-122">底板为有效的消息传递使用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="8dacf-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="8dacf-123">但是，它还适用如果未启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="8dacf-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="8dacf-124">如果你部署 Azure 上的应用程序，请考虑使用 Azure Service Bus 底板。</span><span class="sxs-lookup"><span data-stu-id="8dacf-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="8dacf-125">如果将部署到你自己的服务器场，请考虑 SQL Server 或 Redis 背板。</span><span class="sxs-lookup"><span data-stu-id="8dacf-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="8dacf-126">以下主题包含针对每个底板的分步教程：</span><span class="sxs-lookup"><span data-stu-id="8dacf-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="8dacf-127">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="8dacf-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="8dacf-128">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="8dacf-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="8dacf-129">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="8dacf-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="8dacf-130">实现</span><span class="sxs-lookup"><span data-stu-id="8dacf-130">Implementation</span></span>

<span data-ttu-id="8dacf-131">在 SignalR 通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="8dacf-132">消息总线实现[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，从而提供发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="8dacf-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="8dacf-133">通过替换默认的工作的底板**IMessageBus**含总线为该底板设计的。</span><span class="sxs-lookup"><span data-stu-id="8dacf-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="8dacf-134">例如，Redis 消息总线是[RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)，并使用 Redis [pub/sub](http://redis.io/topics/pubsub)机制来发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="8dacf-135">每个服务器实例连接到通过总线底板。</span><span class="sxs-lookup"><span data-stu-id="8dacf-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="8dacf-136">发送一条消息，它将转到面板，并底板将其发送到每个服务器。</span><span class="sxs-lookup"><span data-stu-id="8dacf-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="8dacf-137">当服务器从底板获取一条消息时，它会在其本地缓存中将该消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="8dacf-138">服务器然后将从其本地缓存消息传送到客户端。</span><span class="sxs-lookup"><span data-stu-id="8dacf-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="8dacf-139">对于每个客户端连接，在读取消息流的客户端的进度被跟踪使用游标。</span><span class="sxs-lookup"><span data-stu-id="8dacf-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="8dacf-140">（游标表示消息流中的位置。）如果客户端断开连接并重新连接，但它会将总线要求提供任何客户端的光标在值后到达的消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="8dacf-141">连接使用时，会发生情况同样[长轮询](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="8dacf-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="8dacf-142">长时轮询请求完成后，客户端将打开一个新连接，并请求到达光标位置后的消息。</span><span class="sxs-lookup"><span data-stu-id="8dacf-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="8dacf-143">光标机制的工作方式即使客户端路由到不同的服务器上重新连接。</span><span class="sxs-lookup"><span data-stu-id="8dacf-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="8dacf-144">底板已意识到所有服务器，并且它并不重要的客户端连接到哪一台服务器。</span><span class="sxs-lookup"><span data-stu-id="8dacf-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="8dacf-145">限制</span><span class="sxs-lookup"><span data-stu-id="8dacf-145">Limitations</span></span>

<span data-ttu-id="8dacf-146">使用基架，则是低于客户端直接与单个服务器节点通信时的最大消息吞吐量。</span><span class="sxs-lookup"><span data-stu-id="8dacf-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="8dacf-147">这是因为底板将转发到每个节点，每条消息，因此底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="8dacf-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="8dacf-148">这一限制是否是问题取决于应用程序。</span><span class="sxs-lookup"><span data-stu-id="8dacf-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="8dacf-149">例如，下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="8dacf-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="8dacf-150">[服务器广播](tutorial-server-broadcast-with-aspnet-signalr.md)（例如，股票行情）： 背板很适合此方案中，因为该服务器控制速率发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="8dacf-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="8dacf-151">[客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）： 在此方案中，底板可能成为瓶颈如果的消息数会随着客户端的数量; 也就是说，如果消息的速率增长按比例随着越来越多的客户端将加入。</span><span class="sxs-lookup"><span data-stu-id="8dacf-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="8dacf-152">[高频率实时](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）： 底板不建议用于此方案。</span><span class="sxs-lookup"><span data-stu-id="8dacf-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="8dacf-153">启用跟踪的 SignalR 扩展</span><span class="sxs-lookup"><span data-stu-id="8dacf-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="8dacf-154">若要启用跟踪背板，请将以下各节添加到 web.config 文件中，根下**配置**元素：</span><span class="sxs-lookup"><span data-stu-id="8dacf-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
