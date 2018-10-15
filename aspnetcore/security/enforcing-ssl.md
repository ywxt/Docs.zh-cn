---
title: 强制实施 HTTPS 在 ASP.NET Core
author: rick-anderson
description: 了解如何在 ASP.NET Core web 应用中需要 HTTPS/TLS。
ms.author: riande
ms.custom: mvc
ms.date: 10/11/2018
uid: security/enforcing-ssl
ms.openlocfilehash: b4c058d3b4f00276043d9520d756e62ed8cac5d9
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325596"
---
# <a name="enforce-https-in-aspnet-core"></a><span data-ttu-id="11494-103">强制实施 HTTPS 在 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="11494-103">Enforce HTTPS in ASP.NET Core</span></span>

<span data-ttu-id="11494-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="11494-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="11494-105">本文档演示如何：</span><span class="sxs-lookup"><span data-stu-id="11494-105">This document shows how to:</span></span>

* <span data-ttu-id="11494-106">要求所有请求使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-106">Require HTTPS for all requests.</span></span>
* <span data-ttu-id="11494-107">将所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-107">Redirect all HTTP requests to HTTPS.</span></span>

<span data-ttu-id="11494-108">没有 API 可以防止客户端上的第一个请求发送敏感数据。</span><span class="sxs-lookup"><span data-stu-id="11494-108">No API can prevent a client from sending sensitive data on the first request.</span></span>

> [!WARNING]
> <span data-ttu-id="11494-109">不要**不**使用[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)接收敏感信息的 Web api。</span><span class="sxs-lookup"><span data-stu-id="11494-109">Do **not** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="11494-110">`RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。</span><span class="sxs-lookup"><span data-stu-id="11494-110">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="11494-111">API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。</span><span class="sxs-lookup"><span data-stu-id="11494-111">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="11494-112">此类客户端可能会通过 HTTP 发送的信息。</span><span class="sxs-lookup"><span data-stu-id="11494-112">Such clients may send information over HTTP.</span></span> <span data-ttu-id="11494-113">Web Api 应具有下列任一：</span><span class="sxs-lookup"><span data-stu-id="11494-113">Web APIs should either:</span></span>
>
> * <span data-ttu-id="11494-114">不侦听 HTTP。</span><span class="sxs-lookup"><span data-stu-id="11494-114">Not listen on HTTP.</span></span>
> * <span data-ttu-id="11494-115">关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="11494-115">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

<a name="require"></a>

## <a name="require-https"></a><span data-ttu-id="11494-116">要求使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="11494-116">Require HTTPS</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="11494-117">我们建议所有生产 ASP.NET Core web 应用调用：</span><span class="sxs-lookup"><span data-stu-id="11494-117">We recommend all production ASP.NET Core web apps call:</span></span>

* <span data-ttu-id="11494-118">HTTPS 重定向中间件 ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) 所有 HTTP 请求重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-118">The HTTPS Redirection Middleware ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) to redirect all HTTP requests to HTTPS.</span></span>
* <span data-ttu-id="11494-119">[UseHsts](#hsts)，HTTP 严格传输安全协议 (HSTS)。</span><span class="sxs-lookup"><span data-stu-id="11494-119">[UseHsts](#hsts), HTTP Strict Transport Security Protocol (HSTS).</span></span>

### <a name="usehttpsredirection"></a><span data-ttu-id="11494-120">UseHttpsRedirection</span><span class="sxs-lookup"><span data-stu-id="11494-120">UseHttpsRedirection</span></span>

<span data-ttu-id="11494-121">下面的代码调用`UseHttpsRedirection`在`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="11494-121">The following code calls `UseHttpsRedirection` in the `Startup` class:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

<span data-ttu-id="11494-122">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="11494-122">The preceding highlighted code:</span></span>

* <span data-ttu-id="11494-123">使用默认[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) ([Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect))。</span><span class="sxs-lookup"><span data-stu-id="11494-123">Uses the default [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) ([Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect)).</span></span>
* <span data-ttu-id="11494-124">使用默认[HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport)除非被重写 (null)`ASPNETCORE_HTTPS_PORT`环境变量或[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)。</span><span class="sxs-lookup"><span data-stu-id="11494-124">Uses the default [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport) (null) unless overridden by the `ASPNETCORE_HTTPS_PORT` environment variable or [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature).</span></span>

