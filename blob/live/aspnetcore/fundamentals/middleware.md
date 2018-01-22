---
title: "ASP.NET 核心中间件"
author: rick-anderson
description: "了解有关 ASP.NET 核心中间件和请求管道。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/middleware
ms.openlocfilehash: af16046c97964e8e1c16a4f5989fcfa794741c4d
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="aspnet-core-middleware-fundamentals"></a><span data-ttu-id="a0ab3-103">ASP.NET 核心中间件基础知识</span><span class="sxs-lookup"><span data-stu-id="a0ab3-103">ASP.NET Core Middleware Fundamentals</span></span>

<a name="fundamentals-middleware"></a>

<span data-ttu-id="a0ab3-104">通过[Rick Anderson](https://twitter.com/RickAndMSFT)和[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="a0ab3-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="a0ab3-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="a0ab3-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-middleware"></a><span data-ttu-id="a0ab3-106">什么是中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-106">What is middleware</span></span>

<span data-ttu-id="a0ab3-107">中间件是汇集到以处理请求和响应的一个应用程序管道的软件。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-107">Middleware is software that is assembled into an application pipeline to handle requests and responses.</span></span> <span data-ttu-id="a0ab3-108">每个组件：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-108">Each component:</span></span>

* <span data-ttu-id="a0ab3-109">可以选择是否要将请求传递到管道中的下一个组件。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-109">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="a0ab3-110">之前和之后调用管道中的下一个组件，可以执行工作。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-110">Can perform work before and after the next component in the pipeline is invoked.</span></span> 

<span data-ttu-id="a0ab3-111">使用请求委托来生成请求管道。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-111">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="a0ab3-112">请求委托处理每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-112">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="a0ab3-113">请求中使用委托来配置[运行](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions)，[映射](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)，和[使用](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)扩展方法。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-113">Request delegates are configured using [Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions), [Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions), and [Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions) extension methods.</span></span> <span data-ttu-id="a0ab3-114">一个单独的请求委托，它可将指定的在行作为匿名方法 （称为中，线中间件），或可以在可重用的类中定义它。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-114">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="a0ab3-115">这些可重用的类和行在匿名方法*中间件*，或*中间件组件*。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-115">These reusable classes and in-line anonymous methods are *middleware*, or *middleware components*.</span></span> <span data-ttu-id="a0ab3-116">在请求管道中的每个中间件组件负责调用管道中的下一个组件，或如果相应短路链。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-116">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline, or short-circuiting the chain if appropriate.</span></span>

<span data-ttu-id="a0ab3-117">[迁移到中间件的 HTTP 模块](../migration/http-modules.md)说明请求管道中 ASP.NET Core 和早期版本之间的差异，并提供更多的中间件示例。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-117">[Migrating HTTP Modules to Middleware](../migration/http-modules.md) explains the difference between request pipelines in ASP.NET Core and the previous versions and provides more middleware samples.</span></span>

## <a name="creating-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="a0ab3-118">使用 IApplicationBuilder 创建中间件管道</span><span class="sxs-lookup"><span data-stu-id="a0ab3-118">Creating a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="a0ab3-119">ASP.NET 核心请求管道由请求委托，调用一次是在另一个，如图所示 （执行如下所示的黑色箭头的线程） 的顺序组成：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-119">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other, as this diagram shows (the thread of execution follows the black arrows):</span></span>

![显示请求到达、 处理通过三个中间件，以及使应用程序的响应的请求处理模式。](middleware/_static/request-delegate-pipeline.png)

<span data-ttu-id="a0ab3-123">每个委托可以执行操作之前和之后的下一步的委托。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="a0ab3-124">委托还可以决定不将请求传递给下一步短路请求管道调用的委托。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-124">A delegate can also decide to not pass a request to the next delegate, which is called short-circuiting the request pipeline.</span></span> <span data-ttu-id="a0ab3-125">短路是通常需要的因为它避免不必要的工作。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="a0ab3-126">例如，静态文件中间件可以返回静态文件的请求和短路管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-126">For example, the static file middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="a0ab3-127">异常处理委托需要调用尽早在管道，因此它们可能会捕获更高版本管道阶段中发生的异常。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-127">Exception-handling delegates need to be called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="a0ab3-128">最简单可能的 ASP.NET Core 应用程序设置了处理所有请求的单个请求委托。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="a0ab3-129">这种情况下不包括实际请求管道。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="a0ab3-130">相反，单个的匿名函数中称为到每个 HTTP 请求的响应。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[Main](middleware/sample/Middleware/Startup.cs)]

<span data-ttu-id="a0ab3-131">第一个[应用。运行](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions)委托终止管道。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-131">The first [app.Run](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.runextensions) delegate terminates the pipeline.</span></span>

<span data-ttu-id="a0ab3-132">你可以链接多个请求委托连同[应用。使用](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions)。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-132">You can chain multiple request delegates together with [app.Use](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.useextensions).</span></span> <span data-ttu-id="a0ab3-133">`next`参数表示管道中的下一步委托。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="a0ab3-134">(请记住，则你可以绕过通过管道*不*调用*下一步*参数。)你可以通常执行操作之前和之后的下一步的委托，如本示例所示：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-134">(Remember that you can short-circuit the pipeline by *not* calling the *next* parameter.) You can typically perform actions both before and after the next delegate, as this example demonstrates:</span></span>

[!code-csharp[Main](middleware/sample/Chain/Startup.cs?name=snippet1)]

>[!WARNING]
> <span data-ttu-id="a0ab3-135">不要调用`next.Invoke`响应发送到客户端后。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-135">Do not call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="a0ab3-136">更改为`HttpResponse`响应启动后将引发异常。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-136">Changes to `HttpResponse` after the response has started will throw an exception.</span></span> <span data-ttu-id="a0ab3-137">例如，更改，例如设置标头、 状态代码等，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-137">For example, changes such as setting headers, status code, etc,  will throw an exception.</span></span> <span data-ttu-id="a0ab3-138">写入之后调用的响应正文`next`:</span><span class="sxs-lookup"><span data-stu-id="a0ab3-138">Writing to the response body after calling `next`:</span></span>
> - <span data-ttu-id="a0ab3-139">可能会导致违反协议。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-139">May cause a protocol violation.</span></span> <span data-ttu-id="a0ab3-140">例如，编写多个规定`content-length`。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-140">For example, writing more than the stated `content-length`.</span></span>
> - <span data-ttu-id="a0ab3-141">可能会损坏正文格式。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-141">May corrupt the body format.</span></span> <span data-ttu-id="a0ab3-142">例如，向 CSS 文件中写入一个 HTML 的页脚。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-142">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="a0ab3-143">[HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted)是一个有用的提示，以指示是否在发送标头和/或写入正文。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-143">[HttpResponse.HasStarted](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.features.httpresponsefeature#Microsoft_AspNetCore_Http_Features_HttpResponseFeature_HasStarted) is a useful hint to indicate if headers have been sent and/or the body has been written to.</span></span>

## <a name="ordering"></a><span data-ttu-id="a0ab3-144">订购</span><span class="sxs-lookup"><span data-stu-id="a0ab3-144">Ordering</span></span>

<span data-ttu-id="a0ab3-145">中间件组件将被添加中的顺序`Configure`方法定义在请求中，调用的顺序和响应相反的顺序。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-145">The order that middleware components are added in the `Configure` method defines the order in which they are invoked on requests, and the reverse order for the response.</span></span> <span data-ttu-id="a0ab3-146">此排序对于安全、 性能和功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-146">This ordering is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="a0ab3-147">Configure 方法 （如下所示） 将添加以下的中间件组件：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-147">The Configure method (shown below) adds the following middleware components:</span></span>

1. <span data-ttu-id="a0ab3-148">异常/错误处理</span><span class="sxs-lookup"><span data-stu-id="a0ab3-148">Exception/error handling</span></span>
2. <span data-ttu-id="a0ab3-149">静态文件服务器</span><span class="sxs-lookup"><span data-stu-id="a0ab3-149">Static file server</span></span>
3. <span data-ttu-id="a0ab3-150">身份验证</span><span class="sxs-lookup"><span data-stu-id="a0ab3-150">Authentication</span></span>
4. <span data-ttu-id="a0ab3-151">MVC</span><span class="sxs-lookup"><span data-stu-id="a0ab3-151">MVC</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a0ab3-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a0ab3-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


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

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a0ab3-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a0ab3-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

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

<span data-ttu-id="a0ab3-154">在上面的代码，`UseExceptionHandler`是添加到管道的第一个中间件组件-因此，它捕获在更高版本调用中发生的任何异常。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-154">In the code above, `UseExceptionHandler` is the first middleware component added to the pipeline—therefore, it catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="a0ab3-155">静态文件中间件称为尽早在管道中，因此它可以处理请求，而无需通过剩余组件短路。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-155">The static file middleware is called early in the pipeline so it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="a0ab3-156">静态文件中间件提供**没有**授权检查。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-156">The static file middleware provides **no** authorization checks.</span></span> <span data-ttu-id="a0ab3-157">由它提供任何文件包括正在*wwwroot*，可公开访问。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-157">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="a0ab3-158">请参阅[使用静态文件](xref:fundamentals/static-files)有关来保护静态文件的方法。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-158">See [Working with static files](xref:fundamentals/static-files) for an approach to secure static files.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a0ab3-159">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a0ab3-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)


