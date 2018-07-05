---
uid: web-pages/overview/releases/top-features-in-web-pages-2
title: ASP.NET Web Pages 2 中功能顶部 |Microsoft Docs
author: microsoft
description: 本主题提供了 ASP.NET Web Pages 2，附带 WebMatr 的轻型 web 编程框架中最新功能的概述...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: cc712e72-c3d0-4e43-bc2d-28cc09cd8f71
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/releases/top-features-in-web-pages-2
msc.type: authoredcontent
ms.openlocfilehash: 3cdb9d83e0f612ad7404bfaa9721b580916e112d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385261"
---
<a name="the-top-features-in-aspnet-web-pages-2"></a>ASP.NET Web Pages 2 中的常用功能
====================
by [Microsoft](https://github.com/microsoft)

> 本文提供的热门新功能在 ASP.NET Web Pages 2 RC 中，包含一个轻型 web 编程框架概述[Microsoft WebMatrix 2 RC](https://www.microsoft.com/web/)。
> 
> **包含的内容：** 
> 
> - [安装 WebMatrix](#install)
> - [新的和增强功能](#New_and_Enhanced_Features)
> 
>     - [RC 版的更改](#Changes_for_the_RC_Version)
>     - [Beta 版的更改](#Changes_for_the_Beta_Version)
>     - [使用新的和更新站点模板](#templates)
>     - [验证用户输入](#validation)
>     - [启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名](#oauthsetup)
>     - [添加映射使用映射帮助器](#maphelper)
>     - [运行 Web Pages 应用程序并排显示](#sidebyside)
>     - [移动设备的呈现页](#mobile)
> - [其他资源](#resources)
> 
> > [!NOTE]
> > 本主题假定使用 WebMatrix 的目的用于 ASP.NET Web Pages 2 代码。 但是，由于 Web Pages 1，您可以创建使用 Visual Studio 的 Web Pages 2 网站，后者可提供增强的 IntelliSense 功能和调试。 若要使用 Visual Studio 中的 Web 页，必须首先安装 Visual Studio 2010 SP1、 Visual Web Developer 速成版 2010 SP1 或 Visual Studio 11 Beta。 然后安装 ASP.NET MVC 4 Beta，其中包括用于 Visual Studio 中创建 ASP.NET MVC 4 和 Web Pages 2 应用程序模板和工具。
> 
> 
> *上次更新： 2012 年 6 月 18*


<a id="install"></a>
## <a name="installing-webmatrix"></a>安装 WebMatrix

若要安装 Web 页，可以使用 Microsoft Web 平台安装程序，它是免费的应用程序，它可以更轻松地安装和配置与 web 相关技术。 将安装 WebMatrix 2 试用版，包括 Web Pages 2 Beta。

1. 浏览到 Web 平台安装程序的最新版本的安装页面：

    [https://go.microsoft.com/fwlink/?LinkId=226883](https://go.microsoft.com/fwlink/?LinkId=226883)

    > [!NOTE]
    > 如果已安装 WebMatrix 1，此安装会更新它为 WebMatrix 2 beta 版本。 你可以运行在同一台计算机上使用 1 或 2 的版本创建的网站。 详细信息，请参阅部分上[运行网页的应用程序并排](#sidebyside)。
2. 选择**立即安装**。 

    如果你使用 Internet Explorer，请转到下一步。 如果使用 Mozilla Firefox 或 Google Chrome 等不同的浏览器，系统会提示保存*Webmatrix.exe*到您的计算机的文件。 保存该文件，然后单击它以启动安装程序。
3. 运行安装程序，然后选择**安装**按钮。 这会安装 WebMatrix 和 Web Pages。

## <a id="New_and_Enhanced_Features"></a>  新的和增强功能

### <a id="Changes_for_the_RC_Version"></a>  预发布版本 (2012 年 6 月) 的更改

2012 年 6 月中的 RC 版本发行已从已于 2012 年 3 月发布 Beta 版本刷新了一些更改。 这些更改是：

- 一个`Validation.AddFormError`方法已添加到`Validation`帮助器。 如果手动执行验证将非常有用 （例如，验证查询字符串中传递一个值） 和你想要添加可显示的错误消息`Html.ValidationSummary`方法。 有关详细信息，请参阅明[验证数据，不会直接从用户](https://go.microsoft.com/fwlink/?LinkId=253002#Validating_Data_That_Doesnt_Come_Directly_from_Users)中[ASP.NET Web Pages (Razor) 站点中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)。
- 已从核心 ASP.NET Web Pages 2 程序集删除了捆绑和缩小功能。 因此，`Assets`本文档后面列出的帮助器不可用。 相反，必须安装[ASP.NET 优化](http://nuget.org/packages/Microsoft.Web.Optimization/0.1)NuGet 包。 有关详细信息，请参阅[捆绑和缩小资产中的 ASP.NET Web Pages (Razor) 站点](https://go.microsoft.com/fwlink/?LinkId=255373)。
- 添加了其他程序集以支持 ASP.NET Web Pages 2。 此更改仅明显影响是，您可能看到的站点中的多个程序集*bin*文件夹后创建一个站点或将站点部署到托管提供商。

<a id="Changes_for_the_Beta_Version"></a>
### <a name="changes-for-the-beta-version-february-2012"></a>测试版 (2012 年 2 月) 的更改

在 2012 年 2 月发布的测试版有一些更改仅从已于 2011 年 12 月发布 Beta 版本。 这些更改是：

- Razor 现在支持条件属性。 在 HTML 元素，如果您将属性设置为一个值，解析到的服务器代码中`false`或`null`，ASP.NET 根本不会使该属性。 例如，假设您有一个复选框的以下标记：

    [!code-html[Main](top-features-in-web-pages-2/samples/sample1.html)]

    如果的值`checked1`解析为`false`或设置为`null`，则`checked`属性不呈现。 这是一项重大更改。
- `Validation.GetHtml`方法已重命名为`Validation.For`。 这是一项重大更改;`Validation.GetHtml` Beta 版本中不起。
- 现在可以包括`~`标记中的运算符，而无需使用引用的站点根目录`Href`函数。 (即，Razor 分析器可以现在找到并解决`~`而无需显式方法调用运算符`Href`。)`Href`方法仍然正常工作，因此这不是一项重大更改。

    例如，如果以前进行过标记，如下：

    `<a href="@Href("~/Default.cshtml")">Home</a>`

    现在可以使用标记，如下：

    `<a href="~/Default.cshtml">Home</a>`
- `Scripts`资产 （资源） 管理的帮助器替换`Assets`帮助器，具有略有不同的方法，如下所示：

  - 有关`Scripts.Add`，使用 `Assets.AddScript`
  - 有关`Scripts.GetScriptTags`，使用 `Assets.GetScripts`

    这是一项重大更改;`Scripts`类不是在 Beta 版本中可用。 已进行此更改更新本文档中使用资产管理的代码示例。

<a id="templates"></a>
### <a name="using-the-new-and-updated-site-templates"></a>使用新的和更新站点模板

**入门网站**模板已经过更新，以便在 Web Pages 2 上运行默认情况下。 它还包括以下新功能：

- 适合移动页面呈现。 通过使用 CSS 样式并`@media`选择器中，**入门网站**较小的屏幕，其中包括移动设备屏幕上提供改进的页的呈现。
- 改进的成员身份和身份验证选项。 您可以让用户登录到您的网站使用其帐户从其他社交网络网站，如 Twitter、 Facebook 和 Windows Live。 有关详细信息，请参阅[启用的登录名从 Facebook 和其他站点使用 OAuth 和 OpenID](#oauthsetup)部分。
- HTML5 元素。

新**个人网站**模板允许您创建包含个人博客、 照片页面和 Twitter 页面的网站。 你可以自定义基于站点**个人网站**模板执行以下操作：

- 通过编辑布局文件来更改网站的外观 (*\_SiteLayout.cshtml*) 和样式文件 (*Site.css*)。
- 将功能添加到你的站点的安装 NuGet 包。 有关如何安装包的信息，包括 ASP.NET Web Helpers Library，请参阅本教程[安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)。

访问**个人网站**模板中，选择**模板**上 WebMatrix**快速启动**屏幕。

[![topseven-personalsite-1](top-features-in-web-pages-2/_static/image2.png)](top-features-in-web-pages-2/_static/image1.png)

在中**模板**对话框框中，选择**个人网站**模板。

[![topseven-personalsite-2](top-features-in-web-pages-2/_static/image4.png)](top-features-in-web-pages-2/_static/image3.png)

登陆页**个人网站**模板，可单击的链接可设置您的博客，Twitter 页和照片页。

[![topseven-personalsite-3](top-features-in-web-pages-2/_static/image6.png)](top-features-in-web-pages-2/_static/image5.png)

<a id="validation"></a>
### <a name="validating-user-input"></a>验证用户输入

在 Web Pages 1 来验证用户输入提交窗体，您使用`System.Web.WebPages.Html.ModelState`类。 (这中所示的代码示例的几个 Web Pages 1 在本教程中标题为[使用数据](../data/5-working-with-data.md)。)仍可以在 Web Pages 2 中使用此方法。 但是，Web Pages 2 还提供了改进的工具，用于验证用户输入：

- 新的验证类，包括`System.Web.WebPages.ValidationHelper`和`System.Web.WebPages.Validator`，能够让你执行几行代码的功能强大的验证任务。
- （可选） 客户端验证，提供即时的反馈而不是请求到服务器的往返行程用户检查验证错误。 （出于安全原因，验证在服务器上，即使事先已在客户端中执行的检查。）

若要使用新的验证功能，请执行以下操作：

在页面的代码中，注册要使用的方法验证元素`Validation`帮助程序： `Validation.RequireField`， `Validation.RequireFields` （若要注册多个元素为必需），或`Validation.Add`。 `Add`方法允许您指定其他类型的验证检查，类似于数据类型检查、 比较不同的字段，字符串长度检查中的条目和模式 （使用正则表达式）。 下面是一些可能的恶意活动：

[!code-html[Main](top-features-in-web-pages-2/samples/sample2.html)]

若要显示特定于字段的错误，请调用`Html.ValidationMessage`正在验证每个元素的标记中：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample3.cshtml)]

若要显示的摘要 (`<ul>`列表) 在页中，所有错误的`Html.ValidationSummary`标记中：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample4.cshtml)]

这些步骤，即可实现服务器端验证。 如果你想要添加客户端验证，请执行以下此外。

添加以下脚本文件引用内部`<head>`web 页面的部分。 前两个脚本引用指向内容交付网络 (CDN) 服务器上的远程文件。 第三个引用将指向本地脚本文件。 当 CDN 不可用时，生产应用应实现回退。 测试回退。

[!code-html[Main](top-features-in-web-pages-2/samples/sample5.html)]

若要获取的本地副本的最简单方法*jquery.validate.unobtrusive.min.js*库是创建新的 Web Pages 站点基于之一 （如入门网站） 的站点模板。 由模板创建该站点包括*jquery.validate.unobtrusive.js*其 Scripts 文件夹中，从中您可以将其复制到你的站点中的文件。

如果你的网站使用<em>\_SiteLayout</em>来控制页面布局页上，可以在该页面中包含这些脚本引用，以便验证可供所有内容页面。 如果你想要仅在特定页面上执行验证，您可以使用资产管理器注册仅这些页上的脚本。 若要执行此操作，调用`Assets.AddScript(path)`中你想要验证并引用每个脚本文件的页。 然后添加对的调用`Assets.GetScripts`中 <em>\_SiteLayout</em>以便呈现的已注册`<script>`标记。 有关详细信息，请参阅明[与资产管理器注册脚本](#resmanagement)。

在单个元素的标记，调用`Validation.For`方法。 此方法发出属性，jQuery 可以挂接以便提供客户端验证。 例如：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample6.cshtml)]

下面的示例显示了页面，用于验证用户输入窗体上。 若要运行和测试此验证代码，请执行此操作：

1. 创建新的 web 站点使用包括 WebMatrix 2 站点模板之一*脚本*文件夹，如**入门网站**模板。
2. 在新站点中，创建一个新 *.cshtml*页和页的内容替换为以下代码。
3. 在浏览器中运行页。 输入有效和无效值，以查看上验证的效果。 例如，将必填的字段保留为空或输入的字母**信用额度**字段。


[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample7.cshtml)]

以下是页，当用户提交有效的输入：

[![topSeven-valid-1](top-features-in-web-pages-2/_static/image8.png)](top-features-in-web-pages-2/_static/image7.png)

当用户提交它与必填字段留空时，以下是页：

[![topSeven-valid-2](top-features-in-web-pages-2/_static/image10.png)](top-features-in-web-pages-2/_static/image9.png)

以下是页，当用户提交它内的整数非**信用额度**字段：

[![topSeven-valid-3](top-features-in-web-pages-2/_static/image12.png)](top-features-in-web-pages-2/_static/image11.png)

有关详细信息，请参阅以下博客文章：

- [更新 Web Pages v2 中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2344)添加验证使用的基础知识`Validation`帮助程序 （仅服务器端）
- [更新 Web Pages v2，第 2 部分中的验证](http://www.mikepope.com/blog/DisplayBlog.aspx?permalink=2347)添加客户端验证。
- [更新 Web Pages v2，第 3 部分中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2351)格式设置验证错误。

<a id="resmanagement"></a>
### <a name="registering-scripts-using-the-assets-manager"></a>注册脚本使用资产管理器

资产管理器是一项新功能，可以使用在服务器代码中进行注册和呈现客户端脚本。 使用在运行时组合到一个页面的多个文件 （如布局页中，内容页面、 帮助程序，等等） 中的代码时，此功能很有用。 资产管理器协调源代码文件，以确保正确引用脚本文件和有效地在呈现的页上，而不考虑哪些代码文件从调用的或者它们被称为多少次。 资产管理器还会呈现`<script>`标记在正确的位置，以便可以快速 （而无需下载脚本在呈现时） 加载此页面，以避免可能发生在呈现之前调用脚本的错误已完成。

例如，假设您创建的自定义帮助程序调用的 JavaScript 文件，并在内容页面代码中三个不同位置上调用此帮助器。 如果不使用的资产管理器注册该脚本调用中帮助程序，三个不同`<script>`都指向同一个脚本文件将显示在呈现页面中的标记。 此外，具体取决于 where`<script>`标记插入到呈现的页面中，如果脚本会尝试访问某些页面元素在页面完全加载之前可能发生错误。 如果您使用资产管理器注册的脚本，则避免这些问题。

您可以使用资产管理器注册一个脚本，通过执行此操作：

- 在代码中，需要引用该脚本，调用`Assets.AddScript`方法。
- 在中 *\_SiteLayout*页上，调用`Assets.GetScripts`方法以呈现`<script>`标记。 

    > [!NOTE]
    > 将对的调用放`Assets.GetScripts`作为中的最后一项`<body>`的元素 *\_SiteLayout*页。 这可以帮助页面加载速度更快，并有助于避免出现脚本错误。

下面的示例显示了资产管理器工作原理。 代码包含以下各项：

- 名为的自定义帮助程序`MakeNote`。 此帮助器将呈现一个框内的字符串通过包装`div`围绕它的元素的边框以及添加已设置样式&quot;注意：&quot;到它。 帮助器也会调用向该便笺添加运行时行为的 JavaScript 文件。 而不是引用的脚本`<script>`标记，该帮助器注册脚本通过调用`Assets.AddScript`。
- 一个 JavaScript 文件。 这是由帮助程序，名为的文件和临时增加了期间注意项的字体大小`mouseover`事件。
- 内容页中，即在引用<em>\_SiteLayout</em>页上，将呈现在正文中，一些内容，然后调用`MakeNote`帮助器。
- 一个 *\_SiteLayout*页。 本页面提供通用标头和页面布局结构。 它还包括调用`Assets.GetScripts`，这是资产管理器如何呈现脚本调用在页面中。

运行示例：

1. 创建一个空的 Web Pages 2 网站。 你可以使用 WebMatrix**空站点**此模板。
2. 创建名为的文件夹*脚本*站点中。
3. 在中*脚本*文件夹中，创建名为的文件*Test.js*，复制*Test.js*到该内容从该示例中，并保存该文件...
4. 创建名为的文件夹*应用程序\_代码*站点中。
5. 在中*应用程序\_代码*文件夹中，创建名为的文件*Helpers.cshtml*，将示例代码复制到它，并将其保存在名为的文件夹中*应用\_代码*根文件夹中。
6. 在站点的根文件夹中创建名为的文件 *\_SiteLayout.cshtml，* 的示例复制到它，并保存该文件。
7. 在站点根目录中创建名为的文件*ContentPage.cshtml*、 添加示例代码，并将其保存。
8. 运行*ContentPage*在浏览器中。 传递给字符串`MakeNote`帮助器呈现为装箱的注意。
9. 鼠标指针经过注意。 该脚本将暂时增加便笺的字体大小。
10. 查看呈现的页面上的源。 由于对的调用放置`Assets.GetScripts`，呈现`<script>`调用的标记*Test.js*是页的正文中的最后一个项。

*Test.js*

[!code-javascript[Main](top-features-in-web-pages-2/samples/sample8.js)]

*Helpers.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample9.cshtml)]

*\_SiteLayout.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample10.html)]

*ContentPage.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample11.cshtml)]

以下屏幕截图显示*ContentPage.cshtml*在浏览器中当鼠标指针拖过注释：

[![topSeven-resmgr-1](top-features-in-web-pages-2/_static/image14.png)](top-features-in-web-pages-2/_static/image13.png)

<a id="oauthsetup"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名

Web Pages 2 提供了增强的成员身份和身份验证的选项。 主要增强功能是有的新[OAuth](http://oauth.net/)并[OpenID](http://openid.net/)提供程序。 使用这些提供程序，可让你使用 Facebook、 Twitter、 Windows Live、 Google 和 Yahoo 从其现有凭据的站点到用户登录。 例如，若要使用 Facebook 帐户登录，用户可以只需选择 Facebook 图标，将它们重定向到它们在其中输入他们的用户信息的 Facebook 登录页。 它们然后可以将 Facebook 登录你的站点上与其帐户相关联。 Web Pages 成员资格功能相关的增强功能是使用你的网站上的单个帐户，用户可以将多个登录名 （包括登录名从社交网站） 相关联。

下图显示了从登录页面**入门网站**模板，用户可以在其中选择一个 Facebook、 Twitter 或 Windows Live 图标，以启用日志记录使用的外部帐户：

[![topSeven-oauth-1](top-features-in-web-pages-2/_static/image16.png)](top-features-in-web-pages-2/_static/image15.png)

你可以启用 OAuth 和 OpenID 的成员身份使用几行代码。 您使用的方法和属性以使用 OAuth 和 OpenID 提供程序位于`WebMatrix.Security.OAuthWebSecurity`类。

但是，而不是使用代码以启用从其他站点的登录名，开始使用新的提供程序的推荐的方法是使用新**入门网站**随 WebMatrix 2 Beta 的模板。 **入门网站**模板包括完整的成员身份基础结构，需要让用户登录到你使用本地凭据或来自另一个站点的站点登录页、 成员资格数据库，与所有的代码完成.

#### <a name="how-to-enable-logins-using-the-oauth-and-openid-providers"></a>如何启用登录名使用 OAuth 和 OpenID 提供程序

本部分举例说明如何让用户从外部站点 （Facebook、 Twitter、 Windows Live、 Google 或 Yahoo） 登录到基于站点**入门网站**模板。 在创建后入门网站，你执行操作 （详细信息按照）：

- 使用 OAuth 提供程序 （Facebook、 Twitter 和 Windows Live） 的站点，外部站点上创建应用程序。 这样，您将需要为了调用这些站点的登录功能的应用程序密钥。 对于使用 OpenID 提供程序 （Google、 Yahoo） 的站点，不需要创建应用程序。 对于所有这些站点，必须具有一个帐户，以便在中记录并创建开发人员应用程序。 

    > [!NOTE]
    > Windows Live 应用程序仅接受工作网站的实时 URL，因此不能用于本地网站 URL 测试登录名。
- 编辑你的网站中的几个文件以指定适当的身份验证提供程序，并将提交到想要使用的站点的登录名。

**若要启用 Google 和 Yahoo 登录**:

1. 在你的网站，编辑 *\_AppStart.cshtml*页上，在 Razor 代码块中调用后面添加以下两行代码`WebSecurity.InitializeDatabaseConnection`方法。 此代码将启用 Google 和 Yahoo OpenID 提供程序。 

    [!code-css[Main](top-features-in-web-pages-2/samples/sample12.css)]
2. 在中 *~/Account/Login.cshtml*页上，从下列选项中删除注释`<fieldset>`快要结束的页面的标记块。 若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。 生成的代码块如下所示：

    [!code-html[Main](top-features-in-web-pages-2/samples/sample13.html)]
3. 添加`<input>`元素的 Google 或 Yahoo 提供程序`<fieldset>`组中 *~/Account/Login.cshtml*页。 已更新`<fieldset>`组`<input>`元素 Google 和 Yahoo 看起来如以下示例： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample14.html)]
4. 在中 *~/Account/AssociateServiceAccount.cshtml*页上，添加`<input>`Google 或 Yahoo 到元素`<fieldset>`组在文件末尾附近。 你可以复制相同`<input>`刚添加到的元素`<fieldset>`主题中 *~/Account/Login.cshtml*页。 

    *~/Account/AssociateServiceAccount.cshtml*可以使用入门网站模板中的页，如果你想要创建的用户可以将其他站点中的多个登录名关联与单个帐户在网站上的页面。

现在，你可以测试 Google 和 Yahoo 登录名。

1. 运行*default.cshtml*您的网站上，然后选择**登录**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Google**或者**Yahoo**提交按钮。 此示例使用 Google 登录名。 

    Web 页面将请求重定向到 Google 登录页。

    [![topSeven-oauth-6](top-features-in-web-pages-2/_static/image18.png)](top-features-in-web-pages-2/_static/image17.png)
3. 输入现有 Google 帐户凭据。
4. 如果出现要求你是否想要允许本地主机要使用帐户中的信息，请单击 Google**允许**。

    代码使用 Google 的令牌对用户进行身份验证，然后返回到此页上你的网站。 此页，可以将其 Google 登录名与你的网站上的现有帐户相关联的用户或用户可以在注册你将使用的外部登录名相关联的站点上的新帐户。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image20.png)](top-features-in-web-pages-2/_static/image19.png)
5. 选择**相关联**按钮。 在浏览器返回到应用程序的主页。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image22.png)](top-features-in-web-pages-2/_static/image21.png)

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image24.png)](top-features-in-web-pages-2/_static/image23.png)

