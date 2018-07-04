---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 中的 HTTP 消息处理程序 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: daf5bac8203beca3be0036b798188e373b02212a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394516"
---
<a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HTTP 消息处理程序
====================
通过[Mike Wasson](https://github.com/MikeWasson)

一个*消息处理程序*是收到 HTTP 请求并返回 HTTP 响应的类。 消息处理程序派生自抽象**HttpMessageHandler**类。

通常情况下，消息处理程序的一系列链接在一起。 第一个处理程序收到 HTTP 请求、 执行某些处理，并提供请求下一个处理程序。 在某些时候，响应创建，并将返回链。 此模式称为*委派*处理程序。

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>服务器端消息处理程序

在服务器端 Web API 管道使用一些内置消息处理程序：

- **HttpServer**从主机获取该请求。
- **HttpRoutingDispatcher**调度基于路由的请求。
- **HttpControllerDispatcher**将请求发送到 Web API 控制器。

您可以向管道添加自定义处理程序。 消息处理程序非常适用于在 HTTP 消息 （而非控制器操作） 的级别运行的横切关注点。 例如，消息处理程序可能：

- 读取或修改请求标头。
- 将响应标头添加到响应。
- 到达控制器之前，请验证的请求。

此图显示了插入到管道的两个自定义处理程序：

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> 在客户端，HttpClient 还使用消息处理程序。 有关详细信息，请参阅[HttpClient 消息处理程序](httpclient-message-handlers.md)。


## <a name="custom-message-handlers"></a>自定义消息处理程序

若要编写自定义消息处理程序，从派生**System.Net.Http.DelegatingHandler**并重写**SendAsync**方法。 此方法具有以下签名：

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

该方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。 典型实现执行以下任务：

1. 处理请求消息。
2. 调用`base.SendAsync`将请求发送到的内部处理程序。
3. 内部处理程序返回响应消息。 （此步骤是异步的。）
4. 处理响应并将其返回给调用方。

下面是一个简单示例：

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> 对调用`base.SendAsync`是异步的。 如果此调用后，该处理程序执行任何工作，使用**await**关键字，如所示。


一个委派处理程序可以跳过内部处理程序，并直接创建响应：

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

如果委托处理程序将创建无需调用响应`base.SendAsync`，请求将跳过管道的其余部分。 这可用于验证请求 （创建错误响应） 的处理程序。

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>向管道添加一个处理程序

若要在服务器端添加消息处理程序，请将添加到处理程序**HttpConfiguration.MessageHandlers**集合。 如果您使用"ASP.NET MVC 4 Web 应用程序"模板创建项目，则可以执行此内部**WebApiConfig**类：

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

消息处理程序调用中出现的相同顺序**MessageHandlers**集合。 因为它们嵌套的在另一个方向传输时响应消息。 也就是说，最后一个处理程序是获取响应消息的第一个。

请注意，不需要设置内部处理程序;Web API 框架会自动连接消息处理程序。

你是否[自我托管](../older-versions/self-host-a-web-api.md)，创建的实例**HttpSelfHostConfiguration**类，并添加到处理程序**MessageHandlers**集合。

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

现在让我们看看一些示例自定义消息处理程序。

## <a name="example-x-http-method-override"></a>示例： X-HTTP-方法-替代

X HTTP 的方法重写为非标准 HTTP 标头。 它专为不能发送特定 HTTP 请求类型，例如 PUT 或 DELETE 的客户端。 相反，客户端发送 POST 请求，且 X HTTP 的方法重写标头设置为所需的方法。 例如：

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

下面是添加了对 X HTTP 的方法重写支持的消息处理程序：

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

在中**SendAsync**方法，该处理程序检查请求消息是否是 POST 请求，以及它是否包含 X HTTP 的方法重写标头。 如果是这样，它将验证标头值，然后修改请求方法。 最后，该处理程序调用`base.SendAsync`若要将消息传递到下一个处理程序。

当请求到达**HttpControllerDispatcher**类， **HttpControllerDispatcher**基于更新的请求方法请求将路由。

## <a name="example-adding-a-custom-response-header"></a>示例： 添加自定义响应标头

下面是将自定义标头添加到每个响应消息的消息处理程序：

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

首先，该处理程序调用`base.SendAsync`将请求传递给内部消息处理程序。 内部处理程序返回响应消息，但它不使用因此以异步方式**任务&lt;T&gt;** 对象。 响应消息不是后才可`base.SendAsync`以异步方式完成。

此示例使用**await**关键字来执行工作后，将异步`SendAsync`完成。 如果你面向的.NET Framework 4.0，使用**任务**&lt;T&gt;**。ContinueWith**方法：

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>示例： 检查 API 密钥

某些 web 服务要求客户端在其请求中包含的 API 密钥。 下面的示例演示消息处理程序可以检查有效的 API 密钥的请求的方式：

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

此处理程序将查找在 URI 查询字符串中的 API 密钥。 （对于此示例中，我们假定该密钥是静态字符串。 真正的实现可能需要使用更复杂的验证。）如果查询字符串包含的密钥，该处理程序会将请求传递给内部处理程序。

如果请求没有有效的密钥，该处理程序创建响应消息与状态 403，禁止访问。 在这种情况下，该处理程序不会调用`base.SendAsync`，因此内部处理程序永远不会收到请求时，也不在控制器。 因此，控制器可以假定所有传入请求具有有效的 API 密钥。

> [!NOTE]
> 如果 API 密钥仅适用于特定控制器操作，请考虑使用操作筛选器而不消息处理程序。 操作筛选器运行 URI 路由执行后。


## <a name="per-route-message-handlers"></a>每个路由的消息处理程序

中的处理程序**HttpConfiguration.MessageHandlers**集合执行全局应用。

或者，可以将消息处理程序添加到特定的路由时定义的路由,：

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

在此示例中，如果在请求 URI 与匹配"Route2"，请求将被调度到`MessageHandler2`。 下图显示了这两个路由的管道：

![](http-message-handlers/_static/image4.png)

请注意，`MessageHandler2`替换的默认值**HttpControllerDispatcher**。 在此示例中，`MessageHandler2`创建响应，并的匹配"Route2"永远不会转到控制器的请求。 这使您的整个 Web API 控制器机制替换为你自己的自定义终结点。

或者，可以每个路由消息处理程序委托给**HttpControllerDispatcher**，后者随后将调度到的控制器。

![](http-message-handlers/_static/image5.png)

下面的代码演示如何配置此路由：

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
