---
title: SignalR 中管理用户和组
author: rachelappel
description: ASP.NET 核心 SignalR 用户和组管理的概述。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/groups
ms.openlocfilehash: 2a2f129863cf7d5cdfa3c0e5b2d901af52144671
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35358427"
---
# <a name="manage-users-and-groups-in-signalr"></a>SignalR 中管理用户和组

通过[Brennan 勇](https://github.com/BrennanConroy)

SignalR 允许消息发送到与特定用户关联的所有连接以及名为的连接组。

[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)

## <a name="users-in-signalr"></a>SignalR 中的用户

SignalR 可用于将消息发送到与特定用户关联的所有连接。 默认情况下使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符的连接。 单个用户可以有多个连接到 SignalR 应用程序。 例如，用户无法连接上他们的桌面，以及他们的电话。 每个设备都有单独的 SignalR 连接，但它们可以与同一用户所有关联。 如果向用户发送一条消息，所有与该用户关联的连接将收到消息。

将一条消息发送到特定用户，通过将传递到的用户标识符`User`函数中心方法中，如下面的示例所示：

> [!NOTE]
> 用户标识符是区分大小写。

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

可以通过创建自定义用户标识符`IUserIdProvider`，并向在`ConfigureServices`。

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> 注册自定义的 SignalR 服务之前，必须调用 AddSignalR。

## <a name="groups-in-signalr"></a>SignalR 中的组

组是与名称关联的连接的集合。 消息可以发送到一个组中的所有连接。 组是将发送到连接或多个连接，因为组由应用程序管理的建议的方法。 连接可以是多个组的成员。 这使得组理想之选类似于下面的聊天应用程序，其中每个房间可以表示为一组。 可以添加到连接，或将其从通过组中删除`AddToGroupAsync`和`RemoveFromGroupAsync`方法。

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

当连接重新连接时，组成员身份不会保留。 需要重新建立时重新加入组的连接。 不能计算组的成员，因为此信息不可用，如果应用程序扩展到多个服务器。

> [!NOTE]
> 组名称是区分大小写。

## <a name="related-resources"></a>相关资源

* [入门](xref:signalr/get-started)
* [中心](xref:signalr/hubs)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
