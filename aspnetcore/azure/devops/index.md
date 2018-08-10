---
title: 通过 ASP.NET Core 和 Azure 实现 DevOps
author: CamSoper
description: 提供有关为托管在 Azure 中的 ASP.NET Core 应用构建 DevOps 管道的端到端指导的指南。
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/index
ms.openlocfilehash: 09ca835e908e81c6f38f9430fb40638ba6dc3350
ms.sourcegitcommit: 29dfe436f54a27fbb4f6494bc639d16c75001fab
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2018
ms.locfileid: "39722525"
---
# <a name="devops-with-aspnet-core-and-azure"></a><span data-ttu-id="302d4-103">通过 ASP.NET Core 和 Azure 实现 DevOps</span><span class="sxs-lookup"><span data-stu-id="302d4-103">DevOps with ASP.NET Core and Azure</span></span>

<span data-ttu-id="302d4-104">欢迎使用适用于 .NET 的 Azure 开发生命周期指南！</span><span class="sxs-lookup"><span data-stu-id="302d4-104">Welcome to the Azure Development Lifecycle guide for .NET!</span></span> <span data-ttu-id="302d4-105">本指南介绍使用 .NET 工具和进程围绕 Azure 构建开发生命周期的基本概念。</span><span class="sxs-lookup"><span data-stu-id="302d4-105">This guide introduces the basic concepts of building a development lifecycle around Azure using .NET tools and processes.</span></span> <span data-ttu-id="302d4-106">读完本指南后，可以获得成熟 DevOps 工具链的优势。</span><span class="sxs-lookup"><span data-stu-id="302d4-106">After finishing this guide, you'll reap the benefits of a mature DevOps toolchain.</span></span>

## <a name="who-this-guide-is-for"></a><span data-ttu-id="302d4-107">本指南适用对象</span><span class="sxs-lookup"><span data-stu-id="302d4-107">Who this guide is for</span></span>

<span data-ttu-id="302d4-108">有经验的 ASP.NET 开发人员（200-300 级别）。</span><span class="sxs-lookup"><span data-stu-id="302d4-108">You should be an experienced ASP.NET developer (200-300 level).</span></span> <span data-ttu-id="302d4-109">无须了解有关 Azure 的任何内容，因为本指南中将进行介绍。</span><span class="sxs-lookup"><span data-stu-id="302d4-109">You don't need to know anything about Azure, as we'll cover that in this introduction.</span></span> <span data-ttu-id="302d4-110">本指南对于更侧重于操作（而不是开发）的 DevOps 工程师可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="302d4-110">This guide may also be useful for DevOps engineers who are more focused on operations than development.</span></span>

<span data-ttu-id="302d4-111">本指南面向 Windows 开发人员。</span><span class="sxs-lookup"><span data-stu-id="302d4-111">This guide targets Windows developers.</span></span> <span data-ttu-id="302d4-112">但是，.NET Core 完全支持 Linux 和 macOS。</span><span class="sxs-lookup"><span data-stu-id="302d4-112">However, Linux and macOS are fully supported by .NET Core.</span></span> <span data-ttu-id="302d4-113">若要针对 Linux/macOS 调整本指南，请注意有关 Linux/macOS 差异的标注。</span><span class="sxs-lookup"><span data-stu-id="302d4-113">To adapt this guide for Linux/macOS, watch for callouts for Linux/macOS differences.</span></span>

## <a name="what-this-guide-doesnt-cover"></a><span data-ttu-id="302d4-114">本指南未涵盖的内容</span><span class="sxs-lookup"><span data-stu-id="302d4-114">What this guide doesn't cover</span></span>

<span data-ttu-id="302d4-115">本指南专注于 .NET 开发人员的端到端持续部署体验。</span><span class="sxs-lookup"><span data-stu-id="302d4-115">This guide is focused on an end-to-end continuous deployment experience for .NET developers.</span></span> <span data-ttu-id="302d4-116">这不是介绍 Azure 中所有内容的全面指南，并不特别着重于适用于 Azure 服务的 .NET API。</span><span class="sxs-lookup"><span data-stu-id="302d4-116">It's not an exhaustive guide to all things Azure, and it doesn't focus extensively on .NET APIs for Azure services.</span></span> <span data-ttu-id="302d4-117">介绍的重点在于持续集成、部署、监视和调试。</span><span class="sxs-lookup"><span data-stu-id="302d4-117">The emphasis is all around continuous integration, deployment, monitoring, and debugging.</span></span> <span data-ttu-id="302d4-118">本指南结尾附近提供了后续步骤建议。</span><span class="sxs-lookup"><span data-stu-id="302d4-118">Near the end of the guide, recommendations for next steps are offered.</span></span> <span data-ttu-id="302d4-119">建议包括对 ASP.NET 开发人员有用的 Azure 平台服务。</span><span class="sxs-lookup"><span data-stu-id="302d4-119">Included in the suggestions are Azure platform services that are useful to ASP.NET developers.</span></span>

## <a name="whats-in-this-guide"></a><span data-ttu-id="302d4-120">本指南内容</span><span class="sxs-lookup"><span data-stu-id="302d4-120">What's in this guide</span></span>

