---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET Web 中的外部网站登录页 (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何登录到你使用 Facebook、 Google、 Twitter、 Yahoo 和其他站点的 ASP.NET Web Pages (Razor) 站点，即如何支持...
ms.author: aspnetcontent
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: e6c5b578b4c74fd04136d31751d51b59ba9197ba
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825432"
---
<a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET Web Pages (Razor) 站点中使用外部站点中的日志记录
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何登录到你使用 Facebook、 Google、 Twitter、 Yahoo 和其他站点的 ASP.NET Web Pages (Razor) 站点 — 即，如何在你的站点中支持 OAuth 和 OpenID。
> 
> 你将学习：
> 
> - 如何使用 WebMatrix 入门网站模板时启用从其他站点的登录名。
> 
> 这是引入一文中的 ASP.NET 功能：
> 
> - `OAuthWebSecurity`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 3

ASP.NET 网页包含对支持[OAuth](http://oauth.net/)并[OpenID](http://openid.net/)提供程序。 使用这些提供程序，可让你使用 Facebook、 Twitter、 Microsoft 和 Google 从其现有凭据的站点到用户登录。 例如，若要使用 Facebook 帐户登录，用户可以只需选择 Facebook 图标，将它们重定向到它们在其中输入他们的用户信息的 Facebook 登录页。 它们然后可以将 Facebook 登录你的站点上与其帐户相关联。 Web Pages 成员资格功能相关的增强功能是使用你的网站上的单个帐户，用户可以将多个登录名 （包括登录名从社交网站） 相关联。

下图显示了从登录页面**入门网站**模板，用户可以在其中选择一个 Facebook、 Twitter、 Google 或 Microsoft 图标，以启用日志记录使用的外部帐户：

![外部提供程序](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

可以通过取消注释几行代码中启用 OAuth 和 OpenID 的成员身份**入门网站**模板。 您使用的方法和属性以使用 OAuth 和 OpenID 提供程序位于`WebMatrix.Security.OAuthWebSecurity`类。 **入门网站**模板包括完整的成员身份基础结构，需要让用户登录到你使用本地凭据或来自另一个站点的站点登录页、 成员资格数据库，与所有的代码完成.

本部分举例说明如何让用户登录从外部站点到站点基于**入门网站**模板。 在创建后入门网站，你执行操作 （详细信息按照）：

- 使用 OAuth 提供程序 （Facebook、 Twitter 和 Microsoft） 的站点，外部站点上创建应用程序。 这样，您将需要为了调用这些站点的登录功能的应用程序密钥。
- 对于使用 OpenID 提供程序 (Google) 的站点，不需要创建应用程序。 对于所有这些站点，必须具有一个帐户，以便在中记录并创建开发人员应用程序。

    > [!NOTE]
    > Microsoft 应用程序仅接受工作网站的实时 URL，因此不能用于本地网站 URL 测试登录名。
- 编辑你的网站中的几个文件以指定适当的身份验证提供程序，并将提交到想要使用的站点的登录名。

本文提供了单独的指令的以下任务：

- [启用 Google 登录名](#To_enable_Google_logins)
- [启用 Facebook 登录名](#To_enable_Facebook_logins)
- [启用 Twitter 登录名](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>启用 Google 登录名

1. 创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。
2. 打开 *\_AppStart.cshtml*页上，并取消注释以下代码行。 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>测试 Google 登录

1. 运行*default.cshtml*您的网站上，然后选择**登录**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Google**或者**Yahoo**提交按钮。 此示例使用 Google 登录名。 

    Web 页面将请求重定向到 Google 登录页。

    ![Google 登录](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 输入现有 Google 帐户凭据。
4. 如果出现要求你是否想要允许 Google *Localhost*若要使用帐户中的信息，请单击**允许**。

    代码使用 Google 的令牌对用户进行身份验证，然后返回到此页上你的网站。 此页，可以将其 Google 登录名与你的网站上的现有帐户相关联的用户或用户可以在注册你将使用的外部登录名相关联的站点上的新帐户。

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. 选择**相关联**按钮。 在浏览器返回到应用程序的主页。

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>启用 Facebook 登录名

1. 转到[Facebook 开发人员站点](https://developers.facebook.com/apps)（如果尚未登录，则日志）。
2. 选择**创建新应用**按钮，然后按照提示进行命名和创建新的应用程序。
3. 在部分**选择如何将您的应用程序与 Facebook**，选择**网站**部分。
4. 填写**站点 URL**字段与你的站点的 URL (例如， `http://www.example.com`)。 **域**字段是可选的; 可以使用此提供对整个域的身份验证 (如*example.com*)。 

    > [!NOTE]
    > 如果你使用 URL 在本地计算机上运行站点喜欢`http://localhost:12345`（其中数是本地端口号），可以添加此值设置为**站点 URL**字段用于测试你的站点。 但是，任何时候，只要你的本地站点更改的端口号，你将需要更新**站点 URL**字段的应用程序。
5. 选择**保存更改**按钮。
6. 选择**应用**同样，选项卡，然后查看你的应用程序的起始页。
7. 复制**应用程序 ID**并**应用程序密码**为应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Facebook 提供程序。
8. 退出 Facebook 开发人员网站。

现在您更改两个页面中你的网站，以便用户将能够登录到网站使用其 Facebook 帐户。

1. 创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。
2. 打开 *\_AppStart.cshtml*页上，并取消注释的代码，为 Facebook OAuth 提供程序。 取消注释的代码块如以下所示： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. 复制**应用程序 ID**从 Facebook 应用程序的值作为值`appId`参数 （在引号内）。
4. 复制**应用程序机密**从 Facebook 应用程序作为值`appSecret`参数值。
5. 保存并关闭文件。

### <a name="testing-facebook-login"></a>测试 Facebook 登录

1. 运行该站点*default.cshtml*页上，然后选择**登录名**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Facebook**图标。 

    Web 页面将请求重定向到 Facebook 登录页。

    ![oauth 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. 登录到 Facebook 帐户。 

    代码使用 Facebook 令牌进行身份验证，然后返回到页您可以在其中将 Facebook 登录名与站点的登录名相关联。 你的用户名称或电子邮件地址填充到**电子邮件**字段在窗体上。

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. 选择**相关联**按钮。 

    在浏览器返回到主页并登录。

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>启用 Twitter 登录名

1. 浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。
2. 选择**创建应用**链接，然后登录到网站。
3. 上**创建的应用程序**窗体中，填写**名称**并**说明**字段。
4. 在中**网站**字段中，输入你的站点的 URL (例如， `http://www.example.com`)。 

    > [!NOTE]
    > 如果您要测试你的本地站点 (使用类似`http://localhost:12345`)，Twitter 可能不接受 URL。 但是，您可能能够使用本地环回 IP 地址 (例如`http://127.0.0.1:12345`)。 这将简化测试本地应用程序的过程。 但是，每次你的本地网站的端口号更改，你将需要更新**网站**字段的应用程序。
5. 在中**回叫 URL**字段中，输入你希望用户在登录后到 Twitter 到返回的网站中的页面的 URL。 例如，若要向用户发送到入门网站 （它将识别其登录的状态） 的主页上，输入中输入的同一个 URL**网站**字段。
6. 接受条款，然后选择**创建 Twitter 应用程序**按钮。
7. 上**我的应用程序**登陆页上，选择你创建的应用程序。
8. 上**详细信息**选项卡上，滚动到底部并选择**创建我的访问令牌**按钮。
9. 上**详细信息**选项卡上，复制**使用者密钥**并**使用者机密**为应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Twitter 提供程序。
10. 退出 Twitter 网站。

现在您更改两个页面中你的网站，以便用户能够登录到使用 Twitter 帐户的站点。

1. 创建或打开 WebMatrix 入门网站模板为基础的 ASP.NET Web Pages 站点。
2. 打开 *\_AppStart.cshtml*页面和 Twitter OAuth 提供程序取消注释的代码。 取消注释的代码块如下所示： 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. 复制**使用者密钥**从 Twitter 应用程序的值作为值`consumerKey`参数 （在引号内）。
4. 复制**使用者机密**从 Twitter 应用程序的值作为值`consumerSecret`参数。
5. 保存并关闭文件。

### <a name="testing-twitter-login"></a>测试 Twitter 登录

1. 运行*default.cshtml*您的网站上，然后选择**登录名**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Twitter**图标。 

    Web 页面将请求重定向到 Twitter 登录页面为您创建的应用程序。

    ![oauth 4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. 登录到 Twitter 帐户。
4. 代码使用 Twitter 令牌进行身份验证用户，然后返回到页你可以将关联您使用您网站的帐户的登录名。 名称或电子邮件地址填充到**电子邮件**字段在窗体上。

    ![oauth 5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. 选择**相关联**按钮。 

    在浏览器返回到主页并登录。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源


- [自定义站点范围内的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [将安全性和成员身份添加到 ASP.NET Web Pages 站点](https://go.microsoft.com/fwlink/?LinkID=202904)
