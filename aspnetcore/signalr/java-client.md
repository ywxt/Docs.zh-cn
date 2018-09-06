---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 09/06/2018
uid: signalr/java-client
ms.openlocfilehash: f110f5391ac34f5cb4a72f64c16d86c8a37369a2
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995409"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="b9f6f-103">ASP.NET Core SignalR Java 客户端</span><span class="sxs-lookup"><span data-stu-id="b9f6f-103">ASP.NET Core SignalR Java Client</span></span>

<span data-ttu-id="b9f6f-104">通过[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="b9f6f-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="b9f6f-105">Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="b9f6f-106">像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="b9f6f-107">Java 客户端是可在 ASP.NET Core 2.2 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="b9f6f-108">在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="b9f6f-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="b9f6f-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="b9f6f-110">SignalR Java 客户端程序包安装</span><span class="sxs-lookup"><span data-stu-id="b9f6f-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="b9f6f-111">*Signalr 0.1.0-preview1 35029* JAR 文件允许客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-111">The *signalr-0.1.0-preview1-35029* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="b9f6f-112">若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav)。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav).</span></span>

<span data-ttu-id="b9f6f-113">如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：</span><span class="sxs-lookup"><span data-stu-id="b9f6f-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.aspnet:signalr:0.1.0-preview1-35029'
```

<span data-ttu-id="b9f6f-114">如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="b9f6f-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="b9f6f-115">连接到中心</span><span class="sxs-lookup"><span data-stu-id="b9f6f-115">Connect to a hub</span></span>

<span data-ttu-id="b9f6f-116">若要建立`HubConnection`，则`HubConnectionBuilder`应使用。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="b9f6f-117">生成连接时，可以配置中心 URL 和日志级别。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="b9f6f-118">配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="b9f6f-119">启动与连接`start`。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=17-20)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="b9f6f-120">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="b9f6f-120">Call hub methods from client</span></span>

<span data-ttu-id="b9f6f-121">调用`send`调用集线器方法。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="b9f6f-122">将中心方法名称和到中心方法中定义的任何参数传递`send`。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=31)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="b9f6f-123">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="b9f6f-123">Call client methods from hub</span></span>

<span data-ttu-id="b9f6f-124">使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="b9f6f-125">构建之后启动连接之前定义的方法。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=22-24)]

## <a name="known-limitations"></a><span data-ttu-id="b9f6f-126">已知限制</span><span class="sxs-lookup"><span data-stu-id="b9f6f-126">Known limitations</span></span>

<span data-ttu-id="b9f6f-127">这是早期的预览版本的 Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-127">This is an early preview release of the Java client.</span></span> <span data-ttu-id="b9f6f-128">有许多功能，目前尚不支持。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-128">There are many features that aren't supported yet.</span></span> <span data-ttu-id="b9f6f-129">正在为将来的版本开发的以下间隔：</span><span class="sxs-lookup"><span data-stu-id="b9f6f-129">The following gaps are being worked on for future releases:</span></span>

* <span data-ttu-id="b9f6f-130">只有基元类型可以作为参数接受和返回类型。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-130">Only primitive types can be accepted as parameters and return types.</span></span>
* <span data-ttu-id="b9f6f-131">Api 是同步的。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-131">The APIs are synchronous.</span></span>
* <span data-ttu-id="b9f6f-132">在此时间支持"发送"的调用类型。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-132">Only the "Send" call type is supported at this time.</span></span> <span data-ttu-id="b9f6f-133">"调用"和流式处理的返回值不受支持。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-133">"Invoke" and streaming of return values aren't supported.</span></span>
* <span data-ttu-id="b9f6f-134">当前不支持客户端[Azure SignalR 服务](/azure/azure-signalr/)。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-134">The client doesn't currently support the [Azure SignalR Service](/azure/azure-signalr/).</span></span>
* <span data-ttu-id="b9f6f-135">支持仅 JSON 协议。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-135">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="b9f6f-136">支持仅 Websocket 传输。</span><span class="sxs-lookup"><span data-stu-id="b9f6f-136">Only the WebSockets transport is supported.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9f6f-137">其他资源</span><span class="sxs-lookup"><span data-stu-id="b9f6f-137">Additional resources</span></span>

* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
