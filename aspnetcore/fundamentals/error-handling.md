---
title: "ASP.NET Core 中的错误处理"
author: ardalis
description: "了解如何处理 ASP.NET Core 应用程序中的错误。"
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 11/30/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/error-handling
ms.openlocfilehash: 5b0cda7b79b8a9523d1ba6a9b321d22d3ccc753a
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-error-handling-in-aspnet-core"></a><span data-ttu-id="e4dda-103">ASP.NET Core 中的错误处理简介</span><span class="sxs-lookup"><span data-stu-id="e4dda-103">Introduction to Error Handling in ASP.NET Core</span></span>

<span data-ttu-id="e4dda-104">作者：[Steve Smith](https://ardalis.com/) 和 [Tom Dykstra](https://github.com/tdykstra/)</span><span class="sxs-lookup"><span data-stu-id="e4dda-104">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra/)</span></span>

<span data-ttu-id="e4dda-105">本文介绍了在 ASP.NET Core 应用中处理错误的常见方法。</span><span class="sxs-lookup"><span data-stu-id="e4dda-105">This article covers common appoaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="e4dda-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="e4dda-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="the-developer-exception-page"></a><span data-ttu-id="e4dda-107">开发人员异常页</span><span class="sxs-lookup"><span data-stu-id="e4dda-107">The developer exception page</span></span>

<span data-ttu-id="e4dda-108">若要配置应用以显示有关异常的详细信息页面，请安装 `Microsoft.AspNetCore.Diagnostics` NuGet 包并将行添加到 [Startup 类中的 Configure 方法](startup.md)：</span><span class="sxs-lookup"><span data-stu-id="e4dda-108">To configure an app to display a page that shows detailed information about exceptions, install the `Microsoft.AspNetCore.Diagnostics` NuGet package and add a line to the [Configure method in the Startup class](startup.md):</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

<span data-ttu-id="e4dda-109">将 `UseDeveloperExceptionPage` 放在想要捕获异常的任何中间件之前，如 `app.UseMvc`。</span><span class="sxs-lookup"><span data-stu-id="e4dda-109">Put `UseDeveloperExceptionPage` before any middleware you want to catch exceptions in, such as `app.UseMvc`.</span></span>

>[!WARNING]
> <span data-ttu-id="e4dda-110">仅当应用在开发环境中运行时，才启用开发人员异常页。</span><span class="sxs-lookup"><span data-stu-id="e4dda-110">Enable the developer exception page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="e4dda-111">在生产环境中运行应用时，无需公开详细的异常信息。</span><span class="sxs-lookup"><span data-stu-id="e4dda-111">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="e4dda-112">[了解有关配置环境的详细信息](environments.md)。</span><span class="sxs-lookup"><span data-stu-id="e4dda-112">[Learn more about configuring environments](environments.md).</span></span>

<span data-ttu-id="e4dda-113">若要查看开发人员异常页，请运行环境设置为 `Development` 的示例应用程序，并将 `?throw=true` 添加到应用的基本 URL。</span><span class="sxs-lookup"><span data-stu-id="e4dda-113">To see the developer exception page, run the sample application with the environment set to `Development`, and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="e4dda-114">该页包含几个有关异常和请求的信息的选项卡。</span><span class="sxs-lookup"><span data-stu-id="e4dda-114">The page includes several tabs with information about the exception and the request.</span></span> <span data-ttu-id="e4dda-115">第一个选项卡包括堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="e4dda-115">The first tab includes a stack trace.</span></span> 

![堆栈跟踪](error-handling/_static/developer-exception-page.png)

<span data-ttu-id="e4dda-117">下一个选项卡显示查询字符串参数（若有）。</span><span class="sxs-lookup"><span data-stu-id="e4dda-117">The next tab shows the query string parameters, if any.</span></span>

![查询字符串参数](error-handling/_static/developer-exception-page-query.png)

<span data-ttu-id="e4dda-119">此请求没有任何 cookie，但是如果有，会显示在“Cookie”选项卡上。可看到最后一个选项卡中传递的标头。</span><span class="sxs-lookup"><span data-stu-id="e4dda-119">This request didn't have any cookies, but if it did, they would appear on the **Cookies** tab. You can see the headers that were passed in the last tab.</span></span>

![标头](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a><span data-ttu-id="e4dda-121">配置自定义异常处理页</span><span class="sxs-lookup"><span data-stu-id="e4dda-121">Configuring a custom exception handling page</span></span>

<span data-ttu-id="e4dda-122">最好配置一个异常处理程序页，可在应用未在 `Development` 环境中运行时使用。</span><span class="sxs-lookup"><span data-stu-id="e4dda-122">It's a good idea to configure an exception handler page to use when the app isn't running in the `Development` environment.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

<span data-ttu-id="e4dda-123">在 MVC 应用中，请勿使用 HTTP 方法属性（如 `HttpGet`）显式修饰错误处理程序操作方法。</span><span class="sxs-lookup"><span data-stu-id="e4dda-123">In an MVC app, don't explicitly decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="e4dda-124">使用显式动词可防止某些请求访问该方法。</span><span class="sxs-lookup"><span data-stu-id="e4dda-124">Using explicit verbs could prevent some requests from reaching the method.</span></span>

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a><span data-ttu-id="e4dda-125">配置状态代码页</span><span class="sxs-lookup"><span data-stu-id="e4dda-125">Configuring status code pages</span></span>

<span data-ttu-id="e4dda-126">默认情况下，应用不会为 HTTP 状态代码（如 500（内部服务器错误）或 404（未找到））提供丰富的状态代码页。</span><span class="sxs-lookup"><span data-stu-id="e4dda-126">By default, your app won't provide a rich status code page for HTTP status codes such as 500 (Internal Server Error) or 404 (Not Found).</span></span> <span data-ttu-id="e4dda-127">可通过将行添加到 `Configure` 方法来配置 `StatusCodePagesMiddleware`：</span><span class="sxs-lookup"><span data-stu-id="e4dda-127">You can configure the `StatusCodePagesMiddleware` by adding a line to the `Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="e4dda-128">默认情况下，该中间件为常见的状态代码添加简单的纯文本处理程序（如 404）：</span><span class="sxs-lookup"><span data-stu-id="e4dda-128">By default, this middleware adds simple, text-only handlers for common status codes, such as 404:</span></span>

![404 页面](error-handling/_static/default-404-status-code.png)

<span data-ttu-id="e4dda-130">中间件支持几种不同的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e4dda-130">The middleware supports several different extension methods.</span></span> <span data-ttu-id="e4dda-131">一种采用 Lambda 表达式，另一种采用内容类型和格式字符串。</span><span class="sxs-lookup"><span data-stu-id="e4dda-131">One takes a lambda expression, another takes a content type and format string.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

<span data-ttu-id="e4dda-132">还有重定向扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e4dda-132">There are also redirect extension methods.</span></span> <span data-ttu-id="e4dda-133">一种向客户端发送 302 状态代码，另一种将原始状态代码返回到客户端，同时执行重定向 URL 的处理程序。</span><span class="sxs-lookup"><span data-stu-id="e4dda-133">One sends a 302 status code to the client, and one returns the original status code to the client but also executes the handler for the redirect URL.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

<span data-ttu-id="e4dda-134">如果需要为某些请求禁用状态代码页，可执行如下操作：</span><span class="sxs-lookup"><span data-stu-id="e4dda-134">If you need to disable status code pages for certain requests, you can do so:</span></span>

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
  statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a><span data-ttu-id="e4dda-135">异常处理代码</span><span class="sxs-lookup"><span data-stu-id="e4dda-135">Exception-handling code</span></span>

<span data-ttu-id="e4dda-136">异常处理页中的代码可能会引发异常。</span><span class="sxs-lookup"><span data-stu-id="e4dda-136">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="e4dda-137">建议在生产错误页面中包含纯静态内容。</span><span class="sxs-lookup"><span data-stu-id="e4dda-137">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="e4dda-138">此外，请注意，一旦发送了响应标头，便不能更改响应的状态代码，也不能运行任何异常页或处理程序。</span><span class="sxs-lookup"><span data-stu-id="e4dda-138">Also, be aware that once the headers for a response have been sent, you can't change the response's status code, nor can any exception pages or handlers run.</span></span> <span data-ttu-id="e4dda-139">响应必须完成，否则连接中止。</span><span class="sxs-lookup"><span data-stu-id="e4dda-139">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="e4dda-140">服务器异常处理</span><span class="sxs-lookup"><span data-stu-id="e4dda-140">Server exception handling</span></span>

<span data-ttu-id="e4dda-141">除了应用中的异常处理逻辑之外，托管应用的[服务器](servers/index.md)还会执行某些异常处理。</span><span class="sxs-lookup"><span data-stu-id="e4dda-141">In addition to the exception handling logic in your app, the [server](servers/index.md) hosting your app performs some exception handling.</span></span> <span data-ttu-id="e4dda-142">如果服务器在发送标头之前捕获到异常，服务器将发送无正文的 500 内部服务器错误响应。</span><span class="sxs-lookup"><span data-stu-id="e4dda-142">If the server catches an exception before the headers are sent, the server sends a 500 Internal Server Error response with no body.</span></span> <span data-ttu-id="e4dda-143">如果服务器在发送标头之后捕获到异常，服务器将关闭连接。</span><span class="sxs-lookup"><span data-stu-id="e4dda-143">If the server catches an exception after the headers have been sent, the server closes the connection.</span></span> <span data-ttu-id="e4dda-144">应用不处理的请求由服务器处理。</span><span class="sxs-lookup"><span data-stu-id="e4dda-144">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="e4dda-145">发生的任何异常都由服务器的异常处理来处理。</span><span class="sxs-lookup"><span data-stu-id="e4dda-145">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="e4dda-146">任何配置的自定义错误页或异常处理中间件或筛选器都不会影响此行为。</span><span class="sxs-lookup"><span data-stu-id="e4dda-146">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="e4dda-147">启动异常处理</span><span class="sxs-lookup"><span data-stu-id="e4dda-147">Startup exception handling</span></span>

<span data-ttu-id="e4dda-148">只有承载层才能处理应用启动过程中发生的异常。</span><span class="sxs-lookup"><span data-stu-id="e4dda-148">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="e4dda-149">可使用 `captureStartupErrors` 和 `detailedErrors` 键[配置主机在启动期间响应错误的行为方式](hosting.md#detailed-errors)。</span><span class="sxs-lookup"><span data-stu-id="e4dda-149">You can [configure how the host behaves in response to errors during startup](hosting.md#detailed-errors) using `captureStartupErrors` and the `detailedErrors` key.</span></span>

<span data-ttu-id="e4dda-150">如果在主机地址/端口绑定之后发生错误，承载只能显示捕获的启动错误的错误页。</span><span class="sxs-lookup"><span data-stu-id="e4dda-150">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="e4dda-151">如果任何绑定由于任何原因失败，承载层记录一个关键异常，dotnet 进程故障，并且不显示错误页。</span><span class="sxs-lookup"><span data-stu-id="e4dda-151">If any binding fails for any reason, the hosting layer logs a critical exception, the dotnet process crashes, and no error page is displayed.</span></span>

## <a name="aspnet-mvc-error-handling"></a><span data-ttu-id="e4dda-152">ASP.NET MVC 错误处理</span><span class="sxs-lookup"><span data-stu-id="e4dda-152">ASP.NET MVC error handling</span></span>

<span data-ttu-id="e4dda-153">[MVC](xref:mvc/overview) 应用有处理错误的某些其他选项，如配置异常筛选器和执行模型验证。</span><span class="sxs-lookup"><span data-stu-id="e4dda-153">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="e4dda-154">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="e4dda-154">Exception Filters</span></span>

<span data-ttu-id="e4dda-155">在 MVC 应用中，可全局配置异常筛选器，也可根据每个控制器或每个操作配置异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="e4dda-155">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="e4dda-156">这些筛选器处理在执行控制器操作或其他筛选器期间发生的任何未处理的异常，在其他情况下并不调用。</span><span class="sxs-lookup"><span data-stu-id="e4dda-156">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter, and are not called otherwise.</span></span> <span data-ttu-id="e4dda-157">了解[筛选器](../mvc/controllers/filters.md)中有关异常筛选器的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4dda-157">Learn more about exception filters in [Filters](../mvc/controllers/filters.md).</span></span>

>[!TIP]
> <span data-ttu-id="e4dda-158">异常筛选器适合捕获 MVC 操作内发生的异常，但它们不如错误处理中间件灵活。</span><span class="sxs-lookup"><span data-stu-id="e4dda-158">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="e4dda-159">一般情况下建议使用中间件；仅在需要根据所选 MVC 操作以不同方式执行错误处理时，才使用筛选器。</span><span class="sxs-lookup"><span data-stu-id="e4dda-159">Prefer middleware for the general case, and use filters only where you need to do error handling *differently* based on which MVC action was chosen.</span></span>

### <a name="handling-model-state-errors"></a><span data-ttu-id="e4dda-160">处理模型状态错误</span><span class="sxs-lookup"><span data-stu-id="e4dda-160">Handling Model State Errors</span></span>

<span data-ttu-id="e4dda-161">在调用每个控制器操作前进行[模型验证](../mvc/models/validation.md)，操作方法负责检查 `ModelState.IsValid` 并作出正确反应。</span><span class="sxs-lookup"><span data-stu-id="e4dda-161">[Model validation](../mvc/models/validation.md) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span>

<span data-ttu-id="e4dda-162">某些应用会选择遵循标准约定来处理模型验证错误，在这种情况下，可以在[筛选器](../mvc/controllers/filters.md)中实现此类策略。</span><span class="sxs-lookup"><span data-stu-id="e4dda-162">Some apps will choose to follow a standard convention for dealing with model validation errors, in which case a [filter](../mvc/controllers/filters.md) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="e4dda-163">应测试操作在无效模型状态下的行为方式。</span><span class="sxs-lookup"><span data-stu-id="e4dda-163">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="e4dda-164">在[测试控制器逻辑](../mvc/controllers/testing.md)中了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4dda-164">Learn more in [Testing controller logic](../mvc/controllers/testing.md).</span></span>



