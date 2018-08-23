---
title: 启用 ASP.NET Core 中的跨域请求 (CORS)
author: rick-anderson
description: 了解如何作为一种标准允许或拒绝在 ASP.NET Core 应用中的跨域请求的 CORS。
ms.author: riande
ms.date: 08/17/2018
uid: security/cors
ms.openlocfilehash: 0dbb7933c76bb0d1d0cab519ea08c6c8f0ebedfd
ms.sourcegitcommit: 64c2ca86fff445944b155635918126165ee0f8aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2018
ms.locfileid: "41832674"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a><span data-ttu-id="5518b-103">启用 ASP.NET Core 中的跨域请求 (CORS)</span><span class="sxs-lookup"><span data-stu-id="5518b-103">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>

<span data-ttu-id="5518b-104">作者：[Mike Wasson](https://github.com/mikewasson)、[Shayne Boyer](https://twitter.com/spboyer) 和 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5518b-104">By [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="5518b-105">浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="5518b-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="5518b-106">此限制称为“同源策略”，可防止恶意站点读取另一个站点中的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="5518b-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="5518b-107">但是，有时你可能需要允许其他站点对你的 Web API 进行跨域请求。</span><span class="sxs-lookup"><span data-stu-id="5518b-107">However, sometimes you might want to let other sites make cross-origin requests to your web API.</span></span>

<span data-ttu-id="5518b-108">[跨域资源共享](http://www.w3.org/TR/cors/)(CORS) 是一种 W3C 标准，允许服务器放宽同源策略。</span><span class="sxs-lookup"><span data-stu-id="5518b-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="5518b-109">使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="5518b-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="5518b-110">CORS 比早期技术（例如 [JSONP](https://wikipedia.org/wiki/JSONP)）更安全、更灵活。</span><span class="sxs-lookup"><span data-stu-id="5518b-110">CORS is safer and more flexible than earlier techniques such as [JSONP](https://wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="5518b-111">本主题演示如何在 ASP.NET Core 应用程序中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="5518b-111">This topic shows how to enable CORS in an ASP.NET Core application.</span></span>

## <a name="what-is-same-origin"></a><span data-ttu-id="5518b-112">什么是"相同的原点"？</span><span class="sxs-lookup"><span data-stu-id="5518b-112">What is "same origin"?</span></span>

<span data-ttu-id="5518b-113">如果它们具有相同方案、 主机和端口，两个 Url 将具有相同的原点。</span><span class="sxs-lookup"><span data-stu-id="5518b-113">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="5518b-114">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="5518b-114">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="5518b-115">以下两个 Url 具有相同的原点：</span><span class="sxs-lookup"><span data-stu-id="5518b-115">These two URLs have the same origin:</span></span>

* `http://example.com/foo.html`

* `http://example.com/bar.html`

<span data-ttu-id="5518b-116">这些 Url 有两个相对上一不同的源：</span><span class="sxs-lookup"><span data-stu-id="5518b-116">These URLs have different origins than the previous two:</span></span>

* <span data-ttu-id="5518b-117">`http://example.net` -不同的域</span><span class="sxs-lookup"><span data-stu-id="5518b-117">`http://example.net` - Different domain</span></span>

* <span data-ttu-id="5518b-118">`http://www.example.com/foo.html` -不同的子域</span><span class="sxs-lookup"><span data-stu-id="5518b-118">`http://www.example.com/foo.html` - Different subdomain</span></span>

* <span data-ttu-id="5518b-119">`https://example.com/foo.html` -不同的方案</span><span class="sxs-lookup"><span data-stu-id="5518b-119">`https://example.com/foo.html` - Different scheme</span></span>

* <span data-ttu-id="5518b-120">`http://example.com:9000/foo.html` -不同的端口</span><span class="sxs-lookup"><span data-stu-id="5518b-120">`http://example.com:9000/foo.html` - Different port</span></span>

> [!NOTE]
> <span data-ttu-id="5518b-121">比较来源时，Internet Explorer 不会考虑该端口。</span><span class="sxs-lookup"><span data-stu-id="5518b-121">Internet Explorer doesn't consider the port when comparing origins.</span></span>

## <a name="enable-cors"></a><span data-ttu-id="5518b-122">启用 CORS</span><span class="sxs-lookup"><span data-stu-id="5518b-122">Enable CORS</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="5518b-123">若要为应用程序设置 CORS，请将 `Microsoft.AspNetCore.Cors` 包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="5518b-123">To set up CORS for your application add the `Microsoft.AspNetCore.Cors` package to your project.</span></span>

::: moniker-end

<span data-ttu-id="5518b-124">调用[AddCors](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors)中`Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="5518b-124">Call [AddCors](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors)]

## <a name="enabling-cors-with-middleware"></a><span data-ttu-id="5518b-125">使用中间件启用 CORS</span><span class="sxs-lookup"><span data-stu-id="5518b-125">Enabling CORS with middleware</span></span>

<span data-ttu-id="5518b-126">若要启用 CORS，请将 CORS 中间件添加到请求管道使用`UseCors`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="5518b-126">To enable CORS, add the CORS middleware to the request pipeline using the `UseCors` extension method.</span></span> <span data-ttu-id="5518b-127">CORS 中间件必须位于之前定义的任何终结点应用程序中你想要支持跨域请求 (例如，对任何调用之前`UseMvc`)。</span><span class="sxs-lookup"><span data-stu-id="5518b-127">The CORS middleware must precede any defined endpoints in your app where you want to support cross-origin requests (For example, before any call to `UseMvc`).</span></span>

<span data-ttu-id="5518b-128">添加 CORS 中间件使用时，可以指定跨域策略[CorsPolicyBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors)类。</span><span class="sxs-lookup"><span data-stu-id="5518b-128">A cross-origin policy can be specified when adding the CORS middleware using the [CorsPolicyBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) class.</span></span> <span data-ttu-id="5518b-129">有两种方法可以实现此目的。</span><span class="sxs-lookup"><span data-stu-id="5518b-129">There are two ways to do this.</span></span> <span data-ttu-id="5518b-130">第一种是调用`UseCors`lambda:</span><span class="sxs-lookup"><span data-stu-id="5518b-130">The first is to call `UseCors` with a lambda:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

<span data-ttu-id="5518b-131">**注意：** 不含尾部斜杠，必须指定的 URL (`/`)。</span><span class="sxs-lookup"><span data-stu-id="5518b-131">**Note:** The URL must be specified without a trailing slash (`/`).</span></span> <span data-ttu-id="5518b-132">如果 URL 以终止`/`，该比较将返回`false`，并将返回无标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-132">If the URL terminates with `/`, the comparison will return `false` and no header will be returned.</span></span>

<span data-ttu-id="5518b-133">Lambda 采用`CorsPolicyBuilder`对象。</span><span class="sxs-lookup"><span data-stu-id="5518b-133">The lambda takes a `CorsPolicyBuilder` object.</span></span> <span data-ttu-id="5518b-134">您会发现一系列[配置选项](#cors-policy-options)本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="5518b-134">You'll find a list of the [configuration options](#cors-policy-options) later in this topic.</span></span> <span data-ttu-id="5518b-135">在此示例中，该策略允许跨域请求从`http://example.com`和任何其他来源。</span><span class="sxs-lookup"><span data-stu-id="5518b-135">In this example, the policy allows cross-origin requests from `http://example.com` and no other origins.</span></span>

<span data-ttu-id="5518b-136">CorsPolicyBuilder 具有 fluent API，因此您可以将方法调用链接：</span><span class="sxs-lookup"><span data-stu-id="5518b-136">CorsPolicyBuilder has a fluent API, so you can chain method calls:</span></span>

[!code-csharp[](../security/cors/sample/CorsExample3/Startup.cs?highlight=3&range=29-32)]

<span data-ttu-id="5518b-137">第二种方法是定义一个或多个命名的 CORS 策略，并在运行时按名称然后选择的策略。</span><span class="sxs-lookup"><span data-stu-id="5518b-137">The second approach is to define one or more named CORS policies, and then select the policy by name at run time.</span></span>

[!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin)]

<span data-ttu-id="5518b-138">此示例将添加一个名为"AllowSpecificOrigin"的 CORS 策略。</span><span class="sxs-lookup"><span data-stu-id="5518b-138">This example adds a CORS policy named "AllowSpecificOrigin".</span></span> <span data-ttu-id="5518b-139">若要选择的策略，将名称传递给`UseCors`。</span><span class="sxs-lookup"><span data-stu-id="5518b-139">To select the policy, pass the name to `UseCors`.</span></span>

## <a name="enabling-cors-in-mvc"></a><span data-ttu-id="5518b-140">在 MVC 启用 CORS</span><span class="sxs-lookup"><span data-stu-id="5518b-140">Enabling CORS in MVC</span></span>

<span data-ttu-id="5518b-141">您或者可以使用 MVC 应用每个操作，每个控制器，或全局范围内的所有控制器特定 CORS。</span><span class="sxs-lookup"><span data-stu-id="5518b-141">You can alternatively use MVC to apply specific CORS per action, per controller, or globally for all controllers.</span></span> <span data-ttu-id="5518b-142">使用 MVC 启用 CORS 时都使用相同的 CORS 服务，但 CORS 中间件不是。</span><span class="sxs-lookup"><span data-stu-id="5518b-142">When using MVC to enable CORS the same CORS services are used, but the CORS middleware isn't.</span></span>

### <a name="per-action"></a><span data-ttu-id="5518b-143">每个操作</span><span class="sxs-lookup"><span data-stu-id="5518b-143">Per action</span></span>

<span data-ttu-id="5518b-144">若要指定特定操作的 CORS 策略添加`[EnableCors]`属性为该操作。</span><span class="sxs-lookup"><span data-stu-id="5518b-144">To specify a CORS policy for a specific action add the `[EnableCors]` attribute to the action.</span></span> <span data-ttu-id="5518b-145">指定策略名称。</span><span class="sxs-lookup"><span data-stu-id="5518b-145">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction)]

