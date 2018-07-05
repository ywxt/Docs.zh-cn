---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 中的路由约定 Odata |Microsoft Docs
author: MikeWasson
description: 本文介绍 Web API 使用的 OData 终结点的路由约定。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/31/2013
ms.topic: article
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63a0e4f4f61580ea9da3bd491e7a45f20cd7aaae
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370534"
---
<a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 中的路由约定 Odata
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> 本文介绍 Web API 使用的 OData 终结点的路由约定。


当 Web API 获取 OData 请求时，但它会将请求映射到控制器名称和操作名称。 映射为基础的 HTTP 方法和 URI。 例如，`GET /odata/Products(1)`映射到`ProductsController.GetProduct`。

在这篇文章的第 1 部分中，我将介绍内置的 OData 路由约定。 这些约定专为 OData 终结点，并且它们替换默认 Web API 路由系统。 (在调用时，会发生情况替换**MapODataRoute**。)

在第 2 部分，我将介绍如何添加自定义的路由约定。 当前的内置约定不涵盖整个范围的 OData Uri，但你可以扩展它们来处理其他情况。

- [内置路由约定](#conventions)
- [自定义的路由约定](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>内置路由约定

我将介绍 Web API 中的 OData 路由约定之前，它是有助于您了解 OData Uri。 [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)组成：

- 服务根
- 资源路径
- 查询选项

![](odata-routing-conventions/_static/image1.png)

对于路由，重要的部分是资源路径。 资源路径分为段。 例如，`/Products(1)/Supplier`有三个段：

- `Products` 引用名为"产品"实体集。
- `1` 是否为实体键，从组中选择单个实体。
- `Supplier` 是一个导航属性，选择相关的实体。

因此此路径提取产品 1 的供应商。

> [!NOTE]
> OData 路径段不始终对应于 URI 段。 例如，"1"被视为一个路径段。


**控制器名称。** 控制器名称始终被派生自的实体集的资源路径根目录。 例如，如果资源路径是`/Products(1)/Supplier`，Web API 将查找名为的控制器`ProductsController`。

**操作名称。** 操作名称派生自的路径段以及实体数据模型 (EDM) 中，为以下表格中列出。 在某些情况下，有两个选择的操作名称。 例如，"Get"或&quot;GetProducts&quot;。

**查询实体**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 获取 /entityset | / 产品 | GetEntitySet 或 Get | GetProducts |
| 获取 /entityset(key) | /Products(1) | GetEntityType 或 Get | 为 getproduct |
| 获取 /entityset （密钥）/强制转换 | /Products(1)/Models.Book | GetEntityType 或 Get | GetBook |

有关详细信息，请参阅[创建只读 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。

**创建、 更新和删除实体**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 发布 /entityset | / 产品 | PostEntityType 或 Post | PostProduct |
| 放置 /entityset(key) | /Products(1) | PutEntityType 或 Put | PutProduct |
| PUT /entityset （密钥）/强制转换 | /Products(1)/Models.Book | PutEntityType 或 Put | PutBook |
| 修补程序 /entityset(key) | /Products(1) | PatchEntityType 或修补程序 | PatchProduct |
| 修补程序 /entityset （密钥）/强制转换 | /Products(1)/Models.Book | PatchEntityType 或修补程序 | PatchBook |
| 删除 /entityset(key) | /Products(1) | DeleteEntityType 或 Delete | DeleteProduct |
| 删除 /entityset （密钥）/强制转换 | /Products(1)/Models.Book | DeleteEntityType 或 Delete | DeleteBook |

**查询的导航属性**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| GET /entityset （密钥） / 导航 | / 产品 （1）/供应商 | GetNavigationFromEntityType 或 GetNavigation | GetSupplierFromProduct |
| 获取 /entityset （密钥）/转换/导航 | /Products(1)/Models.Book/Author | GetNavigationFromEntityType 或 GetNavigation | GetAuthorFromBook |

有关详细信息，请参阅[使用的实体关系](odata-v3/working-with-entity-relations.md)。

**创建和删除链接**

| 请求 | 示例 URI | 操作名称 |
| --- | --- | --- |
| 开机自检 /entityset （密钥） / $links/导航 | / 产品 （1） / $ 链接/供应商 | CreateLink |
| PUT 的 /entityset （密钥） / $links/导航 | / 产品 （1） / $ 链接/供应商 | CreateLink |
| 删除 /entityset （密钥） / $links/导航 | / 产品 （1） / $ 链接/供应商 | DeleteLink |
| 删除 /entityset(key)/$links/navigation(relatedKey) | /Products/(1)/$links/Suppliers(1) | DeleteLink |

有关详细信息，请参阅[使用的实体关系](odata-v3/working-with-entity-relations.md)。

**属性**

*需要 Web API 2*

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| GET /entityset （密钥） / 属性 | /Products(1)/Name | GetPropertyFromEntityType 或 GetProperty | GetNameFromProduct |
| 获取 /entityset （密钥）/转换/属性 | /Products(1)/Models.Book/Author | GetPropertyFromEntityType 或 GetProperty | GetTitleFromBook |

**操作**

| 请求 | 示例 URI | 操作名称 | 示例操作 |
| --- | --- | --- | --- |
| 开机自检 /entityset （密钥） / 操作 | / 产品 （1）/速率 | ActionNameOnEntityType 或 ActionName | RateOnProduct |
| 后 /entityset （密钥）/转换/操作 | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType 或 ActionName | CheckOutOnBook |

有关详细信息，请参阅[OData 操作](odata-v3/odata-actions.md)。

**方法签名**

下面是一些规则的方法签名：

- 如果路径包含一个键，操作应具有一个名为参数*密钥*。
- 如果路径包含一个键到导航属性，该操作应具有名为的参数*relatedKey*。
- 修饰*键*并*relatedKey*使用的参数 **[FromODataUri]** 参数。
- POST 和 PUT 请求需要实体类型的参数。
- PATCH 请求采用的类型参数**增量&lt;T&gt;**，其中*T*是实体类型。

有关参考，下面是一个示例，说明每个内置的 OData 路由约定的方法签名。

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>自定义的路由约定

当前的内置约定不涵盖所有可能的 OData Uri。 可以通过实现来添加新的惯例**IODataRoutingConvention**接口。 此接口有两个方法：

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController**返回控制器的名称。
- **SelectAction**返回操作的名称。

对于这两种方法，如果约定不适用于该请求，该方法应返回 null。

**ODataPath**参数表示已分析的 OData 资源路径。 它包含一系列**[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 实例，一个用于资源路径的每个段。 **ODataPathSegment**是一个抽象类; 每个段类型由派生的类**ODataPathSegment**。

**ODataPath.TemplatePath**属性是一个字符串，表示串联所有路径段。 例如，如果 URI 是`/Products(1)/Supplier`，路径模板&quot;~/entityset/key/navigation&quot;。 请注意，段不直接对应于 URI 段。 例如，实体键 (1) 表示为其自身**ODataPathSegment**。

通常情况下，实现**IODataRoutingConvention**执行以下操作：

1. 进行比较以查看此约定应用于当前请求的路径模板。 如果不适用，则返回 null。
2. 如果约定适用，则使用的属性**ODataPathSegment**控制器和操作名称派生的实例。
3. 对于操作，将添加到路由字典应绑定到操作参数 （通常是实体键） 的任何值。

让我们看一下具体的示例。 导航集合中建立索引不支持的内置路由约定。 换而言之，没有任何 Uri 约定如下所示：

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

下面是查询的自定义的路由约定来处理此类型。

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

注意：

1. 我从派生出**EntitySetRoutingConvention**，因为**SelectController**在该类中的方法适合于此新的路由约定。 这意味着我无需重新实现**SelectController**。
2. 约定仅适用于 GET 请求和路径模板时才&quot;~/entityset/key/navigation/key&quot;。
3. 操作名称是&quot;获取 {EntityType}&quot;，其中 *{EntityType}* 是导航集合的类型。 例如， &quot;GetSupplier&quot;。 可以使用你喜欢的任何命名约定&#8212;只需确保控制器操作匹配。
4. 将名为两个参数的操作*键*并*relatedKey*。 (有关某些预定义的参数名称的列表，请参阅[ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)。)

下一步将新的约定添加到路由约定的列表。 发生这种情况在配置期间，如下面的代码中所示：

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

下面是一些其他示例路由约定的有用来研究：

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

Web API 本身当然是开放源代码，以便您可以看到[源代码](http://aspnetwebstack.codeplex.com/)的内置路由约定。 这些定义在**System.Web.Http.OData.Routing.Conventions**命名空间。
