---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: 针对成员身份用户存储区 (VB) 验证用户凭据 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将说明如何验证用户的凭据针对的成员身份用户存储中使用的编程方法和 Login 控件...
ms.author: aspnetcontent
ms.date: 01/18/2008
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: c5eeb67c8d175173f38ffcbc1b01fd5a5931866e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821399"
---
<a name="validating-user-credentials-against-the-membership-user-store-vb"></a>针对成员身份用户存储区 (VB) 验证用户凭据
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip)或[下载 PDF](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> 在本教程中，我们将说明如何验证根据使用的编程方法和 Login 控件的成员身份用户存储区的用户的凭据。 我们还将介绍如何自定义登录控件的外观和行为。


## <a name="introduction"></a>介绍

在中<a id="Tutorial05"> </a>[前面的教程](creating-user-accounts-vb.md)探讨了如何在成员资格框架中创建新的用户帐户。 我们首先介绍了以编程方式创建用户帐户通过`Membership`类的`CreateUser`方法，并使用 CreateUserWizard Web 控件然后检查。 但是，登录页当前验证提供的凭据与硬编码的用户名和密码对的列表。 我们需要更新登录页面的逻辑，以便验证针对成员资格框架的用户存储的凭据。

更像创建用户帐户，可以验证凭据以编程方式或以声明方式。 成员资格 API 包括用于以编程方式验证用户的凭据对用户存储区的方法。 和 ASP.NET 附带了登录 Web 控件，用于呈现具有文本框用于用户名和密码和一个按钮，用于登录的用户界面。

在本教程中，我们将说明如何验证根据使用的编程方法和 Login 控件的成员身份用户存储区的用户的凭据。 我们还将介绍如何自定义登录控件的外观和行为。 让我们进入正题！

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>步骤 1： 验证针对成员身份用户存储的凭据

对于使用 forms 身份验证的网站，用户登录到网站访问登录页并输入其凭据。 然后，对用户存储比较这些凭据。 如果它们是有效，然后向用户授予窗体身份验证票证，这是一个安全标记，指示的标识和访问者的真实性。

若要验证对成员资格框架用户，请使用`Membership`类的[`ValidateUser`方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)。 `ValidateUser`方法采用两个输入参数的`username`和`password`-并返回指示凭据有效的布尔值。 与处理方式一样`CreateUser`方法在上一教程中，我们探讨`ValidateUser`方法委托实际验证到已配置的成员资格提供程序。

`SqlMembershipProvider`验证所提供的凭据通过获取指定的用户的密码通过`aspnet_Membership_GetPasswordWithFormat`存储过程。 请记住，`SqlMembershipProvider`存储用户的密码使用三种格式之一： 清除，加密的或进行哈希处理。 `aspnet_Membership_GetPasswordWithFormat`存储的过程返回的密码以其原始格式。 对于加密或哈希密码，`SqlMembershipProvider`转换`password`值传递到`ValidateUser`方法转换成其等效加密或哈希处理状态，然后将其与从数据库返回的内容是。 如果在数据库中存储的密码与用户输入的格式化的密码匹配，凭据有效。

让我们更新我们的登录页面 (~ /`Login.aspx`)，以便验证成员资格框架用户存储区对提供的凭据。 我们创建了此登录页回到<a id="Tutorial02"> </a> [*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-vb.md)教程中，使用两个文本框输入用户名和密码，创建一个接口记住我复选框，并登录按钮 （请参阅图 1）。 代码验证输入的凭据与硬编码的用户名和密码对 （Scott/密码、 Jisun/密码和 Sam/密码） 的列表。 在中<a id="Tutorial03"> </a> [*窗体身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)教程，我们更新了登录页面的代码以在窗体中存储的其他信息身份验证票证`UserData`属性。


[![登录页面的接口包含两个文本框、 CheckBoxList 和一个按钮](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**图 1**: 登录页面的接口包括两个文本框、 CheckBoxList 和一个按钮 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png))


登录页的用户界面可保持不变，但我们需要将登录按钮为`Click`验证成员资格框架用户存储区对用户代码与事件处理程序。 更新事件处理程序，使其代码如下所示：

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

此代码是非常简单。 我们首先调用`Membership.ValidateUser`方法，传入提供的用户名和密码。 如果该方法将返回 True，则用户登录到的站点通过`FormsAuthentication`类的 RedirectFromLoginPage 方法。 (如中所述<a id="Tutorial02"> </a> [*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-vb.md)教程中，`FormsAuthentication.RedirectFromLoginPage`创建窗体身份验证票证，然后将用户重定向适当的页。）如果凭据无效，但是，`InvalidCredentialsMessage`显示标签，则通知用户其用户名或密码不正确。

这就是一切就这么简单 ！

若要测试登录页按预期方式工作，请尝试使用在前面的教程中创建的用户帐户之一登录。 或者，如果尚未创建一个帐户，请继续并创建一个从`~/Membership/CreatingUserAccounts.aspx`页。

> [!NOTE]
> 当用户输入其凭据并将在登录页表单提交时，通过 Internet 到 web 服务器中传输凭据，包括她的密码，*纯文本*。 这意味着任何探查的网络流量的黑客可以看到的用户名和密码。 若要防止此情况，是必须使用加密的网络流量[安全套接字层 (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)。 这将确保从那一刻起，它们将保留在浏览器，直到 web 服务器接收加密的凭据 （以及整个页面的 HTML 标记）。


### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>成员资格框架如何处理无效的登录尝试次数

当在访问者达到登录页，并提交其凭据时，其浏览器发出 HTTP 请求到登录页。 如果凭据有效，HTTP 响应将包括在 cookie 中的身份验证票证。 因此，黑客试图进入你的站点无法创建彻底将 HTTP 请求发送到包含有效的用户名和密码猜测的登录页的程序。 如果密码猜测值正确无误，请登录页将返回身份验证票证 cookie，此时该程序知道它有偶然发现有效的用户名/密码对。 通过暴力破解此类程序可能能够发现用户的密码，尤其是在弱密码时。

若要防止此类暴力破解攻击，成员资格框架锁定用户是否存在一定数量的一段时间内的失败登录尝试。 确切的参数是可通过以下两个成员资格提供程序配置设置配置：

- `maxInvalidPasswordAttempts` -指定多少次无效密码尝试在该帐户锁定前的时间段内只允许用户。默认值为 5。
- `passwordAttemptWindow` -指示以分钟为单位指定无效的登录尝试次数将在此期间导致帐户被锁定的时间段。默认值为 10。

如果用户已锁定，她不能登录直到管理员解除锁定她的帐户。 当用户锁定`ValidateUser`方法将*始终*返回`False`，即使在提供有效凭据。 虽然此行为可以减少黑客通过暴力破解方法将为你的站点中断的可能性，则它可能出现锁定只是忘记了密码或意外大写锁定或有错误的类型化一天的有效用户。

遗憾的是，没有内置工具用于解锁用户帐户。 若要解锁帐户，可以修改数据库直接-更改`IsLockedOut`字段中`aspnet_Membership`相应的用户帐户中的表或创建一个基于 web 的界面，其中列出了锁定的并且可以选择解锁帐户。 我们将检查创建的管理接口，用于在以后的教程中实现常见的用户帐户和角色相关任务。

> [!NOTE]
> 一个缺点`ValidateUser`方法是，所提供的凭据无效时，它不提供任何说明，解释原因。 凭据可能无效，原因是未匹配的用户名/密码对在用户存储中，或因为用户尚未批准，或者因为用户锁定。在步骤 4 中，我们将了解如何在其登录尝试失败时向用户显示更详细的消息。


## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>步骤 2： 收集凭据通过登录 Web 控件

[登录 Web 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)呈现非常类似于我们在回复中创建的一个默认用户界面<a id="Tutorial02"> </a> [*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-vb.md)教程。 使用登录控件为我们节省的无需创建要收集的访问者的凭据的接口的工作。 此外，登录控件会自动登录用户 （假设已提交的凭据有效），从而节省了我们无需编写任何代码。

让我们更新`Login.aspx`、 替换手动创建的接口和与登录控件编写代码。 首先删除现有标记和代码中`Login.aspx`。 可能会删除彻底，或只需注释掉。注释掉声明性标记，可以使用与其周围`<%--`和`--%>`分隔符。 可以手动输入这些分隔符，或如图 2 所示，可以选择要添加注释，然后单击工具栏中的选定的行图标注释的文本。 同样，可以使用注释掉的选定的行图标注释掉的代码隐藏类中的所选代码。


[![注释掉的现有声明性标记和 login.aspx 的情况中的源代码](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**图 2**： 注释掉现有声明性标记和 login.aspx 的情况中的源代码 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png))


> [!NOTE]
> 在 Visual Studio 2005 中查看的声明性标记时，注释掉的选定的行图标不可用。 如果不使用 Visual Studio 2008 将需要手动添加`<%--`和`--%>`分隔符。


接下来，从工具箱拖到页上将登录控件，然后设置其`ID`属性设置为`myLogin`。 此时您的屏幕应类似于图 3。 请注意，登录名控件的默认接口包括用于用户名和密码，下次记住我复选框，和一个日志中按钮的文本框控件。 此外，还有`RequiredFieldValidator`的两个文本框控件。


[![将登录控件添加到页面](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**图 3**： 将登录控件添加到页 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png))


大功告成 ！ 单击登录控件的登录按钮时，会发生回发和登录控件将调用`Membership.ValidateUser`方法，传入的输入的用户名和密码。 如果凭据无效，该登录名控件将显示一条消息表明此类。 但是，如果凭据有效，然后登录控件创建窗体身份验证票证，并将用户重定向到相应的页面。

Login 控件使用四个因素来确定合适的页面重定向到用户成功登录后：

- Login 控件是否登录页上定义的`loginUrl`设置在窗体身份验证配置中，此设置的默认值是 `Login.aspx`
- 是否存在`ReturnUrl`查询字符串参数
- 登录名控件的值[`DestinationUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)
- `defaultUrl`中窗体身份验证配置设置指定的值; 此设置的默认值为 Default.aspx

图 4 展示了如何登录控件使用以下四个参数以获得其相应的页决策。


[![将登录控件添加到页面](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**图 4**： 将登录控件添加到页 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png))


请花费片刻时间测试登录控件通过访问的站点通过浏览器并作为成员资格框架中的现有用户登录。

登录名控件的呈现的接口是高度可配置。 有多种会影响它的外观; 的属性更重要的是，Login 控件可转换为精确地对布局控件的模板的用户界面元素。 此步骤的其余部分探讨如何自定义外观和布局。

### <a name="customizing-the-login-controls-appearance"></a>自定义登录控件的外观

登录名控件的默认属性设置呈现以标题 （日志） 的用户界面，为用户名和密码输入，记住我的 TextBox 和 Label 控件下次复选框和一个登录按钮。 这些元素的外观是所有可配置通过登录名控件的许多属性。 此外，可以通过设置的属性或两个添加附加用户界面元素-例如，若要创建新的用户帐户的页面的链接。

让我们花一些时间才能 gussy 向上我们登录控件的外观。 由于`Login.aspx`的页面已具有显示登录页顶部的文本、 登录控件的标题是多余。 因此，清除[`TitleText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx)值，以便删除登录名控件的标题。

用户名: 和密码： 可以通过自定义的两个 TextBox 控件左侧标签[ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx)并[`PasswordLabelText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)分别。 让我们更改用户名： 标签读取 Username:。 是通过可配置的标签和文本框样式[ `LabelStyle` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx)并[`TextBoxStyle`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)分别。

记住我可以通过登录控件设置下一步时间复选框的文本属性[`RememberMeText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)，并且其默认检查状态是可通过配置[`RememberMeSet`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx)（其默认值为 False）。 继续操作并设置`RememberMeSet`将默认情况下选中属性设置为 True，以便记住我下次复选框。

Login 控件提供了两个调整其用户界面控件的布局的属性。 [ `TextLayout`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)指示是否用户名: 和密码： 标签显示在左侧的其对应的文本框 （默认值），或更高版本它们。 [ `Orientation`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)指示的用户名和密码输入是否垂直位置 （上下一个） 或水平。 我打算保留这两个属性设置为其默认值，但我建议您尝试将这两个属性设置为其非默认值，以查看产生的效果。

> [!NOTE]
> 在下一步部分中，配置登录名控件的布局中，我们将介绍如何使用模板来定义精确布局控件的用户界面元素的布局。


通过设置登录名控件的属性设置进行总结[ `CreateUserText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx)和[`CreateUserUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx)为 Not 尚未注册？ 创建一个帐户 ！ 和`~/Membership/CreatingUserAccounts.aspx`分别。 这将超链接添加到登录控件的接口中创建指向页面<a id="Tutorial05"> </a>[前面的教程](creating-user-accounts-vb.md)。 Login 控件[ `HelpPageText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx)并[`HelpPageUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx)并[ `PasswordRecoveryText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx)和[ `PasswordRecoveryUrl` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)即可在同样的方式呈现帮助页和密码恢复页的链接。

这些属性更改后，请登录控件的声明性标记和外观应类似于图 5 中所示。


[![登录名控件的属性值指示其外观](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**图 5**: 登录名控件的属性值指示其外观 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png))


### <a name="configuring-the-login-controls-layout"></a>配置登录名控件的布局

登录 Web 控件的默认用户界面布局中对应的 HTML 界面`<table>`。 但是，如果我们需要更好地控制呈现的输出？ 我们想要替换的也许`<table>`使用一系列`<div>`标记。 或者，如果我们的应用程序需要其他凭据进行身份验证？ 很多财务网站，例如，要求用户提供不仅用户名和密码，但还个人标识号 (PIN) 或其他标识信息。 无论原因可能包括，则可以登录控件转换为模板，在其中我们可以显式定义接口的声明性标记。

我们需要做两件事，以更新要收集其他凭据的登录控件：

1. 更新登录名控件的界面，包括 Web 控件包装要收集的其他凭据。
2. 重写登录控件内部身份验证逻辑，以便用户只能进行身份验证，如果其用户名和密码有效，并且也是有效的其其他凭据。

若要完成的第一个任务，我们需要登录控件转换为模板并添加所需的 Web 控件。 与第二个任务，则可以通过创建控件的事件处理程序取代登录控件的身份验证逻辑[`Authenticate`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)。

让我们更新登录控件，使其提示用户输入其用户名、 密码和电子邮件地址，并仅验证用户身份如果提供的电子邮件地址与在文件上的其电子邮件地址相匹配。 我们首先需要将登录名控件的界面转换为模板。 从登录名控件的智能标记，选择转换为模板选项。


[![将登录控件转换为模板](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**图 6**： 将登录控件转换为模板 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png))


> [!NOTE]
> 若要还原到其预先 template 版本登录控件，单击该控件的智能标记中的重置链接。


将登录控件转换为模板将添加`LayoutTemplate`到控件的声明性标记的 HTML 元素和定义用户界面的 Web 控件。 如图 7 所示，将控件转换为模板中删除多个属性从属性窗口中，如`TitleText`， `CreateUserUrl`，依此类推，因为使用模板时，将忽略这些属性值。


[![更少的属性都是可用的时登录控件转换为模板](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**图 7**： 较少的属性是可用的时登录控件转换为模板 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png))


中的 HTML 标记`LayoutTemplate`可根据需要修改。 同样，随意向模板添加任何新的 Web 控件。 但是，很重要，该登录名控件的核心 Web 控件保留在该模板，并保留其分配`ID`值。 具体而言，不要删除或重命名`UserName`或`Password`文本框中，`RememberMe`复选框，`LoginButton`按钮，`FailureText`标签，或`RequiredFieldValidator`控件。

若要收集的访问者的电子邮件地址，我们需要向模板添加一个文本框。 添加以下声明性标记表行之间 (`<tr>`)，其中包含`Password`文本框和接下来保存记住我的表行的时间复选框：

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

添加后`Email`文本框中，请访问通过浏览器页面。 如图 8 所示，登录名控件的用户界面现在包括第三个文本框。


[![Login 控件现在包括用户的电子邮件地址的文本框](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**图 8**： 登录控件现在包括用户的电子邮件地址的文本框 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png))


此时，Login 控件仍在使用`Membership.ValidateUser`方法来验证所提供的凭据。 相应地，在输入值`Email`文本框中不存在任何上用户可以登录。 在步骤 3 中，我们将介绍如何重写登录控件的身份验证逻辑，以便凭据仅被视为有效的用户名和密码有效且提供的电子邮件地址与在文件上的电子邮件地址匹配如果。

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>步骤 3： 修改登录名控件的身份验证逻辑

时访问者提供其凭据并单击登录按钮，为在回发时，才会和登录名来控制其身份验证工作流中的进行处理时。 工作流开始时引发[`LoggingIn`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)。 与此事件关联的任何事件处理程序可通过设置取消操作中的日志`e.Cancel`属性设置为`True`。

如果在操作中的日志不会被取消，工作流执行过程通过引发[`Authenticate`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)。 如果没有事件处理程序`Authenticate`事件，然后它负责确定提供的凭据是否有效。 如果不指定任何事件处理程序，则该登录名控件使用`Membership.ValidateUser`方法，以确定所提供的凭据的有效性。

如果提供的凭据是否有效，则创建窗体身份验证票证时， [ `LoggedIn`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx)引发，并且用户重定向到相应的页。 如果，但是，凭据被视为无效，则[`LoginError`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx)引发并且显示一条消息，通知用户其凭据无效。 默认情况下，在失败时该登录名控件只需设置其`FailureText`标签控件 Text 属性绑定到 （您登录尝试未成功失败消息。 请重试）。 但是，如果登录名控件的[`FailureAction`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx)设置为`RedirectToLoginPage`，然后登录控件问题`Response.Redirect`追加查询字符串参数的登录页到`loginfailure=1`（这将导致该登录名控件以显示失败消息）。

图 9 提供身份验证工作流流程图。


[![登录名控件的身份验证工作流](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**图 9**: 登录名控件的身份验证工作流 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png))


> [!NOTE]
> 如果想知道何时将使用`FailureAction`的`RedirectToLogin`页选项，请考虑以下方案。 现在我们`Site.master`母版页当前已显示的文本，大家好，stranger 时由匿名用户访问过的左侧列中，但假设我们想要该文本替换为登录控件。 这将允许匿名用户可以从任意页上的站点，而无需直接访问登录页登录。 但是，如果用户不能通过登录控件呈现母版页的登录，可能会有用重定向到登录页 (`Login.aspx`) 因为该页面可能包含其他说明、 链接和其他帮助-例如，若要创建的链接新的帐户或检索的丢失密码的未被添加到母版页。


### <a name="creating-theauthenticateevent-handler"></a>创建`Authenticate`事件处理程序

若要插入到我们的自定义身份验证逻辑中，我们需要创建登录控件的事件处理程序`Authenticate`事件。 创建的事件处理程序`Authenticate`事件将生成以下事件处理程序定义：

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

正如您所看到的`Authenticate`事件处理程序传递类型的对象[ `AuthenticateEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx)作为其第二个输入参数。 `AuthenticateEventArgs`类包含名为的布尔属性`Authenticated`，用于指定所提供的凭据是否有效。 我们的任务，然后，是编写代码，用于确定所提供的凭据是否有效，并设置`e.Authenticate`属性相应地。

### <a name="determining-and-validating-the-supplied-credentials"></a>确定并验证所提供的凭据

使用登录控件[ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx)并[`Password`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx)来确定用户输入的用户名和密码凭据。 若要确定任何其他 Web 控件中输入的值 (如`Email`我们在上一步中添加的文本框)，使用`LoginControlID.FindControl`("*`controlID`*") 来获取对 Web 的编程引用控件模板中`ID`属性等于*`controlID`*。 例如，若要获取对引用`Email`文本框中，使用以下代码：

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

若要验证用户的凭据，我们需要做两件事：

1. 请确保提供的用户名和密码有效
2. 确保输入的电子邮件地址与在用户尝试登录的文件中的电子邮件地址相匹配

若要完成第一次检查我们只需使用`Membership.ValidateUser`像我们在步骤 1 中看到的方法。 第二个检查中，我们需要确定用户的电子邮件地址，以便我们可以将其它们输入到 TextBox 控件的电子邮件地址进行比较。 若要获取特定用户的信息，请使用`Membership`类的[`GetUser`方法](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)。

`GetUser`方法有许多重载。 如果使用未传入任何参数，则返回有关当前已登录用户的信息。 若要获取特定用户的信息，请调用`GetUser`传递其用户名中。 无论哪种方式`GetUser`返回[`MembershipUser`对象](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)，其中包含属性，如`UserName`， `Email`， `IsApproved`， `IsOnline`，依次类推。

下面的代码实现这些两个检查。 如果两者都通过，然后`e.Authenticate`设置为`True`，否则它分配`False`。

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

利用此代码，尝试以输入正确的用户名、 密码和电子邮件地址的有效用户身份登录。 重试，但这次特意使用不正确的电子邮件地址 （请参阅图 10）。 最后，它尝试使用不存在用户名的第三个时间。 在第一种情况下您应已成功登录到站点，但在最后两个情况下应会看到登录控件的凭据无效消息。


[![提供不正确的电子邮件地址时，Tito 无法登录。](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**图 10**: Tito 无法日志中时提供不正确的电子邮件地址 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png))


> [!NOTE]
> 步骤 1 中的如何成员资格框架处理无效登录尝试部分中所述时`Membership.ValidateUser`方法调用并传递凭据无效，它跟踪的无效的登录尝试并锁定用户，如果它们超出某一特定指定的时间范围内的无效尝试的阈值。 因为我们自定义身份验证逻辑调用`ValidateUser`方法中，有效的用户名不正确的密码将无效的登录尝试使计数器递增，但此计数器中的用户名和密码是否有效，这种情况不会增加，但电子邮件地址不正确。 很可能，此行为很合适，因为不太可能黑客会知道用户名和密码，但必须使用暴力破解技术来确定用户的电子邮件地址。


## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>步骤 4： 提高登录控件的凭据无效消息

当用户尝试使用无效凭据登录时，登录名，将显示一条消息说明的登录尝试不成功。 具体而言，该控件显示由指定的消息及其[`FailureText`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)，其中包含默认值为您的登录尝试未成功。 请重试。

回想一下，原因有很多原因，用户的凭据可能无效：

- 用户名可能不存在
- 用户名已存在，但密码为无效
- 用户名和密码有效，但用户尚未批准
- 用户名和密码是否有效，但用户被锁定在扩展 （最可能是因为它们超出了指定的时间范围内的无效的登录尝试次数）

和使用自定义身份验证逻辑时可能会由于其他原因。 例如，代码，我们编写了在步骤 3 中，用户名和密码可能有效，但可能不正确的电子邮件地址。

无论原因的凭据是无效登录名控件显示相同的错误消息。 这种反馈的缺乏容易混淆的帐户尚未批准或已锁定用户的用户。借助极少量的工作，不过，我们可以登录控件显示更合适的消息。

每当用户尝试使用无效凭据登录控件引发登录其`LoginError`事件。 请继续并创建此事件的事件处理程序并添加以下代码：

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

上面的代码首先会设置登录名控件的`FailureText`属性设置为默认值 （您的登录尝试未成功。 请重试）。 然后检查以查看是否提供的用户名将映射到现有的用户帐户。 如果因此，它会查询得到`MembershipUser`对象的`IsLockedOut`和`IsApproved`属性来确定帐户是否已被锁定，或尚未批准。 在任一情况下，`FailureText`属性更新为相应的值。

若要测试此代码，有意尝试记录作为现有用户，但使用了错误的密码。 在 10 分钟时间范围内的行中执行操作这五次，该帐户将被锁定。如图 11 所示，后续登录尝试将始终失败 （即使使用正确的密码），但现在将显示更具描述性的显示你的帐户已锁定由于无效的登录尝试次数太多。 请与管理员联系以具有您的帐户解锁的消息。


[![Tito 执行无效的登录尝试次数太多，并且已被锁定](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**图 11**: Tito 执行太多个无效登录尝试，并具有已锁定 ([单击以查看实际尺寸的图像](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png))


## <a name="summary"></a>总结

先前本教程中，我们登录页验证的用户名/密码对的硬编码列表针对提供的凭据。 在本教程中，我们更新了页面来验证凭据对成员资格框架。 在步骤 1 中我们介绍了使用`Membership.ValidateUser`方法以编程方式。 在步骤 2 中我们替换为我们的手动创建的用户界面和代码登录控件。

Login 控件呈现标准登录名的用户界面，并会自动验证成员资格框架针对用户的凭据。 此外，在发生时有效的凭据，登录控件让用户登录通过窗体身份验证。 简单地说，完全正常运行的登录名的用户体验通过只需将登录控件拖到一个页面、 没有额外的声明性标记或所需的代码是可用。 什么是多个，登录控件是高度可自定义，允许精细地控制呈现的用户界面和身份验证逻辑。

此时我们的网站访问者可以创建新的用户帐户和日志到站点，但我们还未查看限制对页基于经过身份验证的用户的访问。 目前，任何用户经过身份验证或匿名的可以在我们的网站上查看的任何页面。 以及控制对我们网页基于用户的用户的访问，我们可能有它的功能取决于用户的特定页。 下一步的教程讨论如何限制访问和在页根据登录用户的功能。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [显示自定义消息到锁定和未经批准的用户](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [检查 ASP.NET 2.0 的成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何： 创建 ASP.NET 登录页](https://msdn.microsoft.com/library/ms178331.aspx)
- [登录控制技术文档](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [使用登录控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者是 Teresa Murphy 和 Michael Olivero。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](creating-user-accounts-vb.md)
> [下一页](user-based-authorization-vb.md)
