---
title: 使用 ASP.NET Core SignalR 中流式处理
author: tdykstra
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/07/2018
uid: signalr/streaming
ms.openlocfilehash: 0001eed830249ac46ba35331759187bb4e7e8fd3
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095257"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a><span data-ttu-id="a18ff-102">使用 ASP.NET Core SignalR 中流式处理</span><span class="sxs-lookup"><span data-stu-id="a18ff-102">Use streaming in ASP.NET Core SignalR</span></span>

<span data-ttu-id="a18ff-103">通过[brennan，第 Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="a18ff-103">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="a18ff-104">ASP.NET Core SignalR 支持流式处理服务器方法的返回值。</span><span class="sxs-lookup"><span data-stu-id="a18ff-104">ASP.NET Core SignalR supports streaming return values of server methods.</span></span> <span data-ttu-id="a18ff-105">这是适用于其中的数据片段会随时间的方案。</span><span class="sxs-lookup"><span data-stu-id="a18ff-105">This is useful for scenarios where fragments of data will come in over time.</span></span> <span data-ttu-id="a18ff-106">当返回值流式传输到客户端时，每个片段是发送到客户端变得可用，而非等待所有的数据变得可用。</span><span class="sxs-lookup"><span data-stu-id="a18ff-106">When a return value is streamed to the client, each fragment is sent to the client as soon as it becomes available, rather than waiting for all the data to become available.</span></span>

<span data-ttu-id="a18ff-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="a18ff-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="set-up-the-hub"></a><span data-ttu-id="a18ff-108">设置中心</span><span class="sxs-lookup"><span data-stu-id="a18ff-108">Set up the hub</span></span>

<span data-ttu-id="a18ff-109">集线器方法自动成为流式处理的集线器方法时它将返回`ChannelReader<T>`或`Task<ChannelReader<T>>`。</span><span class="sxs-lookup"><span data-stu-id="a18ff-109">A hub method automatically becomes a streaming hub method when it returns a `ChannelReader<T>` or a `Task<ChannelReader<T>>`.</span></span> <span data-ttu-id="a18ff-110">下面是一个示例，显示的数据流式传输到客户端的基础知识。</span><span class="sxs-lookup"><span data-stu-id="a18ff-110">Below is a sample that shows the basics of streaming data to the client.</span></span> <span data-ttu-id="a18ff-111">每当将对象写入到`ChannelReader`该对象将立即发送给客户端。</span><span class="sxs-lookup"><span data-stu-id="a18ff-111">Whenever an object is written to the `ChannelReader` that object is immediately sent to the client.</span></span> <span data-ttu-id="a18ff-112">在结束时，`ChannelReader`完成告诉客户端流已关闭。</span><span class="sxs-lookup"><span data-stu-id="a18ff-112">At the end, the `ChannelReader` is completed to tell the client the stream is closed.</span></span>

> [!NOTE]
> <span data-ttu-id="a18ff-113">写入`ChannelReader`在后台线程并返回`ChannelReader`越早越好。</span><span class="sxs-lookup"><span data-stu-id="a18ff-113">Write to the `ChannelReader` on a background thread and return the `ChannelReader` as soon as possible.</span></span> <span data-ttu-id="a18ff-114">将阻止其他集线器调用，直到`ChannelReader`返回。</span><span class="sxs-lookup"><span data-stu-id="a18ff-114">Other hub invocations will be blocked until a `ChannelReader` is returned.</span></span>

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?range=10-34)]

## <a name="net-client"></a><span data-ttu-id="a18ff-115">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="a18ff-115">.NET client</span></span>

