---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 简介 |Microsoft 文档
author: pfletcher
description: 本文介绍了 SignalR 是什么，以及一些了要创建的解决方案。
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0ceca3edc26d35b1155946e60863a84da0bbe592
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873688"
---
<a name="introduction-to-signalr"></a><span data-ttu-id="63d72-103">SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="63d72-103">Introduction to SignalR</span></span>
====================
<span data-ttu-id="63d72-104">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="63d72-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="63d72-105">本文介绍了 SignalR 是什么，以及一些了要创建的解决方案。</span><span class="sxs-lookup"><span data-stu-id="63d72-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="63d72-106">问题和意见</span><span class="sxs-lookup"><span data-stu-id="63d72-106">Questions and comments</span></span>
> 
> <span data-ttu-id="63d72-107">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="63d72-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="63d72-108">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="63d72-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>


## <a name="what-is-signalr"></a><span data-ttu-id="63d72-109">什么是 SignalR？</span><span class="sxs-lookup"><span data-stu-id="63d72-109">What is SignalR?</span></span>

<span data-ttu-id="63d72-110">ASP.NET SignalR 是为 ASP.NET 开发人员库，它简化了将实时 web 功能添加到应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="63d72-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="63d72-111">实时 web 功能是能够具有服务器代码推送到连接的客户端立即内容变得可用，而不是让服务器等待客户端请求新数据。</span><span class="sxs-lookup"><span data-stu-id="63d72-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="63d72-112">SignalR 可用于将任何种类的"实时"web 功能添加到 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="63d72-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="63d72-113">尽管聊天经常使用作为示例，可以完成得多。</span><span class="sxs-lookup"><span data-stu-id="63d72-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="63d72-114">用户的任何次刷新网页可看到新数据，或页面实现[长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling)若要检索新数据，它是的候选使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="63d72-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="63d72-115">示例包括仪表板和监视应用程序，协作应用程序 （例如同时进行编辑的文档），作业的进度更新和实时窗体。</span><span class="sxs-lookup"><span data-stu-id="63d72-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="63d72-116">SignalR 也启用全新类型的 web 应用程序需要高频率更新在服务器上，例如，实时游戏。</span><span class="sxs-lookup"><span data-stu-id="63d72-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="63d72-117">SignalR 提供一个简单的 API，用于创建从服务器端.NET 代码的浏览器 （和其他客户端平台） 调用客户端中的 JavaScript 函数的服务器到客户端的远程过程调用 (RPC)。</span><span class="sxs-lookup"><span data-stu-id="63d72-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="63d72-118">SignalR 还包括用于连接管理 API （例如，连接和断开连接事件） 和分组连接。</span><span class="sxs-lookup"><span data-stu-id="63d72-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![使用 SignalR 的调用方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="63d72-120">SignalR 自动，处理的连接管理，可以在将消息广播到所有连接的客户端同时，如聊天室。</span><span class="sxs-lookup"><span data-stu-id="63d72-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="63d72-121">你还可以向特定客户端发送消息。</span><span class="sxs-lookup"><span data-stu-id="63d72-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="63d72-122">客户端和服务器之间的连接是持久性的与经典的 HTTP 连接，这是为每个通信重新建立不同。</span><span class="sxs-lookup"><span data-stu-id="63d72-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="63d72-123">SignalR 支持"服务器推送"功能，在其中服务器代码可以调用的客户端代码中使用的浏览器远程过程调用 (RPC)，而不是常见请求-响应模式在 web 上今天。</span><span class="sxs-lookup"><span data-stu-id="63d72-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="63d72-124">SignalR 应用程序可以向外扩展到数千个客户端使用 Service Bus、 SQL Server 或[Redis](http://redis.io)。</span><span class="sxs-lookup"><span data-stu-id="63d72-124">SignalR applications can scale out to thousands of clients using Service Bus, SQL Server or [Redis](http://redis.io).</span></span>

