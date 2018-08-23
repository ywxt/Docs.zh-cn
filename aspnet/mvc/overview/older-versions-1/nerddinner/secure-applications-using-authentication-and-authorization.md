---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权保护应用程序 |Microsoft Docs
author: microsoft
description: 步骤 9 显示了如何添加身份验证和授权来保护我们 NerdDinner 的应用程序，以便用户需要注册并登录到要创建的网站...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d5f1b26312f11fd6d4ab500c7f24a4d89d428e38
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834251"
---
<a name="secure-applications-using-authentication-and-authorization"></a>使用身份验证和授权保护应用程序
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 9 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 9 显示了如何添加身份验证和授权来保护我们 NerdDinner 的应用程序，以便用户需要注册并登录到站点创建新 dinners，以及仅承载 dinner 的用户可以更高版本编辑它。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner 步骤 9： 身份验证和授权

现在我们 NerdDinner 应用程序授予任何人访问站点能够创建和编辑任何 dinner 的详细信息。 此项更改，以便用户需要注册并登录到要创建新 dinners，以便只有承载 dinner 的用户可以更高版本编辑添加的限制的站点。

若要启用此我们将使用身份验证和授权来保护我们的应用程序。

### <a name="understanding-authentication-and-authorization"></a>了解身份验证和授权

*身份验证*是标识和验证客户端访问应用程序身份的过程。 它更简单地说，是指确定""最终用户是谁在访问网站时。 ASP.NET 支持通过多种方式浏览器用户进行身份验证。 对于 Internet web 应用程序，使用最常用的身份验证方法称为"窗体身份验证"。 窗体身份验证使开发人员能够编写自己的应用程序中的 HTML 登录窗体，然后验证最终用户提交针对数据库或其他密码凭据存储区的用户名/密码。 如果用户名/密码组合不正确，开发人员然后可以要求 ASP.NET 发出的加密的 HTTP cookie，若要识别跨今后的请求的用户。 我们将通过与我们 NerdDinner 应用程序使用窗体身份验证。

*授权*是确定身份验证的用户是否有权限访问特定的 URL/资源或执行某些操作的过程。 例如，我们 NerdDinner 应用程序中我们将想要授权登录的用户可以访问 */Dinners/创建*URL，并创建新 Dinners。 我们还需要添加授权逻辑，以便只有承载 dinner 的用户可以其进行编辑，并拒绝所有其他用户编辑访问权限。

### <a name="forms-authentication-and-the-accountcontroller"></a>窗体身份验证和 AccountController

创建新的 ASP.NET MVC 应用程序时，ASP.NET MVC 的默认 Visual Studio 项目模板会自动启用窗体身份验证。 它还会自动向项目 – 可以非常轻松地将站点内的安全集成的预建的帐户登录页实现。

未经身份验证的用户可以访问它时，默认 Site.master 母版页在右上角站点显示"登录"链接：

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

单击"登录"链接可转到用户 */帐户/登录*URL:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

尚未注册的访问者可以通过单击"注册"链接 – 这些链接将转到此， */帐户/注册*URL，使他们可以输入帐户的详细信息：

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

单击"注册"按钮将创建新的用户在 ASP.NET 成员资格系统中，并使用窗体身份验证的站点到用户进行身份验证。

Site.master 登录的用户时，更改要输出"欢迎 [username] ！"的页的右上方 消息和呈现"注销"链接而不是"登录"一。 单击"注销"链接注销用户：

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

已添加到我们的项目的 Visual Studio 创建项目时的 AccountController 类中实现更高版本的登录、 注销和注册功能。 AccountController 的 UI 是使用视图模板 \Views\Account 目录中的实现的：

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 类使用 ASP.NET 窗体身份验证系统发出加密的身份验证 cookie 和 ASP.NET 成员资格 API 来存储和验证用户名/密码。 ASP.NET 成员资格 API 可扩展，并允许使用任何密码凭据存储区。 ASP.NET 附带了存储用户名/密码在 SQL 数据库中，或在 Active Directory 中的内置成员资格提供程序实现。

我们可以配置哪些成员资格提供程序，我们 NerdDinner 的应用程序应使用通过打开项目的根目录处的"web.config"文件并查找&lt;成员身份&gt;在其中的部分。 添加创建项目时的默认 web.config 注册 SQL 成员资格提供程序，并将其配置为使用名为"ApplicationServices"的连接字符串指定的数据库位置。

默认"ApplicationServices"连接字符串 (其内指定&lt;connectionStrings&gt; web.config 文件的部分) 配置为使用 SQL Express。 它指向 SQL Express 数据库名为"ASPNETDB。MDF"的应用程序下"应用\_数据"目录。 如果此数据库不存在第一次应用程序中使用成员资格 API，ASP.NET 会自动创建数据库和在其中将适当的成员身份数据库架构设置：

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

如果不使用 SQL Express 我们想要使用完整的 SQL Server 实例 （或连接到远程数据库），我们需要待办事项是更新 web.config 文件中的"ApplicationServices"连接字符串，请确保适当的成员身份架构已添加到它所指向的数据库。 你可以运行"aspnet\_regsql.exe"实用工具 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目录将成员身份和其他 ASP.NET 应用程序服务的相应架构添加到数据库中。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>授权使用 [Authorize] 筛选器的 Dinners/创建 URL

