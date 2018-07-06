---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 了解操作筛选器 (VB) |Microsoft Docs
author: microsoft
description: 本教程的目的是说明操作筛选器。 操作筛选器是可应用于控制器操作-或整个控制器的属性...
ms.author: aspnetcontent
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 07e02330747b3b8f8bb318d30c7a984aa15baeef
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811177"
---
<a name="understanding-action-filters-vb"></a>了解操作筛选器 (VB)
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> 本教程的目的是说明操作筛选器。 操作筛选器是可应用于控制器操作-或整个 controller--修改在其中执行此操作的方式的属性。


## <a name="understanding-action-filters"></a>了解操作筛选器

本教程的目的是说明操作筛选器。 操作筛选器是可应用于控制器操作-或整个 controller--修改在其中执行此操作的方式的属性。 ASP.NET MVC 框架包括多个操作筛选器：

- OutputCache – 此操作筛选器将缓存指定的时间内的控制器操作的输出。
- HandleError – 此操作筛选器处理时，将执行控制器操作引发的错误。
- 授权 – 此操作筛选器，可限制对特定用户或角色的访问。

此外可以创建自己的自定义操作筛选器。 例如，你可能想要创建自定义操作筛选器，以实现自定义身份验证系统。 或者，你可能想要创建操作筛选器修改的控制器操作返回的视图数据。

在本教程中，您将了解如何构建的基础知识，操作筛选器。 我们创建记录到 Visual Studio 输出窗口的操作处理的不同阶段的日志操作筛选器。

### <a name="using-an-action-filter"></a>使用操作筛选器

操作筛选器是一个属性。 可以将大多数操作筛选器应用到一个单独的控制器操作或整个控制器。

例如，在列表 1 中的数据控制器将公开名为操作`Index()`返回当前时间。 此操作用修饰`OutputCache`操作筛选器。 此筛选器会导致要缓存的 10 秒的操作返回的值。

**代码清单 1 – `Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

如果重复调用`Index()`操作通过你的浏览器的地址栏中输入 URL/数据/索引并点击刷新按钮多次，则会出现在同一时间为 10 秒。 输出`Index()`操作缓存 （见图 1） 的 10 秒。


[![缓存的时间](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**图 01**： 缓存时间 ([单击以查看实际尺寸的图像](understanding-action-filters-vb/_static/image3.png))


在列表 1 中，单个操作筛选器 –`OutputCache`操作筛选器 – 应用于`Index()`方法。 如果需要可以将多个操作筛选器应用到相同的操作。 例如，你可能想要应用同时`OutputCache`和`HandleError`对同一操作的操作筛选器。

在列表 1 中，`OutputCache`操作筛选器应用于`Index()`操作。 您还可以应用到此特性`DataController`类本身。 在这种情况下，在控制器公开的任何操作返回的结果会缓存 10 秒。

### <a name="the-different-types-of-filters"></a>不同类型的筛选器

ASP.NET MVC 框架支持四种不同类型的筛选器：

1. 授权筛选器 – 实现`IAuthorizationFilter`属性。
2. 操作筛选器 – 实现`IActionFilter`属性。
3. 结果筛选器 – 实现`IResultFilter`属性。
4. 异常筛选器 – 实现`IExceptionFilter`属性。

上面列出的顺序执行筛选器。 例如，授权筛选器始终执行的操作筛选器之前和之后每种其他类型的筛选器始终执行异常筛选器。

授权筛选器用于实现身份验证和授权控制器操作。 例如，授权筛选器是授权筛选器的示例。

操作筛选器包含之前和之后，将执行控制器操作执行的逻辑。 可用于操作筛选器，例如，修改控制器操作返回的视图数据。

结果筛选器包含之前和之后执行视图结果执行的逻辑。 例如，你可能想要修改的视图结果之前呈现到浏览器视图。

异常筛选器是筛选器可运行的最后一个类型。 异常筛选器可用于处理由您的控制器操作或控制器操作结果引发的错误。 此外可以使用异常筛选器来记录错误。

按特定顺序执行每种不同类型的筛选器。 如果你想要控制相同类型的筛选器的执行顺序则可以设置筛选器的顺序属性。

所有操作筛选器的基类是`System.Web.Mvc.FilterAttribute`类。 如果你想要实现特定类型的筛选器，则需要创建一个类继承自基本的筛选器类并实现一个或多个 IAuthorizationFilter、 是 IActionFilter、 IResultFilter，或 ExceptionFilter 接口。

### <a name="the-base-actionfilterattribute-class"></a>基本的 ActionFilterAttribute 类

为了使你更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包括基`ActionFilterAttribute`类。 此类同时实现`IActionFilter`并`IResultFilter`接口，并继承`Filter`类。

本文中的术语不完全一致。 从技术上讲，从 ActionFilterAttribute 类继承的类是操作筛选器和结果筛选器。 但是，松散的意义上，在 word 操作筛选器用于对任何类型的 ASP.NET MVC framework 中的筛选器，请参阅。

基本的 ActionFilterAttribute 类具有可重写以下方法：

- OnActionExecuting – 在执行控制器操作之前，将调用此方法。
- OnActionExecuted – 在执行控制器操作后，将调用此方法。
- OnResultExecuting – 调用此方法在执行控制器操作结果之前。
- OnResultExecuted – 调用此方法后在执行控制器操作结果。

在下一步部分中，我们将了解如何实现每种不同方法。

### <a name="creating-a-log-action-filter"></a>创建日志操作筛选器

为了说明如何构建自定义操作筛选器，我们将创建自定义操作筛选器，以记录处理到 Visual Studio 输出窗口的控制器操作的阶段。 我们`LogActionFilter`代码清单 2 中包含。

**代码清单 2 – `ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

列表 2 中`OnActionExecuting()`， `OnActionExecuted()`， `OnResultExecuting()`，和`OnResultExecuted()`方法都调用`Log()`方法。 方法和当前的路由数据的名称传递给`Log()`方法。 `Log()`方法将一条消息写入到 Visual Studio 输出窗口 （请参见图 2）。


[![写入到 Visual Studio 输出窗口](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**图 02**： 写入 Visual Studio 输出窗口 ([单击以查看实际尺寸的图像](understanding-action-filters-vb/_static/image6.png))


主控制器中清单 3 说明了如何将日志操作筛选器应用于整个控制器类。 只要任何 Home 控制器公开的操作调用 – 要么`Index()`方法或`About()`方法 – 处理操作记录到 Visual Studio 输出窗口的阶段。

**代码清单 3 – `Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>总结

在本教程中，已向您介绍 ASP.NET MVC 操作筛选器。 介绍了四个不同类型的筛选器： 授权筛选器、 操作筛选器、 结果筛选器和异常筛选器。 你还了解了有关基本`ActionFilterAttribute`类。

最后，您学习了如何实现简单的操作筛选器。 我们创建了日志的操作筛选器，在日志中记录的处理到 Visual Studio 输出窗口的控制器操作的阶段。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-routing-overview-vb.md)
> [下一页](improving-performance-with-output-caching-vb.md)
