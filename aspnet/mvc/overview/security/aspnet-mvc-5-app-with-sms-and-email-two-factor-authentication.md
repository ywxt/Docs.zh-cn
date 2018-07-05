---
uid: mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
title: 使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用程序 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何生成使用双因素身份验证的 ASP.NET MVC 5 web 应用。 应完成与创建安全的 ASP.NET MVC 5 web 应用...
ms.author: aspnetcontent
ms.date: 08/20/2015
ms.assetid: f50a5cdb-c06a-46ed-aa14-fc5b049dc8dc
msc.legacyurl: /mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 4fd0091effcf2cc0517da91922981e49ef0eef5a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803202"
---
<a name="aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication"></a>使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用程序
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程演示如何生成使用双因素身份验证的 ASP.NET MVC 5 web 应用。 应完成[安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)继续操作之前。 你可以下载已完成的应用程序[此处](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952)。 下载内容包含调试帮助程序，使你可以测试电子邮件确认和短信，而无需设置电子邮件或 SMS 提供程序。
> 
> 本教程由编写[Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。


- [创建 ASP.NET MVC 应用](#createMvc)
- [为 SMS 设置双因素身份验证](#SMS)
- [启用双因素身份验证](#enable2)
- [其他资源](#addRes)

<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a>创建 ASP.NET MVC 应用

首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本。

> [!NOTE]
> 警告： 您应完成[安全的 ASP.NET MVC 5 web 应用程序创建具有登录、 电子邮件确认及密码重置](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)继续操作之前。 必须安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本，若要完成本教程。


1. 创建新的 ASP.NET Web 项目并选择 MVC 模板。 Web 窗体还支持 ASP.NET 标识，因此无法执行类似的步骤，在 web 窗体应用中。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image1.png)
2. 将保留为默认的身份验证**单个用户帐户**。 如果你想要托管该应用程序在 Azure 中的，将选中该复选框。 稍后在本教程中我们将部署到 Azure。 你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
3. 设置[项目，以使用 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

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
  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image2.png)  
  
   地址:  
    `https://webservice.aspsms.com/aspsmsx2.asmx?WSDL`  
  
   命名空间:  
    `ASPSMSX2`
3. **找出 SMS 提供程序用户凭据**  
  
   Twilio:  
   从**仪表板**选项卡上的 Twilio 帐户，复制**帐户 SID**并**身份验证令牌**。  
  
   ASPSMS:  
   在帐户设置中，导航到**Userkey**并将其复制以及自定义**密码**。  
  
   我们将更高版本存储中的这些值*web.config*文件内键`"SMSAccountIdentification"`和`"SMSAccountPassword"`。
4. **指定 SenderID / 原始发件人**  
  
   Twilio:  
   从**数字**选项卡上，复制你的 Twilio 电话号码。  
  
   ASPSMS:  
   内**解锁原始发件人**菜单中，解锁始发者的一个或多个，或选择字母数字发信方 （不支持的所有网络）。  
  
   我们将更高版本存储中的此值*web.config*项中的文件`"SMSAccountFrom"`。
5. **将 SMS 提供程序凭据传输到应用**  
  
   提供的凭据和发件人的电话号码向应用程序。 为了简单起见，我们将存储在这些值*web.config*文件。 当我们将部署到 Azure 时，我们可以存储值安全地在**应用设置**web 站点上的部分配置选项卡。 

    [!code-xml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample1.xml?highlight=8-10)]

    > [!WARNING]
    > 安全性-永远不会存储在源代码中敏感数据。 帐户和凭据添加到上面的代码以使示例保持简单。 请参阅[的密码和其他敏感数据部署到 ASP.NET 和 Azure 最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
6. **数据传输到 SMS 提供程序的实现**  
  
   配置`SmsService`类中*应用程序\_Start\IdentityConfig.cs*文件。  
  
   具体取决于使用 SMS 提供程序激活任一**Twilio**或**ASPSMS**部分： 

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample2.cs)]
7. 更新*Views\Manage\Index.cshtml* Razor 视图: (注意： 不只是在现有代码中删除注释，请使用下面的代码。)  

    [!code-cshtml[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample3.cshtml?highlight=29-66)]
8. 验证是否`EnableTwoFactorAuthentication`并`DisableTwoFactorAuthentication`中的操作方法`ManageController`有[[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.118).aspx)属性：  

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample4.cs?highlight=3,16)]
9. 运行应用并使用之前注册的帐户登录。
10. 单击你的用户 ID，这便激活`Index`中的操作方法`Manage`控制器。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image3.png)
11. 单击添加。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image4.png)
12. `AddPhoneNumber`操作方法显示一个对话框，输入可接收短信的电话号码。

    [!code-csharp[Main](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/samples/sample5.cs)]

    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image5.png)
13. 在几秒钟后将获得使用验证码的短信。 输入它，然后按**提交**。  
    ![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image6.png)
14. 管理视图显示已添加你的电话号码。

<a id="enable2"></a>
## <a name="enable-two-factor-authentication"></a>启用双因素身份验证

在模板生成应用程序中，您需要使用 UI 启用双因素身份验证 (2FA)。 若要启用 2FA，请单击你在导航栏中的用户 ID （电子邮件别名）。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image7.png)

单击启用 2FA。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image8.png)

注销，然后重新登录。 如果已启用电子邮件 (请参阅我[前一篇教程](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md))，可以选择短信或 2FA 的电子邮件。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image9.png)

将显示验证代码页，其中 （从短信或电子邮件） 输入代码。

![](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication/_static/image10.png)

单击**记住此浏览器**复选框将免除你无需使用 2FA 登录时使用的浏览器和设备，你选中的复选框。 只要恶意用户无法访问你的设备，启用 2FA，并单击**记住此浏览器**将为您提供方便的一次性密码访问权限，同时还可以保留的所有访问的强 2FA 保护从非受信任的设备。 可以在您经常使用任何专用设备上执行此操作。

本教程提供了启用 2FA 上新的 ASP.NET MVC 应用程序的快速简介。 我的教程[双因素身份验证使用 SMS 和电子邮件与 ASP.NET 标识](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)进入代码隐藏示例中的详细信息。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [使用 SMS 和电子邮件与 ASP.NET 标识的双因素身份验证](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)进入双因素身份验证的详细信息
- [ASP.NET 标识的链接的推荐资源](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)进入密码恢复和帐户确认的详细信息。
- [MVC 5 应用程序使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程演示如何编写 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth 2 授权。 它还演示如何将其他数据添加到标识数据库。
- [使用成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Azure Web](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 本教程将添加 Azure 部署中，如何保护使用角色，对应用程序如何使用成员资格 API 来添加用户和角色，以及其他安全功能。
- [为 OAuth 2 中创建的 Google 应用程序和应用程序连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [在 Facebook 中创建应用并将应用程序连接到项目](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [设置项目中的 SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
