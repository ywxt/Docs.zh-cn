---
title: 使用 ASP.NET 核心 SignalR 中流式处理
author: rachelappel
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/07/2018
uid: signalr/streaming
ms.openlocfilehash: ae0e733dddfb48db07d77ea73f4673cf8f783b88
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275845"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a>使用 ASP.NET 核心 SignalR 中流式处理

通过[Brennan 勇](https://github.com/BrennanConroy)

ASP.NET 核心 SignalR 支持流式处理服务器方法的返回值。 这是适用于其中的数据片段将出现随时间的方案。 当返回值流式传输到客户端时，每个片段发送到客户端一旦它变为可用，而不是等待可用的所有数据。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="set-up-the-hub"></a>设置中心

当此方法返回后，中心方法将自动成为流式处理的中心方法`ChannelReader<T>`或`Task<ChannelReader<T>>`。 下面是演示流式处理到客户端的数据的基础知识的示例。 每当写入到对象`ChannelReader`该对象立即发送到客户端。 在结束时，`ChannelReader`完成告诉客户端流已关闭。

> [!NOTE]
> 写入`ChannelReader`在后台线程并返回`ChannelReader`越早越好。 将阻止其他中心调用，直到`ChannelReader`返回。

[!code-csharp[Streaming hub method](streaming/sample/hubs/streamhub.cs?range=10-34)]

## <a name="net-client"></a>.NET 客户端

`StreamAsChannelAsync`方法`HubConnection`用于调用流式处理方法。 将中心方法名称、 和到中心方法中定义的自变量传递`StreamAsChannelAsync`。 上的泛型参数`StreamAsChannelAsync<T>`指定流式处理的方法返回的对象的类型。 A`ChannelReader<T>`返回的流调用，并且表示客户端上的流。 若要读取数据，一种常见模式是循环`WaitToReadAsync`并调用`TryRead`数据时可用。 将结束时流已关闭服务器，或取消标记传递给`StreamAsChannelAsync`被取消。

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

## <a name="javascript-client"></a>JavaScript 客户端

JavaScript 客户端调用于中心流式处理方法通过使用`connection.stream`。 `stream`方法接受两个自变量：

* 中心方法的名称。 在以下示例中，中心方法名称是`Counter`。
* 中心方法中定义的自变量。 在下面的示例中的自变量是： 流项，若要接收和流项之间的延迟的数的计数。

`connection.stream` 返回`IStreamResult`其中包含`subscribe`方法。 传递`IStreamSubscriber`到`subscribe`并设置`next`， `error`，和`complete`回调，以获取来自通知`stream`调用。

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

若要结束从客户端调用流`dispose`方法`ISubscription`从返回`subscribe`方法。

## <a name="related-resources"></a>相关资源

* [中心](xref:signalr/hubs)
* [.NET 客户端](xref:signalr/dotnet-client)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)