**若要启用 Facebook 登录名**:

1. 转到[Facebook 开发人员站点](https://developers.facebook.com/apps)（如果尚未登录，则日志）。
2. 选择**创建新应用**按钮，然后按照提示进行命名和创建新的应用程序。
3. 在部分**选择如何将您的应用程序与 Facebook**，选择**网站**部分。
4. 填写**站点 URL**字段与你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。 **域**字段是可选的; 可以使用此提供对整个域的身份验证 (如*example.com*)。 

    > [!NOTE]
    > 如果你使用 URL 在本地计算机上运行站点喜欢`http://localhost:12345`（其中数是本地端口号），可以添加此值设置为**站点 URL**字段用于测试你的站点。 但是，任何时候，只要你的本地站点更改的端口号，你将需要更新**站点 URL**字段的应用程序。
5. 选择**保存更改**按钮。
6. 选择**应用**同样，选项卡，然后查看你的应用程序的起始页。
7. 复制**应用程序 ID**并**应用程序密码**为应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Facebook 提供程序。
8. 退出 Facebook 开发人员网站。

现在您更改两个页面中你的网站，以便用户将能够登录到网站使用其 Facebook 帐户。

1. 在你的网站，编辑 *\_AppStart.cshtml*页上，并取消注释的代码，为 Facebook OAuth 提供程序。 取消注释的代码块如以下所示： 

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample15.xml)]
2. 复制**应用程序 ID**从 Facebook 应用程序的值作为值`consumerKey`参数 （在引号内）。
3. 复制**应用程序机密**从 Facebook 应用程序作为值`consumerSecret`参数值。
4. 保存并关闭文件。
5. 编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。 若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。 带有注释的代码块中删除类似于以下内容： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample16.html)]
6. 保存并关闭文件。

