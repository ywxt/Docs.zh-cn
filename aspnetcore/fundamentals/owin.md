---
title: ".NET 的开放 Web 接口 (OWIN)"
author: ardalis
description: "发现如何 ASP.NET Core 支持打开的 Web 接口的.NET (OWIN)，这允许 web 应用程序从 web 服务器分离。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/owin
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 42ffa01745b7a492b3b8cb2778805f254863b890
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-open-web-interface-for-net-owin"></a><span data-ttu-id="96089-103">若要打开.NET (OWIN) 的 Web 界面的简介</span><span class="sxs-lookup"><span data-stu-id="96089-103">Introduction to Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="96089-104">通过[Steve Smith](https://ardalis.com/)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="96089-104">By [Steve Smith](https://ardalis.com/) and  [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="96089-105">ASP.NET Core 支持 .NET 的开放 Web 接口 (OWIN)。</span><span class="sxs-lookup"><span data-stu-id="96089-105">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="96089-106">OWIN 允许 Web 应用从 Web 服务器分离。</span><span class="sxs-lookup"><span data-stu-id="96089-106">OWIN allows web apps to be decoupled from web servers.</span></span> <span data-ttu-id="96089-107">它定义的中间件来用于在管道中使用，以处理请求和响应关联的标准方法。</span><span class="sxs-lookup"><span data-stu-id="96089-107">It defines a standard way for middleware to be used in a pipeline to handle requests and associated responses.</span></span> <span data-ttu-id="96089-108">ASP.NET Core 应用程序和中间件可以与基于 OWIN 的应用程序、 服务器和中间件互操作。</span><span class="sxs-lookup"><span data-stu-id="96089-108">ASP.NET Core applications and middleware can interoperate with OWIN-based applications, servers, and middleware.</span></span>

<span data-ttu-id="96089-109">OWIN 提供了允许与不同的对象模型一起使用的两个框架解除层。</span><span class="sxs-lookup"><span data-stu-id="96089-109">OWIN provides a decoupling layer that allows two frameworks with disparate object models to be used together.</span></span> <span data-ttu-id="96089-110">`Microsoft.AspNetCore.Owin`包提供了两个适配器实现：</span><span class="sxs-lookup"><span data-stu-id="96089-110">The `Microsoft.AspNetCore.Owin` package provides two adapter implementations:</span></span>
- <span data-ttu-id="96089-111">OWIN 到 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="96089-111">ASP.NET Core to OWIN</span></span> 
- <span data-ttu-id="96089-112">OWIN 到 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="96089-112">OWIN to ASP.NET Core</span></span>

<span data-ttu-id="96089-113">这允许基于 OWIN 兼容服务器/主机，或在 ASP.NET Core 上运行其他 OWIN 兼容组件托管的 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="96089-113">This allows ASP.NET Core to be hosted on top of an OWIN compatible server/host, or for other OWIN compatible components to be run on top of ASP.NET Core.</span></span>

<span data-ttu-id="96089-114">注意： 使用这些适配器附带有一定的性能开销。</span><span class="sxs-lookup"><span data-stu-id="96089-114">Note: Using these adapters comes with a performance cost.</span></span> <span data-ttu-id="96089-115">使用仅 ASP.NET 核心组件的应用程序不应使用 Owin 包或适配器。</span><span class="sxs-lookup"><span data-stu-id="96089-115">Applications using only ASP.NET Core components shouldn't use the Owin package or adapters.</span></span>

<span data-ttu-id="96089-116">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="96089-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="running-owin-middleware-in-the-aspnet-pipeline"></a><span data-ttu-id="96089-117">在 ASP.NET 管线中运行 OWIN 中间件</span><span class="sxs-lookup"><span data-stu-id="96089-117">Running OWIN middleware in the ASP.NET pipeline</span></span>

<span data-ttu-id="96089-118">ASP.NET 核心 OWIN 支持部署的一部分`Microsoft.AspNetCore.Owin`包。</span><span class="sxs-lookup"><span data-stu-id="96089-118">ASP.NET Core's OWIN support is deployed as part of the `Microsoft.AspNetCore.Owin` package.</span></span> <span data-ttu-id="96089-119">你可以通过安装此包导入你的项目的 OWIN 支持。</span><span class="sxs-lookup"><span data-stu-id="96089-119">You can import OWIN support into your project by installing this package.</span></span>

