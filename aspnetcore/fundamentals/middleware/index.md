---
title: ASP.NET Core 中间件
author: rick-anderson
description: 了解 ASP.NET Core 中间件和请求管道。
ms.author: riande
ms.custom: mvc
ms.date: 08/21/2018
uid: fundamentals/middleware/index
ms.openlocfilehash: 84e79df7fcf5790e658a20c80f21d73cdc76c054
ms.sourcegitcommit: 8bf4dff3069e62972c1b0839a93fb444e502afe7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2018
ms.locfileid: "46483004"
---
# <a name="aspnet-core-middleware"></a><span data-ttu-id="d0919-103">ASP.NET Core 中间件</span><span class="sxs-lookup"><span data-stu-id="d0919-103">ASP.NET Core Middleware</span></span>

<span data-ttu-id="d0919-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="d0919-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="d0919-105">中间件是一种装配到应用管道以处理请求和响应的软件。</span><span class="sxs-lookup"><span data-stu-id="d0919-105">Middleware is software that's assembled into an app pipeline to handle requests and responses.</span></span> <span data-ttu-id="d0919-106">每个组件：</span><span class="sxs-lookup"><span data-stu-id="d0919-106">Each component:</span></span>

* <span data-ttu-id="d0919-107">选择是否将请求传递到管道中的下一个组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-107">Chooses whether to pass the request to the next component in the pipeline.</span></span>
* <span data-ttu-id="d0919-108">可在调用管道中的下一个组件前后执行工作。</span><span class="sxs-lookup"><span data-stu-id="d0919-108">Can perform work before and after the next component in the pipeline is invoked.</span></span>

<span data-ttu-id="d0919-109">请求委托用于生成请求管道。</span><span class="sxs-lookup"><span data-stu-id="d0919-109">Request delegates are used to build the request pipeline.</span></span> <span data-ttu-id="d0919-110">请求委托处理每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="d0919-110">The request delegates handle each HTTP request.</span></span>

<span data-ttu-id="d0919-111">使用 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 和 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 扩展方法来配置请求委托。</span><span class="sxs-lookup"><span data-stu-id="d0919-111">Request delegates are configured using <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*>, <xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*>, and <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> extension methods.</span></span> <span data-ttu-id="d0919-112">可将一个单独的请求委托并行指定为匿名方法（称为并行中间件），或在可重用的类中对其进行定义。</span><span class="sxs-lookup"><span data-stu-id="d0919-112">An individual request delegate can be specified in-line as an anonymous method (called in-line middleware), or it can be defined in a reusable class.</span></span> <span data-ttu-id="d0919-113">这些可重用的类和并行匿名方法即为中间件，也叫中间件组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-113">These reusable classes and in-line anonymous methods are *middleware*, also called *middleware components*.</span></span> <span data-ttu-id="d0919-114">请求管道中的每个中间件组件负责调用管道中的下一个组件，或使管道短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-114">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the pipeline.</span></span>

<span data-ttu-id="d0919-115"><xref:migration/http-modules> 介绍了 ASP.NET Core 和 ASP.NET 4.x 中请求管道之间的差异，并提供了更多的中间件示例。</span><span class="sxs-lookup"><span data-stu-id="d0919-115"><xref:migration/http-modules> explains the difference between request pipelines in ASP.NET Core and ASP.NET 4.x and provides more middleware samples.</span></span>

## <a name="create-a-middleware-pipeline-with-iapplicationbuilder"></a><span data-ttu-id="d0919-116">使用 IApplicationBuilder 创建中间件管道</span><span class="sxs-lookup"><span data-stu-id="d0919-116">Create a middleware pipeline with IApplicationBuilder</span></span>

<span data-ttu-id="d0919-117">ASP.NET Core 请求管道包含一系列请求委托，依次调用。</span><span class="sxs-lookup"><span data-stu-id="d0919-117">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="d0919-118">下图演示了这一概念。</span><span class="sxs-lookup"><span data-stu-id="d0919-118">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="d0919-119">沿黑色箭头执行。</span><span class="sxs-lookup"><span data-stu-id="d0919-119">The thread of execution follows the black arrows.</span></span>

![请求处理模式显示请求到达、通过三个中间件进行处理以及响应离开应用。](index/_static/request-delegate-pipeline.png)

<span data-ttu-id="d0919-123">每个委托均可在下一个委托前后执行操作。</span><span class="sxs-lookup"><span data-stu-id="d0919-123">Each delegate can perform operations before and after the next delegate.</span></span> <span data-ttu-id="d0919-124">此外，委托还可以决定不将请求传递给下一个委托，这就是对请求管道进行短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-124">A delegate can also decide to not pass a request to the next delegate, which is called *short-circuiting the request pipeline*.</span></span> <span data-ttu-id="d0919-125">通常需要短路，因为这样可以避免不必要的工作。</span><span class="sxs-lookup"><span data-stu-id="d0919-125">Short-circuiting is often desirable because it avoids unnecessary work.</span></span> <span data-ttu-id="d0919-126">例如，静态文件中间件可以返回静态文件请求并使管道的其余部分短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-126">For example, Static Files Middleware can return a request for a static file and short-circuit the rest of the pipeline.</span></span> <span data-ttu-id="d0919-127">先在管道中调用异常处理委托，以便它们可以捕获在管道的后期阶段所发生的异常。</span><span class="sxs-lookup"><span data-stu-id="d0919-127">Exception-handling delegates are called early in the pipeline, so they can catch exceptions that occur in later stages of the pipeline.</span></span>