现在，你可以测试 Facebook 登录名。

1. 运行该站点*default.cshtml*页上，然后选择**登录名**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Facebook**图标。 

    Web 页面将请求重定向到 Facebook 登录页。

    [![topSeven-oauth-2](top-features-in-web-pages-2/_static/image26.png)](top-features-in-web-pages-2/_static/image25.png)
3. 登录到 Facebook 帐户。 

    代码使用 Facebook 令牌进行身份验证，然后返回到页您可以在其中将 Facebook 登录名与站点的登录名相关联。 你的用户名称或电子邮件地址填充到**电子邮件**字段在窗体上。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image28.png)](top-features-in-web-pages-2/_static/image27.png)
4. 选择**相关联**按钮。 

    在浏览器返回到主页并登录。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image30.png)](top-features-in-web-pages-2/_static/image29.png)

**若要启用 Twitter 登录名：** 

1. 浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。
2. 选择**创建应用**链接，然后登录到网站。
3. 上**创建的应用程序**窗体中，填写**名称**并**说明**字段。
4. 在中**网站**字段中，输入你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。 

    > [!NOTE]
    > 如果您要测试你的本地站点 (使用类似`http://localhost:12345`)，Twitter 可能不接受 URL。 但是，您可能能够使用本地环回 IP 地址 (例如`http://127.0.0.1:12345`)。 这将简化测试本地应用程序的过程。 但是，每次你的本地网站的端口号更改，你将需要更新**网站**字段的应用程序。
