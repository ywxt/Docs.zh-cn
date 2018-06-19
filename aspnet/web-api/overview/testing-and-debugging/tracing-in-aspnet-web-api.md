---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: 在 ASP.NET Web API 2 中进行跟踪 |Microsoft 文档
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中启用跟踪。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7392ae5d9bc4c3aab45a9373099a0ee18e873a4f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
ms.locfileid: "28044203"
---
<a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="a32a2-103">在 ASP.NET Web API 2 中进行跟踪</span><span class="sxs-lookup"><span data-stu-id="a32a2-103">Tracing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="a32a2-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a32a2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="a32a2-105">当你尝试调试基于 web 的应用程序时，没有良好的跟踪日志组无法替代。</span><span class="sxs-lookup"><span data-stu-id="a32a2-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="a32a2-106">本教程演示如何在 ASP.NET Web API 中启用跟踪。</span><span class="sxs-lookup"><span data-stu-id="a32a2-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="a32a2-107">此功能可用于跟踪 Web API 框架之前和之后，它将调用你的控制器的用途。</span><span class="sxs-lookup"><span data-stu-id="a32a2-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="a32a2-108">你还可以使用它来跟踪自己的代码。</span><span class="sxs-lookup"><span data-stu-id="a32a2-108">You can also use it to trace your own code.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a32a2-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a32a2-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a32a2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) （也适用于 Visual Studio 2015）</span><span class="sxs-lookup"><span data-stu-id="a32a2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="a32a2-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a32a2-111">Web API 2</span></span>
> - [<span data-ttu-id="a32a2-112">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="a32a2-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)


## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="a32a2-113">启用 System.Diagnostics 在 Web API 中进行跟踪</span><span class="sxs-lookup"><span data-stu-id="a32a2-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="a32a2-114">首先，我们将创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="a32a2-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="a32a2-115">在 Visual Studio 中，从**文件**菜单上，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-115">In Visual Studio, from the **File** menu, select **New**, then **Project**.</span></span> <span data-ttu-id="a32a2-116">下**模板**， **Web**，选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a32a2-117">选择 Web API 项目模板。</span><span class="sxs-lookup"><span data-stu-id="a32a2-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="a32a2-118">从**工具**菜单上，选择**库程序包管理器**，然后**包管理控制台**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-118">From the **Tools** menu, select **Library Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="a32a2-119">在 Package Manager Console 窗口中，键入以下命令。</span><span class="sxs-lookup"><span data-stu-id="a32a2-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="a32a2-120">第一个命令将安装最新的 Web API 跟踪包。</span><span class="sxs-lookup"><span data-stu-id="a32a2-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="a32a2-121">它还会更新核心 Web API 包。</span><span class="sxs-lookup"><span data-stu-id="a32a2-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="a32a2-122">第二个命令将该 WebApi.WebHost 程序包更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="a32a2-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="a32a2-123">如果你想要针对特定版本的 Web API，使用安装跟踪包时-版本标志。</span><span class="sxs-lookup"><span data-stu-id="a32a2-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>


<span data-ttu-id="a32a2-124">在应用程序中打开文件 WebApiConfig.cs\_开始文件夹。</span><span class="sxs-lookup"><span data-stu-id="a32a2-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="a32a2-125">以下代码添加到**注册**方法。</span><span class="sxs-lookup"><span data-stu-id="a32a2-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="a32a2-126">此代码将添加[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)到 Web API 管道的类。</span><span class="sxs-lookup"><span data-stu-id="a32a2-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="a32a2-127">**SystemDiagnosticsTraceWriter**类写入到跟踪[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)。</span><span class="sxs-lookup"><span data-stu-id="a32a2-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="a32a2-128">若要查看跟踪，请在调试器中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="a32a2-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="a32a2-129">在浏览器中，导航到`/api/values`。</span><span class="sxs-lookup"><span data-stu-id="a32a2-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a32a2-130">跟踪语句写入到 Visual Studio 中的输出窗口中。</span><span class="sxs-lookup"><span data-stu-id="a32a2-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="a32a2-131">(从**视图**菜单上，选择**输出**)。</span><span class="sxs-lookup"><span data-stu-id="a32a2-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a32a2-132">因为**SystemDiagnosticsTraceWriter**写入到跟踪**System.Diagnostics.Trace**，你可以注册其他跟踪侦听器; 例如，若要编写跟踪到日志文件。</span><span class="sxs-lookup"><span data-stu-id="a32a2-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="a32a2-133">有关跟踪编写器的详细信息，请参阅[跟踪侦听器](https://msdn.microsoft.com/library/4y5y10s7.aspx)MSDN 上的主题。</span><span class="sxs-lookup"><span data-stu-id="a32a2-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="a32a2-134">配置 SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="a32a2-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="a32a2-135">下面的代码演示如何配置跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="a32a2-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a32a2-136">有两个可以控制的设置：</span><span class="sxs-lookup"><span data-stu-id="a32a2-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="a32a2-137">IsVerbose： 如果为 false，则每个跟踪包含极少信息。</span><span class="sxs-lookup"><span data-stu-id="a32a2-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="a32a2-138">如果为 true，则跟踪将包含详细信息。</span><span class="sxs-lookup"><span data-stu-id="a32a2-138">If true, traces include more information.</span></span>
- <span data-ttu-id="a32a2-139">MinimumLevel： 设置最小跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="a32a2-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="a32a2-140">跟踪级别，顺序情况下，为调试、 信息、 警告、 错误和严重。</span><span class="sxs-lookup"><span data-stu-id="a32a2-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="a32a2-141">将跟踪添加到 Web API 应用程序</span><span class="sxs-lookup"><span data-stu-id="a32a2-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="a32a2-142">添加跟踪编写器让你直接访问 Web API 管道所创建的跟踪。</span><span class="sxs-lookup"><span data-stu-id="a32a2-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="a32a2-143">你还可以使用跟踪编写器跟踪你自己的代码：</span><span class="sxs-lookup"><span data-stu-id="a32a2-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="a32a2-144">若要获取的跟踪编写器，请调用**HttpConfiguration.Services.GetTraceWriter**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="a32a2-145">此方法是从控制器，可通过访问**ApiController.Configuration**属性。</span><span class="sxs-lookup"><span data-stu-id="a32a2-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="a32a2-146">若要编写跟踪，可以调用**ITraceWriter.Trace**方法直接，但[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)类定义是更友好某些扩展方法。</span><span class="sxs-lookup"><span data-stu-id="a32a2-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="a32a2-147">例如，**信息**上面所示方法使用跟踪级别创建跟踪**信息**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="a32a2-148">Web API 跟踪基础结构</span><span class="sxs-lookup"><span data-stu-id="a32a2-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="a32a2-149">本部分介绍如何编写 Web API 的自定义跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="a32a2-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="a32a2-150">Microsoft.AspNet.WebApi.Tracing 程序包的基于 Web API 中的更多常规跟踪基础结构。</span><span class="sxs-lookup"><span data-stu-id="a32a2-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="a32a2-151">而不是使用 Microsoft.AspNet.WebApi.Tracing，你可以还可以插入在某些其他跟踪/登录库中，如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。</span><span class="sxs-lookup"><span data-stu-id="a32a2-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/loggin library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="a32a2-152">若要收集跟踪，实现**ITraceWriter**接口。</span><span class="sxs-lookup"><span data-stu-id="a32a2-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="a32a2-153">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="a32a2-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a32a2-154">**ITraceWriter.Trace**方法创建一个跟踪。</span><span class="sxs-lookup"><span data-stu-id="a32a2-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="a32a2-155">调用方指定的类别和跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="a32a2-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="a32a2-156">类别可以是任何用户定义的字符串。</span><span class="sxs-lookup"><span data-stu-id="a32a2-156">The category can be any user-defined string.</span></span> <span data-ttu-id="a32a2-157">实现**跟踪**应执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a32a2-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="a32a2-158">创建一个新**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="a32a2-159">并用将其初始化请求、 类别和跟踪级别，如所示。</span><span class="sxs-lookup"><span data-stu-id="a32a2-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="a32a2-160">由调用方提供了这些值。</span><span class="sxs-lookup"><span data-stu-id="a32a2-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="a32a2-161">调用*traceAction*委托。</span><span class="sxs-lookup"><span data-stu-id="a32a2-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="a32a2-162">在此委托，调用方需要填充的其余部分**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="a32a2-163">编写**TraceRecord**，使用你喜欢的任何日志记录方法。</span><span class="sxs-lookup"><span data-stu-id="a32a2-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="a32a2-164">此处显示的示例只需调用到**System.Diagnostics.Trace**。</span><span class="sxs-lookup"><span data-stu-id="a32a2-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="a32a2-165">设置跟踪编写器</span><span class="sxs-lookup"><span data-stu-id="a32a2-165">Setting the Trace Writer</span></span>

<span data-ttu-id="a32a2-166">若要启用跟踪，必须配置要使用的 Web API 你**ITraceWriter**实现。</span><span class="sxs-lookup"><span data-stu-id="a32a2-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="a32a2-167">通过这样做**HttpConfiguration**对象，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="a32a2-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="a32a2-168">只有一个跟踪编写器可以处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="a32a2-168">Only one trace writer can be active.</span></span> <span data-ttu-id="a32a2-169">默认情况下，Web API 将设置&quot;无操作&quot;不执行任何操作的跟踪。</span><span class="sxs-lookup"><span data-stu-id="a32a2-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="a32a2-170">(&quot;无操作&quot;跟踪存在，以便跟踪代码不需要检查的跟踪编写器是否**null**之前编写跟踪。)</span><span class="sxs-lookup"><span data-stu-id="a32a2-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="a32a2-171">如何 Web API 跟踪工作原理</span><span class="sxs-lookup"><span data-stu-id="a32a2-171">How Web API Tracing Works</span></span>

<span data-ttu-id="a32a2-172">跟踪中的 Web API 使用的 Web API 使用*外观*模式： 启用跟踪后，Web API 包装请求管道与执行跟踪调用的类的各个部分。</span><span class="sxs-lookup"><span data-stu-id="a32a2-172">Tracing in Web API uses a in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="a32a2-173">例如，当选择一个控制器，管道使用**IHttpControllerSelector**接口。</span><span class="sxs-lookup"><span data-stu-id="a32a2-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="a32a2-174">使用启用的跟踪，管道将插入一个类以实现**IHttpControllerSelector**但真正实现通过调用：</span><span class="sxs-lookup"><span data-stu-id="a32a2-174">With tracing enabled, the pipleline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 跟踪使用外观模式。](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a32a2-176">这种设计的好处包括：</span><span class="sxs-lookup"><span data-stu-id="a32a2-176">The benefits of this design include:</span></span>

- <span data-ttu-id="a32a2-177">如果您不添加跟踪编写器，跟踪组件未实例化，并使不会影响性能。</span><span class="sxs-lookup"><span data-stu-id="a32a2-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="a32a2-178">如果你如替换默认服务**IHttpControllerSelector**使用你自己的自定义实现，跟踪并不影响，因为跟踪可通过包装器对象。</span><span class="sxs-lookup"><span data-stu-id="a32a2-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="a32a2-179">你也可以替换整个 Web API 跟踪框架使用你自己的自定义框架，通过替换默认的**ITraceManager**服务：</span><span class="sxs-lookup"><span data-stu-id="a32a2-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="a32a2-180">实现**ITraceManager.Initialize**初始化跟踪系统。</span><span class="sxs-lookup"><span data-stu-id="a32a2-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="a32a2-181">请注意，这将替换*整个*跟踪框架，包括所有内置 Web API 的跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="a32a2-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
