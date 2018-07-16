---
title: ASP.NET Core 中的 Facebook、Google 和外部提供程序身份验证
author: rick-anderson
description: 本教程演示如何使用外部身份验证提供程序通过 OAuth 2.0 生成 ASP.NET Core 2.x 应用。
ms.author: riande
ms.date: 11/01/2016
uid: security/authentication/social/index
ms.openlocfilehash: b2176ef40faaee02c5ef53dbb92a802212e58e8b
ms.sourcegitcommit: e12f45ddcbe99102a74d4077df27d6c0ebba49c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2018
ms.locfileid: "39063320"
---
# <a name="facebook-google-and-external-provider-authentication-in-aspnet-core"></a><span data-ttu-id="c8bba-103">ASP.NET Core 中的 Facebook、Google 和外部提供程序身份验证</span><span class="sxs-lookup"><span data-stu-id="c8bba-103">Facebook, Google, and external provider authentication in ASP.NET Core</span></span>

<span data-ttu-id="c8bba-104">作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c8bba-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c8bba-105">本教程演示如何生成 ASP.NET Core 2.x 应用，该应用可让用户使用外部身份验证提供程序提供的凭据通过 OAuth 2.0 登录。</span><span class="sxs-lookup"><span data-stu-id="c8bba-105">This tutorial demonstrates how to build an ASP.NET Core 2.x app that enables users to log in using OAuth 2.0 with credentials from external authentication providers.</span></span>

<span data-ttu-id="c8bba-106">以下几节中介绍了 [Facebook](xref:security/authentication/facebook-logins)、[Twitter](xref:security/authentication/twitter-logins)、[Google](xref:security/authentication/google-logins) 和 [Microsoft](xref:security/authentication/microsoft-logins) 提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8bba-106">[Facebook](xref:security/authentication/facebook-logins), [Twitter](xref:security/authentication/twitter-logins), [Google](xref:security/authentication/google-logins), and [Microsoft](xref:security/authentication/microsoft-logins) providers are covered in the following sections.</span></span> <span data-ttu-id="c8bba-107">第三方程序包中提供了其他提供程序，例如 [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) 和 [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers)。</span><span class="sxs-lookup"><span data-stu-id="c8bba-107">Other providers are available in third-party packages such as [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) and [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers).</span></span>

![Facebook、Twitter、Google plus 和 Windows 的社交媒体图标](index/_static/social.png)

