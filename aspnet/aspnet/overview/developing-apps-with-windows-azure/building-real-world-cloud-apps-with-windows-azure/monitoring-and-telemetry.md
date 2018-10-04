---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 监视和遥测 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f4dae827627103e5cfb9981b6c3b9342cdc34c13
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577998"
---
<a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>监视和遥测 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


很多人依赖于客户能够让他们知道其应用程序出现故障时。 它实际上不是最佳做法是任意位置，尤其是并不在云中。 快速通知时，不能保证和时执行操作获得通知，你通常可以获取有关发生了什么情况的最小或令人误解数据。 具有良好的遥测和日志记录系统，你可以在使用您的应用程序，并在内容了解所发生事件的确实出现时立即查明原因并能有所帮助的故障排除信息，才能使用。

## <a name="buy-or-rent-a-telemetry-solution"></a>购买或租用遥测解决方案

> [!NOTE]
> 撰写本文时前[Application Insights](/azure/application-insights/app-insights-overview)发布。 Application Insights 遥测解决方案在 Azure 上的首选的方法。 请参阅[为 ASP.NET 网站设置 Application Insights](/azure/application-insights/app-insights-asp-net)有关详细信息。


有关云环境很好的事情之一是，它是非常容易购买或租用胜利之路。 遥测是一个示例。 而无需花大力气就可以真正良好的遥测系统最多和正在运行，非常经济高效的方式。 有一系列强大的合作伙伴的与 Azure 集成，并且其中一些具有免费层-以便可以获取基本遥测数据执行任何操作。 下面是一些与当前可在 Azure 上：

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#)还包括监视功能。

我们将快速引导完成设置以显示它是多么使用遥测系统的 New Relic。

在 Azure 管理门户中，为服务注册。 单击**新建**，然后单击**存储区**。 **选择外接程序**对话框随即出现。 向下滚动并单击**New Relic**。

![选择外接程序](monitoring-and-telemetry/_static/image1.png)

单击右箭头并选择所需的服务层。 对于本演示中，我们将使用免费层。

![个性化外接程序](monitoring-and-telemetry/_static/image2.png)

单击右箭头，确认"购买"，New Relic 现在显示为在门户中的外接程序。

![查看购买](monitoring-and-telemetry/_static/image3.png)

![在管理门户中的新 Relic 外接程序](monitoring-and-telemetry/_static/image4.png)

单击**连接信息**，并将复制的许可证密钥。

![连接信息](monitoring-and-telemetry/_static/image5.png)

转到**配置**web 应用在门户中，设置选项卡上**性能监视**到**外接程序**，并设置**选择外接程序**下拉列表**New Relic**。 然后单击**保存**。

![配置选项卡中的 new Relic](monitoring-and-telemetry/_static/image6.png)

在 Visual Studio 中，安装应用程序中的 New Relic NuGet 包。

![配置选项卡中的开发人员分析](monitoring-and-telemetry/_static/image7.png)

将应用部署到 Azure 并开始使用它。 创建几个 Fix It 任务，从而提供某些活动的 New Relic 监视。

然后回到**New Relic**页面**外接程序**选项卡上的门户并单击**管理**。 在门户向你发送到 New Relic 管理门户中，使用单一登录进行身份验证，因此无需再次输入你的凭据。 概述页提供了各种性能统计信息。 （单击图像可查看完整的概述页的大小。）

