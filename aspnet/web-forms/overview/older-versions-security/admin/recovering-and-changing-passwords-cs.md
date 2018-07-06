---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: 恢复和更改密码 (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET 包括用于帮助恢复和更改密码的两个 Web 控件。 PasswordRecovery 控件启用访问者恢复他丢失的 pa...
ms.author: aspnetcontent
ms.date: 04/01/2008
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: e63d3d1153c81c1bb54a1fb6bb242df032899511
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824333"
---
<a name="recovering-and-changing-passwords-c"></a>恢复和更改密码 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET 包括用于帮助恢复和更改密码的两个 Web 控件。 PasswordRecovery 控件，以恢复丢失的密码的访问者。 ChangePassword 控件允许用户更新其密码。 与其他与登录相关 Web 控件类似情况下，我们已了解在本系列教程的 PasswordRecovery 整个和 ChangePassword 控件使用成员资格框架在后台重置或修改用户的密码。


## <a name="introduction"></a>介绍

之间的我的银行、 公用事业公司、 电话公司、 电子邮件帐户和个性化的 web 门户网站，I，与大多数人一样使用了多个要记住的不同密码。 使用凭据这么多，记住这些天，不常见的忘记了密码。 若要考虑到这一点，需要包括一种方法来恢复其密码的用户提供用户帐户的网站。 此过程通常涉及生成一个新的随机密码和文件的用户的电子邮件地址通过电子邮件发送。 接收新密码后大多数用户返回到该站点并到一个更容易记住的随机生成一个从更改其密码。

ASP.NET 包括用于帮助恢复和更改密码的两个 Web 控件。 PasswordRecovery 控件，以恢复丢失的密码的访问者。 ChangePassword 控件允许用户更新其密码。 与其他与登录相关 Web 控件类似情况下，我们已了解在本系列教程的 PasswordRecovery 整个和 ChangePassword 控件使用成员资格框架在后台重置或修改用户的密码。

在本教程中，我们将说明使用这两个控件。 我们还将了解如何以编程方式更改和重置用户的密码，通过`MembershipUser`类的`ChangePassword`和`ResetPassword`方法。

## <a name="step-1-helping-users-recover-lost-passwords"></a>步骤 1： 帮助用户恢复丢失密码

支持用户帐户的所有网站都需要向用户提供一些机制来恢复其遗忘的密码。 好消息是，在 ASP.NET 中实现此类功能是由于 PasswordRecovery Web 控件变得轻而易举。 PasswordRecovery 控件呈现提示用户输入其用户名的接口并根据需要其安全问题答案。 它然后通过电子邮件发送用户其密码。

> [!NOTE]
> 由于电子邮件消息传输通过网络传输纯文本有安全风险所涉及的发送电子邮件的用户的密码。


PasswordRecovery 控件包含三个视图：

- **用户名**-会提示他们的用户名的访问者。 这是初始视图。
- **问题**-显示为文本，以及用户输入其安全问题答案文本框的用户的用户名和安全问题。
- **成功**-显示一条消息，通知用户其密码已发送电子邮件。

显示视图，并由 PasswordRecovery 控件执行的操作取决于以下的成员身份配置设置：

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

成员资格框架`RequiresQuestionAndAnswer`设置指示用户是否必须指定一个安全提示问题和答案时注册的帐户。 如中所述<a id="_msoanchor_1"> </a> [*创建用户帐户*](../membership/creating-user-accounts-cs.md)教程中，如果`RequiresQuestionAndAnswer`为 True （默认值），则 CreateUserWizard 的接口包含文本框控件的新用户的安全问题和答案;如果`RequiresQuestionAndAnswer`为 False 时，会收集任何此类信息。 同样，如果`RequiresQuestionAndAnswer`为 True，则问题查看用户输入其用户名后 PasswordRecovery 控件显示; 仅当在用户输入正确的安全答案为其恢复密码。 如果`RequiresQuestionAndAnswer`为 False，但是，取回控件将直接从用户名视图移到成功视图。

用户已提供其用户名的或其用户名和安全的答案，如果后`RequiresQuestionAndAnswer`为 PasswordRecovery 的 True-其密码的电子邮件用户。 如果`EnablePasswordRetrieval`选项设置为 True，则用户电子邮件通知他们当前的密码。 如果设置为 False 和`EnablePasswordReset`设置为 True，则 PasswordRecovery 控件生成一个新的随机密码，对于用户，并发送电子邮件向其此新密码。 如果这两个`EnablePasswordRetrieval`和`EnablePasswordReset`均为 False，则 PasswordRecovery 控件将引发异常。

> [!NOTE]
> 请记住，`SqlMembershipProvider`将用户的密码存储在三种格式之一： 清除、 哈希 （默认值） 或加密。 使用的存储机制取决于成员身份配置设置;演示应用程序使用 Hashed 密码格式。 使用 Hashed 密码格式时`EnablePasswordRetrieval`选项必须设置为 False，因为系统将无法确定从数据库中存储的哈希版本的用户的实际密码。


图 1 说明 PasswordRecovery 的接口和行为的成员身份配置影响。


[![RequiresQuestionAndAnswer、 EnablePasswordRetrieval 和 EnablePasswordReset 影响 PasswordRecovery 控件的外观和行为](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**图 1**: `RequiresQuestionAndAnswer`， `EnablePasswordRetrieval`，和`EnablePasswordReset`影响 PasswordRecovery 控件的外观和行为 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image3.png))


> [!NOTE]
> 在中<a id="_msoanchor_2"> </a> [ *SQL Server 中创建成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-cs.md)我们通过设置来配置成员资格提供程序的教程`RequiresQuestionAndAnswer`为 True，`EnablePasswordRetrieval`到为 false，和`EnablePasswordReset`为 True。


### <a name="using-the-passwordrecovery-control"></a>使用 PasswordRecovery 控件

让我们看看在 ASP.NET 页面中使用 PasswordRecovery 控件。 打开`RecoverPassword.aspx`并拖动和删除取回控件从工具箱拖到设计器; 设置其`ID`到`RecoverPwd`。 登录名和 CreateUserWizard Web 控件，如 PasswordRecovery 控件的视图呈现丰富的复合界面，其中包括标签、 文本框、 按钮和验证控件。 您可以自定义视图通过控件的样式属性或通过将视图转换为模板的外观。 我将此作为练习留给感读取器。

当用户访问此页她将输入其用户名，然后单击提交按钮。 因为我们已经设置了`RequiresQuestionAndAnswer`控制将属性设置为在我们的成员身份配置设置中，PasswordRecovery True，则显示问题视图。 用户输入其正确的安全答案，并单击提交后，如何将用户的密码更新为一个随机生成的活动，和电子邮件上文件的电子邮件地址的此密码。 所有这些都是没有我们无需编写一行代码 ！

测试此页之前，还有最后一项要倾向于配置的： 我们需要指定中的邮件传递设置`Web.config`。 PasswordRecovery 控件依赖这些设置用于发送电子邮件。

通过指定的邮件传递配置[`<system.net>`元素](https://msdn.microsoft.com/library/6484zdc1.aspx)的[`<mailSettings>`元素](https://msdn.microsoft.com/library/w355a94k.aspx)。 使用[`<smtp>`元素](https://msdn.microsoft.com/library/ms164240.aspx)以指示传递方法和发件人地址默认值。 以下标记将使用名为的网络 SMTP 服务器邮件设置配置为`smtp.example.com`在端口 25 上并使用用户名/密码凭据的用户名和密码。

> [!NOTE]
> `<system.net>` 是根的子元素`<configuration>`元素和的同级`<system.web>`。 因此，不要将放`<system.net>`元素内的`<system.web>`元素; 而是将其放在同一级别上。


[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

除了在网络上使用的 SMTP 服务器，或者可以指定其中应存放要发送的电子邮件的拾取目录。

一旦已配置的 SMTP 设置，请访问`RecoverPassword.aspx`通过浏览器的页。 首先，请尝试输入的用户名的用户存储中不存在。 如图 2 所示，PasswordRecovery 控件将显示一条消息指出无法访问用户信息。 可以通过控件的自定义消息的文本[`UserNameFailureText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)。


[![如果输入无效的用户名，显示一条错误消息](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**图 2**： 如果输入无效的用户名，则会显示错误消息 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image6.png))


现在，输入用户名。 使用知道的电子邮件地址可以访问和回答其安全系统中的帐户的用户名。 输入用户名并单击提交后, PasswordRecovery 控件显示其问题的视图。 作为使用用户名视图中，如果输入不正确回答 PasswordRecovery 控件显示错误消息 （请参见图 3）。 使用[`QuestionFailureText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx)自定义此错误消息。


[![如果用户输入无效的安全提示问题答案，显示一条错误消息](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**图 3**： 如果用户输入无效的安全提示问题答案，会显示错误消息 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image9.png))


最后，输入正确的安全答案，并单击提交。 在后台，PasswordRecovery 控制将生成随机密码，将其分配给用户帐户，将发送一封电子邮件，通知其新密码的用户 （请参阅图 4），然后显示成功视图。


[![向用户发送一封电子邮件使用 His 的新密码](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**图 4**： 向用户发送一封电子邮件使用 His 的新密码 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image12.png))


### <a name="customizing-the-email"></a>自定义电子邮件

发送由 PasswordRecovery 控件的默认电子邮件是相当乏味 （请参阅图 4）。 默认情况下，邮件中指定的帐户从`<smtp>`元素的`from`具有使用者密码属性和纯文本正文：

请返回到该站点，然后使用以下信息登录。

用户名：*用户名*

密码：*密码*

此消息都可以通过为 PasswordRecovery 控件的事件处理程序以编程方式自定义[`SendingMail`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)，或以声明方式通过[`MailDefinition`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)。 我们来探讨这两种选项。

`SendingMail`电子邮件消息发送，并且是我们最后一次机会来以编程方式调整的电子邮件消息之前触发事件。 当引发此事件时，事件处理程序传递类型的对象[ `MailMessageEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)，其`Message`属性包含对要发送的电子邮件的引用。

创建事件处理程序`SendingMail`事件，并添加以下代码，以便以编程方式添加`webmaster@example.com`到抄送列表。

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

此外可以通过声明性方式配置电子邮件。 PasswordRecovery`MailDefinition`属性是一个对象类型[ `MailDefinition` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)。 `MailDefinition`类提供了一系列电子邮件相关的属性，包括`From`， `CC`， `Priority`， `Subject`， `IsBodyHtml`， `BodyFileName`，等等。 对于初学者而言，设置[`Subject`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx)为更具描述性比默认情况下 （密码），如你的密码已重置使用...

若要自定义我们需要创建单独的电子邮件模板文件的电子邮件的正文包含正文的内容。 首先创建一个新的文件夹中名为的网站`EmailTemplates`。 接下来，将新的文本文件添加到此文件夹名为`PasswordRecovery.txt`并添加以下内容：

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

请注意，使用占位符`<%UserName%>`和`<%Password%>`。 使用用户的用户名和已恢复的密码在发送电子邮件前将取回控件自动替换这些两个占位符。

最后，点`MailDefinition`的[`BodyFileName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)到我们刚刚创建的电子邮件模板 (`~/EmailTemplates/PasswordRecovery.txt`)。

执行这些更改重新访问后`RecoverPassword.aspx`页，并输入用户名和安全答案。 你收到应如图 5 中所示的电子邮件。 请注意，`webmaster@example.com`已经将抄送和，已更新的主题和正文。


[![已更新主题、 正文和抄送列表](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**图 5**: 主题、 正文和抄送已更新列表 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image15.png))


若要发送 HTML 格式的电子邮件设置[ `IsBodyHtml` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx)为 True （默认值为 False），并且更新电子邮件模板包含 HTML。

`MailDefinition`属性不是唯一的 PasswordRecovery 类。 我们将在步骤 2 中看到的 ChangePassword 控件还提供了`MailDefinition`属性。 此外，CreateUserWizard 控件包括这样的属性，您可以配置自动向新用户发送欢迎电子邮件消息。

> [!NOTE]
> 当前没有任何链接在左侧导航栏中达到`RecoverPassword.aspx`页。 用户仅有兴趣在如果她已成功登录到该站点无法访问此页。 因此，更新`Login.aspx`页以包含一个指向`RecoverPassword.aspx`页。


### <a name="programmatically-resetting-a-users-password"></a>以编程方式重置用户的密码

当重置用户的密码 PasswordRecovery 控制调用`MembershipUser`对象的[`ResetPassword`方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)。 此方法有两个重载：

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -重置用户的密码。 如果使用此重载`RequiresQuestionAndAnswer`为 False。
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -重置用户的密码仅当提供*securityAnswer*正确无误。 如果使用此重载`RequiresQuestionAndAnswer`为 True。

这两个重载将返回随机生成的新密码。

使用成员资格框架中的其他方法等`ResetPassword`方法委托给配置的提供程序。 `SqlMembershipProvider`调用`aspnet_Membership_ResetPassword`传递存储过程，在用户的用户名、 新密码和其他字段中提供的密码答案。 存储的过程可确保密码提示问题答案与匹配，并更新用户的密码。

几个低级别实现说明：

- 锁定的用户无法重置其密码。 但是，可能会未经批准的用户。 我们将讨论锁定出和批准状态中更详细地<a id="_msoanchor_3"> </a> [ *Unlocking 和批准用户*](unlocking-and-approving-user-accounts-cs.md)帐户教程。
- 如果密码提示问题答案不正确，用户的失败的密码答案尝试计数将递增。 如果指定的时间范围内发生指定的数量的无效的安全提示问题答案尝试，用户被锁定。

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>有关如何的随机密码生成

图 4 和 5 中的电子邮件中所示的随机生成的密码创建的成员资格类[`GeneratePassword`方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)。 此方法接受两个整数输入的参数-*长度*并*numberOfNonAlphanumericCharacters* -并至少返回一个字符串*长度*在长时间使用字符至少*numberOfNonAlphanumericCharacters*非字母数字字符数。 当此方法的调用时从成员资格类或与登录相关 Web 控件中时，将这两个参数的值由成员身份配置`MinRequiredPasswordLength`和`MinRequiredNonalphanumericCharacters`属性，我们分别设置为 7 和 1。

`GeneratePassword`方法使用强加密型随机数生成器来确保中会选择哪些随机字符无偏差。 此外，`GeneratePassword`是`public`，这意味着，您可以使用它直接从 ASP.NET 应用程序如果需要生成随机字符串或密码。

> [!NOTE]
> `SqlMembershipProvider`类始终生成随机密码至少为 14 个字符，因此，如果`MinRequiredPasswordLength`小于 14 就会忽略其值。


## <a name="step-2-changing-passwords"></a>步骤 2： 更改密码

随机生成密码很难记住。 图 4 所示的密码，请考虑： `WWGUZv(f2yM:Bd`。 请尝试提交的内存 ！ 不用说，向用户发送此类随机生成的密码后，她需要的密码更改为更容易记住的内容。

使用 ChangePassword 控件创建一个接口，使用户能够更改其密码。 更类似于 PasswordRecovery 控件的 ChangePassword 控件包含两个视图： 更改密码和成功。 更改密码视图会提示用户输入其旧的和新密码。 在提供正确的旧密码和新密码满足最小长度和非字母数字字符要求，ChangePassword 控件更新用户的密码，并显示成功视图。

> [!NOTE]
> ChangePassword 控件通过调用修改用户的密码`MembershipUser`对象的[`ChangePassword`方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)。 ChangePassword 方法接受两个`string`输入参数的*oldPassword*并*newPassword*的和更新用户的帐户与*newPassword*，假定提供*oldPassword*正确无误。


打开`ChangePassword.aspx`页上，并将 ChangePassword 控件添加到页上，其命名为`ChangePwd`。 此时，设计视图应显示更改密码查看 （请参阅图 6）。 如 PasswordRecovery 控件后，你可以在视图之间切换通过控件的智能标记。 此外，这些视图的外观是通过各种类型的样式属性或将它们转换为模板，可自定义。


[![ChangePassword 控件添加到页面](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**图 6**： 将 ChangePassword 控件添加到页 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image18.png))


ChangePassword 控件可以更新当前已登录的用户的密码*或*另一个，指定用户的密码。 如图 6 所示，默认更改密码视图呈现只是三个文本框控件： 一个用于旧密码，两个新密码。 此默认接口用于更新当前已登录的用户的密码。

若要使用 ChangePassword 控件更新其他用户的密码，设置控件的[`DisplayUserName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx)为 True。 执行此操作将第四个文本框添加到页上，若要更改其密码提示输入用户的用户名。

设置`DisplayUserName`到，如果你想要让已注销用户而无需登录时更改其密码有用则为 True。 就个人而言，我认为没有什么不妥允许用户更改其密码前需登录到用户。 因此，请让`DisplayUserName`设置为 False （其默认值）。 在做出此决策，但是，我们实质上不包括匿名用户访问此页。 更新站点的 URL 授权规则以拒绝匿名用户访问从`ChangePassword.aspx`。 如果你需要刷新你的 URL 授权规则语法上的内存，回头<a id="_msoanchor_4"> </a> [*基于用户的授权*](../membership/user-based-authorization-cs.md)教程。

> [!NOTE]
> 它可能看起来的`DisplayUserName`属性可用于允许管理员更改其他用户的密码。 但是，即使`DisplayUserName`设置为 True 必须知道并输入正确的旧密码。 我们将讨论从而使管理员可以更改在步骤 3 中的用户的密码的方法。


请访问`ChangePassword.aspx`通过浏览器页并更改你的密码。 请注意，是否输入不能满足密码长度和成员身份配置中指定的非字母数字字符要求的新密码将显示一条错误消息 （请参阅图 7）。


[![ChangePassword 控件添加到页面](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**图 7**： 将 ChangePassword 控件添加到页 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image21.png))


在输入正确的旧密码和有效新密码，已登录用户的密码已更改，显示成功视图。

### <a name="sending-a-confirmation-email"></a>发送确认电子邮件

默认情况下，ChangePassword 控件不到刚刚更新了其密码的用户发送一封电子邮件。 如果你想要将发送一封电子邮件，只需配置该控件的`MailDefinition`属性。 让我们配置 ChangePassword 控件，以便向用户发送包含其新密码的 HTML 格式电子邮件。

首先，创建的新文件中`EmailTemplates`文件夹名为`ChangePassword.htm`。 添加以下标记：

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

接下来，设置 ChangePassword 控件`MailDefinition`属性的`BodyFileName`， `IsBodyHtml`，和`Subject`属性设置为 ~ / EmailTemplates/ChangePassword.htm，True 和你的密码已更改 ！ 分别。

进行这些更改之后, 重新访问该页并再次更改密码。 这一次，ChangePassword 控件将发送到用户的电子邮件地址上文件的自定义的 HTML 格式的电子邮件 （请参阅图 8）。


[![电子邮件消息会通知用户，他们的密码已更改](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**图 8**: 电子邮件消息通知用户，他们的密码已更改 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image24.png))


## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>步骤 3： 允许管理员更改用户的密码

在支持用户帐户的应用程序中的一个常见功能是管理用户，以更改其他用户的密码的功能。 有时此功能是必需的因为系统不具备用户更改其自己的密码的功能。 在这种情况下，恢复其忘记了的密码的用户的唯一方法会让管理员将其分配新密码。 PasswordRecovery 和 ChangePassword 控件，但是，管理用户需要不忙本身与更改用户的密码，因为用户能够执行此本身。

但是，如果您的客户端坚持管理用户应该能够更改其他用户的密码？ 遗憾的是，添加此功能可以是一些工作。 若要更改用户的密码，旧的和新密码必须提供给`MembershipUser`对象的`ChangePassword`方法，但管理员无需知道用户的密码，才能对其进行修改。

一种解决办法是首先重置用户的密码，然后将其更改为使用如下所示的代码的新密码：

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

此代码首先会检索有关的信息*用户名*，这是管理员想要更改其密码的用户。 下一步，`ResetPassword`调用方法时，哪些分配和用户的新的随机密码。 方法返回此随机生成的密码并将其存储在变量`resetPwd`。 现在，我们知道用户的密码，我们可以将其更改通过调用`ChangePassword`。

问题是，此代码仅适用如果成员资格系统配置设置，以便`RequiresQuestionAndAnswer`为 False。 如果`RequiresQuestionAndAnswer`为 True，这一点与我们的应用程序，则`ResetPassword`方法需要传递的安全答案，否则它将引发异常。

如果成员资格框架配置为要求安全问题和答案，和你的客户端尚未坚持，管理员必须能够更改用户的密码，则有三个选项：

- 在空中运动引发手，告诉你的客户端，这是不能做的只是一件事。
- 设置`RequiresQuestionAndAnswer`为 False。 这会导致安全级别较低的应用程序。 假设恶意用户获得了对其他用户的电子邮件收件箱的访问。 可能被入侵的用户已离开其办公桌去享用午餐，没有锁定其工作站，或可能是从公共终端访问其电子邮件和未注销。在任一情况下，恶意用户可以访问`RecoverPassword.aspx`页，并输入用户的用户名。 系统将通过电子邮件发送的已恢复的密码而不提示的安全答案。
- 跳过创建的成员资格框架和直接使用 SQL Server 数据库的抽象层。 成员身份架构包括一个名为的存储的过程`aspnet_Membership_SetPassword`，设置用户的密码，并且不需要的安全答案或旧密码的完成其任务。

这些选项都不是特别有吸引力，但这是开发人员的生活有时出现的方式。

下来，实现第三种方法，编写代码时绕过`Membership`并`MembershipUser`类，并直接对其操作`SecurityTutorials`数据库。

> [!NOTE]
> 通过直接使用数据库，提供的成员资格框架的封装已被破坏。 此决定会绑定到我们`SqlMembershipProvider`，从而使我们更少可移植的代码。 此外，此代码可能无法按预期在将来版本的 ASP.NET 中，如果成员身份架构发生更改。 这种方法是一种解决方法，并像大多数解决方法，不是最佳做法的示例。


代码具有一些不严重的位，非常长。 因此，我不想使本教程中使用它的深入探讨变得混乱。 如果您有兴趣学习的详细信息，下载的代码对于此教程，请访问`~/Administration/ManageUsers.aspx`页。 此页上，我们在中创建<a id="_msoanchor_5"> </a>[前面的教程](building-an-interface-to-select-one-user-account-from-many-cs.md)，列出了每个用户。 我更新了 GridView，其中包含一个指向`UserInformation.aspx`页上，将传递查询字符串通过所选的用户的用户名。 `UserInformation.aspx`页显示有关所选的用户和文本框的信息用于更改其密码 （请参阅图 9）。

输入新密码，在第二个文本框中，确认，并单击更新用户按钮后，才会回发和`aspnet_Membership_SetPassword`调用存储的过程时，更新用户的密码。 建议对此功能感兴趣的这些读取器进一步熟悉代码，然后重扩展的功能，包括将一封电子邮件发送到已更改其密码的用户。


[![管理员可能会更改用户的密码](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**图 9**: 管理员可更改用户的密码 ([单击以查看实际尺寸的图像](recovering-and-changing-passwords-cs/_static/image27.png))


> [!NOTE]
> `UserInformation.aspx`网页当前仅适用，如果成员资格框架配置为以清除或哈希格式存储密码。 尽管你受邀添加此功能，它缺少代码的新密码进行加密。 我建议将添加所需的代码的方法是使用如反编译程序[Reflector](http://www.aisto.com/roeder/dotnet/)来检查.NET Framework; 中的方法的源代码先检查`SqlMembershipProvider`类的`ChangePassword`方法。 这是密码的我用来编写用于创建哈希代码的技术。


## <a name="summary"></a>总结

ASP.NET 提供了两个控件，帮助用户管理其密码。 PasswordRecovery 控件可用于用户忘记其密码。 根据成员资格框架的配置，用户可以通过电子邮件用户现有的密码或随机生成的新密码。 ChangePassword 控件使用户能够更新其密码。

登录名和 CreateUserWizard 控件，如 PasswordRecovery 和 ChangePassword 控件呈现丰富的用户界面而无需编写一丁点声明性标记或代码行。 如果默认用户界面不满足您的需要，可以自定义它通过各种样式属性。 或者，控件的接口可能会转换为模板，为更精细的控制。 这些控件使用成员资格 API，在后台调用`MembershipUser`对象的`ResetPassword`和`ChangePassword`方法。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ChangePassword 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` 常见问题](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者包括 Michael Emmings 和 Suchi Banerjee。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [下一页](unlocking-and-approving-user-accounts-cs.md)
