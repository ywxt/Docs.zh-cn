---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 开发概述 |Microsoft Docs
author: rick-anderson
description: 本文档概述了有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能。
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 5c7aa95b18bc0a97f42cc981476c110830286fa5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829038"
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="66eb9-103">ASP.NET 4 和 Visual Studio 2010 Web 开发概述</span><span class="sxs-lookup"><span data-stu-id="66eb9-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>
====================
> <span data-ttu-id="66eb9-104">本文档概述了有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="66eb9-105">下载此白皮书</span><span class="sxs-lookup"><span data-stu-id="66eb9-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


<span data-ttu-id="66eb9-106">**内容**</span><span class="sxs-lookup"><span data-stu-id="66eb9-106">**Contents**</span></span>

<span data-ttu-id="66eb9-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="66eb9-108">Web.config 文件重构</span><span class="sxs-lookup"><span data-stu-id="66eb9-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="66eb9-109">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="66eb9-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="66eb9-110">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="66eb9-111">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="66eb9-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="66eb9-112">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="66eb9-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="66eb9-113">扩展该范围的允许的 Url</span><span class="sxs-lookup"><span data-stu-id="66eb9-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="66eb9-114">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="66eb9-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="66eb9-115">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="66eb9-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="66eb9-116">可扩展的 HTML、 URL 和编码的 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="66eb9-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="66eb9-117">在单个辅助进程中的单个应用程序的性能监视</span><span class="sxs-lookup"><span data-stu-id="66eb9-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="66eb9-118">Multi-Targeting</span><span class="sxs-lookup"><span data-stu-id="66eb9-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="66eb9-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="66eb9-120">使用 Web 窗体和 MVC 包含 jQuery</span><span class="sxs-lookup"><span data-stu-id="66eb9-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="66eb9-121">内容交付网络支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="66eb9-122">ScriptManager 显式脚本</span><span class="sxs-lookup"><span data-stu-id="66eb9-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="66eb9-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="66eb9-124">设置使用 Page.MetaKeywords 和 Page.MetaDescription 属性的 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="66eb9-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="66eb9-125">对单个控件启用视图状态</span><span class="sxs-lookup"><span data-stu-id="66eb9-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="66eb9-126">浏览器功能将变为</span><span class="sxs-lookup"><span data-stu-id="66eb9-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="66eb9-127">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="66eb9-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="66eb9-128">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="66eb9-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="66eb9-129">保持在数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="66eb9-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="66eb9-130">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="66eb9-131">用 QueryExtender 控件筛选数据</span><span class="sxs-lookup"><span data-stu-id="66eb9-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="66eb9-132">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="66eb9-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="66eb9-133">项目模板的更改</span><span class="sxs-lookup"><span data-stu-id="66eb9-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="66eb9-134">CSS 改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="66eb9-135">隐藏 div 元素周围隐藏字段</span><span class="sxs-lookup"><span data-stu-id="66eb9-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="66eb9-136">模板化控件的呈现外部表</span><span class="sxs-lookup"><span data-stu-id="66eb9-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="66eb9-137">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="66eb9-138">CheckBoxList 和 RadioButtonList 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="66eb9-139">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="66eb9-140">向导和 CreateUserWizard 控件 56</span><span class="sxs-lookup"><span data-stu-id="66eb9-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="66eb9-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="66eb9-142">区域支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="66eb9-143">数据注释属性验证支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="66eb9-144">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="66eb9-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="66eb9-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="66eb9-146">对于现有项目中启用动态数据</span><span class="sxs-lookup"><span data-stu-id="66eb9-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="66eb9-147">DynamicDataManager 控件声明性语法</span><span class="sxs-lookup"><span data-stu-id="66eb9-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="66eb9-148">实体模板</span><span class="sxs-lookup"><span data-stu-id="66eb9-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="66eb9-149">新的字段模板的 Url 和电子邮件地址</span><span class="sxs-lookup"><span data-stu-id="66eb9-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="66eb9-150">创建链接与 DynamicHyperLink 控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="66eb9-151">对数据模型中继承的支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="66eb9-152">对多对多关系 （仅适用于实体框架） 的支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="66eb9-153">新属性来控制显示和支持枚举</span><span class="sxs-lookup"><span data-stu-id="66eb9-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="66eb9-154">对筛选器的增强支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="66eb9-155">**[Visual Studio 2010 Web 开发改进](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="66eb9-156">CSS 兼容性得到改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="66eb9-157">HTML 和 JavaScript 代码段</span><span class="sxs-lookup"><span data-stu-id="66eb9-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="66eb9-158">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="66eb9-159">**[Web 应用程序部署使用 Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="66eb9-160">Web 打包</span><span class="sxs-lookup"><span data-stu-id="66eb9-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="66eb9-161">Web.config Transformation</span><span class="sxs-lookup"><span data-stu-id="66eb9-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="66eb9-162">数据库部署</span><span class="sxs-lookup"><span data-stu-id="66eb9-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="66eb9-163">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="66eb9-164">Resources</span><span class="sxs-lookup"><span data-stu-id="66eb9-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="66eb9-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="66eb9-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="66eb9-166">核心服务</span><span class="sxs-lookup"><span data-stu-id="66eb9-166">Core Services</span></span>

<span data-ttu-id="66eb9-167">ASP.NET 4 引入了许多的功能，可提高核心 ASP.NET 服务，如输出缓存和会话状态存储。</span><span class="sxs-lookup"><span data-stu-id="66eb9-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="66eb9-168">重构的 Web.config 文件</span><span class="sxs-lookup"><span data-stu-id="66eb9-168">Web.config File Refactoring</span></span>

<span data-ttu-id="66eb9-169">`Web.config`文件，其中包含配置为 Web 应用程序已增长得多在过去的几个版本的.NET framework 已添加新功能，如 Ajax，如路由，以及与 IIS 7 的集成。</span><span class="sxs-lookup"><span data-stu-id="66eb9-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="66eb9-170">这具有就很难配置或启动新的 Web 应用程序而无需 Visual Studio 之类的工具。</span><span class="sxs-lookup"><span data-stu-id="66eb9-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="66eb9-171">只 NET Framework 4，主要的配置元素已被移动到`machine.config`文件和应用程序现在将继承这些设置。</span><span class="sxs-lookup"><span data-stu-id="66eb9-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="66eb9-172">这允许`Web.config`ASP.NET 4 应用程序可以为空，或者包含仅的以下行，其指定 Visual Studio 的哪个版本的应用程序所面向的框架中的文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="66eb9-173">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="66eb9-173">Extensible Output Caching</span></span>

<span data-ttu-id="66eb9-174">自 ASP.NET 1.0 发布时，输出缓存已启用开发人员能够在内存中存储生成的页面、 控件和 HTTP 响应输出。</span><span class="sxs-lookup"><span data-stu-id="66eb9-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="66eb9-175">在后续的 Web 请求，ASP.NET 可以提供内容更快地通过检索生成的输出从内存而不是重新生成从零开始的输出。</span><span class="sxs-lookup"><span data-stu-id="66eb9-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="66eb9-176">但是，这种方法有一个限制，生成的内容始终具有要存储在内存中，并在遇到大量流量的服务器上，使用输出缓存的内存可以竞争与其它部分中的 Web 应用程序的内存要求。</span><span class="sxs-lookup"><span data-stu-id="66eb9-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="66eb9-177">ASP.NET 4 将添加一个扩展点为输出缓存，使你能够配置一个或多个自定义输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="66eb9-178">输出缓存提供程序可以使用任何存储机制来保持 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="66eb9-179">这就可以为不同的持久性机制，它可以包括本地或远程磁盘，云存储，创建自定义输出缓存提供程序和分布式缓存引擎。</span><span class="sxs-lookup"><span data-stu-id="66eb9-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="66eb9-180">作为派生新类创建自定义输出缓存提供程序*System.Web.Caching.OutputCacheProvider*类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="66eb9-181">然后，可以配置中的提供程序`Web.config`使用新的文件*提供程序*的子节*outputCache*元素，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="66eb9-182">默认情况下，在 ASP.NET 4 中，所有 HTTP 响应，呈现的页面和控件使用内存中输出缓存中，如下所示在上一示例中，其中*defaultProvider*属性设置为 AspNetInternalProvider。</span><span class="sxs-lookup"><span data-stu-id="66eb9-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="66eb9-183">你可以通过指定不同的提供程序名称的 Web 应用程序使用的默认输出缓存提供程序*defaultProvider*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="66eb9-184">此外，可以选择不同的输出缓存提供程序每个控件和每个请求。</span><span class="sxs-lookup"><span data-stu-id="66eb9-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="66eb9-185">若要选择不同的 Web 用户控件的不同输出缓存提供程序的最简单方法是以声明方式使用新进行*providerName*属性中的控件指令，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="66eb9-186">指定的 HTTP 请求的不同的输出缓存提供程序需要更多工作。</span><span class="sxs-lookup"><span data-stu-id="66eb9-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="66eb9-187">而不是以声明方式指定提供程序，则重写的新*GetOuputCacheProviderName*中的方法`Global.asax`文件以编程方式指定要用于特定请求的提供程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="66eb9-188">下面的示例演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="66eb9-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="66eb9-189">通过添加到 ASP.NET 4 的输出缓存提供程序可扩展性，现在可以为您的网站追求更主动和更智能的输出缓存策略。</span><span class="sxs-lookup"><span data-stu-id="66eb9-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="66eb9-190">例如，现可以缓存页面在磁盘有较低流量时缓存在内存中，站点的"前 10 个"页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="66eb9-191">或者，您可以缓存呈现页中，每个不同的组合，但使用分布式的缓存，以便从前端 Web 服务器卸载的内存占用情况。</span><span class="sxs-lookup"><span data-stu-id="66eb9-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="66eb9-192">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="66eb9-193">某些 Web 应用程序需要加载大量数据或执行成本高昂的初始化处理就可为第一个请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="66eb9-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="66eb9-194">在 ASP.NET 的早期版本中，对于这些情况下您必须设计自定义方法"唤醒"ASP.NET 应用程序，然后运行过程中的初始化代码*应用程序\_负载*中的方法`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="66eb9-195">名为的新可伸缩性功能*自动启动*，直接地址提供了此方案的 ASP.NET 4 运行时在 Windows Server 2008 R2 上的 IIS 7.5 上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="66eb9-196">自动启动功能提供了启动应用程序池、 初始化 ASP.NET 应用程序，以及然后接受 HTTP 请求的控制的方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="66eb9-197">用于 IIS 7.5 的 IIS 应用程序预热模块</span><span class="sxs-lookup"><span data-stu-id="66eb9-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="66eb9-198">用于 IIS 7.5，IIS 团队已发布应用程序预热模块的第一个 beta 版测试的版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="66eb9-199">这样，您甚至比前面所述的应用程序正在预热。</span><span class="sxs-lookup"><span data-stu-id="66eb9-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="66eb9-200">而不是编写自定义代码，您指定资源的 Url 以 Web 应用程序接受来自网络的请求之前执行。</span><span class="sxs-lookup"><span data-stu-id="66eb9-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="66eb9-201">在 IIS 服务的启动期间发生此预热 (如果配置的 IIS 应用程序池*AlwaysRunning*) 和 IIS 工作进程回收时。</span><span class="sxs-lookup"><span data-stu-id="66eb9-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="66eb9-202">在回收，过程将继续旧的 IIS 工作进程，以执行请求，直到完全预热新生成的工作进程，以便应用程序出现任何中断或 unprimed 缓存导致的其他问题。</span><span class="sxs-lookup"><span data-stu-id="66eb9-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="66eb9-203">请注意，此模块的工作原理与任何版本的 ASP.NET 2.0 版开始。</span><span class="sxs-lookup"><span data-stu-id="66eb9-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="66eb9-204">有关详细信息，请参阅[应用程序预热](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="66eb9-205">有关演示如何使用预热功能的演练，请参阅[开始使用 IIS 7.5 应用程序预热模块](https://www.iis.net/learn/manage)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>


<span data-ttu-id="66eb9-206">若要使用自动启动功能，IIS 管理员设置了应用程序池在 IIS 7.5，通过使用中的以下配置为自动启动`applicationHost.config`文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="66eb9-207">由于单个应用程序池可以包含多个应用程序，指定单个应用程序通过使用中的以下配置为自动启动`applicationHost.config`文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="66eb9-208">IIS 7.5 的 IIS 7.5 服务器是冷启动或单个应用程序池被回收时，使用中的信息`applicationHost.config`文件以确定哪个 Web 应用程序都需要为自动启动。</span><span class="sxs-lookup"><span data-stu-id="66eb9-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="66eb9-209">对于每个应用程序标记为自动启动，IIS7.5 发送请求到 ASP.NET 4 中启动应用程序中的状态在此期间应用程序暂时不接受 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="66eb9-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="66eb9-210">当它处于此状态时，ASP.NET 实例定义的类型化*serviceAutoStartProvider*属性 （如在前面的示例所示） 并调用到其公共入口点。</span><span class="sxs-lookup"><span data-stu-id="66eb9-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="66eb9-211">使用必要的入口点中实现创建托管的自动启动类型*IProcessHostPreloadClient*接口，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="66eb9-212">在运行代码在初始化后*预加载*方法和方法返回时，ASP.NET 应用程序已准备好处理请求。</span><span class="sxs-lookup"><span data-stu-id="66eb9-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="66eb9-213">添加了对 IIS.5 和 ASP.NET 4 自动启动，您就具有有明确定义的执行成本高昂的应用程序初始化之前处理的第一个 HTTP 请求方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="66eb9-214">例如，可以使用新的自动启动功能初始化应用程序及然后指示应用程序已初始化并准备好接受 HTTP 流量负载均衡器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="66eb9-215">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="66eb9-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="66eb9-216">它是在 Web 应用程序随着时间推移，这可能会导致搜索引擎中的过时链接会累积移动页面和其他内容周围的常见做法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="66eb9-217">在 ASP.NET 中，开发人员具有传统上处理对旧 Url 的请求通过使用通过使用*Response.Redirect*方法以将请求转发到新 URL。</span><span class="sxs-lookup"><span data-stu-id="66eb9-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="66eb9-218">但是，*重定向*方法发出 HTTP 302 已找到 （临时重定向） 响应，这会导致额外的 HTTP 往返当用户尝试访问的旧 Url。</span><span class="sxs-lookup"><span data-stu-id="66eb9-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="66eb9-219">添加一个新的 ASP.NET 4 *RedirectPermanent*帮助器方法，可以方便地对问题 HTTP 301 已永久移动响应，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="66eb9-220">搜索引擎和其他识别永久重定向的用户代理将存储内容，它消除不必要的往返行程所做的临时重定向的浏览器与相关联的新 URL。</span><span class="sxs-lookup"><span data-stu-id="66eb9-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="66eb9-221">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="66eb9-221">Shrinking Session State</span></span>

<span data-ttu-id="66eb9-222">ASP.NET 提供的 Web 场中存储会话状态的两个默认选项： 调用的进程外会话状态服务器的会话状态提供程序和 Microsoft SQL Server 数据库中存储数据的会话状态提供程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="66eb9-223">由于这两个选项涉及存储 Web 应用程序的工作进程之外的状态信息，会话状态必须进行序列化之前将其发送到远程存储。</span><span class="sxs-lookup"><span data-stu-id="66eb9-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="66eb9-224">具体取决于多少开发人员将保存在会话状态的信息，序列化数据的大小可以变得很大。</span><span class="sxs-lookup"><span data-stu-id="66eb9-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="66eb9-225">ASP.NET 4 引入了新的压缩选项，这两种不同的进程外会话状态提供程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="66eb9-226">当*compressionEnabled*下面的示例中所示的配置选项设置为*true*，ASP.NET 将压缩 （和解压缩） 使用.NET Framework序列化的会话状态*System.IO.Compression.GZipStream*类。</span><span class="sxs-lookup"><span data-stu-id="66eb9-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="66eb9-227">通过将新属性的简单添加`Web.config`文件，具有 Web 服务器上的备用 CPU 周期的应用程序可以实现显著减小的大小的序列化会话状态数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="66eb9-228">扩展该范围允许 Url</span><span class="sxs-lookup"><span data-stu-id="66eb9-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="66eb9-229">ASP.NET 4 引入了新选项来扩展应用程序 Url 的大小。</span><span class="sxs-lookup"><span data-stu-id="66eb9-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="66eb9-230">ASP.NET 的早期版本约束为 260 个字符，NTFS 文件路径限制基于 URL 路径长度。</span><span class="sxs-lookup"><span data-stu-id="66eb9-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="66eb9-231">在 ASP.NET 4 中，您可以选择增加 （或减少） 根据您的应用程序，此限制使用两个新*httpRuntime*配置特性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="66eb9-232">下面的示例显示了这些新属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="66eb9-233">若要允许较长或更短路径 （不包括协议、 服务器名称和查询字符串的 URL 的部分），请修改*[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="66eb9-234">若要允许较长或更短的查询字符串，请修改的值*[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="66eb9-235">ASP.NET 4 还可配置的 URL 字符检查使用的字符。</span><span class="sxs-lookup"><span data-stu-id="66eb9-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="66eb9-236">在 ASP.NET 中 URL 的路径部分找到无效的字符，它将拒绝该请求，并发出 HTTP 400 错误。</span><span class="sxs-lookup"><span data-stu-id="66eb9-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="66eb9-237">在以前版本的 ASP.NET 中，URL 字符检查的限制为一组固定的字符。</span><span class="sxs-lookup"><span data-stu-id="66eb9-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="66eb9-238">在 ASP.NET 4 中，你可以自定义使用新的有效字符集*requestPathInvalidChars*的属性*httpRuntime*配置元素，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidChars* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="66eb9-239">默认情况下<em>requestPathInvalidChars</em>属性定义为无效的八个字符。</span><span class="sxs-lookup"><span data-stu-id="66eb9-239">By default, the <em>requestPathInvalidChars</em> attribute defines eight characters as invalid.</span></span> <span data-ttu-id="66eb9-240">(分配给在字符串中<em>requestPathInvalidChars</em>默认情况下<em>，</em>小于 (&lt;)、 大于 (&gt;)，和 and 符 (&amp;) 字符编码的因为`Web.config`文件是一个 XML 文件。)根据需要可以自定义无效字符的组。</span><span class="sxs-lookup"><span data-stu-id="66eb9-240">(In the string that is assigned to <em>requestPathInvalidChars</em> by default<em>,</em>the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="66eb9-241">请注意，ASP.NET 4 始终拒绝包含 0x00 到 0x1F 的 ASCII 范围中的字符的 URL 路径，因为这些无效的 URL 字符中的 IETF RFC 2396 定义 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt))。</span><span class="sxs-lookup"><span data-stu-id="66eb9-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="66eb9-242">在 Windows Server 版本上运行 IIS 6 或更高版本，http.sys 协议设备驱动程序自动拒绝 Url 有了这些字符。</span><span class="sxs-lookup"><span data-stu-id="66eb9-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="66eb9-243">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="66eb9-243">Extensible Request Validation</span></span>

<span data-ttu-id="66eb9-244">ASP.NET 请求验证搜索字符串的常用的传入 HTTP 请求的数据中跨站点脚本 (XSS) 攻击。</span><span class="sxs-lookup"><span data-stu-id="66eb9-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="66eb9-245">如果找到潜在的 XSS 字符串，请求验证标记可疑字符串并返回错误。</span><span class="sxs-lookup"><span data-stu-id="66eb9-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="66eb9-246">仅当它找到的 XSS 攻击中使用的最常见字符串时，内置请求验证将返回错误。</span><span class="sxs-lookup"><span data-stu-id="66eb9-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="66eb9-247">此前在尝试进行 XSS 验证更为严格导致误报过多。</span><span class="sxs-lookup"><span data-stu-id="66eb9-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="66eb9-248">但是，客户可能希望更加严格，或反之可能想要有意放宽 XSS 请求验证检查的特定页面，或者为特定类型的请求。</span><span class="sxs-lookup"><span data-stu-id="66eb9-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="66eb9-249">在 ASP.NET 4 中，请求验证功能进行扩展，以便您可以使用自定义请求验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="66eb9-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="66eb9-250">若要扩展请求验证，您创建派生自新的类*System.Web.Util.RequestValidator*类型，，并配置应用程序 (在*httpRuntime* 部分`Web.config`文件) 以使用自定义的类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="66eb9-251">下面的示例演示如何配置自定义请求验证类：</span><span class="sxs-lookup"><span data-stu-id="66eb9-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="66eb9-252">新*requestValidationType*特性需要指定提供自定义请求验证的类的一个标准的.NET Framework 类型标识符字符串。</span><span class="sxs-lookup"><span data-stu-id="66eb9-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="66eb9-253">对于每个请求，ASP.NET 调用以处理每条传入 HTTP 请求数据的自定义类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="66eb9-254">入站 URL、 所有的 HTTP 标头 （cookie 和自定义标头），和的实体正文都可用于检查由自定义请求验证类在下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="66eb9-255">没有要检查传入的 HTTP 数据一段的情况下，请求验证类可以进行回退，让 ASP.NET 默认请求验证运行只需调用*基。IsValidRequestString。*</span><span class="sxs-lookup"><span data-stu-id="66eb9-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="66eb9-256">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="66eb9-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="66eb9-257">自首次发布以来 ASP.NET 就提供了强大的内存中对象缓存 (*System.Web.Caching.Cache*)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="66eb9-258">缓存实现已很常见，它具有非 Web 应用程序中已使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="66eb9-259">但是，很困难的 Windows 窗体或 WPF 应用程序，包括对引用`System.Web.dll`只是为了能够使用 ASP.NET 对象缓存。</span><span class="sxs-lookup"><span data-stu-id="66eb9-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="66eb9-260">若要使缓存可供所有应用程序，.NET Framework 4 引入了新的程序集、 新的命名空间、 某些基本类型和具体的缓存实现。</span><span class="sxs-lookup"><span data-stu-id="66eb9-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="66eb9-261">新`System.Runtime.Caching.dll`程序集包含在一个新的缓存 API *System.Runtime.Caching*命名空间。</span><span class="sxs-lookup"><span data-stu-id="66eb9-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="66eb9-262">该命名空间包含两个类的核心集：</span><span class="sxs-lookup"><span data-stu-id="66eb9-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="66eb9-263">为构建任何类型的自定义缓存实现提供了基础的抽象类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="66eb9-264">具体的内存中对象缓存实现 ( *system.runtime.caching.memorycache 有关的问题*类)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="66eb9-265">新*MemoryCache*类在 ASP.NET 缓存中，紧密地建模并共享大量的内部缓存引擎逻辑与 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="66eb9-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="66eb9-266">尽管在公共的缓存 Api *System.Runtime.Caching*已更新，以支持开发的自定义缓存，如果您用过 ASP.NET*缓存*对象，您会发现在熟悉的概念新的 Api。</span><span class="sxs-lookup"><span data-stu-id="66eb9-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="66eb9-267">新的深入讨论*MemoryCache*类和支持性的基础 Api 需要整个文档。</span><span class="sxs-lookup"><span data-stu-id="66eb9-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="66eb9-268">但是，下面的示例揭示了新的缓存 API 的工作原理。</span><span class="sxs-lookup"><span data-stu-id="66eb9-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="66eb9-269">该示例针对没有任何依赖项的 Windows 窗体应用程序的编写上`System.Web.dll`。</span><span class="sxs-lookup"><span data-stu-id="66eb9-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="66eb9-270">可扩展的 HTML、 URL 和编码的 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="66eb9-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="66eb9-271">在 ASP.NET 4 中，您可以创建以下常见文本编码任务的自定义编码例程：</span><span class="sxs-lookup"><span data-stu-id="66eb9-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="66eb9-272">HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="66eb9-272">HTML encoding.</span></span>
- <span data-ttu-id="66eb9-273">URL 编码。</span><span class="sxs-lookup"><span data-stu-id="66eb9-273">URL encoding.</span></span>
- <span data-ttu-id="66eb9-274">HTML 特性编码。</span><span class="sxs-lookup"><span data-stu-id="66eb9-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="66eb9-275">编码出站 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="66eb9-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="66eb9-276">可以通过从新派生来创建自定义编码器*System.Web.Util.HttpEncoder*类型，然后配置 ASP.NET 使用中的自定义类型*httpRuntime*一部分`Web.config`文件中，为以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="66eb9-277">配置自定义编码器后，ASP.NET 会自动调用自定义编码实现只要公共编码的方法*System.Web.HttpUtility*或*System.Web.HttpServerUtility*的类称为。</span><span class="sxs-lookup"><span data-stu-id="66eb9-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="66eb9-278">这允许创建自定义编码器实现主动字符编码，尽管 Web 开发团队的其余部分仍使用公共 ASP.NET 编码 Api 的 Web 开发团队的一个部分。</span><span class="sxs-lookup"><span data-stu-id="66eb9-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="66eb9-279">通过集中配置中的自定义编码器*httpRuntime*元素，可以保证从公共 ASP.NET 编码 Api 的所有文本编码呼叫都会都路由通过自定义编码器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="66eb9-280">在单个辅助进程中的单个应用程序的性能监视</span><span class="sxs-lookup"><span data-stu-id="66eb9-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="66eb9-281">为了提高的可以在一台服务器承载的网站的数量，很多宿主在单个辅助进程中运行多个 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="66eb9-282">但是，如果多个应用程序使用单个共享的辅助进程，很难服务器管理员可以确定单个应用程序出现了问题。</span><span class="sxs-lookup"><span data-stu-id="66eb9-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="66eb9-283">ASP.NET 4 利用由 CLR 引入的新资源监视功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="66eb9-284">若要启用此功能，可以添加到下面的 XML 配置片段`aspnet.config`配置文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="66eb9-285">请注意`aspnet.config`文件是在安装.NET Framework 的目录中。</span><span class="sxs-lookup"><span data-stu-id="66eb9-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="66eb9-286">它不是`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-286">It is not the `Web.config` file.</span></span>


<span data-ttu-id="66eb9-287">当*appDomainResourceMonitoring*启用功能，两个新的性能计数器可用于中的"ASP.NET 应用程序"性能类别：*托管处理器时间百分比*并*托管内存使用*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="66eb9-288">这两个这些性能计数器使用新的 CLR 应用程序域资源管理功能来跟踪估计的 CPU 时间和各个 ASP.NET 应用程序的托管的内存使用率。</span><span class="sxs-lookup"><span data-stu-id="66eb9-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="66eb9-289">因此，与 ASP.NET 4 中，管理员现在可以在单个辅助进程中运行的单个应用程序的资源消耗的更精细视图。</span><span class="sxs-lookup"><span data-stu-id="66eb9-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="66eb9-290">多目标</span><span class="sxs-lookup"><span data-stu-id="66eb9-290">Multi-Targeting</span></span>

<span data-ttu-id="66eb9-291">可以创建面向特定版本的.NET framework 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="66eb9-292">在 ASP.NET 4 中，在新的属性*编译*元素的`Web.config`文件允许您面向.NET Framework 4 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="66eb9-293">如果你明确指定目标.NET Framework 4 中，并且包含中的可选元素`Web.config`如的项的文件*system.codedom*，这些元素必须是正确的.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="66eb9-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="66eb9-294">(如果你不明确的目标.NET Framework 4，从中的条目缺乏推断的目标框架`Web.config`文件。)</span><span class="sxs-lookup"><span data-stu-id="66eb9-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="66eb9-295">下面的示例演示如何使用*targetFramework*属性中*编译*元素的`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="66eb9-296">请注意有关的目标.NET Framework 的特定版本的以下信息：</span><span class="sxs-lookup"><span data-stu-id="66eb9-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="66eb9-297">在.NET Framework 4 应用程序池中，ASP.NET 生成系统假定在.NET Framework 4 为目标如果`Web.config`文件不包括*targetFramework*属性或如果`Web.config`找不到文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="66eb9-298">（您可能需要对应用程序，使其运行.NET Framework 4 下进行编码更改。）</span><span class="sxs-lookup"><span data-stu-id="66eb9-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="66eb9-299">如果包括*targetFramework*属性，并且如果*system.codeDom*中定义元素`Web.config`文件，此文件必须针对.NET Framework 4 包含正确的条目。</span><span class="sxs-lookup"><span data-stu-id="66eb9-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="66eb9-300">如果使用的*aspnet\_编译器*命令将其预编译应用程序 （例如在生成环境），则必须使用正确版本的*aspnet\_编译器*目标框架的命令。</span><span class="sxs-lookup"><span data-stu-id="66eb9-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="66eb9-301">使用与.NET Framework 2.0 （%windir%\microsoft.net\framework\v2.0.50727) 随附的编译器进行编译的.NET Framework 3.5 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="66eb9-302">使用与.NET Framework 4 附带的编译器来编译创建的应用程序使用该框架或更高版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="66eb9-303">在运行时，编译器将使用的计算机安装的最新 framework 程序集 (并因此在 GAC 中)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="66eb9-304">如果对 framework 更高版本进行了更新 （例如，安装假设版本 4.1），你将能够即使在较新版本的 framework 中使用功能*targetFramework*属性以较低版本为目标（例如 4.0)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="66eb9-305">(但是，在 Visual Studio 2010，或者在使用中的设计时*aspnet\_编译器*命令时，使用 framework 的较新功能将导致编译器错误)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="66eb9-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="66eb9-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="66eb9-307">jQuery 与 Web 窗体和 MVC 包含</span><span class="sxs-lookup"><span data-stu-id="66eb9-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="66eb9-308">Web 窗体和 MVC 的 Visual Studio 模板包括开放源代码 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="66eb9-309">当您创建新网站或项目时，创建包含以下 3 个文件的脚本文件夹：</span><span class="sxs-lookup"><span data-stu-id="66eb9-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="66eb9-310">jQuery 1.4.1.js – 用户可读，unminified 的 jQuery 库的版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="66eb9-311">jQuery-14.1.min.js – 的缩小版 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="66eb9-312">jQuery-1.4.1-vsdoc.js – jQuery 库的 Intellisense 文档文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="66eb9-313">在开发的应用程序时包括 jQuery 的 unminified 的版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="66eb9-314">包括的缩小的版 jQuery 用于生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="66eb9-315">例如，以下 Web 窗体页说明了如何使用 jQuery，若要更改为黄色，当它们具有焦点时的 ASP.NET TextBox 控件的背景色。</span><span class="sxs-lookup"><span data-stu-id="66eb9-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="66eb9-316">内容交付网络支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-316">Content Delivery Network Support</span></span>

<span data-ttu-id="66eb9-317">Microsoft Ajax 内容交付网络 (CDN)，可轻松地将 ASP.NET Ajax 和 jQuery 脚本添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="66eb9-318">例如，可以开始使用 jQuery 库，只需通过添加`<script>`页指向 Ajax.microsoft.com 如下标记：</span><span class="sxs-lookup"><span data-stu-id="66eb9-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="66eb9-319">通过利用 Microsoft Ajax CDN，可以显著改进 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="66eb9-320">Microsoft Ajax CDN 的内容缓存在位于世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="66eb9-321">此外，Microsoft Ajax CDN 使浏览器可以位于不同域中的网站重用缓存的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="66eb9-322">Microsoft Ajax 内容交付网络支持 SSL (HTTPS)，以防您需要使用安全套接字层为网页提供服务。</span><span class="sxs-lookup"><span data-stu-id="66eb9-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="66eb9-323">当 CDN 不可用时，请实现回退。</span><span class="sxs-lookup"><span data-stu-id="66eb9-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="66eb9-324">测试回退。</span><span class="sxs-lookup"><span data-stu-id="66eb9-324">Test the fallback.</span></span>

<span data-ttu-id="66eb9-325">若要了解有关 Microsoft Ajax CDN 的详细信息，请访问以下网站：</span><span class="sxs-lookup"><span data-stu-id="66eb9-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="66eb9-326">ASP.NET ScriptManager 支持 Microsoft Ajax CDN。</span><span class="sxs-lookup"><span data-stu-id="66eb9-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="66eb9-327">只需通过设置一个属性，EnableCdn 属性，可以从 CDN 检索所有 ASP.NET 框架 JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="66eb9-328">将 EnableCdn 属性设置为值为 true 后，ASP.NET 框架将从 CDN 包括用于验证和 UpdatePanel 的所有 JavaScript 文件检索所有 ASP.NET 框架 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="66eb9-329">设置此属性可以对 web 应用程序的性能具有重大影响。</span><span class="sxs-lookup"><span data-stu-id="66eb9-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="66eb9-330">可以通过使用 WebResource 属性对 JavaScript 文件中设置的 CDN 路径。</span><span class="sxs-lookup"><span data-stu-id="66eb9-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="66eb9-331">新的 CdnPath 属性指定当 EnableCdn 属性设置为值为 true 时，使用 CDN 的路径：</span><span class="sxs-lookup"><span data-stu-id="66eb9-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="66eb9-332">ScriptManager 显式脚本</span><span class="sxs-lookup"><span data-stu-id="66eb9-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="66eb9-333">在过去，如果您使用过 ASP.NET ScriptManger 然后需要加载整个整体化 ASP.NET Ajax 库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="66eb9-334">通过利用新的 ScriptManager.AjaxFrameworkMode 属性，可以控制完全加载 ASP.NET Ajax 库的组件，并加载 ASP.NET Ajax 库所需的组件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="66eb9-335">ScriptManager.AjaxFrameworkMode 属性可以设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="66eb9-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="66eb9-336">已启用-指定 ScriptManager 控件自动包括 MicrosoftAjax.js 脚本文件，它是所有核心框架脚本 （旧版行为） 的合并的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="66eb9-337">禁用-指定所有 Microsoft Ajax 脚本功能将被都禁用，ScriptManager 控件不自动引用任何脚本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="66eb9-338">显式-指定将显式包含对页面所需的单独框架核心脚本文件的脚本引用，并确保将包含对每个脚本文件所需的依赖项的引用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="66eb9-339">例如，如果 AjaxFrameworkMode 属性设置为显式的值，然后可以指定所需的特定 ASP.NET Ajax 组件脚本：</span><span class="sxs-lookup"><span data-stu-id="66eb9-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="66eb9-340">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="66eb9-340">Web Forms</span></span>

<span data-ttu-id="66eb9-341">Web 窗体自 ASP.NET 1.0 发布以来已在 ASP.NET 中的核心功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="66eb9-342">在此区域中的 ASP.NET 4 中，其中包括了许多增强功能：</span><span class="sxs-lookup"><span data-stu-id="66eb9-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="66eb9-343">若要设置的功能*meta*标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="66eb9-344">更好地控制视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-344">More control over view state.</span></span>
- <span data-ttu-id="66eb9-345">可使用浏览器功能的更简单方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="66eb9-346">支持使用 ASP.NET Web 窗体路由。</span><span class="sxs-lookup"><span data-stu-id="66eb9-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="66eb9-347">更好地控制生成的 Id。</span><span class="sxs-lookup"><span data-stu-id="66eb9-347">More control over generated IDs.</span></span>
- <span data-ttu-id="66eb9-348">可以保存在数据控件中选定的行。</span><span class="sxs-lookup"><span data-stu-id="66eb9-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="66eb9-349">更好地控制中呈现的 HTML *FormView*并*ListView*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="66eb9-350">筛选数据源控件的支持。</span><span class="sxs-lookup"><span data-stu-id="66eb9-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="66eb9-351">设置使用 Page.MetaKeywords 和 Page.MetaDescription 属性的 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="66eb9-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="66eb9-352">ASP.NET 4 添加到两个属性*页上*类， *MetaKeywords*并*MetaDescription*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="66eb9-353">这两个属性表示对应*meta*标记在网页中，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="66eb9-354">这两个属性的工作方式相同的方式页*标题*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="66eb9-355">它们遵循以下规则：</span><span class="sxs-lookup"><span data-stu-id="66eb9-355">They follow these rules:</span></span>

1. <span data-ttu-id="66eb9-356">如果有没有*元*标记中*head*与属性名称相匹配的元素 (即命名 ="关键字" *Page.MetaKeywords*和名称 = "说明"*Page.MetaDescription*，不设置这些属性的含义)，则*元*标记将在呈现时添加到页面。</span><span class="sxs-lookup"><span data-stu-id="66eb9-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="66eb9-357">如果已有*meta*带这些名称的标记，这些属性的含义相同 get 和 set 方法的现有标记的内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="66eb9-358">可以在运行时，它可让你从数据库或其他源获取内容并允许您设置动态内容描述的标记中设置这些属性是特定页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="66eb9-359">您还可以设置*关键字*并*说明*中的属性 *@ Page*指令顶部的 Web 窗体页标记中，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="66eb9-360">这将重写*meta*标记已在页中声明的内容 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="66eb9-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="66eb9-361">说明的内容*meta*标记用于改善搜索列出 Google 中的预览。</span><span class="sxs-lookup"><span data-stu-id="66eb9-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="66eb9-362">(有关详细信息，请参阅[提高与元说明功能改进的代码段](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)Google 网站管理员中心博客上。)Google 和 Windows Live Search 不使用的关键字的内容的任何内容，但其他搜索引擎可能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="66eb9-363">有关详细信息，请参阅[Meta 关键字建议](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)搜索引擎指南网站上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="66eb9-364">这些新属性是一个简单的功能，但它们将保存您的要求，以将它们手动添加或编写你自己的代码创建*meta*标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="66eb9-365">对单个控件启用视图状态</span><span class="sxs-lookup"><span data-stu-id="66eb9-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="66eb9-366">默认情况下，页的页上的每个控件可能存储视图状态，即使它不是应用程序需要的结果与启用了视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="66eb9-367">视图状态数据包含在标记中，页面将生成并增大到客户端发送一个页面和回发所需的时间量。</span><span class="sxs-lookup"><span data-stu-id="66eb9-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="66eb9-368">存储不必要的更多视图状态可能会导致性能明显下降。</span><span class="sxs-lookup"><span data-stu-id="66eb9-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="66eb9-369">在 ASP.NET 的早期版本中，开发人员可以禁用单个控件的视图状态，以减少页面大小，但必须明确为单独的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="66eb9-370">在 ASP.NET 4 中，包括 Web 服务器控件*ViewStateMode*允许您默认情况下禁用视图状态，然后启用它仅用于需要在页中的控件的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="66eb9-371">*ViewStateMode*属性采用枚举具有三个值：*已启用*，*禁用*，以及*继承*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="66eb9-372">*已启用*启用视图状态的该控件和设置为任何子控件*继承*或有任何设置。</span><span class="sxs-lookup"><span data-stu-id="66eb9-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="66eb9-373">*已禁用*禁用视图状态，并*继承*指定该控件使用*ViewStateMode*设置从父控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="66eb9-374">下面的示例演示如何*ViewStateMode*属性工作原理。</span><span class="sxs-lookup"><span data-stu-id="66eb9-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="66eb9-375">标记和代码中的以下页面的控件包括的值*ViewStateMode*属性：</span><span class="sxs-lookup"><span data-stu-id="66eb9-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="66eb9-376">如您所见，代码将禁用 PlaceHolder1 控件的视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="66eb9-377">子 label1 控件继承此属性的值 (*Inherit*是默认值为*ViewStateMode*控件。)，从而节省没有视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="66eb9-378">PlaceHolder2 掌控*ViewStateMode*设置为*已启用*，因此 label2 继承此属性并保存视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="66eb9-379">在首次加载页面时*文本*属性均*标签*控件设置为字符串"[DynamicValue]"。</span><span class="sxs-lookup"><span data-stu-id="66eb9-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="66eb9-380">这些设置的效果是，如果页面可加载第一次，下面的输出将显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="66eb9-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="66eb9-381">已禁用 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="66eb9-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="66eb9-382">已启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="66eb9-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="66eb9-383">在回发后但是，将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="66eb9-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="66eb9-384">已禁用 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="66eb9-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="66eb9-385">已启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="66eb9-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="66eb9-386">Label1 控件 (其*ViewStateMode*值设置为*禁用*) 具有不会保留在代码中设置为它的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="66eb9-387">但是，label2 控制 (其*ViewStateMode*值设置为*已启用*) 已保留其状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="66eb9-388">您还可以设置*ViewStateMode*中 *@ Page*指令，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="66eb9-389">*页*类是只是另一个控件，它是作为页面中的所有其他控件的父控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="66eb9-390">默认值*ViewStateMode*是*已启用*有关的实例*页*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="66eb9-391">因为默认为控件*继承*，控件将继承*已启用*属性值，除非您设置*ViewStateMode*页或控制级别。</span><span class="sxs-lookup"><span data-stu-id="66eb9-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="66eb9-392">值*ViewStateMode*属性确定是否视图状态才*EnableViewState*属性设置为*true*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="66eb9-393">如果*EnableViewState*属性设置为*false*，将不保留视图状态即使*ViewStateMode*设置为*已启用*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="66eb9-394">此功能的良好用法是与*ContentPlaceHolder*主页面，可以在其中设置中的控件*ViewStateMode*到*禁用*主数据页上，然后启用它为单独*ContentPlaceHolder*又可以包含需要的控件的控件视图状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="66eb9-395">对浏览器功能的更改</span><span class="sxs-lookup"><span data-stu-id="66eb9-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="66eb9-396">ASP.NET 确定用户用于浏览您的站点通过使用名为的功能的浏览器的功能*浏览器功能*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="66eb9-397">浏览器功能由*HttpBrowserCapabilities*对象 (由公开*Request.Browser*属性)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="66eb9-398">例如，可以使用*HttpBrowserCapabilities*对象，以确定的类型和版本的当前浏览器是否支持 JavaScript 的特定版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="66eb9-399">或者，可以使用*HttpBrowserCapabilities*对象，以确定请求是否来自移动设备。</span><span class="sxs-lookup"><span data-stu-id="66eb9-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="66eb9-400">*HttpBrowserCapabilities*对象由一组的浏览器定义文件驱动。</span><span class="sxs-lookup"><span data-stu-id="66eb9-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="66eb9-401">这些文件包含特定的浏览器的功能信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="66eb9-402">在 ASP.NET 4 中，这些浏览器定义文件已更新为包含有关最近引入的浏览器和设备如 Google Chrome、 研究运动 BlackBerry 智能手机和 Apple iPhone 中的信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="66eb9-403">以下列表显示新的浏览器定义文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="66eb9-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-404">*blackberry.browser*</span></span>
- <span data-ttu-id="66eb9-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-405">*chrome.browser*</span></span>
- <span data-ttu-id="66eb9-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-406">*Default.browser*</span></span>
- <span data-ttu-id="66eb9-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-407">*firefox.browser*</span></span>
- <span data-ttu-id="66eb9-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-408">*gateway.browser*</span></span>
- <span data-ttu-id="66eb9-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-409">*generic.browser*</span></span>
- <span data-ttu-id="66eb9-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-410">*ie.browser*</span></span>
- <span data-ttu-id="66eb9-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-411">*iemobile.browser*</span></span>
- <span data-ttu-id="66eb9-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-412">*iphone.browser*</span></span>
- <span data-ttu-id="66eb9-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-413">*opera.browser*</span></span>
- <span data-ttu-id="66eb9-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="66eb9-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="66eb9-415">使用浏览器功能提供程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="66eb9-416">在 ASP.NET 3.5 版 Service Pack 1，您可以定义浏览器具有以下方面的功能：</span><span class="sxs-lookup"><span data-stu-id="66eb9-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="66eb9-417">在计算机级别中，创建或更新`.browser`以下文件夹中的 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="66eb9-418">定义的浏览器功能后，运行以下命令通过 Visual Studio 命令提示以重新生成浏览器功能程序集并将其添加到 gac 中：</span><span class="sxs-lookup"><span data-stu-id="66eb9-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="66eb9-419">对于单个应用程序，您创建`.browser`应用程序的文件中`App_Browsers`文件夹。</span><span class="sxs-lookup"><span data-stu-id="66eb9-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="66eb9-420">这些方法需要您更改 XML 文件和计算机级别的更改，必须重新启动该应用程序后运行 aspnet\_regbrowsers.exe 过程。</span><span class="sxs-lookup"><span data-stu-id="66eb9-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="66eb9-421">ASP.NET 4 包含一项功能称为*浏览器功能提供程序*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="66eb9-422">顾名思义，此，你可以生成一个提供程序，进而使你可以使用你自己的代码来确定浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="66eb9-423">在实践中，开发人员通常不定义自定义浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="66eb9-424">浏览器文件会进行硬若要更新，该过程相当复杂，对它们进行更新为和的 XML 语法的`.browser`文件可以是复杂，无法使用和定义。</span><span class="sxs-lookup"><span data-stu-id="66eb9-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="66eb9-425">什么会使此过程更加轻松是常见的浏览器定义语法，好像或一个包含最新的浏览器定义或甚至此类数据库的 Web 服务的数据库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="66eb9-426">新的浏览器功能提供程序功能使整个这些方案可能和实用，为第三方开发人员。</span><span class="sxs-lookup"><span data-stu-id="66eb9-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="66eb9-427">有两种主要方法使用新的 ASP.NET 4 浏览器功能提供程序功能： 扩展 ASP.NET 浏览器功能定义功能，或完全替换它。</span><span class="sxs-lookup"><span data-stu-id="66eb9-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="66eb9-428">以下各节首先介绍如何替换功能，以及如何对其进行扩展。</span><span class="sxs-lookup"><span data-stu-id="66eb9-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="66eb9-429">替换 ASP.NET 浏览器功能功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="66eb9-430">若要完全替换 ASP.NET 浏览器功能定义功能，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="66eb9-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="66eb9-431">创建提供程序类派生自*HttpCapabilitiesProvider*它将替代*GetBrowserCapabilities*方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="66eb9-432">此示例中的代码创建一个新*HttpBrowserCapabilities*对象，指定名为浏览器并将该功能设置为 MyCustomBrowser 功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="66eb9-433">将提供程序注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="66eb9-434">若要与应用程序使用提供程序，必须添加*提供程序*归于*browserCaps*主题中`Web.config`或`Machine.config`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="66eb9-435">(您还可以定义中的提供程序属性*位置*元素为应用程序，例如特定的移动设备的文件夹中的特定目录。)下面的示例演示如何设置*提供程序*配置文件中的属性：</span><span class="sxs-lookup"><span data-stu-id="66eb9-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="66eb9-436">若要注册新的浏览器功能定义的另一种方法是使用代码，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="66eb9-437">此代码必须在运行*应用程序\_启动*事件的`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="66eb9-438">将更改为任何*BrowserCapabilitiesProvider*之前执行该应用程序中的任何代码，以确保缓存保留在已解析的有效状态，必须执行类*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="66eb9-439">缓存 HttpBrowserCapabilities 对象</span><span class="sxs-lookup"><span data-stu-id="66eb9-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="66eb9-440">前面的示例中已有一个问题是这些代码将运行自定义提供程序调用以获取每次*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="66eb9-441">这可以在每个请求期间发生多次。</span><span class="sxs-lookup"><span data-stu-id="66eb9-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="66eb9-442">在示例中，提供程序的代码没有多大用处。</span><span class="sxs-lookup"><span data-stu-id="66eb9-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="66eb9-443">但是，如果自定义提供程序中的代码执行中的大量工作以便获得*HttpBrowserCapabilities*对象，这可能会影响性能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="66eb9-444">若要避免这种情况发生，可以缓存*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="66eb9-445">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="66eb9-445">Follow these steps:</span></span>

1. <span data-ttu-id="66eb9-446">创建派生的类*HttpCapabilitiesProvider*，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="66eb9-447">在示例中，代码通过调用自定义 BuildCacheKey 方法，生成的缓存键和此方法通过调用自定义 GetCacheTime 方法获取的缓存的时间长度。</span><span class="sxs-lookup"><span data-stu-id="66eb9-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="66eb9-448">然后代码将添加已解析*HttpBrowserCapabilities*到缓存的对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="66eb9-449">可以从缓存中检索和上重复使用该对象进行的后续请求使用的自定义提供程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="66eb9-450">将提供程序注册应用程序，如前面的过程中所述。</span><span class="sxs-lookup"><span data-stu-id="66eb9-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="66eb9-451">扩展 ASP.NET 浏览器功能的功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="66eb9-452">上一节介绍了如何创建一个新*HttpBrowserCapabilities* ASP.NET 4 中的对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="66eb9-453">此外可以通过将新的浏览器功能定义添加到已在 ASP.NET 中的那些扩展 ASP.NET 浏览器功能的功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="66eb9-454">您可以执行此操作而无需使用 XML 的浏览器定义。</span><span class="sxs-lookup"><span data-stu-id="66eb9-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="66eb9-455">下面的过程演示如何。</span><span class="sxs-lookup"><span data-stu-id="66eb9-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="66eb9-456">创建派生的类*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="66eb9-457">此代码首先使用 ASP.NET 浏览器功能功能来尝试找出在浏览器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="66eb9-458">但是，如果浏览器不确定基于在请求中定义的信息 (即，如果*浏览器*的属性*HttpBrowserCapabilities*对象是字符串"Unknown")，该代码调用自定义提供程序 (MyBrowserCapabilitiesEvaluator) 来标识浏览器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="66eb9-459">将提供程序注册应用程序，如前面的示例中所述。</span><span class="sxs-lookup"><span data-stu-id="66eb9-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="66eb9-460">通过将新功能添加到现有的功能定义扩展浏览器功能的功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="66eb9-461">除了创建自定义浏览器定义提供程序和动态地创建新的浏览器定义，您可以扩展现有的浏览器定义具有其他功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="66eb9-462">这允许您使用接近所需但缺少仅几项功能的定义。</span><span class="sxs-lookup"><span data-stu-id="66eb9-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="66eb9-463">为此，请执行下列步骤。</span><span class="sxs-lookup"><span data-stu-id="66eb9-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="66eb9-464">创建派生的类*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="66eb9-465">此代码示例扩展了现有的 ASP.NET *HttpCapabilitiesEvaluator*类，并获取*HttpBrowserCapabilities*与当前的请求定义通过使用以下代码相匹配的对象:</span><span class="sxs-lookup"><span data-stu-id="66eb9-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="66eb9-466">然后，代码可以添加或修改此浏览器的功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="66eb9-467">有两种方法来指定新的浏览器功能：</span><span class="sxs-lookup"><span data-stu-id="66eb9-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="66eb9-468">添加到的键/值对*IDictionary*对象，它由公开*功能*属性*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="66eb9-469">在上一示例中，该代码将添加一项功能的值创建名为多点触控 *，则返回 true*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="66eb9-470">设置的现有属性*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="66eb9-471">在上述示例中，代码会设置*帧*属性设置为*true*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="66eb9-472">此属性是只需访问器的*IDictionary*对象，它由公开*功能*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="66eb9-473">请注意此模型适用于的任何属性*HttpBrowserCapabilities*，包括控件适配器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="66eb9-474">将提供程序注册应用程序，如前面的过程中所述。</span><span class="sxs-lookup"><span data-stu-id="66eb9-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="66eb9-475">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="66eb9-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="66eb9-476">ASP.NET 4 添加了对使用 Web 窗体路由的内置支持。</span><span class="sxs-lookup"><span data-stu-id="66eb9-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="66eb9-477">路由可以配置为接受的应用程序请求不会映射到物理文件的 Url。</span><span class="sxs-lookup"><span data-stu-id="66eb9-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="66eb9-478">相反，您可以使用路由来定义，对用户有意义和，可帮助你的应用程序的搜索引擎搜索引擎优化 (SEO) 的 Url。</span><span class="sxs-lookup"><span data-stu-id="66eb9-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="66eb9-479">例如，用于显示产品类别中的现有应用程序的页面的 URL 可能如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="66eb9-480">通过使用路由，可以配置应用程序接受以下 URL 来呈现相同的信息：</span><span class="sxs-lookup"><span data-stu-id="66eb9-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="66eb9-481">路由已从 ASP.NET 3.5 SP1 开始提供。</span><span class="sxs-lookup"><span data-stu-id="66eb9-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="66eb9-482">(有关如何使用 ASP.NET 3.5 SP1 中的路由的示例，请参阅文章[路由使用与 WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "此项的标题。")</span><span class="sxs-lookup"><span data-stu-id="66eb9-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="66eb9-483">Phil Haack 的博客。）但是，ASP.NET 4 包括一些功能，使其更轻松地使用路由，其中包括：</span><span class="sxs-lookup"><span data-stu-id="66eb9-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="66eb9-484">*PageRouteHandler*类，该类是一个简单的 HTTP 处理程序定义的路由时所用的。</span><span class="sxs-lookup"><span data-stu-id="66eb9-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="66eb9-485">类将数据传递给请求路由到的页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="66eb9-486">新属性*HttpRequest.RequestContext*并*Page.RouteData* (即为代理*HttpRequest.RequestContext.RouteData*对象)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="66eb9-487">这些属性使其能够更轻松地从该路由传递的访问信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="66eb9-488">下面的新表达式构建器中定义*System.Web.Compilation.RouteUrlExpressionBuilder*并*System.Web.Compilation.RouteValueExpressionBuilder*:</span><span class="sxs-lookup"><span data-stu-id="66eb9-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="66eb9-489">*RouteUrl*，简单的方式来创建对应于 ASP.NET 服务器控件中的路由 URL 的 URL。</span><span class="sxs-lookup"><span data-stu-id="66eb9-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="66eb9-490">*RouteValue*，以简单的方式来提取从信息*RouteContext*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="66eb9-491">*RouteParameter*类，因此可以轻松地将数据包含在传递*RouteContext*针对数据源控件的查询的对象 (类似于[ *FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span><span class="sxs-lookup"><span data-stu-id="66eb9-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="66eb9-492">Web 窗体页的路由</span><span class="sxs-lookup"><span data-stu-id="66eb9-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="66eb9-493">下面的示例演示如何使用新的定义 Web 窗体路由*MapPageRoute*方法*路由*类：</span><span class="sxs-lookup"><span data-stu-id="66eb9-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="66eb9-494">ASP.NET 4 引入了*MapPageRoute*方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="66eb9-495">下面的示例等效于上一示例所示的 SearchRoute 定义，但使用*PageRouteHandler*类。</span><span class="sxs-lookup"><span data-stu-id="66eb9-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="66eb9-496">在示例中的代码映射到物理页的路由 (在第一个路由到`~/search.aspx`)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="66eb9-497">第一个路由定义还指定应从 URL 中提取并传递到页名为 searchterm 的参数。</span><span class="sxs-lookup"><span data-stu-id="66eb9-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="66eb9-498">*MapPageRoute*方法支持以下方法重载：</span><span class="sxs-lookup"><span data-stu-id="66eb9-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="66eb9-499">*MapPageRoute （字符串 routeName，字符串 routeUrl、 字符串 physicalFile，bool checkPhysicalUrlAccess）*</span><span class="sxs-lookup"><span data-stu-id="66eb9-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="66eb9-500">*MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值）*</span><span class="sxs-lookup"><span data-stu-id="66eb9-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="66eb9-501">*MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值、 RouteValueDictionary 约束）*</span><span class="sxs-lookup"><span data-stu-id="66eb9-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="66eb9-502">*CheckPhysicalUrlAccess*参数指定该路由是否应检查其路由到物理页的安全权限 (在本例中为 search.aspx) 以及对传入 URL 的权限 （在这种情况下，搜索/ {searchterm})。</span><span class="sxs-lookup"><span data-stu-id="66eb9-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="66eb9-503">如果的值*checkPhysicalUrlAccess*是*false*，将检查仅传入 URL 的权限。</span><span class="sxs-lookup"><span data-stu-id="66eb9-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="66eb9-504">这些权限定义中`Web.config`文件中使用如下所示的设置：</span><span class="sxs-lookup"><span data-stu-id="66eb9-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="66eb9-505">在示例配置中，访问被拒绝到物理页`search.aspx`除了管理员角色中的所有用户。</span><span class="sxs-lookup"><span data-stu-id="66eb9-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="66eb9-506">当*checkPhysicalUrlAccess*参数设置为*true* （这是其默认值），只有管理员用户允许访问 URL /search/ {searchterm}，因为物理页 search.aspx 是限制为该角色中的用户。</span><span class="sxs-lookup"><span data-stu-id="66eb9-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="66eb9-507">如果*checkPhysicalUrlAccess*设置为*false*和站点配置为在前面的示例所示，将允许所有经过身份验证的用户访问 URL /search/ {searchterm}。</span><span class="sxs-lookup"><span data-stu-id="66eb9-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="66eb9-508">读取 Web 窗体页中的路由信息</span><span class="sxs-lookup"><span data-stu-id="66eb9-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="66eb9-509">在 Web 窗体物理页的代码中，您可以访问路由已从 URL 中提取的信息 (或另一个对象已添加到其他信息*RouteData*对象) 通过使用两个新属性： *HttpRequest.RequestContext*并*Page.RouteData*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="66eb9-510">(*Page.RouteData*包装*HttpRequest.RequestContext.RouteData*。)下面的示例演示如何使用*Page.RouteData*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="66eb9-511">代码将提取如前面的示例路由中定义为 searchterm 参数中，传递的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="66eb9-512">请考虑以下请求 URL:</span><span class="sxs-lookup"><span data-stu-id="66eb9-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="66eb9-513">发出此请求时，会在呈现"scott"一词`search.aspx`页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="66eb9-514">访问标记中的路由信息</span><span class="sxs-lookup"><span data-stu-id="66eb9-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="66eb9-515">在上一部分中所述的方法演示如何在 Web 窗体页中的代码中获取路由数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="66eb9-516">此外可以使用相同的信息让你访问在标记中的表达式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="66eb9-517">表达式生成器是一种功能强大、 巧妙的方法，以使用声明性代码。</span><span class="sxs-lookup"><span data-stu-id="66eb9-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="66eb9-518">(有关详细信息，请参阅文章[Express 自己的自定义表达式生成器](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)Phil Haack 的博客上。)</span><span class="sxs-lookup"><span data-stu-id="66eb9-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="66eb9-519">ASP.NET 4 包括两个新的表达式生成器的 Web 窗体路由。</span><span class="sxs-lookup"><span data-stu-id="66eb9-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="66eb9-520">下面的示例演示如何使用它们。</span><span class="sxs-lookup"><span data-stu-id="66eb9-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="66eb9-521">在示例中， *RouteUrl*表达式用于定义根据路由参数的 URL。</span><span class="sxs-lookup"><span data-stu-id="66eb9-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="66eb9-522">这使您不必将硬编码到标记中，完整的 URL，并允许您更改 URL 结构更高版本而无需对此链接的任何更改。</span><span class="sxs-lookup"><span data-stu-id="66eb9-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="66eb9-523">根据前面定义的路由，此标记将生成以下 URL:</span><span class="sxs-lookup"><span data-stu-id="66eb9-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="66eb9-524">ASP.NET 会自动制定正确的路由 （即，它生成正确的 URL） 根据输入参数。</span><span class="sxs-lookup"><span data-stu-id="66eb9-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="66eb9-525">此外可以在表达式中，从中可以指定要使用的路由包含路由名称。</span><span class="sxs-lookup"><span data-stu-id="66eb9-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="66eb9-526">下面的示例演示如何使用*RouteValue*表达式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="66eb9-527">包含此控件的页的运行时，标签中显示"scott"的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="66eb9-528">*RouteValue*表达式可以轻松地在标记中，使用路由数据和它避免了必须使用更复杂的 Page.RouteData["x"] 在标记中的语法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="66eb9-529">使用路由数据的数据源控件参数</span><span class="sxs-lookup"><span data-stu-id="66eb9-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="66eb9-530">*RouteParameter*类，可以指定作为数据源控件中的查询参数值的路由数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="66eb9-531">它[工作方式非常类似于](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)类，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="66eb9-532">在这种情况下，路由参数 searchterm 的值将用于@companyname中的参数<em>选择</em>语句。</span><span class="sxs-lookup"><span data-stu-id="66eb9-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the <em>Select</em> statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="66eb9-533">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="66eb9-533">Setting Client IDs</span></span>

<span data-ttu-id="66eb9-534">新*ClientIDMode*属性，解决了长期存在的问题在 ASP.NET 中，即如何控件创建*id*所呈现元素的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="66eb9-535">知道*id*呈现元素的属性是重要信息： 如果你的应用程序包括在引用这些元素的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="66eb9-536">*Id*中为 Web 服务器控件呈现的 HTML 属性基于生成*ClientID*控件的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="66eb9-537">ASP.NET 4 中，用于生成算法直到*id*属性从*ClientID*属性已连接的命名容器 （如果有） 的 id，并在重复 （作为中控件的情况下数据控件），添加一个前缀和一个顺序号。</span><span class="sxs-lookup"><span data-stu-id="66eb9-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="66eb9-538">尽管这始终有保证的页面中控件 Id 是唯一，该算法导致控件不是可预测，并且因此非常难以为客户端脚本中引用的 Id。</span><span class="sxs-lookup"><span data-stu-id="66eb9-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="66eb9-539">新*ClientIDMode*属性，可以指定更准确地说如何的客户端 ID 生成的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="66eb9-540">可以设置*ClientIDMode*任何控件，包括页面的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="66eb9-541">可能的设置如下所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-541">Possible settings are the following:</span></span>

- <span data-ttu-id="66eb9-542">*AutoID* – 这是等效于用于生成算法*ClientID* ASP.NET 的早期版本中使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="66eb9-543">*静态*– 此步骤指定*ClientID*值将为无需连接的父命名容器的 Id 的 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="66eb9-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="66eb9-544">这可以是 Web 用户控件中很有用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="66eb9-545">由于 Web 用户控件可能位于不同页上和在不同的容器控件中，可能难以使用的控件的客户端脚本编写*AutoID*算法因为无法预测的 ID 值将是什么.</span><span class="sxs-lookup"><span data-stu-id="66eb9-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="66eb9-546">*可预测*– 此选项主要是为了在使用重复的模板的数据控件中使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="66eb9-547">它将连接在一起的控件的命名容器，但生成的 ID 属性*ClientID*值不包含类似"ctlxxx"字符串。</span><span class="sxs-lookup"><span data-stu-id="66eb9-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="66eb9-548">此设置结合工作*ClientIDRowSuffix*控件的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="66eb9-549">您设置*ClientIDRowSuffix*属性设置为数据字段的名称和该字段的值生成的用后缀*ClientID*值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="66eb9-550">通常使用作为数据记录的主键*ClientIDRowSuffix*值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="66eb9-551">*继承*– 此设置是控件的默认行为; 它指定生成控件的 ID 是其父项相同。</span><span class="sxs-lookup"><span data-stu-id="66eb9-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="66eb9-552">可以设置*ClientIDMode*页面级别的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="66eb9-553">此定义的默认*ClientIDMode*当前页中的所有控件的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="66eb9-554">默认值*ClientIDMode*在页面级别的值是*AutoID*，并且默认值*ClientIDMode*控制级别的值是*继承*.</span><span class="sxs-lookup"><span data-stu-id="66eb9-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="66eb9-555">因此，如果未执行操作在代码中任意位置设置此属性，则所有控件将都默认为*AutoID*算法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="66eb9-556">设置页面级别值 *@ Page*指令，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="66eb9-557">您还可以设置*ClientIDMode*在配置文件中，在计算机 （计算机） 级别或应用程序级别的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="66eb9-558">此定义的默认*ClientIDMode*设置应用程序中的所有页中的所有控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="66eb9-559">如果在计算机级别设置的值，它定义的默认*ClientIDMode*在该计算机上设置的所有 Web 站点。</span><span class="sxs-lookup"><span data-stu-id="66eb9-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="66eb9-560">下面的示例演示*ClientIDMode*配置文件中的设置：</span><span class="sxs-lookup"><span data-stu-id="66eb9-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="66eb9-561">如前文所述的值*ClientID*属性派生自命名容器的控件的父级。</span><span class="sxs-lookup"><span data-stu-id="66eb9-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="66eb9-562">在某些情况下，例如当使用主页面，控件可以得到 Id 类似于以下中呈现的 HTML:</span><span class="sxs-lookup"><span data-stu-id="66eb9-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="66eb9-563">即使*输入*标记所示的元素 (从*文本框*控制) 是只有两个命名容器的页中的深度 (嵌套*ContentPlaceholder*控件)，由于主页面进行处理的方式，最终结果是如下所示的控件 ID:</span><span class="sxs-lookup"><span data-stu-id="66eb9-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="66eb9-564">此 ID 保证是唯一在页中，但在大多数情况对于长是不必要地。</span><span class="sxs-lookup"><span data-stu-id="66eb9-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="66eb9-565">想象你想以减少呈现 ID 的长度并更好地控制如何生成 ID。</span><span class="sxs-lookup"><span data-stu-id="66eb9-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="66eb9-566">（例如，您希望清除"ctlxxx"前缀。）若要实现此目的的最简单方法是通过设置*ClientIDMode*属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="66eb9-567">在此示例中， *ClientIDMode*属性设置为*静态*对于最外面*NamingPanel*元素，并设置为*可预测*为内部*NamingControl*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="66eb9-568">这些设置会导致以下标记 （页和母版页的其余部分被假定为如前面示例中相同）：</span><span class="sxs-lookup"><span data-stu-id="66eb9-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="66eb9-569">*静态*设置的效果的重置包含最外面的任何控件的命名层次结构*NamingPanel*元素，并消除*ContentPlaceHolder*并*MasterPage* Id 从生成的 id。</span><span class="sxs-lookup"><span data-stu-id="66eb9-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="66eb9-570">(*名称*呈现的元素的属性不受影响，以便正常的 ASP.NET 功能保留的事件中，视图状态，依次类推。)重置命名层次结构的一个副作用是，即使移动的标记*NamingPanel*元素为另一种*ContentPlaceholder*控件，呈现客户端 Id 保持不变。</span><span class="sxs-lookup"><span data-stu-id="66eb9-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="66eb9-571">请注意它是由您来确保呈现的控件 Id 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="66eb9-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="66eb9-572">如果它们不是，它会中断任何功能的单个 HTML 元素，如客户端所需的唯一 Id *document.getElementById*函数。</span><span class="sxs-lookup"><span data-stu-id="66eb9-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="66eb9-573">在数据绑定控件中创建可预测的客户端 Id</span><span class="sxs-lookup"><span data-stu-id="66eb9-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="66eb9-574">*ClientID*旧算法的数据绑定列表控件中的控件可以是生成的值长，不是真正的可预测。</span><span class="sxs-lookup"><span data-stu-id="66eb9-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="66eb9-575">*ClientIDMode*功能可以帮助你进行更大的控制权生成通过如何将这些 Id。</span><span class="sxs-lookup"><span data-stu-id="66eb9-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="66eb9-576">下面的示例中的标记包括*ListView*控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="66eb9-577">在上一示例中， *ClientIDMode*并*RowClientIDRowSuffix*标记中设置属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="66eb9-578">*ClientIDRowSuffix*属性可用于仅在数据绑定控件中，并且其行为不同，具体取决于哪个控件使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="66eb9-579">不同之处在于这些：</span><span class="sxs-lookup"><span data-stu-id="66eb9-579">The differences are these:</span></span>

- <span data-ttu-id="66eb9-580">*GridView*控件 — 您可以在数据源中，它在运行时创建客户端 Id 结合指定一个或多个列的名称。</span><span class="sxs-lookup"><span data-stu-id="66eb9-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="66eb9-581">例如，如果您设置*RowClientIDRowSuffix*为"产品名称，产品 id"，控件 Id，用于呈现的元素所采用的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="66eb9-582">*ListView*控件 — 可以追加到客户端 id。 在数据源中指定的单个列</span><span class="sxs-lookup"><span data-stu-id="66eb9-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="66eb9-583">例如，如果您设置*ClientIDRowSuffix* "ProductName"到呈现的控件 Id 所采用的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="66eb9-584">在这种情况下尾随 1 派生自当前数据项的产品 ID。</span><span class="sxs-lookup"><span data-stu-id="66eb9-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="66eb9-585">*Repeater*控件，此控件不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="66eb9-586">在中*Repeater*控件中，当前行的索引使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="66eb9-587">当你使用 ClientIDMode ="可预测" *Repeater*控制，客户端 Id 生成具有以下格式：</span><span class="sxs-lookup"><span data-stu-id="66eb9-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="66eb9-588">尾随 0 是当前行的索引。</span><span class="sxs-lookup"><span data-stu-id="66eb9-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="66eb9-589">*FormView*并*DetailsView*控件不显示多个行，因此它们不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="66eb9-590">保持在数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="66eb9-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="66eb9-591">*GridView*并*ListView*控件可以让用户选择一行。</span><span class="sxs-lookup"><span data-stu-id="66eb9-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="66eb9-592">在以前版本的 ASP.NET，具有已选择基于页上的行索引。</span><span class="sxs-lookup"><span data-stu-id="66eb9-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="66eb9-593">例如，如果你选择第 1 页上的第三个项，然后将其移到第 2 页选择该页面上的第三个项。</span><span class="sxs-lookup"><span data-stu-id="66eb9-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="66eb9-594">仅在.NET Framework 3.5 SP1 中的动态数据项目中最初支持持久化的选择。</span><span class="sxs-lookup"><span data-stu-id="66eb9-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="66eb9-595">如果启用此功能，当前选定的项基于项的数据键。</span><span class="sxs-lookup"><span data-stu-id="66eb9-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="66eb9-596">这意味着，如果您选择第 1 页上的第三个行，并移动到第 2 页，则不选择在第 2 页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="66eb9-597">时移到第 1 页，第三行仍处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="66eb9-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="66eb9-598">现在支持持久化的选择*GridView*并*ListView*使用的所有项目中的控件*EnablePersistedSelection*属性，如中所示下面的示例：</span><span class="sxs-lookup"><span data-stu-id="66eb9-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="66eb9-599">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="66eb9-600">ASP.NET*图表*控件扩展.NET Framework 中的数据可视化产品/服务。</span><span class="sxs-lookup"><span data-stu-id="66eb9-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="66eb9-601">使用*图表*控件，可以创建具有复杂的统计或财务分析使用直观和极具视觉表现力的图表的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="66eb9-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="66eb9-602">ASP.NET*图表*控件作为外接程序引入到.NET Framework 版本 3.5 SP1 版本，.NET Framework 4 版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="66eb9-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="66eb9-603">控件包括以下功能：</span><span class="sxs-lookup"><span data-stu-id="66eb9-603">The control includes the following features:</span></span>

- <span data-ttu-id="66eb9-604">35 种不同的图表类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-604">35 distinct chart types.</span></span>
- <span data-ttu-id="66eb9-605">无限的数量的图表区、 标题、 图例和批注。</span><span class="sxs-lookup"><span data-stu-id="66eb9-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="66eb9-606">各种不同的所有图表元素的外观设置。</span><span class="sxs-lookup"><span data-stu-id="66eb9-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="66eb9-607">对于大多数图表类型的三维支持。</span><span class="sxs-lookup"><span data-stu-id="66eb9-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="66eb9-608">可以自动适应数据点周围的智能数据标签。</span><span class="sxs-lookup"><span data-stu-id="66eb9-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="66eb9-609">条带线、 刻度分隔线和对数缩放。</span><span class="sxs-lookup"><span data-stu-id="66eb9-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="66eb9-610">包含 50 多个用于数据分析和转换的财务和统计公式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="66eb9-611">简单绑定和操作的图表数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="66eb9-612">对支持常见的数据格式，如日期、 时间和货币。</span><span class="sxs-lookup"><span data-stu-id="66eb9-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="66eb9-613">以实现交互性和事件驱动的自定义，包括客户端的支持，请单击使用 Ajax 的事件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="66eb9-614">状态管理。</span><span class="sxs-lookup"><span data-stu-id="66eb9-614">State management.</span></span>
- <span data-ttu-id="66eb9-615">二进制流。</span><span class="sxs-lookup"><span data-stu-id="66eb9-615">Binary streaming.</span></span>

<span data-ttu-id="66eb9-616">以下各图显示所生成的 ASP.NET 图表控件的财务图表的示例。</span><span class="sxs-lookup"><span data-stu-id="66eb9-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="66eb9-617">图 2: ASP.NET 图表控件示例</span><span class="sxs-lookup"><span data-stu-id="66eb9-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="66eb9-618">有关如何使用 ASP.NET 图表控件的更多示例上下载示例代码[Microsoft 图表控件的示例环境](https://go.microsoft.com/fwlink/?LinkId=128300)MSDN 网站上的页。</span><span class="sxs-lookup"><span data-stu-id="66eb9-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="66eb9-619">您可以找到更多示例社区内容在[图表控件论坛](https://go.microsoft.com/fwlink/?LinkId=128713)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="66eb9-620">将图表控件添加到 ASP.NET 页面</span><span class="sxs-lookup"><span data-stu-id="66eb9-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="66eb9-621">下面的示例演示如何添加*图表*到通过使用标记的 ASP.NET 页面的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="66eb9-622">在示例中，*图表*控件生成静态数据点的柱形图。</span><span class="sxs-lookup"><span data-stu-id="66eb9-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="66eb9-623">使用三维图表</span><span class="sxs-lookup"><span data-stu-id="66eb9-623">Using 3-D Charts</span></span>

<span data-ttu-id="66eb9-624">*图表*控件包含*ChartAreas*集合，它可以包含*ChartArea*定义的图表区的特性的对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="66eb9-625">例如，若要使用三维图表区，使用*Area3DStyle*属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="66eb9-626">下图显示了四个系列的三维图表*栏*图表类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="66eb9-627">图 3： 三维条形图</span><span class="sxs-lookup"><span data-stu-id="66eb9-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="66eb9-628">使用刻度分隔线和对数刻度</span><span class="sxs-lookup"><span data-stu-id="66eb9-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="66eb9-629">刻度分隔线和对数刻度是两种方法可以向图表添加复杂。</span><span class="sxs-lookup"><span data-stu-id="66eb9-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="66eb9-630">这些功能是特定于每个轴在图表区中。</span><span class="sxs-lookup"><span data-stu-id="66eb9-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="66eb9-631">例如，若要在图表区的主 Y 轴上使用这些功能，使用*AxisY.IsLogarithmic*并*ScaleBreakStyle*中的属性*ChartArea*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="66eb9-632">以下代码片段演示如何使用主 Y 轴上的刻度分隔线。</span><span class="sxs-lookup"><span data-stu-id="66eb9-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="66eb9-633">下图显示了具有启用了刻度分隔线的 Y 轴。</span><span class="sxs-lookup"><span data-stu-id="66eb9-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="66eb9-634">图 4： 刻度分隔线</span><span class="sxs-lookup"><span data-stu-id="66eb9-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="66eb9-635">用 QueryExtender 控件筛选数据</span><span class="sxs-lookup"><span data-stu-id="66eb9-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="66eb9-636">创建数据驱动的网页开发人员非常常见的任务是筛选数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="66eb9-637">这通常已由执行构建*其中*子句中的数据源控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="66eb9-638">此方法可能很复杂，在某些情况下*其中*语法不允许您充分利用基础数据库的完整功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="66eb9-639">若要简化筛选操作，一个新*QueryExtender*已在 ASP.NET 4 中添加控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="66eb9-640">此控件可以添加到*EntityDataSource*或*LinqDataSource*以便筛选这些控件返回的数据的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="66eb9-641">因为*QueryExtender*控件依赖于 LINQ，则将数据发送到页上，这会导致非常高效地执行操作之前筛选器在数据库服务器上应用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="66eb9-642">*QueryExtender*控件支持的各种筛选器选项。</span><span class="sxs-lookup"><span data-stu-id="66eb9-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="66eb9-643">以下部分介绍了这些选项，并提供有关如何使用它们的示例。</span><span class="sxs-lookup"><span data-stu-id="66eb9-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="66eb9-644">搜索</span><span class="sxs-lookup"><span data-stu-id="66eb9-644">Search</span></span>

<span data-ttu-id="66eb9-645">搜索选项时， *QueryExtender*控件中指定的字段执行搜索。</span><span class="sxs-lookup"><span data-stu-id="66eb9-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="66eb9-646">在以下示例中，该控件使用 TextBoxSearch 控件和对其内容中的搜索中输入的文本`ProductName`并`Supplier.CompanyName`中返回的数据的列*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="66eb9-647">范围</span><span class="sxs-lookup"><span data-stu-id="66eb9-647">Range</span></span>

<span data-ttu-id="66eb9-648">范围选项类似于搜索选项，但指定的值来定义范围的对。</span><span class="sxs-lookup"><span data-stu-id="66eb9-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="66eb9-649">在以下示例中， *QueryExtender*控制搜索`UnitPrice`中返回的数据列*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="66eb9-650">从页面上的 TextBoxFrom 和 TextBoxTo 控件中读取范围。</span><span class="sxs-lookup"><span data-stu-id="66eb9-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="66eb9-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="66eb9-651">PropertyExpression</span></span>

<span data-ttu-id="66eb9-652">属性表达式选项，可以定义为属性值的比较。</span><span class="sxs-lookup"><span data-stu-id="66eb9-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="66eb9-653">如果表达式的计算结果 *，则返回 true*，返回所检查的数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="66eb9-654">在以下示例中， *QueryExtender*控件通过比较中的数据筛选数据`Discontinued`CheckBoxDiscontinued 控件在页上的值列。</span><span class="sxs-lookup"><span data-stu-id="66eb9-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="66eb9-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="66eb9-655">CustomExpression</span></span>

<span data-ttu-id="66eb9-656">最后，可以指定要使用的自定义表达式*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="66eb9-657">此选项可以定义自定义筛选器逻辑的页面中调用函数。</span><span class="sxs-lookup"><span data-stu-id="66eb9-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="66eb9-658">下面的示例演示如何以声明方式指定的自定义表达式*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="66eb9-659">下面的示例演示自定义函数，它通过调用*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="66eb9-660">在这种情况下，而不是使用包含的数据库查询*其中*子句中，代码使用 LINQ 查询来筛选的数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="66eb9-661">以下示例演示了正在使用中只有一个表达式*QueryExtender*控件一次。</span><span class="sxs-lookup"><span data-stu-id="66eb9-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="66eb9-662">但是，可以包含多个表达式内的*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="66eb9-663">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="66eb9-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="66eb9-664">使用依赖于 （特别是使用 ASP.NET MVC) 的某些 ASP.NET 站点`<%` =  `expression %>` （通常称为"代码片段"） 的语法将一些文本写入响应。</span><span class="sxs-lookup"><span data-stu-id="66eb9-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="66eb9-665">当您使用的代码表达式时，它很容易忘记进行 HTML 编码的文本，如果文本来自用户输入，它可能会导致页打开到 XSS （跨站点脚本） 攻击。</span><span class="sxs-lookup"><span data-stu-id="66eb9-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="66eb9-666">ASP.NET 4 引入了以下新代码表达式的语法：</span><span class="sxs-lookup"><span data-stu-id="66eb9-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="66eb9-667">此语法使用写入到响应时，HTML 编码，默认情况下。</span><span class="sxs-lookup"><span data-stu-id="66eb9-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="66eb9-668">此新表达式有效地转换为以下：</span><span class="sxs-lookup"><span data-stu-id="66eb9-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="66eb9-669">例如， &lt;%: 请求"/userinput&gt"%&gt;执行 HTML 编码的值*请求"/userinput&gt"*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="66eb9-670">此功能旨在使其可以替换为旧语法的所有实例的新语法，以便将无需再决定每个步骤要使用哪一个。</span><span class="sxs-lookup"><span data-stu-id="66eb9-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="66eb9-671">但是，一些情况下要输出的文本要作为 HTML 或已经进行了编码，在这种情况下这可能会导致双重解码。</span><span class="sxs-lookup"><span data-stu-id="66eb9-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="66eb9-672">对于这些情况下，ASP.NET 4 引入了一个新的接口*IHtmlString*，具体实现，以及*HtmlString*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="66eb9-673">这些类型的实例，您可以指示，返回值是已正确编码 （或否则检查） 用于显示为 HTML，并，因此值不应为 HTML 编码试。</span><span class="sxs-lookup"><span data-stu-id="66eb9-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="66eb9-674">例如，以下不应为 （并不是） 编码的 HTML:</span><span class="sxs-lookup"><span data-stu-id="66eb9-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="66eb9-675">ASP.NET 4 运行时，已更新为使用此新语法，以便它们不是双编码的但仅限于 ASP.NET MVC 2 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="66eb9-676">运行使用 ASP.NET 3.5 SP1 的应用程序时，则此新语法无效。</span><span class="sxs-lookup"><span data-stu-id="66eb9-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="66eb9-677">请注意这并不保证 XSS 攻击防护。</span><span class="sxs-lookup"><span data-stu-id="66eb9-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="66eb9-678">例如，使用不在引号中的属性值的 HTML 可以包含仍然容易遇到用户输入。</span><span class="sxs-lookup"><span data-stu-id="66eb9-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="66eb9-679">请注意，ASP.NET 控件和 ASP.NET MVC 帮助程序的输出始终包含属性值在引号中，这是建议的方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="66eb9-680">同样，此语法不执行 JavaScript 编码，例如当您创建基于用户输入的 JavaScript 字符串。</span><span class="sxs-lookup"><span data-stu-id="66eb9-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="66eb9-681">项目模板更改</span><span class="sxs-lookup"><span data-stu-id="66eb9-681">Project Template Changes</span></span>

<span data-ttu-id="66eb9-682">在 ASP.NET 的早期版本中，使用 Visual Studio 来创建新网站项目或 Web 应用程序项目时生成的项目包含仅 Default.aspx 页上，默认值`Web.config`文件，和`App_Data`文件夹中，按如下所示图：</span><span class="sxs-lookup"><span data-stu-id="66eb9-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="66eb9-683">Visual Studio 还支持空网站项目类型，不包含任何文件根本下, 图中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="66eb9-684">结果是，对于初学者，很少指导如何构建生产型 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="66eb9-685">因此，ASP.NET 4 引入了三个新模板，另一个为空的 Web 应用程序项目，每个 Web 应用程序和网站项目。</span><span class="sxs-lookup"><span data-stu-id="66eb9-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="66eb9-686">空 Web 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="66eb9-686">Empty Web Application Template</span></span>

<span data-ttu-id="66eb9-687">顾名思义，空 Web 应用程序模板是一个精简的 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="66eb9-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="66eb9-688">下图中所示，可以从 Visual Studio 新项目对话框中，选择此项目模板：</span><span class="sxs-lookup"><span data-stu-id="66eb9-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="66eb9-689">([单击此项可查看原尺寸图像](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="66eb9-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="66eb9-690">创建空的 ASP.NET Web 应用程序时，Visual Studio 将创建以下文件夹布局：</span><span class="sxs-lookup"><span data-stu-id="66eb9-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="66eb9-691">这是类似于空网站布局从早期版本的 ASP.NET 中，有一个例外。</span><span class="sxs-lookup"><span data-stu-id="66eb9-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="66eb9-692">在 Visual Studio 2010 中，空 Web 应用程序和空网站项目包含以下最小`Web.config`文件，其中包含 Visual Studio 用来标识该项目面向的框架的信息：</span><span class="sxs-lookup"><span data-stu-id="66eb9-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="66eb9-693">如果没有此*targetFramework*属性，Visual Studio 默认值为面向.NET Framework 2.0，以打开较旧的应用程序时保持兼容性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="66eb9-694">Web 应用程序和网站项目模板</span><span class="sxs-lookup"><span data-stu-id="66eb9-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="66eb9-695">其他两个新项目模板随附 Visual Studio 2010 包含重大更改。</span><span class="sxs-lookup"><span data-stu-id="66eb9-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="66eb9-696">下图显示了在创建新的 Web 应用程序项目时创建的项目布局。</span><span class="sxs-lookup"><span data-stu-id="66eb9-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="66eb9-697">（对于网站项目布局是几乎完全相同）。</span><span class="sxs-lookup"><span data-stu-id="66eb9-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="66eb9-698">该项目包括一个未在早期版本中创建的文件数。</span><span class="sxs-lookup"><span data-stu-id="66eb9-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="66eb9-699">此外，新的 Web 应用程序项目配置了基本成员资格功能，可让您快速开始保护对新应用程序的访问。</span><span class="sxs-lookup"><span data-stu-id="66eb9-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="66eb9-700">由于此包含`Web.config`文件新的项目包含用于配置成员资格、 角色和配置文件的条目。</span><span class="sxs-lookup"><span data-stu-id="66eb9-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="66eb9-701">下面的示例演示`Web.config`新的 Web 应用程序项目文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="66eb9-702">(在这种情况下， *roleManager*被禁用。)</span><span class="sxs-lookup"><span data-stu-id="66eb9-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="66eb9-703">([单击此项可查看原尺寸图像](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="66eb9-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="66eb9-704">项目还包含第二个`Web.config`文件中`Account`目录。</span><span class="sxs-lookup"><span data-stu-id="66eb9-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="66eb9-705">第二个配置文件提供了一种方法来确保安全访问的 ChangePassword.aspx 页不记录在用户。</span><span class="sxs-lookup"><span data-stu-id="66eb9-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="66eb9-706">下面的示例演示的第二个内容`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="66eb9-707">默认情况下，新的项目模板中创建的页面还包含比在早期版本的详细内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="66eb9-708">此项目包含默认母版页和 CSS 文件，并已配置的默认页面 (Default.aspx) 默认情况下用于主页面。</span><span class="sxs-lookup"><span data-stu-id="66eb9-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="66eb9-709">结果是，如果第一次运行的 Web 应用程序或网站，默认 （家庭） 页将已正常运行。</span><span class="sxs-lookup"><span data-stu-id="66eb9-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="66eb9-710">事实上，它是类似于启动一个新的 MVC 应用程序时，将显示默认页面。</span><span class="sxs-lookup"><span data-stu-id="66eb9-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="66eb9-711">([单击此项可查看原尺寸图像](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="66eb9-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="66eb9-712">项目模板的这些更改的目的是提供有关如何开始构建新的 Web 应用程序的指导。</span><span class="sxs-lookup"><span data-stu-id="66eb9-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="66eb9-713">使用语义正确，严格 XHTML 1.0 符合标记和使用 CSS 指定的布局，在模板中的页表示用于构建 ASP.NET 4 Web 应用程序的最佳实践。</span><span class="sxs-lookup"><span data-stu-id="66eb9-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="66eb9-714">默认页还具有您可以轻松地自定义的两列布局。</span><span class="sxs-lookup"><span data-stu-id="66eb9-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="66eb9-715">例如，假设为新的 Web 应用程序想要更改的某些颜色并插入我的 ASP.NET 应用程序徽标代替你公司的徽标。</span><span class="sxs-lookup"><span data-stu-id="66eb9-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="66eb9-716">若要执行此操作，创建一个新目录下的`Content`来存储你的徽标图像：</span><span class="sxs-lookup"><span data-stu-id="66eb9-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="66eb9-717">若要将映像添加到页面，然后打开`Site.Master`文件中，找到其中我的 ASP.NET 应用程序文本定义，并将其替换为*映像*元素的*src*属性设置为新的徽标图像，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="66eb9-718">([单击此项可查看原尺寸图像](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="66eb9-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="66eb9-719">然后，可以进入 Site.css 文件并修改 CSS 类定义，以更改页面的背景色以及的标头。</span><span class="sxs-lookup"><span data-stu-id="66eb9-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="66eb9-720">这些更改的结果是，可以显示不费吹灰之力自定义的主页上：</span><span class="sxs-lookup"><span data-stu-id="66eb9-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="66eb9-721">([单击此项可查看原尺寸图像](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="66eb9-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="66eb9-722">CSS 改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-722">CSS Improvements</span></span>

<span data-ttu-id="66eb9-723">在 ASP.NET 4 中主要领域之一是工作的帮助呈现 HTML 与最新的 HTML 标准兼容的。</span><span class="sxs-lookup"><span data-stu-id="66eb9-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="66eb9-724">这包括对 ASP.NET Web 服务器控件如何使用 CSS 样式的更改。</span><span class="sxs-lookup"><span data-stu-id="66eb9-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="66eb9-725">呈现的兼容性设置</span><span class="sxs-lookup"><span data-stu-id="66eb9-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="66eb9-726">默认情况下，当 Web 应用程序或网站以.NET Framework 4 为目标*controlRenderingCompatibilityVersion*的属性*页面*元素设置为"4.0"。</span><span class="sxs-lookup"><span data-stu-id="66eb9-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="66eb9-727">此元素定义在计算机级别`Web.config`文件，默认情况下适用于所有 ASP.NET 4 应用程序：</span><span class="sxs-lookup"><span data-stu-id="66eb9-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="66eb9-728">值*controlRenderingCompatibility*是一个字符串，它允许潜在的新版本定义在将来的版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="66eb9-729">在当前版本中，此属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="66eb9-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="66eb9-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="66eb9-730">"3.5".</span></span> <span data-ttu-id="66eb9-731">此设置指示旧式呈现和标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="66eb9-732">呈现的控件的标记是 100%向后兼容，以及设置的*xhtmlConformance*遵循属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="66eb9-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="66eb9-733">"4.0".</span></span> <span data-ttu-id="66eb9-734">如果该属性具有此设置，ASP.NET Web 服务器控件执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="66eb9-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="66eb9-735">*XhtmlConformance*属性始终被视为"Strict"。</span><span class="sxs-lookup"><span data-stu-id="66eb9-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="66eb9-736">因此，控件将呈现 XHTML 1.0 Strict 标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="66eb9-737">禁用非输入控件不再呈现无效样式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="66eb9-738">*div*现在样式围绕隐藏的字段的元素，以便它们不会干扰用户创建 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="66eb9-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="66eb9-739">菜单控件呈现在语义上正确并且符合辅助功能准则的标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="66eb9-740">验证控件不呈现内联样式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="66eb9-741">控制以前呈现边框 ="0"(派生自 ASP.NET 控件*表*控制和 ASP.NET*映像*控件) 不再呈现此属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="66eb9-742">禁用控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-742">Disabling Controls</span></span>

<span data-ttu-id="66eb9-743">在 ASP.NET 3.5 SP1 和更早版本中，该框架呈现*禁用*特性的 HTML 标记中任何控制其*已启用*属性设置为*false*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="66eb9-744">但是，根据 HTML 4.01 规范，仅*输入*元素应具有此属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="66eb9-745">在 ASP.NET 4 中，可以设置*controlRenderingCompatabilityVersion*属性设置为"3.5"，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-745">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="66eb9-746">您可以创建标记*标签*如下所示，禁用了控件的控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="66eb9-747">*标签*控件将呈现以下 HTML:</span><span class="sxs-lookup"><span data-stu-id="66eb9-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="66eb9-748">在 ASP.NET 4 中，可以设置*controlRenderingCompatabilityVersion*为"4.0"。</span><span class="sxs-lookup"><span data-stu-id="66eb9-748">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* to "4.0".</span></span> <span data-ttu-id="66eb9-749">在这种情况下，仅控制呈现的*输入*元素将呈现*禁用*属性时控件的*已启用*属性设置为*false*.</span><span class="sxs-lookup"><span data-stu-id="66eb9-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="66eb9-750">控件不呈现 HTML*输入*改为呈现元素*类*引用可用于定义一个已禁用的控件外观的 CSS 类的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="66eb9-751">例如，*标签*中前面的示例所示的控件将生成以下标记：</span><span class="sxs-lookup"><span data-stu-id="66eb9-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="66eb9-752">为此控件指定的类的默认值为"aspNetDisabled"。</span><span class="sxs-lookup"><span data-stu-id="66eb9-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="66eb9-753">但是，可以更改此默认值通过设置静态*DisabledCssClass*的静态属性*WebControl*类。</span><span class="sxs-lookup"><span data-stu-id="66eb9-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="66eb9-754">对控件开发人员要使用的特定控件的行为还可以定义使用*SupportsDisabledAttribute*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="66eb9-755">隐藏 div 元素周围隐藏字段</span><span class="sxs-lookup"><span data-stu-id="66eb9-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="66eb9-756">ASP.NET 2.0 和更高版本的呈现特定于系统的隐藏的字段 (如*隐藏*用于存储视图状态信息的元素) 内*div*元素中，以便符合 XHTML 标准。</span><span class="sxs-lookup"><span data-stu-id="66eb9-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="66eb9-757">但是，这会导致问题，在 CSS 规则影响*div*页面上的元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="66eb9-758">例如，这样可能会出现在页面中的一个像素行大约隐藏*div*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="66eb9-759">在 ASP.NET 4 中， *div*将由 ASP.NET 生成的隐藏的字段的元素添加 CSS 类引用，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="66eb9-760">然后可以定义仅适用于一个 CSS 类*隐藏*元素生成的 ASP.NET 中，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="66eb9-761">模板化控件的呈现外部表</span><span class="sxs-lookup"><span data-stu-id="66eb9-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="66eb9-762">默认情况下，以下 ASP.NET Web 服务器控件支持的模板的自动包装在用于将应用内联样式的外部表中：</span><span class="sxs-lookup"><span data-stu-id="66eb9-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="66eb9-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="66eb9-763">*FormView*</span></span>
- <span data-ttu-id="66eb9-764">*登录名*</span><span class="sxs-lookup"><span data-stu-id="66eb9-764">*Login*</span></span>
- <span data-ttu-id="66eb9-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="66eb9-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="66eb9-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="66eb9-766">*ChangePassword*</span></span>
- <span data-ttu-id="66eb9-767">*向导*</span><span class="sxs-lookup"><span data-stu-id="66eb9-767">*Wizard*</span></span>
- <span data-ttu-id="66eb9-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="66eb9-768">*CreateUserWizard*</span></span>

<span data-ttu-id="66eb9-769">名为的新属性*RenderOuterTable*已添加到允许的外部表，根据标记要删除这些控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="66eb9-770">例如，考虑下面的示例对*FormView*控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="66eb9-771">此标记呈现到页上，其中包括一个 HTML 表的以下输出：</span><span class="sxs-lookup"><span data-stu-id="66eb9-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="66eb9-772">若要防止表呈现，可以设置*FormView*控件的*RenderOuterTable*属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="66eb9-773">前面的示例将以下输出，而不呈现*表*， *tr*，并*td*元素：</span><span class="sxs-lookup"><span data-stu-id="66eb9-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="66eb9-774">内容</span><span class="sxs-lookup"><span data-stu-id="66eb9-774">Content</span></span>


<span data-ttu-id="66eb9-775">此增强功能可以轻松地使用 CSS 时，控件的内容的样式因为没有任何意外的标记呈现的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="66eb9-776">请注意此更改禁用对 Visual Studio 2010 设计器中中的自动套用格式函数的支持，因为不再*表*可以托管生成的自动套用格式选项的样式特性的元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="66eb9-777">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-777">ListView Control Enhancements</span></span>

<span data-ttu-id="66eb9-778">*ListView*控件变得更轻松地在 ASP.NET 4 中使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="66eb9-779">指定包含与已知 ID 的服务器控件的布局模板被必需的早期版本的控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="66eb9-780">以下标记显示如何使用的典型示例*ListView* ASP.NET 3.5 中的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="66eb9-781">在 ASP.NET 4 中， *ListView*控件不需要布局模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="66eb9-782">可以使用以下标记替换上一示例中所示的标记：</span><span class="sxs-lookup"><span data-stu-id="66eb9-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="66eb9-783">CheckBoxList 和 RadioButtonList 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="66eb9-784">可以在 ASP.NET 3.5 中，指定布局*CheckBoxList*并*RadioButtonList*使用以下两个设置：</span><span class="sxs-lookup"><span data-stu-id="66eb9-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="66eb9-785">*流*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-785">*Flow*.</span></span> <span data-ttu-id="66eb9-786">该控件将呈现*s p a n*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="66eb9-787">*表*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-787">*Table*.</span></span> <span data-ttu-id="66eb9-788">该控件将呈现*表*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="66eb9-789">下面的示例演示这些控件的每个标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="66eb9-790">默认情况下，控件呈现 HTML 与下面类似：</span><span class="sxs-lookup"><span data-stu-id="66eb9-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="66eb9-791">因为这些控件包含的项，以呈现在语义上是正确的 HTML 列表就会呈现使用 HTML 列表及其内容 (*li*) 元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="66eb9-792">这使得更容易读取网页使用辅助技术，并使控件能够更轻松地使用 CSS 样式的用户。</span><span class="sxs-lookup"><span data-stu-id="66eb9-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="66eb9-793">在 ASP.NET 4 中， *CheckBoxList*并*RadioButtonList*控件支持的以下新值*RepeatLayout*属性：</span><span class="sxs-lookup"><span data-stu-id="66eb9-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="66eb9-794">*OrderedList* – 内容呈现为*li*中的元素*ol*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="66eb9-795">*UnorderedList* – 内容呈现为*li*中的元素*ul*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="66eb9-796">下面的示例演示如何使用这些新值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="66eb9-797">上述标记将生成以下 HTML:</span><span class="sxs-lookup"><span data-stu-id="66eb9-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="66eb9-798">请注意是否您设置*RepeatLayout*到*OrderedList*或*UnorderedList*，则*RepeatDirection*属性不再可用，并且将如果标记或代码中设置该属性，则引发运行时异常。</span><span class="sxs-lookup"><span data-stu-id="66eb9-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="66eb9-799">属性将具有任何值，因为这些控件的可视布局而使用 CSS 进行定义。</span><span class="sxs-lookup"><span data-stu-id="66eb9-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="66eb9-800">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-800">Menu Control Improvements</span></span>

<span data-ttu-id="66eb9-801">在 ASP.NET 4 中前,*菜单*呈现控件的一系列 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="66eb9-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="66eb9-802">这变得更困难，应用 CSS 样式设置内联属性之外，也是不符合可访问性标准。</span><span class="sxs-lookup"><span data-stu-id="66eb9-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="66eb9-803">在 ASP.NET 4 中，该控件现在呈现 HTML 中使用的未排序的列表和列表元素组成的语义标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="66eb9-804">下面的示例演示在 ASP.NET 页面的标记*菜单*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="66eb9-805">当页面呈现时，该控件生成以下 HTML ( *onclick*为清楚起见已省略代码):</span><span class="sxs-lookup"><span data-stu-id="66eb9-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="66eb9-806">除了呈现的改进，已使用焦点管理得到改进的菜单的键盘导航。</span><span class="sxs-lookup"><span data-stu-id="66eb9-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="66eb9-807">当*菜单*控件获得焦点，则可以使用箭头键导航元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="66eb9-808">*菜单*控件现在还将附加可访问富 internet 应用程序 (ARIA) 角色和属性 follo[wing](http://www.w3.org/TR/wai-aria-practices/#menu "菜单 ARIA 准则")为了改进可访问性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="66eb9-809">样式块中位于顶部的页上，而不是根据呈现的 HTML 元素呈现菜单控件的样式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="66eb9-810">如果你想要完全控制控件的样式，则可以设置新*IncludeStyleBlock*属性设置为*false*，在这种情况下，将不发出样式块。</span><span class="sxs-lookup"><span data-stu-id="66eb9-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="66eb9-811">若要使用此属性的一种方法是使用 Visual Studio 设计器中的自动套用格式功能设置菜单的外观。</span><span class="sxs-lookup"><span data-stu-id="66eb9-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="66eb9-812">然后可以运行页、 开放源代码的页，然后将呈现的样式块复制到外部 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="66eb9-813">在 Visual Studio 中，撤消样式设置和组*IncludeStyleBlock*到*false*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="66eb9-814">结果是在外部样式表中使用样式定义菜单外观。</span><span class="sxs-lookup"><span data-stu-id="66eb9-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="66eb9-815">向导和 CreateUserWizard 控件</span><span class="sxs-lookup"><span data-stu-id="66eb9-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="66eb9-816">ASP.NET*向导*并*CreateUserWizard*控件支持允许你定义所呈现的 HTML 的模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="66eb9-817">(*CreateUserWizard*派生自*向导*。)下面的示例演示完全模板化的标记*CreateUserWizard*控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="66eb9-818">该控件将呈现 HTML 与下面类似：</span><span class="sxs-lookup"><span data-stu-id="66eb9-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="66eb9-819">在 ASP.NET 3.5 SP1 中，尽管您可以更改模板的内容，您仍然有限地控制的输出*向导*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="66eb9-820">在 ASP.NET 4 中，您可以创建*LayoutTemplate*模板和 insert*占位符*控制 （使用保留的名称） 来指定要如何*向导控件*来呈现。</span><span class="sxs-lookup"><span data-stu-id="66eb9-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="66eb9-821">以下示例演示了此：</span><span class="sxs-lookup"><span data-stu-id="66eb9-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="66eb9-822">此示例包含以下命名中的占位符*LayoutTemplate*元素：</span><span class="sxs-lookup"><span data-stu-id="66eb9-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="66eb9-823">*headerPlaceholder* – 在运行时，这将替换为的内容*HeaderTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="66eb9-824">*sideBarPlaceholder* – 在运行时，这将替换为的内容*SideBarTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="66eb9-825">*wizardStepPlaceHolder* – 在运行时，这将替换为的内容*WizardStepTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="66eb9-826">*navigationPlaceholder* – 在运行时，这将替换为已定义的任何导航模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="66eb9-827">在以下示例中使用占位符的标记 （而不实际在模板中定义的内容） 呈现以下 HTML:</span><span class="sxs-lookup"><span data-stu-id="66eb9-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="66eb9-828">是只是现在不是用户定义的 HTML *s p a n*元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="66eb9-829">(我们预计，将来版本中，甚至*s p a n*元素将不会呈现。)现在可以完全控制由生成的几乎所有内容*向导*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="66eb9-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="66eb9-830">ASP.NET MVC</span></span>

<span data-ttu-id="66eb9-831">ASP.NET MVC 是作为外接程序框架到 ASP.NET 3.5 SP1 中引入 2009 年 3 月。</span><span class="sxs-lookup"><span data-stu-id="66eb9-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="66eb9-832">Visual Studio 2010 包括 ASP.NET MVC 2，其中包括新特性和功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="66eb9-833">区域支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-833">Areas Support</span></span>

<span data-ttu-id="66eb9-834">区域可以组控制器和视图为部分以相对其他部分隔离的大型应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="66eb9-835">每个区域可以作为一个单独的 ASP.NET MVC 项目，然后可由主应用程序引用实现。</span><span class="sxs-lookup"><span data-stu-id="66eb9-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="66eb9-836">这可帮助构建大型应用程序时管理复杂性，并使多个团队能够在单个应用程序协同工作更轻松。</span><span class="sxs-lookup"><span data-stu-id="66eb9-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="66eb9-837">数据注释属性验证支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="66eb9-838">*DataAnnotations*属性，您可以通过使用元数据特性附加到模型的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="66eb9-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="66eb9-839">*DataAnnotations*属性在 ASP.NET 3.5 SP1 中的 ASP.NET 动态数据中引入。</span><span class="sxs-lookup"><span data-stu-id="66eb9-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="66eb9-840">这些属性已集成到默认模型联编程序，并且提供元数据驱动的方法来验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="66eb9-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="66eb9-841">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="66eb9-841">Templated Helpers</span></span>

<span data-ttu-id="66eb9-842">模板化帮助器可自动关联的编辑和显示数据类型的模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="66eb9-843">例如，使用模板帮助器来指定自动为呈现日期选取器 UI 元素*System.DateTime*值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="66eb9-844">这是类似于 ASP.NET 动态数据中的字段模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="66eb9-845">*Html.EditorFor*并*Html.DisplayFor*帮助器方法具有的内置支持的呈现标准数据类型具有多个属性也为复杂对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="66eb9-846">它们还通过自定义呈现让您可以之类的数据注释属性*DisplayName*并*ScaffoldColumn*到*ViewModel*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="66eb9-847">通常，你想要自定义 UI 帮助程序更进一步的输出，并可以完全控制生成的内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="66eb9-848">*Html.EditorFor*并*Html.DisplayFor*帮助器方法支持此功能使用模板化机制，允许您定义外部模板，可以重写和控件呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="66eb9-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="66eb9-849">为类，可以单独呈现模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="66eb9-850">Dynamic Data — 动态数据</span><span class="sxs-lookup"><span data-stu-id="66eb9-850">Dynamic Data</span></span>

<span data-ttu-id="66eb9-851">引入了动态数据中 2008 年年中的.NET Framework 3.5 SP1 版本。</span><span class="sxs-lookup"><span data-stu-id="66eb9-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="66eb9-852">此功能提供了用于创建数据驱动的应用程序，其中包括许多增强功能：</span><span class="sxs-lookup"><span data-stu-id="66eb9-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="66eb9-853">用于快速构建数据驱动网站的 RAD 体验。</span><span class="sxs-lookup"><span data-stu-id="66eb9-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="66eb9-854">基于数据模型中定义的约束的自动验证。</span><span class="sxs-lookup"><span data-stu-id="66eb9-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="66eb9-855">能够轻松地更改为中的字段生成的标记*GridView*并*DetailsView*使用动态数据项目的一部分的字段模板的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="66eb9-856">请注意有关详细信息，请参阅[动态数据文档](https://msdn.microsoft.com/library/cc488545.aspx)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="66eb9-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>


<span data-ttu-id="66eb9-857">为 ASP.NET 4 中，动态数据得到增强，使开发人员能够更强大的功能来快速构建数据驱动的网站。</span><span class="sxs-lookup"><span data-stu-id="66eb9-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="66eb9-858">对于现有项目中启用动态数据</span><span class="sxs-lookup"><span data-stu-id="66eb9-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="66eb9-859">在.NET Framework 3.5 SP1 中提供的动态数据功能引入新功能，如下所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="66eb9-860">字段模板 – 这些将基于数据类型的模板提供的数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="66eb9-861">字段模板提供更简单的方法来自定义比使用为每个字段的模板字段的数据控件的外观。</span><span class="sxs-lookup"><span data-stu-id="66eb9-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="66eb9-862">验证-动态数据，您可以在数据类使用属性来指定为必填的字段范围检查、 类型检查、 使用正则表达式匹配的模式的常见方案的验证和自定义验证。</span><span class="sxs-lookup"><span data-stu-id="66eb9-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="66eb9-863">由数据控件强制进行验证。</span><span class="sxs-lookup"><span data-stu-id="66eb9-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="66eb9-864">但是，这些功能具有以下要求：</span><span class="sxs-lookup"><span data-stu-id="66eb9-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="66eb9-865">数据访问层必须基于 Entity Framework 或 LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="66eb9-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="66eb9-866">唯一的数据源控件支持这些功能已*EntityDataSource*或*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="66eb9-867">功能需要使用动态数据或动态数据实体模板，以支持该功能所需的所有文件已创建的 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="66eb9-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="66eb9-868">在 ASP.NET 4 中的动态数据支持的主要目标是能够为任何 ASP.NET 应用程序的新功能的动态数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="66eb9-869">下面的示例显示了可以在现有页面中充分利用动态数据功能的控件标记的。</span><span class="sxs-lookup"><span data-stu-id="66eb9-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="66eb9-870">在代码页中，必须要使这些控件的动态数据支持添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="66eb9-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="66eb9-871">当*GridView*控件处于编辑模式下，动态数据会自动验证输入的数据是格式正确。</span><span class="sxs-lookup"><span data-stu-id="66eb9-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="66eb9-872">如果不是，显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="66eb9-873">此功能还提供了其他权益，如能够指定默认值插入模式。</span><span class="sxs-lookup"><span data-stu-id="66eb9-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="66eb9-874">如果没有动态数据，要实现一个字段的默认值必须向事件附加，查找控件 (使用*FindControl*)，并将其值设置。</span><span class="sxs-lookup"><span data-stu-id="66eb9-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="66eb9-875">在 ASP.NET 4 中， *EnableDynamicData*调用支持第二个参数，可让你将任何字段的默认值传递对象，在此示例中所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="66eb9-876">DynamicDataManager 控件声明性语法</span><span class="sxs-lookup"><span data-stu-id="66eb9-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="66eb9-877">*DynamicDataManager*控件已得到增强，以便可以将其配置以声明方式，与在 ASP.NET 中，而不是仅在代码的大多数控件一样。</span><span class="sxs-lookup"><span data-stu-id="66eb9-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="66eb9-878">有关标记*DynamicDataManager*控件的外观如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="66eb9-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="66eb9-879">此标记启用动态数据行为中引用的 GridView1 控件*然后*一部分*DynamicDataManager*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="66eb9-880">实体模板</span><span class="sxs-lookup"><span data-stu-id="66eb9-880">Entity Templates</span></span>

<span data-ttu-id="66eb9-881">实体模板提供自定义而无需创建自定义页的数据的布局的新方法。</span><span class="sxs-lookup"><span data-stu-id="66eb9-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="66eb9-882">页上，使用模板*FormView*控件 (而不是*DetailsView*控制，因为在早期版本的动态数据中的页模板中使用) 和*DynamicEntity*要呈现实体模板的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="66eb9-883">这为您提供了更好地控制由动态数据呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="66eb9-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="66eb9-884">以下列表显示了包含实体模板的新项目目录布局：</span><span class="sxs-lookup"><span data-stu-id="66eb9-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="66eb9-885">`EntityTemplate`目录包含有关如何显示的数据模型对象的模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="66eb9-886">默认情况下，通过使用呈现对象`Default.ascx`模板，其中提供了看上去如同创建的标记的标记*DetailsView* ASP.NET 3.5 SP1 中的动态数据使用的控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="66eb9-887">下面的示例演示的标记`Default.ascx`控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="66eb9-888">若要更改整个站点的外观，可以编辑默认模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="66eb9-889">模板用于显示、 编辑和插入操作。</span><span class="sxs-lookup"><span data-stu-id="66eb9-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="66eb9-890">新的模板可以添加根据数据对象的名称才能更改外观和感觉的只是一种类型的对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="66eb9-891">例如，可以添加以下模板：</span><span class="sxs-lookup"><span data-stu-id="66eb9-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="66eb9-892">该模板可能包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="66eb9-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="66eb9-893">新的实体模板显示在页面上使用新的*DynamicEntity*控件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="66eb9-894">在运行时，此控件替换为实体模板的内容。</span><span class="sxs-lookup"><span data-stu-id="66eb9-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="66eb9-895">下面的标记演示*FormView*控制中`Detail.aspx`页使用的实体模板的模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="66eb9-896">请注意*DynamicEntity*标记中的元素。</span><span class="sxs-lookup"><span data-stu-id="66eb9-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="66eb9-897">新的字段模板的 Url 和电子邮件地址</span><span class="sxs-lookup"><span data-stu-id="66eb9-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="66eb9-898">ASP.NET 4 引入了两个新内置字段模板`EmailAddress.ascx`和`Url.ascx`。</span><span class="sxs-lookup"><span data-stu-id="66eb9-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="66eb9-899">这些模板用于标记为字段*EmailAddress*或*Url*与*数据类型*属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="66eb9-900">有关*EmailAddress*对象，该字段显示为超链接，通过创建*mailto:* 协议。</span><span class="sxs-lookup"><span data-stu-id="66eb9-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="66eb9-901">当用户单击该链接时，打开用户的电子邮件客户端，并创建主干消息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="66eb9-902">对象类型化为*Url*显示为普通的超链接。</span><span class="sxs-lookup"><span data-stu-id="66eb9-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="66eb9-903">下面的示例演示如何将标记字段。</span><span class="sxs-lookup"><span data-stu-id="66eb9-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="66eb9-904">与 DynamicHyperLink 控件创建的链接</span><span class="sxs-lookup"><span data-stu-id="66eb9-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="66eb9-905">动态数据使用.NET Framework 3.5 SP1，以控制用户访问网站时，请参阅最终用户的 Url 中添加新路由功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="66eb9-906">新*DynamicHyperLink*控件，可以轻松地生成动态数据站点中页面的链接。</span><span class="sxs-lookup"><span data-stu-id="66eb9-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="66eb9-907">下面的示例演示如何使用*DynamicHyperLink*控件：</span><span class="sxs-lookup"><span data-stu-id="66eb9-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="66eb9-908">此标记创建一个链接，指向的列表页`Products`表中定义的路由基于`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="66eb9-909">该控件自动使用基于动态数据页的默认表名。</span><span class="sxs-lookup"><span data-stu-id="66eb9-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="66eb9-910">对数据模型中继承的支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="66eb9-911">实体框架和 LINQ to SQL 支持在其数据模型中继承。</span><span class="sxs-lookup"><span data-stu-id="66eb9-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="66eb9-912">出现这种可能是一个具有数据库`InsurancePolicy`表。</span><span class="sxs-lookup"><span data-stu-id="66eb9-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="66eb9-913">它还可能包含`CarPolicy`并`HousePolicy`具有相同的字段的表`InsurancePolicy`以及如何将多个字段。</span><span class="sxs-lookup"><span data-stu-id="66eb9-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="66eb9-914">动态数据已被修改，以了解数据模型中继承的对象并继承表中支持搭建基架。</span><span class="sxs-lookup"><span data-stu-id="66eb9-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="66eb9-915">支持多对多关系 （仅适用于实体框架）</span><span class="sxs-lookup"><span data-stu-id="66eb9-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="66eb9-916">实体框架提供的丰富支持实现通过上公开作为集合的关系的表之间的多对多关系*实体*对象。</span><span class="sxs-lookup"><span data-stu-id="66eb9-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="66eb9-917">新`ManyToMany.ascx`和`ManyToMany_Edit.ascx`字段模板已添加用于显示和编辑多对多关系中涉及的数据提供支持。</span><span class="sxs-lookup"><span data-stu-id="66eb9-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="66eb9-918">新属性来控制显示和支持枚举</span><span class="sxs-lookup"><span data-stu-id="66eb9-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="66eb9-919">*DisplayAttribute*已添加为您提供字段的显示方式的更多控制权。</span><span class="sxs-lookup"><span data-stu-id="66eb9-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="66eb9-920">*DisplayName*早期版本允许你更改用作字段标题的名称的动态数据中的属性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="66eb9-921">新*DisplayAttribute*类，可以指定用于显示的字段，例如在其中会显示一个字段，以及是否将使用一个字段作为筛选器顺序的更多选项。</span><span class="sxs-lookup"><span data-stu-id="66eb9-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="66eb9-922">该属性还提供了用于标签的名称的独立控制*GridView*控制中使用的名称*DetailsView*控件，该字段的帮助文本，水印用于字段 （如果该字段接受输入的文本）。</span><span class="sxs-lookup"><span data-stu-id="66eb9-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="66eb9-923">*EnumDataTypeAttribute*类已添加，以便你可以将字段映射到枚举。</span><span class="sxs-lookup"><span data-stu-id="66eb9-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="66eb9-924">当此特性应用于字段时，指定枚举类型。</span><span class="sxs-lookup"><span data-stu-id="66eb9-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="66eb9-925">动态数据使用新`Enumeration.ascx`的字段模板来创建 UI，以显示和编辑枚举值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="66eb9-926">该模板将映射到枚举中的名称来自数据库的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="66eb9-927">对筛选器的增强的支持</span><span class="sxs-lookup"><span data-stu-id="66eb9-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="66eb9-928">动态数据 1.0 附带了内置布尔值列和外键列的筛选器。</span><span class="sxs-lookup"><span data-stu-id="66eb9-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="66eb9-929">筛选器不允许，可以指定是否显示它们，或以何种顺序显示它们。</span><span class="sxs-lookup"><span data-stu-id="66eb9-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="66eb9-930">新*DisplayAttribute*属性解决了这两的这些问题，请为您提供对某列是否显示为筛选器控制并以什么顺序显示。</span><span class="sxs-lookup"><span data-stu-id="66eb9-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="66eb9-931">其他增强功能是，筛选支持已被重新[编写为使用新](#0.2__QueryExtender "_QueryExtender") Web 窗体的功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="66eb9-932">这样可以创建筛选器，而无需了解的数据源控件的筛选器将与一起使用。</span><span class="sxs-lookup"><span data-stu-id="66eb9-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="66eb9-933">这些扩展，以及筛选器也已转换为模板控件，该编辑器可以添加新的。</span><span class="sxs-lookup"><span data-stu-id="66eb9-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="66eb9-934">最后， *DisplayAttribute*前面所述的类允许在相同中重写的默认筛选器的方式*UIHint*允许重写的列的默认字段模板。</span><span class="sxs-lookup"><span data-stu-id="66eb9-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="66eb9-935">Visual Studio 2010 Web 开发改进</span><span class="sxs-lookup"><span data-stu-id="66eb9-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="66eb9-936">对于更高版本 CSS 兼容性，通过 HTML 和 ASP.NET 标记代码段和新动态 IntelliSense JavaScript 提高工作效率增强了 Visual Studio 2010 中的 web 开发。</span><span class="sxs-lookup"><span data-stu-id="66eb9-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="66eb9-937">改进的 CSS 兼容性</span><span class="sxs-lookup"><span data-stu-id="66eb9-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="66eb9-938">Visual Studio 2010 中的 Visual Web Developer 设计器已更新，以提高 CSS 2.1 标准符合性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="66eb9-939">在设计器更好地保留在 HTML 源的完整性和 Visual Studio 的早期版本相比更加可靠。</span><span class="sxs-lookup"><span data-stu-id="66eb9-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="66eb9-940">实质上，体系结构改进还进行了将会更好地启用中呈现、 布局和可维护性的未来增强功能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="66eb9-941">HTML 和 JavaScript 代码片段</span><span class="sxs-lookup"><span data-stu-id="66eb9-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="66eb9-942">在 HTML 编辑器中，IntelliSense 会自动完成的标记名称。</span><span class="sxs-lookup"><span data-stu-id="66eb9-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="66eb9-943">IntelliSense 代码段功能会自动完成整个标记和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="66eb9-944">在 Visual Studio 2010 中，IntelliSense 代码段支持 JavaScript 以及 C# 和 Visual Basic 中，这在 Visual Studio 的早期版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="66eb9-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="66eb9-945">Visual Studio 2010 包括了超过 200 个代码段，可帮助你自动完成常见 ASP.NET 和 HTML 标记，包括必需的属性 (如 runat ="server") 和特定于标记的公共属性 (如*ID*， *DataSourceID*， *ControlToValidate*，和*文本*)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="66eb9-946">您可以下载其他代码段，也可以编写您自己封装的你或你的团队使用的常见任务的标记块的代码段。</span><span class="sxs-lookup"><span data-stu-id="66eb9-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="66eb9-947">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="66eb9-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="66eb9-948">在 Visual 2010 中，JavaScript IntelliSense 经过重新设计，提供更丰富的编辑体验。</span><span class="sxs-lookup"><span data-stu-id="66eb9-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="66eb9-949">IntelliSense 现在可识别具有已动态生成的方法如对象*registerNamespace*和类似的技术使用的其他 JavaScript 框架。</span><span class="sxs-lookup"><span data-stu-id="66eb9-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="66eb9-950">要分析的脚本的大型库并使用很少或没有处理延迟显示 IntelliSense 改进了性能。</span><span class="sxs-lookup"><span data-stu-id="66eb9-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="66eb9-951">若要支持几乎所有第三方库，并以支持各种编码风格已极大地增加兼容性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="66eb9-952">键入并立即利用 intellisense 时，现在进行分析文档注释。</span><span class="sxs-lookup"><span data-stu-id="66eb9-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="66eb9-953">使用 Visual Studio 2010 的 web 应用程序部署</span><span class="sxs-lookup"><span data-stu-id="66eb9-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="66eb9-954">当 ASP.NET 开发人员部署 Web 应用程序时，他们经常发现他们会遇到以下问题：</span><span class="sxs-lookup"><span data-stu-id="66eb9-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="66eb9-955">部署到共享的托管站点需要技术，例如 FTP，可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="66eb9-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="66eb9-956">此外，你必须手动执行任务，例如运行 SQL 脚本来配置数据库，必须更改 IIS 设置，例如，为应用程序中配置虚拟目录文件夹。</span><span class="sxs-lookup"><span data-stu-id="66eb9-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="66eb9-957">在企业环境中，除了部署 Web 应用程序文件，管理员经常必须修改 ASP.NET 配置文件和 IIS 设置。</span><span class="sxs-lookup"><span data-stu-id="66eb9-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="66eb9-958">数据库管理员必须运行一系列 SQL 脚本来获取运行的应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="66eb9-959">此类安装耗费大量精力，通常需要数小时才能完成，并且必须仔细记载。</span><span class="sxs-lookup"><span data-stu-id="66eb9-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="66eb9-960">Visual Studio 2010 包括解决这些问题，以及允许用户无缝地将部署 Web 应用程序的技术。</span><span class="sxs-lookup"><span data-stu-id="66eb9-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="66eb9-961">这些技术之一是 IIS Web 部署工具 (MsDeploy.exe)。</span><span class="sxs-lookup"><span data-stu-id="66eb9-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="66eb9-962">Visual Studio 2010 中的 web 部署功能包括以下主要方面：</span><span class="sxs-lookup"><span data-stu-id="66eb9-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="66eb9-963">Web 打包</span><span class="sxs-lookup"><span data-stu-id="66eb9-963">Web packaging</span></span>
- <span data-ttu-id="66eb9-964">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="66eb9-964">Web.config transformation</span></span>
- <span data-ttu-id="66eb9-965">数据库部署</span><span class="sxs-lookup"><span data-stu-id="66eb9-965">Database deployment</span></span>
- <span data-ttu-id="66eb9-966">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-966">One-click publish for Web applications</span></span>

<span data-ttu-id="66eb9-967">以下部分提供有关这些功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="66eb9-968">Web 打包</span><span class="sxs-lookup"><span data-stu-id="66eb9-968">Web Packaging</span></span>

<span data-ttu-id="66eb9-969">Visual Studio 2010 使用 MSDeploy 工具来创建应用程序，这被称为一个压缩 (.zip) 文件*Web 包*。</span><span class="sxs-lookup"><span data-stu-id="66eb9-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="66eb9-970">包文件包含有关你的应用程序以及以下内容的元数据：</span><span class="sxs-lookup"><span data-stu-id="66eb9-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="66eb9-971">IIS 设置，其中包括应用程序池设置、 错误页设置等。</span><span class="sxs-lookup"><span data-stu-id="66eb9-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="66eb9-972">实际 Web 内容，其中包括 Web 页面、 用户控件、 静态内容 （映像和 HTML 文件） 等。</span><span class="sxs-lookup"><span data-stu-id="66eb9-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="66eb9-973">SQL Server 数据库架构和数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="66eb9-974">安全证书，组件安装在 GAC、 注册表设置等。</span><span class="sxs-lookup"><span data-stu-id="66eb9-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="66eb9-975">可以复制到任何服务器，然后通过使用 IIS 管理器手动安装 Web 包。</span><span class="sxs-lookup"><span data-stu-id="66eb9-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="66eb9-976">或者，对于自动部署，包可安装使用命令行命令或使用部署 Api。</span><span class="sxs-lookup"><span data-stu-id="66eb9-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="66eb9-977">Visual Studio 2010 提供了内置的 MSBuild 任务和目标以创建 Web 包。</span><span class="sxs-lookup"><span data-stu-id="66eb9-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="66eb9-978">有关详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)MSDN 网站上和[10 + 20 原因为何应创建 Web 包](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)在 Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="66eb9-979">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="66eb9-979">Web.config Transformation</span></span>

<span data-ttu-id="66eb9-980">对于 Web 应用程序部署，Visual Studio 2010 引入了[XML 文档转换 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)，这是一项功能，允许你转换`Web.config`开发设置中为生产设置的文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="66eb9-981">转换设置名为的转换文件中指定`web.debug.config`， `web.release.config`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="66eb9-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="66eb9-982">（这些文件的名称匹配 MSBuild 配置。）转换文件包括只是需要对已部署进行的更改`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="66eb9-983">使用简单的语法指定所做的更改。</span><span class="sxs-lookup"><span data-stu-id="66eb9-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="66eb9-984">下面的示例显示了一部分`web.release.config`可能生成部署的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="66eb9-985">在示例中的替换关键字在部署过程中指定*connectionString*中的节点`Web.config`文件将替换示例中列出的值。</span><span class="sxs-lookup"><span data-stu-id="66eb9-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="66eb9-986">有关详细信息，请参阅[Web 应用程序项目部署的 Web.config 转换语法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)msdn <a id="0.2_a"> </a> Web 站点和[Web 部署： Web.Config 转换](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="66eb9-987">数据库部署</span><span class="sxs-lookup"><span data-stu-id="66eb9-987">Database Deployment</span></span>

<span data-ttu-id="66eb9-988">Visual Studio 2010 部署包可以包含 SQL Server 数据库上的依赖项。</span><span class="sxs-lookup"><span data-stu-id="66eb9-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="66eb9-989">为包定义的一部分，为源数据库提供连接字符串。</span><span class="sxs-lookup"><span data-stu-id="66eb9-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="66eb9-990">创建 Web 包时，Visual Studio 2010 创建 SQL 脚本 （可选） 为数据库架构和数据，，然后添加到包。</span><span class="sxs-lookup"><span data-stu-id="66eb9-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="66eb9-991">此外可以提供自定义 SQL 脚本，并指定其应运行在服务器的序列。</span><span class="sxs-lookup"><span data-stu-id="66eb9-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="66eb9-992">在部署时，提供了适合于目标服务器; 一个连接字符串然后，部署过程使用此连接字符串来运行脚本，创建数据库架构，并添加数据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="66eb9-993">此外，通过使用一次单击发布，您可以配置部署应用程序发布到远程共享托管站点时，直接发布你的数据库。</span><span class="sxs-lookup"><span data-stu-id="66eb9-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="66eb9-994">有关详细信息，请参阅[如何： 部署数据库与 Web 应用程序项目](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)MSDN 网站上和[VS 2010 使用的数据库部署](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)在 Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="66eb9-995">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="66eb9-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="66eb9-996">Visual Studio 2010 还允许您使用的 IIS 远程管理服务发布到远程服务器的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="66eb9-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="66eb9-997">为你的托管帐户或测试服务器或暂存服务器，可以创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="66eb9-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="66eb9-998">每个配置文件可以安全地保存相应的凭据。</span><span class="sxs-lookup"><span data-stu-id="66eb9-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="66eb9-999">你可以随后部署到任何目标服务器通过使用 Web 一次单击一次单击发布工具栏。</span><span class="sxs-lookup"><span data-stu-id="66eb9-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="66eb9-1000">使用 Visual Studio 2010，您还可以通过使用 MSBuild 命令行发布。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="66eb9-1001">这允许您配置您的团队生成环境，以持续集成模型中包括发布。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="66eb9-1002">有关详细信息，请参阅[如何： 部署 Web 应用程序项目使用一键式发布和 Web 部署](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)MSDN 网站上和[Web 一键式发布使用 VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)在 Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="66eb9-1003">若要在 Visual Studio 2010 中查看有关 Web 应用程序部署的视频演示，请参阅[VS 2010 Web 开发人员预览版](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html)在 Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="66eb9-1004">资源</span><span class="sxs-lookup"><span data-stu-id="66eb9-1004">Resources</span></span>

<span data-ttu-id="66eb9-1005">以下网站提供有关 ASP.NET 4 和 Visual Studio 2010 的其他信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="66eb9-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — MSDN 网站上的 ASP.NET 4 的官方文档。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="66eb9-1007">[https://www.asp.net/](https://www.asp.net/) — ASP.NET 团队的网站。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="66eb9-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 并[ASP.NET 动态数据内容映射](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)— ASP.NET 团队网站和 ASP.NET 动态数据有关的正式文档中的在线资源。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="66eb9-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — ASP.NET Ajax 开发主 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="66eb9-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — Visual Studio 2010 中包括有关功能的信息 Visual Web 开发人员团队博客。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="66eb9-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — ASP.NET 的预览版本的主要 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="66eb9-1012">免责声明</span><span class="sxs-lookup"><span data-stu-id="66eb9-1012">Disclaimer</span></span>

<span data-ttu-id="66eb9-1013">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="66eb9-1014">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="66eb9-1015">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="66eb9-1016">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="66eb9-1017">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="66eb9-1018">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="66eb9-1019">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="66eb9-1020">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="66eb9-1021">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="66eb9-1022">除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="66eb9-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="66eb9-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="66eb9-1024">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1024">All rights reserved.</span></span>

<span data-ttu-id="66eb9-1025">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="66eb9-1026">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="66eb9-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
