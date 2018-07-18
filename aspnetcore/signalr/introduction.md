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
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="775fe-103">ASP.NET Core SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="775fe-103">Introduction to ASP.NET Core SignalR</span></span>

<span data-ttu-id="775fe-104">作者：[Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="775fe-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="775fe-105">SignalR 是什么？</span><span class="sxs-lookup"><span data-stu-id="775fe-105">What is SignalR?</span></span>

<span data-ttu-id="775fe-106">ASP.NET Core SignalR 是一个库，简化了添加到应用的实时 web 功能。</span><span class="sxs-lookup"><span data-stu-id="775fe-106">ASP.NET Core SignalR is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="775fe-107">实时 web 功能立即使服务器端代码能够将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="775fe-107">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="775fe-108">SignalR 的良好候选项：</span><span class="sxs-lookup"><span data-stu-id="775fe-108">Good candidates for SignalR:</span></span>

* <span data-ttu-id="775fe-109">需要来自服务器的高频率更新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="775fe-109">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="775fe-110">示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="775fe-110">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="775fe-111">仪表板和监视应用程序。</span><span class="sxs-lookup"><span data-stu-id="775fe-111">Dashboards and monitoring apps.</span></span> <span data-ttu-id="775fe-112">示例包括公司的仪表板，即时销售更新或旅行警报。</span><span class="sxs-lookup"><span data-stu-id="775fe-112">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="775fe-113">协作应用程序。</span><span class="sxs-lookup"><span data-stu-id="775fe-113">Collaborative apps.</span></span> <span data-ttu-id="775fe-114">白板应用和团队会议软件是协作应用程序的示例。</span><span class="sxs-lookup"><span data-stu-id="775fe-114">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="775fe-115">需要通知的应用程序。</span><span class="sxs-lookup"><span data-stu-id="775fe-115">Apps that require notifications.</span></span> <span data-ttu-id="775fe-116">社交网络、 电子邮件、 聊天、 游戏、 行程警报和许多其他应用程序使用通知。</span><span class="sxs-lookup"><span data-stu-id="775fe-116">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="775fe-117">SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。</span><span class="sxs-lookup"><span data-stu-id="775fe-117">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="775fe-118">Rpc 在客户端上从服务器端.NET Core 代码中调用 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="775fe-118">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="775fe-119">有关 ASP.NET Core SignalR:</span><span class="sxs-lookup"><span data-stu-id="775fe-119">SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="775fe-120">会自动处理的连接管理。</span><span class="sxs-lookup"><span data-stu-id="775fe-120">Handles connection management automatically.</span></span>
* <span data-ttu-id="775fe-121">允许同时广播到所有连接的客户端的消息。</span><span class="sxs-lookup"><span data-stu-id="775fe-121">Enables broadcasting messages to all connected clients simultaneously.</span></span> <span data-ttu-id="775fe-122">例如，聊天室。</span><span class="sxs-lookup"><span data-stu-id="775fe-122">For example, a chat room.</span></span>
* <span data-ttu-id="775fe-123">允许将消息发送到特定的客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="775fe-123">Enables sending messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="775fe-124">是在开放源代码[GitHub](https://github.com/aspnet/signalr)。</span><span class="sxs-lookup"><span data-stu-id="775fe-124">Is open-sourced at [GitHub](https://github.com/aspnet/signalr).</span></span>
* <span data-ttu-id="775fe-125">可缩放。</span><span class="sxs-lookup"><span data-stu-id="775fe-125">Scalable.</span></span>

<span data-ttu-id="775fe-126">客户端和服务器之间的连接是持久性的与 HTTP 连接不同的。</span><span class="sxs-lookup"><span data-stu-id="775fe-126">The connection between the client and server is persistent, unlike an HTTP connection.</span></span>

## <a name="transports"></a><span data-ttu-id="775fe-127">传输</span><span class="sxs-lookup"><span data-stu-id="775fe-127">Transports</span></span>

<span data-ttu-id="775fe-128">SignalR 通过多种方法用于构建实时 web 应用程序的摘要。</span><span class="sxs-lookup"><span data-stu-id="775fe-128">SignalR abstracts over a number of techniques for building real-time web applications.</span></span> <span data-ttu-id="775fe-129">[Websocket](https://tools.ietf.org/html/rfc7118)是最佳的传输，但这些不可用时，可以使用其他技术，例如服务器发送事件和长轮询。</span><span class="sxs-lookup"><span data-stu-id="775fe-129">[WebSockets](https://tools.ietf.org/html/rfc7118) is the optimal transport, but other techniques like Server-Sent Events and Long Polling can be used when those aren't available.</span></span> <span data-ttu-id="775fe-130">SignalR 将自动检测并初始化适当的传输基于在服务器和客户端上受支持的功能。</span><span class="sxs-lookup"><span data-stu-id="775fe-130">SignalR will automatically detect and initialize the appropriate transport based on features supported on the server and client.</span></span>

## <a name="hubs"></a><span data-ttu-id="775fe-131">中心</span><span class="sxs-lookup"><span data-stu-id="775fe-131">Hubs</span></span>

<span data-ttu-id="775fe-132">SignalR 使用中心客户端和服务器之间进行通信。</span><span class="sxs-lookup"><span data-stu-id="775fe-132">SignalR uses hubs to communicate between clients and servers.</span></span>

<span data-ttu-id="775fe-133">中心是一个高级的管道，用于允许在客户端和服务器相互调用的方法。</span><span class="sxs-lookup"><span data-stu-id="775fe-133">A hub is a high-level pipeline that allows your client and server to call methods on each other.</span></span> <span data-ttu-id="775fe-134">SignalR 处理调度跨计算机界限自动，允许客户端在服务器上调用方法，以轻松地为本地方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="775fe-134">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="775fe-135">中心允许将强类型化参数传递给方法，这样将启用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="775fe-135">Hubs allow passing strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="775fe-136">SignalR 提供了两个内置中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。</span><span class="sxs-lookup"><span data-stu-id="775fe-136">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="775fe-137">MessagePack 通常创建与使用 JSON 相比较小的消息。</span><span class="sxs-lookup"><span data-stu-id="775fe-137">MessagePack generally creates smaller messages than when using JSON.</span></span> <span data-ttu-id="775fe-138">旧版浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)提供 MessagePack 协议支持。</span><span class="sxs-lookup"><span data-stu-id="775fe-138">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="775fe-139">中心调用通过使用活动传输发送消息的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="775fe-139">Hubs call client-side code by sending messages using the active transport.</span></span> <span data-ttu-id="775fe-140">消息包含名称和客户端的方法的参数。</span><span class="sxs-lookup"><span data-stu-id="775fe-140">The messages contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="775fe-141">作为方法参数发送对象是使用配置的协议反序列化。</span><span class="sxs-lookup"><span data-stu-id="775fe-141">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="775fe-142">客户端尝试与客户端代码中的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="775fe-142">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="775fe-143">当找到匹配项时，使用反序列化的参数数据运行的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="775fe-143">When a match happens, the client method runs using the deserialized parameter data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="775fe-144">其他资源</span><span class="sxs-lookup"><span data-stu-id="775fe-144">Additional resources</span></span>

* [<span data-ttu-id="775fe-145">开始使用 SignalR 为 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="775fe-145">Get started with SignalR for ASP.NET Core</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="775fe-146">支持的平台</span><span class="sxs-lookup"><span data-stu-id="775fe-146">Supported Platforms</span></span>](xref:signalr/supported-platforms)
* [<span data-ttu-id="775fe-147">中心</span><span class="sxs-lookup"><span data-stu-id="775fe-147">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="775fe-148">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="775fe-148">JavaScript client</span></span>](xref:signalr/javascript-client)
