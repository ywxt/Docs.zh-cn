---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 支持在 ASP.NET Web API 2 OData 操作 |Microsoft 文档
author: MikeWasson
description: 在 OData 中，操作是一种方法中添加不很容易定义为对实体的 CRUD 操作的服务器端行为。 操作的一些用途包括： 实现...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: acb369ca8f1bab8d7cad14c15f46cfd44beb9fdd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="c34e8-104">支持在 ASP.NET Web API 2 OData 操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-104">Supporting OData Actions in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="c34e8-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c34e8-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c34e8-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="c34e8-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="c34e8-107">在 OData 中，*操作*是一种方法中添加不很容易定义为对实体的 CRUD 操作的服务器端行为。</span><span class="sxs-lookup"><span data-stu-id="c34e8-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="c34e8-108">操作的一些用途包括：</span><span class="sxs-lookup"><span data-stu-id="c34e8-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="c34e8-109">实现复杂的事务处理。</span><span class="sxs-lookup"><span data-stu-id="c34e8-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="c34e8-110">同时对多个实体进行操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="c34e8-111">允许仅对某些属性的实体的更新。</span><span class="sxs-lookup"><span data-stu-id="c34e8-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="c34e8-112">将信息发送到服务器未在实体中定义。</span><span class="sxs-lookup"><span data-stu-id="c34e8-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c34e8-113">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="c34e8-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c34e8-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c34e8-114">Web API 2</span></span>
> - <span data-ttu-id="c34e8-115">OData 版本 3</span><span class="sxs-lookup"><span data-stu-id="c34e8-115">OData Version 3</span></span>
> - <span data-ttu-id="c34e8-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c34e8-116">Entity Framework 6</span></span>


## <a name="example-rating-a-product"></a><span data-ttu-id="c34e8-117">示例： 评级产品</span><span class="sxs-lookup"><span data-stu-id="c34e8-117">Example: Rating a Product</span></span>

<span data-ttu-id="c34e8-118">在此示例中，我们想要让用户速率产品，并为每个产品的平均级别，则公开。</span><span class="sxs-lookup"><span data-stu-id="c34e8-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="c34e8-119">在数据库中，我们将存储评级，与产品的列表。</span><span class="sxs-lookup"><span data-stu-id="c34e8-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="c34e8-120">下面是我们可能使用来表示实体框架中的级别的模型：</span><span class="sxs-lookup"><span data-stu-id="c34e8-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="c34e8-121">但是，我们不希望客户端为 POST`ProductRating`对象添加到"分级"收藏。</span><span class="sxs-lookup"><span data-stu-id="c34e8-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="c34e8-122">直观地说，分级是与产品集合中，关联，客户端应只需发布的分级值。</span><span class="sxs-lookup"><span data-stu-id="c34e8-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="c34e8-123">因此，而不是使用的普通 CRUD 操作，我们定义一个客户端可以调用的操作产品上。</span><span class="sxs-lookup"><span data-stu-id="c34e8-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="c34e8-124">在 OData 术语中，操作是*绑定*到产品实体。</span><span class="sxs-lookup"><span data-stu-id="c34e8-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="c34e8-125">操作在服务器上产生负面影响。</span><span class="sxs-lookup"><span data-stu-id="c34e8-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="c34e8-126">因此，它们会调用使用 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="c34e8-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="c34e8-127">操作可以具有参数和返回类型，所述的服务元数据。</span><span class="sxs-lookup"><span data-stu-id="c34e8-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="c34e8-128">客户端在请求正文中发送参数和服务器发送响应正文中返回的值。</span><span class="sxs-lookup"><span data-stu-id="c34e8-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="c34e8-129">若要调用的"速率产品"操作，客户端，将发送到 URI 如下所示的 POST:</span><span class="sxs-lookup"><span data-stu-id="c34e8-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="c34e8-130">POST 请求中的数据是只需产品级别：</span><span class="sxs-lookup"><span data-stu-id="c34e8-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="c34e8-131">声明实体数据模型中的操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="c34e8-132">在 Web API 配置中，将添加到实体数据模型 (EDM) 的操作：</span><span class="sxs-lookup"><span data-stu-id="c34e8-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="c34e8-133">此代码定义"RateProduct"为可以在产品实体执行一个操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="c34e8-134">它还声明了操作将**int**参数名为"分级"，并返回**int**值。</span><span class="sxs-lookup"><span data-stu-id="c34e8-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="c34e8-135">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="c34e8-135">Add the Action to the Controller</span></span>

