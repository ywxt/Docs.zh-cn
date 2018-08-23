---
title: 在 ASP.NET Core Facebook 外部登录安装程序
author: rick-anderson
description: 本教程演示的集成到现有的 ASP.NET Core 应用程序的 Facebook 帐户用户身份验证。
ms.author: riande
ms.date: 08/01/2017
uid: security/authentication/facebook-logins
ms.openlocfilehash: 3ba6fe7785afa268e54e6032f1963c1867f6bb27
ms.sourcegitcommit: 74c09caec8992635825b45b7f065f871d33c077a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "42634804"
---
# <a name="facebook-external-login-setup-in-aspnet-core"></a><span data-ttu-id="8b2e7-103">在 ASP.NET Core Facebook 外部登录安装程序</span><span class="sxs-lookup"><span data-stu-id="8b2e7-103">Facebook external login setup in ASP.NET Core</span></span>

<span data-ttu-id="8b2e7-104">作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8b2e7-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8b2e7-105">本教程演示如何使用户可以使用示例 ASP.NET Core 2.0 项目上创建其 Facebook 帐户登录[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-105">This tutorial shows you how to enable your users to sign in with their Facebook account using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span> <span data-ttu-id="8b2e7-106">Facebook 身份验证要求[Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-106">Facebook authentication requires the [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) NuGet package.</span></span> <span data-ttu-id="8b2e7-107">我们先按照创建 Facebook 应用程序 ID[官方步骤](https://developers.facebook.com)。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-107">We start by creating a Facebook App ID by following the [official steps](https://developers.facebook.com).</span></span>

## <a name="create-the-app-in-facebook"></a><span data-ttu-id="8b2e7-108">在 Facebook 中创建应用</span><span class="sxs-lookup"><span data-stu-id="8b2e7-108">Create the app in Facebook</span></span>

* <span data-ttu-id="8b2e7-109">导航到[Facebook 开发人员应用](https://developers.facebook.com/apps/)页上，并登录。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-109">Navigate to the [Facebook Developers app](https://developers.facebook.com/apps/) page and sign in.</span></span> <span data-ttu-id="8b2e7-110">如果还没有 Facebook 帐户，使用**注册适用于 Facebook**上登录页后，可以创建一个链接。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-110">If you don't already have a Facebook account, use the **Sign up for Facebook** link on the login page to create one.</span></span>

* <span data-ttu-id="8b2e7-111">点击**添加新的应用**中创建新的应用程序 id。 在右上角的按钮</span><span class="sxs-lookup"><span data-stu-id="8b2e7-111">Tap the **Add a New App** button in the upper right corner to create a new App ID.</span></span>

   ![Microsoft Edge 中打开的 Facebook 开发人员门户](index/_static/FBMyApps.png)

* <span data-ttu-id="8b2e7-113">填写表单，然后点击**创建应用程序 ID**按钮。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-113">Fill out the form and tap the **Create App ID** button.</span></span>

   ![创建新的应用 ID 窗体](index/_static/FBNewAppId.png)

* <span data-ttu-id="8b2e7-115">上**选择一个产品**页上，单击**Set Up**上**Facebook 登录**卡。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-115">On the **Select a product** page, click **Set Up** on the **Facebook Login** card.</span></span>

   ![产品安装程序页](index/_static/FBProductSetup.png)

* <span data-ttu-id="8b2e7-117">**快速入门**向导将启动与**选择一个平台**作为第一页。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-117">The **Quickstart** wizard will launch with **Choose a Platform** as the first page.</span></span> <span data-ttu-id="8b2e7-118">现在跳过该向导，通过单击**设置**在左侧菜单中的链接：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-118">Bypass the wizard for now by clicking the **Settings** link in the menu on the left:</span></span>

   ![跳过快速入门](index/_static/FBSkipQuickStart.png)

* <span data-ttu-id="8b2e7-120">此时会显示**客户端 OAuth 设置**页：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-120">You are presented with the **Client OAuth Settings** page:</span></span>

![客户端 OAuth 设置页](index/_static/FBOAuthSetup.png)

* <span data-ttu-id="8b2e7-122">输入你的开发 URI 与 */signin-facebook*追加到**有效的 OAuth 重定向 Uri**字段 (例如： `https://localhost:44320/signin-facebook`)。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-122">Enter your development URI with */signin-facebook* appended into the **Valid OAuth Redirect URIs** field (for example: `https://localhost:44320/signin-facebook`).</span></span> <span data-ttu-id="8b2e7-123">本教程中稍后配置 Facebook 身份验证将自动处理在请求 */signin-facebook*路由实现 OAuth 流。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-123">The Facebook authentication configured later in this tutorial will automatically handle requests at */signin-facebook* route to implement the OAuth flow.</span></span>

> [!NOTE]
> <span data-ttu-id="8b2e7-124">URI */signin-facebook*设置为 Facebook 身份验证提供程序的默认回调。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-124">The URI */signin-facebook* is set as the default callback of the Facebook authentication provider.</span></span> <span data-ttu-id="8b2e7-125">配置 Facebook 身份验证中间件通过继承时，可以更改默认的回调 URI [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath)的属性[FacebookOptions](/dotnet/api/microsoft.aspnetcore.authentication.facebook.facebookoptions)类。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-125">You can change the default callback URI while configuring the Facebook authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [FacebookOptions](/dotnet/api/microsoft.aspnetcore.authentication.facebook.facebookoptions) class.</span></span>

* <span data-ttu-id="8b2e7-126">单击**保存更改**。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-126">Click **Save Changes**.</span></span>

* <span data-ttu-id="8b2e7-127">单击**设置 > 基本**左侧导航窗格中的链接。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-127">Click **Settings > Basic** link in the left navigation.</span></span> 

    <span data-ttu-id="8b2e7-128">在此页上，记下你`App ID`和你`App Secret`。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-128">On this page, make a note of your `App ID` and your `App Secret`.</span></span> <span data-ttu-id="8b2e7-129">你将添加到 ASP.NET Core 应用程序下一节中：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-129">You will add both into your ASP.NET Core application in the next section:</span></span>


* <span data-ttu-id="8b2e7-130">部署站点时需要重新访问**Facebook 登录**安装页并注册一个新的公共 URI。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-130">When deploying the site you need to revisit the **Facebook Login** setup page and register a new public URI.</span></span>

## <a name="store-facebook-app-id-and-app-secret"></a><span data-ttu-id="8b2e7-131">应用商店 Facebook 应用程序 ID 和应用程序密码</span><span class="sxs-lookup"><span data-stu-id="8b2e7-131">Store Facebook App ID and App Secret</span></span>

<span data-ttu-id="8b2e7-132">链接敏感设置，例如 Facebook`App ID`并`App Secret`到应用程序的配置使用[机密管理器](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-132">Link sensitive settings like Facebook `App ID` and `App Secret` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="8b2e7-133">对于本教程的目的，命名为令牌`Authentication:Facebook:AppId`和`Authentication:Facebook:AppSecret`。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-133">For the purposes of this tutorial, name the tokens `Authentication:Facebook:AppId` and `Authentication:Facebook:AppSecret`.</span></span>

<span data-ttu-id="8b2e7-134">执行以下命令来安全地存储`App ID`和`App Secret`使用机密管理器：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-134">Execute the following commands to securely store `App ID` and `App Secret` using Secret Manager:</span></span>

```console
dotnet user-secrets set Authentication:Facebook:AppId <app-id>
dotnet user-secrets set Authentication:Facebook:AppSecret <app-secret>
```

## <a name="configure-facebook-authentication"></a><span data-ttu-id="8b2e7-135">配置 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="8b2e7-135">Configure Facebook Authentication</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8b2e7-136">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8b2e7-136">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="8b2e7-137">将 Facebook 服务中的添加`ConfigureServices`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-137">Add the Facebook service in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddFacebook(facebookOptions =>
{
    facebookOptions.AppId = Configuration["Authentication:Facebook:AppId"];
    facebookOptions.AppSecret = Configuration["Authentication:Facebook:AppSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](~/includes/chain-auth-providers.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8b2e7-138">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8b2e7-138">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="8b2e7-139">安装[Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook)包。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-139">Install the [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) package.</span></span>

* <span data-ttu-id="8b2e7-140">若要使用 Visual Studio 2017 中安装此包，请右键单击项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-140">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="8b2e7-141">若要使用.NET Core CLI 安装，请在项目目录中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-141">To install with .NET Core CLI, execute the following in your project directory:</span></span>

   `dotnet add package Microsoft.AspNetCore.Authentication.Facebook`

<span data-ttu-id="8b2e7-142">添加在到 Facebook 中间件`Configure`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-142">Add the Facebook middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

<span data-ttu-id="8b2e7-143">请参阅[FacebookOptions](/dotnet/api/microsoft.aspnetcore.builder.facebookoptions) Facebook 身份验证支持的配置选项的详细信息的 API 参考。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-143">See the [FacebookOptions](/dotnet/api/microsoft.aspnetcore.builder.facebookoptions) API reference for more information on configuration options supported by Facebook authentication.</span></span> <span data-ttu-id="8b2e7-144">配置选项可用于：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-144">Configuration options can be used to:</span></span>

* <span data-ttu-id="8b2e7-145">请求有关用户的不同信息。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-145">Request different information about the user.</span></span>
* <span data-ttu-id="8b2e7-146">添加查询字符串参数以自定义登录体验。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-146">Add query string arguments to customize the login experience.</span></span>

## <a name="sign-in-with-facebook"></a><span data-ttu-id="8b2e7-147">使用 Facebook 登录</span><span class="sxs-lookup"><span data-stu-id="8b2e7-147">Sign in with Facebook</span></span>

<span data-ttu-id="8b2e7-148">运行你的应用程序，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-148">Run your application and click **Log in**.</span></span> <span data-ttu-id="8b2e7-149">请参阅使用 Facebook 登录的选项。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-149">You see an option to sign in with Facebook.</span></span>

![Web 应用程序： 用户未经过身份验证](index/_static/DoneFacebook.png)

<span data-ttu-id="8b2e7-151">当您单击**Facebook**，你将重定向到 Facebook 进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-151">When you click on **Facebook**, you are redirected to Facebook for authentication:</span></span>

![Facebook 身份验证页面](index/_static/FBLogin.png)

<span data-ttu-id="8b2e7-153">Facebook 身份验证请求的默认公共配置文件和电子邮件地址：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-153">Facebook authentication requests public profile and email address by default:</span></span>

![Facebook 身份验证页面](index/_static/FBLoginDone.png)

<span data-ttu-id="8b2e7-155">输入你的 Facebook 凭据后你重定向回你的站点，你可以设置你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-155">Once you enter your Facebook credentials you are redirected back to your site where you can set your email.</span></span>

<span data-ttu-id="8b2e7-156">现在已在使用 Facebook 凭据登录：</span><span class="sxs-lookup"><span data-stu-id="8b2e7-156">You are now logged in using your Facebook credentials:</span></span>

![Web 应用程序： 用户通过身份验证](index/_static/Done.png)

## <a name="troubleshooting"></a><span data-ttu-id="8b2e7-158">疑难解答</span><span class="sxs-lookup"><span data-stu-id="8b2e7-158">Troubleshooting</span></span>

* <span data-ttu-id="8b2e7-159">**ASP.NET Core 2.x 仅：** 如果标识未通过调用配置`services.AddIdentity`中`ConfigureServices`，尝试进行身份验证将导致*ArgumentException： 必须提供 SignInScheme 选项*。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-159">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="8b2e7-160">在本教程中使用的项目模板可确保，此操作。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-160">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="8b2e7-161">如果尚未通过应用初始迁移创建站点数据库，则获取*处理请求时，数据库操作失败*错误。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-161">If the site database has not been created by applying the initial migration, you get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="8b2e7-162">点击**应用迁移**创建数据库，并刷新以忽略错误继续。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-162">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b2e7-163">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8b2e7-163">Next steps</span></span>

* <span data-ttu-id="8b2e7-164">本文介绍了您如何可以使用 Facebook 进行验证。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-164">This article showed how you can authenticate with Facebook.</span></span> <span data-ttu-id="8b2e7-165">可以遵循类似的方法来使用上列出其他提供程序进行身份验证[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-165">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="8b2e7-166">一旦您将您的网站发布到 Azure web 应用时，应重置`AppSecret`Facebook 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-166">Once you publish your web site to Azure web app, you should reset the `AppSecret` in the Facebook developer portal.</span></span>

* <span data-ttu-id="8b2e7-167">设置`Authentication:Facebook:AppId`和`Authentication:Facebook:AppSecret`作为在 Azure 门户中的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-167">Set the `Authentication:Facebook:AppId` and `Authentication:Facebook:AppSecret` as application settings in the Azure portal.</span></span> <span data-ttu-id="8b2e7-168">配置系统设置以从环境变量读取密钥。</span><span class="sxs-lookup"><span data-stu-id="8b2e7-168">The configuration system is set up to read keys from environment variables.</span></span>
