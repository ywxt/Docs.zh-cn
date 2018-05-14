---
title: ASP.NET Core 中的 WebSocket 支持
author: tdykstra
description: 了解如何在 ASP.NET Core 中开始使用 WebSocket。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/websockets
ms.openlocfilehash: e744ab5b81ff85f48edb012a86b55003cc74929c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="websockets-support-in-aspnet-core"></a>ASP.NET Core 中的 WebSocket 支持

作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Andrew Stanton-Nurse](https://github.com/anurse)

本文介绍 ASP.NET Core 中 WebSocket 的入门方法。 [WebSocket](https://wikipedia.org/wiki/WebSocket) ([RFC 6455](https://tools.ietf.org/html/rfc6455)) 是一个协议，支持通过 TCP 连接建立持久的双向信道。 它用于从快速实时通信中获益的应用，如聊天、仪表板和游戏应用。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。 有关详细信息，请参阅[后续步骤](#next-steps)部分。

## <a name="prerequisites"></a>系统必备

* ASP.NET Core 1.1 或更高版本
* 支持 ASP.NET Core 的任何操作系统：
  
  * Windows 7/Windows Server 2008 或更高版本
  * Linux
  * macOS
  
* 如果应用在安装了 IIS 的 Windows 上运行：

  * Windows 8 / Windows Server 2012 及更高版本
  * IIS 8 / IIS 8 Express
  * 必须在 IIS 中启用 WebSocket（请参阅 [IIS/IIS Express 支持](#iisiis-express-support)部分。）
  
* 如果应用在 [HTTP.sys](xref:fundamentals/servers/httpsys) 上运行：

  * Windows 8 / Windows Server 2012 及更高版本

* 有关支持的浏览器，请参阅 https://caniuse.com/#feat=websockets。

## <a name="when-to-use-websockets"></a>何时使用 WebSocket

通过 WebSocket 可直接使用套接字连接。 例如，使用 WebSocket 可以让实时游戏达到最佳性能。

[ASP.NET SignalR](/aspnet/signalr/overview/getting-started/introduction-to-signalr) 为实时功能提供了更丰富的应用模型，但它仅在 ASP.NET 4.x 上运行，不能在 ASP.NET Core 上运行。 SignalR 的 ASP.NET Core 版本计划随 ASP.NET Core 2.1 一起发布。 请参阅 [ASP.NET Core 2.1 高级计划](https://github.com/aspnet/Announcements/issues/288)。

发布 SignalR Core 前，可使用 WebSocket。 但 SignalR 的功能必须由开发人员提供和支持。 例如:

* 通过自动回退到替代传输方法来支持更广泛的浏览器版本。
* 连接断开时自动重新连接。
* 支持服务器上的客户端调用方法，反之亦然。
* 支持缩放到多个服务器。

## <a name="how-to-use-it"></a>使用方法

* 安装 [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 包。
* 配置中间件。
* 接受 WebSocket 请求。
* 发送和接收消息。

### <a name="configure-the-middleware"></a>配置中间件

在 `Startup` 类的 `Configure` 方法中添加 WebSocket 中间件：

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

可配置以下设置：

* `KeepAliveInterval` - 向客户端发送“ping”帧的频率，以确保代理保持连接处于打开状态。
* `ReceiveBufferSize` - 用于接收数据的缓冲区的大小。 高级用户可能需要对其进行更改，以便根据数据大小调整性能。

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a>接受 WebSocket 请求

在请求生命周期后期（例如在 `Configure` 方法或 MVC 操作的后期），检查它是否是 WebSocket 请求并接受 WebSocket 请求。

以下示例来自 `Configure` 方法的后期：

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

WebSocket 请求可以来自任何 URL，但此示例代码只接受 `/ws` 的请求。

### <a name="send-and-receive-messages"></a>发送和接收消息

`AcceptWebSocketAsync` 方法将 TCP 连接升级到 WebSocket 连接，并提供 [WebSocket](/dotnet/core/api/system.net.websockets.websocket) 对象。 使用 `WebSocket` 对象发送和接收消息。

之前显示的接受 WebSocket 请求的代码将 `WebSocket` 对象传递给 `Echo` 方法。 代码接收消息并立即发回相同的消息。 循环发送和接收消息，直到客户端关闭连接：

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

如果在开始循环之前接受 WebSocket 连接，中间件管道会结束。 关闭套接字后，管道展开。 即接受 WebSocket 时，请求停止在管道中推进。 循环结束且套接字关闭时，请求继续回到管道。

## <a name="iisiis-express-support"></a>IIS/IIS Express 支持

安装了 IIS/IIS Express 8 或更高版本的 Windows Server 2012 或更高版本以及 Windows 8 或更高版本支持 WebSocket 协议。

在 Windows Server 2012 或更高版本上启用对 WebSocket 协议的支持：

1. 通过“管理”菜单或“服务器管理器”中的链接使用“添加角色和功能”向导。
1. 选择“基于角色或基于功能的安装”。 选择“下一步”。
1. 选择适当的服务器（默认情况下选择本地服务器）。 选择“下一步”。
1. 在“角色”树中展开“Web 服务器 (IIS)”、然后依次展开“Web 服务器”和“应用程序开发”。
1. 选择“WebSocket 协议”。 选择“下一步”。
1. 如果无需其他功能，请选择“下一步”。
1. 选择“安装” 。
1. 安装完成后，选择“关闭”以退出向导。

在 Windows 8 或更高版本上启用对 WebSocket 协议的支持：

1. 导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。
1. 打开以下节点：“Internet Information Services” > “万维网服务” > “应用程序开发功能”。
1. 选择“WebSocket 协议”功能。 选择“确定”。

在 node.js 上使用 socket.io 时禁用 WebSocket

如果在 [Node.js](https://nodejs.org/) 的 [socket.io](https://socket.io/) 中使用 WebSocket 支持，请使用 web.config 或 applicationHost.config 中的 `webSocket` 元素禁用默认的 IIS WebSocket 模块。如果不执行此步骤，IIS WebSocket 模块将尝试处理 WebSocket 通信而不是 Node.js 和应用。

```xml
<system.webServer>
  <webSocket enabled="false" />
</system.webServer>
```

## <a name="next-steps"></a>后续步骤

本文附带的[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)是一个 echo 应用。 它有一个可建立 WebSocket 连接的网页，且服务器将其收到的消息重新发回到客户端。 从命令提示符运行该应用（它未设置为在安装了 IIS Express 的 Visual Studio 中运行）并导航到 http://localhost:5000。 该网页的左上方显示连接状态：

![网页的初始状态](websockets/_static/start.png)

选择“连接”，向显示的 URL 发送 WebSocket 请求。 输入测试消息并选择“发送”。 完成后，请选择“关闭套接字”。 “通信日志”部分会报告每一个发生的“打开”、“发送”和“关闭”操作。

![网页的初始状态](websockets/_static/end.png)
