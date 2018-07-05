---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成员身份 |Microsoft Docs
author: microsoft
description: ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。 ASP.NET 窗体身份验证提供了方便的方式，以 incorp...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ebba0c25fd3c7d6de7182c14559add7902cafe83
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388391"
---
<a name="membership"></a>成员资格
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。 ASP.NET 窗体身份验证提供了方便地将一个登录窗体合并到 ASP.NET 应用程序和对针对数据库或其他数据存储区的用户进行验证。


ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。 ASP.NET 窗体身份验证提供了方便地将一个登录窗体合并到 ASP.NET 应用程序和对针对数据库或其他数据存储区的用户进行验证。 FormsAuthentication 类的成员，使其可以处理身份验证的 cookie，检查有效的登录名，登录将用户注销等。但是，在 ASP.NET 1.x 应用程序中实现窗体身份验证可能需要大量的代码。

在 ASP.NET 2.0 中的成员身份是通过使用单独的窗体身份验证的主要优势。 （成员身份是最可靠与窗体身份验证结合使用时，但使用 Forms 身份验证并不要求）。正如您很快就会看到，您可以使用 ASP.NET Membership 和 login 控件在 ASP.NET 2.0 中根本无需太多的代码实现功能强大的成员身份系统。

## <a name="implementing-membership-in-aspnet-20"></a>在 ASP.NET 2.0 中实现的成员身份

由以下四个步骤实现的成员身份。 请记住，有许多子步骤也可以实现的可选配置以及所涉及的。 这些步骤是为了说明配置成员身份的大图片。

1. 创建成员资格数据库 （如果 SQL Server 用作成员资格存储区。）
2. 在应用程序配置文件中指定的成员身份选项。 （成员身份已启用默认情况下。）
3. 确定你想要使用的成员身份存储的类型。 选项包括： 

    - Microsoft SQL Server （版本 7.0 或更高版本）
    - Active Directory 存储
    - 自定义成员资格提供程序
4. 配置 ASP.NET 窗体身份验证的应用程序。 再次重申，成员资格旨在利用的窗体身份验证，但使用 Forms 身份验证不是一项要求。
5. 定义成员资格的用户帐户并根据需要配置角色。

## <a name="creating-the-membership-database"></a>创建成员资格数据库

如果您正在使用 SQL Server 7.0 或更高版本作为成员身份存储，可以使用 aspnet\_regsql 实用程序 （可非常轻松地从 Visual Studio.NET 2005年命令提示符） 将数据库配置。 Aspnet\_regsql 实用程序可以在命令提示符工具或通过 GUI 向导。 向导方法是将数据库配置的最简单方法。 若要访问该向导，只需运行以下命令：

`aspnet_regsql W`

一旦运行该命令时，还能使用 ASP.NET SQL Server 安装向导，如下所示。


![](membership/_static/image1.jpg)

**图 1**


ASP.NET SQL Server 安装向导在向导中指定的实例中创建该网站。 但是，ASP.NET 将使用连接字符串在 machine.config 文件中连接到你的数据库。 默认情况下，此连接字符串将指向的 SQL Server 2005 实例，因此如果使用的 SQL Server 2000 或 SQL Server 7.0 实例，您将需要修改 machine.config 文件中的连接字符串。 此处可以找到该连接字符串：

[!code-xml[Main](membership/samples/sample1.xml)]

遗憾的是，如果你无需修改连接字符串，ASP.NET 将不为您提供描述性错误。 它只需将继续抱怨说尚未创建数据库。 在上面的示例中，我已修改为指向我的本地 SQL Server 2000 实例的连接字符串。

## <a name="specifying-configuration-and-adding-users-and-roles"></a>指定配置和添加用户和角色

配置成员身份的下一步是将所需的信息添加到应用程序的 web.config 文件。 在 ASP.NET 1.x 中，修改 web.config 文件是有时很难由于 lowerCamelCase 使用和缺少的 Intellisense。 Visual Studio.NET 2005年使任务更容易通过 Intellisense 配置文件，但 ASP.NET 2.0 更进一步通过编辑配置文件的提供的 Web 界面。

可以通过单击在解决方案资源管理器工具栏上，如下所示的 ASP.NET 配置按钮来启动 Web 界面。 此外可以启动的登录名控件插入时，将显示弹出式窗口通过 Web 界面。


![](membership/_static/image2.jpg)

**图 2**


这将启动 ASP.NET 网站管理工具如下所示。 ASP.NET 网站管理是一个四个选项卡界面，它可以更轻松地管理应用程序设置。 提供了以下选项卡：

