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

ASP.NET Core SignalR 与 ASP.NET SignalR 的客户端或服务端不兼容。本文详细介绍了如何在 ASP.NET Core SignalR 中删除和更改相关功能。

## <a name="how-to-identify-the-signalr-version"></a>如何识别 SignalR 版本

|                      | ASP.NET SignalR | ASP.NET Core SignalR |
| -------------------- | --------------- | -------------------- |
| 服务器 NuGet 包 | [Microsoft.AspNet.SignalR](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)<br>[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework) |
| 客户端 NuGet 包 | [Microsoft.AspNet.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[Microsoft.AspNet.SignalR.JS](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [Microsoft.AspNetCore.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| 客户端 npm 包 | [signalr](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| 服务器应用程序类型 | ASP.NET (System.Web) 或 OWIN 自托管 | ASP.NET Core |
| 受支持的服务器平台 | .NET framework 4.5 或更高版本 | .NET Framework 4.6.1 或更高版本<br>.NET core 2.1 或更高版本 |

## <a name="feature-differences"></a>功能差异

### <a name="automatic-reconnects"></a>自动重连

由于 ASP.NET Core SignalR 中不支持自动重连，如果客户端已断开连接，用户如果想要重新连接，则必须显式的启动一个新的连接。 在ASP.NET SignalR 中，如果连接断开，SignalR 会尝试重新连接到服务器。

### <a name="protocol-support"></a>协议支持

ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。 此外，你可以创建自定义协议。

### <a name="transports"></a>传输

ASP.NET Core SignalR 不支持 Forever Frame 传输。

## <a name="differences-on-the-server"></a>在服务端的差异

ASP.NET Core SignalR 服务端库包含在[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中，该包是 **ASP.NET Core Web 应用程序** 中 Razor 和 MVC 模板的一部分。

ASP.NET Core SignalR 是一个 ASP.NET Core 中间件，因此必须通过在 `Startup.ConfigureServices` 中调用 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 来配置它。

```csharp
services.AddSignalR()
```

要配置路由，请在 `Startup.Configure` 方法中将路由映射到 [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) 方法调用的 Hub 中。

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a>Sticky Sessions

ASP.NET SignalR的横向扩展模型允许客户端重新连接并将消息发送到服务器集群中的任何服务端。 在 ASP.NET Core SignalR 中，客户端必须在连接期间与同一服务端进行交互。对于使用Redis的横向扩展，这意味着需要 Sticky Sessions。对于使用[Azure SignalR 服务](/azure/azure-signalr/)的扩展，则不需要 Sticky Sessions，因为该服务处理客户端连接不需要 Sticky Sessions。

### <a name="single-hub-per-connection"></a>每个连接的单个Hub

在 ASP.NET Core SignalR 中，连接模型已经简化。直接连接到单个Hub，而不是单个连接用于共享对多个Hub的访问。

### <a name="streaming"></a>流处理

ASP.NET Core SignalR 现在支持[流处理](xref:signalr/streaming)从Hub到客户端。

### <a name="state"></a>状态

已删除在客户端和Hub之间传递任意状态的能力（通常称为HubState），以及对progress消息的支持。目前没有对应的Hub代理。

### <a name="persistentconnection-removal"></a>删除了 PersistentConnection 

在 ASP.NET Core SignalR 中 [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118))类已被删除。 

### <a name="globalhost"></a>GlobalHost

ASP.NET Core 有内置的依赖关系注入（DI）框架。 服务可以使用 DI 来访问[HubContext](xref:signalr/hubcontext)。 `GlobalHost`对象。
ASP.NET SignalR 中用可以使用 HubContext 来获取GlobalHost对象，但是在ASP.NET Core SignalR 中已经没有了。

### <a name="hubpipeline"></a>HubPipeline

ASP.NET Core SignalR 不支持`HubPipeline`模块。

## <a name="differences-on-the-client"></a>客户端上的差异

### <a name="typescript"></a>TypeScript

ASP.NET Core SignalR 客户端使用[TypeScript](https://www.typescriptlang.org/)。 使用时，可以编写 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>托管于[npm](https://www.npmjs.com/)的 JavaScript 客户端

在上一版本中，JavaScript 客户端通过在 Visual Studio 中的 NuGet 包获取。 对于 Core 版本中， [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 包中包含 JavaScript 库。 这个包已经不包含在**ASP.NET Core Web 应用程序**模板中。 使用 npm 获取并安装`@aspnet/signalr`npm 包。

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

已删除对 jQuery 的依赖关系，但项目仍然可以使用 jQuery。

### <a name="internet-explorer-support"></a>Internet Explorer 支持

ASP.NET Core SignalR 要求Microsoft Internet Explorer 11 或更高版本（ASP.NET SignalR 支持 Microsoft Internet Explorer 8 及更高版本）。

### <a name="javascript-client-method-syntax"></a>JavaScript 客户端语法

JavaScript语法已从以前版本的SignalR做了更改。请使用[HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API创建连接，而不是使用 `$connection` 对象。

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

使用 [on](/javascript/api/@aspnet/signalr/HubConnection#on) 方法指定Hub可以调用的客户端方法。

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```
创建客户端方法后，启动Hub连接。链接一个[catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)方法来记录或处理错误。

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>Hub代理

不再自动生成Hub代理。相反，以字符串API形式传递到方法[invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke)。

### <a name="net-and-other-clients"></a>.NET 和其他客户端

`Microsoft.AspNetCore.SignalR.Client` NuGet 包中包含 ASP.NET Core SignalR 的.NET 客户端库。

使用[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)创建和生成Hub的连接实例。

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a>横向扩展的差异

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
