---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: 在 ASP.NET Web API 2 中进行跟踪 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中启用跟踪。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: e0d525e497cf41a79820417a9c832fa6b5cd7f8a
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912834"
---
<a name="tracing-in-aspnet-web-api-2"></a>在 ASP.NET Web API 2 中进行跟踪
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> 后想要调试的基于 web 的应用程序，有了一整套很好的跟踪日志别无选择。 本教程演示如何在 ASP.NET Web API 中启用跟踪。 此功能可用于跟踪之前和之后它将调用你的控制器 Web API 框架的用途。 此外可以使用它来跟踪自己的代码。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) （也适用于 Visual Studio 2015）
> - Web API 2
> - [Microsoft.AspNet.WebApi.Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>启用 System.Diagnostics 跟踪 Web API 中

首先，我们将创建一个新的 ASP.NET Web 应用程序项目。 在 Visual Studio 中，从**文件**菜单中，选择**新建** > **项目**。 下**模板**， **Web**，选择**ASP.NET Web 应用程序**。

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

选择 Web API 项目模板。

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

从**工具**菜单中，选择**NuGet 包管理器**，然后**包管理控制台**。

在包管理器控制台窗口中，键入以下命令。

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

第一个命令将安装最新的 Web API 跟踪包。 它还会更新 core Web API 包。 第二个命令将 WebApi.WebHost 程序包更新到最新版本。

> [!NOTE]
> 如果你想要面向特定版本的 Web API，使用时安装跟踪包的版本标志。

在应用中打开文件 WebApiConfig.cs\_开始文件夹。 将以下代码添加到**注册**方法。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

此代码将添加[SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx)到 Web API 管道的类。 **SystemDiagnosticsTraceWriter**类将写入到跟踪[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)。

若要查看的跟踪，请在调试器中运行应用程序。 在浏览器中，导航到`/api/values`。

![](tracing-in-aspnet-web-api/_static/image5.png)

跟踪语句将写入 Visual Studio 中的输出窗口。 (从**视图**菜单中，选择**输出**)。

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

因为**SystemDiagnosticsTraceWriter**写入到跟踪**System.Diagnostics.Trace**，可以注册其他跟踪侦听器; 例如，若要编写跟踪日志文件。 有关跟踪编写器的详细信息，请参阅[跟踪侦听器](https://msdn.microsoft.com/library/4y5y10s7.aspx)MSDN 上的主题。

### <a name="configuring-systemdiagnosticstracewriter"></a>配置的 SystemDiagnosticsTraceWriter

下面的代码演示如何配置跟踪编写器。

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

有两个可控制的设置：

- IsVerbose： 如果为 false，则每个跟踪包含最少信息。 如果为 true，则跟踪将包括的详细信息。
- MinimumLevel： 设置最小跟踪级别。 跟踪级别，按顺序，为调试、 信息、 警告、 错误和严重。

## <a name="adding-traces-to-your-web-api-application"></a>将跟踪添加到 Web API 应用程序

添加跟踪编写器为您提供立即访问创建的 Web API 管道的跟踪。 跟踪编写器还可用于跟踪你自己的代码：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

若要获取的跟踪编写器，请调用**HttpConfiguration.Services.GetTraceWriter**。 此方法是从一个控制器，可通过访问**ApiController.Configuration**属性。

若要编写跟踪，可以调用**ITraceWriter.Trace**方法直接，但[ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx)类定义是更友好一些扩展方法。 例如， **Info**上面所示方法使用跟踪级别创建一个跟踪**信息**。

## <a name="web-api-tracing-infrastructure"></a>Web API 跟踪基础结构

本部分介绍如何编写 Web API 的自定义跟踪编写器。

Microsoft.AspNet.WebApi.Tracing 包是基于 Web API 中的更多常规跟踪基础结构。 而不是使用 Microsoft.AspNet.WebApi.Tracing，您也可以插入一些其他跟踪/登录库中，如[NLog](http://nlog-project.org/)或[log4net](http://logging.apache.org/log4net/)。

若要收集跟踪，实现**ITraceWriter**接口。 下面是一个简单的示例：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

**ITraceWriter.Trace**方法创建一个跟踪。 调用方指定的类别和跟踪级别。 类别可以是任何用户定义的字符串。 实现**跟踪**应执行以下操作：

1. 创建一个新**TraceRecord**。 对其进行初始化与请求、 类别和跟踪级别，如所示。 由调用方提供这些值。
2. 调用*traceAction*委托。 在此委托，调用方应填充的其余部分**TraceRecord**。
3. 编写**TraceRecord**，使用你喜欢的任何日志记录方法。 此处显示的示例只是调用**System.Diagnostics.Trace**。

## <a name="setting-the-trace-writer"></a>设置跟踪编写器

若要启用跟踪，必须配置要使用的 Web API 应用**ITraceWriter**实现。 不要通过此**HttpConfiguration**对象，如下面的代码中所示：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

只有一个跟踪编写器处于活动状态。 默认情况下，Web API 设置&quot;不执行任何操作&quot;不执行任何操作的跟踪。 (&quot;不执行任何操作&quot;跟踪标志存在，以便跟踪代码不需要检查的跟踪编写器是否**null**之前写入跟踪。)

## <a name="how-web-api-tracing-works"></a>Web API 跟踪的工作原理

使用 Web API 中的跟踪*外观*模式： 启用跟踪后，Web API 包装包含执行跟踪调用的类的请求管道的各个部分。

例如，当选择一个控制器，该管道将使用**IHttpControllerSelector**接口。 启用跟踪，管道将插入实现的类**IHttpControllerSelector**但真正的实现通过调用：

![Web API 跟踪使用外观模式。](tracing-in-aspnet-web-api/_static/image8.png)

这种设计的优点包括：

- 如果不添加跟踪编写器，跟踪组件不会实例化并没有任何性能影响。
- 如果您替换默认服务，如**IHttpControllerSelector**与您自己的自定义实现，跟踪不受影响，因为跟踪通过包装器对象。

也可以替换整个 Web API 跟踪框架与您自己的自定义框架，通过将替换为默认值**ITraceManager**服务：

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

实现**ITraceManager.Initialize**初始化跟踪系统。 请注意，这将替换*整个*跟踪框架，包括所有已内置到 Web API 的跟踪代码。