### <a name="per-controller"></a><span data-ttu-id="5518b-146">每个控制器</span><span class="sxs-lookup"><span data-stu-id="5518b-146">Per controller</span></span>

<span data-ttu-id="5518b-147">若要指定特定控制器的 CORS 策略添加`[EnableCors]`属性到控制器类。</span><span class="sxs-lookup"><span data-stu-id="5518b-147">To specify the CORS policy for a specific controller add the `[EnableCors]` attribute to the controller class.</span></span> <span data-ttu-id="5518b-148">指定策略名称。</span><span class="sxs-lookup"><span data-stu-id="5518b-148">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController)]

### <a name="globally"></a><span data-ttu-id="5518b-149">全局</span><span class="sxs-lookup"><span data-stu-id="5518b-149">Globally</span></span>

<span data-ttu-id="5518b-150">您可以启用 CORS 全球所有控制器通过添加`CorsAuthorizationFilterFactory`筛选器添加到全局筛选器集合：</span><span class="sxs-lookup"><span data-stu-id="5518b-150">You can enable CORS globally for all controllers by adding the `CorsAuthorizationFilterFactory` filter to the global filter collection:</span></span>

[!code-csharp[](cors/sample/CorsMVC/Startup2.cs?name=snippet_configureservices)]

<span data-ttu-id="5518b-151">优先顺序是： 操作、 控制器、 全局。</span><span class="sxs-lookup"><span data-stu-id="5518b-151">The precedence order is: Action, controller, global.</span></span> <span data-ttu-id="5518b-152">操作级别的策略优先于控制器级别的策略，并且控制器级别的策略优先于全局策略。</span><span class="sxs-lookup"><span data-stu-id="5518b-152">Action-level policies take precedence over controller-level policies, and controller-level policies take precedence over global policies.</span></span>

