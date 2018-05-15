---
title: 启动 HTTP 请求
author: stevejgordon
description: 了解如何将 IHttpClientFactory 接口用于管理 ASP.NET Core 中的逻辑 HttpClient 实例。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 05/02/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/http-requests
ms.openlocfilehash: 30ac239a38376feecffc3010387ec5e0009b6db6
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="initiate-http-requests"></a><span data-ttu-id="660e9-103">启动 HTTP 请求</span><span class="sxs-lookup"><span data-stu-id="660e9-103">Initiate HTTP requests</span></span>

<span data-ttu-id="660e9-104">作者：[Glenn Condron](https://github.com/glennc)[Ryan Nowak](https://github.com/rynowak) 和 [Steve Gordon](https://github.com/stevejgordon)</span><span class="sxs-lookup"><span data-stu-id="660e9-104">By [Glenn Condron](https://github.com/glennc), [Ryan Nowak](https://github.com/rynowak), and [Steve Gordon](https://github.com/stevejgordon)</span></span>

[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="660e9-105">可以注册 `IHttpClientFactory` 并将其用于配置和创建应用中的 [HttpClient](/dotnet/api/system.net.http.httpclient) 实例。</span><span class="sxs-lookup"><span data-stu-id="660e9-105">An `IHttpClientFactory` can be registered and used to configure and create [HttpClient](/dotnet/api/system.net.http.httpclient) instances in an app.</span></span> <span data-ttu-id="660e9-106">这能带来以下好处：</span><span class="sxs-lookup"><span data-stu-id="660e9-106">It offers the following benefits:</span></span>

* <span data-ttu-id="660e9-107">提供一个中心位置，用于命名和配置逻辑 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="660e9-107">Provides a central location for naming and configuring logical `HttpClient` instances.</span></span> <span data-ttu-id="660e9-108">例如，可以注册一个“github”客户端，将其配置为访问 GitHub。</span><span class="sxs-lookup"><span data-stu-id="660e9-108">For example, a "github" client can be registered and configured to access GitHub.</span></span> <span data-ttu-id="660e9-109">可以注册一个默认客户端用于其他用途。</span><span class="sxs-lookup"><span data-stu-id="660e9-109">A default client can be registered for other purposes.</span></span>
* <span data-ttu-id="660e9-110">通过委托 `HttpClient` 中的处理程序整理出站中间件的概念，并提供适用于基于 Polly 的中间件的扩展来利用概念。</span><span class="sxs-lookup"><span data-stu-id="660e9-110">Codifies the concept of outgoing middleware via delegating handlers in `HttpClient` and provides extensions for Polly-based middleware to take advantage of that.</span></span>
* <span data-ttu-id="660e9-111">管理基础 `HttpClientMessageHandler` 实例的池和生存期，避免在手动管理 `HttpClient` 生存期时出现常见的 DNS 问题。</span><span class="sxs-lookup"><span data-stu-id="660e9-111">Manages the pooling and lifetime of underlying `HttpClientMessageHandler` instances to avoid common DNS problems that occur when manually managing `HttpClient` lifetimes.</span></span>
* <span data-ttu-id="660e9-112">（通过 `ILogger`）添加可配置的记录体验，以处理工厂创建的客户端发送的所有请求。</span><span class="sxs-lookup"><span data-stu-id="660e9-112">Adds a configurable logging experience (via `ILogger`) for all requests sent through clients created by the factory.</span></span>

## <a name="consumption-patterns"></a><span data-ttu-id="660e9-113">消耗模式</span><span class="sxs-lookup"><span data-stu-id="660e9-113">Consumption patterns</span></span>

<span data-ttu-id="660e9-114">在应用中可以通过以下多种方式使用 `IHttpClientFactory`：</span><span class="sxs-lookup"><span data-stu-id="660e9-114">There are several ways `IHttpClientFactory` can be used in an app:</span></span>

* [<span data-ttu-id="660e9-115">基本用法</span><span class="sxs-lookup"><span data-stu-id="660e9-115">Basic usage</span></span>](#basic-usage)
* [<span data-ttu-id="660e9-116">命名客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-116">Named clients</span></span>](#named-clients)
* [<span data-ttu-id="660e9-117">类型化客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-117">Typed clients</span></span>](#typed-clients)
* [<span data-ttu-id="660e9-118">生成的客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-118">Generated clients</span></span>](#generated-clients)

<span data-ttu-id="660e9-119">它们之间不存在严格的优先级。</span><span class="sxs-lookup"><span data-stu-id="660e9-119">None of them are strictly superior to another.</span></span> <span data-ttu-id="660e9-120">最佳方法取决于应用的约束条件。</span><span class="sxs-lookup"><span data-stu-id="660e9-120">The best approach depends upon the app's constraints.</span></span>

### <a name="basic-usage"></a><span data-ttu-id="660e9-121">基本用法</span><span class="sxs-lookup"><span data-stu-id="660e9-121">Basic usage</span></span>

<span data-ttu-id="660e9-122">在 Startup.cs 的 `ConfigureServices` 方法中，通过在 `IServiceCollection` 上调用 `AddHttpClient` 扩展方法可以注册 `IHttpClientFactory`。</span><span class="sxs-lookup"><span data-stu-id="660e9-122">The `IHttpClientFactory` can be registered by calling the `AddHttpClient` extension method on the `IServiceCollection`, inside the `ConfigureServices` method in Startup.cs.</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet1)]

<span data-ttu-id="660e9-123">注册后，在可以使用[依赖关系注入](xref:fundamentals/dependency-injection) (DI) 注入服务的任何位置，代码都能接受 `IHttpClientFactory`。</span><span class="sxs-lookup"><span data-stu-id="660e9-123">Once registered, code can accept an `IHttpClientFactory` anywhere services can be injected with [dependency injection](xref:fundamentals/dependency-injection) (DI).</span></span> <span data-ttu-id="660e9-124">`IHttpClientFactory` 可以用于创建 `HttpClient` 实例：</span><span class="sxs-lookup"><span data-stu-id="660e9-124">The `IHttpClientFactory` can be used to create a `HttpClient` instance:</span></span>

[!code-csharp[](http-requests/samples/Pages/BasicUsage.cshtml.cs?name=snippet1&highlight=9-12,20)]

<span data-ttu-id="660e9-125">以这种方式使用 `IHttpClientFactory` 非常适合重构现有应用。</span><span class="sxs-lookup"><span data-stu-id="660e9-125">Using `IHttpClientFactory` in this fashion is a great way to refactor an existing app.</span></span> <span data-ttu-id="660e9-126">这不会影响 `HttpClient` 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="660e9-126">It has no impact on the way `HttpClient` is used.</span></span> <span data-ttu-id="660e9-127">在当前创建 `HttpClient` 实例的位置，使用对 `CreateClient` 的调用替换这些匹配项。</span><span class="sxs-lookup"><span data-stu-id="660e9-127">In places where `HttpClient` instances are currently created, replace those occurrences with a call to `CreateClient`.</span></span>

### <a name="named-clients"></a><span data-ttu-id="660e9-128">命名客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-128">Named clients</span></span>

<span data-ttu-id="660e9-129">如果应用需要区别使用多个 `HttpClient`（每个的配置都不同），可以选择使用“命名客户端”。</span><span class="sxs-lookup"><span data-stu-id="660e9-129">If an app requires multiple distinct uses of `HttpClient`, each with a different configuration, an option is to use **named clients**.</span></span> <span data-ttu-id="660e9-130">可以在 `HttpClient` 中注册时指定命名 `ConfigureServices` 的配置。</span><span class="sxs-lookup"><span data-stu-id="660e9-130">Configuration for a named `HttpClient` can be specified during registration in `ConfigureServices`.</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet2)]

<span data-ttu-id="660e9-131">上述代码调用了 `AddHttpClient`，并提供名称“github”。</span><span class="sxs-lookup"><span data-stu-id="660e9-131">In the preceding code, `AddHttpClient` is called, providing the name "github".</span></span> <span data-ttu-id="660e9-132">此客户端应用了一些默认配置，也就是需要基址和两个标头来使用 GitHub API。</span><span class="sxs-lookup"><span data-stu-id="660e9-132">This client has some default configuration applied&mdash;namely the base address and two headers required to work with the GitHub API.</span></span>

<span data-ttu-id="660e9-133">每次调用 `CreateClient` 时，都会创建 `HttpClient` 的新实例，并调用配置操作。</span><span class="sxs-lookup"><span data-stu-id="660e9-133">Each time `CreateClient` is called, a new instance of `HttpClient` is created and the configuration action is called.</span></span>

<span data-ttu-id="660e9-134">要使用命名客户端，可将字符串参数传递到 `CreateClient`。</span><span class="sxs-lookup"><span data-stu-id="660e9-134">To consume a named client, a string parameter can be passed to `CreateClient`.</span></span> <span data-ttu-id="660e9-135">指定要创建的客户端的名称：</span><span class="sxs-lookup"><span data-stu-id="660e9-135">Specify the name of the client to be created:</span></span>

[!code-csharp[](http-requests/samples/Pages/NamedClient.cshtml.cs?name=snippet1&highlight=20)]

<span data-ttu-id="660e9-136">在上述代码中，请求不需要指定主机名。</span><span class="sxs-lookup"><span data-stu-id="660e9-136">In the preceding code, the request doesn't need to specify a hostname.</span></span> <span data-ttu-id="660e9-137">可以仅传递路径，因为采用了为客户端配置的基址。</span><span class="sxs-lookup"><span data-stu-id="660e9-137">It can pass just the path, since the base address configured for the client is used.</span></span>

### <a name="typed-clients"></a><span data-ttu-id="660e9-138">类型化客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-138">Typed clients</span></span>

<span data-ttu-id="660e9-139">类型化客户端提供与命名客户端一样的功能，不需要将字符串用作密钥。</span><span class="sxs-lookup"><span data-stu-id="660e9-139">Typed clients provide the same capabilities as named clients without the need to use strings as keys.</span></span> <span data-ttu-id="660e9-140">类型化客户端方法在使用客户端时提供 IntelliSense 和编译器帮助。</span><span class="sxs-lookup"><span data-stu-id="660e9-140">The typed client approach provides IntelliSense and compiler help when consuming clients.</span></span> <span data-ttu-id="660e9-141">它们提供单个地址来配置特定 `HttpClient` 并与其进行交互。</span><span class="sxs-lookup"><span data-stu-id="660e9-141">They provide a single location to configure and interact with a particular `HttpClient`.</span></span> <span data-ttu-id="660e9-142">例如，单个类型化客户端可能用于单个后端终结点，并封装此终结点的所有处理逻辑。</span><span class="sxs-lookup"><span data-stu-id="660e9-142">For example, a single typed client might be used for a single backend endpoint and encapsulate all logic dealing with that endpoint.</span></span> <span data-ttu-id="660e9-143">另一个优势是它们使用 DI 且可以被注入到应用中需要的位置。</span><span class="sxs-lookup"><span data-stu-id="660e9-143">Another advantage is that they work with DI and can be injected where required in your app.</span></span>

<span data-ttu-id="660e9-144">类型化客户端在构造函数中接收 `HttpClient` 参数：</span><span class="sxs-lookup"><span data-stu-id="660e9-144">A typed client accepts a `HttpClient` parameter in its constructor:</span></span>

[!code-csharp[](http-requests/samples/GitHub/GitHubService.cs?name=snippet1&highlight=5)]

<span data-ttu-id="660e9-145">在上述代码中，配置转移到了类型化客户端中。</span><span class="sxs-lookup"><span data-stu-id="660e9-145">In the preceding code, the configuration is moved into the typed client.</span></span> <span data-ttu-id="660e9-146">`HttpClient` 对象公开为公共属性。</span><span class="sxs-lookup"><span data-stu-id="660e9-146">The `HttpClient` object is exposed as a public property.</span></span> <span data-ttu-id="660e9-147">可以定义公开 `HttpClient` 功能的特定于 API 的方法。</span><span class="sxs-lookup"><span data-stu-id="660e9-147">It's possible to define API-specific methods that expose `HttpClient` functionality.</span></span> <span data-ttu-id="660e9-148">`GetLatestDocsIssue` 方法从 GitHub 存储库封装查询和分析最新问题所需的代码。</span><span class="sxs-lookup"><span data-stu-id="660e9-148">The `GetLatestDocsIssue` method encapsulates the code needed to query for and parse out the latest issue from a GitHub repository.</span></span>

<span data-ttu-id="660e9-149">要注册类型化客户端，可在 `ConfigureServices` 中使用通用的 `AddHttpClient` 扩展方法，指定类型化客户端类：</span><span class="sxs-lookup"><span data-stu-id="660e9-149">To register a typed client, the generic `AddHttpClient` extension method can be used within `ConfigureServices`, specifying the typed client class:</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet3)]

