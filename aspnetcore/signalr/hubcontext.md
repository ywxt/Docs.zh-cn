---
title: SignalR HubContext
author: rachelappel
description: 了解如何使用 ASP.NET 核心 SignalR HubContext 服务用于向外部的客户端从一个中心发送通知。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubcontext
ms.openlocfilehash: 79b91a776a38a2e6810cc89ff0b8d15fe836ce66
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35726066"
---
# <a name="send-messages-from-outside-a-hub"></a><span data-ttu-id="dcb89-103">发送来自外部集线器的邮件</span><span class="sxs-lookup"><span data-stu-id="dcb89-103">Send messages from outside a hub</span></span>

<span data-ttu-id="dcb89-104">通过[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="dcb89-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="dcb89-105">SignalR hub 是用于将消息发送到客户端连接到 SignalR 服务器核心抽象。</span><span class="sxs-lookup"><span data-stu-id="dcb89-105">The SignalR hub is the core abstraction for sending messages to clients connected to the SignalR server.</span></span> <span data-ttu-id="dcb89-106">你也可将消息从中你的应用使用的其他位置发送`IHubContext`服务。</span><span class="sxs-lookup"><span data-stu-id="dcb89-106">It's also possible to send messages from other places in your app using the `IHubContext` service.</span></span> <span data-ttu-id="dcb89-107">此文章介绍了如何访问 SignalR`IHubContext`将通知发送到外部的客户端从一个中心。</span><span class="sxs-lookup"><span data-stu-id="dcb89-107">This article explains how to access a SignalR `IHubContext` to send notifications to clients from outside a hub.</span></span>

<span data-ttu-id="dcb89-108">[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [（如何下载）](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="dcb89-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="get-an-instance-of-ihubcontext"></a><span data-ttu-id="dcb89-109">获取其实例 `IHubContext`</span><span class="sxs-lookup"><span data-stu-id="dcb89-109">Get an instance of `IHubContext`</span></span>

<span data-ttu-id="dcb89-110">在 ASP.NET 核心 SignalR，您可以访问的实例`IHubContext`通过依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="dcb89-110">In ASP.NET Core SignalR, you can access an instance of `IHubContext` via dependency injection.</span></span> <span data-ttu-id="dcb89-111">你可以将注入的实例`IHubContext`到的控制器，中间件或其他 DI 服务。</span><span class="sxs-lookup"><span data-stu-id="dcb89-111">You can inject an instance of `IHubContext` into a controller, middleware, or other DI service.</span></span> <span data-ttu-id="dcb89-112">使用实例将消息发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="dcb89-112">Use the instance to send messages to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="dcb89-113">这不同于 ASP.NET SignalR GlobalHost 用于提供对访问`IHubContext`。</span><span class="sxs-lookup"><span data-stu-id="dcb89-113">This differs from ASP.NET SignalR which used GlobalHost to provide access to the `IHubContext`.</span></span> <span data-ttu-id="dcb89-114">ASP.NET 核心具有的依赖关系注入框架，无需此全局单一实例。</span><span class="sxs-lookup"><span data-stu-id="dcb89-114">ASP.NET Core has a dependency injection framework that removes the need for this global singleton.</span></span>

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a><span data-ttu-id="dcb89-115">注入的实例`IHubContext`控制器中</span><span class="sxs-lookup"><span data-stu-id="dcb89-115">Inject an instance of `IHubContext` in a controller</span></span>

<span data-ttu-id="dcb89-116">你可以将注入的实例`IHubContext`到通过将它添加到您的构造函数的控制器：</span><span class="sxs-lookup"><span data-stu-id="dcb89-116">You can inject an instance of `IHubContext` into a controller by adding it to your constructor:</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

<span data-ttu-id="dcb89-117">现在，有权访问的实例`IHubContext`，就像是中心本身中，可以调用中心的方法。</span><span class="sxs-lookup"><span data-stu-id="dcb89-117">Now, with access to an instance of `IHubContext`, you can call hub methods as if you were in the hub itself.</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a><span data-ttu-id="dcb89-118">获取其实例`IHubContext`中中间件</span><span class="sxs-lookup"><span data-stu-id="dcb89-118">Get an instance of `IHubContext` in middleware</span></span>

<span data-ttu-id="dcb89-119">访问`IHubContext`在该中间件管道中如下所示：</span><span class="sxs-lookup"><span data-stu-id="dcb89-119">Access the `IHubContext` within the middleware pipeline like so:</span></span>

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
> <span data-ttu-id="dcb89-120">何时中心方法调用程序从外部`Hub`类中，没有与调用关联的任何调用方。</span><span class="sxs-lookup"><span data-stu-id="dcb89-120">When hub methods are called from outside of the `Hub` class, there's no caller associated with the invocation.</span></span> <span data-ttu-id="dcb89-121">因此，没有不能访问`ConnectionId`， `Caller`，和`Others`属性。</span><span class="sxs-lookup"><span data-stu-id="dcb89-121">Therefore, there's no access to the `ConnectionId`, `Caller`, and `Others` properties.</span></span>

## <a name="related-resources"></a><span data-ttu-id="dcb89-122">相关资源</span><span class="sxs-lookup"><span data-stu-id="dcb89-122">Related resources</span></span>

* [<span data-ttu-id="dcb89-123">入门</span><span class="sxs-lookup"><span data-stu-id="dcb89-123">Get started</span></span>](xref:signalr/get-started)
* [<span data-ttu-id="dcb89-124">中心</span><span class="sxs-lookup"><span data-stu-id="dcb89-124">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="dcb89-125">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="dcb89-125">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