<span data-ttu-id="a18ff-116">`StreamAsChannelAsync`方法`HubConnection`用于调用流式处理方法。</span><span class="sxs-lookup"><span data-stu-id="a18ff-116">The `StreamAsChannelAsync` method on `HubConnection` is used to invoke a streaming method.</span></span> <span data-ttu-id="a18ff-117">将中心方法名称和到中心方法中定义的自变量传递`StreamAsChannelAsync`。</span><span class="sxs-lookup"><span data-stu-id="a18ff-117">Pass the hub method name, and arguments defined in the hub method to `StreamAsChannelAsync`.</span></span> <span data-ttu-id="a18ff-118">上的泛型参数`StreamAsChannelAsync<T>`指定流式处理方法返回的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="a18ff-118">The generic parameter on `StreamAsChannelAsync<T>` specifies the type of objects returned by the streaming method.</span></span> <span data-ttu-id="a18ff-119">一个`ChannelReader<T>`返回从流调用，并且表示在客户端上的流。</span><span class="sxs-lookup"><span data-stu-id="a18ff-119">A `ChannelReader<T>` is returned from the stream invocation, and represents the stream on the client.</span></span> <span data-ttu-id="a18ff-120">若要读取数据，常见模式是循环访问`WaitToReadAsync`，并调用`TryRead`数据时可用。</span><span class="sxs-lookup"><span data-stu-id="a18ff-120">To read data, a common pattern is to loop over `WaitToReadAsync` and call `TryRead` when data is available.</span></span> <span data-ttu-id="a18ff-121">循环将结束时该流已关闭服务器，或取消标记传递给`StreamAsChannelAsync`被取消。</span><span class="sxs-lookup"><span data-stu-id="a18ff-121">The loop will end when the stream has been closed by the server, or the cancellation token passed to `StreamAsChannelAsync` is canceled.</span></span>

```csharp
var channel = await hubConnection.StreamAsChannelAsync<int>("Counter", 10, 500, CancellationToken.None);

// Wait asynchronously for data to become available
while (await channel.WaitToReadAsync())
{
    // Read all currently available data synchronously, before waiting for more data
    while (channel.TryRead(out var count))
    {
        Console.WriteLine($"{count}");
    }
}

Console.WriteLine("Streaming completed");
```

## <a name="javascript-client"></a><span data-ttu-id="a18ff-122">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="a18ff-122">JavaScript client</span></span>

<span data-ttu-id="a18ff-123">JavaScript 客户端调用集线器上流式处理方法使用`connection.stream`。</span><span class="sxs-lookup"><span data-stu-id="a18ff-123">JavaScript clients call streaming methods on hubs by using `connection.stream`.</span></span> <span data-ttu-id="a18ff-124">`stream`方法接受两个参数：</span><span class="sxs-lookup"><span data-stu-id="a18ff-124">The `stream` method accepts two arguments:</span></span>

* <span data-ttu-id="a18ff-125">集线器方法的名称。</span><span class="sxs-lookup"><span data-stu-id="a18ff-125">The name of the hub method.</span></span> <span data-ttu-id="a18ff-126">在以下示例中，中心方法名称是`Counter`。</span><span class="sxs-lookup"><span data-stu-id="a18ff-126">In the following example, the hub method name is `Counter`.</span></span>
* <span data-ttu-id="a18ff-127">在集线器方法中定义的参数。</span><span class="sxs-lookup"><span data-stu-id="a18ff-127">Arguments defined in the hub method.</span></span> <span data-ttu-id="a18ff-128">在以下示例中，参数是： 若要接收的流项和流项之间的延迟的数量的计数。</span><span class="sxs-lookup"><span data-stu-id="a18ff-128">In the following example, the arguments are: a count for the number of stream items to receive, and the delay between stream items.</span></span>

<span data-ttu-id="a18ff-129">`connection.stream` 返回`IStreamResult`其中包含`subscribe`方法。</span><span class="sxs-lookup"><span data-stu-id="a18ff-129">`connection.stream` returns an `IStreamResult` which contains a `subscribe` method.</span></span> <span data-ttu-id="a18ff-130">传递`IStreamSubscriber`到`subscribe`并设置`next`， `error`，并`complete`回调以获取来自通知`stream`调用。</span><span class="sxs-lookup"><span data-stu-id="a18ff-130">Pass an `IStreamSubscriber` to `subscribe` and set the `next`, `error`, and `complete` callbacks to get notifications from the `stream` invocation.</span></span>

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

<span data-ttu-id="a18ff-131">若要结束的客户端调用的流`dispose`方法`ISubscription`从返回`subscribe`方法。</span><span class="sxs-lookup"><span data-stu-id="a18ff-131">To end the stream from the client call the `dispose` method on the `ISubscription` that is returned from the `subscribe` method.</span></span>

## <a name="related-resources"></a><span data-ttu-id="a18ff-132">相关资源</span><span class="sxs-lookup"><span data-stu-id="a18ff-132">Related resources</span></span>

* [<span data-ttu-id="a18ff-133">中心</span><span class="sxs-lookup"><span data-stu-id="a18ff-133">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="a18ff-134">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="a18ff-134">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="a18ff-135">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="a18ff-135">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="a18ff-136">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="a18ff-136">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
