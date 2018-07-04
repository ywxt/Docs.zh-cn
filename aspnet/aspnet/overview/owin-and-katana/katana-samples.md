---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 示例 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2014
ms.topic: article
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
ms.technology: ''
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: e81da1e650d8dfd24a3e0fda6aa42b7f360ce12d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393314"
---
<a name="katana-samples"></a><span data-ttu-id="3dc93-102">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="3dc93-102">Katana Samples</span></span>
====================
<span data-ttu-id="3dc93-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3dc93-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="3dc93-104">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="3dc93-104">Katana Samples</span></span>

<span data-ttu-id="3dc93-105">**ASP.NET 路由示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="3dc93-105">**ASP.NET Routes Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)</span></span>  
<span data-ttu-id="3dc93-106">在某些应用程序要挂接 OWIN 组件与非 OWIN 组件并行的 Asp.Net 路由表中。</span><span class="sxs-lookup"><span data-stu-id="3dc93-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="3dc93-107">此示例演示如何使用 MapOwinPath 和提供的 Microsoft.Owin.Host.SystemWeb MapOwinRoute RouteCollection 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="3dc93-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="3dc93-108">**分支管道示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="3dc93-108">**Branching Pipelines Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)</span></span>  
<span data-ttu-id="3dc93-109">OWIN 请求处理管道无需是线性的它们可以分支以不同方式处理请求。</span><span class="sxs-lookup"><span data-stu-id="3dc93-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="3dc93-110">此示例演示如何构造基于请求路径或其他请求数据，例如，标头的分支管道。</span><span class="sxs-lookup"><span data-stu-id="3dc93-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="3dc93-111">这些组件是 Microsoft.Owin.Mapping nuget 包中提供。</span><span class="sxs-lookup"><span data-stu-id="3dc93-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="3dc93-112">**自定义服务器示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs) </span><span class="sxs-lookup"><span data-stu-id="3dc93-112">**Custom Server Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs) </span></span>  
<span data-ttu-id="3dc93-113">演示如何使用自定义的 OWIN 服务器时自托管 OWIN。</span><span class="sxs-lookup"><span data-stu-id="3dc93-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="3dc93-114">**嵌入示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="3dc93-114">**Embedded Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)</span></span>  
<span data-ttu-id="3dc93-115">可以在您自己的进程内运行某些 OWIN 服务器 (&quot;自承载&quot;)。</span><span class="sxs-lookup"><span data-stu-id="3dc93-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="3dc93-116">此示例演示如何开始使用 Microsoft.Owin.Hosting nuget 包提供的工具的 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3dc93-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="3dc93-117">**HelloWorld 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="3dc93-117">**HelloWorld Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)</span></span>  
<span data-ttu-id="3dc93-118">OWIN 是一个 HTTP 服务器 API 抽象，允许跨多个服务器的应用程序可移植性。</span><span class="sxs-lookup"><span data-stu-id="3dc93-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="3dc93-119">此示例演示如何编写的 Hello World 应用程序使用一些**的简单包装**围绕原始 OWIN 抽象和运行 web 服务器上它像 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="3dc93-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="3dc93-120">**Hello World 原始 OWIN 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="3dc93-120">**Hello World Raw OWIN Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)</span></span>  
<span data-ttu-id="3dc93-121">此示例演示如何编写的 Hello World 应用程序使用**原始**OWIN 抽象，如 Asp.Net 的 web 服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="3dc93-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="3dc93-122">**SignalR 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="3dc93-122">**SignalR Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)</span></span>  
<span data-ttu-id="3dc93-123">演示如何自承载 SignalR 使用 OWIN / Katana。</span><span class="sxs-lookup"><span data-stu-id="3dc93-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="3dc93-124">有关自承载 SignalR 的详细信息，请参阅[教程： 自承载 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="3dc93-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="3dc93-125">**静态文件示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs) </span><span class="sxs-lookup"><span data-stu-id="3dc93-125">**Static Files Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs) </span></span>  
<span data-ttu-id="3dc93-126">演示如何支持 HTTP 请求的静态文件使用 OWIN / Katana。</span><span class="sxs-lookup"><span data-stu-id="3dc93-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="3dc93-127">**Web API** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt) </span><span class="sxs-lookup"><span data-stu-id="3dc93-127">**Web API** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt) </span></span>  
<span data-ttu-id="3dc93-128">此示例演示如何承载在 IIS 中的 OWIN 和将 Web API 添加到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="3dc93-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="3dc93-129">**Web 套接字示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs) </span><span class="sxs-lookup"><span data-stu-id="3dc93-129">**Web Socket Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs) </span></span>  
<span data-ttu-id="3dc93-130">演示如何通过使用在 OWIN 支持 Web 套接字[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)类。</span><span class="sxs-lookup"><span data-stu-id="3dc93-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
