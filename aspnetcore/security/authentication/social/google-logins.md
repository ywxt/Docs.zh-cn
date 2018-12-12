---
title: 在 ASP.NET Core Google 外部登录安装程序
author: rick-anderson
description: 本教程演示的集成到现有的 ASP.NET Core 应用程序的 Google 帐户用户身份验证。
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 11/11/2018
uid: security/authentication/google-logins
ms.openlocfilehash: 372504eb4f6fea412b5b160e0d5e9251dafe0d56
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284481"
---
# <a name="google-external-login-setup-in-aspnet-core"></a>在 ASP.NET Core Google 外部登录安装程序

作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

本教程演示如何使用户可以使用示例 ASP.NET Core 2.0 项目上创建其 Google + 帐户登录[上一页](xref:security/authentication/social/index)。 我们首先需要遵循[官方步骤](https://developers.google.com/identity/sign-in/web/devconsole-project)Google API 控制台中创建新的应用程序。

## <a name="create-the-app-in-google-api-console"></a>在 Google API 控制台中创建应用

* 导航到[ https://console.developers.google.com/projectselector/apis/library ](https://console.developers.google.com/projectselector/apis/library)并登录。 如果还没有 Google 帐户，使用**更多选项** > **[创建帐户](https://accounts.google.com/SignUpWithoutGmail?service=cloudconsole&continue=https%3A%2F%2Fconsole.developers.google.com%2Fprojectselector%2Fapis%2Flibrary&ltmpl=api)** 链接创建一个链接：

![Google API 控制台](index/_static/GoogleConsoleLogin.png)

* 将重定向到**API 管理器库**页：

![在 API 管理器库页上的登录](index/_static/GoogleConsoleSwitchboard.png)

* 点击**创建**并输入你**项目名称**:

![“新建项目”对话框](index/_static/GoogleConsoleNewProj.png)

* 接受对话框中，你将重定向回到库页允许您选择新应用的功能。 查找**Google + API**在列表中，单击其链接以添加 API 功能：

![在 API 管理器库页中搜索"Google + API"](index/_static/GoogleConsoleChooseApi.png)

* 显示新添加的 API 的页。 点击**启用**将 Google + 登录功能中添加到您的应用程序：

![API 管理器 Google + API 页上的登录](index/_static/GoogleConsoleEnableApi.png)

* 启用 API 后, 点击**创建凭据**若要配置的机密：

![在 API 管理器 Google + API 页上创建凭据按钮](index/_static/GoogleConsoleGoCredentials.png)

* 选择：
  * **Google + API**
  * **Web 服务器 (例如 node.js，Tomcat)**，和
  * **用户数据**:

![API 管理器凭据页：找出哪些类型的凭据，需要面板](index/_static/GoogleConsoleChooseCred.png)

* 点击**我需要什么凭据？** 转到应用配置，第二个步骤**创建 OAuth 2.0 客户端 ID**:

![API 管理器凭据页：创建 OAuth 2.0 客户端 ID](index/_static/GoogleConsoleCreateClient.png)

* 因为我们将 Google + 项目创建与只是一项功能 （登录），我们可以输入相同**名称**与我们的项目使用 OAuth 2.0 客户端 id。

* 输入你的开发 URI 与`/signin-google`追加到**已授权重定向 Uri**字段 (例如： `https://localhost:44320/signin-google`)。 本教程中稍后配置 Google 身份验证将自动处理在请求`/signin-google`路由实现 OAuth 流。

> [!NOTE]
> URI 段`/signin-google`设置为默认的 Google 身份验证提供程序的回调。 配置 Google 身份验证中间件通过继承时，可以更改默认的回调 URI [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath)的属性[GoogleOptions](/dotnet/api/microsoft.aspnetcore.authentication.google.googleoptions)类。

* 按 tab 键以添加**已授权重定向 Uri**条目。

* 点击**创建客户端 ID**，转到第三个步骤中，其中**设置 OAuth 2.0 许可屏幕**:

![API 管理器凭据页：设置 OAuth 2.0 许可屏幕](index/_static/GoogleConsoleAddCred.png)

* 输入你的公众**电子邮件地址**并**产品名称**Google + 提示用户登录时为你的应用所示。 其他选项都位于**更多自定义选项**。

* 点击**继续**继续到最后一个步骤中，**下载凭据**:

![API 管理器凭据页：下载凭据](index/_static/GoogleConsoleFinish.png)

* 点击**下载**若要使用应用程序机密保存 JSON 文件并**完成**以完成创建新的应用。

* 部署站点时将需要重新访问**Google Console**并注册新的公共 url。

## <a name="store-google-clientid-and-clientsecret"></a>应用商店 Google ClientID 和 ClientSecret

链接敏感设置，例如 Google`Client ID`并`Client Secret`到应用程序的配置使用[机密管理器](xref:security/app-secrets)。 对于本教程的目的，命名为令牌`Authentication:Google:ClientId`和`Authentication:Google:ClientSecret`。

可以在下一步中下载的 JSON 文件中找到这些令牌的值`web.client_id`和`web.client_secret`。

## <a name="configure-google-authentication"></a>配置 Google 身份验证

::: moniker range=">= aspnetcore-2.0"

将 Google 服务中的添加`ConfigureServices`中的方法*Startup.cs*文件：

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

在本教程中使用的项目模板可确保[Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google)安装包。

* 若要使用 Visual Studio 2017 中安装此包，请右键单击项目并选择**管理 NuGet 包**。
* 若要使用.NET Core CLI 安装，请在项目目录中执行以下命令：

`dotnet add package Microsoft.AspNetCore.Authentication.Google`

添加中的 Google 中间件`Configure`中的方法*Startup.cs*文件：

```csharp
app.UseGoogleAuthentication(new GoogleOptions()
{
    ClientId = Configuration["Authentication:Google:ClientId"],
    ClientSecret = Configuration["Authentication:Google:ClientSecret"]
});
```

::: moniker-end

请参阅[GoogleOptions](/dotnet/api/microsoft.aspnetcore.builder.googleoptions) Google 身份验证支持的配置选项的详细信息的 API 参考。 这可以用于请求有关用户的不同信息。

## <a name="sign-in-with-google"></a>使用 Google 登录

运行你的应用程序，然后单击**登录**。 若要使用 Google 登录的选项将显示：

![Microsoft Edge 中运行的 web 应用程序：用户未经过身份验证](index/_static/DoneGoogle.png)

当您单击 Google 时，你将重定向到 Google 进行身份验证：

![Google 身份验证对话框](index/_static/GoogleLogin.png)

后输入你的 Google 凭据，然后你将重定向回 web 站点，你可以设置你的电子邮件。

现在已在使用你的 Google 凭据进行登录：

![Microsoft Edge 中运行的 web 应用程序：用户通过身份验证](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a>疑难解答

* 如果你收到`403 (Forbidden)`从你自己的应用时，请确保在开发模式 （或中断到调试器中相同的错误） 中正在运行错误页**Google + API**中已启用**API 管理器库**按照列出的步骤[本页上早期](#create-the-app-in-google-api-console)。 如果在登录不起作用，并且如果没有收到任何错误，切换到开发模式，以使问题更易于调试。
* **ASP.NET Core 仅限 2.x:** 如果不通过调用配置标识`services.AddIdentity`中`ConfigureServices`，尝试进行身份验证将导致*ArgumentException:必须提供 SignInScheme 选项*。 在本教程中使用的项目模板可确保，此操作。
* 如果尚未通过应用初始迁移创建站点数据库，则会收到*处理请求时，数据库操作失败*错误。 点击**应用迁移**创建数据库，并刷新以忽略错误继续。

## <a name="next-steps"></a>后续步骤

* 本文介绍了您如何可以使用 Google 进行验证。 可以遵循类似的方法来使用上列出其他提供程序进行身份验证[上一页](xref:security/authentication/social/index)。

* 一旦您将您的网站发布到 Azure web 应用时，应重置`ClientSecret`在 Google API 控制台中。

* 设置`Authentication:Google:ClientId`和`Authentication:Google:ClientSecret`作为在 Azure 门户中的应用程序设置。 配置系统设置以从环境变量读取密钥。
