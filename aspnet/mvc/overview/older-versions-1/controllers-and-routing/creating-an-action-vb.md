---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 创建操作 (VB) |Microsoft Docs
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被操作的要求。
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: 6ec69f5aa9f7a789cb533a8dc04dca952adf35d0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824041"
---
<a name="creating-an-action-vb"></a>创建操作 (VB)
====================
by [Microsoft](https://github.com/microsoft)

> 了解如何向 ASP.NET MVC 控制器中添加新操作。 了解有关该方法将被操作的要求。


本教程的目的是说明如何创建新的控制器操作。 了解有关操作方法的要求。 你还了解如何避免方法公开为一个操作。

## <a name="adding-an-action-to-a-controller"></a>将操作添加到控制器

通过将新方法添加到控制器可将新的操作添加到控制器中。 例如，在列表 1 中的控制器包含名为 index （） 的操作和名为 SayHello() 操作。 这两种方法被称为操作。

**代码清单 1-Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

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

如果需要在控制器类中创建一个公共方法，并且不想要公开为控制器操作方法，则可以防止该方法通过调用&lt;NonAction&gt;属性。 例如，在代码清单 2 中的控制器包含一个名为 CompanySecrets() 用修饰的公共方法&lt;NonAction&gt;属性。

**代码清单 2-Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

如果你尝试通过在浏览器地址栏中键入 /Work/CompanySecrets 调用 CompanySecrets() 控制器操作然后将图 1 中收到错误消息。


[![调用 NonAction 方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**图 01**： 调用 NonAction 方法 ([单击以查看实际尺寸的图像](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [上一页](creating-a-controller-vb.md)
> [下一页](aspnet-mvc-controllers-overview-cs.md)
