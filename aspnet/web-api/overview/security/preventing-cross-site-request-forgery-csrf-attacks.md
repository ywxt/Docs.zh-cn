---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 防止 ASP.NET Web API 中的跨站点请求伪造 (CSRF) 攻击 |Microsoft Docs
author: MikeWasson
description: 介绍跨站点请求伪造 (CSRF) 攻击以及如何在 ASP.NET Web API 中实施反 CSRF 度量值。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 7dfddf09a1577cfa7a52f58b37533724a8475435
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379862"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a><span data-ttu-id="a6aec-103">防止 ASP.NET Web API 中的跨站点请求伪造 (CSRF) 攻击</span><span class="sxs-lookup"><span data-stu-id="a6aec-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>
====================
<span data-ttu-id="a6aec-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a6aec-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a6aec-105">跨站点请求伪造 (CSRF) 是一种攻击，恶意站点发送请求到易受攻击的站点在当前登录用户</span><span class="sxs-lookup"><span data-stu-id="a6aec-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="a6aec-106">下面是 CSRF 攻击的一个例子：</span><span class="sxs-lookup"><span data-stu-id="a6aec-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="a6aec-107">用户登录到`www.example.com`使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6aec-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="a6aec-108">服务器对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6aec-108">The server authenticates the user.</span></span> <span data-ttu-id="a6aec-109">从服务器响应包括身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="a6aec-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="a6aec-110">而无需注销，用户访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="a6aec-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="a6aec-111">此恶意站点包含以下 HTML 窗体：</span><span class="sxs-lookup"><span data-stu-id="a6aec-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="a6aec-112">请注意，窗体操作发到易受攻击的站点，不到的恶意站点。</span><span class="sxs-lookup"><span data-stu-id="a6aec-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="a6aec-113">这是 CSRF 的"跨站点"部分。</span><span class="sxs-lookup"><span data-stu-id="a6aec-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="a6aec-114">用户单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="a6aec-114">The user clicks the submit button.</span></span> <span data-ttu-id="a6aec-115">在浏览器包括与请求的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="a6aec-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="a6aec-116">请求与用户的身份验证上下文，在服务器上运行，并可以执行任何操作允许身份验证的用户执行的操作。</span><span class="sxs-lookup"><span data-stu-id="a6aec-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="a6aec-117">虽然此示例需要用户单击窗体按钮，但恶意页面可以同样轻松地运行自动提交窗体的脚本。</span><span class="sxs-lookup"><span data-stu-id="a6aec-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="a6aec-118">此外，使用 SSL 不会阻止实施 CSRF 攻击，因为恶意站点可以发送"https://"请求。</span><span class="sxs-lookup"><span data-stu-id="a6aec-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="a6aec-119">通常情况下，CSRF 攻击是可能对网站使用 cookie 进行身份验证，因为浏览器向目标网站发送所有相关 cookie。</span><span class="sxs-lookup"><span data-stu-id="a6aec-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="a6aec-120">但是，CSRF 攻击并不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="a6aec-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="a6aec-121">例如，基本和摘要式身份验证也是易受攻击的。</span><span class="sxs-lookup"><span data-stu-id="a6aec-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="a6aec-122">之后使用基本或摘要式身份验证用户登录。</span><span class="sxs-lookup"><span data-stu-id="a6aec-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="a6aec-123">浏览器自动发送凭据，直到会话结束。</span><span class="sxs-lookup"><span data-stu-id="a6aec-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="a6aec-124">防伪标记</span><span class="sxs-lookup"><span data-stu-id="a6aec-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="a6aec-125">为了帮助防止 CSRF 攻击，ASP.NET MVC 使用防伪令牌，也称为*请求验证令牌*。</span><span class="sxs-lookup"><span data-stu-id="a6aec-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="a6aec-126">客户端请求包含一个窗体的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="a6aec-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="a6aec-127">服务器在响应中包含两个令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="a6aec-128">一个令牌作为 cookie 发送。</span><span class="sxs-lookup"><span data-stu-id="a6aec-128">One token is sent as a cookie.</span></span> <span data-ttu-id="a6aec-129">其他放置在隐藏窗体字段中。</span><span class="sxs-lookup"><span data-stu-id="a6aec-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="a6aec-130">因此，攻击者无法猜测值，将随机生成令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="a6aec-131">时客户端提交窗体，它必须将这两个令牌发送回服务器。</span><span class="sxs-lookup"><span data-stu-id="a6aec-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="a6aec-132">客户端发送的 cookie 令牌作为 cookie，然后发送窗体数据中的窗体令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="a6aec-133">（浏览器客户端自动执行此要求在用户提交窗体时。）</span><span class="sxs-lookup"><span data-stu-id="a6aec-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="a6aec-134">如果请求不包含这两个令牌，该服务器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="a6aec-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="a6aec-135">下面是使用隐藏的窗体标记 HTML 窗体的示例：</span><span class="sxs-lookup"><span data-stu-id="a6aec-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="a6aec-136">防伪标记起作用，因为恶意页面无法读取用户的令牌，由同域策略引起。</span><span class="sxs-lookup"><span data-stu-id="a6aec-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="a6aec-137">([同域策略](http://www.w3.org/Security/wiki/Same_Origin_Policy)阻止访问彼此的内容的两个不同的站点上托管的文档。</span><span class="sxs-lookup"><span data-stu-id="a6aec-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="a6aec-138">因此在前面的示例中，恶意页可以将请求发送到 example.com，但它无法读取响应。）</span><span class="sxs-lookup"><span data-stu-id="a6aec-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="a6aec-139">若要防止 CSRF 攻击，浏览器以无提示方式发送使用任何身份验证协议使用防伪标记提供凭据后在用户登录。</span><span class="sxs-lookup"><span data-stu-id="a6aec-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="a6aec-140">这包括基于 cookie 的身份验证协议，如窗体身份验证，以及协议，例如基本和摘要式身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6aec-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="a6aec-141">对于任何 nonsafe 方法 （POST、 PUT、 DELETE），应要求防伪令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="a6aec-142">此外，请确保安全方法 （GET、 HEAD） 没有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="a6aec-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="a6aec-143">此外，如果启用跨域支持，如 CORS 或 JSONP，甚至安全方法，如 GET 则可能容易受到 CSRF 攻击，从而允许攻击者能够读取可能敏感的数据。</span><span class="sxs-lookup"><span data-stu-id="a6aec-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="a6aec-144">在 ASP.NET MVC 中的防伪标记</span><span class="sxs-lookup"><span data-stu-id="a6aec-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="a6aec-145">若要将防伪标记添加到 Razor 页面，请使用**HtmlHelper.AntiForgeryToken**帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="a6aec-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="a6aec-146">此方法将添加隐藏窗体字段，还会设置 cookie 令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="a6aec-147">反 CSRF 和 AJAX</span><span class="sxs-lookup"><span data-stu-id="a6aec-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="a6aec-148">窗体令牌可能对 AJAX 请求问题，因为 AJAX 请求可能会发送 JSON 数据，不是 HTML 窗体数据。</span><span class="sxs-lookup"><span data-stu-id="a6aec-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="a6aec-149">一种解决方案是将令牌发送自定义 HTTP 标头中。</span><span class="sxs-lookup"><span data-stu-id="a6aec-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="a6aec-150">下面的代码使用 Razor 语法生成令牌，，然后将令牌添加到 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="a6aec-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="a6aec-151">在服务器中通过调用生成令牌**AntiForgery.GetTokens**。</span><span class="sxs-lookup"><span data-stu-id="a6aec-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="a6aec-152">当处理该请求时，从请求标头中提取令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="a6aec-153">然后调用**AntiForgery.Validate**方法用于验证令牌。</span><span class="sxs-lookup"><span data-stu-id="a6aec-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="a6aec-154">**验证**方法将引发异常，如果令牌无效。</span><span class="sxs-lookup"><span data-stu-id="a6aec-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
