---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: 阻止 ASP.NET Web API 中的跨网站请求伪造 (CSRF) 攻击 |Microsoft 文档
author: MikeWasson
description: 描述跨网站请求伪造 (CSRF) 攻击以及如何在 ASP.NET Web API 中实现反 CSRF 度量值。
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5e7b24c697e0bb37f388341abd89609c76f6b64c
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961232"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a><span data-ttu-id="93a0f-103">阻止 ASP.NET Web API 中的跨网站请求伪造 (CSRF) 攻击</span><span class="sxs-lookup"><span data-stu-id="93a0f-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>
====================
<span data-ttu-id="93a0f-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="93a0f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="93a0f-105">跨站点请求伪造 (CSRF) 是一种攻击，恶意网站将请求发送到在当前登录用户的易受攻击站点的其中</span><span class="sxs-lookup"><span data-stu-id="93a0f-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="93a0f-106">下面是 CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="93a0f-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="93a0f-107">用户登录到`www.example.com`使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="93a0f-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="93a0f-108">服务器对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="93a0f-108">The server authenticates the user.</span></span> <span data-ttu-id="93a0f-109">来自服务器的响应包括身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="93a0f-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="93a0f-110">且无需注销，用户访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="93a0f-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="93a0f-111">此恶意站点包含的以下 HTML 窗体：</span><span class="sxs-lookup"><span data-stu-id="93a0f-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="93a0f-112">请注意，窗体操作发送到易受攻击的站点，不适用于恶意站点。</span><span class="sxs-lookup"><span data-stu-id="93a0f-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="93a0f-113">这是 CSRF 的"跨站点"部分。</span><span class="sxs-lookup"><span data-stu-id="93a0f-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="93a0f-114">用户可单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="93a0f-114">The user clicks the submit button.</span></span> <span data-ttu-id="93a0f-115">浏览器包括与请求的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="93a0f-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="93a0f-116">请求与用户的身份验证上下文，在服务器上运行，并可以执行任何身份验证的用户可以执行的操作。</span><span class="sxs-lookup"><span data-stu-id="93a0f-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="93a0f-117">虽然此示例需要用户单击窗体按钮，恶意页差不多一样轻松地运行自动提交该表单的脚本。</span><span class="sxs-lookup"><span data-stu-id="93a0f-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="93a0f-118">此外，使用 SSL 不会阻止 CSRF 攻击中，因为恶意站点可以发送"https://"请求。</span><span class="sxs-lookup"><span data-stu-id="93a0f-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="93a0f-119">通常情况下，CSRF 攻击是可能对网站进行身份验证，使用 cookie 的因为浏览器向目标网站发送所有相关 cookie。</span><span class="sxs-lookup"><span data-stu-id="93a0f-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="93a0f-120">但是，CSRF 攻击并不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="93a0f-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="93a0f-121">例如，基本和摘要式身份验证也是易受攻击的。</span><span class="sxs-lookup"><span data-stu-id="93a0f-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="93a0f-122">之后使用基本或摘要式身份验证的用户登录。</span><span class="sxs-lookup"><span data-stu-id="93a0f-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="93a0f-123">浏览器会自动发送凭据，直到会话结束。</span><span class="sxs-lookup"><span data-stu-id="93a0f-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="93a0f-124">防伪令牌</span><span class="sxs-lookup"><span data-stu-id="93a0f-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="93a0f-125">为了帮助防止 CSRF 攻击，ASP.NET MVC 使用防伪令牌，也称为*请求验证令牌*。</span><span class="sxs-lookup"><span data-stu-id="93a0f-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="93a0f-126">客户端请求一个包含窗体的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="93a0f-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="93a0f-127">服务器在响应中包含两个令牌。</span><span class="sxs-lookup"><span data-stu-id="93a0f-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="93a0f-128">一个标记是作为 cookie 发送。</span><span class="sxs-lookup"><span data-stu-id="93a0f-128">One token is sent as a cookie.</span></span> <span data-ttu-id="93a0f-129">其他放置在隐藏的表单字段中。</span><span class="sxs-lookup"><span data-stu-id="93a0f-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="93a0f-130">以便攻击者无法猜测值，将随机生成令牌。</span><span class="sxs-lookup"><span data-stu-id="93a0f-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="93a0f-131">当客户端提交表单时，它必须发送两种令牌返回到服务器。</span><span class="sxs-lookup"><span data-stu-id="93a0f-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="93a0f-132">客户端发送的 cookie 令牌作为 cookie，然后发送窗体数据内的窗体标记。</span><span class="sxs-lookup"><span data-stu-id="93a0f-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="93a0f-133">（浏览器客户端会自动完成此用户提交表单时。）</span><span class="sxs-lookup"><span data-stu-id="93a0f-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="93a0f-134">如果请求不包括两种令牌，服务器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="93a0f-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="93a0f-135">下面是与隐藏的表单令牌以 HTML 形式的示例：</span><span class="sxs-lookup"><span data-stu-id="93a0f-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="93a0f-136">防伪令牌，因为恶意页无法读取用户的令牌，由于同源策略工作。</span><span class="sxs-lookup"><span data-stu-id="93a0f-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="93a0f-137">([同源策略](http://www.w3.org/Security/wiki/Same_Origin_Policy)阻止访问彼此的内容的两个不同站点上托管的文档。</span><span class="sxs-lookup"><span data-stu-id="93a0f-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="93a0f-138">因此，在前面的示例中，恶意的页可以将请求发送到 example.com，但它无法读取响应。）</span><span class="sxs-lookup"><span data-stu-id="93a0f-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="93a0f-139">若要阻止 CSRF 攻击，请使用任何身份验证协议使用防伪令牌由浏览器以无提示方式发送凭据后在用户登录。</span><span class="sxs-lookup"><span data-stu-id="93a0f-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="93a0f-140">这包括基于 cookie 的身份验证协议，例如窗体身份验证，以及等基本和摘要式身份验证协议。</span><span class="sxs-lookup"><span data-stu-id="93a0f-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="93a0f-141">你应要求防伪令牌将用于任何 nonsafe 方法 （POST、 PUT、 DELETE）。</span><span class="sxs-lookup"><span data-stu-id="93a0f-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="93a0f-142">此外，请确保安全的方法 （GET、 HEAD） 没有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="93a0f-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="93a0f-143">此外，如果您启用跨域支持，如 CORS 或 JSONP，则 GET 等甚至安全方法都可能容易受到 CSRF 攻击，从而允许攻击者能够读取可能敏感的数据。</span><span class="sxs-lookup"><span data-stu-id="93a0f-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="93a0f-144">ASP.NET mvc 防伪令牌</span><span class="sxs-lookup"><span data-stu-id="93a0f-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="93a0f-145">若要将防伪令牌添加到 Razor 页中，使用**HtmlHelper.AntiForgeryToken**帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="93a0f-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="93a0f-146">此方法添加隐藏的表单字段，并且还设置 cookie 的标记。</span><span class="sxs-lookup"><span data-stu-id="93a0f-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="93a0f-147">反 CSRF 和 AJAX</span><span class="sxs-lookup"><span data-stu-id="93a0f-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="93a0f-148">窗体标记可能 AJAX 请求的问题，因为 AJAX 请求可能会发送 JSON 数据，不 HTML 窗体数据。</span><span class="sxs-lookup"><span data-stu-id="93a0f-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="93a0f-149">一种解决方案是将令牌发送自定义的 HTTP 标头中。</span><span class="sxs-lookup"><span data-stu-id="93a0f-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="93a0f-150">下面的代码使用 Razor 语法生成令牌，，然后将令牌添加到 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="93a0f-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="93a0f-151">在服务器通过调用生成令牌**AntiForgery.GetTokens**。</span><span class="sxs-lookup"><span data-stu-id="93a0f-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="93a0f-152">处理请求时，请从请求标头中提取令牌。</span><span class="sxs-lookup"><span data-stu-id="93a0f-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="93a0f-153">然后调用**AntiForgery.Validate**方法来验证令牌。</span><span class="sxs-lookup"><span data-stu-id="93a0f-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="93a0f-154">**验证**方法引发异常，如果令牌无效。</span><span class="sxs-lookup"><span data-stu-id="93a0f-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
