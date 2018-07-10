---
uid: web-pages/readme/beta3
title: Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件 |Microsoft Docs
author: rick-anderson
description: Web Matrix 和 ASP.NET Web Pages (Razor) Beta 3 版本自述文件
ms.author: aspnetcontent
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: 16b324e555b5450fc1e05c63e7e19985a2d02b89
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831827"
---
<a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="ac9fc-103">Web Matrix 和 ASP.NET Web Pages (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="ac9fc-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>
====================
> <span data-ttu-id="ac9fc-104">Web Matrix 和 ASP.NET Web Pages (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="ac9fc-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="ac9fc-105">2010 年 11 月 9日</span><span class="sxs-lookup"><span data-stu-id="ac9fc-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="ac9fc-106">内容</span><span class="sxs-lookup"><span data-stu-id="ac9fc-106">Contents</span></span>

- [<span data-ttu-id="ac9fc-107">概述</span><span class="sxs-lookup"><span data-stu-id="ac9fc-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="ac9fc-108">安装</span><span class="sxs-lookup"><span data-stu-id="ac9fc-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="ac9fc-109">新功能、 更改和 Beta 3 版本中的已知问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="ac9fc-110">WebMatrix 安装问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="ac9fc-111">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ac9fc-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="ac9fc-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="ac9fc-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="ac9fc-113">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="ac9fc-114">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="ac9fc-115">其他问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="ac9fc-116">有关详细信息</span><span class="sxs-lookup"><span data-stu-id="ac9fc-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="ac9fc-117">概述</span><span class="sxs-lookup"><span data-stu-id="ac9fc-117">Overview</span></span>

> <span data-ttu-id="ac9fc-118">Microsoft WebMatrix Beta 是在几分钟内将安装免费的 web 开发堆栈。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="ac9fc-119">它与数据库和编程框架用于创建单一的集成体验集成的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="ac9fc-120">你可以使用 WebMatrix Beta 来简化代码、 测试和发布自己的 ASP.NET 或 PHP 网站的方式或使用 WebMatrix Beta 启动新的网站使用 DotNetNuke、 Umbraco、 WordPress 或 Joomla 等受欢迎的开源应用。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="ac9fc-121">WebMatrix beta 版使用相同的功能强大的 web 服务器、 数据库引擎和框架环境，将在 internet 上，这使从开发过渡到生产顺畅、 无缝运行你的网站。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>


<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="ac9fc-122">安装</span><span class="sxs-lookup"><span data-stu-id="ac9fc-122">Installation</span></span>

> <span data-ttu-id="ac9fc-123">若要安装 WebMatrix Beta 3，你可以使用[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="ac9fc-124">安装 Web 平台安装程序后，可用于安装 WebMatrix Beta 3。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="ac9fc-125">如果在安装过程中遇到问题，请参阅[问题的 Microsoft Web 平台安装程序疑难解答](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>


<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="ac9fc-126">有关发布应用程序的说明</span><span class="sxs-lookup"><span data-stu-id="ac9fc-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="ac9fc-127">请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="ac9fc-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>


<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="ac9fc-128">新功能、 更改 andKnown 问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="ac9fc-129">WebMatrix Beta 3 安装</span><span class="sxs-lookup"><span data-stu-id="ac9fc-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="ac9fc-130">问题： WebMatrix Beta 3 上才支持 Microsoft.NET Framework 4 的平台</span><span class="sxs-lookup"><span data-stu-id="ac9fc-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="ac9fc-131">WebMatrix beta 版本需要.NET Framework 版本 4。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="ac9fc-132">在某些情况下，WebMatrix beta 版安装程序会让您尝试安装不受支持的配置集的一部分的平台上。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="ac9fc-133">具体而言，Windows Vista SP1 更新将允许您开始安装 WebMatrix beta 版，但.NET Framework 4 组件将失败并且阻止您的安装。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="ac9fc-134">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-134">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-135">安装在受支持的平台，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="ac9fc-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ac9fc-136">Windows 7</span></span>
> - <span data-ttu-id="ac9fc-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="ac9fc-137">Windows Server 2008</span></span>
> - <span data-ttu-id="ac9fc-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ac9fc-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="ac9fc-139">Windows Vista SP1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ac9fc-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="ac9fc-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="ac9fc-140">Windows XP SP3</span></span>
> - <span data-ttu-id="ac9fc-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="ac9fc-141">Windows Server 2003 SP2</span></span>


#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="ac9fc-142">如果没有 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008，问题： 不能安装 WebMatrix Beta 3</span><span class="sxs-lookup"><span data-stu-id="ac9fc-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="ac9fc-143">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-143">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-144">安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)从 Microsoft 下载中心获得。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="ac9fc-145">问题： SQL Server Compact 4.0 某些程序集未安装在 GAC 中</span><span class="sxs-lookup"><span data-stu-id="ac9fc-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="ac9fc-146">在 64 位计算机上安装 SQL Server Compact 4.0 和计算机具有仅.NET Framework 3.5 SP1 客户端安装了配置文件时，SQL Server Compact 4.0 的托管程序集不会放在全局程序集缓存 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="ac9fc-147">未安装在 GAC 中的托管程序集是：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="ac9fc-148">*System.Data.SqlServerCe.dll* （ADO.NET 提供程序）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="ac9fc-149">*System.Data.SqlServerCe.Entity.dll* （ADO.NET 实体框架）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="ac9fc-150">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-150">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-151">卸载 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="ac9fc-152">下载并安装.NET Framework 3.5 SP1 的完整版本，从以下位置：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="ac9fc-153">Microsoft.NET Framework 3.5 Service pack 1 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="ac9fc-154">然后重新安装 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-154">Then reinstall SQL Server Compact 4.0.</span></span>


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="ac9fc-155">问题： 无法卸载 SQL Server Compact 使用命令行</span><span class="sxs-lookup"><span data-stu-id="ac9fc-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="ac9fc-156">卸载 SQL Server Compact 使用命令行选项不适用于此版本。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="ac9fc-157">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-157">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-158">使用*程序和功能*Windows 控制面板卸载 Microsoft SQL Server Compact 4.0 中。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="ac9fc-159">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ac9fc-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="ac9fc-160">文档的本节介绍新功能、 更改和使用 Razor 语法的 Beta 3 版本的 ASP.NET Web Pages 的已知的问题。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="ac9fc-161">新增功能</span><span class="sxs-lookup"><span data-stu-id="ac9fc-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="ac9fc-162">更改</span><span class="sxs-lookup"><span data-stu-id="ac9fc-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="ac9fc-163">问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="ac9fc-164">Beta 3 ASP.NET Web pages with Razor Syntax 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ac9fc-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="ac9fc-165">新增内容:"Html.Raw"方法将呈现未编码的标记</span><span class="sxs-lookup"><span data-stu-id="ac9fc-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="ac9fc-166">新`Html.Raw`方法可呈现 HTML 标记作为标记而不是呈现编码的输出。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="ac9fc-167">（默认情况下，ASP.NET Razor 将编码字符串呈现它们之前。）语法为：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="ac9fc-168">下面的示例演示如何使用 `Html.Raw`：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]


<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="ac9fc-169">在 Beta 3 中 ASP.NET Web pages with Razor Syntax 的更改</span><span class="sxs-lookup"><span data-stu-id="ac9fc-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="ac9fc-170">删除的更改:"HrefAttribute"方法</span><span class="sxs-lookup"><span data-stu-id="ac9fc-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="ac9fc-171">`HrefAttribute`方法的`WebPage`类已删除。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="ac9fc-172">此帮助器用于对 Url 中的不安全字符进行编码。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="ac9fc-173">它是不再需要，因为 ASP.NET Razor 自动对字符串进行编码。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="ac9fc-174">(使用新`Html.Raw`方法以呈现未编码的字符串。)</span><span class="sxs-lookup"><span data-stu-id="ac9fc-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>


#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="ac9fc-175">更改： 语法声明性"@helper"更改帮助程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="ac9fc-176">在 Beta 3 版本中，ASP.NET 更改它将帮助程序，使用创建的解析`@helper`语法。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="ac9fc-177">从本质上讲，`@helper`语法现在分析为一个代码块而不是作为一个的标记可以包含代码块。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="ac9fc-178">因此，帮助器代码不需要用`@{ }`块。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="ac9fc-179">相反，标记帮助器必须显式包含在 HTML 元素或 ASP.NET Razor`<text></text>`标记。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="ac9fc-180">例如，以下`@helper`语法适用于 Beta 3 版本：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="ac9fc-181">在 Beta 3 版本中，必须将此帮助器更改为如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="ac9fc-182">请注意，`@{ }`不再使用的帮助程序中的初始代码周围的字符。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="ac9fc-183">这是因为帮助程序的内容被视为默认情况下一个代码块。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="ac9fc-184">帮助器将呈现标记，开始在打开`<a>`标记。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="ac9fc-185">如果帮助者必须呈现的纯文本或标记，其中不包含结束标记 (例如，`<meta>`标记)，要呈现的内容必须在`<text></text>`标记。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>


#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="ac9fc-186">"WebPageContext.HttpContext"删除更改：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="ac9fc-187">`WebPageContext.HttpContext`删除属性。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="ac9fc-188">请改用 `HttpContext.Current`。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="ac9fc-189">(`WebPageContext.HttpContext`属性只是包装这。)</span><span class="sxs-lookup"><span data-stu-id="ac9fc-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>


#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="ac9fc-190">移动到新的包的更改:"Facebook"帮助程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="ac9fc-191">`Facebook`帮助器已移至*Facebook.Helper*库，其中包括`Facebook`帮助器和其他功能。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="ac9fc-192">您必须安装此库作为单独的包，在"安装帮助程序使用程序包管理器"中所述在本教程[开始使用 ASP.NET 页面](https://go.microsoft.com/fwlink/?LinkId=202889)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>


#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="ac9fc-193">更改： 成员身份、 角色和安全类型移动到新的程序集</span><span class="sxs-lookup"><span data-stu-id="ac9fc-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="ac9fc-194">以下类型都已移动到`WebMatrix.WebData`程序集：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`


#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="ac9fc-195">移动到 System.Web.WebPages.dll 程序集中的更改:"TagBuilder"类</span><span class="sxs-lookup"><span data-stu-id="ac9fc-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="ac9fc-196">`TagBuilde` R 类已被移动到 System.Web.WebPages.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="ac9fc-197">以前，这是 ASP.NET MVC 的一部分的程序集中。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="ac9fc-198">此更改意味着，不需要安装 ASP.NET MVC，以便使用`TagBuilder`类。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="ac9fc-199">但是，此类是仍在`System.Web.Mvc`命名空间。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="ac9fc-200">若要使用`TagBuilder`类 （例如，在一个自定义 ASP.NET Razor 帮助器），必须引用的命名空间 (例如，通过添加`@using System.Web.Mvc`到你的代码)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>


#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="ac9fc-201">更改： 请求验证语法已发生更改;"验证"类中删除</span><span class="sxs-lookup"><span data-stu-id="ac9fc-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="ac9fc-202">在 Beta 3 版本中，若要禁用验证的一个单独的字段或一组字段，您可以调用`Validation.Exclude`方法，传入的名称或排除在验证之外的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="ac9fc-203">跳过验证的 Beta 3 版本中提供了一种新语法。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="ac9fc-204">`Validation` Beta 3 中使用的方法已删除。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="ac9fc-205">如果用户尝试将 HTML 标记 （例如，通过在页面上使用富文本编辑器） 上传未禁用请求验证，如果网站将报告之类的错误*从客户端检测到潜在危险的Request.Form值*都不接受用户输入。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="ac9fc-206">如果禁用请求验证，你必须手动检查用户输入，以确保它不包含具有潜在危险的标记或脚本使用类似[Microsoft 防跨站点脚本库 V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="ac9fc-207">若要禁用自动请求验证，请调用`Request.Unvalidated`方法，并向其传递该字段或你要绕过请求验证的其他文章对象的名称。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="ac9fc-208">可以使用此方法以跳过验证对于中的任何项`Form`， `QueryString`， `Cookies`，和`ServerVariables`集合。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="ac9fc-209">下面的示例演示如何使用`Unvalidated`方法：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]


<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="ac9fc-210">ASP.NET Web Pages with Razor Syntax 的已知的问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="ac9fc-211">问题： 意外的行为时使用自定义用户表的成员身份</span><span class="sxs-lookup"><span data-stu-id="ac9fc-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="ac9fc-212">若要初始化 ASP.NET Razor 网站成员资格提供程序，请调用`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="ac9fc-213">(在 WebMatrix 中，入门网站模板包括对在此方法的调用 *\_AppStart.cshtml*文件。)如果`autoCreateTables`此方法的参数设置为 true (默认情况下它设置为 true 入门网站模板中)，并且如果一个无法识别的表名称传递给方法 （第二个参数），该方法不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="ac9fc-214">相反，它会自动创建的表。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="ac9fc-215">如果你想要使用自定义用户表的成员身份，但将传递到的错误的表名称，这可能是问题`WebSecurity.InitializeDatabaseConnection`方法。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="ac9fc-216">由于该方法不会默认情况下引发错误如果指定的表不存在，并且它改为创建一个新表，该应用程序可以似乎无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="ac9fc-217">但是，依赖于自定义用户表 （和在其中的字段） 的应用程序代码可以最终失败并出现意外错误。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="ac9fc-218">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-218">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-219">请确保名称传入`InitializeDatabaseConnection`方法匹配项的用户配置文件表中的成员资格数据库，或请确保`autoCreateTables`参数设置为 false。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="ac9fc-220">问题:"无法生成 SQL Server 的用户实例"错误</span><span class="sxs-lookup"><span data-stu-id="ac9fc-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="ac9fc-221">如果 WebMatrix Web 应用程序使用 SQL Server Express，并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 不能在运行时检索用户的本地应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="ac9fc-222">**解决方法**请确保应用程序 (通常为 NETWORK SERVICE) 下运行的 Windows 帐户，包含读/写权限的应用程序的根文件夹和子文件夹，例如*应用\_数据*.</span><span class="sxs-lookup"><span data-stu-id="ac9fc-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="ac9fc-223">知识库文章中提供了更多详细的信息[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目的问题](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="ac9fc-224">问题： 在 Visual Studio 中，自定义程序集 (Dll) 的命名空间不自动导入</span><span class="sxs-lookup"><span data-stu-id="ac9fc-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="ac9fc-225">如果在 Visual Studio 中的项目中使用自定义程序集，这些程序集中声明的命名空间将不自动导入在设计时。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="ac9fc-226">因此，对自定义类型的引用可能无法在设计时识别并标记为不能识别 Visual Studio 中 （使用"波形曲线"）。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="ac9fc-227">仅在设计时在 Visual Studio; 中出现此问题应用程序本身能够正常运行。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="ac9fc-228">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-228">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-229">包括`using`语句 (`imports`在 Visual Basic 中)，它引用在设计时无法识别的实体。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="ac9fc-230">问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 版本 3 中可用</span><span class="sxs-lookup"><span data-stu-id="ac9fc-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="ac9fc-231">安装 ASP.NET Web Pages 不同时安装工具用于 Visual Studio 的 ASP.NET Web Pages 应用程序的智能感知和项目模板等。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="ac9fc-232">**解决方法**若要使用 Visual Studio 中的 ASP.NET Web Pages 应用程序的智能感知和项目模板，ASP.NET MVC 3 RC 通过 Web 平台安装程序的安装或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>


#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="ac9fc-233">问题:"&lt;帮助器&gt;找不到类"错误</span><span class="sxs-lookup"><span data-stu-id="ac9fc-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="ac9fc-234">升级到 Beta 3 后，可能会看到错误的帮助器类 (例如，`Facebook`类) 不能找不到。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="ac9fc-235">在 Beta 2 开始，一直在 Beta 3 中，帮助程序已被移到必须显式安装的包。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="ac9fc-236">不升级现有的站点中包含这些包;这包括中的站点*\My Documents\IISExpress*或*\My Documents\My 网站*文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="ac9fc-237">具体而言，您会看到此错误，如果使用中的默认站点*我的网站*(WebSite1)，其中包括对引用`Twitter`帮助器。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="ac9fc-238">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-238">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-239">注释掉对运行的站点中任何帮助程序调用*\_管理员*页，并安装包或包含你想要使用的帮助器的包。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="ac9fc-240">安装此包后，可以取消注释引用帮助程序的行。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>


#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="ac9fc-241">问题： Beta 3 ASP.NET Razor 程序集部署到 Bin 文件夹可能不适用于托管站点</span><span class="sxs-lookup"><span data-stu-id="ac9fc-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="ac9fc-242">如果将 ASP.NET Web Pages 网站部署到托管站点，并将 ASP.NET Razor Beta 3 程序集部署到的站点*Bin*文件夹中，你可能会遇到错误，包括以下：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="ac9fc-243">如果宿主提供程序已安装到服务器的全局应用程序缓存 (GAC) 的 ASP.NET Web Pages Beta 1 程序集，则可能发生此问题。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="ac9fc-244">程序集位于 gac 中本地安装的程序集通过获取优先*Bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="ac9fc-245">**解决方法**联系托管提供商，以确认你看到的错误是由于提供程序的版本之间发生冲突的程序集和你们的。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="ac9fc-246">如果是这样，请求托管提供商更新服务器的 GAC 中的程序集。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="ac9fc-247">问题： 读取源或其他外部数据通过代理服务器</span><span class="sxs-lookup"><span data-stu-id="ac9fc-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="ac9fc-248">如果运行该站点的服务器位于代理服务器后面，可能需要配置中的代理信息*Web.config*以便能够读取来自你的站点之外的信息的文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="ac9fc-249">例如，如果您使用`ReCaptcha`帮助器，帮助者与 reCAPTCHA 服务通信，但可能无法通过代理服务器。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="ac9fc-250">同样，使用 ASP.NET Web Pages 中，如包管理器，使用源的馈送可能需要代理服务器配置。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="ac9fc-251">如果使用外部服务或使用包源中的问题，将以下元素放入应用程序的根*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="ac9fc-252">有关配置代理服务器的详细信息，请参阅[&lt;代理&gt;元素 （网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 网站上。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>


#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="ac9fc-253">问题:"无法加载 Microsoft.Web.Infrastructure.dll"错误</span><span class="sxs-lookup"><span data-stu-id="ac9fc-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="ac9fc-254">如果您以前安装的 Beta 1 版本的 ASP.NET Web Pages 使用 Razor 语法，然后再安装 Beta 3 版本，所有适当的程序集安装在 gac 中除*Microsoft.Web.Infrastructure.dll*。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="ac9fc-255">因此，在运行 ASP.NET Razor 页时，您看到错误，指示*Microsoft.Web.Infrastructure.dll*无法加载。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="ac9fc-256">如果加载的干净计算机上的 Beta 3 版本不会出现此问题。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="ac9fc-257">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-257">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-258">在控制面板中，卸载 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="ac9fc-259">然后重新安装 Beta 3 版本。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-259">Then reinstall the Beta 3 release.</span></span>


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="ac9fc-260">问题： 卸载.NET Framework 版本 4 禁用使用 Razor 语法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="ac9fc-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="ac9fc-261">如果卸载.NET Framework 版本 4，然后重新安装它，则禁用使用 Razor 语法的 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="ac9fc-262">与页 *.cshtml*扩展不能正确运行。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="ac9fc-263">ASP.NET 网页机根目录中注册程序集*Web.config*文件，并删除.NET Framework 中删除该文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="ac9fc-264">重新安装.NET Framework 安装的配置文件的新版本，但不会将引用添加 ASP.NET Web Pages 的程序集。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="ac9fc-265">**解决方法**后重新安装.NET Framework，请重新安装 ASP.NET Web Pages 使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="ac9fc-266">这将添加到下面的元素*Web.config*机根目录，这通常是在以下位置中的文件：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]


#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="ac9fc-267">问题： 使用 ASP.NET 的 Bin 文件夹中的程序集之前部署的应用程序遇到错误</span><span class="sxs-lookup"><span data-stu-id="ac9fc-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="ac9fc-268">在部署期间，ASP.NET Web Pages 程序集的副本 (例如， *Microsoft.WebPages.dll*) 到*Bin*的服务器上的网站的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="ac9fc-269">(可能在部署期间自动发生这或者是因为开发人员显式复制程序集。)但是，当安装 Beta 3 版本，则错误时，如找不到某些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="ac9fc-270">这是因为多个 ASP.NET Web Pages 类型移动到不同的命名空间对于 Beta 3 版本。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="ac9fc-271">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ac9fc-271">**Workaround** </span></span>  
> <span data-ttu-id="ac9fc-272">清除*Bin*文件夹部署的应用程序的新程序集复制到的文件夹 （或重新部署应用程序），然后重新启动该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="ac9fc-273">问题： 无扩展名的 Url 不到在 IIS 7 或 IIS 7.5 上的.cshtml/.vbhtml 文件</span><span class="sxs-lookup"><span data-stu-id="ac9fc-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="ac9fc-274">在 IIS 7 或 IIS 7.5 上，使用类似于以下 URL 的请求不能将查找具有的页 *.cshtml*或 *.vbhtml*扩展：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="ac9fc-275">由于 URL 重写未启用默认情况下为 IIS 7 或 IIS 7.5，则会产生问题。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="ac9fc-276">很可能方案是使用本地 IIS Express，测试时未看到该问题，但在你的网站部署到托管网站时遇到。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="ac9fc-277">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="ac9fc-278">如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述[更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="ac9fc-279">如果您没有对服务器计算机的控制 （例如，要部署到托管的网站），将以下代码添加到该网站*Web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]


#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="ac9fc-280">问题： 在同一应用程序中使用 Web 应用程序项目或 ASP.NET MVC 和 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ac9fc-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="ac9fc-281">如果在 Web 应用程序项目或 ASP.NET MVC 应用程序中使用的 ASP.NET Web Pages，可能会看到错误， *WebPageHttpApplication*找不到。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="ac9fc-282">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-282">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-283">如果收到此错误，将更改应用程序所派生的基类。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="ac9fc-284">在中*Global.asax*文件中，将以下行：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="ac9fc-285">更改为：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="ac9fc-286">这实际上会反转更改引入了使用 Razor 语法的 Beta 1 版本的 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="ac9fc-287">问题： 应用程序部署到不具有 SQL Server Compact 安装的计算机</span><span class="sxs-lookup"><span data-stu-id="ac9fc-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="ac9fc-288">SQL Server Compact 未安装在计算机上可以运行包含 SQL Server Compact 数据库的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="ac9fc-289">Microsoft WebMatrix Beta 3 中自动将这些二进制文件复制，并执行适当*Web.config*文件转换。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="ac9fc-290">**解决方法**如果你需要将这些文件复制并使*Web.config*文件更改手动，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="ac9fc-291">将复制到的数据库引擎程序集*Bin*目标计算机上的应用程序文件夹 （和子文件夹）：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="ac9fc-292">复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **到** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="ac9fc-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="ac9fc-293">复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="ac9fc-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="ac9fc-294">复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="ac9fc-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="ac9fc-295">在该网站的根文件夹中创建或打开*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="ac9fc-296">(此文件类型是在 WebMatrix Beta 3 中，单击**所有**中**选择文件类型**对话框。)</span><span class="sxs-lookup"><span data-stu-id="ac9fc-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="ac9fc-297">将以下元素添加为的子**&lt;配置&gt;** 元素 (而不是在**&lt;system.web&gt;** 元素):</span><span class="sxs-lookup"><span data-stu-id="ac9fc-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="ac9fc-298">问题： 在中等信任在 Visual Basic 中无法工作数据库和 WebGrid 帮助器</span><span class="sxs-lookup"><span data-stu-id="ac9fc-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="ac9fc-299">如果使用的 Visual Basic (创建 *.vbhtml*文件)，则`Database`和`WebGrid`如果应用程序设置为使用中等信任级别，帮助程序将无法工作。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="ac9fc-300">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-300">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-301">暂时将设置应用程序以使用完全信任。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="ac9fc-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="ac9fc-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="ac9fc-303">问题： 无法识别"Encrypt"属性</span><span class="sxs-lookup"><span data-stu-id="ac9fc-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="ac9fc-304">SQL Server Compact 4.0 不能识别`Encrypt`属性的`SqlCeConnection`类。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="ac9fc-305">不应使用此属性来加密数据库文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="ac9fc-306">`Encrypt`属性在 SQL Server Compact 3.5 版本中已弃用，并且仅为向后兼容性保留了。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="ac9fc-307">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-307">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-308">使用`Encryption Mode`属性的`SqlCeConnection`类来加密 SQL Server Compact 4.0 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="ac9fc-309">下面的示例演示如何创建加密的 SQL Server Compact 4.0 数据库使用`Encryption Mode`属性：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="ac9fc-310">若要更改现有的 SQL Server Compact 4.0 数据库的加密模式，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="ac9fc-311">若要加密的未加密的 SQL Server Compact 4.0 数据库，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]


#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="ac9fc-312">Microsoft Visual c + + 2008年运行时库是必需的问题：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="ac9fc-313">本机 Dll 的 SQL Server Compact 4.0 需要 Microsoft Visual c + + 2008年运行时库 （x86、 IA64 和 x64）、 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="ac9fc-314">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-314">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-315">安装.NET Framework 3.5 SP1。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="ac9fc-316">这还会安装 Visual c + + 2008年运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="ac9fc-317">可以从以下位置下载库：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="ac9fc-318">Microsoft Visual c + + 2008 Service Pack 1 可再发行组件包 ATL 安全更新</span><span class="sxs-lookup"><span data-stu-id="ac9fc-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="ac9fc-319">请注意，安装.NET Framework 2.0，3.0，或 4*不*安装 Visual c + + 2008年运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>


#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="ac9fc-320">问题： 如果 SQL Server Compact 安装的计算机上安装.NET Framework 之前，其提供程序固定名称未注册.NET Framework machine.config 文件中</span><span class="sxs-lookup"><span data-stu-id="ac9fc-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="ac9fc-321">SQL Server Compact 可以安装在未安装.NET Framework 安装，因为 SQL Server Compact 确实需要.NET framework 的计算机上。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="ac9fc-322">如果既没有.NET Framework 版本 3.5 和 4 安装在安装 SQL Server Compact 之前，SQL Server Compact 安装程序不会注册在其提供程序固定名称*machine.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="ac9fc-323">任何应用程序都依赖于中的 SQL Server Compact 条目*machine.config*文件将会失败。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="ac9fc-324">中的固定名称注册条目*machine.config*如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="ac9fc-325">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-325">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-326">卸载 SQL Server Compact 4.0 CTP1。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="ac9fc-327">下载并安装.NET Framework 的完整版本，从以下位置：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="ac9fc-328">Microsoft.NET Framework 3.5 Service pack 1 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="ac9fc-329">Microsoft.NET Framework 4.0 版本 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="ac9fc-330">然后重新安装[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>


<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="ac9fc-331">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="ac9fc-332">问题： 安装应用程序可能需要长时间如果用户的 My Documents 文件夹重定向到网络共享</span><span class="sxs-lookup"><span data-stu-id="ac9fc-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="ac9fc-333">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-333">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-334">无。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-334">None.</span></span> <span data-ttu-id="ac9fc-335">应用程序可能需要一段时间才能安装，但将正确安装。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-335">The application might take a while to install, but will install correctly.</span></span>


<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="ac9fc-336">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="ac9fc-337">问题： 站点可能无法在发布如果将"目标 URL"字段不 http:// 或 https:// 开头的前缀后</span><span class="sxs-lookup"><span data-stu-id="ac9fc-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="ac9fc-338">在中**发布设置**对话框中，如果目标 URL 不以开头`http://`或`https://`，部署后，该站点可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="ac9fc-339">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-339">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-340">请确保在发布的站点中的目标 URL 前**发布设置**对话框的开头`http://`或`https://`。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="ac9fc-341">问题： 发布的 MySQL 数据库失败，出现错误"无法将数据库发布。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="ac9fc-342">这可以是远程数据库不能运行脚本。"</span><span class="sxs-lookup"><span data-stu-id="ac9fc-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="ac9fc-343">多种原因可能出现此错误。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="ac9fc-344">可以看到此错误的原因之一是，如果数据库脚本中包含单引号字符 （'），并且目标 MySQL 数据库的默认字符集为 utf-8。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="ac9fc-345">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-345">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-346">设置为远程的 MySQL 数据库设置为 utf-8 的默认字符。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>


<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="ac9fc-347">其他问题</span><span class="sxs-lookup"><span data-stu-id="ac9fc-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="ac9fc-348">问题： 搜索/筛选器不适合在报表中分组依据： 问题类型</span><span class="sxs-lookup"><span data-stu-id="ac9fc-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="ac9fc-349">当运行网站的报告，如果输入中的文本*按 URL 筛选*框，然后单击*搜索*，没有任何反应。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="ac9fc-350">这是因为此控件不起作用时*Group By*报表的状态设置为*问题类型*，这是默认设置。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="ac9fc-351">**解决方法**中*分组依据*选项卡的功能区中，单击*URL*进行分组的项按其源 URL。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="ac9fc-352">文本框和按钮，用于筛选条目都能运行时处于此状态。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-352">The text box and button to filter the entries are functional while in this state.</span></span>


#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="ac9fc-353">问题： 无法使用 IIS Express 运行 WCF 应用程序</span><span class="sxs-lookup"><span data-stu-id="ac9fc-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="ac9fc-354">浏览到 WCF 应用程序会导致类似于以下错误：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="ac9fc-355">*无法加载文件或程序集 Microsoft.Web.Administration，版本 = 7.0.0.0，区域性 = 中性，PublicKeyToken = 31bf3856ad364e35 或其某个依赖项。系统找不到指定的文件。*</span><span class="sxs-lookup"><span data-stu-id="ac9fc-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="ac9fc-356">发生这种情况是因为默认情况下，IIS Express 的 Beta 版本不支持 WCF。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="ac9fc-357">**解决方法**使用下列解决方法之一 (解决方法 2 要求 Microsoft Windows Vista 或更高版本):</span><span class="sxs-lookup"><span data-stu-id="ac9fc-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="ac9fc-358">复制*Microsoft.Web.dll*并*Microsoft.Web.Administration.dll*到 WebMatrix 安装位置中的程序集*bin* WCF 的目录应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="ac9fc-359">默认情况下，在安装 WebMatrix *Microsoft WebMatrix*系统的下的子文件夹*Program Files*文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="ac9fc-360">Microsoft Windows Vista 或更高版本，创建中的程序集的符号链接*bin*目录中使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="ac9fc-361">（这种方法的优点它不会创建一份程序集。）</span><span class="sxs-lookup"><span data-stu-id="ac9fc-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="ac9fc-362">在 GAC 中安装两个程序集。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="ac9fc-363">从提升的提示符下运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]


#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="ac9fc-364">问题： WebMatrix Beta 3 不能执行某些任务需要提升</span><span class="sxs-lookup"><span data-stu-id="ac9fc-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="ac9fc-365">WebMatrix Beta 3 不能执行某些任务需要提升，例如，在以下情况下安装其他组件：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="ac9fc-366">在 Windows Vista 或 Windows 7 中，使用不具有管理权限的帐户登录并禁用用户帐户控制 (UAC)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="ac9fc-367">使用 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="ac9fc-368">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-368">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-369">在 WebMatrix Beta 3 中的大多数任务不需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="ac9fc-370">对于那些确实可以执行的操作以管理员身份，或请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="ac9fc-371">在 Windows Vista 或 Windows 7，启用 UAC。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="ac9fc-372">在 Windows XP 中，将用户添加到管理员安全组。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-372">On Windows XP, add the user to the Administrators security group.</span></span>


#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="ac9fc-373">问题:"从 Web 库的站点"已禁用</span><span class="sxs-lookup"><span data-stu-id="ac9fc-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="ac9fc-374">**站点从 Web 库**如果未安装 Web 平台安装程序 3.0 选项被禁用。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="ac9fc-375">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-375">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-376">安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>


#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="ac9fc-377">问题： 在 Windows Server 2003、 IIS Express 不会启动非管理用户</span><span class="sxs-lookup"><span data-stu-id="ac9fc-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="ac9fc-378">Windows Server 2003 上启动的页或启动 IIS Express，IIS Express 不会启动。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="ac9fc-379">对于 Web 页面，错误将显示，指示某个非管理用户，启动该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="ac9fc-380">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-380">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-381">启动 WebMatrix Beta 3 作为管理用户。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="ac9fc-382">有关更多详细信息，请参阅以下知识库文章：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="ac9fc-383">由非管理用户启动的应用程序无法侦听到 Windows Vista、 Windows Server 2003 或 Windows XP 中运行应用程序的计算机的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="ac9fc-384">问题： Google Chrome 不能作为运行选项</span><span class="sxs-lookup"><span data-stu-id="ac9fc-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="ac9fc-385">在浏览器的列表中不显示 Google Chrome**运行**上**主页**选项卡。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="ac9fc-386">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-386">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-387">某些版本的 Google Chrome 并不能注册正确地与 Windows 中的默认程序功能。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="ac9fc-388">解决此问题，启动 Google Chrome 中，单击*自定义和控制 Google Chrome*菜单上，单击*选项*，然后单击*使 Google Chrome 我的默认浏览器*。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="ac9fc-389">问题:"外键"对话框中不允许输入主键</span><span class="sxs-lookup"><span data-stu-id="ac9fc-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="ac9fc-390">**外键**对话框不允许您输入从主键表的主键名称。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="ac9fc-391">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-391">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-392">这是有意为之。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-392">This is intentional.</span></span> <span data-ttu-id="ac9fc-393">不需要输入主键表的主键的名称。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-393">You do not need to enter the name of the primary key from the primary key table.</span></span>


#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="ac9fc-394">问题:"关系"按钮处于禁用状态</span><span class="sxs-lookup"><span data-stu-id="ac9fc-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="ac9fc-395">**关系**按钮下**表**选项卡中**数据库**禁用 SQL Server Compact 数据库的工作区。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="ac9fc-396">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-396">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-397">无。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-397">None.</span></span> <span data-ttu-id="ac9fc-398">SQL Server Compact 不支持表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-398">SQL Server Compact does not support relationships between tables.</span></span>


#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="ac9fc-399">问题： 参数化的 SQL 查询引发异常</span><span class="sxs-lookup"><span data-stu-id="ac9fc-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="ac9fc-400">在 SQL Server Compact 4.0 中，如果不会如指定的数据类型`SqlDbType`或`DbType`对于参数化查询中的参数，在查询运行时引发异常。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="ac9fc-401">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ac9fc-401">**Workaround**</span></span>  
> <span data-ttu-id="ac9fc-402">显式设置参数的数据类型，如`SqlDbType`或`DbType`。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="ac9fc-403">这是关键的 BLOB 数据类型 (`image`和`ntext`)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="ac9fc-404">使用如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]


<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="ac9fc-405">更多信息</span><span class="sxs-lookup"><span data-stu-id="ac9fc-405">For More Information</span></span>

<span data-ttu-id="ac9fc-406">有关 WebMatrix Beta 3 的详细信息，请参阅以下网站：</span><span class="sxs-lookup"><span data-stu-id="ac9fc-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="ac9fc-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="ac9fc-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="ac9fc-408">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="ac9fc-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="ac9fc-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="ac9fc-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

* * *

<span data-ttu-id="ac9fc-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="ac9fc-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="ac9fc-411">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-411">All Rights Reserved.</span></span> <span data-ttu-id="ac9fc-412">[使用条款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac9fc-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
