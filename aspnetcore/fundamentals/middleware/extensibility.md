---
title: ASP.NET Core 中基于工厂的中间件激活
author: guardrex
description: 了解如何在 ASP.NET Core 中通过基于工厂的激活实现使用强类型中间件。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 08/14/2018
uid: fundamentals/middleware/extensibility
ms.openlocfilehash: 346f5e7b28a9cd17a03a864772ed8b2e4be9455b
ms.sourcegitcommit: 2c158fcfd325cad97ead608a816e525fe3dcf757
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "41751514"
---
# <a name="factory-based-middleware-activation-in-aspnet-core"></a><span data-ttu-id="ac5bd-103">ASP.NET Core 中基于工厂的中间件激活</span><span class="sxs-lookup"><span data-stu-id="ac5bd-103">Factory-based middleware activation in ASP.NET Core</span></span>

<span data-ttu-id="ac5bd-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ac5bd-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ac5bd-105">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)/[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) 是[中间件](xref:fundamentals/middleware/index)激活的扩展点。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-105">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)/[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) is an extensibility point for [middleware](xref:fundamentals/middleware/index) activation.</span></span>

<span data-ttu-id="ac5bd-106">`UseMiddleware` 扩展方法检查中间件的已注册类型是否实现 `IMiddleware`。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-106">`UseMiddleware` extension methods check if a middleware's registered type implements `IMiddleware`.</span></span> <span data-ttu-id="ac5bd-107">如果是，则使用在容器中注册的 `IMiddlewareFactory` 实例来解析 `IMiddleware` 实现，而不使用基于约定的中间件激活逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-107">If it does, the `IMiddlewareFactory` instance registered in the container is used to resolve the `IMiddleware` implementation instead of using the convention-based middleware activation logic.</span></span> <span data-ttu-id="ac5bd-108">中间件在应用的服务容器中注册为作用域或瞬态服务。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-108">The middleware is registered as a scoped or transient service in the app's service container.</span></span>

<span data-ttu-id="ac5bd-109">优点：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-109">Benefits:</span></span>

* <span data-ttu-id="ac5bd-110">按请求（作用域服务的注入）激活</span><span class="sxs-lookup"><span data-stu-id="ac5bd-110">Activation per request (injection of scoped services)</span></span>
* <span data-ttu-id="ac5bd-111">让中间件强类型化</span><span class="sxs-lookup"><span data-stu-id="ac5bd-111">Strong typing of middleware</span></span>

<span data-ttu-id="ac5bd-112">`IMiddleware` 按请求激活，因此作用域服务可以注入到中间件的构造函数中。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-112">`IMiddleware` is activated per request, so scoped services can be injected into the middleware's constructor.</span></span>

<span data-ttu-id="ac5bd-113">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="ac5bd-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="ac5bd-114">示例应用演示了使用以下两种方式激活的中间件：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-114">The sample app demonstrates middleware activated by:</span></span>

* <span data-ttu-id="ac5bd-115">约定。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-115">Convention.</span></span> <span data-ttu-id="ac5bd-116">有关使用约定激活中间件的详细信息，请参阅[中间件](xref:fundamentals/middleware/index)主题。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-116">For more information on conventional middleware activation, see the [Middleware](xref:fundamentals/middleware/index) topic.</span></span>
* <span data-ttu-id="ac5bd-117">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) 实现。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-117">An [IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) implementation.</span></span> <span data-ttu-id="ac5bd-118">默认的 [MiddlewareFactory 类](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory)可激活中间件。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-118">The default [MiddlewareFactory class](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory) activates the middleware.</span></span>

<span data-ttu-id="ac5bd-119">这两种中间件实现的功能相同，并能记录由查询字符串参数 (`key`) 提供的值。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-119">The middleware implementations function identically and record the value provided by a query string parameter (`key`).</span></span> <span data-ttu-id="ac5bd-120">中间件使用插入的数据库上下文（作用域服务）将查询字符串值记录在内存中数据库。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-120">The middlewares use an injected database context (a scoped service) to record the query string value in an in-memory database.</span></span>

## <a name="imiddleware"></a><span data-ttu-id="ac5bd-121">IMiddleware</span><span class="sxs-lookup"><span data-stu-id="ac5bd-121">IMiddleware</span></span>

