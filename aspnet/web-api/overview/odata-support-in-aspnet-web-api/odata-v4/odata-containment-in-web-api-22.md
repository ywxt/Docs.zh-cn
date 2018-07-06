---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: 包含 OData v4 中的使用 Web API 2.2 |Microsoft Docs
author: rick-anderson
description: 传统上，如果它已封装在实体集内可以只访问实体。 但是，OData v4 提供两个其他选项，单独预测查询和 Con...
ms.author: aspnetcontent
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 56e550b56e9ad237dbf4fab04f2bd545164ee90a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824907"
---
<a name="containment-in-odata-v4-using-web-api-22"></a>使用 Web API 2.2 OData v4 中的包含关系
====================
通过 Jinfu Tan

> 传统上，如果它已封装在实体集内可以只访问实体。 但 OData v4 提供了两个附加选项，单独预测查询和包含关系，这两种支持 WebAPI 2.2。


本主题演示如何定义包含 WebApi 2.2 中的 OData 终结点中。 包含有关详细信息，请参阅[包含即将与 OData v4](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)。 若要创建 Web API OData V4 终结点，请参阅[创建 OData v4 终结点使用 ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md)。

首先，我们将在 OData 服务中，使用此数据模型创建包含域模型：

![数据模型](odata-containment-in-web-api-22/_static/image1.png)

一个帐户包含许多 PaymentInstruments (PI)，但我们未定义的实体集为 PI。 相反，仅可以通过帐户访问 Pi。

您可以下载从本主题中使用的解决方案[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)。

## <a name="defining-the-data-model"></a>定义数据模型

1. 定义 CLR 类型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`属性用于包含导航属性。
2. 生成基于 CLR 类型的 EDM 模型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder`将处理生成的 EDM 模型，如果`Contained`属性添加到相应的导航属性。 如果属性为集合类型，`GetCount(string NameContains)`还将创建函数。

    生成的元数据将如下所示：

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`属性指示的导航属性为包含。

## <a name="define-the-containing-entity-set-controller"></a>定义包含实体集控制器

包含的实体不具有其自己的控制器;包含实体集控制器中定义该操作。 在此示例中，没有 AccountsController，但没有 PaymentInstrumentsController。

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

如果 OData 路径是 4 个或多个段，仅特性路由的工作原理，如`[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]`上述控制器中。 否则，属性和传统路由工作原理： 例如，`GetPayInPIs(int key)`匹配`GET ~/Accounts(1)/PayinPIs`。

*感谢您对 Leo Hu 这篇文章的原始内容。*
