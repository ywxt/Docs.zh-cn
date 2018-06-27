---
title: ASP.NET Core 中的 URL 重写中间件
author: guardrex
description: 了解如何在 ASP.NET Core 应用程序中使用 URL 重写中间件进行 URL 重写和重定向。
manager: wpickett
ms.author: riande
ms.date: 08/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/url-rewriting
ms.openlocfilehash: a4ffa512825fedafdc58ade9929097e255593fa9
ms.sourcegitcommit: 40b102ecf88e53d9d872603ce6f3f7044bca95ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35652209"
---
# <a name="url-rewriting-middleware-in-aspnet-core"></a><span data-ttu-id="7c6cd-103">ASP.NET Core 中的 URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="7c6cd-103">URL Rewriting Middleware in ASP.NET Core</span></span>

<span data-ttu-id="7c6cd-104">作者：[Luke Latham](https://github.com/guardrex) 和 [Mikael Mengistu](https://github.com/mikaelm12)</span><span class="sxs-lookup"><span data-stu-id="7c6cd-104">By [Luke Latham](https://github.com/guardrex) and [Mikael Mengistu](https://github.com/mikaelm12)</span></span>

<span data-ttu-id="7c6cd-105">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="7c6cd-106">URL 重写是根据一个或多个预定义规则修改请求 URL 的行为。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-106">URL rewriting is the act of modifying request URLs based on one or more predefined rules.</span></span> <span data-ttu-id="7c6cd-107">URL 重写会在资源位置和地址之间创建一个抽象，使位置和地址不紧密相连。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-107">URL rewriting creates an abstraction between resource locations and their addresses so that the locations and addresses are not tightly linked.</span></span> <span data-ttu-id="7c6cd-108">在以下几种方案中，URL 重写很有价值：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-108">There are several scenarios where URL rewriting is valuable:</span></span>

* <span data-ttu-id="7c6cd-109">暂时或永久移动或替换服务器资源，同时维护这些资源的稳定定位符。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-109">Moving or replacing server resources temporarily or permanently while maintaining stable locators for those resources.</span></span>
* <span data-ttu-id="7c6cd-110">拆分在不同应用或同一应用的不同区域中处理的请求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-110">Splitting request processing across different apps or across areas of one app.</span></span>
* <span data-ttu-id="7c6cd-111">删除、添加或重新组织传入请求上的 URL 段。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-111">Removing, adding, or reorganizing URL segments on incoming requests.</span></span>
* <span data-ttu-id="7c6cd-112">优化搜索引擎优化 (SEO) 的公共 URL。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-112">Optimizing public URLs for Search Engine Optimization (SEO).</span></span>
* <span data-ttu-id="7c6cd-113">允许使用友好的公共 URL 帮助用户预测他们将通过链接找到的内容。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-113">Permitting the use of friendly public URLs to help people predict the content they will find by following a link.</span></span>
* <span data-ttu-id="7c6cd-114">将不安全请求重定向到安全终结点。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-114">Redirecting insecure requests to secure endpoints.</span></span>
* <span data-ttu-id="7c6cd-115">阻止映像盗链。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-115">Preventing image hotlinking.</span></span>

<span data-ttu-id="7c6cd-116">可通过多种方式定义更改 URL 的规则，包括正则表达式、Apache mod_rewrite 模块规则、IIS 重写模块规则以及使用自定义规则逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-116">You can define rules for changing the URL in several ways, including Regex, Apache mod_rewrite module rules, IIS Rewrite Module rules, and using custom rule logic.</span></span> <span data-ttu-id="7c6cd-117">本文档介绍 URL 重写并说明如何在 ASP.NET Core 应用中使用 URL 重写中间件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-117">This document introduces URL rewriting with instructions on how to use URL Rewriting Middleware in ASP.NET Core apps.</span></span>

> [!NOTE]
> <span data-ttu-id="7c6cd-118">URL 重写可能会降低应用的性能。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-118">URL rewriting can reduce the performance of an app.</span></span> <span data-ttu-id="7c6cd-119">如果可行，应限制规则的数量和复杂度。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-119">Where feasible, you should limit the number and complexity of rules.</span></span>

## <a name="url-redirect-and-url-rewrite"></a><span data-ttu-id="7c6cd-120">URL 重定向和 URL 重写</span><span class="sxs-lookup"><span data-stu-id="7c6cd-120">URL redirect and URL rewrite</span></span>

<span data-ttu-id="7c6cd-121">URL 重定向和 URL 重写之间的用词差异乍一看可能很细微，但这对于向客户端提供资源具有重要意义。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-121">The difference in wording between *URL redirect* and *URL rewrite* may seem subtle at first but has important implications for providing resources to clients.</span></span> <span data-ttu-id="7c6cd-122">ASP.NET Core 的 URL 重写中间件能够满足两者的需求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-122">ASP.NET Core's URL Rewriting Middleware is capable of meeting the need for both.</span></span>

<span data-ttu-id="7c6cd-123">URL 重定向是客户端操作，指示客户端访问另一个地址的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-123">A *URL redirect* is a client-side operation, where the client is instructed to access a resource at another address.</span></span> <span data-ttu-id="7c6cd-124">这需要往返服务器。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-124">This requires a round-trip to the server.</span></span> <span data-ttu-id="7c6cd-125">客户端对资源发出新请求时，返回客户端的重定向 URL 会出现在浏览器地址栏。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-125">The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</span></span> 

<span data-ttu-id="7c6cd-126">如果将 `/resource` 重定向到 `/different-resource`，客户端会请求`/resource`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-126">If `/resource` is *redirected* to `/different-resource`, the client requests `/resource`.</span></span> <span data-ttu-id="7c6cd-127">服务器通过指示重定向是临时还是永久的状态代码作出响应，表示客户端应该获取 `/different-resource` 处的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-127">The server responds that the client should obtain the resource at `/different-resource` with a status code indicating that the redirect is either temporary or permanent.</span></span> <span data-ttu-id="7c6cd-128">客户端在重定向 URL 处对资源执行新的请求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-128">The client executes a new request for the resource at the redirect URL.</span></span>

![WebAPI 服务终结点已暂时从服务器上的版本 1 (v1) 更改为版本 2 (v2)。](url-rewriting/_static/url_redirect.png)

<span data-ttu-id="7c6cd-134">将请求重定向到不同的 URL 时，可指示重定向是永久的还是临时的。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-134">When redirecting requests to a different URL, you indicate whether the redirect is permanent or temporary.</span></span> <span data-ttu-id="7c6cd-135">如果资源有一个新的永久性 URL，并且你希望指示客户端所有将来的资源请求都使用新 URL，则使用“301 (永久移动)”状态代码。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-135">The 301 (Moved Permanently) status code is used where the resource has a new, permanent URL and you wish to instruct the client that all future requests for the resource should use the new URL.</span></span> <span data-ttu-id="7c6cd-136">收到 301 状态代码时，客户端可能会缓存响应。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-136">*The client may cache the response when a 301 status code is received.*</span></span> <span data-ttu-id="7c6cd-137">如果重定向是临时的或一般会更改的，则使用“302 (已找到)”状态代码，以使客户端将来不应存储和重用重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-137">The 302 (Found) status code is used where the redirection is temporary or generally subject to change, such that the client shouldn't store and reuse the redirect URL in the future.</span></span> <span data-ttu-id="7c6cd-138">有关详细信息，请参阅 [RFC 2616：状态代码定义](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-138">For more information, see [RFC 2616: Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>

<span data-ttu-id="7c6cd-139">URL 重写是服务器端操作，提供来自不同资源地址的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-139">A *URL rewrite* is a server-side operation to provide a resource from a different resource address.</span></span> <span data-ttu-id="7c6cd-140">重写 URL 不需要往返服务器。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-140">Rewriting a URL doesn't require a round-trip to the server.</span></span> <span data-ttu-id="7c6cd-141">重写的 URL 不会返回客户端，也不会出现在浏览器地址栏。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-141">The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</span></span> <span data-ttu-id="7c6cd-142">`/resource` 重写到 `/different-resource` 时，客户端会请求 `/resource`，并且服务器会在内部提取 `/different-resource` 处的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-142">When `/resource` is *rewritten* to `/different-resource`, the client requests `/resource`, and the server *internally* fetches the resource at `/different-resource`.</span></span> <span data-ttu-id="7c6cd-143">尽管客户端可能能够检索已重写 URL 处的资源，但是，客户端发出请求并收到响应时，并不会知道已重写 URL 处存在的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-143">Although the client might be able to retrieve the resource at the rewritten URL, the client won't be informed that the resource exists at the rewritten URL when it makes its request and receives the response.</span></span>

![WebAPI 服务终结点已从服务器上的版本 1 (v1) 更改为版本 2 (v2)。](url-rewriting/_static/url_rewrite.png)

## <a name="url-rewriting-sample-app"></a><span data-ttu-id="7c6cd-148">URL 重写示例应用</span><span class="sxs-lookup"><span data-stu-id="7c6cd-148">URL rewriting sample app</span></span>

<span data-ttu-id="7c6cd-149">可使用 [URL 重写示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/)了解 URL 重写中间件的功能。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-149">You can explore the features of the URL Rewriting Middleware with the [URL rewriting sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/sample/).</span></span> <span data-ttu-id="7c6cd-150">此应用使用重写和重定向规则，并显示重写或重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-150">The app applies rewrite and redirect rules and shows the rewritten or redirected URL.</span></span>

## <a name="when-to-use-url-rewriting-middleware"></a><span data-ttu-id="7c6cd-151">何时使用 URL 重写中间件</span><span class="sxs-lookup"><span data-stu-id="7c6cd-151">When to use URL Rewriting Middleware</span></span>

<span data-ttu-id="7c6cd-152">无法结合使用 [URL 重写模块](https://www.iis.net/downloads/microsoft/url-rewrite)和 Windows Server 上的 IIS、Apache Server 上的 [Apache mod_rewrite 模块](https://httpd.apache.org/docs/2.4/rewrite/)、[Nginx 上的 URL 重写](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)，或者应用托管在 [HTTP.sys 服务器](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）上时，请使用 URL 重写中间件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-152">Use URL Rewriting Middleware when you are unable to use the [URL Rewrite module](https://www.iis.net/downloads/microsoft/url-rewrite) with IIS on Windows Server, the [Apache mod_rewrite module](https://httpd.apache.org/docs/2.4/rewrite/) on Apache Server, [URL rewriting on Nginx](https://www.nginx.com/blog/creating-nginx-rewrite-rules/), or your app is hosted on [HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="7c6cd-153">在 IIS、Apache 或 Nginx 中使用基于服务器的 URL 重写技术的主要原因是，中间件不支持这些模块的全部功能，而且中间件的性能可能与模块的性能不匹配。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-153">The main reasons to use the server-based URL rewriting technologies in IIS, Apache, or Nginx are that the middleware doesn't support the full features of these modules and the performance of the middleware probably won't match that of the modules.</span></span> <span data-ttu-id="7c6cd-154">但是，服务器模块的某些功能不适用于 ASP.NET Core 项目，例如 IIS 重写模块的 `IsFile` 和 `IsDirectory` 约束。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-154">However, there are some features of the server modules that don't work with ASP.NET Core projects, such as the `IsFile` and `IsDirectory` constraints of the IIS Rewrite module.</span></span> <span data-ttu-id="7c6cd-155">在这些情况下，请改为使用中间件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-155">In these scenarios, use the middleware instead.</span></span>

## <a name="package"></a><span data-ttu-id="7c6cd-156">Package</span><span class="sxs-lookup"><span data-stu-id="7c6cd-156">Package</span></span>

<span data-ttu-id="7c6cd-157">要将中间件包含在项目中，请添加对 [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) 包的引用。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-157">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.Rewrite`](https://www.nuget.org/packages/Microsoft.AspNetCore.Rewrite/) package.</span></span> <span data-ttu-id="7c6cd-158">此功能适用于面向 ASP.NET Core 1.1 或更高版本的应用。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-158">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="extension-and-options"></a><span data-ttu-id="7c6cd-159">扩展和选项</span><span class="sxs-lookup"><span data-stu-id="7c6cd-159">Extension and options</span></span>

<span data-ttu-id="7c6cd-160">通过使用扩展方法为每条规则创建 `RewriteOptions` 类的实例，建立 URL 重写和重定向规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-160">Establish your URL rewrite and redirect rules by creating an instance of the `RewriteOptions` class with extension methods for each of your rules.</span></span> <span data-ttu-id="7c6cd-161">按所需的处理顺序链接多个规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-161">Chain multiple rules in the order that you would like them processed.</span></span> <span data-ttu-id="7c6cd-162">使用 `app.UseRewriter(options);` 将 `RewriteOptions` 添加到请求管道时，它会被传递到 URL 重写中间件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-162">The `RewriteOptions` are passed into the URL Rewriting Middleware as it's added to the request pipeline with `app.UseRewriter(options);`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-163">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-163">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-164">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-164">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1")
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true)
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")
        .Add(RedirectXMLRequests)
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

