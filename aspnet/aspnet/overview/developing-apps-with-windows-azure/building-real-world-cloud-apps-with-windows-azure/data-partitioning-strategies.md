---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 数据分区策略 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: 89921df4f84b86ef7c222f8e8c871f510856b4f3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819794"
---
<a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>数据分区策略 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关序列的信息，请参阅[的第一章](introduction.md)。


前面我们看到，若要通过添加和删除 web 服务器扩展的云应用程序，web 层是多么容易。 但是，如果它们已全部达到相同的数据存储，应用程序的瓶颈将移动从前端到后端和数据层，最难进行缩放。 在这一章中我们介绍如何，将数据分区为多个关系数据库，或将与其他数据存储选项结合使用关系数据库存储，可以使数据层可缩放。

设置分区方案是最佳完成得更清楚前面所述的原因相同： 它是很难之后应用在生产环境中，更改你的数据存储策略。 如果您认为硬预先有关不同的方法，可以避免必须"Twitter 片刻"您的应用程序崩溃或长时间出现故障，而重新组织您的应用程序数据和数据访问代码时。

## <a name="the-three-vs-of-data-storage"></a>数据存储在三个 Vs

若要确定是否需要分区策略，它应该是什么，请考虑有关数据的三个问题：

- 卷-数据量将您最终存储？ 几千兆字节为单位？ 几个几百个千兆字节为单位？ 兆兆字节？ 千万亿字节级别？
- 速度 – 你的数据会增长的速率是什么？ 它是不生成大量数据的内部应用？ 客户将上传图像和视频到外部应用程序？
- 各种 – 类型的数据将存储？ 关系、 图像、 键 / 值对、 社交关系图？

如果您认为您会有大量的卷、 速度或不同，您必须仔细考虑哪种分区方案最会使应用能够随着高效且有效地增长，并以确保您未遇到任何瓶颈。

主要有三种方法与分区：

- 垂直分区
- 水平分区
- 混合分区

## <a name="vertical-partitioning"></a>垂直分区

垂直 portioning 就像表按列进行分离： 一组列都进入一个数据存储，并且另一组列将进入一个不同的数据存储。

例如，假设我的应用程序存储有关的人，包括映像的数据：

![数据表](data-partitioning-strategies/_static/image1.png)

表示此数据作为表并查看不同类型的数据，可以看到在左侧的三个列具有可以有效地存储由关系数据库，而在右侧的两个列是实质上是字节数组的字符串数据的 c从图像文件的 ome。 可以将关系数据库中存储图像文件数据和很多人这样做是因为他们不想要将数据保存到文件系统。 它们可能没有可存储的数据所需的卷的文件系统，或者它们可能不希望管理单独备份和还原系统。 此方法适用于在本地数据库和对于少量的云数据库中的数据。 在本地环境中，可能会更轻松地只是让数据库管理员负责的所有内容。

但在云数据库中，存储成本相对高昂，并且有大量的映像无法使数据库的大小增长到超出限制的它可以有效操作。 可以将数据垂直分区解决这些问题，这意味着数据在表中选择最合适的数据存储的每个列。 什么可能最适合于此示例是将字符串数据放入关系数据库和 Blob 存储中的映像。

![垂直分区的数据表](data-partitioning-strategies/_static/image2.png)

将映像存储在 Blob 存储而非数据库是在本地环境中比在云中更实用，因为无需担心如何设置文件服务器或管理备份和还原的数据存储在关系数据库之外： 所有为您自动处理 Blob 存储服务。

这是分区方法中修复该应用程序中，我们实现和我们将看看代码，在[Blob 存储一章](unstructured-blob-storage.md)。 如果没有此分区方案和假定 3 兆字节为单位的平均图像大小，修复其应用将仅能以达到 150 千兆字节的最大数据库大小之前存储约 40000 个任务。 正在删除映像之后，数据库可以存储 10 倍的任务;你必须考虑有关实施水平分区方案之前，你可以转更长的时间。 并且随着应用程序扩展，您的费用更慢增长因为你的存储需求的大容量进入非常廉价的 Blob 存储。