<span data-ttu-id="d0919-128">尽可能简单的 ASP.NET Core 应用设置了处理所有请求的单个请求委托。</span><span class="sxs-lookup"><span data-stu-id="d0919-128">The simplest possible ASP.NET Core app sets up a single request delegate that handles all requests.</span></span> <span data-ttu-id="d0919-129">这种情况不包括实际请求管道。</span><span class="sxs-lookup"><span data-stu-id="d0919-129">This case doesn't include an actual request pipeline.</span></span> <span data-ttu-id="d0919-130">调用单个匿名函数以响应每个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="d0919-130">Instead, a single anonymous function is called in response to every HTTP request.</span></span>

[!code-csharp[](index/snapshot/Middleware/Startup.cs?name=snippet1)]

<span data-ttu-id="d0919-131">第一个 <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> 委托终止了管道。</span><span class="sxs-lookup"><span data-stu-id="d0919-131">The first <xref:Microsoft.AspNetCore.Builder.RunExtensions.Run*> delegate terminates the pipeline.</span></span>

<span data-ttu-id="d0919-132">用 <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*> 将多个请求委托链接在一起。</span><span class="sxs-lookup"><span data-stu-id="d0919-132">Chain multiple request delegates together with <xref:Microsoft.AspNetCore.Builder.UseExtensions.Use*>.</span></span> <span data-ttu-id="d0919-133">`next` 参数表示管道中的下一个委托。</span><span class="sxs-lookup"><span data-stu-id="d0919-133">The `next` parameter represents the next delegate in the pipeline.</span></span> <span data-ttu-id="d0919-134">可通过不调用 next 参数使管道短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-134">You can short-circuit the pipeline by *not* calling the *next* parameter.</span></span> <span data-ttu-id="d0919-135">通常可在下一个委托前后执行操作，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="d0919-135">You can typically perform actions both before and after the next delegate, as the following example demonstrates:</span></span>

[!code-csharp[](index/snapshot/Chain/Startup.cs?name=snippet1)]

> [!WARNING]
> <span data-ttu-id="d0919-136">在向客户端发送响应后，请勿调用 `next.Invoke`。</span><span class="sxs-lookup"><span data-stu-id="d0919-136">Don't call `next.Invoke` after the response has been sent to the client.</span></span> <span data-ttu-id="d0919-137">响应启动后，针对 <xref:Microsoft.AspNetCore.Http.HttpResponse> 的更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="d0919-137">Changes to <xref:Microsoft.AspNetCore.Http.HttpResponse> after the response has started throw an exception.</span></span> <span data-ttu-id="d0919-138">例如，设置标头和状态代码更改将引发异常。</span><span class="sxs-lookup"><span data-stu-id="d0919-138">For example, changes such as setting headers and a status code throw an exception.</span></span> <span data-ttu-id="d0919-139">调用 `next` 后写入响应正文：</span><span class="sxs-lookup"><span data-stu-id="d0919-139">Writing to the response body after calling `next`:</span></span>
>
> * <span data-ttu-id="d0919-140">可能导致违反协议。</span><span class="sxs-lookup"><span data-stu-id="d0919-140">May cause a protocol violation.</span></span> <span data-ttu-id="d0919-141">例如，写入的长度超过规定的 `Content-Length`。</span><span class="sxs-lookup"><span data-stu-id="d0919-141">For example, writing more than the stated `Content-Length`.</span></span>
> * <span data-ttu-id="d0919-142">可能损坏正文格式。</span><span class="sxs-lookup"><span data-stu-id="d0919-142">May corrupt the body format.</span></span> <span data-ttu-id="d0919-143">例如，向 CSS 文件中写入 HTML 页脚。</span><span class="sxs-lookup"><span data-stu-id="d0919-143">For example, writing an HTML footer to a CSS file.</span></span>
>
> <span data-ttu-id="d0919-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> 是一个有用的提示，指示是否已发送标头或已写入正文。</span><span class="sxs-lookup"><span data-stu-id="d0919-144"><xref:Microsoft.AspNetCore.Http.HttpResponse.HasStarted*> is a useful hint to indicate if headers have been sent or the body has been written to.</span></span>

## <a name="order"></a><span data-ttu-id="d0919-145">顺序</span><span class="sxs-lookup"><span data-stu-id="d0919-145">Order</span></span>

<span data-ttu-id="d0919-146">向 `Startup.Configure` 方法添加中间件组件的顺序定义了针对请求调用这些组件的顺序，以及响应的相反顺序。</span><span class="sxs-lookup"><span data-stu-id="d0919-146">The order that middleware components are added in the `Startup.Configure` method defines the order in which the middleware components are invoked on requests and the reverse order for the response.</span></span> <span data-ttu-id="d0919-147">此排序对于安全性、性能和功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="d0919-147">The order is critical for security, performance, and functionality.</span></span>

