---
uid: web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
title: 创建 ASP.NET Web 窗体应用程序具有 SMS 双因素身份验证 (C#) |Microsoft Docs
author: Erikre
description: 本教程演示如何生成带有双因素身份验证的 ASP.NET Web 窗体应用程序。 本教程旨在补充标题为 Cr 教程...
ms.author: aspnetcontent
ms.date: 10/09/2014
ms.assetid: 716264ae-ab72-45de-bfc5-53a6237089cf
msc.legacyurl: /web-forms/overview/security/create-an-aspnet-web-forms-app-with-sms-two-factor-authentication
msc.type: authoredcontent
ms.openlocfilehash: 16045b116ca5c797e7840f2ee5944e5f2c6282eb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803544"
---
<a name="create-an-aspnet-web-forms-app-with-sms-two-factor-authentication-c"></a>创建 ASP.NET Web 窗体应用程序具有 SMS 双因素身份验证 (C#)
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载电子邮件和 SMS 双因素身份验证的 ASP.NET Web 窗体应用](https://code.msdn.microsoft.com/ASPNET-Web-Forms-App-with-5a0ff94e)

> 本教程演示如何生成带有双因素身份验证的 ASP.NET Web 窗体应用程序。 本教程旨在补充标题为本教程[创建安全的 ASP.NET Web 窗体应用程序具有用户注册、 电子邮件确认及密码重置](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)。 此外，本教程基于 Rick Anderson [MVC 教程](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。


## <a name="introduction"></a>介绍

本教程将指导您完成创建支持双因素身份验证使用 Visual Studio 的 ASP.NET Web 窗体应用程序所需的步骤。 双因素身份验证是一个额外的用户身份验证步骤。 这个额外的步骤在登录期间生成的唯一个人标识号 (PIN)。 PIN 通常发送到电子邮件或短信的用户。 您的应用程序的用户在登录时，然后将 PIN 进入作为附加身份验证措施。

### <a name="tutorial-tasks-and-information"></a>教程任务和信息：

- [创建 ASP.NET Web 窗体应用](#createWebForms)
- [设置短信和双因素身份验证](#SMS)
- [启用双因素身份验证的已注册的用户](#use2FA)
- [其他资源](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>创建 ASP.NET Web 窗体应用

首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本以及。 此外，需要创建[Twilio](https://www.twilio.com/try-twilio)帐户，如下所述。

> [!NOTE]
> 重要说明： 必须安装[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本，若要完成本教程。


1. 创建新的项目 (**文件** - &gt; **新项目**)，然后选择**ASP.NET Web 应用程序**模板以及.NET Framework从版本 4.5.2**新的项目**对话框。
2. 从**新建 ASP.NET 项目**对话框中，选择**Web 窗体**模板。 将保留为默认的身份验证**单个用户帐户**。 然后，单击**确定**创建新项目。  
    ![新建 ASP.NET 项目对话框](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image1.png)
3. 为项目启用安全套接字层 (SSL)。 请按照步骤中提供**为项目启用 SSL**一部分[开始使用 Web 窗体的系列教程](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)。
4. 在 Visual Studio 中打开**程序包管理器控制台**(**工具** - &gt; **NuGet 程序包管理器** - &gt;**程序包管理器控制台**)，并输入以下命令：  
    `Install-Package Twilio`

<a id="SMS"></a>
## <a name="setup-sms-and-two-factor-authentication"></a>设置短信和双因素身份验证

本教程中使用 Twilio，但可以使用任何 SMS 提供程序。

1. 创建[Twilio](https://www.twilio.com/try-twilio)帐户。
2. 从**仪表板**选项卡上的 Twilio 帐户，复制**帐户 SID**和**身份验证令牌。** 你会将它们添加到您的应用程序更高版本。
3. 从**数字**选项卡上，复制你的 Twilio**电话号码**也。
4. Twilio 发起**帐户 SID**，**身份验证令牌**并**电话号码**应用可用的。 若要为简单起见将存储在这些值*web.config*文件。 在部署到 Azure 时，可以存储值安全地在**appSettings** web 站点上的部分配置选项卡。此外，在添加电话号码时，只能使用数字。   
   请注意，您还可以添加 SendGrid 凭据。 SendGrid 是一电子邮件通知的服务。 有关如何启用 SendGrid，有关详细信息，请参阅标题为本教程的挂钩向上 SendGrid 部分[创建安全的 ASP.NET Web 窗体应用程序具有用户注册、 电子邮件确认及密码重置。](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)

    [!code-xml[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample1.xml?highlight=2,6-10)]

    > [!WARNING]
    > 安全性-永远不会存储在源代码中敏感数据。 在此示例中，帐户和凭据存储在**appSettings**一部分*Web.config*文件。 在 Azure 上，您可以安全地存储这些值在**[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 门户中的选项卡。 有关相关信息，请参阅标题为 Rick Anderson 主题[的密码和其他敏感数据部署到 ASP.NET 和 Azure 最佳做法](https://go.microsoft.com/fwlink/?LinkId=513141)。
5. 配置`SmsService`类中*应用程序\_Start\IdentityConfig.cs*文件通过进行以下更改以黄色突出显示： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample2.cs?highlight=5-17)]
6. 添加以下`using`语句的开头*IdentityConfig.cs*文件： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample3.cs?highlight=1-4)]
7. 更新*Account/Manage.aspx*通过删除以黄色突出显示的行的文件：  

    [!code-aspx[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample4.aspx?highlight=38,53,57-60,63,66,70,73)]
8. 在中`Page_Load`处理程序*Manage.aspx.cs*代码隐藏，请取消注释代码使其显示为以黄色突出显示的行后面： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample5.cs?highlight=8)]
9. 中的代码隐藏*帐户*/*TwoFactorAuthenticationSignIn.aspx.cs*，更新`Page_Load`通过添加以下代码以黄色突出显示的处理程序： 

    [!code-csharp[Main](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/samples/sample6.cs?highlight=3-4,13)]

   通过使上面的代码更改，其中包含身份验证选项"提供程序"下拉列表将不重置为第一个值。 这样，用户已成功选择时进行身份验证，而不仅仅是第一个要使用的所有选项。
10. 在中**解决方案资源管理器**，右键单击*Default.aspx* ，然后选择**设为起始页**。
11. 通过测试您的应用程序，首先生成应用 (**Ctrl**+**Shift**+**B**)，然后运行该应用程序 (**F5**) 和请选择**注册**以创建新的用户帐户或选择**登录**如果已注册的用户帐户。
12. 后 （如用户） 登录，用户 ID （电子邮件地址） 中单击要显示的导航栏**管理帐户**页 (Manage.aspx)。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image2.png)
13. 单击**外**旁边**电话号码**上**管理帐户**页。  
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image3.png)
14. 添加您 （作为用户） 想要接收 SMS 消息 （文本消息），然后单击电话号码**提交**按钮。   
    ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image4.png)  
    此时，应用将使用中的凭据*Web.config*联系 Twilio。 将与用户帐户关联的移动电话发送短信 （短信）。 你可以验证 Twilio 消息发送通过查看 Twilio 仪表板。
15. 在几秒钟内，与用户帐户关联的手机会包含验证码的短信。 输入验证代码并按**提交**。  
     ![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image5.png)

<a id="use2FA"></a>
## <a name="enable-two-factor-authentication-for-a-registered-user"></a>启用双因素身份验证的已注册的用户

此时，已为你的应用启用双因素身份验证。 若要使用双因素身份验证的用户，他们可以只需更改其设置，请使用用户界面。 

1. 为您的应用程序的用户可以启用双因素身份验证为特定帐户通过单击用户 ID （电子邮件别名） 在导航栏中显示**管理帐户**页。然后，单击**启用**链接，以启用双因素身份验证的帐户。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image6.png)
2. 注销，然后重新登录。 如果已启用电子邮件，可以选择短信或电子邮件双因素身份验证。 如果尚未启用电子邮件，请参阅标题为教程[创建安全的 ASP.NET Web 窗体应用程序具有用户注册、 电子邮件确认和密码重置](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset.md)。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image7.png)
3. 将显示双因素身份验证页，其中 （从短信或电子邮件） 输入代码。![](create-an-aspnet-web-forms-app-with-sms-two-factor-authentication/_static/image8.png)  
 单击**记住此浏览器**复选框将免除你无需使用双因素身份验证登录时使用的浏览器和设备，你选中的复选框。 恶意用户无法访问你的设备，前提是启用双因素身份验证，并单击**记住此浏览器**将为您提供方便的一次性密码访问权限，同时仍保留强从非受信任的设备的所有访问的双因素身份验证保护。 可以在您经常使用任何专用设备上执行此操作。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [使用 SMS 和 ASP.NET 标识的双因素身份验证](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [ASP.NET 标识的链接的推荐资源](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [包含成员资格、 OAuth 和 SQL 数据库的安全的 ASP.NET Web 窗体应用部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web 窗体的教程系列-添加 OAuth 2.0 提供程序](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [ASP.NET Web 窗体教程系列的项目启用 SSL](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
- [帐户确认和密码恢复与 ASP.NET 标识](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [在 Facebook 中创建应用并将应用程序连接到项目](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