## <a name="horizontal-partitioning-sharding"></a>水平分区 （分片）

水平 portioning 就像按行拆分表： 将一组行进入一个数据存储，并且另一个行集将进入一个不同的数据存储。

给定的相同数据集，另一个选项是在不同的数据库中存储不同范围的客户名称。

![水平分区的数据表](data-partitioning-strategies/_static/image3.png)

你想要非常谨慎以确保数据均匀分布以避免产生热点你分片方案。 此简单示例中使用的最后一个名称的第一个字母不满足该要求，因为很多人具有的某些常见的字母开头的最后一个名称。 将时间早于您所料由于某些数据库将变得很大，在大多数会保持小的同时按表大小限制。

水平分区做的缺点是，它可能很难在所有数据执行的查询。 在此示例中，查询必须最多 26 个不同的数据库，若要获取的所有应用所存储的数据的描述。

## <a name="hybrid-partitioning"></a>混合分区

可以组合使用垂直和水平分区。 例如，在示例数据将无法在 Blob 存储中存储图像和字符串数据水平分区。

![数据分区的表混合](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>分区的生产应用程序

从概念上很容易看到如何均可使用分区方案，但任何分区方案也会增加代码复杂性并引入了许多新的复杂情况，您需要处理。 如果要移动到 blob 存储的映像，您怎么办时的存储服务已停止？ 如何处理 blob 安全？ 如果数据库和 blob 存储获取同步的会发生什么情况？ 如果你是分片，您将如何处理跨所有数据库进行都查询？

只要您计划为其在执行到生产环境之前，复杂性是易于管理。 未执行的操作的许多人希望他们有更高版本。 我们的客户咨询团队 (CAT) 团队从客户的应用程序采用非常大的方式，获取有关每隔一个月的慌慌张张的电话呼叫的平均和他们没有进行此规划。 和其指定类似于:"Help ！ 我把所有内容放在单个数据存储，并在长达 45 天我要对其运行空间不足 ！" 并且如果有大量的业务逻辑中内置了如何访问数据存储区，并且必须使用您的应用程序的客户，没有任何迁移时停机的某一天的好时机。 我们最终会其数据 herculean 工作，以帮助客户分区经过动态无需停机。 它是非常令人兴奋、 非常可怕，并且不是你想要参与如果能避免 ！ 预先考虑这和将其集成到您的应用程序将使您的生活变得更加轻松如果应用程序的增长更高版本。

## <a name="summary"></a>总结

有效的分区方案可以让你的云应用程序扩展到千万亿字节的数据而无需瓶颈在云中。 同时，无需预先为大规模机或广泛的基础结构即用即付可能就像在本地数据中心中运行应用程序。 云可在你可以根据需要并且你只付钱让尽可能使用当你使用此选项以增量方式添加容量。

在中[接下来的章节](unstructured-blob-storage.md)我们将了解如何修复它应用实现通过将图像存储在 Blob 存储中的垂直分区。

## <a name="resources"></a>资源

有关分区策略的详细信息，请参阅以下资源。

文档：

- [Windows Azure 云服务上的大规模服务的设计的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 Mark Simms 和 Michael Thomassy 白皮书。
- [Microsoft 模式和实践的云设计模式](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅数据分区指南，分片模式。

视频：

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分组成的系列 Ulrich Homann、 Marc Mercuri 和 Mark Simms。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 请参阅第 7 中的分区描述。
- [构建大型： 从 Windows Azure 客户的第 I 到的经验教训](https://channel9.msdn.com/Events/Build/2012/3-029)。Mark Simms 讨论了分区方案，分片策略如何实现分片和 SQL Database 联合，开始 19:49。 类似于防故障系列但进入操作方法的更多详细信息。

示例代码：

- [云服务在 Windows Azure 中的基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 示例包括分片数据库的应用程序。 有关实现的分片方案的说明，请参阅[DAL – 分片的 RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) Windows Azure 博客上。

> [!div class="step-by-step"]
> [上一页](data-storage-options.md)
> [下一页](unstructured-blob-storage.md)
