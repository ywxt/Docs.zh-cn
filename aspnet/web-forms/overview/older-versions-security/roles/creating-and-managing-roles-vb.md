---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
title: 创建和管理角色 (VB) |Microsoft Docs
author: rick-anderson
description: 本教程探讨配置角色 framework 的所需的步骤。 接下来，我们将构建 web 页以创建和删除角色。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: 83af9f5f-9a00-4f83-8afc-e98bdd49014e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
msc.type: authoredcontent
ms.openlocfilehash: fbcd8613327ada581289ce613b5d0e0a09df4e19
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386609"
---
<a name="creating-and-managing-roles-vb"></a>创建和管理角色 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.09.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_vb.pdf)

> 本教程探讨配置角色 framework 的所需的步骤。 接下来，我们将构建 web 页以创建和删除角色。


## <a name="introduction"></a>介绍

在中<a id="_msoanchor_1"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程中我们介绍了使用 URL 授权页面的一组限制某些用户，并探讨了声明性和调整基于来访的用户的 ASP.NET 页面的功能的编程技术。 授予权限的访问页或基于用户的用户的功能，但是，可能会变得噩梦方案中的有多个用户帐户或经常更改用户的权限。 任何时候用户获得或失去授权来执行特定任务中，管理员需要更新相应的 URL 授权规则、 声明性标记和代码。

通常最好先对用户进行分类为组或*角色*，然后应用基于角色的角色的权限。 例如，大多数 web 应用程序具有一组特定页面或保留仅供管理用户的任务。 在中使用的技术学习*基于用户的授权*教程中，我们将添加相应的 URL 授权规则、 声明性标记和代码，以允许指定的用户帐户以执行管理任务。 但如果已添加新的管理员或现有的管理员需要能够撤消其管理权限，则必须返回并更新配置文件和网页。 使用角色，但是，我们无法创建名为管理员角色并将这些受信任的用户分配到管理员角色。 接下来，我们将添加相应的 URL 授权规则、 声明性标记和代码，以允许管理员角色才能执行各种管理任务。 使用此基础结构，向站点添加新的管理员或删除现有只需包括或从管理员角色中删除用户。 无需配置、 声明性标记或代码更改是必需的。

ASP.NET 还提供了用于定义角色，并将其与用户帐户关联的角色框架。 我们可以创建和删除角色的角色框架，添加用户或从角色中删除用户，请确定一组属于特定角色，并告知用户是否属于特定角色的用户。 一旦配置了角色框架，我们可以限制对页 URL 授权规则通过基于角色的角色的访问和显示或隐藏的其他信息或基于当前登录的用户的角色页面上的功能。

本教程探讨配置角色 framework 的所需的步骤。 接下来，我们将构建 web 页以创建和删除角色。 在中<a id="_msoanchor_2"> </a> [*向用户分配角色*](assigning-roles-to-users-vb.md)教程我们将介绍如何添加和删除用户角色中。 然后在<a id="_msoanchor_3"> </a> [*基于角色的授权*](role-based-authorization-vb.md)教程中我们将了解如何限制对页以及如何调整页面功能根据基于角色的角色的访问正在访问用户的角色。 让我们进入正题！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤 1： 添加新的 ASP.NET 页面

我们将在本教程并下一步的两个检查各种与角色相关的函数和功能。 我们将需要一系列的 ASP.NET 页面实现检查在这些教程中的主题。 让我们来创建这些页面和更新的站点映射。

首先，创建一个新的文件夹在项目中名为`Roles`。 接下来，添加到四个新的 ASP.NET 页面`Roles`文件夹中，链接与每个页面`Site.master`母版页。 命名页：

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

此时您的项目的解决方案资源管理器应类似于屏幕截图中图 1 所示。


[![四个新页面已添加到角色文件夹](creating-and-managing-roles-vb/_static/image2.png)](creating-and-managing-roles-vb/_static/image1.png)

**图 1**： 四个新页已添加到`Roles`文件夹 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image3.png))


每个页面，此时，应有两个内容控件，另一个用于每个母版页的 Contentplaceholder:`MainContent`和`LoginContent`。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample1.aspx)]