<span data-ttu-id="c34e8-136">"RateProduct"操作绑定到产品实体中。</span><span class="sxs-lookup"><span data-stu-id="c34e8-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="c34e8-137">若要实现此操作，添加一个名为方法`RateProduct`到产品控制器：</span><span class="sxs-lookup"><span data-stu-id="c34e8-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="c34e8-138">请注意的方法名称匹配 EDM 中操作的名称。</span><span class="sxs-lookup"><span data-stu-id="c34e8-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="c34e8-139">该方法具有两个参数：</span><span class="sxs-lookup"><span data-stu-id="c34e8-139">The method has two parameters:</span></span>

- <span data-ttu-id="c34e8-140">*密钥*： 速率的产品密钥。</span><span class="sxs-lookup"><span data-stu-id="c34e8-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="c34e8-141">*参数*： 操作参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="c34e8-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="c34e8-142">如果你使用的默认路由约定，按键参数必须命名为"关键"。</span><span class="sxs-lookup"><span data-stu-id="c34e8-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="c34e8-143">还有一点需要包括 **[FromOdataUri]** 特性，如所示。</span><span class="sxs-lookup"><span data-stu-id="c34e8-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="c34e8-144">此特性告知 Web API，若要在分析请求 URI 中的键时使用 OData 语法规则。</span><span class="sxs-lookup"><span data-stu-id="c34e8-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="c34e8-145">使用*参数*字典，以获取操作参数：</span><span class="sxs-lookup"><span data-stu-id="c34e8-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="c34e8-146">如果客户端发送的操作参数中正确设置格式的值**ModelState.IsValid**为 true。</span><span class="sxs-lookup"><span data-stu-id="c34e8-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="c34e8-147">在这种情况下，你可以使用**ODataActionParameters**为了获取参数值的字典。</span><span class="sxs-lookup"><span data-stu-id="c34e8-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="c34e8-148">在此示例中，`RateProduct`操作采用一个名为"评级"的单个参数。</span><span class="sxs-lookup"><span data-stu-id="c34e8-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="c34e8-149">操作元数据</span><span class="sxs-lookup"><span data-stu-id="c34e8-149">Action Metadata</span></span>

<span data-ttu-id="c34e8-150">若要查看的服务元数据，将 GET 请求发送到 /odata/$ 元数据。</span><span class="sxs-lookup"><span data-stu-id="c34e8-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="c34e8-151">下面是声明的元数据的部分`RateProduct`操作：</span><span class="sxs-lookup"><span data-stu-id="c34e8-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="c34e8-152">**FunctionImport**元素声明的操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="c34e8-153">大多数字段都一目了然，但两个数据类型值得注意：</span><span class="sxs-lookup"><span data-stu-id="c34e8-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="c34e8-154">**IsBindable**意味着操作可以调用针对目标实体至少一些时间。</span><span class="sxs-lookup"><span data-stu-id="c34e8-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="c34e8-155">**IsAlwaysBindable**意味着始终可以针对目标实体调用的操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="c34e8-156">区别是，某些操作始终可供客户端，但其他操作可能依赖于该实体的状态。</span><span class="sxs-lookup"><span data-stu-id="c34e8-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="c34e8-157">例如，假设你定义的"购买"操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="c34e8-158">你仅可以购买的项时库存量。</span><span class="sxs-lookup"><span data-stu-id="c34e8-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="c34e8-159">如果该项是 stock 外，客户端不能调用该操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="c34e8-160">当定义 EDM，**操作**方法创建一个始终可绑定的操作：</span><span class="sxs-lookup"><span data-stu-id="c34e8-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="c34e8-161">我将讨论 not 的始终-可绑定的操作 (也称为*暂时性*操作) 本主题中更高版本。</span><span class="sxs-lookup"><span data-stu-id="c34e8-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="c34e8-162">调用操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-162">Invoking the Action</span></span>

<span data-ttu-id="c34e8-163">现在让我们看看客户端将如何调用此操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="c34e8-164">假设在客户端需要向产品具有 ID 2 的分级 = 4。</span><span class="sxs-lookup"><span data-stu-id="c34e8-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="c34e8-165">下面是一个示例请求消息，使用 JSON 格式的请求正文：</span><span class="sxs-lookup"><span data-stu-id="c34e8-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="c34e8-166">下面是响应消息：</span><span class="sxs-lookup"><span data-stu-id="c34e8-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="c34e8-167">绑定到实体集的操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="c34e8-168">在前面的示例中，操作绑定到单个实体： 客户端进行分级单个产品。</span><span class="sxs-lookup"><span data-stu-id="c34e8-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="c34e8-169">你还可以将操作绑定到实体的集合。</span><span class="sxs-lookup"><span data-stu-id="c34e8-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="c34e8-170">只需进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="c34e8-170">Just make the following changes:</span></span>

