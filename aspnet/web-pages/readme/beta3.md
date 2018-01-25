---
uid: web-pages/readme/beta3
title: "Web 矩阵和 ASP.NET Web 页 (Razor) Beta 3 版本自述文件 |Microsoft 文档"
author: rick-anderson
description: "Web Matrix 和 ASP.NET Web 页 (Razor) Beta 3 版本自述文件"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/10/2011
ms.topic: article
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: def2f4b3e54c8de539e10c1b526a1dababeca8fb
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="4a862-103">Web Matrix 和 ASP.NET Web 页 (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="4a862-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>
====================
> <span data-ttu-id="4a862-104">Web Matrix 和 ASP.NET Web 页 (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="4a862-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="4a862-105">2010 年 11 月 9日</span><span class="sxs-lookup"><span data-stu-id="4a862-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="4a862-106">内容</span><span class="sxs-lookup"><span data-stu-id="4a862-106">Contents</span></span>

- [<span data-ttu-id="4a862-107">概述</span><span class="sxs-lookup"><span data-stu-id="4a862-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="4a862-108">安装</span><span class="sxs-lookup"><span data-stu-id="4a862-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="4a862-109">新功能、 更改和 Beta 3 版本中的已知问题</span><span class="sxs-lookup"><span data-stu-id="4a862-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="4a862-110">WebMatrix 安装问题</span><span class="sxs-lookup"><span data-stu-id="4a862-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="4a862-111">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="4a862-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="4a862-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="4a862-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="4a862-113">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="4a862-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="4a862-114">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="4a862-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="4a862-115">其他问题</span><span class="sxs-lookup"><span data-stu-id="4a862-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="4a862-116">有关详细信息</span><span class="sxs-lookup"><span data-stu-id="4a862-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="4a862-117">概述</span><span class="sxs-lookup"><span data-stu-id="4a862-117">Overview</span></span>

> <span data-ttu-id="4a862-118">Microsoft WebMatrix Beta 是以分钟为单位安装免费的 web 开发堆栈。</span><span class="sxs-lookup"><span data-stu-id="4a862-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="4a862-119">它与数据库和编程框架创建单一的集成体验集成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="4a862-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="4a862-120">你可以使用 WebMatrix Beta 来简化的方法的代码、 测试和发布你自己的 ASP.NET 或 PHP 网站，或者你可以使用 WebMatrix Beta 以启动使用如 DotNetNuke、 Umbraco、 WordPress、 Joomla 的常用的开源应用程序的新网站。</span><span class="sxs-lookup"><span data-stu-id="4a862-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="4a862-121">WebMatrix Beta 使用相同的功能强大的 web 服务器、 数据库引擎和运行你的网站在 internet 上，从而可以从开发到生产环境的转换平滑无缝的框架环境。</span><span class="sxs-lookup"><span data-stu-id="4a862-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>


<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="4a862-122">安装</span><span class="sxs-lookup"><span data-stu-id="4a862-122">Installation</span></span>

> <span data-ttu-id="4a862-123">若要安装 WebMatrix Beta 3，你可以使用[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="4a862-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="4a862-124">安装 Web 平台安装程序后，可用于安装 WebMatrix Beta 3。</span><span class="sxs-lookup"><span data-stu-id="4a862-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="4a862-125">如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的故障排除问题](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="4a862-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>


<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="4a862-126">发布应用程序的说明</span><span class="sxs-lookup"><span data-stu-id="4a862-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="4a862-127">请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="4a862-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>


<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="4a862-128">新功能、 更改 andKnown 问题</span><span class="sxs-lookup"><span data-stu-id="4a862-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="4a862-129">WebMatrix Beta 3 安装</span><span class="sxs-lookup"><span data-stu-id="4a862-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="4a862-130">问题： WebMatrix Beta 3 才支持 Microsoft.NET Framework 4 的平台上可用</span><span class="sxs-lookup"><span data-stu-id="4a862-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="4a862-131">.NET Framework 版本 4 是必需的 WebMatrix Beta。</span><span class="sxs-lookup"><span data-stu-id="4a862-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="4a862-132">在某些情况下，WebMatrix Beta 安装程序将让你尝试在不受支持的配置集的一部分的平台上安装。</span><span class="sxs-lookup"><span data-stu-id="4a862-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="4a862-133">具体而言，不带 SP1 更新的 Windows Vista 将你可以开始安装 WebMatrix Beta，但该.NET Framework 4 组件将失败并阻止你安装。</span><span class="sxs-lookup"><span data-stu-id="4a862-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="4a862-134">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-134">**Workaround**</span></span>  
> <span data-ttu-id="4a862-135">安装上受支持的平台，其中包括：</span><span class="sxs-lookup"><span data-stu-id="4a862-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="4a862-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4a862-136">Windows 7</span></span>
> - <span data-ttu-id="4a862-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="4a862-137">Windows Server 2008</span></span>
> - <span data-ttu-id="4a862-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4a862-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="4a862-139">Windows Vista SP1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="4a862-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="4a862-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="4a862-140">Windows XP SP3</span></span>
> - <span data-ttu-id="4a862-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="4a862-141">Windows Server 2003 SP2</span></span>


#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="4a862-142">如果没有 Microsoft Visual Studio 2008 SP1 的情况下已安装 Microsoft Visual Studio 2008，问题： 不能安装 WebMatrix Beta 3</span><span class="sxs-lookup"><span data-stu-id="4a862-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="4a862-143">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-143">**Workaround**</span></span>  
> <span data-ttu-id="4a862-144">安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)从 Microsoft 下载中心获取。</span><span class="sxs-lookup"><span data-stu-id="4a862-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="4a862-145">问题： SQL Server Compact 4.0 某些程序集未安装在 GAC 中</span><span class="sxs-lookup"><span data-stu-id="4a862-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="4a862-146">在 64 位计算机上安装 SQL Server Compact 4.0 和计算机具有仅.NET Framework 3.5 SP1 客户端安装配置文件时，SQL Server Compact 4.0 的托管程序集不会放置在全局程序集缓存 (GAC)。</span><span class="sxs-lookup"><span data-stu-id="4a862-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="4a862-147">未安装在 GAC 中的托管程序集是：</span><span class="sxs-lookup"><span data-stu-id="4a862-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="4a862-148">*System.Data.SqlServerCe.dll* （ADO.NET 提供程序）</span><span class="sxs-lookup"><span data-stu-id="4a862-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="4a862-149">*System.Data.SqlServerCe.Entity.dll* （ADO.NET 实体框架）</span><span class="sxs-lookup"><span data-stu-id="4a862-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="4a862-150">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-150">**Workaround**</span></span>  
> <span data-ttu-id="4a862-151">卸载 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="4a862-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="4a862-152">下载并安装.NET Framework 3.5 SP1 的完整版本，从以下位置：</span><span class="sxs-lookup"><span data-stu-id="4a862-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="4a862-153">Microsoft.NET Framework 3.5 Service pack 1 （完全包）</span><span class="sxs-lookup"><span data-stu-id="4a862-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="4a862-154">然后重新安装 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="4a862-154">Then reinstall SQL Server Compact 4.0.</span></span>


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="4a862-155">问题： 无法卸载 SQL Server Compact 使用命令行</span><span class="sxs-lookup"><span data-stu-id="4a862-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="4a862-156">卸载 SQL Server Compact 使用命令行选项不在此版本中无效。</span><span class="sxs-lookup"><span data-stu-id="4a862-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="4a862-157">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-157">**Workaround**</span></span>  
> <span data-ttu-id="4a862-158">使用*程序和功能*Windows 控制面板卸载 Microsoft SQL Server Compact 4.0 中。</span><span class="sxs-lookup"><span data-stu-id="4a862-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="4a862-159">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="4a862-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="4a862-160">文档本部分介绍的新增功能、 更改和 Beta 3 版本的 ASP.NET Web Pages 使用 Razor 语法的已知的问题。</span><span class="sxs-lookup"><span data-stu-id="4a862-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="4a862-161">新功能</span><span class="sxs-lookup"><span data-stu-id="4a862-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="4a862-162">更改</span><span class="sxs-lookup"><span data-stu-id="4a862-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="4a862-163">问题</span><span class="sxs-lookup"><span data-stu-id="4a862-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4a862-164">使用 Razor 语法的 ASP.NET 网页测试版 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="4a862-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="4a862-165">"Html.Raw"方法呈现未编码的标记的新增内容：</span><span class="sxs-lookup"><span data-stu-id="4a862-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="4a862-166">新`Html.Raw`方法可让你呈现为而不是呈现编码的输出的标记的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="4a862-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="4a862-167">（默认情况下，ASP.NET Razor 编码字符串在呈现它们之前。）语法为：</span><span class="sxs-lookup"><span data-stu-id="4a862-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="4a862-168">下面的示例演示如何使用 `Html.Raw`：</span><span class="sxs-lookup"><span data-stu-id="4a862-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]


<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4a862-169">使用 Razor 语法的 ASP.NET 网页测试版 3 中的更改</span><span class="sxs-lookup"><span data-stu-id="4a862-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="4a862-170">删除的更改:"HrefAttribute"方法</span><span class="sxs-lookup"><span data-stu-id="4a862-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="4a862-171">`HrefAttribute`方法`WebPage`类已删除。</span><span class="sxs-lookup"><span data-stu-id="4a862-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="4a862-172">此帮助器用于在 Url 中的不安全字符进行编码。</span><span class="sxs-lookup"><span data-stu-id="4a862-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="4a862-173">它不再需要因为 ASP.NET Razor 自动对字符串进行编码。</span><span class="sxs-lookup"><span data-stu-id="4a862-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="4a862-174">(使用新`Html.Raw`方法呈现未编码的字符串。)</span><span class="sxs-lookup"><span data-stu-id="4a862-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>


#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="4a862-175">更改： 语法声明性"@helper"更改帮助器</span><span class="sxs-lookup"><span data-stu-id="4a862-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="4a862-176">在 Beta 3 版本中，ASP.NET 更改如何分析帮助程序，使用创建`@helper`语法。</span><span class="sxs-lookup"><span data-stu-id="4a862-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="4a862-177">从本质上讲，`@helper`语法现在解析为一个代码块而不是作为标记可以包含代码块。</span><span class="sxs-lookup"><span data-stu-id="4a862-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="4a862-178">因此，帮助器内的代码不需要用`@{ }`块。</span><span class="sxs-lookup"><span data-stu-id="4a862-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="4a862-179">相反，标记帮助器内的必须是显式包含在 HTML 元素或 ASP.NET Razor`<text></text>`标记。</span><span class="sxs-lookup"><span data-stu-id="4a862-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="4a862-180">例如，以下`@helper`语法适用于 Beta 3 版本：</span><span class="sxs-lookup"><span data-stu-id="4a862-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="4a862-181">在 Beta 3 版本中，必须更改此帮助器以类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="4a862-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="4a862-182">请注意，`@{ }`不再使用的初始代码的帮助程序中的字符。</span><span class="sxs-lookup"><span data-stu-id="4a862-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="4a862-183">这是因为以下帮助器的内容视为一个代码块，默认情况下。</span><span class="sxs-lookup"><span data-stu-id="4a862-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="4a862-184">帮助器呈现标记，开头开始`<a>`标记。</span><span class="sxs-lookup"><span data-stu-id="4a862-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="4a862-185">如果帮助器必须呈现的纯文本或不包含结束标记的标记 (例如，`<meta>`标记)，要呈现的内容必须在`<text></text>`标记。</span><span class="sxs-lookup"><span data-stu-id="4a862-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>


#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="4a862-186">Change: "WebPageContext.HttpContext" removed</span><span class="sxs-lookup"><span data-stu-id="4a862-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="4a862-187">`WebPageContext.HttpContext`属性已删除。</span><span class="sxs-lookup"><span data-stu-id="4a862-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="4a862-188">请改用 `HttpContext.Current`。</span><span class="sxs-lookup"><span data-stu-id="4a862-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="4a862-189">(`WebPageContext.HttpContext`属性只需包装这。)</span><span class="sxs-lookup"><span data-stu-id="4a862-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>


#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="4a862-190">移动到新的包的更改:"Facebook"帮助程序</span><span class="sxs-lookup"><span data-stu-id="4a862-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="4a862-191">`Facebook`帮助器已移至*Facebook.Helper*库，其中包括`Facebook`帮助器和其他功能。</span><span class="sxs-lookup"><span data-stu-id="4a862-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="4a862-192">你必须安装此库作为一个单独的包，"安装帮助器使用程序包管理器"中所述在本教程[Getting Started with ASP.NET 页](https://go.microsoft.com/fwlink/?LinkId=202889)。</span><span class="sxs-lookup"><span data-stu-id="4a862-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>


#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="4a862-193">更改： 成员资格、 角色和安全类型移动到新的程序集</span><span class="sxs-lookup"><span data-stu-id="4a862-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="4a862-194">以下类型都已移动到`WebMatrix.WebData`程序集：</span><span class="sxs-lookup"><span data-stu-id="4a862-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`


#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="4a862-195">移动到 System.Web.WebPages.dll 程序集的更改:"TagBuilder"类</span><span class="sxs-lookup"><span data-stu-id="4a862-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="4a862-196">`TagBuilde` R 类已移动到 System.Web.WebPages.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="4a862-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="4a862-197">以前，这样做的程序集中的是 ASP.NET MVC 的一部分。</span><span class="sxs-lookup"><span data-stu-id="4a862-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="4a862-198">此更改意味着你不需要安装 ASP.NET MVC，以便使用`TagBuilder`类。</span><span class="sxs-lookup"><span data-stu-id="4a862-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="4a862-199">但是，此类是仍在`System.Web.Mvc`命名空间。</span><span class="sxs-lookup"><span data-stu-id="4a862-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="4a862-200">若要使用`TagBuilder`类 （例如，在自定义 ASP.NET Razor 帮助程序），你必须引用命名空间 (例如，通过添加`@using System.Web.Mvc`到你的代码)。</span><span class="sxs-lookup"><span data-stu-id="4a862-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>


#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="4a862-201">更改： 请求验证语法更改;删除的"验证"类</span><span class="sxs-lookup"><span data-stu-id="4a862-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="4a862-202">在 Beta 3 版本中，若要禁用验证的单个字段或集的字段，你可以调用`Validation.Exclude`方法，同时传入的名称或从验证中排除的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="4a862-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="4a862-203">新的语法是跳过验证的 Beta 3 版本中可用。</span><span class="sxs-lookup"><span data-stu-id="4a862-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="4a862-204">`Validation`中 Beta 3 方法，用于已删除。</span><span class="sxs-lookup"><span data-stu-id="4a862-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="4a862-205">如果用户尝试上载 HTML 标记 （例如，通过在页面上使用的富文本编辑器） 未禁用请求验证，如果网站将报告类错误*从客户端检测到潜在危险的Request.Form值*和未接受用户输入。</span><span class="sxs-lookup"><span data-stu-id="4a862-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="4a862-206">如果禁用请求验证，你必须手动检查用户输入，以确保它不包含具有潜在危险标记或者脚本使用类似[Microsoft 反跨站点脚本库 V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)。</span><span class="sxs-lookup"><span data-stu-id="4a862-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="4a862-207">若要禁用自动请求验证，请调用`Request.Unvalidated`方法，将其传递的字段或你想要绕过请求验证的其他文章对象的名称。</span><span class="sxs-lookup"><span data-stu-id="4a862-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="4a862-208">你可以使用此方法绕过验证中的任何项`Form`， `QueryString`， `Cookies`，和`ServerVariables`集合。</span><span class="sxs-lookup"><span data-stu-id="4a862-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="4a862-209">下面的示例演示如何使用`Unvalidated`方法：</span><span class="sxs-lookup"><span data-stu-id="4a862-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]


<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4a862-210">使用 Razor 语法的 ASP.NET 网页的已知的问题</span><span class="sxs-lookup"><span data-stu-id="4a862-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="4a862-211">问题： 意外的行为时使用的成员身份的自定义用户表</span><span class="sxs-lookup"><span data-stu-id="4a862-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="4a862-212">若要初始化的成员资格提供程序的 ASP.NET Razor 网站，你可以调用`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="4a862-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="4a862-213">(在 WebMatrix 中，入门站点模板包括对在此方法的调用 *\_AppStart.cshtml*文件。)如果`autoCreateTables`此方法的参数设置为 true (默认情况下，它设置为 true 的入门站点模板中)，并且如果无法识别的表名称传递给方法 （第二个参数），该方法不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="4a862-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="4a862-214">相反，它会自动创建表。</span><span class="sxs-lookup"><span data-stu-id="4a862-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="4a862-215">这可能会造成问题，如果你想要使用的成员身份的自定义用户表，但传递到的错误的表名称`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="4a862-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="4a862-216">因为该方法不会默认情况下引发错误如果您指定的表不存在，而且它改为创建一个新表，则应用程序可以似乎无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="4a862-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="4a862-217">但是，依赖于自定义用户表 （和在其中的字段） 的应用程序代码可能最终失败，意外错误。</span><span class="sxs-lookup"><span data-stu-id="4a862-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="4a862-218">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-218">**Workaround**</span></span>  
> <span data-ttu-id="4a862-219">请确保名称传递中`InitializeDatabaseConnection`方法匹配项的用户配置文件表中成员资格数据库中，或确保`autoCreateTables`参数设置为 false。</span><span class="sxs-lookup"><span data-stu-id="4a862-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="4a862-220">问题:"无法生成 SQL Server 的用户实例"错误</span><span class="sxs-lookup"><span data-stu-id="4a862-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="4a862-221">如果 WebMatrix Web 应用程序使用 SQL Server Express 和 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="4a862-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="4a862-222">**解决方法**请确保应用程序 （通常网络服务） 下运行的 Windows 帐户如具有读/写权限的应用程序的根文件夹和子文件夹*应用\_数据*.</span><span class="sxs-lookup"><span data-stu-id="4a862-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="4a862-223">知识库文章中提供了更多详细的信息[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目问题](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="4a862-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="4a862-224">问题： 在 Visual Studio 中，自定义程序集 (Dll) 的命名空间不自动导入</span><span class="sxs-lookup"><span data-stu-id="4a862-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="4a862-225">如果你在 Visual Studio 中的项目中使用自定义程序集，这些程序集中声明的命名空间不自动导入在设计时。</span><span class="sxs-lookup"><span data-stu-id="4a862-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="4a862-226">因此，对自定义类型的引用可能无法识别设计时和标记为无法识别中的 Visual Studio （使用"波形曲线"）。</span><span class="sxs-lookup"><span data-stu-id="4a862-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="4a862-227">仅在 Visual Studio; 中的设计时出现此问题应用程序本身能够正常运行。</span><span class="sxs-lookup"><span data-stu-id="4a862-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="4a862-228">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-228">**Workaround**</span></span>  
> <span data-ttu-id="4a862-229">包括`using`语句 (`imports`在 Visual Basic 中) 引用在设计时无法识别的实体。</span><span class="sxs-lookup"><span data-stu-id="4a862-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="4a862-230">问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 3 版本中可用</span><span class="sxs-lookup"><span data-stu-id="4a862-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="4a862-231">安装 ASP.NET 网页不还安装 tools for Visual Studio 的 ASP.NET Web Pages 应用程序的智能感知和项目模板等。</span><span class="sxs-lookup"><span data-stu-id="4a862-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="4a862-232">**解决方法**若要使用 Visual Studio 中的 ASP.NET Web Pages 应用智能感知和项目模板，ASP.NET MVC 3 RC 通过 Web 平台安装程序的安装或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)。</span><span class="sxs-lookup"><span data-stu-id="4a862-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>


#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="4a862-233">问题:"&lt;帮助器&gt;找不到类"错误</span><span class="sxs-lookup"><span data-stu-id="4a862-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="4a862-234">你升级到 Beta 3 后，你可能会看到错误的帮助器类 (例如，`Facebook`类) 不能找不到。</span><span class="sxs-lookup"><span data-stu-id="4a862-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="4a862-235">在 Beta 2 开始，一直在 Beta 3 中，帮助器均已移至显式必须安装的包。</span><span class="sxs-lookup"><span data-stu-id="4a862-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="4a862-236">现有站点将不升级，以便包括这些包;这包括在站点*\My Documents\IISExpress*或*\My Documents\My 网站*文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a862-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="4a862-237">具体而言，你将看到此错误，如果使用中的默认站点*我的网站*(WebSite1)，其中包括对引用`Twitter`帮助器。</span><span class="sxs-lookup"><span data-stu-id="4a862-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="4a862-238">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-238">**Workaround**</span></span>  
> <span data-ttu-id="4a862-239">注释掉对任何帮助器中运行的站点的调用*\_管理员*页上，并安装包或包中包括你想要使用的帮助器。</span><span class="sxs-lookup"><span data-stu-id="4a862-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="4a862-240">安装包后，你可以取消引用帮助器行的注释。</span><span class="sxs-lookup"><span data-stu-id="4a862-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>


#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="4a862-241">问题： 将 Beta 3 ASP.NET Razor 程序集部署到 Bin 文件夹可能不适用于托管网站</span><span class="sxs-lookup"><span data-stu-id="4a862-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="4a862-242">如果将 ASP.NET Web Pages 网站部署到托管站点，并且将 ASP.NET Razor Beta 3 程序集部署到站点的*Bin*文件夹中，你可能会遇到错误，包括以下：</span><span class="sxs-lookup"><span data-stu-id="4a862-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="4a862-243">如果托管提供商已将 ASP.NET Web Pages Beta 1 程序集安装到服务器的全局应用程序缓存 (GAC)，也可能发生。</span><span class="sxs-lookup"><span data-stu-id="4a862-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="4a862-244">GAC 中的程序集通过程序集安装在本地获取优先*Bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a862-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="4a862-245">**解决方法**联系托管提供商来确认你看到的错误是因为提供程序的版本之间发生冲突的程序集和你的帐户。</span><span class="sxs-lookup"><span data-stu-id="4a862-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="4a862-246">如果是这样，请求托管提供商更新服务器的 GAC 中的程序集。</span><span class="sxs-lookup"><span data-stu-id="4a862-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="4a862-247">问题： 读取源或其他通过代理服务器的外部数据</span><span class="sxs-lookup"><span data-stu-id="4a862-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="4a862-248">如果运行站点的服务器位于代理服务器后面，你可能需要配置中的代理信息*Web.config*为了能够读取来自你的站点之外的信息的文件。</span><span class="sxs-lookup"><span data-stu-id="4a862-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="4a862-249">例如，如果你使用`ReCaptcha`帮助器，帮助器与 reCAPTCHA 服务通信，但可能会阻止由你的代理服务器。</span><span class="sxs-lookup"><span data-stu-id="4a862-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="4a862-250">同样，使用在 ASP.NET Web 页中，如源包管理器使用的源可能需要代理配置。</span><span class="sxs-lookup"><span data-stu-id="4a862-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="4a862-251">如果你遇到中使用的外部服务或使用源的包的问题，将以下元素放入应用程序的根*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="4a862-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="4a862-252">有关配置代理服务器的详细信息，请参阅[&lt;代理&gt;元素 （网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="4a862-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>


#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="4a862-253">问题:"无法加载 Microsoft.Web.Infrastructure.dll"错误</span><span class="sxs-lookup"><span data-stu-id="4a862-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="4a862-254">如果您以前使用 Razor 语法安装 Beta 1 版本的 ASP.NET 网页，然后安装 Beta 3 版本，将所有适当的程序集安装在 GAC 中，除*Microsoft.Web.Infrastructure.dll*。</span><span class="sxs-lookup"><span data-stu-id="4a862-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="4a862-255">因此，当你运行 ASP.NET Razor 页，你看到错误，该值指示*Microsoft.Web.Infrastructure.dll*无法加载。</span><span class="sxs-lookup"><span data-stu-id="4a862-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="4a862-256">如果你加载 Beta 3 版本上的干净计算机，则此问题不会发生。</span><span class="sxs-lookup"><span data-stu-id="4a862-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="4a862-257">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-257">**Workaround**</span></span>  
> <span data-ttu-id="4a862-258">在 Control Panel 中，卸载 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="4a862-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="4a862-259">然后重新安装 Beta 3 版本。</span><span class="sxs-lookup"><span data-stu-id="4a862-259">Then reinstall the Beta 3 release.</span></span>


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4a862-260">问题： 卸载.NET Framework 版本 4 禁用带有 Razor 语法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="4a862-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="4a862-261">如果你卸载.NET Framework 版本 4，然后重新安装它，将禁用使用 Razor 语法的 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="4a862-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="4a862-262">与页*.cshtml*扩展可能无法正常运行。</span><span class="sxs-lookup"><span data-stu-id="4a862-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="4a862-263">ASP.NET Web Pages 机根目录中注册程序集*Web.config*文件，并删除.NET Framework 中删除该文件。</span><span class="sxs-lookup"><span data-stu-id="4a862-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="4a862-264">重新安装.NET Framework 安装新版本的配置文件中，但不会添加 ASP.NET 网页的程序集引用。</span><span class="sxs-lookup"><span data-stu-id="4a862-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="4a862-265">**解决方法**后重新安装.NET Framework，请重新安装 ASP.NET 网页使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="4a862-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="4a862-266">这将添加到下面的元素*Web.config*机根目录，这通常是在以下位置中的文件：</span><span class="sxs-lookup"><span data-stu-id="4a862-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
>   
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
>   
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]


#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="4a862-267">问题： 使用 ASP.NET 的 Bin 文件夹中的程序集以前部署的应用程序遇到错误</span><span class="sxs-lookup"><span data-stu-id="4a862-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="4a862-268">在部署期间，ASP.NET 网页程序集的副本 (例如， *Microsoft.WebPages.dll*) 到*Bin*的服务器上的网站的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a862-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="4a862-269">(这可能是自动在部署过程或由于开发人员显式复制程序集。)但是，当安装 Beta 3 版本时，错误发生，如找不到某些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="4a862-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="4a862-270">这是因为大量的 ASP.NET Web Pages 类型已移动到不同的命名空间对于 Beta 3 版本。</span><span class="sxs-lookup"><span data-stu-id="4a862-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="4a862-271">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="4a862-271">**Workaround** </span></span>  
> <span data-ttu-id="4a862-272">清除*Bin*文件夹部署的应用程序，将新的程序集复制到文件夹 （或重新部署应用程序），然后重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a862-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="4a862-273">问题： 无扩展名的 Url 未找到 IIS 7 或 IIS 7.5 上的.cshtml/.vbhtml 文件</span><span class="sxs-lookup"><span data-stu-id="4a862-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="4a862-274">在 IIS 7 或 IIS 7.5 上，如下所示 URL 的请求不能找到页具有*.cshtml*或*.vbhtml*扩展：</span><span class="sxs-lookup"><span data-stu-id="4a862-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
>   
> `http://www.example.com/ExampleSite/ExampleFile`  
>   
> <span data-ttu-id="4a862-275">由于 URL 重写未启用默认情况下为 IIS 7 或 IIS 7.5，因此会出现此问题。</span><span class="sxs-lookup"><span data-stu-id="4a862-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="4a862-276">很可能的方案是，你看不见问题时测试使用本地 IIS Express，但在将你的网站部署到托管的网站时，会遇到它。</span><span class="sxs-lookup"><span data-stu-id="4a862-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="4a862-277">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="4a862-278">如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述[有可用启用某些 IIS 7.0 或 IIS 7.5 的处理程序，来处理请求其 Url 不要以句点结尾的更新](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="4a862-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="4a862-279">如果您没有对服务器计算机的控制 （例如，您要部署到托管网站），将以下代码添加到网站的*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="4a862-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]


#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="4a862-280">问题： 在同一应用程序中使用 Web 应用程序项目或 ASP.NET MVC 和 ASP.NET Web 页</span><span class="sxs-lookup"><span data-stu-id="4a862-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="4a862-281">如果你在 Web 应用程序项目或 ASP.NET MVC 应用程序中使用 ASP.NET 网页，你可能会看到错误， *WebPageHttpApplication*找不到。</span><span class="sxs-lookup"><span data-stu-id="4a862-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="4a862-282">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-282">**Workaround**</span></span>  
> <span data-ttu-id="4a862-283">如果收到此错误，将更改应用程序所派生的基类。</span><span class="sxs-lookup"><span data-stu-id="4a862-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="4a862-284">在*Global.asax*文件中，更改以下行：</span><span class="sxs-lookup"><span data-stu-id="4a862-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="4a862-285">更改为：</span><span class="sxs-lookup"><span data-stu-id="4a862-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="4a862-286">这实际上将反转引入的更改使用 Razor 语法的 Beta 1 发行版的 ASP.NET Web 页。</span><span class="sxs-lookup"><span data-stu-id="4a862-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="4a862-287">问题： 应用程序部署到不具有 SQL Server Compact 安装的计算机</span><span class="sxs-lookup"><span data-stu-id="4a862-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="4a862-288">其中 SQL Server Compact 未安装的计算机上可以运行的应用程序包括 SQL Server Compact 数据库。</span><span class="sxs-lookup"><span data-stu-id="4a862-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="4a862-289">Microsoft WebMatrix Beta 3 自动为你复制这些二进制文件，并执行相应*Web.config*文件转换。</span><span class="sxs-lookup"><span data-stu-id="4a862-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="4a862-290">**解决方法**如果你需要将这些文件复制并使*Web.config*文件更改手动，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="4a862-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="4a862-291">将复制到的数据库引擎程序集*Bin*文件夹 （和子文件夹） 的目标计算机上的应用程序：</span><span class="sxs-lookup"><span data-stu-id="4a862-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="4a862-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="4a862-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="4a862-293">复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="4a862-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="4a862-294">复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="4a862-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="4a862-295">在网站的根文件夹中创建或打开*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="4a862-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="4a862-296">(在 WebMatrix Beta 3 中，此文件类型是如果你单击可用**所有**中**选择文件类型**对话框。)</span><span class="sxs-lookup"><span data-stu-id="4a862-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="4a862-297">添加以下元素的子级**&lt;配置&gt;**元素 (而不是在 **&lt;system.web&gt;** 元素):</span><span class="sxs-lookup"><span data-stu-id="4a862-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="4a862-298">问题： 数据库和 WebGrid 帮助器中不起作用中等信任在 Visual Basic 中</span><span class="sxs-lookup"><span data-stu-id="4a862-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="4a862-299">如果你使用的 Visual Basic (创建*.vbhtml*文件)，则`Database`和`WebGrid`如果应用程序设置为使用中等信任帮助器将无法工作。</span><span class="sxs-lookup"><span data-stu-id="4a862-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="4a862-300">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-300">**Workaround**</span></span>  
> <span data-ttu-id="4a862-301">暂时将设置用于完全信任的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a862-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="4a862-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="4a862-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="4a862-303">问题： 无法识别"加密"属性</span><span class="sxs-lookup"><span data-stu-id="4a862-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="4a862-304">SQL Server Compact 4.0 无法识别`Encrypt`属性`SqlCeConnection`类。</span><span class="sxs-lookup"><span data-stu-id="4a862-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="4a862-305">不应使用此属性来加密数据库文件。</span><span class="sxs-lookup"><span data-stu-id="4a862-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="4a862-306">`Encrypt`属性在 SQL Server Compact 3.5 版本中已弃用，并且仅为向后兼容性保留了。</span><span class="sxs-lookup"><span data-stu-id="4a862-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="4a862-307">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-307">**Workaround**</span></span>  
> <span data-ttu-id="4a862-308">使用`Encryption Mode`属性`SqlCeConnection`类用于 SQL Server Compact 4.0 数据库文件进行加密。</span><span class="sxs-lookup"><span data-stu-id="4a862-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="4a862-309">下面的示例演示如何创建加密的 SQL Server Compact 4.0 数据库使用`Encryption Mode`属性：</span><span class="sxs-lookup"><span data-stu-id="4a862-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
>  
> [!code-csharp[Main](beta3/samples/sample11.cs)]
>  
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="4a862-310">若要更改现有的 SQL Server Compact 4.0 数据库的加密模式，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="4a862-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
>  
> [!code-csharp[Main](beta3/samples/sample13.cs)]
>  
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="4a862-311">要加密未加密的 SQL Server Compact 4.0 数据库，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="4a862-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
>  
> [!code-csharp[Main](beta3/samples/sample15.cs)]
>  
> [!code-vb[Main](beta3/samples/sample16.vb)]


#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="4a862-312">Microsoft Visual c + + 2008年运行时库所需的问题：</span><span class="sxs-lookup"><span data-stu-id="4a862-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="4a862-313">本机 Dll 的 SQL Server Compact 4.0 需要 Microsoft Visual c + + 2008年运行时库 （x86、 IA64 和 x64）、 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="4a862-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="4a862-314">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-314">**Workaround**</span></span>  
> <span data-ttu-id="4a862-315">安装.NET Framework 3.5 SP1。</span><span class="sxs-lookup"><span data-stu-id="4a862-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="4a862-316">这也将安装 Visual c + + 2008年运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="4a862-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="4a862-317">你可以从以下位置下载这些库：</span><span class="sxs-lookup"><span data-stu-id="4a862-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="4a862-318">Microsoft Visual c + + 2008 Service Pack 1 可再发行组件包 ATL 安全更新</span><span class="sxs-lookup"><span data-stu-id="4a862-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="4a862-319">请注意，安装.NET Framework 2.0，3.0，或 4 不*不*安装 Visual c + + 2008年运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="4a862-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>


#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="4a862-320">问题： 如果 SQL Server Compact 安装的计算机上安装.NET Framework 之前，其提供程序固定名称未注册.NET Framework machine.config 文件中</span><span class="sxs-lookup"><span data-stu-id="4a862-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="4a862-321">SQL Server Compact 可以安装在没有安装，因为 SQL Server Compact 确实需要.NET framework 的.NET Framework 的计算机上。</span><span class="sxs-lookup"><span data-stu-id="4a862-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="4a862-322">如果安装了.NET Framework 版本 3.5 也 4 都不必在安装 SQL Server Compact 之前，SQL Server Compact 安装程序未注册中的其提供程序固定名称*machine.config*文件。</span><span class="sxs-lookup"><span data-stu-id="4a862-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="4a862-323">任何应用程序依赖于中的 SQL Server Compact 条目*machine.config*文件将失败。</span><span class="sxs-lookup"><span data-stu-id="4a862-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="4a862-324">中的固定名称注册条目*machine.config*如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="4a862-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="4a862-325">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-325">**Workaround**</span></span>  
> <span data-ttu-id="4a862-326">卸载 SQL Server Compact 4.0 CTP1。</span><span class="sxs-lookup"><span data-stu-id="4a862-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="4a862-327">下载并安装.NET Framework 的完整版本，从以下位置：</span><span class="sxs-lookup"><span data-stu-id="4a862-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="4a862-328">Microsoft.NET Framework 3.5 Service pack 1 （完全包）</span><span class="sxs-lookup"><span data-stu-id="4a862-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="4a862-329">Microsoft.NET Framework 4.0 版本 （完整包）</span><span class="sxs-lookup"><span data-stu-id="4a862-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="4a862-330">然后重新安装[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。</span><span class="sxs-lookup"><span data-stu-id="4a862-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>


<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="4a862-331">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="4a862-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="4a862-332">问题： 安装应用程序可能需要长时间如果用户的 My Documents 文件夹重定向到网络共享</span><span class="sxs-lookup"><span data-stu-id="4a862-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="4a862-333">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-333">**Workaround**</span></span>  
> <span data-ttu-id="4a862-334">无。</span><span class="sxs-lookup"><span data-stu-id="4a862-334">None.</span></span> <span data-ttu-id="4a862-335">应用程序可能需要一段时间才能安装，但将正确安装。</span><span class="sxs-lookup"><span data-stu-id="4a862-335">The application might take a while to install, but will install correctly.</span></span>


<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="4a862-336">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="4a862-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="4a862-337">问题： 站点可能无法在发布如果"目标 URL"字段不 http:// 或 https:// 开头的前缀后</span><span class="sxs-lookup"><span data-stu-id="4a862-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="4a862-338">在**发布设置**对话框中，如果目标 URL 不以开头`http://`或`https://`，在部署之后，站点可能不工作。</span><span class="sxs-lookup"><span data-stu-id="4a862-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="4a862-339">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-339">**Workaround**</span></span>  
> <span data-ttu-id="4a862-340">请确保在发布站点时中的目标 URL 之前**发布设置**对话框开头`http://`或`https://`。</span><span class="sxs-lookup"><span data-stu-id="4a862-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="4a862-341">问题： 发布 MySQL 数据库失败，出现错误"未能发布数据库。</span><span class="sxs-lookup"><span data-stu-id="4a862-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="4a862-342">可能的原因是远程数据库无法运行脚本。"</span><span class="sxs-lookup"><span data-stu-id="4a862-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="4a862-343">多种原因可能会导致错误。</span><span class="sxs-lookup"><span data-stu-id="4a862-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="4a862-344">你可以看到此错误的原因之一是如果数据库脚本包含单引号字符 （'） 和目标 MySQL 数据库的默认字符集不为 utf-8。</span><span class="sxs-lookup"><span data-stu-id="4a862-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="4a862-345">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-345">**Workaround**</span></span>  
> <span data-ttu-id="4a862-346">设置的默认字符集远程 MySQL 数据库为 utf-8。</span><span class="sxs-lookup"><span data-stu-id="4a862-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>


<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="4a862-347">其他问题</span><span class="sxs-lookup"><span data-stu-id="4a862-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="4a862-348">问题： 搜索/筛选器不适合在报表中分组依据： 问题类型</span><span class="sxs-lookup"><span data-stu-id="4a862-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="4a862-349">当你运行的报表可用于站点时，如果输入中的文本*url 的筛选器*框中，单击*搜索*，会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="4a862-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="4a862-350">这是因为此控件不起作用时*Group By*报告的状态设置为*问题类型*，这是默认设置。</span><span class="sxs-lookup"><span data-stu-id="4a862-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="4a862-351">**解决方法**中*Group By*选项卡的功能区中，单击*URL*进行分组由其源 URL 的条目。</span><span class="sxs-lookup"><span data-stu-id="4a862-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="4a862-352">文本框和按钮用于筛选条目都能运行时处于此状态。</span><span class="sxs-lookup"><span data-stu-id="4a862-352">The text box and button to filter the entries are functional while in this state.</span></span>


#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="4a862-353">问题： WCF 应用程序无法运行使用 IIS Express</span><span class="sxs-lookup"><span data-stu-id="4a862-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="4a862-354">浏览到 WCF 应用程序会导致类似以下错误：</span><span class="sxs-lookup"><span data-stu-id="4a862-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="4a862-355">*无法加载文件或程序集 Microsoft.Web.Administration，Version = 7.0.0.0，区域性 = neutral，PublicKeyToken = 31bf3856ad364e35 或其依赖项之一。系统找不到指定的文件。*</span><span class="sxs-lookup"><span data-stu-id="4a862-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="4a862-356">因为默认情况下，IIS Express Beta 版本不支持 WCF，将发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="4a862-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="4a862-357">**解决方法**使用下列解决方法之一 (解决方法 #2 要求 Microsoft Windows Vista 或更高版本):</span><span class="sxs-lookup"><span data-stu-id="4a862-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="4a862-358">复制*Microsoft.Web.dll*和*Microsoft.Web.Administration.dll*到 WebMatrix 安装位置中的程序集*bin* WCF 目录应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a862-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="4a862-359">默认情况下，在安装 WebMatrix *Microsoft WebMatrix*的子文件夹下系统的*Program Files*文件夹。</span><span class="sxs-lookup"><span data-stu-id="4a862-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="4a862-360">在 Microsoft Windows Vista 或更高版本，创建指向中的程序集的*bin*使用以下命令的目录。</span><span class="sxs-lookup"><span data-stu-id="4a862-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="4a862-361">（这种方法的优点它不创建程序集的副本。）</span><span class="sxs-lookup"><span data-stu-id="4a862-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="4a862-362">安装在 GAC 中的两个程序集。</span><span class="sxs-lookup"><span data-stu-id="4a862-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="4a862-363">从提升的提示符，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="4a862-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]


#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="4a862-364">问题： WebMatrix Beta 3 不能执行某些任务需要提升权限</span><span class="sxs-lookup"><span data-stu-id="4a862-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="4a862-365">WebMatrix Beta 3 不能执行某些任务，需要提升，例如在以下情况下安装其他组件：</span><span class="sxs-lookup"><span data-stu-id="4a862-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="4a862-366">在 Windows Vista 或 Windows 7，使用不具备管理员权限的帐户登录和用户帐户控制 (UAC) 处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="4a862-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="4a862-367">您正在使用 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="4a862-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="4a862-368">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-368">**Workaround**</span></span>  
> <span data-ttu-id="4a862-369">WebMatrix Beta 3 中的大多数任务不需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="4a862-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="4a862-370">对于那些确实，你可以执行该操作作为管理员，或请按照下列步骤：</span><span class="sxs-lookup"><span data-stu-id="4a862-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="4a862-371">在 Windows Vista 或 Windows 7 上，启用 UAC。</span><span class="sxs-lookup"><span data-stu-id="4a862-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="4a862-372">在 Windows XP 中，将用户添加到管理员安全组。</span><span class="sxs-lookup"><span data-stu-id="4a862-372">On Windows XP, add the user to the Administrators security group.</span></span>


#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="4a862-373">问题:"从 Web 库的站点"处于禁用状态</span><span class="sxs-lookup"><span data-stu-id="4a862-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="4a862-374">**站点从 Web 库**如果未安装 Web 平台安装程序 3.0 选项被禁用。</span><span class="sxs-lookup"><span data-stu-id="4a862-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="4a862-375">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-375">**Workaround**</span></span>  
> <span data-ttu-id="4a862-376">安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="4a862-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>


#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="4a862-377">问题： 在 Windows Server 2003，IIS Express 不会启动非管理用户</span><span class="sxs-lookup"><span data-stu-id="4a862-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="4a862-378">在 Windows Server 2003，当您启动页或启动 IIS Express，IIS Express 不启动。</span><span class="sxs-lookup"><span data-stu-id="4a862-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="4a862-379">对 Web 页会显示错误，指示非管理用户，启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="4a862-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="4a862-380">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-380">**Workaround**</span></span>  
> <span data-ttu-id="4a862-381">启动 WebMatrix Beta 3 作为管理用户。</span><span class="sxs-lookup"><span data-stu-id="4a862-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="4a862-382">有关更多详细信息，请参阅以下知识库文章：</span><span class="sxs-lookup"><span data-stu-id="4a862-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="4a862-383">由非管理用户启动的应用程序无法侦听到在其应用程序运行在 Windows Vista、 Windows Server 2003 或 Windows XP 的计算机的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="4a862-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="4a862-384">问题： Google Chrome 不能作为运行选项</span><span class="sxs-lookup"><span data-stu-id="4a862-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="4a862-385">在浏览器的列表中不显示 Google Chrome**运行**上**主页**选项卡。</span><span class="sxs-lookup"><span data-stu-id="4a862-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="4a862-386">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-386">**Workaround**</span></span>  
> <span data-ttu-id="4a862-387">某些版本的 Google Chrome 并不能注册正确与 Windows 中的默认程序功能。</span><span class="sxs-lookup"><span data-stu-id="4a862-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="4a862-388">一种解决方法，启动 Google Chrome 中，单击*自定义和控制 Google Chrome*菜单上，单击*选项*，然后单击*请 Google Chrome 我默认浏览器*。</span><span class="sxs-lookup"><span data-stu-id="4a862-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="4a862-389">问题:"外键"对话框中不允许输入为主键</span><span class="sxs-lookup"><span data-stu-id="4a862-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="4a862-390">**外键**对话框中不允许你从主键表中输入的主键名称。</span><span class="sxs-lookup"><span data-stu-id="4a862-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="4a862-391">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-391">**Workaround**</span></span>  
> <span data-ttu-id="4a862-392">这是有意。</span><span class="sxs-lookup"><span data-stu-id="4a862-392">This is intentional.</span></span> <span data-ttu-id="4a862-393">不需要输入主键表的主键的名称。</span><span class="sxs-lookup"><span data-stu-id="4a862-393">You do not need to enter the name of the primary key from the primary key table.</span></span>


#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="4a862-394">问题:"关系"按钮处于禁用状态</span><span class="sxs-lookup"><span data-stu-id="4a862-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="4a862-395">**关系**按钮下**表**选项卡中**数据库**为 SQL Server Compact 数据库禁用工作区。</span><span class="sxs-lookup"><span data-stu-id="4a862-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="4a862-396">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-396">**Workaround**</span></span>  
> <span data-ttu-id="4a862-397">无。</span><span class="sxs-lookup"><span data-stu-id="4a862-397">None.</span></span> <span data-ttu-id="4a862-398">SQL Server Compact 不支持表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="4a862-398">SQL Server Compact does not support relationships between tables.</span></span>


#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="4a862-399">问题： 参数化的 SQL 查询引发异常</span><span class="sxs-lookup"><span data-stu-id="4a862-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="4a862-400">在 SQL Server Compact 4.0，如果不会如指定的数据类型`SqlDbType`或`DbType`中参数化查询的参数，运行查询时引发异常。</span><span class="sxs-lookup"><span data-stu-id="4a862-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="4a862-401">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="4a862-401">**Workaround**</span></span>  
> <span data-ttu-id="4a862-402">显式设置参数的数据类型，如`SqlDbType`或`DbType`。</span><span class="sxs-lookup"><span data-stu-id="4a862-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="4a862-403">这是在 BLOB 数据类型的情况下关键 (`image`和`ntext`)。</span><span class="sxs-lookup"><span data-stu-id="4a862-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="4a862-404">使用代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="4a862-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
>  
> [!code-vb[Main](beta3/samples/sample21.vb)]


<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="4a862-405">更多信息</span><span class="sxs-lookup"><span data-stu-id="4a862-405">For More Information</span></span>

<span data-ttu-id="4a862-406">有关 WebMatrix Beta 3 的详细信息，请参阅以下网站：</span><span class="sxs-lookup"><span data-stu-id="4a862-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="4a862-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="4a862-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="4a862-408">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="4a862-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="4a862-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="4a862-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

* * *

<span data-ttu-id="4a862-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="4a862-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="4a862-411">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="4a862-411">All Rights Reserved.</span></span> <span data-ttu-id="4a862-412">[使用条款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4a862-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
