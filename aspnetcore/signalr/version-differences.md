---
title: SignalR 和 ASP.NET Core SignalR 之间的差异
author: tdykstra
description: SignalR 和 ASP.NET Core SignalR 之间的差异
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 09/10/2018
uid: signalr/version-differences
ms.openlocfilehash: ea2de2606a99de70fa645c0c42303525fea0a44e
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325531"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="ca5ea-103">ASP.NET SignalR 和 ASP.NET Core SignalR 之间的差异</span><span class="sxs-lookup"><span data-stu-id="ca5ea-103">Differences between ASP.NET SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="ca5ea-104">ASP.NET Core SignalR 不允许客户端或 ASP.NET SignalR 的服务器。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-104">ASP.NET Core SignalR isn't compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="ca5ea-105">本文详细介绍了已删除或更改在 ASP.NET Core SignalR 中的功能。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-105">This article details features which have been removed or changed in ASP.NET Core SignalR.</span></span>

## <a name="how-to-identify-the-signalr-version"></a><span data-ttu-id="ca5ea-106">如何识别 SignalR 版本</span><span class="sxs-lookup"><span data-stu-id="ca5ea-106">How to identify the SignalR version</span></span>

|                      | <span data-ttu-id="ca5ea-107">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="ca5ea-107">ASP.NET SignalR</span></span> | <span data-ttu-id="ca5ea-108">ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="ca5ea-108">ASP.NET Core SignalR</span></span> |
| -------------------- | --------------- | -------------------- |
| <span data-ttu-id="ca5ea-109">服务器 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ca5ea-109">Server NuGet Package</span></span> | [<span data-ttu-id="ca5ea-110">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="ca5ea-110">Microsoft.AspNet.SignalR</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | <span data-ttu-id="ca5ea-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="ca5ea-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span></span><br><span data-ttu-id="ca5ea-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="ca5ea-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span></span> |
| <span data-ttu-id="ca5ea-113">客户端 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ca5ea-113">Client NuGet Packages</span></span> | [<span data-ttu-id="ca5ea-114">Microsoft.AspNet.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="ca5ea-114">Microsoft.AspNet.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[<span data-ttu-id="ca5ea-115">Microsoft.AspNet.SignalR.JS</span><span class="sxs-lookup"><span data-stu-id="ca5ea-115">Microsoft.AspNet.SignalR.JS</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [<span data-ttu-id="ca5ea-116">Microsoft.AspNetCore.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="ca5ea-116">Microsoft.AspNetCore.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| <span data-ttu-id="ca5ea-117">客户端 npm 包</span><span class="sxs-lookup"><span data-stu-id="ca5ea-117">Client npm Package</span></span> | [<span data-ttu-id="ca5ea-118">signalr</span><span class="sxs-lookup"><span data-stu-id="ca5ea-118">signalr</span></span>](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| <span data-ttu-id="ca5ea-119">服务器应用程序类型</span><span class="sxs-lookup"><span data-stu-id="ca5ea-119">Server App Type</span></span> | <span data-ttu-id="ca5ea-120">ASP.NET (System.Web) 或 OWIN 自托管</span><span class="sxs-lookup"><span data-stu-id="ca5ea-120">ASP.NET (System.Web) or OWIN Self-Host</span></span> | <span data-ttu-id="ca5ea-121">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca5ea-121">ASP.NET Core</span></span> |
| <span data-ttu-id="ca5ea-122">受支持的服务器平台</span><span class="sxs-lookup"><span data-stu-id="ca5ea-122">Supported Server Platforms</span></span> | <span data-ttu-id="ca5ea-123">.NET framework 4.5 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ca5ea-123">.NET Framework 4.5 or later</span></span> | <span data-ttu-id="ca5ea-124">.NET Framework 4.6.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ca5ea-124">.NET Framework 4.6.1 or later</span></span><br><span data-ttu-id="ca5ea-125">.NET core 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ca5ea-125">.NET Core 2.1 or later</span></span> |

## <a name="feature-differences"></a><span data-ttu-id="ca5ea-126">功能差异</span><span class="sxs-lookup"><span data-stu-id="ca5ea-126">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="ca5ea-127">自动重新连接</span><span class="sxs-lookup"><span data-stu-id="ca5ea-127">Automatic reconnects</span></span>

