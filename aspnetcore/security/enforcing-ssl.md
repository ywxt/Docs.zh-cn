---
title: 强制实施 HTTPS 在 ASP.NET 核心
author: rick-anderson
description: 演示如何要求在 ASP.NET Core HTTPS/TLS web 应用。
manager: wpickett
ms.author: riande
ms.date: 2/9/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/enforcing-ssl
ms.openlocfilehash: 48a25b7ba7affe84cfa6fe16096409239c510221
ms.sourcegitcommit: 40b102ecf88e53d9d872603ce6f3f7044bca95ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35652183"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="d29e0-103">强制实施 HTTPS 在 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="d29e0-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="d29e0-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d29e0-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d29e0-105">本文档说明如何：</span><span class="sxs-lookup"><span data-stu-id="d29e0-105">This document shows how to:</span></span>

* <span data-ttu-id="d29e0-106">所有请求需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="d29e0-107">所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="d29e0-108">执行**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。</span><span class="sxs-lookup"><span data-stu-id="d29e0-108">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="d29e0-109">`RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。</span><span class="sxs-lookup"><span data-stu-id="d29e0-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="d29e0-110">API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。</span><span class="sxs-lookup"><span data-stu-id="d29e0-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="d29e0-111">此类客户端可能会通过 HTTP 发送信息。</span><span class="sxs-lookup"><span data-stu-id="d29e0-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="d29e0-112">Web Api 应具有下列任一：</span><span class="sxs-lookup"><span data-stu-id="d29e0-112">Web APIs should either:</span></span>
>
> * <span data-ttu-id="d29e0-113">不在 HTTP 上侦听。</span><span class="sxs-lookup"><span data-stu-id="d29e0-113">Not listen on HTTP.</span></span>
> * <span data-ttu-id="d29e0-114">关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="d29e0-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>
## <a name="require-https"></a><span data-ttu-id="d29e0-115">需要 HTTPS</span><span class="sxs-lookup"><span data-stu-id="d29e0-115">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="d29e0-116">我们建议所有 ASP.NET 核心 web 应用都调用 HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 将所有 HTTP 请求重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-116">We recommend all ASP.NET Core web apps call HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="d29e0-117">下面的代码调用`UseHttpsRedirection`中`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="d29e0-117">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

<span data-ttu-id="d29e0-118">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-118">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]</span></span>

<span data-ttu-id="d29e0-119">下面的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：</span><span class="sxs-lookup"><span data-stu-id="d29e0-119">The following code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

<span data-ttu-id="d29e0-120">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-120">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]</span></span>

<span data-ttu-id="d29e0-121">前面的突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="d29e0-121">The preceding highlighted code:</span></span>

* <span data-ttu-id="d29e0-122">集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到`Status307TemporaryRedirect`，这是默认值。</span><span class="sxs-lookup"><span data-stu-id="d29e0-122">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to `Status307TemporaryRedirect`, which is the default value.</span></span> <span data-ttu-id="d29e0-123">生产应用程序应调用[UseHsts](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-123">Production apps should call [UseHsts](#hsts).</span></span>
* <span data-ttu-id="d29e0-124">将 HTTPS 端口设置为 5001。</span><span class="sxs-lookup"><span data-stu-id="d29e0-124">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="d29e0-125">默认值为 443。</span><span class="sxs-lookup"><span data-stu-id="d29e0-125">The default value is 443.</span></span>

<span data-ttu-id="d29e0-126">使用以下机制将自动设置端口：</span><span class="sxs-lookup"><span data-stu-id="d29e0-126">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="d29e0-127">该中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)当以下条件适用：</span><span class="sxs-lookup"><span data-stu-id="d29e0-127">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>
  - <span data-ttu-id="d29e0-128">直接与 HTTPS 终结点使用 kestrel 还是 HTTP.sys （也适用于使用 Visual Studio 代码的调试器中运行应用程序）。</span><span class="sxs-lookup"><span data-stu-id="d29e0-128">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
  - <span data-ttu-id="d29e0-129">仅**一个 HTTPS 端口**应用使用。</span><span class="sxs-lookup"><span data-stu-id="d29e0-129">Only **one HTTPS port** is used by the app.</span></span>
* <span data-ttu-id="d29e0-130">使用 visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d29e0-130">Visual Studio is used:</span></span>
  - <span data-ttu-id="d29e0-131">IIS Express 中包含启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-131">IIS Express has HTTPS enabled.</span></span>
  - <span data-ttu-id="d29e0-132">*launchSettings.json*设置`sslPort`IIS express。</span><span class="sxs-lookup"><span data-stu-id="d29e0-132">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="d29e0-133">反向代理 （例如，IIS，IIS Express），后面运行应用时`IServerAddressesFeature`不可用。</span><span class="sxs-lookup"><span data-stu-id="d29e0-133">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="d29e0-134">必须手动配置端口。</span><span class="sxs-lookup"><span data-stu-id="d29e0-134">The port must be manually configured.</span></span> <span data-ttu-id="d29e0-135">如果未设置端口，请求不重定向。</span><span class="sxs-lookup"><span data-stu-id="d29e0-135">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="d29e0-136">可以通过设置配置端口:</span><span class="sxs-lookup"><span data-stu-id="d29e0-136">The port can be configured by setting the:</span></span>

