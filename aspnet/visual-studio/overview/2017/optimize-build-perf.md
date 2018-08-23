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
# <a name="optimize-build-performance-for-solution"></a>优化解决方案的生成性能
Visual Studio 2017 15.8年和更高版本添加新的菜单项下**生成 > ASP.NET 编译 > 解决方案优化生成性能**。

![新的菜单项的屏幕截图](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET 编译其视图在运行时，这意味着具有一份编译器以来的 ASP.NET 项目。 但是，开发人员计算机上的副本的编译器与 Visual Studio 的副本不匹配时生成性能会受到影响大约每个增量生成 1-3 秒。 此功能将更新的编译器，以匹配 Visual Studio 的增量生成可加快你的项目的副本。

这是适用于 ASP.NET 框架的项目，不适用于 ASP.NET Core。
