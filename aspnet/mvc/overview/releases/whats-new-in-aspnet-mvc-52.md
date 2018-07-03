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
<a name="whats-new-in-aspnet-mvc-52"></a><span data-ttu-id="51b3f-102">什么是 ASP.NET MVC 5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="51b3f-102">What’s New in ASP.NET MVC 5.2</span></span>
====================
<span data-ttu-id="51b3f-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="51b3f-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="51b3f-104">本主题介绍什么是 ASP.NET MVC 5.2 的新增功能[Microsoft.AspNet.MVC 5.2.2](#52)和[ASP.NET MVC 5.2.3、web Beta](#mvc523Beta)</span><span class="sxs-lookup"><span data-stu-id="51b3f-104">This topic describes what's new for ASP.NET MVC 5.2, [Microsoft.AspNet.MVC 5.2.2](#52) and [ASP.NET MVC 5.2.3 Beta](#mvc523Beta)</span></span>

- [<span data-ttu-id="51b3f-105">软件要求</span><span class="sxs-lookup"><span data-stu-id="51b3f-105">Software Requirements</span></span>](#softRequire)
- [<span data-ttu-id="51b3f-106">下载</span><span class="sxs-lookup"><span data-stu-id="51b3f-106">Download</span></span>](#download)
- [<span data-ttu-id="51b3f-107">文档</span><span class="sxs-lookup"><span data-stu-id="51b3f-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="51b3f-108">在 ASP.NET MVC 5.2 的新增功能</span><span class="sxs-lookup"><span data-stu-id="51b3f-108">New Features in ASP.NET MVC 5.2</span></span>](#new-features)

    - [<span data-ttu-id="51b3f-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="51b3f-109">Attribute routing improvements</span></span>](#attributerouting)
- [<span data-ttu-id="51b3f-110">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="51b3f-110">Known Issues and Breaking Changes</span></span>](#knownbreakingchanges)
- [<span data-ttu-id="51b3f-111">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="51b3f-111">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="51b3f-112">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="51b3f-112">Microsoft.AspNet.MVC 5.2.2</span></span>](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a><span data-ttu-id="51b3f-113">软件要求</span><span class="sxs-lookup"><span data-stu-id="51b3f-113">Software Requirements</span></span>

- <span data-ttu-id="51b3f-114">Visual Studio 2012： 下载[ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062)。</span><span class="sxs-lookup"><span data-stu-id="51b3f-114">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="51b3f-115">Visual Studio 2013： 下载[Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="51b3f-115">Visual Studio 2013: Download [Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064) or higher.</span></span> <span data-ttu-id="51b3f-116">编辑 ASP.NET MVC 5.2 Razor 视图时需要此更新。</span><span class="sxs-lookup"><span data-stu-id="51b3f-116">This update is needed for editing ASP.NET MVC 5.2 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="51b3f-117">下载</span><span class="sxs-lookup"><span data-stu-id="51b3f-117">Download</span></span>

<span data-ttu-id="51b3f-118">运行时功能将发布为 NuGet 库中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="51b3f-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="51b3f-119">所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="51b3f-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="51b3f-120">最新的 ASP.NET MVC 5.2 包具有以下版本:"5.2.0"。</span><span class="sxs-lookup"><span data-stu-id="51b3f-120">The latest ASP.NET MVC 5.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="51b3f-121">可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)。</span><span class="sxs-lookup"><span data-stu-id="51b3f-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="51b3f-122">此版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="51b3f-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="51b3f-123">可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="51b3f-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

<span data-ttu-id="51b3f-124">安装包 Microsoft.AspNet.Mvc-5.2.0 版</span><span class="sxs-lookup"><span data-stu-id="51b3f-124">Install-Package Microsoft.AspNet.Mvc -Version 5.2.0</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="51b3f-125">文档</span><span class="sxs-lookup"><span data-stu-id="51b3f-125">Documentation</span></span>

<span data-ttu-id="51b3f-126">教程和有关 ASP.NET MVC 5.2 的其他信息是可通过 ASP.NET 网站 ([https://www.asp.net/mvc](../../index.md))。</span><span class="sxs-lookup"><span data-stu-id="51b3f-126">Tutorials and other information about ASP.NET MVC 5.2 are available from the ASP.NET web site ([https://www.asp.net/mvc](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a><span data-ttu-id="51b3f-127">在 ASP.NET MVC 5.2 的新增功能</span><span class="sxs-lookup"><span data-stu-id="51b3f-127">New Features in ASP.NET MVC 5.2</span></span>

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="51b3f-128">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="51b3f-128">Attribute routing improvements</span></span>

<span data-ttu-id="51b3f-129">属性路由现在提供了一个名为 IDirectRouteProvider，可完全控制如何发现和配置属性路由的扩展点。</span><span class="sxs-lookup"><span data-stu-id="51b3f-129">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="51b3f-130">IDirectRouteProvider 负责提供的操作和控制器以及关联的路由信息来指定这些操作需要何种路由配置的情况完全列表。</span><span class="sxs-lookup"><span data-stu-id="51b3f-130">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="51b3f-131">调用 MapAttributes/MapHttpAttributeRoutes 时，可能会指定 IDirectRouteProvider 实现。</span><span class="sxs-lookup"><span data-stu-id="51b3f-131">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="51b3f-132">自定义 IDirectRouteProvider 将是最简单通过扩展我们的默认实现，DefaultDirectRouteProvider。</span><span class="sxs-lookup"><span data-stu-id="51b3f-132">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="51b3f-133">此类提供了单独可重写虚拟方法，以更改用于发现属性、 创建路由项，以及发现路由前缀和区域前缀的逻辑。</span><span class="sxs-lookup"><span data-stu-id="51b3f-133">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="51b3f-134">具有新属性路由可扩展性的 IDirectRouteProvider，用户可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="51b3f-134">With the new attribute routing extensibility of IDirectRouteProvider, a user could do the following:</span></span>

1. <span data-ttu-id="51b3f-135">支持的属性路由的继承。</span><span class="sxs-lookup"><span data-stu-id="51b3f-135">Support Inheritance of attribute routes.</span></span> <span data-ttu-id="51b3f-136">例如，在以下方案博客和存储控制器使用由 BaseController 定义的属性路由约定。</span><span class="sxs-lookup"><span data-stu-id="51b3f-136">For example, in the following scenario Blog and Store controllers are using an attribute route convention that is defined by the BaseController.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. <span data-ttu-id="51b3f-137">自动生成属性路由的路由的名称。</span><span class="sxs-lookup"><span data-stu-id="51b3f-137">Automatically generate route names for attribute routes.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. <span data-ttu-id="51b3f-138">修改路由前缀; 在一个中心位置，然后路由添加到路由表。</span><span class="sxs-lookup"><span data-stu-id="51b3f-138">Modify route prefixes in one central place before the routes get added to the route table.</span></span>
4. <span data-ttu-id="51b3f-139">筛选出你想要查找的属性路由的控制器。</span><span class="sxs-lookup"><span data-stu-id="51b3f-139">Filter out the controllers on which you want the attribute routing to look for.</span></span> <span data-ttu-id="51b3f-140">我们希望很快 3 和 4 上的博客。</span><span class="sxs-lookup"><span data-stu-id="51b3f-140">We hope to blog on 3 and 4 soon.</span></span>

### <a name="facebook-fixes-for-changed-api-surface"></a><span data-ttu-id="51b3f-141">Facebook 修补程序已更改的 API 图面</span><span class="sxs-lookup"><span data-stu-id="51b3f-141">Facebook fixes for changed API surface</span></span>

<span data-ttu-id="51b3f-142">MVC Facebook 包[已断开](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All)由于 Facebook 所做的一些 API 更改。</span><span class="sxs-lookup"><span data-stu-id="51b3f-142">The MVC Facebook package [was broken](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) due to few API changes made by Facebook.</span></span> <span data-ttu-id="51b3f-143">我们还发布了新的 Facebook 程序包 (Microsoft.AspNet.Facebook 1.0.0) 来解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="51b3f-143">We are also releasing a new Facebook package (Microsoft.AspNet.Facebook 1.0.0) to fix these issues.</span></span>

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="51b3f-144">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="51b3f-144">Known Issues and Breaking Changes</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="51b3f-145">到具有 5.2.0 项目基架 MVC/Web API 包导致 5.1.2 打包以一种是在项目中尚不存在</span><span class="sxs-lookup"><span data-stu-id="51b3f-145">Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="51b3f-146">为 ASP.NET MVC 5.2.0 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="51b3f-146">Updating NuGet packages for ASP.NET MVC 5.2.0 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="51b3f-147">它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。</span><span class="sxs-lookup"><span data-stu-id="51b3f-147">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="51b3f-148">因此，ASP.NET 基架将安装以前版本 (例如 5.1.2 Update 2 中) 的所需的包，如果它们尚不在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="51b3f-148">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="51b3f-149">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。</span><span class="sxs-lookup"><span data-stu-id="51b3f-149">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="51b3f-150">如果您使用 ASP.NET 基架 Web API 2.2 或 ASP.NET MVC 5.2 更新你的项目的包后，请确保了一致的 Web API 和 ASP.NET MVC 版本。</span><span class="sxs-lookup"><span data-stu-id="51b3f-150">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a><span data-ttu-id="51b3f-151">Microsoft.jQuery.Unobtrusive.Validation NuGet 包安装失败，原因是找不到 Microsoft.jQuery.Unobtrusive.Validation 的版本兼容到 jQuery 1.4.1</span><span class="sxs-lookup"><span data-stu-id="51b3f-151">Microsoft.jQuery.Unobtrusive.Validation NuGet package installation fails because it is unable to find a version of Microsoft.jQuery.Unobtrusive.Validation compatible to jQuery 1.4.1</span></span>

<span data-ttu-id="51b3f-152">Microsoft.jQuery.Unobtrusive.Validation 需要 jQuery &gt;= 1.8 和 jQuery.Validation &gt;= 1.8。</span><span class="sxs-lookup"><span data-stu-id="51b3f-152">Microsoft.jQuery.Unobtrusive.Validation requires jQuery &gt;=1.8 and jQuery.Validation &gt;=1.8.</span></span> <span data-ttu-id="51b3f-153">But,jQuery.Validation (1.8) 需要 jQuery (&#8805; 1.3.2 &amp; &amp; &#8804; 1.6)。</span><span class="sxs-lookup"><span data-stu-id="51b3f-153">But,jQuery.Validation (1.8) needs jQuery (&#8805; 1.3.2 &amp;&amp; &#8804; 1.6).</span></span> <span data-ttu-id="51b3f-154">因此，当 NuGet 安装在同一时间，JQuery 1.8 和 jQuery.Validation 1.8 时就会失败。</span><span class="sxs-lookup"><span data-stu-id="51b3f-154">Because of this, when NuGet installs the JQuery 1.8 and jQuery.Validation 1.8 at the same time, it fails.</span></span> <span data-ttu-id="51b3f-155">如果出现此问题，则只需更新到 jQuery.Validation 版本&gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1)具有固定的 jQuery cap 首先，您应能够安装Microsoft.jQuery.Unobtrusive.Validation。</span><span class="sxs-lookup"><span data-stu-id="51b3f-155">When you see this issue, you can simply update the version of jQuery.Validation to &gt;= [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) which has the jQuery cap fixed first, you should be able to install Microsoft.jQuery.Unobtrusive.Validation.</span></span>

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a><span data-ttu-id="51b3f-156">Jquery。验证 nuget 包版本 1.13.0 不能识别某些国际电子邮件地址</span><span class="sxs-lookup"><span data-stu-id="51b3f-156">The jquery.Validation nuget package version 1.13.0 does not recognize some international email addresses</span></span>

<span data-ttu-id="51b3f-157">jQuery.Validation nuget 包版本 1.11.1 是可以识别以下有效的电子邮件地址的最后一个已知的版本。</span><span class="sxs-lookup"><span data-stu-id="51b3f-157">jQuery.Validation nuget package version 1.11.1 is the last known version which recognizes following valid email addresses.</span></span> <span data-ttu-id="51b3f-158">任何更高版本中可能不能识别它们。</span><span class="sxs-lookup"><span data-stu-id="51b3f-158">Any later versions might not be able to recognize them.</span></span> <span data-ttu-id="51b3f-159">例如：</span><span class="sxs-lookup"><span data-stu-id="51b3f-159">For example:</span></span>

<span data-ttu-id="51b3f-160">电子邮件地址国际化 (EAI) 标准 (例如， [ &#29992; &#25143; @domain.com ](mailto:&#29992;&#25143;@domain.com))</span><span class="sxs-lookup"><span data-stu-id="51b3f-160">E-Mail Address Internationalization (EAI) standard (e.g., [&#29992;&#25143;@domain.com](mailto:&#29992;&#25143;@domain.com))</span></span>   
 <span data-ttu-id="51b3f-161">EAI + 国际化资源标识符 (Iri) (例如。， [ &#29992; &#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;。&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span><span class="sxs-lookup"><span data-stu-id="51b3f-161">EAI + Internationalized Resource Identifiers (IRIs) (eg., [&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span></span>

<span data-ttu-id="51b3f-162">在报告的问题 [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span><span class="sxs-lookup"><span data-stu-id="51b3f-162">The issue is reported at [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span></span>

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="51b3f-163">语法突出显示的 Visual Studio 2013 中的 Razor 视图</span><span class="sxs-lookup"><span data-stu-id="51b3f-163">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="51b3f-164">如果您更新到 ASP.NET MVC 5.2 而不更新 Visual Studio 2013，你不会获得 Visual Studio 编辑器支持语法突出显示编辑 Razor 视图时。</span><span class="sxs-lookup"><span data-stu-id="51b3f-164">If you update to ASP.NET MVC 5.2 without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="51b3f-165">您需要更新 Visual Studio 2013，若要获取此支持。</span><span class="sxs-lookup"><span data-stu-id="51b3f-165">You will need to update Visual Studio 2013 to get this support.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="51b3f-166">Bug 修复和细微的功能更新</span><span class="sxs-lookup"><span data-stu-id="51b3f-166">Bug Fixes and Minor feature updates</span></span>

<span data-ttu-id="51b3f-167">此版本还包括几个 bug 修复和细微的功能更新。</span><span class="sxs-lookup"><span data-stu-id="51b3f-167">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="51b3f-168">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="51b3f-168">You can find the complete list here:</span></span>

- [<span data-ttu-id="51b3f-169">5.2 包</span><span class="sxs-lookup"><span data-stu-id="51b3f-169">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a><span data-ttu-id="51b3f-170">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="51b3f-170">Microsoft.AspNet.MVC 5.2.2</span></span>

<span data-ttu-id="51b3f-171">此版本不包含在 MVC 中的新功能或 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="51b3f-171">This release doesn't have any new features or bug fixes in MVC.</span></span> <span data-ttu-id="51b3f-172">我们所做[网页中更改](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx)显著的性能改进并随后更新了我们拥有依赖于此新版本的网页的所有依赖包。</span><span class="sxs-lookup"><span data-stu-id="51b3f-172">We made a [change in Web Pages](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) for a significant performance improvement and have subsequently updated all other dependent packages we own to depend on this new version of Web Pages.</span></span>

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a><span data-ttu-id="51b3f-173">ASP.NET MVC 5.2.3、web Beta</span><span class="sxs-lookup"><span data-stu-id="51b3f-173">ASP.NET MVC 5.2.3 Beta</span></span>

<span data-ttu-id="51b3f-174">你可以阅读发行[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51b3f-174">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="51b3f-175">此版本包含仅 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="51b3f-175">This release contains only bug fixes.</span></span> <span data-ttu-id="51b3f-176">可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。</span><span class="sxs-lookup"><span data-stu-id="51b3f-176">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
