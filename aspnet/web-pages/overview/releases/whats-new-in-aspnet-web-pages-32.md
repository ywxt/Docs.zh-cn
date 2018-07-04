---
uid: web-pages/overview/releases/whats-new-in-aspnet-web-pages-32
title: 什么是新 ASP.NET web Pages 3.2 |Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/30/2014
ms.topic: article
ms.assetid: a652beff-8e6b-48ad-bfe4-3703f7ccf0a5
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/releases/whats-new-in-aspnet-web-pages-32
msc.type: authoredcontent
ms.openlocfilehash: eb5698b2928c1f2d1016ec74c18a63e2df5b3225
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390428"
---
<a name="whats-new-in-aspnet-web-pages-32"></a>什么是 ASP.NET Web Pages 3.2 中的新增功能
====================
by [Microsoft](https://github.com/microsoft)

本主题介绍什么是 ASP.NET Web Pages 3.2，网页 3.2.2 的新增功能和[Pages 3.2.3 beta1](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)

## <a name="aspnet-web-pages-32"></a>ASP.NET 网页 3.2

此版本修复了 bug，并引入了一项新功能。

## <a name="download"></a>下载

运行时功能将发布为 NuGet 库中的 NuGet 包。 所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。 ASP.NET Web Pages 3.2 包具有以下版本： &ldquo;3.2.0&rdquo;。 可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebPages/)。 此版本还包括在 NuGet 上的相应本地化的包。

可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：

[!code-console[Main](whats-new-in-aspnet-web-pages-32/samples/sample1.cmd)]

## <a name="new-feature-and-bug-fix"></a>新功能和 Bug 修复

我们修复一个 bug，并在此版本中进行一个细微的功能的增强功能。 可以针对同一个查找的查询[此处](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC|v5.2%20RTM&amp;assignedTo=All&amp;component=Web%20Pages%2FRazor&amp;sortField=Id&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)。

## <a name="aspnet-web-pages-322"></a>ASP.NET Web Pages 3.2.2

此版本中汇总此更改[ASP.NET Web Pages 3.2.1 Beta 版本](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx)提供呈现大型 razor 页面的显著的性能改善。 请参阅[Codeplex 问题 585](https://aspnetwebstack.codeplex.com/workitem/585)。 此版本与 MVC 5.2.2 密切合作现在将取决于此版本的包。

我们与 MSN 团队合作在呈现大型页。 当页面呈现的数据超过 80 千字节时，我们最终的大型对象堆上的对象。 使用多个层的布局时可以乘以此效果。

在服务器上的结果是额外的 CPU 使用率、 延长保留的内存，并甚至长暂停期间[第 2 代清理](https://msdn.microsoft.com/en-us/library/ms973837.aspx)在垃圾回收器。

下面是演示的分析结果的表[perfview](https://channel9.msdn.com/Series/PerfView-Tutorial)运行。 CPU 保留常量在大约 68%，同时正在呈现大型页。 下表显示，已几乎完全消除第 2 代集合数，并将其结果是更高版本请求速率和大量减少由于垃圾回收暂停。

| **区域** | **Before (3.2)** | **后 (3.2.1)** | **增量 %** |
| --- | --- | --- | --- |
| 总请求 （计数） | 26,986 | 32,591 | <font style="background-color: #4bacc6">20.80%</font> |
| 跟踪持续时间 （秒） | 196.20 | 198.60 | 1.20% |
| 请求/秒 | 137.53 | 164.10 | <font style="background-color: #4bacc6">19.30%</font> |
| CPU 负载 | 68.80% | 68.50% |  -0.40% |
| GC CPU 示例 | 124,323 | 17,543 | <font style="background-color: #4bacc6">-85.90%</font> |
| 总分配数 （计数） | 55,357,146 | 57,222,949 | 3.40% |
| 总 GC 暂停 （示例） | 15,091 | 8,515 | <font style="background-color: #4bacc6">-43.60%</font> |
| Gen0 GC （计数） | 403 | 1,216 | 201.70% |
| Gen1 GC （计数） | 290 | 367 | 26.60% |
| 第 2 代 GC （计数） | 229 | 2 | <font style="background-color: #00ff00">-99.10%</font> |
| CPU / 请求 （示例/请求数） | 19.73 | 16.47 | -16.50% |

| 颜色编码： | <font style="background-color: #00ff00">核心改进</font> | <font style="background-color: #4bacc6">积极影响性能</font> |
|---------------|-----------------------------------------------------------------|-------------------------------------------------------------------------------|
|               |                                                                 |                                                                               |

## <a name="aspnet-web-pages-323-beta1"></a>ASP.NET Web Pages 3.2.3 beta1

此版本包含仅 bug 修复。 可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20Pages%2FRazor&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。
