---
title: ASP.NET Core SignalR 简介
author: tdykstra
description: 了解如何 ASP.NET Core SignalR 库简化了将实时功能添加到应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: bc6f25c3f35e7fb0c2c68220697f2e0fdc6a9958
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095384"
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 简介

作者：[Rachel Appel](https://twitter.com/rachelappel)

## <a name="what-is-signalr"></a>SignalR 是什么？

ASP.NET Core SignalR 是一个库，简化了添加到应用的实时 web 功能。 实时 web 功能立即使服务器端代码能够将内容推送到客户端。

SignalR 的良好候选项：

* 需要来自服务器的高频率更新的应用程序。 示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用程序。
* 仪表板和监视应用程序。 示例包括公司的仪表板，即时销售更新或旅行警报。
* 协作应用程序。 白板应用和团队会议软件是协作应用程序的示例。
* 需要通知的应用程序。 社交网络、 电子邮件、 聊天、 游戏、 行程警报和许多其他应用程序使用通知。

SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。 Rpc 在客户端上从服务器端.NET Core 代码中调用 JavaScript 函数。

有关 ASP.NET Core SignalR:

* 会自动处理的连接管理。
* 允许同时广播到所有连接的客户端的消息。 例如，聊天室。
* 允许将消息发送到特定的客户端或客户端组。
* 是在开放源代码[GitHub](https://github.com/aspnet/signalr)。
* 可缩放。

客户端和服务器之间的连接是持久性的与 HTTP 连接不同的。

## <a name="transports"></a>传输

SignalR 通过多种方法用于构建实时 web 应用程序的摘要。 [Websocket](https://tools.ietf.org/html/rfc7118)是最佳的传输，但这些不可用时，可以使用其他技术，例如服务器发送事件和长轮询。 SignalR 将自动检测并初始化适当的传输基于在服务器和客户端上受支持的功能。

## <a name="hubs"></a>中心

SignalR 使用中心客户端和服务器之间进行通信。

中心是一个高级的管道，用于允许在客户端和服务器相互调用的方法。 SignalR 处理调度跨计算机界限自动，允许客户端在服务器上调用方法，以轻松地为本地方法，反之亦然。 中心允许将强类型化参数传递给方法，这样将启用模型绑定。 SignalR 提供了两个内置中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。  MessagePack 通常创建与使用 JSON 相比较小的消息。 旧版浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)提供 MessagePack 协议支持。

中心调用通过使用活动传输发送消息的客户端代码。 消息包含名称和客户端的方法的参数。 作为方法参数发送对象是使用配置的协议反序列化。 客户端尝试与客户端代码中的方法的名称匹配。 当找到匹配项时，使用反序列化的参数数据运行的客户端方法。

## <a name="additional-resources"></a>其他资源

* [开始使用 SignalR 为 ASP.NET Core](xref:tutorials/signalr)
* [支持的平台](xref:signalr/supported-platforms)
* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
