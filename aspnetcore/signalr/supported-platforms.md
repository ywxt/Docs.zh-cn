---
title: ASP.NET Core SignalR 支持的平台
author: tdykstra
description: 了解 ASP.NET Core SignalR 支持的平台。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/31/2018
uid: signalr/supported-platforms
ms.openlocfilehash: 773f6c020dbb2982911e177b55855473c750d52a
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758175"
---
# <a name="aspnet-core-signalr-supported-platforms"></a>ASP.NET Core SignalR 支持的平台

## <a name="server-system-requirements"></a>服务器系统要求

适用于 ASP.NET Core SignalR 支持 ASP.NET Core 支持的任何服务器平台。

## <a name="javascript-client"></a>JavaScript 客户端

[JavaScript 客户端](https://www.npmjs.com/package/@aspnet/signalr)NodeJS 8 和更高版本和以下浏览器上运行：

| 浏览者                         | 版本 |
| ------------------------------- | ------- |
| Microsoft Edge                  | 当前 |
| Mozilla Firefox                 | 当前 |
| Google Chrome;包括 Android | 当前 |
| Safari;包含 iOS            | 当前 |
| Microsoft Internet Explorer     | 11      |
 
## <a name="net-client"></a>.NET 客户端

[.NET 客户端](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/)在 ASP.NET Core 支持的任何服务器平台上运行。

如果服务器运行 IIS，Websocket 传输要求安装 IIS 8.0 或更高版本 Windows Server 2012 或更高版本。 其他传输在所有平台上都受支持。

## <a name="java-client"></a>Java 客户端

[Java 客户端](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)支持 Java 8 和更高版本。

## <a name="unsupported-clients"></a>不受支持的客户端

以下客户端可用，但会实验性的或非官方。 它们目前不支持，因此可能永远不可。

* [C + + 客户端](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [Swift 的客户端](https://github.com/moozzyk/SignalR-Client-Swift)
