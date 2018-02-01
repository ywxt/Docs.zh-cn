---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-21
title: "ASP.NET Web API 2.1 的新增功能 |Microsoft 文档"
author: microsoft
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: b6721bba-38c8-48c4-acbf-274c1a34e817
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: cc5dc111d88cc7dae6a4a93203317fa0769d5427
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-web-api-21"></a><span data-ttu-id="b1919-102">ASP.NET Web API 2.1 的新增功能</span><span class="sxs-lookup"><span data-stu-id="b1919-102">What's New in ASP.NET Web API 2.1</span></span>
====================
<span data-ttu-id="b1919-103">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b1919-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="b1919-104">本主题介绍什么是用于 ASP.NET Web API 2.1 的新功能。</span><span class="sxs-lookup"><span data-stu-id="b1919-104">This topic describes what's new for ASP.NET Web API 2.1.</span></span>

- [<span data-ttu-id="b1919-105">下载</span><span class="sxs-lookup"><span data-stu-id="b1919-105">Download</span></span>](#download)
- [<span data-ttu-id="b1919-106">文档</span><span class="sxs-lookup"><span data-stu-id="b1919-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="b1919-107">ASP.NET Web API 2.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b1919-107">New Features in ASP.NET Web API 2.1</span></span>](#new-features)

    - [<span data-ttu-id="b1919-108">全局错误处理</span><span class="sxs-lookup"><span data-stu-id="b1919-108">Global Error Handling</span></span>](#global-error)
    - [<span data-ttu-id="b1919-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="b1919-109">Attribute Routing Improvements</span></span>](#attribute-routing)
    - [<span data-ttu-id="b1919-110">帮助页的改进</span><span class="sxs-lookup"><span data-stu-id="b1919-110">Help Page Improvements</span></span>](#help-page)
    - [<span data-ttu-id="b1919-111">IgnoreRoute 支持</span><span class="sxs-lookup"><span data-stu-id="b1919-111">IgnoreRoute Support</span></span>](#ignoreroute)
    - [<span data-ttu-id="b1919-112">BSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="b1919-112">BSON Media-Type Formatter</span></span>](#bson)
    - [<span data-ttu-id="b1919-113">更好地支持异步筛选器</span><span class="sxs-lookup"><span data-stu-id="b1919-113">Better Support for Async Filters</span></span>](#async-filters)
    - [<span data-ttu-id="b1919-114">查询分析格式库客户端</span><span class="sxs-lookup"><span data-stu-id="b1919-114">Query Parsing for the Client Formatting Library</span></span>](#query-parsing)
- [<span data-ttu-id="b1919-115">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="b1919-115">Known Issues and Breaking Changes</span></span>](#known-issues)
- [<span data-ttu-id="b1919-116">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b1919-116">Bug Fixes</span></span>](#bug-fixes)

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="b1919-117">下载</span><span class="sxs-lookup"><span data-stu-id="b1919-117">Download</span></span>

<span data-ttu-id="b1919-118">运行时功能将发布为 NuGet 库上的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b1919-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="b1919-119">所有运行时包按照[语义版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="b1919-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="b1919-120">最新的 ASP.NET Web API 2.1 RTM 包具有以下版本:"5.1.2"。</span><span class="sxs-lookup"><span data-stu-id="b1919-120">The latest ASP.NET Web API 2.1 RTM package has the following version: "5.1.2".</span></span> <span data-ttu-id="b1919-121">你可以安装或更新这些包通过[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)。</span><span class="sxs-lookup"><span data-stu-id="b1919-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/).</span></span> <span data-ttu-id="b1919-122">版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="b1919-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="b1919-123">你可以安装或使用 NuGet 程序包管理器控制台更新到已发布的 NuGet 程序包：</span><span class="sxs-lookup"><span data-stu-id="b1919-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](whats-new-in-aspnet-web-api-21/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="b1919-124">文档</span><span class="sxs-lookup"><span data-stu-id="b1919-124">Documentation</span></span>

<span data-ttu-id="b1919-125">教程和有关 ASP.NET Web API 2.1 RTM 的其他信息可以从 ASP.NET web 站点 ([https://www.asp.net/web-api](../../index.md))。</span><span class="sxs-lookup"><span data-stu-id="b1919-125">Tutorials and other information about ASP.NET Web API 2.1 RTM are available from the ASP.NET web site ([https://www.asp.net/web-api](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-web-api-21"></a><span data-ttu-id="b1919-126">ASP.NET Web API 2.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b1919-126">New Features in ASP.NET Web API 2.1</span></span>

<a id="global-error"></a>
### <a name="global-error-handling"></a><span data-ttu-id="b1919-127">全局错误处理</span><span class="sxs-lookup"><span data-stu-id="b1919-127">Global Error Handling</span></span>

<span data-ttu-id="b1919-128">未经处理的异常的行为可以自定义和通过一个中央机制，现在会记录所有未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="b1919-128">All unhandled exceptions can now be logged through one central mechanism, and the behavior for unhandled exceptions can be customized.</span></span>

<span data-ttu-id="b1919-129">框架支持多个异常记录器，全都请参阅的未经处理的异常和在其中发生，如时要处理的请求的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="b1919-129">The framework supports multiple exception loggers, which all see the unhandled exception and information about the context in which it occurred, such as the request being processed at the time.</span></span>

<span data-ttu-id="b1919-130">例如，下面的代码使用 System.Diagnostics.TraceSource 记录所有未经处理的异常：</span><span class="sxs-lookup"><span data-stu-id="b1919-130">For example, the following code uses System.Diagnostics.TraceSource to log all unhandled exceptions:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample2.cs)]

<span data-ttu-id="b1919-131">你也可以替换默认异常处理程序，以便你可以完全自定义当未经处理的异常时发送的 HTTP 响应消息时发生。</span><span class="sxs-lookup"><span data-stu-id="b1919-131">You can also replace the default exception handler, so that you can fully customize the HTTP response message that is sent when an unhandled exception occurs.</span></span>

<span data-ttu-id="b1919-132">我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt)记录所有未经处理的异常，通过流行的 ELMAH framework。</span><span class="sxs-lookup"><span data-stu-id="b1919-132">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/Elmah/ReadMe.txt) that logs all unhandled exceptions via the popular ELMAH framework.</span></span>

<a id="attribute-routing"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="b1919-133">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="b1919-133">Attribute Routing Improvements</span></span>

<span data-ttu-id="b1919-134">现在的属性路由支持约束，启用版本控制和基于标头的路由选择。</span><span class="sxs-lookup"><span data-stu-id="b1919-134">Attribute routing now supports constraints, enabling versioning and header-based route selection.</span></span> <span data-ttu-id="b1919-135">此外，许多方面的属性路由是现在可通过自定义**IDirectRouteFactory**接口和**RouteFactoryAttribute**类。</span><span class="sxs-lookup"><span data-stu-id="b1919-135">Also, many aspects of attribute routes are now customizable via the **IDirectRouteFactory** interface and **RouteFactoryAttribute** class.</span></span> <span data-ttu-id="b1919-136">路由前缀现在是可扩展的通过**IRoutePrefix**接口和**RoutePrefixAttribute**类。</span><span class="sxs-lookup"><span data-stu-id="b1919-136">The route prefix is now extensible via the **IRoutePrefix** interface and **RoutePrefixAttribute** class.</span></span>

<span data-ttu-id="b1919-137">我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt)，它使用约束动态筛选通过 api 版本 HTTP 标头的控制器。</span><span class="sxs-lookup"><span data-stu-id="b1919-137">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/RoutingConstraintsSample/ReadMe.txt) that uses constraints to dynamically filter controllers by an 'api-version' HTTP header.</span></span>

<a id="help-page"></a>
### <a name="help-page-improvements"></a><span data-ttu-id="b1919-138">帮助页的改进</span><span class="sxs-lookup"><span data-stu-id="b1919-138">Help Page Improvements</span></span>

<span data-ttu-id="b1919-139">Web API 2.1 包括以下增强功能到[API 帮助页](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):</span><span class="sxs-lookup"><span data-stu-id="b1919-139">Web API 2.1 includes the following enhancements to [API Help Pages](../getting-started-with-aspnet-web-api/creating-api-help-pages.md):</span></span>

- <span data-ttu-id="b1919-140">参数或返回类型的操作的各个属性的文档。</span><span class="sxs-lookup"><span data-stu-id="b1919-140">Documentation of individual properties of parameters or return types of actions.</span></span>
- <span data-ttu-id="b1919-141">数据模型批注的文档。</span><span class="sxs-lookup"><span data-stu-id="b1919-141">Documentation of data model annotations.</span></span>

<span data-ttu-id="b1919-142">帮助页的 UI 设计也已更新，以适应这些更改。</span><span class="sxs-lookup"><span data-stu-id="b1919-142">The UI design of the help pages was also updated, to accomodate these changes.</span></span>

<a id="ignoreroute"></a>
### <a name="ignoreroute-support"></a><span data-ttu-id="b1919-143">IgnoreRoute 支持</span><span class="sxs-lookup"><span data-stu-id="b1919-143">IgnoreRoute Support</span></span>

<span data-ttu-id="b1919-144">Web API 2.1 支持忽略 Web API 路由，通过一组中的 URL 模式**IgnoreRoute**上的扩展方法**HttpRouteCollection**。</span><span class="sxs-lookup"><span data-stu-id="b1919-144">Web API 2.1 supports ignoring URL patterns in Web API routing, through a set of **IgnoreRoute** extension methods on **HttpRouteCollection**.</span></span> <span data-ttu-id="b1919-145">这些方法会导致 Web API，若要忽略任何与匹配的指定的模板的 Url，使该主机可应用其他处理，如果适用。</span><span class="sxs-lookup"><span data-stu-id="b1919-145">These methods cause Web API to ignore any URLs that match a specified template, and allow the host to apply additional processing if appropriate.</span></span>

<span data-ttu-id="b1919-146">下面的示例将忽略以开头的 Uri&quot;内容&quot;段：</span><span class="sxs-lookup"><span data-stu-id="b1919-146">The following example ignores URIs that start with a &quot;content&quot; segment:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample3.cs)]

<a id="bson"></a>
### <a name="bson-media-type-formatter"></a><span data-ttu-id="b1919-147">BSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="b1919-147">BSON Media-Type Formatter</span></span>

<span data-ttu-id="b1919-148">Web API 现在支持[BSON](http://bsonspec.org/)连网格式，客户端和服务器。</span><span class="sxs-lookup"><span data-stu-id="b1919-148">Web API now supports the [BSON](http://bsonspec.org/) wire format, both on the client and on the server.</span></span>

<span data-ttu-id="b1919-149">若要在服务器端上启用 BSON，添加**BsonMediaTypeFormatter**到格式化程序集合：</span><span class="sxs-lookup"><span data-stu-id="b1919-149">To enable BSON on the server side, add the **BsonMediaTypeFormatter** to the formatters collection:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample4.cs)]

<span data-ttu-id="b1919-150">下面是如何.NET 客户端可以使用 BSON 格式：</span><span class="sxs-lookup"><span data-stu-id="b1919-150">Here is how a .NET client can consume BSON format:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample5.cs)]

<span data-ttu-id="b1919-151">我们提供了[示例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt)演示客户端和服务器端。</span><span class="sxs-lookup"><span data-stu-id="b1919-151">We have provided a [sample](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/ReadMe.txt) that shows both the client and server side.</span></span>

<span data-ttu-id="b1919-152">有关详细信息，请参阅[BSON 支持在 Web API 2.1](../formats-and-model-binding/bson-support-in-web-api-21.md)</span><span class="sxs-lookup"><span data-stu-id="b1919-152">For more information, see [BSON Support in Web API 2.1](../formats-and-model-binding/bson-support-in-web-api-21.md)</span></span>

<a id="async-filters"></a>
### <a name="better-support-for-async-filters"></a><span data-ttu-id="b1919-153">更好地支持异步筛选器</span><span class="sxs-lookup"><span data-stu-id="b1919-153">Better Support for Async Filters</span></span>

<span data-ttu-id="b1919-154">Web API 现在支持轻松创建异步执行的筛选器。</span><span class="sxs-lookup"><span data-stu-id="b1919-154">Web API now supports an easy way to create filters that execute asynchronously.</span></span> <span data-ttu-id="b1919-155">此功能是有用的是你的筛选器需要执行一个异步操作，例如数据库的访问。</span><span class="sxs-lookup"><span data-stu-id="b1919-155">This feature is useful is your filter needs to perform an async action, such as access a database.</span></span> <span data-ttu-id="b1919-156">以前，若要创建一个异步筛选器，你必须实现筛选器接口你自己，因为筛选器的基类仅公开同步方法。</span><span class="sxs-lookup"><span data-stu-id="b1919-156">Previously, to create an async filter, you had to implement the filter interface yourself, because the filter base classes only exposed synchronous methods.</span></span> <span data-ttu-id="b1919-157">现在你可以重写虚拟`On*Async`方法筛选器的基类。</span><span class="sxs-lookup"><span data-stu-id="b1919-157">Now you can override the virtual `On*Async` methods of the filter base class.</span></span>

<span data-ttu-id="b1919-158">例如: </span><span class="sxs-lookup"><span data-stu-id="b1919-158">For example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample6.cs)]