请记住， `LoginContent` ContentPlaceHolder 的默认标记将显示在登录或注销的站点，具体取决于是否对用户进行身份验证的链接。 是否存在`Content2`内容控件在 ASP.NET 页中，但是，重写主页面的默认标记。 如中所述<a id="_msoanchor_4"> </a> [*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-vb.md)教程中，重写默认标记很有用，我们不希望显示登录相关的页面中左侧列中的选项。

对于这四个页面，但是，我们想要显示的主页面的默认标记`LoginContent`ContentPlaceHolder。 因此，删除的声明性标记`Content2`内容控件。 执行此操作之后, 每四个页面的标记应只包含一个内容控件。

最后，让我们更新站点图 (`Web.sitemap`) 以包括这些新的 web 页面。 添加以下 XML 之后`<siteMapNode>`我们添加了成员身份的教程。

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample2.xml)]

使用更新的站点映射，请访问通过浏览器的站点。 如图 2 所示，在左侧的导航窗格现在为角色教程包括项。


[![四个新页面已添加到角色文件夹](creating-and-managing-roles-vb/_static/image5.png)](creating-and-managing-roles-vb/_static/image4.png)

**图 2**： 四个新页已添加到`Roles`文件夹 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image6.png))


## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>步骤 2： 指定和配置角色框架提供程序

成员资格框架，如角色框架构建提供程序模型之上。 如中所述<a id="_msoanchor_5"> </a> [*安全基础知识和 ASP.NET 支持*](../introduction/security-basics-and-asp-net-support-vb.md)教程中，.NET Framework 附带有三个内置角色提供程序： [ `AuthorizationStoreRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx)[ `WindowsTokenRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)，和[ `SqlRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)。 本系列教程重点介绍`SqlRoleProvider`，它使用 Microsoft SQL Server 数据库作为角色存储。

幕后的角色框架和`SqlRoleProvider`就像成员资格框架工作和`SqlMembershipProvider`。 .NET Framework 包含`Roles`类，充当的角色框架的 API。 `Roles`类具有共享方法，如`CreateRole`， `DeleteRole`， `GetAllRoles`， `AddUserToRole`， `IsUserInRole`，依次类推。 调用下列方法之一时，`Roles`类将调用委托给配置的提供程序。 `SqlRoleProvider`适用于特定于角色的表 (`aspnet_Roles`和`aspnet_UsersInRoles`) 响应中。

若要使用`SqlRoleProvider`我们的应用程序中的提供程序，我们需要指定什么数据库用作在存储区。 `SqlRoleProvider`预期要有特定的数据库表、 视图和存储的过程的指定的角色存储区。 可以使用添加这些必要的数据库对象[`aspnet_regsql.exe`工具](https://msdn.microsoft.com/library/ms229862.aspx)。 现在我们已有具有所需架构的数据库`SqlRoleProvider`。 回到<a id="_msoanchor_6"> </a> [ *SQL Server 中创建成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-vb.md)教程中，我们创建一个名为数据库`SecurityTutorials.mdf`并用`aspnet_regsql.exe`添加该应用程序服务，包括所需的数据库对象`SqlRoleProvider`。 因此我们只需告诉角色框架以启用角色支持，并使用`SqlRoleProvider`与`SecurityTutorials.mdf`作为角色存储的数据库。

角色框架中，通过配置`<roleManager>`元素在应用程序的`Web.config`文件。 默认情况下，禁用角色支持。 若要启用它，必须设置[ `<roleManager>` ](https://msdn.microsoft.com/library/ms164660.aspx)元素的`enabled`属性为`true`如下所示：

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample3.xml)]

默认情况下，所有 web 应用程序都具有名为角色提供程序`AspNetSqlRoleProvider`类型的`SqlRoleProvider`。 此默认提供程序中注册`machine.config`(位于`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample4.xml)]

提供程序的`connectionStringName`属性指定使用角色存储区。 `AspNetSqlRoleProvider`提供程序将此属性设置为`LocalSqlServer`，这也是在`machine.config`和点，默认情况下，到中的 SQL Server 2005 Express Edition 数据库`App_Data`文件夹名为`aspnet.mdf`。

