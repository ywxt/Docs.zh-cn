---
title: 强制实施 HTTPS 在 ASP.NET Core
author: rick-anderson
description: 演示如何要求在 ASP.NET Core HTTPS/TLS web 应用。
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: a4ab91ef23a798c919a23a44f5a050bd3c09d56a
ms.sourcegitcommit: d99a8554c91f626cf5e466911cf504dcbff0e02e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39356683"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="4e198-103">强制实施 HTTPS 在 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4e198-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="4e198-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4e198-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4e198-105">本文档演示如何：</span><span class="sxs-lookup"><span data-stu-id="4e198-105">This document shows how to:</span></span>

* <span data-ttu-id="4e198-106">要求所有请求使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="4e198-107">将所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="4e198-108">不要**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。</span><span class="sxs-lookup"><span data-stu-id="4e198-108">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="4e198-109">`RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。</span><span class="sxs-lookup"><span data-stu-id="4e198-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="4e198-110">API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。</span><span class="sxs-lookup"><span data-stu-id="4e198-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="4e198-111">此类客户端可能会通过 HTTP 发送的信息。</span><span class="sxs-lookup"><span data-stu-id="4e198-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="4e198-112">Web Api 应具有下列任一：</span><span class="sxs-lookup"><span data-stu-id="4e198-112">Web APIs should either:</span></span>
>
> * <span data-ttu-id="4e198-113">不侦听 HTTP。</span><span class="sxs-lookup"><span data-stu-id="4e198-113">Not listen on HTTP.</span></span>
> * <span data-ttu-id="4e198-114">关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="4e198-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="4e198-115">要求使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="4e198-115">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="4e198-116">我们建议所有 ASP.NET Core web 应用都调用 HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 将所有 HTTP 请求重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-116">We recommend all ASP.NET Core web apps call HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="4e198-117">下面的代码调用`UseHttpsRedirection`在`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="4e198-117">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

<span data-ttu-id="4e198-118">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="4e198-118">The preceding highlighted code:</span></span>