---

### <a name="url-redirect"></a><span data-ttu-id="7c6cd-165">URL 重定向</span><span class="sxs-lookup"><span data-stu-id="7c6cd-165">URL redirect</span></span>

<span data-ttu-id="7c6cd-166">使用 `AddRedirect` 将请求重定向。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-166">Use `AddRedirect` to redirect requests.</span></span> <span data-ttu-id="7c6cd-167">第一个参数包含用于匹配传入 URL 路径的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-167">The first parameter contains your regex for matching on the path of the incoming URL.</span></span> <span data-ttu-id="7c6cd-168">第二个参数是替换字符串。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-168">The second parameter is the replacement string.</span></span> <span data-ttu-id="7c6cd-169">第三个参数（如有）指定状态代码。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-169">The third parameter, if present, specifies the status code.</span></span> <span data-ttu-id="7c6cd-170">如不指定状态代码，则默认为“302 (已找到)”，指示资源暂时移动或替换。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-170">If you don't specify the status code, it defaults to 302 (Found), which indicates that the resource is temporarily moved or replaced.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-171">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-171">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-172">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-172">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirect("redirect-rule/(.*)", "redirected/$1");

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-173">在启用了开发人员工具的浏览器中，向路径为 `/redirect-rule/1234/5678` 的示例应用发出请求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-173">In a browser with developer tools enabled, make a request to the sample app with the path `/redirect-rule/1234/5678`.</span></span> <span data-ttu-id="7c6cd-174">正则表达式匹配 `redirect-rule/(.*)` 上的请求路径，且该路径会被 `/redirected/1234/5678` 替代。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-174">The regex matches the request path on `redirect-rule/(.*)`, and the path is replaced with `/redirected/1234/5678`.</span></span> <span data-ttu-id="7c6cd-175">重定向 URL 以“302 (已找到)”状态代码发回客户端。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-175">The redirect URL is sent back to the client with a 302 (Found) status code.</span></span> <span data-ttu-id="7c6cd-176">浏览器会在浏览器地址栏中出现的重定向 URL 上发出新请求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-176">The browser makes a new request at the redirect URL, which appears in the browser's address bar.</span></span> <span data-ttu-id="7c6cd-177">由于示例应用中的任何规则均不匹配重定向 URL，因此第二个请求会收到来自应用的“200 (正常)”响应，且响应正文会显示此重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-177">Since no rules in the sample app match on the redirect URL, the second request receives a 200 (OK) response from the app and the body of the response shows the redirect URL.</span></span> <span data-ttu-id="7c6cd-178">重定向 URL 时，系统将向服务器进行一次往返。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-178">A roundtrip is made to the server when a URL is *redirected*.</span></span>

