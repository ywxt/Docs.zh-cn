---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 本文档介绍 ASP.NET MVC 4 Beta for Visual Studio 2010 的版本。
ms.author: aspnetcontent
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: b9d50114a239b67b1adc263f6ea6d3a811bcc8f7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816686"
---
<a name="aspnet-mvc-4"></a>ASP.NET MVC 4
====================
> 本文档介绍 ASP.NET MVC 4 Beta for Visual Studio 2010 的版本。
> 
> > [!NOTE]
> > 这不是最新版本。 提供了 ASP.NET MVC 4 RC 发行说明[此处](mvc4-release-notes.md)。


- [安装说明](#_Toc303253802)
- [文档](#_Toc303253803)
- [支持](#_Toc303253804)
- [软件要求](#_Toc303253805)
- [将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4](#_Toc303253806)
- [ASP.NET MVC 4 Beta 中的新增功能](#_Toc303253807)

    - [ASP.NET Web API](#_Toc317096197)
    - [ASP.NET 单页面应用程序](#_Toc317096198)
    - [默认项目模板的增强功能](#_Toc303253808)
    - [移动项目模板](#_Toc303253809)
    - [显示模式](#_Toc303253810)
    - [jQuery Mobile，视图切换器和浏览器重写](#_Toc303253811)
    - [用于 Visual Studio 中的代码生成方案](#_Toc303253812)
    - [任务支持异步控制器](#_Toc303253813)
    - [Azure SDK](#_Toc303253814)
    - [已知的问题和重大更改](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>安装说明

可以从安装的 Visual Studio 2010 的 ASP.NET MVC 4 Beta [ASP.NET MVC 4 主页](../mvc/mvc4.md)使用 Web 平台安装程序。

必须先卸载任何以前安装的 ASP.NET MVC 4 在安装 ASP.NET MVC 4 Beta 之前预览。

此版本不兼容的.NET Framework 4.5 开发者预览版。 安装 ASP.NET MVC 4 Beta 之前，必须先卸载.NET 4.5 开发人员预览版。

ASP.NET MVC 4 可以安装，并且可以运行的同时使用 ASP.NET MVC 3。

<a id="_Toc303253803"></a>
## <a name="documentation"></a>文档

ASP.NET MVC 的文档位于以下 URL 的 MSDN 网站上有：

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

教程和其他信息 ASP.NET MVC 是 ASP.NET 网站的 MVC 4 页上提供 ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md))。

<a id="_Toc303253804"></a>
## <a name="support"></a>支持

这是预览版本并不正式支持。 如果必须使用此版本有关的问题，请将其发布到 ASP.NET MVC 论坛 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))，ASP.NET 社区的成员是经常能够提供非正式的支持。

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>软件要求

Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 以及 Service Pack 1 的 Visual Studio 2010 或 Visual Web Developer 学习版 2010 Service Pack 1。

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4

ASP.NET MVC 4 可以与 ASP.NET MVC 3 并行安装使您灵活地选择何时升级到 ASP.NET MVC 4 的 ASP.NET MVC 3 应用程序在同一计算机上。

若要升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目并复制所有视图、 控制器、 代码和内容都文件从现有的 MVC 3 项目到新项目，然后更新程序集引用在新项目以匹配旧项目。 如果到 MVC 3 项目中的 Web.config 文件进行了更改，必须还将这些更改合并到 MVC 4 项目中的 Web.config 文件中。

若要手动升级到版本 4 现有的 ASP.NET MVC 3 应用程序，请执行以下操作：

1. 在项目 （还有一个项目，一个视图文件夹中，一个在你的项目中每个区域的 Views 文件夹的根目录中） 中所有 Web.config 文件中，将为每个实例的以下文本：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    使用以下相应的文本：

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. 在根 Web.config 文件中，更新*webPages:Version*为"2.0.0.0"的元素，并添加新*PreserveLoginUrl*具有值"true"的密钥：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. 在解决方案资源管理器中删除对引用*System.Web.Mvc* （它指向版本 3 的 DLL）。 然后添加对的引用*System.Web.Mvc* (v4.0.0.0)。 具体而言，进行以下更改更新程序集引用。 以下为详细信息：

    1. 在解决方案资源管理器，删除对以下程序集的引用： 

        - *System.Web.Mvc*(v3.0.0.0)
        - *System.Web.WebPages*(v1.0.0.0)
        - *System.Web.Razor*(v1.0.0.0)
        - *System.Web.WebPages.Deployment*(v1.0.0.0)
        - *System.Web.WebPages.Razor*(v1.0.0.0)
    2. 添加对以下程序集引用： 

        - *System.Web.Mvc*(v4.0.0.0)
        - *System.Web.WebPages*(v2.0.0.0)
        - *System.Web.Razor*(v2.0.0.0)
        - *System.Web.WebPages.Deployment*(v2.0.0.0)
        - *System.Web.WebPages.Razor*(v2.0.0.0)
4. 在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。 再次右键单击名称，然后选择编辑*ProjectName*.csproj。
5. 找到*ProjectTypeGuids*元素，并替换 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。
6. 保存所做的更改，关闭您所编辑的项目 (.csproj) 文件，右键单击该项目，然后选择重新加载项目。
7. 如果项目引用任何使用 ASP.NET MVC 的以前版本编译的第三方库，打开根 Web.config 文件并添加以下三种*bindingRedirect*下的元素*配置*部分： 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>ASP.NET MVC 4 Beta 中的新增功能

本部分介绍已引入的功能在 ASP.NET MVC 4 Beta 版本。

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET MVC 4 目前包含 ASP.NET Web API、 新框架，用于创建 HTTP 服务可以访问范围广泛的客户端包括浏览器和移动设备。 ASP.NET Web API 也是用于构建 RESTful 服务的理想平台。

ASP.NET Web API 包括以下功能的支持：

- **现代 HTTP 编程模型：** 直接访问和处理 HTTP 请求和响应 Web Api 使用新的、 强类型化的 HTTP 对象模型中。 相同编程模型和 HTTP 管道是对称通过新的 HttpClient 类型在客户端上可用。
- **完全支持路由**: Web Api 现在支持整套一直 Web 堆栈，包括路由参数和约束的一部分的路由功能。 此外，映射到操作具有完全支持约定，因此不再需要应用属性，如 [HttpPost] 到您的类和方法。
- **内容协商**： 客户端和服务器可以协同工作来确定从 API 返回的数据的正确格式。 我们提供对 XML、 JSON 和窗体 URL 编码格式的默认支持并可以通过添加自己的格式化程序来扩展此支持或甚至替换默认内容协商策略。
- **模型绑定和验证：** 模型联编程序提供了简便的方法来从各个组成部分的 HTTP 请求中提取数据并将这些消息部分转换成可由 Web API 操作的.NET 对象。
- **筛选器：** Web Api 现在支持筛选器，包括已知的筛选器，例如 [Authorize] 特性。 可以编写并插入自己的筛选器操作、 授权和异常处理。
- **在查询撰写：** 通过简单地返回 IQueryable&lt;T&gt;，Web API 将支持通过 OData URL 约定的查询。
- **改进了 HTTP 的详细信息的可测试性：** 而不是静态上下文对象中设置 HTTP 详细信息，Web API 操作现在可以处理的 HttpRequestMessage 和 HttpResponseMessage 实例。 这些对象的通用版本也存在以便你可以使用除 HTTP 类型在自定义类型。
- **改进了控制反转 (IoC) 通过 DependencyResolver:** Web API 现在使用由 MVC 的依赖关系解析程序实现的服务定位器模式获取的许多不同的功能实例。
- **基于代码的配置：** 只有通过代码实现 Web API 配置、 离开 config 文件清理。
- **自承载：** Web Api 可以同时仍可使用的路由的所有功能和其他功能的 Web API 托管在自己的进程除 IIS 之外。

有关在 ASP.NET Web API 的更多详细信息，请访问[ https://www.asp.net/web-api ](../web-api/index.md)。

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET 单页面应用程序

ASP.NET MVC 4 目前包含用于生成单页面应用程序与使用 JavaScript 和 Web Api 的重要客户端的交互体验的早期预览版。 此支持包括：

- 一组更丰富的本地交互使用缓存数据的 JavaScript 库
- 工作单元和 DAL 支持的其他 Web API 组件
- 基架，用于快速开始使用一个 MVC 项目模板

在 ASP.NET MVC 4 支持单页面应用程序的详细信息，请访问[ https://www.asp.net/single-page-application ](../single-page-application/index.md)。

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>默认项目模板的增强功能

已更新用于创建新的 ASP.NET MVC 4 项目模板来创建外观更加现代的网站：

![](mvc4-beta-release-notes/_static/image1.png)

除了修饰性的改进，已改进的新模板中的功能。 该模板采用一种名为自适应呈现妙在桌面浏览器和移动浏览器没有任何自定义项中。

![](mvc4-beta-release-notes/_static/image2.png)

若要查看操作中的自适应呈现，可以使用移动仿真程序，或只是尝试调整大小较小的桌面浏览器窗口。 如果浏览器窗口中获取足够小，将更改页的布局。

默认项目模板的另一个增强功能是使用 JavaScript 来提供更丰富的 UI。 在模板中使用的登录和注册链接是如何使用 jQuery UI 对话框以提供丰富的登录屏幕的示例：

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>移动项目模板

如果要开始一个新项目并想要创建一个网站，专门用于移动和平板电脑浏览器，可以使用新的移动应用程序项目模板。 这基于 jQuery Mobile 的用于构建触控优化的 UI 的开放源代码库：

![](mvc4-beta-release-notes/_static/image4.png)

此模板包含为 Internet 应用程序模板相同的应用程序结构 （和控制器代码是几乎完全相同），但它是样式使用 jQuery Mobile 外观精美，同时也在基于触控的移动设备上的行为。 若要了解有关如何结构化和样式移动 UI 的详细信息，请参阅[jQuery 移动项目网站](http://jquerymobile.com/)。

如果已有面向桌面的站点，你想要添加到，移动优化的视图，或如果想要创建一个站点，提供对桌面和移动浏览器以不同的方式应用了样式的视图，可以使用新的显示模式功能。 （请参阅下一节。）

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>显示模式

新的显示模式功能，可以选择根据发出请求的浏览器视图的应用程序。 例如，如果桌面浏览器主页发送请求，应用程序可能使用 Views\Home\Index.cshtml 模板。 如果在移动浏览器主页发送请求，应用程序可能会返回 Views\Home\Index.mobile.cshtml 模板。

布局和部分也可以为特定浏览器类型重写。 例如：

- 如果你的 views/shared 文件夹包含两\_Layout.cshtml 和\_Layout.mobile.cshtml 模板，默认情况下应用程序将使用\_Layout.mobile.cshtml 期间请求从移动浏览器和\_Layout.cshtml 期间其他请求。
- 如果文件夹包含两\_MyPartial.cshtml 并\_MyPartial.mobile.cshtml，指令@Html.Partial("\_MyPartial") 将呈现\_MyPartial.mobile.cshtml 期间从移动设备的请求浏览器和\_MyPartial.cshtml 期间其他请求。

如果你想要创建更具体的视图、 布局或其他设备的分部视图，则可以注册一个新*为 DefaultDisplayMode*实例可以指定其名称以使其搜索请求满足特定条件。 例如，可以添加以下代码*应用程序\_启动*要将字符串"iPhone"注册为 Apple iPhone 浏览器发出请求时应用的显示模式的 Global.asax 文件中的方法：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

此代码运行，当 Apple iPhone 浏览器发出请求后，你的应用程序将使用 views/shared\\_Layout.iPhone.cshtml 布局 （如果存在）。

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile，视图切换器和浏览器重写

jQuery Mobile 是一个开源库，用于构建触控优化的 web UI。 如果你想要与 ASP.NET MVC 4 应用程序使用 jQuery Mobile，您可以下载并安装一个 NuGet 包，可帮助你开始。 若要从 Visual Studio 包管理器控制台中安装它，请键入以下命令：

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

这将安装 jQuery Mobile 和一些帮助器文件，其中包括：

- Views/Shared/\_Layout.Mobile.cshtml，这是 jQuery 的移动布局。
- 视图切换器组件，其中包括Views/Shared/\_ViewSwitcher.cshtml 分部视图和 ViewSwitcherController.cs 控制器。

安装包后，运行应用程序中使用移动浏览器 (或等效的如 Firefox[用户代理切换器](http://chrispederick.com/work/user-agent-switcher/)外接程序)。 你将发现您的页面起来大不相同，因为 jQuery Mobile 处理布局和样式设置。 若要这样做的优点，请执行以下操作：

- 创建移动特定视图，重写下所述[显示模式](#_Toc303253810)之前 （例如，创建要为移动浏览器中重写 Views\Home\Index.cshtml Views\Home\Index.mobile.cshtml）。
- 读取[jQuery Mobile 文档](http://jquerymobile.com/)若要详细了解如何在移动视图中添加触控优化的 UI 元素。

移动优化 web pages 的约定将添加其文本是如桌面视图或完整的站点模式，使用户切换到桌面版本的页面的链接。 JQuery.Mobile.MVC 包包括用于执行此操作的视图切换器组件的示例。 在默认 views/shared\\_Layout.Mobile.cshtml 视图中，其页呈现时其外观类似如下：

![](mvc4-beta-release-notes/_static/image5.png)

如果访问者单击链接时，它们被切换到桌面版本的相同页。

因为桌面设备布局将不包括视图切换器，默认情况下，访客不会有一种方法以获取到移动模式。 若要启用此功能，将以下引用添加到 *\_ViewSwitcher*为桌面的布局，只需内*&lt;正文&gt;* 元素：

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

视图切换器使用称为重写的浏览器的新功能。 此功能允许将请求视为它们传入应用程序之外的其他浏览器 （用户代理） 从他们实际上从。 下表列出了重写的浏览器提供的方法。

| `HttpContext.SetOverriddenBrowser(userAgentString)` | 重写请求的实际用户代理值使用指定的用户代理。 |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | 如果已指定不重写，返回请求的用户代理重写值或将实际用户代理字符串。 |
| `HttpContext.GetOverriddenBrowser()` | 返回*HttpBrowserCapabilitiesBase*对应于当前设置为请求的用户代理的实例 （实际或重写）。 可以使用此值来获取属性，如*IsMobileDevice*。 |
| `HttpContext.ClearOverriddenBrowser()` | 删除当前请求的任何重写的用户代理。 |

浏览器重写是 ASP.NET MVC 4 的核心功能，即使你不安装 jQuery.Mobile.MVC 包也可用。 但是，它会影响视图、 布局和分部视图选择 — 不会影响依赖于任何其他 ASP.NET 功能*Request.Browser*对象。

默认情况下使用 cookie 存储用户代理重写。 如果你想要存储替代其他位置 （例如，在数据库中），则可以替换默认提供程序 (*BrowserOverrideStores.Current*)。 为此提供程序的文档将可随附于 ASP.NET MVC 的更高版本。

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>用于 Visual Studio 中的代码生成方案

新的方案功能，Visual Studio 生成基于你可以使用 NuGet 安装的包的特定于解决方案的代码。 食谱 framework 简化开发人员能够编写代码生成插件，还可用于替换内置代码生成器添加区域、 添加控制器和添加视图。 因为作为 NuGet 包部署方案，可以轻松地签入源代码管理并自动与该项目的所有开发人员共享。 它们也是在每个解决方案的基础上提供。

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>任务支持异步控制器

您现在可以编写异步操作方法的返回类型的对象为 single 方法*任务*或*任务&lt;ActionResult&gt;*。

例如，如果您使用的 Visual C# 5 (或使用[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx))，可以创建异步操作方法，如以下所示：

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

在前面的操作方法的调用中*newsService.GetHeadlinesAsync*并*sportsService.GetScoresAsync*异步调用，不会阻止线程池中的线程。

返回的异步操作方法*任务*实例还支持超时。 若要使操作方法可取消，添加类型的参数*CancellationToken*到操作方法签名。 下面的示例显示了异步操作方法具有 2500年毫秒的超时并显示*TimedOut*查看到客户端，如果发生超时。

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 Beta 支持 Windows Azure SDK 1.5 2011 年 9 月的发布。

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

- **安装 ASP.NET MVC 4 Beta 之后, 在 Visual Studio 2010 Service Pack 1 CSHTML/VBHTML 编辑器中的 CSHTML/VBHTML 编辑器可能会暂停在 cshtml 或 vbhtml 文件中键入代码片段或 JavaScript 后很长时间。** 仅在有刚刚创建且尚未编译的 ASP.NET MVC 4 应用程序中发生这种情况。

    解决方法是以编译该项目的 bin 文件夹中获取程序集。 请注意，是否清理从 bin 文件夹中删除这些程序集的项目时，编辑器问题将会返回。

    将在下一版本中更正此问题。
- **用于 Visual Studio 11 Beta 的 C# 项目模板包含在 Global.asax.cs 中的不正确的连接字符串。** 在应用程序中指定的默认连接\_Visual Studio 11 Beta 中创建的项目包含 LocalDB 连接字符串，它包含非转义反斜杠的启动方法 (\)字符。 这会导致连接错误后尝试访问 Entity Framework DbContext，因此会产生 SqlException。

    若要更正此问题，转义反斜杠字符在应用中的\_启动 Global.asax.cs 方法，以便它读取，如下所示：

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **面向.NET 4.5 的 ASP.NET MVC 4 应用程序将引发 FileLoadException 后尝试访问在.NET 4.0 下运行时的 System.Net.Http.dll 程序集。** .NET 4.5 下创建的 ASP.NET MVC 4 应用程序包含一个绑定重定向，将导致 FileLoadException 的它指示"无法加载文件或程序集 System.Net.Http 或其某个依赖项。" 应用程序执行时的系统上安装.NET 4.0。 若要更正此问题，请从 web.config 中删除以下绑定重定向：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    修改后的 web.config 中的程序集绑定元素应如下所示：

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>Visual Basic 项目中的"添加控制器"项模板会生成不正确的命名空间时调用</strong><strong>从某个区域内。</strong> 当将控制器添加到使用 Visual Basic 的 ASP.NET MVC 项目中的某个区域中时，项模板会将错误的命名空间插入到控制器。 导航到控制器中的任何操作时，结果将是"找不到文件"错误。  
  
  生成的命名空间的根命名空间后省略的所有内容。 例如，生成的命名空间是*RootNamespace*但应该*RootNamespace.Areas.AreaName.Controllers* 。
- **Razor 视图引擎中的重大更改。** 重写 Razor 分析器的一部分，以下类型已从*System.Web.Mvc.Razor*: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  此外已删除以下方法： 

    - *MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
    - *MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*
    - *MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*
- **WebMatrix.WebData.dll 包含在 ASP.NET MVC 4 应用程序的 /bin 目录中，它将接管窗体身份验证的 URL。** （例如，通过使用添加部署依赖性对话框中时，请选择"ASP.NET Web Pages with Razor 语法"） 将 WebMatrix.WebData.dll 程序集添加到你的应用程序将覆盖为登录/帐户 / 身份验证登录重定向而非 /帐户/登录按预期方式默认 ASP.NET MVC 帐户控制器情况。 若要防止此行为，并使用 web.config 的身份验证部分中已指定的 URL，可以添加名为 PreserveLoginUrl 的 appSetting，并将其设置为 true: 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **NuGet 包管理器失败时尝试安装 ASP.NET MVC 4 的并行安装 Visual Studio 2010 和 Visual Web Developer 2010 的安装。** 若要运行 Visual Studio 2010 和 Visual Web Developer 2010 与 ASP.NET MVC 4 并行必须已安装了这两个版本的 Visual Studio 后安装 ASP.NET MVC 4。
- **如果已卸载系统必备组件卸载 ASP.NET MVC 4 将失败。** 若要完全卸载 ASP.NET MVC 4you 必须在卸载 Visual Studio 之前卸载 ASP.NET MVC 4。
- **运行默认的 Web API 项目中显示了将用户添加使用 RegisterApis 方法，不存在的路由不正确定向的说明。** 应使用 ASP.NET 路由表的 RegisterRoutes 方法中添加的路由。
- **安装 ASP.NET MVC 4 Beta 中断 ASP.NET MVC 3 RTM 应用程序。** 已创建的 ASP.NET MVC 3 应用程序与 RTM 版本 （不使用 ASP.NET MVC 3 Tools Update 发行版） 需要执行以下更改才能使用 ASP.NET MVC 4 Beta 并行。 生成项目而无需进行这些更新结果中的编译错误。 

    **所需的更新**

  1. 在根 Web.config 文件中，添加一个新*&lt;appSettings&gt;* 具有键的项*webPages:Version*和值*1.0.0.0*。

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. 在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。 再次右键单击名称，然后选择编辑*ProjectName*.csproj。
  3. 找到以下程序集引用： 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      使用以下内容替换它们：

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. 保存所做的更改，关闭了编辑，然后右键单击项目并选择重新加载项目 (.csproj) 文件。