<span data-ttu-id="b1919-159">**AuthorizationFilterAttribute**， **ActionFilterAttribute**，和**ExceptionFilterAttribute**类都支持异步中 Web API 2.1。</span><span class="sxs-lookup"><span data-stu-id="b1919-159">The **AuthorizationFilterAttribute**, **ActionFilterAttribute**, and **ExceptionFilterAttribute** classes all support async in Web API 2.1.</span></span>

<a id="query-parsing"></a>
### <a name="query-parsing-for-the-client-formatting-library"></a><span data-ttu-id="b1919-160">查询分析格式库客户端</span><span class="sxs-lookup"><span data-stu-id="b1919-160">Query Parsing for the Client Formatting Library</span></span>

<span data-ttu-id="b1919-161">以前， **System.Net.Http.Formatting**支持分析和更新 URI 查询对于服务器端代码，但等效的可移植库缺少此功能。</span><span class="sxs-lookup"><span data-stu-id="b1919-161">Previously, **System.Net.Http.Formatting** supported parsing and updating URI queries for server-side code, but the equivalent portable library was missing this feature.</span></span> <span data-ttu-id="b1919-162">在 Web API 2.1 中，客户端应用程序可以现在轻松分析和更新查询字符串。</span><span class="sxs-lookup"><span data-stu-id="b1919-162">In Web API 2.1, a client application can now easily parse and update a query string.</span></span>

