---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET 和 Web 工具 2013.2 for Visual Studio 2013 发行说明 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: fb36d9f469265be60a7e40ed7e317d8da6560bf9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824492"
---
<a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET 和 Web 工具 2013.2 for Visual Studio 2013 发行说明
====================
by [Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>安装说明

ASP.NET 和 Web Tools for Visual Studio 2013.2 被捆绑在主安装程序中，并且可以作为的一部分下载[Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521)。

## <a name="documentation"></a>文档

教程和有关 ASP.NET 和 Web 工具的 Visual Studio 2013.2 其他信息中有[ASP.NET web 站点](https://www.asp.net/)。

## <a name="software-requirements"></a>软件要求

ASP.NET 和 Web Tools for Visual Studio 2013.2 需要 Visual Studio 2013。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>ASP.NET 和 Web Tools for Visual Studio 2013.2 中的新增功能

以下部分介绍已在版本中引入的功能。

- [一个 ASP.NET 项目模板](#oneaspnet)
- [启动 IIS Express 上的 Web 应用程序时支持 SSL](#ssl)
- [Visual Studio Web 编辑器增强功能](#vswebeditor)
- [浏览器链接](#browserlink)
- [在 Visual Studio 中的 Azure 应用服务 Web 应用的支持](#waws)
- [创建新的 Web 项目时创建远程 Azure 资源](#AzureResources)
- [Web 发布增强功能](#webpublish)
- [ASP.NET 基架](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web 窗体](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET Web Pages 3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET 标识 2.0.0](#identity)
- [Microsoft OWIN 组件](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>一个 ASP.NET 项目模板

- 对 ASP.NET 项目模板，以支持帐户确认和密码重置的更新。
- 更新以支持使用在本地组织帐户进行身份验证的 ASP.NET Web API 模板。
- ASP.NET SPA 模板现在包含基于 MVC 和服务器端视图的身份验证。 该模板具有只能由经过身份验证的用户访问的 WebAPI 控制器。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>启动 IIS Express 上的 Web 应用程序时支持 SSL

若要消除安全警告浏览和调试在本地主机上的 HTTPS 时，我们添加了一个对话框，以允许 Internet Explorer 和 Chrome 信任自签名的 IIS express SSL 证书。

例如，web 项目属性可以设置为使用 SSL。 单击 F4 以显示属性对话框。 更改**已启用 SSL**为 true。 复制 SSL URL。

![启用 SSL 的属性](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

基于 URL 集的 web 项目属性页 web 选项卡为使用 HTTPS (SSL URL 将为`https://localhost:44300/`除非之前已创建 SSL 网站。)

![设置项目 URL (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

按 Ctrl+F5 运行应用程序。 按照说明信任 IIS Express 生成的自签名的证书。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

读取**安全警告**对话框，然后再单击**是**如果你想要安装表示本地主机的证书。

![安全警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

该站点将显示 IE 或 Chrome 中而无需在浏览器中证书警告。

![HTTPS 页面，而没有发出警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox 会使用其自己的证书存储，因此它将显示一条警告。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio Web 编辑器增强功能

- **新的 JSON 项目项和编辑器**： 我们已向 Visual Studio 中添加 JSON 项目项和编辑器。 当前 JSON 编辑器功能包括着色、 语法验证、 大括号完成、 大纲显示、 工具选项设置和的详细信息。

    ![JSON 编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense 现在支持[JSON 架构](http://json-schema.org/)v3 和 v4。 一个架构组合框来选择现有的架构中，编辑本地架构路径，或只需拖放到它，以获得的相对路径的项目 JSON 文件。

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 架构编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新 Sass (SCSS) 编辑器**： 我们添加了小于 VS2013 RTM，和我们现在有 Sass 项目项和编辑器。 Sass 编辑器功能类似于 LESS 编辑器中，并包括着色、 变量和 Mixin IntelliSense，注释/取消注释、 快速信息、 格式设置、 语法验证、 大纲显示、 转到定义、 颜色选取器工具等设置选项。

    ![添加新项： SCSS 样式表](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![样式表编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **中的 HTML，Razor，CSS，更少的新 URL 选取器和 Sass 文档：** VS 2013 附带的外部 Web 窗体页没有 URL 选取器。 为 HTML，Razor，CSS，更少的新 URL 选取器和 Sass 编辑器是能够理解的对话框免费使用，fluent 键入选取... 并筛选器文件列出相应的 img 标记和链接。

    ![URL 选取器的图像标记](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![URL 选取器的视图](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![针对 CSS URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **通过添加更多的功能的 LESS 编辑器的更新**
- **Knockout Intellisense 升级**： 我们添加了 VS intelliSense 的非标准 KnockOut 语法"ko vs 编辑器 viewModel:"语法。 它可以用于绑定到窗体中使用注释在页面上的多个视图模型：

    ![Knockout Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    我们还添加了对嵌套的 ViewModel IntelliSense 的支持，因此你可能将钻取到 viewmodel 的深度嵌套对象。

    `<div data-bind="text: foo.bar.baz.etc" />`

    显示 IntelilSense 是 JavaScript 对象的完整的 IntelliSense。

    ![Intellisense 显示完整的 JavaScript 对象](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **中的 HTML，Razor，CSS，更少的新 URL 选取器和 Sass 文档**: VS 2013 附带的外部 Web 窗体页没有 URL 选取器。 为 HTML，Razor，CSS，更少的新 URL 选取器和 Sass 编辑器是能够理解的对话框免费使用，fluent 键入选取... 并筛选器文件列出相应的 img 标记和链接。

    ![URL 选取器的图像标记](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![URL 选取器的视图](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![针对 CSS URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>浏览器链接

- 浏览器链接现在支持 HTTPS 连接将列表，并在仪表板与其他连接，只要浏览器信任证书。
- 静态 HTML 源映射
- SPA 支持映射数据
- 自动更新映射数据

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>在 Visual Studio 中的 Azure 应用服务 Web 应用的支持

- **支持 Azure 登录。**
- **远程调试和远程 web 应用的视图**： 我们现在支持[Azure 应用服务中的 web 应用远程调试](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)和 web 应用中的内容文件服务器资源管理器远程视图。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>创建新的 Web 项目时创建远程 Azure 资源

我们添加了 Azure ["创建远程资源"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)新建的 web 应用程序对话框上的复选框。 通过选择它，你将能够创建新的 web 应用程序，设置测试，并在几个简单步骤中创建的发布配置文件的 Azure 发布站点的体验集成。

![使用 Azure 资源的新项目](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![发布到 Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 发布增强功能

- 改善用户体验进行发布。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

- **枚举支持：** 如果您的模型正在使用的枚举，则 MVC 基架将为枚举生成下拉列表。 这将在 MVC 中使用的枚举帮助器。
- **启动支持**： 更新中 MVC 基架的 EditorFor 模板，以便他们使用的 Bootstrap 类。
- **包支持**: MVC 和 Web API 基架将 5.1 包添加 MVC 和 Web API

下面的屏幕截图演示了基架模型。

- 模型的代码：

     ![模型代码](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 编译模型代码，右键单击，并选择**外**，**新基架项**。

     ![添加新的基架的项](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- 选择**MVC5 控制器的包含视图使用 Entity Framework**:

     ![添加新的包含视图 MVC5 控制器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **添加控制器**使用模型：

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 检查生成的代码，例如包含 Views/WeekdayModels/Edit.cshtml `@Html.EnumDropDownListFor`:![查看包含 EnumDropDownListFor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 运行页后，若要查看生成的枚举组合框，请注意，是否值可以为 null，空字符串可选择的组合框。 例如，**创建**页显示以下：

    ![允许空字符串的组合框](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM 将在 2014 年 4 月发布。 以下是要点从发行说明，但请检查[完整的发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.8)有关这些更改的详细信息。

- **面向 Windows Phone 8.1 应用程序**: NuGet 2.8.1 现在支持针对 Windows Phone 8.1 应用程序使用 WindowsPhoneApp、 WPA、 WindowsPhoneApp81 和 WPA81 时，目标框架名字对象。
- **依赖项的修补程序解决**： 时解析包依赖项，NuGet 已从历史上看实现选择满足对包依赖项的最小主版本号和次包版本的策略。 与不同的主版本号和次版本，但是，修补程序版本是始终解析为的最高版本。 该行为是善意的但缺乏安装具有依赖项包的确定性创建它。
- **DependencyVersion 开关**： 尽管 NuGet 2.8 更改*默认*解析依赖项的行为，它还添加了更精确地控制依赖项解析进程通过中的-DependencyVersion 开关包管理器控制台。 开关可以启用对可能的最低版本 （默认行为）、 可能的最高版本，或最高次要或修补程序版本的解析依赖项。 此开关仅适用于在 powershell 命令中的安装包。
- **DependencyVersion 属性**： 除了上面详细说明-DependencyVersion 开关，NuGet 还允许进行定义的默认值什么，如果-DependencyVersion 开关在 nuget.config 文件中设置新的属性的功能未安装包的调用中指定。 NuGet 包管理器对话框中的任何安装包操作还会遵循此值。 若要设置此值，请将以下属性添加到在 nuget.config 文件：

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **预览 NuGet 操作使用-whatif**： 某些 NuGet 包可以有深入的依赖项关系图，并且在这种情况下，它可以在安装过程中会有所帮助、 卸载或更新操作，以首先查看会发生什么情况。 NuGet 2.8 添加标准 PowerShell-如果切换到启用可视化命令将应用于包的完整闭包的安装包、 卸载包和更新包命令。
- **降级包**： 并不少见安装包的预发布版本，以便调查的新功能，然后决定要回滚到上次的稳定版本。 之前 NuGet 2.8，这是一个多步骤过程，以及卸载预发行包和其依赖项，然后安装较早版本。 使用 NuGet 2.8，但是，更新包将现在回滚整个包闭包 （例如包的依赖项树） 到以前的版本。
- **开发依赖项**： 可作为 NuGet 包-包括用于优化开发过程的工具提供许多不同类型的功能。 这些组件，它们可有助于开发新的包，而不应将发布更高版本时，新的包的依赖项。 NuGet 2.8 允许包将自身标识为 developmentDependency.nuspec 文件中。 安装时，此元数据将也添加到已在其中安装了包的项目的 packages.config 文件。 在 nuget.exe 包期间该 packages.config 文件更高版本分析的 NuGet 依赖项，它将排除这些依赖项标记为开发依赖项。
- **针对不同平台的单独的 packages.config 文件**： 开发针对多个目标平台的应用程序，它时，通常会为每个相应的生成环境中有不同的项目文件。 也很常见使用不同的 NuGet 包在不同的项目文件中，如包具有不同级别的不同平台的支持。 NuGet 2.8 支持改进了这种情况下通过创建不同的特定于平台的项目文件的不同 packages.config 文件。
- **回退到本地缓存**： 尽管 NuGet 包会通常占用从远程库等[NuGet 库](http://www.nuget.org)使用的网络连接，有许多方案，客户端未连接。 无网络连接，NuGet 客户端无法成功安装包的即使这些包已在本地 NuGet 缓存中的客户端的计算机上。 NuGet 2.8 将自动缓存回退添加到包管理器控制台。

    缓存回退功能不需要任何特定的命令参数。 此外，只能在包管理器控制台中当前运行缓存回退-行为目前不能在包管理器对话框。
- **Bug 修复**： 所做的主要 bug 修复之一就是更新包中的性能改进的重新安装命令。

    除了这些功能和前面提到的性能修复程序，此版本的 NuGet 还包括许多其他 bug 修复。 出现的版本中解决的 181 总问题。 有关完整列表的工作项中已修复 NuGet 2.8，请查看[NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)对于此版本。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

- Web 窗体模板现在显示如何为 ASP.NET 标识的帐户确认和密码重置。
- 实体数据源控件和 Entity Framework 6 的动态数据访问接口。 有关更多详细信息，请参阅以下 MSDN 博客：[动态数据提供程序和 Entity Framework 6 的 EntityDataSource 控件](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [属性路由改进](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Bootstrap 支持编辑器模板](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [在视图中的枚举支持](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Unobstrusive 支持 MinLength / MaxLength 属性](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [支持非介入式 Ajax 中的 this 上下文](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [全局错误处理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [属性路由的增强功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [帮助页的改进](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 支持](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 的媒体类型格式化程序](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [更好地支持异步筛选器](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [查询分析为客户端格式设置库](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Pages 3.1.2

- 各种[bug 修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

实体框架已更新到版本 6.1，运行时和工具。 实体框架 (EF) 6.1 是 Entity Framework 6 的一个次要更新，包括大量的 bug 修复和新功能。 有关详细信息 EF6.1，包括指向文档的新功能，请参阅[Entity Framework 版本历史记录](https://msdn.microsoft.com/data/jj574253)。 在此版本中的新功能包括：

- **工具合并**提供一致的方法来创建新的 EF 模型。 此功能扩展了 ADO.NET 实体数据模型向导，以支持创建 Code First 模型，包括从现有数据库反向工程。 这些功能都在 EF Power Tools Beta 质量以前不可用。
- **处理的事务提交失败**提供的新[System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx)该协议使用新引入的功能以截获事务操作。 **CommitFailureHandler**允许同时提交事务连接故障自动恢复。
- **IndexAttribute**允许通过将属性 （或属性） 的属性放置在 Code First 模型中指定的索引。 代码首先将然后对应的索引在数据库中创建。
- **公共映射 API**提供对 EF 对如何属性和类型映射到数据库中列和表的信息的访问。 在以前的版本此 API 的内部。
- **能够配置通过 App/Web.config 文件侦听器**（允许拦截器，以添加无需重新编译应用程序）。
- **DatabaseLogger**是一个新的侦听器，它可以更轻松地记录到文件中的所有数据库操作。 与以前的功能组合，这允许您轻松地切换的已部署的应用程序，而无需重新编译的数据库操作的日志记录。
- **迁移模型更改检测**已得到改进，以便更准确; 更改检测进程的性能也大大增强已搭建基架的迁移。
- **性能改进**包括在初始化过程中减少的数据库操作，在 LINQ 查询中的 null 相等比较的优化更快地查看生成 （模型创建） 中更多方案，和更高效具有多个关联的被跟踪实体的具体化。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET 标识 2.0.0

- **双因素身份验证**: ASP.NET 标识现在支持双因素身份验证。 双因素身份验证提供给用户帐户在其中你的密码遭到入侵的情况下安全的额外一层。 此外，还有两个身份代码对暴力破解攻击的保护。
- **帐户锁定：** 提供了一种方法来锁定用户，如果用户输入其密码或双因素代码不正确。 无效的尝试次数和时间跨度的数量的用户被锁定可以配置。 开发人员可以根据需要关闭帐户锁定为特定用户帐户应在需要。
- **帐户确认：** ASP.NET 标识系统现在支持帐户确认。 这是相当常见方案，在今天的大多数网站，网站上的一个新帐户注册时，您需要激活帐户前您可以执行任何操作的网站中确认你的电子邮件。 电子邮件确认很有用，因为它可防止虚假帐户创建。 此功能非常有用，如果您使用电子邮件作为与你的网站等论坛站点、 银行、 电子商务或社交网站的用户进行通信的方法。
- **密码重置：** 密码重置是一项功能，用户才能重置密码，如果用户忘记其密码。
- **（出所有位置的登录） 的安全戳：** 支持一种方式，若要重新生成的用例中的用户的安全令牌，当用户更改其密码或任何其他安全相关信息，例如删除关联的登录名 （例如 Facebook、 Google、Microsoft 帐户等）。 这被需要确保任何使用旧密码生成的令牌都无效。 在示例项目中，如果您更改用户的密码然后为用户生成一个新的令牌和任何以前的令牌都无效。 此功能提供了额外的到当您更改密码，因为应用程序的安全层，你将注销从所有位置注销 （所有其他浏览器），您已登录到此应用程序。
- **创建主键是可扩展的用户和角色的该类型**： 在 ASP.NET 标识 1.0 中，主键的表的用户和角色类型为字符串。 这意味着在 ASP.NET 标识系统中 SQL Server 持久化使用 Entity Framework，我们使用 nvarchar。 没有此 Stack Overflow 上的默认实现的很多话题和基于传入的反馈。 我们提供了扩展性挂钩，您可以在其中指定内容应为您的用户和角色的表的主键。 扩展性挂钩，此功能尤其有用，如果要迁移你的应用程序和应用程序已存储的 Userid 是否 Guid 或整数。
- **在用户和角色上支持 IQueryable**： 添加了的对 IQueryable UsersStore 和 RolesStore，可以轻松地获取用户和角色的列表。
- **支持通过 UserManager 的删除操作**
- **对用户名的索引编制**: ASP.NET 标识实体框架中实现中，我们已添加唯一索引的用户名在 EF 6.1.0 使用新 IndexAttribute。 这可确保用户名始终是唯一的但却没有在其中您最终可能会得到重复用户名的争用条件。
- **增强的密码验证程序：** 随附在 ASP.NET 标识 1.0 的密码验证程序已相当简单的密码验证程序，它仅已验证的最小长度。 没有新的密码验证程序，可提供更好地控制密码的复杂性。 请注意，即使启用此密码中的所有设置，我们执行鼓励您启用双因素身份验证的用户帐户。
- **IdentityFactory 中间件 / CreatePerOwinContext**:

    - **用户管理器**： 可以使用工厂实现以从 OWIN 上下文获取 UserManager 的实例。 此模式非常类似于我们获取 AuthenticationManager OWIN 上下文中登录和注销的使用。 这是推荐的方法来获取每个应用程序请求 UserManager 的实例。
    - **DbContextFactory**: ASP.NET 标识使用 Entity Framework 进行持久保存在 SQL Server 中的标识系统。 若要执行此操作的身份识别系统具有对 ApplicationDbContext 的引用。 DbContextFactory 中间件返回每个请求可以在你的应用程序中使用 ApplicationDbContext 的实例。
- **ASP.NET 标识示例 NuGet 包**： 示例 NuGet 包可以使其更加易于安装和运行示例的 ASP.NET 标识和遵循的最佳做法。 这是一个示例 ASP.NET MVC 应用程序。 请修改该代码以满足你的应用程序之前你将它部署在生产环境中。 该示例应安装在空的 ASP.NET 应用程序。 有关包的详细信息，请转到以下博客文章：[宣布推出 RTM 的 ASP.NET 标识 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 组件

没有大量已在此版本中修复的 bug。 请参阅[2.1.0 的发行说明发行](https://katanaproject.codeplex.com/releases/view/113281)更多详细信息。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

没有大量已在此版本中修复的 bug。 请参阅[2.0.2 的发行说明发行](https://github.com/SignalR/SignalR/releases/tag/2.0.2)更多详细信息。
