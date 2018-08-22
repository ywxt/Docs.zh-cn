---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
title: 解锁和审批用户帐户 (VB) |Microsoft Docs
author: rick-anderson
description: 本教程演示如何生成某一网页寻求管理员可以管理用户的锁定和批准状态。 我们还将了解如何批准新用户 o...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 041854a5-ea8c-4de0-82f1-121ba6cb2893
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 87f27dc1cc7271ddee8785c12d48913e3c9f2c98
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826618"
---
<a name="unlocking-and-approving-user-accounts-vb"></a>解锁和审批用户帐户 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.14.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_vb.pdf)

> 本教程演示如何生成某一网页寻求管理员可以管理用户的锁定和批准状态。 我们还将了解如何批准新用户，仅后他们验证其电子邮件地址。


## <a name="introduction"></a>介绍

用户名、 密码和电子邮件，以及每个用户帐户有两个状态字段指示用户是否可以登录到网站的： 锁定和批准。 用户会自动锁定如果它们提供无效的凭据中指定的 （默认设置后将其锁定用户 10 分钟内的 5 个无效的登录尝试） 的分钟数按指定的次数。 已批准的状态是在其中某项操作必须经过多新的用户能够登录到该站点之前的情况下很有用。 例如，用户可能需要先验证其电子邮件地址或由管理员批准之前都无法提供登录名。

因为锁定或未经批准用户无法登录，它是唯一的自然而然地想知道如何重置这些状态。 ASP.NET 不包括任何内置功能或 Web 控件，用于管理用户的锁定和部分批准状态，因为这些决策需要基于站点的站点进行处理。 某些站点可能会自动批准所有的新用户帐户 （默认行为）。 其他人有管理员批准的新帐户或不批准用户直到他们访问他们注册时提供的电子邮件地址发送的链接。 同样，某些站点可能会锁定用户，直到管理员重置其状态，而其他站点将一封电子邮件发送到 URL 的锁定用户他们可以访问要解锁其帐户。

本教程演示如何生成某一网页寻求管理员可以管理用户的锁定和批准状态。 我们还将了解如何批准新用户，仅后他们验证其电子邮件地址。

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>步骤 1： 管理用户的锁定和批准状态

在中<a id="Tutorial12"> </a> [*到选择一个用户帐户生成一个接口，从很多*](building-an-interface-to-select-one-user-account-from-many-vb.md)教程中我们构造列出中分页，每个用户帐户的页面筛选 GridView。 网格列出每个用户的名称和电子邮件、 及其已批准和锁定状态，无论它们是当前联机和有关用户的任何备注。 若要管理用户的批准和锁定状态，我们无法使此网格可编辑。 若要更改用户的已批准的状态，管理员会首先找到用户帐户，并选中或取消选中已批准复选框，然后编辑相应的 GridView 行。 或者，我们可以管理通过单独的 ASP.NET 页的已批准和锁定状态。

对于本教程，让我们使用两个 ASP.NET 页：`ManageUsers.aspx`和`UserInformation.aspx`。 这里的思路是`ManageUsers.aspx`在系统中，列出的用户帐户时`UserInformation.aspx`使管理员能够管理的特定用户的批准和锁定状态。 我们首要任务是以增加在 GridView`ManageUsers.aspx`包括 HyperLinkField，将呈现为链接的列。 我们希望每个链接以指向`UserInformation.aspx?user=UserName`，其中*用户名*是要编辑的用户的名称。

> [!NOTE]
> 如果你已下载的代码<a id="Tutorial13"> </a> [*恢复和更改密码*](recovering-and-changing-passwords-vb.md)教程，您可能已经注意到，`ManageUsers.aspx`页已包含的一组"管理"链接和`UserInformation.aspx`页会提供一个接口更改选定的用户的密码。 我决定不复制该功能在代码中与本教程中，因为它通过绕过成员身份 API 和操作直接与要更改用户的密码的 SQL Server 数据库的工作。 本教程开始使用从头`UserInformation.aspx`页。


### <a name="adding-manage-links-to-theuseraccountsgridview"></a>添加"管理"链接到`UserAccounts`GridView

