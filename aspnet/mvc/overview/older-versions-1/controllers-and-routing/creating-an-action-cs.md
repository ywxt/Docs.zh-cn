---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 创建操作 (C#) |Microsoft Docs
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被操作的要求。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: d6f981201b93e3650b18f112dd9330f1470aa573
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372493"
---
<a name="creating-an-action-c"></a>创建操作 (C#)
====================
by [Microsoft](https://github.com/microsoft)

> 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被操作的要求。


本教程的目的是说明如何创建新的控制器操作。 了解有关操作方法的要求。 你还了解如何避免方法公开为一个操作。

## <a name="adding-an-action-to-a-controller"></a>将操作添加到控制器

通过将新方法添加到控制器可将新的操作添加到控制器中。 例如，在列表 1 中的控制器包含名为 index （） 的操作和名为 SayHello() 操作。 这两种方法被称为操作。

**代码清单 1-Controllers\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

以便公开到为操作领域，一种方法必须满足某些要求：

- 该方法必须是公共的。
- 该方法不能是静态方法。
- 该方法不能为扩展方法。
- 该方法不能为构造函数、 getter 或 setter。
- 方法不能有开放式泛型类型。
- 方法不是控制器基类的方法。
- 该方法不能包含**ref**或**出**参数。

请注意，没有任何限制控制器操作的返回类型。 控制器操作可以返回一个字符串，datetime 类型，或 void Random 类的实例。 ASP.NET MVC 框架将转换任何不是转换为字符串的操作结果的返回类型，并将呈现到浏览器的字符串。

添加时不违反这些要求到控制器的任何方法，该方法公开为控制器操作。 此处必须认真仔细。 连接到 Internet 的任何人都可以调用控制器操作。 例如，不要创建 DeleteMyWebsite() 控制器操作。

## <a name="preventing-a-public-method-from-being-invoked"></a>防止调用公共方法

如果您需要在控制器类中创建一个公共方法，并且不想要公开为控制器操作方法则可以阻止该方法调用通过使用 [NonAction] 属性。 例如，在代码清单 2 中的控制器包含一个名为使用 [NonAction] 特性修饰的 CompanySecrets() 的公共方法。

**代码清单 2-Controllers\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

如果你尝试通过在浏览器地址栏中键入 /Work/CompanySecrets 调用 CompanySecrets() 控制器操作然后将图 1 中收到错误消息。


[![调用 NonAction 方法](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**图 01**： 调用 NonAction 方法 ([单击以查看实际尺寸的图像](creating-an-action-cs/_static/image2.png))

> [!div class="step-by-step"]
> [上一页](creating-a-controller-cs.md)
> [下一页](asp-net-mvc-routing-overview-vb.md)
