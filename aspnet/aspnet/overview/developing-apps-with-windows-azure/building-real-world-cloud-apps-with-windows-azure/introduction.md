---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 构建真实世界云应用与 Azure |Microsoft 文档
author: MikeWasson
description: 构建真实世界云解决方案中，此电子书指导你完成基于模式的方法。 模式适用于开发过程以及与...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: 5a62818a2dc21128bb0a42a8b296ade460e7b060
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="17bec-104">使用 Azure 构建真实世界云应用</span><span class="sxs-lookup"><span data-stu-id="17bec-104">Building Real-World Cloud Apps with Azure</span></span>
====================
<span data-ttu-id="17bec-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="17bec-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="17bec-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="17bec-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="17bec-107">构建真实世界云解决方案中，此电子书指导你完成基于模式的方法。</span><span class="sxs-lookup"><span data-stu-id="17bec-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="17bec-108">模式将应用于在开发过程以及体系结构和编码做法。</span><span class="sxs-lookup"><span data-stu-id="17bec-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="17bec-109">内容基于由 Scott Guthrie 开发，而由他在挪威语开发人员大会 （（ndc）） 在 2013 年 6 月中的演示文稿 ([第 1 部分](http://vimeo.com/68215538)，[第 2 部分](http://vimeo.com/68215602))，和中的 Microsoft 技术 Ed 澳大利亚2013 年 9 月，([第 1 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)，[第 2 部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325))。</span><span class="sxs-lookup"><span data-stu-id="17bec-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="17bec-110">[许多其他](more-patterns-and-guidance.md#acknowledgments)更新和从视频将它转换为写入形式时扩充内容。</span><span class="sxs-lookup"><span data-stu-id="17bec-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>


## <a name="intended-audience"></a><span data-ttu-id="17bec-111">目标的受众</span><span class="sxs-lookup"><span data-stu-id="17bec-111">Intended Audience</span></span>

<span data-ttu-id="17bec-112">开发人员想要知道的云开发考虑迁移到云，或以云开发将在此找到的最重要的概念和实践他们需要知道的简要概述。</span><span class="sxs-lookup"><span data-stu-id="17bec-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="17bec-113">并附带具体示例，以及每个章节链接到其他资源的更深入的信息说明了概念。</span><span class="sxs-lookup"><span data-stu-id="17bec-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="17bec-114">示例和其他资源的链接适用于 Microsoft 框架和服务，但是不适用于其他 web 开发框架和云以及环境中所述的原理。</span><span class="sxs-lookup"><span data-stu-id="17bec-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="17bec-115">开发人员已为云开发可能会发现想法此处有助于使它们更成功地。</span><span class="sxs-lookup"><span data-stu-id="17bec-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="17bec-116">因此，你可以选取并选择你感兴趣的主题，可以独立，读取序列中的每一章。</span><span class="sxs-lookup"><span data-stu-id="17bec-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="17bec-117">监视 Scott Guthrie 的任何人*构建真实世界云应用程序与 Azure*演示文稿并希望获得更多详细信息和更新的信息将在此找到的。</span><span class="sxs-lookup"><span data-stu-id="17bec-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="17bec-118">云开发模式</span><span class="sxs-lookup"><span data-stu-id="17bec-118">Cloud development patterns</span></span>

<span data-ttu-id="17bec-119">此电子书说明十三个推荐使用云开发的模式。</span><span class="sxs-lookup"><span data-stu-id="17bec-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="17bec-120">"模式"所用此处广义上讲表示建议的方法是执行操作： 如何最好地着手开发、 设计和编码云应用程序。</span><span class="sxs-lookup"><span data-stu-id="17bec-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="17bec-121">这些是关键的模式，它将帮助你"属于成功的 pit"，如果你遵循它们。</span><span class="sxs-lookup"><span data-stu-id="17bec-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="17bec-122">[使一切自动化](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="17bec-123">使用脚本来最大化效率并最大程度减少重复的操作过程中的错误。</span><span class="sxs-lookup"><span data-stu-id="17bec-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="17bec-124">演示： Azure 的管理脚本。</span><span class="sxs-lookup"><span data-stu-id="17bec-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="17bec-125">[源代码管理](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="17bec-126">设置源代码管理中的分支结构有助于 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="17bec-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="17bec-127">演示： 将脚本添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="17bec-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="17bec-128">演示： 保留出源控件的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="17bec-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="17bec-129">演示： 使用 Visual Studio 中的 Git。</span><span class="sxs-lookup"><span data-stu-id="17bec-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="17bec-130">[持续集成和传递](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="17bec-131">自动生成和每个源控件中签入的部署。</span><span class="sxs-lookup"><span data-stu-id="17bec-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="17bec-132">[Web 开发最佳做法](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="17bec-133">保留 web 层无状态。</span><span class="sxs-lookup"><span data-stu-id="17bec-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="17bec-134">演示： 缩放和自动缩放在 Azure App Service Web Apps 中。</span><span class="sxs-lookup"><span data-stu-id="17bec-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="17bec-135">避免会话状态。</span><span class="sxs-lookup"><span data-stu-id="17bec-135">Avoid session state.</span></span>
    - <span data-ttu-id="17bec-136">CDN 不可用时，请使用 CDN，备用方案。</span><span class="sxs-lookup"><span data-stu-id="17bec-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="17bec-137">使用异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="17bec-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="17bec-138">演示： 在 ASP.NET MVC 和实体框架中的异步。</span><span class="sxs-lookup"><span data-stu-id="17bec-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="17bec-139">[单一登录](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="17bec-140">Azure Active Directory 简介。</span><span class="sxs-lookup"><span data-stu-id="17bec-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="17bec-141">演示： 创建 ASP.NET 应用程序使用 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="17bec-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="17bec-142">[数据存储选项](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="17bec-143">类型的数据存储。</span><span class="sxs-lookup"><span data-stu-id="17bec-143">Types of data stores.</span></span>
    - <span data-ttu-id="17bec-144">如何选择正确的数据存储。</span><span class="sxs-lookup"><span data-stu-id="17bec-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="17bec-145">演示： Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="17bec-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="17bec-146">[数据分区策略](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="17bec-147">垂直、 水平分区数据或这二者便于扩展关系数据库。</span><span class="sxs-lookup"><span data-stu-id="17bec-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="17bec-148">[非结构化的 blob 存储](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="17bec-149">使用 blob 服务在云中存储文件。</span><span class="sxs-lookup"><span data-stu-id="17bec-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="17bec-150">演示： 使用修复它应用中的 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="17bec-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="17bec-151">[设计得以失败](design-to-survive-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="17bec-152">类型的故障。</span><span class="sxs-lookup"><span data-stu-id="17bec-152">Types of failures.</span></span>
    - <span data-ttu-id="17bec-153">失败作用域。</span><span class="sxs-lookup"><span data-stu-id="17bec-153">Failure Scope.</span></span>
    - <span data-ttu-id="17bec-154">了解 Sla。</span><span class="sxs-lookup"><span data-stu-id="17bec-154">Understanding SLAs.</span></span>
- <span data-ttu-id="17bec-155">[监视和遥测](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="17bec-156">为什么应同时购买的遥测应用和编写您自己的代码来检测你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="17bec-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="17bec-157">演示： azure 的 New Relic</span><span class="sxs-lookup"><span data-stu-id="17bec-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="17bec-158">演示： 在修复该应用程序日志记录代码。</span><span class="sxs-lookup"><span data-stu-id="17bec-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="17bec-159">演示： 修复它应用中的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="17bec-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="17bec-160">演示： 在 Azure 中的内置日志记录支持。</span><span class="sxs-lookup"><span data-stu-id="17bec-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="17bec-161">[暂时性故障处理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="17bec-162">使用智能重试/退让逻辑可缓解暂时性故障的影响。</span><span class="sxs-lookup"><span data-stu-id="17bec-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="17bec-163">演示： 重试/退避 Entity Framework 6 中。</span><span class="sxs-lookup"><span data-stu-id="17bec-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="17bec-164">[分布式缓存](distributed-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="17bec-165">提高可伸缩性以及通过使用分布式缓存减少数据库事务成本。</span><span class="sxs-lookup"><span data-stu-id="17bec-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="17bec-166">[以队列为中心的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="17bec-167">启用高可用性，并通过松散耦合 web 和辅助层来提高可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="17bec-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="17bec-168">演示： 修复它应用中的 Azure 存储队列。</span><span class="sxs-lookup"><span data-stu-id="17bec-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="17bec-169">[云应用程序模式和指南的更多](more-patterns-and-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="17bec-170">附录：“Fix It”示例应用程序</span><span class="sxs-lookup"><span data-stu-id="17bec-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="17bec-171">已知问题</span><span class="sxs-lookup"><span data-stu-id="17bec-171">Known Issues</span></span>
    - <span data-ttu-id="17bec-172">最佳做法</span><span class="sxs-lookup"><span data-stu-id="17bec-172">Best Practices</span></span>
    - <span data-ttu-id="17bec-173">如何下载、 生成、 运行和部署。</span><span class="sxs-lookup"><span data-stu-id="17bec-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="17bec-174">这些模式适用于所有云环境中，但我们将使用基于 Microsoft 技术和服务，如 Visual Studio、 Team Foundation Service、 ASP.NET 和 Azure 的示例加以说明。</span><span class="sxs-lookup"><span data-stu-id="17bec-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="17bec-175">此本章的其余部分介绍修复它示例应用程序和修复它应用在中运行的 Azure App Service 云环境中的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="17bec-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="17bec-176">该示例应用程序的修补程序</span><span class="sxs-lookup"><span data-stu-id="17bec-176">The Fix it sample application</span></span>

<span data-ttu-id="17bec-177">大部分的屏幕截图和此电子书中所示的代码示例基于修复它应用最初由[Scott Guthrie](https://weblogs.asp.net/scottgu/)来演示推荐的云应用开发模式和实践。</span><span class="sxs-lookup"><span data-stu-id="17bec-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![修复此错误的应用程序主页](introduction/_static/image1.png)

<span data-ttu-id="17bec-179">示例应用程序是票证系统的简单工作项。</span><span class="sxs-lookup"><span data-stu-id="17bec-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="17bec-180">当你需要解决某些问题时，你创建票证和分配到某人，并且其他人可以登录并查看分配的票证到它们，并将票证标记为已完成时完成的工作。</span><span class="sxs-lookup"><span data-stu-id="17bec-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="17bec-181">它是一个标准的 Visual Studio web 项目。</span><span class="sxs-lookup"><span data-stu-id="17bec-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="17bec-182">它基于 ASP.NET MVC 构建，并使用 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="17bec-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="17bec-183">它可以在 IIS Express 中本地运行，并且可以部署到 Azure 网站在云中运行。</span><span class="sxs-lookup"><span data-stu-id="17bec-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="17bec-184">你可以使用窗体身份验证和本地数据库或通过使用社交提供程序，例如 Google 登录。</span><span class="sxs-lookup"><span data-stu-id="17bec-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="17bec-185">（稍后我们将还演示如何能够使用 Active Directory 组织帐户进行登录。）</span><span class="sxs-lookup"><span data-stu-id="17bec-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![登录页](introduction/_static/image2.png)

<span data-ttu-id="17bec-187">登录后您可以在创建票证、 将它分配给人，并上载你想要获取固定的图片。</span><span class="sxs-lookup"><span data-stu-id="17bec-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![创建修复它任务](introduction/_static/image3.png)

![修复它创建的任务](introduction/_static/image4.png)

<span data-ttu-id="17bec-190">你可以跟踪你创建的工作项的进度，请参阅分配给你、 查看票证详细信息，以及将邮件标记为已完成的票证。</span><span class="sxs-lookup"><span data-stu-id="17bec-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="17bec-191">这是一个非常简单的应用，从功能角度看，但你将了解如何生成它，以便它可以扩展到数百万个用户，并将在恢复数据库故障和连接终止数量等。</span><span class="sxs-lookup"><span data-stu-id="17bec-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="17bec-192">你将了解如何创建可启动简单和高效地快速地循环开发周期，更好并更好地使应用程序自动化和敏捷开发工作流。</span><span class="sxs-lookup"><span data-stu-id="17bec-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="17bec-193">在 Azure App Service 中 web 应用</span><span class="sxs-lookup"><span data-stu-id="17bec-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="17bec-194">为 Fix It 应用程序使用的云环境是 azure 的我们调用网站服务。</span><span class="sxs-lookup"><span data-stu-id="17bec-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="17bec-195">此服务是一种方法，你可以在 Azure 中的将自己 web 应用程序承载而无需创建 Vm 并使其更新、 安装和配置 IIS，等等。我们在我们的虚拟机上托管您的网站，并自动提供备份和恢复以及为你的其他服务。</span><span class="sxs-lookup"><span data-stu-id="17bec-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="17bec-196">网站服务适用于 ASP.NET、 Node.js、 PHP 和 Python。</span><span class="sxs-lookup"><span data-stu-id="17bec-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="17bec-197">这样可以非常快速地使用 Visual Studio、 Webdeploy、 FTP、 Git 或 TFS 进行部署。</span><span class="sxs-lookup"><span data-stu-id="17bec-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="17bec-198">它通常是启动部署的时间与 Internet 上可用的更新后的时间之间只需几秒。</span><span class="sxs-lookup"><span data-stu-id="17bec-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="17bec-199">它是所有可用，若要开始，并根据流量的增长可以向上扩展。</span><span class="sxs-lookup"><span data-stu-id="17bec-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="17bec-200">在后台，在 Azure App Service Web Apps 提供了大量的体系结构组件和您将不得不自己生成，如果你已将托管你自己的 Vm 上使用 IIS 网站的功能。</span><span class="sxs-lookup"><span data-stu-id="17bec-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="17bec-201">一个组件是自动配置 IIS 并且在尽可能多的 Vm，当您想要在上运行你的站点上安装你的应用程序的部署结束点。</span><span class="sxs-lookup"><span data-stu-id="17bec-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![部署服务](introduction/_static/image5.png)

<span data-ttu-id="17bec-203">当用户点击 web 站点时，它们不直接命中 IIS Vm，途经[应用程序请求路由 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="17bec-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="17bec-204">你可以使用其与你自己的服务器，但其优点在于，它们为你自动设置。</span><span class="sxs-lookup"><span data-stu-id="17bec-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="17bec-205">它们使用智能启发式方法，将考虑因素： 会话相关性，在 IIS 中，队列深度和上每个 CPU 使用率计算机直接流量发送到虚拟机承载您的网站。</span><span class="sxs-lookup"><span data-stu-id="17bec-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 负载平衡器](introduction/_static/image6.png)

<span data-ttu-id="17bec-207">如果一台计算机出现故障，Azure 自动从轮转中提取、 新的 VM 实例，旋转和开始将流量定向到新的实例，所有与你的应用程序无需停机。</span><span class="sxs-lookup"><span data-stu-id="17bec-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![从计算机发生故障的自动恢复](introduction/_static/image7.png)

<span data-ttu-id="17bec-209">所有这些自动发生。</span><span class="sxs-lookup"><span data-stu-id="17bec-209">All of this takes place automatically.</span></span> <span data-ttu-id="17bec-210">你需要做是创建网站和应用程序部署到它，使用 Windows PowerShell、 Visual Studio 中或 Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="17bec-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="17bec-211">快速而简单分步教程演示如何在 Visual Studio 中创建 web 应用程序并将其部署到 Azure 网站，请参阅[Azure 和 ASP.NET 入门](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="17bec-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="17bec-212">总结</span><span class="sxs-lookup"><span data-stu-id="17bec-212">Summary</span></span>

<span data-ttu-id="17bec-213">本简介已提供一个列表的主题将介绍书，屏幕快照的示例应用程序，并在 Azure App Service 云环境中的 Web 应用的简要概述。</span><span class="sxs-lookup"><span data-stu-id="17bec-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="17bec-214">开发应用和云环境中的最大好处之一是很容易地自动执行重复开发任务，如创建测试环境和部署代码到它。</span><span class="sxs-lookup"><span data-stu-id="17bec-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="17bec-215">如何执行该操作的使用者[下一章](automate-everything.md)。</span><span class="sxs-lookup"><span data-stu-id="17bec-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="17bec-216">资源</span><span class="sxs-lookup"><span data-stu-id="17bec-216">Resources</span></span>

<span data-ttu-id="17bec-217">在本章中的主题有关的详细信息，请参阅以下资源。</span><span class="sxs-lookup"><span data-stu-id="17bec-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="17bec-218">文档：</span><span class="sxs-lookup"><span data-stu-id="17bec-218">Documentation:</span></span>

- <span data-ttu-id="17bec-219">[Web 应用在 Azure App Service 中的](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="17bec-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="17bec-220">有关 Azure Web Apps 文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="17bec-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="17bec-221">Web Apps、 云服务和 Vm： 何时使用何？</span><span class="sxs-lookup"><span data-stu-id="17bec-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="17bec-222">仅可以在 Azure 中运行 web 应用程序的三种方式之一 WAWS 这一章中所示。</span><span class="sxs-lookup"><span data-stu-id="17bec-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="17bec-223">本文介绍的三种方式的区别，并提供有关如何选择哪一个最适合你的方案的指南。</span><span class="sxs-lookup"><span data-stu-id="17bec-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="17bec-224">如网站、 云服务是 Azure PaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="17bec-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="17bec-225">Vm 是 IaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="17bec-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="17bec-226">PaaS 和 IaaS 的说明，请参阅[数据选项](data-storage-options.md#paasiaas)章。</span><span class="sxs-lookup"><span data-stu-id="17bec-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="17bec-227">视频：</span><span class="sxs-lookup"><span data-stu-id="17bec-227">Videos:</span></span>

- [<span data-ttu-id="17bec-228">Scott Guthrie 开始步骤 0-什么是 Azure 云操作系统？</span><span class="sxs-lookup"><span data-stu-id="17bec-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="17bec-229">[网站体系结构-使用 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="17bec-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="17bec-230">[Azure 网站与 Nir Mashkowski 的内部结构](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="17bec-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="17bec-231">下一篇</span><span class="sxs-lookup"><span data-stu-id="17bec-231">Next</span></span>](automate-everything.md)
