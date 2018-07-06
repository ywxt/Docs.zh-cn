---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: 什么是 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能 |Microsoft Docs
author: rick-anderson
description: 本文档介绍新功能和增强功能 ASP.NET 4.5 中引入的。 它还介绍了用于 web 开发正在进行的改进...
ms.author: aspnetcontent
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: cfe9b1a7f05b43d5eb638c8fa7cb581d1edac9d5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835808"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="e3d47-104">什么是 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e3d47-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>
====================
> <span data-ttu-id="e3d47-105">本文档介绍新功能和增强功能 ASP.NET 4.5 中引入的。</span><span class="sxs-lookup"><span data-stu-id="e3d47-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="e3d47-106">它还介绍了 Visual Studio 2012 中针对 web 开发正在进行的改进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="e3d47-107">本文档最初在 2012 年 2 月 29 日发布。</span><span class="sxs-lookup"><span data-stu-id="e3d47-107">This document was originally published on February 29, 2012.</span></span>


- [<span data-ttu-id="e3d47-108">ASP.NET Core 运行时和框架</span><span class="sxs-lookup"><span data-stu-id="e3d47-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="e3d47-109">以异步方式读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="e3d47-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="e3d47-110">HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="e3d47-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="e3d47-111">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="e3d47-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="e3d47-112">为支持*await*并*任务*-基于异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="e3d47-113">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="e3d47-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="e3d47-114">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="e3d47-115">新的 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="e3d47-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="e3d47-116">延迟 （"延迟"） 请求验证</span><span class="sxs-lookup"><span data-stu-id="e3d47-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="e3d47-117">对未经过验证的请求的支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="e3d47-118">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="e3d47-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="e3d47-119">为 WebSockets 协议支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="e3d47-120">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="e3d47-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="e3d47-121">用于 Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="e3d47-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="e3d47-122">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="e3d47-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="e3d47-123">新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="e3d47-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="e3d47-124">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="e3d47-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="e3d47-125">使用多核 JIT 编译的启动速度更快</span><span class="sxs-lookup"><span data-stu-id="e3d47-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="e3d47-126">优化垃圾回收的内存优化</span><span class="sxs-lookup"><span data-stu-id="e3d47-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="e3d47-127">为 web 应用程序的预提取</span><span class="sxs-lookup"><span data-stu-id="e3d47-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="e3d47-128">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="e3d47-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="e3d47-129">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="e3d47-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="e3d47-130">模型绑定</span><span class="sxs-lookup"><span data-stu-id="e3d47-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="e3d47-131">选择数据</span><span class="sxs-lookup"><span data-stu-id="e3d47-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="e3d47-132">值提供程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="e3d47-133">来自控件的值筛选</span><span class="sxs-lookup"><span data-stu-id="e3d47-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="e3d47-134">HTML 编码的数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="e3d47-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="e3d47-135">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="e3d47-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="e3d47-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="e3d47-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="e3d47-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="e3d47-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="e3d47-138">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="e3d47-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="e3d47-139">Visual Studio 2012 候选发布版本</span><span class="sxs-lookup"><span data-stu-id="e3d47-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="e3d47-140">Visual Studio 2010 和 Visual Studio 2012 Release Candidate （项目兼容性） 之间共享的项目</span><span class="sxs-lookup"><span data-stu-id="e3d47-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="e3d47-141">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="e3d47-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="e3d47-142">在 IIS 7 ASP.NET 路由中的本机支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="e3d47-143">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="e3d47-144">智能任务</span><span class="sxs-lookup"><span data-stu-id="e3d47-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="e3d47-145">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="e3d47-146">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="e3d47-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="e3d47-147">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="e3d47-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="e3d47-148">适用于在特性中的代码片段 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="e3d47-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="e3d47-149">匹配的标记重命名开始或结束标记时自动重命名</span><span class="sxs-lookup"><span data-stu-id="e3d47-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="e3d47-150">生成事件处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="e3d47-151">智能缩进</span><span class="sxs-lookup"><span data-stu-id="e3d47-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="e3d47-152">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="e3d47-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="e3d47-153">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="e3d47-154">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="e3d47-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="e3d47-155">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="e3d47-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="e3d47-156">转到定义</span><span class="sxs-lookup"><span data-stu-id="e3d47-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="e3d47-157">ECMAScript5 的支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="e3d47-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="e3d47-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="e3d47-159">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="e3d47-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="e3d47-160">隐式引用</span><span class="sxs-lookup"><span data-stu-id="e3d47-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="e3d47-161">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="e3d47-162">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="e3d47-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="e3d47-163">分层缩进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="e3d47-164">CSS 攻击支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="e3d47-165">供应商特定的架构 (-moz-，-易于使用的功能)</span><span class="sxs-lookup"><span data-stu-id="e3d47-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="e3d47-166">注释和取消注释支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="e3d47-167">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="e3d47-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="e3d47-168">片段</span><span class="sxs-lookup"><span data-stu-id="e3d47-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="e3d47-169">自定义区域</span><span class="sxs-lookup"><span data-stu-id="e3d47-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="e3d47-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="e3d47-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="e3d47-171">发布</span><span class="sxs-lookup"><span data-stu-id="e3d47-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="e3d47-172">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="e3d47-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="e3d47-173">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="e3d47-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="e3d47-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="e3d47-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="e3d47-175">免责声明</span><span class="sxs-lookup"><span data-stu-id="e3d47-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="e3d47-176">ASP.NET Core 运行时和框架</span><span class="sxs-lookup"><span data-stu-id="e3d47-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="e3d47-177">以异步方式读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="e3d47-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="e3d47-178">ASP.NET 4 引入了读取为流使用的 HTTP 请求实体的功能*HttpRequest.GetBufferlessInputStream*方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="e3d47-179">此方法提供流式处理访问请求实体。</span><span class="sxs-lookup"><span data-stu-id="e3d47-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="e3d47-180">但是，它以同步方式执行，其中请求的持续时间内绑定到某个线程。</span><span class="sxs-lookup"><span data-stu-id="e3d47-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="e3d47-181">ASP.NET 4.5 支持读取以异步方式对 HTTP 请求实体，流的功能和能力以异步方式刷新。</span><span class="sxs-lookup"><span data-stu-id="e3d47-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="e3d47-182">ASP.NET 4.5 还提供了双缓冲 HTTP 请求实体，它提供更轻松地集成使用下游 HTTP 处理程序，例如.aspx 页处理程序和 ASP.NET MVC 控制器的功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="e3d47-183">HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="e3d47-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="e3d47-184">ASP.NET 4.5，从返回的 Stream 引用*HttpRequest.GetBufferlessInputStream*支持同步和异步读取的方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="e3d47-185">*Stream*从返回的对象*GetBufferlessInputStream*现在实现了 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="e3d47-186">异步*Stream*方法让你以异步方式读取请求实体的区块，而 ASP.NET 释放当前线程之间的异步读取循环每次迭代。</span><span class="sxs-lookup"><span data-stu-id="e3d47-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="e3d47-187">ASP.NET 4.5 还添加了用于缓冲的方式读取请求实体的配套方法： *HttpRequest.GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="e3d47-188">此新重载的工作方式类似于*GetBufferlessInputStream*，支持同步和异步读取。</span><span class="sxs-lookup"><span data-stu-id="e3d47-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="e3d47-189">但是，因为它读取*GetBufferedInputStream*还将实体字节复制到 ASP.NET 内部缓冲区，以便下游模块和处理程序仍然可以访问请求实体。</span><span class="sxs-lookup"><span data-stu-id="e3d47-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="e3d47-190">例如，如果某些上游管道中的代码已经读取请求实体使用*GetBufferedInputStream*，仍可以使用*HttpRequest.Form*或*HttpRequest.Files*.</span><span class="sxs-lookup"><span data-stu-id="e3d47-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="e3d47-191">这允许您执行异步处理请求 （例如，流式处理大型文件上的传到数据库），但仍运行的.aspx 页和 ASP.NET MVC 控制器之后。</span><span class="sxs-lookup"><span data-stu-id="e3d47-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="e3d47-192">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="e3d47-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="e3d47-193">发送到 HTTP 客户端的响应可能需要相当长的时间时客户端距离遥远，或具有低带宽连接。</span><span class="sxs-lookup"><span data-stu-id="e3d47-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="e3d47-194">通常情况下 ASP.NET 缓冲响应字节数，因为它们创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="e3d47-195">ASP.NET 然后执行一个发送操作的请求处理的最末尾应计缓冲区。</span><span class="sxs-lookup"><span data-stu-id="e3d47-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="e3d47-196">如果将缓冲的响应较大 （例如，流式传输到客户端的大型文件），则必须定期调用*HttpResponse.Flush*将缓冲的输出发送到客户端并保持受控制的内存使用情况。</span><span class="sxs-lookup"><span data-stu-id="e3d47-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="e3d47-197">但是，由于*刷新*是一个同步调用，以迭代方式调用*刷新*仍可能需要长时间运行请求的持续时间内使用一个线程。</span><span class="sxs-lookup"><span data-stu-id="e3d47-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="e3d47-198">ASP.NET 4.5 添加的使用以异步方式执行刷新的支持*BeginFlush*并*EndFlush*方法*HttpResponse*类。</span><span class="sxs-lookup"><span data-stu-id="e3d47-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="e3d47-199">使用这些方法，可以创建异步模块和异步处理程序以增量方式将数据发送到客户端而不必占用操作系统线程。</span><span class="sxs-lookup"><span data-stu-id="e3d47-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="e3d47-200">在中间*BeginFlush*并*EndFlush*调用，ASP.NET 释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="e3d47-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="e3d47-201">这极大地减少了为了支持长时间运行 HTTP 下载所需要的活动线程的总数。</span><span class="sxs-lookup"><span data-stu-id="e3d47-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="e3d47-202">为支持*await*并*任务*-基于异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="e3d47-203">.NET Framework 4 引入了异步编程概念，称为*任务*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="e3d47-204">任务由*任务*类型和中的相关的类型*System.Threading.Tasks*命名空间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="e3d47-205">使用编译器增强功能，请使用此生成.NET Framework 4.5*任务*简单的对象。</span><span class="sxs-lookup"><span data-stu-id="e3d47-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="e3d47-206">在.NET Framework 4.5 中，编译器都支持两个新关键字： *await*并*异步*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="e3d47-207">*Await*关键字是速记语法用于指示在某些其他代码段以异步方式等待一段代码。</span><span class="sxs-lookup"><span data-stu-id="e3d47-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="e3d47-208">*异步*关键字都表示一个提示，可用于将方法标记为基于任务的异步方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="e3d47-209">组合*await*，*异步*，并*任务*对象可大大简化了.NET 4.5 中编写异步代码。</span><span class="sxs-lookup"><span data-stu-id="e3d47-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="e3d47-210">ASP.NET 4.5 支持这些简化与新的 Api，允许你编写异步 HTTP 模块和异步 HTTP 处理程序使用新的编译器增强功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="e3d47-211">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="e3d47-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="e3d47-212">假设你想要执行异步工作中返回的方法*任务*对象。</span><span class="sxs-lookup"><span data-stu-id="e3d47-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="e3d47-213">下面的代码示例定义进行异步调用，若要下载 Microsoft 主页上的异步方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="e3d47-214">请注意，使用*异步*方法签名中的关键字和*await*调用*DownloadStringTaskAsync*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="e3d47-215">这就是你已将所有 —.NET Framework 将自动处理时等待下载完成，以及自动完成下载后将还原的调用堆栈展开调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="e3d47-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="e3d47-216">现在假设你想要在异步 ASP.NET HTTP 模块中使用此异步方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="e3d47-217">ASP.NET 4.5 包括一个帮助器方法 (*EventHandlerTaskAsyncHelper*) 和新的委托类型 (*TaskEventHandler*) 可用来集成有较旧的基于任务的异步方法公开的 ASP.NET HTTP 管道的异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="e3d47-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="e3d47-218">此示例演示如何：</span><span class="sxs-lookup"><span data-stu-id="e3d47-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="e3d47-219">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="e3d47-220">在 ASP.NET 中编写异步处理程序的传统方法是实现*IHttpAsyncHandler*接口。</span><span class="sxs-lookup"><span data-stu-id="e3d47-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="e3d47-221">ASP.NET 4.5 引入了*HttpTaskAsyncHandler*异步的基类型可以派生，这样，就更简单地编写异步处理程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="e3d47-222">*HttpTaskAsyncHandler*类型是抽象的要求你重写*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="e3d47-223">在内部 ASP.NET 负责集成返回签名的 (*任务*对象) 的*ProcessRequestAsync*与由 ASP.NET 管道中使用的较旧异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="e3d47-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="e3d47-224">下面的示例演示如何使用*任务*并*await*作为异步 HTTP 处理程序的实现的一部分：</span><span class="sxs-lookup"><span data-stu-id="e3d47-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="e3d47-225">新的 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="e3d47-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="e3d47-226">默认情况下，ASP.NET 将执行请求验证，它会检查请求以查找标记或脚本中的字段、 标头、 cookie 和等等。</span><span class="sxs-lookup"><span data-stu-id="e3d47-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="e3d47-227">如果任何检测到，ASP.NET 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="e3d47-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="e3d47-228">这相当于一系列第一个阻止潜在的跨站点脚本攻击的防御措施。</span><span class="sxs-lookup"><span data-stu-id="e3d47-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="e3d47-229">ASP.NET 4.5 轻松有选择地读取未经验证的请求数据。</span><span class="sxs-lookup"><span data-stu-id="e3d47-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="e3d47-230">ASP.NET 4.5 还集成了常用的 AntiXSS 库之前为外部库。</span><span class="sxs-lookup"><span data-stu-id="e3d47-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="e3d47-231">开发人员已经常要求能够有选择性地关闭对其应用程序的请求验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="e3d47-232">例如，如果你的应用程序论坛软件，您可能想要允许用户提交 HTML 格式的论坛帖子和提出的意见，但仍确保请求验证检查其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="e3d47-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="e3d47-233">ASP.NET 4.5 引入了两项功能，可以轻松可以有选择地使用未经验证的输入： 延迟 （"延迟"） 请求验证和未经验证的请求数据访问权限。</span><span class="sxs-lookup"><span data-stu-id="e3d47-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="e3d47-234">延迟 （"延迟"） 请求验证</span><span class="sxs-lookup"><span data-stu-id="e3d47-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="e3d47-235">在 ASP.NET 4.5 中，默认情况下所有请求数据都都需要进行请求验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="e3d47-236">但是，可以配置应用程序，以便将延迟实际访问请求数据请求验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="e3d47-237">（这有时称为延迟请求验证，基于的术语，例如延迟加载某些数据方案。）可以配置应用程序的 Web.config 文件中使用推迟的验证，通过设置*requestValidationMode*属性中的 4.5 *httpRUntime*元素，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="e3d47-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="e3d47-238">在请求验证模式设置为 4.5，仅针对特定请求值且仅当你的代码访问该值，会触发请求验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="e3d47-239">例如，如果你的代码获取的值的 Request.Form["forum\_发布"]，仅针对窗体集合中该元素调用请求验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="e3d47-240">无中的其他元素*窗体*集合进行验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="e3d47-241">在以前版本的 ASP.NET 中，请求验证已访问集合中的任何元素时找不到整个请求触发。</span><span class="sxs-lookup"><span data-stu-id="e3d47-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="e3d47-242">新行为轻松查看请求数据的不同部分而不会触发请求验证的其他部分不同的应用程序组件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="e3d47-243">对未经过验证的请求的支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-243">Support for unvalidated requests</span></span>

<span data-ttu-id="e3d47-244">延迟的请求验证就不能解决有选择地绕过请求验证的问题。</span><span class="sxs-lookup"><span data-stu-id="e3d47-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="e3d47-245">调用 Request.Form["forum\_发布"] 仍触发器的请求验证该特定请求值。</span><span class="sxs-lookup"><span data-stu-id="e3d47-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="e3d47-246">但是，你可能想要访问此字段不触发验证，因为你想要允许该字段中的标记。</span><span class="sxs-lookup"><span data-stu-id="e3d47-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="e3d47-247">若要允许此操作，ASP.NET 4.5 现在支持对请求数据未经过验证的访问。</span><span class="sxs-lookup"><span data-stu-id="e3d47-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="e3d47-248">ASP.NET 4.5 包括一个新*Unvalidated*集合属性中的*HttpRequest*类。</span><span class="sxs-lookup"><span data-stu-id="e3d47-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="e3d47-249">此集合提供对所有请求数据的常见值访问类似*窗体*， *QueryString*， *Cookie*，以及*Url*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="e3d47-250">使用论坛的示例中，若要能够读取未经验证的请求数据，首先需要配置应用程序以使用新的请求验证模式：</span><span class="sxs-lookup"><span data-stu-id="e3d47-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="e3d47-251">然后，可以使用*HttpRequest.Unvalidated*读取未经验证的表单值的属性：</span><span class="sxs-lookup"><span data-stu-id="e3d47-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> <span data-ttu-id="e3d47-252">安全性-*谨慎使用未经验证的请求数据 ！*</span><span class="sxs-lookup"><span data-stu-id="e3d47-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="e3d47-253">添加 ASP.NET 4.5 中的未经验证的请求属性和集合以使你更轻松地访问非常具体未经验证的请求数据。</span><span class="sxs-lookup"><span data-stu-id="e3d47-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="e3d47-254">但是，仍必须在原始请求数据，以确保不向用户呈现危险的文本上执行自定义验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="e3d47-255">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="e3d47-255">AntiXSS Library</span></span>

<span data-ttu-id="e3d47-256">由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在结合了核心编码例程与库的版本 4.0。</span><span class="sxs-lookup"><span data-stu-id="e3d47-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="e3d47-257">由实现编码例程*AntiXssEncoder*中的新类型*System.Web.Security.AntiXss*命名空间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="e3d47-258">可以使用*AntiXssEncoder*直接通过调用的任何静态类型中实现的编码方法的类型。</span><span class="sxs-lookup"><span data-stu-id="e3d47-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="e3d47-259">但是，使用新的防 XSS 例程的最简单方法是配置 ASP.NET 应用程序中使用*AntiXssEncoder*默认情况下的类。</span><span class="sxs-lookup"><span data-stu-id="e3d47-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="e3d47-260">若要执行此操作，请将以下属性添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="e3d47-261">当*encoderType*属性设置为使用*AntiXssEncoder*类型，所有输出自动编码在 ASP.NET 中使用新的编码例程。</span><span class="sxs-lookup"><span data-stu-id="e3d47-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="e3d47-262">这些是已合并到 ASP.NET 4.5 中的外部 AntiXSS 库部分：</span><span class="sxs-lookup"><span data-stu-id="e3d47-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="e3d47-263">*HtmlEncode*， *HtmlFormUrlEncode*，和*HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="e3d47-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="e3d47-264">*XmlAttributeEncode*和*XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="e3d47-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="e3d47-265">*UrlEncode*并*UrlPathEncode* （新）</span><span class="sxs-lookup"><span data-stu-id="e3d47-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="e3d47-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="e3d47-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="e3d47-267">为 WebSockets 协议支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="e3d47-268">Websocket 协议是一种基于标准的网络协议，用于定义如何建立基于 HTTP 的客户端和服务器之间的安全、 实时的双向通信。</span><span class="sxs-lookup"><span data-stu-id="e3d47-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="e3d47-269">Microsoft 已经与 IETF 和 W3C 标准主体，以帮助定义的协议。</span><span class="sxs-lookup"><span data-stu-id="e3d47-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="e3d47-270">Websocket 协议被支持任何客户端 （而不仅仅是浏览器），与 Microsoft 投资 WebSockets 协议支持客户端和移动操作系统上的大量资源。</span><span class="sxs-lookup"><span data-stu-id="e3d47-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="e3d47-271">Websocket 协议进行创建客户端和服务器之间的长时间运行的数据传输容易得多。</span><span class="sxs-lookup"><span data-stu-id="e3d47-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="e3d47-272">例如，编写的聊天应用程序是更容易的因为您可以建立客户端和服务器之间，则返回 true 的长时间运行连接。</span><span class="sxs-lookup"><span data-stu-id="e3d47-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="e3d47-273">不需要求助于如定期轮询或 HTTP 长轮询模拟套接字的行为的解决方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="e3d47-274">ASP.NET 4.5 和 IIS 8 包括低级别的 Websocket 支持，使 ASP.NET 开发人员能够使用托管的 Api，用于以异步方式读取和写入 Websocket 对象上的字符串和二进制数据。</span><span class="sxs-lookup"><span data-stu-id="e3d47-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="e3d47-275">为 ASP.NET 4.5 新增了一个*System.Web.WebSockets*包含用于使用 WebSockets 协议的类型的命名空间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="e3d47-276">浏览器客户端会建立 Websocket 连接，通过创建 DOM *WebSocket*中 ASP.NET 应用程序，如以下示例所示的 URL 所指向的对象：</span><span class="sxs-lookup"><span data-stu-id="e3d47-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="e3d47-277">可以在 ASP.NET 中使用任何类型的模块或处理程序创建 Websocket 终结点。</span><span class="sxs-lookup"><span data-stu-id="e3d47-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="e3d47-278">在上一示例中，使用.ashx 文件，因为.ashx 文件创建一个处理程序的快速方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="e3d47-279">根据 Websocket 协议，ASP.NET 应用程序接受客户端的 Websocket 请求通过指示请求应从 HTTP GET 请求升级到 Websocket 请求。</span><span class="sxs-lookup"><span data-stu-id="e3d47-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="e3d47-280">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="e3d47-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="e3d47-281">*AcceptWebSocketRequest*方法接受一个函数委托，因为 ASP.NET 展开当前 HTTP 请求，然后将控制权转交给函数委托。</span><span class="sxs-lookup"><span data-stu-id="e3d47-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="e3d47-282">从概念上讲这种方法是类似于你如何使用*System.Threading.Thread*，其中定义在后台中执行工作的线程启动委托。</span><span class="sxs-lookup"><span data-stu-id="e3d47-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="e3d47-283">ASP.NET 和客户端已成功完成 Websocket 握手后，ASP.NET 将调用您的代理和 Websocket 应用程序开始运行。</span><span class="sxs-lookup"><span data-stu-id="e3d47-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="e3d47-284">下面的代码示例显示了在 ASP.NET 中使用内置的 Websocket 支持的简单的回显应用程序：</span><span class="sxs-lookup"><span data-stu-id="e3d47-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="e3d47-285">在.NET 4.5 中的支持*await*关键字和基于任务的异步操作是生就很适合编写 Websocket 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="e3d47-286">代码示例演示在 ASP.NET 内完全以异步方式运行的 Websocket 请求。</span><span class="sxs-lookup"><span data-stu-id="e3d47-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="e3d47-287">应用程序以异步方式等待通过调用从客户端发送一条消息*await 套接字。ReceiveAsync*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="e3d47-288">同样，您可以将异步消息给客户端通过调用*await 套接字。SendAsync*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="e3d47-289">在浏览器应用程序接收通过 Websocket 消息*onmessage*函数。</span><span class="sxs-lookup"><span data-stu-id="e3d47-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="e3d47-290">若要从浏览器发送一条消息，请调用*发送*方法*WebSocket* DOM 类型，在此示例中所示：</span><span class="sxs-lookup"><span data-stu-id="e3d47-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="e3d47-291">将来，我们可能会发布此功能，抽象消失的低级别的编码，它一些需要在此版本中用于 Websocket 的应用程序的更新。</span><span class="sxs-lookup"><span data-stu-id="e3d47-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="e3d47-292">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="e3d47-292">Bundling and Minification</span></span>

<span data-ttu-id="e3d47-293">绑定可以将各个 JavaScript 和 CSS 文件合并到一个包，可以被视为单个文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="e3d47-294">缩小会 JavaScript 和 CSS 文件将通过删除空白并不是必需的其他字符。</span><span class="sxs-lookup"><span data-stu-id="e3d47-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="e3d47-295">这些功能适用于 Web 窗体、 ASP.NET MVC 和 Web Pages。</span><span class="sxs-lookup"><span data-stu-id="e3d47-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="e3d47-296">使用 Bundle 类或其子类别，ScriptBundle 和 StyleBundle 创建捆绑包。</span><span class="sxs-lookup"><span data-stu-id="e3d47-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="e3d47-297">在配置的绑定实例之后, 捆绑包可对传入的请求只需将其添加到全局 BundleCollection 实例。</span><span class="sxs-lookup"><span data-stu-id="e3d47-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="e3d47-298">默认模板中的绑定配置执行 BundleConfig 文件中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="e3d47-299">这种默认配置创建的所有核心脚本和模板使用的 css 文件的捆绑包。</span><span class="sxs-lookup"><span data-stu-id="e3d47-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="e3d47-300">捆绑包将引用从在视图内使用几个可能的帮助器方法之一。</span><span class="sxs-lookup"><span data-stu-id="e3d47-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="e3d47-301">为了支持呈现不同的标记，在发布模式下与调试时绑定，ScriptBundle 和 StyleBundle 类必须呈现的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="e3d47-302">如果处于调试模式，呈现器将生成捆绑中的每个资源的标记。</span><span class="sxs-lookup"><span data-stu-id="e3d47-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="e3d47-303">在发布模式下，当呈现器将生成整个绑定的单个标记元素。</span><span class="sxs-lookup"><span data-stu-id="e3d47-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="e3d47-304">切换调试和发布之间，可以通过修改 web.config 中的元素的调试属性，如下所示实现模式：</span><span class="sxs-lookup"><span data-stu-id="e3d47-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="e3d47-305">此外，可以直接通过 BundleTable.EnableOptimizations 属性设置启用或禁用优化。</span><span class="sxs-lookup"><span data-stu-id="e3d47-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="e3d47-306">绑定文件，则将首先排序按字母顺序 (中所显示的方式**解决方案资源管理器**)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="e3d47-307">它们然后的组织方式，以便知道库以及其自定义扩展插件 （如 jQuery、 MooTools 和 Dojo） 首次加载。</span><span class="sxs-lookup"><span data-stu-id="e3d47-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="e3d47-308">例如，将为绑定脚本文件夹中，如上面所示的最终顺序：</span><span class="sxs-lookup"><span data-stu-id="e3d47-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="e3d47-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="e3d47-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="e3d47-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="e3d47-310">jquery-ui.js</span></span>
3. <span data-ttu-id="e3d47-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="e3d47-311">jquery.tools.js</span></span>
4. <span data-ttu-id="e3d47-312">a.js</span><span class="sxs-lookup"><span data-stu-id="e3d47-312">a.js</span></span>

<span data-ttu-id="e3d47-313">CSS 文件是按字母顺序排序，然后重新组织，以便 reset.css 和要优先于 normalize.css 出现之前的任何其他文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="e3d47-314">绑定 Styles 文件夹如上所示的最终排序将为此：</span><span class="sxs-lookup"><span data-stu-id="e3d47-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="e3d47-315">reset.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-315">reset.css</span></span>
2. <span data-ttu-id="e3d47-316">content.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-316">content.css</span></span>
3. <span data-ttu-id="e3d47-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-317">forms.css</span></span>
4. <span data-ttu-id="e3d47-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-318">globals.css</span></span>
5. <span data-ttu-id="e3d47-319">menu.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-319">menu.css</span></span>
6. <span data-ttu-id="e3d47-320">styles.css</span><span class="sxs-lookup"><span data-stu-id="e3d47-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="e3d47-321">用于 Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="e3d47-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="e3d47-322">.NET Framework 4.5 和 Windows 8 引入了功能，可帮助您实现显著的性能提升为 web 服务器工作负荷。</span><span class="sxs-lookup"><span data-stu-id="e3d47-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="e3d47-323">这包括减少 （最多 35%) 在这两个启动时间和中的内存占用量 web 宿主使用 ASP.NET 的网站。</span><span class="sxs-lookup"><span data-stu-id="e3d47-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="e3d47-324">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="e3d47-324">Key performance factors</span></span>

<span data-ttu-id="e3d47-325">理想情况下，所有网站应都处于活动状态，并且在内存中以确保快速响应的下一个请求，只要涉及。</span><span class="sxs-lookup"><span data-stu-id="e3d47-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="e3d47-326">可能会影响网站响应能力的因素包括：</span><span class="sxs-lookup"><span data-stu-id="e3d47-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="e3d47-327">为站点的应用池回收后重新启动花费的时间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="e3d47-328">这是网站程序集将不再在内存中时启动该站点在 web 服务器进程所需的时间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="e3d47-329">（平台程序集是仍在内存中，因为它们由其他站点。）这种情况下被称为"冷站点，热 framework 启动"或只是"冷站点启动。"</span><span class="sxs-lookup"><span data-stu-id="e3d47-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="e3d47-330">站点占用的内存量。</span><span class="sxs-lookup"><span data-stu-id="e3d47-330">How much memory the site occupies.</span></span> <span data-ttu-id="e3d47-331">此术语是"每个站点的内存使用情况"取消共享工作集。"</span><span class="sxs-lookup"><span data-stu-id="e3d47-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="e3d47-332">新的性能改进重点介绍这两种因素。</span><span class="sxs-lookup"><span data-stu-id="e3d47-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="e3d47-333">新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="e3d47-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="e3d47-334">新功能的要求可以分为以下类别：</span><span class="sxs-lookup"><span data-stu-id="e3d47-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="e3d47-335">在.NET Framework 4 运行的改进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="e3d47-336">需要.NET Framework 4.5，但可以在任何版本的 Windows 上运行的改进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="e3d47-337">可仅与 Windows 8 上运行的.NET Framework 4.5 的改进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="e3d47-338">性能会增加与改进，可以启用每个级别。</span><span class="sxs-lookup"><span data-stu-id="e3d47-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="e3d47-339">某些.NET Framework 4.5 改进充分利用更广泛应用于其他方案的性能功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="e3d47-340">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="e3d47-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="e3d47-341">**要求**:.NET Framework 4 和 Visual Studio 11 开发者预览版 SDK</span><span class="sxs-lookup"><span data-stu-id="e3d47-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="e3d47-342">在服务器上的不同站点通常使用同一个帮助程序程序集 （例如，从初学者工具包或示例应用程序的程序集）。</span><span class="sxs-lookup"><span data-stu-id="e3d47-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="e3d47-343">每个站点及其 Bin 目录中有其自己的这些程序集副本。</span><span class="sxs-lookup"><span data-stu-id="e3d47-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="e3d47-344">即使对象代码的程序集是相同的它们是物理上独立的程序集，以便每个程序集必须在冷站点启动期间单独读取和单独保留在内存中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="e3d47-345">新 interning 功能解决了这种低效情况并减少内存需求和负载时间。</span><span class="sxs-lookup"><span data-stu-id="e3d47-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="e3d47-346">暂留可让 Windows 在文件系统中，保留每个程序集的单个副本和站点的 Bin 文件夹中的单个程序集将替换单个副本的符号链接。</span><span class="sxs-lookup"><span data-stu-id="e3d47-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="e3d47-347">如果单个站点需要不同版本的程序集，符号链接替换为新版本的程序集，并仅该站点受到影响。</span><span class="sxs-lookup"><span data-stu-id="e3d47-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="e3d47-348">共享使用符号链接的程序集需要名为 aspnet 的新工具\_intern.exe，可以创建和管理的存储中暂留的程序集。</span><span class="sxs-lookup"><span data-stu-id="e3d47-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="e3d47-349">它作为 Visual Studio 11 开发人员预览版 SDK 的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="e3d47-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="e3d47-350">(但是，它将在仅安装.NET Framework 4，如果你已安装最新的系统上运行[更新](https://support.microsoft.com/kb/2468871)。)</span><span class="sxs-lookup"><span data-stu-id="e3d47-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="e3d47-351">若要确保所有符合条件的程序集具有暂留，请运行 aspnet\_intern.exe 定期 （例如，每周一次作为计划任务）。</span><span class="sxs-lookup"><span data-stu-id="e3d47-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="e3d47-352">一种典型用法如下所示：</span><span class="sxs-lookup"><span data-stu-id="e3d47-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="e3d47-353">若要查看所有选项，请不带任何参数运行该工具。</span><span class="sxs-lookup"><span data-stu-id="e3d47-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="e3d47-354">使用多核 JIT 编译的启动速度更快</span><span class="sxs-lookup"><span data-stu-id="e3d47-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="e3d47-355">**要求**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e3d47-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="e3d47-356">对于冷站点启动时，不仅执行程序集必须从磁盘中读取，但站点必须是 JIT 编译。</span><span class="sxs-lookup"><span data-stu-id="e3d47-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="e3d47-357">对于复杂的站点，这可以添加严重的延迟。</span><span class="sxs-lookup"><span data-stu-id="e3d47-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="e3d47-358">.NET Framework 4.5 中新的通用方法通过 JIT 编译分散到可用处理器核数降低这些延迟。</span><span class="sxs-lookup"><span data-stu-id="e3d47-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="e3d47-359">做到这一点的尽可能多，并尽早使用期间收集的信息之前启动的站点。</span><span class="sxs-lookup"><span data-stu-id="e3d47-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="e3d47-360">此功能由实现[System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="e3d47-361">因此不需要执行任何操作来利用此功能，使用多核 JIT 编译是在 ASP.NET 中，默认情况下启用。</span><span class="sxs-lookup"><span data-stu-id="e3d47-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="e3d47-362">如果你想要禁用此功能，请在 Web.config 文件中进行以下设置：</span><span class="sxs-lookup"><span data-stu-id="e3d47-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="e3d47-363">优化垃圾回收的内存优化</span><span class="sxs-lookup"><span data-stu-id="e3d47-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="e3d47-364">**要求**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e3d47-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="e3d47-365">站点运行后，其使用的垃圾回收器 (GC) 堆可以导致其内存使用量的重要因素。</span><span class="sxs-lookup"><span data-stu-id="e3d47-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="e3d47-366">任何垃圾回收器，如.NET Framework GC 使 CPU 时间 （频率和重要性的集合） 和内存消耗 （用于新的、 已释放，或可释放的对象的额外空间） 方面做出权衡。</span><span class="sxs-lookup"><span data-stu-id="e3d47-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="e3d47-367">针对早期版本中，我们提供了指导如何配置之间取得最佳平衡，GC (有关示例，请参阅[ASP.NET 2.0/3.5 共享托管配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。</span><span class="sxs-lookup"><span data-stu-id="e3d47-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="e3d47-368">.NET Framework 4.5 中，而不是多个独立设置，工作负荷定义的配置设置是可用的启用的所有以前建议的 GC 设置，以及新的优化，可提供有关每个站点的其他性能工作集。</span><span class="sxs-lookup"><span data-stu-id="e3d47-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="e3d47-369">若要启用优化的 GC 内存，请将以下设置添加到 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 文件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="e3d47-370">(如果您熟悉到 aspnet.config 更改前面的指导，请注意，此设置将替代旧设置 — 例如，没有必要设置 gcServer、 gcConcurrent，等等。您无需删除旧设置。）</span><span class="sxs-lookup"><span data-stu-id="e3d47-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="e3d47-371">为 web 应用程序的预提取</span><span class="sxs-lookup"><span data-stu-id="e3d47-371">Prefetching for web applications</span></span>

<span data-ttu-id="e3d47-372">**要求**: Windows 8 上运行的.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e3d47-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="e3d47-373">Windows 具有几个版本包含一种技术称为[取](http://en.wikipedia.org/wiki/Prefetcher)这样做可以减小应用程序启动的磁盘读取成本。</span><span class="sxs-lookup"><span data-stu-id="e3d47-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="e3d47-374">由于冷启动是主要的客户端应用程序问题，这一技术尚未包含在 Windows Server 中，其中包含对 server 至关重要的组件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="e3d47-375">预提取现已推出 Windows Server，它可以在其中优化单独的网站的发布的最新版本。</span><span class="sxs-lookup"><span data-stu-id="e3d47-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="e3d47-376">适用于 Windows Server 在默认情况下不启用取。</span><span class="sxs-lookup"><span data-stu-id="e3d47-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="e3d47-377">若要启用和配置用于高密度 web 托管取，请在命令行运行以下命令集：</span><span class="sxs-lookup"><span data-stu-id="e3d47-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="e3d47-378">然后，与 ASP.NET 应用程序集成取，以下代码添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="e3d47-379">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="e3d47-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="e3d47-380">强类型化的数据控件</span><span class="sxs-lookup"><span data-stu-id="e3d47-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="e3d47-381">在 ASP.NET 4.5 Web 窗体包含用于处理数据的一些改进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="e3d47-382">第一个改进是强类型化的数据控件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="e3d47-383">对于在以前版本的 ASP.NET Web 窗体控件，显示数据绑定值使用*Eval*和数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="e3d47-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="e3d47-384">使用双向数据绑定*绑定*:</span><span class="sxs-lookup"><span data-stu-id="e3d47-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="e3d47-385">在运行时，这些调用使用反射来读取指定的成员的值，然后在标记中显示的结果。</span><span class="sxs-lookup"><span data-stu-id="e3d47-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="e3d47-386">这种方法可以轻松将针对任意、 unshaped 数据的数据绑定。</span><span class="sxs-lookup"><span data-stu-id="e3d47-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="e3d47-387">但是，此类数据绑定表达式不为成员名称、 导航 （例如，请转到定义） 或编译时检查这些名称支持 IntelliSense 等功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="e3d47-388">若要解决此问题，ASP.NET 4.5，请添加了声明将控件绑定到的数据的数据类型的功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="e3d47-389">执行此操作使用新*ItemType*属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="e3d47-390">当设置此属性时，两个新的类型化的变量中的数据绑定表达式作用域有：*项*并*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="e3d47-391">由于强类型化变量，可以获得完整的 Visual Studio 开发体验。</span><span class="sxs-lookup"><span data-stu-id="e3d47-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>


<span data-ttu-id="e3d47-392">对于双向数据绑定表达式，使用*BindItem*变量：</span><span class="sxs-lookup"><span data-stu-id="e3d47-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


<span data-ttu-id="e3d47-393">支持数据绑定的 ASP.NET Web 窗体框架中的大多数控件已更新，以支持*ItemType*属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="e3d47-394">模型绑定</span><span class="sxs-lookup"><span data-stu-id="e3d47-394">Model Binding</span></span>

<span data-ttu-id="e3d47-395">模型绑定扩展了 ASP.NET Web 窗体控件中的数据绑定来处理的代码为中心的数据访问。</span><span class="sxs-lookup"><span data-stu-id="e3d47-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="e3d47-396">它包含从概念*ObjectDataSource*控件和从 ASP.NET MVC 中的模型绑定。</span><span class="sxs-lookup"><span data-stu-id="e3d47-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="e3d47-397">选择数据</span><span class="sxs-lookup"><span data-stu-id="e3d47-397">Selecting data</span></span>

<span data-ttu-id="e3d47-398">若要配置以使用模型绑定选择数据的数据控件，设置控件的*SelectMethod*属性设置为在页面的代码中方法的名称。</span><span class="sxs-lookup"><span data-stu-id="e3d47-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="e3d47-399">数据控件在页生命周期中的适当时间调用的方法，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="e3d47-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="e3d47-400">无需显式调用*DataBind*方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="e3d47-401">在以下示例中， *GridView*控件配置为使用一个名为方法*GetCategories*:</span><span class="sxs-lookup"><span data-stu-id="e3d47-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="e3d47-402">您创建*GetCategories*页面的代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="e3d47-403">对于简单的选择操作，该方法不需要参数，且应返回*IEnumerable*或*IQueryable*对象。</span><span class="sxs-lookup"><span data-stu-id="e3d47-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="e3d47-404">如果新*ItemType*属性设置 (它使强类型化数据绑定表达式，如下面所述[强类型数据控件](#_Toc318097386)之前)，这些接口的泛型版本应返回 — *IEnumerable&lt;T&gt;* 或*IQueryable&lt;T&gt;*，与*T*参数类型相匹配*ItemType*属性 (例如， *IQueryable&lt;类别&gt;*)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="e3d47-405">下面的示例演示的代码*GetCategories*方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="e3d47-406">此示例使用 Northwind 示例数据库中使用 Entity Framework Code First 模型。</span><span class="sxs-lookup"><span data-stu-id="e3d47-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="e3d47-407">代码可确保查询将返回方式由的每个类别的相关产品的详细信息*Include*方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="e3d47-408">(这可确保*TemplateField*标记中的元素而无需在每个类别中显示的产品计数[n + 1 选择](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)。)</span><span class="sxs-lookup"><span data-stu-id="e3d47-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="e3d47-409">当该页运行时，则*GridView*控制调用*GetCategories*方法自动呈现返回使用已配置的字段的数据：</span><span class="sxs-lookup"><span data-stu-id="e3d47-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="e3d47-410">由于选择的方法会返回*IQueryable*对象， *GridView*控件可以进一步执行前操作查询。</span><span class="sxs-lookup"><span data-stu-id="e3d47-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="e3d47-411">例如， *GridView*控件可以添加用于排序和分页到返回的查询表达式*IQueryable*对象之前执行，以便这些操作均由基础LINQ 提供程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="e3d47-412">在这种情况下，实体框架将确保在数据库中执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="e3d47-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="e3d47-413">下面的示例演示*GridView*控件修改，以便允许排序和分页：</span><span class="sxs-lookup"><span data-stu-id="e3d47-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="e3d47-414">现在页运行时，该控件可确保显示数据的当前页并按所选列进行排序：</span><span class="sxs-lookup"><span data-stu-id="e3d47-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="e3d47-415">若要筛选返回的数据，需要添加到 select 方法参数。</span><span class="sxs-lookup"><span data-stu-id="e3d47-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="e3d47-416">这些参数将包含在运行时，模型绑定和可用于返回数据之前更改查询。</span><span class="sxs-lookup"><span data-stu-id="e3d47-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="e3d47-417">例如，假设你想要让用户筛选器产品，通过在查询字符串中输入一个关键字。</span><span class="sxs-lookup"><span data-stu-id="e3d47-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="e3d47-418">可以将参数添加到方法，并更新代码以使用参数值：</span><span class="sxs-lookup"><span data-stu-id="e3d47-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="e3d47-419">此代码包括*其中*表达式，如果提供的值*关键字*然后返回查询结果。</span><span class="sxs-lookup"><span data-stu-id="e3d47-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="e3d47-420">值提供程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-420">Value providers</span></span>

<span data-ttu-id="e3d47-421">前面的示例不是特定的位置的值*关键字*参数来自。</span><span class="sxs-lookup"><span data-stu-id="e3d47-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="e3d47-422">若要指示此信息，可以使用参数属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="e3d47-423">对于此示例中，可以使用*QueryStringAttribute*中的类*System.Web.ModelBinding*命名空间：</span><span class="sxs-lookup"><span data-stu-id="e3d47-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="e3d47-424">这会指示要尝试将值绑定到查询字符串中的模型绑定*关键字*在运行时参数。</span><span class="sxs-lookup"><span data-stu-id="e3d47-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="e3d47-425">（这可能涉及执行类型转换，尽管它不会在这种情况下。）如果不能提供一个值，并且该类型是不可以为 null，则将引发异常。</span><span class="sxs-lookup"><span data-stu-id="e3d47-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="e3d47-426">指示要使用的值提供程序的参数属性统称为值提供程序属性和作为值提供程序，这些方法的值的源引用的。</span><span class="sxs-lookup"><span data-stu-id="e3d47-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="e3d47-427">Web 窗体将包括在 Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态，会话状态和配置文件属性值提供程序和所有典型的资源，用户输入的相应属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="e3d47-428">此外可以编写自定义值提供程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-428">You can also write custom value providers.</span></span>

<span data-ttu-id="e3d47-429">默认情况下，参数名称用于作为键的值提供程序集合中查找一个值。</span><span class="sxs-lookup"><span data-stu-id="e3d47-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="e3d47-430">在示例中，代码将查找名为关键字的查询字符串值 (例如，~ / default.aspx?keyword=chef)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="e3d47-431">可以通过将它作为参数传递给参数特性来指定自定义密钥。</span><span class="sxs-lookup"><span data-stu-id="e3d47-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="e3d47-432">例如，若要使用名为 q 的查询字符串变量的值，无法执行此操作：</span><span class="sxs-lookup"><span data-stu-id="e3d47-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="e3d47-433">如果此方法是在页面的代码中，用户可以通过使用查询字符串的关键字筛选结果：</span><span class="sxs-lookup"><span data-stu-id="e3d47-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="e3d47-434">模型绑定可实现许多任务，否则必须手动编写的代码： 读取的值、 检查 null 值、 尝试将其转换为适当的类型、 检查转换是否成功，和最后，使用中的值查询。</span><span class="sxs-lookup"><span data-stu-id="e3d47-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="e3d47-435">模型绑定结果，很少的代码在和中能够重复使用在整个应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="e3d47-436">来自控件的值筛选</span><span class="sxs-lookup"><span data-stu-id="e3d47-436">Filtering by values from a control</span></span>

<span data-ttu-id="e3d47-437">假设你想要扩展的示例，以便用户可以从下拉列表中选择筛选器值。</span><span class="sxs-lookup"><span data-stu-id="e3d47-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="e3d47-438">向标记添加下面的下拉列表并将其配置为从另一个方法使用获取数据*SelectMethod*属性：</span><span class="sxs-lookup"><span data-stu-id="e3d47-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="e3d47-439">通常还会添加*要*元素*GridView*控件，以便控件将显示一条消息，如果找不到任何匹配的产品：</span><span class="sxs-lookup"><span data-stu-id="e3d47-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="e3d47-440">在页代码中，将添加新的选择下拉列表的方法：</span><span class="sxs-lookup"><span data-stu-id="e3d47-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="e3d47-441">最后，更新*GetProducts*选择要包含下拉列表从所选类别的 ID 的新参数：</span><span class="sxs-lookup"><span data-stu-id="e3d47-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="e3d47-442">现在页运行时，用户可以从下拉列表中，选择某个类别并*GridView*控件是否自动显示经过筛选的数据重新绑定。</span><span class="sxs-lookup"><span data-stu-id="e3d47-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="e3d47-443">这可能是因为模型绑定跟踪选择方法的参数的值，并检测到在回发后是否已更改的任何参数值。</span><span class="sxs-lookup"><span data-stu-id="e3d47-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="e3d47-444">如果是这样，模型绑定将强制关联的数据控件重新绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="e3d47-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="e3d47-445">HTML 编码的数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="e3d47-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="e3d47-446">你可以立即进行 HTML 编码数据绑定表达式的结果。</span><span class="sxs-lookup"><span data-stu-id="e3d47-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="e3d47-447">将冒号 （:） 添加到末尾&lt;%# 前缀将标记数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="e3d47-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="e3d47-448">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="e3d47-448">Unobtrusive Validation</span></span>

<span data-ttu-id="e3d47-449">现在可以配置的内置验证程序控件可以将非介入式 JavaScript 用于客户端验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="e3d47-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="e3d47-450">这大大减少了呈现页面标记中的内联 JavaScript 并减少整体的页面大小。</span><span class="sxs-lookup"><span data-stu-id="e3d47-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="e3d47-451">可以按照以下任意方式来配置非介入式 JavaScript 验证程序控件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="e3d47-452">添加以下设置，从而全局*&lt;appSettings&gt;* Web.config 文件中的元素：</span><span class="sxs-lookup"><span data-stu-id="e3d47-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="e3d47-453">通过设置静态全局*System.Web.UI.ValidationSettings.UnobtrusiveValidationMode*属性设置为*UnobtrusiveValidationMode.WebForms* (通常是在*应用程序\_启动*Global.asax 文件中的方法)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="e3d47-454">通过设置新页为单独*UnobtrusiveValidationMode*的属性*页面*类来*UnobtrusiveValidationMode.WebForms*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="e3d47-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="e3d47-455">HTML5 Updates</span></span>

<span data-ttu-id="e3d47-456">某些已得到改进 Web 窗体服务器控件能够充分利用 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="e3d47-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="e3d47-457">*TextMode*的属性*文本框*控件已更新以支持新的 HTML5 输入的类型等*电子邮件*， *datetime*，和等等。</span><span class="sxs-lookup"><span data-stu-id="e3d47-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="e3d47-458">*FileUpload*控件现在支持多个文件上传从支持此 HTML5 功能的浏览器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="e3d47-459">验证程序控件现在支持验证 HTML5 输入的元素。</span><span class="sxs-lookup"><span data-stu-id="e3d47-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="e3d47-460">了现在表示 URL 的属性的新 HTML5 元素支持 runat ="server"。</span><span class="sxs-lookup"><span data-stu-id="e3d47-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="e3d47-461">因此，您可以使用 ASP.NET 约定中 URL 路径，如 ~ 运算符来表示应用程序根目录 (例如，&lt;视频 runat ="server"src="~/myVideo.wmv"/&gt;)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="e3d47-462">*UpdatePanel*控件已修复，以便支持发布 HTML5 输入的字段。</span><span class="sxs-lookup"><span data-stu-id="e3d47-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="e3d47-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="e3d47-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="e3d47-464">ASP.NET MVC 4 beta 版现已随附 Visual Studio 11 Beta。</span><span class="sxs-lookup"><span data-stu-id="e3d47-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="e3d47-465">ASP.NET MVC 是一个框架，用于通过利用模型-视图-控制器 (MVC) 模式开发高度可测试性和可维护 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="e3d47-466">ASP.NET MVC 4 轻松地为移动 Web 构建应用程序，并包含 ASP.NET Web API，它可帮助你构建 HTTP 服务可以访问任何设备。</span><span class="sxs-lookup"><span data-stu-id="e3d47-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="e3d47-467">有关详细信息，请参阅[ASP.NET MVC 4 发行说明](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="e3d47-468">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="e3d47-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="e3d47-469">新功能包括：</span><span class="sxs-lookup"><span data-stu-id="e3d47-469">New features include the following:</span></span>

- <span data-ttu-id="e3d47-470">新的和更新站点模板。</span><span class="sxs-lookup"><span data-stu-id="e3d47-470">New and updated site templates.</span></span>
- <span data-ttu-id="e3d47-471">添加服务器端和客户端验证使用*验证*帮助器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="e3d47-472">若要注册脚本使用资产管理器功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="e3d47-473">正在启用 Facebook 和其他站点使用 OAuth 和 OpenID 登录名。</span><span class="sxs-lookup"><span data-stu-id="e3d47-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="e3d47-474">使用添加图*映射*帮助器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="e3d47-475">运行网页的应用程序的并排方案。</span><span class="sxs-lookup"><span data-stu-id="e3d47-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="e3d47-476">移动设备的呈现页。</span><span class="sxs-lookup"><span data-stu-id="e3d47-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="e3d47-477">有关这些功能和整页的代码示例的详细信息，请参阅[Web Pages 2 Beta 中的常用功能](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="e3d47-478">Visual Web Developer 11 测试版</span><span class="sxs-lookup"><span data-stu-id="e3d47-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="e3d47-479">本部分提供有关 Visual Web Developer 11 测试版和 Visual Studio 2012 Release Candidate 中的 web 开发的改进的信息。</span><span class="sxs-lookup"><span data-stu-id="e3d47-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="e3d47-480">Visual Studio 2010 和 Visual Studio 2012 Release Candidate （项目兼容性） 之间共享的项目</span><span class="sxs-lookup"><span data-stu-id="e3d47-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="e3d47-481">Visual Studio 2012 候选发布版本，直到在较新版本的 Visual Studio 中打开现有项目启动转换向导。</span><span class="sxs-lookup"><span data-stu-id="e3d47-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="e3d47-482">这强制内容 （资产） 的项目和解决方案升级为新格式的内容不向后兼容。</span><span class="sxs-lookup"><span data-stu-id="e3d47-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="e3d47-483">因此，在转换后您无法打开该项目在 Visual Studio 的较旧版本中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="e3d47-484">许多客户告诉我们这不是正确的方法。</span><span class="sxs-lookup"><span data-stu-id="e3d47-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="e3d47-485">在 Visual Studio 11 Beta，我们现在支持共享项目和解决方案的 Visual Studio 2010 SP1。</span><span class="sxs-lookup"><span data-stu-id="e3d47-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="e3d47-486">这意味着，如果您在 Visual Studio 2012 候选发布版本中打开 2010年项目，您将仍将能够在 Visual Studio 2010 SP1 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="e3d47-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d47-487">一些类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 候选发布版本之间共享。</span><span class="sxs-lookup"><span data-stu-id="e3d47-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="e3d47-488">其中包括一些较旧的项目 （如 ASP.NET MVC 2 项目） 或项目出于特定目的 （如安装程序项目）。</span><span class="sxs-lookup"><span data-stu-id="e3d47-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="e3d47-489">当在 Visual Studio 11 Beta 中首次打开 Visual Studio 2010 SP1 Web 项目时，以下属性添加到项目文件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="e3d47-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="e3d47-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="e3d47-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="e3d47-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="e3d47-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="e3d47-492">OldToolsVersion</span></span>
- <span data-ttu-id="e3d47-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="e3d47-493">VisualStudioVersion</span></span>
- <span data-ttu-id="e3d47-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="e3d47-494">VSToolsPath</span></span>

<span data-ttu-id="e3d47-495">FileUpgradeFlags、 UpgradeBackupLocation 和 OldToolsVersion 升级项目文件的进程使用。</span><span class="sxs-lookup"><span data-stu-id="e3d47-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="e3d47-496">它们都使用 Visual Studio 2010 中的项目没有影响。</span><span class="sxs-lookup"><span data-stu-id="e3d47-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="e3d47-497">VisualStudioVersion 是由 MSBuild 4.5，该值指示当前项目的版本的 Visual Studio 的新属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="e3d47-498">在 MSBuild 4.0 （Visual Studio 2010 SP1 使用的 MSBuild 版本） 中不存在此属性，因为我们将默认值注入到项目文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="e3d47-499">VSToolsPath 属性用于确定要导入从 MSBuildExtensionsPath32 设置所表示的路径的正确.targets 文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="e3d47-500">此外，还有与导入元素相关的一些更改。</span><span class="sxs-lookup"><span data-stu-id="e3d47-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="e3d47-501">为了支持这两个版本的 Visual Studio 之间的兼容性需要这些更改。</span><span class="sxs-lookup"><span data-stu-id="e3d47-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d47-502">如果项目 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之间在两台不同计算机上共享，并且该项目包括在应用中的本地数据库\_Data 文件夹中，您必须确保所使用的数据库的 SQL Server 的版本是在这两台计算机上安装。</span><span class="sxs-lookup"><span data-stu-id="e3d47-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="e3d47-503">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="e3d47-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="e3d47-504">为默认值进行了以下更改*Web.config*在 Visual Studio 2012 候选发布版本中使用的网站模板创建的网站文件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="e3d47-505">在中`<httpRuntime>`元素，`encoderType`属性现在设置默认情况下，若要使用 AntiXSS 类型已添加到 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="e3d47-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="e3d47-506">有关详细信息，请参阅[AntiXSS 库](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="e3d47-507">另外，请在`<httpRuntime>`元素，`requestValidationMode`属性设置为"4.5"。</span><span class="sxs-lookup"><span data-stu-id="e3d47-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="e3d47-508">这意味着默认情况下，请求验证配置为使用推迟的 （"延迟"） 验证。</span><span class="sxs-lookup"><span data-stu-id="e3d47-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="e3d47-509">有关详细信息，请参阅[新的 ASP.NET 请求验证功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="e3d47-510">`<modules>`的元素`<system.webServer>`部分不包含`runAllManagedModulesForAllRequests`属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="e3d47-511">（其默认值为 false。）这意味着，如果使用尚未更新到 SP1 的 IIS 7 的版本，则可能必须使用新的站点中的路由问题。</span><span class="sxs-lookup"><span data-stu-id="e3d47-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="e3d47-512">有关详细信息，请参阅[在 IIS 7 ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="e3d47-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="e3d47-513">这些更改不会影响现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="e3d47-514">但是，它们可能表示之间的现有网站和 ASP.NET 4.5 使用新的模板创建的新网站的行为差异。</span><span class="sxs-lookup"><span data-stu-id="e3d47-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="e3d47-515">在 IIS 7 ASP.NET 路由中的本机支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="e3d47-516">这不是这种情况下，更改到 ASP.NET，但如果你正在 IIS 7 未应用 SP1 更新的版本会影响你的新网站项目的模板中的更改。</span><span class="sxs-lookup"><span data-stu-id="e3d47-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="e3d47-517">在 ASP.NET 中，您可以将以下配置设置添加到应用程序以支持路由：</span><span class="sxs-lookup"><span data-stu-id="e3d47-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="e3d47-518">时**runAllManagedModulesForAllRequests**是 true 时，URL 如所示`http://mysite/myapp/home`进入 ASP.NET 中，即使没有任何 *.aspx*， *.mvc*，或在类似扩展URL。</span><span class="sxs-lookup"><span data-stu-id="e3d47-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="e3d47-519">IIS 7，已更新可**runAllManagedModulesForAllRequests**设置不必要和支持 ASP.NET 路由以本机方式。</span><span class="sxs-lookup"><span data-stu-id="e3d47-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="e3d47-520">(有关更新的信息，请参阅 Microsoft 支持文章[更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾](https://support.microsoft.com/kb/980368)。)</span><span class="sxs-lookup"><span data-stu-id="e3d47-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="e3d47-521">如果你的网站正在 IIS 7 上运行，并且如果 IIS 已更新，不需要设置**runAllManagedModulesForAllRequests**为 true。</span><span class="sxs-lookup"><span data-stu-id="e3d47-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="e3d47-522">实际上，将其设置为 true 不是建议，因为它会添加不必要的处理开销请求。</span><span class="sxs-lookup"><span data-stu-id="e3d47-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="e3d47-523">当此设置为 true 时，所有请求，其中包含用于 *.htm*， *.jpg*，和其他静态文件，也都经过了 ASP.NET 请求管道。</span><span class="sxs-lookup"><span data-stu-id="e3d47-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="e3d47-524">如果创建新的 ASP.NET 4.5 网站使用 Visual Studio 2012 RC 中提供的模板，为网站配置不包括**runAllManagedModulesForAllRequests**设置。</span><span class="sxs-lookup"><span data-stu-id="e3d47-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="e3d47-525">这意味着默认情况下设置为 false。</span><span class="sxs-lookup"><span data-stu-id="e3d47-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="e3d47-526">然后，如果您运行该网站在 Windows 7 上没有安装 SP1 的情况下，IIS 7 将不包括所需的更新。</span><span class="sxs-lookup"><span data-stu-id="e3d47-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="e3d47-527">因此，路由不起作用，将看到错误。</span><span class="sxs-lookup"><span data-stu-id="e3d47-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="e3d47-528">如果您遇到的问题，路由不起作用，可以执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="e3d47-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="e3d47-529">更新到 SP1，这样会将更新添加到 IIS 7 的 Windows 7。</span><span class="sxs-lookup"><span data-stu-id="e3d47-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="e3d47-530">安装在前面列出的 Microsoft 技术支持文章中所述的更新。</span><span class="sxs-lookup"><span data-stu-id="e3d47-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="e3d47-531">设置**runAllManagedModulesForAllRequests**为 true，该网站的 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="e3d47-532">请注意，这将向请求添加一些开销。</span><span class="sxs-lookup"><span data-stu-id="e3d47-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="e3d47-533">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="e3d47-534">智能任务</span><span class="sxs-lookup"><span data-stu-id="e3d47-534">Smart Tasks</span></span>

<span data-ttu-id="e3d47-535">在设计视图中，复杂属性的服务器控件通常具有关联的对话框和向导，可轻松地将其设置。</span><span class="sxs-lookup"><span data-stu-id="e3d47-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="e3d47-536">例如，使用特殊的对话框中，若要添加到的数据源*Repeater*控制或将列添加到*GridView*控件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="e3d47-537">但是，这种类型的复杂属性的用户界面帮助尚未在源视图中可用。</span><span class="sxs-lookup"><span data-stu-id="e3d47-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="e3d47-538">因此，Visual Studio 11 引入了源视图的智能任务。</span><span class="sxs-lookup"><span data-stu-id="e3d47-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="e3d47-539">智能任务是在 C# 和 Visual Basic 编辑器中的常用功能的上下文感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="e3d47-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="e3d47-540">对于 ASP.NET Web 窗体控件，智能任务显示服务器标记为较小的标志符号时插入点放在元素内，则：</span><span class="sxs-lookup"><span data-stu-id="e3d47-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="e3d47-541">单击字形或按 CTRL + 时，将扩展智能任务。</span><span class="sxs-lookup"><span data-stu-id="e3d47-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="e3d47-542">（圆点），就像在代码编辑器中一样。</span><span class="sxs-lookup"><span data-stu-id="e3d47-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="e3d47-543">然后，它将显示类似于设计视图中的智能任务的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="e3d47-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="e3d47-544">例如，智能任务在上图中显示的 GridView 任务选项。</span><span class="sxs-lookup"><span data-stu-id="e3d47-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="e3d47-545">如果选择编辑列，将显示以下对话框：</span><span class="sxs-lookup"><span data-stu-id="e3d47-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="e3d47-546">填写对话框设置相同的属性可以设置在设计视图中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="e3d47-547">当您单击确定时，是使用新的设置更新控件的标记：</span><span class="sxs-lookup"><span data-stu-id="e3d47-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="e3d47-548">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-548">WAI-ARIA support</span></span>

<span data-ttu-id="e3d47-549">编写可访问的网站变得越来越重要。</span><span class="sxs-lookup"><span data-stu-id="e3d47-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="e3d47-550">[WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义开发人员应如何编写可访问的网站。</span><span class="sxs-lookup"><span data-stu-id="e3d47-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="e3d47-551">在 Visual Studio 中现在完全支持此标准。</span><span class="sxs-lookup"><span data-stu-id="e3d47-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="e3d47-552">例如，*角色*属性现在具有完整的 IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="e3d47-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="e3d47-553">WAI-ARIA 标准还引入了带有前缀的特性*aria-* 能够让你将语义添加到 HTML5 文档。</span><span class="sxs-lookup"><span data-stu-id="e3d47-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="e3d47-554">Visual Studio 也完全支持这些*aria-* 属性：</span><span class="sxs-lookup"><span data-stu-id="e3d47-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="e3d47-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="e3d47-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="e3d47-556">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="e3d47-556">New HTML5 snippets</span></span>

<span data-ttu-id="e3d47-557">若要使其更快、 更轻松地编写常用的 HTML5 标记，Visual Studio 提供了大量的代码段。</span><span class="sxs-lookup"><span data-stu-id="e3d47-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="e3d47-558">视频的代码段是一个示例：</span><span class="sxs-lookup"><span data-stu-id="e3d47-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="e3d47-559">调用代码段，按 Tab 键两次时在 IntelliSense 中选择元素：</span><span class="sxs-lookup"><span data-stu-id="e3d47-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="e3d47-560">这将产生了可以自定义的段。</span><span class="sxs-lookup"><span data-stu-id="e3d47-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="e3d47-561">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="e3d47-561">Extract to user control</span></span>

<span data-ttu-id="e3d47-562">在大型 web 页中，它可以是一个好办法将各个部分移动到用户控件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="e3d47-563">这种形式的重构可帮助提高页面的可读性和可简化对页结构。</span><span class="sxs-lookup"><span data-stu-id="e3d47-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="e3d47-564">若要简化此过程，编辑源视图中的 Web 窗体页时，您可以立即在页面中选择文本，右键单击它，，然后选择中的提取到用户控件：</span><span class="sxs-lookup"><span data-stu-id="e3d47-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="e3d47-565">适用于在特性中的代码片段 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="e3d47-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="e3d47-566">Visual Studio 一直在为服务器端代码片段中的任何页面或控件提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="e3d47-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="e3d47-567">现在 Visual Studio 包括 IntelliSense 以及 HTML 属性中的代码片段。</span><span class="sxs-lookup"><span data-stu-id="e3d47-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="e3d47-568">这使得更轻松地创建数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="e3d47-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="e3d47-569">匹配的标记重命名开始或结束标记时自动重命名</span><span class="sxs-lookup"><span data-stu-id="e3d47-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="e3d47-570">如果重命名的 HTML 元素 (例如，更改*div*标记为*标头*标记)，则相应的打开或关闭标记也发生实时更改。</span><span class="sxs-lookup"><span data-stu-id="e3d47-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="e3d47-571">这有助于避免忘记更改结束标记或更改的错误的一个错误。</span><span class="sxs-lookup"><span data-stu-id="e3d47-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="e3d47-572">生成事件处理程序</span><span class="sxs-lookup"><span data-stu-id="e3d47-572">Event handler generation</span></span>

<span data-ttu-id="e3d47-573">Visual Studio 现在包含在源视图，以帮助您编写事件处理程序并将其手动绑定中的功能。</span><span class="sxs-lookup"><span data-stu-id="e3d47-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="e3d47-574">如果正在编辑源视图中的事件名称，IntelliSense 将显示&lt;创建新事件&gt;，此操作将创建一个事件处理程序中页面的代码，具有正确的签名：</span><span class="sxs-lookup"><span data-stu-id="e3d47-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="e3d47-575">默认情况下，事件处理程序将使用控件的 ID 的事件处理方法的名称：</span><span class="sxs-lookup"><span data-stu-id="e3d47-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="e3d47-576">生成事件处理程序将如下所示 （在这种情况下，在 C# 中）：</span><span class="sxs-lookup"><span data-stu-id="e3d47-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="e3d47-577">智能缩进</span><span class="sxs-lookup"><span data-stu-id="e3d47-577">Smart indent</span></span>

<span data-ttu-id="e3d47-578">当您按 Enter 空 HTML 元素中的时，编辑器将在适当的位置将插入点：</span><span class="sxs-lookup"><span data-stu-id="e3d47-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="e3d47-579">如果按 Enter 在此位置，结束标记是向下移动和缩进，以匹配的开始标记。</span><span class="sxs-lookup"><span data-stu-id="e3d47-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="e3d47-580">插入点还缩进：</span><span class="sxs-lookup"><span data-stu-id="e3d47-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="e3d47-581">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="e3d47-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="e3d47-582">Visual Studio 现在筛选器基于，以便它显示仅与相关的选项键入的内容中的 IntelliSense 列表：</span><span class="sxs-lookup"><span data-stu-id="e3d47-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="e3d47-583">IntelliSense 筛选器也基于智能感知列表中的各单词的词首字母大写。</span><span class="sxs-lookup"><span data-stu-id="e3d47-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="e3d47-584">例如，如果键入"dl"时，会显示 dl 和 asp: DataList:</span><span class="sxs-lookup"><span data-stu-id="e3d47-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="e3d47-585">此功能，可更快地获取已知元素的语句完成。</span><span class="sxs-lookup"><span data-stu-id="e3d47-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="e3d47-586">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-586">JavaScript Editor</span></span>

<span data-ttu-id="e3d47-587">Visual Studio 2012 Release Candidate 中的 JavaScript 编辑器是一个全新并极大地提高了使用 Visual Studio 中的 JavaScript 的体验。</span><span class="sxs-lookup"><span data-stu-id="e3d47-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="e3d47-588">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="e3d47-588">Code outlining</span></span>

<span data-ttu-id="e3d47-589">大纲区域现在会自动创建的所有函数，允许您折叠不相关的当前焦点的文件部分。</span><span class="sxs-lookup"><span data-stu-id="e3d47-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="e3d47-590">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="e3d47-590">Brace matching</span></span>

<span data-ttu-id="e3d47-591">将插入点放上一个开始标记或右大括号后，编辑器突出显示匹配的一个。</span><span class="sxs-lookup"><span data-stu-id="e3d47-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="e3d47-592">转到定义</span><span class="sxs-lookup"><span data-stu-id="e3d47-592">Go to Definition</span></span>

<span data-ttu-id="e3d47-593">转到定义命令，可以跳转到函数或变量的源。</span><span class="sxs-lookup"><span data-stu-id="e3d47-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="e3d47-594">ECMAScript5 的支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-594">ECMAScript5 support</span></span>

<span data-ttu-id="e3d47-595">在编辑器中 ECMAScript5，介绍了 JavaScript 语言的标准的最新版本支持的新语法和 Api。</span><span class="sxs-lookup"><span data-stu-id="e3d47-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="e3d47-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="e3d47-596">DOM IntelliSense</span></span>

<span data-ttu-id="e3d47-597">IntelliSense for DOM Api 已得到改进，支持许多新 HTML5 Api 包括*querySelector*，DOM 存储，跨文档消息传送，并*画布*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="e3d47-598">DOM IntelliSense 现在是驱动通过一个简单的 JavaScript 文件，而不是本机类型库定义。</span><span class="sxs-lookup"><span data-stu-id="e3d47-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="e3d47-599">这样，可以轻松进行扩展或替换。</span><span class="sxs-lookup"><span data-stu-id="e3d47-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="e3d47-600">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="e3d47-600">VSDOC signature overloads</span></span>

<span data-ttu-id="e3d47-601">详细的 IntelliSense 注释现在为单独的 JavaScript 函数的重载使用新的声明*&lt;签名&gt;* 元素，在此示例中所示：</span><span class="sxs-lookup"><span data-stu-id="e3d47-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="e3d47-602">隐式引用</span><span class="sxs-lookup"><span data-stu-id="e3d47-602">Implicit references</span></span>

<span data-ttu-id="e3d47-603">现在可以添加 JavaScript 文件，将隐式包含的文件列表中任何给定的 JavaScript 文件或块的引用，这意味着，你将获得用于其内容的 IntelliSense 的集中列表。</span><span class="sxs-lookup"><span data-stu-id="e3d47-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="e3d47-604">例如，可以将 jQuery 文件添加到中央列表的文件，并你将获得 IntelliSense 用于 jQuery 函数在文件中，任何 JavaScript 块中是否已显式引用它 (使用 / /&lt;引用 /&gt;) 或不。</span><span class="sxs-lookup"><span data-stu-id="e3d47-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="e3d47-605">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="e3d47-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="e3d47-606">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="e3d47-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="e3d47-607">CSS 现在筛选器基于的 CSS 属性和值受所选架构的智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="e3d47-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="e3d47-608">IntelliSense 还支持标题大小写搜索：</span><span class="sxs-lookup"><span data-stu-id="e3d47-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="e3d47-609">分层缩进</span><span class="sxs-lookup"><span data-stu-id="e3d47-609">Hierarchical indentation</span></span>

<span data-ttu-id="e3d47-610">CSS 编辑器使用缩进显示层次结构的规则，这将使您的级联规则的逻辑上组织方式概述。</span><span class="sxs-lookup"><span data-stu-id="e3d47-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="e3d47-611">在以下示例中，#list 选择器列表的级联子项，因此缩进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="e3d47-612">下面的示例显示了更复杂的继承：</span><span class="sxs-lookup"><span data-stu-id="e3d47-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="e3d47-613">规则的缩进取决于其父规则。</span><span class="sxs-lookup"><span data-stu-id="e3d47-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="e3d47-614">默认情况下，启用分层缩进，但您也可以禁用选项对话框中 （工具，从菜单栏中的选项）：</span><span class="sxs-lookup"><span data-stu-id="e3d47-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="e3d47-615">CSS 攻击支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-615">CSS hacks support</span></span>

<span data-ttu-id="e3d47-616">数百个实际 CSS 文件的分析显示 CSS 攻击是很常见，并且 Visual Studio 现在支持最广泛使用的。</span><span class="sxs-lookup"><span data-stu-id="e3d47-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="e3d47-617">此支持包括 IntelliSense 和验证在星型 (\*) 和下划线 (\_) 属性技巧：</span><span class="sxs-lookup"><span data-stu-id="e3d47-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="e3d47-618">典型的选择器技巧也支持，以便即使在将其应用维护分层缩进。</span><span class="sxs-lookup"><span data-stu-id="e3d47-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="e3d47-619">用于映射到目标 Internet Explorer 7 典型选择器技巧，也是与一个选择器前面加上 *\*： 第一个子 + html*。</span><span class="sxs-lookup"><span data-stu-id="e3d47-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="e3d47-620">使用该规则将维护分层缩进：</span><span class="sxs-lookup"><span data-stu-id="e3d47-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="e3d47-621">供应商特定的架构 (-moz--webkit)</span><span class="sxs-lookup"><span data-stu-id="e3d47-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="e3d47-622">CSS3 引入了在不同的时间由不同的浏览器实现的许多属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="e3d47-623">这以前通过使用特定于供应商的语法的强制开发人员对特定浏览器的代码。</span><span class="sxs-lookup"><span data-stu-id="e3d47-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="e3d47-624">现在在 IntelliSense 中包含这些特定于浏览器的属性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="e3d47-625">注释和取消注释支持</span><span class="sxs-lookup"><span data-stu-id="e3d47-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="e3d47-626">现在可以添加注释和取消注释使用的相同的快捷方式 （Ctrl + K、 注释为 C 和 Ctrl + K，您可以取消注释） 在代码编辑器中使用的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="e3d47-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="e3d47-627">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="e3d47-627">Color picker</span></span>

<span data-ttu-id="e3d47-628">在以前版本的 Visual Studio 中，IntelliSense 的颜色相关属性包括已命名的颜色值的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="e3d47-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="e3d47-629">该列表已替换为全功能颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="e3d47-630">当您输入颜色值时，颜色选取器，将自动显示并显示一个列表的以前用过跟默认颜色调色板的颜色。</span><span class="sxs-lookup"><span data-stu-id="e3d47-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="e3d47-631">可以选择使用鼠标或键盘的颜色。</span><span class="sxs-lookup"><span data-stu-id="e3d47-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="e3d47-632">列表可以扩展到完成颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="e3d47-633">在选取器可用于通过自动转换为任何颜色 RGBA 不透明度滑块移动时控制 alpha 通道：</span><span class="sxs-lookup"><span data-stu-id="e3d47-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="e3d47-634">代码段</span><span class="sxs-lookup"><span data-stu-id="e3d47-634">Snippets</span></span>

<span data-ttu-id="e3d47-635">CSS 编辑器中的代码段可使其更加容易和快速创建跨浏览器样式。</span><span class="sxs-lookup"><span data-stu-id="e3d47-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="e3d47-636">需要特定于浏览器设置的许多 CSS3 属性现在为代码片段已回滚。</span><span class="sxs-lookup"><span data-stu-id="e3d47-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="e3d47-637">CSS 代码段支持高级的方案 （如 CSS3 媒体查询），通过键入 at 符号 (@)，它显示了智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="e3d47-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="e3d47-638">当选择@media值并按 Tab，CSS 编辑器将插入以下代码片段：</span><span class="sxs-lookup"><span data-stu-id="e3d47-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="e3d47-639">与代码的代码段，可以创建自己的 CSS 代码段。</span><span class="sxs-lookup"><span data-stu-id="e3d47-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="e3d47-640">自定义区域</span><span class="sxs-lookup"><span data-stu-id="e3d47-640">Custom regions</span></span>

<span data-ttu-id="e3d47-641">名为代码区域，已在代码编辑器中可用，现可用于编辑 CSS。</span><span class="sxs-lookup"><span data-stu-id="e3d47-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="e3d47-642">这样可以轻松地分组相关的样式块。</span><span class="sxs-lookup"><span data-stu-id="e3d47-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="e3d47-643">一个区域处于折叠状态时将显示区域的名称：</span><span class="sxs-lookup"><span data-stu-id="e3d47-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="e3d47-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="e3d47-644">Page Inspector</span></span>

<span data-ttu-id="e3d47-645">Page Inspector 是一款呈现网页 （HTML、 Web 窗体、 ASP.NET MVC 或网页） 在 Visual Studio IDE 中，并允许您检查源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="e3d47-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="e3d47-646">对于 ASP.NET 页面，Page Inspector 允许您确定哪些服务器端代码生成到浏览器呈现的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="e3d47-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="e3d47-647">有关 Page Inspector 的详细信息，请参阅以下教程：</span><span class="sxs-lookup"><span data-stu-id="e3d47-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="e3d47-648">使用 Page Inspector 中[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="e3d47-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="e3d47-649">使用 Page Inspector 中[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span><span class="sxs-lookup"><span data-stu-id="e3d47-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="e3d47-650">发布</span><span class="sxs-lookup"><span data-stu-id="e3d47-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="e3d47-651">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="e3d47-651">Publish profiles</span></span>

<span data-ttu-id="e3d47-652">在 Visual Studio 2010 中，Web 应用程序项目的发布信息不存储在版本控制中并不适合与他人共享。</span><span class="sxs-lookup"><span data-stu-id="e3d47-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="e3d47-653">在 Visual Studio 2012 候选发布版，已更改的发布配置文件的格式。</span><span class="sxs-lookup"><span data-stu-id="e3d47-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="e3d47-654">变得一个团队项目，并且现在可以轻松地从基于 MSBuild 的生成使用。</span><span class="sxs-lookup"><span data-stu-id="e3d47-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="e3d47-655">生成配置的信息是在发布对话框中，以便您可以轻松地切换发布前的生成配置。</span><span class="sxs-lookup"><span data-stu-id="e3d47-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="e3d47-656">发布配置文件存储在 PublishProfiles 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e3d47-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="e3d47-657">文件夹的位置取决于正在使用哪种编程语言：</span><span class="sxs-lookup"><span data-stu-id="e3d47-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="e3d47-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="e3d47-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="e3d47-659">我 Project\PublishProfiles Visual Basic:</span><span class="sxs-lookup"><span data-stu-id="e3d47-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="e3d47-660">每个配置文件是一个 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="e3d47-661">在发布期间，此文件导入项目的 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="e3d47-662">在 Visual Studio 2010 中，如果你想要更改包或发布过程中，则必须将你的自定义放入名为的文件**ProjectName**。 wpp.targets。</span><span class="sxs-lookup"><span data-stu-id="e3d47-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="e3d47-663">仍受支持，但现在可以将你的自定义放入发布配置文件本身。</span><span class="sxs-lookup"><span data-stu-id="e3d47-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="e3d47-664">这样一来，仅为该配置文件，将使用自定义项。</span><span class="sxs-lookup"><span data-stu-id="e3d47-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="e3d47-665">你可以现在还利用发布配置文件从 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="e3d47-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="e3d47-666">为此，请使用以下命令生成项目时：</span><span class="sxs-lookup"><span data-stu-id="e3d47-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="e3d47-667">Project.csproj 值是项目的路径和 ProfileName 是要发布的配置文件的名称。</span><span class="sxs-lookup"><span data-stu-id="e3d47-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="e3d47-668">或者，而不是传递的配置文件名称*PublishProfile*属性，您可以传入的完整路径的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="e3d47-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="e3d47-669">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="e3d47-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="e3d47-670">对于 Web 应用程序项目，Visual Studio 2012 候选发布版本中添加一个选项，可以预编译和合并发布时你的站点内容或包项目的打包/发布 Web 属性页上。</span><span class="sxs-lookup"><span data-stu-id="e3d47-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="e3d47-671">若要查看这些选项，用鼠标右键单击解决方案资源管理器中的项目，选择属性，然后选择打包/发布 Web 属性页。</span><span class="sxs-lookup"><span data-stu-id="e3d47-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="e3d47-672">下图显示预编译此应用程序，然后发布选项。</span><span class="sxs-lookup"><span data-stu-id="e3d47-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="e3d47-673">选中此选项后，Visual Studio 预编译的应用程序每次您发布或打包 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e3d47-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="e3d47-674">如果你想要控制如何预编译站点或如何合并程序集，请单击高级按钮以配置这些选项。</span><span class="sxs-lookup"><span data-stu-id="e3d47-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="e3d47-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="e3d47-675">IIS Express</span></span>

<span data-ttu-id="e3d47-676">在 Visual Studio 中测试 web 项目的默认 web 服务器现在是 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="e3d47-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="e3d47-677">Visual Studio 开发服务器仍在开发期间，本地 web 服务器的选项，但 IIS Express 现在是建议的服务器。</span><span class="sxs-lookup"><span data-stu-id="e3d47-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="e3d47-678">在 Visual Studio 11 Beta 中使用 IIS Express 的体验是非常类似于在 Visual Studio 2010 SP1 中使用它。</span><span class="sxs-lookup"><span data-stu-id="e3d47-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="e3d47-679">免责声明</span><span class="sxs-lookup"><span data-stu-id="e3d47-679">Disclaimer</span></span>

<span data-ttu-id="e3d47-680">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="e3d47-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="e3d47-681">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="e3d47-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="e3d47-682">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="e3d47-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="e3d47-683">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="e3d47-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="e3d47-684">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="e3d47-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="e3d47-685">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="e3d47-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="e3d47-686">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="e3d47-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="e3d47-687">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="e3d47-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="e3d47-688">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="e3d47-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="e3d47-689">除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。</span><span class="sxs-lookup"><span data-stu-id="e3d47-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="e3d47-690">(C) 2012 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="e3d47-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="e3d47-691">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="e3d47-691">All rights reserved.</span></span>

<span data-ttu-id="e3d47-692">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="e3d47-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="e3d47-693">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="e3d47-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
