---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: 创建用户帐户 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程将探讨如何使用成员资格框架 （通过 SqlMembershipProvider) 来创建新的用户帐户。 我们将了解如何创建新我们...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: c7f5f4ec6ce27c1a52569e6414b8f96892f68574
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834140"
---
<a name="creating-user-accounts-vb"></a>创建用户帐户 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip)或[下载 PDF](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> 在本教程将探讨如何使用成员资格框架 （通过 SqlMembershipProvider) 来创建新的用户帐户。 我们将了解如何以编程方式和通过 ASP 创建新用户。NET 的内置的 CreateUserWizard 控件。


## <a name="introduction"></a>介绍

在中<a id="_msoanchor_1"> </a>[前面的教程](creating-the-membership-schema-in-sql-server-vb.md)我们在数据库中，添加表、 视图和存储过程所需的安装应用程序服务架构`SqlMembershipProvider`和`SqlRoleProvider`。 这创建了本系列教程的其余部分并需要基础结构。 在本教程将探讨如何使用成员资格框架 (通过`SqlMembershipProvider`) 来创建新的用户帐户。 我们将了解如何以编程方式和通过 ASP 创建新用户。NET 的内置的 CreateUserWizard 控件。

除了学习如何创建新的用户帐户，我们还需要更新我们首次在中创建的演示网站 *<a id="_msoanchor_2"> </a>[概述的窗体身份验证](../introduction/an-overview-of-forms-authentication-vb.md)* 教程，然后中增强 *<a id="_msoanchor_3"> </a>[窗体身份验证配置和高级主题](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 教程。 我们的演示 web 应用程序具有登录页面，用于验证针对硬编码用户名/密码对用户的凭据。 此外，`Global.asax`包括用于创建自定义代码`IPrincipal`和`IIdentity`身份验证的用户的对象。 我们将更新登录页后，可以验证成员资格框架针对用户的凭据，并删除自定义主体和标识逻辑。

让我们进入正题！

## <a name="the-forms-authentication-and-membership-checklist"></a>窗体身份验证和成员身份检查表

我们开始使用成员资格框架之前，让我们花点时间查看我们采取了来达到此限制的重要步骤。 使用与成员资格框架时`SqlMembershipProvider`需要在基于窗体的身份验证方案中，在 web 应用程序中实现成员资格功能之前执行以下步骤：

1. **启用基于表单的身份验证。** 如中所述 *<a id="_msoanchor_4"> </a>[概述的窗体身份验证](../introduction/an-overview-of-forms-authentication-vb.md)*，窗体身份验证启用通过编辑`Web.config`并设置`<authentication>`元素的`mode`属性为`Forms`。 启用窗体身份验证，每个传入请求将检查其用于*窗体身份验证票证*，其中，如果存在，标识请求者。
2. **将应用程序服务架构添加到相应的数据库。** 当使用`SqlMembershipProvider`我们需要将应用程序服务架构安装到数据库。 通常此架构添加到同一个数据库用于保存应用程序的数据模型。 *<a id="_msoanchor_5"> </a> [SQL Server 中创建成员身份架构](creating-the-membership-schema-in-sql-server-vb.md)* 教程介绍了使用`aspnet_regsql.exe`工具来实现此目的。
3. **自定义 Web 应用程序的设置以从步骤 2 中引用的数据库。** *SQL Server 中创建成员身份架构*教程介绍了两种方法配置 web 应用程序，以便`SqlMembershipProvider`将使用在步骤 2 中所选的数据库： 通过修改`LocalSqlServer`连接字符串名称;或通过将新注册的提供程序添加到成员资格框架提供程序的列表和自定义该新的提供程序以使用数据库从步骤 2。

当生成 web 应用程序使用的`SqlMembershipProvider`和基于窗体的身份验证，你将需要执行下列三个步骤才能使用`Membership`类或 ASP.NET 登录 Web 控件。 由于我们已在前面的教程中执行这些步骤，我们已准备好开始使用成员资格框架 ！

## <a name="step-1-adding-new-aspnet-pages"></a>步骤 1： 添加新的 ASP.NET 页面

我们将在本教程并下一步的三种检查各种与成员资格相关的函数和功能。 我们将需要一系列的 ASP.NET 页面实现检查在这些教程中的主题。 让我们来创建这些页面，然后站点地图文件`(Web.sitemap)`。

首先，创建一个新的文件夹在项目中名为`Membership`。 接下来，添加到五个新的 ASP.NET 页面`Membership`文件夹中，链接与每个页面`Site.master`母版页。 命名页：

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

此时您的项目的解决方案资源管理器应类似于屏幕截图中图 1 所示。


[![新的 5 个页面已添加到成员资格文件夹](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**图 1**： 五个新页已添加到`Membership`文件夹 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image3.png))


每个页面，此时，应有两个内容控件，另一个用于每个母版页的 Contentplaceholder:`MainContent`和`LoginContent`。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

请记住， `LoginContent` ContentPlaceHolder 的默认标记将显示在登录或注销的站点，具体取决于是否对用户进行身份验证的链接。 是否存在`Content2`内容控件，但是，将覆盖主页面的默认标记。 如中所述 *<a id="_msoanchor_6"> </a>[概述的窗体身份验证](../introduction/an-overview-of-forms-authentication-vb.md)* 教程中，这是在页中，我们不希望在左侧列中显示与登录相关的选项很有用。

对于这些的 5 个页面，但是，我们想要显示的主页面的默认标记`LoginContent`ContentPlaceHolder。 因此，删除的声明性标记`Content2`内容控件。 这样做之后，每个五个页面的标记应只包含一个内容控件。

## <a name="step-2-creating-the-site-map"></a>步骤 2： 创建站点图

除最普通的网站的所有需要实现某种形式的导航用户界面。 导航用户界面可能是一个简单的网站的各个部分的链接列表。 或者，这些链接可能排列成菜单或树视图。 作为页面开发人员创建导航用户界面是故事的一半。 我们还需要一些方法来以可维护且可更新的方式定义站点的逻辑结构。 新页会添加或删除现有页面，我们希望能够更新单个源的站点图-和具有跨站点的导航用户界面会反映这些修改。

-定义了站点地图和实现基于站点地图导航用户界面-这两个任务都能够轻松地完成得益于站点图 framework 和导航 Web 控件中添加了的 ASP.NET 2.0 版。 站点图框架允许开发人员定义站点图，然后通过编程 API 访问它 ( [ `SiteMap`类](https://msdn.microsoft.com/library/system.web.sitemap.aspx))。 包含导航 Web 控件的内置[菜单控件](https://msdn.microsoft.com/library/bz09dy46.aspx)，则[TreeView 控件](https://msdn.microsoft.com/library/3eafky27.aspx)，并[SiteMapPath 控件](https://msdn.microsoft.com/library/3eafky27.aspx)。

成员身份和角色的框架，如站点图 framework 构建之上[提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)。 站点地图提供程序类的任务是生成使用的内存中结构`SiteMap`永久性数据存储，如 XML 文件或数据库表中的类。 .NET Framework 附带的默认站点地图提供程序从 XML 文件读取站点地图数据 ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx))，这是我们将在本教程中使用的提供程序。 对于一些备用的站点地图提供程序实现，请参阅进一步读数部分在本教程末尾。

默认站点地图提供程序需要一个格式正确的 XML 文件，名为`Web.sitemap`存在的根目录。 因为我们要使用此默认提供程序，我们需要添加此类文件，并在相应的 XML 格式中定义的站点映射的结构。 若要添加文件时，右键单击解决方案资源管理器中的项目名称并选择添加新项。 从对话框中，选择要添加的类型名为的站点地图文件`Web.sitemap`。


[![添加一个名为项目的根目录下的 Web.sitemap 文件](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**图 2**： 添加名为文件`Web.sitemap`到项目的根目录 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image6.png))


XML 映射文件定义作为层次结构的网站的结构。 此层次结构的关系建模的体系通过 XML 文件中`<siteMapNode>`元素。 `Web.sitemap`必须开头`<siteMap>`准确地说有的父节点`<siteMapNode>`子。 此顶级`<siteMapNode>`元素表示层次结构中的根，并可能包含任意数目的子代节点。 每个`<siteMapNode>`元素必须包括`title`属性，可以根据需要包含`url`并`description`属性，等等; 每个非空`url`属性必须是唯一的。

输入以下 XML`Web.sitemap`文件：

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

更高版本的站点映射标记定义层次结构中图 3 所示。


[![站点图表示的分层导航结构](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**图 3**： 站点图表示的分层导航结构 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image9.png))


## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>步骤 3： 更新母版页以包括导航用户界面

ASP.NET 包括大量的与导航相关 Web 控件，用于设计用户界面。 其中包括菜单、 树视图和 SiteMapPath 控件。 菜单和 TreeView 控件呈现站点地图结构中一个菜单或树，分别而 SiteMapPath 显示显示了当前节点及其上级以及正在访问痕迹导航。 站点地图数据可以绑定到 Web 控件使用了 SiteMapDataSource 其他数据，可以通过以编程方式访问`SiteMap`类。

由于站点图 framework 和导航控件的全面讨论超出了本系列教程的范围，而不是花费时间编写我们自己的导航用户界面，让我们改为借用中使用我 *[在 ASP.NET 2.0 中使用数据](../../data-access/index.md)* 教程系列中，使用 Repeater 控件显示两个深度项目符号列表的导航链接，如图 4 中所示。

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>在左侧列中添加两个级别的链接列表

若要创建此接口，将添加到下面的声明性标记`Site.master`主页面的左侧栏其中文本 TODO： 菜单将转到此处...当前驻留。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

上述标记将绑定一个名为的 Repeater 控件`menu`到 SiteMapDataSource，它返回站点映射层次结构中定义`Web.sitemap`。 由于 SiteMapDataSource 控件[`ShowStartingNode`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx)设置为 False，就会开始返回站点地图的层次结构从主节点的后代。 Repeater 显示每个节点 （当前只是成员资格） 中`<li>`元素。 另一个，内部 Repeater 中将显示当前节点的子级嵌套的未排序列表。

图 4 显示了上述标记的呈现的输出与我们在步骤 2 中创建站点地图结构。 Repeater 呈现普通的未排序的列表的标记;在中定义的级联样式表规则`Styles.css`负责的审美情趣的布局。 有关上述标记的工作原理的更详细说明，请参阅[母版页和站点导航](https://asp.net/learn/data-access/tutorial-03-vb.aspx)教程。


[![导航用户界面是呈现使用嵌套的未排序列表](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**图 4**: 导航用户界面是呈现使用嵌套的未排序列表 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image12.png))


### <a name="adding-breadcrumb-navigation"></a>添加痕迹导航

除了左侧列中的链接列表，让我们还具有每个页面显示[痕迹导航](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)。 痕迹导航是快速向用户显示其站点层次结构中的当前位置的导航用户界面元素。 SiteMapPath 控件使用的站点映射框架来确定站点图中的当前页的位置，然后显示痕迹根据此信息。

具体而言，添加`<span>`到母版页的标头元素`<div>`元素，并设置新`<span>`元素的`class`痕迹导航属性。 (`Styles.css`类包含用于痕迹导航类的规则。)接下来，将 SiteMapPath 添加到此新`<span>`元素。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

图 5 显示了输出 SiteMapPath 访问时`~/Membership/CreatingUserAccounts.aspx`。


[![痕迹导航显示当前页，并将其站点中的上级映射](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**图 5**： 痕迹导航中显示当前页和其祖先站点地图中 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image15.png))


## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>步骤 4： 删除自定义主体和标识逻辑

在中 *<a id="_msoanchor_7"> </a>[窗体身份验证配置和高级主题](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 我们已了解如何将自定义主体和标识对象向经过身份验证的用户相关联的教程。 我们通过创建事件处理程序中的完成这`Global.asax`的应用程序`PostAuthenticateRequest`后触发的事件`FormsAuthenticationModule`已进行身份验证的用户。 在此事件处理程序中，我们取代`GenericPrincipal`并`FormsIdentity`通过添加的对象`FormsAuthenticationModule`与`CustomPrincipal`和`CustomIdentity`对象我们在该教程中创建。

而自定义主体和标识对象是在某些情况下，在大多数情况下很有用`GenericPrincipal`和`FormsIdentity`对象已足够。 因此，我认为有必要以返回到默认行为。 进行此更改通过删除或注释掉`PostAuthenticateRequest`事件处理程序或通过删除`Global.asax`完全文件。

> [!NOTE]
> 已注释掉或删除中的代码后`Global.asax`，需要将中的代码添加注释`Default.aspx's`强制转换的代码隐藏类`User.Identity`属性设置为`CustomIdentity`实例。


## <a name="step-5-programmatically-creating-a-new-user"></a>步骤 5： 以编程方式创建一个新用户

若要创建新的用户帐户通过使用成员资格 framework`Membership`类的[`CreateUser`方法](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)。 此方法的输入参数为用户名、 密码和其他与用户相关的字段。 在调用，它将新的用户帐户创建委托给配置成员资格提供程序，然后返回[`MembershipUser`对象](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)表示刚创建的用户帐户。

`CreateUser`方法有四个重载，每个接受不同数量的输入参数：

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

这些四个重载的区别收集的信息的量。 第一个重载，例如，需要只是用户名和密码的新用户帐户，而第二个还要求用户的电子邮件地址。

这些重载存在，因为创建新的用户帐户所需的信息取决于成员资格提供程序的配置设置。 在中 *<a id="_msoanchor_8"> </a> [SQL Server 中创建成员身份架构](creating-the-membership-schema-in-sql-server-vb.md)* 教程中的指定成员资格提供程序配置设置，我们探讨`Web.config`。 表 2 包含的配置设置的完整列表。

一个此类成员资格提供程序配置设置的影响什么`CreateUser`可能会使用重载是`requiresQuestionAndAnswer`设置。 如果`requiresQuestionAndAnswer`设置为`true`（默认值），则创建新的用户帐户时我们必须指定一个安全提示问题和答案。 如果用户需要重置或更改其密码，稍后会使用此信息。 具体而言，在该时间它们会显示的安全问题，他们必须输入正确的答案来重置或更改其密码。 因此，如果`requiresQuestionAndAnswer`设置为`true`，然后调用前两个`CreateUser`重载会引发异常，因为缺少的安全问题和答案。 由于我们的应用程序当前配置为需要安全问题和答案，我们将需要时以编程方式创建用户的使用后一种两个重载之一。

为了说明使用`CreateUser`方法，让我们创建一个用户界面，我们其中提示用户输入其名称、 密码、 电子邮件和预定义的安全问题的答案。 打开`CreatingUserAccounts.aspx`页中`Membership`文件夹并将以下 Web 控件添加到内容控件：

- 名为一个文本框 `Username`
- 名为的 TextBox `Password`，其`TextMode`属性设置为 `Password`
- 名为一个文本框 `Email`
- 一个名为标签`SecurityQuestion`使用其`Text`属性中清除
- 名为一个文本框 `SecurityAnswer`
- 名为的按钮`CreateAccountButton`其`Text`属性设置为创建用户帐户
- 名为的标签控件`CreateAccountResults`使用其`Text`属性中清除

此时您的屏幕应类似于屏幕截图中图 6 所示。


[![将各种 Web 控件添加到 CreatingUserAccounts.aspx 页](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**图 6**： 添加到各种 Web 控件`CreatingUserAccounts.aspx Page`([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image18.png))


`SecurityQuestion`标签和`SecurityAnswer`文本框旨在显示预定义的安全问题并收集用户的答案。 请注意，安全问题和答案存储基于用户的用户，因此可以以允许每个用户定义其自己的安全问题。 但是，对于此示例中我已决定使用一个通用安全问题，即： 您喜爱的颜色是什么？

若要实现此预定义的安全问题，请将一个常量添加到页面的代码隐藏类名为`passwordQuestion`，将其分配的安全问题。 然后，在`Page_Load`事件处理程序中，分配给此常量`SecurityQuestion`标签的`Text`属性：

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

接下来，创建的事件处理程序`CreateAccountButton'`s`Click`事件，并添加以下代码：

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

`Click`事件处理程序首先定义一个名为变量`createStatus`类型的[ `MembershipCreateStatus` ](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)。 `MembershipCreateStatus` 是一个枚举，指示状态的`CreateUser`操作。 例如，如果用户帐户创建成功，从而`MembershipCreateStatus`实例将被设置为值为`Success;`另一方面，如果操作失败，因为已存在具有相同的用户名的用户，它将设置为值`DuplicateUserName`. 在中`CreateUser`我们使用的重载，我们需要传递`MembershipCreateStatus`到方法的实例。 此参数设置为适当的值中`CreateUser`方法，并且我们可以在方法调用，以确定是否已成功创建用户帐户后检查其值。

在调用`CreateUser`，并传入`createStatus`即`Select Case`语句用于输出取决于值分配给相应的消息`createStatus`。 图 7 显示的输出时已成功创建一个新用户。 图 8 和 9 显示输出时不创建用户帐户。 在图 8 中，访问者输入了不符合密码强度要求拼成员资格提供程序的配置设置中的五个字母密码。 在图 9 中，访问者正在尝试使用现有的用户名 （图 7 中创建一个） 创建用户帐户。


[![新的用户帐户是已成功创建](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**图 7**: 新的用户帐户是已成功创建 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image21.png))


[![因为提供的密码强度太弱，不创建用户帐户](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**图 8**： 因为提供的密码强度太弱，不会创建用户帐户 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image24.png))


[![用户帐户是不创建是因为用户名是已在使用中](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**图 9**: 用户帐户是不创建是因为用户名是已在使用中的 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image27.png))


> [!NOTE]
> 您可能想知道如何确定成功或失败时使用的前两个之一`CreateUser`方法重载，都不具有类型的参数的`MembershipCreateStatus`。 这些前两个重载会引发[`MembershipCreateUserException`异常](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx)遇到故障时，其中包括[`StatusCode`属性](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx)类型的`MembershipCreateStatus`。


在创建后的几个用户帐户，验证是否已通过列出的内容来创建帐户`aspnet_Users`并`aspnet_Membership`中的表`SecurityTutorials.mdf`数据库。 如图 10 所示，我已添加了两个用户通过`CreatingUserAccounts.aspx`页： Tito 和 Bruce。


[![在成员资格用户存储区中有两个用户： Tito 和 Bruce](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**图 10**： 在成员资格用户存储区中有两个用户： Tito 和 Bruce ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image30.png))


成员身份用户存储现在包括 Bruce 和 Tito 的帐户的信息，我们尚未实现允许 Bruce 或 Tito 登录到该站点上的功能。 目前，`Login.aspx`验证用户的凭据硬编码的一组用户名/密码对-对它执行*不*验证针对成员资格框架提供的凭据。 现在查看中的新用户帐户`aspnet_Users`和`aspnet_Membership`表已经足够。 在下一步的教程中，  *<a id="_msoanchor_9"> </a>[验证用户凭据对成员身份用户存储](validating-user-credentials-against-the-membership-user-store-vb.md)*，我们将更新以验证针对成员身份存储的登录页。

> [!NOTE]
> 如果您看不到任何用户在你`SecurityTutorials.mdf`数据库，则可能是因为 web 应用程序正在使用默认成员资格提供程序， `AspNetSqlMembershipProvider`，其中使用`ASPNETDB.mdf`作为其用户存储区数据库。 若要确定是否该问题，请单击解决方案资源管理器中的刷新按钮。 如果名为的数据库`ASPNETDB.mdf`已添加到`App_Data`文件夹中，这是问题。 返回到的第 4 步 *<a id="_msoanchor_10"> </a> [SQL Server 中创建成员身份架构](creating-the-membership-schema-in-sql-server-vb.md)* 教程，了解如何正确配置成员资格提供程序的说明。


在大多数创建用户帐户方案、 访问者提供某些界面来输入其用户名、 密码、 电子邮件和其他重要信息、 在哪个点创建一个新帐户。 在此步骤中我们介绍了手动构建此类接口，则会看到如何使用`Membership.CreateUser`方法以编程方式添加新用户帐户基于用户的输入。 但是，我们的代码，只需创建新用户帐户。 它没有执行任何后续操作，例如用户访问刚创建的用户帐户，该站点中的日志记录，或在向用户发送确认电子邮件。 以下附加步骤将需要额外的代码中按钮的`Click`事件处理程序。

ASP.NET 附带了 CreateUserWizard 控件，用于处理用户帐户创建过程中，从呈现用于创建新用户帐户，到成员资格框架中创建帐户和执行后的帐户的用户界面创建任务，例如发送确认电子邮件和刚创建的用户登录到网站。 使用 CreateUserWizard 控件只需将 CreateUserWizard 控件从工具箱拖到页上，然后再设置一些属性。 在大多数情况下，不需要编写一行代码。 我们将探讨此有用控件中第 6 步中的详细信息。

如果通过典型创建帐户网页仅创建新的用户帐户，则不太可能曾经需要编写代码，使用`CreateUser`方法中，为 CreateUserWizard 控件可能满足您的需求。 但是，`CreateUser`需要高度自定义的创建帐户的用户体验，或者当您需要以编程方式创建新的用户帐户通过替代接口，方法是在方案中非常方便。 例如，你可能允许用户上传 XML 文件包含从某个其他应用程序的用户信息的页面。 页可能会的分析内容上传的 XML 文件，并在 XML 中创建新的帐户用于表示每个用户，通过调用`CreateUser`方法。

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>步骤 6： 使用 CreateUserWizard 控件创建一个新用户

ASP.NET 附带了大量登录 Web 控件。 这些控件可帮助许多常见用户帐户和登录名相关情况。 [CreateUserWizard 控件](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)是一个此类旨在提供用于将新的用户帐户添加到成员资格框架的用户界面的控件。

像许多其他与登录相关 Web 控件，而无需编写一行代码可以使用 CreateUserWizard。 直观地提供了基于成员资格提供程序的配置设置并在内部调用的用户界面`Membership`类的`CreateUser`方法后用户输入所需的信息并单击创建用户按钮。 CreateUserWizard 控件是极可自定义。 有大量在各个阶段的帐户创建过程期间触发的事件。 我们可以根据需要若要将自定义逻辑注入到帐户创建工作流创建事件处理程序。 此外，CreateUserWizard 的外观是非常灵活。 有多个定义的默认接口; 外观的属性如有必要，该控件可以转换为模板，或可能添加其他用户注册步骤。

让我们开始看使用 CreateUserWizard 控件的默认接口和行为。 然后，我们将探讨如何自定义控件的属性和事件通过外观。

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>检查 CreateUserWizard 的默认接口和行为

返回到`CreatingUserAccounts.aspx`页中`Membership`文件夹中，切换到设计或拆分模式中，并将 CreateUserWizard 控件添加到页面顶部。 在工具箱的登录名控件部分下归档 CreateUserWizard 控件。 添加控件之后, 设置其`ID`属性设置为`RegisterUser`。 在图 11 所示的屏幕截图，如 CreateUserWizard 呈现文本框的新用户的用户名、 密码、 电子邮件地址和安全问题和答案的接口。


[![CreateUserWizard 控件呈现泛型创建用户界面](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**图 11**: CreateUserWizard 控件呈现泛型的创建用户界面 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image33.png))


让我们看一段时间来比较 CreateUserWizard 控件与我们在步骤 5 中创建的接口生成的默认用户界面。 对于初学者而言，CreateUserWizard 控件允许的访问者指定的安全问题和答案，而我们手动创建的接口使用预定义的安全问题。 CreateUserWizard 控件的界面还包括验证控件，而我们不得不尚未实现对我们接口的窗体字段的验证。 和 CreateUserWizard 控件接口包含 （连同以确保输入密码的文本和比较密码文本框相等 CompareValidator) 的确认密码文本框。

有趣的是 CreateUserWizard 控件咨询成员资格提供程序的配置设置，呈现其用户界面时。 例如，安全问题和答案文本框仅显示如果`requiresQuestionAndAnswer`设置为 True。 同样，CreateUserWizard 会自动添加 RegularExpressionValidator 控件，以确保密码强度要求满足，并设置其`ErrorMessage`并`ValidationExpression`属性基于`minRequiredPasswordLength`， `minRequiredNonalphanumericCharacters`，和`passwordStrengthRegularExpression`配置设置。

CreateUserWizard 控件，正如其名，派生自[向导控件](https://msdn.microsoft.com/library/s2etd1ek.aspx)。 向导控件旨在以提供用于完成多步骤任务的接口。 向导控件可能包含任意数目的`WizardSteps`、 其中每个是定义 HTML 的模板和 Web 控件的该步骤。 向导控件最初显示第一个`WizardStep`，以及允许用户可从某一步前进到下一步，或返回到上一步骤的导航控件。

如图 11 中的声明性标记所示，CreateUserWizard 控件的默认接口包含两个`WizardStep`s:

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? 呈现的界面以收集用于创建新的用户帐户信息。 这是在图 11 所示的步骤。
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? 呈现一条消息指出已成功创建帐户。

可以修改 CreateUserWizard 的外观和行为，通过将任一步骤转换为模板，或添加您自己`WizardStep`s。 我们将介绍添加`WizardStep`到中的注册界面*存储的其他用户信息*教程。

我们来看 CreateUserWizard 控件在操作中。 请访问`CreatingUserAccounts.aspx`通过浏览器的页。 首先 CreateUserWizard 的界面中输入无效值。 请尝试输入密码不符合密码强度要求，或将用户名称文本框保留为空。 CreateUserWizard 将显示相应的错误消息。 图 12 显示时尝试创建具有无法强密码的用户的输出。


[![CreateUserWizard 自动注入验证控件](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**图 12**: CreateUserWizard 自动注入验证控件 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image36.png))


接下来，到 CreateUserWizard 输入适当的值，然后单击创建用户按钮。 假设已输入必填的字段，并且密码的强度就足够了，CreateUserWizard 将创建新的用户帐户通过成员资格框架，并随后显示`CompleteWizardStep`的接口 （请参阅图 13）。 在后台，CreateUserWizard 调用`Membership.CreateUser`方法，只需像在步骤 5 中执行。


[![新的用户帐户已成功创建](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**图 13**: 新的用户帐户已成功创建 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image39.png))


> [!NOTE]
> 如图 13 所示，`CompleteWizardStep`的界面包括继续按钮。 但是，现在只需单击执行回发时，在同一页上保留访问者。 自定义 CreateUserWizard 的外观和行为通过其属性部分中我们将探讨如何具有此按钮将发送到访问者`Default.aspx`（或某些其他页面）。


在创建新的用户帐户后, 返回到 Visual Studio，并检查`aspnet_Users`和`aspnet_Membership`我们图 10，以验证是否已成功创建该帐户中的表。

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>自定义 CreateUserWizard 的行为和外观通过其属性

中有许多种情况下，通过属性，可以自定义 CreateUserWizard `WizardStep` s 和事件处理程序。 在本部分中我们将探讨如何自定义控件的外观，通过其属性，下一节介绍扩展通过事件处理程序的控件的行为。

几乎所有 CreateUserWizard 控件的默认用户界面中显示的文本可以进行自定义通过其大量的属性。 例如，在文本框的左侧显示的用户名、 密码、 确认密码、 电子邮件、 安全问题和安全答案标签也可以通过自定义[ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx)， [ `PasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx)， [ `ConfirmPasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx)， [ `EmailLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx)， [ `QuestionLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)，和[ `AnswerLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx)属性，分别。 同样，没有用于指定在创建用户并继续按钮的文本属性`CreateUserWizardStep`和`CompleteWizardStep`，因为如果这些按钮将呈现为按钮、 Linkbutton 或 ImageButtons 也。

颜色、 边框、 字体和其他可视元素是可通过样式属性的主机配置。 CreateUserWizard 控件本身具有常见 Web 控件的样式属性- `BackColor`， `BorderStyle`， `CssClass`， `Font`，等等-和提供多种用于定义的特定部分的外观的样式属性CreateUserWizard 的接口。 [ `TextBoxStyle`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)，例如，定义中的文本框的样式`CreateUserWizardStep`，而[`TitleTextStyle`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx)定义 （注册你新标题的样式帐户）。

除了与外观相关的属性，还有多个影响 CreateUserWizard 控件的行为的属性。 [ `DisplayCancelButton`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)，如果设置为 True，将显示取消按钮旁边的创建用户按钮 （默认值为 False）。 如果显示取消按钮，请确保还设置[`CancelDestinationPageUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)，它指定在单击取消按钮后将用户发送到的页。 在上一节中的继续按钮中所述`CompleteWizardStep`的接口导致回发，但在相同页上保留访问者。 若要发送到其他页面上的访问者，单击继续按钮后，只需指定中的 URL [ `ContinueDestinationPageUrl`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)。

让我们更新`RegisterUser`CreateUserWizard 控件以显示取消按钮，并将发送到访问者`Default.aspx`时单击取消或继续按钮。 若要完成此操作，设置`DisplayCancelButton`属性设置为 True 且两`CancelDestinationPageUrl`和`ContinueDestinationPageUrl`属性设置为 ~ / Default.aspx。 图 14 显示了更新的 CreateUserWizard 时的浏览器查看。


[![CreateUserWizardStep 包括一个取消按钮](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**图 14**:`CreateUserWizardStep`包括一个取消按钮 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image42.png))


当在访问者输入用户名、 密码、 电子邮件地址和安全问题和答案，并单击创建用户时，创建一个新的用户帐户和访问者中记录为该新创建的用户。 假定访问的页面的人正在为自己创建一个新的帐户，这可能是所需的行为。 但是，你可能想要允许管理员添加新用户帐户。 在执行此操作，将创建用户帐户，但管理员仍以管理员身份 （而不是新创建的帐户） 登录。 可以通过布尔值修改此行为[`LoginCreatedUser`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)。

成员资格框架中的用户帐户包含一个已批准的标志;未获批准的用户将无法登录到网站。 默认情况下，新创建的帐户标记为批准的这样就允许用户立即登录到网站。 它有可能，但是，有标记为未批准的新用户帐户。 您可能需要管理员手动批准新用户，他们可以登录; 之前或者，您可能想要验证允许用户在登录之前在注册时输入的电子邮件地址有效。 这种情况可能存在的内容，您可以通过设置 CreateUserWizard 控件的标记为未批准的新创建的用户帐户[`DisableCreatedUser`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)为 True （默认值为 False）。

需要注意的其他行为相关的属性包括`AutoGeneratePassword`和`MailDefinition`。 如果[`AutoGeneratePassword`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx)设置为 True，`CreateUserWizardStep`不会显示在密码和确认密码文本框中; 相反，新创建用户的密码自动生成使用`Membership`类的[`GeneratePassword`方法](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)。 `GeneratePassword`方法构造一个指定长度的和使用足够数量的非字母数字字符，以满足配置的密码强度要求的密码。

[ `MailDefinition`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)如果你想要为帐户创建过程中指定的电子邮件地址发送一封电子邮件将很有用。 `MailDefinition`属性包含一系列的子属性用于定义构造的电子邮件消息有关的信息。 这些子属性包括诸如选项`Subject`， `Priority`， `IsBodyHtml`， `From`， `CC`，并`BodyFileName`。 [ `BodyFileName`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)指向文本或 HTML 文件，其中包含电子邮件的正文。 正文支持两个预定义的占位符：`<%UserName%>`和`<%Password%>`。 这些占位符，如果存在中`BodyFileName`文件中，将替换为刚创建用户的名称和密码。

> [!NOTE]
> `CreateUserWizard`控件的`MailDefinition`属性只需指定当创建一个新帐户时发送电子邮件消息的详细信息。 它不包含任何实际发送电子邮件方式的详细信息 （即，是否使用 SMTP 服务器或邮件投递目录、 任何身份验证信息等）。 需要在中定义这些低级别的详细信息`<system.net>`主题中`Web.config`。 有关这些配置设置和一般情况下发送电子邮件从 ASP.NET 2.0 的详细信息，请参阅[SystemNetMail.com 常见问题解答](http://www.systemnetmail.com/)和我的文章[ASP.NET 2.0 中发送电子邮件](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)。


### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>扩展 CreateUserWizard 的行为使用事件处理程序

CreateUserWizard 控件在其工作流期间引发事件的数。 例如，访问者输入其用户名、 密码和其他相关信息并单击创建用户按钮后，CreateUserWizard 控件引发其[`CreatingUser`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)。 如果在创建过程中，问题[`CreateUserError`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx)激发; 但是，如果已成功创建用户，则[`CreatedUser`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)引发。 获取引发的其他 CreateUserWizard 控件事件，但这些是三个最无关的。

在某些情况下我们可能想要利用 CreateUserWizard 工作流，我们可以通过创建相应的事件的事件处理程序来执行此操作。 为了说明这一点，让我们来改进`RegisterUser`CreateUserWizard 控件以包含一些自定义验证的用户名和密码。 具体而言，让我们来改进我们 CreateUserWizard，以便用户名不能包含前导或尾随空格和用户名不能在密码中任意位置出现如此。 简单地说，我们想要防止某人创建的用户名与"Scott"，或具有如 Scott 和 Scott.1234 用户名/密码组合。

若要完成此我们将创建的事件处理程序`CreatingUser`事件执行我们额外的验证检查。 如果所提供的数据无效，我们需要取消创建过程。 我们还需要将标签 Web 控件添加到页后，可以显示一条消息说明的用户名或密码无效。 首先，通过添加设置的 CreateUserWizard 控件下方的标签控件及其`ID`属性设置为`InvalidUserNameOrPasswordMessage`并将其`ForeColor`属性设置为`Red`。 清除其`Text`属性并设置其`EnableViewState`和`Visible`属性为 False。

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

接下来，创建 CreateUserWizard 控件的事件处理程序`CreatingUser`事件。 若要创建事件处理程序，在设计器中选择的控件，然后转到属性窗口。 从此处，单击闪电形图标，然后双击相应的事件创建事件处理程序。

将以下代码添加到 `CreatingUser` 事件处理程序中：

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

请注意，用户名和密码输入到 CreateUserWizard 控件是可通过其[ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)并[`Password`属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)分别。 我们可以使用上述的事件处理程序中的这些属性以确定提供的用户名是否包含前导或尾部空格，并且密码中找到用户名。 如果满足这些条件之一，则在显示一条错误消息`InvalidUserNameOrPasswordMessage`标签和事件处理程序的`e.Cancel`属性设置为`True`。 如果`e.Cancel`设置为`True`，CreateUserWizard 会简化其工作流，有效地取消用户帐户创建过程。

图 15 所示的屏幕截图`CreatingUserAccounts.aspx`当用户输入的用户名与前导空格。


[![不允许使用前导或尾随空格的用户名](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**图 15**： 不允许使用前导或尾随空格的用户名 ([单击以查看实际尺寸的图像](creating-user-accounts-vb/_static/image45.png))


> [!NOTE]
> 我们将看到使用 CreateUserWizard 控件的示例`CreatedUser`中的事件 *<a id="_msoanchor_11"> </a>[存储的其他用户信息](storing-additional-user-information-vb.md)* 教程。


## <a name="summary"></a>总结

`Membership`类的`CreateUser`方法在成员资格框架中创建新的用户帐户。 它会通过将调用委托给配置成员资格提供程序。 情况下`SqlMembershipProvider`，则`CreateUser`方法将添加到记录`aspnet_Users`和`aspnet_Membership`数据库表。

虽然可以创建新的用户帐户，以编程方式 （如我们在步骤 5 中看到），但速度更快、 更轻松的方法是使用 CreateUserWizard 控件。 此控件将呈现用于收集用户信息并在成员资格框架中创建一个新用户的多步骤的用户界面。 在后台，此控件使用相同`Membership.CreateUser`方法，如检查在步骤 5 中，但该控件中创建用户界面，验证控件和响应的用户帐户创建错误而无需编写一点代码。

现在我们来创建新的用户帐户具有的功能。 但是，登录页仍验证针对我们返回在第二个教程中指定这些硬编码的凭据。 在中<a id="_msoanchor_12"> </a>[下一教程](validating-user-credentials-against-the-membership-user-store-vb.md)我们将更新`Login.aspx`来验证用户的提供对成员资格框架的凭据。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [`CreateUser` 技术文档](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 控件概述](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [创建文件基于系统的站点映射提供程序](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [使用 ASP.NET 2.0 向导控件中创建分步的用户界面](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [检查 ASP.NET 2.0 的 Site navigation — 站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [母版页和站点导航](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [SQL 站点地图提供程序您期待已久](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)。

> [!div class="step-by-step"]
> [上一页](creating-the-membership-schema-in-sql-server-vb.md)
> [下一页](validating-user-credentials-against-the-membership-user-store-vb.md)
