---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: "ASP.NET SignalR 中心 API 指南-服务器 (C#) |Microsoft 文档"
author: pfletcher
description: "本文档介绍了使用代码示例演示为 SignalR 版本 2，编程 ASP.NET SignalR 中心 API 的服务器端..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c2567d4d39a494daf77a23db5dff83c8fae4925d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="d8ecf-103">ASP.NET SignalR 中心 API 指南-服务器 (C#)</span><span class="sxs-lookup"><span data-stu-id="d8ecf-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>
====================
<span data-ttu-id="d8ecf-104">通过[Patrick Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d8ecf-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="d8ecf-105">本文档提供使用代码示例演示常见的选项为 SignalR 版本 2，编程 ASP.NET SignalR 中心 API 的服务器端的简介。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="d8ecf-106">SignalR 中心 API 使您能够远程过程调用 (Rpc) 从连接的客户端到服务器和客户端到服务器。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d8ecf-107">在服务器代码中，你定义可以由客户端，调用的方法和调用客户端运行的方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d8ecf-108">在客户端代码中，定义在服务器上，可以调用的方法，并调用在服务器运行的方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d8ecf-109">SignalR 将负责为你的客户端到服务器管道的所有。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="d8ecf-110">SignalR 还提供了一个称为永久连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d8ecf-111">有关 SignalR、 集线器和永久连接的介绍，请参阅[简介 SignalR 2](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d8ecf-112">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="d8ecf-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="d8ecf-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d8ecf-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="d8ecf-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d8ecf-114">.NET 4.5</span></span>
> - <span data-ttu-id="d8ecf-115">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="d8ecf-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="d8ecf-116">主题版本</span><span class="sxs-lookup"><span data-stu-id="d8ecf-116">Topic versions</span></span>
> 
> <span data-ttu-id="d8ecf-117">有关 SignalR 的早期版本的信息，请参阅[SignalR 较旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="d8ecf-118">问题和意见</span><span class="sxs-lookup"><span data-stu-id="d8ecf-118">Questions and comments</span></span>
> 
> <span data-ttu-id="d8ecf-119">请留下反馈上如何喜欢本教程的方式，我们可以提高在页面底部的注释中。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d8ecf-120">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="d8ecf-121">概述</span><span class="sxs-lookup"><span data-stu-id="d8ecf-121">Overview</span></span>

<span data-ttu-id="d8ecf-122">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="d8ecf-123">如何注册 SignalR 中间件</span><span class="sxs-lookup"><span data-stu-id="d8ecf-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="d8ecf-124">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="d8ecf-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="d8ecf-125">配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="d8ecf-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="d8ecf-126">如何创建和使用 Hub 类</span><span class="sxs-lookup"><span data-stu-id="d8ecf-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="d8ecf-127">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="d8ecf-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="d8ecf-128">混合使用大小写的 JavaScript 客户端中的中心名称</span><span class="sxs-lookup"><span data-stu-id="d8ecf-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="d8ecf-129">多个中心</span><span class="sxs-lookup"><span data-stu-id="d8ecf-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="d8ecf-130">强类型中心</span><span class="sxs-lookup"><span data-stu-id="d8ecf-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="d8ecf-131">如何在客户端可以调用的中心类中定义方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="d8ecf-132">混合使用大小写的 JavaScript 客户端中的方法名称</span><span class="sxs-lookup"><span data-stu-id="d8ecf-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="d8ecf-133">当以异步方式执行</span><span class="sxs-lookup"><span data-stu-id="d8ecf-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="d8ecf-134">定义重载</span><span class="sxs-lookup"><span data-stu-id="d8ecf-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="d8ecf-135">报告从中心方法调用的进度</span><span class="sxs-lookup"><span data-stu-id="d8ecf-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="d8ecf-136">如何从中心类方法调用客户端</span><span class="sxs-lookup"><span data-stu-id="d8ecf-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="d8ecf-137">选择哪些客户端将接收 RPC</span><span class="sxs-lookup"><span data-stu-id="d8ecf-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="d8ecf-138">方法名称没有编译时验证</span><span class="sxs-lookup"><span data-stu-id="d8ecf-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="d8ecf-139">不区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="d8ecf-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="d8ecf-140">异步执行</span><span class="sxs-lookup"><span data-stu-id="d8ecf-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="d8ecf-141">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="d8ecf-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="d8ecf-142">异步执行的 Add 和 Remove 方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="d8ecf-143">组成员身份持久性</span><span class="sxs-lookup"><span data-stu-id="d8ecf-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="d8ecf-144">单用户组</span><span class="sxs-lookup"><span data-stu-id="d8ecf-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="d8ecf-145">如何连接生存期中处理事件的中心类</span><span class="sxs-lookup"><span data-stu-id="d8ecf-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="d8ecf-146">当调用 OnConnected、 OnDisconnected 和 OnReconnected</span><span class="sxs-lookup"><span data-stu-id="d8ecf-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="d8ecf-147">不填充的调用方状态</span><span class="sxs-lookup"><span data-stu-id="d8ecf-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="d8ecf-148">如何从上下文属性中获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="d8ecf-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="d8ecf-149">如何将状态传递客户端和中心类之间</span><span class="sxs-lookup"><span data-stu-id="d8ecf-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="d8ecf-150">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="d8ecf-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="d8ecf-151">如何调用方法的客户端和管理从中心类外部的组</span><span class="sxs-lookup"><span data-stu-id="d8ecf-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="d8ecf-152">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="d8ecf-153">管理组成员资格</span><span class="sxs-lookup"><span data-stu-id="d8ecf-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="d8ecf-154">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="d8ecf-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="d8ecf-155">如何自定义中心管道</span><span class="sxs-lookup"><span data-stu-id="d8ecf-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="d8ecf-156">有关如何程序客户端的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="d8ecf-157">SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="d8ecf-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="d8ecf-158">SignalR 中心 API 指南-.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="d8ecf-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="d8ecf-159">SignalR 2 的服务器组件才.NET 4.5 中提供。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="d8ecf-160">运行.NET 4.0 的服务器必须使用 SignalR 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="d8ecf-161">如何注册 SignalR 中间件</span><span class="sxs-lookup"><span data-stu-id="d8ecf-161">How to register SignalR middleware</span></span>

<span data-ttu-id="d8ecf-162">若要定义的路由的客户端将用于连接到你的中心，调用`MapSignalR`应用程序启动时的方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="d8ecf-163">`MapSignalR`是[扩展方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)为`OwinExtensions`类。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="d8ecf-164">下面的示例演示如何定义使用 OWIN startup 类 SignalR 中心路由。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="d8ecf-165">如果你将 SignalR 功能添加到 ASP.NET MVC 应用程序，请确保在其他路由之前已添加的 SignalR 路由。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="d8ecf-166">有关详细信息，请参阅[教程： 开始使用 SignalR 2 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="d8ecf-167">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="d8ecf-167">The /signalr URL</span></span>

<span data-ttu-id="d8ecf-168">默认情况下，客户端将用于连接到你的中心路由 URL 是"/ signalr"。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="d8ecf-169">（不要将此 URL 以"/ signalr/中心"URL，即自动生成的 JavaScript 文件混淆。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="d8ecf-170">有关生成的代理的详细信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-生成的代理和它为您完成](hubs-api-guide-javascript-client.md#genproxy)。)</span><span class="sxs-lookup"><span data-stu-id="d8ecf-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="d8ecf-171">可能有特殊的情况下，它让 SignalR; 不能使用此基 URL例如，你有一个文件夹中名为的项目*signalr*并且你不想要更改的名称。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="d8ecf-172">在这种情况下，更改基 URL，如下面的示例中所示 (将"/ signalr"与你所需的 URL 的示例代码中)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="d8ecf-173">**指定的 URL 的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="d8ecf-174">**指定的 URL （与生成的代理） 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="d8ecf-175">**指定的 URL （无需生成的代理） 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="d8ecf-176">**指定的 URL 的.NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="d8ecf-177">配置 SignalR 选项</span><span class="sxs-lookup"><span data-stu-id="d8ecf-177">Configuring SignalR Options</span></span>

<span data-ttu-id="d8ecf-178">重载的`MapSignalR`方法使您能够指定的自定义 URL、 自定义的依赖项解析程序和以下选项：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="d8ecf-179">启用从浏览器客户端使用 CORS 或 JSONP 的跨域调用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="d8ecf-180">通常如果浏览器加载从页`http://contoso.com`，SignalR 连接处于同一域中，在`http://contoso.com/signalr`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="d8ecf-181">如果此页`http://contoso.com`建立连接`http://fabrikam.com/signalr`，即跨域连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="d8ecf-182">出于安全原因，默认情况下禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="d8ecf-183">有关详细信息，请参阅[ASP.NET SignalR 中心 API 指南-JavaScript 客户端-如何建立的跨域连接](hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="d8ecf-184">启用详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="d8ecf-185">发生错误时，SignalR 的默认行为是发送到客户端通知消息，而有关发生了什么情况的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="d8ecf-186">向客户端发送详细的错误信息不是建议在生产中，因为恶意用户可能能够使用攻击你的应用程序中的信息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="d8ecf-187">有关故障排除，可以使用此选项以暂时启用更详细的错误报告。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="d8ecf-188">禁用自动生成的 JavaScript 代理文件。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="d8ecf-189">默认情况下，以响应的 URL"/ signalr/中心"生成你的中心类与代理的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="d8ecf-190">如果不想使用 JavaScript 代理，或者如果你想要手动生成此文件并引用的物理文件中你的客户端，你可以使用此选项以禁用代理生成。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="d8ecf-191">有关详细信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-如何为 SignalR 创建物理文件生成代理](hubs-api-guide-javascript-client.md#manualproxy)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="d8ecf-192">下面的示例演示如何对的调用中指定的 SignalR 连接 URL 和这些选项`MapSignalR`方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="d8ecf-193">若要指定自定义 URL，将"/ signalr"在与你想要使用的 URL 的示例。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="d8ecf-194">如何创建和使用 Hub 类</span><span class="sxs-lookup"><span data-stu-id="d8ecf-194">How to create and use Hub classes</span></span>

<span data-ttu-id="d8ecf-195">若要创建一个中心，创建派生自的类[Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="d8ecf-196">下面的示例演示一个简单的中心类聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="d8ecf-197">在此示例中，连接的客户端可以调用`NewContosoChatMessage`方法，和时，收到的数据已将广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="d8ecf-198">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="d8ecf-198">Hub object lifetime</span></span>

<span data-ttu-id="d8ecf-199">未实例化中心类，或从服务器; 上代码中调用其方法来说，为你完成通过 SignalR 中心管道。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="d8ecf-200">SignalR 在每次它需要处理中心操作，例如当客户端连接、 断开连接，或向服务器发出调用的方法时创建中心类的新实例。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="d8ecf-201">因为中心类的实例是暂时的不能使用它们来维护到下一个方法调用中的状态。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="d8ecf-202">每次服务器接收方法调用从客户端，你的中心类进程的新实例的消息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="d8ecf-203">若要维护通过多个连接和方法调用的状态，使用如数据库或一个静态变量的其他某种方法上的中心类或不同类的不是派生自`Hub`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="d8ecf-204">如果您保留在内存中的数据，使用静态变量之类的方法上的中心类，数据将丢失当应用程序域进行回收时。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="d8ecf-205">如果你想要将消息发送到客户端，从你自己的中心类外部运行的代码，则不能通过实例化的中心类实例，但你可以执行此操作通过为您的中心类获取对 SignalR 上下文对象的引用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="d8ecf-206">有关详细信息，请参阅[如何调用方法的客户端和管理从中心类外部的组](#callfromoutsidehub)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="d8ecf-207">混合使用大小写的 JavaScript 客户端中的中心名称</span><span class="sxs-lookup"><span data-stu-id="d8ecf-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="d8ecf-208">默认情况下，JavaScript 客户端到中心通过使用类名称的混合使用大小写版本引用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="d8ecf-209">SignalR 自动使此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="d8ecf-210">前面的示例将称为`contosoChatHub`在 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="d8ecf-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="d8ecf-212">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="d8ecf-213">如果你想要指定客户端使用，添加另一个名称`HubName`属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="d8ecf-214">当你使用`HubName`属性，没有任何名称更改为 JavaScript 客户端上的 camel 大小写。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="d8ecf-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="d8ecf-216">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="d8ecf-217">多个中心</span><span class="sxs-lookup"><span data-stu-id="d8ecf-217">Multiple Hubs</span></span>

<span data-ttu-id="d8ecf-218">应用程序中，可以定义多个中心类。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="d8ecf-219">当你这样做时，共享的连接，但组是单独：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="d8ecf-220">所有客户端将使用相同的 URL 来建立与你的服务的 SignalR 连接 ("/ signalr"或如果你指定一个你自定义 URL)，并且所有中心使用连接的服务定义。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="d8ecf-221">与单个类中定义所有中心功能的多个中心没有性能差异。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="d8ecf-222">所有中心都获取相同的 HTTP 请求信息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="d8ecf-223">由于所有中心都共享相同的连接，服务器获取的唯一的 HTTP 请求信息是什么进入时建立 SignalR 连接的原始 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="d8ecf-224">如果你使用连接请求将信息从客户端传递到服务器，通过指定查询字符串，不能向不同的中心提供不同的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="d8ecf-225">所有中心将都收到相同的信息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="d8ecf-226">生成的 JavaScript 代理文件将包含在一个文件中的所有中心的代理。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="d8ecf-227">有关 JavaScript 代理的信息，请参阅[SignalR 中心 API 指南-JavaScript 客户端-生成的代理和它为您完成](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="d8ecf-228">在中心内定义组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="d8ecf-229">SignalR 可以定义在名为组以将广播到连接的客户端的子集。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="d8ecf-230">组都会单独维护每个中心。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="d8ecf-231">例如，一个名为"管理员"组应包括的客户端的一组你`ContosoChatHub`类和相同的组名称所指一组不同的客户端你`StockTickerHub`类。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="d8ecf-232">强类型中心</span><span class="sxs-lookup"><span data-stu-id="d8ecf-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="d8ecf-233">若要定义一个接口，使你的中心方法，你的客户端可以引用 （和启用 Intellisense 在你的中心方法），派生你的中心`Hub<T>`（SignalR 2.1 中引入） 而非`Hub`:</span><span class="sxs-lookup"><span data-stu-id="d8ecf-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="d8ecf-234">如何在客户端可以调用的中心类中定义方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="d8ecf-235">若要公开你想要从客户端调用的中心上的方法，声明一个公共方法，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="d8ecf-236">你可以指定返回类型和参数，包括复杂类型并对数组，就像在任何 C# 方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="d8ecf-237">客户端和服务器之间进行通信的接收参数或返回到调用方的任何数据是通过使用 JSON，和 SignalR 自动处理复杂对象的绑定和对象的数组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="d8ecf-238">混合使用大小写的 JavaScript 客户端中的方法名称</span><span class="sxs-lookup"><span data-stu-id="d8ecf-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="d8ecf-239">默认情况下，JavaScript 客户端到中心方法通过使用的方法名称的混合使用大小写版本引用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="d8ecf-240">SignalR 自动使此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="d8ecf-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="d8ecf-242">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="d8ecf-243">如果你想要指定客户端使用，添加另一个名称`HubMethodName`属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="d8ecf-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="d8ecf-245">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="d8ecf-246">当以异步方式执行</span><span class="sxs-lookup"><span data-stu-id="d8ecf-246">When to execute asynchronously</span></span>

<span data-ttu-id="d8ecf-247">如果该方法将是长时间运行或已进行的工作将涉及等待，如数据库查找或 web 服务调用，请使中心方法异步通过返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)(代替了`void`返回) 或[任务&lt;T&gt; ](https://msdn.microsoft.com/library/dd321424.aspx)对象 (代替了`T`返回类型)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="d8ecf-248">当您返回`Task`从 SignalR 方法的对象会等待`Task`若要完成，然后发送解包的结果返回到客户端，以便在客户端中的方法调用的代码没有差异。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="d8ecf-249">使得的中心方法异步可避免阻止使用 WebSocket 传输时的连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="d8ecf-250">当传输为 WebSocket Hub 方法以同步方式执行，直到中心方法完成之后将阻止从同一个客户端集线器上的方法的后续调用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="d8ecf-251">下面的示例演示相同的方法编码为异步运行，或以异步方式后, 跟适用于调用任一版本的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="d8ecf-252">**同步**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="d8ecf-253">**异步**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="d8ecf-254">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="d8ecf-255">有关如何在 ASP.NET 4.5 中使用异步方法的详细信息，请参阅[使用 ASP.NET MVC 4 中的异步方法](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="d8ecf-256">定义重载</span><span class="sxs-lookup"><span data-stu-id="d8ecf-256">Defining Overloads</span></span>

<span data-ttu-id="d8ecf-257">如果你想要定义的方法的重载，每个重载中的参数数目必须不同。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="d8ecf-258">如果你只需通过指定不同的参数类型区分重载方法，你的中心类能够编译，但 SignalR 服务将引发当客户端尝试的运行时异常时调用的重载之一。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="d8ecf-259">报告从中心方法调用的进度</span><span class="sxs-lookup"><span data-stu-id="d8ecf-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="d8ecf-260">SignalR 2.1 添加了对支持[进度报告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx).NET 4.5 中引入。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="d8ecf-261">若要实现进度报告，定义`IProgress<T>`为你的客户端可以访问你中心方法的参数：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="d8ecf-262">当编写的长时间运行 server 方法，务必使用异步编程模式类似异步 / 等待而不是阻止中心线程。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="d8ecf-263">如何从中心类方法调用客户端</span><span class="sxs-lookup"><span data-stu-id="d8ecf-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="d8ecf-264">若要从服务器中调用客户端方法，使用`Clients`中心类方法中的属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="d8ecf-265">下面的示例演示调用的服务器代码`addNewMessageToPage`所有连接的客户端和 JavaScript 客户端中定义的方法的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="d8ecf-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="d8ecf-267">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-267">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="d8ecf-268">无法从客户端方法; 获取返回值语法如下`int x = Clients.All.add(1,1)`不起作用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-268">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="d8ecf-269">你可以指定复杂类型和参数的数组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-269">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="d8ecf-270">下面的示例将复杂类型传递到方法参数中的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-270">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="d8ecf-271">**调用使用复杂对象的客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-271">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="d8ecf-272">**定义的复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-272">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="d8ecf-273">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-273">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="d8ecf-274">选择哪些客户端将接收 RPC</span><span class="sxs-lookup"><span data-stu-id="d8ecf-274">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="d8ecf-275">客户端属性返回[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)提供若干选项用于指定哪些客户端将接收 RPC 的对象：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-275">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="d8ecf-276">所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-276">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="d8ecf-277">只有调用客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-277">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="d8ecf-278">除调用客户端以外的所有客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-278">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="d8ecf-279">特定客户端由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-279">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="d8ecf-280">此示例调用`addContosoChatMessageToPage`上调用的客户端并且具有与使用相同的效果`Clients.Caller`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-280">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="d8ecf-281">所有连接的客户端除外指定客户端，并由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-281">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="d8ecf-282">在指定的组的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-282">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="d8ecf-283">在指定的组的所有连接的客户端除外指定客户端，并由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-283">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="d8ecf-284">在指定的组的所有连接的客户端除非调用的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-284">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="d8ecf-285">用户 Id 标识特定用户。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-285">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="d8ecf-286">默认情况下，这是`IPrincipal.Identity.Name`，但这可以通过更改[与全局主机注册的 IUserIdProvider 实现](mapping-users-to-connections.md#IUserIdProvider)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-286">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="d8ecf-287">所有客户端和组列表中的连接 Id。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-287">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="d8ecf-288">组的列表。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-288">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="d8ecf-289">按名称的用户。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-289">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="d8ecf-290">（在 SignalR 2.1 中引入） 的用户名称的列表。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-290">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="d8ecf-291">方法名称没有编译时验证</span><span class="sxs-lookup"><span data-stu-id="d8ecf-291">No compile-time validation for method names</span></span>

<span data-ttu-id="d8ecf-292">你指定的方法名称被解释为动态对象，这意味着没有 IntelliSense 或它的编译时验证。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-292">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="d8ecf-293">在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-293">The expression is evaluated at run time.</span></span> <span data-ttu-id="d8ecf-294">当方法调用执行时，SignalR 将方法名称和参数值发送到客户端，并在客户端有一种方法的名称相匹配，方法被称为和参数值将传递给它。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-294">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="d8ecf-295">如果客户端上不找到任何匹配方法，则不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-295">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="d8ecf-296">有关格式的数据的 SignalR 将传输到客户端在后台调用客户端方法时的信息，请参阅[简介 SignalR](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-296">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="d8ecf-297">不区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="d8ecf-297">Case-insensitive method name matching</span></span>

<span data-ttu-id="d8ecf-298">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-298">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d8ecf-299">例如，`Clients.All.addContosoChatMessageToPage`在服务器上将执行`AddContosoChatMessageToPage`， `addcontosochatmessagetopage`，或`addContosoChatMessageToPage`客户端上。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-299">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="d8ecf-300">异步执行</span><span class="sxs-lookup"><span data-stu-id="d8ecf-300">Asynchronous execution</span></span>

<span data-ttu-id="d8ecf-301">调用此方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-301">The method that you call executes asynchronously.</span></span> <span data-ttu-id="d8ecf-302">提供对客户端的方法调用将立即执行而无需等待 SignalR 完成传输到客户端的数据，除非另行指定，后面的代码行应等待方法完成后的任何代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-302">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="d8ecf-303">下面的代码示例演示如何以按顺序执行两个客户端方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-303">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="d8ecf-304">**使用 Await (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-304">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="d8ecf-305">如果你使用`await`等待直到客户端方法完成之前执行下一步一行代码，这并不表示客户端在执行下的一行代码之前，将实际收到的消息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-305">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="d8ecf-306">"完成"的客户端方法调用仅意味着 SignalR 已完成所需将消息发送的一切。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-306">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="d8ecf-307">如果你需要验证客户端收到消息，你必须自己进行编程该机制。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-307">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="d8ecf-308">例如，无法代码`MessageReceived`方法的中心，并在`addContosoChatMessageToPage`方法在客户端可以调用`MessageReceived`执行完操作后任何起作用，您需要在客户端上执行操作。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-308">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="d8ecf-309">在`MessageReceived`中心中你可以执行任何工作取决于实际的客户端接收和处理的原始方法调用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-309">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="d8ecf-310">如何使用作为方法名称的字符串变量</span><span class="sxs-lookup"><span data-stu-id="d8ecf-310">How to use a string variable as the method name</span></span>

<span data-ttu-id="d8ecf-311">如果你想要通过使用作为强制转换的方法名称的字符串变量调用客户端方法`Clients.All`(或`Clients.Others`，`Clients.Caller`等) 到`IClientProxy`，然后调用[Invoke （方法名称、 参数...）](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="d8ecf-311">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="d8ecf-312">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="d8ecf-312">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="d8ecf-313">SignalR 中的组提供一种方法将消息广播到连接的客户端的指定子集。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-313">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="d8ecf-314">组可以具有任意数量的客户端，并且客户端可以是任意数量的组的成员。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-314">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="d8ecf-315">若要管理组成员身份，使用[添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)和[删除](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)提供方法`Groups`中心类的属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-315">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="d8ecf-316">下面的示例演示`Groups.Add`和`Groups.Remove`方法在由客户端代码调用的中心方法中使用跟调用它们的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-316">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="d8ecf-317">**Server**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-317">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="d8ecf-318">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-318">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="d8ecf-319">你无需显式创建组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-319">You don't have to explicitly create groups.</span></span> <span data-ttu-id="d8ecf-320">实际上自动创建组对的调用中指定其名称的第一个时间`Groups.Add`，并将其删除从中它的成员身份中删除最后一次连接时。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-320">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="d8ecf-321">用于获取组成员身份列表或组的列表中没有任何 API。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-321">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="d8ecf-322">SignalR 将消息发送到客户端和基于组[发布/订阅模型](http://en.wikipedia.org/wiki/Publish/subscribe)，而服务器不保持组或组成员身份的列表。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-322">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="d8ecf-323">这有助于最大程度提高可伸缩性，因为每当向 web 场添加节点时，SignalR 维护任何状态都将传播到新节点。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-323">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="d8ecf-324">异步执行的 Add 和 Remove 方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-324">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="d8ecf-325">`Groups.Add`和`Groups.Remove`方法异步执行。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-325">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="d8ecf-326">如果你想要将客户端添加到组并立即向客户端发送一条消息，通过使用组，则必须确保`Groups.Add`方法先完成。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-326">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="d8ecf-327">下面的代码示例演示如何执行该操作。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-327">The following code example shows how to do that.</span></span>

<span data-ttu-id="d8ecf-328">**向组添加客户端，然后消息传送该客户端**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-328">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="d8ecf-329">组成员身份持久性</span><span class="sxs-lookup"><span data-stu-id="d8ecf-329">Group membership persistence</span></span>

<span data-ttu-id="d8ecf-330">SignalR 跟踪的连接，不是用户，因此，如果你希望某个用户是同一组中每次用户建立的连接，则必须调用`Groups.Add`每次用户建立新连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-330">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="d8ecf-331">后的连接暂时中断，有时 SignalR 可以还原该连接自动。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-331">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="d8ecf-332">在这种情况下，SignalR 正在还原相同的连接，不建立新连接，并因此客户端的组成员身份会自动还原。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-332">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="d8ecf-333">这是可能甚至临时中断时重新启动服务器或发生故障，结果因为对于每个客户端，包括组成员身份的连接状态是往返到客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-333">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="d8ecf-334">如果一台服务器出现故障，并且都替换为新的服务器连接超时之前，客户端可以自动重新连接到新服务器，并重新注册它是成员的组中。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-334">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="d8ecf-335">当不能在连接丢失后自动恢复连接或连接超时时，或客户端断开连接 （例如，当浏览器导航到新页） 时，组成员身份都将丢失。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-335">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="d8ecf-336">在下次用户连接的时将新的连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-336">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="d8ecf-337">若要维护组成员身份，当同一个用户建立新连接时，将应用程序来跟踪用户和组之间的关联和还原每次用户建立新连接的组成员身份。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-337">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="d8ecf-338">有关连接和重新连接的详细信息，请参阅[如何连接生存期中处理事件的中心类](#connectionlifetime)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-338">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="d8ecf-339">单用户组</span><span class="sxs-lookup"><span data-stu-id="d8ecf-339">Single-user groups</span></span>

<span data-ttu-id="d8ecf-340">通常使用 SignalR 的应用程序需要跟踪的用户连接之间的关联才能知道哪些用户已发送一条消息并哪些用户应该能够接收一条消息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-340">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="d8ecf-341">组用于在两种常用模式之一中执行该操作。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-341">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="d8ecf-342">单用户组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-342">Single-user groups.</span></span>

    <span data-ttu-id="d8ecf-343">可以将用户名称指定为组名称，并将当前的连接 ID 添加到组，每次用户连接或重新连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-343">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="d8ecf-344">若要将消息发送到发送到组的用户。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-344">To send messages to the user you send to the group.</span></span> <span data-ttu-id="d8ecf-345">此方法的缺点是组不为您提供了一种方法，若要了解是否用户是联机还是脱机。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-345">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="d8ecf-346">跟踪用户名称和连接 Id 之间的关联。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-346">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="d8ecf-347">你可以将每个用户名称和一个或多个连接 Id 之间的关联存储在字典或数据库，并更新每次用户连接或断开连接的存储的数据。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-347">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="d8ecf-348">若要将消息发送到用户你指定的连接 Id。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-348">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="d8ecf-349">此方法的缺点是它采用更多内存。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-349">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="d8ecf-350">如何连接生存期中处理事件的中心类</span><span class="sxs-lookup"><span data-stu-id="d8ecf-350">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="d8ecf-351">适用于处理连接生存期事件的典型原因是能够跟踪是否某位用户连接，并跟踪的用户名称和连接 Id 之间的关联。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-351">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="d8ecf-352">若要运行你自己的代码，客户端连接或断开连接时，重写`OnConnected`， `OnDisconnected`，和`OnReconnected`虚方法的中心类，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-352">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="d8ecf-353">当调用 OnConnected、 OnDisconnected 和 OnReconnected</span><span class="sxs-lookup"><span data-stu-id="d8ecf-353">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="d8ecf-354">浏览器导航到新页，每次新的连接已建立，这意味着将执行 SignalR`OnDisconnected`方法跟`OnConnected`方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-354">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="d8ecf-355">建立新连接时，SignalR 始终会创建新的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-355">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="d8ecf-356">`OnReconnected` SignalR 可以从自动恢复，如当电缆暂时断开连接后又重新连接超时之前连接的连接已临时中断时，调用方法。`OnDisconnected`时客户端断开连接并且 SignalR 无法自动重新连接，如当浏览器导航到新页调用方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-356">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="d8ecf-357">因此，给定的客户端事件的可能序列是`OnConnected`， `OnReconnected`， `OnDisconnected`; 或`OnConnected`， `OnDisconnected`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-357">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="d8ecf-358">你不会看到序列`OnConnected`， `OnDisconnected`，`OnReconnected`针对给定连接。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-358">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="d8ecf-359">`OnDisconnected`某些情况下，例如服务器出现故障时不会调用方法或应用程序域获取回收。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-359">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="d8ecf-360">当另一台服务器变为联机或应用程序域完成其回收时，某些客户端可能无法重新连接并激发`OnReconnected`事件。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-360">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="d8ecf-361">有关详细信息，请参阅[了解和处理连接生存期中事件的 SignalR](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-361">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="d8ecf-362">不填充的调用方状态</span><span class="sxs-lookup"><span data-stu-id="d8ecf-362">Caller state not populated</span></span>

<span data-ttu-id="d8ecf-363">连接生存期事件处理程序调用这些方法，在服务器上，这意味着将放在任何状态`state`客户端上的对象将不会填充`Caller`服务器上的属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-363">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="d8ecf-364">璝惠`state`对象和`Caller`属性，请参阅[如何将状态传递客户端和中心类之间](#passstate)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-364">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="d8ecf-365">如何从上下文属性中获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="d8ecf-365">How to get information about the client from the Context property</span></span>

<span data-ttu-id="d8ecf-366">若要获取有关客户端的信息，请使用`Context`中心类的属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-366">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="d8ecf-367">`Context`属性返回[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)对象提供了访问权的以下信息：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-367">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="d8ecf-368">调用的客户端连接 ID。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-368">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="d8ecf-369">连接 ID 是由 SignalR （这无法在你自己的代码中指定值） 分配的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-369">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="d8ecf-370">没有为每个连接，并且如果你有多个中心应用程序中，所有中心都使用 ID 的相同连接的一个连接 ID。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-370">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="d8ecf-371">HTTP 标头数据。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-371">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="d8ecf-372">你还可以获取 HTTP 标头从`Context.Headers`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-372">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="d8ecf-373">将相同内容的多个引用的原因在于`Context.Headers`首先，创建`Context.Request`更高版本，已添加属性和`Context.Headers`被保留用于向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-373">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="d8ecf-374">查询字符串数据。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-374">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="d8ecf-375">你还可以获取查询字符串数据从`Context.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-375">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="d8ecf-376">获取此属性中的查询字符串是用于建立 SignalR 连接的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-376">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="d8ecf-377">通过配置的连接，这是一种简便方式从客户端向服务器传递有关客户端的数据，可以在客户端添加查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-377">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="d8ecf-378">下面的示例演示当你使用生成的代理时，JavaScript 客户端中添加的查询字符串的一种方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-378">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="d8ecf-379">有关设置查询字符串参数的详细信息，请参阅针对的 API 指南[JavaScript](hubs-api-guide-javascript-client.md)和[.NET](hubs-api-guide-net-client.md)客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-379">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="d8ecf-380">你可以找到用于在查询字符串数据中，供内部使用 SignalR 的一些其他值一起连接的传输方法：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-380">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="d8ecf-381">值`transportMethod`将"webSockets"、"serverSentEvents"、"foreverFrame"或"longPolling"。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-381">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="d8ecf-382">请注意，如果此值签入`OnConnected`事件处理程序方法中，在某些情况下可能一开始就会传输该值不是连接的最终协商的传输方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-382">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="d8ecf-383">在这种情况下方法将引发异常，建立最终传输方法时进行调用的试更高版本。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-383">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="d8ecf-384">Cookie。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-384">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="d8ecf-385">你还可以获得的 cookie `Context.RequestCookies`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-385">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="d8ecf-386">用户信息。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-386">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="d8ecf-387">请求的 HttpContext 对象：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-387">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="d8ecf-388">使用此方法，而不是获得`HttpContext.Current`获取`HttpContext`SignalR 连接的对象。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-388">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="d8ecf-389">如何将状态传递客户端和中心类之间</span><span class="sxs-lookup"><span data-stu-id="d8ecf-389">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="d8ecf-390">客户端代理提供`state`可以在其中存储要传输到每个方法调用的服务器的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-390">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="d8ecf-391">可以在服务器上访问此数据`Clients.Caller`由客户端调用的中心方法中的属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-391">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="d8ecf-392">`Clients.Caller`连接生存期事件处理程序方法将不填充属性`OnConnected`， `OnDisconnected`，和`OnReconnected`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-392">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="d8ecf-393">创建或更新中的数据`state`对象和`Clients.Caller`属性在两个方向起作用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-393">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="d8ecf-394">您可以更新服务器中的值和它们会传递回客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-394">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="d8ecf-395">下面的示例演示将以发送给每个方法调用的服务器的状态存储的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-395">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="d8ecf-396">下面的示例演示的.NET 客户端中的等效代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-396">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="d8ecf-397">在中心类中，你可以访问此数据`Clients.Caller`属性。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-397">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="d8ecf-398">下面的示例显示检索在前面的示例中称为的状态的代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-398">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="d8ecf-399">状态持久化此机制不适用于大量数据，因为所有内容放在`state`或`Clients.Caller`属性是往返与每个方法调用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-399">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="d8ecf-400">它可用于较小的项，如用户名称或计数器。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-400">It's useful for smaller items such as user names or counters.</span></span>


<span data-ttu-id="d8ecf-401">在 VB.NET 或强类型的中心中，无法通过访问调用方状态对象`Clients.Caller`; 相反，使用`Clients.CallerState`（SignalR 2.1 中引入）：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-401">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="d8ecf-402">**在 C# 中使用 CallerState**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-402">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="d8ecf-403">**在 Visual Basic 中使用 CallerState**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-403">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="d8ecf-404">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="d8ecf-404">How to handle errors in the Hub class</span></span>

<span data-ttu-id="d8ecf-405">若要处理在中心类方法中发生的错误，请使用一个或多个以下方法：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-405">To handle errors that occur in your Hub class methods, use one or more of the following methods:</span></span>

- <span data-ttu-id="d8ecf-406">在 try-catch 块中包装你的方法代码和日志的异常对象。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-406">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="d8ecf-407">出于调试目的可以将异常发送到客户端，但出于安全原因详细的信息发送给在生产环境中的客户端不建议。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-407">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="d8ecf-408">创建处理的中心管道模块[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-408">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="d8ecf-409">下面的示例演示的管道模块，记录错误，跟模块注入中心管道的 Startup.cs 中的代码。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-409">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="d8ecf-410">使用`HubException`（SignalR 2 中引入） 的类。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-410">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="d8ecf-411">可以从任何中心调用引发此错误。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-411">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="d8ecf-412">`HubError`构造函数采用一个字符串消息和一个对象，用于存储额外的错误数据。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-412">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="d8ecf-413">SignalR 将自动序列化异常，并将其发送到客户端，其中它将用于拒绝或失败中心方法调用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-413">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="d8ecf-414">下面的代码示例演示如何引发`HubException`期间的中心调用，以及如何处理在 JavaScript 和.NET 客户端上的异常。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-414">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="d8ecf-415">**服务器代码演示 HubException 类**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-415">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="d8ecf-416">**演示在一个中心中引发 HubException 响应的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-416">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="d8ecf-417">**演示在一个中心中引发 HubException 响应的.NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="d8ecf-417">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="d8ecf-418">有关中心管道模块的详细信息，请参阅[如何自定义中心管道](#hubpipeline)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-418">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="d8ecf-419">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="d8ecf-419">How to enable tracing</span></span>

<span data-ttu-id="d8ecf-420">若要启用服务器端跟踪，system.diagnostics 将元素添加到 Web.config 文件中，在此示例中所示：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-420">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="d8ecf-421">Visual Studio 中运行应用程序时，你可以查看中的日志**输出**窗口。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-421">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="d8ecf-422">如何调用方法的客户端和管理从中心类外部的组</span><span class="sxs-lookup"><span data-stu-id="d8ecf-422">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="d8ecf-423">若要从你的中心类比另一个类中调用客户端方法，中心获取对 SignalR 上下文对象的引用，并使用的客户端上调用方法或管理组。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-423">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="d8ecf-424">下面的示例`StockTicker`类获取上下文对象、 将其存储在类的实例，将类实例存储在静态属性，并使用从单一类实例的上下文调用`updateStockPrice`上的客户端的方法连接到名为集线器`StockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-424">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="d8ecf-425">如果你需要在长生存期对象中使用上下文多个时间，一次获取该引用，并保存它而不是每个时再次开始。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-425">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="d8ecf-426">一次获取上下文可确保 SignalR 将消息发送到相同的序列顺序中心方法使客户端方法调用中的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-426">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="d8ecf-427">有关演示如何使用中心 SignalR 上下文的教程，请参阅[服务器广播使用 ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-427">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="d8ecf-428">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="d8ecf-428">Calling client methods</span></span>

<span data-ttu-id="d8ecf-429">你可以指定哪些客户端将接收 RPC，但是必须比当您调用从中心类较少的选项。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-429">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="d8ecf-430">这样做的原因是，上下文不相关联的特定调用从客户端，因此任何方法，如需要知识的当前的连接 ID， `Clients.Others`，或`Clients.Caller`，或`Clients.OthersInGroup`，不可用。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-430">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="d8ecf-431">可用选项如下：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-431">The following options are available:</span></span>

- <span data-ttu-id="d8ecf-432">所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-432">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="d8ecf-433">特定客户端由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-433">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="d8ecf-434">所有连接的客户端除外指定客户端，并由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-434">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="d8ecf-435">在指定的组的所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-435">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="d8ecf-436">所有连接的客户端在指定的组除指定客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-436">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="d8ecf-437">如果要调用到非中心类从方法中你的中心类，你可以在当前的连接 ID 传递并使用使用`Clients.Client`， `Clients.AllExcept`，或`Clients.Group`以模拟`Clients.Caller`， `Clients.Others`，或`Clients.OthersInGroup`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-437">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="d8ecf-438">在下面的示例中，`MoveShapeHub`类将传递到的连接 ID`Broadcaster`类，以便`Broadcaster`类可以模拟`Clients.Others`。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-438">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="d8ecf-439">管理组成员资格</span><span class="sxs-lookup"><span data-stu-id="d8ecf-439">Managing group membership</span></span>

<span data-ttu-id="d8ecf-440">用于管理组中，与你在中心类具有相同的选项。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-440">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="d8ecf-441">将客户端添加到组</span><span class="sxs-lookup"><span data-stu-id="d8ecf-441">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="d8ecf-442">从组中删除客户端</span><span class="sxs-lookup"><span data-stu-id="d8ecf-442">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="d8ecf-443">如何自定义中心管道</span><span class="sxs-lookup"><span data-stu-id="d8ecf-443">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="d8ecf-444">SignalR 可将你自己的代码注入到中心管道。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-444">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="d8ecf-445">下面的示例演示自定义中心管道模块记录来自客户端和客户端上调用的传出方法调用每个传入方法调用：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-445">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="d8ecf-446">下面的代码中*Startup.cs*文件注册要在中心管线中运行的模块：</span><span class="sxs-lookup"><span data-stu-id="d8ecf-446">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="d8ecf-447">有许多不同的方法可以重写。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-447">There are many different methods that you can override.</span></span> <span data-ttu-id="d8ecf-448">完整列表，请参阅[HubPipelineModule 方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d8ecf-448">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
