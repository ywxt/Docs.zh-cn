---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: 在 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能 |Microsoft 文档
author: rick-anderson
description: 本文档介绍新功能和 ASP.NET 4.5 中引入的增强功能。 它还介绍了为 web 开发正在进行的改进...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/29/2012
ms.topic: article
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 16a2fa4b1b6617430703853543cbf29e18ba1103
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
ms.locfileid: "28886437"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="362ad-104">在 ASP.NET 4.5 和 Visual Studio 2012 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="362ad-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>
====================
> <span data-ttu-id="362ad-105">本文档介绍新功能和 ASP.NET 4.5 中引入的增强功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="362ad-106">它还介绍了对 Visual Studio 2012 中的 web 开发的改进。</span><span class="sxs-lookup"><span data-stu-id="362ad-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="362ad-107">本文档最初在 2012 年 2 月 29 日发布。</span><span class="sxs-lookup"><span data-stu-id="362ad-107">This document was originally published on February 29, 2012.</span></span>


- [<span data-ttu-id="362ad-108">ASP.NET 核心运行时和 Framework</span><span class="sxs-lookup"><span data-stu-id="362ad-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="362ad-109">以异步方式读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="362ad-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="362ad-110">对 HttpRequest 处理改进</span><span class="sxs-lookup"><span data-stu-id="362ad-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="362ad-111">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="362ad-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="362ad-112">支持*await*和*任务*-基于异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="362ad-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="362ad-113">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="362ad-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="362ad-114">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="362ad-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="362ad-115">新的 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="362ad-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="362ad-116">延迟 （"迟缓"） 请求验证</span><span class="sxs-lookup"><span data-stu-id="362ad-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="362ad-117">对未经过验证的请求的支持</span><span class="sxs-lookup"><span data-stu-id="362ad-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="362ad-118">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="362ad-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="362ad-119">Websocket 协议的支持</span><span class="sxs-lookup"><span data-stu-id="362ad-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="362ad-120">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="362ad-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="362ad-121">用于 Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="362ad-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="362ad-122">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="362ad-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="362ad-123">新的性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="362ad-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="362ad-124">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="362ad-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="362ad-125">用于启动速度更快的多核 JIT 编译</span><span class="sxs-lookup"><span data-stu-id="362ad-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="362ad-126">若要针对内存优化的优化垃圾回收</span><span class="sxs-lookup"><span data-stu-id="362ad-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="362ad-127">预提取的 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="362ad-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="362ad-128">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="362ad-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="362ad-129">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="362ad-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="362ad-130">模型绑定</span><span class="sxs-lookup"><span data-stu-id="362ad-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="362ad-131">选择数据</span><span class="sxs-lookup"><span data-stu-id="362ad-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="362ad-132">值在提供程序</span><span class="sxs-lookup"><span data-stu-id="362ad-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="362ad-133">筛选来自控件的值</span><span class="sxs-lookup"><span data-stu-id="362ad-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="362ad-134">HTML 编码数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="362ad-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="362ad-135">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="362ad-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="362ad-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="362ad-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="362ad-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="362ad-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="362ad-138">ASP.NET Web Pages 2</span><span class="sxs-lookup"><span data-stu-id="362ad-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="362ad-139">Visual Studio 2012 候选发布版本</span><span class="sxs-lookup"><span data-stu-id="362ad-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="362ad-140">Visual Studio 2010 和 Visual Studio 2012 候选发布版本 （项目兼容性） 之间共享的项目</span><span class="sxs-lookup"><span data-stu-id="362ad-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="362ad-141">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="362ad-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="362ad-142">在 IIS 7 ASP.NET 路由中的本机支持</span><span class="sxs-lookup"><span data-stu-id="362ad-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="362ad-143">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="362ad-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="362ad-144">智能任务</span><span class="sxs-lookup"><span data-stu-id="362ad-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="362ad-145">WAI ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="362ad-146">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="362ad-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="362ad-147">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="362ad-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="362ad-148">在属性中的代码而有价值的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="362ad-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="362ad-149">当你重命名一个开始标记或结束标记时匹配标记的自动重命名</span><span class="sxs-lookup"><span data-stu-id="362ad-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="362ad-150">事件处理程序生成</span><span class="sxs-lookup"><span data-stu-id="362ad-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="362ad-151">智能缩进</span><span class="sxs-lookup"><span data-stu-id="362ad-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="362ad-152">自动减少语句结束</span><span class="sxs-lookup"><span data-stu-id="362ad-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="362ad-153">JavaScript Editor</span><span class="sxs-lookup"><span data-stu-id="362ad-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="362ad-154">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="362ad-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="362ad-155">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="362ad-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="362ad-156">转到定义</span><span class="sxs-lookup"><span data-stu-id="362ad-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="362ad-157">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="362ad-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="362ad-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="362ad-159">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="362ad-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="362ad-160">隐式引用</span><span class="sxs-lookup"><span data-stu-id="362ad-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="362ad-161">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="362ad-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="362ad-162">自动减少语句结束</span><span class="sxs-lookup"><span data-stu-id="362ad-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="362ad-163">分层缩进。</span><span class="sxs-lookup"><span data-stu-id="362ad-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="362ad-164">CSS hacks 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="362ad-165">供应商特定架构 (-moz-，易于使用的功能)</span><span class="sxs-lookup"><span data-stu-id="362ad-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="362ad-166">注释和 uncommenting 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="362ad-167">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="362ad-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="362ad-168">片段</span><span class="sxs-lookup"><span data-stu-id="362ad-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="362ad-169">自定义区域</span><span class="sxs-lookup"><span data-stu-id="362ad-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="362ad-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="362ad-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="362ad-171">发布</span><span class="sxs-lookup"><span data-stu-id="362ad-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="362ad-172">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="362ad-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="362ad-173">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="362ad-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="362ad-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="362ad-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="362ad-175">Disclaimer</span><span class="sxs-lookup"><span data-stu-id="362ad-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="362ad-176">ASP.NET 核心运行时和 Framework</span><span class="sxs-lookup"><span data-stu-id="362ad-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="362ad-177">以异步方式读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="362ad-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="362ad-178">ASP.NET 4 引入了能够读取 HTTP 请求实体作为流使用*HttpRequest.GetBufferlessInputStream*方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="362ad-179">此方法提供流式处理访问请求实体。</span><span class="sxs-lookup"><span data-stu-id="362ad-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="362ad-180">但是，它以同步方式执行，该请求的持续时间内绑定到某个线程。</span><span class="sxs-lookup"><span data-stu-id="362ad-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="362ad-181">ASP.NET 4.5 支持能够读取流在 HTTP 请求实体，以异步方式和异步刷新的能力。</span><span class="sxs-lookup"><span data-stu-id="362ad-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="362ad-182">ASP.NET 4.5 还为你提供了双缓冲提供与下游 HTTP 处理程序，例如.aspx 页处理程序和 ASP.NET MVC 的轻松集成控制器的 HTTP 请求实体的功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="362ad-183">对 HttpRequest 处理改进</span><span class="sxs-lookup"><span data-stu-id="362ad-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="362ad-184">ASP.NET 4.5，从返回的流引用*HttpRequest.GetBufferlessInputStream*支持同步和异步读取的方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="362ad-185">*流*从返回的对象*GetBufferlessInputStream*现在实现 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="362ad-186">异步*流*方法使你可以以异步方式在读取请求实体中的区块，同时 ASP.NET 释放当前线程之间的异步读取循环每次迭代。</span><span class="sxs-lookup"><span data-stu-id="362ad-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="362ad-187">ASP.NET 4.5 还添加了用于缓冲方式读取请求实体的助理方法： *HttpRequest.GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="362ad-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="362ad-188">此新的重载的工作原理类似*GetBufferlessInputStream*，支持同步和异步读取。</span><span class="sxs-lookup"><span data-stu-id="362ad-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="362ad-189">但是，如读取、 *GetBufferedInputStream*还将实体字节复制到 ASP.NET 内部缓冲区，这样，下游模块和处理程序仍可以访问的请求实体。</span><span class="sxs-lookup"><span data-stu-id="362ad-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="362ad-190">例如，如果某些上游管道中的代码具有已读取请求实体使用*GetBufferedInputStream*，你仍然可以使用*HttpRequest.Form*或*HttpRequest.Files*.</span><span class="sxs-lookup"><span data-stu-id="362ad-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="362ad-191">这允许你对执行异步处理的请求 （例如，流式处理大型文件上载到数据库），但仍运行的.aspx 页和 MVC ASP.NET 控制器之后。</span><span class="sxs-lookup"><span data-stu-id="362ad-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="362ad-192">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="362ad-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="362ad-193">发送到 HTTP 客户端的响应可能需要相当长的时间，当客户端很远，或具有低带宽连接。</span><span class="sxs-lookup"><span data-stu-id="362ad-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="362ad-194">通常 ASP.NET 缓冲响应字节数，因为它们创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="362ad-195">ASP.NET 然后执行一个发送操作的请求处理的最末尾的应计缓冲区。</span><span class="sxs-lookup"><span data-stu-id="362ad-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="362ad-196">如果所有缓冲的响应较大 （例如，流式处理的大型文件，以便客户端），则必须定期调用*HttpResponse.Flush*将缓冲的输出发送到客户端并保持受控制的内存使用量。</span><span class="sxs-lookup"><span data-stu-id="362ad-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="362ad-197">但是，因为*刷新*是同步调用，以迭代方式调用*刷新*仍然可能长时间运行的请求的持续时间内消耗线程。</span><span class="sxs-lookup"><span data-stu-id="362ad-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="362ad-198">ASP.NET 4.5 增加了支持对使用以异步方式执行刷新的*BeginFlush*和*EndFlush*方法*HttpResponse*类。</span><span class="sxs-lookup"><span data-stu-id="362ad-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="362ad-199">使用这些方法，可以创建异步的模块和异步处理程序以增量方式将数据发送到客户端而不会占用操作系统线程。</span><span class="sxs-lookup"><span data-stu-id="362ad-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="362ad-200">在此期间*BeginFlush*和*EndFlush*调用，ASP.NET 释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="362ad-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="362ad-201">这样会明显降低支持长时间运行 HTTP 下载所需的活动线程的总数。</span><span class="sxs-lookup"><span data-stu-id="362ad-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="362ad-202">支持*await*和*任务*-基于异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="362ad-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="362ad-203">.NET Framework 4 引入了称为异步编程概念*任务*。</span><span class="sxs-lookup"><span data-stu-id="362ad-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="362ad-204">任务表示通过*任务*类型和相关的类型中*System.Threading.Tasks*命名空间。</span><span class="sxs-lookup"><span data-stu-id="362ad-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="362ad-205">.NET Framework 4.5 上生成了编译器增强功能，请使用*任务*对象简单。</span><span class="sxs-lookup"><span data-stu-id="362ad-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="362ad-206">在.NET Framework 4.5，编译器支持两个新的关键字： *await*和*异步*。</span><span class="sxs-lookup"><span data-stu-id="362ad-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="362ad-207">*Await*关键字是用于指示语法的一段代码应以异步方式等待代码的其他部分的速记。</span><span class="sxs-lookup"><span data-stu-id="362ad-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="362ad-208">*异步*关键字都表示一个提示，可用于将方法标记为基于任务的异步方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="362ad-209">组合*await*，*异步*，和*任务*对象使可以你在.NET 4.5 中编写异步代码更加容易。</span><span class="sxs-lookup"><span data-stu-id="362ad-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="362ad-210">ASP.NET 4.5 支持可让你编写异步 HTTP 模块和使用新的编译器增强功能的异步 HTTP 处理程序的新 Api 与这些简化形式。</span><span class="sxs-lookup"><span data-stu-id="362ad-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="362ad-211">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="362ad-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="362ad-212">假设你想要执行返回的方法内的异步工作*任务*对象。</span><span class="sxs-lookup"><span data-stu-id="362ad-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="362ad-213">下面的代码示例定义的异步方法，使要下载 Microsoft 主页上的异步调用。</span><span class="sxs-lookup"><span data-stu-id="362ad-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="362ad-214">请注意，使用*异步*方法签名中的关键字和*await*调用*DownloadStringTaskAsync*。</span><span class="sxs-lookup"><span data-stu-id="362ad-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="362ad-215">这就是所有你必须编写 —.NET Framework 自动将处理时等待下载完成，以及下载完成后自动还原调用堆栈展开调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="362ad-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="362ad-216">现在假设你想要在异步 ASP.NET HTTP 模块中使用此异步方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="362ad-217">ASP.NET 4.5 包括一个帮助器方法 (*EventHandlerTaskAsyncHelper*) 和新的委托类型 (*TaskEventHandler*) 可用于集成有较旧的基于任务的异步方法公开的 ASP.NET HTTP 管道的异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="362ad-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="362ad-218">此示例演示如何：</span><span class="sxs-lookup"><span data-stu-id="362ad-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="362ad-219">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="362ad-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="362ad-220">在 ASP.NET 中编写异步处理程序的传统方法是实现*IHttpAsyncHandler*接口。</span><span class="sxs-lookup"><span data-stu-id="362ad-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="362ad-221">ASP.NET 4.5 引入了*HttpTaskAsyncHandler*异步基类型，您可以从其中，这样，就可以更轻松地编写异步处理程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="362ad-222">*HttpTaskAsyncHandler*类型为抽象类，并要求你重写*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="362ad-223">内部 ASP.NET 负责集成返回签名 (*任务*对象) 的*ProcessRequestAsync*与由 ASP.NET 管道的较旧异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="362ad-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="362ad-224">下面的示例演示如何使用*任务*和*await*作为异步 HTTP 处理程序的实现的一部分：</span><span class="sxs-lookup"><span data-stu-id="362ad-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="362ad-225">新的 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="362ad-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="362ad-226">默认情况下，ASP.NET 将执行请求验证-它会检查请求以查找标记或脚本中的字段、 标头，cookie 和等等。</span><span class="sxs-lookup"><span data-stu-id="362ad-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="362ad-227">如果检测到任何时，ASP.NET 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="362ad-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="362ad-228">将充当防范潜在的跨站点脚本攻击第一行。</span><span class="sxs-lookup"><span data-stu-id="362ad-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="362ad-229">ASP.NET 4.5，可以轻松有选择地读取未经过验证的请求数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="362ad-230">ASP.NET 4.5 还集成常用 AntiXSS 库中，以前外部库。</span><span class="sxs-lookup"><span data-stu-id="362ad-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="362ad-231">开发人员已经常要求有选择地关闭请求验证其应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="362ad-232">例如，如果你的应用程序是论坛软件，你可能想要允许用户提交 HTML 格式论坛帖子和注释，但仍确保请求验证检查其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="362ad-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="362ad-233">ASP.NET 4.5 引入了容易让你可以有选择地处理未经过验证的输入的两个功能： 延迟 （"迟缓"） 请求验证并对未经验证的请求数据的访问。</span><span class="sxs-lookup"><span data-stu-id="362ad-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="362ad-234">延迟 （"迟缓"） 请求验证</span><span class="sxs-lookup"><span data-stu-id="362ad-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="362ad-235">在 ASP.NET 4.5 中，默认情况下所有请求数据都将遵循请求验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="362ad-236">但是，你可以配置应用程序，以便将实际访问请求数据延迟请求验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="362ad-237">（这有时称为延迟请求验证，基于等延迟加载对于某些数据方案的术语。）你可以配置应用程序在 Web.config 文件中使用延迟的验证，通过设置*requestValidationMode*属性设为在 4.5 *httpRUntime*元素，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="362ad-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="362ad-238">在请求验证模式设置为 4.5，仅可用于特定请求值，而仅在你的代码访问该值时，才会触发请求验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="362ad-239">例如，如果你的代码获取的值的 Request.Form["forum\_文章"]，仅为该元素在窗体集合调用请求验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="362ad-240">中的其他元素的任何*窗体*集合进行验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="362ad-241">在以前版本的 ASP.NET，请求验证已访问集合中的任何元素时找不到整个请求触发。</span><span class="sxs-lookup"><span data-stu-id="362ad-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="362ad-242">新行为使容易一下不触发请求验证其他介质上的不同片段的请求数据的不同应用程序组件。</span><span class="sxs-lookup"><span data-stu-id="362ad-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="362ad-243">对未经过验证的请求的支持</span><span class="sxs-lookup"><span data-stu-id="362ad-243">Support for unvalidated requests</span></span>

<span data-ttu-id="362ad-244">单独的延迟的请求验证不解决此问题的有选择地绕过请求验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="362ad-245">Request.Form["forum 调用\_文章"] 仍触发器请求该特定请求值的验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="362ad-246">但是，你可能想要访问此字段不触发验证，因为你想要允许该字段中的标记。</span><span class="sxs-lookup"><span data-stu-id="362ad-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="362ad-247">若要做到这一点，ASP.NET 4.5 现在支持未经过验证的访问请求数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="362ad-248">ASP.NET 4.5 包括一个新*Unvalidated*集合属性中的*HttpRequest*类。</span><span class="sxs-lookup"><span data-stu-id="362ad-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="362ad-249">此集合提供访问所有请求数据的常见值如*窗体*， *QueryString*， *Cookie*，和*Url*。</span><span class="sxs-lookup"><span data-stu-id="362ad-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="362ad-250">使用论坛示例中，若要能够读取未经验证的请求数据，首先需要配置应用程序以使用新的请求验证模式：</span><span class="sxs-lookup"><span data-stu-id="362ad-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="362ad-251">然后，可以使用*HttpRequest.Unvalidated*要读取未经过验证的窗体值属性：</span><span class="sxs-lookup"><span data-stu-id="362ad-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> <span data-ttu-id="362ad-252">安全-*谨慎使用未经验证的请求数据 ！*</span><span class="sxs-lookup"><span data-stu-id="362ad-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="362ad-253">ASP.NET 4.5 增加的未经验证的请求属性和集合以使其更轻松地访问非常具体未经验证的请求数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="362ad-254">但是，你仍必须在原始请求数据，以确保危险的文本不呈现给用户来执行自定义验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="362ad-255">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="362ad-255">AntiXSS Library</span></span>

<span data-ttu-id="362ad-256">由于 Microsoft AntiXSS 库受欢迎程度，ASP.NET 4.5 现在集成了核心编码例程与库的版本 4.0。</span><span class="sxs-lookup"><span data-stu-id="362ad-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="362ad-257">由实现编码例程*AntiXssEncoder*在新的类型*System.Web.Security.AntiXss*命名空间。</span><span class="sxs-lookup"><span data-stu-id="362ad-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="362ad-258">你可以使用*AntiXssEncoder*直接通过调用静态的类型中实现的编码任何的方法类型。</span><span class="sxs-lookup"><span data-stu-id="362ad-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="362ad-259">但是，使用新的反 XSS 例程的最简单方法是配置 ASP.NET 应用程序使用*AntiXssEncoder*默认情况下的类。</span><span class="sxs-lookup"><span data-stu-id="362ad-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="362ad-260">若要执行此操作，请将以下属性添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="362ad-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="362ad-261">当*encoderType*属性设置为使用*AntiXssEncoder*类型，所有输出自动编码在 ASP.NET 中使用新的编码例程。</span><span class="sxs-lookup"><span data-stu-id="362ad-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="362ad-262">这些是已合并到 ASP.NET 4.5 的外部 AntiXSS 库的部分：</span><span class="sxs-lookup"><span data-stu-id="362ad-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="362ad-263">*HtmlEncode*， *HtmlFormUrlEncode*，和*HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="362ad-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="362ad-264">*XmlAttributeEncode*和*XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="362ad-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="362ad-265">*执行 UrlEncode*和*UrlPathEncode* （新）</span><span class="sxs-lookup"><span data-stu-id="362ad-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="362ad-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="362ad-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="362ad-267">Websocket 协议的支持</span><span class="sxs-lookup"><span data-stu-id="362ad-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="362ad-268">Websocket 协议是基于标准的定义如何通过 HTTP 建立客户端和服务器之间的安全、 实时双向通信的网络协议。</span><span class="sxs-lookup"><span data-stu-id="362ad-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="362ad-269">Microsoft 已经与 IETF 和 W3C 标准正文以帮助定义的协议。</span><span class="sxs-lookup"><span data-stu-id="362ad-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="362ad-270">与方面投入大量资源客户端和移动操作系统上支持 Websocket 协议的 Microsoft （而不仅仅是浏览器），任何客户端支持的 Websocket 协议。</span><span class="sxs-lookup"><span data-stu-id="362ad-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="362ad-271">Websocket 协议，使得可以更轻松地创建客户端和服务器之间的长时间运行的数据传输。</span><span class="sxs-lookup"><span data-stu-id="362ad-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="362ad-272">例如，编写的聊天应用程序是要容易得多的因为你可以建立 true 长时间运行连接客户端和服务器之间。</span><span class="sxs-lookup"><span data-stu-id="362ad-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="362ad-273">无需采用如定期轮询或 HTTP 长轮询来模拟套接字的行为的解决方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="362ad-274">ASP.NET 4.5 和 IIS 8 包括低级别的 Websocket 支持，使 ASP.NET 开发人员能够使用托管的 Api，用于以异步方式读取和 Websocket 对象上写入字符串和二进制数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="362ad-275">为 ASP.NET 4.5，新增了一个*System.Web.WebSockets*包含用于使用 Websocket 协议的类型的命名空间。</span><span class="sxs-lookup"><span data-stu-id="362ad-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="362ad-276">浏览器客户端通过创建一个 DOM 建立的 Websocket 连接*WebSocket*指向中 ASP.NET 应用程序，如以下示例所示的 URL 的对象：</span><span class="sxs-lookup"><span data-stu-id="362ad-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="362ad-277">你可以在 ASP.NET 中使用任何类型的模块或处理程序创建 Websocket 终结点。</span><span class="sxs-lookup"><span data-stu-id="362ad-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="362ad-278">在前面的示例中，使用.ashx 文件，因为.ashx 文件创建一个处理程序的快速方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="362ad-279">根据 Websocket 协议，ASP.NET 应用程序接受客户端的 Websocket 请求通过指示请求应通过 HTTP GET 请求升级到的 Websocket 请求。</span><span class="sxs-lookup"><span data-stu-id="362ad-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="362ad-280">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="362ad-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="362ad-281">*AcceptWebSocketRequest*方法接受一个函数委托，因为 ASP.NET 展开当前 HTTP 请求，然后将控件传输到的函数委托。</span><span class="sxs-lookup"><span data-stu-id="362ad-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="362ad-282">从概念上讲，此方法非常类似于你如何使用*计数*、 你在其中定义在哪个后台执行工作线程开始委托。</span><span class="sxs-lookup"><span data-stu-id="362ad-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="362ad-283">ASP.NET 和客户端已成功完成的 Websocket 握手后，ASP.NET 将调用委托和 Websocket 应用程序开始运行。</span><span class="sxs-lookup"><span data-stu-id="362ad-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="362ad-284">下面的代码示例演示一个简单的回显应用程序，在 ASP.NET 中使用内置的 Websocket 支持：</span><span class="sxs-lookup"><span data-stu-id="362ad-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="362ad-285">有关.NET 4.5 中的支持*await*关键字和基于任务的异步操作是天生适合对编写 Websocket 应用程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="362ad-286">代码示例演示在 ASP.NET 内完全以异步方式运行的 Websocket 请求。</span><span class="sxs-lookup"><span data-stu-id="362ad-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="362ad-287">在应用程序以异步方式等待要通过调用从客户端发送的消息*await 套接字。ReceiveAsync*。</span><span class="sxs-lookup"><span data-stu-id="362ad-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="362ad-288">同样，你可以将异步消息到客户端通过调用*await 套接字。SendAsync*。</span><span class="sxs-lookup"><span data-stu-id="362ad-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="362ad-289">在浏览器中，应用程序接收通过 Websocket 消息*onmessage*函数。</span><span class="sxs-lookup"><span data-stu-id="362ad-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="362ad-290">若要从浏览器发送消息，请调用*发送*方法*WebSocket* DOM 类型，如本示例中所示：</span><span class="sxs-lookup"><span data-stu-id="362ad-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="362ad-291">将来，我们可能会发布与此功能，抽象消失的低级别的编码，它一些需要在此版本中用于 Websocket 应用程序的更新。</span><span class="sxs-lookup"><span data-stu-id="362ad-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="362ad-292">绑定和缩减</span><span class="sxs-lookup"><span data-stu-id="362ad-292">Bundling and Minification</span></span>

<span data-ttu-id="362ad-293">绑定允许您将各个 JavaScript 和 CSS 文件合并到一个包，可以被视为单个文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="362ad-294">缩减将 JavaScript 和 CSS 文件集中删除空格和不需要的其他字符。</span><span class="sxs-lookup"><span data-stu-id="362ad-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="362ad-295">这些功能适用于 Web 窗体、 ASP.NET MVC 和 Web 页。</span><span class="sxs-lookup"><span data-stu-id="362ad-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="362ad-296">捆绑包是使用捆绑类或其子类，ScriptBundle 和 StyleBundle 之一创建的。</span><span class="sxs-lookup"><span data-stu-id="362ad-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="362ad-297">在配置后的捆绑包实例，捆绑包将提供给传入的请求通过只需将其添加到全局 BundleCollection 实例。</span><span class="sxs-lookup"><span data-stu-id="362ad-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="362ad-298">在默认模板中，捆绑包配置都被执行 BundleConfig 文件中。</span><span class="sxs-lookup"><span data-stu-id="362ad-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="362ad-299">此默认配置创建的核心脚本和 css 文件的模板使用所有的捆绑包。</span><span class="sxs-lookup"><span data-stu-id="362ad-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="362ad-300">捆绑包从内引用视图通过使用几个可能的帮助器方法之一。</span><span class="sxs-lookup"><span data-stu-id="362ad-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="362ad-301">为了支持呈现时在发布模式下与调试捆绑包的不同标记，ScriptBundle 和 StyleBundle 类具有呈现的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="362ad-302">如果处于调试模式，呈现器将生成捆绑中的每个资源的标记。</span><span class="sxs-lookup"><span data-stu-id="362ad-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="362ad-303">在发布模式下，呈现器将生成整个捆绑的单个标记元素。</span><span class="sxs-lookup"><span data-stu-id="362ad-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="362ad-304">切换之间调试和发布，可以通过如下所示修改 web.config 中的元素的调试属性实现模式：</span><span class="sxs-lookup"><span data-stu-id="362ad-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="362ad-305">此外，可以直接通过 BundleTable.EnableOptimizations 属性设置启用或禁用优化。</span><span class="sxs-lookup"><span data-stu-id="362ad-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="362ad-306">当文件会捆绑时，它们是首先按字母顺序排序 (中所显示的方式**解决方案资源管理器**)。</span><span class="sxs-lookup"><span data-stu-id="362ad-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="362ad-307">然后，它们进行组织，以便已知库和首先加载其自定义扩展 （如 jQuery、 MooTools 和 Dojo）。</span><span class="sxs-lookup"><span data-stu-id="362ad-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="362ad-308">例如，脚本文件夹如上所示的绑定的最终顺序将：</span><span class="sxs-lookup"><span data-stu-id="362ad-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="362ad-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="362ad-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="362ad-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="362ad-310">jquery-ui.js</span></span>
3. <span data-ttu-id="362ad-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="362ad-311">jquery.tools.js</span></span>
4. <span data-ttu-id="362ad-312">a.js</span><span class="sxs-lookup"><span data-stu-id="362ad-312">a.js</span></span>

<span data-ttu-id="362ad-313">CSS 文件也按字母顺序排序，然后重新组织以便 reset.css 和 normalize.css 之上的任何其他文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="362ad-314">最终排序的绑定上面所示的样式文件夹将为此：</span><span class="sxs-lookup"><span data-stu-id="362ad-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="362ad-315">reset.css</span><span class="sxs-lookup"><span data-stu-id="362ad-315">reset.css</span></span>
2. <span data-ttu-id="362ad-316">content.css</span><span class="sxs-lookup"><span data-stu-id="362ad-316">content.css</span></span>
3. <span data-ttu-id="362ad-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="362ad-317">forms.css</span></span>
4. <span data-ttu-id="362ad-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="362ad-318">globals.css</span></span>
5. <span data-ttu-id="362ad-319">menu.css</span><span class="sxs-lookup"><span data-stu-id="362ad-319">menu.css</span></span>
6. <span data-ttu-id="362ad-320">styles.css</span><span class="sxs-lookup"><span data-stu-id="362ad-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="362ad-321">用于 Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="362ad-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="362ad-322">.NET Framework 4.5 和 Windows 8 引入了可帮助您实现显著的性能提升为 web 服务器工作负荷的功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="362ad-323">这包括减少 （最多 35%) 在这两个启动时间和 web 托管使用 ASP.NET 站点上的内存需求量。</span><span class="sxs-lookup"><span data-stu-id="362ad-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="362ad-324">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="362ad-324">Key performance factors</span></span>