<span data-ttu-id="11494-125">我们建议使用临时重定向而不是永久重定向，因为链接缓存可能会在开发环境中导致不稳定行为。</span><span class="sxs-lookup"><span data-stu-id="11494-125">We recommend using temporary redirects rather than permanent redirects, as link caching can cause unstable behavior in development environments.</span></span> <span data-ttu-id="11494-126">我们建议使用[HSTS](#hsts)将信号发送到仅保护资源的客户端请求应发送到应用 （仅在生产中）。</span><span class="sxs-lookup"><span data-stu-id="11494-126">We recommend using [HSTS](#hsts) to signal to clients that only secure resource requests should be sent to the app (only in production).</span></span>

> [!WARNING]
> <span data-ttu-id="11494-127">端口必须是可用于中间件重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-127">A port must be available for the middleware to redirect to HTTPS.</span></span> <span data-ttu-id="11494-128">如果任何端口，不则不会发生重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-128">If no port is available, redirection to HTTPS doesn't occur.</span></span> <span data-ttu-id="11494-129">可以使用任何以下方法之一指定 HTTPS 端口：</span><span class="sxs-lookup"><span data-stu-id="11494-129">The HTTPS port can be specified using any of the following approaches:</span></span>
>
> * <span data-ttu-id="11494-130">设置`HttpsRedirectionOptions.HttpsPort`。</span><span class="sxs-lookup"><span data-stu-id="11494-130">Set `HttpsRedirectionOptions.HttpsPort`.</span></span>
> * <span data-ttu-id="11494-131">设置 `ASPNETCORE_HTTPS_PORT` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="11494-131">Set the `ASPNETCORE_HTTPS_PORT` environment variable.</span></span>
> * <span data-ttu-id="11494-132">在开发中，在中设置 HTTPS URL *launchsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="11494-132">In development, set an HTTPS URL in *launchsettings.json*.</span></span>
> * <span data-ttu-id="11494-133">配置的 HTTPS URL 终结点[Kestrel](xref:fundamentals/servers/kestrel)或[HTTP.sys](xref:fundamentals/servers/httpsys)。</span><span class="sxs-lookup"><span data-stu-id="11494-133">Configure an HTTPS URL endpoint for [Kestrel](xref:fundamentals/servers/kestrel) or [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>
>
> <span data-ttu-id="11494-134">当 Kestrel 或 HTTP.sys 用作面向公众的边缘服务器时，必须配置 Kestrel 或 HTTP.sys，若要在其上同时侦听：</span><span class="sxs-lookup"><span data-stu-id="11494-134">When Kestrel or HTTP.sys is used as a public-facing edge server, Kestrel or HTTP.sys must be configured to listen on both:</span></span>
>
> * <span data-ttu-id="11494-135">其中重定向客户端的安全端口 (通常情况下，在生产和开发中的为 5001 的 443)。</span><span class="sxs-lookup"><span data-stu-id="11494-135">The secure port where the client is redirected (typically, 443 in production and 5001 in development).</span></span>
> * <span data-ttu-id="11494-136">不安全端口 (通常情况下，在生产环境中为 80) 和 5000 开发中。</span><span class="sxs-lookup"><span data-stu-id="11494-136">The insecure port (typically, 80 in production and 5000 in development).</span></span>
>
> <span data-ttu-id="11494-137">不安全的端口必须可访问的应用顺序中的客户端以接收不安全的请求并将其重定向到安全的端口。</span><span class="sxs-lookup"><span data-stu-id="11494-137">The insecure port must be accessible by the client in order for the app to receive an insecure request and redirect it to the secure port.</span></span>
>
> <span data-ttu-id="11494-138">客户端和服务器之间的所有防火墙也都必须打开的流量的端口。</span><span class="sxs-lookup"><span data-stu-id="11494-138">Any firewall between the client and server must also have the ports open for traffic.</span></span>
>
> <span data-ttu-id="11494-139">有关详细信息，请参阅[Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)或<xref:fundamentals/servers/httpsys>。</span><span class="sxs-lookup"><span data-stu-id="11494-139">For more information, see [Kestrel endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration) or <xref:fundamentals/servers/httpsys>.</span></span>

<span data-ttu-id="11494-140">以下突出显示的代码调用[AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection)配置中间件选项：</span><span class="sxs-lookup"><span data-stu-id="11494-140">The following highlighted code calls [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) to configure middleware options:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

<span data-ttu-id="11494-141">调用`AddHttpsRedirection`只是用来更改的值`HttpsPort`或`RedirectStatusCode`。</span><span class="sxs-lookup"><span data-stu-id="11494-141">Calling `AddHttpsRedirection` is only necessary to change the values of `HttpsPort` or `RedirectStatusCode`.</span></span>

<span data-ttu-id="11494-142">前面突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="11494-142">The preceding highlighted code:</span></span>

* <span data-ttu-id="11494-143">集[HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode)到[Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect)，这是默认值。</span><span class="sxs-lookup"><span data-stu-id="11494-143">Sets [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) to [Status307TemporaryRedirect](/dotnet/api/microsoft.aspnetcore.http.statuscodes.status307temporaryredirect), which is the default value.</span></span> <span data-ttu-id="11494-144">使用的字段[StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes)类的分配到`RedirectStatusCode`。</span><span class="sxs-lookup"><span data-stu-id="11494-144">Use the fields of the [StatusCodes](/dotnet/api/microsoft.aspnetcore.http.statuscodes) class for assignments to `RedirectStatusCode`.</span></span>
* <span data-ttu-id="11494-145">设置 HTTPS 端口为 5001。</span><span class="sxs-lookup"><span data-stu-id="11494-145">Sets the HTTPS port to 5001.</span></span> <span data-ttu-id="11494-146">默认值为 443。</span><span class="sxs-lookup"><span data-stu-id="11494-146">The default value is 443.</span></span>

<span data-ttu-id="11494-147">以下机制自动设置端口：</span><span class="sxs-lookup"><span data-stu-id="11494-147">The following mechanisms set the port automatically:</span></span>

* <span data-ttu-id="11494-148">中间件可以发现通过端口[IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)时满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="11494-148">The middleware can discover the ports via [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) when the following conditions apply:</span></span>

  * <span data-ttu-id="11494-149">Kestrel 或 HTTP.sys 直接与 HTTPS 终结点一起使用 （也适用于使用 Visual Studio Code 的调试器中运行应用程序）。</span><span class="sxs-lookup"><span data-stu-id="11494-149">Kestrel or HTTP.sys is used directly with HTTPS endpoints (also applies to running the app with Visual Studio Code's debugger).</span></span>
  * <span data-ttu-id="11494-150">仅**一个 HTTPS 端口**应用使用。</span><span class="sxs-lookup"><span data-stu-id="11494-150">Only **one HTTPS port** is used by the app.</span></span>

* <span data-ttu-id="11494-151">使用 visual Studio:</span><span class="sxs-lookup"><span data-stu-id="11494-151">Visual Studio is used:</span></span>

  * <span data-ttu-id="11494-152">IIS Express 已启用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-152">IIS Express has HTTPS enabled.</span></span>
  * <span data-ttu-id="11494-153">*launchSettings.json*设置`sslPort`IIS express。</span><span class="sxs-lookup"><span data-stu-id="11494-153">*launchSettings.json* sets the `sslPort` for IIS Express.</span></span>

> [!NOTE]
> <span data-ttu-id="11494-154">当应用程序运行时在反向代理 （例如，IIS，IIS Express），后面`IServerAddressesFeature`不可用。</span><span class="sxs-lookup"><span data-stu-id="11494-154">When an app is run behind a reverse proxy (for example, IIS, IIS Express), `IServerAddressesFeature` isn't available.</span></span> <span data-ttu-id="11494-155">必须手动配置端口。</span><span class="sxs-lookup"><span data-stu-id="11494-155">The port must be manually configured.</span></span> <span data-ttu-id="11494-156">如果端口未设置，请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="11494-156">When the port isn't set, requests aren't redirected.</span></span>

<span data-ttu-id="11494-157">可以通过设置配置端口[https_port Web 主机配置设置](xref:fundamentals/host/web-host#https-port):</span><span class="sxs-lookup"><span data-stu-id="11494-157">The port can be configured by setting the [https_port Web Host configuration setting](xref:fundamentals/host/web-host#https-port):</span></span>

<span data-ttu-id="11494-158">**密钥**: https_port</span><span class="sxs-lookup"><span data-stu-id="11494-158">**Key**: https_port</span></span>  
<span data-ttu-id="11494-159">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="11494-159">**Type**: *string*</span></span>  
<span data-ttu-id="11494-160">**默认**： 未设置默认值。</span><span class="sxs-lookup"><span data-stu-id="11494-160">**Default**: A default value isn't set.</span></span>  
<span data-ttu-id="11494-161">**设置使用**：`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="11494-161">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="11494-162">**环境变量**: `<PREFIX_>HTTPS_PORT` (前缀是`ASPNETCORE_`使用 Web 主机时。)</span><span class="sxs-lookup"><span data-stu-id="11494-162">**Environment variable**: `<PREFIX_>HTTPS_PORT` (The prefix is `ASPNETCORE_` when using the Web Host.)</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("https_port", "8080")
```

> [!NOTE]
> <span data-ttu-id="11494-163">可以通过设置与 URL 间接配置端口`ASPNETCORE_URLS`环境变量。</span><span class="sxs-lookup"><span data-stu-id="11494-163">The port can be configured indirectly by setting the URL with the `ASPNETCORE_URLS` environment variable.</span></span> <span data-ttu-id="11494-164">环境变量配置的服务器，，然后在中间件间接发现通过 HTTPS 端口`IServerAddressesFeature`。</span><span class="sxs-lookup"><span data-stu-id="11494-164">The environment variable configures the server, and then the middleware indirectly discovers the HTTPS port via `IServerAddressesFeature`.</span></span>

<span data-ttu-id="11494-165">如果没有端口设置：</span><span class="sxs-lookup"><span data-stu-id="11494-165">If no port is set:</span></span>

* <span data-ttu-id="11494-166">请求不会重定向。</span><span class="sxs-lookup"><span data-stu-id="11494-166">Requests aren't redirected.</span></span>
* <span data-ttu-id="11494-167">中间件将记录警告"无法确定重定向的 https 端口。"</span><span class="sxs-lookup"><span data-stu-id="11494-167">The middleware logs the warning "Failed to determine the https port for redirect."</span></span>

> [!NOTE]
> <span data-ttu-id="11494-168">使用 HTTPS 重定向中间件的替代方法 (`UseHttpsRedirection`) 是使用 URL 重写中间件 (`AddRedirectToHttps`)。</span><span class="sxs-lookup"><span data-stu-id="11494-168">An alternative to using HTTPS Redirection Middleware (`UseHttpsRedirection`) is to use URL Rewriting Middleware (`AddRedirectToHttps`).</span></span> <span data-ttu-id="11494-169">`AddRedirectToHttps` 此外可以设置的状态代码和端口时执行重定向。</span><span class="sxs-lookup"><span data-stu-id="11494-169">`AddRedirectToHttps` can also set the status code and port when the redirect is executed.</span></span> <span data-ttu-id="11494-170">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="11494-170">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>
>
> <span data-ttu-id="11494-171">当将重定向到 HTTPS 而无需其他重定向规则，我们建议使用 HTTPS 重定向中间件 (`UseHttpsRedirection`) 本主题中所述。</span><span class="sxs-lookup"><span data-stu-id="11494-171">When redirecting to HTTPS without the requirement for additional redirect rules, we recommend using HTTPS Redirection Middleware (`UseHttpsRedirection`) described in this topic.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="11494-172">[RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于要求 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="11494-172">The [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require HTTPS.</span></span> <span data-ttu-id="11494-173">`[RequireHttpsAttribute]` 可以修饰控制器或方法，也可以全局应用。</span><span class="sxs-lookup"><span data-stu-id="11494-173">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="11494-174">若要全局应用该属性，将以下代码添加到`ConfigureServices`在`Startup`:</span><span class="sxs-lookup"><span data-stu-id="11494-174">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](~/security/authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="11494-175">前面突出显示的代码要求所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="11494-175">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="11494-176">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="11494-176">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="11494-177">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="11494-177">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="11494-178">中间件还允许应用执行重定向时设置的状态代码或状态代码和端口。</span><span class="sxs-lookup"><span data-stu-id="11494-178">The middleware also permits the app to set the status code or the status code and the port when the redirect is executed.</span></span>

<span data-ttu-id="11494-179">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="11494-179">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="11494-180">将应用`[RequireHttps]`属性设置为所有控制器/Razor 页面不会被视为与需要 HTTPS 全局一样安全。</span><span class="sxs-lookup"><span data-stu-id="11494-180">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="11494-181">不能保证`[RequireHttps]`时添加新的控制器和 Razor 页面应用属性。</span><span class="sxs-lookup"><span data-stu-id="11494-181">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>

## <a name="http-strict-transport-security-protocol-hsts"></a><span data-ttu-id="11494-182">HTTP 严格传输安全协议 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="11494-182">HTTP Strict Transport Security Protocol (HSTS)</span></span>

<span data-ttu-id="11494-183">每个[OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project)， [HTTP 严格传输安全性 (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)是通过响应标头使用的 web 应用指定选择的安全增强功能。</span><span class="sxs-lookup"><span data-stu-id="11494-183">Per [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [HTTP Strict Transport Security (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) is an opt-in security enhancement that's specified by a web app through the use of a response header.</span></span> <span data-ttu-id="11494-184">当[浏览器支持 HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)收到此标头：</span><span class="sxs-lookup"><span data-stu-id="11494-184">When a [browser that supports HSTS](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support) receives this header:</span></span>

* <span data-ttu-id="11494-185">在浏览器将会阻止通过 HTTP 发送的任何通信的域的配置存储。</span><span class="sxs-lookup"><span data-stu-id="11494-185">The browser stores configuration for the domain that prevents sending any communication over HTTP.</span></span> <span data-ttu-id="11494-186">在浏览器强制通过 HTTPS 进行的所有通信。</span><span class="sxs-lookup"><span data-stu-id="11494-186">The browser forces all communication over HTTPS.</span></span>
* <span data-ttu-id="11494-187">在浏览器可防止用户使用不受信任或无效的证书。</span><span class="sxs-lookup"><span data-stu-id="11494-187">The browser prevents the user from using untrusted or invalid certificates.</span></span> <span data-ttu-id="11494-188">在浏览器禁用允许用户暂时信任此证书的提示。</span><span class="sxs-lookup"><span data-stu-id="11494-188">The browser disables prompts that allow a user to temporarily trust such a certificate.</span></span>

<span data-ttu-id="11494-189">因为由客户端强制执行 HSTS 它具有一些限制：</span><span class="sxs-lookup"><span data-stu-id="11494-189">Because HSTS is enforced by the client it has some limitations:</span></span>

* <span data-ttu-id="11494-190">客户端必须支持 HSTS。</span><span class="sxs-lookup"><span data-stu-id="11494-190">The client must support HSTS.</span></span>
* <span data-ttu-id="11494-191">HSTS 要求至少一个成功的 HTTPS 请求能够建立 HSTS 策略。</span><span class="sxs-lookup"><span data-stu-id="11494-191">HSTS requires at least one successful HTTPS request to establish the HSTS policy.</span></span>
* <span data-ttu-id="11494-192">应用程序必须检查每个 HTTP 请求和重定向或拒绝的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="11494-192">The application must check every HTTP request and redirect or reject the HTTP request.</span></span>

<span data-ttu-id="11494-193">ASP.NET Core 2.1 或更高版本实现与 HSTS`UseHsts`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="11494-193">ASP.NET Core 2.1 or later implements HSTS with the `UseHsts` extension method.</span></span> <span data-ttu-id="11494-194">下面的代码调用`UseHsts`时应用不在[开发模式](xref:fundamentals/environments):</span><span class="sxs-lookup"><span data-stu-id="11494-194">The following code calls `UseHsts` when the app isn't in [development mode](xref:fundamentals/environments):</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

<span data-ttu-id="11494-195">`UseHsts` 不建议在开发过程中由于 HSTS 设置高度可缓存的浏览器。</span><span class="sxs-lookup"><span data-stu-id="11494-195">`UseHsts` isn't recommended in development because the HSTS settings are highly cacheable by browsers.</span></span> <span data-ttu-id="11494-196">默认情况下，`UseHsts`排除本地环回地址。</span><span class="sxs-lookup"><span data-stu-id="11494-196">By default, `UseHsts` excludes the local loopback address.</span></span>

<span data-ttu-id="11494-197">对于生产环境首次实现 HTTPS 初始 HSTS 将值设置为较小的值。</span><span class="sxs-lookup"><span data-stu-id="11494-197">For production environments implementing HTTPS for the first time, set the initial HSTS value to a small value.</span></span> <span data-ttu-id="11494-198">设置的值从小时数不超过一天的以防到时需要还原 HTTP 到 HTTPS 基础结构。</span><span class="sxs-lookup"><span data-stu-id="11494-198">Set the value from hours to no more than a single day in case you need to revert the HTTPS infrastructure to HTTP.</span></span> <span data-ttu-id="11494-199">确信 HTTPS 配置的可持续发展中后，增加 HSTS 最大期限值;常用的值为一年。</span><span class="sxs-lookup"><span data-stu-id="11494-199">After you're confident in the sustainability of the HTTPS configuration, increase the HSTS max-age value; a commonly used value is one year.</span></span> 

<span data-ttu-id="11494-200">下面的代码：</span><span class="sxs-lookup"><span data-stu-id="11494-200">The following code:</span></span>

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* <span data-ttu-id="11494-201">设置预加载严格传输安全性标头的参数。</span><span class="sxs-lookup"><span data-stu-id="11494-201">Sets the preload parameter of the Strict-Transport-Security header.</span></span> <span data-ttu-id="11494-202">预加载不属于[RFC HSTS 规范](https://tools.ietf.org/html/rfc6797)，但要预加载 HSTS 站点上执行全新安装的 web 浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="11494-202">Preload isn't part of the [RFC HSTS specification](https://tools.ietf.org/html/rfc6797), but is supported by web browsers to preload HSTS sites on fresh install.</span></span> <span data-ttu-id="11494-203">有关详细信息，请参阅 [https://hstspreload.org/](https://hstspreload.org/)。</span><span class="sxs-lookup"><span data-stu-id="11494-203">See [https://hstspreload.org/](https://hstspreload.org/) for more information.</span></span>
* <span data-ttu-id="11494-204">使[includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2)，这将 HSTS 策略应用到主机的子域。</span><span class="sxs-lookup"><span data-stu-id="11494-204">Enables [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), which applies the HSTS policy to Host subdomains.</span></span>
* <span data-ttu-id="11494-205">显式将严格传输安全性标头的最大期限参数设置为 60 天。</span><span class="sxs-lookup"><span data-stu-id="11494-205">Explicitly sets the max-age parameter of the Strict-Transport-Security header to 60 days.</span></span> <span data-ttu-id="11494-206">如果未设置，默认值为 30 天。</span><span class="sxs-lookup"><span data-stu-id="11494-206">If not set, defaults to 30 days.</span></span> <span data-ttu-id="11494-207">请参阅[最大期限指令](https://tools.ietf.org/html/rfc6797#section-6.1.1)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="11494-207">See the [max-age directive](https://tools.ietf.org/html/rfc6797#section-6.1.1) for more information.</span></span>
* <span data-ttu-id="11494-208">添加`example.com`到主机以排除列表。</span><span class="sxs-lookup"><span data-stu-id="11494-208">Adds `example.com` to the list of hosts to exclude.</span></span>

<span data-ttu-id="11494-209">`UseHsts` 不包括以下环回主机：</span><span class="sxs-lookup"><span data-stu-id="11494-209">`UseHsts` excludes the following loopback hosts:</span></span>

* <span data-ttu-id="11494-210">`localhost` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="11494-210">`localhost` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="11494-211">`127.0.0.1` : IPv4 环回地址。</span><span class="sxs-lookup"><span data-stu-id="11494-211">`127.0.0.1` : The IPv4 loopback address.</span></span>
* <span data-ttu-id="11494-212">`[::1]` : IPv6 环回地址。</span><span class="sxs-lookup"><span data-stu-id="11494-212">`[::1]` : The IPv6 loopback address.</span></span>

<span data-ttu-id="11494-213">前面的示例演示如何添加其他主机。</span><span class="sxs-lookup"><span data-stu-id="11494-213">The preceding example shows how to add additional hosts.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>

## <a name="opt-out-of-httpshsts-on-project-creation"></a><span data-ttu-id="11494-214">选择退出的 HTTPS/HSTS 在项目创建</span><span class="sxs-lookup"><span data-stu-id="11494-214">Opt-out of HTTPS/HSTS on project creation</span></span>

<span data-ttu-id="11494-215">在其中连接安全处理面向公众边缘网络的某些后端服务情况下，无需在每个节点上配置连接安全。</span><span class="sxs-lookup"><span data-stu-id="11494-215">In some backend service scenarios where connection security is handled at the public-facing edge of the network, configuring connection security at each node isn't required.</span></span> <span data-ttu-id="11494-216">Web 应用从 Visual Studio 中或从模板生成[dotnet 新](/dotnet/core/tools/dotnet-new)命令启用[HTTPS 的重定向](#require)并[HSTS](#hsts)。</span><span class="sxs-lookup"><span data-stu-id="11494-216">Web apps generated from the templates in Visual Studio or from the [dotnet new](/dotnet/core/tools/dotnet-new) command enable [HTTPS redirection](#require) and [HSTS](#hsts).</span></span> <span data-ttu-id="11494-217">对于不需要这些方案的部署，你可以选择退出的 HTTPS/HSTS 时从模板创建的应用。</span><span class="sxs-lookup"><span data-stu-id="11494-217">For deployments that don't require these scenarios, you can opt-out of HTTPS/HSTS when the app is created from the template.</span></span>

<span data-ttu-id="11494-218">若要选择退出的 HTTPS/HSTS:</span><span class="sxs-lookup"><span data-stu-id="11494-218">To opt-out of HTTPS/HSTS:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="11494-219">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11494-219">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="11494-220">取消选中**配置为支持 HTTPS**复选框。</span><span class="sxs-lookup"><span data-stu-id="11494-220">Uncheck the **Configure for HTTPS** checkbox.</span></span>

![实体关系图](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="11494-222">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="11494-222">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="11494-223">使用 `--no-https` 选项。</span><span class="sxs-lookup"><span data-stu-id="11494-223">Use the `--no-https` option.</span></span> <span data-ttu-id="11494-224">例如</span><span class="sxs-lookup"><span data-stu-id="11494-224">For example</span></span>

```console
dotnet new webapp --no-https
```

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-set-up-a-developer-certificate-for-docker"></a><span data-ttu-id="11494-225">如何设置适用于 Docker 的开发人员证书</span><span class="sxs-lookup"><span data-stu-id="11494-225">How to set up a developer certificate for Docker</span></span>

<span data-ttu-id="11494-226">请参阅[此 GitHub 问题](https://github.com/aspnet/Docs/issues/6199)。</span><span class="sxs-lookup"><span data-stu-id="11494-226">See [this GitHub issue](https://github.com/aspnet/Docs/issues/6199).</span></span>

::: moniker-end

## <a name="additional-information"></a><span data-ttu-id="11494-227">其他信息</span><span class="sxs-lookup"><span data-stu-id="11494-227">Additional information</span></span>

* [<span data-ttu-id="11494-228">OWASP HSTS 浏览器支持</span><span class="sxs-lookup"><span data-stu-id="11494-228">OWASP HSTS browser support</span></span>](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet#Browser_Support)
