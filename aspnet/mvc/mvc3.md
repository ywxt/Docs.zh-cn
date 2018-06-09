---
uid: mvc/mvc3
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: (包括 2011 年 4 月工具更新)ASP.NET MVC 3 是一个框架，用于构建使用成熟设计模式的可缩放的、 基于标准的 web 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/05/2010
ms.topic: article
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: c7eee987b28a5d7f8b40fe89a7bf7517ec06646f
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "28034732"
---
<a name="aspnet-mvc-3"></a><span data-ttu-id="31601-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="31601-103">ASP.NET MVC 3</span></span>
====================
> <span data-ttu-id="31601-104">*(包括 2011 年 4 月工具更新)*</span><span class="sxs-lookup"><span data-stu-id="31601-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="31601-105">ASP.NET MVC 3 是一个框架，用于构建可缩放的、 基于标准的 web 应用程序使用成熟设计模式以及 ASP.NET 和.NET Framework 的能力。</span><span class="sxs-lookup"><span data-stu-id="31601-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="31601-106">ASP.NET MVC 2，以便开始使用它现在安装并排显示 ！</span><span class="sxs-lookup"><span data-stu-id="31601-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="31601-107">下载[此处安装程序](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="31601-107">Download the [installer here](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>


## <a name="top-features"></a><span data-ttu-id="31601-108">靠前的特征</span><span class="sxs-lookup"><span data-stu-id="31601-108">Top Features</span></span>

- <span data-ttu-id="31601-109">通过 NuGet 可扩展的集成基架系统</span><span class="sxs-lookup"><span data-stu-id="31601-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="31601-110">HTML 5 启用的项目模板</span><span class="sxs-lookup"><span data-stu-id="31601-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="31601-111">包括新的 Razor 视图引擎的表达视图</span><span class="sxs-lookup"><span data-stu-id="31601-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="31601-112">与依赖关系注入和全局操作筛选器的功能强大挂钩</span><span class="sxs-lookup"><span data-stu-id="31601-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="31601-113">丰富的 JavaScript 支持非介入式 JavaScript、 jQuery 验证，以及 JSON 绑定</span><span class="sxs-lookup"><span data-stu-id="31601-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="31601-114">*读取完整功能列表[下面](#overview)*</span><span class="sxs-lookup"><span data-stu-id="31601-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="31601-115">顶部的链接</span><span class="sxs-lookup"><span data-stu-id="31601-115">Top Links</span></span>

<span data-ttu-id="31601-116">什么是 ASP.NET MVC 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="31601-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="31601-117">Phil Haack: [ASP.NET MVC 3 发布](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="31601-118">Scott Hanselman: [ASP.NET MVC3、 WebMatrix、 NuGet、 IIS Express 和 Orchard 发布的上下文中的 Microsoft 年 1 月 Web 版本](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="31601-119">Scott Guthrie:[宣布的 ASP.NET MVC 3、 IIS Express、 SQL CE 4、 Web 场框架、 Orchard、 WebMatrix 发布](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="31601-120">ASP.NET MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="31601-121">安装和帮助</span><span class="sxs-lookup"><span data-stu-id="31601-121">Installation and Help</span></span>