<span data-ttu-id="ac5bd-122">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) 定义应用的请求管道的中间件。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-122">[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) defines middleware for the app's request pipeline.</span></span> <span data-ttu-id="ac5bd-123">[InvokeAsync(HttpContext, RequestDelegate)](/dotnet/api/microsoft.aspnetcore.http.imiddleware.invokeasync#Microsoft_AspNetCore_Http_IMiddleware_InvokeAsync_Microsoft_AspNetCore_Http_HttpContext_Microsoft_AspNetCore_Http_RequestDelegate_) 方法处理请求，并返回代表中间件执行的 `Task`。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-123">The [InvokeAsync(HttpContext, RequestDelegate)](/dotnet/api/microsoft.aspnetcore.http.imiddleware.invokeasync#Microsoft_AspNetCore_Http_IMiddleware_InvokeAsync_Microsoft_AspNetCore_Http_HttpContext_Microsoft_AspNetCore_Http_RequestDelegate_) method handles requests and returns a `Task` that represents the execution of the middleware.</span></span>

<span data-ttu-id="ac5bd-124">使用约定激活的中间件：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-124">Middleware activated by convention:</span></span>

[!code-csharp[](extensibility/sample/Middleware/ConventionalMiddleware.cs?name=snippet1)]

<span data-ttu-id="ac5bd-125">使用 `MiddlewareFactory` 激活的中间件：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-125">Middleware activated by `MiddlewareFactory`:</span></span>

[!code-csharp[](extensibility/sample/Middleware/FactoryActivatedMiddleware.cs?name=snippet1)]

<span data-ttu-id="ac5bd-126">程序会为中间件创建扩展：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-126">Extensions are created for the middlewares:</span></span>

[!code-csharp[](extensibility/sample/Middleware/MiddlewareExtensions.cs?name=snippet1)]

<span data-ttu-id="ac5bd-127">无法通过 `UseMiddleware` 将对象传递给工厂激活的中间件：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-127">It isn't possible to pass objects to the factory-activated middleware with `UseMiddleware`:</span></span>

```csharp
public static IApplicationBuilder UseFactoryActivatedMiddleware(
    this IApplicationBuilder builder, bool option)
{
    // Passing 'option' as an argument throws a NotSupportedException at runtime.
    return builder.UseMiddleware<FactoryActivatedMiddleware>(option);
}
```

<span data-ttu-id="ac5bd-128">将工厂激活的中间件添加到 *Startup.cs* 的内置容器中：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-128">The factory-activated middleware is added to the built-in container in *Startup.cs*:</span></span>

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet1&highlight=12)]

<span data-ttu-id="ac5bd-129">两个中间件均在 `Configure` 的请求处理管道中注册：</span><span class="sxs-lookup"><span data-stu-id="ac5bd-129">Both middlewares are registered in the request processing pipeline in `Configure`:</span></span>

[!code-csharp[](extensibility/sample/Startup.cs?name=snippet2&highlight=14-15)]

## <a name="imiddlewarefactory"></a><span data-ttu-id="ac5bd-130">IMiddlewareFactory</span><span class="sxs-lookup"><span data-stu-id="ac5bd-130">IMiddlewareFactory</span></span>

<span data-ttu-id="ac5bd-131">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) 提供中间件的创建方法。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-131">[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) provides methods to create middleware.</span></span> <span data-ttu-id="ac5bd-132">中间件工厂实现在容器中注册为作用域服务。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-132">The middleware factory implementation is registered in the container as a scoped service.</span></span>

<span data-ttu-id="ac5bd-133">可在 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 包中找到默认的 `IMiddlewareFactory` 实现（即 [MiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory)）。</span><span class="sxs-lookup"><span data-stu-id="ac5bd-133">The default `IMiddlewareFactory` implementation, [MiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.middlewarefactory), is found in the [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) package.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac5bd-134">其他资源</span><span class="sxs-lookup"><span data-stu-id="ac5bd-134">Additional resources</span></span>

* <xref:fundamentals/middleware/index>
* <xref:fundamentals/middleware/extensibility-third-party-container>
