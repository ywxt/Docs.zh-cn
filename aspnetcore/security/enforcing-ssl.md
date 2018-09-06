---
title: 强制实施 HTTPS 在 ASP.NET Core
author: rick-anderson
description: 演示如何要求在 ASP.NET Core HTTPS/TLS web 应用。
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 838cd00545f36736461616f806942249aaf6eee0
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893173"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="cc0ca-103">强制实施 HTTPS 在 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cc0ca-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="cc0ca-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cc0ca-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cc0ca-105">本文档演示如何：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-105">This document shows how to:</span></span>

* <span data-ttu-id="cc0ca-106">要求所有请求使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="cc0ca-107">将所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-107">Redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="cc0ca-108">没有 API 可以防止客户端上的第一个请求发送敏感数据。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-108">No API can prevent a client from sending sensitive data on the first request.</span></span>

> [!WARNING]
> <span data-ttu-id="cc0ca-109">不要**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-109">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="cc0ca-110">`RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-110">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="cc0ca-111">API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-111">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="cc0ca-112">此类客户端可能会通过 HTTP 发送的信息。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-112">Such clients may send information over HTTP.</span></span> <span data-ttu-id="cc0ca-113">Web Api 应具有下列任一：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-113">Web APIs should either:</span></span>
>
> * <span data-ttu-id="cc0ca-114">不侦听 HTTP。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-114">Not listen on HTTP.</span></span>
> * <span data-ttu-id="cc0ca-115">关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-115">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="cc0ca-116">要求使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="cc0ca-116">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="cc0ca-117">我们建议所有生产 ASP.NET Core web 应用调用：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-117">We recommend all production ASP.NET Core web apps call:</span></span>