5. 在中**回叫 URL**字段中，输入你希望用户在登录后到 Twitter 到返回的网站中的页面的 URL。 例如，若要向用户发送到入门网站 （它将识别其登录的状态） 的主页上，输入中输入的同一个 URL**网站**字段。
6. 接受条款，然后选择**创建 Twitter 应用程序**按钮。
7. 上**我的应用程序**登陆页上，选择你创建的应用程序。
8. 上**详细信息**选项卡上，滚动到底部并选择**创建我的访问令牌**按钮。
9. 上**详细信息**选项卡上，复制**使用者密钥**并**使用者机密**为应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Twitter 提供程序。
10. 退出 Twitter 网站。

现在您更改两个页面中你的网站，以便用户能够登录到使用 Twitter 帐户的站点。

1. 在你的网站，编辑 *\_AppStart.cshtml*页面和 Twitter OAuth 提供程序取消注释的代码。 取消注释的代码块如下所示： 

    [!code-csharp[Main](top-features-in-web-pages-2/samples/sample17.cs)]
2. 复制**使用者密钥**从 Twitter 应用程序的值作为值`consumerKey`参数 （在引号内）。
3. 复制**使用者机密**从 Twitter 应用程序的值作为值`consumerSecret`参数。
4. 保存并关闭文件。
5. 编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。 若要取消注释的代码，请删除`@*`字符之前和之后`<fieldset>`块。 带有注释的代码块中删除类似于以下内容： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample18.html)]
6. 保存并关闭文件。

