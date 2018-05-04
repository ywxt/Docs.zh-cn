---
title: ASP.NET Core 中间件
author: rick-anderson
description: 了解 ASP.NET Core 中间件和请求管道。
manager: wpickett
ms.author: riande
ms.date: 01/22/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/middleware/index
ms.openlocfilehash: 4c44063fb3385fc625c35c8a3cf06a35b5b0afb7
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="33fd8-103">ASP.NET Core 中间件</span><span class="sxs-lookup"><span data-stu-id="33fd8-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="33fd8-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="33fd8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="33fd8-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="33fd8-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-middleware"></a><span data-ttu-id="33fd8-106">什么是中间件？</span><span class="sxs-lookup"><span data-stu-id="33fd8-106">What is middleware?</span></span>

<span data-ttu-id="33fd8-107">中间件是一种装配到应用程序管道以处理请求和响应的软件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-107">Middleware is software that's assembled into an application pipeline to handle requests and responses.</span></span> <span data-ttu-id="33fd8-108">每个组件：</span><span class="sxs-lookup"><span data-stu-id="33fd8-108">Each component:</span></span>

* <span data-ttu-id="33fd8-109">选择是否将请求传递到管道中的下一个组件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-109">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="33fd8-110">可在调用管道中的下一个组件前后执行工作。</span><span class="sxs-lookup"><span data-stu-id="33fd8-110">Can perform work before and after the next component in the pipeline is invoked.</span></span> 

<span data-ttu-id="33fd8-111">请求委托用于生成请求管道。</span><span class="sxs-lookup"><span data-stu-id="33fd8-111">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="33fd8-112">请求委托处理每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="33fd8-112">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="33fd8-113">使用 [Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions)、[Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions) 和 [Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions) 扩展方法来配置请求委托。</span><span class="sxs-lookup"><span data-stu-id="33fd8-113">Request delegates are configured using [Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions), [Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions), and [Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions) extension methods.</span></span> <span data-ttu-id="33fd8-114">可将一个单独的请求委托并行指定为匿名方法（称为并行中间件），或在可重用的类中对其进行定义。</span><span class="sxs-lookup"><span data-stu-id="33fd8-114">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="33fd8-115">这些可重用的类和并行匿名方法即为中间件或中间件组件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-115">These reusable classes and in-line anonymous methods are *middleware*, or *middleware components*.</span></span> <span data-ttu-id="33fd8-116">请求管道中的每个中间件组件负责调用管道中的下一个组件，或在适当情况下使链发生短路。</span><span class="sxs-lookup"><span data-stu-id="33fd8-116">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline, or short-circuiting the chain if appropriate.</span></span>

<span data-ttu-id="33fd8-117">[将 HTTP 模块迁移到中间件](xref:migration/http-modules)介绍了 ASP.NET Core 和 ASP.NET 4.x 中请求管道之间的差异，并提供了更多的中间件示例。</span><span class="sxs-lookup"><span data-stu-id="33fd8-117">[Migrate HTTP Modules to Middleware](xref:migration/http-modules) explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="33fd8-118">使用 IApplicationBuilder 创建中间件管道</span><span class="sxs-lookup"><span data-stu-id="33fd8-118">Creating a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="33fd8-119">ASP.NET Core 请求管道包含一系列相继调用的请求委托，如下图所示（执行过程遵循黑色箭头）：</span><span class="sxs-lookup"><span data-stu-id="33fd8-119">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other, as this diagram shows (the thread of execution follows the black arrows):</span></span>