<span data-ttu-id="b1919-163">下面的示例演示如何分析、 修改和生成 URI 查询。</span><span class="sxs-lookup"><span data-stu-id="b1919-163">The following examples show how to parse, modify, and generate URI queries.</span></span> <span data-ttu-id="b1919-164">（示例中显示为简单起见一个控制台应用程序。）</span><span class="sxs-lookup"><span data-stu-id="b1919-164">(The examples show a console application for simplicity.)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-web-api-21/samples/sample7.cs)]

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="b1919-165">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="b1919-165">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="b1919-166">本部分介绍已知的问题和 ASP.NET Web API 2.1 RTM 中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="b1919-166">This section describes known issues and breaking changes in the ASP.NET Web API 2.1 RTM.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="b1919-167">属性路由</span><span class="sxs-lookup"><span data-stu-id="b1919-167">Attribute Routing</span></span>

<span data-ttu-id="b1919-168">在属性路由匹配项中的多义性现在还报告错误，而不是无需选择第一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="b1919-168">Ambiguities in attribute routing matches now report an error rather than choosing the first match.</span></span>

<span data-ttu-id="b1919-169">属性路由禁止使用*{controller}*参数，并从使用*{action}*路由的参数放置在操作上。</span><span class="sxs-lookup"><span data-stu-id="b1919-169">Attribute routes are prohibited from using the *{controller}* parameter, and from using the *{action}* parameter on routes placed on actions.</span></span> <span data-ttu-id="b1919-170">这些参数将很有可能会导致多义性。</span><span class="sxs-lookup"><span data-stu-id="b1919-170">These parameters would very likely cause ambiguities.</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="b1919-171">到 5.1 包在中使用结果尚不存在项目中的那些 5.0 包项目的基架 MVC/Web API</span><span class="sxs-lookup"><span data-stu-id="b1919-171">Scaffolding MVC/Web API into a project with 5.1 packages results in 5.0 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="b1919-172">在更新 NuGet 包适用于 ASP.NET Web API 2.1 RTM 不更新的 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="b1919-172">Updating NuGet packages for ASP.NET Web API 2.1 RTM does not update the Visual Studio tools, such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="b1919-173">它们使用以前版本的 ASP.NET 运行时包 (5.0.0.0)。</span><span class="sxs-lookup"><span data-stu-id="b1919-173">They use the previous version of the ASP.NET runtime packages (5.0.0.0).</span></span> <span data-ttu-id="b1919-174">因此，ASP.NET 基架将安装所需的包的以前版本 (5.0.0.0)，如果它们尚不存在在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="b1919-174">As a result, the ASP.NET scaffolding will install the previous version (5.0.0.0) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="b1919-175">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖你的项目中的最新包。</span><span class="sxs-lookup"><span data-stu-id="b1919-175">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span>