打开`ManageUsers.aspx`页上，添加到 HyperLinkField `UserAccounts` GridView。 设置 HyperLinkField`Text`属性设置为"管理"并将其`DataNavigateUrlFields`并`DataNavigateUrlFormatString`属性设置为`UserName`和"UserInformation.aspx?user={0}"分别。 这些设置以便所有超链接显示文本"管理"，但每个链接会将传递在相应配置 HyperLinkField*用户名*到查询字符串值。

添加后 HyperLinkField 到 GridView，花点时间查看`ManageUsers.aspx`通过浏览器的页。 如图 1 所示，每个 GridView 行现在包括"管理"链接。 Bruce 的"管理"链接指向`UserInformation.aspx?user=Bruce`，而 Dave 的"管理"链接指向`UserInformation.aspx?user=Dave`。


[![添加了 HyperLinkField](unlocking-and-approving-user-accounts-vb/_static/image2.png)](unlocking-and-approving-user-accounts-vb/_static/image1.png)

**图 1**: HyperLinkField 将为每个用户帐户添加的"管理"链接 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image3.png))


创建用户界面，并为代码`UserInformation.aspx`页中时刻，但首先让我们讨论有关如何以编程方式更改用户的锁定和批准状态。 [ `MembershipUser`类](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)具有[ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)并[`IsApproved`属性](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)。 `IsLockedOut`属性是只读的。 没有任何机制来以编程方式锁定用户;若要解锁用户，请使用`MembershipUser`类的[`UnlockUser`方法](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)。 `IsApproved`属性是可读和可写。 若要保存对此属性的任何更改，我们需要调用`Membership`类的[`UpdateUser`方法](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)，并传入已修改`MembershipUser`对象。

因为`IsApproved`属性是可读和可写，复选框控件可能是用于配置此属性的最佳用户界面元素。 但是，一个复选框将不能用于`IsLockedOut`属性管理员不能锁定用户，因为她可能仅解锁用户。 为一个合适的用户界面`IsLockedOut`属性是一个按钮，单击时，解除了该用户帐户。 如果用户锁定，则只应启用此按钮。

### <a name="creating-theuserinformationaspxpage"></a>创建`UserInformation.aspx`页

我们现已准备好实现中的用户界面`UserInformation.aspx`。 打开此页并添加以下 Web 控件：

- 超链接控件，单击时，返回到管理员`ManageUsers.aspx`页。
- 用于显示所选的用户的名称的标签 Web 控件。 设置此标签`ID`到`UserNameLabel`并将清除其 Text 属性。
- 名为的复选框控件`IsApproved`。 设置其`AutoPostBack`属性设置为`True`。
- 用于显示用户的标签控件的上一次锁定出日期。 命名此标签`LastLockedOutDateLabel`并将清除其`Text`属性。
- 用于解锁用户按钮。 命名此按钮`UnlockUserButton`并设置其`Text`属性设置为"解锁用户"。
- 标签控件用于显示状态消息，例如"已更新用户的已批准的状态"。 命名此控件`StatusMessage`，清除出其`Text`属性，并设置其`CssClass`属性设置为`Important`。 ( `Important` CSS 类中定义`Styles.css`样式表文件; 它以大型、 红色字体显示相应的文本。)

添加这些控件之后, 在 Visual Studio 中的设计视图应类似于屏幕截图图 2 中。


[![创建 UserInformation.aspx 的用户界面](unlocking-and-approving-user-accounts-vb/_static/image5.png)](unlocking-and-approving-user-accounts-vb/_static/image4.png)

**图 2**： 创建的用户界面`UserInformation.aspx`([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image6.png))


用户界面完成后，我们的下一个任务是设置`IsApproved`复选框和其他控件根据所选的用户的信息。 创建页面的一个事件处理程序`Load`事件，并添加以下代码：

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample1.vb)]

上面的代码首先会确保这第一次访问的页面并不在后续回发。 随后，将通过传递的用户名`user`查询字符串字段，并检索有关该用户帐户，通过信息`Membership.GetUser(username)`方法。 如果没有用户名提供通过在查询字符串，或者如果找不到指定的用户，管理员发送回`ManageUsers.aspx`页。

`MembershipUser`对象的`UserName`值然后显示在`UserNameLabel`并且`IsApproved`选中复选框根据`IsApproved`属性值。