![请求处理模式显示请求到达、通过三个中间件进行处理以及响应离开应用程序。](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="33fd8-123">每个委托均可在下一个委托前后执行操作。</span><span class="sxs-lookup"><span data-stu-id="33fd8-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="33fd8-124">此外，委托还可以决定不将请求传递给下一个委托，这就是对请求管道进行短路。</span><span class="sxs-lookup"><span data-stu-id="33fd8-124">A delegate can also decide to not pass a request to the next delegate, which is called short-circuiting the request pipeline.</span></span> <span data-ttu-id="33fd8-125">通常需要短路，因为这样可以避免不必要的工作。</span><span class="sxs-lookup"><span data-stu-id="33fd8-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="33fd8-126">例如，静态文件中间件可以返回静态文件请求并使管道的其余部分短路。</span><span class="sxs-lookup"><span data-stu-id="33fd8-126">For example, the static file middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="33fd8-127">需要尽早在管道中调用异常处理委托，以便它们可以捕获在管道的后期阶段所发生的异常。</span><span class="sxs-lookup"><span data-stu-id="33fd8-127">Exception-handling delegates need to be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="33fd8-128">尽可能简单的 ASP.NET Core 应用设置了处理所有请求的单个请求委托。</span><span class="sxs-lookup"><span data-stu-id="33fd8-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="33fd8-129">这种情况不包括实际请求管道。</span><span class="sxs-lookup"><span data-stu-id="33fd8-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="33fd8-130">调用单个匿名函数以响应每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="33fd8-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/sample/Middleware/Startup.cs)]

<span data-ttu-id="33fd8-131">第一个 [app.Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions) 委托终止了管道。</span><span class="sxs-lookup"><span data-stu-id="33fd8-131">The first [app.Run](/dotnet/api/microsoft.aspnetcore.builder.runextensions) delegate terminates the pipeline.</span></span>

<span data-ttu-id="33fd8-132">可使用 [app.Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions) 将多个请求委托链接在一起。</span><span class="sxs-lookup"><span data-stu-id="33fd8-132">You can chain multiple request delegates together with [app.Use](/dotnet/api/microsoft.aspnetcore.builder.useextensions).</span></span> <span data-ttu-id="33fd8-133">`next` 参数表示管道中的下一个委托。</span><span class="sxs-lookup"><span data-stu-id="33fd8-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="33fd8-134">（请记住，可通过不调用 next 参数使管道短路。）通常可在下一个委托前后执行操作，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="33fd8-134">(Remember that you can short-circuit the pipeline by *not* calling the *next* parameter.) You can typically perform actions both before and after the next delegate, as this example demonstrates:</span></span>

[!code-csharp[](index/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> <span data-ttu-id="33fd8-135">在向客户端发送响应后，请勿调用 `next.Invoke`。</span><span class="sxs-lookup"><span data-stu-id="33fd8-135">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="33fd8-136">响应启动后，针对 `HttpResponse` 的更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="33fd8-136">Changes to `HttpResponse` after the response has started will throw an exception.</span></span> <span data-ttu-id="33fd8-137">例如，设置标头、状态代码等更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="33fd8-137">For example, changes such as setting headers, status code, etc,  will throw an exception.</span></span> <span data-ttu-id="33fd8-138">调用 `next` 后写入响应正文：</span><span class="sxs-lookup"><span data-stu-id="33fd8-138">Writing to the response body after calling `next`:</span></span>
> - <span data-ttu-id="33fd8-139">可能导致违反协议。</span><span class="sxs-lookup"><span data-stu-id="33fd8-139">May cause a protocol violation.</span></span> <span data-ttu-id="33fd8-140">例如，写入的长度超过规定的 `content-length`。</span><span class="sxs-lookup"><span data-stu-id="33fd8-140">For example, writing more than the stated `content-length`.</span></span>
> - <span data-ttu-id="33fd8-141">可能损坏正文格式。</span><span class="sxs-lookup"><span data-stu-id="33fd8-141">May corrupt the body format.</span></span> <span data-ttu-id="33fd8-142">例如，向 CSS 文件中写入 HTML 页脚。</span><span class="sxs-lookup"><span data-stu-id="33fd8-142">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="33fd8-143">[HttpResponse.HasStarted](/dotnet/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted) 是一个有用的提示，指示是否已发送标头和/或已写入正文。</span><span class="sxs-lookup"><span data-stu-id="33fd8-143">[HttpResponse.HasStarted](/dotnet/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted) is a useful hint to indicate if headers have been sent and/or the body has been written to.</span></span>

## <a name="ordering"></a><span data-ttu-id="33fd8-144">中间件排序</span><span class="sxs-lookup"><span data-stu-id="33fd8-144">Ordering</span></span>

<span data-ttu-id="33fd8-145">向 `Configure` 方法添加中间件组件的顺序定义了针对请求调用这些组件的顺序，以及响应的相反顺序。</span><span class="sxs-lookup"><span data-stu-id="33fd8-145">The order that middleware components are added in the `Configure` method defines the order in which they're invoked on requests, and the reverse order for the response.</span></span> <span data-ttu-id="33fd8-146">此排序对于安全性、性能和功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="33fd8-146">This ordering is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="33fd8-147">Configure 方法（如下所示）添加以下中间件组件：</span><span class="sxs-lookup"><span data-stu-id="33fd8-147">The Configure method (shown below) adds the following middleware components:</span></span>

1. <span data-ttu-id="33fd8-148">异常/错误处理</span><span class="sxs-lookup"><span data-stu-id="33fd8-148">Exception/error handling</span></span>
2. <span data-ttu-id="33fd8-149">静态文件服务器</span><span class="sxs-lookup"><span data-stu-id="33fd8-149">Static file server</span></span>
3. <span data-ttu-id="33fd8-150">身份验证</span><span class="sxs-lookup"><span data-stu-id="33fd8-150">Authentication</span></span>
4. <span data-ttu-id="33fd8-151">MVC</span><span class="sxs-lookup"><span data-stu-id="33fd8-151">MVC</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="33fd8-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="33fd8-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseAuthentication();               // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="33fd8-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="33fd8-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseExceptionHandler("/Home/Error"); // Call first to catch exceptions
                                            // thrown in the following middleware.

    app.UseStaticFiles();                   // Return static files and end pipeline.

    app.UseIdentity();                     // Authenticate before you access
                                           // secure resources.

    app.UseMvcWithDefaultRoute();          // Add MVC to the request pipeline.
}
```

-----------

<span data-ttu-id="33fd8-154">在以上代码中，`UseExceptionHandler` 是添加到管道的第一个中间件组件，因此，该组件可捕获在后面的调用中发生的任何异常。</span><span class="sxs-lookup"><span data-stu-id="33fd8-154">In the code above, `UseExceptionHandler` is the first middleware component added to the pipeline—therefore, it catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="33fd8-155">因为尽早在管道中调用静态文件中间件，因此该组件可处理请求并使引致短路，而无需通过剩余组件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-155">The static file middleware is called early in the pipeline so it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="33fd8-156">静态文件中间件不提供授权检查。</span><span class="sxs-lookup"><span data-stu-id="33fd8-156">The static file middleware provides **no** authorization checks.</span></span> <span data-ttu-id="33fd8-157">可公开访问由静态文件中间件服务的任何文件，包括 wwwroot 下的文件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-157">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="33fd8-158">请参阅[使用静态文件](xref:fundamentals/static-files)获取有关保护静态文件的方法。</span><span class="sxs-lookup"><span data-stu-id="33fd8-158">See [Work with static files](xref:fundamentals/static-files) for an approach to secure static files.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="33fd8-159">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="33fd8-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


<span data-ttu-id="33fd8-160">如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的标识中间件 (`app.UseAuthentication`)。</span><span class="sxs-lookup"><span data-stu-id="33fd8-160">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseAuthentication`), which performs authentication.</span></span> <span data-ttu-id="33fd8-161">标识不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="33fd8-161">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="33fd8-162">虽然标识对请求进行身份验证，但仅在 MVC 选择特定 Razor 页或控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="33fd8-162">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific Razor Page or controller and action.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="33fd8-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="33fd8-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="33fd8-164">如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的标识中间件 (`app.UseIdentity`)。</span><span class="sxs-lookup"><span data-stu-id="33fd8-164">If the request isn't handled by the static file middleware, it's passed on to the Identity middleware (`app.UseIdentity`), which performs authentication.</span></span> <span data-ttu-id="33fd8-165">标识不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="33fd8-165">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="33fd8-166">虽然标识对请求进行身份验证，但仅在 MVC 选择特定控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="33fd8-166">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

-----------

<span data-ttu-id="33fd8-167">以下示例演示中间件排序，其中静态文件的请求在响应压缩中间件前由静态文件中间件进行处理。</span><span class="sxs-lookup"><span data-stu-id="33fd8-167">The following example demonstrates a middleware ordering where requests for static files are handled by the static file middleware before the response compression middleware.</span></span> <span data-ttu-id="33fd8-168">静态文件未通过此中间件排序进行压缩。</span><span class="sxs-lookup"><span data-stu-id="33fd8-168">Static files are not compressed with this ordering of the middleware.</span></span> <span data-ttu-id="33fd8-169">可压缩来自 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 的 MVC 响应。</span><span class="sxs-lookup"><span data-stu-id="33fd8-169">The MVC responses from [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseStaticFiles();         // Static files not compressed
                                  // by middleware.
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

<a name="middleware-run-map-use"></a>

### <a name="use-run-and-map"></a><span data-ttu-id="33fd8-170">Use、Run 和 Map</span><span class="sxs-lookup"><span data-stu-id="33fd8-170">Use, Run, and Map</span></span>

<span data-ttu-id="33fd8-171">使用 `Use`、`Run` 和 `Map` 配置 HTTP 管道。</span><span class="sxs-lookup"><span data-stu-id="33fd8-171">You configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="33fd8-172">`Use` 方法可使管道短路（即不调用 `next` 请求委托）。</span><span class="sxs-lookup"><span data-stu-id="33fd8-172">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="33fd8-173">`Run` 是一种约定，并且某些中间件组件可公开在管道末尾运行的 `Run[Middleware]` 方法。</span><span class="sxs-lookup"><span data-stu-id="33fd8-173">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="33fd8-174">`Map*` 扩展用作约定来创建管道分支。</span><span class="sxs-lookup"><span data-stu-id="33fd8-174">`Map*` extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="33fd8-175">[Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions) 基于给定请求路径的匹配项来创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="33fd8-175">[Map](/dotnet/api/microsoft.aspnetcore.builder.mapextensions) branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="33fd8-176">如果请求路径以给定路径开头，则执行分支。</span><span class="sxs-lookup"><span data-stu-id="33fd8-176">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/sample/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="33fd8-177">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应：</span><span class="sxs-lookup"><span data-stu-id="33fd8-177">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="33fd8-178">请求</span><span class="sxs-lookup"><span data-stu-id="33fd8-178">Request</span></span> | <span data-ttu-id="33fd8-179">响应</span><span class="sxs-lookup"><span data-stu-id="33fd8-179">Response</span></span> |
| --- | --- |
| <span data-ttu-id="33fd8-180">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="33fd8-180">localhost:1234</span></span> | <span data-ttu-id="33fd8-181">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="33fd8-181">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="33fd8-182">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="33fd8-182">localhost:1234/map1</span></span> | <span data-ttu-id="33fd8-183">Map 测试 1</span><span class="sxs-lookup"><span data-stu-id="33fd8-183">Map Test 1</span></span> |
| <span data-ttu-id="33fd8-184">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="33fd8-184">localhost:1234/map2</span></span> | <span data-ttu-id="33fd8-185">Map 测试 2</span><span class="sxs-lookup"><span data-stu-id="33fd8-185">Map Test 2</span></span> |
| <span data-ttu-id="33fd8-186">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="33fd8-186">localhost:1234/map3</span></span> | <span data-ttu-id="33fd8-187">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="33fd8-187">Hello from non-Map delegate.</span></span>  |

<span data-ttu-id="33fd8-188">使用 `Map` 时，将从 `HttpRequest.Path` 中删除匹配的线段，并针对每个请求将该线段追加到 `HttpRequest.PathBase`。</span><span class="sxs-lookup"><span data-stu-id="33fd8-188">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="33fd8-189">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) 基于给定谓词的结果创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="33fd8-189">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="33fd8-190">`Func<HttpContext, bool>` 类型的任何谓词均可用于将请求映射到管道的新分支。</span><span class="sxs-lookup"><span data-stu-id="33fd8-190">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="33fd8-191">在以下示例中，谓词用于检测查询字符串变量 `branch` 是否存在：</span><span class="sxs-lookup"><span data-stu-id="33fd8-191">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/sample/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="33fd8-192">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应：</span><span class="sxs-lookup"><span data-stu-id="33fd8-192">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="33fd8-193">请求</span><span class="sxs-lookup"><span data-stu-id="33fd8-193">Request</span></span> | <span data-ttu-id="33fd8-194">响应</span><span class="sxs-lookup"><span data-stu-id="33fd8-194">Response</span></span> |
| --- | --- |
| <span data-ttu-id="33fd8-195">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="33fd8-195">localhost:1234</span></span> | <span data-ttu-id="33fd8-196">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="33fd8-196">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="33fd8-197">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="33fd8-197">localhost:1234/?branch=master</span></span> | <span data-ttu-id="33fd8-198">使用的分支 = 主要分支</span><span class="sxs-lookup"><span data-stu-id="33fd8-198">Branch used = master</span></span>|

<span data-ttu-id="33fd8-199">`Map` 支持嵌套，例如：</span><span class="sxs-lookup"><span data-stu-id="33fd8-199">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
       level1App.Map("/level2a", level2AApp => {
           // "/level1/level2a"
           //...
       });
       level1App.Map("/level2b", level2BApp => {
           // "/level1/level2b"
           //...
       });
   });
   ```

<span data-ttu-id="33fd8-200">此外，`Map` 还可同时匹配多个段，例如：</span><span class="sxs-lookup"><span data-stu-id="33fd8-200">`Map` can also match multiple segments at once, for example:</span></span>

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a><span data-ttu-id="33fd8-201">内置中间件</span><span class="sxs-lookup"><span data-stu-id="33fd8-201">Built-in middleware</span></span>

<span data-ttu-id="33fd8-202">ASP.NET Core 附带以下中间件组件，以及用于添加这些组件的顺序的说明：</span><span class="sxs-lookup"><span data-stu-id="33fd8-202">ASP.NET Core ships with the following middleware components, as well as a description of the order in which they should be added:</span></span>

| <span data-ttu-id="33fd8-203">中间件</span><span class="sxs-lookup"><span data-stu-id="33fd8-203">Middleware</span></span> | <span data-ttu-id="33fd8-204">描述</span><span class="sxs-lookup"><span data-stu-id="33fd8-204">Description</span></span> | <span data-ttu-id="33fd8-205">顺序</span><span class="sxs-lookup"><span data-stu-id="33fd8-205">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="33fd8-206">身份验证</span><span class="sxs-lookup"><span data-stu-id="33fd8-206">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="33fd8-207">提供身份验证支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-207">Provides authentication support.</span></span> | <span data-ttu-id="33fd8-208">在需要 `HttpContext.User` 之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-208">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="33fd8-209">OAuth 回叫的终端。</span><span class="sxs-lookup"><span data-stu-id="33fd8-209">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="33fd8-210">CORS</span><span class="sxs-lookup"><span data-stu-id="33fd8-210">CORS</span></span>](xref:security/cors) | <span data-ttu-id="33fd8-211">配置跨域资源共享。</span><span class="sxs-lookup"><span data-stu-id="33fd8-211">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="33fd8-212">在使用 CORS 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-212">Before components that use CORS.</span></span> |
| [<span data-ttu-id="33fd8-213">诊断</span><span class="sxs-lookup"><span data-stu-id="33fd8-213">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="33fd8-214">配置诊断。</span><span class="sxs-lookup"><span data-stu-id="33fd8-214">Configures diagnostics.</span></span> | <span data-ttu-id="33fd8-215">在生成错误的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-215">Before components that generate errors.</span></span> |
| [<span data-ttu-id="33fd8-216">ForwardedHeaders/HttpOverrides</span><span class="sxs-lookup"><span data-stu-id="33fd8-216">ForwardedHeaders/HttpOverrides</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="33fd8-217">将代理标头转发到当前请求。</span><span class="sxs-lookup"><span data-stu-id="33fd8-217">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="33fd8-218">在使用更新的字段（示例：Scheme、Host、ClientIP、Method）的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-218">Before components that consume the updated fields (examples: Scheme, Host, ClientIP, Method).</span></span> |
| [<span data-ttu-id="33fd8-219">响应缓存</span><span class="sxs-lookup"><span data-stu-id="33fd8-219">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="33fd8-220">提供对缓存响应的支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-220">Provides support for caching responses.</span></span> | <span data-ttu-id="33fd8-221">在需要缓存的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-221">Before components that require caching.</span></span> |
| [<span data-ttu-id="33fd8-222">响应压缩</span><span class="sxs-lookup"><span data-stu-id="33fd8-222">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="33fd8-223">提供对压缩响应的支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-223">Provides support for compressing responses.</span></span> | <span data-ttu-id="33fd8-224">在需要压缩的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-224">Before components that require compression.</span></span> |
| [<span data-ttu-id="33fd8-225">RequestLocalization</span><span class="sxs-lookup"><span data-stu-id="33fd8-225">RequestLocalization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="33fd8-226">提供本地化支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-226">Provides localization support.</span></span> | <span data-ttu-id="33fd8-227">在对本地化敏感的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-227">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="33fd8-228">路由</span><span class="sxs-lookup"><span data-stu-id="33fd8-228">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="33fd8-229">定义和约束请求路由。</span><span class="sxs-lookup"><span data-stu-id="33fd8-229">Defines and constrains request routes.</span></span> | <span data-ttu-id="33fd8-230">用于匹配路由的终端。</span><span class="sxs-lookup"><span data-stu-id="33fd8-230">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="33fd8-231">会话</span><span class="sxs-lookup"><span data-stu-id="33fd8-231">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="33fd8-232">提供对管理用户会话的支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-232">Provides support for managing user sessions.</span></span> | <span data-ttu-id="33fd8-233">在需要会话的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-233">Before components that require Session.</span></span> |
| [<span data-ttu-id="33fd8-234">静态文件</span><span class="sxs-lookup"><span data-stu-id="33fd8-234">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="33fd8-235">为提供静态文件和目录浏览提供支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-235">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="33fd8-236">如果请求与文件匹配，则为终端。</span><span class="sxs-lookup"><span data-stu-id="33fd8-236">Terminal if a request matches files.</span></span> |
| [<span data-ttu-id="33fd8-237">URL 重写</span><span class="sxs-lookup"><span data-stu-id="33fd8-237">URL Rewriting </span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="33fd8-238">提供对重写 URL 和重定向请求的支持。</span><span class="sxs-lookup"><span data-stu-id="33fd8-238">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="33fd8-239">在使用 URL 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-239">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="33fd8-240">WebSockets</span><span class="sxs-lookup"><span data-stu-id="33fd8-240">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="33fd8-241">启用 WebSockets 协议。</span><span class="sxs-lookup"><span data-stu-id="33fd8-241">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="33fd8-242">在接受 WebSocket 请求所需的组件之前。</span><span class="sxs-lookup"><span data-stu-id="33fd8-242">Before components that are required to accept WebSocket requests.</span></span> |

<a name="middleware-writing-middleware"></a>

## <a name="writing-middleware"></a><span data-ttu-id="33fd8-243">写入中间件</span><span class="sxs-lookup"><span data-stu-id="33fd8-243">Writing middleware</span></span>

<span data-ttu-id="33fd8-244">通常，中间件封装在类中，并且通过扩展方法公开。</span><span class="sxs-lookup"><span data-stu-id="33fd8-244">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="33fd8-245">请考虑以下中间件，该中间件通过查询字符串设置当前请求的区域性：</span><span class="sxs-lookup"><span data-stu-id="33fd8-245">Consider the following middleware, which sets the culture for the current request from the query string:</span></span>

[!code-csharp[](index/sample/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="33fd8-246">注意：以上示例代码用于演示创建中间件组件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-246">Note: The sample code above is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="33fd8-247">有关 ASP.NET Core 的内置本地化支持，请参阅[全球化和本地化](xref:fundamentals/localization)。</span><span class="sxs-lookup"><span data-stu-id="33fd8-247">See [ Globalization and localization](xref:fundamentals/localization) for ASP.NET Core's built-in localization support.</span></span>

<span data-ttu-id="33fd8-248">可通过传入区域性（如 `http://localhost:7997/?culture=no`）测试中间件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-248">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="33fd8-249">以下代码将中间件委托移动到类：</span><span class="sxs-lookup"><span data-stu-id="33fd8-249">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/sample/Culture/RequestCultureMiddleware.cs)]