* <span data-ttu-id="d29e0-137">`ASPNETCORE_HTTPS_PORT` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="d29e0-137">`ASPNETCORE_HTTPS_PORT` environment variable.</span></span>
* <span data-ttu-id="d29e0-138">`http_port` 主机配置项 (例如，通过*hostsettings.json*或命令行自变量)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-138">`http_port` host configuration key (for example, via *hostsettings.json* or a command line argument).</span></span>
* <span data-ttu-id="d29e0-139">[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-139">[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport).</span></span> <span data-ttu-id="d29e0-140">请参阅前面的示例演示如何设置为 5001 的端口。</span><span class="sxs-lookup"><span data-stu-id="d29e0-140">See the preceding example that shows how to set the port to 5001.</span></span>

> [!NOTE]
> <span data-ttu-id="d29e0-141">可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。</span><span class="sxs-lookup"><span data-stu-id="d29e0-141">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="d29e0-142">环境变量配置服务器，，然后该中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。</span><span class="sxs-lookup"><span data-stu-id="d29e0-142">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="d29e0-143">如果没有端口设置：</span><span class="sxs-lookup"><span data-stu-id="d29e0-143">If no port is set:</span></span>

* <span data-ttu-id="d29e0-144">请求没有重定向。</span><span class="sxs-lookup"><span data-stu-id="d29e0-144">Requests aren't redirected.</span></span>
* <span data-ttu-id="d29e0-145">该中间件记录警告。</span><span class="sxs-lookup"><span data-stu-id="d29e0-145">The middleware logs a warning.</span></span>

> [!NOTE]
> <span data-ttu-id="d29e0-146">使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-146">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="d29e0-147">`AddRedirectToHttps` 此外可以设置的状态代码和端口执行重定向时。</span><span class="sxs-lookup"><span data-stu-id="d29e0-147">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="d29e0-148">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-148">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="d29e0-149">当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。</span><span class="sxs-lookup"><span data-stu-id="d29e0-149">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="d29e0-150">[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-150">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="d29e0-151">`[RequireHttpsAttribute]` 可修饰控制器或方法，或可以全局应用。</span><span class="sxs-lookup"><span data-stu-id="d29e0-151">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="d29e0-152">若要全局应用该属性，以下代码添加到`ConfigureServices`中`Startup`:</span><span class="sxs-lookup"><span data-stu-id="d29e0-152">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

<span data-ttu-id="d29e0-153">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-153">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]</span></span>

<span data-ttu-id="d29e0-154">前面的突出显示的代码中需要的所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="d29e0-154">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="d29e0-155">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d29e0-155">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

<span data-ttu-id="d29e0-156">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-156">[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]</span></span>

<span data-ttu-id="d29e0-157">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-157">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="d29e0-158">该中间件还允许应用程序以执行重定向时设置的状态代码或状态代码和端口。</span><span class="sxs-lookup"><span data-stu-id="d29e0-158">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="d29e0-159">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="d29e0-159">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="d29e0-160">应用`[RequireHttps]`特性应用到所有控制器/Razor 页面不会被视为尽可能安全全局需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-160">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="d29e0-161">你不能保证`[RequireHttps]`添加新控制器和 Razor 页时应用特性。</span><span class="sxs-lookup"><span data-stu-id="d29e0-161">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="d29e0-162">HTTP 严格的传输安全协议 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="d29e0-162">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="d29e0-163">每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是由 web 应用程序通过使用特殊的响应标头指定可以选择使用的安全增强。</span><span class="sxs-lookup"><span data-stu-id="d29e0-163">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that is specified by a web application through the use of a special response header.</span></span> <span data-ttu-id="d29e0-164">支持的浏览器收到此标头后该浏览器将阻止从正在通过 HTTP 发送到指定的域的任何通信，并改为将通过 HTTPS 发送的所有通信。</span><span class="sxs-lookup"><span data-stu-id="d29e0-164">Once a supported browser receives this header that browser will prevent any communications from being sent over HTTP to the specified domain and will instead send all communications over HTTPS.</span></span> <span data-ttu-id="d29e0-165">它还可以防止 HTTPS 单击通过在浏览器上的提示。</span><span class="sxs-lookup"><span data-stu-id="d29e0-165">It also prevents HTTPS click through prompts on browsers.</span></span>

<span data-ttu-id="d29e0-166">ASP.NET 核心 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="d29e0-166">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="d29e0-167">下面的代码调用`UseHsts`时应用程序不在[开发模式](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="d29e0-167">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

<span data-ttu-id="d29e0-168">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-168">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]</span></span>

<span data-ttu-id="d29e0-169">`UseHsts` 不建议在开发过程中的因为 HSTS 标头是高度可通过浏览器缓存。</span><span class="sxs-lookup"><span data-stu-id="d29e0-169">`UseHsts` is not recommend in development because the HSTS header is highly cachable by browsers.</span></span> <span data-ttu-id="d29e0-170">默认情况下，UseHsts 排除本地环回地址。</span><span class="sxs-lookup"><span data-stu-id="d29e0-170">By default, UseHsts excludes the local loopback address.</span></span>

<span data-ttu-id="d29e0-171">下面的代码：</span><span class="sxs-lookup"><span data-stu-id="d29e0-171">The following code:</span></span>

<span data-ttu-id="d29e0-172">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]</span><span class="sxs-lookup"><span data-stu-id="d29e0-172">[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]</span></span>

* <span data-ttu-id="d29e0-173">设置预加载参数 Strict 传输安全标头。</span><span class="sxs-lookup"><span data-stu-id="d29e0-173">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="d29e0-174">预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但若要预加载 HSTS 站点上执行全新安装的 web 浏览器都支持。</span><span class="sxs-lookup"><span data-stu-id="d29e0-174">Preload is not part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="d29e0-175">有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-175">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="d29e0-176">使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，该方案 HSTS 策略适用于主机子域。</span><span class="sxs-lookup"><span data-stu-id="d29e0-176">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span> 
* <span data-ttu-id="d29e0-177">显式将 Strict 传输安全标头到的最大有效期参数设置为 60 天。</span><span class="sxs-lookup"><span data-stu-id="d29e0-177">Explicitly sets the max-age parameter of the Strict-Transport-Security header to to 60 days.</span></span> <span data-ttu-id="d29e0-178">如果未设置，默认值为 30 天。</span><span class="sxs-lookup"><span data-stu-id="d29e0-178">If not set, defaults to 30 days.</span></span> <span data-ttu-id="d29e0-179">请参阅[最长时间指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="d29e0-179">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="d29e0-180">将添加`example.com`到的主机排除列表。</span><span class="sxs-lookup"><span data-stu-id="d29e0-180">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="d29e0-181">`UseHsts` 排除以下环回主机：</span><span class="sxs-lookup"><span data-stu-id="d29e0-181">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="d29e0-182">`localhost` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="d29e0-182">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="d29e0-183">`127.0.0.1` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="d29e0-183">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="d29e0-184">`[::1]` : IPv6 环回地址。</span><span class="sxs-lookup"><span data-stu-id="d29e0-184">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="d29e0-185">前面的示例演示如何添加其他主机。</span><span class="sxs-lookup"><span data-stu-id="d29e0-185">The preceding example shows how to add additional hosts.</span></span>
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a><span data-ttu-id="d29e0-186">选择退出的 HTTPS 在项目创建</span><span class="sxs-lookup"><span data-stu-id="d29e0-186">Opt-out of HTTPS on project creation</span></span>

<span data-ttu-id="d29e0-187">ASP.NET 核心 2.1 或更高版本的 web 应用程序模板 （从 Visual Studio 或 dotnet 命令行） 启用[HTTPS 重定向](#require)和[HSTS](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-187">The ASP.NET Core 2.1 or later web application templates (from Visual Studio or the dotnet command line) enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="d29e0-188">对于不需要 HTTPS 的部署，你可以选择退出的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d29e0-188">For deployments that don't require HTTPS, you can opt-out of HTTPS.</span></span> <span data-ttu-id="d29e0-189">例如，不需要其中 HTTPS 正在处理外部在边缘，在每个节点使用 HTTPS 某些后端服务。</span><span class="sxs-lookup"><span data-stu-id="d29e0-189">For example, some backend services where HTTPS is being handled externally at the edge, using HTTPS at each node is not needed.</span></span>

<span data-ttu-id="d29e0-190">若要选择退出的 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d29e0-190">To opt-out of HTTPS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d29e0-191">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d29e0-191">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="d29e0-192">取消选中**针对 HTTPS 配置**复选框。</span><span class="sxs-lookup"><span data-stu-id="d29e0-192">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="d29e0-194">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="d29e0-194">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="d29e0-195">使用 `--no-https` 选项。</span><span class="sxs-lookup"><span data-stu-id="d29e0-195">Use the `--no-https` option.</span></span> <span data-ttu-id="d29e0-196">例如</span><span class="sxs-lookup"><span data-stu-id="d29e0-196">For example</span></span>

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a><span data-ttu-id="d29e0-198">如何为 Docker 设置开发人员证书</span><span class="sxs-lookup"><span data-stu-id="d29e0-198">How to setup a developer certificate for Docker</span></span>

<span data-ttu-id="d29e0-199">请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。</span><span class="sxs-lookup"><span data-stu-id="d29e0-199">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end