### <a name="disable-cors"></a><span data-ttu-id="5518b-153">禁用 CORS</span><span class="sxs-lookup"><span data-stu-id="5518b-153">Disable CORS</span></span>

<span data-ttu-id="5518b-154">若要禁用 CORS 的控制器或操作，请使用`[DisableCors]`属性。</span><span class="sxs-lookup"><span data-stu-id="5518b-154">To disable CORS for a controller or action, use the `[DisableCors]` attribute.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction)]

## <a name="cors-policy-options"></a><span data-ttu-id="5518b-155">CORS 策略选项</span><span class="sxs-lookup"><span data-stu-id="5518b-155">CORS policy options</span></span>

<span data-ttu-id="5518b-156">本部分介绍您可以在 CORS 策略设置的各种选项。</span><span class="sxs-lookup"><span data-stu-id="5518b-156">This section describes the various options that you can set in a CORS policy.</span></span>

* [<span data-ttu-id="5518b-157">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="5518b-157">Set the allowed origins</span></span>](#set-the-allowed-origins)

* [<span data-ttu-id="5518b-158">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5518b-158">Set the allowed HTTP methods</span></span>](#set-the-allowed-http-methods)

* [<span data-ttu-id="5518b-159">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="5518b-159">Set the allowed request headers</span></span>](#set-the-allowed-request-headers)

* [<span data-ttu-id="5518b-160">设置公开的响应标头</span><span class="sxs-lookup"><span data-stu-id="5518b-160">Set the exposed response headers</span></span>](#set-the-exposed-response-headers)

* [<span data-ttu-id="5518b-161">跨域请求中的凭据</span><span class="sxs-lookup"><span data-stu-id="5518b-161">Credentials in cross-origin requests</span></span>](#credentials-in-cross-origin-requests)

* [<span data-ttu-id="5518b-162">将预检过期时间设置</span><span class="sxs-lookup"><span data-stu-id="5518b-162">Set the preflight expiration time</span></span>](#set-the-preflight-expiration-time)

<span data-ttu-id="5518b-163">有关一些选项，可能会有帮助读取[如何 CORS 工作](#how-cors-works)第一个。</span><span class="sxs-lookup"><span data-stu-id="5518b-163">For some options, it may be helpful to read [How CORS works](#how-cors-works) first.</span></span>

### <a name="set-the-allowed-origins"></a><span data-ttu-id="5518b-164">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="5518b-164">Set the allowed origins</span></span>

<span data-ttu-id="5518b-165">若要允许一个或多个特定源：</span><span class="sxs-lookup"><span data-stu-id="5518b-165">To allow one or more specific origins:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=19-23)]

<span data-ttu-id="5518b-166">若要允许所有来源：</span><span class="sxs-lookup"><span data-stu-id="5518b-166">To allow all origins:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs??range=27-31)]

<span data-ttu-id="5518b-167">允许任何来源的请求之前，请仔细考虑。</span><span class="sxs-lookup"><span data-stu-id="5518b-167">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="5518b-168">这意味着几乎任何网站可以进行 AJAX 调用 API。</span><span class="sxs-lookup"><span data-stu-id="5518b-168">It means that literally any website can make AJAX calls to your API.</span></span>

### <a name="set-the-allowed-http-methods"></a><span data-ttu-id="5518b-169">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5518b-169">Set the allowed HTTP methods</span></span>

<span data-ttu-id="5518b-170">若要允许所有 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="5518b-170">To allow all HTTP methods:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=44-49)]

<span data-ttu-id="5518b-171">这会影响预检请求和访问的控制的允许的方法标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-171">This affects pre-flight requests and Access-Control-Allow-Methods header.</span></span>

### <a name="set-the-allowed-request-headers"></a><span data-ttu-id="5518b-172">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="5518b-172">Set the allowed request headers</span></span>

<span data-ttu-id="5518b-173">CORS 预检请求可能包括一个访问控制的请求标头标头，列出应用程序设置的 HTTP 标头 (所谓"author 请求标头")。</span><span class="sxs-lookup"><span data-stu-id="5518b-173">A CORS preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span>

<span data-ttu-id="5518b-174">到允许列表的特定标头：</span><span class="sxs-lookup"><span data-stu-id="5518b-174">To whitelist specific headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=53-58)]