<span data-ttu-id="d0919-148">以下 `Startup.Configure` 方法将为常见应用方案添加中间件组件：</span><span class="sxs-lookup"><span data-stu-id="d0919-148">The following `Startup.Configure` method adds middleware components for common app scenarios:</span></span>

::: moniker range=">= aspnetcore-2.0"

1. <span data-ttu-id="d0919-149">异常/错误处理</span><span class="sxs-lookup"><span data-stu-id="d0919-149">Exception/error handling</span></span>
1. <span data-ttu-id="d0919-150">HTTP 严格传输安全协议</span><span class="sxs-lookup"><span data-stu-id="d0919-150">HTTP Strict Transport Security Protocol</span></span>
1. <span data-ttu-id="d0919-151">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="d0919-151">HTTPS redirection</span></span>
1. <span data-ttu-id="d0919-152">静态文件服务器</span><span class="sxs-lookup"><span data-stu-id="d0919-152">Static file server</span></span>
1. <span data-ttu-id="d0919-153">Cookie 策略实施</span><span class="sxs-lookup"><span data-stu-id="d0919-153">Cookie policy enforcement</span></span>
1. <span data-ttu-id="d0919-154">身份验证</span><span class="sxs-lookup"><span data-stu-id="d0919-154">Authentication</span></span>
1. <span data-ttu-id="d0919-155">会话</span><span class="sxs-lookup"><span data-stu-id="d0919-155">Session</span></span>
1. <span data-ttu-id="d0919-156">MVC</span><span class="sxs-lookup"><span data-stu-id="d0919-156">MVC</span></span>

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
    // Protection Regulation (GDPR) regulations.
    app.UseCookiePolicy();

    // Authenticate before the user accesses secure resources.
    app.UseAuthentication();

    // If the app uses session state, call Session Middleware after Cookie 
    // Policy Middleware and before MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvc();
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. <span data-ttu-id="d0919-157">异常/错误处理</span><span class="sxs-lookup"><span data-stu-id="d0919-157">Exception/error handling</span></span>
1. <span data-ttu-id="d0919-158">静态文件</span><span class="sxs-lookup"><span data-stu-id="d0919-158">Static files</span></span>
1. <span data-ttu-id="d0919-159">身份验证</span><span class="sxs-lookup"><span data-stu-id="d0919-159">Authentication</span></span>
1. <span data-ttu-id="d0919-160">会话</span><span class="sxs-lookup"><span data-stu-id="d0919-160">Session</span></span>
1. <span data-ttu-id="d0919-161">MVC</span><span class="sxs-lookup"><span data-stu-id="d0919-161">MVC</span></span>

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

    // If the app uses session state, call UseSession before 
    // MVC Middleware.
    app.UseSession();

    // Add MVC to the request pipeline.
    app.UseMvcWithDefaultRoute();
}
```

::: moniker-end

<span data-ttu-id="d0919-162">在前面的示例代码中，每个中间件扩展方法都通过 <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> 命名空间在 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 上公开。</span><span class="sxs-lookup"><span data-stu-id="d0919-162">In the preceding example code, each middleware extension method is exposed on <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> through the <xref:Microsoft.AspNetCore.Builder?displayProperty=fullName> namespace.</span></span>

<span data-ttu-id="d0919-163"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> 是添加到管道的第一个中间件组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-163"><xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> is the first middleware component added to the pipeline.</span></span> <span data-ttu-id="d0919-164">因此，异常处理程序中间件可捕获稍后调用中发生的任何异常。</span><span class="sxs-lookup"><span data-stu-id="d0919-164">Therefore, the Exception Handler Middleware catches any exceptions that occur in later calls.</span></span>

<span data-ttu-id="d0919-165">因为尽早在管道中调用静态文件中间件，因此该组件可处理请求并使其短路，而无需通过剩余组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-165">Static Files Middleware is called early in the pipeline so that it can handle requests and short-circuit without going through the remaining components.</span></span> <span data-ttu-id="d0919-166">静态文件中间件不提供授权检查。</span><span class="sxs-lookup"><span data-stu-id="d0919-166">The Static Files Middleware provides **no** authorization checks.</span></span> <span data-ttu-id="d0919-167">可公开访问由静态文件中间件服务的任何文件，包括 wwwroot 下的文件。</span><span class="sxs-lookup"><span data-stu-id="d0919-167">Any files served by it, including those under *wwwroot*, are publicly available.</span></span> <span data-ttu-id="d0919-168">若要了解如何保护静态文件，请参阅 <xref:fundamentals/static-files>。</span><span class="sxs-lookup"><span data-stu-id="d0919-168">For an approach to secure static files, see <xref:fundamentals/static-files>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="d0919-169">如果静态文件中间件未处理请求，则请求将被传递给身份验证中间件 (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>)，它将执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="d0919-169">If the request isn't handled by the Static Files Middleware, it's passed on to the Authentication Middleware (<xref:Microsoft.AspNetCore.Builder.AuthAppBuilderExtensions.UseAuthentication*>), which performs authentication.</span></span> <span data-ttu-id="d0919-170">身份验证不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-170">Authentication doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="d0919-171">虽然身份验证中间件对请求进行身份验证，但仅在 MVC 选择特定 Razor 页或 MVC 控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="d0919-171">Although Authentication Middleware authenticates requests, authorization (and rejection) occurs only after MVC selects a specific Razor Page or MVC controller and action.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="d0919-172">如果静态文件中间件未处理请求，则请求将被传递给执行身份验证的标识中间件 (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>)。</span><span class="sxs-lookup"><span data-stu-id="d0919-172">If the request isn't handled by Static Files Middleware, it's passed on to the Identity Middleware (<xref:Microsoft.AspNetCore.Builder.BuilderExtensions.UseIdentity*>), which performs authentication.</span></span> <span data-ttu-id="d0919-173">标识不使未经身份验证的请求短路。</span><span class="sxs-lookup"><span data-stu-id="d0919-173">Identity doesn't short-circuit unauthenticated requests.</span></span> <span data-ttu-id="d0919-174">虽然标识对请求进行身份验证，但仅在 MVC 选择特定控制器和操作后，才发生授权（和拒绝）。</span><span class="sxs-lookup"><span data-stu-id="d0919-174">Although Identity authenticates requests, authorization (and rejection) occurs only after MVC selects a specific controller and action.</span></span>

::: moniker-end

<span data-ttu-id="d0919-175">以下示例演示中间件排序，其中静态文件的请求在响应压缩中间件前由静态文件中间件进行处理。</span><span class="sxs-lookup"><span data-stu-id="d0919-175">The following example demonstrates a middleware order where requests for static files are handled by Static Files Middleware before Response Compression Middleware.</span></span> <span data-ttu-id="d0919-176">使用此中间件顺序不压缩静态文件。</span><span class="sxs-lookup"><span data-stu-id="d0919-176">Static files aren't compressed with this middleware order.</span></span> <span data-ttu-id="d0919-177">可以压缩来自 <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> 的 MVC 响应。</span><span class="sxs-lookup"><span data-stu-id="d0919-177">The MVC responses from <xref:Microsoft.AspNetCore.Builder.MvcApplicationBuilderExtensions.UseMvcWithDefaultRoute*> can be compressed.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    // Static files not compressed by Static Files Middleware.
    app.UseStaticFiles();
    app.UseResponseCompression();
    app.UseMvcWithDefaultRoute();
}
```