<span data-ttu-id="660e9-150">使用 DI 将类型客户端注册为暂时客户端。</span><span class="sxs-lookup"><span data-stu-id="660e9-150">The typed client is registered as transient with DI.</span></span> <span data-ttu-id="660e9-151">可以直接插入或使用类型化客户端：</span><span class="sxs-lookup"><span data-stu-id="660e9-151">The typed client can be injected and consumed directly:</span></span>

[!code-csharp[](http-requests/samples/Pages/TypedClient.cshtml.cs?name=snippet1&highlight=11-14,20)]

<span data-ttu-id="660e9-152">根据你的喜好，可以在 `ConfigureServices` 中注册时指定类型化客户端的配置，而不是在类型化客户端的构造函数中指定：</span><span class="sxs-lookup"><span data-stu-id="660e9-152">If preferred, the configuration for a typed client can be specified during registration in `ConfigureServices`, rather than in the typed client's constructor:</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet4)]

<span data-ttu-id="660e9-153">可以将 `HttpClient` 完全封装在类型化客户端中。</span><span class="sxs-lookup"><span data-stu-id="660e9-153">It's possible to entirely encapsulate the `HttpClient` within a typed client.</span></span> <span data-ttu-id="660e9-154">不是将它公开为属性，而是可以提供公共方法，用于在内部调用 `HttpClient`。</span><span class="sxs-lookup"><span data-stu-id="660e9-154">Rather than exposing it as a property, public methods can be provided which call the `HttpClient` instance internally.</span></span>