<span data-ttu-id="5518b-175">若要允许所有作者的请求标头：</span><span class="sxs-lookup"><span data-stu-id="5518b-175">To allow all author request headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=62-67)]

<span data-ttu-id="5518b-176">浏览器不在它们如何设置访问控制的请求标头完全一致。</span><span class="sxs-lookup"><span data-stu-id="5518b-176">Browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="5518b-177">如果将标头设置到的任何内容不是"\*"，您至少应包含"接受"，"内容类型"，，和"源"，以及你想要支持任何自定义标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-177">If you set headers to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

### <a name="set-the-exposed-response-headers"></a><span data-ttu-id="5518b-178">设置公开的响应标头</span><span class="sxs-lookup"><span data-stu-id="5518b-178">Set the exposed response headers</span></span>

<span data-ttu-id="5518b-179">默认情况下，在浏览器不会公开所有向应用程序的响应标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-179">By default, the browser doesn't expose all of the response headers to the application.</span></span> <span data-ttu-id="5518b-180">(请参阅[ http://www.w3.org/TR/cors/#simple-response-header ](http://www.w3.org/TR/cors/#simple-response-header)。)默认情况下可用的响应标头是：</span><span class="sxs-lookup"><span data-stu-id="5518b-180">(See [http://www.w3.org/TR/cors/#simple-response-header](http://www.w3.org/TR/cors/#simple-response-header).) The response headers that are available by default are:</span></span>