> [!NOTE]
> <span data-ttu-id="33fd8-250">在 ASP.NET Core 1.x 中，中间件 `Task` 方法的名称必须是 `Invoke`。</span><span class="sxs-lookup"><span data-stu-id="33fd8-250">In ASP.NET Core 1.x, the middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="33fd8-251">在 ASP.NET Core 2.0 或更高版本中，该名称可以为 `Invoke` 或 `InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="33fd8-251">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

<span data-ttu-id="33fd8-252">以下扩展方法通过 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) 公开中间件：</span><span class="sxs-lookup"><span data-stu-id="33fd8-252">The following extension method exposes the middleware through [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder):</span></span>

[!code-csharp[](index/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="33fd8-253">以下代码通过 `Configure` 调用中间件：</span><span class="sxs-lookup"><span data-stu-id="33fd8-253">The following code calls the middleware from `Configure`:</span></span>

[!code-csharp[](index/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="33fd8-254">中间件应通过在其构造函数中公开其依赖项来遵循[显式依赖项原则](http://deviq.com/explicit-dependencies-principle/)。</span><span class="sxs-lookup"><span data-stu-id="33fd8-254">Middleware should follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="33fd8-255">在每个应用程序生存期构造一次中间件。</span><span class="sxs-lookup"><span data-stu-id="33fd8-255">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="33fd8-256">如果需要与请求中的中间件共享服务，请参阅下面讲述的按请求依赖项。</span><span class="sxs-lookup"><span data-stu-id="33fd8-256">See *Per-request dependencies* below if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="33fd8-257">中间件组件可通过构造函数参数从依赖关系注入解析其依赖项。</span><span class="sxs-lookup"><span data-stu-id="33fd8-257">Middleware components can resolve their dependencies from dependency injection through constructor parameters.</span></span> <span data-ttu-id="33fd8-258">此外，[`UseMiddleware<T>`](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary) 还可直接接受其他参数。</span><span class="sxs-lookup"><span data-stu-id="33fd8-258">[`UseMiddleware<T>`](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="33fd8-259">按请求依赖项</span><span class="sxs-lookup"><span data-stu-id="33fd8-259">Per-request dependencies</span></span>

<span data-ttu-id="33fd8-260">由于中间件是在应用启动时构造的，而不是按请求构造的，因此在每个请求过程中，中间件构造函数使用的范围内生存期服务不与其他依赖关系注入类型共享。</span><span class="sxs-lookup"><span data-stu-id="33fd8-260">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors are not  shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="33fd8-261">如果必须在中间件和其他类型之间共享范围内服务，请将这些服务添加到 `Invoke` 方法的签名。</span><span class="sxs-lookup"><span data-stu-id="33fd8-261">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="33fd8-262">`Invoke` 方法可接受由依赖关系注入填充的其他参数。</span><span class="sxs-lookup"><span data-stu-id="33fd8-262">The `Invoke` method can accept additional parameters that are populated by dependency injection.</span></span> <span data-ttu-id="33fd8-263">例如:</span><span class="sxs-lookup"><span data-stu-id="33fd8-263">For example:</span></span>

```csharp
public class MyMiddleware
{
    private readonly RequestDelegate _next;

    public MyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="33fd8-264">其他资源</span><span class="sxs-lookup"><span data-stu-id="33fd8-264">Additional resources</span></span>

* [<span data-ttu-id="33fd8-265">将 HTTP 模块迁移到中间件</span><span class="sxs-lookup"><span data-stu-id="33fd8-265">Migrate HTTP Modules to Middleware</span></span>](xref:migration/http-modules)
* [<span data-ttu-id="33fd8-266">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="33fd8-266">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="33fd8-267">请求功能</span><span class="sxs-lookup"><span data-stu-id="33fd8-267">Request Features</span></span>](xref:fundamentals/request-features)
* [<span data-ttu-id="33fd8-268">基于工厂的中间件激活</span><span class="sxs-lookup"><span data-stu-id="33fd8-268">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
* [<span data-ttu-id="33fd8-269">第三方容器中的中间件激活</span><span class="sxs-lookup"><span data-stu-id="33fd8-269">Middleware activation with a third-party container</span></span>](xref:fundamentals/middleware/extensibility-third-party-container)
