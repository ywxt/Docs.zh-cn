---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 示例 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: a26cdf144d02f0b429994df9d7863163807ac7b5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827267"
---
<a name="katana-samples"></a>Katana 示例
====================
by [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 示例

**ASP.NET 路由示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)  
在某些应用程序要挂接 OWIN 组件与非 OWIN 组件并行的 Asp.Net 路由表中。 此示例演示如何使用 MapOwinPath 和提供的 Microsoft.Owin.Host.SystemWeb MapOwinRoute RouteCollection 扩展方法。

**分支管道示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)  
OWIN 请求处理管道无需是线性的它们可以分支以不同方式处理请求。 此示例演示如何构造基于请求路径或其他请求数据，例如，标头的分支管道。 这些组件是 Microsoft.Owin.Mapping nuget 包中提供。

**自定义服务器示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs)   
演示如何使用自定义的 OWIN 服务器时自托管 OWIN。

**嵌入示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)  
可以在您自己的进程内运行某些 OWIN 服务器 (&quot;自承载&quot;)。 此示例演示如何开始使用 Microsoft.Owin.Hosting nuget 包提供的工具的 OWIN 应用程序。

**HelloWorld 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)  
OWIN 是一个 HTTP 服务器 API 抽象，允许跨多个服务器的应用程序可移植性。 此示例演示如何编写的 Hello World 应用程序使用一些**的简单包装**围绕原始 OWIN 抽象和运行 web 服务器上它像 ASP.NET。

**Hello World 原始 OWIN 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)  
此示例演示如何编写的 Hello World 应用程序使用**原始**OWIN 抽象，如 Asp.Net 的 web 服务器上运行。

**SignalR 示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)  
演示如何自承载 SignalR 使用 OWIN / Katana。 有关自承载 SignalR 的详细信息，请参阅[教程： 自承载 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

**静态文件示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs)   
演示如何支持 HTTP 请求的静态文件使用 OWIN / Katana。

**Web API** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt)   
此示例演示如何承载在 IIS 中的 OWIN 和将 Web API 添加到 OWIN 管道。

**Web 套接字示例** | [源代码](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs)   
演示如何通过使用在 OWIN 支持 Web 套接字[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)类。
