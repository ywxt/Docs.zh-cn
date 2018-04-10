---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 开发概述 |Microsoft 文档
author: rick-anderson
description: 本文档提供有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能的概述。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 6ce52c387ff835eda46bc1882b8b974889e2d4af
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="f8a2c-103">ASP.NET 4 和 Visual Studio 2010 Web 开发概述</span><span class="sxs-lookup"><span data-stu-id="f8a2c-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>
====================
> <span data-ttu-id="f8a2c-104">本文档提供有关 ASP.NET 中的.net Framework 4 和 Visual Studio 2010 中包含的许多新功能的概述。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="f8a2c-105">下载此白皮书</span><span class="sxs-lookup"><span data-stu-id="f8a2c-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


<span data-ttu-id="f8a2c-106">**内容**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-106">**Contents**</span></span>

<span data-ttu-id="f8a2c-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="f8a2c-108">Web.config 文件重构</span><span class="sxs-lookup"><span data-stu-id="f8a2c-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="f8a2c-109">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="f8a2c-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="f8a2c-110">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="f8a2c-111">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="f8a2c-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="f8a2c-112">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="f8a2c-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="f8a2c-113">扩展该范围允许 Url</span><span class="sxs-lookup"><span data-stu-id="f8a2c-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="f8a2c-114">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="f8a2c-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="f8a2c-115">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="f8a2c-116">可扩展的 HTML、 URL 和 HTTP 标头编码</span><span class="sxs-lookup"><span data-stu-id="f8a2c-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="f8a2c-117">为在单个辅助进程中的单个应用程序性能监视</span><span class="sxs-lookup"><span data-stu-id="f8a2c-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="f8a2c-118">Multi-Targeting</span><span class="sxs-lookup"><span data-stu-id="f8a2c-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="f8a2c-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="f8a2c-120">jQuery 包含在 Web 窗体和 MVC</span><span class="sxs-lookup"><span data-stu-id="f8a2c-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="f8a2c-121">内容传送网络支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="f8a2c-122">ScriptManager Explicit Scripts</span><span class="sxs-lookup"><span data-stu-id="f8a2c-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="f8a2c-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="f8a2c-124">设置与 Page.MetaKeywords 和 Page.MetaDescription 属性的 Meta 标记</span><span class="sxs-lookup"><span data-stu-id="f8a2c-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="f8a2c-125">启用视图状态的单个控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="f8a2c-126">更改为浏览器功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="f8a2c-127">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="f8a2c-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="f8a2c-128">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="f8a2c-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="f8a2c-129">保持数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="f8a2c-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="f8a2c-130">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="f8a2c-131">筛选数据与 QueryExtender 控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="f8a2c-132">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="f8a2c-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="f8a2c-133">项目模板更改</span><span class="sxs-lookup"><span data-stu-id="f8a2c-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="f8a2c-134">CSS Improvements</span><span class="sxs-lookup"><span data-stu-id="f8a2c-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="f8a2c-135">隐藏 div 元素周围隐藏字段</span><span class="sxs-lookup"><span data-stu-id="f8a2c-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="f8a2c-136">模板化控件呈现的外部表</span><span class="sxs-lookup"><span data-stu-id="f8a2c-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="f8a2c-137">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="f8a2c-138">按和说明如何增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="f8a2c-139">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="f8a2c-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="f8a2c-140">向导和 CreateUserWizard 控件 56</span><span class="sxs-lookup"><span data-stu-id="f8a2c-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="f8a2c-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="f8a2c-142">区域支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="f8a2c-143">数据注释属性验证支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="f8a2c-144">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="f8a2c-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="f8a2c-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="f8a2c-146">启用动态数据的现有项目</span><span class="sxs-lookup"><span data-stu-id="f8a2c-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="f8a2c-147">Declarative DynamicDataManager Control Syntax</span><span class="sxs-lookup"><span data-stu-id="f8a2c-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="f8a2c-148">实体模板</span><span class="sxs-lookup"><span data-stu-id="f8a2c-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="f8a2c-149">Url 和电子邮件地址的新字段模板</span><span class="sxs-lookup"><span data-stu-id="f8a2c-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="f8a2c-150">创建链接与 DynamicHyperLink 控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="f8a2c-151">对数据模型中的继承支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="f8a2c-152">对多对多关系 （仅用于实体框架） 支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="f8a2c-153">控件显示和支持枚举的新特性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="f8a2c-154">对筛选器的增强支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="f8a2c-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="f8a2c-156">改进的 CSS 兼容性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="f8a2c-157">HTML 和 JavaScript 代码段</span><span class="sxs-lookup"><span data-stu-id="f8a2c-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="f8a2c-158">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="f8a2c-159">**[Web 应用程序部署使用 Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="f8a2c-160">Web Packaging</span><span class="sxs-lookup"><span data-stu-id="f8a2c-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="f8a2c-161">Web.config Transformation</span><span class="sxs-lookup"><span data-stu-id="f8a2c-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="f8a2c-162">Database Deployment</span><span class="sxs-lookup"><span data-stu-id="f8a2c-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="f8a2c-163">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="f8a2c-164">Resources</span><span class="sxs-lookup"><span data-stu-id="f8a2c-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="f8a2c-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="f8a2c-166">核心服务</span><span class="sxs-lookup"><span data-stu-id="f8a2c-166">Core Services</span></span>

<span data-ttu-id="f8a2c-167">ASP.NET 4 引入了大量改进输出缓存和会话状态存储等的核心 ASP.NET 服务的功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="f8a2c-168">重构的 Web.config 文件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-168">Web.config File Refactoring</span></span>

<span data-ttu-id="f8a2c-169">`Web.config`文件，其中包含配置有关 Web 应用程序变得相当通过过去的几个版本的.NET framework 已添加新功能，如 Ajax，如路由，以及与 IIS 7 的集成。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="f8a2c-170">这得更难来配置或启动新的 Web 应用程序，而无需 Visual Studio 之类的工具。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="f8a2c-171">来 NET Framework 4，主要的配置元素均已移至`machine.config`文件和应用程序现在继承这些设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="f8a2c-172">这允许`Web.config`ASP.NET 4 应用程序可以为空，或者以包含仅的以下行，其指定 Visual Studio 的哪个版本的应用程序所面向的 framework 中的文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="f8a2c-173">可扩展的输出缓存</span><span class="sxs-lookup"><span data-stu-id="f8a2c-173">Extensible Output Caching</span></span>

<span data-ttu-id="f8a2c-174">自 ASP.NET 1.0 发布的时间，输出缓存已启用了开发人员可以在内存中存储生成的输出的页、 控件和 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="f8a2c-175">在后续的 Web 请求，ASP.NET 可提供内容更快地服务通过从内存而不是重新生成从零开始的输出检索生成的输出。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="f8a2c-176">但是，此方法有一个限制-生成的内容始终具有要存储在内存中，并在服务器上遇到通信流量过大，占用输出缓存的内存可以争取从 Web 应用程序的其他部分的内存需求。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="f8a2c-177">ASP.NET 4 将添加一个扩展点的输出缓存，使你能够配置一个或多个自定义输出缓存提供程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="f8a2c-178">输出缓存提供程序可以使用任何存储机制保留 HTML 的内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="f8a2c-179">这使它能够为各种持久性机制，可以包括本地或远程磁盘，云存储，创建自定义输出缓存提供程序和分布式缓存引擎。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="f8a2c-180">为从新派生的类创建自定义输出缓存提供程序*System.Web.Caching.OutputCacheProvider*类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="f8a2c-181">然后，你可以配置中的提供程序`Web.config`使用新的文件*提供程序*的小节*outputCache*元素，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="f8a2c-182">默认情况下，在 ASP.NET 4 中，所有 HTTP 响应，呈现的页面和控件使用内存中输出缓存中，如下所示在前面的示例，其中*defaultProvider*属性设置为 AspNetInternalProvider。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="f8a2c-183">你可以更改 Web 应用程序使用通过指定不同的提供程序名称的默认输出缓存提供程序*defaultProvider*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="f8a2c-184">此外，你可以选择不同的输出缓存提供程序每个控件和每个请求。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="f8a2c-185">选择不同的输出缓存提供程序为不同 Web 用户控件的最简单方法是以声明方式使用新进行*providerName*属性中控件指令，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="f8a2c-186">指定的 HTTP 请求不同的输出缓存提供程序需要稍有更多工作。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="f8a2c-187">而不是以声明方式指定提供程序，则重写新*GetOuputCacheProviderName*中的方法`Global.asax`文件以编程方式指定要用于特定请求的提供程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="f8a2c-188">下面的示例演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="f8a2c-189">为 ASP.NET 4 的输出缓存提供程序扩展性的添加后，您现在可以为您的网站通过更主动和更智能的输出缓存策略。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="f8a2c-190">例如，现可以同时在缓存磁盘获得较低流量的页面缓存在内存中，站点的"Top 10"页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="f8a2c-191">或者，可以缓存呈现的页上，每个不同的组合，但使用分布式的缓存，以便将内存消耗卸载从前端 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="f8a2c-192">自动启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="f8a2c-193">某些 Web 应用程序需要加载大量数据或执行昂贵的初始化，然后才能处理相关的第一个请求处理。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="f8a2c-194">在早期版本的 ASP.NET，针对这些情况你必须设计自定义方法"唤醒"ASP.NET 应用程序，然后运行过程中的初始化代码*应用程序\_负载*中的方法`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="f8a2c-195">一个名为的新的可伸缩性功能*自动启动*，直接地址提供了此方案的 ASP.NET 4 运行时在 Windows Server 2008 R2 上的 IIS 7.5 上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="f8a2c-196">自动启动功能提供了启动应用程序池，初始化 ASP.NET 应用程序，然后接受 HTTP 请求提供受控的方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f8a2c-197">IIS 7.5 的 IIS 应用程序预热模块</span><span class="sxs-lookup"><span data-stu-id="f8a2c-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="f8a2c-198">IIS 团队已为 IIS 7.5 中发布应用程序预热模块的第一个测试版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="f8a2c-199">这使得预热你的应用程序更加容易，不是前面所述。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="f8a2c-200">而不是编写自定义代码，你可以指定要执行之前的 Web 应用程序接受来自网络的请求资源的 Url。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="f8a2c-201">在 IIS 服务的启动期间发生此预热 (如果配置 IIS 应用程序池作为*AlwaysRunning*) 和 IIS 工作进程的回收时。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="f8a2c-202">在回收，旧的 IIS 工作进程继续执行请求，直到完全预热新生成的工作进程，以便应用程序发生任何中断或由于 unprimed 缓存其他问题。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="f8a2c-203">请注意，此模块的工作原理的任何版本的 ASP.NET，从 2.0 版开始。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="f8a2c-204">有关详细信息，请参阅[应用程序预热](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="f8a2c-205">有关演示如何使用预热功能的演练，请参阅[Getting Started with IIS 7.5 应用程序预热模块](https://www.iis.net/learn/manage)IIS.net 网站上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>


<span data-ttu-id="f8a2c-206">若要使用自动启动功能，是 IIS 管理员设置的应用程序池使用中的以下配置为自动启动的 IIS 7.5 中`applicationHost.config`文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="f8a2c-207">由于单个应用程序池可以包含多个应用程序，你指定要通过使用中的以下配置自动启动的单个应用程序`applicationHost.config`文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="f8a2c-208">IIS 7.5 冷启动 IIS 7.5 服务器时，或单独的应用程序池回收时，使用中的信息`applicationHost.config`文件以确定哪些 Web 应用程序需要自动启动。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="f8a2c-209">对于每个应用程序标记为自动启动，IIS7.5 发送一个请求到 ASP.NET 4，以启动应用程序处于状态在此期间应用程序暂时不接受 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="f8a2c-210">ASP.NET 在这种状态时，都会定义的类型实例化*serviceAutoStartProvider*属性 （如前面的示例中所示） 并调用到其公共入口点。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="f8a2c-211">你创建具有必要的入口点通过实现托管的自动启动类型*IProcessHostPreloadClient*接口，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="f8a2c-212">在中运行代码在你初始化后*预加载*方法和方法返回时，ASP.NET 应用程序已准备好处理请求。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="f8a2c-213">添加到 IIS.5 和 ASP.NET 4 自动启动后，你现在可以执行成本高昂的应用程序初始化之前处理的第一个 HTTP 请求提供明确定义的方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="f8a2c-214">例如，可以使用新的自动启动功能以初始化应用程序和应用程序已初始化并准备接受 HTTP 流量，则然后信号负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="f8a2c-215">永久重定向页面</span><span class="sxs-lookup"><span data-stu-id="f8a2c-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="f8a2c-216">它是在 Web 应用程序随着时间推移，这会导致的搜索引擎中的陈旧链接的累积移动页面和其他内容周围的常见做法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="f8a2c-217">在 ASP.NET 中，开发人员已传统上处理对旧 Url 的请求通过使用通过使用*Response.Redirect*方法以将请求转发到新 URL。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="f8a2c-218">但是，*重定向*方法会将一个 HTTP 302 找到 （临时重定向） 响应，这会导致额外 HTTP 往返当用户尝试访问的旧 Url。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="f8a2c-219">添加一个新的 ASP.NET 4 *RedirectPermanent*帮助器方法，可以方便地对问题 HTTP 301 永久移动响应，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="f8a2c-220">搜索引擎和识别永久重定向的其他用户代理将存储与内容，从而消除了不必要的往返行程由临时重定向的浏览器相关联的新 URL。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="f8a2c-221">收缩会话状态</span><span class="sxs-lookup"><span data-stu-id="f8a2c-221">Shrinking Session State</span></span>

<span data-ttu-id="f8a2c-222">ASP.NET 提供用于在 Web 场中存储会话状态的两个默认选项： 的会话状态提供程序时，将调用的进程外会话状态服务器，并在 Microsoft SQL Server 数据库中存储数据的会话状态提供程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="f8a2c-223">由于这两种方法涉及存储 Web 应用程序的工作进程之外的状态信息，会话状态已发送到远程存储之前要序列化。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="f8a2c-224">具体取决于开发人员将保存在会话状态多少信息，序列化数据的大小可以变得相当大。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="f8a2c-225">ASP.NET 4 为这两种进程外会话状态提供程序引入了新的压缩选项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="f8a2c-226">当*compressionEnabled*下面的示例所示的配置选项设置为*true*，ASP.NET 将压缩 （和解压缩） 使用.NET Framework序列化的会话状态*System.IO.Compression.GZipStream*类。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="f8a2c-227">通过简单的新特性的添加`Web.config`文件，使用备用的 CPU 周期，在 Web 服务器上的应用程序可以实现的序列化的会话状态数据的大小大幅降低。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="f8a2c-228">扩展该范围允许 Url</span><span class="sxs-lookup"><span data-stu-id="f8a2c-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="f8a2c-229">ASP.NET 4 引入了用于扩展应用程序 Url 的大小的新选项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="f8a2c-230">ASP.NET 的早期版本约束 URL 路径长度为 260 个字符，基于 NTFS 文件路径限制。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="f8a2c-231">在 ASP.NET 4 中，你可以选择增加 （或减少） 根据你的应用程序，此限制使用两个新*httpRuntime*配置特性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="f8a2c-232">下面的示例演示这些新属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="f8a2c-233">若要允许长于或短的路径 （不包括协议、 服务器名称和查询字符串的 URL 的部分），修改*[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="f8a2c-234">若要允许长于或短的查询字符串，可修改的值*[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="f8a2c-235">ASP.NET 4 还可配置的 URL 字符检查使用的字符。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="f8a2c-236">当 ASP.NET 的 url 的路径部分中找到无效的字符时，它将拒绝该请求，并发出 HTTP 400 错误。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="f8a2c-237">在以前版本的 ASP.NET，URL 字符检查是限于一组固定的字符。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="f8a2c-238">在 ASP.NET 4 中，你可以自定义的一套使用新的有效字符*requestPathInvalidChars*属性*httpRuntime*配置元素，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidChars* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="f8a2c-239">默认情况下， <em>requestPathInvalidChars</em>属性定义为无效的八个字符。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-239">By default, the <em>requestPathInvalidChars</em> attribute defines eight characters as invalid.</span></span> <span data-ttu-id="f8a2c-240">(分配给字符串中<em>requestPathInvalidChars</em>默认情况下<em>，</em>小于 (&lt;)、 大于 (&gt;)，和 & 符 (&amp;) 字符都是编码，因为`Web.config`文件是一个 XML 文件。)根据需要可以自定义的一套无效字符。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-240">(In the string that is assigned to <em>requestPathInvalidChars</em> by default<em>,</em>the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a2c-241">请注意 ASP.NET 4 始终拒绝包含 0x00 到 0x1F、 ASCII 范围内的字符的 URL 路径，因为这些无效的 URL 字符中的 IETF RFC 2396 定义 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt))。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="f8a2c-242">在 Windows Server 版本上运行 IIS 6 或更高版本，http.sys 协议设备驱动程序会自动拒绝 Url 有了这些字符。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="f8a2c-243">可扩展请求验证</span><span class="sxs-lookup"><span data-stu-id="f8a2c-243">Extensible Request Validation</span></span>

<span data-ttu-id="f8a2c-244">ASP.NET 请求验证在跨站点脚本 (XSS) 攻击中搜索字符串的常用的传入 HTTP 请求的数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="f8a2c-245">如果找到潜在 XSS 字符串，请求验证标记的可疑的字符串，并返回错误。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="f8a2c-246">仅当它找到 XSS 攻击中使用的最常见字符串时，内置请求验证将返回错误。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="f8a2c-247">以前进行 XSS 验证更为严格的尝试导致误报过多。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="f8a2c-248">但是，客户可能希望更加严格，或反之可能想要有意放宽 XSS 请求验证检查的特定页面，或者为特定类型的请求。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="f8a2c-249">在 ASP.NET 4 中，请求验证功能已经成为可扩展，以便你可以使用自定义请求验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="f8a2c-250">若要扩展请求验证，你可以创建从新派生的类*System.Web.Util.RequestValidator*类型，并且你配置应用程序 (在*httpRuntime*一部分`Web.config`文件) 以使用自定义的类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="f8a2c-251">下面的示例演示如何配置自定义请求验证类：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="f8a2c-252">新*requestValidationType*特性需要指定的类，提供自定义请求验证的标准.NET Framework 类型标识符字符串。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="f8a2c-253">对于每个请求，ASP.NET 将调用自定义的类型，以处理每个传入的 HTTP 请求数据片段。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="f8a2c-254">传入的 URL、 所有 HTTP 标头 （cookie 和自定义标头），以及实体正文都可用于检查由自定义请求验证类类似下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="f8a2c-255">有关在你不希望检查传入的 HTTP 数据片段的情况下，请求验证类可以回退到使用让 ASP.NET 默认请求验证运行通过只需调用*基。IsValidRequestString。*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="f8a2c-256">对象缓存和对象缓存扩展性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="f8a2c-257">自其第一个版本中，ASP.NET 就提供了强大的内存中对象缓存 (*System.Web.Caching.Cache*)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="f8a2c-258">缓存实现已很常见，它已用于非 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="f8a2c-259">但是，它是一个 Windows 窗体或 WPF 应用程序，以包含对引用冲`System.Web.dll`只是为了能够使用 ASP.NET 对象缓存。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="f8a2c-260">若要使缓存可供所有应用程序，.NET Framework 4 引入了新的程序集、 新的命名空间、 某些基本类型和一个具体缓存实现。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="f8a2c-261">新`System.Runtime.Caching.dll`程序集包含在一个新的缓存 API *System.Runtime.Caching*命名空间。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="f8a2c-262">命名空间包含两个核心组类：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="f8a2c-263">为生成任何类型的自定义缓存实现提供了基础的抽象类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="f8a2c-264">具体的内存中对象的缓存实现 ( *system.runtime.caching.memorycache 有关的问题*类)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="f8a2c-265">新*MemoryCache*类密切建模于 ASP.NET 缓存，并在共享的内部缓存引擎逻辑大部分与 ASP.NET 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="f8a2c-266">尽管公共缓存 Api *System.Runtime.Caching*已经更新，以支持开发的自定义缓存，如果你已使用 ASP.NET*缓存*对象，您会发现在熟悉的概念新的 Api。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="f8a2c-267">新的深度讨论*MemoryCache*类和受支持的基 Api 都需要整个文档。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="f8a2c-268">但是，下面的示例揭示了新的缓存 API 的工作原理。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="f8a2c-269">该示例针对没有任何依赖项的 Windows 窗体应用程序的编写上`System.Web.dll`。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="f8a2c-270">可扩展的 HTML、 URL 和编码的 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="f8a2c-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="f8a2c-271">在 ASP.NET 4 中，你可以创建以下常见文本编码任务的自定义编码例程：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="f8a2c-272">HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-272">HTML encoding.</span></span>
- <span data-ttu-id="f8a2c-273">URL 编码。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-273">URL encoding.</span></span>
- <span data-ttu-id="f8a2c-274">HTML 编码属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="f8a2c-275">编码出站 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="f8a2c-276">你可以通过从新派生创建自定义编码器*System.Web.Util.HttpEncoder*类型中，然后配置 ASP.NET 用于中的自定义类型*httpRuntime*部分`Web.config`文件中，为下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="f8a2c-277">已配置自定义编码器后，ASP.NET 会自动调用每当公共编码方法的自定义的编码实现*System.Web.HttpUtility*或*System.Web.HttpServerUtility*类称为。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="f8a2c-278">这允许创建自定义编码器实现积极的字符编码，而 Web 开发团队的其余部分将继续使用公共 ASP.NET 编码 Api 的 Web 开发团队的一个组成部分。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="f8a2c-279">通过集中配置自定义编码器在*httpRuntime*元素，则可保证通过自定义编码器进行路由从公共 ASP.NET 编码 Api 的所有文本编码调用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="f8a2c-280">为在单个辅助进程中的单个应用程序性能监视</span><span class="sxs-lookup"><span data-stu-id="f8a2c-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="f8a2c-281">若要增加可以在一台服务器承载的网站数，许多托管商的单个辅助进程中运行多个 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="f8a2c-282">但是，如果多个应用程序使用单个共享的辅助进程，很难服务器管理员能够找出单个应用程序中遇到问题。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="f8a2c-283">ASP.NET 4 利用由 CLR 引入的新资源监视功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="f8a2c-284">若要启用此功能，你可以添加到下面的 XML 配置片段`aspnet.config`配置文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="f8a2c-285">请注意`aspnet.config`文件位于安装.NET Framework 的目录。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="f8a2c-286">它不是`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-286">It is not the `Web.config` file.</span></span>


<span data-ttu-id="f8a2c-287">当*appDomainResourceMonitoring*已启用功能、"ASP.NET 应用程序"性能类别中提供了两个新的性能计数器：*托管处理器时间百分比*和*管理内存使用*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="f8a2c-288">这两个这些性能计数器使用新的 CLR 应用程序域资源管理功能跟踪估计的 CPU 时间和各个 ASP.NET 应用程序托管的内存使用率。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="f8a2c-289">因此，与 ASP.NET 4 中，管理员现在可以在单个辅助进程中运行的单个应用程序的资源消耗更加详细地查看。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="f8a2c-290">多目标</span><span class="sxs-lookup"><span data-stu-id="f8a2c-290">Multi-Targeting</span></span>

<span data-ttu-id="f8a2c-291">你可以创建面向.NET Framework 的特定版本的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="f8a2c-292">在 ASP.NET 4 中中的新属性*编译*元素`Web.config`文件，可以面向.NET Framework 4 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="f8a2c-293">如果你明确指定目标.NET Framework 4 中，并且包含中的可选元素`Web.config`文件的项如*system.codedom*，这些元素必须是正确的针对.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="f8a2c-294">(如果不显式面向.NET Framework 4，目标框架，则从将项记入缺乏推断`Web.config`文件。)</span><span class="sxs-lookup"><span data-stu-id="f8a2c-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="f8a2c-295">下面的示例演示如何使用*targetFramework*属性中*编译*元素`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="f8a2c-296">请注意下列有关面向特定的.NET framework 版本：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="f8a2c-297">.NET Framework 4 的应用程序池中，ASP.NET 生成系统的时候承担.NET Framework 4 为目标`Web.config`文件不包含*targetFramework*属性或如果`Web.config`找不到文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="f8a2c-298">（你可能需要更改你的应用程序，以使其在.NET Framework 4 下运行的编码。）</span><span class="sxs-lookup"><span data-stu-id="f8a2c-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="f8a2c-299">如果包括*targetFramework*属性，并且如果*system.codeDom*中定义了元素`Web.config`文件，此文件必须包含正确的输入，针对.NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="f8a2c-300">如果你使用*aspnet\_编译器*命令预编译你的应用程序 （如生成环境），则必须使用的正确版本*aspnet\_编译器*在目标框架的命令。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="f8a2c-301">使用编译器随附.NET Framework 2.0 （%windir%\microsoft.net\framework\v2.0.50727) 为.NET Framework 3.5 和更早版本编译。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="f8a2c-302">使用使用.NET Framework 4 附带的编译器来编译创建的应用程序使用该框架或使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="f8a2c-303">在运行时，编译器使用的计算机安装的最新的 framework 程序集 (并因此在 gac 中)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="f8a2c-304">如果框架到更高版本进行了更新 （例如，安装假设版本 4.1），你将能够即使框架的更新版本中使用功能*targetFramework*属性以较低的版本为目标（例如 4.0)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="f8a2c-305">(但是，在设计时在 Visual Studio 2010 或当你使用*aspnet\_编译器*命令时，使用较新的 framework 的功能将导致编译器错误)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="f8a2c-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="f8a2c-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="f8a2c-307">jQuery 包含在 Web 窗体和 MVC</span><span class="sxs-lookup"><span data-stu-id="f8a2c-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="f8a2c-308">Web 窗体和 MVC 的 Visual Studio 模板包括开放源代码 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="f8a2c-309">当你创建新网站或项目时，创建包含以下 3 个文件的脚本文件夹：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="f8a2c-310">jQuery 1.4.1.js – 用户可读，unminified jQuery 库版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="f8a2c-311">jQuery-14.1.min.js – jQuery 库的缩减版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="f8a2c-312">jQuery-1.4.1-vsdoc.js – jQuery 库的 Intellisense 文档文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="f8a2c-313">在开发应用程序时包括 jQuery 的 unminified 的版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="f8a2c-314">包括对于生产应用程序的 jQuery 的缩减的版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="f8a2c-315">例如，下面的 Web 窗体页显示如何使用 jQuery 更改 ASP.NET TextBox 控件以黄色当它们具有焦点时的背景色。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="f8a2c-316">内容传送网络支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-316">Content Delivery Network Support</span></span>