我们无需编写任何代码即可启用安全的身份验证和 NerdDinner 应用程序的帐户管理实现。 用户可以使用我们的应用程序和登录/注销的站点注册新帐户。

现在我们可以将授权逻辑添加到应用程序，并使用的身份验证状态和用户名的访问者的控制他们可以和不能在站点内执行操作。 让我们首先将授权逻辑添加到我们的 DinnersController 类的"创建"操作方法。 具体而言，我们将需要访问的用户 */Dinners/创建*必须登录 URL。 如果它们不会记录在我们将重定向，它们到登录页以便他们可以登录。

实现此逻辑是这么简单。 我们需要待办事项，只需将 [Authorize] 筛选器特性添加到我们创建的操作方法如下所示：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC 支持的功能，可创建"操作筛选器"可用于实现可以以声明方式应用于操作方法的可重用逻辑。 [Authorize] 筛选器是一个由 ASP.NET MVC 提供的内置操作筛选器，它使开发人员能够以声明方式将授权规则应用于操作方法和控制器类。

不带任何参数 （如上所述） 应用时执行操作方法请求的用户都必须登录 –，并且它会自动将浏览器重定向到登录名 URL 如果它们不是，强制实施的 [Authorize] 筛选器。 在执行此重定向最初请求的 URL 将作为查询字符串参数传递时 (例如: / 帐户/登录？ReturnUrl = %2fDinners %2fcreate)。 AccountController 将然后将用户重定向回最初请求的 URL 后登录。

[Authorize] 筛选器可以选择支持的功能，可以指定可用于要求，用户同时登录位于允许的用户或允许的安全角色的成员的列表中的"用户"或"角色"属性。 例如，下面的代码仅允许两个特定用户、"scottgu"和"billg"来访问 Dinners/创建 URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

嵌入代码中的特定用户名称通常不过是相当不易于维护。 更好的方法是定义更高级别的"角色"，检查代码，然后将用户映射到角色使用数据库或 active directory 系统 （启用要从代码外部存储的实际用户映射列表）。 ASP.NET 包括内置的角色管理 API，以及一组内置角色提供程序 （其中包括用于 SQL 和 Active Directory），可帮助执行此用户/角色映射。 然后，我们无法更新代码以仅允许特定的"管理员"角色中的用户访问 Dinners/创建 URL:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>创建时使用 User.Identity.Name 属性 Dinners

我们可以检索使用控制器基类上公开的 User.Identity.Name 属性的请求的当前登录的用户的用户名。

前面我们实现我们 create （） 操作方法的 HTTP POST 版本时我们具有硬编码为静态字符串 Dinner"HostedBy"属性。 我们可以立即更新此代码以改用 User.Identity.Name 属性，以及自动添加为主机创建 Dinner 的 RSVP:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

因为我们已添加到 create （） 方法的 [Authorize] 特性，可确保 ASP.NET MVC，操作方法才会执行用户访问 Dinners/创建 URL 中记录在站点上。 在这种情况下，User.Identity.Name 属性值将始终包含一个有效的用户名。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>编辑时使用 User.Identity.Name 属性 Dinners

现在让我们添加一些授权逻辑，可将用户限制，以便它们只能编辑他们自己承载的 dinners 属性。

若要帮助实现此目的，我们将首先到我们的 Dinner 对象 （在我们之前生成的 Dinner.cs 分部类） 中添加一个"IsHostedBy(username)"帮助程序方法。 此帮助器方法返回 true 或 false 具体取决于是否提供的用户名匹配的 Dinner HostedBy 属性，并封装执行不区分大小写的字符串比较它们所需的逻辑：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

我们然后将我们 DinnersController 类中对 edit （） 操作方法添加 [Authorize] 特性。 这将确保用户必须登录请求 */Dinners/编辑 / [id]* URL。

然后，我们可以将代码添加到我们使用 Dinner.IsHostedBy(username) 帮助器方法来验证登录的用户与 Dinner 主机的编辑方法。 如果用户不是主机，我们将显示"InvalidOwner"视图，并终止请求。 若要执行此操作的代码类似于下面：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

我们可以右键单击 \Views\Dinners 目录，然后选择添加-&gt;查看菜单命令来创建新的"InvalidOwner"视图。 我们将填充与该错误消息如下：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

和现在当用户尝试编辑不拥有 dinner，他们将获得一条错误消息：

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

控制器可以锁定，删除 Dinners，并确保只有 Dinner 主持人可以删除它的权限中，我们可以 delete （） 操作方法的重复相同的步骤。

### <a name="showinghiding-edit-and-delete-links"></a>显示/隐藏编辑和删除链接

我们要链接到我们的 DinnersController 类的编辑和删除操作方法的详细信息 url:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

目前，我们将演示不考虑到详细信息 URL 的访问者是否 dinner 的主机的编辑和删除操作链接。 让我们更改，以便只显示链接，如果正在访问的用户是 dinner 的所有者。

Details() 操作方法中我们 DinnersController 检索 Dinner 对象，然后将其作为模型对象中传递给视图模板：

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

我们可以更新视图模板来有条件地显示/隐藏编辑和删除链接使用 Dinner.IsHostedBy() 帮助器方法，如下所示：

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>后续步骤

让我们现在看看如何启用对使用 AJAX 的 dinner 的 RSVP 的已经过身份验证的用户。

> [!div class="step-by-step"]
> [上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)