* <span data-ttu-id="cc0ca-118">HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 所有 HTTP 请求重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-118">The HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>
* <span data-ttu-id="cc0ca-119">[UseHsts](#hsts)，HTTP 严格传输安全协议 (HSTS)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-119">[UseHsts](#hsts), HTTP Strict Transport Security Protocol (HSTS).</span></span>

### <a name="usehttpsredirection"></a><span data-ttu-id="cc0ca-120">UseHttpsRedirection</span><span class="sxs-lookup"><span data-stu-id="cc0ca-120">UseHttpsRedirection</span></span>

<span data-ttu-id="cc0ca-121">下面的代码调用`UseHttpsRedirection`在`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-121">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

<span data-ttu-id="cc0ca-122">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-122">The preceding highlighted code:</span></span>

* <span data-ttu-id="cc0ca-123">使用默认[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-123">Uses the default [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) (`Status307TemporaryRedirect`).</span></span>
* <span data-ttu-id="cc0ca-124">使用默认[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)除非被重写 (null)`ASPNETCORE_HTTPS_PORT`环境变量或[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-124">Uses the default [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (null) unless overridden by the `ASPNETCORE_HTTPS_PORT` environment variable or [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature).</span></span>

> [!WARNING] 
><span data-ttu-id="cc0ca-125">端口必须是可用于中间件重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-125">A port must be available for the middleware to redirect to HTTPS.</span></span> <span data-ttu-id="cc0ca-126">如果没有端口不可用，则不会发生重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-126">If no port is available, redirection to HTTPS does not occur.</span></span> <span data-ttu-id="cc0ca-127">可以通过任何以下设置指定 HTTPS 端口：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-127">The HTTPS port can be specified by any of the following setting:</span></span>
> 
>* `HttpsRedirectionOptions.HttpsPort` 
>* <span data-ttu-id="cc0ca-128">`ASPNETCORE_HTTPS_PORT`环境变量。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-128">The `ASPNETCORE_HTTPS_PORT` environment variable.</span></span> 
>* <span data-ttu-id="cc0ca-129">在开发中，在 HTTPS url *launchsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-129">In development, an HTTPS url in *launchsettings.json*.</span></span> 
>* <span data-ttu-id="cc0ca-130">直接在 Kestrel 或 HttpSys 上配置 HTTPS url。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-130">An HTTPS url configured directly on Kestrel or HttpSys.</span></span> 

<span data-ttu-id="cc0ca-131">以下突出显示的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-131">The following highlighted code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

<span data-ttu-id="cc0ca-132">调用`AddHttpsRedirection`只是用来更改的值` HttpsPort`或` RedirectStatusCode`;</span><span class="sxs-lookup"><span data-stu-id="cc0ca-132">Calling `AddHttpsRedirection` is only necessary to change the values of ` HttpsPort` or ` RedirectStatusCode`;</span></span>

<span data-ttu-id="cc0ca-133">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-133">The preceding highlighted code:</span></span>

* <span data-ttu-id="cc0ca-134">集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到`Status307TemporaryRedirect`，这是默认值。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-134">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to `Status307TemporaryRedirect`, which is the default value.</span></span>
* <span data-ttu-id="cc0ca-135">设置 HTTPS 端口为 5001。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-135">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="cc0ca-136">默认值为 443。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-136">The default value is 443.</span></span>

<span data-ttu-id="cc0ca-137">以下机制自动设置端口：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-137">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="cc0ca-138">中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)时满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-138">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>

   * <span data-ttu-id="cc0ca-139">Kestrel 或 HTTP.sys 直接与 HTTPS 终结点一起使用 （也适用于使用 Visual Studio Code 的调试器中运行应用程序）。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-139">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
   * <span data-ttu-id="cc0ca-140">仅**一个 HTTPS 端口**应用使用。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-140">Only **one HTTPS port** is used by the app.</span></span>

* <span data-ttu-id="cc0ca-141">使用 visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cc0ca-141">Visual Studio is used:</span></span>
   * <span data-ttu-id="cc0ca-142">IIS Express 已启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-142">IIS Express has HTTPS enabled.</span></span>
   * <span data-ttu-id="cc0ca-143">*launchSettings.json*设置`sslPort`IIS express。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-143">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="cc0ca-144">当应用程序运行时在反向代理 （例如，IIS，IIS Express），后面`IServerAddressesFeature`不可用。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-144">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="cc0ca-145">必须手动配置端口。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-145">The port must be manually configured.</span></span> <span data-ttu-id="cc0ca-146">如果端口未设置，请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-146">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="cc0ca-147">可以通过设置配置端口[https_port Web 主机配置设置](xref:fundamentals/host/web-host#https-port):</span><span class="sxs-lookup"><span data-stu-id="cc0ca-147">The port can be configured by setting the [https_port Web Host configuration setting](xref:fundamentals/host/web-host#https-port):</span></span>

<span data-ttu-id="cc0ca-148">**密钥**: https_port</span><span class="sxs-lookup"><span data-stu-id="cc0ca-148">**Key**: https_port</span></span>  
<span data-ttu-id="cc0ca-149">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="cc0ca-149">**Type**: *string*</span></span>  
<span data-ttu-id="cc0ca-150">**默认**： 未设置默认值。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-150">**Default**: A default value isn't set.</span></span>  
<span data-ttu-id="cc0ca-151">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="cc0ca-151">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="cc0ca-152">**环境变量**: `<PREFIX_>HTTPS_PORT` (前缀是`ASPNETCORE_`使用 Web 主机时。)</span><span class="sxs-lookup"><span data-stu-id="cc0ca-152">**Environment variable**: `<PREFIX_>HTTPS_PORT` (The prefix is `ASPNETCORE_` when using the Web Host.)</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> <span data-ttu-id="cc0ca-153">可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-153">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="cc0ca-154">环境变量配置的服务器，，然后在中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-154">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="cc0ca-155">如果没有端口设置：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-155">If no port is set:</span></span>

* <span data-ttu-id="cc0ca-156">请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-156">Requests aren't redirected.</span></span>
* <span data-ttu-id="cc0ca-157">中间件将记录警告"无法确定重定向的 https 端口。"</span><span class="sxs-lookup"><span data-stu-id="cc0ca-157">The middleware logs the warning "Failed to determine the https port for redirect."</span></span>

> [!NOTE]
> <span data-ttu-id="cc0ca-158">使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-158">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="cc0ca-159">`AddRedirectToHttps` 此外可以设置的状态代码和端口时执行重定向。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-159">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="cc0ca-160">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-160">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="cc0ca-161">当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-161">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="cc0ca-162">[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于要求 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-162">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="cc0ca-163">`[RequireHttpsAttribute]` 可以修饰控制器或方法，也可以全局应用。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-163">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="cc0ca-164">若要全局应用该属性，将以下代码添加到`ConfigureServices`在`Startup`:</span><span class="sxs-lookup"><span data-stu-id="cc0ca-164">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="cc0ca-165">前面突出显示的代码要求所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-165">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="cc0ca-166">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="cc0ca-166">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="cc0ca-167">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-167">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="cc0ca-168">中间件还允许应用执行重定向时设置的状态代码或状态代码和端口。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-168">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="cc0ca-169">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-169">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="cc0ca-170">将应用`[RequireHttps]`属性设置为所有控制器/Razor 页面不会被视为与需要 HTTPS 全局一样安全。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-170">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="cc0ca-171">不能保证`[RequireHttps]`时添加新的控制器和 Razor 页面应用属性。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-171">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="cc0ca-172">HTTP 严格传输安全协议 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="cc0ca-172">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="cc0ca-173">每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全性 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是通过响应标头使用的 web 应用指定选择的安全增强功能。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-173">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that's specified by a web app through the use of a response header.</span></span> <span data-ttu-id="cc0ca-174">当[浏览器支持 HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)收到此标头：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-174">When a [browser that supports HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support) receives this header:</span></span>

* <span data-ttu-id="cc0ca-175">在浏览器将会阻止通过 HTTP 发送的任何通信的域的配置存储。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-175">The browser stores configuration for the domain that prevents sending any communication over HTTP.</span></span> <span data-ttu-id="cc0ca-176">在浏览器强制通过 HTTPS 进行的所有通信。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-176">The browser forces all communication over HTTPS.</span></span>
* <span data-ttu-id="cc0ca-177">在浏览器可防止用户使用不受信任或无效的证书。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-177">The browser prevents the user from using untrusted or invalid certificates.</span></span> <span data-ttu-id="cc0ca-178">在浏览器禁用允许用户暂时信任此证书的提示。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-178">The browser disables prompts that allow a user to temporarily trust such a certificate.</span></span>

<span data-ttu-id="cc0ca-179">因为由客户端强制执行 HSTS 它具有一些限制：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-179">Because HSTS is enforced by the client it has some limitations:</span></span>

* <span data-ttu-id="cc0ca-180">客户端必须支持 HSTS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-180">The client must support HSTS.</span></span>
* <span data-ttu-id="cc0ca-181">HSTS 要求至少一个成功的 HTTPS 请求能够建立 HSTS 策略。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-181">HSTS requires at least one successful HTTPS request to establish the HSTS policy.</span></span>
* <span data-ttu-id="cc0ca-182">应用程序必须检查每个 HTTP 请求和重定向或拒绝的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-182">The application must check every HTTP request and redirect or reject the HTTP request.</span></span>

<span data-ttu-id="cc0ca-183">ASP.NET Core 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-183">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="cc0ca-184">下面的代码调用`UseHsts`时应用不在[开发模式](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="cc0ca-184">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

<span data-ttu-id="cc0ca-185">`UseHsts` 不建议在开发过程中由于 HSTS 设置高度可缓存的浏览器。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-185">`UseHsts` isn't recommended in development because the HSTS settings are highly cacheable by browsers.</span></span> <span data-ttu-id="cc0ca-186">默认情况下，`UseHsts`排除本地环回地址。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-186">By default, `UseHsts` excludes the local loopback address.</span></span>

<span data-ttu-id="cc0ca-187">对于生产环境首次实现 HTTPS 初始 HSTS 将值设置为较小的值。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-187">For production environments implementing HTTPS for the first time, set the initial HSTS value to a small value.</span></span> <span data-ttu-id="cc0ca-188">设置的值从小时数不超过一天的以防到时需要还原 HTTP 到 HTTPS 基础结构。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-188">Set the value from hours to no more than a single day in case you need to revert the HTTPS infrastructure to HTTP.</span></span> <span data-ttu-id="cc0ca-189">确信 HTTPS 配置的可持续发展中后，增加 HSTS 最大期限值;常用的值为一年。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-189">After you're confident in the sustainability of the HTTPS configuration, increase the HSTS max-age value; a commonly used value is one year.</span></span> 

<span data-ttu-id="cc0ca-190">下面的代码：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-190">The following code:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* <span data-ttu-id="cc0ca-191">设置预加载严格传输安全性标头的参数。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-191">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="cc0ca-192">预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但要预加载 HSTS 站点上执行全新安装的 web 浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-192">Preload isn't part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="cc0ca-193">有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-193">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="cc0ca-194">使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，这将 HSTS 策略应用到主机的子域。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-194">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="cc0ca-195">显式将严格传输安全性标头的最大期限参数设置为 60 天。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-195">Explicitly sets the max-age parameter of the Strict-Transport-Security header to 60 days.</span></span> <span data-ttu-id="cc0ca-196">如果未设置，默认值为 30 天。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-196">If not set, defaults to 30 days.</span></span> <span data-ttu-id="cc0ca-197">请参阅[最大期限指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-197">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="cc0ca-198">添加`example.com`到主机以排除列表。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-198">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="cc0ca-199">`UseHsts` 不包括以下环回主机：</span><span class="sxs-lookup"><span data-stu-id="cc0ca-199">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="cc0ca-200">`localhost` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-200">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="cc0ca-201">`127.0.0.1` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-201">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="cc0ca-202">`[::1]` : IPv6 环回地址。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-202">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="cc0ca-203">前面的示例演示如何添加其他主机。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-203">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="cc0ca-204">选择退出的 HTTPS 在项目创建</span><span class="sxs-lookup"><span data-stu-id="cc0ca-204">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="cc0ca-205">ASP.NET Core 2.1 或更高版本的 web 应用程序模板 （从 Visual Studio 或 dotnet 命令行） 启用[HTTPS 重定向](#require)和[HSTS](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-205">The ASP.NET Core 2.1 or later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="cc0ca-206">对于不需要 HTTPS 的部署，你可以选择退出的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-206">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="cc0ca-207">例如，不需要其中 HTTPS 正在从外部在边缘，每个节点，使用 HTTPS 某些后端服务。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-207">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node isn't needed.</span></span>

<span data-ttu-id="cc0ca-208">若要选择退出的 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="cc0ca-208">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="cc0ca-209">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc0ca-209">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="cc0ca-210">取消选中**配置为支持 HTTPS**复选框。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-210">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="cc0ca-212">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="cc0ca-212">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="cc0ca-213">使用 `--no-https` 选项。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-213">Use the `--no-https` option.</span></span> <span data-ttu-id="cc0ca-214">例如</span><span class="sxs-lookup"><span data-stu-id="cc0ca-214">For example</span></span>

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-set-up-a-developer-certificate-for-docker"></a><span data-ttu-id="cc0ca-215">如何设置适用于 Docker 的开发人员证书</span><span class="sxs-lookup"><span data-stu-id="cc0ca-215">How to set up a developer certificate for Docker</span></span>

<span data-ttu-id="cc0ca-216">请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。</span><span class="sxs-lookup"><span data-stu-id="cc0ca-216">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end

## <a name="additional-information"></a><span data-ttu-id="cc0ca-217">其他信息</span><span class="sxs-lookup"><span data-stu-id="cc0ca-217">Additional information</span></span>

* [<span data-ttu-id="cc0ca-218">OWASP HSTS 浏览器支持</span><span class="sxs-lookup"><span data-stu-id="cc0ca-218">OWASP HSTS browser support</span></span>](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)