* <span data-ttu-id="5518b-181">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="5518b-181">Cache-Control</span></span>

* <span data-ttu-id="5518b-182">内容语言</span><span class="sxs-lookup"><span data-stu-id="5518b-182">Content-Language</span></span>

* <span data-ttu-id="5518b-183">Content-Type</span><span class="sxs-lookup"><span data-stu-id="5518b-183">Content-Type</span></span>

* <span data-ttu-id="5518b-184">过期</span><span class="sxs-lookup"><span data-stu-id="5518b-184">Expires</span></span>

* <span data-ttu-id="5518b-185">上次修改</span><span class="sxs-lookup"><span data-stu-id="5518b-185">Last-Modified</span></span>

* <span data-ttu-id="5518b-186">杂注</span><span class="sxs-lookup"><span data-stu-id="5518b-186">Pragma</span></span>

<span data-ttu-id="5518b-187">CORS 规范调用这些*简单响应标头*。</span><span class="sxs-lookup"><span data-stu-id="5518b-187">The CORS spec calls these *simple response headers*.</span></span> <span data-ttu-id="5518b-188">要使其他标头可用于应用程序：</span><span class="sxs-lookup"><span data-stu-id="5518b-188">To make other headers available to the application:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=71-76)]

### <a name="credentials-in-cross-origin-requests"></a><span data-ttu-id="5518b-189">跨域请求中的凭据</span><span class="sxs-lookup"><span data-stu-id="5518b-189">Credentials in cross-origin requests</span></span>

<span data-ttu-id="5518b-190">凭据要求特殊处理 CORS 请求中。</span><span class="sxs-lookup"><span data-stu-id="5518b-190">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="5518b-191">默认情况下，在浏览器不会发送与跨域请求的任何凭据。</span><span class="sxs-lookup"><span data-stu-id="5518b-191">By default, the browser doesn't send any credentials with a cross-origin request.</span></span> <span data-ttu-id="5518b-192">凭据包含 cookie，以及 HTTP 身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="5518b-192">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="5518b-193">若要发送凭据与跨域请求，客户端必须设置为 true 的 XMLHttpRequest.withCredentials。</span><span class="sxs-lookup"><span data-stu-id="5518b-193">To send credentials with a cross-origin request, the client must set XMLHttpRequest.withCredentials to true.</span></span>

<span data-ttu-id="5518b-194">直接使用 XMLHttpRequest:</span><span class="sxs-lookup"><span data-stu-id="5518b-194">Using XMLHttpRequest directly:</span></span>

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://www.example.com/api/test');
xhr.withCredentials = true;
```

<span data-ttu-id="5518b-195">在 jQuery 中：</span><span class="sxs-lookup"><span data-stu-id="5518b-195">In jQuery:</span></span>

```jQuery
$.ajax({
  type: 'get',
  url: 'http://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

<span data-ttu-id="5518b-196">此外，服务器必须允许凭据。</span><span class="sxs-lookup"><span data-stu-id="5518b-196">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="5518b-197">若要允许跨域凭据：</span><span class="sxs-lookup"><span data-stu-id="5518b-197">To allow cross-origin credentials:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=80-85)]

