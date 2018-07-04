---
title: SignalR HubContext
author: rachelappel
description: 了解如何使用 ASP.NET Core SignalR HubContext 服务用于向外部的客户端从一个中心发送通知。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: ccfcdc8337275fd26e09c1a43db36cf9ab90cf46
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277756"
---
# <a name="send-messages-from-outside-a-hub"></a>发送来自外部集线器的邮件

通过[Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR hub 是用于将消息发送到客户端连接到 SignalR 服务器核心抽象。 你也可将消息从中你的应用使用的其他位置发送`IHubContext`服务。 此文章介绍了如何访问 SignalR`IHubContext`将通知发送到外部的客户端从一个中心。

[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>获取其实例 `IHubContext`

在 ASP.NET Core SignalR，您可以访问的实例`IHubContext`通过依赖关系注入。 你可以将注入的实例`IHubContext`到的控制器，中间件或其他 DI 服务。 使用实例将消息发送到客户端。

> [!NOTE]
> 这不同于 ASP.NET SignalR GlobalHost 用于提供对访问`IHubContext`。 ASP.NET Core 具有的依赖关系注入框架，无需此全局单一实例。

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>注入的实例`IHubContext`控制器中

你可以将注入的实例`IHubContext`到通过将它添加到您的构造函数的控制器：

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

现在，有权访问的实例`IHubContext`，就像是中心本身中，可以调用中心的方法。

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a>获取其实例`IHubContext`中中间件

访问`IHubContext`在该中间件管道中如下所示：

```csharp
app.Use(next => (context) =>
{
    var hubContext = (IHubContext<MyHub>)context
                        .RequestServices
                        .GetServices<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> 何时中心方法调用程序从外部`Hub`类中，没有与调用关联的任何调用方。 因此，没有不能访问`ConnectionId`， `Caller`，和`Others`属性。

## <a name="related-resources"></a>相关资源

* [入门](xref:tutorials/signalr)
* [中心](xref:signalr/hubs)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
