---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 简介 |Microsoft Docs
author: pfletcher
description: 本文介绍了 SignalR 是什么，以及一些了要创建的解决方案。
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 2f4353e88287f0716967362e255d94df0c522475
ms.sourcegitcommit: 260abb706ed17f07a53288d8a0c3e69fc13e7468
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38966739"
---
<a name="introduction-to-signalr"></a><span data-ttu-id="a45fb-103">SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="a45fb-103">Introduction to SignalR</span></span>
====================

<span data-ttu-id="a45fb-104">本教程中的更新的版本是可用[此处](/aspnet/core/tutorials/signalr)使用 Visual Studio 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="a45fb-104">An updated version of this tutorial is available [here](/aspnet/core/tutorials/signalr) using the latest version of Visual Studio.</span></span> <span data-ttu-id="a45fb-105">新教程使用[ASP.NET Core](/aspnet/core/)，通过本教程提供许多改进。</span><span class="sxs-lookup"><span data-stu-id="a45fb-105">The new tutorial uses [ASP.NET Core](/aspnet/core/), which provides many improvements over this tutorial.</span></span>

<span data-ttu-id="a45fb-106">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a45fb-106">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="a45fb-107">本文介绍了 SignalR 是什么，以及一些了要创建的解决方案。</span><span class="sxs-lookup"><span data-stu-id="a45fb-107">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="a45fb-108">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="a45fb-108">Questions and comments</span></span>
> 
> <span data-ttu-id="a45fb-109">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="a45fb-109">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a45fb-110">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-110">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>


## <a name="what-is-signalr"></a><span data-ttu-id="a45fb-111">SignalR 是什么？</span><span class="sxs-lookup"><span data-stu-id="a45fb-111">What is SignalR?</span></span>

