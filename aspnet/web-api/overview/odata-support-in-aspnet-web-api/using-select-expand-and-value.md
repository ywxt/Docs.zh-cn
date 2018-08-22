---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: 使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/11/2013
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: d198ecf40155cba36204bc0810f4735aae6b100b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825679"
---
<a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a>使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value
====================
通过[Mike Wasson](https://github.com/MikeWasson)

Web API 2 添加了支持 $ expand，$select 和在 OData 中的 $value 选项。 这些选项允许客户端来控制该通道从服务器返回的表示形式。

- **$expand**导致相关的实体是以内联形式包含在响应中的。
- **$select**选择要在响应中包含的属性的子集。
- **$value**获取属性的原始值。

## <a name="example-schema"></a>示例架构

对于本文中，我将使用 OData 服务，用于定义三个实体： 产品、 供应商和类别。 每个产品都有一个类别和一个供应商。

![](using-select-expand-and-value/_static/image1.png)

下面是定义实体模型的 C# 类：

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

请注意，`Product`类定义的导航属性`Supplier`和`Category`。 `Category`类定义中每个类别的产品的导航属性。

若要创建此架构的 OData 终结点，请使用 Visual Studio 2013 的基架，如中所述[在 ASP.NET Web API 中创建 OData 终结点](odata-v3/creating-an-odata-endpoint.md)。 有关产品、 类别和供应商添加单独的控制器。

## <a name="enabling-expand-and-select"></a>启用 $展开和 $select

在 Visual Studio 2013 中，Web API OData 基架创建一个控制器，来自动支持 $expand 和 $select。 有关参考，下面是支持 $ 要求展开和 $select 控制器中的。

对于集合，该控制器`Get`方法必须返回**IQueryable**。

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

对于单个实体，返回**可取值为 SingleResult&lt;T&gt;**，其中 T 为**IQueryable** ，其中包含零个或一个实体。

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

此外，修饰您`Get`方法与 **[Queryable]** 属性，如前面的代码片段中所示。 或者，调用**EnableQuerySupport**上**HttpConfiguration**在启动时的对象。 (有关详细信息，请参阅[启用 OData 查询选项](supporting-odata-query-options.md#enable)。)

## <a name="using-expand"></a>使用 $expand

在查询的 OData 实体或集合时，默认响应不包括相关的实体。 例如，下面是类别实体集的默认响应：

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

正如您所看到的即使类别实体具有一个产品的导航链接响应不包括任何产品。 但是，客户端可以使用 $展开此项可获取每个类别的产品列表。 $Expand 选项中请求的查询字符串：

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

现在服务器将包括每个类别，各类别的内联的产品。 下面是响应负载：

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

请注意"value"数组中的每个项包含的产品列表。

$ Expand 选项采用以逗号分隔列表与要扩展的导航属性。 以下请求展开该类别和产品的供应商。

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

下面是响应正文：

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

您可以展开多个导航属性的级别。 下面的示例包括一个类别的所有产品以及每个产品的供应商。

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

下面是响应正文：

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

默认情况下，Web API 限制为 2 的最大展开深度。 防止发送等复杂请求客户端`$expand=Orders/OrderDetails/Product/Supplier/Region`，这可能很低效查询并创建大型的响应。 若要重写默认值，设置**MaxExpansionDepth**上的属性 **[Queryable]** 属性。

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

详细了解 $ expand 选项，请参阅[展开 ($expand) 系统查询选项](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand)官方 OData 文档中。

## <a name="using-select"></a>使用 $select

$Select 选项指定要在响应正文中包含的属性的子集。 例如，若要获取的名称和每个产品的价格，请使用以下查询：

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

下面是响应正文：

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

你可以组合 $select 和 $expand 中相同的查询。 请确保在 $select 选项中包含扩展的属性。 例如，以下请求获取的产品名称和供应商。

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

下面是响应正文：

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

此外可以选择一个扩展属性中的属性。 以下请求扩展产品，并选择类别名称和产品名称。

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

下面是响应正文：

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

有关 $select 选项的详细信息，请参阅[Select 系统查询选项 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select)官方 OData 文档中。

## <a name="getting-individual-properties-of-an-entity-value"></a>获取单个实体 ($value) 的属性

有两种方法可从实体获取的个别属性的 OData 客户端。 客户端可以获取 OData 格式的值或获取属性的原始值。

以下请求获取 OData 格式的属性。

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

此处是 JSON 格式的示例响应：

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

若要获取的属性的原始值，向 URI 追加 $value:

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

下面是响应。 请注意，内容类型"text/plain"不是 JSON。

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

若要在 OData 控制器中支持这些查询，将添加一个名为方法`GetProperty`，其中`Property`是属性的名称。 例如，若要获取的 Name 属性的方法将被命名为`GetName`。 该方法应返回该属性的值：

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
