---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: 创建 MVC 5 应用程序与 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何构建 ASP.NET MVC 5 web 应用程序，使用户能够使用 OAuth 2.0 和外部身份验证的凭据...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 330cb290668ae951e822b95990ed92100b790cd5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833723"
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>创建 ASP.NET MVC 5 应用程序使用 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录 (C#)
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程演示如何生成使用 ASP.NET MVC 5 web 应用程序，使用户能够登录[OAuth 2.0](http://oauth.net/2/)使用 Facebook、 Twitter、 LinkedIn、 Microsoft 或 Google 之类的外部身份验证提供程序的凭据。 为简单起见，本教程重点介绍使用 Facebook 和 Google 凭据。
> 
> 启用这些凭据在您的网站中提供一个明显的优势，因为数以百万计的用户已获得与这些外部提供商的帐户。 这些用户可能更倾向于注册为您的网站，如果它们不需要创建和记住一组新的凭据。
> 
> 另请参阅[使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。
> 
> 本教程还介绍如何添加配置文件数据的用户，以及如何使用成员资格 API 添加角色。 本教程由编写[Rick Anderson](https://blogs.msdn.com/rickAndy) (请在 Twitter 上关注我： [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。


<a id="start"></a>
## <a name="getting-started"></a>入门

首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。 有关 Dropbox、 GitHub、 Linkedin、 Instagram、 缓冲区、 Salesforce、 流、 Stack Exchange、 Tripit、 Twitch、 Twitter、 yahoo ！ 和的详细信息的帮助，请参阅此[示例项目](https://github.com/matthewdunsdon/oauthforaspnet)。

> [!NOTE]
> 必须安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本使用 Google OAuth 2 和本地调试而无需 SSL 警告。


单击**新的项目**从**启动**页上，或者可以使用菜单并选择**文件**，然后**新项目**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a>创建第一个应用程序

单击**新的项目**，然后选择**Visual C#** 在左侧，然后**Web** ，然后选择**ASP.NET Web 应用程序**。 "MvcAuth"将项目命名，然后单击**确定**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

在中**新建 ASP.NET 项目**对话框中，单击**MVC**。 如果身份验证不是**单个用户帐户**，单击**更改身份验证**按钮，然后选择**单个用户帐户**。 通过检查**在云中托管**，应用将为非常轻松地在 Azure 中托管。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

如果所选**在云中托管**，完成配置对话框中。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>使用 NuGet 更新到最新的 OWIN 中间件

使用 NuGet 包管理器更新[OWIN 中间件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。 选择**更新**在左侧菜单中。 你可以单击**全部更新**按钮也可以搜索仅 OWIN 包 （下一步图中所示）：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

在下图显示仅 OWIN 包：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

从包管理器控制台 (PMC) 中，您可以输入`Update-Package`命令，将更新所有包。

按**F5**或**Ctrl + F5**运行该应用程序。 下图中的端口号是 1234年。 当您运行该应用程序时，您将看到不同的端口号。

具体取决于浏览器窗口的大小，可能需要单击导航图标以查看**主页**，**有关**，**联系人**，**注册**并**登录**链接。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>设置项目中的 SSL

若要连接到 Google 和 Facebook 身份验证提供程序，您需要设置为使用 SSL 的 IIS Express。 务必要在登录后使用 SSL 来保留和未退回到 HTTP，登录 cookie 是只需为机密作为用户名和密码，也无需使用的 SSL 要通过网络以明文发送它。 此外，您已经完成了执行握手和安全通道 （这是使 HTTPS 慢于 HTTP 的大容量） 的时间运行 MVC 管道之前，因此重定向回 HTTP 在登录后不会带来的当前请求或未来请求要快得多。

1. 在中**解决方案资源管理器**，单击**MvcAuth**项目。
2. 按 F4 键显示项目属性。 或者，从**视图**可以选择的菜单**属性窗口**。
3. 更改**已启用 SSL**为 True。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. 复制 SSL URL (这将是`https://localhost:44300/`除非你已创建其他 SSL 项目)。
5. 在中**解决方案资源管理器**，右键单击**MvcAuth**项目，然后选择**属性**。
6. 选择**Web**选项卡，然后粘贴到 SSL URL**项目 Url**框。 保存文件 (Ctl + S)。 将需要此 URL 来配置 Facebook 和 Google 身份验证应用。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 添加[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性为`Home`控制器需要的所有请求必须使用 HTTPS。 更安全的方法是将添加[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)筛选器添加到应用程序。 请参阅的部分&quot;保护应用程序使用 SSL 和 Authorize 属性&quot;中我 tutoral[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 下面显示了主控制器的一部分。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. 按 Ctrl+F5 运行应用程序。 如果在过去，在已安装了证书，可以跳过本部分的其余部分并跳转到[OAuth 2 中创建的 Google 应用程序和应用连接到该项目](#goog)，否则，请按照说明信任自签名IIS Express 已生成的证书。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 读取**安全警告**对话框，然后再单击**是**如果你想要安装表示本地主机的证书。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 会显示*主页*页上并不会出现 SSL 警告。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 也接受证书并将显示 HTTPS 内容而不发出警告。 Firefox 会使用其自己的证书存储，因此它将显示一条警告。 对于我们的应用程序，你可以安全地单击**我了解风险**。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>为 OAuth 2 中创建的 Google 应用程序和应用程序连接到项目

> [!WARNING]
> 当前的 Google OAuth 说明，请参阅[ASP.NET Core 中的配置 Google 身份验证](/aspnet/core/security/authentication/social/google-logins)。

1. 导航到[Google 开发人员控制台](https://console.developers.google.com/)。
2. 如果尚未创建的项目之前，请选择**凭据**在左侧选项卡，然后选择**创建**。
3. 在左侧选项卡中，单击**凭据**。
4. 单击**创建凭据**然后**OAuth 客户端 ID**。 

    1. 在中**创建客户端 ID**对话框中，保留默认**Web 应用程序**为应用程序类型。
    2. 设置**授权的 JavaScript**上面使用的 SSL url 的来源 (`https://localhost:44300/`除非你已创建其他 SSL 项目)
    3. 设置**已授权重定向 URI**到：  
         `https://localhost:44300/signin-google`
5. 单击 OAuth 许可屏幕菜单项，然后设置你的电子邮件地址和产品名称。 当您完成窗体中单击**保存**。
6. 单击库菜单项，搜索**Google + API**，单击它，然后按启用。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   下图显示了已启用的 Api。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. 从 Google Api API 管理器中，请访问**凭据**选项卡来获取**客户端 ID**。 若要使用应用程序机密保存 JSON 文件的下载。 复制并粘贴**ClientId**并**ClientSecret**到`UseGoogleAuthentication`方法中找到*Startup.Auth.cs*文件*App_Start*文件夹。 **ClientId**并**ClientSecret**如下所示的值是示例，它们不起作用。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 安全性-永远不会存储在源代码中敏感数据。 帐户和凭据添加到上面的代码以使示例保持简单。 请参阅[的密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
8. 按**CTRL + F5**生成并运行应用程序。 单击**登录**链接。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 下**使用其他服务进行登录**，单击**Google**。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 如果您错过任何上述步骤将获取 HTTP 401 错误。 重新检查上述步骤。 如果你缺少所需的设置 (例如**产品名称**)、 添加缺少的项，并保存; 可能需要几分钟时间验证才能工作。
10. 你将重定向到 Google 站点将在其中输入你的凭据。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 输入你的凭据后，您将会提示您刚创建的 web 应用程序对其授予权限：
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 单击**接受**。 你将立即重定向回**注册**MvcAuth 应用程序可以在其中注册你的 Google 帐户页。 可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但你通常想要保留的默认电子邮件别名 （即，一个用于身份验证）。 单击“注册”。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>在 Facebook 中创建应用并将应用程序连接到项目

> [!WARNING]
> 当前 Facebook OAuth2 身份验证说明，请参阅[配置 Facebook 身份验证](/aspnet/core/security/authentication/social/facebook-logins)


<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>检查成员身份数据

在中**视图**菜单上，单击**服务器资源管理器**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

展开**DefaultConnection (MvcAuth)**，展开**表**，右键单击**AspNetUsers**然后单击**显示表数据**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 表数据](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>将配置文件数据添加到用户类

在本部分中您将添加出生日期和家庭城镇对用户数据在注册期间，在下图中所示。

![使用家庭城镇和 Bday reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

打开*Models\IdentityModels.cs*文件，并添加出生日期和主页城镇属性：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

打开*Models\AccountViewModels.cs*文件和组出生日期和主页中的城镇属性`ExternalLoginConfirmationViewModel`。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

打开*Controllers\AccountController.cs*文件，并添加代码中的出生日期和主页城镇`ExternalLoginConfirmation`操作方法所示：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

添加出生日期和到主城镇*Views\Account\ExternalLoginConfirmation.cshtml*文件：

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

删除成员资格数据库，使您可以再次使用你的应用程序注册你的 Facebook 帐户并验证可以添加新的出生日期和家庭城镇配置文件信息。

从**解决方案资源管理器**，单击**显示所有文件**图标，然后右键单击*添加\_Data\aspnet-MvcAuth-&lt;日期戳&gt;.mdf*然后单击**删除**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**(PMC)。 在 PMC 中输入以下命令。

1. 启用迁移
2. 添加迁移 Init
3. 更新数据库

运行应用程序并使用 FaceBook 和 Google 登录并注册某些用户。

## <a name="examine-the-membership-data"></a>检查成员身份数据

在中**视图**菜单上，单击**服务器资源管理器**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

右键单击**AspNetUsers**然后单击**显示表数据**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown`和`BirthDate`字段如下所示。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>您的应用程序中注销并使用另一个帐户中的日志记录

如果使用 Facebook、 向应用登录，然后注销并尝试登录再次使用其他 Facebook 帐户 （使用的同一浏览器），你将立即登录到您使用的上一个 Facebook 帐户。 若要使用另一个帐户，需要导航到 Facebook，然后在 Facebook 上注销。 同一规则适用于任何其他第三方身份验证提供程序。 或者，您可以将另一个帐户登录使用不同的浏览器。

## <a name="next-steps"></a>后续步骤

请参阅[引入 owin Yahoo 和 LinkedIn OAuth 安全提供程序](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)通过 Jerrie Pelser 有关 Yahoo 和 LinkedIn 的说明。 请参阅 Jerrie 的美观社交登录按钮的 ASP.NET MVC 5，获取启用社交登录按钮。

请遵循我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)，它将继续本教程并显示以下：

1. 如何将应用部署到 Azure。
2. 如何保护应用程序与角色。
3. 如何保护应用程序与[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)并[Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)筛选器。
4. 如何使用成员资格 API 来添加用户和角色。

请在你喜欢本教程的内容，我们可以提高上留下反馈。 此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。 甚至可以请求并对要添加到 ASP.NET 的新功能进行投票。 例如，可以投票到工具[创建和管理用户和角色。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

有关 ASP.NET 外部身份验证服务的工作方式的很好的说明，请参阅 Robert McMurray[外部身份验证服务](https://asp.net/web-api/overview/security/external-authentication-services)。 Robert 的文章还介绍在启用 Microsoft 和 Twitter 身份验证的详细信息。 Tom Dykstra 的绝佳[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)演示如何使用实体框架。