`MembershipUser`对象的[`LastLockoutDate`属性](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx)返回`DateTime`值，该值指示用户上次已锁定。如果用户永远不会被锁定，返回的值取决于成员资格提供程序。 创建新的帐户后，`SqlMembershipProvider`设置`aspnet_Membership`表的`LastLockoutDate`字段`1754-01-01 12:00:00 AM`。 上面的代码显示在一个空字符串`LastLockoutDateLabel`如果`LastLockoutDate`属性出现在年之前 2000年; 否则为的日期部分`LastLockoutDate`标签中显示属性。 `UnlockUserButton`的`Enabled`属性设置为用户的锁定状态，这意味着如果用户锁定才会启用此按钮。

请花费片刻时间来测试`UserInformation.aspx`通过浏览器的页。 您将当然，需要开始`ManageUsers.aspx`，然后选择要管理的用户帐户。 在到达`UserInformation.aspx`，请注意，`IsApproved`仅已选中复选框，如果用户批准。 如果用户曾经已锁定，则显示上一个锁定日期。 用户当前被锁定的情况下，才启用解锁用户按钮。选中或取消选中`IsApproved`复选框或单击解除锁定用户按钮会导致回发，但不修改都会对用户帐户，因为我们尚未为创建这些事件的事件处理程序。

返回到 Visual Studio 并创建事件处理程序`IsApproved`复选框的`CheckedChanged`事件并`UnlockUser`按钮的`Click`事件。 在中`CheckedChanged`事件处理程序设置的用户`IsApproved`属性设置为`Checked`属性的复选框，然后保存所做更改，通过调用`Membership.UpdateUser`。 在中`Click`事件处理程序，只需调用`MembershipUser`对象的`UnlockUser`方法。 在这两个事件处理程序中，显示在合适的消息`StatusMessage`标签。

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample2.vb)]

### <a name="testing-theuserinformationaspxpage"></a>测试`UserInformation.aspx`页

在发生这些事件处理程序，与重新访问该页和未批准的用户。 图 3 所示，你应该看到一条消息，指示在页上用户的简短`IsApproved`已成功修改属性。


[![Chris 已被未批准](unlocking-and-approving-user-accounts-vb/_static/image8.png)](unlocking-and-approving-user-accounts-vb/_static/image7.png)

**图 3**: Chris 已被未批准 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image9.png))


接下来，先注销，然后重试以用户身份登录其帐户时只是未批准。 用户未获批准，因为它们不能登录。 默认情况下，Login 控件显示同一消息，如果用户无法登录，无论是什么原因。 但在<a id="Tutorial6"> </a> [*验证用户凭据对成员身份用户存储*](../membership/validating-user-credentials-against-the-membership-user-store-vb.md)教程探讨了增强登录控件以显示更合适的消息。 如图 4 所示，Chris 是显示一条消息说明，他不能成功登录，因为他的帐户尚未批准。


[![Chris 不能登录因为 His 帐户未批准](unlocking-and-approving-user-accounts-vb/_static/image11.png)](unlocking-and-approving-user-accounts-vb/_static/image10.png)

**图 4**: Chris 不能登录因为 His 帐户是否未批准 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image12.png))


若要测试的锁定的功能，请尝试作为已批准用户，登录，但使用了错误的密码。 重复此过程所需数量的次多次，直至用户的帐户已锁定。Login 控件也已更新为显示自定义消息如果尝试从锁定的帐户登录。 您知道，帐户已锁定后，开始看到在登录页上的以下消息:"你的帐户已锁定由于无效的登录尝试次数太多。 请与管理员联系以解锁帐户。"

返回到`ManageUsers.aspx`页上，单击管理链接为锁定状态的用户。 图 5 所示，你应该看到中的值`LastLockedOutDateLabel`应启用解锁用户按钮。 单击解除锁定用户按钮以解锁用户帐户。 一旦解锁用户，他们将能够再次登录。


[![Dave 锁定系统](unlocking-and-approving-user-accounts-vb/_static/image14.png)](unlocking-and-approving-user-accounts-vb/_static/image13.png)

**图 5**: Dave 具有已锁定的系统 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image15.png))


## <a name="step-2-specifying-new-users-approved-status"></a>步骤 2： 指定新用户的批准状态

