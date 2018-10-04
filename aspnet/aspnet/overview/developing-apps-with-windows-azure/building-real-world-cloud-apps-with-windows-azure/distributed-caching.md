---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分布式缓存 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 26866ef9d13a198aab627ccf0f5e1ff3d2304427
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577532"
---
<a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分布式缓存 （构建实际云应用程序与 Azure）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


上一章介绍了暂时性故障处理和提到缓存作为断路器策略。 本章给出了更多背景有关缓存，包括何时使用它的使用情况，常见模式，以及如何在 Azure 中实现。

## <a name="what-is-distributed-caching"></a>什么被分布式缓存

缓存提供高吞吐量、 低延迟访问经常访问的应用程序数据，通过在内存中存储的数据。 对于云应用程序最有用的缓存类型是分布式的缓存，这意味着数据不会存储在单独的 web 服务器的内存，但对其他云资源，以及缓存的数据可供所有应用程序的 web 服务器 （或其他云 Vm 该 are 应用程序使用的)。

![显示访问相同的缓存服务器的多个 web 服务器的关系图](distributed-caching/_static/image1.png)

当通过添加或删除服务器，来缩放应用程序或服务器替换由于升级或故障时，缓存的数据仍然可供运行该应用程序的每个服务器访问。

通过避免永久性数据存储的高延迟数据访问，缓存可以显著提高应用程序响应能力。 例如，从缓存中检索数据是从关系数据库中检索它比快得多。

缓存的一个额外的好处减少为永久性数据存储到永久性数据存储，数据流出量时，可能会导致较低的成本的流量费用。

## <a name="when-to-use-distributed-caching"></a>何时使用分布式缓存

最适合应用程序工作负荷执行多个读取与写入数据，并当数据模型支持的键/值组织的使用来存储和检索缓存中的数据的缓存工作原理。 如果应用程序的用户共享的常见数据; 很多，此选项也更有用例如，缓存会提供尽可能多的好处，如果每个用户通常检索到该用户的唯一数据。 产品目录是的示例其中缓存可能会非常非常有用，因为数据不会频繁更改和所有客户都查看相同的数据。

缓存的好处变得越来越多地可用测量应用程序的横向越多，随着的吞吐量限制和延迟延迟的持久数据存储区的总体应用程序性能的限制的详细信息。 但是，您可以实现缓存的性能以及比其他原因。 对于不一定是完全保持最新状态时向用户显示的数据，缓存的访问时可作为有关断路器永久性数据存储已停止响应或不可用。

## <a name="popular-cache-population-strategies"></a>常用缓存填充策略

为了能够从缓存中检索数据，必须将其第一次存储存在。 有几种策略来到缓存中获取所需的数据：

- 按需 / 缓存预留

    应用程序尝试从缓存检索数据，当缓存中无数据 ("miss")，该应用程序将数据存储在缓存中，以便它将提供下一次。 它会查找下一次应用程序尝试获取相同的数据，它查找的内容缓存 （"射击"） 中。 若要防止对数据库中提取已更改的缓存的数据，您使缓存失效的到数据存储进行更改时。
- 后台数据推送

    后台服务将数据推送到缓存定期计划和应用程序始终提取从缓存。 此方法的工作原理很好地与不总是需要您的高延迟数据源返回的最新数据。
- 断路器

    在应用程序通常传播直接与永久性数据存储，但应用程序时永久性数据存储存在可用性问题，从缓存检索数据。 可能使用缓存到某个位置或背景的数据推送策略的缓存中放置数据。 这是错误处理策略而不是性能增强策略。

为了使缓存中的数据当前，你的应用程序创建、 更新、 或删除数据时，可以删除相关的缓存项。 如果你的应用程序有时会略有过时的数据是好了，您可以借助以多久缓存数据可以是上设置的限制可配置的过期时间。

你可以配置绝对过期 （自创建后的缓存项的时间量） 或可调过期 （自从上次访问缓存项的时间量）。 具体取决于缓存过期机制来防止数据而言太过时上时，使用绝对到期。 在修复其应用中，我们将手动逐出陈旧缓存项和我们将使用可调到期的最新数据保留在缓存中。 无论你选择的过期策略，缓存将自动逐出最旧的 （最近最少使用或 LRU） 项目时达到缓存的内存限制。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Fix It 应用程序的示例缓存端代码

