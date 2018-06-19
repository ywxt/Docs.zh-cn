---
uid: web-pages/overview/releases/top-features-in-web-pages-2
title: 所需的 ASP.NET Web Pages 2 中的顶部功能 |Microsoft 文档
author: microsoft
description: 本主题概述在 ASP.NET 网页 2 中，一个附带 WebMatr 的轻型 web 编程框架的顶部新功能...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: cc712e72-c3d0-4e43-bc2d-28cc09cd8f71
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/releases/top-features-in-web-pages-2
msc.type: authoredcontent
ms.openlocfilehash: f0d32edd3ab54c55aa06c803cd91e01cbbb8f08a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30899377"
---
<a name="the-top-features-in-aspnet-web-pages-2"></a>在 ASP.NET Web Pages 2 靠前的特征
====================
by [Microsoft](https://github.com/microsoft)

> 本文概述了 ASP.NET Web Pages 2 RC，附带的轻型 web 编程框架中最新功能的[Microsoft WebMatrix 2 RC](https://www.microsoft.com/web/)。
> 
> **包含的内容：** 
> 
> - [安装 WebMatrix](#install)
> - [新的和增强功能](#New_and_Enhanced_Features)
> 
>     - [对于 RC 版本更改](#Changes_for_the_RC_Version)
>     - [Beta 版的更改](#Changes_for_the_Beta_Version)
>     - [使用新的和更新站点模板](#templates)
>     - [验证用户输入](#validation)
>     - [启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名](#oauthsetup)
>     - [添加使用地图帮助程序图](#maphelper)
>     - [运行 Web 页面应用程序并行](#sidebyside)
>     - [为移动设备中呈现页](#mobile)
> - [其他资源](#resources)
> 
> > [!NOTE]
> > 本主题假定使用 WebMatrix 的目的若要使用 ASP.NET Web Pages 2 代码。 但是，由于 Web Pages 1，您可以创建使用 Visual Studio Web Pages 2 网站，它会为你提供增强的 IntelliSense 功能和调试。 若要使用 Visual Studio 中的网页，你必须首先安装 Visual Studio 2010 SP1、 Visual Web Developer Express 2010 SP1 中或 Visual Studio 11 Beta。 然后，安装 ASP.NET MVC 4 Beta 的说明进行操作，其中包括模板和工具用于在 Visual Studio 中创建 ASP.NET MVC 4 和 Web Pages 2 的应用程序。
> 
> 
> *上次更新： 2012 年 6 月 18*


<a id="install"></a>
## <a name="installing-webmatrix"></a>安装 WebMatrix

若要安装 Web 页，可以使用 Microsoft Web 平台安装程序，这是一个免费的应用程序，可以轻松地安装和配置 web 相关技术。 将安装 WebMatrix 2 Beta，其中包括 Web Pages 2 Beta。

1. 浏览到 Web 平台安装程序的最新版本的安装页面：

    [https://go.microsoft.com/fwlink/?LinkId=226883](https://go.microsoft.com/fwlink/?LinkId=226883)

    > [!NOTE]
    > 如果你没有安装 WebMatrix 1，此安装程序更新它为 WebMatrix 2 Beta。 你可以运行在同一台计算机上使用版本 1 或 2 创建的网站。 有关详细信息，请参阅部分[运行网页的应用程序并行](#sidebyside)。
2. 选择**立即安装**。 

    如果你使用 Internet Explorer，请转到下一步。 如果你使用不同的浏览器，如 Mozilla Firefox 或 Google Chrome，则会提示您保存*Webmatrix.exe*到你的计算机的文件。 保存该文件，然后单击它以启动安装程序。
3. 运行安装程序并选择**安装**按钮。 这将安装 WebMatrix 和 Web 页。

## <a id="New_and_Enhanced_Features"></a>  新的和增强功能

### <a id="Changes_for_the_RC_Version"></a>  RC 版本 (2012 年 6 月) 的更改

在 2012 年 6 月 RC 版本发布具有少量更改从 2012 年 3 月发布的 Beta 版本刷新。 这些更改包括：

- A`Validation.AddFormError`方法已添加到`Validation`帮助器。 这是手动执行验证的情况下很有用 （例如，验证查询字符串中传递一个值） 和你想要添加可由显示的错误消息`Html.ValidationSummary`方法。 有关详细信息，请参阅明[验证数据，不会直接从用户](https://go.microsoft.com/fwlink/?LinkId=253002#Validating_Data_That_Doesnt_Come_Directly_from_Users)中[ASP.NET Web 页 (Razor) 站点中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)。
- 已从核心 ASP.NET 网页 2 程序集绑定和缩减的功能。 因此，`Assets`本文档后面部分中列出的帮助器不可用。 相反，你必须安装[ASP.NET 优化](http://nuget.org/packages/Microsoft.Web.Optimization/0.1)NuGet 包。 有关详细信息，请参阅[捆绑和贴图层 ASP.NET Web 页 (Razor) 站点中的资产](https://go.microsoft.com/fwlink/?LinkId=255373)。
- 添加了其他程序集以支持 ASP.NET Web Pages 2。 此更改仅明显的影响是，你可能看到的站点中的多个程序集*bin*后创建一个站点或将站点部署到宿主提供程序的文件夹。

<a id="Changes_for_the_Beta_Version"></a>
### <a name="changes-for-the-beta-version-february-2012"></a>对于 Beta 版本 (2012 年 2 月) 的更改

在 2012 年 2 月发布的 Beta 版本具有来自于 2011 年 12 月发布的 Beta 版本仅少量更改。 这些更改包括：

- Razor 现在支持条件属性。 在 HTML 元素，如果你将属性设置为一个值，解析到的服务器代码中`false`或`null`，ASP.NET 不会在所有呈现该属性。 例如，假设有一个复选框的以下标记：

    [!code-html[Main](top-features-in-web-pages-2/samples/sample1.html)]

    如果值`checked1`解析为`false`或`null`、`checked`不呈现属性。 这是一项重大更改。
- `Validation.GetHtml`方法已重命名为`Validation.For`。 这是一项重大更改;`Validation.GetHtml` Beta 版本中将不工作。
- 你现在可以包含`~`运算符在标记中无需使用引用的站点根目录`Href`函数。 (即，Razor 分析器可以现在找到并解决`~`而无需对的显式方法调用运算符`Href`。)`Href`方法仍然正常工作，因此这不是一项重大更改。

    例如，如果你以前标记如下：

    `<a href="@Href("~/Default.cshtml")">Home</a>`

    你现在可以使用标记如下：

    `<a href="~/Default.cshtml">Home</a>`
- `Scripts`帮助资产 （资源） 管理器已替换`Assets`帮助器，有略有不同的方法，如下所示：

  - 有关`Scripts.Add`，使用 `Assets.AddScript`
  - 有关`Scripts.GetScriptTags`，使用 `Assets.GetScripts`

    这是一项重大更改;`Scripts`类不是在 Beta 版本中可用。 进行此更改后已更新使用资产管理本文档中的代码示例。

<a id="templates"></a>
### <a name="using-the-new-and-updated-site-templates"></a>使用新的和更新站点模板

**入门站点**模板已更新以便使其在网页 2 上运行默认情况下。 它还包括以下新功能：

- 良好移动性页面呈现。 通过使用 CSS 样式和`@media`选择器，**入门站点**较小的屏幕，包括移动设备屏幕上提供改进的呈现的页。
- 改进的成员身份和身份验证选项。 你可以让用户登录到你从 Twitter、 Facebook、 和 Windows Live 等其他社交网络站点中使用其帐户的站点。 有关详细信息，请参阅[将登录名启用从 Facebook 和其他站点使用 OAuth 和 OpenID](#oauthsetup)部分。
- HTML5 元素。

新**个人站点**模板允许你创建包含个人博客、 照片页和 Twitter 页面的网站。 你可以自定义基于站点**个人站点**通过执行以下模板：

- 通过编辑布局文件来更改查找范围的站点 (*\_SiteLayout.cshtml*) 和样式文件 (*Site.css*)。
- 安装 NuGet 包可将功能添加到你的站点。 有关如何安装包的信息，包括 ASP.NET Web 帮助程序库，请参阅本教程[安装帮助器](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)。

访问**个人站点**模板中，选择**模板**上 WebMatrix**快速启动**屏幕。

[![topseven-personalsite-1](top-features-in-web-pages-2/_static/image2.png)](top-features-in-web-pages-2/_static/image1.png)

在**模板**对话框框中，选择**个人站点**模板。

[![topseven-personalsite-2](top-features-in-web-pages-2/_static/image4.png)](top-features-in-web-pages-2/_static/image3.png)

登录页**个人站点**模板允许你跟踪链接以设置您的博客，Twitter 页和照片页。

[![topseven-personalsite-3](top-features-in-web-pages-2/_static/image6.png)](top-features-in-web-pages-2/_static/image5.png)

<a id="validation"></a>
### <a name="validating-user-input"></a>验证用户输入

在 Web 页 1 来验证用户输入提交窗体上，你使用`System.Web.WebPages.Html.ModelState`类。 (此进行了阐释几个代码示例中标题为网页 1 教程[使用数据](../data/5-working-with-data.md)。)你仍可以在 Web Pages 2 中使用此方法。 但是，Web Pages 2 还提供改进的工具，用于验证用户输入：

- 新的验证类，包括`System.Web.WebPages.ValidationHelper`和`System.Web.WebPages.Validator`，能够让你执行功能强大的验证任务使用的代码的几行。
- （可选） 提供即时的反馈给此用户而不是要求到服务器的往返行程，以检查是否有验证错误的客户端验证。 （出于安全原因，验证在服务器上即使事先在客户端执行检查。）

若要使用新的验证功能，请执行以下操作：

在页面的代码中，注册要由使用的方法验证元素`Validation`帮助器： `Validation.RequireField`， `Validation.RequireFields` （若要注册多个元素是必需），或`Validation.Add`。 `Add`方法允许您指定其他类型的验证检查，如数据类型检查、 比较不同的字段，字符串长度检查中的条目并模式 （使用正则表达式）。 下面是一些可能的恶意活动：

[!code-html[Main](top-features-in-web-pages-2/samples/sample2.html)]

若要显示特定于字段的错误，请调用`Html.ValidationMessage`正被验证每个元素的标记中：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample3.cshtml)]

若要显示的摘要 (`<ul>`列表) 的在页中，所有错误`Html.ValidationSummary`标记中：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample4.cshtml)]

这些步骤足以实现服务器端验证。 如果你想要添加客户端验证，执行以下此外。

添加以下脚本文件引用内的`<head>`web 页的部分。 前两个脚本引用点移到内容交付网络 (CDN) 服务器上的远程文件。 第三个引用将指向本地脚本文件。 CDN 不可用时，生产应用程序应实现回退。 测试回退。

[!code-html[Main](top-features-in-web-pages-2/samples/sample5.html)]

若要获取的本地副本的最简单方法*jquery.validate.unobtrusive.min.js*库是创建新的 Web 页站点基于之一 （如入门站点） 的站点模板。 由模板创建该网站包含*jquery.validate.unobtrusive.js*其脚本文件夹中，从中你可以将其复制到你的站点中的文件。

如果你的网站使用<em>\_SiteLayout</em>页来控制页面布局中，你可以在该页中包括这些脚本引用，以便验证可供所有内容页。 如果你想要仅在特定的页上执行验证，你可以使用的资产管理器注册仅这些页面上的脚本。 若要执行此操作，调用`Assets.AddScript(path)`中你想要验证并引用每个脚本文件的页。 然后添加对的调用`Assets.GetScripts`中 <em>\_SiteLayout</em>以便呈现的已注册的页`<script>`标记。 有关详细信息，请参阅明[与资产管理器注册脚本](#resmanagement)。

单个元素的标记，在调用`Validation.For`方法。 此方法发出特性该 jQuery 可以挂钩以便提供客户端验证。 例如：

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample6.cshtml)]

下面的示例演示验证窗体上的用户输入的页。 若要运行和测试此验证代码，请执行此操作：

1. 创建新的网站使用包括 WebMatrix 2 站点模板之一*脚本*文件夹，如**入门站点**模板。
2. 在新的站点中，创建一个新 *.cshtml*页，然后将页面内容替换为下面的代码。
3. 在浏览器中运行页面。 输入有效和无效的值，以查看对验证的影响。 例如，将必填的字段留空，或输入的字母**信用额度**字段。


[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample7.cshtml)]

下面是页上，当用户提交有效输入：

[![topSeven-valid-1](top-features-in-web-pages-2/_static/image8.png)](top-features-in-web-pages-2/_static/image7.png)

当用户提交它与必填字段留空，下面是页：

[![topSeven-valid-2](top-features-in-web-pages-2/_static/image10.png)](top-features-in-web-pages-2/_static/image9.png)

下面是页上，当用户提交它与内的整数以外**信用额度**字段：

[![topSeven-valid-3](top-features-in-web-pages-2/_static/image12.png)](top-features-in-web-pages-2/_static/image11.png)

有关详细信息，请参阅以下博客文章：

- [更新网页 v2 中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2344)添加验证使用的基础知识`Validation`帮助器 （仅服务器端）
- [更新网页 v2，第 2 部分中的验证](http://www.mikepope.com/blog/DisplayBlog.aspx?permalink=2347)添加客户端验证。
- [更新网页 v2，第 3 部分中的验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2351)格式设置验证错误。

<a id="resmanagement"></a>
### <a name="registering-scripts-using-the-assets-manager"></a>注册脚本使用的资产管理器

资产管理器是可用于在服务器代码中注册并呈现客户端脚本的新功能。 如果你正在使用中 （如布局页、 内容页、 帮助器等） 在运行时合并成单个页面的多个文件的代码，此功能非常有用。 资产经理进行协调源代码文件，以确保正确引用脚本文件和有效地在呈现的页上，而不考虑哪些代码文件从调用的或者调用的次数。 资产管理器还会呈现`<script>`标记在适当的位置，以便快速 （而无需下载在呈现时的脚本） 可以加载此页面，以避免如果脚本调用在呈现之前可以发生的错误为完成。

例如，假设你创建的自定义帮助程序调用一个 JavaScript 文件，并在内容页代码在以下三个不同的位置上调用此帮助器。 如果你不使用的资产管理器注册中的帮助程序，三个不同的调用脚本`<script>`所有指向同一个脚本文件将都显示在你呈现的页面的标记。 另外，具体取决于 where`<script>`在呈现的页面中插入标记时，错误可能会发生如果脚本尝试以页完全加载之前访问某些页元素。 如果你使用的资产管理器注册脚本，则将避免这些问题。

你可以向的资产管理器注册脚本，通过执行此操作：

- 在代码中，需要引用该脚本，调用`Assets.AddScript`方法。
- 在 *\_SiteLayout*页上，调用`Assets.GetScripts`方法呈现`<script>`标记。 

    > [!NOTE]
    > 将调用`Assets.GetScripts`作为最后一项出现在`<body>`元素 *\_SiteLayout*页。 这有助于页面加载速度更快，并有助于避免脚本错误。

下面的示例显示的资产管理器的工作原理。 代码包含以下各项：

- 名为自定义 helper `MakeNote`。 此帮助器通过包装来呈现一个框内的字符串`div`元素在其周围的边框以及添加具有风格&quot;注意：&quot;到它。 帮助器还会调用将运行时行为添加到注释的 JavaScript 文件。 而不是引用的脚本`<script>`标记，帮助程序通过调用注册的脚本`Assets.AddScript`。
- 一个 JavaScript 文件。 这是调用的帮助程序，该文件，同时可注意项目期间的字体大小暂时增加`mouseover`事件。
- 内容页中，即在引用<em>\_SiteLayout</em>页上，呈现在正文中，某些内容，然后调用`MakeNote`帮助器。
- A  *\_SiteLayout*页。 此页会提供常见标头和页面布局结构。 它还包括调用`Assets.GetScripts`，即的资产管理器，如何呈现脚本调用在页中。

若要运行示例：

1. 创建空 Web Pages 2 网站。 可使用 WebMatrix**空网站**此模板。
2. 创建名为的文件夹*脚本*站点中。
3. 在*脚本*文件夹中，创建名为的文件*Test.js*，复制*Test.js*内容到该示例中，并保存该文件...
4. 创建名为的文件夹*应用\_代码*站点中。
5. 在*应用\_代码*文件夹中，创建名为的文件*Helpers.cshtml*、 执行它，请复制代码示例并将其保存在名为的文件夹中*应用\_代码*的根文件夹中。
6. 在站点的根文件夹中，创建名为的文件 *\_SiteLayout.cshtml，* 将本示例复制到其中，并保存该文件。
7. 在网站根下创建名为的文件*ContentPage.cshtml*、 添加示例代码中，并将其保存。
8. 运行*内容页*在浏览器。 传递给字符串`MakeNote`帮助器呈现为装箱的注意。
9. 将鼠标指针移注意。 该脚本暂时增大注意的字号。
10. 查看所呈现的页面的源。 由于其中放置到调用`Assets.GetScripts`，呈现`<script>`调用的标记*Test.js*是页面的正文中的最后一个项。

*Test.js*

[!code-javascript[Main](top-features-in-web-pages-2/samples/sample8.js)]

*Helpers.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample9.cshtml)]

*\_SiteLayout.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample10.html)]

*ContentPage.cshtml*

[!code-cshtml[Main](top-features-in-web-pages-2/samples/sample11.cshtml)]

以下屏幕快照显示*ContentPage.cshtml*在浏览器中时将鼠标指针拖过注意：

[![topSeven-resmgr-1](top-features-in-web-pages-2/_static/image14.png)](top-features-in-web-pages-2/_static/image13.png)

<a id="oauthsetup"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名

Web Pages 2 提供有关成员身份和身份验证的增强的选项。 主要增强功能就是新[OAuth](http://oauth.net/)和[OpenID](http://openid.net/)提供程序。 使用这些提供程序，你可以到你的站点使用 Facebook、 Twitter、 Windows Live、 Google 和 Yahoo 从其现有凭据让用户登录。 例如，若要使用 Facebook 帐户登录，用户可以只选择 Facebook 图标，将它们重定向到它们在其中输入他们的用户信息的 Facebook 登录页。 它们然后可以将 Facebook 登录名与你的站点上其帐户关联。 对网页成员资格功能的相关的增强与你的网站上的单个帐户是用户可以将多个登录名 （包括社交网络站点中的登录名） 相关联。

此图显示了从登录页**入门站点**模板，用户可以在其中选择一个 Facebook、 Twitter 或 Windows Live 图标，以允许使用外部帐户登录：

[![topSeven-oauth-1](top-features-in-web-pages-2/_static/image16.png)](top-features-in-web-pages-2/_static/image15.png)

你可以使用几行代码的 OAuth 和 OpenID 成员身份。 您使用的方法和属性才能使用 OAuth 和 OpenID 提供程序位于`WebMatrix.Security.OAuthWebSecurity`类。

但是，而不是使用代码来启用其他站点中的登录名，若要开始使用新的提供程序的建议的方法是使用新**入门站点**附带 WebMatrix 2 Beta 的模板。 **入门站点**模板包括完整的成员身份基础结构，登录页、 成员资格数据库，与所有的代码完成您需要允许用户登录到你使用本地凭据或来自另一个站点的站点.

#### <a name="how-to-enable-logins-using-the-oauth-and-openid-providers"></a>如何启用使用 OAuth 和 OpenID 提供程序的登录名

本部分举例说明如何让用户从外部网站 （Facebook、 Twitter、 Windows Live、 Google 或 Yahoo） 登录到站点基于**入门站点**模板。 创建一个入门站点之后, 你执行此 （详细信息按照）：

- 使用 OAuth 提供程序 （Facebook、 Twitter 和 Windows Live） 的站点，外部站点上创建应用程序。 这样，你将需要以调用这些站点的登录功能的应用程序密钥。 对于使用 OpenID 提供程序 （Google、 Yahoo） 的站点，不需要创建应用程序。 对于所有这些站点，必须具有一个帐户，以便在中记录并创建开发人员应用程序。 

    > [!NOTE]
    > Windows Live 应用程序只接受的实时工作网站，URL，因此不能用于本地网站 URL 测试登录名。
- 编辑你的网站中的几个文件，才能指定适当的身份验证提供程序和提交登录名添加到你想要使用的站点。

**若要启用 Google 和 Yahoo 登录**:

1. 在你的网站，编辑 *\_AppStart.cshtml*页上，在 Razor 代码块中的调用后添加以下两行代码`WebSecurity.InitializeDatabaseConnection`方法。 此代码使 Google 和 Yahoo OpenID 提供程序。 

    [!code-css[Main](top-features-in-web-pages-2/samples/sample12.css)]
2. 在 *~/Account/Login.cshtml*页上，从以下删除注释`<fieldset>`块的结尾处页面的标记。 若要取消注释的代码，删除`@*`前面或后面的字符`<fieldset>`块。 生成的代码块如下所示：

    [!code-html[Main](top-features-in-web-pages-2/samples/sample13.html)]
3. 添加`<input>`的 Google 或 Yahoo 提供程序的元素`<fieldset>`组中 *~/Account/Login.cshtml*页。 已更新`<fieldset>`组具有`<input>`如以下示例中为 Google 和 Yahoo 如下所示的元素： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample14.html)]
4. 在 *~/Account/AssociateServiceAccount.cshtml*页上，添加`<input>`Google 或 Yahoo 到元素`<fieldset>`组文件末尾附近。 你可以复制相同`<input>`刚添加到的元素`<fieldset>`主题中 *~/Account/Login.cshtml*页。 

    *~/Account/AssociateServiceAccount.cshtml*可以使用入门站点模板中的页，如果你想要创建在其的用户可以将其他站点中的多个登录名关联与你的网站上的单个帐户页。

现在，你可以测试 Google 和 Yahoo 登录名。

1. 运行*default.cshtml*您的网站上，选择**登录**按钮。
2. 上*登录*页上，在**使用另一个服务以要求在登录**部分中，选择以下两者之一**Google**或**Yahoo**提交按钮。 此示例使用 Google 登录名。 

    网页将请求重定向到 Google 登录页。

    [![topSeven-oauth-6](top-features-in-web-pages-2/_static/image18.png)](top-features-in-web-pages-2/_static/image17.png)
3. 输入现有的 Google 帐户凭据。
4. 如果出现要求你是否想要允许 Localhost 来使用帐户中的信息，请单击 Google**允许**。

    代码使用 Google 令牌进行身份验证用户，然后在网站上返回到此页。 可以使用此页将其 Google 登录名与你的网站上的现有帐户相关联的用户或用户可以在注册你将使用的外部登录名相关联的站点上的新帐户。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image20.png)](top-features-in-web-pages-2/_static/image19.png)
5. 选择**关联**按钮。 浏览器返回到应用程序的主页。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image22.png)](top-features-in-web-pages-2/_static/image21.png)

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image24.png)](top-features-in-web-pages-2/_static/image23.png)

**若要启用 Facebook 登录名**:

1. 转到[Facebook 开发人员站点](https://developers.facebook.com/apps)（如果尚未登录，则日志）。
2. 选择**创建新的应用程序**按钮，然后按照提示进行命名和创建新的应用程序。
3. 部分中**选择你的应用程序将如何集成到 Facebook**，选择**网站**部分。
4. 填写**站点 URL**字段替换你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。 **域**字段是可选的; 可以使用此提供对于整个域的身份验证 (如*example.com*)。 

    > [!NOTE]
    > 如果你正在使用 URL 你本地计算机上运行站点诸如`http://localhost:12345`（其中数是本地端口号），则可以添加到此值**站点 URL**字段用于测试你的站点。 但是，任何时候，只要你的本地站点更改的端口号，你将需要更新**站点 URL**你的应用程序的字段。
5. 选择**保存更改**按钮。
6. 选择**应用**再次，选项卡，然后查看你的应用程序的起始页。
7. 复制**应用程序 ID**和**应用程序密钥**你的应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Facebook 提供程序。
8. 退出 Facebook 开发人员网站。

现在你进行更改的两个页面中你的网站，以便用户将能够登录到使用其 Facebook 帐户的网站。

1. 在你的网站，编辑 *\_AppStart.cshtml*页上，取消注释的代码，为 Facebook OAuth 提供程序。 取消注释的代码块如下所示： 

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample15.xml)]
2. 复制**应用程序 ID**从 Facebook 应用程序的值作为值`consumerKey`（引号） 内的参数。
3. 复制**应用程序密钥**值从 Facebook 应用程序作为`consumerSecret`参数值。
4. 保存并关闭文件。
5. 编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。 若要取消注释的代码，删除`@*`前面或后面的字符`<fieldset>`块。 注释的代码块中删除类似于以下内容： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample16.html)]
6. 保存并关闭文件。

