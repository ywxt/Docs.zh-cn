---
title: ASP.NET Core SignalR 简介
author: rachelappel
description: 了解如何 ASP.NET Core SignalR 库简化了将实时功能添加到应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: 0c833acea139d22883a69a02c2357a71f3ac8db8
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277899"
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 简介

作者：[Rachel Appel](https://twitter.com/rachelappel)

## <a name="what-is-signalr"></a>什么是 SignalR？

ASP.NET Core SignalR 是一个库，简化了添加到应用的实时 web 功能。 实时 web 功能可立即使服务器端代码能够将内容推送到客户端。

适用于 SignalR 的良好候选：

* 需要从服务器的高频率更新的应用程序。 示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用。
* 仪表板和监视应用程序。 示例包括公司的仪表板，即时销售更新，或经常出差警报。
* 协作应用程序。 白板应用和团队会议软件是协作应用程序的示例。
* 需要通知的应用程序。 社交网络、 电子邮件、 聊天、 游戏、 旅行警报和很多其他应用程序使用通知。

SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。 Rpc 在客户端上从服务器端.NET Core代码中调用 JavaScript 函数。

有关 ASP.NET Core SignalR:

* 自动处理的连接管理。
* 允许同时广播到所有连接的客户端的消息。 例如，聊天室。
* 允许将消息发送到特定客户端或客户端组。
* 为在开放源代码[GitHub](https://github.com/aspnet/signalr)。
* 可缩放。

客户端和服务器之间的连接是持久性的与 HTTP 连接不同。

## <a name="transports"></a>传输

SignalR 通过多种方法用于构建实时 web 应用程序的摘要。 [Websocket](https://tools.ietf.org/html/rfc7118)是最佳的传输，但那些不可用时，可以使用其他技术 Server-Sent 事件和长轮询。 SignalR 将自动检测并初始化了合适的传输，基于在服务器和客户端上受支持的功能。

## <a name="hubs"></a>中心

SignalR 使用中心客户端和服务器之间进行通信。

中心是一种高级的管道，允许你的客户端和服务器相互调用方法。 SignalR 处理调度跨计算机界限自动，允许客户端在服务器上调用方法，作为轻松地为本地方法，反之亦然。 中心允许将强类型参数传递给方法，从而使模型绑定。 SignalR 提供两个内置的中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。  MessagePack 通常会产生较小比时使用 JSON 消息。 较旧的浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)以提供 MessagePack 协议支持。

中心调用通过使用活动传输发送消息的客户端代码。 消息包含的名称和客户端方法的参数。 为方法参数发送的对象是使用已配置的协议反序列化。 客户端尝试匹配到客户端代码中的方法的名称。 如果找到匹配项，使用反序列化的参数数据运行客户端方法。

## <a name="additional-resources"></a>其他资源

* [开始使用 SignalR 为 ASP.NET Core](xref:tutorials/signalr)
* [支持的平台](xref:signalr/supported-platforms)
* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
