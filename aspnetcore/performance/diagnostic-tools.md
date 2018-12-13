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
# <a name="performance-diagnostic-tools"></a>性能诊断工具

通过[Mike Rousos](https://github.com/mjrousos)

本文列出了诊断 ASP.NET Core 中的性能问题的工具。

## <a name="visual-studio-diagnostic-tools"></a>Visual Studio 诊断工具

[分析和诊断工具](/visualstudio/profiling)内置到 Visual Studio 是开始调查性能问题的好时机。 这些工具是功能强大且方便地从 Visual Studio 开发环境使用。 此工具允许在 ASP.NET Core 应用中 CPU 使用情况、 内存使用情况和性能事件的分析。

中提供了详细信息[Visual Studio 文档](/visualstudio/profiling/profiling-overview)。

## <a name="application-insights"></a>Application Insights

[Application Insights](/azure/application-insights/app-insights-overview)为您的应用程序提供深入的性能数据。 Application Insights 自动响应率、 故障率、 依赖项响应时间和的详细信息上收集数据。 Application Insights 支持自定义事件和特定的指标记录到您的应用程序。

可以在各种环境中使用 application Insights:

* 优化，可在 Azure 中。
* 生产、 开发和过渡环境中的工作原理。
* 可从在本地工作[Visual Studio](/azure/application-insights/app-insights-visual-studio)或其他托管环境中。

有关详细信息，请参阅[用于 ASP.NET Core 的 Application Insights](/azure/application-insights/app-insights-asp-net-core)。

## <a name="perfview"></a>PerfView

[PerfView](https://github.com/Microsoft/perfview)是性能分析工具创建的.NET 团队专门为诊断.NET 性能问题。 PerfView 允许分析 CPU 使用情况、 内存和 GC 行为、 性能事件和时钟时间。

您可以了解有关 PerfView 以及如何入门的详细信息[PerfView 视频教程](http://channel9.msdn.com/Series/PerfView-Tutorial)或通过读取用户的指南，可以在工具或[GitHub 上](https://github.com/Microsoft/perfview)。

## <a name="perfcollect"></a>PerfCollect

PerfView 时.NET 方案一有用的性能分析工具，它仅在上运行 Windows 因此不能使用它来从 ASP.NET Core 应用在 Linux 环境中运行收集跟踪。

[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)是使用分析工具的本机 Linux 的 bash 脚本 ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page)并[LTTng](https://lttng.org/)) 以 PerfView 可以分析在 Linux 上收集跟踪。 在其中不能直接使用 PerfView 的 Linux 环境中出现的性能问题时，PerfCollect 非常有用。 相反，PerfCollect 可以收集跟踪然后分析的.NET Core 应用中使用 PerfView 的 Windows 计算机上。

提供了有关如何安装和开始使用 PerfCollect 的详细信息[GitHub 上](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)。
