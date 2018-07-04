---
title: SignalR 和 ASP.NET Core SignalR 之间的差异
author: rachelappel
description: SignalR 和 ASP.NET Core SignalR 之间的差异
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.date: 06/30/2018
uid: signalr/version-differences
ms.openlocfilehash: fd314d93333bd159aef4bb4863be50c646809cf0
ms.sourcegitcommit: 1faf2525902236428dae6a59e375519bafd5d6d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090058"
---
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a>SignalR 和 ASP.NET Core SignalR 之间的差异

ASP.NET Core SignalR 与不兼容客户端或适用于 ASP.NET SignalR 的服务器。 此文章详细介绍了已删除或更改在 ASP.NET Core SignalR 的功能。

## <a name="feature-differences"></a>功能差异

### <a name="automatic-reconnects"></a>自动重新连接

不再支持自动重新连接。 以前，SignalR 尝试重新连接到服务器，如果连接已断开。 现在，如果断开客户端用户必须显式会启动一个新连接，如果他们想要重新连接。

### <a name="protocol-support"></a>协议支持

ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。 此外，可以创建自定义协议。

## <a name="differences-on-the-server"></a>在服务器上的差异

SignalR 服务器端库包含在`Microsoft.AspNetCore.App`是的一部分的包**ASP.NET Core Web 应用程序**Razor 和 MVC 项目模板的。

SignalR 是 ASP.NET Core 中间件，因此它必须通过调用配置`AddSignalR`中`Startup.ConfigureServices`。

```csharp
services.AddSignalR();
```

若要配置路由，请将路由映射到内的中心`UseSignalR`方法调用`Startup.Configure`方法。

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a>现在所需的粘性会话

由于横向扩展的工作方式在以前版本的 SignalR，客户端无法重新连接，并将消息发送到服务器场中的任何服务器。 由于更改应用于横向扩展模型，以及不支持重新连接，这不再受支持。 现在，客户端连接到服务器后它需要进行连接的持续时间内与同一台服务器交互。

### <a name="single-hub-per-connection"></a>每个连接的单个中心

在 ASP.NET Core SignalR 连接模型进行了简化。 直接对单个中心，而不是单个连接用于共享对多个中心访问权限进行连接。

### <a name="streaming"></a>流式处理

SignalR 现在支持[流式处理数据](xref:signalr/streaming)从客户端到中心。

### <a name="state"></a>状态

将任意状态传递客户端与中心 （通常称为 HubState） 之间的功能已删除，并且支持进度消息。 目前中心代理没有对应项。

## <a name="differences-on-the-client"></a>客户端上的差异

### <a name="typescript"></a>TypeScript

写入 SignalR 的 ASP.NET Core 版本[TypeScript](https://www.typescriptlang.org/)。 当使用时，可以编写在 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>JavaScript 客户端托管在[npm](https://www.npmjs.com/)

在以前版本中，JavaScript 客户端是通过 Visual Studio 中的 NuGet 包获得的。 对于核心版本中， [ @aspnet/signalr npm 包](https://www.npmjs.com/package/@aspnet/signalr)包含 JavaScript 库。 此包不包括在**ASP.NET Core Web 应用程序**模板。 使用 npm 获取并安装`@aspnet/signalr`npm 包。

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

已删除对 jQuery 的依赖关系，不过项目仍然可以使用 jQuery。

### <a name="javascript-client-method-syntax"></a>JavaScript 客户端方法语法

JavaScript 语法 SignalR 的先前版本中已更改。 而不是使用`$connection`对象，请创建连接使用`HubConnectionBuilder`API。

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

使用`connection.on`指定中心可以调用的客户端方法。

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

在创建客户端方法，启动集线器连接。 链`catch`方法可以登录或处理错误。

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>中心代理

中心代理将不再自动生成。 相反，将方法名称传递给`invoke`字符串形式的 API。

### <a name="net-and-other-clients"></a>.NET 和其他客户端

`Microsoft.AspNetCore.SignalR.Client` NuGet 程序包包含 ASP.NET Core signalr 的.NET 客户端库。

使用`HubConnectionBuilder`若要创建和生成到一个中心的连接的实例。

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="additional-resources"></a>其他资源

* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [.NET 客户端](xref:signalr/dotnet-client)
* [支持的平台](xref:signalr/supported-platforms)
