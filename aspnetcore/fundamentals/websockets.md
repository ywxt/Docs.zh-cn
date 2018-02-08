---
title: "ASP.NET Core 中的 WebSocket 支持"
author: tdykstra
description: "了解如何在 ASP.NET Core 中开始使用 WebSocket。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/25/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/websockets
ms.openlocfilehash: 306eca28b9f1f66e1ccaf185ccae87db8dea1b01
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-websockets-in-aspnet-core"></a><span data-ttu-id="7c32f-103">ASP.NET Core 中 WebSocket 的介绍</span><span class="sxs-lookup"><span data-stu-id="7c32f-103">Introduction to WebSockets in ASP.NET Core</span></span>

<span data-ttu-id="7c32f-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Andrew Stanton-Nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="7c32f-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="7c32f-105">本文介绍 ASP.NET Core 中 WebSocket 的入门方法。</span><span class="sxs-lookup"><span data-stu-id="7c32f-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="7c32f-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) 是一个协议，支持通过 TCP 连接建立持久的双向信道。</span><span class="sxs-lookup"><span data-stu-id="7c32f-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="7c32f-107">它可用于聊天、股票报价和游戏等应用程序，以及 Web 应用程序中需要实时功能的任何情景。</span><span class="sxs-lookup"><span data-stu-id="7c32f-107">It's used for applications such as chat, stock tickers, games, anywhere you want real-time functionality in a web application.</span></span>