在下面的示例代码中，我们在缓存中检查首先检索 Fix It 任务时。 如果在缓存中找到该任务，我们将返回它;如果未找到，我们从数据库获取并将其存储在缓存中。 所做的更改将添加到缓存`FindTaskByIdAsync`方法会突出显示。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

当你更新或删除 Fix It 任务时，必须要使之无效 （删除） 的已缓存任务。 否则，未来尝试读取该任务将继续从缓存中获取旧的数据。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

这些是示例来演示简单的缓存代码;缓存尚未实现的可下载 Fix It 项目中。

## <a name="azure-caching-services"></a>Azure 缓存服务

Azure 提供了以下缓存服务： [Azure Redis 缓存](https://msdn.microsoft.com/library/dn690523.aspx)并[Azure 托管缓存](https://msdn.microsoft.com/library/dn386094.aspx)。 Azure Redis 缓存基于热门[开放源代码 Redis 缓存](http://redis.io/)和大多数的第一个选项缓存方案。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用缓存提供程序的 ASP.NET 会话状态

如中所述[web 开发最佳实践一章](web-development-best-practices.md)，最佳做法是避免使用会话状态。 如果你的应用程序需要会话状态下, 一步最佳做法是避免默认内存中提供程序，因为它不会启用 scale out （web 服务器的多个实例）。 ASP.NET SQL Server 会话状态提供程序启用要使用会话状态的多个 web 服务器运行的站点，但它会导致相比于内存中提供程序的高延迟成本。 如果您必须使用会话状态的最佳解决方案是使用缓存提供程序，如[用于 Azure Cache 的会话状态提供程序](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)。

## <a name="summary"></a>总结

您已了解如何修复它应用实现缓存以提高响应时间和可伸缩性，并使应用程序继续在数据库不可用时能够读取操作的响应。 在中[接下来的章节](queue-centric-work-pattern.md)我们将介绍如何进一步提高可伸缩性并使应用程序继续写入操作的响应速度快。

## <a name="resources"></a>资源

有关缓存的详细信息，请参阅以下资源。

文档

- [Azure 缓存](https://msdn.microsoft.com/library/gg278356.aspx)。 有关 Azure 中的缓存的官方 MSDN 文档。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅缓存指南和缓存端模式。
- [防故障： 弹性云体系结构指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 Marc Mercuri、 Ulrich Homann 和 Andrew Townhill 白皮书。 在缓存，请参阅部分。
- [Azure 云服务上的大规模服务的设计的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. Mark Simms 和 Michael Thomassy 白皮书。 在分布式缓存，请参阅部分。
- [分布式缓存可伸缩性的路径](https://msdn.microsoft.com/magazine/dd942840.aspx)。 较旧的 (2009) MSDN 杂志 》 文章，但一般情况下; 分布式缓存的清晰编写的简介深入比防故障和最佳实践白皮书的缓存部分。

视频

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分组成的系列 Ulrich Homann、 Marc Mercuri 和 Mark Simms。 提供了如何构建云应用的 400 级视图。 此系列重点介绍从理论上讲并原因原因;有关更多操作方法的详细信息，请参阅由 Mark Simms 构建大系列。 请参阅第 3 开始 1:24:14 中的缓存讨论。
- [构建大型： 从 Azure 客户的第 I 到的经验教训](https://channel9.msdn.com/Events/Build/2012/3-029)。Simon Davies 讨论了分布式缓存开始 46:00。 类似于防故障系列但进入操作方法的更多详细信息。 此演示文稿提供 2012 年 10 月 31 日，因此它不涵盖 2013年中引入的 Azure 应用服务中的 Web 应用程序的缓存服务。

代码示例

- [云服务在 Azure 中的基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 实现分布式缓存的示例应用程序。 请参阅随附的博客文章[云服务基础知识-缓存的基础知识](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)。

> [!div class="step-by-step"]
> [上一页](transient-fault-handling.md)
> [下一页](queue-centric-work-pattern.md)
