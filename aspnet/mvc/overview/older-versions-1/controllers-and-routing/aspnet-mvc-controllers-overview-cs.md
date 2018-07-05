---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET MVC 控制器概述 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 向您介绍 ASP.NET MVC 控制器。 了解如何创建新的控制器，并返回不同类型的操作 res...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: e1834498d5a0f5d84f650faf32bb6352f2ad3e70
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370082"
---
<a name="aspnet-mvc-controller-overview-c"></a>ASP.NET MVC 控制器概述 (C#)
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 向您介绍 ASP.NET MVC 控制器。 了解如何创建新的控制器，并返回不同类型的操作结果。


本教程探讨了 ASP.NET MVC 控制器、 控制器操作和操作结果的主题。 完成本教程后，你将了解如何使用控制器控制与 ASP.NET MVC 网站访问者进行交互的方式。

## <a name="understanding-controllers"></a>了解控制器

MVC 控制器负责响应对 ASP.NET MVC 网站发出的请求。 每个浏览器请求映射到特定控制器。 例如，假设您的浏览器的地址栏中输入以下 URL:

`http://localhost/Product/Index/3`

在这种情况下，将调用名为 ProductController 的控制器。 ProductController 负责生成对浏览器请求的响应。 例如，在控制器可能会返回到浏览器返回的特定视图或控制器可能会将用户重定向到另一个控制器。

代码清单 1 包含名为 ProductController 的简单控制器。

**Listing1 - Controllers\ProductController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

您可以看到从列表 1 中，控制器是只是一个类 （Visual Basic.NET 或 C# 类）。 控制器是从 system.web.mvc.controller 中衍生基类派生的类。 由于从这个基类继承控制器，控制器将免费继承多个有用的方法 （我们将讨论在一段时间中这些方法）。

## <a name="understanding-controller-actions"></a>了解控制器操作

在控制器公开控制器操作。 操作是在浏览器地址栏中输入特定的 URL 时调用的控制器上的方法。 例如，假设以下 URL 发出请求：

`http://localhost/Product/Index/3`

在这种情况下，在 ProductController 类调用 index （） 方法。 Index （） 方法是控制器操作的示例。

控制器操作必须是控制器类的公共方法。 默认情况下，C# 方法，为私有方法。 请注意到控制器类添加任何公共方法自动公开为控制器操作 （您必须小心这由于控制器操作可以调用 universe 中的任何人只需通过浏览器地址栏中键入正确的 URL）。

有一些必须满足的控制器操作的其他要求。 不能重载用作控制器操作的方法。 此外，控制器操作不能是静态方法。 除此之外，可以使用任何方法作为控制器操作。

## <a name="understanding-action-results"></a>了解操作结果

控制器操作返回所谓*操作结果*。 操作结果是控制器操作返回到浏览器请求的响应中。

ASP.NET MVC 框架支持多种类型的操作的结果，包括：

1. ViewResult-表示 HTML 和标记。
2. EmptyResult-表示没有结果。
3. RedirectResult-表示重定向到新 URL。
4. JsonResult-表示可在 AJAX 应用程序的 JavaScript 对象表示法结果。
5. JavaScriptResult-表示 JavaScript 脚本。
6. ContentResult-表示文本结果。
7. FileContentResult-表示可下载的文件 （具有二进制内容）。
8. FilePathResult-表示可下载的文件 （包括路径）。
9. FileStreamResult-表示一个可下载文件 （使用文件流）。

所有这些操作的结果从 ActionResult 类的基类继承。

在大多数情况下，控制器操作返回 ViewResult。 例如，在代码清单 2 中的索引控制器操作返回 ViewResult。

**代码清单 2-Controllers\BookController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

当操作返回 ViewResult 时，HTML 返回到浏览器。 代码清单 2 中的 index （） 方法返回到浏览器名为 Index 的视图。

请注意，代码清单 2 中的 index （） 操作不会返回 ViewResult()。 相反，调用控制器的基类的 View() 方法。 通常情况下，您不会返回一个操作结果直接。 相反，您调用控制器的基类的以下方法之一：

1. 查看-返回一个 ViewResult 操作结果。
2. 重定向-返回 RedirectResult 操作结果。
3. RedirectToAction-返回 RedirectToRouteResult 操作结果。
4. RedirectToRoute-返回 RedirectToRouteResult 操作结果。
5. Json-返回 JsonResult 操作结果。
6. JavaScriptResult-返回 JavaScriptResult。
7. 内容-返回 ContentResult 操作结果。
8. 文件-FileContentResult、 FilePathResult 或 FileStreamResult 具体取决于参数传递给该方法返回。

因此，如果你想要返回到浏览器的视图，则调用 View() 方法。 如果你想要从一个控制器操作到另一个将用户重定向，则调用 RedirectToAction() 方法。 例如，清单 3 中的 Details() 操作显示的视图或将用户重定向到 index （） 操作，具体取决于 Id 参数是否具有值。

**代码清单 3-CustomerController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

ContentResult 操作结果比较特殊。 您可以使用 ContentResult 操作结果返回操作结果以纯文本格式。 例如，列表 4 中的 index （） 方法返回一条消息以明文形式而不是作为 HTML。

**列表 4-Controllers\StatusController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

当调用 StatusController.Index() 操作时，则不会返回一个视图。 相反，原始文本"Hello World ！" 返回到浏览器。

如果控制器操作返回的结果是不是一个操作结果-例如，日期或整数-然后将结果包装在 ContentResult 自动。 例如，调用 WorkController 列表 5 中的 index （） 操作时，返回的日期是 ContentResult 为自动。

**列表 5-WorkController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

列表 5 中的 index （） 操作返回一个 DateTime 对象。 ASP.NET MVC 框架将 DateTime 对象转换为字符串和日期时间值中 ContentResult 可以自动换行。 在浏览器接收的日期和时间以纯文本格式。

## <a name="summary"></a>总结

本教程的目的是向您介绍了 ASP.NET MVC 控制器、 控制器操作和控制器操作结果的概念。 在第一个部分中，您学习了如何将新的控制器添加到 ASP.NET MVC 项目。 接下来，您学习了如何公共控制器方法被称为宇宙到控制器操作。 最后，我们讨论了不同类型的操作可以从控制器操作返回的结果。 具体而言，我们讨论了如何从控制器操作返回一个 ViewResult，RedirectToActionResult 和 ContentResult。

> [!div class="step-by-step"]
> [上一页](creating-an-action-vb.md)
> [下一页](creating-custom-routes-cs.md)
