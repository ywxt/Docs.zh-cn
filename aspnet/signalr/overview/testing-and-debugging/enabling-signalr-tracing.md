---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: "启用 SignalR 跟踪 |Microsoft 文档"
author: tfitzmac
description: "本文档介绍如何启用和配置对 SignalR 服务器和客户端的跟踪。 跟踪可用于查看有关事件的诊断信息..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/08/2014
ms.topic: article
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: ac979acf162084a195bb769f842e77ad2498c7f3
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="enabling-signalr-tracing"></a><span data-ttu-id="02f99-104">启用 SignalR 跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-104">Enabling SignalR Tracing</span></span>
====================
<span data-ttu-id="02f99-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="02f99-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="02f99-106">本文档介绍如何启用和配置对 SignalR 服务器和客户端的跟踪。</span><span class="sxs-lookup"><span data-stu-id="02f99-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="02f99-107">跟踪可用于 SignalR 应用程序中查看有关事件的诊断信息。</span><span class="sxs-lookup"><span data-stu-id="02f99-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
> 
> <span data-ttu-id="02f99-108">本主题最初由 Patrick Fletcher 编写。</span><span class="sxs-lookup"><span data-stu-id="02f99-108">This topic was originally written by Patrick Fletcher.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="02f99-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="02f99-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="02f99-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="02f99-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="02f99-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="02f99-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="02f99-112">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="02f99-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="02f99-113">问题和意见</span><span class="sxs-lookup"><span data-stu-id="02f99-113">Questions and comments</span></span>
> 
> <span data-ttu-id="02f99-114">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="02f99-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="02f99-115">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="02f99-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="02f99-116">启用跟踪后，SignalR 应用程序创建事件日志的条目。</span><span class="sxs-lookup"><span data-stu-id="02f99-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="02f99-117">你可以从客户端和服务器登录事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="02f99-118">跟踪对服务器日志连接、 向外扩展提供程序和消息总线事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="02f99-119">跟踪客户端日志连接事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="02f99-120">SignalR 2.1 及更高版本，客户端上的跟踪记录中心调用消息的全部内容。</span><span class="sxs-lookup"><span data-stu-id="02f99-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="02f99-121">内容</span><span class="sxs-lookup"><span data-stu-id="02f99-121">Contents</span></span>

