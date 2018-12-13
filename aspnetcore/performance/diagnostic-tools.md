---
title: 性能诊断工具
author: mjrousos
description: 诊断 ASP.NET Core 应用中的性能问题的有用工具。
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.date: 12/07/2018
uid: performance/diagnostic-tools
ms.openlocfilehash: 3093b7d646e4fa943334c7b1e70ddc007ab18780
ms.sourcegitcommit: 1ea1b4fc58055c62728143388562689f1ef96cb2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53329194"
---
# <a name="performance-diagnostic-tools"></a><span data-ttu-id="4b331-103">性能诊断工具</span><span class="sxs-lookup"><span data-stu-id="4b331-103">Performance Diagnostic Tools</span></span>

<span data-ttu-id="4b331-104">通过[Mike Rousos](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="4b331-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="4b331-105">本文列出了诊断 ASP.NET Core 中的性能问题的工具。</span><span class="sxs-lookup"><span data-stu-id="4b331-105">This article lists tools for diagnosing performance issues in ASP.NET Core.</span></span>

## <a name="visual-studio-diagnostic-tools"></a><span data-ttu-id="4b331-106">Visual Studio 诊断工具</span><span class="sxs-lookup"><span data-stu-id="4b331-106">Visual Studio Diagnostic Tools</span></span>

<span data-ttu-id="4b331-107">[分析和诊断工具](/visualstudio/profiling)内置到 Visual Studio 是开始调查性能问题的好时机。</span><span class="sxs-lookup"><span data-stu-id="4b331-107">The [profiling and diagnostic tools](/visualstudio/profiling) built into Visual Studio are a good place to start investigating performance issues.</span></span> <span data-ttu-id="4b331-108">这些工具是功能强大且方便地从 Visual Studio 开发环境使用。</span><span class="sxs-lookup"><span data-stu-id="4b331-108">These tools are powerful and convenient to use from the Visual Studio development environment.</span></span> <span data-ttu-id="4b331-109">此工具允许在 ASP.NET Core 应用中 CPU 使用情况、 内存使用情况和性能事件的分析。</span><span class="sxs-lookup"><span data-stu-id="4b331-109">The tooling allows analysis of CPU usage, memory usage, and performance events in ASP.NET Core apps.</span></span>

<span data-ttu-id="4b331-110">中提供了详细信息[Visual Studio 文档](/visualstudio/profiling/profiling-overview)。</span><span class="sxs-lookup"><span data-stu-id="4b331-110">More information is available in [Visual Studio documentation](/visualstudio/profiling/profiling-overview).</span></span>

## <a name="application-insights"></a><span data-ttu-id="4b331-111">Application Insights</span><span class="sxs-lookup"><span data-stu-id="4b331-111">Application Insights</span></span>

<span data-ttu-id="4b331-112">[Application Insights](/azure/application-insights/app-insights-overview)为您的应用程序提供深入的性能数据。</span><span class="sxs-lookup"><span data-stu-id="4b331-112">[Application Insights](/azure/application-insights/app-insights-overview) provides in-depth performance data for your app.</span></span> <span data-ttu-id="4b331-113">Application Insights 自动响应率、 故障率、 依赖项响应时间和的详细信息上收集数据。</span><span class="sxs-lookup"><span data-stu-id="4b331-113">Application Insights automatically collects data on response rates, failure rates, dependency response times, and more.</span></span> <span data-ttu-id="4b331-114">Application Insights 支持自定义事件和特定的指标记录到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4b331-114">Application Insights supports logging custom events and metrics specific to your app.</span></span>

<span data-ttu-id="4b331-115">可以在各种环境中使用 application Insights:</span><span class="sxs-lookup"><span data-stu-id="4b331-115">Application Insights can be used in a variety environments:</span></span>

* <span data-ttu-id="4b331-116">优化，可在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="4b331-116">Optimized to work in Azure.</span></span>
* <span data-ttu-id="4b331-117">生产、 开发和过渡环境中的工作原理。</span><span class="sxs-lookup"><span data-stu-id="4b331-117">Works in production, development, and staging.</span></span>
* <span data-ttu-id="4b331-118">可从在本地工作[Visual Studio](/azure/application-insights/app-insights-visual-studio)或其他托管环境中。</span><span class="sxs-lookup"><span data-stu-id="4b331-118">Works locally from [Visual Studio](/azure/application-insights/app-insights-visual-studio) or in other hosting environments.</span></span>

<span data-ttu-id="4b331-119">有关详细信息，请参阅[用于 ASP.NET Core 的 Application Insights](/azure/application-insights/app-insights-asp-net-core)。</span><span class="sxs-lookup"><span data-stu-id="4b331-119">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="perfview"></a><span data-ttu-id="4b331-120">PerfView</span><span class="sxs-lookup"><span data-stu-id="4b331-120">PerfView</span></span>

<span data-ttu-id="4b331-121">[PerfView](https://github.com/Microsoft/perfview)是性能分析工具创建的.NET 团队专门为诊断.NET 性能问题。</span><span class="sxs-lookup"><span data-stu-id="4b331-121">[PerfView](https://github.com/Microsoft/perfview) is a performance analysis tool created by the .NET team specifically for diagnosing .NET performance issues.</span></span> <span data-ttu-id="4b331-122">PerfView 允许分析 CPU 使用情况、 内存和 GC 行为、 性能事件和时钟时间。</span><span class="sxs-lookup"><span data-stu-id="4b331-122">PerfView allows analysis of CPU usage, memory and GC behavior, performance events, and wall clock time.</span></span>

<span data-ttu-id="4b331-123">您可以了解有关 PerfView 以及如何入门的详细信息[PerfView 视频教程](http://channel9.msdn.com/Series/PerfView-Tutorial)或通过读取用户的指南，可以在工具或[GitHub 上](https://github.com/Microsoft/perfview)。</span><span class="sxs-lookup"><span data-stu-id="4b331-123">You can learn more about PerfView and how to get started with [PerfView video tutorials](http://channel9.msdn.com/Series/PerfView-Tutorial) or by reading the user's guide available in the tool or [on GitHub](https://github.com/Microsoft/perfview).</span></span>

## <a name="perfcollect"></a><span data-ttu-id="4b331-124">PerfCollect</span><span class="sxs-lookup"><span data-stu-id="4b331-124">PerfCollect</span></span>

<span data-ttu-id="4b331-125">PerfView 时.NET 方案一有用的性能分析工具，它仅在上运行 Windows 因此不能使用它来从 ASP.NET Core 应用在 Linux 环境中运行收集跟踪。</span><span class="sxs-lookup"><span data-stu-id="4b331-125">While PerfView is a useful performance analysis tool for .NET scenarios, it only runs on Windows so you can't use it to collect traces from ASP.NET Core apps running in Linux environments.</span></span>

<span data-ttu-id="4b331-126">[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)是使用分析工具的本机 Linux 的 bash 脚本 ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page)并[LTTng](https://lttng.org/)) 以 PerfView 可以分析在 Linux 上收集跟踪。</span><span class="sxs-lookup"><span data-stu-id="4b331-126">[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md) is a bash script that uses native Linux profiling tools ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page) and [LTTng](https://lttng.org/)) to collect traces on Linux that can be analyzed by PerfView.</span></span> <span data-ttu-id="4b331-127">在其中不能直接使用 PerfView 的 Linux 环境中出现的性能问题时，PerfCollect 非常有用。</span><span class="sxs-lookup"><span data-stu-id="4b331-127">PerfCollect is useful when performance problems show up in Linux environments where PerfView can't be used directly.</span></span> <span data-ttu-id="4b331-128">相反，PerfCollect 可以收集跟踪然后分析的.NET Core 应用中使用 PerfView 的 Windows 计算机上。</span><span class="sxs-lookup"><span data-stu-id="4b331-128">Instead, PerfCollect can collect traces from .NET Core apps that are then analyzed on a Windows computer using PerfView.</span></span>

<span data-ttu-id="4b331-129">提供了有关如何安装和开始使用 PerfCollect 的详细信息[GitHub 上](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)。</span><span class="sxs-lookup"><span data-stu-id="4b331-129">More information about how to install and get started with PerfCollect is available [on GitHub](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md).</span></span>