已批准的状态是在想要一个新用户能够登录并访问该站点的特定于用户的功能之前执行某些操作的情况下很有用。 例如，您可能在运行所有页面，除了登录名和注册页中，仅供经过身份验证的用户访问专用网站。 但是，会发生什么情况象是达到你的网站，查找注册页上，并创建一个帐户？ 若要避免这种情况发生无法移动到注册页`Administration`文件夹中，并且需要管理员手动创建的每个帐户。 或者，您可以允许任何人进行注册，但禁止站点访问，直到得到管理员的批准的用户帐户。

默认情况下，CreateUserWizard 控件批准新的帐户。 你可以配置使用控件的此行为[`DisableCreatedUser`属性](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)。 将此属性设置为`True`不批准新的用户帐户。

> [!NOTE]
> 默认情况下 CreateUserWizard 控件自动登录新用户帐户。 此行为由该控件的指定[`LoginCreatedUser`属性](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)。 未批准的用户无法登录到站点，因为当`DisableCreatedUser`是`True`新的用户帐户未登录到站点，而不考虑值`LoginCreatedUser`属性。


如果要以编程方式创建新用户帐户通过`Membership.CreateUser`方法中，若要创建的未批准的用户帐户使用接受新用户的重载之一`IsApproved`作为输入参数的属性值。

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>步骤 3： 批准用户通过验证其电子邮件地址

支持用户帐户的很多网站不批准新用户，直到它们验证时注册它们提供的电子邮件地址。 此验证过程通常用于防止机器人、 垃圾邮件发送者和不入流，因为它需要是唯一的已验证电子邮件地址，并在注册过程中添加一个额外的步骤。 借助此模型中，当新用户注册时它们会发送电子邮件，其中包含链接到验证页。 通过访问以下链接用户已被证明他们收到该电子邮件和，因此，提供的电子邮件，地址有效。 验证页是负责审批用户。 这可能会自动发生，从而批准的任何用户都到达此页上，或仅在用户提供一些其他信息，如后[CAPTCHA](http://en.wikipedia.org/wiki/Captcha)。

为了适应此工作流，我们需要首先更新帐户创建页面，以便新用户未获批准。 打开`EnhancedCreateUserWizard.aspx`页中`Membership`文件夹并设置 CreateUserWizard 控件`DisableCreatedUser`属性设置为`True`。

接下来，我们需要配置 CreateUserWizard 控件以将一封电子邮件发送到新用户，说明如何验证其帐户。 具体而言，我们将电子邮件中包含一个链接`Verification.aspx`页 (我们尚未为其创建)，并传入新用户的`UserId`通过在查询字符串。 `Verification.aspx`页将查找指定的用户，并将其批准的标记。

### <a name="sending-a-verification-email-to-new-users"></a>将验证电子邮件发送到新用户

若要从 CreateUserWizard 控件发送一封电子邮件，配置其`MailDefinition`属性正确。 如中所述<a id="Tutorial13"> </a>[前一篇教程](recovering-and-changing-passwords-vb.md)，ChangePassword 和 PasswordRecovery 控件包括[`MailDefinition`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)其工作方式与CreateUserWizard 控件的。

> [!NOTE]
> 若要使用`MailDefinition`中的属性需要指定邮件传递选项`Web.config`。 有关详细信息，请参阅[在 ASP.NET 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)。


首先，创建一个名为的新电子邮件模板`CreateUserWizard.txt`在`EmailTemplates`文件夹。 模板使用以下文本：

[!code-aspx[Main](unlocking-and-approving-user-accounts-vb/samples/sample3.aspx)]

设置`MailDefinition`的`BodyFileName`属性设置为"~ / EmailTemplates/CreateUserWizard.txt"并将其`Subject`属性设置为"欢迎使用我的网站 ！ 请激活您的帐户。"

请注意，`CreateUserWizard.txt`电子邮件模板包括`<%VerificationUrl%>`占位符。 这就是 URL`Verification.aspx`将放置页。 将自动替换 CreateUserWizard`<%UserName%>`并`<%Password%>`占位符替换新帐户的用户名和密码，但没有内置的`<%VerificationUrl%>`占位符。 我们需要手动将其替换为相应的验证 URL。

若要实现此目的，创建一个事件处理程序 CreateUserWizard [ `SendingMail`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx)并添加以下代码：

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample4.vb)]

