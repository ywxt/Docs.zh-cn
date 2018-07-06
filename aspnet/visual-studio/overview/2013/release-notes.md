---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET 和 Web Tools for Visual Studio 2013 发行说明 |Microsoft Docs
author: microsoft
description: 本文档介绍 ASP.NET 和 Web Tools for Visual Studio 2013 的版本。
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 0f5b8d6a4e0cbfefb7a1fa1d81d9bd27af4a5ad6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833719"
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="eee97-103">ASP.NET 和 Web Tools for Visual Studio 2013 发行说明</span><span class="sxs-lookup"><span data-stu-id="eee97-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>
====================
<span data-ttu-id="eee97-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="eee97-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="eee97-105">本文档介绍 ASP.NET 和 Web Tools for Visual Studio 2013 的版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>


## <a name="contents"></a><span data-ttu-id="eee97-106">内容</span><span class="sxs-lookup"><span data-stu-id="eee97-106">Contents</span></span>

- [<span data-ttu-id="eee97-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="eee97-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="eee97-108">文档</span><span class="sxs-lookup"><span data-stu-id="eee97-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="eee97-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="eee97-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="eee97-110">ASP.NET 和 Web Tools for Visual Studio 2013 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="eee97-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="eee97-111">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eee97-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="eee97-112">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="eee97-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="eee97-113">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="eee97-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="eee97-114">浏览器链接</span><span class="sxs-lookup"><span data-stu-id="eee97-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="eee97-115">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="eee97-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="eee97-116">在 Visual Studio 中的 azure 应用服务 Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="eee97-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="eee97-117">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="eee97-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="eee97-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="eee97-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="eee97-119">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="eee97-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="eee97-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="eee97-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="eee97-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="eee97-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="eee97-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="eee97-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="eee97-123">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="eee97-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="eee97-124">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="eee97-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="eee97-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="eee97-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="eee97-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="eee97-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="eee97-127">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="eee97-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="eee97-128">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="eee97-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="eee97-129">安装说明</span><span class="sxs-lookup"><span data-stu-id="eee97-129">Installation Notes</span></span>

<span data-ttu-id="eee97-130">ASP.NET 和 Web Tools for Visual Studio 2013 在主安装程序中捆绑和可下载[此处](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="eee97-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="eee97-131">文档</span><span class="sxs-lookup"><span data-stu-id="eee97-131">Documentation</span></span>

<span data-ttu-id="eee97-132">教程和有关 ASP.NET 和 Web Tools for Visual Studio 2013 的其他信息中有[ASP.NET web 站点](https://www.asp.net/)。</span><span class="sxs-lookup"><span data-stu-id="eee97-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="eee97-133">软件要求</span><span class="sxs-lookup"><span data-stu-id="eee97-133">Software Requirements</span></span>

<span data-ttu-id="eee97-134">ASP.NET 和 Web 工具需要 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="eee97-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="eee97-135">ASP.NET 和 Web Tools for Visual Studio 2013 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="eee97-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="eee97-136">以下部分介绍已在版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="eee97-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="eee97-137">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eee97-137">One ASP.NET</span></span>

<span data-ttu-id="eee97-138">使用 Visual Studio 2013 的发布，我们已向统一的体验使用 ASP.NET 技术，以便您可以轻松地混合和匹配所的需的步骤。</span><span class="sxs-lookup"><span data-stu-id="eee97-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="eee97-139">例如，您可以启动使用 MVC 的项目和轻松地向项目添加 Web 窗体页更高版本，或创建 Web Api 基架 Web 窗体项目中。</span><span class="sxs-lookup"><span data-stu-id="eee97-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="eee97-140">一个 ASP.NET 就是让它更容易为你执行的操作在 ASP.NET 中您喜欢的开发人员。</span><span class="sxs-lookup"><span data-stu-id="eee97-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="eee97-141">无论选择何种技术，可以有要在同一 ASP.NET 的受信任的基础框架生成的置信度。</span><span class="sxs-lookup"><span data-stu-id="eee97-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="eee97-142">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="eee97-142">New Web Project Experience</span></span>

<span data-ttu-id="eee97-143">提供了增强的 Visual Studio 2013 中创建新的 web 项目的体验。</span><span class="sxs-lookup"><span data-stu-id="eee97-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="eee97-144">在中**新的 ASP.NET Web 项目**对话框，可以选择希望、 配置技术 (Web 窗体、 MVC、 Web API) 的任意组合，配置身份验证选项，以及添加单元测试项目的项目类型。</span><span class="sxs-lookup"><span data-stu-id="eee97-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新建 ASP.NET 项目](release-notes/_static/image1.png)

<span data-ttu-id="eee97-146">新建对话框可以更改许多模板的默认身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="eee97-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="eee97-147">例如，创建 ASP.NET Web 窗体项目时您可以选择以下选项之一：</span><span class="sxs-lookup"><span data-stu-id="eee97-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="eee97-148">无身份验证</span><span class="sxs-lookup"><span data-stu-id="eee97-148">No Authentication</span></span>
- <span data-ttu-id="eee97-149">单个用户帐户 （ASP.NET 成员身份或社交提供程序登录）</span><span class="sxs-lookup"><span data-stu-id="eee97-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="eee97-150">组织帐户 (Active Directory 中的 internet 应用程序)</span><span class="sxs-lookup"><span data-stu-id="eee97-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="eee97-151">Windows 身份验证 (Active Directory 中的 intranet 应用程序)</span><span class="sxs-lookup"><span data-stu-id="eee97-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![身份验证选项](release-notes/_static/image2.png)

<span data-ttu-id="eee97-153">有关创建 web 项目的新过程的详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="eee97-154">有关新的身份验证选项的详细信息，请参阅[ASP.NET 标识](#TOC8)本文档中更高版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="eee97-155">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="eee97-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="eee97-156">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="eee97-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="eee97-157">它可以轻松地将样板代码添加到项目中使用的数据模型进行交互。</span><span class="sxs-lookup"><span data-stu-id="eee97-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="eee97-158">在以前版本的 Visual Studio 中，基架被限制为 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="eee97-159">使用 Visual Studio 2013，现在可以用于任何 ASP.NET 项目，包括 Web 窗体使用基架。</span><span class="sxs-lookup"><span data-stu-id="eee97-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="eee97-160">Visual Studio 2013 当前不支持生成页对于 Web 窗体项目，但您仍可以使用基架使用 Web 窗体通过向项目添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="eee97-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="eee97-161">将在未来更新中添加对生成的 Web 窗体页的支持。</span><span class="sxs-lookup"><span data-stu-id="eee97-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="eee97-162">在使用基架，我们确保所有必需的依赖项安装在项目中。</span><span class="sxs-lookup"><span data-stu-id="eee97-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="eee97-163">例如，如果您开始创建 ASP.NET Web 窗体项目，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用将自动添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="eee97-164">若要将 MVC 基架添加到 Web 窗体项目，添加**新基架项**，然后选择**MVC 5 依赖项**在对话框窗口中。</span><span class="sxs-lookup"><span data-stu-id="eee97-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="eee97-165">有两个选项基架 MVC;最小和完全。</span><span class="sxs-lookup"><span data-stu-id="eee97-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="eee97-166">如果你选择最小，NuGet 包和 ASP.NET MVC 的引用添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="eee97-167">如果选择完全选项，添加最小依赖项，以及对于 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="eee97-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="eee97-168">对基架异步控制器的支持使用从 Entity Framework 6 的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="eee97-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="eee97-169">有关详细信息和教程，请参阅[ASP.NET 基架概述](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="eee97-170">浏览器链接-浏览器和 Visual Studio 之间的通道，SignalR</span><span class="sxs-lookup"><span data-stu-id="eee97-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="eee97-171">新[浏览器链接](using-browser-link.md)功能可以连接到 Visual Studio 的多个浏览器并刷新其所有通过单击工具栏中的按钮。</span><span class="sxs-lookup"><span data-stu-id="eee97-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="eee97-172">可以将多个浏览器连接到开发站点，其中包括移动仿真程序，并单击全部在同一时间刷新到刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="eee97-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="eee97-173">浏览器链接还公开一个 API，使开发人员能够编写浏览器链接扩展。</span><span class="sxs-lookup"><span data-stu-id="eee97-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="eee97-174">通过使开发人员能够充分利用浏览器链接 API，就可以创建跨边界的 Visual Studio 和任何已连接的浏览器之间的非常高级的方案。</span><span class="sxs-lookup"><span data-stu-id="eee97-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="eee97-175">Web Essentials 利用 API 创建 Visual Studio 和浏览器的开发人员工具、 远程控制移动仿真程序和更多操作之间的集成的体验。</span><span class="sxs-lookup"><span data-stu-id="eee97-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="eee97-176">Visual Studio Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="eee97-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="eee97-177">Visual Studio 2013 web 应用程序中包含新的 HTML 编辑器的 Razor 文件和 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="eee97-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="eee97-178">新的 HTML 编辑器提供基于 HTML5 的单个统一的架构。</span><span class="sxs-lookup"><span data-stu-id="eee97-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="eee97-179">它具有大括号自动完成、 jQuery UI 和 AngularJS 特性 IntelliSense 中，IntelliSense 分组、 ID 和类名 Intellisense 和其他改进包括更好的性能，格式设置属性和智能标记。</span><span class="sxs-lookup"><span data-stu-id="eee97-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="eee97-180">下面的屏幕截图演示了如何使用 HTML 编辑器中的 Bootstrap 属性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="eee97-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 编辑器中的 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="eee97-182">Visual Studio 2013 还就使用这两个 CoffeeScript 和更低的编辑器中生成。</span><span class="sxs-lookup"><span data-stu-id="eee97-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="eee97-183">LESS 编辑器与所有出色的功能来自 CSS 编辑器，而是在中的所有较少文档均适用于变量和 mixin 的特定 Intellisense@import链。</span><span class="sxs-lookup"><span data-stu-id="eee97-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="eee97-184">在 Visual Studio 中的 azure 应用服务 Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="eee97-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="eee97-185">在 Azure SDK for.NET 2.2 与 Visual Studio 2013，你可以使用**服务器资源管理器**直接与你的远程 web 应用进行交互。</span><span class="sxs-lookup"><span data-stu-id="eee97-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="eee97-186">可以登录到 Azure 帐户，创建新的 web 应用、 配置应用程序、 查看实时日志等等。</span><span class="sxs-lookup"><span data-stu-id="eee97-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="eee97-187">不久后终止 SDK 2.2 即将发布，您将能够在 Azure 中远程调试模式运行。</span><span class="sxs-lookup"><span data-stu-id="eee97-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="eee97-188">安装当前版本的 Azure sdk for.NET 时，大多数 Azure 应用服务 Web 应用的新功能也适用于 Visual Studio 2012 中。</span><span class="sxs-lookup"><span data-stu-id="eee97-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="eee97-189">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="eee97-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="eee97-190">在 Azure 应用服务中创建 ASP.NET web 应用</span><span class="sxs-lookup"><span data-stu-id="eee97-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="eee97-191">使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="eee97-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="eee97-192">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="eee97-192">Web Publish Enhancements</span></span>

<span data-ttu-id="eee97-193">Visual Studio 2013 包含新的和增强的 Web 发布功能。</span><span class="sxs-lookup"><span data-stu-id="eee97-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="eee97-194">以下是其中一些：</span><span class="sxs-lookup"><span data-stu-id="eee97-194">Here are a few of them:</span></span>

- <span data-ttu-id="eee97-195">轻松[自动执行 Web.config 文件加密](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="eee97-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="eee97-196">（此链接和以下两个点可能不可用之前在 10/17 天较晚的 MSDN 上的文档。）</span><span class="sxs-lookup"><span data-stu-id="eee97-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="eee97-197">轻松[自动采用应用程序在部署期间脱机](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="eee97-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="eee97-198">配置对 Web 部署[使用文件校验和，而不是上次更改日期](https://go.microsoft.com/fwlink/?LinkId=325531)用于确定哪些文件应复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="eee97-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="eee97-199">使用 FTP 或文件系统发布方法时，以及使用 Web 部署，快速发布单个所选的文件 （包括 Web.config）。</span><span class="sxs-lookup"><span data-stu-id="eee97-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="eee97-200">有关 ASP.NET web 部署的详细信息，请参阅[ASP.NET 站点](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="eee97-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="eee97-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="eee97-201">NuGet 2.7</span></span>

<span data-ttu-id="eee97-202">NuGet 2.7 包括一套丰富的新功能描述了这些详细的介绍[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)。</span><span class="sxs-lookup"><span data-stu-id="eee97-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="eee97-203">此版本的 NuGet 还无需提供显式同意的 NuGet 包还原功能，若要下载的包。</span><span class="sxs-lookup"><span data-stu-id="eee97-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="eee97-204">通过安装 NuGet 现在授予同意的情况下 （和 NuGet 的首选项对话框中的关联复选框）。</span><span class="sxs-lookup"><span data-stu-id="eee97-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="eee97-205">现在包还原只是默认情况下适用。</span><span class="sxs-lookup"><span data-stu-id="eee97-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="eee97-206">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="eee97-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="eee97-207">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eee97-207">One ASP.NET</span></span>

<span data-ttu-id="eee97-208">Web 窗体项目模板将与新的 One ASP.NET 功能无缝集成。</span><span class="sxs-lookup"><span data-stu-id="eee97-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="eee97-209">您可以添加到你的 Web 窗体项目，支持 MVC 和 Web API，你可以配置身份验证使用 One ASP.NET 项目创建向导。</span><span class="sxs-lookup"><span data-stu-id="eee97-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="eee97-210">有关详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="eee97-211">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="eee97-211">ASP.NET Identity</span></span>

<span data-ttu-id="eee97-212">Web 窗体项目模板支持新的 ASP.NET 标识框架。</span><span class="sxs-lookup"><span data-stu-id="eee97-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="eee97-213">此外，模板现在支持创建 Web 窗体 intranet 项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="eee97-214">有关详细信息，请参阅[身份验证方法](creating-web-projects-in-visual-studio.md#auth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="eee97-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="eee97-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="eee97-215">Bootstrap</span></span>

<span data-ttu-id="eee97-216">使用 Web 窗体模板[Bootstrap](http://twitter.github.io/bootstrap/)提供时尚且响应迅速的界面外观，可以轻松地自定义。</span><span class="sxs-lookup"><span data-stu-id="eee97-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="eee97-217">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 Bootstrap](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="eee97-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="eee97-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="eee97-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="eee97-219">一个 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eee97-219">One ASP.NET</span></span>

<span data-ttu-id="eee97-220">Web MVC 项目模板将与新的 One ASP.NET 功能无缝集成。</span><span class="sxs-lookup"><span data-stu-id="eee97-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="eee97-221">您可以自定义 MVC 项目和配置身份验证使用 One ASP.NET 项目创建向导。</span><span class="sxs-lookup"><span data-stu-id="eee97-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="eee97-222">为 ASP.NET MVC 5 的介绍性教程，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="eee97-223">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="eee97-224">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="eee97-224">ASP.NET Identity</span></span>

<span data-ttu-id="eee97-225">已更新的 MVC 项目模板来使用 ASP.NET 标识进行身份验证和标识管理。</span><span class="sxs-lookup"><span data-stu-id="eee97-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="eee97-226">提供 Facebook 和 Google 身份验证和新的成员资格 API 的教程，请参阅[创建 ASP.NET MVC 5 应用程序使用 Facebook 和 Google OAuth2 和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)和[使用身份验证创建 ASP.NET MVC 应用和SQL 数据库并将其部署到 Azure 应用服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="eee97-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="eee97-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="eee97-227">Bootstrap</span></span>

<span data-ttu-id="eee97-228">MVC 项目模板已更新为使用[Bootstrap](http://getbootstrap.com/)提供时尚且响应迅速的界面外观，可以轻松地自定义。</span><span class="sxs-lookup"><span data-stu-id="eee97-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="eee97-229">有关详细信息，请参阅[Visual Studio 2013 web 项目模板中的 Bootstrap](creating-web-projects-in-visual-studio.md#bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="eee97-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="eee97-230">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="eee97-230">Authentication filters</span></span>

<span data-ttu-id="eee97-231">身份验证筛选器是一种新的筛选器在 ASP.NET MVC 中，在 ASP.NET MVC 管道中的授权筛选器之前运行，并允许您指定身份验证逻辑每个操作，每个控制器或全局范围内的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="eee97-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="eee97-232">身份验证筛选器处理在请求中的凭据，并提供相应的用户权限。</span><span class="sxs-lookup"><span data-stu-id="eee97-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="eee97-233">身份验证筛选器还可以在未经授权的请求响应中添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="eee97-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="eee97-234">筛选器替代项</span><span class="sxs-lookup"><span data-stu-id="eee97-234">Filter overrides</span></span>

<span data-ttu-id="eee97-235">你现在可以重写的筛选器适用于给定的操作方法或控制器通过指定重写筛选器。</span><span class="sxs-lookup"><span data-stu-id="eee97-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="eee97-236">覆盖筛选器指定一的组不应运行给定作用域 （操作或控制器） 的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="eee97-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="eee97-237">这允许你配置的全局应用，但然后排除特定全局筛选器应用到特定操作或控制器筛选器。</span><span class="sxs-lookup"><span data-stu-id="eee97-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="eee97-238">属性路由</span><span class="sxs-lookup"><span data-stu-id="eee97-238">Attribute routing</span></span>

<span data-ttu-id="eee97-239">ASP.NET MVC 现在支持属性路由中，由 Tim McCall，一书的作者的发布内容衷心[ http://attributerouting.net ](http://attributerouting.net)。</span><span class="sxs-lookup"><span data-stu-id="eee97-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="eee97-240">使用属性路由可以对操作和控制器进行批注来指定路由。</span><span class="sxs-lookup"><span data-stu-id="eee97-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="eee97-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="eee97-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="eee97-242">属性路由</span><span class="sxs-lookup"><span data-stu-id="eee97-242">Attribute routing</span></span>

<span data-ttu-id="eee97-243">ASP.NET Web API 现在支持属性路由中，由 Tim McCall，一书的作者的发布内容衷心[ http://attributerouting.net ](http://attributerouting.net)。</span><span class="sxs-lookup"><span data-stu-id="eee97-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="eee97-244">使用属性路由可以对操作和控制器，此类进行批注来指定 Web API 路由：</span><span class="sxs-lookup"><span data-stu-id="eee97-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="eee97-245">属性路由可以更好地控制 Uri 在你的 web API。</span><span class="sxs-lookup"><span data-stu-id="eee97-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="eee97-246">例如，您可以轻松地定义资源层次结构使用单个 API 控制器：</span><span class="sxs-lookup"><span data-stu-id="eee97-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="eee97-247">属性路由还提供一种方便语法，用于指定可选参数、 默认值和路由约束：</span><span class="sxs-lookup"><span data-stu-id="eee97-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="eee97-248">有关属性路由的详细信息，请参阅[Web API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="eee97-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="eee97-249">OAuth 2.0</span></span>

<span data-ttu-id="eee97-250">Web API 和单页应用程序项目模板现在支持使用 OAuth 2.0 授权。</span><span class="sxs-lookup"><span data-stu-id="eee97-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="eee97-251">OAuth 2.0 是一个框架，用于授予对受保护资源的客户端访问权限。</span><span class="sxs-lookup"><span data-stu-id="eee97-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="eee97-252">它适用于各种客户端包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="eee97-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="eee97-253">对 OAuth 2.0 的支持取决于新安全中间件为持有者身份验证提供由 Microsoft OWIN 组件和实现授权服务器角色。</span><span class="sxs-lookup"><span data-stu-id="eee97-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="eee97-254">或者，可以授权客户端使用的组织的授权服务器，如 Azure Active Directory 或 Windows Server 2012 R2 中的 ad FS。</span><span class="sxs-lookup"><span data-stu-id="eee97-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="eee97-255">OData 的改进</span><span class="sxs-lookup"><span data-stu-id="eee97-255">OData Improvements</span></span>

<span data-ttu-id="eee97-256">**支持 $select，$ expand、 $batch 和 $value**</span><span class="sxs-lookup"><span data-stu-id="eee97-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="eee97-257">ASP.NET Web API OData 现在有 $select 的完整支持、 $expand、 和 $value。</span><span class="sxs-lookup"><span data-stu-id="eee97-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="eee97-258">此外可以使用 $batch 请求批处理和处理的变更集。</span><span class="sxs-lookup"><span data-stu-id="eee97-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="eee97-259">$Select 和 $expand 选项使您可以更改从 OData 终结点返回的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="eee97-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="eee97-260">有关详细信息，请参阅[简介 $select 和 $expand 中 Web API OData 支持](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="eee97-261">**改进了可扩展性**</span><span class="sxs-lookup"><span data-stu-id="eee97-261">**Improved extensibility**</span></span>

<span data-ttu-id="eee97-262">OData 格式化程序现在是可扩展的。</span><span class="sxs-lookup"><span data-stu-id="eee97-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="eee97-263">可以添加 Atom 项元数据、 支持命名的流和媒体链接条目、 添加实例批注和自定义生成链接的方式。</span><span class="sxs-lookup"><span data-stu-id="eee97-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="eee97-264">**无类型的支持**</span><span class="sxs-lookup"><span data-stu-id="eee97-264">**Type-less support**</span></span>

<span data-ttu-id="eee97-265">现在可以生成 OData 服务而无需定义实体类型的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="eee97-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="eee97-266">相反，你的 OData 控制器可以接受或返回的实例**IEdmObject**，这是 OData 格式化程序序列化/反序列化。</span><span class="sxs-lookup"><span data-stu-id="eee97-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="eee97-267">**重复使用现有模型**</span><span class="sxs-lookup"><span data-stu-id="eee97-267">**Reuse an existing model**</span></span>

<span data-ttu-id="eee97-268">如果已有现有的实体数据模型 (EDM) 中，你可以现在重复使用它直接，而无需生成一个新。</span><span class="sxs-lookup"><span data-stu-id="eee97-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="eee97-269">例如，如果使用实体框架，您可以使用 EF 为您生成 EDM。</span><span class="sxs-lookup"><span data-stu-id="eee97-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="eee97-270">批处理请求</span><span class="sxs-lookup"><span data-stu-id="eee97-270">Request Batching</span></span>

<span data-ttu-id="eee97-271">请求批处理将合并到单个 HTTP POST 请求，以减少网络流量，并提供流畅些，更少聊天式用户界面的多个操作。</span><span class="sxs-lookup"><span data-stu-id="eee97-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="eee97-272">ASP.NET Web API 现在支持用于请求批处理的几种策略：</span><span class="sxs-lookup"><span data-stu-id="eee97-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="eee97-273">使用 OData 服务的 $batch 终结点。</span><span class="sxs-lookup"><span data-stu-id="eee97-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="eee97-274">打包成单个 MIME 多部分请求多个请求。</span><span class="sxs-lookup"><span data-stu-id="eee97-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="eee97-275">使用自定义的批处理格式。</span><span class="sxs-lookup"><span data-stu-id="eee97-275">Use a custom batching format.</span></span>

<span data-ttu-id="eee97-276">若要启用批处理请求，只需将批处理的处理程序的路由添加到你的 Web API 配置：</span><span class="sxs-lookup"><span data-stu-id="eee97-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="eee97-277">您还可以控制是否请求或按顺序或按任意顺序执行。</span><span class="sxs-lookup"><span data-stu-id="eee97-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="eee97-278">可移植的 ASP.NET Web API 客户端</span><span class="sxs-lookup"><span data-stu-id="eee97-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="eee97-279">ASP.NET Web API 客户端现在可用于创建工作的可移植类库跨 Windows 应用商店和 Windows Phone 8 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eee97-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="eee97-280">此外可以创建可移植的格式化程序可以在客户端和服务器之间共享。</span><span class="sxs-lookup"><span data-stu-id="eee97-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="eee97-281">改进了可测试性</span><span class="sxs-lookup"><span data-stu-id="eee97-281">Improved Testability</span></span>

<span data-ttu-id="eee97-282">Web API 2 使它更容易进行单元测试 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="eee97-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="eee97-283">只需实例化与您的请求消息和配置，在 API 控制器，然后调用你想要测试的操作方法。</span><span class="sxs-lookup"><span data-stu-id="eee97-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="eee97-284">它也很容易模拟**UrlHelper**类，用于执行链接生成的操作方法。</span><span class="sxs-lookup"><span data-stu-id="eee97-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="eee97-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="eee97-285">IHttpActionResult</span></span>

<span data-ttu-id="eee97-286">现在，可以实现 IHttpActionResult 封装 Web API 操作方法的结果。</span><span class="sxs-lookup"><span data-stu-id="eee97-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="eee97-287">从 Web API 操作方法返回 IHttpActionResult 执行由 ASP.NET Web API 运行时以生成结果的响应消息。</span><span class="sxs-lookup"><span data-stu-id="eee97-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="eee97-288">可以从任何 Web API 操作来简化单元返回 IHttpActionResult 测试 Web API 实现。</span><span class="sxs-lookup"><span data-stu-id="eee97-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="eee97-289">为方便起见数 IHttpActionResult 实现提供开箱包含用于返回特定状态代码的结果，格式的内容或内容协商响应。</span><span class="sxs-lookup"><span data-stu-id="eee97-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="eee97-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="eee97-290">HttpRequestContext</span></span>

<span data-ttu-id="eee97-291">新**HttpRequestContext**跟踪与请求相关联，但不是从请求立即可用的任何状态。</span><span class="sxs-lookup"><span data-stu-id="eee97-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="eee97-292">例如，可以使用**HttpRequestContext**若要获取路由数据，请求客户端证书，与关联的主体**UrlHelper**和虚拟路径根。</span><span class="sxs-lookup"><span data-stu-id="eee97-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="eee97-293">您可以轻松地创建**HttpRequestContext**进行单元测试目的。</span><span class="sxs-lookup"><span data-stu-id="eee97-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="eee97-294">因为请求的主体进行流处理的请求而不是依靠**Thread.CurrentPrincipal**，在 Web API 管道时，主体现可在请求的整个生存期内。</span><span class="sxs-lookup"><span data-stu-id="eee97-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="eee97-295">CORS</span><span class="sxs-lookup"><span data-stu-id="eee97-295">CORS</span></span>

<span data-ttu-id="eee97-296">由于从 Brock Allen 的另一个良好发布内容，ASP.NET 现在完全支持跨域请求共享 (CORS)。</span><span class="sxs-lookup"><span data-stu-id="eee97-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="eee97-297">浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="eee97-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="eee97-298">[CORS](http://www.w3.org/TR/cors/)是一项 W3C 标准，可让服务器放宽同域策略。</span><span class="sxs-lookup"><span data-stu-id="eee97-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="eee97-299">使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="eee97-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="eee97-300">Web API 2 现在支持 CORS，包括自动处理的预检请求。</span><span class="sxs-lookup"><span data-stu-id="eee97-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="eee97-301">有关详细信息，请参阅[ASP.NET Web API 中启用跨域请求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="eee97-302">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="eee97-302">Authentication Filters</span></span>

<span data-ttu-id="eee97-303">身份验证筛选器是一种新的筛选器，在 ASP.NET Web API 管道中的授权筛选器之前运行，并允许您指定身份验证逻辑每个操作，ASP.NET Web API 中每个控制器或全局范围内的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="eee97-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="eee97-304">身份验证筛选器处理在请求中的凭据，并提供相应的用户权限。</span><span class="sxs-lookup"><span data-stu-id="eee97-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="eee97-305">身份验证筛选器还可以在未经授权的请求响应中添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="eee97-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="eee97-306">筛选器覆盖</span><span class="sxs-lookup"><span data-stu-id="eee97-306">Filter Overrides</span></span>

<span data-ttu-id="eee97-307">你现在可以重写的筛选器应用于给定的操作方法或控制器，通过指定重写筛选器。</span><span class="sxs-lookup"><span data-stu-id="eee97-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="eee97-308">覆盖筛选器指定一的组给定作用域 （操作或控制器），不应运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="eee97-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="eee97-309">这允许您添加全局筛选器、 但然后排除一些从特定操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="eee97-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="eee97-310">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="eee97-310">OWIN Integration</span></span>

<span data-ttu-id="eee97-311">ASP.NET Web API 现在完全支持 OWIN，并可以在任何 OWIN 支持主机上运行。</span><span class="sxs-lookup"><span data-stu-id="eee97-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="eee97-312">此外包括**HostAuthenticationFilter** ，它提供与 OWIN 身份验证系统集成。</span><span class="sxs-lookup"><span data-stu-id="eee97-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="eee97-313">通过 OWIN 集成，可以在您自己的进程以及其他的 OWIN 中间件，例如 SignalR 中自托管 Web API。</span><span class="sxs-lookup"><span data-stu-id="eee97-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="eee97-314">有关详细信息，请参阅[使用 OWIN 自托管 ASP.NET Web API 来](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="eee97-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="eee97-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="eee97-316">以下部分介绍 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="eee97-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="eee97-317">基于 OWIN</span><span class="sxs-lookup"><span data-stu-id="eee97-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="eee97-318">MapHubs 和 MapConnection 现 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="eee97-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="eee97-319">跨域支持</span><span class="sxs-lookup"><span data-stu-id="eee97-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="eee97-320">iOS 和 Android 支持通过 MonoTouch 和 MonoDroid</span><span class="sxs-lookup"><span data-stu-id="eee97-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="eee97-321">可移植.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="eee97-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="eee97-322">新的自承载包</span><span class="sxs-lookup"><span data-stu-id="eee97-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="eee97-323">向后兼容服务器支持</span><span class="sxs-lookup"><span data-stu-id="eee97-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="eee97-324">删除了对.NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="eee97-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="eee97-325">将消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="eee97-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="eee97-326">向特定用户发送一条消息</span><span class="sxs-lookup"><span data-stu-id="eee97-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="eee97-327">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="eee97-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="eee97-328">更轻松的单元测试的中心</span><span class="sxs-lookup"><span data-stu-id="eee97-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="eee97-329">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="eee97-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="eee97-330">有关如何升级现有的 1.x 项目到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.x 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="eee97-331">基于 OWIN</span><span class="sxs-lookup"><span data-stu-id="eee97-331">Built on OWIN</span></span>

<span data-ttu-id="eee97-332">完全在构建 SignalR 2.0 [OWIN (Open Web Interface for.NET)](http://owin.org/)。</span><span class="sxs-lookup"><span data-stu-id="eee97-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="eee97-333">此更改使 SignalR 的安装过程更加一致 web 承载和自承载 SignalR 应用程序，但也需要使用的 API 更改数。</span><span class="sxs-lookup"><span data-stu-id="eee97-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="eee97-334">MapHubs 和 MapConnection 现 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="eee97-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="eee97-335">为了与 OWIN 标准兼容，这些方法已重命名为`MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="eee97-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="eee97-336">`MapSignalR` 调用无参数将映射所有中心 (作为`MapHubs`在版本 1.x); 映射单个**PersistentConnection**对象，指定连接类型作为类型参数，并适用于所用连接的 URL 扩展第一个参数。</span><span class="sxs-lookup"><span data-stu-id="eee97-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="eee97-337">`MapSignalR` Owin startup 类中调用方法。</span><span class="sxs-lookup"><span data-stu-id="eee97-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="eee97-338">Visual Studio 2013 包含用于 Owin 启动类; 的新模板若要使用此模板，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="eee97-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="eee97-339">右键单击该项目</span><span class="sxs-lookup"><span data-stu-id="eee97-339">Right-click on the project</span></span>
2. <span data-ttu-id="eee97-340">选择**添加**，**新项...**</span><span class="sxs-lookup"><span data-stu-id="eee97-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="eee97-341">选择**Owin 启动类**。</span><span class="sxs-lookup"><span data-stu-id="eee97-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="eee97-342">将新类命名**Startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="eee97-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="eee97-343">在中**Web 应用程序，** Owin 启动类包含`MapSignalR`方法随后将添加到 Owin 的启动过程中的 Web.Config 文件中，应用程序设置节点中使用的项，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eee97-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="eee97-344">在中**自承载应用程序**，启动类的类型参数作为传递`WebApp.Start`方法。</span><span class="sxs-lookup"><span data-stu-id="eee97-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="eee97-345">**中心和 SignalR 中的连接映射 （从 web 应用程序中的全局应用程序文件） 的 1.x:**</span><span class="sxs-lookup"><span data-stu-id="eee97-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="eee97-346">**中心和 SignalR 2.0 （从 Owin 启动类文件） 中的连接的映射：**</span><span class="sxs-lookup"><span data-stu-id="eee97-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="eee97-347">在中**自承载应用程序**，作为类型参数传递的 Startup 类`WebApp.Start`方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eee97-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="eee97-348">跨域支持</span><span class="sxs-lookup"><span data-stu-id="eee97-348">Cross-Domain Support</span></span>

<span data-ttu-id="eee97-349">在 SignalR 1.x 中的，跨域请求已由单个 EnableCrossDomain 标志控制。</span><span class="sxs-lookup"><span data-stu-id="eee97-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="eee97-350">此标志控制 JSONP 和 CORS 请求。</span><span class="sxs-lookup"><span data-stu-id="eee97-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="eee97-351">对于更大的灵活性，所有的 CORS 支持已从 SignalR 的服务器组件 （JavaScript lients 仍使用 CORS 通常如果检测到由浏览器支持它），以及新的 OWIN 中间件变得可用于支持这些方案。</span><span class="sxs-lookup"><span data-stu-id="eee97-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript lients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="eee97-352">在 SignalR 2.0 中，如果 JSONP 客户端上 （支持需要跨域请求旧版浏览器中），它将需要通过设置显式启用`EnableJSONP`上`HubConfiguration`对象传递给`true`，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eee97-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="eee97-353">JSONP 是默认禁用，因为它比 CORS 不太安全。</span><span class="sxs-lookup"><span data-stu-id="eee97-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="eee97-354">若要添加新的 CORS 中间件 SignalR 2.0 中，添加`Microsoft.Owin.Cors`库项目，并调用`UseCors`之前 SignalR 中间件，如下面的部分中所示。</span><span class="sxs-lookup"><span data-stu-id="eee97-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="eee97-355">**向项目添加 Microsoft.Owin.Cors**： 若要安装此库，包管理器控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="eee97-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="eee97-356">此命令会将 2.0.0 添加到你的项目包的版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="eee97-357">**调用 UseCors**</span><span class="sxs-lookup"><span data-stu-id="eee97-357">**Calling UseCors**</span></span>

<span data-ttu-id="eee97-358">下面的代码段演示如何实现跨域连接在 SignalR 1.x 和 2.0。</span><span class="sxs-lookup"><span data-stu-id="eee97-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="eee97-359">**在 SignalR 中实现跨域请求 （从全局应用程序文件中） 的 1.x**</span><span class="sxs-lookup"><span data-stu-id="eee97-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="eee97-360">**在 SignalR 2.0 （从 C# 代码文件） 中实现跨域请求**</span><span class="sxs-lookup"><span data-stu-id="eee97-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="eee97-361">下面的代码演示如何启用 CORS 或 JSONP 的 SignalR 2.0 项目中。</span><span class="sxs-lookup"><span data-stu-id="eee97-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="eee97-362">此代码示例使用`Map`并`RunSignalR`而不是`MapSignalR`，以便将 CORS 中间件运行仅针对需要 CORS 支持 SignalR 请求 (而不是对中指定的路径上的所有流量`MapSignalR`。)`Map`还可用于运行针对特定的 URL 前缀，而不是整个应用程序所需的任何其他中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="eee97-363">iOS 和 Android 支持通过 MonoTouch 和 MonoDroid</span><span class="sxs-lookup"><span data-stu-id="eee97-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="eee97-364">适用于 iOS 和 Android 客户端都使用 MonoTouch 和 MonoDroid 组件添加了支持[Xamarin 库](https://xamarin.com/)。</span><span class="sxs-lookup"><span data-stu-id="eee97-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="eee97-365">有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="eee97-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="eee97-366">这些组件将在中提供[Xamarin 应用商店](https://store.xamarin.com/)SignalR RTW 版本时可用。</span><span class="sxs-lookup"><span data-stu-id="eee97-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a> <span data-ttu-id="eee97-367"># # # 可移植.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="eee97-367">### Portable .NET client</span></span>

<span data-ttu-id="eee97-368">以更好地促进跨平台开发、 Silverlight、 WinRT 并且 Windows Phone 客户端已替换为单个可移植.NET 客户端支持以下平台：</span><span class="sxs-lookup"><span data-stu-id="eee97-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="eee97-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="eee97-369">NET 4.5</span></span>
- <span data-ttu-id="eee97-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="eee97-370">Silverlight 5</span></span>
- <span data-ttu-id="eee97-371">WinRT (适用于 Windows 应用商店应用程序的.NET)</span><span class="sxs-lookup"><span data-stu-id="eee97-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="eee97-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="eee97-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="eee97-373">新的自承载包</span><span class="sxs-lookup"><span data-stu-id="eee97-373">New Self-Host Package</span></span>

<span data-ttu-id="eee97-374">现在有了 NuGet 包可以轻松地开始使用自承载的 SignalR （托管在进程中的 SignalR 应用程序或其他应用程序，而托管在 web 服务器）。</span><span class="sxs-lookup"><span data-stu-id="eee97-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="eee97-375">若要升级使用 SignalR 构建的自承载项目 1.x 中，删除 Microsoft.AspNet.SignalR.Owin 程序包，并添加 Microsoft.AspNet.SignalR.SelfHost 包。</span><span class="sxs-lookup"><span data-stu-id="eee97-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="eee97-376">有关如何开始使用自承载包的详细信息，请参阅[教程： 自承载 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="eee97-377">向后兼容服务器支持</span><span class="sxs-lookup"><span data-stu-id="eee97-377">Backward-compatible server support</span></span>

<span data-ttu-id="eee97-378">在以前版本的 SignalR，SignalR 包在客户端中使用和需要完全相同的服务器的版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="eee97-379">为了支持胖客户端应用程序将会很难更新，SignalR 2.0 现在支持使用旧版客户端的较新的服务器版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="eee97-380">**注意： SignalR 2.0 不支持使用较旧版本与更高版本的客户端生成的服务器。**</span><span class="sxs-lookup"><span data-stu-id="eee97-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="eee97-381">删除了对.NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="eee97-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="eee97-382">SignalR 2.0 已删除对 server 结合使用.NET 4.0 的互操作性的支持。</span><span class="sxs-lookup"><span data-stu-id="eee97-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="eee97-383">与 SignalR 2.0 服务器，必须使用.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="eee97-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="eee97-384">仍是 SignalR 2.0 的.NET 4.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="eee97-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="eee97-385">将消息发送到客户端和组的列表</span><span class="sxs-lookup"><span data-stu-id="eee97-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="eee97-386">在 SignalR 2.0 中，则可以使用客户端和组 Id 的列表发送邮件。</span><span class="sxs-lookup"><span data-stu-id="eee97-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="eee97-387">以下代码片段演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="eee97-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="eee97-388">**将消息发送到客户端和使用 PersistentConnection 组的列表**</span><span class="sxs-lookup"><span data-stu-id="eee97-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="eee97-389">**将消息发送到客户端和组使用中心的列表**</span><span class="sxs-lookup"><span data-stu-id="eee97-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="eee97-390">向特定用户发送一条消息</span><span class="sxs-lookup"><span data-stu-id="eee97-390">Sending a message to a specific user</span></span>

<span data-ttu-id="eee97-391">此功能允许用户指定用户 Id 是基于通过新界面 IUserIdProvider IRequest:</span><span class="sxs-lookup"><span data-stu-id="eee97-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="eee97-392">**IUserIdProvider 接口**</span><span class="sxs-lookup"><span data-stu-id="eee97-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="eee97-393">默认情况下将使用用户的 IPrincipal.Identity.Name 作为用户名的实现。</span><span class="sxs-lookup"><span data-stu-id="eee97-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="eee97-394">在中心，你将能够将消息发送到这些用户通过一个新的 API:</span><span class="sxs-lookup"><span data-stu-id="eee97-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="eee97-395">**使用 Clients.User API**</span><span class="sxs-lookup"><span data-stu-id="eee97-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="eee97-396">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="eee97-396">Better Error Handling Support</span></span>

<span data-ttu-id="eee97-397">用户现在可能会引发**HubException**从任何集线器调用。</span><span class="sxs-lookup"><span data-stu-id="eee97-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="eee97-398">构造函数**HubException**字符串消息和对象可能需要额外的错误数据。</span><span class="sxs-lookup"><span data-stu-id="eee97-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="eee97-399">SignalR 将自动序列化异常，并将其发送到客户端，它将用于拒绝/失败集线器方法调用。</span><span class="sxs-lookup"><span data-stu-id="eee97-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="eee97-400">**显示详细的中心异常**设置没有任何影响**HubException**发回到客户端或不是; 它始终发送。</span><span class="sxs-lookup"><span data-stu-id="eee97-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="eee97-401">**演示将 HubException 发送到客户端的服务器端代码**</span><span class="sxs-lookup"><span data-stu-id="eee97-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="eee97-402">**演示从服务器发送 HubException 响应的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="eee97-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="eee97-403">**演示从服务器发送 HubException 响应的.NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="eee97-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="eee97-404">更轻松的单元测试的中心</span><span class="sxs-lookup"><span data-stu-id="eee97-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="eee97-405">SignalR 2.0 包括一个称为接口`IHubCallerConnectionContext`中心，可简化创建端调用的模拟客户端上。</span><span class="sxs-lookup"><span data-stu-id="eee97-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="eee97-406">下面的代码段演示如何使用常用的测试工具使用此接口[xUnit.net](https://github.com/xunit/xunit)并[moq](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="eee97-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="eee97-407">**使用单元测试 SignalR xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="eee97-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="eee97-408">**单元测试使用 moq SignalR**</span><span class="sxs-lookup"><span data-stu-id="eee97-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="eee97-409">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="eee97-409">JavaScript error handling</span></span>

<span data-ttu-id="eee97-410">在 SignalR 2.0 中，所有 JavaScript 错误处理回调都返回 JavaScript 错误对象，而不是原始字符串。</span><span class="sxs-lookup"><span data-stu-id="eee97-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="eee97-411">这样，SignalR 流动到错误处理程序更丰富的信息。</span><span class="sxs-lookup"><span data-stu-id="eee97-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="eee97-412">可以获取来自内部异常`source`错误的属性。</span><span class="sxs-lookup"><span data-stu-id="eee97-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="eee97-413">**JavaScript 客户端代码处理 Start.Fail 异常**</span><span class="sxs-lookup"><span data-stu-id="eee97-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="eee97-414">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="eee97-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="eee97-415">新的 ASP.NET 成员身份系统</span><span class="sxs-lookup"><span data-stu-id="eee97-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="eee97-416">ASP.NET 标识是为 ASP.NET 应用程序的新成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="eee97-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="eee97-417">ASP.NET 标识，可以轻松地将特定于用户的配置文件数据与应用程序数据集成。</span><span class="sxs-lookup"><span data-stu-id="eee97-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="eee97-418">ASP.NET 标识还可以选择在应用程序中的用户配置文件的持久性模型。</span><span class="sxs-lookup"><span data-stu-id="eee97-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="eee97-419">你可以将数据存储在 SQL Server 数据库或其他数据存储，包括 Azure 存储表等 NoSQL 数据存储。</span><span class="sxs-lookup"><span data-stu-id="eee97-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="eee97-420">有关详细信息，请参阅[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="eee97-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="eee97-421">基于声明的身份验证</span><span class="sxs-lookup"><span data-stu-id="eee97-421">Claims-based authentication</span></span>

<span data-ttu-id="eee97-422">ASP.NET 现在支持基于声明的身份验证，其中用户的标识都表示为一组从受信任的颁发者的声明。</span><span class="sxs-lookup"><span data-stu-id="eee97-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="eee97-423">用户可以是经过身份验证使用的用户名和密码保留在应用程序数据库中，也可以使用社交标识提供者 (例如： Microsoft 帐户、 Facebook、 Google、 Twitter)，或使用通过 Azure Active Directory 的组织帐户或Active Directory 联合身份验证服务 (ADFS)。</span><span class="sxs-lookup"><span data-stu-id="eee97-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="eee97-424">与 Azure Active Directory 和 Windows Server Active Directory 的集成</span><span class="sxs-lookup"><span data-stu-id="eee97-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="eee97-425">现在可以创建使用 Azure Active Directory 或 Windows Server Active Directory (AD) 进行身份验证的 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="eee97-426">有关详细信息，请参阅[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)中**在 Visual Studio 2013 中创建 ASP.NET Web 项目**。</span><span class="sxs-lookup"><span data-stu-id="eee97-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="eee97-427">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="eee97-427">OWIN Integration</span></span>

<span data-ttu-id="eee97-428">ASP.NET 身份验证现在基于可在任何基于 OWIN 的主机使用的 OWIN 中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="eee97-429">有关 OWIN 的详细信息，请参阅以下[Microsoft OWIN 组件](#TOC7)部分。</span><span class="sxs-lookup"><span data-stu-id="eee97-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="eee97-430">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="eee97-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="eee97-431">[用于.NET 开放 Web 接口](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="eee97-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="eee97-432">OWIN 将分离 web 应用程序从服务器中，使 web 应用程序主机不可知。</span><span class="sxs-lookup"><span data-stu-id="eee97-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="eee97-433">例如，可以托管在 IIS 中的基于 OWIN 的 web 应用程序或自承载服务中的自定义进程。</span><span class="sxs-lookup"><span data-stu-id="eee97-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="eee97-434">Microsoft OWIN 组件 （也称为 Katana 项目） 中引入的更改包括新的服务器和主机组件、 新的帮助程序库和中间件和新的身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="eee97-435">有关 OWIN 和 Katana 的详细信息，请参阅[什么是新的 OWIN 和 Katana](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="eee97-436">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序不能在 IIS 经典模式下运行; 它们必须在集成模式下运行。**</span><span class="sxs-lookup"><span data-stu-id="eee97-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="eee97-437">**注意： [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)必须以完全信任运行的应用程序。**</span><span class="sxs-lookup"><span data-stu-id="eee97-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="eee97-438">新的服务器和主机</span><span class="sxs-lookup"><span data-stu-id="eee97-438">New Servers and Hosts</span></span>

<span data-ttu-id="eee97-439">此版本中，添加了新的组件以启用自承载方案。</span><span class="sxs-lookup"><span data-stu-id="eee97-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="eee97-440">这些组件包括以下 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="eee97-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="eee97-441">**Microsoft.Owin.Host.HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="eee97-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="eee97-442">提供使用的 OWIN 服务器**HttpListener**侦听 HTTP 请求并将它们定向到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="eee97-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="eee97-443">**Microsoft.Owin.Hosting**的开发人员想要自托管 OWIN 管道中自定义过程，如控制台应用程序或 Windows 服务提供了一个库。</span><span class="sxs-lookup"><span data-stu-id="eee97-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="eee97-444">**OwinHost**。</span><span class="sxs-lookup"><span data-stu-id="eee97-444">**OwinHost**.</span></span> <span data-ttu-id="eee97-445">提供了独立的可执行文件，用于包装`Microsoft.Owin.Hosting`，并允许您自托管 OWIN 管道，而无需编写自定义主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="eee97-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="eee97-446">此外，`Microsoft.Owin.Host.SystemWeb`包现在允许中间件来提供对提示**SystemWeb**服务器，它指示应在特定的 ASP.NET 管道阶段调用中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="eee97-447">此功能时尤其有用身份验证中间件，应尽早在 ASP.NET 管道中运行。</span><span class="sxs-lookup"><span data-stu-id="eee97-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="eee97-448">帮助程序库和中间件</span><span class="sxs-lookup"><span data-stu-id="eee97-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="eee97-449">尽管您可以编写使用只有函数和类型定义了 OWIN 规范，从 OWIN 组件的新`Microsoft.Owin`包提供一组更为用户友好的抽象。</span><span class="sxs-lookup"><span data-stu-id="eee97-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="eee97-450">此包将合并多个早期包 (例如， `Owin.Extensions`， `Owin.Types`) 到结构良好的单个对象模型中，然后可以按其他 OWIN 组件易于使用。</span><span class="sxs-lookup"><span data-stu-id="eee97-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="eee97-451">实际上，大多数 Microsoft OWIN 组件现在使用此包。</span><span class="sxs-lookup"><span data-stu-id="eee97-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="eee97-452">[OWIN](http://www.owin.org)应用程序不能在 IIS 经典模式下运行; 它们必须在集成模式下运行。</span><span class="sxs-lookup"><span data-stu-id="eee97-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="eee97-453">[OWIN](http://www.owin.org)必须以完全信任运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="eee97-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="eee97-454">此版本还包括 Microsoft.Owin.Diagnostics 包，其中包括中间件来验证正在运行的 OWIN 应用程序，以及错误页中间件，以帮助调查故障。</span><span class="sxs-lookup"><span data-stu-id="eee97-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="eee97-455">身份验证组件</span><span class="sxs-lookup"><span data-stu-id="eee97-455">Authentication Components</span></span>

<span data-ttu-id="eee97-456">提供的以下身份验证组件。</span><span class="sxs-lookup"><span data-stu-id="eee97-456">The following authentication components are available.</span></span>

- <span data-ttu-id="eee97-457">**Microsoft.Owin.Security.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="eee97-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="eee97-458">启用身份验证使用在本地或基于云的目录服务。</span><span class="sxs-lookup"><span data-stu-id="eee97-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="eee97-459">**Microsoft.Owin.Security.Cookies**启用身份验证使用 cookie。</span><span class="sxs-lookup"><span data-stu-id="eee97-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="eee97-460">此包以前名为`Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="eee97-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="eee97-461">**Microsoft.Owin.Security.Facebook**启用身份验证使用 Facebook 的基于 OAuth 的服务。</span><span class="sxs-lookup"><span data-stu-id="eee97-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="eee97-462">**Microsoft.Owin.Security.Google**启用身份验证使用 Google 的基于 OpenID 的服务。</span><span class="sxs-lookup"><span data-stu-id="eee97-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="eee97-463">**Microsoft.Owin.Security.Jwt**启用身份验证使用 JWT 令牌。</span><span class="sxs-lookup"><span data-stu-id="eee97-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="eee97-464">**Microsoft.Owin.Security.MicrosoftAccount**启用身份验证使用 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="eee97-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="eee97-465">**Microsoft.Owin.Security.OAuth**。</span><span class="sxs-lookup"><span data-stu-id="eee97-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="eee97-466">提供对持有者令牌进行身份验证的 OAuth 授权服务器以及中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="eee97-467">**Microsoft.Owin.Security.Twitter**启用身份验证使用 Twitter 的基于 OAuth 的服务。</span><span class="sxs-lookup"><span data-stu-id="eee97-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="eee97-468">此版本还包括`Microsoft.Owin.Cors`包，其中包含用于处理跨域 HTTP 请求的中间件。</span><span class="sxs-lookup"><span data-stu-id="eee97-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="eee97-469">对 JWT 签名的支持已在 Visual Studio 2013 的最终版本中已删除。</span><span class="sxs-lookup"><span data-stu-id="eee97-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="eee97-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="eee97-470">Entity Framework 6</span></span>

<span data-ttu-id="eee97-471">有关新功能和 Entity Framework 6 中的其他更改的列表，请参阅[Entity Framework 版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="eee97-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="eee97-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="eee97-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="eee97-473">ASP.NET Razor 3 包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="eee97-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="eee97-474">支持选项卡上编辑。</span><span class="sxs-lookup"><span data-stu-id="eee97-474">Support for Tab editing.</span></span> <span data-ttu-id="eee97-475">Preivously，**格式的文档**命令、 自动缩进和格式设置在 Visual Studio 中的自动未正常工作时使用**保留选项卡**选项。</span><span class="sxs-lookup"><span data-stu-id="eee97-475">Preivously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="eee97-476">此更改更正了 Visual Studio 的格式设置选项卡的 Razor 代码格式设置。</span><span class="sxs-lookup"><span data-stu-id="eee97-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="eee97-477">对 URL 重写规则时生成链接的支持。</span><span class="sxs-lookup"><span data-stu-id="eee97-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="eee97-478">删除的安全透明特性。</span><span class="sxs-lookup"><span data-stu-id="eee97-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="eee97-479">这是一项重大更改，并使 Razor 3 不兼容与 MVC4 及更早版本，而 Razor 2 是与 MVC5 或针对 MVC5 编译的程序集不兼容。</span><span class="sxs-lookup"><span data-stu-id="eee97-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="eee97-480">可在预发行版中已修复 Visual Studio 2013 中的 razor 3 问题[此处](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="eee97-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="eee97-481">ASP.NET 应用挂起</span><span class="sxs-lookup"><span data-stu-id="eee97-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="eee97-482">ASP.NET 应用程序挂起是从根本上更改的用户体验和承载的 ASP.NET 站点一台计算机上的较大数字的经济模型在.NET Framework 4.5.1 中的改变游戏规则的功能。</span><span class="sxs-lookup"><span data-stu-id="eee97-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="eee97-483">有关详细信息，请参阅[ASP.NET 应用挂-响应迅速的共享.NET web 宿主](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eee97-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="eee97-484">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="eee97-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="eee97-485">本部分介绍了适用于 Visual Studio 2013 的已知的问题和 ASP.NET 和 Web 工具中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="eee97-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="eee97-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="eee97-486">NuGet</span></span>

- <span data-ttu-id="eee97-487">[新的包还原不起作用 Mono 使用 SLN 文件时](https://nuget.codeplex.com/workitem/3596)– 将在即将发布的 nuget.exe 下载修复并[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新。</span><span class="sxs-lookup"><span data-stu-id="eee97-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="eee97-488">[新的包还原不使用 Wix 项目](https://nuget.codeplex.com/workitem/3598)– 将在即将发布的 nuget.exe 下载修复并[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新。</span><span class="sxs-lookup"><span data-stu-id="eee97-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="eee97-489">[自动包还原不适用于解决方案文件夹下的项目](https://nuget.codeplex.com/workitem/3625)– 将在 NuGet 2.8 中修复。</span><span class="sxs-lookup"><span data-stu-id="eee97-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="eee97-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="eee97-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="eee97-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` 不会返回`IQueryable<T>`随着我们添加了对始终`$select`和`$expand`。</span><span class="sxs-lookup"><span data-stu-id="eee97-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="eee97-492">适用于我们早期示例`ODataQueryOptions<T>`始终强制转换后的返回值从`ApplyTo`到`IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="eee97-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="eee97-493">这以前工作正常查询选项，因为我们前面所支持 (`$filter`， `$orderby`， `$skip`， `$top`) 不更改查询的形状。</span><span class="sxs-lookup"><span data-stu-id="eee97-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="eee97-494">现在，我们支持`$select`并`$expand`的返回值`ApplyTo`不会`IQueryable<T>`始终。</span><span class="sxs-lookup"><span data-stu-id="eee97-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="eee97-495">如果使用从前面的示例代码，它将继续工作，如果客户端不会发送`$select`和`$expand`。</span><span class="sxs-lookup"><span data-stu-id="eee97-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="eee97-496">但是，如果你想要支持`$select`和`$expand`必须将该代码更改为。</span><span class="sxs-lookup"><span data-stu-id="eee97-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="eee97-497">**批处理请求过程的 Request.Url 或 RequestContext.Url 为 null**</span><span class="sxs-lookup"><span data-stu-id="eee97-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="eee97-498">在批处理方案中， **UrlHelper**为 null 时从访问**Request.Url**或**RequestContext.Url**。</span><span class="sxs-lookup"><span data-stu-id="eee97-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="eee97-499">当前此处跟踪此问题： [BatchRequestContext.Url 为 null 的批处理请求](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="eee97-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="eee97-500">此问题的解决方法是创建的新实例**UrlHelper**，如下面的示例：</span><span class="sxs-lookup"><span data-stu-id="eee97-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="eee97-501">**创建新的 UrlHelper 实例**</span><span class="sxs-lookup"><span data-stu-id="eee97-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="eee97-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="eee97-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="eee97-503">当使用 MVC5 和 OrgAuth，如果具有视图 AntiForgerToken 验证来执行此操作，时可能遇到以下错误在发布后的视图的数据：</span><span class="sxs-lookup"><span data-stu-id="eee97-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="eee97-504">**错误**:</span><span class="sxs-lookup"><span data-stu-id="eee97-504">**Error**:</span></span>

    <span data-ttu-id="eee97-505">*'/' 应用程序中的服务器错误。*</span><span class="sxs-lookup"><span data-stu-id="eee97-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="eee97-506"><em>一个声明的类型<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>或<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>不存在上提供的 ClaimsIdentity 的。若要启用基于声明的身份验证的防伪令牌支持，请验证已配置的声明提供程序提供这两个生成的 ClaimsIdentity 实例上这些声明。如果已配置的声明提供程序改为使用不同的声明类型作为唯一标识符，这可以通过设置静态属性 AntiForgeryConfig.UniqueClaimTypeIdentifier 配置。</em></span><span class="sxs-lookup"><span data-stu-id="eee97-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="eee97-507">**解决方法**:</span><span class="sxs-lookup"><span data-stu-id="eee97-507">**Workaround**:</span></span>

    <span data-ttu-id="eee97-508">若要修复此错误的 Global.asax 中添加以下行：</span><span class="sxs-lookup"><span data-stu-id="eee97-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="eee97-509">这将修复的下一个版本。</span><span class="sxs-lookup"><span data-stu-id="eee97-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="eee97-510">升级到 MVC5 MVC4 应用程序之后, 生成解决方案并启动它。</span><span class="sxs-lookup"><span data-stu-id="eee97-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="eee97-511">您应该看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="eee97-511">You should see the following error:</span></span>

    <span data-ttu-id="eee97-512">[A]System.Web.WebPages.Razor.Configuration.HostSection 无法强制转换为 [B]System.Web.WebPages.Razor.Configuration.HostSection。</span><span class="sxs-lookup"><span data-stu-id="eee97-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="eee97-513">类型来自 System.Web.WebPages.Razor，Version = 2.0.0.0，区域性 = neutral，PublicKeyToken = 31bf3856ad364e35 上下文 Default 在位置中 C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll。</span><span class="sxs-lookup"><span data-stu-id="eee97-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="eee97-514">B 类型来自 System.Web.WebPages.Razor，版本 = 3.0.0.0，区域性 = 中性，PublicKeyToken = 31bf3856ad364e35 上下文 Default 在位置中 C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll。</span><span class="sxs-lookup"><span data-stu-id="eee97-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="eee97-515">若要解决上述错误，请打开*所有*中你的项目和，请执行以下的 Web.config 文件 （包括在视图文件夹中的）：</span><span class="sxs-lookup"><span data-stu-id="eee97-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="eee97-516">更新版本"4.0.0.0"的"System.Web.Mvc"的"5.0.0.0"的所有匹配的项。</span><span class="sxs-lookup"><span data-stu-id="eee97-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="eee97-517">更新版本"2.0.0.0"的"System.Web.Helpers"的所有匹配项&quot;System.Web.WebPages&quot;并&quot;System.Web.WebPages.Razor&quot;到"3.0.0.0"</span><span class="sxs-lookup"><span data-stu-id="eee97-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="eee97-518">例如，进行上述更改后，程序集绑定应如下所示：</span><span class="sxs-lookup"><span data-stu-id="eee97-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="eee97-519">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将 ASP.NET MVC 4 和 Web API 项目升级到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="eee97-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="eee97-520">当与 jQuery 非介入式验证使用客户端验证，验证消息有时是正确类型的 HTML input 元素 = number。</span><span class="sxs-lookup"><span data-stu-id="eee97-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="eee97-521">验证错误所需的值 （"年龄字段为必需"） 显示了当而不是正确的消息需要有效的数字的输入数无效。</span><span class="sxs-lookup"><span data-stu-id="eee97-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="eee97-522">此问题通常具有整数属性上创建和编辑视图模型找到基架代码使用。</span><span class="sxs-lookup"><span data-stu-id="eee97-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="eee97-523">若要解决此问题，请更改从编辑器帮助程序：</span><span class="sxs-lookup"><span data-stu-id="eee97-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="eee97-524">到:</span><span class="sxs-lookup"><span data-stu-id="eee97-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="eee97-525">ASP.NET MVC 5 不再支持部分信任。</span><span class="sxs-lookup"><span data-stu-id="eee97-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="eee97-526">将链接到 MVC 或 WebAPI 二进制文件的项目应删除[SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="eee97-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="eee97-527">删除这些属性将消除编译器错误，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eee97-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="eee97-528">请注意，为此，你的副作用不能在同一个应用程序中使用 4.0 和 5.0 程序集。</span><span class="sxs-lookup"><span data-stu-id="eee97-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="eee97-529">需要所有这些更新为 5.0。</span><span class="sxs-lookup"><span data-stu-id="eee97-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="eee97-530">SPA 模板与 Facebook 授权可能会导致不稳定 IE intranet 区域中托管的网站时</span><span class="sxs-lookup"><span data-stu-id="eee97-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="eee97-531">SPA 模板提供了使用 Facebook 的外部日志。</span><span class="sxs-lookup"><span data-stu-id="eee97-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="eee97-532">使用模板创建的项目本地运行时，登录可能会导致崩溃的 IE。</span><span class="sxs-lookup"><span data-stu-id="eee97-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="eee97-533">解决方案：</span><span class="sxs-lookup"><span data-stu-id="eee97-533">Solution:</span></span>

1. <span data-ttu-id="eee97-534">托管该网站在 internet 区域;或</span><span class="sxs-lookup"><span data-stu-id="eee97-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="eee97-535">在非 IE 浏览器中测试该方案。</span><span class="sxs-lookup"><span data-stu-id="eee97-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="eee97-536">Web 窗体基架</span><span class="sxs-lookup"><span data-stu-id="eee97-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="eee97-537">Web 窗体基架已从 VS2013 中删除，并将在 Visual Studio 的将来更新中提供。</span><span class="sxs-lookup"><span data-stu-id="eee97-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="eee97-538">但是，仍可以通过添加 MVC 依赖项和生成的 MVC 基架使用 Web 窗体项目中的基架。</span><span class="sxs-lookup"><span data-stu-id="eee97-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="eee97-539">你的项目将包含 Web 窗体和 MVC 的组合。</span><span class="sxs-lookup"><span data-stu-id="eee97-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="eee97-540">若要添加到 Web 窗体项目的 MVC，添加一个新的基架的项，然后选择**MVC 5 依赖项**。</span><span class="sxs-lookup"><span data-stu-id="eee97-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="eee97-541">选择最小或完整具体取决于您是否需要的所有内容文件，例如脚本。</span><span class="sxs-lookup"><span data-stu-id="eee97-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="eee97-542">然后，添加基架的项 mvc，将在你的项目中创建视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="eee97-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="eee97-543">MVC 和 Web API 基架-HTTP 404 找不到错误</span><span class="sxs-lookup"><span data-stu-id="eee97-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="eee97-544">如果将基架的项添加到项目时遇到错误，，则可能你的项目将会处于不一致的状态。</span><span class="sxs-lookup"><span data-stu-id="eee97-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="eee97-545">一些将基架所做的更改将被回滚，但其他更改，例如已安装的 NuGet 包，将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="eee97-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="eee97-546">如果回滚路由的配置更改，用户将收到 HTTP 404 错误时导航到已搭建基架的项。</span><span class="sxs-lookup"><span data-stu-id="eee97-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="eee97-547">解决方法：</span><span class="sxs-lookup"><span data-stu-id="eee97-547">Workaround:</span></span>

- <span data-ttu-id="eee97-548">若要对 MVC 修复此错误，请添加一个新的基架的项，然后选择 MVC 5 依赖项 （最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="eee97-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="eee97-549">此过程将向你的项目添加所有所需的更改。</span><span class="sxs-lookup"><span data-stu-id="eee97-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="eee97-550">若要对 Web API 来修复此错误：</span><span class="sxs-lookup"><span data-stu-id="eee97-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="eee97-551">将 WebApiConfig 类添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="eee97-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="eee97-552">应用程序中配置 WebApiConfig.Register\_Global.asax 中的 Start 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eee97-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