<span data-ttu-id="f8a2c-317">Microsoft Ajax 内容交付网络 (CDN)，可轻松地将 ASP.NET Ajax 和 jQuery 脚本添加到 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="f8a2c-318">例如，你可以开始使用 jQuery 库只需通过添加`<script>`标记添加到你指向 Ajax.microsoft.com 如下的页：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="f8a2c-319">通过利用 Microsoft Ajax CDN，就可以显著提高 Ajax 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="f8a2c-320">Microsoft Ajax CDN 的内容进行缓存在世界各地的服务器上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="f8a2c-321">此外，Microsoft Ajax CDN 使浏览器重用缓存的 JavaScript 文件位于不同域中的网站。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="f8a2c-322">Microsoft Ajax 内容交付网络支持 SSL (HTTPS)，以防你需要服务网页上使用安全套接字层。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="f8a2c-323">实现了回退 CDN 不可用时。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="f8a2c-324">测试回退。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-324">Test the fallback.</span></span>

<span data-ttu-id="f8a2c-325">若要了解有关 Microsoft Ajax CDN 的详细信息，请访问以下网站：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="f8a2c-326">ASP.NET ScriptManager 支持 Microsoft Ajax CDN。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="f8a2c-327">只需通过设置一个属性，EnableCdn 属性中，你可以从 CDN 检索所有 ASP.NET framework JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="f8a2c-328">EnableCdn 属性设置为值 true 后，ASP.NET 框架将从 CDN 包括用于验证和 UpdatePanel 的所有 JavaScript 文件中检索所有 ASP.NET framework JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="f8a2c-329">设置此一个属性可以极大影响 web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="f8a2c-330">通过使用 web 资源属性，可以对 JavaScript 文件设置 CDN 路径。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="f8a2c-331">新的 CdnPath 属性指定 CDN 使用 EnableCdn 属性设置为值 true 时的路径：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="f8a2c-332">ScriptManager 显式脚本</span><span class="sxs-lookup"><span data-stu-id="f8a2c-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="f8a2c-333">在过去，如果你使用 ASP.NET ScriptManger 然后需要加载整个整体 ASP.NET Ajax 库。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="f8a2c-334">通过利用新的 ScriptManager.AjaxFrameworkMode 属性，您可以控制完全加载 ASP.NET Ajax 库的组件和加载仅需要 ASP.NET Ajax 库的组件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="f8a2c-335">ScriptManager.AjaxFrameworkMode 属性可以设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="f8a2c-336">启用-指定 ScriptManager 控件自动包括 MicrosoftAjax.js 脚本文件，它是每个核心框架脚本 （旧行为） 的组合的脚本文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="f8a2c-337">禁用-指定所有 Microsoft Ajax 脚本功能将被都禁用，ScriptManager 控件不会自动引用的任何脚本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="f8a2c-338">显式-指定将显式包含了对你的页面要求的单个 framework 核心脚本文件的脚本引用，并确保将包含每个脚本文件所需的依赖关系的引用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="f8a2c-339">例如，如果 AjaxFrameworkMode 属性设置为值 Explicit 则可以指定所需的特定 ASP.NET Ajax 组件脚本：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="f8a2c-340">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="f8a2c-340">Web Forms</span></span>

