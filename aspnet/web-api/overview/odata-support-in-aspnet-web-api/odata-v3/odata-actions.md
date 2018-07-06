---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 支持 ASP.NET Web API 2 中的 OData 操作 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。 操作的一些用途包括： 实现...
ms.author: aspnetcontent
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: e02ab21b864e328fe6892a00e5d5aca3f88eb9a2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837767"
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a>支持 ASP.NET Web API 2 中的 OData 操作
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 在 OData 中，*操作*是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。 操作的一些用途包括：
> 
> - 实现复杂的事务处理。
> - 在一次处理多个实体。
> - 允许仅对实体的某些属性的更新。
> - 将信息发送到未定义实体中的服务器。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Web API 2
> - OData 版本 3
> - Entity Framework 6


## <a name="example-rating-a-product"></a>示例： 评级产品

在此示例中，我们想要让用户评级的产品，并公开的每个产品的平均分级。 在数据库中，我们会存储一组分级，对产品进行键控。

下面是我们可能会用于表示实体框架中的评级的模型：

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

但我们不希望客户端针对 POST `ProductRating` "比率"集合的对象。 直观地说，此级别与产品集合中，关联，客户端应只需发布的分级值。

因此，而不是使用普通的 CRUD 操作，我们定义客户端可以调用的操作在产品上。 在 OData 术语中，该操作是*绑定*对产品实体。

>操作在服务器上产生负面影响。 出于此原因，它们会调用使用 HTTP POST 请求。 操作可以具有参数和返回类型，服务元数据中所述。 客户端请求正文中发送参数和服务器响应正文中发送的返回值。 若要调用的"速率产品"操作，客户端将 POST 发送到如下所示的 URI:

[!code-console[Main](odata-actions/samples/sample2.cmd)]

POST 请求中的数据是只需产品评级：

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>声明的实体数据模型中的操作

在 Web API 配置中，将添加到实体数据模型 (EDM 中) 的操作：

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

此代码定义"RateProduct"作为可以对产品实体执行的操作。 它还声明将的操作**int**参数名为"Rating"，并返回**int**值。

## <a name="add-the-action-to-the-controller"></a>将操作添加到控制器

"RateProduct"操作绑定到产品实体。 若要实现此操作，添加一个名为`RateProduct`到产品控制器：

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

请注意方法名与 EDM 中的操作的名称相匹配。 该方法具有两个参数：

- *密钥*： 速率的产品密钥。
- *参数*： 操作参数值的字典。

如果使用的默认路由约定，key 参数必须命名为"密钥"。 还有一点需要包括 **[FromOdataUri]** 属性，如所示。 此属性告知 Web API 使用 OData 语法规则分析请求 URI 中的键时。

使用*参数*获取操作参数的字典：

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

如果客户端中正确发送操作参数，值的格式设置**ModelState.IsValid**为 true。 在这种情况下，可以使用**ODataActionParameters**获取参数值的字典。 在此示例中，`RateProduct`操作采用单个参数名为"Rating"。

## <a name="action-metadata"></a>操作元数据

若要查看的服务元数据，请向 /odata/$ metadata 发送 GET 请求。 下面是声明的元数据一部分`RateProduct`操作：

[!code-xml[Main](odata-actions/samples/sample7.xml)]

**FunctionImport**元素声明了操作。 大多数字段都很容易理解，但两个值得一提：

- **IsBindable**意味着操作可以调用目标实体上至少部分时间。
- **IsAlwaysBindable**意味着始终可以在目标实体上调用操作。

不同之处是，某些操作始终都可供客户端，但其他操作可能取决于实体的状态。 例如，假设您定义一个操作，"购买"。 你可以只购买是库存的项。 如果该项是脱销，客户端不能调用该操作。

定义 EDM 中，当**操作**方法创建一个始终可绑定的操作：

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

我将讨论不始终-绑定操作 (也称为*暂时性*操作) 在此主题的后面。

## <a name="invoking-the-action"></a>调用操作

现在让我们看如何在客户端将调用此操作。 假设客户端想要让其分级为 2 的产品 ID = 4。 下面是使用 JSON 格式的请求正文的示例请求消息：

[!code-console[Main](odata-actions/samples/sample9.cmd)]

下面是响应消息：

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>绑定到实体集的操作

在上一示例中，操作绑定到单个实体： 客户端费率一个产品。 您还可以绑定到实体的集合的操作。 只需进行以下更改：

在 EDM 中，将操作添加到实体的**集合**属性。

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

在控制器方法中，省略*密钥*参数。

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

现在客户端调用 Products 实体集上的操作：

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>使用集合参数的操作

操作可以获取的值的集合的参数。 在 EDM 中，使用**CollectionParameter&lt;T&gt;** 若要将参数声明。

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

这会将名为"分级"采用的集合的参数声明**int**值。 在控制器方法中，您仍获取参数值从**ODataActionParameters**对象，但现在的值是**ICollection&lt;int&gt;** 值：

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>暂时性的操作

在"RateProduct"示例中，用户可以始终对产品评估，因此操作都可用。 但是，某些操作取决于实体的状态。 例如，在视频租赁服务中，"签出"操作不是始终可用。 （它取决于是否提供了该视频的一个副本。）此类型的操作称为*暂时性*操作。

在服务元数据，暂时性操作具有**IsAlwaysBindable**等于 false。 这是实际的默认值，因此元数据将如下所示：

[!code-xml[Main](odata-actions/samples/sample16.xml)]

此处为什么这很重要： 如果操作是暂时性的服务器需要告诉客户端操作时可用。 通过在实体中包含指向操作的执行此操作。 下面是一个示例，用于电影实体：

[!code-console[Main](odata-actions/samples/sample17.cmd)]

"#CheckOut"属性包含签出操作的链接。 如果操作不可用，则服务器会忽略链接。

若要声明 EDM 中的暂时性操作，请调用**TransientAction**方法：

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

此外，必须提供一个函数，返回给定实体的操作链接。 设置此函数通过调用**HasActionLink**。 您可以编写函数作为 lambda 表达式：

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

如果操作不可用，lambda 表达式返回一个链接到的操作。 OData 序列化程序包括此链接时序列化实体。 当操作不可用时，该函数返回`null`。

## <a name="additional-resources"></a>其他资源

[OData 操作示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
