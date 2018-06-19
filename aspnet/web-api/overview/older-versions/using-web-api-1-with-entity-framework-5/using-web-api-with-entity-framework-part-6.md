---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 第 6 部分： 创建产品和顺序控制器 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: 6bd485d29821af12b9ebe31b2d04a2d9ab826731
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869382"
---
<a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="7e274-102">第 6 部分： 创建产品和顺序控制器</span><span class="sxs-lookup"><span data-stu-id="7e274-102">Part 6: Creating Product and Order Controllers</span></span>
====================
<span data-ttu-id="7e274-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7e274-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7e274-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="7e274-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="7e274-105">添加产品控制器</span><span class="sxs-lookup"><span data-stu-id="7e274-105">Add a Products Controller</span></span>

<span data-ttu-id="7e274-106">管理控制器是具有管理员特权权限的用户。</span><span class="sxs-lookup"><span data-stu-id="7e274-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="7e274-107">客户，另一方面，可以查看产品但不能创建、 更新或删除它们。</span><span class="sxs-lookup"><span data-stu-id="7e274-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="7e274-108">我们可以轻松地限制访问的 Post、 Put 和 Delete 的方法，同时 Get 方法。</span><span class="sxs-lookup"><span data-stu-id="7e274-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="7e274-109">但讨论的产品返回的数据：</span><span class="sxs-lookup"><span data-stu-id="7e274-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="7e274-110">`ActualCost`属性不应为对客户可见 ！</span><span class="sxs-lookup"><span data-stu-id="7e274-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="7e274-111">解决方法是定义*数据传输对象*(DTO)，包括应对客户可见的属性的子集。</span><span class="sxs-lookup"><span data-stu-id="7e274-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="7e274-112">我们将向项目中使用 LINQ`Product`实例到`ProductDTO`实例。</span><span class="sxs-lookup"><span data-stu-id="7e274-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="7e274-113">添加一个名为类`ProductDTO`到 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="7e274-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="7e274-114">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="7e274-114">Now add the controller.</span></span> <span data-ttu-id="7e274-115">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="7e274-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="7e274-116">选择**添加**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="7e274-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="7e274-117">在**添加控制器**对话框中，控制器&quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="7e274-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="7e274-118">下**模板**，选择**空 API 控制器**。</span><span class="sxs-lookup"><span data-stu-id="7e274-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="7e274-119">将源文件中的所有内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7e274-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="7e274-120">控制器仍使用`OrdersContext`查询数据库。</span><span class="sxs-lookup"><span data-stu-id="7e274-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="7e274-121">但而不是返回`Product`实例直接，我们调用`MapProducts`投影到它们`ProductDTO`实例：</span><span class="sxs-lookup"><span data-stu-id="7e274-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="7e274-122">`MapProducts`方法返回**IQueryable**，因此我们可以编写结果与其他查询参数。</span><span class="sxs-lookup"><span data-stu-id="7e274-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="7e274-123">你可以看到此中`GetProduct`方法，以便将添加**其中**对查询子句：</span><span class="sxs-lookup"><span data-stu-id="7e274-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="7e274-124">添加 Orders 控制器</span><span class="sxs-lookup"><span data-stu-id="7e274-124">Add an Orders Controller</span></span>