<span data-ttu-id="f8a2c-341">Web 窗体的 ASP.NET 1.0 发布以来已在 ASP.NET 中的一项核心功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="f8a2c-342">许多增强功能已在此区域中为 ASP.NET 4，其中包括：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="f8a2c-343">能够设置*元*标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="f8a2c-344">更好地控制视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-344">More control over view state.</span></span>
- <span data-ttu-id="f8a2c-345">若要使用浏览器功能的简单方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="f8a2c-346">支持使用 ASP.NET 路由与 Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="f8a2c-347">更好地控制生成的 Id。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-347">More control over generated IDs.</span></span>
- <span data-ttu-id="f8a2c-348">可以保存数据控件中的选定的行。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="f8a2c-349">更好地控制中呈现的 HTML *FormView*和*ListView*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="f8a2c-350">筛选对数据源控件的支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="f8a2c-351">设置与 Page.MetaKeywords 和 Page.MetaDescription 属性的元标记</span><span class="sxs-lookup"><span data-stu-id="f8a2c-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="f8a2c-352">ASP.NET 4 将两个属性添加*页*类， *MetaKeywords*和*MetaDescription*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="f8a2c-353">这两个属性表示对应*元*标记在页中，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="f8a2c-354">这两个属性的工作方式相同的方式页面的*标题*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="f8a2c-355">它们遵循以下规则：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-355">They follow these rules:</span></span>

1. <span data-ttu-id="f8a2c-356">如果有任何*元*标记中*头*属性的名称匹配的元素 (也就是说，命名 ="关键字" *Page.MetaKeywords*和名称 = "描述"*Page.MetaDescription*，尚未设置这些属性的含义)、*元*标记将在呈现时添加到页面。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="f8a2c-357">如果已有*元*与这些名称的标记，这些属性执行操作作为 get 和 set 方法的现有标记的内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="f8a2c-358">你可以在运行时，它可让你从数据库或其他源获取的内容和它可让你设置标记动态来描述什么设置这些属性的特定页适用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="f8a2c-359">你还可以设置*关键字*和*说明*中的属性*@ Page*指令顶部的 Web 窗体页标记中，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="f8a2c-360">这将覆盖*元*标记已在页中声明的内容 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="f8a2c-361">说明的内容*元*标记用于改善搜索列出 Google 中的预览。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="f8a2c-362">(有关详细信息，请参阅[提高代码段与元说明 makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) Google 站长中央博客上。)Google 和 Windows Live 搜索不使用关键字的内容的任何内容，但其他搜索引擎可能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="f8a2c-363">有关详细信息，请参阅[元关键字建议](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)搜索引擎指南网站上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="f8a2c-364">这些新属性是一个简单的功能，但它们将保存你的要求，以将它们手动添加从或编写你自己的代码创建*元*标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="f8a2c-365">对单个控件启用视图状态</span><span class="sxs-lookup"><span data-stu-id="f8a2c-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="f8a2c-366">默认情况下，为包含页上的每个控件可能存储视图状态，即使不需要应用程序的结果的页面，可启用视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="f8a2c-367">一个页生成，并且会增加将页面发送到客户端和发回所需的时间量，在标记中包含视图状态数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="f8a2c-368">存储比所需的详细视图状态可能会导致性能明显下降。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="f8a2c-369">在 ASP.NET 的早期版本中，开发人员为了减少页大小，无法禁用单独的控件的视图状态，但出现了因此显式为单独的控件执行操作。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="f8a2c-370">在 ASP.NET 4 中，Web 服务器控件包括*ViewStateMode*允许您默认情况下禁用视图状态，然后仅为需要它在页中的控件中启用它的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="f8a2c-371">*ViewStateMode*属性采用一个枚举，其中有三个值：*已启用*，*禁用*，和*继承*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="f8a2c-372">*启用*启用视图状态针对该控件和任何子控件的设置为*继承*或有执行任何操作设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="f8a2c-373">*已禁用*禁用视图状态，和*继承*指定该控件使用*ViewStateMode*从父控件设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="f8a2c-374">下面的示例演示如何*ViewStateMode*属性会发生作用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="f8a2c-375">标记和代码中的以下页面的控件包括值*ViewStateMode*属性：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="f8a2c-376">如你所见，代码将禁用 PlaceHolder1 控件的视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="f8a2c-377">子 label1 控件继承此属性的值 (*继承*默认值为*ViewStateMode*控件。)，并因此将保存的视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="f8a2c-378">在 PlaceHolder2 控件中， *ViewStateMode*设置为*已启用*，因此 label2 继承此属性并保存视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="f8a2c-379">当首次加载页时，*文本*属性均*标签*控件设置为字符串"[DynamicValue]"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="f8a2c-380">这些设置的效果是，如果首次加载页面，下面的输出将显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="f8a2c-381">已禁用 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="f8a2c-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="f8a2c-382">启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="f8a2c-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="f8a2c-383">回发后，但是，将显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="f8a2c-384">已禁用 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="f8a2c-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="f8a2c-385">启用：`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="f8a2c-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="f8a2c-386">Label1 控件 (其*ViewStateMode*值设置为*禁用*) 具有不会保留在代码中设置为它的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="f8a2c-387">但是，label2 控制 (其*ViewStateMode*值设置为*已启用*) 均保留其状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="f8a2c-388">你还可以设置*ViewStateMode*中*@ Page*指令，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="f8a2c-389">*页*类是另一个控件; 它作为页中的所有其他控件的父控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="f8a2c-390">默认值*ViewStateMode*是*已启用*有关的实例*页*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="f8a2c-391">因为默认为控件*继承*，控件将继承*已启用*属性值，除非你设置*ViewStateMode*页或控制级别。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="f8a2c-392">值*ViewStateMode*属性确定仅在是否维护视图状态*应*属性设置为*true*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="f8a2c-393">如果*应*属性设置为*false*，将不保留视图状态即使*ViewStateMode*设置为*已启用*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="f8a2c-394">此功能很好的用途是与*ContentPlaceHolder*主页面，可以在其中设置中的控件*ViewStateMode*到*禁用*主数据页上，然后启用它为单独*ContentPlaceHolder*又可以包含需要的控件的控件视图状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="f8a2c-395">与浏览器功能的更改</span><span class="sxs-lookup"><span data-stu-id="f8a2c-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="f8a2c-396">ASP.NET 确定用户用于浏览您的站点，通过使用一种称为功能的浏览器的功能*浏览器功能*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="f8a2c-397">浏览器功能由*HttpBrowserCapabilities*对象 (由公开*Request.Browser*属性)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="f8a2c-398">例如，你可以使用*HttpBrowserCapabilities*对象确定的类型和版本的当前浏览器是否支持 JavaScript 的特定版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="f8a2c-399">或者，你可以使用*HttpBrowserCapabilities*对象确定请求是否来自移动设备。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="f8a2c-400">*HttpBrowserCapabilities*对象都由一组的浏览器定义文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="f8a2c-401">这些文件包含的特定浏览器的功能的信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="f8a2c-402">在 ASP.NET 4 中，这些浏览器定义文件已更新为包含有关最近引入的浏览器和如 Google Chrome、 研究运动 BlackBerry smartphone 以及 Apple iPhone 中的设备的信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="f8a2c-403">以下列表显示新的浏览器定义文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="f8a2c-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-404">*blackberry.browser*</span></span>
- <span data-ttu-id="f8a2c-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-405">*chrome.browser*</span></span>
- <span data-ttu-id="f8a2c-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-406">*Default.browser*</span></span>
- <span data-ttu-id="f8a2c-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-407">*firefox.browser*</span></span>
- <span data-ttu-id="f8a2c-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-408">*gateway.browser*</span></span>
- <span data-ttu-id="f8a2c-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-409">*generic.browser*</span></span>
- <span data-ttu-id="f8a2c-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-410">*ie.browser*</span></span>
- <span data-ttu-id="f8a2c-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-411">*iemobile.browser*</span></span>
- <span data-ttu-id="f8a2c-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-412">*iphone.browser*</span></span>
- <span data-ttu-id="f8a2c-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-413">*opera.browser*</span></span>
- <span data-ttu-id="f8a2c-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="f8a2c-415">使用浏览器功能提供程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="f8a2c-416">在 ASP.NET 3.5 Service Pack 1，你可以定义的功能的浏览器具有以下方式：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="f8a2c-417">在计算机级别中，创建或更新`.browser`以下文件夹中的 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="f8a2c-418">在定义的浏览器功能后，你运行以下命令从 Visual Studio 命令提示符以重新生成浏览器功能程序集并将其添加到 gac 中：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="f8a2c-419">对于单个应用程序，您创建`.browser`中应用程序的文件`App_Browsers`文件夹。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="f8a2c-420">这些方法要求你更改 XML 文件，但计算机级别更改，你必须重新启动应用程序后运行 aspnet\_regbrowsers.exe 过程。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="f8a2c-421">ASP.NET 4 包含功能称为*浏览器功能提供程序*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="f8a2c-422">顾名思义，此允许您生成的提供程序在进而使你可以使用你自己的代码来确定浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="f8a2c-423">在实践中，开发人员通常未定义自定义浏览器功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="f8a2c-424">浏览器文件会进行硬若要更新，该过程相当复杂，对它们进行更新为和的 XML 语法`.browser`文件可以是复杂，无法使用和定义。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="f8a2c-425">新增功能将使此过程更容易是如果没有常见的浏览器定义语法，或包含最新的浏览器的定义或甚至此类数据库的 Web 服务的数据库。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="f8a2c-426">新的浏览器功能提供程序功能使得整个这些方案可能和实践，为第三方开发人员。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="f8a2c-427">有两种主要方法为使用新的 ASP.NET 4 浏览器功能提供程序功能： 扩展 ASP.NET 浏览器功能定义功能，或完全替换它。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="f8a2c-428">下列各节首先介绍如何替换功能，以及如何对其进行扩展。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="f8a2c-429">替换 ASP.NET 浏览器功能的功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="f8a2c-430">若要完全替换 ASP.NET 浏览器功能定义功能，请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="f8a2c-431">创建派生自的提供程序类*HttpCapabilitiesProvider*它将替代*GetBrowserCapabilities*方法，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="f8a2c-432">此示例中的代码创建一个新*HttpBrowserCapabilities*对象，指定名为浏览器并将该功能设置为 MyCustomBrowser 功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="f8a2c-433">与应用程序注册提供程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="f8a2c-434">为了与应用程序使用提供程序，您必须添加*提供程序*属性设为*browserCaps*主题中`Web.config`或`Machine.config`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="f8a2c-435">(你还可以定义中的提供程序属性*位置*目录应用程序，例如在特定的移动设备的文件夹中的特定文件的元素。)下面的示例演示如何设置*提供程序*配置文件中的属性：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="f8a2c-436">注册新的浏览器功能定义另一种方法是使用代码，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="f8a2c-437">此代码必须在运行*应用程序\_启动*事件`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="f8a2c-438">任何将更改为*BrowserCapabilitiesProvider*执行应用程序中的任何代码，以确保缓存仍保留在已解析的有效状态之前，可能必须出现类*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="f8a2c-439">缓存 HttpBrowserCapabilities 对象</span><span class="sxs-lookup"><span data-stu-id="f8a2c-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="f8a2c-440">前面的示例具有一个问题，这是代码将运行自定义提供程序调用以获取每次*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="f8a2c-441">这可能在每个请求期间发生多次。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="f8a2c-442">在示例中，提供程序的代码没有多大用处。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="f8a2c-443">但是，如果自定义提供程序中的代码执行中的大量工作以便获得*HttpBrowserCapabilities*对象，这可能会影响性能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="f8a2c-444">若要防止此类情况发生，你可以缓存*HttpBrowserCapabilities*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="f8a2c-445">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-445">Follow these steps:</span></span>

