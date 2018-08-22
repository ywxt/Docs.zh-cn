---
uid: identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
title: 使用 SMS 和电子邮件与 ASP.NET 标识的双因素身份验证 |Microsoft Docs
author: HaoK
description: 本教程将演示如何设置双因素身份验证 (2FA) 使用 SMS 和电子邮件。 由 Rick Anderson 撰写本文时 ( @RickAndMSFT )、 Pr....
ms.author: riande
ms.date: 09/15/2015
ms.assetid: 053e23c4-13c9-40fa-87cb-3e9b0823b31e
msc.legacyurl: /identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 4454f011960f74c20ac590c3d034028cfc867e7d
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823557"
---
<a name="two-factor-authentication-using-sms-and-email-with-aspnet-identity"></a>使用 SMS 和电子邮件与 ASP.NET 标识的双因素身份验证
====================
通过[Hao 永远](https://github.com/HaoK)， [Pranav rastogi 撰写](https://github.com/rustd)， [Rick Anderson](https://github.com/Rick-Anderson)， [Suhas Joshi](https://github.com/suhasj)

> 本教程将演示如何设置双因素身份验证 (2FA) 使用 SMS 和电子邮件。
> 
> 由 Rick Anderson 撰写本文时 ([@RickAndMSFT](https://twitter.com/#!/RickAndMSFT))，Pranav rastogi 撰写 ([@rustd](https://twitter.com/rustd))，Hao 永远和 Suhas Joshi。 NuGet 示例主要由 Hao 永远编写。


本主题涵盖以下产品：

- [生成标识示例](#build)
- [为 SMS 设置双因素身份验证](#SMS)
- [启用双因素身份验证](#enable2)
- [如何注册的双因素身份验证提供程序](#reg)
- [合并的社交和本地登录帐户](#combine)
- [免受暴力攻击的帐户锁定](#lock)

<a id="build"></a>

## <a name="building-the-identity-sample"></a>生成标识示例

在本部分中，您将使用 NuGet 来下载我们将使用的示例。 首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。

> [!NOTE]
> 警告： 您必须安装 Visual Studio [2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)要完成本教程。


1. 创建一个新***空***ASP.NET Web 项目。
2. 在包管理器控制台中，输入以下内容的以下命令：  
  
    `Install-Package SendGrid`  
    `Install-Package -Prerelease Microsoft.AspNet.Identity.Samples`  
  
   在本教程中，我们将使用[SendGrid](http://sendgrid.com/)发送电子邮件并[Twilio](https://www.twilio.com/)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)的 sms 短。 `Identity.Samples`包将安装我们将使用的代码。
3. 设置[项目，以使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. *可选*： 请遵循我[电子邮件确认教程](account-confirmation-and-password-recovery-with-aspnet-identity.md)挂接 SendGrid 然后运行应用并注册的电子邮件帐户。
5. * 可选: * 删除中的示例演示电子邮件链接确认代码 (`ViewBag.Link`帐户控制器中的代码。 请参阅`DisplayEmail`和`ForgotPasswordConfirmation`操作方法和 razor 视图)。
6. <em>可选: * 中删除`ViewBag.Status`代码从管理和帐户控制器和 *Views\Account\VerifyCode.cshtml</em>并<em>Views\Manage\VerifyPhoneNumber.cshtml</em> razor 视图。 或者，可以保留`ViewBag.Status`显示效果以测试此应用本地而无需挂钩和发送电子邮件和短信的工作方式。

> [!NOTE]
> 警告： 如果在此示例中的安全设置的任何更改，生产应用程序将需要进行显式调用所做的更改的安全审核。


<a id="SMS"></a>

## <a name="set-up-sms-for-two-factor-authentication"></a>为 SMS 设置双因素身份验证

本教程提供了有关使用 Twilio 或 ASPSMS 的说明，但可以使用任何其他 SMS 提供程序。

1. **使用 SMS 提供程序创建用户帐户**  
  
   创建[Twilio](https://www.twilio.com/try-twilio)或[ASPSMS](https://www.aspsms.com/asp.net/identity/testcredits/)帐户。
2. **安装其他包或添加服务引用**  
  
   Twilio:  
   在包管理器控制台中，输入以下命令：  
    `Install-Package Twilio`  
  
   ASPSMS:  
   需要添加以下服务引用：  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image1.png)  
  
   地址:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空间:  
    `ASPSMSX2`
3. **找出 SMS 提供程序用户凭据**  
  
   Twilio:  
   从**仪表板**选项卡上的 Twilio 帐户，复制**帐户 SID**并**身份验证令牌**。  
  
   ASPSMS:  
   在帐户设置中，导航到**Userkey**并将其复制以及自定义**密码**。  
  
   我们稍后将这些值存储在变量`SMSAccountIdentification`和`SMSAccountPassword`。
4. **指定 SenderID / 原始发件人**  
  
   Twilio:  
   从**数字**选项卡上，复制你的 Twilio 电话号码。  
  
   ASPSMS:  
   内**解锁原始发件人**菜单中，解锁始发者的一个或多个，或选择字母数字发信方 （不支持的所有网络）。  
  
   更高版本，我们会将此值存储在变量中`SMSAccountFrom`。
5. **将 SMS 提供程序凭据传输到应用**  
  
   提供的凭据和发件人的电话号码向应用程序：

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample1.cs)]

    > [!WARNING]
    > 安全性-永远不会存储在源代码中敏感数据。 帐户和凭据添加到上面的代码以使示例保持简单。 请参阅 Jon 输入[ASP.NET MVC： 保留专用源代码管理设置带](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。
6. **数据传输到 SMS 提供程序的实现**  
  
   配置`SmsService`类中*应用程序\_Start\IdentityConfig.cs*文件。  
  
   具体取决于使用 SMS 提供程序激活任一**Twilio**或**ASPSMS**部分： 

    [!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample2.cs)]
7. 运行应用并使用之前注册的帐户登录。
8. 单击你的用户 ID，这便激活`Index`中的操作方法`Manage`控制器。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image2.png)
9. 单击添加。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image3.png)
10. 在几秒钟后将获得使用验证码的短信。 输入它，然后按**提交**。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image4.png)
11. 管理视图显示已添加你的电话号码。  
  
    ![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image5.png)

### <a name="examine-the-code"></a>检查代码

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample3.cs?highlight=2)]

`Index`中的操作方法`Manage`控制器设置根据上一操作的状态消息，并提供链接以更改您的本地密码或添加本地帐户。 `Index`方法还会显示状态或你 2FA 电话号码、 外部登录名、 2FA 启用，并请记住此浏览器 （稍后介绍） 的 2FA 方法。 单击你的标题栏中的用户 ID （电子邮件） 未通过一条消息。 单击**电话号码： 删除**链接传递`Message=RemovePhoneSuccess`作为查询字符串。  
  
`https://localhost:44300/Manage?Message=RemovePhoneSuccess`

[![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image6.png)]

`AddPhoneNumber`操作方法显示一个对话框，输入可接收短信的电话号码。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample4.cs)]

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image7.png)

单击**发送验证码**按钮将电话号码发送到 HTTP POST`AddPhoneNumber`操作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample5.cs?highlight=12)]

