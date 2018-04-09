---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 阻止打开重定向攻击 (C#) |Microsoft 文档
author: jongalloway
description: 本教程介绍如何在 ASP.NET MVC 应用程序阻止打开重定向攻击。 本教程讨论所做的更改...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: ec1cd1791eb6d32e7c1ea50bc6626929cad2960e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="c92b1-104">阻止打开重定向攻击 (C#)</span><span class="sxs-lookup"><span data-stu-id="c92b1-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="c92b1-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="c92b1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="c92b1-106">本教程介绍如何在 ASP.NET MVC 应用程序阻止打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="c92b1-107">本教程讨论了已在 ASP.NET MVC 3 中 AccountController 中进行的更改，并演示你现有的 ASP.NET MVC 1.0 和 2 的应用程序中，你就可以应用这些更改。</span><span class="sxs-lookup"><span data-stu-id="c92b1-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="c92b1-108">什么是打开的重定向攻击？</span><span class="sxs-lookup"><span data-stu-id="c92b1-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="c92b1-109">任何 web 应用程序将重定向到通过如查询字符串或窗体数据请求指定的 URL 可能可能被篡改将用户重定向到外部、 恶意 URL。</span><span class="sxs-lookup"><span data-stu-id="c92b1-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="c92b1-110">此篡改称为打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="c92b1-111">每当应用程序逻辑将重定向到指定的 URL，你必须验证重定向 URL 尚未被篡改。</span><span class="sxs-lookup"><span data-stu-id="c92b1-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="c92b1-112">默认情况下 AccountController 中用于 ASP.NET MVC 1.0 和 ASP.NET MVC 2 的登录名极易收到打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="c92b1-113">幸运的是，很容易地更新您现有的应用程序，以使用从 ASP.NET MVC 3 预览版更正操作。</span><span class="sxs-lookup"><span data-stu-id="c92b1-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="c92b1-114">若要了解漏洞的修补程序，让我们看一下默认 ASP.NET MVC 2 Web 应用程序项目中的登录重定向工作原理。</span><span class="sxs-lookup"><span data-stu-id="c92b1-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="c92b1-115">在此应用程序，尝试访问的控制器操作具有 [Authorize] 特性将重定向未经授权的用户到 /Account/LogOn 视图。</span><span class="sxs-lookup"><span data-stu-id="c92b1-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="c92b1-116">此重定向到 /Account/LogOn 将包括 returnUrl 查询字符串参数，以便用户可以在用户成功登录后返回最初请求的 url。</span><span class="sxs-lookup"><span data-stu-id="c92b1-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="c92b1-117">在下面的屏幕截图中，我们可以看到，尝试访问 /Account/ChangePassword 视图未登录时导致重定向到 /Account/LogOn？ReturnUrl = %2faccount%2fChangePassword %2f。</span><span class="sxs-lookup"><span data-stu-id="c92b1-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="c92b1-118">**图 01**： 与打开的重定向的登录页</span><span class="sxs-lookup"><span data-stu-id="c92b1-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="c92b1-119">由于 ReturnUrl 查询字符串参数未通过验证，攻击者可以修改它以将任何 URL 地址注入要执行的打开的重定向攻击的参数。</span><span class="sxs-lookup"><span data-stu-id="c92b1-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="c92b1-120">若要进行此演示，我们可以修改的 ReturnUrl 参数[ http://bing.com ](http://bing.com)，因此将生成的登录 URL/帐户/登录？ReturnUrl =<http://www.bing.com/>。</span><span class="sxs-lookup"><span data-stu-id="c92b1-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="c92b1-121">在成功登录到站点，我们将重定向到[ http://bing.com ](http://bing.com)。此重定向未通过验证，因为它无法改为指向恶意站点，试图欺骗用户。</span><span class="sxs-lookup"><span data-stu-id="c92b1-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com). Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="c92b1-122">更复杂的打开重定向攻击</span><span class="sxs-lookup"><span data-stu-id="c92b1-122">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="c92b1-123">打开重定向攻击是非常危险的因为攻击者知道，我们将尝试登录到特定的网站，这将使我们易受[网络钓鱼攻击](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c92b1-123">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="c92b1-124">例如，攻击者无法尝试捕获其密码，将恶意电子邮件发送到网站用户。</span><span class="sxs-lookup"><span data-stu-id="c92b1-124">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="c92b1-125">让我们看一下这工作原理 NerdDinner 站点上。</span><span class="sxs-lookup"><span data-stu-id="c92b1-125">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="c92b1-126">（请注意，已更新实时 NerdDinner 站点以防止打开重定向攻击。）</span><span class="sxs-lookup"><span data-stu-id="c92b1-126">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="c92b1-127">首先，攻击者向我们发送链接到 NerdDinner 包括重定向到他们伪造的页面上的登录页：</span><span class="sxs-lookup"><span data-stu-id="c92b1-127">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="c92b1-128">请注意，返回的 URL 指向 nerddiner.com，缺少"n"从 word dinner。</span><span class="sxs-lookup"><span data-stu-id="c92b1-128">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="c92b1-129">在此示例中，这是攻击者控制的域。</span><span class="sxs-lookup"><span data-stu-id="c92b1-129">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="c92b1-130">当我们访问上面的链接时，我们将会转到合法 NerdDinner.com 登录页。</span><span class="sxs-lookup"><span data-stu-id="c92b1-130">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="c92b1-131">**图 02**: NerdDinner 与打开的重定向的登录页</span><span class="sxs-lookup"><span data-stu-id="c92b1-131">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="c92b1-132">我们正确登录时，ASP.NET MVC AccountController 登录操作将重我们定向到 returnUrl 查询字符串参数中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="c92b1-132">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="c92b1-133">在这种情况下，它是攻击者已进入，即 URL [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="c92b1-133">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="c92b1-134">除非我们极 watchful，它是很有可能，我们不会发现这种情况，尤其是因为攻击者已小心，确保其伪造的页的外观完全一样的合法的登录页。</span><span class="sxs-lookup"><span data-stu-id="c92b1-134">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="c92b1-135">此登录页包括错误消息，请求我们重新登录。</span><span class="sxs-lookup"><span data-stu-id="c92b1-135">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="c92b1-136">非常笨拙我们，我们必须有误我们的密码。</span><span class="sxs-lookup"><span data-stu-id="c92b1-136">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="c92b1-137">**图 03**： 伪造 NerdDinner 登录屏幕</span><span class="sxs-lookup"><span data-stu-id="c92b1-137">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="c92b1-138">当我们重新键入我们用户名和密码时，伪造的登录页将信息保存，并向我们发送回合法 NerdDinner.com 站点。</span><span class="sxs-lookup"><span data-stu-id="c92b1-138">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="c92b1-139">此时，NerdDinner.com 站点具有已进行身份验证 us，因而伪造的登录页可以直接进入该页面将重定向。</span><span class="sxs-lookup"><span data-stu-id="c92b1-139">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="c92b1-140">最终结果是攻击者将有我们用户名和密码，并且我们不会意识到，我们已向其提供它。</span><span class="sxs-lookup"><span data-stu-id="c92b1-140">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="c92b1-141">查看在 AccountController 登录操作易受攻击的代码</span><span class="sxs-lookup"><span data-stu-id="c92b1-141">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="c92b1-142">ASP.NET MVC 2 应用程序中的登录操作的代码所示。</span><span class="sxs-lookup"><span data-stu-id="c92b1-142">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="c92b1-143">请注意，一旦成功登录，则控制器将返回到的重定向到 returnUrl。</span><span class="sxs-lookup"><span data-stu-id="c92b1-143">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="c92b1-144">你可以看到与 returnUrl 参数执行任何验证。</span><span class="sxs-lookup"><span data-stu-id="c92b1-144">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="c92b1-145">**列表 1 – 中的 ASP.NET MVC 2 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="c92b1-145">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="c92b1-146">现在让我们看一下 ASP.NET MVC 3 登录操作的更改。</span><span class="sxs-lookup"><span data-stu-id="c92b1-146">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="c92b1-147">此代码已更改，以通过调用中名为的 System.Web.Mvc.Url 帮助器类的新方法验证 returnUrl 参数`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="c92b1-147">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="c92b1-148">**列出 2 – 在 ASP.NET MVC 3 登录操作 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="c92b1-148">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="c92b1-149">已更改来验证的调用中 System.Web.Mvc.Url 帮助器类的新方法的返回 URL 参数`IsLocalUrl()`。</span><span class="sxs-lookup"><span data-stu-id="c92b1-149">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="c92b1-150">保护你的 ASP.NET MVC 1.0 和 MVC 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="c92b1-150">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="c92b1-151">通过添加 IsLocalUrl() 帮助器方法和更新的登录操作来验证该 returnUrl 参数，我们可以在我们现有的 ASP.NET MVC 1.0 和 2 的应用程序充分利用 ASP.NET MVC 3 更改。</span><span class="sxs-lookup"><span data-stu-id="c92b1-151">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="c92b1-152">ASP.NET Web Pages 应用程序也使用 UrlHelper IsLocalUrl() 方法实际上就调用到中 System.Web.WebPages，作为此验证的方法。</span><span class="sxs-lookup"><span data-stu-id="c92b1-152">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="c92b1-153">**列出 3-从 ASP.NET MVC 3 UrlHelper IsLocalUrl() 方法 `class`**</span><span class="sxs-lookup"><span data-stu-id="c92b1-153">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="c92b1-154">IsUrlLocalToHost 方法包含实际的验证逻辑，列出 4 中所示。</span><span class="sxs-lookup"><span data-stu-id="c92b1-154">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="c92b1-155">**列出 4 – 从 System.Web.WebPages RequestExtensions 类 IsUrlLocalToHost() 方法**</span><span class="sxs-lookup"><span data-stu-id="c92b1-155">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="c92b1-156">在我们的 ASP.NET MVC 1.0 或 2 的应用程序中，我们将向 AccountController 中，添加 IsLocalUrl() 方法，但你建议如有可能将其添加到一个单独的帮助器类。</span><span class="sxs-lookup"><span data-stu-id="c92b1-156">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="c92b1-157">我们会使两个小型更改到 IsLocalUrl() 的 ASP.NET MVC 3 版本，以便它将在 AccountController 中工作。</span><span class="sxs-lookup"><span data-stu-id="c92b1-157">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="c92b1-158">首先，我们将更改它通过公共方法为私有方法，因为可作为控制器操作访问控制器中的公共方法。</span><span class="sxs-lookup"><span data-stu-id="c92b1-158">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="c92b1-159">其次，我们将修改检查 URL 主机针对应用程序主机的调用。</span><span class="sxs-lookup"><span data-stu-id="c92b1-159">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="c92b1-160">调用，将使用本地 requestcontext 已 UrlHelper 类中的字段。</span><span class="sxs-lookup"><span data-stu-id="c92b1-160">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="c92b1-161">而不是使用这种情况。RequestContext.HttpContext.Request.Url.Host，我们将使用它。Request.Url.Host。</span><span class="sxs-lookup"><span data-stu-id="c92b1-161">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="c92b1-162">下面的代码演示在 ASP.NET MVC 1.0 和 2 的应用程序使用了控制器类修改后的 IsLocalUrl() 方法。</span><span class="sxs-lookup"><span data-stu-id="c92b1-162">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="c92b1-163">**列出 5 – IsLocalUrl() 方法，这被修改用于 MVC 控制器类**</span><span class="sxs-lookup"><span data-stu-id="c92b1-163">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="c92b1-164">IsLocalUrl() 方法已到位，我们就可以调用它从我们的登录操作来验证该 returnUrl 参数，如下面的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="c92b1-164">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="c92b1-165">**列出 6-验证 returnUrl 参数更新登录方法**</span><span class="sxs-lookup"><span data-stu-id="c92b1-165">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="c92b1-166">现在我们可以通过尝试使用外部的返回 URL 登录测试打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-166">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="c92b1-167">让我们使用 /Account/LogOn？ReturnUrl =<http://www.bing.com/>试。</span><span class="sxs-lookup"><span data-stu-id="c92b1-167">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="c92b1-168">**图 04**： 测试更新后的登录操作</span><span class="sxs-lookup"><span data-stu-id="c92b1-168">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="c92b1-169">已成功登录后，我们将重定向到 Home/Index 控制器操作而不是外部 URL。</span><span class="sxs-lookup"><span data-stu-id="c92b1-169">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="c92b1-170">**图 05**： 打开重定向攻击失效</span><span class="sxs-lookup"><span data-stu-id="c92b1-170">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="c92b1-171">总结</span><span class="sxs-lookup"><span data-stu-id="c92b1-171">Summary</span></span>

<span data-ttu-id="c92b1-172">重定向 Url 作为应用程序的 URL 中的参数传递时，会发生打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-172">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="c92b1-173">模板包括代码，以防止对 ASP.NET MVC 3 打开重定向攻击。</span><span class="sxs-lookup"><span data-stu-id="c92b1-173">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="c92b1-174">你可以添加与 ASP.NET MVC 1.0 和 2 的应用程序进行一些修改此代码。</span><span class="sxs-lookup"><span data-stu-id="c92b1-174">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="c92b1-175">若要防止打开重定向攻击，登录到 ASP.NET 1.0 和 2 的应用程序时，将 IsLocalUrl() 方法添加并验证中的登录操作的 returnUrl 参数。</span><span class="sxs-lookup"><span data-stu-id="c92b1-175">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