<span data-ttu-id="96089-120">OWIN 中间件符合[OWIN 规范](http://owin.org/spec/spec/owin-1.0.0.html)，这要求`Func<IDictionary<string, object>, Task>`接口和特定的密钥设置 (如`owin.ResponseBody`)。</span><span class="sxs-lookup"><span data-stu-id="96089-120">OWIN middleware conforms to the [OWIN specification](http://owin.org/spec/spec/owin-1.0.0.html), which requires a `Func<IDictionary<string, object>, Task>` interface, and specific keys be set (such as `owin.ResponseBody`).</span></span> <span data-ttu-id="96089-121">以下简单的 OWIN 中间件将显示"Hello World":</span><span class="sxs-lookup"><span data-stu-id="96089-121">The following simple OWIN middleware displays "Hello World":</span></span>

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: http://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

<span data-ttu-id="96089-122">示例签名返回`Task`并接受`IDictionary<string, object>`OWIN 通过所需的方式。</span><span class="sxs-lookup"><span data-stu-id="96089-122">The sample signature returns a `Task` and accepts an `IDictionary<string, object>` as required by OWIN.</span></span>

<span data-ttu-id="96089-123">下面的代码演示如何添加`OwinHello`（上面所述） 向 ASP.NET 管道使用的中间件`UseOwin`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="96089-123">The following code shows how to add the `OwinHello` middleware (shown above) to the ASP.NET pipeline with the `UseOwin` extension method.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

<span data-ttu-id="96089-124">你可以配置在 OWIN 管道中进行其他操作。</span><span class="sxs-lookup"><span data-stu-id="96089-124">You can configure other actions to take place within the OWIN pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="96089-125">仅应在首次向响应流写入之前修改响应标头。</span><span class="sxs-lookup"><span data-stu-id="96089-125">Response headers should only be modified prior to the first write to the response stream.</span></span>

> [!NOTE]
> <span data-ttu-id="96089-126">多次调用`UseOwin`出于性能原因不建议这样做。</span><span class="sxs-lookup"><span data-stu-id="96089-126">Multiple calls to `UseOwin` is discouraged for performance reasons.</span></span> <span data-ttu-id="96089-127">如果组合在一起，OWIN 组件将最好地运行。</span><span class="sxs-lookup"><span data-stu-id="96089-127">OWIN components will operate best if grouped together.</span></span>

```csharp
app.UseOwin(pipeline =>
{
    pipeline(next =>
    {
        // do something before
        return OwinHello;
        // do something after
    });
});
```

<a name="hosting-on-owin"></a>

## <a name="using-aspnet-hosting-on-an-owin-based-server"></a><span data-ttu-id="96089-128">使用基于 OWIN 的服务器上的 ASP.NET 宿主</span><span class="sxs-lookup"><span data-stu-id="96089-128">Using ASP.NET Hosting on an OWIN-based server</span></span>

<span data-ttu-id="96089-129">基于 OWIN 的服务器可以承载 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="96089-129">OWIN-based servers can host ASP.NET applications.</span></span> <span data-ttu-id="96089-130">此类的一台服务器是[Nowin](https://github.com/Bobris/Nowin)，.NET OWIN web 服务器。</span><span class="sxs-lookup"><span data-stu-id="96089-130">One such server is [Nowin](https://github.com/Bobris/Nowin), a .NET OWIN web server.</span></span> <span data-ttu-id="96089-131">在本文示例中，我已包含引用 Nowin 并使用它来创建一个项目项目`IServer`能够自承载 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="96089-131">In the sample for this article, I've included a project that references Nowin and uses it to create an `IServer` capable of self-hosting ASP.NET Core.</span></span>

[!code-csharp[Main](owin/sample/src/NowinSample/Program.cs?highlight=15)]

<span data-ttu-id="96089-132">`IServer`是接口，需要`Features`属性和`Start`方法。</span><span class="sxs-lookup"><span data-stu-id="96089-132">`IServer` is an interface that requires an `Features` property and a `Start` method.</span></span>

<span data-ttu-id="96089-133">`Start`负责配置和启动服务器，在这种情况下通过一系列从 IServerAddressesFeature 设置地址分析的 fluent API 调用。</span><span class="sxs-lookup"><span data-stu-id="96089-133">`Start` is responsible for configuring and starting the server, which in this case is done through a series of fluent API calls that set addresses parsed from the IServerAddressesFeature.</span></span> <span data-ttu-id="96089-134">请注意的 fluent 配置`_builder`变量指定将由处理请求`appFunc`先前在方法中定义。</span><span class="sxs-lookup"><span data-stu-id="96089-134">Note that the fluent configuration of the `_builder` variable specifies that requests will be handled by the `appFunc` defined earlier in the method.</span></span> <span data-ttu-id="96089-135">这`Func`称为上每个请求以处理传入的请求。</span><span class="sxs-lookup"><span data-stu-id="96089-135">This `Func` is called on each request to process incoming requests.</span></span>

<span data-ttu-id="96089-136">我们还将添加`IWebHostBuilder`扩展，以便可以方便地添加和配置 Nowin 服务器。</span><span class="sxs-lookup"><span data-stu-id="96089-136">We'll also add an `IWebHostBuilder` extension to make it easy to add and configure the Nowin server.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Hosting.Server;
using Microsoft.Extensions.DependencyInjection;
using Nowin;
using NowinSample;

namespace Microsoft.AspNetCore.Hosting
{
    public static class NowinWebHostBuilderExtensions
    {
        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder)
        {
            return builder.ConfigureServices(services =>
            {
                services.AddSingleton<IServer, NowinServer>();
            });
        }

        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder, Action<ServerBuilder> configure)
        {
            builder.ConfigureServices(services =>
            {
                services.Configure(configure);
            });
            return builder.UseNowin();
        }
    }
}
```

<span data-ttu-id="96089-137">与此就地，所有，具有需要运行 ASP.NET 应用程序使用此自定义服务器调用扩展*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="96089-137">With this in place, all that's required to run an ASP.NET application using this custom server to call the extension in *Program.cs*:</span></span>

```csharp

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Hosting;

