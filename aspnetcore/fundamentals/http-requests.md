---
title: 启动 HTTP 请求
author: stevejgordon
description: 了解如何将 IHttpClientFactory 接口用于管理 ASP.NET Core 中的逻辑 HttpClient 实例。
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 08/07/2018
uid: fundamentals/http-requests
ms.openlocfilehash: 693e9d64f47704400cbfa9e46b866f39278d82f6
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207636"
---
# <a name="initiate-http-requests"></a><span data-ttu-id="7d7bc-103">启动 HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="7d7bc-103">Initiate HTTP requests</span></span>

<span data-ttu-id="7d7bc-104">作者：[Glenn Condron](https://github.com/glennc)[Ryan Nowak](https://github.com/rynowak) 和 [Steve Gordon](https://github.com/stevejgordon)</span><span class="sxs-lookup"><span data-stu-id="7d7bc-104">By [Glenn Condron](https://github.com/glennc), [Ryan Nowak](https://github.com/rynowak), and [Steve Gordon](https://github.com/stevejgordon)</span></span>

<span data-ttu-id="7d7bc-105">可以注册 [IHttpClientFactory](/dotnet/api/system.net.http.ihttpclientfactory) 并将其用于配置和创建应用中的 [HttpClient](/dotnet/api/system.net.http.httpclient) 实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-105">An [IHttpClientFactory](/dotnet/api/system.net.http.ihttpclientfactory) can be registered and used to configure and create [HttpClient](/dotnet/api/system.net.http.httpclient) instances in an app.</span></span> <span data-ttu-id="7d7bc-106">这能带来以下好处：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-106">It offers the following benefits:</span></span>

* <span data-ttu-id="7d7bc-107">提供一个中心位置，用于命名和配置逻辑 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-107">Provides a central location for naming and configuring logical `HttpClient` instances.</span></span> <span data-ttu-id="7d7bc-108">例如，可以注册 github 客户端，并将它配置为访问 GitHub。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-108">For example, a *github* client can be registered and configured to access GitHub.</span></span> <span data-ttu-id="7d7bc-109">可以注册一个默认客户端用于其他用途。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-109">A default client can be registered for other purposes.</span></span>
* <span data-ttu-id="7d7bc-110">通过委托 `HttpClient` 中的处理程序整理出站中间件的概念，并提供适用于基于 Polly 的中间件的扩展来利用概念。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-110">Codifies the concept of outgoing middleware via delegating handlers in `HttpClient` and provides extensions for Polly-based middleware to take advantage of that.</span></span>
* <span data-ttu-id="7d7bc-111">管理基础 `HttpClientMessageHandler` 实例的池和生存期，避免在手动管理 `HttpClient` 生存期时出现常见的 DNS 问题。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-111">Manages the pooling and lifetime of underlying `HttpClientMessageHandler` instances to avoid common DNS problems that occur when manually managing `HttpClient` lifetimes.</span></span>
* <span data-ttu-id="7d7bc-112">（通过 `ILogger`）添加可配置的记录体验，以处理工厂创建的客户端发送的所有请求。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-112">Adds a configurable logging experience (via `ILogger`) for all requests sent through clients created by the factory.</span></span>

<span data-ttu-id="7d7bc-113">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/http-requests/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="7d7bc-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/http-requests/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7bc-114">系统必备</span><span class="sxs-lookup"><span data-stu-id="7d7bc-114">Prerequisites</span></span>

<span data-ttu-id="7d7bc-115">面向.NET Framework 的项目要求安装 [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-115">Projects targeting .NET Framework require installation of the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) NuGet package.</span></span> <span data-ttu-id="7d7bc-116">面向 .NET Core 且引用 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)的项目已经包括 `Microsoft.Extensions.Http` 包。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-116">Projects that target .NET Core and reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) already include the `Microsoft.Extensions.Http` package.</span></span>

## <a name="consumption-patterns"></a><span data-ttu-id="7d7bc-117">消耗模式</span><span class="sxs-lookup"><span data-stu-id="7d7bc-117">Consumption patterns</span></span>

<span data-ttu-id="7d7bc-118">在应用中可以通过以下多种方式使用 `IHttpClientFactory`：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-118">There are several ways `IHttpClientFactory` can be used in an app:</span></span>

* [<span data-ttu-id="7d7bc-119">基本用法</span><span class="sxs-lookup"><span data-stu-id="7d7bc-119">Basic usage</span></span>](#basic-usage)
* [<span data-ttu-id="7d7bc-120">命名客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-120">Named clients</span></span>](#named-clients)
* [<span data-ttu-id="7d7bc-121">类型化客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-121">Typed clients</span></span>](#typed-clients)
* [<span data-ttu-id="7d7bc-122">生成的客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-122">Generated clients</span></span>](#generated-clients)

<span data-ttu-id="7d7bc-123">它们之间不存在严格的优先级。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-123">None of them are strictly superior to another.</span></span> <span data-ttu-id="7d7bc-124">最佳方法取决于应用的约束条件。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-124">The best approach depends upon the app's constraints.</span></span>

### <a name="basic-usage"></a><span data-ttu-id="7d7bc-125">基本用法</span><span class="sxs-lookup"><span data-stu-id="7d7bc-125">Basic usage</span></span>

<span data-ttu-id="7d7bc-126">在 `Startup.ConfigureServices` 方法中，通过在 `IServiceCollection` 上调用 `AddHttpClient` 扩展方法可以注册 `IHttpClientFactory`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-126">The `IHttpClientFactory` can be registered by calling the `AddHttpClient` extension method on the `IServiceCollection`, inside the `Startup.ConfigureServices` method.</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet1)]

<span data-ttu-id="7d7bc-127">注册后，在可以使用[依赖关系注入](xref:fundamentals/dependency-injection) (DI) 注入服务的任何位置，代码都能接受 `IHttpClientFactory`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-127">Once registered, code can accept an `IHttpClientFactory` anywhere services can be injected with [dependency injection](xref:fundamentals/dependency-injection) (DI).</span></span> <span data-ttu-id="7d7bc-128">`IHttpClientFactory` 可以用于创建 `HttpClient` 实例：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-128">The `IHttpClientFactory` can be used to create a `HttpClient` instance:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/BasicUsage.cshtml.cs?name=snippet1&highlight=9-12,21)]

<span data-ttu-id="7d7bc-129">以这种方式使用 `IHttpClientFactory` 非常适合重构现有应用。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-129">Using `IHttpClientFactory` in this fashion is a great way to refactor an existing app.</span></span> <span data-ttu-id="7d7bc-130">这不会影响 `HttpClient` 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-130">It has no impact on the way `HttpClient` is used.</span></span> <span data-ttu-id="7d7bc-131">在当前创建 `HttpClient` 实例的位置上，通过调用 [CreateClient](/dotnet/api/system.net.http.ihttpclientfactory.createclient) 替换出现的这些实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-131">In places where `HttpClient` instances are currently created, replace those occurrences with a call to [CreateClient](/dotnet/api/system.net.http.ihttpclientfactory.createclient).</span></span>

### <a name="named-clients"></a><span data-ttu-id="7d7bc-132">命名客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-132">Named clients</span></span>

<span data-ttu-id="7d7bc-133">如果应用需要有许多不同的 `HttpClient` 用法（每种用法的配置都不同），可以视情况使用命名客户端。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-133">If an app requires many distinct uses of `HttpClient`, each with a different configuration, an option is to use **named clients**.</span></span> <span data-ttu-id="7d7bc-134">可以在 `HttpClient` 中注册时指定命名 `Startup.ConfigureServices` 的配置。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-134">Configuration for a named `HttpClient` can be specified during registration in `Startup.ConfigureServices`.</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet2)]

<span data-ttu-id="7d7bc-135">上面的代码调用 `AddHttpClient`，同时提供名称“github”。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-135">In the preceding code, `AddHttpClient` is called, providing the name *github*.</span></span> <span data-ttu-id="7d7bc-136">此客户端应用了一些默认配置，也就是需要基址和两个标头来使用 GitHub API。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-136">This client has some default configuration applied&mdash;namely the base address and two headers required to work with the GitHub API.</span></span>

<span data-ttu-id="7d7bc-137">每次调用 `CreateClient` 时，都会创建 `HttpClient` 的新实例，并调用配置操作。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-137">Each time `CreateClient` is called, a new instance of `HttpClient` is created and the configuration action is called.</span></span>

<span data-ttu-id="7d7bc-138">要使用命名客户端，可将字符串参数传递到 `CreateClient`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-138">To consume a named client, a string parameter can be passed to `CreateClient`.</span></span> <span data-ttu-id="7d7bc-139">指定要创建的客户端的名称：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-139">Specify the name of the client to be created:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/NamedClient.cshtml.cs?name=snippet1&highlight=21)]

