---
title: 处理 ASP.NET Core 中的错误
author: ardalis
description: 了解如何处理 ASP.NET Core 应用程序中的错误。
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 11/30/2016
uid: fundamentals/error-handling
ms.openlocfilehash: 2fe46ecc32d61a7fafb2ad6e2a35456476608251
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273704"
---
# <a name="handle-errors-in-aspnet-core"></a><span data-ttu-id="f4de8-103">处理 ASP.NET Core 中的错误</span><span class="sxs-lookup"><span data-stu-id="f4de8-103">Handle errors in ASP.NET Core</span></span>

<span data-ttu-id="f4de8-104">作者：[Steve Smith](https://ardalis.com/) 和 [Tom Dykstra](https://github.com/tdykstra/)</span><span class="sxs-lookup"><span data-stu-id="f4de8-104">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra/)</span></span>

<span data-ttu-id="f4de8-105">本文介绍了处理 ASP.NET Core 应用中常见错误的一些方法。</span><span class="sxs-lookup"><span data-stu-id="f4de8-105">This article covers common appoaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="f4de8-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="f4de8-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="the-developer-exception-page"></a><span data-ttu-id="f4de8-107">开发人员异常页</span><span class="sxs-lookup"><span data-stu-id="f4de8-107">The developer exception page</span></span>

<span data-ttu-id="f4de8-108">如需在应用中配置可以显示异常详细信息的页面，请先安装 `Microsoft.AspNetCore.Diagnostics` NuGet 包并将以下代码行添加到 Startup 类 [Startup 类配置方法](xref:fundamentals/startup)：</span><span class="sxs-lookup"><span data-stu-id="f4de8-108">To configure an app to display a page that shows detailed information about exceptions, install the `Microsoft.AspNetCore.Diagnostics` NuGet package and add a line to the [Configure method in the Startup class](xref:fundamentals/startup):</span></span>

[!code-csharp[](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

<span data-ttu-id="f4de8-109">`UseDeveloperExceptionPage` 需要放在所有你想要捕获异常的中间件声明之前，如`app.UseMvc`。</span><span class="sxs-lookup"><span data-stu-id="f4de8-109">Put `UseDeveloperExceptionPage` before any middleware you want to catch exceptions in, such as `app.UseMvc`.</span></span>

>[!WARNING]
> <span data-ttu-id="f4de8-110">**仅当应用程序在开发环境中运行时**才启用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="f4de8-110">Enable the developer exception page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="f4de8-111">否则当应用程序在生产环境中运行时，详细的异常信息会向公众泄露</span><span class="sxs-lookup"><span data-stu-id="f4de8-111">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="f4de8-112">了解[环境配置](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="f4de8-112">[Learn more about configuring environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="f4de8-113">若要查看开发人员异常页，可使用`Development`环境来运行应用程序，并在基础 URL 后添加`?throw=true`。</span><span class="sxs-lookup"><span data-stu-id="f4de8-113">To see the developer exception page, run the sample application with the environment set to `Development`, and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="f4de8-114">该页面包括几个选项卡，这些选项卡中包含关于异常和请求的信息。</span><span class="sxs-lookup"><span data-stu-id="f4de8-114">The page includes several tabs with information about the exception and the request.</span></span> <span data-ttu-id="f4de8-115">第一个选项卡包括堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="f4de8-115">The first tab includes a stack trace.</span></span> 

![堆栈跟踪](error-handling/_static/developer-exception-page.png)

<span data-ttu-id="f4de8-117">下一个`Query`选项卡将显示查询字符串参数信息（如有）。</span><span class="sxs-lookup"><span data-stu-id="f4de8-117">The next tab shows the query string parameters, if any.</span></span>

![查询字符串参数](error-handling/_static/developer-exception-page-query.png)

<span data-ttu-id="f4de8-119">示例请求没有任何 cookie，但如果有的话，它们将出现在 **Cookies**选项卡。最后一个选项卡显示请求的标头。</span><span class="sxs-lookup"><span data-stu-id="f4de8-119">This request didn't have any cookies, but if it did, they would appear on the **Cookies** tab. You can see the headers that were passed in the last tab.</span></span>

![标头](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a><span data-ttu-id="f4de8-121">配置自定义异常处理页</span><span class="sxs-lookup"><span data-stu-id="f4de8-121">Configuring a custom exception handling page</span></span>

<span data-ttu-id="f4de8-122">配置当应用未在 `Development` 环境中运行时要使用的异常处理程序页。</span><span class="sxs-lookup"><span data-stu-id="f4de8-122">Configure an exception handler page to use when the app isn't running in the `Development` environment.</span></span>

[!code-csharp[](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

<span data-ttu-id="f4de8-123">在 Razor Pages 应用中，[dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages 模板在 Pages 文件夹中提供“错误”页面和 `ErrorModel` 页面模型类。</span><span class="sxs-lookup"><span data-stu-id="f4de8-123">In a Razor Pages app, the [dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages template provides an Error page and `ErrorModel` page model class in the *Pages* folder.</span></span>

<span data-ttu-id="f4de8-124">在 MVC 应用中，不要使用 HTTP 方法特性（如 `HttpGet`）修饰错误处理程序操作方法。</span><span class="sxs-lookup"><span data-stu-id="f4de8-124">In an MVC app, don't decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="f4de8-125">显式谓词可阻止某些请求访问方法。</span><span class="sxs-lookup"><span data-stu-id="f4de8-125">Explicit verbs prevent some requests from reaching the method.</span></span> <span data-ttu-id="f4de8-126">允许匿名访问方法，以便未经身份验证的用户能够接收错误视图。</span><span class="sxs-lookup"><span data-stu-id="f4de8-126">Allow anonymous access to the method so that unauthenticated users are able to receive the error view.</span></span>

<span data-ttu-id="f4de8-127">例如，以下错误处理程序方法由 [dotnet new](/dotnet/core/tools/dotnet-new) MVC 模板提供并在主控制器中显示：</span><span class="sxs-lookup"><span data-stu-id="f4de8-127">For example, the following error handler method is provided by the [dotnet new](/dotnet/core/tools/dotnet-new) MVC template and appears in the Home controller:</span></span>

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

## <a name="configuring-status-code-pages"></a><span data-ttu-id="f4de8-128">配置状态代码页</span><span class="sxs-lookup"><span data-stu-id="f4de8-128">Configuring status code pages</span></span>

<span data-ttu-id="f4de8-129">默认情况下，应用不会为 HTTP 状态代码提供丰富状态代码页，例如 404 未找到。</span><span class="sxs-lookup"><span data-stu-id="f4de8-129">By default, an app doesn't provide a rich status code page for HTTP status codes, such as *404 Not Found*.</span></span> <span data-ttu-id="f4de8-130">要提供状态代码页，请通过向 `Startup.Configure` 方法添加行来配置状态代码页中间件：</span><span class="sxs-lookup"><span data-stu-id="f4de8-130">To provide status code pages, configure the Status Code Pages Middleware by adding a line to the `Startup.Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="f4de8-131">默认情况下，状态代码页中间件为常见状态代码（如 404）添加简单的纯文本处理程序：</span><span class="sxs-lookup"><span data-stu-id="f4de8-131">By default, Status Code Pages Middleware adds simple, text-only handlers for common status codes, such as 404:</span></span>

![404 页面](error-handling/_static/default-404-status-code.png)

<span data-ttu-id="f4de8-133">该中间件支持多种扩展方法。</span><span class="sxs-lookup"><span data-stu-id="f4de8-133">The middleware supports several extension methods.</span></span> <span data-ttu-id="f4de8-134">一种方法采用 Lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="f4de8-134">One method takes a lambda expression:</span></span>

[!code-csharp[](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

<span data-ttu-id="f4de8-135">另一种方法采用内容类型和格式字符串：</span><span class="sxs-lookup"><span data-stu-id="f4de8-135">Another method takes a content type and format string:</span></span>

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

<span data-ttu-id="f4de8-136">也可以使用重定向和重新执行扩展方法。</span><span class="sxs-lookup"><span data-stu-id="f4de8-136">There are also redirect and re-execute extension methods.</span></span> <span data-ttu-id="f4de8-137">重定向方法向客户端发送 302 状态代码：</span><span class="sxs-lookup"><span data-stu-id="f4de8-137">The redirect method sends a 302 status code to the client:</span></span>

[!code-csharp[](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

<span data-ttu-id="f4de8-138">重新执行方法将原始状态代码返回到客户端，但同时还会执行重定向 URL 的处理程序：</span><span class="sxs-lookup"><span data-stu-id="f4de8-138">The re-execute method returns the original status code to the client but also executes the handler for the redirect URL:</span></span>

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

<span data-ttu-id="f4de8-139">可禁用 Razor 页处理程序方法或 MVC 控制器中的特定请求的状态代码页。</span><span class="sxs-lookup"><span data-stu-id="f4de8-139">Status code pages can be disabled for specific requests in a Razor Pages handler method or in an MVC controller.</span></span> <span data-ttu-id="f4de8-140">要禁用状态代码页，请尝试从请求的 [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) 集合中检索 [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature)，并在功能可用时禁用该功能：</span><span class="sxs-lookup"><span data-stu-id="f4de8-140">To disable status code pages, attempt to retrieve the [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature) from the request's [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) collection and disable the feature if it's available:</span></span>

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

<span data-ttu-id="f4de8-141">如果使用指向应用中的终结点的 `UseStatusCodePages*` 重载，请为该终结点创建 MVC 视图或 Razor Page。</span><span class="sxs-lookup"><span data-stu-id="f4de8-141">If using a `UseStatusCodePages*` overload that points to an endpoint within the app, create an MVC view or Razor Page for the endpoint.</span></span> <span data-ttu-id="f4de8-142">例如，Razor Pages 应用的 [dotnet new](/dotnet/core/tools/dotnet-new) 模板将生成以下页面和页面模型类：</span><span class="sxs-lookup"><span data-stu-id="f4de8-142">For example, the [dotnet new](/dotnet/core/tools/dotnet-new) template for a Razor Pages app produces the following page and page model class:</span></span>

<span data-ttu-id="f4de8-143">Error.cshtml：</span><span class="sxs-lookup"><span data-stu-id="f4de8-143">*Error.cshtml*:</span></span>

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
    Swapping to <strong>Development</strong> environment will display more detailed information about the error that occurred.
</p>
<p>
    <strong>Development environment should not be enabled in deployed applications</strong>, as it can result in sensitive information from exceptions being displayed to end users. For local debugging, development environment can be enabled by setting the <strong>ASPNETCORE_ENVIRONMENT</strong> environment variable to <strong>Development</strong>, and restarting the application.
</p>
```

<span data-ttu-id="f4de8-144">Error.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="f4de8-144">*Error.cshtml.cs*:</span></span>

```csharp
public class ErrorModel : PageModel
{
    public string RequestId { get; set; }

    public bool ShowRequestId => !string.IsNullOrEmpty(RequestId);

    [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, NoStore = true)]
    public void OnGet()
    {
        RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier;
    }
}
```

## <a name="exception-handling-code"></a><span data-ttu-id="f4de8-145">异常处理代码</span><span class="sxs-lookup"><span data-stu-id="f4de8-145">Exception-handling code</span></span>

<span data-ttu-id="f4de8-146">异常处理页中的代码可能会引发异常。</span><span class="sxs-lookup"><span data-stu-id="f4de8-146">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="f4de8-147">建议在生产错误页面中包含纯静态内容。</span><span class="sxs-lookup"><span data-stu-id="f4de8-147">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="f4de8-148">此外还要注意，一旦发送响应的标头，则无法更改响应的状态代码，也不能运行任何异常页或处理程序。</span><span class="sxs-lookup"><span data-stu-id="f4de8-148">Also, be aware that once the headers for a response have been sent, you can't change the response's status code, nor can any exception pages or handlers run.</span></span> <span data-ttu-id="f4de8-149">必须完成响应或中止连接。</span><span class="sxs-lookup"><span data-stu-id="f4de8-149">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="f4de8-150">服务器异常处理</span><span class="sxs-lookup"><span data-stu-id="f4de8-150">Server exception handling</span></span>

<span data-ttu-id="f4de8-151">除应用程序中的异常处理逻辑外，托管应用程序的服务器[服务器](xref:fundamentals/servers/index)也会执行一些异常处理。</span><span class="sxs-lookup"><span data-stu-id="f4de8-151">In addition to the exception handling logic in your app, the [server](xref:fundamentals/servers/index) hosting your app performs some exception handling.</span></span> <span data-ttu-id="f4de8-152">如果服务器在发送标头之前捕获异常，服务器将发送没有正文的 500 内部服务器错误响应。</span><span class="sxs-lookup"><span data-stu-id="f4de8-152">If the server catches an exception before the headers are sent, the server sends a *500 Internal Server Error* response with no body.</span></span> <span data-ttu-id="f4de8-153">如果服务器在已发送标头后捕获异常，服务器会关闭连接。</span><span class="sxs-lookup"><span data-stu-id="f4de8-153">If the server catches an exception after the headers have been sent, the server closes the connection.</span></span> <span data-ttu-id="f4de8-154">应用程序无法处理的请求将由服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="f4de8-154">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="f4de8-155">发生的任何异常都将由服务器进行处理。</span><span class="sxs-lookup"><span data-stu-id="f4de8-155">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="f4de8-156">任何配置的自定义错误页面或异常处理中间件或筛选器都不会影响此行为。</span><span class="sxs-lookup"><span data-stu-id="f4de8-156">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="f4de8-157">启动异常处理</span><span class="sxs-lookup"><span data-stu-id="f4de8-157">Startup exception handling</span></span>

<span data-ttu-id="f4de8-158">应用程序启动期间发生的异常仅可在承载层进行处理。</span><span class="sxs-lookup"><span data-stu-id="f4de8-158">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="f4de8-159">利用 [Web](xref:fundamentals/host/web-host) 主机，你可以使用 `captureStartupErrors` 和 `detailedErrors` 键[配置主机在响应启动期间出现错误时的行为方式](xref:fundamentals/host/web-host#detailed-errors)。</span><span class="sxs-lookup"><span data-stu-id="f4de8-159">Using the [Web Host](xref:fundamentals/host/web-host), you can [configure how the host behaves in response to errors during startup](xref:fundamentals/host/web-host#detailed-errors) with the `captureStartupErrors` and `detailedErrors` keys.</span></span>

<span data-ttu-id="f4de8-160">仅当捕获的启动错误发生在主机地址/端口绑定之后，承载层才会为该错误显示错误页。</span><span class="sxs-lookup"><span data-stu-id="f4de8-160">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="f4de8-161">如果绑定因任何原因而失败，则承载层会记录关键异常，dotnet 进程崩溃，且在 [Kestrel](xref:fundamentals/servers/kestrel) 服务器上运行应用时，不会显示任何错误页。</span><span class="sxs-lookup"><span data-stu-id="f4de8-161">If any binding fails for any reason, the hosting layer logs a critical exception, the dotnet process crashes, and no error page is displayed when the app is running on the [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span>

<span data-ttu-id="f4de8-162">在 [IIS](/iis) 或 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 上运行应用时，如果无法启动进程，[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)将返回 502.5 进程失败。</span><span class="sxs-lookup"><span data-stu-id="f4de8-162">When running on [IIS](/iis) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), a *502.5 Process Failure* is returned by the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) if the process can't be started.</span></span> <span data-ttu-id="f4de8-163">请按照[对 IIS 上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/iis/troubleshoot)主题中的故障排除建议进行操作。</span><span class="sxs-lookup"><span data-stu-id="f4de8-163">Follow the troubleshooting advice in the [Troubleshoot ASP.NET Core on IIS](xref:host-and-deploy/iis/troubleshoot) topic.</span></span>

## <a name="aspnet-mvc-error-handling"></a><span data-ttu-id="f4de8-164">ASP.NET MVC 错误处理</span><span class="sxs-lookup"><span data-stu-id="f4de8-164">ASP.NET MVC error handling</span></span>

<span data-ttu-id="f4de8-165">[MVC](xref:mvc/overview) 应用还有一些其他的错误处理选项，例如配置异常筛选器和执行模型验证。</span><span class="sxs-lookup"><span data-stu-id="f4de8-165">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="f4de8-166">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="f4de8-166">Exception Filters</span></span>

<span data-ttu-id="f4de8-167">在 MVC 应用中，异常筛选器可以进行全局配置，也可以为每个控制器或每个操作单独配置。</span><span class="sxs-lookup"><span data-stu-id="f4de8-167">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="f4de8-168">这些筛选器处理在执行控制器操作或其他筛选器时出现的任何未处理的异常，且不会以其他方式调用。</span><span class="sxs-lookup"><span data-stu-id="f4de8-168">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter, and are not called otherwise.</span></span> <span data-ttu-id="f4de8-169">通过[筛选器](xref:mvc/controllers/filters)详细了解异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="f4de8-169">Learn more about exception filters in [Filters](xref:mvc/controllers/filters).</span></span>

> [!TIP]
> <span data-ttu-id="f4de8-170">异常筛选器非常适用于捕获 MVC 操作内出现的异常，但灵活性不如错误处理中间件。</span><span class="sxs-lookup"><span data-stu-id="f4de8-170">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="f4de8-171">一般情况下建议使用中间件；仅在需要根据所选 MVC 操作以不同方式执行错误处理时，才使用筛选器。</span><span class="sxs-lookup"><span data-stu-id="f4de8-171">Prefer middleware for the general case, and use filters only where you need to do error handling *differently* based on which MVC action was chosen.</span></span>

### <a name="handling-model-state-errors"></a><span data-ttu-id="f4de8-172">处理模型状态错误</span><span class="sxs-lookup"><span data-stu-id="f4de8-172">Handling Model State Errors</span></span>

<span data-ttu-id="f4de8-173">[模型验证](xref:mvc/models/validation)在每个控制器操作被调用之前发生，操作方法负责检查 `ModelState.IsValid` 并相应地作出反应。</span><span class="sxs-lookup"><span data-stu-id="f4de8-173">[Model validation](xref:mvc/models/validation) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span>

<span data-ttu-id="f4de8-174">某些应用会使用标准约定来处理模型验证错误，在这种情况下，使用[筛选器](xref:mvc/controllers/filters)可以更好地实施这种策略。</span><span class="sxs-lookup"><span data-stu-id="f4de8-174">Some apps will choose to follow a standard convention for dealing with model validation errors, in which case a [filter](xref:mvc/controllers/filters) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="f4de8-175">你需要使用无效模型状态测试操作的行为。</span><span class="sxs-lookup"><span data-stu-id="f4de8-175">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="f4de8-176">查看[测试控制器逻辑](xref:mvc/controllers/testing)了解详情。</span><span class="sxs-lookup"><span data-stu-id="f4de8-176">Learn more in [Test controller logic](xref:mvc/controllers/testing).</span></span>