[!code-csharp[](http-requests/samples/GitHub/RepoService.cs?name=snippet1&highlight=3)]

<span data-ttu-id="660e9-155">在上述代码中，`HttpClient` 存储未私有字段。</span><span class="sxs-lookup"><span data-stu-id="660e9-155">In the preceding code, the `HttpClient` is stored as a private field.</span></span> <span data-ttu-id="660e9-156">进行外部调用的所有访问都经由 `GetRepos` 方法。</span><span class="sxs-lookup"><span data-stu-id="660e9-156">All access to make external calls goes through the `GetRepos` method.</span></span>

### <a name="generated-clients"></a><span data-ttu-id="660e9-157">生成的客户端</span><span class="sxs-lookup"><span data-stu-id="660e9-157">Generated clients</span></span>

<span data-ttu-id="660e9-158">`IHttpClientFactory` 可结合其他第三方库（例如 [Refit](https://github.com/paulcbetts/refit)）使用。</span><span class="sxs-lookup"><span data-stu-id="660e9-158">`IHttpClientFactory` can be used in combination with other third-party libraries such as [Refit](https://github.com/paulcbetts/refit).</span></span> <span data-ttu-id="660e9-159">Refit 是.NET 的 REST 库。</span><span class="sxs-lookup"><span data-stu-id="660e9-159">Refit is a REST library for .NET.</span></span> <span data-ttu-id="660e9-160">它将 REST API 转换为实时接口。</span><span class="sxs-lookup"><span data-stu-id="660e9-160">It converts REST APIs into live interfaces.</span></span> <span data-ttu-id="660e9-161">`RestService` 动态生成该接口的实现，使用 `HttpClient` 进行外部 HTTP 调用。</span><span class="sxs-lookup"><span data-stu-id="660e9-161">An implementation of the interface is generated dynamically by the `RestService`, using `HttpClient` to make the external HTTP calls.</span></span>

<span data-ttu-id="660e9-162">定义了接口和答复来代表外部 API 及其响应：</span><span class="sxs-lookup"><span data-stu-id="660e9-162">An interface and a reply are defined to represent the external API and its response:</span></span>

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

<span data-ttu-id="660e9-163">可以添加类型化客户端，使用 Refit 生成实现：</span><span class="sxs-lookup"><span data-stu-id="660e9-163">A typed client can be added, using Refit to generate the implementation:</span></span>

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

<span data-ttu-id="660e9-164">可以在必要时使用定义的接口，以及由 DI 和 Refit 提供的实现：</span><span class="sxs-lookup"><span data-stu-id="660e9-164">The defined interface can be consumed where necessary, with the implementation provided by DI and Refit:</span></span>

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

## <a name="outgoing-request-middleware"></a><span data-ttu-id="660e9-165">出站请求中间件</span><span class="sxs-lookup"><span data-stu-id="660e9-165">Outgoing request middleware</span></span>

<span data-ttu-id="660e9-166">`HttpClient` 已经具有委托处理程序的概念，这些委托处理程序可以链接在一起，处理出站 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="660e9-166">`HttpClient` already has the concept of delegating handlers that can be linked together for outgoing HTTP requests.</span></span> <span data-ttu-id="660e9-167">`IHttpClientFactory` 可以轻松定义处理程序并应用于每个命名客户端。</span><span class="sxs-lookup"><span data-stu-id="660e9-167">The `IHttpClientFactory` makes it easy to define the handlers to apply for each named client.</span></span> <span data-ttu-id="660e9-168">它支持注册和链接多个处理程序，以生成出站请求中间件管道。</span><span class="sxs-lookup"><span data-stu-id="660e9-168">It supports registration and chaining of multiple handlers to build an outgoing request middleware pipeline.</span></span> <span data-ttu-id="660e9-169">每个处理程序都可以在出站请求前后执行工作。</span><span class="sxs-lookup"><span data-stu-id="660e9-169">Each of these handlers is able to perform work before and after the outgoing request.</span></span> <span data-ttu-id="660e9-170">此模式类似于 ASP.NET Core 中的入站中间件管道。</span><span class="sxs-lookup"><span data-stu-id="660e9-170">This pattern is similar to the inbound middleware pipeline in ASP.NET Core.</span></span> <span data-ttu-id="660e9-171">此模式提供了一种用于管理围绕 HTTP 请求的横切关注点的机制，包括缓存、错误处理、序列化以及日志记录。</span><span class="sxs-lookup"><span data-stu-id="660e9-171">The pattern provides a mechanism to manage cross-cutting concerns around HTTP requests, including caching, error handling, serialization, and logging.</span></span>

<span data-ttu-id="660e9-172">要创建处理程序，请定义一个派生自 `DelegatingHandler` 的类。</span><span class="sxs-lookup"><span data-stu-id="660e9-172">To create a handler, define a class deriving from `DelegatingHandler`.</span></span> <span data-ttu-id="660e9-173">重写 `SendAsync` 方法，在将请求传递至管道中的下一个处理程序之前执行代码：</span><span class="sxs-lookup"><span data-stu-id="660e9-173">Override the `SendAsync` method to execute code before passing the request to the next handler in the pipeline:</span></span>

[!code-csharp[Main](http-requests/samples/Handlers/ValidateHeaderHandler.cs?name=snippet1)]

<span data-ttu-id="660e9-174">上述代码定义了基本处理程序。</span><span class="sxs-lookup"><span data-stu-id="660e9-174">The preceding code defines a basic handler.</span></span> <span data-ttu-id="660e9-175">它会在遇到请求时检查是否包括 X-API-KEY 标头。</span><span class="sxs-lookup"><span data-stu-id="660e9-175">It checks to see if an X-API-KEY header has been included on the request.</span></span> <span data-ttu-id="660e9-176">如果标头缺失，它可以避免 HTTP 调用，并返回合适的响应。</span><span class="sxs-lookup"><span data-stu-id="660e9-176">If the header is missing, it can avoid the HTTP call and return a suitable response.</span></span>

<span data-ttu-id="660e9-177">在注册期间可将一个或多个标头添加到 `HttpClient` 的配置。</span><span class="sxs-lookup"><span data-stu-id="660e9-177">During registration, one or more handlers can be added to the configuration for a `HttpClient`.</span></span> <span data-ttu-id="660e9-178">此任务通过 `IHttpClientBuilder` 上的扩展方法完成。</span><span class="sxs-lookup"><span data-stu-id="660e9-178">This task is accomplished via extension methods on the `IHttpClientBuilder`.</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet5)]

