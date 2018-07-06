---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: 以队列为中心的工作模式 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: f9916e4ecbe6234ee12bcb56519e7e2c0e490972
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840183"
---
<a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>以队列为中心的工作模式 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


更早版本，我们看到的那样，使用多个服务可能会导致"复合"SLA，其中是应用的有效 SLA*产品*的单独的 Sla。 例如，修复其应用程序使用网站、 存储和 SQL 数据库。 如果这些服务的任何一个失败时，应用将向用户返回错误。

缓存是好的方法来处理暂时性故障的只读的内容。 但是，如果应用程序需要进行的工作？ 例如，当用户提交新的 Fix It 任务，该应用程序不能只是将此任务放置到缓存。 应用程序需要将 Fix It 任务写入到永久性数据存储，以便可以进行处理。

这是以队列为中心的工作模式的作用所在。 此模式可让 web 层和后端服务之间的松散耦合。

下面是该模式的工作原理。 当应用程序获取请求时，它的工作项放入队列，并立即返回响应。 然后单独的后端进程中拉取队列中的工作项，并执行工作。

以队列为中心的工作模式非常有用：

- 较长时间 （高延迟） 的工作。
- 需要可能始终不可用的外部服务的工作。
- 它是工作占用大量资源 （cpu 使用率较高）。
- 受益于 （取决于突发性负载突发） 调节率的工作。

## <a name="reduced-latency"></a>减少的延迟

队列可的随时执行耗时的工作。 如果任务需要几秒钟或更长，而不是阻止最终用户，放入队列工作项。 告诉用户"我们正在努力，"，然后使用队列侦听器来处理在后台任务。

例如，当你购买在线零售商的内容，网站上确认你的订单立即。 但这并不意味着你的内容已在卡车传递。 将任务放在队列中，且在后台进行信用检查，供发运，准备你的项和它们等等。

对于较短的延迟的情况下，总的端到端时间可能较长使用队列，与以同步方式执行该任务。 但即使这样，其他好处可以超过该缺点。

## <a name="increased-reliability"></a>更高的可靠性

在修复它，我们介绍了在到目前为止的版本中，web 前端与 SQL 数据库后端紧密耦合。 如果 SQL 数据库服务不可用，用户会收到错误。 如果重试不起作用 （也就是说，故障是多个暂时性的），可以执行的唯一操作是显示错误，并要求用户稍后再试。

![关系图显示 web 前端失败的 SQL 数据库后端的失败时](queue-centric-work-pattern/_static/image1.png)