namespace NowinSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseNowin()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
}

```

<span data-ttu-id="96089-138">了解有关 ASP.NET[服务器](servers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="96089-138">Learn more about ASP.NET [Servers](servers/index.md).</span></span>

## <a name="run-aspnet-core-on-an-owin-based-server-and-use-its-websockets-support"></a><span data-ttu-id="96089-139">基于 OWIN 的服务器上运行 ASP.NET 核心，并使用其 Websocket 支持</span><span class="sxs-lookup"><span data-stu-id="96089-139">Run ASP.NET Core on an OWIN-based server and use its WebSockets support</span></span>

<span data-ttu-id="96089-140">如何基于 OWIN 的服务器的功能的另一个示例可以利用 ASP.NET 核心是对等 Websocket 功能的访问。</span><span class="sxs-lookup"><span data-stu-id="96089-140">Another example of how OWIN-based servers' features can be leveraged by ASP.NET Core is access to features like WebSockets.</span></span> <span data-ttu-id="96089-141">在前面的示例使用的.NET OWIN web 服务器具有用于 Web 套接字内置的这可以利用 ASP.NET Core 应用程序支持。</span><span class="sxs-lookup"><span data-stu-id="96089-141">The .NET OWIN web server used in the previous example has support for Web Sockets built in, which can be leveraged by an ASP.NET Core application.</span></span> <span data-ttu-id="96089-142">下面的示例演示一个简单的 web 应用，支持 Web 套接字回显 Websocket 通过向服务器发送的所有内容。</span><span class="sxs-lookup"><span data-stu-id="96089-142">The example below shows a simple web app that supports Web Sockets and echoes back everything sent to the server through WebSockets.</span></span>

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            if (context.WebSockets.IsWebSocketRequest)
            {
                WebSocket webSocket = await context.WebSockets.AcceptWebSocketAsync();
                await EchoWebSocket(webSocket);
            }
            else
            {
                await next();
            }
        });

        app.Run(context =>
        {
            return context.Response.WriteAsync("Hello World");
        });
    }

    private async Task EchoWebSocket(WebSocket webSocket)
    {
        byte[] buffer = new byte[1024];
        WebSocketReceiveResult received = await webSocket.ReceiveAsync(
            new ArraySegment<byte>(buffer), CancellationToken.None);

        while (!webSocket.CloseStatus.HasValue)
        {
            // Echo anything we receive
            await webSocket.SendAsync(new ArraySegment<byte>(buffer, 0, received.Count), 
                received.MessageType, received.EndOfMessage, CancellationToken.None);

            received = await webSocket.ReceiveAsync(new ArraySegment<byte>(buffer), 
                CancellationToken.None);
        }

        await webSocket.CloseAsync(webSocket.CloseStatus.Value, 
            webSocket.CloseStatusDescription, CancellationToken.None);
    }
}
```

