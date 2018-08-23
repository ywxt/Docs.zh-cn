---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web Tools 2012.2 发行说明 |Microsoft Docs
author: rick-anderson
description: ASP.NET 和 Web 工具 2012.2 发行说明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: 0566a362b36f6cfb73b6479cd490e82c63455459
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833751"
---
<a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 发行说明
====================
> 本文档介绍 ASP.NET 和 Web Tools 2012.2 的发布。 它是对 Visual Studio Web 工具和 ASP.NET 的更新。


- [安装说明](#_Installation)
- [文档](#_Documentation)
- [支持](#_Support)
- [软件要求](#_Software_Requirements)
- [ASP.NET 和 Web 工具 2012.2 中的新增功能](#_New_Features_in)

    - [工具](#_Tooling)
    - [Web 发布](#_Web_Publishing)
    - [ASP.NET MVC 模板](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 友好 Url](#_ASP.NET_Friendly_URLs)
- [已知的问题和重大更改](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安装说明

ASP.NET 和 Web Tools 2012.2 适用于 Visual Studio 2012 可以使用安装[Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)。 这是对 Visual Studio 2012 或 Visual Studio Express 2012 for Web，这是必需的更新。 如果还没有安装 Visual Studio，将安装 Visual Studio Express 2012 for Web。

您可以手动安装 ASP.NET 和 Web Tools 2012.2。 您必须具有 Visual Studio 2012 或 Visual Studio Express 2012 for Web 安装。 然后使用以下说明： 

1. 下载[ASP.NET 和 Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)从下载中心安装程序。
2. 当提示的单击运行。 此外可以保存该文件以更高版本运行。
3. 验证你将更新的 Visual Studio 的版本。 可以通过启动 Visual Studio 你想要更新执行此操作。 然后单击帮助菜单项。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 如果你看到的菜单项&quot;有关 Microsoft Visual Studio 2012 for Web&quot;然后下载[Web 开发人员工具 2012.2-Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228)。 否则下载[Web 开发人员工具 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。
5. 当提示的单击运行。 此外可以保存该文件以更高版本运行。

> [!NOTE]
> ASP.NET 和 Web 工具 2012.2 发行版不包括 SQL Server Data Tools。 SQL Server 和 Windows Azure SQL 数据库提供了更加丰富的工具包括脱机支持项目的开发、 架构比较和增强的数据库部署功能的数据库。 有关详细信息或要安装 SQL Server Data Tools 请访问[ https://go.microsoft.com/fwlink/?LinkID=237127 ](https://go.microsoft.com/fwlink/?LinkID=237127)。

<a id="_Documentation"></a>
## <a name="documentation"></a>文档

教程和有关 ASP.NET 和 Web Tools 2012.2 的其他信息是可通过 ASP.NET 网站 ( https://www.asp.net)。

<a id="_Support"></a>
## <a name="support"></a>支持

ASP.NET 和 Web Tools 2012.2 是正式发布，支持。 可以使用普通的支持通道。 你可以将问题发布到 ASP.NET 论坛 ([https://forums.asp.net/](https://forums.asp.net/))，ASP.NET 社区的成员是经常能够提供非正式的支持。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET 和 Web Tools 2012.2 需要 Visual Studio 2012 或 Visual Studio Express 2012 for Web。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET 和 Web 工具 2012.2 中的新增功能

本部分介绍已在 ASP.NET 和 Web 工具 2012.2 发行版中引入的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>工具

- Page Inspector 

    - 支持 JavaScript 选择映射允许 Page Inspector 将映射到页回发至相应的 JavaScript 代码动态添加的项。
    - 若要查看实时 CSS 更新功能。
    - 有关详细信息，请阅读[CSS 自动同步和在 Page Inspector 中的 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 编辑器 

    - 支持的 CoffeeScript、 Mustache、 Handlebars 和 JsRender 语法高亮显示。
    - HTML 编辑器提供 Intellisense 用于 Knockout 绑定。
    - 更少的编辑和编译器支持，以使构建动态 CSS 使用更少。
    - 将 JSON 粘贴为.NET 类。 使用此特殊粘贴命令可以将 JSON 粘贴到 C# 或 VB.NET 代码文件和 Visual Studio 将自动生成.NET 类从 JSON 这方面的推断。
- 移动版仿真器支持添加可扩展性挂钩，以便可作为 VSIX 安装第三方仿真程序。 安装仿真程序将显示在 F5 下拉列表中，这样开发人员可以预览自己的网站上的各种移动设备。 详细了解此功能的 Scott Hanselman 的博客文章[与 Visual Studio 的新 BrowserStack 集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 发布

- 网站项目现可包括发布到 Windows Azure 网站的 Web 应用程序项目相同的发布体验。
- 选择性发布&#8211;的一个或多个文件您可以执行以下操作 （在发布到 Web 部署终结点）： 

    - 发布选定的文件。
    - 请参阅本地文件和远程文件之间的差异。
    - 使用远程文件更新本地文件或使用本地文件更新远程文件。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 模板

- 新的 Facebook 应用程序模板使应用程序轻松编写 Facebook Canvas。 在几个简单步骤，可以创建一个 Facebook 应用程序，从已登录用户获取数据并与其好友集成。 该模板包含一个新的库中构建 Facebook 应用程序，包括身份验证、 权限、 访问 Facebook 数据等所涉及的所有基本功能，需要注意。 使用 Facebook 应用程序模板的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkID=269921 ](https://go.microsoft.com/fwlink/?LinkID=269921)。
- 新的单一页面应用程序 MVC 模板允许开发人员构建交互式客户端的 web 应用程序使用 HTML 5、 CSS 3 和常用的 Knockout 和 jQuery JavaScript 库，基于 ASP.NET Web API。 该模板包含一个"todo"列表应用程序，演示如何生成使用 RESTful 服务器 API 的 JavaScript HTML5 应用程序的常见做法。 您可以阅读详细信息，请[ https://www.asp.net/single-page-application ](../../../single-page-application/index.md)。
- 现在可以创建将新模板添加到 ASP.NET MVC 新项目对话框的 VSIX。 此处了解操作方法： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 包&#8211;的 MVC 项目模板已更新，以包括新的 FixedDisplayModes NuGet 包，其中包含 MVC 4 中的 bug 的解决方法。 有关包中包含的修补程序的详细信息，请参阅这篇博客文章 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) 从 MVC 团队。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 已得到增强几项新功能：

- ASP.NET Web API OData
- ASP.NET Web API 跟踪
- ASP.NET Web API 帮助页

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 提供任何数据源上构建具有丰富的业务逻辑的 OData 终结点所需的灵活性。 使用 ASP.NET Web API OData 您控制想要公开的 OData 语义的量。 ASP.NET Web API OData 随 ASP.NET MVC 4 项目模板，也可从 NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata))。

ASP.NET Web API OData 目前支持以下功能：

- 通过将 [Queryable] 特性应用支持 OData 查询语义。
- 轻松验证 OData 查询和限制的支持的查询选项、 运算符和函数集。
- 参数绑定到 ODataQueryOptions 直接以获取查询，然后可以验证并应用于 IQueryable 或 IEnumerable 的抽象语法树表示形式。
- 通过指定结果限制 [Queryable] 属性上启用服务驱动的分页和下一步页链接生成。
- 请求的匹配的资源使用 $inlinecount 总数的内联的计数。
- 控制 null 传播。
- 在 $ $filter 中的任何/所有运算符。
- 通过约定推断的实体数据模型或显式自定义的方式类似到 Entity Framework 代码优先模型。
- 公开实体集通过从 EntitySetController 派生。
- 用于公开导航属性、 操作的链接和实现 OData 操作的简单、 可自定义约定。
- 简化使用 MapODataRoute 扩展方法进行路由。
- 通过公开多个 EDM 模型的版本控制支持。
- 为 Web API 公开服务文档和 $metadata 以便可以生成客户端 （.NET、 Windows Phone、 Windows 应用商店等）。
- 支持 OData Atom、 JSON 和 JSON 详细格式。
- 创建、 更新、 部分更新 (PATCH) 和删除实体。
- 查询和操作实体之间的关系。
- 创建将与你的路由的关系链接。
- 复杂类型。
- 实体类型继承。
- 集合属性。
- 枚举。
- OData 操作。
- 为 WCF 数据服务，即 ODataLib 的同一个基础之上构建 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata))。

ASP.NET Web API OData 的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkId=271141 ](https://go.microsoft.com/fwlink/?LinkId=271141)。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 跟踪

ASP.NET Web API 跟踪.NET 跟踪与集成，从你的 web Api 的跟踪数据。 它现在是默认情况下，Web API 项目模板中启用。 跟踪数据的 web Api 发送到输出窗口和可通过 IntelliTrace。 ASP.NET Web API 跟踪的跟踪信息时通过使用集成 Windows Azure 上托管 Web API 使你[Windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)。 此外可以安装并启用 ASP.NET Web API 跟踪在任何应用程序中使用 ASP.NET Web API 跟踪的 NuGet 包 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing))。

有关配置和使用 ASP.NET Web API 跟踪的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkID=269874 ](https://go.microsoft.com/fwlink/?LinkID=269874)。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 帮助页

默认情况下，在 Web API 项目模板现在包含 ASP.NET Web API 帮助页。 ASP.NET Web API 帮助页会自动生成 web Api 包括 HTTP 终结点、 支持的 HTTP 方法、 参数和示例请求和响应消息负载的文档。 从代码中的注释自动提取文档。 此外可以向使用 ASP.NET Web API 帮助页 NuGet 包的任何应用程序添加 ASP.NET Web API 帮助页 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage))。

有关详细信息的设置和自定义 ASP.NET Web API 帮助页，请参阅[ https://go.microsoft.com/fwlink/?LinkId=271140 ](https://go.microsoft.com/fwlink/?LinkId=271140)。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 简化了将实时 web 功能添加到 ASP.NET 应用程序，使用 Websocket，如果可用，并自动回退到其他技术时它不是。

使用 ASP.NET SignalR 的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkId=271271 ](https://go.microsoft.com/fwlink/?LinkId=271271)。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 友好 Url

ASP.NET FriendlyURLs 得非常简单的 web 窗体开发人员能够生成清除器查找 （而不使用.aspx 扩展名） 的 Url。 它需要的不配置少并可与现有 ASP.NET v4.0 应用程序。 FriendlyURLs 功能还使开发人员能够通过支持桌面和移动视图之间进行切换将移动设备的支持添加到其应用程序更加容易。

有关安装和使用 ASP.NET 友好 Url 的详细信息请参阅[ http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx ](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

本部分介绍的已知的问题和 ASP.NET 和 Web Tools 2012.2 版本中的重大更改。

### <a name="installation-issues"></a>安装问题

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>无序的 Visual Studio 2012 安装

安装 ASP.NET 和 Web Tools 2012.2 将需要修复操作后，请安装其他 SKU 的 Visual Studio 2012。 请考虑以下序列：

1. 安装 Visual Studio 2012 Express for Web
2. 安装 ASP.NET 和 Web 工具 2012.2
3. 安装 Visual Studio 2012 Professional、 Premium 或 Ultimate

步骤 2，结果只能为 Express for Web 安装更新。 若要确保在步骤 3 期间安装的其他 SKU 包含更新将需要修复 ASP.NET 和 Web Tools 2012.2，若要安装的最后一个 SKU 安装更新。 如果在步骤 1 中的 Sku 和 3 都将被恢复也适用。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>打开 Visual Studio 时安装 Microsoft ASP.NET 和 Web 工具 2012.2

如果在安装 Microsoft ASP.NET 和 Web Tools 2012.2 的过程，VS 处于打开状态，Visual Studio 可能会处于错误状态。 建议用户关闭再继续安装 Visual Studio 的所有实例。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>取消 ASP.NET 和 Web Tools 2012.2 安装程序安装的过程

取消 ASP.NET 和 Web Tools 2012.2 安装程序安装的过程将使 Visual Studio 处于错误状态。 若要解决此问题，请执行以下步骤： 

- 转到添加/删除程序
- 如果存在，请卸载 Microsoft ASP.NET 和 Web Tools 2012.2。
- 重新安装 Microsoft ASP.NET 和 Web 工具 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>卸载 ASP.NET 和 Web Tools 2012.2 ASP.NET MVC 4 后模板和 Razor v2 网站模板是缺失

卸载 ASP.NET 和 Web Tools 2012.2 将也卸载所有的 ASP.NET MVC 4 和 Razor v2 网站模板从 Visual Studio 2012。

解决方法是修复 Visual Studio 2012 安装重新安装 ASP.NET MVC 4 和 Razor v2 网站模板。

### <a name="tooling-issues"></a>工具问题

#### <a name="nuget-error-reported-during-project-creation"></a>NuGet 会在项目创建期间报告错误

安装 ASP.NET 和 Web Tools 2012.2 后您可能会看到以下错误时创建的 MVC 4 项目

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET 和 Web Tools 2012.2 提供 NuGet 2.1，并将升级 Visual Studio 2012 中的扩展。 在某些情况下，VSIX 安装程序将无法正确更新 VSIX。 以下步骤将允许你为解决此问题：

1. 以管理员身份启动 Visual Studio 2012
2. 转到工具-&gt;扩展和更新和卸载 NuGet。
3. 关闭 Visual Studio
4. 导航到 ASP.NET 和 Web Tools 2012.2 的安装文件夹：

    1. 适用于 Visual Studio 2012:**程序 Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**
    2. 有关 Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**
5. 双击 NuGet.Tools.vsix 重新安装 NuGet

### <a name="web-api-issues"></a>Web API 问题

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>分析 $filter 和日期时间文字中的问题

OData URI 分析器无法正确分析部分的日期时间文字。 例如，$filter = 开始 eq 日期时间"2012年-12-31T12:00 无法正确分析。 一种解决方法是使用完整文本，$filter = 开始 eq 日期时间"2012年-12-31T12:00:00。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 不支持不区分大小写的属性名称。

OData 并不支持 OData 查询和 odata 路径中不区分大小写的属性名称。 工作项，请参阅：

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果用户具有在 javascript 客户端和服务器端上的不同大小写，它们可能会遇到此问题。 此问题是 odata 协议中的设计。 但是，许多用户报告此问题。 若要解决此问题，用户必须更正它们在 URL 中的用例。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>默认 OData 路由约定不支持 POST/PUT 导航属性。

默认 OData 路由约定不支持 POST/PUT 导航属性。 请参见工作项[ http://aspnetwebstack.codeplex.com/workitem/366 ](http://aspnetwebstack.codeplex.com/workitem/366)。 我们缺少这种常用的默认约定规定。

若要解决此问题，用户需要扩展新的路由约定，以支持它。

### <a name="facebook-template-issues"></a>Facebook 模板问题

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 应用程序模板只能是使用.NET 4.5

必须在新建项目对话框，请参阅在 ASP.NET MVC 4 Facebook 应用程序模板中的 framework 下拉列表中选择.NET 4.5。

#### <a name="real-time-update-controller"></a>实时更新控制器

Facebook 应用程序模板允许用户轻松地创建 Web API 控制器，用于处理 facebook 实时更新。 如果你的开发计算机位于 NAT 后面，你的控制器可能无法工作而无需进一步网络配置。 有关详细信息，请参阅此处： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查询与 Facebook OAuth 参数的字符串值冲突

以下字段冲突与 Facebook OAuth 对话框的调用返回 URL。 不添加你自己的查询字符串值使用以下名称： 代码、 错误、 错误\_说明、 错误\_原因。

#### <a name="using-page-inspector-with-facebook-template"></a>使用 Facebook 模板中使用 Page Inspector

调试你的 Facebook 应用程序时，不能在 Visual Studio 2012 中使用 Page Inspector 功能。 Page Inspector 当前不支持 iframe。

### <a name="single-page-application-template-issues"></a>单页面应用程序模板问题

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>与 JQuery 1.9/Knockout 2.2.1 更新，运行默认 MVC SPA 项目中，新的 todo 项编辑时输入焦点事件是不正确处理。

与 JQuery 1.9/Knockout 2.2.1 更新，运行时默认 MVC SPA 项目，新的 todo 项编辑输入不再焦点返回到新的 todo 项编辑框新的 todo 项输入到 todo 列表后。

解决方法引用[ http://knockoutjs.com/documentation/hasfocus-binding.html ](http://knockoutjs.com/documentation/hasfocus-binding.html)，并对下面的示例代码进行类似的修补程序：

文件 todo.model.js  
 函数 todolist(data) 中，添加以下：  
 **self.isSelected = ko.observable(false);**

函数 todoList.prototype.addTodo 中，添加以下 blacked 的文本：  
 **self.isSelected(true);**  
 self.newTodoTitle(&quot;&quot;);

Index.cshtml 文件中，添加以下 blacked 的文本：  
 &lt;窗体数据绑定 =&quot;提交： addTodo&quot;&gt;  
 &lt;输入类 =&quot;addTodo&quot;类型 =&quot;文本&quot;数据绑定 =&quot;值： newTodoTitle，占位符: Type 此处以添加、 blurOnEnter： 为 true，则**hasfocus: isSelected**，事件: {模糊： addTodo}&quot; /&gt;  
 &lt;/form&gt;