- <span data-ttu-id="31601-122">安装 ASP.NET MVC 3 使用[Web 平台安装程序 （推荐）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span><span class="sxs-lookup"><span data-stu-id="31601-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="31601-123">安装 ASP.NET MVC 3 使用[可执行安装程序](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="31601-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="31601-124">安装[Visual Studio 11 开发者预览版的 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="31601-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="31601-125">读取[简介 ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span><span class="sxs-lookup"><span data-stu-id="31601-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="31601-126">获取帮助和讨论中的 ASP.NET MVC 3[论坛](https://forums.asp.net/1146.aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="31601-127">ASP.NET MVC 3 概述</span><span class="sxs-lookup"><span data-stu-id="31601-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="31601-128">ASP.NET MVC 3 基于 ASP.NET MVC 1 和 2，添加两者都简化你的代码，让更深入地扩展性的强大功能。</span><span class="sxs-lookup"><span data-stu-id="31601-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="31601-129">本主题提供许多新功能包含在此版本中，已组织到以下各节的概述：</span><span class="sxs-lookup"><span data-stu-id="31601-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="31601-130">MvcScaffold 集成可扩展基架</span><span class="sxs-lookup"><span data-stu-id="31601-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="31601-131">HTML 5 启用的项目模板</span><span class="sxs-lookup"><span data-stu-id="31601-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="31601-132">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="31601-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="31601-133">对多个视图引擎的支持</span><span class="sxs-lookup"><span data-stu-id="31601-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="31601-134">控制器改进</span><span class="sxs-lookup"><span data-stu-id="31601-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="31601-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="31601-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="31601-136">模型验证的改进</span><span class="sxs-lookup"><span data-stu-id="31601-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="31601-137">依赖关系注入改进</span><span class="sxs-lookup"><span data-stu-id="31601-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="31601-138">其他新功能</span><span class="sxs-lookup"><span data-stu-id="31601-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="31601-139">MvcScaffold 集成可扩展基架</span><span class="sxs-lookup"><span data-stu-id="31601-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="31601-140">新的基架系统更加简单可以选取并开始高效使用，如果你是全新的 framework，并可自动执行常见的开发任务，如果你有经验和已知道你要做什么。</span><span class="sxs-lookup"><span data-stu-id="31601-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="31601-141">这支持新的 NuGet*基架*包调用**MvcScaffolding**。</span><span class="sxs-lookup"><span data-stu-id="31601-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="31601-142">术语"基架"由许多软件技术用于意味着"快速生成的基本概述的软件，你可以然后编辑和自定义"。</span><span class="sxs-lookup"><span data-stu-id="31601-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="31601-143">我们正在创建的 ASP.NET MVC 基架包是极大地有益在几种场景：</span><span class="sxs-lookup"><span data-stu-id="31601-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="31601-144">**如果你首次了解 ASP.NET MVC**，因为它可用于获取一些有用的工作代码，，然后可以编辑，并根据需要调整的快捷方法。</span><span class="sxs-lookup"><span data-stu-id="31601-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="31601-145">它将保存你的看一看空白页，并且不知道从何处着手缩短从 ！</span><span class="sxs-lookup"><span data-stu-id="31601-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="31601-146">**如果您非常熟悉 ASP.NET MVC，而且现在浏览某些新的外接程序技术**的对象关系映射器、 视图引擎、 测试的库，如等，因为该技术的创建者可能还创建了基架程序包它。</span><span class="sxs-lookup"><span data-stu-id="31601-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="31601-147">**如果涉及到你的工作，重复创建相似的类或某种类型的文件**，这是因为你可以创建自定义 scaffolders 输出测试装置、 部署脚本或你需要的任何其他内容。</span><span class="sxs-lookup"><span data-stu-id="31601-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="31601-148">你的团队中的每个人都可以将你的自定义 scaffolders。</span><span class="sxs-lookup"><span data-stu-id="31601-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="31601-149">MvcScaffolding 中的其他功能包括：</span><span class="sxs-lookup"><span data-stu-id="31601-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="31601-150">对于 C# 和 VB 项目的支持</span><span class="sxs-lookup"><span data-stu-id="31601-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="31601-151">对 Razor 和 ASPX 视图引擎的支持</span><span class="sxs-lookup"><span data-stu-id="31601-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="31601-152">支持为 ASP.NET MVC 区域基架和使用自定义视图布局/母版</span><span class="sxs-lookup"><span data-stu-id="31601-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="31601-153">你可以轻松地输出通过编辑自定义 T4 模板</span><span class="sxs-lookup"><span data-stu-id="31601-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="31601-154">你可以添加全新 scaffolders 使用自定义 PowerShell 逻辑和自定义 T4 模板。</span><span class="sxs-lookup"><span data-stu-id="31601-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="31601-155">这些 （和你向用户提供了任何自定义参数） 会自动出现在控制台 tab 自动补全列表。</span><span class="sxs-lookup"><span data-stu-id="31601-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="31601-156">你可以包含不同技术的其他 scaffolders 的 NuGet 包 （例如，不存在的概念证明一个 linq to SQL 现在） 和混合和匹配它们在一起</span><span class="sxs-lookup"><span data-stu-id="31601-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="31601-157">ASP.NET MVC 3 Tools 更新包括全力 Visual Studio 支持此基架系统，如：</span><span class="sxs-lookup"><span data-stu-id="31601-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="31601-158">添加控制器对话框现在支持完全自动的基架创建、 读取、 更新和删除控制器操作和相应的视图。</span><span class="sxs-lookup"><span data-stu-id="31601-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="31601-159">默认情况下，这的基架使用 EF Code First 数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="31601-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="31601-160">添加控制器对话框支持*可扩展的基架*通过 NuGet 包如*MvcScaffolding*。</span><span class="sxs-lookup"><span data-stu-id="31601-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="31601-161">这样将允许你使用适用于 ODBCDirect 创建 NHibernate 或甚至 JET 等其他数据访问技术的基架，如果你要因此并在对话框的自定义基架插入 ！</span><span class="sxs-lookup"><span data-stu-id="31601-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="31601-162">有关 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="31601-163">Steve Sanderson 文章系列，包括：</span><span class="sxs-lookup"><span data-stu-id="31601-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="31601-164">简介： 搭建基架 ASP.NET MVC 3 项目与 MvcScaffolding 包</span><span class="sxs-lookup"><span data-stu-id="31601-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="31601-165">标准用法： 典型用例和选项</span><span class="sxs-lookup"><span data-stu-id="31601-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="31601-166">一个对多关系</span><span class="sxs-lookup"><span data-stu-id="31601-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="31601-167">基架操作和单元测试</span><span class="sxs-lookup"><span data-stu-id="31601-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="31601-168">重写 T4 模板</span><span class="sxs-lookup"><span data-stu-id="31601-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="31601-169">此文章： 创建自定义 scaffolders</span><span class="sxs-lookup"><span data-stu-id="31601-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="31601-170">从在 PDC 2010 会话 Scott Hanselman post[构建与 Microsoft"未命名包的 Web Love"博客](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="31601-171">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="31601-172">HTML 5 项目模板</span><span class="sxs-lookup"><span data-stu-id="31601-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="31601-173">新项目对话框包括项目模板的复选框启用 HTML 5 版本。</span><span class="sxs-lookup"><span data-stu-id="31601-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="31601-174">这些模板利用 Modernizr 1.7，以提供对 HTML 5 和 CSS 3 在低级别浏览器中的兼容性支持。</span><span class="sxs-lookup"><span data-stu-id="31601-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="31601-175">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="31601-175">The Razor View Engine</span></span>

<span data-ttu-id="31601-176">ASP.NET MVC 3 附带了名为提供以下好处的 Razor 新视图引擎：</span><span class="sxs-lookup"><span data-stu-id="31601-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="31601-177">Razor 语法是干净和简洁，需最小数量的击键。</span><span class="sxs-lookup"><span data-stu-id="31601-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="31601-178">Razor 很容易地了解，在某种因为它基于现有的语言，如 C# 和 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="31601-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="31601-179">Visual Studio 包含 Razor 语法的 IntelliSense 和代码着色。</span><span class="sxs-lookup"><span data-stu-id="31601-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="31601-180">Razor 视图可以是单元测试，而无需您运行应用程序或启动 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="31601-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="31601-181">一些新的 Razor 功能包括：</span><span class="sxs-lookup"><span data-stu-id="31601-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="31601-182">`@model` 用于指定传递到该视图的类型的语法。</span><span class="sxs-lookup"><span data-stu-id="31601-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="31601-183">`@* *@` 注释语法。</span><span class="sxs-lookup"><span data-stu-id="31601-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="31601-184">能够指定默认值 (如`layoutpage`) 一次针对整个站点。</span><span class="sxs-lookup"><span data-stu-id="31601-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="31601-185">`Html.Raw`用于显示不带 HTML 编码的文本的方法它。</span><span class="sxs-lookup"><span data-stu-id="31601-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="31601-186">对多个视图之间共享代码的支持 (*\_viewstart.cshtml*或 *\_viewstart.vbhtml*文件)。</span><span class="sxs-lookup"><span data-stu-id="31601-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="31601-187">Razor 还包括新的 HTML 帮助器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31601-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="31601-188">`Chart`。</span><span class="sxs-lookup"><span data-stu-id="31601-188">`Chart`.</span></span> <span data-ttu-id="31601-189">呈现图表中，产品与 ASP.NET 4 中的图表控件相同的功能。</span><span class="sxs-lookup"><span data-stu-id="31601-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="31601-190">`WebGrid`。</span><span class="sxs-lookup"><span data-stu-id="31601-190">`WebGrid`.</span></span> <span data-ttu-id="31601-191">呈现数据网格中，完成，但分页和排序功能。</span><span class="sxs-lookup"><span data-stu-id="31601-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="31601-192">`Crypto`。</span><span class="sxs-lookup"><span data-stu-id="31601-192">`Crypto`.</span></span> <span data-ttu-id="31601-193">使用哈希算法来创建正确 salted 和哈希处理密码。</span><span class="sxs-lookup"><span data-stu-id="31601-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="31601-194">`WebImage`。</span><span class="sxs-lookup"><span data-stu-id="31601-194">`WebImage`.</span></span> <span data-ttu-id="31601-195">呈现图像。</span><span class="sxs-lookup"><span data-stu-id="31601-195">Renders an image.</span></span>
- <span data-ttu-id="31601-196">`WebMail`。</span><span class="sxs-lookup"><span data-stu-id="31601-196">`WebMail`.</span></span> <span data-ttu-id="31601-197">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="31601-197">Sends an email message.</span></span>

<span data-ttu-id="31601-198">有关 Razor 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="31601-199">引入 Razor Scott Guthrie 的博客文章</span><span class="sxs-lookup"><span data-stu-id="31601-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="31601-200">Scott Guthrie 的博客文章简介@model关键字</span><span class="sxs-lookup"><span data-stu-id="31601-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="31601-201">Scott Guthrie 的博客文章简介 Razor 布局</span><span class="sxs-lookup"><span data-stu-id="31601-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="31601-202">Razor API 快速参考</span><span class="sxs-lookup"><span data-stu-id="31601-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="31601-203">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="31601-204">对多个视图引擎的支持</span><span class="sxs-lookup"><span data-stu-id="31601-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="31601-205">**添加视图**ASP.NET MVC 3 中的对话框，可以选择你想要使用的视图引擎和**新项目**对话框中，可以指定项目的默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="31601-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="31601-206">你可以如选择 Web 窗体视图引擎 (ASPX)、 Razor 或开放源代码视图引擎[Spark](http://sparkviewengine.com/)， [NHaml](https://code.google.com/p/nhaml/)，或[NDjango](http://ndjango.org/)。</span><span class="sxs-lookup"><span data-stu-id="31601-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="31601-207">控制器改进</span><span class="sxs-lookup"><span data-stu-id="31601-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="31601-208">全局操作筛选器</span><span class="sxs-lookup"><span data-stu-id="31601-208">Global Action Filters</span></span>

<span data-ttu-id="31601-209">有时你想要执行逻辑操作方法运行之前或之后运行的操作方法。</span><span class="sxs-lookup"><span data-stu-id="31601-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="31601-210">若要支持此功能，ASP.NET MVC 2 提供的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="31601-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="31601-211">操作筛选器是提供一种将预操作和后操作行为添加到特定控制器操作方法的声明性方法的自定义属性。</span><span class="sxs-lookup"><span data-stu-id="31601-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="31601-212">但是，在某些情况下你可能想要指定适用于所有的操作方法的操作前行为或操作后行为。</span><span class="sxs-lookup"><span data-stu-id="31601-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="31601-213">MVC 3，可以通过将它们添加到指定全局筛选器`GlobalFilters`集合。</span><span class="sxs-lookup"><span data-stu-id="31601-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="31601-214">有关全局操作筛选器的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="31601-215">MVC 3 Preview 上的 Scott Guthrie 的博客</span><span class="sxs-lookup"><span data-stu-id="31601-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="31601-216">[在 ASP.NET MVC 中筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="31601-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="31601-217">新的"ViewBag"属性</span><span class="sxs-lookup"><span data-stu-id="31601-217">New "ViewBag" Property</span></span>

<span data-ttu-id="31601-218">MVC 2 控制器支持`ViewData`使您能够将数据传递给使用后期绑定字典 API 的视图模板的属性。</span><span class="sxs-lookup"><span data-stu-id="31601-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="31601-219">在 MVC 3，你还可以使用某种程度上更简单的语法与`ViewBag`属性来完成相同的目的。</span><span class="sxs-lookup"><span data-stu-id="31601-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="31601-220">例如，而不是编写`ViewData["Message"]="text"`，你可以编写`ViewBag.Message="text"`。</span><span class="sxs-lookup"><span data-stu-id="31601-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="31601-221">不需要定义任何强类型类使用`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="31601-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="31601-222">因为它是动态的属性，你可以转而只需获取或设置属性和它将解析它们动态在运行时。</span><span class="sxs-lookup"><span data-stu-id="31601-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="31601-223">在内部，`ViewBag`属性存储为名称/值对中`ViewData`字典。</span><span class="sxs-lookup"><span data-stu-id="31601-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="31601-224">(注意： 在大多数的预发行版本的 MVC 3`ViewBag`属性的名称为`ViewModel`属性。)</span><span class="sxs-lookup"><span data-stu-id="31601-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="31601-225">新的"ActionResult"类型</span><span class="sxs-lookup"><span data-stu-id="31601-225">New "ActionResult" Types</span></span>

<span data-ttu-id="31601-226">以下`ActionResult`新增或增强在 MVC 3 是类型和相应的帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="31601-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="31601-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="31601-228">向客户端返回 HTTP 状态代码为 404。</span><span class="sxs-lookup"><span data-stu-id="31601-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="31601-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="31601-230">返回临时重定向 （HTTP 302 状态代码） 或根据一个布尔型参数的永久重定向 （HTTP 301 状态代码）。</span><span class="sxs-lookup"><span data-stu-id="31601-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="31601-231">与此更改后，结合[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在具有执行永久重定向的三个方法： `RedirectPermanent`， `RedirectToRoutePermanent`，和`RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="31601-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="31601-232">这些方法返回的实例`RedirectResult`与`Permanent`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="31601-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="31601-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="31601-234">返回用户指定的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="31601-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="31601-235">JavaScript 和 Ajax 改进</span><span class="sxs-lookup"><span data-stu-id="31601-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="31601-236">默认情况下，在 MVC 3 的 Ajax 和验证帮助器使用的非介入式 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="31601-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="31601-237">非介入式 JavaScript 可避免将内联 JavaScript 注入到 HTML。</span><span class="sxs-lookup"><span data-stu-id="31601-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="31601-238">这可以让你 HTML 较小、 更混乱，并使其更轻松地替换或自定义 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="31601-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="31601-239">MVC 3 中的验证帮助器还使用`jQueryValidate`默认的插件。</span><span class="sxs-lookup"><span data-stu-id="31601-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="31601-240">如果你想 MVC 2 行为，则可以禁用非介入式 JavaScript 使用*web.config*文件设置。</span><span class="sxs-lookup"><span data-stu-id="31601-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="31601-241">有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="31601-242">Wikipedia 站点上的非介入式 JavaScript 的基本简介</span><span class="sxs-lookup"><span data-stu-id="31601-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="31601-243">Brad wilson 制作的非介入式 JavaScript Post</span><span class="sxs-lookup"><span data-stu-id="31601-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="31601-244">Brad wilson 制作的非介入式 JavaScript 验证 Post</span><span class="sxs-lookup"><span data-stu-id="31601-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="31601-245">[使用 Razor 和非介入式 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 站点上教程）</span><span class="sxs-lookup"><span data-stu-id="31601-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="31601-246">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="31601-247">默认情况下启用的客户端验证</span><span class="sxs-lookup"><span data-stu-id="31601-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="31601-248">在早期版本的 MVC，你需要显式调用`Html.EnableClientValidation`从以启用客户端验证视图的方法。</span><span class="sxs-lookup"><span data-stu-id="31601-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="31601-249">在 MVC 3 这不再需要因为默认情况下启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="31601-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="31601-250">(你可以禁用此选项使用中的设置*web.config*文件。)</span><span class="sxs-lookup"><span data-stu-id="31601-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="31601-251">为了使客户端验证正常工作，你仍需要引用相应 jQuery 和你的站点中的 jQuery 验证库。</span><span class="sxs-lookup"><span data-stu-id="31601-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="31601-252">可以在你自己的服务器上托管这些库，也可以从 Microsoft 或 Google Cdn 等内容交付网络 (CDN) 中引用它们。</span><span class="sxs-lookup"><span data-stu-id="31601-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="31601-253">远程验证程序</span><span class="sxs-lookup"><span data-stu-id="31601-253">Remote Validator</span></span>

<span data-ttu-id="31601-254">ASP.NET MVC 3 支持新[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)使您能够利用 jQuery 验证即插即用中的类所提供的远程验证程序支持。</span><span class="sxs-lookup"><span data-stu-id="31601-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="31601-255">这使客户端验证库自动调用若要执行仅可完成的验证逻辑服务器定义的自定义方法服务器端。</span><span class="sxs-lookup"><span data-stu-id="31601-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="31601-256">在下面的示例中，`Remote`属性指定客户端验证将调用名为操作`UserNameAvailable`上`UsersController`若要验证的类`UserName`字段。</span><span class="sxs-lookup"><span data-stu-id="31601-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="31601-257">下面的示例显示相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="31601-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="31601-258">有关如何使用`Remote`属性，请参阅[如何： 在 ASP.NET MVC 实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="31601-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="31601-259">JSON 绑定支持</span><span class="sxs-lookup"><span data-stu-id="31601-259">JSON Binding Support</span></span>

<span data-ttu-id="31601-260">ASP.NET MVC 3 包括内置 JSON 绑定支持，使得操作接收 JSON 编码数据和模型它将与绑定操作方法参数的方法。</span><span class="sxs-lookup"><span data-stu-id="31601-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="31601-261">此功能是涉及客户端模板和数据绑定的方案中十分有用。</span><span class="sxs-lookup"><span data-stu-id="31601-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="31601-262">（客户端可以模板来格式化并使用在客户端执行的模板显示单个数据项的集。）MVC 3 可以轻松地将客户端模板连接使用的服务器上的操作方法，来发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="31601-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="31601-263">有关 JSON 绑定支持的详细信息，请参阅**JavaScript 和 AJAX 改进**部分[Scott Guthrie 的博客文章 MVC 3 预览](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="31601-264">模型验证的改进</span><span class="sxs-lookup"><span data-stu-id="31601-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="31601-265">"DataAnnotations"元数据属性</span><span class="sxs-lookup"><span data-stu-id="31601-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="31601-266">ASP.NET MVC 3 支持`DataAnnotations`元数据特性例如`DisplayAttribute`。</span><span class="sxs-lookup"><span data-stu-id="31601-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="31601-267">"ValidationAttribute"类</span><span class="sxs-lookup"><span data-stu-id="31601-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="31601-268">`ValidationAttribute`类也已经过改进在.NET Framework 4，以支持新`IsValid`提供了有关当前验证上下文，如哪些对象正在验证的详细信息的重载。</span><span class="sxs-lookup"><span data-stu-id="31601-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="31601-269">这使你可以在其中验证基于模型的另一个属性的当前值的更丰富方案。</span><span class="sxs-lookup"><span data-stu-id="31601-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="31601-270">例如，新`CompareAttribute`特性，可以比较两个模型属性的值。</span><span class="sxs-lookup"><span data-stu-id="31601-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="31601-271">在下面的示例中，`ComparePassword`属性必须与匹配`Password`字段才有效。</span><span class="sxs-lookup"><span data-stu-id="31601-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="31601-272">验证接口</span><span class="sxs-lookup"><span data-stu-id="31601-272">Validation Interfaces</span></span>

<span data-ttu-id="31601-273">[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)界面使您可以执行模型级别验证，并且它使您能够提供特定于整个模型，或在模型内的两个属性之间的状态的错误消息的验证.</span><span class="sxs-lookup"><span data-stu-id="31601-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="31601-274">MVC 3 现在检索从错误`IValidatableObject`接口时模型绑定，并自动标志或突出显示了影响使用的内置的 HTML 窗体的帮助器的视图中的字段。</span><span class="sxs-lookup"><span data-stu-id="31601-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="31601-275">[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)接口使验证程序是否对客户端验证的支持在运行时发现的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="31601-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="31601-276">此接口已经过设计，因此，它可以与多种验证框架集成。</span><span class="sxs-lookup"><span data-stu-id="31601-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="31601-277">有关验证接口的详细信息，请参阅**模型验证改进**部分[Scott Guthrie 的博客文章 MVC 3 预览](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="31601-278">（但是，请注意，对"IValidateObject"博客中的引用应"IValidatableObject"。）</span><span class="sxs-lookup"><span data-stu-id="31601-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="31601-279">依赖关系注入改进</span><span class="sxs-lookup"><span data-stu-id="31601-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="31601-280">ASP.NET MVC 3 应用依赖关系注入 (DI) 和集成与依赖关系注入或控制反向 (IOC) 容器提供更好地支持。</span><span class="sxs-lookup"><span data-stu-id="31601-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="31601-281">以下区域中添加了对 DI 支持：</span><span class="sxs-lookup"><span data-stu-id="31601-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="31601-282">（注册和将注入控制器工厂，将注入控制器） 的控制器。</span><span class="sxs-lookup"><span data-stu-id="31601-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="31601-283">（注册以及将注入视图引擎，将依赖关系注入到视图页） 视图。</span><span class="sxs-lookup"><span data-stu-id="31601-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="31601-284">操作筛选器 （查找和将注入筛选器）。</span><span class="sxs-lookup"><span data-stu-id="31601-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="31601-285">模型联编程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="31601-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="31601-286">为模型验证提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="31601-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="31601-287">为模型元数据提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="31601-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="31601-288">值提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="31601-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="31601-289">MVC 3 还支持[常见服务定位器](https://github.com/unitycontainer/commonservicelocator)库和支持该库的任何 DI 容器`IServiceLocator`接口。</span><span class="sxs-lookup"><span data-stu-id="31601-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="31601-290">它还支持新`IDependencyResolver`轻松地集成 DI 框架的接口。</span><span class="sxs-lookup"><span data-stu-id="31601-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="31601-291">有关 DI MVC 3 中的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="31601-292">Brad wilson 制作的系列的服务位置上的博客文章</span><span class="sxs-lookup"><span data-stu-id="31601-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="31601-293">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="31601-294">其他新功能</span><span class="sxs-lookup"><span data-stu-id="31601-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="31601-295">NuGet 集成</span><span class="sxs-lookup"><span data-stu-id="31601-295">NuGet Integration</span></span>

<span data-ttu-id="31601-296">ASP.NET MVC 3 自动安装，并作为其安装的一部分启用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="31601-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="31601-297">NuGet 是一个免费的开源包管理器，可以轻松地查找、 安装和在你项目中使用.NET 库和工具。</span><span class="sxs-lookup"><span data-stu-id="31601-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="31601-298">它适用于所有 Visual Studio 项目类型 （包括 ASP.NET Web 窗体和 ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="31601-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="31601-299">NuGet 让开发人员维护开放源代码项目 （例如，如 Moq、 NHibernate、 Ninject、 StructureMap、 NUnit、 Windsor、 RhinoMocks 和 Elmah 的项目） 以其库打包并在联机库中注册它们。</span><span class="sxs-lookup"><span data-stu-id="31601-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="31601-300">然后，它很容易的.NET 开发人员想要使用这些库之一来找到程序包，然后将它安装在他们正在处理的项目。</span><span class="sxs-lookup"><span data-stu-id="31601-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="31601-301">与 ASP.NET 3 Tools 更新，项目模板包括 JavaScript 库预安装的 NuGet 包，因此它们是通过 NuGet 可更新。</span><span class="sxs-lookup"><span data-stu-id="31601-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="31601-302">Entity Framework Code First 还预安装了作为 NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="31601-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="31601-303">有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="31601-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="31601-304">局部页面输出缓存</span><span class="sxs-lookup"><span data-stu-id="31601-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="31601-305">ASP.NET MVC 具有支持版本 1 以来，输出缓存的完整的页面响应。</span><span class="sxs-lookup"><span data-stu-id="31601-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="31601-306">MVC 3 还支持局部页面输出缓存，使您能够轻松地缓存区域或的响应片段。</span><span class="sxs-lookup"><span data-stu-id="31601-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="31601-307">有关缓存的详细信息，请参阅**部分页面输出缓存**部分[Scott Guthrie 的博客文章在 MVC 3 候选发布版](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)和**子操作输出缓存**部分[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="31601-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="31601-308">对请求验证进行精细控制</span><span class="sxs-lookup"><span data-stu-id="31601-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="31601-309">ASP.NET MVC 具有自动有助于保护计算机免受 XSS 和 HTML 注入攻击的内置请求验证。</span><span class="sxs-lookup"><span data-stu-id="31601-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="31601-310">但是，有时要显式禁用请求验证，例如，如果你想要让用户发布 HTML 内容 （例如，在博客条目或 CMS 内容）。</span><span class="sxs-lookup"><span data-stu-id="31601-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="31601-311">你现在可以添加[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性设为模型或查看模型禁用基于每个属性过程模型绑定中的请求验证。</span><span class="sxs-lookup"><span data-stu-id="31601-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="31601-312">有关请求验证的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="31601-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="31601-313">**非介入式 JavaScript 和验证**主题中[Scott Guthrie 的博客文章在 MVC 3 候选发布版](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)。</span><span class="sxs-lookup"><span data-stu-id="31601-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="31601-314">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="31601-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="31601-315">可扩展的"新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="31601-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="31601-316">在 ASP.NET MVC 3 中，你可以添加项目模板，视图引擎和单元测试项目框架到**新项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="31601-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="31601-317">模板基架改进</span><span class="sxs-lookup"><span data-stu-id="31601-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="31601-318">ASP.NET MVC 3 基架模板执行更好地标识模型上的主键属性并进行相应地比在早期版本的 MVC 处理。</span><span class="sxs-lookup"><span data-stu-id="31601-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="31601-319">（例如，基架模板现在确保为主键不为一个可编辑窗体字段基架。）</span><span class="sxs-lookup"><span data-stu-id="31601-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="31601-320">默认情况下，创建和编辑的基架现在使用`Html.EditorFor`帮助器而不是`Html.TextBoxFor`帮助器。</span><span class="sxs-lookup"><span data-stu-id="31601-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="31601-321">这可改进对形式的数据模型的元数据支持批注属性时**添加视图**对话框生成视图。</span><span class="sxs-lookup"><span data-stu-id="31601-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="31601-322">"Html.LabelFor"和"Html.LabelForModel"的新重载</span><span class="sxs-lookup"><span data-stu-id="31601-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="31601-323">为添加新的方法重载了`LabelFor`和`LabelForModel`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="31601-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="31601-324">新的重载使你能够指定或重写的标签文本。</span><span class="sxs-lookup"><span data-stu-id="31601-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="31601-325">无会话控制器支持</span><span class="sxs-lookup"><span data-stu-id="31601-325">Sessionless Controller Support</span></span>

<span data-ttu-id="31601-326">在 ASP.NET MVC 3 中你可以指示是否要在控制器类，以使用会话状态，并且如果是这样，是否会话状态应为读/写或只读的。</span><span class="sxs-lookup"><span data-stu-id="31601-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="31601-327">有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="31601-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="31601-328">新的"AdditionalMetadataAttribute"类</span><span class="sxs-lookup"><span data-stu-id="31601-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="31601-329">你可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)特性来填充`ModelMetadata.AdditionalValues`模型属性的字典。</span><span class="sxs-lookup"><span data-stu-id="31601-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="31601-330">例如，如果视图模型具有一个属性，应仅向管理员显示，还可以批注该属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="31601-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="31601-331">呈现产品视图模型时，此元数据将提供给任何显示或编辑器模板。</span><span class="sxs-lookup"><span data-stu-id="31601-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="31601-332">它是由您来解释的元数据信息。</span><span class="sxs-lookup"><span data-stu-id="31601-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="31601-333">AccountController 改进</span><span class="sxs-lookup"><span data-stu-id="31601-333">AccountController improvements</span></span>

<span data-ttu-id="31601-334">AccountController 中的 Internet 项目模板中已大大改进。</span><span class="sxs-lookup"><span data-stu-id="31601-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="31601-335">新建 Intranet 项目模板</span><span class="sxs-lookup"><span data-stu-id="31601-335">New Intranet Project Template</span></span>

<span data-ttu-id="31601-336">新的 Intranet 项目模板是包含其启用 Windows 身份验证并删除 AccountController 中。</span><span class="sxs-lookup"><span data-stu-id="31601-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>