* <span data-ttu-id="4e198-119">使用默认[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`)。</span><span class="sxs-lookup"><span data-stu-id="4e198-119">Uses the default [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span></span> <span data-ttu-id="4e198-120">生产应用应调用[UseHsts](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="4e198-120">Production apps should call [UseHsts](#hsts).</span></span>
* <span data-ttu-id="4e198-121">使用默认[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (443)。</span><span class="sxs-lookup"><span data-stu-id="4e198-121">Uses the default [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (443).</span></span>

<span data-ttu-id="4e198-122">下面的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：</span><span class="sxs-lookup"><span data-stu-id="4e198-122">The following code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

<span data-ttu-id="4e198-123">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="4e198-123">The preceding highlighted code:</span></span>

* <span data-ttu-id="4e198-124">集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到`Status307TemporaryRedirect`，这是默认值。</span><span class="sxs-lookup"><span data-stu-id="4e198-124">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to `Status307TemporaryRedirect`, which is the default value.</span></span> <span data-ttu-id="4e198-125">生产应用应调用[UseHsts](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="4e198-125">Production apps should call [UseHsts](#hsts).</span></span>
* <span data-ttu-id="4e198-126">设置 HTTPS 端口为 5001。</span><span class="sxs-lookup"><span data-stu-id="4e198-126">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="4e198-127">默认值为 443。</span><span class="sxs-lookup"><span data-stu-id="4e198-127">The default value is 443.</span></span>

<span data-ttu-id="4e198-128">以下机制自动设置端口：</span><span class="sxs-lookup"><span data-stu-id="4e198-128">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="4e198-129">中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)时满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="4e198-129">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>
  - <span data-ttu-id="4e198-130">Kestrel 或 HTTP.sys 直接与 HTTPS 终结点一起使用 （也适用于使用 Visual Studio Code 的调试器中运行应用程序）。</span><span class="sxs-lookup"><span data-stu-id="4e198-130">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
  - <span data-ttu-id="4e198-131">仅**一个 HTTPS 端口**应用使用。</span><span class="sxs-lookup"><span data-stu-id="4e198-131">Only **one HTTPS port** is used by the app.</span></span>
* <span data-ttu-id="4e198-132">使用 visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4e198-132">Visual Studio is used:</span></span>
  - <span data-ttu-id="4e198-133">IIS Express 已启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-133">IIS Express has HTTPS enabled.</span></span>
  - <span data-ttu-id="4e198-134">*launchSettings.json*设置`sslPort`IIS express。</span><span class="sxs-lookup"><span data-stu-id="4e198-134">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="4e198-135">当应用程序运行时在反向代理 （例如，IIS，IIS Express），后面`IServerAddressesFeature`不可用。</span><span class="sxs-lookup"><span data-stu-id="4e198-135">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="4e198-136">必须手动配置端口。</span><span class="sxs-lookup"><span data-stu-id="4e198-136">The port must be manually configured.</span></span> <span data-ttu-id="4e198-137">如果端口未设置，请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="4e198-137">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="4e198-138">可以通过设置配置端口[https_port Web 主机配置设置](xref:fundamentals/host/web-host#https-port):</span><span class="sxs-lookup"><span data-stu-id="4e198-138">The port can be configured by setting the [https_port Web Host configuration setting](xref:fundamentals/host/web-host#https-port):</span></span>

<span data-ttu-id="4e198-139">**键**: https_port**类型**:*字符串*
**默认**： 未设置默认值。</span><span class="sxs-lookup"><span data-stu-id="4e198-139">**Key**: https_port **Type**: *string*
**Default**: A default value isn't set.</span></span>
<span data-ttu-id="4e198-140">**使用设置**: `UseSetting` 
**环境变量**: `<PREFIX_>HTTPS_PORT` (该前缀是`ASPNETCORE_`使用 Web 主机时。)</span><span class="sxs-lookup"><span data-stu-id="4e198-140">**Set using**: `UseSetting`
**Environment variable**: `<PREFIX_>HTTPS_PORT` (The prefix is `ASPNETCORE_` when using the Web Host.)</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> <span data-ttu-id="4e198-141">可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。</span><span class="sxs-lookup"><span data-stu-id="4e198-141">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="4e198-142">环境变量配置的服务器，，然后在中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。</span><span class="sxs-lookup"><span data-stu-id="4e198-142">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="4e198-143">如果没有端口设置：</span><span class="sxs-lookup"><span data-stu-id="4e198-143">If no port is set:</span></span>

* <span data-ttu-id="4e198-144">请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="4e198-144">Requests aren't redirected.</span></span>
* <span data-ttu-id="4e198-145">中间件记录警告。</span><span class="sxs-lookup"><span data-stu-id="4e198-145">The middleware logs a warning.</span></span>

> [!NOTE]
> <span data-ttu-id="4e198-146">使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。</span><span class="sxs-lookup"><span data-stu-id="4e198-146">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="4e198-147">`AddRedirectToHttps` 此外可以设置的状态代码和端口时执行重定向。</span><span class="sxs-lookup"><span data-stu-id="4e198-147">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="4e198-148">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="4e198-148">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="4e198-149">当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。</span><span class="sxs-lookup"><span data-stu-id="4e198-149">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="4e198-150">[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于要求 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-150">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="4e198-151">`[RequireHttpsAttribute]` 可以修饰控制器或方法，也可以全局应用。</span><span class="sxs-lookup"><span data-stu-id="4e198-151">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="4e198-152">若要全局应用该属性，将以下代码添加到`ConfigureServices`在`Startup`:</span><span class="sxs-lookup"><span data-stu-id="4e198-152">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="4e198-153">前面突出显示的代码要求所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="4e198-153">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="4e198-154">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="4e198-154">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="4e198-155">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="4e198-155">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="4e198-156">中间件还允许应用执行重定向时设置的状态代码或状态代码和端口。</span><span class="sxs-lookup"><span data-stu-id="4e198-156">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="4e198-157">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="4e198-157">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="4e198-158">将应用`[RequireHttps]`属性设置为所有控制器/Razor 页面不会被视为与需要 HTTPS 全局一样安全。</span><span class="sxs-lookup"><span data-stu-id="4e198-158">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="4e198-159">不能保证`[RequireHttps]`时添加新的控制器和 Razor 页面应用属性。</span><span class="sxs-lookup"><span data-stu-id="4e198-159">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="4e198-160">HTTP 严格传输安全协议 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="4e198-160">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="4e198-161">每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全性 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是通过使用特殊响应标头的 web 应用程序指定选择的安全增强功能。</span><span class="sxs-lookup"><span data-stu-id="4e198-161">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that is specified by a web application through the use of a special response header.</span></span> <span data-ttu-id="4e198-162">支持的浏览器收到此标头后该浏览器将阻止通过 HTTP 发送到指定的域的任何通信，并改为将通过 HTTPS 发送的所有通信。</span><span class="sxs-lookup"><span data-stu-id="4e198-162">Once a supported browser receives this header that browser will prevent any communications from being sent over HTTP to the specified domain and will instead send all communications over HTTPS.</span></span> <span data-ttu-id="4e198-163">它还可以防止 HTTPS 点击提示在浏览器上。</span><span class="sxs-lookup"><span data-stu-id="4e198-163">It also prevents HTTPS click through prompts on browsers.</span></span>

<span data-ttu-id="4e198-164">ASP.NET Core 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="4e198-164">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="4e198-165">下面的代码调用`UseHsts`时应用不在[开发模式](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="4e198-165">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

<span data-ttu-id="4e198-166">`UseHsts` 不建议在开发过程中由于 HSTS 标头是高度可缓存的浏览器。</span><span class="sxs-lookup"><span data-stu-id="4e198-166">`UseHsts` isn't recommended in development because the HSTS header is highly cacheable by browsers.</span></span> <span data-ttu-id="4e198-167">默认情况下，`UseHsts`排除本地环回地址。</span><span class="sxs-lookup"><span data-stu-id="4e198-167">By default, `UseHsts` excludes the local loopback address.</span></span>

<span data-ttu-id="4e198-168">下面的代码：</span><span class="sxs-lookup"><span data-stu-id="4e198-168">The following code:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* <span data-ttu-id="4e198-169">设置预加载严格传输安全性标头的参数。</span><span class="sxs-lookup"><span data-stu-id="4e198-169">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="4e198-170">预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但要预加载 HSTS 站点上执行全新安装的 web 浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="4e198-170">Preload is not part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="4e198-171">有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。</span><span class="sxs-lookup"><span data-stu-id="4e198-171">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="4e198-172">使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，这将 HSTS 策略应用到主机的子域。</span><span class="sxs-lookup"><span data-stu-id="4e198-172">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="4e198-173">显式将到严格传输安全性标头的最大期限参数设置为 60 天。</span><span class="sxs-lookup"><span data-stu-id="4e198-173">Explicitly sets the max-age parameter of the Strict-Transport-Security header to to 60 days.</span></span> <span data-ttu-id="4e198-174">如果未设置，默认值为 30 天。</span><span class="sxs-lookup"><span data-stu-id="4e198-174">If not set, defaults to 30 days.</span></span> <span data-ttu-id="4e198-175">请参阅[最大期限指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="4e198-175">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="4e198-176">添加`example.com`到主机以排除列表。</span><span class="sxs-lookup"><span data-stu-id="4e198-176">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="4e198-177">`UseHsts` 不包括以下环回主机：</span><span class="sxs-lookup"><span data-stu-id="4e198-177">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="4e198-178">`localhost` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="4e198-178">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="4e198-179">`127.0.0.1` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="4e198-179">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="4e198-180">`[::1]` : IPv6 环回地址。</span><span class="sxs-lookup"><span data-stu-id="4e198-180">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="4e198-181">前面的示例演示如何添加其他主机。</span><span class="sxs-lookup"><span data-stu-id="4e198-181">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="4e198-182">选择退出的 HTTPS 在项目创建</span><span class="sxs-lookup"><span data-stu-id="4e198-182">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="4e198-183">ASP.NET Core 2.1 或更高版本的 web 应用程序模板 （从 Visual Studio 或 dotnet 命令行） 启用[HTTPS 重定向](#require)和[HSTS](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="4e198-183">The ASP.NET Core 2.1 or later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="4e198-184">对于不需要 HTTPS 的部署，你可以选择退出的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="4e198-184">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="4e198-185">例如，不需要其中 HTTPS 正在从外部在边缘，每个节点，使用 HTTPS 某些后端服务。</span><span class="sxs-lookup"><span data-stu-id="4e198-185">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node is not needed.</span></span>

<span data-ttu-id="4e198-186">若要选择退出的 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="4e198-186">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="4e198-187">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e198-187">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="4e198-188">取消选中**配置为支持 HTTPS**复选框。</span><span class="sxs-lookup"><span data-stu-id="4e198-188">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="4e198-190">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="4e198-190">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="4e198-191">使用 `--no-https` 选项。</span><span class="sxs-lookup"><span data-stu-id="4e198-191">Use the `--no-https` option.</span></span> <span data-ttu-id="4e198-192">例如</span><span class="sxs-lookup"><span data-stu-id="4e198-192">For example</span></span>

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a><span data-ttu-id="4e198-193">如何设置用于 Docker 的开发人员证书</span><span class="sxs-lookup"><span data-stu-id="4e198-193">How to setup a developer certificate for Docker</span></span>

<span data-ttu-id="4e198-194">请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。</span><span class="sxs-lookup"><span data-stu-id="4e198-194">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end
