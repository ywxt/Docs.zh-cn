---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: 为 ASP.NET MVC 应用程序 (VB) 创建单元测试 |Microsoft Docs
author: StephenWalther
description: 了解如何创建单元测试控制器操作。 在本教程中，Stephen Walther 演示了如何测试控制器操作返回 parti 是否...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bce5456d9c5465156daf511d0f75a68b35cf7d9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825678"
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a>为 ASP.NET MVC 应用程序 (VB) 创建单元测试
====================
通过[Stephen Walther](https://github.com/StephenWalther)

[下载 PDF](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> 了解如何创建单元测试控制器操作。 在本教程中，Stephen Walther 演示了如何测试是否控制器操作返回的特定视图，返回一组特定的数据，或返回不同类型的操作结果。


本教程的目的是演示如何编写单元测试的控制器在 ASP.NET MVC 应用程序。 我们讨论如何构建三种不同类型的单元测试。 介绍如何测试控制器操作返回的视图、 如何测试控制器操作，返回的视图数据以及如何测试一个控制器操作可以重定向到第二个控制器操作。

## <a name="creating-the-controller-under-test"></a>创建测试控制器

让我们首先创建我们想要测试的控制器。 控制器，名为`ProductController`，包含在列表 1 中。

**代码清单 1 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

`ProductController`包含名为两个操作方法`Index()`和`Details()`。 这两个操作方法返回一个视图。 请注意，`Details()`操作接受一个参数，名为 id。

## <a name="testing-the-view-returned-by-a-controller"></a>测试该视图返回的控制器

假设我们想要测试是否`ProductController`返回右视图。 我们想要确保，当`ProductController.Details()`调用操作，则返回的详细信息视图。 代码清单 2 中的测试类包含用于测试返回的视图的单元测试`ProductController.Details()`操作。

**代码清单 2 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

代码清单 2 中的类包括一个名为测试方法`TestDetailsView()`。 此方法包含三行代码。 第一行代码创建的新实例`ProductController`类。 第二行代码将调用控制器的`Details()`操作方法。 最后，代码检查是否在视图返回的最后一行`Details()`操作是详细信息视图。

`ViewResult.ViewName`属性表示返回由控制器的视图的名称。 有关测试此属性的一个大警告。 有两种方法是控制器可以返回视图。 控制器可以显式返回视图，如下：

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

或者，可以从控制器操作，此类的名称推断的视图的名称：

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

此控制器操作也会返回一个名为视图`Details`。 但是，从操作名称推断的视图的名称。 如果你想要测试的视图名称，然后必须从控制器操作显式返回视图名称。

可以在代码清单 2 中运行单元测试，通过输入键盘组合**Ctrl-R、 A**或单击**运行解决方案中的所有测试**按钮 （请参见图 1）。 如果测试通过，您将看到图 2 中的测试结果窗口。


[![在解决方案中运行所有测试](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)

**图 01**： 在解决方案中运行所有测试 ([单击以查看实际尺寸的图像](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))


[![成功 ！](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)

**图 02**： 成功 ！ ([单击此项可查看原尺寸图像](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))


## <a name="testing-the-view-data-returned-by-a-controller"></a>测试视图数据返回的控制器

一个 MVC 控制器将数据传递给视图通过使用所谓*`View Data`*。 例如，假设你想要显示某一特定产品的详细信息，当你调用`ProductController Details()`操作。 在这种情况下，可以创建的实例`Product`类 （在您的模型中定义），并将传递到实例`Details`视图通过利用`View Data`。

已修改`ProductController`清单 3 中包括的已更新`Details()`返回产品的操作。

**代码清单 3 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

首先，`Details()`操作将创建的新实例`Product`类表示便携式计算机。 接下来，实例`Product`类作为第二个参数传递给`View()`方法。

您可以编写单元测试来测试是否为预期的数据包含在视图中的数据。 列表 4 测试中的单元测试是否在调用时返回表示便携式计算机的产品`ProductController Details()`操作方法。

**列表 4 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

列表 4 中`TestDetailsView()`方法测试通过调用返回的视图数据`Details()`方法。 `ViewData`上作为属性公开`ViewResult`返回通过调用`Details()`方法。 `ViewData.Model`属性包含传递给视图的产品。 此测试只需将验证视图数据中包含该产品具有便携式计算机的名称。

## <a name="testing-the-action-result-returned-by-a-controller"></a>测试操作结果返回的控制器

更复杂的控制器操作可能会返回不同类型的具体值取决于传递到控制器操作的参数的操作结果。 控制器操作可以返回各种类型的操作的结果，包括`ViewResult`， `RedirectToRouteResult`，或`JsonResult`。

例如，修改`Details()`列表 5 中的操作返回`Details`查看有效的产品 Id 传递给该操作时。 如果传递无效的产品 Id-的 Id 值小于 1 则将重定向到`Index()`操作。

**列表 5 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

可以测试的行为`Details()`列表 6 中的单元测试的操作。 列表 6 中的单元测试验证是否将重定向到`Index`查看时具有的值为-1 的 Id 传递给`Details()`方法。

**代码清单 6 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

当您调用`RedirectToAction()`方法的控制器操作中，控制器操作返回`RedirectToRouteResult`。 测试检查是否`RedirectToRouteResult`将用户重定向到名为的控制器操作`Index`。

## <a name="summary"></a>总结

在本教程中，您学习了如何生成单元测试的 MVC 控制器操作。 首先，您学习了如何验证是否由控制器操作返回了正确的视图。 您学习了如何使用`ViewResult.ViewName`属性以验证视图的名称。

接下来，我们探讨了如何测试的内容`View Data`。 您学习了如何检查是否已在中返回正确的产品`View Data`后调用的控制器操作。

最后，我们讨论了如何测试是否从控制器操作返回不同类型的操作结果。 您学习了如何测试控制器将返回是否`ViewResult`或`RedirectToRouteResult`。

> [!div class="step-by-step"]
> [上一篇](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
