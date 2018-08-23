---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-21
title: 什么是 ASP.NET Web API 2.1 中的新增功能 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: b6721bba-38c8-48c4-acbf-274c1a34e817
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 6c5a73b95955663d76238e88009ca700f9ace010
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825249"
---
<a name="whats-new-in-aspnet-web-api-21"></a>什么是 ASP.NET Web API 2.1 中的新增功能
====================
by [Microsoft](https://github.com/microsoft)

本主题介绍什么是 ASP.NET Web API 2.1 的新增功能。

- [下载](#download)
- [文档](#documentation)
- [ASP.NET Web API 2.1 中的新增功能](#new-features)

    - [全局错误处理](#global-error)
    - [属性路由改进](#attribute-routing)
    - [帮助页的改进](#help-page)
    - [IgnoreRoute 支持](#ignoreroute)
    - [BSON 的媒体类型格式化程序](#bson)
    - [更好地支持异步筛选器](#async-filters)
    - [查询解析为客户端格式设置库](#query-parsing)
- [已知的问题和重大更改](#known-issues)
- [Bug 修复](#bug-fixes)

<a id="download"></a>
## <a name="download"></a>下载

运行时功能将发布为 NuGet 库中的 NuGet 包。 所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。 最新的 ASP.NET Web API 2.1 RTM 包具有以下版本:"5.1.2"。 可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)。 此版本还包括在 NuGet 上的相应本地化的包。

可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：

[!code-console[Main](whats-new-in-aspnet-web-api-21/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>文档

教程和有关 ASP.NET Web API 2.1 RTM 的其他信息是可通过 ASP.NET 网站 ([https://www.asp.net/web-api](../../index.md))。

<a id="new-features"></a>
## <a name="new-features-in-aspnet-web-api-21"></a>ASP.NET Web API 2.1 中的新增功能

<a id="global-error"></a>
### <a name="global-error-handling"></a>全局错误处理

现在可以通过一个中央机制，记录所有未经处理的异常，可以自定义的未经处理的异常行为。

该框架支持多个异常记录器，其所有未经处理的异常并在其中它发生，例如，在时间处理的请求的上下文相关信息请参阅。

例如，以下代码使用 System.Diagnostics.TraceSource 记录所有未经处理的异常：

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample2.cs)]

您还可以替换默认异常处理程序，以便您可以完全自定义当未经处理的异常时发送的 HTTP 响应消息时发生。

我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt)，用于记录所有未经处理的异常，通过受欢迎的 ELMAH 框架。

<a id="attribute-routing"></a>
### <a name="attribute-routing-improvements"></a>属性路由改进

属性路由现在支持约束，启用版本控制和基于标头的路由选择。 此外，现可通过自定义属性路由的许多方面**IDirectRouteFactory**接口并**RouteFactoryAttribute**类。 路由前缀现在是通过可扩展**IRoutePrefix**接口并**RoutePrefixAttribute**类。

我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt)，它使用约束 api 版本 HTTP 标头进行动态筛选控制器。

<a id="help-page"></a>
### <a name="help-page-improvements"></a>帮助页的改进

Web API 2.1 包括以下增强功能[API 帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):

- 参数或返回类型的操作的各个属性的文档。
- 数据模型注释的文档。

帮助页的 UI 设计也已更新，为适应这些变化。

<a id="ignoreroute"></a>
### <a name="ignoreroute-support"></a>IgnoreRoute 支持

Web API 2.1 支持忽略在 Web API 路由中，通过一系列 URL 模式**IgnoreRoute**上的扩展方法**HttpRouteCollection**。 这些方法会导致 Web API 忽略匹配指定的模板，任何 Url，并允许应用附加处理，如果相应的主机。

下面的示例将忽略以开头的 Uri&quot;内容&quot;段：

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample3.cs)]

<a id="bson"></a>
### <a name="bson-media-type-formatter"></a>BSON 的媒体类型格式化程序

Web API 现在支持[BSON](http://bsonspec.org/)连网格式，客户端和服务器。

若要启用服务器端 BSON，添加**BsonMediaTypeFormatter**到格式化程序集合：

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample4.cs)]

下面是如何将.NET 客户端可以使用 BSON 格式：

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample5.cs)]

我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt)显示客户端和服务器端。

有关详细信息，请参阅[中 Web API 2.1 对 BSON 的支持](../formats-and-model-binding/bson-support-in-web-api-21.md)

<a id="async-filters"></a>
### <a name="better-support-for-async-filters"></a>更好地支持异步筛选器

Web API 现在支持创建筛选器，以异步方式执行的简单方法。 此功能可为你的筛选器需要对其执行异步操作，例如一个数据库的访问权限。 以前，若要创建异步筛选器，您必须实现筛选器接口，因为筛选器基类仅公开同步方法。 现在，您可以重写虚拟`On*Async`方法筛选器的基类。

例如：

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample6.cs)]

**AuthorizationFilterAttribute**， **ActionFilterAttribute**，并**ExceptionFilterAttribute**类都在 Web API 2.1 中支持异步。

<a id="query-parsing"></a>
### <a name="query-parsing-for-the-client-formatting-library"></a>查询解析为客户端格式设置库

以前， **System.Net.Http.Formatting**支持分析和更新服务器端代码的 URI 查询但等效的可移植库缺少此功能。 在 Web API 2.1 中，客户端应用程序可轻松地分析，并更新查询字符串。

以下示例演示如何分析、 修改和生成 URI 的查询。 （的示例演示控制台应用程序为简单起见）。

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample7.cs)]

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

本部分介绍的已知的问题和 ASP.NET Web API 2.1 RTM 中的重大更改。

### <a name="attribute-routing"></a>属性路由

现在，属性路由的匹配项方面的多义性问题报告错误，而不是无需选择第一个匹配项。

禁止使用属性路由 *{controller}* 参数，并使用 *{action}* 操作上放置路由上的参数。 这些参数会很有可能会导致多义性。

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a>基架 MVC/Web API 插入具有 5.1 包结果尚不存在的项目中的那些 5.0 包中的项目

ASP.NET Web API 2.1 rtm 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。 它们使用以前版本的 ASP.NET 运行时包 (5.0.0.0)。 因此，ASP.NET 基架将安装以前版本 (5.0.0.0) 的所需的包，如果它们尚不在你项目中可用。 但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。

如果使用 ASP.NET 基架 Web API 2.1 或 ASP.NET MVC 5.1 更新包后的，请确保 Web API 和 MVC 的版本一致。

### <a name="type-renames"></a>类型重命名

从 RC 到 2.1 RTM 一些使用属性路由可扩展性的类型已重命名。

| 旧类型名称 (2.1 RC) | 新的类型名称 (2.1 RTM) |
| --- | --- |
| IDirectRouteProvider | IDirectRouteFactory |
| RouteProviderAttribute | RouteFactoryAttribute |
| DirectRouteProviderContext | DirectRouteFactoryContext |

### <a name="exception-filters-do-not-unwrap-aggregate-exceptions-thrown-in-async-actions"></a>异常筛选器不 unwrap 聚合中异步操作引发的异常

以前，如果引发了异步操作**AggregateException**，异常筛选器将解包该异常，并**OnException**会得到基本异常。 在 2.1 中，异常筛选器不会不解包，并**OnException**获取原始**AggregateException**。

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a>Bug 修复

此版本还包括多项 bug 修复。 您可以找到完整的列表：

- [5.1.0 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=Web%20API|Web%20API%20OData&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [5.1.1 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.1.1%20RTM&assignedTo=All&component=Web%20API&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

5.1.2 包包含 IntelliSense 更新，但任何 bug 修复。
