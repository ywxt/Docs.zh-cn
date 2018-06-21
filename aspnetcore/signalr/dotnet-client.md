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
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="67f26-103">ASP.NET 核心 SignalR.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="67f26-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="67f26-104">作者：[Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="67f26-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="67f26-105">ASP.NET 核心 SignalR.NET 客户端可以使用 Xamarin、 WPF、 Windows 窗体，控制台中和.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="67f26-105">The ASP.NET Core SignalR .NET client can be used by Xamarin, WPF, Windows Forms, Console, and .NET Core apps.</span></span> <span data-ttu-id="67f26-106">如[JavaScript 客户端](xref:signalr/javascript-client)，.NET 客户端可以接收和发送和实时接收到中心的消息。</span><span class="sxs-lookup"><span data-stu-id="67f26-106">Like the [JavaScript client](xref:signalr/javascript-client), the .NET client enables you to receive and send and receive messages to a hub in real time.</span></span>

<span data-ttu-id="67f26-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="67f26-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="67f26-108">这篇文章中的代码示例是使用 ASP.NET 核心 SignalR.NET 客户端的 WPF 应用。</span><span class="sxs-lookup"><span data-stu-id="67f26-108">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="setup-client"></a><span data-ttu-id="67f26-109">安装客户端</span><span class="sxs-lookup"><span data-stu-id="67f26-109">Setup client</span></span>

<span data-ttu-id="67f26-110">`Microsoft.AspNetCore.SignalR.Client`包所需的.NET 客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="67f26-110">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="67f26-111">若要安装的客户端库，运行以下命令**程序包管理器控制台**窗口：</span><span class="sxs-lookup"><span data-stu-id="67f26-111">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="67f26-112">连接到中心</span><span class="sxs-lookup"><span data-stu-id="67f26-112">Connect to a hub</span></span>

<span data-ttu-id="67f26-113">若要建立的连接，创建`HubConnectionBuilder`并调用`Build`。</span><span class="sxs-lookup"><span data-stu-id="67f26-113">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="67f26-114">建立连接时，可以配置中心 URL、 协议、 传输类型、 日志级别、 头和其他选项。</span><span class="sxs-lookup"><span data-stu-id="67f26-114">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="67f26-115">配置任何必需的选项的方法是插入的任何`HubConnectionBuilder`方法到`Build`。</span><span class="sxs-lookup"><span data-stu-id="67f26-115">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="67f26-116">启动与连接`StartAsync`。</span><span class="sxs-lookup"><span data-stu-id="67f26-116">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="67f26-117">从客户端调用中心方法</span><span class="sxs-lookup"><span data-stu-id="67f26-117">Call hub methods from client</span></span>

<span data-ttu-id="67f26-118">`InvokeAsync` 在中心调用方法。</span><span class="sxs-lookup"><span data-stu-id="67f26-118">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="67f26-119">将中心方法名称和到中心方法中定义的任何自变量传递`InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="67f26-119">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="67f26-120">SignalR 是异步的因此请使用`async`和`await`时进行调用。</span><span class="sxs-lookup"><span data-stu-id="67f26-120">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="67f26-121">从中心调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="67f26-121">Call client methods from hub</span></span>

<span data-ttu-id="67f26-122">定义使用中心调用的方法`connection.On`之后生成过程中，但之前启动连接。</span><span class="sxs-lookup"><span data-stu-id="67f26-122">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

<span data-ttu-id="67f26-123">在前面的代码`connection.On`运行时服务器端代码将调用它使用`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="67f26-123">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="67f26-124">错误处理和日志记录</span><span class="sxs-lookup"><span data-stu-id="67f26-124">Error handling and logging</span></span>

<span data-ttu-id="67f26-125">处理使用 try catch 语句的错误。</span><span class="sxs-lookup"><span data-stu-id="67f26-125">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="67f26-126">检查`Exception`对象确定要执行发生错误后的正确操作。</span><span class="sxs-lookup"><span data-stu-id="67f26-126">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a><span data-ttu-id="67f26-127">其他资源</span><span class="sxs-lookup"><span data-stu-id="67f26-127">Additional resources</span></span>

* [<span data-ttu-id="67f26-128">中心</span><span class="sxs-lookup"><span data-stu-id="67f26-128">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="67f26-129">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="67f26-129">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="67f26-130">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="67f26-130">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)