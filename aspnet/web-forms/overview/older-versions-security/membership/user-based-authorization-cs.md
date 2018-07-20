---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-cs
title: 基于用户的授权 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将查看限制对页的访问并限制在页面级别功能通过各种技术。
ms.author: aspnetcontent
ms.date: 01/18/2008
ms.assetid: 3c815a9e-2296-4b9b-b945-776d54989daa
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fe1dbc7e5fd609870975fbf41849522bbeed534
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823979"
---
<a name="user-based-authorization-c"></a>基于用户的授权 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_CS.zip)或[下载 PDF](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_cs.pdf)

> 在本教程中我们将查看限制对页的访问并限制在页面级别功能通过各种技术。


## <a name="introduction"></a>介绍

大多数 web 应用程序提供用户帐户的此部分来限制某些访问者访问网站内的某些网页中。 在大多数网上论坛站点，例如，-匿名和经过身份验证-的所有用户都都可以查看论坛帖子，但只有经过身份验证的用户可以访问 web 页后，可以创建新的帖子。 和可能存在才可供特定用户 （或一组特定的用户） 访问的管理页面。 此外，可以基于用户的用户不同页面级别的功能。 查看一系列文章，身份验证的用户显示的接口进行评分每篇文章，而此接口不供匿名访问者。

ASP.NET 简化了定义基于用户的授权规则。 通过一些中标记`Web.config`，以便它们仅可以访问指定的用户子集可以向下锁定特定 web 页面或整个目录。 页级别的功能可以打开或关闭基于当前登录的用户通过以编程方式和声明性方式。

在本教程中我们将查看限制对页的访问并限制在页面级别功能通过各种技术。 让我们进入正题！

## <a name="a-look-at-the-url-authorization-workflow"></a>查看 URL 授权工作流

如中所述[*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-cs.md)教程中，当 ASP.NET 运行时处理的请求，对于 ASP.NET 资源请求在其生命周期期间引发的事件数。 *HTTP 模块*是在响应特定事件在请求生命周期中执行其代码的托管的类。 ASP.NET 附带有多个执行的基本任务在后台的 HTTP 模块。

是这样一个 HTTP 模块[ `FormsAuthenticationModule` ](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)。 前面的教程中的主函数中所述`FormsAuthenticationModule`是确定当前请求的标识。 通过检查窗体身份验证票证，位于在 cookie 中或嵌入到 URL 中完成此操作。 此标识发生期间[`AuthenticateRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)。

另一个重要的 HTTP 模块，是[ `UrlAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)，这引发以响应[`AuthorizeRequest`事件](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)(之后会发生该情况`AuthenticateRequest`事件)。 `UrlAuthorizationModule`检查中的配置标记`Web.config`以确定当前的标识是否有权访问指定的页。 此过程称为*URL 授权*。

我们将介绍在步骤 1 中的 URL 授权规则的语法但首先让我们看看什么`UrlAuthorizationModule`does 具体取决于是否对请求进行授权或不。 如果`UrlAuthorizationModule`确定对请求进行授权，则它不执行任何操作，并请求将继续完成其生命周期。 但是，如果请求*不*获得授权，则`UrlAuthorizationModule`中止生命周期，并指示`Response`要返回对象[HTTP 401 未授权](http://www.checkupdown.com/status/E401.html)状态。 使用窗体身份验证时此 HTTP 401 状态从不返回到客户端因为如果`FormsAuthenticationModule`检测到 HTTP 401 状态是修改[HTTP 302 重定向](http://www.checkupdown.com/status/E302.html)到登录页。

图 1 所示的 ASP.NET 管道中，工作流`FormsAuthenticationModule`，和`UrlAuthorizationModule`未授权的请求到达时。 具体而言，图 1 显示了用于匿名访问者的请求`ProtectedPage.aspx`，这是一个页面，拒绝匿名用户访问。 访问者是匿名的因为`UrlAuthorizationModule`中止请求并返回 HTTP 401 未授权状态。 `FormsAuthenticationModule`然后转换为 401 状态 302 重定向到登录页。 用户进行身份验证通过登录页面后，他将重定向到`ProtectedPage.aspx`。 这一次`FormsAuthenticationModule`标识基于其身份验证票证的用户。 现在，访问者进行身份验证，`UrlAuthorizationModule`允许对页的访问。


[![窗体身份验证和 URL 授权工作流](user-based-authorization-cs/_static/image2.png)](user-based-authorization-cs/_static/image1.png)

**图 1**: 窗体身份验证和 URL 授权工作流 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image3.png))


图 1 所示的匿名访问者尝试访问不是提供给匿名用户的资源时出现的交互。 在这种情况下，匿名访问者重定向到登录页与她尝试访问在查询字符串中指定的页。 用户已成功登录后，系统会自动将她重定向回最初她正在尝试查看的资源。

此工作流时未经授权的请求由匿名用户，非常简单和轻松的访问者，若要了解已发生了什么情况及其原因。 但请记住`FormsAuthenticationModule`将重定向*任何*未经授权的用户到登录页上，即使通过身份验证的用户发出请求。 如果身份验证的用户尝试访问的页，可为其她缺少颁发机构，这可能导致令人困惑的用户体验。