因此，如果我们只需启用角色框架未在我们的应用程序中指定的任何提供程序信息`Web.config`文件，该应用程序使用已注册的默认角色提供程序， `AspNetSqlRoleProvider`。 如果`~/App_Data/aspnet.mdf`数据库不存在，ASP.NET 运行时将自动创建并添加应用程序服务架构。 但是，我们不想要使用`aspnet.mdf`数据库; 而是，我们想要使用`SecurityTutorials.mdf`我们已经创建并添加到应用程序服务架构的数据库。 此修改可以在两种方式之一完成：

- <strong>为指定值</strong><strong>`LocalSqlServer`</strong><strong>中的连接字符串名称</strong><strong>`Web.config`</strong><strong>。</strong> 通过覆盖`LocalSqlServer`中的连接字符串名称值`Web.config`，我们可以使用已注册的默认角色提供程序 (`AspNetSqlRoleProvider`)，并将其正确处理`SecurityTutorials.mdf`数据库。 有关此技术的详细信息，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[配置为使用 SQL Server 2000 或 SQL Server 2005 ASP.NET 2.0 应用程序服务](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>添加新注册的提供程序类型</strong><strong>`SqlRoleProvider`</strong><strong>并配置其</strong><strong>`connectionStringName`</strong><strong>设置以指向</strong><strong>`SecurityTutorials.mdf`</strong><strong>数据库。</strong> 这是我建议，在中使用的方法<a id="_msoanchor_7"> </a> [ *SQL Server 中创建成员身份架构*](../membership/creating-the-membership-schema-in-sql-server-vb.md)教程中，它是我在本教程还将使用的方法。

添加到以下角色配置标记`Web.config`文件。 此标记将注册为的新提供程序 `SecurityTutorialsSqlRoleProvider.`

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample5.xml)]

上述标记定义`SecurityTutorialsSqlRoleProvider`作为默认提供程序 (通过`defaultProvider`属性中`<roleManager>`元素)。 它还设置`SecurityTutorialsSqlRoleProvider`的`applicationName`将设置为`SecurityTutorials`，这是相同`applicationName`成员资格提供程序所使用的设置 (`SecurityTutorialsSqlMembershipProvider`)。 虽然未在此处，显示[`<add>`元素](https://msdn.microsoft.com/library/ms164662.aspx)有关`SqlRoleProvider`还可能包含`commandTimeout`属性来指定数据库超时持续时间，以秒为单位。 默认值为 30。

与此配置标记中的位置，我们已做好开始使用我们的应用程序中的角色功能。

> [!NOTE]
> 上面的配置标记说明了如何使用`<roleManager>`元素的`enabled`和`defaultProvider`属性。 有多种影响角色框架如何将基于用户的用户角色信息相关联的其他属性。 我们将检查这些设置<a id="_msoanchor_8"> </a> [*基于角色的授权*](role-based-authorization-vb.md)教程。


## <a name="step-3-examining-the-roles-api"></a>第 3 步： 检查角色 API

角色框架的功能已通过公开[`Roles`类](https://msdn.microsoft.com/library/system.web.security.roles.aspx)，其中包含十三个共享的方法，用于执行基于角色的操作。 当我们介绍创建和删除步骤 4 中的角色，6 我们将运用[ `CreateRole` ](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx)并[ `DeleteRole` ](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx)方法，这将添加或从系统中删除角色。

若要获取系统中的所有角色的列表，请使用[`GetAllRoles`方法](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)（请参阅第 5 步）。 [ `RoleExists`方法](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx)返回一个布尔值，该值指示是否存在指定的角色。

在下一教程中，我们将说明如何将用户与角色相关联。 `Roles`类的[ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)， [ `AddUserToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx)， [ `AddUsersToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)，和[ `AddUsersToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx)方法将一个或多个用户添加到一个或多个角色。 若要从角色中删除用户，请使用[ `RemoveUserFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)， [ `RemoveUserFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx)， [ `RemoveUsersFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)，或[ `RemoveUsersFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx)方法。

在中<a id="_msoanchor_9"> </a> [*基于角色的授权*](role-based-authorization-vb.md)我们将看看如何以编程方式显示或隐藏基于当前登录的用户的角色功能的教程。 若要实现此目的，我们可以使用角色类的[ `FindUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx)， [ `GetRolesForUser` ](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)， [ `GetUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)，或[ `IsUserInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)方法。

> [!NOTE]
> 请注意，调用这些方法之一的任何时间，`Roles`类将调用委托给配置的提供程序。 在本例中，这意味着发送到调用`SqlRoleProvider`。 `SqlRoleProvider`然后执行相应的数据库操作基于调用的方法。 例如，代码`Roles.CreateRole("Administrators")`会导致`SqlRoleProvider`执行`aspnet_Roles_CreateRole`存储过程，将插入新记录到`aspnet_Roles`表名为管理员。


本教程的其余部分介绍使用`Roles`类的`CreateRole`， `GetAllRoles`，和`DeleteRole`方法来管理系统中的角色。

## <a name="step-4-creating-new-roles"></a>步骤 4： 创建新的角色

角色提供给任意组用户，一种方法，通常这种分组用于更方便的方式来应用授权规则。 但是，为了将用作我们首先需要定义在应用程序中有哪些角色的授权机制的角色。 遗憾的是，ASP.NET 没有包含 CreateRoleWizard 控件。 若要添加新角色，我们需要创建一个合适的用户界面和自己调用角色 API。 好消息是，这是很容易实现。

> [!NOTE]
> 虽然没有任何 CreateRoleWizard Web 控件，但没有[ASP.NET 网站管理工具](https://msdn.microsoft.com/library/ms228053.aspx)，这是本地 ASP.NET 应用程序，旨在帮助进行查看和管理 web 应用程序的配置。 但是，我并不非常热衷于 ASP.NET 网站管理工具有两个原因。 首先，有些错误并且用户体验离开还有很大。 其次，ASP.NET 网站管理工具旨在仅在本地运行，这意味着需要构建你自己的角色管理网页，如果需要远程管理在实时站点上的角色。 有关这两个原因，本教程，下一步将重点介绍在网页中的管理工具生成必要的角色，而不是依赖于 ASP.NET 网站管理工具。


打开`ManageRoles.aspx`页中`Roles`文件夹并向页面添加一个文本框和按钮 Web 控件。 设置 TextBox 控件`ID`属性设置为`RoleName`和按钮的`ID`并`Text`属性设置为`CreateRoleButton`和创建角色，分别。 在此情况下，页面的声明性标记应类似以下：

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample6.aspx)]

接下来，双击`CreateRoleButton`按钮在设计器中创建的控件`Click`事件处理程序，然后添加以下代码：

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample7.vb)]