<span data-ttu-id="5518b-198">现在，HTTP 响应将包括一个访问控制的允许的凭据标头，服务器允许跨域请求凭据将告诉浏览器。</span><span class="sxs-lookup"><span data-stu-id="5518b-198">Now the HTTP response will include an Access-Control-Allow-Credentials header, which tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="5518b-199">如果浏览器发送的凭据，但响应不包含有效的访问控制的允许的凭据标头，在浏览器就不会暴露给应用程序，响应和 AJAX 请求失败。</span><span class="sxs-lookup"><span data-stu-id="5518b-199">If the browser sends credentials, but the response doesn't include a valid Access-Control-Allow-Credentials header, the browser won't expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="5518b-200">允许跨域凭据时要小心。</span><span class="sxs-lookup"><span data-stu-id="5518b-200">Be careful when allowing cross-origin credentials.</span></span> <span data-ttu-id="5518b-201">在另一个域的网站可以向应用而无需在用户不知情的用户的名义发送登录的用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="5518b-201">A website at another domain can send a logged-in user's credentials to the app on the user's behalf without the user's knowledge.</span></span> <span data-ttu-id="5518b-202">CORS 规范还会说明该设置到来源`"*"`（所有来源） 是无效的如果`Access-Control-Allow-Credentials`标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-202">The CORS specification also states that setting origins to `"*"` (all origins) is invalid if the `Access-Control-Allow-Credentials` header is present.</span></span>

### <a name="set-the-preflight-expiration-time"></a><span data-ttu-id="5518b-203">将预检过期时间设置</span><span class="sxs-lookup"><span data-stu-id="5518b-203">Set the preflight expiration time</span></span>

<span data-ttu-id="5518b-204">访问控制的最大有效期标头指定可以缓存预检请求的响应的时间。</span><span class="sxs-lookup"><span data-stu-id="5518b-204">The Access-Control-Max-Age header specifies how long the response to the preflight request can be cached.</span></span> <span data-ttu-id="5518b-205">若要设置此标头：</span><span class="sxs-lookup"><span data-stu-id="5518b-205">To set this header:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=89-94)]

<a name="cors-how-cors-works"></a>

## <a name="how-cors-works"></a><span data-ttu-id="5518b-206">CORS 的工作原理</span><span class="sxs-lookup"><span data-stu-id="5518b-206">How CORS works</span></span>

<span data-ttu-id="5518b-207">本部分介绍在 CORS 请求的 HTTP 消息级别中会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="5518b-207">This section describes what happens in a CORS request at the level of the HTTP messages.</span></span> <span data-ttu-id="5518b-208">请务必了解，以便可以正确配置和调试时出现意外的行为的 CORS 策略 CORS 的工作原理。</span><span class="sxs-lookup"><span data-stu-id="5518b-208">It's important to understand how CORS works so that the CORS policy can be configured correctly and debugged when unexpected behaviors occur.</span></span>

<span data-ttu-id="5518b-209">CORS 规范引入了几个新的 HTTP 标头启用跨域请求。</span><span class="sxs-lookup"><span data-stu-id="5518b-209">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="5518b-210">如果浏览器支持 CORS，则将设置自动跨域请求这些标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-210">If a browser supports CORS, it sets these headers automatically for cross-origin requests.</span></span> <span data-ttu-id="5518b-211">自定义 JavaScript 代码不需要启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="5518b-211">Custom JavaScript code isn't required to enable CORS.</span></span>

<span data-ttu-id="5518b-212">下面是跨域请求的示例。</span><span class="sxs-lookup"><span data-stu-id="5518b-212">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="5518b-213">`Origin`标头提供发出请求的站点的域：</span><span class="sxs-lookup"><span data-stu-id="5518b-213">The `Origin` header provides the domain of the site that's making the request:</span></span>