假设我们的网站，必须配置其 URL 授权规则，以便在 ASP.NET 页`OnlyTito.aspx`是可访问仅向 Tito。 现在，假设 Sam 访问站点，登录，并将尝试访问`OnlyTito.aspx`。 `UrlAuthorizationModule`将暂停请求生命周期，并返回 HTTP 401 未授权的状态，其中`FormsAuthenticationModule`将检测，然后将 Sam 重定向到登录页。 由于 Sam 尚未登录，但是，她可能想知道为什么她已发送回登录页。 她可能原因，由于某种原因，她的登录凭据已丢失或她输入了无效凭据。 如果 Sam 重新输入其凭据从登录页面她将 （再次） 登录，并重定向到`OnlyTito.aspx`。 `UrlAuthorizationModule`会检测到 Sam 不能访问此页并她将返回到登录页。

图 2 描绘了此令人困惑的工作流。


[![默认工作流可能会导致令人困惑的周期](user-based-authorization-cs/_static/image5.png)](user-based-authorization-cs/_static/image4.png)

**图 2**: 默认工作流可能会导致混淆周期 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image6.png))


图 2 所示的工作流可以快速 befuddle 甚至大多数计算机技术精湛访问者。 我们将考察方法为防止这种混淆在步骤 2 中的周期。

> [!NOTE]
> ASP.NET 使用两种机制来确定当前用户是否可以访问特定的 web 页： URL 授权和文件授权。 由实现文件授权[ `FileAuthorizationModule` ](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)，用于确定颁发机构咨询服务的请求的文件的 Acl。 使用 Windows 身份验证最常使用文件授权，因为使用 Acl 是适用于 Windows 帐户的权限。 时使用的窗体身份验证，所有操作系统和文件系统级别请求都执行通过相同的 Windows 帐户，而不考虑用户访问网站。 由于本系列教程着重于窗体身份验证，我们将不会讨论文件授权。


### <a name="the-scope-of-url-authorization"></a>URL 授权作用域

`UrlAuthorizationModule`是托管代码的是 ASP.NET 运行时的一部分。 之前的 Microsoft 的版本 7 [Internet 信息服务 (IIS)](https://www.iis.net/) web 服务器没有 IIS 的 HTTP 管道，ASP.NET 运行时的管道之间的非重复障碍。 简单地说，在 IIS 6 和更早版本，ASP。NET 的`UrlAuthorizationModule`时请求从 IIS 委派给 ASP.NET 运行时才会执行。 默认情况下，IIS 处理类似 HTML 页面和 CSS、 JavaScript 和图像文件的静态内容本身的并仅将传送到 ASP.NET 运行时使用的扩展的页面时请求`.aspx`， `.asmx`，或`.ashx`请求。

IIS 7，但是，允许集成的 IIS 和 ASP.NET 管道。 使用几项配置设置，你可以设置 IIS 7 来调用`UrlAuthorizationModule`有关*所有*请求，这意味着，可以为任何类型的文件中定义 URL 授权规则。 此外，IIS 7 还包括其自己的 URL 授权引擎。 ASP.NET 集成和 IIS 7 本机 URL 授权功能的详细信息，请参阅[了解 IIS7 URL 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)。 有关 ASP.NET 和 IIS 7 集成更深入探讨，选取一份 Shahram Khosravi 书籍*Professional IIS 7 和 ASP.NET 集成编程*(ISBN: 978 0470152539)。

简单地说，在 IIS 7 之前的版本，URL 授权规则是仅应用于由 ASP.NET 运行时处理的资源。 但与 IIS 7 可以使用 IIS 的本机 URL 授权功能或集成 ASP。NET 的`UrlAuthorizationModule`到 IIS 的 HTTP 管道，从而将扩展到所有请求此功能。

> [!NOTE]
> 有一些细微但却很重要的差异，如何在 ASP。NET 的`UrlAuthorizationModule`和 IIS 7 的 URL 授权功能处理授权规则。 本教程不检查 IIS 7 的 URL 授权功能或如何分析相比的授权规则的差异`UrlAuthorizationModule`。 有关这些主题的详细信息，请参阅 MSDN 上或在 IIS 7 文档[www.iis.net](https://www.iis.net/)。


## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>步骤 1： 定义中的 URL 授权规则`Web.config`

`UrlAuthorizationModule`确定是否授予或拒绝访问请求的资源的基于应用程序的配置中定义的 URL 授权规则的特定标识。 授权规则中将逐一[`<authorization>`元素](https://msdn.microsoft.com/library/8d82143t.aspx)中的窗体`<allow>`和`<deny>`子元素。 每个`<allow>`和`<deny>`子元素可以指定：

- 特定用户
- 以逗号分隔的用户列表
- 所有匿名用户，由问号 （？） 表示
- 所有用户，为由一个星号 (\*)

以下标记演示了如何使用 URL 授权规则来允许用户 Tito 和 Scott 和拒绝所有其他：

[!code-xml[Main](user-based-authorization-cs/samples/sample1.xml)]

`<allow>`元素定义允许哪些用户-Tito 和 Scott-虽然`<deny>`元素指示*所有*用户被拒绝。

> [!NOTE]
> `<allow>`和`<deny>`元素还可以指定角色的授权规则。 我们将检查在将来的教程中基于角色的授权。


以下设置对 Sam （包括匿名访问者） 以外的任何人授予访问权限：

[!code-xml[Main](user-based-authorization-cs/samples/sample2.xml)]

若要允许仅经过身份验证的用户，请使用以下配置，它对所有匿名用户拒绝访问：

[!code-xml[Main](user-based-authorization-cs/samples/sample3.xml)]

中定义的授权规则`<system.web>`中的元素`Web.config`和适用于所有 web 应用程序中的 ASP.NET 资源。 通常，应用程序具有不同的授权规则的不同部分。 例如，在电子商务网站，所有访问者可能细读产品，请参阅产品评论、 搜索目录，等等。 但是，只有经过身份验证的用户可能会达到签出或要管理的发货历史记录的页面。 此外，可能存在才可通过选择用户，例如网站管理员访问的站点的部分。

ASP.NET 简化了在站点中定义不同的文件和文件夹的不同的授权规则。 指定的根文件夹中的授权规则`Web.config`文件将应用于站点中的所有 ASP.NET 资源。 但是，这些默认授权设置可以通过为特定文件夹添加`Web.config`与`<authorization>`部分。

让我们更新我们的网站，以便只有经过身份验证的用户可以访问中的 ASP.NET 页`Membership`文件夹。 若要完成此我们需要添加`Web.config`文件为`Membership`文件夹并设置其授权的设置以拒绝匿名用户。 右键单击`Membership`文件夹在解决方案资源管理器，从上下文菜单中，选择添加新项菜单上，并添加名为新的 Web 配置文件`Web.config`。


[![将 Web.config 文件添加到成员资格文件夹](user-based-authorization-cs/_static/image8.png)](user-based-authorization-cs/_static/image7.png)

**图 3**： 添加`Web.config`的文件`Membership`文件夹 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image9.png))


此时你的项目应包含两个`Web.config`文件： 一个在根目录下，一个在`Membership`文件夹。


[![你的应用程序现在应包含两个 Web.config 文件](user-based-authorization-cs/_static/image11.png)](user-based-authorization-cs/_static/image10.png)

**图 4**： 您应用程序应现在包含两个`Web.config`文件 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image12.png))