现在，你可以测试 Twitter 登录名。

1. 运行*default.cshtml*您的网站上，然后选择**登录名**按钮。
2. 上*登录名*页上，在**使用其他服务进行登录**部分中，选择**Twitter**图标。 

    Web 页面将请求重定向到 Twitter 登录页面为您创建的应用程序。

    [![topSeven-oauth-4](top-features-in-web-pages-2/_static/image32.png)](top-features-in-web-pages-2/_static/image31.png)
3. 登录到 Twitter 帐户。
4. 代码使用 Twitter 令牌进行身份验证用户，然后返回到页你可以将关联您使用您网站的帐户的登录名。 名称或电子邮件地址填充到**电子邮件**字段在窗体上。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image34.png)](top-features-in-web-pages-2/_static/image33.png)
5. 选择**相关联**按钮。 

    在浏览器返回到主页并登录。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image36.png)](top-features-in-web-pages-2/_static/image35.png)

<a id="maphelper"></a>
### <a name="adding-maps-using-the-maps-helper"></a>添加映射使用映射帮助器

Web Pages 2 包括添加到 ASP.NET Web Helpers Library，这是 Web Pages 站点加载项的包。 其中一种是由提供的映射组件`Microsoft.Web.Helpers.Maps`类。 可以使用`Maps`类生成基于一个地址或一组的经度和纬度坐标的地图。 `Maps`类的允许您直接在包括必应、 Google、 MapQuest 和 Yahoo 的常用映射引擎调用。

