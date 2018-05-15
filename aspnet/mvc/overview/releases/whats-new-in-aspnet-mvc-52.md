---
uid: mvc/overview/releases/whats-new-in-aspnet-mvc-52
title: 什么是 ASP.NET MVC 5.2 中的新增功能 |Microsoft 文档
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 97972587-2720-48b4-b158-f35f2e855fbf
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/whats-new-in-aspnet-mvc-52
msc.type: authoredcontent
ms.openlocfilehash: 94f6131fdb86d1694c1f563c5f6806f119c71266
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-mvc-52"></a><span data-ttu-id="23bcb-102">什么是 ASP.NET MVC 5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="23bcb-102">What’s New in ASP.NET MVC 5.2</span></span>
====================
<span data-ttu-id="23bcb-103">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="23bcb-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="23bcb-104">本主题介绍什么是新的 ASP.NET MVC 5.2 [Microsoft.AspNet.MVC 5.2.2](#52)和[ASP.NET MVC 5.2.3 Beta](#mvc523Beta)</span><span class="sxs-lookup"><span data-stu-id="23bcb-104">This topic describes what's new for ASP.NET MVC 5.2, [Microsoft.AspNet.MVC 5.2.2](#52) and [ASP.NET MVC 5.2.3 Beta](#mvc523Beta)</span></span>

