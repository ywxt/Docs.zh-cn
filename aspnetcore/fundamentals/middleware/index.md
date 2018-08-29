---
title: ASP.NET Core 中间件
author: rick-anderson
description: 了解 ASP.NET Core 中间件和请求管道。
ms.author: riande
ms.custom: mvc
ms.date: 08/21/2018
uid: fundamentals/middleware/index
ms.openlocfilehash: e6dc76b7cb80e0dfda102df5aefb5d9ce9b821ed
ms.sourcegitcommit: 847cc1de5526ff42a7303491e6336c2dbdb45de4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43055801"
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="67697-103">ASP.NET Core 中间件</span><span class="sxs-lookup"><span data-stu-id="67697-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="67697-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="67697-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="67697-105">中间件是一种装配到应用管道以处理请求和响应的软件。</span><span class="sxs-lookup"><span data-stu-id="67697-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="67697-106">每个组件：</span><span class="sxs-lookup"><span data-stu-id="67697-106">Each component:</span></span>

* <span data-ttu-id="67697-107">选择是否将请求传递到管道中的下一个组件。</span><span class="sxs-lookup"><span data-stu-id="67697-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="67697-108">可在调用管道中的下一个组件前后执行工作。</span><span class="sxs-lookup"><span data-stu-id="67697-108">Can perform work before and after the next component in the pipeline is invoked.</span></span>

<span data-ttu-id="67697-109">请求委托用于生成请求管道。</span><span class="sxs-lookup"><span data-stu-id="67697-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="67697-110">请求委托处理每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="67697-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="67697-111">使用 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 和 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 扩展方法来配置请求委托。</span><span class="sxs-lookup"><span data-stu-id="67697-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="67697-112">可将一个单独的请求委托并行指定为匿名方法（称为并行中间件），或在可重用的类中对其进行定义。</span><span class="sxs-lookup"><span data-stu-id="67697-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="67697-113">这些可重用的类和并行匿名方法即为中间件，也叫中间件组件。</span><span class="sxs-lookup"><span data-stu-id="67697-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="67697-114">请求管道中的每个中间件组件负责调用管道中的下一个组件，或使管道短路。</span><span class="sxs-lookup"><span data-stu-id="67697-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span>

<span data-ttu-id="67697-115"><xref:migration/http-modules> 介绍了 ASP.NET Core 和 ASP.NET 4.x 中请求管道之间的差异，并提供了更多的中间件示例。</span><span class="sxs-lookup"><span data-stu-id="67697-115"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="67697-116">使用 IApplicationBuilder 创建中间件管道</span><span class="sxs-lookup"><span data-stu-id="67697-116">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="67697-117">ASP.NET Core 请求管道包含一系列请求委托，依次调用。</span><span class="sxs-lookup"><span data-stu-id="67697-117">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="67697-118">下图演示了这一概念。</span><span class="sxs-lookup"><span data-stu-id="67697-118">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="67697-119">沿黑色箭头执行。</span><span class="sxs-lookup"><span data-stu-id="67697-119">The thread of execution follows the black arrows.</span></span>

