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
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="4da4e-103">SignalR 和 ASP.NET Core SignalR 之间的差异</span><span class="sxs-lookup"><span data-stu-id="4da4e-103">Differences between SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="4da4e-104">ASP.NET Core SignalR 与不兼容客户端或适用于 ASP.NET SignalR 的服务器。</span><span class="sxs-lookup"><span data-stu-id="4da4e-104">ASP.NET Core SignalR is not compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="4da4e-105">此文章详细介绍了已删除或更改在 ASP.NET Core SignalR 的功能。</span><span class="sxs-lookup"><span data-stu-id="4da4e-105">This article details the features which have been removed or changed in the ASP.NET Core SignalR.</span></span>

## <a name="feature-differences"></a><span data-ttu-id="4da4e-106">功能差异</span><span class="sxs-lookup"><span data-stu-id="4da4e-106">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="4da4e-107">自动重新连接</span><span class="sxs-lookup"><span data-stu-id="4da4e-107">Automatic reconnects</span></span>

<span data-ttu-id="4da4e-108">不再支持自动重新连接。</span><span class="sxs-lookup"><span data-stu-id="4da4e-108">Automatic reconnects are no longer supported.</span></span> <span data-ttu-id="4da4e-109">以前，SignalR 尝试重新连接到服务器，如果连接已断开。</span><span class="sxs-lookup"><span data-stu-id="4da4e-109">Previously, SignalR tried to reconnect to the server if the connection was dropped.</span></span> <span data-ttu-id="4da4e-110">现在，如果断开客户端用户必须显式会启动一个新连接，如果他们想要重新连接。</span><span class="sxs-lookup"><span data-stu-id="4da4e-110">Now, if the client is disconnected the user must explicitly start a new connection if they want to reconnect.</span></span>

### <a name="protocol-support"></a><span data-ttu-id="4da4e-111">协议支持</span><span class="sxs-lookup"><span data-stu-id="4da4e-111">Protocol support</span></span>

<span data-ttu-id="4da4e-112">ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。</span><span class="sxs-lookup"><span data-stu-id="4da4e-112">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="4da4e-113">此外，可以创建自定义协议。</span><span class="sxs-lookup"><span data-stu-id="4da4e-113">Additionally, custom protocols can be created.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="4da4e-114">在服务器上的差异</span><span class="sxs-lookup"><span data-stu-id="4da4e-114">Differences on the server</span></span>

<span data-ttu-id="4da4e-115">SignalR 服务器端库包含在`Microsoft.AspNetCore.App`是的一部分的包**ASP.NET Core Web 应用程序**Razor 和 MVC 项目模板的。</span><span class="sxs-lookup"><span data-stu-id="4da4e-115">The SignalR server-side libraries are included in the `Microsoft.AspNetCore.App` package that is part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="4da4e-116">SignalR 是 ASP.NET Core 中间件，因此它必须通过调用配置`AddSignalR`中`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="4da4e-116">SignalR is an ASP.NET Core middleware, so it must be configured by calling `AddSignalR` in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR();
```