<span data-ttu-id="660e9-179">在上述代码中通过 DI 注册了 `ValidateHeaderHandler`。</span><span class="sxs-lookup"><span data-stu-id="660e9-179">In the preceding code, the `ValidateHeaderHandler` is registered with DI.</span></span> <span data-ttu-id="660e9-180">处理程序必须在 DI 中注册为临时处理程序。</span><span class="sxs-lookup"><span data-stu-id="660e9-180">The handler **must** be registered in DI as transient.</span></span> <span data-ttu-id="660e9-181">注册后可以调用 `AddHttpMessageHandler`，传入标头的类型。</span><span class="sxs-lookup"><span data-stu-id="660e9-181">Once registered, `AddHttpMessageHandler` can be called, passing in the type for the handler.</span></span>

<span data-ttu-id="660e9-182">可以按处理程序应该执行的顺序注册多个处理程序。</span><span class="sxs-lookup"><span data-stu-id="660e9-182">Multiple handlers can be registered in the order that they should execute.</span></span> <span data-ttu-id="660e9-183">每个处理程序都会覆盖下一个处理程序，直到最终 `HttpClientHandler` 执行请求：</span><span class="sxs-lookup"><span data-stu-id="660e9-183">Each handler wraps the next handler until the final `HttpClientHandler` executes the request:</span></span>