上面的代码首先会将修整的角色名称中输入`RoleName`文本框中的为`newRoleName`变量。 下一步，`Roles`类的`RoleExists`方法调用以确定如果角色`newRoleName`系统中已存在。 如果角色不存在，则创建它通过调用`CreateRole`方法。 如果`CreateRole`方法将传递在系统中，已存在的角色名称`ProviderException`引发异常。 这就是原因代码首先检查以确保该角色已中不存在之前调用系统`CreateRole`。 `Click`事件处理程序通过清除结束`RoleName`文本框的`Text`属性。

> [!NOTE]
> 您可能想知道会发生什么情况如果用户没有输入任何值`RoleName`文本框中。 如果将值传递到`CreateRole`方法是`Nothing`或空字符串，异常引发。 同样，如果角色名称包含逗号被引发异常。 因此，页应包含验证控制措施来确保用户输入一个角色，并且它不包含任何逗号。 我将留给读者作为练习。


让我们创建一个名为管理员角色。 请访问`ManageRoles.aspx`通过浏览器页上，在管理员键入到文本框 （请参见图 3），然后单击创建角色按钮。


[![创建管理员角色](creating-and-managing-roles-vb/_static/image8.png)](creating-and-managing-roles-vb/_static/image7.png)

**图 3**： 创建管理员角色 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image9.png))


会发生什么情况？ 产生的回发，但没有任何视觉提示，角色实际上已被添加到系统。 我们将更新以包括可视反馈的步骤 5 中的此页面。 现在，但是，您可以验证是否已通过转到创建角色`SecurityTutorials.mdf`数据库和数据的`aspnet_Roles`表。 如图 4 所示，`aspnet_Roles`表包含一条记录为刚添加管理员角色。