<span data-ttu-id="7d7bc-140">在上述代码中，请求不需要指定主机名。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-140">In the preceding code, the request doesn't need to specify a hostname.</span></span> <span data-ttu-id="7d7bc-141">可以仅传递路径，因为采用了为客户端配置的基址。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-141">It can pass just the path, since the base address configured for the client is used.</span></span>

### <a name="typed-clients"></a><span data-ttu-id="7d7bc-142">类型化客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-142">Typed clients</span></span>

<span data-ttu-id="7d7bc-143">类型化客户端提供与命名客户端一样的功能，不需要将字符串用作密钥。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-143">Typed clients provide the same capabilities as named clients without the need to use strings as keys.</span></span> <span data-ttu-id="7d7bc-144">类型化客户端方法在使用客户端时提供 IntelliSense 和编译器帮助。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-144">The typed client approach provides IntelliSense and compiler help when consuming clients.</span></span> <span data-ttu-id="7d7bc-145">它们提供单个地址来配置特定 `HttpClient` 并与其进行交互。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-145">They provide a single location to configure and interact with a particular `HttpClient`.</span></span> <span data-ttu-id="7d7bc-146">例如，单个类型化客户端可能用于单个后端终结点，并封装此终结点的所有处理逻辑。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-146">For example, a single typed client might be used for a single backend endpoint and encapsulate all logic dealing with that endpoint.</span></span> <span data-ttu-id="7d7bc-147">另一个优势是它们使用 DI 且可以被注入到应用中需要的位置。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-147">Another advantage is that they work with DI and can be injected where required in your app.</span></span>

