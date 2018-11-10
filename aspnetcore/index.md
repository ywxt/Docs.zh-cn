---
title: ASP.NET Core 简介
author: rick-anderson
description: 获取 ASP.NET Core 的简介，它是一个跨平台的高性能开源框架，用于生成基于云且连接 Internet 的新式应用程序。
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: index
ms.openlocfilehash: 60f7d64baa0441b90befb2d785999a707e1025c5
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225390"
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="e600f-103">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="e600f-103">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="e600f-104">作者：[Daniel Roth](https://github.com/danroth27)[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="e600f-104">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="e600f-105">ASP.NET Core 是一个跨平台的高性能[开源](https://github.com/aspnet/home)框架，用于生成基于云且连接 Internet 的新式应用程序。</span><span class="sxs-lookup"><span data-stu-id="e600f-105">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="e600f-106">使用 ASP.NET Core，您可以：</span><span class="sxs-lookup"><span data-stu-id="e600f-106">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="e600f-107">建置 Web 应用程序和服务、[IoT](https://www.microsoft.com/internet-of-things/) 应用和移动后端。</span><span class="sxs-lookup"><span data-stu-id="e600f-107">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="e600f-108">在 Windows、macOS 和 Linux 上使用喜爱的开发工具。</span><span class="sxs-lookup"><span data-stu-id="e600f-108">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="e600f-109">部署到云或本地。</span><span class="sxs-lookup"><span data-stu-id="e600f-109">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="e600f-110">在 [.NET Core 或 .NET Framework](/dotnet/articles/standard/choosing-core-framework-server) 上运行。</span><span class="sxs-lookup"><span data-stu-id="e600f-110">Run on [.NET Core or .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="e600f-111">为何使用 ASP.NET Core？</span><span class="sxs-lookup"><span data-stu-id="e600f-111">Why use ASP.NET Core?</span></span>

<span data-ttu-id="e600f-112">数百万开发人员使用过（并将继续使用）[ASP.NET 4.x](/aspnet/overview) 创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="e600f-112">Millions of developers have used (and continue to use) [ASP.NET 4.x](/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="e600f-113">ASP.NET Core 是重新设计的 ASP.NET 4.x，更改了体系结构，形成了更精简的模块化框架。</span><span class="sxs-lookup"><span data-stu-id="e600f-113">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="e600f-114">使用 ASP.NET Core MVC 生成 Web API 和 Web UI</span><span class="sxs-lookup"><span data-stu-id="e600f-114">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="e600f-115">ASP.NET Core MVC 提供生成 [Web API](xref:tutorials/first-web-api) 和 [Web 应用](xref:tutorials/razor-pages/index)所需的功能：</span><span class="sxs-lookup"><span data-stu-id="e600f-115">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/first-web-api) and [web apps](xref:tutorials/razor-pages/index):</span></span>

* <span data-ttu-id="e600f-116">[Model-View-Controller (MVC) 模式](xref:mvc/overview) 使 Web API 和 Web 应用可测试。</span><span class="sxs-lookup"><span data-stu-id="e600f-116">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps testable.</span></span>
* <span data-ttu-id="e600f-117">ASP.NET Core 2.0 中新增的 [Razor 页面](xref:razor-pages/index)是基于页面的编程模型，可简化 Web UI 生成并提高工作效率。</span><span class="sxs-lookup"><span data-stu-id="e600f-117">[Razor Pages](xref:razor-pages/index) (new in ASP.NET Core 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="e600f-118">[Razor 标记](xref:mvc/views/razor)提供了适用于 [Razor 页面](xref:razor-pages/index)和 [MVC 视图](xref:mvc/views/overview)的高效语法。</span><span class="sxs-lookup"><span data-stu-id="e600f-118">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="e600f-119">[标记帮助程序](xref:mvc/views/tag-helpers/intro)使服务器端代码可以在 Razor 文件中参与创建和呈现 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="e600f-119">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="e600f-120">内置的[多数据格式和内容协商](xref:web-api/advanced/formatting)支持使 Web API 可访问多种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="e600f-120">Built-in support for [multiple data formats and content negotiation](xref:web-api/advanced/formatting) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="e600f-121">[模型绑定](xref:mvc/models/model-binding)自动将 HTTP 请求中的数据映射到操作方法参数。</span><span class="sxs-lookup"><span data-stu-id="e600f-121">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="e600f-122">[模型验证](xref:mvc/models/validation)自动执行客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="e600f-122">[Model validation](xref:mvc/models/validation) automatically performs client-side and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="e600f-123">客户端开发</span><span class="sxs-lookup"><span data-stu-id="e600f-123">Client-side development</span></span>

<span data-ttu-id="e600f-124">ASP.NET Core 与常用客户端框架和库（包括 [Angular](xref:spa/angular)、[React](xref:spa/react) 和 [Bootstrap](https://getbootstrap.com/)）无缝集成。</span><span class="sxs-lookup"><span data-stu-id="e600f-124">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](https://getbootstrap.com/).</span></span> <span data-ttu-id="e600f-125">有关详细信息，请参阅[客户端开发](xref:client-side/index)。</span><span class="sxs-lookup"><span data-stu-id="e600f-125">For more information, see [Client-side development](xref:client-side/index).</span></span>

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a><span data-ttu-id="e600f-126">面向 .NET Framework 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e600f-126">ASP.NET Core targeting .NET Framework</span></span>

<span data-ttu-id="e600f-127">ASP.NET Core 2.x 可以面向 .NET Core 或 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="e600f-127">ASP.NET Core 2.x can target .NET Core or .NET Framework.</span></span> <span data-ttu-id="e600f-128">面向 .NET Framework 的 ASP.NET Core 应用无法跨平台，它们仅在 Windows 上运行。</span><span class="sxs-lookup"><span data-stu-id="e600f-128">ASP.NET Core apps targeting .NET Framework aren't cross-platform&mdash;they run on Windows only.</span></span> <span data-ttu-id="e600f-129">通常，ASP.NET Core 2.x 由 [.NET Standard](/dotnet/standard/net-standard) 库组成。</span><span class="sxs-lookup"><span data-stu-id="e600f-129">Generally, ASP.NET Core 2.x is made up of [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="e600f-130">使用 .NET Standard 2.0 编写的应用可在 NET Standard 2.0 支持的任何位置运行。</span><span class="sxs-lookup"><span data-stu-id="e600f-130">Apps written with .NET Standard 2.0 run anywhere that .NET Standard 2.0 is supported.</span></span>

<span data-ttu-id="e600f-131">与 .NET Standard 2.0 兼容的 .NET Framework 版本支持 ASP.NET Core 2.x：</span><span class="sxs-lookup"><span data-stu-id="e600f-131">ASP.NET Core 2.x is supported on .NET Framework versions compatible with .NET Standard 2.0:</span></span>

* <span data-ttu-id="e600f-132">强烈建议使用 .NET Framework 4.7.1 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="e600f-132">.NET Framework 4.7.1 and later is strongly recommended.</span></span>
* <span data-ttu-id="e600f-133">.NET Framework 4.6.1 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="e600f-133">.NET Framework 4.6.1 and later.</span></span>

<span data-ttu-id="e600f-134">ASP.NET Core 3.0 以及更高版本只能在 .NET Core 中运行。</span><span class="sxs-lookup"><span data-stu-id="e600f-134">ASP.NET Core 3.0 and later will only run on .NET Core.</span></span> <span data-ttu-id="e600f-135">有关此更改的详细信息，请参阅 [A first look at changes coming in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/)（抢先了解 ASP.NET Core 3.0 即将推出的更改）。</span><span class="sxs-lookup"><span data-stu-id="e600f-135">For more details regarding this change, see [A first look at changes coming in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/).</span></span>

<span data-ttu-id="e600f-136">面向 .NET Core 有以下几个优势，并且这些优势会随着每次发布增加。</span><span class="sxs-lookup"><span data-stu-id="e600f-136">There are several advantages to targeting .NET Core, and these advantages increase with each release.</span></span> <span data-ttu-id="e600f-137">与 .NET Framework 相比，.NET Core 的部分优势包括：</span><span class="sxs-lookup"><span data-stu-id="e600f-137">Some advantages of .NET Core over .NET Framework include:</span></span>

* <span data-ttu-id="e600f-138">跨平台。</span><span class="sxs-lookup"><span data-stu-id="e600f-138">Cross-platform.</span></span> <span data-ttu-id="e600f-139">在 macOS、Linux 和 Windows 上运行。</span><span class="sxs-lookup"><span data-stu-id="e600f-139">Runs on macOS, Linux, and Windows.</span></span>
* <span data-ttu-id="e600f-140">提高的性能</span><span class="sxs-lookup"><span data-stu-id="e600f-140">Improved performance</span></span>
* <span data-ttu-id="e600f-141">并行版本控制</span><span class="sxs-lookup"><span data-stu-id="e600f-141">Side-by-side versioning</span></span>
* <span data-ttu-id="e600f-142">新 API</span><span class="sxs-lookup"><span data-stu-id="e600f-142">New APIs</span></span>
* <span data-ttu-id="e600f-143">开源</span><span class="sxs-lookup"><span data-stu-id="e600f-143">Open source</span></span>

<span data-ttu-id="e600f-144">我们正努力缩小 .NET Framework 与 .NET Core 的 API 差距。</span><span class="sxs-lookup"><span data-stu-id="e600f-144">We're working hard to close the API gap from .NET Framework to .NET Core.</span></span> <span data-ttu-id="e600f-145">[Windows 兼容性包](/dotnet/core/porting/windows-compat-pack)使数千个仅可在Windows运行的API 可在 .NET Core 中使用。</span><span class="sxs-lookup"><span data-stu-id="e600f-145">The [Windows Compatibility Pack](/dotnet/core/porting/windows-compat-pack) made thousands of Windows-only APIs available in .NET Core.</span></span> <span data-ttu-id="e600f-146">这些 API 在 .NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="e600f-146">These APIs weren't available in .NET Core 1.x.</span></span>

## <a name="how-to-download-a-sample"></a><span data-ttu-id="e600f-147">如何下载示例</span><span class="sxs-lookup"><span data-stu-id="e600f-147">How to download a sample</span></span>

<span data-ttu-id="e600f-148">很多文章和教程中都包含有示例代码链接。</span><span class="sxs-lookup"><span data-stu-id="e600f-148">Many of the articles and tutorials include links to sample code.</span></span>

1. <span data-ttu-id="e600f-149">[下载 ASP.NET 存储库 zip 文件](https://codeload.github.com/aspnet/Docs/zip/master)。</span><span class="sxs-lookup"><span data-stu-id="e600f-149">[Download the ASP.NET repository zip file](https://codeload.github.com/aspnet/Docs/zip/master).</span></span>
1. <span data-ttu-id="e600f-150">解压缩 Docs-master.zip 文件。</span><span class="sxs-lookup"><span data-stu-id="e600f-150">Unzip the *Docs-master.zip* file.</span></span>
1. <span data-ttu-id="e600f-151">使用示例链接中的 URL 帮助你导航到示例目录。</span><span class="sxs-lookup"><span data-stu-id="e600f-151">Use the URL in the sample link to help you navigate to the sample directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e600f-152">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e600f-152">Next steps</span></span>

<span data-ttu-id="e600f-153">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="e600f-153">For more information, see the following resources:</span></span>

* [<span data-ttu-id="e600f-154">Razor 页面入门</span><span class="sxs-lookup"><span data-stu-id="e600f-154">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [<span data-ttu-id="e600f-155">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="e600f-155">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="e600f-156">[每周 ASP.NET Community Standup](https://live.asp.net/) 介绍了团队的工作进度和计划。</span><span class="sxs-lookup"><span data-stu-id="e600f-156">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="e600f-157">它以新博客和第三方软件为重点。</span><span class="sxs-lookup"><span data-stu-id="e600f-157">It features new blogs and third-party software.</span></span>
