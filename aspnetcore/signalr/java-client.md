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
# <a name="aspnet-core-signalr-java-client"></a>ASP.NET Core SignalR Java 客户端

通过[Mikael Mengistu](https://twitter.com/MikaelM_12)

Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。 像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。 Java 客户端是可在 ASP.NET Core 2.2 及更高版本。

在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="install-the-signalr-java-client-package"></a>SignalR Java 客户端程序包安装

*Signalr 0.1.0-preview1 35029* JAR 文件允许客户端连接到 SignalR 集线器。 若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav)。

如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：

```gradle
implementation 'com.microsoft.aspnet:signalr:0.1.0-preview1-35029'
```

如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a>连接到中心

若要建立`HubConnection`，则`HubConnectionBuilder`应使用。 生成连接时，可以配置中心 URL 和日志级别。 配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。 启动与连接`start`。

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=17-20)]

## <a name="call-hub-methods-from-client"></a>从客户端调用集线器方法

调用`send`调用集线器方法。 将中心方法名称和到中心方法中定义的任何参数传递`send`。

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=31)]

## <a name="call-client-methods-from-hub"></a>从集线器调用客户端方法

使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。 构建之后启动连接之前定义的方法。

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=22-24)]

## <a name="known-limitations"></a>已知限制

这是早期的预览版本的 Java 客户端。 有许多功能，目前尚不支持。 正在为将来的版本开发的以下间隔：

* 只有基元类型可以作为参数接受和返回类型。
* Api 是同步的。
* 在此时间支持"发送"的调用类型。 "调用"和流式处理的返回值不受支持。
* 当前不支持客户端[Azure SignalR 服务](/azure/azure-signalr/)。
* 支持仅 JSON 协议。
* 支持仅 Websocket 传输。

## <a name="additional-resources"></a>其他资源

* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
