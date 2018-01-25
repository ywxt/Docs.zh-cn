---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: "将 SignalR 用户映射至在 SignalR 连接 1.x |Microsoft 文档"
author: pfletcher
description: "本主题说明如何保留有关用户和他们的连接信息。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 896bf4142ce090e39ed5697ff053cd56728318ed
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="d4ae1-103">将 SignalR 用户映射至在 SignalR 连接 1.x</span><span class="sxs-lookup"><span data-stu-id="d4ae1-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>
====================
<span data-ttu-id="d4ae1-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d4ae1-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d4ae1-105">本主题说明如何保留有关用户和他们的连接信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-105">This topic shows how to retain information about users and their connections.</span></span>


## <a name="introduction"></a><span data-ttu-id="d4ae1-106">介绍</span><span class="sxs-lookup"><span data-stu-id="d4ae1-106">Introduction</span></span>

<span data-ttu-id="d4ae1-107">每个客户端将连接到中心将传递唯一连接 id。你可以检索中的此值`Context.ConnectionId`中心上下文的属性。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="d4ae1-108">如果你的应用程序需要以将用户映射到的连接 id 并将保留该映射，你可以使用以下项之一：</span><span class="sxs-lookup"><span data-stu-id="d4ae1-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="d4ae1-109">[内存中存储](#inmemory)，如字典</span><span class="sxs-lookup"><span data-stu-id="d4ae1-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="d4ae1-110">每个用户的的 SignalR 组</span><span class="sxs-lookup"><span data-stu-id="d4ae1-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="d4ae1-111">[永久、 外部存储](#database)，如数据库表或 Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="d4ae1-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="d4ae1-112">每个这些实现是此主题中所示。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="d4ae1-113">你使用`OnConnected`， `OnDisconnected`，和`OnReconnected`方法`Hub`类来跟踪用户连接状态。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="d4ae1-114">你的应用程序的最佳方法取决于：</span><span class="sxs-lookup"><span data-stu-id="d4ae1-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="d4ae1-115">承载你的应用程序的 web 服务器的数目。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="d4ae1-116">是否需要获取当前连接的用户的列表。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="d4ae1-117">是否需要应用程序或服务器重新启动时持久保存组和用户信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="d4ae1-118">调用外部服务器的滞后时间是否出现问题。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="d4ae1-119">下表显示了哪种方法适用于这些注意事项。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="d4ae1-120">多个服务器</span><span class="sxs-lookup"><span data-stu-id="d4ae1-120">More than one server</span></span> | <span data-ttu-id="d4ae1-121">获取当前连接的用户的列表</span><span class="sxs-lookup"><span data-stu-id="d4ae1-121">Get list of currently connected users</span></span> | <span data-ttu-id="d4ae1-122">将重新启动后的信息保留</span><span class="sxs-lookup"><span data-stu-id="d4ae1-122">Persist information after restarts</span></span> | <span data-ttu-id="d4ae1-123">获得最佳性能</span><span class="sxs-lookup"><span data-stu-id="d4ae1-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d4ae1-124">内存中</span><span class="sxs-lookup"><span data-stu-id="d4ae1-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="d4ae1-125">单用户组</span><span class="sxs-lookup"><span data-stu-id="d4ae1-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="d4ae1-126">永久外部</span><span class="sxs-lookup"><span data-stu-id="d4ae1-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="d4ae1-127">内存中存储</span><span class="sxs-lookup"><span data-stu-id="d4ae1-127">In-memory storage</span></span>

<span data-ttu-id="d4ae1-128">下面的示例演示如何保留一个字典，其中存储在内存中的连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="d4ae1-129">字典使用`HashSet`存储的连接 id。在任何时候用户可能具有多个连接到 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="d4ae1-130">例如，通过多个设备或多个浏览器选项卡连接的用户将具有多个连接 id。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="d4ae1-131">如果应用程序关闭时，所有信息都将丢失，但它也将进行重新填充，如用户重新建立连接。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="d4ae1-132">如果您的环境包括多个 web 服务器，因为每个服务器都可以单独的连接集合，则内存中存储无效。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="d4ae1-133">第一个示例演示管理连接到的用户的映射的类。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="d4ae1-134">HashSet 的键将为用户的名称。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="d4ae1-135">下一个示例演示如何使用连接映射类从一个中心。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="d4ae1-136">类的实例存储在变量名`_connections`。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="d4ae1-137">单用户组</span><span class="sxs-lookup"><span data-stu-id="d4ae1-137">Single-user groups</span></span>

<span data-ttu-id="d4ae1-138">可以为每个用户创建组，然后将消息发送到该组，当你想要访问只允许该用户。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="d4ae1-139">每个组的名称是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="d4ae1-140">如果用户具有多个连接，则将每个连接 id 添加到用户的组。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="d4ae1-141">你不应手动删除用户从组用户断开连接时。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="d4ae1-142">由 SignalR 框架自动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="d4ae1-143">下面的示例演示如何实现单用户组。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="d4ae1-144">永久、 外部存储</span><span class="sxs-lookup"><span data-stu-id="d4ae1-144">Permanent, external storage</span></span>

<span data-ttu-id="d4ae1-145">本主题演示如何使用数据库或 Azure 表存储来存储连接信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="d4ae1-146">当你有多个 web 服务器，因为每个 web 服务器可以与相同的数据存储库进行交互时，此方法有效。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="d4ae1-147">如果你的 web 服务器停止工作或应用程序重新启动，`OnDisconnected`不调用方法。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="d4ae1-148">因此，很可能你的数据存储库将具有的连接 id，将不再有效的记录。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="d4ae1-149">若要清理这些孤立的记录，你可能希望使与你的应用程序相关的时间范围之外创建任何连接。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="d4ae1-150">此部分中的示例包括用于跟踪，创建连接时的一个值，但不是显示如何清除旧的记录，因为你可能想要执行此操作作为后台进程。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="d4ae1-151">数据库</span><span class="sxs-lookup"><span data-stu-id="d4ae1-151">Database</span></span>

<span data-ttu-id="d4ae1-152">下面的示例演示如何保留在数据库中的连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="d4ae1-153">你可以使用任何数据访问技术;但是，下面的示例演示如何定义使用 Entity Framework 模型。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="d4ae1-154">这些实体模型对应于数据库表和字段。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="d4ae1-155">您的数据结构无法千差万别，具体取决于你的应用程序的要求。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="d4ae1-156">第一个示例演示如何定义可以与多个连接实体相关联的用户实体。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="d4ae1-157">然后，从中心，你可以跟踪每个连接的状态与下面显示的代码。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="d4ae1-158">Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="d4ae1-158">Azure table storage</span></span>

<span data-ttu-id="d4ae1-159">下面的 Azure 表存储示例是类似于数据库的示例。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="d4ae1-160">它不包括所有需要若要开始使用 Azure 表存储服务的信息。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="d4ae1-161">有关信息，请参阅[如何通过.NET 使用表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="d4ae1-162">下面的示例演示用于存储连接信息的表实体。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="d4ae1-163">它按用户名称，将数据分区，并由连接 id 标识每个实体，以便用户可以在任何时间有多个连接。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="d4ae1-164">在中心，你可以跟踪每个用户的连接的状态。</span><span class="sxs-lookup"><span data-stu-id="d4ae1-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
