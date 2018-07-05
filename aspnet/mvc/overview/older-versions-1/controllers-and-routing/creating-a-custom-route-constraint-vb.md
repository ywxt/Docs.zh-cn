---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 创建自定义路由约束 (VB) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何创建自定义路由约束。 我们实现一个简单的自定义的约束，可防止路由匹配 w...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2009
ms.topic: article
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: cc30cfd49402b10274e22eb27abba73329811b7e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385490"
---
<a name="creating-a-custom-route-constraint-vb"></a>创建自定义路由约束 (VB)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 演示了如何创建自定义路由约束。 我们实现简单的自定义约束，以防止浏览器请求进行从远程计算机时要匹配的路由。


本教程的目的是演示如何创建自定义路由约束。 自定义路由约束，可防止路由除非匹配某些自定义的条件匹配。

在本教程中，我们将创建本地主机路由约束。 本地主机路由约束只匹配来自本地计算机的请求。 从在 Internet 上的远程请求都不匹配。

通过实现 IRouteConstraint 接口实现自定义路由约束。 这是一个极其简单接口，用于描述一个方法：

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

该方法返回一个布尔值。 如果返回 False，与约束关联的路由不会与浏览器请求匹配。

在列表 1 中包含的 Localhost 约束。

**代码清单 1-LocalhostConstraint.vb**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

在列表 1 中的约束利用由 HttpRequest 类公开的 IsLocal 属性。 该请求的 IP 地址是任一 127.0.0.1 或请求的 IP 是服务器的 IP 地址相同时，此属性返回 true。

使用 Global.asax 文件中定义的路由中的自定义约束。 代码清单 2 中的 Global.asax 文件使用 Localhost 约束以防止任何人请求管理页，除非它们从本地服务器发出请求。 例如，从远程服务器进行时，将失败 /Admin/DeleteAll 的请求。

**代码清单 2-Global.asax**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

管理路由的定义中使用 Localhost 约束。 此路由不会由远程浏览器请求匹配。 但请注意，在 Global.asax 中定义其他路由可能与相同的请求匹配。 请务必了解约束匹配的请求阻止特定路由，并不是所有路由在 Global.asax 文件中都定义。

请注意，默认路由已被注释掉从代码清单 2 中的 Global.asax 文件。 如果包含默认路由，默认路由将匹配的管理控制器的请求。 在这种情况下，远程用户仍可以调用的管理控制器的操作，即使它们的请求不匹配的管理路由。

> [!div class="step-by-step"]
> [上一篇](creating-a-route-constraint-vb.md)