更新配置文件中的`Membership`文件夹，以便它不允许匿名用户访问权限。

[!code-xml[Main](user-based-authorization-cs/samples/sample4.xml)]

这就是一切就这么简单 ！

若要测试此更改，访问在浏览器主页并确保您已注销。由于 ASP.NET 应用程序的默认行为是允许所有访问者，并且由于我们没有进行到根目录的任何授权修改`Web.config`文件中，我们将能够访问作为匿名访问者的根目录中的文件。

单击创建用户帐户链接的左侧列中找到。 这会转到`~/Membership/CreatingUserAccounts.aspx`。 由于`Web.config`文件中`Membership`文件夹定义的授权规则，以禁止匿名访问，`UrlAuthorizationModule`中止请求并返回 HTTP 401 未授权状态。 `FormsAuthenticationModule`此到 302 重定向状态中，向我们发送到登录页进行了修改。 请注意，页面我们已尝试访问 (`CreatingUserAccounts.aspx`) 传递到登录页通过`ReturnUrl`查询字符串参数。


[![自 URL 授权规则禁止匿名访问，我们将重定向到登录页](user-based-authorization-cs/_static/image14.png)](user-based-authorization-cs/_static/image13.png)

**图 5**： 由于 URL 授权规则禁止匿名访问，我们将重定向到登录页 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image15.png))


在成功登录后, 我们将重定向到`CreatingUserAccounts.aspx`页。 这一次`UrlAuthorizationModule`允许对页的访问，因为我们无法再匿名。

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>应用到特定位置的 URL 授权规则

中定义的授权设置`<system.web>`一部分`Web.config`适用于所有该目录及其子目录中的 ASP.NET 资源 (否则由另一个重写之前`Web.config`文件)。 在某些情况下，不过，我们可能想给定目录以获得一个或两个特定页除外的特定授权配置中的所有 ASP.NET 资源。 这可以通过添加`<location>`中的元素`Web.config`、 指向其授权规则各不相同，文件和其中定义其唯一的授权规则。

若要演示如何使用`<location>`元素来重写特定资源的配置设置，让我们自定义授权设置，以便可以访问仅 Tito `CreatingUserAccounts.aspx`。 若要完成此操作，添加`<location>`元素`Membership`文件夹的`Web.config`文件并更新其标记，以便它看起来如下所示：

[!code-xml[Main](user-based-authorization-cs/samples/sample5.xml)]

`<authorization>`中的元素`<system.web>`定义中的 ASP.NET 资源的默认 URL 授权规则`Membership`文件夹及其子文件夹。 `<location>`元素可用于重写这些特定资源的规则。 在上面的标记`<location>`元素引用`CreatingUserAccounts.aspx`页上，并指定其的授权规则允许 Tito，例如但拒绝其他所有人。

