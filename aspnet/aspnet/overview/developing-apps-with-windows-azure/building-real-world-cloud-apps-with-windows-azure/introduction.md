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
<a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="a0f6b-104">使用 Azure 构建实际云应用</span><span class="sxs-lookup"><span data-stu-id="a0f6b-104">Building Real-World Cloud Apps with Azure</span></span>
====================
<span data-ttu-id="a0f6b-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a0f6b-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="a0f6b-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="a0f6b-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="a0f6b-107">这本电子书将指导你通过基于模式的方法构建实际云解决方案。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="a0f6b-108">这些模式适用于开发流程以及体系结构和编码实践。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="a0f6b-109">其内容基于演示文稿由 Scott Guthrie 开发并通过他的挪威开发人员大会 (NDC) 中传递的 2013 年 6 月 ([第 1 部分](http://vimeo.com/68215538)，[第 2 部分](http://vimeo.com/68215602))，而是在 Microsoft Tech Ed 澳大利亚中2013 年 9 月，([第 1 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)，[第 2 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325))。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="a0f6b-110">[许多其他](more-patterns-and-guidance.md#acknowledgments)更新和增加内容时从视频转换为书面形式。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>


## <a name="intended-audience"></a><span data-ttu-id="a0f6b-111">目标的受众</span><span class="sxs-lookup"><span data-stu-id="a0f6b-111">Intended Audience</span></span>

<span data-ttu-id="a0f6b-112">很想知道云，开发的迁移到云，或云开发新手开发人员将在此处查找最重要的概念和实践他们需要了解的简要概述。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="a0f6b-113">使用具体的示例和每个章节链接到其他资源的更深入的信息说明了概念。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="a0f6b-114">示例和其他资源的链接是针对 Microsoft 框架与服务，但其阐释的原理适用于其他 web 开发框架和云的环境，以及。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="a0f6b-115">已开发针对云开发人员可能会发现想法此处，可帮助使其更大的成功。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="a0f6b-116">因此您可以选择，然后选择你感兴趣的主题，可以独立地读取序列中的每一章。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="a0f6b-117">观看 Scott Guthrie 的任何人*构建真实世界云应用，使用 Azure*演示文稿并希望获得更多详细信息和更新的信息将在此处查找的。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="a0f6b-118">云开发模式</span><span class="sxs-lookup"><span data-stu-id="a0f6b-118">Cloud development patterns</span></span>

