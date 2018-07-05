---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 暂时性故障处理 （构建实际云应用与 Azure） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/03/2015
ms.topic: article
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: 13ed8c2373c22070d21519bc495161e956b0ac4d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398409"
---
<a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>暂时性故障处理 （构建使用 Azure 的真实世界云应用程序）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


当您正在设计的真实世界云应用程序时，您必须考虑的事情之一是如何处理临时服务中断的情况。 此问题是云应用中唯一重要的因为您因此依赖网络连接和外部服务。 您都可以获得自我通常修复的小问题，如果您不准备好以智能方式处理它们，它们将导致非常糟糕的体验为您的客户。

## <a name="causes-of-transient-failures"></a>暂时性故障的原因

您会发现云环境的失败和已删除的数据库连接在发生定期。 这是一定程度上因为您将通过多个负载均衡器与在本地环境相比，web 服务器和数据库服务器具有的直接物理连接。 此外，有时，当你是多租户服务相关时你将看到调用服务，获取速度较慢或超时，因为其他人使用该服务的用户很大程度抵达此端口。 在其他情况下可能是过于频繁，达到该服务的用户和该服务故意限制-拒绝连接 – 您以防止产生负面影响其他租户的服务。

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>使用智能重试/回退逻辑来缓解暂时性故障的影响

而不是引发异常并向客户显示不可用或错误页，可以识别通常暂时性的错误，并自动重试该操作中导致错误，希望的之后，长时间将会成功。 大多数情况下，此操作将成功在第二个尝试，并你将从错误中恢复而无需客户曾遇到过注意时出现问题。

有几种方法可以实现智能重试逻辑。

- Microsoft 模式&amp;实践组具有[暂时性故障处理应用程序块](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx)的执行所有操作，如果使用 ADO.NET 的 SQL 数据库 （而不是通过实体框架） 的访问权限。 只需设置的策略进行重试 – 多少次重试查询或命令并等待的时间之间尝试 – 和包装在 SQL 中的代码*使用*块。

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    此外支持 TFH [Azure 角色中缓存](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx)并[服务总线](https://azure.microsoft.com/services/service-bus/)。
- 使用实体框架时您通常不直接使用 SQL 连接，因此不能使用此模式和实践的包，但 Entity Framework 6 到框架生成这种重试逻辑。 在以类似的方式指定重试策略，并 EF 使用该策略无论何时访问数据库。

    若要修复其应用中使用此功能，我们只需是添加一个类，派生自*DbConfiguration*开启重试逻辑。

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    对于框架标识为通常暂时性错误的 SQL 数据库例外，所示的代码指示 EF 使用指数退让延迟之间重试和最大延迟为 5 秒重试该操作最多 3 次。 指数退让意味着每个失败的重试后它将等待较长的时间，然后重试。 如果行中的三次尝试失败，它将引发异常。 断路器有关的以下部分介绍了您为何指数退避和有限的重试次数。

    使用 Azure 存储服务，如修复其应用执行对于 Blob，并已将.NET 存储客户端 API 实现同样的逻辑时，可能出现类似问题。 只需指定重试策略，或您甚至无需执行该操作，如果您愿意使用默认设置。

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>断路器

有多个原因您不想重试次数太多太长一段：

- 永久重试失败的请求太多用户可能会降低其他用户的体验。 如果数以百万计的人是进行重复所有重试请求您可以占用 IIS 调度队列并阻止您的应用程序为其否则无法成功处理的请求提供服务。
- 如果每个人都正在重试由于服务失败，那里可能进行如此多的请求排队等候启动恢复时，该服务获取来路。
- 如果错误是由于受到限制，并且没有的时间限制的服务使用的窗口，继续重试无法将该窗口移出，导致限制以继续。
- 您可能必须等待 web 页的用户来呈现。 让用户等待太长可能会更令人讨厌的该相对较快建议他们稍后再试。

指数退让解决这些问题的一些通过限制的服务能够获得您的应用程序的重试频率。 但还需要具有*断路器*： 这意味着，在某一特定重试您的应用程序将停止重试和采用一些其他操作，如以下阈值：

- 自定义回退。 如果您不能从 Reuters 获取股票价格，或许您可以获得它从 Bloomberg;或者，如果不能从数据库获取数据，或许您可以将其从缓存。
- 失败无提示。 如果您从服务需要不要么为你的应用，只需返回 null 时无法获取数据。 如果在显示 Fix It 任务，并且 Blob 服务没有响应，无法显示而无需在映像任务详细信息。
- 快速失败。 编写用户若要避免填满该服务与错误重试请求，这可能会导致其他用户的服务中断或扩展限制时段。 您可以显示一条友好"稍后重试"消息。

没有一刀切的重试策略。 可以重试更多次，并等待更长时间在异步后台工作进程中不是将在同步的 web 应用中用户正在等待响应。 你可以等待更长时间的关系数据库服务的重试之间不是将缓存服务。 以下是一些示例建议重试策略，以使这些数字可能发生的变化的了解。 （"快速第一个"意味着在首次重试之前没有任何延迟。

![示例重试策略](transient-fault-handling/_static/image1.png)

SQL 数据库重试策略指南，请参阅[暂时性故障和连接到 SQL 数据库的错误进行故障排除](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)。

## <a name="summary"></a>总结

重试/退让策略可以帮助使临时错误不可见客户大多数情况下，和 Microsoft 提供了可用于最大程度减少你实施策略，无论你使用 ADO.NET、 实体框架中或在 Azure 的工作的框架存储服务。

在中[接下来的章节](distributed-caching.md)，我们将介绍如何提高性能和可靠性，因为它使用分布式缓存。

## <a name="resources"></a>资源

有关更多信息，请参见以下资源：

文档

- [Azure 云服务上的大规模服务的设计的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 Mark Simms 和 Michael Thomassy 白皮书。 类似于防故障系列但进入操作方法的更多详细信息。 请参阅遥测和诊断部分。
- [防故障： 弹性云体系结构指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 Marc Mercuri、 Ulrich Homann 和 Andrew Townhill 白皮书。 防故障系列视频的 web 页面版本。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅重试模式，计划程序代理监督程序模式。
- [Azure SQL Database 中的容错能力](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)。 Tony Petrossian 的博客文章。
- [实体框架的连接复原 / 重试逻辑](https://msdn.microsoft.com/data/dn456835)。 如何使用和自定义临时故障处理的 Entity Framework 6 的功能。
- [连接复原和命令截获与 ASP.NET MVC 应用程序中的实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四个包含 9 个部分组成的教程系列，演示如何设置针对 SQL Database EF 6 连接复原功能。

视频

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分组成的系列 Ulrich Homann、 Marc Mercuri 和 Mark Simms。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 请参阅断路器在段 3 开始 40:55 的讨论。
- [构建大型： 从 Azure 客户的第 ii 部分到的经验教训](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simms 谈到了如何设计失败，暂时性错误处理，以及检测所有内容。

代码示例

- [云服务在 Azure 中的基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 示例应用程序创建的 Microsoft Azure 客户顾问团队，演示如何使用[企业库暂时性故障处理块](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)(TFH)。 有关详细信息，请参阅[云服务基础数据访问层-临时故障处理](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)。 TFH 建议用于使用 ADO.NET 直接 （而不使用实体框架） 的数据库访问权限。

> [!div class="step-by-step"]
> [上一页](monitoring-and-telemetry.md)
> [下一页](distributed-caching.md)