- **主文件夹**
- **安全**配置用户、 角色和访问权限。
- **应用程序**配置应用程序设置。
- **提供程序**配置和测试应用程序成员资格提供程序。

网站管理工具，可以轻松地创建新用户，创建新的角色，以及管理用户和角色。 在 Windows 界面中不提供此功能。 Windows 界面允许您可以轻松地定义授权设置要添加、 删除和管理提供程序，无法在网站管理工具中的功能。

若要启动 Windows 界面，打开 Internet Information Services 管理单元、 应用程序中，右键单击并选择属性。 单击 ASP.NET 选项卡，然后单击编辑配置按钮。 （若要启用编辑配置按钮的 ASP.NET 2.0 下必须运行该应用程序。 你可以配置 ASP.NET 版本在 ASP.NET 对话框。）如下所示，将显示 ASP.NET 配置设置对话框。


![](membership/_static/image3.jpg)

**图 3**


在常规选项卡上列出连接字符串和应用程序设置。 在父配置文件 （machine.config 或更高级别的 web.config） 中定义以斜体显示的任何设置，不以斜体显示的设置是从应用程序配置文件。 如果添加一个设置，已删除或编辑应用程序级别中，ASP.NET 将添加、 删除或修改在应用程序级别 web.config 而不是从它继承的配置文件中删除该设置的设置。

身份验证选项卡如下所示。 这是在将配置你的成员身份设置。 窗体身份验证设置，成员资格提供程序，并在此处配置角色提供程序。


![](membership/_static/image4.jpg)

**图 4**


## <a name="implementing-membership-in-your-application"></a>在你的应用程序中实现的成员身份

在你的应用程序中实现 ASP.NET 2.0 成员身份的最简单方法是使用提供的登录控件。 此方法可以实现 ASP.NET 2.0 成员身份的基础知识，而无需编写任何代码。

以下的登录控件是 ASP.NET 2.0 中提供：

## <a name="login-control"></a>Login 控件

Login 控件提供一个接口，使用户能够登录到成员资格系统。 你提供用户名和密码 textboxt 和登录按钮。 许多其他常见功能，如将其注册为那些尚未做这样一个复选框，允许在后续的访问会自动登录到用户的用户的链接、 密码提示等的链接。登录名控件的所有功能都都可自定义通过控件的属性。

在 ASP.NET 1.x 中，开发人员必须编写大量的代码以使用窗体身份验证时执行搜索。 ASP.NET 2.0 成员身份，你可以对用户进行验证而无需编写任何代码。 ASP.NET 会自动为您执行用户执行的查找。 (如果不使用 ASP.NET 成员资格将登录控件，则可以使用**OnAuthenticate**方法来验证用户。)

## <a name="loginview-control"></a>LoginView 控件

LoginView 控件是默认情况下; 提供两个模板的模板化控件AnonymousTemplate 和 LoggedInTemplate。 用户登录到成员资格系统确定将显示该模板。 此控件通常用于显示登录控件时，用户尚未登录，LoginStatus 控件和/或其他登录控件，当用户已登录。 如果在 ASP.NET 应用程序中使用角色管理，LoginView 控件可显示特定的模板基于用户角色。 （更多关于 ASP.NET 角色管理将在后面。）

## <a name="passwordrecovery-control"></a>PasswordRecovery 控件

PasswordRecovery 控件允许用户收到电子邮件，其当前密码或重置其密码。 明文和加密的密码可以恢复并通过电子邮件发送给用户。 如果密码哈希处理，它不能恢复。 而是用户将需要执行密码重置。

## <a name="loginstatus-control"></a>登录状态控件

LoginStatus 控件用于显示当前登录的用户未登录的用户的登录名指示器和注销指示器。 Request.IsAuthenticated 属性用于确定要显示的指示器。 LoginStatus 控件显示的指示器可以是文本 (通过实现**LoginText**并**LogoutText**属性) 或图像 (通过实现**LoginImageUrl**并**LogoutImageUrl**属性。)

当用户注销通过 LoginStatus 控件时，他或她将重定向到指定的 URL **LogoutPageUrl**属性。 如果未设置该属性，会刷新当前页。 站点可能受窗体身份验证，因为当前页的刷新将用户重定向到该站点的登录页。

## <a name="loginname-control"></a>登录名控件

LoginName 控件显示当前已登录到该站点的用户的用户名。

## <a name="createuserwizard-control"></a>CreateUserWizard 控件

