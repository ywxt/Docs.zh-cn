---
title: ASP.NET Core SignalR.NET 客户端
author: tdykstra
description: 有关 ASP.NET Core SignalR.NET 客户端信息
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/10/2018
uid: signalr/dotnet-client
ms.openlocfilehash: 205ca8ca228dcc2cc77f7e9b6431943851a3b152
ms.sourcegitcommit: 1a2fc47fb5d3da0f2a3c3269613ab20eb3b0da2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2018
ms.locfileid: "44373314"
---
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="3c955-103">ASP.NET Core SignalR.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="3c955-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="3c955-104">作者：[Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="3c955-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="3c955-105">ASP.NET Core SignalR.NET 客户端库可让你与 SignalR 集线器从.NET 应用程序进行通信。</span><span class="sxs-lookup"><span data-stu-id="3c955-105">The ASP.NET Core SignalR .NET client library lets you communicate with SignalR hubs from .NET apps.</span></span>

> [!NOTE]
> <span data-ttu-id="3c955-106">Xamarin 有特殊要求 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="3c955-106">Xamarin has special requirements for Visual Studio version.</span></span> <span data-ttu-id="3c955-107">有关详细信息，请参阅[在 Xamarin 中的 SignalR 客户端 2.1.1](https://github.com/aspnet/Announcements/issues/305)。</span><span class="sxs-lookup"><span data-stu-id="3c955-107">For more information, see [SignalR Client 2.1.1 in Xamarin](https://github.com/aspnet/Announcements/issues/305).</span></span>

<span data-ttu-id="3c955-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="3c955-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="3c955-109">这篇文章中的代码示例是使用 ASP.NET Core SignalR.NET 客户端的 WPF 应用。</span><span class="sxs-lookup"><span data-stu-id="3c955-109">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="install-the-signalr-net-client-package"></a><span data-ttu-id="3c955-110">安装 SignalR.NET 客户端包</span><span class="sxs-lookup"><span data-stu-id="3c955-110">Install the SignalR .NET client package</span></span>

<span data-ttu-id="3c955-111">`Microsoft.AspNetCore.SignalR.Client`包所需的.NET 客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="3c955-111">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="3c955-112">若要安装客户端库，请运行以下命令**程序包管理器控制台**窗口：</span><span class="sxs-lookup"><span data-stu-id="3c955-112">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="3c955-113">连接到中心</span><span class="sxs-lookup"><span data-stu-id="3c955-113">Connect to a hub</span></span>

<span data-ttu-id="3c955-114">若要建立连接，创建`HubConnectionBuilder`，并调用`Build`。</span><span class="sxs-lookup"><span data-stu-id="3c955-114">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="3c955-115">生成一个连接时，可以配置中心 URL、 协议、 传输类型、 日志级别、 标头，和其他选项。</span><span class="sxs-lookup"><span data-stu-id="3c955-115">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="3c955-116">配置任何必需的选项的方法是插入的任何`HubConnectionBuilder`方法转换`Build`。</span><span class="sxs-lookup"><span data-stu-id="3c955-116">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="3c955-117">启动与连接`StartAsync`。</span><span class="sxs-lookup"><span data-stu-id="3c955-117">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_MainWindowClass&highlight=14-16,32)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="3c955-118">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="3c955-118">Call hub methods from client</span></span>

<span data-ttu-id="3c955-119">`InvokeAsync` 在该中心将调用方法。</span><span class="sxs-lookup"><span data-stu-id="3c955-119">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="3c955-120">将中心方法名称和到中心方法中定义的任何参数传递`InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="3c955-120">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="3c955-121">SignalR 是异步的因此请使用`async`和`await`时进行调用。</span><span class="sxs-lookup"><span data-stu-id="3c955-121">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_InvokeAsync)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="3c955-122">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="3c955-122">Call client methods from hub</span></span>

<span data-ttu-id="3c955-123">定义使用集线器调用的方法`connection.On`之后生成，但之前启动连接。</span><span class="sxs-lookup"><span data-stu-id="3c955-123">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ConnectionOn)]

<span data-ttu-id="3c955-124">在前面的代码`connection.On`运行时服务器端代码将调用它使用`SendAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="3c955-124">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?name=snippet_SendMessage)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="3c955-125">错误处理和日志记录</span><span class="sxs-lookup"><span data-stu-id="3c955-125">Error handling and logging</span></span>

<span data-ttu-id="3c955-126">处理 try catch 语句的错误。</span><span class="sxs-lookup"><span data-stu-id="3c955-126">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="3c955-127">检查`Exception`对象，以确定要执行后发生错误的适当操作。</span><span class="sxs-lookup"><span data-stu-id="3c955-127">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ErrorHandling)]

## <a name="additional-resources"></a><span data-ttu-id="3c955-128">其他资源</span><span class="sxs-lookup"><span data-stu-id="3c955-128">Additional resources</span></span>

* [<span data-ttu-id="3c955-129">中心</span><span class="sxs-lookup"><span data-stu-id="3c955-129">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="3c955-130">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="3c955-130">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="3c955-131">发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="3c955-131">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
