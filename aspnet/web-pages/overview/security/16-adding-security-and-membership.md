---
uid: web-pages/overview/security/16-adding-security-and-membership
title: 将安全性和成员身份添加到 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本章展示如何保护你的网站，使某些页面能够仅向登录的人员。 （您还可以看到如何创建页 tha...
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: ae574706ecd14f1cafdb2d8b6340477e50246a32
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833275"
---
<a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>将安全性和成员身份添加到 ASP.NET Web Pages (Razor) 站点
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 此文章介绍了如何保护 ASP.NET Web Pages (Razor) 网站，以便仅供用户登录页面的一些。 （您还可以看到如何创建任何人都可以访问的页面。）
> 
> **你将学习：** 
> 
> - 如何创建了注册页，然后登录页，因此，对于某些页面可以限制对仅成员的访问的网站。
> - 如何创建公共和仅限成员的页。
> - 如何定义角色，即你的站点具有不同的安全权限的组以及如何将用户分配到角色。
> - 如何使用 CAPTCHA 阻止自动化的程序 （机器人） 创建帐户的成员。
>   
> 
> 下面是在本文中引入的 ASP.NET 功能：
> 
> - WebMatrix**入门网站**模板。
> - `WebSecurity`帮助器和`Roles`类。
> - `ReCaptcha`帮助器。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 2
> - WebMatrix 3
> - ASP.NET Web Helpers Library


您可以设置你的网站，以便用户可以登录到该&#8212;，即，以便站点支持*成员身份*。 这很有用的原因有很多。 例如，你的站点可能有应仅供成员使用的页。 在某些情况下，可能会要求用户进行登录以向你发送反馈或发表评论。

即使你的网站支持的成员身份，用户不是必需，若要登录，然后在站点上使用的一些页。 用户没有登录名为*匿名用户*。

用户可以注册你的网站上，并可以然后登录到该站点。 网站需要用户名 （电子邮件地址） 和密码以确认用户的身份属实。 中的日志记录并确认用户的标识的此过程称为*身份验证*。

您可以设置安全性和成员身份以不同的方式：

- 如果您使用的 WebMatrix 的简单方法是创建基于新站点作为**入门网站**模板。 此模板已配置用于安全和成员身份，并已注册页中，登录页上，依次类推。

    由模板创建站点还拥有一个选项可让用户使用 Facebook、 Google 等外部站点登录或 Twitter。
- 如果你想要将安全添加到现有站点，或如果不想要使用**入门网站**模板，您可以创建您自己注册页上，登录页上，依次类推。

本文重点介绍第一个选项&mdash;如何通过添加安全**入门网站**模板。 它还提供了有关如何实现您自己的安全一些基本信息，然后提供指向有关如何执行此操作的详细信息。 此外，还有如何启用外部登录名，在单独的文章中的更详细地介绍有关的信息。

## <a name="creating-website-security-using-the-starter-site-template"></a>使用初学者网站模板创建网站安全

在 WebMatrix 中，可以使用**入门网站**模板来创建包含以下网站：

- 用于存储用户名和密码，为您的成员数据库。
- 一个匿名的 （新） 用户可以在其中注册的注册页面。
- 登录和注销页面。
- 密码恢复和重置页。

以下过程介绍如何创建站点，并对其进行配置。

