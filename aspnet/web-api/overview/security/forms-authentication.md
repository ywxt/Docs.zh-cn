---
uid: web-api/overview/security/forms-authentication
title: 在 ASP.NET Web API 中窗体身份验证 |Microsoft 文档
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用 Forms 身份验证。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 9027d76bcf8854fc85f11906d3651511f350cd32
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508306"
---
<a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="a1ab1-103">ASP.NET Web API 中的窗体身份验证</span><span class="sxs-lookup"><span data-stu-id="a1ab1-103">Forms Authentication in ASP.NET Web API</span></span>
====================
<span data-ttu-id="a1ab1-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a1ab1-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a1ab1-105">窗体身份验证使用 HTML 窗体向服务器发送用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="a1ab1-106">它不是一种 Internet 标准。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-106">It is not an Internet standard.</span></span> <span data-ttu-id="a1ab1-107">窗体身份验证才适用于 web 从 web 应用程序，调用的 Api，以便用户可以与 HTML 窗体进行交互。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="a1ab1-108">优点</span><span class="sxs-lookup"><span data-stu-id="a1ab1-108">Advantages</span></span> | <span data-ttu-id="a1ab1-109">缺点</span><span class="sxs-lookup"><span data-stu-id="a1ab1-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="a1ab1-110">-容易实现： 内置于 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="a1ab1-111">-使用 ASP.NET 成员资格提供程序，这样，就更容易地管理用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="a1ab1-112">-不标准的 HTTP 身份验证机制;使用 HTTP cookie，而不是标准的 Authorization 标头。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="a1ab1-113">-需要浏览器客户端。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-113">- Requires a browser client.</span></span> <span data-ttu-id="a1ab1-114">的以纯文本形式发送凭据。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="a1ab1-115">-容易受到跨网站请求伪造 (CSRF);需要反 CSRF 度量值。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="a1ab1-116">-从 nonbrowser 客户端使用困难。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="a1ab1-117">登录名需要浏览器。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-117">Login requires a browser.</span></span> <span data-ttu-id="a1ab1-118">用户凭据在请求中发送。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="a1ab1-119">-某些用户禁用 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="a1ab1-120">简而言之，在 ASP.NET 中的窗体身份验证工作原理如下：</span><span class="sxs-lookup"><span data-stu-id="a1ab1-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="a1ab1-121">客户端请求需要身份验证的资源。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="a1ab1-122">如果用户未通过身份验证，服务器将返回 HTTP 302 （找到），而将重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="a1ab1-123">用户输入凭据，并提交该表单。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="a1ab1-124">服务器返回另一个重定向回原始的 URI 的 HTTP 302。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="a1ab1-125">此响应包含的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="a1ab1-126">客户端再次请求资源。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-126">The client requests the resource again.</span></span> <span data-ttu-id="a1ab1-127">请求包括身份验证 cookie，因此服务器授予请求。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="a1ab1-128">有关详细信息，请参阅[概述的窗体身份验证。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="a1ab1-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="a1ab1-129">使用 Web API 的窗体身份验证</span><span class="sxs-lookup"><span data-stu-id="a1ab1-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="a1ab1-130">若要创建使用窗体身份验证的应用程序，请在 MVC 4 项目向导中选择"Internet 应用程序"模板。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="a1ab1-131">此模板创建 MVC 控制器用于帐户管理。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="a1ab1-132">你还可以使用"单页面应用程序"模板，在 ASP.NET 秋季 2012年更新中提供。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="a1ab1-133">在你的 web API 控制器，你可以通过使用限制访问`[Authorize]`特性，如中所述[使用 [Authorize] 属性](authentication-and-authorization-in-aspnet-web-api.md#auth3)。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="a1ab1-134">窗体身份验证使用的会话 cookie 请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="a1ab1-135">浏览器自动向目标网站发送所有相关 cookie。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="a1ab1-136">此功能使窗体身份验证可能易受到跨站点请求伪造 (CSRF) 攻击，请参阅[防止跨站点请求伪造 (CSRF) 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="a1ab1-137">窗体身份验证不加密用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="a1ab1-138">因此，不安全的除非用于 SSL 窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="a1ab1-139">请参阅[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ab1-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
