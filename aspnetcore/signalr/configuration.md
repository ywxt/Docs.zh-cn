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
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="2a18b-103">ASP.NET Core SignalR 配置</span><span class="sxs-lookup"><span data-stu-id="2a18b-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="2a18b-104">JSON/MessagePack 序列化选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="2a18b-105">ASP.NET Core SignalR 支持两个协议为消息编码： [JSON](https://www.json.org/)和[MessagePack](https://msgpack.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="2a18b-106">每个协议已序列化配置选项。</span><span class="sxs-lookup"><span data-stu-id="2a18b-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="2a18b-107">JSON 序列化可以配置服务器使用[ `AddJsonProtocol` ](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol)扩展方法，可将其添加后[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)中你`Startup.ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="2a18b-107">JSON serialization can be configured on the server using the [`AddJsonProtocol`](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="2a18b-108">`AddJsonProtocol`方法采用一个委托，接收`options`对象。</span><span class="sxs-lookup"><span data-stu-id="2a18b-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="2a18b-109">[ `PayloadSerializerSettings` ](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings)对该对象的属性是 JSON.NET`JsonSerializerSettings`可以用于配置的自变量的序列化和返回值的对象。</span><span class="sxs-lookup"><span data-stu-id="2a18b-109">The [`PayloadSerializerSettings`](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="2a18b-110">请参阅[JSON.NET 文档](https://www.newtonsoft.com/json/help/html/Introduction.htm)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="2a18b-111">例如，若要配置的序列化程序，而不是默认的"驼峰匹配"名称，使用"PascalCase"属性名称，使用下面的代码:</span><span class="sxs-lookup"><span data-stu-id="2a18b-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="2a18b-112">在.NET 客户端，相同`AddJsonHubProtocol`扩展方法位于[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-112">In the .NET client, the same `AddJsonHubProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="2a18b-113">`Microsoft.Extensions.DependencyInjection`必须导入命名空间，若要解决该扩展方法：</span><span class="sxs-lookup"><span data-stu-id="2a18b-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

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
> <span data-ttu-id="2a18b-114">不能在此时间中的 JavaScript 客户端配置 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="2a18b-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="2a18b-115">MessagePack 序列化选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-115">MessagePack serialization options</span></span>

<span data-ttu-id="2a18b-116">可以通过提供委托给配置 MessagePack 序列化[AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol)调用。</span><span class="sxs-lookup"><span data-stu-id="2a18b-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="2a18b-117">请参阅[中 SignalR MessagePack](xref:signalr/messagepackhubprotocol)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="2a18b-118">不能在此时间中的 JavaScript 客户端配置 MessagePack 序列化。</span><span class="sxs-lookup"><span data-stu-id="2a18b-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="2a18b-119">配置服务器选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-119">Configure server options</span></span>

<span data-ttu-id="2a18b-120">下表介绍用于配置 SignalR 集线器的选项：</span><span class="sxs-lookup"><span data-stu-id="2a18b-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="2a18b-121">选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-121">Option</span></span> | <span data-ttu-id="2a18b-122">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-122">Description</span></span> |
| ------ | ----------- |
| `HandshakeTimeout` | <span data-ttu-id="2a18b-123">如果客户端不在此时间间隔内发送初次握手消息，则连接将关闭。</span><span class="sxs-lookup"><span data-stu-id="2a18b-123">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="2a18b-124">如果服务器未在此间隔内发送一条消息，会自动发送 ping 消息以使连接保持打开。</span><span class="sxs-lookup"><span data-stu-id="2a18b-124">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> |
| `SupportedProtocols` | <span data-ttu-id="2a18b-125">此中心支持的协议。</span><span class="sxs-lookup"><span data-stu-id="2a18b-125">Protocols supported by this hub.</span></span> <span data-ttu-id="2a18b-126">默认情况下允许在服务器上注册的所有协议，但可以从若要禁用特定协议的单个中心此列表中删除协议。</span><span class="sxs-lookup"><span data-stu-id="2a18b-126">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | <span data-ttu-id="2a18b-127">如果`true`、 详细的中心方法中引发异常时，异常消息将返回到客户端。</span><span class="sxs-lookup"><span data-stu-id="2a18b-127">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="2a18b-128">默认值是`false`，这些异常消息可以包含敏感信息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-128">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="2a18b-129">可以通过提供一个选项委托，它为所有中心的配置选项`AddSignalR`调用`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="2a18b-129">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

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

