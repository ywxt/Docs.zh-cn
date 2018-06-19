---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET 和 Web Tools for Visual Studio 2013 发行说明 |Microsoft 文档
author: microsoft
description: 本文档介绍 ASP.NET 和 Web Tools for Visual Studio 2013 的版本。
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: e9ddd96f186564834ff6bb2c30cf0ed5444cbf1b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877796"
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="46c1a-103">ASP.NET 和 Web Tools for Visual Studio 2013 发行说明</span><span class="sxs-lookup"><span data-stu-id="46c1a-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>
====================
<span data-ttu-id="46c1a-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="46c1a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="46c1a-105">本文档介绍 ASP.NET 和 Web Tools for Visual Studio 2013 的版本。</span><span class="sxs-lookup"><span data-stu-id="46c1a-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>


## <a name="contents"></a><span data-ttu-id="46c1a-106">内容</span><span class="sxs-lookup"><span data-stu-id="46c1a-106">Contents</span></span>

- [<span data-ttu-id="46c1a-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="46c1a-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="46c1a-108">文档</span><span class="sxs-lookup"><span data-stu-id="46c1a-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="46c1a-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="46c1a-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="46c1a-110">ASP.NET 和 Web Tools for Visual Studio 2013 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="46c1a-111">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="46c1a-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="46c1a-112">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="46c1a-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="46c1a-113">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="46c1a-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="46c1a-114">浏览器链接</span><span class="sxs-lookup"><span data-stu-id="46c1a-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="46c1a-115">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="46c1a-116">Visual Studio 中的 azure App Service Web Apps 支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="46c1a-117">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="46c1a-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="46c1a-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="46c1a-119">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="46c1a-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="46c1a-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="46c1a-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="46c1a-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="46c1a-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="46c1a-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="46c1a-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="46c1a-123">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="46c1a-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="46c1a-124">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="46c1a-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="46c1a-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="46c1a-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="46c1a-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="46c1a-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="46c1a-127">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="46c1a-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="46c1a-128">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="46c1a-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="46c1a-129">安装说明</span><span class="sxs-lookup"><span data-stu-id="46c1a-129">Installation Notes</span></span>

<span data-ttu-id="46c1a-130">ASP.NET 和 Web Tools for Visual Studio 2013 在主安装程序中捆绑在一起，可以下载[此处](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="46c1a-131">文档</span><span class="sxs-lookup"><span data-stu-id="46c1a-131">Documentation</span></span>

<span data-ttu-id="46c1a-132">教程和有关 ASP.NET 和 Web Tools for Visual Studio 2013 的其他信息可以从[ASP.NET 网站](https://www.asp.net/)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="46c1a-133">软件要求</span><span class="sxs-lookup"><span data-stu-id="46c1a-133">Software Requirements</span></span>

<span data-ttu-id="46c1a-134">ASP.NET 和 Web 工具需要 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="46c1a-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="46c1a-135">ASP.NET 和 Web Tools for Visual Studio 2013 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="46c1a-136">以下各节描述了已在版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="46c1a-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="46c1a-137">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="46c1a-137">One ASP.NET</span></span>

<span data-ttu-id="46c1a-138">在 Visual Studio 2013 的版本中，我们已经实现统一的体验，以便可以轻松混合和匹配的选出您希望使用 ASP.NET 技术的步。</span><span class="sxs-lookup"><span data-stu-id="46c1a-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="46c1a-139">例如，你可以启动使用 MVC 的项目和轻松地更高版本，向项目中添加 Web 窗体页或 Web 窗体项目中创建的 Web Api 基架。</span><span class="sxs-lookup"><span data-stu-id="46c1a-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="46c1a-140">一个 ASP.NET 是核心重点更容易地为你作为开发人员如何在 ASP.NET 中喜欢的内容。</span><span class="sxs-lookup"><span data-stu-id="46c1a-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="46c1a-141">无论你选择哪种技术，你可以要在一个 ASP.NET 的受信任基础框架生成的置信度。</span><span class="sxs-lookup"><span data-stu-id="46c1a-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="46c1a-142">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="46c1a-142">New Web Project Experience</span></span>

<span data-ttu-id="46c1a-143">我们已增强，在 Visual Studio 2013 中创建新的 web 项目的体验。</span><span class="sxs-lookup"><span data-stu-id="46c1a-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="46c1a-144">在**新的 ASP.NET Web 项目**对话框，你可以选择想、 配置技术 (Web 窗体，MVC、 Web API) 的任意组合，配置身份验证选项和添加单元测试项目的项目类型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新建 ASP.NET 项目](release-notes/_static/image1.png)

<span data-ttu-id="46c1a-146">新建对话框可以更改模板中的许多的默认身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="46c1a-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="46c1a-147">例如，创建 ASP.NET Web 窗体项目时可以选择任意下列选项：</span><span class="sxs-lookup"><span data-stu-id="46c1a-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="46c1a-148">无身份验证</span><span class="sxs-lookup"><span data-stu-id="46c1a-148">No Authentication</span></span>
- <span data-ttu-id="46c1a-149">单个用户帐户 （ASP.NET 成员资格或社交提供程序登录）</span><span class="sxs-lookup"><span data-stu-id="46c1a-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="46c1a-150">组织帐户 (internet 应用程序中的 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="46c1a-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="46c1a-151">Windows 身份验证 (intranet 应用程序中的 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="46c1a-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![身份验证选项](release-notes/_static/image2.png)

<span data-ttu-id="46c1a-153">有关用于创建 web 项目的新过程的详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="46c1a-154">有关新的身份验证选项的详细信息，请参阅[ASP.NET 标识](#TOC8)本文档后面部分。</span><span class="sxs-lookup"><span data-stu-id="46c1a-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="46c1a-155">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="46c1a-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="46c1a-156">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="46c1a-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="46c1a-157">它可以轻松将样板文件代码添加到您的项目，与数据模型进行交互。</span><span class="sxs-lookup"><span data-stu-id="46c1a-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="46c1a-158">在以前版本的 Visual Studio 中，基架只限于 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="46c1a-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="46c1a-159">使用 Visual Studio 2013，现在可以用于任何 ASP.NET 项目，包括 Web 窗体使用基架。</span><span class="sxs-lookup"><span data-stu-id="46c1a-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="46c1a-160">Visual Studio 2013 当前不支持生成页对于 Web 窗体项目，但你仍可以使用基架，Web 窗体通过向项目添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="46c1a-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="46c1a-161">将在将来更新中添加对生成的 Web 窗体页支持。</span><span class="sxs-lookup"><span data-stu-id="46c1a-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="46c1a-162">在使用基架，我们确保所有必需的项目中安装依赖关系。</span><span class="sxs-lookup"><span data-stu-id="46c1a-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="46c1a-163">例如，如果您首先 ASP.NET Web 窗体项目，然后使用基架添加一个 Web API 控制器，所需的 NuGet 程序包和引用将自动添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="46c1a-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="46c1a-164">若要将 MVC 基架添加到 Web 窗体项目，添加**新建基架项**和选择**MVC 5 依赖项**对话框窗口中。</span><span class="sxs-lookup"><span data-stu-id="46c1a-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="46c1a-165">有两个选项的基架 MVC;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="46c1a-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="46c1a-166">如果你选择最小，只有的 NuGet 包和 ASP.NET MVC 的引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="46c1a-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="46c1a-167">如果选择完整选项，添加最小依赖关系，以及对于 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="46c1a-168">对基架异步控制器支持使用 Entity Framework 6 中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="46c1a-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="46c1a-169">有关详细信息和教程，请参阅[ASP.NET 基架概述](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="46c1a-170">浏览器链接-浏览器和 Visual Studio 之间的 SignalR 通道</span><span class="sxs-lookup"><span data-stu-id="46c1a-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="46c1a-171">新[Browser Link](using-browser-link.md)功能可让你连接到 Visual Studio 的多个浏览器并刷新它们所有通过单击工具栏中的按钮。</span><span class="sxs-lookup"><span data-stu-id="46c1a-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="46c1a-172">可以将多个浏览器连接到开发站点，其中包括移动模拟器，并单击全部在同一时间刷新到刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="46c1a-173">浏览器链接还公开的 API，使开发人员编写 Browser Link 扩展。</span><span class="sxs-lookup"><span data-stu-id="46c1a-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="46c1a-174">通过使开发人员能够利用浏览器链接 API，它将成为可以创建跨边界的 Visual Studio 和任何连接的浏览器之间的非常高级的方案。</span><span class="sxs-lookup"><span data-stu-id="46c1a-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="46c1a-175">Web Essentials 利用 API 创建 Visual Studio 和浏览器的开发人员工具，远程控制移动模拟器和更多操作之间的集成的体验。</span><span class="sxs-lookup"><span data-stu-id="46c1a-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="46c1a-176">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="46c1a-177">Visual Studio 2013 web 应用程序中包括新的 HTML 编辑器中为 Razor 文件和 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="46c1a-178">新的 HTML 编辑器提供了基于 HTML5 的单个统一的架构。</span><span class="sxs-lookup"><span data-stu-id="46c1a-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="46c1a-179">它包含自动括号补全、 jQuery UI 和 AngularJS 特性 IntelliSense，特性 IntelliSense 分组、 ID 和类名 Intellisense、 和其他改进包括更好的性能，格式设置和智能标记。</span><span class="sxs-lookup"><span data-stu-id="46c1a-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="46c1a-180">下面的屏幕截图演示如何使用在 HTML 编辑器中的 Bootstrap 特性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="46c1a-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 编辑器中的 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="46c1a-182">Visual Studio 2013 还附带与这两个 CoffeeScript 和更低的内置的编辑器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="46c1a-183">LESS 编辑器与所有冷的功能来自 CSS 编辑器，而在中的所有更少文档中具有特定 Intellisense 变量和 mixins@import链。</span><span class="sxs-lookup"><span data-stu-id="46c1a-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="46c1a-184">Visual Studio 中的 azure App Service Web Apps 支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="46c1a-185">在 Azure SDK for.NET 2.2 与 Visual Studio 2013，你可以使用**服务器资源管理器**直接与你的远程 web 应用进行交互。</span><span class="sxs-lookup"><span data-stu-id="46c1a-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="46c1a-186">你可以登录到你的 Azure 帐户、 创建新 web 应用、 配置应用、 查看实时日志等等。</span><span class="sxs-lookup"><span data-stu-id="46c1a-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="46c1a-187">SDK 2.2 之后不久即将发布，你将能够在 Azure 中远程调试模式下运行。</span><span class="sxs-lookup"><span data-stu-id="46c1a-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="46c1a-188">当你安装最新版本的 Azure sdk for.NET 时，大部分 Azure App Service Web Apps 的新功能也适用于 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="46c1a-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="46c1a-189">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="46c1a-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="46c1a-190">在 Azure App Service 中创建 ASP.NET web 应用</span><span class="sxs-lookup"><span data-stu-id="46c1a-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="46c1a-191">对 Azure App Service 中使用 Visual Studio 中的 web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="46c1a-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="46c1a-192">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="46c1a-192">Web Publish Enhancements</span></span>

<span data-ttu-id="46c1a-193">Visual Studio 2013 包含的新功能和增强 Web 发布功能。</span><span class="sxs-lookup"><span data-stu-id="46c1a-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="46c1a-194">下面是其中一些：</span><span class="sxs-lookup"><span data-stu-id="46c1a-194">Here are a few of them:</span></span>

- <span data-ttu-id="46c1a-195">轻松[自动执行 Web.config 文件加密](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="46c1a-196">（此链接和以下两个点可能不可用之前在 10/17 当天的后期的 MSDN 上的文档。）</span><span class="sxs-lookup"><span data-stu-id="46c1a-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="46c1a-197">轻松[自动采用应用程序脱机在部署过程中](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="46c1a-198">配置 Web 部署到[而上次更改日期不是使用文件校验和](https://go.microsoft.com/fwlink/?LinkId=325531)用于确定哪些文件应复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="46c1a-199">要使用 FTP 或文件系统发布方法时，以及使用 Web 部署，快速发布单个所选的文件 （包括 Web.config）。</span><span class="sxs-lookup"><span data-stu-id="46c1a-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="46c1a-200">有关 ASP.NET web 部署的详细信息，请参阅[ASP.NET 站点](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="46c1a-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="46c1a-201">NuGet 2.7</span></span>

<span data-ttu-id="46c1a-202">NuGet 2.7 详细的介绍包含一组丰富的新的特征描述了这些[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="46c1a-203">此版本的 NuGet 还会删除，需要为提供明确同意的 NuGet 包还原功能，若要下载包。</span><span class="sxs-lookup"><span data-stu-id="46c1a-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="46c1a-204">现在通过安装 NuGet 授予同意的情况下 （和 NuGet 的首选项对话框中的关联复选框）。</span><span class="sxs-lookup"><span data-stu-id="46c1a-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="46c1a-205">现在程序包还原只需默认的工作方式。</span><span class="sxs-lookup"><span data-stu-id="46c1a-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="46c1a-206">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="46c1a-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="46c1a-207">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="46c1a-207">One ASP.NET</span></span>

<span data-ttu-id="46c1a-208">Web 窗体项目模板与新的一个 ASP.NET 体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="46c1a-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="46c1a-209">你可以添加 MVC 和 Web API 支持为 Web 窗体项目，并且你可以配置身份验证使用一个 ASP.NET 项目创建向导。</span><span class="sxs-lookup"><span data-stu-id="46c1a-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="46c1a-210">有关详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="46c1a-211">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="46c1a-211">ASP.NET Identity</span></span>

<span data-ttu-id="46c1a-212">Web 窗体项目模板支持新的 ASP.NET Identity framework。</span><span class="sxs-lookup"><span data-stu-id="46c1a-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="46c1a-213">此外，模板现在支持创建 Web 窗体 intranet 项目。</span><span class="sxs-lookup"><span data-stu-id="46c1a-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="46c1a-214">有关详细信息，请参阅[身份验证方法](creating-web-projects-in-visual-studio.md#auth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="46c1a-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="46c1a-215">Bootstrap</span></span>

<span data-ttu-id="46c1a-216">Web 窗体模板使用[Bootstrap](http://twitter.github.io/bootstrap/)提供作为时尚且高度可响应外观和感觉，你可以轻松自定义。</span><span class="sxs-lookup"><span data-stu-id="46c1a-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="46c1a-217">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 Bootstrap](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="46c1a-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="46c1a-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="46c1a-219">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="46c1a-219">One ASP.NET</span></span>

<span data-ttu-id="46c1a-220">Web MVC 项目模板与新的一个 ASP.NET 体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="46c1a-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="46c1a-221">可以自定义 MVC 项目，并使用一个 ASP.NET 项目创建向导配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="46c1a-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="46c1a-222">处找不到 ASP.NET MVC 5 的介绍性教程[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="46c1a-223">有关升级到 MVC 5 的 MVC 4 项目的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="46c1a-224">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="46c1a-224">ASP.NET Identity</span></span>

<span data-ttu-id="46c1a-225">MVC 项目模板已更新为使用 ASP.NET 标识进行身份验证和标识管理。</span><span class="sxs-lookup"><span data-stu-id="46c1a-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="46c1a-226">处找不到具有 Facebook 和 Google 身份验证和新的成员资格 API 教程，说明如何[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)和[使用身份验证创建的 ASP.NET MVC 应用程序和SQL 数据库并将其部署到 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="46c1a-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="46c1a-227">Bootstrap</span></span>

<span data-ttu-id="46c1a-228">MVC 项目模板已更新为使用[Bootstrap](http://getbootstrap.com/)提供作为时尚且高度可响应外观和感觉，你可以轻松自定义。</span><span class="sxs-lookup"><span data-stu-id="46c1a-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="46c1a-229">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 Bootstrap](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="46c1a-230">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="46c1a-230">Authentication filters</span></span>

<span data-ttu-id="46c1a-231">身份验证筛选器是一种新的筛选器在 ASP.NET MVC，在 ASP.NET MVC 管道中的授权筛选器之前运行并且使您能够指定身份验证逻辑每个操作，每个控制器或全局范围内的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="46c1a-232">身份验证筛选器处理请求中的凭据，并提供相应的用户权限。</span><span class="sxs-lookup"><span data-stu-id="46c1a-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="46c1a-233">身份验证筛选器还可以添加身份验证质询响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="46c1a-234">筛选器将重写</span><span class="sxs-lookup"><span data-stu-id="46c1a-234">Filter overrides</span></span>

<span data-ttu-id="46c1a-235">现在，你可以重写筛选器应用于给定的操作方法或控制器通过指定一个替代的筛选器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="46c1a-236">重写筛选器指定一的组不应为给定作用域 （操作或控制器） 运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="46c1a-237">这允许您配置执行全局应用，但然后从将应用于特定操作或控制器中排除某些全局筛选器的筛选器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="46c1a-238">属性路由</span><span class="sxs-lookup"><span data-stu-id="46c1a-238">Attribute routing</span></span>

<span data-ttu-id="46c1a-239">ASP.NET MVC 现在支持的属性路由，感谢通过 Tim McCall 的作者贡献[ http://attributerouting.net ](http://attributerouting.net)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="46c1a-240">使用的属性路由可以对你的操作和控制器进行批注来指定路由。</span><span class="sxs-lookup"><span data-stu-id="46c1a-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="46c1a-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="46c1a-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="46c1a-242">属性路由</span><span class="sxs-lookup"><span data-stu-id="46c1a-242">Attribute routing</span></span>

<span data-ttu-id="46c1a-243">ASP.NET Web API 现在支持的属性路由，感谢通过 Tim McCall 的作者贡献[ http://attributerouting.net ](http://attributerouting.net)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="46c1a-244">使用的属性路由，您可以指定 Web API 路由进行批注你的操作和控制器如下：</span><span class="sxs-lookup"><span data-stu-id="46c1a-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="46c1a-245">属性路由可更好地控制 Uri 在你的 web API。</span><span class="sxs-lookup"><span data-stu-id="46c1a-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="46c1a-246">例如，你可以轻松地定义资源层次结构中使用一个 API 控制器：</span><span class="sxs-lookup"><span data-stu-id="46c1a-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="46c1a-247">属性的路由还提供一种方便语法，用于指定可选参数、 默认值和路由约束：</span><span class="sxs-lookup"><span data-stu-id="46c1a-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="46c1a-248">有关的属性路由的详细信息，请参阅[Web API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="46c1a-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="46c1a-249">OAuth 2.0</span></span>

<span data-ttu-id="46c1a-250">Web API 和单页面应用程序项目模板现在支持使用 OAuth 2.0 的授权。</span><span class="sxs-lookup"><span data-stu-id="46c1a-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="46c1a-251">OAuth 2.0 是一个框架，用于授予对受保护资源的客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="46c1a-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="46c1a-252">它适用于各种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="46c1a-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="46c1a-253">OAuth 2.0 的支持取决于新安全中间件持有者身份验证提供的 Microsoft OWIN 组件和实现授权服务器角色。</span><span class="sxs-lookup"><span data-stu-id="46c1a-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="46c1a-254">或者，可以使用组织的授权服务器，如 Azure Active Directory 或 Windows Server 2012 R2 中的 ad FS 授权客户端。</span><span class="sxs-lookup"><span data-stu-id="46c1a-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="46c1a-255">OData 改进</span><span class="sxs-lookup"><span data-stu-id="46c1a-255">OData Improvements</span></span>

<span data-ttu-id="46c1a-256">**支持 $select，$ 展开，$batch 和 $value**</span><span class="sxs-lookup"><span data-stu-id="46c1a-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="46c1a-257">ASP.NET Web API OData 现在有 $select 的完全支持、 $expand、 和 $value。</span><span class="sxs-lookup"><span data-stu-id="46c1a-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="46c1a-258">你可以还 $batch 用于批处理和处理变更集的请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="46c1a-259">$Select 和 $展开选项使您可以更改从 OData 终结点返回的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="46c1a-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="46c1a-260">有关详细信息，请参阅[简介 $select 和 $展开 Web API OData 中的支持](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="46c1a-261">**改进的可扩展性**</span><span class="sxs-lookup"><span data-stu-id="46c1a-261">**Improved extensibility**</span></span>

<span data-ttu-id="46c1a-262">OData 格式化程序现在是可扩展的。</span><span class="sxs-lookup"><span data-stu-id="46c1a-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="46c1a-263">可以添加 Atom 条目元数据、 支持命名的流和媒体链接项、 添加实例批注和自定义链接的生成方式。</span><span class="sxs-lookup"><span data-stu-id="46c1a-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="46c1a-264">**类型的支持**</span><span class="sxs-lookup"><span data-stu-id="46c1a-264">**Type-less support**</span></span>

<span data-ttu-id="46c1a-265">现在可以生成 OData 服务，而无需定义实体类型的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="46c1a-266">相反，你的 OData 控制器可以使用或不返回的实例**IEdmObject**，后者是 OData 格式化程序序列化/反序列化。</span><span class="sxs-lookup"><span data-stu-id="46c1a-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="46c1a-267">**重用现有模型**</span><span class="sxs-lookup"><span data-stu-id="46c1a-267">**Reuse an existing model**</span></span>

<span data-ttu-id="46c1a-268">如果你已有现有的实体数据模型 (EDM)，你可以现在重用它直接，而无需生成一个新。</span><span class="sxs-lookup"><span data-stu-id="46c1a-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="46c1a-269">例如，如果使用实体框架，你可以使用为您建立 EF EDM。</span><span class="sxs-lookup"><span data-stu-id="46c1a-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="46c1a-270">请求批处理</span><span class="sxs-lookup"><span data-stu-id="46c1a-270">Request Batching</span></span>

<span data-ttu-id="46c1a-271">请求批处理将合并到单个 HTTP POST 请求，以减少网络流量，并提供流畅些，小于聊天式用户界面的多个操作。</span><span class="sxs-lookup"><span data-stu-id="46c1a-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="46c1a-272">ASP.NET Web API 现在支持用于请求批处理的几种策略：</span><span class="sxs-lookup"><span data-stu-id="46c1a-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="46c1a-273">使用 OData 服务的 $batch 终结点。</span><span class="sxs-lookup"><span data-stu-id="46c1a-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="46c1a-274">打包成单个多部分 MIME 请求多个请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="46c1a-275">使用自定义批处理格式。</span><span class="sxs-lookup"><span data-stu-id="46c1a-275">Use a custom batching format.</span></span>

<span data-ttu-id="46c1a-276">若要启用批处理的请求，只需将批处理的处理程序的路由添加到你的 Web API 配置：</span><span class="sxs-lookup"><span data-stu-id="46c1a-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="46c1a-277">此外可以控制是否请求或按顺序或按任意顺序执行。</span><span class="sxs-lookup"><span data-stu-id="46c1a-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="46c1a-278">可移植的 ASP.NET Web API 客户端</span><span class="sxs-lookup"><span data-stu-id="46c1a-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="46c1a-279">现在可以使用 ASP.NET Web API 客户端要在 Windows 应用商店和 Windows Phone 8 应用程序之间创建的工作的可移植类库。</span><span class="sxs-lookup"><span data-stu-id="46c1a-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="46c1a-280">你还可以创建可在客户端和服务器之间共享的可移植格式化程序。</span><span class="sxs-lookup"><span data-stu-id="46c1a-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="46c1a-281">改进的可测试性</span><span class="sxs-lookup"><span data-stu-id="46c1a-281">Improved Testability</span></span>

<span data-ttu-id="46c1a-282">Web API 2 使它更容易单元测试你的 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="46c1a-283">只需实例化请求消息和配置，你的 API 控制器，然后调用你想要测试的操作方法。</span><span class="sxs-lookup"><span data-stu-id="46c1a-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="46c1a-284">它很容易模拟**UrlHelper**类，用于执行链接生成的操作方法。</span><span class="sxs-lookup"><span data-stu-id="46c1a-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="46c1a-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="46c1a-285">IHttpActionResult</span></span>

<span data-ttu-id="46c1a-286">现在，可以实现 IHttpActionResult 来封装你 Web API 的操作方法的结果。</span><span class="sxs-lookup"><span data-stu-id="46c1a-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="46c1a-287">从 Web API 操作方法返回 IHttpActionResult 执行由 ASP.NET Web API 运行时来生成结果的响应消息中。</span><span class="sxs-lookup"><span data-stu-id="46c1a-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="46c1a-288">可以从任何 Web API 操作来简化单元返回 IHttpActionResult 测试你的 Web API 实现。</span><span class="sxs-lookup"><span data-stu-id="46c1a-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="46c1a-289">为方便起见多 IHttpActionResult 实现提供在初始状态下包括用于返回特定的状态代码的结果，格式的内容或内容协商响应。</span><span class="sxs-lookup"><span data-stu-id="46c1a-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="46c1a-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="46c1a-290">HttpRequestContext</span></span>

<span data-ttu-id="46c1a-291">新**HttpRequestContext**跟踪限于请求而不是从请求立即可用的任何状态。</span><span class="sxs-lookup"><span data-stu-id="46c1a-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="46c1a-292">例如，你可以使用**HttpRequestContext**获取路由数据，与请求中，客户端证书，关联的主体**UrlHelper**和根虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="46c1a-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="46c1a-293">你可以轻松创建**HttpRequestContext**为单元测试。</span><span class="sxs-lookup"><span data-stu-id="46c1a-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="46c1a-294">因为请求的主体进行流处理请求而不是依靠**Thread.CurrentPrincipal**，Web API 管道中时，主体现在是可用的整个生存期内请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="46c1a-295">CORS</span><span class="sxs-lookup"><span data-stu-id="46c1a-295">CORS</span></span>

<span data-ttu-id="46c1a-296">感谢从 Brock Allen 的另一个良好发布内容，ASP.NET 现在完全支持跨域请求共享 (CORS)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="46c1a-297">浏览器安全阻止到另一个域进行 AJAX 请求 web 页。</span><span class="sxs-lookup"><span data-stu-id="46c1a-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="46c1a-298">[CORS](http://www.w3.org/TR/cors/)是一种 W3C 标准允许放宽同源策略的服务器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="46c1a-299">使用 CORS，服务器可以显式允许某些跨源请求时拒绝其他人。</span><span class="sxs-lookup"><span data-stu-id="46c1a-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="46c1a-300">Web API 2 现在支持 CORS，包括自动处理的预检请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="46c1a-301">有关详细信息，请参阅[ASP.NET Web API 中启用跨域请求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="46c1a-302">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="46c1a-302">Authentication Filters</span></span>

<span data-ttu-id="46c1a-303">身份验证筛选器是一种新的 ASP.NET Web API 管道中的授权筛选器之前运行并且使您能够指定身份验证逻辑每个操作，ASP.NET Web API 中的筛选器的每个控制器或全局范围内的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="46c1a-304">身份验证筛选器处理请求中的凭据，并提供相应的用户权限。</span><span class="sxs-lookup"><span data-stu-id="46c1a-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="46c1a-305">身份验证筛选器还可以添加身份验证质询响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="46c1a-306">筛选器替代</span><span class="sxs-lookup"><span data-stu-id="46c1a-306">Filter Overrides</span></span>

<span data-ttu-id="46c1a-307">现在，你可以重写筛选器应用于给定的操作方法或控制器，通过指定一个替代的筛选器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="46c1a-308">重写筛选器指定一的组不应为给定作用域 （操作或控制器） 运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="46c1a-309">这样，你可以添加全局筛选器，但然后排除一些特定操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="46c1a-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="46c1a-310">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="46c1a-310">OWIN Integration</span></span>

<span data-ttu-id="46c1a-311">ASP.NET Web API 现在完全支持 OWIN，并可以在任何 OWIN 支持主机上运行。</span><span class="sxs-lookup"><span data-stu-id="46c1a-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="46c1a-312">此外包含**HostAuthenticationFilter** ，它提供与 OWIN 身份验证系统的集成。</span><span class="sxs-lookup"><span data-stu-id="46c1a-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="46c1a-313">通过 OWIN 集成，你可以自承载 Web API，在与其他 OWIN 中间件，例如 SignalR 一起过程中。</span><span class="sxs-lookup"><span data-stu-id="46c1a-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="46c1a-314">有关详细信息，请参阅[使用 OWIN 自承载 ASP.NET Web API 来](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="46c1a-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="46c1a-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="46c1a-316">下列各节描述 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="46c1a-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="46c1a-317">基于 OWIN</span><span class="sxs-lookup"><span data-stu-id="46c1a-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="46c1a-318">MapHubs 和 MapConnection 现 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="46c1a-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="46c1a-319">跨域支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="46c1a-320">iOS 和 Android 支持通过 MonoTouch 和 MonoDroid</span><span class="sxs-lookup"><span data-stu-id="46c1a-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="46c1a-321">可移植.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="46c1a-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="46c1a-322">新的自承载的包</span><span class="sxs-lookup"><span data-stu-id="46c1a-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="46c1a-323">向后兼容服务器支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="46c1a-324">删除 server 对.NET 4.0 的支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="46c1a-325">将一条消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="46c1a-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="46c1a-326">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="46c1a-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="46c1a-327">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="46c1a-328">更轻松的单元测试的中心</span><span class="sxs-lookup"><span data-stu-id="46c1a-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="46c1a-329">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="46c1a-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="46c1a-330">有关如何将现有 1.x 项目升级到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.x 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="46c1a-331">基于 OWIN</span><span class="sxs-lookup"><span data-stu-id="46c1a-331">Built on OWIN</span></span>

<span data-ttu-id="46c1a-332">完全上创建 SignalR 2.0 [OWIN （适用于.NET 的打开 Web 接口）](http://owin.org/)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="46c1a-333">此更改使适用于 SignalR 的安装过程更 web 承载和自承载 SignalR 应用程序之间保持一致，但也需要大量的 API 更改此标识。</span><span class="sxs-lookup"><span data-stu-id="46c1a-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="46c1a-334">MapHubs 和 MapConnection 现 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="46c1a-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="46c1a-335">为了与 OWIN 标准兼容，这些方法具有已重命名为`MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="46c1a-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="46c1a-336">`MapSignalR` 调用没有参数将映射所有中心 (作为`MapHubs`在版本 1.x); 如果要都映射单独**PersistentConnection**对象，指定连接类型作为类型参数中，和作为连接的 URL 扩展第一个参数。</span><span class="sxs-lookup"><span data-stu-id="46c1a-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="46c1a-337">`MapSignalR` Owin 启动类中调用方法。</span><span class="sxs-lookup"><span data-stu-id="46c1a-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="46c1a-338">Visual Studio 2013 包含的 Owin 启动类; 的新模板若要使用此模板，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="46c1a-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="46c1a-339">右键单击该项目</span><span class="sxs-lookup"><span data-stu-id="46c1a-339">Right-click on the project</span></span>
2. <span data-ttu-id="46c1a-340">选择**添加**，**新建项...**</span><span class="sxs-lookup"><span data-stu-id="46c1a-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="46c1a-341">选择**Owin 启动类**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="46c1a-342">将新类**Startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="46c1a-343">在**Web 应用程序，** Owin 启动类包含`MapSignalR`方法然后添加到 Owin 的启动过程中的 Web.Config 文件中，应用程序设置节点中使用的项，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46c1a-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="46c1a-344">在**自承载应用程序**，Startup 类传递的类型参数作为`WebApp.Start`方法。</span><span class="sxs-lookup"><span data-stu-id="46c1a-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="46c1a-345">**映射中心和在 SignalR 连接 1.x （从 web 应用程序中的全局应用程序文件）：**</span><span class="sxs-lookup"><span data-stu-id="46c1a-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="46c1a-346">**映射中心和 SignalR 2.0 （从 Owin 启动类文件） 中的连接：**</span><span class="sxs-lookup"><span data-stu-id="46c1a-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="46c1a-347">在**自承载应用程序**，Startup 类传递的类型参数作为`WebApp.Start`方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46c1a-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="46c1a-348">跨域支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-348">Cross-Domain Support</span></span>

<span data-ttu-id="46c1a-349">在 SignalR 1.x，跨域请求已由单个 EnableCrossDomain 标志控制。</span><span class="sxs-lookup"><span data-stu-id="46c1a-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="46c1a-350">此标志控制 JSONP 和 CORS 请求。</span><span class="sxs-lookup"><span data-stu-id="46c1a-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="46c1a-351">所有 CORS 都支持更大的灵活性，已从 SignalR 的服务器组件 （JavaScript lients 仍使用 CORS 通常如果检测到由浏览器支持它），和新的 OWIN 中间件已可用于都支持这些方案。</span><span class="sxs-lookup"><span data-stu-id="46c1a-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript lients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="46c1a-352">在 SignalR 2.0 中，如果 JSONP 客户端上 （支持需要跨域请求在较旧的浏览器中），它将需要通过设置显式启用`EnableJSONP`上`HubConfiguration`对象传递给`true`，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46c1a-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="46c1a-353">JSONP 已禁用默认情况下，因为它比 CORS 不太安全。</span><span class="sxs-lookup"><span data-stu-id="46c1a-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="46c1a-354">若要添加新的 CORS 中间件 SignalR 2.0 中，添加`Microsoft.Owin.Cors`库连接到你的项目，然后调用`UseCors`之前 SignalR 中间件，如下面的部分中所示。</span><span class="sxs-lookup"><span data-stu-id="46c1a-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="46c1a-355">**向项目中添加 Microsoft.Owin.Cors**： 若要安装此库，包管理器控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="46c1a-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="46c1a-356">此命令将添加 2.0.0 到你的项目的包版本。</span><span class="sxs-lookup"><span data-stu-id="46c1a-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="46c1a-357">**调用 UseCors**</span><span class="sxs-lookup"><span data-stu-id="46c1a-357">**Calling UseCors**</span></span>

<span data-ttu-id="46c1a-358">以下代码段演示如何在 SignalR 中实现跨域连接 1.x 和 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="46c1a-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="46c1a-359">**在 SignalR 中实现跨域请求 1.x （从全局应用程序文件中）**</span><span class="sxs-lookup"><span data-stu-id="46c1a-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="46c1a-360">**在 SignalR 2.0 （来自 C# 代码文件） 中实现跨域请求**</span><span class="sxs-lookup"><span data-stu-id="46c1a-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="46c1a-361">下面的代码演示如何在 SignalR 2.0 项目中启用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="46c1a-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="46c1a-362">此代码示例使用`Map`和`RunSignalR`而不是`MapSignalR`，以便 CORS 中间件运行仅对于需要 CORS 支持 SignalR 请求 (而不是对在指定的路径上的所有流量`MapSignalR`。)`Map`还用于运行特定的 URL 前缀，而不是整个应用程序所需要的任何其他中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="46c1a-363">iOS 和 Android 支持通过 MonoTouch 和 MonoDroid</span><span class="sxs-lookup"><span data-stu-id="46c1a-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="46c1a-364">已为 iOS 和 Android 客户端都使用 MonoTouch 和 MonoDroid 组件添加支持[Xamarin 库](https://xamarin.com/)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="46c1a-365">有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="46c1a-366">这些组件可在[Xamarin 应用商店](https://store.xamarin.com/)SignalR RTW 版本时可用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a> <span data-ttu-id="46c1a-367"># # # 可移植.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="46c1a-367">### Portable .NET client</span></span>

<span data-ttu-id="46c1a-368">更好地便于实现跨平台开发、 Silverlight、 WinRT 并 Windows Phone 客户端已替换为单个可移植.NET 客户端支持以下平台：</span><span class="sxs-lookup"><span data-stu-id="46c1a-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="46c1a-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="46c1a-369">NET 4.5</span></span>
- <span data-ttu-id="46c1a-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="46c1a-370">Silverlight 5</span></span>
- <span data-ttu-id="46c1a-371">WinRT (Windows 应用商店应用的.NET)</span><span class="sxs-lookup"><span data-stu-id="46c1a-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="46c1a-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="46c1a-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="46c1a-373">新的自承载的包</span><span class="sxs-lookup"><span data-stu-id="46c1a-373">New Self-Host Package</span></span>

<span data-ttu-id="46c1a-374">现在有了 NuGet 包，以使其更轻松地开始使用 SignalR 自承载 （的进程中承载的 SignalR 应用程序或其他应用程序，而非托管的 web 服务器中）。</span><span class="sxs-lookup"><span data-stu-id="46c1a-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="46c1a-375">若要升级使用 SignalR 构建的自承载项目 1.x，删除 Microsoft.AspNet.SignalR.Owin 包，并添加 Microsoft.AspNet.SignalR.SelfHost 包。</span><span class="sxs-lookup"><span data-stu-id="46c1a-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="46c1a-376">有关如何开始使用的自承载的包的详细信息，请参阅[教程： 自承载的 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="46c1a-377">向后兼容服务器支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-377">Backward-compatible server support</span></span>

<span data-ttu-id="46c1a-378">在以前版本的 SignalR，需要进行相同的服务器和使用在客户端的 SignalR 包的版本。</span><span class="sxs-lookup"><span data-stu-id="46c1a-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="46c1a-379">为了支持粗客户端应用程序将会很难更新，SignalR 2.0 现在支持使用旧版客户端的较新的服务器版本。</span><span class="sxs-lookup"><span data-stu-id="46c1a-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="46c1a-380">**注意： SignalR 2.0 不支持与较新的客户端生成较旧版本的服务器。**</span><span class="sxs-lookup"><span data-stu-id="46c1a-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="46c1a-381">删除 server 对.NET 4.0 的支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="46c1a-382">SignalR 2.0 已删除，对与.NET 4.0 的服务器互操作性的支持。</span><span class="sxs-lookup"><span data-stu-id="46c1a-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="46c1a-383">与 SignalR 2.0 服务器，必须使用.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="46c1a-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="46c1a-384">仍是 SignalR 2.0 的.NET 4.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="46c1a-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="46c1a-385">将一条消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="46c1a-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="46c1a-386">在 SignalR 2.0 中，则可以使用客户端和组 Id 的列表发送邮件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="46c1a-387">下面的代码段演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="46c1a-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="46c1a-388">**将一条消息发送到客户端和使用 PersistentConnection 组的列表**</span><span class="sxs-lookup"><span data-stu-id="46c1a-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="46c1a-389">**将一条消息发送到客户端和使用中心的组的列表**</span><span class="sxs-lookup"><span data-stu-id="46c1a-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="46c1a-390">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="46c1a-390">Sending a message to a specific user</span></span>

<span data-ttu-id="46c1a-391">此功能允许用户指定用户 Id 是基于通过新接口 IUserIdProvider IRequest:</span><span class="sxs-lookup"><span data-stu-id="46c1a-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="46c1a-392">**IUserIdProvider 接口**</span><span class="sxs-lookup"><span data-stu-id="46c1a-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="46c1a-393">默认情况下将使用作为用户名的用户的 IPrincipal.Identity.Name 的实现。</span><span class="sxs-lookup"><span data-stu-id="46c1a-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="46c1a-394">在中心，你将能够将消息发送到一个新的 API 通过这些用户：</span><span class="sxs-lookup"><span data-stu-id="46c1a-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="46c1a-395">**使用 Clients.User API**</span><span class="sxs-lookup"><span data-stu-id="46c1a-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="46c1a-396">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="46c1a-396">Better Error Handling Support</span></span>

<span data-ttu-id="46c1a-397">用户可以立即引发**HubException**从任何中心调用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="46c1a-398">构造函数**HubException**可以采用字符串消息和一个对象额外的错误数据。</span><span class="sxs-lookup"><span data-stu-id="46c1a-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="46c1a-399">SignalR 将自动序列化异常，并将其发送到客户端，它将用于拒绝/失败中心方法调用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="46c1a-400">**显示详细的中心异常**设置没有任何影响**HubException**发送回客户端或不; 它始终发送。</span><span class="sxs-lookup"><span data-stu-id="46c1a-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="46c1a-401">**演示将 HubException 发送到客户端的服务器端代码**</span><span class="sxs-lookup"><span data-stu-id="46c1a-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="46c1a-402">**演示对从服务器发送 HubException 作出响应的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="46c1a-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="46c1a-403">**演示对从服务器发送 HubException 作出响应的.NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="46c1a-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="46c1a-404">更轻松的单元测试的中心</span><span class="sxs-lookup"><span data-stu-id="46c1a-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="46c1a-405">SignalR 2.0 包括一个接口，称为`IHubCallerConnectionContext`上轻松地创建端调用的模拟客户端的中心。</span><span class="sxs-lookup"><span data-stu-id="46c1a-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="46c1a-406">下面的代码段演示如何使用常用的测试工具使用此接口[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="46c1a-407">**使用单元测试 SignalR xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="46c1a-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="46c1a-408">**使用单元测试 SignalR moq**</span><span class="sxs-lookup"><span data-stu-id="46c1a-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="46c1a-409">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="46c1a-409">JavaScript error handling</span></span>

<span data-ttu-id="46c1a-410">在 SignalR 2.0 中，所有 JavaScript 错误处理回调都返回而不是原始字符串的 JavaScript 错误对象。</span><span class="sxs-lookup"><span data-stu-id="46c1a-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="46c1a-411">这允许 SignalR 流动到错误处理程序更加丰富的信息。</span><span class="sxs-lookup"><span data-stu-id="46c1a-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="46c1a-412">你可以从内部异常`source`的错误的属性。</span><span class="sxs-lookup"><span data-stu-id="46c1a-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="46c1a-413">**处理 Start.Fail 异常的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="46c1a-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="46c1a-414">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="46c1a-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="46c1a-415">新的 ASP.NET 成员资格系统</span><span class="sxs-lookup"><span data-stu-id="46c1a-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="46c1a-416">ASP.NET 标识是为 ASP.NET 应用程序的新成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="46c1a-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="46c1a-417">ASP.NET 标识容易地将特定于用户的配置文件的数据集成与应用程序数据。</span><span class="sxs-lookup"><span data-stu-id="46c1a-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="46c1a-418">ASP.NET 标识还可选择你的应用程序中的用户配置文件的持久性模型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="46c1a-419">你可以将数据存储在 SQL Server 数据库或其他数据存储，包括 Azure 存储表等 NoSQL 数据存储区。</span><span class="sxs-lookup"><span data-stu-id="46c1a-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="46c1a-420">有关详细信息，请参阅[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="46c1a-421">基于声明的身份验证</span><span class="sxs-lookup"><span data-stu-id="46c1a-421">Claims-based authentication</span></span>

<span data-ttu-id="46c1a-422">ASP.NET 现在支持基于声明的身份验证，其中用户的标识表示为一组从受信任的颁发者的声明。</span><span class="sxs-lookup"><span data-stu-id="46c1a-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="46c1a-423">用户可以是经过身份验证的使用用户名和密码在应用程序数据库中维护或使用社交标识提供程序 (例如： Microsoft 帐户、 Facebook、 Google、 Twitter)，或使用通过 Azure Active Directory 的组织帐户或Active Directory 联合身份验证服务 (ADFS)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="46c1a-424">与 Azure Active Directory 和 Windows Server Active Directory 集成</span><span class="sxs-lookup"><span data-stu-id="46c1a-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="46c1a-425">你现在可以创建使用 Azure Active Directory 或 Windows Server Active Directory (AD) 进行身份验证的 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="46c1a-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="46c1a-426">有关详细信息，请参阅[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="46c1a-427">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="46c1a-427">OWIN Integration</span></span>

<span data-ttu-id="46c1a-428">ASP.NET 身份验证现在基于可在任何基于 OWIN 的主机的 OWIN 中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="46c1a-429">有关 OWIN 的详细信息，请参阅以下[Microsoft OWIN 组件](#TOC7)部分。</span><span class="sxs-lookup"><span data-stu-id="46c1a-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="46c1a-430">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="46c1a-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="46c1a-431">[打开针对.NET 的 Web 界面](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="46c1a-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="46c1a-432">OWIN 将脱耦 web 应用程序在服务器上，使 web 应用程序主机无关。</span><span class="sxs-lookup"><span data-stu-id="46c1a-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="46c1a-433">例如，你可以托管在 IIS 中基于 OWIN 的 web 应用程序或自承载服务中自定义过程。</span><span class="sxs-lookup"><span data-stu-id="46c1a-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="46c1a-434">Microsoft OWIN 组件 （也称为 Katana 项目） 中引入的更改包括新的服务器和主机组件、 新的帮助程序库和中间件和新的身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="46c1a-435">有关 OWIN 和 Katana 的详细信息，请参阅[OWIN 和 Katana 中的新增](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="46c1a-436">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序无法在 IIS 经典模式下运行; 必须在集成模式中运行时。**</span><span class="sxs-lookup"><span data-stu-id="46c1a-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="46c1a-437">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序必须运行在完全信任。**</span><span class="sxs-lookup"><span data-stu-id="46c1a-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="46c1a-438">新的服务器和主机</span><span class="sxs-lookup"><span data-stu-id="46c1a-438">New Servers and Hosts</span></span>

<span data-ttu-id="46c1a-439">此版本中，添加了新组件以启用自承载方案。</span><span class="sxs-lookup"><span data-stu-id="46c1a-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="46c1a-440">这些组件包括以下 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="46c1a-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="46c1a-441">**Microsoft.Owin.Host.HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="46c1a-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="46c1a-442">提供使用 OWIN 服务器**HttpListener**以侦听 HTTP 请求并将它们定向到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="46c1a-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="46c1a-443">**Microsoft.Owin.Hosting**适用于想要自承载于自定义过程中，如控制台应用程序或 Windows 服务的一个 OWIN 管道开发人员提供了一个库。</span><span class="sxs-lookup"><span data-stu-id="46c1a-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="46c1a-444">**OwinHost**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-444">**OwinHost**.</span></span> <span data-ttu-id="46c1a-445">提供独立的可执行文件，用于包装`Microsoft.Owin.Hosting`，可以在自承载 OWIN 管道，而无需编写自定义主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="46c1a-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="46c1a-446">此外，`Microsoft.Owin.Host.SystemWeb`包现在可让中间件来提供对提示**SystemWeb**服务器，它指示应在特定的 ASP.NET 管道阶段调用中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="46c1a-447">此功能很适合用于身份验证中间件，应尽早在 ASP.NET 管道中运行。</span><span class="sxs-lookup"><span data-stu-id="46c1a-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="46c1a-448">帮助程序库和中间件</span><span class="sxs-lookup"><span data-stu-id="46c1a-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="46c1a-449">尽管您可以编写 OWIN 组件使用仅中的函数和类型定义 OWIN 规范中，新`Microsoft.Owin`包提供了抽象更加友好的用户组。</span><span class="sxs-lookup"><span data-stu-id="46c1a-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="46c1a-450">此产品包结合了多个更早版本的包 (例如， `Owin.Extensions`， `Owin.Types`) 到单一、 明确的结构化对象模型，然后可以由其他 OWIN 组件轻松地使用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="46c1a-451">事实上，Microsoft OWIN 组件的大部分现在使用此包。</span><span class="sxs-lookup"><span data-stu-id="46c1a-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="46c1a-452">[OWIN](http://www.owin.org)应用程序无法在 IIS 经典模式下运行; 必须在集成模式中运行时。</span><span class="sxs-lookup"><span data-stu-id="46c1a-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="46c1a-453">[OWIN](http://www.owin.org)应用程序必须运行在完全信任。</span><span class="sxs-lookup"><span data-stu-id="46c1a-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="46c1a-454">此版本还包括 Microsoft.Owin.Diagnostics 程序包，其中包括中间件验证正在运行的 OWIN 应用程序，以及有助于调查失败的错误页中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="46c1a-455">身份验证组件</span><span class="sxs-lookup"><span data-stu-id="46c1a-455">Authentication Components</span></span>

<span data-ttu-id="46c1a-456">以下的身份验证组件可用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-456">The following authentication components are available.</span></span>

- <span data-ttu-id="46c1a-457">**Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="46c1a-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="46c1a-458">启用使用本地或基于云的目录服务的身份验证。</span><span class="sxs-lookup"><span data-stu-id="46c1a-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="46c1a-459">**Microsoft.Owin.Security.Cookies**启用身份验证使用 cookie。</span><span class="sxs-lookup"><span data-stu-id="46c1a-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="46c1a-460">此包之前名为`Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="46c1a-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="46c1a-461">**Microsoft.Owin.Security.Facebook**启用身份验证使用 Facebook 的基于 OAuth 的服务。</span><span class="sxs-lookup"><span data-stu-id="46c1a-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="46c1a-462">**Microsoft.Owin.Security.Google**启用身份验证使用 Google 的基于 OpenID 的服务。</span><span class="sxs-lookup"><span data-stu-id="46c1a-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="46c1a-463">**Microsoft.Owin.Security.Jwt**启用身份验证使用 JWT 令牌。</span><span class="sxs-lookup"><span data-stu-id="46c1a-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="46c1a-464">**Microsoft.Owin.Security.MicrosoftAccount**启用身份验证使用 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="46c1a-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="46c1a-465">**Microsoft.Owin.Security.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="46c1a-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="46c1a-466">提供对持有者令牌进行身份验证的 OAuth 授权服务器以及中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="46c1a-467">**Microsoft.Owin.Security.Twitter**启用身份验证使用 Twitter 的基于 OAuth 的服务。</span><span class="sxs-lookup"><span data-stu-id="46c1a-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="46c1a-468">此版本还包括`Microsoft.Owin.Cors`包，其中包含用于处理跨域 HTTP 请求的中间件。</span><span class="sxs-lookup"><span data-stu-id="46c1a-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="46c1a-469">在 Visual Studio 2013 的最终版本中删除了为 JWT 签名的支持。</span><span class="sxs-lookup"><span data-stu-id="46c1a-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="46c1a-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="46c1a-470">Entity Framework 6</span></span>

<span data-ttu-id="46c1a-471">有关新功能和 Entity Framework 6 中的其他更改的列表，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="46c1a-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="46c1a-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="46c1a-473">ASP.NET Razor 3 包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="46c1a-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="46c1a-474">支持选项卡上编辑。</span><span class="sxs-lookup"><span data-stu-id="46c1a-474">Support for Tab editing.</span></span> <span data-ttu-id="46c1a-475">Preivously，**格式文档**命令、 自动缩进，并自动在 Visual Studio 中设置格式未正常工作时使用**保留选项卡**选项。</span><span class="sxs-lookup"><span data-stu-id="46c1a-475">Preivously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="46c1a-476">此更改将更正的格式设置的选项卡的 Razor 代码格式设置的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="46c1a-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="46c1a-477">对 URL 重写规则生成的链接时的支持。</span><span class="sxs-lookup"><span data-stu-id="46c1a-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="46c1a-478">删除的安全透明特性。</span><span class="sxs-lookup"><span data-stu-id="46c1a-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="46c1a-479">这是一项重大更改，并使 Razor 3 不兼容与 MVC4 及更早版本，而 Razor 2 与 MVC5 或针对 MVC5 编译的程序集不兼容。</span><span class="sxs-lookup"><span data-stu-id="46c1a-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="46c1a-480">找不到 Visual Studio 2013 中已修复从预发行版本的 razor 3 问题[此处](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="46c1a-481">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="46c1a-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="46c1a-482">ASP.NET 应用挂起是从根本上更改的用户体验和经济的承载大量的一台计算机上的 ASP.NET 站点模型的.NET Framework 4.5.1 中的改变游戏规则的功能。</span><span class="sxs-lookup"><span data-stu-id="46c1a-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="46c1a-483">有关详细信息，请参阅[.NET web 承载的 ASP.NET 应用挂起 – 响应共享](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="46c1a-484">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="46c1a-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="46c1a-485">本节介绍用于 Visual Studio 2013 的已知的问题和 ASP.NET 和 Web Tools 中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="46c1a-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="46c1a-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="46c1a-486">NuGet</span></span>

- <span data-ttu-id="46c1a-487">[使用 SLN 文件时，新的程序包还原不能在 Mono](https://nuget.codeplex.com/workitem/3596) – 将在即将到来的 nuget.exe 下载中修复和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新。</span><span class="sxs-lookup"><span data-stu-id="46c1a-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="46c1a-488">[新的程序包还原不能使用 Wix 项目](https://nuget.codeplex.com/workitem/3598)– 将在即将到来的 nuget.exe 下载中修复和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新。</span><span class="sxs-lookup"><span data-stu-id="46c1a-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="46c1a-489">[自动包还原不起作用的解决方案文件夹下的项目](https://nuget.codeplex.com/workitem/3625)– 将在 NuGet 2.8 中修复。</span><span class="sxs-lookup"><span data-stu-id="46c1a-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="46c1a-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="46c1a-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="46c1a-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` 不返回`IQueryable<T>`如我们增加了对支持始终`$select`和`$expand`。</span><span class="sxs-lookup"><span data-stu-id="46c1a-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="46c1a-492">我们前面的示例为`ODataQueryOptions<T>`始终强制转换的返回值从`ApplyTo`到`IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="46c1a-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="46c1a-493">此查询选项，因为以前工作正常我们前面要支持 (`$filter`， `$orderby`， `$skip`， `$top`) 不会更改查询的形状。</span><span class="sxs-lookup"><span data-stu-id="46c1a-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="46c1a-494">现在，我们支持`$select`和`$expand`中的返回值`ApplyTo`将不会`IQueryable<T>`始终。</span><span class="sxs-lookup"><span data-stu-id="46c1a-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="46c1a-495">如果你使用的从前面的示例代码，它将继续工作，如果客户端不会发送`$select`和`$expand`。</span><span class="sxs-lookup"><span data-stu-id="46c1a-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="46c1a-496">但是，如果你想要支持`$select`和`$expand`你需要将该代码更改为。</span><span class="sxs-lookup"><span data-stu-id="46c1a-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="46c1a-497">**在批处理请求过程的 Request.Url 或 RequestContext.Url 为 null**</span><span class="sxs-lookup"><span data-stu-id="46c1a-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="46c1a-498">在批处理方案中， **UrlHelper**为 null 时从访问**Request.Url**或**RequestContext.Url**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="46c1a-499">此问题当前在此处跟踪： [BatchRequestContext.Url 不适用于批处理请求](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="46c1a-500">此问题的解决方法是创建的新实例**UrlHelper**，下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="46c1a-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="46c1a-501">**创建 UrlHelper 的新实例**</span><span class="sxs-lookup"><span data-stu-id="46c1a-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="46c1a-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="46c1a-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="46c1a-503">使用 MVC5 和时 OrgAuth，如果具有 AntiForgerToken 验证来执行此操作的视图，您可能遇到以下错误，当你将数据发布到该视图：</span><span class="sxs-lookup"><span data-stu-id="46c1a-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="46c1a-504">**错误**:</span><span class="sxs-lookup"><span data-stu-id="46c1a-504">**Error**:</span></span>

    <span data-ttu-id="46c1a-505">*'/' 应用程序中的服务器错误。*</span><span class="sxs-lookup"><span data-stu-id="46c1a-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="46c1a-506"><em>一个声明的类型<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'或'<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>未提供 ClaimsIdentity 上存在。若要启用防伪令牌支持基于声明的身份验证，请验证配置的声明提供程序提供这两个在它生成 ClaimsIdentity 实例上的这些声明。如果配置的声明提供方改为使用不同的声明类型，以唯一标识符形式，这可以通过设置静态属性 AntiForgeryConfig.UniqueClaimTypeIdentifier 进行配置。</em></span><span class="sxs-lookup"><span data-stu-id="46c1a-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="46c1a-507">**解决方法**:</span><span class="sxs-lookup"><span data-stu-id="46c1a-507">**Workaround**:</span></span>

    <span data-ttu-id="46c1a-508">若要修复此错误的 Global.asax 中添加以下行：</span><span class="sxs-lookup"><span data-stu-id="46c1a-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="46c1a-509">在下一个版本将解决此问题。</span><span class="sxs-lookup"><span data-stu-id="46c1a-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="46c1a-510">在升级到 MVC5 MVC4 应用程序之后, 生成解决方案并启动它。</span><span class="sxs-lookup"><span data-stu-id="46c1a-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="46c1a-511">你应看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="46c1a-511">You should see the following error:</span></span>

    <span data-ttu-id="46c1a-512">[A]System.Web.WebPages.Razor.Configuration.HostSection 不能强制转换为 [B]System.Web.WebPages.Razor.Configuration.HostSection。</span><span class="sxs-lookup"><span data-stu-id="46c1a-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="46c1a-513">A 类型是来自 System.Web.WebPages.Razor，Version = 2.0.0.0，区域性 = neutral，PublicKeyToken = 31bf3856ad364e35' 默认位置处的上下文中 C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll。</span><span class="sxs-lookup"><span data-stu-id="46c1a-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="46c1a-514">类型 B 源自 System.Web.WebPages.Razor，Version = 3.0.0.0，区域性 = neutral，PublicKeyToken = 31bf3856ad364e35' 默认位置处的上下文中 C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll。</span><span class="sxs-lookup"><span data-stu-id="46c1a-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="46c1a-515">若要修复上述错误，请打开*所有*中你的项目和执行以下的 Web.config 文件 （包括视图文件夹中的）：</span><span class="sxs-lookup"><span data-stu-id="46c1a-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="46c1a-516">更新版本"4.0.0.0"的"System.Web.Mvc"到"5.0.0.0"的所有匹配的项。</span><span class="sxs-lookup"><span data-stu-id="46c1a-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="46c1a-517">更新的"System.Web.Helpers"版本"2.0.0.0"的所有匹配项&quot;System.Web.WebPages&quot;和&quot;System.Web.WebPages.Razor&quot;到"3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="46c1a-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="46c1a-518">例如，进行上述更改后，程序集绑定应如下所示：</span><span class="sxs-lookup"><span data-stu-id="46c1a-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="46c1a-519">有关升级到 MVC 5 的 MVC 4 项目的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="46c1a-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="46c1a-520">当使用 jQuery 非介入式验证客户端验证，验证消息有时是 HTML 输入元素类型不正确 = number。</span><span class="sxs-lookup"><span data-stu-id="46c1a-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="46c1a-521">验证错误的所需的值 （"年龄字段必填") 显示数量无效而不是正确的消息有效的号码是必填的输入时。</span><span class="sxs-lookup"><span data-stu-id="46c1a-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="46c1a-522">此问题通常找到了具有基架代码具有整数属性上创建和编辑视图模型。</span><span class="sxs-lookup"><span data-stu-id="46c1a-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="46c1a-523">若要解决此问题，请更改从的编辑器帮助程序：</span><span class="sxs-lookup"><span data-stu-id="46c1a-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="46c1a-524">到:</span><span class="sxs-lookup"><span data-stu-id="46c1a-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="46c1a-525">ASP.NET MVC 5 不再支持部分信任。</span><span class="sxs-lookup"><span data-stu-id="46c1a-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="46c1a-526">将链接到 MVC 或 WebAPI 二进制文件的项目应删除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="46c1a-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="46c1a-527">移除这些特性可避免编译器错误，如下所示。</span><span class="sxs-lookup"><span data-stu-id="46c1a-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="46c1a-528">请注意，为此，你的副作用不能在同一个应用程序中使用 4.0 和 5.0 程序集。</span><span class="sxs-lookup"><span data-stu-id="46c1a-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="46c1a-529">你需要它们全部更新为 5.0。</span><span class="sxs-lookup"><span data-stu-id="46c1a-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="46c1a-530">与 Facebook 授权 SPA 模板可能导致不稳定在 IE 中时在 intranet 区域中承载网站</span><span class="sxs-lookup"><span data-stu-id="46c1a-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="46c1a-531">SPA 模板提供了外部 Facebook 登录。</span><span class="sxs-lookup"><span data-stu-id="46c1a-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="46c1a-532">当本地运行时使用模板创建的项目时，则在登录可能会导致 IE 崩溃。</span><span class="sxs-lookup"><span data-stu-id="46c1a-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="46c1a-533">解决方案：</span><span class="sxs-lookup"><span data-stu-id="46c1a-533">Solution:</span></span>

1. <span data-ttu-id="46c1a-534">托管该网站在 internet 区域;或</span><span class="sxs-lookup"><span data-stu-id="46c1a-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="46c1a-535">在非 IE 浏览器中测试的方案。</span><span class="sxs-lookup"><span data-stu-id="46c1a-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="46c1a-536">Web 窗体基架</span><span class="sxs-lookup"><span data-stu-id="46c1a-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="46c1a-537">Web 窗体基架已从 VS2013 中删除，并将在未来的更新到 Visual Studio 中可用。</span><span class="sxs-lookup"><span data-stu-id="46c1a-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="46c1a-538">但是，你仍可以通过添加 MVC 依赖项并为 MVC 生成基架使用在 Web 窗体项目中的基架。</span><span class="sxs-lookup"><span data-stu-id="46c1a-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="46c1a-539">你的项目将包含 Web 窗体和 MVC 的组合。</span><span class="sxs-lookup"><span data-stu-id="46c1a-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="46c1a-540">若要添加到你的 Web 窗体项目的 MVC，添加新的基架的项，并选择**MVC 5 依赖项**。</span><span class="sxs-lookup"><span data-stu-id="46c1a-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="46c1a-541">选择最少监视或完整具体取决于是否需要的所有内容文件，如脚本。</span><span class="sxs-lookup"><span data-stu-id="46c1a-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="46c1a-542">然后，添加基架的项 MVC，将在你的项目中创建视图和控制器的。</span><span class="sxs-lookup"><span data-stu-id="46c1a-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="46c1a-543">MVC 和 Web API 基架-HTTP 404 找不到错误</span><span class="sxs-lookup"><span data-stu-id="46c1a-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="46c1a-544">如果在将基架的项添加到项目时遇到错误，，则可能你的项目将处于不一致状态。</span><span class="sxs-lookup"><span data-stu-id="46c1a-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="46c1a-545">某些将基架所做的更改将被回滚，但其他更改，例如已安装的 NuGet 程序包，将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="46c1a-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="46c1a-546">如果回滚路由的配置更改，则用户将收到 HTTP 404 错误，当导航到基架项。</span><span class="sxs-lookup"><span data-stu-id="46c1a-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="46c1a-547">解决方法：</span><span class="sxs-lookup"><span data-stu-id="46c1a-547">Workaround:</span></span>

- <span data-ttu-id="46c1a-548">若要为 MVC 修复此错误，添加新的基架的项，然后选择 MVC 5 依赖项 （最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="46c1a-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="46c1a-549">此过程将向你的项目添加所有所需的更改。</span><span class="sxs-lookup"><span data-stu-id="46c1a-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="46c1a-550">若要为 Web API 修复此错误：</span><span class="sxs-lookup"><span data-stu-id="46c1a-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="46c1a-551">将 WebApiConfig 类添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="46c1a-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="46c1a-552">在应用程序中配置 WebApiConfig.Register\_，如下所示在 Global.asax 中启动方法：</span><span class="sxs-lookup"><span data-stu-id="46c1a-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
