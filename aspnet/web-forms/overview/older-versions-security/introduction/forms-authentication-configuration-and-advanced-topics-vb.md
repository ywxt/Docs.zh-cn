---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: 窗体身份验证配置和高级的主题 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将检查各种窗体身份验证设置，并了解如何通过窗体元素对其进行修改。 这将需要一个详细...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/14/2008
ms.topic: article
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: 493cb81271ea1c0439f7b499c5b48e659d3589b5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390856"
---
<a name="forms-authentication-configuration-and-advanced-topics-vb"></a>窗体身份验证配置和高级的主题 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip)或[下载 PDF](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> 在本教程中我们将检查各种窗体身份验证设置，并了解如何通过窗体元素对其进行修改。 这将需要自定义窗体身份验证票证超时值，使用自定义 URL （例如 SignIn.aspx 而不是 login.aspx 的情况) 和无 cookie forms 身份验证票证的登录页的详细的信息。


## <a name="introduction"></a>介绍

在中[前一篇教程](an-overview-of-forms-authentication-vb.md)，我们介绍了在 ASP.NET 应用程序，从 Web.config 中指定配置设置要在页中显示不同创建日志中实现窗体身份验证所必需的步骤用户经过身份验证和匿名用户的内容。 回想一下，我们将此网站配置为使用窗体身份验证的模式属性设置&lt;身份验证&gt;向窗体元素。 &lt;身份验证&gt;元素可以根据需要包含&lt;窗体&gt;子元素，可以通过它指定具有多种类型的窗体身份验证设置。

在本教程中我们将检查各种窗体身份验证设置，并了解如何通过修改&lt;窗体&gt;元素。 这将需要自定义窗体身份验证票证超时值，使用自定义 URL （例如 SignIn.aspx 而不是 login.aspx 的情况) 和无 cookie forms 身份验证票证的登录页的详细的信息。 我们将更加仔细地检查窗体身份验证票证的构成，并请参阅 ASP.NET 所需确保票证的数据安全的即使检查和篡改的预防措施。 最后，我们将考察如何将额外的用户数据存储在窗体身份验证票证以及如何通过自定义主体对象的此数据进行建模。

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>第 1 步： 检查&lt;窗体&gt;配置设置

在 ASP.NET 中的窗体身份验证系统提供多种可自定义应用程序的应用程序基础的配置设置。 这包括设置，例如： 票证生存期的窗体身份验证;哪种保护应用于票证;在哪些条件无 cookie 身份验证票证都使用;登录页中; 的路径和其他信息。 若要修改的默认值，添加[&lt;窗体&gt;元素](https://msdn.microsoft.com/library/1d3t3c61.aspx)的小孩[&lt;身份验证&gt;元素](https://msdn.microsoft.com/library/532aee0e.aspx)，指定这些属性想要自定义为 XML 属性的值如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

表 1 总结了可以通过自定义的属性&lt;窗体&gt;元素。 Web.config 是一个 XML 文件，因为左侧列中的属性名称是区分大小写。


| <strong>特性</strong> |                                                                                                                                                                                                                                     <strong>说明</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         无 cookie         |                                                                                                                此属性指定在什么条件下的身份验证票证存储在与要在 URL 中嵌入的 cookie。 允许的值为： UseCookies;UseUri;自动检测;和 UseDeviceProfile （默认值）。 步骤 2 检查更多详细信息中的此设置。                                                                                                                |
|         defaultUrl         |                                                                                                                                                         指示用户将重定向到登录后从登录页如果不存在 RedirectUrl 值在查询字符串中指定的 URL。 默认值为 default.aspx。                                                                                                                                                         |
|           域           | 当使用基于 cookie 的身份验证票证，此设置指定 cookie s 域值。 默认值为空字符串，这会导致浏览器使用从该情况下，它已签发 （如 www.yourdomain.com) 的域。 在这种情况下，将 cookie<strong>不</strong>到子域，例如 admin.yourdomain.com 进行请求时发送。 如果您想要传递给自定义将其设置为 yourdomain.com 域的属性所需的所有子域的 cookie。 |
|  enableCrossAppRedirects   |                                                                                                                                                                   一个布尔值，该值指示是否在同一台服务器上其他 web 应用程序重定向到 Url 时要记住身份验证的用户。 默认值为 false。                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      登录页的 URL。 默认值为 login.aspx 的情况。                                                                                                                                                                                                                      |
|            name            |                                                                                                                                                                                                   在使用基于 cookie 的身份验证票证的 cookie 的名称。 默认值为。ASPXAUTH。                                                                                                                                                                                                   |
|            path            |                                                                             当使用基于 cookie 的身份验证票证，此设置指定 cookie s 路径属性。 路径属性使开发人员来限制到特定的目录层次结构的 cookie 的范围。 默认值是/，通知将发送到对域进行的任何请求的身份验证票证 cookie 的浏览器。                                                                              |
|         保护         |                                                                                                                                            指示哪些技术用于保护窗体身份验证票证。 允许的值为： 所有 （默认）;加密;None;和验证。 在步骤 3 中的详细讨论了这些设置。                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                一个布尔值，该值指示是否需要 SSL 连接来传输身份验证 cookie。 默认值为 False。                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 一个布尔值，该值指示用户是否每次重置的身份验证 cookie s 超时值在单个会话期间访问该网站。 默认值为 true。 在指定的更详细地讨论身份验证票证超时策略票证的超时值部分。                                                                                                 |
|          超时           |                                                                                                                               指定时间，以分钟为单位，在其后的身份验证票证 cookie 过期。 默认值为 30。 在指定的更详细地讨论身份验证票证超时策略票证的超时值部分。                                                                                                                               |

**表 1**: 摘要&lt;窗体&gt;元素的特性

