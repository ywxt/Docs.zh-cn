---
title: ASP.NET Core SignalR 配置
author: rachelappel
description: 了解如何配置 ASP.NET Core SignalR 应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/30/2018
uid: signalr/configuration
ms.openlocfilehash: 167b8828efd093d755aeb1c91e080dbd22b5d485
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961977"
---
# <a name="aspnet-core-signalr-configuration"></a>ASP.NET Core SignalR 配置

## <a name="jsonmessagepack-serialization-options"></a>JSON/MessagePack 序列化选项

ASP.NET Core SignalR 支持两个协议为消息编码： [JSON](https://www.json.org/)和[MessagePack](https://msgpack.org/index.html)。 每个协议已序列化配置选项。

JSON 序列化可以配置服务器使用[ `AddJsonProtocol` ](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol)扩展方法，可将其添加后[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)中你`Startup.ConfigureServices`方法。 `AddJsonProtocol`方法采用一个委托，接收`options`对象。 [ `PayloadSerializerSettings` ](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings)对该对象的属性是 JSON.NET`JsonSerializerSettings`可以用于配置的自变量的序列化和返回值的对象。 请参阅[JSON.NET 文档](https://www.newtonsoft.com/json/help/html/Introduction.htm)有关详细信息。

例如，若要配置的序列化程序，而不是默认的"驼峰匹配"名称，使用"PascalCase"属性名称，使用下面的代码:

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

在.NET 客户端，相同`AddJsonHubProtocol`扩展方法位于[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)。 `Microsoft.Extensions.DependencyInjection`必须导入命名空间，若要解决该扩展方法：

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
.AddJsonHubProtocol(options => {
    options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
});
```

> [!NOTE]
> 不能在此时间中的 JavaScript 客户端配置 JSON 序列化。

### <a name="messagepack-serialization-options"></a>MessagePack 序列化选项

可以通过提供委托给配置 MessagePack 序列化[AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol)调用。 请参阅[中 SignalR MessagePack](xref:signalr/messagepackhubprotocol)有关详细信息。

> [!NOTE]
> 不能在此时间中的 JavaScript 客户端配置 MessagePack 序列化。

## <a name="configure-server-options"></a>配置服务器选项

下表介绍用于配置 SignalR 集线器的选项：

| 选项 | 描述 |
| ------ | ----------- |
| `HandshakeTimeout` | 如果客户端不在此时间间隔内发送初次握手消息，则连接将关闭。 |
| `KeepAliveInterval` | 如果服务器未在此间隔内发送一条消息，会自动发送 ping 消息以使连接保持打开。 |
| `SupportedProtocols` | 此中心支持的协议。 默认情况下允许在服务器上注册的所有协议，但可以从若要禁用特定协议的单个中心此列表中删除协议。 |
| `EnableDetailedErrors` | 如果`true`、 详细的中心方法中引发异常时，异常消息将返回到客户端。 默认值是`false`，这些异常消息可以包含敏感信息。 |

可以通过提供一个选项委托，它为所有中心的配置选项`AddSignalR`调用`Startup.ConfigureServices`。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    })
}
```

单个中心的选项重写中提供的全局选项`AddSignalR`，并可使用配置[ `AddHubOptions<T>` ](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

使用`HttpConnectionDispatcherOptions`配置与传输和内存缓冲区管理相关的高级的设置。 通过将传递到委托配置这些选项[ `MapHub<T>` ](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)。

| 选项 | 描述 |
| ------ | ----------- |
| `ApplicationMaxBufferSize` | 最大从客户端收到的字节数，服务器缓冲区。 增加此值允许服务器接收更大的消息，但会产生负面影响内存消耗。 默认值为 32 KB。 |
| `AuthorizationData` | 一份[ `IAuthorizeData` ](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata)对象用于确定客户端有权连接到集线器。 默认情况下，这填充的值从`Authorize`特性应用于中心类。 |
| `TransportMaxBufferSize` | 最大应用程序发送的字节数，服务器缓冲区。 增加此值允许服务器以发送较大的邮件，但可能带来负面影响内存消耗。 默认值为 32 KB。 |
| `Transports` | 一个位屏蔽`HttpTransportType`客户端连接而可以使用可以限制所使用的传输的值。 默认情况下，启用所有传输。 |
| `LongPolling` | 特定于长轮询传输的其他选项。 |
| `WebSockets` | 特定于 Websocket 传输的其他选项。 |

长轮询传输的其他选项，可以使用配置`LongPolling`属性：

| 选项 | 描述 |
| ------ | ----------- |
| `PollTimeout` | 最长时间等待消息之前要发送到客户端终止单个轮询请求服务器。 减小此值会导致客户端更频繁地发出新轮询请求。 默认值为 90 秒。 |

WebSocket 传输的其他选项，可以使用配置`WebSockets`属性：

| 选项 | 描述 |
| ------ | ----------- |
| `CloseTimeout` | 服务器关闭，如果客户端无法在此时间间隔内关闭后，已终止连接。 |
| `SubProtocolSelector` | 可以用来设置委托`Sec-WebSocket-Protocol`为自定义值的标头。 委托接收请求的客户端作为输入的值，还应返回所需的值。 |

## <a name="configure-client-options"></a>配置客户端选项

可以在配置客户端选项`HubConnectionBuilder`类型 （在.NET 和 JavaScript 客户端中可用），以及上`HubConnection`本身。

### <a name="configure-logging"></a>配置日志记录

在使用.NET 客户端中配置日志记录`ConfigureLogging`方法。 可以按相同的方式注册日志记录提供程序和筛选器，因为它们是在服务器上。 请参阅[登录 ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) 文档以了解更多信息。

> [!NOTE]
> 若要注册日志记录提供程序，你必须安装所需的包。 请参阅[内置日志记录提供程序](xref:fundamentals/logging/index#built-in-logging-providers)一部分的文档的完整列表。

例如，若要启用控制台日志记录，安装`Microsoft.Extensions.Logging.Console`NuGet 包。 调用`AddConsole`扩展方法：

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

在 JavaScript 客户端，类似`configureLogging`方法存在。 提供`LogLevel`值，该值指示要生成的日志消息的最低级别。 日志将写入浏览器控制台窗口。

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> 若要禁用日志记录完全，指定`signalR.LogLevel.None`中`configureLogging`方法。

下面列出了可用于 JavaScript 客户端的日志级别。 将日志级别设置为下列值之一启用日志记录的消息在**或更高版本**该级别。

| 级别 | 描述 |
| ----- | ----------- |
| `None` | 未不记录任何消息。 |
| `Critical` | 表示在整个应用程序失败的消息。 |
| `Error` | 表示在当前操作失败的消息。 |
| `Warning` | 指示非致命性问题的消息。 |
| `Information` | 信息性消息。 |
| `Debug` | 可用于调试的诊断消息。 |
| `Trace` | 用于诊断特定问题的非常详细诊断消息。 |

### <a name="configure-allowed-transports"></a>配置允许的传输

可以在中配置的传输使用 SignalR`WithUrl`调用 (`withUrl`在 JavaScript 中)。 按位 OR 的值`HttpTransportType`可以用于限制客户端仅使用指定的传输。 默认情况下，启用所有传输。

例如，若要禁用 Server-Sent 事件传输，但允许 Websocket 和长轮询连接：

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

在 JavaScript 客户端，通过设置配置传输`transport`字段上的选项对象，提供给`withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a>配置持有者身份验证

若要提供以及 SignalR 请求的身份验证数据，使用`AccessTokenProvider`选项 (`accessTokenFactory`在 JavaScript 中) 以指定函数返回的所需的访问令牌。 在.NET 客户端，此访问令牌中作为传递 HTTP"持有者身份验证"令牌 (使用`Authorization`具有一种类型的标头`Bearer`)。 在 JavaScript 客户端，将使用访问令牌作为持有者令牌，**除**在少数情况下在其中浏览器 Api 限制能够将应用 （具体而言，Server-Sent 事件和 Websocket 请求） 中的标头。 在这些情况下，访问令牌提供作为查询字符串值`access_token`。

在.NET 客户端，`AccessTokenProvider`可以使用中的选项委托指定选项`WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

在 JavaScript 客户端，通过设置配置的访问令牌`accessTokenFactory`字段中的选项对象`withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a>配置超时和保持活动状态的选项

还提供用于配置超时和保持活动状态的行为的其他选项`HubConnection`对象本身：

| .NET 选项 | JavaScript 选项 | 描述 |
| ----------- | ----------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | 服务器活动的超时值。 如果服务器未在此时间间隔内发送任何消息，客户端会将服务器断开连接而触发器`Closed`事件 (`onclose`在 JavaScript 中)。 |
| `HandshakeTimeout` | 不可配置 | 初始服务器握手的超时值。 如果服务器不在此时间间隔内发送握手响应，客户端取消握手和触发器`Closed`事件 (`onclose`在 JavaScript 中)。 |

在.NET 客户端，超时值被指定为`TimeSpan`值。 在 JavaScript 客户端，超时值被指定为数字。 数字表示以毫秒为单位的时间值。

### <a name="configure-additional-options"></a>配置其他选项

可以在中配置其他选项`WithUrl`(`withUrl`在 JavaScript 中) 上的方法`HubConnectionBuilder`:

| .NET 选项 | JavaScript 选项 | 描述 |
| ----------- | ----------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | 返回一个字符串，作为持有者身份验证令牌在 HTTP 请求中提供的函数。 |
| `SkipNegotiation` | `skipNegotiation` | 将其设置为`true`可跳过协商步骤。 **仅支持 Websocket 传输时仅启用的传输**。 使用 Azure SignalR 服务时，无法启用此设置。 |
| `ClientCertificates` | 不可配置 * | 要进行身份验证请求而发送的 TLS 证书的集合。 |
| `Cookies` | 不可配置 * | 要与每个 HTTP 请求一起发送的 HTTP cookie 的集合。 |
| `Credentials` | 不可配置 * | 要与每个 HTTP 请求一起发送的凭据。 |
| `CloseTimeout` | 不可配置 * | 仅 Websocket。 要确认关闭请求的服务器的关闭之后的最大时间量客户端将等待。 如果服务器不在此时间内收到结束时，客户端断开连接。 |
| `Headers` | 不可配置 * | 其他 HTTP 标头以与每个 HTTP 请求发送一个字典。 |
| `HttpMessageHandlerFactory` | 不可配置 * | 一个委托，可用于配置或替换`HttpMessageHandler`用于发送 HTTP 请求。 不用于 WebSocket 连接。 此委托必须返回非 null 值，并且它接收作为参数的默认值。 修改设置，该默认值并返回它，或者返回完整的全新`HttpMessageHandler`实例。 |
| `Proxy` | 不可配置 * | 发送 HTTP 请求时要使用 HTTP 代理。 |
| `UseDefaultCredentials` | 不可配置 * | 设置此布尔值以发送 HTTP 和 Websocket 请求的默认凭据。 这使使用 Windows 身份验证。 |
| `WebSocketConfiguration` | 不可配置 * | 一个委托，用于配置其他的 WebSocket 选项。 接收实例[ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions)可用来配置选项。 |

标有星号 （*） 的选项不是可在 JavaScript 客户端，由于在浏览器 Api 中的限制配置。

在.NET 客户端，这些选项可以修改选项委托提供给`WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

在 JavaScript 客户端，可以提供给 JavaScript 对象中提供这些选项`withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a>其他资源

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
