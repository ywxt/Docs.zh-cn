---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: 验证使用服务层 (C#) |Microsoft Docs
author: StephenWalther
description: 了解如何将移动应用验证逻辑从控制器操作和到单独的服务层。 在本教程中，Stephen Walther 解释了如何在...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 69ff78949589017d12a791231e38b400b49f2917
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824759"
---
<a name="validating-with-a-service-layer-c"></a>使用服务层 (C#) 进行验证
====================
通过[Stephen Walther](https://github.com/StephenWalther)

> 了解如何将移动应用验证逻辑从控制器操作和到单独的服务层。 在本教程中，Stephen Walther 解释了如何通过隔离您从控制器层的服务层维护清晰分离关注点。


本教程的目的是介绍 ASP.NET MVC 应用程序中执行验证的一种方法。 在本教程中，您将学习如何移动你的验证逻辑超出你的控制器和到单独的服务层。

## <a name="separating-concerns"></a>分离关注点

在生成的 ASP.NET MVC 应用程序时，不应在控制器操作内将你数据库的逻辑。 混合数据库和控制器逻辑使得你的应用程序随着时间的推移维护更困难。 建议是您将所有数据库逻辑放置在一个独立的存储库层。

例如，列表 1 中包含名为化 ProductRepository 简单的存储库。 产品存储库包含所有应用程序的数据访问代码。 该列表还包括产品存储库实现的 IProductRepository 接口。

**代码清单 1-Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

列表 2 中的控制器在其 index （） 和 create （） 操作中使用存储库层。 请注意，此控制器不包含数据库的任何逻辑。 创建存储库层，可保持完全分离关注点。 控制器负责应用程序流控制逻辑和存储库是负责数据访问逻辑。

**代码清单 2-Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>创建服务层

因此，应用程序流控制逻辑位于控制器和数据访问逻辑所属的存储库中。 在这种情况下，您认为您的验证逻辑？ 一种方法是将放置在您的验证逻辑*服务层*。

服务层是 ASP.NET MVC 应用程序，可协调控制器和存储库层之间的通信的附加层。 服务层包含业务逻辑。 具体而言，它包含验证逻辑。

例如，清单 3 中的产品服务层具有 CreateProduct() 方法。 CreateProduct() 方法调用 ValidateProduct() 方法来验证新产品，然后再将该产品传递到产品存储库。

**代码清单 3-Models\ProductService.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

列表 4，而不是存储库层使用的服务层中的已更新的产品控制器。 控制器层与服务层进行通信。 服务层与存储库层。 每个层都有单独的责任。

**列表 4-Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

请注意，产品控制器构造函数中创建产品服务。 创建产品服务时，模型状态字典传递到服务。 产品服务使用模型状态将验证错误消息传递到控制器。

## <a name="decoupling-the-service-layer"></a>分离的服务层

我们无法隔离的控制器和在以下方面的服务层。 控制器和服务层进行通信来通过模型状态。 换而言之，服务层具有 ASP.NET MVC framework 的某个特定功能的依赖项。

我们想要隔离我们尽可能多的控制器层中的服务层。 从理论上讲，我们应该能够使用任何类型的应用程序并不只一个 ASP.NET MVC 应用程序使用的服务层。 例如，在将来，我们可能想要生成 WPF 应用程序前端。 我们应从我们的服务层提供一种方法来删除对 ASP.NET MVC 的依赖关系模型状态。

在清单 5 的服务层进行了更新，以使其不再使用的模型状态。 相反，它使用的任何类都实现 IValidationDictionary 接口。

**列表 5-Models\ProductService.cs （分离式）**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

列表 6 中定义了 IValidationDictionary 接口。 此简单接口具有单个方法和单个属性。

**代码清单 6-Models\IValidationDictionary.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

在列表 7 中，名为 ModelStateWrapper 类，该类实现 IValidationDictionary 接口。 可以通过将模型状态字典传递到构造函数来实例化 ModelStateWrapper 类。

**列表 7-Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

最后，代码清单 8 中已更新的控制器使用 ModelStateWrapper 在其构造函数中创建的服务层时。

**代码清单 8-Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

使用 IValidationDictionary 接口和 ModelStateWrapper 类使我们能够将我们的服务层从我们的控制器层完全隔离。 服务层不再依赖于模型状态。 可以将传递的任何类都实现为服务层 IValidationDictionary 接口。 例如，WPF 应用程序可以实现简单的集合类的 IValidationDictionary 接口。

## <a name="summary"></a>总结

本教程的目的是讨论 ASP.NET MVC 应用程序中执行验证的一种方法。 在本教程中，您学习了如何将您的验证逻辑超出你的控制器和到单独的服务层的所有移动。 您还学习了如何通过创建 ModelStateWrapper 类隔离您从控制器层的服务层。

> [!div class="step-by-step"]
> [上一页](validating-with-the-idataerrorinfo-interface-cs.md)
> [下一页](validation-with-the-data-annotation-validators-cs.md)
