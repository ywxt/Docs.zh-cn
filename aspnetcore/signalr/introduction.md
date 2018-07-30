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
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="15b87-103">ASP.NET Core SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="15b87-103">Introduction to ASP.NET Core SignalR</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="15b87-104">SignalR 是什么？</span><span class="sxs-lookup"><span data-stu-id="15b87-104">What is SignalR?</span></span>

<span data-ttu-id="15b87-105">ASP.NET Core SignalR 是一个开放源代码库，它简化了向应用添加实时 web 功能。</span><span class="sxs-lookup"><span data-stu-id="15b87-105">ASP.NET Core SignalR is an open-source library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="15b87-106">实时 web 功能立即使服务器端代码能够将内容推送到客户端。</span><span class="sxs-lookup"><span data-stu-id="15b87-106">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="15b87-107">SignalR 的良好候选项：</span><span class="sxs-lookup"><span data-stu-id="15b87-107">Good candidates for SignalR:</span></span>

* <span data-ttu-id="15b87-108">需要来自服务器的高频率更新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="15b87-108">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="15b87-109">示例包括游戏、 社交网络、 投票、 拍卖、 映射和 GPS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="15b87-109">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="15b87-110">仪表板和监视应用程序。</span><span class="sxs-lookup"><span data-stu-id="15b87-110">Dashboards and monitoring apps.</span></span> <span data-ttu-id="15b87-111">示例包括公司的仪表板，即时销售更新或旅行警报。</span><span class="sxs-lookup"><span data-stu-id="15b87-111">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="15b87-112">协作应用程序。</span><span class="sxs-lookup"><span data-stu-id="15b87-112">Collaborative apps.</span></span> <span data-ttu-id="15b87-113">白板应用和团队会议软件是协作应用程序的示例。</span><span class="sxs-lookup"><span data-stu-id="15b87-113">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="15b87-114">需要通知的应用程序。</span><span class="sxs-lookup"><span data-stu-id="15b87-114">Apps that require notifications.</span></span> <span data-ttu-id="15b87-115">社交网络、 电子邮件、 聊天、 游戏、 行程警报和许多其他应用程序使用通知。</span><span class="sxs-lookup"><span data-stu-id="15b87-115">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="15b87-116">SignalR 提供了一个 API，用于创建服务器到客户端[远程过程调用 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。</span><span class="sxs-lookup"><span data-stu-id="15b87-116">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="15b87-117">Rpc 在客户端上从服务器端.NET Core 代码中调用 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="15b87-117">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="15b87-118">下面是适用于 ASP.NET Core SignalR 的一些功能：</span><span class="sxs-lookup"><span data-stu-id="15b87-118">Here are some features of SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="15b87-119">会自动处理的连接管理。</span><span class="sxs-lookup"><span data-stu-id="15b87-119">Handles connection management automatically.</span></span>
* <span data-ttu-id="15b87-120">同时将消息发送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="15b87-120">Sends messages to all connected clients simultaneously.</span></span> <span data-ttu-id="15b87-121">例如，聊天室。</span><span class="sxs-lookup"><span data-stu-id="15b87-121">For example, a chat room.</span></span>
* <span data-ttu-id="15b87-122">将消息发送到特定的客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="15b87-122">Sends messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="15b87-123">扩展以处理增加的流量。</span><span class="sxs-lookup"><span data-stu-id="15b87-123">Scales to handle increasing traffic.</span></span>

<span data-ttu-id="15b87-124">源托管在[SignalR GitHub 上的存储库](https://github.com/aspnet/signalr)。</span><span class="sxs-lookup"><span data-stu-id="15b87-124">The source is hosted in a [SignalR repository on GitHub](https://github.com/aspnet/signalr).</span></span>

## <a name="transports"></a><span data-ttu-id="15b87-125">传输</span><span class="sxs-lookup"><span data-stu-id="15b87-125">Transports</span></span>

<span data-ttu-id="15b87-126">SignalR 支持几种方法用于处理实时通信：</span><span class="sxs-lookup"><span data-stu-id="15b87-126">SignalR supports several techniques for handling real-time communications:</span></span>

* [<span data-ttu-id="15b87-127">WebSockets</span><span class="sxs-lookup"><span data-stu-id="15b87-127">WebSockets</span></span>](https://tools.ietf.org/html/rfc7118)
* <span data-ttu-id="15b87-128">服务器发送事件</span><span class="sxs-lookup"><span data-stu-id="15b87-128">Server-Sent Events</span></span>
* <span data-ttu-id="15b87-129">很长的轮询</span><span class="sxs-lookup"><span data-stu-id="15b87-129">Long Polling</span></span>

<span data-ttu-id="15b87-130">SignalR 会自动选择最佳传输方法内的服务器和客户端的功能。</span><span class="sxs-lookup"><span data-stu-id="15b87-130">SignalR automatically chooses the best transport method that is within the capabilities of the server and client.</span></span>

## <a name="hubs"></a><span data-ttu-id="15b87-131">中心</span><span class="sxs-lookup"><span data-stu-id="15b87-131">Hubs</span></span>

<span data-ttu-id="15b87-132">使用 SignalR*中心*客户端和服务器之间进行通信。</span><span class="sxs-lookup"><span data-stu-id="15b87-132">SignalR uses *hubs* to communicate between clients and servers.</span></span>

<span data-ttu-id="15b87-133">中心是一个高级的管道，用于允许客户端和服务器相互调用的方法。</span><span class="sxs-lookup"><span data-stu-id="15b87-133">A hub is a high-level pipeline that allows a client and server to call methods on each other.</span></span> <span data-ttu-id="15b87-134">SignalR 处理调度跨计算机界限自动，允许客户端调用的方法在服务器上，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="15b87-134">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server and vice versa.</span></span> <span data-ttu-id="15b87-135">您可以强类型化参数传递到方法，这样将启用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="15b87-135">You can pass strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="15b87-136">SignalR 提供了两个内置中心协议： 文本协议基于 JSON 和基于二进制协议[MessagePack](https://msgpack.org/)。</span><span class="sxs-lookup"><span data-stu-id="15b87-136">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="15b87-137">MessagePack 通常会产生较小的消息为 JSON 进行比较。</span><span class="sxs-lookup"><span data-stu-id="15b87-137">MessagePack generally creates smaller messages compared to JSON.</span></span> <span data-ttu-id="15b87-138">旧版浏览器必须支持[XHR 级别 2](https://caniuse.com/#feat=xhr2)提供 MessagePack 协议支持。</span><span class="sxs-lookup"><span data-stu-id="15b87-138">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="15b87-139">中心通过发送消息，其中包含名称和客户端的方法的参数调用客户端代码。</span><span class="sxs-lookup"><span data-stu-id="15b87-139">Hubs call client-side code by sending messages that contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="15b87-140">作为方法参数发送对象是使用配置的协议反序列化。</span><span class="sxs-lookup"><span data-stu-id="15b87-140">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="15b87-141">客户端尝试与客户端代码中的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="15b87-141">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="15b87-142">当客户端找到了匹配项时，它调用方法，并将反序列化的参数数据传递给它。</span><span class="sxs-lookup"><span data-stu-id="15b87-142">When the client finds a match, it calls the method and passes to it the deserialized parameter data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15b87-143">其他资源</span><span class="sxs-lookup"><span data-stu-id="15b87-143">Additional resources</span></span>

* [<span data-ttu-id="15b87-144">开始使用 SignalR 为 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="15b87-144">Get started with SignalR for ASP.NET Core</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="15b87-145">支持的平台</span><span class="sxs-lookup"><span data-stu-id="15b87-145">Supported Platforms</span></span>](xref:signalr/supported-platforms)
* [<span data-ttu-id="15b87-146">中心</span><span class="sxs-lookup"><span data-stu-id="15b87-146">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="15b87-147">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="15b87-147">JavaScript client</span></span>](xref:signalr/javascript-client)