<span data-ttu-id="96089-143">这[示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)使用相同配置`NowinServer`与之前的唯一的区别是在应用程序中的配置方式其`Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="96089-143">This [sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) is configured using the same `NowinServer` as the previous one - the only difference is in how the application is configured in its `Configure` method.</span></span> <span data-ttu-id="96089-144">测试使用[简单 websocket 客户端](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en)演示应用程序：</span><span class="sxs-lookup"><span data-stu-id="96089-144">A test using [a simple websocket client](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en) demonstrates  the application:</span></span>

![Web 套接字测试客户端](owin/_static/websocket-test.png)

## <a name="owin-environment"></a><span data-ttu-id="96089-146">OWIN 环境</span><span class="sxs-lookup"><span data-stu-id="96089-146">OWIN environment</span></span>

<span data-ttu-id="96089-147">你可以构造 OWIN 环境使用`HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="96089-147">You can construct a OWIN environment using the `HttpContext`.</span></span>

```csharp

   var environment = new OwinEnvironment(HttpContext);
   var features = new OwinFeatureCollection(environment);
   ```

## <a name="owin-keys"></a><span data-ttu-id="96089-148">OWIN 键</span><span class="sxs-lookup"><span data-stu-id="96089-148">OWIN keys</span></span>

<span data-ttu-id="96089-149">取决于 OWIN`IDictionary<string,object>`对象进行通信信息的整个 HTTP 请求/响应交换。</span><span class="sxs-lookup"><span data-stu-id="96089-149">OWIN depends on an `IDictionary<string,object>` object to communicate information throughout an HTTP Request/Response exchange.</span></span> <span data-ttu-id="96089-150">ASP.NET 核心实现下面列出的密钥。</span><span class="sxs-lookup"><span data-stu-id="96089-150">ASP.NET Core implements the keys listed below.</span></span> <span data-ttu-id="96089-151">请参阅[主规范、 扩展](http://owin.org/#spec)，和[OWIN 键指导原则和常见的键](http://owin.org/spec/spec/CommonKeys.html)。</span><span class="sxs-lookup"><span data-stu-id="96089-151">See the [primary specification, extensions](http://owin.org/#spec), and [OWIN Key Guidelines and Common Keys](http://owin.org/spec/spec/CommonKeys.html).</span></span>

### <a name="request-data-owin-v100"></a><span data-ttu-id="96089-152">请求的数据 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="96089-152">Request Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="96089-153">键</span><span class="sxs-lookup"><span data-stu-id="96089-153">Key</span></span>               | <span data-ttu-id="96089-154">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-154">Value (type)</span></span> | <span data-ttu-id="96089-155">描述</span><span class="sxs-lookup"><span data-stu-id="96089-155">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-156">owin.RequestScheme</span><span class="sxs-lookup"><span data-stu-id="96089-156">owin.RequestScheme</span></span> | `String` |  |
| <span data-ttu-id="96089-157">owin.RequestMethod</span><span class="sxs-lookup"><span data-stu-id="96089-157">owin.RequestMethod</span></span>  | `String` | |    
| <span data-ttu-id="96089-158">owin.RequestPathBase</span><span class="sxs-lookup"><span data-stu-id="96089-158">owin.RequestPathBase</span></span>  | `String` | |    
| <span data-ttu-id="96089-159">owin.RequestPath</span><span class="sxs-lookup"><span data-stu-id="96089-159">owin.RequestPath</span></span> | `String` | |     
| <span data-ttu-id="96089-160">owin.RequestQueryString</span><span class="sxs-lookup"><span data-stu-id="96089-160">owin.RequestQueryString</span></span>  | `String` | |    
| <span data-ttu-id="96089-161">owin.RequestProtocol</span><span class="sxs-lookup"><span data-stu-id="96089-161">owin.RequestProtocol</span></span>  | `String` | |    
| <span data-ttu-id="96089-162">owin.RequestHeaders</span><span class="sxs-lookup"><span data-stu-id="96089-162">owin.RequestHeaders</span></span> | `IDictionary<string,string[]>`  | |
| <span data-ttu-id="96089-163">owin.RequestBody</span><span class="sxs-lookup"><span data-stu-id="96089-163">owin.RequestBody</span></span> | `Stream`  | |

### <a name="request-data-owin-v110"></a><span data-ttu-id="96089-164">请求的数据 (OWIN v1.1.0)</span><span class="sxs-lookup"><span data-stu-id="96089-164">Request Data (OWIN v1.1.0)</span></span>

| <span data-ttu-id="96089-165">键</span><span class="sxs-lookup"><span data-stu-id="96089-165">Key</span></span>               | <span data-ttu-id="96089-166">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-166">Value (type)</span></span> | <span data-ttu-id="96089-167">描述</span><span class="sxs-lookup"><span data-stu-id="96089-167">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-168">owin.RequestId</span><span class="sxs-lookup"><span data-stu-id="96089-168">owin.RequestId</span></span> | `String` | <span data-ttu-id="96089-169">Optional</span><span class="sxs-lookup"><span data-stu-id="96089-169">Optional</span></span> |

### <a name="response-data-owin-v100"></a><span data-ttu-id="96089-170">响应数据 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="96089-170">Response Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="96089-171">键</span><span class="sxs-lookup"><span data-stu-id="96089-171">Key</span></span>               | <span data-ttu-id="96089-172">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-172">Value (type)</span></span> | <span data-ttu-id="96089-173">描述</span><span class="sxs-lookup"><span data-stu-id="96089-173">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-174">owin.ResponseStatusCode</span><span class="sxs-lookup"><span data-stu-id="96089-174">owin.ResponseStatusCode</span></span> | `int` | <span data-ttu-id="96089-175">Optional</span><span class="sxs-lookup"><span data-stu-id="96089-175">Optional</span></span> |
| <span data-ttu-id="96089-176">owin.ResponseReasonPhrase</span><span class="sxs-lookup"><span data-stu-id="96089-176">owin.ResponseReasonPhrase</span></span> | `String` | <span data-ttu-id="96089-177">Optional</span><span class="sxs-lookup"><span data-stu-id="96089-177">Optional</span></span> |
| <span data-ttu-id="96089-178">owin.ResponseHeaders</span><span class="sxs-lookup"><span data-stu-id="96089-178">owin.ResponseHeaders</span></span> | `IDictionary<string,string[]>`  | |
| <span data-ttu-id="96089-179">owin.ResponseBody</span><span class="sxs-lookup"><span data-stu-id="96089-179">owin.ResponseBody</span></span> | `Stream`  | |


### <a name="other-data-owin-v100"></a><span data-ttu-id="96089-180">其他数据 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="96089-180">Other Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="96089-181">键</span><span class="sxs-lookup"><span data-stu-id="96089-181">Key</span></span>               | <span data-ttu-id="96089-182">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-182">Value (type)</span></span> | <span data-ttu-id="96089-183">描述</span><span class="sxs-lookup"><span data-stu-id="96089-183">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-184">owin.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="96089-184">owin.CallCancelled</span></span> | `CancellationToken` |  |
| <span data-ttu-id="96089-185">owin.Version</span><span class="sxs-lookup"><span data-stu-id="96089-185">owin.Version</span></span>  | `String` | |   


### <a name="common-keys"></a><span data-ttu-id="96089-186">常见的键</span><span class="sxs-lookup"><span data-stu-id="96089-186">Common Keys</span></span>

| <span data-ttu-id="96089-187">键</span><span class="sxs-lookup"><span data-stu-id="96089-187">Key</span></span>               | <span data-ttu-id="96089-188">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-188">Value (type)</span></span> | <span data-ttu-id="96089-189">描述</span><span class="sxs-lookup"><span data-stu-id="96089-189">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-190">ssl.ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="96089-190">ssl.ClientCertificate</span></span> | `X509Certificate` |  |
| <span data-ttu-id="96089-191">ssl.LoadClientCertAsync</span><span class="sxs-lookup"><span data-stu-id="96089-191">ssl.LoadClientCertAsync</span></span>  | `Func<Task>` | |    
| <span data-ttu-id="96089-192">server.RemoteIpAddress</span><span class="sxs-lookup"><span data-stu-id="96089-192">server.RemoteIpAddress</span></span>  | `String` | |    
| <span data-ttu-id="96089-193">server.RemotePort</span><span class="sxs-lookup"><span data-stu-id="96089-193">server.RemotePort</span></span> | `String` | |     
| <span data-ttu-id="96089-194">server.LocalIpAddress</span><span class="sxs-lookup"><span data-stu-id="96089-194">server.LocalIpAddress</span></span>  | `String` | |    
| <span data-ttu-id="96089-195">server.LocalPort</span><span class="sxs-lookup"><span data-stu-id="96089-195">server.LocalPort</span></span>  | `String` | |    
| <span data-ttu-id="96089-196">server.IsLocal</span><span class="sxs-lookup"><span data-stu-id="96089-196">server.IsLocal</span></span>  | `bool` | |    
| <span data-ttu-id="96089-197">server.OnSendingHeaders</span><span class="sxs-lookup"><span data-stu-id="96089-197">server.OnSendingHeaders</span></span>  | `Action<Action<object>,object>` | |


### <a name="sendfiles-v030"></a><span data-ttu-id="96089-198">SendFiles v0.3.0</span><span class="sxs-lookup"><span data-stu-id="96089-198">SendFiles v0.3.0</span></span>

| <span data-ttu-id="96089-199">键</span><span class="sxs-lookup"><span data-stu-id="96089-199">Key</span></span>               | <span data-ttu-id="96089-200">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-200">Value (type)</span></span> | <span data-ttu-id="96089-201">描述</span><span class="sxs-lookup"><span data-stu-id="96089-201">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-202">sendfile.SendAsync</span><span class="sxs-lookup"><span data-stu-id="96089-202">sendfile.SendAsync</span></span> | <span data-ttu-id="96089-203">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-203">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> | <span data-ttu-id="96089-204">每个请求</span><span class="sxs-lookup"><span data-stu-id="96089-204">Per Request</span></span> |


### <a name="opaque-v030"></a><span data-ttu-id="96089-205">不透明 v0.3.0</span><span class="sxs-lookup"><span data-stu-id="96089-205">Opaque v0.3.0</span></span>

| <span data-ttu-id="96089-206">键</span><span class="sxs-lookup"><span data-stu-id="96089-206">Key</span></span>               | <span data-ttu-id="96089-207">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-207">Value (type)</span></span> | <span data-ttu-id="96089-208">描述</span><span class="sxs-lookup"><span data-stu-id="96089-208">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-209">opaque.Version</span><span class="sxs-lookup"><span data-stu-id="96089-209">opaque.Version</span></span> | `String` |  |
| <span data-ttu-id="96089-210">opaque.Upgrade</span><span class="sxs-lookup"><span data-stu-id="96089-210">opaque.Upgrade</span></span> | `OpaqueUpgrade` | <span data-ttu-id="96089-211">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-211">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> |
| <span data-ttu-id="96089-212">opaque.Stream</span><span class="sxs-lookup"><span data-stu-id="96089-212">opaque.Stream</span></span> | `Stream` |  |
| <span data-ttu-id="96089-213">opaque.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="96089-213">opaque.CallCancelled</span></span> | `CancellationToken` |  |


### <a name="websocket-v030"></a><span data-ttu-id="96089-214">WebSocket v0.3.0</span><span class="sxs-lookup"><span data-stu-id="96089-214">WebSocket v0.3.0</span></span>

| <span data-ttu-id="96089-215">键</span><span class="sxs-lookup"><span data-stu-id="96089-215">Key</span></span>               | <span data-ttu-id="96089-216">值 （类型）</span><span class="sxs-lookup"><span data-stu-id="96089-216">Value (type)</span></span> | <span data-ttu-id="96089-217">描述</span><span class="sxs-lookup"><span data-stu-id="96089-217">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="96089-218">websocket.Version</span><span class="sxs-lookup"><span data-stu-id="96089-218">websocket.Version</span></span> | `String` |  |
| <span data-ttu-id="96089-219">websocket.Accept</span><span class="sxs-lookup"><span data-stu-id="96089-219">websocket.Accept</span></span> | `WebSocketAccept` | <span data-ttu-id="96089-220">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-220">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> |
| <span data-ttu-id="96089-221">websocket.AcceptAlt</span><span class="sxs-lookup"><span data-stu-id="96089-221">websocket.AcceptAlt</span></span> |  | <span data-ttu-id="96089-222">非规范</span><span class="sxs-lookup"><span data-stu-id="96089-222">Non-spec</span></span> |
| <span data-ttu-id="96089-223">websocket.SubProtocol</span><span class="sxs-lookup"><span data-stu-id="96089-223">websocket.SubProtocol</span></span> | `String` | <span data-ttu-id="96089-224">请参阅[RFC6455 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2)步骤 5.5</span><span class="sxs-lookup"><span data-stu-id="96089-224">See [RFC6455 Section 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2) Step 5.5</span></span> |
| <span data-ttu-id="96089-225">websocket.SendAsync</span><span class="sxs-lookup"><span data-stu-id="96089-225">websocket.SendAsync</span></span> | `WebSocketSendAsync` | <span data-ttu-id="96089-226">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-226">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="96089-227">websocket.ReceiveAsync</span><span class="sxs-lookup"><span data-stu-id="96089-227">websocket.ReceiveAsync</span></span> | `WebSocketReceiveAsync` | <span data-ttu-id="96089-228">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-228">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="96089-229">websocket.CloseAsync</span><span class="sxs-lookup"><span data-stu-id="96089-229">websocket.CloseAsync</span></span> | `WebSocketCloseAsync` | <span data-ttu-id="96089-230">请参阅[委托签名](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="96089-230">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="96089-231">websocket.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="96089-231">websocket.CallCancelled</span></span> | `CancellationToken` |  |
| <span data-ttu-id="96089-232">websocket.ClientCloseStatus</span><span class="sxs-lookup"><span data-stu-id="96089-232">websocket.ClientCloseStatus</span></span> | `int` | <span data-ttu-id="96089-233">Optional</span><span class="sxs-lookup"><span data-stu-id="96089-233">Optional</span></span> |
| <span data-ttu-id="96089-234">websocket.ClientCloseDescription</span><span class="sxs-lookup"><span data-stu-id="96089-234">websocket.ClientCloseDescription</span></span> | `String` | <span data-ttu-id="96089-235">Optional</span><span class="sxs-lookup"><span data-stu-id="96089-235">Optional</span></span> |


## <a name="additional-resources"></a><span data-ttu-id="96089-236">其他资源</span><span class="sxs-lookup"><span data-stu-id="96089-236">Additional Resources</span></span>

* [<span data-ttu-id="96089-237">中间件</span><span class="sxs-lookup"><span data-stu-id="96089-237">Middleware</span></span>](middleware.md)

* [<span data-ttu-id="96089-238">服务器</span><span class="sxs-lookup"><span data-stu-id="96089-238">Servers</span></span>](servers/index.md)