<span data-ttu-id="7d7bc-148">类型化客户端在构造函数中接收 `HttpClient` 参数：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-148">A typed client accepts a `HttpClient` parameter in its constructor:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/GitHub/GitHubService.cs?name=snippet1&highlight=5)]

<span data-ttu-id="7d7bc-149">在上述代码中，配置转移到了类型化客户端中。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-149">In the preceding code, the configuration is moved into the typed client.</span></span> <span data-ttu-id="7d7bc-150">`HttpClient` 对象公开为公共属性。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-150">The `HttpClient` object is exposed as a public property.</span></span> <span data-ttu-id="7d7bc-151">可以定义公开 `HttpClient` 功能的特定于 API 的方法。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-151">It's possible to define API-specific methods that expose `HttpClient` functionality.</span></span> <span data-ttu-id="7d7bc-152">`GetAspNetDocsIssues` 方法从 GitHub 存储库封装查询和分析最新待解决问题所需的代码。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-152">The `GetAspNetDocsIssues` method encapsulates the code needed to query for and parse out the latest open issues from a GitHub repository.</span></span>

<span data-ttu-id="7d7bc-153">要注册类型化客户端，可在 `Startup.ConfigureServices` 中使用通用的 `AddHttpClient` 扩展方法，指定类型化客户端类：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-153">To register a typed client, the generic `AddHttpClient` extension method can be used within `Startup.ConfigureServices`, specifying the typed client class:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet3)]

<span data-ttu-id="7d7bc-154">使用 DI 将类型客户端注册为暂时客户端。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-154">The typed client is registered as transient with DI.</span></span> <span data-ttu-id="7d7bc-155">可以直接插入或使用类型化客户端：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-155">The typed client can be injected and consumed directly:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/TypedClient.cshtml.cs?name=snippet1&highlight=11-14,20)]

<span data-ttu-id="7d7bc-156">根据你的喜好，可以在 `Startup.ConfigureServices` 中注册时指定类型化客户端的配置，而不是在类型化客户端的构造函数中指定：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-156">If preferred, the configuration for a typed client can be specified during registration in `Startup.ConfigureServices`, rather than in the typed client's constructor:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet4)]

<span data-ttu-id="7d7bc-157">可以将 `HttpClient` 完全封装在类型化客户端中。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-157">It's possible to entirely encapsulate the `HttpClient` within a typed client.</span></span> <span data-ttu-id="7d7bc-158">不是将它公开为属性，而是可以提供公共方法，用于在内部调用 `HttpClient`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-158">Rather than exposing it as a property, public methods can be provided which call the `HttpClient` instance internally.</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/GitHub/RepoService.cs?name=snippet1&highlight=4)]

<span data-ttu-id="7d7bc-159">在上述代码中，`HttpClient` 存储未私有字段。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-159">In the preceding code, the `HttpClient` is stored as a private field.</span></span> <span data-ttu-id="7d7bc-160">进行外部调用的所有访问都经由 `GetRepos` 方法。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-160">All access to make external calls goes through the `GetRepos` method.</span></span>

### <a name="generated-clients"></a><span data-ttu-id="7d7bc-161">生成的客户端</span><span class="sxs-lookup"><span data-stu-id="7d7bc-161">Generated clients</span></span>

