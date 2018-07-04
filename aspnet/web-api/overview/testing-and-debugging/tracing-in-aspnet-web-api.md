---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: 在 ASP.NET Web API 2 中进行跟踪 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中启用跟踪。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f9c33e62a1d04bc7851be13560a2bd39e997448f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366859"
---
<a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="a7cb3-103">在 ASP.NET Web API 2 中进行跟踪</span><span class="sxs-lookup"><span data-stu-id="a7cb3-103">Tracing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="a7cb3-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a7cb3-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="a7cb3-105">后想要调试的基于 web 的应用程序，有了一整套很好的跟踪日志别无选择。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="a7cb3-106">本教程演示如何在 ASP.NET Web API 中启用跟踪。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="a7cb3-107">此功能可用于跟踪之前和之后它将调用你的控制器 Web API 框架的用途。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="a7cb3-108">此外可以使用它来跟踪自己的代码。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-108">You can also use it to trace your own code.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a7cb3-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a7cb3-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="a7cb3-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) （也适用于 Visual Studio 2015）</span><span class="sxs-lookup"><span data-stu-id="a7cb3-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="a7cb3-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a7cb3-111">Web API 2</span></span>
> - [<span data-ttu-id="a7cb3-112">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="a7cb3-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)


## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="a7cb3-113">启用 System.Diagnostics 跟踪 Web API 中</span><span class="sxs-lookup"><span data-stu-id="a7cb3-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="a7cb3-114">首先，我们将创建一个新的 ASP.NET Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="a7cb3-115">在 Visual Studio 中，从**文件**菜单中，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-115">In Visual Studio, from the **File** menu, select **New**, then **Project**.</span></span> <span data-ttu-id="a7cb3-116">下**模板**， **Web**，选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a7cb3-117">选择 Web API 项目模板。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="a7cb3-118">从**工具**菜单中，选择**库程序包管理器**，然后**包管理控制台**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-118">From the **Tools** menu, select **Library Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="a7cb3-119">在包管理器控制台窗口中，键入以下命令。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="a7cb3-120">第一个命令将安装最新的 Web API 跟踪包。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="a7cb3-121">它还会更新 core Web API 包。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="a7cb3-122">第二个命令将 WebApi.WebHost 程序包更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="a7cb3-123">如果你想要面向特定版本的 Web API，使用时安装跟踪包的版本标志。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>


<span data-ttu-id="a7cb3-124">在应用中打开文件 WebApiConfig.cs\_开始文件夹。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="a7cb3-125">将以下代码添加到**注册**方法。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="a7cb3-126">此代码将添加[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)到 Web API 管道的类。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="a7cb3-127">**SystemDiagnosticsTraceWriter**类将写入到跟踪[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="a7cb3-128">若要查看的跟踪，请在调试器中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="a7cb3-129">在浏览器中，导航到`/api/values`。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a7cb3-130">跟踪语句将写入 Visual Studio 中的输出窗口。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="a7cb3-131">(从**视图**菜单中，选择**输出**)。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a7cb3-132">因为**SystemDiagnosticsTraceWriter**写入到跟踪**System.Diagnostics.Trace**，可以注册其他跟踪侦听器; 例如，若要编写跟踪日志文件。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="a7cb3-133">有关跟踪编写器的详细信息，请参阅[跟踪侦听器](https://msdn.microsoft.com/library/4y5y10s7.aspx)MSDN 上的主题。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="a7cb3-134">配置的 SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="a7cb3-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="a7cb3-135">下面的代码演示如何配置跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a7cb3-136">有两个可控制的设置：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="a7cb3-137">IsVerbose： 如果为 false，则每个跟踪包含最少信息。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="a7cb3-138">如果为 true，则跟踪将包括的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-138">If true, traces include more information.</span></span>
- <span data-ttu-id="a7cb3-139">MinimumLevel： 设置最小跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="a7cb3-140">跟踪级别，按顺序，为调试、 信息、 警告、 错误和严重。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="a7cb3-141">将跟踪添加到 Web API 应用程序</span><span class="sxs-lookup"><span data-stu-id="a7cb3-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="a7cb3-142">添加跟踪编写器为您提供立即访问创建的 Web API 管道的跟踪。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="a7cb3-143">跟踪编写器还可用于跟踪你自己的代码：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="a7cb3-144">若要获取的跟踪编写器，请调用**HttpConfiguration.Services.GetTraceWriter**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="a7cb3-145">此方法是从一个控制器，可通过访问**ApiController.Configuration**属性。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="a7cb3-146">若要编写跟踪，可以调用**ITraceWriter.Trace**方法直接，但[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)类定义是更友好一些扩展方法。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="a7cb3-147">例如， **Info**上面所示方法使用跟踪级别创建一个跟踪**信息**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="a7cb3-148">Web API 跟踪基础结构</span><span class="sxs-lookup"><span data-stu-id="a7cb3-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="a7cb3-149">本部分介绍如何编写 Web API 的自定义跟踪编写器。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="a7cb3-150">Microsoft.AspNet.WebApi.Tracing 包是基于 Web API 中的更多常规跟踪基础结构。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="a7cb3-151">而不是使用 Microsoft.AspNet.WebApi.Tracing，您也可以插入一些其他跟踪/登录库中，如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/loggin library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="a7cb3-152">若要收集跟踪，实现**ITraceWriter**接口。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="a7cb3-153">下面是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a7cb3-154">**ITraceWriter.Trace**方法创建一个跟踪。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="a7cb3-155">调用方指定的类别和跟踪级别。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="a7cb3-156">类别可以是任何用户定义的字符串。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-156">The category can be any user-defined string.</span></span> <span data-ttu-id="a7cb3-157">实现**跟踪**应执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="a7cb3-158">创建一个新**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="a7cb3-159">对其进行初始化与请求、 类别和跟踪级别，如所示。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="a7cb3-160">由调用方提供这些值。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="a7cb3-161">调用*traceAction*委托。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="a7cb3-162">在此委托，调用方应填充的其余部分**TraceRecord**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="a7cb3-163">编写**TraceRecord**，使用你喜欢的任何日志记录方法。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="a7cb3-164">此处显示的示例只是调用**System.Diagnostics.Trace**。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="a7cb3-165">设置跟踪编写器</span><span class="sxs-lookup"><span data-stu-id="a7cb3-165">Setting the Trace Writer</span></span>

<span data-ttu-id="a7cb3-166">若要启用跟踪，必须配置要使用的 Web API 应用**ITraceWriter**实现。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="a7cb3-167">不要通过此**HttpConfiguration**对象，如下面的代码中所示：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="a7cb3-168">只有一个跟踪编写器处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-168">Only one trace writer can be active.</span></span> <span data-ttu-id="a7cb3-169">默认情况下，Web API 设置&quot;不执行任何操作&quot;不执行任何操作的跟踪。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="a7cb3-170">(&quot;不执行任何操作&quot;跟踪标志存在，以便跟踪代码不需要检查的跟踪编写器是否**null**之前写入跟踪。)</span><span class="sxs-lookup"><span data-stu-id="a7cb3-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="a7cb3-171">Web API 跟踪的工作原理</span><span class="sxs-lookup"><span data-stu-id="a7cb3-171">How Web API Tracing Works</span></span>

<span data-ttu-id="a7cb3-172">在使用中的 Web API 使用的 Web API 中进行跟踪*外观*模式： 启用跟踪后，Web API 包装包含执行跟踪调用的类的请求管道的各个部分。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-172">Tracing in Web API uses a in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="a7cb3-173">例如，当选择一个控制器，该管道将使用**IHttpControllerSelector**接口。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="a7cb3-174">启用跟踪，管道将插入实现的类**IHttpControllerSelector**但真正的实现通过调用：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-174">With tracing enabled, the pipleline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 跟踪使用外观模式。](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a7cb3-176">这种设计的优点包括：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-176">The benefits of this design include:</span></span>

- <span data-ttu-id="a7cb3-177">如果不添加跟踪编写器，跟踪组件不会实例化并没有任何性能影响。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="a7cb3-178">如果您替换默认服务，如**IHttpControllerSelector**与您自己的自定义实现，跟踪不受影响，因为跟踪通过包装器对象。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="a7cb3-179">也可以替换整个 Web API 跟踪框架与您自己的自定义框架，通过将替换为默认值**ITraceManager**服务：</span><span class="sxs-lookup"><span data-stu-id="a7cb3-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="a7cb3-180">实现**ITraceManager.Initialize**初始化跟踪系统。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="a7cb3-181">请注意，这将替换*整个*跟踪框架，包括所有已内置到 Web API 的跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="a7cb3-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