若要测试此授权更改，首先访问作为匿名用户网站。 如果你尝试访问中的任意页面`Membership`文件夹，如`UserBasedAuthorization.aspx`，则`UrlAuthorizationModule`将拒绝该请求将重定向到登录页。 作为说，Scott，登录后，您可以访问中的任何网页`Membership`文件夹*除*为`CreatingUserAccounts.aspx`。 尝试访问`CreatingUserAccounts.aspx`以任何人登录但 Tito 会导致未经授权的访问尝试，将你重定向回登录页。

> [!NOTE]
> `<location>`元素必须出现在配置的之外`<system.web>`元素。 您需要使用一个单独`<location>`你想要重写其授权设置的每个资源的元素。


### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>如何查看`UrlAuthorizationModule`使用授权规则来允许或拒绝访问

`UrlAuthorizationModule`确定通过分析 URL 授权特定的 URL 授权特定的标识，使规则是否一次，从第一个开始并一路一个。 一旦找到匹配项，授予或拒绝访问用户，具体取决于在找到匹配项`<allow>`或`<deny>`元素。 <strong>如果不找到任何匹配项，则该用户被授予访问权限。</strong> 因此，如果你想要限制访问，则必须使用`<deny>`URL 授权配置中的最后一个元素的元素。 <strong>如果省略</strong><strong>`<deny>`</strong><strong>元素中，所有用户将被都授予访问权限。</strong>

若要更好地了解使用的过程`UrlAuthorizationModule`若要确定颁发机构，请考虑示例探讨了之前在此步骤中的 URL 授权规则。 第一个规则是`<allow>`元素，它允许对 Tito 和 Scott 的访问。 第二个规则是`<deny>`每个人都拒绝访问的元素。 如果匿名用户访问时，`UrlAuthorizationModule`通过询问，开始为匿名 Scott 或 Tito？ 答案很明显，是不可以，因此它将继续进行第二个规则。 是匿名的每个人都集中？ 因为答案此处是肯定的`<deny>`有效放置规则和访问者重定向到登录页。 同样，如果访问 Jisun，`UrlAuthorizationModule`首先会询问是 Jisun Scott 或 Tito？ 由于她不可以，`UrlAuthorizationModule`继续到第二个问题，在集中的每个人都是 Jisun？ 她是，因此，她也被拒绝访问。 最后，如果 Tito 访问时，第一个问题带来的`UrlAuthorizationModule`是肯定应答，因此 Tito 被授予访问权限。

由于`UrlAuthorizationModule`授权规则从上到下停止在任何匹配项，务必要具有更具体的规则之前不太特定的进程。 即，定义禁止 Jisun 和匿名用户，但允许所有其他身份验证的用户的授权规则，则将使用最具体的规则-一个会影响 Jisun-启动并继续更具体的规则 — 允许所有其他那些经过身份验证的用户，但拒绝所有匿名用户。 以下 URL 授权规则通过首先拒绝 Jisun，，然后拒绝任何匿名用户来实现此策略。 Jisun 以外的任何经过身份验证的用户将被授予访问因为这两个命令`<deny>`语句将匹配。

