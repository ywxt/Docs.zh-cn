---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-vb
title: 基于角色的授权 (VB) |Microsoft Docs
author: rick-anderson
description: 本教程首先介绍在角色框架如何将用户的角色相关联与他的安全上下文。 然后，它会检查如何应用基于角色的 URL...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: 83b4f5a4-4f5a-4380-ba33-f0b5c5ac6a75
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: b8cf8cc5fa802eb812482b236c8b2825423027e7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390980"
---
<a name="role-based-authorization-vb"></a>基于角色的授权 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.11.zip)或[下载 PDF](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_vb.pdf)

> 本教程首先介绍在角色框架如何将用户的角色相关联与他的安全上下文。 然后，它会检查如何应用基于角色的 URL 授权规则。 之后，我们将介绍如何使用声明性和编程性手段更改显示的数据和由 ASP.NET 页面提供的功能。


## <a name="introduction"></a>介绍

在中<a id="_msoanchor_1"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程中我们已了解如何使用 URL 授权来指定哪些用户可以访问一组特定的页。 只需少量的标记中使用`Web.config`，我们可以指示 ASP.NET，以便只有经过身份验证的用户访问页面。 或者我们可以规定，允许用户 Tito 和 Bob，或指示允许所有经过身份验证的用户 Sam 除外。

除了 URL 授权，我们还了解了声明性和编程技术，用于控制显示的数据和基础用户访问的页所提供的功能。 具体而言，我们创建了一个页面，列出当前目录的内容。 任何人都无法访问此页上，但只有经过身份验证的用户可以查看文件的内容和仅 Tito 无法删除的文件。

基于用户的用户应用授权规则可以增长到簿记噩梦。 更易于维护的方法是使用基于角色的授权。 值得高兴的是，我们已经为应用授权规则的工具的效果与在用户帐户以及与角色。 URL 授权规则可以指定而不是用户的角色。 LoginView 控件，将呈现为经过身份验证和匿名用户不同的输出，可以配置为显示不同的内容根据登录的用户的角色。 和角色 API 包括用于确定登录的用户的角色的方法。

本教程首先介绍在角色框架如何将用户的角色相关联与他的安全上下文。 然后，它会检查如何应用基于角色的 URL 授权规则。 之后，我们将介绍如何使用声明性和编程性手段更改显示的数据和由 ASP.NET 页面提供的功能。 让我们进入正题！

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>了解如何角色关联的用户的安全上下文

每当请求进入 ASP.NET 管道是一个安全上下文，其中包括标识请求者的信息与相关联。 当使用窗体身份验证，身份验证票证用作一个标识令牌。 如中所述<a id="_msoanchor_2"> </a> [*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-vb.md)并<a id="_msoanchor_3"> </a> [*窗体身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)教程中，`FormsAuthenticationModule`负责确定请求者，它执行期间的标识[`AuthenticateRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx).

如果找到有效且未过期的身份验证票证，则`FormsAuthenticationModule`进行解码以确定请求者的标识。 创建一个新`GenericPrincipal`对象并将分配到`HttpContext.User`对象。 用途的主体，如`GenericPrincipal`，是标识已经过身份验证的用户的名称以及她所属于的角色。 目的就是这一事实的所有主体对象都有明显`Identity`属性和一个`IsInRole(roleName)`方法。 `FormsAuthenticationModule`，但是，不希望录制角色信息和`GenericPrincipal`它创建的对象未指定任何角色。

如果启用了角色框架， [ `RoleManagerModule` ](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) HTTP 模块中的步骤后`FormsAuthenticationModule`，并标识已经过身份验证的用户的角色期间[`PostAuthenticateRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)、 哪些之后才激发`AuthenticateRequest`事件。 如果该请求是否来自已验证的用户，`RoleManagerModule`将覆盖`GenericPrincipal`对象创建的`FormsAuthenticationModule`并将其替换[`RolePrincipal`对象](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)。 `RolePrincipal`类使用角色 API 来确定哪些用户所属的角色。

图 1 所示的 ASP.NET 管道工作流时使用窗体身份验证和角色框架。 `FormsAuthenticationModule` ，则首先执行、 标识用户通过其身份验证票证，并创建一个新`GenericPrincipal`对象。 下一步，`RoleManagerModule`中的步骤，并将覆盖`GenericPrincipal`对象`RolePrincipal`对象。

如果匿名用户访问该网站，既不`FormsAuthenticationModule`也不`RoleManagerModule`创建主体对象。


[![身份验证的用户使用 Forms 身份验证和角色框架时 ASP.NET 管道事件](role-based-authorization-vb/_static/image2.png)](role-based-authorization-vb/_static/image1.png)

**图 1**: 经过身份验证用户时使用窗体身份验证和角色框架的 ASP.NET 管道事件 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image3.png))


### <a name="caching-role-information-in-a-cookie"></a>缓存在 Cookie 中的角色信息

