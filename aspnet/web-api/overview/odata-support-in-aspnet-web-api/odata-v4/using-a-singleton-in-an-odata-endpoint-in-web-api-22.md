---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 创建 OData v4 中的单一实例使用 Web API 2.2 |Microsoft Docs
author: rick-anderson
description: 本主题演示如何在 Web API 2.2 中的 OData 终结点中定义单一实例。
ms.author: aspnetcontent
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: baccfed79949ae4efd45395bed3ad0058549cb4c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830511"
---
<a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>创建使用 Web API 2.2 OData v4 中的单一实例
====================
通过 Zoe 卢奥语

> 传统上，如果它已封装在实体集内可以只访问实体。 但 OData v4 提供了两个附加选项，单独预测查询和包含关系，这两种支持 WebAPI 2.2。


本文介绍如何在 Web API 2.2 中的 OData 终结点中定义单一实例。 有关哪些单一实例以及如何从使用它受益的信息，请参阅[使用单一实例定义特殊实体](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。 若要创建 Web API OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。 

使用以下数据模型在 Web API 项目中，我们将创建单一实例：

![数据模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

名为单一实例`Umbrella`将根据类型来定义`Company`，和实体集命名`Employees`将基于类型定义`Employee`。

可以从下载本教程中使用的解决方案[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)。

## <a name="define-the-data-model"></a>定义数据模型

1. 定义 CLR 类型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. 生成基于 CLR 类型的 EDM 模型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    在这里，`builder.Singleton<Company>("Umbrella")`告知模型生成器来创建名为单一实例`Umbrella`EDM 模型中。

    生成的元数据将如下所示：

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    从元数据中我们可以看到，导航属性`Company`中`Employees`实体集绑定到单一实例`Umbrella`。 会自动完成绑定`ODataConventionModelBuilder`，因为仅`Umbrella`具有`Company`类型。 如果在模型中存在任何多义性，可以使用`HasSingletonBinding`显式将一个导航属性绑定到单一实例;`HasSingletonBinding`具有相同的效果与使用`Singleton`CLR 类型定义中的属性：

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>定义单一实例控制器

单一实例控制器从与 EntitySet 控制器类似的继承`ODataController`，并单独控制器名称应为`[singletonName]Controller`。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

若要处理不同类型的请求，操作需要进行预定义，在控制器中。 **属性路由**WebApi 2.2 中的默认情况下启用。 例如，若要定义要处理查询的操作`Revenue`从`Company`使用属性路由中，使用以下：

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

如果您不愿意来定义每个操作的属性，只需定义按照你的操作[OData 路由约定](../odata-routing-conventions.md)。 由于密钥不需要查询单一实例，单独控制器中定义的操作是从 entityset 控制器中定义的操作略有不同。

有关参考，下面列出了每个操作定义中的单一实例控制器中的方法签名。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

基本上，这是所有需要在服务端上执行操作。 [示例项目](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含的所有解决方案和演示如何使用单一实例的 OData 客户端代码。 中的步骤生成客户端[创建 OData v4 客户端应用](create-an-odata-v4-client-app.md)。

. 

*感谢您对 Leo Hu 这篇文章的原始内容。*