若要使用新`Maps`类在你的网站，您必须首先安装 Web Helpers Library 版本 2。 若要执行此操作，请转到用于安装当前版本的说明[ASP.NET Web Helpers Library](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)并安装版本 2。

向页面添加映射的步骤是相同的调用无论哪个映射引擎的。 您只需添加对映射页的 JavaScript 文件引用，然后再添加呈现的调用`<script>`上您的页面的标记。 然后在映射页中上, 调用你想要使用的映射引擎。

下面的示例演示如何创建将基于一个地址，结构图呈现的页面和呈现地图基于经度和纬度坐标的另一页。 地址映射示例使用 Google 地图和坐标映射示例使用必应地图。 请注意在代码中的以下元素：

- 对调用`Assets.AddScript`在两个映射页的顶部。 此方法将添加到的引用*jquery 1.6.2.min.js*附带的文件**入门网站**模板和所要求的`Maps`类。
- 对调用`Assets.GetScripts`布局文件中的方法。 此方法将呈现`<script>`两个映射页上标记。
- 在调用`@Maps.GetGoogleHtml`和`@Maps.GetBingHtml`映射页中的方法。 若要查找某个地址，必须传递地址字符串。 若要映射的坐标，必须通过经度和纬度坐标。 对于必应地图引擎中，你还必须传递一个密钥 (通过在注册获取免费[必应地图开发人员站点](https://www.microsoft.com/maps/developers/web.aspx))。 其他映射引擎的方法的工作方式类似 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。

若要创建映射页：

1. 创建基于网站**入门网站**模板。
2. 创建名为的文件*MapAddress.cshtml*站点的根目录中。 此页面将生成基于将传递给它的地址的映射。
3. 将以下代码复制到文件中，覆盖现有内容。 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample19.cshtml)]
4. 创建名为的文件 *\_MapLayout.cshtml*站点的根目录中。 此页将为两个映射页的布局页。
5. 将以下代码复制到文件中，覆盖现有内容。 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample20.html)]
6. 创建名为的文件*MapCoordinates.cshtml*站点的根目录中。 此页面将生成基于一组向其传递的坐标的映射。
7. 将以下代码复制到文件中，覆盖现有内容。 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample21.cshtml)]