现在，你可以测试 Facebook 登录名。

1. 运行站点的*default.cshtml*页上，选择**登录**按钮。
2. 上*登录*页上，在**使用另一个服务以要求在登录**部分中，选择**Facebook**图标。 

    网页将请求重定向到 Facebook 登录页。

    [![topSeven-oauth-2](top-features-in-web-pages-2/_static/image26.png)](top-features-in-web-pages-2/_static/image25.png)
3. 登录到 Facebook 帐户。 

    代码使用 Facebook 令牌你进行身份验证，然后返回到页你可以在其中将 Facebook 登录名使用网站的登录名相关联。 你的用户名称或电子邮件地址填充到**电子邮件**窗体上字段。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image28.png)](top-features-in-web-pages-2/_static/image27.png)
4. 选择**关联**按钮。 

    浏览器返回到主页页面并登录。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image30.png)](top-features-in-web-pages-2/_static/image29.png)

**若要启用 Twitter 登录名：** 

1. 浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。
2. 选择**创建应用**链接，然后登录到网站。
3. 上**创建应用程序**窗体中，填写**名称**和**说明**字段。
4. 在**网站**字段中，输入你的站点的 URL (例如， [ `http://www.example.com` ](http://www.example.com))。 

    > [!NOTE]
    > 如果你正在测试你的本地站点 (使用如 URL `http://localhost:12345`)，Twitter 可能不接受该 URL。 但是，你可能能够使用本地环回 IP 地址 (例如`http://127.0.0.1:12345`)。 这可以简化测试本地应用程序的过程。 但是，每次你的本地网站的端口号更改，你将需要更新**网站**你的应用程序的字段。
5. 在**回调 URL**字段中，输入你希望用户在登录后到 Twitter 到返回的网站中的页的 URL。 例如，若要将用户发送到 （它将识别其登录的状态） 的入门站点主页上，输入中输入的相同 URL**网站**字段。
6. 接受条款，然后选择**创建 Twitter 应用程序**按钮。
7. 上**我的应用程序**登陆页，选择你创建的应用程序。
8. 上**详细信息**选项卡上，滚动到底部，选择**创建我访问令牌**按钮。
9. 上**详细信息**选项卡上，复制**使用者密钥**和**使用者机密**你的应用程序的值并将其粘贴到一个临时的文本文件。 网站代码中，会将这些值传递到 Twitter 提供程序。
10. 退出 Twitter 网站。

现在你进行更改的两个页面中你的网站，以便用户能够登录到使用其 Twitter 帐户的网站。

1. 在你的网站，编辑 *\_AppStart.cshtml*页上，取消注释的代码，Twitter OAuth 提供程序。 取消注释的代码块如下所示： 

    [!code-csharp[Main](top-features-in-web-pages-2/samples/sample17.cs)]
2. 复制**使用者密钥**值形式的值的 Twitter 应用程序从`consumerKey`（引号） 内的参数。
3. 复制**使用者机密**值形式的值的 Twitter 应用程序从`consumerSecret`参数。
4. 保存并关闭文件。
5. 编辑 *~/Account/Login.cshtml*页上，删除从注释`<fieldset>`页末尾附近的块。 若要取消注释的代码，删除`@*`前面或后面的字符`<fieldset>`块。 注释的代码块中删除类似于以下内容： 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample18.html)]
6. 保存并关闭文件。

