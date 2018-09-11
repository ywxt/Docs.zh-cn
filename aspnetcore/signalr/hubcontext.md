---
title: SignalR HubContext
author: tdykstra
description: 了解如何使用 ASP.NET Core SignalR HubContext 服务用于向外部的客户端从一个中心发送通知。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: 2d7d37b655bf7dbb71b321919314bbb8bef8db17
ms.sourcegitcommit: 57eccdea7d89a62989272f71aad655465f1c600a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2018
ms.locfileid: "44339973"
---
# <a name="send-messages-from-outside-a-hub"></a>从向外发送邮件中心

通过[Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR 中心是用于将消息发送到客户端连接到 SignalR 服务器的核心抽象。 还有可能将消息从你的应用使用中的其他位置发送`IHubContext`服务。 此文章介绍了如何访问 SignalR`IHubContext`将通知发送到外部的客户端从一个中心。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>获取的实例 `IHubContext`

在 ASP.NET Core SignalR，您可以访问的实例`IHubContext`通过依赖关系注入。 您可以注入的实例`IHubContext`到控制器、 中间件或其他 DI 服务。 使用的实例将消息发送到客户端。

> [!NOTE]
> 这不同于 ASP.NET 4.x SignalR GlobalHost 用于提供对访问`IHubContext`。 ASP.NET Core具有的依赖关系注入框架，无需此全局单一实例。

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>注入的实例`IHubContext`控制器中

您可以注入的实例`IHubContext`插入控制器将其添加到您的构造函数：

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

现在，有权访问的实例`IHubContext`，好像您在中心本身中，可以调用集线器方法。

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a>获取的实例`IHubContext`中间件中

访问`IHubContext`中间件管道中如下所示：

```csharp
app.Use(next => async (context) =>
{
    var hubContext = context.RequestServices
                            .GetRequiredService<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> 外部的从调用集线器方法时`Hub`类中，没有与调用相关联的任何调用方。 因此，没有不能访问`ConnectionId`， `Caller`，和`Others`属性。

## <a name="related-resources"></a>相关资源

* [入门](xref:tutorials/signalr)
* [中心](xref:signalr/hubs)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
