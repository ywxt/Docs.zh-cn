---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 中心 API 指南-.NET 客户端 (SignalR 1.x) |Microsoft 文档
author: pfletcher
description: 本文档提供使用 SignalR 在.NET 客户端，如 Windows 应用商店 (WinRT)、 WPF、 Silverlight 和 cons 版本 2 的中心 API 的说明...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/17/2013
ms.topic: article
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 9a61bd255a217876aa2fdbeb6389539483b9f013
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28037475"
---
<a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="cb016-103">ASP.NET SignalR 中心 API 指南-.NET 客户端 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="cb016-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>
====================
<span data-ttu-id="cb016-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="cb016-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="cb016-105">本文档提供使用 SignalR 在.NET 客户端，例如 Windows 应用商店 (WinRT)、 WPF、 Silverlight 和控制台应用程序中的版本 2 的中心 API 的简介。</span><span class="sxs-lookup"><span data-stu-id="cb016-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="cb016-106">SignalR 中心 API 使您能够远程过程调用 (Rpc) 从连接的客户端到服务器和客户端到服务器。</span><span class="sxs-lookup"><span data-stu-id="cb016-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="cb016-107">在服务器代码中，你定义可以由客户端，调用的方法和调用客户端运行的方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="cb016-108">在客户端代码中，定义在服务器上，可以调用的方法，并调用在服务器运行的方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="cb016-109">SignalR 将负责为你的客户端到服务器管道的所有。</span><span class="sxs-lookup"><span data-stu-id="cb016-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="cb016-110">SignalR 还提供了一个称为永久连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="cb016-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="cb016-111">简介 SignalR、 集线器和永久连接，或者有关演示如何生成完整的 SignalR 应用程序的教程，请参阅[SignalR-入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="cb016-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>


## <a name="overview"></a><span data-ttu-id="cb016-112">概述</span><span class="sxs-lookup"><span data-stu-id="cb016-112">Overview</span></span>

<span data-ttu-id="cb016-113">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="cb016-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="cb016-114">客户端安装程序</span><span class="sxs-lookup"><span data-stu-id="cb016-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="cb016-115">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="cb016-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="cb016-116">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="cb016-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="cb016-117">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="cb016-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="cb016-118">如何在 WPF 客户端中设置的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="cb016-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="cb016-119">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="cb016-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="cb016-120">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="cb016-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="cb016-121">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="cb016-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="cb016-122">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="cb016-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="cb016-123">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="cb016-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="cb016-124">如何在该服务器可以调用的客户端上定义方法</span><span class="sxs-lookup"><span data-stu-id="cb016-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="cb016-125">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="cb016-126">具有指定参数类型的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="cb016-127">使用指定的参数的动态对象的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="cb016-128">如何移除处理程序</span><span class="sxs-lookup"><span data-stu-id="cb016-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="cb016-129">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="cb016-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="cb016-130">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="cb016-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="cb016-131">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="cb016-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="cb016-132">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="cb016-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="cb016-133">WPF、 Silverlight 和控制台应用程序的代码示例，该服务器可以调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="cb016-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="cb016-134">有关示例.NET 客户端项目，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="cb016-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="cb016-135">[gustavo armenta / SignalR 示例](https://github.com/gustavo-armenta/SignalR-Samples)GitHub.com （WinRT、 Silverlight，控制台应用程序示例） 上。</span><span class="sxs-lookup"><span data-stu-id="cb016-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="cb016-136">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) GitHub.com （WPF 示例） 上。</span><span class="sxs-lookup"><span data-stu-id="cb016-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="cb016-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) GitHub.com （控制台应用程序示例） 上。</span><span class="sxs-lookup"><span data-stu-id="cb016-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="cb016-138">有关如何进行编程的服务器或 JavaScript 客户端的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="cb016-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="cb016-139">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="cb016-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="cb016-140">SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="cb016-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="cb016-141">API 参考主题的链接将指向 API 的.NET 4.5 版本。</span><span class="sxs-lookup"><span data-stu-id="cb016-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="cb016-142">如果你使用.NET 4，请参阅[API 主题的.NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb016-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="cb016-143">客户端安装程序</span><span class="sxs-lookup"><span data-stu-id="cb016-143">Client setup</span></span>