`SendingMail`事件后会激发`CreatedUser`事件，这意味着，上述的事件处理程序执行新用户时已创建帐户。 我们就可以访问新用户的`UserId`值通过调用`Membership.GetUser`方法，传入`UserName`CreateUserWizard 控件中输入。 接下来，将形成的验证 URL。 该语句`Request.Url.GetLeftPart(UriPartial.Authority)`返回`http://yourserver.com`一部分而定。`Request.ApplicationPath`返回应用程序的根节点位置的路径。 验证 URL 然后定义为`Verification.aspx?ID=userId`。 然后将其连接这两个字符串以形成完整的 URL。 最后，将电子邮件正文 (`e.Message.Body`) 具有的所有匹配项`<%VerificationUrl%>`替换为完整的 URL。

实际效果是新用户未批准的这意味着它们不能登录到网站。 此外，它们将自动发送包含链接的电子邮件到的验证 URL （请参阅图 6）。


[![新用户会收到包含验证 URL 的链接的电子邮件](unlocking-and-approving-user-accounts-vb/_static/image17.png)](unlocking-and-approving-user-accounts-vb/_static/image16.png)

**图 6**： 新的用户会收到包含验证 URL 的链接的电子邮件 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image18.png))


> [!NOTE]
> CreateUserWizard 控件的默认 CreateUserWizard 步骤才会显示一条消息，告知的用户其帐户已创建并显示继续按钮。 单击此将用户转到由该控件的指定的 URL`ContinueDestinationPageUrl`属性。 在 CreateUserWizard`EnhancedCreateUserWizard.aspx`配置为发送新用户添加到`~/Membership/AdditionalUserInfo.aspx`，此时会提示用户输入其家乡，主页 URL 和签名。 因为此信息只能通过登录的用户，所以应该更新此属性，以向用户发送回站点的主页 (`~/Default.aspx`)。 此外，`EnhancedCreateUserWizard.aspx`应增加页面或 CreateUserWizard 步骤向用户通知它们已发送验证电子邮件和不会激活其帐户，直到它们按照此电子邮件中的说明。 我将这些修改作为练习留给读者。


### <a name="creating-the-verification-page"></a>创建验证页

最后一项任务是创建`Verification.aspx`页。 将此页添加到根文件夹，将其与`Site.master`母版页。 像我们所做的大部分添加到该站点在前面的内容页中，删除引用的内容控件`LoginContent`ContentPlaceHolder，以便内容页使用母版页的默认内容。

添加到标签 Web 控件`Verification.aspx`页上，将其`ID`到`StatusMessage`并将清除其 text 属性。 接下来，创建`Page_Load`事件处理程序并添加以下代码：

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample5.vb)]

上面的代码中的大容量会验证是否通过在查询字符串提供的用户 Id 存在，它是一个有效`Guid`值和它引用现有的用户帐户。 如果所有这些检查通过，批准的用户帐户;否则，将显示一条合适的状态消息。

图 7 显示了`Verification.aspx`页上通过浏览器访问时。


[![新用户的帐户是现在批准](unlocking-and-approving-user-accounts-vb/_static/image20.png)](unlocking-and-approving-user-accounts-vb/_static/image19.png)

**图 7**: 新用户的帐户是现在批准 ([单击以查看实际尺寸的图像](unlocking-and-approving-user-accounts-vb/_static/image21.png))


## <a name="summary"></a>总结

所有成员资格用户帐户具有确定用户可以登录到网站的两种状态：`IsLockedOut`和`IsApproved`。 两个属性必须是`True`该用户的登录名。

用户的锁定状态用作一种安全措施以减少黑客通过暴力破解方法到站点中断的可能性。 具体而言，用户被锁定是否存在一定数量的特定的时间窗口内的无效登录尝试。 这些边界是通过中的成员资格提供程序设置可配置`Web.config`。

已批准的状态通常用作一种方法来禁止新用户登录，直到某项操作已发生的情况。 站点可能需要先由管理员批准的新帐户或与我们在步骤 3 中看到通过验证其电子邮件地址。

快乐编程 ！

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](recovering-and-changing-passwords-vb.md)