<span data-ttu-id="63d72-125">SignalR 是开放源代码，可通过访问[GitHub](https://github.com/signalr)。</span><span class="sxs-lookup"><span data-stu-id="63d72-125">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="63d72-126">SignalR 和 WebSocket</span><span class="sxs-lookup"><span data-stu-id="63d72-126">SignalR and WebSocket</span></span>

<span data-ttu-id="63d72-127">SignalR 可用的地方，使用新的 WebSocket 传输，并在必要时回退到较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="63d72-127">SignalR uses the new WebSocket transport where available, and falls back to older transports where necessary.</span></span> <span data-ttu-id="63d72-128">虽然您肯定可以编写你直接使用 WebSocket，并使用 SignalR 意味着大量的额外功能，你将需要实现将已进行了为你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="63d72-128">While you could certainly write your application using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement will already have been done for you.</span></span> <span data-ttu-id="63d72-129">最重要的是，这意味着，你可以编写代码，你的应用程序以利用而无需担心创建一个单独的代码路径的较旧的客户端 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="63d72-129">Most importantly, this means that you can code your application to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="63d72-130">SignalR 还可保护你无需担心对 WebSocket，更新，因为 SignalR 将继续更新以支持在基础传输协议，更改各个 WebSocket 版本提供你的应用程序一致的接口。</span><span class="sxs-lookup"><span data-stu-id="63d72-130">SignalR also shields you from having to worry about updates to WebSocket, since SignalR will continue to be updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<span data-ttu-id="63d72-131">虽然你肯定可以创建使用 WebSocket 单独的解决方案，SignalR 提供了所有需要编写你自己，如回退到其他传输和修改你的应用程序更新到 WebSocket 实现的功能。</span><span class="sxs-lookup"><span data-stu-id="63d72-131">While you could certainly create a solution using WebSocket alone, SignalR provides all of the functionality you would need to write yourself, such as fallback to other transports and revising your application for updates to WebSocket implementations.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="63d72-132">传输和回退</span><span class="sxs-lookup"><span data-stu-id="63d72-132">Transports and fallbacks</span></span>

<span data-ttu-id="63d72-133">SignalR 是上某些要求进行客户端和服务器之间的实时工作的传输的抽象。</span><span class="sxs-lookup"><span data-stu-id="63d72-133">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="63d72-134">SignalR 连接作为 HTTP，启动，并在可用然后提升到的 WebSocket 连接。</span><span class="sxs-lookup"><span data-stu-id="63d72-134">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="63d72-135">因为它将建立最有效的服务器内存使用、 具有最低的延迟，并具有最基础功能 （如完整双工客户端和服务器之间的通信），但它还具有最严格，WebSocket 处于 SignalR 的理想传输要求： WebSocket 要求服务器使用 Windows Server 2012 或 Windows 8 和.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="63d72-135">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="63d72-136">如果不满足这些要求，SignalR 将尝试使用其他传输以其连接。</span><span class="sxs-lookup"><span data-stu-id="63d72-136">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="63d72-137">HTML 5 传输</span><span class="sxs-lookup"><span data-stu-id="63d72-137">HTML 5 transports</span></span>

<span data-ttu-id="63d72-138">这些传输依赖于支持[HTML 5](http://en.wikipedia.org/wiki/HTML5)。</span><span class="sxs-lookup"><span data-stu-id="63d72-138">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="63d72-139">如果客户端浏览器不支持 HTML 5 标准，将使用较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="63d72-139">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="63d72-140">**WebSocket** (如果服务器和浏览器指示其可以支持 Websocket)。</span><span class="sxs-lookup"><span data-stu-id="63d72-140">**WebSocket** (if the both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="63d72-141">WebSocket 是建立客户端和服务器之间的 true 持久的双向连接的唯一传输。</span><span class="sxs-lookup"><span data-stu-id="63d72-141">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="63d72-142">但是，WebSocket 还具有最严格的要求;它仅在最新版本的 Microsoft Internet Explorer、 Google Chrome 和 Mozilla Firefox 受到完全支持，并在其他浏览器，如 Opera 和 Safari 中只有部分实现。</span><span class="sxs-lookup"><span data-stu-id="63d72-142">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="63d72-143">**服务器发送事件**，也称为 EventSource （如果浏览器支持服务器发送事件，它本质上是除 Internet Explorer 的所有浏览器）。</span><span class="sxs-lookup"><span data-stu-id="63d72-143">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="63d72-144">Comet 传输</span><span class="sxs-lookup"><span data-stu-id="63d72-144">Comet transports</span></span>

<span data-ttu-id="63d72-145">基于以下传输[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 应用程序模型，在浏览器或其他客户端维护一个长时间保留的 HTTP 请求，服务器可以用于将数据推送到客户端不使用客户端专门请求它。</span><span class="sxs-lookup"><span data-stu-id="63d72-145">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="63d72-146">**不限次数帧**（适用于仅 Internet Explorer)。</span><span class="sxs-lookup"><span data-stu-id="63d72-146">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="63d72-147">不限次数帧创建隐藏的 IFrame 的未完成的服务器上的终结点向发出请求。</span><span class="sxs-lookup"><span data-stu-id="63d72-147">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="63d72-148">服务器然后不断脚本向发送客户端立即执行，从而提供从服务器到客户端的单向实时连接。</span><span class="sxs-lookup"><span data-stu-id="63d72-148">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="63d72-149">从客户端到服务器的连接使用单独的连接从服务器到客户端连接和每个需要发送的数据的标准的 HTTP 请求，如创建新的连接。</span><span class="sxs-lookup"><span data-stu-id="63d72-149">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="63d72-150">**Ajax 长轮询**。</span><span class="sxs-lookup"><span data-stu-id="63d72-150">**Ajax long polling**.</span></span> <span data-ttu-id="63d72-151">长轮询不会创建持续性连接，但改为轮询具有保持打开状态直到服务器响应，此时将关闭连接，并且立即请求新的连接的请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="63d72-151">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="63d72-152">连接重置时，这会产生一定的延迟。</span><span class="sxs-lookup"><span data-stu-id="63d72-152">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="63d72-153">有关哪些传输受支持的配置下的详细信息，请参阅[支持的平台](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="63d72-153">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="63d72-154">传输选择过程</span><span class="sxs-lookup"><span data-stu-id="63d72-154">Transport selection process</span></span>

<span data-ttu-id="63d72-155">以下列表显示 SignalR 使用来决定该传输使用的步骤。</span><span class="sxs-lookup"><span data-stu-id="63d72-155">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="63d72-156">如果浏览器为 Internet Explorer 8 或更早版本，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="63d72-156">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="63d72-157">如果配置 JSONP (即，`jsonp`参数设置为`true`连接在启动时)，使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="63d72-157">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="63d72-158">如果操作正在进行的跨域连接，（即，如果该 SignalR 终结点不作为宿主的页位于同一域中），然后 WebSocket 将使用如果满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="63d72-158">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="63d72-159">客户端支持 CORS （跨域资源共享）。</span><span class="sxs-lookup"><span data-stu-id="63d72-159">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="63d72-160">有关在其的客户端支持 CORS 的详细信息，请参阅[在 caniuse.com CORS](http://www.caniuse.com/CORS)。</span><span class="sxs-lookup"><span data-stu-id="63d72-160">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="63d72-161">客户端支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="63d72-161">The client supports WebSocket</span></span>
   - <span data-ttu-id="63d72-162">服务器支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="63d72-162">The server supports WebSocket</span></span>

     <span data-ttu-id="63d72-163">如果不满足任何这些条件，则将使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="63d72-163">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="63d72-164">跨域连接的详细信息，请参阅[如何建立的跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="63d72-164">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="63d72-165">如果未配置 JSONP 并且此连接不是跨域，如果客户端和服务器支持它，将使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="63d72-165">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="63d72-166">如果客户端或服务器不支持 WebSocket，如果可用，则使用服务器发送事件。</span><span class="sxs-lookup"><span data-stu-id="63d72-166">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="63d72-167">如果服务器发送事件不可用，将尝试永久帧。</span><span class="sxs-lookup"><span data-stu-id="63d72-167">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="63d72-168">如果永久帧失败，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="63d72-168">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="63d72-169">监视传输</span><span class="sxs-lookup"><span data-stu-id="63d72-169">Monitoring transports</span></span>

<span data-ttu-id="63d72-170">你可以确定你的应用程序使用通过启用日志记录在你的中心，并在浏览器中打开控制台窗口什么传输。</span><span class="sxs-lookup"><span data-stu-id="63d72-170">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="63d72-171">若要启用在浏览器的中心的事件的日志记录，请向客户端应用程序添加以下命令：</span><span class="sxs-lookup"><span data-stu-id="63d72-171">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="63d72-172">在 Internet Explorer 中，通过按 F12，打开开发人员工具，然后单击控制台选项卡。</span><span class="sxs-lookup"><span data-stu-id="63d72-172">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![在 Microsoft Internet 资源管理器控制台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="63d72-174">在 Chrome 中，通过按 Ctrl + Shift + J 打开控制台。</span><span class="sxs-lookup"><span data-stu-id="63d72-174">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![在 Google Chrome 的控制台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="63d72-176">控制台打开和启用日志记录，你将能够看到 SignalR 正在使用的传输。</span><span class="sxs-lookup"><span data-stu-id="63d72-176">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![控制台在 Internet Explorer 中显示 WebSocket 传输](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="63d72-178">指定传输</span><span class="sxs-lookup"><span data-stu-id="63d72-178">Specifying a transport</span></span>

<span data-ttu-id="63d72-179">协商传输需要一定的时间和客户端/服务器资源。</span><span class="sxs-lookup"><span data-stu-id="63d72-179">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="63d72-180">如果已知的客户端功能，则传输可以指定在启动客户端连接时。</span><span class="sxs-lookup"><span data-stu-id="63d72-180">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="63d72-181">下面的代码段演示如何启动使用 Ajax 长轮询传输中，因为如果它已知道，客户端不支持任何其他协议将使用的连接：</span><span class="sxs-lookup"><span data-stu-id="63d72-181">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="63d72-182">如果你想要尝试按顺序的特定传输的客户端，你可以指定回退的顺序。</span><span class="sxs-lookup"><span data-stu-id="63d72-182">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="63d72-183">下面的代码段演示试图 WebSocket 和失败、 直接转到长轮询。</span><span class="sxs-lookup"><span data-stu-id="63d72-183">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="63d72-184">用于指定传输的字符串常量定义，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63d72-184">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="63d72-185">连接和中心</span><span class="sxs-lookup"><span data-stu-id="63d72-185">Connections and Hubs</span></span>

<span data-ttu-id="63d72-186">SignalR API 包含用于客户端和服务器之间进行通信的两个模型： 永久连接和中心。</span><span class="sxs-lookup"><span data-stu-id="63d72-186">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="63d72-187">连接表示发送单收件人、 分组，或广播消息的简单终结的点。</span><span class="sxs-lookup"><span data-stu-id="63d72-187">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="63d72-188">开发人员直接访问 SignalR 公开的低级别的通信协议 （以.NET 代码 PersistentConnection 类表示） 的持久性连接 API 提供。</span><span class="sxs-lookup"><span data-stu-id="63d72-188">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="63d72-189">使用连接通信模型将熟悉的开发人员可以使用基于连接的 Api，如 Windows Communication Foundation。</span><span class="sxs-lookup"><span data-stu-id="63d72-189">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="63d72-190">中心是基于连接 API，从而使你的客户端和服务器相互直接调用方法的更多高级管道。</span><span class="sxs-lookup"><span data-stu-id="63d72-190">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="63d72-191">SignalR 处理跨计算机界限调度像是通过幻数，从而允许客户端在服务器上调用方法，作为轻松地为本地方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="63d72-191">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="63d72-192">使用中心通信模型将熟悉的开发人员可以使用远程调用 Api 如.NET 远程处理。</span><span class="sxs-lookup"><span data-stu-id="63d72-192">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="63d72-193">使用中心还使你可以将强类型的参数传递给方法，使模型绑定。</span><span class="sxs-lookup"><span data-stu-id="63d72-193">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="63d72-194">体系结构关系图</span><span class="sxs-lookup"><span data-stu-id="63d72-194">Architecture diagram</span></span>

<span data-ttu-id="63d72-195">下图显示了中心、 永久连接和的传输使用的基础技术之间的关系。</span><span class="sxs-lookup"><span data-stu-id="63d72-195">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![显示 Api、 传输和客户端的 SignalR 体系结构图示](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="63d72-197">中心的工作原理</span><span class="sxs-lookup"><span data-stu-id="63d72-197">How Hubs work</span></span>

<span data-ttu-id="63d72-198">当服务器端代码在客户端上调用方法时，跨包含的名称和要调用的方法的参数的活动传输发送一个数据包 （与方法参数发送一个对象，它使用序列化 JSON）。</span><span class="sxs-lookup"><span data-stu-id="63d72-198">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="63d72-199">客户端在客户端代码中定义的方法将方法名称，然后进行匹配。</span><span class="sxs-lookup"><span data-stu-id="63d72-199">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="63d72-200">如果没有匹配项，则将执行客户端方法使用的反序列化的参数数据。</span><span class="sxs-lookup"><span data-stu-id="63d72-200">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="63d72-201">可以使用类似的工具来监视的方法调用[Fiddler。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="63d72-201">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="63d72-202">下图显示从 SignalR 服务器发送到 web 浏览器客户端在 Fiddler 日志窗格中的方法调用。</span><span class="sxs-lookup"><span data-stu-id="63d72-202">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="63d72-203">方法调用从调用的集线器发送`MoveShapeHub`，正在调用的方法称为`updateShape`。</span><span class="sxs-lookup"><span data-stu-id="63d72-203">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![Fiddler 日志显示 SignalR 流量视图](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="63d72-205">在此示例中，中心名称标识与`H`参数; 该方法名称识别具有以下`M`参数，并且发送到该方法的数据识别具有以下`A`参数。</span><span class="sxs-lookup"><span data-stu-id="63d72-205">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="63d72-206">生成此消息的应用程序创建在[高频率实时](tutorial-high-frequency-realtime-with-signalr.md)教程。</span><span class="sxs-lookup"><span data-stu-id="63d72-206">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="63d72-207">选择的通信模型</span><span class="sxs-lookup"><span data-stu-id="63d72-207">Choosing a communication model</span></span>

<span data-ttu-id="63d72-208">大多数应用程序应使用的中心 API。</span><span class="sxs-lookup"><span data-stu-id="63d72-208">Most applications should use the Hubs API.</span></span> <span data-ttu-id="63d72-209">可在以下情况下使用连接 API:</span><span class="sxs-lookup"><span data-stu-id="63d72-209">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="63d72-210">需要指定将发送的实际消息的格式。</span><span class="sxs-lookup"><span data-stu-id="63d72-210">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="63d72-211">开发人员更愿意使用一种消息传递和调度模式，而不是远程调用模型。</span><span class="sxs-lookup"><span data-stu-id="63d72-211">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="63d72-212">现有应用程序使用消息传送模型是在移植后使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="63d72-212">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