[![新 Relic 监视选项卡](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

下面是一些您所见的统计信息：

- 在一天中的不同时间的平均响应时间。

    ![响应时间](monitoring-and-telemetry/_static/image10.png)
- 在一天中的不同时间的吞吐率 （以每分钟的请求）。

    ![吞吐量](monitoring-and-telemetry/_static/image11.png)
- 处理不同的 HTTP 请求所用的服务器 CPU 时间。

    ![Web 事务时间](monitoring-and-telemetry/_static/image12.png)
- 在应用程序代码的不同部分中所用的 CPU 时间：

    ![跟踪详细信息](monitoring-and-telemetry/_static/image13.png)
- 历史性能统计信息。

    ![历史性能](monitoring-and-telemetry/_static/image14.png)
- 对 Blob 服务和有关如何可靠且高度可响应的统计信息等外部服务的调用已被该服务。

    ![外部服务](monitoring-and-telemetry/_static/image15.png)

    ![外部服务](monitoring-and-telemetry/_static/image16.png)

    ![外部服务](monitoring-and-telemetry/_static/image17.png)
- 有关在何处世界上或在美国 web 应用流量的来源中的信息。

    ![Geography](monitoring-and-telemetry/_static/image18.png)

此外可以设置报告和事件。 例如，可以说，开始看到错误的任何时间，将一封电子邮件发送到的问题的警报的支持人员。

![报表](monitoring-and-telemetry/_static/image19.png)

New Relic 是只是一个示例中的遥测系统;可以从其他服务中实现所有这些数据。 在云中的优点是，而无需编写任何代码，且为最小也没有费用，突然可以获取有关你的应用程序的使用方式和您的客户实际上如何遇到大量详细信息。

<a id="log"></a>
## <a name="log-for-insight"></a>见解记录

遥测包是很好的第一步，但你仍然需要检测您自己的代码。 遥测服务告知您问题时，并告诉您哪些客户遇到，但它可能不提供大量深入了解这怎么回事在代码中。

您不希望能够远程连接到生产服务器，请参阅您的应用程序的作用。 这可能是实际时您有一台服务器，但在什么时候已扩展到数百台服务器并且您不知道的哪些需要远程连接到？ 日志记录应提供足够的信息永远不会具有远程连接到生产服务器来分析和调试的问题。 您应将日志记录足够的信息，以便可以隔离仅通过日志的问题。

### <a name="log-in-production"></a>在生产环境中的日志

很多人启用跟踪在生产环境中仅时出现问题，他们想要调试。 这可以大量之间加入延迟的时间了解所造成的问题和获取有关它的有用疑难解答信息的时间。 你获得的信息可能不很有帮助的间歇性错误。

我们建议存储比较便宜的云环境其中是您始终保留在生产环境中的日志记录。 这样一来，当你已有这些记录，并且具有可帮助的历史数据，会出现错误时你分析随着时间的推移开发或定期在不同时间发生的问题。 无法自动清除过程，以删除旧日志，但您可能会发现更昂贵，若要设置此类过程，比保留日志。

故障排除的时间和金钱可以保存所提供的信息时出现问题，你需要已提供所有的量相比，额外的费用的日志记录并不重要。 然后当有人告诉您它们具有随机错误一段时间大约 8:00 昨晚，但它们不记得该错误，您可以轻松地找出了什么问题。

对于小于 4 美元每月另一方面，可以保留 50 千兆字节的日志和日志记录的性能影响是简单，只要保持注意-若要避免性能瓶颈，请确保你的日志记录库是异步的一件事。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>需要执行操作的日志区分开来的通知日志

日志是应该做的 （我希望您知道的内容） 的通知或采取措施 （我希望您执行某些操作）。 请注意仅编写真正需要一个人或自动化的过程采取操作问题，ACT 日志。 过多的 ACT 日志会造成干扰，需要过多的工作要筛查一切找出真正的问题。 如果 ACT 日志自动触发一些操作，如发送电子邮件支持人员，避免让数以千计的此类操作触发的一个问题。

在.NET System.Diagnostics 跟踪日志可以分配错误、 警告、 信息和调试/详细级别。 通过保留 ACT 日志将错误级别以及为使用较低级别的通知日志，您可以从通知日志区分 ACT。

![日志级别](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在运行时配置日志记录级别

日志记录始终在生产环境中有必要准备时，另一种最佳做法是实现使您可以在运行时调整的要记录的详细信息，而不重新部署或重新启动你的应用程序级别的日志记录框架。 例如当使用跟踪工具中的`System.Diagnostics`错误、 警告、 信息，可以创建并调试/详细记录。 我们建议始终记录错误、 警告、 信息记录在生产中，并将想要能够动态地添加调试/详细日志记录以进行故障排除案例的基础上。

在 Azure 应用服务中的 web 应用具有内置支持，以进行写入`System.Diagnostics`日志传输到文件系统、 表存储或 Blob 存储。 可以选择不同的日志记录级别的每个存储目标，并且可以无需重新启动你的应用程序更改动态日志记录级别。 Blob 存储支持可更轻松地运行[HDInsight](https://docs.microsoft.com/azure/hdinsight/)分析的作业，在应用程序日志，因为 HDInsight 知道如何直接使用 Blob 存储。

### <a name="log-exceptions"></a>记录异常

请勿只在放入*异常。Tostring （)* 日志记录代码中。 这会忽略的上下文信息。 如果 SQL 发生错误，则将保留出 SQL 错误号。 所有异常，包括上下文信息、 本身，异常和内部异常以确保你要提供的所有内容，将需要进行故障排除。 例如，上下文信息可能包括服务器名称、 事务标识符和用户名称 （但不是密码或任何机密 ！）。

如果您依赖于每个开发人员执行正确的操作与日志记录的异常，其中一些不会。 若要确保，完成右侧方法每次，生成的异常处理直接在你记录器的接口： 传递给 logger 类的异常对象本身和正确的记录器类中记录异常数据。

### <a name="log-calls-to-services"></a>对服务的日志调用

我们强烈建议您编写日志每次您的应用程序会调用服务，无论它是数据库或 REST API 或任何外部服务。 包括在日志中不仅相对值的指示成功或失败，但每个请求需要多长时间。 在云环境中通常将看到与突降而不是完整的服务中断相关的问题。 这通常需要对 10 毫秒可能会突然开始执行第二个。 当有人告诉您在应用运行速度慢时，你想要能够查看 New Relic 或任何遥测服务具有和验证他们的体验，然后希望能够查看您自己的日志，深入了解为什么说是慢速的详细信息。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 接口

我们建议执行此创建生产应用程序时将创建一个简单*ILogger*接口，并在其中粘贴一些方法。 这样，可以轻松更改日志记录实现更高版本并无需再执行所有代码，执行此操作。 可以使用我们`System.Diagnostics.Trace`类在整个 Fix It 应用，但改为我们将使用它的日志记录类中实现后台*ILogger*，并赚*ILogger*方法调用在整个应用程序。

这样一来，如果你想要让你的日志记录更丰富，您可以替换[ `System.Diagnostics.Trace` ](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs)要与任何日志记录机制。 例如，随着您的应用程序的增长您可能决定你想要使用更全面的日志记录包，如[NLog](http://nlog-project.org/)或[企业库日志记录应用程序块](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。 ([Log4Net](http://logging.apache.org/log4net/)是另一个常用的日志记录框架，但它不执行异步日志记录。)

使用 NLog 之类的框架的一个可能原因是便于分解成独立的大容量和高价值数据存储日志记录输出。 可帮助你有效地存储大量不需要快速对执行查询，同时保持快速访问 ACT 数据的通知数据。

### <a name="semantic-logging"></a>语义式日志记录

执行操作可以生成更有用的诊断信息的日志记录相对较新方法，请参阅[企业库语义式日志记录应用程序块 (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 使用碎片[Windows 的事件跟踪](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)(ETW) 和[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)支持.NET 4.5 才能使您能够创建更多结构化和可查询日志中。 定义每种类型的记录，这样就可以自定义您编写的信息的事件的不同方法。 例如，若要记录可能调用一个 SQL 数据库错误`LogSQLDatabaseError`方法。 对于这种异常，您知道一段关键信息是错误号，因此无法将方法签名中包括错误编号参数和记录的错误号为您编写的日志记录中的单独字段。 因为数在单独的字段，你可以更轻松、 可靠地获取基于 SQL 错误号，如果只已将错误号连成一个消息字符串，您可以比的报表。

## <a name="logging-in-the-fix-it-app"></a>记录解决方法在应用程序

### <a name="the-ilogger-interface"></a>ILogger 接口

下面是*ILogger*修复其应用中的接口。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

这些方法，可以编写在支持的相同的四个级别的日志*System.Diagnostics*。 有关延迟的信息的日志记录的外部服务调用适用的 TraceApi 方法。 您还可以添加一组用于调试/详细级别的方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 接口的记录器实现

接口的实现过程非常简单。 它基本上只是调用到标准版*System.Diagnostics*方法。 以下代码片段显示了所有这三个信息方法另外两个分别的其他人。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>调用 ILogger 方法

每次代码修复其应用中的捕获异常，它将调用*ILogger*方法来记录异常详细信息。 每次它会为数据库、 Blob 服务或 REST API 调用，它启动 stopwatch 调用前的，停止 stopwatch 时该服务返回，并记录经过的时间以及成功或失败的相关信息。

请注意，日志消息包含的类名称和方法名称。 最好确保日志消息标识应用程序代码的哪个部分编写它们。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

现在每个时间 Fix It 应用已对 SQL 数据库的调用，您所见的调用中，调用了它，该方法，并完全多少时间花费了。

![在日志中的 SQL 数据库查询](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果转浏览日志，可以看到数据库调用所花费的时间是变量。 信息可能会很有用： 因为应用程序将所有这些记录可以分析历史趋势如何随着时间的推移执行数据库服务。 例如，服务可能会快速大多数情况下，但请求可能会失败或响应可能会降低在一天的特定时间。

每次应用将上传新文件，则日志，您可以看到完全所用的时间将每个文件上传时，您可为 Blob 服务 – 相同的操作。

![Blob 上传日志](monitoring-and-telemetry/_static/image23.png)

它是代码的要编写每次调用服务，并且现在每当有人回答说他们遇到了问题，您知道确切问题是代码的什么，无论它是代码的一个错误，或即使只速度缓慢运行只需几个额外行。 可以查明问题根源，而无需远程连接到服务器或启用日志记录后该错误发生，并且希望能够重新创建它。

## <a name="dependency-injection-in-the-fix-it-app"></a>解决方法中的依赖关系注入其应用程序

您可能想知道如何上面所示的示例中的存储库构造函数获取记录器接口实现：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

若要将连接接口到实现该应用程序使用[依赖关系注入](http://en.wikipedia.org/wiki/Dependency_injection)(DI) 与[AutoFac](http://autofac.org/)。 DI 使您可以使用基于多个位置在整个代码中的接口的对象，并只需指定在一个位置获取该接口实例化时使用的实现。 这使得更易于更改实现： 例如，你可能想要替换 NLog 记录器 System.Diagnostics 记录器。 或者，以进行自动测试，可能想要替换的记录器的模拟版本。

Fix It 应用程序使用所有存储库和所有控制器中的 DI。 控制器类的构造函数获取*ITaskRepository*接口相同的方式存储库获取记录器接口：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

应用程序使用 AutoFac DI 库自动提供*TaskRepository*并*记录器*这些构造函数的实例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

此代码的基本含义是，任何位置构造函数需要*ILogger*接口，传递的实例中*记录器*类，并且只要它需要*IFixItTaskRepository*接口，则实例中传递*FixItTaskRepository*类。

[AutoFac](http://autofac.org/)是可以使用的许多依赖关系注入框架之一。 另一个受欢迎的一个是[Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)，这是建议，Microsoft 模式与实践中的支持。

## <a name="built-in-logging-support-in-azure"></a>在 Azure 中的内置日志记录支持

Azure 支持以下类型的[日志记录，用于在 Azure 应用服务中 Web 应用](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- （可以打开和关闭和动态设置级别，而无需重新启动站点） 的 System.Diagnostics 跟踪。
- Windows 事件。
- IIS 日志 (HTTP/FREB)。

Azure 支持以下类型的[云服务中的日志记录](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics):

- System.Diagnostics 跟踪。
- 性能计数器。
- Windows 事件。
- IIS 日志 (HTTP/FREB)。
- 监视自定义目录。

Fix It 应用程序使用 System.Diagnostics 跟踪。 需要执行的操作启用日志记录的 web 应用中的 System.Diagnostics 的只是在门户中翻转开关或调用 REST API。 在门户中，单击**配置**选项卡为您的网站，并向下滚动以查看**应用程序诊断**部分。 您可以启用或禁用日志记录并选择所需的日志记录级别。 您可以将日志写入到文件系统或存储帐户的 Azure。

![应用程序诊断和配置选项卡中的站点诊断](monitoring-and-telemetry/_static/image24.png)

启用日志记录在 Azure 中后，可以看到 Visual Studio 输出窗口中的日志，如创建它们。

![流式处理日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![流式处理日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

您还可以将日志写入你的存储帐户并查看其使用任何工具，它可以访问 Azure 存储表服务，例如**服务器资源管理器**Visual Studio 中或[Azure 存储资源管理器](https://azure.microsoft.com/features/storage-explorer/)。

![服务器资源管理器中的日志](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>总结

它是很容易实现的箱遥测系统、 检测你自己的代码中的日志记录和配置 Azure 中的日志记录。 并在遇到生产问题，遥测系统和自定义日志的组合将帮助您快速解决问题，它们可以为您的客户主要问题之前。

在中[接下来的章节](transient-fault-handling.md)我们将介绍如何处理暂时性错误，因此它们不会遇到要调查的生产问题。

## <a name="resources"></a>资源

有关更多信息，请参见以下资源。

主要与遥测数据的文档：

- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅检测和遥测指南、 服务计量指南、 运行状况终结点监视模式和运行时重新配置模式。
- [在云中收缩手势的尾： 启用新 Relic 性能监视的 Azure 网站上](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [Azure 云服务上的大规模服务的设计的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 Mark Simms 和 Michael Thomassy 白皮书。 请参阅遥测和诊断部分。
- [使用 Application Insights 的下一代开发](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN 杂志 》 一文。

有关日志记录的主要文档：

- [语义式日志记录应用程序块 (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 Neil Mackenzie 显示与碎片的语义式日志记录这种情况。
- [使用语义日志记录创建结构化、 更有意义的日志](https://channel9.msdn.com/Events/Build/2013/3-336)。 （视频）罗马儒略 Dominguez 显示与碎片的语义式日志记录这种情况。
- [EF6 SQL 日志记录 – 第 1 部分： 简单的日志记录](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 演示如何登录 EF 6 中的实体框架执行的查询。
- [连接复原和命令截获与 ASP.NET MVC 应用程序中的实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四个包含 9 个部分组成的教程系列，演示如何使用 ef6 命令拦截功能来记录发送到数据库的实体框架的 SQL 命令。
- [改进日志记录使用 C# 5.0 调用方信息特性](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何轻松地记录而无需它硬编码到文本或使用反射来手动获取调用的方法的名称。

主要与故障排除的文档：

- [Azure 的故障排除&amp;调试博客](https://blogs.msdn.com/b/kwill/)。
- [AzureTools – 诊断实用程序使用的 Azure 开发人员支持团队](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 介绍并提供一种工具，可用于在 Azure VM 上下载并运行各种诊断和监视工具的下载链接。 当您需要诊断在特定 VM 上的问题时很有用。
- [使用 Visual Studio 的 Azure 应用服务中 web 应用进行故障排除](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 有关开始使用 System.Diagnostics 跟踪和远程调试的分步教程。

视频：

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分组成的系列 Ulrich Homann、 Marc Mercuri 和 Mark Simms。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 视频 4 和 9 是有关监视和遥测。 第 9 包括监视服务 MetricsHub、 AppDynamics、 New Relic 中，和 PagerDuty 的概述。
- [构建大型： 从 Azure 客户的第 ii 部分到的经验教训](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simms 介绍了设计失败以及检测所有内容。 类似于防故障系列但进入操作方法的更多详细信息。

代码示例：

- [云服务在 Azure 中的基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 Microsoft Azure 客户咨询团队创建的示例应用程序。 以下文章中所述演示遥测和日志记录做法。 此示例通过使用实现应用程序日志记录[NLog](http://nlog-project.org/)。 相关文档，请参阅[系列的四个有关遥测和日志记录的 TechNet wiki 文章](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [上一页](design-to-survive-failures.md)
> [下一页](transient-fault-handling.md)
