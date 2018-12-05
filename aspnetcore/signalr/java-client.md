---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 11/07/2018
uid: signalr/java-client
ms.openlocfilehash: d0eff38c1f622b896ed1dc3002238aec7b6bfd38
ms.sourcegitcommit: 8a65f6c2cbe290fb2418eed58f60fb74c95392c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2018
ms.locfileid: "52892089"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="78b62-103">ASP.NET Core SignalR Java 客户端</span><span class="sxs-lookup"><span data-stu-id="78b62-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="78b62-104">通过[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="78b62-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="78b62-105">Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。</span><span class="sxs-lookup"><span data-stu-id="78b62-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="78b62-106">像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。</span><span class="sxs-lookup"><span data-stu-id="78b62-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="78b62-107">Java 客户端是可在 ASP.NET Core 2.2 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="78b62-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="78b62-108">在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="78b62-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="78b62-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="78b62-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="78b62-110">SignalR Java 客户端程序包安装</span><span class="sxs-lookup"><span data-stu-id="78b62-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="78b62-111">*Signalr 1.0.0* JAR 文件允许客户端连接到 SignalR 集线器。</span><span class="sxs-lookup"><span data-stu-id="78b62-111">The *signalr-1.0.0* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="78b62-112">若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)。</span><span class="sxs-lookup"><span data-stu-id="78b62-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="78b62-113">如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：</span><span class="sxs-lookup"><span data-stu-id="78b62-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0'
```

<span data-ttu-id="78b62-114">如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="78b62-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="78b62-115">连接到中心</span><span class="sxs-lookup"><span data-stu-id="78b62-115">Connect to a hub</span></span>

<span data-ttu-id="78b62-116">若要建立`HubConnection`，则`HubConnectionBuilder`应使用。</span><span class="sxs-lookup"><span data-stu-id="78b62-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="78b62-117">生成连接时，可以配置中心 URL 和日志级别。</span><span class="sxs-lookup"><span data-stu-id="78b62-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="78b62-118">配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。</span><span class="sxs-lookup"><span data-stu-id="78b62-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="78b62-119">启动与连接`start`。</span><span class="sxs-lookup"><span data-stu-id="78b62-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="78b62-120">从客户端调用集线器方法</span><span class="sxs-lookup"><span data-stu-id="78b62-120">Call hub methods from client</span></span>

<span data-ttu-id="78b62-121">调用`send`调用集线器方法。</span><span class="sxs-lookup"><span data-stu-id="78b62-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="78b62-122">将中心方法名称和到中心方法中定义的任何参数传递`send`。</span><span class="sxs-lookup"><span data-stu-id="78b62-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="78b62-123">从集线器调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="78b62-123">Call client methods from hub</span></span>

<span data-ttu-id="78b62-124">使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。</span><span class="sxs-lookup"><span data-stu-id="78b62-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="78b62-125">构建之后启动连接之前定义的方法。</span><span class="sxs-lookup"><span data-stu-id="78b62-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="78b62-126">添加日志记录</span><span class="sxs-lookup"><span data-stu-id="78b62-126">Add logging</span></span>

<span data-ttu-id="78b62-127">SignalR Java 客户端使用[SLF4J](https://www.slf4j.org/)用于日志记录库。</span><span class="sxs-lookup"><span data-stu-id="78b62-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="78b62-128">它是库的一个高级日志记录 API，允许通过将特定的日志记录依赖项中选择其自己特定的日志记录实现的用户。</span><span class="sxs-lookup"><span data-stu-id="78b62-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="78b62-129">下面的代码段演示如何使用`java.util.logging`的 SignalR Java 客户端。</span><span class="sxs-lookup"><span data-stu-id="78b62-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="78b62-130">如果没有配置依赖项中的日志记录，SLF4J 加载具有以下警告消息的默认无操作记录器：</span><span class="sxs-lookup"><span data-stu-id="78b62-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="78b62-131">这可以安全地忽略。</span><span class="sxs-lookup"><span data-stu-id="78b62-131">This can safely be ignored.</span></span>

## <a name="android-development-notes"></a><span data-ttu-id="78b62-132">Android 开发说明</span><span class="sxs-lookup"><span data-stu-id="78b62-132">Android development notes</span></span>

<span data-ttu-id="78b62-133">与 SignalR 客户端功能的 Android SDK 兼容性时，请考虑以下各项指定你的目标 Android SDK 版本：</span><span class="sxs-lookup"><span data-stu-id="78b62-133">With regards to Android SDK compatibility for the SignalR client features, consider the following items when specifying your target Android SDK version:</span></span>

* <span data-ttu-id="78b62-134">SignalR Java 客户端将运行 Android API 级别 16 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="78b62-134">The SignalR Java Client will run on Android API Level 16 and later.</span></span>
* <span data-ttu-id="78b62-135">通过 Azure SignalR 服务连接将需要 20 及更高版本的 Android API 级别因为[Azure SignalR 服务](/azure/azure-signalr/signalr-overview)需要 TLS 1.2，并且不支持基于 SHA-1 的密码套件。</span><span class="sxs-lookup"><span data-stu-id="78b62-135">Connecting through the Azure SignalR Service will require Android API Level 20 and later because the [Azure SignalR Service](/azure/azure-signalr/signalr-overview) requires TLS 1.2 and doesn't support SHA-1-based cipher suites.</span></span> <span data-ttu-id="78b62-136">Android[添加支持 SHA-256 （和更高版本） 的密码套件](https://developer.android.com/reference/javax/net/ssl/SSLSocket)API 20 级中。</span><span class="sxs-lookup"><span data-stu-id="78b62-136">Android [added support for SHA-256 (and above) cipher suites](https://developer.android.com/reference/javax/net/ssl/SSLSocket) in API Level 20.</span></span>

## <a name="configure-bearer-token-authentication"></a><span data-ttu-id="78b62-137">配置持有者令牌身份验证</span><span class="sxs-lookup"><span data-stu-id="78b62-137">Configure bearer token authentication</span></span>

<span data-ttu-id="78b62-138">在 SignalR Java 客户端，可配置的持有者令牌，用于通过提供"访问令牌工厂"进行身份验证，向[HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java)。</span><span class="sxs-lookup"><span data-stu-id="78b62-138">In the SignalR Java client, you can configure a bearer token to use for authentication by providing an "access token factory" to the [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span></span> <span data-ttu-id="78b62-139">使用[withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__)提供[RxJava](https://github.com/ReactiveX/RxJava) [单一<String>](http://reactivex.io/documentation/single.html)。</span><span class="sxs-lookup"><span data-stu-id="78b62-139">Use [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) to provide an [RxJava](https://github.com/ReactiveX/RxJava) [Single<String>](http://reactivex.io/documentation/single.html).</span></span> <span data-ttu-id="78b62-140">通过调用[Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-)，可以编写逻辑来为您的客户端生成访问令牌。</span><span class="sxs-lookup"><span data-stu-id="78b62-140">With a call to [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), you can write logic to produce access tokens for your client.</span></span>

```java
HubConnection hubConnection = HubConnectionBuilder.create("YOUR HUB URL HERE")
    .withAccessTokenProvider(Single.defer(() -> {
        // Your logic here.
        return Single.just("An Access Token");
    })).build();
```

## <a name="known-limitations"></a><span data-ttu-id="78b62-141">已知限制</span><span class="sxs-lookup"><span data-stu-id="78b62-141">Known limitations</span></span>

* <span data-ttu-id="78b62-142">支持仅 JSON 协议。</span><span class="sxs-lookup"><span data-stu-id="78b62-142">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="78b62-143">支持仅 Websocket 传输。</span><span class="sxs-lookup"><span data-stu-id="78b62-143">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="78b62-144">流式处理尚不支持。</span><span class="sxs-lookup"><span data-stu-id="78b62-144">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78b62-145">其他资源</span><span class="sxs-lookup"><span data-stu-id="78b62-145">Additional resources</span></span>

* [<span data-ttu-id="78b62-146">Java API 参考</span><span class="sxs-lookup"><span data-stu-id="78b62-146">Java API reference</span></span>](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
