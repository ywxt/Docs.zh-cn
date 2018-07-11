---
title: ASP.NET Core SignalR.NET 客户端
author: rachelappel
description: 有关 ASP.NET Core SignalR.NET 客户端信息
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/29/2018
uid: signalr/dotnet-client
ms.openlocfilehash: 35dc1d3abf0d35e17d1835ec462f8cc4feb728eb
ms.sourcegitcommit: 661d30492d5ef7bbca4f7e709f40d8f3309d2dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2018
ms.locfileid: "37938249"
---
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="0cd29-103">ASP.NET Core SignalR.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="0cd29-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="0cd29-104">作者：[Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="0cd29-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="0cd29-105">ASP.NET Core SignalR.NET 客户端可以使用 Xamarin、 WPF、 Windows 窗体，控制台中和.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="0cd29-105">The ASP.NET Core SignalR .NET client can be used by Xamarin, WPF, Windows Forms, Console, and .NET Core apps.</span></span> <span data-ttu-id="0cd29-106">像[JavaScript 客户端](xref:signalr/javascript-client)，.NET 客户端，可以接收和发送并实时接收到的集线器的消息。</span><span class="sxs-lookup"><span data-stu-id="0cd29-106">Like the [JavaScript client](xref:signalr/javascript-client), the .NET client enables you to receive and send and receive messages to a hub in real time.</span></span>

<span data-ttu-id="0cd29-107">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="0cd29-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="0cd29-108">这篇文章中的代码示例是使用 ASP.NET Core SignalR.NET 客户端的 WPF 应用。</span><span class="sxs-lookup"><span data-stu-id="0cd29-108">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="install-the-signalr-net-client-package"></a><span data-ttu-id="0cd29-109">安装 SignalR.NET 客户端包</span><span class="sxs-lookup"><span data-stu-id="0cd29-109">Install the SignalR .NET client package</span></span>

<span data-ttu-id="0cd29-110">`Microsoft.AspNetCore.SignalR.Client`包所需的.NET 客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="0cd29-110">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="0cd29-111">若要安装客户端库，请运行以下命令**程序包管理器控制台**窗口：</span><span class="sxs-lookup"><span data-stu-id="0cd29-111">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="0cd29-112">连接到中心</span><span class="sxs-lookup"><span data-stu-id="0cd29-112">Connect to a hub</span></span>

<span data-ttu-id="0cd29-113">若要建立连接，创建`HubConnectionBuilder`，并调用`Build`。</span><span class="sxs-lookup"><span data-stu-id="0cd29-113">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="0cd29-114">生成一个连接时，可以配置中心 URL、 协议、 传输类型、 日志级别、 标头，和其他选项。</span><span class="sxs-lookup"><span data-stu-id="0cd29-114">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="0cd29-115">配置任何必需的选项的方法是插入的任何`HubConnectionBuilder`方法转换`Build`。</span><span class="sxs-lookup"><span data-stu-id="0cd29-115">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="0cd29-116">启动与连接`StartAsync`。</span><span class="sxs-lookup"><span data-stu-id="0cd29-116">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="0cd29-117">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="0cd29-117">Call hub methods from client</span></span>

<span data-ttu-id="0cd29-118">`InvokeAsync` 在该中心将调用方法。</span><span class="sxs-lookup"><span data-stu-id="0cd29-118">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="0cd29-119">将中心方法名称和到中心方法中定义的任何参数传递`InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="0cd29-119">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="0cd29-120">SignalR 是异步的因此请使用`async`和`await`时进行调用。</span><span class="sxs-lookup"><span data-stu-id="0cd29-120">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="0cd29-121">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="0cd29-121">Call client methods from hub</span></span>

<span data-ttu-id="0cd29-122">定义使用集线器调用的方法`connection.On`之后生成，但之前启动连接。</span><span class="sxs-lookup"><span data-stu-id="0cd29-122">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

<span data-ttu-id="0cd29-123">在前面的代码`connection.On`运行时服务器端代码将调用它使用`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="0cd29-123">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="0cd29-124">错误处理和日志记录</span><span class="sxs-lookup"><span data-stu-id="0cd29-124">Error handling and logging</span></span>

<span data-ttu-id="0cd29-125">处理 try catch 语句的错误。</span><span class="sxs-lookup"><span data-stu-id="0cd29-125">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="0cd29-126">检查`Exception`对象，以确定要执行后发生错误的适当操作。</span><span class="sxs-lookup"><span data-stu-id="0cd29-126">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a><span data-ttu-id="0cd29-127">其他资源</span><span class="sxs-lookup"><span data-stu-id="0cd29-127">Additional resources</span></span>

* [<span data-ttu-id="0cd29-128">中心</span><span class="sxs-lookup"><span data-stu-id="0cd29-128">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="0cd29-129">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="0cd29-129">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="0cd29-130">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="0cd29-130">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
