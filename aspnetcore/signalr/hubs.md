---
title: 在 ASP.NET Core SignalR 使用中心
author: tdykstra
description: 了解如何在 ASP.NET Core SignalR 中使用中心。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/12/2018
uid: signalr/hubs
ms.openlocfilehash: 27aedc5b2f2060d961070fbd1ff5304eaa3956d1
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225351"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET Core 使用 SignalR 中的中心

通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin Griffin](https://twitter.com/1kevgriff)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [（如何下载）](xref:index#how-to-download-a-sample)

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

> [!NOTE]
> 中心是暂时的：
> * 不要将状态存储在中心类的属性。 每个集线器方法调用新的中心实例上执行。  
> * 使用`await`调用取决于中心保持活动状态的异步方法时。 例如，如方法`Clients.All.SendAsync(...)`如果调用，但不可能会失败`await`和集线器方法完成之前`SendAsync`完成。

## <a name="the-context-object"></a>上下文对象

`Hub`类具有`Context`属性，其中包含以下属性与连接有关的信息：

| 属性 | 描述 |
| ------ | ----------- |
| `ConnectionId` | 获取用于此连接，由 SignalR 分配的唯一 ID。 没有为每个连接的一个连接 ID。|
| `UserIdentifier` | 获取[用户标识符](xref:signalr/groups)。 默认情况下，使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符连接相关联。 |
| `User` | 获取`ClaimsPrincipal`与当前用户相关联。 |
| `Items` | 获取可用于共享此连接的作用域内的数据的键/值集合。 数据可以存储在此集合中，它将连接在不同的集线器方法调用中保持原样。 |
| `Features` | 获取在连接上的可用功能的集合。 现在，此集合不需要在大多数情况下，因此它不尚未记录在详细信息。 |
| `ConnectionAborted` | 获取`CancellationToken`，时连接中止通知。 |

`Hub.Context` 此外包含以下方法：

| 方法 | 描述 |
| ------ | ----------- |
| `GetHttpContext` | 返回`HttpContext`用于此连接，或`null`如果连接不是与 HTTP 请求相关联。 对于 HTTP 连接，可以使用此方法以获取 HTTP 标头和查询字符串等信息。 |
| `Abort` | 中止的连接。 |

## <a name="the-clients-object"></a>客户端对象

`Hub`类具有`Clients`属性，其中包含服务器和客户端之间通信的以下属性：

| 属性 | 描述 |
| ------ | ----------- |
| `All` | 在所有连接的客户端上调用的方法 |
| `Caller` | 在客户端调用集线器方法调用的方法 |
| `Others` | 除调用该方法的客户端的所有已连接客户端上调用的方法 |


`Hub.Clients` 此外包含以下方法：

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

## <a name="strongly-typed-hubs"></a>强类型化的中心

使用的一个缺点`SendAsync`是依赖于使用魔幻字符串来指定客户端方法调用。 这将使运行时错误，如果方法名称的拼写错误的代码打开或缺少从客户端。

使用的替代方法`SendAsync`是强类型化`Hub`与<xref:Microsoft.AspNetCore.SignalR.Hub`1>。 在以下示例中，`ChatHub`客户端方法具有出提取到一个接口，称为`IChatClient`。  

[!code-csharp[Interface for IChatClient](hubs/sample/hubs/ichatclient.cs?name=snippet_IChatClient)]

此接口可用于重构前面`ChatHub`示例。

[!code-csharp[Strongly typed ChatHub](hubs/sample/hubs/StronglyTypedChatHub.cs?range=8-18,36)]

使用`Hub<IChatClient>`启用编译时检查的客户端方法。 这可以防止由于使用魔幻字符串导致的问题`Hub<T>`可以仅提供访问权限在接口中定义的方法。

使用强类型化`Hub<T>`禁用的功能使用`SendAsync`。

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
