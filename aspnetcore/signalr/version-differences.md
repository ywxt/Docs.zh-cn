---
title: SignalR 和 ASP.NET Core SignalR 之间的差异
author: tdykstra
description: SignalR 和 ASP.NET Core SignalR 之间的差异
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 11/14/2018
uid: signalr/version-differences
ms.openlocfilehash: c9302f1c9e7cd4e62eaeaef871feb54ef26aa3ca
ms.sourcegitcommit: 09bcda59a58019fdf47b2db5259fe87acf19dd38
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51708408"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a>ASP.NET SignalR 和 ASP.NET Core SignalR 之间的差异

ASP.NET Core SignalR 不允许客户端或 ASP.NET SignalR 的服务器。 本文详细介绍了已删除或更改在 ASP.NET Core SignalR 中的功能。

## <a name="how-to-identify-the-signalr-version"></a>如何识别 SignalR 版本

|                      | ASP.NET SignalR | ASP.NET Core SignalR |
| -------------------- | --------------- | -------------------- |
| 服务器 NuGet 包 | [Microsoft.AspNet.SignalR](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)<br>[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework) |
| 客户端 NuGet 包 | [Microsoft.AspNet.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[Microsoft.AspNet.SignalR.JS](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [Microsoft.AspNetCore.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| 客户端 npm 包 | [signalr](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| 服务器应用程序类型 | ASP.NET (System.Web) 或 OWIN 自托管 | ASP.NET Core |
| 受支持的服务器平台 | .NET framework 4.5 或更高版本 | .NET Framework 4.6.1 或更高版本<br>.NET core 2.1 或更高版本 |

## <a name="feature-differences"></a>功能差异

### <a name="automatic-reconnects"></a>自动重新连接

在 ASP.NET Core SignalR 中不支持自动重新连接。 如果客户端已断开连接，用户必须显式会启动新的连接，如果用户想要重新连接。 在 ASP.NET SignalR，SignalR 尝试重新连接到服务器，如果在连接断开。 

### <a name="protocol-support"></a>协议支持

ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。 此外，可以创建自定义协议。

### <a name="transports"></a>传输

在 ASP.NET Core SignalR 中不支持永久帧传输。

## <a name="differences-on-the-server"></a>在服务器上的差异

ASP.NET Core SignalR 服务器端库包含在[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)包的一部分**ASP.NET Core Web 应用程序**Razor 和 MVC 模板项目。

ASP.NET Core SignalR 是 ASP.NET Core 中间件，因此它必须通过调用配置[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)中`Startup.ConfigureServices`。

```csharp
services.AddSignalR()
```

若要配置路由，请将路由映射到中心内[UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr)方法调用中`Startup.Configure`方法。

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a>粘性会话

ASP.NET SignalR 的横向扩展模型允许客户端重新连接，并将消息发送到服务器场中的任何服务器。 在 ASP.NET Core SignalR 客户端必须进行交互与同一台服务器连接的持续时间。 有关使用 Redis 的横向扩展，这意味着粘性会话是必需的。 使用横向扩展[Azure SignalR 服务](/azure/azure-signalr/)，因为该服务处理客户端连接不需要粘性会话。 

### <a name="single-hub-per-connection"></a>每个连接的单个中心

在 ASP.NET Core SignalR 连接模型进行了简化。 直接向单个中心，而不是单个连接正在使用共享到多个中心的访问权限进行连接。

### <a name="streaming"></a>流式处理

ASP.NET Core SignalR 现在支持[流式处理数据](xref:signalr/streaming)从中心向客户端。

### <a name="state"></a>状态

已删除将任意状态传递客户端与中心 （通常称为 HubState） 之间的功能，以及对进度消息的支持。 目前中心代理没有对应。

### <a name="persistentconnection-removal"></a>PersistentConnection 删除

在 ASP.NET Core SignalR [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118))类已删除。 

### <a name="globalhost"></a>GlobalHost

ASP.NET Core 具有内置于 framework 的依赖关系注入 (DI)。 服务可以使用 DI 来访问[HubContext](xref:signalr/hubcontext)。 `GlobalHost`对象，ASP.NET SignalR 中用来实现`HubContext`ASP.NET Core SignalR 中不存在。

### <a name="hubpipeline"></a>HubPipeline

ASP.NET Core SignalR 不具有对支持`HubPipeline`模块。

## <a name="differences-on-the-client"></a>在客户端上的差异

### <a name="typescript"></a>TypeScript

ASP.NET Core SignalR 客户端用[TypeScript](https://www.typescriptlang.org/)。 使用时，可以编写 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>JavaScript 客户端托管于[npm](https://www.npmjs.com/)

在上一版本中，JavaScript 客户端已通过在 Visual Studio 中的 NuGet 包获取。 对于核心版本中， [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 包中包含的 JavaScript 库。 此包不包括在**ASP.NET Core Web 应用程序**模板。 使用 npm 获取并安装`@aspnet/signalr`npm 包。

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

已删除对 jQuery 的依赖关系，但项目仍然可以使用 jQuery。

### <a name="internet-explorer-support"></a>Internet Explorer 支持

ASP.NET Core SignalR 要求 （ASP.NET SignalR 支持 Microsoft Internet Explorer 8 及更高版本） 的 Microsoft Internet Explorer 11 或更高版本。

### <a name="javascript-client-method-syntax"></a>JavaScript 客户端方法语法

JavaScript 语法已从以前版本的 SignalR。 而不是使用`$connection`对象，请创建连接使用[HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API。

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

使用[上](/javascript/api/@aspnet/signalr/HubConnection#on)方法，以指定客户端可以调用该集线器的方法。

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

在创建后的客户端方法，启动集线器连接。 链[捕获](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)方法来记录或处理的错误。

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>中心代理

不能再自动生成中心代理。 相反，传递到方法名称[调用](/javascript/api/%40aspnet/signalr/hubconnection#invoke)以字符串形式的 API。

### <a name="net-and-other-clients"></a>.NET 和其他客户端

`Microsoft.AspNetCore.SignalR.Client` NuGet 程序包包含 ASP.NET Core signalr 的.NET 客户端库。

使用[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)创建和生成到集线器的连接的实例。

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a>横向扩展差异

ASP.NET SignalR 支持 SQL Server 和 Redis。 ASP.NET Core SignalR 支持 Azure SignalR 服务和 Redis。

### <a name="aspnet"></a>ASP.NET

* [使用 Azure 服务总线的 SignalR 横向扩展](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [使用 Redis 的 SignalR 横向扩展](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [使用 SQL Server 的 SignalR 横向扩展](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a>ASP.NET Core

* [Azure SignalR 服务](/azure/azure-signalr/)

## <a name="additional-resources"></a>其他资源

* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [.NET 客户端](xref:signalr/dotnet-client)
* [支持的平台](xref:signalr/supported-platforms)
