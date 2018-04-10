---
title: 在 ASP.NET 核心中的捆绑和 minifiy 静态资产
author: scottaddie
description: 了解如何通过应用绑定和缩减技术优化 ASP.NET 核心 web 应用程序中的静态资源。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 01/10/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: client-side/bundling-and-minification
ms.openlocfilehash: a155422c0fd638f46fe4a9d8a77faebc0b2a5681
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
---
# <a name="bundle-and-minifiy-static-assets-in-aspnet-core"></a><span data-ttu-id="b2fb0-103">在 ASP.NET 核心中的捆绑和 minifiy 静态资产</span><span class="sxs-lookup"><span data-stu-id="b2fb0-103">Bundle and minifiy static assets in ASP.NET Core</span></span>

<span data-ttu-id="b2fb0-104">作者：[Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="b2fb0-104">By [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="b2fb0-105">本文介绍了应用绑定和缩减，包括如何使用 ASP.NET Core web apps 使用这些功能的好处。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-105">This article explains the benefits of applying bundling and minification, including how these features can be used with ASP.NET Core web apps.</span></span>

## <a name="what-is-bundling-and-minification"></a><span data-ttu-id="b2fb0-106">绑定和缩减是什么？</span><span class="sxs-lookup"><span data-stu-id="b2fb0-106">What is bundling and minification?</span></span>

<span data-ttu-id="b2fb0-107">绑定和缩减是可以应用的 web 应用中的两个不同的性能优化。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-107">Bundling and minification are two distinct performance optimizations you can apply in a web app.</span></span> <span data-ttu-id="b2fb0-108">一起使用时，绑定和缩减提高性能通过减少服务器请求数和减少的请求的静态资产的大小。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-108">Used together, bundling and minification improve performance by reducing the number of server requests and reducing the size of the requested static assets.</span></span>

<span data-ttu-id="b2fb0-109">绑定和缩减主要提高第一个页面请求加载时间。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-109">Bundling and minification primarily improve the first page request load time.</span></span> <span data-ttu-id="b2fb0-110">一旦已请求网页上，浏览器缓存静态资产 （JavaScript、 CSS 和图像）。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-110">Once a web page has been requested, the browser caches the static assets (JavaScript, CSS, and images).</span></span> <span data-ttu-id="b2fb0-111">因此，绑定和缩减不时提高性能请求的同一页上或页，请求相同的资产在同一站点上。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-111">Consequently, bundling and minification don't improve performance when requesting the same page, or pages, on the same site requesting the same assets.</span></span> <span data-ttu-id="b2fb0-112">如果过期在资产上未正确设置标头和如果未使用绑定和缩减，浏览器的新鲜度试探方法将标记资产陈旧在几天后。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-112">If the expires header isn't set correctly on the assets and if bundling and minification isn't used, the browser's freshness heuristics mark the assets stale after a few days.</span></span> <span data-ttu-id="b2fb0-113">此外，浏览器需要为每个资产的验证请求。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-113">Additionally, the browser requires a validation request for each asset.</span></span> <span data-ttu-id="b2fb0-114">在这种情况下，绑定和缩减提供在第一个页面请求后的提高性能。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-114">In this case, bundling and minification provide a performance improvement even after the first page request.</span></span>

### <a name="bundling"></a><span data-ttu-id="b2fb0-115">绑定</span><span class="sxs-lookup"><span data-stu-id="b2fb0-115">Bundling</span></span>

<span data-ttu-id="b2fb0-116">绑定将多个文件合并到单个文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-116">Bundling combines multiple files into a single file.</span></span> <span data-ttu-id="b2fb0-117">绑定可减少的所需呈现 web 资产，例如 web 页的服务器请求数。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-117">Bundling reduces the number of server requests which are necessary to render a web asset, such as a web page.</span></span> <span data-ttu-id="b2fb0-118">可以专门为 CSS、 JavaScript 等创建任意数量的各项捆绑。少选一些文件意味着从浏览器到服务器或提供你的应用程序的服务的少数几个 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-118">You can create any number of individual bundles specifically for CSS, JavaScript, etc. Fewer files means fewer HTTP requests from the browser to the server or from the service providing your application.</span></span> <span data-ttu-id="b2fb0-119">第一个页面加载性能改善中的此结果。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-119">This results in improved first page load performance.</span></span>

### <a name="minification"></a><span data-ttu-id="b2fb0-120">缩减</span><span class="sxs-lookup"><span data-stu-id="b2fb0-120">Minification</span></span>

<span data-ttu-id="b2fb0-121">缩减从代码中移除而无需更改功能的不必要的字符。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-121">Minification removes unnecessary characters from code without altering functionality.</span></span> <span data-ttu-id="b2fb0-122">结果是显著的大小减少请求资产 （如 CSS、 映像和 JavaScript 文件） 中。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-122">The result is a significant size reduction in requested assets (such as CSS, images, and JavaScript files).</span></span> <span data-ttu-id="b2fb0-123">常见的缩减的负面影响包括缩短为一个字符的变量名和删除注释和多余的空格。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-123">Common side effects of minification include shortening variable names to one character and removing comments and unnecessary whitespace.</span></span>

<span data-ttu-id="b2fb0-124">请考虑下面的 JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-124">Consider the following JavaScript function:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

<span data-ttu-id="b2fb0-125">缩减缩小为以下函数：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-125">Minification reduces the function to the following:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

<span data-ttu-id="b2fb0-126">除了删除注释和多余的空格，则以下参数和变量已重命名名称，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-126">In addition to removing the comments and unnecessary whitespace, the following parameter and variable names were renamed as follows:</span></span>

<span data-ttu-id="b2fb0-127">原始</span><span class="sxs-lookup"><span data-stu-id="b2fb0-127">Original</span></span> | <span data-ttu-id="b2fb0-128">重命名</span><span class="sxs-lookup"><span data-stu-id="b2fb0-128">Renamed</span></span>
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a><span data-ttu-id="b2fb0-129">绑定和缩减的影响</span><span class="sxs-lookup"><span data-stu-id="b2fb0-129">Impact of bundling and minification</span></span>

<span data-ttu-id="b2fb0-130">下表概述了单独加载资产与使用绑定和缩减之间的差异：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-130">The following table outlines differences between individually loading assets and using bundling and minification:</span></span>

<span data-ttu-id="b2fb0-131">操作</span><span class="sxs-lookup"><span data-stu-id="b2fb0-131">Action</span></span> | <span data-ttu-id="b2fb0-132">与 B/M</span><span class="sxs-lookup"><span data-stu-id="b2fb0-132">With B/M</span></span> | <span data-ttu-id="b2fb0-133">而无需 B/M</span><span class="sxs-lookup"><span data-stu-id="b2fb0-133">Without B/M</span></span> | <span data-ttu-id="b2fb0-134">更改</span><span class="sxs-lookup"><span data-stu-id="b2fb0-134">Change</span></span>
--- | :---: | :---: | :---:
<span data-ttu-id="b2fb0-135">文件请求</span><span class="sxs-lookup"><span data-stu-id="b2fb0-135">File Requests</span></span>  | <span data-ttu-id="b2fb0-136">7</span><span class="sxs-lookup"><span data-stu-id="b2fb0-136">7</span></span>   | <span data-ttu-id="b2fb0-137">18</span><span class="sxs-lookup"><span data-stu-id="b2fb0-137">18</span></span>     | <span data-ttu-id="b2fb0-138">157%</span><span class="sxs-lookup"><span data-stu-id="b2fb0-138">157%</span></span>
<span data-ttu-id="b2fb0-139">传输的 KB</span><span class="sxs-lookup"><span data-stu-id="b2fb0-139">KB Transferred</span></span> | <span data-ttu-id="b2fb0-140">156</span><span class="sxs-lookup"><span data-stu-id="b2fb0-140">156</span></span> | <span data-ttu-id="b2fb0-141">264.68</span><span class="sxs-lookup"><span data-stu-id="b2fb0-141">264.68</span></span> | <span data-ttu-id="b2fb0-142">70%</span><span class="sxs-lookup"><span data-stu-id="b2fb0-142">70%</span></span>
<span data-ttu-id="b2fb0-143">加载时间 (ms)</span><span class="sxs-lookup"><span data-stu-id="b2fb0-143">Load Time (ms)</span></span> | <span data-ttu-id="b2fb0-144">885</span><span class="sxs-lookup"><span data-stu-id="b2fb0-144">885</span></span> | <span data-ttu-id="b2fb0-145">2360</span><span class="sxs-lookup"><span data-stu-id="b2fb0-145">2360</span></span>   | <span data-ttu-id="b2fb0-146">167%</span><span class="sxs-lookup"><span data-stu-id="b2fb0-146">167%</span></span>

<span data-ttu-id="b2fb0-147">浏览器是相当详细方面 HTTP 请求标头。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-147">Browsers are fairly verbose with regard to HTTP request headers.</span></span> <span data-ttu-id="b2fb0-148">发送的总字节数度量值绑定时见到显著减少。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-148">The total bytes sent metric saw a significant reduction when bundling.</span></span> <span data-ttu-id="b2fb0-149">加载时显示的重大进步，但此示例中本地运行。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-149">The load time shows a significant improvement, however this example ran locally.</span></span> <span data-ttu-id="b2fb0-150">使用资产的绑定和缩减通过网络传输时，在实现更高的性能增益。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-150">Greater performance gains are realized when using bundling and minification with assets transferred over a network.</span></span>

## <a name="choose-a-bundling-and-minification-strategy"></a><span data-ttu-id="b2fb0-151">选择绑定和缩减策略</span><span class="sxs-lookup"><span data-stu-id="b2fb0-151">Choose a bundling and minification strategy</span></span>

<span data-ttu-id="b2fb0-152">MVC 和 Razor 页项目模板提供的绑定和缩减包含的 JSON 配置文件的现成可用解决方案。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-152">The MVC and Razor Pages project templates provide an out-of-the-box solution for bundling and minification consisting of a JSON configuration file.</span></span> <span data-ttu-id="b2fb0-153">第三方工具，如[Gulp](xref:client-side/using-gulp)和[Grunt](xref:client-side/using-grunt)任务流道，完成相同任务的更多的复杂性。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-153">Third-party tools, such as the [Gulp](xref:client-side/using-gulp) and [Grunt](xref:client-side/using-grunt) task runners, accomplish the same tasks with a bit more complexity.</span></span> <span data-ttu-id="b2fb0-154">第三方工具开发工作流需要超出绑定和缩减的处理时非常适合&mdash;如 linting 和映像的优化。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-154">A third-party tool is a great fit when your development workflow requires processing beyond bundling and minification&mdash;such as linting and image optimization.</span></span> <span data-ttu-id="b2fb0-155">通过使用设计时绑定和缩减，在应用程序的部署之前创建缩减的文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-155">By using design-time bundling and minification, the minified files are created prior to the app's deployment.</span></span> <span data-ttu-id="b2fb0-156">绑定和在部署前贴图层提供减少的服务器负载的优点。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-156">Bundling and minifying before deployment provides the advantage of reduced server load.</span></span> <span data-ttu-id="b2fb0-157">但是，务必要识别该设计时绑定，缩减会增加生成复杂性，并且仅适用于静态文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-157">However, it's important to recognize that design-time bundling and minification increases build complexity and only works with static files.</span></span>

## <a name="configure-bundling-and-minification"></a><span data-ttu-id="b2fb0-158">配置绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="b2fb0-158">Configure bundling and minification</span></span>

<span data-ttu-id="b2fb0-159">MVC 和 Razor 页项目模板提供了*bundleconfig.json*配置文件用于定义每个捆绑包的选项。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-159">The MVC and Razor Pages project templates provide a *bundleconfig.json* configuration file which defines the options for each bundle.</span></span> <span data-ttu-id="b2fb0-160">默认情况下，一个捆绑包配置定义的自定义 javascript (*wwwroot/js/site.js*) 和样式表 (*wwwroot/css/site.css*) 文件：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-160">By default, a single bundle configuration is defined for the custom JavaScript (*wwwroot/js/site.js*) and stylesheet (*wwwroot/css/site.css*) files:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

<span data-ttu-id="b2fb0-161">配置选项包括：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-161">Configuration options include:</span></span>

* <span data-ttu-id="b2fb0-162">`outputFileName`： 要输出的捆绑文件名称。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-162">`outputFileName`: The name of the bundle file to output.</span></span> <span data-ttu-id="b2fb0-163">可以包含中的相对路径*bundleconfig.json*文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-163">Can contain a relative path from the *bundleconfig.json* file.</span></span> <span data-ttu-id="b2fb0-164">**required**</span><span class="sxs-lookup"><span data-stu-id="b2fb0-164">**required**</span></span>
* <span data-ttu-id="b2fb0-165">`inputFiles`： 要将捆绑在一起的文件的数组。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-165">`inputFiles`: An array of files to bundle together.</span></span> <span data-ttu-id="b2fb0-166">这些是配置文件的相对路径。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-166">These are relative paths to the configuration file.</span></span> <span data-ttu-id="b2fb0-167">**可选**，\* 空值会在空的输出文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-167">**optional**, \*an empty value results in an empty output file.</span></span> <span data-ttu-id="b2fb0-168">[组合](http://www.tldp.org/LDP/abs/html/globbingref.html)支持模式。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-168">[globbing](http://www.tldp.org/LDP/abs/html/globbingref.html) patterns are supported.</span></span>
* <span data-ttu-id="b2fb0-169">`minify`： 输出类型缩减选项。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-169">`minify`: The minification options for the output type.</span></span> <span data-ttu-id="b2fb0-170">**可选**，*默认值- `minify: { enabled: true }`*</span><span class="sxs-lookup"><span data-stu-id="b2fb0-170">**optional**, *default - `minify: { enabled: true }`*</span></span>
  * <span data-ttu-id="b2fb0-171">每个输出文件类型有配置选项。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-171">Configuration options are available per output file type.</span></span>
    * [<span data-ttu-id="b2fb0-172">CSS Minifier</span><span class="sxs-lookup"><span data-stu-id="b2fb0-172">CSS Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [<span data-ttu-id="b2fb0-173">JavaScript Minifier</span><span class="sxs-lookup"><span data-stu-id="b2fb0-173">JavaScript Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [<span data-ttu-id="b2fb0-174">HTML Minifier</span><span class="sxs-lookup"><span data-stu-id="b2fb0-174">HTML Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki)
* <span data-ttu-id="b2fb0-175">`includeInProject`： 指示是否将生成的文件添加到项目文件的标志。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-175">`includeInProject`: Flag indicating whether to add generated files to project file.</span></span> <span data-ttu-id="b2fb0-176">**可选**，*默认-false*</span><span class="sxs-lookup"><span data-stu-id="b2fb0-176">**optional**, *default - false*</span></span>
* <span data-ttu-id="b2fb0-177">`sourceMap`： 指示是否生成捆绑的文件的源映射的标志。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-177">`sourceMap`: Flag indicating whether to generate a source map for the bundled file.</span></span> <span data-ttu-id="b2fb0-178">**可选**，*默认-false*</span><span class="sxs-lookup"><span data-stu-id="b2fb0-178">**optional**, *default - false*</span></span>
* <span data-ttu-id="b2fb0-179">`sourceMapRootPath`： 用于存储生成的源代码映射文件的根路径。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-179">`sourceMapRootPath`: The root path for storing the generated source map file.</span></span>

## <a name="build-time-execution-of-bundling-and-minification"></a><span data-ttu-id="b2fb0-180">生成时执行的绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="b2fb0-180">Build-time execution of bundling and minification</span></span>

<span data-ttu-id="b2fb0-181">[BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet 包启用的绑定执行并在生成时的缩减。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-181">The [BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet package enables the execution of bundling and minification at build time.</span></span> <span data-ttu-id="b2fb0-182">包插入[MSBuild 目标](/visualstudio/msbuild/msbuild-targets)在生成和清理时间运行。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-182">The package injects [MSBuild Targets](/visualstudio/msbuild/msbuild-targets) which run at build and clean time.</span></span> <span data-ttu-id="b2fb0-183">*Bundleconfig.json*文件分析由生成过程以生成基于定义的配置的输出文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-183">The *bundleconfig.json* file is analyzed by the build process to produce the output files based on the defined configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="b2fb0-184">BuildBundlerMinifier 属于在为其 Microsoft 不提供支持的 GitHub 上的社区主导项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-184">BuildBundlerMinifier belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="b2fb0-185">应归档问题[此处](https://github.com/madskristensen/BundlerMinifier/issues)。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-185">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="b2fb0-186">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b2fb0-186">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="b2fb0-187">添加*BuildBundlerMinifier*包到你的项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-187">Add the *BuildBundlerMinifier* package to your project.</span></span>

<span data-ttu-id="b2fb0-188">生成项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-188">Build the project.</span></span> <span data-ttu-id="b2fb0-189">以下内容出现在输出窗口：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-189">The following appears in the Output window:</span></span>

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Begin processing bundleconfig.json
1>  Minified wwwroot/css/site.min.css
1>  Minified wwwroot/js/site.min.js
1>Bundler: Done processing bundleconfig.json
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

<span data-ttu-id="b2fb0-190">清除该项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-190">Clean the project.</span></span> <span data-ttu-id="b2fb0-191">以下内容出现在输出窗口：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-191">The following appears in the Output window:</span></span>

```console
1>------ Clean started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Cleaning output from bundleconfig.json
1>Bundler: Done cleaning output file from bundleconfig.json
========== Clean: 1 succeeded, 0 failed, 0 skipped ==========
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="b2fb0-192">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="b2fb0-192">.NET Core CLI</span></span>](#tab/netcore-cli) 

<span data-ttu-id="b2fb0-193">添加*BuildBundlerMinifier*包到你的项目：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-193">Add the *BuildBundlerMinifier* package to your project:</span></span>

```console
dotnet add package BuildBundlerMinifier
```

<span data-ttu-id="b2fb0-194">如果使用 ASP.NET 核心 1.x，还原新添加的包：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-194">If using ASP.NET Core 1.x, restore the newly added package:</span></span>

```console
dotnet restore
```

<span data-ttu-id="b2fb0-195">生成项目：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-195">Build the project:</span></span>

```console
dotnet build
```

<span data-ttu-id="b2fb0-196">将显示以下：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-196">The following appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


    Bundler: Begin processing bundleconfig.json
    Bundler: Done processing bundleconfig.json
    BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
```

<span data-ttu-id="b2fb0-197">清除该项目：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-197">Clean the project:</span></span>

```console
dotnet clean
```

<span data-ttu-id="b2fb0-198">显示以下输出：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-198">The following output appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a><span data-ttu-id="b2fb0-199">绑定和缩减的即席执行</span><span class="sxs-lookup"><span data-stu-id="b2fb0-199">Ad hoc execution of bundling and minification</span></span>

<span data-ttu-id="b2fb0-200">它是无法在临时上, 运行的绑定和缩减的任务，而不生成项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-200">It's possible to run the bundling and minification tasks on an ad hoc basis, without building the project.</span></span> <span data-ttu-id="b2fb0-201">添加[BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/)到你的项目的 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-201">Add the [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet package to your project:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> <span data-ttu-id="b2fb0-202">BundlerMinifier.Core 属于在为其 Microsoft 不提供支持的 GitHub 上的社区主导项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-202">BundlerMinifier.Core belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="b2fb0-203">应归档问题[此处](https://github.com/madskristensen/BundlerMinifier/issues)。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-203">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="b2fb0-204">此包扩展以包括.NET 核心 CLI *dotnet 捆绑*工具。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-204">This package extends the .NET Core CLI to include the *dotnet-bundle* tool.</span></span> <span data-ttu-id="b2fb0-205">在包管理器控制台 (PMC) 窗口中或在命令行界面，可以执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-205">The following command can be executed in the Package Manager Console (PMC) window or in a command shell:</span></span>

```console
dotnet bundle
```

> [!IMPORTANT]
> <span data-ttu-id="b2fb0-206">NuGet 包管理器将依赖项添加到 \*.csproj 文件作为`<PackageReference />`节点。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-206">NuGet Package Manager adds dependencies to the \*.csproj file as `<PackageReference />` nodes.</span></span> <span data-ttu-id="b2fb0-207">`dotnet bundle`命令注册.NET 核心 CLI 时，才`<DotNetCliToolReference />`使用节点。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-207">The `dotnet bundle` command is registered with the .NET Core CLI only when a `<DotNetCliToolReference />` node is used.</span></span> <span data-ttu-id="b2fb0-208">相应地修改 \*.csproj 文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-208">Modify the \*.csproj file accordingly.</span></span>

## <a name="add-files-to-workflow"></a><span data-ttu-id="b2fb0-209">将文件添加到工作流</span><span class="sxs-lookup"><span data-stu-id="b2fb0-209">Add files to workflow</span></span>

<span data-ttu-id="b2fb0-210">考虑在其中一个示例附加*custom.css*文件会添加与下面类似的：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-210">Consider an example in which an additional *custom.css* file is added resembling the following:</span></span>

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

<span data-ttu-id="b2fb0-211">若要 minify *custom.css*和捆绑其与*site.css*到*site.min.css*文件中，添加的相对路径*bundleconfig.json*:</span><span class="sxs-lookup"><span data-stu-id="b2fb0-211">To minify *custom.css* and bundle it with *site.css* into a *site.min.css* file, add the relative path to *bundleconfig.json*:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> <span data-ttu-id="b2fb0-212">或者，可使用以下的组合模式：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-212">Alternatively, the following globbing pattern could be used:</span></span>
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css)"]
> ```
>
> <span data-ttu-id="b2fb0-213">此组合模式匹配所有 CSS 文件，并排除缩减的文件模式。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-213">This globbing pattern matches all CSS files and excludes the minified file pattern.</span></span>

<span data-ttu-id="b2fb0-214">生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-214">Build the application.</span></span> <span data-ttu-id="b2fb0-215">打开*site.min.css* ，并注意的内容*custom.css*追加到文件末尾。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-215">Open *site.min.css* and notice the content of *custom.css* is appended to the end of the file.</span></span>

## <a name="environment-based-bundling-and-minification"></a><span data-ttu-id="b2fb0-216">基于环境的绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="b2fb0-216">Environment-based bundling and minification</span></span>

<span data-ttu-id="b2fb0-217">作为最佳做法，应在生产环境中使用你的应用的捆绑和缩减型文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-217">As a best practice, the bundled and minified files of your app should be used in a production environment.</span></span> <span data-ttu-id="b2fb0-218">在开发期间，为方便调试应用程序将使原始文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-218">During development, the original files make for easier debugging of the app.</span></span>

<span data-ttu-id="b2fb0-219">指定要通过使用在您的网页中包括哪些文件[环境标记帮助器](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)在您的视图。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-219">Specify which files to include in your pages by using the [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) in your views.</span></span> <span data-ttu-id="b2fb0-220">环境标记帮助器只呈现其内容，在特定运行时[环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-220">The Environment Tag Helper only renders its contents when running in specific [environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="b2fb0-221">以下`environment`标记将呈现的未处理的 CSS 文件，在运行时`Development`环境：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-221">The following `environment` tag renders the unprocessed CSS files when running in the `Development` environment:</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b2fb0-222">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b2fb0-222">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b2fb0-223">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b2fb0-223">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

* * *
<span data-ttu-id="b2fb0-224">以下`environment`标记呈现捆绑和缩减型 CSS 文件，而不在环境中运行时`Development`。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-224">The following `environment` tag renders the bundled and minified CSS files when running in an environment other than `Development`.</span></span> <span data-ttu-id="b2fb0-225">例如，在运行`Production`或`Staging`触发这些样式表的呈现：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-225">For example, running in `Production` or `Staging` triggers the rendering of these stylesheets:</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b2fb0-226">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b2fb0-226">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b2fb0-227">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b2fb0-227">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

* * *
## <a name="consume-bundleconfigjson-from-gulp"></a><span data-ttu-id="b2fb0-228">使用从 Gulp bundleconfig.json</span><span class="sxs-lookup"><span data-stu-id="b2fb0-228">Consume bundleconfig.json from Gulp</span></span>

<span data-ttu-id="b2fb0-229">在情况下在其中应用的绑定和缩减工作流需要额外的处理。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-229">There are cases in which an app's bundling and minification workflow requires additional processing.</span></span> <span data-ttu-id="b2fb0-230">示例包括映像优化、 缓存清除功能，和 CDN 资产处理。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-230">Examples include image optimization, cache busting, and CDN asset processing.</span></span> <span data-ttu-id="b2fb0-231">若要满足这些要求，则可以将绑定和缩减工作流使用 Gulp。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-231">To satisfy these requirements, you can convert the bundling and minification workflow to use Gulp.</span></span>

### <a name="use-the-bundler--minifier-extension"></a><span data-ttu-id="b2fb0-232">使用捆绑包 （&） Minifier 扩展</span><span class="sxs-lookup"><span data-stu-id="b2fb0-232">Use the Bundler & Minifier extension</span></span>

<span data-ttu-id="b2fb0-233">Visual Studio[捆绑包 （&) Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier)扩展会转换为 Gulp。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-233">The Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) extension handles the conversion to Gulp.</span></span>

> [!NOTE]
> <span data-ttu-id="b2fb0-234">捆绑包 （&） Minifier 扩展属于在为其 Microsoft 不提供支持的 GitHub 上的社区主导项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-234">The Bundler & Minifier extension belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="b2fb0-235">应归档问题[此处](https://github.com/madskristensen/BundlerMinifier/issues)。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-235">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="b2fb0-236">右键单击*bundleconfig.json*文件在解决方案资源管理器中，然后选择**捆绑包 （&) Minifier** > **转换到的 Gulp...**:</span><span class="sxs-lookup"><span data-stu-id="b2fb0-236">Right-click the *bundleconfig.json* file in Solution Explorer and select **Bundler & Minifier** > **Convert To Gulp...**:</span></span>

![将转换到的 Gulp 上下文菜单项](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

<span data-ttu-id="b2fb0-238">*Gulpfile.js*和*package.json*文件添加到项目。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-238">The *gulpfile.js* and *package.json* files are added to the project.</span></span> <span data-ttu-id="b2fb0-239">支持[npm](https://www.npmjs.com/)中列出的包*package.json*文件的`devDependencies`部分安装。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-239">The supporting [npm](https://www.npmjs.com/) packages listed in the *package.json* file's `devDependencies` section are installed.</span></span>

<span data-ttu-id="b2fb0-240">为全局依赖项安装的 Gulp CLI PMC 窗口中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-240">Run the following command in the PMC window to install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="b2fb0-241">*Gulpfile.js*文件读取*bundleconfig.json*输入、 输出和设置的文件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-241">The *gulpfile.js* file reads the *bundleconfig.json* file for the inputs, outputs, and settings.</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a><span data-ttu-id="b2fb0-242">手动转换</span><span class="sxs-lookup"><span data-stu-id="b2fb0-242">Convert manually</span></span>

<span data-ttu-id="b2fb0-243">如果 Visual Studio 和/或捆绑包 （&） Minifier 扩展都不可用，将转换手动。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-243">If Visual Studio and/or the Bundler & Minifier extension aren't available, convert manually.</span></span>

<span data-ttu-id="b2fb0-244">添加*package.json*文件中的，替换为以下`devDependencies`，与项目根目录：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-244">Add a *package.json* file, with the following `devDependencies`, to the project root:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

<span data-ttu-id="b2fb0-245">通过在相同的级别中运行以下命令安装依赖项*package.json*:</span><span class="sxs-lookup"><span data-stu-id="b2fb0-245">Install the dependencies by running the following command at the same level as *package.json*:</span></span>

```console
npm i
```

<span data-ttu-id="b2fb0-246">为全局依赖项安装的 Gulp CLI:</span><span class="sxs-lookup"><span data-stu-id="b2fb0-246">Install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="b2fb0-247">复制*gulpfile.js*到项目根目录下面文件：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-247">Copy the *gulpfile.js* file below to the project root:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a><span data-ttu-id="b2fb0-248">运行 Gulp 任务</span><span class="sxs-lookup"><span data-stu-id="b2fb0-248">Run Gulp tasks</span></span>

<span data-ttu-id="b2fb0-249">若要触发 Gulp 缩减任务之前生成 Visual Studio 中的项目，添加以下[MSBuild 目标](/visualstudio/msbuild/msbuild-targets)\*.csproj 文件：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-249">To trigger the Gulp minification task before the project builds in Visual Studio, add the following [MSBuild Target](/visualstudio/msbuild/msbuild-targets) to the \*.csproj file:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

<span data-ttu-id="b2fb0-250">在此示例中，在内定义的任何任务`MyPreCompileTarget`目标之前预定义运行`Build`目标。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-250">In this example, any tasks defined within the `MyPreCompileTarget` target run before the predefined `Build` target.</span></span> <span data-ttu-id="b2fb0-251">在 Visual Studio 输出窗口将显示类似于下面的输出：</span><span class="sxs-lookup"><span data-stu-id="b2fb0-251">Output similar to the following appears in Visual Studio's Output window:</span></span>

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
1>[14:17:49] Using gulpfile C:\BuildBundlerMinifierApp\gulpfile.js
1>[14:17:49] Starting 'min:js'...
1>[14:17:49] Starting 'min:css'...
1>[14:17:49] Starting 'min:html'...
1>[14:17:49] Finished 'min:js' after 83 ms
1>[14:17:49] Finished 'min:css' after 88 ms
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

<span data-ttu-id="b2fb0-252">或者，Visual Studio 任务运行程序资源管理器可能用于将 Gulp 任务绑定到特定的 Visual Studio 事件。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-252">Alternatively, Visual Studio's Task Runner Explorer may be used to bind Gulp tasks to specific Visual Studio events.</span></span> <span data-ttu-id="b2fb0-253">请参阅[正在运行的默认任务](xref:client-side/using-gulp#running-default-tasks)有关执行此操作的说明。</span><span class="sxs-lookup"><span data-stu-id="b2fb0-253">See [Running default tasks](xref:client-side/using-gulp#running-default-tasks) for instructions on doing that.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2fb0-254">其他资源</span><span class="sxs-lookup"><span data-stu-id="b2fb0-254">Additional resources</span></span>

* [<span data-ttu-id="b2fb0-255">使用 Gulp</span><span class="sxs-lookup"><span data-stu-id="b2fb0-255">Use Gulp</span></span>](xref:client-side/using-gulp)
* [<span data-ttu-id="b2fb0-256">使用 Grunt</span><span class="sxs-lookup"><span data-stu-id="b2fb0-256">Use Grunt</span></span>](xref:client-side/using-grunt)
* [<span data-ttu-id="b2fb0-257">使用多个环境</span><span class="sxs-lookup"><span data-stu-id="b2fb0-257">Work with Multiple Environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="b2fb0-258">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="b2fb0-258">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
