---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: 设计来克服的故障 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 29a430a223fb62d9530ea00a60d458a6dbc5199a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820650"
---
<a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>设计来克服的故障 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


您不必考虑任何类型的应用程序，但尤其是将其中很多人将使用它，在云中运行的生成时的项目之一是如何设计应用程序，以便它可以适当地处理故障并继续提供的价值高达可能。 只要有足够的时间，操作将会在任何环境或任何软件系统中出错。 您的应用程序如何处理这些情况下确定你的客户将获得如何不安和多长时间需要花费分析和解决问题。

## <a name="types-of-failures"></a>类型的故障

有两种基本类别的故障，你将想要以不同方式处理：

- 暂时性故障，自愈如间歇性网络连接问题的故障。
- 需要干预的辩论失败。

对于暂时性故障，可以实现重试策略来确保该最快速和自动恢复应用程序的时间。 你的客户可能会注意到稍长的响应时间，但否则它们不会受到影响。 我们将介绍一些方法来处理这些错误中的[暂时性故障处理一章](transient-fault-handling.md)。

对于持久故障，可以实现监视和日志记录功能，当出现问题并促进根本原因分析时立即通知你。 我们将介绍一些方法可帮助您掌握这些类型中的错误[监视和遥测章](monitoring-and-telemetry.md)。

## <a name="failure-scope"></a>故障范围

您还必须考虑失败作用域 – 是否会影响一台计算机，例如 SQL 数据库或存储或整个区域的整个服务。