现在，你可以测试 Twitter 登录。

1. 运行*default.cshtml*您的网站上，选择**登录**按钮。
2. 上*登录*页上，在**使用另一个服务以要求在登录**部分中，选择**Twitter**图标。 

    网页将请求重定向到 Twitter 登录页为您创建的应用程序中。

    [![topSeven-oauth-4](top-features-in-web-pages-2/_static/image32.png)](top-features-in-web-pages-2/_static/image31.png)
3. 登录到 Twitter 帐户。
4. 该代码使用 Twitter 令牌来验证用户身份，然后返回到页你可以将关联您的登录名与你网站的帐户。 您的名称或电子邮件地址填充到**电子邮件**窗体上字段。

    [![topSeven-oauth-5](top-features-in-web-pages-2/_static/image34.png)](top-features-in-web-pages-2/_static/image33.png)
5. 选择**关联**按钮。 

    浏览器返回到主页页面并登录。

    [![topSeven-oauth-3](top-features-in-web-pages-2/_static/image36.png)](top-features-in-web-pages-2/_static/image35.png)

<a id="maphelper"></a>
### <a name="adding-maps-using-the-maps-helper"></a>添加使用地图帮助程序图

Web Pages 2 包括添加到 ASP.NET Web 帮助程序库，后者是网页站点的加载项包。 其中一种是由提供的映射组件`Microsoft.Web.Helpers.Maps`类。 你可以使用`Maps`类以生成基于地址或一组的经度和纬度坐标的地图。 `Maps`类，可以直接在包括必应、 Google、 MapQuest 和 Yahoo 常用映射引擎调用。