<span data-ttu-id="a0f6b-119">这本电子书介绍了十三个建议的云开发模式。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="a0f6b-120">"模式"所用此处广义上讲表示执行操作的推荐的方法： 如何最好地着手开发、 设计和编码的云应用。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="a0f6b-121">这些是关键模式，可以借助此"归为成功的陷阱"如果您遵循它们。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="a0f6b-122">[使一切自动化](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="a0f6b-123">使用脚本来最大限度地提高效率和最大程度减少重复的操作过程中的错误。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="a0f6b-124">演示： Azure 管理脚本。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="a0f6b-125">[源代码管理](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="a0f6b-126">设置源代码管理中的分支结构，以便于 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="a0f6b-127">演示： 将脚本添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="a0f6b-128">演示： 保持敏感数据不受源代码管理。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="a0f6b-129">演示： 在 Visual Studio 中使用 Git。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="a0f6b-130">[持续集成和交付](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="a0f6b-131">自动执行生成和部署每个源控件中签入。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="a0f6b-132">[Web 开发最佳做法](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="a0f6b-133">保留 web 层无状态。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="a0f6b-134">演示： 缩放和自动缩放 Azure 应用服务中的 Web 应用中。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="a0f6b-135">避免会话状态。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-135">Avoid session state.</span></span>
    - <span data-ttu-id="a0f6b-136">当 CDN 不可用时，备用方案使用 CDN。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="a0f6b-137">使用异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="a0f6b-138">演示： 在 ASP.NET MVC 和 Entity Framework 的异步。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="a0f6b-139">[单一登录](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="a0f6b-140">Azure Active Directory 简介。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="a0f6b-141">演示： 创建使用 Azure Active Directory 的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="a0f6b-142">[数据存储选项](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="a0f6b-143">类型的数据存储。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-143">Types of data stores.</span></span>
    - <span data-ttu-id="a0f6b-144">如何选择适当的数据存储。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="a0f6b-145">演示： Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="a0f6b-146">[数据分区策略](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="a0f6b-147">垂直、 水平分区数据或为了便于扩展关系数据库。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="a0f6b-148">[非结构化的 blob 存储](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="a0f6b-149">使用 blob 服务在云中存储文件。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="a0f6b-150">演示： 修复其应用中使用 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="a0f6b-151">[若要从故障中恢复的设计](design-to-survive-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="a0f6b-152">类型的故障。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-152">Types of failures.</span></span>
    - <span data-ttu-id="a0f6b-153">故障范围。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-153">Failure Scope.</span></span>
    - <span data-ttu-id="a0f6b-154">了解 Sla。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-154">Understanding SLAs.</span></span>
- <span data-ttu-id="a0f6b-155">[监视和遥测](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="a0f6b-156">为什么应同时购买的遥测数据应用程序和编写你自己的代码来检测您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="a0f6b-157">适用于 Azure 的演示： New Relic</span><span class="sxs-lookup"><span data-stu-id="a0f6b-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="a0f6b-158">演示： 在 Fix It 应用登录代码。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="a0f6b-159">演示： 修复其应用中的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="a0f6b-160">演示： 在 Azure 中的内置日志记录支持。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="a0f6b-161">[暂时性故障处理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="a0f6b-162">使用智能重试/回退逻辑来缓解暂时性故障的影响。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="a0f6b-163">演示： 重试/回退 Entity Framework 6 中。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="a0f6b-164">[分布式缓存](distributed-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="a0f6b-165">提高可伸缩性和降低数据库事务成本，通过使用分布式缓存。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="a0f6b-166">[以队列为中心的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="a0f6b-167">启用高可用性，并通过松散耦合 web 和辅助角色层来提高可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="a0f6b-168">演示： 修复其应用中的 Azure 存储队列。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="a0f6b-169">[云应用程序模式和指南的详细信息](more-patterns-and-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="a0f6b-170">附录：“Fix It”示例应用程序</span><span class="sxs-lookup"><span data-stu-id="a0f6b-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="a0f6b-171">已知问题</span><span class="sxs-lookup"><span data-stu-id="a0f6b-171">Known Issues</span></span>
    - <span data-ttu-id="a0f6b-172">最佳做法</span><span class="sxs-lookup"><span data-stu-id="a0f6b-172">Best Practices</span></span>
    - <span data-ttu-id="a0f6b-173">如何下载、 构建、 运行和部署。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="a0f6b-174">这些模式适用于所有云环境，但我们将通过使用基于 Microsoft 技术和服务，例如 Visual Studio、 Team Foundation Service、 ASP.NET 和 Azure 的示例演示它们。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="a0f6b-175">这一章的余下内容介绍 Fix It 示例应用程序和修复其应用在中运行的 Azure 应用服务云环境中的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="a0f6b-176">示例应用程序修补程序</span><span class="sxs-lookup"><span data-stu-id="a0f6b-176">The Fix it sample application</span></span>

<span data-ttu-id="a0f6b-177">此电子书中所示的代码示例的屏幕截图的大多数基于 Fix It 应用最初由[Scott Guthrie](https://weblogs.asp.net/scottgu/)来演示推荐的云应用开发模式和实践。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![修复此错误应用主页](introduction/_static/image1.png)

<span data-ttu-id="a0f6b-179">示例应用是票证系统的简单工作项。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="a0f6b-180">当您需要解决某些问题时，创建票证和分配到人，以及其他可以登录并查看分配的票证到它们，并将票证标记为完成时完成工作。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="a0f6b-181">它是一个标准的 Visual Studio web 项目。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="a0f6b-182">它基于 ASP.NET MVC，并使用 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="a0f6b-183">它可以在 IIS Express 中本地运行，并且可被部署到 Azure 网站云中运行。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="a0f6b-184">你可以记录在使用窗体身份验证和本地数据库或通过使用如 Google 的社交提供程序。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="a0f6b-185">（稍后我们还将展示如何使用 Active Directory 组织帐户登录。）</span><span class="sxs-lookup"><span data-stu-id="a0f6b-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![登录页](introduction/_static/image2.png)

<span data-ttu-id="a0f6b-187">登录后在创建票证、 将其分配给某人，和上传你想要获取已修复的图片。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![创建 Fix It 任务](introduction/_static/image3.png)

![修复此错误创建任务](introduction/_static/image4.png)

<span data-ttu-id="a0f6b-190">您可以跟踪你创建的工作项的进度，请参阅分配给查看票证详细信息，并将邮件标记为已完成的票证。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="a0f6b-191">这是一个非常简单的应用程序，从功能角度看，但您将了解如何生成它，以便它可以扩展到数以百万计的用户，并将能够弹性应对数据库故障和连接终止等内容。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="a0f6b-192">您还将了解如何创建自动化和敏捷开发工作流，这样就可以开始简单和高效和快速迭代开发周期，更好和更好地使应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="a0f6b-193">在 Azure 应用服务中 web 应用</span><span class="sxs-lookup"><span data-stu-id="a0f6b-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="a0f6b-194">用于修复其应用程序的云环境是 Azure，我们调用 Web 站点的服务。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="a0f6b-195">此服务是一种方法，您可以托管你自己在 Azure 中的 web 应用，而无需创建 Vm 并保持最新、 安装和配置 IIS，等等。我们在 Vm 上托管你的站点，并自动提供备份和恢复以及用于你的其他服务。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="a0f6b-196">网站服务适用于 ASP.NET、 Node.js、 PHP 和 Python。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="a0f6b-197">这样可以非常快速地使用 Visual Studio、 Webdeploy、 FTP、 Git 或 TFS 进行部署。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="a0f6b-198">它通常是在启动部署时与你的更新可通过 Internet 的时间之间只需几秒。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="a0f6b-199">它是完全免费，若要开始，并根据流量的增长可以增加。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="a0f6b-200">在后台，Azure 应用服务中的 Web 应用提供了大量的体系结构组件和功能，您将不得不自己进行构建，如果您将拥有一个使用你自己的 Vm 上的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="a0f6b-201">一个组件是自动配置 IIS，并将在你想要运行你的站点的所有 Vm 上安装应用程序部署终结点。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![部署服务](introduction/_static/image5.png)

<span data-ttu-id="a0f6b-203">当用户点击 web 站点时，它们不会直接达到 IIS Vm，它们经历[应用程序请求路由 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)负载均衡器。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="a0f6b-204">可以使用它们与您自己的服务器，但其优点在于，它们为你自动设置。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="a0f6b-205">他们使用智能启发式方法，将考虑几个因素： 会话相关性，在 IIS 中，队列深度和每个 CPU 使用情况机器流量定向到 Vm 承载您的网站。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 负载均衡器](introduction/_static/image6.png)

<span data-ttu-id="a0f6b-207">如果一台计算机出现故障，Azure 自动从轮转提取、 启动新的 VM 实例，并开始将流量定向到新实例，所有与你的应用程序没有停机时间。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![从计算机发生故障自动恢复](introduction/_static/image7.png)

<span data-ttu-id="a0f6b-209">所有这些自动发生。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-209">All of this takes place automatically.</span></span> <span data-ttu-id="a0f6b-210">需要做的只是创建网站和应用程序部署到它，使用 Windows PowerShell、 Visual Studio 中或在 Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="a0f6b-211">快速而简单分步教程演示如何在 Visual Studio 中创建 web 应用程序并将其部署到 Azure 网站，请参阅[开始使用 Azure 和 ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="a0f6b-212">总结</span><span class="sxs-lookup"><span data-stu-id="a0f6b-212">Summary</span></span>

<span data-ttu-id="a0f6b-213">本简介提供了一系列主题将介绍一书中，示例应用程序的屏幕截图和 Azure 应用服务云环境中的 Web 应用的简要概述。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="a0f6b-214">开发应用程序中和云的最大好处之一是很容易地自动执行重复的开发任务，例如创建测试环境，并将代码部署到它。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="a0f6b-215">如何执行的操作的使用者[接下来的章节](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="a0f6b-216">资源</span><span class="sxs-lookup"><span data-stu-id="a0f6b-216">Resources</span></span>

<span data-ttu-id="a0f6b-217">在这一章中所涵盖主题的详细信息，请参阅以下资源。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="a0f6b-218">文档：</span><span class="sxs-lookup"><span data-stu-id="a0f6b-218">Documentation:</span></span>

- <span data-ttu-id="a0f6b-219">[Azure 应用服务中的 web 应用](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="a0f6b-220">有关 Web 应用的 Azure 文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="a0f6b-221">Web 应用、 云服务和 Vm： 何时使用何？</span><span class="sxs-lookup"><span data-stu-id="a0f6b-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="a0f6b-222">只可以在 Azure 中运行 web 应用的三种方式之一 WAWS 这一章中所示。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="a0f6b-223">本文介绍的三种方法之间的差异，并提供有关如何选择哪一个适合你的方案的指南。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="a0f6b-224">例如网站、 云服务是 Azure PaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="a0f6b-225">Vm 是 IaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="a0f6b-226">PaaS 与 IaaS 的说明，请参阅[数据选项](data-storage-options.md#paasiaas)一章。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="a0f6b-227">视频：</span><span class="sxs-lookup"><span data-stu-id="a0f6b-227">Videos:</span></span>

- [<span data-ttu-id="a0f6b-228">Scott Guthrie 开始步骤 0-什么是 Azure 云操作系统？</span><span class="sxs-lookup"><span data-stu-id="a0f6b-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="a0f6b-229">[网站的体系结构-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="a0f6b-230">[Azure 网站内部结构与 Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="a0f6b-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a0f6b-231">下一篇</span><span class="sxs-lookup"><span data-stu-id="a0f6b-231">Next</span></span>](automate-everything.md)
