---
uid: mvc/overview/releases/whats-new-in-aspnet-mvc-52
title: 什么是 ASP.NET MVC 5.2 中的新增功能 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 97972587-2720-48b4-b158-f35f2e855fbf
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/releases/whats-new-in-aspnet-mvc-52
msc.type: authoredcontent
ms.openlocfilehash: bcffaa9fddfb13db0b7bd203029e850903a13a54
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389939"
---
<a name="whats-new-in-aspnet-mvc-52"></a>什么是 ASP.NET MVC 5.2 中的新增功能
====================
by [Microsoft](https://github.com/microsoft)

本主题介绍什么是 ASP.NET MVC 5.2 的新增功能[Microsoft.AspNet.MVC 5.2.2](#52)和[ASP.NET MVC 5.2.3、web Beta](#mvc523Beta)

- [软件要求](#softRequire)
- [下载](#download)
- [文档](#documentation)
- [在 ASP.NET MVC 5.2 的新增功能](#new-features)

    - [属性路由改进](#attributerouting)
- [已知的问题和重大更改](#knownbreakingchanges)
- [Bug 修复](#bug-fixes)
- [Microsoft.AspNet.MVC 5.2.2](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a>软件要求

- Visual Studio 2012： 下载[ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062)。
- Visual Studio 2013： 下载[Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064)或更高版本。 编辑 ASP.NET MVC 5.2 Razor 视图时需要此更新。

<a id="download"></a>
## <a name="download"></a>下载

运行时功能将发布为 NuGet 库中的 NuGet 包。 所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。 最新的 ASP.NET MVC 5.2 包具有以下版本:"5.2.0"。 可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)。 此版本还包括在 NuGet 上的相应本地化的包。

可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：

安装包 Microsoft.AspNet.Mvc-5.2.0 版

<a id="documentation"></a>
## <a name="documentation"></a>文档

教程和有关 ASP.NET MVC 5.2 的其他信息是可通过 ASP.NET 网站 ([https://www.asp.net/mvc](../../index.md))。

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a>在 ASP.NET MVC 5.2 的新增功能

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a>属性路由改进

属性路由现在提供了一个名为 IDirectRouteProvider，可完全控制如何发现和配置属性路由的扩展点。 IDirectRouteProvider 负责提供的操作和控制器以及关联的路由信息来指定这些操作需要何种路由配置的情况完全列表。 调用 MapAttributes/MapHttpAttributeRoutes 时，可能会指定 IDirectRouteProvider 实现。

自定义 IDirectRouteProvider 将是最简单通过扩展我们的默认实现，DefaultDirectRouteProvider。 此类提供了单独可重写虚拟方法，以更改用于发现属性、 创建路由项，以及发现路由前缀和区域前缀的逻辑。

具有新属性路由可扩展性的 IDirectRouteProvider，用户可以执行以下操作：

1. 支持的属性路由的继承。 例如，在以下方案博客和存储控制器使用由 BaseController 定义的属性路由约定。 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. 自动生成属性路由的路由的名称。 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. 修改路由前缀; 在一个中心位置，然后路由添加到路由表。
4. 筛选出你想要查找的属性路由的控制器。 我们希望很快 3 和 4 上的博客。

### <a name="facebook-fixes-for-changed-api-surface"></a>Facebook 修补程序已更改的 API 图面

MVC Facebook 包[已断开](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All)由于 Facebook 所做的一些 API 更改。 我们还发布了新的 Facebook 程序包 (Microsoft.AspNet.Facebook 1.0.0) 来解决这些问题。

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a>到具有 5.2.0 项目基架 MVC/Web API 包导致 5.1.2 打包以一种是在项目中尚不存在

为 ASP.NET MVC 5.2.0 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。 它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。 因此，ASP.NET 基架将安装以前版本 (例如 5.1.2 Update 2 中) 的所需的包，如果它们尚不在你项目中可用。 但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。 如果您使用 ASP.NET 基架 Web API 2.2 或 ASP.NET MVC 5.2 更新你的项目的包后，请确保了一致的 Web API 和 ASP.NET MVC 版本。

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a>Microsoft.jQuery.Unobtrusive.Validation NuGet 包安装失败，原因是找不到 Microsoft.jQuery.Unobtrusive.Validation 的版本兼容到 jQuery 1.4.1

Microsoft.jQuery.Unobtrusive.Validation 需要 jQuery &gt;= 1.8 和 jQuery.Validation &gt;= 1.8。 But,jQuery.Validation (1.8) 需要 jQuery (&#8805; 1.3.2 &amp; &amp; &#8804; 1.6)。 因此，当 NuGet 安装在同一时间，JQuery 1.8 和 jQuery.Validation 1.8 时就会失败。 如果出现此问题，则只需更新到 jQuery.Validation 版本&gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1)具有固定的 jQuery cap 首先，您应能够安装Microsoft.jQuery.Unobtrusive.Validation。

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a>Jquery。验证 nuget 包版本 1.13.0 不能识别某些国际电子邮件地址

jQuery.Validation nuget 包版本 1.11.1 是可以识别以下有效的电子邮件地址的最后一个已知的版本。 任何更高版本中可能不能识别它们。 例如：

电子邮件地址国际化 (EAI) 标准 (例如， [ &#29992; &#25143; @domain.com ](mailto:&#29992;&#25143;@domain.com))   
 EAI + 国际化资源标识符 (Iri) (例如。， [ &#29992; &#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;。&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))

在报告的问题 [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a>语法突出显示的 Visual Studio 2013 中的 Razor 视图

如果您更新到 ASP.NET MVC 5.2 而不更新 Visual Studio 2013，你不会获得 Visual Studio 编辑器支持语法突出显示编辑 Razor 视图时。 您需要更新 Visual Studio 2013，若要获取此支持。

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a>Bug 修复和细微的功能更新

此版本还包括几个 bug 修复和细微的功能更新。 您可以找到完整的列表：

- [5.2 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a>Microsoft.AspNet.MVC 5.2.2

此版本不包含在 MVC 中的新功能或 bug 修复。 我们所做[网页中更改](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx)显著的性能改进并随后更新了我们拥有依赖于此新版本的网页的所有依赖包。

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a>ASP.NET MVC 5.2.3、web Beta

你可以阅读发行[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。 此版本包含仅 bug 修复。 可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。
