---
uid: mvc/overview/releases/mvc51-release-notes
title: 什么是 ASP.NET MVC 5.1 中的新增功能 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 9a83a058-9b01-48aa-acce-ec041e694567
msc.legacyurl: /mvc/overview/releases/mvc51-release-notes
msc.type: authoredcontent
ms.openlocfilehash: d2e67f64e725e73c3bf9021295da3fe870079a45
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825643"
---
<a name="whats-new-in-aspnet-mvc-51"></a>什么是 ASP.NET MVC 5.1 中的新增功能
====================
by [Microsoft](https://github.com/microsoft)

本主题介绍什么是 ASP.NET Web MVC 5.1 的新增功能。

- [软件要求](#SoftwareRequirements)
- [下载](#download)
- [文档](#documentation)
- [ASP.NET MVC 5.1 中的新增功能](#new-features)

    - [属性路由改进](#AttributeRouting)
    - [Bootstrap 支持编辑器模板](#Bootstrap)
    - [在视图中的枚举支持](#Enum)
    - [对于 MinLength/MaxLength 属性的非介入式验证](#Unobtrusive)
    - [支持非介入式 Ajax 中的 this 上下文](#thisContext)
- [已知问题和重大更改](#KnownBreakingChanges)- [Bug 修复](#bug-fixes)

<a id="SoftwareRequirements"></a>
## <a name="software-requirements"></a>软件要求

- Visual Studio 2012： 下载[ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062)。
- Visual Studio 2013： 下载[Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=390064)。 编辑 ASP.NET MVC 5.1 Razor 视图时需要此更新。

<a id="download"></a>
## <a name="download"></a>下载

运行时功能将发布为 NuGet 库中的 NuGet 包。 所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。 最新的 ASP.NET MVC 5.1 RTM 包具有以下版本:"5.1.2"。 可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)。 此版本还包括在 NuGet 上的相应本地化的包。

可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：

[!code-console[Main](mvc51-release-notes/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>文档

教程和有关 ASP.NET MVC 5.1 RTM 的其他信息是可从 ASP.NET web 站点 ( https://www.asp.net)。 

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-51"></a>ASP.NET MVC 5.1 中的新增功能

<a id="AttributeRouting"></a>

### <a name="attribute-routing-improvements"></a>属性路由改进

 基于路由选择路由现在支持约束，启用版本控制和标头的属性。 现可通过自定义属性路由的许多方面`IDirectRouteFactory`接口和`RouteFactoryAttribute`类。 路由前缀现在是通过可扩展`IRoutePrefix`接口和`RoutePrefixAttribute`类。 

<a id="Enum"></a>

### <a name="enum-support-in-views"></a>在视图中的枚举支持

1. 新`@Html.EnumDropDownListFor()`帮助器方法。 应注意，该表达式的计算结果必须为的 HTML 帮助器最使用这些[enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx)类型或[Nullable&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx)其中`T`是[枚举](https://msdn.microsoft.com/en-us/library/cc138362.aspx)类型。 使用`EnumHelper.IsValidForEnumHelper()`以检查这些要求。
2. 新`EnumHelper.GetSelectList()`方法返回`IList<SelectListItem>`。 当您需要处理之前调用，例如，选择列表时，这是很有用`@Html.DropDownListFor()`，或当你希望显示的名称的`@Html.EnumDropDownListFor()`显示。

下面的代码显示了这些 Api。

[!code-cshtml[Main](mvc51-release-notes/samples/sample2.cshtml)]

您所见的完整示例[此处](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/)。

<a id="Bootstrap"></a>

### <a name="bootstrap-support-for-editor-templates"></a>Bootstrap 支持编辑器模板

我们现在允许在 HTML 属性中传递[EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx)作为[匿名对象](https://msdn.microsoft.com/en-us/library/bb397696.aspx)。

例如：

[!code-cshtml[Main](mvc51-release-notes/samples/sample3.cshtml)]

<a id="Unobtrusive"></a>

### <a name="unobtrusive-validation-for-minlengthattribute-and-maxlengthattribute"></a>非介入式验证 MinLengthAttribute 和 MaxLengthAttribute

将现在支持字符串和数组类型的客户端验证，有关使用属性修饰[MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx)并[MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx)属性。

<a id="thisContext"></a>

### <a name="supporting-the-this-context-in-unobtrusive-ajax"></a>支持非介入式 Ajax 中的 this 上下文

回调函数 (`OnBegin, OnComplete, OnFailure, OnSuccess`) 现在将能够找到调用元素通过`this`上下文。 例如：

[!code-html[Main](mvc51-release-notes/samples/sample4.html)]

<a id="KnownBreakingChanges"></a>

## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

### <a name="attribute-routing"></a>属性路由

方面属性路由的匹配项的多义性问题现在将报告错误，而不是无需选择第一个匹配项。

禁止使用属性路由`{controller}`参数，以及使用`{action}`操作上放置路由上的参数。 这些参数的用法很有可能会导致二义性。 

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a>基架 MVC/Web API 插入具有 5.1 包结果尚不存在的项目中的那些 5.0 包中的项目

有关 ASP.NET MVC 5.1 RTM 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。 它们使用以前版本的 ASP.NET 运行时包 (5.0.0.0)。 因此，ASP.NET 基架将安装以前版本 (5.0.0.0) 的所需的包，如果它们尚不在你项目中可用。 但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。 如果使用 ASP.NET 基架 Web API 2.1 或 ASP.NET MVC 5.1 更新你的项目的包后，请确保了一致的 Web API 和 ASP.NET MVC 版本。 

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a>语法突出显示的 Visual Studio 2013 中的 Razor 视图

如果您更新到 ASP.NET MVC 5.1 RTM 而不更新 Visual Studio 2013，你不会获得 Visual Studio 编辑器支持语法突出显示编辑 Razor 视图时。 您需要更新 Visual Studio 2013，若要获取此支持。 

### <a name="type-renames"></a>类型重命名

5.1 RTM 中重命名为某些使用属性路由可扩展性的类型。

| **旧类型名称 (5.1 RC)** | **新的类型名称 (5.1 RTM)** |
| --- | --- |
| IDirectRouteProvider | IDirectRouteFactory |
| RouteProviderAttribute | RouteFactoryAttribute |
| DirectRouteProviderContext | DirectRouteFactoryContext |

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a>Bug 修复

此版本还包括多项 bug 修复。 您可以找到完整的列表：

- [5.1.0 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [5.1.1 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.1.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

5.1.2 包包含 IntelliSense 更新，但任何 bug 修复。