[!code-xml[Main](user-based-authorization-cs/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>步骤 2： 修复工作流的未经授权的、 经过身份验证的用户

如我们在本教程中的对比介绍 URL 授权工作流部分前面所述，随时怎样未授权的请求，`UrlAuthorizationModule`中止请求并返回 HTTP 401 未授权状态。 通过修改此 401 状态`FormsAuthenticationModule`到 302 重定向到登录页会将用户的状态。 即使用户进行身份验证，任何未经授权的请求，会出现此工作流。

返回到登录页的身份验证的用户很可能将它们相混淆，因为用户已登录到系统。 借助极少量的工作，我们可以改进此工作流通过将经过身份验证的用户说明他们已尝试访问受限的页面的页面进行未经授权的请求重定向。

首先在名为 web 应用程序的根文件夹中创建一个新的 ASP.NET 页面`UnauthorizedAccess.aspx`; 别忘了将使用此页相关联`Site.master`母版页。 在创建后此页上，删除引用的内容控件`LoginContent`ContentPlaceHolder 以便主页面的默认内容将显示。 接下来，添加一条消息，说明了这种情况，即用户尝试访问受保护的资源。 在添加此类消息之后,`UnauthorizedAccess.aspx`页面的声明性标记应如下所示：

[!code-aspx[Main](user-based-authorization-cs/samples/sample7.aspx)]

现在，我们需要更改工作流，因此，如果通过身份验证的用户来执行未授权的请求发送到`UnauthorizedAccess.aspx`页而不是登录页。 将未经授权的请求重定向到登录页的逻辑隐藏的私有方法中的信息`FormsAuthenticationModule`类，因此我们不能自定义此行为。 我们可以做什么，但是，是将我们自己的逻辑添加到重定向到用户的登录页`UnauthorizedAccess.aspx`，如果需要。

当`FormsAuthenticationModule`未经授权的访问者将重定向到登录页将追加到名称与在查询字符串的请求、 未经授权 URL `ReturnUrl`。 例如，如果未经授权的用户尝试访问`OnlyTito.aspx`，则`FormsAuthenticationModule`会将其重定向到`Login.aspx?ReturnUrl=OnlyTito.aspx`。 因此，如果通过使用查询字符串包含身份验证的用户访问登录页`ReturnUrl`参数，则我们知道此未经身份验证的用户只需尝试访问她无权查看的页面。 在这种情况下，我们想要重定向到她`UnauthorizedAccess.aspx`。

若要完成此操作，请将以下代码添加到登录页`Page_Load`事件处理程序：

[!code-csharp[Main](user-based-authorization-cs/samples/sample8.cs)]

上面的代码将重定向到经过身份验证、 未经授权用户`UnauthorizedAccess.aspx`页。 若要查看此逻辑在操作中的，请访问作为匿名访问者的站点，并单击左侧列中的创建用户帐户链接。 这会转到`~/Membership/CreatingUserAccounts.aspx`页，它在步骤 1 中我们配置为仅允许访问 Tito。 由于匿名用户禁止的因此`FormsAuthenticationModule`将我们重定向回登录页。

此时，我们已匿名，因此`Request.IsAuthenticated`将返回`false`我们将不会重定向到`UnauthorizedAccess.aspx`。 相反，将显示登录页。 Tito，如 Bruce 以外的用户登录。 输入相应凭据之后, 的登录页将重定向我们回到`~/Membership/CreatingUserAccounts.aspx`。 但是，此页才可以访问 Tito，因为我们无权查看它，并立即返回到登录页。 但是，这次`Request.IsAuthenticated`返回`true`(和`ReturnUrl`存在查询字符串参数)，因此我们将重定向到`UnauthorizedAccess.aspx`页。


[![经过身份验证，未经授权的用户将会重定向到 UnauthorizedAccess.aspx](user-based-authorization-cs/_static/image17.png)](user-based-authorization-cs/_static/image16.png)

**图 6**： 经过身份验证，未经授权的用户将会重定向到`UnauthorizedAccess.aspx`([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image18.png))


此自定义工作流短路循环如下图 2 展示更合理、 简单的用户体验。

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>步骤 3： 限制基于当前登录的用户功能

URL 授权轻松指定粗略的授权规则。 正如我们在步骤 1 中看到的使用 URL 授权我们可以用于简单地说明允许哪些标识以及哪些拒绝查看文件夹中的特定页面或所有页面。 在某些情况下，但是，我们可能想要允许所有用户访问页上，但限制基于用户访问它的页面的功能。

请考虑使经过身份验证的访问者可以查看他们的产品的电子商务网站的情况。 当某个匿名用户访问产品页时，他们将看到的产品信息并不会有机会在留下评论。 但是，身份验证的用户访问相同的页面会检查接口。 如果已经过身份验证的用户具有未审阅此产品，该接口允许他们才能提交评审;否则它会显示它们提供其先前所提交的审阅。 若要退后一步，这种情况下进一步，产品页可能会显示其他信息并提供扩展的功能为这些用户的电子商务公司工作。 例如，产品页可能会列出库存清单并包含用于编辑产品的价格和描述供员工访问时选项。

可以以声明方式或以编程方式 （或某些结合在一起的两个），可以实现此类精细授权规则。 下一节中，我们将了解如何实现通过登录视图控件的细粒度授权。 接下来，我们将探讨编程技术。 我们可以看看应用细粒度授权规则之前，但是，我们首先需要创建它的功能取决于用户访问它的页面。

让我们创建一个页面，其中列出了在 GridView 中特定目录中的文件。 GridView 将列出每个文件的名称、 大小和其他信息，以及包含的 Linkbutton 的两个列： 一个标题为视图和一个名为的 Delete。 如果单击视图 LinkButton，则将显示所选文件的内容;如果单击删除 LinkButton 时，将删除该文件。 让我们最初创建此页，以便其视图和删除功能可供所有用户如此。 在使用中，我们将了解如何启用或禁用这些功能根据用户访问的页面的 LoginView 控件和以编程方式限制功能部分。

> [!NOTE]
> 我们将要构建的 ASP.NET 页使用 GridView 控件来显示文件的列表。 本教程系列重点介绍窗体身份验证、 授权、 用户帐户和角色，因为我不想花费太多时间来讨论 GridView 控件的内部工作机制。 虽然本教程提供了特定设置此页的分步说明，它不会不研究一下为什么未进行某些选择，或影响特定属性对呈现的输出的详细信息。 GridView 控件的全面介绍，请查阅我*[使用 ASP.NET 2.0 中的数据](../../data-access/index.md)* 系列教程。


首先打开`UserBasedAuthorization.aspx`文件中`Membership`文件夹，然后将 GridView 控件添加到名为页`FilesGrid`。 从 GridView 的智能标记上，单击编辑列链接以启动字段对话框。 在这里，取消选中自动生成字段中的复选框左下角。 接下来，添加选择按钮、 删除按钮和两个 BoundFields 从左上角 （选择和删除按钮可以 CommandField 类型下找到）。 设置选择按钮`SelectText`属性设置为视图和第一个 BoundField`HeaderText`和`DataField`名称的属性。 设置第二个 BoundField`HeaderText`属性设置为大小 （字节），其`DataField`属性设置为长度，其`DataFormatString`属性设置为{0:N0}并将其`HtmlEncode`属性设置为 False。

配置后 GridView 的列，单击确定关闭字段对话框。 从属性窗口中，设置 GridView`DataKeyNames`属性设置为`FullName`。 此时 GridView 的声明性标记应如下所示：

[!code-aspx[Main](user-based-authorization-cs/samples/sample9.aspx)]

使用 GridView 的标记中创建，我们就可以编写的代码会检索特定目录中的文件，并将其绑定到 GridView。 将以下代码添加到页面的`Page_Load`事件处理程序：

[!code-csharp[Main](user-based-authorization-cs/samples/sample10.cs)]

上面的代码中使用[`DirectoryInfo`类](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx)若要获取的应用程序的根文件夹中的文件列表。 [ `GetFiles()`方法](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx)返回的所有文件的目录中数组的形式[`FileInfo`对象](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)，后者然后绑定到 GridView。 `FileInfo`对象包含具有多种类型的属性，例如`Name`， `Length`，和`IsReadOnly`，等等。 您可以看到从其声明性标记，只需显示 GridView`Name`和`Length`属性。

> [!NOTE]
> `DirectoryInfo`并`FileInfo`中找到类[`System.IO`命名空间](https://msdn.microsoft.com/library/system.io.aspx)。 因此，您需要为其命名空间名称与这些类名称的前面加上或具有到类文件导入的命名空间 (通过`using System.IO`)。


请花费片刻时间来访问此页，通过浏览器。 它会显示驻留在应用程序的根目录中的文件的列表。 单击任何视图或删除 Linkbutton 将引起回发，但不发生任何操作，因为我们尚未为创建必要的事件处理程序。


[![GridView 列出了 Web 应用程序的根目录中的文件](user-based-authorization-cs/_static/image20.png)](user-based-authorization-cs/_static/image19.png)

**图 7**: GridView 列出了 Web 应用程序的根目录中的文件 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image21.png))


我们需要一种方法来显示所选文件的内容。 返回到 Visual Studio 并添加名为文本框`FileContents`上面 GridView。 设置其`TextMode`属性设置为`MultiLine`并将其`Columns`和`Rows`为 95%和 10，属性分别。

[!code-aspx[Main](user-based-authorization-cs/samples/sample11.aspx)]

接下来，为 GridView 的创建事件处理程序[`SelectedIndexChanged`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx)并添加以下代码：

[!code-csharp[Main](user-based-authorization-cs/samples/sample12.cs)]

此代码使用 GridView 的`SelectedValue`属性来确定所选文件的完整文件名。 在内部，`DataKeys`以获取引用集合`SelectedValue`，因此必须设置 GridView 的`DataKeyNames`为名称，如之前在此步骤中所述的属性。 [ `File`类](https://msdn.microsoft.com/library/system.io.file.aspx)用于所选的文件的内容读入一个字符串，然后分配给`FileContents`文本框的`Text`属性，从而显示页面上所选文件的内容。


[![在文本框中显示所选文件的内容](user-based-authorization-cs/_static/image23.png)](user-based-authorization-cs/_static/image22.png)

**图 8**： 在文本框中显示所选文件的内容 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image24.png))