1. <span data-ttu-id="f8a2c-446">创建一个类，派生自*HttpCapabilitiesProvider*，如下面的示例中：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="f8a2c-447">在示例中，代码调用的自定义的 BuildCacheKey 方法，而生成的缓存密钥和它通过调用自定义的 GetCacheTime 方法获取的缓存的时间长度。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="f8a2c-448">然后该代码将添加已解析*HttpBrowserCapabilities*到缓存的对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="f8a2c-449">可以从缓存中检索并在上重复使用该对象进行的后续请求使用的自定义提供程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="f8a2c-450">注册提供程序与应用程序，如前面的过程中所述。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="f8a2c-451">扩展 ASP.NET 浏览器功能的功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="f8a2c-452">上一节描述了如何创建一个新*HttpBrowserCapabilities* ASP.NET 4 中的对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="f8a2c-453">你还可以通过将新的浏览器功能定义添加到已在 ASP.NET 中的那些扩展 ASP.NET 浏览器功能的功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="f8a2c-454">你可以执行此操作而无需使用的 XML 浏览器定义。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="f8a2c-455">下面的过程演示如何。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="f8a2c-456">创建一个类，派生自*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="f8a2c-457">此代码首先使用 ASP.NET 浏览器功能的功能来尝试将浏览器标识。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="f8a2c-458">但是，如果标识没有浏览器基于定义在请求中的信息 (即，如果*浏览器*属性*HttpBrowserCapabilities*对象是字符串"Unknown")，该代码调用自定义提供程序 (MyBrowserCapabilitiesEvaluator) 若要将浏览器标识。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="f8a2c-459">注册提供程序与应用程序，如前面的示例中所述。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="f8a2c-460">通过将新功能添加到现有的功能定义扩展浏览器功能的功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="f8a2c-461">除了创建自定义浏览器定义提供程序并且动态创建新的浏览器定义中，你可以扩展具有附加功能的现有浏览器定义。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="f8a2c-462">这允许你使用的定义，位于接近你想，但没有仅的一些功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="f8a2c-463">为此，请执行下列步骤。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="f8a2c-464">创建一个类，派生自*HttpCapabilitiesEvaluator*它将替代*GetBrowserCapabilities*方法，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="f8a2c-465">此代码示例将扩展现有的 ASP.NET *HttpCapabilitiesEvaluator*类，并获取*HttpBrowserCapabilities*与当前的请求定义通过使用下面的代码相匹配的对象:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="f8a2c-466">然后，代码可以添加或修改此浏览器的功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="f8a2c-467">有两种方法来指定新的浏览器功能：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="f8a2c-468">添加到的键/值对*IDictionary*由公开的对象*功能*属性*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="f8a2c-469">在前面的示例中，该代码将添加名为的值的多点触控功能*true*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="f8a2c-470">设置的现有属性*HttpCapabilitiesBase*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="f8a2c-471">在前面的示例中，代码会设置*帧*属性*true*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="f8a2c-472">此属性是只需访问器的*IDictionary*由公开的对象*功能*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="f8a2c-473">请注意此模型将应用到的任何属性*HttpBrowserCapabilities*，包括控件适配器。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="f8a2c-474">注册提供程序与应用程序，如前面的过程中所述。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="f8a2c-475">ASP.NET 4 中的路由</span><span class="sxs-lookup"><span data-stu-id="f8a2c-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="f8a2c-476">ASP.NET 4 添加了对使用 Web 窗体使用的路由的内置支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="f8a2c-477">路由使你能够配置应用程序可以接受请求不映射到物理文件的 Url。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="f8a2c-478">相反，你可以使用路由定义 Url，并向用户意义，可帮助你的应用程序的搜索引擎搜索引擎优化 (SEO)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="f8a2c-479">例如，对于现有的应用程序中显示产品类别的页面的 URL 可能类似于下面的示例：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="f8a2c-480">通过使用路由，你可以配置应用程序接受要呈现的相同信息的以下 URL:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="f8a2c-481">路由已从 ASP.NET 3.5 SP1 开始提供。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="f8a2c-482">(有关如何使用路由在 ASP.NET 3.5 SP1 中的示例，请参阅文章[路由使用与 WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "此项的标题。")</span><span class="sxs-lookup"><span data-stu-id="f8a2c-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="f8a2c-483">在 Phil Haack 博客。）但是，ASP.NET 4 包括一些功能，它可以更轻松地使用路由，其中包括：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="f8a2c-484">*PageRouteHandler*类，该类定义路由时，你使用的简单 HTTP 处理程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="f8a2c-485">类将数据传递给请求路由到的页面。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="f8a2c-486">新属性*HttpRequest.RequestContext*和*Page.RouteData* (即用于代理*HttpRequest.RequestContext.RouteData*对象)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="f8a2c-487">这些属性使其更轻松地从路由传递的访问信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="f8a2c-488">下面的新的表达式生成器，在中定义*System.Web.Compilation.RouteUrlExpressionBuilder*和*System.Web.Compilation.RouteValueExpressionBuilder*:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="f8a2c-489">*RouteUrl*，该属性提供一种简单的方法来创建到 ASP.NET 服务器控件中的路由 URL 相对应的 URL。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="f8a2c-490">*RouteValue*，该属性提供一种简单的方法，以提取信息*RouteContext*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="f8a2c-491">*RouteParameter*类，它可以更轻松地将中包含的数据传递*RouteContext*对数据源控件的查询的对象 (类似于[ *FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f8a2c-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="f8a2c-492">Web 窗体页的路由</span><span class="sxs-lookup"><span data-stu-id="f8a2c-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="f8a2c-493">下面的示例演示如何使用新的定义的 Web 窗体路由*MapPageRoute*方法*路由*类：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="f8a2c-494">ASP.NET 4 引入了*MapPageRoute*方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="f8a2c-495">下面的示例与上一示例所示的 SearchRoute 定义是等效，但使用*PageRouteHandler*类。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="f8a2c-496">示例中的代码映射到一个物理页的路由 (在第一个路由，到`~/search.aspx`)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="f8a2c-497">第一个的路由定义也指定应从 URL 中提取并传递到页面的参数名术语。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="f8a2c-498">*MapPageRoute*方法支持以下的方法重载：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="f8a2c-499">*MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess）*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="f8a2c-500">*MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值）*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="f8a2c-501">*MapPageRoute （字符串 routeName、 字符串 routeUrl、 字符串 physicalFile、 bool checkPhysicalUrlAccess、 RouteValueDictionary 默认值、 RouteValueDictionary 约束）*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="f8a2c-502">*CheckPhysicalUrlAccess*参数指定该路由是否应检查路由到的物理页的安全权限 (在这种情况下，search.aspx) 以及针对传入 URL 的权限 （在这种情况下，搜索/ {术语})。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="f8a2c-503">如果值*checkPhysicalUrlAccess*是*false*，将进行检查，仅传入 URL 的权限。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="f8a2c-504">在中定义这些权限`Web.config`文件中使用类似如下设置：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="f8a2c-505">在示例配置中，访问被拒绝到物理页`search.aspx`除管理员角色中的所有用户。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="f8a2c-506">当*checkPhysicalUrlAccess*参数设置为*true* （这是其默认值），只有管理员用户允许访问 URL /search/ {术语}，因为物理页 search.aspx 是限制为该角色中的用户。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="f8a2c-507">如果*checkPhysicalUrlAccess*设置为*false*和站点配置中前面的示例所示，将允许所有经过身份验证的用户访问 URL /search/ {术语}。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="f8a2c-508">Web 窗体页中的路由信息的读取</span><span class="sxs-lookup"><span data-stu-id="f8a2c-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="f8a2c-509">在 Web 窗体物理页的代码中，你可以访问路由已从 URL 中提取的信息 (或另一个对象已添加到其他信息*RouteData*对象) 通过使用两个新属性： *HttpRequest.RequestContext*和*Page.RouteData*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="f8a2c-510">(*Page.RouteData*包装*HttpRequest.RequestContext.RouteData*。)下面的示例演示如何使用*Page.RouteData*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="f8a2c-511">代码中提取前面示例路由中定义为术语参数，而传递的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="f8a2c-512">请考虑以下请求 URL:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="f8a2c-513">发出此请求时，"scott"将呈现在 word`search.aspx`页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="f8a2c-514">访问在标记中的路由信息</span><span class="sxs-lookup"><span data-stu-id="f8a2c-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="f8a2c-515">上一节中所述的方法演示如何在 Web 窗体页中的代码中获取路由数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="f8a2c-516">你还可以使用相同的信息有权访问在标记中的表达式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="f8a2c-517">表达式生成器是一种功能强大且简洁的方式来使用声明性代码。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="f8a2c-518">(有关详细信息，请参阅文章[Express 自己与自定义表达式生成器](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)Phil Haack 博客上。)</span><span class="sxs-lookup"><span data-stu-id="f8a2c-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="f8a2c-519">ASP.NET 4 包含两个新的表达式生成器用于 Web 窗体路由。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="f8a2c-520">下面的示例演示如何使用它们。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="f8a2c-521">在示例中， *RouteUrl*表达式用于定义基于路由的参数的 URL。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="f8a2c-522">这样可以节省你无需编写硬编码的完整 URL 向的标记，并可让你更高版本更改 URL 结构，而无需对此链接的任何更改。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="f8a2c-523">根据前面定义的路由，此标记将生成以下 URL:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="f8a2c-524">ASP.NET 自动工作出正确的路由 （即，它生成正确的 URL） 基于输入参数。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="f8a2c-525">您还可以包含在表达式中，这样就可以指定要使用的路由的路由名称。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="f8a2c-526">下面的示例演示如何使用*RouteValue*表达式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="f8a2c-527">包含此控件的页在运行时，标签中显示的值"scott"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="f8a2c-528">*RouteValue*表达式可以很容易地在标记中，使用路由数据，而且它避免了无需使用更复杂的 Page.RouteData["x"] 在标记中的语法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="f8a2c-529">使用适用于数据源控件参数路线数据</span><span class="sxs-lookup"><span data-stu-id="f8a2c-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="f8a2c-530">*RouteParameter*类可作为数据源控件中的查询的参数值指定路由数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="f8a2c-531">它[工作方式非常类似于](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)类，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="f8a2c-532">在这种情况下，路由参数术语的值将用于@companyname中的参数<em>选择</em>语句。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the <em>Select</em> statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="f8a2c-533">设置客户端 Id</span><span class="sxs-lookup"><span data-stu-id="f8a2c-533">Setting Client IDs</span></span>

<span data-ttu-id="f8a2c-534">新*ClientIDMode*属性解决了长期存在的问题，在 ASP.NET 中，即如何控件创建*id*所呈现元素的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="f8a2c-535">了解*id*呈现元素的属性是重要信息： 如果你的应用程序包括引用这些元素的客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="f8a2c-536">*Id*中呈现 Web 服务器控件的 HTML 特性基于生成*ClientID*的控件属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="f8a2c-537">ASP.NET 4 中，生成的算法之前*id*属性从*ClientID*属性已要连接的命名容器 （如果有） 替换为 ID，并在重复 （作为中控件的情况下数据控件），以添加前缀和序列号。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="f8a2c-538">虽然这始终有保证的页中的控件 Id 是唯一的该算法导致了控制未可预测，并且因此非常难以在客户端脚本中引用的 Id。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="f8a2c-539">新*ClientIDMode*属性，允许您指定更确切地说如何的客户端 ID 生成的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="f8a2c-540">你可以设置*ClientIDMode*任何控件，包括页的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="f8a2c-541">可能的设置如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-541">Possible settings are the following:</span></span>

- <span data-ttu-id="f8a2c-542">*AutoID* – 这相当于生成的算法*ClientID*的 ASP.NET 的早期版本中使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="f8a2c-543">*静态*– 这是指定*ClientID*值将为而无需连接的命名容器的父 Id 的 ID 相同。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="f8a2c-544">这可在 Web 用户控件中。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="f8a2c-545">Web 用户控件可以位于不同页上和不同的容器控件中，因为它可能很难编写使用控件的客户端脚本*AutoID*算法因为你无法预测的 ID 值将是什么.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="f8a2c-546">*可预测*– 此选项主要用于在使用重复的模板的数据控件中使用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="f8a2c-547">它将连接在一起的控件的命名容器，但生成的 ID 属性*ClientID*值不包含字符串，例如"ctlxxx"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="f8a2c-548">此设置与结合工作*ClientIDRowSuffix*的控件属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="f8a2c-549">你设置*ClientIDRowSuffix*生成使用的后缀数据字段中，名称和该字段的值的属性*ClientID*值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="f8a2c-550">通常使用作为数据记录的主键*ClientIDRowSuffix*值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="f8a2c-551">*继承*– 此设置是控件的默认行为; 它指定控件的 ID 生成，并为其父项相同。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="f8a2c-552">你可以设置*ClientIDMode*页级别的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="f8a2c-553">这定义了默认的*ClientIDMode*当前页中的所有控件的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="f8a2c-554">默认值*ClientIDMode*页级别的值是*AutoID*，也是默认值*ClientIDMode*控件级别的值是*继承*.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="f8a2c-555">因此，如果不执行在代码中任何位置设置此属性，则所有控件将都默认为*AutoID*算法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="f8a2c-556">在中设置的页级别值*@ Page*指令，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="f8a2c-557">你还可以设置*ClientIDMode*在配置文件中，在计算机级别或应用程序级别的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="f8a2c-558">这定义了默认的*ClientIDMode*设置应用程序中的所有页中的所有控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="f8a2c-559">如果在计算机级别设置的值，它定义了默认的*ClientIDMode*在该计算机上的所有 Web 站点设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="f8a2c-560">下面的示例演示*ClientIDMode*在配置文件中设置：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="f8a2c-561">如前文所述的值*ClientID*属性从命名容器派生的控件的父级。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="f8a2c-562">在某些情况下，例如，当你使用主页面，控件最终可能会具有 Id 类似于以下中呈现 HTML:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="f8a2c-563">即使*输入*显示在标记中的元素 (从*文本框中*控件) 是仅有两个命名的容器在页中的深度 (嵌套*ContentPlaceholder*控件)，由于处理母版页的方法，最终结果是如下所示的控件 ID:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="f8a2c-564">此 ID 保证在页上，必须唯一，但不必要地长的大多数情况下。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="f8a2c-565">假设你想要减少的呈现 ID 的长度并更好地控制如何生成 ID。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="f8a2c-566">（例如，你想要消除"ctlxxx"前缀。）实现此目的的最简单方法是通过设置*ClientIDMode*属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="f8a2c-567">在此示例中， *ClientIDMode*属性设置为*静态*的最外面*NamingPanel*元素，并设置为*可预测*为内部*NamingControl*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="f8a2c-568">这些设置会导致 （了页面和主页上的 rest 假定要如下所示前面的示例相同） 的以下标记：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="f8a2c-569">*静态*设置的效果的重置包含最外面的任何控件的命名层次结构*NamingPanel*元素，并消除*ContentPlaceHolder*和*母版页*Id 从生成的 id。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="f8a2c-570">(*名称*呈现元素的属性不受影响，因此正常的 ASP.NET 功能保留的事件中，查看状态，依次类推。)重置命名层次结构会产生副作用是，即使移动的标记*NamingPanel*为另一种元素*ContentPlaceholder*控件，呈现客户端 Id 保持不变。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a2c-571">请注意它是由您来确保呈现的控件 Id 是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="f8a2c-572">如果它们不是，它能中断为单个 HTML 元素，如客户端需要唯一的 Id 的任何功能*document.getElementById*函数。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="f8a2c-573">在数据绑定控件中创建可预测的客户端 Id</span><span class="sxs-lookup"><span data-stu-id="f8a2c-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="f8a2c-574">*ClientID*为旧算法的数据绑定列表控件中的控件可以是生成的值长，不是真正可预测。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="f8a2c-575">*ClientIDMode*功能可以帮助你进行更大的控制权生成通过这些 Id。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="f8a2c-576">下面的示例中的标记包括*ListView*控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="f8a2c-577">在前面的示例中， *ClientIDMode*和*RowClientIDRowSuffix*标记中设置属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="f8a2c-578">*ClientIDRowSuffix*属性可以使用仅在数据绑定控件中，并且其行为不同，具体取决于哪个控件使用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="f8a2c-579">差异如下：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-579">The differences are these:</span></span>

- <span data-ttu-id="f8a2c-580">*GridView*控件 — 你可以在数据源中，在运行时创建客户端 Id 组合的指定一个或多个列的名称。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="f8a2c-581">例如，如果你设置*RowClientIDRowSuffix*为"产品名称，ProductId"，呈现的元素将具有类似于下面的格式控件 Id:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="f8a2c-582">*ListView*控件 — 你可以指定追加到客户端 id。 的数据源中的单个列</span><span class="sxs-lookup"><span data-stu-id="f8a2c-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="f8a2c-583">例如，如果你设置*ClientIDRowSuffix*呈现的控件 Id 将为"产品名称"，具有一种格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="f8a2c-584">在这种情况下尾随 1 派生自当前数据项的产品 ID。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="f8a2c-585">*转发器*控件 — 此控件不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="f8a2c-586">在*中继器*使用控件，当前行的索引。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="f8a2c-587">当你使用 ClientIDMode ="可预测"替换*中继器*控制，客户端 Id，将生成具有以下格式：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="f8a2c-588">尾随 0 是当前行的索引。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="f8a2c-589">*FormView*和*说明*控件不显示多个行，因此它们不支持*ClientIDRowSuffix*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="f8a2c-590">保持数据控件中的行选择</span><span class="sxs-lookup"><span data-stu-id="f8a2c-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="f8a2c-591">*GridView*和*ListView*控件可以让用户选择一行。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="f8a2c-592">在以前版本的 ASP.NET，具有已选择基于在页上的行索引。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="f8a2c-593">例如，如果你选择第 1 页上的第三个项，并且然后将其移动到第 2 页，选择该页面上的第三个项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="f8a2c-594">仅在.NET Framework 3.5 SP1 中的动态数据项目中，最初已支持持久化的选择。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="f8a2c-595">启用此功能后，当前所选的项取决于项的数据键。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="f8a2c-596">这意味着，如果您选择的第三个行，第 1 页上，并移动到第 2 页，则不选择在第 2 页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="f8a2c-597">当您移回到第 1 页时，第三行仍处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="f8a2c-598">现在支持持久化的选择*GridView*和*ListView*使用的所有项目中的控件*EnablePersistedSelection*属性，如下所示下面的示例：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="f8a2c-599">ASP.NET 图表控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="f8a2c-600">ASP.NET*图表*控件扩展.NET Framework 中的数据可视化产品。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="f8a2c-601">使用*图表*控件，你可以创建具有直观和极具视觉表现力的图表进行复杂的统计或财务分析的 ASP.NET 页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="f8a2c-602">ASP.NET*图表*控件作为外接程序引入到.NET Framework 版本 3.5 SP1 版本，.NET Framework 4 版本的一部分。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="f8a2c-603">控件包括以下功能：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-603">The control includes the following features:</span></span>

- <span data-ttu-id="f8a2c-604">35 种不同的图表类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-604">35 distinct chart types.</span></span>
- <span data-ttu-id="f8a2c-605">无限的数量的图表区、 标题、 图例和批注。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="f8a2c-606">所有图表元素的外观设置了多种不同。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="f8a2c-607">对于大多数图表类型的三维支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="f8a2c-608">可以自动调整数据点的智能数据标签。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="f8a2c-609">条带线、 刻度分隔线和对数缩放。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="f8a2c-610">包含 50 多个用于数据分析和转换的财务和统计公式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="f8a2c-611">简单绑定和操作中的图表数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="f8a2c-612">对常见数据格式，例如日期、 时间和货币的支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="f8a2c-613">交互性和事件驱动的自定义，包括客户端的支持，请单击使用 Ajax 事件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="f8a2c-614">状态管理。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-614">State management.</span></span>
- <span data-ttu-id="f8a2c-615">二进制流。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-615">Binary streaming.</span></span>

<span data-ttu-id="f8a2c-616">下图显示由 ASP.NET 图表控件的财务图表的示例。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="f8a2c-617">图 2: ASP.NET 图表控件示例</span><span class="sxs-lookup"><span data-stu-id="f8a2c-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="f8a2c-618">有关如何使用 ASP.NET 图表控件中的更多示例上下载的示例代码[Microsoft 图表控件的示例环境](https://go.microsoft.com/fwlink/?LinkId=128300)MSDN 网站上的页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="f8a2c-619">你可以找到更多示例的社区内容在[图表控件论坛](https://go.microsoft.com/fwlink/?LinkId=128713)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="f8a2c-620">将图表控件添加到 ASP.NET 页</span><span class="sxs-lookup"><span data-stu-id="f8a2c-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="f8a2c-621">下面的示例演示如何将添加*图表*到 ASP.NET 页使用标记的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="f8a2c-622">在示例中，*图表*控件生成静态数据点的柱形图。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="f8a2c-623">使用三维图表</span><span class="sxs-lookup"><span data-stu-id="f8a2c-623">Using 3-D Charts</span></span>

<span data-ttu-id="f8a2c-624">*图表*控件包含*ChartAreas*集合，其中可包含*ChartArea*定义图表区的特征的对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="f8a2c-625">例如，若要使用三维图表区，请使用*Area3DStyle*属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="f8a2c-626">下图显示具有四个系列的三维图表*栏*图表类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="f8a2c-627">图 3： 三维条形图</span><span class="sxs-lookup"><span data-stu-id="f8a2c-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="f8a2c-628">使用刻度分隔线和对数刻度</span><span class="sxs-lookup"><span data-stu-id="f8a2c-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="f8a2c-629">刻度分隔线和对数刻度是两种方法可以向图表中添加复杂。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="f8a2c-630">这些功能是特定于每个轴在图表区。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="f8a2c-631">例如，若要在图表区的主 Y 轴上使用这些功能，使用*AxisY.IsLogarithmic*和*ScaleBreakStyle*中的属性*ChartArea*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="f8a2c-632">下面的代码段演示如何使用刻度分隔线的主 Y 轴上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="f8a2c-633">下图显示 Y 轴具有启用刻度分隔线。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="f8a2c-634">图 4： 刻度分隔线</span><span class="sxs-lookup"><span data-stu-id="f8a2c-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="f8a2c-635">用 QueryExtender 控件筛选数据</span><span class="sxs-lookup"><span data-stu-id="f8a2c-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="f8a2c-636">创建数据驱动的网页的开发人员的非常常见任务是筛选数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="f8a2c-637">这通常已执行通过构建*其中*子句在数据源控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="f8a2c-638">此方法可能比较复杂，在某些情况下*其中*语法不允许您充分利用基础数据库的完整功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="f8a2c-639">为简化筛选操作，新*QueryExtender*控件已添加 ASP.NET 4 中。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="f8a2c-640">此控件可添加到*EntityDataSource*或*LinqDataSource*以便筛选由这些控件返回的数据的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="f8a2c-641">因为*QueryExtender*控件依赖于 LINQ、 应用筛选器是在数据库服务器上之前的数据发送到页上，这会导致非常高效的操作。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="f8a2c-642">*QueryExtender*控件支持的广泛的筛选器选项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="f8a2c-643">以下部分介绍了这些选项，并提供如何使用它们的示例。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="f8a2c-644">搜索</span><span class="sxs-lookup"><span data-stu-id="f8a2c-644">Search</span></span>

<span data-ttu-id="f8a2c-645">搜索选项时， *QueryExtender*控件执行搜索指定字段中。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="f8a2c-646">在下面的示例中，该控件使用输入中 TextBoxSearch 控件并将其内容搜索的文本`ProductName`和`Supplier.CompanyName`中从返回的数据的列*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="f8a2c-647">范围</span><span class="sxs-lookup"><span data-stu-id="f8a2c-647">Range</span></span>

<span data-ttu-id="f8a2c-648">范围选项类似于搜索选项，但指定要定义的范围的值对。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="f8a2c-649">在下面的示例中， *QueryExtender*控制搜索`UnitPrice`中返回的数据列*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="f8a2c-650">从页上的 TextBoxFrom 和 TextBoxTo 控件中读取的范围。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="f8a2c-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="f8a2c-651">PropertyExpression</span></span>

<span data-ttu-id="f8a2c-652">属性表达式选项，可以定义为属性值的比较。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="f8a2c-653">如果表达式计算结果为*true*，返回正在读取的数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="f8a2c-654">在下面的示例中， *QueryExtender*控件通过比较中的数据来筛选数据`Discontinued`从 CheckBoxDiscontinued 控件在页上的值的列。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="f8a2c-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="f8a2c-655">CustomExpression</span></span>

<span data-ttu-id="f8a2c-656">最后，可以指定要使用的自定义表达式*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="f8a2c-657">此选项，你可以调用一个函数中定义自定义筛选器逻辑页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="f8a2c-658">下面的示例演示如何以声明方式指定的自定义表达式*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="f8a2c-659">下面的示例演示通过调用的自定义函数*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="f8a2c-660">在这种情况下，而不是使用包含的数据库查询*其中*子句，代码使用 LINQ 查询来筛选的数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="f8a2c-661">以下示例演示只有一个表达式中正在使用*QueryExtender*一次的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="f8a2c-662">但是，您可以包含多个表达式内的*QueryExtender*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="f8a2c-663">Html 编码的代码表达式</span><span class="sxs-lookup"><span data-stu-id="f8a2c-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="f8a2c-664">使用依赖于某些 ASP.NET 站点 （尤其是使用 ASP.NET MVC) `<%` =  `expression %>` （通常称为"代码问题"） 的语法为一些文本写入响应。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="f8a2c-665">当你使用的代码表达式时，很容易忘记进行 HTML 编码的文本，如果文本来自用户输入，它可能会导致页打开与 XSS （跨站点脚本） 攻击。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="f8a2c-666">ASP.NET 4 中引入的代码表达式的以下新语法：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="f8a2c-667">此语法使用写入到响应时，HTML 编码，默认情况下。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="f8a2c-668">这个新的表达式有效地转换为以下：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="f8a2c-669">例如， &lt;%: 请求"UserInput"%&gt;执行 HTML 编码的值*请求"UserInput"*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="f8a2c-670">此功能旨在使将旧语法的所有实例替换为新的语法，以便你并不强制的每一个步骤决定使用哪一个。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="f8a2c-671">但是，一些情况下在其中输出的文本要作为 HTML，或已进行编码时，在这种情况下这可能导致双重解码。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="f8a2c-672">对于这些情况下，ASP.NET 4 中引入了新接口， *IHtmlString*，以及具体实现， *HtmlString*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="f8a2c-673">这些类型的实例，您可以指示，返回值是已正确编码 （或否则检查） 用于显示为 HTML，且，因此值不应为 HTML 编码试。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="f8a2c-674">例如，以下不应为 （而不是） HTML 编码：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="f8a2c-675">如果您运行的 ASP.NET 4，已经过更新以使用此新语法，以便它们不双编码，但只有 ASP.NET MVC 2 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="f8a2c-676">当你运行使用 ASP.NET 3.5 SP1 的应用程序，则此新语法不起作用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="f8a2c-677">请记住这并不保证从 XSS 攻击的保护。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="f8a2c-678">例如，使用不是用引号引起来的属性值的 HTML 可以包含仍容易的用户输入。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="f8a2c-679">请注意，ASP.NET 控件和 ASP.NET MVC 帮助器的输出始终包含属性值用引号引起来，这是建议的方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="f8a2c-680">同样，此语法不执行 JavaScript 编码，如当你创建 JavaScript 字符串根据用户输入。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="f8a2c-681">项目模板更改</span><span class="sxs-lookup"><span data-stu-id="f8a2c-681">Project Template Changes</span></span>

<span data-ttu-id="f8a2c-682">在早期版本的 ASP.NET，当你使用 Visual Studio 创建新网站项目或 Web 应用程序项目，生成的项目包含仅 Default.aspx 页上，默认`Web.config`文件，和`App_Data`文件夹，如以下所示图：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="f8a2c-683">Visual Studio 也支持空网站项目类型，不包含任何文件根本下, 图中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="f8a2c-684">结果是，对于初学者，很少的指南如何生成生产型 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="f8a2c-685">因此，ASP.NET 4 中引入了三个新模板，另一个为空的 Web 应用程序项目，每个 Web 应用程序和网站项目。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="f8a2c-686">空 Web 应用程序模板</span><span class="sxs-lookup"><span data-stu-id="f8a2c-686">Empty Web Application Template</span></span>

<span data-ttu-id="f8a2c-687">顾名思义，空 Web 应用程序模板是精简的 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="f8a2c-688">下图中所示，可以从 Visual Studio 的新项目对话框中，选择此项目模板：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="f8a2c-689">([单击以查看实际尺寸的图像](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="f8a2c-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="f8a2c-690">在创建空的 ASP.NET Web 应用程序时，Visual Studio 将创建以下文件夹布局：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="f8a2c-691">这是类似于空网站布局从早期版本的 ASP.NET，有一个例外。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="f8a2c-692">在 Visual Studio 2010 中，空 Web 应用程序和空网站项目包含以下最小`Web.config`包含 Visual Studio 用于标识的项目所面向的 framework 的信息的文件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="f8a2c-693">如果没有此*targetFramework*属性，Visual Studio 默认值为面向.NET Framework 2.0，以打开较旧的应用程序时保持兼容性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="f8a2c-694">Web 应用程序和网站项目模板</span><span class="sxs-lookup"><span data-stu-id="f8a2c-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="f8a2c-695">其他两个新项目模板随附 Visual Studio 2010 包含重大更改。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="f8a2c-696">下图显示在创建新的 Web 应用程序项目时创建的项目布局。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="f8a2c-697">（网站项目中的布局是几乎相同的。）</span><span class="sxs-lookup"><span data-stu-id="f8a2c-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="f8a2c-698">该项目包括一个未在早期版本中创建的文件数。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="f8a2c-699">此外，新的 Web 应用程序项目被配置为具有基本成员资格功能，这样就可以快速开始保护新的应用程序的访问。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="f8a2c-700">由于此包含`Web.config`文件新的项目包括用于配置成员资格、 角色和配置文件的项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="f8a2c-701">下面的示例演示`Web.config`新的 Web 应用程序项目文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="f8a2c-702">(在这种情况下， *roleManager*处于禁用状态。)</span><span class="sxs-lookup"><span data-stu-id="f8a2c-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="f8a2c-703">([单击以查看实际尺寸的图像](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="f8a2c-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="f8a2c-704">项目还包含第二个`Web.config`文件中`Account`目录。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="f8a2c-705">第二个配置文件提供一种方法来确保安全访问的 ChangePassword.aspx 页非-已登录的用户。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="f8a2c-706">下面的示例演示的第二个内容`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="f8a2c-707">默认情况下，新的项目模板中创建的页还包含比在早期版本中的其他内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="f8a2c-708">项目包含一个默认母版页和 CSS 文件，并且默认页 (Default.aspx) 配置为使用母版页默认情况下。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="f8a2c-709">结果是，如果首次运行的 Web 应用程序或网站，默认 （主） 页将已正常运行。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="f8a2c-710">事实上，它是类似于你启动新的 MVC 应用程序时，将显示默认页。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="f8a2c-711">([单击以查看实际尺寸的图像](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="f8a2c-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="f8a2c-712">这些更改的项目模板的目的是提供有关如何开始生成新的 Web 应用程序的指导。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="f8a2c-713">在语义上正确，严格 XHTML 1.0 符合标记并且使用 CSS 指定的布局，在模板中的页体现生成 ASP.NET 4 Web 应用程序的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="f8a2c-714">默认页还具有你可以轻松自定义的两列布局。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="f8a2c-715">例如，假设，为新的 Web 应用程序想要更改某些颜色和插入我的 ASP.NET 应用程序徽标代替你公司的徽标。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="f8a2c-716">若要执行此操作，你创建下的新建一个目录`Content`来存储你的徽标图像：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="f8a2c-717">若要将映像添加到页面中，然后打开`Site.Master`文件中，查找其中我的 ASP.NET 应用程序文本定义，并将其替换*映像*元素其*src*属性设置为新的徽标映像，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="f8a2c-718">([单击以查看实际尺寸的图像](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="f8a2c-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="f8a2c-719">然后，可以进入 Site.css 文件和修改 CSS 类定义，以更改页的背景色以及的标头。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="f8a2c-720">这些更改的结果是，你可以显示一个包含很少的工作量的自定义的主页：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="f8a2c-721">([单击以查看实际尺寸的图像](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="f8a2c-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="f8a2c-722">CSS 改进</span><span class="sxs-lookup"><span data-stu-id="f8a2c-722">CSS Improvements</span></span>

<span data-ttu-id="f8a2c-723">ASP.NET 4 中主要区域之一是工作的帮助呈现符合最新的 HTML 标准的 HTML。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="f8a2c-724">这包括对 ASP.NET Web 服务器控件如何使用 CSS 样式更改。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="f8a2c-725">呈现的兼容性设置</span><span class="sxs-lookup"><span data-stu-id="f8a2c-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="f8a2c-726">默认情况下，当 Web 应用程序或网站面向.NET Framework 4， *controlRenderingCompatibilityVersion*属性*页*元素设置为"4.0"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="f8a2c-727">在计算机级别中定义此元素`Web.config`文件和默认情况下适用于所有 ASP.NET 4 应用程序：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="f8a2c-728">值*controlRenderingCompatibility*是一个字符串，它允许潜在新版本定义在将来的版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="f8a2c-729">在当前版本中，此属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="f8a2c-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="f8a2c-730">"3.5".</span></span> <span data-ttu-id="f8a2c-731">此设置指示旧的呈现和标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="f8a2c-732">标记由控件呈现为 100%向后兼容，以及设置的*xhtmlConformance*遵循属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="f8a2c-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="f8a2c-733">"4.0".</span></span> <span data-ttu-id="f8a2c-734">如果该属性具有此设置，ASP.NET Web 服务器控件将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="f8a2c-735">*XhtmlConformance*属性始终被视为"Strict"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="f8a2c-736">因此，控件呈现 XHTML 1.0 Strict 标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="f8a2c-737">禁用非输入控件不再呈现无效的样式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="f8a2c-738">*div*围绕隐藏的字段的元素的现在风格，因此它们不会干扰用户创建 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="f8a2c-739">菜单控件呈现在语义上正确，并符合辅助功能准则的标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="f8a2c-740">验证控件不会呈现内联样式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="f8a2c-741">控制以前呈现边框 ="0"(从 ASP.NET 派生的控件*表*控制和 ASP.NET*映像*控件) 不再呈现此属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="f8a2c-742">禁用控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-742">Disabling Controls</span></span>

<span data-ttu-id="f8a2c-743">在 ASP.NET 3.5 SP1 和更早版本中，框架呈现*禁用*特性的 HTML 标记中任何控制其*已启用*属性设置为*false*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="f8a2c-744">但是，根据 HTML 4.01 规范，仅*输入*元素应具有此属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="f8a2c-745">在 ASP.NET 4 中，你可以设置*controlRenderingCompatabilityVersion*属性设置为"3.5"，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-745">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="f8a2c-746">你可能会创建标记*标签*如下所示，禁用控件的控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="f8a2c-747">*标签*控件将会设置以下 HTML 呈现：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="f8a2c-748">在 ASP.NET 4 中，你可以设置*controlRenderingCompatabilityVersion*为"4.0"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-748">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* to "4.0".</span></span> <span data-ttu-id="f8a2c-749">在这种情况下，仅控制该呈现*输入*元素将呈现*禁用*属性时控件的*已启用*属性设置为*false*.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="f8a2c-750">无法呈现 HTML 控件*输入*元素改为呈现*类*引用可用于定义控件的已禁用的面貌 CSS 类的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="f8a2c-751">例如，*标签*前面示例中所示的控件也会生成以下标记：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="f8a2c-752">指定对于此控件的类的默认值是"aspNetDisabled"。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="f8a2c-753">但是，可以通过设置静态更改此默认值*DisabledCssClass*的静态属性*WebControl*类。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="f8a2c-754">为控件开发人员要使用的特定控件的行为也可以定义使用*SupportsDisabledAttribute*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="f8a2c-755">隐藏 div 元素周围隐藏字段</span><span class="sxs-lookup"><span data-stu-id="f8a2c-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="f8a2c-756">ASP.NET 2.0 和更高版本呈现特定于系统的隐藏的字段 (如*隐藏*元素，用于存储视图状态信息) 内*div*为了遵守 XHTML 标准元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="f8a2c-757">但是，这会导致问题，如果 CSS 规则影响*div*页上的元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="f8a2c-758">例如，这会导致在页中显示一个像素行大约隐藏*div*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="f8a2c-759">在 ASP.NET 4 中， *div*将由 ASP.NET 生成的隐藏的字段括起来的元素添加 CSS 类引用，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="f8a2c-760">然后可以定义仅适用于的 CSS 类*隐藏*元素都由 ASP.NET，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="f8a2c-761">模板化控件呈现的外部表</span><span class="sxs-lookup"><span data-stu-id="f8a2c-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="f8a2c-762">默认情况下，以下支持模板的 ASP.NET Web 服务器控件自动将封装在用于将内联样式应用的外部表：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="f8a2c-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-763">*FormView*</span></span>
- <span data-ttu-id="f8a2c-764">*Login*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-764">*Login*</span></span>
- <span data-ttu-id="f8a2c-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="f8a2c-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-766">*ChangePassword*</span></span>
- <span data-ttu-id="f8a2c-767">*Wizard*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-767">*Wizard*</span></span>
- <span data-ttu-id="f8a2c-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="f8a2c-768">*CreateUserWizard*</span></span>

<span data-ttu-id="f8a2c-769">名为的新属性*RenderOuterTable*已添加到允许的外部表，从标记要删除这些控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="f8a2c-770">例如，考虑下面的示例对*FormView*控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="f8a2c-771">此标记将呈现到页上，其中包括 HTML 表的以下输出：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="f8a2c-772">若要防止呈现表，可以设置*FormView*控件的*RenderOuterTable*属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="f8a2c-773">前面的示例呈现以下输出，而不*表*， *tr*，和*td*元素：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="f8a2c-774">内容</span><span class="sxs-lookup"><span data-stu-id="f8a2c-774">Content</span></span>


<span data-ttu-id="f8a2c-775">此增强功能可以更轻松到样式的控件内容的使用 CSS，因为无意外的标记所呈现控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a2c-776">请注意此更改不支持 Visual Studio 2010 设计器中中的自动套用格式函数，因为不再有*表*元素可以承载生成的自动套用格式选项的样式特性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="f8a2c-777">ListView 控件增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-777">ListView Control Enhancements</span></span>

<span data-ttu-id="f8a2c-778">*ListView*控件已便于在 ASP.NET 4 中使用。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="f8a2c-779">指定包含一个具有已知 ID 的服务器控件的布局模板所需的控件的早期版本</span><span class="sxs-lookup"><span data-stu-id="f8a2c-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="f8a2c-780">以下标记显示如何使用的典型示例*ListView* ASP.NET 3.5 中的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="f8a2c-781">在 ASP.NET 4 中， *ListView*控件不需要的布局模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="f8a2c-782">在前面的示例所示的标记可以替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="f8a2c-783">按和说明如何增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="f8a2c-784">可以在 ASP.NET 3.5 中，指定布局*按*和*说明如何*使用以下两个设置：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="f8a2c-785">*流*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-785">*Flow*.</span></span> <span data-ttu-id="f8a2c-786">控件呈现*跨越*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="f8a2c-787">*表*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-787">*Table*.</span></span> <span data-ttu-id="f8a2c-788">控件呈现*表*元素以包含其内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="f8a2c-789">下面的示例演示上述每个控件的标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="f8a2c-790">默认情况下，控件将呈现 HTML 类似于以下：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="f8a2c-791">因为这些控件包含列表项呈现在语义上是正确的 HTML，它们应呈现其内容使用 HTML 列表 (*li*) 元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="f8a2c-792">这简化它为读取网页使用辅助技术，并使控件能够更轻松地使用 CSS 样式的用户。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="f8a2c-793">在 ASP.NET 4 中，*按*和*说明如何*控件支持的以下新值*适用*属性：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="f8a2c-794">*OrderedList* – 内容呈现为*li*中的元素*ol*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="f8a2c-795">*UnorderedList* – 内容呈现为*li*中的元素*ul*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="f8a2c-796">下面的示例演示如何使用这些新值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="f8a2c-797">前面的标记生成的以下 HTML:</span><span class="sxs-lookup"><span data-stu-id="f8a2c-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="f8a2c-798">请注意，是否你设置*适用*到*OrderedList*或*UnorderedList*、 *RepeatDirection*属性不再可用，并将如果已在标记或代码中设置的属性，则引发运行时异常。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="f8a2c-799">属性将具有任何值，因为这些控件的可视布局定义改为使用 CSS。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="f8a2c-800">菜单控件改进</span><span class="sxs-lookup"><span data-stu-id="f8a2c-800">Menu Control Improvements</span></span>

<span data-ttu-id="f8a2c-801">ASP.NET 4 之前*菜单*控件呈现的 HTML 表的一系列。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="f8a2c-802">这变得更难应用 CSS 样式外部设置内联属性并且也不符合辅助功能标准。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="f8a2c-803">在 ASP.NET 4 中，则控件现在呈现使用未经排序的列表和列表元素组成的语义标记的 HTML。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="f8a2c-804">下面的示例演示在 ASP.NET 页中标记*菜单*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="f8a2c-805">如果页面呈现时，控件便会生成以下 HTML ( *onclick*代码已被省略为清楚起见):</span><span class="sxs-lookup"><span data-stu-id="f8a2c-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="f8a2c-806">呈现除改进外，已使用焦点管理得到改善菜单的键盘导航。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="f8a2c-807">当*菜单*控件获得焦点时，你可以使用箭头键导航元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="f8a2c-808">*菜单*控件现在还将附加访问的丰富 internet 应用程序 (ARIA) 角色和属性如下[机翼](http://www.w3.org/TR/wai-aria-practices/#menu "菜单 ARIA 准则")以改进可访问性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="f8a2c-809">菜单控件的样式呈现的样式块中的顶部的页上，而不是根据呈现的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="f8a2c-810">如果你想要对该控件的样式的完全控制，则可以设置新*IncludeStyleBlock*属性*false*，在这种情况下不发出样式块。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="f8a2c-811">使用此属性的一种方法是使用中的 Visual Studio 设计器的自动套用格式功能来设置菜单的外观。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="f8a2c-812">然后可以运行页上，打开页面源文件中，，然后将呈现的样式块复制到外部 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="f8a2c-813">在 Visual Studio 中，撤消的样式和集*IncludeStyleBlock*到*false*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="f8a2c-814">结果是使用外部样式表中的样式定义菜单外观。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="f8a2c-815">向导和 CreateUserWizard 控件</span><span class="sxs-lookup"><span data-stu-id="f8a2c-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="f8a2c-816">ASP.NET*向导*和*CreateUserWizard*控件支持使你能够定义他们呈现的 HTML 的模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="f8a2c-817">(*CreateUserWizard*派生自*向导*。)下面的示例演示的标记完全模板化*CreateUserWizard*控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="f8a2c-818">控件上呈现 HTML 类似如下：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="f8a2c-819">在 ASP.NET 3.5 SP1 中，尽管您可以更改的模板内容，但你仍具有有限的控制的输出*向导*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="f8a2c-820">在 ASP.NET 4 中，你可以创建*LayoutTemplate*模板和插入*占位符*控制 （使用保留的名称） 以指定你希望如何*向导控件*来呈现。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="f8a2c-821">下面的示例演示了此过程：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="f8a2c-822">该示例包含以下名为中的占位符*LayoutTemplate*元素：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="f8a2c-823">*headerPlaceholder* – 在运行时，这替换的内容*HeaderTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="f8a2c-824">*sideBarPlaceholder* – 在运行时，这替换的内容*SideBarTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="f8a2c-825">*wizardStepPlaceHolder* – 在运行时，这替换的内容*WizardStepTemplate*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="f8a2c-826">*navigationPlaceholder* – 在运行时，这替换为已定义的任何导航模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="f8a2c-827">在以下示例中使用占位符的标记的以下 HTML 呈现 （而不实际的模板中定义的内容）：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="f8a2c-828">是现在不是用户定义的唯一 HTML 是*跨越*元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="f8a2c-829">(我们预计这在将来版本中，即使*跨越*元素将不会呈现。)现在可以完全控制由生成的几乎所有内容*向导*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="f8a2c-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f8a2c-830">ASP.NET MVC</span></span>

<span data-ttu-id="f8a2c-831">ASP.NET MVC 引入了作为外接程序框架到 ASP.NET 3.5 SP1 在 2009 年 3 月中。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="f8a2c-832">Visual Studio 2010 包括 ASP.NET MVC 2，其中包括新特性和功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="f8a2c-833">区域支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-833">Areas Support</span></span>

<span data-ttu-id="f8a2c-834">区域，你可以组控制器和视图到相对独立于其他部分中的大型应用程序的部分。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="f8a2c-835">每个区域可以作为一个单独的 ASP.NET MVC 项目，然后可以引用的主应用程序实现。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="f8a2c-836">这可帮助管理复杂性，在生成大型应用程序时，并使其便于在单个应用程序协同工作的多个团队。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="f8a2c-837">数据注释属性验证支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="f8a2c-838">*DataAnnotations*属性，可以通过使用元数据特性附加到模型的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="f8a2c-839">*DataAnnotations* ASP.NET 3.5 SP1 中的 ASP.NET 动态数据中引入了属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="f8a2c-840">这些特性已集成到默认的模型联编程序，提供的元数据驱动方法验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="f8a2c-841">模板化帮助器</span><span class="sxs-lookup"><span data-stu-id="f8a2c-841">Templated Helpers</span></span>

<span data-ttu-id="f8a2c-842">模板化帮助器使你自动相关联的编辑和显示数据类型的模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="f8a2c-843">例如，你可以使用模板帮助程序来指定自动为呈现日期选取器 UI 元素*System.DateTime*值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="f8a2c-844">这是类似于 ASP.NET 动态数据中的字段模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="f8a2c-845">*Html.EditorFor*和*Html.DisplayFor*帮助器方法具有内置支持，对于呈现标准数据类型具有多个属性也为复杂对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="f8a2c-846">他们还进行自定义呈现通过让你将应用这样的数据注释属性*DisplayName*和*ScaffoldColumn*到*ViewModel*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="f8a2c-847">通常，你想要自定义 UI 帮助器甚至可更进一步的输出，并对什么生成具有完全控制。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="f8a2c-848">*Html.EditorFor*和*Html.DisplayFor*帮助器方法支持此使用模板化一种机制，你可以定义外部可以重写的模板和控件呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="f8a2c-849">模板的类可以单独来呈现。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="f8a2c-850">Dynamic Data — 动态数据</span><span class="sxs-lookup"><span data-stu-id="f8a2c-850">Dynamic Data</span></span>

<span data-ttu-id="f8a2c-851">引入了动态数据中中旬 2008年中的.NET Framework 3.5 SP1 版本。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="f8a2c-852">此功能提供了用于创建数据驱动的应用程序，其中包括许多增强功能：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="f8a2c-853">快速生成数据驱动的网站提供 RAD 的体验。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="f8a2c-854">基于数据模型中定义的约束的自动验证。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="f8a2c-855">能够轻松地将更改为中的字段生成的标记*GridView*和*说明*使用是动态的数据项目的一部分的字段模板的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a2c-856">请注意有关详细信息，请参阅[动态数据文档](https://msdn.microsoft.com/library/cc488545.aspx)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>


<span data-ttu-id="f8a2c-857">为 ASP.NET 4 中，动态数据得到增强，为开发人员快速生成数据驱动的网站提供更强大。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="f8a2c-858">启用动态数据的现有项目</span><span class="sxs-lookup"><span data-stu-id="f8a2c-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="f8a2c-859">在.NET Framework 3.5 SP1 中提供的动态数据功能引入新功能如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="f8a2c-860">字段模板 – 这些将基于数据类型的模板提供的数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="f8a2c-861">字段模板提供更简单的方法，以自定义控件的外观的数据比使用为每个字段的模板字段。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="f8a2c-862">验证 – 动态数据允许您在数据类中使用属性来指定为必填的字段、 范围检查、 类型检查、 模式匹配使用正则表达式，之类的常见方案的验证和自定义验证。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="f8a2c-863">由数据控件强制执行验证。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="f8a2c-864">但是，这些功能具有以下要求：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="f8a2c-865">数据访问层必须基于实体框架或 LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="f8a2c-866">唯一的数据源控件支持这些功能已*EntityDataSource*或*LinqDataSource*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="f8a2c-867">功能需要以具有以便具有需要支持功能的所有文件使用的动态数据或动态数据实体模板已创建的 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="f8a2c-868">ASP.NET 4 中的动态数据支持的主要目标是能够对任何 ASP.NET 应用程序的新功能的动态数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="f8a2c-869">下面的示例演示可以利用动态数据功能中的现有的页面的控件的标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="f8a2c-870">在代码页中，必须要使这些控件的动态数据支持添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="f8a2c-871">当*GridView*控件处于编辑模式时，动态数据自动验证输入的数据将采用正确的格式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="f8a2c-872">如果不是这样，将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="f8a2c-873">此功能还提供其他好处，如能够指定默认值插入模式。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="f8a2c-874">不包含动态数据，以实现一个字段，字段的默认值将附加到事件，因此必须查找控件 (使用*FindControl*)，并将其值设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="f8a2c-875">在 ASP.NET 4 中， *EnableDynamicData*调用支持第二个参数，可让你将任何字段默认值传递对象，如本示例中所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="f8a2c-876">声明性 DynamicDataManager 控件语法</span><span class="sxs-lookup"><span data-stu-id="f8a2c-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="f8a2c-877">*DynamicDataManager*管理已得到增强，以便可以将其配置以声明方式，与在 ASP.NET 中，而不是仅在代码的大多数控件一样。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="f8a2c-878">标记*DynamicDataManager*控件的外观如下例所示：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="f8a2c-879">此标记启用动态数据行为中引用的 GridView1 控件*DataControls*部分*DynamicDataManager*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="f8a2c-880">实体模板</span><span class="sxs-lookup"><span data-stu-id="f8a2c-880">Entity Templates</span></span>

<span data-ttu-id="f8a2c-881">实体模板提供自定义而无需创建自定义页的布局的数据的新方法。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="f8a2c-882">页上，模板使用*FormView*控件 (而不是*说明*控件，在早期版本的动态数据中的页模板中使用) 和*DynamicEntity*呈现实体模板的控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="f8a2c-883">这样，可以更好地控制由动态数据呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="f8a2c-884">以下列表显示包含实体模板的新项目目录布局：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="f8a2c-885">`EntityTemplate`目录包含有关如何显示数据模型对象的模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="f8a2c-886">默认情况下，通过使用呈现对象`Default.ascx`模板，它提供类似的创建的标记的标记*说明*使用 ASP.NET 3.5 SP1 中的动态数据控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="f8a2c-887">下面的示例演示的标记`Default.ascx`控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="f8a2c-888">可以编辑默认模板，以更改整个站点的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="f8a2c-889">有用于显示模板、 编辑和插入操作。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="f8a2c-890">新的模板可以添加基于数据对象的名称以更改只是一种类型的对象的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="f8a2c-891">例如，你可以添加以下模板：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="f8a2c-892">该模板可能包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="f8a2c-893">在页面上显示新的实体模板，应使用新*DynamicEntity*控件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="f8a2c-894">在运行时，此控件将被替换实体模板的内容。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="f8a2c-895">下面的标记演示*FormView*中控制`Detail.aspx`页使用实体模板的模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="f8a2c-896">请注意*DynamicEntity*标记中的元素。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="f8a2c-897">新的字段模板的 Url 和电子邮件地址</span><span class="sxs-lookup"><span data-stu-id="f8a2c-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="f8a2c-898">ASP.NET 4 引入了两个新的内置字段模板，`EmailAddress.ascx`和`Url.ascx`。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="f8a2c-899">这些模板用于字段标记为*EmailAddress*或*Url*与*DataType*属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="f8a2c-900">有关*EmailAddress*对象，该字段显示为超链接，通过创建*mailto:*协议。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="f8a2c-901">当用户单击此链接时，打开用户的电子邮件客户端，并创建主干消息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="f8a2c-902">对象类型化为*Url*显示为普通的超链接。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="f8a2c-903">下面的示例演示如何将标记字段。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="f8a2c-904">创建与 DynamicHyperLink 控件的链接</span><span class="sxs-lookup"><span data-stu-id="f8a2c-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="f8a2c-905">动态数据使用.NET Framework 3.5 SP1，以控制用户访问网站时，请参阅最终用户的 Url 中添加新路由功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="f8a2c-906">新*DynamicHyperLink*控件，可以轻松生成的动态数据站点中的页面链接。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="f8a2c-907">下面的示例演示如何使用*DynamicHyperLink*控件：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="f8a2c-908">此标记创建一个链接，指向的列表页`Products`表基于在中定义的路由`Global.asax`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="f8a2c-909">该控件自动使用动态数据页基于默认表名称。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="f8a2c-910">对数据模型中的继承支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="f8a2c-911">实体框架和 LINQ to SQL 可在其数据模型中支持继承。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="f8a2c-912">此示例可能具有的数据库`InsurancePolicy`表。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="f8a2c-913">它可能还包含`CarPolicy`和`HousePolicy`具有相同的字段的表`InsurancePolicy`，然后添加更多的字段。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="f8a2c-914">动态数据已被修改，以了解数据模型中继承的对象，并可以支持继承的表中的基架。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="f8a2c-915">对多对多关系 （仅用于实体框架） 的支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="f8a2c-916">实体框架具有丰富的支持供实现通过上公开为一个集合的关系的表之间的多对多关系*实体*对象。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="f8a2c-917">新`ManyToMany.ascx`和`ManyToMany_Edit.ascx`字段模板已添加以用于显示和编辑涉及多对多关系的数据提供支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="f8a2c-918">控件显示和支持枚举的新特性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="f8a2c-919">*DisplayAttribute*已添加要向你提供对字段的显示方式的其他控制。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="f8a2c-920">*DisplayName*在早期版本的动态数据允许你更改用作字段标题的名称的属性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="f8a2c-921">新*DisplayAttribute*类允许您指定用于显示字段，如顺序显示的字段以及字段是否将用作筛选器的更多选项。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="f8a2c-922">该属性还提供了用于中的标签的名称的独立控制*GridView*控制中使用的名称*说明*控制，该字段的帮助文本和水印用于字段 （如果字段接受输入的文本）。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="f8a2c-923">*EnumDataTypeAttribute*类已添加，以便你可以将字段映射到枚举。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="f8a2c-924">当此属性应用于字段时，你将指定枚举类型。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="f8a2c-925">动态数据使用新`Enumeration.ascx`字段模板来创建 UI，用于显示和编辑枚举值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="f8a2c-926">模板将映射到枚举中的名称来自数据库的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="f8a2c-927">增强了对筛选器支持</span><span class="sxs-lookup"><span data-stu-id="f8a2c-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="f8a2c-928">动态数据 1.0 附带了内置布尔值列和外键列的筛选器。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="f8a2c-929">筛选器不允许您指定是否显示它们，或以何种顺序显示它们。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="f8a2c-930">新*DisplayAttribute*对列是否显示为筛选器控制属性解决了这两向您提供这些问题并在何种顺序显示。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="f8a2c-931">其他增强功能就是确保筛选支持已重新[编写为使用新](#0.2__QueryExtender "_QueryExtender") Web 窗体功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="f8a2c-932">这样可以创建筛选器，而无需将与用于筛选器数据源控件的知识。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="f8a2c-933">这些扩展，以及筛选器也已转换为模板控件，该编辑器可以添加新的。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="f8a2c-934">最后， *DisplayAttribute*前面所述的类允许默认筛选器中重写，在相同的方式*UIHint*允许列中被重写的默认字段模板。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="f8a2c-935">Visual Studio 2010 Web 开发改进</span><span class="sxs-lookup"><span data-stu-id="f8a2c-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="f8a2c-936">Visual Studio 2010 中的 web 开发已得到增强的更大 CSS 兼容性，通过 HTML 和 ASP.NET 标记代码段和新动态 IntelliSense JavaScript 提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="f8a2c-937">改进了的 CSS 兼容性</span><span class="sxs-lookup"><span data-stu-id="f8a2c-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="f8a2c-938">在 Visual Studio 2010 的 Visual Web Developer 设计器已更新，提高 CSS 2.1 标准合规性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="f8a2c-939">在设计器更好地保留的 HTML 源文件的完整性和 Visual Studio 的早期版本比更加可靠。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="f8a2c-940">实质上，体系结构改进还进行该更好地实现中呈现、 布局和可维护性将来增强功能。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="f8a2c-941">HTML 和 JavaScript 代码段</span><span class="sxs-lookup"><span data-stu-id="f8a2c-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="f8a2c-942">在 HTML 编辑器中，IntelliSense 会自动完成标记名称。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="f8a2c-943">IntelliSense 代码段功能整个标记以及更多设置为自动完成。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="f8a2c-944">在 Visual Studio 2010 中，IntelliSense 代码段将支持 JavaScript，以及 C# 和 Visual Basic 中，这在 Visual Studio 的早期版本中受支持。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="f8a2c-945">Visual Studio 2010 包括超过 200 个代码段，帮助你自动完成常见 ASP.NET 和 HTML 标记，包括必需的属性 (如 runat ="server") 和特定于标记的公共属性 (如*ID*， *DataSourceID*， *ControlToValidate*，和*文本*)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="f8a2c-946">你可以下载其他代码段，也可以编写自己的代码段，用于封装各种你或你的团队使用的常见任务的标记的块。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="f8a2c-947">JavaScript IntelliSense 增强功能</span><span class="sxs-lookup"><span data-stu-id="f8a2c-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="f8a2c-948">在 Visual 2010 中，JavaScript IntelliSense 已经过重新设计提供甚至更丰富的编辑体验。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="f8a2c-949">IntelliSense 现在识别对象具有已动态生成的方法如*registerNamespace*和其他 JavaScript 框架使用的类似技术。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="f8a2c-950">若要分析的脚本的大型库，以及与很少或没有处理延迟一起显示 IntelliSense，性能得到了提高。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="f8a2c-951">若要支持几乎所有第三方库并支持各种编码风格已大大增加兼容性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="f8a2c-952">现在其作为你键入并立即利用 IntelliSense 分析文档注释。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="f8a2c-953">使用 Visual Studio 2010 的 web 应用程序部署</span><span class="sxs-lookup"><span data-stu-id="f8a2c-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="f8a2c-954">在 ASP.NET 开发人员部署 Web 应用程序时，它们通常发现他们遇到如下问题：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="f8a2c-955">部署到共享的宿主站点需要技术如 FTP，可能会很慢。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="f8a2c-956">此外，你必须手动执行任务，如运行 SQL 脚本，配置数据库，并且你必须更改 IIS 设置，例如为应用程序配置的虚拟目录文件夹。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="f8a2c-957">在企业环境中，除了部署 Web 应用程序文件，管理员通常必须修改 ASP.NET 配置文件和 IIS 设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="f8a2c-958">数据库管理员必须运行 SQL 脚本，以获得运行的应用程序数据库的一系列。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="f8a2c-959">此类安装耗费大量精力，通常需要小时才能完成，并且必须仔细了介绍。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="f8a2c-960">Visual Studio 2010 包括的技术，解决这些问题，能够让你无缝地部署 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="f8a2c-961">这些技术之一是 IIS 的 Web 部署工具 (MsDeploy.exe)。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="f8a2c-962">Visual Studio 2010 中的 web 部署功能包括以下主要方面：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="f8a2c-963">Web 打包</span><span class="sxs-lookup"><span data-stu-id="f8a2c-963">Web packaging</span></span>
- <span data-ttu-id="f8a2c-964">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="f8a2c-964">Web.config transformation</span></span>
- <span data-ttu-id="f8a2c-965">数据库部署</span><span class="sxs-lookup"><span data-stu-id="f8a2c-965">Database deployment</span></span>
- <span data-ttu-id="f8a2c-966">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-966">One-click publish for Web applications</span></span>

<span data-ttu-id="f8a2c-967">下列各节提供有关这些功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="f8a2c-968">Web 打包</span><span class="sxs-lookup"><span data-stu-id="f8a2c-968">Web Packaging</span></span>

<span data-ttu-id="f8a2c-969">Visual Studio 2010 使用 MSDeploy 工具来创建你的应用程序，即所谓的压缩 (.zip) 文件*Web 包*。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="f8a2c-970">包文件包含有关你的应用程序以及以下内容的元数据：</span><span class="sxs-lookup"><span data-stu-id="f8a2c-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="f8a2c-971">IIS 设置，包括应用程序池设置、 错误页设置等。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="f8a2c-972">实际 Web 内容，其中包括网页、 用户控件、 静态内容 （映像和 HTML 文件） 和等等。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="f8a2c-973">SQL Server 数据库架构和数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="f8a2c-974">安全证书，要安装在 GAC、 注册表设置等组件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="f8a2c-975">可以复制到任何服务器，然后通过使用 IIS 管理器手动安装 Web 包。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="f8a2c-976">或者，用于自动部署，包可以安装通过使用命令行命令或通过使用部署 Api。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="f8a2c-977">Visual Studio 2010 提供内置的 MSBuild 任务和用于创建 Web 包的目标。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="f8a2c-978">有关详细信息，请参阅[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)MSDN 网站上和[为什么应创建 Web 包的 10 + 20 原因](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="f8a2c-979">Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="f8a2c-979">Web.config Transformation</span></span>

<span data-ttu-id="f8a2c-980">对于 Web 应用程序部署，Visual Studio 2010 引入了[XML 文档转换 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)，这是一种功能，可以将转换`Web.config`文件从开发设置到生产环境设置。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="f8a2c-981">转换设置在名为的转换文件中指定`web.debug.config`， `web.release.config`，依次类推。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="f8a2c-982">（这些文件的名称匹配 MSBuild 配置。）转换文件包括只需更改，你需要对部署进行`Web.config`文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="f8a2c-983">通过使用简单的语法指定所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="f8a2c-984">下面的示例显示的一部分`web.release.config`可能生成的发布配置的部署的文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="f8a2c-985">该示例中的替换关键字在部署期间指定*connectionString*中的节点`Web.config`文件将替换为示例中列出的值。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="f8a2c-986">有关详细信息，请参阅[Web 应用程序项目部署的 Web.config 转换语法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx)MSDN 上<a id="0.2_a"></a>网站和[Web 部署： Web.Config 转换](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="f8a2c-987">数据库部署</span><span class="sxs-lookup"><span data-stu-id="f8a2c-987">Database Deployment</span></span>

<span data-ttu-id="f8a2c-988">Visual Studio 2010 部署包可以包含 SQL Server 数据库上的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="f8a2c-989">作为包定义的一部分，为源数据库提供的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="f8a2c-990">当你创建的 Web 包时，Visual Studio 2010 创建 SQL 脚本的数据库架构和 （可选） 的数据，然后将它们添加到包。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="f8a2c-991">你还可以提供自定义 SQL 脚本，并指定它们应运行在服务器的序列。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="f8a2c-992">在部署时，你可以提供适合于目标服务器中; 的连接字符串部署过程然后使用此连接字符串来运行脚本，创建数据库架构并添加数据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="f8a2c-993">此外，通过使用一键式发布，您可以配置部署，以便应用程序发布到远程共享宿主站点时，直接发布你的数据库。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="f8a2c-994">有关详细信息，请参阅[如何： 部署数据库与 Web 应用程序项目](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)MSDN 网站上和[使用 VS 2010 数据库部署](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="f8a2c-995">单击发布为 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="f8a2c-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="f8a2c-996">Visual Studio 2010 还允许你使用 IIS 的远程管理服务发布到远程服务器的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="f8a2c-997">你可以为你的托管帐户或测试服务器或过渡服务器创建的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="f8a2c-998">每个配置文件可以安全地保存相应的凭据。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="f8a2c-999">你可以随后部署到任何目标服务器通过使用 Web 一键式一次单击发布工具栏。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="f8a2c-1000">使用 Visual Studio 2010，你还可以通过使用 MSBuild 命令行发布。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="f8a2c-1001">这允许您配置您的团队生成环境，要包括在持续集成模型中的发布。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="f8a2c-1002">有关详细信息，请参阅[如何： 部署 Web 应用程序项目使用一键式发布和 Web 部署](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)MSDN 网站上和[Web 1 单击发布使用 VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="f8a2c-1003">若要在 Visual Studio 2010 中查看有关 Web 应用程序部署的视频演示文稿，请参阅[的 Web 开发人员预览版的 VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) Vishal Joshi 博客上。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="f8a2c-1004">资源</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1004">Resources</span></span>

<span data-ttu-id="f8a2c-1005">以下网站提供有关 ASP.NET 4 和 Visual Studio 2010 的其他信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="f8a2c-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 网站上的 ASP.NET 4 的官方文档。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="f8a2c-1007">[https://www.asp.net/](https://www.asp.net/) -ASP.NET 团队自己的网站。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="f8a2c-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 和[ASP.NET 动态数据内容映射](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-联机资源 ASP.NET 团队站点上和中的 ASP.NET 动态数据有关的正式文档。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="f8a2c-1009">[https://www.asp.net/ajax/](../../ajax/index.md) ASP.NET Ajax 开发-主 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="f8a2c-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) 有关功能的信息包含在 Visual Studio 2010 中-Visual Web 开发人员团队博客。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="f8a2c-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET 的预览版本的主 Web 资源。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="f8a2c-1012">免责声明</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1012">Disclaimer</span></span>

<span data-ttu-id="f8a2c-1013">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="f8a2c-1014">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="f8a2c-1015">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="f8a2c-1016">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="f8a2c-1017">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="f8a2c-1018">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="f8a2c-1019">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="f8a2c-1020">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="f8a2c-1021">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="f8a2c-1022">除非另行说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件此处所述虚构，是的无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 位置或事件旨在或妄加推断。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="f8a2c-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="f8a2c-1024">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1024">All rights reserved.</span></span>

<span data-ttu-id="f8a2c-1025">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="f8a2c-1026">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="f8a2c-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
