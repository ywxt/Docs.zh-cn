---
uid: signalr/overview/performance/signalr-performance
title: "SignalR 性能 |Microsoft 文档"
author: pfletcher
description: "SignalR 性能"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 4468ee8031afccca847db67bd4b5b263f0a2c5ac
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="signalr-performance"></a><span data-ttu-id="274c2-103">SignalR 性能</span><span class="sxs-lookup"><span data-stu-id="274c2-103">SignalR Performance</span></span>
====================
<span data-ttu-id="274c2-104">通过[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="274c2-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="274c2-105">本主题介绍如何设计、 测量和提高 SignalR 应用程序中的性能。</span><span class="sxs-lookup"><span data-stu-id="274c2-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="274c2-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="274c2-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="274c2-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="274c2-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="274c2-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="274c2-108">.NET 4.5</span></span>
> - <span data-ttu-id="274c2-109">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="274c2-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="274c2-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="274c2-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="274c2-111">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="274c2-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="274c2-112">问题和意见</span><span class="sxs-lookup"><span data-stu-id="274c2-112">Questions and comments</span></span>
> 
> <span data-ttu-id="274c2-113">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="274c2-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="274c2-114">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="274c2-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="274c2-115">有关对 SignalR 性能和缩放一个新演示文稿，请参阅[缩放使用 ASP.NET SignalR 实时 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。</span><span class="sxs-lookup"><span data-stu-id="274c2-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="274c2-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="274c2-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="274c2-117">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="274c2-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="274c2-118">优化性能你 SignalR 服务器</span><span class="sxs-lookup"><span data-stu-id="274c2-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="274c2-119">故障排除性能问题</span><span class="sxs-lookup"><span data-stu-id="274c2-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="274c2-120">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="274c2-121">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="274c2-122">其他资源</span><span class="sxs-lookup"><span data-stu-id="274c2-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="274c2-123">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="274c2-123">Design considerations</span></span>

<span data-ttu-id="274c2-124">本部分介绍可以实现 SignalR 应用程序，以确保不影响性能通过生成不必要的网络流量的设计过程中的模式。</span><span class="sxs-lookup"><span data-stu-id="274c2-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="274c2-125">限制消息频率</span><span class="sxs-lookup"><span data-stu-id="274c2-125">Throttling message frequency</span></span>

<span data-ttu-id="274c2-126">即使在发出高频率 （如实时游戏应用程序） 的消息的应用，大多数应用程序无需发送第二个较多消息。</span><span class="sxs-lookup"><span data-stu-id="274c2-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="274c2-127">若要减少的每个客户端生成的流量，消息循环可以实现队列和发送出消息不能超过固定费率频繁 （即最多一定数量的消息将发送每隔一秒，如果在该时间中有消息terval 发送)。</span><span class="sxs-lookup"><span data-stu-id="274c2-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="274c2-128">限制为某些传输率 （从客户端和服务器） 的消息的示例应用，请参阅[使用 SignalR 高频率实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="274c2-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="274c2-129">减少消息大小</span><span class="sxs-lookup"><span data-stu-id="274c2-129">Reducing message size</span></span>

<span data-ttu-id="274c2-130">你可以减少 SignalR 消息的大小，从而降低的序列化对象的大小。</span><span class="sxs-lookup"><span data-stu-id="274c2-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="274c2-131">在服务器代码中，如果您要发送的对象，其中包含要传输不需要的属性，防止这些属性进行序列化使用`JsonIgnore`属性。</span><span class="sxs-lookup"><span data-stu-id="274c2-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="274c2-132">属性的名称也存储在 message;可以使用缩短至属性的名称`JsonProperty`属性。</span><span class="sxs-lookup"><span data-stu-id="274c2-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="274c2-133">下面的代码示例演示如何从正在发送到客户端，排除属性以及如何缩短属性名称：</span><span class="sxs-lookup"><span data-stu-id="274c2-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="274c2-134">**.NET 服务器代码来演示 JsonIgnore 属性来排除数据被发送到客户端，以及要减少消息大小的 JsonProperty 属性**</span><span class="sxs-lookup"><span data-stu-id="274c2-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="274c2-135">若要保留可读性 / 在客户端代码可维护性，在收到消息后，缩写的属性名称可以是重新映射到用户友好名称。</span><span class="sxs-lookup"><span data-stu-id="274c2-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="274c2-136">下面的代码示例演示如何重新映射到较长的通过定义消息协定 （映射） 的缩写的名称的可能方法和使用`reMap`函数可将协定应用于优化的消息类：</span><span class="sxs-lookup"><span data-stu-id="274c2-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="274c2-137">**重新映射的客户端 JavaScript 代码缩短到用户可读名称的属性名称**</span><span class="sxs-lookup"><span data-stu-id="274c2-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="274c2-138">名称可以缩短到服务器，从客户端的消息中使用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="274c2-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="274c2-139">减少内存占用量 （即的消息所使用的内存量） 消息的对象还可提高性能。</span><span class="sxs-lookup"><span data-stu-id="274c2-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="274c2-140">例如，如果的完整范围的`int`不需要`short`或`byte`可以改为使用。</span><span class="sxs-lookup"><span data-stu-id="274c2-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="274c2-141">因为消息存储在服务器内存，从而减少的消息的大小中的消息总线还可以解决服务器内存问题。</span><span class="sxs-lookup"><span data-stu-id="274c2-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="274c2-142">优化性能你 SignalR 服务器</span><span class="sxs-lookup"><span data-stu-id="274c2-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="274c2-143">以下配置设置可以用于调整为更好的性能 SignalR 应用程序服务器。</span><span class="sxs-lookup"><span data-stu-id="274c2-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="274c2-144">有关如何提高性能 ASP.NET 应用程序中的常规信息，请参阅[因而提高了 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="274c2-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="274c2-145">**SignalR 配置设置**</span><span class="sxs-lookup"><span data-stu-id="274c2-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="274c2-146">**DefaultMessageBufferSize**： 默认情况下，SignalR 将保留在内存中的每个连接的中心每 1000 条消息。</span><span class="sxs-lookup"><span data-stu-id="274c2-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="274c2-147">如果正在使用大消息，这可能产生内存问题，这可以缓解通过减小此值。</span><span class="sxs-lookup"><span data-stu-id="274c2-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="274c2-148">可以在设置此设置`Application_Start`事件处理程序在 ASP.NET 应用程序，或在`Configuration`在自承载应用程序的 OWIN 启动类的方法。</span><span class="sxs-lookup"><span data-stu-id="274c2-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="274c2-149">下面的示例演示如何以减少你的应用程序，以减少使用的服务器内存量的内存需求量减小此值：</span><span class="sxs-lookup"><span data-stu-id="274c2-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="274c2-150">**会在 Startup.cs 的.NET 服务器代码用于减少默认消息缓冲区大小**</span><span class="sxs-lookup"><span data-stu-id="274c2-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="274c2-151">**IIS 配置设置**</span><span class="sxs-lookup"><span data-stu-id="274c2-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="274c2-152">**每个应用程序的最大并发请求**： 并发 IIS 数目增加请求将增加可用于为请求提供服务的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="274c2-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="274c2-153">默认值为 5000;若要增加此设置，请在提升的命令提示符执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="274c2-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="274c2-154">**ApplicationPool QueueLength**： 这是最大 Http.sys 排队应用程序池的请求数。</span><span class="sxs-lookup"><span data-stu-id="274c2-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="274c2-155">如果队列已满，新请求将收到 503"服务不可用"响应。</span><span class="sxs-lookup"><span data-stu-id="274c2-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="274c2-156">默认值为 1000。</span><span class="sxs-lookup"><span data-stu-id="274c2-156">The default value is 1000.</span></span>

    <span data-ttu-id="274c2-157">缩短的工作进程中承载你的应用程序的应用程序池的队列长度将节省内存资源。</span><span class="sxs-lookup"><span data-stu-id="274c2-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="274c2-158">有关详细信息，请参阅[管理、 优化和配置应用程序池](https://technet.microsoft.com/library/cc745955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="274c2-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="274c2-159">**ASP.NET 配置设置**</span><span class="sxs-lookup"><span data-stu-id="274c2-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="274c2-160">本节包含可以在中设置的配置设置`aspnet.config`文件。</span><span class="sxs-lookup"><span data-stu-id="274c2-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="274c2-161">两个位置之一，具体取决于平台中可以找到此文件：</span><span class="sxs-lookup"><span data-stu-id="274c2-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="274c2-162">可能会提高 SignalR 性能的 ASP.NET 设置包括：</span><span class="sxs-lookup"><span data-stu-id="274c2-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="274c2-163">**每个 CPU 的最大并发请求**： 增加此设置可以缓解性能瓶颈。</span><span class="sxs-lookup"><span data-stu-id="274c2-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="274c2-164">若要增加此设置，添加以下配置设置来`aspnet.config`文件：</span><span class="sxs-lookup"><span data-stu-id="274c2-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="274c2-165">**请求队列限制**： 当连接总数超过`maxConcurrentRequestsPerCPU`设置，ASP.NET 将开始限制使用队列的请求。</span><span class="sxs-lookup"><span data-stu-id="274c2-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="274c2-166">若要增加队列的大小，你可以增加`requestQueueLimit`设置。</span><span class="sxs-lookup"><span data-stu-id="274c2-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="274c2-167">若要执行此操作，将添加到以下配置设置`processModel`中的节点`config/machine.config`(而非`aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="274c2-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="274c2-168">故障排除性能问题</span><span class="sxs-lookup"><span data-stu-id="274c2-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="274c2-169">本部分介绍如何在你的应用程序中查找性能瓶颈。</span><span class="sxs-lookup"><span data-stu-id="274c2-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="274c2-170">验证正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="274c2-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="274c2-171">尽管 SignalR 可以使用各种传输方式，客户端和服务器之间的通信，WebSocket 提供显著的性能优势，并且应在客户端和服务器支持它。</span><span class="sxs-lookup"><span data-stu-id="274c2-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="274c2-172">若要确定客户端和服务器是否满足 WebSocket 的要求，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="274c2-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="274c2-173">若要确定你的应用程序中正在使用什么传输，可以使用浏览器开发人员工具，并检查日志以查看连接的使用什么传输。</span><span class="sxs-lookup"><span data-stu-id="274c2-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="274c2-174">有关使用 Internet Explorer 和 Chrome 中的浏览器开发工具的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="274c2-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="274c2-175">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-175">Using SignalR performance counters</span></span>

<span data-ttu-id="274c2-176">本部分介绍如何启用和使用 SignalR 性能计数器，在中找到`Microsoft.AspNet.SignalR.Utils`包。</span><span class="sxs-lookup"><span data-stu-id="274c2-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="274c2-177">安装 signalr.exe</span><span class="sxs-lookup"><span data-stu-id="274c2-177">Installing signalr.exe</span></span>

<span data-ttu-id="274c2-178">可以使用名为 SignalR.exe 的实用工具向服务器添加性能计数器。</span><span class="sxs-lookup"><span data-stu-id="274c2-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="274c2-179">若要安装此实用程序，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="274c2-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="274c2-180">在 Visual Studio 应用程序中，选择**工具**，**库程序包管理器**，**管理解决方案的 NuGet 包...**</span><span class="sxs-lookup"><span data-stu-id="274c2-180">In your Visual Studio application, select **Tools**, **Library Package Manager**, **Manage NuGet Packages for Solution...**</span></span>
2. <span data-ttu-id="274c2-181">搜索**signalr.utils**，并选择安装。</span><span class="sxs-lookup"><span data-stu-id="274c2-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="274c2-182">接受的许可协议才能安装包。</span><span class="sxs-lookup"><span data-stu-id="274c2-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="274c2-183">SignalR.exe 将安装到`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。</span><span class="sxs-lookup"><span data-stu-id="274c2-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="274c2-184">使用 SignalR.exe 安装性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="274c2-185">若要安装 SignalR 性能计数器，请在提升的命令提示符使用以下参数运行 SignalR.exe:</span><span class="sxs-lookup"><span data-stu-id="274c2-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="274c2-186">若要删除 SignalR 性能计数器，请在提升的命令提示符使用以下参数运行 SignalR.exe:</span><span class="sxs-lookup"><span data-stu-id="274c2-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="274c2-187">SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-187">SignalR Performance counters</span></span>

<span data-ttu-id="274c2-188">实用工具程序包将安装以下性能计数器。</span><span class="sxs-lookup"><span data-stu-id="274c2-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="274c2-189">"总"计数器测量事件的数，因为最后一个应用程序池或服务器重新启动。</span><span class="sxs-lookup"><span data-stu-id="274c2-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="274c2-190">**连接度量值**</span><span class="sxs-lookup"><span data-stu-id="274c2-190">**Connection metrics**</span></span>

<span data-ttu-id="274c2-191">以下度量值度量发生的连接生存期事件。</span><span class="sxs-lookup"><span data-stu-id="274c2-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="274c2-192">有关详细信息，请参阅[了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="274c2-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="274c2-193">**连接的连接**</span><span class="sxs-lookup"><span data-stu-id="274c2-193">**Connections Connected**</span></span>
- <span data-ttu-id="274c2-194">**重新连接的连接**</span><span class="sxs-lookup"><span data-stu-id="274c2-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="274c2-195">**断开连接的连接**</span><span class="sxs-lookup"><span data-stu-id="274c2-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="274c2-196">**连接当前**</span><span class="sxs-lookup"><span data-stu-id="274c2-196">**Connections Current**</span></span>

<span data-ttu-id="274c2-197">**消息度量值**</span><span class="sxs-lookup"><span data-stu-id="274c2-197">**Message metrics**</span></span>

<span data-ttu-id="274c2-198">以下度量值度量值产生 SignalR 的消息流量。</span><span class="sxs-lookup"><span data-stu-id="274c2-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="274c2-199">**接收连接消息的总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="274c2-200">**发送的总连接消息**</span><span class="sxs-lookup"><span data-stu-id="274c2-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="274c2-201">**连接接收的消息/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="274c2-202">**连接发送的消息/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="274c2-203">**消息总线度量值**</span><span class="sxs-lookup"><span data-stu-id="274c2-203">**Message bus metrics**</span></span>

<span data-ttu-id="274c2-204">以下度量值度量流量通过内部 SignalR 消息总线，位于所有传入和传出 SignalR 消息队列。</span><span class="sxs-lookup"><span data-stu-id="274c2-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="274c2-205">一条消息是**已发布**发送或广播时。</span><span class="sxs-lookup"><span data-stu-id="274c2-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="274c2-206">A**订阅服务器**在此上下文是消息总线上的订阅; 此选项应等于数客户端加上在服务器本身。</span><span class="sxs-lookup"><span data-stu-id="274c2-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="274c2-207">**分配辅助**是一个组件，将数据发送到活动连接;**忙的辅助**是指正在发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="274c2-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="274c2-208">**消息总线消息接收的总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="274c2-209">**消息总线消息 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="274c2-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="274c2-210">**发布内容的消息总线消息总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="274c2-211">**消息总线邮件发布/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="274c2-212">**消息总线订阅服务器当前**</span><span class="sxs-lookup"><span data-stu-id="274c2-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="274c2-213">**消息总线订阅服务器总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="274c2-214">**消息总线订阅服务器/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="274c2-215">**消息总线分配辅助角色**</span><span class="sxs-lookup"><span data-stu-id="274c2-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="274c2-216">**消息总线忙碌工作线程**</span><span class="sxs-lookup"><span data-stu-id="274c2-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="274c2-217">**消息总线主题当前**</span><span class="sxs-lookup"><span data-stu-id="274c2-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="274c2-218">**错误度量值**</span><span class="sxs-lookup"><span data-stu-id="274c2-218">**Error metrics**</span></span>

<span data-ttu-id="274c2-219">以下度量值度量 SignalR 消息流量所生成错误。</span><span class="sxs-lookup"><span data-stu-id="274c2-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="274c2-220">**中心解析**无法解析中心或中心方法时发生错误。</span><span class="sxs-lookup"><span data-stu-id="274c2-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="274c2-221">**中心调用**错误是调用 hub 方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="274c2-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="274c2-222">**传输**错误是在 HTTP 请求或响应过程中引发的连接错误。</span><span class="sxs-lookup"><span data-stu-id="274c2-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="274c2-223">**错误： 所有总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-223">**Errors: All Total**</span></span>
- <span data-ttu-id="274c2-224">**错误： All/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="274c2-225">**错误： 中心解析总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="274c2-226">**错误： 中心解析/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="274c2-227">**错误： 中心调用总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="274c2-228">**错误： 中心调用/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="274c2-229">**错误： 传输总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="274c2-230">**错误： 传输/秒**</span><span class="sxs-lookup"><span data-stu-id="274c2-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="274c2-231">**向外缩放度量值**</span><span class="sxs-lookup"><span data-stu-id="274c2-231">**Scaleout metrics**</span></span>

<span data-ttu-id="274c2-232">以下度量值度量流量和向外扩展提供程序生成的错误。</span><span class="sxs-lookup"><span data-stu-id="274c2-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="274c2-233">A**流**在此上下文中程序是一个扩展单元向外扩展提供程序使用; 这是如果使用的 SQL Server 表，如果使用 Service Bus，主题和订阅如果使用 Redis。</span><span class="sxs-lookup"><span data-stu-id="274c2-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="274c2-234">每个流可确保有序的读取和写入操作;单个流是一个潜在的缩放瓶颈，因此可以增加流的数量，以帮助减少该瓶颈。</span><span class="sxs-lookup"><span data-stu-id="274c2-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="274c2-235">如果使用多个流，则 SignalR 将自动分布这些流的方式，以确保从任何给定的连接发送的消息是按顺序的 （分片） 消息。</span><span class="sxs-lookup"><span data-stu-id="274c2-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="274c2-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)设置由 SignalR 维护的向外缩放发送队列长度的控件。</span><span class="sxs-lookup"><span data-stu-id="274c2-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="274c2-237">将其设置为一个值大于 0 将将所有消息都放入发送队列发送一次一个地到配置的消息传递基架。</span><span class="sxs-lookup"><span data-stu-id="274c2-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="274c2-238">如果队列的大小超过所配置的长度，将发送的后续调用失败，立即并[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)直到中队列的消息数小于设置试。</span><span class="sxs-lookup"><span data-stu-id="274c2-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="274c2-239">默认情况下，因为实现背板通常具有其自己的队列或流控制就地，队列处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="274c2-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="274c2-240">对于 SQL Server 连接池有效地限制进展情况在任何时候的发送的数目。</span><span class="sxs-lookup"><span data-stu-id="274c2-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="274c2-241">默认情况下，只有一个流适用于 SQL Server 和 Redis，五个流用于服务总线和队列处于禁用状态，但可以通过在 SQL Server 和 Service Bus 上的配置更改这些设置：</span><span class="sxs-lookup"><span data-stu-id="274c2-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="274c2-242">**.NET 服务器代码配置 SQL Server 底板的表计数和队列长度**</span><span class="sxs-lookup"><span data-stu-id="274c2-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="274c2-243">**.NET 服务器代码配置 Service Bus 底板的主题计数和队列长度**</span><span class="sxs-lookup"><span data-stu-id="274c2-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="274c2-244">A**缓冲功能**流是指已进入错误的状态; 出错状态流时，发送到底板所有消息之前，都无法立即流不再出现错误。</span><span class="sxs-lookup"><span data-stu-id="274c2-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="274c2-245">**发送队列长度**是公布的但尚未发送的消息数。</span><span class="sxs-lookup"><span data-stu-id="274c2-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="274c2-246">**向外扩展消息总线消息 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="274c2-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="274c2-247">**向外缩放流总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="274c2-248">**向外缩放流式处理打开**</span><span class="sxs-lookup"><span data-stu-id="274c2-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="274c2-249">**向外缩放流缓冲**</span><span class="sxs-lookup"><span data-stu-id="274c2-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="274c2-250">**向外缩放错误总数**</span><span class="sxs-lookup"><span data-stu-id="274c2-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="274c2-251">**Scaleout Errors/Sec**</span><span class="sxs-lookup"><span data-stu-id="274c2-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="274c2-252">**向外缩放发送队列长度**</span><span class="sxs-lookup"><span data-stu-id="274c2-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="274c2-253">这些计数器测量的新增功能的详细信息，请参阅[采用 Azure Service Bus 的 SignalR 扩展](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="274c2-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="274c2-254">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="274c2-254">Using other performance counters</span></span>

<span data-ttu-id="274c2-255">以下性能计数器也可能是用于监视应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="274c2-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="274c2-256">**Memory**</span><span class="sxs-lookup"><span data-stu-id="274c2-256">**Memory**</span></span>

- <span data-ttu-id="274c2-257">.NET CLR 内存\\所有堆 （对于 w3wp) 中的 # 字节</span><span class="sxs-lookup"><span data-stu-id="274c2-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="274c2-258">**ASP.NET 2.0**</span><span class="sxs-lookup"><span data-stu-id="274c2-258">**ASP.NET**</span></span>

- <span data-ttu-id="274c2-259">ASP.NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="274c2-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="274c2-260">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="274c2-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="274c2-261">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="274c2-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="274c2-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="274c2-262">**CPU**</span></span>

- <span data-ttu-id="274c2-263">处理器 Information\Processor 时间</span><span class="sxs-lookup"><span data-stu-id="274c2-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="274c2-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="274c2-264">**TCP/IP**</span></span>

- <span data-ttu-id="274c2-265">TCPv6/已建立的连接</span><span class="sxs-lookup"><span data-stu-id="274c2-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="274c2-266">TCPv4/已建立的连接</span><span class="sxs-lookup"><span data-stu-id="274c2-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="274c2-267">**Web 服务**</span><span class="sxs-lookup"><span data-stu-id="274c2-267">**Web Service**</span></span>

- <span data-ttu-id="274c2-268">Web Service\Current Connections</span><span class="sxs-lookup"><span data-stu-id="274c2-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="274c2-269">Web Service\Maximum 连接</span><span class="sxs-lookup"><span data-stu-id="274c2-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="274c2-270">**线程处理**</span><span class="sxs-lookup"><span data-stu-id="274c2-270">**Threading**</span></span>

- <span data-ttu-id="274c2-271">.NET CLR 锁定和线程\\的当前逻辑线程数</span><span class="sxs-lookup"><span data-stu-id="274c2-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="274c2-272">.NET CLR 锁定和线程\\的当前物理线程数</span><span class="sxs-lookup"><span data-stu-id="274c2-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="274c2-273">其他资源</span><span class="sxs-lookup"><span data-stu-id="274c2-273">Other Resources</span></span>

<span data-ttu-id="274c2-274">ASP.NET 性能监视和优化的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="274c2-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="274c2-275">[ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="274c2-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="274c2-276">在 IIS 7.5、 IIS 7.0 中和 IIS 6.0 上的 ASP.NET 线程使用情况</span><span class="sxs-lookup"><span data-stu-id="274c2-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="274c2-277">&lt;applicationPool&gt;元素 （Web 设置）</span><span class="sxs-lookup"><span data-stu-id="274c2-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