- [<span data-ttu-id="23bcb-105">软件要求</span><span class="sxs-lookup"><span data-stu-id="23bcb-105">Software Requirements</span></span>](#softRequire)
- [<span data-ttu-id="23bcb-106">下载</span><span class="sxs-lookup"><span data-stu-id="23bcb-106">Download</span></span>](#download)
- [<span data-ttu-id="23bcb-107">文档</span><span class="sxs-lookup"><span data-stu-id="23bcb-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="23bcb-108">ASP.NET MVC 5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="23bcb-108">New Features in ASP.NET MVC 5.2</span></span>](#new-features)

    - [<span data-ttu-id="23bcb-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="23bcb-109">Attribute routing improvements</span></span>](#attributerouting)
- [<span data-ttu-id="23bcb-110">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="23bcb-110">Known Issues and Breaking Changes</span></span>](#knownbreakingchanges)
- [<span data-ttu-id="23bcb-111">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="23bcb-111">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="23bcb-112">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="23bcb-112">Microsoft.AspNet.MVC 5.2.2</span></span>](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a><span data-ttu-id="23bcb-113">软件要求</span><span class="sxs-lookup"><span data-stu-id="23bcb-113">Software Requirements</span></span>

- <span data-ttu-id="23bcb-114">Visual Studio 2012： 下载[ASP.NET 和 Web Tools for Visual Studio 2012 2013.1](https://go.microsoft.com/fwlink/?LinkId=390062)。</span><span class="sxs-lookup"><span data-stu-id="23bcb-114">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="23bcb-115">Visual Studio 2013： 下载[Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="23bcb-115">Visual Studio 2013: Download [Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064) or higher.</span></span> <span data-ttu-id="23bcb-116">编辑 ASP.NET MVC 5.2 Razor 视图需要此更新。</span><span class="sxs-lookup"><span data-stu-id="23bcb-116">This update is needed for editing ASP.NET MVC 5.2 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="23bcb-117">下载</span><span class="sxs-lookup"><span data-stu-id="23bcb-117">Download</span></span>

<span data-ttu-id="23bcb-118">运行时功能将发布为 NuGet 库上的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="23bcb-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="23bcb-119">所有运行时包按照[语义版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="23bcb-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="23bcb-120">最新的 ASP.NET MVC 5.2 包具有以下版本:"5.2.0"。</span><span class="sxs-lookup"><span data-stu-id="23bcb-120">The latest ASP.NET MVC 5.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="23bcb-121">你可以安装或更新这些包通过[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)。</span><span class="sxs-lookup"><span data-stu-id="23bcb-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="23bcb-122">版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="23bcb-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="23bcb-123">你可以安装或使用 NuGet 程序包管理器控制台更新到已发布的 NuGet 程序包：</span><span class="sxs-lookup"><span data-stu-id="23bcb-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

<span data-ttu-id="23bcb-124">安装包 Microsoft.AspNet.Mvc-Version 5.2.0</span><span class="sxs-lookup"><span data-stu-id="23bcb-124">Install-Package Microsoft.AspNet.Mvc -Version 5.2.0</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="23bcb-125">文档</span><span class="sxs-lookup"><span data-stu-id="23bcb-125">Documentation</span></span>

<span data-ttu-id="23bcb-126">教程和有关 ASP.NET MVC 5.2 的其他信息可以从 ASP.NET web 站点 ([https://www.asp.net/mvc](../../index.md))。</span><span class="sxs-lookup"><span data-stu-id="23bcb-126">Tutorials and other information about ASP.NET MVC 5.2 are available from the ASP.NET web site ([https://www.asp.net/mvc](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a><span data-ttu-id="23bcb-127">ASP.NET MVC 5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="23bcb-127">New Features in ASP.NET MVC 5.2</span></span>

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="23bcb-128">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="23bcb-128">Attribute routing improvements</span></span>

<span data-ttu-id="23bcb-129">现在的属性路由提供调用 IDirectRouteProvider，允许完全控制属性路由如何发现和配置一个扩展点。</span><span class="sxs-lookup"><span data-stu-id="23bcb-129">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="23bcb-130">IDirectRouteProvider 负责提供的操作和以及关联的路由信息以指定哪些路由配置所需的这些操作完全的控制器的列表。</span><span class="sxs-lookup"><span data-stu-id="23bcb-130">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="23bcb-131">调用 MapAttributes/MapHttpAttributeRoutes 时，可能指定 IDirectRouteProvider 实现。</span><span class="sxs-lookup"><span data-stu-id="23bcb-131">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="23bcb-132">自定义 IDirectRouteProvider 是最简单的扩展了默认实现，DefaultDirectRouteProvider。</span><span class="sxs-lookup"><span data-stu-id="23bcb-132">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="23bcb-133">此类提供单独可重写虚拟方法，若要更改用于发现属性、 创建的路由项和发现的路由前缀和区域前缀的逻辑。</span><span class="sxs-lookup"><span data-stu-id="23bcb-133">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="23bcb-134">使用 IDirectRouteProvider 的新属性路由扩展性，用户无法执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="23bcb-134">With the new attribute routing extensibility of IDirectRouteProvider, a user could do the following:</span></span>

1. <span data-ttu-id="23bcb-135">支持属性路由的继承。</span><span class="sxs-lookup"><span data-stu-id="23bcb-135">Support Inheritance of attribute routes.</span></span> <span data-ttu-id="23bcb-136">例如，在以下方案博客和存储控制器中使用由 BaseController 定义的属性路由约定。</span><span class="sxs-lookup"><span data-stu-id="23bcb-136">For example, in the following scenario Blog and Store controllers are using an attribute route convention that is defined by the BaseController.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. <span data-ttu-id="23bcb-137">自动生成属性路由的路由的名称。</span><span class="sxs-lookup"><span data-stu-id="23bcb-137">Automatically generate route names for attribute routes.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. <span data-ttu-id="23bcb-138">先获取将路由添加到路由表，请修改在一个中心位置中的路由前缀。</span><span class="sxs-lookup"><span data-stu-id="23bcb-138">Modify route prefixes in one central place before the routes get added to the route table.</span></span>
4. <span data-ttu-id="23bcb-139">筛选出你想要查找的属性路由的控制器。</span><span class="sxs-lookup"><span data-stu-id="23bcb-139">Filter out the controllers on which you want the attribute routing to look for.</span></span> <span data-ttu-id="23bcb-140">我们希望推出 3 和 4 上的博客。</span><span class="sxs-lookup"><span data-stu-id="23bcb-140">We hope to blog on 3 and 4 soon.</span></span>

### <a name="facebook-fixes-for-changed-api-surface"></a><span data-ttu-id="23bcb-141">Facebook 修补已更改的 API 图面</span><span class="sxs-lookup"><span data-stu-id="23bcb-141">Facebook fixes for changed API surface</span></span>

<span data-ttu-id="23bcb-142">MVC Facebook 包[已断开](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All)由于 Facebook 所做的一些 API 更改。</span><span class="sxs-lookup"><span data-stu-id="23bcb-142">The MVC Facebook package [was broken](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) due to few API changes made by Facebook.</span></span> <span data-ttu-id="23bcb-143">我们即将发布新的 Facebook 包 (Microsoft.AspNet.Facebook 1.0.0) 来解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="23bcb-143">We are also releasing a new Facebook package (Microsoft.AspNet.Facebook 1.0.0) to fix these issues.</span></span>

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="23bcb-144">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="23bcb-144">Known Issues and Breaking Changes</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="23bcb-145">到 5.2.0 与项目的基架 MVC/Web API 包导致 5.1.2 打包以一种是在项目中尚不存在</span><span class="sxs-lookup"><span data-stu-id="23bcb-145">Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="23bcb-146">有关 ASP.NET MVC 5.2.0 更新 NuGet 程序包不会更新 Visual Studio 工具，例如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="23bcb-146">Updating NuGet packages for ASP.NET MVC 5.2.0 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="23bcb-147">它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。</span><span class="sxs-lookup"><span data-stu-id="23bcb-147">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="23bcb-148">因此，ASP.NET 基架将安装所需的包的以前版本 (例如 5.1.2 Update 2 中)，如果它们尚不存在在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="23bcb-148">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="23bcb-149">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖你的项目中的最新包。</span><span class="sxs-lookup"><span data-stu-id="23bcb-149">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="23bcb-150">如果您使用 ASP.NET Web API 2.2 或 ASP.NET MVC 5.2 到更新你的项目的包之后的基架，请确保 Web API 和 ASP.NET MVC 的版本都一致。</span><span class="sxs-lookup"><span data-stu-id="23bcb-150">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a><span data-ttu-id="23bcb-151">Microsoft.jQuery.Unobtrusive.Validation NuGet 软件包安装失败，因为它是找不到 Microsoft.jQuery.Unobtrusive.Validation 的版本兼容 jQuery 1.4.1</span><span class="sxs-lookup"><span data-stu-id="23bcb-151">Microsoft.jQuery.Unobtrusive.Validation NuGet package installation fails because it is unable to find a version of Microsoft.jQuery.Unobtrusive.Validation compatible to jQuery 1.4.1</span></span>

<span data-ttu-id="23bcb-152">Microsoft.jQuery.Unobtrusive.Validation 需要 jQuery &gt;= 1.8 和 jQuery.Validation &gt;= 1.8。</span><span class="sxs-lookup"><span data-stu-id="23bcb-152">Microsoft.jQuery.Unobtrusive.Validation requires jQuery &gt;=1.8 and jQuery.Validation &gt;=1.8.</span></span> <span data-ttu-id="23bcb-153">But,jQuery.Validation (1.8) 需要 jQuery (&#8805; 1.3.2 &amp; &amp; &#8804; 1.6)。</span><span class="sxs-lookup"><span data-stu-id="23bcb-153">But,jQuery.Validation (1.8) needs jQuery (&#8805; 1.3.2 &amp;&amp; &#8804; 1.6).</span></span> <span data-ttu-id="23bcb-154">因此，NuGet 安装一次的 JQuery 1.8 和 jQuery.Validation 1.8 时就会失败。</span><span class="sxs-lookup"><span data-stu-id="23bcb-154">Because of this, when NuGet installs the JQuery 1.8 and jQuery.Validation 1.8 at the same time, it fails.</span></span> <span data-ttu-id="23bcb-155">当你看到此问题时，你可以只需更新的版本到 jQuery.Validation &gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1)具有固定的 jQuery cap 首先，你应能够安装Microsoft.jQuery.Unobtrusive.Validation。</span><span class="sxs-lookup"><span data-stu-id="23bcb-155">When you see this issue, you can simply update the version of jQuery.Validation to &gt;= [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) which has the jQuery cap fixed first, you should be able to install Microsoft.jQuery.Unobtrusive.Validation.</span></span>

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a><span data-ttu-id="23bcb-156">Jquery。验证 nuget 程序包版本 1.13.0 无法识别某些国际电子邮件地址</span><span class="sxs-lookup"><span data-stu-id="23bcb-156">The jquery.Validation nuget package version 1.13.0 does not recognize some international email addresses</span></span>

<span data-ttu-id="23bcb-157">jQuery.Validation nuget 程序包版本 1.11.1 是识别以下有效的电子邮件地址的最后一个已知的版本。</span><span class="sxs-lookup"><span data-stu-id="23bcb-157">jQuery.Validation nuget package version 1.11.1 is the last known version which recognizes following valid email addresses.</span></span> <span data-ttu-id="23bcb-158">任何更高版本可能不能识别它们。</span><span class="sxs-lookup"><span data-stu-id="23bcb-158">Any later versions might not be able to recognize them.</span></span> <span data-ttu-id="23bcb-159">例如: </span><span class="sxs-lookup"><span data-stu-id="23bcb-159">For example:</span></span>

<span data-ttu-id="23bcb-160">电子邮件地址国际化 (EAI) 标准 (例如， [&#29992; &#25143;@domain.com](mailto:&#29992;&#25143;@domain.com))</span><span class="sxs-lookup"><span data-stu-id="23bcb-160">E-Mail Address Internationalization (EAI) standard (e.g., [&#29992;&#25143;@domain.com](mailto:&#29992;&#25143;@domain.com))</span></span>   
 <span data-ttu-id="23bcb-161">EAI + Internationalized 资源标识符 (IRIs) (例如。， [（& a) #29992; &#25143; @&#1076; （& a) #1086; （& a) #1084; &#1077; （& a) #1085;。&#1088; &#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span><span class="sxs-lookup"><span data-stu-id="23bcb-161">EAI + Internationalized Resource Identifiers (IRIs) (eg., [&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span></span>

<span data-ttu-id="23bcb-162">在报告问题[https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span><span class="sxs-lookup"><span data-stu-id="23bcb-162">The issue is reported at [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span></span>

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="23bcb-163">Visual Studio 2013 中的 Razor 视图的语法突出显示</span><span class="sxs-lookup"><span data-stu-id="23bcb-163">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="23bcb-164">如果你更新到 ASP.NET MVC 5.2 而无需更新 Visual Studio 2013，你将获取 Visual Studio 编辑器支持语法突出显示编辑 Razor 视图时。</span><span class="sxs-lookup"><span data-stu-id="23bcb-164">If you update to ASP.NET MVC 5.2 without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="23bcb-165">你将需要更新 Visual Studio 2013，若要获得此支持。</span><span class="sxs-lookup"><span data-stu-id="23bcb-165">You will need to update Visual Studio 2013 to get this support.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="23bcb-166">Bug 修复和细微的功能更新</span><span class="sxs-lookup"><span data-stu-id="23bcb-166">Bug Fixes and Minor feature updates</span></span>

<span data-ttu-id="23bcb-167">此版本还包括几个 bug 修复和细微的功能更新。</span><span class="sxs-lookup"><span data-stu-id="23bcb-167">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="23bcb-168">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="23bcb-168">You can find the complete list here:</span></span>

- [<span data-ttu-id="23bcb-169">5.2 包</span><span class="sxs-lookup"><span data-stu-id="23bcb-169">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a><span data-ttu-id="23bcb-170">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="23bcb-170">Microsoft.AspNet.MVC 5.2.2</span></span>

<span data-ttu-id="23bcb-171">此版本不具有任何新功能或 bug 修复的 MVC。</span><span class="sxs-lookup"><span data-stu-id="23bcb-171">This release doesn't have any new features or bug fixes in MVC.</span></span> <span data-ttu-id="23bcb-172">我们进行了[Web 页中更改](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx)显著的性能改进，并且随后更新我们拥有取决于此新版本的网页的所有其他从属包。</span><span class="sxs-lookup"><span data-stu-id="23bcb-172">We made a [change in Web Pages](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) for a significant performance improvement and have subsequently updated all other dependent packages we own to depend on this new version of Web Pages.</span></span>

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a><span data-ttu-id="23bcb-173">ASP.NET MVC 5.2.3 Beta</span><span class="sxs-lookup"><span data-stu-id="23bcb-173">ASP.NET MVC 5.2.3 Beta</span></span>

<span data-ttu-id="23bcb-174">你可以阅读有关版本[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。</span><span class="sxs-lookup"><span data-stu-id="23bcb-174">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="23bcb-175">此版本包含仅 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="23bcb-175">This release contains only bug fixes.</span></span> <span data-ttu-id="23bcb-176">你可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。</span><span class="sxs-lookup"><span data-stu-id="23bcb-176">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