<span data-ttu-id="c34e8-171">在 EDM 中，将操作添加到实体的**集合**属性。</span><span class="sxs-lookup"><span data-stu-id="c34e8-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="c34e8-172">在控制器方法中，省略*密钥*参数。</span><span class="sxs-lookup"><span data-stu-id="c34e8-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="c34e8-173">现在客户端时，将调用产品的实体集上的操作：</span><span class="sxs-lookup"><span data-stu-id="c34e8-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="c34e8-174">使用集合参数的操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="c34e8-175">操作可以接受值的集合的参数。</span><span class="sxs-lookup"><span data-stu-id="c34e8-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="c34e8-176">在 EDM 中，使用**CollectionParameter&lt;T&gt;** 若要将参数声明。</span><span class="sxs-lookup"><span data-stu-id="c34e8-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="c34e8-177">这会将声明一个名为"分级"采用的集合参数**int**值。</span><span class="sxs-lookup"><span data-stu-id="c34e8-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="c34e8-178">在控制器方法中，你仍获取参数值**ODataActionParameters**对象，但现在的值是**ICollection&lt;int&gt;** 值：</span><span class="sxs-lookup"><span data-stu-id="c34e8-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="c34e8-179">暂时性的操作</span><span class="sxs-lookup"><span data-stu-id="c34e8-179">Transient Actions</span></span>

<span data-ttu-id="c34e8-180">在"RateProduct"示例中，用户可以始终对产品评估，因此操作将始终可用。</span><span class="sxs-lookup"><span data-stu-id="c34e8-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="c34e8-181">但某些操作依赖于该实体的状态。</span><span class="sxs-lookup"><span data-stu-id="c34e8-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="c34e8-182">例如，在视频租赁服务中，"签出"操作并不总是可用。</span><span class="sxs-lookup"><span data-stu-id="c34e8-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="c34e8-183">（它取决于一份该视频是否可用。）此类型的操作称为*暂时性*操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="c34e8-184">在服务元数据，暂时性操作具有**IsAlwaysBindable**等于 false。</span><span class="sxs-lookup"><span data-stu-id="c34e8-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="c34e8-185">即实际默认值，因此元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="c34e8-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="c34e8-186">此处为什么这很重要： 如果操作是暂时性的服务器需要告诉客户端操作时可用。</span><span class="sxs-lookup"><span data-stu-id="c34e8-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="c34e8-187">通过在实体中包括指向操作的执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c34e8-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="c34e8-188">下面是一个示例，用于电影实体：</span><span class="sxs-lookup"><span data-stu-id="c34e8-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="c34e8-189">"#CheckOut"属性包含到签出操作的链接。</span><span class="sxs-lookup"><span data-stu-id="c34e8-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="c34e8-190">如果操作不可用，服务器会忽略链接。</span><span class="sxs-lookup"><span data-stu-id="c34e8-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="c34e8-191">若要声明 EDM 中的暂时性操作，请调用**TransientAction**方法：</span><span class="sxs-lookup"><span data-stu-id="c34e8-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="c34e8-192">此外，你必须提供一个函数，返回为给定实体的操作链接。</span><span class="sxs-lookup"><span data-stu-id="c34e8-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="c34e8-193">设置此函数通过调用**HasActionLink**。</span><span class="sxs-lookup"><span data-stu-id="c34e8-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="c34e8-194">您可以编写函数作为 lambda 表达式：</span><span class="sxs-lookup"><span data-stu-id="c34e8-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="c34e8-195">可用的操作，如果 lambda 表达式将返回到操作的链接。</span><span class="sxs-lookup"><span data-stu-id="c34e8-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="c34e8-196">OData 序列化程序包括此链接时其序列化实体。</span><span class="sxs-lookup"><span data-stu-id="c34e8-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="c34e8-197">当操作不可用时，函数将返回`null`。</span><span class="sxs-lookup"><span data-stu-id="c34e8-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c34e8-198">其他资源</span><span class="sxs-lookup"><span data-stu-id="c34e8-198">Additional Resources</span></span>

[<span data-ttu-id="c34e8-199">OData 操作示例</span><span class="sxs-lookup"><span data-stu-id="c34e8-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
