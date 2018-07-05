---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web 开发最佳做法 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: f31798032c3b690fcb6dfa8326580255f3412826
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371033"
---
<a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web 开发最佳做法 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


前三个模式那样设置敏捷开发过程;其余部分是有关体系结构和代码。 这个是一系列 web 开发最佳做法：

- [无状态 web 服务器](#stateless)智能负载均衡器后面。
- [避免会话状态](#sessionstate)（或者如果无法避免，使用分布式的缓存而不是数据库）。
- [使用 CDN](#cdn)边缘缓存静态文件资产 （图像、 脚本）。
- [使用.NET 4.5 的异步支持](#async)以避免阻止调用。

这些实践适用于所有的 web 开发，而不仅仅是对云应用程序，但它们对云应用程序尤为重要。 它们协同工作以帮助您更好地利用云环境提供高度灵活缩放。 如果不遵循这些实践，您会遇到限制，当您尝试缩放应用程序。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>智能负载均衡器后面的无状态 web 层

*无状态 web 层*意味着不要将任何应用程序数据存储在 web 服务器的内存或文件系统中。 保持无状态 web 层，可同时提供更好的客户体验并节省运营成本：

- 如果 web 层是无状态，并且它位于负载均衡器后，你可以快速响应的应用程序流量中的更改，通过动态添加或删除服务器。 在云环境中，只需支付的服务器资源，只要你实际使用，该响应的需求变化的能力可以转换为多么大的节省。
- 无状态 web 层是体系结构方面更易于横向扩展应用程序。 也可用于响应更快地缩放需求和成本更低但花上开发和测试过程中。
- 云服务器，如在本地服务器，需要完成修补和偶尔; 重新启动并且，如果无状态 web 层，当服务器暂时出现故障时重新路由流量不会导致错误或意外的行为。

大多数实际的应用程序需要 web 会话; 存储状态这里的主要意思并不是将其存储在 web 服务器上。 在 cookie 中或从进程服务器端 ASP.NET 会话状态使用缓存提供程序中的客户端上，可以如存储在其他方面的状态。 可以存储在文件中的[Windows Azure Blob 存储](unstructured-blob-storage.md)而不是本地文件系统。

若要缩放的应用程序在 Windows Azure 网站中，如果你的 web 层是无状态是多么的示例，请参阅**规模**选项卡上为 Windows Azure 网站管理门户中：

![缩放选项卡](web-development-best-practices/_static/image1.png)

如果你想要添加 web 服务器，您可以只是向右拖动实例计数滑块。 设置为 5，然后单击**保存**，几秒钟内有 5 个 web 服务器处理网站的流量的 Windows Azure 中。

![五个实例](web-development-best-practices/_static/image2.png)

您可以轻松地设置实例计数 3 下或到 1。 当你扩展后时，开始省钱立即因为 Windows Azure 费用按分钟，不按小时数。

此外可以指示 Windows Azure 自动增加或减少根据 CPU 使用率的 web 服务器的数量。 在以下示例中，当 CPU 使用率低于 60%，web 服务器的数量将减少至最小为 2，而且，如果 CPU 使用率高于 80%，web 服务器的数量将增加最大为 4。

![按 CPU 使用率扩展](web-development-best-practices/_static/image3.png)

或者，如果您知道，你的站点将只是忙在工作时间内？ 您可以指示 Windows Azure 在白天运行多个服务器，并减少至 evenings、 加班，一台服务器和周末。 以下一系列屏幕快照显示了如何将网站设置为在工作时间从上午 8 点到下午 5 点运行一台服务器在空闲时间和 4 台服务器。

![按计划缩放](web-development-best-practices/_static/image4.png)

![设置计划时间](web-development-best-practices/_static/image5.png)

![Daytime 计划](web-development-best-practices/_static/image6.png)

![Weeknight 计划](web-development-best-practices/_static/image7.png)

![周末计划](web-development-best-practices/_static/image8.png)

当然可以在脚本中也同样如下所示在门户中完成所有这些。

若要横向扩展应用程序的功能是几乎无限制的 Windows Azure 中，处理程序，但前提是避免妨碍动态添加或删除服务器的 Vm，通过将 web 层保持无状态。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>避免会话状态

它通常是不现实中实际云应用程序以避免存储某种形式的状态，以便用户会话，但某些方法影响性能和可伸缩性比其他更多。 如果必须存储状态，最佳解决方案是使状态量小，并将其存储在 cookie 中。 如果这不可行下, 一步最佳解决方案是使用 ASP.NET 会话状态提供程序[分布式内存中缓存](distributed-caching.md#sessionstate)。 从性能和可伸缩性的角度来看最差的解决方案是使用数据库支持的会话状态提供程序。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>使用 CDN 来缓存静态文件资产

CDN 是内容交付网络的首字母缩写。 您提供给 CDN 提供商，如图像和脚本文件的静态文件资产和提供程序，以便用户访问你的应用程序，无论他们有相对较快的响应和低延迟的缓存可以缓存这些文件在世界各地的数据中心中资产。 这加快了站点的总体负载时间并减少 web 服务器上的负载。 Cdn 是尤为重要，如果到达的受众的分布广泛地理位置。

Windows Azure 提供 CDN，而可以在 Windows Azure 或任何 web 托管环境中运行的应用程序中使用其他 Cdn。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>使用.NET 4.5 的异步支持以避免阻止调用

.NET 4.5 增强的 C# 和 VB 的编程语言，以使其以异步方式处理任务要简单得多。 异步编程的好处不再仅仅用于并行处理的情况下，例如当你想要同时启动多个 web 服务调用。 它还使 web 服务器，以更有效地执行和可靠的高负载条件下。 在 web 服务器仅具有有限的数量的线程可用，并且在高负载条件下时的所有线程都在使用中，传入的请求必须等待，直到线程被释放。 如果应用程序代码不会处理任务，例如异步数据库查询和 web 服务调用，多线程服务器等待 I/O 响应时不必要地关联起来。 这将限制的服务器能够在高负载条件下处理的流量。 使用异步编程时，线程正在等待 web 服务或数据库返回数据最新请求提供服务之前释放数据接收到。 在繁忙的 web 服务器，数百或数千个请求可以然后处理立即其中否则会等待线程释放了。

您先前看到的很容易减少处理您的网站，因为它是以提高它们的 web 服务器的数目。 因此如果一个服务器可以实现更大的吞吐量，则不需要为许多它们，你可以降低成本，因为需要更少的服务器为给定的流量否则相比。

在 ASP.NET 4.5 Web 窗体、 MVC 和 Web API; 包含.NET 4.5 的异步编程模型的支持在实体框架 6，并在[Windows Azure 存储 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)。

### <a name="async-support-in-aspnet-45"></a>在 ASP.NET 4.5 中异步支持

在 ASP.NET 4.5 支持异步编程新增了对不只是为语言，而且还 MVC、 Web 窗体和 Web API 框架。 例如，ASP.NET MVC 控制器操作方法接收来自 web 请求的数据，并将数据传递给视图然后再创建要发送到浏览器的 HTML。 频繁的操作方法需要从数据库或 web 服务获取数据，以便显示在网页上或保存在网页中输入的数据。 在这些情况下很容易地使异步操作方法： 而不是返回*ActionResult*对象，则返回*任务&lt;ActionResult&gt;* 和标记的方法与*异步*关键字。 在方法中，当涉及到等待时间的操作启动了一行代码时你将其标记使用 await 关键字。

下面是为数据库查询调用的存储库方法的简单的操作方法：

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

而以下是以异步方式处理数据库调用的相同方法：

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

在后台编译器将生成相应的异步代码。 当应用程序发出的调用`FindTaskByIdAsync`，ASP.NET 可`FindTask`请求和展开工作线程并使数据可用于处理其他请求。 当`FindTask`操作的请求，一个线程重新启动以继续处理该调用之后的代码。 在此期间之间时`FindTask`发起请求并且时返回的数据，必须可用于执行有用的工作，否则为将会等待响应相关联的线程。

异步代码的一些系统开销，但在低负载情况下这些开销不计，同时在你能够处理等待可用线程都将保留的请求的高负载条件下。

它就可以进行异步编程以来 ASP.NET 1.1 中，这种类型，但却难以编写、 容易出错且难以调试。 现在，我们简化了编码为其 ASP.NET 4.5 中，没有理由这样做了。

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6 中的异步支持

4.5 中异步支持的一部分，我们提供异步支持 web 服务调用、 套接字和文件系统 I/O，但 web 应用程序的最常见模式是命中数据库和我们的数据的库不支持异步。 现在 Entity Framework 6 添加了对数据库访问权限的异步支持。

Entity Framework 6 中会导致查询或命令发送到数据库的所有方法都具有异步版本。 此处的示例显示的异步版本*查找*方法。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

与此异步支持适用于不只是插入、 删除、 更新和简单的查找，则它还会使用 LINQ 查询：

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

没有`Async`版本的`ToList`方法因为就在此代码中，则查询发送到数据库的方法。 `Where`并`OrderByDescending`方法仅配置查询，而`ToListAsync`方法执行查询，并将存储中的响应`result`变量。

## <a name="summary"></a>总结

可以实现在任何 web 编程框架和任何云环境，此处所述的 web 开发最佳实践，但我们有方便的 ASP.NET 和 Windows Azure 中的工具。 如果您遵循这些模式，您可以轻松地扩展 web 层，并要尽可能减少您的费用，因为每个服务器将能够处理更多流量。

[接下来的章节](single-sign-on.md)探讨如何在云中实现单一登录方案。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源。

无状态 web 服务器：

- [Microsoft 模式和做法的自动缩放指南](https://msdn.microsoft.com/library/dn589774.aspx)。
- [禁用 ARR 实例在 Windows Azure 网站中的相关性](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)。 由 Erez benari 撰写的博客文章介绍了会话相关性在 Windows Azure 网站中。

CDN:

- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分由 Ulrich Homann、 Marc Mercuri 和 Mark Simms 的视频系列。 请参阅 CDN 讨论中段 3 开始 1:34:00。
- [Microsoft 模式和实践静态内容托管模式](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 评审](http://www.cdnreviews.com/)。 许多 Cdn 的概述。

异步编程：

- [在 ASP.NET MVC 4 中使用异步方法](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。 由 Rick Anderson 的教程。
- [异步编程使用 Async 和 Await （C# 和 Visual Basic）](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)。 介绍用于异步编程的基本原理、 ASP.NET 4.5 中的工作方式以及如何编写代码来实现该 MSDN 白皮书。
- [Entity Framework 异步查询和保存](https://msdn.microsoft.com/data/jj819165)
- [如何生成 ASP.NET Web 应用程序使用 Async](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)。 Rowan Miller 的视频演示文稿。 包括图形演示可以简化异步编程的显著提高了 web 服务器在高负载条件下的吞吐量。
- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分由 Ulrich Homann、 Marc Mercuri 和 Mark Simms 的视频系列。 影响的可伸缩性的异步编程的讨论，请参阅第 4 和 episode 8。
- [使用 ASP.NET 4.5 和重要 gotcha 中的异步方法的神奇之处](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)。 有关在 ASP.NET Web 窗体应用程序中使用 async 主要是 Scott Hanselman 的博客文章。

其他 web 开发最佳做法，请参阅以下资源：

- [解决方法示例应用程序的最佳实践](the-fix-it-sample-application.md#bestpractices)。 这本电子书的附录列出了大量修复其应用程序中实现的最佳做法。
- [Web 开发人员检查表](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [上一页](continuous-integration-and-continuous-delivery.md)
> [下一页](single-sign-on.md)
