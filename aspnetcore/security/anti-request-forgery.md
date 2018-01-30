---
title: "阻止在 ASP.NET 核心中的跨网站请求伪造 (XSRF/CSRF) 攻击"
author: steve-smith
description: "阻止在 ASP.NET 核心中的跨网站请求伪造 (XSRF/CSRF) 攻击"
manager: wpickett
ms.author: riande
ms.date: 7/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: e076e301004c04b5c516d775353a4b6e50a3f36e
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="preventing-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a><span data-ttu-id="9dc2d-103">阻止在 ASP.NET 核心中的跨网站请求伪造 (XSRF/CSRF) 攻击</span><span class="sxs-lookup"><span data-stu-id="9dc2d-103">Preventing Cross-Site Request Forgery (XSRF/CSRF) Attacks in ASP.NET Core</span></span>

<span data-ttu-id="9dc2d-104">[Steve Smith](https://ardalis.com/)， [Fiyaz Hasan](https://twitter.com/FiyazBinHasan)，和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9dc2d-104">[Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-attack-does-anti-forgery-prevent"></a><span data-ttu-id="9dc2d-105">防伪阻止哪些攻击？</span><span class="sxs-lookup"><span data-stu-id="9dc2d-105">What attack does anti-forgery prevent?</span></span>

<span data-ttu-id="9dc2d-106">跨站点请求伪造 (也称为 XSRF 或 CSRF，发音*，请参阅冲浪*) 是针对恶意网站凭此可以影响客户端浏览器和信任的网站之间的交互的 web 托管的应用程序的攻击该浏览器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-106">Cross-site request forgery (also known as XSRF or CSRF, pronounced *see-surf*) is an attack against web-hosted applications whereby a malicious web site can influence the interaction between a client browser and a web site that trusts that browser.</span></span> <span data-ttu-id="9dc2d-107">因为 web 浏览器将自动与每个请求某些类型的身份验证令牌发送到网站，这些攻击都可能。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-107">These attacks are made possible because web browsers send some types of authentication tokens automatically with every request to a web site.</span></span> <span data-ttu-id="9dc2d-108">这种形式的攻击也称为的*一键式攻击*或*会话乘坐*，因为用户攻击利用的先前进行身份验证会话。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-108">This form of exploit's also known as a *one-click attack* or as *session riding*, because the attack takes advantage of the user's previously authenticated session.</span></span>

<span data-ttu-id="9dc2d-109">CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-109">An example of a CSRF attack:</span></span>

1. <span data-ttu-id="9dc2d-110">用户登录到`www.example.com`，使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-110">A user logs into `www.example.com`, using forms authentication.</span></span>
2. <span data-ttu-id="9dc2d-111">服务器对用户进行身份验证，并发出包含身份验证 cookie 的响应。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-111">The server authenticates the user and issues a response that includes an authentication cookie.</span></span>
3. <span data-ttu-id="9dc2d-112">用户访问恶意站点。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-112">The user visits a malicious site.</span></span>

   <span data-ttu-id="9dc2d-113">恶意站点包含类似于以下的 HTML 窗体：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-113">The malicious site contains an HTML form similar to the following:</span></span>

```html
   <h1>You Are a Winner!</h1>
     <form action="http://example.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw" />
       <input type="hidden" name="Amount" value="1000000" />
     <input type="submit" value="Click Me"/>
   </form>
```

<span data-ttu-id="9dc2d-114">请注意，窗体操作发送到易受攻击的站点，不适用于恶意站点。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-114">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="9dc2d-115">这是 CSRF 的"跨站点"部分。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-115">This is the “cross-site” part of CSRF.</span></span>

4. <span data-ttu-id="9dc2d-116">用户可单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-116">The user clicks the submit button.</span></span> <span data-ttu-id="9dc2d-117">浏览器会自动包括请求的域 （在此情况下易受攻击的站点） 与请求的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-117">The browser automatically includes the authentication cookie for the requested domain (the vulnerable site in this case) with the request.</span></span>
5. <span data-ttu-id="9dc2d-118">请求与用户的身份验证上下文的服务器上运行，并可以执行的已经过身份验证的用户可以执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-118">The request runs on the server with the user's authentication context and can perform any action that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="9dc2d-119">此示例要求用户通过单击窗体按钮。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-119">This example requires the user to click the form button.</span></span> <span data-ttu-id="9dc2d-120">无法恶意页：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-120">The malicious page could:</span></span>

* <span data-ttu-id="9dc2d-121">运行自动提交该表单的脚本。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-121">Run a script that automatically submits the form.</span></span>
* <span data-ttu-id="9dc2d-122">将窗体提交作为 AJAX 请求中发送。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-122">Sends a form submission as an AJAX request.</span></span> 
* <span data-ttu-id="9dc2d-123">使用 CSS 的隐藏的表单。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-123">Use a hidden form with CSS.</span></span> 

<span data-ttu-id="9dc2d-124">使用 SSL，则不会阻止 CSRF 攻击，恶意的站点系统可以将发送`https://`请求。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-124">Using SSL doesn't prevent a CSRF attack, the malicious site can send an `https://` request.</span></span> 

<span data-ttu-id="9dc2d-125">一些攻击目标响应的网站终结点`GET`请求，该用例的图像标记可以用于执行 （这种形式的攻击常见论坛在站点是允许映像但阻止 JavaScript） 的操作。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-125">Some attacks  target site endpoints that respond to `GET` requests, in which case an image tag can be used to perform the action (this form of attack is common on forum sites that permit images but block JavaScript).</span></span> <span data-ttu-id="9dc2d-126">更改状态的应用程序`GET`请求是容易受到恶意攻击的攻击。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-126">Applications that change state with `GET` requests are  vulnerable from malicious attacks.</span></span>

<span data-ttu-id="9dc2d-127">因为浏览器向目标网站发送所有相关 cookie，CSRF 攻击是可能对网站进行身份验证，使用 cookie 的。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-127">CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="9dc2d-128">但是，CSRF 攻击并不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-128">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="9dc2d-129">例如，基本和摘要式身份验证也是易受攻击的。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-129">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="9dc2d-130">用户登录时基本或摘要式身份验证后，浏览器会话结束之前会自动发送凭据。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-130">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

<span data-ttu-id="9dc2d-131">注意： 在此上下文中，*会话*指的是在此期间用户进行身份验证的客户端会话。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-131">Note: In this context, *session* refers to the client-side session during which the user is authenticated.</span></span> <span data-ttu-id="9dc2d-132">它是与服务器端会话无关或[会话中间件](xref:fundamentals/app-state)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-132">It's unrelated to server-side sessions or [session middleware](xref:fundamentals/app-state).</span></span>

<span data-ttu-id="9dc2d-133">用户可以防止通过 CSRF 漏洞：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-133">Users can guard against CSRF vulnerabilities by:</span></span>
* <span data-ttu-id="9dc2d-134">在完成使用它们时，日志记录从网站中移出。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-134">Logging off of web sites when they have finished using them.</span></span>
* <span data-ttu-id="9dc2d-135">定期清除其浏览器 cookie。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-135">Clearing their browser's cookies periodically.</span></span>

<span data-ttu-id="9dc2d-136">但是，CSRF 漏洞基本上是 web 应用，而不是最终用户有问题。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-136">However, CSRF vulnerabilities are fundamentally a problem with the web app, not the end user.</span></span>

## <a name="how-does-aspnet-core-mvc-address-csrf"></a><span data-ttu-id="9dc2d-137">ASP.NET 核心 MVC 如何解决 CSRF？</span><span class="sxs-lookup"><span data-stu-id="9dc2d-137">How does ASP.NET Core MVC address CSRF?</span></span>

> [!WARNING]
> <span data-ttu-id="9dc2d-138">ASP.NET 核心实现防 request 伪造使用[ASP.NET 核心数据保护堆栈](xref:security/data-protection/introduction)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-138">ASP.NET Core implements anti-request-forgery using the [ASP.NET Core data protection stack](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="9dc2d-139">ASP.NET 核心数据保护必须配置为在服务器场中正常工作。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-139">ASP.NET Core data protection must be configured to work in a server farm.</span></span> <span data-ttu-id="9dc2d-140">请参阅[配置数据保护](xref:security/data-protection/configuration/overview)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-140">See [Configuring data protection](xref:security/data-protection/configuration/overview) for more information.</span></span>

<span data-ttu-id="9dc2d-141">ASP.NET 核心防 request 伪造默认数据保护配置</span><span class="sxs-lookup"><span data-stu-id="9dc2d-141">ASP.NET Core anti-request-forgery  default data protection configuration</span></span> 

<span data-ttu-id="9dc2d-142">在 ASP.NET 核心 MVC 2.0 [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper)插入 HTML 窗体元素的防伪令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-142">In ASP.NET Core MVC 2.0 the [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) injects anti-forgery tokens for HTML form elements.</span></span> <span data-ttu-id="9dc2d-143">例如，Razor 文件中的以下标记将自动生成防伪令牌：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-143">For example, the following markup in a Razor file will automatically generate anti-forgery tokens:</span></span>

```html
<form method="post">
  <!-- form markup -->
</form>
```

<span data-ttu-id="9dc2d-144">自动生成的防伪令牌 HTML 窗体元素发生时：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-144">The automatic generation of anti-forgery tokens for HTML form elements happens when:</span></span>

* <span data-ttu-id="9dc2d-145">`form`标记包含`method="post"`属性 AND</span><span class="sxs-lookup"><span data-stu-id="9dc2d-145">The `form` tag contains the `method="post"` attribute AND</span></span>

  * <span data-ttu-id="9dc2d-146">操作属性为空。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-146">The action attribute is empty.</span></span> <span data-ttu-id="9dc2d-147">( `action=""`) 或</span><span class="sxs-lookup"><span data-stu-id="9dc2d-147">( `action=""`) OR</span></span>
  * <span data-ttu-id="9dc2d-148">未提供操作属性。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-148">The action attribute isn't supplied.</span></span> <span data-ttu-id="9dc2d-149">(`<form method="post">`)</span><span class="sxs-lookup"><span data-stu-id="9dc2d-149">(`<form method="post">`)</span></span>

<span data-ttu-id="9dc2d-150">您可以禁用自动生成的防伪令牌通过 HTML 窗体元素：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-150">You can disable automatic generation of anti-forgery tokens for HTML form elements by:</span></span>

* <span data-ttu-id="9dc2d-151">显式禁用`asp-antiforgery`。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-151">Explicitly disabling `asp-antiforgery`.</span></span> <span data-ttu-id="9dc2d-152">例如</span><span class="sxs-lookup"><span data-stu-id="9dc2d-152">For example</span></span>

 ```html
  <form method="post" asp-antiforgery="false">
  </form>
  ```

* <span data-ttu-id="9dc2d-153">使用标记帮助器选择标记帮助程序外的窗体元素[！ 选择退出符号](xref:mvc/views/tag-helpers/intro#opt-out)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-153">Opt the form element out of Tag Helpers by using the Tag Helper [! opt-out symbol](xref:mvc/views/tag-helpers/intro#opt-out).</span></span>

 ```html
  <!form method="post">
  </!form>
  ```

* <span data-ttu-id="9dc2d-154">删除`FormTagHelper`从视图。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-154">Remove the `FormTagHelper` from the view.</span></span> <span data-ttu-id="9dc2d-155">你可以删除`FormTagHelper`从视图中向 Razor 视图中添加以下指令：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-155">You can remove the `FormTagHelper` from a view by adding the following directive to the Razor view:</span></span>

 ```html
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> <span data-ttu-id="9dc2d-156">[Razor 页](xref:mvc/razor-pages/index)会自动防范 XSRF/CSRF。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-156">[Razor Pages](xref:mvc/razor-pages/index) are automatically protected from XSRF/CSRF.</span></span> <span data-ttu-id="9dc2d-157">你无需额外编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-157">You don't have to write any additional code.</span></span> <span data-ttu-id="9dc2d-158">请参阅[XSRF/CSRF 和 Razor 页](xref:mvc/razor-pages/index#xsrf)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-158">See [XSRF/CSRF and Razor Pages](xref:mvc/razor-pages/index#xsrf) for more information.</span></span>

<span data-ttu-id="9dc2d-159">防御 CSRF 攻击的最常见方法是同步器令牌模式 (STP)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-159">The most common approach to defending against CSRF attacks is the synchronizer token pattern (STP).</span></span> <span data-ttu-id="9dc2d-160">STP 是在用户请求具有窗体数据的页时使用的方法。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-160">STP is a technique used when the user requests a page with form data.</span></span> <span data-ttu-id="9dc2d-161">服务器将发送到客户端的当前用户的标识与关联的令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-161">The server sends a token associated with the current user's identity to the client.</span></span> <span data-ttu-id="9dc2d-162">客户端返回将令牌发送到服务器以进行验证。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-162">The client sends back the token to the server for verification.</span></span> <span data-ttu-id="9dc2d-163">如果服务器收到与经过身份验证的用户的标识不匹配的令牌，而拒绝该请求。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-163">If the server receives a token that doesn't match the authenticated user's identity, the request is rejected.</span></span> <span data-ttu-id="9dc2d-164">该令牌的唯一且不可预测。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-164">The token is unique and unpredictable.</span></span> <span data-ttu-id="9dc2d-165">该令牌还可用来确保正确地执行序列化的一系列 （确保第 1 页之前之前第 3 页的页 2） 的请求。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-165">The token can also be used to ensure proper sequencing of a series of requests (ensuring page 1 precedes page 2 which precedes page 3).</span></span> <span data-ttu-id="9dc2d-166">ASP.NET 核心 MVC 模板中的所有窗体生成 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-166">All the forms in ASP.NET Core MVC templates generate antiforgery tokens.</span></span> <span data-ttu-id="9dc2d-167">下面的两个示例的视图逻辑生成 antiforgery 令牌：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-167">The following two examples of view logic generate antiforgery tokens:</span></span>

```html
<form asp-controller="Manage" asp-action="ChangePassword" method="post">

</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    
}
```

<span data-ttu-id="9dc2d-168">你可以显式添加到 antiforgery 令牌``<form>``没有标记帮助程序使用的 HTML 帮助程序元素``@Html.AntiForgeryToken``:</span><span class="sxs-lookup"><span data-stu-id="9dc2d-168">You can explicitly add an antiforgery token to a ``<form>`` element without using tag helpers with the HTML helper ``@Html.AntiForgeryToken``:</span></span>


```html
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

<span data-ttu-id="9dc2d-169">在每个前面的情况下，ASP.NET Core 将添加类似于以下的隐藏的表单字段：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-169">In each of the preceding cases, ASP.NET Core will add a hidden form field similar to the following:</span></span>
```html
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkSldwD9CpLRyOtm6FiJB1Jr_F3FQJQDvhlHoLNJJrLA6zaMUmhjMsisu2D2tFkAiYgyWQawJk9vNm36sYP1esHOtamBEPvSk1_x--Sg8Ey2a-d9CV2zHVWIN9MVhvKHOSyKqdZFlYDVd69XYx-rOWPw3ilHGLN6K0Km-1p83jZzF0E4WU5OGg5ns2-m9Yw" />
```

<span data-ttu-id="9dc2d-170">ASP.NET 核心包括三个[筛选器](xref:mvc/controllers/filters)来处理 antiforgery 令牌： ``ValidateAntiForgeryToken``， ``AutoValidateAntiforgeryToken``，和``IgnoreAntiforgeryToken``。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-170">ASP.NET Core includes three [filters](xref:mvc/controllers/filters) for working with antiforgery tokens: ``ValidateAntiForgeryToken``, ``AutoValidateAntiforgeryToken``, and ``IgnoreAntiforgeryToken``.</span></span>

<a name="vaft"></a>

### <a name="validateantiforgerytoken"></a><span data-ttu-id="9dc2d-171">ValidateAntiForgeryToken</span><span class="sxs-lookup"><span data-stu-id="9dc2d-171">ValidateAntiForgeryToken</span></span>

<span data-ttu-id="9dc2d-172">``ValidateAntiForgeryToken``是操作筛选器，可以应用于单个操作，一个控制器或全局范围内。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-172">The ``ValidateAntiForgeryToken`` is an action filter that can be applied to an individual action, a controller, or globally.</span></span> <span data-ttu-id="9dc2d-173">将阻止对已应用此筛选器的操作发出的请求，除非请求包含有效的 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-173">Requests made to actions that have this filter applied will be blocked unless the request includes a valid antiforgery token.</span></span>

```c#
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();
    if (user != null)
    {
        var result = await _userManager.RemoveLoginAsync(user, account.LoginProvider, account.ProviderKey);
        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }
    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

<span data-ttu-id="9dc2d-174">``ValidateAntiForgeryToken``属性修饰，包括对操作方法的请求需要使用令牌`HTTP GET`请求。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-174">The ``ValidateAntiForgeryToken`` attribute requires a token for requests to action methods it decorates, including `HTTP GET` requests.</span></span> <span data-ttu-id="9dc2d-175">如果广泛应用，你可以重写它与``IgnoreAntiforgeryToken``属性。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-175">If you apply it broadly, you can override it with the ``IgnoreAntiforgeryToken`` attribute.</span></span>

### <a name="autovalidateantiforgerytoken"></a><span data-ttu-id="9dc2d-176">AutoValidateAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="9dc2d-176">AutoValidateAntiforgeryToken</span></span>

<span data-ttu-id="9dc2d-177">ASP.NET Core 应用通常不生成 antiforgery 令牌安全 HTTP 方法 （GET、 HEAD、 选项和跟踪）。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-177">ASP.NET Core apps generally don't generate antiforgery tokens for HTTP safe methods (GET, HEAD, OPTIONS, and TRACE).</span></span> <span data-ttu-id="9dc2d-178">而不是广泛应用``ValidateAntiForgeryToken``属性，然后重写它与``IgnoreAntiforgeryToken``属性，可以使用``AutoValidateAntiforgeryToken``属性。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-178">Instead of broadly applying the ``ValidateAntiForgeryToken`` attribute and then overriding it with ``IgnoreAntiforgeryToken`` attributes, you can use the ``AutoValidateAntiforgeryToken`` attribute.</span></span> <span data-ttu-id="9dc2d-179">此属性适用类似``ValidateAntiForgeryToken``特性，只不过它不需要使用以下的 HTTP 方法发出的请求令牌：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-179">This attribute works identically to the ``ValidateAntiForgeryToken`` attribute, except that it doesn't require tokens for requests made using the following HTTP methods:</span></span>

* <span data-ttu-id="9dc2d-180">GET</span><span class="sxs-lookup"><span data-stu-id="9dc2d-180">GET</span></span>
* <span data-ttu-id="9dc2d-181">HEAD</span><span class="sxs-lookup"><span data-stu-id="9dc2d-181">HEAD</span></span>
* <span data-ttu-id="9dc2d-182">选项</span><span class="sxs-lookup"><span data-stu-id="9dc2d-182">OPTIONS</span></span>
* <span data-ttu-id="9dc2d-183">TRACE</span><span class="sxs-lookup"><span data-stu-id="9dc2d-183">TRACE</span></span>

<span data-ttu-id="9dc2d-184">我们建议你使用``AutoValidateAntiforgeryToken``广泛的非 API 方案。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-184">We recommend you use ``AutoValidateAntiforgeryToken`` broadly for non-API scenarios.</span></span> <span data-ttu-id="9dc2d-185">这可确保你的 POST 操作保护默认情况下。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-185">This ensures your POST actions are protected by default.</span></span> <span data-ttu-id="9dc2d-186">替代项是默认情况下，将忽略 antiforgery 令牌除非``ValidateAntiForgeryToken``应用于各个操作的方法。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-186">The alternative is to ignore antiforgery tokens by default, unless ``ValidateAntiForgeryToken`` is applied to the individual action method.</span></span> <span data-ttu-id="9dc2d-187">在此方案中的 POST 操作方法是更有可能不受保护，使你的应用程序容易受到 CSRF 攻击的左侧。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-187">It's more likely in this scenario for a POST action method to be left unprotected, leaving your app vulnerable to CSRF attacks.</span></span> <span data-ttu-id="9dc2d-188">即使匿名文章应发送 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-188">Even anonymous POSTS should send the antiforgery token.</span></span>

<span data-ttu-id="9dc2d-189">注意： Api 没有一种用于发送令牌; 的非 cookie 一部分的自动机制您的实现可能将取决于你的客户端代码实现。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-189">Note: APIs don't have an automatic mechanism for sending the non-cookie part of the token; your implementation will likely depend on your client code implementation.</span></span> <span data-ttu-id="9dc2d-190">下面显示了一些示例。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-190">Some examples are shown below.</span></span>


<span data-ttu-id="9dc2d-191">示例 （类级别）：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-191">Example (class level):</span></span>

```c#
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

<span data-ttu-id="9dc2d-192">示例 （全局）：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-192">Example (global):</span></span>

```c#
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

<a name="iaft"></a>

### <a name="ignoreantiforgerytoken"></a><span data-ttu-id="9dc2d-193">IgnoreAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="9dc2d-193">IgnoreAntiforgeryToken</span></span>

<span data-ttu-id="9dc2d-194">``IgnoreAntiforgeryToken``使用筛选器以消除 antiforgery 令牌为给定操作 （或控制器） 的需要。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-194">The ``IgnoreAntiforgeryToken`` filter is used to eliminate the need for an antiforgery token to be present for a given action (or controller).</span></span> <span data-ttu-id="9dc2d-195">当应用时，此筛选器将重写``ValidateAntiForgeryToken``和/或``AutoValidateAntiforgeryToken``（全局或在控制器上） 在高级别指定筛选器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-195">When applied, this filter will override ``ValidateAntiForgeryToken`` and/or ``AutoValidateAntiforgeryToken`` filters specified at a higher level (globally or on a controller).</span></span>

```c#
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

## <a name="javascript-ajax-and-spas"></a><span data-ttu-id="9dc2d-196">JavaScript、 AJAX 和 Spa</span><span class="sxs-lookup"><span data-stu-id="9dc2d-196">JavaScript, AJAX, and SPAs</span></span>

<span data-ttu-id="9dc2d-197">在传统的基于 HTML 的应用程序，antiforgery 令牌将传递到使用隐藏的表单域的服务器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-197">In traditional HTML-based applications, antiforgery tokens are passed to the server using hidden form fields.</span></span> <span data-ttu-id="9dc2d-198">在基于 JavaScript 的现代应用和单页面应用程序 (Spa)，以编程方式进行多请求。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-198">In modern JavaScript-based apps and single page applications (SPAs), many requests are made programmatically.</span></span> <span data-ttu-id="9dc2d-199">这些 AJAX 请求可能使用其他方法 （如请求标头或 cookie） 将该令牌发送。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-199">These AJAX requests may use other techniques (such as request headers or cookies) to send the token.</span></span> <span data-ttu-id="9dc2d-200">如果使用 cookie 来存储身份验证令牌，并在服务器上的 API 请求进行身份验证，则 CSRF 将的潜在问题。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-200">If cookies are used to store authentication tokens and to authenticate API requests on the server, then CSRF will be a potential problem.</span></span> <span data-ttu-id="9dc2d-201">但是，如果本地存储用于存储令牌，CSRF 漏洞，可以缓解，因为从本地存储的值不会自动发送到每个新请求服务器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-201">However, if local storage is used to store the token, CSRF vulnerability may be mitigated, since values from local storage are not sent automatically to the server with every new request.</span></span> <span data-ttu-id="9dc2d-202">因此，使用本地存储来存储客户端和发送令牌，因为请求标头是建议的方法上的 antiforgery 令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-202">Thus, using local storage to store the antiforgery token on the client and sending the token as a request header is a recommended approach.</span></span>

### <a name="angularjs"></a><span data-ttu-id="9dc2d-203">AngularJS</span><span class="sxs-lookup"><span data-stu-id="9dc2d-203">AngularJS</span></span>

<span data-ttu-id="9dc2d-204">AngularJS 使用到地址 CSRF 的约定。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-204">AngularJS uses a convention to address CSRF.</span></span> <span data-ttu-id="9dc2d-205">如果服务器发送具有该名称的 cookie ``XSRF-TOKEN``，角``$http``服务将添加的值此 cookie 到标头时它将请求发送到此服务器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-205">If the server sends a cookie with the name ``XSRF-TOKEN``, the Angular ``$http`` service will add the value from this cookie to a header when it sends a request to this server.</span></span> <span data-ttu-id="9dc2d-206">此过程是自动;你不需要显式设置标头。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-206">This process is automatic; you don't need to set the header explicitly.</span></span> <span data-ttu-id="9dc2d-207">标头名称是``X-XSRF-TOKEN``。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-207">The header name is ``X-XSRF-TOKEN``.</span></span> <span data-ttu-id="9dc2d-208">服务器应检测此标头，并验证其内容。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-208">The server should detect this header and validate its contents.</span></span>

<span data-ttu-id="9dc2d-209">有关 ASP.NET 核心 API 使用此约定：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-209">For ASP.NET Core API work with this convention:</span></span>

* <span data-ttu-id="9dc2d-210">配置你的应用程序提供在 cookie 中调用的令牌``XSRF-TOKEN``</span><span class="sxs-lookup"><span data-stu-id="9dc2d-210">Configure your app to provide a token in a cookie called ``XSRF-TOKEN``</span></span>
* <span data-ttu-id="9dc2d-211">配置 antiforgery 服务以查找名为的标头``X-XSRF-TOKEN``</span><span class="sxs-lookup"><span data-stu-id="9dc2d-211">Configure the antiforgery service to look for a header named ``X-XSRF-TOKEN``</span></span>

```c#
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

<span data-ttu-id="9dc2d-212">[查看示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-212">[View sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample).</span></span>

### <a name="javascript"></a><span data-ttu-id="9dc2d-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9dc2d-213">JavaScript</span></span>

<span data-ttu-id="9dc2d-214">使用视图支持 JavaScript，你可以创建使用从您的视图中的服务的令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-214">Using JavaScript with views, you can create the token using a service from within your view.</span></span> <span data-ttu-id="9dc2d-215">为此，请将注入`Microsoft.AspNetCore.Antiforgery.IAntiforgery`到视图并调用服务`GetAndStoreTokens`，如所示：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-215">To do so, you inject the `Microsoft.AspNetCore.Antiforgery.IAntiforgery` service into the view and call `GetAndStoreTokens`, as shown:</span></span>

[!code-csharp[Main](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,24)]

<span data-ttu-id="9dc2d-216">此方法不需要直接处理从服务器设置 cookie 或从客户端读取它们。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-216">This approach eliminates the need to deal directly with setting cookies from the server or reading them from the client.</span></span>

<span data-ttu-id="9dc2d-217">JavaScript 可以还访问 cookie 中, 提供的令牌，然后使用 cookie 的内容创建的标头与令牌的值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-217">JavaScript can also access tokens provided in cookies, and then use the cookie's contents to create a header with the token's value, as shown below.</span></span>

```c#
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
  new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

<span data-ttu-id="9dc2d-218">然后，假设构造脚本请求将该令牌发送调用标头中``X-CSRF-TOKEN``，配置 antiforgery 服务以查找``X-CSRF-TOKEN``标头：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-218">Then, assuming you construct your script requests to send the token in a header called ``X-CSRF-TOKEN``, configure the antiforgery service to look for the ``X-CSRF-TOKEN`` header:</span></span>

```c#
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

<span data-ttu-id="9dc2d-219">下面的示例使用 jQuery 发出 AJAX 请求与相应的标头：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-219">The following example uses jQuery to make an AJAX request with the appropriate header:</span></span>

```javascript
var csrfToken = $.cookie("CSRF-TOKEN");

$.ajax({
    url: "/api/password/changepassword",
    contentType: "application/json",
    data: JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }),
    type: "POST",
    headers: {
        "X-CSRF-TOKEN": csrfToken
    }
});
```

## <a name="configuring-antiforgery"></a><span data-ttu-id="9dc2d-220">配置 Antiforgery</span><span class="sxs-lookup"><span data-stu-id="9dc2d-220">Configuring Antiforgery</span></span>

<span data-ttu-id="9dc2d-221">`IAntiforgery`提供要配置 antiforgery 系统的 API。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-221">`IAntiforgery` provides the API to configure the antiforgery system.</span></span> <span data-ttu-id="9dc2d-222">它可以在请求`Configure`方法`Startup`类。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-222">It can be requested in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="9dc2d-223">下面的示例使用从应用程序的主页上的中间件生成 antiforgery 令牌并将其发送响应中将其作为 cookie （使用上文所述的默认角度命名约定）：</span><span class="sxs-lookup"><span data-stu-id="9dc2d-223">The following example uses middleware from the app's home page to generate an antiforgery token and send it in the response as a cookie (using the default Angular naming convention described above):</span></span>


```c#
public void Configure(IApplicationBuilder app, 
    IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;
        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // We can send the request token as a JavaScript-readable cookie, 
            // and Angular will use it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
    //
}
```

### <a name="options"></a><span data-ttu-id="9dc2d-224">选项</span><span class="sxs-lookup"><span data-stu-id="9dc2d-224">Options</span></span>

<span data-ttu-id="9dc2d-225">你可以自定义[antiforgery 选项](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions#fields_summary)中`ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="9dc2d-225">You can customize [antiforgery options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions#fields_summary) in `ConfigureServices`:</span></span>

```c#
services.AddAntiforgery(options => 
{
  options.CookieDomain = "mydomain.com";
  options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
  options.CookiePath = "Path";
  options.FormFieldName = "AntiforgeryFieldname";
  options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
  options.RequireSsl = false;
  options.SuppressXFrameOptionsHeader = false;
});
```

<!-- QAfix fix table -->

|<span data-ttu-id="9dc2d-226">选项</span><span class="sxs-lookup"><span data-stu-id="9dc2d-226">Option</span></span>        | <span data-ttu-id="9dc2d-227">描述</span><span class="sxs-lookup"><span data-stu-id="9dc2d-227">Description</span></span> |
|------------- | ----------- |
|<span data-ttu-id="9dc2d-228">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="9dc2d-228">CookieDomain</span></span>  | <span data-ttu-id="9dc2d-229">Cookie 的域。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-229">The domain of the cookie.</span></span> <span data-ttu-id="9dc2d-230">默认为 `null`。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-230">Defaults to `null`.</span></span> |
|<span data-ttu-id="9dc2d-231">CookieName</span><span class="sxs-lookup"><span data-stu-id="9dc2d-231">CookieName</span></span>    | <span data-ttu-id="9dc2d-232">Cookie 的名称。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-232">The name of the cookie.</span></span> <span data-ttu-id="9dc2d-233">如果未设置，系统将生成一个唯一的名称开头`DefaultCookiePrefix`("。AspNetCore.Antiforgery。") 下。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-233">If not set, the system will generate a unique name beginning with the `DefaultCookiePrefix` (".AspNetCore.Antiforgery.").</span></span> |
|<span data-ttu-id="9dc2d-234">CookiePath</span><span class="sxs-lookup"><span data-stu-id="9dc2d-234">CookiePath</span></span>    | <span data-ttu-id="9dc2d-235">在 cookie 上设置的路径。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-235">The path set on the cookie.</span></span> |
|<span data-ttu-id="9dc2d-236">FormFieldName</span><span class="sxs-lookup"><span data-stu-id="9dc2d-236">FormFieldName</span></span> | <span data-ttu-id="9dc2d-237">Antiforgery 系统用于呈现 antiforgery 令牌在视图中的隐藏的表单字段的名称。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-237">The name of the hidden form field used by the antiforgery system to render antiforgery tokens in views.</span></span> |
|<span data-ttu-id="9dc2d-238">HeaderName</span><span class="sxs-lookup"><span data-stu-id="9dc2d-238">HeaderName</span></span>    | <span data-ttu-id="9dc2d-239">Antiforgery 系统使用的标头的名称。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-239">The name of the header used by the antiforgery system.</span></span> <span data-ttu-id="9dc2d-240">如果`null`，则系统将考虑仅窗体数据。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-240">If `null`, the system will consider only form data.</span></span> |
|<span data-ttu-id="9dc2d-241">RequireSsl</span><span class="sxs-lookup"><span data-stu-id="9dc2d-241">RequireSsl</span></span>    | <span data-ttu-id="9dc2d-242">指定是否由 antiforgery 系统需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-242">Specifies whether SSL is required by the antiforgery system.</span></span> <span data-ttu-id="9dc2d-243">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-243">Defaults to `false`.</span></span> <span data-ttu-id="9dc2d-244">如果`true`，非 SSL 请求将会失败。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-244">If `true`, non-SSL requests will fail.</span></span> |
|<span data-ttu-id="9dc2d-245">SuppressXFrameOptionsHeader</span><span class="sxs-lookup"><span data-stu-id="9dc2d-245">SuppressXFrameOptionsHeader</span></span>  | <span data-ttu-id="9dc2d-246">指定是否禁止生成`X-Frame-Options`标头。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-246">Specifies whether to suppress generation of the `X-Frame-Options` header.</span></span> <span data-ttu-id="9dc2d-247">默认情况下，值为"SAMEORIGIN"生成标头。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-247">By default, the header is generated with a value of "SAMEORIGIN".</span></span> <span data-ttu-id="9dc2d-248">默认为 `false`。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-248">Defaults to `false`.</span></span> |

<span data-ttu-id="9dc2d-249">请参阅 https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.cookieauthenticationoptions 有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-249">See https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.cookieauthenticationoptions for more info.</span></span>

### <a name="extending-antiforgery"></a><span data-ttu-id="9dc2d-250">扩展 Antiforgery</span><span class="sxs-lookup"><span data-stu-id="9dc2d-250">Extending Antiforgery</span></span>

<span data-ttu-id="9dc2d-251">[IAntiForgeryAdditionalDataProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider)类型允许开发人员通过往返中每个令牌的其他数据扩展的 ANTI-XSRF 系统的行为。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-251">The [IAntiForgeryAdditionalDataProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) type allows developers to extend the behavior of the anti-XSRF system by round-tripping additional data in each token.</span></span> <span data-ttu-id="9dc2d-252">[GetAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_GetAdditionalData_Microsoft_AspNetCore_Http_HttpContext_)每次调用方法生成的字段标记，和在生成的标记内嵌入的返回值。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-252">The [GetAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_GetAdditionalData_Microsoft_AspNetCore_Http_HttpContext_) method is called each time a field token is generated, and the return value is embedded within the generated token.</span></span> <span data-ttu-id="9dc2d-253">实施者无法返回时间戳、 nonce 或任何其他值，然后调用[ValidateAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_ValidateAdditionalData_Microsoft_AspNetCore_Http_HttpContext_System_String_)时验证令牌验证此数据。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-253">An implementer could return a timestamp, a nonce, or any other value and then call [ValidateAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_ValidateAdditionalData_Microsoft_AspNetCore_Http_HttpContext_System_String_) to validate this data when the token is validated.</span></span> <span data-ttu-id="9dc2d-254">客户端的用户名已嵌入在生成的令牌中，因此无需包括此信息。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-254">The client's username is already embedded in the generated tokens, so there's no need to include this information.</span></span> <span data-ttu-id="9dc2d-255">如果令牌包括补充数据但不是`IAntiForgeryAdditionalDataProvider`已配置，不验证补充数据。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-255">If a token includes supplemental data but no `IAntiForgeryAdditionalDataProvider` has been configured, the supplemental data isn't validated.</span></span>

## <a name="fundamentals"></a><span data-ttu-id="9dc2d-256">基础知识</span><span class="sxs-lookup"><span data-stu-id="9dc2d-256">Fundamentals</span></span>

<span data-ttu-id="9dc2d-257">CSRF 攻击依赖于发送与每个请求都会到该域的域关联的 cookie 的默认浏览器的行为。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-257">CSRF attacks rely on the default browser behavior of sending cookies associated with a domain with every request made to that domain.</span></span> <span data-ttu-id="9dc2d-258">这些 cookie 存储在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-258">These cookies are stored within the browser.</span></span> <span data-ttu-id="9dc2d-259">它们通常包括身份验证的用户的会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-259">They frequently include session cookies for authenticated users.</span></span> <span data-ttu-id="9dc2d-260">基于 cookie 的身份验证是一种身份验证的常用形式。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-260">Cookie-based authentication is a popular form of authentication.</span></span> <span data-ttu-id="9dc2d-261">基于令牌的身份验证系统一直增长中受欢迎程度，特别是对于 Spa 和其他"智能客户端"方案。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-261">Token-based authentication systems have been growing in popularity, especially for SPAs and other "smart client" scenarios.</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="9dc2d-262">基于 cookie 的身份验证</span><span class="sxs-lookup"><span data-stu-id="9dc2d-262">Cookie-based authentication</span></span>

<span data-ttu-id="9dc2d-263">一旦用户已经使用其用户名和密码身份验证，它们被颁发一个令牌，可用来将它们标识和验证它们进行了身份验证。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-263">Once a user has authenticated using their username and password, they're issued a token that can be used to identify them and validate that they have been authenticated.</span></span> <span data-ttu-id="9dc2d-264">随着工作的附带的每个请求客户端的 cookie 的令牌存储。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-264">The token is stored as a cookie that accompanies every request the client makes.</span></span> <span data-ttu-id="9dc2d-265">生成和验证此 cookie 可通过 cookie 身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-265">Generating and validating this cookie is done by the cookie authentication middleware.</span></span> <span data-ttu-id="9dc2d-266">ASP.NET Core 提供 cookie[中间件](../fundamentals/middleware.md)其用户主体序列化为的加密 cookie，然后，在后续请求中，将验证该 cookie，重新创建主体，并将它分配给`User`属性`HttpContext`.</span><span class="sxs-lookup"><span data-stu-id="9dc2d-266">ASP.NET Core provides cookie [middleware](../fundamentals/middleware.md) which serializes a user principal into an encrypted cookie and then, on subsequent requests, validates the cookie, recreates the principal and assigns it to the `User` property on `HttpContext`.</span></span>

<span data-ttu-id="9dc2d-267">当使用 cookie 时，身份验证 cookie 只是一个容器的窗体身份验证票证。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-267">When a cookie is used, The authentication cookie is just a container for the forms authentication ticket.</span></span> <span data-ttu-id="9dc2d-268">票证作为随每个请求的窗体身份验证 cookie 的值传递和 forms 身份验证，在服务器上，用于标识已经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-268">The ticket is passed as the value of the forms authentication cookie with each request and is used by forms authentication, on the server, to identify an authenticated user.</span></span>

<span data-ttu-id="9dc2d-269">当用户登录到系统时，用户会话在服务器端上创建并存储在数据库或某些其他持久存储区中。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-269">When a user is logged in to a system, a user session is created on the server-side and is stored in a database or some other persistent store.</span></span> <span data-ttu-id="9dc2d-270">系统生成在数据存储指向实际会话的会话密钥，并将其作为客户端端 cookie 发送。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-270">The system generates a session key that points to the actual session in the data store and it's sent as a client side cookie.</span></span> <span data-ttu-id="9dc2d-271">Web 服务器将检查此会话密钥的用户请求的资源要求获得授权的任何时间。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-271">The web server will check this session key any time a user requests a resource that requires authorization.</span></span> <span data-ttu-id="9dc2d-272">系统会检查关联的用户会话是否有权访问请求的资源。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-272">The system checks whether the associated user session has the privilege to access the requested resource.</span></span> <span data-ttu-id="9dc2d-273">如果是这样，请求将继续。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-273">If so, the request continues.</span></span> <span data-ttu-id="9dc2d-274">否则，请求将返回未授权。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-274">Otherwise, the request returns as not authorized.</span></span> <span data-ttu-id="9dc2d-275">在此方法中，使用 cookie 使似乎是有状态应用程序，因为它是能够"记住"的用户具有先前进行身份验证与服务器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-275">In this approach, cookies are used to make the application appear to be stateful, since it's able to "remember" that the user has previously authenticated with the server.</span></span>

### <a name="user-tokens"></a><span data-ttu-id="9dc2d-276">用户令牌</span><span class="sxs-lookup"><span data-stu-id="9dc2d-276">User tokens</span></span>

<span data-ttu-id="9dc2d-277">基于令牌的身份验证不存储在服务器上的会话。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-277">Token-based authentication doesn't store session on the server.</span></span> <span data-ttu-id="9dc2d-278">当用户登录时，它们被颁发一个令牌 （不 antiforgery 令牌）。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-278">When a user is logged in, they're issued a token (not an antiforgery token).</span></span> <span data-ttu-id="9dc2d-279">此令牌包含要求该令牌进行验证的数据。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-279">This token holds the data that's required to validate the token.</span></span> <span data-ttu-id="9dc2d-280">它还包含中的窗体的用户信息[声明](https://docs.microsoft.com/dotnet/framework/security/claims-based-identity-model)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-280">It also contains user information in the form of [claims](https://docs.microsoft.com/dotnet/framework/security/claims-based-identity-model).</span></span> <span data-ttu-id="9dc2d-281">当用户想要访问要求进行身份验证的服务器资源时，令牌将发送至的其他授权标头中的持有者 {令牌} 形式的服务器。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-281">When a user wants to access a server resource requiring authentication, the token is sent to the server with an additional authorization header in form of Bearer {token}.</span></span> <span data-ttu-id="9dc2d-282">这使得应用程序无状态，因为在每个后续请求令牌中传递请求服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-282">This makes the application stateless since in each subsequent request the token is passed in the request for server-side validation.</span></span> <span data-ttu-id="9dc2d-283">此令牌不*加密*; 而是*编码*。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-283">This token isn't *encrypted*; rather it's *encoded*.</span></span> <span data-ttu-id="9dc2d-284">在服务器端，都可以解码令牌来访问令牌中的原始信息。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-284">On the server-side, the token can be decoded to access the raw information within the token.</span></span> <span data-ttu-id="9dc2d-285">若要在后续请求中发送令牌，或者将其存储在浏览器的本地存储中或在一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-285">To send the token in subsequent requests, either store it in the browser's local storage or in a cookie.</span></span> <span data-ttu-id="9dc2d-286">不必担心 XSRF 漏洞，如果的令牌存储在本地存储区，但如果的令牌存储在一个 cookie，则会出现问题。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-286">Don't worry about XSRF vulnerability if the token is stored in the local storage, but it's an issue if the token is stored in a cookie.</span></span>

### <a name="multiple-applications-are-hosted-in-one-domain"></a><span data-ttu-id="9dc2d-287">在一个域中托管多个应用程序</span><span class="sxs-lookup"><span data-stu-id="9dc2d-287">Multiple applications are hosted in one domain</span></span>

<span data-ttu-id="9dc2d-288">尽管`example1.cloudapp.net`和`example2.cloudapp.net`是不同的主机下的主机之间没有隐式信任关系`*.cloudapp.net`域。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-288">Although `example1.cloudapp.net` and `example2.cloudapp.net` are different hosts, there's an implicit trust relationship between hosts under the `*.cloudapp.net` domain.</span></span> <span data-ttu-id="9dc2d-289">此隐式信任关系允许影响对方的 cookie （控制 AJAX 请求的同源策略不一定适用于 HTTP cookie） 可能不受信任的主机。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-289">This implicit trust relationship allows potentially untrusted hosts to affect each other's cookies (the same-origin policies that govern AJAX requests don't necessarily apply to HTTP cookies).</span></span> <span data-ttu-id="9dc2d-290">ASP.NET 核心运行时，用户名将嵌入到字段标记提供一些缓解。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-290">The ASP.NET Core runtime provides some mitigation in that the username is embedded into the field token.</span></span> <span data-ttu-id="9dc2d-291">即使恶意子域能够覆盖会话令牌，它无法生成用户的有效字段令牌。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-291">Even if a malicious subdomain is able to overwrite a session token, it can't generate a valid field token for the user.</span></span> <span data-ttu-id="9dc2d-292">当承载于此类环境中，内置的 ANTI-XSRF 例程仍不能抵御会话劫持或登录名 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-292">When hosted in such an environment, the built-in anti-XSRF routines still can't defend against session hijacking or login CSRF attacks.</span></span> <span data-ttu-id="9dc2d-293">共享宿主环境为 vunerable 会话劫持、 登录 CSRF，和其他的攻击。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-293">Shared hosting environments are vunerable to session hijacking, login CSRF, and other attacks.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="9dc2d-294">其他资源</span><span class="sxs-lookup"><span data-stu-id="9dc2d-294">Additional resources</span></span>

* <span data-ttu-id="9dc2d-295">[XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))上[打开 Web 应用程序安全项目](https://www.owasp.org/index.php/Main_Page)(OWASP)。</span><span class="sxs-lookup"><span data-stu-id="9dc2d-295">[XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) on [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP).</span></span>