### <a name="use-run-and-map"></a><span data-ttu-id="d0919-178">Use、Run 和 Map</span><span class="sxs-lookup"><span data-stu-id="d0919-178">Use, Run, and Map</span></span>

<span data-ttu-id="d0919-179">使用 `Use`、`Run` 和 `Map` 配置 HTTP 管道。</span><span class="sxs-lookup"><span data-stu-id="d0919-179">Configure the HTTP pipeline using `Use`, `Run`, and `Map`.</span></span> <span data-ttu-id="d0919-180">`Use` 方法可使管道短路（即不调用 `next` 请求委托）。</span><span class="sxs-lookup"><span data-stu-id="d0919-180">The `Use` method can short-circuit the pipeline (that is, if it doesn't call a `next` request delegate).</span></span> <span data-ttu-id="d0919-181">`Run` 是一种约定，并且某些中间件组件可公开在管道末尾运行的 `Run[Middleware]` 方法。</span><span class="sxs-lookup"><span data-stu-id="d0919-181">`Run` is a convention, and some middleware components may expose `Run[Middleware]` methods that run at the end of the pipeline.</span></span>

<span data-ttu-id="d0919-182"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> 扩展用作约定来创建管道分支。</span><span class="sxs-lookup"><span data-stu-id="d0919-182"><xref:Microsoft.AspNetCore.Builder.MapExtensions.Map*> extensions are used as a convention for branching the pipeline.</span></span> <span data-ttu-id="d0919-183">`Map*` 基于给定请求路径的匹配项来创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="d0919-183">`Map*` branches the request pipeline based on matches of the given request path.</span></span> <span data-ttu-id="d0919-184">如果请求路径以给定路径开头，则执行分支。</span><span class="sxs-lookup"><span data-stu-id="d0919-184">If the request path starts with the given path, the branch is executed.</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMap.cs?name=snippet1)]

<span data-ttu-id="d0919-185">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。</span><span class="sxs-lookup"><span data-stu-id="d0919-185">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="d0919-186">请求</span><span class="sxs-lookup"><span data-stu-id="d0919-186">Request</span></span>             | <span data-ttu-id="d0919-187">响应</span><span class="sxs-lookup"><span data-stu-id="d0919-187">Response</span></span>                     |
| ------------------- | ---------------------------- |
| <span data-ttu-id="d0919-188">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="d0919-188">localhost:1234</span></span>      | <span data-ttu-id="d0919-189">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="d0919-189">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="d0919-190">localhost:1234/map1</span><span class="sxs-lookup"><span data-stu-id="d0919-190">localhost:1234/map1</span></span> | <span data-ttu-id="d0919-191">Map Test 1</span><span class="sxs-lookup"><span data-stu-id="d0919-191">Map Test 1</span></span>                   |
| <span data-ttu-id="d0919-192">localhost:1234/map2</span><span class="sxs-lookup"><span data-stu-id="d0919-192">localhost:1234/map2</span></span> | <span data-ttu-id="d0919-193">Map Test 2</span><span class="sxs-lookup"><span data-stu-id="d0919-193">Map Test 2</span></span>                   |
| <span data-ttu-id="d0919-194">localhost:1234/map3</span><span class="sxs-lookup"><span data-stu-id="d0919-194">localhost:1234/map3</span></span> | <span data-ttu-id="d0919-195">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="d0919-195">Hello from non-Map delegate.</span></span> |

