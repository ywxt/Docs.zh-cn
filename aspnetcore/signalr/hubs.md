---
title: 在 ASP.NET Core SignalR 使用中心
author: tdykstra
description: 了解如何在 ASP.NET Core SignalR 中使用中心。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/01/2018
uid: signalr/hubs
ms.openlocfilehash: be39666373e2b099054bb71f4a7fcf17aeb9a01c
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095276"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET Core 使用 SignalR 中的中心

通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin Griffin](https://twitter.com/1kevgriff)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)

## <a name="what-is-a-signalr-hub"></a>SignalR 中心是什么

SignalR 中心 API，可从服务器在连接的客户端上调用方法。 在服务器代码中，定义客户端调用的方法。 在客户端代码中，定义从服务器调用的方法。 SignalR 负责在后台实现实时的客户端到服务器和服务器到客户端通信的所有内容。

## <a name="configure-signalr-hubs"></a>配置 SignalR 集线器

SignalR 中间件需要某些服务，通过调用配置`services.AddSignalR`。

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

在 SignalR 功能添加到 ASP.NET Core 应用程序时，通过调用设置 SignalR 路由`app.UseSignalR`中`Startup.Configure`方法。

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a>创建和使用中心

通过声明继承的类创建一个中心`Hub`，并向其添加公共方法。 客户端可以调用方法定义为`public`。

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

您可以指定返回类型和参数，包括复杂类型和数组，就像在任何 C# 方法中。 SignalR 处理序列化和反序列化复杂对象和数组中参数和返回值。

## <a name="the-clients-object"></a>客户端对象

每个实例`Hub`类有一个名为`Clients`，其中包含服务器和客户端之间通信的以下成员：

| 属性 | 描述 |
| ------ | ----------- |
| `All` | 在所有连接的客户端上调用的方法 |
| `Caller` | 在客户端调用集线器方法调用的方法 |
| `Others` | 除调用该方法的客户端的所有已连接客户端上调用的方法 |


此外，`Hub.Clients`包含以下方法：

| 方法 | 描述 |
| ------ | ----------- |
| `AllExcept` | 除了指定连接的所有已连接客户端上调用的方法 |
| `Client` | 调用特定连接的客户端上的方法 |
| `Clients` | 调用特定连接的客户端上的方法 |
| `Group` | 调用指定的组中的所有连接到的方法  |
| `GroupExcept` | 调用中指定的组，除非指定连接到的所有连接的方法 |
| `Groups` | 调用到多个组的连接方法  |
| `OthersInGroup` | 调用到一组连接，不包括客户端调用集线器方法的方法  |
| `User` | 调用与特定用户关联的所有连接到的方法 |
| `Users` | 调用到与指定的用户相关联的所有连接的方法 |

每个属性或方法上表中的返回一个包含对象`SendAsync`方法。 `SendAsync`方法允许您提供的名称和要调用的客户端方法的参数。

## <a name="send-messages-to-clients"></a>将消息发送到客户端

若要使对特定的客户端的调用，使用的属性`Clients`对象。 在以下示例中，`SendMessageToCaller`方法演示如何将消息发送到调用集线器方法的连接。 `SendMessageToGroups`方法将消息发送到存储中的组`List`名为`groups`。

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a>处理连接事件

SignalR 中心 API 提供了`OnConnectedAsync`和`OnDisconnectedAsync`管理和跟踪连接的虚拟方法。 重写`OnConnectedAsync`虚拟方法，客户端连接到中心，如将其添加到组时，执行操作。

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a>处理错误

集线器方法中引发的异常将发送到的客户端的调用的方法。 在 JavaScript 客户端`invoke`方法将返回[JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)。 当客户端收到的错误处理程序附加到承诺使用`catch`，它具有调用，并且作为 JavaScript 传递`Error`对象。

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a>相关资源

* [ASP.NET Core SignalR 简介](xref:signalr/introduction)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
