---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: e6ad37d51e0475631314c1110f13fe8aef2f954c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831065"
---
<a name="aspnet-mvc-3"></a><span data-ttu-id="b000b-102">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="b000b-102">ASP.NET MVC 3</span></span>
====================
- [<span data-ttu-id="b000b-103">概述</span><span class="sxs-lookup"><span data-stu-id="b000b-103">Overview</span></span>](#overview)
- [<span data-ttu-id="b000b-104">安装说明</span><span class="sxs-lookup"><span data-stu-id="b000b-104">Installation Notes</span></span>](#installation-notes)
- [<span data-ttu-id="b000b-105">软件要求</span><span class="sxs-lookup"><span data-stu-id="b000b-105">Software Requirements</span></span>](#software-requirements)
- [<span data-ttu-id="b000b-106">文档</span><span class="sxs-lookup"><span data-stu-id="b000b-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="b000b-107">支持</span><span class="sxs-lookup"><span data-stu-id="b000b-107">Support</span></span>](#support)
- [<span data-ttu-id="b000b-108">将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="b000b-108">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>](#upgrading)
- [<span data-ttu-id="b000b-109">ASP.NET MVC 3 工具更新 (2011 年 4 月 12 日)</span><span class="sxs-lookup"><span data-stu-id="b000b-109">ASP.NET MVC 3 Tools Update (April 12, 2011)</span></span>](#tu-changes)

    - [<span data-ttu-id="b000b-110">"添加控制器"对话框现在可以快速生成控制器及视图和数据访问代码</span><span class="sxs-lookup"><span data-stu-id="b000b-110">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>](#tu-AddControllerDialog)
    - [<span data-ttu-id="b000b-111">对改进"ASP.NET MVC 3 新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-111">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>](#tu-ImprovementsNewDialogBox)
    - [<span data-ttu-id="b000b-112">项目模板现在包含 Modernizr 1.7</span><span class="sxs-lookup"><span data-stu-id="b000b-112">Project templates now include Modernizr 1.7</span></span>](#tu-Modernizr)
    - [<span data-ttu-id="b000b-113">项目模板包含 jQuery、 jQuery UI 和 jQuery 的更新的版本验证</span><span class="sxs-lookup"><span data-stu-id="b000b-113">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>](#tu-UpdatedJQuery)
    - [<span data-ttu-id="b000b-114">项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b000b-114">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>](#tu-EF)
    - [<span data-ttu-id="b000b-115">项目模板包含 JavaScript 库作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b000b-115">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>](#tu-JavaScriptLibsNuget)
    - [<span data-ttu-id="b000b-116">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-116">Known Issues</span></span>](#tu-KI)
- [<span data-ttu-id="b000b-117">ASP.NET MVC 3 RTM (2011 年 1 月 13 日)</span><span class="sxs-lookup"><span data-stu-id="b000b-117">ASP.NET MVC 3 RTM (January 13, 2011)</span></span>](#MVC3RTM)

    - [<span data-ttu-id="b000b-118">更改： 更新版本的 jQuery UI 1.8.7 为</span><span class="sxs-lookup"><span data-stu-id="b000b-118">Change: Updated the version of jQuery UI to 1.8.7</span></span>](#RTM-1)
    - [<span data-ttu-id="b000b-119">更改： 更改 ModelMetadataProvider 回 DataAnnotationsModelMetadataProvider 了默认值</span><span class="sxs-lookup"><span data-stu-id="b000b-119">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>](#RTM-2)
    - [<span data-ttu-id="b000b-120">已修复： 粘贴 Razor 表达式包含空格导致它被反转的部分</span><span class="sxs-lookup"><span data-stu-id="b000b-120">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>](#RTM-3)
    - [<span data-ttu-id="b000b-121">已修复： 重命名在编辑器中打开的 Razor 文件禁用语法着色和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b000b-121">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>](#RTM-4)
    - [<span data-ttu-id="b000b-122">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-122">Known Issues</span></span>](#RTM-KI)
    - [<span data-ttu-id="b000b-123">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-123">Breaking Changes</span></span>](#RTM-BC)
- [<span data-ttu-id="b000b-124">ASP.NET MVC 3 候选发布 2 (2010 年 12 月 10 日)</span><span class="sxs-lookup"><span data-stu-id="b000b-124">ASP.NET MVC 3 Release Candidate 2 (December 10, 2010)</span></span>](#_Toc2)

    - [<span data-ttu-id="b000b-125">项目模板更改为包括 jQuery 1.4.4、 jQuery 验证 1.7 和 jQuery UI 1.8.6y UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b000b-125">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6y UI 1.8.6</span></span>](#_Toc2_1)
    - [<span data-ttu-id="b000b-126">添加了"AdditionalMetadataAttribute"类</span><span class="sxs-lookup"><span data-stu-id="b000b-126">Added "AdditionalMetadataAttribute" Class</span></span>](#_Toc2_2)
    - [<span data-ttu-id="b000b-127">改进了的视图基架</span><span class="sxs-lookup"><span data-stu-id="b000b-127">Improved View Scaffolding</span></span>](#_Toc2_3)
    - [<span data-ttu-id="b000b-128">添加的 Html.Raw 方法</span><span class="sxs-lookup"><span data-stu-id="b000b-128">Added Html.Raw Method</span></span>](#_Toc2_3)
    - [<span data-ttu-id="b000b-129">已重命名"Controller.ViewModel"属性和"ViewBag"到"视图"属性</span><span class="sxs-lookup"><span data-stu-id="b000b-129">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>](#_Toc2_4)
    - [<span data-ttu-id="b000b-130">已重命名"ControllerSessionStateAttribute"类"SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="b000b-130">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>](#_Toc2_5)
    - [<span data-ttu-id="b000b-131">已重命名的 RemoteAttribute"字段"属性设置为"AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="b000b-131">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>](#_Toc2_6)
    - [<span data-ttu-id="b000b-132">重命名"SkipRequestValidationAttribute"到"AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="b000b-132">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>](#_Toc2_7)
    - [<span data-ttu-id="b000b-133">已更改"Html.ValidationMessage"方法来显示第一条有用的错误消息</span><span class="sxs-lookup"><span data-stu-id="b000b-133">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>](#_Toc2_8)
    - [<span data-ttu-id="b000b-134">固定@model声明，以将空格添加到文档</span><span class="sxs-lookup"><span data-stu-id="b000b-134">Fixed @model Declaration to not Add Whitespace to the Document</span></span>](#_Toc2_9)
    - [<span data-ttu-id="b000b-135">添加了"FileExtensions"属性设置为视图引擎，以支持特定于引擎的文件的名称</span><span class="sxs-lookup"><span data-stu-id="b000b-135">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>](#_Toc2_10)
    - [<span data-ttu-id="b000b-136">要发出"For"属性的正确值的固定"LabelFor"帮助程序</span><span class="sxs-lookup"><span data-stu-id="b000b-136">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>](#_Toc2_11)
    - [<span data-ttu-id="b000b-137">固定"RenderAction"方法，从而使在模型绑定期间的显式值优先级</span><span class="sxs-lookup"><span data-stu-id="b000b-137">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>](#_Toc2_12)
    - [<span data-ttu-id="b000b-138">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-138">Breaking Changes</span></span>](#_Toc2_BC)
    - [<span data-ttu-id="b000b-139">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-139">Known Issues</span></span>](#_Toc2_KI)
- [<span data-ttu-id="b000b-140">ASP.NET MVC 3 候选发布 (2010 年 11 月 9 日)</span><span class="sxs-lookup"><span data-stu-id="b000b-140">ASP.NET MVC 3 Release Candidate (Nov 9, 2010)</span></span>](#TOC_ASP_NET_3_RC)

    - [<span data-ttu-id="b000b-141">ASP.NET MVC 3 RC 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b000b-141">New Features in ASP.NET MVC 3 RC</span></span>](#_Toc276711785)
    - [<span data-ttu-id="b000b-142">NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="b000b-142">NuGet Package Manager</span></span>](#_Toc276711786)
    - [<span data-ttu-id="b000b-143">改进了"新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-143">Improved "New Project" Dialog Box</span></span>](#_Toc276711787)
    - [<span data-ttu-id="b000b-144">无会话控制器</span><span class="sxs-lookup"><span data-stu-id="b000b-144">Sessionless Controllers</span></span>](#_Toc276711788)
    - [<span data-ttu-id="b000b-145">新的验证特性</span><span class="sxs-lookup"><span data-stu-id="b000b-145">New Validation Attributes</span></span>](#_Toc276711789)
    - [<span data-ttu-id="b000b-146">有关"LabelFor"和"LabelForModel"方法的新重载</span><span class="sxs-lookup"><span data-stu-id="b000b-146">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>](#_Toc276711790)
    - [<span data-ttu-id="b000b-147">子操作输出缓存</span><span class="sxs-lookup"><span data-stu-id="b000b-147">Child Action Output Caching</span></span>](#_Toc276711791)
    - [<span data-ttu-id="b000b-148">"添加视图"对话框框中改进</span><span class="sxs-lookup"><span data-stu-id="b000b-148">"Add View" Dialog Box Improvements</span></span>](#_Toc276711792)
    - [<span data-ttu-id="b000b-149">粒度请求验证</span><span class="sxs-lookup"><span data-stu-id="b000b-149">Granular Request Validation</span></span>](#_Toc276711793)
    - [<span data-ttu-id="b000b-150">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-150">Breaking Changes</span></span>](#_Toc276711794)
    - [<span data-ttu-id="b000b-151">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-151">Known Issues</span></span>](#_Toc276711795)
- [<span data-ttu-id="b000b-152">ASP。MVC 3 Beta 说明 (2010 年 10 月 6 日)</span><span class="sxs-lookup"><span data-stu-id="b000b-152">ASP.MVC 3 Beta Notes (Oct 6, 2010)</span></span>](#TOC_ASP_NET_3_Beta)

    - [<span data-ttu-id="b000b-153">ASP.NET MVC 3 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b000b-153">New Features in ASP.NET MVC 3 Beta</span></span>](#0.1__Toc274034215)
    - [<span data-ttu-id="b000b-154">NuPack 包管理器</span><span class="sxs-lookup"><span data-stu-id="b000b-154">NuPack Package Manager</span></span>](#0.1__Toc274034216)
    - [<span data-ttu-id="b000b-155">改进了新建项目对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-155">Improved New Project Dialog Box</span></span>](#0.1__Toc274034217)
    - [<span data-ttu-id="b000b-156">简化的方法来指定强类型模型在 Razor 视图中</span><span class="sxs-lookup"><span data-stu-id="b000b-156">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>](#0.1__Toc274034218)
    - [<span data-ttu-id="b000b-157">支持新的 ASP.NET Web 页的帮助器方法</span><span class="sxs-lookup"><span data-stu-id="b000b-157">Support for New ASP.NET Web Pages Helper Methods</span></span>](#0.1__Toc274034219)
    - [<span data-ttu-id="b000b-158">其他依赖项注入支持</span><span class="sxs-lookup"><span data-stu-id="b000b-158">Additional Dependency Injection Support</span></span>](#0.1__Toc274034220)
    - [<span data-ttu-id="b000b-159">新的非介入式 jQuery 基于 Ajax 的支持</span><span class="sxs-lookup"><span data-stu-id="b000b-159">New Support for Unobtrusive jQuery-Based Ajax</span></span>](#0.1__Toc274034221)
    - [<span data-ttu-id="b000b-160">对于非介入式 jQuery 验证新的支持</span><span class="sxs-lookup"><span data-stu-id="b000b-160">New Support for Unobtrusive jQuery Validation</span></span>](#0.1__Toc274034222)
    - [<span data-ttu-id="b000b-161">客户端验证和非介入式 JavaScript 的新应用程序范围内标志</span><span class="sxs-lookup"><span data-stu-id="b000b-161">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>](#0.1__Toc274034223)
    - [<span data-ttu-id="b000b-162">对视图运行前运行的代码的新支持</span><span class="sxs-lookup"><span data-stu-id="b000b-162">New Support for Code that Runs Before Views Run</span></span>](#0.1__Toc274034224)
    - [<span data-ttu-id="b000b-163">新的 VBHTML Razor 语法支持</span><span class="sxs-lookup"><span data-stu-id="b000b-163">New Support for the VBHTML Razor Syntax</span></span>](#0.1__Toc274034225)
    - [<span data-ttu-id="b000b-164">更精细地控制 ValidateInputAttribute</span><span class="sxs-lookup"><span data-stu-id="b000b-164">More Granular Control over ValidateInputAttribute</span></span>](#0.1__Toc274034226)
    - [<span data-ttu-id="b000b-165">帮助程序对于使用匿名对象指定的 HTML 特性名称将下划线转换为连字符</span><span class="sxs-lookup"><span data-stu-id="b000b-165">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>](#0.1__Toc274034227)
    - [<span data-ttu-id="b000b-166">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b000b-166">Bug Fixes</span></span>](#0.1__Toc274034228)
    - [<span data-ttu-id="b000b-167">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-167">Breaking Changes</span></span>](#0.1__Toc274034229)
    - [<span data-ttu-id="b000b-168">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-168">Known Issues</span></span>](#0.1__Toc274034230)
- [<span data-ttu-id="b000b-169">免责声明</span><span class="sxs-lookup"><span data-stu-id="b000b-169">Disclaimer</span></span>](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a><span data-ttu-id="b000b-170">概述</span><span class="sxs-lookup"><span data-stu-id="b000b-170">Overview</span></span>

<span data-ttu-id="b000b-171">本文档介绍的 ASP.NET MVC 3 RTM for Visual Studio 2010 的版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-171">This document describes the release of ASP.NET MVC 3 RTM for Visual Studio 2010.</span></span> <span data-ttu-id="b000b-172">ASP.NET MVC 是一个框架，用于开发 Web 应用程序使用模型-视图-控制器 (MVC) 模式。</span><span class="sxs-lookup"><span data-stu-id="b000b-172">ASP.NET MVC is a framework for developing Web applications that uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="b000b-173">ASP.NET MVC 3 安装程序包括以下组件：</span><span class="sxs-lookup"><span data-stu-id="b000b-173">The ASP.NET MVC 3 installer includes the following components:</span></span>

- <span data-ttu-id="b000b-174">ASP.NET MVC 3 运行时组件</span><span class="sxs-lookup"><span data-stu-id="b000b-174">ASP.NET MVC 3 runtime components</span></span>
- <span data-ttu-id="b000b-175">ASP.NET MVC 3 Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="b000b-175">ASP.NET MVC 3 Visual Studio 2010 tools</span></span>
- <span data-ttu-id="b000b-176">ASP.NET 网页运行时组件</span><span class="sxs-lookup"><span data-stu-id="b000b-176">ASP.NET Web Pages run-time components</span></span>
- <span data-ttu-id="b000b-177">ASP.NET Web Pages Visual Studio 2010 工具</span><span class="sxs-lookup"><span data-stu-id="b000b-177">ASP.NET Web Pages Visual Studio 2010 tools</span></span>
- <span data-ttu-id="b000b-178">Microsoft.NET (NuGet) 包管理器</span><span class="sxs-lookup"><span data-stu-id="b000b-178">Microsoft Package Manager for .NET (NuGet)</span></span>
- <span data-ttu-id="b000b-179">支持 Razor 语法的 Visual Studio 2010 的更新。</span><span class="sxs-lookup"><span data-stu-id="b000b-179">An update for Visual Studio 2010 that enables support for Razor syntax.</span></span> <span data-ttu-id="b000b-180">（有关详细信息，请参阅知识库文章 2483190）。</span><span class="sxs-lookup"><span data-stu-id="b000b-180">(For details, see KnowledgeBase article 2483190.)</span></span>

<span data-ttu-id="b000b-181">可以在位于以下 URL 的 ASP.NET 网站上找到的每个预发行版本的 ASP.NET MVC 3 发行说明的完整集：</span><span class="sxs-lookup"><span data-stu-id="b000b-181">The full set of release notes for each pre-release version of ASP.NET MVC 3 can be found on the ASP.NET website at the following URL:</span></span>

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a><span data-ttu-id="b000b-182">安装说明</span><span class="sxs-lookup"><span data-stu-id="b000b-182">Installation Notes</span></span>

<span data-ttu-id="b000b-183">若要安装 ASP.NET MVC 3 RTM 使用 Web 平台安装程序 (Web PI)，请访问以下页面：</span><span class="sxs-lookup"><span data-stu-id="b000b-183">To install ASP.NET MVC 3 RTM using the Web Platform Installer (Web PI), visit the following page:</span></span>

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

<span data-ttu-id="b000b-184">或者，可以下载 ASP.NET MVC 3 RTM 的安装程序的 Visual Studio 2010 中的以下页面：</span><span class="sxs-lookup"><span data-stu-id="b000b-184">Alternatively, you can download the installer for ASP.NET MVC 3 RTM for Visual Studio 2010 from the following page:</span></span>

https://go.microsoft.com/fwlink/?LinkID=208140

<span data-ttu-id="b000b-185">ASP.NET MVC 3 可以安装，并且可以运行的同时使用 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="b000b-185">ASP.NET MVC 3 can be installed and can run side-by-side with ASP.NET MVC 2.</span></span>

<a id="software-requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="b000b-186">软件要求</span><span class="sxs-lookup"><span data-stu-id="b000b-186">Software Requirements</span></span>

<span data-ttu-id="b000b-187">ASP.NET MVC 3 运行时组件需要以下软件：</span><span class="sxs-lookup"><span data-stu-id="b000b-187">The ASP.NET MVC 3 run-time components require the following software:</span></span>

- <span data-ttu-id="b000b-188">.NET framework 版本 4。</span><span class="sxs-lookup"><span data-stu-id="b000b-188">.NET Framework version 4.</span></span> 

    <span data-ttu-id="b000b-189">ASP.NET MVC 3 Visual Studio 2010 工具需要以下软件：</span><span class="sxs-lookup"><span data-stu-id="b000b-189">ASP.NET MVC 3 Visual Studio 2010 tools require the following software:</span></span>
- <span data-ttu-id="b000b-190">Visual Studio 2010 或 Visual Web Developer 2010 速成版。</span><span class="sxs-lookup"><span data-stu-id="b000b-190">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="b000b-191">文档</span><span class="sxs-lookup"><span data-stu-id="b000b-191">Documentation</span></span>

<span data-ttu-id="b000b-192">在 MSDN 网站上的以下 URL 上提供了 ASP.NET MVC 的文档：</span><span class="sxs-lookup"><span data-stu-id="b000b-192">Documentation for ASP.NET MVC is available on the MSDN Web site at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

<span data-ttu-id="b000b-193">教程和有关 ASP.NET MVC 的其他信息可在以下 URL 处的 ASP.NET Web 站点的 MVC 页上：</span><span class="sxs-lookup"><span data-stu-id="b000b-193">Tutorials and other information about ASP.NET MVC are available on the MVC page of the ASP.NET Web site at the following URL:</span></span>

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a><span data-ttu-id="b000b-194">支持</span><span class="sxs-lookup"><span data-stu-id="b000b-194">Support</span></span>

<span data-ttu-id="b000b-195">这是完全受支持的版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-195">This is a fully supported release.</span></span> <span data-ttu-id="b000b-196">有关获得技术支持的信息可在[Microsoft 支持网站](https://support.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="b000b-196">Information about getting technical support can be found at the [Microsoft Support website](https://support.microsoft.com/).</span></span>

<span data-ttu-id="b000b-197">也可随意 ASP.NET 社区的成员是经常能够提供非正式的支持在 ASP.NET MVC 论坛中发布有关此发行版的问题：</span><span class="sxs-lookup"><span data-stu-id="b000b-197">Also feel free to post questions about this release to the ASP.NET MVC forum, where members of the ASP.NET community are frequently able to provide informal support:</span></span>

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a><span data-ttu-id="b000b-198">将 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="b000b-198">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="b000b-199">ASP.NET MVC 3 可以与 ASP.NET MVC 2 并行安装使您灵活地选择何时升级到 ASP.NET MVC 3 的 ASP.NET MVC 2 应用程序在同一计算机上。</span><span class="sxs-lookup"><span data-stu-id="b000b-199">ASP.NET MVC 3 can be installed side by side with ASP.NET MVC 2 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 2 application to ASP.NET MVC 3.</span></span>

<span data-ttu-id="b000b-200">若要手动升级到版本 3 现有的 ASP.NET MVC 2 应用程序，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="b000b-200">To manually upgrade an existing ASP.NET MVC 2 application to version 3, do the following:</span></span>

1. <span data-ttu-id="b000b-201">在计算机上创建一个新的空 ASP.NET MVC 3 项目。</span><span class="sxs-lookup"><span data-stu-id="b000b-201">Create a new empty ASP.NET MVC 3 project on your computer.</span></span> <span data-ttu-id="b000b-202">此项目将包含所需的升级某些文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-202">This project will contain some files that are required for the upgrade.</span></span>
2. <span data-ttu-id="b000b-203">将以下文件从 ASP.NET MVC 3 项目复制到 ASP.NET MVC 2 项目的相应位置。</span><span class="sxs-lookup"><span data-stu-id="b000b-203">Copy the following files from the ASP.NET MVC 3 project into the corresponding location of your ASP.NET MVC 2 project.</span></span> <span data-ttu-id="b000b-204">你将需要更新对 jQuery 库，以说明新的文件名 (jQuery-1.5.1.js) 的任何引用：</span><span class="sxs-lookup"><span data-stu-id="b000b-204">You'll need to update any references to the jQuery library to account for the new filename ( jQuery-1.5.1.js):</span></span> 

    - <span data-ttu-id="b000b-205">/Views/Web.config</span><span class="sxs-lookup"><span data-stu-id="b000b-205">/Views/Web.config</span></span>
    - <span data-ttu-id="b000b-206">/packages.config</span><span class="sxs-lookup"><span data-stu-id="b000b-206">/packages.config</span></span>
    - <span data-ttu-id="b000b-207">/scripts/\*.js</span><span class="sxs-lookup"><span data-stu-id="b000b-207">/scripts/\*.js</span></span>
    - <span data-ttu-id="b000b-208">/内容/主题/\*。\*</span><span class="sxs-lookup"><span data-stu-id="b000b-208">/Content/themes/\*.\*</span></span>
3. <span data-ttu-id="b000b-209">复制*包*解决方案，即解决方案的.sln 文件所在的目录的根目录到空的 ASP.NET MVC 3 项目解决方案的根目录中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b000b-209">Copy the *packages* folder in the root of the empty ASP.NET MVC 3 project solution into the root of your solution, which is in the directory where the solution's .sln file is located.</span></span>
4. <span data-ttu-id="b000b-210">如果你的 ASP.NET MVC 2 项目包含任何区域，则 /Views/Web.config 文件复制到*视图*的每个区域的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b000b-210">If your ASP.NET MVC 2 project contains any areas, copy the /Views/Web.config file to the *Views* folder of each area.</span></span>
5. <span data-ttu-id="b000b-211">在 ASP.NET MVC 2 项目中的这两个 Web.config 文件，全局搜索，并替换 ASP.NET MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-211">In both Web.config files in the ASP.NET MVC 2 project, globally search and replace the ASP.NET MVC version.</span></span> <span data-ttu-id="b000b-212">找到以下：</span><span class="sxs-lookup"><span data-stu-id="b000b-212">Find the following:</span></span> 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="b000b-213">使用以下标记替换它：</span><span class="sxs-lookup"><span data-stu-id="b000b-213">Replace it with the following:</span></span>

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. <span data-ttu-id="b000b-214">在解决方案资源管理器中删除对引用*System.Web.Mvc* （哪个点的 dll 版本 2），然后添加对的引用*System.Web.Mvc* (v3.0.0.0)。</span><span class="sxs-lookup"><span data-stu-id="b000b-214">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the DLL from version 2), then add a reference to *System.Web.Mvc* (v3.0.0.0).</span></span>
7. <span data-ttu-id="b000b-215">添加对 System.Web.WebPages.dll 和 system.web.helpers.dll 的引用的引用。</span><span class="sxs-lookup"><span data-stu-id="b000b-215">Add a reference to System.Web.WebPages.dll and System.Web.Helpers.dll.</span></span> <span data-ttu-id="b000b-216">这些程序集位于以下文件夹：</span><span class="sxs-lookup"><span data-stu-id="b000b-216">These assemblies are located in the following folders:</span></span> 

    - <span data-ttu-id="b000b-217">%ProgramFiles%\Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span><span class="sxs-lookup"><span data-stu-id="b000b-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span></span>
    - <span data-ttu-id="b000b-218">%ProgramFiles%\Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span><span class="sxs-lookup"><span data-stu-id="b000b-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span></span>
8. <span data-ttu-id="b000b-219">在解决方案资源管理器，右键单击项目名称并选择卸载项目。</span><span class="sxs-lookup"><span data-stu-id="b000b-219">In Solution Explorer, right-click the project name and select Unload Project.</span></span> <span data-ttu-id="b000b-220">再次右键单击项目名称，然后选择编辑*ProjectName*.csproj。</span><span class="sxs-lookup"><span data-stu-id="b000b-220">Then right-click the project name again and select Edit *ProjectName*.csproj.</span></span>
9. <span data-ttu-id="b000b-221">找到*ProjectTypeGuids*元素，并替换 {F85E285D-A4E0-4152-9332-AB1D724D3325} 为 {E53F8FEA-EAE0-44A6-8774-FFD645390401}。</span><span class="sxs-lookup"><span data-stu-id="b000b-221">Locate the *ProjectTypeGuids* element and replace {F85E285D-A4E0-4152-9332-AB1D724D3325} with {E53F8FEA-EAE0-44A6-8774-FFD645390401}.</span></span>
10. <span data-ttu-id="b000b-222">保存所做的更改，右键单击项目，并选择重新加载项目。</span><span class="sxs-lookup"><span data-stu-id="b000b-222">Save the changes, right-click the project, and then select Reload Project.</span></span>
11. <span data-ttu-id="b000b-223">在应用程序的根 Web.config 文件中，添加以下设置来*程序集*部分。</span><span class="sxs-lookup"><span data-stu-id="b000b-223">In the application's root Web.config file, add the following settings to the *assemblies* section.</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. <span data-ttu-id="b000b-224">如果项目引用了使用 ASP.NET MVC 2 编译任何第三方库，添加以下突出显示*bindingRedirect*元素下的应用程序根目录中的 Web.config 文件*配置*部分：</span><span class="sxs-lookup"><span data-stu-id="b000b-224">If the project references any third-party libraries that are compiled using ASP.NET MVC 2, add the following highlighted *bindingRedirect* element to the Web.config file in the application root under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a><span data-ttu-id="b000b-225">ASP.NET MVC 3 工具的更新中更改</span><span class="sxs-lookup"><span data-stu-id="b000b-225">Changes in ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="b000b-226">本部分介绍 ASP.NET MVC 3 RTM 版本发布以来 ASP.NET MVC 3 Tools Update 版本中所做的更改。</span><span class="sxs-lookup"><span data-stu-id="b000b-226">This section describes changes made in the ASP.NET MVC 3 Tools Update release since the ASP.NET MVC 3 RTM release.</span></span>

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a><span data-ttu-id="b000b-227">"添加控制器"对话框现在可以快速生成控制器及视图和数据访问代码</span><span class="sxs-lookup"><span data-stu-id="b000b-227">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>

<span data-ttu-id="b000b-228">基架是一种方法快速生成控制器和视图为您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-228">Scaffolding is a way of quickly generating a controller and views for your application.</span></span> <span data-ttu-id="b000b-229">生成的代码后，可以编辑它以满足你的项目的要求。</span><span class="sxs-lookup"><span data-stu-id="b000b-229">After the code has been generated, you can edit it to meet your project's requirements.</span></span>

<span data-ttu-id="b000b-230">若要启动*添加控制器*对话框在 ASP.NET MVC 3 中，右键单击*控制器*文件夹中的*解决方案资源管理器*，单击*添加*，然后依次*控制器*。</span><span class="sxs-lookup"><span data-stu-id="b000b-230">To launch the *Add Controller* dialog box in ASP.NET MVC 3, right-click the *Controllers* folder in *Solution Explorer*, click *Add*, and then click *Controller*.</span></span> <span data-ttu-id="b000b-231">对话框的已得到增强，以便提供其他创建基架选项。</span><span class="sxs-lookup"><span data-stu-id="b000b-231">The dialog box has been enhanced to offer additional scaffolding options.</span></span>

![](mvc3-release-notes/_static/image1.png)

<span data-ttu-id="b000b-232">有三个基架模板默认情况下。</span><span class="sxs-lookup"><span data-stu-id="b000b-232">There are three scaffolding templates available by default.</span></span>

#### <a name="empty-controller"></a><span data-ttu-id="b000b-233">空控制器</span><span class="sxs-lookup"><span data-stu-id="b000b-233">Empty Controller</span></span>

<span data-ttu-id="b000b-234">此模板生成一个空的控制器文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-234">This template generates an empty controller file.</span></span> <span data-ttu-id="b000b-235">此模板等效于不检查*添加的创建、 编辑、 详细信息的操作，删除方案*在以前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="b000b-235">This template is equivalent to not checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="b000b-236">如果选择此项，没有进一步可用选项。</span><span class="sxs-lookup"><span data-stu-id="b000b-236">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-empty-readwrite-actions"></a><span data-ttu-id="b000b-237">包含空读/写操作的控制器</span><span class="sxs-lookup"><span data-stu-id="b000b-237">Controller with empty read/write actions</span></span>

<span data-ttu-id="b000b-238">此模板将生成具有所有必需的操作方法，但没有实现代码的方法中的控制器文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-238">This template generates a controller file that has all the required action methods but no implementation code in the methods.</span></span> <span data-ttu-id="b000b-239">此模板等效于检查*添加的创建、 编辑、 详细信息的操作，删除方案*在以前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="b000b-239">This template is equivalent to checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="b000b-240">如果选择此项，没有进一步可用选项。</span><span class="sxs-lookup"><span data-stu-id="b000b-240">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a><span data-ttu-id="b000b-241">包含读/写操作和视图，使用实体框架的控制器</span><span class="sxs-lookup"><span data-stu-id="b000b-241">Controller with read/write actions and views, using Entity Framework</span></span>

<span data-ttu-id="b000b-242">此模板，可快速创建工作数据输入用户界面。</span><span class="sxs-lookup"><span data-stu-id="b000b-242">This template enables you to quickly create a working data-entry user interface.</span></span> <span data-ttu-id="b000b-243">它会生成处理各种常见要求和方案，如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="b000b-243">It generates code that handles a range of common requirements and scenarios, such as the following:</span></span>

- <span data-ttu-id="b000b-244">*数据访问*。</span><span class="sxs-lookup"><span data-stu-id="b000b-244">*Data access*.</span></span> <span data-ttu-id="b000b-245">生成的代码读取和写入数据库中的实体。</span><span class="sxs-lookup"><span data-stu-id="b000b-245">The generated code reads and writes entities in a database.</span></span> <span data-ttu-id="b000b-246">如果您选择一个现有的数据上下文类，或者让生成一个新的模板，它会使用 Entity Framework Code First 的方法*DbContext*类。</span><span class="sxs-lookup"><span data-stu-id="b000b-246">It works with the Entity Framework Code First approach if you choose an existing data context class or if you let the template generate a new *DbContext* class.</span></span> <span data-ttu-id="b000b-247">它还会使用 Entity Framework 数据库优先或模型优先方法如果你选择的现有*ObjectContext*类。</span><span class="sxs-lookup"><span data-stu-id="b000b-247">It also works with the Entity Framework Database First or Model First approach if you choose an existing *ObjectContext* class.</span></span>
- <span data-ttu-id="b000b-248">*验证*。</span><span class="sxs-lookup"><span data-stu-id="b000b-248">*Validation*.</span></span> <span data-ttu-id="b000b-249">生成的代码使用 ASP.NET MVC 模型绑定和元数据功能，以便窗体提交验证根据在模型类上声明的规则。</span><span class="sxs-lookup"><span data-stu-id="b000b-249">The generated code uses ASP.NET MVC model binding and metadata features so that form submissions are validated according to rules declared on your model class.</span></span> <span data-ttu-id="b000b-250">这包括内置验证规则，如*所需*并*StringLength*属性和自定义验证规则。</span><span class="sxs-lookup"><span data-stu-id="b000b-250">This includes built-in validation rules, such as the *Required* and *StringLength* attributes, and custom validation rules.</span></span>
- <span data-ttu-id="b000b-251">*一个对多关系*。</span><span class="sxs-lookup"><span data-stu-id="b000b-251">*One-to-many relationships*.</span></span> <span data-ttu-id="b000b-252">如果模型类之间定义一个多外键关系，生成的代码将生成下拉列表中的选择相关的实体。</span><span class="sxs-lookup"><span data-stu-id="b000b-252">If you define one-to-many foreign-key relationships between your model classes, the generated code will produce drop-down lists for selecting related entities.</span></span> <span data-ttu-id="b000b-253">例如，可能会定义以下 Entity Framework Code First 约定的模型类：</span><span class="sxs-lookup"><span data-stu-id="b000b-253">For example, you might define the following model classes following Entity Framework Code First conventions:</span></span> 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    <span data-ttu-id="b000b-254">当您然后搭建基架的控制器*产品*类，其视图将允许用户选择*类别*每个对象*产品*实例。</span><span class="sxs-lookup"><span data-stu-id="b000b-254">When you then scaffold a controller for the *Product* class, its views will allow users to choose a *Category* object for each *Product* instance.</span></span>

    <span data-ttu-id="b000b-255">此模板提供了附加选项中的*添加控制器*对话框。</span><span class="sxs-lookup"><span data-stu-id="b000b-255">This template enables additional options in the *Add Controller* dialog box.</span></span> <span data-ttu-id="b000b-256">有关*模型类*，可以在解决方案中，它确定的用户将能够创建或编辑的数据类型选择任意模型类：</span><span class="sxs-lookup"><span data-stu-id="b000b-256">For *Model class*, you can choose any model class in your solution, which determines the type of data that users will be able to create or edit:</span></span>
- <span data-ttu-id="b000b-257">如果你想要使用 Entity Framework Code First，可以选择任意模型类。</span><span class="sxs-lookup"><span data-stu-id="b000b-257">If you want to use Entity Framework Code First, you can choose any model class.</span></span>
- <span data-ttu-id="b000b-258">如果使用 Entity Framework 数据库优先或 Entity Framework 模型优先，请务必选择在概念模型中定义的实体类。</span><span class="sxs-lookup"><span data-stu-id="b000b-258">If you are using Entity Framework Database First or Entity Framework Model First, be sure to choose an entity class defined in your conceptual model.</span></span>

<span data-ttu-id="b000b-259">有关*数据上下文类*，可以进行以下选择：</span><span class="sxs-lookup"><span data-stu-id="b000b-259">For *Data Context class*, you can make these choices:</span></span>

- <span data-ttu-id="b000b-260">如果你想要使用 Code First 且没有现有的数据上下文类中，选择 * * 新的数据上下文 * *。</span><span class="sxs-lookup"><span data-stu-id="b000b-260">If you want to use Code First and have no existing data context class, choose **New data context **.</span></span> <span data-ttu-id="b000b-261">然后会为您生成数据上下文类。</span><span class="sxs-lookup"><span data-stu-id="b000b-261">A data context class will then be generated for you.</span></span>
- <span data-ttu-id="b000b-262">如果你想要使用 Code First，并且具有一个现有的数据上下文类，此处将其选定。</span><span class="sxs-lookup"><span data-stu-id="b000b-262">If you want to use Code First and have an existing data context class, choose it here.</span></span> <span data-ttu-id="b000b-263">它将更新以保存所选模型类。</span><span class="sxs-lookup"><span data-stu-id="b000b-263">It will be updated to persist the model class you have selected.</span></span>
- <span data-ttu-id="b000b-264">如果使用 Database First 或 Model First，选择您的对象上下文类。</span><span class="sxs-lookup"><span data-stu-id="b000b-264">If you are using Database First or Model First, choose your object context class here.</span></span>

<span data-ttu-id="b000b-265">对于视图，选择所需的视图引擎，或选择无如果不想要创建的任何视图基架。</span><span class="sxs-lookup"><span data-stu-id="b000b-265">For Views, choose the view engine you want to use, or choose None if you don't want to scaffold any views.</span></span>

<span data-ttu-id="b000b-266">您可以选择高级选项可用来进一步指定生成的视图的选项。</span><span class="sxs-lookup"><span data-stu-id="b000b-266">You can select Advanced Optionsto specify further options for the generated views.</span></span> <span data-ttu-id="b000b-267">例如，可以选择布局或母版页中以使用。</span><span class="sxs-lookup"><span data-stu-id="b000b-267">For example, you can choose the layout or master page to use.</span></span>

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a><span data-ttu-id="b000b-268">对改进"ASP.NET MVC 3 新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-268">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>

<span data-ttu-id="b000b-269">用于创建新的 ASP.NET MVC 3 项目对话框的包括多项改进，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b000b-269">The dialog box you use to create new ASP.NET MVC 3 projects includes multiple improvements, as listed below.</span></span>

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a><span data-ttu-id="b000b-270">新的"Intranet 项目"模板</span><span class="sxs-lookup"><span data-stu-id="b000b-270">New "Intranet Project" Template</span></span>

<span data-ttu-id="b000b-271">项目模板列表中包括新的 Intranet 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="b000b-271">The Project Template list includes a new Intranet Application template.</span></span> <span data-ttu-id="b000b-272">此模板包含用于生成而不窗体身份验证使用 Windows 身份验证的 web 应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="b000b-272">This template contains settings for building a web application using Windows authentication instead of forms authentication.</span></span> <span data-ttu-id="b000b-273">由于 intranet 应用程序需要某些不能在项目模板中封装的 IIS 设置，该模板将包含有关如何使项目模板在 IIS 中工作说明的自述文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-273">Because an intranet application requires some IIS settings that can't be encapsulated in a project template, the template includes a readme file with instructions for how to make the project template work in IIS.</span></span> <span data-ttu-id="b000b-274">文档位于以下 URL 的 MSDN 网站上提供了新的 Intranet 应用程序模板：</span><span class="sxs-lookup"><span data-stu-id="b000b-274">Documentation for the a new Intranet Application template is available on the MSDN website at the following URL:</span></span>

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a><span data-ttu-id="b000b-275">项目模板现在都支持 HTML5</span><span class="sxs-lookup"><span data-stu-id="b000b-275">Project templates are now HTML5 enabled</span></span>

<span data-ttu-id="b000b-276">新建项目对话框现在包含一个选项以将 HTML5 特定功能添加到项目模板。</span><span class="sxs-lookup"><span data-stu-id="b000b-276">The new-project dialog box now contains an option to add HTML5-specific features to the project templates.</span></span> <span data-ttu-id="b000b-277">选择该选项将导致视图以生成包含新的 HTML5 `<header>`， `<footer>`，和`<navigation>`元素。</span><span class="sxs-lookup"><span data-stu-id="b000b-277">Selecting the option causes views to be generated that contain the new HTML5 `<header>`, `<footer>`, and `<navigation>` elements.</span></span>

<span data-ttu-id="b000b-278">请注意，早期版本的浏览器不支持 HTML5 特定的标记。</span><span class="sxs-lookup"><span data-stu-id="b000b-278">Note that earlier versions of browsers do not support HTML5-specific tags.</span></span> <span data-ttu-id="b000b-279">若要解决此限制，HTML5 项目模板包含对 Modernizr 库的引用。</span><span class="sxs-lookup"><span data-stu-id="b000b-279">To address this limitation, the HTML5 project templates include a reference to the Modernizr library.</span></span> <span data-ttu-id="b000b-280">（请参阅下一节。）</span><span class="sxs-lookup"><span data-stu-id="b000b-280">(See the next section.)</span></span>

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a><span data-ttu-id="b000b-281">项目模板现在包含 Modernizr 1.7</span><span class="sxs-lookup"><span data-stu-id="b000b-281">Project templates now include Modernizr 1.7</span></span>

<span data-ttu-id="b000b-282">Modernizr 是一个 JavaScript 库，支持 CSS 3 和 HTML5 的浏览器中尚不支持这些功能。</span><span class="sxs-lookup"><span data-stu-id="b000b-282">Modernizr is a JavaScript library that enables support for CSS 3 and HTML5 in browsers that do not yet support these features.</span></span> <span data-ttu-id="b000b-283">此库是作为预安装的 NuGet 包的 ASP.NET MVC 3 项目模板中包含在内。</span><span class="sxs-lookup"><span data-stu-id="b000b-283">This library is included as a pre-installed NuGet package in templates for ASP.NET MVC 3 projects.</span></span> <span data-ttu-id="b000b-284">有关 Modernizr 的详细信息，请参阅[ http://www.modernizr.com/ ](http://www.modernizr.com/)。</span><span class="sxs-lookup"><span data-stu-id="b000b-284">For more information about Modernizr, see [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a><span data-ttu-id="b000b-285">项目模板包含 jQuery、 jQuery UI 和 jQuery 的更新的版本验证</span><span class="sxs-lookup"><span data-stu-id="b000b-285">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>

<span data-ttu-id="b000b-286">项目模板现在包含 jQuery 脚本的以下版本：</span><span class="sxs-lookup"><span data-stu-id="b000b-286">The project templates now include the following versions of the jQuery scripts:</span></span>

- <span data-ttu-id="b000b-287">jQuery 1.5.1</span><span class="sxs-lookup"><span data-stu-id="b000b-287">jQuery 1.5.1</span></span>
- <span data-ttu-id="b000b-288">jQuery 验证 1.8</span><span class="sxs-lookup"><span data-stu-id="b000b-288">jQuery Validation 1.8</span></span>
- <span data-ttu-id="b000b-289">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="b000b-289">jQuery UI 1.8.11</span></span>

<span data-ttu-id="b000b-290">作为预安装的 NuGet 包中包含这些库。</span><span class="sxs-lookup"><span data-stu-id="b000b-290">These libraries are included as pre-installed NuGet packages.</span></span>

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a><span data-ttu-id="b000b-291">项目模板现在包含 ADO.NET Entity Framework 4.1 作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b000b-291">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>

<span data-ttu-id="b000b-292">ADO.NET Entity Framework 4.1 包含代码优先功能。</span><span class="sxs-lookup"><span data-stu-id="b000b-292">The ADO.NET Entity Framework 4.1 includes the Code First feature.</span></span> <span data-ttu-id="b000b-293">Code First 是 ADO.NET 实体框架提供的现有数据库优先和模型优先模式的替代方法的新开发模式。</span><span class="sxs-lookup"><span data-stu-id="b000b-293">Code First is a new development pattern for the ADO.NET Entity Framework that provides an alternative to the existing Database First and Model First patterns.</span></span>

<span data-ttu-id="b000b-294">首先是专注于代码周围定义模型使用 POCO 类 （"普通旧 CLR 对象"） 在 Visual Basic 或 C# 编写。</span><span class="sxs-lookup"><span data-stu-id="b000b-294">Code First is focused around defining your model using POCO classes ("plain old CLR objects") written in Visual Basic or C#.</span></span> <span data-ttu-id="b000b-295">这些类然后可以映射到现有数据库或用于生成数据库架构。</span><span class="sxs-lookup"><span data-stu-id="b000b-295">These classes can then be mapped to an existing database or be used to generate a database schema.</span></span> <span data-ttu-id="b000b-296">可以使用提供额外的配置*DataAnnotations*属性或使用 fluent Api。</span><span class="sxs-lookup"><span data-stu-id="b000b-296">Additional configuration can be supplied using *DataAnnotations* attributes or using fluent APIs.</span></span>

<span data-ttu-id="b000b-297">有关使用代码 Firstwith ASP.NET MVC 文档位于以下 Url 的 ASP.NET 网站上有：</span><span class="sxs-lookup"><span data-stu-id="b000b-297">Documentation for using Code Firstwith ASP.NET MVC is available on the ASP.NET website at the following URLs:</span></span>

<span data-ttu-id="b000b-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="b000b-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span></span>

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a><span data-ttu-id="b000b-299">项目模板包含 JavaScript 库作为预安装的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b000b-299">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>

<span data-ttu-id="b000b-300">该项目时创建新的 ASP.NET MVC 3 项目时，通过安装其包括前面提到的 JavaScript 文件 （例如，Modernizr 库） 而不直接将脚本添加到脚本文件夹中的项目模板中使用 NuGet内容。</span><span class="sxs-lookup"><span data-stu-id="b000b-300">When you create a new ASP.NET MVC 3 project, the project includes the JavaScript files mentioned previously (for example, the Modernizr library) by installing them using NuGet instead of directly adding the scripts to the Scripts folder in the project template contents.</span></span> <span data-ttu-id="b000b-301">这使您能够使用 NuGet，当发布新版本的脚本时将脚本更新为最新版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-301">This enables you to use NuGet to update the scripts to the latest version when new versions of the scripts are released.</span></span>

<span data-ttu-id="b000b-302">例如，提供新的 jQuery 版本频率以后，项目模板中包含的 jQuery 版本在某个时候将过期。</span><span class="sxs-lookup"><span data-stu-id="b000b-302">For example, given the frequency of new jQuery releases, the version of jQuery included in the project template will at some point be out of date.</span></span> <span data-ttu-id="b000b-303">但是，由于 jQuery 是作为已安装的 NuGet 软件包包含在内，您将时通知你在 NuGet 对话框中提供了较新版本的 jQuery。</span><span class="sxs-lookup"><span data-stu-id="b000b-303">However, because jQuery is included as an installed NuGet package, you will be notified in the NuGet dialog box when newer versions of jQuery are available.</span></span>

<span data-ttu-id="b000b-304">由于 jQuery 在文件名中包含的版本号，因此更新到最新版本的 jQuery 还需要更新`<script>`引用 jQuery 文件以使用新的文件名称的标记。</span><span class="sxs-lookup"><span data-stu-id="b000b-304">Because jQuery includes the version number in the file name, updating jQuery to the latest version also requires updating the `<script>` tag that references the jQuery file to use the new file name.</span></span> <span data-ttu-id="b000b-305">其他包含的脚本库不包括版本号中的脚本名称，因此它们可以更轻松地更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-305">Other included script libraries do not include the version number in the script name, so they can be more easily updated to their latest versions.</span></span>

<a id="tu-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="b000b-306">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-306">Known Issues</span></span>

- <span data-ttu-id="b000b-307">在某些情况下，安装可能会因错误消息"安装失败，错误代码为 (0x80070643)"。</span><span class="sxs-lookup"><span data-stu-id="b000b-307">In some cases, installation may fail with the error message "Installation failed with error code (0x80070643)".</span></span> <span data-ttu-id="b000b-308">有关如何解决此问题的信息，请参阅[知识库文章 2531566](https://support.microsoft.com/kb/2531566)。</span><span class="sxs-lookup"><span data-stu-id="b000b-308">For information about how to work around this issue, see [KnowledgeBase article 2531566](https://support.microsoft.com/kb/2531566).</span></span>
- <span data-ttu-id="b000b-309">添加控制器基架不会创建利用实体继承支持实体框架中的实体基架。</span><span class="sxs-lookup"><span data-stu-id="b000b-309">The scaffolding for adding a controller does not scaffold entities that take advantage of entity inheritance support within Entity Framework.</span></span> <span data-ttu-id="b000b-310">例如，给定基*Person*由继承的类*学生*类，搭建基架*学生*类将导致生成不会进行编译的代码。</span><span class="sxs-lookup"><span data-stu-id="b000b-310">For example, given a base *Person* class that's inherited by a *Student* class, scaffolding the *Student* class will result in generated code that does not compile.</span></span>
- <span data-ttu-id="b000b-311">创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="b000b-311">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="b000b-312">解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="b000b-312">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="b000b-313">在安装 ReSharper 时 IntelliSense for Razor 语法无效。</span><span class="sxs-lookup"><span data-stu-id="b000b-313">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="b000b-314">如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。</span><span class="sxs-lookup"><span data-stu-id="b000b-314">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="b000b-315">在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。</span><span class="sxs-lookup"><span data-stu-id="b000b-315">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="b000b-316">当您编辑 Razor 视图 (.cshtml 或。*vbhtml*文件)，视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-316">When you are editing a Razor view (.cshtml or .*vbhtml* file), views.</span></span> <span data-ttu-id="b000b-317">ASP.NET MVC 3 不包括 Razor 视图的任何代码段...aspxselecting ASP.NET MVC 的代码段将显示有关代码段</span><span class="sxs-lookup"><span data-stu-id="b000b-317">ASP.NET MVC 3 does not include any snippets for Razor views..aspxselecting a code snippet for ASP.NET MVC will show snippets for</span></span>
- <span data-ttu-id="b000b-318">如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="b000b-318">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="b000b-319">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-319">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="b000b-320">ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。</span><span class="sxs-lookup"><span data-stu-id="b000b-320">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a><span data-ttu-id="b000b-321">ASP.NET MVC 3 RTM 中的更改</span><span class="sxs-lookup"><span data-stu-id="b000b-321">Changes in ASP.NET MVC 3 RTM</span></span>

<span data-ttu-id="b000b-322">本部分介绍更改和自 RC2 发行以来 ASP.NET MVC 3 RTM 版本中所做的 bug 修补程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-322">This section describes changes and bug fixes made in the ASP.NET MVC 3 RTM release since the RC2 release.</span></span>

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a><span data-ttu-id="b000b-323">更改： 更新版本的 jQuery UI 1.8.7 为</span><span class="sxs-lookup"><span data-stu-id="b000b-323">Change: Updated the version of jQuery UI to 1.8.7</span></span>

<span data-ttu-id="b000b-324">Visual Studio 的 ASP.NET MVC 项目模板已更新以包括最新版本的 jQuery UI 库。</span><span class="sxs-lookup"><span data-stu-id="b000b-324">The ASP.NET MVC project templates for Visual Studio were updated to include the latest version of the jQuery UI library.</span></span> <span data-ttu-id="b000b-325">模板还包含所需的 jQuery UI，如关联的 CSS 和图像文件的资源文件的最小集。</span><span class="sxs-lookup"><span data-stu-id="b000b-325">The templates also include the minimal set of resource files required by jQuery UI, such as the associated CSS and image files.</span></span>

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a><span data-ttu-id="b000b-326">更改： 更改 ModelMetadataProvider 回 DataAnnotationsModelMetadataProvider 了默认值</span><span class="sxs-lookup"><span data-stu-id="b000b-326">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>

<span data-ttu-id="b000b-327">RC2 版本的 ASP.NET MVC 3 引入*CachedDataAnnotationsMetadataProvider*类，提供基于现有缓存*DataAnnotationsModelMetadataProvider*声明为类性能改进。</span><span class="sxs-lookup"><span data-stu-id="b000b-327">The RC2 release of ASP.NET MVC 3 introduced a *CachedDataAnnotationsMetadataProvider* class that provided caching on top of the existing *DataAnnotationsModelMetadataProvider* class as a performance improvement.</span></span> <span data-ttu-id="b000b-328">但是，某些 bug 报告与此实现中，以便还原此更改并将其移到 MVC Futures 项目，可在[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)。</span><span class="sxs-lookup"><span data-stu-id="b000b-328">However, some bugs were reported with this implementation, so the change has been reverted and moved into the MVC Futures project, which is available at [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a><span data-ttu-id="b000b-329">已修复： 粘贴 Razor 表达式包含空格导致它被反转的部分</span><span class="sxs-lookup"><span data-stu-id="b000b-329">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>

<span data-ttu-id="b000b-330">在 ASP.NET MVC 3 的预发布版本中，粘贴到 Razor 文件中，包含空格的 Razor 表达式的一部分时所生成的表达式应反向执行。</span><span class="sxs-lookup"><span data-stu-id="b000b-330">In pre-release versions of ASP.NET MVC 3, when you paste a part of a Razor expression that contains whitespace into a Razor file, the resulting expression is reversed.</span></span> <span data-ttu-id="b000b-331">例如，考虑以下 Razor 代码块：</span><span class="sxs-lookup"><span data-stu-id="b000b-331">For example, consider the following Razor code block:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

<span data-ttu-id="b000b-332">如果您在第一种方法中选择"第一个 param"文本并将其作为自变量粘贴到第二种方法，则结果是，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-332">If you select the text "first param" in the first method and paste it as an argument into the second method, the result is as follows:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="b000b-333">正确的行为是粘贴操作应导致以下：</span><span class="sxs-lookup"><span data-stu-id="b000b-333">The correct behavior is that the paste operation should result in the following:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

<span data-ttu-id="b000b-334">已在 RTM 版本中修复此问题，以便表达式正确地保留在粘贴操作。</span><span class="sxs-lookup"><span data-stu-id="b000b-334">This issue has been fixed in the RTM release so that the expression is correctly preserved during the paste operation.</span></span>

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a><span data-ttu-id="b000b-335">已修复： 重命名在编辑器中打开的 Razor 文件禁用语法着色和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b000b-335">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>

<span data-ttu-id="b000b-336">重命名在编辑器窗口中打开文件时使用解决方案资源管理器的 Razor 文件会导致语法突出显示和 IntelliSense 停止工作，为该文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-336">Renaming a Razor file using Solution Explorer while the file is opened in the editor window causes syntax highlighting and IntelliSense to stop working for that file.</span></span> <span data-ttu-id="b000b-337">此问题已修复，以便突出显示和 IntelliSense 维护之后重命名。</span><span class="sxs-lookup"><span data-stu-id="b000b-337">This has been fixed so that highlighting and IntelliSense are maintained after a rename.</span></span>

<a id="RTM-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="b000b-338">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-338">Known Issues</span></span>

- <span data-ttu-id="b000b-339">如果您关闭 Visual Studio 2010 SP1 Beta，NuGet 包管理器控制台处于打开状态时，Visual Studio 崩溃，并尝试重新启动。</span><span class="sxs-lookup"><span data-stu-id="b000b-339">If you close Visual Studio 2010 SP1 Beta while the NuGet Package Manager Console is open, Visual Studio crashes and attempts to restart.</span></span> <span data-ttu-id="b000b-340">这将修复 Visual Studio 2010 SP1 的 RTM 版本中。</span><span class="sxs-lookup"><span data-stu-id="b000b-340">This will be fixed in the RTM release of Visual Studio 2010 SP1.</span></span>
- <span data-ttu-id="b000b-341">ASP.NET MVC 3 安装程序才能够安装 NuGet 包管理器的初始版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-341">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="b000b-342">已安装的初始版本后，NuGet 可以安装和使用 Visual Studio Extension Manager 更新。</span><span class="sxs-lookup"><span data-stu-id="b000b-342">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="b000b-343">如果已安装 NuGet，请转到 Visual Studio 扩展库更新到最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="b000b-343">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="b000b-344">创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="b000b-344">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="b000b-345">解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="b000b-345">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="b000b-346">安装程序可能需要更长的时间比以前版本的 ASP.NET MVC 来完成。</span><span class="sxs-lookup"><span data-stu-id="b000b-346">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="b000b-347">这是因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-347">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="b000b-348">在安装 ReSharper 时 IntelliSense for Razor 语法无效。</span><span class="sxs-lookup"><span data-stu-id="b000b-348">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="b000b-349">如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。</span><span class="sxs-lookup"><span data-stu-id="b000b-349">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="b000b-350">与 ASP.NET MVC 3 的测试版创建的 CCSHTML 和 VBHTML 视图没有正确设置其生成操作，使用这些查看结果类型时省略了该项目发布。</span><span class="sxs-lookup"><span data-stu-id="b000b-350">CCSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="b000b-351">这些文件的生成操作值应设置为"内容"。</span><span class="sxs-lookup"><span data-stu-id="b000b-351">The Build Action value for these files should be set to "Content".</span></span> <span data-ttu-id="b000b-352">ASP.NET MVC 3 RTM 修复了对新文件，此问题，但不会更正与预发布版本创建的项目的现有文件的设置。</span><span class="sxs-lookup"><span data-stu-id="b000b-352">ASP.NET MVC 3 RTM fixes this issue for new files, but doesn't correct the setting for existing files for a project created with prerelease versions.</span></span>
- ![](mvc3-release-notes/_static/image3.png)
- <span data-ttu-id="b000b-353">在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。</span><span class="sxs-lookup"><span data-stu-id="b000b-353">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="b000b-354">编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。</span><span class="sxs-lookup"><span data-stu-id="b000b-354">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="b000b-355">如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="b000b-355">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="b000b-356">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-356">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="b000b-357">ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。</span><span class="sxs-lookup"><span data-stu-id="b000b-357">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="b000b-358">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-358">Breaking Changes</span></span>

- <span data-ttu-id="b000b-359">在以前版本的 ASP.NET MVC，操作筛选器是每个请求除在少数情况下创建。</span><span class="sxs-lookup"><span data-stu-id="b000b-359">In previous versions of ASP.NET MVC, action filters are create per request except in a few cases.</span></span> <span data-ttu-id="b000b-360">此行为永远不会有保证的行为，但只是实现详细信息，筛选器的约定是将其视为无状态。</span><span class="sxs-lookup"><span data-stu-id="b000b-360">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="b000b-361">在 ASP.NET MVC 3 中，将更主动的方式缓存筛选器。</span><span class="sxs-lookup"><span data-stu-id="b000b-361">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="b000b-362">因此，实例状态不正确存储任何自定义操作筛选器可能已损坏。</span><span class="sxs-lookup"><span data-stu-id="b000b-362">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="b000b-363">异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-363">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="b000b-364">在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*值上的操作方法的异常筛选器之前执行这些操作方法上时。</span><span class="sxs-lookup"><span data-stu-id="b000b-364">In ASP.NET MVC 2 and earlier, exception filters on the controller that have the same *Order* value as those on an action method are executed before the exception filters on the action method.</span></span> <span data-ttu-id="b000b-365">这通常会是这种情况，异常筛选器应用时没有指定*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-365">This would typically be the case when exception filters are applied without a specified *Order* value.</span></span> <span data-ttu-id="b000b-366">在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。</span><span class="sxs-lookup"><span data-stu-id="b000b-366">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="b000b-367">在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="b000b-367">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="b000b-368">名为的新属性*FileExtensions*已添加到*VirtualPathProviderViewEngine*基类。</span><span class="sxs-lookup"><span data-stu-id="b000b-368">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="b000b-369">当 ASP.NET 视图按路径 （不按名称查找） 时，被视为唯一视图与此新属性指定的列表中包含的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-369">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="b000b-370">若要启用 Web 窗体视图的自定义文件扩展注册自定义生成提供程序和提供程序使用完整路径而不是一个名称来引用这些视图，这是在应用程序中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="b000b-370">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="b000b-371">解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-371">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="b000b-372">直接实现的自定义控制器工厂实现*IControllerFactory*接口必须提供的新实现*GetControllerSessionBehavior*方法添加到此版本中的接口。</span><span class="sxs-lookup"><span data-stu-id="b000b-372">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="b000b-373">一般情况下，建议您不要直接实现此接口和改为从类派生*借助于 DefaultControllerFactory*。</span><span class="sxs-lookup"><span data-stu-id="b000b-373">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a><span data-ttu-id="b000b-374">ASP.NET MVC 3 RC2 中的更改</span><span class="sxs-lookup"><span data-stu-id="b000b-374">Changes in ASP.NET MVC 3 RC2</span></span>

<span data-ttu-id="b000b-375">本部分介绍了 RC 版本发布以来 ASP.NET MVC 3 RC2 版本中所做的更改 （新功能和 bug 修复）。</span><span class="sxs-lookup"><span data-stu-id="b000b-375">This section describes changes (new features and bug fixes) made in the ASP.NET MVC 3 RC2 release since the RC release.</span></span>

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a><span data-ttu-id="b000b-376">项目模板更改为包括 jQuery 1.4.4、 jQuery 验证 1.7 和 jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b000b-376">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6</span></span>

<span data-ttu-id="b000b-377">ASP.NET MVC 3 的项目模板现在包括最新版本的 jQuery、 验证、 jQuery 和 jQuery UI。</span><span class="sxs-lookup"><span data-stu-id="b000b-377">The project templates for ASP.NET MVC 3 now include the latest versions of jQuery, jQuery Validation, and jQuery UI.</span></span> <span data-ttu-id="b000b-378">jQuery UI 是一个新项目模板，并提供有用的用户界面小组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-378">jQuery UI is a new addition to the project templates and provides useful user interface widgets.</span></span> <span data-ttu-id="b000b-379">有关的 jQuery UI 的详细信息，请访问其主页： [ http://jqueryui.com/ ](http://jqueryui.com/)。</span><span class="sxs-lookup"><span data-stu-id="b000b-379">For more information about jQuery UI, visit their homepage: [http://jqueryui.com/](http://jqueryui.com/).</span></span>

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a><span data-ttu-id="b000b-380">添加了"AdditionalMetadataAttribute"类</span><span class="sxs-lookup"><span data-stu-id="b000b-380">Added "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="b000b-381">可以使用*AdditionalMetadataAttribute*类来填充*ModelMetadata.AdditionalValues*模型属性的字典。</span><span class="sxs-lookup"><span data-stu-id="b000b-381">You can use the *AdditionalMetadataAttribute* class to populate the *ModelMetadata.AdditionalValues* dictionary for a model property.</span></span>

<span data-ttu-id="b000b-382">例如，假设视图模型具有应仅向管理员显示的属性。</span><span class="sxs-lookup"><span data-stu-id="b000b-382">For example, suppose a view model has properties that should be displayed only to an administrator.</span></span> <span data-ttu-id="b000b-383">该模型可以批注使用新的属性使用 AdminOnly 作为密钥并将 true 作为值，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-383">That model can be annotated with the new attribute using AdminOnly as the key and true as the value, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

<span data-ttu-id="b000b-384">呈现产品视图模型时，此元数据将提供到任何显示或编辑器的模板。</span><span class="sxs-lookup"><span data-stu-id="b000b-384">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="b000b-385">它取决于您是为应用程序开发人员解释元数据信息。</span><span class="sxs-lookup"><span data-stu-id="b000b-385">It is up to you as application developer to interpret the metadata information.</span></span>

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a><span data-ttu-id="b000b-386">改进了的视图基架</span><span class="sxs-lookup"><span data-stu-id="b000b-386">Improved View Scaffolding</span></span>

<span data-ttu-id="b000b-387">现在使用的基架视图的 T4 模板生成对模板帮助器方法的调用，如*EditorFor*而不是帮助程序，例如*TextBoxFor*。</span><span class="sxs-lookup"><span data-stu-id="b000b-387">The T4 templates used for scaffolding views now generate calls to template helper methods such as *EditorFor* instead of helpers such as *TextBoxFor*.</span></span> <span data-ttu-id="b000b-388">当添加视图对话框中生成一个视图时，此更改将提高对数据批注特性的窗体中的模型的元数据的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-388">This change improves support for metadata on the model in the form of data annotation attributes when the Add View dialog box generates a view.</span></span>

<span data-ttu-id="b000b-389">添加视图基架还包括改进的检测和主键信息基于约定的模型上的使用情况。</span><span class="sxs-lookup"><span data-stu-id="b000b-389">The Add View scaffolding also includes improved detection and usage of primary key information on the model, based on convention.</span></span> <span data-ttu-id="b000b-390">例如，添加视图对话框中使用此信息以确保主键值不基架为可编辑窗体字段。</span><span class="sxs-lookup"><span data-stu-id="b000b-390">For example, the Add View dialog box uses this information to ensure that the primary key value is not scaffolded as an editable form field.</span></span>

<span data-ttu-id="b000b-391">默认编辑和创建模板包括对客户端验证所需的 jQuery 脚本的引用。</span><span class="sxs-lookup"><span data-stu-id="b000b-391">The default Edit and Create templates include references to the jQuery scripts needed for client validation.</span></span>

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a><span data-ttu-id="b000b-392">添加的 Html.Raw 方法</span><span class="sxs-lookup"><span data-stu-id="b000b-392">Added Html.Raw Method</span></span>

<span data-ttu-id="b000b-393">默认情况下，Razor 视图引擎进行 HTML 编码的所有值。</span><span class="sxs-lookup"><span data-stu-id="b000b-393">By default, the Razor view engine HTML-encodes all values.</span></span> <span data-ttu-id="b000b-394">例如，下面的代码段将编码的问候语变量中的 HTML，以便显示在页中作为`<strong>Hello World!</strong>`。</span><span class="sxs-lookup"><span data-stu-id="b000b-394">For example, the following code snippet encodes the HTML inside the greeting variable so that it is displayed in the page as `<strong>Hello World!</strong>`.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

<span data-ttu-id="b000b-395">新*Html.Raw*方法提供了显示未编码的 HTML 时知道的内容是安全的简单方式。</span><span class="sxs-lookup"><span data-stu-id="b000b-395">The new *Html.Raw* method provides a simple way of displaying unencoded HTML when the content is known to be safe.</span></span> <span data-ttu-id="b000b-396">下面的示例显示相同的字符串，但该字符串呈现为标记：</span><span class="sxs-lookup"><span data-stu-id="b000b-396">The following example displays the same string, but the string is rendered as markup:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a><span data-ttu-id="b000b-397">已重命名"Controller.ViewModel"属性和"ViewBag"到"视图"属性</span><span class="sxs-lookup"><span data-stu-id="b000b-397">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>

<span data-ttu-id="b000b-398">以前， *ViewModel*的属性*控制器*对应于*视图*视图的属性。</span><span class="sxs-lookup"><span data-stu-id="b000b-398">Previously, the *ViewModel* property of *Controller* corresponded to the *View* property of a view.</span></span> <span data-ttu-id="b000b-399">两个属性提供的访问值的方式*ViewDataDictionary*对象使用动态属性访问器语法。</span><span class="sxs-lookup"><span data-stu-id="b000b-399">Both of these properties provide a way to access values of the *ViewDataDictionary* object using dynamic property-accessor syntax.</span></span> <span data-ttu-id="b000b-400">这两个属性已重命名为相同以避免产生混淆和更一致。</span><span class="sxs-lookup"><span data-stu-id="b000b-400">Both properties have been renamed to be the same in order to avoid confusion and to be more consistent.</span></span>

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a><span data-ttu-id="b000b-401">已重命名"ControllerSessionStateAttribute"类"SessionStateAttribute"</span><span class="sxs-lookup"><span data-stu-id="b000b-401">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>

<span data-ttu-id="b000b-402">*ControllerSessionStateAttribute* RC 版本的 ASP.NET MVC 3 中引入了类。</span><span class="sxs-lookup"><span data-stu-id="b000b-402">The *ControllerSessionStateAttribute* class was introduced in the RC release of ASP.NET MVC 3.</span></span> <span data-ttu-id="b000b-403">该属性已重命名为更简洁。</span><span class="sxs-lookup"><span data-stu-id="b000b-403">The property was renamed to be more succinct.</span></span>

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a><span data-ttu-id="b000b-404">已重命名的 RemoteAttribute"字段"属性设置为"AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="b000b-404">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>

<span data-ttu-id="b000b-405">*RemoteAttribute*类的*字段*属性造成了某些困扰用户之间。</span><span class="sxs-lookup"><span data-stu-id="b000b-405">The *RemoteAttribute* class's *Fields* property caused some confusion among users.</span></span> <span data-ttu-id="b000b-406">重命名此属性设置为*AdditionalFields*阐明了其意图。</span><span class="sxs-lookup"><span data-stu-id="b000b-406">Renaming this property to *AdditionalFields* clarifies its intent.</span></span>

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a><span data-ttu-id="b000b-407">重命名"SkipRequestValidationAttribute"到"AllowHtmlAttribute"</span><span class="sxs-lookup"><span data-stu-id="b000b-407">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>

<span data-ttu-id="b000b-408">*SkipRequestValidationAttribute*属性已重命名为*AllowHtmlAttribute*来更好地表示其预期的用法。</span><span class="sxs-lookup"><span data-stu-id="b000b-408">The *SkipRequestValidationAttribute* attribute was renamed to *AllowHtmlAttribute* to better represent its intended usage.</span></span>

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a><span data-ttu-id="b000b-409">已更改"Html.ValidationMessage"方法来显示第一条有用的错误消息</span><span class="sxs-lookup"><span data-stu-id="b000b-409">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>

<span data-ttu-id="b000b-410">*Html.ValidationMessage*方法已固定的以便显示而不是只需显示的第一个错误的第一个有用的错误消息。</span><span class="sxs-lookup"><span data-stu-id="b000b-410">The *Html.ValidationMessage* method was fixed to show the first useful error message instead of simply displaying the first error.</span></span>

<span data-ttu-id="b000b-411">在模型绑定期间*ModelState*可以通过使用有关的属性，包括从模型本身的错误消息的多个源填充字典 (如果它实现了*IValidatableObject*)，从验证特性应用于属性，以及从在访问属性时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="b000b-411">During model binding, the *ModelState* dictionary can be populated from multiple sources with error messages about the property, including from the model itself (if it implements *IValidatableObject*), from validation attributes applied to the property, and from exceptions thrown while the property is being accessed.</span></span>

<span data-ttu-id="b000b-412">当*Html.ValidationMessage*方法显示一条验证消息时，它将模型状态，其中可包含一个异常，跳过，因为这些通常不应为最终用户。</span><span class="sxs-lookup"><span data-stu-id="b000b-412">When the *Html.ValidationMessage* method displays a validation message, it skips model-state entries that include an exception, because these are generally not intended for the end user.</span></span> <span data-ttu-id="b000b-413">相反，该方法将查找不是与异常相关联，并显示该消息的第一个验证消息。</span><span class="sxs-lookup"><span data-stu-id="b000b-413">Instead, the method looks for the first validation message that is not associated with an exception and displays that message.</span></span> <span data-ttu-id="b000b-414">如果不找到任何此类消息，则默认为与第一个异常相关联的一般性错误消息。</span><span class="sxs-lookup"><span data-stu-id="b000b-414">If no such message is found, it defaults to a generic error message that is associated with the first exception.</span></span>

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a><span data-ttu-id="b000b-415">固定@model声明，以将空格添加到文档</span><span class="sxs-lookup"><span data-stu-id="b000b-415">Fixed @model Declaration to not Add Whitespace to the Document</span></span>

<span data-ttu-id="b000b-416">在早期版本中， <em>@model</em>视图顶部的声明添加到呈现的 HTML 输出一个空行。</span><span class="sxs-lookup"><span data-stu-id="b000b-416">In earlier releases, the <em>@model</em> declaration at the top of a view added a blank line to the rendered HTML output.</span></span> <span data-ttu-id="b000b-417">此问题已修复，以便声明不会引入的空格。</span><span class="sxs-lookup"><span data-stu-id="b000b-417">This has been fixed so that the declaration does not introduce whitespace.</span></span>

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a><span data-ttu-id="b000b-418">添加了"FileExtensions"属性设置为视图引擎，以支持特定于引擎的文件的名称</span><span class="sxs-lookup"><span data-stu-id="b000b-418">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>

<span data-ttu-id="b000b-419">视图引擎可以返回视图，使用显式视图路径如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-419">A view engine can return a view using an explicit view path as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

<span data-ttu-id="b000b-420">第一个视图引擎始终尝试呈现视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-420">The first view engine always attempts to render the view.</span></span> <span data-ttu-id="b000b-421">默认情况下，Web 窗体视图引擎是第一个视图引擎;因为 Web 窗体引擎不能呈现 Razor 视图，就会出错。</span><span class="sxs-lookup"><span data-stu-id="b000b-421">By default, the Web Forms view engine is the first view engine; because the Web Forms engine cannot render a Razor view, an error occurs.</span></span> <span data-ttu-id="b000b-422">视图引擎现在都有*FileExtensions*它们支持的属性，用于指定哪些文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-422">View engines now have a *FileExtensions* property that is used to specify which file extensions they support.</span></span> <span data-ttu-id="b000b-423">当 ASP.NET 确定视图引擎是否可以呈现文件时，检查此属性。</span><span class="sxs-lookup"><span data-stu-id="b000b-423">This property is checked when ASP.NET determines whether a view engine can render a file.</span></span> <span data-ttu-id="b000b-424">这是一项重大更改，更多详细信息包含在[的重大更改](#_Toc2_BC)本文档的部分。</span><span class="sxs-lookup"><span data-stu-id="b000b-424">This is a breaking change and more details are included in the [Breaking Changes](#_Toc2_BC) section of this document.</span></span>

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a><span data-ttu-id="b000b-425">要发出"For"属性的正确值的固定"LabelFor"帮助程序</span><span class="sxs-lookup"><span data-stu-id="b000b-425">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>

<span data-ttu-id="b000b-426">已修复 bug 的位置*LabelFor*方法呈现*有关*匹配的属性*输入*元素的*名称*特性其 id。</span><span class="sxs-lookup"><span data-stu-id="b000b-426">A bug was fixed where the *LabelFor* method rendered a *for* attribute that matches the *input* element's *name* attribute instead of its ID.</span></span> <span data-ttu-id="b000b-427">根据 W3C*有关*属性应与匹配*输入*元素的 id。</span><span class="sxs-lookup"><span data-stu-id="b000b-427">According to the W3C, the *for* attribute should match the *input* element's ID.</span></span>

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a><span data-ttu-id="b000b-428">固定"RenderAction"方法，从而使在模型绑定期间的显式值优先级</span><span class="sxs-lookup"><span data-stu-id="b000b-428">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>

<span data-ttu-id="b000b-429">在早期版本中，显式值传递给*RenderAction*方法已被忽略，以便支持当前的窗体值在子操作中的模型绑定期间。</span><span class="sxs-lookup"><span data-stu-id="b000b-429">In earlier versions, explicit values that were passed to the *RenderAction* method were being ignored in favor of the current form values during model binding inside a child action.</span></span> <span data-ttu-id="b000b-430">此修复可以确保，在模型绑定期间优先的显式值。</span><span class="sxs-lookup"><span data-stu-id="b000b-430">The fix ensures that explicit values take precedence during model binding.</span></span>

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="b000b-431">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-431">Breaking Changes</span></span>

- <span data-ttu-id="b000b-432">在以前版本的 ASP.NET MVC 中，每个请求除在少数情况下创建操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="b000b-432">In previous versions of ASP.NET MVC, action filters were created per request except in a few cases.</span></span> <span data-ttu-id="b000b-433">此行为永远不会有保证的行为，但只是实现详细信息，筛选器的约定是将其视为无状态。</span><span class="sxs-lookup"><span data-stu-id="b000b-433">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="b000b-434">在 ASP.NET MVC 3 中，将更主动的方式缓存筛选器。</span><span class="sxs-lookup"><span data-stu-id="b000b-434">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="b000b-435">因此，实例状态不正确存储任何自定义操作筛选器可能已损坏。</span><span class="sxs-lookup"><span data-stu-id="b000b-435">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="b000b-436">异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-436">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="b000b-437">在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*值上的操作方法的异常筛选器之前执行这些操作方法上。</span><span class="sxs-lookup"><span data-stu-id="b000b-437">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* value as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="b000b-438">异常筛选器应用时，这通常会发生此情况没有指定*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-438">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="b000b-439">在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。</span><span class="sxs-lookup"><span data-stu-id="b000b-439">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="b000b-440">在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="b000b-440">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="b000b-441">名为的新属性*FileExtensions*已添加到*VirtualPathProviderViewEngine*基类。</span><span class="sxs-lookup"><span data-stu-id="b000b-441">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="b000b-442">当 ASP.NET 视图按路径 （不按名称查找） 时，被视为唯一视图与此新属性指定的列表中包含的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-442">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="b000b-443">若要启用 Web 窗体视图的自定义文件扩展注册自定义生成提供程序和提供程序使用完整路径而不是一个名称来引用这些视图，这是在应用程序中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="b000b-443">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="b000b-444">解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-444">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="b000b-445">直接实现的自定义控制器工厂实现<em>IControllerFactory</em>接口必须提供的新实现<em>GetControllerSessionBehavior</em> <em>已添加到此版本中的接口方法</em>。</span><span class="sxs-lookup"><span data-stu-id="b000b-445">Custom controller factory implementations that directly implement the <em>IControllerFactory</em> interface must provide an implementation of the new <em>GetControllerSessionBehavior</em><em>method that was added to the interface in this release</em>.</span></span> <span data-ttu-id="b000b-446">一般情况下，建议您不要直接实现此接口和改为从类派生<em>借助于 DefaultControllerFactory</em>。</span><span class="sxs-lookup"><span data-stu-id="b000b-446">In general, it is recommended that you do not implement this interface directly and instead derive your class from <em>DefaultControllerFactory</em>.</span></span>

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a><span data-ttu-id="b000b-447">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-447">Known Issues</span></span>

- <span data-ttu-id="b000b-448">ASP.NET MVC 3 安装程序才能够安装 NuGet 包管理器的初始版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-448">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="b000b-449">已安装的初始版本后，NuGet 可以安装和使用 Visual Studio Extension Manager 更新。</span><span class="sxs-lookup"><span data-stu-id="b000b-449">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="b000b-450">如果已安装 NuGet，请转到 Visual Studio 扩展库更新到最新版本的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="b000b-450">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="b000b-451">创建新的 ASP.NET MVC 3 项目解决方案文件夹中的原因*NullReferenceException*错误。</span><span class="sxs-lookup"><span data-stu-id="b000b-451">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="b000b-452">解决方法是在解决方案的根目录中创建 ASP.NET MVC 3 项目，然后将它移动到解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="b000b-452">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="b000b-453">安装程序可能需要更长的时间比以前版本的 ASP.NET MVC 来完成。</span><span class="sxs-lookup"><span data-stu-id="b000b-453">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="b000b-454">这是因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-454">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="b000b-455">在安装 ReSharper 时 IntelliSense for Razor 语法无效。</span><span class="sxs-lookup"><span data-stu-id="b000b-455">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="b000b-456">如果安装了 ReSharper 并且想要在 ASP.NET MVC 3 RC2 中利用 Razor IntelliSense 支持，请参阅文章[Razor Intellisense 和 ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)上 Hadi Hariri 的博客文章，其中讨论了如何立即使用它们在一起。</span><span class="sxs-lookup"><span data-stu-id="b000b-456">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3 RC2, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="b000b-457">与 ASP.NET MVC 3 的测试版创建的 CSHTML 和 VBHTML 视图没有正确设置其生成操作，使用这些查看结果类型时省略了该项目发布。</span><span class="sxs-lookup"><span data-stu-id="b000b-457">CSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="b000b-458">*生成操作*值这些文件应设置为内容"。</span><span class="sxs-lookup"><span data-stu-id="b000b-458">The *Build Action* value for these files should be set to Content".</span></span> <span data-ttu-id="b000b-459">ASP.NET MVC 3 RC2 修复了对新文件，此问题，但不会更正与测试版创建的项目的现有文件的设置。![](mvc3-release-notes/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b000b-459">ASP.NET MVC 3 RC2 fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta version.![](mvc3-release-notes/_static/image4.png)</span></span>
- <span data-ttu-id="b000b-460">在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。</span><span class="sxs-lookup"><span data-stu-id="b000b-460">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="b000b-461">编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。</span><span class="sxs-lookup"><span data-stu-id="b000b-461">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="b000b-462">如果 ASP.NET MVC 3 Visual Web Developer 速成版上安装的计算机，其中未安装 Visual Studio，并在以后安装 Visual Studio，则必须重新安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="b000b-462">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="b000b-463">Visual Studio 和 Visual Web Developer Express 共享由 ASP.NET MVC 3 安装程序升级的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-463">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="b000b-464">ASP.NET MVC 3 是 Visual studio 尚未 Visual Web Developer 速成版和更高版本安装 Visual Web Developer 速成版的计算机上安装适用于相同的问题。</span><span class="sxs-lookup"><span data-stu-id="b000b-464">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>
- <span data-ttu-id="b000b-465">安装 ASP.NET MVC 3 RC 2 不会更新 NuGet，如果你已安装它。</span><span class="sxs-lookup"><span data-stu-id="b000b-465">Installing ASP.NET MVC 3 RC 2 does not update NuGet if you already have it installed.</span></span> <span data-ttu-id="b000b-466">若要升级 NuGet，请转到 Visual Studio 扩展管理器和它应显示为可用的更新。</span><span class="sxs-lookup"><span data-stu-id="b000b-466">To upgrade NuGet, go to the Visual Studio Extension manager and it should show up as an available update.</span></span> <span data-ttu-id="b000b-467">你可以升级到最新版本从那里 NuGet。</span><span class="sxs-lookup"><span data-stu-id="b000b-467">You can upgrade NuGet to the latest release from there.</span></span>

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a><span data-ttu-id="b000b-468">ASP.NET MVC 3 的候选发布版本</span><span class="sxs-lookup"><span data-stu-id="b000b-468">ASP.NET MVC 3 Release Candidate</span></span>

<span data-ttu-id="b000b-469">ASP.NET MVC 候选发布版本已于 2010 年 11 月 9 日发布。</span><span class="sxs-lookup"><span data-stu-id="b000b-469">ASP.NET MVC Release Candidate was released on November 9, 2010.</span></span>

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a><span data-ttu-id="b000b-470">ASP.NET MVC 3 RC 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="b000b-470">New Features in ASP.NET MVC 3 RC</span></span>

<span data-ttu-id="b000b-471">本部分介绍已引入的功能的 Beta 版本以来 ASP.NET MVC 3 RC 版本中。</span><span class="sxs-lookup"><span data-stu-id="b000b-471">This section describes features that have been introduced in the ASP.NET MVC 3 RC release since the Beta release.</span></span>

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a><span data-ttu-id="b000b-472">NuGet 程序包管理器</span><span class="sxs-lookup"><span data-stu-id="b000b-472">NuGet Package Manager</span></span>

<span data-ttu-id="b000b-473">ASP.NET MVC 3 包含 NuGet 包管理器 （以前称为 NuPack），这是将库和工具添加到 Visual Studio 项目的集成的包管理工具。</span><span class="sxs-lookup"><span data-stu-id="b000b-473">ASP.NET MVC 3 includes the NuGet Package Manager (formerly known as NuPack), which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="b000b-474">此工具自动执行开发人员立即采取来访问其源树的一个库的步骤。</span><span class="sxs-lookup"><span data-stu-id="b000b-474">This tool automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="b000b-475">你可以使用 NuGet，作为命令行工具，在 Visual Studio 2010 中，在 Visual Studio 上下文菜单中的集成的控制台窗口和一组 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b000b-475">You can work with NuGet as a command-line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as a set of PowerShell cmdlets.</span></span>

<span data-ttu-id="b000b-476">有关 NuGet 的详细信息，请阅读[Nuget 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="b000b-476">For more information about NuGet, read the [Nuget Documentation](https://docs.microsoft.com/nuget/).</span></span>

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a><span data-ttu-id="b000b-477">改进了"新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-477">Improved "New Project" Dialog Box</span></span>

<span data-ttu-id="b000b-478">当创建新项目时，新建项目对话框中现在允许你指定的视图引擎，以及 ASP.NET MVC 项目类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-478">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image5.png)

<span data-ttu-id="b000b-479">在此版本中包含对修改的模板和引擎列在对话框中的视图列表支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-479">Support for modifying the list of templates and view engines listed in the dialog box is included in this release.</span></span>

<span data-ttu-id="b000b-480">默认模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-480">The default templates are the following:</span></span>

<span data-ttu-id="b000b-481">为空。</span><span class="sxs-lookup"><span data-stu-id="b000b-481">Empty.</span></span> <span data-ttu-id="b000b-482">包含一组最小的 ASP.NET MVC 项目中，其中包括默认目录结构对于 ASP.NET MVC 项目，包含的默认 ASP.NET MVC 样式，并包含默认的 JavaScript 文件的脚本目录的 Site.css 文件的文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-482">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="b000b-483">Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-483">Internet Application.</span></span> <span data-ttu-id="b000b-484">包含演示如何使用 ASP.NET MVC 使用成员资格提供程序的示例功能。</span><span class="sxs-lookup"><span data-stu-id="b000b-484">Contains sample functionality that demonstrates how to use the membership provider with ASP.NET MVC.</span></span>

<span data-ttu-id="b000b-485">Windows 注册表中指定显示在对话框中的项目模板列表。</span><span class="sxs-lookup"><span data-stu-id="b000b-485">The list of project templates that is displayed in the dialog box is specified in the Windows registry.</span></span>

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a><span data-ttu-id="b000b-486">无会话控制器</span><span class="sxs-lookup"><span data-stu-id="b000b-486">Sessionless Controllers</span></span>

<span data-ttu-id="b000b-487">新*ControllerSessionStateAttribute*提供更好地控制会话状态行为控制器通过指定[System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx)枚举值。</span><span class="sxs-lookup"><span data-stu-id="b000b-487">The new *ControllerSessionStateAttribute* gives you more control over session-state behavior for controllers by specifying a [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) enumeration value.</span></span>

<span data-ttu-id="b000b-488">下面的示例演示如何关闭到控制器的所有请求的会话状态。</span><span class="sxs-lookup"><span data-stu-id="b000b-488">The following example shows how to turn off session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

<span data-ttu-id="b000b-489">下面的示例演示如何将所有请求的只读会话状态设置为一个控制器。</span><span class="sxs-lookup"><span data-stu-id="b000b-489">The following example shows how to set read-only session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a><span data-ttu-id="b000b-490">新的验证特性</span><span class="sxs-lookup"><span data-stu-id="b000b-490">New Validation Attributes</span></span>

#### <a name="compareattribute"></a><span data-ttu-id="b000b-491">CompareAttribute</span><span class="sxs-lookup"><span data-stu-id="b000b-491">CompareAttribute</span></span>

<span data-ttu-id="b000b-492">新*CompareAttribute*验证特性可用于比较两个不同模型的属性的值。</span><span class="sxs-lookup"><span data-stu-id="b000b-492">The new *CompareAttribute* validation attribute lets you compare the values of two different properties of a model.</span></span> <span data-ttu-id="b000b-493">在以下示例中， *ComparePassword*属性必须与匹配*密码*是有效的字段。</span><span class="sxs-lookup"><span data-stu-id="b000b-493">In the following example, the *ComparePassword* property must match the *Password* field in order to be valid.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a><span data-ttu-id="b000b-494">RemoteAttribute</span><span class="sxs-lookup"><span data-stu-id="b000b-494">RemoteAttribute</span></span>

<span data-ttu-id="b000b-495">新*RemoteAttribute*验证特性利用 jQuery 验证插件的远程验证程序，从而使客户端验证来执行实际验证逻辑的服务器上调用的方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-495">The new *RemoteAttribute* validation attribute takes advantage of the jQuery Validation plug-in's remote validator, which enables client-side validation to call a method on the server that performs the actual validation logic.</span></span>

<span data-ttu-id="b000b-496">在以下示例中，*用户名*属性具有*RemoteAttribute*应用。</span><span class="sxs-lookup"><span data-stu-id="b000b-496">In the following example, the *UserName* property has the *RemoteAttribute* applied.</span></span> <span data-ttu-id="b000b-497">客户端验证时编辑此属性在编辑视图中的，将调用名为操作*UserNameAvailable*上*UsersController*以验证此字段的类。</span><span class="sxs-lookup"><span data-stu-id="b000b-497">When editing this property in an Edit view, client validation will call an action named *UserNameAvailable* on the *UsersController* class in order to validate this field.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

<span data-ttu-id="b000b-498">下面的示例显示了相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="b000b-498">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

<span data-ttu-id="b000b-499">默认情况下，该特性应用于的属性名称是作为查询字符串参数发送到操作方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-499">By default, the property name that the attribute is applied to is sent to the action method as a query-string parameter.</span></span>

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a><span data-ttu-id="b000b-500">有关"LabelFor"和"LabelForModel"方法的新重载</span><span class="sxs-lookup"><span data-stu-id="b000b-500">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>

<span data-ttu-id="b000b-501">已添加的新重载*LabelFor*并*LabelForModel*方法，可指定标签文本。</span><span class="sxs-lookup"><span data-stu-id="b000b-501">New overloads have been added for the *LabelFor* and *LabelForModel* methods that let you specify the label text.</span></span> <span data-ttu-id="b000b-502">下面的示例演示如何使用这些重载。</span><span class="sxs-lookup"><span data-stu-id="b000b-502">The following example shows how to use these overloads.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a><span data-ttu-id="b000b-503">子操作输出缓存</span><span class="sxs-lookup"><span data-stu-id="b000b-503">Child Action Output Caching</span></span>

<span data-ttu-id="b000b-504">*OutputCacheAttribute*支持通过使用调用子操作的输出缓存*Html.RenderAction*或*Html.Action*帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-504">The *OutputCacheAttribute* supports output caching of child actions that are called by using the *Html.RenderAction* or *Html.Action* helper methods.</span></span> <span data-ttu-id="b000b-505">下面的示例演示一个视图，它调用另一个操作。</span><span class="sxs-lookup"><span data-stu-id="b000b-505">The following example shows a view that calls another action.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

<span data-ttu-id="b000b-506">*GetDate*操作将批注*OutputCacheAttribute*:</span><span class="sxs-lookup"><span data-stu-id="b000b-506">The *GetDate* action is annotated with the *OutputCacheAttribute*:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

<span data-ttu-id="b000b-507">此代码运行时，100 秒缓存到 Html.Action("GetDate") 调用的结果。</span><span class="sxs-lookup"><span data-stu-id="b000b-507">When this code runs, the result of the call to Html.Action("GetDate") is cached for 100 seconds.</span></span>

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a><span data-ttu-id="b000b-508">"添加视图"对话框框中改进</span><span class="sxs-lookup"><span data-stu-id="b000b-508">"Add View" Dialog Box Improvements</span></span>

<span data-ttu-id="b000b-509">当添加强类型化的视图时，添加视图对话框中现在筛选出比早期版本中，例如，许多核心.NET Framework 类型中的多个不适用的类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-509">When you add a strongly typed view, the Add View dialog box now filters out more non-applicable types than in previous releases, such as many core .NET Framework types.</span></span> <span data-ttu-id="b000b-510">此外，现在排序列表，按类名而不是由完全限定的类型名称，因此可以轻松地查找类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-510">Also, the list is now sorted by the class name and not by the fully qualified type name, which makes it easier to find types.</span></span> <span data-ttu-id="b000b-511">例如，类型名称现在显示如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-511">For example, the type name is now displayed as in the following example:</span></span>

<span data-ttu-id="b000b-512">类名 （命名空间）</span><span class="sxs-lookup"><span data-stu-id="b000b-512">ClassName (namespace)</span></span>

<span data-ttu-id="b000b-513">在早期版本中，这将显示如下所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-513">In earlier releases, this would have been displayed as the following:</span></span>

<span data-ttu-id="b000b-514">Namespace.ClassName</span><span class="sxs-lookup"><span data-stu-id="b000b-514">Namespace.ClassName</span></span>

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a><span data-ttu-id="b000b-515">粒度请求验证</span><span class="sxs-lookup"><span data-stu-id="b000b-515">Granular Request Validation</span></span>

<span data-ttu-id="b000b-516">*排除*的属性*ValidateInputAttribute*不再存在。</span><span class="sxs-lookup"><span data-stu-id="b000b-516">The *Exclude* property of *ValidateInputAttribute* no longer exists.</span></span> <span data-ttu-id="b000b-517">相反，如果希望在模型绑定期间跳过的模型的特定属性的请求验证，请使用新*SkipRequestValidationAttribute*。</span><span class="sxs-lookup"><span data-stu-id="b000b-517">Instead, to have request validation skipped for specific properties of a model during model binding, use the new *SkipRequestValidationAttribute*.</span></span>

<span data-ttu-id="b000b-518">例如，假设操作方法用来编辑一篇博客文章：</span><span class="sxs-lookup"><span data-stu-id="b000b-518">For example, suppose an action method is used to edit a blog post:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

<span data-ttu-id="b000b-519">下面的示例显示了一篇博客文章的视图模型。</span><span class="sxs-lookup"><span data-stu-id="b000b-519">The following example shows the view model for a blog post.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

<span data-ttu-id="b000b-520">当用户提交的 Description 属性一些标记时，模型绑定将由于请求验证将失败。</span><span class="sxs-lookup"><span data-stu-id="b000b-520">When a user submits some markup for the Description property, model binding will fail due to request validation.</span></span> <span data-ttu-id="b000b-521">若要禁用请求验证在博客文章说明的模型绑定期间，应用*SkipRequpestValidationAttribute*到属性，如在此示例中所示:。</span><span class="sxs-lookup"><span data-stu-id="b000b-521">To disable request validation during model binding for the blog post Description, apply the *SkipRequpestValidationAttribute* to the property, as shown in this example:.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

<span data-ttu-id="b000b-522">或者，若要关闭该模型的每个属性的请求验证，请应用*ValidateInputAttribute*值为*false*到操作方法：</span><span class="sxs-lookup"><span data-stu-id="b000b-522">Alternatively, to turn off request validation for every property of the model, apply *ValidateInputAttribute* with a value of *false* to the action method:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a><span data-ttu-id="b000b-523">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-523">Breaking Changes</span></span>

- <span data-ttu-id="b000b-524">异常筛选器的执行顺序已更改的异常筛选器具有相同*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-524">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="b000b-525">在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的控制器上*顺序*如操作方法上的异常筛选器之前执行这些操作方法上。</span><span class="sxs-lookup"><span data-stu-id="b000b-525">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="b000b-526">异常筛选器应用时，这通常会发生此情况没有指定*顺序*值。</span><span class="sxs-lookup"><span data-stu-id="b000b-526">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="b000b-527">在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。</span><span class="sxs-lookup"><span data-stu-id="b000b-527">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="b000b-528">在早期版本中，如果*顺序*显式指定属性、 筛选器运行指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="b000b-528">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="b000b-529">添加名为的新属性*FileExtensions*到*VirtualPathProviderViewEngine*基类。</span><span class="sxs-lookup"><span data-stu-id="b000b-529">Added a new property named *FileExtensions* to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="b000b-530">查找视图的路径 （并不是按名称），仅具有文件扩展名中包含的视图时被视为指定此新属性的列表。</span><span class="sxs-lookup"><span data-stu-id="b000b-530">When looking up a view by path (and not by name), only views with a file extension contained in the list specified by this new property is considered.</span></span> <span data-ttu-id="b000b-531">这是一项重大更改的用户注册自定义生成提供程序以启用自定义的文件扩展名为 web 窗体视图和所使用的完整路径而不是一个名称来引用这些视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-531">This is a breaking change for those who register a custom build provider to enable a custom file extension for web form views and are referencing those views by using a full path rather than a name.</span></span> <span data-ttu-id="b000b-532">解决方法是修改的值*FileExtensions*属性以包含自定义的文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-532">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>

<a id="_Toc276711795"></a>
## <a name="known-issues"></a><span data-ttu-id="b000b-533">已知问题</span><span class="sxs-lookup"><span data-stu-id="b000b-533">Known Issues</span></span>

- <span data-ttu-id="b000b-534">安装程序可能需要更长的时间比以前版本的 ASP.NET MVC，才能完成，因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-534">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="b000b-535">添加视图基架时选择 astrongly 类型化视图的基架只写属性。</span><span class="sxs-lookup"><span data-stu-id="b000b-535">The Add View scaffolding when selecting astrongly typed view scaffolds write-only properties.</span></span> <span data-ttu-id="b000b-536">始终通过搭建基架会忽略这些。</span><span class="sxs-lookup"><span data-stu-id="b000b-536">These should always be ignored by scaffolding.</span></span> <span data-ttu-id="b000b-537">添加视图对话框还搭建基架以只读属性时生成的"编辑"创建"视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-537">The Add View dialog also scaffolds read-only properties when generating an "Edit" or "Create" view.</span></span> <span data-ttu-id="b000b-538">仅只读属性显示和列表视图的基架。</span><span class="sxs-lookup"><span data-stu-id="b000b-538">Read-only properties should only be scaffolded for the Display and List views.</span></span>
- <span data-ttu-id="b000b-539">与异步 ctp 版本一起安装 ASP.NET MVC 3 时，调试不起作用。</span><span class="sxs-lookup"><span data-stu-id="b000b-539">Debugging doesn't work when ASP.NET MVC 3 is installed alongside the Async CTP.</span></span> <span data-ttu-id="b000b-540">ASP.NET MVC 3 不能与 Async ctp 版本并行安装。</span><span class="sxs-lookup"><span data-stu-id="b000b-540">ASP.NET MVC 3 cannot be installed side-by-side with the Async CTP.</span></span> <span data-ttu-id="b000b-541">卸载 Async CTP 修复调试。</span><span class="sxs-lookup"><span data-stu-id="b000b-541">Uninstall the Async CTP to repair debugging.</span></span> <span data-ttu-id="b000b-542">有关更多详细信息，请阅读[这篇博客文章](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html)有关卸载的 ASP.NET MVC 3 RC 的所有部分。</span><span class="sxs-lookup"><span data-stu-id="b000b-542">For more details, read [this blog post](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) about uninstalling all the pieces of ASP.NET MVC 3 RC.</span></span>
- <span data-ttu-id="b000b-543">在安装 Resharper 时，则 razor Intellisense 无效。</span><span class="sxs-lookup"><span data-stu-id="b000b-543">Razor Intellisense does not work when Resharper is installed.</span></span> <span data-ttu-id="b000b-544">如果安装了 ReSharper 并且想要利用 Razor intellisense 支持在 ASP.NET MVC 3 RC，请阅读[这篇博客文章](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/)来自 JetBrains 其中讨论了如何立即使用它们在一起。</span><span class="sxs-lookup"><span data-stu-id="b000b-544">If you have ReSharper installed and want to take advantage of the Razor intellisense support in ASP.NET MVC 3 RC, please read [this blog post](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) from JetBrains which discusses ways to use them together today.</span></span>
- <span data-ttu-id="b000b-545">使用 ASP.NET MVC 3 的 Beta 创建的 CSHTML 和 VBHTML 视图没有这些文件的生成操作正确它从发布中省略它们。</span><span class="sxs-lookup"><span data-stu-id="b000b-545">CSHTML and VBHTML views created with Beta of ASP.NET MVC 3 do not have their build action correctly which omits them from publishing.</span></span> <span data-ttu-id="b000b-546">*生成操作*这些文件应设置为"内容"。</span><span class="sxs-lookup"><span data-stu-id="b000b-546">The *Build Action* for these files should be set to "Content".</span></span> <span data-ttu-id="b000b-547">ASP.NET MVC 3 RC 解决了新文件，此问题，但不会更正对现有文件或使用测试版创建的项目的设置。</span><span class="sxs-lookup"><span data-stu-id="b000b-547">ASP.NET MVC 3 RC fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta.</span></span>
- <span data-ttu-id="b000b-548">安装程序可能需要更长的时间比以前版本的 ASP.NET MVC，才能完成，因为它会更新 Visual Studio 2010 的组件。</span><span class="sxs-lookup"><span data-stu-id="b000b-548">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="b000b-549">添加视图基架时选择"编辑"强类型化视图的基架只读属性。</span><span class="sxs-lookup"><span data-stu-id="b000b-549">The Add View scaffolding when selecting an "Edit" strongly typed view scaffolds read only properties.</span></span> <span data-ttu-id="b000b-550">同样，只写属性都已搭建基架"Display"视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-550">Likewise, write-only properties are scaffolded for "Display" views.</span></span>
- <span data-ttu-id="b000b-551">在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。</span><span class="sxs-lookup"><span data-stu-id="b000b-551">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="b000b-552">安装 Visual Studio Async CTP 包含工具安装 ASP.NET MVC 3 Razor 版本将导致冲突。</span><span class="sxs-lookup"><span data-stu-id="b000b-552">Installing the Visual Studio Async CTP causes a conflict with the Razor release that is included as part of the ASP.NET MVC 3 tooling installation.</span></span> <span data-ttu-id="b000b-553">请确保不尝试在同一台计算机上安装 Visual Studio Async CTP 和 Razor 版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-553">Make sure that you do not try to install both the Visual Studio Async CTP and the Razor release on the same machine.</span></span>
- <span data-ttu-id="b000b-554">编辑 Razor 视图 （.cshtml 文件），Visual Studio 中的转到控制器菜单项将不可用，并且不有任何代码段。</span><span class="sxs-lookup"><span data-stu-id="b000b-554">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a><span data-ttu-id="b000b-555">ASP.NET MVC 3 Beta</span><span class="sxs-lookup"><span data-stu-id="b000b-555">ASP.NET MVC 3 Beta</span></span>

<span data-ttu-id="b000b-556">ASP.NET MVC 3 试用版已于 2010 年 10 月 6 日发布。</span><span class="sxs-lookup"><span data-stu-id="b000b-556">ASP.NET MVC 3 Beta was released on October 6, 2010.</span></span> <span data-ttu-id="b000b-557">以下说明仅适用于 Beta 版，并受到任何更新或更高版本的 ASP.NET MVC 3 Release Candidate 部分中引用的更改。</span><span class="sxs-lookup"><span data-stu-id="b000b-557">The following notes are specific to the Beta release, and are subject to any updates or changes referenced in the ASP.NET MVC 3 Release Candidate section above.</span></span>

## <a id="0.1__Toc274034215"></a>  <span data-ttu-id="b000b-558">新 Featuresin ASP.NET MVC 3 的 beta 版本</span><span class="sxs-lookup"><span data-stu-id="b000b-558">New Featuresin ASP.NET MVC 3 Beta</span></span>

<a id="0.1__Default_validation_system"></a><span data-ttu-id="b000b-559">本部分介绍已引入的功能在 ASP.NET MVC 3 Beta 版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-559">This section describes features that have been introduced in the ASP.NET MVC 3 Beta release.</span></span>

### <a id="0.1__Toc274034216"></a>  <span data-ttu-id="b000b-560">NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="b000b-560">NuGet Package Manager</span></span>

<span data-ttu-id="b000b-561">ASP.NET MVC 3 包含 NuGet 包管理器，这是添加的库的集成的包管理工具和 Visual Studio 项目的工具。</span><span class="sxs-lookup"><span data-stu-id="b000b-561">ASP.NET MVC 3 includes NuGet Package Manager, which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="b000b-562">大多数情况下，它自动执行开发人员立即采取来访问其源树的一个库的步骤。</span><span class="sxs-lookup"><span data-stu-id="b000b-562">For the most part, it automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="b000b-563">你可以使用 NuGet，作为命令行工具，在 Visual Studio 2010 中，在 Visual Studio 上下文菜单中的集成的控制台窗口和组的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b000b-563">You can work with NuGet as a command line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as set of PowerShell cmdlets.</span></span>

<span data-ttu-id="b000b-564">有关 NuGet 的详细信息，请阅读[NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="b000b-564">For more information about NuGet, read the [NuGet Documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a id="0.1__Toc274034217"></a>  <span data-ttu-id="b000b-565">改进了新建项目对话框</span><span class="sxs-lookup"><span data-stu-id="b000b-565">Improved New Project Dialog Box</span></span>

<span data-ttu-id="b000b-566">当创建新项目时，新建项目对话框中现在允许你指定的视图引擎，以及 ASP.NET MVC 项目类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-566">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image6.png)

<span data-ttu-id="b000b-567">在此版本中不包含对修改的模板和引擎列在对话框中的视图列表支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-567">Support for modifying the list of templates and view engines listed in the dialog box is not included in this release.</span></span>

<span data-ttu-id="b000b-568">默认模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-568">The default templates are the following:</span></span>

<span data-ttu-id="b000b-569">为空。</span><span class="sxs-lookup"><span data-stu-id="b000b-569">Empty.</span></span> <span data-ttu-id="b000b-570">包含一组最小的 ASP.NET MVC 项目中，其中包括默认目录结构对于 ASP.NET MVC 项目，包含的默认 ASP.NET MVC 样式，并包含默认的 JavaScript 文件的脚本目录的小 Site.css 文件的文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-570">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a small Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="b000b-571">Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-571">Internet Application.</span></span> <span data-ttu-id="b000b-572">包含演示如何使用 ASP.NET MVC 中的成员资格提供程序的示例功能。</span><span class="sxs-lookup"><span data-stu-id="b000b-572">Contains sample functionality that demonstrates how to use the membership provider within ASP.NET MVC.</span></span>

### <a id="0.1__Toc274034218"></a>  <span data-ttu-id="b000b-573">简化的方法来指定强类型模型在 Razor 视图中</span><span class="sxs-lookup"><span data-stu-id="b000b-573">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>

<span data-ttu-id="b000b-574">指定强类型化的 Razor 视图的模型类型的方法已经使用新的进行了简化@model指令的 CSHTML 视图和@ModelTypeVBHTML 视图的指令。</span><span class="sxs-lookup"><span data-stu-id="b000b-574">The way to specify the model type for strongly typed Razor views has been simplified by using the new @model directive for CSHTML views and @ModelType directive for VBHTML views.</span></span> <span data-ttu-id="b000b-575">在早期版本的 ASP.NET MVC 中，则会指定一个强类型化的模型，Razor 视图这种方式：</span><span class="sxs-lookup"><span data-stu-id="b000b-575">In earlier versions of ASP.NET MVC, you would specify a strongly typed model for Razor views this way:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

<span data-ttu-id="b000b-576">在此版本中，可以使用以下语法：</span><span class="sxs-lookup"><span data-stu-id="b000b-576">In this release, you can use the following syntax:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>  <span data-ttu-id="b000b-577">支持新的 ASP.NET Web 页的帮助器方法</span><span class="sxs-lookup"><span data-stu-id="b000b-577">Support for New ASP.NET Web Pages Helper Methods</span></span>

<span data-ttu-id="b000b-578">新的 ASP.NET Web Pages 技术包括一组可用于将常用的功能添加到视图和控制器的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-578">The new ASP.NET Web Pages technology includes a set of helper methods that are useful for adding commonly used functionality to views and controllers.</span></span> <span data-ttu-id="b000b-579">ASP.NET MVC 3 支持使用控制器和视图中的这些帮助器方法 （如果适用）。</span><span class="sxs-lookup"><span data-stu-id="b000b-579">ASP.NET MVC 3 supports using these helper methods within controllers and views (where appropriate).</span></span> <span data-ttu-id="b000b-580">这些方法包含在 System.Web.Helpers 程序集。</span><span class="sxs-lookup"><span data-stu-id="b000b-580">These methods are contained in the System.Web.Helpers assembly.</span></span> <span data-ttu-id="b000b-581">下表列出了几个 ASP.NET Web Pages 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-581">The following table lists a few of the ASP.NET Web Pages helper methods.</span></span>

| <span data-ttu-id="b000b-582">**帮助程序**</span><span class="sxs-lookup"><span data-stu-id="b000b-582">**Helper**</span></span> | <span data-ttu-id="b000b-583">**说明**</span><span class="sxs-lookup"><span data-stu-id="b000b-583">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b000b-584">Chart</span><span class="sxs-lookup"><span data-stu-id="b000b-584">Chart</span></span> | <span data-ttu-id="b000b-585">呈现的图表视图中。</span><span class="sxs-lookup"><span data-stu-id="b000b-585">Renders a chart within a view.</span></span> <span data-ttu-id="b000b-586">包含如 Chart.ToWebImage、 Chart.Save 和 Chart.Write 方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-586">Contains methods such as Chart.ToWebImage, Chart.Save, and Chart.Write.</span></span> |
| <span data-ttu-id="b000b-587">加密</span><span class="sxs-lookup"><span data-stu-id="b000b-587">Crypto</span></span> | <span data-ttu-id="b000b-588">使用哈希算法来创建正确加盐，哈希处理密码。</span><span class="sxs-lookup"><span data-stu-id="b000b-588">Uses hashing algorithms to create properly salted and hashed passwords.</span></span> |
| <span data-ttu-id="b000b-589">WebGrid</span><span class="sxs-lookup"><span data-stu-id="b000b-589">WebGrid</span></span> | <span data-ttu-id="b000b-590">为网格中呈现的对象 （通常情况下，数据库中的数据） 的集合。</span><span class="sxs-lookup"><span data-stu-id="b000b-590">Renders a collection of objects (typically, data from a database) as a grid.</span></span> <span data-ttu-id="b000b-591">分页和排序的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-591">Supports paging and sorting.</span></span> |
| <span data-ttu-id="b000b-592">WebImage</span><span class="sxs-lookup"><span data-stu-id="b000b-592">WebImage</span></span> | <span data-ttu-id="b000b-593">呈现图像。</span><span class="sxs-lookup"><span data-stu-id="b000b-593">Renders an image.</span></span> |
| <span data-ttu-id="b000b-594">WebMail</span><span class="sxs-lookup"><span data-stu-id="b000b-594">WebMail</span></span> | <span data-ttu-id="b000b-595">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="b000b-595">Sends an email message.</span></span> |

<span data-ttu-id="b000b-596">可用的快速参考主题列出了帮助程序和基本语法是 ASP.NET Razor 语法文档位于以下 URL 的一部分：</span><span class="sxs-lookup"><span data-stu-id="b000b-596">A quick reference topic that lists the helpers and basic syntax is available as part of the ASP.NET Razor syntax documentation at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>  <span data-ttu-id="b000b-597">其他依赖项注入支持</span><span class="sxs-lookup"><span data-stu-id="b000b-597">Additional Dependency Injection Support</span></span>

<span data-ttu-id="b000b-598">当前版本的 ASP.NET MVC 3 Preview 1 版本上构建，包括添加了的对两个新服务和四个现有的服务，以及对依赖项解析和公共服务定位器的改进的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-598">Building on the ASP.NET MVC 3 Preview 1 release, the current release includes added support for two new services and four existing services, and improved support for dependency resolution and the Common Service Locator.</span></span>

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a><span data-ttu-id="b000b-599">细粒度的控制器实例化新 IControllerActivator 接口</span><span class="sxs-lookup"><span data-stu-id="b000b-599">New IControllerActivator Interface for Fine-Grained Controller Instantiation</span></span>

<span data-ttu-id="b000b-600">新的 IControllerActivator 接口提供了如何通过依赖关系注入实例化控制器的更精细地控制。</span><span class="sxs-lookup"><span data-stu-id="b000b-600">The new IControllerActivator interface provides more fine-grained control over how controllers are instantiated via dependency injection.</span></span> <span data-ttu-id="b000b-601">以下示例演示的接口：</span><span class="sxs-lookup"><span data-stu-id="b000b-601">The following example shows the interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

<span data-ttu-id="b000b-602">相反的角色的控制器工厂。</span><span class="sxs-lookup"><span data-stu-id="b000b-602">Contrast this to the role of the controller factory.</span></span> <span data-ttu-id="b000b-603">控制器工厂是实现 IControllerFactory 接口，从而负责查找控制器类型并实例化该控制器类型的实例。</span><span class="sxs-lookup"><span data-stu-id="b000b-603">A controller factory is an implementation of the IControllerFactory interface, which is responsible both for locating a controller type and for instantiating an instance of that controller type.</span></span>

<span data-ttu-id="b000b-604">控制器激活器仅负责实例化控制器类型的实例。</span><span class="sxs-lookup"><span data-stu-id="b000b-604">Controller activators are responsible only for instantiating an instance of a controller type.</span></span> <span data-ttu-id="b000b-605">它们不会执行控制器类型查找。</span><span class="sxs-lookup"><span data-stu-id="b000b-605">They do not perform the controller type lookup.</span></span> <span data-ttu-id="b000b-606">找到后正确的控制器类型，控制器工厂应委托到 IControllerActivator 实例来处理控制器的实际实例化。</span><span class="sxs-lookup"><span data-stu-id="b000b-606">After locating a proper controller type, controller factories should delegate to an instance of IControllerActivator to handle the actual instantiation of the controller.</span></span>

<span data-ttu-id="b000b-607">借助于 DefaultControllerFactory 类具有新的构造函数接受 IControllerFactory 实例。</span><span class="sxs-lookup"><span data-stu-id="b000b-607">The DefaultControllerFactory class has a new constructor that accepts an IControllerFactory instance.</span></span> <span data-ttu-id="b000b-608">这可将应用依赖关系注入，若要管理的控制器创建的这个方面，而无需重写默认控制器类型查找行为。</span><span class="sxs-lookup"><span data-stu-id="b000b-608">This lets you apply Dependency Injection to manage this aspect of controller creation without having to override the default controller-type lookup behavior.</span></span>

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a><span data-ttu-id="b000b-609">替换为 IDependencyResolver IServiceLocator 接口</span><span class="sxs-lookup"><span data-stu-id="b000b-609">IServiceLocator Interface Replaced with IDependencyResolver</span></span>

<span data-ttu-id="b000b-610">根据社区反馈，ASP.NET MVC 3 Beta 版本已替换 IServiceLocator 接口使用特定于 ASP.NET MVC 的需求的简化的 IDependencyResolver 接口。</span><span class="sxs-lookup"><span data-stu-id="b000b-610">Based on community feedback, the ASP.NET MVC 3 Beta release has replaced the use of the IServiceLocator interface with a slimmed-down IDependencyResolver interface specific to the needs of ASP.NET MVC.</span></span> <span data-ttu-id="b000b-611">下面的示例演示新界面：</span><span class="sxs-lookup"><span data-stu-id="b000b-611">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

<span data-ttu-id="b000b-612">作为此更改的一部分，ServiceLocator 类还使用 DependencyResolver 类取代。</span><span class="sxs-lookup"><span data-stu-id="b000b-612">As part of this change, the ServiceLocator class was also replaced with the DependencyResolver class.</span></span> <span data-ttu-id="b000b-613">注册的依赖关系解析程序是类似于早期版本的 ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="b000b-613">Registration of a dependency resolver is similar to earlier versions of ASP.NET MVC:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

<span data-ttu-id="b000b-614">此接口的实现应只需委托基础依赖关系注入容器提供已注册的服务请求的类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-614">Implementations of this interface should simply delegate to the underlying dependency injection container to provide the registered service for the requested type.</span></span>

<span data-ttu-id="b000b-615">当不没有所请求类型的任何已注册的服务时，ASP.NET MVC 期望从 GetService 返回 null 并返回一个空集合从 getservices 进行提取此接口的实现。</span><span class="sxs-lookup"><span data-stu-id="b000b-615">When there are no registered services of the requested type, ASP.NET MVC expects implementations of this interface to return null from GetService and to return an empty collection from GetServices.</span></span>

<span data-ttu-id="b000b-616">新 DependencyResolver 类，可以注册新的 IDependencyResolver 接口或公共服务定位器接口 (IServiceLocator) 实现的类。</span><span class="sxs-lookup"><span data-stu-id="b000b-616">The new DependencyResolver class lets you register classes that implement either the new IDependencyResolver interface or the Common Service Locator interface (IServiceLocator).</span></span> <span data-ttu-id="b000b-617">有关公共服务定位器的详细信息，请参阅[CommonServiceLocator GitHub 上的](https://github.com/unitycontainer/commonservicelocator)。</span><span class="sxs-lookup"><span data-stu-id="b000b-617">For more information about Common Service Locator, see [CommonServiceLocator on GitHub](https://github.com/unitycontainer/commonservicelocator).</span></span>

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a><span data-ttu-id="b000b-618">细粒度视图页实例化新 IViewActivator 接口</span><span class="sxs-lookup"><span data-stu-id="b000b-618">New IViewActivator Interface for Fine-Grained View Page Instantiation</span></span>

<span data-ttu-id="b000b-619">新的 IViewPageActivator 接口提供了更加精细地控制如何通过依赖关系注入实例化视图页。</span><span class="sxs-lookup"><span data-stu-id="b000b-619">The new IViewPageActivator interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="b000b-620">这适用于 WebFormView 实例和 RazorView 实例。</span><span class="sxs-lookup"><span data-stu-id="b000b-620">This applies to both WebFormView instances and RazorView instances.</span></span> <span data-ttu-id="b000b-621">下面的示例演示新界面：</span><span class="sxs-lookup"><span data-stu-id="b000b-621">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

<span data-ttu-id="b000b-622">这些类现在接受 IViewPageActivator 构造函数参数，它允许你使用依赖关系注入来控制如何实例化的 ViewPage、 ViewUserControl 和 WebViewPage 类型。</span><span class="sxs-lookup"><span data-stu-id="b000b-622">These classes now accept an IViewPageActivator constructor argument, which lets you use dependency injection to control how the ViewPage, ViewUserControl, and WebViewPage types are instantiated.</span></span>

#### <a name="new-dependency-resolver-support-for-existing-services"></a><span data-ttu-id="b000b-623">新的依赖关系解析程序支持的现有服务</span><span class="sxs-lookup"><span data-stu-id="b000b-623">New Dependency Resolver Support for Existing Services</span></span>

<span data-ttu-id="b000b-624">新版本包括对以下服务的依赖关系解析支持：</span><span class="sxs-lookup"><span data-stu-id="b000b-624">The new release includes dependency resolution support for the following services:</span></span>

- <span data-ttu-id="b000b-625">模型验证程序提供程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-625">Model validation providers.</span></span> <span data-ttu-id="b000b-626">实现 ModelValidatorProvider 的类可以注册在依赖关系解析程序，并且系统将使用它们来支持客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="b000b-626">Classes that implement ModelValidatorProvider can be registered in the dependency resolver, and the system will use them to support client- and server-side validation.</span></span>
- <span data-ttu-id="b000b-627">模型元数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-627">Model metadata provider.</span></span> <span data-ttu-id="b000b-628">可以在依赖关系解析程序中, 注册的单个类，实现 ModelMetadataProvider 和系统将使用它提供的模板化和验证系统元数据。</span><span class="sxs-lookup"><span data-stu-id="b000b-628">A single class that implements ModelMetadataProvider can be registered in the dependency resolver, and the system will use it to provide metadata for the templating and validation systems.</span></span>
- <span data-ttu-id="b000b-629">值提供程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-629">Value providers.</span></span> <span data-ttu-id="b000b-630">实现 ValueProviderFactory 的类可以注册在依赖关系解析程序，并在系统将使用它们创建控制器和模型绑定期间使用的值提供程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-630">Classes that implement ValueProviderFactory can be registered in the dependency resolver, and the system will use them to create value providers that are consumed by the controller and during model binding.</span></span>
- <span data-ttu-id="b000b-631">模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-631">Model binders.</span></span> <span data-ttu-id="b000b-632">实现 IModelBinderProvider 的类可以注册在依赖关系解析程序，并在系统将使用它们创建模型绑定系统使用的模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="b000b-632">Classes that implement IModelBinderProvider can be registered in the dependency resolver, and the system will use them to create model binders that are consumed by the model binding system.</span></span>

### <a id="0.1__Toc274034221"></a>  <span data-ttu-id="b000b-633">新的非介入式 jQuery 基于 Ajax 的支持</span><span class="sxs-lookup"><span data-stu-id="b000b-633">New Support for Unobtrusive jQuery-Based Ajax</span></span>

<span data-ttu-id="b000b-634">ASP.NET MVC 包括 Ajax 帮助器方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-634">ASP.NET MVC includes Ajax helper methods such as the following:</span></span>

- <span data-ttu-id="b000b-635">Ajax.ActionLink</span><span class="sxs-lookup"><span data-stu-id="b000b-635">Ajax.ActionLink</span></span>
- <span data-ttu-id="b000b-636">Ajax.RouteLink</span><span class="sxs-lookup"><span data-stu-id="b000b-636">Ajax.RouteLink</span></span>
- <span data-ttu-id="b000b-637">Ajax.BeginForm</span><span class="sxs-lookup"><span data-stu-id="b000b-637">Ajax.BeginForm</span></span>
- <span data-ttu-id="b000b-638">Ajax.BeginRouteForm</span><span class="sxs-lookup"><span data-stu-id="b000b-638">Ajax.BeginRouteForm</span></span>

<span data-ttu-id="b000b-639">这些方法使用 JavaScript 来调用服务器，而无需使用完全回发操作方法。</span><span class="sxs-lookup"><span data-stu-id="b000b-639">These methods use JavaScript to invoke an action method on the server rather than using a full postback.</span></span> <span data-ttu-id="b000b-640">已更新此功能才能利用 jQuery 非介入式的方式。</span><span class="sxs-lookup"><span data-stu-id="b000b-640">This functionality has been updated to take advantage of jQuery in an unobtrusive manner.</span></span> <span data-ttu-id="b000b-641">而不是干扰的方式发出内联客户端脚本，这些帮助器方法分隔行为根据标记发出使用 HTML5 属性*数据 ajax*前缀。</span><span class="sxs-lookup"><span data-stu-id="b000b-641">Rather than intrusively emitting inline client scripts, these helper methods separate the behavior from the markup by emitting HTML5 attributes using the *data-ajax* prefix.</span></span> <span data-ttu-id="b000b-642">然后将行为应用于标记通过引用适当的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-642">Behavior is then applied to the markup by referencing the appropriate JavaScript files.</span></span> <span data-ttu-id="b000b-643">请确保引用以下 JavaScript 文件：</span><span class="sxs-lookup"><span data-stu-id="b000b-643">Make sure that the following JavaScript files are referenced:</span></span>

- <span data-ttu-id="b000b-644">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="b000b-644">jquery-1.4.1.js</span></span>
- <span data-ttu-id="b000b-645">jquery.unobtrusive.ajax.js</span><span class="sxs-lookup"><span data-stu-id="b000b-645">jquery.unobtrusive.ajax.js</span></span>

<span data-ttu-id="b000b-646">此功能的 Web.config 文件中的 ASP.NET MVC 3 新建项目模板，默认情况下启用，但默认情况下，对于现有项目处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="b000b-646">This feature is enabled by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="b000b-647">有关详细信息，请参阅[添加的客户端验证和非介入式 JavaScript 的应用程序范围内标志](#0.1_AddedApplicationWideFlagsForClientValida)本文档中更高版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-647">For more information, see [Added application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

### <a id="0.1__Toc274034222"></a>  <span data-ttu-id="b000b-648">对于非介入式 jQuery 验证新的支持</span><span class="sxs-lookup"><span data-stu-id="b000b-648">New Support for Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="b000b-649">默认情况下，ASP.NET MVC 3 Beta 使用 jQuery 验证，以非介入式方式以便执行客户端验证。</span><span class="sxs-lookup"><span data-stu-id="b000b-649">By default, ASP.NET MVC 3 Beta uses jQuery validation in an unobtrusive manner in order to perform client-side validation.</span></span> <span data-ttu-id="b000b-650">若要启用非介入式客户端验证，请如下从视图中所示的调用：</span><span class="sxs-lookup"><span data-stu-id="b000b-650">To enable unobtrusive client validation, make a call like the following from within a view:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

<span data-ttu-id="b000b-651">这需要 ViewContext.UnobtrusiveJavaScriptEnabled 属性设置为 true 时，您可以通过进行以下调用来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="b000b-651">This requires that ViewContext.UnobtrusiveJavaScriptEnabled property is set to true, which you can do by making the following call:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

<span data-ttu-id="b000b-652">此外请确保引用的以下 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-652">Also make sure the following JavaScript files are referenced.</span></span>

- <span data-ttu-id="b000b-653">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="b000b-653">jquery-1.4.1.js</span></span>
- <span data-ttu-id="b000b-654">jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="b000b-654">jquery.validate.js</span></span>
- <span data-ttu-id="b000b-655">jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="b000b-655">jquery.validate.unobtrusive.js</span></span>

<span data-ttu-id="b000b-656">此功能上的 Web.config 文件中的 ASP.NET MVC 3 新建项目模板，默认情况下启用，但默认情况下，对于现有项目处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="b000b-656">This feature is enabled on by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="b000b-657">有关详细信息，请参阅[客户端验证和非介入式 JavaScript 的新应用程序范围内标志](#0.1_AddedApplicationWideFlagsForClientValida)本文档中更高版本。</span><span class="sxs-lookup"><span data-stu-id="b000b-657">For more information, see [New application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>  <span data-ttu-id="b000b-658">客户端验证和非介入式 JavaScript 的新应用程序范围内标志</span><span class="sxs-lookup"><span data-stu-id="b000b-658">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>

<span data-ttu-id="b000b-659">您可以启用或禁用客户端验证和非介入式 JavaScript 全局使用 HtmlHelper 类，如以下示例所示的静态成员：</span><span class="sxs-lookup"><span data-stu-id="b000b-659">You can enable or disable client validation and unobtrusive JavaScript globally using static members of the HtmlHelper class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

<span data-ttu-id="b000b-660">默认项目模板默认启用非介入式 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="b000b-660">The default project templates enable unobtrusive JavaScript by default.</span></span> <span data-ttu-id="b000b-661">您还可以启用或禁用应用程序中使用以下设置的根 Web.config 文件中的这些功能：</span><span class="sxs-lookup"><span data-stu-id="b000b-661">You can also enable or disable these features in the root Web.config file of your application using the following settings:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

<span data-ttu-id="b000b-662">默认情况下，可以启用这些功能，因为新重载引入到 HtmlHelper 类，允许您替代默认设置，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-662">Because you can enable these features by default, new overloads were introduced to the HtmlHelper class that let you override the default settings, as shown in the following examples:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

<span data-ttu-id="b000b-663">为了向后兼容，这两项功能默认情况下禁用。</span><span class="sxs-lookup"><span data-stu-id="b000b-663">For backward compatibility, both of these features are disabled by default.</span></span>

### <a id="0.1__Toc274034224"></a>  <span data-ttu-id="b000b-664">对视图运行前运行的代码的新支持</span><span class="sxs-lookup"><span data-stu-id="b000b-664">New Support for Code that Runs Before Views Run</span></span>

<span data-ttu-id="b000b-665">现在可以将名为的文件\_viewstart.cshtml (或\_viewstart.vbhtml) 中 Views 目录并将代码添加到它将在多个视图之间共享该目录及其子目录中。</span><span class="sxs-lookup"><span data-stu-id="b000b-665">You can now put a file named \_viewstart.cshtml (or \_viewstart.vbhtml) in the Views directory and add code to it that will be shared among multiple views in that directory and its subdirectories.</span></span> <span data-ttu-id="b000b-666">例如，可能会将下面的代码插入\_viewstart.cshtml 页 ~/Views 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="b000b-666">For example, you might put the following code into the \_viewstart.cshtml page in the ~/Views folder:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

<span data-ttu-id="b000b-667">这会设置布局页的视图文件夹中的每个视图和所有其子文件夹以递归方式。</span><span class="sxs-lookup"><span data-stu-id="b000b-667">This sets the layout page for every view within the Views folder and all its subfolders recursively.</span></span> <span data-ttu-id="b000b-668">视图正在呈现时中的代码\_viewstart.cshtml 文件运行之前查看代码运行。</span><span class="sxs-lookup"><span data-stu-id="b000b-668">When a view is being rendered, the code in the \_viewstart.cshtml file runs before the view code runs.</span></span> <span data-ttu-id="b000b-669">\_Viewstart.cshtml 代码适用于该文件夹中的每个视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-669">The \_viewstart.cshtml code applies to every view in that folder.</span></span>

<span data-ttu-id="b000b-670">默认情况下中的代码\_viewstart.cshtml 文件也适用于任何子文件夹中的视图。</span><span class="sxs-lookup"><span data-stu-id="b000b-670">By default, the code in the \_viewstart.cshtml file also applies to views in any subfolder.</span></span> <span data-ttu-id="b000b-671">但是，单个子文件夹可以具有其自己版本的\_viewstart.cshtml 文件;，因为的情况下，本地版本将优先。</span><span class="sxs-lookup"><span data-stu-id="b000b-671">However, individual subfolders can have their own version of the \_viewstart.cshtml file; in that case, the local version takes precedence.</span></span> <span data-ttu-id="b000b-672">例如，若要运行普遍适用于 HomeController 的所有视图的代码，将\_viewstart.cshtml ~/Views/Home 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="b000b-672">For example, to run code that is common to all views for the HomeController, put a \_viewstart.cshtml file in the ~/Views/Home folder.</span></span>

### <a id="0.1__Toc274034225"></a>  <span data-ttu-id="b000b-673">新的 VBHTML Razor 语法支持</span><span class="sxs-lookup"><span data-stu-id="b000b-673">New Support for the VBHTML Razor Syntax</span></span>

<span data-ttu-id="b000b-674">以前的 ASP.NET MVC 预览版包括对视图使用 Razor 语法基于 C# 的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-674">The previous ASP.NET MVC preview included support for views using Razor syntax based on C#.</span></span> <span data-ttu-id="b000b-675">这些视图使用.cshtml 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="b000b-675">These views use the .cshtml file extension.</span></span> <span data-ttu-id="b000b-676">作为正在进行的工作来支持 Razor 的一部分，ASP.NET MVC 3 Beta 引入了对在 Visual Basic 中使用的.vbhtml 文件扩展名的 Razor 语法的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-676">As part of ongoing work to support Razor, the ASP.NET MVC 3 Beta introduces support for the Razor syntax in Visual Basic, which uses the .vbhtml file extension.</span></span>

<span data-ttu-id="b000b-677">VBHTML 页中使用 Visual Basic 语法的说明，请参阅本教程在以下 URL:</span><span class="sxs-lookup"><span data-stu-id="b000b-677">For an introduction to using Visual Basic syntax in VBHTML pages, see the tutorial at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>  <span data-ttu-id="b000b-678">更精细地控制 ValidateInputAttribute</span><span class="sxs-lookup"><span data-stu-id="b000b-678">More Granular Control over ValidateInputAttribute</span></span>

<span data-ttu-id="b000b-679">ASP.NET MVC 具有始终包括 ValidateInputAttribute 类，该类调用核心 ASP.NET 请求验证基础结构以确保传入的请求不包含潜在的恶意输入。</span><span class="sxs-lookup"><span data-stu-id="b000b-679">ASP.NET MVC has always included the ValidateInputAttribute class, which invokes the core ASP.NET request validation infrastructure to make sure that the incoming request does not contain potentially malicious input.</span></span> <span data-ttu-id="b000b-680">默认情况下启用输入的验证。</span><span class="sxs-lookup"><span data-stu-id="b000b-680">By default, input validation is enabled.</span></span> <span data-ttu-id="b000b-681">则可以禁用请求验证使用 ValidateInputAttribute 属性，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-681">It is possible to disable request validation by using the ValidateInputAttribute attribute, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

<span data-ttu-id="b000b-682">但是，许多 web 应用程序有需要时剩余的字段不应允许 HTML，单个窗体字段。</span><span class="sxs-lookup"><span data-stu-id="b000b-682">However, many web applications have individual form fields that need to allow HTML, while the remaining fields should not.</span></span> <span data-ttu-id="b000b-683">ValidateInputAttribute 类现在允许您指定不应包含在请求验证的字段的列表。</span><span class="sxs-lookup"><span data-stu-id="b000b-683">The ValidateInputAttribute class now lets you specify a list of fields that should not be included in request validation.</span></span>

<span data-ttu-id="b000b-684">例如，如果你正在开发的博客引擎，您可能想要允许在正文和摘要字段中的标记。</span><span class="sxs-lookup"><span data-stu-id="b000b-684">For example, if you are developing a blog engine, you might want to allow markup in the Body and Summary fields.</span></span> <span data-ttu-id="b000b-685">这些字段可能由两个输入元素，每个都有属性名称 （"正文"和"摘要"） 对应一个 name 属性表示。</span><span class="sxs-lookup"><span data-stu-id="b000b-685">These fields might be represented by two input element, each with a name attribute corresponding to the property name ("Body" and "Summary").</span></span> <span data-ttu-id="b000b-686">若要禁用请求验证为这些字段，指定 （以逗号分隔） ValidateInput 类，如以下示例所示的 Exclude 属性中的名称：</span><span class="sxs-lookup"><span data-stu-id="b000b-686">To disable request validation for these fields only, specify the names (comma-separated) in the Exclude property of the ValidateInput class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>  <span data-ttu-id="b000b-687">帮助程序对于使用匿名对象指定的 HTML 特性名称将下划线转换为连字符</span><span class="sxs-lookup"><span data-stu-id="b000b-687">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>

<span data-ttu-id="b000b-688">帮助器方法，可以指定属性名称/值对使用匿名对象，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b000b-688">Helper methods let you specify attribute name/value pairs using an anonymous object, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

<span data-ttu-id="b000b-689">因为 ASP.NET 中的属性名称不能使用连字符，这种方法不允许您使用属性名称中的连字符。</span><span class="sxs-lookup"><span data-stu-id="b000b-689">This approach doesn't let you use hyphens in the attribute name, because a hyphen cannot be used for a property name in ASP.NET.</span></span> <span data-ttu-id="b000b-690">但是，连字符非常重要的自定义 HTML5 属性;例如，HTML5，使用"数据-"前缀。</span><span class="sxs-lookup"><span data-stu-id="b000b-690">However, hyphens are important for custom HTML5 attributes; for example, HTML5 uses the "data-" prefix.</span></span>

<span data-ttu-id="b000b-691">在此同时，下划线不能用于在 HTML 中，属性名称，但将属性名称中有效。</span><span class="sxs-lookup"><span data-stu-id="b000b-691">At the same time, underscores cannot be used for attribute names in HTML, but are valid within property names.</span></span> <span data-ttu-id="b000b-692">因此，如果指定使用的匿名对象的属性和属性名称中包含下划线、 帮助程序方法会将下划线转换为连字符。</span><span class="sxs-lookup"><span data-stu-id="b000b-692">Therefore, if you specify attributes using an anonymous object, and if the attribute names include an underscore,, helper methods will convert the underscores to hyphens.</span></span> <span data-ttu-id="b000b-693">例如，以下帮助器语法使用下划线：</span><span class="sxs-lookup"><span data-stu-id="b000b-693">For example, the following helper syntax uses an underscore:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

<span data-ttu-id="b000b-694">前面的示例将呈现以下标记帮助程序运行时：</span><span class="sxs-lookup"><span data-stu-id="b000b-694">The previous example renders the following markup when the helper runs:</span></span>

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>  <span data-ttu-id="b000b-695">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="b000b-695">Bug Fixes</span></span>

<span data-ttu-id="b000b-696">EditorFor 和 DisplayFor 模板帮助器的默认对象模板现在支持 DisplayAttribute.Order 属性中指定的顺序。</span><span class="sxs-lookup"><span data-stu-id="b000b-696">The default object template for the EditorFor and DisplayFor template helpers now supports the ordering specified in the DisplayAttribute.Order property.</span></span> <span data-ttu-id="b000b-697">（在早期版本中，顺序设置不是使用。）</span><span class="sxs-lookup"><span data-stu-id="b000b-697">(In previous versions, the Order setting was not used.)</span></span>

<span data-ttu-id="b000b-698">客户端验证现在支持已应用的验证特性的重写属性的验证。</span><span class="sxs-lookup"><span data-stu-id="b000b-698">Client validation now supports validation of overridden properties that have validation attributes applied.</span></span>

<span data-ttu-id="b000b-699">JsonValueProviderFactory 现在默认情况下注册。</span><span class="sxs-lookup"><span data-stu-id="b000b-699">JsonValueProviderFactory is now registered by default.</span></span>

## <a id="0.1__Toc274034229"></a>  <span data-ttu-id="b000b-700">重大更改</span><span class="sxs-lookup"><span data-stu-id="b000b-700">Breaking Changes</span></span>

<span data-ttu-id="b000b-701">异常筛选器的执行顺序已更改的异常筛选器具有相同的顺序值。</span><span class="sxs-lookup"><span data-stu-id="b000b-701">The order of execution for exception filters has changed for exception filters that have the same Order value.</span></span> <span data-ttu-id="b000b-702">在 ASP.NET MVC 2 及更早版本，异常筛选器具有相同的顺序在控制器上，如操作方法上的异常筛选器之前执行这些操作方法上。</span><span class="sxs-lookup"><span data-stu-id="b000b-702">In ASP.NET MVC 2 and earlier, exception filters on the controller with the same Order as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="b000b-703">异常筛选器应用而无需指定的顺序值时，这通常会发生此情况。</span><span class="sxs-lookup"><span data-stu-id="b000b-703">This would typically be the case when exception filters were applied without a specified Order value.</span></span> <span data-ttu-id="b000b-704">在 ASP.NET MVC 3 中，此顺序已反转，以便最具体的异常处理程序最先执行。</span><span class="sxs-lookup"><span data-stu-id="b000b-704">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="b000b-705">在早期版本中，如果显式指定 Order 属性，以指定顺序运行筛选器。</span><span class="sxs-lookup"><span data-stu-id="b000b-705">As in earlier versions, if the Order property is explicitly specified, the filters are run in the specified order.</span></span>

## <a id="0.1__Toc274034230"></a>  <span data-ttu-id="b000b-706">已知的问题</span><span class="sxs-lookup"><span data-stu-id="b000b-706">Known Issues</span></span>

<span data-ttu-id="b000b-707">在安装期间，EULA 接受对话框在小于预期的窗口中显示的许可条款。</span><span class="sxs-lookup"><span data-stu-id="b000b-707">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>

<span data-ttu-id="b000b-708">Razor 视图没有 IntelliSense 支持和语法突出显示。</span><span class="sxs-lookup"><span data-stu-id="b000b-708">Razor views do not have IntelliSense support nor syntax highlighting.</span></span> <span data-ttu-id="b000b-709">我们已预见到会更高版本的一部分包含在 Visual Studio 中的 Razor 语法的支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-709">It is anticipated that support for Razor syntax in Visual Studio will be included as part of a later release.</span></span>

<span data-ttu-id="b000b-710">在编辑 Razor 视图 （CSHTML 文件） 时<a id="0.1__Toc224729061"> </a> <a id="0.1__Toc238051347"> </a>转到控制器在 Visual Studio 中的菜单项将不可用，并且不有任何代码段。</span><span class="sxs-lookup"><span data-stu-id="b000b-710">When you are editing a Razor view (CSHTML file), the <a id="0.1__Toc224729061"></a><a id="0.1__Toc238051347"></a> Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<span data-ttu-id="b000b-711">当使用@model语法来指定强类型化的 CSHTML 视图中，无法识别的类型的特定于语言的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="b000b-711">When using the @model syntax to specify a strongly typed CSHTML view, language-specific shortcuts for types are not recognized.</span></span> <span data-ttu-id="b000b-712">例如， @model int 不起作用，但@modelInt32 将起作用。</span><span class="sxs-lookup"><span data-stu-id="b000b-712">For example, @model int will not work, but @model Int32 will work.</span></span> <span data-ttu-id="b000b-713">此 bug 的解决方法是指定模型类型时使用的实际类型名称。</span><span class="sxs-lookup"><span data-stu-id="b000b-713">The workaround for this bug is to use the actual type name when you specify the model type.</span></span>

<span data-ttu-id="b000b-714">使用时@model语法来指定强类型化的 CSHTML 视图 (或@ModelType来指定强类型化的 VBHTML 视图)，可以为 null 的类型和数组声明不受支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-714">When using the @model syntax to specify a strongly typed CSHTML view (or @ModelType to specify a strongly typed VBHTML view), nullable types and array declarations are not supported.</span></span> <span data-ttu-id="b000b-715">例如， @model int？ 不受支持。</span><span class="sxs-lookup"><span data-stu-id="b000b-715">For example, @model int? is not supported.</span></span> <span data-ttu-id="b000b-716">请改用`@model Nullable<Int32>`。</span><span class="sxs-lookup"><span data-stu-id="b000b-716">Instead, use `@model Nullable<Int32>`.</span></span> <span data-ttu-id="b000b-717">语法@modelstring []，也不支持; 请改用`@model IList<string>`。</span><span class="sxs-lookup"><span data-stu-id="b000b-717">The syntax @model string[] is also not supported; instead, use `@model IList<string>`.</span></span>

<span data-ttu-id="b000b-718">当 ASP.NET MVC 2 项目升级到 ASP.NET MVC 3 时，请确保以下代码添加到 Web.config 文件的 appSettings 节：</span><span class="sxs-lookup"><span data-stu-id="b000b-718">When you upgrade an ASP.NET MVC 2 project to ASP.NET MVC 3, make sure to add the following to the appSettings section of the Web.config file:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

<span data-ttu-id="b000b-719">没有一个已知的问题，会导致窗体身份验证始终将未经身份验证的用户重定向到 ~/Account/登录名，忽略在 Web.config 中使用的窗体身份验证设置。解决方法是添加以下应用设置。</span><span class="sxs-lookup"><span data-stu-id="b000b-719">There's a known issue that causes Forms Authentication to always redirect unauthenticated users to ~/Account/Login, ignoring the forms authentication setting used in Web.config. The workaround is to add the following app setting.</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>  <span data-ttu-id="b000b-720">免责声明</span><span class="sxs-lookup"><span data-stu-id="b000b-720">Disclaimer</span></span>

<span data-ttu-id="b000b-721">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="b000b-721">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="b000b-722">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="b000b-722">All rights reserved.</span></span> <span data-ttu-id="b000b-723">本文档提供"作为-是。"</span><span class="sxs-lookup"><span data-stu-id="b000b-723">This document is provided "as-is."</span></span> <span data-ttu-id="b000b-724">恕不另行通知可能会更改的信息和包括 URL 和其他 Internet 网站参考，本文档中表达的观点。</span><span class="sxs-lookup"><span data-stu-id="b000b-724">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span> <span data-ttu-id="b000b-725">您自行承担其使用风险。</span><span class="sxs-lookup"><span data-stu-id="b000b-725">You bear the risk of using it.</span></span>

<span data-ttu-id="b000b-726">本文档未向您提供任何 Microsoft 产品中任何知识产权的任何合法权利。</span><span class="sxs-lookup"><span data-stu-id="b000b-726">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="b000b-727">您可为了内部参考目的复制和使用本文档。</span><span class="sxs-lookup"><span data-stu-id="b000b-727">You may copy and use this document for your internal, reference purposes.</span></span>
