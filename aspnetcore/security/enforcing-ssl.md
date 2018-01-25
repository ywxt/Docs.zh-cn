---
title: "在 ASP.NET Core 应用程序实施 SSL"
author: rick-anderson
description: "演示如何要求在 ASP.NET Core SSL web 应用"
ms.author: riande
manager: wpickett
ms.date: 07/19/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/enforcing-ssl
ms.openlocfilehash: f248e9c0463cf4a46a447a9c896b3276a50f5f08
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="enforcing-ssl-in-an-aspnet-core-app"></a><span data-ttu-id="259eb-103">在 ASP.NET Core 应用程序实施 SSL</span><span class="sxs-lookup"><span data-stu-id="259eb-103">Enforcing SSL in an ASP.NET Core app</span></span>

<span data-ttu-id="259eb-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="259eb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="259eb-105">本文档说明如何：</span><span class="sxs-lookup"><span data-stu-id="259eb-105">This document shows how to:</span></span>

- <span data-ttu-id="259eb-106">要求将 SSL 用于所有请求 （仅适用于 HTTPS 请求）。</span><span class="sxs-lookup"><span data-stu-id="259eb-106">Require SSL for all requests (HTTPS requests only).</span></span>
- <span data-ttu-id="259eb-107">所有 HTTP 请求重都定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="259eb-107">Redirect all HTTP requests to HTTPS.</span></span>

## <a name="require-ssl"></a><span data-ttu-id="259eb-108">要求 SSL</span><span class="sxs-lookup"><span data-stu-id="259eb-108">Require SSL</span></span>

<span data-ttu-id="259eb-109">[RequireHttpsAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute)用于要求 SSL。</span><span class="sxs-lookup"><span data-stu-id="259eb-109">The [RequireHttpsAttribute](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) is used to require SSL.</span></span> <span data-ttu-id="259eb-110">你可以修饰控制器或具有此特性的方法，或可以将其应用全局如下所示：</span><span class="sxs-lookup"><span data-stu-id="259eb-110">You can decorate controllers or methods with this attribute or you can apply it globally as shown below:</span></span>

<span data-ttu-id="259eb-111">以下代码添加到`ConfigureServices`中`Startup`:</span><span class="sxs-lookup"><span data-stu-id="259eb-111">Add the following code to `ConfigureServices` in `Startup`:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-)]

<span data-ttu-id="259eb-112">上面的突出显示的代码需要所有请求都使用`HTTPS`，因此 HTTP 请求将被忽略。</span><span class="sxs-lookup"><span data-stu-id="259eb-112">The highlighted code above requires all requests use `HTTPS`, therefore HTTP requests are ignored.</span></span> <span data-ttu-id="259eb-113">以下突出显示的代码将所有 HTTP 请求重都定向到 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="259eb-113">The following highlighted code redirects all HTTP requests to HTTPS:</span></span>

[!code-csharp[Main](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-)]

<span data-ttu-id="259eb-114">请参阅[URL 重写中间件](xref:fundamentals/url-rewriting)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="259eb-114">See [URL Rewriting Middleware](xref:fundamentals/url-rewriting) for more information.</span></span>

<span data-ttu-id="259eb-115">全局需要 HTTPS (`options.Filters.Add(new RequireHttpsAttribute());`) 是最佳安全方案。</span><span class="sxs-lookup"><span data-stu-id="259eb-115">Requiring HTTPS globally (`options.Filters.Add(new RequireHttpsAttribute());`) is a security best practice.</span></span> <span data-ttu-id="259eb-116">应用`[RequireHttps]`特性应用到所有控制器不会被视为尽可能安全全局需要 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="259eb-116">Applying the `[RequireHttps]` attribute to all controller isn't considered as secure as requiring HTTPS globally.</span></span> <span data-ttu-id="259eb-117">你不能保证新控制器添加到你的应用程序将记住应用`[RequireHttps]`属性。</span><span class="sxs-lookup"><span data-stu-id="259eb-117">You can't guarantee new controllers added to your app will remember to apply the `[RequireHttps]` attribute.</span></span>