<span data-ttu-id="ca5ea-128">在 ASP.NET Core SignalR 中不支持自动重新连接。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-128">Automatic reconnects aren't supported in ASP.NET Core SignalR.</span></span> <span data-ttu-id="ca5ea-129">如果客户端已断开连接，用户必须显式会启动新的连接，如果用户想要重新连接。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-129">If the client is disconnected, the user must explicitly start a new connection if they want to reconnect.</span></span> <span data-ttu-id="ca5ea-130">在 ASP.NET SignalR，SignalR 尝试重新连接到服务器，如果在连接断开。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-130">In ASP.NET SignalR, SignalR attempts to reconnect to the server if the connection is dropped.</span></span> 

### <a name="protocol-support"></a><span data-ttu-id="ca5ea-131">协议支持</span><span class="sxs-lookup"><span data-stu-id="ca5ea-131">Protocol support</span></span>

<span data-ttu-id="ca5ea-132">ASP.NET Core SignalR 支持 JSON，以及一种新的二进制协议，它基于[MessagePack](xref:signalr/messagepackhubprotocol)。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-132">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="ca5ea-133">此外，可以创建自定义协议。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-133">Additionally, custom protocols can be created.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="ca5ea-134">在服务器上的差异</span><span class="sxs-lookup"><span data-stu-id="ca5ea-134">Differences on the server</span></span>

