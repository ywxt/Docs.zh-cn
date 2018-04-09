---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: 在 IIS 中的 OWIN 中间件集成管道 |Microsoft 文档
author: Praburaj
description: 这篇文章演示如何运行 OWIN 中间件组件 (OMCs) 在 IIS 集成管道、 如何设置管道事件 OMC 上并运行。 你应该...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2013
ms.topic: article
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 5df70c80084a32c5f61ac9288c8cdbfaaa47f124
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="owin-middleware-in-the-iis-integrated-pipeline"></a><span data-ttu-id="8c0dd-104">在 IIS 集成管道中的 OWIN 中间件</span><span class="sxs-lookup"><span data-stu-id="8c0dd-104">OWIN Middleware in the IIS integrated pipeline</span></span>
====================
<span data-ttu-id="8c0dd-105">通过[Praburaj Thiagarajan](https://github.com/Praburaj)， [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="8c0dd-105">by [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="8c0dd-106">这篇文章演示如何运行 OWIN 中间件组件 (OMCs) 在 IIS 集成管道、 如何设置管道事件 OMC 上并运行。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-106">This article shows how to run OWIN middleware Components (OMCs) in the IIS integrated pipeline, and how to set the pipeline event an OMC runs on.</span></span> <span data-ttu-id="8c0dd-107">你应查看[项目概述 Katana](an-overview-of-project-katana.md)和[OWIN 启动类检测](owin-startup-class-detection.md)阅读本教程之前。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-107">You should review [An Overview of Project Katana](an-overview-of-project-katana.md) and [OWIN Startup Class Detection](owin-startup-class-detection.md) before reading this tutorial.</span></span> <span data-ttu-id="8c0dd-108">本教程编写由 Rick Anderson ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )，Chris 跨、 Praburaj Thiagarajan 和 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) )。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Chris Ross, Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>


<span data-ttu-id="8c0dd-109">尽管[OWIN](an-overview-of-project-katana.md)中间件组件 (OMCs) 主要用于在服务器不可知管线中运行，则你可以在 IIS 集成管道也中运行 OMC (**经典模式是*不*支持**)。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-109">Although [OWIN](an-overview-of-project-katana.md) middleware components (OMCs) are primarily designed to run in a server-agnostic pipeline, it is possible to run an OMC in the IIS integrated pipeline as well (**classic mode is *not* supported**).</span></span> <span data-ttu-id="8c0dd-110">可进行 OMC IIS 集成管道中的工作后，通过安装以下包从包管理器控制台 (PMC):</span><span class="sxs-lookup"><span data-stu-id="8c0dd-110">An OMC can be made to work in the IIS integrated pipeline by installing the following package from the Package Manager Console (PMC):</span></span>

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

<span data-ttu-id="8c0dd-111">这意味着所有应用程序框架，甚至那些尚未不能在 IIS 和 System.Web，外部运行可以受益于现有的 OWIN 中间件组件。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-111">This means that all application frameworks, even those that are not yet able to run outside of IIS and System.Web, can benefit from existing OWIN middleware components.</span></span> 

> [!NOTE]
> <span data-ttu-id="8c0dd-112">所有`Microsoft.Owin.Security.*`包随附在 Visual Studio 2013 中新的标识系统 (例如： Cookie、 Microsoft 帐户、 Google、 Facebook、 Twitter[持有者令牌](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html)，OAuth，授权服务器，JWT，Azure Active目录中，和 Active directory 联合身份验证服务） 被编写为 OMCs，并可以在自承载和承载于 IIS 中的方案中使用。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-112">All of the `Microsoft.Owin.Security.*` packages shipping with the new Identity System in Visual Studio 2013 (for example: Cookies, Microsoft Account, Google, Facebook, Twitter, [Bearer Token](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, Authorization server, JWT, Azure Active directory, and Active directory federation services) are authored as OMCs, and can be used in both self-hosted and IIS-hosted scenarios.</span></span>

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a><span data-ttu-id="8c0dd-113">OWIN 中间件 IIS 集成管道中的执行方式</span><span class="sxs-lookup"><span data-stu-id="8c0dd-113">How OWIN Middleware Executes in the IIS Integrated Pipeline</span></span>

<span data-ttu-id="8c0dd-114">OWIN 控制台应用程序，应用程序管道使用构建为[启动配置](owin-startup-class-detection.md)由组件添加使用的顺序设置`IAppBuilder.Use`方法。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-114">For OWIN console applications, the application pipeline built using the [startup configuration](owin-startup-class-detection.md) is set by the order the components are added using the `IAppBuilder.Use` method.</span></span> <span data-ttu-id="8c0dd-115">也就是说，在 OWIN 管道[Katana](an-overview-of-project-katana.md)运行时将使用注册的顺序处理 OMCs `IAppBuilder.Use`。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-115">That is, the OWIN pipeline in the [Katana](an-overview-of-project-katana.md) runtime will process OMCs in the order they were registered using `IAppBuilder.Use`.</span></span> <span data-ttu-id="8c0dd-116">在 IIS 集成管道请求管道组成[Httpmodule](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx)如订阅一组预定义的管道事件[BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)， [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)， [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)等。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-116">In the IIS integrated pipeline the request pipeline consists of [HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) subscribed to a pre-defined set of the pipeline events such as [BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx), etc.</span></span>

<span data-ttu-id="8c0dd-117">如果我们将进行比较的 OMC [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx)在 ASP.NET 世界中，OMC 必须注册到正确的预定义的管道事件。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-117">If we compare an OMC to that of an [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) in the ASP.NET world, an OMC must be registered to the correct pre-defined pipeline event.</span></span> <span data-ttu-id="8c0dd-118">例如，HttpModule`MyModule`请求到达时将调用[AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)管道中的阶段：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-118">For example, the HttpModule `MyModule` will get invoked when a request comes to the [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) stage in the pipeline:</span></span>

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

<span data-ttu-id="8c0dd-119">用于 OMC 参与此相同的、 基于事件的执行排序顺序[Katana](an-overview-of-project-katana.md)通过扫描运行时代码[启动配置](owin-startup-class-detection.md)和订阅的每个到中间件组件集成的管道事件。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-119">In order for an OMC to participate in this same, event-based execution ordering, the [Katana](an-overview-of-project-katana.md) runtime code scans through the [startup configuration](owin-startup-class-detection.md) and subscribes each of the middleware components to an integrated pipeline event.</span></span> <span data-ttu-id="8c0dd-120">例如，以下的 OMC 和注册代码允许你查看的中间件组件的默认事件注册。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-120">For example, the following OMC and registration code enables you to see the default event registration of middleware components.</span></span> <span data-ttu-id="8c0dd-121">(有关更多详细创建的 OWIN 启动类的说明，请参阅[OWIN 启动类检测](owin-startup-class-detection.md)。)</span><span class="sxs-lookup"><span data-stu-id="8c0dd-121">(For more detailed instructions on creating an OWIN startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).)</span></span>

1. <span data-ttu-id="8c0dd-122">创建一个空 web 应用程序项目并将其命名**owin2**。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-122">Create an empty web application project and name it **owin2**.</span></span>
2. <span data-ttu-id="8c0dd-123">从包管理器控制台 (PMC) 中，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-123">From the Package Manager Console (PMC), run the following command:</span></span> 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. <span data-ttu-id="8c0dd-124">添加`OWIN Startup Class`并将其命名`Startup`。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-124">Add an `OWIN Startup Class` and name it `Startup`.</span></span> <span data-ttu-id="8c0dd-125">生成的代码替换为以下 （突出显示所做的更改）：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-125">Replace the generated code with the following (the changes are highlighted):</span></span>  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. <span data-ttu-id="8c0dd-126">按 F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-126">Hit F5 to run the app.</span></span>

<span data-ttu-id="8c0dd-127">启动配置设置了三个中间件组件、 与前两个显示的诊断信息并且对事件作出响应的最后一个 （也显示诊断信息） 的管道。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-127">The Startup configuration sets up a pipeline with three middleware components, the first two displaying diagnostic information and the last one responding to events (and also displaying diagnostic information).</span></span> <span data-ttu-id="8c0dd-128">`PrintCurrentIntegratedPipelineStage`方法显示此中间件调用的集成的管道事件和消息。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-128">The `PrintCurrentIntegratedPipelineStage` method displays the integrated pipeline event this middleware is invoked on and a message.</span></span> <span data-ttu-id="8c0dd-129">输出窗口显示以下信息：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-129">The output windows displays the following:</span></span>

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

<span data-ttu-id="8c0dd-130">Katana 运行时映射到的 OWIN 中间件组件的每个[PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)默认情况下，它对应于 IIS 管道事件[PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-130">The Katana runtime mapped each of the OWIN middleware components to [PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) by default, which corresponds to the IIS pipeline event [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx).</span></span>

## <a name="stage-markers"></a><span data-ttu-id="8c0dd-131">阶段标记</span><span class="sxs-lookup"><span data-stu-id="8c0dd-131">Stage Markers</span></span>

<span data-ttu-id="8c0dd-132">你可以将标记 OMCs 通过使用在特定的管道阶段都执行`IAppBuilder UseStageMarker()`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-132">You can mark OMCs to execute at specific stages of the pipeline by using the `IAppBuilder UseStageMarker()` extension method.</span></span> <span data-ttu-id="8c0dd-133">若要在特定阶段运行的一组中间件组件，阶段标记在右侧插入后的最后一个组件是在注册过程的组。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-133">To run a set of middleware components during a particular stage, insert a stage marker right after the last component is the set during registration.</span></span> <span data-ttu-id="8c0dd-134">有关管道的哪个阶段，你可以执行中间件的规则和顺序组件必须运行 （在教程后面部分解释了规则）。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-134">There are rules on which stage of the pipeline you can execute middleware and the order components must run (The rules are explained later in the tutorial).</span></span> <span data-ttu-id="8c0dd-135">添加`UseStageMarker`方法`Configuration`代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-135">Add the `UseStageMarker` method to the `Configuration` code as shown below:</span></span>

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

<span data-ttu-id="8c0dd-136">`app.UseStageMarker(PipelineStage.Authenticate)`调用配置 （在此情况下，我们两个诊断组件） 的所有以前注册的中间件组件在管道的身份验证阶段上运行。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-136">The `app.UseStageMarker(PipelineStage.Authenticate)` call configures all the previously registered middleware components (in this case, our two diagnostic components) to run on the authentication stage of the pipeline.</span></span> <span data-ttu-id="8c0dd-137">将在上运行的最后一个的中间件组件 （该显示诊断并响应请求）`ResolveCache`阶段 ( [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx)事件)。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-137">The last middleware component (which displays diagnostics and responds to requests) will run on the `ResolveCache` stage (the [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) event).</span></span>

<span data-ttu-id="8c0dd-138">按 F5 运行应用程序。输出窗口显示以下信息：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-138">Hit F5 to run the app.The output window shows the following:</span></span>

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a><span data-ttu-id="8c0dd-139">阶段标记规则</span><span class="sxs-lookup"><span data-stu-id="8c0dd-139">Stage Marker Rules</span></span>

<span data-ttu-id="8c0dd-140">Owin 中间件组件 (OMC) 可以配置为在以下 OWIN 管道阶段事件运行：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-140">Owin middleware components (OMC) can be configured to run at the following OWIN pipeline stage events:</span></span>

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. <span data-ttu-id="8c0dd-141">默认情况下，在最后一个事件将运行 OMCs (`PreHandlerExecute`)。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-141">By default, OMCs run at the last event (`PreHandlerExecute`).</span></span> <span data-ttu-id="8c0dd-142">这正是我们第一个示例代码显示"PreExecuteRequestHandler"。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-142">That's why our first example code displayed "PreExecuteRequestHandler".</span></span>
2. <span data-ttu-id="8c0dd-143">你可以使用`app.UseStageMarker`中列出的方法来注册 OMC 运行更早版本，在任何阶段 OWIN 管道`PipelineStage`枚举。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-143">You can use the a `app.UseStageMarker` method to register a OMC to run earlier, at any stage of the OWIN pipeline listed in the `PipelineStage` enum.</span></span>
3. <span data-ttu-id="8c0dd-144">OWIN 管道和 IIS 管道已经过排序，因此调用`app.UseStageMarker`必须按顺序。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-144">The OWIN pipeline and the IIS pipeline is ordered, therefore calls to `app.UseStageMarker` must be in order.</span></span> <span data-ttu-id="8c0dd-145">无法将事件处理程序设置为之前使用注册到的最后一个事件的事件`app.UseStageMarker`。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-145">You cannot set the event handler to an event that precedes the last event registered with to `app.UseStageMarker`.</span></span> <span data-ttu-id="8c0dd-146">例如，*后*调用：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-146">For example, *after* calling:</span></span>

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   <span data-ttu-id="8c0dd-147">调用`app.UseStageMarker`传递`Authenticate`或`PostAuthenticate`不会遵循，并且会引发任何异常。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-147">calls to `app.UseStageMarker` passing `Authenticate` or `PostAuthenticate` will not be honored, and no exception will be thrown.</span></span> <span data-ttu-id="8c0dd-148">在最新的阶段，即默认情况下运行的 OMCs `PreHandlerExecute`。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-148">OMCs run at the latest stage, which by default is `PreHandlerExecute`.</span></span> <span data-ttu-id="8c0dd-149">阶段标记用于使其运行更早版本。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-149">The stage markers are used to make them to run earlier.</span></span> <span data-ttu-id="8c0dd-150">如果你指定无序的阶段标记，则我们舍入到早期标记中。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-150">If you specify stage markers out of order, we round to the earlier marker.</span></span> <span data-ttu-id="8c0dd-151">换而言之，添加一个阶段标记将显示"最晚阶段 X 运行"。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-151">In other words, adding a stage marker says "Run no later than stage X".</span></span> <span data-ttu-id="8c0dd-152">在其后添加 OWIN 管道中的最早阶段标记 OMC 的运行。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-152">OMC's run at the earliest stage marker added after them in the OWIN pipeline.</span></span>
4. <span data-ttu-id="8c0dd-153">对的调用的最早阶段`app.UseStageMarker`wins。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-153">The earliest stage of calls to `app.UseStageMarker` wins.</span></span> <span data-ttu-id="8c0dd-154">例如，如果你切换的顺序`app.UseStageMarker`我们上一示例中的调用：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-154">For example, if you switch the order of `app.UseStageMarker` calls from our previous example:</span></span>

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   <span data-ttu-id="8c0dd-155">输出窗口将显示：</span><span class="sxs-lookup"><span data-stu-id="8c0dd-155">The output window will display:</span></span> 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   <span data-ttu-id="8c0dd-156">在所有运行的 OMCs`AuthenticateRequest`阶段，因为最后一个 OMC 注册与`Authenticate`事件，和`Authenticate`事件之前的所有其他事件。</span><span class="sxs-lookup"><span data-stu-id="8c0dd-156">The OMCs all run in the `AuthenticateRequest` stage, because the last OMC registered with the `Authenticate` event, and the `Authenticate` event precedes all other events.</span></span>
