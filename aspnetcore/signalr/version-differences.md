---
title: SignalR 和 ASP.NET Core SignalR 之间的差异
author: tdykstra
description: SignalR 和 ASP.NET Core SignalR 之间的差异
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 06/30/2018
uid: signalr/version-differences
ms.openlocfilehash: 6ed7e2e1ecadef08d71c4d7a7c3469738d07bcda
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095003"
---
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a>SignalR 和 ASP.NET Core SignalR 之间的差异

ASP.NET Core SignalR 与不兼容客户端或适用于 ASP.NET SignalR 的服务器。 此文章详细介绍了已删除或更改在 ASP.NET Core SignalR 的功能。

## <a name="feature-differences"></a>功能差异

### <a name="automatic-reconnects"></a>自动重新连接

不再支持自动重新连接。 以前，SignalR 将尝试重新连接到服务器，如果连接已断开。 现在，如果客户端已断开连接用户必须显式启动新的连接如果用户想要重新连接。

### <a name="protocol-support"></a>协议支持

ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。 此外，可以创建自定义协议。

## <a name="differences-on-the-server"></a>在服务器上的差异

SignalR 服务器端库包含在`Microsoft.AspNetCore.App`是的一部分的包**ASP.NET Core Web 应用程序**Razor 和 MVC 项目模板的。

SignalR 是 ASP.NET Core 中间件，因此它必须通过调用配置`AddSignalR`中`Startup.ConfigureServices`。

```csharp
services.AddSignalR();
```

若要配置路由，请将路由映射到中心内`UseSignalR`方法调用中`Startup.Configure`方法。

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a>现在需要粘性会话

由于扩展的工作方式在以前版本的 SignalR，客户端无法重新连接，并将消息发送到服务器场中的任何服务器。 由于对横向扩展模型，以及不支持重新连接更改，这不再受支持。 现在，客户端连接到服务器后它需要连接的持续时间与在同一台服务器进行交互。

### <a name="single-hub-per-connection"></a>每个连接的单个中心

在 ASP.NET Core SignalR 连接模型进行了简化。 直接向单个中心，而不是单个连接正在使用共享到多个中心的访问权限进行连接。

### <a name="streaming"></a>流式处理

SignalR 现在支持[流式处理数据](xref:signalr/streaming)从中心向客户端。

### <a name="state"></a>状态

已删除将任意状态传递客户端与中心 （通常称为 HubState） 之间的功能，以及对进度消息的支持。 目前中心代理没有对应。

## <a name="differences-on-the-client"></a>在客户端上的差异

### <a name="typescript"></a>TypeScript

写入 SignalR 的 ASP.NET Core 版本[TypeScript](https://www.typescriptlang.org/)。 使用时，可以编写 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>JavaScript 客户端托管于[npm](https://www.npmjs.com/)

在上一版本中，JavaScript 客户端已通过在 Visual Studio 中的 NuGet 包获取。 对于核心版本中， [ @aspnet/signalr npm 包](https://www.npmjs.com/package/@aspnet/signalr)包含 JavaScript 库。 此包不包括在**ASP.NET Core Web 应用程序**模板。 使用 npm 获取并安装`@aspnet/signalr`npm 包。

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

已删除对 jQuery 的依赖关系，但项目仍然可以使用 jQuery。

### <a name="javascript-client-method-syntax"></a>JavaScript 客户端方法语法

JavaScript 语法已从以前版本的 SignalR。 而不是使用`$connection`对象，请创建连接使用`HubConnectionBuilder`API。

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

使用`connection.on`来指定客户端可以调用该集线器的方法。

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

在创建后的客户端方法，启动集线器连接。 链`catch`方法来记录或处理的错误。

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>中心代理

不能再自动生成中心代理。 相反，传递到方法名称`invoke`以字符串形式的 API。

### <a name="net-and-other-clients"></a>.NET 和其他客户端

`Microsoft.AspNetCore.SignalR.Client` NuGet 程序包包含 ASP.NET Core signalr 的.NET 客户端库。

使用`HubConnectionBuilder`创建和生成到集线器的连接的实例。

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
