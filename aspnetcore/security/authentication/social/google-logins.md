---
title: 在 ASP.NET Core Google 外部登录安装程序
author: rick-anderson
description: 本教程演示的集成到现有的 ASP.NET Core 应用程序的 Google 帐户用户身份验证。
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 11/11/2018
uid: security/authentication/google-logins
ms.openlocfilehash: e5deda5d521643e3155be00f4630a86c6a82575c
ms.sourcegitcommit: 49faca2644590fc081d86db46ea5e29edfc28b7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2018
ms.locfileid: "53121526"
---
# <a name="google-external-login-setup-in-aspnet-core"></a><span data-ttu-id="e37c5-103">在 ASP.NET Core Google 外部登录安装程序</span><span class="sxs-lookup"><span data-stu-id="e37c5-103">Google external login setup in ASP.NET Core</span></span>

<span data-ttu-id="e37c5-104">作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e37c5-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e37c5-105">本教程演示如何使用户可以使用示例 ASP.NET Core 2.0 项目上创建其 Google + 帐户登录[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="e37c5-105">This tutorial shows you how to enable your users to sign in with their Google+ account using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span> <span data-ttu-id="e37c5-106">我们首先需要遵循[官方步骤](https://developers.google.com/identity/sign-in/web/devconsole-project)Google API 控制台中创建新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e37c5-106">We start by following the [official steps](https://developers.google.com/identity/sign-in/web/devconsole-project) to create a new app in Google API Console.</span></span>

## <a name="create-the-app-in-google-api-console"></a><span data-ttu-id="e37c5-107">在 Google API 控制台中创建应用</span><span class="sxs-lookup"><span data-stu-id="e37c5-107">Create the app in Google API Console</span></span>

* <span data-ttu-id="e37c5-108">导航到[ https://console.developers.google.com/projectselector/apis/library ](https://console.developers.google.com/projectselector/apis/library)并登录。</span><span class="sxs-lookup"><span data-stu-id="e37c5-108">Navigate to [https://console.developers.google.com/projectselector/apis/library](https://console.developers.google.com/projectselector/apis/library) and sign in.</span></span> <span data-ttu-id="e37c5-109">如果还没有 Google 帐户，使用**更多选项** > **[创建帐户](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)** 链接创建一个链接：</span><span class="sxs-lookup"><span data-stu-id="e37c5-109">If you don't already have a Google account, use **More options** > **[Create account](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)** link to create one:</span></span>

![Google API 控制台](index/_static/GoogleConsoleLogin.png)

* <span data-ttu-id="e37c5-111">将重定向到**API 管理器库**页：</span><span class="sxs-lookup"><span data-stu-id="e37c5-111">You are redirected to **API Manager Library** page:</span></span>

![在 API 管理器库页上的登录](index/_static/GoogleConsoleSwitchboard.png)

* <span data-ttu-id="e37c5-113">点击**创建**并输入你**项目名称**:</span><span class="sxs-lookup"><span data-stu-id="e37c5-113">Tap **Create** and enter your **Project name**:</span></span>

![“新建项目”对话框](index/_static/GoogleConsoleNewProj.png)

* <span data-ttu-id="e37c5-115">接受对话框中，你将重定向回到库页允许您选择新应用的功能。</span><span class="sxs-lookup"><span data-stu-id="e37c5-115">After accepting the dialog, you are redirected back to the Library page allowing you to choose features for your new app.</span></span> <span data-ttu-id="e37c5-116">查找**Google + API**在列表中，单击其链接以添加 API 功能：</span><span class="sxs-lookup"><span data-stu-id="e37c5-116">Find **Google+ API** in the list and click on its link to add the API feature:</span></span>

![在 API 管理器库页中搜索"Google + API"](index/_static/GoogleConsoleChooseApi.png)

* <span data-ttu-id="e37c5-118">显示新添加的 API 的页。</span><span class="sxs-lookup"><span data-stu-id="e37c5-118">The page for the newly added API is displayed.</span></span> <span data-ttu-id="e37c5-119">点击**启用**将 Google + 登录功能中添加到您的应用程序：</span><span class="sxs-lookup"><span data-stu-id="e37c5-119">Tap **Enable** to add Google+ sign in feature to your app:</span></span>

![API 管理器 Google + API 页上的登录](index/_static/GoogleConsoleEnableApi.png)

* <span data-ttu-id="e37c5-121">启用 API 后, 点击**创建凭据**若要配置的机密：</span><span class="sxs-lookup"><span data-stu-id="e37c5-121">After enabling the API, tap **Create credentials** to configure the secrets:</span></span>

![在 API 管理器 Google + API 页上创建凭据按钮](index/_static/GoogleConsoleGoCredentials.png)

* <span data-ttu-id="e37c5-123">选择：</span><span class="sxs-lookup"><span data-stu-id="e37c5-123">Choose:</span></span>
  * <span data-ttu-id="e37c5-124">**Google + API**</span><span class="sxs-lookup"><span data-stu-id="e37c5-124">**Google+ API**</span></span>
  * <span data-ttu-id="e37c5-125">**Web 服务器 (例如 node.js，Tomcat)**，和</span><span class="sxs-lookup"><span data-stu-id="e37c5-125">**Web server (e.g. node.js, Tomcat)**, and</span></span>
  * <span data-ttu-id="e37c5-126">**用户数据**:</span><span class="sxs-lookup"><span data-stu-id="e37c5-126">**User data**:</span></span>

![API 管理器凭据页： 找出哪些类型的凭据，需要面板](index/_static/GoogleConsoleChooseCred.png)

* <span data-ttu-id="e37c5-128">点击**我需要什么凭据？** 转到应用配置，第二个步骤**创建 OAuth 2.0 客户端 ID**:</span><span class="sxs-lookup"><span data-stu-id="e37c5-128">Tap **What credentials do I need?** which takes you to the second step of app configuration, **Create an OAuth 2.0 client ID**:</span></span>

![API 管理器凭据页： 创建 OAuth 2.0 客户端 ID](index/_static/GoogleConsoleCreateClient.png)

* <span data-ttu-id="e37c5-130">因为我们将 Google + 项目创建与只是一项功能 （登录），我们可以输入相同**名称**与我们的项目使用 OAuth 2.0 客户端 id。</span><span class="sxs-lookup"><span data-stu-id="e37c5-130">Because we are creating a Google+ project with just one feature (sign in), we can enter the same **Name** for the OAuth 2.0 client ID as the one we used for the project.</span></span>

* <span data-ttu-id="e37c5-131">输入你的开发 URI 与`/signin-google`追加到**已授权重定向 Uri**字段 (例如： `https://localhost:44320/signin-google`)。</span><span class="sxs-lookup"><span data-stu-id="e37c5-131">Enter your development URI with `/signin-google` appended into the **Authorized redirect URIs** field (for example: `https://localhost:44320/signin-google`).</span></span> <span data-ttu-id="e37c5-132">本教程中稍后配置 Google 身份验证将自动处理在请求`/signin-google`路由实现 OAuth 流。</span><span class="sxs-lookup"><span data-stu-id="e37c5-132">The Google authentication configured later in this tutorial will automatically handle requests at `/signin-google` route to implement the OAuth flow.</span></span>

> [!NOTE]
> <span data-ttu-id="e37c5-133">URI 段`/signin-google`设置为默认的 Google 身份验证提供程序的回调。</span><span class="sxs-lookup"><span data-stu-id="e37c5-133">The URI segment `/signin-google` is set as the default callback of the Google authentication provider.</span></span> <span data-ttu-id="e37c5-134">配置 Google 身份验证中间件通过继承时，可以更改默认的回调 URI [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath)的属性[GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions)类。</span><span class="sxs-lookup"><span data-stu-id="e37c5-134">You can change the default callback URI while configuring the Google authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions) class.</span></span>

* <span data-ttu-id="e37c5-135">按 tab 键以添加**已授权重定向 Uri**条目。</span><span class="sxs-lookup"><span data-stu-id="e37c5-135">Press TAB to add the **Authorized redirect URIs** entry.</span></span>

* <span data-ttu-id="e37c5-136">点击**创建客户端 ID**，转到第三个步骤中，其中**设置 OAuth 2.0 许可屏幕**:</span><span class="sxs-lookup"><span data-stu-id="e37c5-136">Tap **Create client ID**, which takes you to the third step, **Set up the OAuth 2.0 consent screen**:</span></span>

![API 管理器凭据页： 设置 OAuth 2.0 许可屏幕](index/_static/GoogleConsoleAddCred.png)

* <span data-ttu-id="e37c5-138">输入你的公众**电子邮件地址**并**产品名称**Google + 提示用户登录时为你的应用所示。</span><span class="sxs-lookup"><span data-stu-id="e37c5-138">Enter your public facing **Email address** and the **Product name** shown for your app when Google+ prompts the user to sign in.</span></span> <span data-ttu-id="e37c5-139">其他选项都位于**更多自定义选项**。</span><span class="sxs-lookup"><span data-stu-id="e37c5-139">Additional options are available under **More customization options**.</span></span>

* <span data-ttu-id="e37c5-140">点击**继续**继续到最后一个步骤中，**下载凭据**:</span><span class="sxs-lookup"><span data-stu-id="e37c5-140">Tap **Continue** to proceed to the last step, **Download credentials**:</span></span>

![API 管理器凭据页： 下载凭据](index/_static/GoogleConsoleFinish.png)

* <span data-ttu-id="e37c5-142">点击**下载**若要使用应用程序机密保存 JSON 文件并**完成**以完成创建新的应用。</span><span class="sxs-lookup"><span data-stu-id="e37c5-142">Tap **Download** to save a JSON file with application secrets, and **Done** to complete creation of the new app.</span></span>

* <span data-ttu-id="e37c5-143">部署站点时将需要重新访问**Google Console**并注册新的公共 url。</span><span class="sxs-lookup"><span data-stu-id="e37c5-143">When deploying the site you'll need to revisit the **Google Console** and register a new public url.</span></span>

## <a name="store-google-clientid-and-clientsecret"></a><span data-ttu-id="e37c5-144">应用商店 Google ClientID 和 ClientSecret</span><span class="sxs-lookup"><span data-stu-id="e37c5-144">Store Google ClientID and ClientSecret</span></span>

<span data-ttu-id="e37c5-145">链接敏感设置，例如 Google`Client ID`并`Client Secret`到应用程序的配置使用[机密管理器](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="e37c5-145">Link sensitive settings like Google `Client ID` and `Client Secret` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="e37c5-146">对于本教程的目的，命名为令牌`Authentication:Google:ClientId`和`Authentication:Google:ClientSecret`。</span><span class="sxs-lookup"><span data-stu-id="e37c5-146">For the purposes of this tutorial, name the tokens `Authentication:Google:ClientId` and `Authentication:Google:ClientSecret`.</span></span>

<span data-ttu-id="e37c5-147">可以在下一步中下载的 JSON 文件中找到这些令牌的值`web.client_id`和`web.client_secret`。</span><span class="sxs-lookup"><span data-stu-id="e37c5-147">The values for these tokens can be found in the JSON file downloaded in the previous step under `web.client_id` and `web.client_secret`.</span></span>

## <a name="configure-google-authentication"></a><span data-ttu-id="e37c5-148">配置 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="e37c5-148">Configure Google Authentication</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e37c5-149">将 Google 服务中的添加`ConfigureServices`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="e37c5-149">Add the Google service in the `ConfigureServices` method in *Startup.cs* file:</span></span>

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddGoogle(googleOptions =>
{
    googleOptions.ClientId = Configuration["Authentication:Google:ClientId"];
    googleOptions.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e37c5-150">在本教程中使用的项目模板可确保[Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google)安装包。</span><span class="sxs-lookup"><span data-stu-id="e37c5-150">The project template used in this tutorial ensures that [Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google) package is installed.</span></span>

* <span data-ttu-id="e37c5-151">若要使用 Visual Studio 2017 中安装此包，请右键单击项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="e37c5-151">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="e37c5-152">若要使用.NET Core CLI 安装，请在项目目录中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e37c5-152">To install with .NET Core CLI, execute the following in your project directory:</span></span>

`dotnet add package Microsoft.AspNetCore.Authentication.Google`

<span data-ttu-id="e37c5-153">添加中的 Google 中间件`Configure`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="e37c5-153">Add the Google middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseGoogleAuthentication(new GoogleOptions()
{
    ClientId = Configuration["Authentication:Google:ClientId"],
    ClientSecret = Configuration["Authentication:Google:ClientSecret"]
});
```

::: moniker-end

<span data-ttu-id="e37c5-154">请参阅[GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) Google 身份验证支持的配置选项的详细信息的 API 参考。</span><span class="sxs-lookup"><span data-stu-id="e37c5-154">See the [GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) API reference for more information on configuration options supported by Google authentication.</span></span> <span data-ttu-id="e37c5-155">这可以用于请求有关用户的不同信息。</span><span class="sxs-lookup"><span data-stu-id="e37c5-155">This can be used to request different information about the user.</span></span>

## <a name="sign-in-with-google"></a><span data-ttu-id="e37c5-156">使用 Google 登录</span><span class="sxs-lookup"><span data-stu-id="e37c5-156">Sign in with Google</span></span>

<span data-ttu-id="e37c5-157">运行你的应用程序，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="e37c5-157">Run your application and click **Log in**.</span></span> <span data-ttu-id="e37c5-158">若要使用 Google 登录的选项将显示：</span><span class="sxs-lookup"><span data-stu-id="e37c5-158">An option to sign in with Google appears:</span></span>

![Microsoft Edge 中运行 web 应用程序： 用户未经过身份验证](index/_static/DoneGoogle.png)

<span data-ttu-id="e37c5-160">当您单击 Google 时，你将重定向到 Google 进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="e37c5-160">When you click on Google, you are redirected to Google for authentication:</span></span>

![Google 身份验证对话框](index/_static/GoogleLogin.png)

<span data-ttu-id="e37c5-162">后输入你的 Google 凭据，然后你将重定向回 web 站点，你可以设置你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="e37c5-162">After entering your Google credentials, then you are redirected back to the web site where you can set your email.</span></span>

<span data-ttu-id="e37c5-163">现在已在使用你的 Google 凭据进行登录：</span><span class="sxs-lookup"><span data-stu-id="e37c5-163">You are now logged in using your Google credentials:</span></span>

![Microsoft Edge 中运行 web 应用程序： 用户通过身份验证](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a><span data-ttu-id="e37c5-165">疑难解答</span><span class="sxs-lookup"><span data-stu-id="e37c5-165">Troubleshooting</span></span>

* <span data-ttu-id="e37c5-166">如果你收到`403 (Forbidden)`从你自己的应用时，请确保在开发模式 （或中断到调试器中相同的错误） 中正在运行错误页**Google + API**中已启用**API 管理器库**按照列出的步骤[本页上早期](#create-the-app-in-google-api-console)。</span><span class="sxs-lookup"><span data-stu-id="e37c5-166">If you receive a `403 (Forbidden)` error page from your own app when running in development mode (or break into the debugger with the same error), ensure that **Google+ API** has been enabled in the **API Manager Library** by following the steps listed [earlier on this page](#create-the-app-in-google-api-console).</span></span> <span data-ttu-id="e37c5-167">如果在登录不起作用，并且如果没有收到任何错误，切换到开发模式，以使问题更易于调试。</span><span class="sxs-lookup"><span data-stu-id="e37c5-167">If the sign in doesn't work and you aren't getting any errors, switch to development mode to make the issue easier to debug.</span></span>
* <span data-ttu-id="e37c5-168">**ASP.NET Core 2.x 仅：** 如果标识未通过调用配置`services.AddIdentity`中`ConfigureServices`，尝试进行身份验证将导致*ArgumentException： 必须提供 SignInScheme 选项*。</span><span class="sxs-lookup"><span data-stu-id="e37c5-168">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="e37c5-169">在本教程中使用的项目模板可确保，此操作。</span><span class="sxs-lookup"><span data-stu-id="e37c5-169">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="e37c5-170">如果尚未通过应用初始迁移创建站点数据库，则会收到*处理请求时，数据库操作失败*错误。</span><span class="sxs-lookup"><span data-stu-id="e37c5-170">If the site database has not been created by applying the initial migration, you will get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="e37c5-171">点击**应用迁移**创建数据库，并刷新以忽略错误继续。</span><span class="sxs-lookup"><span data-stu-id="e37c5-171">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e37c5-172">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e37c5-172">Next steps</span></span>

* <span data-ttu-id="e37c5-173">本文介绍了您如何可以使用 Google 进行验证。</span><span class="sxs-lookup"><span data-stu-id="e37c5-173">This article showed how you can authenticate with Google.</span></span> <span data-ttu-id="e37c5-174">可以遵循类似的方法来使用上列出其他提供程序进行身份验证[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="e37c5-174">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="e37c5-175">一旦您将您的网站发布到 Azure web 应用时，应重置`ClientSecret`在 Google API 控制台中。</span><span class="sxs-lookup"><span data-stu-id="e37c5-175">Once you publish your web site to Azure web app, you should reset the `ClientSecret` in the Google API Console.</span></span>

* <span data-ttu-id="e37c5-176">设置`Authentication:Google:ClientId`和`Authentication:Google:ClientSecret`作为在 Azure 门户中的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="e37c5-176">Set the `Authentication:Google:ClientId` and `Authentication:Google:ClientSecret` as application settings in the Azure portal.</span></span> <span data-ttu-id="e37c5-177">配置系统设置以从环境变量读取密钥。</span><span class="sxs-lookup"><span data-stu-id="e37c5-177">The configuration system is set up to read keys from environment variables.</span></span>
