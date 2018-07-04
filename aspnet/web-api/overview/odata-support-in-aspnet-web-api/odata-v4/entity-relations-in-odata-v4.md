---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: 使用 ASP.NET Web API 2.2 OData v4 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。 使用 OData，可以通过导航的客户端...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 56cadbabaa7ca64ba39232495e25178849d5e3c2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37377641"
---
<a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>使用 ASP.NET Web API 2.2 OData v4 中的实体关系
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> 大多数的数据集定义实体之间的关系： 客户拥有订单。书有作者;产品有供应商。 使用 OData，可以通过实体关系导航的客户端。 给定产品，您可以找到供应商。 此外可以创建或删除关系。 例如，可以设置一种产品的供应商。
> 
> 本教程演示如何支持使用 ASP.NET Web API OData v4 中的这些操作。 本教程以教程为基础[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Web API 2.1
> - OData v4
> - [Visual Studio 2013 Update 2](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - Entity Framework 6
> - .NET 4.5
> 
> 
> ## <a name="tutorial-versions"></a>教程版本
> 
> OData 版本 3，请参阅[支持 OData v3 中的实体关系](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)。


## <a name="add-a-supplier-entity"></a>添加 Supplier 实体

> [!NOTE]
> 本教程以教程为基础[创建 OData v4 终结点使用 ASP.NET Web API 2](create-an-odata-v4-endpoint.md)。


首先，我们需要相关的实体。 添加一个名为类`Supplier`模型文件夹中。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

导航属性添加到`Product`类：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

添加一个新**DbSet**到`ProductsContext`类，以便实体框架将在数据库中包含的供应商表。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

在 WebApiConfig.cs 中，添加&quot;供应商&quot;实体设置为实体数据模型：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>添加供应商控制器

添加`SuppliersController`类到 Controllers 文件夹。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

我不会显示如何添加此控制器的 CRUD 操作。 步骤是产品控制器一样 (请参阅[创建 OData v4 终结点](create-an-odata-v4-endpoint.md))。

## <a name="getting-related-entities"></a>获取相关的实体

若要获取产品的供应商，客户端发送 GET 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

若要支持此请求，添加以下方法`ProductsController`类：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

此方法使用默认命名约定

- 方法名称： GetX，其中 X 是导航属性。
- 参数名称：*密钥*

如果遵循以下命名约定，Web API 会自动将 HTTP 请求映射到控制器方法。

示例 HTTP 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

HTTP 响应示例：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>获取相关的集合

在上一示例中，产品有一个供应商。 一个导航属性还可以返回一个集合。 以下代码获取供应商的产品：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

在这种情况下，该方法返回**IQueryable**而不是**可取值为 SingleResult&lt;T&gt;**

示例 HTTP 请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

HTTP 响应示例：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>创建实体之间的关系

OData 支持创建或删除现有的两个实体之间的关系。 在 OData v4 术语中，关系是&quot;引用&quot;。 (在 OData v3，称为关系*链接*。 协议差异没有影响此教程。）

引用具有自己的 URI，处理该窗体`/Entity/NavigationProperty/$ref`。 例如，下面是用于解决产品和其供应商之间的引用的 URI:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

若要添加关系时，客户端将 POST 或 PUT 请求发送到此地址。

- 如果导航属性是一个单一实体，如`Product.Supplier`。
- 如果导航属性是一个集合，如发布`Supplier.Products`。

请求的正文包含关系中的其他实体的 URI。 下面是示例请求：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

在此示例中，客户端发送到的 PUT 请求`/Products(6)/Supplier/$ref`，即为 $ref URI`Supplier`的产品 id = 6。 如果请求成功，服务器会发送 204 （无内容） 响应：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

下面是要添加到关系的控制器方法`Product`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*NavigationProperty*参数指定要设置的关系。 (如果该实体的多个导航属性，可以添加更多`case`语句。)

*链接*参数包含供应商的 URI。 Web API 会自动分析请求正文，以获取此参数的值。

若要查找供应商，我们需要 ID （或密钥），这是的一部分*链接*参数。 若要执行此操作，请使用以下帮助器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

基本上，此方法使用 OData 库 URI 路径拆分成段，找到的段包含的密钥，然后将密钥转换为正确的类型。

## <a name="deleting-a-relationship-between-entities"></a>删除实体之间的关系

若要删除关系，客户端将 HTTP DELETE 请求发送到 $ref URI 中：

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

下面是要删除某个产品和供应商之间的关系的控制器方法：

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

在这种情况下，`Product.Supplier`是&quot;1&quot;末尾 1 对多关系，以便可以删除此关系只需通过设置`Product.Supplier`到`null`。

在中&quot;许多&quot;末尾的关系，客户端必须指定哪些相关实体中删除。 若要执行此操作，客户端发送请求的查询字符串中的相关实体的 URI。 例如，若要删除"产品 1"从"供应商 1":

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

若要在 Web API 中支持此功能，我们需要包括中的额外参数`DeleteRef`方法。 下面是要从产品中删除的控制器方法`Supplier.Products`关系。

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*键*参数是供应商的键和*relatedKey*参数是要从中删除从产品的关键`Products`关系。 请注意，Web API 会自动从查询字符串获取的密钥。