> [!NOTE]
> 如果您查看包含 HTML 标记的文件的内容，然后尝试查看或删除的文件，则会收到`HttpRequestValidationException`错误。 这是因为在回发时将文本框的内容发送回 web 服务器。 默认情况下，ASP.NET 将引发`HttpRequestValidationException`错误，每当检测到潜在的危险回发的内容，例如 HTML 标记。 若要禁用的发生此错误，关闭请求验证页通过添加`ValidateRequest="false"`到`@Page`指令。 有关优点的详细信息，以及哪些预防措施应执行时的请求验证的禁用它，阅读[请求验证-阻止脚本攻击](https://asp.net/learn/whitepapers/request-validation/)。


最后，将事件处理程序使用以下代码添加为 GridView [ `RowDeleting`事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx):

[!code-csharp[Main](user-based-authorization-cs/samples/sample13.cs)]

该代码只是显示要删除中的文件的全名`FileContents`文本框*而无需*实际删除该文件。


[![单击删除按钮不会实际删除该文件](user-based-authorization-cs/_static/image26.png)](user-based-authorization-cs/_static/image25.png)

**图 9**： 单击删除按钮不会实际删除的文件 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image27.png))


我们在步骤 1 中配置 URL 授权规则，以禁止匿名用户查看中的页`Membership`文件夹。 为了更好地表现出细粒度身份验证，让我们允许匿名用户访问`UserBasedAuthorization.aspx`页上，但使用有限的功能。 若要打开此页以的所有用户访问，添加以下`<location>`元素`Web.config`文件中`Membership`文件夹：

[!code-xml[Main](user-based-authorization-cs/samples/sample14.xml)]

添加这后`<location>`元素中，通过从该站点的日志记录来测试新的 URL 授权规则。 作为匿名用户，应允许访问`UserBasedAuthorization.aspx`页。