在 ASP.NET 2.0 及更高版本，默认窗体身份验证值是硬编码在.NET Framework 中的 FormsAuthenticationConfiguration 类中。 必须在 Web.config 文件中应用程序的应用程序的基础上应用任何修改。 这不同于 ASP.NET 1.x 中，其中默认窗体身份验证值在 machine.config 文件中存储 （并因此无法修改通过编辑 machine.config）。 While 主题有关的 ASP.NET 1.x 中，有必要提及窗体身份验证系统设置的数量在 ASP.NET 2.0 中具有不同的默认值及其他比在 ASP.NET 1.x。 如果要从 ASP.NET 1.x 环境迁移你的应用程序，它是必须要注意的这些差异。 请查阅[&lt;窗体&gt;元素技术文档](https://msdn.microsoft.com/library/1d3t3c61.aspx)有关差异的列表。

> [!NOTE]
> 多个窗体身份验证设置，如超时、 域和路径，指定生成的窗体身份验证票证 cookie 的详细信息。 对 cookie、 工作原理和它们的各种属性的详细信息，请阅读[此 Cookie 教程](http://www.quirksmode.org/js/cookies.html)。


### <a name="specifying-the-tickets-timeout-value"></a>指定的票证超时值

窗体身份验证票证是表示标识的令牌。 使用基于 cookie 的身份验证票证，此令牌中以 cookie 的形式保存并发送到 web 服务器上每个请求。 拥有的令牌，从本质上讲，声明，我*用户名*，我已登录，并使用，以便可以跨页面访问记住用户的标识。

窗体身份验证票证不仅包括用户的标识，而且还包含可帮助确保完整性和安全令牌的信息。 毕竟，我们不希望恶意用户能够创建盗版的令牌，或以某种 underhanded 方式修改合法的令牌。

包含在票证中的一个此类位是*到期*，即的日期和时间票证将不再有效。 FormsAuthenticationModule 将检查身份验证票证，每次它确保不具有尚未传递票证的到期。 如果是，它不考虑该票证，并标识为匿名用户。 这种保护措施，帮助防止重播攻击。 而无需到期时间，如果黑客已能够通过物理访问其计算机并通过其 cookie 根可能是获取用户的有效的身份验证票证-她动手-他们可以将请求发送到具有此被盗的身份验证票证的服务器和获取条目。 虽然到期时间不会阻止这种情况下，它却限制此类攻击可能会成功在此期间的窗口。

> [!NOTE]
> 步骤 3 个窗体身份验证系统用来保护身份验证票证的详细信息更多技术。


在创建时的身份验证票证，窗体身份验证系统通过咨询超时设置来确定其到期。 表 1 中，将默认值设置为 30 分钟的超时值中所述这意味着，在创建窗体身份验证票证时其到期设置为日期和时间在将来 30 分钟。

到期时间定义一个绝对时间在将来的窗体身份验证票证过期时。 但开发人员通常要实现可调到期，一个每次用户将回顾站点重置。 此行为由 slidingExpiration 设置确定。 如果设置为 true （默认值），每次 FormsAuthenticationModule 将用户进行身份验证的时，它将更新票证的到期。 如果设置为 false，过期日期未更新对每个请求，从而导致票证过期完全超时分钟数票证最初创建。

> [!NOTE]
> 存储在身份验证票证的到期时间是绝对日期和时间值，如 2008 年 8 月 2 日上午 11:34。 此外，日期和时间都是相对于 web 服务器的本地时间。 这种设计决策可能会有一些有趣的副作用围绕夏时制 (DST)，这是在美国的时钟移动提前一小时 （假设 web 服务器所在的位置夏时制观察到的区域设置中） 时。 请考虑会发生什么情况为 ASP.NET 网站使用 DST 开始时间 30 分钟后到期 （这是凌晨 2:00）。 假设访问者登录到站点在 2008 年 3 月 11 日凌晨 1:55。 这会生成将在到期日期为 2008 年 3 月 11 日凌晨 2:25 （将来 30 分钟） 的窗体身份验证票证。 但是，一旦围绕回滚凌晨 2:00，时钟跳转到凌晨 3:00 由于 DST。 当用户加载新页面 （在上午 3:01） 在登录后的六分钟时，FormsAuthenticationModule 将说明在票证已过期，将用户重定向到登录页。 这和其他身份验证票证超时问题，以及解决方法有关的更全面讨论，选取一份 Stefan Schackow *Professional ASP.NET 2.0 安全、 成员资格和角色管理*(ISBN:978-0-7645-9698-8)。


图 1 说明了在工作流时 slidingExpiration 设置为 false，超时设置为 30。 请注意，在登录时生成的身份验证票证包含到期日期，并在后续请求中未更新此值。 如果 FormsAuthenticationModule 找到此票证已到期，它将其丢弃，并将请求视为匿名。


[![以图形形式的窗体身份验证票证到期时 slidingExpiration 为 false](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**图 01**: 的窗体身份验证票证到期时 slidingExpiration 的图形表示形式为 false ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png))


图 2 显示了工作流时 slidingExpiration 设置为 true，并且超时设置为 30。 时 （使用非过期票证） 收到的已经过身份验证的请求其到期将更新为在将来分钟的超时数。


[![以图形形式的窗体身份验证票证 slidingExpiration 条件为 true 时](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**图 02**： 窗体身份验证票证的图形表示形式 slidingExpiration 条件为 true 时 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png))


在使用基于 cookie 的身份验证票证 （默认值），这一讨论将变得有点令人困惑，因为 cookie 还可以指定自己满。 Cookie 的到期 （或缺少局域） 会指示浏览器 cookie 应销毁时。 如果 cookie 缺少到期时间，销毁浏览器关闭时。 如果过期时间存在，但是，cookie 的日期之前会一直存储在用户计算机上，指定在到期时间已通过。 Cookie 时销毁由浏览器，它不能再发送到 web 服务器。 因此，进行销毁是 cookie 的类似于用户注销站点。

> [!NOTE]
> 当然，用户可以主动删除存储在其计算机上的任何 cookie。 在 Internet Explorer 7 中，将转到工具，选项，并单击浏览历史记录部分中的删除按钮。 在这里，单击删除 cookie 按钮。


窗体身份验证系统将创建基于会话的或基于过期的 cookie，具体取决于传递给的值*persistCookie*参数。 回想一下，FormsAuthentication 类 GetAuthCookie、 SetAuthCookie 和 RedirectFromLoginPage 方法采用两个输入参数：*用户名*并*persistCookie*。 我们在前面的教程中创建的登录页包含一个记住我的复选框，来确定是否已创建持久 cookie。 永久 cookie 是基于到期的;非持久性 cookie 是基于会话的。

已讨论过的超时和 slidingExpiration 概念不适用于相同这两种基于会话和过期的 cookie。 没有在执行过程中只有一个细微的差别： 当使用基于过期的 cookie slidingTimeout 设置为 true 时，cookie 的到期只会更新当超过一半的指定时间已过。

让我们更新我们网站的身份验证票证超时策略，使票证超时 （60 分钟），一小时后的使用可调到期。 若要此更改生效，更新 Web.config 文件中，添加&lt;窗体&gt;元素&lt;身份验证&gt;元素使用以下标记：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>使用 login.aspx 的情况以外的登录页 URL

因为 FormsAuthenticationModule 自动重定向到登录页的未经授权的用户，必须知道登录页面的 URL。 中的 loginUrl 属性指定此 URL&lt;窗体&gt;元素，默认值为 login.aspx 的情况。 如果要将迁移对现有网站，你可能已使用不同的 URL，其中一个已设置为书签并被搜索引擎索引登录页。 而不是正在对现有的登录页重命名为 login.aspx 的情况和重大链接和用户的书签，而是可以修改 loginUrl 属性以指向您的登录页。

例如，如果您的登录页名为 SignIn.aspx 并且位于用户目录中，您可以指向 ~/Users/SignIn.aspx loginUrl 配置设置如下所示：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

由于我们的当前应用程序已具有一个名为 login.aspx 的情况的登录页，则无需指定自定义值中的&lt;窗体&gt;元素。

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>步骤 2： 使用无 Cookie Forms 身份验证票证

默认情况下窗体身份验证系统确定是否将其身份验证票证存储在 cookie 集合或将它们嵌入中基于用户代理访问网站的 URL。 所有主流桌面浏览器等 Internet Explorer、 Firefox、 Opera 和 Safari 支持 cookie，但并非所有移动设备执行操作。

使用窗体身份验证系统的 cookie 策略取决于中的无 cookie 设置&lt;窗体&gt;元素，它可以分配四个值之一：

- UseCookies-指定将始终使用基于 cookie 的身份验证票证。
- UseUri-指示将永远不使用基于 cookie 的身份验证票证。
- 不使用自动检测功能-如果设备配置文件不支持 cookie，基于 cookie 的身份验证票证;如果设备配置文件支持 cookie，探测机制用于确定是否已启用 cookie。
- UseDeviceProfile-默认设置;仅当设备配置文件支持 cookie，请使用基于 cookie 的身份验证票证。 不使用任何探测机制。

自动检测和 UseDeviceProfile 设置依赖*设备配置文件*中认定是否使用基于 cookie 的或无 cookie 身份验证票证。 ASP.NET 维护的各种设备和其功能，例如是否支持 cookie，它们支持的 JavaScript 和等等的哪些版本的数据库。 每次设备请求 web 页从 web 服务器发送沿*用户代理*标识设备类型的 HTTP 标头。 ASP.NET 会自动与指定在其数据库中的相应配置文件匹配提供的用户代理字符串。

> [!NOTE]
> 设备功能的此数据库存储在多个 XML 文件符合[浏览器定义文件架构](https://msdn.microsoft.com/library/ms228122.aspx)。 默认设备配置文件位于 %windir%\microsoft.net\framework\v2.0.50727\config\browsers。 此外可以将自定义文件添加到应用程序的应用\_浏览器文件夹。 有关详细信息，请参阅[如何： 检测浏览器类型在 ASP.NET Web Pages](https://msdn.microsoft.com/library/3yekbd5b.aspx)。


因为默认设置为 UseDeviceProfile，将通过其配置文件报告它不支持 cookie 的设备访问该站点时使用无 cookie forms 身份验证票证。

### <a name="encoding-the-authentication-ticket-in-the-url"></a>编码的 URL 中的身份验证票证

Cookie 是一个自然媒体是默认窗体身份验证设置使用 cookie，如果正在访问的设备支持它们的原因将特定网站的每个请求中包含从浏览器的信息。 如果不支持 cookie，必须使用用于将从客户端身份验证票证传递到服务器的替代方法。 用于无 cookie 的环境中常见的解决方法是在 URL 中的 cookie 数据进行编码。

请参阅如何在 URL 中嵌入此类信息的最佳方式是强制站点以使用无 cookie 身份验证票证。 这可以通过将无 cookie 的配置设置设置为 UseUri 来实现：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

您一次进行此更改，请访问通过浏览器站点。 如果以匿名用户访问，Url 会查找完全像以前一样。 例如，访问 Default.aspx 页时我的浏览器地址栏显示了以下 URL:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

但是，在记录，窗体身份验证票证被嵌入到 URL。 例如，访问登录页和 Sam 的身份登录之后, 我就会返回到 Default.aspx 页但 URL 这一次是：

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

窗体身份验证票证已嵌入到 URL 中。 字符串 (F (jaIOIDTJxIr12xYS VVgkqKCVAuIoW30Bu0diWi6flQC FyMaLXJfow\_Vd9GZkB2Cv rfezq0gKadKX0YPZCkA2) 表示十六进制编码的身份验证票证信息，并且是相同的数据通常存储在一个 cookie。

为了使无 cookie 身份验证票证，若要运行，系统必须对所有 Url 的页上，以包含身份验证票证数据进行都编码，否则身份验证票证时将会丢失用户单击的链接。 幸运的是，自动执行此嵌入的逻辑。 若要演示此功能，打开 Default.aspx 页，并添加超链接控件，分别将其文本和 NavigateUrl 属性设置为测试链接和 SomePage.aspx。 它并不重要，真的没有一个页面中名为 SomePage.aspx 我们的项目。

将所做的更改保存到 Default.aspx，然后通过浏览器访问它。 在登录到站点，以便在 URL 中嵌入窗体身份验证票证。 接下来，从 Default.aspx，单击测试链接链接。 这是怎么回事？ 如果不存在名为 SomePage.aspx 任何页，则表示出现 404 错误，但这是不值得在此处。 相反，重点介绍在您的浏览器的地址栏。 请注意，它包含窗体身份验证票证在 URL 中 ！

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

链接中 URL SomePage.aspx 已自动转换为一个 URL，包括身份验证票证-我们不需要编写一点代码 ！ 窗体身份验证票证将自动嵌入在 URL 中的任何不是以 http:// 开头的超链接或 /。 如果在调用 Response.Redirect、 超链接控件，或定位 HTML 元素中出现的超链接并不重要 (即&lt;href ="..."&gt;...&lt;/a&gt;)。 只要 URL 不是类似于http://www.someserver.com/SomePage.aspx或 /SomePage.aspx，身份验证票证将嵌入为我们的窗体。

> [!NOTE]
> 无 cookie forms 身份验证票证遵循相同的超时策略作为基于 cookie 的身份验证票证。 但是，无 cookie 身份验证票证的更容易出现重播攻击，因为在 URL 中直接嵌入身份验证票证。 假设访问网站并记录在中，然后再将 URL 粘贴到同事的电子邮件中的用户。 如果该同事达到过期日期之前单击该链接，它们将作为其发送电子邮件的用户记录 ！


## <a name="step-3-securing-the-authentication-ticket"></a>步骤 3： 保护身份验证票证

通过网络传输的窗体身份验证票证 cookie 中或直接在 URL 中嵌入。 标识信息的补充身份验证票证还可以包含用户数据，（正如我们将在步骤 4 中看到的）。 因此，很重要的已加密的票证数据防止被 （更重要的是） 的窗体身份验证系统可以保证票证被未篡改。

若要确保票证的数据的隐私，窗体身份验证系统可以加密票证数据。 无法加密票证数据通过网络传输纯文本发送可能敏感的信息。

若要确保票证的真实性，窗体身份验证系统必须*验证*票证。 验证是确保数据的特定部分未进行修改，并通过完成的 act *[消息身份验证代码 (MAC)](http://en.wikipedia.org/wiki/Message_authentication_code)*。 简单地说，MAC 是信息的标识需要验证 （在此情况下，该票证） 的数据的一小部分。 如果修改了 MAC 所表示的数据，然后在 MAC 和数据将不匹配。 此外，它是计算硬黑客同时修改数据并生成自己的 MAC 以与已修改的数据一致。

创建 （或修改） 时的票证，窗体身份验证系统创建 MAC，并将其附加到的票证数据。 当后续请求到达时，窗体身份验证系统进行比较来验证票证数据的真实性的 MAC 和票证数据。 图 3 以图形方式显示此工作流。


[![票证的真实性确保通过 MAC](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**图 03**： 通过 MAC 确保票证的真实性 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png))


什么是安全度量值应用于身份验证票证中的保护设置取决于&lt;窗体&gt;元素。 保护设置可能会分配给以下三个值之一：

- 所有的票证已加密，并进行数字签名 （默认值）。
- 加密-仅加密已应用-无 MAC 生成。
- 无-票证是加密和数字签名。
- 生成验证-MAC，但通过网络传输纯文本发送票证数据。

Microsoft 强烈建议使用的所有设置。

### <a name="setting-the-validation-and-decryption-keys"></a>设置验证和解密密钥

加密和哈希算法由窗体身份验证系统中用于加密和验证身份验证票证是通过可自定义[ &lt;machineKey&gt;元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)在 Web.config 中。表 2 轮廓&lt;machineKey&gt;元素的特性和其可能的值。

| **特性** | **说明** |
| --- | --- |
| 解密 | 指示用于加密的算法。 此属性可以具有以下四个值之一:-自动-默认设置;确定基于 decryptionKey 属性的长度的算法。 使用 AES-[高级加密标准 (AES)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)算法。 DES-使用[数据加密标准 (DES)](http://en.wikipedia.org/wiki/Data_Encryption_Standard)此算法被视为计算弱，因此不应。 -3DES-使用[三重 DES](http://en.wikipedia.org/wiki/Triple_DES)算法工作方式是应用三次的 DES 算法。 |
| decryptionKey | 使用的加密算法密钥。 此值必须是适当的长度 （基于中解密值）、 自动生成或附加，其中任何一个值的十六进制字符串 IsolateApps。 添加 IsolateApps 指示 ASP.NET 为每个应用程序使用的唯一值。 默认值为 AutoGenerate，IsolateApps。 |
| 验证 | 指示用于验证的算法。 此属性可以具有以下四个值之一:-AES-使用高级加密标准 (AES) 算法。 -MD5-使用[消息摘要 5 (MD5)](http://en.wikipedia.org/wiki/MD5)算法。 -SHA1-使用[SHA1](http://en.wikipedia.org/wiki/Sha1)算法 （默认值）。 -3DES-使用三重 DES 算法。 |
| validationKey | 由验证算法密钥。 此值必须是适当的长度 （基于在验证中的值）、 自动生成或附加，其中任何一个值的十六进制字符串 IsolateApps。 添加 IsolateApps 指示 ASP.NET 为每个应用程序使用的唯一值。 默认值为 AutoGenerate，IsolateApps。 |

**表 2**: &lt;machineKey&gt;元素特性

这些加密和验证的选项，和专业人员的全面讨论和缺点的各种算法，不在本教程的范围。 为深入了解一下这些问题，包括要使用，哪些加密和验证算法的指南哪些密钥长度，若要使用，以及如何才能生成这些密钥，请参阅*Professional ASP.NET 2.0 安全、 成员资格和角色管理*.

默认情况下，对于每个应用程序，自动生成用于加密和验证的密钥，这些键存储在本地安全机构 (LSA)。 简单地说，默认设置保证 web 服务器的 web 服务器和应用程序的应用程序的基础上的唯一键。 因此，此默认行为将不能用于以下两种情况：

- **Web 场**-在[web 场](http://en.wikipedia.org/wiki/Web_farm)方案中，单个 web 应用程序托管在可伸缩性和冗余性的目的的多个 web 服务器上。 每个传入请求调度到的服务器场，这意味着，在用户的会话的生存期，不同的服务器可用于处理其各种请求中。 因此，每个服务器必须使用相同的加密和验证密钥，以便创建窗体身份验证票证、 加密和验证在上一台服务器可以解密，并在该场中的不同服务器上进行验证。
- **跨应用程序票证共享**-单个 web 服务器可以托管多个 ASP.NET 应用程序。 如果你需要有关这些不同应用程序共享单个窗体身份验证票证，它是命令性，他们加密和验证的密钥匹配。

在处理在 web 场中设置或在同一台服务器上的应用程序之间共享身份验证票证时，你将需要配置&lt;machineKey&gt;在受影响的应用程序中的元素，以便其 decryptionKey 和validationKey 值匹配。

尽管上述方案都不适用于我们的示例应用程序，我们仍可以指定显式 decryptionKey 和 validationKey 值并定义要使用的算法。 添加&lt;machineKey&gt;将设置为 Web.config 文件：

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

有关详细信息，请查看[如何： 在 ASP.NET 2.0 配置 MachineKey](https://msdn.microsoft.com/library/ms998288.aspx)。

> [!NOTE]
> DecryptionKey 和 validationKey 值截取自[Steve Gibson](http://www.grc.com/stevegibson.htm)的[完美密码网页](https://www.grc.com/passwords.htm)，其中每个页，请访问上生成 64 随机的十六进制字符。 若要降低对生产应用程序正在影响这些密钥的可能性，建议您的更高版本的密钥替换为从完美密码页随机生成的。


## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>步骤 4： 存储在票证中的其他用户数据

许多 web 应用程序显示有关的信息，或使基于当前登录用户的页面的显示。 例如，web 页可能会显示用户的名称和她上次登录的每个页面右上角的日期。 窗体身份验证票证存储当前登录的用户的用户名，但页面需要的任何其他信息时，必须转到要查找不会存储在身份验证票证的信息的用户存储区-通常数据库。

很少的代码与我们可以存储在窗体身份验证票证的其他用户信息。 可以通过表示此类数据[FormsAuthenticationTicket 类](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)的[UserData 属性](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)。 这是信息的一个有用地方安置的少量通常所需的用户有关。 UserData 属性包含在身份验证票证 cookie，并像其他票证字段、 是加密和验证中指定的值基于窗体身份验证系统的配置。 默认情况下，UserData 为空字符串。

为了在身份验证票证中存储用户数据，我们需要在登录页上获取特定于用户的信息并将其存储在票证中编写一些代码。 由于用户数据是字符串类型的属性，在其中存储的数据必须正确地序列化为字符串。 例如，假设，我们的用户存储包含每个用户的出生日期和雇主，名称中，我们想要将这些两个属性值存储在身份验证票证。 我们可能这些值序列化到字符串通过串联雇主名称后跟出生的字符串的竖线 (|) 的用户的日期。 用户在 1974 年 8 月 15，云中生成适用于 Northwind Traders，我们将 UserData 属性将字符串分配： 1974年-08-15 |Northwind Traders。

我们需要访问存储在票证中的数据，只要我们能做到获取当前请求的 FormsAuthenticationTicket 和反序列化的 UserData 属性。 出生和雇主名称示例的日期，在我们会将 UserData 字符串拆分为两个基于分隔符 (|) 的子字符串。


[![其他用户信息可以存储在身份验证票证](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**图 04**： 其他用户的信息可以存储在身份验证票证 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png))


### <a name="writing-information-to-userdata"></a>UserData 将信息写入

遗憾的是，将特定于用户的信息添加到窗体身份验证票证不像这样简单如您所料。 FormsAuthenticationTicket 类的 UserData 属性是只读的并且只能通过 FormsAuthenticationTicket 类构造函数指定。 指定时 UserData 属性构造函数中，我们还需要提供票证的其他值： 用户名、 发布日期、 过期和等等。 我们在前面的教程中创建的登录页，这是所有由为我们 FormsAuthentication 类。 向添加时 UserData FormsAuthenticationTicket，我们将需要编写代码来复制很多 FormsAuthentication 类已提供的功能。

我们来探讨使用 UserData 通过更新 Login.aspx 页面，以记录有关用户身份验证票证的其他信息所需的代码。 假设我们的用户存储包含有关适用于用户的公司和其标题的信息，我们想要的身份验证票证中获取此信息。 更新 Login.aspx 页面 LoginButton Click 事件处理程序，使代码看起来如下所示：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

让我们逐步完成此一行代码一次。 该方法开始时通过定义四个字符串数组： 用户、 密码、 companyName 和 titleAtCompany。 这些列阵储存用户名、 密码、 公司名称和标题的用户帐户在系统中的其中有三个： Scott、 Jisun 和 Sam。 在实际的应用程序，将从用户存储区，并非硬编码的页面的源代码中查询这些值。

在上一教程中，如果提供的凭据不有效我们只需调用 FormsAuthentication.RedirectFromLoginPage （UserName.Text，RememberMe.Checked），执行以下步骤：

1. 创建窗体身份验证票证
2. 票证写入在适当的存储。 对于基于 cookie 的身份验证票证，所使用的浏览器的 cookie 集合;为无 cookie 身份验证票证的票证数据序列化到 URL
3. 被该用户重定向到相应的页

在上面的代码中复制这些步骤。 首先，我们最终将 UserData 属性中存储的字符串是通过合并的公司名称和标题，并分隔两个值的竖线字符 (|) 形成的。

Dim userDataString As String = String.Concat(companyName(i), "|", titleAtCompany(i))

接下来，调用方法时，这会创建身份验证票证，FormsAuthentication.GetAuthCookie 加密和验证根据配置设置，并将其置于 HttpCookie 对象。

Dim authCookie 作为 HttpCookie = FormsAuthentication.GetAuthCookie （UserName.Text，RememberMe.Checked）

若要使用的 cookie 中嵌入 FormAuthenticationTicket，我们需要调用 FormAuthentication 类[解密方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)、 传入的 cookie 值。

Dim ticket As FormsAuthenticationTicket = FormsAuthentication.Decrypt(authCookie.Value)

然后，创建*新*FormsAuthenticationTicket 实例根据现有 FormsAuthenticationTicket 值。 但是，此新票证包含特定于用户的信息 (userDataString)。

Dim newTicket 作为 FormsAuthenticationTicket = 新 FormsAuthenticationTicket(ticket.版本中，票证。名称，票证。IssueDate、 票证。过期时间，票证。IsPersistent，userDataString)

我们然后加密 （和验证） 新 FormsAuthenticationTicket 实例通过调用[加密方法](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)，并将其置于 authCookie 回此加密 （和验证） 的数据。

authCookie.Value = FormsAuthentication.Encrypt(newTicket)

最后，authCookie 添加到 Response.Cookies 集合并调用 GetRedirectUrl 方法来确定向用户发送的相应页。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

需要所有这些代码，因为 UserData 属性是只读的它 FormsAuthentication 类不提供其 GetAuthCookie、 SetAuthCookie 或 RedirectFromLoginPage 方法中指定用户数据信息的任何方法。

> [!NOTE]
> 我们刚检查的代码将特定于用户的信息存储在基于 cookie 的身份验证票证。 负责序列化到的 URL 的窗体身份验证票证的类是.NET Framework 的内部。 长话短说，不能在无 cookie forms 身份验证票证中存储用户数据。


### <a name="accessing-the-userdata-information"></a>访问用户数据信息

现在每个用户的公司名称和标题存储在窗体身份验证票证的 UserData 属性在登录时。 可以从任何页面上的身份验证票证访问此信息，而无需用户存储到的行程。 为了说明如何从 UserData 属性检索此信息，让我们更新 Default.aspx，以便其欢迎消息包括不仅用户的名称，但还它们适用于公司和职位。

目前，Default.aspx 将 AuthenticatedMessagePanel 面板包含一个名为 WelcomeBackMessage 的标签控件。 向经过身份验证的用户仅显示此面板。 更新 Default.aspx 的页中的代码\_加载事件处理程序，使其如下所示：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

如果 Request.IsAuthenticated 为 True，则首先将 WelcomeBackMessage 的文本属性设置为欢迎使用后，*用户名*。 然后，User.Identity 属性是强制转换为 FormsIdentity 对象，以便我们可以访问基础 FormsAuthenticationTicket。 FormsAuthenticationTicket 后，我们反 UserData 属性序列化为的公司名称和标题。 通过将拆分管道字符中的字符串来完成此操作。 WelcomeBackMessage 标签中然后会显示公司名称和标题。

图 5 显示了操作中的此显示的屏幕截图。 日志记录为 Scott 显示包含 Scott 的公司和标题的欢迎使用后的消息。


[![会显示当前登录的用户的公司和标题](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**图 05**： 显示当前登录的用户的公司和标题 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png))


> [!NOTE]
> 身份验证票证的 UserData 属性将充当用户存储的缓存。 与任何缓存一样，它需要时修改基础数据进行更新。 例如，如果用户可以从中更新其配置文件的网页，必须刷新缓存 UserData 属性中的字段以反映用户所做的更改。


## <a name="step-5-using-a-custom-principal"></a>步骤 5： 使用自定义主体

在每个传入请求 FormsAuthenticationModule 尝试对用户进行身份验证。 如果存在未过期的身份验证票证，则 FormsAuthenticationModule 将 HttpContext.User 属性分配给一个新的 GenericPrincipal 对象。 此 GenericPrincipal 对象具有类型 FormsIdentity，其中包括对窗体身份验证票证的引用的标识。 GenericPrincipal 类包含实现 IPrincipal 的类所需的裸机最小功能-它只是具有 Identity 属性和 IsInRole 方法。

主体对象具有两项职责： 若要指示为该用户所属的角色并提供标识信息。 这通过 IPrincipal 接口 IsInRole (*roleName*) 方法和标识属性，分别。 GenericPrincipal 类允许角色名称的字符串数组指定通过其构造函数;其 IsInRole (*roleName*) 方法只是检查以查看是否已传递的中*roleName*存在于字符串数组。 当 FormsAuthenticationModule 创建 GenericPrincipal 时，会传递一个空字符串数组中给 GenericPrincipal 的构造函数。 因此，对 IsInRole 的任何调用将始终返回 False。

GenericPrincipal 类能满足大多数窗体基于的身份验证方案不使用角色的需求。 对于这些情况下，默认角色处理时不足或者当需要将自定义的 IIdentity 对象与用户相关联，可以在身份验证工作流过程中创建自定义 IPrincipal 对象并将其分配给 HttpContext.User 属性。

> [!NOTE]
> 我们会在将来的教程中，当 ASP。启用 NET 的角色框架创建类型的自定义主体对象[RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)并覆盖窗体身份验证创建 GenericPrincipal 对象。 若要自定义角色框架的 API 与主体的 IsInRole 方法执行此操作。


由于我们具有不关心自己角色尚未，我们必须用于此时，必须查明创建自定义主体的唯一原因是将自定义的 IIdentity 对象向主体相关联。 在步骤 4 中还介绍了用户的公司名称和其标题中特定身份验证票证的 UserData 属性中存储其他用户信息。 但是，UserData 信息只是将可通过身份验证票证访问，然后仅为序列化字符串，这意味着，只要我们想要查看用户信息存储在票证中我们需要分析 UserData 属性。

我们可以通过创建实现 IIdentity 和包括 CompanyName 和 Title 属性的类来提高开发人员体验。 这样一来，开发人员可以访问当前登录的用户的公司名称和标题直接通过公司名称和标题属性，而不需要了解如何分析 UserData 属性。

### <a name="creating-the-custom-identity-and-principal-classes"></a>创建自定义标识和主体类

对于本教程，让我们将创建在应用程序中的自定义主体和标识对象\_代码文件夹。 首先，通过添加应用\_代码到你的项目的文件夹-右键单击解决方案资源管理器中的项目名称，选择添加 ASP.NET 文件夹选项，并选择应用\_代码。 应用\_代码文件夹是一个特殊的 ASP.NET 文件夹包含类文件特定于该网站。

> [!NOTE]
> 应用\_管理通过网站项目模型项目时，应仅使用代码文件夹。 如果使用的[Web 应用程序项目模型](https://msdn.microsoft.com/asp.net/Aa336618.aspx)、 创建标准文件夹并将类添加到的。 例如，无法添加名为类的新文件夹，并那里将你的代码。


接下来，将两个新类文件添加到应用\_代码文件夹，一个命名的 CustomIdentity.vb，另一个名为 CustomPrincipal.vb。


[![将 CustomIdentity 和 CustomPrincipal 类添加到你的项目](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**图 06**： 将 CustomIdentity 和 CustomPrincipal 类添加到你的项目 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png))


CustomIdentity 类负责实现 IIdentity 接口，定义 AuthenticationType、 IsAuthenticated 和名称属性。 除了这些必需的属性，我们感兴趣公开基础窗体身份验证票证，以及用户的公司名称和标题的属性。 下面的代码进入 CustomIdentity 类。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

请注意，此类包含一个 FormsAuthenticationTicket 成员变量 (\_票证) 和通过构造函数时必须提供此票证的信息。 在返回的标识名称，则使用此票证数据其 UserData 属性进行分析，以返回公司名称和标题属性的值。

接下来，创建 CustomPrincipal 类。 因为我们不关心角色此时，必须查明，CustomPrincipal 类的构造函数接受仅 CustomIdentity 对象;它的 IsInRole 方法始终返回 False。

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>CustomPrincipal 对象分配给传入请求的安全上下文

现在，我们扩展了默认 IIdentity 规范，包括公司名称和标题属性的类，以及使用自定义标识的自定义主体类。 我们可以单步执行 ASP.NET 管道，并将我们的自定义主体对象分配给传入请求的安全上下文。

在 ASP.NET 管道接收传入请求并处理它通过一系列步骤。 每个步骤中，在引发特定事件以使开发人员可以利用 ASP.NET 管道并修改其生命周期中的特定点处的请求。 FormsAuthenticationModule，例如，等待 ASP.NET 引发[AuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)，此时它会检查身份验证票证的传入请求。 如果找到一个身份验证票证，则是创建一个 GenericPrincipal 对象并将其分配给 HttpContext.User 属性。

AuthenticateRequest 事件之后，ASP.NET 管道引发[PostAuthenticateRequest 事件](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)，这是我们可以替换为创建的实例与 FormsAuthenticationModule 的 GenericPrincipal 对象我们CustomPrincipal 对象。 图 7 显示了此工作流。


[![GenericPrincipal CustomPrincipal PostAuthenticationRequest 事件中被替换为](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**图 07**: GenericPrincipal CustomPrincipal PostAuthenticationRequest 事件中被替换为 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png))


若要执行的代码以响应 ASP.NET 管道事件，我们可以在 Global.asax 中创建相应的事件处理程序，或创建我们自己的 HTTP 模块。 对于本教程让我们在 Global.asax 中创建的事件处理程序。 首先将 Global.asax 添加到你的网站。 右键单击解决方案资源管理器中的项目名称并添加名为 Global.asax 的全局应用程序类类型的项。


[![Global.asax 文件添加到你的网站](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**图 08**： 将 Global.asax 文件添加到您的网站 ([单击以查看实际尺寸的图像](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png))


默认 Global.asax 模板包括多个 ASP.NET 管道事件，包括开始时，最终的事件处理程序和[错误事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，等等。 可以删除这些事件处理程序，因为我们不需要这些服务为此应用程序。 我们感兴趣的事件是 PostAuthenticateRequest。 更新在 Global.asax 文件，使其标记看起来类似于以下：

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

应用程序\_OnPostAuthenticateRequest 方法执行每次 ASP.NET 运行时将引发 PostAuthenticateRequest 事件，这种情况发生在每个传入的页请求上一次。 事件处理程序首先会检查以查看用户进行身份验证，并且通过窗体身份验证进行身份验证。 如果是这样，新的 CustomIdentity 对象创建，并在其构造函数中传递当前请求的身份验证票证。 接下来，CustomPrincipal 对象是创建并在其构造函数中传递的刚创建 CustomIdentity 对象。 最后，将当前请求的安全上下文被分配给新创建的 CustomPrincipal 对象。

请注意-将 CustomPrincipal 对象与请求的安全上下文关联的最后一步将主体分配到两个属性： HttpContext.User 和 Thread.CurrentPrincipal。 由于在 ASP.NET 中处理的安全上下文的方式，这些两个分配是必需的。 .NET Framework 将与每个正在运行的线程; 相关联的安全上下文此信息是可通过 IPrincipal 对象用作[线程对象](https://msdn.microsoft.com/library/system.threading.thread.aspx)的[CurrentPrincipal 属性](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)。 让人困惑的是 ASP.NET 有其自己的安全上下文信息 (HttpContext.User)。

在某些情况下，确定的安全上下文; 时检查 Thread.CurrentPrincipal 属性在其他情况下，使用 HttpContext.User。 例如，有在.NET 中的安全功能，可让开发人员以声明方式状态的哪些用户或角色可以实例化类或调用特定方法 (请参阅[添加到业务和数据层使用的授权规则PrincipalPermissionAttributes](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx))。 实际上，这些声明性方法确定通过 Thread.CurrentPrincipal 属性的安全上下文。

在其他情况下，使用 HttpContext.User 属性。 例如上, 一教程中我们使用此属性以显示当前登录的用户的用户名。 很明显，然后，它是命令性，匹配的 Thread.CurrentPrincipal 和 HttpContext.User 属性中的安全上下文信息。

ASP.NET 运行时自动同步为我们的这些属性值。 但是，AuthenticateRequest 事件之后，会发生这种同步，但*之前*PostAuthenticateRequest 事件。 因此，我们 PostAuthenticateRequest 事件中添加自定义主体时需要进行某些手动分配 Thread.CurrentPrincipal，否则 Thread.CurrentPrincipal，HttpContext.User 将不同步。请参阅[Context.User vs。Thread.CurrentPrincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/)有关此问题的更多详细讨论。

### <a name="accessing-the-companyname-and-title-properties"></a>访问公司名称和标题属性

每当请求到达并分派给 ASP.NET 引擎，该应用程序\_OnPostAuthenticateRequest Global.asax 中的事件处理程序将激发。 如果请求已成功经过 formsauthenticationmodule，事件处理程序将使用基于窗体身份验证票证的 CustomIdentity 对象创建一个新的 CustomPrincipal 对象。 在位置对此逻辑，使用访问有关当前已登录的用户的公司名称和标题信息是非常简单。

返回到页\_在 Default.aspx 中，其中在步骤 4 中，我们编写了代码，以检索窗体身份验证票证和分析 UserData 属性以显示用户的公司名称和标题的 Load 事件处理程序。 与使用现在的 CustomPrincipal 和 CustomIdentity 对象，就不必分析出票证的 UserData 属性的值。 相反，只需获取对 CustomIdentity 对象的引用，并使用其公司名称和标题属性：

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>总结

在本教程中介绍了如何自定义通过 Web.config 的窗体身份验证系统的设置。我们了解了如何处理的身份验证票证到期日期以及如何使用加密和验证安全措施来防止检查和修改的票证。 最后，我们讨论了使用身份验证票证的 UserData 属性存储在票证本身中的其他用户信息以及如何使用自定义主体和标识对象来以更加便于开发人员的方式公开此信息。

本教程最后，我们对 ASP.NET 中的窗体身份验证执行的检查。 下一教程将启动到成员资格框架之旅。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [仔细分析窗体身份验证](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [ASP.NET 2.0 中所述： 窗体身份验证](https://msdn.microsoft.com/library/aa480476.aspx)
- [如何： 保护 ASP.NET 2.0 中的窗体身份验证](https://msdn.microsoft.com/library/ms998310.aspx)
- [专业 ASP.NET 2.0 安全、 成员资格和角色管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)(ISBN: 978-0-7645-9698-8)
- [保护登录控件](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;身份验证&gt;元素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;窗体&gt;元素&lt;身份验证&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;MachineKey&gt;元素](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [了解窗体身份验证票证和 Cookie](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>在本教程中包含的主题的视频培训

- [如何更改窗体身份验证属性](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [如何在 ASP.NET 应用程序中的设置和使用无 Cookie 身份验证](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 窗体登录重定位](../../../videos/authentication/asp-forms-login-relocation.md)
- [窗体登录自定义密钥配置](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [向身份验证方法添加自定义数据](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [使用自定义主体对象](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>关于作者

自 1998 年以来，Scott Mitchell，多部 asp/ASP.NET 书籍的作者及 4GuysFromRolla.com 的已从事 Microsoft Web 技术工作。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是 *[Sams Teach 自己 ASP.NET 2.0 24 小时内](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在达到 Scott [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Alicja Maziarz。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)。

> [!div class="step-by-step"]
> [上一篇](an-overview-of-forms-authentication-vb.md)