CreateUserWizard 控件为用户提供注册成员身份系统的简便方法。 你可以通过如下所示的接口添加步骤 （实现为一系列 WizardSteps）。


![](membership/_static/image5.jpg)

**图 5**


CreateUserWizard 是模板化控件，用于从向导类派生并提供以下模板：

- **HeaderTemplate**此模板控制向导的标头的外观。
- **SidebarTemplate**此模板控制向导边栏的外观。
- **StartNavigationTemplate**导航的外观是在开始步骤向导的此模板控件。
- **StepNavigationTemplate**此模板控制在不启动或完成步骤时的导航区域的外观。
- **FinishNavigationTemplate**此模板控制时在完成步骤的导航区域的外观。

此外，对于每个添加到向导的步骤，ASP.NET 将创建包含 ContentTemplate 和为该步骤 CustomNavigationTemplate 的自定义模板。 自定义 CreateUserWizard 的完整详细信息，请参阅 VS.NET 2005 文档：

## <a name="changepassword-control"></a>ChangePassword 控件

ChangePassword 控件允许用户更改其密码。 如果 DisplayUserName 属性为 true （它是默认值为 false），用户可以更改其密码时不将它们记录。 如果用户*是*已登录和 DisplayUserName 属性为 true，用户将能够更改不记录在提供他们知道该用户的用户 ID 的另一个用户的密码。

请记住，如果你希望用户能够更改密码，而无需登录，你将需要确保 ChangePassword 控件显示在其的页面允许匿名访问。 显然，用户将必须提供旧密码，以更改其密码。

## <a name="role-management"></a>角色管理

角色管理，可将用户分配到特定角色，然后限制对某些文件或文件夹基于该角色的访问。 角色管理还提供了一个 API，以便可以以编程方式确定，方便用户角色或确定特定角色中的所有用户并相应地做出响应。

角色管理不是在 ASP.NET 成员资格要求也不是为了使用角色管理要求的成员身份。 但是，这两个很好地补充彼此并很可能，开发人员会使用它们与相互结合使用。

若要启用应用程序中的角色管理，请在 web.config 文件中进行以下更改：

[!code-xml[Main](membership/samples/sample2.xml)]

当**cacheRolesInCookie**属性设置为 true，ASP.NET 缓存客户端的 cookie 中的用户角色成员身份。 这允许角色查找，以调入 RoleProvider 的情况下发生。 使用此属性时，建议，请确保开发人员将**cookieProtection**属性设置为 All。 （这是默认设置。）这可确保 cookie 数据进行加密，并有助于确保 cookie 内容尚未更改。 可以使用网站管理工具添加角色。 它允许您轻松地定义角色、 配置的访问权限的基于这些角色的站点部分并将用户分配到角色。


![](membership/_static/image6.jpg)

**图 6**


如上所示，可以通过只需输入角色的名称，然后单击添加角色添加新的角色。 可以管理或通过单击相应的链接的现有角色列表中删除现有角色。

当你管理角色时，可以添加或删除用户，如下所示。


![](membership/_static/image7.jpg)

**图 7**


通过检查用户属于角色复选框，可以轻松地将用户添加到特定角色中。 使用适当的项，ASP.NET 将自动更新成员资格数据库。 此外需要配置你的应用程序的访问规则。 ASP.NET 1.x 开发人员都熟悉通过这样做&lt;授权&gt;web.config 文件中，该选项中的元素是在 ASP.NET 2.0 中仍然可用。 但是，轻松地管理访问权限的规则使用网站管理工具如图所示下面。


![](membership/_static/image8.jpg)

**图 8**


在这种情况下，突出显示管理文件夹 （将很难看到，因为该工具使其突出显示以浅灰色） 以及管理员角色是否已授予访问权限。 将拒绝所有其他用户。 您可以单击头图标以选择一个规则，然后使用上移和下移按钮来排列规则。 与 ASP.NET 一样&lt;授权&gt;元素，它们出现的顺序处理规则。 换而言之，如果上面截图中的规则的顺序已反转，没有人将可以访问对管理文件夹因为 ASP.NET 将会遇到的第一个规则将会拒绝所有人的文件夹的规则。

ASP.NET 2.0 将 web.config 文件添加到要为其指定访问规则的文件夹。 访问规则可以通过配置文件或通过网站管理工具进行编辑。 换而言之，网站管理工具是只需通过它可以在用户友好的环境中编辑配置文件的接口。

## <a name="using-roles-in-code"></a>在代码中使用角色