<span data-ttu-id="d0919-196">使用 `Map` 时，将从 `HttpRequest.Path` 中删除匹配的路径段，并针对每个请求将该路径段追加到 `HttpRequest.PathBase`。</span><span class="sxs-lookup"><span data-stu-id="d0919-196">When `Map` is used, the matched path segment(s) are removed from `HttpRequest.Path` and appended to `HttpRequest.PathBase` for each request.</span></span>

<span data-ttu-id="d0919-197">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) 基于给定谓词的结果创建请求管道分支。</span><span class="sxs-lookup"><span data-stu-id="d0919-197">[MapWhen](/dotnet/api/microsoft.aspnetcore.builder.mapwhenextensions) branches the request pipeline based on the result of the given predicate.</span></span> <span data-ttu-id="d0919-198">`Func<HttpContext, bool>` 类型的任何谓词均可用于将请求映射到管道的新分支。</span><span class="sxs-lookup"><span data-stu-id="d0919-198">Any predicate of type `Func<HttpContext, bool>` can be used to map requests to a new branch of the pipeline.</span></span> <span data-ttu-id="d0919-199">在以下示例中，谓词用于检测查询字符串变量 `branch` 是否存在：</span><span class="sxs-lookup"><span data-stu-id="d0919-199">In the following example, a predicate is used to detect the presence of a query string variable `branch`:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMapWhen.cs?name=snippet1)]

<span data-ttu-id="d0919-200">下表使用前面的代码显示来自 `http://localhost:1234` 的请求和响应。</span><span class="sxs-lookup"><span data-stu-id="d0919-200">The following table shows the requests and responses from `http://localhost:1234` using the previous code.</span></span>

| <span data-ttu-id="d0919-201">请求</span><span class="sxs-lookup"><span data-stu-id="d0919-201">Request</span></span>                       | <span data-ttu-id="d0919-202">响应</span><span class="sxs-lookup"><span data-stu-id="d0919-202">Response</span></span>                     |
| ----------------------------- | ---------------------------- |
| <span data-ttu-id="d0919-203">localhost:1234</span><span class="sxs-lookup"><span data-stu-id="d0919-203">localhost:1234</span></span>                | <span data-ttu-id="d0919-204">Hello from non-Map delegate.</span><span class="sxs-lookup"><span data-stu-id="d0919-204">Hello from non-Map delegate.</span></span> |
| <span data-ttu-id="d0919-205">localhost:1234/?branch=master</span><span class="sxs-lookup"><span data-stu-id="d0919-205">localhost:1234/?branch=master</span></span> | <span data-ttu-id="d0919-206">Branch used = master</span><span class="sxs-lookup"><span data-stu-id="d0919-206">Branch used = master</span></span>         |

<span data-ttu-id="d0919-207">`Map` 支持嵌套，例如：</span><span class="sxs-lookup"><span data-stu-id="d0919-207">`Map` supports nesting, for example:</span></span>

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

<span data-ttu-id="d0919-208">此外，`Map` 还可同时匹配多个段：</span><span class="sxs-lookup"><span data-stu-id="d0919-208">`Map` can also match multiple segments at once:</span></span>

[!code-csharp[](index/snapshot/Chain/StartupMultiSeg.cs?name=snippet1&highlight=13)]

## <a name="built-in-middleware"></a><span data-ttu-id="d0919-209">内置中间件</span><span class="sxs-lookup"><span data-stu-id="d0919-209">Built-in middleware</span></span>

<span data-ttu-id="d0919-210">ASP.NET Core 附带以下中间件组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-210">ASP.NET Core ships with the following middleware components.</span></span> <span data-ttu-id="d0919-211">顺序列提供备注，说明中间件在请求管道中的放置，以及中间件可能终止请求并阻止其他中间件处理请求的条件。</span><span class="sxs-lookup"><span data-stu-id="d0919-211">The *Order* column provides notes on the middleware's placement in the request pipeline and under what conditions the middleware may terminate the request and prevent other middleware from processing a request.</span></span>

