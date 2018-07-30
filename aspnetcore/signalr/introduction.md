---
title: ASP.NET Core SignalR 简介
author: tdykstra
description: 了解如何 ASP.NET Core SignalR 库简化了将实时功能添加到应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: 2fff24609caf7592bad763a077288990a29617aa
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342544"
---
# <a name="introduction-to-aspnet-core-signalr"></a>ASP.NET Core SignalR 简介

## <a name="what-is-signalr"></a>SignalR 是什么？

ASP.NET Core SignalR 是一个开放源代码库，它简化了向应用添加实时 web 功能。 实时 web 功能立即使服务器端代码能够将内容推送到客户端。

SignalR 的良好候选项：

* 需要来自服务器的高频率更新的应用程序。 示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用程序。
* 仪表板和监视应用程序。 示例包括公司的仪表板，即时销售更新或旅行警报。
* 协作应用程序。 白板应用和团队会议软件是协作应用程序的示例。
* 需要通知的应用程序。 社交网络、 电子邮件、 聊天、 游戏、 行程警报和许多其他应用程序使用通知。

SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。 Rpc 在客户端上从服务器端.NET Core 代码中调用 JavaScript 函数。

下面是适用于 ASP.NET Core SignalR 的一些功能：

* 会自动处理的连接管理。
* 同时将消息发送到所有连接的客户端。 例如，聊天室。
* 将消息发送到特定的客户端或客户端组。
* 扩展以处理增加的流量。

源托管在[SignalR GitHub 上的存储库](https://github.com/aspnet/signalr)。

## <a name="transports"></a>传输

SignalR 支持几种方法用于处理实时通信：

* [WebSockets](https://tools.ietf.org/html/rfc7118)
* 服务器发送事件
* 很长的轮询

SignalR 会自动选择最佳传输方法内的服务器和客户端的功能。

## <a name="hubs"></a>中心

使用 SignalR*中心*客户端和服务器之间进行通信。

中心是一个高级的管道，用于允许客户端和服务器相互调用的方法。 SignalR 处理调度跨计算机界限自动，允许客户端调用的方法在服务器上，反之亦然。 您可以强类型化参数传递到方法，这样将启用模型绑定。 SignalR 提供了两个内置中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。  MessagePack 通常会产生较小的消息为 JSON 进行比较。 旧版浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)提供 MessagePack 协议支持。

中心通过发送消息，其中包含名称和客户端的方法的参数调用客户端代码。 作为方法参数发送对象是使用配置的协议反序列化。 客户端尝试与客户端代码中的方法的名称匹配。 当客户端找到了匹配项时，它调用方法，并将反序列化的参数数据传递给它。

## <a name="additional-resources"></a>其他资源

* [开始使用 SignalR 为 ASP.NET Core](xref:tutorials/signalr)
* [支持的平台](xref:signalr/supported-platforms)
* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