> [!WARNING]
> <span data-ttu-id="7c6cd-179">建立重定向规则时务必小心。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-179">Be cautious when establishing your redirect rules.</span></span> <span data-ttu-id="7c6cd-180">系统会根据应用的每个请求（包括重定向后的请求）对重定向规则进行评估。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-180">Your redirect rules are evaluated on each request to the app, including after a redirect.</span></span> <span data-ttu-id="7c6cd-181">很容易便会意外创建无限重定向循环。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-181">It's easy to accidently create a loop of infinite redirects.</span></span>

<span data-ttu-id="7c6cd-182">原始请求：`/redirect-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-182">Original Request: `/redirect-rule/1234/5678`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_redirect.png)

<span data-ttu-id="7c6cd-184">括号内的表达式部分称为“捕获组”。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-184">The part of the expression contained within parentheses is called a *capture group*.</span></span> <span data-ttu-id="7c6cd-185">表达式的点 (`.`) 表示匹配任何字符。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-185">The dot (`.`) of the expression means *match any character*.</span></span> <span data-ttu-id="7c6cd-186">星号 (`*`) 表示零次或多次匹配前面的字符。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-186">The asterisk (`*`) indicates *match the preceding character zero or more times*.</span></span> <span data-ttu-id="7c6cd-187">因此，URL 的最后两个路径段 `1234/5678` 由捕获组 `(.*)` 捕获。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-187">Therefore, the last two path segments of the URL, `1234/5678`, are captured by capture group `(.*)`.</span></span> <span data-ttu-id="7c6cd-188">在请求 URL 中提供的位于 `redirect-rule/` 之后的任何值均由此单个捕获组捕获。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-188">Any value you provide in the request URL after `redirect-rule/` is captured by this single capture group.</span></span>

<span data-ttu-id="7c6cd-189">在替换字符串中，将捕获组注入带有美元符号 (`$`)、后跟捕获序列号的字符串中。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-189">In the replacement string, captured groups are injected into the string with the dollar sign (`$`) followed by the sequence number of the capture.</span></span> <span data-ttu-id="7c6cd-190">获取的第一个捕获组值为 `$1`，第二个为 `$2`，并且正则表达式中的其他捕获组值将依次继续排列。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-190">The first capture group value is obtained with `$1`, the second with `$2`, and they continue in sequence for the capture groups in your regex.</span></span> <span data-ttu-id="7c6cd-191">示例应用的重定向规则正则表达式中只有一个捕获组，因此替换字符串中只有一个注入组，即 `$1`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-191">There's only one captured group in the redirect rule regex in the sample app, so there's only one injected group in the replacement string, which is `$1`.</span></span> <span data-ttu-id="7c6cd-192">如果应用此规则，URL 将变为 `/redirected/1234/5678`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-192">When the rule is applied, the URL becomes `/redirected/1234/5678`.</span></span>

### <a name="url-redirect-to-a-secure-endpoint"></a><span data-ttu-id="7c6cd-193">URL 重定向到安全的终结点</span><span class="sxs-lookup"><span data-stu-id="7c6cd-193">URL redirect to a secure endpoint</span></span>

<span data-ttu-id="7c6cd-194">使用 `AddRedirectToHttps` 将 HTTP 请求重定向到采用 HTTPS (`https://`) 的相同主机和路径。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-194">Use `AddRedirectToHttps` to redirect HTTP requests to the same host and path using HTTPS (`https://`).</span></span> <span data-ttu-id="7c6cd-195">如不提供状态代码，则中间件默认为“302(已找到)”。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-195">If the status code isn't supplied, the middleware defaults to 302 (Found).</span></span> <span data-ttu-id="7c6cd-196">如不提供端口，则中间件默认为 `null`，这表示协议更改为 `https://` 且客户端访问端口 443 上的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-196">If the port isn't supplied, the middleware defaults to `null`, which means the protocol changes to `https://` and the client accesses the resource on port 443.</span></span> <span data-ttu-id="7c6cd-197">该示例演示如何将状态代码设置为“301(永久移动)”并将端口更改为 5001。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-197">The example shows how to set the status code to 301 (Moved Permanently) and change the port to 5001.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttps(301, 5001);

    app.UseRewriter(options);
}
```

<span data-ttu-id="7c6cd-198">使用 `AddRedirectToHttpsPermanent` 将不安全的请求重定向到采用安全 HTTPS 协议（端口 443 上的 `https://`）的相同主机和路径。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-198">Use `AddRedirectToHttpsPermanent` to redirect insecure requests to the same host and path with secure HTTPS protocol (`https://` on port 443).</span></span> <span data-ttu-id="7c6cd-199">中间件将状态代码设置为“301 (永久移动)”。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-199">The middleware sets the status code to 301 (Moved Permanently).</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRedirectToHttpsPermanent();

    app.UseRewriter(options);
}
```

> [!NOTE]
> <span data-ttu-id="7c6cd-200">当重定向到 HTTPS 并且不需要其他重定向规则时，建议使用 HTTPS 重定向中间件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-200">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware.</span></span> <span data-ttu-id="7c6cd-201">有关详细信息，请参阅[强制使用 HTTPS](xref:security/enforcing-ssl#require-https)主题。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-201">For more information, see the [Enforce HTTPS](xref:security/enforcing-ssl#require-https) topic.</span></span>

<span data-ttu-id="7c6cd-202">示例应用能够演示如何使用 `AddRedirectToHttps` 或 `AddRedirectToHttpsPermanent`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-202">The sample app is capable of demonstrating how to use `AddRedirectToHttps` or `AddRedirectToHttpsPermanent`.</span></span> <span data-ttu-id="7c6cd-203">将扩展方法添加到 `RewriteOptions`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-203">Add the extension method to the `RewriteOptions`.</span></span> <span data-ttu-id="7c6cd-204">在任何 URL 上向应用发出不安全的请求。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-204">Make an insecure request to the app at any URL.</span></span> <span data-ttu-id="7c6cd-205">消除自签名证书不受信任的浏览器安全警告，或创建例外以信任证书。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-205">Dismiss the browser security warning that the self-signed certificate is untrusted or create an exception to trust the certificate.</span></span>

<span data-ttu-id="7c6cd-206">使用 `AddRedirectToHttps(301, 5001)` 的原始请求：`http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-206">Original Request using `AddRedirectToHttps(301, 5001)`: `http://localhost:5000/secure`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_redirect_to_https.png)

<span data-ttu-id="7c6cd-208">使用 `AddRedirectToHttpsPermanent` 的原始请求：`http://localhost:5000/secure`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-208">Original Request using `AddRedirectToHttpsPermanent`: `http://localhost:5000/secure`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_redirect_to_https_permanent.png)