若要使用新`Maps`类在你的网站，你必须首先安装 Web 帮助程序库的版本 2。 若要执行此操作，请转到安装的当前发行的版的说明[ASP.NET Web 帮助程序库](https://go.microsoft.com/fwlink/?LinkId=202889#webhelpers)并安装版本 2。

将映射添加到页的步骤都相同的调用而与所映射引擎。 只需添加对您的映射页面的 JavaScript 文件引用并将呈现的调用`<script>`在你的页面上标记。 然后在映射页面中上, 调用你想要使用映射引擎。

下面的示例演示如何创建将基于一个地址，结构图呈现一个页，并且将基于经度和纬度坐标结构图呈现的另一页。 地址映射示例使用 Google 地图和坐标映射示例使用必应地图。 请注意在代码中的以下元素：

- 调用`Assets.AddScript`顶部的两个映射页。 此方法将引用添加到*jquery 1.6.2.min.js*附带的文件**入门站点**模板和所需`Maps`类。
- 调用`Assets.GetScripts`布局文件中的方法。 此方法呈现`<script>`的两个映射页面的标记。
- 调用`@Maps.GetGoogleHtml`和`@Maps.GetBingHtml`中的映射页的方法。 若要将地址映射，你必须传递地址字符串。 若要映射坐标时，必须传递经度和纬度坐标。 对于 Bing 地图引擎中，你还必须传递一个密钥 (可通过在注册获取免费[必应地图开发人员站点](https://www.microsoft.com/maps/developers/web.aspx))。 对于其他映射引擎方法的工作原理类似的方式 (`@Maps.GetYahooHtml`， `@Maps.GetMapQuestHtml`)。

若要创建映射页：

1. 创建基于网站**入门站点**模板。
2. 创建名为的文件*MapAddress.cshtml*站点的根目录中。 此页将生成基于传递给它的地址映射。
3. 将以下代码复制到文件中，覆盖现有的内容。 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample19.cshtml)]
4. 创建名为的文件 *\_MapLayout.cshtml*站点的根目录中。 此页将两个映射页的布局页。
5. 将以下代码复制到文件中，覆盖现有的内容。 

    [!code-html[Main](top-features-in-web-pages-2/samples/sample20.html)]
6. 创建名为的文件*MapCoordinates.cshtml*站点的根目录中。 此页将生成基于一组坐标传递给它的映射。
7. 将以下代码复制到文件中，覆盖现有的内容。 

    [!code-cshtml[Main](top-features-in-web-pages-2/samples/sample21.cshtml)]

若要测试映射页面：

1. 运行页面*MapAddress.cshtml*文件。
2. 输入包括街道地址、 状态或自治区和邮政编码的完整地址字符串，然后选择**Map It**按钮。 呈现地图页面，从 Google 地图： 

    [![topseven-maphelper-1](top-features-in-web-pages-2/_static/image38.png)](top-features-in-web-pages-2/_static/image37.png)
3. 查找的特定位置的纬度和经度坐标集。
4. 运行页面*MapCoordinates.cshtml*。 输入坐标，然后选择**Map It**按钮。 将呈现的地图页面从 Bing 地图： 

    [![topseven-maphelper-2](top-features-in-web-pages-2/_static/image40.png)](top-features-in-web-pages-2/_static/image39.png)

<a id="sidebyside"></a>
### <a name="running-web-pages-applications-side-by-side"></a>运行 Web 页面应用程序并行

Web Pages 2 添加了运行并行应用程序的功能。 这使你能够继续用于运行 Web Pages 1 应用程序、 生成新的 Web Pages 2 应用程序，和在同一台计算机上运行所有这些。

下面是在使用 WebMatrix 安装 Web Pages 2 Beta 时要记住一些事项：

- 默认情况下，现有的 Web 页面应用程序将在你的计算机上运行为版本 2 的应用程序。 （版本 2 的程序集安装到 GAC 中并且将自动使用。）
- 如果你想要运行使用网页版本 1 （而不是默认值，如下所示的以前的点） 的站点，你可以配置站点以执行该操作。 如果你的站点还没有*web.config*文件在站点的根目录中，创建一个新然后将以下 XML 复制到其中，覆盖现有的内容。 如果该站点已包含*web.config*文件中，添加`<appSettings>`到以下所示的元素`<configuration>`部分。

    [!code-xml[Main](top-features-in-web-pages-2/samples/sample22.xml)]
  -如果不指定中的版本*web.config*文件，站点部署为版本 2 站点。 (版本 2 程序集复制到*bin*已部署的站点中的文件夹。)
- Web Matrix 2 Beta 包括在站点中的网页版本 2 程序集的版本中使用的站点模板创建的新应用程序*bin*文件夹。

一般情况下，你可以始终控制哪个版本的 Web 页面以通过使用 NuGet 将相应的程序集安装到站点的使用与您的网站*bin*文件夹。 若要查找程序包，请访问[NuGet.org](http://NuGet.org)。

<a id="mobile"></a>
### <a name="rendering-pages-for-mobile-devices"></a>为移动设备中呈现页

Web Pages 2 中，可以在移动或其他设备上创建自定义呈现内容的显示。

`System.Web.WebPages`命名空间包含允许您使用的显示模式的以下类： `DefaultDisplayMode`， `DisplayInfo`，和`DisplayModes`。 你可以直接使用这些类，并且可以编写呈现特定设备的正确输出的代码。

或者，你可以创建使用如下的文件命名模式的特定于设备的页面： <em>FileName。</em><em>移动</em><em>.cshtml</em>。 例如，可以创建两个版本的页上，一个名为<em>MyFile.cshtml</em>和一个名为<em>MyFile.Mobile.cshtml</em>。 在运行的时，当移动设备请求<em>MyFile.cshtml</em>，网页将从内容呈现<em>MyFile.Mobile.cshtml</em>。 否则为<em>MyFile.cshtml</em>呈现。

下面的示例演示如何通过添加移动设备的内容页中启用移动呈现。 *Page1.cshtml*包含内容以及导航侧边栏。 *Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。

若要生成并运行的代码示例：

1. 在网页网站中，创建名为的文件*Page1.cshtml*和复制*Page1.cshtml*内容到该示例中。
2. 创建名为的文件*Page1.Mobile.cshtml*和复制*Page1.Mobile.cshtml*内容到该示例中。 请注意该页面的移动版本省略更好地呈现较小屏幕上的导航部分。
3. 运行桌面浏览器并浏览到*Page1.cshtml*。
4. 运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。 请注意这一次 Web 页呈现页面的移动版本。 

    > [!NOTE]
    > 若要测试移动页，可以使用在台式计算机运行的移动设备模拟器。 此工具允许你测试 web 页面，因为它们将显示在移动设备上 （即，通常通过小得多显示区域）。 模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/en-us/firefox/addon/user-agent-switcher/)对 Mozilla Firefox，它可让你模拟从桌面版本的 Firefox 的各种移动浏览器。

*Page1.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample23.html)]

