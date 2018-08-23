---
uid: visual-studio/overview/2017/optimize-build-perf
title: 优化解决方案的生成性能
author: tfitzmac
description: 优化解决方案的生成性能
ms.author: riande
ms.date: 08/22/2018
msc.type: authoredcontent
ms.openlocfilehash: 19f190835e7477e69db470b74edac9e211fd9158
ms.sourcegitcommit: 5a2456cbf429069dc48aaa2823cde14100e4c438
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "41909884"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="63919-103">优化解决方案的生成性能</span><span class="sxs-lookup"><span data-stu-id="63919-103">Optimize build performance for solution</span></span>
<span data-ttu-id="63919-104">Visual Studio 2017 15.8年和更高版本添加新的菜单项下**生成 > ASP.NET 编译 > 解决方案优化生成性能**。</span><span class="sxs-lookup"><span data-stu-id="63919-104">Visual Studio 2017 15.8 and later added a new menu item under **Build > ASP.NET Compilation > Optimize Build Performance for Solution**.</span></span>

![新的菜单项的屏幕截图](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="63919-106">ASP.NET 编译其视图在运行时，这意味着具有一份编译器以来的 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="63919-106">ASP.NET compiles its views at runtime, which means your ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="63919-107">但是，开发人员计算机上的副本的编译器与 Visual Studio 的副本不匹配时生成性能会受到影响大约每个增量生成 1-3 秒。</span><span class="sxs-lookup"><span data-stu-id="63919-107">However, on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, your build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="63919-108">此功能将更新的编译器，以匹配 Visual Studio 的增量生成可加快你的项目的副本。</span><span class="sxs-lookup"><span data-stu-id="63919-108">This feature will update your project's copy of the compiler to match Visual Studio's which should speed up incremental builds.</span></span>

<span data-ttu-id="63919-109">这是适用于 ASP.NET 框架的项目，不适用于 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="63919-109">This is applicable to ASP.NET Framework projects only, it does not apply to ASP.NET Core.</span></span>