### <a name="url-rewrite"></a><span data-ttu-id="7c6cd-210">URL 重写</span><span class="sxs-lookup"><span data-stu-id="7c6cd-210">URL rewrite</span></span>

<span data-ttu-id="7c6cd-211">使用 `AddRewrite` 创建重写 URL 的规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-211">Use `AddRewrite` to create a rule for rewriting URLs.</span></span> <span data-ttu-id="7c6cd-212">第一个参数包含用于匹配传入 URL 路径的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-212">The first parameter contains your regex for matching on the incoming URL path.</span></span> <span data-ttu-id="7c6cd-213">第二个参数是替换字符串。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-213">The second parameter is the replacement string.</span></span> <span data-ttu-id="7c6cd-214">第三个参数 `skipRemainingRules: {true|false}` 指示如果当前规则适用，中间件是否要跳过其他重写规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-214">The third parameter, `skipRemainingRules: {true|false}`, indicates to the middleware whether or not to skip additional rewrite rules if the current rule is applied.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-215">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-215">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=10-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-216">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-216">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", 
            skipRemainingRules: true);

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-217">原始请求：`/rewrite-rule/1234/5678`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-217">Original Request: `/rewrite-rule/1234/5678`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_rewrite.png)

<span data-ttu-id="7c6cd-219">在正则表达式中首先注意到的是表达式开头的脱字号 (`^`)。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-219">The first thing you notice in the regex is the carat (`^`) at the beginning of the expression.</span></span> <span data-ttu-id="7c6cd-220">这意味着匹配从 URL 路径的开头处开始。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-220">This means that matching starts at the beginning of the URL path.</span></span>

<span data-ttu-id="7c6cd-221">在上述采用重定向规则 `redirect-rule/(.*)` 的示例中，正则表达式的开头没有任何脱字号；因此，成功匹配的路径中的任何字符都可以位于 `redirect-rule/` 之前。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-221">In the earlier example with the redirect rule, `redirect-rule/(.*)`, there's no carat at the start of the regex; therefore, any characters may precede `redirect-rule/` in the path for a successful match.</span></span>

| <span data-ttu-id="7c6cd-222">路径</span><span class="sxs-lookup"><span data-stu-id="7c6cd-222">Path</span></span>                               | <span data-ttu-id="7c6cd-223">匹配</span><span class="sxs-lookup"><span data-stu-id="7c6cd-223">Match</span></span> |
| ---------------------------------- | :---: |
| `/redirect-rule/1234/5678`         | <span data-ttu-id="7c6cd-224">是</span><span class="sxs-lookup"><span data-stu-id="7c6cd-224">Yes</span></span>   |
| `/my-cool-redirect-rule/1234/5678` | <span data-ttu-id="7c6cd-225">是</span><span class="sxs-lookup"><span data-stu-id="7c6cd-225">Yes</span></span>   |
| `/anotherredirect-rule/1234/5678`  | <span data-ttu-id="7c6cd-226">是</span><span class="sxs-lookup"><span data-stu-id="7c6cd-226">Yes</span></span>   |

<span data-ttu-id="7c6cd-227">重写规则 `^rewrite-rule/(\d+)/(\d+)` 只能与以 `rewrite-rule/` 开头的路径匹配。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-227">The rewrite rule, `^rewrite-rule/(\d+)/(\d+)`, only matches paths if they start with `rewrite-rule/`.</span></span> <span data-ttu-id="7c6cd-228">请注意以下重写规则和以上重定向规则之间的匹配差异。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-228">Notice the difference in matching between the rewrite rule below and the redirect rule above.</span></span>

| <span data-ttu-id="7c6cd-229">路径</span><span class="sxs-lookup"><span data-stu-id="7c6cd-229">Path</span></span>                              | <span data-ttu-id="7c6cd-230">匹配</span><span class="sxs-lookup"><span data-stu-id="7c6cd-230">Match</span></span> |
| --------------------------------- | :---: |
| `/rewrite-rule/1234/5678`         | <span data-ttu-id="7c6cd-231">是</span><span class="sxs-lookup"><span data-stu-id="7c6cd-231">Yes</span></span>   |
| `/my-cool-rewrite-rule/1234/5678` | <span data-ttu-id="7c6cd-232">否</span><span class="sxs-lookup"><span data-stu-id="7c6cd-232">No</span></span>    |
| `/anotherrewrite-rule/1234/5678`  | <span data-ttu-id="7c6cd-233">否</span><span class="sxs-lookup"><span data-stu-id="7c6cd-233">No</span></span>    |

<span data-ttu-id="7c6cd-234">在表达式的 `^rewrite-rule/` 部分之后，有两个捕获组 `(\d+)/(\d+)`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-234">Following the `^rewrite-rule/` portion of the expression, there are two capture groups, `(\d+)/(\d+)`.</span></span> <span data-ttu-id="7c6cd-235">`\d` 表示与数字匹配。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-235">The `\d` signifies *match a digit (number)*.</span></span> <span data-ttu-id="7c6cd-236">加号 (`+`) 表示与前面的一个或多个字符匹配。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-236">The plus sign (`+`) means *match one or more of the preceding character*.</span></span> <span data-ttu-id="7c6cd-237">因此，URL 必须包含数字加正斜杠加另一个数字的形式。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-237">Therefore, the URL must contain a number followed by a forward-slash followed by another number.</span></span> <span data-ttu-id="7c6cd-238">这些捕获组以 `$1` 和 `$2` 的形式注入重写 URL 中。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-238">These capture groups are injected into the rewritten URL as `$1` and `$2`.</span></span> <span data-ttu-id="7c6cd-239">重写规则替换字符串将捕获组放入查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-239">The rewrite rule replacement string places the captured groups into the querystring.</span></span> <span data-ttu-id="7c6cd-240">重写 `/rewrite-rule/1234/5678` 的请求路径，获取 `/rewritten?var1=1234&var2=5678` 处的资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-240">The requested path of `/rewrite-rule/1234/5678` is rewritten to obtain the resource at `/rewritten?var1=1234&var2=5678`.</span></span> <span data-ttu-id="7c6cd-241">如果原始请求中存在查询字符串，则重写 URL 时会保留此字符串。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-241">If a querystring is present on the original request, it's preserved when the URL is rewritten.</span></span>

<span data-ttu-id="7c6cd-242">无需往返服务器来获取资源。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-242">There's no roundtrip to the server to obtain the resource.</span></span> <span data-ttu-id="7c6cd-243">如果资源存在，系统会提取资源并以“200 (正常)”状态代码返回给客户端。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-243">If the resource exists, it's fetched and returned to the client with a 200 (OK) status code.</span></span> <span data-ttu-id="7c6cd-244">因为客户端不会被重定向，所以浏览器地址栏中的 URL 不会发生更改。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-244">Because the client isn't redirected, the URL in the browser address bar doesn't change.</span></span> <span data-ttu-id="7c6cd-245">对客户端来说，从未发生过 URL 重写操作。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-245">As far as the client is concerned, the URL rewrite operation never occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="7c6cd-246">尽可能使用 `skipRemainingRules: true`，因为匹配规则代价高昂且会减少应用响应时间。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-246">Use `skipRemainingRules: true` whenever possible, because matching rules is an expensive process and reduces app response time.</span></span> <span data-ttu-id="7c6cd-247">对于最快的应用响应：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-247">For the fastest app response:</span></span>
> * <span data-ttu-id="7c6cd-248">按照从最频繁匹配的规则到最不频繁匹配的规则排列重写规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-248">Order your rewrite rules from the most frequently matched rule to the least frequently matched rule.</span></span>
> * <span data-ttu-id="7c6cd-249">如果出现匹配项且无需处理任何其他规则，则跳过剩余规则的处理。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-249">Skip the processing of the remaining rules when a match occurs and no additional rule processing is required.</span></span>

