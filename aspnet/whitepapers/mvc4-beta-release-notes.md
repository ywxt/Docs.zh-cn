---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 本文档介绍 ASP.NET MVC 4 Beta for Visual Studio 2010 的版本。
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: f1d949ec716ea8cb677c54fe5b07431161c58fbc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826426"
---
<a name="aspnet-mvc-4"></a><span data-ttu-id="16e2d-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="16e2d-103">ASP.NET MVC 4</span></span>
====================
> <span data-ttu-id="16e2d-104">本文档介绍 ASP.NET MVC 4 Beta for Visual Studio 2010 的版本。</span><span class="sxs-lookup"><span data-stu-id="16e2d-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="16e2d-105">这不是最新版本。</span><span class="sxs-lookup"><span data-stu-id="16e2d-105">This is not the most current release.</span></span> <span data-ttu-id="16e2d-106">提供了 ASP.NET MVC 4 RC 发行说明[此处](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>


- [<span data-ttu-id="16e2d-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="16e2d-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="16e2d-108">文档</span><span class="sxs-lookup"><span data-stu-id="16e2d-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="16e2d-109">支持</span><span class="sxs-lookup"><span data-stu-id="16e2d-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="16e2d-110">软件要求</span><span class="sxs-lookup"><span data-stu-id="16e2d-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="16e2d-111">将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="16e2d-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="16e2d-112">ASP.NET MVC 4 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="16e2d-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="16e2d-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="16e2d-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="16e2d-114">ASP.NET 单页面应用程序</span><span class="sxs-lookup"><span data-stu-id="16e2d-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="16e2d-115">默认项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="16e2d-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="16e2d-116">移动项目模板</span><span class="sxs-lookup"><span data-stu-id="16e2d-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="16e2d-117">显示模式</span><span class="sxs-lookup"><span data-stu-id="16e2d-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="16e2d-118">jQuery Mobile，视图切换器和浏览器重写</span><span class="sxs-lookup"><span data-stu-id="16e2d-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="16e2d-119">用于 Visual Studio 中的代码生成方案</span><span class="sxs-lookup"><span data-stu-id="16e2d-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="16e2d-120">任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="16e2d-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="16e2d-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="16e2d-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="16e2d-122">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="16e2d-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="16e2d-123">安装说明</span><span class="sxs-lookup"><span data-stu-id="16e2d-123">Installation Notes</span></span>

<span data-ttu-id="16e2d-124">可以从安装的 Visual Studio 2010 的 ASP.NET MVC 4 Beta [ASP.NET MVC 4 主页](../mvc/mvc4.md)使用 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="16e2d-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="16e2d-125">必须先卸载任何以前安装的 ASP.NET MVC 4 在安装 ASP.NET MVC 4 Beta 之前预览。</span><span class="sxs-lookup"><span data-stu-id="16e2d-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="16e2d-126">此版本不兼容的.NET Framework 4.5 开发者预览版。</span><span class="sxs-lookup"><span data-stu-id="16e2d-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="16e2d-127">安装 ASP.NET MVC 4 Beta 之前，必须先卸载.NET 4.5 开发人员预览版。</span><span class="sxs-lookup"><span data-stu-id="16e2d-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="16e2d-128">ASP.NET MVC 4 可以安装，并且可以运行的同时使用 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="16e2d-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="16e2d-129">文档</span><span class="sxs-lookup"><span data-stu-id="16e2d-129">Documentation</span></span>

<span data-ttu-id="16e2d-130">ASP.NET MVC 的文档位于以下 URL 的 MSDN 网站上有：</span><span class="sxs-lookup"><span data-stu-id="16e2d-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="16e2d-131">教程和其他信息 ASP.NET MVC 是 ASP.NET 网站的 MVC 4 页上提供 ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md))。</span><span class="sxs-lookup"><span data-stu-id="16e2d-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="16e2d-132">支持</span><span class="sxs-lookup"><span data-stu-id="16e2d-132">Support</span></span>

<span data-ttu-id="16e2d-133">这是预览版本并不正式支持。</span><span class="sxs-lookup"><span data-stu-id="16e2d-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="16e2d-134">如果必须使用此版本有关的问题，请将其发布到 ASP.NET MVC 论坛 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))，ASP.NET 社区的成员是经常能够提供非正式的支持。</span><span class="sxs-lookup"><span data-stu-id="16e2d-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="16e2d-135">软件要求</span><span class="sxs-lookup"><span data-stu-id="16e2d-135">Software Requirements</span></span>

<span data-ttu-id="16e2d-136">Visual Studio 的 ASP.NET MVC 4 组件需要 PowerShell 2.0 以及 Service Pack 1 的 Visual Studio 2010 或 Visual Web Developer 学习版 2010 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="16e2d-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="16e2d-137">将 ASP.NET MVC 3 项目升级到 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="16e2d-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="16e2d-138">ASP.NET MVC 4 可以与 ASP.NET MVC 3 并行安装使您灵活地选择何时升级到 ASP.NET MVC 4 的 ASP.NET MVC 3 应用程序在同一计算机上。</span><span class="sxs-lookup"><span data-stu-id="16e2d-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="16e2d-139">若要升级的最简单方法是创建一个新的 ASP.NET MVC 4 项目并复制所有视图、 控制器、 代码和内容都文件从现有的 MVC 3 项目到新项目，然后更新程序集引用在新项目以匹配旧项目。</span><span class="sxs-lookup"><span data-stu-id="16e2d-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="16e2d-140">如果到 MVC 3 项目中的 Web.config 文件进行了更改，必须还将这些更改合并到 MVC 4 项目中的 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="16e2d-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="16e2d-141">若要手动升级到版本 4 现有的 ASP.NET MVC 3 应用程序，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="16e2d-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="16e2d-142">在项目 （还有一个项目，一个视图文件夹中，一个在你的项目中每个区域的 Views 文件夹的根目录中） 中所有 Web.config 文件中，将为每个实例的以下文本：</span><span class="sxs-lookup"><span data-stu-id="16e2d-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="16e2d-143">使用以下相应的文本：</span><span class="sxs-lookup"><span data-stu-id="16e2d-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="16e2d-144">在根 Web.config 文件中，更新*webPages:Version*为"2.0.0.0"的元素，并添加新*PreserveLoginUrl*具有值"true"的密钥：</span><span class="sxs-lookup"><span data-stu-id="16e2d-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="16e2d-145">在解决方案资源管理器中删除对引用*System.Web.Mvc* （它指向版本 3 的 DLL）。</span><span class="sxs-lookup"><span data-stu-id="16e2d-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="16e2d-146">然后添加对的引用*System.Web.Mvc* (v4.0.0.0)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="16e2d-147">具体而言，进行以下更改更新程序集引用。</span><span class="sxs-lookup"><span data-stu-id="16e2d-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="16e2d-148">以下为详细信息：</span><span class="sxs-lookup"><span data-stu-id="16e2d-148">Here are the details:</span></span>

    1. <span data-ttu-id="16e2d-149">在解决方案资源管理器，删除对以下程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="16e2d-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="16e2d-150">*System.Web.Mvc*(v3.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-151">*System.Web.WebPages*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-152">*System.Web.Razor*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="16e2d-155">添加对以下程序集引用：</span><span class="sxs-lookup"><span data-stu-id="16e2d-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="16e2d-156">*System.Web.Mvc*(v4.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-157">*System.Web.WebPages*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-158">*System.Web.Razor*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="16e2d-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="16e2d-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="16e2d-161">在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。</span><span class="sxs-lookup"><span data-stu-id="16e2d-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="16e2d-162">再次右键单击名称，然后选择编辑*ProjectName*.csproj。</span><span class="sxs-lookup"><span data-stu-id="16e2d-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="16e2d-163">找到*ProjectTypeGuids*元素，并替换 {E53F8FEA-EAE0-44A6-8774-FFD645390401} 为 {E3E379DF-F4C6-4180-9B81-6769533ABE47}。</span><span class="sxs-lookup"><span data-stu-id="16e2d-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="16e2d-164">保存所做的更改，关闭您所编辑的项目 (.csproj) 文件，右键单击该项目，然后选择重新加载项目。</span><span class="sxs-lookup"><span data-stu-id="16e2d-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="16e2d-165">如果项目引用任何使用 ASP.NET MVC 的以前版本编译的第三方库，打开根 Web.config 文件并添加以下三种*bindingRedirect*下的元素*配置*部分：</span><span class="sxs-lookup"><span data-stu-id="16e2d-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="16e2d-166">ASP.NET MVC 4 Beta 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="16e2d-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="16e2d-167">本部分介绍已引入的功能在 ASP.NET MVC 4 Beta 版本。</span><span class="sxs-lookup"><span data-stu-id="16e2d-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="16e2d-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="16e2d-168">ASP.NET Web API</span></span>

<span data-ttu-id="16e2d-169">ASP.NET MVC 4 目前包含 ASP.NET Web API、 新框架，用于创建 HTTP 服务可以访问范围广泛的客户端包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="16e2d-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="16e2d-170">ASP.NET Web API 也是用于构建 RESTful 服务的理想平台。</span><span class="sxs-lookup"><span data-stu-id="16e2d-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="16e2d-171">ASP.NET Web API 包括以下功能的支持：</span><span class="sxs-lookup"><span data-stu-id="16e2d-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="16e2d-172">**现代 HTTP 编程模型：** 直接访问和处理 HTTP 请求和响应 Web Api 使用新的、 强类型化的 HTTP 对象模型中。</span><span class="sxs-lookup"><span data-stu-id="16e2d-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="16e2d-173">相同编程模型和 HTTP 管道是对称通过新的 HttpClient 类型在客户端上可用。</span><span class="sxs-lookup"><span data-stu-id="16e2d-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="16e2d-174">**完全支持路由**: Web Api 现在支持整套一直 Web 堆栈，包括路由参数和约束的一部分的路由功能。</span><span class="sxs-lookup"><span data-stu-id="16e2d-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="16e2d-175">此外，映射到操作具有完全支持约定，因此不再需要应用属性，如 [HttpPost] 到您的类和方法。</span><span class="sxs-lookup"><span data-stu-id="16e2d-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="16e2d-176">**内容协商**： 客户端和服务器可以协同工作来确定从 API 返回的数据的正确格式。</span><span class="sxs-lookup"><span data-stu-id="16e2d-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="16e2d-177">我们提供对 XML、 JSON 和窗体 URL 编码格式的默认支持并可以通过添加自己的格式化程序来扩展此支持或甚至替换默认内容协商策略。</span><span class="sxs-lookup"><span data-stu-id="16e2d-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="16e2d-178">**模型绑定和验证：** 模型联编程序提供了简便的方法来从各个组成部分的 HTTP 请求中提取数据并将这些消息部分转换成可由 Web API 操作的.NET 对象。</span><span class="sxs-lookup"><span data-stu-id="16e2d-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="16e2d-179">**筛选器：** Web Api 现在支持筛选器，包括已知的筛选器，例如 [Authorize] 特性。</span><span class="sxs-lookup"><span data-stu-id="16e2d-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="16e2d-180">可以编写并插入自己的筛选器操作、 授权和异常处理。</span><span class="sxs-lookup"><span data-stu-id="16e2d-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="16e2d-181">**在查询撰写：** 通过简单地返回 IQueryable&lt;T&gt;，Web API 将支持通过 OData URL 约定的查询。</span><span class="sxs-lookup"><span data-stu-id="16e2d-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="16e2d-182">**改进了 HTTP 的详细信息的可测试性：** 而不是静态上下文对象中设置 HTTP 详细信息，Web API 操作现在可以处理的 HttpRequestMessage 和 HttpResponseMessage 实例。</span><span class="sxs-lookup"><span data-stu-id="16e2d-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="16e2d-183">这些对象的通用版本也存在以便你可以使用除 HTTP 类型在自定义类型。</span><span class="sxs-lookup"><span data-stu-id="16e2d-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="16e2d-184">**改进了控制反转 (IoC) 通过 DependencyResolver:** Web API 现在使用由 MVC 的依赖关系解析程序实现的服务定位器模式获取的许多不同的功能实例。</span><span class="sxs-lookup"><span data-stu-id="16e2d-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="16e2d-185">**基于代码的配置：** 只有通过代码实现 Web API 配置、 离开 config 文件清理。</span><span class="sxs-lookup"><span data-stu-id="16e2d-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="16e2d-186">**自承载：** Web Api 可以同时仍可使用的路由的所有功能和其他功能的 Web API 托管在自己的进程除 IIS 之外。</span><span class="sxs-lookup"><span data-stu-id="16e2d-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="16e2d-187">有关在 ASP.NET Web API 的更多详细信息，请访问[ https://www.asp.net/web-api ](../web-api/index.md)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="16e2d-188">ASP.NET 单页面应用程序</span><span class="sxs-lookup"><span data-stu-id="16e2d-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="16e2d-189">ASP.NET MVC 4 目前包含用于生成单页面应用程序与使用 JavaScript 和 Web Api 的重要客户端的交互体验的早期预览版。</span><span class="sxs-lookup"><span data-stu-id="16e2d-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="16e2d-190">此支持包括：</span><span class="sxs-lookup"><span data-stu-id="16e2d-190">This support includes:</span></span>

- <span data-ttu-id="16e2d-191">一组更丰富的本地交互使用缓存数据的 JavaScript 库</span><span class="sxs-lookup"><span data-stu-id="16e2d-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="16e2d-192">工作单元和 DAL 支持的其他 Web API 组件</span><span class="sxs-lookup"><span data-stu-id="16e2d-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="16e2d-193">基架，用于快速开始使用一个 MVC 项目模板</span><span class="sxs-lookup"><span data-stu-id="16e2d-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="16e2d-194">在 ASP.NET MVC 4 支持单页面应用程序的详细信息，请访问[ https://www.asp.net/single-page-application ](../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="16e2d-195">默认项目模板的增强功能</span><span class="sxs-lookup"><span data-stu-id="16e2d-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="16e2d-196">已更新用于创建新的 ASP.NET MVC 4 项目模板来创建外观更加现代的网站：</span><span class="sxs-lookup"><span data-stu-id="16e2d-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="16e2d-197">除了修饰性的改进，已改进的新模板中的功能。</span><span class="sxs-lookup"><span data-stu-id="16e2d-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="16e2d-198">该模板采用一种名为自适应呈现妙在桌面浏览器和移动浏览器没有任何自定义项中。</span><span class="sxs-lookup"><span data-stu-id="16e2d-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="16e2d-199">若要查看操作中的自适应呈现，可以使用移动仿真程序，或只是尝试调整大小较小的桌面浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="16e2d-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="16e2d-200">如果浏览器窗口中获取足够小，将更改页的布局。</span><span class="sxs-lookup"><span data-stu-id="16e2d-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="16e2d-201">默认项目模板的另一个增强功能是使用 JavaScript 来提供更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="16e2d-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="16e2d-202">在模板中使用的登录和注册链接是如何使用 jQuery UI 对话框以提供丰富的登录屏幕的示例：</span><span class="sxs-lookup"><span data-stu-id="16e2d-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="16e2d-203">移动项目模板</span><span class="sxs-lookup"><span data-stu-id="16e2d-203">Mobile Project Template</span></span>

<span data-ttu-id="16e2d-204">如果要开始一个新项目并想要创建一个网站，专门用于移动和平板电脑浏览器，可以使用新的移动应用程序项目模板。</span><span class="sxs-lookup"><span data-stu-id="16e2d-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="16e2d-205">这基于 jQuery Mobile 的用于构建触控优化的 UI 的开放源代码库：</span><span class="sxs-lookup"><span data-stu-id="16e2d-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="16e2d-206">此模板包含为 Internet 应用程序模板相同的应用程序结构 （和控制器代码是几乎完全相同），但它是样式使用 jQuery Mobile 外观精美，同时也在基于触控的移动设备上的行为。</span><span class="sxs-lookup"><span data-stu-id="16e2d-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="16e2d-207">若要了解有关如何结构化和样式移动 UI 的详细信息，请参阅[jQuery 移动项目网站](http://jquerymobile.com/)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="16e2d-208">如果已有面向桌面的站点，你想要添加到，移动优化的视图，或如果想要创建一个站点，提供对桌面和移动浏览器以不同的方式应用了样式的视图，可以使用新的显示模式功能。</span><span class="sxs-lookup"><span data-stu-id="16e2d-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="16e2d-209">（请参阅下一节。）</span><span class="sxs-lookup"><span data-stu-id="16e2d-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="16e2d-210">显示模式</span><span class="sxs-lookup"><span data-stu-id="16e2d-210">Display Modes</span></span>

<span data-ttu-id="16e2d-211">新的显示模式功能，可以选择根据发出请求的浏览器视图的应用程序。</span><span class="sxs-lookup"><span data-stu-id="16e2d-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="16e2d-212">例如，如果桌面浏览器主页发送请求，应用程序可能使用 Views\Home\Index.cshtml 模板。</span><span class="sxs-lookup"><span data-stu-id="16e2d-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="16e2d-213">如果在移动浏览器主页发送请求，应用程序可能会返回 Views\Home\Index.mobile.cshtml 模板。</span><span class="sxs-lookup"><span data-stu-id="16e2d-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="16e2d-214">布局和部分也可以为特定浏览器类型重写。</span><span class="sxs-lookup"><span data-stu-id="16e2d-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="16e2d-215">例如：</span><span class="sxs-lookup"><span data-stu-id="16e2d-215">For example:</span></span>

- <span data-ttu-id="16e2d-216">如果你的 views/shared 文件夹包含两\_Layout.cshtml 和\_Layout.mobile.cshtml 模板，默认情况下应用程序将使用\_Layout.mobile.cshtml 期间请求从移动浏览器和\_Layout.cshtml 期间其他请求。</span><span class="sxs-lookup"><span data-stu-id="16e2d-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="16e2d-217">如果文件夹包含两\_MyPartial.cshtml 并\_MyPartial.mobile.cshtml，指令@Html.Partial("\_MyPartial") 将呈现\_MyPartial.mobile.cshtml 期间从移动设备的请求浏览器和\_MyPartial.cshtml 期间其他请求。</span><span class="sxs-lookup"><span data-stu-id="16e2d-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="16e2d-218">如果你想要创建更具体的视图、 布局或其他设备的分部视图，则可以注册一个新*为 DefaultDisplayMode*实例可以指定其名称以使其搜索请求满足特定条件。</span><span class="sxs-lookup"><span data-stu-id="16e2d-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="16e2d-219">例如，可以添加以下代码*应用程序\_启动*要将字符串"iPhone"注册为 Apple iPhone 浏览器发出请求时应用的显示模式的 Global.asax 文件中的方法：</span><span class="sxs-lookup"><span data-stu-id="16e2d-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="16e2d-220">此代码运行，当 Apple iPhone 浏览器发出请求后，你的应用程序将使用 views/shared\\_Layout.iPhone.cshtml 布局 （如果存在）。</span><span class="sxs-lookup"><span data-stu-id="16e2d-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="16e2d-221">jQuery Mobile，视图切换器和浏览器重写</span><span class="sxs-lookup"><span data-stu-id="16e2d-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="16e2d-222">jQuery Mobile 是一个开源库，用于构建触控优化的 web UI。</span><span class="sxs-lookup"><span data-stu-id="16e2d-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="16e2d-223">如果你想要与 ASP.NET MVC 4 应用程序使用 jQuery Mobile，您可以下载并安装一个 NuGet 包，可帮助你开始。</span><span class="sxs-lookup"><span data-stu-id="16e2d-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="16e2d-224">若要从 Visual Studio 包管理器控制台中安装它，请键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="16e2d-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="16e2d-225">这将安装 jQuery Mobile 和一些帮助器文件，其中包括：</span><span class="sxs-lookup"><span data-stu-id="16e2d-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="16e2d-226">Views/Shared/\_Layout.Mobile.cshtml，这是 jQuery 的移动布局。</span><span class="sxs-lookup"><span data-stu-id="16e2d-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="16e2d-227">视图切换器组件，其中包括Views/Shared/\_ViewSwitcher.cshtml 分部视图和 ViewSwitcherController.cs 控制器。</span><span class="sxs-lookup"><span data-stu-id="16e2d-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="16e2d-228">安装包后，运行应用程序中使用移动浏览器 (或等效的如 Firefox[用户代理切换器](http://chrispederick.com/work/user-agent-switcher/)外接程序)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="16e2d-229">你将发现您的页面起来大不相同，因为 jQuery Mobile 处理布局和样式设置。</span><span class="sxs-lookup"><span data-stu-id="16e2d-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="16e2d-230">若要这样做的优点，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="16e2d-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="16e2d-231">创建移动特定视图，重写下所述[显示模式](#_Toc303253810)之前 （例如，创建要为移动浏览器中重写 Views\Home\Index.cshtml Views\Home\Index.mobile.cshtml）。</span><span class="sxs-lookup"><span data-stu-id="16e2d-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="16e2d-232">读取[jQuery Mobile 文档](http://jquerymobile.com/)若要详细了解如何在移动视图中添加触控优化的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="16e2d-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="16e2d-233">移动优化 web pages 的约定将添加其文本是如桌面视图或完整的站点模式，使用户切换到桌面版本的页面的链接。</span><span class="sxs-lookup"><span data-stu-id="16e2d-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="16e2d-234">JQuery.Mobile.MVC 包包括用于执行此操作的视图切换器组件的示例。</span><span class="sxs-lookup"><span data-stu-id="16e2d-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="16e2d-235">在默认 views/shared\\_Layout.Mobile.cshtml 视图中，其页呈现时其外观类似如下：</span><span class="sxs-lookup"><span data-stu-id="16e2d-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="16e2d-236">如果访问者单击链接时，它们被切换到桌面版本的相同页。</span><span class="sxs-lookup"><span data-stu-id="16e2d-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="16e2d-237">因为桌面设备布局将不包括视图切换器，默认情况下，访客不会有一种方法以获取到移动模式。</span><span class="sxs-lookup"><span data-stu-id="16e2d-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="16e2d-238">若要启用此功能，将以下引用添加到 *\_ViewSwitcher*为桌面的布局，只需内*&lt;正文&gt;* 元素：</span><span class="sxs-lookup"><span data-stu-id="16e2d-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="16e2d-239">视图切换器使用称为重写的浏览器的新功能。</span><span class="sxs-lookup"><span data-stu-id="16e2d-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="16e2d-240">此功能允许将请求视为它们传入应用程序之外的其他浏览器 （用户代理） 从他们实际上从。</span><span class="sxs-lookup"><span data-stu-id="16e2d-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="16e2d-241">下表列出了重写的浏览器提供的方法。</span><span class="sxs-lookup"><span data-stu-id="16e2d-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="16e2d-242">重写请求的实际用户代理值使用指定的用户代理。</span><span class="sxs-lookup"><span data-stu-id="16e2d-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="16e2d-243">如果已指定不重写，返回请求的用户代理重写值或将实际用户代理字符串。</span><span class="sxs-lookup"><span data-stu-id="16e2d-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="16e2d-244">返回*HttpBrowserCapabilitiesBase*对应于当前设置为请求的用户代理的实例 （实际或重写）。</span><span class="sxs-lookup"><span data-stu-id="16e2d-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="16e2d-245">可以使用此值来获取属性，如*IsMobileDevice*。</span><span class="sxs-lookup"><span data-stu-id="16e2d-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="16e2d-246">删除当前请求的任何重写的用户代理。</span><span class="sxs-lookup"><span data-stu-id="16e2d-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="16e2d-247">浏览器重写是 ASP.NET MVC 4 的核心功能，即使你不安装 jQuery.Mobile.MVC 包也可用。</span><span class="sxs-lookup"><span data-stu-id="16e2d-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="16e2d-248">但是，它会影响视图、 布局和分部视图选择 — 不会影响依赖于任何其他 ASP.NET 功能*Request.Browser*对象。</span><span class="sxs-lookup"><span data-stu-id="16e2d-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="16e2d-249">默认情况下使用 cookie 存储用户代理重写。</span><span class="sxs-lookup"><span data-stu-id="16e2d-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="16e2d-250">如果你想要存储替代其他位置 （例如，在数据库中），则可以替换默认提供程序 (*BrowserOverrideStores.Current*)。</span><span class="sxs-lookup"><span data-stu-id="16e2d-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="16e2d-251">为此提供程序的文档将可随附于 ASP.NET MVC 的更高版本。</span><span class="sxs-lookup"><span data-stu-id="16e2d-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="16e2d-252">用于 Visual Studio 中的代码生成方案</span><span class="sxs-lookup"><span data-stu-id="16e2d-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="16e2d-253">新的方案功能，Visual Studio 生成基于你可以使用 NuGet 安装的包的特定于解决方案的代码。</span><span class="sxs-lookup"><span data-stu-id="16e2d-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="16e2d-254">食谱 framework 简化开发人员能够编写代码生成插件，还可用于替换内置代码生成器添加区域、 添加控制器和添加视图。</span><span class="sxs-lookup"><span data-stu-id="16e2d-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="16e2d-255">因为作为 NuGet 包部署方案，可以轻松地签入源代码管理并自动与该项目的所有开发人员共享。</span><span class="sxs-lookup"><span data-stu-id="16e2d-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="16e2d-256">它们也是在每个解决方案的基础上提供。</span><span class="sxs-lookup"><span data-stu-id="16e2d-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="16e2d-257">任务支持异步控制器</span><span class="sxs-lookup"><span data-stu-id="16e2d-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="16e2d-258">您现在可以编写异步操作方法的返回类型的对象为 single 方法*任务*或*任务&lt;ActionResult&gt;*。</span><span class="sxs-lookup"><span data-stu-id="16e2d-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="16e2d-259">例如，如果您使用的 Visual C# 5 (或使用[Async CTP](https://msdn.microsoft.com/vstudio/async.aspx))，可以创建异步操作方法，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="16e2d-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="16e2d-260">在前面的操作方法的调用中*newsService.GetHeadlinesAsync*并*sportsService.GetScoresAsync*异步调用，不会阻止线程池中的线程。</span><span class="sxs-lookup"><span data-stu-id="16e2d-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="16e2d-261">返回的异步操作方法*任务*实例还支持超时。</span><span class="sxs-lookup"><span data-stu-id="16e2d-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="16e2d-262">若要使操作方法可取消，添加类型的参数*CancellationToken*到操作方法签名。</span><span class="sxs-lookup"><span data-stu-id="16e2d-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="16e2d-263">下面的示例显示了异步操作方法具有 2500年毫秒的超时并显示*TimedOut*查看到客户端，如果发生超时。</span><span class="sxs-lookup"><span data-stu-id="16e2d-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="16e2d-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="16e2d-264">Azure SDK</span></span>

<span data-ttu-id="16e2d-265">ASP.NET MVC 4 Beta 支持 Windows Azure SDK 1.5 2011 年 9 月的发布。</span><span class="sxs-lookup"><span data-stu-id="16e2d-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="16e2d-266">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="16e2d-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="16e2d-267">**安装 ASP.NET MVC 4 Beta 之后, 在 Visual Studio 2010 Service Pack 1 CSHTML/VBHTML 编辑器中的 CSHTML/VBHTML 编辑器可能会暂停在 cshtml 或 vbhtml 文件中键入代码片段或 JavaScript 后很长时间。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="16e2d-268">仅在有刚刚创建且尚未编译的 ASP.NET MVC 4 应用程序中发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="16e2d-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="16e2d-269">解决方法是以编译该项目的 bin 文件夹中获取程序集。</span><span class="sxs-lookup"><span data-stu-id="16e2d-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="16e2d-270">请注意，是否清理从 bin 文件夹中删除这些程序集的项目时，编辑器问题将会返回。</span><span class="sxs-lookup"><span data-stu-id="16e2d-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="16e2d-271">将在下一版本中更正此问题。</span><span class="sxs-lookup"><span data-stu-id="16e2d-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="16e2d-272">**用于 Visual Studio 11 Beta 的 C# 项目模板包含在 Global.asax.cs 中的不正确的连接字符串。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="16e2d-273">在应用程序中指定的默认连接\_Visual Studio 11 Beta 中创建的项目包含 LocalDB 连接字符串，它包含非转义反斜杠的启动方法 (\)字符。</span><span class="sxs-lookup"><span data-stu-id="16e2d-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="16e2d-274">这会导致连接错误后尝试访问 Entity Framework DbContext，因此会产生 SqlException。</span><span class="sxs-lookup"><span data-stu-id="16e2d-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="16e2d-275">若要更正此问题，转义反斜杠字符在应用中的\_启动 Global.asax.cs 方法，以便它读取，如下所示：</span><span class="sxs-lookup"><span data-stu-id="16e2d-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="16e2d-276">**面向.NET 4.5 的 ASP.NET MVC 4 应用程序将引发 FileLoadException 后尝试访问在.NET 4.0 下运行时的 System.Net.Http.dll 程序集。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="16e2d-277">.NET 4.5 下创建的 ASP.NET MVC 4 应用程序包含一个绑定重定向，将导致 FileLoadException 的它指示"无法加载文件或程序集 System.Net.Http 或其某个依赖项。"</span><span class="sxs-lookup"><span data-stu-id="16e2d-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="16e2d-278">应用程序执行时的系统上安装.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="16e2d-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="16e2d-279">若要更正此问题，请从 web.config 中删除以下绑定重定向：</span><span class="sxs-lookup"><span data-stu-id="16e2d-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="16e2d-280">修改后的 web.config 中的程序集绑定元素应如下所示：</span><span class="sxs-lookup"><span data-stu-id="16e2d-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="16e2d-281"><strong>Visual Basic 项目中的"添加控制器"项模板会生成不正确的命名空间时调用</strong><strong>从某个区域内。</strong></span><span class="sxs-lookup"><span data-stu-id="16e2d-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="16e2d-282">当将控制器添加到使用 Visual Basic 的 ASP.NET MVC 项目中的某个区域中时，项模板会将错误的命名空间插入到控制器。</span><span class="sxs-lookup"><span data-stu-id="16e2d-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="16e2d-283">导航到控制器中的任何操作时，结果将是"找不到文件"错误。</span><span class="sxs-lookup"><span data-stu-id="16e2d-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="16e2d-284">生成的命名空间的根命名空间后省略的所有内容。</span><span class="sxs-lookup"><span data-stu-id="16e2d-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="16e2d-285">例如，生成的命名空间是*RootNamespace*但应该*RootNamespace.Areas.AreaName.Controllers* 。</span><span class="sxs-lookup"><span data-stu-id="16e2d-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="16e2d-286">**Razor 视图引擎中的重大更改。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="16e2d-287">重写 Razor 分析器的一部分，以下类型已从*System.Web.Mvc.Razor*:</span><span class="sxs-lookup"><span data-stu-id="16e2d-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="16e2d-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="16e2d-288">*ModelSpan*</span></span>
    - <span data-ttu-id="16e2d-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="16e2d-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="16e2d-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="16e2d-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="16e2d-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="16e2d-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="16e2d-292">此外已删除以下方法：</span><span class="sxs-lookup"><span data-stu-id="16e2d-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="16e2d-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="16e2d-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="16e2d-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span><span class="sxs-lookup"><span data-stu-id="16e2d-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="16e2d-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="16e2d-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="16e2d-296">**WebMatrix.WebData.dll 包含在 ASP.NET MVC 4 应用程序的 /bin 目录中，它将接管窗体身份验证的 URL。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="16e2d-297">（例如，通过使用添加部署依赖性对话框中时，请选择"ASP.NET Web Pages with Razor 语法"） 将 WebMatrix.WebData.dll 程序集添加到你的应用程序将覆盖为登录/帐户 / 身份验证登录重定向而非 /帐户/登录按预期方式默认 ASP.NET MVC 帐户控制器情况。</span><span class="sxs-lookup"><span data-stu-id="16e2d-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="16e2d-298">若要防止此行为，并使用 web.config 的身份验证部分中已指定的 URL，可以添加名为 PreserveLoginUrl 的 appSetting，并将其设置为 true:</span><span class="sxs-lookup"><span data-stu-id="16e2d-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="16e2d-299">**NuGet 包管理器失败时尝试安装 ASP.NET MVC 4 的并行安装 Visual Studio 2010 和 Visual Web Developer 2010 的安装。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="16e2d-300">若要运行 Visual Studio 2010 和 Visual Web Developer 2010 与 ASP.NET MVC 4 并行必须已安装了这两个版本的 Visual Studio 后安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="16e2d-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="16e2d-301">**如果已卸载系统必备组件卸载 ASP.NET MVC 4 将失败。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="16e2d-302">若要完全卸载 ASP.NET MVC 4you 必须在卸载 Visual Studio 之前卸载 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="16e2d-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="16e2d-303">**运行默认的 Web API 项目中显示了将用户添加使用 RegisterApis 方法，不存在的路由不正确定向的说明。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="16e2d-304">应使用 ASP.NET 路由表的 RegisterRoutes 方法中添加的路由。</span><span class="sxs-lookup"><span data-stu-id="16e2d-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="16e2d-305">**安装 ASP.NET MVC 4 Beta 中断 ASP.NET MVC 3 RTM 应用程序。**</span><span class="sxs-lookup"><span data-stu-id="16e2d-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="16e2d-306">已创建的 ASP.NET MVC 3 应用程序与 RTM 版本 （不使用 ASP.NET MVC 3 Tools Update 发行版） 需要执行以下更改才能使用 ASP.NET MVC 4 Beta 并行。</span><span class="sxs-lookup"><span data-stu-id="16e2d-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="16e2d-307">生成项目而无需进行这些更新结果中的编译错误。</span><span class="sxs-lookup"><span data-stu-id="16e2d-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="16e2d-308">**所需的更新**</span><span class="sxs-lookup"><span data-stu-id="16e2d-308">**Required updates**</span></span>

  1. <span data-ttu-id="16e2d-309">在根 Web.config 文件中，添加一个新*&lt;appSettings&gt;* 具有键的项*webPages:Version*和值*1.0.0.0*。</span><span class="sxs-lookup"><span data-stu-id="16e2d-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="16e2d-310">在解决方案资源管理器，右键单击项目名称，然后选择卸载项目。</span><span class="sxs-lookup"><span data-stu-id="16e2d-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="16e2d-311">再次右键单击名称，然后选择编辑*ProjectName*.csproj。</span><span class="sxs-lookup"><span data-stu-id="16e2d-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="16e2d-312">找到以下程序集引用：</span><span class="sxs-lookup"><span data-stu-id="16e2d-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="16e2d-313">使用以下内容替换它们：</span><span class="sxs-lookup"><span data-stu-id="16e2d-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="16e2d-314">保存所做的更改，关闭了编辑，然后右键单击项目并选择重新加载项目 (.csproj) 文件。</span><span class="sxs-lookup"><span data-stu-id="16e2d-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