用于角色管理 API 一直没有更改版本 1.x。 **IsInRole**方法用于确定用户是否属于特定角色。

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET 还为当前上下文的成员创建 RolePrincipal 实例。 RolePrincipal 对象可用于获取所有给用户，如下所示所属的角色：

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>用 LoginView 控件使用 RoleGroups

现在，已了解角色管理和成员身份，让我们如何 LoginView 控件利用此功能在 ASP.NET 2.0 中简要讨论一下。 如前面所述，LoginView 控件是默认设置。 包含两个模板的模板化控件AnonymousTemplate 和 LoggedInTemplate。 在 LoginView 任务对话框是一个链接 （如下所示），您可以编辑 RoleGroups。


![](membership/_static/image9.jpg)

**图 9**


每个 RoleGroup 对象包含一个字符串数组，用于定义 RoleGroup 适用于哪些角色。 若要添加新 RoleGroup LoginView 控件，单击编辑 RoleGroups 链接。 在上图中，可以看到我已添加了新 RoleGroup 为管理员。 通过选择该 RoleGroup （RoleGroup[0]) 从视图下拉列表中，我可以将模板配置的管理员角色的成员才会显示。 在下图中，我添加了适用于 Sales 角色和分发角色的成员的新 RoleGroup。 这会向登录视图任务对话框中的视图下拉列表中添加第二个 RoleGroup 而不显示任何内容添加到该模板中的销售或分发的任何用户角色。


![](membership/_static/image10.jpg)

**图 10**


## <a name="overriding-the-existing-membership-provider"></a>重写现有成员资格提供程序

有两种方法可以扩展的 ASP.NET 成员资格功能。 首先，您可以通过从它继承和重写其方法显然更改 SqlMembershipProvider 类的现有功能。 例如，如果你想要实现您自己的功能创建用户时，可以创建自己的类继承自 SqlMembershipProvider，如下所示：

[!code-csharp[Main](membership/samples/sample5.cs)]

如果，但是，你想要创建自己的提供程序 （用于存储成员资格信息在访问数据库中，例如所示），可以创建自己的提供程序。

## <a name="creating-your-own-membership-provider"></a>创建你自己的成员资格提供程序

若要创建你自己的成员资格提供程序，首先需要创建一个继承自 MembershipProvider 类的类。 如果正在使用 VB.NET，Visual Studio 2005 将添加所有需要重写的方法存根。 如果使用的 C#，则取决于您要添加存根 （stub）。

你将需要重写以下：

- 应用程序名称属性
- ChangePassword 函数
- ChangePasswordQuestionAndAnswer 函数
- CreateUser 函数
- DeleteUser 函数
- EnablePasswordReset 属性
- EnablePasswordRetrieval 属性
- FindUsersByEmail 函数
- FindUsersByName 函数
- GetAllUsers 函数
- GetNumberOfUsersOnline 函数
- GetPassword 函数
- GetUser 函数
- GetUserNameByEmail 函数
- MaxInvalidPasswordAttempts 属性
- MinRequiredNonAlphanumericCharacters 属性
- MinRequiredPasswordLength 属性
- PasswordAttemptWindow 属性
- PasswordFormat 属性
- PasswordStrengthRegularExpression 属性
- RequiresQuestionAndAnswer 属性
- RequiresUniqueEmail 属性
- ResetPassword 函数
- 解锁用户函数
- UpdateUser 函数
- ValidateUser 函数

这会很多列表作为 C# 开发人员来实现。 您可能会发现更轻松地在 VB.NET 中创建类，而无需任何实现，然后使用.NET Reflector 或类似的工具将代码转换为 C#。

连接字符串和其他属性应设置为它们的 Initialize 方法中的默认值。 （Initialize 方法时触发的提供程序是在运行时加载。）Initialize 方法的第二个参数的类型 System.Collections.Specialized.NameValueCollection 和是对的引用&lt;添加&gt;与您的 web.config 文件中的自定义提供程序相关联的元素。 该条目如下所示：

[!code-xml[Main](membership/samples/sample6.xml)]

下面是 Initialize 方法的示例。

[!code-csharp[Main](membership/samples/sample7.cs)]

若要验证用户在提交登录窗体时，你将需要使用 ValidateUser 方法。 当用户单击登录控件中的登录按钮时，会触发此方法。 会将你的代码执行此方法中的用户查找。

如您所见，编写你自己的成员资格提供程序并不困难，并可以扩展此强大的功能的 ASP.NET 2.0。