`GenerateChangePhoneNumberTokenAsync`方法将生成安全令牌都将设置中的 SMS 消息。 如果 SMS 服务已配置，作为字符串发送令牌&quot;你的安全代码是&lt;令牌&gt;&quot;。 `SmsService.SendAsync`方法调用以异步方式，然后应用重定向到`VerifyPhoneNumber`操作方法 （后者将显示以下对话框），您可以在其中输入验证码。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image8.png)

一旦您输入代码，然后单击提交，将代码发布到 HTTP POST`VerifyPhoneNumber`操作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample6.cs)]

`ChangePhoneNumberAsync`方法检查的已发布的安全代码。 如果代码正确无误，电话号码添加到`PhoneNumber`字段的`AspNetUsers`表。 如果该调用成功，`SignInAsync`调用方法：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample7.cs)]

`isPersistent`参数设置是否跨多个请求身份验证会话保持不变。

更改安全配置文件时，生成并存储在一个新的安全戳`SecurityStamp`字段*AspNetUsers*表。 请注意，`SecurityStamp`字段是不同的安全 cookie。 安全 cookie 不会存储在`AspNetUsers`表 （或标识 DB 中的其他任何位置）。 使用自签名安全 cookie 令牌[DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx)并使用创建`UserId, SecurityStamp`和过期时间信息。

