---
title: ASP.NET Core SignalR 配置
author: tdykstra
description: 了解如何配置 ASP.NET Core SignalR 应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/30/2018
uid: signalr/configuration
ms.openlocfilehash: f5a345795f17dafd482e359e77a151d5b0a15688
ms.sourcegitcommit: 8b68e144aab75374af52605a71717c77345a28b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2018
ms.locfileid: "39182585"
---
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="289fa-103">ASP.NET Core SignalR 配置</span><span class="sxs-lookup"><span data-stu-id="289fa-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="289fa-104">JSON/MessagePack 序列化选项</span><span class="sxs-lookup"><span data-stu-id="289fa-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="289fa-105">ASP.NET Core SignalR 支持两个协议为消息编码： [JSON](https://www.json.org/)和[MessagePack](https://msgpack.org/index.html)。</span><span class="sxs-lookup"><span data-stu-id="289fa-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="289fa-106">每个协议具有序列化配置选项。</span><span class="sxs-lookup"><span data-stu-id="289fa-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="289fa-107">可以使用 server 上配置 JSON 序列化[ `AddJsonProtocol` ](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol)扩展方法，可以添加后[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)中你`Startup.ConfigureServices`方法。</span><span class="sxs-lookup"><span data-stu-id="289fa-107">JSON serialization can be configured on the server using the [`AddJsonProtocol`](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="289fa-108">`AddJsonProtocol`方法采用一个委托，接收`options`对象。</span><span class="sxs-lookup"><span data-stu-id="289fa-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="289fa-109">[ `PayloadSerializerSettings` ](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings)对该对象的属性是 JSON.NET`JsonSerializerSettings`可用于配置序列化的参数和返回值的对象。</span><span class="sxs-lookup"><span data-stu-id="289fa-109">The [`PayloadSerializerSettings`](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="289fa-110">请参阅[JSON.NET 文档](https://www.newtonsoft.com/json/help/html/Introduction.htm)的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="289fa-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="289fa-111">例如，若要配置的序列化程序，而不是默认的"驼峰式大小写"名称，使用"pascal 命名法"属性名称，使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="289fa-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="289fa-112">在.NET 客户端，相同`AddJsonHubProtocol`上存在扩展方法[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)。</span><span class="sxs-lookup"><span data-stu-id="289fa-112">In the .NET client, the same `AddJsonHubProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="289fa-113">`Microsoft.Extensions.DependencyInjection`必须导入命名空间，若要解决的扩展方法：</span><span class="sxs-lookup"><span data-stu-id="289fa-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

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
> <span data-ttu-id="289fa-114">不能在这一次配置 JavaScript 客户端中的 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="289fa-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="289fa-115">MessagePack 序列化选项</span><span class="sxs-lookup"><span data-stu-id="289fa-115">MessagePack serialization options</span></span>

<span data-ttu-id="289fa-116">可以通过提供委托，配置 MessagePack 序列化[AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol)调用。</span><span class="sxs-lookup"><span data-stu-id="289fa-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="289fa-117">请参阅[SignalR 中的 MessagePack](xref:signalr/messagepackhubprotocol)的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="289fa-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="289fa-118">不能在此时间在 JavaScript 客户端中配置 MessagePack 序列化。</span><span class="sxs-lookup"><span data-stu-id="289fa-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="289fa-119">配置服务器选项</span><span class="sxs-lookup"><span data-stu-id="289fa-119">Configure server options</span></span>

<span data-ttu-id="289fa-120">下表描述了用于配置 SignalR 集线器的选项：</span><span class="sxs-lookup"><span data-stu-id="289fa-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="289fa-121">选项</span><span class="sxs-lookup"><span data-stu-id="289fa-121">Option</span></span> | <span data-ttu-id="289fa-122">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-122">Description</span></span> |
| ------ | ----------- |
| `HandshakeTimeout` | <span data-ttu-id="289fa-123">如果客户端不会在此时间间隔内发送初始握手消息，该连接已关闭。</span><span class="sxs-lookup"><span data-stu-id="289fa-123">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> <span data-ttu-id="289fa-124">这是一种高级的设置，如果由于出现严重的网络延迟发生握手超时错误应仅修改。</span><span class="sxs-lookup"><span data-stu-id="289fa-124">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="289fa-125">握手过程的更多详细信息，请参阅[SignalR 集线器协议规范](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)。</span><span class="sxs-lookup"><span data-stu-id="289fa-125">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="289fa-126">如果服务器尚未在此时间间隔内发送一条消息，是自动发送一条 ping 消息使连接保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="289fa-126">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> |
| `SupportedProtocols` | <span data-ttu-id="289fa-127">此中心支持的协议。</span><span class="sxs-lookup"><span data-stu-id="289fa-127">Protocols supported by this hub.</span></span> <span data-ttu-id="289fa-128">默认情况下，允许在服务器上注册的所有协议，但可以从禁用特定协议的单个中心此列表中删除协议。</span><span class="sxs-lookup"><span data-stu-id="289fa-128">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | <span data-ttu-id="289fa-129">如果`true`、 详细异常消息返回到客户端集线器方法中引发异常。</span><span class="sxs-lookup"><span data-stu-id="289fa-129">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="289fa-130">默认值是`false`，因为这些异常消息可能包含敏感信息。</span><span class="sxs-lookup"><span data-stu-id="289fa-130">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="289fa-131">可以通过提供一个选项委托到的所有中心配置选项`AddSignalR`调用中`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="289fa-131">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

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

<span data-ttu-id="289fa-132">有关单个集线器的选项重写中提供的全局选项`AddSignalR`，可以使用配置[ `AddHubOptions<T>` ](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="289fa-132">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [`AddHubOptions<T>`](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

<span data-ttu-id="289fa-133">使用`HttpConnectionDispatcherOptions`配置与传输和内存缓冲区管理相关的高级的设置。</span><span class="sxs-lookup"><span data-stu-id="289fa-133">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="289fa-134">通过将传递委托，配置这些选项[ `MapHub<T>` ](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)。</span><span class="sxs-lookup"><span data-stu-id="289fa-134">These options are configured by passing a delegate to [`MapHub<T>`](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub).</span></span>

| <span data-ttu-id="289fa-135">选项</span><span class="sxs-lookup"><span data-stu-id="289fa-135">Option</span></span> | <span data-ttu-id="289fa-136">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-136">Description</span></span> |
| ------ | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="289fa-137">从客户端接收的字节数最大数量的服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="289fa-137">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="289fa-138">增加此值允许服务器以接收更大的消息，但会降低内存占用情况。</span><span class="sxs-lookup"><span data-stu-id="289fa-138">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="289fa-139">默认值为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="289fa-139">The default value is 32KB.</span></span> |
| `AuthorizationData` | <span data-ttu-id="289fa-140">一系列[ `IAuthorizeData` ](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata)对象用于确定客户端有权连接到中心。</span><span class="sxs-lookup"><span data-stu-id="289fa-140">A list of [`IAuthorizeData`](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> <span data-ttu-id="289fa-141">默认情况下，这填充的值从`Authorize`应用于集线器类的特性。</span><span class="sxs-lookup"><span data-stu-id="289fa-141">By default, this is populated with values from the `Authorize` attributes applied to the Hub class.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="289fa-142">最大的应用发送的字节数的服务器缓冲区。</span><span class="sxs-lookup"><span data-stu-id="289fa-142">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="289fa-143">增加此值允许服务器以发送较大的消息，但会降低内存占用情况。</span><span class="sxs-lookup"><span data-stu-id="289fa-143">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="289fa-144">默认值为 32 KB。</span><span class="sxs-lookup"><span data-stu-id="289fa-144">The default value is 32KB.</span></span> |
| `Transports` | <span data-ttu-id="289fa-145">一个位掩码的`HttpTransportType`值可用于限制传输客户端可用来连接。</span><span class="sxs-lookup"><span data-stu-id="289fa-145">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> <span data-ttu-id="289fa-146">默认情况下启用所有传输。</span><span class="sxs-lookup"><span data-stu-id="289fa-146">All transports are enabled by default.</span></span> |
| `LongPolling` | <span data-ttu-id="289fa-147">特定于长轮询传输的其他选项。</span><span class="sxs-lookup"><span data-stu-id="289fa-147">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="289fa-148">其他选项特定于 Websocket 传输。</span><span class="sxs-lookup"><span data-stu-id="289fa-148">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="289fa-149">长轮询传输中包含其他选项，可以使用配置`LongPolling`属性：</span><span class="sxs-lookup"><span data-stu-id="289fa-149">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="289fa-150">选项</span><span class="sxs-lookup"><span data-stu-id="289fa-150">Option</span></span> | <span data-ttu-id="289fa-151">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-151">Description</span></span> |
| ------ | ----------- |
| `PollTimeout` | <span data-ttu-id="289fa-152">服务器等待要终止单个轮询请求之前发送到客户端的消息的最大时间量。</span><span class="sxs-lookup"><span data-stu-id="289fa-152">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="289fa-153">减小此值会导致客户端更频繁地发出新轮询请求。</span><span class="sxs-lookup"><span data-stu-id="289fa-153">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> <span data-ttu-id="289fa-154">默认值为 90 秒。</span><span class="sxs-lookup"><span data-stu-id="289fa-154">The default value is 90 seconds.</span></span> |

<span data-ttu-id="289fa-155">WebSocket 传输中包含其他选项，可以使用配置`WebSockets`属性：</span><span class="sxs-lookup"><span data-stu-id="289fa-155">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="289fa-156">选项</span><span class="sxs-lookup"><span data-stu-id="289fa-156">Option</span></span> | <span data-ttu-id="289fa-157">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-157">Description</span></span> |
| ------ | ----------- |
| `CloseTimeout` | <span data-ttu-id="289fa-158">在服务器关闭，如果客户端无法在此时间间隔内关闭后，连接将终止。</span><span class="sxs-lookup"><span data-stu-id="289fa-158">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | <span data-ttu-id="289fa-159">一个委托，它可以用来设置`Sec-WebSocket-Protocol`为自定义值的标头。</span><span class="sxs-lookup"><span data-stu-id="289fa-159">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="289fa-160">该委托接收作为输入客户端请求的值，并应返回所需的值。</span><span class="sxs-lookup"><span data-stu-id="289fa-160">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="289fa-161">配置客户端选项</span><span class="sxs-lookup"><span data-stu-id="289fa-161">Configure client options</span></span>

<span data-ttu-id="289fa-162">可以在配置客户端选项`HubConnectionBuilder`类型 （适用于.NET 和 JavaScript 客户端），以及`HubConnection`本身。</span><span class="sxs-lookup"><span data-stu-id="289fa-162">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="289fa-163">配置日志记录</span><span class="sxs-lookup"><span data-stu-id="289fa-163">Configure logging</span></span>

<span data-ttu-id="289fa-164">使用.NET 客户端中配置日志记录`ConfigureLogging`方法。</span><span class="sxs-lookup"><span data-stu-id="289fa-164">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="289fa-165">可以在相同的方式注册日志记录提供程序和筛选器，因为它们是在服务器上。</span><span class="sxs-lookup"><span data-stu-id="289fa-165">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="289fa-166">请参阅[登录 ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) 文档以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="289fa-166">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="289fa-167">若要注册日志记录提供程序，必须安装所需的包。</span><span class="sxs-lookup"><span data-stu-id="289fa-167">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="289fa-168">请参阅[内置日志记录提供程序](xref:fundamentals/logging/index#built-in-logging-providers)部分有关的完整列表。</span><span class="sxs-lookup"><span data-stu-id="289fa-168">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="289fa-169">例如，若要启用控制台日志记录，安装`Microsoft.Extensions.Logging.Console`NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="289fa-169">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="289fa-170">调用`AddConsole`扩展方法：</span><span class="sxs-lookup"><span data-stu-id="289fa-170">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="289fa-171">在 JavaScript 客户端，类似`configureLogging`方法存在。</span><span class="sxs-lookup"><span data-stu-id="289fa-171">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="289fa-172">提供`LogLevel`值，该值指示要生成的日志消息的最小级别。</span><span class="sxs-lookup"><span data-stu-id="289fa-172">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="289fa-173">日志将写入浏览器控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="289fa-173">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="289fa-174">若要禁用完全日志记录，请指定`signalR.LogLevel.None`在`configureLogging`方法。</span><span class="sxs-lookup"><span data-stu-id="289fa-174">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="289fa-175">下面列出了可用于 JavaScript 客户端的日志级别。</span><span class="sxs-lookup"><span data-stu-id="289fa-175">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="289fa-176">将日志级别设置为下列值之一，则记录上的消息**或更高版本**该级别。</span><span class="sxs-lookup"><span data-stu-id="289fa-176">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="289fa-177">级别</span><span class="sxs-lookup"><span data-stu-id="289fa-177">Level</span></span> | <span data-ttu-id="289fa-178">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-178">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="289fa-179">未不记录任何消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-179">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="289fa-180">表示在整个应用程序时失败的消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-180">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="289fa-181">表示在当前操作失败的消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-181">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="289fa-182">表示非致命性问题的消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-182">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="289fa-183">信息性消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-183">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="289fa-184">用于调试的诊断消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-184">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="289fa-185">用于诊断特定问题非常详细的诊断消息。</span><span class="sxs-lookup"><span data-stu-id="289fa-185">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="289fa-186">配置允许的传输</span><span class="sxs-lookup"><span data-stu-id="289fa-186">Configure allowed transports</span></span>

<span data-ttu-id="289fa-187">可以在中配置的 SignalR 使用的传输`WithUrl`调用 (`withUrl`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="289fa-187">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="289fa-188">位 OR 运算的值`HttpTransportType`可以用于限制客户端仅使用指定的传输。</span><span class="sxs-lookup"><span data-stu-id="289fa-188">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="289fa-189">默认情况下启用所有传输。</span><span class="sxs-lookup"><span data-stu-id="289fa-189">All transports are enabled by default.</span></span>

<span data-ttu-id="289fa-190">例如，若要禁用服务器发送事件传输，但允许 Websocket 和长轮询连接：</span><span class="sxs-lookup"><span data-stu-id="289fa-190">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="289fa-191">在 JavaScript 客户端，通过设置来配置传输`transport`字段上的选项对象提供给`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="289fa-191">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="289fa-192">配置持有者身份验证</span><span class="sxs-lookup"><span data-stu-id="289fa-192">Configure bearer authentication</span></span>

<span data-ttu-id="289fa-193">若要提供身份验证数据以及 SignalR 请求，请使用`AccessTokenProvider`选项 (`accessTokenFactory`在 JavaScript 中) 指定函数返回的所需的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="289fa-193">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="289fa-194">在.NET 客户端，此访问令牌作为传入 HTTP"持有者身份验证"令牌 (使用`Authorization`具有一种类型的标头`Bearer`)。</span><span class="sxs-lookup"><span data-stu-id="289fa-194">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="289fa-195">在 JavaScript 客户端，使用访问令牌作为持有者令牌，**除**在少数情况下，在其中浏览器 Api 限制应用 （具体而言，在服务器发送事件和 Websocket 请求） 的标头的能力。</span><span class="sxs-lookup"><span data-stu-id="289fa-195">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="289fa-196">在这些情况下，查询字符串值中提供的访问令牌`access_token`。</span><span class="sxs-lookup"><span data-stu-id="289fa-196">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="289fa-197">在.NET 客户端，`AccessTokenProvider`可以使用中的选项委托指定选项`WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="289fa-197">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

<span data-ttu-id="289fa-198">在 JavaScript 客户端，通过设置配置的访问令牌`accessTokenFactory`字段中的选项对象`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="289fa-198">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

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

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="289fa-199">配置超时和保持活动状态的选项</span><span class="sxs-lookup"><span data-stu-id="289fa-199">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="289fa-200">还提供用于配置超时和保持活动状态的行为的其他选项`HubConnection`对象本身：</span><span class="sxs-lookup"><span data-stu-id="289fa-200">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="289fa-201">.NET 选项</span><span class="sxs-lookup"><span data-stu-id="289fa-201">.NET Option</span></span> | <span data-ttu-id="289fa-202">JavaScript 选项</span><span class="sxs-lookup"><span data-stu-id="289fa-202">JavaScript Option</span></span> | <span data-ttu-id="289fa-203">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-203">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="289fa-204">服务器活动的超时时间。</span><span class="sxs-lookup"><span data-stu-id="289fa-204">Timeout for server activity.</span></span> <span data-ttu-id="289fa-205">如果服务器尚未在此时间间隔内发送一条消息，客户端会考虑服务器断开连接和触发器`Closed`事件 (`onclose`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="289fa-205">If the server hasn't sent a message in this interval, the client considers the server disconnected and triggers the `Closed` event (`onclose` in JavaScript).</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="289fa-206">不可配置</span><span class="sxs-lookup"><span data-stu-id="289fa-206">Not configurable</span></span> | <span data-ttu-id="289fa-207">初始服务器握手的超时时间。</span><span class="sxs-lookup"><span data-stu-id="289fa-207">Timeout for initial server handshake.</span></span> <span data-ttu-id="289fa-208">如果服务器不在此时间间隔内发送握手响应，客户端取消握手和触发器`Closed`事件 (`onclose`在 JavaScript 中)。</span><span class="sxs-lookup"><span data-stu-id="289fa-208">If the server doesn't send a handshake response in this interval, the client cancels the handshake and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="289fa-209">这是一种高级的设置，如果由于出现严重的网络延迟发生握手超时错误应仅修改。</span><span class="sxs-lookup"><span data-stu-id="289fa-209">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="289fa-210">握手过程的更多详细信息，请参阅[SignalR 集线器协议规范](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)。</span><span class="sxs-lookup"><span data-stu-id="289fa-210">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |

<span data-ttu-id="289fa-211">在.NET 客户端，超时值指定为`TimeSpan`值。</span><span class="sxs-lookup"><span data-stu-id="289fa-211">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="289fa-212">在 JavaScript 客户端，超时值指定为一个数字，指示以毫秒为单位的持续时间。</span><span class="sxs-lookup"><span data-stu-id="289fa-212">In the JavaScript client, timeout values are specified as a number indicating the duration in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="289fa-213">配置其他选项</span><span class="sxs-lookup"><span data-stu-id="289fa-213">Configure additional options</span></span>

<span data-ttu-id="289fa-214">可以在配置其他选项`WithUrl`(`withUrl`在 JavaScript 中) 上的方法`HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="289fa-214">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="289fa-215">.NET 选项</span><span class="sxs-lookup"><span data-stu-id="289fa-215">.NET Option</span></span> | <span data-ttu-id="289fa-216">JavaScript 选项</span><span class="sxs-lookup"><span data-stu-id="289fa-216">JavaScript Option</span></span> | <span data-ttu-id="289fa-217">描述</span><span class="sxs-lookup"><span data-stu-id="289fa-217">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | <span data-ttu-id="289fa-218">返回一个字符串，作为持有者身份验证令牌的 HTTP 请求中提供的函数。</span><span class="sxs-lookup"><span data-stu-id="289fa-218">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | <span data-ttu-id="289fa-219">将此设置为`true`跳过协商步骤。</span><span class="sxs-lookup"><span data-stu-id="289fa-219">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="289fa-220">**WebSockets 传输是唯一的已启用的传输时，才支持**。</span><span class="sxs-lookup"><span data-stu-id="289fa-220">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="289fa-221">使用 Azure SignalR 服务时，不能启用此设置。</span><span class="sxs-lookup"><span data-stu-id="289fa-221">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="289fa-222">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-222">Not configurable \*</span></span> | <span data-ttu-id="289fa-223">若要发送请求进行身份验证的 TLS 证书的集合。</span><span class="sxs-lookup"><span data-stu-id="289fa-223">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="289fa-224">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-224">Not configurable \*</span></span> | <span data-ttu-id="289fa-225">要与每个 HTTP 请求一起发送的 HTTP cookie 的集合。</span><span class="sxs-lookup"><span data-stu-id="289fa-225">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="289fa-226">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-226">Not configurable \*</span></span> | <span data-ttu-id="289fa-227">要与每个 HTTP 请求一起发送的凭据。</span><span class="sxs-lookup"><span data-stu-id="289fa-227">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="289fa-228">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-228">Not configurable \*</span></span> | <span data-ttu-id="289fa-229">仅 Websocket。</span><span class="sxs-lookup"><span data-stu-id="289fa-229">WebSockets only.</span></span> <span data-ttu-id="289fa-230">最长时间之后关闭服务器以确认关闭请求等待客户端。</span><span class="sxs-lookup"><span data-stu-id="289fa-230">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="289fa-231">如果服务器不在此时间内收到结束时，客户端断开连接。</span><span class="sxs-lookup"><span data-stu-id="289fa-231">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="289fa-232">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-232">Not configurable \*</span></span> | <span data-ttu-id="289fa-233">附加 HTTP 标头要与每个 HTTP 请求一起发送的字典。</span><span class="sxs-lookup"><span data-stu-id="289fa-233">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="289fa-234">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-234">Not configurable \*</span></span> | <span data-ttu-id="289fa-235">一个委托，它可用于配置或替换`HttpMessageHandler`用于发送 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="289fa-235">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="289fa-236">不用于 WebSocket 连接。</span><span class="sxs-lookup"><span data-stu-id="289fa-236">Not used for WebSocket connections.</span></span> <span data-ttu-id="289fa-237">此委托必须返回一个非 null 值，并接收作为参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="289fa-237">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="289fa-238">修改该默认值上的设置，返回它，或者返回完整的全新`HttpMessageHandler`实例。</span><span class="sxs-lookup"><span data-stu-id="289fa-238">Either modify settings on that default value and return it, or return a completely new `HttpMessageHandler` instance.</span></span> |
| `Proxy` | <span data-ttu-id="289fa-239">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-239">Not configurable \*</span></span> | <span data-ttu-id="289fa-240">发送 HTTP 请求时要使用 HTTP 代理。</span><span class="sxs-lookup"><span data-stu-id="289fa-240">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="289fa-241">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-241">Not configurable \*</span></span> | <span data-ttu-id="289fa-242">设置此布尔值，若要发送的 HTTP 和 Websocket 请求的默认凭据。</span><span class="sxs-lookup"><span data-stu-id="289fa-242">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="289fa-243">这使使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="289fa-243">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="289fa-244">不可配置 \*</span><span class="sxs-lookup"><span data-stu-id="289fa-244">Not configurable \*</span></span> | <span data-ttu-id="289fa-245">一个委托，可用于配置更多的 WebSocket 选项。</span><span class="sxs-lookup"><span data-stu-id="289fa-245">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="289fa-246">接收的实例[ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions)可用于配置选项。</span><span class="sxs-lookup"><span data-stu-id="289fa-246">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="289fa-247">选项标有星号 （\*） 不是可在 JavaScript 客户端，由于浏览器 Api 中的限制中配置的。</span><span class="sxs-lookup"><span data-stu-id="289fa-247">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="289fa-248">在.NET 客户端，这些选项可以修改选项委托提供给`WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="289fa-248">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="289fa-249">在 JavaScript 客户端，可以提供给 JavaScript 对象中提供这些选项`withUrl`:</span><span class="sxs-lookup"><span data-stu-id="289fa-249">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="289fa-250">其他资源</span><span class="sxs-lookup"><span data-stu-id="289fa-250">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
