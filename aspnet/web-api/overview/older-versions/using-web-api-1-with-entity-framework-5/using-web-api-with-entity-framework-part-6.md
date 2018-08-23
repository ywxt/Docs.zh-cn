---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 第 6 部分： 创建产品和订单控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: 642ff4554ed3664af0b5cc8e49d6b236c568131b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832921"
---
<a name="part-6-creating-product-and-order-controllers"></a>第 6 部分： 创建产品和订单控制器
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>添加产品控制器

管理控制器是具有管理员权限的用户。 客户，但是，可以查看产品，但不能创建、 更新或删除它们。

我们可以轻松地限制对访问 Post、 Put 和 Delete 方法时在打开的 Get 方法。 但是，查看产品返回的数据：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

`ActualCost`属性应为对客户可见 ！ 解决方法是定义*数据传输对象*(DTO)，包括应为对客户可见的属性的子集。 我们将向项目中使用 LINQ`Product`实例到`ProductDTO`实例。

添加一个名为类`ProductDTO`到 Models 文件夹。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

现在添加控制器。 在解决方案资源管理器，右键单击 Controllers 文件夹。 选择**外**，然后选择**控制器**。 在中**添加控制器**对话框中，将控制器命名&quot;ProductsController&quot;。 下**模板**，选择**空 API 控制器**。

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

源文件中的所有内容替换为以下代码：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

控制器仍使用`OrdersContext`查询数据库。 而不是返回，但是`Product`实例直接，我们调用`MapProducts`投影到它们`ProductDTO`实例：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts`方法将返回**IQueryable**，因此我们可以编写其他查询参数的结果。 您所见到这`GetProduct`方法，这会增加**其中**对查询子句：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>添加一个订单控制器

接下来，添加一个控制器，使用户能够创建和查看订单。

我们将开始另一个 DTO。 在解决方案资源管理器，右键单击模型文件夹并添加一个名为类`OrderDTO`使用以下实现：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

现在添加控制器。 在解决方案资源管理器，右键单击 Controllers 文件夹。 选择**外**，然后选择**控制器**。 在中**添加控制器**对话框中，设置以下选项：

- 下**控制器名称**，输入"OrdersController"。
- 下**模板**，选择"包含读/写操作，使用实体框架 API 控制器"。
- 下**模型类**，选择&quot;顺序 (ProductStore.Models)&quot;。
- 下**数据上下文类**，选择&quot;OrdersContext (ProductStore.Models)&quot;。

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

单击 **添加**。 这会添加一个名为 OrdersController.cs 文件。 接下来，我们需要修改控制器的默认实现。

首先，删除`PutOrder`和`DeleteOrder`方法。 对于此示例中，客户不能修改或删除现有订单。 在实际的应用程序，需要大量的后端逻辑来处理这些情况。 （例如，是订单已发货？）

更改`GetOrders`方法以返回只属于用户的订单：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

更改`GetOrder`方法，如下所示：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

下面是我们对该方法所做的更改：

- 返回值是`OrderDTO`实例，而不是`Order`。
- 当我们查询数据库中的顺序时，我们使用[DbQuery.Include](https://msdn.microsoft.com/library/gg696395)方法来提取相关`OrderDetail`和`Product`实体。
- 我们使用投影来平展结果。

HTTP 响应将包含产品数量与的数组：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

此格式是便于客户端能够使用比原始对象图，其中包含嵌套的实体 （顺序、 详细信息，和产品）。

最后一个方法以将其视为`PostOrder`。 现在，此方法采用`Order`实例。 请考虑会发生什么情况，但如果客户端发送请求正文如下：

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

这是一个结构良好的顺序，并且实体框架将值得庆幸的是将其插入到数据库。 但是，它包含的产品实体的以前不存在。 客户端只需在我们的数据库创建一个新的产品 ！ 如果用户知道 koala 熊的顺序，这将是顺序 fullfilment 部门层大为吃惊。 要说明的是，实际上谨慎接受 POST 或 PUT 请求中的数据。

若要避免此问题，请更改`PostOrder`方法才能`OrderDTO`实例。 使用`OrderDTO`若要创建`Order`。

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

请注意，我们使用`ProductID`和`Quantity`属性和我们忽略任何客户端发送的产品名称或价格的值。 如果产品 ID 不是有效的它将违反外的键约束在数据库中，并插入将失败，它应该。

下面是完整`PostOrder`方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

最后，添加**Authorize**属性到控制器：

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

现在，只有已注册的用户可以创建或查看订单。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-5.md)
> [下一页](using-web-api-with-entity-framework-part-7.md)