- [<span data-ttu-id="02f99-122">在服务器上启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="02f99-123">服务器事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="02f99-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="02f99-124">服务器事件记录到事件日志</span><span class="sxs-lookup"><span data-stu-id="02f99-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="02f99-125">在.NET 客户端 （仅限 Windows 桌面应用） 中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="02f99-126">桌面客户端事件记录到控制台</span><span class="sxs-lookup"><span data-stu-id="02f99-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="02f99-127">桌面客户端事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="02f99-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="02f99-128">在 Windows Phone 8 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="02f99-129">Windows Phone 客户端事件记录到 UI</span><span class="sxs-lookup"><span data-stu-id="02f99-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="02f99-130">Windows Phone 客户端事件记录到调试控制台</span><span class="sxs-lookup"><span data-stu-id="02f99-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="02f99-131">在 JavaScript 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="02f99-132">在服务器上启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-132">Enabling tracing on the server</span></span>

<span data-ttu-id="02f99-133">启用应用程序的配置文件 （App.config 或 Web.config，具体取决于项目的类型。） 中的服务器的跟踪你指定要记录的事件的类别。</span><span class="sxs-lookup"><span data-stu-id="02f99-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="02f99-134">在配置文件中，你还指定是否事件记录到文本文件、 Windows 事件日志中或使用的实现一个自定义日志[TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="02f99-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="02f99-135">服务器事件类别包括以下类型的消息：</span><span class="sxs-lookup"><span data-stu-id="02f99-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="02f99-136">源</span><span class="sxs-lookup"><span data-stu-id="02f99-136">Source</span></span> | <span data-ttu-id="02f99-137">消息</span><span class="sxs-lookup"><span data-stu-id="02f99-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="02f99-138">SignalR.SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="02f99-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="02f99-139">SQL 消息总线向外扩展提供程序安装程序、 数据库操作、 错误和超时事件</span><span class="sxs-lookup"><span data-stu-id="02f99-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="02f99-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="02f99-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="02f99-141">服务总线向外扩展提供程序主题创建和订阅、 错误和消息事件</span><span class="sxs-lookup"><span data-stu-id="02f99-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="02f99-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="02f99-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="02f99-143">Redis 向外扩展提供程序连接、 断开连接和错误事件</span><span class="sxs-lookup"><span data-stu-id="02f99-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="02f99-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="02f99-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="02f99-145">向外扩展消息事件</span><span class="sxs-lookup"><span data-stu-id="02f99-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="02f99-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="02f99-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="02f99-147">WebSocket 传输连接、 断开连接、 消息和错误事件</span><span class="sxs-lookup"><span data-stu-id="02f99-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="02f99-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="02f99-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="02f99-149">ServerSentEvents 传输连接、 断开连接、 消息和错误事件</span><span class="sxs-lookup"><span data-stu-id="02f99-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="02f99-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="02f99-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="02f99-151">ForeverFrame 传输连接、 断开连接、 消息和错误事件</span><span class="sxs-lookup"><span data-stu-id="02f99-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="02f99-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="02f99-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="02f99-153">LongPolling 传输连接、 断开连接、 消息和错误事件</span><span class="sxs-lookup"><span data-stu-id="02f99-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="02f99-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="02f99-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="02f99-155">传输连接、 断开连接和 keepalive 事件</span><span class="sxs-lookup"><span data-stu-id="02f99-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="02f99-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="02f99-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="02f99-157">中心发现事件</span><span class="sxs-lookup"><span data-stu-id="02f99-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="02f99-158">服务器事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="02f99-158">Logging server events to text files</span></span>

<span data-ttu-id="02f99-159">下面的代码演示如何启用跟踪每个类别的事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="02f99-160">此示例将配置应用程序事件记录到文本文件。</span><span class="sxs-lookup"><span data-stu-id="02f99-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="02f99-161">**启用跟踪的 XML 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="02f99-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="02f99-162">在上面的代码，`SignalRSwitch`条目指定[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx)用于发送到指定的日志的事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="02f99-163">在这种情况下，设置为`Verbose`这意味着所有的调试和跟踪消息记录。</span><span class="sxs-lookup"><span data-stu-id="02f99-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="02f99-164">下面的输出显示的条目`transports.log.txt`使用上面的配置文件的应用程序的文件。</span><span class="sxs-lookup"><span data-stu-id="02f99-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="02f99-165">显示一个新连接、 已删除的连接和传输检测信号事件。</span><span class="sxs-lookup"><span data-stu-id="02f99-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="02f99-166">服务器事件记录到事件日志</span><span class="sxs-lookup"><span data-stu-id="02f99-166">Logging server events to the event log</span></span>

<span data-ttu-id="02f99-167">若要事件记录到事件日志，而不是一个文本文件，将更改中的条目的值`sharedListeners`节点。</span><span class="sxs-lookup"><span data-stu-id="02f99-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="02f99-168">下面的代码演示如何服务器事件记录到事件日志：</span><span class="sxs-lookup"><span data-stu-id="02f99-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="02f99-169">**XML 用于日志记录事件写入事件日志的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="02f99-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="02f99-170">事件记录在应用程序日志中，并且可通过事件查看器中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="02f99-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![显示 SignalR 日志的事件查看器](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="02f99-172">在使用事件日志时，设置**TraceLevel**到**错误**需要可管理的消息数。</span><span class="sxs-lookup"><span data-stu-id="02f99-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="02f99-173">在.NET 客户端 （仅限 Windows 桌面应用） 中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="02f99-174">.NET 客户端控制台中，一个文本文件，或使用的实现自定义日志可以记录事件[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)。</span><span class="sxs-lookup"><span data-stu-id="02f99-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="02f99-175">若要启用日志记录在.NET 客户端中，设置连接的`TraceLevel`属性[TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx)值，与`TraceWriter`到有效的属性[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)实例。</span><span class="sxs-lookup"><span data-stu-id="02f99-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="02f99-176">桌面客户端事件记录到控制台</span><span class="sxs-lookup"><span data-stu-id="02f99-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="02f99-177">下面的 C# 代码演示如何在.NET 客户端到控制台中记录事件：</span><span class="sxs-lookup"><span data-stu-id="02f99-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="02f99-178">桌面客户端事件记录到文本文件</span><span class="sxs-lookup"><span data-stu-id="02f99-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="02f99-179">下面的 C# 代码演示如何在.NET 客户端到文本文件中记录事件：</span><span class="sxs-lookup"><span data-stu-id="02f99-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="02f99-180">下面的输出显示的条目`ClientLog.txt`使用上面的配置文件的应用程序的文件。</span><span class="sxs-lookup"><span data-stu-id="02f99-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="02f99-181">它显示客户端将连接到服务器，并调用客户端方法的中心调用`addMessage`:</span><span class="sxs-lookup"><span data-stu-id="02f99-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="02f99-182">在 Windows Phone 8 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="02f99-183">对于 Windows Phone 应用程序的 SignalR 应用程序使用相同的.NET 客户端作为桌面应用，但[Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)和写入的文件[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)不可用。</span><span class="sxs-lookup"><span data-stu-id="02f99-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="02f99-184">相反，你需要创建的自定义实现[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)跟踪。</span><span class="sxs-lookup"><span data-stu-id="02f99-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span> 

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="02f99-185">Windows Phone 客户端事件记录到 UI</span><span class="sxs-lookup"><span data-stu-id="02f99-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="02f99-186">[SignalR 基本代码](https://github.com/SignalR/SignalR/archive/master.zip)包括将跟踪输出写入一个 Windows Phone 示例[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)使用自定义[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)实现调用`TextBlockWriter`。</span><span class="sxs-lookup"><span data-stu-id="02f99-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="02f99-187">此类可在**samples/Microsoft.AspNet.SignalR.Client.WP8.Samples**项目。</span><span class="sxs-lookup"><span data-stu-id="02f99-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="02f99-188">创建的实例时`TextBlockWriter`，在当前传递[SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)，和一个[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)其中它将创建[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)要用于跟踪输出：</span><span class="sxs-lookup"><span data-stu-id="02f99-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="02f99-189">然后将将跟踪输出写入到新[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx)中创建[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中传递：</span><span class="sxs-lookup"><span data-stu-id="02f99-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="02f99-190">Windows Phone 客户端事件记录到调试控制台</span><span class="sxs-lookup"><span data-stu-id="02f99-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="02f99-191">若要将输出发送到调试控制台而不是 UI 中，创建的实现[TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) ，写入调试窗口中，并将其分配给连接的[TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx)属性：</span><span class="sxs-lookup"><span data-stu-id="02f99-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="02f99-192">然后将跟踪信息写入 Visual Studio 中的调试窗口：</span><span class="sxs-lookup"><span data-stu-id="02f99-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="02f99-193">在 JavaScript 客户端中启用跟踪</span><span class="sxs-lookup"><span data-stu-id="02f99-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="02f99-194">若要启用客户端日志记录在连接上，设置`logging`属性上的连接对象，然后才能调用`start`方法，以建立连接。</span><span class="sxs-lookup"><span data-stu-id="02f99-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="02f99-195">**客户端 JavaScript 代码来启用跟踪到浏览器控制台 （的生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="02f99-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="02f99-196">**客户端 JavaScript 代码来启用跟踪到浏览器控制台 （而无需生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="02f99-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="02f99-197">当启用了跟踪时，JavaScript 客户端会将事件记录到浏览器控制台中。</span><span class="sxs-lookup"><span data-stu-id="02f99-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="02f99-198">若要访问浏览器控制台，请参阅[监视传输](../getting-started/introduction-to-signalr.md#MonitoringTransports)。</span><span class="sxs-lookup"><span data-stu-id="02f99-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="02f99-199">下面的屏幕截图显示 SignalR JavaScript 客户端使用启用的跟踪。</span><span class="sxs-lookup"><span data-stu-id="02f99-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="02f99-200">它显示浏览器控制台中的连接和中心调用事件：</span><span class="sxs-lookup"><span data-stu-id="02f99-200">It shows connection and hub invocation events in the browser console:</span></span>

![在浏览器控制台中的 SignalR 跟踪事件](enabling-signalr-tracing/_static/image4.png)