![请求处理模式显示请求到达、通过三个中间件进行处理以及响应离开应用。](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="67697-123">每个委托均可在下一个委托前后执行操作。</span><span class="sxs-lookup"><span data-stu-id="67697-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="67697-124">此外，委托还可以决定不将请求传递给下一个委托，这就是对请求管道进行短路。</span><span class="sxs-lookup"><span data-stu-id="67697-124">A delegate can also decide to not pass a request to the next delegate, which is called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="67697-125">通常需要短路，因为这样可以避免不必要的工作。</span><span class="sxs-lookup"><span data-stu-id="67697-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="67697-126">例如，静态文件中间件可以返回静态文件请求并使管道的其余部分短路。</span><span class="sxs-lookup"><span data-stu-id="67697-126">For example, Static Files Middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="67697-127">先在管道中调用异常处理委托，以便它们可以捕获在管道的后期阶段所发生的异常。</span><span class="sxs-lookup"><span data-stu-id="67697-127">Exception-handling delegates are called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="67697-128">尽可能简单的 ASP.NET Core 应用设置了处理所有请求的单个请求委托。</span><span class="sxs-lookup"><span data-stu-id="67697-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="67697-129">这种情况不包括实际请求管道。</span><span class="sxs-lookup"><span data-stu-id="67697-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="67697-130">调用单个匿名函数以响应每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="67697-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="67697-131">第一个 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> 委托终止了管道。</span><span class="sxs-lookup"><span data-stu-id="67697-131">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="67697-132">用 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 将多个请求委托链接在一起。</span><span class="sxs-lookup"><span data-stu-id="67697-132">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="67697-133">`next` 参数表示管道中的下一个委托。</span><span class="sxs-lookup"><span data-stu-id="67697-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="67697-134">可通过不调用 next 参数使管道短路。</span><span class="sxs-lookup"><span data-stu-id="67697-134">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="67697-135">通常可在下一个委托前后执行操作，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="67697-135">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

> [!WARNING]
> <span data-ttu-id="67697-136">在向客户端发送响应后，请勿调用 `next.Invoke`。</span><span class="sxs-lookup"><span data-stu-id="67697-136">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="67697-137">响应启动后，针对 <xref:Microsoft.AspNetCore.Http.HttpResponse> 的更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="67697-137">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="67697-138">例如，设置标头和状态代码更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="67697-138">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="67697-139">调用 `next` 后写入响应正文：</span><span class="sxs-lookup"><span data-stu-id="67697-139">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="67697-140">可能导致违反协议。</span><span class="sxs-lookup"><span data-stu-id="67697-140">May cause a protocol violation.</span></span> <span data-ttu-id="67697-141">例如，写入的长度超过规定的 `Content-Length`。</span><span class="sxs-lookup"><span data-stu-id="67697-141">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="67697-142">可能损坏正文格式。</span><span class="sxs-lookup"><span data-stu-id="67697-142">May corrupt the body format.</span></span> <span data-ttu-id="67697-143">例如，向 CSS 文件中写入 HTML 页脚。</span><span class="sxs-lookup"><span data-stu-id="67697-143">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="67697-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> 是一个有用的提示，指示是否已发送标头或已写入正文。</span><span class="sxs-lookup"><span data-stu-id="67697-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="67697-145">顺序</span><span class="sxs-lookup"><span data-stu-id="67697-145">Order</span></span>

<span data-ttu-id="67697-146">向 `Startup.Configure` 方法添加中间件组件的顺序定义了针对请求调用这些组件的顺序，以及响应的相反顺序。</span><span class="sxs-lookup"><span data-stu-id="67697-146">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="67697-147">此排序对于安全性、性能和功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="67697-147">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="67697-148">以下 `Configure` 方法会添加以下中间件组件：</span><span class="sxs-lookup"><span data-stu-id="67697-148">The following `Configure` method adds the following middleware components:</span></span>

1. <span data-ttu-id="67697-149">异常/错误处理</span><span class="sxs-lookup"><span data-stu-id="67697-149">Exception/error handling</span></span>
2. <span data-ttu-id="67697-150">静态文件服务器</span><span class="sxs-lookup"><span data-stu-id="67697-150">Static file server</span></span>
3. <span data-ttu-id="67697-151">身份验证</span><span class="sxs-lookup"><span data-stu-id="67697-151">Authentication</span></span>
4. <span data-ttu-id="67697-152">MVC</span><span class="sxs-lookup"><span data-stu-id="67697-152">MVC</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    if (env.IsDevelopment())
    {
        // When the app runs in the Development environment:
        //   Use the Developer Exception Page to report app runtime errors.
        //   Use the Database Error Page to report database runtime errors.
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
    }
    else
    {
        // When the app doesn't run in the Development environment:
        //   Enable the Exception Handler Middleware to catch exceptions
        //     thrown in the following middlewares.
        //   Use the HTTP Strict Transport Security Protocol (HSTS)
        //     Middleware.
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    // Use HTTPS Redirection Middleware to redirect HTTP requests to HTTPS.
    app.UseHttpsRedirection();

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Use Cookie Policy Middleware to conform to EU General Data 
    //   Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable the Exception Handler Middleware to catch exceptions
    //   thrown in the following middlewares.
    app.UseExceptionHandler("/Home/Error");

    // Return static files and end the pipeline.
    app.UseStaticFiles();

    // Authenticate before you access secure resources.
    app.UseIdentity();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="67697-153">在前面的示例代码中，每个中间件扩展方法都通过 <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> 命名空间在 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 上公开。</span><span class="sxs-lookup"><span data-stu-id="67697-153">In the preceding example code, each middleware extension method is exposed on <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> through the <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> namespace.</span></span>

<span data-ttu-id="67697-154"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> 是添加到管道的第一个中间件组件。</span><span class="sxs-lookup"><span data-stu-id="67697-154"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="67697-155">因此，异常处理程序中间件可捕获稍后调用中发生的任何异常。</span><span class="sxs-lookup"><span data-stu-id="67697-155">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="67697-156">因为尽早在管道中调用静态文件中间件，因此该组件可处理请求并使其短路，而无需通过剩余组件。</span><span class="sxs-lookup"><span data-stu-id="67697-156">Static Files Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="67697-157">静态文件中间件不提供授权检查。</span><span class="sxs-lookup"><span data-stu-id="67697-157">The Static Files Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="67697-158">可公开访问由静态文件中间件服务的任何文件，包括 wwwroot 下的文件。</span><span class="sxs-lookup"><span data-stu-id="67697-158">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="67697-159">若要了解如何保护静态文件，请参阅 <xref:fundamentals/static-files>。</span><span class="sxs-lookup"><span data-stu-id="67697-159">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="67697-160">如果静态文件中间件未处理请求，则请求将被传递给身份验证中间件 (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>)，它将执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="67697-160">If the request isn't handled by the Static Files Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="67697-161">身份验证不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="67697-161">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="67697-162">虽然身份验证中间件对请求进行身份验证，但仅在 MVC 选择特定 Razor 页或 MVC 控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="67697-162">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="67697-163">如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的标识中间件 (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>)。</span><span class="sxs-lookup"><span data-stu-id="67697-163">If the request isn't handled by Static Files Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="67697-164">标识不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="67697-164">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="67697-165">虽然标识对请求进行身份验证，但仅在 MVC 选择特定控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="67697-165">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="67697-166">以下示例演示中间件排序，其中静态文件的请求在响应压缩中间件前由静态文件中间件进行处理。</span><span class="sxs-lookup"><span data-stu-id="67697-166">The following example demonstrates a middleware order where requests for static files are handled by Static Files Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="67697-167">使用此中间件顺序不压缩静态文件。</span><span class="sxs-lookup"><span data-stu-id="67697-167">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="67697-168">可以压缩来自 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 的 MVC 响应。</span><span class="sxs-lookup"><span data-stu-id="67697-168">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static Files Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="67697-169">Use、Run 和 Map</span><span class="sxs-lookup"><span data-stu-id="67697-169">Use, Run, and Map</span></span>

<span data-ttu-id="67697-170">使用 `Use`、`Run` 和 `Map` 配置 HTTP 管道。</span><span class="sxs-lookup"><span data-stu-id="67697-170">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="67697-171">`Use` 方法可使管道短路（即不调用 `next` 请求委托）。</span><span class="sxs-lookup"><span data-stu-id="67697-171">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="67697-172">`Run` 是一种约定，并且某些中间件组件可公开在管道末尾运行的 `Run[Middleware]` 方法。</span><span class="sxs-lookup"><span data-stu-id="67697-172">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="67697-173"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 扩展用作约定来创建管道分支。</span><span class="sxs-lookup"><span data-stu-id="67697-173"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="67697-174">`Map*` 基于给定请求路径的匹配项来创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="67697-174">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="67697-175">如果请求路径以给定路径开头，则执行分支。</span><span class="sxs-lookup"><span data-stu-id="67697-175">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="67697-176">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。</span><span class="sxs-lookup"><span data-stu-id="67697-176">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="67697-177">请求</span><span class="sxs-lookup"><span data-stu-id="67697-177">Request</span></span>             | <span data-ttu-id="67697-178">响应</span><span class="sxs-lookup"><span data-stu-id="67697-178">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="67697-179">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="67697-179">localhost:1234</span></span>      | <span data-ttu-id="67697-180">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="67697-180">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="67697-181">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="67697-181">localhost:1234/map1</span></span> | <span data-ttu-id="67697-182">Map 测试 1</span><span class="sxs-lookup"><span data-stu-id="67697-182">Map Test 1</span></span>                   |
| <span data-ttu-id="67697-183">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="67697-183">localhost:1234/map2</span></span> | <span data-ttu-id="67697-184">Map 测试 2</span><span class="sxs-lookup"><span data-stu-id="67697-184">Map Test 2</span></span>                   |
| <span data-ttu-id="67697-185">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="67697-185">localhost:1234/map3</span></span> | <span data-ttu-id="67697-186">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="67697-186">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="67697-187">使用 `Map` 时，将从 `HttpRequest.Path` 中删除匹配的线段，并针对每个请求将该线段追加到 `HttpRequest.PathBase`。</span><span class="sxs-lookup"><span data-stu-id="67697-187">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="67697-188">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) 基于给定谓词的结果创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="67697-188">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="67697-189">`Func<HttpContext, bool>` 类型的任何谓词均可用于将请求映射到管道的新分支。</span><span class="sxs-lookup"><span data-stu-id="67697-189">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="67697-190">在以下示例中，谓词用于检测查询字符串变量 `branch` 是否存在：</span><span class="sxs-lookup"><span data-stu-id="67697-190">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="67697-191">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。</span><span class="sxs-lookup"><span data-stu-id="67697-191">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="67697-192">请求</span><span class="sxs-lookup"><span data-stu-id="67697-192">Request</span></span>                       | <span data-ttu-id="67697-193">响应</span><span class="sxs-lookup"><span data-stu-id="67697-193">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="67697-194">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="67697-194">localhost:1234</span></span>                | <span data-ttu-id="67697-195">来自非 Map 委托的 Hello。</span><span class="sxs-lookup"><span data-stu-id="67697-195">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="67697-196">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="67697-196">localhost:1234/?branch=master</span></span> | <span data-ttu-id="67697-197">使用的分支 = 主要分支</span><span class="sxs-lookup"><span data-stu-id="67697-197">Branch used = master</span></span>         |

<span data-ttu-id="67697-198">`Map` 支持嵌套，例如：</span><span class="sxs-lookup"><span data-stu-id="67697-198">`Map` supports nesting, for example:</span></span>

```csharp
app.Map("/level1", level1App => {
    level1App.Map("/level2a", level2AApp => {
        // "/level1/level2a" processing
    });
    level1App.Map("/level2b", level2BApp => {
        // "/level1/level2b" processing
    });
});
   ```

<span data-ttu-id="67697-199">此外，`Map` 还可同时匹配多个段：</span><span class="sxs-lookup"><span data-stu-id="67697-199">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="67697-200">内置中间件</span><span class="sxs-lookup"><span data-stu-id="67697-200">Built-in middleware</span></span>

<span data-ttu-id="67697-201">ASP.NET Core 附带以下中间件组件。</span><span class="sxs-lookup"><span data-stu-id="67697-201">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="67697-202">顺序列提供备注，说明中间件在请求管道中的放置，以及中间件可能终止请求并阻止其他中间件处理请求的条件。</span><span class="sxs-lookup"><span data-stu-id="67697-202">The *Order* column provides notes on the middleware's placement in the request pipeline and under what conditions the middleware may terminate the request and prevent other middleware from processing a request.</span></span>

| <span data-ttu-id="67697-203">中间件</span><span class="sxs-lookup"><span data-stu-id="67697-203">Middleware</span></span> | <span data-ttu-id="67697-204">描述</span><span class="sxs-lookup"><span data-stu-id="67697-204">Description</span></span> | <span data-ttu-id="67697-205">顺序</span><span class="sxs-lookup"><span data-stu-id="67697-205">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="67697-206">身份验证</span><span class="sxs-lookup"><span data-stu-id="67697-206">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="67697-207">提供身份验证支持。</span><span class="sxs-lookup"><span data-stu-id="67697-207">Provides authentication support.</span></span> | <span data-ttu-id="67697-208">在需要 `HttpContext.User` 之前。</span><span class="sxs-lookup"><span data-stu-id="67697-208">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="67697-209">OAuth 回叫的终端。</span><span class="sxs-lookup"><span data-stu-id="67697-209">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="67697-210">CORS</span><span class="sxs-lookup"><span data-stu-id="67697-210">CORS</span></span>](xref:security/cors) | <span data-ttu-id="67697-211">配置跨域资源共享。</span><span class="sxs-lookup"><span data-stu-id="67697-211">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="67697-212">在使用 CORS 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-212">Before components that use CORS.</span></span> |
| [<span data-ttu-id="67697-213">诊断</span><span class="sxs-lookup"><span data-stu-id="67697-213">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="67697-214">配置诊断。</span><span class="sxs-lookup"><span data-stu-id="67697-214">Configures diagnostics.</span></span> | <span data-ttu-id="67697-215">在生成错误的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-215">Before components that generate errors.</span></span> |
| [<span data-ttu-id="67697-216">转接头</span><span class="sxs-lookup"><span data-stu-id="67697-216">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="67697-217">将代理标头转发到当前请求。</span><span class="sxs-lookup"><span data-stu-id="67697-217">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="67697-218">在使用更新的字段（示例：架构、主机、客户端 IP、方法）的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-218">Before components that consume the updated fields (examples: scheme, host, client IP, method).</span></span> |
| [<span data-ttu-id="67697-219">HTTP 方法重写</span><span class="sxs-lookup"><span data-stu-id="67697-219">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="67697-220">允许传入 POST 请求重写方法。</span><span class="sxs-lookup"><span data-stu-id="67697-220">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="67697-221">在使用已更新方法的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-221">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="67697-222">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="67697-222">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="67697-223">将所有 HTTP 请求重定向到 HTTPS（ASP.NET Core 2.1 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="67697-223">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="67697-224">在使用 URL 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-224">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="67697-225">HTTP 严格传输安全性 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="67697-225">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="67697-226">添加特殊响应标头的安全增强中间件（ASP.NET Core 2.1 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="67697-226">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="67697-227">在发送响应之前，修改请求的组件（例如转接头、URL 重写）之后。</span><span class="sxs-lookup"><span data-stu-id="67697-227">Before responses are sent and after components that modify requests (for example, Forwarded Headers, URL Rewriting).</span></span> |
| [<span data-ttu-id="67697-228">MVC</span><span class="sxs-lookup"><span data-stu-id="67697-228">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="67697-229">用 MVC/Razor Pages 处理请求（ASP.NET Core 2.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="67697-229">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="67697-230">如果请求与路由匹配，则为终端。</span><span class="sxs-lookup"><span data-stu-id="67697-230">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="67697-231">OWIN</span><span class="sxs-lookup"><span data-stu-id="67697-231">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="67697-232">与基于 OWIN 的应用、服务器和中间件进行互操作。</span><span class="sxs-lookup"><span data-stu-id="67697-232">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="67697-233">如果 OWIN 中间件处理完请求，则为终端。</span><span class="sxs-lookup"><span data-stu-id="67697-233">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="67697-234">响应缓存</span><span class="sxs-lookup"><span data-stu-id="67697-234">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="67697-235">提供对缓存响应的支持。</span><span class="sxs-lookup"><span data-stu-id="67697-235">Provides support for caching responses.</span></span> | <span data-ttu-id="67697-236">在需要缓存的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-236">Before components that require caching.</span></span> |
| [<span data-ttu-id="67697-237">响应压缩</span><span class="sxs-lookup"><span data-stu-id="67697-237">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="67697-238">提供对压缩响应的支持。</span><span class="sxs-lookup"><span data-stu-id="67697-238">Provides support for compressing responses.</span></span> | <span data-ttu-id="67697-239">在需要压缩的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-239">Before components that require compression.</span></span> |
| [<span data-ttu-id="67697-240">请求本地化</span><span class="sxs-lookup"><span data-stu-id="67697-240">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="67697-241">提供本地化支持。</span><span class="sxs-lookup"><span data-stu-id="67697-241">Provides localization support.</span></span> | <span data-ttu-id="67697-242">在对本地化敏感的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-242">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="67697-243">路由</span><span class="sxs-lookup"><span data-stu-id="67697-243">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="67697-244">定义和约束请求路由。</span><span class="sxs-lookup"><span data-stu-id="67697-244">Defines and constrains request routes.</span></span> | <span data-ttu-id="67697-245">用于匹配路由的终端。</span><span class="sxs-lookup"><span data-stu-id="67697-245">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="67697-246">会话</span><span class="sxs-lookup"><span data-stu-id="67697-246">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="67697-247">提供对管理用户会话的支持。</span><span class="sxs-lookup"><span data-stu-id="67697-247">Provides support for managing user sessions.</span></span> | <span data-ttu-id="67697-248">在需要会话的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-248">Before components that require Session.</span></span> |
| [<span data-ttu-id="67697-249">静态文件</span><span class="sxs-lookup"><span data-stu-id="67697-249">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="67697-250">为提供静态文件和目录浏览提供支持。</span><span class="sxs-lookup"><span data-stu-id="67697-250">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="67697-251">如果请求与文件匹配，则为终端。</span><span class="sxs-lookup"><span data-stu-id="67697-251">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="67697-252">URL 重写</span><span class="sxs-lookup"><span data-stu-id="67697-252">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="67697-253">提供对重写 URL 和重定向请求的支持。</span><span class="sxs-lookup"><span data-stu-id="67697-253">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="67697-254">在使用 URL 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-254">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="67697-255">WebSockets</span><span class="sxs-lookup"><span data-stu-id="67697-255">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="67697-256">启用 WebSockets 协议。</span><span class="sxs-lookup"><span data-stu-id="67697-256">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="67697-257">在接受 WebSocket 请求所需的组件之前。</span><span class="sxs-lookup"><span data-stu-id="67697-257">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="write-middleware"></a><span data-ttu-id="67697-258">编写中间件</span><span class="sxs-lookup"><span data-stu-id="67697-258">Write middleware</span></span>

<span data-ttu-id="67697-259">通常，中间件封装在类中，并且通过扩展方法公开。</span><span class="sxs-lookup"><span data-stu-id="67697-259">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="67697-260">请考虑以下中间件，该中间件通过查询字符串设置当前请求的区域性：</span><span class="sxs-lookup"><span data-stu-id="67697-260">Consider the following middleware, which sets the culture for the current request from a query string:</span></span>

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="67697-261">以上示例代码用于演示创建中间件组件。</span><span class="sxs-lookup"><span data-stu-id="67697-261">The preceding sample code is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="67697-262">有关 ASP.NET Core 的内置本地化支持，请参阅 <xref:fundamentals/localization>。</span><span class="sxs-lookup"><span data-stu-id="67697-262">For ASP.NET Core's built-in localization support, see <xref:fundamentals/localization>.</span></span>

<span data-ttu-id="67697-263">可通过传入区域性（如 `http://localhost:7997/?culture=no`）测试中间件。</span><span class="sxs-lookup"><span data-stu-id="67697-263">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="67697-264">以下代码将中间件委托移动到类：</span><span class="sxs-lookup"><span data-stu-id="67697-264">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="67697-265">中间件 `Task` 方法的名称必须是 `Invoke`。</span><span class="sxs-lookup"><span data-stu-id="67697-265">The middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="67697-266">在 ASP.NET Core 2.0 或更高版本中，该名称可以为 `Invoke` 或 `InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="67697-266">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

::: moniker-end

<span data-ttu-id="67697-267">以下扩展方法通过 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 公开中间件：</span><span class="sxs-lookup"><span data-stu-id="67697-267">The following extension method exposes the middleware through <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="67697-268">以下代码通过 `Startup.Configure` 调用中间件：</span><span class="sxs-lookup"><span data-stu-id="67697-268">The following code calls the middleware from `Startup.Configure`:</span></span>

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="67697-269">中间件应通过在其构造函数中公开其依赖项来遵循[显式依赖项原则](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="67697-269">Middleware should follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="67697-270">在每个应用程序生存期构造一次中间件。</span><span class="sxs-lookup"><span data-stu-id="67697-270">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="67697-271">如果需要与请求中的中间件共享服务，请参阅[按请求依赖项](#per-request-dependencies)部分。</span><span class="sxs-lookup"><span data-stu-id="67697-271">See the [Per-request dependencies](#per-request-dependencies) section if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="67697-272">中间件组件可通过构造函数参数从[依赖关系注入 (DI)](xref:fundamentals/dependency-injection) 解析其依赖项。</span><span class="sxs-lookup"><span data-stu-id="67697-272">Middleware components can resolve their dependencies from [dependency injection (DI)](xref:fundamentals/dependency-injection) through constructor parameters.</span></span> <span data-ttu-id="67697-273">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) 也可直接接受其他参数。</span><span class="sxs-lookup"><span data-stu-id="67697-273">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="67697-274">按请求依赖项</span><span class="sxs-lookup"><span data-stu-id="67697-274">Per-request dependencies</span></span>

<span data-ttu-id="67697-275">由于中间件是在应用启动时构造的，而不是按请求构造的，因此在每个请求过程中，中间件构造函数使用的范围内生存期服务不与其他依赖关系注入类型共享。</span><span class="sxs-lookup"><span data-stu-id="67697-275">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors aren't shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="67697-276">如果必须在中间件和其他类型之间共享范围内服务，请将这些服务添加到 `Invoke` 方法的签名。</span><span class="sxs-lookup"><span data-stu-id="67697-276">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="67697-277">`Invoke` 方法可接受由 DI 填充的其他参数：</span><span class="sxs-lookup"><span data-stu-id="67697-277">The `Invoke` method can accept additional parameters that are populated by DI:</span></span>

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    // IMyScopedService is injected into Invoke
    public async Task Invoke(HttpContext httpContext, IMyScopedService svc)
    {
        svc.MyProperty = 1000;
        await _next(httpContext);
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="67697-278">其他资源</span><span class="sxs-lookup"><span data-stu-id="67697-278">Additional resources</span></span>

* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