### <a name="apache-modrewrite"></a><span data-ttu-id="7c6cd-250">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="7c6cd-250">Apache mod_rewrite</span></span>

<span data-ttu-id="7c6cd-251">使用 `AddApacheModRewrite` 应用 Apache mod_rewrite 规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-251">Apply Apache mod_rewrite rules with `AddApacheModRewrite`.</span></span> <span data-ttu-id="7c6cd-252">请确保将规则文件与应用一起部署。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-252">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="7c6cd-253">有关 mod_rewrite 规则的详细信息和示例，请参阅 [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/)。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-253">For more information and examples of mod_rewrite rules, see [Apache mod_rewrite](https://httpd.apache.org/docs/2.4/rewrite/).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="7c6cd-255">`StreamReader` 用于读取 ApacheModRewrite.txt 规则文件中的规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-255">A `StreamReader` is used to read the rules from the *ApacheModRewrite.txt* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=3-4,12)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-256">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-256">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="7c6cd-257">第一个参数采用 `IFileProvider`，后者可通过[依赖关系注入](dependency-injection.md)提供。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-257">The first parameter takes an `IFileProvider`, which is provided via [Dependency Injection](dependency-injection.md).</span></span> <span data-ttu-id="7c6cd-258">注入 `IHostingEnvironment` 以提供 `ContentRootFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-258">The `IHostingEnvironment` is injected to provide the `ContentRootFileProvider`.</span></span> <span data-ttu-id="7c6cd-259">第二个参数是规则文件（即示例应用中的 ApacheModRewrite.txt）的路径。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-259">The second parameter is the path to your rules file, which is *ApacheModRewrite.txt* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt");

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-260">示例应用将请求从 `/apache-mod-rules-redirect/(.\*)` 重定向到 `/redirected?id=$1`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-260">The sample app redirects requests from `/apache-mod-rules-redirect/(.\*)` to `/redirected?id=$1`.</span></span> <span data-ttu-id="7c6cd-261">响应状态代码为“302 (已找到)”。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-261">The response status code is 302 (Found).</span></span>

[!code[](url-rewriting/sample/ApacheModRewrite.txt)]

<span data-ttu-id="7c6cd-262">原始请求：`/apache-mod-rules-redirect/1234`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-262">Original Request: `/apache-mod-rules-redirect/1234`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_apache_mod_redirect.png)

##### <a name="supported-server-variables"></a><span data-ttu-id="7c6cd-264">受支持的服务器变量</span><span class="sxs-lookup"><span data-stu-id="7c6cd-264">Supported server variables</span></span>

<span data-ttu-id="7c6cd-265">中间件支持下列 Apache mod_rewrite 服务器变量：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-265">The middleware supports the following Apache mod_rewrite server variables:</span></span>

* <span data-ttu-id="7c6cd-266">CONN_REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-266">CONN_REMOTE_ADDR</span></span>
* <span data-ttu-id="7c6cd-267">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-267">HTTP_ACCEPT</span></span>
* <span data-ttu-id="7c6cd-268">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="7c6cd-268">HTTP_CONNECTION</span></span>
* <span data-ttu-id="7c6cd-269">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="7c6cd-269">HTTP_COOKIE</span></span>
* <span data-ttu-id="7c6cd-270">HTTP_FORWARDED</span><span class="sxs-lookup"><span data-stu-id="7c6cd-270">HTTP_FORWARDED</span></span>
* <span data-ttu-id="7c6cd-271">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="7c6cd-271">HTTP_HOST</span></span>
* <span data-ttu-id="7c6cd-272">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="7c6cd-272">HTTP_REFERER</span></span>
* <span data-ttu-id="7c6cd-273">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-273">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="7c6cd-274">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7c6cd-274">HTTPS</span></span>
* <span data-ttu-id="7c6cd-275">IPV6</span><span class="sxs-lookup"><span data-stu-id="7c6cd-275">IPV6</span></span>
* <span data-ttu-id="7c6cd-276">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="7c6cd-276">QUERY_STRING</span></span>
* <span data-ttu-id="7c6cd-277">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-277">REMOTE_ADDR</span></span>
* <span data-ttu-id="7c6cd-278">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-278">REMOTE_PORT</span></span>
* <span data-ttu-id="7c6cd-279">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="7c6cd-279">REQUEST_FILENAME</span></span>
* <span data-ttu-id="7c6cd-280">REQUEST_METHOD</span><span class="sxs-lookup"><span data-stu-id="7c6cd-280">REQUEST_METHOD</span></span>
* <span data-ttu-id="7c6cd-281">REQUEST_SCHEME</span><span class="sxs-lookup"><span data-stu-id="7c6cd-281">REQUEST_SCHEME</span></span>
* <span data-ttu-id="7c6cd-282">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="7c6cd-282">REQUEST_URI</span></span>
* <span data-ttu-id="7c6cd-283">SCRIPT_FILENAME</span><span class="sxs-lookup"><span data-stu-id="7c6cd-283">SCRIPT_FILENAME</span></span>
* <span data-ttu-id="7c6cd-284">SERVER_ADDR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-284">SERVER_ADDR</span></span>
* <span data-ttu-id="7c6cd-285">SERVER_PORT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-285">SERVER_PORT</span></span>
* <span data-ttu-id="7c6cd-286">SERVER_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="7c6cd-286">SERVER_PROTOCOL</span></span>
* <span data-ttu-id="7c6cd-287">TIME</span><span class="sxs-lookup"><span data-stu-id="7c6cd-287">TIME</span></span>
* <span data-ttu-id="7c6cd-288">TIME_DAY</span><span class="sxs-lookup"><span data-stu-id="7c6cd-288">TIME_DAY</span></span>
* <span data-ttu-id="7c6cd-289">TIME_HOUR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-289">TIME_HOUR</span></span>
* <span data-ttu-id="7c6cd-290">TIME_MIN</span><span class="sxs-lookup"><span data-stu-id="7c6cd-290">TIME_MIN</span></span>
* <span data-ttu-id="7c6cd-291">TIME_MON</span><span class="sxs-lookup"><span data-stu-id="7c6cd-291">TIME_MON</span></span>
* <span data-ttu-id="7c6cd-292">TIME_SEC</span><span class="sxs-lookup"><span data-stu-id="7c6cd-292">TIME_SEC</span></span>
* <span data-ttu-id="7c6cd-293">TIME_WDAY</span><span class="sxs-lookup"><span data-stu-id="7c6cd-293">TIME_WDAY</span></span>
* <span data-ttu-id="7c6cd-294">TIME_YEAR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-294">TIME_YEAR</span></span>

### <a name="iis-url-rewrite-module-rules"></a><span data-ttu-id="7c6cd-295">IIS URL 重写模块规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-295">IIS URL Rewrite Module rules</span></span>

