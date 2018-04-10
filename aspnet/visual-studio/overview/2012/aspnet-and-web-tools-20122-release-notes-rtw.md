---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web Tools 2012.2 的发行说明 |Microsoft 文档
author: rick-anderson
description: ASP.NET 和 Web Tools 2012.2 的发行说明。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2013
ms.topic: article
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: ab1642f1a3de298919aa9c6c1ddbd6bbb0cb99b5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
<a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="2b1be-103">ASP.NET 和 Web Tools 2012.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="2b1be-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>
====================
> <span data-ttu-id="2b1be-104">本文档介绍 ASP.NET 和 Web Tools 2012.2 发行的版本。</span><span class="sxs-lookup"><span data-stu-id="2b1be-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="2b1be-105">它是对 Visual Studio Web 工具和 ASP.NET 的更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>


- [<span data-ttu-id="2b1be-106">安装说明</span><span class="sxs-lookup"><span data-stu-id="2b1be-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="2b1be-107">文档</span><span class="sxs-lookup"><span data-stu-id="2b1be-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="2b1be-108">支持</span><span class="sxs-lookup"><span data-stu-id="2b1be-108">Support</span></span>](#_Support)
- [<span data-ttu-id="2b1be-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="2b1be-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="2b1be-110">ASP.NET 和 Web Tools 2012.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="2b1be-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="2b1be-111">工具</span><span class="sxs-lookup"><span data-stu-id="2b1be-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="2b1be-112">Web 发布</span><span class="sxs-lookup"><span data-stu-id="2b1be-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="2b1be-113">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="2b1be-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="2b1be-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2b1be-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="2b1be-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="2b1be-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="2b1be-116">ASP.NET 友好的 Url</span><span class="sxs-lookup"><span data-stu-id="2b1be-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="2b1be-117">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="2b1be-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="2b1be-118">安装说明</span><span class="sxs-lookup"><span data-stu-id="2b1be-118">Installation Notes</span></span>

<span data-ttu-id="2b1be-119">ASP.NET 和 Web Tools 2012.2 for Visual Studio 2012 可以使用安装[Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="2b1be-120">这是对 Visual Studio 2012 或 Visual Studio Express 2012 for Web，这是必需的更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="2b1be-121">如果你没有安装 Visual Studio，则将安装 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="2b1be-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="2b1be-122">你可以手动安装 ASP.NET 和 Web Tools 2012.2。</span><span class="sxs-lookup"><span data-stu-id="2b1be-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="2b1be-123">你必须具有 Visual Studio 2012 或 Visual Studio Express 2012 for Web 安装。</span><span class="sxs-lookup"><span data-stu-id="2b1be-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="2b1be-124">然后，使用以下说明：</span><span class="sxs-lookup"><span data-stu-id="2b1be-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="2b1be-125">下载[ASP.NET 和 Web 框架 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)从下载中心安装程序。</span><span class="sxs-lookup"><span data-stu-id="2b1be-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="2b1be-126">当提示的单击运行。</span><span class="sxs-lookup"><span data-stu-id="2b1be-126">When prompted click Run.</span></span> <span data-ttu-id="2b1be-127">你还可以保存该文件以更高版本运行。</span><span class="sxs-lookup"><span data-stu-id="2b1be-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="2b1be-128">验证你将更新的 Visual Studio 的版本。</span><span class="sxs-lookup"><span data-stu-id="2b1be-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="2b1be-129">可以通过启动 Visual Studio 你想要更新执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2b1be-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="2b1be-130">然后单击帮助菜单项。</span><span class="sxs-lookup"><span data-stu-id="2b1be-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="2b1be-131">如果你看到的菜单项&quot;有关 Microsoft Visual Studio 2012 for Web&quot;然后下载[Web 开发人员工具 2012.2-Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="2b1be-132">否则下载[Web 开发人员工具 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="2b1be-133">当提示的单击运行。</span><span class="sxs-lookup"><span data-stu-id="2b1be-133">When prompted click Run.</span></span> <span data-ttu-id="2b1be-134">你还可以保存该文件以更高版本运行。</span><span class="sxs-lookup"><span data-stu-id="2b1be-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="2b1be-135">ASP.NET 和 Web Tools 2012.2 版不包括 SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="2b1be-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="2b1be-136">SQL Server 和 Windows Azure SQL 数据库提供更丰富的数据库工具包括脱机支持项目的开发，架构比较和增强的数据库部署功能集。</span><span class="sxs-lookup"><span data-stu-id="2b1be-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="2b1be-137">有关详细信息或要安装 SQL Server Data Tools，请访问[ https://go.microsoft.com/fwlink/?LinkID=237127 ](https://go.microsoft.com/fwlink/?LinkID=237127)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="2b1be-138">文档</span><span class="sxs-lookup"><span data-stu-id="2b1be-138">Documentation</span></span>

<span data-ttu-id="2b1be-139">教程和有关 ASP.NET 和 Web Tools 2012.2 的其他信息可以从 ASP.NET web 站点 ( https://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="2b1be-140">支持</span><span class="sxs-lookup"><span data-stu-id="2b1be-140">Support</span></span>

<span data-ttu-id="2b1be-141">ASP.NET 和 Web Tools 2012.2 是正式发布，支持。</span><span class="sxs-lookup"><span data-stu-id="2b1be-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="2b1be-142">你可以使用你正常支持渠道。</span><span class="sxs-lookup"><span data-stu-id="2b1be-142">You can use your normal support channel.</span></span> <span data-ttu-id="2b1be-143">此外可以将问题发布到 ASP.NET 论坛 ([https://forums.asp.net/](https://forums.asp.net/))，其中 ASP.NET 社区的成员都是经常能够提供非正式的支持。</span><span class="sxs-lookup"><span data-stu-id="2b1be-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="2b1be-144">软件要求</span><span class="sxs-lookup"><span data-stu-id="2b1be-144">Software Requirements</span></span>

<span data-ttu-id="2b1be-145">ASP.NET 和 Web Tools 2012.2 需要 Visual Studio 2012 或 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="2b1be-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="2b1be-146">ASP.NET 和 Web Tools 2012.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="2b1be-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="2b1be-147">本部分介绍已在 ASP.NET 和 Web Tools 2012.2 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="2b1be-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="2b1be-148">工具</span><span class="sxs-lookup"><span data-stu-id="2b1be-148">Tooling</span></span>

- <span data-ttu-id="2b1be-149">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="2b1be-149">Page Inspector</span></span> 

    - <span data-ttu-id="2b1be-150">支持 JavaScript 选择映射允许 Page inspector 设置为将动态添加到页面回发到相应的 JavaScript 代码的项映射。</span><span class="sxs-lookup"><span data-stu-id="2b1be-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="2b1be-151">请参阅 CSS 的能力会在实时更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="2b1be-152">详细信息，请阅读[CSS 自动同步和在 Page Inspector 的 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="2b1be-153">编辑器</span><span class="sxs-lookup"><span data-stu-id="2b1be-153">Editor</span></span> 

    - <span data-ttu-id="2b1be-154">支持语法突出显示的 CoffeeScript、 Mustache、 车和 JsRender。</span><span class="sxs-lookup"><span data-stu-id="2b1be-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="2b1be-155">HTML 编辑器提供 Intellisense Knockout 绑定。</span><span class="sxs-lookup"><span data-stu-id="2b1be-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="2b1be-156">较少的编辑和编译器支持启用生成使用小于动态 CSS。</span><span class="sxs-lookup"><span data-stu-id="2b1be-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="2b1be-157">将 JSON 粘贴为一个.NET 类。</span><span class="sxs-lookup"><span data-stu-id="2b1be-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="2b1be-158">使用此特殊粘贴命令来将 JSON 粘贴到 C# 或 VB.NET 代码文件中和 Visual Studio 将自动生成从 JSON 推断出的.NET 类。</span><span class="sxs-lookup"><span data-stu-id="2b1be-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="2b1be-159">移动模拟器支持添加扩展性挂钩，以便可以作为 VSIX 安装第三方仿真程序。</span><span class="sxs-lookup"><span data-stu-id="2b1be-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="2b1be-160">安装仿真程序将显示在 F5 下拉列表中，以便开发人员可以预览自己的网站上的各种移动设备。</span><span class="sxs-lookup"><span data-stu-id="2b1be-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="2b1be-161">阅读有关在上 Scott Hanselman 的博客条目中此功能的详细信息[与 Visual Studio 的新 BrowserStack 集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="2b1be-162">Web 发布</span><span class="sxs-lookup"><span data-stu-id="2b1be-162">Web Publishing</span></span>

- <span data-ttu-id="2b1be-163">网站项目现在具有包括发布到 Windows Azure 网站的 Web 应用程序项目与相同的发布体验。</span><span class="sxs-lookup"><span data-stu-id="2b1be-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="2b1be-164">选择性发布&#8211;的一个或多个文件之后可以执行以下操作 （发布到 Web 部署的终结点）：</span><span class="sxs-lookup"><span data-stu-id="2b1be-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="2b1be-165">发布所选的文件。</span><span class="sxs-lookup"><span data-stu-id="2b1be-165">Publish selected files.</span></span>
    - <span data-ttu-id="2b1be-166">请参阅本地文件和远程文件之间的差异。</span><span class="sxs-lookup"><span data-stu-id="2b1be-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="2b1be-167">使用远程文件更新本地文件或使用本地文件更新远程文件。</span><span class="sxs-lookup"><span data-stu-id="2b1be-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="2b1be-168">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="2b1be-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="2b1be-169">新的 Facebook 应用程序模板可以编写简单的应用程序的 Facebook 画布。</span><span class="sxs-lookup"><span data-stu-id="2b1be-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="2b1be-170">在几个简单步骤，你可以创建的 Facebook 应用程序在已登录用户从获取数据并与他们的朋友集成。</span><span class="sxs-lookup"><span data-stu-id="2b1be-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="2b1be-171">该模板包含新的库来处理无足轻重的所有生成 Facebook 应用程序，包括身份验证，访问 Facebook 数据以及更多的权限，所涉及的管道。</span><span class="sxs-lookup"><span data-stu-id="2b1be-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="2b1be-172">使用 Facebook 应用程序模板的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkID=269921 ](https://go.microsoft.com/fwlink/?LinkID=269921)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="2b1be-173">新的单页面应用程序 MVC 模板允许开发人员可以构建使用 HTML 5、 CSS 3 和常用 Knockout 和 jQuery JavaScript 库，基于 ASP.NET Web API 的客户端的交互式 web 应用。</span><span class="sxs-lookup"><span data-stu-id="2b1be-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="2b1be-174">该模板包含的"todo"列表应用程序演示如何构建使用 RESTful 服务器 API 的 JavaScript HTML5 应用程序的常见做法。</span><span class="sxs-lookup"><span data-stu-id="2b1be-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="2b1be-175">你可以阅读更多信息，请访问[ https://www.asp.net/single-page-application ](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="2b1be-176">你现在可以创建 VSIX 中，以便将新模板添加到 ASP.NET MVC 新项目对话框。</span><span class="sxs-lookup"><span data-stu-id="2b1be-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="2b1be-177">此处了解操作方法： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="2b1be-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="2b1be-178">FixedDisplayModes 包&#8211;MVC 项目模板已更新，以包括新的 FixedDisplayModes NuGet 包，其中包含一个 MVC 4 中的 bug 的解决方法。</span><span class="sxs-lookup"><span data-stu-id="2b1be-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="2b1be-179">有关包中包含此修补程序的详细信息，请参阅这篇博客文章 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) 从 MVC 团队。</span><span class="sxs-lookup"><span data-stu-id="2b1be-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="2b1be-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2b1be-180">ASP.NET Web API</span></span>

<span data-ttu-id="2b1be-181">ASP.NET Web API 进行了增强的几个新功能：</span><span class="sxs-lookup"><span data-stu-id="2b1be-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="2b1be-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="2b1be-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="2b1be-183">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="2b1be-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="2b1be-184">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="2b1be-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="2b1be-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="2b1be-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="2b1be-186">ASP.NET Web API OData，可通过任何数据源生成具有丰富的业务逻辑的 OData 终结点所需的灵活性。</span><span class="sxs-lookup"><span data-stu-id="2b1be-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="2b1be-187">使用 ASP.NET Web API OData 中，您将控制你想要公开的 OData 语义的量。</span><span class="sxs-lookup"><span data-stu-id="2b1be-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="2b1be-188">ASP.NET Web API OData 是附带的 ASP.NET MVC 4 项目模板，也可以从 NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata))。</span><span class="sxs-lookup"><span data-stu-id="2b1be-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="2b1be-189">ASP.NET Web API OData 当前支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="2b1be-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="2b1be-190">通过将 [Queryable] 特性应用启用 OData 查询语义。</span><span class="sxs-lookup"><span data-stu-id="2b1be-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="2b1be-191">轻松验证 OData 查询和限制的一套支持的查询选项、 运算符和函数。</span><span class="sxs-lookup"><span data-stu-id="2b1be-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="2b1be-192">参数绑定到 ODataQueryOptions 直接以获取的抽象语法树表示形式的查询，然后可以验证并应用于 IQueryable 或 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="2b1be-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="2b1be-193">通过指定 [Queryable] 属性的结果限制启用服务驱动的分页和下一步生成的页面链接。</span><span class="sxs-lookup"><span data-stu-id="2b1be-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="2b1be-194">请求的使用 $inlinecount 的匹配资源总数的内联的计数。</span><span class="sxs-lookup"><span data-stu-id="2b1be-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="2b1be-195">控制 null 传播。</span><span class="sxs-lookup"><span data-stu-id="2b1be-195">Control null propagation.</span></span>
- <span data-ttu-id="2b1be-196">$Filter 中的任何/所有运算符。</span><span class="sxs-lookup"><span data-stu-id="2b1be-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="2b1be-197">按照约定推断实体数据模型或显式自定义的方式类似到实体框架代码的第一个模型。</span><span class="sxs-lookup"><span data-stu-id="2b1be-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="2b1be-198">公开的实体集从 EntitySetController 派生。</span><span class="sxs-lookup"><span data-stu-id="2b1be-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="2b1be-199">用于公开导航属性，操作链接和实现 OData 操作的简单的自定义约定。</span><span class="sxs-lookup"><span data-stu-id="2b1be-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="2b1be-200">简化使用 MapODataRoute 扩展方法进行路由。</span><span class="sxs-lookup"><span data-stu-id="2b1be-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="2b1be-201">通过公开多个 EDM 模型的版本控制支持。</span><span class="sxs-lookup"><span data-stu-id="2b1be-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="2b1be-202">为你的 Web API 公开的服务文档和 $metadata 以便你可以生成客户端 （.NET、 Windows Phone、 Windows 应用商店等）。</span><span class="sxs-lookup"><span data-stu-id="2b1be-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="2b1be-203">对 OData Atom、 JSON 和 JSON 详细格式的支持。</span><span class="sxs-lookup"><span data-stu-id="2b1be-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="2b1be-204">创建、 更新、 部分更新 (PATCH) 和删除实体。</span><span class="sxs-lookup"><span data-stu-id="2b1be-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="2b1be-205">查询和操作实体之间的关系。</span><span class="sxs-lookup"><span data-stu-id="2b1be-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="2b1be-206">创建连接路由到的关系链接。</span><span class="sxs-lookup"><span data-stu-id="2b1be-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="2b1be-207">复杂类型。</span><span class="sxs-lookup"><span data-stu-id="2b1be-207">Complex types.</span></span>
- <span data-ttu-id="2b1be-208">实体类型继承。</span><span class="sxs-lookup"><span data-stu-id="2b1be-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="2b1be-209">集合属性。</span><span class="sxs-lookup"><span data-stu-id="2b1be-209">Collection properties.</span></span>
- <span data-ttu-id="2b1be-210">枚举。</span><span class="sxs-lookup"><span data-stu-id="2b1be-210">Enums.</span></span>
- <span data-ttu-id="2b1be-211">OData 操作。</span><span class="sxs-lookup"><span data-stu-id="2b1be-211">OData actions.</span></span>
- <span data-ttu-id="2b1be-212">作为 WCF 数据服务，即 ODataLib 相同的基础之上构建 ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata))。</span><span class="sxs-lookup"><span data-stu-id="2b1be-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="2b1be-213">有关 ASP.NET Web API OData 的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkId=271141 ](https://go.microsoft.com/fwlink/?LinkId=271141)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="2b1be-214">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="2b1be-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="2b1be-215">ASP.NET Web API 跟踪与.NET 跟踪集成，从你的 web Api 的跟踪数据。</span><span class="sxs-lookup"><span data-stu-id="2b1be-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="2b1be-216">默认情况下，Web API 项目模板中现在启用它。</span><span class="sxs-lookup"><span data-stu-id="2b1be-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="2b1be-217">跟踪数据的你的 web Api 发送到输出窗口和通过 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="2b1be-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="2b1be-218">ASP.NET Web API Tracing 使您能够了解你的 Web API 时通过与集成在 Windows Azure 上托管的跟踪信息[Windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="2b1be-219">此外可以安装并启用在使用 ASP.NET Web API 跟踪 NuGet 包的任何应用程序中的 ASP.NET Web API Tracing ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing))。</span><span class="sxs-lookup"><span data-stu-id="2b1be-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="2b1be-220">有关配置和使用 ASP.NET Web API Tracing 的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkID=269874 ](https://go.microsoft.com/fwlink/?LinkID=269874)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="2b1be-221">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="2b1be-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="2b1be-222">默认情况下，Web API 项目模板中现在包含 ASP.NET Web API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="2b1be-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="2b1be-223">ASP.NET Web API 帮助页自动生成 web Api 包括 HTTP 终结点、 支持的 HTTP 方法、 参数和示例请求和响应消息负载的文档。</span><span class="sxs-lookup"><span data-stu-id="2b1be-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="2b1be-224">从代码中的注释自动拉取文档。</span><span class="sxs-lookup"><span data-stu-id="2b1be-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="2b1be-225">此外可以向任何应用程序使用 ASP.NET Web API 帮助页 NuGet 包添加 ASP.NET Web API 帮助页 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage))。</span><span class="sxs-lookup"><span data-stu-id="2b1be-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="2b1be-226">有关详细信息来设置和自定义 ASP.NET Web API 帮助页，请参阅[ https://go.microsoft.com/fwlink/?LinkId=271140 ](https://go.microsoft.com/fwlink/?LinkId=271140)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="2b1be-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="2b1be-227">ASP.NET SignalR</span></span>

<span data-ttu-id="2b1be-228">ASP.NET SignalR 非常容易地将实时 web 功能添加到 ASP.NET 应用程序，使用 Websocket，如果可用，并自动回退到其他技术时它不可以。</span><span class="sxs-lookup"><span data-stu-id="2b1be-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="2b1be-229">有关使用 ASP.NET SignalR 的详细信息请参阅[ https://go.microsoft.com/fwlink/?LinkId=271271 ](https://go.microsoft.com/fwlink/?LinkId=271271)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="2b1be-230">ASP.NET 友好的 Url</span><span class="sxs-lookup"><span data-stu-id="2b1be-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="2b1be-231">ASP.NET FriendlyURLs 使非常简便 web 窗体开发人员能够生成清除器正在 Url 查找 （无.aspx 扩展名）。</span><span class="sxs-lookup"><span data-stu-id="2b1be-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="2b1be-232">它需要的没有配置少，并可与现有的 ASP.NET v4.0 应用程序使用。</span><span class="sxs-lookup"><span data-stu-id="2b1be-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="2b1be-233">FriendlyURLs 功能还便于开发人员能够将移动支持添加到其应用程序，通过支持桌面和移动视图之间切换。</span><span class="sxs-lookup"><span data-stu-id="2b1be-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="2b1be-234">安装和使用 ASP.NET 友好 Url 的详细信息请参阅[ http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx ](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="2b1be-235">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="2b1be-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="2b1be-236">本部分介绍已知的问题和 ASP.NET 和 Web Tools 2012.2 版本中的重大更改。</span><span class="sxs-lookup"><span data-stu-id="2b1be-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="2b1be-237">安装问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="2b1be-238">无序安装的 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2b1be-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="2b1be-239">在安装 ASP.NET 和 Web Tools 2012.2 需要修复操作之后，请安装其他 SKU 的 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="2b1be-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="2b1be-240">请考虑按以下顺序：</span><span class="sxs-lookup"><span data-stu-id="2b1be-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="2b1be-241">安装 Visual Studio 2012 Express for Web</span><span class="sxs-lookup"><span data-stu-id="2b1be-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="2b1be-242">安装 ASP.NET 和 Web Tools 2012.2</span><span class="sxs-lookup"><span data-stu-id="2b1be-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="2b1be-243">安装 Visual Studio 2012 Professional、 Premium 或 Ultimate</span><span class="sxs-lookup"><span data-stu-id="2b1be-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="2b1be-244">步骤 2 将仅导致为 Express for Web 安装更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="2b1be-245">若要确保在步骤 3 中安装的其他 SKU 包含更新将需要修复 ASP.NET 和 Web Tools 2012.2 安装的最后一个 sku 安装更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="2b1be-246">如果在步骤 1 中的 Sku 和 3 会反转也适用。</span><span class="sxs-lookup"><span data-stu-id="2b1be-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="2b1be-247">打开 Visual Studio 时，请安装 Microsoft ASP.NET 和 Web Tools 2012.2</span><span class="sxs-lookup"><span data-stu-id="2b1be-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="2b1be-248">如果在安装的 Microsoft ASP.NET 和 Web Tools 2012.2 过程打开 VS，Visual Studio 可能结束处于错误的状态。</span><span class="sxs-lookup"><span data-stu-id="2b1be-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="2b1be-249">建议用户关闭继续安装之前的 Visual Studio 的所有实例。</span><span class="sxs-lookup"><span data-stu-id="2b1be-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="2b1be-250">如果取消安装 ASP.NET 和 Web Tools 2012.2 的安装程序</span><span class="sxs-lookup"><span data-stu-id="2b1be-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="2b1be-251">取消 ASP.NET 和 Web Tools 2012.2 安装的安装程序将处于错误状态保留 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2b1be-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="2b1be-252">若要解决此问题，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="2b1be-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="2b1be-253">转到添加/删除程序</span><span class="sxs-lookup"><span data-stu-id="2b1be-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="2b1be-254">如果存在，请卸载 Microsoft ASP.NET 和 Web Tools 2012.2。</span><span class="sxs-lookup"><span data-stu-id="2b1be-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="2b1be-255">重新安装 Microsoft ASP.NET 和 Web Tools 2012.2</span><span class="sxs-lookup"><span data-stu-id="2b1be-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="2b1be-256">在卸载 ASP.NET 和 Web Tools 2012.2 ASP.NET MVC 4 后模板和 Razor v2 网站模板是缺少</span><span class="sxs-lookup"><span data-stu-id="2b1be-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="2b1be-257">卸载 ASP.NET 和 Web Tools 2012.2 则也将卸载所有的 ASP.NET MVC 4 和 Razor v2 网站模板从 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="2b1be-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="2b1be-258">解决方法是来修复 Visual Studio 2012 安装用于重新安装 ASP.NET MVC 4 和 Razor v2 网站模板。</span><span class="sxs-lookup"><span data-stu-id="2b1be-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="2b1be-259">工具问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="2b1be-260">在项目创建期间报告的 NuGet 错误</span><span class="sxs-lookup"><span data-stu-id="2b1be-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="2b1be-261">在安装 ASP.NET 和 Web Tools 2012.2 你可能会看到以下错误时创建的 MVC 4 项目</span><span class="sxs-lookup"><span data-stu-id="2b1be-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="2b1be-262">ASP.NET 和 Web Tools 2012.2 附带 NuGet 2.1，并将升级 Visual Studio 2012 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="2b1be-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="2b1be-263">在某些情况下，将无法正确更新 VSIX VSIX 安装程序。</span><span class="sxs-lookup"><span data-stu-id="2b1be-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="2b1be-264">以下步骤将允许你解决此问题：</span><span class="sxs-lookup"><span data-stu-id="2b1be-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="2b1be-265">以管理员身份启动 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2b1be-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="2b1be-266">转到 Tools-&gt;扩展和更新和卸载 NuGet。</span><span class="sxs-lookup"><span data-stu-id="2b1be-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="2b1be-267">关闭 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b1be-267">Close Visual Studio</span></span>
4. <span data-ttu-id="2b1be-268">导航到 ASP.NET 和 Web Tools 2012.2 安装文件夹：</span><span class="sxs-lookup"><span data-stu-id="2b1be-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="2b1be-269">对于 Visual Studio 2012:**程序 Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="2b1be-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="2b1be-270">有关 Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span><span class="sxs-lookup"><span data-stu-id="2b1be-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="2b1be-271">双击 NuGet.Tools.vsix 重新安装 NuGet</span><span class="sxs-lookup"><span data-stu-id="2b1be-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="2b1be-272">Web API 问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="2b1be-273">分析 $filter 和日期时间文本中的问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="2b1be-274">OData URI 分析器无法正确分析部分的日期时间文本中。</span><span class="sxs-lookup"><span data-stu-id="2b1be-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="2b1be-275">例如，$filter = 开始 eq 日期时间"2012年-12-31T12:00 无法正确分析。</span><span class="sxs-lookup"><span data-stu-id="2b1be-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="2b1be-276">一种解决方法是使用完整文本 $filter = 开始 eq 日期时间"2012年-12-31T12:00:00。</span><span class="sxs-lookup"><span data-stu-id="2b1be-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="2b1be-277">OData 不支持不区分大小写的属性名称。</span><span class="sxs-lookup"><span data-stu-id="2b1be-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="2b1be-278">OData 不支持 OData 查询和 odata 路径中的不区分大小写的属性名称。</span><span class="sxs-lookup"><span data-stu-id="2b1be-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="2b1be-279">工作项，请参阅：</span><span class="sxs-lookup"><span data-stu-id="2b1be-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="2b1be-280">如果用户具有 javascript 客户端和服务器端上的不同大小写，它们可能会遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="2b1be-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="2b1be-281">此问题是 odata 协议中的设计。</span><span class="sxs-lookup"><span data-stu-id="2b1be-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="2b1be-282">但是，许多用户会报告此问题。</span><span class="sxs-lookup"><span data-stu-id="2b1be-282">However, many users reports this issue.</span></span> <span data-ttu-id="2b1be-283">若要解决这个问题，用户必须更正它们在 URL 中的用例。</span><span class="sxs-lookup"><span data-stu-id="2b1be-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="2b1be-284">默认 OData 路由约定不支持 POST/PUT 导航属性。</span><span class="sxs-lookup"><span data-stu-id="2b1be-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="2b1be-285">默认 OData 路由约定不支持 POST/PUT 导航属性。</span><span class="sxs-lookup"><span data-stu-id="2b1be-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="2b1be-286">请参阅工作项[ http://aspnetwebstack.codeplex.com/workitem/366 ](http://aspnetwebstack.codeplex.com/workitem/366)。</span><span class="sxs-lookup"><span data-stu-id="2b1be-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="2b1be-287">我们缺少默认的约定中此常用的约定。</span><span class="sxs-lookup"><span data-stu-id="2b1be-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="2b1be-288">若要解决这个问题，用户需要扩展新种路由约定无法支持它。</span><span class="sxs-lookup"><span data-stu-id="2b1be-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="2b1be-289">Facebook 模板问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="2b1be-290">Facebook 应用程序模板只能是使用.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2b1be-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="2b1be-291">你必须在新项目对话框以查看 ASP.NET MVC 4 中的 Facebook 应用程序模板中的框架下拉列表中选择.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="2b1be-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="2b1be-292">实时更新控制器</span><span class="sxs-lookup"><span data-stu-id="2b1be-292">Real-time Update Controller</span></span>

<span data-ttu-id="2b1be-293">Facebook 应用程序模板允许用户轻松地创建一个 Web API 控制器来处理从 Facebook 的实时更新。</span><span class="sxs-lookup"><span data-stu-id="2b1be-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="2b1be-294">如果你的开发计算机位于 NAT 后面，你的控制器可能无法工作而无需进一步网络配置。</span><span class="sxs-lookup"><span data-stu-id="2b1be-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="2b1be-295">有关详细信息，请参阅此处： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="2b1be-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="2b1be-296">查询与 Facebook OAuth 参数的字符串值冲突</span><span class="sxs-lookup"><span data-stu-id="2b1be-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="2b1be-297">以下字段冲突 Facebook OAuth 对话框中的调用返回 URL。</span><span class="sxs-lookup"><span data-stu-id="2b1be-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="2b1be-298">不添加你自己的查询字符串值具有以下名称： 代码、 错误、 错误\_说明、 错误\_原因。</span><span class="sxs-lookup"><span data-stu-id="2b1be-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="2b1be-299">Page Inspector 使用 Facebook 模板</span><span class="sxs-lookup"><span data-stu-id="2b1be-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="2b1be-300">在调试 Facebook 应用程序时，不能在 Visual Studio 2012 中使用 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="2b1be-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="2b1be-301">Page Inspector 当前不支持 iframe。</span><span class="sxs-lookup"><span data-stu-id="2b1be-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="2b1be-302">单页面应用程序模板问题</span><span class="sxs-lookup"><span data-stu-id="2b1be-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="2b1be-303">使用 JQuery 1.9/Knockout 2.2.1 更新，运行默认 MVC SPA 项目中，新的 todo 项编辑时输入焦点事件不正确处理。</span><span class="sxs-lookup"><span data-stu-id="2b1be-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="2b1be-304">与 JQuery 1.9/Knockout 2.2.1 更新，当运行默认 MVC SPA 项目时，新的 todo 项编辑不再焦点回新的 todo 项编辑框后输入到 todo 列表中输入新的 todo 项。</span><span class="sxs-lookup"><span data-stu-id="2b1be-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="2b1be-305">解决方法引用[ http://knockoutjs.com/documentation/hasfocus-binding.html ](http://knockoutjs.com/documentation/hasfocus-binding.html)，并对下面的示例代码进行类似的修复：</span><span class="sxs-lookup"><span data-stu-id="2b1be-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="2b1be-306">文件 todo.model.js</span><span class="sxs-lookup"><span data-stu-id="2b1be-306">File todo.model.js</span></span>  
 <span data-ttu-id="2b1be-307">函数 todolist(data) 中，添加以下：</span><span class="sxs-lookup"><span data-stu-id="2b1be-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="2b1be-308">**self.isSelected = ko.observable(false);**</span><span class="sxs-lookup"><span data-stu-id="2b1be-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="2b1be-309">函数 todoList.prototype.addTodo 中，添加以下 blacked 的文本：</span><span class="sxs-lookup"><span data-stu-id="2b1be-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="2b1be-310">**self.isSelected(true);**</span><span class="sxs-lookup"><span data-stu-id="2b1be-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="2b1be-311">self.newTodoTitle(&quot;&quot;);</span><span class="sxs-lookup"><span data-stu-id="2b1be-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="2b1be-312">Index.cshtml 文件中，添加以下 blacked 的文本：</span><span class="sxs-lookup"><span data-stu-id="2b1be-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="2b1be-313">&lt;窗体数据绑定 =&quot;提交： addTodo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="2b1be-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="2b1be-314">&lt;输入类 =&quot;addTodo&quot;类型 =&quot;文本&quot;数据绑定 =&quot;值： newTodoTitle，占位符: Type 此处以添加、 blurOnEnter： 为 true，**有焦点： isSelected**，事件: {模糊： addTodo}&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="2b1be-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="2b1be-315">&lt;/form&gt;</span><span class="sxs-lookup"><span data-stu-id="2b1be-315">&lt;/form&gt;</span></span>
