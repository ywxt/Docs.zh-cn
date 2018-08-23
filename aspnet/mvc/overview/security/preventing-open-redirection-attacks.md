---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 阻止打开重定向攻击 (C#) |Microsoft Docs
author: jongalloway
description: 本教程介绍了如何在 ASP.NET MVC 应用程序中阻止打开重定向攻击。 本教程讨论所做的更改...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 767f9c85527fbcdf34e700eb32fe0c6cad30bf0c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832519"
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="971f6-104">阻止打开重定向攻击 (C#)</span><span class="sxs-lookup"><span data-stu-id="971f6-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="971f6-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="971f6-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="971f6-106">本教程介绍了如何在 ASP.NET MVC 应用程序中阻止打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="971f6-107">本教程讨论在 AccountController 中在 ASP.NET MVC 3 中所做的更改，并演示如何在现有的 ASP.NET MVC 1.0 和 2 个应用程序中应用这些更改。</span><span class="sxs-lookup"><span data-stu-id="971f6-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="971f6-108">打开重定向攻击是什么？</span><span class="sxs-lookup"><span data-stu-id="971f6-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="971f6-109">将重定向到的 URL，例如查询字符串或窗体数据的请求通过指定任何 web 应用程序可以有可能被篡改，同时将用户重定向到恶意的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="971f6-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="971f6-110">此篡改称为开放重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="971f6-111">每当应用程序逻辑将重定向到指定的 URL，必须验证重定向 URL 尚未被篡改。</span><span class="sxs-lookup"><span data-stu-id="971f6-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="971f6-112">为 ASP.NET MVC 1.0 和 ASP.NET MVC 2 默认 AccountController 中使用的登录名是易受攻击，以打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="971f6-113">幸运的是，很容易地更新现有的应用程序以使用从 ASP.NET MVC 3 预览版的更正。</span><span class="sxs-lookup"><span data-stu-id="971f6-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="971f6-114">若要了解此漏洞，让我们看一下默认 ASP.NET MVC 2 Web 应用程序项目中的登录重定向工作原理。</span><span class="sxs-lookup"><span data-stu-id="971f6-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="971f6-115">在此应用程序，尝试访问具有 [Authorize] 特性的控制器操作将重定向未经授权的用户到 /Account/LogOn 视图。</span><span class="sxs-lookup"><span data-stu-id="971f6-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="971f6-116">此重定向到 /Account/LogOn，以便用户可以返回到最初请求的 URL，它们已成功登录后将 returnUrl 查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="971f6-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="971f6-117">在下面的屏幕截图，我们可以看到，尝试访问 /Account/ChangePassword 视图未登录时导致重定向到 /Account/LogOn？ReturnUrl = %2faccount%2fChangePassword %2f。</span><span class="sxs-lookup"><span data-stu-id="971f6-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="971f6-118">**图 01**： 支持开放重定向的登录页</span><span class="sxs-lookup"><span data-stu-id="971f6-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="971f6-119">由于不验证 ReturnUrl 查询字符串参数，因此攻击者可以修改它以将任何 URL 地址注入到要执行的开放重定向攻击的参数。</span><span class="sxs-lookup"><span data-stu-id="971f6-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="971f6-120">若要说明这一点，我们可以修改的 ReturnUrl 参数[ http://bing.com ](http://bing.com)，因此将生成的登录名 URL/帐户/登录？ReturnUrl =<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="971f6-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="971f6-121">在成功登录到站点后, 我们将重定向到[ http://bing.com ](http://bing.com)。</span><span class="sxs-lookup"><span data-stu-id="971f6-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="971f6-122">由于不验证此重定向，因此它可以改为指向恶意站点，试图欺骗用户。</span><span class="sxs-lookup"><span data-stu-id="971f6-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="971f6-123">更复杂的开放重定向攻击</span><span class="sxs-lookup"><span data-stu-id="971f6-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="971f6-124">打开重定向攻击是尤其危险，因为攻击者知道，我们正在尝试登录到特定的网站，这将使我们受到[钓鱼攻击](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="971f6-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="971f6-125">例如，攻击者可能发送恶意电子邮件向网站用户在尝试捕获其密码。</span><span class="sxs-lookup"><span data-stu-id="971f6-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="971f6-126">让我们看看这工作原理 NerdDinner 站点上。</span><span class="sxs-lookup"><span data-stu-id="971f6-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="971f6-127">（请注意，已更新 NerdDinner 现场开放重定向攻击。）</span><span class="sxs-lookup"><span data-stu-id="971f6-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="971f6-128">首先，攻击者向我们发送一个链接到 NerdDinner 包括重定向到其伪造的页面上的登录页：</span><span class="sxs-lookup"><span data-stu-id="971f6-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="971f6-129">请注意，返回 URL 指向 nerddiner.com，缺少"n"从 word dinner。</span><span class="sxs-lookup"><span data-stu-id="971f6-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="971f6-130">在此示例中，这是，攻击者控制的域。</span><span class="sxs-lookup"><span data-stu-id="971f6-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="971f6-131">当我们访问上面的链接时，我们会转到合法 NerdDinner.com 登录页。</span><span class="sxs-lookup"><span data-stu-id="971f6-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="971f6-132">**图 02**: NerdDinner 的开放重定向的登录页</span><span class="sxs-lookup"><span data-stu-id="971f6-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="971f6-133">我们正确登录时，ASP.NET MVC AccountController 的登录操作将重我们定向到 returnUrl 查询字符串参数中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="971f6-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="971f6-134">在这种情况下，它是攻击者已进入，即的 URL [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="971f6-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="971f6-135">除非我们非常密切，它是很有可能，我们不会发现此问题，特别是因为攻击者已小心，确保其伪造的页面看起来完全一样的合法的登录页。</span><span class="sxs-lookup"><span data-stu-id="971f6-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="971f6-136">此登录页包括错误消息，请求我们再次登录。</span><span class="sxs-lookup"><span data-stu-id="971f6-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="971f6-137">不太妥当我们，我们必须有误我们的密码。</span><span class="sxs-lookup"><span data-stu-id="971f6-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="971f6-138">**图 03**： 伪造 NerdDinner 登录屏幕</span><span class="sxs-lookup"><span data-stu-id="971f6-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="971f6-139">当我们重新键入我们的用户名和密码时，伪造的登录页会将信息保存，并向我们发送回合法 NerdDinner.com 站点。</span><span class="sxs-lookup"><span data-stu-id="971f6-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="971f6-140">此时，NerdDinner.com 站点具有已进行身份验证，因而伪造的登录页可以直接访问该页面将重定向。</span><span class="sxs-lookup"><span data-stu-id="971f6-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="971f6-141">最终结果是，攻击者有我们的用户名和密码，并且我们不知道，我们已向其提供它。</span><span class="sxs-lookup"><span data-stu-id="971f6-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="971f6-142">查看 AccountController 登录操作中的易受攻击代码</span><span class="sxs-lookup"><span data-stu-id="971f6-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="971f6-143">ASP.NET MVC 2 应用程序中的登录操作的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="971f6-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="971f6-144">请注意，一旦成功登录，将控制器返回重定向到 returnUrl。</span><span class="sxs-lookup"><span data-stu-id="971f6-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="971f6-145">您可以看到针对 returnUrl 参数执行任何验证。</span><span class="sxs-lookup"><span data-stu-id="971f6-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="971f6-146">**代码清单 1 – 在 ASP.NET MVC 2 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="971f6-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="971f6-147">现在让我们看看对 ASP.NET MVC 3 登录操作的更改。</span><span class="sxs-lookup"><span data-stu-id="971f6-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="971f6-148">此代码已更改，以便通过名为 System.Web.Mvc.Url 帮助程序类中调用新方法验证 returnUrl 参数`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="971f6-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="971f6-149">**代码清单 2 – 在 ASP.NET MVC 3 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="971f6-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="971f6-150">这已更改为在 System.Web.Mvc.Url 帮助程序类中，调用新方法来验证返回 URL 参数`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="971f6-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="971f6-151">保护 ASP.NET MVC 1.0 和 MVC 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="971f6-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="971f6-152">我们可以利用 ASP.NET MVC 3 更改我们现有的 ASP.NET MVC 1.0 和 2 个应用程序中通过添加 IsLocalUrl() 帮助器方法并更新要验证的 returnUrl 参数的登录操作。</span><span class="sxs-lookup"><span data-stu-id="971f6-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="971f6-153">ASP.NET Web Pages 应用程序还使用 UrlHelper IsLocalUrl() 方法实际上就调用中 System.Web.WebPages，作为此验证的方法。</span><span class="sxs-lookup"><span data-stu-id="971f6-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="971f6-154">**代码清单 3 – 从 ASP.NET MVC 3 UrlHelper IsLocalUrl() 方法 `class`**</span><span class="sxs-lookup"><span data-stu-id="971f6-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="971f6-155">IsUrlLocalToHost 方法包含的实际验证逻辑，如列表 4 中所示。</span><span class="sxs-lookup"><span data-stu-id="971f6-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="971f6-156">**列表 4 – 从 System.Web.WebPages 为 RequestExtensions 类 IsUrlLocalToHost() 方法**</span><span class="sxs-lookup"><span data-stu-id="971f6-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="971f6-157">在我们的 ASP.NET MVC 1.0 或 2 个应用程序中，我们将向 AccountController 中，添加 IsLocalUrl() 方法，但最好尽可能将其添加到一个单独的帮助器类。</span><span class="sxs-lookup"><span data-stu-id="971f6-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="971f6-158">我们将两个较小的更改 IsLocalUrl() 的 ASP.NET MVC 3 版本，以便它将在 AccountController 中工作。</span><span class="sxs-lookup"><span data-stu-id="971f6-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="971f6-159">首先，我们将更改它通过公共方法为私有方法，因为控制器中的公共方法可作为控制器操作进行访问。</span><span class="sxs-lookup"><span data-stu-id="971f6-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="971f6-160">其次，我们将修改检查针对应用程序主机 URL 主机的调用。</span><span class="sxs-lookup"><span data-stu-id="971f6-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="971f6-161">调用将使用的本地 RequestContext UrlHelper 类中的字段。</span><span class="sxs-lookup"><span data-stu-id="971f6-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="971f6-162">而不是使用这种情况。RequestContext.HttpContext.Request.Url.Host，我们将使用它。Request.Url.Host。</span><span class="sxs-lookup"><span data-stu-id="971f6-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="971f6-163">下面的代码演示在 ASP.NET MVC 1.0 和 2 个应用程序与控制器类一起使用的已修改的 IsLocalUrl() 方法。</span><span class="sxs-lookup"><span data-stu-id="971f6-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="971f6-164">**列表 5 – IsLocalUrl() 方法，这被修改用于 MVC 控制器类**</span><span class="sxs-lookup"><span data-stu-id="971f6-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="971f6-165">现在 IsLocalUrl() 方法已准备就绪，我们可以调用它从我们的登录操作来验证该 returnUrl 参数，如下面的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="971f6-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="971f6-166">**代码清单 6 – Updated 登录方法验证 returnUrl 参数**</span><span class="sxs-lookup"><span data-stu-id="971f6-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="971f6-167">现在我们可以通过尝试使用外部的返回 URL 登录测试打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="971f6-168">让我们使用 /Account/LogOn？ReturnUrl =<http://www.bing.com/>试。</span><span class="sxs-lookup"><span data-stu-id="971f6-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="971f6-169">**图 04**： 测试更新后的登录操作</span><span class="sxs-lookup"><span data-stu-id="971f6-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="971f6-170">已成功登录后，我们将重定向到 Home/Index 控制器操作而不是外部 URL。</span><span class="sxs-lookup"><span data-stu-id="971f6-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="971f6-171">**图 05**： 犬队击败开放重定向攻击</span><span class="sxs-lookup"><span data-stu-id="971f6-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="971f6-172">总结</span><span class="sxs-lookup"><span data-stu-id="971f6-172">Summary</span></span>

<span data-ttu-id="971f6-173">重定向 Url 作为应用程序的 URL 中的参数传递时，会发生开放重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="971f6-174">ASP.NET MVC 3 模板包括代码，以防止打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="971f6-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="971f6-175">您可以添加此代码进行一些修改后对 ASP.NET MVC 1.0 和 2 个应用程序。</span><span class="sxs-lookup"><span data-stu-id="971f6-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="971f6-176">若要防止打开重定向攻击到 ASP.NET 1.0 和 2 个应用程序进行日志记录时，将 IsLocalUrl() 方法添加并验证的登录操作中的 returnUrl 参数。</span><span class="sxs-lookup"><span data-stu-id="971f6-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