Cookie 中间件将检查每个请求的 cookie。 `SecurityStampValidator`中的方法`Startup`类达到数据库，并定期检查安全戳指定的`validateInterval`。 除非您更改安全配置文件，这仅发生 （在本示例中） 每隔 30 分钟。 选择 30 分钟时间间隔内的目的是尽量减少对数据库的访问。

`SignInAsync`方法需要对安全配置文件进行任何更改时调用。 安全配置文件发生更改，数据库将更新`SecurityStamp`字段，然后无需调用`SignInAsync`方法会保持登录*仅*直到下一个 OWIN 管道的时间达到数据库 ( `validateInterval`). 您可以通过更改对此进行测试`SignInAsync`方法以立即返回，并设置 cookie`validateInterval`属性从 30 分钟内为 5 秒：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample8.cs?highlight=3)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample9.cs?highlight=20-21)]

使用上面的代码更改，可以更改安全配置文件 (例如，通过更改的状态**启用两个因素**)，你将注销 5 秒内时`SecurityStampValidator.OnValidateIdentity`方法失败。 删除中的返回行`SignInAsync`方法中，进行更改的另一个安全配置文件并将不记录。`SignInAsync`方法将生成一个新的安全 cookie。

<a id="enable2"></a>

## <a name="enable-two-factor-authentication"></a>启用双因素身份验证

在示例应用中，您需要使用 UI 启用双因素身份验证 (2FA)。 若要启用 2FA，请单击你在导航栏中的用户 ID （电子邮件别名）。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image9.png)  
单击启用 2FA。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image10.png) 注销，然后重新登录。 如果已启用电子邮件 (请参阅我[前一篇教程](account-confirmation-and-password-recovery-with-aspnet-identity.md))，可以选择短信或 2FA 的电子邮件。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image11.png) 将显示验证代码页，其中 （从短信或电子邮件） 输入代码。![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image12.png) 单击**记住此浏览器**复选框将免除你无需使用 2FA 登录使用该计算机和浏览器。 启用 2FA，并单击**记住此浏览器**将为您提供强 2FA 保护免受恶意用户尝试访问你的帐户，只要它们不能访问您的计算机。 您经常使用的任何专用计算机上，可以执行此操作。 通过设置**记住此浏览器**，请从计算机不经常使用的情况下，获取 2FA 提高的安全性，您可以方便地在无需在你自己的计算机上经过 2FA。 

<a id="reg"></a>
## <a name="how-to-register-a-two-factor-authentication-provider"></a>如何注册的双因素身份验证提供程序

创建一个新的 MVC 项目时*IdentityConfig.cs*文件包含注册的双因素身份验证提供程序的以下代码：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample10.cs?highlight=22-35)]

## <a name="add-a-phone-number-for-2fa"></a>添加用于 2FA 的电话号码

`AddPhoneNumber`中的操作方法`Manage`控制器生成安全令牌，并提供了发送到手机号。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample11.cs)]

发送令牌后，它将重定向到`VerifyPhoneNumber`操作方法，您可以在其中输入 2fa 注册短信的代码。 不使用 SMS 2FA，直到您已验证的电话号码。

## <a name="enabling-2fa"></a>启用 2FA

`EnableTFA`操作方法启用 2FA:

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample12.cs)]

请注意`SignInAsync`必须调用，因为启用 2FA 是对安全配置文件的更改。 启用 2FA 后，用户将需要使用 2FA 登录，使用 2FA 方法注册 （SMS 和电子邮件示例中的）。

您可以添加更多 2FA 提供程序，如 QR 代码生成器也可以编写自己的 (请参阅[使用 Google 身份验证器与 ASP.NET 标识](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/))。

> [!NOTE]
> 使用生成 2FA 代码[基于时间的一次性密码算法](http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)和代码的有效期为 6 分钟。 如果需要多个六分钟，输入代码时，你将收到无效的代码错误消息。


<a id="combine"></a>

## <a name="combine-social-and-local-login-accounts"></a>合并的社交和本地登录帐户

您可以通过单击电子邮件链接组合本地和社交帐户。 按以下顺序&quot; RickAndMSFT@gmail.com &quot;首次创建为本地登录名，但可以作为第一个，一个社交登录创建帐户，然后添加本地登录名。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image13.png)

