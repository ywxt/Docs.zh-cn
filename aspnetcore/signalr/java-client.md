---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 10/18/2018
uid: signalr/java-client
ms.openlocfilehash: 3d2cfe5f58cc41741512c68cebbbc90e8f714cba
ms.sourcegitcommit: 54655f1e1abf0b64d19506334d94cfdb0caf55f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148780"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="3f7b2-103">ASP.NET Core SignalR Java 客户端</span><span class="sxs-lookup"><span data-stu-id="3f7b2-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="3f7b2-104">通过[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="3f7b2-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="3f7b2-105">Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="3f7b2-106">像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="3f7b2-107">Java 客户端是可在 ASP.NET Core 2.2 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="3f7b2-108">在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="3f7b2-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="3f7b2-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="3f7b2-110">SignalR Java 客户端程序包安装</span><span class="sxs-lookup"><span data-stu-id="3f7b2-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="3f7b2-111">*Signalr 1.0.0-preview3 35501* JAR 文件允许客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-111">The *signalr-1.0.0-preview3-35501* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="3f7b2-112">若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="3f7b2-113">如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：</span><span class="sxs-lookup"><span data-stu-id="3f7b2-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0-preview3-35501'
implementation 'io.reactivex.rxjava2:rxjava:2.2.2'
```

<span data-ttu-id="3f7b2-114">如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="3f7b2-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="3f7b2-115">连接到中心</span><span class="sxs-lookup"><span data-stu-id="3f7b2-115">Connect to a hub</span></span>

<span data-ttu-id="3f7b2-116">若要建立`HubConnection`，则`HubConnectionBuilder`应使用。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="3f7b2-117">生成连接时，可以配置中心 URL 和日志级别。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="3f7b2-118">配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="3f7b2-119">启动与连接`start`。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="3f7b2-120">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="3f7b2-120">Call hub methods from client</span></span>

<span data-ttu-id="3f7b2-121">调用`send`调用集线器方法。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="3f7b2-122">将中心方法名称和到中心方法中定义的任何参数传递`send`。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="3f7b2-123">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="3f7b2-123">Call client methods from hub</span></span>

<span data-ttu-id="3f7b2-124">使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="3f7b2-125">构建之后启动连接之前定义的方法。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="3f7b2-126">添加日志记录</span><span class="sxs-lookup"><span data-stu-id="3f7b2-126">Add logging</span></span>

<span data-ttu-id="3f7b2-127">SignalR Java 客户端使用[SLF4J](https://www.slf4j.org/)用于日志记录库。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="3f7b2-128">它是库的一个高级日志记录 API，允许通过将特定的日志记录依赖项中选择其自己特定的日志记录实现的用户。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="3f7b2-129">下面的代码段演示如何使用`java.util.logging`的 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="3f7b2-130">如果没有配置依赖项中的日志记录，SLF4J 加载具有以下警告消息的默认无操作记录器：</span><span class="sxs-lookup"><span data-stu-id="3f7b2-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="3f7b2-131">这可以安全地忽略。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-131">This can safely be ignored.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="3f7b2-132">已知限制</span><span class="sxs-lookup"><span data-stu-id="3f7b2-132">Known limitations</span></span>

<span data-ttu-id="3f7b2-133">这是预览版本的 Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-133">This is a preview release of the Java client.</span></span> <span data-ttu-id="3f7b2-134">不支持某些功能：</span><span class="sxs-lookup"><span data-stu-id="3f7b2-134">Some features aren't supported:</span></span>

* <span data-ttu-id="3f7b2-135">支持仅 JSON 协议。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-135">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="3f7b2-136">支持仅 Websocket 传输。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-136">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="3f7b2-137">流式处理尚不支持。</span><span class="sxs-lookup"><span data-stu-id="3f7b2-137">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f7b2-138">其他资源</span><span class="sxs-lookup"><span data-stu-id="3f7b2-138">Additional resources</span></span>

* [<span data-ttu-id="3f7b2-139">Java API 参考</span><span class="sxs-lookup"><span data-stu-id="3f7b2-139">Java API reference</span></span>](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
