---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 本文档介绍 ASP.NET MVC 4 的发布。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: a4f78061850ef5ad8c3381daafdb5ea6bca4cb2f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830219"
---
<a name="aspnet-mvc-4"></a>ASP.NET MVC 4
====================
> 本文档介绍 ASP.NET MVC 4 的发布。


- [安装说明](#_Toc303253802)
- [文档](#_Toc303253803)
- [支持](#_Toc303253804)
- [软件要求](#_Toc303253805)
- [在 ASP.NET MVC 4 中的新增功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [默认项目模板的增强功能](#_Toc303253808)
    - [移动项目模板](#_Toc303253809)
    - [显示模式](#_Toc303253810)
    - [jQuery Mobile，视图切换器和浏览器重写](#_Toc303253811)
    - [任务支持异步控制器](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [数据库迁移](#_Toc303253818)
    - [空项目模板](#_Toc303253819)
    - [将控制器添加到任何项目文件夹](#_Toc303253820)
    - [捆绑和缩小](#_Toc303253821)
    - [启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名](#_Toc303253822)
- [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 的候选发布版本中的更改](#_Toc303253817)
- [已知的问题和重大更改](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安装说明

可以从安装适用于 Visual Studio 2010 的 ASP.NET MVC 4 [ASP.NET MVC 4 主页](../mvc/mvc4.md)使用 Web 平台安装程序。

我们建议卸载任何以前安装在安装 ASP.NET MVC 4 之前的 ASP.NET MVC 4 的预览。 可以无需卸载的 ASP.NET MVC 4 Beta 和候选发布版本升级到 ASP.NET MVC 4。

此版本中不与任何.NET Framework 4.5 的预览版本兼容。 到在安装 ASP.NET MVC 4 之前的最终版本，必须单独升级.NET Framework 4.5 的任何已安装的预览版本。

ASP.NET MVC 4 可以是安装和运行的并行使用 ASP.NET MVC 3。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文档

ASP.NET MVC 的文档位于以下 URL 的 MSDN 网站上有：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

教程和其他信息 ASP.NET MVC 是 ASP.NET 网站的 MVC 4 页上提供 ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md))。

<a id="_Toc303253804"></a>
## <a name="support"></a>支持

ASP.NET MVC 4 完全支持。 如果您有关于使用此版本的问题您还可以发布它们在 ASP.NET MVC 论坛 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))，ASP.NET 社区的成员是经常能够提供非正式的支持。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>软件要求

Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 以及 Service Pack 1 的 Visual Studio 2010 或 Visual Web Developer 学习版 2010 Service Pack 1。

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>在 ASP.NET MVC 4 中的新增功能

本部分介绍已引入的功能在 ASP.NET MVC 4 版本。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 包含 ASP.NET Web API，用于创建可以访问范围广泛的客户端包括浏览器和移动设备的 HTTP 服务的新框架。 ASP.NET Web API 也是用于构建 RESTful 服务的理想平台。

ASP.NET Web API 包括以下功能的支持：

- **现代 HTTP 编程模型：** 直接访问和处理 HTTP 请求和响应 Web Api 使用新的、 强类型化的 HTTP 对象模型中。 相同编程模型和 HTTP 管道是对称的新客户端上可用*HttpClient*类型。
- **完全支持路由：** ASP.NET Web API 支持 ASP.NET 路由，包括路由参数和约束的路由功能的完整集。 此外，使用简单约定操作映射到 HTTP 方法。
- **内容协商：** 客户端和服务器可以协同工作来确定从 web API 返回的数据的正确格式。 ASP.NET Web API 提供了对 XML、 JSON 的默认支持和窗体 URL 编码格式和您可以通过添加自己的格式化程序来扩展此支持或甚至替换默认内容协商策略。
- **模型绑定和验证：** 模型联编程序提供了简便的方法来从各个组成部分的 HTTP 请求中提取数据并将这些消息部分转换成可由 Web API 操作的.NET 对象。 对基于数据批注操作参数还执行验证。
- **筛选器：** ASP.NET Web API 支持筛选器包括的已知的筛选器，如 *[Authorize]* 属性。 可以编写并插入自己的筛选器操作、 授权和异常处理。
- **在查询撰写：** 使用 *[Queryable]* 返回的操作筛选器特性*IQueryable*以启用查询 web API 通过 OData 查询约定的支持。
- **改进了可测试性：** 而不是静态上下文对象中设置 HTTP 详细信息，web API 操作工作的实例，并用*HttpRequestMessage*并*HttpResponseMessage*。 创建单元测试项目以及 Web API 项目若要开始快速编写针对您的 Web API 功能的单元测试。
- **基于代码的配置：** 只有通过代码实现 ASP.NET Web API 配置、 离开 config 文件清理。 使用提供的服务定位器模式配置的扩展点。
- **改进了对控制反转 (IoC) 容器的支持：** ASP.NET Web API 以通过改善了依赖关系解析程序抽象的 IoC 容器提供强大支持
- **自承载：** Web Api 可以同时仍可使用的路由的所有功能和其他功能的 Web API 托管在自己的进程除 IIS 之外。
- **创建自定义帮助和测试页：** 你现在可以轻松构建自定义帮助和使用新的 web Api 测试页面*IApiExplorer*服务以获取你的 web Api 的完整的运行时说明。
- **监视和诊断：** ASP.NET Web API 现在提供轻量跟踪基础结构，它可以更轻松地与现有的日志记录解决方案，如 System.Diagnostics、 ETW 和第三方日志记录框架集成。 可以启用跟踪，从而*ITraceWriter*实现并将其添加到你的 web API 配置。
- **链接生成：** 使用 ASP.NET Web API *UrlHelper*生成在同一应用程序的相关资源的链接。
- **Web API 项目模板：** 选择新 Web API 项目窗体以快速了解 ASP.NET Web API 启动并运行新的 MVC 4 项目向导。
- **基架：** 使用**添加控制器**对话框，可以快速创建基于实体框架的 web API 控制器基架基于的模型类型。

有关在 ASP.NET Web API 的更多详细信息，请访问[ https://www.asp.net/web-api ](../web-api/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>默认项目模板的增强功能

已更新用于创建新的 ASP.NET MVC 4 项目模板来创建外观更加现代的网站：

![](mvc4-release-notes/_static/image1.png)

除了修饰性的改进，已改进的新模板中的功能。 该模板采用一种名为自适应呈现妙在桌面浏览器和移动浏览器没有任何自定义项中。

![](mvc4-release-notes/_static/image2.png)

若要查看操作中的自适应呈现，可以使用移动仿真程序，或只是尝试调整大小较小的桌面浏览器窗口。 如果浏览器窗口中获取足够小，将更改页的布局。

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>移动项目模板

如果要开始一个新项目并想要创建一个网站，专门用于移动和平板电脑浏览器，可以使用新的移动应用程序项目模板。 这基于 jQuery Mobile 的用于构建触控优化的 UI 的开放源代码库：

![](mvc4-release-notes/_static/image3.png)

此模板包含为 Internet 应用程序模板相同的应用程序结构 （和控制器代码是几乎完全相同），但它是样式使用 jQuery Mobile 外观精美，同时也在基于触控的移动设备上的行为。 若要了解有关如何结构化和样式移动 UI 的详细信息，请参阅[jQuery 移动项目网站](http://jquerymobile.com/)。

如果已有面向桌面的站点，你想要添加到，移动优化的视图，或如果想要创建一个站点，提供对桌面和移动浏览器以不同的方式应用了样式的视图，可以使用新的显示模式功能。 （请参阅下一节。）

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>显示模式

新的显示模式功能，可以选择根据发出请求的浏览器视图的应用程序。 例如，如果桌面浏览器主页发送请求，应用程序可能使用 Views\Home\Index.cshtml 模板。 如果在移动浏览器主页发送请求，应用程序可能会返回 Views\Home\Index.mobile.cshtml 模板。

布局和部分也可以为特定浏览器类型重写。 例如：

- 如果你的 views/shared 文件夹包含两\_Layout.cshtml 和\_Layout.mobile.cshtml 模板，默认情况下应用程序将使用\_Layout.mobile.cshtml 期间请求从移动浏览器和\_Layout.cshtml 期间其他请求。
- 如果文件夹包含两\_MyPartial.cshtml 并\_MyPartial.mobile.cshtml，指令@Html.Partial("\_MyPartial") 将呈现\_MyPartial.mobile.cshtml 期间从移动设备的请求浏览器和\_MyPartial.cshtml 期间其他请求。

如果你想要创建更具体的视图、 布局或其他设备的分部视图，则可以注册一个新*为 DefaultDisplayMode*实例可以指定其名称以使其搜索请求满足特定条件。 例如，可以添加以下代码*应用程序\_启动*要将字符串"iPhone"注册为 Apple iPhone 浏览器发出请求时应用的显示模式的 Global.asax 文件中的方法：

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

此代码运行，当 Apple iPhone 浏览器发出请求后，你的应用程序将使用 views/shared\\_Layout.iPhone.cshtml 布局 （如果存在）。 显示模式的详细信息，请参阅[ASP.NET MVC 4 移动功能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)。 应安装应用程序使用 DisplayModeProvider[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 包。 [ASP.NET Fall 2012 Update](https://go.microsoft.com/fwlink/?LinkID=271322)包括[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes)新项目模板中的 NuGet 包。 请参阅[ASP.NET 的 MVC 已由 4 移动缓存的 Bug Fixedd](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)有关解决方法的详细信息。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>jQuery Mobile 和 Mobile 功能

有关构建 ASP.NET MVC 4 移动应用程序使用 jQuery Mobile，请参阅本教程[ASP.NET MVC 4 移动功能](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md)。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>任务支持异步控制器

您现在可以编写异步操作方法的返回类型的对象为 single 方法*任务*或*任务&lt;ActionResult&gt;*。

 有关详细信息请参阅[ASP.NET MVC 4 中使用异步方法](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 支持 Windows Azure SDK 1.6 和较新的版本。

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>数据库迁移

ASP.NET MVC 4 项目现在包括 Entity Framework 5。 Entity Framework 5 中强大的功能之一是对数据库迁移的支持。 此功能，可轻松改进您使用专注于代码的同时保留数据库中的数据迁移的数据库架构。 数据库迁移的详细信息，请参阅[将新字段添加到电影模型和表](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md)中[introduction to ASP.NET MVC 4 教程简介](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>空项目模板

空 MVC 项目模板现在是真正的空的以便您可以从完全干净状态启动。 空项目模板的早期版本已更名为基本。

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>将控制器添加到任何项目文件夹

现在可以右键单击，然后选择**添加控制器**在 MVC 项目中的任意文件夹中。 这为您提供了更灵活地组织你的控制器，但你想，包括将 MVC 和 Web API 控制器保存在单独的文件夹。

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>捆绑和缩小

捆绑和缩小框架，从而减少必须将 Web 页以便通过将单个文件组合成一个单一的脚本和 CSS 捆绑文件的 HTTP 请求数。 然后它可以减少这些请求的总体大小缩小绑定的内容。 缩小可包含例如消除空格缩短到甚至折叠 CSS 选择器基于它们的语义的变量名称的活动。 绑定声明中并配置代码是轻松地引用和通过帮助程序方法可以生成任何一个视图中的单个链接到该绑定，或在调试时，多个链接到单个绑定的内容。 有关详细信息请参阅[捆绑和缩减](../mvc/overview/performance/bundling-and-minification.md)。

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名

在 ASP.NET MVC 4 Internet 项目模板中的默认模板现在包括对使用由 DotNetOpenAuth 库的 OAuth 和 OpenID 登录的支持。 配置 OAuth 或 OpenID 提供程序的信息，请参阅[OAuth/OpenID 支持 WebForms、 MVC 和网页](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx)并[OAuth 和 OpenID 功能文档在 ASP.NET Web Pages](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup)。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4

ASP.NET MVC 4 可以与 ASP.NET MVC 3 并行安装使您灵活地选择何时升级到 ASP.NET MVC 4 的 ASP.NET MVC 3 应用程序在同一计算机上。

若要升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目并复制所有视图、 控制器、 代码和内容都文件从现有的 MVC 3 项目到新项目，然后更新程序集引用中要匹配任何非 MVC 模板中的新项目获取组件保存正在使用。 如果到 MVC 3 项目中的 Web.config 文件进行了更改，必须还将这些更改合并到 MVC 4 项目中的 Web.config 文件中。

若要手动升级到版本 4 现有的 ASP.NET MVC 3 应用程序，请执行以下操作：

1. 在所有 Web.config 文件在项目中 （还有一个项目，一个视图文件夹中，一个在你的项目中每个区域的 Views 文件夹的根目录中），将为以下文本的每个实例 (请注意： System.Web.WebPages，版本 = 中找不到 1.0.0.0项目使用 Visual Studio 2012 创建的）： 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    使用以下相应的文本：

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. 在根 Web.config 文件中，更新*webPages:Version*为"2.0.0.0"的元素，并添加新*PreserveLoginUrl*具有值"true"的密钥： 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. 在解决方案资源管理器，右键单击引用并选择管理 NuGet 包。 在左窗格中，选择**Online\NuGet 官方程序包源代码**，然后更新以下：

    - ASP.NET MVC 4
    - （可选） jQuery、 jQuery 验证和 jQuery UI
    - （可选）实体框架
    - (Optonal)Modernizr
4. 在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。 再次右键单击名称，然后选择编辑*ProjectName*.csproj。
5. 找到*ProjectTypeGuids*元素，并替换 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 保存所做的更改，关闭您所编辑的项目 (.csproj) 文件，右键单击该项目，然后选择重新加载项目。
7. 如果项目引用任何使用 ASP.NET MVC 的以前版本编译的第三方库，打开根 Web.config 文件并添加以下三种*bindingRedirect*下的元素*配置*部分： 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>ASP.NET MVC 4 的候选发布版本中的更改

ASP.NET MVC 4 Release Candidate 的发行说明可在此处找到：

下面总结了从 ASP.NET MVC 4 发布候选版本此版本中的重大更改：

- **每个控制器配置：** ASP.NET Web API 控制器可以与实现的自定义属性归*IControllerConfiguration*设置其自己的格式化程序、 操作选择器和参数绑定器. *HttpControllerConfigurationAttribute*已删除。
- **每个路由消息处理程序：** 你现在可以指定给定路由的请求链中的最后一条消息处理程序。 这使对持续一段时间沿框架路由以使用发送到其自身的支持 (非*IHttpController*) 终结点。
- **进度通知：** *ProgressMessageHandler*生成进度通知的请求实体正在上传和下载的响应实体。 使用此处理程序很可能延伸的范围是上传请求正文还是正在下载响应正文跟踪的。
- **将内容推送：** *PushStreamContent*类启用了数据生产者希望直接写入请求或响应 （同步或异步） 使用一个流的方案。 当*PushStreamContent*已准备好接受它调用一个操作委托，它与输出流的数据。 为长达必要和关闭时写入的流已完成，开发人员然后可以写入到流。 *PushStreamContent*检测到的流的结尾，并完成基础异步*任务*用于写出内容。
- **创建错误响应：** 使用*HttpError*类型来一致地表示错误中的信息，例如验证错误和异常同时仍然允许*IncludeErrorDetailPolicy*. 使用新*CreateErrorResponse*扩展方法，可以轻松地创建错误的响应*HttpError*作为内容。 *HttpError*内容是完全内容协商。
- **删除 MediaRangeMapping:** 媒体类型范围现在由默认内容协商者。
- **现在是简单类型参数的默认参数绑定 [FromUri]:** 在以前版本的 ASP.NET Web API 的默认参数绑定使用模型绑定的简单类型参数。 简单类型参数的默认参数绑定现 *[FromUri]*。
- **操作选择遵循必需的参数：** ASP.NET Web API 中的操作选择现在将仅选择一个操作如果提供了所有必需的参数来自 URI 的。 参数可以通过提供操作方法签名中参数的默认值指定为可选。
- **自定义 HTTP 参数绑定：** 使用*ParameterBindingAttribute*自定义特定的操作参数的参数绑定或使用*ParameterBindingRules*上*HttpConfiguration*可以自定义参数绑定更加广泛。
- **MediaTypeFormatter 改进：** 格式化程序现在有权访问完整*HttpContent*实例。
- **缓冲策略选择的主机：** 实现和配置*IHostBufferPolicySelector*服务在 ASP.NET Web API 以启用主机以确定当缓冲时要使用的策略。
- **以主机不可知的方式访问客户端证书：** 使用*GetClientCertificate*扩展方法，以将请求消息中获取所提供的客户端证书。
- **内容协商可扩展性：** 通过从派生自定义内容协商*为 DefaultContentNegotiator*和重写内容协商想要的任何方面。
- **针对返回 406 不可接受的响应的支持：** 你现在可以返回 406 不可接受的响应在 ASP.NET Web API 中通过创建找不到合适的格式化程序时*为 DefaultContentNegotiator* 与*excludeMatchOnTypeOnly*参数设置为 *，则返回 true*。
- **作为 NameValueCollection 或 JToken 读取窗体数据：** 可以读取窗体数据 URI 查询字符串中或在请求正文中作为*NameValueCollection*使用*ParseQueryString*并*ReadAsFormDataAsync*扩展方法分别。 同样，您可以读取窗体数据 URI 查询字符串中或在请求正文中作为*JToken*使用*TryReadQueryAsJson*并*ReadAsAsync*&lt;T&gt;扩展方法分别。
- **多部分改进：** 现可以编写*MultipartStreamProvider*完全针对 MIME 多部分数据，它可以读取并以最佳方式向用户显示结果的类型。 您还可以挂接后续处理步骤上*MultipartStreamProvider*允许实现来完成任何后期处理它要将 MIME 多部分正文部分上的。 例如， *MultipartFormDataStreamProvider*实现读取 HTML 窗体数据部分，并将它们添加到*NameValueCollection*以便它们可以轻松从调用方处获取。
- **链接生成改进：** *UrlHelper*不再依赖*HttpControllerContext*。 现在可以访问*UrlHelper*从任何上下文位置*HttpRequestMessage*可用。
- **消息处理程序执行顺序更改：** 现在它们按相反的顺序配置而不是顺序执行消息处理程序。
- **消息处理程序绑定的帮助器：** 的新*HttpClientFactory* ，可以绑定*DelegatingHandlers*并创建*HttpClient*与所需的管道准备就绪。 它还提供有关使用备用的内部处理程序绑定的功能 (默认值是*HttpClientHandler*) 以及使用时，执行连接*HttpMessageInvoker*或另一个*DelegatingHandler*而不是*HttpClient*作为前调用程序。
- **支持 ASP.NET Web 优化的 Cdn:** ASP.NET Web 优化的 CDN 备用路径，使您可以指定每个捆绑附加 URL 指向该资源的内容交付网络上现在提供支持。 支持 Cdn，可获取脚本和样式绑定地理位置更靠近最终使用者的 Web 应用程序。 当 CDN 不可用时，生产应用应实现回退。 测试回退。
- **ASP.NET Web API 路由，并配置移动到*WebApiConfig.Register*可以是 resused 测试代码中的静态方法。** ASP.NET Web API 路由之前已在中添加*RouteConfig.RegisterRoutes*以及标准的 MVC 路由。 在单独现在处理的 ASP.NET Web API 路由的默认值和配置*WebApiConfig.Register*方法以便进行测试。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

- **ASP.NET MVC 4 的 RC 和 RTM 版本不正确返回缓存的桌面视图时应返回移动视图。**

    - 请参阅[ASP.NET MVC 4 移动缓存 Bug 固定](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)有关解决方法的详细信息。 可以从安装该修补程序[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) NuGet 包。
- **Razor 视图引擎中的重大更改**。 以下类型已从*System.Web.Mvc.Razor*: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  此外已删除以下方法： 

    - *MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
    - *MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*
    - *MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
- **WebMatrix.WebData.dll 包含在 ASP.NET MVC 4 应用程序的 /bin 目录中，它将接管窗体身份验证的 URL。** （例如，通过使用添加部署依赖性对话框中时，请选择"ASP.NET Web Pages with Razor 语法"） 将 WebMatrix.WebData.dll 程序集添加到你的应用程序将覆盖为登录/帐户 / 身份验证登录重定向而非 /帐户/登录按预期方式默认 ASP.NET MVC 帐户控制器情况。 若要防止此行为，并使用 web.config 的身份验证部分中已指定的 URL，可以添加名为 PreserveLoginUrl 的 appSetting，并将其设置为 true: 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **NuGet 包管理器失败时尝试安装 ASP.NET MVC 4 的并行安装 Visual Studio 2010 和 Visual Web Developer 2010 的安装。** 若要运行 Visual Studio 2010 和 Visual Web Developer 2010 与 ASP.NET MVC 4 并行必须已安装了这两个版本的 Visual Studio 后安装 ASP.NET MVC 4。
- **如果已卸载系统必备组件卸载 ASP.NET MVC 4 将失败。** 若要完全卸载 ASP.NET MVC 4you 必须在卸载 Visual Studio 之前卸载 ASP.NET MVC 4。
- **安装 ASP.NET MVC 4 分页符 ASP.NET MVC 3 RTM 应用程序。** ASP.NET MVC 3 创建的应用程序与 RTM 版本 (不能与[ASP.NET MVC 3 Tools Update](https://www.microsoft.com/download/details.aspx?id=1491)发布) 需要执行以下更改才能使用 ASP.NET MVC 4 并行。 生成项目而无需进行这些更新结果中的编译错误。 

    **所需的更新**

  1. 在根 Web.config 文件中，添加一个新*&lt;appSettings&gt;* 具有键的项*webPages:Version*和值*1.0.0.0*。 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. 在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。 再次右键单击名称，然后选择编辑*ProjectName*.csproj。
  3. 找到以下程序集引用： 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      使用以下内容替换它们：

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. 保存所做的更改，关闭了编辑，然后右键单击项目并选择重新加载项目 (.csproj) 文件。

- **从 4.5 将 ASP.NET MVC 4 项目更改为目标 4.0 不会更新 EntityFramework 程序集引用：** 如果您的 ASP.NET MVC 4 项目后更改为目标 4.0 针对 4.5 EntityFramework 程序集的引用将仍指向4.5 版本。 若要解决此问题卸载并重新安装 EntityFramework NuGet 包。
- **从 4.5 更改为目标 4.0 后，Azure 上运行的 ASP.NET MVC 4 应用程序时的 403 禁止访问：** 如果针对 4.5 之后，ASP.NET MVC 4 项目更改为目标 4.0，然后部署到 Azure 可能会看到 403 禁止访问错误在运行时。 解决此问题添加到 web.config 以下项： `<modules runAllManagedModulesForAllRequests="true" />`
- **当你键入时，visual Studio 2012 崩溃\'字符串文本中的 Razor 文件中。** 要解决此问题第一次输入字符串文本的右引号。
- <strong>浏览到&quot;帐户/管理&quot;Internet 模板结果中 CHS、 TRK 和 CHT 语言运行时错误。</strong> 若要解决此问题修改页后，可以分离出来<em>@User.Identity.Name</em>将其放作为中的唯一内容<em>&lt;强&gt;</em>标记。
- **Google 和 LinkedIn 提供程序不支持 Azure 网站中。** 部署到 Azure 网站时，请使用备用身份验证提供程序。
- **当使用 UriPathExtensionMapping 与 IIS 8 Express/IIS，您将收到 404 找不到错误，当您尝试使用该扩展。** 静态文件处理程序会干扰对 web Api 使用的请求*UriPathExtensionMappings*。 设置*runAllManagedModulesForAllRequests = true*中 web.config 以解决此问题。
- **不能再调用 Controller.Execute 方法。** 现在始终以异步方式执行所有 MVC 控制器。
