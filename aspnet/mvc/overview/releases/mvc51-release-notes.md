---
uid: mvc/overview/releases/mvc51-release-notes
title: 什么是 ASP.NET MVC 5.1 中的新增功能 |Microsoft 文档
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9a83a058-9b01-48aa-acce-ec041e694567
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/mvc51-release-notes
msc.type: authoredcontent
ms.openlocfilehash: be10486c9fd39738f44cdda4fedb409058017601
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="whats-new-in-aspnet-mvc-51"></a><span data-ttu-id="1cf31-102">什么是 ASP.NET MVC 5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="1cf31-102">What's New in ASP.NET MVC 5.1</span></span>
====================
<span data-ttu-id="1cf31-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1cf31-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="1cf31-104">本主题介绍什么是用于 ASP.NET Web MVC 5.1 的新功能。</span><span class="sxs-lookup"><span data-stu-id="1cf31-104">This topic describes what's new for ASP.NET Web MVC 5.1.</span></span>

- [<span data-ttu-id="1cf31-105">软件要求</span><span class="sxs-lookup"><span data-stu-id="1cf31-105">Software Requirements</span></span>](#SoftwareRequirements)
- [<span data-ttu-id="1cf31-106">下载</span><span class="sxs-lookup"><span data-stu-id="1cf31-106">Download</span></span>](#download)
- [<span data-ttu-id="1cf31-107">文档</span><span class="sxs-lookup"><span data-stu-id="1cf31-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="1cf31-108">ASP.NET MVC 5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="1cf31-108">New Features in ASP.NET MVC 5.1</span></span>](#new-features)

    - [<span data-ttu-id="1cf31-109">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="1cf31-109">Attribute routing improvements</span></span>](#AttributeRouting)
    - [<span data-ttu-id="1cf31-110">Bootstrap 支持编辑器模板</span><span class="sxs-lookup"><span data-stu-id="1cf31-110">Bootstrap support for editor templates</span></span>](#Bootstrap)
    - [<span data-ttu-id="1cf31-111">在视图中的枚举支持</span><span class="sxs-lookup"><span data-stu-id="1cf31-111">Enum support in views</span></span>](#Enum)
    - [<span data-ttu-id="1cf31-112">非介入式 MinLength/MaxLength 属性验证</span><span class="sxs-lookup"><span data-stu-id="1cf31-112">Unobtrusive validation for MinLength/MaxLength Attributes</span></span>](#Unobtrusive)
    - [<span data-ttu-id="1cf31-113">支持在非介入式 Ajax 中的 this 上下文</span><span class="sxs-lookup"><span data-stu-id="1cf31-113">Supporting the ‘this' context in Unobtrusive Ajax</span></span>](#thisContext)
- <span data-ttu-id="1cf31-114">[已知问题和重大更改](#KnownBreakingChanges)- [Bug 修复](#bug-fixes)</span><span class="sxs-lookup"><span data-stu-id="1cf31-114">[Known Issues and Breaking Changes](#KnownBreakingChanges)- [Bug Fixes](#bug-fixes)</span></span>

<a id="SoftwareRequirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="1cf31-115">软件要求</span><span class="sxs-lookup"><span data-stu-id="1cf31-115">Software Requirements</span></span>

- <span data-ttu-id="1cf31-116">Visual Studio 2012： 下载[ASP.NET 和 Web Tools for Visual Studio 2012 2013.1](https://go.microsoft.com/fwlink/?LinkId=390062)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-116">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="1cf31-117">Visual Studio 2013： 下载[Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=390064)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-117">Visual Studio 2013: Download [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=390064).</span></span> <span data-ttu-id="1cf31-118">编辑 ASP.NET MVC 5.1 Razor 视图需要此更新。</span><span class="sxs-lookup"><span data-stu-id="1cf31-118">This update is needed for editing ASP.NET MVC 5.1 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="1cf31-119">下载</span><span class="sxs-lookup"><span data-stu-id="1cf31-119">Download</span></span>

<span data-ttu-id="1cf31-120">运行时功能将发布为 NuGet 库上的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1cf31-120">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="1cf31-121">所有运行时包按照[语义版本控制](http://semver.org/)规范。</span><span class="sxs-lookup"><span data-stu-id="1cf31-121">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="1cf31-122">最新的 ASP.NET MVC 5.1 RTM 包具有以下版本:"5.1.2"。</span><span class="sxs-lookup"><span data-stu-id="1cf31-122">The latest ASP.NET MVC 5.1 RTM package has the following version: "5.1.2".</span></span> <span data-ttu-id="1cf31-123">你可以安装或更新这些包通过[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-123">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="1cf31-124">版本还包括在 NuGet 上的相应本地化的包。</span><span class="sxs-lookup"><span data-stu-id="1cf31-124">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="1cf31-125">你可以安装或使用 NuGet 程序包管理器控制台更新到已发布的 NuGet 程序包：</span><span class="sxs-lookup"><span data-stu-id="1cf31-125">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

[!code-console[Main](mvc51-release-notes/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="1cf31-126">文档</span><span class="sxs-lookup"><span data-stu-id="1cf31-126">Documentation</span></span>

<span data-ttu-id="1cf31-127">教程和有关 ASP.NET MVC 5.1 RTM 的其他信息可以从 ASP.NET web 站点 ( https://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-127">Tutorials and other information about ASP.NET MVC 5.1 RTM are available from the ASP.NET web site ( https://www.asp.net).</span></span> 

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-51"></a><span data-ttu-id="1cf31-128">ASP.NET MVC 5.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="1cf31-128">New Features in ASP.NET MVC 5.1</span></span>

<a id="AttributeRouting"></a>

### <a name="attribute-routing-improvements"></a><span data-ttu-id="1cf31-129">属性路由改进</span><span class="sxs-lookup"><span data-stu-id="1cf31-129">Attribute routing improvements</span></span>

 <span data-ttu-id="1cf31-130">基于路由选择路由现在支持约束，启用版本控制和标头的属性。</span><span class="sxs-lookup"><span data-stu-id="1cf31-130">Attribute routing now supports constraints, enabling versioning and header based route selection.</span></span> <span data-ttu-id="1cf31-131">现可通过自定义的属性路由的许多方面`IDirectRouteFactory`接口和`RouteFactoryAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="1cf31-131">Many aspects of attribute routes are now customizable via the `IDirectRouteFactory` interface and `RouteFactoryAttribute` class.</span></span> <span data-ttu-id="1cf31-132">路由前缀现在是可扩展的通过`IRoutePrefix`接口和`RoutePrefixAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="1cf31-132">The route prefix is now extensible via the `IRoutePrefix` interface and `RoutePrefixAttribute` class.</span></span> 

<a id="Enum"></a>

### <a name="enum-support-in-views"></a><span data-ttu-id="1cf31-133">在视图中的枚举支持</span><span class="sxs-lookup"><span data-stu-id="1cf31-133">Enum support in views</span></span>

1. <span data-ttu-id="1cf31-134">新`@Html.EnumDropDownListFor()`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="1cf31-134">New `@Html.EnumDropDownListFor()` helper methods.</span></span> <span data-ttu-id="1cf31-135">这些应使用与大多数表达式的计算结果必须为需要注意的 HTML 帮助器[枚举](https://msdn.microsoft.com/en-us/library/cc138362.aspx)类型或[可以为 Null&lt;T&gt; ](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx)其中`T`是[枚举](https://msdn.microsoft.com/en-us/library/cc138362.aspx)类型。</span><span class="sxs-lookup"><span data-stu-id="1cf31-135">These should be used like most of the HTML helpers with the caveat that the expression must evaluate to an [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) type or a [Nullable&lt;T&gt;](https://msdn.microsoft.com/en-us/library/2cf62fcy.aspx) where `T` is an [enum](https://msdn.microsoft.com/en-us/library/cc138362.aspx) type.</span></span> <span data-ttu-id="1cf31-136">使用`EnumHelper.IsValidForEnumHelper()`检查这些要求。</span><span class="sxs-lookup"><span data-stu-id="1cf31-136">Use `EnumHelper.IsValidForEnumHelper()` to check these requirements.</span></span>
2. <span data-ttu-id="1cf31-137">新`EnumHelper.GetSelectList()`返回方法`IList<SelectListItem>`。</span><span class="sxs-lookup"><span data-stu-id="1cf31-137">New `EnumHelper.GetSelectList()` methods which return an `IList<SelectListItem>`.</span></span> <span data-ttu-id="1cf31-138">这是有用的需要进行操作之前调用，例如，选择列表时`@Html.DropDownListFor()`，当您希望显示的名称或其`@Html.EnumDropDownListFor()`显示。</span><span class="sxs-lookup"><span data-stu-id="1cf31-138">This is useful when you need to manipulate a select list prior to calling, for example, `@Html.DropDownListFor()`, or when you wish to display the names which `@Html.EnumDropDownListFor()` shows.</span></span>

<span data-ttu-id="1cf31-139">下面的代码演示了这些 Api。</span><span class="sxs-lookup"><span data-stu-id="1cf31-139">The following code shows these APIs.</span></span>

[!code-cshtml[Main](mvc51-release-notes/samples/sample2.cshtml)]

<span data-ttu-id="1cf31-140">你可以看到的完整示例[此处](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-140">You can see a complete example [here](https://aspnet.codeplex.com/SourceControl/latest#Samples/MVC/EnumSample/).</span></span>

<a id="Bootstrap"></a>

### <a name="bootstrap-support-for-editor-templates"></a><span data-ttu-id="1cf31-141">Bootstrap 支持编辑器模板</span><span class="sxs-lookup"><span data-stu-id="1cf31-141">Bootstrap support for editor templates</span></span>

<span data-ttu-id="1cf31-142">我们现在允许在中的 HTML 特性中使用传递[EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx)作为[匿名对象](https://msdn.microsoft.com/en-us/library/bb397696.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-142">We now allow passing in HTML attributes in [EditorFor](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(v=vs.100).aspx) as an [anonymous object](https://msdn.microsoft.com/en-us/library/bb397696.aspx).</span></span>

<span data-ttu-id="1cf31-143">例如：</span><span class="sxs-lookup"><span data-stu-id="1cf31-143">For example:</span></span>

[!code-cshtml[Main](mvc51-release-notes/samples/sample3.cshtml)]

<a id="Unobtrusive"></a>

### <a name="unobtrusive-validation-for-minlengthattribute-and-maxlengthattribute"></a><span data-ttu-id="1cf31-144">MinLengthAttribute 和 MaxLengthAttribute 非介入式验证</span><span class="sxs-lookup"><span data-stu-id="1cf31-144">Unobtrusive validation for MinLengthAttribute and MaxLengthAttribute</span></span>

<span data-ttu-id="1cf31-145">只有在为使用修饰属性，现在支持字符串和数组类型的客户端验证[MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx)和[MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="1cf31-145">Client-side validation for string and array types will now be supported for properties decorated with the [MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx) and [MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx) attributes.</span></span>

<a id="thisContext"></a>

### <a name="supporting-the-this-context-in-unobtrusive-ajax"></a><span data-ttu-id="1cf31-146">支持在非介入式 Ajax 中的 this 上下文</span><span class="sxs-lookup"><span data-stu-id="1cf31-146">Supporting the ‘this' context in Unobtrusive Ajax</span></span>

<span data-ttu-id="1cf31-147">回调函数 (`OnBegin, OnComplete, OnFailure, OnSuccess`) 现在能够找到调用元素通过`this`上下文。</span><span class="sxs-lookup"><span data-stu-id="1cf31-147">The callback functions (`OnBegin, OnComplete, OnFailure, OnSuccess`) will now be able to locate the invoking element via the `this` context.</span></span> <span data-ttu-id="1cf31-148">例如：</span><span class="sxs-lookup"><span data-stu-id="1cf31-148">For example:</span></span>

[!code-html[Main](mvc51-release-notes/samples/sample4.html)]

<a id="KnownBreakingChanges"></a>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="1cf31-149">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="1cf31-149">Known Issues and Breaking Changes</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="1cf31-150">属性路由</span><span class="sxs-lookup"><span data-stu-id="1cf31-150">Attribute Routing</span></span>

<span data-ttu-id="1cf31-151">在属性路由匹配项中的多义性现在将报告错误，而不是无需选择第一个匹配项。</span><span class="sxs-lookup"><span data-stu-id="1cf31-151">Ambiguities in attribute routing matches will now report an error rather than choosing the first match.</span></span>

<span data-ttu-id="1cf31-152">属性路由禁止使用`{controller}`参数，并从使用`{action}`路由的参数放置在操作上。</span><span class="sxs-lookup"><span data-stu-id="1cf31-152">Attribute routes are prohibited from using the `{controller}` parameter, and from using the `{action}` parameter on routes placed on actions.</span></span> <span data-ttu-id="1cf31-153">使用这些参数会很有可能导致多义性。</span><span class="sxs-lookup"><span data-stu-id="1cf31-153">Uses of these parameters would very likely lead to ambiguities.</span></span> 

### <a name="scaffolding-mvcweb-api-into-a-project-with-51-packages-results-in-50-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="1cf31-154">到 5.1 包在中使用结果尚不存在项目中的那些 5.0 包项目的基架 MVC/Web API</span><span class="sxs-lookup"><span data-stu-id="1cf31-154">Scaffolding MVC/Web API into a project with 5.1 packages results in 5.0 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="1cf31-155">有关 ASP.NET MVC 5.1 RTM 更新 NuGet 程序包不会更新 Visual Studio 工具，例如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="1cf31-155">Updating NuGet packages for ASP.NET MVC 5.1 RTM does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="1cf31-156">它们使用以前版本的 ASP.NET 运行时包 (5.0.0.0)。</span><span class="sxs-lookup"><span data-stu-id="1cf31-156">They use the previous version of the ASP.NET runtime packages (5.0.0.0).</span></span> <span data-ttu-id="1cf31-157">因此，ASP.NET 基架将安装所需的包的以前版本 (5.0.0.0)，如果它们尚不存在在你项目中可用。</span><span class="sxs-lookup"><span data-stu-id="1cf31-157">As a result, the ASP.NET scaffolding will install the previous version (5.0.0.0) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="1cf31-158">但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖你的项目中的最新包。</span><span class="sxs-lookup"><span data-stu-id="1cf31-158">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="1cf31-159">如果您使用 ASP.NET 后更新你的项目的包到 Web API 2.1 或 ASP.NET MVC 5.1 的基架，请确保 Web API 和 ASP.NET MVC 的版本都一致。</span><span class="sxs-lookup"><span data-stu-id="1cf31-159">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.1 or ASP.NET MVC 5.1, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span> 

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="1cf31-160">Visual Studio 2013 中的 Razor 视图的语法突出显示</span><span class="sxs-lookup"><span data-stu-id="1cf31-160">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="1cf31-161">如果你更新到 ASP.NET MVC 5.1 RTM 而无需更新 Visual Studio 2013，你将获取 Visual Studio 编辑器支持语法突出显示编辑 Razor 视图时。</span><span class="sxs-lookup"><span data-stu-id="1cf31-161">If you update to ASP.NET MVC 5.1 RTM without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="1cf31-162">你将需要更新 Visual Studio 2013，若要获得此支持。</span><span class="sxs-lookup"><span data-stu-id="1cf31-162">You will need to update Visual Studio 2013 to get this support.</span></span> 

### <a name="type-renames"></a><span data-ttu-id="1cf31-163">类型重命名</span><span class="sxs-lookup"><span data-stu-id="1cf31-163">Type Renames</span></span>

<span data-ttu-id="1cf31-164">一些用于属性路由扩展的类型将在 5.1 RTM 中重命名。</span><span class="sxs-lookup"><span data-stu-id="1cf31-164">Some of the types used for attribute routing extensibility are renamed in 5.1 RTM.</span></span>

| <span data-ttu-id="1cf31-165">**旧的类型名称 (5.1 RC)**</span><span class="sxs-lookup"><span data-stu-id="1cf31-165">**Old Type Name (5.1 RC)**</span></span> | <span data-ttu-id="1cf31-166">**新的类型名称 (5.1 RTM)**</span><span class="sxs-lookup"><span data-stu-id="1cf31-166">**New Type Name (5.1 RTM)**</span></span> |
| --- | --- |
| <span data-ttu-id="1cf31-167">IDirectRouteProvider</span><span class="sxs-lookup"><span data-stu-id="1cf31-167">IDirectRouteProvider</span></span> | <span data-ttu-id="1cf31-168">IDirectRouteFactory</span><span class="sxs-lookup"><span data-stu-id="1cf31-168">IDirectRouteFactory</span></span> |
| <span data-ttu-id="1cf31-169">RouteProviderAttribute</span><span class="sxs-lookup"><span data-stu-id="1cf31-169">RouteProviderAttribute</span></span> | <span data-ttu-id="1cf31-170">RouteFactoryAttribute</span><span class="sxs-lookup"><span data-stu-id="1cf31-170">RouteFactoryAttribute</span></span> |
| <span data-ttu-id="1cf31-171">DirectRouteProviderContext</span><span class="sxs-lookup"><span data-stu-id="1cf31-171">DirectRouteProviderContext</span></span> | <span data-ttu-id="1cf31-172">DirectRouteFactoryContext</span><span class="sxs-lookup"><span data-stu-id="1cf31-172">DirectRouteFactoryContext</span></span> |

<a id="bug-fixes"></a>
## <a name="bug-fixes"></a><span data-ttu-id="1cf31-173">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="1cf31-173">Bug Fixes</span></span>

<span data-ttu-id="1cf31-174">此版本还包括多项 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="1cf31-174">This release also includes several bug fixes.</span></span> <span data-ttu-id="1cf31-175">您可以找到完整的列表：</span><span class="sxs-lookup"><span data-stu-id="1cf31-175">You can find the complete list here:</span></span>

- [<span data-ttu-id="1cf31-176">5.1.0 包</span><span class="sxs-lookup"><span data-stu-id="1cf31-176">5.1.0 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.1%20Preview|v5.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)
- [<span data-ttu-id="1cf31-177">5.1.1 包</span><span class="sxs-lookup"><span data-stu-id="1cf31-177">5.1.1 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.1.1%20RTM&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<span data-ttu-id="1cf31-178">5.1.2 包包含 IntelliSense 更新但没有 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="1cf31-178">The 5.1.2 package contains IntelliSense updates but no bug fixes.</span></span>