```
GET http://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: http://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: http://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

<span data-ttu-id="5518b-214">如果服务器允许该请求，则将在响应中设置访问控制的允许的域标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-214">If the server allows the request, it sets the Access-Control-Allow-Origin header in the response.</span></span> <span data-ttu-id="5518b-215">此标头的值匹配源标头从请求，或为通配符值"\*"，允许任何源的含义：</span><span class="sxs-lookup"><span data-stu-id="5518b-215">The value of this header either matches the Origin header from the request, or is the wildcard value "\*", meaning that any origin is allowed:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

<span data-ttu-id="5518b-216">如果响应不包含访问控制的允许的域标头，AJAX 请求失败。</span><span class="sxs-lookup"><span data-stu-id="5518b-216">If the response doesn't include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="5518b-217">具体而言，在浏览器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="5518b-217">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="5518b-218">即使服务器返回成功的响应，请在浏览器不会使响应可供客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="5518b-218">Even if the server returns a successful response, the browser doesn't make the response available to the client application.</span></span>

### <a name="preflight-requests"></a><span data-ttu-id="5518b-219">预检请求</span><span class="sxs-lookup"><span data-stu-id="5518b-219">Preflight Requests</span></span>

<span data-ttu-id="5518b-220">对于某些 CORS 请求，浏览器发送额外的请求，名为"预检请求，"，再发送实际请求的资源。</span><span class="sxs-lookup"><span data-stu-id="5518b-220">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span> <span data-ttu-id="5518b-221">在浏览器可以跳过预检请求，如果满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="5518b-221">The browser can skip the preflight request if the following conditions are true:</span></span>

* <span data-ttu-id="5518b-222">请求方法是 GET、 HEAD 或 POST，和</span><span class="sxs-lookup"><span data-stu-id="5518b-222">The request method is GET, HEAD, or POST, and</span></span>

* <span data-ttu-id="5518b-223">应用程序不会设置之外接受，接受语言的内容语言，任何请求标头内容类型或最后一个事件 ID 和</span><span class="sxs-lookup"><span data-stu-id="5518b-223">The application doesn't set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, and</span></span>

* <span data-ttu-id="5518b-224">内容类型标头 (如果设置) 是以下之一：</span><span class="sxs-lookup"><span data-stu-id="5518b-224">The Content-Type header (if set) is one of the following:</span></span>

  * <span data-ttu-id="5518b-225">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="5518b-225">application/x-www-form-urlencoded</span></span>

  * <span data-ttu-id="5518b-226">多部分/窗体数据</span><span class="sxs-lookup"><span data-stu-id="5518b-226">multipart/form-data</span></span>

  * <span data-ttu-id="5518b-227">文本/无格式</span><span class="sxs-lookup"><span data-stu-id="5518b-227">text/plain</span></span>

<span data-ttu-id="5518b-228">有关请求标头规则适用于通过 XMLHttpRequest 对象上调用 setRequestHeader 来设置应用程序的标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-228">The rule about request headers applies to headers that the application sets by calling setRequestHeader on the XMLHttpRequest object.</span></span> <span data-ttu-id="5518b-229">（CORS 规范调用这些"作者请求标头"。）此规则不适用于在浏览器可以设置，例如用户代理、 主机或内容长度标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-229">(The CORS specification calls these "author request headers".) The rule doesn't apply to headers the browser can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="5518b-230">下面是预检请求的示例：</span><span class="sxs-lookup"><span data-stu-id="5518b-230">Here is an example of a preflight request:</span></span>

```
OPTIONS http://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: http://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

<span data-ttu-id="5518b-231">预检请求使用 HTTP OPTIONS 方法。</span><span class="sxs-lookup"><span data-stu-id="5518b-231">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="5518b-232">它包括两个特殊的标头：</span><span class="sxs-lookup"><span data-stu-id="5518b-232">It includes two special headers:</span></span>

* <span data-ttu-id="5518b-233">访问控制的请求的方法： 将用作实际请求 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="5518b-233">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>

* <span data-ttu-id="5518b-234">访问的控件的请求的标头： 在实际请求的应用程序设置的请求标头的列表。</span><span class="sxs-lookup"><span data-stu-id="5518b-234">Access-Control-Request-Headers: A list of request headers that the application set on the actual request.</span></span> <span data-ttu-id="5518b-235">（同样，这不包括在浏览器设置的标头。）</span><span class="sxs-lookup"><span data-stu-id="5518b-235">(Again, this doesn't include headers that the browser sets.)</span></span>

<span data-ttu-id="5518b-236">下面是示例响应中，假定服务器允许请求：</span><span class="sxs-lookup"><span data-stu-id="5518b-236">Here is an example response, assuming that the server allows the request:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

<span data-ttu-id="5518b-237">响应包括访问的控制的允许的方法标头，其中列出了允许的方法，和 （可选） 访问的控制的允许的标头标头，其中列出了允许的标头。</span><span class="sxs-lookup"><span data-stu-id="5518b-237">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="5518b-238">如果预检请求成功，则浏览器发送实际请求，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="5518b-238">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>
