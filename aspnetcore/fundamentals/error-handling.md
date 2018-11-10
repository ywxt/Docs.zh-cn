---
title: 处理 ASP.NET Core 中的错误
author: tdykstra
description: 了解如何处理 ASP.NET Core 应用中的错误。
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/01/2018
uid: fundamentals/error-handling
ms.openlocfilehash: 89117d78486493747d649c3bb0d9cce9f97ef419
ms.sourcegitcommit: 85f2939af7a167b9694e1d2093277ffc9a741b23
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "50968314"
---
# <a name="handle-errors-in-aspnet-core"></a><span data-ttu-id="d5dca-103">处理 ASP.NET Core 中的错误</span><span class="sxs-lookup"><span data-stu-id="d5dca-103">Handle errors in ASP.NET Core</span></span>

<span data-ttu-id="d5dca-104">作者：[Steve Smith](https://ardalis.com/) 和 [Tom Dykstra](https://github.com/tdykstra/)</span><span class="sxs-lookup"><span data-stu-id="d5dca-104">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra/)</span></span>

<span data-ttu-id="d5dca-105">本文介绍了处理 ASP.NET Core 应用中常见错误的一些方法。</span><span class="sxs-lookup"><span data-stu-id="d5dca-105">This article covers common approaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="d5dca-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x/ErrorHandlingSample)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="d5dca-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x/ErrorHandlingSample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="the-developer-exception-page"></a><span data-ttu-id="d5dca-107">开发人员异常页</span><span class="sxs-lookup"><span data-stu-id="d5dca-107">The Developer Exception Page</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="d5dca-108">要将应用配置为显示有关异常的详细信息的页面，请使用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-108">To configure an app to display a page that shows detailed information about exceptions, use the *Developer Exception Page*.</span></span> <span data-ttu-id="d5dca-109">该页面通过 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中的 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-109">The page is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="d5dca-110">向 `Startup.Configure` 方法添加代码行：</span><span class="sxs-lookup"><span data-stu-id="d5dca-110">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="d5dca-111">要将应用配置为显示有关异常的详细信息的页面，请使用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-111">To configure an app to display a page that shows detailed information about exceptions, use the *Developer Exception Page*.</span></span> <span data-ttu-id="d5dca-112">该页面通过 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中的 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-112">The page is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="d5dca-113">向 `Startup.Configure` 方法添加代码行：</span><span class="sxs-lookup"><span data-stu-id="d5dca-113">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="d5dca-114">要将应用配置为显示有关异常的详细信息的页面，请使用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-114">To configure an app to display a page that shows detailed information about exceptions, use the *Developer Exception Page*.</span></span> <span data-ttu-id="d5dca-115">该页面通过在项目文件中添加 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包的包引用提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-115">The page is made available by adding a package reference for the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package in the project file.</span></span> <span data-ttu-id="d5dca-116">向 `Startup.Configure` 方法添加代码行：</span><span class="sxs-lookup"><span data-stu-id="d5dca-116">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

<span data-ttu-id="d5dca-117">将对 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 的调用放在要对其捕获异常的任何中间件（例如，`app.UseMvc`）前面。</span><span class="sxs-lookup"><span data-stu-id="d5dca-117">Place the call to [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) in front of any middleware where you want to catch exceptions, such as `app.UseMvc`.</span></span>

> [!WARNING]
> <span data-ttu-id="d5dca-118">仅当应用程序在开发环境中运行时才启用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-118">Enable the Developer Exception Page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="d5dca-119">否则当应用程序在生产环境中运行时，详细的异常信息会向公众泄露</span><span class="sxs-lookup"><span data-stu-id="d5dca-119">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="d5dca-120">了解[环境配置](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="d5dca-120">[Learn more about configuring environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="d5dca-121">要查看开发人员异常页，请将环境设置为 `Development`，运行示例应用，并向应用的基 URL 添加 `?throw=true`。</span><span class="sxs-lookup"><span data-stu-id="d5dca-121">To see the Developer Exception Page, run the sample app with the environment set to `Development` and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="d5dca-122">该页面包括几个选项卡，这些选项卡中包含关于异常和请求的信息。</span><span class="sxs-lookup"><span data-stu-id="d5dca-122">The page includes several tabs with information about the exception and the request.</span></span> <span data-ttu-id="d5dca-123">第一个选项卡包括堆栈跟踪：</span><span class="sxs-lookup"><span data-stu-id="d5dca-123">The first tab includes a stack trace:</span></span>

![堆栈跟踪](error-handling/_static/developer-exception-page.png)

<span data-ttu-id="d5dca-125">下一个选项卡显示查询字符串参数（如有）：</span><span class="sxs-lookup"><span data-stu-id="d5dca-125">The next tab shows the query string parameters, if any:</span></span>

![查询字符串参数](error-handling/_static/developer-exception-page-query.png)

<span data-ttu-id="d5dca-127">如果请求具有 cookie，它们在“Cookie”选项卡上显示。标头出现在最后一个选项卡中：</span><span class="sxs-lookup"><span data-stu-id="d5dca-127">If the request has cookies, they appear on the **Cookies** tab. Headers are seen in the last tab:</span></span>

![标头](error-handling/_static/developer-exception-page-headers.png)

## <a name="configure-a-custom-exception-handling-page"></a><span data-ttu-id="d5dca-129">配置自定义异常处理页</span><span class="sxs-lookup"><span data-stu-id="d5dca-129">Configure a custom exception handling page</span></span>

<span data-ttu-id="d5dca-130">配置当应用未在 `Development` 环境中运行时要使用的异常处理程序页：</span><span class="sxs-lookup"><span data-stu-id="d5dca-130">Configure an exception handler page to use when the app isn't running in the `Development` environment:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

<span data-ttu-id="d5dca-131">在 Razor Pages 应用中，[dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages 模板在 Pages 文件夹中提供“错误”页面和错误 `PageModel` 类。</span><span class="sxs-lookup"><span data-stu-id="d5dca-131">In a Razor Pages app, the [dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages template provides an Error page and an error `PageModel` class in the *Pages* folder.</span></span>

<span data-ttu-id="d5dca-132">在 MVC 应用中，不要使用 HTTP 方法特性（如 `HttpGet`）修饰错误处理程序操作方法。</span><span class="sxs-lookup"><span data-stu-id="d5dca-132">In an MVC app, don't decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="d5dca-133">显式谓词可阻止某些请求访问方法。</span><span class="sxs-lookup"><span data-stu-id="d5dca-133">Explicit verbs prevent some requests from reaching the method.</span></span> <span data-ttu-id="d5dca-134">允许匿名访问方法，以便未经身份验证的用户能够接收错误视图。</span><span class="sxs-lookup"><span data-stu-id="d5dca-134">Allow anonymous access to the method so that unauthenticated users are able to receive the error view.</span></span>

<span data-ttu-id="d5dca-135">例如，以下错误处理程序方法由 [dotnet new](/dotnet/core/tools/dotnet-new) MVC 模板提供并在主控制器中显示：</span><span class="sxs-lookup"><span data-stu-id="d5dca-135">For example, the following error handler method is provided by the [dotnet new](/dotnet/core/tools/dotnet-new) MVC template and appears in the Home controller:</span></span>

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel 
        { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

## <a name="configure-status-code-pages"></a><span data-ttu-id="d5dca-136">配置状态代码页</span><span class="sxs-lookup"><span data-stu-id="d5dca-136">Configure status code pages</span></span>

<span data-ttu-id="d5dca-137">默认情况下，应用不会为 HTTP 状态代码提供丰富状态代码页，例如 404 未找到。</span><span class="sxs-lookup"><span data-stu-id="d5dca-137">By default, an app doesn't provide a rich status code page for HTTP status codes, such as *404 Not Found*.</span></span> <span data-ttu-id="d5dca-138">要提供状态代码页，请使用状态代码页中间件。</span><span class="sxs-lookup"><span data-stu-id="d5dca-138">To provide status code pages, use Status Code Pages Middleware.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="d5dca-139">该中间件通过 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中的 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-139">The middleware is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="d5dca-140">该中间件通过 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中的 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-140">The middleware is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="d5dca-141">该中间件通过在项目文件中添加 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 包的包引用提供。</span><span class="sxs-lookup"><span data-stu-id="d5dca-141">The middleware is made available by adding a package reference for the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package in the project file.</span></span>

::: moniker-end

<span data-ttu-id="d5dca-142">向 `Startup.Configure` 方法添加代码行：</span><span class="sxs-lookup"><span data-stu-id="d5dca-142">Add a line to the `Startup.Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="d5dca-143">应在管道中的请求处理中间件之前调用 <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>（例如，静态文件中间件和 MVC 中间件）。</span><span class="sxs-lookup"><span data-stu-id="d5dca-143"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> should be called before request handling middlewares in the pipeline (for example, Static Files Middleware and MVC Middleware).</span></span>

<span data-ttu-id="d5dca-144">默认情况下，状态代码页中间件为常见状态代码（如 404）添加纯文本处理程序：</span><span class="sxs-lookup"><span data-stu-id="d5dca-144">By default, Status Code Pages Middleware adds text-only handlers for common status codes, such as 404:</span></span>

![404 页面](error-handling/_static/default-404-status-code.png)

<span data-ttu-id="d5dca-146">该中间件支持多种扩展方法。</span><span class="sxs-lookup"><span data-stu-id="d5dca-146">The middleware supports several extension methods.</span></span> <span data-ttu-id="d5dca-147">一种方法采用 Lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="d5dca-147">One method takes a lambda expression:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePages)]

<span data-ttu-id="d5dca-148">`UseStatusCodePages` 重载需要使用内容类型和格式字符串：</span><span class="sxs-lookup"><span data-stu-id="d5dca-148">An overload of `UseStatusCodePages` takes a content type and format string:</span></span>

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```
### <a name="redirect-re-execute-extension-methods"></a><span data-ttu-id="d5dca-149">重定向重新执行扩展方法</span><span class="sxs-lookup"><span data-stu-id="d5dca-149">Redirect re-execute extension methods</span></span>

<span data-ttu-id="d5dca-150"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>：</span><span class="sxs-lookup"><span data-stu-id="d5dca-150"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>:</span></span>

* <span data-ttu-id="d5dca-151">向客户端发送“302 - 已找到”状态代码。</span><span class="sxs-lookup"><span data-stu-id="d5dca-151">Sends a *302 - Found* status code to the client.</span></span>
* <span data-ttu-id="d5dca-152">将客户端重定向到 URL 模板中的位置。</span><span class="sxs-lookup"><span data-stu-id="d5dca-152">Redirects the client to the location provided in the URL template.</span></span> 

<span data-ttu-id="d5dca-153">该模板可能包括状态代码的 `{0}` 占位符。</span><span class="sxs-lookup"><span data-stu-id="d5dca-153">The template may include a `{0}` placeholder for the status code.</span></span> <span data-ttu-id="d5dca-154">模板必须以正斜杠 (`/`) 开头。</span><span class="sxs-lookup"><span data-stu-id="d5dca-154">The template must start with a forward slash (`/`).</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

<span data-ttu-id="d5dca-155"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>：</span><span class="sxs-lookup"><span data-stu-id="d5dca-155"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>:</span></span>

* <span data-ttu-id="d5dca-156">向客户端返回原始状态代码。</span><span class="sxs-lookup"><span data-stu-id="d5dca-156">Returns the original status code to the client.</span></span>
* <span data-ttu-id="d5dca-157">指定应使用备用路径重新执行请求管道，从而生成响应正文。</span><span class="sxs-lookup"><span data-stu-id="d5dca-157">Specifies that the response body should be generated by re-executing the request pipeline using an alternate path.</span></span> 

<span data-ttu-id="d5dca-158">该模板可能包括状态代码的 `{0}` 占位符。</span><span class="sxs-lookup"><span data-stu-id="d5dca-158">The template may include a `{0}` placeholder for the status code.</span></span> <span data-ttu-id="d5dca-159">模板必须以正斜杠 (`/`) 开头。</span><span class="sxs-lookup"><span data-stu-id="d5dca-159">The template must start with a forward slash (`/`).</span></span>

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

<span data-ttu-id="d5dca-160">可禁用 Razor 页处理程序方法或 MVC 控制器中的特定请求的状态代码页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-160">Status code pages can be disabled for specific requests in a Razor Pages handler method or in an MVC controller.</span></span> <span data-ttu-id="d5dca-161">要禁用状态代码页，请尝试从请求的 [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) 集合中检索 [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature)，并在功能可用时禁用该功能：</span><span class="sxs-lookup"><span data-stu-id="d5dca-161">To disable status code pages, attempt to retrieve the [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature) from the request's [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) collection and disable the feature if it's available:</span></span>

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

<span data-ttu-id="d5dca-162">若要在应用中使用指向终结点的 `UseStatusCodePages*` 重载，请为终结点创建 MVC 视图或 Razor Page。</span><span class="sxs-lookup"><span data-stu-id="d5dca-162">To use a `UseStatusCodePages*` overload that points to an endpoint within the app, create an MVC view or Razor Page for the endpoint.</span></span> <span data-ttu-id="d5dca-163">例如，Razor Pages 应用的 [dotnet new](/dotnet/core/tools/dotnet-new) 模板将生成以下页面和页面模型类：</span><span class="sxs-lookup"><span data-stu-id="d5dca-163">For example, the [dotnet new](/dotnet/core/tools/dotnet-new) template for a Razor Pages app produces the following page and page model class:</span></span>

<span data-ttu-id="d5dca-164">Error.cshtml：</span><span class="sxs-lookup"><span data-stu-id="d5dca-164">*Error.cshtml*:</span></span>

```cshtml
@page
@model ErrorModel
@{
    ViewData["Title"] = "Error";
}

<h1 class="text-danger">Error.</h1>
<h2 class="text-danger">An error occurred while processing your request.</h2>

@if (Model.ShowRequestId)
{
    <p>
        <strong>Request ID:</strong> <code>@Model.RequestId</code>
    </p>
}

<h3>Development Mode</h3>
<p>
    Swapping to <strong>Development</strong> environment will display more detailed 
    information about the error that occurred.
</p>
<p>
    <strong>Development environment should not be enabled in deployed applications
    </strong>, as it can result in sensitive information from exceptions being 
    displayed to end users. For local debugging, development environment can be 
    enabled by setting the <strong>ASPNETCORE_ENVIRONMENT</strong> environment 
    variable to <strong>Development</strong>, and restarting the application.
</p>
```

<span data-ttu-id="d5dca-165">Error.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="d5dca-165">*Error.cshtml.cs*:</span></span>

```csharp
public class ErrorModel : PageModel
{
    public string RequestId { get; set; }

    public bool ShowRequestId => !string.IsNullOrEmpty(RequestId);

    [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, 
        NoStore = true)]
    public void OnGet()
    {
        RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier;
    }
}
```

## <a name="exception-handling-code"></a><span data-ttu-id="d5dca-166">异常处理代码</span><span class="sxs-lookup"><span data-stu-id="d5dca-166">Exception-handling code</span></span>

<span data-ttu-id="d5dca-167">异常处理页中的代码可能会引发异常。</span><span class="sxs-lookup"><span data-stu-id="d5dca-167">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="d5dca-168">建议在生产错误页面中包含纯静态内容。</span><span class="sxs-lookup"><span data-stu-id="d5dca-168">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="d5dca-169">此外还要注意，一旦发送响应的标头，则无法更改响应的状态代码，也不能运行任何异常页或处理程序。</span><span class="sxs-lookup"><span data-stu-id="d5dca-169">Also, be aware that once the headers for a response have been sent, you can't change the response's status code, nor can any exception pages or handlers run.</span></span> <span data-ttu-id="d5dca-170">必须完成响应或中止连接。</span><span class="sxs-lookup"><span data-stu-id="d5dca-170">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="d5dca-171">服务器异常处理</span><span class="sxs-lookup"><span data-stu-id="d5dca-171">Server exception handling</span></span>

<span data-ttu-id="d5dca-172">除应用程序中的异常处理逻辑外，托管应用程序的服务器[服务器](xref:fundamentals/servers/index)也会执行一些异常处理。</span><span class="sxs-lookup"><span data-stu-id="d5dca-172">In addition to the exception handling logic in your app, the [server](xref:fundamentals/servers/index) hosting your app performs some exception handling.</span></span> <span data-ttu-id="d5dca-173">如果服务器在发送标头之前捕获异常，服务器将发送没有正文的 500 内部服务器错误响应。</span><span class="sxs-lookup"><span data-stu-id="d5dca-173">If the server catches an exception before the headers are sent, the server sends a *500 Internal Server Error* response with no body.</span></span> <span data-ttu-id="d5dca-174">如果服务器在已发送标头后捕获异常，服务器会关闭连接。</span><span class="sxs-lookup"><span data-stu-id="d5dca-174">If the server catches an exception after the headers have been sent, the server closes the connection.</span></span> <span data-ttu-id="d5dca-175">应用程序无法处理的请求将由服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="d5dca-175">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="d5dca-176">发生的任何异常都将由服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="d5dca-176">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="d5dca-177">任何配置的自定义错误页面或异常处理中间件或筛选器都不会影响此行为。</span><span class="sxs-lookup"><span data-stu-id="d5dca-177">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="d5dca-178">启动异常处理</span><span class="sxs-lookup"><span data-stu-id="d5dca-178">Startup exception handling</span></span>

<span data-ttu-id="d5dca-179">应用程序启动期间发生的异常仅可在承载层进行处理。</span><span class="sxs-lookup"><span data-stu-id="d5dca-179">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="d5dca-180">利用 [Web](xref:fundamentals/host/web-host) 主机，你可以使用 `captureStartupErrors` 和 `detailedErrors` 键[配置主机在响应启动期间出现错误时的行为方式](xref:fundamentals/host/web-host#detailed-errors)。</span><span class="sxs-lookup"><span data-stu-id="d5dca-180">Using the [Web Host](xref:fundamentals/host/web-host), you can [configure how the host behaves in response to errors during startup](xref:fundamentals/host/web-host#detailed-errors) with the `captureStartupErrors` and `detailedErrors` keys.</span></span>

<span data-ttu-id="d5dca-181">仅当捕获的启动错误发生在主机地址/端口绑定之后，承载层才会为该错误显示错误页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-181">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="d5dca-182">如果绑定因任何原因而失败，则承载层会记录关键异常，dotnet 进程崩溃，且在 [Kestrel](xref:fundamentals/servers/kestrel) 服务器上运行应用时，不会显示任何错误页。</span><span class="sxs-lookup"><span data-stu-id="d5dca-182">If any binding fails for any reason, the hosting layer logs a critical exception, the dotnet process crashes, and no error page is displayed when the app is running on the [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span>

<span data-ttu-id="d5dca-183">在 [IIS](/iis) 或 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 上运行应用时，如果无法启动进程，[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)将返回 502.5 进程失败。</span><span class="sxs-lookup"><span data-stu-id="d5dca-183">When running on [IIS](/iis) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), a *502.5 Process Failure* is returned by the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) if the process can't be started.</span></span> <span data-ttu-id="d5dca-184">要了解在通过 IIS 托管时如何排查启动问题，请参阅 <xref:host-and-deploy/iis/troubleshoot>。</span><span class="sxs-lookup"><span data-stu-id="d5dca-184">For information on troubleshooting startup issues when hosting with IIS, see <xref:host-and-deploy/iis/troubleshoot>.</span></span> <span data-ttu-id="d5dca-185">要了解如何排查 Azure 应用服务的启动问题，请参阅 <xref:host-and-deploy/azure-apps/troubleshoot>。</span><span class="sxs-lookup"><span data-stu-id="d5dca-185">For information on troubleshooting startup issues with Azure App Service, see <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>

## <a name="aspnet-core-mvc-error-handling"></a><span data-ttu-id="d5dca-186">ASP.NET Core MVC 错误处理</span><span class="sxs-lookup"><span data-stu-id="d5dca-186">ASP.NET Core MVC error handling</span></span>

<span data-ttu-id="d5dca-187">[MVC](xref:mvc/overview) 应用还有一些其他的错误处理选项，例如配置异常筛选器和执行模型验证。</span><span class="sxs-lookup"><span data-stu-id="d5dca-187">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="d5dca-188">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="d5dca-188">Exception filters</span></span>

<span data-ttu-id="d5dca-189">在 MVC 应用中，异常筛选器可以进行全局配置，也可以为每个控制器或每个操作单独配置。</span><span class="sxs-lookup"><span data-stu-id="d5dca-189">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="d5dca-190">这些筛选器处理在执行控制器操作或其他筛选器时出现的任何未处理的异常。</span><span class="sxs-lookup"><span data-stu-id="d5dca-190">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter.</span></span> <span data-ttu-id="d5dca-191">不会以其他方式调用这些筛选器。</span><span class="sxs-lookup"><span data-stu-id="d5dca-191">These filters aren't called otherwise.</span></span> <span data-ttu-id="d5dca-192">要了解详细信息，请参阅[筛选器](xref:mvc/controllers/filters)。</span><span class="sxs-lookup"><span data-stu-id="d5dca-192">To learn more, see [Filters](xref:mvc/controllers/filters).</span></span>

> [!TIP]
> <span data-ttu-id="d5dca-193">异常筛选器非常适用于捕获 MVC 操作内出现的异常，但灵活性不如错误处理中间件。</span><span class="sxs-lookup"><span data-stu-id="d5dca-193">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="d5dca-194">一般情况下最好使用中间件；仅在需要根据所选 MVC 操作以不同方式执行错误处理时，才使用筛选器。</span><span class="sxs-lookup"><span data-stu-id="d5dca-194">Generally prefer the use of middleware, and use filters only where you need to perform error handling *differently* based on which MVC action is chosen.</span></span>

### <a name="handling-model-state-errors"></a><span data-ttu-id="d5dca-195">处理模型状态错误</span><span class="sxs-lookup"><span data-stu-id="d5dca-195">Handling model state errors</span></span>

<span data-ttu-id="d5dca-196">[模型验证](xref:mvc/models/validation)在每个控制器操作被调用之前发生，操作方法负责检查 `ModelState.IsValid` 并相应地作出反应。</span><span class="sxs-lookup"><span data-stu-id="d5dca-196">[Model validation](xref:mvc/models/validation) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span>

<span data-ttu-id="d5dca-197">某些应用使用标准约定处理模型验证错误，在这种情况下，使用[筛选器](xref:mvc/controllers/filters)可以更好地实施这种策略。</span><span class="sxs-lookup"><span data-stu-id="d5dca-197">Some apps choose to follow a standard convention for dealing with model validation errors, in which case a [filter](xref:mvc/controllers/filters) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="d5dca-198">你需要使用无效模型状态测试操作的行为。</span><span class="sxs-lookup"><span data-stu-id="d5dca-198">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="d5dca-199">查看[测试控制器逻辑](xref:mvc/controllers/testing)了解详情。</span><span class="sxs-lookup"><span data-stu-id="d5dca-199">Learn more in [Test controller logic](xref:mvc/controllers/testing).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5dca-200">其他资源</span><span class="sxs-lookup"><span data-stu-id="d5dca-200">Additional resources</span></span>

* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
