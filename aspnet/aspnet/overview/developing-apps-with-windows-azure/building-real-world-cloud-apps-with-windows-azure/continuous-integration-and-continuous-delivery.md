---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 持续集成和持续交付 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: 787aacfd843f5f72e567670d601fb036a2c474bc
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824661"
---
<a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>持续集成和持续交付 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


前两个建议的开发流程模式已[使一切自动化](automate-everything.md)并[源代码管理](source-control.md)，第三个流程模式将它们合并。 持续集成 (CI) 是指开发人员签入到源代码存储库的代码，只要自动触发生成。 持续交付 (CD) 进一步执行此步骤： 生成和自动化的单元测试是成功后，自动部署到环境可以执行更多深入测试应用程序。

云使你能够维护测试环境，因为您只需支付环境资源，只要它们的成本降至最低。 CD 过程可以设置测试环境时需要它，以及完成后，可能需要向该环境下测试。

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>持续集成和持续交付工作流

通常，我们建议不要向你的开发和过渡环境进行持续交付。 大多数团队，甚至在 Microsoft，对于生产部署需要手动审查和批准流程。 对于生产的开发团队的关键人员的支持，或在低流量期间可用时，将执行可能想要确保它的部署。 但没有执行任何操作，以防用户完全自动执行开发和测试环境，以便开发人员只需签入更改和环境进行验收测试设置。

下图出自[Microsoft 模式和实践电子书有关持续交付](http://aka.ms/ReleasePipeline)说明了典型的工作流。 单击此图像可查看它在其原始上下文中的完整大小。

[![持续交付工作流](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>如何在云中通过经济高效的 CI 和 CD

在 Azure 中的这些流程的自动化非常简单。 因为您在云中运行的所有内容，您无需购买或管理你的生成或测试环境的服务器。 同时，无需等待服务器可用于执行操作上测试。 每个版本执行的操作，可以构建测试环境在 Azure 中使用自动化脚本、 运行的验收测试或更多深入测试反对这样做，，然后只需完成后即将其拆散。 如果只有 2 个小时或 8 小时一次或一天运行该服务器，您必须为其付费的金额是最小的因为你只付钱让实际运行一台计算机的时间。 例如，在环境所需的修补程序应用程序基本上花费大约 1%为千瓦时，如果一个层上升从免费级别。 每月的过程中，如果只运行一次的每隔一小时的环境对测试环境所需可能的成本购买在星巴克 latte 小于。

## <a name="visual-studio-team-services-vsts"></a>Visual Studio Team Services (VSTS)

VSTS 提供了许多功能可帮助您进行从规划到部署的应用程序开发。

- 它支持 （分布） 的 Git 和 TFVC （集中式） 源控件。
- 它提供弹性生成服务，这意味着它会动态在需要时创建生成服务器并将关闭完成时。 您可以自动开始生成时有人签入源代码更改，并且没有已分配，并为你自己的生成服务器位于空闲大部分时间支付费用。 生成服务是免费的只要不超过一定数量的生成。 如果您希望执行大批量的生成，可以将很少的额外支付保留的生成服务器。
- 它支持向 Azure 持续交付。
- 它支持自动的负载测试。 负载测试对云应用程序至关重要，但往往会忽视直到已经太迟。 负载测试模拟由数以千计的用户，这样可以找出瓶颈并提高吞吐量的应用程序的大量使用，在发布到生产应用之前。
- 它支持团队聊天室协作，该工具可帮助实时通信和适用于小型敏捷团队的协作。
- 它支持敏捷项目管理。


持续集成和交付 VSTS 功能的详细信息，请参阅[Visual Studio Team Services](https://www.visualstudio.com/team-services/)。

如果正在寻找有关统包式项目管理、 团队协作和源代码控制解决方案，请访问 VSTS。 该服务是对最多 5 个用户免费，你可以在注册[Visual Studio Team Services](https://www.visualstudio.com/team-services/)。

## <a name="summary"></a>总结

有关如何实现具有较低的周期时间的可重复、 可靠、 可预测的开发进程被第三个云开发模式。 在中[接下来的章节](web-development-best-practices.md)我们开始探讨体系结构和编码模式。

## <a name="resources"></a>资源

有关详细信息，请参阅[部署 Azure 应用服务中的 web 应用](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)。

另请参阅以下资源：

- [构建发布管道与 Team Foundation Server 2012](http://aka.ms/ReleasePipeline)。 电子书、 动手实验和示例代码由 Microsoft 模式和实践，深入介绍到持续交付。 介绍使用 Visual Studio 实验室管理工具版和 Visual Studio Release Management。
- [ALM Rangers DevOps 工具和指南](https://aka.ms/vsarsolutions/)。 ALM Rangers 引入 DevOps Workbench 示例配套解决方案和协作的模式中的实用指南&amp;实践书籍*构建发布管道与 TFS 2012*，作为更好地开始了解 DevOps 的概念&amp;Release Management 适用于 TFS 2012 和进行检验。 本指南演示如何生成一次，将部署到多个环境。
- [使用 Visual Studio 2012 对连续交付测试](https://msdn.microsoft.com/library/jj159345.aspx)。 电子书由 Microsoft 模式和实践，解释了如何将集成使用持续交付的自动化测试。
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker)。 旨在捕获从 TFS （基于标签） 生成、 生成它、 将其打包，允许某人 DevOps 角色，才能配置它的特定方面并将其推送到 Azure 的工具的源代码。 该工具以支持操作以"回滚"到以前部署的版本跟踪部署过程。 该工具没有外部依赖关系，并可以函数独立使用 TFS Api 和 Azure SDK。
- [持续交付： 通过生成、 测试和部署自动化可靠的软件版本](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)。 通过 Jez Humble 书籍。
- [释放它 ！设计和部署生产就绪软件](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)。 Michael T.nygard 书籍。

> [!div class="step-by-step"]
> [上一页](source-control.md)
> [下一页](web-development-best-practices.md)