<span data-ttu-id="cb016-144">安装[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 包 (不[Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包)。</span><span class="sxs-lookup"><span data-stu-id="cb016-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="cb016-145">此包支持的.NET 4 和.NET 4.5 WinRT、 Silverlight、 WPF、 控制台应用程序和 Windows Phone 客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="cb016-146">如果对客户端的 SignalR 的版本必须在服务器的版本不同，SignalR 通常是能够适应差异。</span><span class="sxs-lookup"><span data-stu-id="cb016-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="cb016-147">例如，当发布 SignalR 2.0 版并在服务器上安装的服务器将支持具有 1.1.x 以及安装了 2.0 的客户端安装的客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="cb016-148">如果服务器上的版本和客户端上的版本之间的差异太高，将引发 SignalR`InvalidOperationException`客户端尝试建立连接时出现异常。</span><span class="sxs-lookup"><span data-stu-id="cb016-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="cb016-149">错误消息为"`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"。</span><span class="sxs-lookup"><span data-stu-id="cb016-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="cb016-150">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="cb016-150">How to establish a connection</span></span>

<span data-ttu-id="cb016-151">你可以建立连接之前，你必须创建`HubConnection`对象，并创建代理。</span><span class="sxs-lookup"><span data-stu-id="cb016-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="cb016-152">若要建立连接，请调用`Start`方法`HubConnection`对象。</span><span class="sxs-lookup"><span data-stu-id="cb016-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="cb016-153">对于 JavaScript 客户端必须注册至少一个事件处理程序之前调用`Start`方法，以建立连接。</span><span class="sxs-lookup"><span data-stu-id="cb016-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="cb016-154">这不是必需的.NET 客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="cb016-155">对于 JavaScript 客户端，生成的代理代码会自动创建为存在的所有中心的代理的服务器上，并注册处理程序是如何指示哪些中心你的客户端打算使用。</span><span class="sxs-lookup"><span data-stu-id="cb016-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="cb016-156">但是.NET 客户端您中心代理手动创建，因此 SignalR 假定，需要使用任何创建的代理的中心。</span><span class="sxs-lookup"><span data-stu-id="cb016-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="cb016-157">示例代码使用默认值"/ signalr"URL 以连接到你 SignalR 的服务。</span><span class="sxs-lookup"><span data-stu-id="cb016-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="cb016-158">有关如何指定不同的基 URL 的信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-/signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="cb016-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="cb016-159">`Start`方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="cb016-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="cb016-160">若要确保后面的代码行不执行直到建立连接后，使用`await`在 ASP.NET 4.5 异步方法或`.Wait()`中一种同步方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="cb016-161">不要使用`.Wait()`WinRT 客户端中。</span><span class="sxs-lookup"><span data-stu-id="cb016-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="cb016-162">`HubConnection` 类是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="cb016-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="cb016-163">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="cb016-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="cb016-164">有关如何启用从 Silverlight 客户端的跨域连接的信息，请参阅[服务跨域边界提供](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb016-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="cb016-165">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="cb016-165">How to configure the connection</span></span>

<span data-ttu-id="cb016-166">建立连接之前，你可以指定任何以下选项：</span><span class="sxs-lookup"><span data-stu-id="cb016-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="cb016-167">并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="cb016-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="cb016-168">查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="cb016-168">Query string parameters.</span></span>
- <span data-ttu-id="cb016-169">传输方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-169">The transport method.</span></span>
- <span data-ttu-id="cb016-170">HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="cb016-170">HTTP headers.</span></span>
- <span data-ttu-id="cb016-171">客户端证书。</span><span class="sxs-lookup"><span data-stu-id="cb016-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="cb016-172">如何在 WPF 客户端中设置的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="cb016-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="cb016-173">在 WPF 客户端，你可能需要增加从其默认值为 2 的并发连接的最大数目。</span><span class="sxs-lookup"><span data-stu-id="cb016-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="cb016-174">建议的值为 10。</span><span class="sxs-lookup"><span data-stu-id="cb016-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="cb016-175">有关详细信息，请参阅[ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb016-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="cb016-176">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="cb016-176">How to specify query string parameters</span></span>

<span data-ttu-id="cb016-177">如果你想要将数据发送到服务器，当客户端连接时，你可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="cb016-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="cb016-178">下面的示例演示如何在客户端代码中设置的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="cb016-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="cb016-179">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="cb016-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="cb016-180">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="cb016-180">How to specify the transport method</span></span>

<span data-ttu-id="cb016-181">作为连接的过程的一部分，SignalR 客户端通常与服务器协商来确定支持的最佳传输由服务器和客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="cb016-182">如果你已经知道你想要使用的传输，你可以绕过此协商过程。</span><span class="sxs-lookup"><span data-stu-id="cb016-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="cb016-183">若要指定的传输方法，传入传输对象指向 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="cb016-184">下面的示例演示如何在客户端代码中指定的传输方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="cb016-185">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包括可用于指定的传输的以下类。</span><span class="sxs-lookup"><span data-stu-id="cb016-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="cb016-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="cb016-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="cb016-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="cb016-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="cb016-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （可用仅当服务器和客户端使用.NET 4.5。）</span><span class="sxs-lookup"><span data-stu-id="cb016-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="cb016-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （会自动选择支持的客户端和服务器的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="cb016-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="cb016-190">这是默认传输。</span><span class="sxs-lookup"><span data-stu-id="cb016-190">This is the default transport.</span></span> <span data-ttu-id="cb016-191">通过此到`Start`方法具有相同的效果不传递任何内容。)</span><span class="sxs-lookup"><span data-stu-id="cb016-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="cb016-192">此列表中不包括 ForeverFrame 传输，因为它仅由浏览器使用。</span><span class="sxs-lookup"><span data-stu-id="cb016-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="cb016-193">有关如何检查在服务器代码中的传输方法的信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-如何从上下文属性中获取有关客户端的信息](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="cb016-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="cb016-194">有关传输和回退机制的详细信息，请参阅[简介 SignalR 的传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="cb016-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="cb016-195">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="cb016-195">How to specify HTTP headers</span></span>

<span data-ttu-id="cb016-196">若要设置 HTTP 标头，使用`Headers`连接对象上的属性。</span><span class="sxs-lookup"><span data-stu-id="cb016-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="cb016-197">下面的示例演示如何添加一个 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="cb016-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="cb016-198">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="cb016-198">How to specify client certificates</span></span>

<span data-ttu-id="cb016-199">若要添加客户端证书，请使用`AddClientCertificate`连接对象上的方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="cb016-200">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="cb016-200">How to create the Hub proxy</span></span>

<span data-ttu-id="cb016-201">为了从服务器中，可以调用一个中心的客户端上定义方法，并调用在服务器上的集线器上的方法，通过调用创建的中心代理`CreateHubProxy`连接对象上。</span><span class="sxs-lookup"><span data-stu-id="cb016-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="cb016-202">字符串在传入到`CreateHubProxy`是你的中心类的名称或指定的名称`HubName`属性如果其中一个已在服务器上使用。</span><span class="sxs-lookup"><span data-stu-id="cb016-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="cb016-203">名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="cb016-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="cb016-204">**在服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="cb016-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="cb016-205">**创建中心类用于客户端代理**</span><span class="sxs-lookup"><span data-stu-id="cb016-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="cb016-206">如果修饰你中心类`HubName`特性，请使用该名称。</span><span class="sxs-lookup"><span data-stu-id="cb016-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="cb016-207">**在服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="cb016-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="cb016-208">**创建中心类用于客户端代理**</span><span class="sxs-lookup"><span data-stu-id="cb016-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="cb016-209">代理对象是线程安全的。</span><span class="sxs-lookup"><span data-stu-id="cb016-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="cb016-210">事实上，如果你调用`HubConnection.CreateHubProxy`多次具有相同`hubName`，获取相同的缓存`IHubProxy`对象。</span><span class="sxs-lookup"><span data-stu-id="cb016-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="cb016-211">如何在该服务器可以调用的客户端上定义方法</span><span class="sxs-lookup"><span data-stu-id="cb016-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="cb016-212">若要定义该服务器可以调用一个方法，使用代理服务器的`On`方法以注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="cb016-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="cb016-213">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="cb016-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="cb016-214">例如，`Clients.All.UpdateStockPrice`在服务器上将执行`updateStockPrice`， `updatestockprice`，或`UpdateStockPrice`客户端上。</span><span class="sxs-lookup"><span data-stu-id="cb016-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="cb016-215">不同的客户端平台都具有不同的要求，有关如何编写方法的代码以更新 UI。</span><span class="sxs-lookup"><span data-stu-id="cb016-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="cb016-216">所示的示例适用于 WinRT (Windows 应用商店.NET) 客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="cb016-217">中提供了 WPF、 Silverlight 和控制台应用程序示例[本主题中后面的一个单独的段](#wpfsl)。</span><span class="sxs-lookup"><span data-stu-id="cb016-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="cb016-218">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-218">Methods without parameters</span></span>

<span data-ttu-id="cb016-219">如果要处理的方法没有参数，使用的非泛型重载`On`方法：</span><span class="sxs-lookup"><span data-stu-id="cb016-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="cb016-220">**服务器代码调用不带参数的客户端方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="cb016-221">**方法的 WinRT 客户端代码调用不带参数的服务器 ([请参阅本主题中的更高版本的 WPF 和 Silverlight 示例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="cb016-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="cb016-222">具有指定参数类型的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="cb016-223">如果正在处理该方法具有参数，指定的参数类型作为泛型类型的`On`方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="cb016-224">存在一些泛型重载`On`方法，以使您可以指定最多 8 个参数 (在 Windows Phone 7 上的 4)。</span><span class="sxs-lookup"><span data-stu-id="cb016-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="cb016-225">在以下示例中，一个参数发送到`UpdateStockPrice`方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="cb016-226">**服务器代码调用带有参数的客户端方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="cb016-227">**用于参数 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="cb016-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="cb016-228">**服务器与一个参数调用的方法的 WinRT 客户端代码 ([请参阅本主题中的更高版本的 WPF 和 Silverlight 示例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="cb016-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="cb016-229">使用指定的参数的动态对象的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="cb016-230">作为泛型类型的指定参数的替代方法`On`方法，你可以指定参数作为动态对象：</span><span class="sxs-lookup"><span data-stu-id="cb016-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="cb016-231">**服务器代码调用带有参数的客户端方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="cb016-232">**用于参数 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="cb016-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="cb016-233">**服务器与一个参数，参数中使用的动态对象调用方法的 WinRT 客户端代码 ([请参阅本主题中的更高版本的 WPF 和 Silverlight 示例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="cb016-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="cb016-234">如何移除处理程序</span><span class="sxs-lookup"><span data-stu-id="cb016-234">How to remove a handler</span></span>

<span data-ttu-id="cb016-235">若要移除处理程序，调用其`Dispose`方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="cb016-236">**从服务器调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="cb016-237">**客户端代码将处理程序移除**</span><span class="sxs-lookup"><span data-stu-id="cb016-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="cb016-238">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="cb016-238">How to call server methods from the client</span></span>

<span data-ttu-id="cb016-239">若要在服务器上调用方法，使用`Invoke`中心代理上的方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="cb016-240">如果服务器方法没有返回值，使用的非泛型重载`Invoke`方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="cb016-241">**服务器代码的方法没有返回值**</span><span class="sxs-lookup"><span data-stu-id="cb016-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="cb016-242">**客户端代码调用没有返回值的方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="cb016-243">如果服务器方法具有一个返回值，指定的返回类型的泛型类型作为`Invoke`方法。</span><span class="sxs-lookup"><span data-stu-id="cb016-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="cb016-244">**服务器代码具有一个返回值并采用复杂类型参数的方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="cb016-245">**使用参数和返回值的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="cb016-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="cb016-246">**客户端代码调用方法，它具有一个返回值并采用 ASP.NET 4.5 的异步方法中的复杂类型参数，**</span><span class="sxs-lookup"><span data-stu-id="cb016-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="cb016-247">**客户端代码调用方法，它具有一个返回值并采用一种同步方法中的复杂类型参数，**</span><span class="sxs-lookup"><span data-stu-id="cb016-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="cb016-248">`Invoke`方法以异步方式执行，并返回`Task`对象。</span><span class="sxs-lookup"><span data-stu-id="cb016-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="cb016-249">如果没有指定`await`或`.Wait()`下, 一行代码将执行之前调用的方法执行完毕。</span><span class="sxs-lookup"><span data-stu-id="cb016-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="cb016-250">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="cb016-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="cb016-251">SignalR 提供以下连接可以处理的生存期事件：</span><span class="sxs-lookup"><span data-stu-id="cb016-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="cb016-252">`Received`： 引发时的连接上收到任何数据。</span><span class="sxs-lookup"><span data-stu-id="cb016-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="cb016-253">提供接收到的数据。</span><span class="sxs-lookup"><span data-stu-id="cb016-253">Provides the received data.</span></span>
- <span data-ttu-id="cb016-254">`ConnectionSlow`： 当客户端检测到慢速或经常删除连接时引发。</span><span class="sxs-lookup"><span data-stu-id="cb016-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="cb016-255">`Reconnecting`： 基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="cb016-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="cb016-256">`Reconnected`： 基础传输已重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="cb016-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="cb016-257">`StateChanged`： 在连接状态更改时引发。</span><span class="sxs-lookup"><span data-stu-id="cb016-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="cb016-258">提供的旧状态和新的状态。</span><span class="sxs-lookup"><span data-stu-id="cb016-258">Provides the old state and the new state.</span></span> <span data-ttu-id="cb016-259">有关连接状态的值请参阅[ConnectionState 枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="cb016-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="cb016-260">`Closed`： 连接已断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="cb016-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="cb016-261">例如，如果你想要显示的错误的不严重，但会导致间歇性连接问题的警告消息，如缓慢或频繁删除的连接，处理`ConnectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="cb016-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="cb016-262">有关详细信息，请参阅[了解和处理连接生存期中事件的 SignalR](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="cb016-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="cb016-263">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="cb016-263">How to handle errors</span></span>

<span data-ttu-id="cb016-264">如果未显式启用服务器上的详细的错误消息，在出错后返回 SignalR 的异常对象包含有关错误的极少信息。</span><span class="sxs-lookup"><span data-stu-id="cb016-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="cb016-265">例如，如果调用`newContosoChatMessage`失败，错误对象中的错误消息包含"`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`"发送到在生产环境中的客户端的详细的错误消息不建议出于安全原因，但如果你想要启用详细的错误消息疑难解答的目的，在服务器上使用下面的代码。</span><span class="sxs-lookup"><span data-stu-id="cb016-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="cb016-266">若要处理 SignalR 引发的错误，你可以添加的处理程序`Error`连接对象上的事件。</span><span class="sxs-lookup"><span data-stu-id="cb016-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="cb016-267">若要处理方法调用中的错误，请在 try catch 块中包装代码。</span><span class="sxs-lookup"><span data-stu-id="cb016-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="cb016-268">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="cb016-268">How to enable client-side logging</span></span>

<span data-ttu-id="cb016-269">若要启用客户端日志记录，将设置`TraceLevel`和`TraceWriter`连接对象上的属性。</span><span class="sxs-lookup"><span data-stu-id="cb016-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="cb016-270">WPF、 Silverlight 和控制台应用程序的代码示例，该服务器可以调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="cb016-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="cb016-271">用于定义该服务器可以调用的客户端方法的前面所示的代码示例适用于 WinRT 客户端。</span><span class="sxs-lookup"><span data-stu-id="cb016-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="cb016-272">下面的示例演示为 WPF、 Silverlight 和控制台应用程序客户端的等效代码。</span><span class="sxs-lookup"><span data-stu-id="cb016-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="cb016-273">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-273">Methods without parameters</span></span>

<span data-ttu-id="cb016-274">**不带参数的服务器从调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="cb016-275">**不带参数的服务器从调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="cb016-276">**从服务器不带参数调用方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="cb016-277">具有指定参数类型的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="cb016-278">**服务器与一个参数调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="cb016-279">**Silverlight 客户端代码来调用服务器与一个参数的方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="cb016-280">**控制台应用程序服务器与一个参数调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="cb016-281">使用指定的参数的动态对象的参数的方法</span><span class="sxs-lookup"><span data-stu-id="cb016-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="cb016-282">**服务器与一个参数，使用动态对象参数进行调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="cb016-283">**Silverlight 客户端代码来调用服务器与一个参数，参数中使用的动态对象的方法**</span><span class="sxs-lookup"><span data-stu-id="cb016-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="cb016-284">**控制台应用程序服务器与一个参数，使用动态对象参数进行调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cb016-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