[![Aspnet_Roles 表中有一行管理员](creating-and-managing-roles-vb/_static/image11.png)](creating-and-managing-roles-vb/_static/image10.png)

**图 4**:`aspnet_Roles`表具有一个行管理员 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image12.png))


## <a name="step-5-displaying-the-roles-in-the-system"></a>步骤 5： 显示系统中的角色

让我们来增强`ManageRoles.aspx`页以包含在系统中的当前角色的列表。 若要完成此操作，向页添加 GridView 控件并设置其`ID`属性设置为`RoleList`。 接下来，将方法添加到页面的代码隐藏类名为`DisplayRolesInGrid`使用以下代码：

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample8.vb)]

`Roles`类的`GetAllRoles`方法返回的所有角色在系统中作为一个字符串数组。 此字符串数组，然后绑定到 GridView。 为了将角色列表绑定到 GridView，首次加载页面时，我们需要调用`DisplayRolesInGrid`方法从页面的`Page_Load`事件处理程序。 当首次访问页面，但不是在后续回发，以下代码将调用此方法。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample9.vb)]

利用此代码，请访问通过浏览器页面。 图 5 所示，你应该看到一个网格，包含单个列标记为项。 网格包含我们在步骤 4 中添加的管理员角色的行。


[![GridView 显示单个列中的角色](creating-and-managing-roles-vb/_static/image14.png)](creating-and-managing-roles-vb/_static/image13.png)

**图 5**: GridView 显示单个列中的角色 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image15.png))


GridView 显示单个列标记为项，因为 GridView`AutoGenerateColumns`属性设置为 True （默认值），这会导致 GridView 自动创建一个列中每个属性及其`DataSource`。 数组具有一个属性，即表示 GridView 中的单个列的数组，因此中的元素。

显示与 GridView 数据时，我喜欢显式定义我的专栏，而不将它们隐式生成的 GridView。 通过显式定义列是更轻松地设置数据的格式、 重新排列这些列和执行其他常见任务。 因此，让我们更新 GridView 的声明性标记，以便其列显式定义如此。

首先设置 GridView 的`AutoGenerateColumns`属性设置为 False。 接下来，将为 TemplateField 添加到网格中，设置其`HeaderText`属性设置为角色，并配置其`ItemTemplate`，以便它将显示数组的内容。 若要完成此操作，将添加一个名为标签 Web 控件`RoleNameLabel`到`ItemTemplate`，并将绑定其`Text`属性 `Container.DataItem.`

这些属性和`ItemTemplate`的内容可以设置以声明方式或通过 GridView 的字段对话框和编辑模板接口。 若要访问字段对话框中，单击 GridView 的智能标记中的编辑列链接。 接下来，取消选中自动生成字段复选框以设置`AutoGenerateColumns`属性设置为 False，并将 TemplateField 添加到 GridView，设置其`HeaderText`到角色的属性。 若要定义`ItemTemplate`的内容，从 GridView 的智能标记中选择编辑模板选项。 将标签 Web 控件拖到`ItemTemplate`，请将其`ID`属性设置为`RoleNameLabel`，并配置其数据绑定设置，以便其`Text`属性绑定到`Container.DataItem`。

无论您使用什么方法，GridView 的所得的声明性标记应类似于以下完成后。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample10.aspx)]

> [!NOTE]
> 数组的内容将显示使用数据绑定语法`<%# Container.DataItem %>`。 显示数组的内容绑定到 GridView 时为什么要使用此语法的详尽描述不在本教程的范围。 有关此问题的详细信息，请参阅[标量数组绑定到数据 Web 控件](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)。


目前， `RoleList` GridView 只绑定到的角色列表，当首次访问页面时。 我们需要添加新角色时刷新该网格。 若要完成此操作，更新`CreateRoleButton`按钮的`Click`事件处理程序以便调用`DisplayRolesInGrid`方法如果创建新的角色。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample11.vb)]

现在当用户添加新角色`RoleList`GridView 显示刚添加的角色在回发时，提供视觉反馈已成功创建该角色。 若要说明这一点，请访问`ManageRoles.aspx`通过浏览器页上，添加名为在监督器的角色。 单击创建角色按钮，为在回发将会随之发生和网格将更新以包括管理员以及新角色，在监督器。