1. 启动 WebMatrix 并在**快速启动**页上，选择**从模板**。
2. 选择**入门网站**模板，然后单击**确定**。 WebMatrix 将创建新站点。
3. 在左窗格中，单击**文件**工作区选择器。
4. 在你的网站的根文件夹，打开 *\_AppStart.cshtml*文件，它是用于包含全局设置的特殊文件。 它包含已被注释掉使用某些语句`//`字符：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    这些语句配置`WebMail`帮助器，可用于发送电子邮件。 成员资格系统可以使用电子邮件发送确认消息，当用户注册时或在想要更改其密码时。 （例如，用户注册后，会得到他们可以单击以完成注册过程的链接的电子邮件。）

    发送电子邮件需要 SMTP 服务器的访问权限，如中所述[添加到 ASP.NET Web Pages 站点的电子邮件](https://go.microsoft.com/fwlink/?LinkId=202899)。 将此 central 中存储的电子邮件设置 *\_AppStart.cshtml*文件，以便无需到可以发送电子邮件的每个页中重复代码。 （无需配置 SMTP 设置，以设置注册数据库; 如果你想要验证其电子邮件别名的用户和让用户重置忘记的密码，则会仅需要 SMTP 设置。）
5. 取消注释语句删除`//`前面每个。

    如果您不想要设置电子邮件确认，则可以跳过此步骤和下一步。 如果未设置 SMTP 值，新帐户将立即显示而无需确认电子邮件。
6. 修改代码中电子邮件相关的以下设置：

   - 设置`WebMail.SmtpServer`到有权访问 SMTP 服务器的名称。
   - 将保留`WebMail.EnableSsl`设置为`true`。 此设置可保护对它们进行加密发送到 SMTP 服务器的凭据。
   - 设置`WebMail.UserName`到 SMTP 服务器帐户的用户名。
   - 设置`WebMail.Password`为 SMTP 服务器帐户的密码。
   - 设置`WebMail.From`到电子邮件地址。 这是从发送消息的电子邮件地址。

     > [!NOTE] 
     > 
     > **提示**有关这些属性的值的其他信息，请参阅[配置电子邮件设置](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings)中[自定义网站的行为为 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkID=202906)。
7. 保存并关闭 *\_AppStart.cshtml*。
8. 运行*Default.cshtml*页在浏览器中。

    ![安全-成员身份-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 如果看到一个错误，指出属性必须是实例`ExtendedMembershipProvider`，不可能将站点配置为使用 ASP.NET Web Pages 成员资格系统 （simplemembership 一起）。 这可能有时如果不同于你的本地服务器配置宿主提供程序的服务器。 若要解决此问题，请将以下元素添加到站点的*Web.config*文件：
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 将此元素添加为的子`<configuration>`元素的对等的以及`<system.web>`元素。
9. 在页面右上角，单击**注册**链接。 *Register.cshtml*显示页。
10. 输入用户名和密码，然后单击**注册**。

    ![安全-成员身份-3](16-adding-security-and-membership/_static/image2.png)

    创建从网站时**入门网站**模板，名为的数据库*StarterSite.sdf*在站点中创建*应用\_数据*文件夹。 在注册期间，你的用户信息添加到数据库。 如果将 SMTP 值，一条消息是发送到电子邮件地址中，使用以便完成注册。

    ![安全-成员身份-4](16-adding-security-and-membership/_static/image3.png)
11. 转到您的电子邮件程序，找到消息，这将与站点中没有您的确认代码和的超链接。
12. 单击超链接以激活你的帐户。 确认超链接打开注册确认页。

    ![安全-成员身份-5](16-adding-security-and-membership/_static/image4.png)
13. 单击**登录名**链接，并使用你注册的帐户，然后登录。

      您登录后**登录名**并**注册**替换为链接**注销**链接。 您的登录名显示为链接。 （该链接可转到一个页面，您可以在其中更改你的密码。）

      ![安全的成员身份 6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 默认情况下，ASP.NET web 页面将凭据发送到服务器以明文形式 （作为用户可读文本）。 生产站点应使用安全 HTTP (https:// ，也称为*安全套接字层*或 SSL) 与服务器交换的敏感信息进行加密。 可以所需的电子邮件要发送的消息通过设置使用 SSL`WebMail.EnableSsl=true`如前面的示例中所示。 有关 SSL 的详细信息，请参阅[保护 Web 通信： 证书、 SSL 和 https://](https://go.microsoft.com/fwlink/?LinkId=208660)。

## <a name="additional-membership-functionality-in-the-site"></a>在站点中的其他成员资格功能

您的网站包含其他功能，让用户管理他们的帐户。 用户可以执行以下操作：

- 更改其密码。 登录后，他们可以单击用户名 （这是一个链接）。 这使它们转到一个页面，用于创建新密码 (*Account/ChangePassword.cshtml*)。
- 恢复忘记的密码。 在登录页上，是一个链接 (**是否忘记了密码？**)，使用户进入页面 (*Account/ForgotPassword.cshtml*) 可在其中输入电子邮件地址。 该站点将其发送电子邮件具有他们可以单击以设置新密码的链接 (*Account/PasswordReset.cshtml*)。

您还可以让用户还可以使用外部站点，登录，如下所述更高版本。

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>创建仅限成员的页面

目前，任何人都可以浏览到你的网站中的任意页面。 但你可能想要仅适用于已登录用户的页面 (即，对成员)。 ASP.NET 允许您创建仅登录的成员可以访问的页面。 通常情况下，如果匿名用户尝试访问的仅限成员的页面，您将重定向它们到登录页。

在此过程中，将创建一个文件夹将包含仅供已登录的用户的页面。

1. 在站点的根目录，创建一个新文件夹。 (在功能区中，单击下的箭头**新建**，然后选择**新文件夹**。)
2. 将新文件夹命名*成员*。
3. 内部*成员*文件夹中，创建一个新页面，并将其命名为*MembersInformation.cshtml*。
4. 现有内容替换为以下代码和标记：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    此代码会测试`IsAuthenticated`的属性`WebSecurity`对象，它将返回`true`如果用户已登录。 如果用户未登录，该代码调用`Response.Redirect`发送到用户*Login.cshtml*页面*帐户*文件夹。

    重定向的 URL 中包括`returnUrl`查询字符串值使用`Request.Url.LocalPath`设置当前页的路径。 如果您设置`returnUrl`如下查询字符串中的值 （和返回 URL 是否是本地路径），登录页将用户后返回到此页进行登录。

    此代码还设置 *\_SiteLayout.cshtml*作为其布局页的页。 (有关布局页的详细信息，请参阅[在 ASP.NET Web Pages 站点中创建一致布局](https://go.microsoft.com/fwlink/?LinkId=202891)。)
5. 运行该站点。 如果你仍登录，请单击**注销**在页面顶部的按钮。
6. 在浏览器请求页面 */成员/MembersInformation*。 例如，URL 可能如下所示：

    `http://localhost:38366/Members/MembersInformation`

    （端口号 (38366) 可能会在你的 URL 不同。）

    将重定向到*Login.cshtml*页上，因为您没有登录。
7. 使用前面创建的帐户登录。 重定向回*MembersInformation*页。 因为在登录，此时会显示页面内容。

若要保护对多个页的访问，可以执行此操作：

- 添加到每个页面的安全检查。
- 创建 *\_PageStart.cshtml*其中保留受保护的页面，并添加的安全检查的文件夹中的页。 *\_PageStart.cshtml*页充当一种的文件夹中的所有页面全局网页。 中更详细地解释此技术[自定义网站的行为为 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)。

## <a name="creating-security-for-groups-of-users-roles"></a>创建安全组的用户 （角色）

如果你的站点包含大量成员，它不是高效分别检查每个用户的权限，然后让他们看到的页面。 您可以执行的操作是创建组，或*角色*，各个成员属于。 然后可以检查基于角色的权限。 在本部分中，将创建&quot;管理员&quot;角色，然后创建可供用户访问的页面中 （属于） 该角色。

ASP.NET 成员资格系统设置以支持角色。 但是，与成员身份注册和登录名，不同**入门网站**模板不包含页，帮助您管理角色。 （管理角色是管理任务，而不是用户任务。）但是，您可以直接在 WebMatrix 中的成员资格数据库中添加组。

1. 在 WebMatrix 中，单击**数据库**工作区选择器。
2. 在左窗格中，打开*StarterSite.sdf*节点，打开**表**节点，然后再双击*网页\_角色*表。

    ![安全的成员身份-7](16-adding-security-and-membership/_static/image6.png)
3. 添加名为的角色&quot;管理员&quot;。 *RoleId*自动填写字段。 (它是主键，并已设置是标识字段，如中所述[使用 ASP.NET Web Pages 站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)。)
4. 记下的值是什么*RoleId*字段。 （如果这是你定义的第一个角色，它将为 1）。

    ![安全的成员身份 8](16-adding-security-and-membership/_static/image7.png)
5. 关闭*网页\_角色*表。
6. 打开*UserProfile*表。
7. 请记下的*UserId*的一个或多个表，然后关闭表中的用户值。
8. 打开*网页\_UserInRoles*表并输入*UserID*和一个*RoleID*到表的值。 例如，若要将放入用户 2&quot;管理员&quot;角色，将输入以下值：

    ![安全的成员身份 9](16-adding-security-and-membership/_static/image8.png)
9. 关闭*网页\_UsersInRoles*表。

    现在，已定义的角色，可以配置该角色中的用户都可访问的页面。
10. 在网站根文件夹中，创建一个名为的新页*AdminError.cshtml*和现有内容替换为以下代码。 这将是如果它们不允许访问的页的用户将重定向到的页。

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 在网站根文件夹中，创建一个名为的新页*AdminOnly.cshtml*和现有代码替换为以下代码：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    `Roles.IsUserInRole`方法将返回`true`当前用户是否属于指定角色 （在此情况下，"管理员"角色）。
12. 运行*Default.cshtml*在浏览器中，但不登录。 （如果你尚未登录，注销。）
13. 在浏览器的地址栏中添加*AdminOnly*在 URL 中。 (即，请求*AdminOnly.cshtml*文件。)将重定向到*AdminError.cshtml*页上，因为您不当前登录为中的用户&quot;管理员&quot;角色。
14. 返回到*Default.cshtml*并以将用户添加到登录&quot;管理员&quot;角色。
15. 浏览到*AdminOnly.cshtml*页。 此时会显示页面。

## <a name="preventing-automated-programs-from-joining-your-website"></a>防止自动的程序加入你的网站

登录页不会停止自动的程序 (有时称为*web 机器人*或*机器人*) 从注册到你的网站。 此过程描述如何启用注册页的 ReCaptcha 测试。

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. 注册你的网站在 ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))。 完成注册后，您将获得一个公钥和私钥。
2. 将 ASP.NET Web Helpers Library 添加到你的网站，如中所述[ASP.NET Web Pages 站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)，如果你尚未准备好。
3. 在中*帐户*文件夹中，打开该文件命名为*Register.cshtml*。
4. 在页面顶部的代码中，找到以下行并取消其注释通过删除`//`注释字符：

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. 替换为`PRIVATE_KEY`与自己 ReCaptcha 私钥。
6. 在页面的标记中，删除`@*`和`*@`从周围页面标记中的以下行的注释字符：

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. 替换为`PUBLIC_KEY`与你的密钥。
8. 如果还没有已删除它，则删除`<div>`包含文本"若要启用 CAPTCHA 验证..."开头的元素。 (删除整个`<div>`元素及其内容。)

9. 运行*Default.cshtml*在浏览器中。 如果你登录到该站点，请单击**注销**链接。
10. 单击**注册**链接和测试使用 CAPTCHA 测试注册。

     ![安全-成员身份-10](16-adding-security-and-membership/_static/image9.png)

有关详细信息`ReCaptcha`帮助器，请参阅[防止自动程序 （机器人） 从使用 ASP.NET Web 站点使用 CATPCHA](https://go.microsoft.com/fwlink/?LinkId=251967)。

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>允许用户在使用外部站点进行登录

**入门网站**模板包括代码和标记，可让用户使用 Facebook、 Windows Live、 Twitter、 Google 或 Yahoo 登录。 默认情况下不启用此功能。 一般的过程使用让用户使用这些外部提供程序的登录名是这样：

- 决定你想要支持哪些外部站点。
- 如果需要，请转到该站点并设置登录应用。 （例如，您需要执行此操作以允许 Facebook 登录名。）
- 在网站中，配置提供程序。 在大多数情况下，只需取消注释中的某些代码 *\_AppStart.cshtml*文件。
- 将标记添加到注册页，以便其他人中的日志记录的外部站点的链接。 通常可以将复制需要并稍有更改的文本的标记。

可以在主题中找到的分步说明[启用从 ASP.NET Web Pages 站点中的外部站点的登录名](https://go.microsoft.com/fwlink/?LinkId=251969)。

用户登录时从另一个站点后，用户在返回到你的站点和*相关联*该登录名与您的网站。 实际上，这将在用户的外部登录名的站点中创建成员资格条目。 这允许您使用外部登录名使用 （例如角色） 的成员身份的正常功能。

## <a name="adding-security-to-an-existing-website"></a>向现有的网站的安全性

在本文前面的过程依赖于使用**入门网站**作为网站安全的基础模板。 如果不是你能够从启动**入门网站**模板或要从基于该模板站点复制相关的页，可以实现相同的安全类型在自己网站中自行编码。 创建相同的页面类型 — 注册、 登录名，等等 — 然后使用帮助程序和类将成员资格设置。

基本过程在博客文章中所述[最基本的方法来实现 ASP.NET Razor 安全](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)。 完成大部分工作是使用以下方法和属性`WebSecurity`帮助程序：

- [WebSecurty.UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx)， [WebSecurity.CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx)。 这些方法可确定是否有人是否已注册，以及如何注册它们。
- [WebSecurty.IsAuthenticated](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx)。 此属性可以确定当前用户是否已登录。 这可用于将用户重定向到登录页，如果它们具有尚未登录。
- [WebSecurity.Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx)， [WebSecurity.Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx)。 这些方法记录用户扩展或缩减。
- [WebSecurity.CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx)。 此属性可用于显示当前用户的登录的名称 （如果用户已登录）。
- [WebSecurity.ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx)。 此方法很有用，如果设置了注册的电子邮件确认。 (详细信息所述的博客文章[确认功能用于 ASP.NET Web Pages 安全](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)。)

若要管理角色，可以使用[角色](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx)并[成员身份](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx)类，如博客文章中所述。

## <a name="additional-resources"></a>其他资源

- [自定义站点范围内的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
- [保护 Web 通信： 证书、 SSL 和 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [若要实现 ASP.NET Razor 安全性的最基本方法](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)并[确认功能用于 ASP.NET Web Pages 安全](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)。 这些是介绍如何实现 ASP.NET 成员资格功能而无需使用的博客文章**入门网站**模板。
- [在 ASP.NET 网站中启用从外部站点进行登录](https://go.microsoft.com/fwlink/?LinkId=251969)
- [WebSecurity 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99))(MSDN)
- [SimpleRoleProvider 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99))(MSDN)
- [SimpleMembershipProvider 类 API 参考](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99))(MSDN)