若要测试映射页：

1. 运行页*MapAddress.cshtml*文件。
2. 输入包括街道地址、 状态或省和邮政编码，完整地址字符串，然后选择**Map It**按钮。 呈现地图页面，从 Google 地图： 

    [![topseven-maphelper-1](top-features-in-web-pages-2/_static/image38.png)](top-features-in-web-pages-2/_static/image37.png)
3. 找到的特定位置的纬度和经度坐标集。
4. 运行页*MapCoordinates.cshtml*。 输入坐标，然后选择**Map It**按钮。 页面从必应地图呈现地图： 

    [![topseven-maphelper-2](top-features-in-web-pages-2/_static/image40.png)](top-features-in-web-pages-2/_static/image39.png)

<a id="sidebyside"></a>
### <a name="running-web-pages-applications-side-by-side"></a>运行 Web Pages 应用程序并排显示

Web Pages 2 添加了运行应用程序并排显示的功能。 这样可以继续运行 Web Pages 1 应用程序，构建新的 Web Pages 2 应用程序，并在同一台计算机上运行所有这些。

下面是要使用 WebMatrix 安装 Web Pages 2 试用版时，应注意一些事项：

- 默认情况下，现有的 Web Pages 应用程序将在计算机上运行作为版本 2 应用程序。 （版本 2 的程序集安装到 GAC 中并且将自动使用。）
- 如果你想要运行使用 Web Pages 版本 1 （而不是默认值，如下所示的上一个点） 的站点，您可以配置要执行此操作的站点。 如果您的网站还没有*web.config*文件位于站点的根目录中，创建一个新，并将以下 XML 复制到其中，覆盖现有内容。 如果站点中已包含*web.config*文件中，添加`<appSettings>`元素到如下`<configuration>`部分。

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample22.xml)]
  -如果未指定的版本中*web.config*文件中，将站点部署为版本 2 站点。 (第 2 版程序集复制到*bin*已部署站点中的文件夹。)