<span data-ttu-id="ca5ea-135">ASP.NET Core SignalR 服务器端库包含在[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)包的一部分**ASP.NET Core Web 应用程序**Razor 和 MVC 模板项目。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-135">The ASP.NET Core SignalR server-side libraries are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) package that's part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="ca5ea-136">ASP.NET Core SignalR 是 ASP.NET Core 中间件，因此它必须通过调用配置[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)中`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-136">ASP.NET Core SignalR is an ASP.NET Core middleware, so it must be configured by calling [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR()
```

<span data-ttu-id="ca5ea-137">若要配置路由，请将路由映射到中心内[UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr)方法调用中`Startup.Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-137">To configure routing, map routes to hubs inside the [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a><span data-ttu-id="ca5ea-138">现在需要粘性会话</span><span class="sxs-lookup"><span data-stu-id="ca5ea-138">Sticky sessions now required</span></span>

<span data-ttu-id="ca5ea-139">由于扩展的工作方式在 ASP.NET SignalR 中，客户端无法重新连接，并将消息发送到服务器场中的任何服务器。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-139">Because of how scale-out worked in ASP.NET SignalR, clients could reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="ca5ea-140">由于对横向扩展模型，以及不支持重新连接更改，这不再受支持。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-140">Due to changes to the scale-out model, as well as not supporting reconnects, this is no longer supported.</span></span> <span data-ttu-id="ca5ea-141">客户端连接到服务器后，它必须与交互在同一台服务器连接的持续时间。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-141">Once the client connects to the server, it must interact with the same server for the duration of the connection.</span></span>

### <a name="single-hub-per-connection"></a><span data-ttu-id="ca5ea-142">每个连接的单个中心</span><span class="sxs-lookup"><span data-stu-id="ca5ea-142">Single hub per connection</span></span>

<span data-ttu-id="ca5ea-143">在 ASP.NET Core SignalR 连接模型进行了简化。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-143">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="ca5ea-144">直接向单个中心，而不是单个连接正在使用共享到多个中心的访问权限进行连接。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-144">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="ca5ea-145">流式处理</span><span class="sxs-lookup"><span data-stu-id="ca5ea-145">Streaming</span></span>

<span data-ttu-id="ca5ea-146">ASP.NET Core SignalR 现在支持[流式处理数据](xref:signalr/streaming)从中心向客户端。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-146">ASP.NET Core SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="ca5ea-147">状态</span><span class="sxs-lookup"><span data-stu-id="ca5ea-147">State</span></span>

<span data-ttu-id="ca5ea-148">已删除将任意状态传递客户端与中心 （通常称为 HubState） 之间的功能，以及对进度消息的支持。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-148">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="ca5ea-149">目前中心代理没有对应。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-149">There is no counterpart of hub proxies at the moment.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="ca5ea-150">在客户端上的差异</span><span class="sxs-lookup"><span data-stu-id="ca5ea-150">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="ca5ea-151">TypeScript</span><span class="sxs-lookup"><span data-stu-id="ca5ea-151">TypeScript</span></span>

<span data-ttu-id="ca5ea-152">ASP.NET Core SignalR 客户端用[TypeScript](https://www.typescriptlang.org/)。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-152">The ASP.NET Core SignalR client is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="ca5ea-153">使用时，可以编写 JavaScript 或 TypeScript [JavaScript 客户端](xref:signalr/javascript-client)。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-153">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="ca5ea-154">JavaScript 客户端托管于[npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="ca5ea-154">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="ca5ea-155">在上一版本中，JavaScript 客户端已通过在 Visual Studio 中的 NuGet 包获取。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-155">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="ca5ea-156">对于核心版本中， [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 包中包含的 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-156">For the Core versions, the [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm package contains the JavaScript libraries.</span></span> <span data-ttu-id="ca5ea-157">此包不包括在**ASP.NET Core Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-157">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="ca5ea-158">使用 npm 获取并安装`@aspnet/signalr`npm 包。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-158">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="ca5ea-159">jQuery</span><span class="sxs-lookup"><span data-stu-id="ca5ea-159">jQuery</span></span>

<span data-ttu-id="ca5ea-160">已删除对 jQuery 的依赖关系，但项目仍然可以使用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-160">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="ca5ea-161">JavaScript 客户端方法语法</span><span class="sxs-lookup"><span data-stu-id="ca5ea-161">JavaScript client method syntax</span></span>

<span data-ttu-id="ca5ea-162">JavaScript 语法已从以前版本的 SignalR。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-162">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="ca5ea-163">而不是使用`$connection`对象，请创建连接使用[HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-163">Rather than using the `$connection` object, create a connection using the [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="ca5ea-164">使用[上](/javascript/api/@aspnet/signalr/HubConnection#on)方法，以指定客户端可以调用该集线器的方法。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-164">Use the [on](/javascript/api/@aspnet/signalr/HubConnection#on) method to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="ca5ea-165">在创建后的客户端方法，启动集线器连接。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-165">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="ca5ea-166">链[捕获](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)方法来记录或处理的错误。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-166">Chain a [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="ca5ea-167">中心代理</span><span class="sxs-lookup"><span data-stu-id="ca5ea-167">Hub proxies</span></span>

<span data-ttu-id="ca5ea-168">不能再自动生成中心代理。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-168">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="ca5ea-169">相反，传递到方法名称[调用](/javascript/api/%40aspnet/signalr/hubconnection#invoke)以字符串形式的 API。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-169">Instead, the method name is passed into the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="ca5ea-170">.NET 和其他客户端</span><span class="sxs-lookup"><span data-stu-id="ca5ea-170">.NET and other clients</span></span>

<span data-ttu-id="ca5ea-171">`Microsoft.AspNetCore.SignalR.Client` NuGet 程序包包含 ASP.NET Core signalr 的.NET 客户端库。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-171">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="ca5ea-172">使用[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)创建和生成到集线器的连接的实例。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-172">Use the [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a><span data-ttu-id="ca5ea-173">横向扩展差异</span><span class="sxs-lookup"><span data-stu-id="ca5ea-173">Scaleout differences</span></span>

<span data-ttu-id="ca5ea-174">ASP.NET SignalR 支持 SQL Server 和 Redis。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-174">ASP.NET SignalR supports both SQL Server and Redis.</span></span> <span data-ttu-id="ca5ea-175">ASP.NET Core SignalR 支持 Azure SignalR 服务和 Redis。</span><span class="sxs-lookup"><span data-stu-id="ca5ea-175">ASP.NET Core SignalR supports both Azure SignalR Service and Redis.</span></span>

### <a name="aspnet"></a><span data-ttu-id="ca5ea-176">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ca5ea-176">ASP.NET</span></span>

* [<span data-ttu-id="ca5ea-177">使用 Azure 服务总线的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="ca5ea-177">SignalR scaleout with Azure Service Bus</span></span>](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [<span data-ttu-id="ca5ea-178">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="ca5ea-178">SignalR scaleout with Redis</span></span>](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [<span data-ttu-id="ca5ea-179">使用 SQL Server 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="ca5ea-179">SignalR scaleout with SQL Server</span></span>](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a><span data-ttu-id="ca5ea-180">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca5ea-180">ASP.NET Core</span></span>

* [<span data-ttu-id="ca5ea-181">Azure SignalR 服务</span><span class="sxs-lookup"><span data-stu-id="ca5ea-181">Azure SignalR Service</span></span>](/azure/azure-signalr/)

## <a name="additional-resources"></a><span data-ttu-id="ca5ea-182">其他资源</span><span class="sxs-lookup"><span data-stu-id="ca5ea-182">Additional resources</span></span>

* [<span data-ttu-id="ca5ea-183">中心</span><span class="sxs-lookup"><span data-stu-id="ca5ea-183">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="ca5ea-184">JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="ca5ea-184">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="ca5ea-185">.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="ca5ea-185">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="ca5ea-186">支持的平台</span><span class="sxs-lookup"><span data-stu-id="ca5ea-186">Supported platforms</span></span>](xref:signalr/supported-platforms)