<span data-ttu-id="b1919-176">如果您使用 ASP.NET Web API 2.1 或 ASP.NET MVC 5.1 在更新包后的基架，请确保 Web API 和 MVC 的版本都一致。</span><span class="sxs-lookup"><span data-stu-id="b1919-176">If you use ASP.NET scaffolding after updating the packages to Web API 2.1 or ASP.NET MVC 5.1, make sure the versions of Web API and MVC are consistent.</span></span>

### <a name="type-renames"></a><span data-ttu-id="b1919-177">类型重命名</span><span class="sxs-lookup"><span data-stu-id="b1919-177">Type Renames</span></span>

<span data-ttu-id="b1919-178">从 RC 到 2.1 RTM 一些用于属性路由扩展的类型已重命名。</span><span class="sxs-lookup"><span data-stu-id="b1919-178">Some of the types used for attribute routing extensibility were renamed from the RC to the 2.1 RTM.</span></span>

| <span data-ttu-id="b1919-179">旧的类型名称 (2.1 RC)</span><span class="sxs-lookup"><span data-stu-id="b1919-179">Old type name (2.1 RC)</span></span> | <span data-ttu-id="b1919-180">新的类型名称 (2.1 RTM)</span><span class="sxs-lookup"><span data-stu-id="b1919-180">New Type Name (2.1 RTM)</span></span> |
| --- | --- |
| <span data-ttu-id="b1919-181">IDirectRouteProvider</span><span class="sxs-lookup"><span data-stu-id="b1919-181">IDirectRouteProvider</span></span> | <span data-ttu-id="b1919-182">IDirectRouteFactory</span><span class="sxs-lookup"><span data-stu-id="b1919-182">IDirectRouteFactory</span></span> |
| <span data-ttu-id="b1919-183">RouteProviderAttribute</span><span class="sxs-lookup"><span data-stu-id="b1919-183">RouteProviderAttribute</span></span> | <span data-ttu-id="b1919-184">RouteFactoryAttribute</span><span class="sxs-lookup"><span data-stu-id="b1919-184">RouteFactoryAttribute</span></span> |
| <span data-ttu-id="b1919-185">DirectRouteProviderContext</span><span class="sxs-lookup"><span data-stu-id="b1919-185">DirectRouteProviderContext</span></span> | <span data-ttu-id="b1919-186">DirectRouteFactoryContext</span><span class="sxs-lookup"><span data-stu-id="b1919-186">DirectRouteFactoryContext</span></span> |