<span data-ttu-id="362ad-325">理想情况下，所有网站应都处于活动状态，并且在内存中以确保快速响应下一个请求，每当涉及。</span><span class="sxs-lookup"><span data-stu-id="362ad-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="362ad-326">可能会影响网站响应能力的因素包括：</span><span class="sxs-lookup"><span data-stu-id="362ad-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="362ad-327">要重新启动后应用程序池进行回收的站点所花费的时间。</span><span class="sxs-lookup"><span data-stu-id="362ad-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="362ad-328">这是以启动 web 服务器进程的站点的站点程序集不再在内存中时的时间。</span><span class="sxs-lookup"><span data-stu-id="362ad-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="362ad-329">（平台程序集是仍在内存中，因为它们由其他站点。）这种情况下被称为"冷站点暖 framework 启动"，或只是"冷站点启动。"</span><span class="sxs-lookup"><span data-stu-id="362ad-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="362ad-330">站点占用的内存量。</span><span class="sxs-lookup"><span data-stu-id="362ad-330">How much memory the site occupies.</span></span> <span data-ttu-id="362ad-331">此术语是"每个站点的内存使用情况"非共享工作集。"</span><span class="sxs-lookup"><span data-stu-id="362ad-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="362ad-332">新的性能改进专注于这两种因素。</span><span class="sxs-lookup"><span data-stu-id="362ad-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="362ad-333">新的性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="362ad-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="362ad-334">新功能的要求可以分为以下几类：</span><span class="sxs-lookup"><span data-stu-id="362ad-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="362ad-335">在.NET Framework 4 运行的改进。</span><span class="sxs-lookup"><span data-stu-id="362ad-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="362ad-336">需要.NET Framework 4.5，但可以在任何版本的 Windows 上运行的改进。</span><span class="sxs-lookup"><span data-stu-id="362ad-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="362ad-337">有只能与 Windows 8 上运行的.NET Framework 4.5 的改进。</span><span class="sxs-lookup"><span data-stu-id="362ad-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="362ad-338">性能会增加，你将能够启用的改进的每个级别。</span><span class="sxs-lookup"><span data-stu-id="362ad-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="362ad-339">一些.NET Framework 4.5 改进可利用的更广泛应用于其他方案，以及的性能功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="362ad-340">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="362ad-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="362ad-341">**要求**:.NET Framework 4 和 Visual Studio 11 开发者预览版 SDK</span><span class="sxs-lookup"><span data-stu-id="362ad-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="362ad-342">在服务器上的不同站点通常使用相同的帮助程序程序集 （例如，从初学者工具包或示例应用程序的程序集）。</span><span class="sxs-lookup"><span data-stu-id="362ad-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="362ad-343">每个站点有其自己的这些程序集副本在其 Bin 目录中。</span><span class="sxs-lookup"><span data-stu-id="362ad-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="362ad-344">即使的程序集的对象代码是相同的它们物理上独立的程序集，因此每个程序集必须在冷站点启动期间单独读取并单独保存在内存中。</span><span class="sxs-lookup"><span data-stu-id="362ad-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="362ad-345">新的 interning 功能解决了这种低效情况，并可减少内存需求和负载时间。</span><span class="sxs-lookup"><span data-stu-id="362ad-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="362ad-346">暂留可让 Windows 在文件系统中，来使每个程序集的单个副本和站点 Bin 文件夹中的单个程序集将替换对单个副本的符号链接。</span><span class="sxs-lookup"><span data-stu-id="362ad-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="362ad-347">如果单个站点时需要不同版本的程序集，符号链接替换为新版本的程序集，并仅该站点受到影响。</span><span class="sxs-lookup"><span data-stu-id="362ad-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="362ad-348">共享程序集使用符号链接，需要一个名为 aspnet 的新工具\_intern.exe，这样就可以创建和管理暂存的程序集的存储。</span><span class="sxs-lookup"><span data-stu-id="362ad-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="362ad-349">它提供作为 Visual Studio 11 开发人员预览版 SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="362ad-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="362ad-350">(但是，它将在仅安装.NET Framework 4，如果你已安装最新的系统上运行[更新](https://support.microsoft.com/kb/2468871)。)</span><span class="sxs-lookup"><span data-stu-id="362ad-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="362ad-351">若要确保所有符合条件的程序集具有已暂留，你可以运行 aspnet\_intern.exe 定期 （例如，每周一次作为计划任务）。</span><span class="sxs-lookup"><span data-stu-id="362ad-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="362ad-352">一个典型用途是，如下所示：</span><span class="sxs-lookup"><span data-stu-id="362ad-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="362ad-353">若要查看所有选项，请不带任何参数运行该工具。</span><span class="sxs-lookup"><span data-stu-id="362ad-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="362ad-354">用于启动速度更快的多核 JIT 编译</span><span class="sxs-lookup"><span data-stu-id="362ad-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="362ad-355">**要求**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="362ad-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="362ad-356">对于冷站点启动时，不仅能执行程序集具有要读取从磁盘，但的站点必须是 JIT 编译。</span><span class="sxs-lookup"><span data-stu-id="362ad-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="362ad-357">对于复杂的站点，这可以添加明显的延迟。</span><span class="sxs-lookup"><span data-stu-id="362ad-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="362ad-358">.NET Framework 4.5 中的新通用技术可减少这些延迟 JIT 编译分散可用处理器内核。</span><span class="sxs-lookup"><span data-stu-id="362ad-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="362ad-359">它尽可能多执行此操作并尽早使用期间收集的信息之前启动的站点。</span><span class="sxs-lookup"><span data-stu-id="362ad-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="362ad-360">由实现此功能[System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="362ad-361">JIT 编译的使用多个内核处于启用状态默认情况下，在 ASP.NET 中，因此不需要执行任何操作来利用此功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="362ad-362">如果你想要禁用此功能，请在 Web.config 文件中进行以下设置：</span><span class="sxs-lookup"><span data-stu-id="362ad-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="362ad-363">若要针对内存优化的优化垃圾回收</span><span class="sxs-lookup"><span data-stu-id="362ad-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="362ad-364">**要求**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="362ad-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="362ad-365">站点运行后，垃圾回收器 (GC) 堆其使用可以为其内存使用量的重要考虑因素。</span><span class="sxs-lookup"><span data-stu-id="362ad-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="362ad-366">任意垃圾回收器，如.NET Framework GC 使 CPU 时间 （频率和重要性的集合） 和内存消耗 （用于新的、 已释放，或可释放的对象的额外空间） 之间的折衷方案。</span><span class="sxs-lookup"><span data-stu-id="362ad-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="362ad-367">为以前版本中，我们提供指导如何配置以实现最佳平衡 GC (有关示例，请参阅[ASP.NET 2.0/3.5 共享承载配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。</span><span class="sxs-lookup"><span data-stu-id="362ad-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="362ad-368">.NET Framework 4.5，而不是多个独立设置，工作负荷定义配置设置可用，它将使所有以前建议的 GC 设置，以及新的优化，可提供有关每个站点的其他性能工作集。</span><span class="sxs-lookup"><span data-stu-id="362ad-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="362ad-369">若要启用优化的 GC 内存，请向 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="362ad-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="362ad-370">(如果你熟悉到 aspnet.config 更改的上一个指南，请注意，此设置将替代旧设置-例如，则不需要设置 gcServer、 gcConcurrent，等等。你无需删除旧的设置。）</span><span class="sxs-lookup"><span data-stu-id="362ad-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="362ad-371">预提取的 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="362ad-371">Prefetching for web applications</span></span>

<span data-ttu-id="362ad-372">**要求**: Windows 8 上运行的.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="362ad-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="362ad-373">Windows 具有几个版本包含一种技术称为[取](http://en.wikipedia.org/wiki/Prefetcher)可减少应用程序启动的磁盘读取成本。</span><span class="sxs-lookup"><span data-stu-id="362ad-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="362ad-374">因为冷启动客户端应用程序的主要问题，此技术尚未包含在 Windows Server 中，其中包括对 server 至关重要的组件。</span><span class="sxs-lookup"><span data-stu-id="362ad-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="362ad-375">预提取现已在 Windows Server，它可以在其中优化启动单独的网站的最新版本。</span><span class="sxs-lookup"><span data-stu-id="362ad-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="362ad-376">对于 Windows Server，在默认情况下不启用取。</span><span class="sxs-lookup"><span data-stu-id="362ad-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="362ad-377">若要启用和配置用于高密度 web 托管取，请在命令行运行以下命令集：</span><span class="sxs-lookup"><span data-stu-id="362ad-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="362ad-378">然后，为了与 ASP.NET 应用程序集成取，将以下代码添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="362ad-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="362ad-379">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="362ad-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="362ad-380">强类型化的数据控件</span><span class="sxs-lookup"><span data-stu-id="362ad-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="362ad-381">在 ASP.NET 4.5 Web 窗体包含用于使用数据的一些改进。</span><span class="sxs-lookup"><span data-stu-id="362ad-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="362ad-382">第一个改善是强类型化的数据控制。</span><span class="sxs-lookup"><span data-stu-id="362ad-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="362ad-383">对于在以前版本的 ASP.NET Web 窗体控件，显示数据绑定值使用*Eval*和数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="362ad-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="362ad-384">对于双向数据绑定，你使用*绑定*:</span><span class="sxs-lookup"><span data-stu-id="362ad-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="362ad-385">在运行时，这些调用使用反射来读取的指定成员的值，然后在标记中显示的结果。</span><span class="sxs-lookup"><span data-stu-id="362ad-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="362ad-386">这种方法轻松对任意、 unshaped 数据的数据绑定。</span><span class="sxs-lookup"><span data-stu-id="362ad-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="362ad-387">但是，这样的数据绑定表达式不支持 IntelliSense 等功能的成员名称、 导航 （例如转到定义） 或编译时检查这些名称。</span><span class="sxs-lookup"><span data-stu-id="362ad-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="362ad-388">若要解决此问题，ASP.NET 4.5，请添加了声明将控件绑定到的数据的数据类型的功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="362ad-389">执行此操作使用新*ItemType*属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="362ad-390">当设置此属性时，两个新的类型化的变量是否为数据绑定表达式的作用域中可用：*项*和*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="362ad-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="362ad-391">由于强类型化变量，你将获取 Visual Studio 开发体验的全部好处。</span><span class="sxs-lookup"><span data-stu-id="362ad-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>


<span data-ttu-id="362ad-392">对于双向数据绑定表达式中，使用*BindItem*变量：</span><span class="sxs-lookup"><span data-stu-id="362ad-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


<span data-ttu-id="362ad-393">支持数据绑定的 ASP.NET Web 窗体 framework 中的大多数控件已更新，以支持*ItemType*属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="362ad-394">模型绑定</span><span class="sxs-lookup"><span data-stu-id="362ad-394">Model Binding</span></span>

<span data-ttu-id="362ad-395">模型绑定扩展 ASP.NET Web 窗体控件中的数据绑定来使用代码为中心的数据访问。</span><span class="sxs-lookup"><span data-stu-id="362ad-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="362ad-396">它包含从概念*ObjectDataSource*控件和从 ASP.NET MVC 中的模型绑定。</span><span class="sxs-lookup"><span data-stu-id="362ad-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="362ad-397">选择数据</span><span class="sxs-lookup"><span data-stu-id="362ad-397">Selecting data</span></span>

<span data-ttu-id="362ad-398">若要配置一个数据控件要使用模型绑定来选择数据，你设置的控件的*SelectMethod*属性页的代码中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="362ad-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="362ad-399">数据控件在页生命周期中适当的时间调用的方法，并自动将绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="362ad-400">没有无需显式调用*DataBind*方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="362ad-401">在下面的示例中， *GridView*控件配置为使用一个名为方法*GetCategories*:</span><span class="sxs-lookup"><span data-stu-id="362ad-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="362ad-402">你创建*GetCategories*页的代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="362ad-403">对于简单的选择操作，该方法不需要参数，且应返回*IEnumerable*或*IQueryable*对象。</span><span class="sxs-lookup"><span data-stu-id="362ad-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="362ad-404">如果新*ItemType*设置属性 (它使强类型化数据绑定表达式下所述[强类型化数据控件](#_Toc318097386)更早版本)，这些接口的泛型版本应返回 — *IEnumerable&lt;T&gt;* 或*IQueryable&lt;T&gt;*，与*T*参数匹配的一种*ItemType*属性 (例如， *IQueryable&lt;类别&gt;*)。</span><span class="sxs-lookup"><span data-stu-id="362ad-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="362ad-405">下面的示例演示的代码*GetCategories*方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="362ad-406">此示例使用 Northwind 示例数据库使用 Entity Framework Code First 模型。</span><span class="sxs-lookup"><span data-stu-id="362ad-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="362ad-407">这段代码将确保查询返回通过每个类别的相关产品的详细信息*包括*方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="362ad-408">(这可确保*TemplateField*标记中的元素中显示的产品计数每个类别中，而无需[n + 1 选择](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)。)</span><span class="sxs-lookup"><span data-stu-id="362ad-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="362ad-409">当运行此页，则*GridView*控制调用*GetCategories*方法自动并呈现返回的数据使用的配置的字段：</span><span class="sxs-lookup"><span data-stu-id="362ad-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="362ad-410">因为选择方法将返回*IQueryable*对象， *GridView*控件可以在执行前进一步操作查询。</span><span class="sxs-lookup"><span data-stu-id="362ad-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="362ad-411">例如， *GridView*控件可以添加用于排序和分页到返回的查询表达式*IQueryable*对象之前执行，以便这些操作由基础执行LINQ 提供程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="362ad-412">在这种情况下，实体框架将确保在数据库中执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="362ad-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="362ad-413">下面的示例演示*GridView*控件修改，以便允许排序和分页：</span><span class="sxs-lookup"><span data-stu-id="362ad-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="362ad-414">现在页运行时，控件可确保，显示数据的当前页并按所选列进行排序：</span><span class="sxs-lookup"><span data-stu-id="362ad-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="362ad-415">若要筛选返回的数据，参数必须添加到选择的方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="362ad-416">这些参数将在运行时，模型绑定用来填充和可用于返回数据前更改查询。</span><span class="sxs-lookup"><span data-stu-id="362ad-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="362ad-417">例如，假设你想要让用户筛选器产品，通过在查询字符串中输入一个关键字。</span><span class="sxs-lookup"><span data-stu-id="362ad-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="362ad-418">你可以向方法添加参数，并更新代码以使用参数值：</span><span class="sxs-lookup"><span data-stu-id="362ad-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="362ad-419">此代码包括*其中*如果提供的值的表达式*关键字*然后返回查询结果。</span><span class="sxs-lookup"><span data-stu-id="362ad-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="362ad-420">值在提供程序</span><span class="sxs-lookup"><span data-stu-id="362ad-420">Value providers</span></span>

<span data-ttu-id="362ad-421">前面的示例不是有关在何处特定的值*关键字*来自参数。</span><span class="sxs-lookup"><span data-stu-id="362ad-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="362ad-422">若要指示此信息，可以使用参数属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="362ad-423">对于此示例中，你可以使用*QueryStringAttribute*中类*System.Web.ModelBinding*命名空间：</span><span class="sxs-lookup"><span data-stu-id="362ad-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="362ad-424">这会指示要尝试将值绑定到查询字符串中的模型绑定*关键字*在运行时的参数。</span><span class="sxs-lookup"><span data-stu-id="362ad-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="362ad-425">（这可能涉及执行类型转换，尽管它不在此情况下。）如果不能提供的值且不可为 null 的类型，是引发异常。</span><span class="sxs-lookup"><span data-stu-id="362ad-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="362ad-426">这些方法的值的源统称为值在提供程序，并指示要使用的值提供程序的参数属性统称为值提供程序属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="362ad-427">Web 窗体将包括在 Web 窗体应用程序，例如查询字符串、 cookie、 窗体值、 控件、 视图状态、 会话状态和配置文件属性的值在提供程序和所有用户输入的典型源的相应属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="362ad-428">你还可以编写自定义值在提供程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-428">You can also write custom value providers.</span></span>

<span data-ttu-id="362ad-429">默认情况下，参数名称用于作为键的值提供程序集合中查找一个值。</span><span class="sxs-lookup"><span data-stu-id="362ad-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="362ad-430">在示例中，代码将查找名为关键字的查询字符串值 (例如，~ / default.aspx?keyword=chef)。</span><span class="sxs-lookup"><span data-stu-id="362ad-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="362ad-431">你可以通过将它作为自变量传递给参数属性中指定的自定义密钥。</span><span class="sxs-lookup"><span data-stu-id="362ad-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="362ad-432">例如，若要使用名为 q 的查询字符串变量的值，无法执行此操作：</span><span class="sxs-lookup"><span data-stu-id="362ad-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="362ad-433">如果此方法在页的代码中，用户可以通过使用查询字符串的关键字筛选结果：</span><span class="sxs-lookup"><span data-stu-id="362ad-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="362ad-434">模型绑定可实现那些原本要进行手动编码的许多任务： 读取的值、 检查是否有 null 值，尝试将其转换为适当的类型，检查指示转换是否成功，和最后，使用中的值查询。</span><span class="sxs-lookup"><span data-stu-id="362ad-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="362ad-435">模型绑定结果，在更少代码和进行重复使用在整个应用程序的功能的能力。</span><span class="sxs-lookup"><span data-stu-id="362ad-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="362ad-436">筛选来自控件的值</span><span class="sxs-lookup"><span data-stu-id="362ad-436">Filtering by values from a control</span></span>

<span data-ttu-id="362ad-437">假设你想要扩展的示例，以使用户能够从下拉列表中选择一个筛选器值。</span><span class="sxs-lookup"><span data-stu-id="362ad-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="362ad-438">将下面的下拉列表添加到标记并将其配置为从另一个方法使用获取其数据*SelectMethod*属性：</span><span class="sxs-lookup"><span data-stu-id="362ad-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="362ad-439">通常还会添加*要*元素*GridView*控制，以便控件将显示一条消息，如果不找到任何匹配产品：</span><span class="sxs-lookup"><span data-stu-id="362ad-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="362ad-440">在网页代码中，将添加新选择的下拉列表的方法：</span><span class="sxs-lookup"><span data-stu-id="362ad-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="362ad-441">最后，更新*GetProducts*选择方法才能包含下拉列表从所选类别的 ID 的新参数：</span><span class="sxs-lookup"><span data-stu-id="362ad-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="362ad-442">现在页运行时，用户可以从下拉列表中，选择类别和*GridView*控件是自动显示经过筛选的数据重新绑定。</span><span class="sxs-lookup"><span data-stu-id="362ad-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="362ad-443">这可能是因为模型绑定跟踪选择方法的参数的值，并检测是否在回发后已更改任何参数值。</span><span class="sxs-lookup"><span data-stu-id="362ad-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="362ad-444">如果是这样，模型绑定强制关联的数据控件重新绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="362ad-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="362ad-445">HTML 编码数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="362ad-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="362ad-446">你可以现在进行 HTML 编码的数据绑定表达式的结果。</span><span class="sxs-lookup"><span data-stu-id="362ad-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="362ad-447">将一个冒号 （:） 添加到末尾&lt;%# 前缀将标记数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="362ad-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="362ad-448">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="362ad-448">Unobtrusive Validation</span></span>

<span data-ttu-id="362ad-449">你现在可以配置用于非介入式 JavaScript 进行客户端验证逻辑的内置的验证程序控件。</span><span class="sxs-lookup"><span data-stu-id="362ad-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="362ad-450">这显著缩短 JavaScript 呈现的页标记中的内联量，并减少总体的页大小。</span><span class="sxs-lookup"><span data-stu-id="362ad-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="362ad-451">你可以在以下任一方式来配置非介入式 JavaScript 的验证程序控件：</span><span class="sxs-lookup"><span data-stu-id="362ad-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="362ad-452">全局通过添加以下设置来 *&lt;appSettings&gt;*  Web.config 文件中的元素：</span><span class="sxs-lookup"><span data-stu-id="362ad-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="362ad-453">通过设置静态全局*System.Web.UI.ValidationSettings.UnobtrusiveValidationMode*属性*UnobtrusiveValidationMode.WebForms* (通常在*应用程序\_启动*Global.asax 文件中的方法)。</span><span class="sxs-lookup"><span data-stu-id="362ad-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="362ad-454">通过设置新的页为单独*UnobtrusiveValidationMode*属性*页*类到*UnobtrusiveValidationMode.WebForms*。</span><span class="sxs-lookup"><span data-stu-id="362ad-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="362ad-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="362ad-455">HTML5 Updates</span></span>

<span data-ttu-id="362ad-456">某些已得到改进 Web 窗体到服务器控件，若要利用的 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="362ad-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="362ad-457">*TextMode*属性*文本框中*已更新控件以支持如新的 HTML5 输入的类型*电子邮件*， *datetime*，和等等。</span><span class="sxs-lookup"><span data-stu-id="362ad-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="362ad-458">*FileUpload*控件现在支持多个文件上载从支持此 HTML5 功能的浏览器。</span><span class="sxs-lookup"><span data-stu-id="362ad-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="362ad-459">验证程序控制现在支持验证 HTML5 输入的元素。</span><span class="sxs-lookup"><span data-stu-id="362ad-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="362ad-460">具有现在表示 URL 的特性的新 HTML5 元素支持 runat ="server"。</span><span class="sxs-lookup"><span data-stu-id="362ad-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="362ad-461">因此，你愿意，可以使用 ASP.NET 约定 URL 路径中 ~ 运算符来表示应用程序根目录 (例如，&lt;视频 runat ="server"src="~/myVideo.wmv"/&gt;)。</span><span class="sxs-lookup"><span data-stu-id="362ad-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="362ad-462">*UpdatePanel*控件具有已固定的以便支持发布 HTML5 输入的字段。</span><span class="sxs-lookup"><span data-stu-id="362ad-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="362ad-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="362ad-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="362ad-464">ASP.NET MVC 4 Beta 现附带 Visual Studio 11 Beta。</span><span class="sxs-lookup"><span data-stu-id="362ad-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="362ad-465">ASP.NET MVC 是一个框架，用于开发高度可测试和可维护 Web 应用程序通过利用模型-视图-控制器 (MVC) 模式。</span><span class="sxs-lookup"><span data-stu-id="362ad-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="362ad-466">ASP.NET MVC 4 可以轻松地生成适用于移动 Web 应用程序，并包含 ASP.NET Web API，可帮助你生成可以访问任何设备的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="362ad-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="362ad-467">有关详细信息，请参阅[ASP.NET MVC 4 发行说明](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="362ad-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="362ad-468">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="362ad-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="362ad-469">新功能包括：</span><span class="sxs-lookup"><span data-stu-id="362ad-469">New features include the following:</span></span>

- <span data-ttu-id="362ad-470">新的和更新站点模板。</span><span class="sxs-lookup"><span data-stu-id="362ad-470">New and updated site templates.</span></span>
- <span data-ttu-id="362ad-471">添加服务器端和客户端验证使用*验证*帮助器。</span><span class="sxs-lookup"><span data-stu-id="362ad-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="362ad-472">注册脚本使用资产管理器的能力。</span><span class="sxs-lookup"><span data-stu-id="362ad-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="362ad-473">启用从 Facebook 和其他站点使用 OAuth 和 OpenID 登录名。</span><span class="sxs-lookup"><span data-stu-id="362ad-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="362ad-474">使用添加图*映射*帮助器。</span><span class="sxs-lookup"><span data-stu-id="362ad-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="362ad-475">运行 Web 页面应用程序的并行。</span><span class="sxs-lookup"><span data-stu-id="362ad-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="362ad-476">移动设备的呈现页。</span><span class="sxs-lookup"><span data-stu-id="362ad-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="362ad-477">有关这些功能和整页的代码示例的详细信息，请参阅[顶部功能网页 2 beta](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="362ad-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="362ad-478">Visual Web Developer 11 Beta</span><span class="sxs-lookup"><span data-stu-id="362ad-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="362ad-479">本部分提供有关在 Visual Web Developer 11 Beta 和 Visual Studio 2012 候选发布版本中的 web 开发的改进的信息。</span><span class="sxs-lookup"><span data-stu-id="362ad-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="362ad-480">Visual Studio 2010 和 Visual Studio 2012 候选发布版本 （项目兼容性） 之间共享的项目</span><span class="sxs-lookup"><span data-stu-id="362ad-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="362ad-481">Visual Studio 2012 候选发布版本，直到在较新版本的 Visual Studio 中打开现有项目启动转换向导。</span><span class="sxs-lookup"><span data-stu-id="362ad-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="362ad-482">这为未向后兼容的新格式强制升级的内容 （资产） 的项目和解决方案。</span><span class="sxs-lookup"><span data-stu-id="362ad-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="362ad-483">因此，在转换后你无法打开该项目中较旧版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="362ad-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="362ad-484">许多客户告诉我们这不是适当的方法。</span><span class="sxs-lookup"><span data-stu-id="362ad-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="362ad-485">在 Visual Studio 11 Beta，我们现在支持共享的项目和解决方案与 Visual Studio 2010 SP1。</span><span class="sxs-lookup"><span data-stu-id="362ad-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="362ad-486">这意味着，如果你在 Visual Studio 2012 候选发布版本中打开 2010年项目，你仍将能够在 Visual Studio 2010 SP1 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="362ad-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="362ad-487">Visual Studio 2010 SP1 和 Visual Studio 2012 候选发布版本之间无法共享几种类型的项目。</span><span class="sxs-lookup"><span data-stu-id="362ad-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="362ad-488">这些包括一些 （如 ASP.NET MVC 2 项目） 的较旧项目 （如安装程序项目） 的特殊用途。</span><span class="sxs-lookup"><span data-stu-id="362ad-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="362ad-489">在 Visual Studio 11 Beta 中首次打开 Visual Studio 2010 SP1 Web 项目时，以下属性添加到项目文件：</span><span class="sxs-lookup"><span data-stu-id="362ad-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="362ad-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="362ad-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="362ad-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="362ad-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="362ad-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="362ad-492">OldToolsVersion</span></span>
- <span data-ttu-id="362ad-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="362ad-493">VisualStudioVersion</span></span>
- <span data-ttu-id="362ad-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="362ad-494">VSToolsPath</span></span>

<span data-ttu-id="362ad-495">升级项目文件的过程使用 FileUpgradeFlags、 UpgradeBackupLocation 和 OldToolsVersion。</span><span class="sxs-lookup"><span data-stu-id="362ad-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="362ad-496">它们会产生任何影响使用 Visual Studio 2010 中的项目。</span><span class="sxs-lookup"><span data-stu-id="362ad-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="362ad-497">VisualStudioVersion 是使用 MSBuild 4.5，该值指示当前项目的版本的 Visual Studio 的一个新属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="362ad-498">因为此属性没有在 MSBuild 4.0 （Visual Studio 2010 SP1 使用的 MSBuild 的版本） 中，我们将默认值插入项目文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="362ad-499">VSToolsPath 属性用于确定正确的.targets 文件以导入从 MSBuildExtensionsPath32 设置所表示的路径。</span><span class="sxs-lookup"><span data-stu-id="362ad-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="362ad-500">也有一些与导入元素相关的更改。</span><span class="sxs-lookup"><span data-stu-id="362ad-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="362ad-501">这些更改是为了支持这两个版本的 Visual Studio 之间的兼容性必需的。</span><span class="sxs-lookup"><span data-stu-id="362ad-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="362ad-502">如果项目 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之间两个不同的计算机上，共享的并且该项目包括在应用程序的本地数据库\_数据文件夹，你必须确保使用的数据库的 SQL Server 的版本是在这两台计算机上安装。</span><span class="sxs-lookup"><span data-stu-id="362ad-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="362ad-503">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="362ad-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="362ad-504">为默认值进行了以下更改*Web.config*在 Visual Studio 2012 候选发布版本中使用的网站模板创建的网站文件：</span><span class="sxs-lookup"><span data-stu-id="362ad-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="362ad-505">在`<httpRuntime>`元素，`encoderType`属性现在设置默认情况下，若要使用已添加到 ASP.NET AntiXSS 类型。</span><span class="sxs-lookup"><span data-stu-id="362ad-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="362ad-506">有关详细信息，请参阅[AntiXSS 库](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="362ad-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="362ad-507">另外，请在`<httpRuntime>`元素，`requestValidationMode`属性设置为"4.5"。</span><span class="sxs-lookup"><span data-stu-id="362ad-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="362ad-508">这意味着默认情况下，请求验证配置为使用延迟的 （"迟缓"） 验证。</span><span class="sxs-lookup"><span data-stu-id="362ad-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="362ad-509">有关详细信息，请参阅[新的 ASP.NET 请求验证功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="362ad-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="362ad-510">`<modules>`元素`<system.webServer>`部分不包含`runAllManagedModulesForAllRequests`属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="362ad-511">（其默认值为 false）这意味着，如果你使用的 IIS 7 且尚未更新到 SP1 的版本，你可能具有与新站点中的路由的问题。</span><span class="sxs-lookup"><span data-stu-id="362ad-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="362ad-512">有关详细信息，请参阅[在 IIS 7 ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="362ad-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="362ad-513">这些更改不会影响现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="362ad-514">但是，它们可能表示现有的网站和为 ASP.NET 4.5 使用新的模板创建的新网站之间的行为差异。</span><span class="sxs-lookup"><span data-stu-id="362ad-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="362ad-515">在 IIS 7 ASP.NET 路由中的本机支持</span><span class="sxs-lookup"><span data-stu-id="362ad-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="362ad-516">这不是 ASP.NET 的更改在这种情况下，但如果你正在尚未应用 SP1 更新的 IIS 7 的版本会影响你的新网站项目的模板中的更改。</span><span class="sxs-lookup"><span data-stu-id="362ad-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="362ad-517">在 ASP.NET 中，你可以将以下配置设置添加到应用程序以支持路由：</span><span class="sxs-lookup"><span data-stu-id="362ad-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="362ad-518">时**runAllManagedModulesForAllRequests**是 true，如 URL`http://mysite/myapp/home`就会转到 ASP.NET，即使没有任何 *.aspx*， *.mvc*，或类似的扩展名URL。</span><span class="sxs-lookup"><span data-stu-id="362ad-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="362ad-519">IIS 7，已更新使**runAllManagedModulesForAllRequests**设置不必要和支持 ASP.NET 本机路由。</span><span class="sxs-lookup"><span data-stu-id="362ad-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="362ad-520">(有关更新的信息，请参阅 Microsoft 支持文章[有可用启用某些 IIS 7.0 或 IIS 7.5 的处理程序，来处理请求其 Url 不要以句点结尾的更新](https://support.microsoft.com/kb/980368)。)</span><span class="sxs-lookup"><span data-stu-id="362ad-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="362ad-521">如果在 IIS 7 上运行你的网站和 IIS 已更新，如果你不需要设置**runAllManagedModulesForAllRequests**为 true。</span><span class="sxs-lookup"><span data-stu-id="362ad-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="362ad-522">事实上，将其设置为 true 不是建议，因为它会不必要的处理开销到请求。</span><span class="sxs-lookup"><span data-stu-id="362ad-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="362ad-523">当此设置为 true 时，所有请求，包括 *.htm*， *.jpg*，和其他静态文件，也需要通过 ASP.NET 请求管道。</span><span class="sxs-lookup"><span data-stu-id="362ad-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="362ad-524">如果创建新的 ASP.NET 4.5 网站，以使用 Visual Studio 2012 RC 中提供的模板时，该网站的配置不包括**runAllManagedModulesForAllRequests**设置。</span><span class="sxs-lookup"><span data-stu-id="362ad-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="362ad-525">这意味着默认情况下设置为 false。</span><span class="sxs-lookup"><span data-stu-id="362ad-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="362ad-526">然后，如果你运行的网站在 Windows 7 上没有安装 SP1 的情况下，IIS 7 将不包含所需的更新。</span><span class="sxs-lookup"><span data-stu-id="362ad-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="362ad-527">因此，路由无法工作，你将看到错误。</span><span class="sxs-lookup"><span data-stu-id="362ad-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="362ad-528">如果你有问题，其中路由不起作用，可以执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="362ad-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="362ad-529">更新到 SP1，会将更新添加到 IIS 7 的 Windows 7。</span><span class="sxs-lookup"><span data-stu-id="362ad-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="362ad-530">安装前面列出的 Microsoft 支持文章中所述的更新。</span><span class="sxs-lookup"><span data-stu-id="362ad-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="362ad-531">设置**runAllManagedModulesForAllRequests**为 true，该网站的 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="362ad-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="362ad-532">请注意，这将向请求添加一些开销。</span><span class="sxs-lookup"><span data-stu-id="362ad-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="362ad-533">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="362ad-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="362ad-534">智能任务</span><span class="sxs-lookup"><span data-stu-id="362ad-534">Smart Tasks</span></span>

<span data-ttu-id="362ad-535">在设计视图中，复杂属性的服务器控件通常具有关联的对话框和向导，以便可以方便地设置它们。</span><span class="sxs-lookup"><span data-stu-id="362ad-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="362ad-536">例如，可以使用特殊的对话框中添加到数据源*中继器*控制或将列添加到*GridView*控件。</span><span class="sxs-lookup"><span data-stu-id="362ad-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="362ad-537">但是，这种类型的复杂属性的 UI 帮助尚未在源视图中可用。</span><span class="sxs-lookup"><span data-stu-id="362ad-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="362ad-538">因此，Visual Studio 11 引入了源视图的智能任务。</span><span class="sxs-lookup"><span data-stu-id="362ad-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="362ad-539">智能任务是在 C# 和 Visual Basic 编辑器的常用功能的上下文感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="362ad-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="362ad-540">对于 ASP.NET Web 窗体控件，智能任务在上显示服务器标记为小型的标志符号时插入点位于元素内：</span><span class="sxs-lookup"><span data-stu-id="362ad-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="362ad-541">在你单击的标志符号或按 CTRL + 的扩展智能任务。</span><span class="sxs-lookup"><span data-stu-id="362ad-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="362ad-542">（点），代码编辑器中一样。</span><span class="sxs-lookup"><span data-stu-id="362ad-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="362ad-543">然后，它将显示类似于设计视图中的智能任务的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="362ad-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="362ad-544">例如，智能任务在上图中显示的 GridView 任务选项。</span><span class="sxs-lookup"><span data-stu-id="362ad-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="362ad-545">如果选择编辑列，将显示以下对话框中：</span><span class="sxs-lookup"><span data-stu-id="362ad-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="362ad-546">填写对话框设置相同的属性可以设置在设计视图中。</span><span class="sxs-lookup"><span data-stu-id="362ad-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="362ad-547">当你单击确定时，会随新的设置更新控件的标记：</span><span class="sxs-lookup"><span data-stu-id="362ad-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="362ad-548">WAI ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-548">WAI-ARIA support</span></span>

<span data-ttu-id="362ad-549">编写可访问的网站变得越来越重要。</span><span class="sxs-lookup"><span data-stu-id="362ad-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="362ad-550">[WAI ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义开发人员编写可访问的网站的方式。</span><span class="sxs-lookup"><span data-stu-id="362ad-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="362ad-551">在 Visual Studio 中现在完全支持此标准。</span><span class="sxs-lookup"><span data-stu-id="362ad-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="362ad-552">例如，*角色*属性现在具有完整的 IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="362ad-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="362ad-553">WAI ARIA 标准还引入了带有前缀的特性*aria-* 能够让你将语义添加到 HTML5 文档。</span><span class="sxs-lookup"><span data-stu-id="362ad-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="362ad-554">Visual Studio 还完全支持这些*aria-* 属性：</span><span class="sxs-lookup"><span data-stu-id="362ad-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="362ad-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="362ad-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="362ad-556">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="362ad-556">New HTML5 snippets</span></span>

<span data-ttu-id="362ad-557">若要使其更快且更易于编写常用的 HTML5 标记，Visual Studio 提供了大量的代码段。</span><span class="sxs-lookup"><span data-stu-id="362ad-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="362ad-558">视频段是一个示例：</span><span class="sxs-lookup"><span data-stu-id="362ad-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="362ad-559">调用代码段，请按 tab 键两次时在 IntelliSense 中选择了该元素：</span><span class="sxs-lookup"><span data-stu-id="362ad-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="362ad-560">这将生成你可以自定义代码段。</span><span class="sxs-lookup"><span data-stu-id="362ad-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="362ad-561">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="362ad-561">Extract to user control</span></span>

<span data-ttu-id="362ad-562">在大型网页中，它可以将各个部分移到用户控件的一个好办法。</span><span class="sxs-lookup"><span data-stu-id="362ad-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="362ad-563">这种形式的重构有助于提高页的可读性，并可以简化页结构。</span><span class="sxs-lookup"><span data-stu-id="362ad-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="362ad-564">若要简化此过程，当您编辑在源视图中的 Web 窗体页面时，你可以现在在页中选择文本，右键单击它，，然后选择提取到用户控件：</span><span class="sxs-lookup"><span data-stu-id="362ad-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="362ad-565">在属性中的代码而有价值的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="362ad-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="362ad-566">Visual Studio 始终提供的任何页面或控件中的服务器端代码而有价值的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="362ad-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="362ad-567">现在 Visual Studio 包括 IntelliSense 中以及 HTML 特性的代码而有价值。</span><span class="sxs-lookup"><span data-stu-id="362ad-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="362ad-568">这使得更轻松地创建数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="362ad-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="362ad-569">当你重命名一个开始标记或结束标记时匹配标记的自动重命名</span><span class="sxs-lookup"><span data-stu-id="362ad-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="362ad-570">如果重命名的 HTML 元素 (例如，更改*div*标记要*标头*标记)，则相应的打开或关闭标记也会更改实时。</span><span class="sxs-lookup"><span data-stu-id="362ad-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="362ad-571">这有助于避免忘记更改结束标记或更改的错误的一个错误。</span><span class="sxs-lookup"><span data-stu-id="362ad-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="362ad-572">事件处理程序生成</span><span class="sxs-lookup"><span data-stu-id="362ad-572">Event handler generation</span></span>

<span data-ttu-id="362ad-573">Visual Studio 现在包含在源视图来帮助你编写事件处理程序并手动将其绑定中的功能。</span><span class="sxs-lookup"><span data-stu-id="362ad-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="362ad-574">如果你正在编辑源视图中的事件名称，IntelliSense 将显示&lt;创建新事件&gt;，这将创建一个事件处理程序页的代码中包含正确的签名：</span><span class="sxs-lookup"><span data-stu-id="362ad-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="362ad-575">默认情况下，事件处理程序将使用控件的 ID，用于事件处理方法的名称：</span><span class="sxs-lookup"><span data-stu-id="362ad-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="362ad-576">生成的事件处理程序将如下所示 （在这种情况下，在 C# 中）：</span><span class="sxs-lookup"><span data-stu-id="362ad-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="362ad-577">智能缩进</span><span class="sxs-lookup"><span data-stu-id="362ad-577">Smart indent</span></span>

<span data-ttu-id="362ad-578">按 enter 键空 HTML 元素中的时，编辑器将将插入点放在正确的位置：</span><span class="sxs-lookup"><span data-stu-id="362ad-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="362ad-579">如果按 enter 键，在此位置，结束标记是向下移动和缩进以匹配的开始标记。</span><span class="sxs-lookup"><span data-stu-id="362ad-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="362ad-580">插入点还缩进：</span><span class="sxs-lookup"><span data-stu-id="362ad-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="362ad-581">自动减少语句结束</span><span class="sxs-lookup"><span data-stu-id="362ad-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="362ad-582">Visual Studio 现在筛选器基于，使其显示仅相关选项输入的内容中的 IntelliSense 列表：</span><span class="sxs-lookup"><span data-stu-id="362ad-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="362ad-583">IntelliSense 还筛选器基于的智能感知列表中的各单词的词首字母大写。</span><span class="sxs-lookup"><span data-stu-id="362ad-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="362ad-584">例如，如果键入"dl"，dl 和 asp: DataList 显示：</span><span class="sxs-lookup"><span data-stu-id="362ad-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="362ad-585">此功能可以更快地获取已知元素的语句结束。</span><span class="sxs-lookup"><span data-stu-id="362ad-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="362ad-586">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="362ad-586">JavaScript Editor</span></span>

<span data-ttu-id="362ad-587">Visual Studio 2012 候选发布版本中的 JavaScript 编辑器是全新并极大地改善了使用 Visual Studio 中的 JavaScript 的体验。</span><span class="sxs-lookup"><span data-stu-id="362ad-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="362ad-588">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="362ad-588">Code outlining</span></span>

<span data-ttu-id="362ad-589">大纲区域，现在将自动创建适用于所有功能，从而可以折叠不可与你当前焦点相关的文件部分。</span><span class="sxs-lookup"><span data-stu-id="362ad-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="362ad-590">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="362ad-590">Brace matching</span></span>

<span data-ttu-id="362ad-591">将插入点放在一个开始标记或右大括号后，编辑器突出显示匹配的一个。</span><span class="sxs-lookup"><span data-stu-id="362ad-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="362ad-592">转到定义</span><span class="sxs-lookup"><span data-stu-id="362ad-592">Go to Definition</span></span>

<span data-ttu-id="362ad-593">转到定义命令，可以跳转到函数或变量的源。</span><span class="sxs-lookup"><span data-stu-id="362ad-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="362ad-594">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-594">ECMAScript5 support</span></span>

<span data-ttu-id="362ad-595">编辑器在 ECMAScript5，描述 JavaScript 语言的标准的最新版本中支持的新语法和 Api。</span><span class="sxs-lookup"><span data-stu-id="362ad-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="362ad-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="362ad-596">DOM IntelliSense</span></span>

<span data-ttu-id="362ad-597">DOM Api 的 IntelliSense 得到了提高，支持的许多新 HTML5 Api 包括与*querySelector*，DOM 存储，跨文档消息传递，和*画布*。</span><span class="sxs-lookup"><span data-stu-id="362ad-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="362ad-598">按一个单一的简单 JavaScript 文件，而不是本机类型库定义现在驱动 DOM IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="362ad-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="362ad-599">这使得容易扩展或替换。</span><span class="sxs-lookup"><span data-stu-id="362ad-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="362ad-600">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="362ad-600">VSDOC signature overloads</span></span>

<span data-ttu-id="362ad-601">详细的 IntelliSense 注释现在为 JavaScript 函数的单独重载使用新的声明*&lt;签名&gt;* 元素，如本示例中所示：</span><span class="sxs-lookup"><span data-stu-id="362ad-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="362ad-602">隐式引用</span><span class="sxs-lookup"><span data-stu-id="362ad-602">Implicit references</span></span>

<span data-ttu-id="362ad-603">你现在可以将 JavaScript 文件添加到将隐式包含在文件列表中，任何给定的 JavaScript 文件或块的引用，这意味着，你将获得 IntelliSense 其内容的中央列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="362ad-604">例如，可以将 jQuery 文件添加到中央列表的文件，并且你将获取 IntelliSense jQuery 函数在文件中，任何 JavaScript 块是否已显式引用它 (使用 / /&lt;引用 /&gt;) 或不。</span><span class="sxs-lookup"><span data-stu-id="362ad-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="362ad-605">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="362ad-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="362ad-606">自动减少语句结束</span><span class="sxs-lookup"><span data-stu-id="362ad-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="362ad-607">用于 CSS 现在筛选器基于的 CSS 属性和所选架构支持的值的智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="362ad-608">IntelliSense 还支持标题大小写搜索：</span><span class="sxs-lookup"><span data-stu-id="362ad-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="362ad-609">分层缩进</span><span class="sxs-lookup"><span data-stu-id="362ad-609">Hierarchical indentation</span></span>

<span data-ttu-id="362ad-610">CSS 编辑器用于缩进显示层次结构的规则，这为你提供的级联的规则的逻辑上组织方式概述。</span><span class="sxs-lookup"><span data-stu-id="362ad-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="362ad-611">在下面的示例中，#list 选择器级联子级的列表，并且因此缩进。</span><span class="sxs-lookup"><span data-stu-id="362ad-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="362ad-612">下面的示例演示更复杂的继承：</span><span class="sxs-lookup"><span data-stu-id="362ad-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="362ad-613">由其父规则确定的规则的缩进。</span><span class="sxs-lookup"><span data-stu-id="362ad-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="362ad-614">默认情况下，启用分层缩进，但你可以禁用它 （工具，从菜单栏中的选项） 选项对话框：</span><span class="sxs-lookup"><span data-stu-id="362ad-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="362ad-615">CSS hacks 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-615">CSS hacks support</span></span>

<span data-ttu-id="362ad-616">数百个真实世界 CSS 文件分析显示 CSS 黑客攻击是很常见，并且 Visual Studio 现在支持使用最广泛的。</span><span class="sxs-lookup"><span data-stu-id="362ad-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="362ad-617">这种支持包括 IntelliSense 和验证在星型 (\*) 和下划线 (\_) 属性黑客攻击：</span><span class="sxs-lookup"><span data-stu-id="362ad-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="362ad-618">典型的选择器黑客攻击也支持以便即使在它们应用维护分层缩进。</span><span class="sxs-lookup"><span data-stu-id="362ad-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="362ad-619">用于对目标 Internet Explorer 7 典型的选择器 hack 是前面附加与选择器 *\*： 第一个子级 + html*。</span><span class="sxs-lookup"><span data-stu-id="362ad-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="362ad-620">使用该规则将维护的分层缩进：</span><span class="sxs-lookup"><span data-stu-id="362ad-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="362ad-621">供应商特定架构 (-moz--webkit)</span><span class="sxs-lookup"><span data-stu-id="362ad-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="362ad-622">CSS3 引入了在不同时间由不同的浏览器实现的许多属性。</span><span class="sxs-lookup"><span data-stu-id="362ad-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="362ad-623">以前，这使用特定于供应商的语法通过强制为特定浏览器的代码的开发人员。</span><span class="sxs-lookup"><span data-stu-id="362ad-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="362ad-624">这些浏览器特定属性现在包含在 IntelliSense 中。</span><span class="sxs-lookup"><span data-stu-id="362ad-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="362ad-625">注释和 uncommenting 支持</span><span class="sxs-lookup"><span data-stu-id="362ad-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="362ad-626">现在，你可以注释，并取消注释使用代码编辑器 (Ctrl + K、 注释的 C 和 Ctrl + K，你可以取消注释） 中使用的同一个快捷方式的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="362ad-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="362ad-627">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="362ad-627">Color picker</span></span>

<span data-ttu-id="362ad-628">在以前版本的 Visual Studio 中，与颜色相关的属性的智能感知功能包括命名的颜色值的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="362ad-629">全功能颜色选取器已替换为该列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="362ad-630">当你输入颜色值时，颜色选取器会自动显示，并显示以前用过跟默认颜色调色板的颜色的列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="362ad-631">你可以选择使用鼠标或键盘的颜色。</span><span class="sxs-lookup"><span data-stu-id="362ad-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="362ad-632">列表可以扩展到完成颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="362ad-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="362ad-633">选取器，可通过自动将任何颜色转换 RGBA 时移动的不透明度滑块来控制 alpha 通道：</span><span class="sxs-lookup"><span data-stu-id="362ad-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="362ad-634">代码段</span><span class="sxs-lookup"><span data-stu-id="362ad-634">Snippets</span></span>

<span data-ttu-id="362ad-635">CSS 编辑器中的代码段使其更加容易和快速创建跨浏览器样式。</span><span class="sxs-lookup"><span data-stu-id="362ad-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="362ad-636">需要特定于浏览器的设置的许多 CSS3 属性现在已回滚到代码段。</span><span class="sxs-lookup"><span data-stu-id="362ad-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="362ad-637">CSS 代码段支持高级的方案 （如 CSS3 媒体查询），通过键入在符号 (@)，其中说明了智能感知列表。</span><span class="sxs-lookup"><span data-stu-id="362ad-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="362ad-638">当选择@media值并按 tab 键，CSS 编辑器将插入以下代码段：</span><span class="sxs-lookup"><span data-stu-id="362ad-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="362ad-639">与代码段，你可以创建自己的 CSS 代码段。</span><span class="sxs-lookup"><span data-stu-id="362ad-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="362ad-640">自定义区域</span><span class="sxs-lookup"><span data-stu-id="362ad-640">Custom regions</span></span>

<span data-ttu-id="362ad-641">名为代码区域，在已经可用在代码编辑器中，现可用于编辑 CSS。</span><span class="sxs-lookup"><span data-stu-id="362ad-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="362ad-642">这样可以轻松地分组相关的样式块。</span><span class="sxs-lookup"><span data-stu-id="362ad-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="362ad-643">当区域处于折叠状态时将显示区域的名称：</span><span class="sxs-lookup"><span data-stu-id="362ad-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="362ad-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="362ad-644">Page Inspector</span></span>

<span data-ttu-id="362ad-645">Page Inspector 是一种工具，可以呈现网页 （HTML、 Web 窗体、 ASP.NET MVC 或网页） 在 Visual Studio IDE 中，并允许您检查源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="362ad-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="362ad-646">适用于 ASP.NET 页中，Page Inspector 可让你确定哪些服务器端代码生成到浏览器呈现的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="362ad-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="362ad-647">有关 Page Inspector 的详细信息，请参阅以下教程：</span><span class="sxs-lookup"><span data-stu-id="362ad-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="362ad-648">使用 Page Inspector 中[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="362ad-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="362ad-649">使用 Page Inspector 中[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span><span class="sxs-lookup"><span data-stu-id="362ad-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="362ad-650">发布</span><span class="sxs-lookup"><span data-stu-id="362ad-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="362ad-651">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="362ad-651">Publish profiles</span></span>

<span data-ttu-id="362ad-652">在 Visual Studio 2010 中，对于 Web 应用程序项目的发布信息不会存储在版本控制而不是与其他人共享。</span><span class="sxs-lookup"><span data-stu-id="362ad-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="362ad-653">Visual Studio 2012 候选发布版本中，已更改的发布配置文件的格式。</span><span class="sxs-lookup"><span data-stu-id="362ad-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="362ad-654">已经过一个团队项目，并且现在可以轻松地从基于 MSBuild 的生成使用。</span><span class="sxs-lookup"><span data-stu-id="362ad-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="362ad-655">生成配置信息位于发布对话框中，以便您可以轻松地切换在发布前的生成配置。</span><span class="sxs-lookup"><span data-stu-id="362ad-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="362ad-656">发布配置文件将存储在 PublishProfiles 文件夹。</span><span class="sxs-lookup"><span data-stu-id="362ad-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="362ad-657">文件夹的位置取决于你正在使用哪种编程语言：</span><span class="sxs-lookup"><span data-stu-id="362ad-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="362ad-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="362ad-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="362ad-659">Visual Basic： 我 Project\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="362ad-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="362ad-660">每个配置文件是一个 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="362ad-661">在发布期间，此文件将导入项目的 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="362ad-662">在 Visual Studio 2010 中，如果你想要更改发布或包过程中，则必须将你的自定义放入名为的文件**ProjectName**。 wpp.targets。</span><span class="sxs-lookup"><span data-stu-id="362ad-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="362ad-663">仍支持此行为，但现在可以将你的自定义放入发布配置文件本身。</span><span class="sxs-lookup"><span data-stu-id="362ad-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="362ad-664">这样一来，将仅对该配置文件使用自定义项。</span><span class="sxs-lookup"><span data-stu-id="362ad-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="362ad-665">你可以现在还利用发布配置文件，从 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="362ad-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="362ad-666">为此，请使用以下命令生成项目时：</span><span class="sxs-lookup"><span data-stu-id="362ad-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="362ad-667">Project.csproj 值是从项目的路径，ProfileName 是要发布的配置文件的名称。</span><span class="sxs-lookup"><span data-stu-id="362ad-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="362ad-668">或者，而不是传递的配置文件名称*PublishProfile*属性，您可以传入的完整路径到发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="362ad-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="362ad-669">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="362ad-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="362ad-670">对于 Web 应用程序项目，Visual Studio 2012 候选发布版本中添加一个可用于预编译和合并发布时的站点的内容或包项目的打包/发布 Web 属性页上的选项。</span><span class="sxs-lookup"><span data-stu-id="362ad-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="362ad-671">若要查看这些选项，用鼠标右键单击解决方案资源管理器中的项目，选择属性，然后选择打包/发布 Web 属性页。</span><span class="sxs-lookup"><span data-stu-id="362ad-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="362ad-672">下图显示 Precompile 此应用程序，然后发布选项。</span><span class="sxs-lookup"><span data-stu-id="362ad-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="362ad-673">选中此选项后，Visual Studio 预编译的应用程序每次您发布或打包 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="362ad-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="362ad-674">如果你想要控制如何预编译站点或如何合并程序集，请单击高级按钮以配置这些选项。</span><span class="sxs-lookup"><span data-stu-id="362ad-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="362ad-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="362ad-675">IIS Express</span></span>

<span data-ttu-id="362ad-676">在 Visual Studio 中的测试 web 项目的默认 web 服务器现在是 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="362ad-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="362ad-677">Visual Studio 开发服务器仍是本地 web 服务器在开发期间，一个选项，但 IIS Express 现在是建议的服务器。</span><span class="sxs-lookup"><span data-stu-id="362ad-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="362ad-678">在 Visual Studio 11 Beta 中使用 IIS Express 的体验是非常类似于使用 Visual Studio 2010 SP1 中。</span><span class="sxs-lookup"><span data-stu-id="362ad-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="362ad-679">免责声明</span><span class="sxs-lookup"><span data-stu-id="362ad-679">Disclaimer</span></span>

<span data-ttu-id="362ad-680">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="362ad-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="362ad-681">本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。</span><span class="sxs-lookup"><span data-stu-id="362ad-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="362ad-682">由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。</span><span class="sxs-lookup"><span data-stu-id="362ad-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="362ad-683">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="362ad-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="362ad-684">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="362ad-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="362ad-685">遵守所有适用的著作权法是用户的责任。</span><span class="sxs-lookup"><span data-stu-id="362ad-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="362ad-686">未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。</span><span class="sxs-lookup"><span data-stu-id="362ad-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="362ad-687">对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="362ad-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="362ad-688">除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。</span><span class="sxs-lookup"><span data-stu-id="362ad-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="362ad-689">除非另行说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件此处所述虚构，是的无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 位置或事件旨在或妄加推断。</span><span class="sxs-lookup"><span data-stu-id="362ad-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="362ad-690">(C) 2012 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="362ad-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="362ad-691">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="362ad-691">All rights reserved.</span></span>

<span data-ttu-id="362ad-692">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="362ad-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="362ad-693">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="362ad-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
