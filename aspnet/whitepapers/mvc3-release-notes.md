---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 7342b5f4a7e2327f3f3850941510a6e46ec30842
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823549"
---
<a name="aspnet-mvc-3"></a>ASP.NET MVC 3
====================
- [概述](#overview)
- [安装说明](#installation-notes)
- [软件要求](#software-requirements)
- [文档](#documentation)
- [支持](#support)
- [将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新](#upgrading)
- [ASP.NET MVC 3 工具更新 (2011 年 4 月 12 日)](#tu-changes)

    - ["添加控制器"对话框现在可以快速生成控制器及视图和数据访问代码](#tu-AddControllerDialog)
    - [对改进"ASP.NET MVC 3 新建项目"对话框](#tu-ImprovementsNewDialogBox)
    - [项目模板现在包含 Modernizr 1.7](#tu-Modernizr)
    - [项目模板包含 jQuery、 jQuery UI 和 jQuery 的更新的版本验证](#tu-UpdatedJQuery)
    - [项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包](#tu-EF)
    - [项目模板包含 JavaScript 库作为预安装的 NuGet 包](#tu-JavaScriptLibsNuget)
    - [已知问题](#tu-KI)
- [ASP.NET MVC 3 RTM (2011 年 1 月 13 日)](#MVC3RTM)

    - [更改： 更新版本的 jQuery UI 1.8.7 为](#RTM-1)
    - [更改： 更改 ModelMetadataProvider 回 DataAnnotationsModelMetadataProvider 了默认值](#RTM-2)
    - [已修复： 粘贴 Razor 表达式包含空格导致它被反转的部分](#RTM-3)
    - [已修复： 重命名在编辑器中打开的 Razor 文件禁用语法着色和 IntelliSense](#RTM-4)
    - [已知问题](#RTM-KI)
    - [重大更改](#RTM-BC)
- [ASP.NET MVC 3 候选发布 2 (2010 年 12 月 10 日)](#_Toc2)

    - [项目模板更改为包括 jQuery 1.4.4、 jQuery 验证 1.7 和 jQuery UI 1.8.6y UI 1.8.6](#_Toc2_1)
    - [添加了"AdditionalMetadataAttribute"类](#_Toc2_2)
    - [改进了的视图基架](#_Toc2_3)
    - [添加的 Html.Raw 方法](#_Toc2_3)
    - [已重命名"Controller.ViewModel"属性和"ViewBag"到"视图"属性](#_Toc2_4)
    - [已重命名"ControllerSessionStateAttribute"类"SessionStateAttribute"](#_Toc2_5)
    - [已重命名的 RemoteAttribute"字段"属性设置为"AdditionalFields"](#_Toc2_6)
    - [重命名"SkipRequestValidationAttribute"到"AllowHtmlAttribute"](#_Toc2_7)
    - [已更改"Html.ValidationMessage"方法来显示第一条有用的错误消息](#_Toc2_8)
    - [固定@model声明，以将空格添加到文档](#_Toc2_9)
    - [添加了"FileExtensions"属性设置为视图引擎，以支持特定于引擎的文件的名称](#_Toc2_10)
    - [要发出"For"属性的正确值的固定"LabelFor"帮助程序](#_Toc2_11)
    - [固定"RenderAction"方法，从而使在模型绑定期间的显式值优先级](#_Toc2_12)
    - [重大更改](#_Toc2_BC)
    - [已知问题](#_Toc2_KI)
- [ASP.NET MVC 3 候选发布 (2010 年 11 月 9 日)](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC 中的新增功能](#_Toc276711785)
    - [NuGet 包管理器](#_Toc276711786)
    - [改进了"新建项目"对话框](#_Toc276711787)
    - [无会话控制器](#_Toc276711788)
    - [新的验证特性](#_Toc276711789)
    - [有关"LabelFor"和"LabelForModel"方法的新重载](#_Toc276711790)
    - [子操作输出缓存](#_Toc276711791)
    - ["添加视图"对话框框中改进](#_Toc276711792)
    - [粒度请求验证](#_Toc276711793)
    - [重大更改](#_Toc276711794)
    - [已知问题](#_Toc276711795)
- [ASP。MVC 3 Beta 说明 (2010 年 10 月 6 日)](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 Beta 中的新增功能](#0.1__Toc274034215)
    - [NuPack 包管理器](#0.1__Toc274034216)
    - [改进了新建项目对话框](#0.1__Toc274034217)
    - [简化的方法来指定强类型模型在 Razor 视图中](#0.1__Toc274034218)
    - [支持新的 ASP.NET Web 页的帮助器方法](#0.1__Toc274034219)
    - [其他依赖项注入支持](#0.1__Toc274034220)
    - [新的非介入式 jQuery 基于 Ajax 的支持](#0.1__Toc274034221)
    - [对于非介入式 jQuery 验证新的支持](#0.1__Toc274034222)
    - [客户端验证和非介入式 JavaScript 的新应用程序范围内标志](#0.1__Toc274034223)
    - [对视图运行前运行的代码的新支持](#0.1__Toc274034224)
    - [新的 VBHTML Razor 语法支持](#0.1__Toc274034225)
    - [更精细地控制 ValidateInputAttribute](#0.1__Toc274034226)
    - [帮助程序对于使用匿名对象指定的 HTML 特性名称将下划线转换为连字符](#0.1__Toc274034227)
    - [Bug 修复](#0.1__Toc274034228)
    - [重大更改](#0.1__Toc274034229)
    - [已知问题](#0.1__Toc274034230)
- [免责声明](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>概述

本文档介绍的 ASP.NET MVC 3 RTM for Visual Studio 2010 的版本。 ASP.NET MVC 是一个框架，用于开发 Web 应用程序使用模型-视图-控制器 (MVC) 模式。 ASP.NET MVC 3 安装程序包括以下组件：

- ASP.NET MVC 3 运行时组件
- ASP.NET MVC 3 Visual Studio 2010 工具
- ASP.NET 网页运行时组件
- ASP.NET Web Pages Visual Studio 2010 工具
- Microsoft.NET (NuGet) 包管理器
- 支持 Razor 语法的 Visual Studio 2010 的更新。 （有关详细信息，请参阅知识库文章 2483190）。

可以在位于以下 URL 的 ASP.NET 网站上找到的每个预发行版本的 ASP.NET MVC 3 发行说明的完整集：

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>安装说明

若要安装 ASP.NET MVC 3 RTM 使用 Web 平台安装程序 (Web PI)，请访问以下页面：

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

或者，可以下载 ASP.NET MVC 3 RTM 的安装程序的 Visual Studio 2010 中的以下页面：

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 可以安装，并且可以运行的同时使用 ASP.NET MVC 2。

<a id="software-requirements"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET MVC 3 运行时组件需要以下软件：

- .NET framework 版本 4。 

    ASP.NET MVC 3 Visual Studio 2010 工具需要以下软件：
- Visual Studio 2010 或 Visual Web Developer 2010 速成版。

<a id="documentation"></a>
## <a name="documentation"></a>文档

在 MSDN 网站上的以下 URL 上提供了 ASP.NET MVC 的文档：

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

教程和有关 ASP.NET MVC 的其他信息可在以下 URL 处的 ASP.NET Web 站点的 MVC 页上：

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>支持

这是完全受支持的版本。 有关获得技术支持的信息可在[Microsoft 支持网站](https://support.microsoft.com/)。

也可随意 ASP.NET 社区的成员是经常能够提供非正式的支持在 ASP.NET MVC 论坛中发布有关此发行版的问题：

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新

ASP.NET MVC 3 可以与 ASP.NET MVC 2 并行安装使您灵活地选择何时升级到 ASP.NET MVC 3 的 ASP.NET MVC 2 应用程序在同一计算机上。

若要手动升级到版本 3 现有的 ASP.NET MVC 2 应用程序，请执行以下操作：

1. 在计算机上创建一个新的空 ASP.NET MVC 3 项目。 此项目将包含所需的升级某些文件。
2. 将以下文件从 ASP.NET MVC 3 项目复制到 ASP.NET MVC 2 项目的相应位置。 你将需要更新对 jQuery 库，以说明新的文件名 (jQuery-1.5.1.js) 的任何引用： 

    - /Views/Web.config
    - /packages.config
    - /scripts/\*.js
    - /内容/主题/\*。\*
3. 复制*包*解决方案，即解决方案的.sln 文件所在的目录的根目录到空的 ASP.NET MVC 3 项目解决方案的根目录中的文件夹。
4. 如果你的 ASP.NET MVC 2 项目包含任何区域，则 /Views/Web.config 文件复制到*视图*的每个区域的文件夹。
5. 在 ASP.NET MVC 2 项目中的这两个 Web.config 文件，全局搜索，并替换 ASP.NET MVC 版本。 找到以下： 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    使用以下标记替换它：

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. 在解决方案资源管理器中删除对引用*System.Web.Mvc* （哪个点的 dll 版本 2），然后添加对的引用*System.Web.Mvc* (v3.0.0.0)。
7. 添加对 System.Web.WebPages.dll 和 system.web.helpers.dll 的引用的引用。 这些程序集位于以下文件夹： 

    - %ProgramFiles%\Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. 在解决方案资源管理器，右键单击项目名称并选择卸载项目。 再次右键单击项目名称，然后选择编辑*ProjectName*.csproj。
9. 找到*ProjectTypeGuids*元素，并替换 {F85E285D-A4E0-4152-9332-AB1D724D3325} 为 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。
10. 保存所做的更改，右键单击项目，并选择重新加载项目。
11. 在应用程序的根 Web.config 文件中，添加以下设置来*程序集*部分。 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. 如果项目引用了使用 ASP.NET MVC 2 编译任何第三方库，添加以下突出显示*bindingRedirect*元素下的应用程序根目录中的 Web.config 文件*配置*部分： 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 工具的更新中更改

本部分介绍 ASP.NET MVC 3 RTM 版本发布以来 ASP.NET MVC 3 Tools Update 版本中所做的更改。

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>"添加控制器"对话框现在可以快速生成控制器及视图和数据访问代码

基架是一种方法快速生成控制器和视图为您的应用程序。 生成的代码后，可以编辑它以满足你的项目的要求。

若要启动*添加控制器*对话框在 ASP.NET MVC 3 中，右键单击*控制器*文件夹中的*解决方案资源管理器*，单击*添加*，然后依次*控制器*。 对话框的已得到增强，以便提供其他创建基架选项。

![](mvc3-release-notes/_static/image1.png)

有三个基架模板默认情况下。

#### <a name="empty-controller"></a>空控制器

此模板生成一个空的控制器文件。 此模板等效于不检查*添加的创建、 编辑、 详细信息的操作，删除方案*在以前版本的 ASP.NET MVC。 如果选择此项，没有进一步可用选项。

#### <a name="controller-with-empty-readwrite-actions"></a>包含空读/写操作的控制器

此模板将生成具有所有必需的操作方法，但没有实现代码的方法中的控制器文件。 此模板等效于检查*添加的创建、 编辑、 详细信息的操作，删除方案*在以前版本的 ASP.NET MVC。 如果选择此项，没有进一步可用选项。

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>包含读/写操作和视图，使用实体框架的控制器

此模板，可快速创建工作数据输入用户界面。 它会生成处理各种常见要求和方案，如下所示的代码：

- *数据访问*。 生成的代码读取和写入数据库中的实体。 如果您选择一个现有的数据上下文类，或者让生成一个新的模板，它会使用 Entity Framework Code First 的方法*DbContext*类。 它还会使用 Entity Framework 数据库优先或模型优先方法如果你选择的现有*ObjectContext*类。
- *验证*。 生成的代码使用 ASP.NET MVC 模型绑定和元数据功能，以便窗体提交验证根据在模型类上声明的规则。 这包括内置验证规则，如*所需*并*StringLength*属性和自定义验证规则。
- *一个对多关系*。 如果模型类之间定义一个多外键关系，生成的代码将生成下拉列表中的选择相关的实体。 例如，可能会定义以下 Entity Framework Code First 约定的模型类： 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    当您然后搭建基架的控制器*产品*类，其视图将允许用户选择*类别*每个对象*产品*实例。

    此模板提供了附加选项中的*添加控制器*对话框。 有关*模型类*，可以在解决方案中，它确定的用户将能够创建或编辑的数据类型选择任意模型类：
- 如果你想要使用 Entity Framework Code First，可以选择任意模型类。
- 如果使用 Entity Framework 数据库优先或 Entity Framework 模型优先，请务必选择在概念模型中定义的实体类。

有关*数据上下文类*，可以进行以下选择：

- 如果你想要使用 Code First 且没有现有的数据上下文类中，选择 * * 新的数据上下文 * *。 然后会为您生成数据上下文类。
- 如果你想要使用 Code First，并且具有一个现有的数据上下文类，此处将其选定。 它将更新以保存所选模型类。
- 如果使用 Database First 或 Model First，选择您的对象上下文类。

对于视图，选择所需的视图引擎，或选择无如果不想要创建的任何视图基架。

您可以选择高级选项可用来进一步指定生成的视图的选项。 例如，可以选择布局或母版页中以使用。

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>对改进"ASP.NET MVC 3 新建项目"对话框

用于创建新的 ASP.NET MVC 3 项目对话框的包括多项改进，如下所示。

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>新的"Intranet 项目"模板

项目模板列表中包括新的 Intranet 应用程序模板。 此模板包含用于生成而不窗体身份验证使用 Windows 身份验证的 web 应用程序设置。 由于 intranet 应用程序需要某些不能在项目模板中封装的 IIS 设置，该模板将包含有关如何使项目模板在 IIS 中工作说明的自述文件。 文档位于以下 URL 的 MSDN 网站上提供了新的 Intranet 应用程序模板：

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>项目模板现在都支持 HTML5

新建项目对话框现在包含一个选项以将 HTML5 特定功能添加到项目模板。 选择该选项将导致视图以生成包含新的 HTML5 `<header>`， `<footer>`，和`<navigation>`元素。

请注意，早期版本的浏览器不支持 HTML5 特定的标记。 若要解决此限制，HTML5 项目模板包含对 Modernizr 库的引用。 （请参阅下一节。）

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>项目模板现在包含 Modernizr 1.7

Modernizr 是一个 JavaScript 库，支持 CSS 3 和 HTML5 的浏览器中尚不支持这些功能。 此库是作为预安装的 NuGet 包的 ASP.NET MVC 3 项目模板中包含在内。 有关 Modernizr 的详细信息，请参阅[ http://www.modernizr.com/ ](http://www.modernizr.com/)。

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>项目模板包含 jQuery、 jQuery UI 和 jQuery 的更新的版本验证

项目模板现在包含 jQuery 脚本的以下版本：

- jQuery 1.5.1
- jQuery 验证 1.8
- jQuery UI 1.8.11

作为预安装的 NuGet 包中包含这些库。

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包

ADO.NET Entity Framework 4.1 包含代码优先功能。 Code First 是 ADO.NET 实体框架提供的现有数据库优先和模型优先模式的替代方法的新开发模式。

首先是专注于代码周围定义模型使用 POCO 类 （"普通旧 CLR 对象"） 在 Visual Basic 或 C# 编写。 这些类然后可以映射到现有数据库或用于生成数据库架构。 可以使用提供额外的配置*DataAnnotations*属性或使用 fluent Api。

有关使用代码 Firstwith ASP.NET MVC 文档位于以下 Url 的 ASP.NET 网站上有：

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>项目模板包含 JavaScript 库作为预安装的 NuGet 包

该项目时创建新的 ASP.NET MVC 3 项目时，通过安装其包括前面提到的 JavaScript 文件 （例如，Modernizr 库） 而不直接将脚本添加到脚本文件夹中的项目模板中使用 NuGet内容。 这使您能够使用 NuGet，当发布新版本的脚本时将脚本更新为最新版本。

例如，提供新的 jQuery 版本频率以后，项目模板中包含的 jQuery 版本在某个时候将过期。 但是，由于 jQuery 是作为已安装的 NuGet 软件包包含在内，您将时通知你在 NuGet 对话框中提供了较新版本的 jQuery。

由于 jQuery 在文件名中包含的版本号，因此更新到最新版本的 jQuery 还需要更新`<script>`引用 jQuery 文件以使用新的文件名称的标记。 其他包含的脚本库不包括版本号中的脚本名称，因此它们可以更轻松地更新到最新版本。

<a id="tu-KI"></a>
## <a name="known-issues"></a>已知问题

- 在某些情况下，安装可能会因错误消息"安装失败，错误代码为 (0x80070643)"。 有关如何解决此问题的信息，请参阅[知识库文章 2531566](https://support.microsoft.com/kb/2531566)。
- 添加控制器基架不会创建利用实体继承支持实体框架中的实体基架。 例如，给定基*Person*由继承的类*学生*类，搭建基架*学生*类将导致生成不会进行编译的代码。
- 创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。 解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。
- 在安装 ReSharper 时 IntelliSense for Razor 语法无效。 如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。
- 在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。
- 当您编辑 Razor 视图 (.cshtml 或。*vbhtml*文件)，视图。 ASP.NET MVC 3 不包括 Razor 视图的任何代码段...aspxselecting ASP.NET MVC 的代码段将显示有关代码段
- 如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM 中的更改

本部分介绍更改和自 RC2 发行以来 ASP.NET MVC 3 RTM 版本中所做的 bug 修补程序。

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>更改： 更新版本的 jQuery UI 1.8.7 为

Visual Studio 的 ASP.NET MVC 项目模板已更新以包括最新版本的 jQuery UI 库。 模板还包含所需的 jQuery UI，如关联的 CSS 和图像文件的资源文件的最小集。

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>更改： 更改 ModelMetadataProvider 回 DataAnnotationsModelMetadataProvider 了默认值

RC2 版本的 ASP.NET MVC 3 引入*CachedDataAnnotationsMetadataProvider*类，提供基于现有缓存*DataAnnotationsModelMetadataProvider*声明为类性能改进。 但是，某些 bug 报告与此实现中，以便还原此更改并将其移到 MVC Futures 项目，可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)。

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>已修复： 粘贴 Razor 表达式包含空格导致它被反转的部分

在 ASP.NET MVC 3 的预发布版本中，粘贴到 Razor 文件中，包含空格的 Razor 表达式的一部分时所生成的表达式应反向执行。 例如，考虑以下 Razor 代码块：

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

如果您在第一种方法中选择"第一个 param"文本并将其作为自变量粘贴到第二种方法，则结果是，如下所示：

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

正确的行为是粘贴操作应导致以下：

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

已在 RTM 版本中修复此问题，以便表达式正确地保留在粘贴操作。

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>已修复： 重命名在编辑器中打开的 Razor 文件禁用语法着色和 IntelliSense

重命名在编辑器窗口中打开文件时使用解决方案资源管理器的 Razor 文件会导致语法突出显示和 IntelliSense 停止工作，为该文件。 此问题已修复，以便突出显示和 IntelliSense 维护之后重命名。

<a id="RTM-KI"></a>
## <a name="known-issues"></a>已知问题

- 如果您关闭 Visual Studio 2010 SP1 Beta，NuGet 包管理器控制台处于打开状态时，Visual Studio 崩溃，并尝试重新启动。 这将修复 Visual Studio 2010 SP1 的 RTM 版本中。
- ASP.NET MVC 3 安装程序才能够安装 NuGet 包管理器的初始版本。 已安装的初始版本后，NuGet 可以安装和使用 Visual Studio Extension Manager 更新。 如果已安装 NuGet，请转到 Visual Studio 扩展库更新到最新版本的 NuGet。
- 创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。 解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。
- 安装程序可能需要更长的时间比以前版本的 ASP.NET MVC 来完成。 这是因为它会更新 Visual Studio 2010 的组件。
- 在安装 ReSharper 时 IntelliSense for Razor 语法无效。 如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。
- 与 ASP.NET MVC 3 的测试版创建的 CCSHTML 和 VBHTML 视图没有正确设置其生成操作，使用这些查看结果类型时省略了该项目发布。 这些文件的生成操作值应设置为"内容"。 ASP.NET MVC 3 RTM 修复了对新文件，此问题，但不会更正与预发布版本创建的项目的现有文件的设置。
- ![](mvc3-release-notes/_static/image3.png)
- 在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。
- 编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。
- 如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>重大更改

- 在以前版本的 ASP.NET MVC，操作筛选器是每个请求除在少数情况下创建。 此行为永远不会有保证的行为，但只是实现详细信息，筛选器的约定是将其视为无状态。 在 ASP.NET MVC 3 中，将更主动的方式缓存筛选器。 因此，实例状态不正确存储任何自定义操作筛选器可能已损坏。
- 异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。 在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*值上的操作方法的异常筛选器之前执行这些操作方法上时。 这通常会是这种情况，异常筛选器应用时没有指定*顺序*值。 在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。 在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。
- 名为的新属性*FileExtensions*已添加到*VirtualPathProviderViewEngine*基类。 当 ASP.NET 视图按路径 （不按名称查找） 时，被视为唯一视图与此新属性指定的列表中包含的文件扩展名。 若要启用 Web 窗体视图的自定义文件扩展注册自定义生成提供程序和提供程序使用完整路径而不是一个名称来引用这些视图，这是在应用程序中的重大更改。 解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。
- 直接实现的自定义控制器工厂实现*IControllerFactory*接口必须提供的新实现*GetControllerSessionBehavior*方法添加到此版本中的接口。 一般情况下，建议您不要直接实现此接口和改为从类派生*借助于 DefaultControllerFactory*。

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2 中的更改

本部分介绍了 RC 版本发布以来 ASP.NET MVC 3 RC2 版本中所做的更改 （新功能和 bug 修复）。

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>项目模板更改为包括 jQuery 1.4.4、 jQuery 验证 1.7 和 jQuery UI 1.8.6

ASP.NET MVC 3 的项目模板现在包括最新版本的 jQuery、 验证、 jQuery 和 jQuery UI。 jQuery UI 是一个新项目模板，并提供有用的用户界面小组件。 有关的 jQuery UI 的详细信息，请访问其主页： [ http://jqueryui.com/ ](http://jqueryui.com/)。

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>添加了"AdditionalMetadataAttribute"类

可以使用*AdditionalMetadataAttribute*类来填充*ModelMetadata.AdditionalValues*模型属性的字典。

例如，假设视图模型具有应仅向管理员显示的属性。 该模型可以批注使用新的属性使用 AdminOnly 作为密钥并将 true 作为值，如以下示例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

呈现产品视图模型时，此元数据将提供到任何显示或编辑器的模板。 它取决于您是为应用程序开发人员解释元数据信息。

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>改进了的视图基架

现在使用的基架视图的 T4 模板生成对模板帮助器方法的调用，如*EditorFor*而不是帮助程序，例如*TextBoxFor*。 当添加视图对话框中生成一个视图时，此更改将提高对数据批注特性的窗体中的模型的元数据的支持。

添加视图基架还包括改进的检测和主键信息基于约定的模型上的使用情况。 例如，添加视图对话框中使用此信息以确保主键值不基架为可编辑窗体字段。

默认编辑和创建模板包括对客户端验证所需的 jQuery 脚本的引用。

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>添加的 Html.Raw 方法

默认情况下，Razor 视图引擎进行 HTML 编码的所有值。 例如，下面的代码段将编码的问候语变量中的 HTML，以便显示在页中作为`<strong>Hello World!</strong>`。

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

新*Html.Raw*方法提供了显示未编码的 HTML 时知道的内容是安全的简单方式。 下面的示例显示相同的字符串，但该字符串呈现为标记：

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>已重命名"Controller.ViewModel"属性和"ViewBag"到"视图"属性

以前， *ViewModel*的属性*控制器*对应于*视图*视图的属性。 两个属性提供的访问值的方式*ViewDataDictionary*对象使用动态属性访问器语法。 这两个属性已重命名为相同以避免产生混淆和更一致。

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>已重命名"ControllerSessionStateAttribute"类"SessionStateAttribute"

*ControllerSessionStateAttribute* RC 版本的 ASP.NET MVC 3 中引入了类。 该属性已重命名为更简洁。

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>已重命名的 RemoteAttribute"字段"属性设置为"AdditionalFields"

*RemoteAttribute*类的*字段*属性造成了某些困扰用户之间。 重命名此属性设置为*AdditionalFields*阐明了其意图。

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>重命名"SkipRequestValidationAttribute"到"AllowHtmlAttribute"

*SkipRequestValidationAttribute*属性已重命名为*AllowHtmlAttribute*来更好地表示其预期的用法。

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>已更改"Html.ValidationMessage"方法来显示第一条有用的错误消息

*Html.ValidationMessage*方法已固定的以便显示而不是只需显示的第一个错误的第一个有用的错误消息。

在模型绑定期间*ModelState*可以通过使用有关的属性，包括从模型本身的错误消息的多个源填充字典 (如果它实现了*IValidatableObject*)，从验证特性应用于属性，以及从在访问属性时引发的异常。

当*Html.ValidationMessage*方法显示一条验证消息时，它将模型状态，其中可包含一个异常，跳过，因为这些通常不应为最终用户。 相反，该方法将查找不是与异常相关联，并显示该消息的第一个验证消息。 如果不找到任何此类消息，则默认为与第一个异常相关联的一般性错误消息。

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>固定@model声明，以将空格添加到文档

在早期版本中， <em>@model</em>视图顶部的声明添加到呈现的 HTML 输出一个空行。 此问题已修复，以便声明不会引入的空格。

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>添加了"FileExtensions"属性设置为视图引擎，以支持特定于引擎的文件的名称

视图引擎可以返回视图，使用显式视图路径如以下示例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

第一个视图引擎始终尝试呈现视图。 默认情况下，Web 窗体视图引擎是第一个视图引擎;因为 Web 窗体引擎不能呈现 Razor 视图，就会出错。 视图引擎现在都有*FileExtensions*它们支持的属性，用于指定哪些文件扩展名。 当 ASP.NET 确定视图引擎是否可以呈现文件时，检查此属性。 这是一项重大更改，更多详细信息包含在[的重大更改](#_Toc2_BC)本文档的部分。

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>要发出"For"属性的正确值的固定"LabelFor"帮助程序

已修复 bug 的位置*LabelFor*方法呈现*有关*匹配的属性*输入*元素的*名称*特性其 id。 根据 W3C*有关*属性应与匹配*输入*元素的 id。

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>固定"RenderAction"方法，从而使在模型绑定期间的显式值优先级

在早期版本中，显式值传递给*RenderAction*方法已被忽略，以便支持当前的窗体值在子操作中的模型绑定期间。 此修复可以确保，在模型绑定期间优先的显式值。

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>重大更改

- 在以前版本的 ASP.NET MVC 中，每个请求除在少数情况下创建操作筛选器。 此行为永远不会有保证的行为，但只是实现详细信息，筛选器的约定是将其视为无状态。 在 ASP.NET MVC 3 中，将更主动的方式缓存筛选器。 因此，实例状态不正确存储任何自定义操作筛选器可能已损坏。
- 异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。 在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*值上的操作方法的异常筛选器之前执行这些操作方法上。 异常筛选器应用时，这通常会发生此情况没有指定*顺序*值。 在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。 在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。
- 名为的新属性*FileExtensions*已添加到*VirtualPathProviderViewEngine*基类。 当 ASP.NET 视图按路径 （不按名称查找） 时，被视为唯一视图与此新属性指定的列表中包含的文件扩展名。 若要启用 Web 窗体视图的自定义文件扩展注册自定义生成提供程序和提供程序使用完整路径而不是一个名称来引用这些视图，这是在应用程序中的重大更改。 解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。
- 直接实现的自定义控制器工厂实现<em>IControllerFactory</em>接口必须提供的新实现<em>GetControllerSessionBehavior</em> <em>已添加到此版本中的接口方法</em>。 一般情况下，建议您不要直接实现此接口和改为从类派生<em>借助于 DefaultControllerFactory</em>。

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>已知问题

- ASP.NET MVC 3 安装程序才能够安装 NuGet 包管理器的初始版本。 已安装的初始版本后，NuGet 可以安装和使用 Visual Studio Extension Manager 更新。 如果已安装 NuGet，请转到 Visual Studio 扩展库更新到最新版本的 NuGet。
- 创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。 解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。
- 安装程序可能需要更长的时间比以前版本的 ASP.NET MVC 来完成。 这是因为它会更新 Visual Studio 2010 的组件。
- 在安装 ReSharper 时 IntelliSense for Razor 语法无效。 如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 RC2 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。
- 与 ASP.NET MVC 3 的测试版创建的 CSHTML 和 VBHTML 视图没有正确设置其生成操作，使用这些查看结果类型时省略了该项目发布。 *生成操作*值这些文件应设置为内容"。 ASP.NET MVC 3 RC2 修复了对新文件，此问题，但不会更正与测试版创建的项目的现有文件的设置。![](mvc3-release-notes/_static/image4.png)
- 在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。
- 编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。
- 如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。 Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。 ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。
- 安装 ASP.NET MVC 3 RC 2 不会更新 NuGet，如果你已安装它。 若要升级 NuGet，请转到 Visual Studio 扩展管理器和它应显示为可用的更新。 你可以升级到最新版本从那里 NuGet。

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 的候选发布版本

ASP.NET MVC 候选发布版本已于 2010 年 11 月 9 日发布。

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC 中的新增功能

本部分介绍已引入的功能的 Beta 版本以来 ASP.NET MVC 3 RC 版本中。

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet 程序包管理器

ASP.NET MVC 3 包含 NuGet 包管理器 （以前称为 NuPack），这是将库和工具添加到 Visual Studio 项目的集成的包管理工具。 此工具自动执行开发人员立即采取来访问其源树的一个库的步骤。

你可以使用 NuGet，作为命令行工具，在 Visual Studio 2010 中，在 Visual Studio 上下文菜单中的集成的控制台窗口和一组 PowerShell cmdlet。

有关 NuGet 的详细信息，请阅读[Nuget 文档](https://docs.microsoft.com/nuget/)。

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>改进了"新建项目"对话框

当创建新项目时，新建项目对话框中现在允许你指定的视图引擎，以及 ASP.NET MVC 项目类型。

![](mvc3-release-notes/_static/image5.png)

在此版本中包含对修改的模板和引擎列在对话框中的视图列表支持。

默认模板如下所示：

为空。 包含一组最小的 ASP.NET MVC 项目中，其中包括默认目录结构对于 ASP.NET MVC 项目，包含的默认 ASP.NET MVC 样式，并包含默认的 JavaScript 文件的脚本目录的 Site.css 文件的文件。

Internet 应用程序。 包含演示如何使用 ASP.NET MVC 使用成员资格提供程序的示例功能。

Windows 注册表中指定显示在对话框中的项目模板列表。

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>无会话控制器

新*ControllerSessionStateAttribute*提供更好地控制会话状态行为控制器通过指定[System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)枚举值。

下面的示例演示如何关闭到控制器的所有请求的会话状态。

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

下面的示例演示如何将所有请求的只读会话状态设置为一个控制器。

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>新的验证特性

#### <a name="compareattribute"></a>CompareAttribute

新*CompareAttribute*验证特性可用于比较两个不同模型的属性的值。 在以下示例中， *ComparePassword*属性必须与匹配*密码*是有效的字段。

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

新*RemoteAttribute*验证特性利用 jQuery 验证插件的远程验证程序，从而使客户端验证来执行实际验证逻辑的服务器上调用的方法。

在以下示例中，*用户名*属性具有*RemoteAttribute*应用。 客户端验证时编辑此属性在编辑视图中的，将调用名为操作*UserNameAvailable*上*UsersController*以验证此字段的类。

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

下面的示例显示了相应的控制器。

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

默认情况下，该特性应用于的属性名称是作为查询字符串参数发送到操作方法。

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>有关"LabelFor"和"LabelForModel"方法的新重载

已添加的新重载*LabelFor*并*LabelForModel*方法，可指定标签文本。 下面的示例演示如何使用这些重载。

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>子操作输出缓存

*OutputCacheAttribute*支持通过使用调用子操作的输出缓存*Html.RenderAction*或*Html.Action*帮助器方法。 下面的示例演示一个视图，它调用另一个操作。

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate*操作将批注*OutputCacheAttribute*:

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

此代码运行时，100 秒缓存到 Html.Action("GetDate") 调用的结果。

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>"添加视图"对话框框中改进

当添加强类型化的视图时，添加视图对话框中现在筛选出比早期版本中，例如，许多核心.NET Framework 类型中的多个不适用的类型。 此外，现在排序列表，按类名而不是由完全限定的类型名称，因此可以轻松地查找类型。 例如，类型名称现在显示如以下示例所示：

类名 （命名空间）

在早期版本中，这将显示如下所示：

Namespace.ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>粒度请求验证

*排除*的属性*ValidateInputAttribute*不再存在。 相反，如果希望在模型绑定期间跳过的模型的特定属性的请求验证，请使用新*SkipRequestValidationAttribute*。

例如，假设操作方法用来编辑一篇博客文章：

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

下面的示例显示了一篇博客文章的视图模型。

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

当用户提交的 Description 属性一些标记时，模型绑定将由于请求验证将失败。 若要禁用请求验证在博客文章说明的模型绑定期间，应用*SkipRequpestValidationAttribute*到属性，如在此示例中所示:。

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

或者，若要关闭该模型的每个属性的请求验证，请应用*ValidateInputAttribute*值为*false*到操作方法：

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>重大更改

- 异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。 在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*如操作方法上的异常筛选器之前执行这些操作方法上。 异常筛选器应用时，这通常会发生此情况没有指定*顺序*值。 在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。 在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。
- 添加名为的新属性*FileExtensions*到*VirtualPathProviderViewEngine*基类。 查找视图的路径 （并不是按名称），仅具有文件扩展名中包含的视图时被视为指定此新属性的列表。 这是一项重大更改的用户注册自定义生成提供程序以启用自定义的文件扩展名为 web 窗体视图和所使用的完整路径而不是一个名称来引用这些视图。 解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>已知问题

- 安装程序可能需要更长的时间比以前版本的 ASP.NET MVC，才能完成，因为它会更新 Visual Studio 2010 的组件。
- 添加视图基架时选择 astrongly 类型化视图的基架只写属性。 始终通过搭建基架会忽略这些。 添加视图对话框还搭建基架以只读属性时生成的"编辑"创建"视图。 仅只读属性显示和列表视图的基架。
- 与异步 ctp 版本一起安装 ASP.NET MVC 3 时，调试不起作用。 ASP.NET MVC 3 不能与 Async ctp 版本并行安装。 卸载 Async CTP 修复调试。 有关更多详细信息，请阅读[这篇博客文章](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)有关卸载的 ASP.NET MVC 3 RC 的所有部分。
- 在安装 Resharper 时，则 razor Intellisense 无效。 如果安装了 ReSharper 并且想要利用 Razor intellisense 支持在 ASP.NET MVC 3 RC，请阅读[这篇博客文章](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)来自 JetBrains 其中讨论了如何立即使用它们在一起。
- 使用 ASP.NET MVC 3 的 Beta 创建的 CSHTML 和 VBHTML 视图没有这些文件的生成操作正确它从发布中省略它们。 *生成操作*这些文件应设置为"内容"。 ASP.NET MVC 3 RC 解决了新文件，此问题，但不会更正对现有文件或使用测试版创建的项目的设置。
- 安装程序可能需要更长的时间比以前版本的 ASP.NET MVC，才能完成，因为它会更新 Visual Studio 2010 的组件。
- 添加视图基架时选择"编辑"强类型化视图的基架只读属性。 同样，只写属性都已搭建基架"Display"视图。
- 在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。
- 安装 Visual Studio Async CTP 包含工具安装 ASP.NET MVC 3 Razor 版本将导致冲突。 请确保不尝试在同一台计算机上安装 Visual Studio Async CTP 和 Razor 版本。
- 编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 Beta

ASP.NET MVC 3 试用版已于 2010 年 10 月 6 日发布。 以下说明仅适用于 Beta 版，并受到任何更新或更高版本的 ASP.NET MVC 3 Release Candidate 部分中引用的更改。

## <a id="0.1__Toc274034215"></a>  新 Featuresin ASP.NET MVC 3 的 beta 版本

<a id="0.1__Default_validation_system"></a>本部分介绍已引入的功能在 ASP.NET MVC 3 Beta 版本。

### <a id="0.1__Toc274034216"></a>  NuGet 包管理器

ASP.NET MVC 3 包含 NuGet 包管理器，这是添加的库的集成的包管理工具和 Visual Studio 项目的工具。 大多数情况下，它自动执行开发人员立即采取来访问其源树的一个库的步骤。

你可以使用 NuGet，作为命令行工具，在 Visual Studio 2010 中，在 Visual Studio 上下文菜单中的集成的控制台窗口和组的 PowerShell cmdlet。

有关 NuGet 的详细信息，请阅读[NuGet 文档](https://docs.microsoft.com/nuget/)。

### <a id="0.1__Toc274034217"></a>  改进了新建项目对话框

当创建新项目时，新建项目对话框中现在允许你指定的视图引擎，以及 ASP.NET MVC 项目类型。

![](mvc3-release-notes/_static/image6.png)

在此版本中不包含对修改的模板和引擎列在对话框中的视图列表支持。

默认模板如下所示：

为空。 包含一组最小的 ASP.NET MVC 项目中，其中包括默认目录结构对于 ASP.NET MVC 项目，包含的默认 ASP.NET MVC 样式，并包含默认的 JavaScript 文件的脚本目录的小 Site.css 文件的文件。

Internet 应用程序。 包含演示如何使用 ASP.NET MVC 中的成员资格提供程序的示例功能。

### <a id="0.1__Toc274034218"></a>  简化的方法来指定强类型模型在 Razor 视图中

指定强类型化的 Razor 视图的模型类型的方法已经使用新的进行了简化@model指令的 CSHTML 视图和@ModelTypeVBHTML 视图的指令。 在早期版本的 ASP.NET MVC 中，则会指定一个强类型化的模型，Razor 视图这种方式：

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

在此版本中，可以使用以下语法：

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>  支持新的 ASP.NET Web 页的帮助器方法

新的 ASP.NET Web Pages 技术包括一组可用于将常用的功能添加到视图和控制器的帮助器方法。 ASP.NET MVC 3 支持使用控制器和视图中的这些帮助器方法 （如果适用）。 这些方法包含在 System.Web.Helpers 程序集。 下表列出了几个 ASP.NET Web Pages 帮助器方法。

| **帮助程序** | **说明** |
| --- | --- |
| Chart | 呈现的图表视图中。 包含如 Chart.ToWebImage、 Chart.Save 和 Chart.Write 方法。 |
| 加密 | 使用哈希算法来创建正确加盐，哈希处理密码。 |
| WebGrid | 为网格中呈现的对象 （通常情况下，数据库中的数据） 的集合。 分页和排序的支持。 |
| WebImage | 呈现图像。 |
| WebMail | 发送电子邮件。 |

可用的快速参考主题列出了帮助程序和基本语法是 ASP.NET Razor 语法文档位于以下 URL 的一部分：

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>  其他依赖项注入支持

当前版本的 ASP.NET MVC 3 Preview 1 版本上构建，包括添加了的对两个新服务和四个现有的服务，以及对依赖项解析和公共服务定位器的改进的支持。

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>细粒度的控制器实例化新 IControllerActivator 接口

新的 IControllerActivator 接口提供了如何通过依赖关系注入实例化控制器的更精细地控制。 以下示例演示的接口：

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

相反的角色的控制器工厂。 控制器工厂是实现 IControllerFactory 接口，从而负责查找控制器类型并实例化该控制器类型的实例。

控制器激活器仅负责实例化控制器类型的实例。 它们不会执行控制器类型查找。 找到后正确的控制器类型，控制器工厂应委托到 IControllerActivator 实例来处理控制器的实际实例化。

借助于 DefaultControllerFactory 类具有新的构造函数接受 IControllerFactory 实例。 这可将应用依赖关系注入，若要管理的控制器创建的这个方面，而无需重写默认控制器类型查找行为。

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>替换为 IDependencyResolver IServiceLocator 接口

根据社区反馈，ASP.NET MVC 3 Beta 版本已替换 IServiceLocator 接口使用特定于 ASP.NET MVC 的需求的简化的 IDependencyResolver 接口。 下面的示例演示新界面：

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

作为此更改的一部分，ServiceLocator 类还使用 DependencyResolver 类取代。 注册的依赖关系解析程序是类似于早期版本的 ASP.NET MVC:

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

此接口的实现应只需委托基础依赖关系注入容器提供已注册的服务请求的类型。

当不没有所请求类型的任何已注册的服务时，ASP.NET MVC 期望从 GetService 返回 null 并返回一个空集合从 getservices 进行提取此接口的实现。

新 DependencyResolver 类，可以注册新的 IDependencyResolver 接口或公共服务定位器接口 (IServiceLocator) 实现的类。 有关公共服务定位器的详细信息，请参阅[CommonServiceLocator GitHub 上的](https://github.com/unitycontainer/commonservicelocator)。

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>细粒度视图页实例化新 IViewActivator 接口

新的 IViewPageActivator 接口提供了更加精细地控制如何通过依赖关系注入实例化视图页。 这适用于 WebFormView 实例和 RazorView 实例。 下面的示例演示新界面：

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

这些类现在接受 IViewPageActivator 构造函数参数，它允许你使用依赖关系注入来控制如何实例化的 ViewPage、 ViewUserControl 和 WebViewPage 类型。

#### <a name="new-dependency-resolver-support-for-existing-services"></a>新的依赖关系解析程序支持的现有服务

新版本包括对以下服务的依赖关系解析支持：

- 模型验证程序提供程序。 实现 ModelValidatorProvider 的类可以注册在依赖关系解析程序，并且系统将使用它们来支持客户端和服务器端验证。
- 模型元数据提供程序。 可以在依赖关系解析程序中, 注册的单个类，实现 ModelMetadataProvider 和系统将使用它提供的模板化和验证系统元数据。
- 值提供程序。 实现 ValueProviderFactory 的类可以注册在依赖关系解析程序，并在系统将使用它们创建控制器和模型绑定期间使用的值提供程序。
- 模型联编程序。 实现 IModelBinderProvider 的类可以注册在依赖关系解析程序，并在系统将使用它们创建模型绑定系统使用的模型联编程序。

### <a id="0.1__Toc274034221"></a>  新的非介入式 jQuery 基于 Ajax 的支持

ASP.NET MVC 包括 Ajax 帮助器方法，如下所示：

- Ajax.ActionLink
- Ajax.RouteLink
- Ajax.BeginForm
- Ajax.BeginRouteForm

这些方法使用 JavaScript 来调用服务器，而无需使用完全回发操作方法。 已更新此功能才能利用 jQuery 非介入式的方式。 而不是干扰的方式发出内联客户端脚本，这些帮助器方法分隔行为根据标记发出使用 HTML5 属性*数据 ajax*前缀。 然后将行为应用于标记通过引用适当的 JavaScript 文件。 请确保引用以下 JavaScript 文件：

- jquery-1.4.1.js
- jquery.unobtrusive.ajax.js

此功能的 Web.config 文件中的 ASP.NET MVC 3 新建项目模板，默认情况下启用，但默认情况下，对于现有项目处于禁用状态。 有关详细信息，请参阅[添加的客户端验证和非介入式 JavaScript 的应用程序范围内标志](#0.1_AddedApplicationWideFlagsForClientValida)本文档中更高版本。

### <a id="0.1__Toc274034222"></a>  对于非介入式 jQuery 验证新的支持

默认情况下，ASP.NET MVC 3 Beta 使用 jQuery 验证，以非介入式方式以便执行客户端验证。 若要启用非介入式客户端验证，请如下从视图中所示的调用：

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

这需要 ViewContext.UnobtrusiveJavaScriptEnabled 属性设置为 true 时，您可以通过进行以下调用来执行此操作：

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

此外请确保引用的以下 JavaScript 文件。

- jquery-1.4.1.js
- jquery.validate.js
- jquery.validate.unobtrusive.js

此功能上的 Web.config 文件中的 ASP.NET MVC 3 新建项目模板，默认情况下启用，但默认情况下，对于现有项目处于禁用状态。 有关详细信息，请参阅[客户端验证和非介入式 JavaScript 的新应用程序范围内标志](#0.1_AddedApplicationWideFlagsForClientValida)本文档中更高版本。

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>  客户端验证和非介入式 JavaScript 的新应用程序范围内标志

您可以启用或禁用客户端验证和非介入式 JavaScript 全局使用 HtmlHelper 类，如以下示例所示的静态成员：

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

默认项目模板默认启用非介入式 JavaScript。 您还可以启用或禁用应用程序中使用以下设置的根 Web.config 文件中的这些功能：

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

默认情况下，可以启用这些功能，因为新重载引入到 HtmlHelper 类，允许您替代默认设置，如以下示例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

为了向后兼容，这两项功能默认情况下禁用。

### <a id="0.1__Toc274034224"></a>  对视图运行前运行的代码的新支持

现在可以将名为的文件\_viewstart.cshtml (或\_viewstart.vbhtml) 中 Views 目录并将代码添加到它将在多个视图之间共享该目录及其子目录中。 例如，可能会将下面的代码插入\_viewstart.cshtml 页 ~/Views 文件夹中：

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

这会设置布局页的视图文件夹中的每个视图和所有其子文件夹以递归方式。 视图正在呈现时中的代码\_viewstart.cshtml 文件运行之前查看代码运行。 \_Viewstart.cshtml 代码适用于该文件夹中的每个视图。

默认情况下中的代码\_viewstart.cshtml 文件也适用于任何子文件夹中的视图。 但是，单个子文件夹可以具有其自己版本的\_viewstart.cshtml 文件;，因为的情况下，本地版本将优先。 例如，若要运行普遍适用于 HomeController 的所有视图的代码，将\_viewstart.cshtml ~/Views/Home 文件夹中的文件。

### <a id="0.1__Toc274034225"></a>  新的 VBHTML Razor 语法支持

以前的 ASP.NET MVC 预览版包括对视图使用 Razor 语法基于 C# 的支持。 这些视图使用.cshtml 文件扩展名。 作为正在进行的工作来支持 Razor 的一部分，ASP.NET MVC 3 Beta 引入了对在 Visual Basic 中使用的.vbhtml 文件扩展名的 Razor 语法的支持。

VBHTML 页中使用 Visual Basic 语法的说明，请参阅本教程在以下 URL:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>  更精细地控制 ValidateInputAttribute

ASP.NET MVC 具有始终包括 ValidateInputAttribute 类，该类调用核心 ASP.NET 请求验证基础结构以确保传入的请求不包含潜在的恶意输入。 默认情况下启用输入的验证。 则可以禁用请求验证使用 ValidateInputAttribute 属性，如以下示例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

但是，许多 web 应用程序有需要时剩余的字段不应允许 HTML，单个窗体字段。 ValidateInputAttribute 类现在允许您指定不应包含在请求验证的字段的列表。

例如，如果你正在开发的博客引擎，您可能想要允许在正文和摘要字段中的标记。 这些字段可能由两个输入元素，每个都有属性名称 （"正文"和"摘要"） 对应一个 name 属性表示。 若要禁用请求验证为这些字段，指定 （以逗号分隔） ValidateInput 类，如以下示例所示的 Exclude 属性中的名称：

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>  帮助程序对于使用匿名对象指定的 HTML 特性名称将下划线转换为连字符

帮助器方法，可以指定属性名称/值对使用匿名对象，如以下示例所示：

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

因为 ASP.NET 中的属性名称不能使用连字符，这种方法不允许您使用属性名称中的连字符。 但是，连字符非常重要的自定义 HTML5 属性;例如，HTML5，使用"数据-"前缀。

在此同时，下划线不能用于在 HTML 中，属性名称，但将属性名称中有效。 因此，如果指定使用的匿名对象的属性和属性名称中包含下划线、 帮助程序方法会将下划线转换为连字符。 例如，以下帮助器语法使用下划线：

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

前面的示例将呈现以下标记帮助程序运行时：

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>  Bug 修复

EditorFor 和 DisplayFor 模板帮助器的默认对象模板现在支持 DisplayAttribute.Order 属性中指定的顺序。 （在早期版本中，顺序设置不是使用。）

客户端验证现在支持已应用的验证特性的重写属性的验证。

JsonValueProviderFactory 现在默认情况下注册。

## <a id="0.1__Toc274034229"></a>  重大更改

异常筛选器的执行顺序已更改的异常筛选器具有相同的顺序值。 在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的顺序在控制器上，如操作方法上的异常筛选器之前执行这些操作方法上。 异常筛选器应用而无需指定的顺序值时，这通常会发生此情况。 在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。 在早期版本中，如果显式指定 Order 属性，以指定顺序运行筛选器。

## <a id="0.1__Toc274034230"></a>  已知的问题

在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。

Razor 视图没有 IntelliSense 支持和语法突出显示。 我们已预见到会更高版本的一部分包含在 Visual Studio 中的 Razor 语法的支持。

在编辑 Razor 视图 （CSHTML 文件） 时<a id="0.1__Toc224729061"> </a> <a id="0.1__Toc238051347"> </a>转到控制器在 Visual Studio 中的菜单项将不可用，并且不有任何代码段。

当使用@model语法来指定强类型化的 CSHTML 视图中，无法识别的类型的特定于语言的快捷方式。 例如， @model int 不起作用，但@modelInt32 将起作用。 此 bug 的解决方法是指定模型类型时使用的实际类型名称。

使用时@model语法来指定强类型化的 CSHTML 视图 (或@ModelType来指定强类型化的 VBHTML 视图)，可以为 null 的类型和数组声明不受支持。 例如， @model int？ 不受支持。 请改用`@model Nullable<Int32>`。 语法@modelstring []，也不支持; 请改用`@model IList<string>`。

当 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 时，请确保以下代码添加到 Web.config 文件的 appSettings 节：

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

没有一个已知的问题，会导致窗体身份验证始终将未经身份验证的用户重定向到 ~/Account/登录名，忽略在 Web.config 中使用的窗体身份验证设置。解决方法是添加以下应用设置。

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>  免责声明

© 2011 Microsoft Corporation. 保留所有权利。 本文档提供"作为-是。" 恕不另行通知可能会更改的信息和包括 URL 和其他 Internet 网站参考，本文档中表达的观点。 您自行承担其使用风险。

本文档未向您提供任何 Microsoft 产品中任何知识产权的任何合法权利。 您可为了内部参考目的复制和使用本文档。