<span data-ttu-id="7d7bc-162">`IHttpClientFactory` 可结合其他第三方库（例如 [Refit](https://github.com/paulcbetts/refit)）使用。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-162">`IHttpClientFactory` can be used in combination with other third-party libraries such as [Refit](https://github.com/paulcbetts/refit).</span></span> <span data-ttu-id="7d7bc-163">Refit 是.NET 的 REST 库。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-163">Refit is a REST library for .NET.</span></span> <span data-ttu-id="7d7bc-164">它将 REST API 转换为实时接口。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-164">It converts REST APIs into live interfaces.</span></span> <span data-ttu-id="7d7bc-165">`RestService` 动态生成该接口的实现，使用 `HttpClient` 进行外部 HTTP 调用。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-165">An implementation of the interface is generated dynamically by the `RestService`, using `HttpClient` to make the external HTTP calls.</span></span>

<span data-ttu-id="7d7bc-166">定义了接口和答复来代表外部 API 及其响应：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-166">An interface and a reply are defined to represent the external API and its response:</span></span>

```csharp
public interface IHelloClient
{
    [Get("/helloworld")]
    Task<Reply> GetMessageAsync();
}

public class Reply
{
    public string Message { get; set; }
}
```

<span data-ttu-id="7d7bc-167">可以添加类型化客户端，使用 Refit 生成实现：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-167">A typed client can be added, using Refit to generate the implementation:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHttpClient("hello", c =>
    {
        c.BaseAddress = new Uri("http://localhost:5000");
    })
    .AddTypedClient(c => Refit.RestService.For<IHelloClient>(c));

    services.AddMvc();
}
```

<span data-ttu-id="7d7bc-168">可以在必要时使用定义的接口，以及由 DI 和 Refit 提供的实现：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-168">The defined interface can be consumed where necessary, with the implementation provided by DI and Refit:</span></span>

```csharp
[ApiController]
public class ValuesController : ControllerBase
{
    private readonly IHelloClient _client;

    public ValuesController(IHelloClient client)
    {
        _client = client;
    }