单击**管理**链接。 请注意与此帐户关联的 0 外部 （社交登录名）。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image14.png)

单击服务中的另一个日志的链接，接受应用程序请求。 已合并两个帐户，你将能够使用任一帐户登录。 可能希望用户在身份验证服务中的其社交日志已关闭，或已为其社交帐户失去访问更有可能的情况下添加本地帐户。

在下图中，Tom 是社交登录 (其中可以看到从**外部登录名： 1**的页上显示)。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image15.png)

单击**选取一个密码**允许你上添加本地日志使用相同的帐户相关联。

![](two-factor-authentication-using-sms-and-email-with-aspnet-identity/_static/image16.png)

<a id="lock"></a>

## <a name="account-lockout-from-brute-force-attacks"></a>免受暴力攻击的帐户锁定

可以通过启用用户锁定字典式攻击中的应用上保护帐户。 下面的代码中`ApplicationUserManager Create`方法可配置锁定：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample13.cs)]

上面的代码允许进行双因素身份验证的锁定。 尽管可以通过更改启用锁定登录名`shouldLockout`为 true`Login`在 account 控制器的方法，我们建议您不能启用锁定登录名，因为它使帐户遭受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)登录名攻击。 在示例代码中，为管理员帐户中创建禁用锁定`ApplicationDbInitializer Seed`方法：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample14.cs?highlight=19)]

## <a name="requiring-a-user-to-have-a-validated-email-account"></a>要求用户具有验证电子邮件帐户

下面的代码要求用户可以在登录前具有验证电子邮件帐户：

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample15.cs?highlight=8-17)]

## <a name="how-signinmanager-checks-for-2fa-requirement"></a>SignInManager 如何检查 2FA 要求

在本地日志和检查，以查看是否已启用 2FA 的社交登录上。 如果启用 2FA，则`SignInManager`登录方法返回`SignInStatus.RequiresVerification`，并将用户重定向到`SendCode`操作方法，它们将需要输入用于完成日志序列中的代码。 如果用户有 RememberMe 设置上的用户本地 cookie`SignInManager`将返回`SignInStatus.Success`，它们不需要经历 2FA。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample16.cs?highlight=20-22)]

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample17.cs?highlight=10-11,17-18)]

下面的代码演示`SendCode`操作方法。 一个[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)与为用户启用所有 2FA 方法创建。 [SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx)传递给[DropDownListFor](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist.aspx)帮助程序，这样用户就可以选择使用 2FA 方法 （通常电子邮件和短信）。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample18.cs)]

用户发送 2FA 方法，一旦`HTTP POST SendCode`调用操作方法时， `SignInManager` 2FA 代码和用户将重定向到的发送`VerifyCode`可在其中输入代码以完成的日志中的操作方法。

[!code-csharp[Main](two-factor-authentication-using-sms-and-email-with-aspnet-identity/samples/sample19.cs?highlight=3,13-14,18)]

## <a name="2fa-lockout"></a>2FA 锁定

尽管您可以设置帐户锁定登录名的密码尝试失败，这种方法使您的登录名到易受[DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack)锁定。 我们建议仅使用 2FA 使用帐户锁定。 当`ApplicationUserManager`是创建的示例代码设置 2FA 锁定和`MaxFailedAccessAttemptsBeforeLockout`五个。 后 （通过本地帐户或社交帐户） 在用户登录后，存储 2FA 在每次失败的尝试，并且如果达到最大尝试次数，锁定该用户是 5 分钟 (您可以设置时间与锁定`DefaultAccountLockoutTimeSpan`)。

<a id="addRes"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET 标识建议的资源](../getting-started/aspnet-identity-recommended-resources.md)因此链接标识的博客、 视频、 教程和很好的完整列表。
- [MVC 5 应用程序使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)还演示如何将配置文件信息添加到用户表。
- [ASP.NET MVC 和标识 2.0： 了解基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)通过 John 输入。
- [帐户确认和密码恢复与 ASP.NET 标识](account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET 标识简介](../getting-started/introduction-to-aspnet-identity.md)
- [宣布推出 RTM 的 ASP.NET 标识 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) Pranav rastogi 撰写。
- [ASP.NET 标识 2.0： 设置在验证帐户和两个身份授权](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)通过 John 输入。
