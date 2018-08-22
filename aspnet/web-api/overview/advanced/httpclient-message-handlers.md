---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API 中的 HttpClient 消息处理程序 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/01/2012
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 764244d1299d8cfcb59c3f15d63b42ebff4f6ac0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826219"
---
<a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API 中的 HttpClient 消息处理程序
====================
通过[Mike Wasson](https://github.com/MikeWasson)

一个*消息处理程序*是收到 HTTP 请求并返回 HTTP 响应的类。

通常情况下，消息处理程序的一系列链接在一起。 第一个处理程序收到 HTTP 请求、 执行某些处理，并提供请求下一个处理程序。 在某些时候，响应创建，并将返回链。 此模式称为*委派*处理程序。

![](httpclient-message-handlers/_static/image1.png)

客户端侧**HttpClient**类使用消息处理程序来处理请求。 默认处理程序是**HttpClientHandler**，其通过网络发送请求，并从服务器获取响应。 可以插入到客户端管道的自定义消息处理程序：

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API 在服务器端还使用消息处理程序。 有关详细信息，请参阅[HTTP 消息处理程序](http-message-handlers.md)。


## <a name="custom-message-handlers"></a>自定义消息处理程序

若要编写自定义消息处理程序，从派生**System.Net.Http.DelegatingHandler**并重写**SendAsync**方法。 以下是方法签名：

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

该方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。 典型实现执行以下任务：

1. 处理请求消息。
2. 调用`base.SendAsync`将请求发送到的内部处理程序。
3. 内部处理程序返回响应消息。 （此步骤是异步的。）
4. 处理响应并将其返回给调用方。

下面的示例显示了将自定义标头添加到传出请求的消息处理程序：

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

对调用`base.SendAsync`是异步的。 如果此调用后，该处理程序执行任何工作，使用**await**关键字在方法完成后恢复执行。 下面的示例演示的处理程序日志错误代码。 日志记录本身不是很有趣，但该示例演示如何获取在处理程序的响应。

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>将消息处理程序添加到客户端管道

若要添加到自定义处理程序**HttpClient**，使用**HttpClientFactory.Create**方法：

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

消息处理程序调用传递到它们的顺序**创建**方法。 嵌套的处理程序，因为在另一个方向传输时的响应消息。 也就是说，最后一个处理程序是获取响应消息的第一个。
