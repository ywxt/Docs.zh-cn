---
title: 在 ASP.NET Core 防止跨站点请求伪造 (XSRF/CSRF) 攻击
author: steve-smith
description: 了解如何防止对恶意网站可能会影响客户端浏览器和应用程序之间的交互的 web 应用的攻击。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/19/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: 3bca96f4a2e247eeeb93140df93221371d88d4d3
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341855"
---
# <a name="prevent-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a><span data-ttu-id="9a58c-103">在 ASP.NET Core 防止跨站点请求伪造 (XSRF/CSRF) 攻击</span><span class="sxs-lookup"><span data-stu-id="9a58c-103">Prevent Cross-Site Request Forgery (XSRF/CSRF) attacks in ASP.NET Core</span></span>

<span data-ttu-id="9a58c-104">通过[Steve Smith](https://ardalis.com/)， [Fiyaz Hasan](https://twitter.com/FiyazBinHasan)，和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9a58c-104">By [Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9a58c-105">跨站点请求伪造 (也称为 XSRF 或 CSRF，发音 *，请参阅冲浪*) 是针对恶意网站凭此可以影响客户端浏览器和信任，一个 web 应用程序之间的交互的 web 承载的应用程序的攻击浏览器。</span><span class="sxs-lookup"><span data-stu-id="9a58c-105">Cross-site request forgery (also known as XSRF or CSRF, pronounced *see-surf*) is an attack against web-hosted apps whereby a malicious web app can influence the interaction between a client browser and a web app that trusts that browser.</span></span> <span data-ttu-id="9a58c-106">这些攻击是可能的因为 web 浏览器将自动与每个请求某些类型的身份验证令牌发送到网站。</span><span class="sxs-lookup"><span data-stu-id="9a58c-106">These attacks are possible because web browsers send some types of authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="9a58c-107">这种形式的攻击也称为是*一键式攻击*或*会话乘坐*因为攻击充分利用用户的先前进行身份验证会话。</span><span class="sxs-lookup"><span data-stu-id="9a58c-107">This form of exploit is also known as a *one-click attack* or *session riding* because the attack takes advantage of the user's previously authenticated session.</span></span>

<span data-ttu-id="9a58c-108">CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="9a58c-108">An example of a CSRF attack:</span></span>

1. <span data-ttu-id="9a58c-109">用户登录到`www.good-banking-site.com`使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="9a58c-109">A user signs into `www.good-banking-site.com` using forms authentication.</span></span> <span data-ttu-id="9a58c-110">服务器对用户进行身份验证，并发出包含身份验证 cookie 的响应。</span><span class="sxs-lookup"><span data-stu-id="9a58c-110">The server authenticates the user and issues a response that includes an authentication cookie.</span></span> <span data-ttu-id="9a58c-111">该站点处于易受到攻击，因为它信任的任何请求都收到与有效的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-111">The site is vulnerable to attack because it trusts any request that it receives with a valid authentication cookie.</span></span>
1. <span data-ttu-id="9a58c-112">用户访问恶意站点， `www.bad-crook-site.com`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-112">The user visits a malicious site, `www.bad-crook-site.com`.</span></span>

   <span data-ttu-id="9a58c-113">恶意站点， `www.bad-crook-site.com`，包含类似于以下的 HTML 窗体：</span><span class="sxs-lookup"><span data-stu-id="9a58c-113">The malicious site, `www.bad-crook-site.com`, contains an HTML form similar to the following:</span></span>

   ```html
   <h1>Congratulations! You're a Winner!</h1>
   <form action="http://good-banking-site.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw">
       <input type="hidden" name="Amount" value="1000000">
       <input type="submit" value="Click to collect your prize!">
   </form>
   ```

   <span data-ttu-id="9a58c-114">请注意，窗体的`action`文章到易受攻击的站点上，而不是恶意的站点。</span><span class="sxs-lookup"><span data-stu-id="9a58c-114">Notice that the form's `action` posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="9a58c-115">这是 CSRF 的"跨站点"部分。</span><span class="sxs-lookup"><span data-stu-id="9a58c-115">This is the "cross-site" part of CSRF.</span></span>

1. <span data-ttu-id="9a58c-116">用户选择提交按钮。</span><span class="sxs-lookup"><span data-stu-id="9a58c-116">The user selects the submit button.</span></span> <span data-ttu-id="9a58c-117">浏览器发出请求，并自动将请求的域中，身份验证 cookie `www.good-banking-site.com`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-117">The browser makes the request and automatically includes the authentication cookie for the requested domain, `www.good-banking-site.com`.</span></span>
1. <span data-ttu-id="9a58c-118">在上运行的请求`www.good-banking-site.com`与用户的身份验证上下文的服务器，并且可以执行允许经过身份验证的用户执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="9a58c-118">The request runs on the `www.good-banking-site.com` server with the user's authentication context and can perform any action that an authenticated user is allowed to perform.</span></span>

<span data-ttu-id="9a58c-119">除了其中用户选择按钮以提交该表单的方案中，恶意的站点无法：</span><span class="sxs-lookup"><span data-stu-id="9a58c-119">In addition to the scenario where the user selects the button to submit the form, the malicious site could:</span></span>

* <span data-ttu-id="9a58c-120">运行自动提交该表单的脚本。</span><span class="sxs-lookup"><span data-stu-id="9a58c-120">Run a script that automatically submits the form.</span></span>
* <span data-ttu-id="9a58c-121">将窗体提交作为 AJAX 请求中发送。</span><span class="sxs-lookup"><span data-stu-id="9a58c-121">Send the form submission as an AJAX request.</span></span>
* <span data-ttu-id="9a58c-122">隐藏使用 CSS 窗体。</span><span class="sxs-lookup"><span data-stu-id="9a58c-122">Hide the form using CSS.</span></span>

<span data-ttu-id="9a58c-123">这些备用方案无需任何操作或从用户而不是最初访问恶意网站的输入。</span><span class="sxs-lookup"><span data-stu-id="9a58c-123">These alternative scenarios don't require any action or input from the user other than initially visiting the malicious site.</span></span>

<span data-ttu-id="9a58c-124">使用 HTTPS，则不会阻止 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="9a58c-124">Using HTTPS doesn't prevent a CSRF attack.</span></span> <span data-ttu-id="9a58c-125">恶意站点可以将发送`https://www.good-banking-site.com/`请求一样轻松它可发送的不安全的请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-125">The malicious site can send an `https://www.good-banking-site.com/` request just as easily as it can send an insecure request.</span></span>

<span data-ttu-id="9a58c-126">一些攻击目标响应 GET 请求的终结点，在这种情况下使用的图像标记要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="9a58c-126">Some attacks target endpoints that respond to GET requests, in which case an image tag can be used to perform the action.</span></span> <span data-ttu-id="9a58c-127">允许映像但阻止 JavaScript 的论坛站点上，这种攻击十分常见。</span><span class="sxs-lookup"><span data-stu-id="9a58c-127">This form of attack is common on forum sites that permit images but block JavaScript.</span></span> <span data-ttu-id="9a58c-128">应用程序更改的状态 GET 请求中，在其中修改变量或资源，就很容易遭受恶意攻击。</span><span class="sxs-lookup"><span data-stu-id="9a58c-128">Apps that change state on GET requests, where variables or resources are altered, are vulnerable to malicious attacks.</span></span> <span data-ttu-id="9a58c-129">**更改状态的 GET 请求是不安全的。最佳做法是永远不会更改在 GET 请求的状态。**</span><span class="sxs-lookup"><span data-stu-id="9a58c-129">**GET requests that change state are insecure. A best practice is to never change state on a GET request.**</span></span>

<span data-ttu-id="9a58c-130">针对 web 应用可用于身份验证的 cookie，因为可能会出现 CSRF 攻击：</span><span class="sxs-lookup"><span data-stu-id="9a58c-130">CSRF attacks are possible against web apps that use cookies for authentication because:</span></span>

* <span data-ttu-id="9a58c-131">浏览器存储颁发的 web 应用的 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-131">Browsers store cookies issued by a web app.</span></span>
* <span data-ttu-id="9a58c-132">存储的 cookie 包括用于身份验证的用户的会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-132">Stored cookies include session cookies for authenticated users.</span></span>
* <span data-ttu-id="9a58c-133">浏览器发送的所有 cookie 与域关联到 web 应用程序而不考虑如何向应用程序请求生成浏览器中的每个请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-133">Browsers send all of the cookies associated with a domain to the web app every request regardless of how the request to app was generated within the browser.</span></span>

<span data-ttu-id="9a58c-134">但是，CSRF 攻击不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-134">However, CSRF attacks aren't limited to exploiting cookies.</span></span> <span data-ttu-id="9a58c-135">例如，基本和摘要式身份验证也是易受攻击的。</span><span class="sxs-lookup"><span data-stu-id="9a58c-135">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="9a58c-136">浏览器使用基本或摘要式身份验证的用户登录后，直到会话才会自动发送凭据&dagger;结束。</span><span class="sxs-lookup"><span data-stu-id="9a58c-136">After a user signs in with Basic or Digest authentication, the browser automatically sends the credentials until the session&dagger; ends.</span></span>

<span data-ttu-id="9a58c-137">&dagger;在此上下文中，*会话*指的是在此期间用户进行身份验证的客户端会话。</span><span class="sxs-lookup"><span data-stu-id="9a58c-137">&dagger;In this context, *session* refers to the client-side session during which the user is authenticated.</span></span> <span data-ttu-id="9a58c-138">它是与服务器端会话无关或[ASP.NET 核心会话中间件](xref:fundamentals/app-state)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-138">It's unrelated to server-side sessions or [ASP.NET Core Session Middleware](xref:fundamentals/app-state).</span></span>

<span data-ttu-id="9a58c-139">用户可以通过采取预防措施来防止 CSRF 漏洞：</span><span class="sxs-lookup"><span data-stu-id="9a58c-139">Users can guard against CSRF vulnerabilities by taking precautions:</span></span>

* <span data-ttu-id="9a58c-140">从 web 应用程序在完成后使用这些签名。</span><span class="sxs-lookup"><span data-stu-id="9a58c-140">Sign off of web apps when finished using them.</span></span>
* <span data-ttu-id="9a58c-141">定期清除浏览器 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-141">Clear browser cookies periodically.</span></span>

<span data-ttu-id="9a58c-142">但是，CSRF 漏洞基本上是 web 应用，而不是最终用户有问题。</span><span class="sxs-lookup"><span data-stu-id="9a58c-142">However, CSRF vulnerabilities are fundamentally a problem with the web app, not the end user.</span></span>

## <a name="authentication-fundamentals"></a><span data-ttu-id="9a58c-143">身份验证基础知识</span><span class="sxs-lookup"><span data-stu-id="9a58c-143">Authentication fundamentals</span></span>

<span data-ttu-id="9a58c-144">基于 cookie 的身份验证是一种身份验证的常用形式。</span><span class="sxs-lookup"><span data-stu-id="9a58c-144">Cookie-based authentication is a popular form of authentication.</span></span> <span data-ttu-id="9a58c-145">基于令牌的身份验证系统中受欢迎程度，特别是对于单页面应用程序 (Spa) 增长。</span><span class="sxs-lookup"><span data-stu-id="9a58c-145">Token-based authentication systems are growing in popularity, especially for Single Page Applications (SPAs).</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="9a58c-146">基于 cookie 的身份验证</span><span class="sxs-lookup"><span data-stu-id="9a58c-146">Cookie-based authentication</span></span>

<span data-ttu-id="9a58c-147">当用户身份验证使用其用户名和密码时，它们被颁发一个令牌，包含可以用于身份验证和授权的身份验证票证。</span><span class="sxs-lookup"><span data-stu-id="9a58c-147">When a user authenticates using their username and password, they're issued a token, containing an authentication ticket that can be used for authentication and authorization.</span></span> <span data-ttu-id="9a58c-148">随着工作的附带的每个请求客户端的 cookie 的令牌存储。</span><span class="sxs-lookup"><span data-stu-id="9a58c-148">The token is stored as a cookie that accompanies every request the client makes.</span></span> <span data-ttu-id="9a58c-149">生成和验证此 cookie 的 Cookie 身份验证中间件执行。</span><span class="sxs-lookup"><span data-stu-id="9a58c-149">Generating and validating this cookie is performed by the Cookie Authentication Middleware.</span></span> <span data-ttu-id="9a58c-150">[中间件](xref:fundamentals/middleware/index)的加密 cookie 序列化为一个用户主体。</span><span class="sxs-lookup"><span data-stu-id="9a58c-150">The [middleware](xref:fundamentals/middleware/index) serializes a user principal into an encrypted cookie.</span></span> <span data-ttu-id="9a58c-151">在后续请求，该中间件将验证 cookie，重新创建主体，并将分配到主体[用户](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)属性[HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-151">On subsequent requests, the middleware validates the cookie, recreates the principal, and assigns the principal to the [User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user) property of [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext).</span></span>

### <a name="token-based-authentication"></a><span data-ttu-id="9a58c-152">基于令牌的身份验证</span><span class="sxs-lookup"><span data-stu-id="9a58c-152">Token-based authentication</span></span>

<span data-ttu-id="9a58c-153">当用户进行身份验证时，它们被颁发一个令牌 （不 antiforgery 令牌）。</span><span class="sxs-lookup"><span data-stu-id="9a58c-153">When a user is authenticated, they're issued a token (not an antiforgery token).</span></span> <span data-ttu-id="9a58c-154">令牌包含用户信息的形式[声明](/dotnet/framework/security/claims-based-identity-model)或指向维护应用程序中的用户状态的应用程序的引用令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-154">The token contains user information in the form of [claims](/dotnet/framework/security/claims-based-identity-model) or a reference token that points the app to user state maintained in the app.</span></span> <span data-ttu-id="9a58c-155">当用户尝试访问要求进行身份验证的资源时，令牌将发送到使用的其他授权标头中的持有者令牌的窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a58c-155">When a user attempts to access a resource requiring authentication, the token is sent to the app with an additional authorization header in form of Bearer token.</span></span> <span data-ttu-id="9a58c-156">这使得应用程序无状态。</span><span class="sxs-lookup"><span data-stu-id="9a58c-156">This makes the app stateless.</span></span> <span data-ttu-id="9a58c-157">在每个后续请求中，令牌请求中传递进行服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="9a58c-157">In each subsequent request, the token is passed in the request for server-side validation.</span></span> <span data-ttu-id="9a58c-158">此令牌不*加密*; 它具有*编码*。</span><span class="sxs-lookup"><span data-stu-id="9a58c-158">This token isn't *encrypted*; it's *encoded*.</span></span> <span data-ttu-id="9a58c-159">在服务器上，将解码令牌来访问其信息。</span><span class="sxs-lookup"><span data-stu-id="9a58c-159">On the server, the token is decoded to access its information.</span></span> <span data-ttu-id="9a58c-160">若要在后续请求中发送令牌，请在浏览器的本地存储中存储令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-160">To send the token on subsequent requests, store the token in the browser's local storage.</span></span> <span data-ttu-id="9a58c-161">如果该令牌存储在浏览器的本地存储，则不会关心 CSRF 漏洞。</span><span class="sxs-lookup"><span data-stu-id="9a58c-161">Don't be concerned about CSRF vulnerability if the token is stored in the browser's local storage.</span></span> <span data-ttu-id="9a58c-162">CSRF 是一个问题时的令牌存储在一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="9a58c-162">CSRF is a concern when the token is stored in a cookie.</span></span>

### <a name="multiple-apps-hosted-at-one-domain"></a><span data-ttu-id="9a58c-163">在一个域托管的多个应用程序</span><span class="sxs-lookup"><span data-stu-id="9a58c-163">Multiple apps hosted at one domain</span></span>

<span data-ttu-id="9a58c-164">共享宿主环境包括易受到会话劫持、 登录 CSRF 和其他的攻击。</span><span class="sxs-lookup"><span data-stu-id="9a58c-164">Shared hosting environments are vulnerable to session hijacking, login CSRF, and other attacks.</span></span>

<span data-ttu-id="9a58c-165">尽管`example1.contoso.net`和`example2.contoso.net`是不同的主机下的主机之间没有隐式信任关系`*.contoso.net`域。</span><span class="sxs-lookup"><span data-stu-id="9a58c-165">Although `example1.contoso.net` and `example2.contoso.net` are different hosts, there's an implicit trust relationship between hosts under the `*.contoso.net` domain.</span></span> <span data-ttu-id="9a58c-166">此隐式信任关系允许影响对方的 cookie （控制 AJAX 请求的同源策略不一定适用于 HTTP cookie） 可能不受信任的主机。</span><span class="sxs-lookup"><span data-stu-id="9a58c-166">This implicit trust relationship allows potentially untrusted hosts to affect each other's cookies (the same-origin policies that govern AJAX requests don't necessarily apply to HTTP cookies).</span></span>

<span data-ttu-id="9a58c-167">可以通过不能共享域防止利用在同一个域上托管的应用程序之间的受信任的 cookie 的攻击。</span><span class="sxs-lookup"><span data-stu-id="9a58c-167">Attacks that exploit trusted cookies between apps hosted on the same domain can be prevented by not sharing domains.</span></span> <span data-ttu-id="9a58c-168">当每个应用程序托管在自身域中时，没有任何隐式 cookie 信任关系，以便利用。</span><span class="sxs-lookup"><span data-stu-id="9a58c-168">When each app is hosted on its own domain, there is no implicit cookie trust relationship to exploit.</span></span>

## <a name="aspnet-core-antiforgery-configuration"></a><span data-ttu-id="9a58c-169">ASP.NET 核心 antiforgery 配置</span><span class="sxs-lookup"><span data-stu-id="9a58c-169">ASP.NET Core antiforgery configuration</span></span>

> [!WARNING]
> <span data-ttu-id="9a58c-170">ASP.NET 核心实现 antiforgery 使用[ASP.NET 核心数据保护](xref:security/data-protection/introduction)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-170">ASP.NET Core implements antiforgery using [ASP.NET Core Data Protection](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="9a58c-171">数据保护堆栈必须配置为在服务器场中正常工作。</span><span class="sxs-lookup"><span data-stu-id="9a58c-171">The data protection stack must be configured to work in a server farm.</span></span> <span data-ttu-id="9a58c-172">请参阅[配置数据保护](xref:security/data-protection/configuration/overview)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="9a58c-172">See [Configuring data protection](xref:security/data-protection/configuration/overview) for more information.</span></span>

<span data-ttu-id="9a58c-173">在 ASP.NET 核心 2.0 或更高版本， [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) antiforgery 令牌注入 HTML 窗体元素。</span><span class="sxs-lookup"><span data-stu-id="9a58c-173">In ASP.NET Core 2.0 or later, the [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) injects antiforgery tokens into HTML form elements.</span></span> <span data-ttu-id="9a58c-174">Razor 文件中的以下标记将自动生成 antiforgery 令牌：</span><span class="sxs-lookup"><span data-stu-id="9a58c-174">The following markup in a Razor file automatically generates antiforgery tokens:</span></span>

```cshtml
<form method="post">
    ...
</form>
```

<span data-ttu-id="9a58c-175">类似地， [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) antiforgery 令牌生成默认情况下，如果窗体的方法不 GET。</span><span class="sxs-lookup"><span data-stu-id="9a58c-175">Similarily, [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) generates antiforgery tokens by default if the form's method isn't GET.</span></span>

<span data-ttu-id="9a58c-176">自动生成的 antiforgery 令牌 HTML 窗体元素发生时`<form>`标记包含`method="post"`属性和以下任一条件：</span><span class="sxs-lookup"><span data-stu-id="9a58c-176">The automatic generation of antiforgery tokens for HTML form elements happens when the `<form>` tag contains the `method="post"` attribute and either of the following are true:</span></span>

  * <span data-ttu-id="9a58c-177">操作属性为空 (`action=""`)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-177">The action attribute is empty (`action=""`).</span></span>
  * <span data-ttu-id="9a58c-178">操作属性不提供 (`<form method="post">`)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-178">The action attribute isn't supplied (`<form method="post">`).</span></span>

<span data-ttu-id="9a58c-179">可以禁用自动生成的 antiforgery 令牌 HTML 窗体元素：</span><span class="sxs-lookup"><span data-stu-id="9a58c-179">Automatic generation of antiforgery tokens for HTML form elements can be disabled:</span></span>

* <span data-ttu-id="9a58c-180">显式禁用 antiforgery 令牌`asp-antiforgery`属性：</span><span class="sxs-lookup"><span data-stu-id="9a58c-180">Explicitly disable antiforgery tokens with the `asp-antiforgery` attribute:</span></span>

  ```cshtml
  <form method="post" asp-antiforgery="false">
      ...
  </form>
  ```

* <span data-ttu-id="9a58c-181">Form 元素是已选择扩展的标记帮助程序通过使用标记帮助器[！ 选择退出符号](xref:mvc/views/tag-helpers/intro#opt-out):</span><span class="sxs-lookup"><span data-stu-id="9a58c-181">The form element is opted-out of Tag Helpers by using the Tag Helper [! opt-out symbol](xref:mvc/views/tag-helpers/intro#opt-out):</span></span>

  ```cshtml
  <!form method="post">
      ...
  </!form>
  ```

* <span data-ttu-id="9a58c-182">删除`FormTagHelper`从视图。</span><span class="sxs-lookup"><span data-stu-id="9a58c-182">Remove the `FormTagHelper` from the view.</span></span> <span data-ttu-id="9a58c-183">`FormTagHelper`可以通过将以下指令添加到 Razor 视图从视图中删除：</span><span class="sxs-lookup"><span data-stu-id="9a58c-183">The `FormTagHelper` can be removed from a view by adding the following directive to the Razor view:</span></span>

  ```cshtml
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> <span data-ttu-id="9a58c-184">[Razor 页](xref:mvc/razor-pages/index)会自动防范 XSRF/CSRF。</span><span class="sxs-lookup"><span data-stu-id="9a58c-184">[Razor Pages](xref:mvc/razor-pages/index) are automatically protected from XSRF/CSRF.</span></span> <span data-ttu-id="9a58c-185">有关详细信息，请参阅[XSRF/CSRF 和 Razor 页](xref:mvc/razor-pages/index#xsrf)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-185">For more information, see [XSRF/CSRF and Razor Pages](xref:mvc/razor-pages/index#xsrf).</span></span>

<span data-ttu-id="9a58c-186">防御 CSRF 攻击的最常见方法是使用*同步器令牌模式*(STP)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-186">The most common approach to defending against CSRF attacks is to use the *Synchronizer Token Pattern* (STP).</span></span> <span data-ttu-id="9a58c-187">在用户请求具有窗体数据的页时，使用 STP:</span><span class="sxs-lookup"><span data-stu-id="9a58c-187">STP is used when the user requests a page with form data:</span></span>

1. <span data-ttu-id="9a58c-188">服务器将发送到客户端的当前用户的标识与关联的令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-188">The server sends a token associated with the current user's identity to the client.</span></span>
1. <span data-ttu-id="9a58c-189">客户端返回将令牌发送到服务器以进行验证。</span><span class="sxs-lookup"><span data-stu-id="9a58c-189">The client sends back the token to the server for verification.</span></span>
1. <span data-ttu-id="9a58c-190">如果服务器收到与经过身份验证的用户的标识不匹配的令牌，而拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-190">If the server receives a token that doesn't match the authenticated user's identity, the request is rejected.</span></span>

<span data-ttu-id="9a58c-191">该令牌的唯一且不可预测。</span><span class="sxs-lookup"><span data-stu-id="9a58c-191">The token is unique and unpredictable.</span></span> <span data-ttu-id="9a58c-192">此外可以使用令牌以确保正确地执行序列化的一系列请求 (例如，确保请求序列的： 第 1 页&ndash;页上 2&ndash;第 3 页)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-192">The token can also be used to ensure proper sequencing of a series of requests (for example, ensuring the request sequence of: page 1 &ndash; page 2 &ndash; page 3).</span></span> <span data-ttu-id="9a58c-193">ASP.NET 核心 MVC 和 Razor 页模板中的窗体的所有生成 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-193">All of the forms in ASP.NET Core MVC and Razor Pages templates generate antiforgery tokens.</span></span> <span data-ttu-id="9a58c-194">以下两个视图的示例生成 antiforgery 令牌：</span><span class="sxs-lookup"><span data-stu-id="9a58c-194">The following pair of view examples generate antiforgery tokens:</span></span>

```cshtml
<form asp-controller="Manage" asp-action="ChangePassword" method="post">
    ...
</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    ...
}
```

<span data-ttu-id="9a58c-195">显式添加到 antiforgery 令牌`<form>`没有标记帮助程序使用的 HTML 帮助程序元素[ @Html.AntiForgeryToken ](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):</span><span class="sxs-lookup"><span data-stu-id="9a58c-195">Explicitly add an antiforgery token to a `<form>` element without using Tag Helpers with the HTML helper [@Html.AntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):</span></span>

```cshtml
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

<span data-ttu-id="9a58c-196">在每个前面的情况下，ASP.NET Core 添加类似于以下一个隐藏的表单字段：</span><span class="sxs-lookup"><span data-stu-id="9a58c-196">In each of the preceding cases, ASP.NET Core adds a hidden form field similar to the following:</span></span>

```cshtml
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkS ... s2-m9Yw">
```

<span data-ttu-id="9a58c-197">ASP.NET 核心包括三个[筛选器](xref:mvc/controllers/filters)来处理 antiforgery 令牌：</span><span class="sxs-lookup"><span data-stu-id="9a58c-197">ASP.NET Core includes three [filters](xref:mvc/controllers/filters) for working with antiforgery tokens:</span></span>

* [<span data-ttu-id="9a58c-198">ValidateAntiForgeryToken</span><span class="sxs-lookup"><span data-stu-id="9a58c-198">ValidateAntiForgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)
* [<span data-ttu-id="9a58c-199">AutoValidateAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="9a58c-199">AutoValidateAntiforgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)
* [<span data-ttu-id="9a58c-200">IgnoreAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="9a58c-200">IgnoreAntiforgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)

## <a name="antiforgery-options"></a><span data-ttu-id="9a58c-201">Antiforgery 选项</span><span class="sxs-lookup"><span data-stu-id="9a58c-201">Antiforgery options</span></span>

<span data-ttu-id="9a58c-202">自定义[antiforgery 选项](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions)中`Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="9a58c-202">Customize [antiforgery options](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions) in `Startup.ConfigureServices`:</span></span>

```csharp
services.AddAntiforgery(options => 
{
    options.CookieDomain = "contoso.com";
    options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
    options.CookiePath = "Path";
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.RequireSsl = false;
    options.SuppressXFrameOptionsHeader = false;
});
```

| <span data-ttu-id="9a58c-203">选项</span><span class="sxs-lookup"><span data-stu-id="9a58c-203">Option</span></span> | <span data-ttu-id="9a58c-204">描述</span><span class="sxs-lookup"><span data-stu-id="9a58c-204">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="9a58c-205">Cookie</span><span class="sxs-lookup"><span data-stu-id="9a58c-205">Cookie</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookie) | <span data-ttu-id="9a58c-206">确定用于创建 antiforgery cookie 的设置。</span><span class="sxs-lookup"><span data-stu-id="9a58c-206">Determines the settings used to create the antiforgery cookies.</span></span> |
| [<span data-ttu-id="9a58c-207">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="9a58c-207">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiedomain) | <span data-ttu-id="9a58c-208">Cookie 的域。</span><span class="sxs-lookup"><span data-stu-id="9a58c-208">The domain of the cookie.</span></span> <span data-ttu-id="9a58c-209">默认为 `null`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-209">Defaults to `null`.</span></span> <span data-ttu-id="9a58c-210">此属性已过时，并在未来版本中将删除。</span><span class="sxs-lookup"><span data-stu-id="9a58c-210">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="9a58c-211">建议的替代项是 Cookie.Domain。</span><span class="sxs-lookup"><span data-stu-id="9a58c-211">The recommended alternative is Cookie.Domain.</span></span> |
| [<span data-ttu-id="9a58c-212">CookieName</span><span class="sxs-lookup"><span data-stu-id="9a58c-212">CookieName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiename) | <span data-ttu-id="9a58c-213">Cookie 的名称。</span><span class="sxs-lookup"><span data-stu-id="9a58c-213">The name of the cookie.</span></span> <span data-ttu-id="9a58c-214">如果未设置，则系统会生成一个唯一的名称开头[DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) ("。AspNetCore.Antiforgery。") 下。</span><span class="sxs-lookup"><span data-stu-id="9a58c-214">If not set, the system generates a unique name beginning with the [DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) (".AspNetCore.Antiforgery.").</span></span> <span data-ttu-id="9a58c-215">此属性已过时，并在未来版本中将删除。</span><span class="sxs-lookup"><span data-stu-id="9a58c-215">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="9a58c-216">建议的替代项是 Cookie.Name。</span><span class="sxs-lookup"><span data-stu-id="9a58c-216">The recommended alternative is Cookie.Name.</span></span> |
| [<span data-ttu-id="9a58c-217">CookiePath</span><span class="sxs-lookup"><span data-stu-id="9a58c-217">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiepath) | <span data-ttu-id="9a58c-218">在 cookie 上设置的路径。</span><span class="sxs-lookup"><span data-stu-id="9a58c-218">The path set on the cookie.</span></span> <span data-ttu-id="9a58c-219">此属性已过时，并在未来版本中将删除。</span><span class="sxs-lookup"><span data-stu-id="9a58c-219">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="9a58c-220">建议的替代项是 Cookie.Path。</span><span class="sxs-lookup"><span data-stu-id="9a58c-220">The recommended alternative is Cookie.Path.</span></span> |
| [<span data-ttu-id="9a58c-221">FormFieldName</span><span class="sxs-lookup"><span data-stu-id="9a58c-221">FormFieldName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.formfieldname) | <span data-ttu-id="9a58c-222">Antiforgery 系统用于呈现 antiforgery 令牌在视图中的隐藏的表单字段的名称。</span><span class="sxs-lookup"><span data-stu-id="9a58c-222">The name of the hidden form field used by the antiforgery system to render antiforgery tokens in views.</span></span> |
| [<span data-ttu-id="9a58c-223">HeaderName</span><span class="sxs-lookup"><span data-stu-id="9a58c-223">HeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.headername) | <span data-ttu-id="9a58c-224">Antiforgery 系统使用的标头的名称。</span><span class="sxs-lookup"><span data-stu-id="9a58c-224">The name of the header used by the antiforgery system.</span></span> <span data-ttu-id="9a58c-225">如果`null`，系统会考虑仅窗体数据。</span><span class="sxs-lookup"><span data-stu-id="9a58c-225">If `null`, the system considers only form data.</span></span> |
| [<span data-ttu-id="9a58c-226">RequireSsl</span><span class="sxs-lookup"><span data-stu-id="9a58c-226">RequireSsl</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.requiressl) | <span data-ttu-id="9a58c-227">指定是否由 antiforgery 系统需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="9a58c-227">Specifies whether SSL is required by the antiforgery system.</span></span> <span data-ttu-id="9a58c-228">如果`true`，非 SSL 请求将失败。</span><span class="sxs-lookup"><span data-stu-id="9a58c-228">If `true`, non-SSL requests fail.</span></span> <span data-ttu-id="9a58c-229">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-229">Defaults to `false`.</span></span> <span data-ttu-id="9a58c-230">此属性已过时，并在未来版本中将删除。</span><span class="sxs-lookup"><span data-stu-id="9a58c-230">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="9a58c-231">建议的替代项是设置 Cookie.SecurePolicy。</span><span class="sxs-lookup"><span data-stu-id="9a58c-231">The recommended alternative is to set Cookie.SecurePolicy.</span></span> |
| [<span data-ttu-id="9a58c-232">SuppressXFrameOptionsHeader</span><span class="sxs-lookup"><span data-stu-id="9a58c-232">SuppressXFrameOptionsHeader</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.suppressxframeoptionsheader) | <span data-ttu-id="9a58c-233">指定是否禁止生成`X-Frame-Options`标头。</span><span class="sxs-lookup"><span data-stu-id="9a58c-233">Specifies whether to suppress generation of the `X-Frame-Options` header.</span></span> <span data-ttu-id="9a58c-234">默认情况下，值为"SAMEORIGIN"生成标头。</span><span class="sxs-lookup"><span data-stu-id="9a58c-234">By default, the header is generated with a value of "SAMEORIGIN".</span></span> <span data-ttu-id="9a58c-235">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-235">Defaults to `false`.</span></span> |

<span data-ttu-id="9a58c-236">有关详细信息，请参阅[CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-236">For more information, see [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions).</span></span>

## <a name="configure-antiforgery-features-with-iantiforgery"></a><span data-ttu-id="9a58c-237">使用 IAntiforgery 配置 antiforgery 功能</span><span class="sxs-lookup"><span data-stu-id="9a58c-237">Configure antiforgery features with IAntiforgery</span></span>

<span data-ttu-id="9a58c-238">[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery)提供 API 来配置 antiforgery 功能。</span><span class="sxs-lookup"><span data-stu-id="9a58c-238">[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) provides the API to configure antiforgery features.</span></span> <span data-ttu-id="9a58c-239">`IAntiforgery` 可以在请求`Configure`方法`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="9a58c-239">`IAntiforgery` can be requested in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="9a58c-240">下面的示例使用从应用程序的主页上的中间件生成 antiforgery 令牌并将其发送响应中将其作为 cookie （使用在本主题后面所述的默认角度命名约定）：</span><span class="sxs-lookup"><span data-stu-id="9a58c-240">The following example uses middleware from the app's home page to generate an antiforgery token and send it in the response as a cookie (using the default Angular naming convention described later in this topic):</span></span>

```csharp
public void Configure(IApplicationBuilder app, IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;

        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // The request token can be sent as a JavaScript-readable cookie, 
            // and Angular uses it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
}
```

### <a name="require-antiforgery-validation"></a><span data-ttu-id="9a58c-241">要求 antiforgery 验证</span><span class="sxs-lookup"><span data-stu-id="9a58c-241">Require antiforgery validation</span></span>

<span data-ttu-id="9a58c-242">[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)是操作筛选器，可以应用于单个操作，一个控制器或全局范围内。</span><span class="sxs-lookup"><span data-stu-id="9a58c-242">[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute) is an action filter that can be applied to an individual action, a controller, or globally.</span></span> <span data-ttu-id="9a58c-243">除非请求包含有效的 antiforgery 令牌，将阻止对已应用此筛选器的操作发出的请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-243">Requests made to actions that have this filter applied are blocked unless the request includes a valid antiforgery token.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();

    if (user != null)
    {
        var result = 
            await _userManager.RemoveLoginAsync(
                user, account.LoginProvider, account.ProviderKey);

        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }

    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

<span data-ttu-id="9a58c-244">`ValidateAntiForgeryToken`属性修饰，包括 HTTP GET 请求对操作方法的请求要求令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-244">The `ValidateAntiForgeryToken` attribute requires a token for requests to the action methods it decorates, including HTTP GET requests.</span></span> <span data-ttu-id="9a58c-245">如果`ValidateAntiForgeryToken`属性应用跨应用程序的控制器，则可以重写与`IgnoreAntiforgeryToken`属性。</span><span class="sxs-lookup"><span data-stu-id="9a58c-245">If the `ValidateAntiForgeryToken` attribute is applied across the app's controllers, it can be overridden with the `IgnoreAntiforgeryToken` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="9a58c-246">ASP.NET Core 不支持自动将 antiforgery 令牌添加到 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-246">ASP.NET Core doesn't support adding antiforgery tokens to GET requests automatically.</span></span>

### <a name="automatically-validate-antiforgery-tokens-for-unsafe-http-methods-only"></a><span data-ttu-id="9a58c-247">自动验证 antiforgery 令牌仅不安全的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="9a58c-247">Automatically validate antiforgery tokens for unsafe HTTP methods only</span></span>

<span data-ttu-id="9a58c-248">ASP.NET Core 应用不生成 antiforgery 令牌进行安全的 HTTP 方法 （GET、 HEAD、 选项和跟踪）。</span><span class="sxs-lookup"><span data-stu-id="9a58c-248">ASP.NET Core apps don't generate antiforgery tokens for safe HTTP methods (GET, HEAD, OPTIONS, and TRACE).</span></span> <span data-ttu-id="9a58c-249">而不是广泛应用`ValidateAntiForgeryToken`属性，然后重写它与`IgnoreAntiforgeryToken`特性， [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)可以使用属性。</span><span class="sxs-lookup"><span data-stu-id="9a58c-249">Instead of broadly applying the `ValidateAntiForgeryToken` attribute and then overriding it with `IgnoreAntiforgeryToken` attributes, the [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute) attribute can be used.</span></span> <span data-ttu-id="9a58c-250">此属性适用类似`ValidateAntiForgeryToken`特性，只不过它不需要使用以下的 HTTP 方法发出的请求令牌：</span><span class="sxs-lookup"><span data-stu-id="9a58c-250">This attribute works identically to the `ValidateAntiForgeryToken` attribute, except that it doesn't require tokens for requests made using the following HTTP methods:</span></span>

* <span data-ttu-id="9a58c-251">GET</span><span class="sxs-lookup"><span data-stu-id="9a58c-251">GET</span></span>
* <span data-ttu-id="9a58c-252">HEAD</span><span class="sxs-lookup"><span data-stu-id="9a58c-252">HEAD</span></span>
* <span data-ttu-id="9a58c-253">选项</span><span class="sxs-lookup"><span data-stu-id="9a58c-253">OPTIONS</span></span>
* <span data-ttu-id="9a58c-254">TRACE</span><span class="sxs-lookup"><span data-stu-id="9a58c-254">TRACE</span></span>

<span data-ttu-id="9a58c-255">我们建议使用`AutoValidateAntiforgeryToken`广泛的非 API 方案。</span><span class="sxs-lookup"><span data-stu-id="9a58c-255">We recommend use of `AutoValidateAntiforgeryToken` broadly for non-API scenarios.</span></span> <span data-ttu-id="9a58c-256">这可确保默认情况下保护 POST 操作。</span><span class="sxs-lookup"><span data-stu-id="9a58c-256">This ensures POST actions are protected by default.</span></span> <span data-ttu-id="9a58c-257">替代项是默认情况下，将忽略 antiforgery 令牌除非`ValidateAntiForgeryToken`应用于单个操作方法。</span><span class="sxs-lookup"><span data-stu-id="9a58c-257">The alternative is to ignore antiforgery tokens by default, unless `ValidateAntiForgeryToken` is applied to individual action methods.</span></span> <span data-ttu-id="9a58c-258">它更有可能在此方案中保留的 POST 操作方法不受保护错误地使应用程序容易受到 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="9a58c-258">It's more likely in this scenario for a POST action method to be left unprotected by mistake, leaving the app vulnerable to CSRF attacks.</span></span> <span data-ttu-id="9a58c-259">所有文章应都发送 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-259">All POSTs should send the antiforgery token.</span></span>

<span data-ttu-id="9a58c-260">Api 没有一种用于发送令牌的非 cookie 一部分的自动机制。</span><span class="sxs-lookup"><span data-stu-id="9a58c-260">APIs don't have an automatic mechanism for sending the non-cookie part of the token.</span></span> <span data-ttu-id="9a58c-261">实现可能取决于客户端代码实现。</span><span class="sxs-lookup"><span data-stu-id="9a58c-261">The implementation probably depends on the client code implementation.</span></span> <span data-ttu-id="9a58c-262">一些示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a58c-262">Some examples are shown below:</span></span>

<span data-ttu-id="9a58c-263">类级别示例：</span><span class="sxs-lookup"><span data-stu-id="9a58c-263">Class-level example:</span></span>

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

<span data-ttu-id="9a58c-264">全局示例：</span><span class="sxs-lookup"><span data-stu-id="9a58c-264">Global example:</span></span>

```csharp
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

### <a name="override-global-or-controller-antiforgery-attributes"></a><span data-ttu-id="9a58c-265">替代全局或控制器 antiforgery 属性</span><span class="sxs-lookup"><span data-stu-id="9a58c-265">Override global or controller antiforgery attributes</span></span>

<span data-ttu-id="9a58c-266">[IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)筛选器用于消除对给定操作 （或控制器） 的 antiforgery 令牌的需要。</span><span class="sxs-lookup"><span data-stu-id="9a58c-266">The [IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute) filter is used to eliminate the need for an antiforgery token for a given action (or controller).</span></span> <span data-ttu-id="9a58c-267">当应用时，此筛选器将重写`ValidateAntiForgeryToken`和`AutoValidateAntiforgeryToken`（全局或在控制器上） 在高级别指定筛选器。</span><span class="sxs-lookup"><span data-stu-id="9a58c-267">When applied, this filter overrides `ValidateAntiForgeryToken` and `AutoValidateAntiforgeryToken` filters specified at a higher level (globally or on a controller).</span></span>

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
    [HttpPost]
    [IgnoreAntiforgeryToken]
    public async Task<IActionResult> DoSomethingSafe(SomeViewModel model)
    {
        // no antiforgery token required
    }
}
```

## <a name="refresh-tokens-after-authentication"></a><span data-ttu-id="9a58c-268">身份验证后刷新令牌</span><span class="sxs-lookup"><span data-stu-id="9a58c-268">Refresh tokens after authentication</span></span>

<span data-ttu-id="9a58c-269">用户进行身份验证通过将用户重定向到一个视图或 Razor 页页后，应刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-269">Tokens should be refreshed after the user is authenticated by redirecting the user to a view or Razor Pages page.</span></span>

## <a name="javascript-ajax-and-spas"></a><span data-ttu-id="9a58c-270">JavaScript、 AJAX 和 Spa</span><span class="sxs-lookup"><span data-stu-id="9a58c-270">JavaScript, AJAX, and SPAs</span></span>

<span data-ttu-id="9a58c-271">在传统的基于 HTML 的应用，antiforgery 令牌将传递到使用隐藏的表单域的服务器。</span><span class="sxs-lookup"><span data-stu-id="9a58c-271">In traditional HTML-based apps, antiforgery tokens are passed to the server using hidden form fields.</span></span> <span data-ttu-id="9a58c-272">在基于 JavaScript 的现代应用和 Spa 中，以编程方式进行多请求。</span><span class="sxs-lookup"><span data-stu-id="9a58c-272">In modern JavaScript-based apps and SPAs, many requests are made programmatically.</span></span> <span data-ttu-id="9a58c-273">这些 AJAX 请求可能使用其他方法 （如请求标头或 cookie） 将该令牌发送。</span><span class="sxs-lookup"><span data-stu-id="9a58c-273">These AJAX requests may use other techniques (such as request headers or cookies) to send the token.</span></span>

<span data-ttu-id="9a58c-274">如果使用 cookie 来存储身份验证令牌，并在服务器上的 API 请求进行身份验证，CSRF 是一个潜在的问题。</span><span class="sxs-lookup"><span data-stu-id="9a58c-274">If cookies are used to store authentication tokens and to authenticate API requests on the server, CSRF is a potential problem.</span></span> <span data-ttu-id="9a58c-275">如果本地存储用于存储令牌，因为从本地存储的值不会自动发送到每个请求的服务器可能会缓解 CSRF 漏洞。</span><span class="sxs-lookup"><span data-stu-id="9a58c-275">If local storage is used to store the token, CSRF vulnerability might be mitigated because values from local storage aren't sent automatically to the server with every request.</span></span> <span data-ttu-id="9a58c-276">因此，使用本地存储来存储客户端和发送令牌，因为请求标头是建议的方法上的 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9a58c-276">Thus, using local storage to store the antiforgery token on the client and sending the token as a request header is a recommended approach.</span></span>

### <a name="javascript"></a><span data-ttu-id="9a58c-277">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9a58c-277">JavaScript</span></span>

<span data-ttu-id="9a58c-278">使用视图支持 JavaScript，令牌可以创建使用从视图中的服务。</span><span class="sxs-lookup"><span data-stu-id="9a58c-278">Using JavaScript with views, the token can be created using a service from within the view.</span></span> <span data-ttu-id="9a58c-279">注入[Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery)到视图并调用服务[GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):</span><span class="sxs-lookup"><span data-stu-id="9a58c-279">Inject the [Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) service into the view and call [GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):</span></span>

[!code-csharp[](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,12-13,35-36)]

<span data-ttu-id="9a58c-280">此方法不需要直接处理从服务器设置 cookie 或从客户端读取它们。</span><span class="sxs-lookup"><span data-stu-id="9a58c-280">This approach eliminates the need to deal directly with setting cookies from the server or reading them from the client.</span></span>

<span data-ttu-id="9a58c-281">前面的示例使用 JavaScript 的 AJAX POST 标头中读取的隐藏的字段值。</span><span class="sxs-lookup"><span data-stu-id="9a58c-281">The preceding example uses JavaScript to read the hidden field value for the AJAX POST header.</span></span>

<span data-ttu-id="9a58c-282">JavaScript 还可以访问在 cookie 令牌并使用 cookie 的内容与令牌的值创建的标头。</span><span class="sxs-lookup"><span data-stu-id="9a58c-282">JavaScript can also access tokens in cookies and use the cookie's contents to create a header with the token's value.</span></span>

```csharp
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
    new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

<span data-ttu-id="9a58c-283">假设脚本请求将该令牌发送调用标头中`X-CSRF-TOKEN`，配置 antiforgery 服务以查找`X-CSRF-TOKEN`标头：</span><span class="sxs-lookup"><span data-stu-id="9a58c-283">Assuming the script requests to send the token in a header called `X-CSRF-TOKEN`, configure the antiforgery service to look for the `X-CSRF-TOKEN` header:</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

<span data-ttu-id="9a58c-284">下面的示例使用 JavaScript 进行了相应的标头使用的 AJAX 请求：</span><span class="sxs-lookup"><span data-stu-id="9a58c-284">The following example uses JavaScript to make an AJAX request with the appropriate header:</span></span>

```javascript
function getCookie(cname) {
    var name = cname + "=";
    var decodedCookie = decodeURIComponent(document.cookie);
    var ca = decodedCookie.split(';');
    for(var i = 0; i <ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

var csrfToken = getCookie("CSRF-TOKEN");

var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (xhttp.readyState == XMLHttpRequest.DONE) {
        if (xhttp.status == 200) {
            alert(xhttp.responseText);
        } else {
            alert('There was an error processing the AJAX request.');
        }
    }
};
xhttp.open('POST', '/api/password/changepassword', true);
xhttp.setRequestHeader("Content-type", "application/json");
xhttp.setRequestHeader("X-CSRF-TOKEN", csrfToken);
xhttp.send(JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }));
```

### <a name="angularjs"></a><span data-ttu-id="9a58c-285">AngularJS</span><span class="sxs-lookup"><span data-stu-id="9a58c-285">AngularJS</span></span>

<span data-ttu-id="9a58c-286">AngularJS 使用到地址 CSRF 的约定。</span><span class="sxs-lookup"><span data-stu-id="9a58c-286">AngularJS uses a convention to address CSRF.</span></span> <span data-ttu-id="9a58c-287">如果服务器发送具有该名称的 cookie `XSRF-TOKEN`，AngularJS`$http`服务将 cookie 值添加到标头时它将请求发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="9a58c-287">If the server sends a cookie with the name `XSRF-TOKEN`, the AngularJS `$http` service adds the cookie value to a header when it sends a request to the server.</span></span> <span data-ttu-id="9a58c-288">此过程是自动进行。</span><span class="sxs-lookup"><span data-stu-id="9a58c-288">This process is automatic.</span></span> <span data-ttu-id="9a58c-289">标头不需要显式设置。</span><span class="sxs-lookup"><span data-stu-id="9a58c-289">The header doesn't need to be set explicitly.</span></span> <span data-ttu-id="9a58c-290">标头名称是`X-XSRF-TOKEN`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-290">The header name is `X-XSRF-TOKEN`.</span></span> <span data-ttu-id="9a58c-291">服务器应检测此标头，并验证其内容。</span><span class="sxs-lookup"><span data-stu-id="9a58c-291">The server should detect this header and validate its contents.</span></span>

<span data-ttu-id="9a58c-292">有关 ASP.NET 核心 API 使用此约定：</span><span class="sxs-lookup"><span data-stu-id="9a58c-292">For ASP.NET Core API work with this convention:</span></span>

* <span data-ttu-id="9a58c-293">配置你的应用程序提供在调用 cookie 令牌`XSRF-TOKEN`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-293">Configure your app to provide a token in a cookie called `XSRF-TOKEN`.</span></span>
* <span data-ttu-id="9a58c-294">将查找名为的标头 antiforgery 服务配置为`X-XSRF-TOKEN`。</span><span class="sxs-lookup"><span data-stu-id="9a58c-294">Configure the antiforgery service to look for a header named `X-XSRF-TOKEN`.</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

<span data-ttu-id="9a58c-295">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="9a58c-295">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="extend-antiforgery"></a><span data-ttu-id="9a58c-296">扩展 antiforgery</span><span class="sxs-lookup"><span data-stu-id="9a58c-296">Extend antiforgery</span></span>

<span data-ttu-id="9a58c-297">[IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider)类型允许开发人员通过往返中每个令牌的其他数据扩展的反 CSRF 系统行为。</span><span class="sxs-lookup"><span data-stu-id="9a58c-297">The [IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) type allows developers to extend the behavior of the anti-CSRF system by round-tripping additional data in each token.</span></span> <span data-ttu-id="9a58c-298">[GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata)每次调用方法生成的字段标记，和在生成的标记内嵌入的返回值。</span><span class="sxs-lookup"><span data-stu-id="9a58c-298">The [GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata) method is called each time a field token is generated, and the return value is embedded within the generated token.</span></span> <span data-ttu-id="9a58c-299">实施者无法返回时间戳、 nonce 或任何其他值，然后调用[ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata)时验证令牌验证此数据。</span><span class="sxs-lookup"><span data-stu-id="9a58c-299">An implementer could return a timestamp, a nonce, or any other value and then call [ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata) to validate this data when the token is validated.</span></span> <span data-ttu-id="9a58c-300">客户端的用户名已嵌入在生成的令牌中，因此无需包括此信息。</span><span class="sxs-lookup"><span data-stu-id="9a58c-300">The client's username is already embedded in the generated tokens, so there's no need to include this information.</span></span> <span data-ttu-id="9a58c-301">如果令牌包括补充数据但不是`IAntiForgeryAdditionalDataProvider`是配置，不验证补充数据。</span><span class="sxs-lookup"><span data-stu-id="9a58c-301">If a token includes supplemental data but no `IAntiForgeryAdditionalDataProvider` is configured, the supplemental data isn't validated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a58c-302">其他资源</span><span class="sxs-lookup"><span data-stu-id="9a58c-302">Additional resources</span></span>

* <span data-ttu-id="9a58c-303">[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))上[打开 Web 应用程序安全项目](https://www.owasp.org/index.php/Main_Page)(OWASP)。</span><span class="sxs-lookup"><span data-stu-id="9a58c-303">[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) on [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP).</span></span>
