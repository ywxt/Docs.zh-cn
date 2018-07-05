---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: 适用于 ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 发行说明 |Microsoft Docs
author: microsoft
description: 本文档介绍 ASP.NET 和 Web 工具 2013.1 for Visual Studio 2012 的版本。
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2013
ms.topic: article
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 85cd45c25e0f2ad3c8d6d6de73a1a493533e7f7b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374255"
---
<a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 发行说明
====================
by [Microsoft](https://github.com/microsoft)

> 本文档介绍 ASP.NET 和 Web 工具 2013.1 for Visual Studio 2012 的版本。


## <a name="contents"></a>内容

- [安装说明](#install)
- [软件要求](#requirements)
- ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 中的新增功能

    - [Bootstrap](#bootstrap)
    - [模板](#templates)

        - [ASP.NET MVC 5 模板](#mvc5template)
        - [ASP.NET Web API 2 模板](#apitemplate)
        - [项模板](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 基架](#scaffold)
    - [Razor 编辑器](#razor)
    - [NuGet 2.7](#nuget)
- 已知的问题和重大更改

    - [ASP.NET 基架](#issuescaffolding)

        - [MVC 和 Web API 基架-HTTP 404 找不到错误](#404issue)
        - [Visual Studio Express 2012 for Web 添加基架的项后停止工作](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [查看使用浏览方式或 F5 的 cshtml 文件会导致服务器错误](#browseissue)
        - [Url 重写和 Tilde(~)](#rewriteissue)
    - [模板](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>安装说明

[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012。

<a id="requirements"></a>
## <a name="software-requirements"></a>软件要求

您必须具有 Visual Studio 2012 或 Visual Studio Express 2012 for Web。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 中的新增功能

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

当你创建的基架 MVC 5 控制器和视图时，视图的标记使用[Bootstrap](http://getbootstrap.com/)。

<a id="templates"></a>
### <a name="templates"></a>模板

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 模板

我们添加了新的 MVC 5 模板。 它引用最新的 MVC 5 NuGet 包，并可以使用基架添加控制器和视图。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 模板

我们添加了新的 Web API 2 模板。 它引用最新的 Web API 2 NuGet 包，并可以使用基架添加控制器和视图。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>项模板

我们添加了新项模板的 MVC 5 视图、 网页 (Razor 3) 和 Web API 2 控制器。 在添加新项时相关的 NuGet 包安装到项目。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

当您创建基架 MVC 或 Web API 控制器使用 Entity Framework 时，我们使用 Framework 6。 有关实体框架的详细信息，请参阅[Entity Framework 版本历史记录](https://msdn.com/data/jj574253)。

您还可以下载并安装用于 Visual Studio 2012 的 Entity Framework 6 工具。 请参阅[获取实体框架](https://msdn.com/data/ee712906#tooling)。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。 它可以轻松地将样板代码添加到项目中使用的数据模型进行交互。

在以前版本的 Visual Studio 中，基架被限制为 ASP.NET MVC 项目。 利用此更新，现在可以用于任何 ASP.NET 项目，包括 Web 窗体中使用基架。 此更新不支持的 Web 窗体项目，生成页，但您仍可以使用基架，Web 窗体通过向项目添加 MVC 依赖项。 将在未来更新中添加对生成的 Web 窗体页的支持。

在使用基架，我们确保所有必需的依赖项安装在项目中。 例如，如果您开始创建 ASP.NET Web 窗体项目，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用将自动添加到你的项目。

若要将 MVC 基架添加到 Web 窗体项目，添加**新基架项**，然后选择**MVC 5 依赖项**在对话框窗口中。 有两个选项基架 MVC;最小和完全。 如果你选择最小，NuGet 包和 ASP.NET MVC 的引用添加到你的项目。 如果选择完全选项，添加最小依赖项，以及对于 MVC 项目所需的内容文件。

对基架异步控制器的支持使用从 Entity Framework 6 的新异步功能。

有关详细信息和教程，请参阅[ASP.NET 基架概述](../2013/aspnet-scaffolding-overview.md)。 这些教程介绍基架使用 Visual Studio 2013，但它们也适用于 ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012。

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 编辑器

利用此更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包括一套丰富的新功能描述了这些详细的介绍[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)。

此版本的 NuGet 不再需要用户显式允许 NuGet 还原缺失的包。 在安装时 NuGet 2.7，用户隐式同意自动还原缺失的包。 用户可以显式选择不通过 Visual Studio 中的 NuGet 设置包还原。 此更改，简化了包还原的工作原理。

## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 基架

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 基架-HTTP 404 找不到错误

如果将基架的项添加到项目时遇到错误，，则可能你的项目将会处于不一致的状态。 一些将基架所做的更改将被回滚，但其他更改，例如已安装的 NuGet 包，将不会回滚。 如果回滚路由的配置更改，用户将收到 HTTP 404 错误时导航到已搭建基架的项。

若要对 MVC 修复此错误，请添加一个新的基架的项，然后选择 MVC 5 依赖项 （最小或完整）。 此过程将向你的项目添加所有所需的更改。

若要对 Web API 来修复此错误：

1. 将以下 WebApiConfig 类添加到你的项目。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 应用程序中配置 WebApiConfig.Register\_Global.asax 中的 Start 方法，如下所示：

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 for Web 添加基架的项后停止工作

如果 Visual Studio Express 2012 for Web 添加与实体框架 （例如 Web API 2 控制器的操作，使用实体框架） 的基架的项后停止工作，就可以，Visual Studio 速成版无法加载程序集的本机映像依赖于 System.Web.Extensions。

若要更正此问题，请配置 Visual Studio Express 使用 System.Web.Extensions MSIL 映像：

1. 在管理员模式下打开命令提示符。
2. 转到 %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE 或 %programfiles(x86) %\Microsoft Visual Studio 11.0\Common7\IDE （适用于 64 位 Windows）。
3. 在文本编辑器中打开 VWDExpress.exe.config。
4. 添加以下行下的&lt;配置&gt;/&lt;运行时&gt;元素：  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 重新启动 Visual Studio Express 2012 for Web。

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-withbrowse-withorf5causes-a-server-error"></a>查看服务器错误的 cshtml 文件 withBrowse WithorF5causes

当您在 Visual Studio 2012 （或在 Visual Studio 2013 中创建的 Visual Studio 2012 MVC 5 项目中打开） 中创建的 MVC 5 项目，并尝试通过浏览方式或 F5 查看 cshtml 文件时，将收到一个错误，指明-**中的服务器错误'/' 应用程序**。 服务器将尝试导航到 `http://localhost:XXXX/Views/../XXXX.cshtml`

若要解决此问题，请更改**启动操作**在您的项目中设置**特定页**。 不需要为页面提供一个值。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

此更改后，选择 f5 键导航到你的应用程序的根目录 (`http://localhost:XXXX`)。 此行为不是相同的行为对于 MVC 5 项目在 Visual Studio 2013 中，其中**当前页**设置启动打开页。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 重写和 Tilde(~)

升级到 ASP.NET Razor 3 或 ASP.NET MVC 5 后，tilde(~) 表示法可能无法再正常工作如果您使用的 URL 重写。 URL 重写会影响 tilde(~) 表示法中的 HTML 元素，如&lt;A /&gt;，&lt;脚本 /&gt;，&lt;链接 /&gt;，并因此颚化符不再将映射到的根目录。

例如，如果您重写的请求**asp.net/content**到**asp.net**中的 href 属性&lt;href ="~/content/"/&gt;解析为 **/content/内容 /** 而不是**/**。 若要禁止显示此更改，可以设置**IIS\_WasUrlRewritten**为 false，在每个网页中或在上下文**应用程序\_BeginRequest** Global.asax 中。

<a id="templateissue"></a>
### <a name="templates"></a>模板

当您创建 ASP.NET MVC 项目使用 Visual Studio 2012 Windows 8.1 或 Windows Server 2012 R2，Visual Studio 上显示错误消息，指出"配置 Web [url] 用于 ASP.NET 4.5 失败。"

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

因为 Visual Studio 2012 不会启用 ASP.NET 4.5 功能，这些版本的 Windows 上安装时看到此错误。 若要启用 ASP.NET 4.5，请执行中所述的步骤[打开或关闭打开的 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)。

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

或者，您可以通过命令行启用 ASP.NET 4.5。

1. 在管理员模式下打开命令提示符。
2. 运行以下命令以启用 ASP.NET 4.5。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
