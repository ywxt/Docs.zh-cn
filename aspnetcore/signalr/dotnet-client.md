---
title: ASP.NET 核心 SignalR.NET 客户端
author: rachelappel
description: 有关 ASP.NET 核心 SignalR.NET 客户端信息
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/18/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/dotnet-client
ms.openlocfilehash: 412d2362575789f1fb4792940df6d3dd24dbdd5a
ms.sourcegitcommit: 300a1127957dcdbce1b6ad79a7b9dc676f571510
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34459017"
---
# <a name="aspnet-core-signalr-net-client"></a>ASP.NET 核心 SignalR.NET 客户端

作者：[Rachel Appel](http://twitter.com/rachelappel)

ASP.NET 核心 SignalR.NET 客户端可以使用 Xamarin、 WPF、 Windows 窗体，控制台中和.NET Core 应用。 如[JavaScript 客户端](xref:signalr/javascript-client)，.NET 客户端可以接收和发送和实时接收到中心的消息。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

这篇文章中的代码示例是使用 ASP.NET 核心 SignalR.NET 客户端的 WPF 应用。

## <a name="setup-client"></a>安装客户端

`Microsoft.AspNetCore.SignalR.Client`包所需的.NET 客户端连接到 SignalR 集线器。 若要安装的客户端库，运行以下命令**程序包管理器控制台**窗口：

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a>连接到中心

若要建立的连接，创建`HubConnectionBuilder`并调用`Build`。 建立连接时，可以配置中心 URL、 协议、 传输类型、 日志级别、 头和其他选项。 配置任何必需的选项的方法是插入的任何`HubConnectionBuilder`方法到`Build`。 启动与连接`StartAsync`。

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a>从客户端调用中心方法

`InvokeAsync` 在中心调用方法。 将中心方法名称和到中心方法中定义的任何自变量传递`InvokeAsync`。 SignalR 是异步的因此请使用`async`和`await`时进行调用。

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a>从中心调用客户端方法

定义使用中心调用的方法`connection.On`之后生成过程中，但之前启动连接。

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

在前面的代码`connection.On`运行时服务器端代码将调用它使用`SendAsync`方法。

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a>错误处理和日志记录

处理使用 try catch 语句的错误。 检查`Exception`对象确定要执行发生错误后的正确操作。

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a>其他资源

* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)