![故障范围](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>计算机故障

在 Azure 中，一个新自动替换为出现故障的服务器和设计良好的云应用程序自动快速地从这种类型的故障恢复。 前面我们强调无状态 web 层的可伸缩性优势和易用性从发生故障的服务器恢复是无状态的另一个好处。 易用性恢复也是平台即服务 (PaaS) 功能，例如 SQL 数据库和 Azure 应用服务 Web 应用的优势之一。 硬件故障很少见，但当它们出现的这些服务处理它们自动保存功能。您甚至无需编写代码来处理计算机失败时要使用其中一种服务。

### <a name="service-failures"></a>服务故障

云应用程序通常使用多个服务。 例如，修复其应用程序使用 SQL 数据库服务，存储服务和 web 应用部署到 Azure 应用服务。 有什么将您的应用程序？ 如果你依赖的服务之一出现故障 某些服务失败友好"很抱歉，稍后重试"消息可能是的最佳做法。 但在许多情况下会更好。 例如，当后端数据存储区已关闭，你可以接受用户输入、 显示"你的请求已收到，"和存储其他任何位置的输入暂时;如果您需要的服务再次正常运行，然后可以检索输入，并对其进行处理。

[以队列为中心的工作模式](queue-centric-work-pattern.md)章演示一种方法来处理这种情况。 Fix It 应用将任务存储在 SQL 数据库中，但它无需退出工作时 SQL 数据库已关闭。 这一章中我们将了解如何将用户输入任务存储在队列中，并使用工作进程队列中读取和更新任务。 如果 SQL 已关闭，创建 Fix It 任务的能力会受到影响;工作进程可以等待和 SQL 数据库可用时处理新的任务。

### <a name="region-failures"></a>区域故障

整个区域可能会失败。 自然灾难可能会破坏数据中心，它可能被 meteor 获取压扁，trunk 行到数据中心可能会中断通过 burying backhoe 等 cow farmer。如果您的应用程序托管在 stricken 数据中心要怎么做？ 可以将您的应用程序在 Azure 中设置多个区域中同时运行，以便如果在一个灾难，继续在另一个区域中运行它。 此类故障是极少发生，并通过将无需确保不间断的服务，通过这种故障，大多数应用程序不跳转。 请参阅有关如何使您的应用程序甚至通过区域故障的信息的一章末尾处的资源部分。

Azure 的目标是使处理所有的故障更容易，这些类型，将看到我们所执行的以下章节中的一些示例。

## <a name="slas"></a>服务级别协议

人们经常听到有关云环境中的服务级别协议 (Sla)。 基本上，这些都是如何可靠其服务的公司所做的承诺。 99.9 %sla 意味着你应该会正常 99.9%的时间运行的服务。 这个功能 SLA 的相当典型值，这听起来像数目很大，但是可能不知道多少停机时间。 1%实际上相当于。 下面是表显示了各种 SLA 百分比通过一年、 月和每周金额为多少停机时间。

![SLA 表](design-to-survive-failures/_static/image2.png)

因此 99.9 %sla 意味着你的服务可能向 8.76 小时下一年或每个月的 43.2 分钟。 这是更多的停机时间不是大多数人都知道。 作为开发人员，因此你想要了解一定的停机时间，有可能，并妥善的方式对其进行处理。 在某一时刻人想要使用您的应用程序和服务将会关闭，并且想要最大程度减少的负面影响的客户。

您应该了解的 SLA 的一点是它为引用的哪个时间段： 时钟重置每周、 每个月或每年？ 在 Azure 中我们将时钟重置每个月，这是比每年的 SLA，为您好，因为每年 SLA 可以通过一系列的很好的几个月偏移它们隐藏错误几个月。

当然我们始终能够以合理方式做得更好 SLA;通常，您可以在下比这少得多。 承诺是，如果这就是不断失败的时间超过最大停机时间则可以要求退款。 您得到可能的金额不会完全弥补您的业务影响的停机时间，过多，但该方面的 SLA 充当强制策略，并让你知道，我们执行它非常重视。

### <a name="composite-slas"></a>复合 Sla

考虑时还需考虑服务级别协议的一个重点是在应用中，每个具有单独的 SLA 服务上使用多个服务的影响。 例如，修复其应用使用 Azure 应用服务 Web 应用、 Azure 存储和 SQL 数据库。 以下是截至日期在 2013 年 12 月，编写这本电子书其 SLA 号码：

![SLA 网站、 存储、 SQL 数据库](design-to-survive-failures/_static/image3.png)

停机时间你所期望的应用程序中基于这些服务 Sla 的最大值是什么？ 您可能认为，停机时间将等于最差的 SLA 百分比或 99.9%在这种情况下。 这将是 true，如果所有三个服务始终失败一次，但这并不是一定究竟发生了什么。 每个服务可能会失败独立地在不同的时间，因此您必须将单独的 SLA 数字相乘来计算的复合 SLA。

![复合 SLA](design-to-survive-failures/_static/image4.png)

因此您的应用程序是停机 43.2 分钟不只是一个月，但该 3 倍数量，每个月 – 108 分钟，仍是 Azure SLA 限制范围内。

此问题不是唯一的 Azure。 我们实际提供最佳云服务级别协议的任何云服务可用，并且你将有类似的问题，如果你使用任何供应商的云服务处理。 这突出显示是想法的关于如何可以设计您的应用程序正确地，处理不可避免地存在服务失败，因为它们可能会发生频率不够高，以影响会客户或用户的重要性。

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>云与企业停机的情况下体验相比的 Sla

人们有时说，"我的企业应用程序中我永远不会有这些问题。" 如果需要多大停机时间是每月他们实际上有，他们通常所说，"嗯，它会发生情况有时。" 如果需要何种频率，它们的承认"有时我们需要备份或安装新的服务器或更新软件。" 当然的计数为停机时间。 大多数企业应用除非它们是特别是关键任务都已实际关闭对多个通过我们的服务的 Sla 所允许的时间量。 但你的服务器和基础结构，并且你要负责为它和它的控件中，往往会更少反响感受下降时间。 在云环境中，你是依赖于其他人并不知道正在运行的内容，因此可能往往容易变得更关注它。

当企业可实现更高版本的运行时间百分比不是从云 SLA 获取时，他们可以执行该操作在硬件上花费更多资金。 云服务可以做到这一点，但必须从其服务的更多收取相关费用。 不过，您可以利用经济高效的服务，设计您的软件，以便不可避免故障导致最小中断到你的客户。 为云应用程序设计器作业不这么多需要避免为了避免灾难，失败，则执行该操作通过侧重于软件，不在硬件上。 企业应用程序尽量以最大化平均无故障时间，而云应用程序尽可能最小化平均恢复时间。

### <a name="not-all-cloud-services-have-slas"></a>并非所有云服务都具有服务级别协议

注意还不是每个云服务甚至提供 SLA。 如果您的应用程序依赖于没有正常运行时间保证的服务，你可能关闭比您想象的更长。 例如，如果您启用到你的站点使用 Facebook 或 Twitter 等社交提供程序日志中，检查与服务提供商，以找出，是否没有 SLA，而且您会发现有根本没有连接。 但是，如果身份验证服务出现故障或无法支持你的请求数量，客户被锁定之外，您的应用程序。 天或更长时间，可能已关闭。 一个新的应用程序的创建者应数以亿计的下载内容和依赖于 Facebook 身份验证 – 但不太迟将实时和发现之前与 Facebook 联系，没有为该服务没有 SLA。

### <a name="not-all-downtime-counts-toward-slas"></a>并非所有的停机时间将计入 Sla

如果您的应用程序过度使用这些，一些云服务可能会有意拒绝服务。 这称为*限制*。 如果服务提供 SLA，应说明条件，在其下您可能会受到限制，以及应用程序设计应避免出现这些情况并作出正确反应受到限制，如果发生这种情况。 例如，如果对服务发出请求开始时超过一定数量每秒失败时，你想要确保自动重试不发生如此之快，它们会导致限制以继续。 我们将更详细说明了中的阻止行为[暂时性故障处理一章](transient-fault-handling.md)。

## <a name="summary"></a>总结

这一章已尝试帮助您实现具有真实世界云应用程序设计为从故障中恢复正常的原因。 从开始[接下来的章节](monitoring-and-telemetry.md)，本系列教程的其余模式转到更详细地介绍一些策略可用于执行此操作：

- 有好[监视和遥测](monitoring-and-telemetry.md)，以便您快速查明故障需要干预，并具有足够的信息来解决这些问题。
- [处理暂时性故障](transient-fault-handling.md)通过实现智能重试逻辑，以便您的应用程序将自动恢复时可以并会返回到[断路器](transient-fault-handling.md#circuitbreakers)逻辑时它不能。
- 使用[分布式缓存](distributed-caching.md)以尽可能减少吞吐量、 延迟和连接问题的数据库访问权限。
- 实现松散耦合通过[以队列为中心的工作模式](queue-centric-work-pattern.md)，以便应用前端可以继续工作时后端已关闭。

## <a name="resources"></a>资源

有关详细信息，请参阅后面的章节中这本电子书和以下资源。

文档：

- [防故障： 弹性云体系结构指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 Marc Mercuri、 Ulrich Homann 和 Andrew Townhill 白皮书。 防故障系列视频的 web 页面版本。
- [Azure 云服务上的大规模服务的设计的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 Mark Simms 和 Michael Thomassy 白皮书。
- [Azure 业务连续性技术指南](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx)。 Patrick Wickline 和 Jason Roth 白皮书。
- [灾难恢复和高可用性 Azure 应用程序的](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx)。 由 Michael McKeown、 Hanu Kommalapati 和 Jason Roth 白皮书。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅多数据中心部署指南，断路器模式。
- [Azure 支持-服务级别协议](https://azure.microsoft.com/support/legal/sla/)。
- [Azure SQL 数据库中的业务连续性](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx)。 有关 SQL 数据库高可用性和灾难恢复功能的文档。
- [高可用性和灾难恢复 Azure 虚拟机中 SQL Server 的](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)。

视频：

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分组成的系列 Ulrich Homann、 Marc Mercuri 和 Mark Simms。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 剧集 1 和 8 进入中进行深入设计云应用程序以从故障中恢复的原因。 另请参阅第 2 节开始 49:57、 故障点和在第 2 节开始 56:05，故障模式的讨论和断路器在段 3 开始 40:55 的讨论中的阻止行为跟进的讨论。
- [构建大型： 从 Azure 客户的第 ii 部分到的经验教训](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simms 介绍了设计失败以及检测所有内容。 类似于防故障系列但进入操作方法的更多详细信息。

> [!div class="step-by-step"]
> [上一页](unstructured-blob-storage.md)
> [下一页](monitoring-and-telemetry.md)
