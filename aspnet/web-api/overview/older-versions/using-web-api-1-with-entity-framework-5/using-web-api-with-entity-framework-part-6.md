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
<a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="a20f7-102">第 6 部分： 创建产品和订单控制器</span><span class="sxs-lookup"><span data-stu-id="a20f7-102">Part 6: Creating Product and Order Controllers</span></span>
====================
<span data-ttu-id="a20f7-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a20f7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a20f7-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="a20f7-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="a20f7-105">添加产品控制器</span><span class="sxs-lookup"><span data-stu-id="a20f7-105">Add a Products Controller</span></span>

<span data-ttu-id="a20f7-106">管理控制器是具有管理员权限的用户。</span><span class="sxs-lookup"><span data-stu-id="a20f7-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="a20f7-107">客户，但是，可以查看产品，但不能创建、 更新或删除它们。</span><span class="sxs-lookup"><span data-stu-id="a20f7-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="a20f7-108">我们可以轻松地限制对访问 Post、 Put 和 Delete 方法时在打开的 Get 方法。</span><span class="sxs-lookup"><span data-stu-id="a20f7-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="a20f7-109">但是，查看产品返回的数据：</span><span class="sxs-lookup"><span data-stu-id="a20f7-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="a20f7-110">`ActualCost`属性应为对客户可见 ！</span><span class="sxs-lookup"><span data-stu-id="a20f7-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="a20f7-111">解决方法是定义*数据传输对象*(DTO)，包括应为对客户可见的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="a20f7-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="a20f7-112">我们将向项目中使用 LINQ`Product`实例到`ProductDTO`实例。</span><span class="sxs-lookup"><span data-stu-id="a20f7-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="a20f7-113">添加一个名为类`ProductDTO`到 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="a20f7-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="a20f7-114">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="a20f7-114">Now add the controller.</span></span> <span data-ttu-id="a20f7-115">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="a20f7-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="a20f7-116">选择**外**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="a20f7-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="a20f7-117">在中**添加控制器**对话框中，将控制器命名&quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="a20f7-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="a20f7-118">下**模板**，选择**空 API 控制器**。</span><span class="sxs-lookup"><span data-stu-id="a20f7-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="a20f7-119">源文件中的所有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a20f7-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="a20f7-120">控制器仍使用`OrdersContext`查询数据库。</span><span class="sxs-lookup"><span data-stu-id="a20f7-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="a20f7-121">而不是返回，但是`Product`实例直接，我们调用`MapProducts`投影到它们`ProductDTO`实例：</span><span class="sxs-lookup"><span data-stu-id="a20f7-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="a20f7-122">`MapProducts`方法将返回**IQueryable**，因此我们可以编写其他查询参数的结果。</span><span class="sxs-lookup"><span data-stu-id="a20f7-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="a20f7-123">您所见到这`GetProduct`方法，这会增加**其中**对查询子句：</span><span class="sxs-lookup"><span data-stu-id="a20f7-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="a20f7-124">添加一个订单控制器</span><span class="sxs-lookup"><span data-stu-id="a20f7-124">Add an Orders Controller</span></span>