### <a name="tools-and-downloadsxrefazuredevopstools-and-downloads"></a>[<span data-ttu-id="302d4-121">工具和下载</span><span class="sxs-lookup"><span data-stu-id="302d4-121">Tools and downloads</span></span>](xref:azure/devops/tools-and-downloads)

<span data-ttu-id="302d4-122">了解在何处获取本指南中使用的工具。</span><span class="sxs-lookup"><span data-stu-id="302d4-122">Learn where to acquire the tools used in this guide.</span></span>

### <a name="deploy-to-app-servicexrefazuredevopsdeploy-to-app-service"></a>[<span data-ttu-id="302d4-123">部署到应用服务</span><span class="sxs-lookup"><span data-stu-id="302d4-123">Deploy to App Service</span></span>](xref:azure/devops/deploy-to-app-service)

<span data-ttu-id="302d4-124">了解将 ASP.NET Core 应用部署到 Azure 应用服务的各种方法。</span><span class="sxs-lookup"><span data-stu-id="302d4-124">Learn the various methods for deploying an ASP.NET Core app to Azure App Service.</span></span>

### <a name="continuous-integration-and-deploymentxrefazuredevopscicd"></a>[<span data-ttu-id="302d4-125">持续集成和部署</span><span class="sxs-lookup"><span data-stu-id="302d4-125">Continuous integration and deployment</span></span>](xref:azure/devops/cicd)

<span data-ttu-id="302d4-126">通过 GitHub、VSTS 和 Azure，为 ASP.NET Core 应用生成端到端持续集成和部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="302d4-126">Build an end-to-end continuous integration and deployment solution for your ASP.NET Core app with GitHub, VSTS, and Azure.</span></span>

### <a name="monitor-and-debugxrefazuredevopsmonitor"></a>[<span data-ttu-id="302d4-127">监视和调试</span><span class="sxs-lookup"><span data-stu-id="302d4-127">Monitor and debug</span></span>](xref:azure/devops/monitor)

<span data-ttu-id="302d4-128">使用 Azure 工具监视、故障排除和优化应用程序。</span><span class="sxs-lookup"><span data-stu-id="302d4-128">Use Azure's tools to monitor, troubleshoot, and tune your application.</span></span>

### <a name="next-stepsxrefazuredevopsnext-steps"></a>[<span data-ttu-id="302d4-129">后续步骤</span><span class="sxs-lookup"><span data-stu-id="302d4-129">Next steps</span></span>](xref:azure/devops/next-steps)

<span data-ttu-id="302d4-130">ASP.NET Core 开发人员学习 Azure 的其他学习路径。</span><span class="sxs-lookup"><span data-stu-id="302d4-130">Other learning paths for the ASP.NET Core developer learning Azure.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="302d4-131">鸣谢</span><span class="sxs-lookup"><span data-stu-id="302d4-131">Acknowledgments</span></span>

<span data-ttu-id="302d4-132">特此感谢为本指南提供了有用的建议的所有 .NET 社区成员！</span><span class="sxs-lookup"><span data-stu-id="302d4-132">Thank you to everyone in the .NET community who contributed to this guide with helpful suggestions!</span></span> <span data-ttu-id="302d4-133">特别感谢以下社区成员，他们参与了此材料的最终审核：</span><span class="sxs-lookup"><span data-stu-id="302d4-133">We'd like to specifically thank the following community members who contributed to the final review of this material:</span></span>

* [<span data-ttu-id="302d4-134">Sam Wronski</span><span class="sxs-lookup"><span data-stu-id="302d4-134">Sam Wronski</span></span>](https://www.youtube.com/c/worldofzerodevelopment)
* [<span data-ttu-id="302d4-135">Jeffrey Palermo</span><span class="sxs-lookup"><span data-stu-id="302d4-135">Jeffrey Palermo</span></span>](https://twitter.com/jeffreypalermo)

## <a name="conclusion"></a><span data-ttu-id="302d4-136">结束语</span><span class="sxs-lookup"><span data-stu-id="302d4-136">Conclusion</span></span>

<span data-ttu-id="302d4-137">本指南可帮助你围绕 ASP.NET Core 和 Azure 应用服务构建持续集成开发生命周期。</span><span class="sxs-lookup"><span data-stu-id="302d4-137">This guide prepares you to build a continuous integration development lifecycle built around ASP.NET Core and Azure App Service.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="302d4-138">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="302d4-138">Additional reading</span></span>

* [<span data-ttu-id="302d4-139">什么是云计算？</span><span class="sxs-lookup"><span data-stu-id="302d4-139">What is Cloud Computing?</span></span>](https://azure.microsoft.com/overview/what-is-cloud-computing/)
* [<span data-ttu-id="302d4-140">云计算示例</span><span class="sxs-lookup"><span data-stu-id="302d4-140">Examples of Cloud Computing</span></span>](https://azure.microsoft.com/overview/examples-of-cloud-computing/)
* [<span data-ttu-id="302d4-141">什么是 IaaS？</span><span class="sxs-lookup"><span data-stu-id="302d4-141">What is IaaS?</span></span>](https://azure.microsoft.com/overview/what-is-iaas/)
* [<span data-ttu-id="302d4-142">什么是 PaaS？</span><span class="sxs-lookup"><span data-stu-id="302d4-142">What is PaaS?</span></span>](https://azure.microsoft.com/overview/what-is-paas/)