<span data-ttu-id="7e274-125">接下来，添加允许用户创建和查看订单的控制器。</span><span class="sxs-lookup"><span data-stu-id="7e274-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="7e274-126">我们将开始另一个 DTO。</span><span class="sxs-lookup"><span data-stu-id="7e274-126">We'll start with another DTO.</span></span> <span data-ttu-id="7e274-127">在解决方案资源管理器，右键单击 Models 文件夹，并添加一个名为类`OrderDTO`使用以下实现：</span><span class="sxs-lookup"><span data-stu-id="7e274-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="7e274-128">现在添加控制器。</span><span class="sxs-lookup"><span data-stu-id="7e274-128">Now add the controller.</span></span> <span data-ttu-id="7e274-129">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="7e274-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="7e274-130">选择**添加**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="7e274-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="7e274-131">在**添加控制器**对话框中，设置以下选项：</span><span class="sxs-lookup"><span data-stu-id="7e274-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="7e274-132">下**控制器名称**，输入"OrdersController"。</span><span class="sxs-lookup"><span data-stu-id="7e274-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="7e274-133">下**模板**，选择"读/写操作，使用 Entity Framework 的 API 控制器"。</span><span class="sxs-lookup"><span data-stu-id="7e274-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="7e274-134">下**模型类**，选择&quot;顺序 (ProductStore.Models)&quot;。</span><span class="sxs-lookup"><span data-stu-id="7e274-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="7e274-135">下**数据上下文类**，选择&quot;OrdersContext (ProductStore.Models)&quot;。</span><span class="sxs-lookup"><span data-stu-id="7e274-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="7e274-136">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="7e274-136">Click **Add**.</span></span> <span data-ttu-id="7e274-137">这将添加一个名为 OrdersController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="7e274-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="7e274-138">接下来，我们需要修改控制器的默认实现。</span><span class="sxs-lookup"><span data-stu-id="7e274-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="7e274-139">首先，删除`PutOrder`和`DeleteOrder`方法。</span><span class="sxs-lookup"><span data-stu-id="7e274-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="7e274-140">此示例中，客户无法修改或删除现有的订单。</span><span class="sxs-lookup"><span data-stu-id="7e274-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="7e274-141">在实际应用中，您将需要大量的后端逻辑来处理这些情况。</span><span class="sxs-lookup"><span data-stu-id="7e274-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="7e274-142">（例如，订单已发货？）</span><span class="sxs-lookup"><span data-stu-id="7e274-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="7e274-143">更改`GetOrders`方法来返回仅属于用户的订单：</span><span class="sxs-lookup"><span data-stu-id="7e274-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="7e274-144">更改`GetOrder`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7e274-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="7e274-145">下面是我们对方法进行了更改：</span><span class="sxs-lookup"><span data-stu-id="7e274-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="7e274-146">返回值是`OrderDTO`实例，而不是`Order`。</span><span class="sxs-lookup"><span data-stu-id="7e274-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="7e274-147">当我们查询数据库中的顺序时，我们使用[DbQuery.Include](https://msdn.microsoft.com/library/gg696395)方法以提取相关`OrderDetail`和`Product`实体。</span><span class="sxs-lookup"><span data-stu-id="7e274-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="7e274-148">我们使用投影来平展结果。</span><span class="sxs-lookup"><span data-stu-id="7e274-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="7e274-149">HTTP 响应将包含产品与数量的数组：</span><span class="sxs-lookup"><span data-stu-id="7e274-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="7e274-150">此格式是客户端使用比原始对象图，其中包含嵌套的实体 （顺序、 详细信息，和产品） 更容易。</span><span class="sxs-lookup"><span data-stu-id="7e274-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="7e274-151">要考虑将它的最后一个方法`PostOrder`。</span><span class="sxs-lookup"><span data-stu-id="7e274-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="7e274-152">现在，此方法采用`Order`实例。</span><span class="sxs-lookup"><span data-stu-id="7e274-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="7e274-153">请考虑会发生什么情况，但如果客户端发送请求正文如下：</span><span class="sxs-lookup"><span data-stu-id="7e274-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="7e274-154">这是一个结构良好的顺序，并且实体框架将不假思索地将其插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="7e274-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="7e274-155">但是，它包含以前不存在 Product 实体。</span><span class="sxs-lookup"><span data-stu-id="7e274-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="7e274-156">客户端只在我们的数据库中创建新产品 ！</span><span class="sxs-lookup"><span data-stu-id="7e274-156">The client just created a new product in our database!</span></span> <span data-ttu-id="7e274-157">如果用户知道考拉关闭的顺序，这将是向顺序 fullfilment 部门，意外情况发生。</span><span class="sxs-lookup"><span data-stu-id="7e274-157">This will be a suprise to the order fullfilment department, when they see an order for koala bears.</span></span> <span data-ttu-id="7e274-158">这说明了什么是，请真正谨慎接受 POST 或 PUT 请求中的数据。</span><span class="sxs-lookup"><span data-stu-id="7e274-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="7e274-159">若要避免此问题，更改`PostOrder`方法才能`OrderDTO`实例。</span><span class="sxs-lookup"><span data-stu-id="7e274-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="7e274-160">使用`OrderDTO`创建`Order`。</span><span class="sxs-lookup"><span data-stu-id="7e274-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="7e274-161">请注意，我们使用`ProductID`和`Quantity`属性和我们忽略客户端发送的产品名称或价格任何值。</span><span class="sxs-lookup"><span data-stu-id="7e274-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="7e274-162">如果产品 ID 不是有效的它将违反外的键约束在数据库中，并插入将失败，它也应如此。</span><span class="sxs-lookup"><span data-stu-id="7e274-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="7e274-163">下面是完整`PostOrder`方法：</span><span class="sxs-lookup"><span data-stu-id="7e274-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="7e274-164">最后，添加**Authorize**到控制器属性：</span><span class="sxs-lookup"><span data-stu-id="7e274-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="7e274-165">现在只允许注册的用户可以创建或查看订单。</span><span class="sxs-lookup"><span data-stu-id="7e274-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e274-166">[上一页](using-web-api-with-entity-framework-part-5.md)
> [下一页](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="7e274-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
