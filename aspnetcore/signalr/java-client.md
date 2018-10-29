---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 10/18/2018
uid: signalr/java-client
ms.openlocfilehash: 646118c78d5d38b44b89d399cd06a5332a11d064
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207766"
---
# <a name="aspnet-core-signalr-java-client"></a>ASP.NET Core SignalR Java 客户端

通过[Mikael Mengistu](https://twitter.com/MikaelM_12)

Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。 像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。 Java 客户端是可在 ASP.NET Core 2.2 及更高版本。

在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="install-the-signalr-java-client-package"></a>SignalR Java 客户端程序包安装

*Signalr 1.0.0-preview3 35501* JAR 文件允许客户端连接到 SignalR 集线器。 若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)。

如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0-preview3-35501'
implementation 'io.reactivex.rxjava2:rxjava:2.2.2'
```

如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a>连接到中心

若要建立`HubConnection`，则`HubConnectionBuilder`应使用。 生成连接时，可以配置中心 URL 和日志级别。 配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。 启动与连接`start`。

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a>从客户端调用集线器方法

调用`send`调用集线器方法。 将中心方法名称和到中心方法中定义的任何参数传递`send`。

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a>从集线器调用客户端方法

使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。 构建之后启动连接之前定义的方法。

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a>添加日志记录

SignalR Java 客户端使用[SLF4J](https://www.slf4j.org/)用于日志记录库。 它是库的一个高级日志记录 API，允许通过将特定的日志记录依赖项中选择其自己特定的日志记录实现的用户。 下面的代码段演示如何使用`java.util.logging`的 SignalR Java 客户端。

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

如果没有配置依赖项中的日志记录，SLF4J 加载具有以下警告消息的默认无操作记录器：

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

这可以安全地忽略。

## <a name="known-limitations"></a>已知限制

这是预览版本的 Java 客户端。 不支持某些功能：

* 支持仅 JSON 协议。
* 支持仅 Websocket 传输。
* 流式处理尚不支持。

## <a name="additional-resources"></a>其他资源

* [Java API 参考](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