<span data-ttu-id="a0ab3-160">如果请求未由静态文件中间件，它将传递给该标识中间件 (`app.UseAuthentication`)，这将执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-160">If the request is not handled by the static file middleware, it's passed on to the Identity middleware (`app.UseAuthentication`), which performs authentication.</span></span> <span data-ttu-id="a0ab3-161">标识不会短路未经身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-161">Identity does not short-circuit unauthenticated requests.</span></span> <span data-ttu-id="a0ab3-162">标识对请求进行身份验证，尽管仅后 MVC 选择特定 Razor 页或控制器和操作时，才会发生授权 （和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-162">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific Razor Page or controller and action.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a0ab3-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a0ab3-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="a0ab3-164">如果请求未由静态文件中间件，它将传递给该标识中间件 (`app.UseIdentity`)，这将执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-164">If the request is not handled by the static file middleware, it's passed on to the Identity middleware (`app.UseIdentity`), which performs authentication.</span></span> <span data-ttu-id="a0ab3-165">标识不会短路未经身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-165">Identity does not short-circuit unauthenticated requests.</span></span> <span data-ttu-id="a0ab3-166">标识对请求进行身份验证，尽管仅后 MVC 选择特定控制器和操作时，才会发生授权 （和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-166">Although Identity authenticates requests,  authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