目前，任何经过身份验证或匿名用户可以访问`UserBasedAuthorization.aspx`页并查看或删除文件。 让它，以便只有经过身份验证的用户可以查看文件的内容和仅 Tito 删除文件。 以声明方式、 以编程方式或通过组合使用这两种方法，可以应用此类精细授权规则。 让我们使用声明性方法来限制谁可以查看文件; 的内容我们将使用编程方法来限制可以删除文件。

### <a name="using-the-loginview-control"></a>使用 LoginView 控件

如我们在过去的教程中所见，LoginView 控件可用于显示已经过身份验证和匿名用户，不同的接口，提供简单的方法来隐藏不能由匿名用户访问的功能。 由于匿名用户无法查看或删除文件，我们只需显示`FileContents`文本框时通过身份验证的用户访问页面时。 若要实现此目的，将 LoginView 控件添加到页，将其命名`LoginViewForFileContentsTextBox`，并移动`FileContents`LoginView 控件到文本框中的声明性标记`LoggedInTemplate`。

[!code-aspx[Main](user-based-authorization-cs/samples/sample15.aspx)]

登录视图的模板中的 Web 控件不再从代码隐藏类直接访问。 例如， `FilesGrid` GridView`SelectedIndexChanged`并`RowDeleting`事件处理程序当前引用`FileContents`TextBox 控件，代码如：

[!code-csharp[Main](user-based-authorization-cs/samples/sample16.cs)]

但是，此代码将不再有效。 通过移动`FileContents`文本框中的为`LoggedInTemplate`文本框不能直接访问。 相反，我们必须使用`FindControl("controlId")`方法以编程方式引用该控件。 更新`FilesGrid`引用文本框中的事件处理程序如下所示：

[!code-csharp[Main](user-based-authorization-cs/samples/sample17.cs)]

之后将文本框移动到 LoginView`LoggedInTemplate`和页面的代码更新为引用文本框使用`FindControl("controlId")`模式，请访问作为匿名用户页。 如图 10 所示，`FileContents`不显示文本框。 但是，仍显示视图 LinkButton。


[![LoginView 控件只呈现 FileContents 文本框中的身份验证的用户](user-based-authorization-cs/_static/image29.png)](user-based-authorization-cs/_static/image28.png)

**图 10**: LoginView 控件只呈现`FileContents`文本框中的身份验证的用户 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image30.png))


若要隐藏的匿名用户视图按钮的一种方法是 GridView 字段转换为 TemplateField。 这将生成的视图 LinkButton 包含声明性标记的模板。 我们然后可以将 LoginView 控件添加到 TemplateField 并将放置内 LoginView 的 LinkButton `LoggedInTemplate`，从而隐藏从匿名访问者视图按钮。 若要完成此操作，单击 GridView 的智能标记以启动字段对话框中的编辑列链接。 接下来，从列表中较低的左上角选择选择按钮，然后单击转换为 TemplateField 链接此字段。 执行此操作将修改该字段的声明性标记中：

[!code-aspx[Main](user-based-authorization-cs/samples/sample18.aspx)]

 到: 

[!code-aspx[Main](user-based-authorization-cs/samples/sample19.aspx)]

此时，我们可以将登录视图添加到 TemplateField。 以下标记显示视图 LinkButton 仅适用于已经过身份验证的用户。

[!code-aspx[Main](user-based-authorization-cs/samples/sample20.aspx)]

如图 11 所示，最终结果是不，非常作为视图列仍显示即使视图 Linkbutton 列中处于隐藏状态。 我们将在下一部分探讨如何隐藏整个 GridView 列 （和不只是 LinkButton）。


[![LoginView 控件隐藏视图 Linkbutton 的匿名访问者](user-based-authorization-cs/_static/image32.png)](user-based-authorization-cs/_static/image31.png)

**图 11**: LoginView 控件对于匿名访问者隐藏视图 Linkbutton ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image33.png))


### <a name="programmatically-limiting-functionality"></a>以编程方式限制功能

在某些情况下，声明性技术是不足，无法限制到页面的功能。 例如，某些页面功能的可用性可能依赖于之外访问的页面，用户是匿名或经过身份验证的条件。 在这种情况下，可以显示或隐藏通过编程方式的各种用户界面元素。

若要以编程方式限制功能，我们需要执行两项任务：

1. 确定用户访问的页面是否可以访问功能，并
2. 以编程方式修改基于用户是否有权访问相关的功能的用户界面。

若要演示这两项任务的应用程序，让我们仅允许 Tito GridView 从删除文件。 然后，我们的第一个任务是确定它是否是 Tito 访问的页面。 一旦已确定的我们需要隐藏 （或显示） GridView 的删除列。 GridView 列都可通过访问其`Columns`属性; 如果仅呈现一列及其`Visible`属性设置为`true`（默认值）。

将以下代码添加到`Page_Load`之前将数据绑定到 GridView 的事件处理程序：

[!code-csharp[Main](user-based-authorization-cs/samples/sample21.cs)]