[!code-csharp[](http-requests/samples/Startup.cs?name=snippet6)]

## <a name="use-polly-based-handlers"></a><span data-ttu-id="660e9-184">使用基于 Polly 的处理程序</span><span class="sxs-lookup"><span data-stu-id="660e9-184">Use Polly-based handlers</span></span>

<span data-ttu-id="660e9-185">`IHttpClientFactory` 与一个名为 [Polly](https://github.com/App-vNext/Polly) 的热门第三方库集成。</span><span class="sxs-lookup"><span data-stu-id="660e9-185">`IHttpClientFactory` integrates with a popular third-party library called [Polly](https://github.com/App-vNext/Polly).</span></span> <span data-ttu-id="660e9-186">Polly 是适用于 .NET 的全面恢复和临时故障处理库。</span><span class="sxs-lookup"><span data-stu-id="660e9-186">Polly is a comprehensive resilience and transient fault-handling library for .NET.</span></span> <span data-ttu-id="660e9-187">开发人员通过它可以表达策略，例如以流畅且线程安全的方式处理重试、断路器、超时、Bulkhead 隔离和回退。</span><span class="sxs-lookup"><span data-stu-id="660e9-187">It allows developers to express policies such as Retry, Circuit Breaker, Timeout, Bulkhead Isolation, and Fallback in a fluent and thread-safe manner.</span></span>

<span data-ttu-id="660e9-188">提供了扩展方法，以实现将 Polly 策略用于配置的 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="660e9-188">Extension methods are provided to enable the use of Polly policies with configured `HttpClient` instances.</span></span> <span data-ttu-id="660e9-189">在名为“Microsoft.Extensions.Http.Polly”的 NuGet 包中可以使用 Polly 扩展。</span><span class="sxs-lookup"><span data-stu-id="660e9-189">The Polly extensions are available in a NuGet package called 'Microsoft.Extensions.Http.Polly'.</span></span> <span data-ttu-id="660e9-190">“Microsoft.AspNetCore.App”元包在默认情况下不包含此包。</span><span class="sxs-lookup"><span data-stu-id="660e9-190">This package is not included by default by the 'Microsoft.AspNetCore.App' metapackage.</span></span> <span data-ttu-id="660e9-191">若要使用扩展，需要将 PackageReference 显式包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="660e9-191">To use the extensions, a PackageReference should be explicitly included in the project.</span></span>

[!code-csharp[](http-requests/samples/HttpClientFactorySample.csproj?highlight=9)]

<span data-ttu-id="660e9-192">还原此包后，可以使用扩展方法来支持将基于 Polly 的处理程序添加至客户端。</span><span class="sxs-lookup"><span data-stu-id="660e9-192">After restoring this package, extension methods are available to support adding Polly-based handlers to clients.</span></span>

### <a name="handle-transient-faults"></a><span data-ttu-id="660e9-193">处理临时故障</span><span class="sxs-lookup"><span data-stu-id="660e9-193">Handle transient faults</span></span>

<span data-ttu-id="660e9-194">在执行外部 HTTP 调用时，最可能遇到的故障是临时故障。</span><span class="sxs-lookup"><span data-stu-id="660e9-194">The most common faults you may expect to occur when making external HTTP calls will be transient.</span></span> <span data-ttu-id="660e9-195">包含了一种简便的扩展方法，该方法名为 `AddTransientHttpErrorPolicy`，允许定义策略来处理临时故障。</span><span class="sxs-lookup"><span data-stu-id="660e9-195">A convenient extension method called `AddTransientHttpErrorPolicy` is included which allows a policy to be defined to handle transient errors.</span></span> <span data-ttu-id="660e9-196">使用这种扩展方法配置的策略可以处理 `HttpRequestException`、HTTP 5xx 响应以及 HTTP 408 响应。</span><span class="sxs-lookup"><span data-stu-id="660e9-196">Policies configured with this extension method handle `HttpRequestException`, HTTP 5xx responses, and HTTP 408 responses.</span></span>

<span data-ttu-id="660e9-197">`AddTransientHttpErrorPolicy` 扩展可在 `ConfigureServices` 内使用。</span><span class="sxs-lookup"><span data-stu-id="660e9-197">The `AddTransientHttpErrorPolicy` extension can be used within `ConfigureServices`.</span></span> <span data-ttu-id="660e9-198">该扩展可以提供 `PolicyBuilder` 对象的访问权限，该对象配置为处理表示可能的临时故障的错误：</span><span class="sxs-lookup"><span data-stu-id="660e9-198">The extension provides access to a `PolicyBuilder` object configured to handle errors representing a possible transient fault:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet7)]

