---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 通过 MVC 4 使用 OAuth 提供程序 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何构建 ASP.NET MVC 4 web 应用程序，使用户能够从 Facebo 之类的外部提供程序的凭据登录...
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: d0203b62c911056fc56ed103c1c42f67816cbbf0
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021750"
---
<a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="4c4d9-103">通过 MVC 4 使用 OAuth 提供程序</span><span class="sxs-lookup"><span data-stu-id="4c4d9-103">Using OAuth Providers with MVC 4</span></span>
====================
<span data-ttu-id="4c4d9-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4c4d9-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4c4d9-105">本教程演示如何构建 ASP.NET MVC 4 web 应用程序，使用户能够从外部提供程序，如 Facebook、 Twitter、 Microsoft 或 Google 凭据登录，然后将集成到这些提供程序的功能的一些应用web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="4c4d9-106">为简单起见，本教程重点介绍使用来自 Facebook 的凭据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="4c4d9-107">若要在 ASP.NET MVC 5 web 应用程序中使用外部凭据，请参阅[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="4c4d9-108">启用这些凭据在您的网站中提供一个明显的优势，因为数以百万计的用户已获得与这些外部提供商的帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="4c4d9-109">这些用户可能更倾向于注册为您的网站，如果它们不需要创建和记住一组新的凭据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="4c4d9-110">此外，通过这些提供程序之一的用户已登录后，您可以将从提供程序的社交操作整合。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="4c4d9-111">你将生成</span><span class="sxs-lookup"><span data-stu-id="4c4d9-111">What you'll build</span></span>

<span data-ttu-id="4c4d9-112">在本教程中有两个主要目标：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="4c4d9-113">使用户能够使用 OAuth 提供程序的凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="4c4d9-114">从提供程序检索帐户信息并将该信息与你的站点的帐户注册集成。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="4c4d9-115">虽然在本教程中的这些示例着重于将 Facebook 用作身份验证提供程序，你可修改代码以使用任何提供程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="4c4d9-116">若要实现任何提供程序的步骤是非常类似于您将看到在本教程中的步骤。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="4c4d9-117">只会注意到设置的显著区别时直接调用提供程序的 API。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c4d9-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="4c4d9-118">Prerequisites</span></span>

- <span data-ttu-id="4c4d9-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="4c4d9-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="4c4d9-120">Or</span><span class="sxs-lookup"><span data-stu-id="4c4d9-120">Or</span></span>

- <span data-ttu-id="4c4d9-121">Microsoft Visual Studio 2010 SP1 或[Visual Web Developer 速成版 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="4c4d9-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="4c4d9-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="4c4d9-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="4c4d9-123">此外，本主题假定你具有有关 ASP.NET MVC 和 Visual Studio 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="4c4d9-124">如果您需要 ASP.NET MVC 4 简介，请参阅[ASP.NET MVC 4 简介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="4c4d9-125">创建项目</span><span class="sxs-lookup"><span data-stu-id="4c4d9-125">Create the project</span></span>

<span data-ttu-id="4c4d9-126">在 Visual Studio 中新建 ASP.NET MVC 4 Web 应用程序，并将其命名&quot;OAuthMVC&quot;。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="4c4d9-127">你可以面向.NET Framework 4.5 或 4。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-127">You can target either .NET Framework 4.5 or 4.</span></span>

![创建项目](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="4c4d9-129">在新建 ASP.NET MVC 4 项目窗口中，选择**Internet 应用程序**并保留**Razor**作为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![选择 Internet 应用程序](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="4c4d9-131">启用提供程序</span><span class="sxs-lookup"><span data-stu-id="4c4d9-131">Enable a provider</span></span>

<span data-ttu-id="4c4d9-132">如果使用 Internet 应用程序模板创建的 MVC 4 web 应用程序，项目将创建具有名为 AuthConfig.cs 应用中的文件\_开始文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 文件](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="4c4d9-134">AuthConfig 文件包含注册外部身份验证提供程序的客户端的代码。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="4c4d9-135">默认情况下，此代码是加上注释，以便启用任何外部提供程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="4c4d9-136">必须取消注释此代码以使用外部身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="4c4d9-137">取消注释只想要包括在你的站点中的提供程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="4c4d9-138">对于本教程，你将只启用 Facebook 凭据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="4c4d9-139">请注意，在上面的示例中，该方法包含空字符串用于注册参数。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="4c4d9-140">如果尝试运行应用程序现在，应用程序将引发参数异常，因为参数不允许使用空字符串。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="4c4d9-141">若要提供有效的值，必须注册您的网站向外部提供程序，如在下一节中所示。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="4c4d9-142">使用外部提供程序注册</span><span class="sxs-lookup"><span data-stu-id="4c4d9-142">Registering with an external provider</span></span>

<span data-ttu-id="4c4d9-143">用户进行身份验证使用外部提供程序的凭据，必须使用提供程序注册你的网站。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="4c4d9-144">注册你的站点时，你将收到参数 （如密钥或 id 和密码） 来注册客户端时包括。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="4c4d9-145">您必须有你想要使用的提供程序的帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="4c4d9-146">本教程不会不会显示所有使用这些提供程序进行注册，必须执行的步骤。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="4c4d9-147">不执行这些步骤通常比较困难。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-147">The steps are typically not difficult.</span></span> <span data-ttu-id="4c4d9-148">若要成功注册你的站点，请按照这些网站上提供的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="4c4d9-149">若要开始使用注册你的网站，请参阅有关在开发人员网站：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="4c4d9-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="4c4d9-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="4c4d9-151">Google</span><span class="sxs-lookup"><span data-stu-id="4c4d9-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="4c4d9-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="4c4d9-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="4c4d9-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="4c4d9-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="4c4d9-154">如果向 Facebook 注册你的网站，则可以提供&quot;localhost&quot;站点域和`&quot; http://localhost/&quot;`对于 URL，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="4c4d9-155">使用 localhost 适用于大多数提供程序，但当前不使用 Microsoft 提供程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="4c4d9-156">对于 Microsoft 提供程序，必须包含有效的网站 URL。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![注册站点](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="4c4d9-158">在上图中，已删除的应用程序 id、 应用程序密码和联系人电子邮件的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="4c4d9-159">实际注册你的站点时，这些值将会显示。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="4c4d9-160">想要注意的应用程序 id 和应用机密的值，因为会将它们添加到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="4c4d9-161">创建测试用户</span><span class="sxs-lookup"><span data-stu-id="4c4d9-161">Creating test users</span></span>

<span data-ttu-id="4c4d9-162">如果您不介意使用现有的 Facebook 帐户来测试您的站点，则可以跳过本部分中。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="4c4d9-163">为应用程序的 Facebook 应用程序管理页中，可以轻松创建测试用户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="4c4d9-164">您可以使用这些测试帐户登录到你的站点。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="4c4d9-165">通过单击创建测试用户**角色**在左侧的导航窗格中单击链接**创建**链接。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![创建测试用户](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="4c4d9-167">Facebook 站点会自动创建测试帐户的请求数。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="4c4d9-168">从提供程序中添加应用程序 id 和机密</span><span class="sxs-lookup"><span data-stu-id="4c4d9-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="4c4d9-169">现在，已从 Facebook 中接收的 id 和密码，请返回到 AuthConfig 文件并将其添加作为参数值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="4c4d9-170">下面显示的值不是实际值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="4c4d9-171">外部凭据登录</span><span class="sxs-lookup"><span data-stu-id="4c4d9-171">Log in with external credentials</span></span>

<span data-ttu-id="4c4d9-172">这是所要执行的操作启用你的站点中的外部凭据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="4c4d9-173">运行你的应用程序并单击右上角的登录链接。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="4c4d9-174">该模板会自动识别你已注册为提供程序的 Facebook 和提供程序包括一个按钮。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="4c4d9-175">如果注册多个提供程序时，会自动包括为每个按钮。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![外部登录](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="4c4d9-177">本教程不介绍如何为外部提供程序自定义按钮中的日志。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="4c4d9-178">该信息，请参阅[时使用 OAuth/OpenID 自定义登录 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="4c4d9-179">单击 Facebook 按钮，能够使用 Facebook 凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="4c4d9-180">您选择其中一个外部提供程序，意味着，将重定向到该站点并且该服务以用户身份登录系统提示。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="4c4d9-181">下图显示为 Facebook 登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="4c4d9-182">它指出，使用的你的 Facebook 帐户登录到名为 oauthmvcexample 的站点。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 身份验证](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="4c4d9-184">使用 Facebook 凭据登录后, 一个页面将通知用户该站点将有权访问的基本信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![请求权限](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="4c4d9-186">选择后**转到应用**，用户必须注册为该站点。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="4c4d9-187">用户使用 Facebook 凭据登录后，下图显示了注册页。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="4c4d9-188">用户名称是通常使用与该提供程序的名称预先填充。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="4c4d9-190">单击**注册**以完成注册。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="4c4d9-191">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-191">Close the browser.</span></span>

<span data-ttu-id="4c4d9-192">您可以看到新的帐户已添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="4c4d9-193">在服务器资源管理器中打开**DefaultConnection**数据库，打开**表**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![数据库表](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="4c4d9-195">右键单击**UserProfile**表，然后选择**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![显示数据](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="4c4d9-197">你将看到添加的新帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-197">You will see the new account you added.</span></span> <span data-ttu-id="4c4d9-198">查看中的数据**网页\_OAuthMembership**表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="4c4d9-199">你将看到与刚刚添加的帐户的外部提供程序相关的更多数据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="4c4d9-200">如果只想要启用外部身份验证，则已完成。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="4c4d9-201">但是，您可以进一步将集成从提供程序的信息到新用户注册过程中，如以下各节中所示。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="4c4d9-202">创建模型的其他用户信息</span><span class="sxs-lookup"><span data-stu-id="4c4d9-202">Create models for additional user information</span></span>

<span data-ttu-id="4c4d9-203">您注意到在前面部分中，您不需要检索要处理的内置帐户注册任何其他信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="4c4d9-204">但是，大多数外部提供程序传递有关用户的附加信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="4c4d9-205">以下部分说明如何保留这些信息并将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="4c4d9-206">具体而言，将保留用户的完整名称，用户的个人 web 页的 URI 的值和一个值，指示是否验证 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="4c4d9-207">将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)添加用于存储其他用户信息的表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="4c4d9-208">要添加到现有数据库表，因此您首先需要创建当前数据库的快照。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="4c4d9-209">通过创建当前数据库的快照，稍后可以创建包含新的表的迁移。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="4c4d9-210">若要创建当前数据库的快照：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="4c4d9-211">打开**包管理器控制台**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="4c4d9-212">运行命令**启用迁移**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="4c4d9-213">运行命令**IgnoreChanges 添加迁移初始 –**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="4c4d9-214">运行命令**更新数据库**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-214">Run the command **update-database**</span></span>

<span data-ttu-id="4c4d9-215">现在，您将添加新属性。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-215">Now, you will add the new properties.</span></span> <span data-ttu-id="4c4d9-216">在 Models 文件夹中，打开 AccountModels.cs 文件中，并查找 RegisterExternalLoginModel 类。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="4c4d9-217">RegisterExternalLoginModel 类保存回来自身份验证提供程序的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="4c4d9-218">添加命名 FullName 和链接，为以下突出显示部分的属性。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="4c4d9-219">此外在 AccountModels.cs，添加一个名为 ExtraUserInformation 的新类。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="4c4d9-220">此类表示将在数据库中创建的新表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="4c4d9-221">在 UsersContext 类中，添加突出显示的代码下面创建新的类的 DbSet 属性。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="4c4d9-222">现在您就可以创建新表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-222">You are now ready to create the new table.</span></span> <span data-ttu-id="4c4d9-223">再次，这一次打开包管理器控制台：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="4c4d9-224">运行命令**添加迁移 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="4c4d9-225">运行命令**更新数据库**</span><span class="sxs-lookup"><span data-stu-id="4c4d9-225">Run the command **update-database**</span></span>

<span data-ttu-id="4c4d9-226">在数据库中现在存在新表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="4c4d9-227">检索其他数据</span><span class="sxs-lookup"><span data-stu-id="4c4d9-227">Retrieve the additional data</span></span>

<span data-ttu-id="4c4d9-228">有两种方法来检索其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="4c4d9-229">第一种方法是保留用户数据传递回去，默认情况下，身份验证请求过程。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="4c4d9-230">第二种方法是专门调用提供程序 API 和请求的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="4c4d9-231">FullName 和链接值都会自动传递回的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="4c4d9-232">通过 Facebook API 调用检索值，该值指示是否验证 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="4c4d9-233">首先，将为 FullName 和链接，填充值，然后更高版本，你将获取已验证的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="4c4d9-234">若要检索其他用户数据，请打开**AccountController.cs**中的文件**控制器**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="4c4d9-235">此文件包含日志记录、 注册和管理帐户的逻辑。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="4c4d9-236">具体而言，请注意，调用的方法**ExternalLoginCallback**并**ExternalLoginConfirmation**。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="4c4d9-237">在这些方法中，可以添加代码以自定义应用程序的外部登录操作。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="4c4d9-238">第一行**ExternalLoginCallback**方法包含：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="4c4d9-239">其他用户数据将传回到**ExtraData**的属性**AuthenticationResult**从返回的对象**VerifyAuthentication**方法。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="4c4d9-240">Facebook 客户端包含中的以下值**ExtraData**属性：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="4c4d9-241">id</span><span class="sxs-lookup"><span data-stu-id="4c4d9-241">id</span></span>
- <span data-ttu-id="4c4d9-242">name</span><span class="sxs-lookup"><span data-stu-id="4c4d9-242">name</span></span>
- <span data-ttu-id="4c4d9-243">链接</span><span class="sxs-lookup"><span data-stu-id="4c4d9-243">link</span></span>
- <span data-ttu-id="4c4d9-244">性别</span><span class="sxs-lookup"><span data-stu-id="4c4d9-244">gender</span></span>
- <span data-ttu-id="4c4d9-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="4c4d9-245">accesstoken</span></span>

<span data-ttu-id="4c4d9-246">其他提供程序将 ExtraData 属性中具有类似但略有不同的数据。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="4c4d9-247">如果用户是您的网站的新手，将检索某些其他数据，并将该数据传递给确认视图。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="4c4d9-248">仅当用户不熟悉你的站点运行的方法中代码的最后一个块。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="4c4d9-249">替换为以下行：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="4c4d9-250">用下面这行：</span><span class="sxs-lookup"><span data-stu-id="4c4d9-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="4c4d9-251">此更改仅包括 FullName 和链接属性的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="4c4d9-252">在中**ExternalLoginConfirmation**方法中，修改以下代码，突出显示的那样以保存其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="4c4d9-253">调整视图</span><span class="sxs-lookup"><span data-stu-id="4c4d9-253">Adjusting the view</span></span>

<span data-ttu-id="4c4d9-254">从提供程序检索其他用户数据将显示在注册页。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="4c4d9-255">在中**视图**/**帐户**文件夹中，打开**ExternalLoginConfirmation.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="4c4d9-256">以下用户名称与现有字段，为 FullName、 链接和 PictureLink 中添加字段。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="4c4d9-257">你现基本准备好运行应用程序并注册一个新用户保存的其他信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="4c4d9-258">必须具有与站点尚未注册一个帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="4c4d9-259">您可以使用不同的测试帐户，或删除中的行**UserProfile**并**网页\_OAuthMembership**你想要重复使用的帐户的表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="4c4d9-260">通过删除这些行，您需要确保重新注册了该帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="4c4d9-261">运行应用程序并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-261">Run the application and register the new user.</span></span> <span data-ttu-id="4c4d9-262">请注意，这一次确认页包含更多的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="4c4d9-264">注册后，关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-264">After completing registration, close the browser.</span></span> <span data-ttu-id="4c4d9-265">请注意中的新值在数据库中查找**ExtraUserInformation**表。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="4c4d9-266">安装用于 Facebook API NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4c4d9-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="4c4d9-267">提供 Facebook [API](https://developers.facebook.com/docs/reference/apis/)可调用以执行操作。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="4c4d9-268">通过将定向发送 HTTP 请求，或使用安装 NuGet 包，它方便了发送这些请求，可以调用 Facebook API。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="4c4d9-269">使用 NuGet 包显示在本教程中，但安装 NuGet 包不重要。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="4c4d9-270">本教程演示如何使用 Facebook C# SDK 包。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="4c4d9-271">有其他帮助调用 Facebook API 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="4c4d9-272">从**管理 NuGet 包**windows 中，选择 Facebook C# SDK 包。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![安装包](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="4c4d9-274">将使用 Facebook C# SDK 调用的用户需要访问令牌的操作。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="4c4d9-275">下一部分演示如何获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="4c4d9-276">检索访问令牌</span><span class="sxs-lookup"><span data-stu-id="4c4d9-276">Retrieve access token</span></span>

<span data-ttu-id="4c4d9-277">验证用户的凭据后最外部提供程序传递回访问令牌。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="4c4d9-278">此访问令牌是非常重要，因为它使你可以调用仅可供经过身份验证的用户的操作。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="4c4d9-279">因此，检索和存储访问令牌时非常重要您想要提供更多的功能。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="4c4d9-280">根据外部提供程序，访问令牌可能只在有限是时间的有效。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="4c4d9-281">若要确保您有一个有效的访问令牌，您将检索它每次用户登录，并将其存储为会话值而不是将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="4c4d9-282">在中**ExternalLoginCallback**方法，返回还传递访问令牌**ExtraData**属性**AuthenticationResult**对象。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="4c4d9-283">添加到突出显示的代码**ExternalLoginCallback**以保存中的访问令牌**会话**对象。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="4c4d9-284">每次用户使用 Facebook 帐户登录时运行此代码。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="4c4d9-285">虽然此示例从 Facebook 中检索访问令牌，可以通过相同的键名为从任何外部提供程序检索访问令牌&quot;accesstoken&quot;。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="4c4d9-286">注销</span><span class="sxs-lookup"><span data-stu-id="4c4d9-286">Logging off</span></span>

<span data-ttu-id="4c4d9-287">默认值**注销**方法记录用户从应用程序，但不会记录用户从外部提供程序。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="4c4d9-288">若要从 Facebook，将用户登录，并防止令牌保持用户注销后，可以添加到以下突出显示的代码**注销**AccountController 中的方法。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="4c4d9-289">中提供的值`next`参数是要使用后用户已从 Facebook 注销的 URL。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="4c4d9-290">在测试时在本地计算机上，将为你的本地网站提供正确的端口号。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="4c4d9-291">在生产中，将提供一个默认页，例如 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="4c4d9-292">检索需要访问令牌的用户信息</span><span class="sxs-lookup"><span data-stu-id="4c4d9-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="4c4d9-293">现在，存储的访问令牌并安装 Facebook C# SDK 包后，你可以使用它们一起以从 Facebook 中请求的其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="4c4d9-294">在中**ExternalLoginConfirmation**方法中，创建的实例**FacebookClient**类通过将访问令牌的值传递。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="4c4d9-295">请求的值**验证**当前经过身份验证的用户的属性。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="4c4d9-296">**验证**属性指示是否 Facebook 已验证的帐户通过其他方式，如到移动电话发送短信。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="4c4d9-297">在数据库中保存此值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="4c4d9-298">再次需要删除用户，在数据库中的记录或使用其他 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="4c4d9-299">运行该应用程序，并注册新的用户。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-299">Run the application, and register the new user.</span></span> <span data-ttu-id="4c4d9-300">看看**ExtraUserInformation**表以查看已验证属性的值。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4c4d9-301">结束语</span><span class="sxs-lookup"><span data-stu-id="4c4d9-301">Conclusion</span></span>

<span data-ttu-id="4c4d9-302">在本教程中，您可以创建与 Facebook 集成进行用户身份验证和注册数据的站点。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="4c4d9-303">您学习了如何为 MVC 4 web 应用程序，以及如何自定义该默认行为设置的默认行为。</span><span class="sxs-lookup"><span data-stu-id="4c4d9-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="4c4d9-304">相关主题</span><span class="sxs-lookup"><span data-stu-id="4c4d9-304">Related topics</span></span>

- [<span data-ttu-id="4c4d9-305">使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="4c4d9-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