<span data-ttu-id="7c6cd-296">要使用适用于 IIS URL 重写模块的规则，请使用 `AddIISUrlRewrite`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-296">To use rules that apply to the IIS URL Rewrite Module, use `AddIISUrlRewrite`.</span></span> <span data-ttu-id="7c6cd-297">请确保将规则文件与应用一起部署。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-297">Make sure that the rules file is deployed with the app.</span></span> <span data-ttu-id="7c6cd-298">当 web.config 文件在 Windows Server IIS 上运行时，请勿指示中间件使用该文件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-298">Don't direct the middleware to use your *web.config* file when running on Windows Server IIS.</span></span> <span data-ttu-id="7c6cd-299">使用 IIS 时，应将这些规则存储在 web.config 之外，避免与 IIS 重写模块发生冲突。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-299">With IIS, these rules should be stored outside of your *web.config* to avoid conflicts with the IIS Rewrite module.</span></span> <span data-ttu-id="7c6cd-300">有关 IIS URL 重写模块规则的详细信息和示例，请参阅 [Using Url Rewrite Module 2.0](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)（使用 URL 重写模块 2.0）和 [URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)（URL 重写模块配置引用）。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-300">For more information and examples of IIS URL Rewrite Module rules, see [Using Url Rewrite Module 2.0](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20) and [URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-301">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-301">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="7c6cd-302">`StreamReader` 用于读取 IISUrlRewrite.xml 规则文件中的规则。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-302">A `StreamReader` is used to read the rules from the *IISUrlRewrite.xml* rules file.</span></span>

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=5-6,13)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-303">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-303">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="7c6cd-304">第一个参数采用 `IFileProvider`，而第二个参数是 XML 规则文件（即示例应用中的 IISUrlRewrite.xml）的路径。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-304">The first parameter takes an `IFileProvider`, while the second parameter is the path to your XML rules file, which is *IISUrlRewrite.xml* in the sample app.</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    var options = new RewriteOptions()
        .AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml");

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-305">示例应用将请求从 `/iis-rules-rewrite/(.*)` 重写为 `/rewritten?id=$1`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-305">The sample app rewrites requests from `/iis-rules-rewrite/(.*)` to `/rewritten?id=$1`.</span></span> <span data-ttu-id="7c6cd-306">以“200 (正常)”状态代码作为响应发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-306">The response is sent to the client with a 200 (OK) status code.</span></span>

[!code-xml[](url-rewriting/sample/IISUrlRewrite.xml)]

<span data-ttu-id="7c6cd-307">原始请求：`/iis-rules-rewrite/1234`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-307">Original Request: `/iis-rules-rewrite/1234`</span></span>

![开发人员工具正跟踪请求和响应的浏览器窗口](url-rewriting/_static/add_iis_url_rewrite.png)

<span data-ttu-id="7c6cd-309">如果有配置了服务器级别规则（可对应用产生不利影响）的活动 IIS 重写模块，则可禁用应用的 IIS 重写模块。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-309">If you have an active IIS Rewrite Module with server-level rules configured that would impact your app in undesirable ways, you can disable the IIS Rewrite Module for an app.</span></span> <span data-ttu-id="7c6cd-310">有关详细信息，请参阅[禁用 IIS 模块](xref:host-and-deploy/iis/modules#disabling-iis-modules)。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-310">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

#### <a name="unsupported-features"></a><span data-ttu-id="7c6cd-311">不支持的功能</span><span class="sxs-lookup"><span data-stu-id="7c6cd-311">Unsupported features</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-312">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-312">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="7c6cd-313">与 ASP.NET Core 2.x 一同发布的中间件不支持以下 IIS URL 重写模块功能：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-313">The middleware released with ASP.NET Core 2.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="7c6cd-314">出站规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-314">Outbound Rules</span></span>
* <span data-ttu-id="7c6cd-315">自定义服务器变量</span><span class="sxs-lookup"><span data-stu-id="7c6cd-315">Custom Server Variables</span></span>
* <span data-ttu-id="7c6cd-316">通配符</span><span class="sxs-lookup"><span data-stu-id="7c6cd-316">Wildcards</span></span>
* <span data-ttu-id="7c6cd-317">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="7c6cd-317">LogRewrittenUrl</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-318">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-318">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="7c6cd-319">与 ASP.NET Core 1.x 一同发布的中间件不支持以下 IIS URL 重写模块功能：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-319">The middleware released with ASP.NET Core 1.x doesn't support the following IIS URL Rewrite Module features:</span></span>

* <span data-ttu-id="7c6cd-320">全局规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-320">Global Rules</span></span>
* <span data-ttu-id="7c6cd-321">出站规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-321">Outbound Rules</span></span>
* <span data-ttu-id="7c6cd-322">重写映射</span><span class="sxs-lookup"><span data-stu-id="7c6cd-322">Rewrite Maps</span></span>
* <span data-ttu-id="7c6cd-323">CustomResponse 操作</span><span class="sxs-lookup"><span data-stu-id="7c6cd-323">CustomResponse Action</span></span>
* <span data-ttu-id="7c6cd-324">自定义服务器变量</span><span class="sxs-lookup"><span data-stu-id="7c6cd-324">Custom Server Variables</span></span>
* <span data-ttu-id="7c6cd-325">通配符</span><span class="sxs-lookup"><span data-stu-id="7c6cd-325">Wildcards</span></span>
* <span data-ttu-id="7c6cd-326">Action:CustomResponse</span><span class="sxs-lookup"><span data-stu-id="7c6cd-326">Action:CustomResponse</span></span>
* <span data-ttu-id="7c6cd-327">LogRewrittenUrl</span><span class="sxs-lookup"><span data-stu-id="7c6cd-327">LogRewrittenUrl</span></span>

---

#### <a name="supported-server-variables"></a><span data-ttu-id="7c6cd-328">受支持的服务器变量</span><span class="sxs-lookup"><span data-stu-id="7c6cd-328">Supported server variables</span></span>

<span data-ttu-id="7c6cd-329">中间件支持下列 IIS URL 重写模块服务器变量：</span><span class="sxs-lookup"><span data-stu-id="7c6cd-329">The middleware supports the following IIS URL Rewrite Module server variables:</span></span>

* <span data-ttu-id="7c6cd-330">CONTENT_LENGTH</span><span class="sxs-lookup"><span data-stu-id="7c6cd-330">CONTENT_LENGTH</span></span>
* <span data-ttu-id="7c6cd-331">CONTENT_TYPE</span><span class="sxs-lookup"><span data-stu-id="7c6cd-331">CONTENT_TYPE</span></span>
* <span data-ttu-id="7c6cd-332">HTTP_ACCEPT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-332">HTTP_ACCEPT</span></span>
* <span data-ttu-id="7c6cd-333">HTTP_CONNECTION</span><span class="sxs-lookup"><span data-stu-id="7c6cd-333">HTTP_CONNECTION</span></span>
* <span data-ttu-id="7c6cd-334">HTTP_COOKIE</span><span class="sxs-lookup"><span data-stu-id="7c6cd-334">HTTP_COOKIE</span></span>
* <span data-ttu-id="7c6cd-335">HTTP_HOST</span><span class="sxs-lookup"><span data-stu-id="7c6cd-335">HTTP_HOST</span></span>
* <span data-ttu-id="7c6cd-336">HTTP_REFERER</span><span class="sxs-lookup"><span data-stu-id="7c6cd-336">HTTP_REFERER</span></span>
* <span data-ttu-id="7c6cd-337">HTTP_URL</span><span class="sxs-lookup"><span data-stu-id="7c6cd-337">HTTP_URL</span></span>
* <span data-ttu-id="7c6cd-338">HTTP_USER_AGENT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-338">HTTP_USER_AGENT</span></span>
* <span data-ttu-id="7c6cd-339">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7c6cd-339">HTTPS</span></span>
* <span data-ttu-id="7c6cd-340">LOCAL_ADDR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-340">LOCAL_ADDR</span></span>
* <span data-ttu-id="7c6cd-341">QUERY_STRING</span><span class="sxs-lookup"><span data-stu-id="7c6cd-341">QUERY_STRING</span></span>
* <span data-ttu-id="7c6cd-342">REMOTE_ADDR</span><span class="sxs-lookup"><span data-stu-id="7c6cd-342">REMOTE_ADDR</span></span>
* <span data-ttu-id="7c6cd-343">REMOTE_PORT</span><span class="sxs-lookup"><span data-stu-id="7c6cd-343">REMOTE_PORT</span></span>
* <span data-ttu-id="7c6cd-344">REQUEST_FILENAME</span><span class="sxs-lookup"><span data-stu-id="7c6cd-344">REQUEST_FILENAME</span></span>
* <span data-ttu-id="7c6cd-345">REQUEST_URI</span><span class="sxs-lookup"><span data-stu-id="7c6cd-345">REQUEST_URI</span></span>