[![在监督器角色具有已添加](creating-and-managing-roles-vb/_static/image17.png)](creating-and-managing-roles-vb/_static/image16.png)

**图 6**: 在监督器角色具有已添加 ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image18.png))


## <a name="step-6-deleting-roles"></a>步骤 6： 删除角色

现在用户可以创建新的角色并查看中的所有现有角色`ManageRoles.aspx`页。 让我们允许用户删除角色。 `Roles.DeleteRole`方法有两个重载：

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -删除该角色*roleName*。 如果角色包含一个或多个成员，将引发异常。
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -删除该角色*roleName*。 如果*throwOnPopulateRole*是`True`，则该角色包含一个或多个成员而引发异常。 如果*throwOnPopulateRole*是`False`，则它或不包含任何成员是否删除此角色。 在内部，`DeleteRole(roleName)`方法调用`DeleteRole(roleName, True)`。

`DeleteRole`方法也将引发异常，如果*roleName*是`Nothing`或空字符串或者，如果*roleName*包含逗号。 如果*roleName*不在系统中，存在`DeleteRole`失败以无提示方式，并且不会引发异常。

让我们来增强 GridView 中的`ManageRoles.aspx`包括一个删除按钮，单击时，将删除所选的角色。 首先通过转到字段对话框并添加一个删除按钮，位于 CommandField 选项下将删除按钮添加到 GridView。 请删除按钮左侧的列，然后设置其`DeleteText`属性设置为删除的角色。


[![将删除按钮添加到 RoleList GridView](creating-and-managing-roles-vb/_static/image20.png)](creating-and-managing-roles-vb/_static/image19.png)

**图 7**： 添加到一个删除按钮`RoleList`GridView ([单击以查看实际尺寸的图像](creating-and-managing-roles-vb/_static/image21.png))


以后将添加删除按钮，GridView 的声明性标记看起来应类似于下面：

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample12.aspx)]

接下来，为 GridView 的创建事件处理程序`RowDeleting`事件。 这是单击删除角色按钮时，在回发时引发的事件。 将以下代码添加到该事件处理程序中。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample13.vb)]

代码将开始通过以编程方式引用`RoleNameLabel`Web 控件中的删除角色按钮被单击的行。 `Roles.DeleteRole`然后调用方法，并传入`Text`的`RoleNameLabel`和`False`，从而删除该角色，而不管是否有任何与角色关联的用户。 最后， `RoleList` GridView 刷新，以便只删除角色不会再出现在网格中。

> [!NOTE]
> 删除角色按钮不需要用户确认删除该角色之前的任何排序。 若要确认某项操作的最简单方法之一是通过客户端的确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-vb.aspx)。


## <a name="summary"></a>总结

许多 web 应用程序具有特定的授权规则或页级别仅可供特定类别的用户的功能。 例如，可能有一组只有管理员才可以访问的 web 页面。 而不是基于用户的用户定义这些授权规则，通常很多有用来定义基于角色的规则。 也就是说，而不是显式允许用户访问管理网页，Scott 并 Jisun，更易于维护的方法是，允许管理员角色的成员访问这些页面，然后分别表示为属于用户 Scott 和 Jisun管理员角色。

角色框架轻松创建和管理角色。 在本教程中介绍了如何配置要使用的角色框架`SqlRoleProvider`，它使用 Microsoft SQL Server 数据库作为角色存储。 我们还创建一个网页，列出了系统中的现有角色，并允许创建的新角色和现有功能，可删除。 在后续教程中我们将看到如何将用户分配到角色以及如何将应用基于角色的授权。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [检查 ASP.NET 2.0 的成员资格、 角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何： 在 ASP.NET 2.0 中使用角色管理器](https://msdn.microsoft.com/library/ms998314.aspx)
- [角色提供程序](https://msdn.microsoft.com/library/aa478950.aspx)
- [滚动你自己的网站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [技术文档`<roleManager>`元素](https://msdn.microsoft.com/library/ms164660.aspx)
- [使用成员资格和角色管理器 Api](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者包括 Alicja Maziarz、 Suchi Banerjee 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](role-based-authorization-cs.md)
> [下一页](assigning-roles-to-users-vb.md)