如中所述[*概述的窗体身份验证*](../introduction/an-overview-of-forms-authentication-cs.md)教程中，`User.Identity.Name`返回标识的名称。 这对应于登录名控件中输入的用户名。 如果它是访问的页面，GridView 的第二列的 Tito`Visible`属性设置为`true`; 否则为设置为`false`。 最终结果是，当 Tito 以外的其他人访问页上，另一个身份验证的用户或匿名用户，删除列不呈现 （见图 12）;但是，当 Tito 访问该页面，删除列是存在 （请参阅图 13）。


[![删除列是不呈现时访问过的人以外的其他 Tito （如 Bruce)](user-based-authorization-cs/_static/image35.png)](user-based-authorization-cs/_static/image34.png)

**图 12**: 删除的列是不呈现时访问过的人以外的其他 Tito （如 Bruce) ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image36.png))


[![删除列呈现为 Tito](user-based-authorization-cs/_static/image38.png)](user-based-authorization-cs/_static/image37.png)

**图 13**： 为 Tito 呈现删除列 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image39.png))


## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>步骤 4： 将授权规则应用于类和方法

在步骤 3 中我们不允许匿名用户查看文件的内容，并禁止所有用户，但 Tito 删除文件。 这是通过隐藏的关联的用户界面元素为未经授权的访问者通过声明性和编程技术来实现。 简单示例中，正确隐藏用户界面元素是很简单，但如何更为复杂的网站在可能存在多种不同方式执行相同的功能？ 在限制的未经授权的用户的该功能，会发生什么情况如果我们忘了隐藏或禁用的所有适用的用户界面元素？

以确保未经授权的用户无法访问特定的一项功能的简单方法是来修饰该类或方法替换[`PrincipalPermission`属性](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)。 当.NET 运行时使用的类或执行某一方法时，它将检查以确保当前的安全上下文有权使用类或执行方法。 `PrincipalPermission`属性提供了一种机制，通过它我们可以定义这些规则。

让我们来演示如何使用`PrincipalPermission`GridView 的特性`SelectedIndexChanged`和`RowDeleting`分别禁止匿名用户和用户而不是 Tito，将执行的事件处理程序。 我们需要做的就是添加在每个函数定义的相应属性：

[!code-csharp[Main](user-based-authorization-cs/samples/sample22.cs)]

属性`SelectedIndexChanged`事件处理程序指示只有经过身份验证的用户可以执行事件处理程序，其中为属性`RowDeleting`事件处理程序限制到 Tito 执行。

如果由于某种原因，Tito 以外的用户尝试执行`RowDeleting`事件处理程序或未经身份验证的用户尝试执行`SelectedIndexChanged`事件处理程序，.NET 运行时将引发`SecurityException`。


[![如果未经授权的安全上下文来执行此方法，则将引发 SecurityException](user-based-authorization-cs/_static/image41.png)](user-based-authorization-cs/_static/image40.png)

**图 14**： 如果未经授权的安全上下文来执行此方法`SecurityException`引发 ([单击以查看实际尺寸的图像](user-based-authorization-cs/_static/image42.png))


> [!NOTE]
> 若要允许多个安全上下文来访问类或方法，修饰的类或方法使用`PrincipalPermission`为每个安全上下文的属性。 也就是说，以允许 Tito 和 Bruce 执行`RowDeleting`事件处理程序中，添加*两个*`PrincipalPermission`属性：


[!code-csharp[Main](user-based-authorization-cs/samples/sample23.cs)]

除了 ASP.NET 页中，许多应用程序还具有包含各层，如业务逻辑和数据访问层的体系结构。 这些层通常作为类库实现，提供类和方法来执行业务逻辑和数据相关的功能。 `PrincipalPermission`属性可用于将授权规则应用于这些层。

有关使用的详细信息`PrincipalPermission`属性来定义类和方法上的授权规则，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章[业务和数据层使用添加授权规则`PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>总结

在本教程中我们介绍了如何应用基于用户的授权规则。 我们开始使用 ASP 一看。NET 的 URL 授权框架。 在每个请求时，ASP.NET 引擎的`UrlAuthorizationModule`检查以确定是否授权该标识来访问所请求的资源的应用程序的配置中定义的 URL 授权规则。 简单地说，URL 授权可以轻松地指定特定目录中的授权规则的特定页面或所有页面。

URL 授权框架根据按页应用授权规则。 使用 URL 授权时，有权访问特定资源或不请求标识。 许多情况下，但是，调用细粒度的更多授权规则。 而不是定义谁有权访问的页面，我们可能需要让所有人访问的页面，但显示不同的数据或提供不同的功能，具体取决于用户访问的页面。 页级授权通常涉及到隐藏特定的用户界面元素，以防止未经授权的用户访问被禁止的功能。 此外，就可以使用属性来限制对类和某些用户及其方法的执行访问。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [将授权规则添加到业务和数据层使用 `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 授权](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6 与 IIS7 安全之间的更改](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [配置特定的文件和子目录](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [限制基于用户的数据修改功能](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs.md)
- [LoginView 控件快速入门](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [了解 IIS7 URL 授权](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 技术文档](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [使用 ASP.NET 2.0 中的数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)。

> [!div class="step-by-step"]
> [上一页](validating-user-credentials-against-the-membership-user-store-cs.md)
> [下一页](storing-additional-user-information-cs.md)