| <span data-ttu-id="d0919-212">中间件</span><span class="sxs-lookup"><span data-stu-id="d0919-212">Middleware</span></span> | <span data-ttu-id="d0919-213">描述</span><span class="sxs-lookup"><span data-stu-id="d0919-213">Description</span></span> | <span data-ttu-id="d0919-214">顺序</span><span class="sxs-lookup"><span data-stu-id="d0919-214">Order</span></span> |
| ---------- | ----------- | ----- |
| [<span data-ttu-id="d0919-215">身份验证</span><span class="sxs-lookup"><span data-stu-id="d0919-215">Authentication</span></span>](xref:security/authentication/identity) | <span data-ttu-id="d0919-216">提供身份验证支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-216">Provides authentication support.</span></span> | <span data-ttu-id="d0919-217">在需要 `HttpContext.User` 之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-217">Before `HttpContext.User` is needed.</span></span> <span data-ttu-id="d0919-218">OAuth 回叫的终端。</span><span class="sxs-lookup"><span data-stu-id="d0919-218">Terminal for OAuth callbacks.</span></span> |
| [<span data-ttu-id="d0919-219">Cookie 策略</span><span class="sxs-lookup"><span data-stu-id="d0919-219">Cookie Policy</span></span>](xref:security/gdpr) | <span data-ttu-id="d0919-220">跟踪用户是否同意存储个人信息，并强制实施 cookie 字段（如 `secure` 和 `SameSite`）的最低标准。</span><span class="sxs-lookup"><span data-stu-id="d0919-220">Tracks consent from users for storing personal information and enforces minimum standards for cookie fields, such as `secure` and `SameSite`.</span></span> | <span data-ttu-id="d0919-221">在发出 cookie 的中间件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-221">Before middleware that issues cookies.</span></span> <span data-ttu-id="d0919-222">示例：身份验证、会话、MVC (TempData)。</span><span class="sxs-lookup"><span data-stu-id="d0919-222">Examples: Authentication, Session, MVC (TempData).</span></span> |
| [<span data-ttu-id="d0919-223">CORS</span><span class="sxs-lookup"><span data-stu-id="d0919-223">CORS</span></span>](xref:security/cors) | <span data-ttu-id="d0919-224">配置跨域资源共享。</span><span class="sxs-lookup"><span data-stu-id="d0919-224">Configures Cross-Origin Resource Sharing.</span></span> | <span data-ttu-id="d0919-225">在使用 CORS 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-225">Before components that use CORS.</span></span> |
| [<span data-ttu-id="d0919-226">诊断</span><span class="sxs-lookup"><span data-stu-id="d0919-226">Diagnostics</span></span>](xref:fundamentals/error-handling) | <span data-ttu-id="d0919-227">配置诊断。</span><span class="sxs-lookup"><span data-stu-id="d0919-227">Configures diagnostics.</span></span> | <span data-ttu-id="d0919-228">在生成错误的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-228">Before components that generate errors.</span></span> |
| [<span data-ttu-id="d0919-229">转接头</span><span class="sxs-lookup"><span data-stu-id="d0919-229">Forwarded Headers</span></span>](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions) | <span data-ttu-id="d0919-230">将代理标头转发到当前请求。</span><span class="sxs-lookup"><span data-stu-id="d0919-230">Forwards proxied headers onto the current request.</span></span> | <span data-ttu-id="d0919-231">在使用已更新字段的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-231">Before components that consume the updated fields.</span></span> <span data-ttu-id="d0919-232">示例：方案、主机、客户端 IP、方法。</span><span class="sxs-lookup"><span data-stu-id="d0919-232">Examples: scheme, host, client IP, method.</span></span> |
| [<span data-ttu-id="d0919-233">HTTP 方法重写</span><span class="sxs-lookup"><span data-stu-id="d0919-233">HTTP Method Override</span></span>](/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions) | <span data-ttu-id="d0919-234">允许传入 POST 请求重写方法。</span><span class="sxs-lookup"><span data-stu-id="d0919-234">Allows an incoming POST request to override the method.</span></span> | <span data-ttu-id="d0919-235">在使用已更新方法的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-235">Before components that consume the updated method.</span></span> |
| [<span data-ttu-id="d0919-236">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="d0919-236">HTTPS Redirection</span></span>](xref:security/enforcing-ssl#require-https) | <span data-ttu-id="d0919-237">将所有 HTTP 请求重定向到 HTTPS（ASP.NET Core 2.1 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="d0919-237">Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="d0919-238">在使用 URL 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-238">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="d0919-239">HTTP 严格传输安全性 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="d0919-239">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts) | <span data-ttu-id="d0919-240">添加特殊响应标头的安全增强中间件（ASP.NET Core 2.1 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="d0919-240">Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</span></span> | <span data-ttu-id="d0919-241">在发送响应之前，修改请求的组件之后。</span><span class="sxs-lookup"><span data-stu-id="d0919-241">Before responses are sent and after components that modify requests.</span></span> <span data-ttu-id="d0919-242">示例：转接头、URL 重写。</span><span class="sxs-lookup"><span data-stu-id="d0919-242">Examples: Forwarded Headers, URL Rewriting.</span></span> |
| [<span data-ttu-id="d0919-243">MVC</span><span class="sxs-lookup"><span data-stu-id="d0919-243">MVC</span></span>](xref:mvc/overview) | <span data-ttu-id="d0919-244">用 MVC/Razor Pages 处理请求（ASP.NET Core 2.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="d0919-244">Processes requests with MVC/Razor Pages (ASP.NET Core 2.0 or later).</span></span> | <span data-ttu-id="d0919-245">如果请求与路由匹配，则为终端。</span><span class="sxs-lookup"><span data-stu-id="d0919-245">Terminal if a request matches a route.</span></span> |
| [<span data-ttu-id="d0919-246">OWIN</span><span class="sxs-lookup"><span data-stu-id="d0919-246">OWIN</span></span>](xref:fundamentals/owin) | <span data-ttu-id="d0919-247">与基于 OWIN 的应用、服务器和中间件进行互操作。</span><span class="sxs-lookup"><span data-stu-id="d0919-247">Interop with OWIN-based apps, servers, and middleware.</span></span> | <span data-ttu-id="d0919-248">如果 OWIN 中间件处理完请求，则为终端。</span><span class="sxs-lookup"><span data-stu-id="d0919-248">Terminal if the OWIN Middleware fully processes the request.</span></span> |
| [<span data-ttu-id="d0919-249">响应缓存</span><span class="sxs-lookup"><span data-stu-id="d0919-249">Response Caching</span></span>](xref:performance/caching/middleware) | <span data-ttu-id="d0919-250">提供对缓存响应的支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-250">Provides support for caching responses.</span></span> | <span data-ttu-id="d0919-251">在需要缓存的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-251">Before components that require caching.</span></span> |
| [<span data-ttu-id="d0919-252">响应压缩</span><span class="sxs-lookup"><span data-stu-id="d0919-252">Response Compression</span></span>](xref:performance/response-compression) | <span data-ttu-id="d0919-253">提供对压缩响应的支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-253">Provides support for compressing responses.</span></span> | <span data-ttu-id="d0919-254">在需要压缩的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-254">Before components that require compression.</span></span> |
| [<span data-ttu-id="d0919-255">请求本地化</span><span class="sxs-lookup"><span data-stu-id="d0919-255">Request Localization</span></span>](xref:fundamentals/localization) | <span data-ttu-id="d0919-256">提供本地化支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-256">Provides localization support.</span></span> | <span data-ttu-id="d0919-257">在对本地化敏感的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-257">Before localization sensitive components.</span></span> |
| [<span data-ttu-id="d0919-258">路由</span><span class="sxs-lookup"><span data-stu-id="d0919-258">Routing</span></span>](xref:fundamentals/routing) | <span data-ttu-id="d0919-259">定义和约束请求路由。</span><span class="sxs-lookup"><span data-stu-id="d0919-259">Defines and constrains request routes.</span></span> | <span data-ttu-id="d0919-260">用于匹配路由的终端。</span><span class="sxs-lookup"><span data-stu-id="d0919-260">Terminal for matching routes.</span></span> |
| [<span data-ttu-id="d0919-261">会话</span><span class="sxs-lookup"><span data-stu-id="d0919-261">Session</span></span>](xref:fundamentals/app-state) | <span data-ttu-id="d0919-262">提供对管理用户会话的支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-262">Provides support for managing user sessions.</span></span> | <span data-ttu-id="d0919-263">在需要会话的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-263">Before components that require Session.</span></span> |
| [<span data-ttu-id="d0919-264">静态文件</span><span class="sxs-lookup"><span data-stu-id="d0919-264">Static Files</span></span>](xref:fundamentals/static-files) | <span data-ttu-id="d0919-265">为提供静态文件和目录浏览提供支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-265">Provides support for serving static files and directory browsing.</span></span> | <span data-ttu-id="d0919-266">如果请求与文件匹配，则为终端。</span><span class="sxs-lookup"><span data-stu-id="d0919-266">Terminal if a request matches a file.</span></span> |
| [<span data-ttu-id="d0919-267">URL 重写</span><span class="sxs-lookup"><span data-stu-id="d0919-267">URL Rewriting</span></span>](xref:fundamentals/url-rewriting) | <span data-ttu-id="d0919-268">提供对重写 URL 和重定向请求的支持。</span><span class="sxs-lookup"><span data-stu-id="d0919-268">Provides support for rewriting URLs and redirecting requests.</span></span> | <span data-ttu-id="d0919-269">在使用 URL 的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-269">Before components that consume the URL.</span></span> |
| [<span data-ttu-id="d0919-270">WebSockets</span><span class="sxs-lookup"><span data-stu-id="d0919-270">WebSockets</span></span>](xref:fundamentals/websockets) | <span data-ttu-id="d0919-271">启用 WebSockets 协议。</span><span class="sxs-lookup"><span data-stu-id="d0919-271">Enables the WebSockets protocol.</span></span> | <span data-ttu-id="d0919-272">在接受 WebSocket 请求所需的组件之前。</span><span class="sxs-lookup"><span data-stu-id="d0919-272">Before components that are required to accept WebSocket requests.</span></span> |

## <a name="write-middleware"></a><span data-ttu-id="d0919-273">编写中间件</span><span class="sxs-lookup"><span data-stu-id="d0919-273">Write middleware</span></span>

<span data-ttu-id="d0919-274">通常，中间件封装在类中，并且通过扩展方法公开。</span><span class="sxs-lookup"><span data-stu-id="d0919-274">Middleware is generally encapsulated in a class and exposed with an extension method.</span></span> <span data-ttu-id="d0919-275">请考虑以下中间件，该中间件通过查询字符串设置当前请求的区域性：</span><span class="sxs-lookup"><span data-stu-id="d0919-275">Consider the following middleware, which sets the culture for the current request from a query string:</span></span>

[!code-csharp[](index/snapshot/Culture/StartupCulture.cs?name=snippet1)]

<span data-ttu-id="d0919-276">以上示例代码用于演示创建中间件组件。</span><span class="sxs-lookup"><span data-stu-id="d0919-276">The preceding sample code is used to demonstrate creating a middleware component.</span></span> <span data-ttu-id="d0919-277">有关 ASP.NET Core 的内置本地化支持，请参阅 <xref:fundamentals/localization>。</span><span class="sxs-lookup"><span data-stu-id="d0919-277">For ASP.NET Core's built-in localization support, see <xref:fundamentals/localization>.</span></span>

<span data-ttu-id="d0919-278">可通过传入区域性（如 `http://localhost:7997/?culture=no`）测试中间件。</span><span class="sxs-lookup"><span data-stu-id="d0919-278">You can test the middleware by passing in the culture, for example `http://localhost:7997/?culture=no`.</span></span>

<span data-ttu-id="d0919-279">以下代码将中间件委托移动到类：</span><span class="sxs-lookup"><span data-stu-id="d0919-279">The following code moves the middleware delegate to a class:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddleware.cs)]

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="d0919-280">中间件 `Task` 方法的名称必须是 `Invoke`。</span><span class="sxs-lookup"><span data-stu-id="d0919-280">The middleware `Task` method's name must be `Invoke`.</span></span> <span data-ttu-id="d0919-281">在 ASP.NET Core 2.0 或更高版本中，该名称可以为 `Invoke` 或 `InvokeAsync`。</span><span class="sxs-lookup"><span data-stu-id="d0919-281">In ASP.NET Core 2.0 or later, the name can be either `Invoke` or `InvokeAsync`.</span></span>