> [!NOTE]
> <span data-ttu-id="7c6cd-346">也可通过 `PhysicalFileProvider` 获取 `IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-346">You can also obtain an `IFileProvider` via a `PhysicalFileProvider`.</span></span> <span data-ttu-id="7c6cd-347">这种方法可为重写规则文件的位置提供更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-347">This approach may provide greater flexibility for the location of your rewrite rules files.</span></span> <span data-ttu-id="7c6cd-348">请确保将重写规则文件部署到所提供路径的服务器中。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-348">Make sure that your rewrite rules files are deployed to the server at the path you provide.</span></span>
> ```csharp
> PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
> ```

### <a name="method-based-rule"></a><span data-ttu-id="7c6cd-349">基于方法的规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-349">Method-based rule</span></span>

<span data-ttu-id="7c6cd-350">使用 `Add(Action<RewriteContext> applyRule)` 在方法中实现自己的规则逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-350">Use `Add(Action<RewriteContext> applyRule)` to implement your own rule logic in a method.</span></span> <span data-ttu-id="7c6cd-351">为了在方法中使用 `HttpContext`，`RewriteContext` 会将其公开。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-351">The `RewriteContext` exposes the `HttpContext` for use in your method.</span></span> <span data-ttu-id="7c6cd-352">`context.Result` 决定如何处理其他管道进程。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-352">The `context.Result` determines how additional pipeline processing is handled.</span></span>

| <span data-ttu-id="7c6cd-353">context.Result</span><span class="sxs-lookup"><span data-stu-id="7c6cd-353">context.Result</span></span>                       | <span data-ttu-id="7c6cd-354">操作</span><span class="sxs-lookup"><span data-stu-id="7c6cd-354">Action</span></span>                                                          |
| ------------------------------------ | --------------------------------------------------------------- |
| <span data-ttu-id="7c6cd-355">`RuleResult.ContinueRules`（默认值）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-355">`RuleResult.ContinueRules` (default)</span></span> | <span data-ttu-id="7c6cd-356">继续应用规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-356">Continue applying rules</span></span>                                         |
| `RuleResult.EndResponse`             | <span data-ttu-id="7c6cd-357">停止应用规则并发送响应</span><span class="sxs-lookup"><span data-stu-id="7c6cd-357">Stop applying rules and send the response</span></span>                       |
| `RuleResult.SkipRemainingRules`      | <span data-ttu-id="7c6cd-358">停止应用规则并将上下文发送给下一个中间件</span><span class="sxs-lookup"><span data-stu-id="7c6cd-358">Stop applying rules and send the context to the next middleware</span></span> |

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-359">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-359">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=14)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-360">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-360">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(RedirectXMLRequests);

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-361">示例应用演示了如何对以 .xml 结尾的路径的请求进行重定向。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-361">The sample app demonstrates a method that redirects requests for paths that end with *.xml*.</span></span> <span data-ttu-id="7c6cd-362">如果为 `/file.xml` 发出请求，则它将重定向到 `/xmlfiles/file.xml`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-362">If you make a request for `/file.xml`, it's redirected to `/xmlfiles/file.xml`.</span></span> <span data-ttu-id="7c6cd-363">状态代码设置为“301 (永久移动)”。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-363">The status code is set to 301 (Moved Permanently).</span></span> <span data-ttu-id="7c6cd-364">对于重定向，必须明确设置响应的状态代码；否则会返回 “200 (正常)”状态代码，且在客户端上不会进行重定向。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-364">For a redirect, you must explicitly set the status code of the response; otherwise, a 200 (OK) status code is returned and the redirect won't occur on the client.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet1)]

<span data-ttu-id="7c6cd-365">原始请求：`/file.xml`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-365">Original Request: `/file.xml`</span></span>

![开发人员工具正跟踪 file.xml 的请求和响应的浏览器窗口](url-rewriting/_static/add_redirect_xml_requests.png)

### <a name="irule-based-rule"></a><span data-ttu-id="7c6cd-367">基于 IRule 的规则</span><span class="sxs-lookup"><span data-stu-id="7c6cd-367">IRule-based rule</span></span>

<span data-ttu-id="7c6cd-368">使用 `Add(IRule)` 在派生自 `IRule` 的类中实现自己的规则逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-368">Use `Add(IRule)` to implement your own rule logic in a class that derives from `IRule`.</span></span> <span data-ttu-id="7c6cd-369">通过 `IRule` 为使用基于方法的规则方式提供更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-369">Using an `IRule` provides greater flexibility over using the method-based rule approach.</span></span> <span data-ttu-id="7c6cd-370">派生类可能包含构造函数，你可在其中传入 `ApplyRule` 方法的参数。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-370">Your derived class may include a constructor, where you can pass in parameters for the `ApplyRule` method.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="7c6cd-371">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-371">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](url-rewriting/sample/Startup.cs?name=snippet1&highlight=15-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="7c6cd-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="7c6cd-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
public void Configure(IApplicationBuilder app)
{
    var options = new RewriteOptions()
        .Add(new RedirectImageRequests(".png", "/png-images"))
        .Add(new RedirectImageRequests(".jpg", "/jpg-images"));

    app.UseRewriter(options);
}
```

---