使用队列，当用户提交 Fix It 任务，该应用程序向队列写入消息。 消息有效负载[JSON](http://json.org/)任务的表示形式。 一旦将消息写入队列，该应用返回并立即向用户显示一条成功消息。

如果任何后端服务，如 SQL 数据库或队列侦听器--处于脱机状态，用户仍然可以提交新 Fix It 任务。 之前的后端服务会重新可用，只需将排队等待消息。 此时后, 端服务将同步在积压工作上。

![Web 前端持续运行 SQL 数据库错误时显示的关系图](queue-centric-work-pattern/_static/image2.png)

此外，现在您可以添加更多的后端逻辑而无需担心前端的复原能力。 例如，你可能想要时新修复为它分配给所有者发送电子邮件或短信。 如果电子邮件或 SMS 服务变为不可用，可以处理其他任何内容，，然后将消息放入单独的队列用于发送电子邮件/短信。

以前，我们有效的 SLA 是 Web 应用&times;存储&times;SQL 数据库 = 99.7%。 (请参阅[设计，以从故障中恢复](design-to-survive-failures.md)。)

当我们更改应用程序以使用队列时，web 前端仅取决于 Web 应用和存储，为复合 99.8%的 SLA。 （请注意，队列将是 Azure 存储服务的一部分，因此将它们包括在相同的 SLA 作为 blob 存储）。

如果需要比 99.8%甚至更好，您可以在两个不同区域中创建两个队列。 将一个作为主，另一个指定为辅助数据库。 在应用中，故障转移到辅助队列如果主队列不可用。 这两个不可在同一时间的机会是非常小。

## <a name="rate-leveling-and-independent-scaling"></a>调节率和独立扩展性

队列还可以用于所谓*速率调节*或*负载分级*。

Web 应用很容易就激增的流量。 虽然可以使用自动缩放会自动添加 web 服务器来处理增加的 web 流量，自动缩放可能不能以足够快的速度响应来处理突然发生的负载高峰。 如果 web 服务器可以将卸载的一些工作要执行的操作向队列写入一条消息，它们可以处理更多流量。 然后后, 端服务可以从队列中读取消息并处理它们。 队列深度将进行扩大或收缩随着传入负载的变化。

其中许多其耗时的工作转移到后端服务，web 层可以更轻松地响应突发流量高峰。 和您节约资金，因为更少的 web 服务器可以处理任意给定的数量的流量。

您可以独立缩放的 web 层和后端服务。 例如，可能需要三个 web 服务器，但只有一个服务器处理队列消息。 或者，如果要在后台运行计算密集型任务，则可能需要更多的后端服务器。

![](queue-centric-work-pattern/_static/image3.png)

自动缩放适用于后端服务以及 web 层。 可以纵向扩展或缩减正在处理的任务在队列中，基于后端 Vm 的 CPU 使用情况的 Vm 数量。 或者，可以根据队列中有多少项自动缩放。 例如，您可以告诉自动缩放来尝试保留在队列中的不超过 10 个项。 如果队列有 10 个以上的项，则自动缩放会将 Vm 添加。 当它们赶上时，自动缩放将拆解额外的 Vm。

## <a name="adding-queues-to-the-fix-it-application"></a>添加到修补程序对其进行排队应用程序

若要实现队列模式，我们需要执行两项更改修复其应用到。

- 当用户提交新的 Fix It 任务时，请将此任务放置在队列中，而不是写入到数据库。
- 创建一个后端服务来处理队列中的消息。

对于队列中，我们将使用[Azure 队列存储服务](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)。 另一种方法是使用[Azure 服务总线](https://docs.microsoft.com/azure/service-bus/)。

若要确定要使用的队列服务，请考虑如何应用需要发送和接收消息的队列中：

- 如果必须协同生产者和使用者竞争，请考虑使用 Azure 队列存储服务。 "联合生成者"意味着多个进程都将消息添加到队列。 "使用者竞争"意味着多个进程正在请求从队列的消息来处理，但任意给定的消息只能处理由一个"使用者。" 如果需要比使用单个队列可以获得更大的吞吐量，，使用其他队列和/或其他存储帐户。
- 如果你需要[发布/订阅模型](http://en.wikipedia.org/wiki/Publish/subscribe)，请考虑使用 Azure 服务总线队列。

Fix It 应用适合协同生成者和竞争使用者模型。

另一个注意事项是应用程序的可用性。 队列存储服务是我们用于 blob 存储，因此使用它没有任何影响我们的 SLA 的相同服务的一部分。 Azure 服务总线是借助其自己的 SLA，单独的服务。 如果我们使用服务总线队列，我们必须考虑其他的 SLA 百分比，和我们的复合 SLA 是较低。 选择队列服务，请确保您了解您选择对应用程序可用性的影响。 有关详细信息，请参阅[资源](#resources)部分。

## <a name="creating-queue-messages"></a>创建队列消息

若要在队列上将 Fix It 任务，web 前端，请执行以下步骤：

1. 创建[CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx)实例。 `CloudQueueClient`实例用于针对队列服务执行请求。
2. 创建队列，如果它尚不存在。
3. 序列化 Fix It 任务。
4. 调用[CloudQueue.AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx)将消息放入队列。

我们将完成这项工作在构造函数和`SendMessageAsync`方法的一个新`FixItQueueManager`类。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

此处我们使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库进行序列化到 JSON 格式 fix it。 可以使用你喜欢的任何序列化方法。 JSON 具有的优点是用户可读，而且比 XML 更简便。

生产品质的代码将添加错误处理逻辑、 暂停如果数据库变得不可用、 更彻底地处理恢复、 在应用程序启动时创建队列和管理"[有害"消息](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)。 （病毒消息是由于某种原因无法处理的消息。 您不希望有害消息进入队列，其中辅助角色将不断尝试处理它们、 失败、 重试、 失败，依次类推。）

在前端的 MVC 应用程序中，我们需要更新创建新任务的代码。 而不是将任务放入存储库，调用`SendMessageAsync`如上所示的方法。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>处理队列消息

若要处理队列中的消息，我们将创建的后端服务。 后端服务将运行无限循环，执行以下步骤：

1. 从队列获取下一条消息。
2. 反序列化到 Fix It 任务消息。
3. Fix It 任务写入数据库。

若要托管后端服务，我们将创建一个 Azure 云服务，包含*辅助角色*。 辅助角色包含一个或多个 Vm，可以执行后端处理。 在这些虚拟机中运行的代码将请求消息从队列作为它们变得可用。 对于每个消息中，我们将反序列化的 JSON 有效负载并修复它任务实体的实例将写入数据库，使用我们之前在 web 层中使用的相同存储库。

以下步骤说明如何添加工作线程角色项目具有标准的 web 项目的解决方案。 已修复它在项目中，您可以下载完成这些步骤。

第一次将云服务项目添加到 Visual Studio 解决方案。 右键单击解决方案并选择**外**，然后**新项目**。 在左窗格中，展开**Visual C#** ，然后选择**云**。

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

在中**新的 Azure 云服务**对话框中，展开**Visual C#** 在左窗格中的节点。 选择**辅助角色**，然后单击右箭头图标。

![](queue-centric-work-pattern/_static/image6.png)

(请注意，您还可以添加*web 角色*。 我们可以运行修复它前端而非运行在 Azure 网站在相同云服务中。 具有一些优势中轻松地协调前端和后端之间的连接。 但是，为了简化本演示，我们保持前端在 Azure 应用服务 Web 应用和仅在云服务中运行后端。）

默认名称分配给辅助角色。 若要更改名称，将鼠标悬停在右窗格中，辅助角色，然后单击铅笔图标。

![](queue-centric-work-pattern/_static/image7.png)

单击**确定**以完成对话框。 这会将两个项目添加到 Visual Studio 解决方案。

- Azure 项目，用于定义云服务，包括配置信息。
- 辅助角色项目，用于定义辅助角色。

![](queue-centric-work-pattern/_static/image8.png)

有关详细信息，请参阅[使用 Visual Studio 创建 Azure 项目。](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

在辅助角色中，我们轮询消息通过调用`ProcessMessageAsync`方法的`FixItQueueManager`我们早先看到的类。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync`方法检查是否正在等待消息。 如果没有一个，它反序列化到消息`FixItTask`实体，并将实体保存在数据库中。 它循环执行，直到队列为空。

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

轮询队列消息会产生较小的事务进行收费，因此，如果没有消息等待处理，辅助角色`RunAsync`方法将等待秒轮询之前再次通过调用`Task.Delay(1000)`。

在 web 项目中，添加异步代码可自动提高性能，因为 IIS 管理有限的线程池。 不是辅助角色项目中的用例。 若要提高可伸缩性的辅助角色，你可以编写多线程的代码或使用异步代码来实现[并行编程](https://msdn.microsoft.com/library/ff963553.aspx)。 该示例不会实现并行编程，但显示了如何使代码异步，因此可以实现的并行编程。

## <a name="summary"></a>总结

在本章中，你已了解如何通过实现以队列为中心的工作模式来提高应用程序响应能力、 可靠性和可伸缩性。

这是此电子书中介绍的 13 模式的最后一个，但当然还有许多其他模式和实践，从而帮助您构建成功的云应用程序。 [最后一章](more-patterns-and-guidance.md)并未涵盖这些 13 模式中的主题提供了资源链接。

<a id="resources"></a>
## <a name="resources"></a>资源

有关队列的详细信息，请参阅以下资源。

文档：

- [Microsoft Azure 存储队列第 1 部分： 入门](http://justazure.com/microsoft-azure-storage-queues-part-1-getting-started/)。 Roman Schacherl 的文章。
- [执行后台任务](https://msdn.microsoft.com/library/ff803365.aspx)的第 5 章[应用程序移动到云，第三版](https://msdn.microsoft.com/library/ff728592.aspx)从 Microsoft 模式和实践。 (具体而言，部分["使用 Azure 存储队列"](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。)
- [最大程度提高可伸缩性和成本的效益的 Azure 上的基于队列的消息传送解决方案的最佳做法](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)。 Valery Mizonov 的白皮书。
- [比较 Azure 队列和服务总线队列](https://msdn.microsoft.com/magazine/jj159884.aspx)。 MSDN 杂志 》 文章提供了可帮助您选择要使用的队列服务的其他信息。 该文档提到服务总线是依赖于 ACS 进行身份验证，这意味着 SB 队列将不可用时 ACS 将不可用。 但是，因为在撰写本文时，SB 已更改为使你能够使用[SAS 令牌](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx)作为 ACS 的替代方法。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅异步消息传送入门、 管道和筛选器模式，补偿事务模式，使用者竞争模式、 CQRS 模式。
- [CQRS 旅程](https://msdn.microsoft.com/library/jj554200)。 了解 CQRS，Microsoft 模式与实践中的电子书。

视频：

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分由 Ulrich Homann、 Marc Mercuri 和 Mark Simms 的视频系列。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 有关 Azure 存储服务和队列的介绍，请参阅第 5 开始 35:13。

> [!div class="step-by-step"]
> [上一页](distributed-caching.md)
> [下一页](more-patterns-and-guidance.md)