    [HttpGet("/")]
    public async Task<ActionResult<Reply>> Index()
    {
        return await _client.GetMessageAsync();
    }
}
```

## <a name="outgoing-request-middleware"></a><span data-ttu-id="7d7bc-169">出站请求中间件</span><span class="sxs-lookup"><span data-stu-id="7d7bc-169">Outgoing request middleware</span></span>

<span data-ttu-id="7d7bc-170">`HttpClient` 已经具有委托处理程序的概念，这些委托处理程序可以链接在一起，处理出站 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-170">`HttpClient` already has the concept of delegating handlers that can be linked together for outgoing HTTP requests.</span></span> <span data-ttu-id="7d7bc-171">`IHttpClientFactory` 可以轻松定义处理程序并应用于每个命名客户端。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-171">The `IHttpClientFactory` makes it easy to define the handlers to apply for each named client.</span></span> <span data-ttu-id="7d7bc-172">它支持注册和链接多个处理程序，以生成出站请求中间件管道。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-172">It supports registration and chaining of multiple handlers to build an outgoing request middleware pipeline.</span></span> <span data-ttu-id="7d7bc-173">每个处理程序都可以在出站请求前后执行工作。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-173">Each of these handlers is able to perform work before and after the outgoing request.</span></span> <span data-ttu-id="7d7bc-174">此模式类似于 ASP.NET Core 中的入站中间件管道。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-174">This pattern is similar to the inbound middleware pipeline in ASP.NET Core.</span></span> <span data-ttu-id="7d7bc-175">此模式提供了一种用于管理围绕 HTTP 请求的横切关注点的机制，包括缓存、错误处理、序列化以及日志记录。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-175">The pattern provides a mechanism to manage cross-cutting concerns around HTTP requests, including caching, error handling, serialization, and logging.</span></span>

<span data-ttu-id="7d7bc-176">要创建处理程序，请定义一个派生自 `DelegatingHandler` 的类。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-176">To create a handler, define a class deriving from `DelegatingHandler`.</span></span> <span data-ttu-id="7d7bc-177">重写 `SendAsync` 方法，在将请求传递至管道中的下一个处理程序之前执行代码：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-177">Override the `SendAsync` method to execute code before passing the request to the next handler in the pipeline:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Handlers/ValidateHeaderHandler.cs?name=snippet1)]

<span data-ttu-id="7d7bc-178">上述代码定义了基本处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-178">The preceding code defines a basic handler.</span></span> <span data-ttu-id="7d7bc-179">它检查请求中是否包含 `X-API-KEY` 头。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-179">It checks to see if an `X-API-KEY` header has been included on the request.</span></span> <span data-ttu-id="7d7bc-180">如果标头缺失，它可以避免 HTTP 调用，并返回合适的响应。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-180">If the header is missing, it can avoid the HTTP call and return a suitable response.</span></span>

<span data-ttu-id="7d7bc-181">在注册期间可将一个或多个标头添加到 `HttpClient` 的配置。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-181">During registration, one or more handlers can be added to the configuration for a `HttpClient`.</span></span> <span data-ttu-id="7d7bc-182">此任务通过 [IHttpClientBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.ihttpclientbuilder) 的扩展方法完成。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-182">This task is accomplished via extension methods on the [IHttpClientBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.ihttpclientbuilder).</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet5)]

<span data-ttu-id="7d7bc-183">在上述代码中通过 DI 注册了 `ValidateHeaderHandler`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-183">In the preceding code, the `ValidateHeaderHandler` is registered with DI.</span></span> <span data-ttu-id="7d7bc-184">处理程序必须在 DI 中注册为临时处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-184">The handler **must** be registered in DI as transient.</span></span> <span data-ttu-id="7d7bc-185">注册后，即可调用 [AddHttpMessageHandler](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.addhttpmessagehandler)，同时传入头类型。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-185">Once registered, [AddHttpMessageHandler](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.addhttpmessagehandler) can be called, passing in the type for the handler.</span></span>

<span data-ttu-id="7d7bc-186">可以按处理程序应该执行的顺序注册多个处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-186">Multiple handlers can be registered in the order that they should execute.</span></span> <span data-ttu-id="7d7bc-187">每个处理程序都会覆盖下一个处理程序，直到最终 `HttpClientHandler` 执行请求：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-187">Each handler wraps the next handler until the final `HttpClientHandler` executes the request:</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet6)]

## <a name="use-polly-based-handlers"></a><span data-ttu-id="7d7bc-188">使用基于 Polly 的处理程序</span><span class="sxs-lookup"><span data-stu-id="7d7bc-188">Use Polly-based handlers</span></span>

<span data-ttu-id="7d7bc-189">`IHttpClientFactory` 与一个名为 [Polly](https://github.com/App-vNext/Polly) 的热门第三方库集成。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-189">`IHttpClientFactory` integrates with a popular third-party library called [Polly](https://github.com/App-vNext/Polly).</span></span> <span data-ttu-id="7d7bc-190">Polly 是适用于 .NET 的全面恢复和临时故障处理库。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-190">Polly is a comprehensive resilience and transient fault-handling library for .NET.</span></span> <span data-ttu-id="7d7bc-191">开发人员通过它可以表达策略，例如以流畅且线程安全的方式处理重试、断路器、超时、Bulkhead 隔离和回退。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-191">It allows developers to express policies such as Retry, Circuit Breaker, Timeout, Bulkhead Isolation, and Fallback in a fluent and thread-safe manner.</span></span>

<span data-ttu-id="7d7bc-192">提供了扩展方法，以实现将 Polly 策略用于配置的 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-192">Extension methods are provided to enable the use of Polly policies with configured `HttpClient` instances.</span></span> <span data-ttu-id="7d7bc-193">[Microsoft.Extensions.Http.Polly](https://www.nuget.org/packages/Microsoft.Extensions.Http.Polly/) NuGet 包中提供 Polly 扩展。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-193">The Polly extensions are available in the [Microsoft.Extensions.Http.Polly](https://www.nuget.org/packages/Microsoft.Extensions.Http.Polly/) NuGet package.</span></span> <span data-ttu-id="7d7bc-194">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中不包括此包。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-194">This package isn't included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="7d7bc-195">若要使用扩展，项目中应该包括显式 `<PackageReference />`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-195">To use the extensions, an explicit `<PackageReference />` should be included in the project.</span></span>

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/HttpClientFactorySample.csproj?highlight=9)]

<span data-ttu-id="7d7bc-196">还原此包后，可以使用扩展方法来支持将基于 Polly 的处理程序添加至客户端。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-196">After restoring this package, extension methods are available to support adding Polly-based handlers to clients.</span></span>

### <a name="handle-transient-faults"></a><span data-ttu-id="7d7bc-197">处理临时故障</span><span class="sxs-lookup"><span data-stu-id="7d7bc-197">Handle transient faults</span></span>

<span data-ttu-id="7d7bc-198">大多数常见错误在暂时执行外部 HTTP 调用时发生。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-198">Most common faults occur when external HTTP calls are transient.</span></span> <span data-ttu-id="7d7bc-199">包含了一种简便的扩展方法，该方法名为 `AddTransientHttpErrorPolicy`，允许定义策略来处理临时故障。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-199">A convenient extension method called `AddTransientHttpErrorPolicy` is included which allows a policy to be defined to handle transient errors.</span></span> <span data-ttu-id="7d7bc-200">使用这种扩展方法配置的策略可以处理 `HttpRequestException`、HTTP 5xx 响应以及 HTTP 408 响应。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-200">Policies configured with this extension method handle `HttpRequestException`, HTTP 5xx responses, and HTTP 408 responses.</span></span>

<span data-ttu-id="7d7bc-201">`AddTransientHttpErrorPolicy` 扩展可在 `Startup.ConfigureServices` 内使用。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-201">The `AddTransientHttpErrorPolicy` extension can be used within `Startup.ConfigureServices`.</span></span> <span data-ttu-id="7d7bc-202">该扩展可以提供 `PolicyBuilder` 对象的访问权限，该对象配置为处理表示可能的临时故障的错误：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-202">The extension provides access to a `PolicyBuilder` object configured to handle errors representing a possible transient fault:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet7)]

<span data-ttu-id="7d7bc-203">上述代码中定义了 `WaitAndRetryAsync` 策略。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-203">In the preceding code, a `WaitAndRetryAsync` policy is defined.</span></span> <span data-ttu-id="7d7bc-204">请求失败后最多可以重试三次，每次尝试间隔 600 ms。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-204">Failed requests are retried up to three times with a delay of 600 ms between attempts.</span></span>

### <a name="dynamically-select-policies"></a><span data-ttu-id="7d7bc-205">动态选择策略</span><span class="sxs-lookup"><span data-stu-id="7d7bc-205">Dynamically select policies</span></span>

<span data-ttu-id="7d7bc-206">存在其他扩展方法，可以用于添加基于 Polly 的处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-206">Additional extension methods exist which can be used to add Polly-based handlers.</span></span> <span data-ttu-id="7d7bc-207">这类扩展的其中一个是 `AddPolicyHandler`，它具备多个重载。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-207">One such extension is `AddPolicyHandler`, which has multiple overloads.</span></span> <span data-ttu-id="7d7bc-208">一个重载允许在定义要应用的策略时检查该请求：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-208">One overload allows the request to be inspected when defining which policy to apply:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet8)]

<span data-ttu-id="7d7bc-209">在上述代码中，如果出站请求为 GET，则应用 10 秒超时。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-209">In the preceding code, if the outgoing request is a GET, a 10-second timeout is applied.</span></span> <span data-ttu-id="7d7bc-210">其他所有 HTTP 方法应用 30 秒超时。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-210">For any other HTTP method, a 30-second timeout is used.</span></span>

### <a name="add-multiple-polly-handlers"></a><span data-ttu-id="7d7bc-211">添加多个 Polly 处理程序</span><span class="sxs-lookup"><span data-stu-id="7d7bc-211">Add multiple Polly handlers</span></span>

<span data-ttu-id="7d7bc-212">嵌套 Polly 策略以增强功能是很常见的：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-212">It is common to nest Polly policies to provide enhanced functionality:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet9)]

<span data-ttu-id="7d7bc-213">在上述示例中，添加两个处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-213">In the preceding example, two handlers are added.</span></span> <span data-ttu-id="7d7bc-214">第一个使用 `AddTransientHttpErrorPolicy` 扩展添加重试策略。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-214">The first uses the `AddTransientHttpErrorPolicy` extension to add a retry policy.</span></span> <span data-ttu-id="7d7bc-215">若请求失败，最多可重试三次。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-215">Failed requests are retried up to three times.</span></span> <span data-ttu-id="7d7bc-216">第一个调用 `AddTransientHttpErrorPolicy` 添加断路器策略。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-216">The second call to `AddTransientHttpErrorPolicy` adds a circuit breaker policy.</span></span> <span data-ttu-id="7d7bc-217">如果尝试连续失败了五次，则会阻止后续外部请求 30 秒。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-217">Further external requests are blocked for 30 seconds if five failed attempts occur sequentially.</span></span> <span data-ttu-id="7d7bc-218">断路器策略处于监控状态。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-218">Circuit breaker policies are stateful.</span></span> <span data-ttu-id="7d7bc-219">通过此客户端进行的所有调用都共享同样的线路状态。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-219">All calls through this client share the same circuit state.</span></span>

### <a name="add-policies-from-the-polly-registry"></a><span data-ttu-id="7d7bc-220">从 Polly 注册表添加策略</span><span class="sxs-lookup"><span data-stu-id="7d7bc-220">Add policies from the Polly registry</span></span>

<span data-ttu-id="7d7bc-221">管理常用策略的一种方法是一次性定义它们并使用 `PolicyRegistry` 注册它们。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-221">An approach to managing regularly used policies is to define them once and register them with a `PolicyRegistry`.</span></span> <span data-ttu-id="7d7bc-222">提供了一种扩展方法，可以使用注册表中的策略添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-222">An extension method is provided which allows a handler to be added using a policy from the registry:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet10)]

<span data-ttu-id="7d7bc-223">在上面的代码中，两个策略在 `PolicyRegistry` 添加到 `ServiceCollection` 中时进行注册。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-223">In the preceding code, two policies are registered when the `PolicyRegistry` is added to the `ServiceCollection`.</span></span> <span data-ttu-id="7d7bc-224">若要使用注册表中的策略，请使用 `AddPolicyHandlerFromRegistry` 方法，同时传递要应用的策略的名称。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-224">To use a policy from the registry, the `AddPolicyHandlerFromRegistry` method is used, passing the name of the policy to apply.</span></span>

<span data-ttu-id="7d7bc-225">要进一步了解 `IHttpClientFactory` 和 Polly 集成，请参考 [Polly Wiki](https://github.com/App-vNext/Polly/wiki/Polly-and-HttpClientFactory)。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-225">Further information about `IHttpClientFactory` and Polly integrations can be found on the [Polly wiki](https://github.com/App-vNext/Polly/wiki/Polly-and-HttpClientFactory).</span></span>

## <a name="httpclient-and-lifetime-management"></a><span data-ttu-id="7d7bc-226">HttpClient 和生存期管理</span><span class="sxs-lookup"><span data-stu-id="7d7bc-226">HttpClient and lifetime management</span></span>

<span data-ttu-id="7d7bc-227">每次对 `IHttpClientFactory` 调用 `CreateClient` 都会返回一个新 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-227">A new `HttpClient` instance is returned each time `CreateClient` is called on the `IHttpClientFactory`.</span></span> <span data-ttu-id="7d7bc-228">每个命名客户端都有一个 [HttpMessageHandler](/dotnet/api/system.net.http.httpmessagehandler)。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-228">There's an [HttpMessageHandler](/dotnet/api/system.net.http.httpmessagehandler) per named client.</span></span> <span data-ttu-id="7d7bc-229">`IHttpClientFactory` 将工厂创建的 `HttpMessageHandler` 实例汇集到池中，以减少资源消耗。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-229">`IHttpClientFactory` pools the `HttpMessageHandler` instances created by the factory to reduce resource consumption.</span></span> <span data-ttu-id="7d7bc-230">新建 `HttpClient` 实例时，可能会重用池中的 `HttpMessageHandler` 实例（如果生存期尚未到期的话）。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-230">An `HttpMessageHandler` instance may be reused from the pool when creating a new `HttpClient` instance if its lifetime hasn't expired.</span></span>

<span data-ttu-id="7d7bc-231">由于每个处理程序通常管理自己的基础 HTTP 连接，因此需要池化处理程序。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-231">Pooling of handlers is desirable as each handler typically manages its own underlying HTTP connections.</span></span> <span data-ttu-id="7d7bc-232">创建超出必要数量的处理程序可能会导致连接延迟。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-232">Creating more handlers than necessary can result in connection delays.</span></span> <span data-ttu-id="7d7bc-233">部分处理程序还保持连接无期限地打开，这样可以防止处理程序对 DNS 更改作出反应。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-233">Some handlers also keep connections open indefinitely, which can prevent the handler from reacting to DNS changes.</span></span>

<span data-ttu-id="7d7bc-234">处理程序的默认生存期为两分钟。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-234">The default handler lifetime is two minutes.</span></span> <span data-ttu-id="7d7bc-235">可在每个命名客户端上重写默认值。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-235">The default value can be overridden on a per named client basis.</span></span> <span data-ttu-id="7d7bc-236">若要替代值，请对创建客户端时返回的 `IHttpClientBuilder` 调用 [SetHandlerLifetime](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.sethandlerlifetime)：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-236">To override it, call [SetHandlerLifetime](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.sethandlerlifetime) on the `IHttpClientBuilder` that is returned when creating the client:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet11)]

<span data-ttu-id="7d7bc-237">无需处置客户端。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-237">Disposal of the client isn't required.</span></span> <span data-ttu-id="7d7bc-238">处置既取消传出请求，又保证在调用 [Dispose](/dotnet/api/system.idisposable.dispose#System_IDisposable_Dispose) 后无法使用给定的 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-238">Disposal cancels outgoing requests and guarantees the given `HttpClient` instance can't be used after calling [Dispose](/dotnet/api/system.idisposable.dispose#System_IDisposable_Dispose).</span></span> <span data-ttu-id="7d7bc-239">`IHttpClientFactory` 跟踪和处置 `HttpClient` 实例使用的资源。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-239">`IHttpClientFactory` tracks and disposes resources used by `HttpClient` instances.</span></span> <span data-ttu-id="7d7bc-240">`HttpClient` 实例通常可视为无需处置的 .NET 对象。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-240">The `HttpClient` instances can generally be treated as .NET objects not requiring disposal.</span></span>

<span data-ttu-id="7d7bc-241">保持各个 `HttpClient` 实例长时间处于活动状态是在 `IHttpClientFactory` 推出前使用的常见模式。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-241">Keeping a single `HttpClient` instance alive for a long duration is a common pattern used before the inception of `IHttpClientFactory`.</span></span> <span data-ttu-id="7d7bc-242">迁移到 `IHttpClientFactory` 后，就无需再使用此模式。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-242">This pattern becomes unnecessary after migrating to `IHttpClientFactory`.</span></span>

## <a name="logging"></a><span data-ttu-id="7d7bc-243">日志记录</span><span class="sxs-lookup"><span data-stu-id="7d7bc-243">Logging</span></span>

<span data-ttu-id="7d7bc-244">通过 `IHttpClientFactory` 创建的客户端记录所有请求的日志消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-244">Clients created via `IHttpClientFactory` record log messages for all requests.</span></span> <span data-ttu-id="7d7bc-245">在日志记录配置中启用合适的信息级别可以查看默认日志消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-245">Enable the appropriate information level in your logging configuration to see the default log messages.</span></span> <span data-ttu-id="7d7bc-246">仅在跟踪级别包含附加日志记录（例如请求标头的日志记录）。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-246">Additional logging, such as the logging of request headers, is only included at trace level.</span></span>

<span data-ttu-id="7d7bc-247">用于每个客户端的日志类别包含客户端名称。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-247">The log category used for each client includes the name of the client.</span></span> <span data-ttu-id="7d7bc-248">例如，名为“MyNamedClient”的客户端使用 `System.Net.Http.HttpClient.MyNamedClient.LogicalHandler` 类别来记录消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-248">A client named *MyNamedClient*, for example, logs messages with a category of `System.Net.Http.HttpClient.MyNamedClient.LogicalHandler`.</span></span> <span data-ttu-id="7d7bc-249">后缀为 LogicalHandler 的消息在请求处理程序管道外部发生。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-249">Messages suffixed with *LogicalHandler* occur outside the request handler pipeline.</span></span> <span data-ttu-id="7d7bc-250">在请求时，在管道中的任何其他处理程序处理请求之前记录消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-250">On the request, messages are logged before any other handlers in the pipeline have processed it.</span></span> <span data-ttu-id="7d7bc-251">在响应时，在任何其他管道处理程序接收响应之后记录消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-251">On the response, messages are logged after any other pipeline handlers have received the response.</span></span>

<span data-ttu-id="7d7bc-252">日志记录还在请求处理程序管道内部发生。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-252">Logging also occurs inside the request handler pipeline.</span></span> <span data-ttu-id="7d7bc-253">在“MyNamedClient”示例中，这些消息是针对日志类别 `System.Net.Http.HttpClient.MyNamedClient.ClientHandler` 进行记录。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-253">In the *MyNamedClient* example, those messages are logged against the log category `System.Net.Http.HttpClient.MyNamedClient.ClientHandler`.</span></span> <span data-ttu-id="7d7bc-254">在请求时，在所有其他处理程序运行后，以及刚好在通过网络发出请求之前记录消息。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-254">For the request, this occurs after all other handlers have run and immediately before the request is sent out on the network.</span></span> <span data-ttu-id="7d7bc-255">在响应时，此日志记录包含响应在通过处理程序管道被传递回去之前的状态。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-255">On the response, this logging includes the state of the response before it passes back through the handler pipeline.</span></span>

<span data-ttu-id="7d7bc-256">在管道内外启用日志记录，可以检查其他管道处理程序做出的更改。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-256">Enabling logging outside and inside the pipeline enables inspection of the changes made by the other pipeline handlers.</span></span> <span data-ttu-id="7d7bc-257">例如，其中可能包含对请求标头的更改，或者对响应状态代码的更改。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-257">This may include changes to request headers, for example, or to the response status code.</span></span>

<span data-ttu-id="7d7bc-258">通过在日志类别中包含客户端名称，可以在必要时对特定的命名客户端筛选日志。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-258">Including the name of the client in the log category enables log filtering for specific named clients where necessary.</span></span>

## <a name="configure-the-httpmessagehandler"></a><span data-ttu-id="7d7bc-259">配置 HttpMessageHandler</span><span class="sxs-lookup"><span data-stu-id="7d7bc-259">Configure the HttpMessageHandler</span></span>

<span data-ttu-id="7d7bc-260">控制客户端使用的内部 `HttpMessageHandler` 的配置是有必要的。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-260">It may be necessary to control the configuration of the inner `HttpMessageHandler` used by a client.</span></span>

<span data-ttu-id="7d7bc-261">在添加命名客户端或类型化客户端时，会返回 `IHttpClientBuilder`。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-261">An `IHttpClientBuilder` is returned when adding named or typed clients.</span></span> <span data-ttu-id="7d7bc-262">[ConfigurePrimaryHttpMessageHandler](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.configureprimaryhttpmessagehandler) 扩展方法可用于定义委托。</span><span class="sxs-lookup"><span data-stu-id="7d7bc-262">The [ConfigurePrimaryHttpMessageHandler](/dotnet/api/microsoft.extensions.dependencyinjection.httpclientbuilderextensions.configureprimaryhttpmessagehandler) extension method can be used to define a delegate.</span></span> <span data-ttu-id="7d7bc-263">委托用于创建和配置客户端使用的主要 `HttpMessageHandler`：</span><span class="sxs-lookup"><span data-stu-id="7d7bc-263">The delegate is used to create and configure the primary `HttpMessageHandler` used by that client:</span></span>

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet12)]