<span data-ttu-id="4da4e-117">若要配置路由，请将路由映射到内的中心`UseSignalR`方法调用`Startup.Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="4da4e-117">To configure routing, map routes to hubs inside the `UseSignalR` method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a><span data-ttu-id="4da4e-118">现在所需的粘性会话</span><span class="sxs-lookup"><span data-stu-id="4da4e-118">Sticky sessions now required</span></span>

<span data-ttu-id="4da4e-119">由于横向扩展的工作方式在以前版本的 SignalR，客户端无法重新连接，并将消息发送到服务器场中的任何服务器。</span><span class="sxs-lookup"><span data-stu-id="4da4e-119">Because of how scale-out worked in the previous versions of SignalR, clients could reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="4da4e-120">由于更改应用于横向扩展模型，以及不支持重新连接，这不再受支持。</span><span class="sxs-lookup"><span data-stu-id="4da4e-120">Due to changes to the scale-out model, as well as not supporting reconnects, this is no longer supported.</span></span> <span data-ttu-id="4da4e-121">现在，客户端连接到服务器后它需要进行连接的持续时间内与同一台服务器交互。</span><span class="sxs-lookup"><span data-stu-id="4da4e-121">Now, once the client connects to the server it needs to interact with the same server for the duration of the connection.</span></span>

### <a name="single-hub-per-connection"></a><span data-ttu-id="4da4e-122">每个连接的单个中心</span><span class="sxs-lookup"><span data-stu-id="4da4e-122">Single hub per connection</span></span>

<span data-ttu-id="4da4e-123">在 ASP.NET Core SignalR 连接模型进行了简化。</span><span class="sxs-lookup"><span data-stu-id="4da4e-123">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="4da4e-124">直接对单个中心，而不是单个连接用于共享对多个中心访问权限进行连接。</span><span class="sxs-lookup"><span data-stu-id="4da4e-124">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="4da4e-125">流式处理</span><span class="sxs-lookup"><span data-stu-id="4da4e-125">Streaming</span></span>

<span data-ttu-id="4da4e-126">SignalR 现在支持[流式处理数据](xref:signalr/streaming)从客户端到中心。</span><span class="sxs-lookup"><span data-stu-id="4da4e-126">SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="4da4e-127">状态</span><span class="sxs-lookup"><span data-stu-id="4da4e-127">State</span></span>

<span data-ttu-id="4da4e-128">将任意状态传递客户端与中心 （通常称为 HubState） 之间的功能已删除，并且支持进度消息。</span><span class="sxs-lookup"><span data-stu-id="4da4e-128">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="4da4e-129">目前中心代理没有对应项。</span><span class="sxs-lookup"><span data-stu-id="4da4e-129">There is no counterpart of hub proxies at the moment.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="4da4e-130">客户端上的差异</span><span class="sxs-lookup"><span data-stu-id="4da4e-130">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="4da4e-131">TypeScript</span><span class="sxs-lookup"><span data-stu-id="4da4e-131">TypeScript</span></span>

<span data-ttu-id="4da4e-132">写入 SignalR 的 ASP.NET Core 版本[TypeScript](https://www.typescriptlang.org/)。</span><span class="sxs-lookup"><span data-stu-id="4da4e-132">The ASP.NET Core version of SignalR is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="4da4e-133">当使用时，可以编写在 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。</span><span class="sxs-lookup"><span data-stu-id="4da4e-133">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="4da4e-134">JavaScript 客户端托管在[npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="4da4e-134">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="4da4e-135">在以前版本中，JavaScript 客户端是通过 Visual Studio 中的 NuGet 包获得的。</span><span class="sxs-lookup"><span data-stu-id="4da4e-135">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="4da4e-136">对于核心版本中， [ @aspnet/signalr npm 包](https://www.npmjs.com/package/@aspnet/signalr)包含 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="4da4e-136">For the Core versions, the [@aspnet/signalr npm package](https://www.npmjs.com/package/@aspnet/signalr) contains the JavaScript libraries.</span></span> <span data-ttu-id="4da4e-137">此包不包括在**ASP.NET Core Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="4da4e-137">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="4da4e-138">使用 npm 获取并安装`@aspnet/signalr`npm 包。</span><span class="sxs-lookup"><span data-stu-id="4da4e-138">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="4da4e-139">jQuery</span><span class="sxs-lookup"><span data-stu-id="4da4e-139">jQuery</span></span>

<span data-ttu-id="4da4e-140">已删除对 jQuery 的依赖关系，不过项目仍然可以使用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="4da4e-140">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="4da4e-141">JavaScript 客户端方法语法</span><span class="sxs-lookup"><span data-stu-id="4da4e-141">JavaScript client method syntax</span></span>

<span data-ttu-id="4da4e-142">JavaScript 语法 SignalR 的先前版本中已更改。</span><span class="sxs-lookup"><span data-stu-id="4da4e-142">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="4da4e-143">而不是使用`$connection`对象，请创建连接使用`HubConnectionBuilder`API。</span><span class="sxs-lookup"><span data-stu-id="4da4e-143">Rather than using the `$connection` object, create a connection using the `HubConnectionBuilder` API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="4da4e-144">使用`connection.on`指定中心可以调用的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="4da4e-144">Use `connection.on` to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="4da4e-145">在创建客户端方法，启动集线器连接。</span><span class="sxs-lookup"><span data-stu-id="4da4e-145">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="4da4e-146">链`catch`方法可以登录或处理错误。</span><span class="sxs-lookup"><span data-stu-id="4da4e-146">Chain a `catch` method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="4da4e-147">中心代理</span><span class="sxs-lookup"><span data-stu-id="4da4e-147">Hub proxies</span></span>

<span data-ttu-id="4da4e-148">中心代理将不再自动生成。</span><span class="sxs-lookup"><span data-stu-id="4da4e-148">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="4da4e-149">相反，将方法名称传递给`invoke`字符串形式的 API。</span><span class="sxs-lookup"><span data-stu-id="4da4e-149">Instead, the method name is passed into the `invoke` API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="4da4e-150">.NET 和其他客户端</span><span class="sxs-lookup"><span data-stu-id="4da4e-150">.NET and other clients</span></span>

<span data-ttu-id="4da4e-151">`Microsoft.AspNetCore.SignalR.Client` NuGet 程序包包含 ASP.NET Core signalr 的.NET 客户端库。</span><span class="sxs-lookup"><span data-stu-id="4da4e-151">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="4da4e-152">使用`HubConnectionBuilder`若要创建和生成到一个中心的连接的实例。</span><span class="sxs-lookup"><span data-stu-id="4da4e-152">Use the `HubConnectionBuilder` to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="additional-resources"></a><span data-ttu-id="4da4e-153">其他资源</span><span class="sxs-lookup"><span data-stu-id="4da4e-153">Additional resources</span></span>

* [<span data-ttu-id="4da4e-154">中心</span><span class="sxs-lookup"><span data-stu-id="4da4e-154">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="4da4e-155">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="4da4e-155">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="4da4e-156">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="4da4e-156">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="4da4e-157">支持的平台</span><span class="sxs-lookup"><span data-stu-id="4da4e-157">Supported platforms</span></span>](xref:signalr/supported-platforms)
