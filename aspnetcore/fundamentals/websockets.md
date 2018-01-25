---
title: "WebSockets 支持，在 ASP.NET 核心"
author: tdykstra
description: "了解如何开始使用 ASP.NET Core 中的 Websocket。"
ms.author: tdykstra
manager: wpickett
ms.date: 03/25/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: fundamentals/websockets
ms.openlocfilehash: 6f335376c72cd0c68f4667cf0e661a25bf448980
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-websockets-in-aspnet-core"></a><span data-ttu-id="66d2b-103">在 ASP.NET Core Websocket 简介</span><span class="sxs-lookup"><span data-stu-id="66d2b-103">Introduction to WebSockets in ASP.NET Core</span></span>

<span data-ttu-id="66d2b-104">通过[Tom Dykstra](https://github.com/tdykstra)和[Andrew Stanton 护士](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="66d2b-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="66d2b-105">此文章介绍了如何开始使用 ASP.NET Core 中的 Websocket。</span><span class="sxs-lookup"><span data-stu-id="66d2b-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="66d2b-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) 是一个协议，支持通过 TCP 连接建立持久的双向信道。</span><span class="sxs-lookup"><span data-stu-id="66d2b-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="66d2b-107">用于如聊天、 股票代码、 游戏的应用程序，你希望在 web 应用程序中的实时功能的任何位置。</span><span class="sxs-lookup"><span data-stu-id="66d2b-107">It's used for applications such as chat, stock tickers, games, anywhere you want real-time functionality in a web application.</span></span>

<span data-ttu-id="66d2b-108">[查看或下载的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)([如何下载](xref:tutorials/index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="66d2b-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="66d2b-109">请参阅[后续步骤](#next-steps)部分以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="66d2b-109">See the [Next Steps](#next-steps) section for more information.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="66d2b-110">系统必备</span><span class="sxs-lookup"><span data-stu-id="66d2b-110">Prerequisites</span></span>

* <span data-ttu-id="66d2b-111">ASP.NET 核心 1.1 （无法在 1.0 运行）</span><span class="sxs-lookup"><span data-stu-id="66d2b-111">ASP.NET Core 1.1 (doesn't run on 1.0)</span></span>
* <span data-ttu-id="66d2b-112">任何 ASP.NET Core 运行的操作系统：</span><span class="sxs-lookup"><span data-stu-id="66d2b-112">Any OS that ASP.NET Core runs on:</span></span>
  
  * <span data-ttu-id="66d2b-113">Windows 7 / Windows Server 2008 及更高版本</span><span class="sxs-lookup"><span data-stu-id="66d2b-113">Windows 7 / Windows Server 2008 and later</span></span>
  * <span data-ttu-id="66d2b-114">Linux</span><span class="sxs-lookup"><span data-stu-id="66d2b-114">Linux</span></span>
  * <span data-ttu-id="66d2b-115">macOS</span><span class="sxs-lookup"><span data-stu-id="66d2b-115">macOS</span></span>

* <span data-ttu-id="66d2b-116">**异常**： 如果在 IIS 中，使用的 Windows 上运行你的应用程序或使用 WebListener，必须使用：</span><span class="sxs-lookup"><span data-stu-id="66d2b-116">**Exception**: If your app runs on Windows with IIS, or with WebListener, you must use:</span></span>

  * <span data-ttu-id="66d2b-117">Windows 8 / Windows Server 2012 或更高版本</span><span class="sxs-lookup"><span data-stu-id="66d2b-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="66d2b-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="66d2b-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="66d2b-119">必须在 IIS 中启用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="66d2b-119">WebSocket must be enabled in IIS</span></span>

* <span data-ttu-id="66d2b-120">有关支持的浏览器，请参阅 http://caniuse.com/#feat=websockets。</span><span class="sxs-lookup"><span data-stu-id="66d2b-120">For supported browsers, see http://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-it"></a><span data-ttu-id="66d2b-121">何时使用</span><span class="sxs-lookup"><span data-stu-id="66d2b-121">When to use it</span></span>

<span data-ttu-id="66d2b-122">当你需要直接使用的套接字连接时，请使用 Websocket。</span><span class="sxs-lookup"><span data-stu-id="66d2b-122">Use WebSockets when you need to work directly with a socket connection.</span></span> <span data-ttu-id="66d2b-123">例如，你可能要进行实时的游戏需要最佳性能。</span><span class="sxs-lookup"><span data-stu-id="66d2b-123">For example, you might need the best possible performance for a real-time game.</span></span>

<span data-ttu-id="66d2b-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr)提供更丰富的实时功能，但它的应用程序模型仅在 ASP.NET 中，不带 ASP.NET Core 上运行。</span><span class="sxs-lookup"><span data-stu-id="66d2b-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) provides a richer application model for real-time functionality, but it runs only on ASP.NET, not ASP.NET Core.</span></span> <span data-ttu-id="66d2b-125">SignalR Core 版本正处于开发;要了解其进度，请参阅[SignalR Core 的 GitHub 存储库](https://github.com/aspnet/SignalR)。</span><span class="sxs-lookup"><span data-stu-id="66d2b-125">A Core version of SignalR is under development; to follow its progress, see the [GitHub repository for SignalR Core](https://github.com/aspnet/SignalR).</span></span>

<span data-ttu-id="66d2b-126">如果你不想等待 SignalR Core，你现在可以使用 Websocket 直接。</span><span class="sxs-lookup"><span data-stu-id="66d2b-126">If you don't want to wait for SignalR Core, you can use WebSockets directly now.</span></span> <span data-ttu-id="66d2b-127">但是，你可能需要开发功能，它们提供将 SignalR，如：</span><span class="sxs-lookup"><span data-stu-id="66d2b-127">But you might have to develop features that SignalR would provide, such as:</span></span>

* <span data-ttu-id="66d2b-128">支持广泛的浏览器版本，通过使用自动回退到备用的传输方法。</span><span class="sxs-lookup"><span data-stu-id="66d2b-128">Support for a broader range of browser versions by using automatic fallback to alternative transport methods.</span></span>
* <span data-ttu-id="66d2b-129">当连接将自动重新连接。</span><span class="sxs-lookup"><span data-stu-id="66d2b-129">Automatic reconnection when a connection drops.</span></span>
* <span data-ttu-id="66d2b-130">支持的客户端调用方法的服务器上，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="66d2b-130">Support for clients calling methods on the server or vice versa.</span></span>
* <span data-ttu-id="66d2b-131">缩放到多个服务器的支持。</span><span class="sxs-lookup"><span data-stu-id="66d2b-131">Support for scaling to multiple servers.</span></span>

## <a name="how-to-use-it"></a><span data-ttu-id="66d2b-132">使用方法</span><span class="sxs-lookup"><span data-stu-id="66d2b-132">How to use it</span></span>

* <span data-ttu-id="66d2b-133">安装[Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/)包。</span><span class="sxs-lookup"><span data-stu-id="66d2b-133">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="66d2b-134">配置该中间件。</span><span class="sxs-lookup"><span data-stu-id="66d2b-134">Configure the middleware.</span></span>
* <span data-ttu-id="66d2b-135">接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="66d2b-135">Accept WebSocket requests.</span></span>
* <span data-ttu-id="66d2b-136">发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="66d2b-136">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="66d2b-137">配置该中间件</span><span class="sxs-lookup"><span data-stu-id="66d2b-137">Configure the middleware</span></span>

<span data-ttu-id="66d2b-138">添加中的 Websocket 中间件`Configure`方法`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="66d2b-138">Add the WebSockets middleware in the `Configure` method of the `Startup` class.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="66d2b-139">可以配置下列设置：</span><span class="sxs-lookup"><span data-stu-id="66d2b-139">The following settings can be configured:</span></span>

* <span data-ttu-id="66d2b-140">`KeepAliveInterval`-如何频繁地发送到客户端，以确保代理使连接保持打开的"ping"帧。</span><span class="sxs-lookup"><span data-stu-id="66d2b-140">`KeepAliveInterval` - How frequently to send "ping" frames to the client, to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="66d2b-141">`ReceiveBufferSize`的用于接收数据的缓冲区大小。</span><span class="sxs-lookup"><span data-stu-id="66d2b-141">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="66d2b-142">只有高级的用户将需要更改此设置，以进行性能优化基于其数据的大小。</span><span class="sxs-lookup"><span data-stu-id="66d2b-142">Only advanced users would need to change this, for performance tuning based on the size of their data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="66d2b-143">接受 WebSocket 请求</span><span class="sxs-lookup"><span data-stu-id="66d2b-143">Accept WebSocket requests</span></span>

<span data-ttu-id="66d2b-144">请求生命周期中某个位置更高版本 (后面`Configure`方法或 MVC 操作，例如中) 检查它是否是 WebSocket 请求并接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="66d2b-144">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="66d2b-145">此示例摘自更高版本在`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="66d2b-145">This example is from later in the `Configure` method.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="66d2b-146">上任何 URL，也可以来自 WebSocket 请求，但此代码示例仅接受请求`/ws`。</span><span class="sxs-lookup"><span data-stu-id="66d2b-146">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="66d2b-147">发送和接收消息</span><span class="sxs-lookup"><span data-stu-id="66d2b-147">Send and receive messages</span></span>

<span data-ttu-id="66d2b-148">`AcceptWebSocketAsync`方法升级 TCP 连接到 WebSocket 连接并为你提供[WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket)对象。</span><span class="sxs-lookup"><span data-stu-id="66d2b-148">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and gives you a [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="66d2b-149">使用 WebSocket 对象发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="66d2b-149">Use the WebSocket object to send and receive messages.</span></span>

<span data-ttu-id="66d2b-150">接受的 WebSocket 请求前面所示的代码将传递`WebSocket`对象传递给`Echo`方法; 如果此处的`Echo`方法。</span><span class="sxs-lookup"><span data-stu-id="66d2b-150">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method; here's the `Echo` method.</span></span> <span data-ttu-id="66d2b-151">该代码将收到一条消息，并立即发送同一消息。</span><span class="sxs-lookup"><span data-stu-id="66d2b-151">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="66d2b-152">将一直留在循环执行该操作，直到客户端将关闭连接。</span><span class="sxs-lookup"><span data-stu-id="66d2b-152">It stays in a loop doing that until the client closes the connection.</span></span> 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="66d2b-153">当您在开始此循环之前接受 WebSocket 时，中间件管道结束。</span><span class="sxs-lookup"><span data-stu-id="66d2b-153">When you accept the WebSocket before beginning this loop, the middleware pipeline ends.</span></span>  <span data-ttu-id="66d2b-154">在关闭套接字后, 管道展开。</span><span class="sxs-lookup"><span data-stu-id="66d2b-154">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="66d2b-155">即，向前移动在管道中当接受 WebSocket，就像它在请求停止将命中 MVC 操作，例如时。</span><span class="sxs-lookup"><span data-stu-id="66d2b-155">That is, the request stops moving forward in the pipeline when you accept a WebSocket, just as it would when you hit an MVC action, for example.</span></span>  <span data-ttu-id="66d2b-156">但当你完成此循环，并关闭套接字，则继续备份管道处理请求。</span><span class="sxs-lookup"><span data-stu-id="66d2b-156">But when you finish this loop and close the socket, the request proceeds back up the pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d2b-157">后续步骤</span><span class="sxs-lookup"><span data-stu-id="66d2b-157">Next steps</span></span>

<span data-ttu-id="66d2b-158">[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)附带此文章是一个简单的回显应用程序。</span><span class="sxs-lookup"><span data-stu-id="66d2b-158">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is a simple echo application.</span></span> <span data-ttu-id="66d2b-159">它具有一个网页，建立 WebSocket 连接，以及服务器只重新发送回客户端收到任何消息。</span><span class="sxs-lookup"><span data-stu-id="66d2b-159">It has a web page that makes WebSocket connections, and the server just resends back to the client any messages it receives.</span></span> <span data-ttu-id="66d2b-160">（它具有将设置为从与 IIS Express 的 Visual Studio 运行） 在命令提示符下运行它，然后导航到 http://localhost:5000/。</span><span class="sxs-lookup"><span data-stu-id="66d2b-160">Run it from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="66d2b-161">网页显示在左上方的连接状态：</span><span class="sxs-lookup"><span data-stu-id="66d2b-161">The web page shows connection status at the upper left:</span></span>

![网页的初始状态](websockets/_static/start.png)

<span data-ttu-id="66d2b-163">选择**连接**向显示的 URL 中发送的 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="66d2b-163">Select **Connect** to send a WebSocket request to the URL shown.</span></span>  <span data-ttu-id="66d2b-164">输入测试消息，然后选择**发送**。</span><span class="sxs-lookup"><span data-stu-id="66d2b-164">Enter a test message and select **Send**.</span></span> <span data-ttu-id="66d2b-165">完成后，选择**关闭套接字**。</span><span class="sxs-lookup"><span data-stu-id="66d2b-165">When done, select **Close Socket**.</span></span> <span data-ttu-id="66d2b-166">**通信日志**部分报告每次打开时，发送，并为它的关闭操作。</span><span class="sxs-lookup"><span data-stu-id="66d2b-166">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![网页的初始状态](websockets/_static/end.png)