`RolePrincipal`对象的`IsInRole(roleName)`方法调用`Roles`。`GetRolesForUser` 若要获取用户的角色，以便确定用户是否属于*roleName*。 当使用`SqlRoleProvider`，这样就在查询中为角色存储数据库。 当使用基于角色的 URL 授权规则`RolePrincipal`的`IsInRole`将对每个请求保护的基于角色的 URL 授权规则页调用方法。 而不是必须查找数据库中对每个请求的角色信息`Roles`framework 包含缓存在 cookie 中的用户的角色的选项。

如果配置角色框架来缓存在 cookie 中，用户的角色`RoleManagerModule`在 ASP.NET 管道的过程中创建 cookie [ `EndRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)。 中的后续请求中使用此 cookie `PostAuthenticateRequest`，这是当`RolePrincipal`创建对象。 如果 cookie 有效，并且未过期，cookie 中的数据分析和使用以填充用户的角色，这样可节省`RolePrincipal`无需调用`Roles`类来确定用户的角色。 图 2 描绘了此工作流。


[![用户的角色信息可以存储在 Cookie 来提高性能](role-based-authorization-vb/_static/image5.png)](role-based-authorization-vb/_static/image4.png)

**图 2**: 用户的角色的信息可以存储在 Cookie 中提高性能 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image6.png))


默认情况下，禁用角色缓存 cookie 机制。 可以通过启用`<roleManager>`; 中的配置标记`Web.config`。 我们讨论了使用[`<roleManager>`元素](https://msdn.microsoft.com/library/ms164660.aspx)来指定角色中的提供程序<a id="_msoanchor_4"> </a> [*创建和管理角色*](creating-and-managing-roles-vb.md)教程中，因此您应该已经在应用程序的此元素`Web.config`文件。 为属性的指定角色缓存 cookie 设置`<roleManager>`; 元素，并汇总了表 1。

> [!NOTE]
> 表 1 中列出的配置设置指定生成的角色缓存 cookie 的属性。 对 cookie、 工作原理和它们的各种属性的详细信息，请阅读[此 Cookie 教程](http://www.quirksmode.org/js/cookies.html)。


| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>说明</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              一个布尔值，该值指示是否使用 cookie 缓存。 默认为 `false`。                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     角色缓存 cookie 的名称。 默认值是"。ASPXROLES"。                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                角色名称 cookie 的路径。 路径属性使开发人员来限制到特定的目录层次结构的 cookie 的范围。 默认值是"/"，它通知将发送到对域进行的任何请求的身份验证票证 cookie 的浏览器。                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               指示哪些技术可用来保护角色缓存 cookie。 允许的值为： `All` （默认值）;`Encryption`;`None`; 和`Validation`。 回头参考的步骤 3 <a id="_anchor_5"> </a> [*窗体身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)教程，了解有关这些保护级别的详细信息。                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   一个布尔值，该值指示是否需要 SSL 连接来传输身份验证 cookie。 默认值为 `false`。                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  一个布尔值，该值指示用户是否每次重置 cookie 超时值在单个会话期间访问该网站。 默认值为 `false`。 此值才相关`createPersistentCookie`设置为`true`。                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         指定时间，以分钟为单位，在其后的身份验证票证 cookie 过期。 默认值为 `30`。 此值才相关`createPersistentCookie`设置为`true`。                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   一个布尔值，该值指定角色缓存 cookie 的会话 cookie 或持久性 cookie。 如果`false`（默认值），使用会话 cookie，则这在浏览器关闭时删除。 如果`true`，使用持久性 cookie; 过期`cookieTimeout`数分钟后已创建的或前一次访问，具体取决于值之后`cookieSlidingExpiration`。                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 指定 cookie 的域值。 默认值为空字符串，这会导致浏览器使用从该情况下，它已签发 （如 www.yourdomain.com) 的域。 在这种情况下，将 cookie<strong>不</strong>到子域，例如 admin.yourdomain.com 进行请求时发送。 如果你想要传递给所有子域的 cookie 需要自定义`domain`属性，将其设置为"yourdomain.com"。                                                                                                                                                 |
|    `maxCachedResults`     | 指定在 cookie 中缓存的角色名称的最大数目。 默认值为 25。 `RoleManagerModule`不会创建属于用户的 cookie 超过`maxCachedResults`角色。 因此，`RolePrincipal`对象的`IsInRole`方法将使用`Roles`类来确定用户的角色。 原因`maxCachedResults`存在是因为许多用户代理不允许 cookie 大于 4,096 字节。 因此，此线帽旨在减少可能超出此大小限制。 如果具有极长的角色名称，你可能想要考虑指定较小`maxCachedResults`值; contrariwise，如果您具有极短的角色的名称，您可以可能增大此值。 |

**表 1**： 角色缓存 Cookie 配置选项

让我们配置应用程序以使用非永久性角色缓存 cookie。 若要完成此操作，更新`<roleManager>`中的元素`Web.config`包括 cookie 相关的以下属性：

[!code-xml[Main](role-based-authorization-vb/samples/sample1.xml)]

我更新`<roleManager>`; 元素通过添加三个属性： `cacheRolesInCookie`， `createPersistentCookie`，和`cookieProtection`。 通过设置`cacheRolesInCookie`到`true`，则`RoleManagerModule`现在自动缓存在 cookie 中的用户的角色，而无需查找每个请求的用户的角色信息。 我显式设置`createPersistentCookie`并`cookieProtection`向属性`false`和`All`分别。 从技术上讲，我不需要指定这些属性，因为我只是它们分配给其默认值，但我放到这里来明确作出值清除我不使用持久性 cookie，并且 cookie 同时加密和验证。

这就是一切就这么简单 ！ 自此以后，角色框架将缓存在 cookie 中的用户的角色。 如果用户的浏览器不支持 cookie，或如果其 cookie 被删除或丢失，由于某种原因，它并非难事 –`RolePrincipal`对象时将只使用`Roles`任何 cookie （或一个无效或已过期） 是可用的情况下的类。

> [!NOTE]
> Microsoft 的模式&amp;实践组不鼓励使用持久性角色缓存 cookie。 如果黑客可以以某种方式访问有效用户的 cookie，因为角色缓存 cookie 拥有不足以证明角色成员身份，他可以模拟该用户。 发生这种情况的可能性会增加用户的浏览器上保存 cookie。 有关此安全建议，以及其他安全问题的详细信息，请参阅[ASP.NET 2.0 的安全问题列表](https://msdn.microsoft.com/library/ms998375.aspx)。


## <a name="step-1-defining-role-based-url-authorization-rules"></a>步骤 1： 定义基于角色的 URL 授权规则

如中所述<a id="_msoanchor_6"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程中，URL 授权提供了一种方法来限制对一组页上的用户的用户或角色的角色的访问基数。 URL 授权规则中将逐一`Web.config`使用[`<authorization>`元素](https://msdn.microsoft.com/library/8d82143t.aspx)与`<allow>`和`<deny>`子元素。 除了前面的教程中所述的与用户相关的授权规则每个`<allow>`和`<deny>`还可以包含子元素：

- 一个特定的角色
- 角色的以逗号分隔列表

例如，URL 授权规则授予访问权限的用户的管理员和在监督器角色，但拒绝向所有其他用户的访问：

[!code-xml[Main](role-based-authorization-vb/samples/sample2.xml)]

`<allow>`上述标记中的元素声明，则允许管理员和主管角色; `<deny>`; 元素指示*所有*用户被拒绝。

让我们配置我们的应用程序，以便`ManageRoles.aspx`， `UsersAndRoles.aspx`，并`CreateUserWizardWithRoles.aspx`页仅在管理员角色中，这些用户可以访问时`RoleBasedAuthorization.aspx`页仍然可供所有访问者访问。

若要完成此操作，首先添加`Web.config`文件为`Roles`文件夹。


[![将 Web.config 文件添加到角色目录](role-based-authorization-vb/_static/image8.png)](role-based-authorization-vb/_static/image7.png)

**图 3**： 添加`Web.config`的文件`Roles`目录 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image9.png))


接下来，添加以下配置标记到`Web.config`:

[!code-xml[Main](role-based-authorization-vb/samples/sample3.xml)]

`<authorization>`中的元素`<system.web>`部分指示只有管理员角色中的用户可能访问中的 ASP.NET 资源`Roles`目录。 `<location>`元素定义一组替代的 URL 授权规则`RoleBasedAuthorization.aspx`页中，因此所有用户访问页面。

保存到所做的更改后`Web.config`、 以不在管理员角色的用户身份登录，然后尝试访问其中一个受保护的页面。 `UrlAuthorizationModule`将检测到没有权限访问所请求的资源; 因此，`FormsAuthenticationModule`将重定向到登录页。 登录页将然后重定向到`UnauthorizedAccess.aspx`页面 （请参阅图 4）。 从登录页面到此最终重定向`UnauthorizedAccess.aspx`错误是由于我们添加到在步骤 2 中的登录页的代码导致<a id="_msoanchor_7"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程。 具体而言，登录页自动重定向到任何身份验证的用户`UnauthorizedAccess.aspx`如果在查询字符串包含`ReturnUrl`参数，作为此参数指示，用户转到登录页面后尝试查看他不是的页面查看权限。


[![只有管理员角色中的用户可以查看受保护的页面](role-based-authorization-vb/_static/image11.png)](role-based-authorization-vb/_static/image10.png)

**图 4**： 只有管理员角色中的用户可以查看受保护页面 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image12.png))


注销，然后以管理员角色中的用户身份登录。 现在，应能够查看三个受保护的页面。


[![可以通过访问 Tito UsersAndRoles.aspx 页因为他是管理员角色中](role-based-authorization-vb/_static/image14.png)](role-based-authorization-vb/_static/image13.png)

**图 5**： 可以访问 Tito`UsersAndRoles.aspx`页因为他是管理员角色中 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image15.png))


> [!NOTE]
> 指定 URL 授权规则 – 角色或用户 – 时务必要记住的规则包括已分析了一次，从顶部向下。 一旦找到匹配项，授予或拒绝访问用户，具体取决于在找到匹配项`<allow>`或`<deny>`元素。 **如果不找到任何匹配项，则该用户被授予访问权限。** 因此，如果你想要限制对一个或多个用户帐户的访问，则必须使用`<deny>`URL 授权配置中的最后一个元素的元素。 **如果不包括您的 URL 授权规则**`<deny>`**元素中，所有用户将被都授予访问权限。** 有关如何分析 URL 授权规则的更全面讨论，请返回到"How`UrlAuthorizationModule`使用授权规则来允许或拒绝访问"部分<a id="_msoanchor_8"> </a> [ *基于用户的授权*](../membership/user-based-authorization-vb.md)教程。


## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>步骤 2： 限制基于当前登录的用户的角色功能

允许使用哪些标识，可以轻松地指定粗略的授权规则该状态的 URL 授权使和哪些拒绝从查看特定页面 （或一个文件夹及其子文件夹中的所有页面）。 但是，在某些情况下我们可能想要允许所有用户访问页上，但是限制对基于来访的用户的角色页面的功能。 这可能需要显示或隐藏数据基于用户的角色，或为属于特定角色的用户提供其他功能。

可以实现这种细粒度基于角色的授权规则，可以以声明方式或以编程方式 （或某些结合在一起的两个）。 下一节中，我们将了解如何实施声明性的细粒度授权通过登录视图控件。 接下来，我们将探讨编程技术。 我们可以看看应用细粒度授权规则之前，但是，我们首先需要创建它的功能取决于访问它的用户角色的页面。

让我们创建的系统 GridView 中列出的所有用户帐户的页面。 GridView 将包括每个用户的用户名、 电子邮件地址、 上次登录日期和有关用户的注释。 除了显示每个用户的信息，GridView 将包括编辑和删除功能。 我们最初将此页创建与编辑和删除功能可供所有用户。 在"使用 LoginView 控件"和"以编程方式限制功能"部分中，我们将了解如何启用或禁用这些功能基于来访的用户的角色。

> [!NOTE]
> 我们将要构建的 ASP.NET 页使用 GridView 控件来显示用户帐户。 本教程系列重点介绍窗体身份验证、 授权、 用户帐户和角色，因为我不想花费太多时间来讨论 GridView 控件的内部工作机制。 虽然本教程提供了特定设置此页的分步说明，它不会不研究一下为什么未进行某些选择，或影响特定属性对呈现的输出的详细信息。 有关对 GridView 控件的全面检查，请参阅我*[使用 ASP.NET 2.0 中的数据](../../data-access/index.md)* 系列教程。


首先打开`RoleBasedAuthorization.aspx`页中`Roles`文件夹。 从拖到设计器和组页将 GridView 及其`ID`到`UserGrid`。 稍后我们将编写代码，调用`Membership`。`GetAllUsers` 方法，并将绑定生成`MembershipUserCollection`对象到 GridView。 `MembershipUserCollection`包含`MembershipUser`中系统; 每个用户帐户的对象`MembershipUser`对象具有属性，如`UserName`，`Email`，`LastLoginDate` ，依此类推。

我们编写的代码，将用户帐户绑定到网格之前，让我们首先定义 GridView 的字段。 从 GridView 的智能标记上，单击"编辑列"链接以启动字段对话框 （请参见图 6）。 在这里，取消选中左下角中的"自动生成字段"复选框。 由于我们希望此 GridView 编辑和删除功能，包括添加 CommandField 并设置其`ShowEditButton`和`ShowDeleteButton`属性为 True。 接下来，添加用于显示四个字段`UserName`， `Email`， `LastLoginDate`，和`Comment`属性。 BoundField 用于两个只读属性 (`UserName`并`LastLoginDate`) 和两个可编辑字段的 Templatefield (`Email`和`Comment`)。

使第一个 BoundField 显示`UserName`属性; 将设置其`HeaderText`和`DataField`为"UserName"的属性。 此字段将不可编辑，因此可将其`ReadOnly`属性设为 True。 配置`LastLoginDate`BoundField 通过设置其`HeaderText`为"上次登录"并将其`DataField`到"LastLoginDate"。 让我们设置此 BoundField 的输出格式，以便只是日期显示 （而不是日期和时间）。 若要完成此操作，设置此 BoundField`HtmlEncode`属性设置为 False 并将其`DataFormatString`属性设置为"{0:d}"。 此外设置`ReadOnly`属性设为 True。

设置`HeaderText`"电子邮件"和"注释"两个 Templatefield 的属性。


[![可通过字段对话框配置 GridView 的字段](role-based-authorization-vb/_static/image17.png)](role-based-authorization-vb/_static/image16.png)

**图 6**： 的 GridView 字段可以是配置通过字段对话框 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image18.png))


现在，我们需要定义`ItemTemplate`和`EditItemTemplate`"Email"和"注释"Templatefield。 将标签 Web 控件添加到每个`ItemTemplates`，并将绑定其`Text`属性设置为`Email`和`Comment`属性，分别。

对于"电子邮件"TemplateField，添加名为的 TextBox`Email`到其`EditItemTemplate`，并将绑定其`Text`属性设置为`Email`使用双向数据绑定的属性。 添加一个 RequiredFieldValidator 和 RegularExpressionValidator 到`EditItemTemplate`以确保访问者编辑电子邮件属性输入一个有效的电子邮件地址。 对于"注释"TemplateField，添加名为多行文本框`Comment`到其`EditItemTemplate`。 设置文本框的`Columns`和`Rows`属性设置为 40 和 4 中，分别，然后将绑定其`Text`属性设置为`Comment`使用双向数据绑定的属性。

以后配置这些 Templatefield，其声明性标记看起来应类似于下面：

[!code-aspx[Main](role-based-authorization-vb/samples/sample4.aspx)]

编辑或删除我们将需要知道该用户的用户帐户时`UserName`属性值。 设置 GridView`DataKeyNames`为"UserName"的属性，以便此信息可通过 GridView 的`DataKeys`集合。

最后，向页面添加验证摘要控件并设置其`ShowMessageBox`属性设为 True 并将其`ShowSummary`属性设置为 False。 使用这些设置，ValidationSummary 将显示客户端的警报，如果用户尝试编辑具有缺失或无效的电子邮件地址的用户帐户。

[!code-aspx[Main](role-based-authorization-vb/samples/sample5.aspx)]

我们现在已经完成此页面的声明性标记。 我们的下一个任务是将用户帐户的组绑定到 GridView。 添加一个名为`BindUserGrid`到`RoleBasedAuthorization.aspx`绑定的页面的代码隐藏类`MembershipUserCollection`返回`Membership.GetAllUsers`到`UserGrid`GridView。 调用此方法从`Page_Load`上第一次的页面访问事件处理程序。

[!code-vb[Main](role-based-authorization-vb/samples/sample6.vb)]

利用此代码，请访问通过浏览器页面。 如图 7 所示，应会看到 GridView 列出系统中的每个用户帐户的相关信息。


[![UserGrid GridView 列出系统中的每个用户的信息](role-based-authorization-vb/_static/image20.png)](role-based-authorization-vb/_static/image19.png)

**图 7**: `UserGrid` GridView 列出信息有关每个用户在系统中 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image21.png))


> [!NOTE]
> `UserGrid` GridView 列出所有的非分页界面中的用户。 此简单网格接口并不适用于方案有多个几十个或多个用户。 一种选择是配置 GridView，若要启用分页。 `Membership.GetAllUsers`方法有两个重载： 一个可接受任何输入的参数并返回的所有用户，另一个使用的页索引和页大小的整数值并都返回仅指定用户的子集。 第二个重载可用于对更高效地通过用户的页面，因为它返回的用户帐户只是精确的子集而非*所有*它们。 如果有成千上万的用户帐户，你可能需要考虑基于筛选器的接口，仅显示其用户名所选字符开头，例如这些用户。 [ `Membership.FindUsersByName`方法](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)非常适合生成基于筛选器的用户界面。 我们将介绍在将来的教程中构建此类接口。


GridView 控件提供了内置的编辑和删除支持时该控件绑定到正确配置的数据源控件，例如 SqlDataSource 或对象数据源。 `UserGrid` GridView，但是，具有其数据以编程方式绑定; 因此，我们必须编写代码来执行这两项任务。 具体而言，我们将需要创建的事件处理程序 GridView `RowEditing`， `RowCancelingEdit`， `RowUpdating`，和`RowDeleting`事件，当在访问者单击 GridView 的触发编辑，取消，更新，或删除按钮。

首先创建事件处理程序为 GridView `RowEditing`， `RowCancelingEdit`，和`RowUpdating`事件，然后添加以下代码：

[!code-vb[Main](role-based-authorization-vb/samples/sample7.vb)]

`RowEditing`并`RowCancelingEdit`事件处理程序只需设置 GridView 的`EditIndex`属性，然后重新绑定的列表的用户帐户添加到网格。 有趣的事情发生在`RowUpdating`事件处理程序。 此事件处理程序首先确保数据有效，然后获取`UserName`值中的已编辑的用户帐户`DataKeys`集合。 `Email`并`Comment`文本框中两个 Templatefield `EditItemTemplate` s 然后以编程方式引用。 其`Text`属性包含已编辑的电子邮件地址和注释。

若要更新通过成员身份 API 的用户帐户，我们需要先获取用户的信息，我们通过调用`Membership.GetUser(userName)`。 返回`MembershipUser`对象的`Email`和`Comment`属性然后更新为从编辑界面输入到两个文本框的值。 最后，通过调用保存这些修改[ `Membership.UpdateUser` ](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)。 `RowUpdating`事件处理程序通过还原到其预先编辑界面 GridView 来完成。

接下来，创建`RowDeleting`RowDeleting 事件处理程序，然后添加以下代码：

[!code-vb[Main](role-based-authorization-vb/samples/sample8.vb)]

上述的事件处理程序将启动方法是获取`UserName`GridView 的取值`DataKeys`集合; 这`UserName`然后将值传递到成员资格类[`DeleteUser`方法](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)。 `DeleteUser`方法系统，包括相关的成员身份数据 （如哪些角色此用户归属的） 中删除用户帐户。 删除用户，在网格的后`EditIndex`（如果用户单击删除另一个行处于编辑模式时） 设置为-1 和`BindUserGrid`调用方法。

> [!NOTE]
> 删除按钮不需要任何种类的来自用户之前删除的用户帐户的确认。 建议您添加某种形式的用户确认要降低出现意外删除的帐户的可能性。 若要确认某项操作的最简单方法之一是通过客户端的确认对话框。 有关此技术的详细信息，请参阅[删除时添加客户端确认](https://asp.net/learn/data-access/tutorial-42-vb.aspx)。


验证此页可以按照预期方式。 您应能够编辑任何用户的电子邮件地址和注释，以及删除任何用户帐户。 由于`RoleBasedAuthorization.aspx`页是所有用户访问，任何用户 – 甚至匿名访问者 – 可以访问此页面并编辑和删除用户帐户 ！ 让我们更新此页，以便只有监督员和管理员角色中的用户可以编辑用户的电子邮件地址和注释，并且只有管理员才可以删除用户帐户。

"使用 LoginView 控件"部分介绍使用 LoginView 控件来显示说明特定于用户的角色。 如果管理员角色中的用户访问此页时，我们将演示说明如何编辑和删除用户。 如果在监督器角色的用户达到此页，我们将编辑用户显示的说明。 并且如果访问者是匿名的或不在的主管或管理员角色，我们将显示一条消息说明不能编辑或删除用户帐户信息。 在"以编程方式限制功能"部分中，我们将编写代码以编程方式显示或隐藏基于用户的角色的编辑和删除按钮。

### <a name="using-the-loginview-control"></a>使用 LoginView 控件

如我们在过去的教程中所见，LoginView 控件可用于显示不同的接口为经过身份验证和匿名用户，但 LoginView 控件还可用于显示不同的标记，基于用户的角色。 让我们使用 LoginView 控件显示基于来访用户角色的不同指令。

通过添加上述 LoginView 开始`UserGrid`GridView。 LoginView 控件如我们之前讨论过，有两个内置模板：`AnonymousTemplate`和`LoggedInTemplate`。 在这种不能编辑或删除任何用户信息通知用户这些模板中输入一个简短的消息。

[!code-aspx[Main](role-based-authorization-vb/samples/sample9.aspx)]

除了`AnonymousTemplate`和`LoggedInTemplate`，可以包括 LoginView 控件*RoleGroups*，这是特定于角色的模板。 每个 RoleGroup 包含一个属性， `Roles`，它指定 RoleGroup 适用于哪些角色。 `Roles`属性可以设置到 （如"管理员"） 的单个角色或角色 （如"管理员，在监督器"） 的逗号分隔列表。

若要管理 RoleGroups，单击要打开 RoleGroup 集合编辑器的控件的智能标记中的"编辑 RoleGroups"链接。 添加两个新 RoleGroups。 设置第一个 RoleGroup`Roles`属性设置为"管理员"和"监督"到秒。


[![管理登录视图的特定于角色的模板通过 RoleGroup 集合编辑器](role-based-authorization-vb/_static/image23.png)](role-based-authorization-vb/_static/image22.png)

**图 8**： 管理登录视图的特定于角色的模板通过 RoleGroup 集合编辑器 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image24.png))


单击确定关闭 RoleGroup 集合编辑器;这会更新登录视图的声明性标记，以包括`<RoleGroups>`节替换`<asp:RoleGroup>`RoleGroup 集合编辑器中的每个 RoleGroup 的子元素定义。 此外，"视图"下拉列表中 LoginView 的智能标记的最初列出，只需`AnonymousTemplate`和`LoggedInTemplate`– 现在包括还添加了的 RoleGroups。

编辑 RoleGroups，以便在监督器角色中的用户显示的有关如何编辑用户帐户，但管理员角色中的用户显示的编辑和删除说明。 进行这些更改后，登录视图的声明性标记应类似于以下。

[!code-aspx[Main](role-based-authorization-vb/samples/sample10.aspx)]

进行这些更改之后, 保存页面，并通过浏览器然后访问它。 首次作为匿名用户访问页面。 应显示该消息，"您未登录到系统。 因此您无法编辑或删除任何用户信息。" 然后作为身份验证的用户，但既不主管或管理员角色中的其中一个登录。 此时应看到消息"你不是在监督器或管理员角色的成员。 因此您无法编辑或删除任何用户信息。"

接下来，以在监督器角色的成员的用户登录。 此时应会看到在监督器特定于角色的消息 （请参阅图 9）。 如果您以中应会看到特定于角色的管理员角色消息 （请参阅图 10） 的管理员的用户身份登录。


[![Bruce 显示在监督器特定于角色的消息](role-based-authorization-vb/_static/image26.png)](role-based-authorization-vb/_static/image25.png)

**图 9**: Bruce 显示在监督器特定于角色的消息 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image27.png))


[![Tito 显示管理员特定于角色的消息](role-based-authorization-vb/_static/image29.png)](role-based-authorization-vb/_static/image28.png)

**图 10**: Tito 显示管理员特定于角色的消息 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image30.png))


图 9 中的屏幕截图和 10 个显示，LoginView 仅呈现一个模板，即使多个模板应用。 Bruce 和 Tito 都记录在用户，但登录视图呈现仅匹配 RoleGroup 和 not `LoggedInTemplate`。 此外，Tito 属于管理员和在监督器角色，但 LoginView 控件呈现管理员特定于角色的模板而不是在监督器之一。

图 11 说明了由 LoginView 控件用来确定哪些模板来呈现的工作流。 请注意，如果有多个 RoleGroup 指定，LoginView 模板用于呈现*第一个*RoleGroup 相匹配。 换而言之，如果我们必须放置在监督器 RoleGroup 作为第一个 RoleGroup 和第二个管理员，然后 Tito 访问此页时他会看到在监督器消息。


[![用于确定哪个模板呈现 LoginView 控件的工作流](role-based-authorization-vb/_static/image32.png)](role-based-authorization-vb/_static/image31.png)

**图 11**： 用于确定什么模板呈现 LoginView 控件的工作流 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>以编程方式限制功能

当 LoginView 控件显示不同的说明基于角色的用户访问的页面时，编辑和取消按钮都保持对所有可见。 我们需要以编程方式对匿名访问者和监督员和管理员都不角色中的用户隐藏编辑和删除按钮。 我们需要为每个用户不是管理员隐藏删除按钮。 为了实现此目的，我们将编写一些代码以编程方式引用 CommandField 的编辑和删除 Linkbutton 和设置其`Visible`属性设置为`False`，如果有必要。

若要以编程方式引用 CommandField 中的控件的最简单方法是首先将其转换为模板。 若要实现此目的，单击 GridView 的智能标记中的"编辑列"链接，从当前字段的列表中选择 CommandField 并单击"将此字段转换为 TemplateField"链接。 这将转换为 TemplateField CommandField`ItemTemplate`和`EditItemTemplate`。 `ItemTemplate`包含编辑和删除时的 Linkbutton`EditItemTemplate`存储更新和取消 Linkbutton。


[![CommandField 转换为 TemplateField](role-based-authorization-vb/_static/image35.png)](role-based-authorization-vb/_static/image34.png)

**图 12**： 将转换 TemplateField CommandField 到 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image36.png))


更新编辑和删除中的 Linkbutton `ItemTemplate`，并设置其`ID`的值的属性`EditButton`和`DeleteButton`分别。

[!code-aspx[Main](role-based-authorization-vb/samples/sample11.aspx)]

GridView 数据绑定到 GridView，只要枚举中的记录及其`DataSource`属性，并生成相应`GridViewRow`对象。 为每个`GridViewRow`创建对象后，`RowCreated`触发事件。 为了隐藏未经授权的用户的编辑和删除按钮，我们需要创建此事件的事件处理程序，并以编程方式引用的编辑和删除的 Linkbutton，设置其`Visible`属性相应地。

创建事件处理程序`RowCreated`事件，然后添加以下代码：

[!code-vb[Main](role-based-authorization-vb/samples/sample12.vb)]

请记住`RowCreated`事件触发*所有*的 GridView 行，其中包括标头、 页脚、 寻呼程序接口等。 我们只想要以编程方式引用的编辑和删除 Linkbutton，如果我们处理的数据行不在编辑模式下 （因为在编辑模式下的行已更新和取消按钮而不是编辑和删除）。 此检查由`If`语句。

如果我们处理的数据行不是处于编辑模式下，引用的编辑和删除 Linkbutton 和他们`Visible`属性根据返回的布尔值设置`User`对象的`IsInRole(roleName)`方法。 `User`对象引用由创建的主体`RoleManagerModule`; 因此，`IsInRole(roleName)`方法使用角色 API 来确定当前的访问者是否属于*roleName*。

> [!NOTE]
> 我们也可以使用角色类直接，替换为调用`User.IsInRole(roleName)`通过调用[`Roles.IsUserInRole(roleName)`方法](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)。 我决定使用主体对象的`IsInRole(roleName)`方法在此示例中因为它是比直接使用角色 API 更高效。 在本教程前面我们配置要缓存在 cookie 中的用户的角色的角色管理器。 此缓存的 cookie 数据时仅使用主体的`IsInRole(roleName)`调用方法; 对角色 API 的直接调用总是涉及到对角色存储行程。 即使角色不缓存在 cookie 中，调用的主体对象`IsInRole(roleName)`方法通常更高效，是因为对于其缓存结果的第一次在请求的调用时。 角色 API，但是，不执行任何缓存。 因为`RowCreated`事件触发一次的每一行在 GridView 中，使用`User.IsInRole(roleName)`涉及对角色存储只是检索一次，而`Roles.IsUserInRole(roleName)`需要*N*行程，其中*N*是在网格中显示的用户帐户数。


编辑按钮`Visible`属性设置为`True`如果用户访问此页为管理员或主管角色; 否则它设置为`False`。 删除按钮`Visible`属性设置为`True`仅当用户是管理员角色中。

通过浏览器的此页进行测试。 作为匿名访问者或既主管，也没有管理员的用户访问页面，CommandField 为空;它仍然存在，但作为瘦薄片而无需编辑或删除按钮。

> [!NOTE]
> 可以隐藏 CommandField 完全时的非监督程序和非管理员为访问的页面。 我将此当作练习留给读者。


[![编辑和删除按钮处于隐藏状态为非监督和非管理员](role-based-authorization-vb/_static/image38.png)](role-based-authorization-vb/_static/image37.png)

**图 13**: 编辑和删除按钮处于隐藏状态为非监督和非管理员 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image39.png))


如果属于主管角色 （而不是属于管理员角色） 的用户访问，他会看到只有编辑按钮。


[![适用于在监督器编辑按钮时，删除按钮处于隐藏状态](role-based-authorization-vb/_static/image41.png)](role-based-authorization-vb/_static/image40.png)

**图 14**： 虽然的编辑按钮，可用于在监督器中，删除按钮处于隐藏状态 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image42.png))


如果管理员访问时，她有权编辑和删除按钮。


[![编辑和删除按钮才可用的管理员](role-based-authorization-vb/_static/image44.png)](role-based-authorization-vb/_static/image43.png)

**图 15**: 编辑和删除按钮仅可为管理员 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image45.png))


## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>步骤 3： 将基于角色的授权规则应用于类和方法

在步骤 2 中，我们仅限于编辑监督员和管理员角色中的用户的功能和删除功能仅对管理员。 这是通过隐藏未经授权的用户，通过编程技术的相关联的用户界面元素来实现。 此类度量值不能保证未经授权的用户将不能执行特权的操作。 可能有更高版本添加的用户界面元素或我们忘了要隐藏的未经授权的用户。 或黑客可能会发现通过其他方式来获取 ASP.NET 页后，可以执行所需的方法。

以确保未经授权的用户无法访问特定的一项功能的简单方法是来修饰该类或方法替换[`PrincipalPermission`属性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)。 当.NET 运行时使用的类或执行某一方法时，它将检查以确保当前的安全上下文拥有的权限。 `PrincipalPermission`属性提供了一种机制，通过它我们可以定义这些规则。

我们在使用`PrincipalPermission`属性返回<a id="_msoanchor_9"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程。 具体而言，我们已了解如何在修饰 GridView`SelectedIndexChanged`和`RowDeleting`事件处理程序，以便它们可以仅执行由经过身份验证的用户和 Tito，分别。 `PrincipalPermission`属性也适用的角色。

让我们来演示如何使用`PrincipalPermission`GridView 的特性`RowUpdating`和`RowDeleting`事件处理程序以禁止执行未经授权的用户。 我们需要做的就是添加在每个函数定义的相应属性：

[!code-vb[Main](role-based-authorization-vb/samples/sample13.vb)]

属性`RowUpdating`决定了事件处理程序，只有管理员或主管角色中的用户可以在为属性执行事件处理程序，`RowDeleting`中管理员的用户执行的事件处理程序限制角色。


> [!NOTE]
> `PrincipalPermission`属性表示为中的一个类`System.Security.Permissions`命名空间。 请务必添加`Imports System.Security.Permissions`顶部的代码隐藏类文件，以导入此命名空间的语句。


如果由于某种原因，非管理员尝试执行`RowDeleting`事件处理程序或如果要执行非监督程序或非管理员尝试`RowUpdating`事件处理程序，.NET 运行时将引发`SecurityException`。


[![如果未经授权的安全上下文来执行此方法，则将引发 SecurityException](role-based-authorization-vb/_static/image47.png)](role-based-authorization-vb/_static/image46.png)

**图 16**： 如果未经授权的安全上下文来执行此方法`SecurityException`引发 ([单击以查看实际尺寸的图像](role-based-authorization-vb/_static/image48.png))


除了 ASP.NET 页中，许多应用程序还具有包含各层，如业务逻辑和数据访问层的体系结构。 这些层通常作为类库实现，提供类和方法来执行业务逻辑和数据相关的功能。 `PrincipalPermission`属性是将授权规则应用到这些层也很有用。

有关使用的详细信息`PrincipalPermission`属性来定义类和方法上的授权规则，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[业务和数据层使用添加授权规则`PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>总结

在本教程中我们介绍了如何指定粗和细粒度授权规则基于用户的角色。 ASP。NET 的 URL 授权功能允许页面开发人员指定哪些标识允许或拒绝访问哪些页面。 返回中可以看到<a id="_msoanchor_10"> </a> [*基于用户的授权*](../membership/user-based-authorization-vb.md)教程中，URL 授权规则可以应用基于用户的用户。 它们也可以应用基于角色的角色，在本教程的步骤 1 中所示。

以声明方式或以编程方式，可能会应用细粒度授权规则。 在步骤 2 中介绍了使用 LoginView 控件 RoleGroups 功能可呈现基于来访用户角色的不同输出。 我们还了解了如何以编程方式确定用户是否属于特定角色以及如何相应地调整页面的功能。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [将授权规则添加到业务和数据层使用 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [检查 ASP.NET 2.0 的成员资格、 角色和配置文件： 使用角色](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [Asp.net 2.0 的安全问题列表](https://msdn.microsoft.com/library/ms998375.aspx)
- [技术文档`<roleManager>`元素](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢...

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者包括 Suchi Banerjee 和 Teresa Murphy。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](assigning-roles-to-users-vb.md)