<span data-ttu-id="c8bba-109">使用户能够使用其当前凭据登录对用户来说十分便利，并且这样做可以将管理登录进程许多复杂操作转移给第三方。</span><span class="sxs-lookup"><span data-stu-id="c8bba-109">Enabling users to sign in with their existing credentials is convenient for the users and shifts many of the complexities of managing the sign-in process onto a third party.</span></span> <span data-ttu-id="c8bba-110">有关社交登录如何驱动流量和客户转换的示例，请参阅 [Facebook](https://www.facebook.com/unsupportedbrowser) 和 [Twitter](https://dev.twitter.com/resources/case-studies) 的案例分析。</span><span class="sxs-lookup"><span data-stu-id="c8bba-110">For examples of how social logins can drive traffic and customer conversions, see case studies by [Facebook](https://www.facebook.com/unsupportedbrowser) and [Twitter](https://dev.twitter.com/resources/case-studies).</span></span>

<span data-ttu-id="c8bba-111">请注意：此处展示的程序包提取了 OAuth 身份验证流的大量复杂操作，但进行故障排除时，可能需要了解相关详细信息。</span><span class="sxs-lookup"><span data-stu-id="c8bba-111">Note: Packages presented here abstract a great deal of complexity of the OAuth authentication flow, but understanding the details may become necessary when troubleshooting.</span></span> <span data-ttu-id="c8bba-112">有许多资源可用，例如，请参阅 [Introduction to OAuth 2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)（OAuth 2 简介）或 [Understanding OAuth 2](http://www.bubblecode.net/2016/01/22/understanding-oauth2/)（了解 OAuth 2）。</span><span class="sxs-lookup"><span data-stu-id="c8bba-112">Many resources are available; for example, see [Introduction to OAuth 2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2) or [Understanding OAuth 2](http://www.bubblecode.net/2016/01/22/understanding-oauth2/).</span></span> <span data-ttu-id="c8bba-113">某些问题可通过查看 [ASP.NET Core source code for the provider packages](https://github.com/aspnet/Security/tree/master/src)（提供程序包的 ASP.NET Core 源代码）解决。</span><span class="sxs-lookup"><span data-stu-id="c8bba-113">Some issues can be resolved by looking at the [ASP.NET Core source code for the provider packages](https://github.com/aspnet/Security/tree/master/src).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="c8bba-114">创建新的 ASP.NET Core 项目</span><span class="sxs-lookup"><span data-stu-id="c8bba-114">Create a New ASP.NET Core Project</span></span>

* <span data-ttu-id="c8bba-115">在 Visual Studio 2017 中，从“开始”页创建新项目，或通过“文件”>“新建”>“项目”进行创建。</span><span class="sxs-lookup"><span data-stu-id="c8bba-115">In Visual Studio 2017, create a new project from the Start Page, or via **File > New > Project**.</span></span>

* <span data-ttu-id="c8bba-116">选择“Visual C#”>“.NET Core”分类中提供的“ASP.NET Core Web 应用程序”模板：</span><span class="sxs-lookup"><span data-stu-id="c8bba-116">Select the **ASP.NET Core Web Application** template available in **Visual C# > .NET Core** category:</span></span>

![“新建项目”对话框](index/_static/new-project.png)

* <span data-ttu-id="c8bba-118">点击“Web 应用程序”，验证“身份验证”是否设置为“单个用户帐户”：</span><span class="sxs-lookup"><span data-stu-id="c8bba-118">Tap **Web Application** and verify **Authentication** is set to **Individual User Accounts**:</span></span>

![“新建 Web 应用程序”对话框](index/_static/select-project.png)

<span data-ttu-id="c8bba-120">请注意：本教程适用于可从向导顶部选择的 ASP.NET Core 2.0 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c8bba-120">Note: This tutorial applies to ASP.NET Core 2.0 SDK version which can be selected at the top of the wizard.</span></span>

## <a name="apply-migrations"></a><span data-ttu-id="c8bba-121">应用迁移</span><span class="sxs-lookup"><span data-stu-id="c8bba-121">Apply migrations</span></span>

* <span data-ttu-id="c8bba-122">运行应用并选择“登录”链接。</span><span class="sxs-lookup"><span data-stu-id="c8bba-122">Run the app and select the **Log in** link.</span></span>
* <span data-ttu-id="c8bba-123">选择“以新用户身份注册”链接。</span><span class="sxs-lookup"><span data-stu-id="c8bba-123">Select the **Register as a new user** link.</span></span>
* <span data-ttu-id="c8bba-124">输入新帐户的电子邮件地址和密码，再选择“注册”。</span><span class="sxs-lookup"><span data-stu-id="c8bba-124">Enter the email and password for the new account, and then select **Register**.</span></span>
* <span data-ttu-id="c8bba-125">按照说明操作来应用迁移。</span><span class="sxs-lookup"><span data-stu-id="c8bba-125">Follow the instructions to apply migrations.</span></span>

## <a name="require-ssl"></a><span data-ttu-id="c8bba-126">要求 SSL</span><span class="sxs-lookup"><span data-stu-id="c8bba-126">Require SSL</span></span>

<span data-ttu-id="c8bba-127">OAuth 2.0 需要使用 SSL 通过 HTTPS 协议进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c8bba-127">OAuth 2.0 requires the use of SSL for authentication over the HTTPS protocol.</span></span>

<span data-ttu-id="c8bba-128">请注意：如果如上图所示，在项目向导的“更改身份验证”对话框上选择“单个用户帐户”选项，使用 ASP.NET Core 2.x 的“Web 应用程序”或“Web API”项目模板创建的项目自动配置为启用 SSL 并通过 http URL 启动。</span><span class="sxs-lookup"><span data-stu-id="c8bba-128">Note: Projects created using **Web Application** or **Web API** project templates for ASP.NET Core 2.x are automatically configured to enable SSL and launch with https URL if the **Individual User Accounts** option was selected on **Change Authentication dialog** in the project wizard as shown above.</span></span>

* <span data-ttu-id="c8bba-129">按照[在 ASP.NET Core 应用中强制实施 SSL](xref:security/enforcing-ssl)主题中的步骤进行操作，要求在站点上使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="c8bba-129">Require SSL on your site by following the steps in [Enforce SSL in an ASP.NET Core app](xref:security/enforcing-ssl) topic.</span></span>

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a><span data-ttu-id="c8bba-130">使用 SecretManager 存储登录提供程序分配的令牌</span><span class="sxs-lookup"><span data-stu-id="c8bba-130">Use SecretManager to store tokens assigned by login providers</span></span>

<span data-ttu-id="c8bba-131">社交登录提供程序在注册过程中分配“应用程序 ID”和“应用程序机密”。</span><span class="sxs-lookup"><span data-stu-id="c8bba-131">Social login providers assign **Application Id** and **Application Secret** tokens during the registration process.</span></span> <span data-ttu-id="c8bba-132">确切的令牌名称因提供程序而异。</span><span class="sxs-lookup"><span data-stu-id="c8bba-132">The exact token names vary by provider.</span></span> <span data-ttu-id="c8bba-133">这些令牌代表应用用来访问其 API 的凭据。</span><span class="sxs-lookup"><span data-stu-id="c8bba-133">These tokens represent the credentials your app uses to access their API.</span></span> <span data-ttu-id="c8bba-134">令牌构成“机密”，可利用[机密管理器](xref:security/app-secrets#secret-manager)将其链接到应用配置。</span><span class="sxs-lookup"><span data-stu-id="c8bba-134">The tokens constitute the "secrets" that can be linked to your app configuration with the help of [Secret Manager](xref:security/app-secrets#secret-manager).</span></span> <span data-ttu-id="c8bba-135">机密管理器是在配置文件（例如 appsettings.json）中存储令牌更安全替代方法。</span><span class="sxs-lookup"><span data-stu-id="c8bba-135">Secret Manager is a more secure alternative to storing the tokens in a configuration file, such as *appsettings.json*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8bba-136">机密管理器仅用于开发目的。</span><span class="sxs-lookup"><span data-stu-id="c8bba-136">Secret Manager is for development purposes only.</span></span> <span data-ttu-id="c8bba-137">可使用 [Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)存储和保护 Azure 测试和生产机密。</span><span class="sxs-lookup"><span data-stu-id="c8bba-137">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

<span data-ttu-id="c8bba-138">按照[在 ASP.NET Core 中进行开发期间安全存储应用机密](xref:security/app-secrets)主题中的步骤进行操作，以便存储以下每个登录提供程序分配的令牌。</span><span class="sxs-lookup"><span data-stu-id="c8bba-138">Follow the steps in [Safe storage of app secrets in development in ASP.NET Core](xref:security/app-secrets) topic to store tokens assigned by each login provider below.</span></span>

## <a name="setup-login-providers-required-by-your-application"></a><span data-ttu-id="c8bba-139">应用程序所需的安装登录提供程序</span><span class="sxs-lookup"><span data-stu-id="c8bba-139">Setup login providers required by your application</span></span>

<span data-ttu-id="c8bba-140">使用以下主题配置应用程序，以使用相应的提供程序：</span><span class="sxs-lookup"><span data-stu-id="c8bba-140">Use the following topics to configure your application to use the respective providers:</span></span>

* <span data-ttu-id="c8bba-141">[Facebook](xref:security/authentication/facebook-logins) 相关说明</span><span class="sxs-lookup"><span data-stu-id="c8bba-141">[Facebook](xref:security/authentication/facebook-logins) instructions</span></span>
* <span data-ttu-id="c8bba-142">[Twitter](xref:security/authentication/twitter-logins) 相关说明</span><span class="sxs-lookup"><span data-stu-id="c8bba-142">[Twitter](xref:security/authentication/twitter-logins) instructions</span></span>
* <span data-ttu-id="c8bba-143">[Google](xref:security/authentication/google-logins) 相关说明</span><span class="sxs-lookup"><span data-stu-id="c8bba-143">[Google](xref:security/authentication/google-logins) instructions</span></span>
* <span data-ttu-id="c8bba-144">[Microsoft](xref:security/authentication/microsoft-logins) 相关说明</span><span class="sxs-lookup"><span data-stu-id="c8bba-144">[Microsoft](xref:security/authentication/microsoft-logins) instructions</span></span>
* <span data-ttu-id="c8bba-145">[其他提供程序](xref:security/authentication/otherlogins)相关说明</span><span class="sxs-lookup"><span data-stu-id="c8bba-145">[Other provider](xref:security/authentication/otherlogins) instructions</span></span>

[!INCLUDE[](~/includes/chain-auth-providers.md)]

## <a name="optionally-set-password"></a><span data-ttu-id="c8bba-146">选择性地设置密码</span><span class="sxs-lookup"><span data-stu-id="c8bba-146">Optionally set password</span></span>

<span data-ttu-id="c8bba-147">使用外部登录提供程序注册，即表明还没有向应用注册密码。</span><span class="sxs-lookup"><span data-stu-id="c8bba-147">When you register with an external login provider, you don't have a password registered with the app.</span></span> <span data-ttu-id="c8bba-148">这可让用户无需创建和记住站点密码，但也会使用户依赖外部登录提供程序。</span><span class="sxs-lookup"><span data-stu-id="c8bba-148">This alleviates you from creating and remembering a password for the site, but it also makes you dependent on the external login provider.</span></span> <span data-ttu-id="c8bba-149">如果外部登录提供程序不可用，则无法登录网站。</span><span class="sxs-lookup"><span data-stu-id="c8bba-149">If the external login provider is unavailable, you won't be able to log in to the web site.</span></span>

<span data-ttu-id="c8bba-150">使用外部提供程序在登录过程中设置的电子邮箱创建密码和登录：</span><span class="sxs-lookup"><span data-stu-id="c8bba-150">To create a password and sign in using your email that you set during the sign in process with external providers:</span></span>

* <span data-ttu-id="c8bba-151">点击右上角的“Hello &lt;电子邮件别名&gt;”链接，导航到“管理”视图。</span><span class="sxs-lookup"><span data-stu-id="c8bba-151">Tap the **Hello &lt;email alias&gt;** link at the top right corner to navigate to the **Manage** view.</span></span>

![Web 应用程序“管理”视图](index/_static/pass1a.png)

* <span data-ttu-id="c8bba-153">点击“创建”</span><span class="sxs-lookup"><span data-stu-id="c8bba-153">Tap **Create**</span></span>

![“设置密码”页](index/_static/pass2a.png)

* <span data-ttu-id="c8bba-155">设置一个有效密码，可以用此密码和邮箱登录。</span><span class="sxs-lookup"><span data-stu-id="c8bba-155">Set a valid password and you can use this to sign in with your email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8bba-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c8bba-156">Next steps</span></span>

* <span data-ttu-id="c8bba-157">本文介绍了外部身份验证，并说明了向 ASP.NET Core 应用添加外部登录所需的先决条件。</span><span class="sxs-lookup"><span data-stu-id="c8bba-157">This article introduced external authentication and explained the prerequisites required to add external logins to your ASP.NET Core app.</span></span>

* <span data-ttu-id="c8bba-158">引用特定于提供程序的页，为应用所需的提供程序配置登录。</span><span class="sxs-lookup"><span data-stu-id="c8bba-158">Reference provider-specific pages to configure logins for the providers required by your app.</span></span>
