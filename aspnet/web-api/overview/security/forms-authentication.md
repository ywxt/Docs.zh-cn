---
uid: web-api/overview/security/forms-authentication
title: 在 ASP.NET Web API 中窗体身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用窗体身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 7642a30816a04a88a25ef8bf4f01e766fda362ce
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365066"
---
<a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="a1f3c-103">ASP.NET Web API 中的窗体身份验证</span><span class="sxs-lookup"><span data-stu-id="a1f3c-103">Forms Authentication in ASP.NET Web API</span></span>
====================
<span data-ttu-id="a1f3c-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a1f3c-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a1f3c-105">窗体身份验证使用 HTML 窗体向服务器发送用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="a1f3c-106">它不是一种 Internet 标准。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-106">It is not an Internet standard.</span></span> <span data-ttu-id="a1f3c-107">窗体身份验证是仅适用于 web 的 web 应用，从调用的 Api，以便用户可以与 HTML 窗体进行交互。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="a1f3c-108">优点</span><span class="sxs-lookup"><span data-stu-id="a1f3c-108">Advantages</span></span> | <span data-ttu-id="a1f3c-109">缺点</span><span class="sxs-lookup"><span data-stu-id="a1f3c-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="a1f3c-110">-可轻松实现： 内置到 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="a1f3c-111">-使用 ASP.NET 成员资格提供程序，可以轻松管理用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="a1f3c-112">-未一个标准的 HTTP 身份验证机制;使用 HTTP cookie 而不是标准授权标头。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="a1f3c-113">-需要浏览器客户端。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-113">- Requires a browser client.</span></span> <span data-ttu-id="a1f3c-114">的以纯文本形式发送凭据。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="a1f3c-115">-易受到跨站点请求伪造 (CSRF);需要反 CSRF 的度量值。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="a1f3c-116">-难以 nonbrowser 客户端配合使用。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="a1f3c-117">登录要求浏览器。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-117">Login requires a browser.</span></span> <span data-ttu-id="a1f3c-118">的在请求中发送用户凭据。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="a1f3c-119">-某些用户禁用 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="a1f3c-120">简单地说，在 ASP.NET 中的窗体身份验证的工作方式如下：</span><span class="sxs-lookup"><span data-stu-id="a1f3c-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="a1f3c-121">客户端请求需要身份验证的资源。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="a1f3c-122">如果用户未经过身份验证，服务器将返回 HTTP 302 （已找到），并将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="a1f3c-123">用户输入凭据，并提交窗体。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="a1f3c-124">服务器将返回另一个 HTTP 302 重定向回原始的 URI。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="a1f3c-125">此响应包括身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="a1f3c-126">客户端再次请求该资源。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-126">The client requests the resource again.</span></span> <span data-ttu-id="a1f3c-127">请求包含身份验证 cookie，因此服务器授予请求。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="a1f3c-128">有关详细信息，请参阅[概述的窗体身份验证。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a1f3c-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="a1f3c-129">将窗体身份验证用于 Web API</span><span class="sxs-lookup"><span data-stu-id="a1f3c-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="a1f3c-130">若要创建使用窗体身份验证的应用程序，请在 MVC 4 项目向导中选择"Internet 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="a1f3c-131">此模板创建 MVC 控制器用于帐户管理。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="a1f3c-132">此外可以使用"单页面应用程序"模板，在 ASP.NET Fall 2012 Update 中可用。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="a1f3c-133">在你的 web API 控制器，你可以通过使用限制访问`[Authorize]`属性，如中所述[使用 [Authorize] 特性](authentication-and-authorization-in-aspnet-web-api.md#auth3)。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="a1f3c-134">窗体身份验证使用会话 cookie 进行身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="a1f3c-135">浏览器自动向目标网站发送所有相关 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="a1f3c-136">此功能使窗体身份验证可能易受到跨站点请求伪造 (CSRF) 攻击，请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="a1f3c-137">窗体身份验证不会加密用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="a1f3c-138">因此，不使用 SSL 安全窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="a1f3c-139">请参阅[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