-----------

<span data-ttu-id="a0ab3-167">下面的示例演示中间排序静态文件的请求将由前响应压缩中间件的静态文件中间件。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-167">The following example demonstrates a middleware ordering where requests for static files are handled by the static file middleware before the response compression middleware.</span></span> <span data-ttu-id="a0ab3-168">静态文件将不压缩此排序的中间件。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-168">Static files are not compressed with this ordering of the middleware.</span></span> <span data-ttu-id="a0ab3-169">从 MVC 响应[UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)可以压缩。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-169">The MVC responses from [UseMvcWithDefaultRoute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) can be compressed.</span></span>

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

### <a name="use-run-and-map"></a><span data-ttu-id="a0ab3-170">使用、 运行和映射</span><span class="sxs-lookup"><span data-stu-id="a0ab3-170">Use, Run, and Map</span></span>

<span data-ttu-id="a0ab3-171">配置 HTTP 管道使用`Use`， `Run`，和`Map`。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-171">You configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="a0ab3-172">`Use`方法则可以绕过管道 (即，如果它未调用`next`请求委托)。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-172">The `Use` method can short-circuit the pipeline (that is, if it does not call a `next` request delegate).</span></span> <span data-ttu-id="a0ab3-173">`Run`是一种约定，并且可能会使某些中间件组件`Run[Middleware]`管道结束时运行的方法。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-173">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="a0ab3-174">`Map*`扩展用作分支管道约定。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-174">`Map*` extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="a0ab3-175">[映射](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions)请求管道基于给定的请求路径的匹配项的分支。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-175">[Map](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapextensions) branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="a0ab3-176">如果请求路径开头的给定路径，则执行分支。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-176">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[Main](middleware/sample/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="a0ab3-177">下表显示的请求和响应从`http://localhost:1234`使用前面的代码：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-177">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="a0ab3-178">请求</span><span class="sxs-lookup"><span data-stu-id="a0ab3-178">Request</span></span> | <span data-ttu-id="a0ab3-179">响应</span><span class="sxs-lookup"><span data-stu-id="a0ab3-179">Response</span></span> |
| --- | --- |
| <span data-ttu-id="a0ab3-180">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="a0ab3-180">localhost:1234</span></span> | <span data-ttu-id="a0ab3-181">从非映射委托 hello。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-181">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="a0ab3-182">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="a0ab3-182">localhost:1234/map1</span></span> | <span data-ttu-id="a0ab3-183">测试 1 映射</span><span class="sxs-lookup"><span data-stu-id="a0ab3-183">Map Test 1</span></span> |
| <span data-ttu-id="a0ab3-184">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="a0ab3-184">localhost:1234/map2</span></span> | <span data-ttu-id="a0ab3-185">测试 2 映射</span><span class="sxs-lookup"><span data-stu-id="a0ab3-185">Map Test 2</span></span> |
| <span data-ttu-id="a0ab3-186">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="a0ab3-186">localhost:1234/map3</span></span> | <span data-ttu-id="a0ab3-187">从非映射委托 hello。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-187">Hello from non-Map delegate.</span></span>  |

<span data-ttu-id="a0ab3-188">当`Map`是使用，从删除匹配的路径段`HttpRequest.Path`和追加到`HttpRequest.PathBase`为每个请求。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-188">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="a0ab3-189">[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions)分支请求管道根据给定的谓词的结果。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-189">[MapWhen](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="a0ab3-190">类型的任何谓词`Func<HttpContext, bool>`可以用于将请求映射到管道的新分支。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-190">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="a0ab3-191">在下面的示例中，谓词使用查询字符串变量的状态进行检测`branch`:</span><span class="sxs-lookup"><span data-stu-id="a0ab3-191">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[Main](middleware/sample/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="a0ab3-192">下表显示的请求和响应从`http://localhost:1234`使用前面的代码：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-192">The following table shows the requests and responses from `http://localhost:1234` using the previous code:</span></span>

| <span data-ttu-id="a0ab3-193">请求</span><span class="sxs-lookup"><span data-stu-id="a0ab3-193">Request</span></span> | <span data-ttu-id="a0ab3-194">响应</span><span class="sxs-lookup"><span data-stu-id="a0ab3-194">Response</span></span> |
| --- | --- |
| <span data-ttu-id="a0ab3-195">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="a0ab3-195">localhost:1234</span></span> | <span data-ttu-id="a0ab3-196">从非映射委托 hello。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-196">Hello from non-Map delegate.</span></span>  |
| <span data-ttu-id="a0ab3-197">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="a0ab3-197">localhost:1234/?branch=master</span></span> | <span data-ttu-id="a0ab3-198">使用分支 = master</span><span class="sxs-lookup"><span data-stu-id="a0ab3-198">Branch used = master</span></span>|

<span data-ttu-id="a0ab3-199">`Map`支持嵌套，例如：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-199">`Map` supports nesting, for example:</span></span>

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

<span data-ttu-id="a0ab3-200">`Map`此外可以匹配多个段，例如：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-200">`Map` can also match multiple segments at once, for example:</span></span>

 ```csharp
app.Map("/level1/level2", HandleMultiSeg);
```

## <a name="built-in-middleware"></a><span data-ttu-id="a0ab3-201">内置的中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-201">Built-in middleware</span></span>

<span data-ttu-id="a0ab3-202">ASP.NET 核心附带以下的中间件组件：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-202">ASP.NET Core ships with the following middleware components:</span></span>

| <span data-ttu-id="a0ab3-203">中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-203">Middleware</span></span> | <span data-ttu-id="a0ab3-204">描述</span><span class="sxs-lookup"><span data-stu-id="a0ab3-204">Description</span></span> |
| ----- | ------- |
| [<span data-ttu-id="a0ab3-205">身份验证</span><span class="sxs-lookup"><span data-stu-id="a0ab3-205">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="a0ab3-206">提供的身份验证支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-206">Provides authentication support.</span></span> |
| [<span data-ttu-id="a0ab3-207">CORS</span><span class="sxs-lookup"><span data-stu-id="a0ab3-207">CORS</span></span>](xref:security/cors) | <span data-ttu-id="a0ab3-208">配置跨域资源共享。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-208">Configures Cross-Origin Resource Sharing.</span></span> |
| [<span data-ttu-id="a0ab3-209">响应缓存</span><span class="sxs-lookup"><span data-stu-id="a0ab3-209">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="a0ab3-210">提供对缓存响应支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-210">Provides support for caching responses.</span></span> |
| [<span data-ttu-id="a0ab3-211">响应压缩</span><span class="sxs-lookup"><span data-stu-id="a0ab3-211">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="a0ab3-212">提供用于压缩响应的支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-212">Provides support for compressing responses.</span></span> |
| [<span data-ttu-id="a0ab3-213">路由</span><span class="sxs-lookup"><span data-stu-id="a0ab3-213">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="a0ab3-214">定义和约束请求路由。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-214">Defines and constrains request routes.</span></span> |
| [<span data-ttu-id="a0ab3-215">会话</span><span class="sxs-lookup"><span data-stu-id="a0ab3-215">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="a0ab3-216">提供用于管理用户会话的支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-216">Provides support for managing user sessions.</span></span> |
| [<span data-ttu-id="a0ab3-217">静态文件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-217">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="a0ab3-218">为静态文件和目录浏览提供服务提供支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-218">Provides support for serving static files and directory browsing.</span></span> |
| [<span data-ttu-id="a0ab3-219">URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-219">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="a0ab3-220">用于重写 Url，并将请求重定向的支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-220">Provides support for rewriting URLs and redirecting requests.</span></span> |

<a name="middleware-writing-middleware"></a>

## <a name="writing-middleware"></a><span data-ttu-id="a0ab3-221">编写中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-221">Writing middleware</span></span>

<span data-ttu-id="a0ab3-222">通常，中间件是封装在一个类，并且通过扩展方法公开。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-222">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="a0ab3-223">请考虑以下中间件，它将为当前请求的区域性设置从查询字符串：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-223">Consider the following middleware, which sets the culture for the current request from the query string:</span></span>

[!code-csharp[Main](middleware/sample/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="a0ab3-224">注意： 上面的示例代码用于演示创建中间件组件。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-224">Note: The sample code above is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="a0ab3-225">请参阅[全球化和本地化](xref:fundamentals/localization)ASP.NET 核心内置的本地化支持。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-225">See [ Globalization and localization](xref:fundamentals/localization) for ASP.NET Core's built-in localization support.</span></span>

<span data-ttu-id="a0ab3-226">你可以通过例如传递区域性中测试该中间件`http://localhost:7997/?culture=no`。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-226">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="a0ab3-227">下面的代码将移动到的类的中间件委托：</span><span class="sxs-lookup"><span data-stu-id="a0ab3-227">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddleware.cs)]

<span data-ttu-id="a0ab3-228">下面的扩展方法公开通过中间件[IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder):</span><span class="sxs-lookup"><span data-stu-id="a0ab3-228">The following extension method exposes the middleware through [IApplicationBuilder](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.iapplicationbuilder):</span></span>

[!code-csharp[Main](middleware/sample/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="a0ab3-229">下面的代码调用从中间件`Configure`:</span><span class="sxs-lookup"><span data-stu-id="a0ab3-229">The following code calls the middleware from `Configure`:</span></span>

[!code-csharp[Main](middleware/sample/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="a0ab3-230">中间件应遵循[显式依赖关系原则](http://deviq.com/explicit-dependencies-principle/)通过公开其依赖项在其构造函数。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-230">Middleware should follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="a0ab3-231">每次构造中间件*应用程序生存期*。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-231">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="a0ab3-232">请参阅*每个请求的依赖关系*下面如果你需要与请求中的中间件共享服务。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-232">See *Per-request dependencies* below if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="a0ab3-233">中间件组件可以解决通过构造函数参数的依赖关系注入从其依赖关系。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-233">Middleware components can resolve their dependencies from dependency injection through constructor parameters.</span></span> <span data-ttu-id="a0ab3-234">[`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary)此外可以接受其他参数直接。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-234">[`UseMiddleware<T>`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.usemiddlewareextensions#methods_summary) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="a0ab3-235">每个请求的依赖关系</span><span class="sxs-lookup"><span data-stu-id="a0ab3-235">Per-request dependencies</span></span>

<span data-ttu-id="a0ab3-236">中间件构造在应用启动时，不根据请求，因为*范围*生存期服务使用的中间件构造函数不能与其他依赖关系注入类型共享在每个请求过程。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-236">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors are not  shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="a0ab3-237">如果必须共享*范围*服务中间件和其他类型之间，添加到这些服务`Invoke`方法的签名。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-237">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="a0ab3-238">`Invoke`方法可以接受由依赖关系注入填充的附加参数。</span><span class="sxs-lookup"><span data-stu-id="a0ab3-238">The `Invoke` method can accept additional parameters that are populated by dependency injection.</span></span> <span data-ttu-id="a0ab3-239">例如:</span><span class="sxs-lookup"><span data-stu-id="a0ab3-239">For example:</span></span>

```c#
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

## <a name="resources"></a><span data-ttu-id="a0ab3-240">资源</span><span class="sxs-lookup"><span data-stu-id="a0ab3-240">Resources</span></span>

* [<span data-ttu-id="a0ab3-241">在本文档中使用的示例代码</span><span class="sxs-lookup"><span data-stu-id="a0ab3-241">Sample code used in this doc</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/sample)
* [<span data-ttu-id="a0ab3-242">将 HTTP 模块迁移到中间件</span><span class="sxs-lookup"><span data-stu-id="a0ab3-242">Migrating HTTP Modules to Middleware</span></span>](../migration/http-modules.md)
* [<span data-ttu-id="a0ab3-243">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="a0ab3-243">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="a0ab3-244">请求功能</span><span class="sxs-lookup"><span data-stu-id="a0ab3-244">Request Features</span></span>](request-features.md)
