---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET Web 中的外部网站登录页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何登录到你使用 Facebook、 Google、 Twitter、 Yahoo 和其他站点的 ASP.NET Web Pages (Razor) 站点，即如何支持...
ms.author: aspnetcontent
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: e6c5b578b4c74fd04136d31751d51b59ba9197ba
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825432"
---
<a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c8f0c-103">在 ASP.NET Web Pages (Razor) 站点中使用外部站点中的日志记录</span><span class="sxs-lookup"><span data-stu-id="c8f0c-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="c8f0c-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c8f0c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c8f0c-105">本文介绍如何登录到你使用 Facebook、 Google、 Twitter、 Yahoo 和其他站点的 ASP.NET Web Pages (Razor) 站点 — 即，如何在你的站点中支持 OAuth 和 OpenID。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="c8f0c-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c8f0c-107">如何使用 WebMatrix 入门网站模板时启用从其他站点的登录名。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="c8f0c-108">这是引入一文中的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="c8f0c-109">`OAuthWebSecurity`帮助器。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c8f0c-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="c8f0c-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c8f0c-111">ASP.NET 网页 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="c8f0c-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="c8f0c-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c8f0c-112">WebMatrix 3</span></span>

<span data-ttu-id="c8f0c-113">ASP.NET 网页包含对支持[OAuth](http://oauth.net/)并[OpenID](http://openid.net/)提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="c8f0c-114">使用这些提供程序，可让你使用 Facebook、 Twitter、 Microsoft 和 Google 从其现有凭据的站点到用户登录。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="c8f0c-115">例如，若要使用 Facebook 帐户登录，用户可以只需选择 Facebook 图标，将它们重定向到它们在其中输入他们的用户信息的 Facebook 登录页。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="c8f0c-116">它们然后可以将 Facebook 登录你的站点上与其帐户相关联。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="c8f0c-117">Web Pages 成员资格功能相关的增强功能是使用你的网站上的单个帐户，用户可以将多个登录名 （包括登录名从社交网站） 相关联。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="c8f0c-118">下图显示了从登录页面**入门网站**模板，用户可以在其中选择一个 Facebook、 Twitter、 Google 或 Microsoft 图标，以启用日志记录使用的外部帐户：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![外部提供程序](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="c8f0c-120">可以通过取消注释几行代码中启用 OAuth 和 OpenID 的成员身份**入门网站**模板。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="c8f0c-121">您使用的方法和属性以使用 OAuth 和 OpenID 提供程序位于`WebMatrix.Security.OAuthWebSecurity`类。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="c8f0c-122">**入门网站**模板包括完整的成员身份基础结构，需要让用户登录到你使用本地凭据或来自另一个站点的站点登录页、 成员资格数据库，与所有的代码完成.</span><span class="sxs-lookup"><span data-stu-id="c8f0c-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="c8f0c-123">本部分举例说明如何让用户登录从外部站点到站点基于**入门网站**模板。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="c8f0c-124">在创建后入门网站，你执行操作 （详细信息按照）：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="c8f0c-125">使用 OAuth 提供程序 （Facebook、 Twitter 和 Microsoft） 的站点，外部站点上创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="c8f0c-126">这样，您将需要为了调用这些站点的登录功能的应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="c8f0c-127">对于使用 OpenID 提供程序 (Google) 的站点，不需要创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="c8f0c-128">对于所有这些站点，必须具有一个帐户，以便在中记录并创建开发人员应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8f0c-129">Microsoft 应用程序仅接受工作网站的实时 URL，因此不能用于本地网站 URL 测试登录名。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="c8f0c-130">编辑你的网站中的几个文件以指定适当的身份验证提供程序，并将提交到想要使用的站点的登录名。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="c8f0c-131">本文提供了单独的指令的以下任务：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="c8f0c-132">启用 Google 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="c8f0c-133">启用 Facebook 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="c8f0c-134">启用 Twitter 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="c8f0c-135">启用 Google 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="c8f0c-136">创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="c8f0c-137">打开 *\_AppStart.cshtml*页上，并取消注释以下代码行。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="c8f0c-138">测试 Google 登录</span><span class="sxs-lookup"><span data-stu-id="c8f0c-138">Testing Google login</span></span>

1. <span data-ttu-id="c8f0c-139">运行*default.cshtml*您的网站上，然后选择**登录**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="c8f0c-140">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Google**或者**Yahoo**提交按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="c8f0c-141">此示例使用 Google 登录名。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="c8f0c-142">Web 页面将请求重定向到 Google 登录页。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-142">The web page redirects the request to the Google login page.</span></span>

    ![Google 登录](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="c8f0c-144">输入现有 Google 帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="c8f0c-145">如果出现要求你是否想要允许 Google *Localhost*若要使用帐户中的信息，请单击**允许**。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="c8f0c-146">代码使用 Google 的令牌对用户进行身份验证，然后返回到此页上你的网站。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="c8f0c-147">此页，可以将其 Google 登录名与你的网站上的现有帐户相关联的用户或用户可以在注册你将使用的外部登录名相关联的站点上的新帐户。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="c8f0c-149">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-149">Choose the **Associate** button.</span></span> <span data-ttu-id="c8f0c-150">在浏览器返回到应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="c8f0c-151">启用 Facebook 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="c8f0c-152">转到[Facebook 开发人员站点](https://developers.facebook.com/apps)（如果尚未登录，则日志）。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="c8f0c-153">选择**创建新应用**按钮，然后按照提示进行命名和创建新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="c8f0c-154">在部分**选择如何将您的应用程序与 Facebook**，选择**网站**部分。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="c8f0c-155">填写**站点 URL**字段与你的站点的 URL (例如， `http://www.example.com`)。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="c8f0c-156">**域**字段是可选的; 可以使用此提供对整个域的身份验证 (如*example.com*)。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c8f0c-157">如果你使用 URL 在本地计算机上运行站点喜欢`http://localhost:12345`（其中数是本地端口号），可以添加此值设置为**站点 URL**字段用于测试你的站点。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="c8f0c-158">但是，任何时候，只要你的本地站点更改的端口号，你将需要更新**站点 URL**字段的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="c8f0c-159">选择**保存更改**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="c8f0c-160">选择**应用**同样，选项卡，然后查看你的应用程序的起始页。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="c8f0c-161">复制**应用程序 ID**并**应用程序密码**为应用程序的值并将其粘贴到一个临时的文本文件。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="c8f0c-162">网站代码中，会将这些值传递到 Facebook 提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="c8f0c-163">退出 Facebook 开发人员网站。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="c8f0c-164">现在您更改两个页面中你的网站，以便用户将能够登录到网站使用其 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="c8f0c-165">创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="c8f0c-166">打开 *\_AppStart.cshtml*页上，并取消注释的代码，为 Facebook OAuth 提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="c8f0c-167">取消注释的代码块如以下所示：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="c8f0c-168">复制**应用程序 ID**从 Facebook 应用程序的值作为值`appId`参数 （在引号内）。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="c8f0c-169">复制**应用程序机密**从 Facebook 应用程序作为值`appSecret`参数值。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="c8f0c-170">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="c8f0c-171">测试 Facebook 登录</span><span class="sxs-lookup"><span data-stu-id="c8f0c-171">Testing Facebook login</span></span>

1. <span data-ttu-id="c8f0c-172">运行该站点*default.cshtml*页上，然后选择**登录名**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="c8f0c-173">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Facebook**图标。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="c8f0c-174">Web 页面将请求重定向到 Facebook 登录页。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="c8f0c-176">登录到 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="c8f0c-177">代码使用 Facebook 令牌进行身份验证，然后返回到页您可以在其中将 Facebook 登录名与站点的登录名相关联。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="c8f0c-178">你的用户名称或电子邮件地址填充到**电子邮件**字段在窗体上。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="c8f0c-180">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="c8f0c-181">在浏览器返回到主页并登录。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="c8f0c-182">启用 Twitter 登录名</span><span class="sxs-lookup"><span data-stu-id="c8f0c-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="c8f0c-183">浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="c8f0c-184">选择**创建应用**链接，然后登录到网站。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="c8f0c-185">上**创建的应用程序**窗体中，填写**名称**并**说明**字段。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="c8f0c-186">在中**网站**字段中，输入你的站点的 URL (例如， `http://www.example.com`)。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c8f0c-187">如果您要测试你的本地站点 (使用类似`http://localhost:12345`)，Twitter 可能不接受 URL。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="c8f0c-188">但是，您可能能够使用本地环回 IP 地址 (例如`http://127.0.0.1:12345`)。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="c8f0c-189">这将简化测试本地应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="c8f0c-190">但是，每次你的本地网站的端口号更改，你将需要更新**网站**字段的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="c8f0c-191">在中**回叫 URL**字段中，输入你希望用户在登录后到 Twitter 到返回的网站中的页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="c8f0c-192">例如，若要向用户发送到入门网站 （它将识别其登录的状态） 的主页上，输入中输入的同一个 URL**网站**字段。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="c8f0c-193">接受条款，然后选择**创建 Twitter 应用程序**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="c8f0c-194">上**我的应用程序**登陆页上，选择你创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="c8f0c-195">上**详细信息**选项卡上，滚动到底部并选择**创建我的访问令牌**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="c8f0c-196">上**详细信息**选项卡上，复制**使用者密钥**并**使用者机密**为应用程序的值并将其粘贴到一个临时的文本文件。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="c8f0c-197">网站代码中，会将这些值传递到 Twitter 提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="c8f0c-198">退出 Twitter 网站。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-198">Exit the Twitter site.</span></span>

<span data-ttu-id="c8f0c-199">现在您更改两个页面中你的网站，以便用户能够登录到使用 Twitter 帐户的站点。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="c8f0c-200">创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="c8f0c-201">打开 *\_AppStart.cshtml*页面和 Twitter OAuth 提供程序取消注释的代码。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="c8f0c-202">取消注释的代码块如下所示：</span><span class="sxs-lookup"><span data-stu-id="c8f0c-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="c8f0c-203">复制**使用者密钥**从 Twitter 应用程序的值作为值`consumerKey`参数 （在引号内）。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="c8f0c-204">复制**使用者机密**从 Twitter 应用程序的值作为值`consumerSecret`参数。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="c8f0c-205">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="c8f0c-206">测试 Twitter 登录</span><span class="sxs-lookup"><span data-stu-id="c8f0c-206">Testing Twitter login</span></span>

1. <span data-ttu-id="c8f0c-207">运行*default.cshtml*您的网站上，然后选择**登录名**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="c8f0c-208">上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Twitter**图标。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="c8f0c-209">Web 页面将请求重定向到 Twitter 登录页面为您创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth 4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="c8f0c-211">登录到 Twitter 帐户。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="c8f0c-212">代码使用 Twitter 令牌进行身份验证用户，然后返回到页你可以将关联您使用您网站的帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="c8f0c-213">名称或电子邮件地址填充到**电子邮件**字段在窗体上。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="c8f0c-215">选择**相关联**按钮。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="c8f0c-216">在浏览器返回到主页并登录。</span><span class="sxs-lookup"><span data-stu-id="c8f0c-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c8f0c-217">其他资源</span><span class="sxs-lookup"><span data-stu-id="c8f0c-217">Additional Resources</span></span>


- [<span data-ttu-id="c8f0c-218">自定义站点范围内的行为</span><span class="sxs-lookup"><span data-stu-id="c8f0c-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="c8f0c-219">将安全性和成员身份添加到 ASP.NET Web Pages 站点</span><span class="sxs-lookup"><span data-stu-id="c8f0c-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
