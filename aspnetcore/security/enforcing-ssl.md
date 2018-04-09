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
ms.openlocfilehash: 2ebb975e1ea17698cee13ca00d3f5df4a5135e38
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="enforce-https-in-an-aspnet-core"></a><span data-ttu-id="0e1f7-103">强制实施 HTTPS 在 ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="0e1f7-103">Enforce HTTPS in an ASP.NET Core</span></span>

<span data-ttu-id="0e1f7-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0e1f7-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0e1f7-105">本文档说明如何：</span><span class="sxs-lookup"><span data-stu-id="0e1f7-105">This document shows how to:</span></span>

- <span data-ttu-id="0e1f7-106">所有请求需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-106">Require HTTPS for all requests.</span></span>
- <span data-ttu-id="0e1f7-107">所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-107">Redirect all HTTP requests to HTTPS.</span></span>

> [!WARNING]
> <span data-ttu-id="0e1f7-108">执行**不**使用`RequireHttpsAttribute`接收敏感信息的 Web api。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-108">Do **not** use `RequireHttpsAttribute` on Web APIs that receive sensitive information.</span></span> <span data-ttu-id="0e1f7-109">`RequireHttpsAttribute` 使用 HTTP 状态代码将从 HTTP 到 HTTPS 的浏览器重定向。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-109">`RequireHttpsAttribute` uses HTTP status codes to redirect browsers from HTTP to HTTPS.</span></span> <span data-ttu-id="0e1f7-110">API 客户端可能无法理解或遵循从 HTTP 到 HTTPS 的重定向。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-110">API clients may not understand or obey redirects from HTTP to HTTPS.</span></span> <span data-ttu-id="0e1f7-111">此类客户端可能会通过 HTTP 发送信息。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-111">Such clients may send information over HTTP.</span></span> <span data-ttu-id="0e1f7-112">Web Api 应具有下列任一：</span><span class="sxs-lookup"><span data-stu-id="0e1f7-112">Web APIs should either:</span></span>
>
>* <span data-ttu-id="0e1f7-113">不在 HTTP 上侦听。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-113">Not listen on HTTP.</span></span>
>* <span data-ttu-id="0e1f7-114">关闭与状态代码 400 （错误请求） 的连接并不为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-114">Close the connection with status code 400 (Bad Request) and not serve the request.</span></span>

## <a name="require-https"></a><span data-ttu-id="0e1f7-115">需要 HTTPS</span><span class="sxs-lookup"><span data-stu-id="0e1f7-115">Require HTTPS</span></span>

<span data-ttu-id="0e1f7-116">[RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute)用于需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-116">The [RequireHttpsAttribute](/dotnet/api/Microsoft.AspNetCore.Mvc.RequireHttpsAttribute) is used to require HTTPS.</span></span> <span data-ttu-id="0e1f7-117">`[RequireHttpsAttribute]` 可修饰控制器或方法，或可以全局应用。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-117">`[RequireHttpsAttribute]` can decorate controllers or methods, or can be applied globally.</span></span> <span data-ttu-id="0e1f7-118">若要全局应用该属性，以下代码添加到`ConfigureServices`中`Startup`:</span><span class="sxs-lookup"><span data-stu-id="0e1f7-118">To apply the attribute globally, add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

<span data-ttu-id="0e1f7-119">前面的突出显示的代码中需要的所有请求都使用`HTTPS`; 因此，HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-119">The preceding highlighted code requires all requests use `HTTPS`; therefore, HTTP requests are ignored.</span></span> <span data-ttu-id="0e1f7-120">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="0e1f7-120">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

<span data-ttu-id="0e1f7-121">有关详细信息，请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-121">For more information, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span>

<span data-ttu-id="0e1f7-122">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-122">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="0e1f7-123">应用`[RequireHttps]`特性应用到所有控制器/Razor 页面不会被视为尽可能安全全局需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-123">Applying the `[RequireHttps]` attribute to all controllers/Razor Pages isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="0e1f7-124">你不能保证`[RequireHttps]`添加新控制器和 Razor 页时应用特性。</span><span class="sxs-lookup"><span data-stu-id="0e1f7-124">You can't guarantee the `[RequireHttps]` attribute is applied when new controllers and Razor Pages are added.</span></span>