<span data-ttu-id="2a18b-130">单个中心的选项重写中提供的全局选项`AddSignalR`，并可使用配置[ `AddHubOptions<T>` ](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="2a18b-130">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [`AddHubOptions<T>`](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

<span data-ttu-id="2a18b-131">使用`HttpConnectionDispatcherOptions`配置与传输和内存缓冲区管理相关的高级的设置。</span><span class="sxs-lookup"><span data-stu-id="2a18b-131">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="2a18b-132">通过将传递到委托配置这些选项[ `MapHub<T>` ](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-132">These options are configured by passing a delegate to [`MapHub<T>`](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub).</span></span>

| <span data-ttu-id="2a18b-133">选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-133">Option</span></span> | <span data-ttu-id="2a18b-134">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-134">Description</span></span> |
| ------ | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="2a18b-135">最大从客户端收到的字节数，服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="2a18b-135">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="2a18b-136">增加此值允许服务器接收更大的消息，但会产生负面影响内存消耗。</span><span class="sxs-lookup"><span data-stu-id="2a18b-136">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="2a18b-137">默认值为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="2a18b-137">The default value is 32KB.</span></span> |
| `AuthorizationData` | <span data-ttu-id="2a18b-138">一份[ `IAuthorizeData` ](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata)对象用于确定客户端有权连接到集线器。</span><span class="sxs-lookup"><span data-stu-id="2a18b-138">A list of [`IAuthorizeData`](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> <span data-ttu-id="2a18b-139">默认情况下，这填充的值从`Authorize`特性应用于中心类。</span><span class="sxs-lookup"><span data-stu-id="2a18b-139">By default, this is populated with values from the `Authorize` attributes applied to the Hub class.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="2a18b-140">最大应用程序发送的字节数，服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="2a18b-140">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="2a18b-141">增加此值允许服务器以发送较大的邮件，但可能带来负面影响内存消耗。</span><span class="sxs-lookup"><span data-stu-id="2a18b-141">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="2a18b-142">默认值为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="2a18b-142">The default value is 32KB.</span></span> |
| `Transports` | <span data-ttu-id="2a18b-143">一个位屏蔽`HttpTransportType`客户端连接而可以使用可以限制所使用的传输的值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-143">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> <span data-ttu-id="2a18b-144">默认情况下，启用所有传输。</span><span class="sxs-lookup"><span data-stu-id="2a18b-144">All transports are enabled by default.</span></span> |
| `LongPolling` | <span data-ttu-id="2a18b-145">特定于长轮询传输的其他选项。</span><span class="sxs-lookup"><span data-stu-id="2a18b-145">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="2a18b-146">特定于 Websocket 传输的其他选项。</span><span class="sxs-lookup"><span data-stu-id="2a18b-146">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="2a18b-147">长轮询传输的其他选项，可以使用配置`LongPolling`属性：</span><span class="sxs-lookup"><span data-stu-id="2a18b-147">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="2a18b-148">选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-148">Option</span></span> | <span data-ttu-id="2a18b-149">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-149">Description</span></span> |
| ------ | ----------- |
| `PollTimeout` | <span data-ttu-id="2a18b-150">最长时间等待消息之前要发送到客户端终止单个轮询请求服务器。</span><span class="sxs-lookup"><span data-stu-id="2a18b-150">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="2a18b-151">减小此值会导致客户端更频繁地发出新轮询请求。</span><span class="sxs-lookup"><span data-stu-id="2a18b-151">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> <span data-ttu-id="2a18b-152">默认值为 90 秒。</span><span class="sxs-lookup"><span data-stu-id="2a18b-152">The default value is 90 seconds.</span></span> |

<span data-ttu-id="2a18b-153">WebSocket 传输的其他选项，可以使用配置`WebSockets`属性：</span><span class="sxs-lookup"><span data-stu-id="2a18b-153">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="2a18b-154">选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-154">Option</span></span> | <span data-ttu-id="2a18b-155">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-155">Description</span></span> |
| ------ | ----------- |
| `CloseTimeout` | <span data-ttu-id="2a18b-156">服务器关闭，如果客户端无法在此时间间隔内关闭后，已终止连接。</span><span class="sxs-lookup"><span data-stu-id="2a18b-156">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | <span data-ttu-id="2a18b-157">可以用来设置委托`Sec-WebSocket-Protocol`为自定义值的标头。</span><span class="sxs-lookup"><span data-stu-id="2a18b-157">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="2a18b-158">委托接收请求的客户端作为输入的值，还应返回所需的值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-158">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="2a18b-159">配置客户端选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-159">Configure client options</span></span>

<span data-ttu-id="2a18b-160">可以在配置客户端选项`HubConnectionBuilder`类型 （在.NET 和 JavaScript 客户端中可用），以及上`HubConnection`本身。</span><span class="sxs-lookup"><span data-stu-id="2a18b-160">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="2a18b-161">配置日志记录</span><span class="sxs-lookup"><span data-stu-id="2a18b-161">Configure logging</span></span>

<span data-ttu-id="2a18b-162">在使用.NET 客户端中配置日志记录`ConfigureLogging`方法。</span><span class="sxs-lookup"><span data-stu-id="2a18b-162">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="2a18b-163">可以按相同的方式注册日志记录提供程序和筛选器，因为它们是在服务器上。</span><span class="sxs-lookup"><span data-stu-id="2a18b-163">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="2a18b-164">请参阅[登录 ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers)文档以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-164">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="2a18b-165">若要注册日志记录提供程序，你必须安装所需的包。</span><span class="sxs-lookup"><span data-stu-id="2a18b-165">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="2a18b-166">请参阅[内置日志记录提供程序](xref:fundamentals/logging/index#built-in-logging-providers)一部分的文档的完整列表。</span><span class="sxs-lookup"><span data-stu-id="2a18b-166">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="2a18b-167">例如，若要启用控制台日志记录，安装`Microsoft.Extensions.Logging.Console`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="2a18b-167">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="2a18b-168">调用`AddConsole`扩展方法：</span><span class="sxs-lookup"><span data-stu-id="2a18b-168">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="2a18b-169">在 JavaScript 客户端，类似`configureLogging`方法存在。</span><span class="sxs-lookup"><span data-stu-id="2a18b-169">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="2a18b-170">提供`LogLevel`值，该值指示要生成的日志消息的最低级别。</span><span class="sxs-lookup"><span data-stu-id="2a18b-170">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="2a18b-171">日志将写入浏览器控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="2a18b-171">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="2a18b-172">若要禁用日志记录完全，指定`signalR.LogLevel.None`中`configureLogging`方法。</span><span class="sxs-lookup"><span data-stu-id="2a18b-172">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="2a18b-173">下面列出了可用于 JavaScript 客户端的日志级别。</span><span class="sxs-lookup"><span data-stu-id="2a18b-173">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="2a18b-174">将日志级别设置为下列值之一启用日志记录的消息在**或更高版本**该级别。</span><span class="sxs-lookup"><span data-stu-id="2a18b-174">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="2a18b-175">级别</span><span class="sxs-lookup"><span data-stu-id="2a18b-175">Level</span></span> | <span data-ttu-id="2a18b-176">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-176">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="2a18b-177">未不记录任何消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-177">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="2a18b-178">表示在整个应用程序失败的消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-178">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="2a18b-179">表示在当前操作失败的消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-179">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="2a18b-180">指示非致命性问题的消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-180">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="2a18b-181">信息性消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-181">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="2a18b-182">可用于调试的诊断消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-182">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="2a18b-183">用于诊断特定问题的非常详细诊断消息。</span><span class="sxs-lookup"><span data-stu-id="2a18b-183">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="2a18b-184">配置允许的传输</span><span class="sxs-lookup"><span data-stu-id="2a18b-184">Configure allowed transports</span></span>

<span data-ttu-id="2a18b-185">可以在中配置的传输使用 SignalR`WithUrl`调用 (`withUrl`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-185">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="2a18b-186">按位 OR 的值`HttpTransportType`可以用于限制客户端仅使用指定的传输。</span><span class="sxs-lookup"><span data-stu-id="2a18b-186">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="2a18b-187">默认情况下，启用所有传输。</span><span class="sxs-lookup"><span data-stu-id="2a18b-187">All transports are enabled by default.</span></span>

<span data-ttu-id="2a18b-188">例如，若要禁用 Server-Sent 事件传输，但允许 Websocket 和长轮询连接：</span><span class="sxs-lookup"><span data-stu-id="2a18b-188">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="2a18b-189">在 JavaScript 客户端，通过设置配置传输`transport`字段上的选项对象，提供给`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-189">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="2a18b-190">配置持有者身份验证</span><span class="sxs-lookup"><span data-stu-id="2a18b-190">Configure bearer authentication</span></span>

<span data-ttu-id="2a18b-191">若要提供以及 SignalR 请求的身份验证数据，使用`AccessTokenProvider`选项 (`accessTokenFactory`在 JavaScript 中) 以指定函数返回的所需的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="2a18b-191">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="2a18b-192">在.NET 客户端，此访问令牌中作为传递 HTTP"持有者身份验证"令牌 (使用`Authorization`具有一种类型的标头`Bearer`)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-192">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="2a18b-193">在 JavaScript 客户端，将使用访问令牌作为持有者令牌，**除**在少数情况下在其中浏览器 Api 限制能够将应用 （具体而言，Server-Sent 事件和 Websocket 请求） 中的标头。</span><span class="sxs-lookup"><span data-stu-id="2a18b-193">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="2a18b-194">在这些情况下，访问令牌提供作为查询字符串值`access_token`。</span><span class="sxs-lookup"><span data-stu-id="2a18b-194">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="2a18b-195">在.NET 客户端，`AccessTokenProvider`可以使用中的选项委托指定选项`WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-195">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

<span data-ttu-id="2a18b-196">在 JavaScript 客户端，通过设置配置的访问令牌`accessTokenFactory`字段中的选项对象`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-196">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

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

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="2a18b-197">配置超时和保持活动状态的选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-197">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="2a18b-198">还提供用于配置超时和保持活动状态的行为的其他选项`HubConnection`对象本身：</span><span class="sxs-lookup"><span data-stu-id="2a18b-198">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="2a18b-199">.NET 选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-199">.NET Option</span></span> | <span data-ttu-id="2a18b-200">JavaScript 选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-200">JavaScript Option</span></span> | <span data-ttu-id="2a18b-201">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-201">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="2a18b-202">服务器活动的超时值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-202">Timeout for server activity.</span></span> <span data-ttu-id="2a18b-203">如果服务器未在此时间间隔内发送任何消息，客户端会将服务器断开连接而触发器`Closed`事件 (`onclose`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-203">If the server hasn't sent any message in this interval, the client considers the server disconnected and trigger the `Closed` event (`onclose` in JavaScript).</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="2a18b-204">不可配置</span><span class="sxs-lookup"><span data-stu-id="2a18b-204">Not configurable</span></span> | <span data-ttu-id="2a18b-205">初始服务器握手的超时值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-205">Timeout for initial server handshake.</span></span> <span data-ttu-id="2a18b-206">如果服务器不在此时间间隔内发送握手响应，客户端取消握手和触发器`Closed`事件 (`onclose`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="2a18b-206">If the server doesn't send a handshake response in this interval, the client cancels the handshake and trigger the `Closed` event (`onclose` in JavaScript).</span></span> |

<span data-ttu-id="2a18b-207">在.NET 客户端，超时值被指定为`TimeSpan`值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-207">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="2a18b-208">在 JavaScript 客户端，超时值被指定为数字。</span><span class="sxs-lookup"><span data-stu-id="2a18b-208">In the JavaScript client, timeout values are specified as numbers.</span></span> <span data-ttu-id="2a18b-209">数字表示以毫秒为单位的时间值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-209">The numbers represent time values in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="2a18b-210">配置其他选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-210">Configure additional options</span></span>

<span data-ttu-id="2a18b-211">可以在中配置其他选项`WithUrl`(`withUrl`在 JavaScript 中) 上的方法`HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-211">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="2a18b-212">.NET 选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-212">.NET Option</span></span> | <span data-ttu-id="2a18b-213">JavaScript 选项</span><span class="sxs-lookup"><span data-stu-id="2a18b-213">JavaScript Option</span></span> | <span data-ttu-id="2a18b-214">描述</span><span class="sxs-lookup"><span data-stu-id="2a18b-214">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | <span data-ttu-id="2a18b-215">返回一个字符串，作为持有者身份验证令牌在 HTTP 请求中提供的函数。</span><span class="sxs-lookup"><span data-stu-id="2a18b-215">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | <span data-ttu-id="2a18b-216">将其设置为`true`可跳过协商步骤。</span><span class="sxs-lookup"><span data-stu-id="2a18b-216">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="2a18b-217">**仅支持 Websocket 传输时仅启用的传输**。</span><span class="sxs-lookup"><span data-stu-id="2a18b-217">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="2a18b-218">使用 Azure SignalR 服务时，无法启用此设置。</span><span class="sxs-lookup"><span data-stu-id="2a18b-218">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="2a18b-219">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-219">Not configurable \*</span></span> | <span data-ttu-id="2a18b-220">要进行身份验证请求而发送的 TLS 证书的集合。</span><span class="sxs-lookup"><span data-stu-id="2a18b-220">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="2a18b-221">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-221">Not configurable \*</span></span> | <span data-ttu-id="2a18b-222">要与每个 HTTP 请求一起发送的 HTTP cookie 的集合。</span><span class="sxs-lookup"><span data-stu-id="2a18b-222">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="2a18b-223">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-223">Not configurable \*</span></span> | <span data-ttu-id="2a18b-224">要与每个 HTTP 请求一起发送的凭据。</span><span class="sxs-lookup"><span data-stu-id="2a18b-224">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="2a18b-225">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-225">Not configurable \*</span></span> | <span data-ttu-id="2a18b-226">仅 Websocket。</span><span class="sxs-lookup"><span data-stu-id="2a18b-226">WebSockets only.</span></span> <span data-ttu-id="2a18b-227">要确认关闭请求的服务器的关闭之后的最大时间量客户端将等待。</span><span class="sxs-lookup"><span data-stu-id="2a18b-227">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="2a18b-228">如果服务器不在此时间内收到结束时，客户端断开连接。</span><span class="sxs-lookup"><span data-stu-id="2a18b-228">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="2a18b-229">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-229">Not configurable \*</span></span> | <span data-ttu-id="2a18b-230">其他 HTTP 标头以与每个 HTTP 请求发送一个字典。</span><span class="sxs-lookup"><span data-stu-id="2a18b-230">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="2a18b-231">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-231">Not configurable \*</span></span> | <span data-ttu-id="2a18b-232">一个委托，可用于配置或替换`HttpMessageHandler`用于发送 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="2a18b-232">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="2a18b-233">不用于 WebSocket 连接。</span><span class="sxs-lookup"><span data-stu-id="2a18b-233">Not used for WebSocket connections.</span></span> <span data-ttu-id="2a18b-234">此委托必须返回非 null 值，并且它接收作为参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="2a18b-234">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="2a18b-235">修改设置，该默认值并返回它，或者返回完整的全新`HttpMessageHandler`实例。</span><span class="sxs-lookup"><span data-stu-id="2a18b-235">Either modify settings on that default value and return it, or return a completely new `HttpMessageHandler` instance.</span></span> |
| `Proxy` | <span data-ttu-id="2a18b-236">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-236">Not configurable \*</span></span> | <span data-ttu-id="2a18b-237">发送 HTTP 请求时要使用 HTTP 代理。</span><span class="sxs-lookup"><span data-stu-id="2a18b-237">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="2a18b-238">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-238">Not configurable \*</span></span> | <span data-ttu-id="2a18b-239">设置此布尔值以发送 HTTP 和 Websocket 请求的默认凭据。</span><span class="sxs-lookup"><span data-stu-id="2a18b-239">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="2a18b-240">这使使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="2a18b-240">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="2a18b-241">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="2a18b-241">Not configurable \*</span></span> | <span data-ttu-id="2a18b-242">一个委托，用于配置其他的 WebSocket 选项。</span><span class="sxs-lookup"><span data-stu-id="2a18b-242">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="2a18b-243">接收实例[ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions)可用来配置选项。</span><span class="sxs-lookup"><span data-stu-id="2a18b-243">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="2a18b-244">标有星号 （\*） 的选项不是可在 JavaScript 客户端，由于在浏览器 Api 中的限制配置。</span><span class="sxs-lookup"><span data-stu-id="2a18b-244">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="2a18b-245">在.NET 客户端，这些选项可以修改选项委托提供给`WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-245">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="2a18b-246">在 JavaScript 客户端，可以提供给 JavaScript 对象中提供这些选项`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="2a18b-246">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="2a18b-247">其他资源</span><span class="sxs-lookup"><span data-stu-id="2a18b-247">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