::: moniker-end

<span data-ttu-id="d0919-282">以下扩展方法通过 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 公开中间件：</span><span class="sxs-lookup"><span data-stu-id="d0919-282">The following extension method exposes the middleware through <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>:</span></span>

[!code-csharp[](index/snapshot/Culture/RequestCultureMiddlewareExtensions.cs)]

<span data-ttu-id="d0919-283">以下代码通过 `Startup.Configure` 调用中间件：</span><span class="sxs-lookup"><span data-stu-id="d0919-283">The following code calls the middleware from `Startup.Configure`:</span></span>

[!code-csharp[](index/snapshot/Culture/Startup.cs?name=snippet1&highlight=5)]

<span data-ttu-id="d0919-284">中间件应通过在其构造函数中公开其依赖项来遵循[显式依赖项原则](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies)。</span><span class="sxs-lookup"><span data-stu-id="d0919-284">Middleware should follow the [Explicit Dependencies Principle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#explicit-dependencies) by exposing its dependencies in its constructor.</span></span> <span data-ttu-id="d0919-285">在每个应用程序生存期构造一次中间件。</span><span class="sxs-lookup"><span data-stu-id="d0919-285">Middleware is constructed once per *application lifetime*.</span></span> <span data-ttu-id="d0919-286">如果需要与请求中的中间件共享服务，请参阅[按请求依赖项](#per-request-dependencies)部分。</span><span class="sxs-lookup"><span data-stu-id="d0919-286">See the [Per-request dependencies](#per-request-dependencies) section if you need to share services with middleware within a request.</span></span>

<span data-ttu-id="d0919-287">中间件组件可通过构造函数参数从[依赖关系注入 (DI)](xref:fundamentals/dependency-injection) 解析其依赖项。</span><span class="sxs-lookup"><span data-stu-id="d0919-287">Middleware components can resolve their dependencies from [dependency injection (DI)](xref:fundamentals/dependency-injection) through constructor parameters.</span></span> <span data-ttu-id="d0919-288">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) 也可直接接受其他参数。</span><span class="sxs-lookup"><span data-stu-id="d0919-288">[UseMiddleware&lt;T&gt;](/dotnet/api/microsoft.aspnetcore.builder.usemiddlewareextensions.usemiddleware#Microsoft_AspNetCore_Builder_UseMiddlewareExtensions_UseMiddleware_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Type_System_Object___) can also accept additional parameters directly.</span></span>

### <a name="per-request-dependencies"></a><span data-ttu-id="d0919-289">按请求依赖项</span><span class="sxs-lookup"><span data-stu-id="d0919-289">Per-request dependencies</span></span>

<span data-ttu-id="d0919-290">由于中间件是在应用启动时构造的，而不是按请求构造的，因此在每个请求过程中，中间件构造函数使用的范围内生存期服务不与其他依赖关系注入类型共享。</span><span class="sxs-lookup"><span data-stu-id="d0919-290">Because middleware is constructed at app startup, not per-request, *scoped* lifetime services used by middleware constructors aren't shared with other dependency-injected types during each request.</span></span> <span data-ttu-id="d0919-291">如果必须在中间件和其他类型之间共享范围内服务，请将这些服务添加到 `Invoke` 方法的签名。</span><span class="sxs-lookup"><span data-stu-id="d0919-291">If you must share a *scoped* service between your middleware and other types, add these services to the `Invoke` method's signature.</span></span> <span data-ttu-id="d0919-292">`Invoke` 方法可接受由 DI 填充的其他参数：</span><span class="sxs-lookup"><span data-stu-id="d0919-292">The `Invoke` method can accept additional parameters that are populated by DI:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="d0919-293">其他资源</span><span class="sxs-lookup"><span data-stu-id="d0919-293">Additional resources</span></span>

* <xref:migration/http-modules>
* <xref:fundamentals/startup>
* <xref:fundamentals/request-features>
* <xref:fundamentals/middleware/extensibility>
* <xref:fundamentals/middleware/extensibility-third-party-container>
