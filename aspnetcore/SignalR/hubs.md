---
title: 在 ASP.NET 核心 SignalR 使用中心
author: rachelappel
description: 了解如何在 ASP.NET 核心 SignalR 中使用中心。
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubs
ms.openlocfilehash: 73397ba6951f2752653575920bdf739439874366
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2018
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET 核心使用 SignalR 中的中心

通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin 怪兽](https://twitter.com/1kevgriff)

## <a name="what-is-a-signalr-hub"></a>什么是 SignalR hub

SignalR 中心 API，你可以从服务器连接的客户端上调用方法。 在服务器代码中，你可以定义客户端调用的方法。 在客户端代码中，你可以定义从服务器调用的方法。 SignalR 负责在后台，使实时客户端到服务器和服务器客户端通信的所有内容。

## <a name="configure-signalr-hubs"></a>配置 SignalR 集线器

SignalR 中间件需要某些服务，通过调用配置`services.AddSignalR`。

[!code-csharp[Configure service](hubs/sample/startup.cs?range=35)]

在 SignalR 功能添加到 ASP.NET 核心应用程序时，通过调用设置 SignalR 路由`app.UseSignalR`中`Startup.Configure`方法。

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=55-58)]

## <a name="create-and-use-hubs"></a>创建并使用中心

通过声明一个类继承自创建中心`Hub`，并向其中添加公共方法。 客户端可以调用方法定义为`public`。

[!code-csharp[Create and use hubs](hubs/sample/chathub.cs?range=10-13)]

你可以指定返回类型和参数，包括复杂类型并对数组，就像在任何 C# 方法。 SignalR 处理的序列化和反序列化的复杂对象和数组中参数和返回值。

## <a name="the-clients-object"></a>客户端对象

每个实例`Hub`类有一个名为`Clients`包含服务器和客户端之间通信的以下成员：

| 属性 | 描述 |
| ------ | ----------- |
| `All` | 在所有连接的客户端上调用方法 |
| `Caller` | 调用 hub 方法在客户端上调用方法 |
| `Others` | 除调用的方法的客户端的所有连接客户端上调用方法 |

此外，`Hub`类包含以下方法：

| 方法 | 描述 |
| ------ | ----------- |
| `AllExcept` | 在指定的连接除外的所有连接的客户端上调用方法 |
| `Client` | 在特定连接的客户端上调用方法 |
| `Clients` | 在特定连接的客户端上调用方法 |
| `Group` | 将消息发送到指定的组中的所有连接  |
| `GroupExcept` | 将消息发送到指定的组，除非指定连接中的所有连接 |
| `Groups` | 将一条消息发送到多个组的连接  |
| `OthersInGroup` | 将一条消息发送到一组的连接，不包括客户端调用 hub 方法  |
| `User` | 将消息发送到与特定用户关联的所有连接 |
| `Users` | 将消息发送到与指定的用户相关联的所有连接 |

每个属性或方法上表中的返回一个包含对象`SendAsync`方法。 `SendAsync`方法允许你提供的名称和要调用的客户端方法的参数。

## <a name="send-messages-to-clients"></a>将消息发送到客户端

若要使对特定客户端的调用，使用的属性`Clients`对象。 在下面的示例在以下示例中，`SendMessageToCaller`方法演示如何将消息发送到调用 hub 方法的连接。 `SendMessageToGroups`方法将消息发送到存储中的组`List`名为`groups`。

[!code-csharp[Send messages](hubs/sample/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a>处理事件的连接

SignalR 中心 API 提供`OnConnectedAsync`和`OnDisconnectedAsync`虚拟方法，以管理和跟踪连接。 重写`OnConnectedAsync`虚拟方法，客户端连接到集线器，如将其添加到组时，执行操作。

[!code-csharp[Handle events](hubs/sample/chathub.cs?range=26-30)]

## <a name="handle-errors"></a>处理错误

在中心方法中引发的异常会发送到调用的方法的客户端。 JavaScript 客户端上`invoke`方法返回[JavaScript 承诺](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)。 当客户端收到错误处理程序附加到承诺使用`catch`，其调用和作为 JavaScript 传递`Error`对象。

[!code-javascript[Error](hubs/sample/chat.js?range=20)]
[!code-javascript[Error](hubs/sample/chat.js?range=16-18)]

## <a name="related-resources"></a>相关资源

[ASP.NET 核心 SignalR 简介](xref:signalr/introduction)