<span data-ttu-id="660e9-199">上述代码中定义了 `WaitAndRetryAsync` 策略。</span><span class="sxs-lookup"><span data-stu-id="660e9-199">In the preceding code, a `WaitAndRetryAsync` policy is defined.</span></span> <span data-ttu-id="660e9-200">请求失败后最多可以重试三次，每次尝试间隔 600 ms。</span><span class="sxs-lookup"><span data-stu-id="660e9-200">Failed requests are retried up to three times with a delay of 600 ms between attempts.</span></span>

### <a name="dynamically-select-policies"></a><span data-ttu-id="660e9-201">动态选择策略</span><span class="sxs-lookup"><span data-stu-id="660e9-201">Dynamically select policies</span></span>

<span data-ttu-id="660e9-202">存在其他扩展方法，可以用于添加基于 Polly 的处理程序。</span><span class="sxs-lookup"><span data-stu-id="660e9-202">Additional extension methods exist which can be used to add Polly-based handlers.</span></span> <span data-ttu-id="660e9-203">这类扩展的其中一个是 `AddPolicyHandler`，它具备多个重载。</span><span class="sxs-lookup"><span data-stu-id="660e9-203">One such extension is `AddPolicyHandler`, which has multiple overloads.</span></span> <span data-ttu-id="660e9-204">一个重载允许在定义要应用的策略时检查该请求：</span><span class="sxs-lookup"><span data-stu-id="660e9-204">One overload allows the request to be inspected when defining which policy to apply:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet8)]

<span data-ttu-id="660e9-205">在上述代码中，如果出站请求为 GET，则应用 10 秒超时。</span><span class="sxs-lookup"><span data-stu-id="660e9-205">In the preceding code, if the outgoing request is a GET, a 10-second timeout is applied.</span></span> <span data-ttu-id="660e9-206">其他所有 HTTP 方法应用 30 秒超时。</span><span class="sxs-lookup"><span data-stu-id="660e9-206">For any other HTTP method, a 30-second timeout is used.</span></span>

### <a name="add-multiple-polly-handlers"></a><span data-ttu-id="660e9-207">添加多个 Polly 处理程序</span><span class="sxs-lookup"><span data-stu-id="660e9-207">Add multiple Polly handlers</span></span>

<span data-ttu-id="660e9-208">嵌套 Polly 策略以增强功能是很常见的：</span><span class="sxs-lookup"><span data-stu-id="660e9-208">It is common to nest Polly policies to provide enhanced functionality:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet9)]

<span data-ttu-id="660e9-209">在上述示例中，添加两个处理程序。</span><span class="sxs-lookup"><span data-stu-id="660e9-209">In the preceding example, two handlers are added.</span></span> <span data-ttu-id="660e9-210">第一个使用 `AddTransientHttpErrorPolicy` 扩展添加重试策略。</span><span class="sxs-lookup"><span data-stu-id="660e9-210">The first uses the `AddTransientHttpErrorPolicy` extension to add a retry policy.</span></span> <span data-ttu-id="660e9-211">若请求失败，最多可重试三次。</span><span class="sxs-lookup"><span data-stu-id="660e9-211">Failed requests are retried up to three times.</span></span> <span data-ttu-id="660e9-212">第一个调用 `AddTransientHttpErrorPolicy` 添加断路器策略。</span><span class="sxs-lookup"><span data-stu-id="660e9-212">The second call to `AddTransientHttpErrorPolicy` adds a circuit breaker policy.</span></span> <span data-ttu-id="660e9-213">如果尝试连续失败了五次，则会阻止后续外部请求 30 秒。</span><span class="sxs-lookup"><span data-stu-id="660e9-213">Further external requests are blocked for 30 seconds if five failed attempts occur sequentially.</span></span> <span data-ttu-id="660e9-214">断路器策略处于监控状态。</span><span class="sxs-lookup"><span data-stu-id="660e9-214">Circuit breaker policies are stateful.</span></span> <span data-ttu-id="660e9-215">通过此客户端进行的所有调用都共享同样的线路状态。</span><span class="sxs-lookup"><span data-stu-id="660e9-215">All calls through this client share the same circuit state.</span></span>