*Page1.Mobile.cshtml*

[!code-html[Main](top-features-in-web-pages-2/samples/sample24.html)]

*Page1.cshtml*在桌面浏览器中呈现：

[![topseven-displaymodes-1](top-features-in-web-pages-2/_static/image42.png)](top-features-in-web-pages-2/_static/image41.png)

*Page1.Mobile.cshtml* Firefox 浏览器中的 Apple iPhone 模拟器视图中显示。 即使该请求是*Page1.cshtml*，应用程序呈现*Page1.Mobile.cshtml*。

[![topseven-displaymodes-2](top-features-in-web-pages-2/_static/image44.png)](top-features-in-web-pages-2/_static/image43.png)

<a id="resources"></a>
## <a name="additional-resources"></a>其他资源

### <a name="aspnet-web-pages-1-resources"></a>ASP.NET Web Pages 1 资源

> [!NOTE]
> 大多数 Web Pages 1 编程和 API 资源仍适用于 Web Pages 2。

- [ASP.NET Web Pages 编程简介](https://go.microsoft.com/fwlink/?LinkId=202890)

### <a name="webmatrix-resources"></a>WebMatrix 资源

- [WebMatrix 2 新增功能](http://webmatrix.com/next)
- [Microsoft WebMatrix Site](https://go.microsoft.com/fwlink/?LinkID=195076)
- [开始使用 Microsoft WebMatrix 的 Web 开发](https://msdn.microsoft.com/en-us/library/hh145669(v=VS.99).aspx)（包括一个完整的示例 Web 页面应用程序）