<span data-ttu-id="a45fb-112">ASP.NET SignalR 是一个面向 ASP.NET 开发人员的库，可简化将实时 web 功能添加到应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="a45fb-112">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="a45fb-113">实时 web 功能是让服务器代码将内容推送到连接的客户端立即可用，而不是让服务器等待客户端请求新数据的能力。</span><span class="sxs-lookup"><span data-stu-id="a45fb-113">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="a45fb-114">SignalR 可用于将任何类型的"实时"web 功能添加到 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a45fb-114">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="a45fb-115">尽管聊天通常用作示例，您可以更为很多。</span><span class="sxs-lookup"><span data-stu-id="a45fb-115">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="a45fb-116">只要用户刷新 web 页面以查看新数据或页面实现[长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling)若要检索新数据，可以考虑对它使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="a45fb-116">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="a45fb-117">示例包括仪表板和监视应用程序，协作应用程序 （如同时进行编辑的文档） 时，作业的进度更新，并实时窗体。</span><span class="sxs-lookup"><span data-stu-id="a45fb-117">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="a45fb-118">SignalR 还能让全新类型的 web 应用程序需要高频率更新从服务器中，例如，实时游戏。</span><span class="sxs-lookup"><span data-stu-id="a45fb-118">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="a45fb-119">SignalR 提供一个简单的 API，用于创建从服务器端.NET 代码中调用 JavaScript 函数在客户端浏览器 （和其他客户端平台） 的服务器到客户端的远程过程调用 (RPC)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-119">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="a45fb-120">SignalR 还包括连接管理的 API （例如，连接和断开连接事件），并对连接进行分组。</span><span class="sxs-lookup"><span data-stu-id="a45fb-120">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![使用 signalr 实现调用方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="a45fb-122">SignalR 自动处理的连接管理，并允许您将消息广播到所有连接的客户端同时，如聊天室。</span><span class="sxs-lookup"><span data-stu-id="a45fb-122">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="a45fb-123">您还可以将消息发送到特定的客户端。</span><span class="sxs-lookup"><span data-stu-id="a45fb-123">You can also send messages to specific clients.</span></span> <span data-ttu-id="a45fb-124">客户端和服务器之间的连接是持久性的与不同的是经典的 HTTP 连接，这是重新建立的每个通信。</span><span class="sxs-lookup"><span data-stu-id="a45fb-124">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="a45fb-125">SignalR 支持"服务器推送"功能，在其中服务器代码可以调用远程过程调用 (RPC)，而不是常见请求-响应模式目前上使用 web 浏览器中的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="a45fb-125">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="a45fb-126">SignalR 应用程序可以横向扩展到数千个客户端使用服务总线、 SQL Server 或[Redis](http://redis.io)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-126">SignalR applications can scale out to thousands of clients using Service Bus, SQL Server or [Redis](http://redis.io).</span></span>

<span data-ttu-id="a45fb-127">SignalR 是开放源代码，可通过访问[GitHub](https://github.com/signalr)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-127">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="a45fb-128">SignalR 和 WebSocket</span><span class="sxs-lookup"><span data-stu-id="a45fb-128">SignalR and WebSocket</span></span>

<span data-ttu-id="a45fb-129">SignalR 使用新的 WebSocket 传输 （如果有），并在必要时回退到较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-129">SignalR uses the new WebSocket transport where available, and falls back to older transports where necessary.</span></span> <span data-ttu-id="a45fb-130">尽管您当然可以编写直接使用 WebSocket，并使用 SignalR 意味着已将大量的额外功能，您需要实现应用程序已为您完成。</span><span class="sxs-lookup"><span data-stu-id="a45fb-130">While you could certainly write your application using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement will already have been done for you.</span></span> <span data-ttu-id="a45fb-131">最重要的是，这意味着您可以编写代码才能使用 WebSocket，而无需担心如何创建单独的代码路径的较旧的客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="a45fb-131">Most importantly, this means that you can code your application to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="a45fb-132">SignalR 还使你免受无需担心对 WebSocket，更新，因为 SignalR 将继续更新，以支持基础传输中的更改的 WebSocket 版本间提供你的应用程序一致的接口。</span><span class="sxs-lookup"><span data-stu-id="a45fb-132">SignalR also shields you from having to worry about updates to WebSocket, since SignalR will continue to be updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<span data-ttu-id="a45fb-133">尽管肯定无法创建使用单独的 WebSocket 的解决方案，SignalR 提供了所有需要自己编写，如回退到其他传输和修订的更新到 WebSocket 实现应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="a45fb-133">While you could certainly create a solution using WebSocket alone, SignalR provides all of the functionality you would need to write yourself, such as fallback to other transports and revising your application for updates to WebSocket implementations.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="a45fb-134">传输和回退</span><span class="sxs-lookup"><span data-stu-id="a45fb-134">Transports and fallbacks</span></span>

<span data-ttu-id="a45fb-135">SignalR 是一种抽象，通过某些要求进行客户端和服务器之间的实时工作的传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-135">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="a45fb-136">SignalR 连接作为 HTTP，启动，然后升级到 WebSocket 连接是否可用。</span><span class="sxs-lookup"><span data-stu-id="a45fb-136">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="a45fb-137">WebSocket 是 SignalR 的理想之选传输，因为它使服务器内存的最有效地使用，具有最低的延迟，并且具有最基本功能 （如完整双工客户端和服务器之间的通信），但它还具有最严格要求： WebSocket 要求要使用 Windows Server 2012 或 Windows 8 和.NET Framework 4.5 的服务器。</span><span class="sxs-lookup"><span data-stu-id="a45fb-137">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="a45fb-138">如果不满足这些要求，SignalR 将尝试使用其他传输以其连接。</span><span class="sxs-lookup"><span data-stu-id="a45fb-138">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="a45fb-139">HTML 5 传输</span><span class="sxs-lookup"><span data-stu-id="a45fb-139">HTML 5 transports</span></span>

<span data-ttu-id="a45fb-140">这些传输协议依赖于支持[HTML 5](http://en.wikipedia.org/wiki/HTML5)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-140">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="a45fb-141">如果客户端浏览器不支持 HTML 5 标准，将使用较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-141">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="a45fb-142">**WebSocket** (如果服务器和浏览器指示它们可以支持 Websocket)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-142">**WebSocket** (if the both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="a45fb-143">WebSocket 是建立的则返回 true 的持久的双向连接客户端和服务器之间的唯一传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-143">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="a45fb-144">但是，WebSocket 还具有最严格的要求;它完全支持仅在最新版本的 Microsoft Internet Explorer、 Google Chrome 和 Mozilla Firefox 和 Opera 和 Safari 等其他浏览器中只有部分实现。</span><span class="sxs-lookup"><span data-stu-id="a45fb-144">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="a45fb-145">**服务器发送事件**，也称为 EventSource （如果在浏览器支持服务器发送事件，它基本上是除 Internet Explorer 的所有浏览器）。</span><span class="sxs-lookup"><span data-stu-id="a45fb-145">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="a45fb-146">Comet 传输</span><span class="sxs-lookup"><span data-stu-id="a45fb-146">Comet transports</span></span>

<span data-ttu-id="a45fb-147">基于以下传输[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 应用程序模型中，浏览器或其他客户端维护服务器可以用于将数据推送到客户端不使用客户端专门的长时间持有 HTTP 请求请求它。</span><span class="sxs-lookup"><span data-stu-id="a45fb-147">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="a45fb-148">**永久帧**（适用于 Internet Explorer)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-148">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="a45fb-149">永久帧创建隐藏的 IFrame 的未完成的服务器上的终结点向发出请求。</span><span class="sxs-lookup"><span data-stu-id="a45fb-149">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="a45fb-150">服务器然后不断会脚本发送到客户端立即执行，提供从服务器到客户端的单向实时连接。</span><span class="sxs-lookup"><span data-stu-id="a45fb-150">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="a45fb-151">从客户端与服务器的连接使用单独的连接从服务器到客户端连接和像标准的 HTTP 请求，为每个条需要发送的数据创建新的连接。</span><span class="sxs-lookup"><span data-stu-id="a45fb-151">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="a45fb-152">**Ajax 长轮询**。</span><span class="sxs-lookup"><span data-stu-id="a45fb-152">**Ajax long polling**.</span></span> <span data-ttu-id="a45fb-153">长轮询不创建持久性连接，但改为轮询具有保持打开状态直到服务器做出响应，此时将关闭连接，并立即请求新的连接的请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="a45fb-153">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="a45fb-154">连接重置时，这可能会造成一些延迟。</span><span class="sxs-lookup"><span data-stu-id="a45fb-154">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="a45fb-155">有关哪些传输受支持的配置下的详细信息，请参阅[支持的平台](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-155">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="a45fb-156">传输选择过程</span><span class="sxs-lookup"><span data-stu-id="a45fb-156">Transport selection process</span></span>

<span data-ttu-id="a45fb-157">以下列表显示 SignalR 使用来确定使用哪个传输的步骤。</span><span class="sxs-lookup"><span data-stu-id="a45fb-157">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="a45fb-158">如果浏览器是 Internet Explorer 8 或更早版本，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="a45fb-158">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="a45fb-159">如果配置 JSONP (即`jsonp`参数设置为`true`启动连接时)，使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="a45fb-159">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="a45fb-160">如果操作正在进行的跨域连接，（即，如果 SignalR 终结点不在托管的页面所在的域中），然后 WebSocket 将在满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="a45fb-160">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="a45fb-161">客户端支持 CORS （跨域资源共享）。</span><span class="sxs-lookup"><span data-stu-id="a45fb-161">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="a45fb-162">在其的客户端支持 CORS 的详细信息，请参阅[CORS 在 caniuse.com](http://www.caniuse.com/CORS)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-162">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="a45fb-163">客户端支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="a45fb-163">The client supports WebSocket</span></span>
   - <span data-ttu-id="a45fb-164">服务器支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="a45fb-164">The server supports WebSocket</span></span>

     <span data-ttu-id="a45fb-165">如果不满足任何这些条件，则将使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="a45fb-165">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="a45fb-166">有关跨域连接的详细信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="a45fb-166">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="a45fb-167">如果未配置 JSONP 并且连接不跨域，如果客户端和服务器支持它，则将使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a45fb-167">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="a45fb-168">如果客户端或服务器不支持 WebSocket，如果可用，则使用服务器发送事件。</span><span class="sxs-lookup"><span data-stu-id="a45fb-168">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="a45fb-169">如果服务器发送事件不可用，请尝试使用永久帧。</span><span class="sxs-lookup"><span data-stu-id="a45fb-169">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="a45fb-170">如果永久帧失败，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="a45fb-170">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="a45fb-171">监视传输</span><span class="sxs-lookup"><span data-stu-id="a45fb-171">Monitoring transports</span></span>

<span data-ttu-id="a45fb-172">您可以确定应用程序在中心上的日志记录和在浏览器中打开控制台窗口，从而使用什么传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-172">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="a45fb-173">若要启用浏览器中的中心的事件日志记录，客户端应用程序中添加以下命令：</span><span class="sxs-lookup"><span data-stu-id="a45fb-173">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="a45fb-174">在 Internet Explorer 中，通过按 F12 打开开发人员工具，并单击控制台选项卡。</span><span class="sxs-lookup"><span data-stu-id="a45fb-174">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![在 Microsoft Internet 资源管理器控制台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="a45fb-176">在 Chrome 中，通过按 Ctrl + Shift + J 打开控制台。</span><span class="sxs-lookup"><span data-stu-id="a45fb-176">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![在 Google Chrome 中的控制台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="a45fb-178">控制台打开和启用日志记录后，你可以查看 SignalR 正在使用哪种传输。</span><span class="sxs-lookup"><span data-stu-id="a45fb-178">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![控制台中显示 WebSocket 传输的 Internet 资源管理器](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="a45fb-180">指定在传输协议</span><span class="sxs-lookup"><span data-stu-id="a45fb-180">Specifying a transport</span></span>

<span data-ttu-id="a45fb-181">协商传输只占用一定的时间和客户端/服务器的资源。</span><span class="sxs-lookup"><span data-stu-id="a45fb-181">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="a45fb-182">如果已知的客户端功能，则传输可以指定启动客户端连接时。</span><span class="sxs-lookup"><span data-stu-id="a45fb-182">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="a45fb-183">下面的代码段演示如何启动使用 Ajax 长轮询传输方式，因为如果它已知客户端不支持任何其他协议将使用的连接：</span><span class="sxs-lookup"><span data-stu-id="a45fb-183">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="a45fb-184">如果你想要尝试按顺序的特定传输的客户端，可以指定回退的顺序。</span><span class="sxs-lookup"><span data-stu-id="a45fb-184">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="a45fb-185">下面的代码段演示尝试 WebSocket，并且如果没有问题，，直接转到长轮询。</span><span class="sxs-lookup"><span data-stu-id="a45fb-185">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="a45fb-186">用于指定传输中的字符串常数定义，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a45fb-186">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="a45fb-187">连接和集线器</span><span class="sxs-lookup"><span data-stu-id="a45fb-187">Connections and Hubs</span></span>

<span data-ttu-id="a45fb-188">SignalR API 包含客户端和服务器之间进行通信的两个模型： 永久连接和中心。</span><span class="sxs-lookup"><span data-stu-id="a45fb-188">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="a45fb-189">连接表示用于发送单个收件人、 分组或广播消息的简单终结点。</span><span class="sxs-lookup"><span data-stu-id="a45fb-189">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="a45fb-190">开发人员直接访问 SignalR 公开低级别通信协议 （由 PersistentConnection 类的.NET 代码中表示） 的持久性连接 API 提供。</span><span class="sxs-lookup"><span data-stu-id="a45fb-190">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="a45fb-191">使用连接的通信模型都会熟悉的开发人员已使用基于连接的 Api，如 Windows Communication Foundation。</span><span class="sxs-lookup"><span data-stu-id="a45fb-191">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="a45fb-192">中心是基于连接 API，从而使您的客户端和服务器直接相互调用方法的更多高级管道。</span><span class="sxs-lookup"><span data-stu-id="a45fb-192">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="a45fb-193">SignalR 处理跨计算机界限调度像变魔术一样，是通过允许客户端在服务器上调用方法，以轻松地为本地方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="a45fb-193">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="a45fb-194">使用中心的通信模型都会熟悉的开发人员已使用远程调用 Api，如.NET 远程处理。</span><span class="sxs-lookup"><span data-stu-id="a45fb-194">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="a45fb-195">使用中心还允许您将强类型化的参数传递给方法，使模型绑定。</span><span class="sxs-lookup"><span data-stu-id="a45fb-195">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="a45fb-196">体系结构关系图</span><span class="sxs-lookup"><span data-stu-id="a45fb-196">Architecture diagram</span></span>

<span data-ttu-id="a45fb-197">下图显示了中心、 永久连接和用于传输的基础技术之间的关系。</span><span class="sxs-lookup"><span data-stu-id="a45fb-197">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![显示 Api、 传输和客户端 SignalR 体系结构图示](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="a45fb-199">中心的工作原理</span><span class="sxs-lookup"><span data-stu-id="a45fb-199">How Hubs work</span></span>

<span data-ttu-id="a45fb-200">服务器端代码在客户端上调用的方法时发送一个数据包，在活动传输包含名称和要调用的方法的参数 （作为方法参数发送一个对象，它使用 JSON 序列化）。</span><span class="sxs-lookup"><span data-stu-id="a45fb-200">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="a45fb-201">然后，客户端匹配到客户端代码中定义的方法的方法名称。</span><span class="sxs-lookup"><span data-stu-id="a45fb-201">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="a45fb-202">如果没有匹配项，将使用反序列化的参数数据执行客户端方法。</span><span class="sxs-lookup"><span data-stu-id="a45fb-202">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="a45fb-203">可以使用像这样的工具监视方法调用[Fiddler。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="a45fb-203">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="a45fb-204">下图显示了从 SignalR 服务器发送到 web 浏览器客户端在 Fiddler 日志窗格中的方法调用。</span><span class="sxs-lookup"><span data-stu-id="a45fb-204">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="a45fb-205">方法调用从集线器调用发送`MoveShapeHub`，并正在调用的方法称为`updateShape`。</span><span class="sxs-lookup"><span data-stu-id="a45fb-205">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![显示 SignalR 流量的 Fiddler 日志的视图](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="a45fb-207">在此示例中，中心名称标识与`H`参数; 方法名称标识`M`参数，并发送到该方法的数据标识`A`参数。</span><span class="sxs-lookup"><span data-stu-id="a45fb-207">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="a45fb-208">生成此消息的应用程序中创建[高频率实时功能](tutorial-high-frequency-realtime-with-signalr.md)教程。</span><span class="sxs-lookup"><span data-stu-id="a45fb-208">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="a45fb-209">选择通信模型</span><span class="sxs-lookup"><span data-stu-id="a45fb-209">Choosing a communication model</span></span>

<span data-ttu-id="a45fb-210">大多数应用程序应使用中心 API。</span><span class="sxs-lookup"><span data-stu-id="a45fb-210">Most applications should use the Hubs API.</span></span> <span data-ttu-id="a45fb-211">可在以下情况下使用连接 API:</span><span class="sxs-lookup"><span data-stu-id="a45fb-211">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="a45fb-212">需要指定将发送的实际消息的格式。</span><span class="sxs-lookup"><span data-stu-id="a45fb-212">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="a45fb-213">开发人员倾向于使用消息传送与调度模型而不是远程调用模型。</span><span class="sxs-lookup"><span data-stu-id="a45fb-213">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="a45fb-214">使用消息传送模型的现有应用程序移植以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="a45fb-214">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
