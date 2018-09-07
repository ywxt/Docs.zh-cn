---
title: 启用 ASP.NET Core 中的跨域请求 (CORS)
author: rick-anderson
description: 了解如何作为一种标准允许或拒绝在 ASP.NET Core 应用中的跨域请求的 CORS。
ms.author: riande
ms.custom: mvc
ms.date: 09/05/2018
uid: security/cors
ms.openlocfilehash: f654260411f1bd5725a0e3d14951c7e9bbc893e8
ms.sourcegitcommit: 08bf41d4b3e696ab512b044970e8304816f8cc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "44039973"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a><span data-ttu-id="0be7a-103">启用 ASP.NET Core 中的跨域请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="0be7a-103">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>

<span data-ttu-id="0be7a-104">作者：[Mike Wasson](https://github.com/mikewasson)、[Shayne Boyer](https://twitter.com/spboyer) 和 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0be7a-104">By [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0be7a-105">浏览器安全性以防止网页从发出请求到不同的域的 web 页面提供服务。</span><span class="sxs-lookup"><span data-stu-id="0be7a-105">Browser security prevents a web page from making requests to a different domain than the one that served the web page.</span></span> <span data-ttu-id="0be7a-106">此限制称为*同域策略*。</span><span class="sxs-lookup"><span data-stu-id="0be7a-106">This restriction is called the *same-origin policy*.</span></span> <span data-ttu-id="0be7a-107">同域策略可阻止恶意站点读取另一个站点中的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="0be7a-107">The same-origin policy prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="0be7a-108">有时，你可能想要允许其他站点对您的应用程序进行跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-108">Sometimes, you might want to allow other sites make cross-origin requests to your app.</span></span>

<span data-ttu-id="0be7a-109">[跨域资源共享](https://www.w3.org/TR/cors/)(CORS) 是一种 W3C 标准，允许服务器放宽同源策略。</span><span class="sxs-lookup"><span data-stu-id="0be7a-109">[Cross Origin Resource Sharing](https://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="0be7a-110">使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-110">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="0be7a-111">CORS 是更安全、 更灵活比早期技术，如[JSONP](https://wikipedia.org/wiki/JSONP)。</span><span class="sxs-lookup"><span data-stu-id="0be7a-111">CORS is safer and more flexible than earlier techniques, such as [JSONP](https://wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="0be7a-112">本主题演示如何在 ASP.NET Core 应用中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="0be7a-112">This topic shows how to enable CORS in an ASP.NET Core app.</span></span>

## <a name="same-origin"></a><span data-ttu-id="0be7a-113">相同的原点</span><span class="sxs-lookup"><span data-stu-id="0be7a-113">Same origin</span></span>

<span data-ttu-id="0be7a-114">如果它们具有相同方案、 主机和端口，两个 Url 将具有相同的原点 ([RFC 6454](https://tools.ietf.org/html/rfc6454))。</span><span class="sxs-lookup"><span data-stu-id="0be7a-114">Two URLs have the same origin if they have identical schemes, hosts, and ports ([RFC 6454](https://tools.ietf.org/html/rfc6454)).</span></span>

<span data-ttu-id="0be7a-115">以下两个 Url 具有相同的原点：</span><span class="sxs-lookup"><span data-stu-id="0be7a-115">These two URLs have the same origin:</span></span>

* `https://example.com/foo.html`
* `https://example.com/bar.html`

<span data-ttu-id="0be7a-116">这些 Url 具有不同的源，比以前的两个 Url:</span><span class="sxs-lookup"><span data-stu-id="0be7a-116">These URLs have different origins than the previous two URLs:</span></span>

* <span data-ttu-id="0be7a-117">`https://example.net` &ndash; 不同的域</span><span class="sxs-lookup"><span data-stu-id="0be7a-117">`https://example.net` &ndash; Different domain</span></span>
* <span data-ttu-id="0be7a-118">`https://www.example.com/foo.html` &ndash; 不同的子域</span><span class="sxs-lookup"><span data-stu-id="0be7a-118">`https://www.example.com/foo.html` &ndash; Different subdomain</span></span>
* <span data-ttu-id="0be7a-119">`http://example.com/foo.html` &ndash; 不同的方案</span><span class="sxs-lookup"><span data-stu-id="0be7a-119">`http://example.com/foo.html` &ndash; Different scheme</span></span>
* <span data-ttu-id="0be7a-120">`https://example.com:9000/foo.html` &ndash; 不同的端口</span><span class="sxs-lookup"><span data-stu-id="0be7a-120">`https://example.com:9000/foo.html` &ndash; Different port</span></span>

> [!NOTE]
> <span data-ttu-id="0be7a-121">比较来源时，Internet Explorer 不会考虑该端口。</span><span class="sxs-lookup"><span data-stu-id="0be7a-121">Internet Explorer doesn't consider the port when comparing origins.</span></span>

## <a name="register-cors-services"></a><span data-ttu-id="0be7a-122">注册的 CORS 服务</span><span class="sxs-lookup"><span data-stu-id="0be7a-122">Register CORS services</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="0be7a-123">引用[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)或添加到的包引用[Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/)包。</span><span class="sxs-lookup"><span data-stu-id="0be7a-123">Reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="0be7a-124">引用[Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)或添加到的包引用[Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/)包。</span><span class="sxs-lookup"><span data-stu-id="0be7a-124">Reference the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) or add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="0be7a-125">添加到包引用[Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/)包。</span><span class="sxs-lookup"><span data-stu-id="0be7a-125">Add a package reference to the [Microsoft.AspNetCore.Cors](https://www.nuget.org/packages/Microsoft.AspNetCore.Cors/) package.</span></span>

::: moniker-end

<span data-ttu-id="0be7a-126">调用<xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*>在`Startup.ConfigureServices`将 CORS 服务添加到应用程序的服务容器：</span><span class="sxs-lookup"><span data-stu-id="0be7a-126">Call <xref:Microsoft.Extensions.DependencyInjection.MvcCorsMvcCoreBuilderExtensions.AddCors*> in `Startup.ConfigureServices` to add CORS services to the app's service container:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors&highlight=3)]

## <a name="enable-cors"></a><span data-ttu-id="0be7a-127">启用 CORS</span><span class="sxs-lookup"><span data-stu-id="0be7a-127">Enable CORS</span></span>

<span data-ttu-id="0be7a-128">注册之后的 CORS 服务，使用以下方法之一在 ASP.NET Core 应用中启用 CORS:</span><span class="sxs-lookup"><span data-stu-id="0be7a-128">After registering CORS services, use either of the following approaches to enable CORS in an ASP.NET Core app:</span></span>

* <span data-ttu-id="0be7a-129">[CORS 中间件](#enable-cors-with-cors-middleware)&ndash;全局到通过中间件应用程序的应用的 CORS 策略。</span><span class="sxs-lookup"><span data-stu-id="0be7a-129">[CORS Middleware](#enable-cors-with-cors-middleware) &ndash; Apply CORS policies globally to the app via middleware.</span></span>
* <span data-ttu-id="0be7a-130">[在 MVC 中的 CORS](#enable-cors-in-mvc) &ndash;每个操作或每个控制器应用 CORS 策略。</span><span class="sxs-lookup"><span data-stu-id="0be7a-130">[CORS in MVC](#enable-cors-in-mvc) &ndash; Apply CORS policies per action or per controller.</span></span> <span data-ttu-id="0be7a-131">不会使用 CORS 中间件。</span><span class="sxs-lookup"><span data-stu-id="0be7a-131">CORS Middleware isn't used.</span></span>

### <a name="enable-cors-with-cors-middleware"></a><span data-ttu-id="0be7a-132">启用 CORS 的 CORS 中间件</span><span class="sxs-lookup"><span data-stu-id="0be7a-132">Enable CORS with CORS Middleware</span></span>

<span data-ttu-id="0be7a-133">CORS 中间件处理向应用程序的跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-133">CORS Middleware handles cross-origin requests to the app.</span></span> <span data-ttu-id="0be7a-134">若要在请求处理管道中启用 CORS 中间件，请调用<xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*>中的扩展方法`Startup.Configure`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-134">To enable CORS Middleware in the request processing pipeline, call the <xref:Microsoft.AspNetCore.Builder.CorsMiddlewareExtensions.UseCors*> extension method in `Startup.Configure`.</span></span>

<span data-ttu-id="0be7a-135">CORS 中间件必须位于之前定义的任何终结点应用程序中你想要支持跨域请求 (例如，在对调用之前`UseMvc`MVC/Razor 页中间件)。</span><span class="sxs-lookup"><span data-stu-id="0be7a-135">CORS Middleware must precede any defined endpoints in your app where you want to support cross-origin requests (for example, before the call to `UseMvc` for MVC/Razor Pages Middleware).</span></span>

<span data-ttu-id="0be7a-136">一个*跨域策略*添加 CORS 中间件使用时可以指定<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder>类。</span><span class="sxs-lookup"><span data-stu-id="0be7a-136">A *cross-origin policy* can be specified when adding the CORS Middleware using the <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> class.</span></span> <span data-ttu-id="0be7a-137">有两种方法用于定义 CORS 策略：</span><span class="sxs-lookup"><span data-stu-id="0be7a-137">There are two approaches for defining a CORS policy:</span></span>

* <span data-ttu-id="0be7a-138">调用`UseCors`lambda:</span><span class="sxs-lookup"><span data-stu-id="0be7a-138">Call `UseCors` with a lambda:</span></span>

  [!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

  <span data-ttu-id="0be7a-139">Lambda 采用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder>对象。</span><span class="sxs-lookup"><span data-stu-id="0be7a-139">The lambda takes a <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder> object.</span></span> <span data-ttu-id="0be7a-140">[配置选项](#cors-policy-options)，如`WithOrigins`，本主题后面所述。</span><span class="sxs-lookup"><span data-stu-id="0be7a-140">[Configuration options](#cors-policy-options), such as `WithOrigins`, are described later in this topic.</span></span> <span data-ttu-id="0be7a-141">在前面的示例中，该策略允许跨域请求从`https://example.com`和任何其他来源。</span><span class="sxs-lookup"><span data-stu-id="0be7a-141">In the preceding example, the policy allows cross-origin requests from `https://example.com` and no other origins.</span></span>

  <span data-ttu-id="0be7a-142">不含尾部斜杠，必须指定的 URL (`/`)。</span><span class="sxs-lookup"><span data-stu-id="0be7a-142">The URL must be specified without a trailing slash (`/`).</span></span> <span data-ttu-id="0be7a-143">如果 URL 以终止`/`，则比较操作返回`false`并返回无标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-143">If the URL terminates with `/`, the comparison returns `false` and no header is returned.</span></span>

  <span data-ttu-id="0be7a-144">`CorsPolicyBuilder` 具有 fluent API，因此您可以将方法调用链接：</span><span class="sxs-lookup"><span data-stu-id="0be7a-144">`CorsPolicyBuilder` has a fluent API, so you can chain method calls:</span></span>

  [!code-csharp[](cors/sample/CorsExample3/Startup.cs?highlight=2-3&range=29-32)]

* <span data-ttu-id="0be7a-145">定义一个或多个命名的 CORS 策略并按名称在运行时选择的策略。</span><span class="sxs-lookup"><span data-stu-id="0be7a-145">Define one or more named CORS policies and select the policy by name at runtime.</span></span> <span data-ttu-id="0be7a-146">下面的示例添加名为的用户定义 CORS 策略*AllowSpecificOrigin*。</span><span class="sxs-lookup"><span data-stu-id="0be7a-146">The following example adds a user-defined CORS policy named *AllowSpecificOrigin*.</span></span> <span data-ttu-id="0be7a-147">若要选择的策略，将名称传递给`UseCors`:</span><span class="sxs-lookup"><span data-stu-id="0be7a-147">To select the policy, pass the name to `UseCors`:</span></span>

  [!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin&highlight=5-6,21)]

### <a name="enable-cors-in-mvc"></a><span data-ttu-id="0be7a-148">启用在 MVC 中的 CORS</span><span class="sxs-lookup"><span data-stu-id="0be7a-148">Enable CORS in MVC</span></span>

<span data-ttu-id="0be7a-149">或者，可以使用 MVC 应用特定 CORS 策略针对每个操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="0be7a-149">You can alternatively use MVC to apply specific CORS policies per action or per controller.</span></span> <span data-ttu-id="0be7a-150">在使用 MVC 启用 CORS，使用了已注册的 CORS 服务。</span><span class="sxs-lookup"><span data-stu-id="0be7a-150">When using MVC to enable CORS, the registered CORS services are used.</span></span> <span data-ttu-id="0be7a-151">不会使用 CORS 中间件。</span><span class="sxs-lookup"><span data-stu-id="0be7a-151">The CORS Middleware isn't used.</span></span>

### <a name="per-action"></a><span data-ttu-id="0be7a-152">每个操作</span><span class="sxs-lookup"><span data-stu-id="0be7a-152">Per action</span></span>

<span data-ttu-id="0be7a-153">若要指定特定操作的 CORS 策略，添加[ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute)属性为该操作。</span><span class="sxs-lookup"><span data-stu-id="0be7a-153">To specify a CORS policy for a specific action, add the [&lbrack;EnableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) attribute to the action.</span></span> <span data-ttu-id="0be7a-154">指定策略名称。</span><span class="sxs-lookup"><span data-stu-id="0be7a-154">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction&highlight=2)]

### <a name="per-controller"></a><span data-ttu-id="0be7a-155">每个控制器</span><span class="sxs-lookup"><span data-stu-id="0be7a-155">Per controller</span></span>

<span data-ttu-id="0be7a-156">若要指定特定控制器的 CORS 策略，添加[ &lbrack;EnableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute)属性到控制器类。</span><span class="sxs-lookup"><span data-stu-id="0be7a-156">To specify the CORS policy for a specific controller, add the [&lbrack;EnableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.EnableCorsAttribute) attribute to the controller class.</span></span> <span data-ttu-id="0be7a-157">指定策略名称。</span><span class="sxs-lookup"><span data-stu-id="0be7a-157">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController&highlight=2)]

<span data-ttu-id="0be7a-158">优先顺序是：</span><span class="sxs-lookup"><span data-stu-id="0be7a-158">The precedence order is:</span></span>

1. <span data-ttu-id="0be7a-159">action</span><span class="sxs-lookup"><span data-stu-id="0be7a-159">action</span></span>
1. <span data-ttu-id="0be7a-160">控制器</span><span class="sxs-lookup"><span data-stu-id="0be7a-160">controller</span></span>

### <a name="disable-cors"></a><span data-ttu-id="0be7a-161">禁用 CORS</span><span class="sxs-lookup"><span data-stu-id="0be7a-161">Disable CORS</span></span>

<span data-ttu-id="0be7a-162">若要禁用 CORS 的控制器或操作，请使用[ &lbrack;DisableCors&rbrack; ](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute)属性：</span><span class="sxs-lookup"><span data-stu-id="0be7a-162">To disable CORS for a controller or action, use the [&lbrack;DisableCors&rbrack;](xref:Microsoft.AspNetCore.Cors.DisableCorsAttribute) attribute:</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction&highlight=2)]

## <a name="cors-policy-options"></a><span data-ttu-id="0be7a-163">CORS 策略选项</span><span class="sxs-lookup"><span data-stu-id="0be7a-163">CORS policy options</span></span>

<span data-ttu-id="0be7a-164">本部分介绍您可以在 CORS 策略设置的各种选项。</span><span class="sxs-lookup"><span data-stu-id="0be7a-164">This section describes the various options that you can set in a CORS policy.</span></span>

* [<span data-ttu-id="0be7a-165">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="0be7a-165">Set the allowed origins</span></span>](#set-the-allowed-origins)
* [<span data-ttu-id="0be7a-166">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0be7a-166">Set the allowed HTTP methods</span></span>](#set-the-allowed-http-methods)
* [<span data-ttu-id="0be7a-167">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="0be7a-167">Set the allowed request headers</span></span>](#set-the-allowed-request-headers)
* [<span data-ttu-id="0be7a-168">设置公开的响应标头</span><span class="sxs-lookup"><span data-stu-id="0be7a-168">Set the exposed response headers</span></span>](#set-the-exposed-response-headers)
* [<span data-ttu-id="0be7a-169">跨域请求中的凭据</span><span class="sxs-lookup"><span data-stu-id="0be7a-169">Credentials in cross-origin requests</span></span>](#credentials-in-cross-origin-requests)
* [<span data-ttu-id="0be7a-170">将预检过期时间设置</span><span class="sxs-lookup"><span data-stu-id="0be7a-170">Set the preflight expiration time</span></span>](#set-the-preflight-expiration-time)

<span data-ttu-id="0be7a-171">有关一些选项，可能会有帮助读取[如何 CORS 工作](#how-cors-works)部分第一次。</span><span class="sxs-lookup"><span data-stu-id="0be7a-171">For some options, it may be helpful to read the [How CORS works](#how-cors-works) section first.</span></span>

### <a name="set-the-allowed-origins"></a><span data-ttu-id="0be7a-172">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="0be7a-172">Set the allowed origins</span></span>

<span data-ttu-id="0be7a-173">若要允许一个或多个特定源，调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithOrigins*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-173">To allow one or more specific origins, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithOrigins*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=20-24&highlight=4)]

<span data-ttu-id="0be7a-174">若要允许所有来源，请调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-174">To allow all origins, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyOrigin*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=28-32&highlight=4)]

<span data-ttu-id="0be7a-175">允许任何来源的请求之前，请仔细考虑。</span><span class="sxs-lookup"><span data-stu-id="0be7a-175">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="0be7a-176">允许任何来源的请求意味着*的任何网站*可以对您的应用程序进行跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-176">Allowing requests from any origin means that *any website* can make cross-origin requests to your app.</span></span>

<span data-ttu-id="0be7a-177">此设置会影响[预检请求和访问控制的允许的域标头](#preflight-requests)（在本主题后面所述）。</span><span class="sxs-lookup"><span data-stu-id="0be7a-177">This setting affects [preflight requests and the Access-Control-Allow-Origin header](#preflight-requests) (described later in this topic).</span></span>

### <a name="set-the-allowed-http-methods"></a><span data-ttu-id="0be7a-178">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0be7a-178">Set the allowed HTTP methods</span></span>

<span data-ttu-id="0be7a-179">若要允许所有 HTTP 方法，调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-179">To allow all HTTP methods, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyMethod*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=45-50&highlight=5)]

<span data-ttu-id="0be7a-180">此设置会影响[预检请求和访问的控制的允许的方法标头](#preflight-requests)（在本主题后面所述）。</span><span class="sxs-lookup"><span data-stu-id="0be7a-180">This setting affects [preflight requests and the Access-Control-Allow-Methods header](#preflight-requests) (described later in this topic).</span></span>

### <a name="set-the-allowed-request-headers"></a><span data-ttu-id="0be7a-181">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="0be7a-181">Set the allowed request headers</span></span>

<span data-ttu-id="0be7a-182">若要允许特定标头发送在 CORS 请求中，调用*创作请求标头*，调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>并指定允许的标头：</span><span class="sxs-lookup"><span data-stu-id="0be7a-182">To allow specific headers to be sent in a CORS request, called *author request headers*, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*> and specify the allowed headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

<span data-ttu-id="0be7a-183">若要允许所有作者的请求标头调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-183">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

<span data-ttu-id="0be7a-184">此设置会影响[预检请求和访问控制的请求标头标头](#preflight-requests)（在本主题后面所述）。</span><span class="sxs-lookup"><span data-stu-id="0be7a-184">This setting affects [preflight requests and the Access-Control-Request-Headers header](#preflight-requests) (described later in this topic).</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="0be7a-185">CORS 中间件策略匹配所指定的特定标头`WithHeaders`时，才可以发送标头`Access-Control-Request-Headers`与中所述的标头完全匹配`WithHeaders`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-185">A CORS Middleware policy match to specific headers specified by `WithHeaders` is only possible when the headers sent in `Access-Control-Request-Headers` exactly match the headers stated in `WithHeaders`.</span></span>

<span data-ttu-id="0be7a-186">例如，假设配置，如下所示的应用：</span><span class="sxs-lookup"><span data-stu-id="0be7a-186">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="0be7a-187">CORS 中间件拒绝包含以下请求标头的预检请求，因为`Content-Language`([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage)) 中未列出`WithHeaders`:</span><span class="sxs-lookup"><span data-stu-id="0be7a-187">CORS Middleware declines a preflight request with the following request header because `Content-Language` ([HeaderNames.ContentLanguage](xref:Microsoft.Net.Http.Headers.HeaderNames.ContentLanguage)) isn't listed in `WithHeaders`:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

<span data-ttu-id="0be7a-188">应用程序返回*200 确定*响应但不会发送回的 CORS 标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-188">The app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="0be7a-189">因此，在浏览器不会尝试执行跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-189">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="0be7a-190">CORS 中间件始终允许在四个标头`Access-Control-Request-Headers`发送而不考虑 CorsPolicy.Headers 中配置的值。</span><span class="sxs-lookup"><span data-stu-id="0be7a-190">CORS Middleware always allows four headers in the `Access-Control-Request-Headers` to be sent regardless of the values configured in CorsPolicy.Headers.</span></span> <span data-ttu-id="0be7a-191">此列表的标头包括：</span><span class="sxs-lookup"><span data-stu-id="0be7a-191">This list of headers includes:</span></span>

* `Accept`
* `Accept-Language`
* `Content-Language`
* `Origin`

<span data-ttu-id="0be7a-192">例如，假设配置，如下所示的应用：</span><span class="sxs-lookup"><span data-stu-id="0be7a-192">For instance, consider an app configured as follows:</span></span>

```csharp
app.UseCors(policy => policy.WithHeaders(HeaderNames.CacheControl));
```

<span data-ttu-id="0be7a-193">CORS 中间件成功响应以下请求标头的预检请求因为`Content-Language`始终是已列入允许列表：</span><span class="sxs-lookup"><span data-stu-id="0be7a-193">CORS Middleware responds successfully to a preflight request with the following request header because `Content-Language` is always whitelisted:</span></span>

```
Access-Control-Request-Headers: Cache-Control, Content-Language
```

::: moniker-end

### <a name="set-the-exposed-response-headers"></a><span data-ttu-id="0be7a-194">设置公开的响应标头</span><span class="sxs-lookup"><span data-stu-id="0be7a-194">Set the exposed response headers</span></span>

<span data-ttu-id="0be7a-195">默认情况下，在浏览器不会公开所有向应用程序的响应标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-195">By default, the browser doesn't expose all of the response headers to the app.</span></span> <span data-ttu-id="0be7a-196">有关详细信息，请参阅[W3C 跨域资源共享 （术语）： 简单的响应标头](https://www.w3.org/TR/cors/#simple-response-header)。</span><span class="sxs-lookup"><span data-stu-id="0be7a-196">For more information, see [W3C Cross-Origin Resource Sharing (Terminology): Simple Response Header](https://www.w3.org/TR/cors/#simple-response-header).</span></span>

<span data-ttu-id="0be7a-197">默认情况下可用的响应标头是：</span><span class="sxs-lookup"><span data-stu-id="0be7a-197">The response headers that are available by default are:</span></span>

* `Cache-Control`
* `Content-Language`
* `Content-Type`
* `Expires`
* `Last-Modified`
* `Pragma`

<span data-ttu-id="0be7a-198">CORS 规范调用这些标头*简单响应标头*。</span><span class="sxs-lookup"><span data-stu-id="0be7a-198">The CORS specification calls these headers *simple response headers*.</span></span> <span data-ttu-id="0be7a-199">若要使其他标头可用于应用程序，请调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-199">To make other headers available to the app, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithExposedHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=72-77&highlight=5)]

### <a name="credentials-in-cross-origin-requests"></a><span data-ttu-id="0be7a-200">跨域请求中的凭据</span><span class="sxs-lookup"><span data-stu-id="0be7a-200">Credentials in cross-origin requests</span></span>

<span data-ttu-id="0be7a-201">凭据要求特殊处理 CORS 请求中。</span><span class="sxs-lookup"><span data-stu-id="0be7a-201">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="0be7a-202">默认情况下，在浏览器不会发送与跨域请求的凭据。</span><span class="sxs-lookup"><span data-stu-id="0be7a-202">By default, the browser doesn't send credentials with a cross-origin request.</span></span> <span data-ttu-id="0be7a-203">凭据包括 cookie 和 HTTP 身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="0be7a-203">Credentials include cookies and HTTP authentication schemes.</span></span> <span data-ttu-id="0be7a-204">若要将发送具有跨源请求的凭据，客户端必须设置`XMLHttpRequest.withCredentials`到`true`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-204">To send credentials with a cross-origin request, the client must set `XMLHttpRequest.withCredentials` to `true`.</span></span>

<span data-ttu-id="0be7a-205">使用`XMLHttpRequest`直接：</span><span class="sxs-lookup"><span data-stu-id="0be7a-205">Using `XMLHttpRequest` directly:</span></span>

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'https://www.example.com/api/test');
xhr.withCredentials = true;
```

<span data-ttu-id="0be7a-206">在 jQuery 中：</span><span class="sxs-lookup"><span data-stu-id="0be7a-206">In jQuery:</span></span>

```jQuery
$.ajax({
  type: 'get',
  url: 'https://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

<span data-ttu-id="0be7a-207">此外，服务器必须允许凭据。</span><span class="sxs-lookup"><span data-stu-id="0be7a-207">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="0be7a-208">若要允许跨域凭据，调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-208">To allow cross-origin credentials, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowCredentials*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=81-86&highlight=5)]

<span data-ttu-id="0be7a-209">HTTP 响应包括`Access-Control-Allow-Credentials`标头，服务器允许跨域请求凭据将告诉浏览器。</span><span class="sxs-lookup"><span data-stu-id="0be7a-209">The HTTP response includes an `Access-Control-Allow-Credentials` header, which tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="0be7a-210">如果浏览器发送凭据，但响应不包含有效`Access-Control-Allow-Credentials`标头，在浏览器不会公开的响应应用程序中，并且跨域请求失败。</span><span class="sxs-lookup"><span data-stu-id="0be7a-210">If the browser sends credentials but the response doesn't include a valid `Access-Control-Allow-Credentials` header, the browser doesn't expose the response to the app, and the cross-origin request fails.</span></span>

<span data-ttu-id="0be7a-211">允许跨域凭据时要小心。</span><span class="sxs-lookup"><span data-stu-id="0be7a-211">Be careful when allowing cross-origin credentials.</span></span> <span data-ttu-id="0be7a-212">在另一个域的网站可以向应用而无需在用户不知情的用户的名义发送登录的用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="0be7a-212">A website at another domain can send a signed-in user's credentials to the app on the user's behalf without the user's knowledge.</span></span>

<span data-ttu-id="0be7a-213">CORS 规范还会说明该设置到来源`"*"`（所有来源） 是无效的如果`Access-Control-Allow-Credentials`标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-213">The CORS specification also states that setting origins to `"*"` (all origins) is invalid if the `Access-Control-Allow-Credentials` header is present.</span></span>

### <a name="preflight-requests"></a><span data-ttu-id="0be7a-214">预检请求</span><span class="sxs-lookup"><span data-stu-id="0be7a-214">Preflight requests</span></span>

<span data-ttu-id="0be7a-215">对于某些 CORS 请求，在浏览器发出实际请求之前发送其他请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-215">For some CORS requests, the browser sends an additional request before making the actual request.</span></span> <span data-ttu-id="0be7a-216">调用此请求*预检请求*。</span><span class="sxs-lookup"><span data-stu-id="0be7a-216">This request is called a *preflight request*.</span></span> <span data-ttu-id="0be7a-217">在浏览器可以跳过预检请求，如果满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="0be7a-217">The browser can skip the preflight request if the following conditions are true:</span></span>

* <span data-ttu-id="0be7a-218">请求方法是 GET、 HEAD 或 POST。</span><span class="sxs-lookup"><span data-stu-id="0be7a-218">The request method is GET, HEAD, or POST.</span></span>
* <span data-ttu-id="0be7a-219">应用程序不会设置以外的其他请求标头`Accept`， `Accept-Language`， `Content-Language`， `Content-Type`，或`Last-Event-ID`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-219">The app doesn't set request headers other than `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, or `Last-Event-ID`.</span></span>
* <span data-ttu-id="0be7a-220">`Content-Type`标头，如果设置，有一个以下值之一：</span><span class="sxs-lookup"><span data-stu-id="0be7a-220">The `Content-Type` header, if set, has one of the one of the following values:</span></span>
  * `application/x-www-form-urlencoded`
  * `multipart/form-data`
  * `text/plain`

<span data-ttu-id="0be7a-221">在请求标头的规则集的客户端请求适用于通过调用来设置应用程序的标头`setRequestHeader`上`XMLHttpRequest`对象。</span><span class="sxs-lookup"><span data-stu-id="0be7a-221">The rule on request headers set for the client request applies to headers that the app sets by calling `setRequestHeader` on the `XMLHttpRequest` object.</span></span> <span data-ttu-id="0be7a-222">CORS 规范调用这些标头*创作请求标头*。</span><span class="sxs-lookup"><span data-stu-id="0be7a-222">The CORS specification calls these headers *author request headers*.</span></span> <span data-ttu-id="0be7a-223">该规则不能应用于标头设置可以在浏览器，如`User-Agent`， `Host`，或`Content-Length`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-223">The rule doesn't apply to headers the browser can set, such as `User-Agent`, `Host`, or `Content-Length`.</span></span>

<span data-ttu-id="0be7a-224">下面是预检请求的示例：</span><span class="sxs-lookup"><span data-stu-id="0be7a-224">The following is an example of a preflight request:</span></span>

```
OPTIONS https://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: https://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

<span data-ttu-id="0be7a-225">预检请求使用 HTTP OPTIONS 方法。</span><span class="sxs-lookup"><span data-stu-id="0be7a-225">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="0be7a-226">它包括两个特殊的标头：</span><span class="sxs-lookup"><span data-stu-id="0be7a-226">It includes two special headers:</span></span>

* <span data-ttu-id="0be7a-227">`Access-Control-Request-Method`: 将用作实际请求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="0be7a-227">`Access-Control-Request-Method`: The HTTP method that will be used for the actual request.</span></span>
* <span data-ttu-id="0be7a-228">`Access-Control-Request-Headers`： 设置实际请求中应用的请求标头的列表。</span><span class="sxs-lookup"><span data-stu-id="0be7a-228">`Access-Control-Request-Headers`: A list of request headers that the app sets on the actual request.</span></span> <span data-ttu-id="0be7a-229">如前面所述，这不包括标头的浏览器设置，如`User-Agent`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-229">As stated earlier, this doesn't include headers that the browser sets, such as `User-Agent`.</span></span>

<span data-ttu-id="0be7a-230">CORS 预检请求可能包括`Access-Control-Request-Headers`标头，指示服务器与实际请求一起发送的标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-230">A CORS preflight request might include an `Access-Control-Request-Headers` header, which indicates to the server the headers that are sent with the actual request.</span></span>

<span data-ttu-id="0be7a-231">若要允许的特定标头，请调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-231">To allow specific headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.WithHeaders*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=54-59&highlight=5)]

<span data-ttu-id="0be7a-232">若要允许所有作者的请求标头调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-232">To allow all author request headers, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.AllowAnyHeader*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=63-68&highlight=5)]

<span data-ttu-id="0be7a-233">浏览器不是在设置方式完全一致`Access-Control-Request-Headers`。</span><span class="sxs-lookup"><span data-stu-id="0be7a-233">Browsers aren't entirely consistent in how they set `Access-Control-Request-Headers`.</span></span> <span data-ttu-id="0be7a-234">如果将标头设置到的任何内容以外`"*"`(或使用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>)，至少应包含`Accept`， `Content-Type`，和`Origin`，以及你想要支持任何自定义标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-234">If you set headers to anything other than `"*"` (or use <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicy.AllowAnyHeader*>), you should include at least `Accept`, `Content-Type`, and `Origin`, plus any custom headers that you want to support.</span></span>

<span data-ttu-id="0be7a-235">下面是预检请求 （假设服务器允许请求） 的示例响应：</span><span class="sxs-lookup"><span data-stu-id="0be7a-235">The following is an example response to the preflight request (assuming that the server allows the request):</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

<span data-ttu-id="0be7a-236">响应包括`Access-Control-Allow-Methods`标头，其中列出了允许的方法和 （可选）`Access-Control-Allow-Headers`标头，其中列出了允许的标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-236">The response includes an `Access-Control-Allow-Methods` header that lists the allowed methods and optionally an `Access-Control-Allow-Headers` header, which lists the allowed headers.</span></span> <span data-ttu-id="0be7a-237">如果预检请求成功，则浏览器发送实际请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-237">If the preflight request succeeds, the browser sends the actual request.</span></span>

<span data-ttu-id="0be7a-238">如果预检请求被拒绝，该应用程序将返回*200 确定*响应但不会发送回的 CORS 标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-238">If the preflight request is denied, the app returns a *200 OK* response but doesn't send the CORS headers back.</span></span> <span data-ttu-id="0be7a-239">因此，在浏览器不会尝试执行跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-239">Therefore, the browser doesn't attempt the cross-origin request.</span></span>

### <a name="set-the-preflight-expiration-time"></a><span data-ttu-id="0be7a-240">将预检过期时间设置</span><span class="sxs-lookup"><span data-stu-id="0be7a-240">Set the preflight expiration time</span></span>

<span data-ttu-id="0be7a-241">`Access-Control-Max-Age`标头指定可以缓存预检请求的响应的时间。</span><span class="sxs-lookup"><span data-stu-id="0be7a-241">The `Access-Control-Max-Age` header specifies how long the response to the preflight request can be cached.</span></span> <span data-ttu-id="0be7a-242">若要设置此标头，请调用<xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span><span class="sxs-lookup"><span data-stu-id="0be7a-242">To set this header, call <xref:Microsoft.AspNetCore.Cors.Infrastructure.CorsPolicyBuilder.SetPreflightMaxAge*>:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=90-95&highlight=5)]

## <a name="how-cors-works"></a><span data-ttu-id="0be7a-243">CORS 的工作原理</span><span class="sxs-lookup"><span data-stu-id="0be7a-243">How CORS works</span></span>

<span data-ttu-id="0be7a-244">本部分介绍在 CORS 请求的 HTTP 消息级别中会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="0be7a-244">This section describes what happens in a CORS request at the level of the HTTP messages.</span></span> <span data-ttu-id="0be7a-245">请务必了解，以便可以正确配置和调试时出现意外的行为的 CORS 策略 CORS 的工作原理。</span><span class="sxs-lookup"><span data-stu-id="0be7a-245">It's important to understand how CORS works so that the CORS policy can be configured correctly and debugged when unexpected behaviors occur.</span></span>

<span data-ttu-id="0be7a-246">CORS 规范引入了几个新的 HTTP 标头启用跨域请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-246">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="0be7a-247">如果浏览器支持 CORS，则将设置自动跨域请求这些标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-247">If a browser supports CORS, it sets these headers automatically for cross-origin requests.</span></span> <span data-ttu-id="0be7a-248">自定义 JavaScript 代码不需要启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="0be7a-248">Custom JavaScript code isn't required to enable CORS.</span></span>

<span data-ttu-id="0be7a-249">下面是跨域请求的示例。</span><span class="sxs-lookup"><span data-stu-id="0be7a-249">The following is an example of a cross-origin request.</span></span> <span data-ttu-id="0be7a-250">`Origin`标头提供发出请求的站点的域：</span><span class="sxs-lookup"><span data-stu-id="0be7a-250">The `Origin` header provides the domain of the site that's making the request:</span></span>

```
GET https://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: https://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: https://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

<span data-ttu-id="0be7a-251">如果服务器允许该请求，它会设置`Access-Control-Allow-Origin`在响应中的标头。</span><span class="sxs-lookup"><span data-stu-id="0be7a-251">If the server allows the request, it sets the `Access-Control-Allow-Origin` header in the response.</span></span> <span data-ttu-id="0be7a-252">此标头的值或者与匹配`Origin`请求标头或为通配符值`"*"`，允许任何源的含义：</span><span class="sxs-lookup"><span data-stu-id="0be7a-252">The value of this header either matches the `Origin` header from the request or is the wildcard value `"*"`, meaning that any origin is allowed:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: https://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

<span data-ttu-id="0be7a-253">如果响应不包括`Access-Control-Allow-Origin`标头，跨域请求会失败。</span><span class="sxs-lookup"><span data-stu-id="0be7a-253">If the response doesn't include the `Access-Control-Allow-Origin` header, the cross-origin request fails.</span></span> <span data-ttu-id="0be7a-254">具体而言，在浏览器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="0be7a-254">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="0be7a-255">即使服务器返回成功的响应，请在浏览器不使响应可供客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="0be7a-255">Even if the server returns a successful response, the browser doesn't make the response available to the client app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0be7a-256">其他资源</span><span class="sxs-lookup"><span data-stu-id="0be7a-256">Additional resources</span></span>

* [<span data-ttu-id="0be7a-257">跨域资源共享 (CORS)</span><span class="sxs-lookup"><span data-stu-id="0be7a-257">Cross-Origin Resource Sharing (CORS)</span></span>](https://developer.mozilla.org/docs/Web/HTTP/CORS)
