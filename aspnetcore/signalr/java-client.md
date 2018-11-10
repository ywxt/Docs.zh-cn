---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 11/06/2018
uid: signalr/java-client
ms.openlocfilehash: 4ee4e61fc301ebeec4d95b1167f94f16c38f3ac5
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225416"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="78fbd-103">ASP.NET Core SignalR Java 客户端</span><span class="sxs-lookup"><span data-stu-id="78fbd-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="78fbd-104">通过[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="78fbd-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="78fbd-105">Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。</span><span class="sxs-lookup"><span data-stu-id="78fbd-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="78fbd-106">像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。</span><span class="sxs-lookup"><span data-stu-id="78fbd-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="78fbd-107">Java 客户端是可在 ASP.NET Core 2.2 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="78fbd-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="78fbd-108">在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="78fbd-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="78fbd-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="78fbd-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="78fbd-110">SignalR Java 客户端程序包安装</span><span class="sxs-lookup"><span data-stu-id="78fbd-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="78fbd-111">*Signalr 1.0.0-preview3 35501* JAR 文件允许客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="78fbd-111">The *signalr-1.0.0-preview3-35501* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="78fbd-112">若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)。</span><span class="sxs-lookup"><span data-stu-id="78fbd-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="78fbd-113">如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：</span><span class="sxs-lookup"><span data-stu-id="78fbd-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0-preview3-35501'
implementation 'io.reactivex.rxjava2:rxjava:2.2.2'
```

<span data-ttu-id="78fbd-114">如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="78fbd-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="78fbd-115">连接到中心</span><span class="sxs-lookup"><span data-stu-id="78fbd-115">Connect to a hub</span></span>

<span data-ttu-id="78fbd-116">若要建立`HubConnection`，则`HubConnectionBuilder`应使用。</span><span class="sxs-lookup"><span data-stu-id="78fbd-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="78fbd-117">生成连接时，可以配置中心 URL 和日志级别。</span><span class="sxs-lookup"><span data-stu-id="78fbd-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="78fbd-118">配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。</span><span class="sxs-lookup"><span data-stu-id="78fbd-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="78fbd-119">启动与连接`start`。</span><span class="sxs-lookup"><span data-stu-id="78fbd-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="78fbd-120">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="78fbd-120">Call hub methods from client</span></span>

<span data-ttu-id="78fbd-121">调用`send`调用集线器方法。</span><span class="sxs-lookup"><span data-stu-id="78fbd-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="78fbd-122">将中心方法名称和到中心方法中定义的任何参数传递`send`。</span><span class="sxs-lookup"><span data-stu-id="78fbd-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="78fbd-123">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="78fbd-123">Call client methods from hub</span></span>

<span data-ttu-id="78fbd-124">使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。</span><span class="sxs-lookup"><span data-stu-id="78fbd-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="78fbd-125">构建之后启动连接之前定义的方法。</span><span class="sxs-lookup"><span data-stu-id="78fbd-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="78fbd-126">添加日志记录</span><span class="sxs-lookup"><span data-stu-id="78fbd-126">Add logging</span></span>

<span data-ttu-id="78fbd-127">SignalR Java 客户端使用[SLF4J](https://www.slf4j.org/)用于日志记录库。</span><span class="sxs-lookup"><span data-stu-id="78fbd-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="78fbd-128">它是库的一个高级日志记录 API，允许通过将特定的日志记录依赖项中选择其自己特定的日志记录实现的用户。</span><span class="sxs-lookup"><span data-stu-id="78fbd-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="78fbd-129">下面的代码段演示如何使用`java.util.logging`的 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="78fbd-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="78fbd-130">如果没有配置依赖项中的日志记录，SLF4J 加载具有以下警告消息的默认无操作记录器：</span><span class="sxs-lookup"><span data-stu-id="78fbd-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="78fbd-131">这可以安全地忽略。</span><span class="sxs-lookup"><span data-stu-id="78fbd-131">This can safely be ignored.</span></span>


## <a name="configure-bearer-token-authentication"></a><span data-ttu-id="78fbd-132">配置持有者令牌身份验证</span><span class="sxs-lookup"><span data-stu-id="78fbd-132">Configure bearer token authentication</span></span>

<span data-ttu-id="78fbd-133">在 SignalR Java 客户端，可配置的持有者令牌，用于通过提供"访问令牌工厂"进行身份验证，向[HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java)。</span><span class="sxs-lookup"><span data-stu-id="78fbd-133">In the SignalR Java client, you can configure a bearer token to use for authentication by providing an "access token factory" to the [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span></span> <span data-ttu-id="78fbd-134">使用[withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__)提供[RxJava](https://github.com/ReactiveX/RxJava) [单一<String>](http://reactivex.io/documentation/single.html)。</span><span class="sxs-lookup"><span data-stu-id="78fbd-134">Use [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) to provide an [RxJava](https://github.com/ReactiveX/RxJava) [Single<String>](http://reactivex.io/documentation/single.html).</span></span> <span data-ttu-id="78fbd-135">通过调用[Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-)，可以编写逻辑来为您的客户端生成访问令牌。</span><span class="sxs-lookup"><span data-stu-id="78fbd-135">With a call to [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), you can write logic to produce access tokens for your client.</span></span>

```java
HubConnection hubConnection = HubConnectionBuilder.create("YOUR HUB URL HERE")
    .withAccessTokenProvider(Single.defer(() -> {
        // Your logic here.
        return Single.just("An Access Token");
    })).build();
```

## <a name="known-limitations"></a><span data-ttu-id="78fbd-136">已知限制</span><span class="sxs-lookup"><span data-stu-id="78fbd-136">Known limitations</span></span>

<span data-ttu-id="78fbd-137">这是预览版本的 Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="78fbd-137">This is a preview release of the Java client.</span></span> <span data-ttu-id="78fbd-138">不支持某些功能：</span><span class="sxs-lookup"><span data-stu-id="78fbd-138">Some features aren't supported:</span></span>

* <span data-ttu-id="78fbd-139">支持仅 JSON 协议。</span><span class="sxs-lookup"><span data-stu-id="78fbd-139">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="78fbd-140">支持仅 Websocket 传输。</span><span class="sxs-lookup"><span data-stu-id="78fbd-140">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="78fbd-141">流式处理尚不支持。</span><span class="sxs-lookup"><span data-stu-id="78fbd-141">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78fbd-142">其他资源</span><span class="sxs-lookup"><span data-stu-id="78fbd-142">Additional resources</span></span>

* [<span data-ttu-id="78fbd-143">Java API 参考</span><span class="sxs-lookup"><span data-stu-id="78fbd-143">Java API reference</span></span>](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