<span data-ttu-id="a20f7-125">接下来，添加一个控制器，使用户能够创建和查看订单。</span><span class="sxs-lookup"><span data-stu-id="a20f7-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="a20f7-126">我们将开始另一个 DTO。</span><span class="sxs-lookup"><span data-stu-id="a20f7-126">We'll start with another DTO.</span></span> <span data-ttu-id="a20f7-127">在解决方案资源管理器，右键单击模型文件夹并添加一个名为类`OrderDTO`使用以下实现：</span><span class="sxs-lookup"><span data-stu-id="a20f7-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="a20f7-128">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="a20f7-128">Now add the controller.</span></span> <span data-ttu-id="a20f7-129">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="a20f7-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="a20f7-130">选择**外**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="a20f7-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="a20f7-131">在中**添加控制器**对话框中，设置以下选项：</span><span class="sxs-lookup"><span data-stu-id="a20f7-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="a20f7-132">下**控制器名称**，输入"OrdersController"。</span><span class="sxs-lookup"><span data-stu-id="a20f7-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="a20f7-133">下**模板**，选择"包含读/写操作，使用实体框架 API 控制器"。</span><span class="sxs-lookup"><span data-stu-id="a20f7-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="a20f7-134">下**模型类**，选择&quot;顺序 (ProductStore.Models)&quot;。</span><span class="sxs-lookup"><span data-stu-id="a20f7-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="a20f7-135">下**数据上下文类**，选择&quot;OrdersContext (ProductStore.Models)&quot;。</span><span class="sxs-lookup"><span data-stu-id="a20f7-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="a20f7-136">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="a20f7-136">Click **Add**.</span></span> <span data-ttu-id="a20f7-137">这会添加一个名为 OrdersController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="a20f7-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="a20f7-138">接下来，我们需要修改控制器的默认实现。</span><span class="sxs-lookup"><span data-stu-id="a20f7-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="a20f7-139">首先，删除`PutOrder`和`DeleteOrder`方法。</span><span class="sxs-lookup"><span data-stu-id="a20f7-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="a20f7-140">对于此示例中，客户不能修改或删除现有订单。</span><span class="sxs-lookup"><span data-stu-id="a20f7-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="a20f7-141">在实际的应用程序，需要大量的后端逻辑来处理这些情况。</span><span class="sxs-lookup"><span data-stu-id="a20f7-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="a20f7-142">（例如，是订单已发货？）</span><span class="sxs-lookup"><span data-stu-id="a20f7-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="a20f7-143">更改`GetOrders`方法以返回只属于用户的订单：</span><span class="sxs-lookup"><span data-stu-id="a20f7-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="a20f7-144">更改`GetOrder`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a20f7-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="a20f7-145">下面是我们对该方法所做的更改：</span><span class="sxs-lookup"><span data-stu-id="a20f7-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="a20f7-146">返回值是`OrderDTO`实例，而不是`Order`。</span><span class="sxs-lookup"><span data-stu-id="a20f7-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="a20f7-147">当我们查询数据库中的顺序时，我们使用[DbQuery.Include](https://msdn.microsoft.com/library/gg696395)方法来提取相关`OrderDetail`和`Product`实体。</span><span class="sxs-lookup"><span data-stu-id="a20f7-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="a20f7-148">我们使用投影来平展结果。</span><span class="sxs-lookup"><span data-stu-id="a20f7-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="a20f7-149">HTTP 响应将包含产品数量与的数组：</span><span class="sxs-lookup"><span data-stu-id="a20f7-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="a20f7-150">此格式是便于客户端能够使用比原始对象图，其中包含嵌套的实体 （顺序、 详细信息，和产品）。</span><span class="sxs-lookup"><span data-stu-id="a20f7-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="a20f7-151">最后一个方法以将其视为`PostOrder`。</span><span class="sxs-lookup"><span data-stu-id="a20f7-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="a20f7-152">现在，此方法采用`Order`实例。</span><span class="sxs-lookup"><span data-stu-id="a20f7-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="a20f7-153">请考虑会发生什么情况，但如果客户端发送请求正文如下：</span><span class="sxs-lookup"><span data-stu-id="a20f7-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="a20f7-154">这是一个结构良好的顺序，并且实体框架将值得庆幸的是将其插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="a20f7-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="a20f7-155">但是，它包含的产品实体的以前不存在。</span><span class="sxs-lookup"><span data-stu-id="a20f7-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="a20f7-156">客户端只需在我们的数据库创建一个新的产品 ！</span><span class="sxs-lookup"><span data-stu-id="a20f7-156">The client just created a new product in our database!</span></span> <span data-ttu-id="a20f7-157">如果用户知道 koala 熊的顺序，这将是顺序 fullfilment 部门层大为吃惊。</span><span class="sxs-lookup"><span data-stu-id="a20f7-157">This will be a suprise to the order fullfilment department, when they see an order for koala bears.</span></span> <span data-ttu-id="a20f7-158">要说明的是，实际上谨慎接受 POST 或 PUT 请求中的数据。</span><span class="sxs-lookup"><span data-stu-id="a20f7-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="a20f7-159">若要避免此问题，请更改`PostOrder`方法才能`OrderDTO`实例。</span><span class="sxs-lookup"><span data-stu-id="a20f7-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="a20f7-160">使用`OrderDTO`若要创建`Order`。</span><span class="sxs-lookup"><span data-stu-id="a20f7-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="a20f7-161">请注意，我们使用`ProductID`和`Quantity`属性和我们忽略任何客户端发送的产品名称或价格的值。</span><span class="sxs-lookup"><span data-stu-id="a20f7-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="a20f7-162">如果产品 ID 不是有效的它将违反外的键约束在数据库中，并插入将失败，它应该。</span><span class="sxs-lookup"><span data-stu-id="a20f7-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="a20f7-163">下面是完整`PostOrder`方法：</span><span class="sxs-lookup"><span data-stu-id="a20f7-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="a20f7-164">最后，添加**Authorize**属性到控制器：</span><span class="sxs-lookup"><span data-stu-id="a20f7-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="a20f7-165">现在，只有已注册的用户可以创建或查看订单。</span><span class="sxs-lookup"><span data-stu-id="a20f7-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a20f7-166">[上一页](using-web-api-with-entity-framework-part-5.md)
> [下一页](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="a20f7-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