### <a name="add-policies-from-the-polly-registry"></a><span data-ttu-id="660e9-216">从 Polly 注册表添加策略</span><span class="sxs-lookup"><span data-stu-id="660e9-216">Add policies from the Polly registry</span></span>

<span data-ttu-id="660e9-217">管理常用策略的一种方法是一次性定义它们并使用 `PolicyRegistry` 注册它们。</span><span class="sxs-lookup"><span data-stu-id="660e9-217">An approach to managing regularly used policies is to define them once and register them with a `PolicyRegistry`.</span></span> <span data-ttu-id="660e9-218">提供了一种扩展方法，可以使用注册表中的策略添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="660e9-218">An extension method is provided which allows a handler to be added using a policy from the registry:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet10)]

<span data-ttu-id="660e9-219">在上述代码中，将 PolicyRegistry 添加到了 `ServiceCollection`，并使用它注册了两个策略。</span><span class="sxs-lookup"><span data-stu-id="660e9-219">In the preceding code, a PolicyRegistry is added to the `ServiceCollection` and two policies are registered with it.</span></span> <span data-ttu-id="660e9-220">要使用注册表中的策略，请使用 `AddPolicyHandlerFromRegistry` 方法传递要应用的策略的名称。</span><span class="sxs-lookup"><span data-stu-id="660e9-220">In order to use a policy from the registry, the `AddPolicyHandlerFromRegistry` method is used, passing the name of the policy to apply.</span></span>

<span data-ttu-id="660e9-221">要进一步了解 `IHttpClientFactory` 和 Polly 集成，请参考 [Polly Wiki](https://github.com/App-vNext/Polly/wiki/Polly-and-HttpClientFactory)。</span><span class="sxs-lookup"><span data-stu-id="660e9-221">Further information about `IHttpClientFactory` and Polly integrations can be found on the [Polly wiki](https://github.com/App-vNext/Polly/wiki/Polly-and-HttpClientFactory).</span></span>

## <a name="httpclient-and-lifetime-management"></a><span data-ttu-id="660e9-222">HttpClient 和生存期管理</span><span class="sxs-lookup"><span data-stu-id="660e9-222">HttpClient and lifetime management</span></span>

<span data-ttu-id="660e9-223">每次在 `IHttpClientFactory` 上调用 `CreateClient` 都会返回一个新的 `HttpClient` 实例。</span><span class="sxs-lookup"><span data-stu-id="660e9-223">Each time `CreateClient` is called on the `IHttpClientFactory`, a new instance of a `HttpClient` is returned.</span></span> <span data-ttu-id="660e9-224">每个命名客户端都会有一个 `HttpMessageHandler`。</span><span class="sxs-lookup"><span data-stu-id="660e9-224">There will be a `HttpMessageHandler` per named client.</span></span> <span data-ttu-id="660e9-225">`IHttpClientFactory` 将汇集工厂创建的 `HttpMessageHandler` 实例，以减少资源消耗。</span><span class="sxs-lookup"><span data-stu-id="660e9-225">`IHttpClientFactory` will pool the `HttpMessageHandler` instances created by the factory to reduce resource consumption.</span></span> <span data-ttu-id="660e9-226">如果 `HttpMessageHandler` 实例的生存期尚未过期，那么在创建新的 `HttpClient` 实例时，可能会从池中重用该实例。</span><span class="sxs-lookup"><span data-stu-id="660e9-226">A `HttpMessageHandler` instance may be reused from the pool when creating a new `HttpClient` instance if its lifetime hasn't expired.</span></span> 

<span data-ttu-id="660e9-227">由于每个处理程序通常都管理自己的基础 HTTP 连接，所以有必要汇集处理程序；创建的处理程序数量如果多于必需的数量，则可能导致连接延迟。</span><span class="sxs-lookup"><span data-stu-id="660e9-227">Pooling of handlers is desirable as each handler typically manages its own underlying HTTP connections; creating more handlers than necessary can result in connection delays.</span></span> <span data-ttu-id="660e9-228">部分处理程序还保持连接无期限地打开，这样可以防止处理程序对 DNS 更改作出反应。</span><span class="sxs-lookup"><span data-stu-id="660e9-228">Some handlers also keep connections open indefinitely, which can prevent the handler from reacting to DNS changes.</span></span>

<span data-ttu-id="660e9-229">处理程序的默认生存期为两分钟。</span><span class="sxs-lookup"><span data-stu-id="660e9-229">The default handler lifetime is two minutes.</span></span> <span data-ttu-id="660e9-230">可在每个命名客户端上重写默认值。</span><span class="sxs-lookup"><span data-stu-id="660e9-230">The default value can be overridden on a per named client basis.</span></span> <span data-ttu-id="660e9-231">要重写该值，请在创建客户端时在返回的 `IHttpClientBuilder` 上调用 `SetHandlerLifetime`：</span><span class="sxs-lookup"><span data-stu-id="660e9-231">To override it, call `SetHandlerLifetime` on the `IHttpClientBuilder` that is returned when creating the client:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet11)]

## <a name="logging"></a><span data-ttu-id="660e9-232">日志记录</span><span class="sxs-lookup"><span data-stu-id="660e9-232">Logging</span></span>

