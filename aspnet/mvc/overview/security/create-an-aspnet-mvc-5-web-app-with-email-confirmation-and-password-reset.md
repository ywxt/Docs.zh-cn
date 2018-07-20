---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: 安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何生成电子邮件确认和密码重置使用 ASP.NET 标识成员资格系统的 ASP.NET MVC 5 web 应用。 Ca...
ms.author: aspnetcontent
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 1387c3e9c03e011b610a070aa0c273ded23b463e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823542"
---
<a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a>安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置 (C#)
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程演示如何生成电子邮件确认和密码重置使用 ASP.NET 标识成员资格系统的 ASP.NET MVC 5 web 应用。 你可以下载已完成的应用程序[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。 下载内容包含调试帮助程序，使你可以测试电子邮件确认和短信，而无需设置电子邮件或 SMS 提供程序。
> 
> 本教程由编写[Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>创建 ASP.NET MVC 应用

首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

> [!NOTE]
> 警告： 您必须安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本，若要完成本教程。


1. 创建新的 ASP.NET Web 项目并选择 MVC 模板。 Web 窗体还支持 ASP.NET 标识，因此无法执行类似的步骤，在 web 窗体应用中。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. 将保留为默认的身份验证**单个用户帐户**。 如果你想要托管该应用程序在 Azure 中的，将选中该复选框。 稍后在本教程中我们将部署到 Azure。 你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 设置[项目，以使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 运行该应用程序中，单击**注册**链接并注册用户。 在此情况下，电子邮件的唯一验证是使用[[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)属性。
5. 在服务器资源管理器，导航到**数据 Connections\DefaultConnection\Tables\AspNetUsers**，右键单击并选择**打开表定义**。

    下图显示了`AspNetUsers`架构：

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. 右键单击**AspNetUsers**表，然后选择**显示表数据**。  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 此时该电子邮件尚未被确认。
7. 单击对应的行并选择删除。 将在下一步中，再次添加此电子邮件并发送确认电子邮件。

## <a name="email-confirmation"></a>电子邮件确认

它是最佳做法以确认新的用户注册，以验证它们不模拟其他人的电子邮件地址 （也就是说，他们尚未注册与其他人的电子邮件）。 假设你有讨论论坛，你会想要防止`"bob@example.com"`注册为`"joe@contoso.com"`。 而无需电子邮件确认`"joe@contoso.com"`无法收到您的应用程序不需要的电子邮件。 假设 Bob 意外注册为`"bib@example.com"`没有注意到，他将无法使用密码恢复，因为此应用没有其正确的电子邮件。 电子邮件确认从智能机器人提供有限的保护，并不会从确定垃圾邮件发送者提供保护，它们具有许多可用于注册的工作电子邮件别名。

你通常想要阻止新用户之前他们确认已通过电子邮件、 短信或另一种机制将发布到网站的任何数据。 <a id="build"></a>在以下部分中，我们将启用电子邮件确认，并修改代码以防止新注册的用户登录之前确认其电子邮件。

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>将挂接到 SendGrid

虽然本教程仅演示了如何添加通过电子邮件通知[SendGrid](http://sendgrid.com/)，可以发送电子邮件使用 SMTP 和其他机制 (请参阅[的其他资源](#addRes))。

1. 在包管理器控制台中，输入以下命令： 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. 转到[Azure SendGrid 注册页面](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409)并注册一个免费的 SendGrid 帐户。 通过添加类似于中的以下代码来配置 SendGrid *App_Start/IdentityConfig.cs*:

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

你将需要添加下列内容包括：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

若要使此示例简单明了，我们将存储中的应用设置*web.config*文件：

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> 安全性-永远不会存储在源代码中敏感数据。 AppSetting 中存储的帐户和凭据。 在 Azure 上，您可以安全地存储这些值在**[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。 请参阅[的密码和其他敏感数据部署到 ASP.NET 和 Azure 最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。


### <a name="enable-email-confirmation-in-the-account-controller"></a>启用帐户控制器中的电子邮件确认

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

验证是否*Views\Account\ConfirmEmail.cshtml*文件具有正确的 razor 语法。 (@ 字符在第一个行可能会丢失。 )

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

运行应用并单击注册链接。 一旦提交注册表单，你已登录。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

检查你的电子邮件帐户，并单击链接以确认你的电子邮件。

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>需要电子邮件确认之前登录

当前用户完成注册表单之后, 将它们记录。 你通常想要在中登录之前确认其电子邮件。 在下面的部分中，我们将修改要要求新用户在登录之前能够确认电子邮件 （通过身份验证） 的代码。 更新`HttpPost Register`有以下突出显示更改的方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

通过注释掉`SignInAsync`方法，用户将未进行签名在注册的。 `TempData["ViewBagLink"] = callbackUrl;`行可用于[调试应用程序](#dbg)并测试而不发送电子邮件的注册。 `ViewBag.Message` 用于显示的确认说明进行操作。 [下载示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)包含代码来测试电子邮件确认，而无需设置电子邮件，并且还可用于调试应用程序。

创建`Views\Shared\Info.cshtml`文件，并添加以下 razor 标记：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

添加[Authorize 属性](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx)到`Contact`主页控制器操作方法。 你可以单击**联系人**链接以验证匿名用户无权访问和身份验证的用户具有访问权限。

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

您还必须更新`HttpPost Login`操作方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

更新*Views\Shared\Error.cshtml*视图以显示错误消息：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

删除中的任何帐户**AspNetUsers**包含你想要测试的电子邮件别名的表。 运行应用并验证直到您已确认你的电子邮件地址不能登录。 一旦确认电子邮件地址，请单击**联系人**链接。

<a id="reset"></a>
## <a name="password-recoveryreset"></a>密码恢复/重置

删除注释字符从`HttpPost ForgotPassword`帐户控制器中的操作方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

删除中的注释字符`ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx)中*Views\Account\Login.cshtml* razor 视图文件：

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

登录页现在将显示用于重置密码的链接。

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>重新发送电子邮件确认链接

一旦用户创建新的本地帐户时，它们是电子邮件通知他们需要使用在登录之前确认链接。 如果用户意外删除的确认电子邮件，或者永远不会收到电子邮件，他们将需要再次发送的确认链接。 以下代码更改演示如何启用此功能。

将以下帮助器方法添加到底部*Controllers\AccountController.cs*文件：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

更新要使用新的帮助程序的注册方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

更新要重新发送密码，如果尚未被确认用户帐户的登录方法：

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a>合并的社交和本地登录帐户

您可以通过单击电子邮件链接组合本地和社交帐户。 按以下顺序**RickAndMSFT@gmail.com**首次创建为本地登录名，但可以作为第一个，一个社交登录创建帐户，然后添加本地登录名。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

单击**管理**链接。 请注意**外部登录名： 0**与此帐户关联。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

单击服务中的另一个日志的链接，接受应用程序请求。 已合并两个帐户，你将能够使用任一帐户登录。 可能希望用户在身份验证服务中的其社交日志已关闭，或已为其社交帐户失去访问更有可能的情况下添加本地帐户。

在下图中，Tom 是社交登录 (其中可以看到从**外部登录名： 1**的页上显示)。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

单击**选取一个密码**允许你上添加本地日志使用相同的帐户相关联。

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a>中更深入的电子邮件确认

我的教程[帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)将进入此主题具有更多详细信息。

<a id="dbg"></a>
## <a name="debugging-the-app"></a>调试应用

如果没有收到电子邮件包含的链接：

- 请检查垃圾邮件或垃圾邮件文件夹。
- 登录到你的 SendGrid 帐户，然后单击[电子邮件活动链接](https://sendgrid.com/logs/index)。

若要测试没有电子邮件验证链接，下载[已完成的示例](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。 将在页上显示的确认链接和确认代码。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [ASP.NET 标识的链接的推荐资源](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)进入密码恢复和帐户确认的详细信息。
- [MVC 5 应用程序使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程演示如何编写 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth 2 授权。 它还演示如何将其他数据添加到标识数据库。
- [将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教程将添加 Azure 部署中，如何保护使用角色，对应用程序如何使用成员资格 API 来添加用户和角色，以及其他安全功能。
- [为 OAuth 2 中创建的 Google 应用程序和应用程序连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中创建应用并将应用程序连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [设置项目中的 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