- Web Matrix 2 Beta 在站点中包含 Web Pages 版本 2 程序集的版本中使用的站点模板创建的新应用程序*bin*文件夹。

一般情况下，您可以始终控制 Web 页以使用你的网站，通过使用 NuGet 将相应的程序集安装到站点的哪些版本*bin*文件夹。 若要查找程序包，请访问[NuGet.org](http://NuGet.org)。

<a id="mobile"></a>
### <a name="rendering-pages-for-mobile-devices"></a>移动设备的呈现页

Web Pages 2 允许您移动或其他设备上创建自定义显示的呈现内容。

`System.Web.WebPages`命名空间包含允许您使用的显示模式的以下类： `DefaultDisplayMode`， `DisplayInfo`，和`DisplayModes`。 你可以直接使用这些类，并写入呈现特定设备的正确输出的代码。

或者，可以通过使用此类文件命名模式创建特定于设备的页面：<em>文件名。</em><em>Mobile</em><em>.cshtml</em>。 例如，可以创建两个版本的页上，一个名为<em>MyFile.cshtml</em>另一个名为<em>MyFile.Mobile.cshtml</em>。 在运行的时，移动设备的请求时<em>MyFile.cshtml</em>，将从内容呈现在网页<em>MyFile.Mobile.cshtml</em>。 否则为<em>MyFile.cshtml</em>呈现。

下面的示例演示如何通过添加内容页的移动设备启用移动呈现。 *Page1.cshtml*包含内容，以及导航侧边栏。 *Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。

若要生成并运行的代码示例：

1. 在 Web Pages 站点中，创建名为的文件*Page1.cshtml*并复制*Page1.cshtml*到该示例的内容。
2. 创建名为的文件*Page1.Mobile.cshtml*并复制*Page1.Mobile.cshtml*到该示例的内容。 请注意，页上的移动版本省略以便更好地呈现在较小屏幕上的导航部分。
3. 运行桌面浏览器并浏览到*Page1.cshtml*。
4. 运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。 请注意，这一次 Web 页呈现页的移动版本。 

    > [!NOTE]
    > 若要测试移动页面，可以使用在桌面计算机运行的移动设备模拟器。 此工具允许您测试网页，如他们的移动设备上的外观 （即，通常使用小得多显示区域）。 模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/)Mozilla firefox，它可以模拟各种移动浏览器，从桌面版本的 Firefox。

*Page1.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample23.html)]

*Page1.Mobile.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample24.html)]

*Page1.cshtml*桌面浏览器中呈现：

[![topseven-displaymodes-1](top-features-in-web-pages-2/_static/image42.png)](top-features-in-web-pages-2/_static/image41.png)

*Page1.Mobile.cshtml* Firefox 浏览器中的 Apple iPhone 模拟器视图中显示。 即使该请求是对*Page1.cshtml*，应用程序呈现*Page1.Mobile.cshtml*。

[![topseven-displaymodes-2](top-features-in-web-pages-2/_static/image44.png)](top-features-in-web-pages-2/_static/image43.png)

<a id="resources"></a>
## <a name="additional-resources"></a>其他资源

### <a name="aspnet-web-pages-1-resources"></a>ASP.NET Web Pages 1 资源

> [!NOTE]
> 大多数 Web Pages 1 编程和 API 资源仍适用于 Web Pages 2。

- [ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkId=202890)

### <a name="webmatrix-resources"></a>WebMatrix 资源

- [WebMatrix 2 新增功能](http://webmatrix.com/next)
- [Microsoft WebMatrix 站点](https://go.microsoft.com/fwlink/?LinkID=195076)
- [使用 Microsoft WebMatrix 开始 Web 开发](https://msdn.microsoft.com/en-us/library/hh145669(v=VS.99).aspx)（包括完整的示例 Web Pages 应用程序）
