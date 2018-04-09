---
title: 在 ASP.NET Core 上的 SignalR 简介
author: rachelappel
description: 了解如何 ASP.NET 核心 SignalR 库简化了将实时 web 功能添加到应用。
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/07/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/introduction-signalr-core
ms.openlocfilehash: 3fa70c957b246787d4e457c74f90ad797b3af766
ms.sourcegitcommit: 6548a3dd0cd1e3e92ac2310dee757ddad9fd6456
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="358de-103">SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="358de-103">Introduction to SignalR</span></span>

<span data-ttu-id="358de-104">作者：[Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="358de-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="358de-105">什么是 SignalR？</span><span class="sxs-lookup"><span data-stu-id="358de-105">What is SignalR?</span></span>

<span data-ttu-id="358de-106">ASP.NET 核心 SignalR 是一个库，简化了添加到应用的实时 web 功能。</span><span class="sxs-lookup"><span data-stu-id="358de-106">ASP.NET Core SignalR is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="358de-107">实时 web 功能可立即使服务器端代码能够将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="358de-107">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="358de-108">适用于 SignalR 的良好候选：</span><span class="sxs-lookup"><span data-stu-id="358de-108">Good candidates for SignalR:</span></span>

* <span data-ttu-id="358de-109">需要从服务器的高频率更新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="358de-109">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="358de-110">示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用。</span><span class="sxs-lookup"><span data-stu-id="358de-110">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="358de-111">仪表板和监视应用程序。</span><span class="sxs-lookup"><span data-stu-id="358de-111">Dashboards and monitoring apps.</span></span> <span data-ttu-id="358de-112">示例包括公司的仪表板，即时销售更新，或经常出差警报。</span><span class="sxs-lookup"><span data-stu-id="358de-112">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="358de-113">协作应用程序。</span><span class="sxs-lookup"><span data-stu-id="358de-113">Collaborative apps.</span></span> <span data-ttu-id="358de-114">白板应用和团队会议软件是协作应用程序的示例。</span><span class="sxs-lookup"><span data-stu-id="358de-114">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="358de-115">需要通知的应用程序。</span><span class="sxs-lookup"><span data-stu-id="358de-115">Apps that require notifications.</span></span> <span data-ttu-id="358de-116">社交网络、 电子邮件、 聊天、 游戏、 旅行警报和很多其他应用程序使用通知。</span><span class="sxs-lookup"><span data-stu-id="358de-116">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="358de-117">SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。</span><span class="sxs-lookup"><span data-stu-id="358de-117">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="358de-118">Rpc 在客户端上从服务器端.NET 核心代码中调用 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="358de-118">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="358de-119">有关 ASP.NET 核心 SignalR:</span><span class="sxs-lookup"><span data-stu-id="358de-119">SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="358de-120">自动处理的连接管理。</span><span class="sxs-lookup"><span data-stu-id="358de-120">Handles connection management automatically.</span></span>
* <span data-ttu-id="358de-121">允许同时广播到所有连接的客户端的消息。</span><span class="sxs-lookup"><span data-stu-id="358de-121">Enables broadcasting messages to all connected clients simultaneously.</span></span> <span data-ttu-id="358de-122">例如，聊天室。</span><span class="sxs-lookup"><span data-stu-id="358de-122">For example, a chat room.</span></span>
* <span data-ttu-id="358de-123">允许将消息发送到特定客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="358de-123">Enables sending messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="358de-124">为在开放源代码[GitHub](https://github.com/aspnet/signalr)。</span><span class="sxs-lookup"><span data-stu-id="358de-124">Is open-sourced at [GitHub](https://github.com/aspnet/signalr).</span></span>
* <span data-ttu-id="358de-125">可缩放。</span><span class="sxs-lookup"><span data-stu-id="358de-125">Scalable.</span></span>

<span data-ttu-id="358de-126">客户端和服务器之间的连接是持久性的与 HTTP 连接不同。</span><span class="sxs-lookup"><span data-stu-id="358de-126">The connection between the client and server is persistent, unlike an HTTP connection.</span></span>

## <a name="transports"></a><span data-ttu-id="358de-127">传输</span><span class="sxs-lookup"><span data-stu-id="358de-127">Transports</span></span>

<span data-ttu-id="358de-128">SignalR 通过多种方法用于构建实时 web 应用程序的摘要。</span><span class="sxs-lookup"><span data-stu-id="358de-128">SignalR abstracts over a number of techniques for building real-time web applications.</span></span> <span data-ttu-id="358de-129">[Websocket](https://tools.ietf.org/html/rfc7118)是最佳的传输，但那些不可用时，可以使用其他技术 Server-Sent 事件和长轮询。</span><span class="sxs-lookup"><span data-stu-id="358de-129">[WebSockets](https://tools.ietf.org/html/rfc7118) is the optimal transport, but other techniques like Server-Sent Events and Long Polling can be used when those aren't available.</span></span> <span data-ttu-id="358de-130">SignalR 将自动检测并初始化了合适的传输，基于在服务器和客户端上受支持的功能。</span><span class="sxs-lookup"><span data-stu-id="358de-130">SignalR will automatically detect and initialize the appropriate transport based on features supported on the server and client.</span></span>

## <a name="hubs-and-endpoints"></a><span data-ttu-id="358de-131">中心和终结点</span><span class="sxs-lookup"><span data-stu-id="358de-131">Hubs and Endpoints</span></span>

<span data-ttu-id="358de-132">SignalR 使用中心和终结点，客户端和服务器之间进行通信。</span><span class="sxs-lookup"><span data-stu-id="358de-132">SignalR uses Hubs and Endpoints to communicate between clients and servers.</span></span> <span data-ttu-id="358de-133">中心 API 介绍的大多数方案。</span><span class="sxs-lookup"><span data-stu-id="358de-133">The Hubs API covers the most scenarios.</span></span>

<span data-ttu-id="358de-134">基于终结点 API，从而使你的客户端和服务器相互调用方法的高级管道，则集线器。</span><span class="sxs-lookup"><span data-stu-id="358de-134">A hub is a high-level pipeline built upon the Endpoint API that allows your client and server to call methods on each other.</span></span> <span data-ttu-id="358de-135">SignalR 处理调度跨计算机界限自动，允许客户端在服务器上调用方法，作为轻松地为本地方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="358de-135">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="358de-136">中心允许将强类型参数传递给方法，从而使模型绑定。</span><span class="sxs-lookup"><span data-stu-id="358de-136">Hubs allow passing strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="358de-137">SignalR 提供两个内置的中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。</span><span class="sxs-lookup"><span data-stu-id="358de-137">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="358de-138">MessagePack 通常会产生较小比时使用 JSON 消息。</span><span class="sxs-lookup"><span data-stu-id="358de-138">MessagePack generally creates smaller messages than when using JSON.</span></span> <span data-ttu-id="358de-139">较旧的浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)以提供 MessagePack 协议支持。</span><span class="sxs-lookup"><span data-stu-id="358de-139">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="358de-140">中心调用通过使用活动传输发送消息的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="358de-140">Hubs call client-side code by sending messages using the active transport.</span></span> <span data-ttu-id="358de-141">消息包含的名称和客户端方法的参数。</span><span class="sxs-lookup"><span data-stu-id="358de-141">The messages contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="358de-142">为方法参数发送的对象是使用已配置的协议反序列化。</span><span class="sxs-lookup"><span data-stu-id="358de-142">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="358de-143">客户端尝试匹配到客户端代码中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="358de-143">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="358de-144">如果找到匹配项，使用反序列化的参数数据运行客户端方法。</span><span class="sxs-lookup"><span data-stu-id="358de-144">When a match happens, the client method runs using the deserialized parameter data.</span></span>

<span data-ttu-id="358de-145">终结点提供原始类似套接字的 API，使其能够读取和写入来自客户端。</span><span class="sxs-lookup"><span data-stu-id="358de-145">Endpoints provide a raw socket-like API, enabling them to read and write from the client.</span></span> <span data-ttu-id="358de-146">它是最多向开发人员处理分组、 广播和其他功能。</span><span class="sxs-lookup"><span data-stu-id="358de-146">It's up to the developer to handle grouping, broadcasting, and other functions.</span></span> <span data-ttu-id="358de-147">中心 API 基于终结点层。</span><span class="sxs-lookup"><span data-stu-id="358de-147">The Hubs API is built on top of the Endpoints layer.</span></span>

<span data-ttu-id="358de-148">下图显示了中心、 终结点，和客户端之间的关系。</span><span class="sxs-lookup"><span data-stu-id="358de-148">The following diagram shows the relationship between hubs, endpoints, and clients.</span></span>

![SignalR 映射](introduction-signalr-core/_static/signalr-core-architecture.png)

## <a name="related-resources"></a><span data-ttu-id="358de-150">相关资源</span><span class="sxs-lookup"><span data-stu-id="358de-150">Related resources</span></span>

[<span data-ttu-id="358de-151">开始使用 SignalR 为 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="358de-151">Get started with SignalR for ASP.NET Core</span></span>](xref:signalr/get-started-signalr-core)