<span data-ttu-id="660e9-233">通过 `IHttpClientFactory` 创建的客户端记录所有请求的日志消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-233">Clients created via `IHttpClientFactory` record log messages for all requests.</span></span> <span data-ttu-id="660e9-234">你将需要在日志记录配置中启用合适的信息级别，从而查看默认日志消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-234">You'll need to enable the appropriate information level in your logging configuration to see the default log messages.</span></span> <span data-ttu-id="660e9-235">仅在跟踪级别包含附加日志记录（例如请求标头的日志记录）。</span><span class="sxs-lookup"><span data-stu-id="660e9-235">Additional logging, such as the logging of request headers, is only included at trace level.</span></span>

<span data-ttu-id="660e9-236">用于每个客户端的日志类别包含客户端名称。</span><span class="sxs-lookup"><span data-stu-id="660e9-236">The log category used for each client includes the name of the client.</span></span> <span data-ttu-id="660e9-237">例如，名为“MyNamedClient”的客户端会使用 `System.Net.Http.HttpClient.MyNamedClient.LogicalHandler` 类别记录消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-237">A client named "MyNamedClient", for example, logs messages with a category of `System.Net.Http.HttpClient.MyNamedClient.LogicalHandler`.</span></span> <span data-ttu-id="660e9-238">请求处理程序管道的外部会出现带有“LogicalHandler”后缀的消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-238">Messages with the suffix of "LogicalHandler" occur on the outside of request handler pipeline.</span></span> <span data-ttu-id="660e9-239">在请求时，在管道中的任何其他处理程序处理请求之前记录消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-239">On the request, messages are logged before any other handlers in the pipeline have processed it.</span></span> <span data-ttu-id="660e9-240">在响应时，在任何其他管道处理程序接收响应之后记录消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-240">On the response, messages are logged after any other pipeline handlers have received the response.</span></span>

<span data-ttu-id="660e9-241">在请求处理程序管道内部也会进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="660e9-241">Logging also occurs on the inside of the request handler pipeline.</span></span> <span data-ttu-id="660e9-242">在“MyNamedClient”的例子中，针对日志类别 `System.Net.Http.HttpClient.MyNamedClient.ClientHandler` 记录了这些消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-242">In the case of the "MyNamedClient" example, those messages are logged against the log category `System.Net.Http.HttpClient.MyNamedClient.ClientHandler`.</span></span> <span data-ttu-id="660e9-243">在请求时，在所有其他处理程序运行后，以及刚好在通过网络发出请求之前记录消息。</span><span class="sxs-lookup"><span data-stu-id="660e9-243">For the request, this occurs after all other handlers have run and immediately before the request is sent out on the network.</span></span> <span data-ttu-id="660e9-244">在响应时，此日志记录包含响应在通过处理程序管道被传递回去之前的状态。</span><span class="sxs-lookup"><span data-stu-id="660e9-244">On the response, this logging includes the state of the response before it passes back through the handler pipeline.</span></span>

<span data-ttu-id="660e9-245">在管道内外启用日志记录，可以检查其他管道处理程序所作的更改。</span><span class="sxs-lookup"><span data-stu-id="660e9-245">Enabling logging on the outside and inside of the pipeline enables inspection of the changes made by the other pipeline handlers.</span></span> <span data-ttu-id="660e9-246">例如，其中可能包含对请求标头的更改，或者对响应状态代码的更改。</span><span class="sxs-lookup"><span data-stu-id="660e9-246">This may include changes to request headers, for example, or to the response status code.</span></span>

<span data-ttu-id="660e9-247">通过在日志类别中包含客户端名称，可以在必要时对特定的命名客户端筛选日志。</span><span class="sxs-lookup"><span data-stu-id="660e9-247">Including the name of the client in the log category enables log filtering for specific named clients where necessary.</span></span>

## <a name="configure-the-httpmessagehandler"></a><span data-ttu-id="660e9-248">配置 HttpMessageHandler</span><span class="sxs-lookup"><span data-stu-id="660e9-248">Configure the HttpMessageHandler</span></span>

<span data-ttu-id="660e9-249">控制客户端使用的内部 `HttpMessageHandler` 的配置是有必要的。</span><span class="sxs-lookup"><span data-stu-id="660e9-249">It may be necessary to control the configuration of the inner `HttpMessageHandler` used by a client.</span></span>

<span data-ttu-id="660e9-250">在添加命名客户端或类型化客户端时，会返回 `IHttpClientBuilder`。</span><span class="sxs-lookup"><span data-stu-id="660e9-250">An `IHttpClientBuilder` is returned when adding named or typed clients.</span></span> <span data-ttu-id="660e9-251">`ConfigurePrimaryHttpMessageHandler` 扩展方法可以用于定义委托。</span><span class="sxs-lookup"><span data-stu-id="660e9-251">The `ConfigurePrimaryHttpMessageHandler` extension method can be used to define a delegate.</span></span> <span data-ttu-id="660e9-252">委托用于创建和配置客户端使用的主要 `HttpMessageHandler`：</span><span class="sxs-lookup"><span data-stu-id="660e9-252">The delegate is used to create and configure the primary `HttpMessageHandler` used by that client:</span></span>

[!code-csharp[Main](http-requests/samples/Startup.cs?name=snippet12)]
