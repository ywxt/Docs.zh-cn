---
title: ASP.NET Core 中的 Facebook、Google 和外部提供程序身份验证
author: rick-anderson
description: 本教程演示如何使用外部身份验证提供程序通过 OAuth 2.0 生成 ASP.NET Core 2.x 应用。
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/social/index
ms.openlocfilehash: 063d452fb6ab91b712ade7f7b7ed99823dbdc657
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098813"
---
# <a name="facebook-google-and-external-provider-authentication-in-aspnet-core"></a>ASP.NET Core 中的 Facebook、Google 和外部提供程序身份验证

作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

本教程演示如何生成 ASP.NET Core 2.x 应用，该应用可让用户使用外部身份验证提供程序提供的凭据通过 OAuth 2.0 登录。

以下几节中介绍了 [Facebook](xref:security/authentication/facebook-logins)、[Twitter](xref:security/authentication/twitter-logins)、[Google](xref:security/authentication/google-logins) 和 [Microsoft](xref:security/authentication/microsoft-logins) 提供程序。 第三方程序包中提供了其他提供程序，例如 [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) 和 [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers)。

![Facebook、Twitter、Google plus 和 Windows 的社交媒体图标](index/_static/social.png)

使用户能够使用其当前凭据登录对用户来说十分便利，并且这样做可以将管理登录进程许多复杂操作转移给第三方。 有关社交登录如何驱动流量和客户转换的示例，请参阅 [Facebook](https://www.facebook.com/unsupportedbrowser) 和 [Twitter](https://dev.twitter.com/resources/case-studies) 的案例分析。

## <a name="create-a-new-aspnet-core-project"></a>创建新的 ASP.NET Core 项目

* 在 Visual Studio 2017 中，从“开始”页创建新项目，或通过“文件”>“新建”>“项目”进行创建 >  > 。

* 选择“Visual C#” > “.NET Core”分类中提供的“ASP.NET Core Web 应用程序”模板：

![“新建项目”对话框](index/_static/new-project.png)

* 点击“Web 应用程序”，验证“身份验证”是否设置为“单个用户帐户”：

![“新建 Web 应用程序”对话框](index/_static/select-project.png)

注意:本教程适用于 ASP.NET Core 2.0 SDK 版本，可以在向导顶部选择此版本。

## <a name="apply-migrations"></a>应用迁移

* 运行应用并选择“登录”链接。
* 选择“以新用户身份注册”链接。
* 输入新帐户的电子邮件地址和密码，再选择“注册”。
* 按照说明操作来应用迁移。

## <a name="require-https"></a>要求使用 HTTPS

OAuth 2.0 需要使用 SSL/TLS 通过 HTTPS 协议进行身份验证。

使用 Web 应用程序或 Web API 项目模板以及 ASP.NET Core 2.1 或更高版本创建的项目会自动配置为启用 HTTPS。 如果在项目向导的“更改身份验证”对话框中选择“单个用户帐户”选项，应用会在安全默认终结点启动。

有关更多信息，请参见<xref:security/enforcing-ssl>。

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a>使用 SecretManager 存储登录提供程序分配的令牌

社交登录提供程序在注册过程中分配“应用程序 ID”和“应用程序机密”。 确切的令牌名称因提供程序而异。 这些令牌代表应用用来访问其 API 的凭据。 令牌构成“机密”，可利用[机密管理器](xref:security/app-secrets#secret-manager)将其链接到应用配置。 机密管理器是在配置文件（例如 appsettings.json）中存储令牌更安全替代方法。

> [!IMPORTANT]
> 机密管理器仅用于开发目的。 可使用 [Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)存储和保护 Azure 测试和生产机密。

按照[在 ASP.NET Core 中进行开发期间安全存储应用机密](xref:security/app-secrets)主题中的步骤进行操作，以便存储以下每个登录提供程序分配的令牌。

## <a name="setup-login-providers-required-by-your-application"></a>应用程序所需的安装登录提供程序

使用以下主题配置应用程序，以使用相应的提供程序：

* [Facebook](xref:security/authentication/facebook-logins) 相关说明
* [Twitter](xref:security/authentication/twitter-logins) 相关说明
* [Google](xref:security/authentication/google-logins) 相关说明
* [Microsoft](xref:security/authentication/microsoft-logins) 相关说明
* [其他提供程序](xref:security/authentication/otherlogins)相关说明

[!INCLUDE[](includes/chain-auth-providers.md)]

## <a name="optionally-set-password"></a>选择性地设置密码

使用外部登录提供程序注册，即表明还没有向应用注册密码。 这可让用户无需创建和记住站点密码，但也会使用户依赖外部登录提供程序。 如果外部登录提供程序不可用，则无法登录网站。

使用外部提供程序在登录过程中设置的电子邮箱创建密码和登录：

* 点击右上角的“Hello &lt;电子邮件别名&gt;”链接，导航到“管理”视图。

![Web 应用程序“管理”视图](index/_static/pass1a.png)

* 点击“创建”

![“设置密码”页](index/_static/pass2a.png)

* 设置一个有效密码，可以用此密码和邮箱登录。

## <a name="next-steps"></a>后续步骤

* 本文介绍了外部身份验证，并说明了向 ASP.NET Core 应用添加外部登录所需的先决条件。

* 引用特定于提供程序的页，为应用所需的提供程序配置登录。

* 可能需要保留有关用户及其访问和刷新令牌的其他数据。 有关更多信息，请参见<xref:security/authentication/social/additional-claims>。