<span data-ttu-id="7c6cd-373">检查示例应用中 `extension` 和 `newPath` 的参数值是否符合多个条件。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-373">The values of the parameters in the sample app for the `extension` and the `newPath` are checked to meet several conditions.</span></span> <span data-ttu-id="7c6cd-374">`extension` 须包含一个值，并且该值必须是 .png、.jpg 或 .gif。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-374">The `extension` must contain a value, and the value must be *.png*, *.jpg*, or *.gif*.</span></span> <span data-ttu-id="7c6cd-375">如果 `newPath` 无效，则会引发 `ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-375">If the `newPath` isn't valid, an `ArgumentException` is thrown.</span></span> <span data-ttu-id="7c6cd-376">如果为 image.png 发出请求，则它将重定向到 `/png-images/image.png`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-376">If you make a request for *image.png*, it's redirected to `/png-images/image.png`.</span></span> <span data-ttu-id="7c6cd-377">如果为 image.jpg 发出请求，则它将重定向到 `/jpg-images/image.jpg`。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-377">If you make a request for *image.jpg*, it's redirected to `/jpg-images/image.jpg`.</span></span> <span data-ttu-id="7c6cd-378">状态代码设置为“301 (永久移动)”，`context.Result` 设置为停止处理规则并发送响应。</span><span class="sxs-lookup"><span data-stu-id="7c6cd-378">The status code is set to 301 (Moved Permanently), and the `context.Result` is set to stop processing rules and send the response.</span></span>

[!code-csharp[](url-rewriting/sample/RewriteRules.cs?name=snippet2)]

<span data-ttu-id="7c6cd-379">原始请求：`/image.png`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-379">Original Request: `/image.png`</span></span>

![开发人员工具正跟踪 image.png 的请求和响应的浏览器窗口](url-rewriting/_static/add_redirect_png_requests.png)

<span data-ttu-id="7c6cd-381">原始请求：`/image.jpg`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-381">Original Request: `/image.jpg`</span></span>

![开发人员工具正跟踪 image.jpg 的请求和响应的浏览器窗口](url-rewriting/_static/add_redirect_jpg_requests.png)

## <a name="regex-examples"></a><span data-ttu-id="7c6cd-383">正则表达式示例</span><span class="sxs-lookup"><span data-stu-id="7c6cd-383">Regex examples</span></span>

| <span data-ttu-id="7c6cd-384">目标</span><span class="sxs-lookup"><span data-stu-id="7c6cd-384">Goal</span></span> | <span data-ttu-id="7c6cd-385">正则表达式字符串和</span><span class="sxs-lookup"><span data-stu-id="7c6cd-385">Regex String &</span></span><br><span data-ttu-id="7c6cd-386">匹配示例</span><span class="sxs-lookup"><span data-stu-id="7c6cd-386">Match Example</span></span> | <span data-ttu-id="7c6cd-387">替换字符串和</span><span class="sxs-lookup"><span data-stu-id="7c6cd-387">Replacement String &</span></span><br><span data-ttu-id="7c6cd-388">输出示例</span><span class="sxs-lookup"><span data-stu-id="7c6cd-388">Output Example</span></span> |
| ---- | :-----------------------------: | :------------------------------------: |
| <span data-ttu-id="7c6cd-389">将路径重写为查询字符串</span><span class="sxs-lookup"><span data-stu-id="7c6cd-389">Rewrite path into querystring</span></span> | `^path/(.*)/(.*)`<br>`/path/abc/123` | `path?var1=$1&var2=$2`<br>`/path?var1=abc&var2=123` |
| <span data-ttu-id="7c6cd-390">去掉尾部反斜杠</span><span class="sxs-lookup"><span data-stu-id="7c6cd-390">Strip trailing slash</span></span> | `(.*)/$`<br>`/path/` | `$1`<br>`/path` |
| <span data-ttu-id="7c6cd-391">强制添加尾部反斜杠</span><span class="sxs-lookup"><span data-stu-id="7c6cd-391">Enforce trailing slash</span></span> | `(.*[^/])$`<br>`/path` | `$1/`<br>`/path/` |
| <span data-ttu-id="7c6cd-392">避免重写特定请求</span><span class="sxs-lookup"><span data-stu-id="7c6cd-392">Avoid rewriting specific requests</span></span> | <span data-ttu-id="7c6cd-393">`^(.*)(?<!\.axd)$` 或 `^(?!.*\.axd$)(.*)$`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-393">`^(.*)(?<!\.axd)$` or `^(?!.*\.axd$)(.*)$`</span></span><br><span data-ttu-id="7c6cd-394">正确：`/resource.htm`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-394">Yes: `/resource.htm`</span></span><br><span data-ttu-id="7c6cd-395">错误：`/resource.axd`</span><span class="sxs-lookup"><span data-stu-id="7c6cd-395">No: `/resource.axd`</span></span> | `rewritten/$1`<br>`/rewritten/resource.htm`<br>`/resource.axd` |
| <span data-ttu-id="7c6cd-396">重新排列 URL 段</span><span class="sxs-lookup"><span data-stu-id="7c6cd-396">Rearrange URL segments</span></span> | `path/(.*)/(.*)/(.*)`<br>`path/1/2/3` | `path/$3/$2/$1`<br>`path/3/2/1` |
| <span data-ttu-id="7c6cd-397">替换 URL 段</span><span class="sxs-lookup"><span data-stu-id="7c6cd-397">Replace a URL segment</span></span> | `^(.*)/segment2/(.*)`<br>`/segment1/segment2/segment3` | `$1/replaced/$2`<br>`/segment1/replaced/segment3` |

## <a name="additional-resources"></a><span data-ttu-id="7c6cd-398">其他资源</span><span class="sxs-lookup"><span data-stu-id="7c6cd-398">Additional resources</span></span>

* [<span data-ttu-id="7c6cd-399">应用程序启动</span><span class="sxs-lookup"><span data-stu-id="7c6cd-399">Application Startup</span></span>](startup.md)
* [<span data-ttu-id="7c6cd-400">中间件</span><span class="sxs-lookup"><span data-stu-id="7c6cd-400">Middleware</span></span>](xref:fundamentals/middleware/index)
* [<span data-ttu-id="7c6cd-401">.NET 中的正则表达式</span><span class="sxs-lookup"><span data-stu-id="7c6cd-401">Regular expressions in .NET</span></span>](/dotnet/articles/standard/base-types/regular-expressions)
* [<span data-ttu-id="7c6cd-402">正则表达式语言 - 快速参考</span><span class="sxs-lookup"><span data-stu-id="7c6cd-402">Regular expression language - quick reference</span></span>](/dotnet/articles/standard/base-types/quick-ref)
* [<span data-ttu-id="7c6cd-403">Apache mod_rewrite</span><span class="sxs-lookup"><span data-stu-id="7c6cd-403">Apache mod_rewrite</span></span>](https://httpd.apache.org/docs/2.4/rewrite/)
* [<span data-ttu-id="7c6cd-404">使用 URL 重写模块 2.0（适用于 IIS）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-404">Using Url Rewrite Module 2.0 (for IIS)</span></span>](/iis/extensions/url-rewrite-module/using-url-rewrite-module-20)
* <span data-ttu-id="7c6cd-405">[URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)（URL 重写模块配置引用）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-405">[URL Rewrite Module Configuration Reference](/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference)</span></span>
* [<span data-ttu-id="7c6cd-406">IIS URL 重写模块论坛</span><span class="sxs-lookup"><span data-stu-id="7c6cd-406">IIS URL Rewrite Module Forum</span></span>](https://forums.iis.net/1152.aspx)
* <span data-ttu-id="7c6cd-407">[Keep a simple URL structure](https://support.google.com/webmasters/answer/76329?hl=en)（保持简单的 URL 结构）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-407">[Keep a simple URL structure](https://support.google.com/webmasters/answer/76329?hl=en)</span></span>
* <span data-ttu-id="7c6cd-408">[10 URL Rewriting Tips and Tricks](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)（10 个 URL 重写提示和技巧）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-408">[10 URL Rewriting Tips and Tricks](http://ruslany.net/2009/04/10-url-rewriting-tips-and-tricks/)</span></span>
* <span data-ttu-id="7c6cd-409">[To slash or not to slash](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)（用斜杠或不用斜杠）</span><span class="sxs-lookup"><span data-stu-id="7c6cd-409">[To slash or not to slash](https://webmasters.googleblog.com/2010/04/to-slash-or-not-to-slash.html)</span></span>
