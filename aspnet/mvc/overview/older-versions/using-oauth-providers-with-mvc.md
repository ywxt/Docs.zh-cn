---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: OAuth 提供程序使用 MVC 4 |Microsoft 文档
author: tfitzmac
description: 本教程演示了如何生成的 ASP.NET MVC 4 web 应用程序使用户能够从 Facebo 之类的外部提供程序的凭据登录...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/19/2013
ms.topic: article
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: f0d053cecbf9a59f258470ee370852e3f112908c
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28033563"
---
<a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="1c82d-103">OAuth 提供程序使用 MVC 4</span><span class="sxs-lookup"><span data-stu-id="1c82d-103">Using OAuth Providers with MVC 4</span></span>
====================
<span data-ttu-id="1c82d-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1c82d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1c82d-105">本教程演示如何生成的 ASP.NET MVC 4 web 应用程序使用户能够从外部提供程序，如 Facebook、 Twitter、 Microsoft 或 Google 凭据登录，然后集成到这些访问接口中的功能的一些你web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="1c82d-106">为简单起见，本教程重点介绍使用从 Facebook 的凭据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="1c82d-107">若要在一个 ASP.NET MVC 5 web 应用程序中使用外部凭据，请参阅[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="1c82d-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="1c82d-108">启用这些凭据在您的网站提供一个明显的优势，因为支持数百万个用户已与这些外部提供程序的帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="1c82d-109">这些用户可能更倾向于注册为您的网站，如果它们不需要创建并记住一组新的凭据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="1c82d-110">此外，通过这些提供程序之一的用户已登录后，你可以集成社交操作从提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="1c82d-111">你将生成</span><span class="sxs-lookup"><span data-stu-id="1c82d-111">What you'll build</span></span>

<span data-ttu-id="1c82d-112">在本教程中有两个主要目标：</span><span class="sxs-lookup"><span data-stu-id="1c82d-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="1c82d-113">使用户能够从 OAuth 提供程序的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="1c82d-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="1c82d-114">从提供程序检索帐户信息和将该信息与你的站点的帐户注册集成。</span><span class="sxs-lookup"><span data-stu-id="1c82d-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="1c82d-115">虽然本教程中的示例重点关注将 Facebook 用作身份验证提供程序，你可以修改代码以使用任何提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="1c82d-116">实现任何提供程序的步骤都非常类似于将在本教程中看到的步骤。</span><span class="sxs-lookup"><span data-stu-id="1c82d-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="1c82d-117">只会注意到大的差异进行对提供程序的 API 的直接调用时设置。</span><span class="sxs-lookup"><span data-stu-id="1c82d-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c82d-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="1c82d-118">Prerequisites</span></span>

- <span data-ttu-id="1c82d-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="1c82d-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="1c82d-120">Or</span><span class="sxs-lookup"><span data-stu-id="1c82d-120">Or</span></span>

- <span data-ttu-id="1c82d-121">Microsoft Visual Studio 2010 SP1 或[Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="1c82d-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="1c82d-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="1c82d-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="1c82d-123">此外，本主题假定你具有有关 ASP.NET MVC 和 Visual Studio 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="1c82d-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="1c82d-124">如果你需要 ASP.NET MVC 4 的简介，请参阅[ASP.NET MVC 4 简介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="1c82d-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="1c82d-125">创建项目</span><span class="sxs-lookup"><span data-stu-id="1c82d-125">Create the project</span></span>

<span data-ttu-id="1c82d-126">在 Visual Studio 中，创建新 ASP.NET MVC 4 Web 应用程序，并将其命名&quot;OAuthMVC&quot;。</span><span class="sxs-lookup"><span data-stu-id="1c82d-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="1c82d-127">你可以面向.NET Framework 4.5 或 4。</span><span class="sxs-lookup"><span data-stu-id="1c82d-127">You can target either .NET Framework 4.5 or 4.</span></span>

![创建项目](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="1c82d-129">在新建 ASP.NET MVC 4 项目窗口中，选择**Internet 应用程序**并使**Razor**作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="1c82d-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![选择 Internet 应用程序](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="1c82d-131">启用提供程序</span><span class="sxs-lookup"><span data-stu-id="1c82d-131">Enable a provider</span></span>

<span data-ttu-id="1c82d-132">如果使用 Internet 应用程序模板创建 MVC 4 web 应用程序时，项目将创建具有一个名为应用程序中的 AuthConfig.cs 文件\_开始文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c82d-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 文件](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="1c82d-134">AuthConfig 文件包含代码以注册外部身份验证提供程序的客户端。</span><span class="sxs-lookup"><span data-stu-id="1c82d-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="1c82d-135">默认情况下，此代码已被注释掉，因此未启用任何外部提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="1c82d-136">你必须取消注释以下代码以使用外部身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="1c82d-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="1c82d-137">取消注释仅想要包括在你的站点中的提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="1c82d-138">对于本教程中，你将仅启用的 Facebook 凭据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="1c82d-139">请注意，在上面的示例中，此方法包含空字符串用于注册参数。</span><span class="sxs-lookup"><span data-stu-id="1c82d-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="1c82d-140">如果你尝试运行该应用程序现在，应用程序将引发参数异常，因为空字符串不被允许的参数。</span><span class="sxs-lookup"><span data-stu-id="1c82d-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="1c82d-141">若要提供有效的值，你必须注册您的网站外部提供程序，如在下一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="1c82d-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="1c82d-142">使用外部提供程序注册</span><span class="sxs-lookup"><span data-stu-id="1c82d-142">Registering with an external provider</span></span>

<span data-ttu-id="1c82d-143">若要使用从外部提供程序的凭据的用户进行身份验证，你必须注册您的网站提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="1c82d-144">在注册你的站点，你将收到参数 （如密钥或 id 和密码） 以包括注册客户端时。</span><span class="sxs-lookup"><span data-stu-id="1c82d-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="1c82d-145">你必须有你想要使用的提供程序的帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="1c82d-146">本教程不显示所有必须执行以便注册这些提供程序的步骤。</span><span class="sxs-lookup"><span data-stu-id="1c82d-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="1c82d-147">步骤通常并不困难。</span><span class="sxs-lookup"><span data-stu-id="1c82d-147">The steps are typically not difficult.</span></span> <span data-ttu-id="1c82d-148">若要成功注册你的站点，请按照这些网站上提供的说明。</span><span class="sxs-lookup"><span data-stu-id="1c82d-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="1c82d-149">若要开始使用注册您的网站，请参阅开发者网站为:</span><span class="sxs-lookup"><span data-stu-id="1c82d-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="1c82d-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="1c82d-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="1c82d-151">Google</span><span class="sxs-lookup"><span data-stu-id="1c82d-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="1c82d-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="1c82d-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="1c82d-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="1c82d-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="1c82d-154">当向 Facebook 注册你的站点，你可以提供&quot;localhost&quot;站点域和`&quot;http://localhost/&quot;`对于 URL，如下面的图像中所示。</span><span class="sxs-lookup"><span data-stu-id="1c82d-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="1c82d-155">使用 localhost 适用于大多数提供程序，但目前并不适用于 Microsoft 提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="1c82d-156">Microsoft 提供程序，必须包含有效的网站 URL。</span><span class="sxs-lookup"><span data-stu-id="1c82d-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![注册站点](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="1c82d-158">在上图中，已删除的应用程序 id、 应用密钥和联系人电子邮件的值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="1c82d-159">实际注册你的站点时，这些值将会显示。</span><span class="sxs-lookup"><span data-stu-id="1c82d-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="1c82d-160">你将想要注意的应用程序 id 和应用程序密钥的值，因为将添加到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="1c82d-161">创建测试用户</span><span class="sxs-lookup"><span data-stu-id="1c82d-161">Creating test users</span></span>

<span data-ttu-id="1c82d-162">如果你不介意使用现有的 Facebook 帐户来测试你的站点，则可以跳过本节。</span><span class="sxs-lookup"><span data-stu-id="1c82d-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="1c82d-163">你的应用程序在 Facebook 应用程序管理页，可以轻松创建测试用户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="1c82d-164">你可以使用这些测试帐户登录到你的站点。</span><span class="sxs-lookup"><span data-stu-id="1c82d-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="1c82d-165">通过单击创建测试用户**角色**在左侧的导航窗格中，单击链接**创建**链接。</span><span class="sxs-lookup"><span data-stu-id="1c82d-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![创建测试用户](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="1c82d-167">Facebook 站点将自动创建你请求的测试帐户数。</span><span class="sxs-lookup"><span data-stu-id="1c82d-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="1c82d-168">从提供程序中添加应用程序 id 和机密</span><span class="sxs-lookup"><span data-stu-id="1c82d-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="1c82d-169">现在，你已从 Facebook 接收的 id 和机密，请返回到 AuthConfig 文件并将它们添加为参数值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="1c82d-170">下面显示的值不是实际值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="1c82d-171">外部凭据登录</span><span class="sxs-lookup"><span data-stu-id="1c82d-171">Log in with external credentials</span></span>

<span data-ttu-id="1c82d-172">这是你所要做，以启用你的站点中的外部凭据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="1c82d-173">运行你的应用程序并单击右上角的登录链接。</span><span class="sxs-lookup"><span data-stu-id="1c82d-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="1c82d-174">模板自动识别你已注册为提供程序的 Facebook 和提供程序包括一个按钮。</span><span class="sxs-lookup"><span data-stu-id="1c82d-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="1c82d-175">如果你注册多个提供程序，将自动包含每个按钮。</span><span class="sxs-lookup"><span data-stu-id="1c82d-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![外部登录名](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="1c82d-177">本教程不涉及如何为外部提供程序自定义按钮中的日志。</span><span class="sxs-lookup"><span data-stu-id="1c82d-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="1c82d-178">该信息，请参阅[时使用 OAuth/OpenID 自定义登录用户界面](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1c82d-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="1c82d-179">单击 Facebook 按钮 Facebook 凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="1c82d-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="1c82d-180">当你选择其中一个外部提供程序时，你重定向到该站点并且提示由该服务进行登录。</span><span class="sxs-lookup"><span data-stu-id="1c82d-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="1c82d-181">下图显示 Facebook 登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="1c82d-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="1c82d-182">它指出，使用的你的 Facebook 帐户登录到名为 oauthmvcexample 的站点。</span><span class="sxs-lookup"><span data-stu-id="1c82d-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 身份验证](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="1c82d-184">登录后的 Facebook 凭据，页面通知用户该站点将有权访问的基本信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![请求权限](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="1c82d-186">选择后**转到应用**，用户必须注册为该站点。</span><span class="sxs-lookup"><span data-stu-id="1c82d-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="1c82d-187">用户已使用 Facebook 凭据登录后下, 图显示在注册页。</span><span class="sxs-lookup"><span data-stu-id="1c82d-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="1c82d-188">用户名称是通常预先填入从提供程序的名称。</span><span class="sxs-lookup"><span data-stu-id="1c82d-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="1c82d-190">单击**注册**来完成注册。</span><span class="sxs-lookup"><span data-stu-id="1c82d-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="1c82d-191">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="1c82d-191">Close the browser.</span></span>

<span data-ttu-id="1c82d-192">你可以看到，已将新帐户添加到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="1c82d-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="1c82d-193">在服务器资源管理器，打开**DefaultConnection**数据库，然后打开**表**文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c82d-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![数据库表](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="1c82d-195">右键单击**UserProfile**表，然后选择**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="1c82d-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![显示数据](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="1c82d-197">你将看到你添加的新帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-197">You will see the new account you added.</span></span> <span data-ttu-id="1c82d-198">查看中的数据**网页\_OAuthMembership**表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="1c82d-199">你将看到与用于你刚添加的帐户的外部提供程序相关的更多数据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="1c82d-200">如果你只想要启用外部身份验证，你已完成。</span><span class="sxs-lookup"><span data-stu-id="1c82d-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="1c82d-201">但是，你可以进一步将集成从提供程序的信息到新的用户注册过程中，如以下各节中所示。</span><span class="sxs-lookup"><span data-stu-id="1c82d-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="1c82d-202">为其他用户信息创建模型</span><span class="sxs-lookup"><span data-stu-id="1c82d-202">Create models for additional user information</span></span>

<span data-ttu-id="1c82d-203">如前面的部分中，你注意到，你不需要检索要工作的内置帐户注册任何其他信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="1c82d-204">但是，最外部提供程序将传递有关用户的其他信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="1c82d-205">以下部分说明如何保留该信息并将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="1c82d-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="1c82d-206">具体而言，你将保留用户的完整名称，用户的个人的 web 页的 URI 的值和一个值，该值指示是否 Facebook 已验证帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="1c82d-207">你将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)添加用于存储的其他用户信息的表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="1c82d-208">要添加到现有数据库，表，因此你将首先需要创建当前数据库的快照。</span><span class="sxs-lookup"><span data-stu-id="1c82d-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="1c82d-209">通过创建当前数据库的快照，稍后可以创建包含新的表的迁移。</span><span class="sxs-lookup"><span data-stu-id="1c82d-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="1c82d-210">若要创建当前数据库的快照：</span><span class="sxs-lookup"><span data-stu-id="1c82d-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="1c82d-211">打开**程序包管理器控制台**</span><span class="sxs-lookup"><span data-stu-id="1c82d-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="1c82d-212">运行命令**启用迁移**</span><span class="sxs-lookup"><span data-stu-id="1c82d-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="1c82d-213">运行命令**IgnoreChanges 添加迁移初始 –**</span><span class="sxs-lookup"><span data-stu-id="1c82d-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="1c82d-214">运行命令**更新数据库**</span><span class="sxs-lookup"><span data-stu-id="1c82d-214">Run the command **update-database**</span></span>

<span data-ttu-id="1c82d-215">现在，你将添加新属性。</span><span class="sxs-lookup"><span data-stu-id="1c82d-215">Now, you will add the new properties.</span></span> <span data-ttu-id="1c82d-216">在 Models 文件夹中，打开 AccountModels.cs 文件，并查找 RegisterExternalLoginModel 类。</span><span class="sxs-lookup"><span data-stu-id="1c82d-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="1c82d-217">RegisterExternalLoginModel 类包含来自身份验证提供程序返回的值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="1c82d-218">添加命名 FullName 和链接，为下面突出显示的属性。</span><span class="sxs-lookup"><span data-stu-id="1c82d-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="1c82d-219">此外在 AccountModels.cs，添加名 ExtraUserInformation 的新类。</span><span class="sxs-lookup"><span data-stu-id="1c82d-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="1c82d-220">此类表示将在数据库中创建的新表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="1c82d-221">在 UsersContext 类中，添加突出显示下面的代码以创建新的类的 DbSet 属性。</span><span class="sxs-lookup"><span data-stu-id="1c82d-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="1c82d-222">现在你就可以创建新的表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-222">You are now ready to create the new table.</span></span> <span data-ttu-id="1c82d-223">再次和此时间，请打开程序包管理器控制台：</span><span class="sxs-lookup"><span data-stu-id="1c82d-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="1c82d-224">运行命令**添加迁移 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="1c82d-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="1c82d-225">运行命令**更新数据库**</span><span class="sxs-lookup"><span data-stu-id="1c82d-225">Run the command **update-database**</span></span>

<span data-ttu-id="1c82d-226">数据库中现在存在新的表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="1c82d-227">检索附加的数据</span><span class="sxs-lookup"><span data-stu-id="1c82d-227">Retrieve the additional data</span></span>

<span data-ttu-id="1c82d-228">有两种方法来检索其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="1c82d-229">第一种方法是保留传回，默认情况下，身份验证请求过程的用户数据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="1c82d-230">第二种方式是专门调用提供程序 API 和请求的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="1c82d-231">返回由 Facebook 自动传递个 FullName 和链接值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="1c82d-232">通过 Facebook API 调用中检索值，该值指示是否 Facebook 已验证帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="1c82d-233">首先，将 FullName 和链接，填充值，然后更高版本，你将获取已验证的值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="1c82d-234">若要检索其他用户数据，请打开**AccountController.cs**文件中**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c82d-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="1c82d-235">此文件包含日志记录、 注册和管理帐户的逻辑。</span><span class="sxs-lookup"><span data-stu-id="1c82d-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="1c82d-236">具体而言，请注意调用的方法**ExternalLoginCallback**和**ExternalLoginConfirmation**。</span><span class="sxs-lookup"><span data-stu-id="1c82d-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="1c82d-237">在这些方法，你可以添加代码以自定义你的应用程序的外部登录名操作。</span><span class="sxs-lookup"><span data-stu-id="1c82d-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="1c82d-238">第一行**ExternalLoginCallback**方法包含：</span><span class="sxs-lookup"><span data-stu-id="1c82d-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="1c82d-239">其他用户数据传递回**ExtraData**属性**AuthenticationResult**从返回的对象**VerifyAuthentication**方法。</span><span class="sxs-lookup"><span data-stu-id="1c82d-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="1c82d-240">Facebook 客户端包含中的以下值**ExtraData**属性：</span><span class="sxs-lookup"><span data-stu-id="1c82d-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="1c82d-241">id</span><span class="sxs-lookup"><span data-stu-id="1c82d-241">id</span></span>
- <span data-ttu-id="1c82d-242">name</span><span class="sxs-lookup"><span data-stu-id="1c82d-242">name</span></span>
- <span data-ttu-id="1c82d-243">链接</span><span class="sxs-lookup"><span data-stu-id="1c82d-243">link</span></span>
- <span data-ttu-id="1c82d-244">性别</span><span class="sxs-lookup"><span data-stu-id="1c82d-244">gender</span></span>
- <span data-ttu-id="1c82d-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="1c82d-245">accesstoken</span></span>

<span data-ttu-id="1c82d-246">其他提供程序将 ExtraData 属性中有类似但略有不同的数据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="1c82d-247">如果用户是您的网站的新手，您将检索某些附加的数据，并将该数据传递给确认视图。</span><span class="sxs-lookup"><span data-stu-id="1c82d-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="1c82d-248">仅当用户为您的网站的新手，运行代码的方法中的最后一个块。</span><span class="sxs-lookup"><span data-stu-id="1c82d-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="1c82d-249">将以下行：</span><span class="sxs-lookup"><span data-stu-id="1c82d-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="1c82d-250">用下面这行：</span><span class="sxs-lookup"><span data-stu-id="1c82d-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="1c82d-251">此更改仅包括 FullName 和链接的属性的值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="1c82d-252">在**ExternalLoginConfirmation**方法中，修改下面的代码的突出显示部分以保存的其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="1c82d-253">调整视图</span><span class="sxs-lookup"><span data-stu-id="1c82d-253">Adjusting the view</span></span>

<span data-ttu-id="1c82d-254">在注册页中，将显示从提供程序检索其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="1c82d-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="1c82d-255">在**视图**/**帐户**文件夹中，打开**ExternalLoginConfirmation.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="1c82d-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="1c82d-256">用户名称的现有字段下, 为 FullName、 链接和 PictureLink 中添加字段。</span><span class="sxs-lookup"><span data-stu-id="1c82d-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="1c82d-257">你现差不多已做好运行该应用程序并将新用户注册保存的其他信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="1c82d-258">你必须具有与站点中不能已注册的帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="1c82d-259">您可以使用不同的测试帐户，或删除中的行**UserProfile**和**网页\_OAuthMembership**你想要重复使用的帐户的表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="1c82d-260">通过删除这些行，将确保该帐户再次注册。</span><span class="sxs-lookup"><span data-stu-id="1c82d-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="1c82d-261">运行应用程序并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-261">Run the application and register the new user.</span></span> <span data-ttu-id="1c82d-262">请注意，这一次确认页包含多个值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="1c82d-264">注册后，关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="1c82d-264">After completing registration, close the browser.</span></span> <span data-ttu-id="1c82d-265">请注意中的新值的数据库中查找**ExtraUserInformation**表。</span><span class="sxs-lookup"><span data-stu-id="1c82d-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="1c82d-266">为 Facebook API 安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="1c82d-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="1c82d-267">Facebook 提供[API](https://developers.facebook.com/docs/reference/apis/)可以调用以执行操作。</span><span class="sxs-lookup"><span data-stu-id="1c82d-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="1c82d-268">你可以通过将定向发送 HTTP 请求，或通过使用安装 NuGet 包，它方便了发送这些请求调用 Facebook API。</span><span class="sxs-lookup"><span data-stu-id="1c82d-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="1c82d-269">使用 NuGet 包显示在此教程中，但安装 NuGet 包是不重要。</span><span class="sxs-lookup"><span data-stu-id="1c82d-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="1c82d-270">本教程演示如何使用 Facebook C# SDK 包。</span><span class="sxs-lookup"><span data-stu-id="1c82d-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="1c82d-271">有其他帮助调用 Facebook API 的 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="1c82d-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="1c82d-272">从**管理 NuGet 包**windows 中，选择的 Facebook C# SDK 包。</span><span class="sxs-lookup"><span data-stu-id="1c82d-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![安装包](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="1c82d-274">你将使用 Facebook C# SDK 可以调用用户需要访问令牌的操作。</span><span class="sxs-lookup"><span data-stu-id="1c82d-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="1c82d-275">下一节演示如何获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="1c82d-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="1c82d-276">检索访问令牌</span><span class="sxs-lookup"><span data-stu-id="1c82d-276">Retrieve access token</span></span>

<span data-ttu-id="1c82d-277">验证用户的凭据后，最外部提供程序返回传递访问令牌。</span><span class="sxs-lookup"><span data-stu-id="1c82d-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="1c82d-278">此访问令牌是非常重要，因为它使您能够调用仅供经过身份验证的用户的操作。</span><span class="sxs-lookup"><span data-stu-id="1c82d-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="1c82d-279">因此，检索并将存储访问令牌时，将基本你想要提供更多的功能。</span><span class="sxs-lookup"><span data-stu-id="1c82d-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="1c82d-280">具体取决于外部提供程序，访问令牌可能有效仅将有限的时间量。</span><span class="sxs-lookup"><span data-stu-id="1c82d-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="1c82d-281">若要确保您有一个有效的访问令牌，您将检索它每次用户登录，并将其存储为一个会话值而不是将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="1c82d-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="1c82d-282">在**ExternalLoginCallback**方法，返回还传递访问令牌**ExtraData**属性**AuthenticationResult**对象。</span><span class="sxs-lookup"><span data-stu-id="1c82d-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="1c82d-283">添加到突出显示的代码**ExternalLoginCallback**保存访问令牌中的**会话**对象。</span><span class="sxs-lookup"><span data-stu-id="1c82d-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="1c82d-284">每次用户登录时的 Facebook 帐户时，运行此代码。</span><span class="sxs-lookup"><span data-stu-id="1c82d-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="1c82d-285">虽然此示例从 Facebook 检索访问令牌，可以通过相同的键名为从任何外部提供程序检索访问令牌&quot;accesstoken&quot;。</span><span class="sxs-lookup"><span data-stu-id="1c82d-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="1c82d-286">注销</span><span class="sxs-lookup"><span data-stu-id="1c82d-286">Logging off</span></span>

<span data-ttu-id="1c82d-287">默认值**注销**方法记录将用户从你的应用程序，但不会记录将用户从外部提供程序。</span><span class="sxs-lookup"><span data-stu-id="1c82d-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="1c82d-288">若要登录将用户从 Facebook，并禁止令牌保持用户已注销后，可以添加以下突出显示的代码**注销**在 AccountController 中的方法。</span><span class="sxs-lookup"><span data-stu-id="1c82d-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="1c82d-289">在中提供的值`next`参数是要使用后用户已从 Facebook 注销的 URL。</span><span class="sxs-lookup"><span data-stu-id="1c82d-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="1c82d-290">当测试本地计算机上时，你将为您的本地站点提供正确的端口号。</span><span class="sxs-lookup"><span data-stu-id="1c82d-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="1c82d-291">在生产中，你将提供一个默认页，例如 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="1c82d-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="1c82d-292">检索需要访问令牌的用户信息</span><span class="sxs-lookup"><span data-stu-id="1c82d-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="1c82d-293">现在，使用存储访问令牌，并且安装的 Facebook C# SDK 包，你可以使用它们一起从 Facebook 请求的其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="1c82d-294">在**ExternalLoginConfirmation**方法，创建的实例**FacebookClient**类通过将访问令牌值传递。</span><span class="sxs-lookup"><span data-stu-id="1c82d-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="1c82d-295">请求的值**验证**当前经过身份验证的用户的属性。</span><span class="sxs-lookup"><span data-stu-id="1c82d-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="1c82d-296">**验证**属性指示 Facebook 是否已验证的帐户通过某些其他方式，如向移动电话发送消息。</span><span class="sxs-lookup"><span data-stu-id="1c82d-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="1c82d-297">将此值保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="1c82d-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="1c82d-298">将再次需要删除的用户数据库中的记录或使用其他 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="1c82d-299">运行该应用程序，并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="1c82d-299">Run the application, and register the new user.</span></span> <span data-ttu-id="1c82d-300">查看**ExtraUserInformation**表以查看已验证属性的值。</span><span class="sxs-lookup"><span data-stu-id="1c82d-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1c82d-301">结束语</span><span class="sxs-lookup"><span data-stu-id="1c82d-301">Conclusion</span></span>

<span data-ttu-id="1c82d-302">你可以在本教程中，创建与 Facebook 集成以支持用户身份验证和注册数据的站点。</span><span class="sxs-lookup"><span data-stu-id="1c82d-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="1c82d-303">您学习了如何为 MVC 4 web 应用程序，以及如何自定义该默认行为设置的默认行为。</span><span class="sxs-lookup"><span data-stu-id="1c82d-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="1c82d-304">相关主题</span><span class="sxs-lookup"><span data-stu-id="1c82d-304">Related topics</span></span>

- [<span data-ttu-id="1c82d-305">使用身份验证和 SQL 数据库中创建的 ASP.NET MVC 应用并部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1c82d-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