<span data-ttu-id="7c32f-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="7c32f-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="7c32f-109">有关详细信息，请参阅[后续步骤](#next-steps)。</span><span class="sxs-lookup"><span data-stu-id="7c32f-109">See the [Next Steps](#next-steps) section for more information.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7c32f-110">系统必备</span><span class="sxs-lookup"><span data-stu-id="7c32f-110">Prerequisites</span></span>

* <span data-ttu-id="7c32f-111">ASP.NET Core 1.1（无法在 1.0 上运行）</span><span class="sxs-lookup"><span data-stu-id="7c32f-111">ASP.NET Core 1.1 (doesn't run on 1.0)</span></span>
* <span data-ttu-id="7c32f-112">ASP.NET Core 运行的任何操作系统：</span><span class="sxs-lookup"><span data-stu-id="7c32f-112">Any OS that ASP.NET Core runs on:</span></span>
  
  * <span data-ttu-id="7c32f-113">Windows 7 / Windows Server 2008 及更高版本</span><span class="sxs-lookup"><span data-stu-id="7c32f-113">Windows 7 / Windows Server 2008 and later</span></span>
  * <span data-ttu-id="7c32f-114">Linux</span><span class="sxs-lookup"><span data-stu-id="7c32f-114">Linux</span></span>
  * <span data-ttu-id="7c32f-115">macOS</span><span class="sxs-lookup"><span data-stu-id="7c32f-115">macOS</span></span>

* <span data-ttu-id="7c32f-116">**例外**：如果在带有 IIS 或 WebListener 的 Windows 上运行应用，必须使用：</span><span class="sxs-lookup"><span data-stu-id="7c32f-116">**Exception**: If your app runs on Windows with IIS, or with WebListener, you must use:</span></span>

  * <span data-ttu-id="7c32f-117">Windows 8 / Windows Server 2012 及更高版本</span><span class="sxs-lookup"><span data-stu-id="7c32f-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="7c32f-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="7c32f-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="7c32f-119">必须在 IIS 中启用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="7c32f-119">WebSocket must be enabled in IIS</span></span>

* <span data-ttu-id="7c32f-120">有关受支持的浏览器，请参阅 http://caniuse.com/#feat=websockets。</span><span class="sxs-lookup"><span data-stu-id="7c32f-120">For supported browsers, see http://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-it"></a><span data-ttu-id="7c32f-121">何时使用</span><span class="sxs-lookup"><span data-stu-id="7c32f-121">When to use it</span></span>

<span data-ttu-id="7c32f-122">需要直接使用套接字连接时，请使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="7c32f-122">Use WebSockets when you need to work directly with a socket connection.</span></span> <span data-ttu-id="7c32f-123">例如，实时游戏可能需要最佳性能。</span><span class="sxs-lookup"><span data-stu-id="7c32f-123">For example, you might need the best possible performance for a real-time game.</span></span>

<span data-ttu-id="7c32f-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) 为实时功能提供了更丰富的应用程序模型，但它仅在 ASP.NET 上运行，不能在 ASP.NET Core 上运行。</span><span class="sxs-lookup"><span data-stu-id="7c32f-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) provides a richer application model for real-time functionality, but it runs only on ASP.NET, not ASP.NET Core.</span></span> <span data-ttu-id="7c32f-125">SignalR 的 Core 版本正在开发中；若要了解其进度，请参阅 [适用于 SignalR Core 的 GitHub 存储库](https://github.com/aspnet/SignalR)。</span><span class="sxs-lookup"><span data-stu-id="7c32f-125">A Core version of SignalR is under development; to follow its progress, see the [GitHub repository for SignalR Core](https://github.com/aspnet/SignalR).</span></span>

<span data-ttu-id="7c32f-126">如果不想等待 SignalR Core，现在可直接使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="7c32f-126">If you don't want to wait for SignalR Core, you can use WebSockets directly now.</span></span> <span data-ttu-id="7c32f-127">但是可能必须开发 SignalR 提供的功能，例如：</span><span class="sxs-lookup"><span data-stu-id="7c32f-127">But you might have to develop features that SignalR would provide, such as:</span></span>

* <span data-ttu-id="7c32f-128">通过自动回退到替代传输方法来支持更广泛的浏览器版本。</span><span class="sxs-lookup"><span data-stu-id="7c32f-128">Support for a broader range of browser versions by using automatic fallback to alternative transport methods.</span></span>
* <span data-ttu-id="7c32f-129">连接断开时自动重新连接。</span><span class="sxs-lookup"><span data-stu-id="7c32f-129">Automatic reconnection when a connection drops.</span></span>
* <span data-ttu-id="7c32f-130">支持服务器上的客户端调用方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="7c32f-130">Support for clients calling methods on the server or vice versa.</span></span>
* <span data-ttu-id="7c32f-131">支持缩放到多个服务器。</span><span class="sxs-lookup"><span data-stu-id="7c32f-131">Support for scaling to multiple servers.</span></span>

## <a name="how-to-use-it"></a><span data-ttu-id="7c32f-132">使用方法</span><span class="sxs-lookup"><span data-stu-id="7c32f-132">How to use it</span></span>

* <span data-ttu-id="7c32f-133">安装 [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 包。</span><span class="sxs-lookup"><span data-stu-id="7c32f-133">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="7c32f-134">配置中间件。</span><span class="sxs-lookup"><span data-stu-id="7c32f-134">Configure the middleware.</span></span>
* <span data-ttu-id="7c32f-135">接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="7c32f-135">Accept WebSocket requests.</span></span>
* <span data-ttu-id="7c32f-136">发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="7c32f-136">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="7c32f-137">配置中间件</span><span class="sxs-lookup"><span data-stu-id="7c32f-137">Configure the middleware</span></span>

<span data-ttu-id="7c32f-138">在 `Startup` 类的 `Configure` 方法中添加 WebSocket 中间件。</span><span class="sxs-lookup"><span data-stu-id="7c32f-138">Add the WebSockets middleware in the `Configure` method of the `Startup` class.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="7c32f-139">可配置以下设置：</span><span class="sxs-lookup"><span data-stu-id="7c32f-139">The following settings can be configured:</span></span>

* <span data-ttu-id="7c32f-140">`KeepAliveInterval` - 向客户端发送“ping”帧的频率，以确保代理保持连接处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="7c32f-140">`KeepAliveInterval` - How frequently to send "ping" frames to the client, to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="7c32f-141">`ReceiveBufferSize` - 用于接收数据的缓冲区的大小。</span><span class="sxs-lookup"><span data-stu-id="7c32f-141">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="7c32f-142">只有高级用户才需要对其进行更改，以便根据数据大小调整性能。</span><span class="sxs-lookup"><span data-stu-id="7c32f-142">Only advanced users would need to change this, for performance tuning based on the size of their data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="7c32f-143">接受 WebSocket 请求</span><span class="sxs-lookup"><span data-stu-id="7c32f-143">Accept WebSocket requests</span></span>

<span data-ttu-id="7c32f-144">在请求生命周期后期（例如在 `Configure` 方法或 MVC 操作的后期），检查它是否是 WebSocket 请求并接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="7c32f-144">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="7c32f-145">该示例来自 `Configure` 方法的后期。</span><span class="sxs-lookup"><span data-stu-id="7c32f-145">This example is from later in the `Configure` method.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="7c32f-146">WebSocket 请求可以来自任何 URL，但此示例代码只接受 `/ws` 的请求。</span><span class="sxs-lookup"><span data-stu-id="7c32f-146">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="7c32f-147">发送和接收消息</span><span class="sxs-lookup"><span data-stu-id="7c32f-147">Send and receive messages</span></span>

<span data-ttu-id="7c32f-148">`AcceptWebSocketAsync` 方法将 TCP 连接升级到 WebSocket 连接，并提供 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 对象。</span><span class="sxs-lookup"><span data-stu-id="7c32f-148">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and gives you a [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="7c32f-149">使用 WebSocket 对象发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="7c32f-149">Use the WebSocket object to send and receive messages.</span></span>

<span data-ttu-id="7c32f-150">之前显示的接受 WebSocket 请求的代码将 `WebSocket` 对象传递给 `Echo` 方法；此处为 `Echo` 方法。</span><span class="sxs-lookup"><span data-stu-id="7c32f-150">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method; here's the `Echo` method.</span></span> <span data-ttu-id="7c32f-151">代码接收消息并立即发回相同的消息。</span><span class="sxs-lookup"><span data-stu-id="7c32f-151">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="7c32f-152">一直在循环中执行此操作，直到客户端关闭连接。</span><span class="sxs-lookup"><span data-stu-id="7c32f-152">It stays in a loop doing that until the client closes the connection.</span></span> 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="7c32f-153">如果在开始此循环之前接受 WebSocket，中间件管道会结束。</span><span class="sxs-lookup"><span data-stu-id="7c32f-153">When you accept the WebSocket before beginning this loop, the middleware pipeline ends.</span></span>  <span data-ttu-id="7c32f-154">关闭套接字后，管道展开。</span><span class="sxs-lookup"><span data-stu-id="7c32f-154">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="7c32f-155">也就是说，如果接受 WebSocket ，请求会在管道中停止前进，就像点击 MVC 操作一样。</span><span class="sxs-lookup"><span data-stu-id="7c32f-155">That is, the request stops moving forward in the pipeline when you accept a WebSocket, just as it would when you hit an MVC action, for example.</span></span>  <span data-ttu-id="7c32f-156">但是完成此循环并关闭套接字时，请求将在管道中后退。</span><span class="sxs-lookup"><span data-stu-id="7c32f-156">But when you finish this loop and close the socket, the request proceeds back up the pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c32f-157">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7c32f-157">Next steps</span></span>

<span data-ttu-id="7c32f-158">本文附带的[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)是一个简单的回显应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c32f-158">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is a simple echo application.</span></span> <span data-ttu-id="7c32f-159">它有一个可建立 WebSocket 连接的网页，且服务器仅将其收到的消息重新发回到客户端。</span><span class="sxs-lookup"><span data-stu-id="7c32f-159">It has a web page that makes WebSocket connections, and the server just resends back to the client any messages it receives.</span></span> <span data-ttu-id="7c32f-160">从命令提示符运行它（它未设置为从具有 IIS Express 的 Visual Studio 运行）并导航到 http://localhost:5000。</span><span class="sxs-lookup"><span data-stu-id="7c32f-160">Run it from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="7c32f-161">该网页的左上方显示连接状态：</span><span class="sxs-lookup"><span data-stu-id="7c32f-161">The web page shows connection status at the upper left:</span></span>

![网页的初始状态](websockets/_static/start.png)

<span data-ttu-id="7c32f-163">选择“连接”，向显示的 URL 发送 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="7c32f-163">Select **Connect** to send a WebSocket request to the URL shown.</span></span>  <span data-ttu-id="7c32f-164">输入测试消息并选择“发送”。</span><span class="sxs-lookup"><span data-stu-id="7c32f-164">Enter a test message and select **Send**.</span></span> <span data-ttu-id="7c32f-165">完成后，请选择“关闭套接字”。</span><span class="sxs-lookup"><span data-stu-id="7c32f-165">When done, select **Close Socket**.</span></span> <span data-ttu-id="7c32f-166">“通信日志”部分会报告每一个发生的“打开”、“发送”和“关闭”操作。</span><span class="sxs-lookup"><span data-stu-id="7c32f-166">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![网页的初始状态](websockets/_static/end.png)
