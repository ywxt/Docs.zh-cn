---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 构建实际云应用程序使用 Azure |Microsoft Docs
author: MikeWasson
description: 这本电子书将指导你通过基于模式的方法构建实际云解决方案。 这些模式适用于开发流程以及与...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: 15e5c0a0411e3cd9433544e9a09b6373311daf6b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396209"
---
<a name="building-real-world-cloud-apps-with-azure"></a>使用 Azure 构建实际云应用
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 这本电子书将指导你通过基于模式的方法构建实际云解决方案。 这些模式适用于开发流程以及体系结构和编码实践。
> 
> 其内容基于演示文稿由 Scott Guthrie 开发并通过他的挪威开发人员大会 (NDC) 中传递的 2013 年 6 月 ([第 1 部分](http://vimeo.com/68215538)，[第 2 部分](http://vimeo.com/68215602))，而是在 Microsoft Tech Ed 澳大利亚中2013 年 9 月，([第 1 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)，[第 2 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325))。 [许多其他](more-patterns-and-guidance.md#acknowledgments)更新和增加内容时从视频转换为书面形式。


## <a name="intended-audience"></a>目标的受众

很想知道云，开发的迁移到云，或云开发新手开发人员将在此处查找最重要的概念和实践他们需要了解的简要概述。 使用具体的示例和每个章节链接到其他资源的更深入的信息说明了概念。 示例和其他资源的链接是针对 Microsoft 框架与服务，但其阐释的原理适用于其他 web 开发框架和云的环境，以及。

已开发针对云开发人员可能会发现想法此处，可帮助使其更大的成功。 因此您可以选择，然后选择你感兴趣的主题，可以独立地读取序列中的每一章。

观看 Scott Guthrie 的任何人*构建真实世界云应用，使用 Azure*演示文稿并希望获得更多详细信息和更新的信息将在此处查找的。

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>云开发模式

这本电子书介绍了十三个建议的云开发模式。 "模式"所用此处广义上讲表示执行操作的推荐的方法： 如何最好地着手开发、 设计和编码的云应用。 这些是关键模式，可以借助此"归为成功的陷阱"如果您遵循它们。

- [使一切自动化](automate-everything.md)。

    - 使用脚本来最大限度地提高效率和最大程度减少重复的操作过程中的错误。
    - 演示： Azure 管理脚本。
- [源代码管理](source-control.md)。 

    - 设置源代码管理中的分支结构，以便于 DevOps 工作流。
    - 演示： 将脚本添加到源代码管理。
    - 演示： 保持敏感数据不受源代码管理。
    - 演示： 在 Visual Studio 中使用 Git。
- [持续集成和交付](continuous-integration-and-continuous-delivery.md)。 

    - 自动执行生成和部署每个源控件中签入。
- [Web 开发最佳做法](web-development-best-practices.md)。 

    - 保留 web 层无状态。
    - 演示： 缩放和自动缩放 Azure 应用服务中的 Web 应用中。
    - 避免会话状态。
    - 当 CDN 不可用时，备用方案使用 CDN。
    - 使用异步编程模型。
    - 演示： 在 ASP.NET MVC 和 Entity Framework 的异步。
- [单一登录](single-sign-on.md)。 

    - Azure Active Directory 简介。
    - 演示： 创建使用 Azure Active Directory 的 ASP.NET 应用程序。
- [数据存储选项](data-storage-options.md)。 

    - 类型的数据存储。
    - 如何选择适当的数据存储。
    - 演示： Azure SQL 数据库。
- [数据分区策略](data-partitioning-strategies.md)。 

    - 垂直、 水平分区数据或为了便于扩展关系数据库。
- [非结构化的 blob 存储](unstructured-blob-storage.md)。 

    - 使用 blob 服务在云中存储文件。
    - 演示： 修复其应用中使用 blob 存储。
- [若要从故障中恢复的设计](design-to-survive-failures.md)。 

    - 类型的故障。
    - 故障范围。
    - 了解 Sla。
- [监视和遥测](monitoring-and-telemetry.md)。 

    - 为什么应同时购买的遥测数据应用程序和编写你自己的代码来检测您的应用程序。
    - 适用于 Azure 的演示： New Relic
    - 演示： 在 Fix It 应用登录代码。
    - 演示： 修复其应用中的依赖关系注入。
    - 演示： 在 Azure 中的内置日志记录支持。
- [暂时性故障处理](transient-fault-handling.md)。 

    - 使用智能重试/回退逻辑来缓解暂时性故障的影响。
    - 演示： 重试/回退 Entity Framework 6 中。
- [分布式缓存](distributed-caching.md)。 

    - 提高可伸缩性和降低数据库事务成本，通过使用分布式缓存。
- [以队列为中心的工作模式](queue-centric-work-pattern.md)。 

    - 启用高可用性，并通过松散耦合 web 和辅助角色层来提高可伸缩性。
    - 演示： 修复其应用中的 Azure 存储队列。
- [云应用程序模式和指南的详细信息](more-patterns-and-guidance.md)。
- [附录：“Fix It”示例应用程序](the-fix-it-sample-application.md)

    - 已知问题
    - 最佳做法
    - 如何下载、 构建、 运行和部署。

这些模式适用于所有云环境，但我们将通过使用基于 Microsoft 技术和服务，例如 Visual Studio、 Team Foundation Service、 ASP.NET 和 Azure 的示例演示它们。

这一章的余下内容介绍 Fix It 示例应用程序和修复其应用在中运行的 Azure 应用服务云环境中的 Web 应用。

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>示例应用程序修补程序

此电子书中所示的代码示例的屏幕截图的大多数基于 Fix It 应用最初由[Scott Guthrie](https://weblogs.asp.net/scottgu/)来演示推荐的云应用开发模式和实践。

![修复此错误应用主页](introduction/_static/image1.png)

示例应用是票证系统的简单工作项。 当您需要解决某些问题时，创建票证和分配到人，以及其他可以登录并查看分配的票证到它们，并将票证标记为完成时完成工作。

它是一个标准的 Visual Studio web 项目。 它基于 ASP.NET MVC，并使用 SQL Server 数据库。 它可以在 IIS Express 中本地运行，并且可被部署到 Azure 网站云中运行。 你可以记录在使用窗体身份验证和本地数据库或通过使用如 Google 的社交提供程序。 （稍后我们还将展示如何使用 Active Directory 组织帐户登录。）

![登录页](introduction/_static/image2.png)

登录后在创建票证、 将其分配给某人，和上传你想要获取已修复的图片。

![创建 Fix It 任务](introduction/_static/image3.png)

![修复此错误创建任务](introduction/_static/image4.png)

您可以跟踪你创建的工作项的进度，请参阅分配给查看票证详细信息，并将邮件标记为已完成的票证。

这是一个非常简单的应用程序，从功能角度看，但您将了解如何生成它，以便它可以扩展到数以百万计的用户，并将能够弹性应对数据库故障和连接终止等内容。 您还将了解如何创建自动化和敏捷开发工作流，这样就可以开始简单和高效和快速迭代开发周期，更好和更好地使应用程序。

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>在 Azure 应用服务中 web 应用

用于修复其应用程序的云环境是 Azure，我们调用 Web 站点的服务。 此服务是一种方法，您可以托管你自己在 Azure 中的 web 应用，而无需创建 Vm 并保持最新、 安装和配置 IIS，等等。我们在 Vm 上托管你的站点，并自动提供备份和恢复以及用于你的其他服务。 网站服务适用于 ASP.NET、 Node.js、 PHP 和 Python。 这样可以非常快速地使用 Visual Studio、 Webdeploy、 FTP、 Git 或 TFS 进行部署。 它通常是在启动部署时与你的更新可通过 Internet 的时间之间只需几秒。 它是完全免费，若要开始，并根据流量的增长可以增加。

在后台，Azure 应用服务中的 Web 应用提供了大量的体系结构组件和功能，您将不得不自己进行构建，如果您将拥有一个使用你自己的 Vm 上的 IIS 网站。 一个组件是自动配置 IIS，并将在你想要运行你的站点的所有 Vm 上安装应用程序部署终结点。

![部署服务](introduction/_static/image5.png)

当用户点击 web 站点时，它们不会直接达到 IIS Vm，它们经历[应用程序请求路由 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)负载均衡器。 可以使用它们与您自己的服务器，但其优点在于，它们为你自动设置。 他们使用智能启发式方法，将考虑几个因素： 会话相关性，在 IIS 中，队列深度和每个 CPU 使用情况机器流量定向到 Vm 承载您的网站。

![ARR 负载均衡器](introduction/_static/image6.png)

如果一台计算机出现故障，Azure 自动从轮转提取、 启动新的 VM 实例，并开始将流量定向到新实例，所有与你的应用程序没有停机时间。

![从计算机发生故障自动恢复](introduction/_static/image7.png)

所有这些自动发生。 需要做的只是创建网站和应用程序部署到它，使用 Windows PowerShell、 Visual Studio 中或在 Azure 管理门户。

快速而简单分步教程演示如何在 Visual Studio 中创建 web 应用程序并将其部署到 Azure 网站，请参阅[开始使用 Azure 和 ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。

<a id="summary"></a>
## <a name="summary"></a>总结

本简介提供了一系列主题将介绍一书中，示例应用程序的屏幕截图和 Azure 应用服务云环境中的 Web 应用的简要概述。 开发应用程序中和云的最大好处之一是很容易地自动执行重复的开发任务，例如创建测试环境，并将代码部署到它。 如何执行的操作的使用者[接下来的章节](automate-everything.md)。

## <a name="resources"></a>资源

在这一章中所涵盖主题的详细信息，请参阅以下资源。

文档：

- [Azure 应用服务中的 web 应用](https://azure.microsoft.com/services/app-service/web/)。 有关 Web 应用的 Azure 文档的门户页。
- [Web 应用、 云服务和 Vm： 何时使用何？](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) 只可以在 Azure 中运行 web 应用的三种方式之一 WAWS 这一章中所示。 本文介绍的三种方法之间的差异，并提供有关如何选择哪一个适合你的方案的指南。 例如网站、 云服务是 Azure PaaS 功能。 Vm 是 IaaS 功能。 PaaS 与 IaaS 的说明，请参阅[数据选项](data-storage-options.md#paasiaas)一章。

视频：

- [Scott Guthrie 开始步骤 0-什么是 Azure 云操作系统？](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [网站的体系结构-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。
- [Azure 网站内部结构与 Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。

> [!div class="step-by-step"]
> [下一篇](automate-everything.md)