### <a name="exception-filters-do-not-unwrap-aggregate-exceptions-thrown-in-async-actions"></a><span data-ttu-id="b1919-187">异常筛选器不 unwrap 聚合异步操作中引发的异常</span><span class="sxs-lookup"><span data-stu-id="b1919-187">Exception filters do not unwrap aggregate exceptions thrown in async actions</span></span>

<span data-ttu-id="b1919-188">以前，如果异步操作引发了**AggregateException**，异常筛选器将解包该异常，和**OnException**将获取使用基异常。</span><span class="sxs-lookup"><span data-stu-id="b1919-188">Previously, if an async action threw an **AggregateException**, an exception filter would unwrap the exception, and **OnException** would get the base exception.</span></span> <span data-ttu-id="b1919-189">在 2.1 中，异常筛选器不会不 unwrap，和**OnException**获取原始**AggregateException**。</span><span class="sxs-lookup"><span data-stu-id="b1919-189">In 2.1, the exception filter does not unwrap it, and **OnException** gets the original **AggregateException**.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a><span data-ttu-id="b1919-190">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b1919-190">Bug Fixes</span></span>

<span data-ttu-id="b1919-191">此版本还包括多项 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="b1919-191">This release also includes several bug fixes.</span></span> <span data-ttu-id="b1919-192">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="b1919-192">You can find the complete list here:</span></span>

- [<span data-ttu-id="b1919-193">5.1.0 包</span><span class="sxs-lookup"><span data-stu-id="b1919-193">5.1.0 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=Web%20API|Web%20API%20OData&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [<span data-ttu-id="b1919-194">5.1.1 包</span><span class="sxs-lookup"><span data-stu-id="b1919-194">5.1.1 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.1.1%20RTM&assignedTo=All&component=Web%20API&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<span data-ttu-id="b1919-195">5.1.2 包包含 IntelliSense 更新但没有 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="b1919-195">The 5.1.2 package contains IntelliSense updates but no bug fixes.</span></span>
